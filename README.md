# 🌌 N-Body Gravity Ultimate

> **Experience the cosmos at your fingertips.** A high-performance, interactive gravity simulator that brings the beauty and chaos of celestial mechanics to your browser.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Physics](https://img.shields.io/badge/physics-Newtonian-green.svg)
![Performance](https://img.shields.io/badge/optimization-Octree-orange.svg)

---

## ✨ What Is This?

**N-Body Gravity Ultimate** is a real-time gravitational physics simulator that lets you create, manipulate, and watch entire universes unfold. From spiral galaxies to solar systems, from chaotic collisions to elegant orbital dances—witness the fundamental force that shapes our cosmos.

Built with cutting-edge **Barnes-Hut Octree optimization**, this simulator can handle hundreds of bodies simultaneously while maintaining smooth, responsive performance.

---

## 🚀 Features

### 🌟 Pre-built Universe Templates
- **Spiral Galaxy** - Watch majestic spiral arms form and evolve
- **Elliptical Galaxy** - Witness the elegant chaos of elliptical formations
- **Milky Way** - Our home galaxy with realistic 4-arm spiral structure
- **Andromeda** - The approaching neighbor with its distinctive 2-arm design
- **Solar System** - Explore our cosmic backyard with orbital mechanics
- **Black Holes** - Create gravitational singularities that bend spacetime itself

### 🎮 Interactive Physics Playground
- **Drag & Launch** - Click and drag to fling bodies into orbit
- **Mass Control** - Adjust the mass of spawned objects
- **Velocity Control** - Fine-tune simulation speed
- **Collision Physics** - Bodies merge realistically, conserving momentum
- **Explosion Effects** - Watch massive bodies go supernova

### 🎨 Visual Spectacular
- **Comet Tails** - Fast-moving objects leave glowing trails
- **Orbital Paths** - Visualize elliptical orbits around parent bodies
- **Sun Glow Effects** - Stellar objects radiate realistic halos
- **Particle Systems** - Collisions create beautiful sparkle effects
- **Trail Rendering** - Toggle orbital history visualization

### 🔬 Advanced Physics Modes
- **Dark Matter** - Enable mysterious cosmic web forces
- **Repulsor Mode** - Create anti-gravity objects that push instead of pull
- **3D Mode** - Full three-dimensional simulation with camera controls
- **Focus Tracking** - Follow the largest body automatically

### 💾 Persistence
- **Save Galaxies** - Store your creations in browser storage
- **Load Galaxies** - Resume where you left off
- **Multiple Saves** - Manage unlimited universe snapshots

---

## 🎯 Quick Start

### Just Want to Play?
1. Open `index.html` in any modern browser
2. Click **"Spiral Galaxy"** to spawn a beautiful galaxy
3. Click and drag anywhere to add new bodies
4. Watch the gravitational ballet unfold

### Want to Create?
1. Adjust **Mass** slider for heavier objects
2. Hold and drag to set velocity vectors
3. Enable **Repulsor** for anti-gravity chaos
4. Save your masterpiece with the **Save** button

---

## 🎮 Controls

### Mouse Controls
| Action | Effect |
|--------|--------|
| **Click & Drag** | Create new body with velocity |
| **Mouse Wheel** | Zoom in/out |
| **3D Mode Drag** | Rotate camera |

### Keyboard Controls (3D Mode)
| Keys | Action |
|------|--------|
| **W/S** | Move forward/backward |
| **A/D** | Strafe left/right |
| **Q/E** | Move up/down |
| **Space** | Pause/Play |

### UI Buttons
| Button | Function |
|--------|----------|
| **Pause** | Freeze time |
| **Clear** | Reset universe |
| **Focus Largest** | Track most massive body |
| **Repulsor: OFF** | Toggle anti-gravity mode |
| **Dark Matter: OFF** | Enable cosmic web forces |
| **3D: OFF** | Switch to 3D mode |
| **Trail: ON** | Toggle orbital trails |
| **Black Hole** | Spawn gravitational singularity |

---

## 🧮 The Physics

### Gravitational Force
```
F = G · (m₁ · m₂) / r²
```

Where:
- **F** = Gravitational force
- **G** = Gravitational constant (50 in simulation units)
- **m₁, m₂** = Masses of interacting bodies
- **r** = Distance between centers

### Barnes-Hut Octree Algorithm
For N bodies, naive computation is **O(N²)**. This simulator uses the Barnes-Hut algorithm to reduce complexity to **O(N log N)** by:
1. Dividing 3D space into octants recursively
2. Grouping distant bodies into clusters
3. Treating distant clusters as single massive bodies
4. Achieving 85-95% accuracy with 10x+ performance

**Theta parameter**: 0.5 (configurable in code)
- Lower = more accurate, slower
- Higher = faster, less accurate

### Collision Detection
Bodies merge when their radii overlap:
```javascript
newMass = m₁ + m₂
newVelocity = (m₁·v₁ + m₂·v₂) / (m₁ + m₂)
newPosition = (m₁·p₁ + m₂·p₂) / (m₁ + m₂)
```

Conservation of momentum ensures realistic interactions.

---

## 🏗️ Technical Architecture

### Performance Optimizations
- **Octree Spatial Partitioning** - O(N log N) force calculations
- **Adaptive Time Stepping** - Prevents simulation instabilities
- **Smart Trail Management** - Fixed-size trail buffers (100 points)
- **Depth Sorting** - Correct 3D rendering order
- **Canvas Rendering** - Hardware-accelerated 2D context

### Code Structure
```
├── Body Class
│   ├── Position & Velocity (3D)
│   ├── Physics Integration
│   ├── Trail Management
│   ├── Comet Tail Effects
│   └── Orbital Path Calculation
│
├── BlackHole Class (extends Body)
│   ├── Static Position
│   └── Accretion Disk Rendering
│
├── OctreeNode Class
│   ├── Recursive Subdivision
│   ├── Center of Mass Calculation
│   └── Force Approximation
│
├── Galaxy Templates
│   ├── Spiral (logarithmic arms)
│   ├── Elliptical (3D distribution)
│   ├── Milky Way (4-arm spiral)
│   └── Andromeda (2-arm spiral)
│
└── Rendering Pipeline
    ├── Orbital Paths (dashed)
    ├── Comet Tails (gradient)
    ├── Trails (faded)
    ├── Body Circles
    └── Particle Effects
```

---

## 🎨 Customization

### Modify Physics Constants
```javascript
// Line 18: Gravitational constant
const G = 50; // Increase for stronger gravity

// Line 446: Octree precision
const force = rootNode.calculateForce(b, 0.5);
                                         // ↑ Theta value
                                         // Lower = more accurate
```

### Add Your Own Galaxy Template
```javascript
function generateMyGalaxy(n = 300) {
    bodies = [];
    const cx = W/2, cy = H/2;
    
    // Create central body
    const center = new Body(cx, cy, 0, 0, 0, 0, 200, '#fff', 1);
    bodies.push(center);
    
    // Add orbiting bodies
    for (let i = 0; i < n; i++) {
        // Your custom distribution logic here
        const x = cx + /* your X calculation */;
        const y = cy + /* your Y calculation */;
        const vx = /* your velocity X */;
        const vy = /* your velocity Y */;
        
        bodies.push(new Body(x, y, 0, vx, vy, 0, mass, color, 1));
    }
    
    updateInfo();
}
```

### Change Visual Style
```css
/* Lines 8-9: Background and accent colors */
body {
    background: #000; /* Change to #001 for deep blue */
    color: #0ff;      /* Change accent color */
}

/* Lines 18-30: Button styling */
.btn {
    background: rgba(0,255,255,0.2);
    border: 2px solid #0ff;
    /* Customize to your theme */
}
```

---

## 🌟 Example Scenarios

### Create a Binary Star System
1. Click **Clear**
2. Set **Mass** to 50
3. Drag from left → right to create first star
4. Drag from right → left to create second star
5. Watch them orbit their common center of mass

### Galactic Collision
1. Click **Milky Way**
2. Click **Save** → "Milky Way"
3. Click **Andromeda**
4. Click **3D** and adjust view
5. Give one galaxy lateral velocity by dragging
6. Watch the merger over thousands of years

### Black Hole Accretion
1. Click **Spiral Galaxy**
2. Click **Black Hole** at the center
3. Enable **Focus Largest**
4. Watch stars spiral into oblivion

### Chaos Mode
1. Enable **Repulsor**
2. Increase **Mass** to maximum
3. Rapidly click around the screen
4. Enable **Dark Matter** for extra chaos
5. Enjoy the cosmic fireworks

---

## 🧪 Educational Value

This simulator demonstrates:
- **Newtonian Mechanics** - F = ma in action
- **Orbital Dynamics** - Kepler's laws emerge naturally
- **Conservation Laws** - Momentum and energy conservation
- **N-Body Problem** - Why 3+ bodies create chaos
- **Computational Physics** - How scientists simulate galaxies
- **Algorithm Optimization** - Barnes-Hut tree methods

Perfect for:
- Physics students visualizing gravitational concepts
- Astronomy enthusiasts exploring celestial mechanics
- Programmers learning spatial algorithms
- Anyone fascinated by the cosmos

---

## 🐛 Known Limitations

- **Collision Detection**: O(N²) - can slow down with 500+ bodies
- **Energy Loss**: Numerical integration causes slight energy drift over time
- **Relativistic Effects**: Not simulated (pure Newtonian physics)
- **Tidal Forces**: Bodies treated as point masses
- **Browser Storage**: Save files limited by localStorage quota

---

## 🔮 Future Enhancements

Potential additions:
- [ ] WebGL renderer for 1000+ body simulations
- [ ] Gravitational wave visualization
- [ ] N-body choreography finder
- [ ] Export to video/GIF
- [ ] Relativistic corrections
- [ ] Roche limit calculations
- [ ] Lagrange point visualization
- [ ] Multi-threading with Web Workers
- [ ] VR mode support

---

## 🎓 Learning Resources

Want to understand the math behind this?

**Gravity & Orbits:**
- [Newton's Law of Universal Gravitation](https://en.wikipedia.org/wiki/Newton%27s_law_of_universal_gravitation)
- [Orbital Mechanics](https://en.wikipedia.org/wiki/Orbital_mechanics)
- [The Three-Body Problem](https://en.wikipedia.org/wiki/Three-body_problem)

**Algorithms:**
- [Barnes-Hut Algorithm](https://en.wikipedia.org/wiki/Barnes%E2%80%93Hut_simulation)
- [Octree Data Structure](https://en.wikipedia.org/wiki/Octree)
- [Verlet Integration](https://en.wikipedia.org/wiki/Verlet_integration)

**Astrophysics:**
- [Galaxy Formation](https://en.wikipedia.org/wiki/Galaxy_formation_and_evolution)
- [Dark Matter](https://en.wikipedia.org/wiki/Dark_matter)
- [Black Holes](https://en.wikipedia.org/wiki/Black_hole)

---

## 💡 Tips & Tricks

1. **Performance**: Limit bodies to ~300 for smooth 60fps
2. **Stable Orbits**: Use galaxy templates as starting points
3. **Close Approaches**: Slow down time to watch gravitational slingshots
4. **3D Exploration**: Combine WASD movement with mouse rotation
5. **Artistic Creations**: Toggle trails and adjust colors for screenshots
6. **Save Often**: Complex systems can be hard to recreate

---

## 🤝 Contributing

Found a bug? Have an idea? Want to add a feature?

This is a single-file HTML project, making it easy to modify:
1. Fork or download the HTML file
2. Make your changes
3. Test in your browser
4. Share your enhanced version!

---

## 📜 License

This project is open source and available for educational and personal use.

**Based on Newtonian physics** - Thank you, Sir Isaac Newton (1643-1727)

**Octree algorithm** - Inspired by Barnes & Hut (1986)

---

## 🌌 Final Thoughts

> *"The universe is under no obligation to make sense to you."* - Neil deGrasse Tyson

But that doesn't mean we can't try to understand it. This simulator is a tiny window into the gravitational forces that shaped our cosmos—from the birth of galaxies to the orbits that make life on Earth possible.

Whether you're here to learn, create, or simply marvel at the beauty of physics in motion, I hope this tool inspires wonder and curiosity about the universe we inhabit.

**Now go forth and create universes.** 🚀

---

*Made with gravity and code* ⚛️
