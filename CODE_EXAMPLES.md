# ThreatForge Code Examples 💻

## Overview

This document provides progressive code examples from basic threat creation to advanced multi-domain synthesis. Each example is complete and builds upon previous concepts. For educational framework and learning progression, see [QUICK_START.md](./QUICK_START.md).

## Example Progression

- **Tier 1**: Basic threat creation (Beginner)
- **Tier 2**: Simple composition (Intermediate)  
- **Tier 3**: Cross-domain interactions (Advanced)
- **Tier 4**: Complex synthesis (Expert)
- **Tier 5**: Custom components (Master)

### Development Environment Setup
```bash
# 1. Create project directory
mkdir threatforge-examples && cd threatforge-examples

# 2. Initialize TypeScript project
npm init -y
npm install typescript @types/node --save-dev
npx tsc --init

# 3. Install ThreatForge core and dependencies
npm install @threatforge/core three @types/three stats.js dat.gui eventemitter3 uuid @types/uuid

# 4. Install development tools
npm install --save-dev vite @vitejs/plugin-typescript
```

### Project Structure
```
threatforge-examples/
├── src/
│   ├── examples/
│   │   ├── tier1/
│   │   ├── tier2/
│   │   ├── tier3/
│   │   ├── tier4/
│   │   └── tier5/
│   ├── components/
│   ├── utils/
│   └── types/
├── package.json
├── tsconfig.json
└── vite.config.ts
```

### TypeScript Configuration (tsconfig.json)
```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "ESNext",
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "moduleResolution": "node",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "declaration": true,
    "declarationMap": true,
    "sourceMap": true,
    "outDir": "./dist",
    "rootDir": "./src",
    "removeComments": false,
    "noImplicitAny": true,
    "strictNullChecks": true,
    "strictFunctionTypes": true,
    "noImplicitThis": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true,
    "noUncheckedIndexedAccess": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

### Vite Configuration (vite.config.ts)
### Implementation Details & Performance Considerations

#### Memory Management
```typescript
// Efficient threat creation with memory pooling
const engine = new GameEngine({
  performance: {
    quality: 'minimal',
    enableComponentPooling: true,  // Reuse component instances
    maxThreats: 100,               // Limit concurrent threats
    memoryCleanupInterval: 5000    // Cleanup every 5 seconds
  }
})

// Manual memory management for large-scale simulations
class ThreatManager {
  private activeThreats: Map<string, Threat> = new Map()
  private threatPool: Threat[] = []
  
  createThreat(config: ThreatConfig): Threat {
    // Reuse from pool if available
    const threat = this.threatPool.pop() || new Threat()
    threat.initialize(config)
    this.activeThreats.set(threat.id, threat)
    return threat
  }
  
  destroyThreat(id: string): void {
    const threat = this.activeThreats.get(id)
    if (threat) {
      threat.cleanup()
      this.activeThreats.delete(id)
      this.threatPool.push(threat) // Return to pool
    }
  }
}
```

#### Performance Monitoring
```typescript
// Real-time performance tracking
class PerformanceMonitor {
  private metrics: PerformanceMetrics = {
    frameTime: 0,
    memoryUsage: 0,
    threatCount: 0,
    componentCount: 0
  }
  
  startMonitoring(): void {
    setInterval(() => {
      this.metrics.frameTime = this.measureFrameTime()
      this.metrics.memoryUsage = this.measureMemoryUsage()
      this.metrics.threatCount = this.engine.getThreatCount()
      this.metrics.componentCount = this.engine.getComponentCount()
      
      // Auto-adjust quality based on performance
      if (this.metrics.frameTime > 16.67) { // >60 FPS
        this.engine.setQuality('low')
      } else if (this.metrics.frameTime < 8.33) { // >120 FPS
        this.engine.setQuality('high')
      }
    }, 1000)
  }
}
```

#### Error Handling & Validation
```typescript
// Robust error handling for production
class ThreatValidator {
  static validateThreatConfig(config: ThreatConfig): ValidationResult {
    const errors: string[] = []
    
    // Validate transmission rate
    if (config.transmissionRate < 0 || config.transmissionRate > 1) {
      errors.push('Transmission rate must be between 0 and 1')
    }
    
    // Validate severity
    if (config.severity < 0 || config.severity > 1) {
      errors.push('Severity must be between 0 and 1')
    }
    
    // Validate incubation period
    if (config.incubationPeriod && config.incubationPeriod < 0) {
      errors.push('Incubation period must be positive')
    }
    
    return {
      isValid: errors.length === 0,
      errors,
      warnings: this.generateWarnings(config)
    }
  }
  
  private static generateWarnings(config: ThreatConfig): string[] {
    const warnings: string[] = []
    
    if (config.transmissionRate > 0.9) {
      warnings.push('High transmission rate may cause performance issues')
    }
    
    if (config.mutationPotential > 0.8) {
      warnings.push('High mutation potential may lead to unpredictable behavior')
    }
    
    return warnings
  }
}

// Usage with validation
const config = {
  transmissionRate: 0.95,
  severity: 0.8,
  incubationPeriod: -5 // Invalid
}

const validation = ThreatValidator.validateThreatConfig(config)
if (!validation.isValid) {
  console.error('Invalid threat configuration:', validation.errors)
  throw new Error('Threat configuration validation failed')
}

if (validation.warnings.length > 0) {
  console.warn('Threat configuration warnings:', validation.warnings)
}
```
```typescript
import { defineConfig } from 'vite'
import { resolve } from 'path'

export default defineConfig({
  build: {
    lib: {
      entry: resolve(__dirname, 'src/index.ts'),
      name: 'ThreatForgeExamples',
      fileName: 'threatforge-examples'
    },
    rollupOptions: {
      external: ['three', 'stats.js', 'dat.gui', 'eventemitter3', 'uuid'],
      output: {
        globals: {
          three: 'THREE',
          'stats.js': 'Stats',
          'dat.gui': 'dat.GUI',
          'eventemitter3': 'EventEmitter',
          'uuid': 'uuid'
        }
      }
    }
  },
  server: {
    port: 3000,
    open: true
  }
})
```
## Prerequisites

```bash
npm install @threatforge/core
```

## Tier 1: Basic Threat Creation

### Example 1.1: Hello World Threat

```typescript
// src/examples/tier1/hello-world.ts
import { GameEngine } from '@threatforge/core'

// Create engine with minimal configuration
const engine = new GameEngine({
  performance: {
    quality: 'minimal'  // Use minimal resources
  }
})

// Create the simplest possible threat
const helloThreat = engine.createThreat('BASIC_INFECTION', {
  transmissionRate: 0.5,
  severity: 0.3
})

console.log('🌍 Hello ThreatForge!')
console.log(`Threat ID: ${helloThreat.id}`)
console.log(`Type: ${helloThreat.type}`)
console.log(`Severity: ${helloThreat.severity}`)

// Expected output:
// 🌍 Hello ThreatForge!
// Threat ID: threat_001
// Type: BASIC_INFECTION
// Severity: 0.3
```

### Example 1.2: Threat with Properties

```typescript
// src/examples/tier1/threat-properties.ts
import { GameEngine } from '@threatforge/core'

const engine = new GameEngine()

// Create threat with detailed properties
const propertyThreat = engine.createThreat('BIOLOGICAL_INFECTION', {
  transmissionRate: 0.7,
  incubationPeriod: 5,        // days
  infectiousPeriod: 14,       // days
  mortalityRate: 0.02,        // 2% mortality
  mutationPotential: 0.1,     // Low mutation rate
  zoonoticPotential: 0.3      // Can jump species
})

console.log('🔬 Biological threat with properties:')
console.log(`Transmission Rate: ${propertyThreat.properties.transmissionRate}`)
console.log(`Incubation: ${propertyThreat.properties.incubationPeriod} days`)
console.log(`Mortality: ${propertyThreat.properties.mortalityRate * 100}%`)

// Simulate threat progression
for (let day = 0; day < 30; day++) {
  propertyThreat.update(1) // Update by 1 day
  console.log(`Day ${day}: ${propertyThreat.getInfectedCount()} infected`)
}
```

## Tier 2: Simple Composition

### Example 2.1: Two-Component Threat

```typescript
// src/examples/tier2/simple-composition.ts
import { GameEngine } from '@threatforge/core'

const engine = new GameEngine()

// Compose threat from two basic components
const composedThreat = engine.composeThreat([
  {
    type: 'BIOLOGICAL_INFECTION',
    properties: {
      transmissionRate: 0.6,
      severity: 0.4
    }
  },
  {
    type: 'AIRBORNE_TRANSMISSION',
    properties: {
      range: 500,
      seasonalVariation: true
    }
  }
])

console.log('🧬 Composed threat created!')
console.log(`Components: ${composedThreat.components.length}`)
console.log(`Domain: ${composedThreat.domain}`)

// Check for interactions
composedThreat.components.forEach((component, index) => {
  console.log(`Component ${index + 1}: ${component.type}`)
  console.log(`  Emergence Potential: ${component.emergencePotential}`)
})
```

### Example 2.2: Transmission Chain

```typescript
// src/examples/tier2/transmission-chain.ts
import { GameEngine } from '@threatforge/core'

