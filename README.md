# ThreatForge 🚀

## Overview

ThreatForge is a cutting-edge game engine that simulates modern global threats through **component-based emergent behaviors**. Instead of pre-defined threats, you compose complex scenarios from atomic behavioral components that interact to create unpredictable, realistic outcomes with **dynamically adjustable performance** to run on everything from mobile devices to high-end gaming systems.

### What Makes ThreatForge Unique

Traditional threat simulations use rigid, pre-defined threats. ThreatForge revolutionizes this approach by implementing a **component-based architecture** where complex threats **emerge naturally** from simple, atomic components interacting across multiple domains, with **adaptive performance** that scales to your hardware.

## 🎯 Quick Start (2 Minutes)

```bash
# Clone and setup
git clone https://github.com/threatforge/engine.git
cd engine
npm install

# Start development server
npm run dev
# Open http://localhost:5173
```

```typescript
// Your first emergent threat with adaptive performance
import { GameEngine } from '@threatforge/core'

const engine = new GameEngine({
  performance: {
    quality: 'adaptive',  // Auto-adjusts to your hardware
    targetFPS: 60,
    detailLevel: 'auto'
  }
})

const pandemic = engine.composeThreat([
  { type: 'AIRBORNE_TRANSMISSION', properties: { range: 1000 } },
  { type: 'MUTATION_ENGINE', properties: { rate: 0.001 } }
])

console.log(`Created threat with ${pandemic.emergentBehaviors.length} emergent behaviors`)
console.log(`Running at ${pandemic.performanceMetrics.currentFPS} FPS`)
```

## 🧩 Core Concepts

### Component-Based Architecture

Threats are **composed** from atomic behavioral components, not hardcoded:

```typescript
// Traditional approach (rigid, limited)
const covid = new PredefinedThreat('COVID_VARIANT')

// ThreatForge approach (flexible, emergent, performance-aware)
const covid = new ThreatComposer({
  performance: {
    quality: 'balanced',
    maxEmergentBehaviors: 50
  }
})
  .addComponent('AIRBORNE_TRANSMISSION', { range: 1000 })
  .addComponent('MUTATION_ENGINE', { rate: 0.001 })
  .addComponent('SEASONAL_VARIATION', { amplitude: 0.3 })
  .compose() // Emergent behaviors discovered automatically
```

### Cross-Domain Interactions

Components from different domains create **unexpected synergies**:

- **Cyber + Biological**: AI-generated pathogens with network propagation
- **Quantum + Information**: Quantum-entangled disinformation campaigns
- **Environmental + Robotic**: Climate-triggered autonomous system failures
- **Radiological + Cognitive**: Radiation-induced behavioral modification

### Emergent Complexity

Simple components combine to create **unpredictable outcomes**:

```typescript
// Individual components are simple...
const quantum = { coherence: 0.8, range: 500 }
const bio = { transmission: 0.6, mutation: 0.01 }

// ...but their interactions create complex behaviors
const hybrid = compose(quantum, bio, {
  performance: 'adaptive',
  complexity: 'high'
})
// Results in: Quantum-accelerated viral evolution
//            Predictive variant generation
//            Coherence-dependent infectivity
//            Performance automatically optimized
```

## 🎮 Key Features

### Component-Based Threat Composition
- **50+ Atomic Components**: Transmission, effects, evolution, and special behaviors
- **Dynamic Runtime Assembly**: Threats composed at runtime from component libraries
- **Emergent Interactions**: Unexpected behaviors arise from component combinations
- **Cross-Domain Synergy**: Natural interactions between cyber, bio, quantum, and other domains
- **Performance Scaling**: Automatically adjusts complexity based on hardware capabilities

### Unified 3D Visualization
- **WebGL/WebGPU Rendering**: High-performance 3D globe with dynamic data layers
- **Contextual Visualization**: Heatmaps, vector fields, particle systems
- **Adaptive Quality**: 5-tier quality system from minimal to ultra detail
- **Special Effects**: Quantum interference, radiological glow, swarm behaviors
- **Performance Optimization**: Automatic LOD and culling based on hardware

### Adaptive Performance System
- **Hardware Detection**: Automatically detects device capabilities
- **Dynamic Quality Adjustment**: Real-time performance optimization
- **Configurable Detail Levels**: User-controlled quality vs performance trade-offs
- **Mobile Optimization**: Special modes for battery and thermal management
- **Progressive Enhancement**: Features gracefully scale with hardware

### Asymmetric Faction System
- **8 Unique Factions**: Each with distinct capabilities and win conditions
- **Specialized Roles**: Technocrat, Mitigator, Nation-State, Resistance, and more
- **Cross-Domain Capabilities**: Quantum operations, radiological containment, robotic command
- **Dynamic Alliances**: Shifting diplomatic relationships and betrayals
- **Performance-Balanced**: Faction abilities scale with system performance

### Educational Integration
- **Real-World Parallels**: Historical comparison system with actual events
- **Interactive Learning**: Context-sensitive tutorials and scenario-based education
- **Physics Validation**: Real-world vs simulated propagation models
- **Learning Analytics**: Track educational progress and understanding
- **Accessibility**: Multiple difficulty and complexity levels

### Development Tools
- **Runtime Inspector**: Real-time entity and state inspection
- **Time Control**: Pause, slow-motion, fast-forward for analysis
- **Component Laboratory**: Experiment with component combinations
- **Performance Profiling**: Detailed performance metrics and optimization suggestions
- **Quality Configuration**: Adjust visualization and simulation quality on-the-fly

