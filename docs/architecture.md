# Cabineo - Complete Architecture Document

## Project Overview

**Project Name:** Cabineo (Cabinet + Neo)
**Goal:** 3D furniture configurator built with React, TypeScript, and Three.js for portfolio showcase
**Target:** Learn Three.js, enhance React/TS skills, impress potential employers

### Scope Definition
- **Single Focus:** Side cabinet configurator
- **Core Features:** 
  - Edit dimensions (width, height, depth)
  - Configure 1-3 bays
  - Toggle doors per bay (with/without)
  - Select shelf count per bay (0-3)
  - Choose materials for carcase and doors separately

### UI Layout
- **Split-screen interface:** Left panel (controls) + Right panel (3D scene)
- **Left panel tabs:** Design | BOM | URL
- **3D scene:** Slowly spinning cabinet with real-time updates

---

## Architecture Decisions (Locked ✅)

### 1. Coordinate System ✅
```
X = Width (left to right)
Y = Height (bottom to top) - Three.js standard
Z = Depth (front to back)
```
- Cabinet faces forward toward camera
- Avoids CAD vs Three.js conversion issues

### 2. Hardware System ✅
**Construction Method:** Cam and dowel fittings
**Base Hardware:**
- 8 cam bolts + 8 wood dowels for main carcase
- 4 cam bolts + 4 wood dowels per internal divider

**Door Hardware Logic:**
- Hinges: 2 per door if height < 900mm, 3 per door if height ≥ 900mm
- Shelf pins: 4 per shelf
- Door handles: 1 per door

### 3. 3D Geometry Generation ✅
**Approach:** Code-generated geometry using Three.js BoxGeometry
- **Why:** Parametric design requires real-time geometry updates
- **Method:** BoxGeometry + mathematical positioning
- **Performance:** Simple regeneration (rebuild entire cabinet on config change)

### 4. State Management ✅
**Approach:** Sliced Zustand stores
```typescript
// Separate stores for different concerns
useCabinetStore    // Cabinet configuration
useMaterialStore   // Material selection and library
useUIStore         // Active tab, UI state
```
**Benefits:** Prevents unnecessary re-renders, clean separation of concerns

### 5. Material System ✅
**Approach:** PBR materials with texture library
- **Format:** Complete PBR texture sets (diffuse + normal + roughness)
- **Source:** Existing professional texture library
- **Implementation:** Three.js MeshStandardMaterial with texture maps
- **Grain Direction:** ⏳ Pending design research

### 6. Scene Setup & Lighting ✅
**Lighting:** HDRI environment lighting
- **Why:** Professional furniture rendering standard
- **Benefits:** Realistic reflections, proper PBR material response
- **Implementation:** RGBELoader with EquirectangularReflectionMapping

### 7. Camera & Interaction ✅
**Approach:** Hybrid auto-rotation + user controls
- **Default:** Slow auto-rotation (showcases design)
- **User Interaction:** Manual orbit controls when user interacts
- **Return:** Auto-rotation resumes after 3 seconds of inactivity

### 8. Performance Strategy ✅
**Approach:** Simple geometry regeneration
- **Reasoning:** Cabinet complexity (~10-18 box geometries) is trivial for modern browsers
- **Focus:** Prioritize visual quality over premature optimization

---

## Technical Stack

### Core Dependencies
```json
{
  "react": "18.3.1",
  "react-dom": "18.3.1",
  "typescript": "5.5.4",
  "three": "0.166.1",
  "@react-three/fiber": "8.15.12",
  "zustand": "4.5.2",
  "tailwindcss": "3.4.7",
  "lucide-react": "0.295.0",
  "@tanstack/react-table": "8.11.0",
  "zod": "3.23.8"
}
```

### Development Tools
```json
{
  "@biomejs/biome": "1.7.0",
  "husky": "9.1.3",
  "vite": "5.4.6",
  "vite-tsconfig-paths": "4.3.1"
}
```

### Build Setup
- **Framework:** React 18 + Vite
- **Styling:** Tailwind CSS
- **Linting:** Biome (formatting + linting + import sorting)
- **Pre-commit:** Husky with Biome checks
- **Validation:** Zod for runtime type safety

---

## File Structure