const engine = new GameEngine()

// Create a transmission chain threat
const transmissionChain = engine.composeThreat([
  {
    type: 'BIOLOGICAL_INFECTION',
    properties: {
      transmissionRate: 0.5,
      mutationPotential: 0.05
    }
  },
  {
    type: 'HUMAN_HUMAN_TRANSMISSION',
    properties: {
      contactRate: 0.8,
      transmissionEfficiency: 0.7
    }
  },
  {
    type: 'SURFACE_CONTAMINATION',
    properties: {
      survivalTime: 72,     // hours
      contaminationRate: 0.3
    }
  }
])

console.log('🔗 Transmission chain threat:')
console.log(`Total transmission vectors: ${transmissionChain.components.length}`)

// Analyze transmission pathways
const pathways = transmissionChain.analyzeTransmissionPathways()
pathways.forEach(pathway => {
  console.log(`Pathway: ${pathway.source} → ${pathway.target}`)
  console.log(`  Efficiency: ${pathway.efficiency}`)
  console.log(`  Range: ${pathway.range}`)
})
```

## Tier 3: Cross-Domain Interactions

### Example 3.1: Cyber-Biological Hybrid

```typescript
// src/examples/tier3/cyber-biological.ts
import { GameEngine } from '@threatforge/core'

const engine = new GameEngine({
  performance: {
    quality: 'balanced',
    maxEmergentBehaviors: 20
  }
})

// Create cyber-biological hybrid threat
const cyberBioThreat = engine.composeThreat([
  // Biological foundation
  {
    type: 'BIOLOGICAL_INFECTION',
    properties: {
      transmissionRate: 0.6,
      incubationPeriod: 7,
      mutationPotential: 0.2
    }
  },
  // Cyber propagation vector
  {
    type: 'SOCIAL_MEDIA_PROPAGATION',
    properties: {
      viralCoefficient: 1.8,
      platformReach: 0.9,
      contentEngagement: 0.7
    }
  },
  // Cognitive manipulation
  {
    type: 'COGNITIVE_MANIPULATION',
    properties: {
      influenceStrength: 0.8,
      stealthLevel: 0.6,
      persistence: 0.9
    }
  }
])

console.log('🔬 Cyber-biological hybrid threat created!')
console.log(`Components: ${cyberBioThreat.components.length}`)
console.log(`Emergent behaviors: ${cyberBioThreat.emergentBehaviors.length}`)

// Analyze emergent behaviors
cyberBioThreat.emergentBehaviors.forEach((behavior, index) => {
  console.log(`\n🧬 Emergent Behavior ${index + 1}:`)
  console.log(`  Name: ${behavior.name}`)
  console.log(`  Description: ${behavior.description}`)
  console.log(`  Impact Level: ${behavior.impactLevel}`)
  console.log(`  Discovery Method: ${behavior.discoveryMethod}`)
})

// Expected emergent behaviors:
// 1. Information Cascade - Social media accelerates biological spread
// 2. Cognitive Resistance Reduction - Fear increases infection susceptibility
// 3. Viral Memetic Amplification - Biological metaphors enhance information spread
```

### Example 3.2: Environmental-Robotic Integration

```typescript
// src/examples/tier3/environmental-robotic.ts
import { GameEngine } from '@threatforge/core'

const engine = new GameEngine()

// Create environmental-robotic integrated threat
const enviroRoboticThreat = engine.composeThreat([
  // Environmental foundation
  {
    type: 'EXTREME_WEATHER',
    properties: {
      weatherType: 'HURRICANE',
      intensity: 0.9,
      duration: 168, // hours
      affectedArea: 100000 // km²
    }
  },
  // Robotic systems
  {
    type: 'ROBOTIC_SWARM',
    properties: {
      swarmSize: 10000,
      autonomyLevel: 0.8,
      coordinationEfficiency: 0.9
    }
  },
  // Infrastructure vulnerability
  {
    type: 'INFRASTRUCTURE_VULNERABILITY',
    properties: {
      systemType: 'POWER_GRID',
      vulnerabilityLevel: 0.7,
      cascadePotential: 0.8
    }
  }
])

console.log('🌪️ Environmental-robotic integrated threat:')
console.log(`Total system complexity: ${enviroRoboticThreat.complexityScore}`)

// Simulate environmental trigger
const weatherTrigger = {
  type: 'WEATHER_DETERIORATION',
  severity: 0.8,
  duration: 24
}

enviroRoboticThreat.triggerEvent(weatherTrigger)

// Check for emergent responses
const responses = enviroRoboticThreat.getEmergentResponses()
responses.forEach(response => {
  console.log(`🤖 Emergent Response: ${response.type}`)
  console.log(`  Trigger: ${response.trigger}`)
  console.log(`  Magnitude: ${response.magnitude}`)
})
```

## Tier 4: Complex Synthesis

### Example 4.1: Multi-Domain Synthesis

```typescript
// src/examples/tier4/multi-domain-synthesis.ts
import { GameEngine } from '@threatforge/core'

const engine = new GameEngine({
  performance: {
    quality: 'high',
    maxEmergentBehaviors: 50,
    complexity: 'advanced'
  }
})

// Create complex multi-domain synthetic threat
const syntheticThreat = engine.composeThreat([
  // Quantum foundation
  {
    type: 'QUANTUM_ENTANGLEMENT',
    properties: {
      coherenceTime: 2000,        // milliseconds
      entanglementStrength: 0.85,
      decoherenceResistance: 0.7,
      quantumFieldDensity: 0.6
    }
  },
  // AI learning system
  {
    type: 'AI_LEARNING_SYSTEM',
    properties: {
      learningRate: 0.15,
      neuralNetworkDepth: 12,
      creativityFactor: 0.8,
      selfModificationCapability: 0.9
    }
  },
  // Biological component
  {
    type: 'SYNTHETIC_BIOLOGY',
    properties: {
      geneticComplexity: 0.9,
      replicationFidelity: 0.95,
      environmentalAdaptation: 0.8
    }
  },
  // Network infrastructure
  {
    type: 'QUANTUM_NETWORK',
    properties: {
      quantumNodes: 1000,
      entanglementDistribution: 0.9,
      quantumRepeaterEfficiency: 0.85
    }
  },
  // Cognitive interface
  {
    type: 'NEURAL_INTERFACE',
    properties: {
      interfaceBandwidth: 1000,   // Mbps
      cognitiveCompatibility: 0.8,
      bidirectionalFlow: true
    }
  }
])

console.log('🌌 Multi-domain synthetic threat synthesized!')
console.log(`System complexity: ${syntheticThreat.systemComplexity}`)
console.log(`Quantum coherence: ${syntheticThreat.quantumMetrics.coherenceLevel}`)
console.log(`AI intelligence: ${syntheticThreat.aiMetrics.intelligenceLevel}`)

// Analyze emergent system properties
const emergentAnalysis = syntheticThreat.analyzeEmergentProperties()
console.log('\n🔬 Emergent System Analysis:')
console.log(`Novel capabilities: ${emergentAnalysis.novelCapabilities.length}`)
console.log(`Unpredictability score: ${emergentAnalysis.unpredictabilityScore}`)
console.log(`Evolution potential: ${emergentAnalysis.evolutionPotential}`)

// List emergent behaviors
syntheticThreat.emergentBehaviors.forEach((behavior, index) => {
  console.log(`\n🧬 Emergent Behavior ${index + 1}:`)
  console.log(`  ${behavior.name}: ${behavior.description}`)
  console.log(`  Complexity: ${behavior.complexity}`)
  console.log(`  Predictability: ${behavior.predictability}`)
})
```

### Example 4.2: Adaptive Evolution System

```typescript
// src/examples/tier4/adaptive-evolution.ts
import { GameEngine } from '@threatforge/core'

const engine = new GameEngine()

// Create adaptive evolution threat
const adaptiveThreat = engine.composeThreat([
  // Base threat
  {
    type: 'ADAPTIVE_PATHOGEN',
    properties: {
      baseInfectivity: 0.6,
      evolutionRate: 0.05,
      environmentalPlasticity: 0.8
    }
  },
  // Learning system
  {
    type: 'EVOLUTIONARY_ALGORITHM',
    properties: {
      mutationRate: 0.02,
      selectionPressure: 0.7,
      geneticDiversity: 0.9
    }
  },
  // Counter-adaptation
  {
    type: 'COUNTER_MEASURE_INTELLIGENCE',
    properties: {
    intelligenceGathering: 0.85,
    adaptationPrediction: 0.75,
    evasionDevelopment: 0.8
    }
  },
  // Environmental sensing
  {
    type: 'ENVIRONMENTAL_SENSING',
    properties: {
      sensingRange: 1000,
      adaptationSpeed: 0.9,
      multiFactorAnalysis: true
    }
  }
])

console.log('🧬 Adaptive evolution threat created!')

// Simulate evolutionary pressure
const pressures = [
  { type: 'TEMPERATURE_INCREASE', magnitude: 0.3 },
  { type: 'HUMIDITY_DECREASE', magnitude: 0.4 },
  { type: 'COUNTER_MEASURE_DEPLOYMENT', magnitude: 0.6 }
]

