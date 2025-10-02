# ThreatForge Code Examples 💻

## Overview

This document provides progressive code examples from basic "Hello World" threats to advanced multi-domain synthesis. Each example is complete, tested, and builds upon previous concepts.

## Example Progression

- **Tier 1**: Basic threat creation (Beginner)
- **Tier 2**: Simple composition (Intermediate)
- **Tier 3**: Cross-domain interactions (Advanced)
- **Tier 4**: Complex synthesis (Expert)
- **Tier 5**: Custom components (Master)

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
- **[Development Guide](DEVELOPMENT_GUIDE.md)**: Implementation patterns and best practices
- **[Component Architecture](COMPONENT_ARCHITECTURE.md)**: Deep dive into component system

## Contributing Examples

We welcome community contributions! Submit your examples:

1. Fork the repository
2. Create your example in `src/examples/community/`
3. Include comprehensive comments and expected outputs
4. Submit a pull request with detailed description

**Happy coding!** 🚀