```
cabineo/
├── public/
│   ├── textures/
│   │   ├── carcase/
│   │   │   ├── white-melamine/
│   │   │   │   ├── diffuse.jpg
│   │   │   │   ├── normal.jpg
│   │   │   │   └── roughness.jpg
│   │   │   └── oak-veneer/
│   │   └── doors/
│   ├── hdri/
│   │   └── studio.hdr
│   └── index.html
├── src/
│   ├── components/
│   │   ├── ui/                 # Reusable UI components
│   │   │   ├── Tabs.tsx
│   │   │   ├── Button.tsx
│   │   │   ├── Slider.tsx
│   │   │   └── MaterialSwatch.tsx
│   │   ├── panels/             # Tab panel components
│   │   │   ├── DesignPanel.tsx
│   │   │   ├── BOMPanel.tsx
│   │   │   └── URLPanel.tsx
│   │   ├── scene/              # Three.js React components
│   │   │   ├── Scene3D.tsx
│   │   │   ├── Cabinet.tsx
│   │   │   ├── Environment.tsx
│   │   │   └── Controls.tsx
│   │   └── layout/             # Layout components
│   │       ├── SplitView.tsx
│   │       └── LeftPanel.tsx
│   ├── stores/                 # Zustand state management
│   │   ├── cabinetStore.ts
│   │   ├── materialStore.ts
│   │   └── uiStore.ts
│   ├── types/                  # TypeScript interfaces
│   │   ├── cabinet.ts
││   ├── materials.ts
│   │   └── bom.ts
│   ├── lib/                    # Business logic (no React/UI)
│   │   ├── geometry/           # 3D geometry generation
│   │   │   ├── cabinetGenerator.ts
│   │   │   ├── shelfGenerator.ts
│   │   │   └── doorGenerator.ts
│   │   ├── materials/          # Material and texture logic
│   │   │   ├── materialLoader.ts
│   │   │   └── grainDirection.ts
│   │   ├── bom/                # Bill of materials logic
│   │   │   ├── bomGenerator.ts
│   │   │   └── pricing.ts
│   │   └── utils/              # Shared utilities
│   │       ├── math.ts
│   │       └── constants.ts
│   ├── data/                   # Static configuration
│   │   ├── materials.json
│   │   └── pricing.json
│   ├── App.tsx
│   ├── main.tsx
│   └── index.css
├── package.json
├── tsconfig.json
├── vite.config.ts
├── tailwind.config.js
├── biome.json
└── README.md
```

---

## Data Types (Draft)

### Cabinet Configuration
```typescript
interface CabinetConfig {
  dimensions: {
    widthX: number;   // mm
    heightY: number;  // mm
    depthZ: number;   // mm
  };
  bays: {
    count: 1 | 2 | 3;
    configs: BayConfig[];
  };
  materials: {
    carcase: MaterialId;
    doors: MaterialId;
  };
}

interface BayConfig {
  hasDoor: boolean;
  shelfCount: 0 | 1 | 2 | 3;
}
```

### PBR Material System
```typescript
interface PBRMaterial {
  id: string;
  name: string;
  type: 'carcase' | 'door';
  textures: {
    diffuse: string;     # Base color/wood grain
    normal: string;      # Surface bump detail  
    roughness: string;   # Matte vs glossy finish
  };
  properties: {
    roughnessValue: number; # 0.0-1.0
    metallicValue: number;  # Usually 0.0 for wood
  };
}
```

### BOM Structure
```typescript
interface BOMItem {
  id: string;
  name: string;
  category: 'material' | 'hardware';
  quantity: number;
  unit: string;
  unitPrice: number;
  totalPrice: number;
  material?: string;
  dimensions?: string;
}
```

---

## BOM System Design

### Materials Sub-tab
- Panel breakdown with dimensions
- Material assignments
- Quantity calculations
- Area/volume totals

### Hardware Sub-tab  
- Cam bolts and dowels (8+8 base, 4+4 per divider)
- Hinges (2 or 3 per door based on height)
- Shelf pins (4 per shelf)
- Door handles
- Pricing with totals

---

## Pending Decisions

### ⏳ Grain Direction Rules
**Status:** Awaiting design research
**Impact:** Texture rotation logic for different cabinet panels
**Research Needed:** 
- Vertical vs horizontal panel grain orientation
- Door grain direction standards
- Shelf and divider grain rules

---

## Implementation Philosophy

### Code Quality Standards
- **Type Safety:** Zod validation + TypeScript
- **Separation of Concerns:** UI components contain no business logic
- **Performance:** Simple solutions first, optimize only when needed
- **Maintainability:** Clear folder structure and naming conventions

### Professional GitHub Practices
- **Branching:** Feature branches from develop
- **Issues:** GitHub Issues for all features
- **Commits:** Conventional commit messages (feat/fix/docs/chore)
- **Documentation:** Comprehensive README with setup instructions

---

## Success Criteria

### Technical Learning Goals
- ✅ Master Three.js fundamentals through real project
- ✅ Advanced React patterns with complex state
- ✅ Professional TypeScript practices
- ✅ Modern build tooling and development workflow

### Portfolio Impact
- ✅ Unique domain expertise (furniture + web development)
- ✅ Visually impressive 3D experience
- ✅ Professional code quality and documentation
- ✅ Real-world application complexity

### Timeline
- **Target:** 10 weeks development
- **Commitment:** 4-5 hours/day, 5 days/week
- **Approach:** Iterative development with weekly milestones