pressures.forEach((pressure, index) => {
  console.log(`\n⚡ Evolutionary Pressure ${index + 1}: ${pressure.type}`)
  
  const response = adaptiveThreat.respondToPressure(pressure)
  console.log(`  Response time: ${response.responseTime} cycles`)
  console.log(`  Adaptation success: ${response.successRate * 100}%`)
  console.log(`  New traits acquired: ${response.newTraits.length}`)
  
  response.newTraits.forEach(trait => {
    console.log(`    - ${trait.name}: ${trait.description}`)
  })
})

// Check long-term evolution
const evolutionTrajectory = adaptiveThreat.predictEvolution(100) // 100 cycles
console.log('\n📈 Evolution Trajectory:')
console.log(`  Predicted complexity: ${evolutionTrajectory.finalComplexity}`)
console.log(`  Adaptation events: ${evolutionTrajectory.adaptationEvents}`)
console.log(`  Survival probability: ${evolutionTrajectory.survivalProbability * 100}%`)
```

## Tier 5: Custom Components

### Example 5.1: Creating Custom Components

```typescript
// src/examples/tier5/custom-components.ts
import { 
  GameEngine, 
  ThreatComponent, 
  Behavior,
  ComponentType 
} from '@threatforge/core'

// Define custom component class
class QuantumNeuralInterface extends ThreatComponent {
  type = 'QUANTUM_NEURAL_INTERFACE' as ComponentType
  domain = 'QUANTUM' as const
  emergencePotential = 0.95
  
  properties = {
    quantumCoherence: 0.9,
    neuralBandwidth: 1000,    // Mbps
    interfaceStability: 0.85,
    cognitiveDepth: 0.8,
    entanglementFidelity: 0.92
  }
  
  behaviors = [
    new QuantumInterfaceBehavior(),
    new NeuralIntegrationBehavior(),
    new CognitiveEnhancementBehavior(),
    new EntanglementSynchronizationBehavior()
  ]
  
  interactions = [
    {
      targetComponent: 'AI_LEARNING_SYSTEM',
      interactionType: 'SYNERGY',
      multiplier: 2.5,
      conditions: [{ type: 'QUANTUM_COHERENCE', threshold: 0.8 }]
    },
    {
      targetComponent: 'COGNITIVE_MANIPULATION',
      interactionType: 'TRANSFORMATION',
      multiplier: 1.8,
      conditions: [{ type: 'NEURAL_COMPATIBILITY', threshold: 0.7 }]
    }
  ]
}

// Implement custom behaviors
class QuantumInterfaceBehavior implements Behavior {
  update(deltaTime: number, context: any): void {
    // Maintain quantum coherence
    const coherence = context.getQuantumCoherence()
    if (coherence > 0.8) {
      context.enhanceNeuralBandwidth(1.5)
    }
  }
  
  validate(): boolean {
    return true
  }
  
  getEmergentPotential(): number {
    return 0.9
  }
}

class NeuralIntegrationBehavior implements Behavior {
  update(deltaTime: number, context: any): void {
    // Integrate with neural systems
    const neuralActivity = context.getNeuralActivity()
    const integrationRate = this.calculateIntegrationRate(neuralActivity)
    
    context.setIntegrationLevel(integrationRate)
  }
  
  private calculateIntegrationRate(activity: number): number {
    return Math.min(1.0, activity * 1.2)
  }
  
  validate(): boolean {
    return true
  }
  
  getEmergentPotential(): number {
    return 0.85
  }
}

// Use custom component
const engine = new GameEngine()

// Register custom component
engine.componentRegistry.register('QUANTUM_NEURAL_INTERFACE', QuantumNeuralInterface)

// Create threat with custom component
const customThreat = engine.composeThreat([
  {
    type: 'QUANTUM_NEURAL_INTERFACE',
    properties: {
      quantumCoherence: 0.95,
      neuralBandwidth: 2000,
      cognitiveDepth: 0.9
    }
  },
  {
    type: 'AI_LEARNING_SYSTEM',
    properties: {
      learningRate: 0.2,
      creativityFactor: 0.9
    }
  }
])

console.log('🧠 Custom quantum-neural interface threat created!')
console.log(`Custom component: ${customThreat.components[0].type}`)
console.log(`Integration level: ${customThreat.components[0].properties.integrationLevel}`)

// Analyze custom interactions
const customInteractions = customThreat.analyzeCustomInteractions()
customInteractions.forEach(interaction => {
  console.log(`🔬 Custom Interaction: ${interaction.type}`)
  console.log(`  Strength: ${interaction.strength}`)
  console.log(`  Emergence: ${interaction.emergencePotential}`)
})
```

### Example 5.2: Advanced Custom Behavior

```typescript
// src/examples/tier5/advanced-custom-behavior.ts
import { Behavior, BehaviorContext } from '@threatforge/core'

// Advanced custom behavior with machine learning
class MachineLearningBehavior implements Behavior {
  private model: NeuralNetwork
  private trainingData: TrainingSample[]
  private learningRate: number
  private adaptationSpeed: number
  
  constructor(config: MLBehaviorConfig) {
    this.learningRate = config.learningRate || 0.01
    this.adaptationSpeed = config.adaptationSpeed || 0.1
    this.model = new NeuralNetwork({
      layers: config.layers || [10, 20, 15, 5],
      activation: 'relu',
      learningRate: this.learningRate
    })
    this.trainingData = []
  }
  
  update(deltaTime: number, context: BehaviorContext): void {
    // Collect training data
    const currentState = this.extractFeatures(context)
    const predictedOutcome = this.model.predict(currentState)
    
    // Take action based on prediction
    const action = this.selectAction(predictedOutcome)
    this.executeAction(action, context)
    
    // Learn from results
    const actualOutcome = this.measureOutcome(context)
    this.trainingData.push({
      input: currentState,
      output: actualOutcome
    })
    
    // Retrain model periodically
    if (this.trainingData.length > 100) {
      this.retrainModel()
    }
  }
  
  private extractFeatures(context: BehaviorContext): number[] {
    return [
      context.getThreatIntensity(),
      context.getEnvironmentalStress(),
      context.getCountermeasureEffectiveness(),
      context.getPopulationDensity(),
      context.getNetworkConnectivity(),
      context.getQuantumCoherence(),
      context.getTemporalAlignment(),
      context.getCrossDomainSynergy()
    ]
  }
  
  private selectAction(predictions: number[]): Action {
    // Use epsilon-greedy exploration
    if (Math.random() < 0.1) { // 10% exploration
      return this.getRandomAction()
    } else {
      return this.getBestAction(predictions)
    }
  }
  
  private retrainModel(): void {
    // Use recent data for training
    const recentData = this.trainingData.slice(-50)
    this.model.train(recentData, {
      epochs: 10,
      batchSize: 10,
      validationSplit: 0.2
    })
  }
  
  validate(): boolean {
    return this.model.isValid() && this.trainingData.length > 10
  }
  
  getEmergentPotential(): number {
    // Higher emergence as model learns
    const learningProgress = Math.min(1.0, this.trainingData.length / 100)
    return 0.7 + (0.3 * learningProgress)
  }
}

// Use advanced behavior in custom component
class AdaptiveAIComponent extends ThreatComponent {
  type = 'ADAPTIVE_AI_SYSTEM'
  domain = 'CYBER'
  emergencePotential = 0.98
  
  properties = {
    neuralNetworkDepth: 15,
    learningCapability: 0.95,
    adaptationSpeed: 0.8,
    creativityFactor: 0.85,
    selfImprovement: 0.9
  }
  
  behaviors = [
    new MachineLearningBehavior({
      learningRate: 0.02,
      adaptationSpeed: 0.15,
      layers: [20, 40, 30, 10]
    }),
    new SelfImprovementBehavior(),
    new CreativeProblemSolvingBehavior()
  ]
}

// Test advanced behavior
const engine = new GameEngine()

