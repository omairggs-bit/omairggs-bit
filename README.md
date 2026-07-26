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
