3D GitHub Repository Visualizer Implementation Plan
A high-performance interactive 3D web application to visualize any public GitHub repository as an interactive 3D scene (Code City & Branch Graph) powered by Three.js and the GitHub REST API.

1. Overview & Architecture
The application will transform GitHub repository file trees, branches, and commit histories into dynamic 3D structures:

Files & Folders: Visualized as 3D extruded blocks/buildings (height scaled to file size/lines, position structured by folder hierarchy).
Branches: Connecting 3D paths / glowing splines connecting branch roots and commit nodes.
Commits: Glowing, animated 3D spheres positioned along branch paths with pulse animations.
Activity & Heatmap Colors:
🟢 Neon Green: Active / frequently modified files
🔵 Cyan Blue: Stable / foundational files
🔴 Hot Crimson: Recently modified / high activity files
Modes: Code City layout, 3D Force-Graph/Tree view, and Commit Timeline view.
Bonus Capabilities: 3D scene export as .GLTF, deep-linking via query parameters (?repo=owner/repo), optional GitHub Personal Access Token support to bypass public API rate limits, and fallback mock repository generator for offline testing or instant preview.
2. Directory & File Structure
Project location: C:\Users\wisal\.gemini\antigravity\scratch\repo-visualizer-3d


repo-visualizer-3d/
├── index.html                  # Main HTML shell with sleek HUD overlay & canvas wrapper
├── package.json                # Project dependencies (three, three-stdlib, lucide, vite)
├── vite.config.js              # Vite configuration
├── public/
│   └── favicon.svg             # App favicon
└── src/
    ├── main.js                 # Application entry point & controller initialization
    ├── style.css               # Design system, glassmorphism UI, neon cyberpunk dark/light themes
    ├── services/
    │   └── github.js           # GitHub API client (REST API + Rate limit handling + Mock repo fallback)
    ├── scene/
    │   ├── engine.js           # Three.js scene, renderer, camera, lighting, environment, animations
    │   ├── cityLayout.js       # Procedural 3D Code City layout generator (buildings & districts)
    │   ├── graphLayout.js      # 3D Branch & Commit graph renderer (splines & glowing spheres)
    │   ├── interaction.js      # Raycasting, hover tooltips, click selection, camera target transitions
    │   └── exporter.js         # GLTFExporter integration for downloading 3D scene files
    └── ui/
        ├── hud.js              # Top bar, preset selector, search input, stats overlay, legend
        ├── inspector.js        # File detail sidebar & commit inspector
        └── toast.js            # Toast notifications for export and sharing links
3. Implementation Steps
Phase 1: Project Setup & Core Environment
Initialize Vite + Vanilla JS application in C:\Users\wisal\.gemini\antigravity\scratch\repo-visualizer-3d.
Install three, three-stdlib (for OrbitControls and GLTFExporter), and lucide icons.
Setup CSS design system with CSS custom properties (Cyberpunk dark background #0b0f19, neon green #00ff9d, cyan #00f0ff, crimson #ff0055, glassmorphic HUD overlays).
Phase 2: GitHub API Service & Data Processing
Build github.js to fetch:
Repository metadata (GET /repos/{owner}/{repo}).
Recursive Git file tree (GET /repos/{owner}/{repo}/git/trees/{branch}?recursive=1).
Branch list (GET /repos/{owner}/{repo}/branches).
Recent commit history (GET /repos/{owner}/{repo}/commits).
Implement rate-limit indicator & local storage GitHub Token option.
Include a built-in mock repository generator (e.g. standard project structures) for immediate instant loading and rate-limit resilience.
Phase 3: 3D Scene Engine & Layout Algorithms
Base Engine (engine.js):
Three.js WebGLRenderer with anti-aliasing, shadow mapping, and bloom-ready lighting setup.
Interactive OrbitControls with smooth damping and camera movement tweening.
Futuristic particle environment grid and ambient lighting.
Code City Layout (cityLayout.js):
Converts folder trees into spatial bounding areas (districts) and files into 3D box meshes.
Height determined by file size; color mapped to recency/type; emissive neon edge highlights.
Branch & Commit Graph Layout (graphLayout.js):
Draws 3D CatmullRom splines for git branches.
Places glowing SphereGeometry nodes with pulse animation for commit history points.
Phase 4: Interactions, Tooltips & Inspector
Raycaster on canvas to detect hovered/clicked 3D buildings or commit spheres.
Hover tooltip display: File path, file size (KB), language extension, last commit date/author.
Click to inspect: Smoothly animate camera target to the building/node and open the right Inspector sidebar with full details and direct GitHub link.
Phase 5: Features & UI Polish (Bonus Features)
Preset Repo Quick Selectors (facebook/react, vuejs/core, mrdoob/three.js, torvalds/linux).
GLTF Exporter: Download current 3D visual scene as .gltf file for Blender / 3D software.
Share Link: Encodes repo name in URL #repo=owner/repo or query string for direct sharing.
Theme Switcher: Dark Neon mode (default) and Light Mode.
Responsive legend HUD explaining shapes, colors, and layout metrics.
4. Verification Plan
Automated & Build Verification
Run npm run build to verify clean compilation with no bundle or syntax errors.
Run npm run dev to start dev server locally and verify responsiveness.
Functional Verification
Repository Loading: Input facebook/react or custom repo -> verify API call, tree parse, and 3D rendering.
3D Navigation: Pan, zoom, rotate using OrbitControls; verify performance at 60 FPS.
Hover & Click: Hover over buildings -> check tooltip; Click building -> check smooth camera transition and inspector panel.
GLTF Export: Click "Export .GLTF" -> verify .gltf file download.
Share Link: Click "Share" -> copy link and load in new tab -> verify auto-loading of shared repository.