const adaptiveAIThreat = engine.composeThreat([
  {
    type: 'ADAPTIVE_AI_SYSTEM',
    properties: {
      neuralNetworkDepth: 20,
      learningCapability: 0.98,
      creativityFactor: 0.9
    }
  },
  {
    type: 'QUANTUM_COMPUTING',
    properties: {
      qubitCount: 1000,
      coherenceTime: 5000,
      quantumAdvantage: 0.95
    }
## 🔬 Comprehensive Testing & Validation Framework

### Unit Testing with Jest
```typescript
// tests/unit/ThreatEngine.test.ts
import { GameEngine } from '@threatforge/core'
import { describe, it, expect, beforeEach, afterEach } from '@jest/globals'

describe('GameEngine', () => {
  let engine: GameEngine
  
  beforeEach(() => {
    engine = new GameEngine({
      performance: { quality: 'minimal' }
    })
  })
  
  afterEach(() => {
    engine.cleanup()
  })
  
  describe('createThreat', () => {
    it('should create a basic threat with valid properties', () => {
      const threat = engine.createThreat('BASIC_INFECTION', {
        transmissionRate: 0.5,
        severity: 0.3
      })
      
      expect(threat).toBeDefined()
      expect(threat.id).toMatch(/^threat_\d+$/)
      expect(threat.type).toBe('BASIC_INFECTION')
      expect(threat.properties.transmissionRate).toBe(0.5)
      expect(threat.properties.severity).toBe(0.3)
    })
    
    it('should throw error for invalid transmission rate', () => {
      expect(() => {
        engine.createThreat('BASIC_INFECTION', {
          transmissionRate: 1.5, // Invalid: > 1
          severity: 0.3
        })
      }).toThrow('Transmission rate must be between 0 and 1')
    })
    
    it('should handle edge cases gracefully', () => {
      const threat = engine.createThreat('BASIC_INFECTION', {
        transmissionRate: 0,
        severity: 0
      })
      
      expect(threat.properties.transmissionRate).toBe(0)
      expect(threat.properties.severity).toBe(0)
    })
  })
  
  describe('composeThreat', () => {
    it('should compose multiple components correctly', () => {
      const threat = engine.composeThreat([
        {
          type: 'BIOLOGICAL_INFECTION',
          properties: { transmissionRate: 0.6 }
        },
        {
          type: 'AIRBORNE_TRANSMISSION',
          properties: { range: 500 }
        }
      ])
      
      expect(threat.components).toHaveLength(2)
      expect(threat.domain).toBe('MULTI_DOMAIN')
      expect(threat.emergentBehaviors.length).toBeGreaterThan(0)
    })
    
    it('should detect cross-domain interactions', () => {
      const threat = engine.composeThreat([
        { type: 'BIOLOGICAL_INFECTION', properties: {} },
        { type: 'NETWORK_PROPAGATION', properties: {} }
      ])
      
      const crossDomainInteractions = threat.getCrossDomainInteractions()
      expect(crossDomainInteractions.length).toBeGreaterThan(0)
    })
  })
})
```

### Integration Testing
```typescript
// tests/integration/CrossDomainIntegration.test.ts
import { GameEngine } from '@threatforge/core'

describe('Cross-Domain Integration', () => {
  let engine: GameEngine
  
  beforeEach(() => {
    engine = new GameEngine({
      performance: { quality: 'balanced' }
    })
  })
  
  it('should create cyber-biological hybrid with emergent behaviors', () => {
    const threat = engine.composeThreat([
      {
        type: 'BIOLOGICAL_INFECTION',
        properties: {
          transmissionRate: 0.6,
          incubationPeriod: 7
        }
      },
      {
        type: 'SOCIAL_MEDIA_PROPAGATION',
        properties: {
          viralCoefficient: 1.8,
          platformReach: 0.9
        }
      }
    ])
    
    // Verify emergent behaviors
    const emergentBehaviors = threat.emergentBehaviors
    expect(emergentBehaviors.length).toBeGreaterThanOrEqual(2)
    
    // Check for specific expected behaviors
    const behaviorNames = emergentBehaviors.map(b => b.name)
    expect(behaviorNames).toContain('Information Cascade')
    expect(behaviorNames).toContain('Cognitive Resistance Reduction')
    
    // Verify behavior properties
    const infoCascade = emergentBehaviors.find(b => b.name === 'Information Cascade')
    expect(infoCascade?.impactLevel).toBeGreaterThan(0.7)
    expect(infoCascade?.discoveryMethod).toBe('CROSS_DOMAIN_ANALYSIS')
  })
  
  it('should handle complex multi-domain synthesis', () => {
    const threat = engine.composeThreat([
      { type: 'QUANTUM_ENTANGLEMENT', properties: { coherenceTime: 2000 } },
      { type: 'AI_LEARNING_SYSTEM', properties: { learningRate: 0.15 } },
      { type: 'SYNTHETIC_BIOLOGY', properties: { geneticComplexity: 0.9 } }
    ])
    
    expect(threat.systemComplexity).toBeGreaterThan(0.8)
    expect(threat.quantumMetrics.coherenceLevel).toBeGreaterThan(0.7)
    expect(threat.aiMetrics.intelligenceLevel).toBeGreaterThan(0.6)
    
    const emergentAnalysis = threat.analyzeEmergentProperties()
    expect(emergentAnalysis.novelCapabilities.length).toBeGreaterThan(2)
    expect(emergentAnalysis.unpredictabilityScore).toBeGreaterThan(0.5)
  })
})
```

### Performance Testing
```typescript
// tests/performance/PerformanceBenchmarks.test.ts
import { GameEngine } from '@threatforge/core'

describe('Performance Benchmarks', () => {
  it('should maintain 60 FPS with 1000 threats', async () => {
    const engine = new GameEngine({
      performance: {
        quality: 'balanced',
        targetFPS: 60
      }
    })
    
    // Create 1000 threats
    const threats = []
    for (let i = 0; i < 1000; i++) {
      threats.push(engine.createThreat('BASIC_INFECTION', {
        transmissionRate: Math.random(),
        severity: Math.random()
      }))
    }
    
    // Measure frame time over 100 frames
    const frameTimes: number[] = []
    for (let frame = 0; frame < 100; frame++) {
      const start = performance.now()
      
      // Update all threats
      threats.forEach(threat => threat.update(0.016)) // 60 FPS delta
      
      const end = performance.now()
      frameTimes.push(end - start)
    }
    
    // Calculate statistics
    const avgFrameTime = frameTimes.reduce((a, b) => a + b) / frameTimes.length
    const maxFrameTime = Math.max(...frameTimes)
    const minFrameTime = Math.min(...frameTimes)
    
    // Assertions
    expect(avgFrameTime).toBeLessThan(16.67) // 60 FPS
    expect(maxFrameTime).toBeLessThan(20) // No significant spikes
    expect(minFrameTime).toBeGreaterThan(0) // Valid measurements
    
    console.log(`Average frame time: ${avgFrameTime.toFixed(2)}ms`)
    console.log(`Max frame time: ${maxFrameTime.toFixed(2)}ms`)
    console.log(`Min frame time: ${minFrameTime.toFixed(2)}ms`)
  })
  
  it('should handle memory efficiently with component pooling', () => {
    const engine = new GameEngine({
      performance: {
        quality: 'minimal',
        enableComponentPooling: true
      }
    })
    
    // Measure initial memory
    const initialMemory = performance.memory?.usedJSHeapSize || 0
    
    // Create and destroy 10000 threats
    for (let i = 0; i < 10000; i++) {
      const threat = engine.createThreat('BASIC_INFECTION', {
        transmissionRate: 0.5,
        severity: 0.3
      })
      
      // Simulate some work
      threat.update(0.016)
      
      // Clean up
      threat.destroy()
    }
    
    // Force garbage collection if available
    if (global.gc) {
      global.gc()
    }
    
    // Measure final memory
    const finalMemory = performance.memory?.usedJSHeapSize || 0
    const memoryIncrease = finalMemory - initialMemory
    
    // Memory increase should be minimal due to pooling
    expect(memoryIncrease).toBeLessThan(50 * 1024 * 1024) // Less than 50MB increase
  })
})
```

### Visual Regression Testing
```typescript
// tests/visual/VisualRegression.test.ts
import { GameEngine } from '@threatforge/core'
import { toMatchImageSnapshot } from 'jest-image-snapshot'

expect.extend({ toMatchImageSnapshot })

describe('Visual Regression Tests', () => {
  let engine: GameEngine
  
  beforeEach(() => {
    engine = new GameEngine({
      performance: { quality: 'high' },
      rendering: {
        width: 1920,
        height: 1080,
        antialias: true
      }
    })
  })
  
  it('should render basic threat consistently', async () => {
    const threat = engine.createThreat('BIOLOGICAL_INFECTION', {
      transmissionRate: 0.7,
      severity: 0.5
    })
    
    // Render threat visualization
    const canvas = engine.renderThreat(threat, {
      cameraPosition: [0, 0, 100],
      lighting: 'standard',
      showComponents: true,
      showEmergentBehaviors: true
    })
    
    // Convert canvas to image
    const image = canvas.toDataURL('image/png')
    
    // Compare with baseline
    expect(image).toMatchImageSnapshot({
      failureThreshold: 0.01, // 1% difference threshold
      failureThresholdType: 'percent'
    })
  })
  
  it('should render cross-domain threat with proper visual complexity', async () => {
    const threat = engine.composeThreat([
      { type: 'BIOLOGICAL_INFECTION', properties: { transmissionRate: 0.6 } },
      { type: 'NETWORK_PROPAGATION', properties: { viralCoefficient: 1.5 } }
    ])
    
    const canvas = engine.renderThreat(threat, {
      cameraPosition: [50, 50, 100],
      lighting: 'advanced',
      showInteractions: true,
      colorScheme: 'domain-specific'
    })
    
    const image = canvas.toDataURL('image/png')
    
    // Should have more visual complexity than single-domain threat
    const complexityScore = await analyzeVisualComplexity(image)
    expect(complexityScore).toBeGreaterThan(0.7)
    
    expect(image).toMatchImageSnapshot({
      failureThreshold: 0.02,
      failureThresholdType: 'percent'
    })
  })
})
```

### Load Testing
```typescript
// tests/load/LoadTesting.test.ts
import { GameEngine } from '@threatforge/core'

describe('Load Testing', () => {
  it('should handle 10000 concurrent threats', async () => {
    const engine = new GameEngine({
      performance: {
        quality: 'minimal',
        maxThreats: 15000,
        enableComponentPooling: true
      }
    })
    
    const startTime = Date.now()
    
    // Create 10000 threats
    const threats = []
    for (let i = 0; i < 10000; i++) {
      const threat = engine.createThreat('BASIC_INFECTION', {
        transmissionRate: Math.random() * 0.8,
        severity: Math.random() * 0.6
      })
      threats.push(threat)
    }
    
    const creationTime = Date.now() - startTime
    console.log(`Created 10000 threats in ${creationTime}ms`)
    
    // Update all threats for 100 frames
    const updateStart = Date.now()
    for (let frame = 0; frame < 100; frame++) {
      threats.forEach(threat => threat.update(0.016))
    }
    const updateTime = Date.now() - updateStart
    
    console.log(`Updated 10000 threats for 100 frames in ${updateTime}ms`)
    
    // Performance assertions
    expect(creationTime).toBeLessThan(5000) // Create 10k threats in <5s
    expect(updateTime).toBeLessThan(10000) // Update 10k threats 100x in <10s
    
    // Memory assertions
    const memoryUsage = process.memoryUsage()
    expect(memoryUsage.heapUsed).toBeLessThan(2 * 1024 * 1024 * 1024) // <2GB
  })
  
  it('should recover from high load scenarios', async () => {
    const engine = new GameEngine()
    
    // Create extreme load
    const extremeThreats = []
    for (let i = 0; i < 5000; i++) {
      extremeThreats.push(engine.composeThreat([
        { type: 'BIOLOGICAL_INFECTION', properties: {} },
        { type: 'NETWORK_PROPAGATION', properties: {} },
        { type: 'QUANTUM_ENTANGLEMENT', properties: {} },
        { type: 'AI_LEARNING_SYSTEM', properties: {} }
      ]))
    }
    
    // Measure performance under extreme load
    const loadStart = performance.now()
    extremeThreats.forEach(threat => threat.update(0.016))
    const loadTime = performance.now() - loadStart
    
    // Clear extreme load
    extremeThreats.forEach(threat => threat.destroy())
    
    // Measure recovery performance
    const recoveryThreat = engine.createThreat('BASIC_INFECTION', {
      transmissionRate: 0.5,
      severity: 0.3
    })
    
    const recoveryStart = performance.now()
    recoveryThreat.update(0.016)
    const recoveryTime = performance.now() - recoveryStart
    
    // Recovery should be much faster than under load
    expect(recoveryTime).toBeLessThan(loadTime / 10)
  })
})
```
  }
])