## 🛠️ Installation Options

### Option 1: Progressive Web App (Recommended)
```bash
npm run build
# Serve the dist/ folder
# Visit in browser and click "Install" when prompted
# Launch from home screen for native-like experience
```

### Option 2: Desktop Application
```bash
npm run build:desktop
# Creates standalone executable
# No browser required, full offline capability
```

### Option 3: Development Mode
```bash
npm run dev
# Access development tools at http://localhost:5173/dev
# Real-time component inspection
# Performance profiling
# Emergent behavior visualization
```

## 🎯 Your First Emergent Threat

```typescript
import { GameEngine, ComponentType } from '@threatforge/core'

// Initialize the engine with performance settings
const engine = new GameEngine({
  canvas: document.getElementById('canvas'),
  enableDevTools: true,
  performance: {
    quality: 'adaptive',
    targetFPS: 60,
    detailLevel: 'auto'
  }
})

// Create a quantum-biological pandemic with cognitive manipulation
const hybridPandemic = engine.composeThreat([
  {
    type: ComponentType.QUANTUM_ENTANGLEMENT,
    properties: {
      coherenceTime: 2000,
      entanglementStrength: 0.8
    }
  },
  {
    type: ComponentType.BIOLOGICAL_INFECTION,
    properties: {
      transmissionRate: 0.7,
      incubationPeriod: 5,
      mutationPotential: 0.4
    }
  },
  {
    type: ComponentType.COGNITIVE_MANIPULATION,
    properties: {
      influenceStrength: 0.9,
      stealthLevel: 0.8
    }
  }
])

console.log(`🧬 Created hybrid pandemic with ${hybridPandemic.emergentBehaviors.length} emergent behaviors:`)
hybridPandemic.emergentBehaviors.forEach(behavior => {
  console.log(`  - ${behavior.name}: ${behavior.description}`)
})

console.log(`⚡ Performance: ${hybridPandemic.performanceMetrics.currentFPS} FPS`)
console.log(`🔧 Quality: ${hybridPandemic.qualitySettings.renderQuality}`)
```

## 🏗️ Architecture Overview

### Technology Stack
- **Frontend**: HTML5, TypeScript, WebGL/WebGPU
- **3D Rendering**: Three.js with advanced shaders
- **Physics**: Custom Newtonian mechanics with Web Workers
- **State Management**: Component-based composition
- **Build Tools**: Vite, TypeScript, ESLint, Prettier
- **Testing**: Playwright, Jest, Custom framework

### Core Architecture Patterns
- **Component Composition**: Atomic components compose into complex threats
- **Event-Driven**: Pub/Sub pattern for decoupled communication
- **Plugin System**: JSON manifests with lifecycle hooks
- **Emergent Design**: Behaviors emerge from component interactions
- **Cross-Domain Integration**: Natural interaction between threat domains
- **Adaptive Performance**: Quality scales with hardware capabilities

### Performance Targets (Configurable)
- **Frame Rate**: 30-120 FPS based on user preference and hardware
- **Entity Count**: 500-10,000+ composed threats based on complexity settings
- **Memory Usage**: 2GB-16GB based on quality settings
- **Load Time**: <30 seconds initial generation
- **Hardware**: Scales from mobile devices to high-end gaming systems

## 🎓 Educational Applications

ThreatForge transforms complex systems understanding through interactive simulation:

- **Crisis Simulation**: Experience how small events cascade into global crises
- **Policy Testing**: Evaluate intervention strategies in safe virtual environments
- **Cross-Domain Learning**: Discover interconnected threat relationships
- **Emergent Behavior Study**: Observe simple components creating complex outcomes
- **Historical Analysis**: Compare simulations with real-world events
- **Adaptive Learning**: Difficulty adjusts to learner's pace and understanding

## 🤝 Community & Contributing

We welcome contributions across multiple areas:

- **🔧 Component Development**: Create new atomic behavioral components
- **🌍 Domain Expertise**: Contribute real-world threat knowledge
- **📚 Educational Content**: Develop learning materials and scenarios
- **⚡ Technical Improvements**: Optimize performance and add features
- **📝 Documentation**: Improve guides, tutorials, and API docs
- **🎨 Accessibility**: Help make the system accessible to all users

See our [Contributing Guide](CONTRIBUTING.md) and [Code of Conduct](CODE_OF_CONDUCT.md).

## 📄 License & Support

- **License**: MIT License - see [LICENSE](LICENSE)
- **Documentation**: Comprehensive guides and API reference
- **Community**: Active forum for discussions and support
- **Education**: Lesson plans and learning materials
- **Development**: Inspector tools, profiler, and debugger
- **Performance**: Detailed optimization guides and profiling tools

---

**ThreatForge**: Where atomic components create emergent complexity with performance that adapts to your hardware. Discover how simple interactions cascade into civilization-altering events through the power of emergent systems, running smoothly on everything from phones to gaming rigs.

## 📚 Next Steps

- **Get Started**: Follow our [Quick Start Guide](./QUICK_START.md)
- **Learn Concepts**: Read [Component Architecture](./COMPONENT_ARCHITECTURE.md)
- **See Examples**: Explore [Code Examples](./CODE_EXAMPLES.md)
- **Join Community**: Connect with other developers and users
- **Performance Guide**: Learn about [Adaptive Performance](./PERFORMANCE.md)
- **Educational Resources**: Access [Learning Materials](./EDUCATION.md)