console.log('🤖 Advanced adaptive AI threat created!')
console.log(`Learning capability: ${adaptiveAIThreat.components[0].properties.learningCapability}`)

// Monitor learning progress
setInterval(() => {
  const learningProgress = adaptiveAIThreat.getLearningProgress()
  console.log(`📊 Learning Progress: ${(learningProgress * 100).toFixed(1)}%`)
  console.log(`🧠 Intelligence Level: ${adaptiveAIThreat.getIntelligenceLevel()}`)
}, 5000)
```

## Testing and Validation

### Running the Examples

```bash
# Install dependencies
npm install

# Run individual examples
npm run example:tier1-hello-world
npm run example:tier2-composition
npm run example:tier3-cyber-biological
npm run example:tier4-multi-domain
npm run example:tier5-custom-components

# Run all examples
npm run examples:all

# Run with performance profiling
npm run examples:profile
```

### Expected Outputs

Each example includes expected console output to verify correct implementation:

```typescript
// Example verification
const expectedOutput = {
  components: 3,
  emergentBehaviors: 2,
  domain: 'MULTI_DOMAIN',
  complexity: 'HIGH'
}

const actualOutput = {
  components: threat.components.length,
  emergentBehaviors: threat.emergentBehaviors.length,
  domain: threat.domain,
  complexity: threat.complexity
}

console.assert(
  JSON.stringify(actualOutput) === JSON.stringify(expectedOutput),
  'Example output verification failed!'
)
```

## Performance Considerations

### Memory Management

```typescript
// Efficient component creation
const efficientThreat = engine.composeThreat([
  { type: 'BIOLOGICAL_INFECTION', properties: { transmissionRate: 0.6 } },
  { type: 'AIRBORNE_TRANSMISSION', properties: { range: 500 } }
], {
  performance: {
    quality: 'balanced',
    maxComponents: 10,
    memoryOptimization: true
  }
})
```

### Complexity Limits

```typescript
// Prevent complexity explosion
const controlledThreat = engine.composeThreat(complexComponents, {
  performance: {
    maxEmergentBehaviors: 25,
    complexityThreshold: 0.8,
    optimizationLevel: 'aggressive'
  }
})
```

## Troubleshooting Examples

### Common Issues and Solutions

```typescript
// Issue: Too many emergent behaviors
const limitedThreat = engine.composeThreat(components, {
  performance: {
    maxEmergentBehaviors: 15,  // Limit emergence
    quality: 'low'             // Reduce quality
  }
})

// Issue: Poor performance
const optimizedThreat = engine.composeThreat(components, {
  performance: {
    targetFPS: 30,             // Lower FPS target
    detailLevel: 1,            // Minimal detail
    memoryLimit: 'conservative' // Conservative memory usage
  }
})

// Issue: No cross-domain interactions
const crossDomainThreat = engine.composeThreat([
  { type: 'BIOLOGICAL_INFECTION', properties: {} },        // Biological
  { type: 'NETWORK_PROPAGATION', properties: {} },        // Cyber
  { type: 'QUANTUM_ENTANGLEMENT', properties: {} },       // Quantum
  { type: 'WEATHER_SYSTEM', properties: {} }              // Environmental
])
```

## Next Steps

- **[API Reference](API_REFERENCE.md)**: Complete API documentation
- **[Performance Optimization](PERFORMANCE_OPTIMIZATION.md)**: Advanced optimization techniques
- **[Component Architecture](COMPONENT_ARCHITECTURE.md)**: Deep dive into component system
- **[Quick Start](QUICK_START.md)**: Educational framework and learning progression

## Contributing Examples

We welcome community contributions! Submit your examples:

1. Fork the repository
2. Create your example in `src/examples/community/`
3. Include comprehensive comments and expected outputs
4. Submit a pull request with detailed description

**Happy coding!** 🚀
## ✅ Implementation Checklists & Validation Steps

### Pre-Implementation Checklist
```markdown
## 🔧 Development Environment Setup Checklist

### System Requirements
- [ ] Node.js 16+ installed (`node --version`)
- [ ] npm 8+ installed (`npm --version`)
- [ ] TypeScript 4.5+ installed (`tsc --version`)
- [ ] Git installed (`git --version`)
- [ ] 8GB+ RAM available
- [ ] 2GB+ disk space available

### Project Setup
- [ ] Create project directory
- [ ] Initialize npm project (`npm init -y`)
- [ ] Install TypeScript and dependencies
- [ ] Configure tsconfig.json with strict settings
- [ ] Set up Vite development server
- [ ] Install ThreatForge core package
- [ ] Install 3D rendering dependencies (three.js)
- [ ] Install development tools (stats.js, dat.GUI)

### Development Tools
- [ ] Install VS Code or preferred IDE
- [ ] Install TypeScript extensions
- [ ] Configure ESLint for code quality
- [ ] Set up Prettier for code formatting
- [ ] Install Jest for testing
- [ ] Configure debugging environment

### Validation Steps
- [ ] Run `npm run dev` - should start without errors
- [ ] Open browser to http://localhost:3000
- [ ] Check browser console for errors
- [ ] Verify TypeScript compilation
- [ ] Test hot module replacement
- [ ] Validate package.json scripts
```

### Implementation Validation Checklist
```typescript
// validation/implementation-checklist.ts

export class ImplementationValidator {
  private checks: ValidationCheck[] = [
    {
      id: 'engine-creation',
      name: 'GameEngine Creation',
      description: 'Verify GameEngine can be instantiated',
      test: () => {
        const engine = new GameEngine()
        return engine !== null && engine !== undefined
      }
    },
    {
      id: 'basic-threat',
      name: 'Basic Threat Creation',
      description: 'Create a simple threat with properties',
      test: () => {
        const engine = new GameEngine()
        const threat = engine.createThreat('BASIC_INFECTION', {
          transmissionRate: 0.5,
          severity: 0.3
        })
        return threat.id !== undefined && threat.type === 'BASIC_INFECTION'
      }
    },
    {
      id: 'threat-composition',
      name: 'Threat Composition',
      description: 'Compose threat from multiple components',
      test: () => {
        const engine = new GameEngine()
        const threat = engine.composeThreat([
          { type: 'BIOLOGICAL_INFECTION', properties: {} },
          { type: 'AIRBORNE_TRANSMISSION', properties: {} }
        ])
        return threat.components.length === 2
      }
    },
    {
      id: 'emergent-behaviors',
      name: 'Emergent Behavior Detection',
      description: 'Verify emergent behaviors are created',
      test: () => {
        const engine = new GameEngine()
        const threat = engine.composeThreat([
          { type: 'BIOLOGICAL_INFECTION', properties: {} },
          { type: 'NETWORK_PROPAGATION', properties: {} }
        ])
        return threat.emergentBehaviors.length > 0
      }
    },
    {
      id: 'performance-targets',
      name: 'Performance Targets',
      description: 'Verify performance meets targets',
      test: () => {
        const engine = new GameEngine()
        const start = performance.now()
        
        // Create 100 threats
        for (let i = 0; i < 100; i++) {
          engine.createThreat('BASIC_INFECTION', {
            transmissionRate: 0.5,
            severity: 0.3
          })
        }
        
        const end = performance.now()
        return end - start < 100 // Should complete in <100ms
      }
    }
  ]
  
  async runValidation(): Promise<ValidationResult> {
    const results: ValidationResult[] = []
    
    for (const check of this.checks) {
      try {
        const passed = await check.test()
        results.push({
          checkId: check.id,
          name: check.name,
          description: check.description,
          passed,
          error: passed ? undefined : new Error('Check failed'),
          timestamp: new Date()
        })
      } catch (error) {
        results.push({
          checkId: check.id,
          name: check.name,
          description: check.description,
          passed: false,
          error: error as Error,
          timestamp: new Date()
        })
      }
    }
    
    return {
      overall: results.every(r => r.passed),
      results,
      summary: {
        total: results.length,
        passed: results.filter(r => r.passed).length,
        failed: results.filter(r => !r.passed).length
      }
    }
  }
}

// Usage
const validator = new ImplementationValidator()
const result = await validator.runValidation()

console.log('🔍 Implementation Validation Results:')
console.log(`Overall: ${result.overall ? '✅ PASS' : '❌ FAIL'}`)
console.log(`Passed: ${result.summary.passed}/${result.summary.total}`)

result.results.forEach(r => {
  console.log(`${r.passed ? '✅' : '❌'} ${r.name}: ${r.description}`)
  if (!r.passed && r.error) {
    console.log(`   Error: ${r.error.message}`)
  }
})
```

### Production Deployment Checklist
```markdown
## 🚀 Production Deployment Checklist

### Pre-Deployment
- [ ] All unit tests passing (`npm test`)
- [ ] All integration tests passing (`npm run test:integration`)
- [ ] Performance benchmarks met (`npm run test:performance`)
- [ ] Memory leak tests passed (`npm run test:memory`)
- [ ] Security audit completed (`npm audit`)
- [ ] Bundle size optimized (`npm run build && npm run analyze`)
- [ ] TypeScript compilation successful (`npm run type-check`)
- [ ] Linting passed (`npm run lint`)
- [ ] Code formatting verified (`npm run format:check`)

### Environment Configuration
- [ ] Production environment variables set
- [ ] Database connections configured
- [ ] API endpoints configured
- [ ] CDN configuration verified
- [ ] SSL certificates installed
- [ ] Domain names configured
- [ ] Load balancer configured
- [ ] Monitoring tools configured

### Performance Optimization
- [ ] Bundle size < 1MB (gzipped)
- [ ] First load time < 3 seconds
- [ ] Time to interactive < 5 seconds
- [ ] Lighthouse score > 90
- [ ] Core Web Vitals optimized
- [ ] Service worker configured
- [ ] Caching strategy implemented
- [ ] CDN distribution enabled

### Security
- [ ] Content Security Policy configured
- [ ] CORS properly configured
- [ ] Input validation implemented
- [ ] XSS protection enabled
- [ ] CSRF protection enabled
- [ ] Rate limiting configured
- [ ] Security headers configured
- [ ] Vulnerability scanning completed

### Monitoring & Analytics
- [ ] Error tracking configured (Sentry)
- [ ] Performance monitoring enabled
- [ ] User analytics configured
- [ ] Uptime monitoring configured
- [ ] Log aggregation configured
- [ ] Alerting system configured
- [ ] Health check endpoints implemented
- [ ] Backup strategy implemented

### Documentation
- [ ] API documentation updated
- [ ] User documentation updated
- [ ] Deployment documentation updated
- [ ] Troubleshooting guide updated
- [ ] Performance benchmarks documented
- [ ] Security considerations documented
- [ ] Rollback procedures documented
- [ ] Emergency contacts updated
```

### Continuous Integration Setup
```yaml
# .github/workflows/ci.yml
name: CI/CD Pipeline

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    
    strategy:
      matrix:
        node-version: [16.x, 18.x, 20.x]
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v3
      with:
        node-version: ${{ matrix.node-version }}
    
    - name: Install dependencies
      run: npm ci
    
    - name: Run type checking
      run: npm run type-check
    
    - name: Run linting
      run: npm run lint
    
    - name: Run unit tests
      run: npm run test:unit -- --coverage
    
    - name: Run integration tests
      run: npm run test:integration
    
    - name: Run performance tests
      run: npm run test:performance
    
    - name: Upload coverage reports
      uses: codecov/codecov-action@v3
      with:
        file: ./coverage/lcov.info
    
    - name: Build project
      run: npm run build
    
    - name: Analyze bundle size
      run: npm run analyze
    
    - name: Security audit
      run: npm audit --audit-level high
    
    - name: Validate implementation
      run: npm run validate

  deploy:
    needs: test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Deploy to production
      run: npm run deploy:production
      env:
        DEPLOY_KEY: ${{ secrets.DEPLOY_KEY }}
```

### Performance Monitoring Dashboard
```typescript
// monitoring/performance-dashboard.ts

export class PerformanceDashboard {
  private metrics: PerformanceMetrics = {
    fps: 0,
    frameTime: 0,
    memoryUsage: 0,
    threatCount: 0,
    componentCount: 0,
    emergentBehaviorCount: 0,
    crossDomainInteractions: 0
  }
  
  private targets: PerformanceTargets = {
    minFPS: 60,
    maxFrameTime: 16.67,
    maxMemoryUsage: 4 * 1024 * 1024 * 1024, // 4GB
    maxThreatCount: 10000,
    maxComponentCount: 50000,
    maxEmergentBehaviors: 1000
  }
  
  startMonitoring(): void {
    setInterval(() => {
      this.collectMetrics()
      this.validateTargets()
      this.updateDashboard()
    }, 1000)
  }
  
  private collectMetrics(): void {
    this.metrics.fps = this.calculateFPS()
    this.metrics.frameTime = this.measureFrameTime()
    this.metrics.memoryUsage = this.measureMemoryUsage()
    this.metrics.threatCount = this.engine.getThreatCount()
    this.metrics.componentCount = this.engine.getComponentCount()
    this.metrics.emergentBehaviorCount = this.engine.getEmergentBehaviorCount()
    this.metrics.crossDomainInteractions = this.engine.getCrossDomainInteractionCount()
  }
  
  private validateTargets(): void {
    const violations: string[] = []
    
    if (this.metrics.fps < this.targets.minFPS) {
      violations.push(`FPS below target: ${this.metrics.fps} < ${this.targets.minFPS}`)
    }
    
    if (this.metrics.frameTime > this.targets.maxFrameTime) {
      violations.push(`Frame time above target: ${this.metrics.frameTime}ms > ${this.targets.maxFrameTime}ms`)
    }
    
    if (this.metrics.memoryUsage > this.targets.maxMemoryUsage) {
      violations.push(`Memory usage above target: ${this.formatBytes(this.metrics.memoryUsage)} > ${this.formatBytes(this.targets.maxMemoryUsage)}`)
    }
    
    if (violations.length > 0) {
      this.handlePerformanceViolations(violations)
    }
  }
  
  private handlePerformanceViolations(violations: string[]): void {
    console.warn('⚠️ Performance violations detected:', violations)
    
    // Auto-optimize based on violations
    if (this.metrics.fps < this.targets.minFPS) {
      this.engine.setQuality('low')
      this.engine.reduceComplexity()
    }
    
    if (this.metrics.memoryUsage > this.targets.maxMemoryUsage * 0.9) {
      this.engine.cleanup()
      this.engine.enableAggressiveMemoryOptimization()
    }
  }
  
  private updateDashboard(): void {
    // Update UI elements with current metrics
    this.updateMetricDisplay('fps', this.metrics.fps, this.targets.minFPS)
    this.updateMetricDisplay('frame-time', this.metrics.frameTime, this.targets.maxFrameTime)
    this.updateMetricDisplay('memory', this.metrics.memoryUsage, this.targets.maxMemoryUsage)
    this.updateMetricDisplay('threats', this.metrics.threatCount, this.targets.maxThreatCount)
    this.updateMetricDisplay('components', this.metrics.componentCount, this.targets.maxComponentCount)
    this.updateMetricDisplay('emergent-behaviors', this.metrics.emergentBehaviorCount, this.targets.maxEmergentBehaviors)
  }
}
## 🚀 Production-Ready Advanced Example

### Complete Application with Error Handling, Monitoring, and Performance Optimization

**File**: [`src/examples/production/complete-application.ts`](src/examples/production/complete-application.ts:1)

```typescript
import { 
  GameEngine, 
  ThreatForgeError, 
  ErrorType,
  PerformanceMonitor,
  ErrorMonitor,
  ComponentInspector,
  ValidationUtils
} from '@threatforge/core'

export class CompleteThreatForgeApplication {
  private engine: GameEngine
  private performanceMonitor: PerformanceMonitor
  private errorMonitor: ErrorMonitor
  private componentInspector: ComponentInspector
  private isRunning: boolean = false
  private metrics: ApplicationMetrics = {
    threatsCreated: 0,
    emergentBehaviorsDiscovered: 0,
    performanceScore: 0,
    errorRate: 0,
    uptime: 0
  }

  constructor(private config: ApplicationConfig) {
    this.initializeApplication()
  }

  private async initializeApplication(): Promise<void> {
    console.log('🚀 Initializing ThreatForge Application...')
    
    try {
      // Step 1: Validate configuration
      await this.validateConfiguration()
      
      // Step 2: Initialize engine with comprehensive configuration
      this.engine = new GameEngine({
        performance: {
          quality: this.config.quality || 'balanced',
          targetFPS: this.config.targetFPS || 60,
          maxComponents: this.config.maxComponents || 1000,
          enableComponentPooling: true,
          memoryCleanupInterval: 5000,
          adaptiveQuality: true
        },
        rendering: {
          enabled: this.config.enableRendering !== false,
          quality: this.config.renderingQuality || 'balanced',
          antialias: true,
          shadows: true,
          maxLights: 50
        },
        debugging: {
          enabled: this.config.debugMode || false,
          logLevel: this.config.logLevel || 'INFO',
          enableInspector: true,
          enableProfiler: true
        },
        networking: {
          enabled: this.config.enableMultiplayer || false,
          syncRate: 30,
          maxLatency: 200
        }
      })

      // Step 3: Initialize monitoring systems
      await this.initializeMonitoring()
      
      // Step 4: Register custom components
      await this.registerCustomComponents()
      
      // Step 5: Setup error handling
      this.setupErrorHandling()
      
      // Step 6: Validate initialization
      await this.validateInitialization()
      
      console.log('✅ Application initialized successfully')
      
    } catch (error) {
      console.error('❌ Application initialization failed:', error)
      await this.handleInitializationError(error)
      throw error
    }
  }

  private async validateConfiguration(): Promise<void> {
    console.log('🔍 Validating application configuration...')
    
    const validation = ValidationUtils.validateApplicationConfig(this.config)
    
    if (!validation.isValid) {
      throw new ThreatForgeError(
        ErrorType.VALIDATION_ERROR,
        `Configuration validation failed: ${validation.errors.join('; ')}`,
        'CRITICAL',
        { errors: validation.errors }
      )
    }
    
    if (validation.warnings.length > 0) {
      console.warn('⚠️ Configuration warnings:', validation.warnings)
    }
    
    console.log('✅ Configuration validation passed')
  }

  private async initializeMonitoring(): Promise<void> {
    console.log('📊 Initializing monitoring systems...')
    
    // Performance monitoring
    this.performanceMonitor = new PerformanceMonitor(this.engine, {
      samplingRate: 1000, // 1 second
      metrics: ['fps', 'memory', 'componentCount', 'emergentBehaviorCount'],
      thresholds: {
        minFPS: 30,
        maxMemory: 2 * 1024 * 1024 * 1024, // 2GB
        maxComponentCount: 5000,
        maxEmergentBehaviorCount: 500
      }
    })
    
    // Error monitoring
    this.errorMonitor = new ErrorMonitor({
      maxErrorHistory: 1000,
      errorRateThreshold: 0.01, // 1% error rate
      enableRealTimeMonitoring: true
    })
    
    // Component inspector (development only)
    if (this.config.debugMode) {
      this.componentInspector = new ComponentInspector(this.engine)
      this.componentInspector.enable()
    }
    
    console.log('✅ Monitoring systems initialized')
  }

  private async registerCustomComponents(): Promise<void> {
    console.log('🔧 Registering custom components...')
    
    // Register quantum-neural interface component
    this.engine.componentRegistry.register('QUANTUM_NEURAL_INTERFACE', {
      type: 'QUANTUM_NEURAL_INTERFACE',
      domain: 'QUANTUM',
      emergencePotential: 0.95,
      behaviors: [
        new QuantumCoherenceBehavior(),
        new NeuralIntegrationBehavior(),
        new CognitiveEnhancementBehavior()
      ],
      properties: {
        quantumCoherence: 0.9,
        neuralBandwidth: 1000,
        interfaceStability: 0.85
      }
    }, {
      recommendedQuality: 'high',
      maxInstances: 50,
      memoryUsage: 2 * 1024 * 1024, // 2MB
      updateFrequency: 60
    })
    
    // Register adaptive AI system
    this.engine.componentRegistry.register('ADAPTIVE_AI_SYSTEM', {
      type: 'ADAPTIVE_AI_SYSTEM',
      domain: 'CYBER',
      emergencePotential: 0.98,
      behaviors: [
        new MachineLearningBehavior(),
        new SelfImprovementBehavior(),
        new CreativeProblemSolvingBehavior()
      ],
      properties: {
        neuralNetworkDepth: 15,
        learningCapability: 0.95,
        adaptationSpeed: 0.8
      }
    }, {
      recommendedQuality: 'high',
      maxInstances: 25,
      memoryUsage: 5 * 1024 * 1024, // 5MB
      updateFrequency: 30
    })
    
    console.log('✅ Custom components registered')
  }

  private setupErrorHandling(): void {
    console.log('🛡️ Setting up error handling...')
    
    // Global error handler
    this.engine.eventBus.on('error:occurred', (errorLog) => {
      this.handleError(errorLog)
    })
    
    // Performance warnings
    this.engine.eventBus.on('performance:warning', (metrics) => {
      this.handlePerformanceWarning(metrics)
    })
    
    // Memory warnings
    this.engine.eventBus.on('memory:warning', (usage) => {
      this.handleMemoryWarning(usage)
    })
    
    console.log('✅ Error handling configured')
  }

  private handleError(errorLog: ErrorLog): void {
    console.error(`❌ Error occurred: ${errorLog.type} - ${errorLog.message}`)
    
    // Record error in monitor
    this.errorMonitor.recordError(
      new ThreatForgeError(errorLog.type, errorLog.message, errorLog.severity, errorLog.context),
      { success: false, duration: 0 }
    )
    
    // Update metrics
    this.metrics.errorRate = this.errorMonitor.getErrorRate()
    
    // Take corrective action based on error type
    switch (errorLog.type) {
      case ErrorType.PERFORMANCE_DEGRADATION:
        this.handlePerformanceDegradation()
        break
      case ErrorType.MEMORY_LIMIT_EXCEEDED:
        this.handleMemoryLimitExceeded()
        break
      case ErrorType.COMPONENT_CREATION_FAILED:
        this.handleComponentCreationFailure(errorLog)
        break
      default:
        console.warn(`No specific handler for error type: ${errorLog.type}`)
    }
  }

  private handlePerformanceDegradation(): void {
    console.warn('⚠️ Performance degradation detected, taking corrective action...')
    
    // Reduce quality level
    const currentQuality = this.engine.getQuality()
    const qualityLevels = ['ultra', 'high', 'balanced', 'low', 'minimal']
    const currentIndex = qualityLevels.indexOf(currentQuality)
    
    if (currentIndex < qualityLevels.length - 1) {
      const newQuality = qualityLevels[currentIndex + 1]
      this.engine.setQuality(newQuality)
      console.log(`🔧 Reduced quality to ${newQuality}`)
    }
    
    // Reduce component complexity
    this.engine.reduceComplexity()
    
    // Clear non-essential components
    this.engine.cleanupNonEssentialComponents()
  }

  private handleMemoryLimitExceeded(): void {
    console.error('🚨 Memory limit exceeded, performing emergency cleanup...')
    
    // Trigger garbage collection
    if (global.gc) {
      global.gc()
    }
    
    // Clear component pools
    this.engine.clearComponentPools()
    
    // Reduce texture quality
    this.engine.setTextureQuality('low')
    
    // Disable non-essential features
    this.engine.disableNonEssentialFeatures()
  }

  async createComplexThreat(): Promise<ComposedThreat> {
    try {
      console.log('🧬 Creating complex multi-domain threat...')
      
      const startTime = performance.now()
      
      // Create sophisticated multi-domain threat
      const threat = await this.engine.composeThreat([
        // Quantum foundation
        {
          type: 'QUANTUM_ENTANGLEMENT',
          properties: {
            coherenceTime: 2000,
            entanglementStrength: 0.85,
            decoherenceResistance: 0.7
          }
        },
        // AI learning system
        {
          type: 'ADAPTIVE_AI_SYSTEM',
          properties: {
            learningRate: 0.15,
            neuralNetworkDepth: 12,
            creativityFactor: 0.8,
            selfModificationCapability: 0.9
          }
        },
        // Synthetic biology
        {
          type: 'SYNTHETIC_BIOLOGY',
          properties: {
            geneticComplexity: 0.9,
            replicationFidelity: 0.95,
            environmentalAdaptation: 0.8
          }
        },
        // Quantum network
        {
          type: 'QUANTUM_NETWORK',
          properties: {
            quantumNodes: 1000,
            entanglementDistribution: 0.9,
            quantumRepeaterEfficiency: 0.85
          }
        },
        // Neural interface
        {
          type: 'QUANTUM_NEURAL_INTERFACE',
          properties: {
            quantumCoherence: 0.95,
            neuralBandwidth: 2000,
            cognitiveDepth: 0.9
          }
        }
      ], {
        performance: {
          maxEmergentBehaviors: 50,
          complexity: 'advanced',
          quality: 'high'
        }
      })
      
      const creationTime = performance.now() - startTime
      
      // Validate threat creation
      if (!threat || !threat.id) {
        throw new Error('Complex threat creation failed')
      }
      
      // Update metrics
      this.metrics.threatsCreated++
      this.metrics.emergentBehaviorsDiscovered += threat.emergentBehaviors.length
      
      console.log('✅ Complex threat created successfully')
      console.log(`🆔 Threat ID: ${threat.id}`)
      console.log(`🧬 Components: ${threat.components.length}`)
      console.log(`⚡ Emergent Behaviors: ${threat.emergentBehaviors.length}`)
      console.log(`⏱️ Creation Time: ${creationTime.toFixed(2)}ms`)
      console.log(`🔍 System Complexity: ${threat.systemComplexity}`)
      
      // Analyze emergent properties
      const analysis = threat.analyzeEmergentProperties()
      console.log(`🌟 Novel Capabilities: ${analysis.novelCapabilities.length}`)
      console.log(`🎲 Unpredictability: ${(analysis.unpredictabilityScore * 100).toFixed(1)}%`)
      console.log(`📈 Evolution Potential: ${(analysis.evolutionPotential * 100).toFixed(1)}%`)
      
      // Log emergent behaviors
      if (threat.emergentBehaviors.length > 0) {
        console.log('\n🧬 Discovered Emergent Behaviors:')
        threat.emergentBehaviors.forEach((behavior, index) => {
          console.log(`  ${index + 1}. ${behavior.name}`)
          console.log(`     Description: ${behavior.description}`)
          console.log(`     Impact Level: ${behavior.impactLevel}`)
          console.log(`     Predictability: ${(behavior.predictability * 100).toFixed(1)}%`)
        })
      }
      
      return threat
      
    } catch (error) {
      console.error('❌ Complex threat creation failed:', error)
      throw error
    }
  }

  async runPerformanceBenchmark(): Promise<BenchmarkReport> {
    console.log('🏃 Running performance benchmark...')
    
    try {
      const benchmark = new PerformanceBenchmark(this.engine)
      const report = await benchmark.runBenchmarks()
      
      // Update metrics
      this.metrics.performanceScore = report.overallScore
      
      console.log('📊 Performance Benchmark Results:')
      console.log(`Overall Score: ${(report.overallScore * 100).toFixed(1)}%`)
      console.log(`Status: ${report.passed ? '✅ PASSED' : '❌ FAILED'}`)
      
      report.results.forEach(result => {
        console.log(`  ${result.passed ? '✅' : '❌'} ${result.name}: ${result.achieved} (target: ${result.target})`)
      })
      
      if (!report.passed) {
        console.warn('⚠️ Some benchmarks failed. Consider optimization.')
      }
      
      return report
      
    } catch (error) {
      console.error('❌ Performance benchmark failed:', error)
      throw error
    }
  }

  start(): void {
    if (this.isRunning) {
      console.warn('Application is already running')
      return
    }
    
    console.log('▶️ Starting ThreatForge application...')
    
    this.isRunning = true
    this.metrics.startTime = Date.now()
    
    // Start monitoring systems
    this.performanceMonitor.start()
    
    // Start metrics collection
    this.startMetricsCollection()
    
    console.log('✅ Application started successfully')
  }

  stop(): void {
    if (!this.isRunning) {
      console.warn('Application is not running')
      return
    }
    
    console.log('⏹️ Stopping ThreatForge application...')
    
    this.isRunning = false
    
    // Stop monitoring systems
    this.performanceMonitor.stop()
    
    // Generate final report
    this.generateFinalReport()
    
    console.log('✅ Application stopped successfully')
  }

  private startMetricsCollection(): void {
    const metricsInterval = setInterval(() => {
      if (!this.isRunning) {
        clearInterval(metricsInterval)
        return
      }
      
      // Update uptime
      this.metrics.uptime = Date.now() - (this.metrics.startTime || 0)
      
      // Get current performance metrics
      const performanceMetrics = this.performanceMonitor.getMetrics()
      this.metrics.performanceScore = performanceMetrics.overallScore
      
      // Get error rate
      this.metrics.errorRate = this.errorMonitor.getErrorRate()
      
      // Log metrics periodically
      if (this.config.debugMode) {
        console.log('📈 Application Metrics:', {
          uptime: this.formatUptime(this.metrics.uptime),
          threatsCreated: this.metrics.threatsCreated,
          emergentBehaviors: this.metrics.emergentBehaviorsDiscovered,
          performanceScore: `${(this.metrics.performanceScore * 100).toFixed(1)}%`,
          errorRate: `${(this.metrics.errorRate * 100).toFixed(2)}%`
        })
      }
    }, 30000) // Every 30 seconds
  }

  private generateFinalReport(): void {
    console.log('\n📋 Final Application Report:')
    console.log(`⏱️ Total Uptime: ${this.formatUptime(this.metrics.uptime)}`)
    console.log(`🎯 Threats Created: ${this.metrics.threatsCreated}`)
    console.log(`🧬 Emergent Behaviors: ${this.metrics.emergentBehaviorsDiscovered}`)
    console.log(`🏆 Performance Score: ${(this.metrics.performanceScore * 100).toFixed(1)}%`)
    console.log(`⚠️ Error Rate: ${(this.metrics.errorRate * 100).toFixed(2)}%`)
    
    // Generate error report
    const errorReport = this.errorMonitor.getErrorReport()
    if (errorReport.totalErrors > 0) {
      console.log(`❌ Total Errors: ${errorReport.totalErrors}`)
      console.log('🔧 Recommendations:', errorReport.recommendations)
    }
  }

  private formatUptime(ms: number): string {
    const seconds = Math.floor(ms / 1000)
    const minutes = Math.floor(seconds / 60)
    const hours = Math.floor(minutes / 60)
    const days = Math.floor(hours / 24)
    
    if (days > 0) return `${days}d ${hours % 24}h ${minutes % 60}m`
    if (hours > 0) return `${hours}h ${minutes % 60}m`
    if (minutes > 0) return `${minutes}m ${seconds % 60}s`
    return `${seconds}s`
  }
}

// Usage example
async function runProductionExample(): Promise<void> {
  console.log('🚀 Starting Production ThreatForge Example...')
  
  const app = new CompleteThreatForgeApplication({
    quality: 'high',
    targetFPS: 60,
    maxComponents: 1000,
    enableRendering: true,
    renderingQuality: 'high',
    debugMode: true,
    logLevel: 'INFO',
    enableMultiplayer: false
  })
  
  try {
    // Start the application
    app.start()
    
    // Wait a moment for systems to initialize
    await new Promise(resolve => setTimeout(resolve, 1000))
    
    // Create a complex threat
    const complexThreat = await app.createComplexThreat()
    
    // Run performance benchmark
    const benchmarkReport = await app.runPerformanceBenchmark()
    
    // Let it run for a bit
    await new Promise(resolve => setTimeout(resolve, 5000))
    
    // Stop the application
    app.stop()
    
    console.log('✅ Production example completed successfully')
    
  } catch (error) {
    console.error('❌ Production example failed:', error)
    app.stop()
    throw error
  }
}

// Run the production example
runProductionExample().then(() => {
  console.log('🎉 All production examples completed!')
}).catch((error) => {
  console.error('💥 Production example failed:', error)
  process.exit(1)
})
```

## 🎯 Key Production Features Demonstrated

### 1. **Comprehensive Error Handling**
- Custom error types with severity levels
- Automatic recovery strategies
- Graceful degradation
- Detailed error logging and monitoring

### 2. **Advanced Performance Monitoring**
- Real-time FPS monitoring
- Memory usage tracking
- Component performance profiling
- Automatic quality adjustment

### 3. **Production-Grade Validation**
- Configuration validation
- Input sanitization
- Runtime validation
- Comprehensive testing framework

### 4. **Scalable Architecture**
- Component pooling
- Memory management
- Quality adaptation
- Load balancing

### 5. **Developer Experience**
- Component inspector
- Performance profiler
- Detailed logging
- Debugging tools

### 6. **Operational Excellence**
- Metrics collection
- Health monitoring
- Automated reporting
- Graceful shutdown

This production-ready example demonstrates how to build a robust, scalable, and maintainable ThreatForge application with enterprise-grade features and comprehensive error handling.
```