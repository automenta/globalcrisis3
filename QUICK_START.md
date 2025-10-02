# ThreatForge Quick Start Guide 🚀

## Overview

This guide will take you from zero to creating your first emergent threats in under 10 minutes. We'll build progressively more complex examples while learning the core concepts of component-based threat composition.

## Prerequisites

- Basic JavaScript/TypeScript knowledge
- Node.js 16+ installed
- A modern web browser (Chrome 90+, Firefox 88+, Safari 14+)

## Step 1: Setup (2 minutes)

### Install ThreatForge

```bash
# Clone the repository
git clone https://github.com/threatforge/engine.git
cd engine

# Install dependencies
npm install

# Start development server
npm run dev

# Open http://localhost:5173 in your browser
```

### Verify Installation

Open the browser console and you should see:
```
🎯 ThreatForge Engine v1.0.0 initialized
⚡ Performance: Adaptive quality enabled
🧩 Component registry loaded with 50+ components
```

## Step 2: Your First Threat (3 minutes)

### Tier 1: Simple Biological Threat

```typescript
// Import the core engine
import { GameEngine } from '@threatforge/core'

// Create engine instance with default settings
const engine = new GameEngine()

// Compose your first threat - a simple biological infection
const basicThreat = engine.composeThreat([
  {
    type: 'BIOLOGICAL_INFECTION',
    properties: {
      transmissionRate: 0.5,
      severity: 0.3
    }
  }
])

console.log('🦠 Basic threat created!')
console.log(`Components: ${basicThreat.components.length}`)
console.log(`Emergent behaviors: ${basicThreat.emergentBehaviors.length}`)
```

**Expected Output:**
```
🦠 Basic threat created!
Components: 1
Emergent behaviors: 0
```

### Tier 2: Adding Transmission

```typescript
// Create a more realistic pandemic threat
const pandemic = engine.composeThreat([
  {
    type: 'BIOLOGICAL_INFECTION',
    properties: {
      transmissionRate: 0.7,
      incubationPeriod: 5,
      severity: 0.4
    }
  },
  {
    type: 'AIRBORNE_TRANSMISSION',
    properties: {
      range: 1000,
      seasonalVariation: true
    }
  }
])

console.log('🌍 Pandemic threat created!')
console.log(`Components: ${pandemic.components.length}`)
console.log(`Emergent behaviors: ${pandemic.emergentBehaviors.length}`)

// Check for emergent behaviors
if (pandemic.emergentBehaviors.length > 0) {
  console.log('✨ Emergent behaviors discovered:')
  pandemic.emergentBehaviors.forEach(behavior => {
    console.log(`  - ${behavior.name}: ${behavior.description}`)
  })
}
```

**Expected Output:**
```
🌍 Pandemic threat created!
Components: 2
Emergent behaviors: 1
✨ Emergent behaviors discovered:
  - Seasonal Transmission Pattern: Infection rate varies with seasons
```

## Step 3: Cross-Domain Interactions (3 minutes)

### Tier 3: Cyber-Biological Hybrid

```typescript
// Create a sophisticated cyber-biological threat
const cyberBioThreat = engine.composeThreat([
  {
    type: 'BIOLOGICAL_INFECTION',
    properties: {
      transmissionRate: 0.6,
      mutationPotential: 0.3
    }
  },
  {
    type: 'NETWORK_PROPAGATION',
    properties: {
      spreadVector: 'social_media',
      viralCoefficient: 1.5
    }
  },
  {
    type: 'COGNITIVE_MANIPULATION',
    properties: {
      influenceStrength: 0.8,
      stealthLevel: 0.7
    }
  }
])

console.log('🔬 Cyber-biological threat created!')
console.log(`Components: ${cyberBioThreat.components.length}`)
console.log(`Emergent behaviors: ${cyberBioThreat.emergentBehaviors.length}`)

// Analyze the emergent behaviors
cyberBioThreat.emergentBehaviors.forEach(behavior => {
  console.log(`🧬 ${behavior.name}:`)
  console.log(`   ${behavior.description}`)
  console.log(`   Impact: ${behavior.impactLevel}`)
})
```

**Expected Output:**
```
🔬 Cyber-biological threat created!
Components: 3
Emergent behaviors: 2
🧬 Information Cascade:
   Disinformation accelerates biological spread through social networks
   Impact: HIGH
🧬 Cognitive Resistance Reduction:
   Fear and confusion make populations more susceptible to infection
   Impact: MEDIUM
```

## Step 4: Advanced Composition (2 minutes)

### Tier 4: Multi-Domain Synthesis

```typescript
// Create a complex multi-domain threat
const syntheticThreat = engine.composeThreat([
  // Quantum foundation
  {
    type: 'QUANTUM_ENTANGLEMENT',
    properties: {
      coherenceTime: 1500,
      entanglementStrength: 0.9
    }
  },
  // Biological component
  {
    type: 'BIOLOGICAL_INFECTION',
    properties: {
      transmissionRate: 0.8,
      mutationPotential: 0.5
    }
  },
  // AI learning
  {
    type: 'AI_LEARNING',
    properties: {
      learningRate: 0.1,
      creativityFactor: 0.7
    }
  },
  // Network infrastructure
  {
    type: 'NETWORK_INFRASTRUCTURE',
    properties: {
      coverage: 0.95,
      bandwidth: 'high'
    }
  }
], {
  performance: {
    quality: 'high',
    maxEmergentBehaviors: 10
  }
})

console.log('🌌 Multi-domain synthetic threat created!')
console.log(`Components: ${syntheticThreat.components.length}`)
console.log(`Emergent behaviors: ${syntheticThreat.emergentBehaviors.length}`)

// Performance metrics
console.log(`⚡ Performance: ${syntheticThreat.performanceMetrics.currentFPS} FPS`)
console.log(`🔧 Quality: ${syntheticThreat.qualitySettings.renderQuality}`)
```

**Expected Output:**
```
🌌 Multi-domain synthetic threat created!
Components: 4
Emergent behaviors: 5
⚡ Performance: 58 FPS
🔧 Quality: HIGH
```

## Step 5: Performance Optimization (Optional)

### Adaptive Performance Settings

```typescript
// Create engine with custom performance settings
const optimizedEngine = new GameEngine({
  performance: {
    quality: 'adaptive',        // Auto-adjust based on hardware
    targetFPS: 60,              // Target frame rate
    detailLevel: 'auto',        // Auto detail level
    maxEmergentBehaviors: 50,   // Limit complexity
    memoryLimit: 'adaptive'     // Adaptive memory management
  }
})

// Monitor performance in real-time
optimizedEngine.on('performance:warning', (metrics) => {
  console.log(`⚠️ Performance warning: ${metrics.fps} FPS`)
  console.log(`Reducing quality to maintain target performance`)
})

optimizedEngine.on('performance:optimized', (metrics) => {
  console.log(`✅ Performance optimized: ${metrics.fps} FPS`)
  console.log(`Quality level: ${metrics.quality}`)
})
```

## Common Patterns

### Pattern 1: Pandemic Simulation
```typescript
const pandemic = engine.composeThreat([
  { type: 'BIOLOGICAL_INFECTION', properties: { transmissionRate: 0.7 } },
  { type: 'AIRBORNE_TRANSMISSION', properties: { range: 800 } },
  { type: 'MUTATION_ENGINE', properties: { rate: 0.001 } }
])
```

### Pattern 2: Cyber Attack
```typescript
const cyberAttack = engine.composeThreat([
  { type: 'NETWORK_PROPAGATION', properties: { spreadVector: 'email' } },
  { type: 'DATA_CORRUPTION', properties: { severity: 0.8 } },
  { type: 'STEALTH_MECHANISM', properties: { detectionDifficulty: 0.9 } }
])
```

### Pattern 3: Environmental Disaster
```typescript
const disaster = engine.composeThreat([
  { type: 'WEATHER_SYSTEM', properties: { intensity: 0.9 } },
  { type: 'CONTAMINATION', properties: { spreadRate: 0.6 } },
  { type: 'INFRASTRUCTURE_DAMAGE', properties: { cascadePotential: 0.7 } }
])
```

## Troubleshooting

### Common Issues

**Issue: "Component not found"**
```typescript
// ❌ Wrong component type
const threat = engine.composeThreat([
  { type: 'INVALID_COMPONENT', properties: {} }
])

// ✅ Use valid component types
const threat = engine.composeThreat([
  { type: 'BIOLOGICAL_INFECTION', properties: {} }
])
```

**Issue: Poor performance**
```typescript
// ❌ Too many complex components
const threat = engine.composeThreat([
  // 20+ high-complexity components
])

// ✅ Limit complexity and use adaptive quality
const threat = engine.composeThreat([
  { type: 'BIOLOGICAL_INFECTION', properties: {} },
  { type: 'AIRBORNE_TRANSMISSION', properties: {} }
], {
  performance: {
    quality: 'adaptive',
    maxEmergentBehaviors: 10
  }
})
```

**Issue: No emergent behaviors**
```typescript
// ❌ Single domain components
const threat = engine.composeThreat([
  { type: 'BIOLOGICAL_INFECTION', properties: {} },
  { type: 'HEALTH_IMPACT', properties: {} }
])

// ✅ Mix different domains
const threat = engine.composeThreat([
  { type: 'BIOLOGICAL_INFECTION', properties: {} },
  { type: 'NETWORK_PROPAGATION', properties: {} } // Different domain
])
```

## Next Steps

Now that you've created your first threats, explore these advanced topics:

- **[Component Architecture](COMPONENT_ARCHITECTURE.md)**: Deep dive into the component system
- **[Code Examples](CODE_EXAMPLES.md)**: More complex examples and patterns
- **[Performance Optimization](PERFORMANCE_OPTIMIZATION.md)**: Advanced performance tuning
- **[Development Tools](DEVELOPMENT_GUIDE.md)**: Inspector and debugging tools

## Getting Help

- **Community Forum**: [GitHub Discussions](https://github.com/threatforge/engine/discussions)
- **Issue Tracker**: [GitHub Issues](https://github.com/threatforge/engine/issues)
- **Documentation**: Check the [full documentation](DOCUMENTATION_INDEX.md)

**Happy threat composing!** 🎯

## Enhanced Educational Framework: Scientific Discovery Learning

### Learning Progression with Measurable Outcomes

#### Stage 1: Atomic Component Understanding
**Learning Objectives:**
- Identify basic threat components and their scientific properties
- Predict individual component behaviors using scientific reasoning
- Apply systematic observation and documentation skills

**Discovery Activities:**
```typescript
// Scientific observation framework
const observationFramework = {
  hypothesis: "Single components exhibit predictable behaviors",
  variables: {
    independent: "componentType",
    dependent: "behaviorOutcome",
    controlled: ["environment", "timeScale", "initialConditions"]
  },
  measurement: {
    behaviorMetrics: ["transmissionRate", "severity", "spreadPattern"],
    observationFrequency: "real-time",
    dataCollection: "automatedLogging"
  }
};

// Guided discovery experiment
const experiment = engine.createScientificExperiment({
  hypothesis: "Biological infection components follow epidemiological models",
  component: "BIOLOGICAL_INFECTION",
  parameters: {
    transmissionRate: { min: 0.1, max: 0.9, step: 0.1 },
    severity: { min: 0.1, max: 0.9, step: 0.1 }
  },
  measurements: ["infectionSpread", "populationImpact", "timeToPeak"]
});

// Run experiment and collect data
const results = await experiment.run();
const analysis = experiment.analyzeResults(results);
```

**Assessment Criteria:**
- [ ] Correctly identify component properties (80% accuracy)
- [ ] Predict basic component behavior (75% accuracy)
- [ ] Document observations using scientific format
- [ ] Formulate testable hypotheses about component behavior

#### Stage 2: Component Interaction Discovery
**Learning Objectives:**
- Discover how components interact through systematic experimentation
- Identify patterns in cross-domain interactions
- Apply statistical analysis to interaction outcomes

**Scientific Method Application:**
```typescript
// Hypothesis-driven interaction discovery
const interactionExperiment = {
  hypothesis: "Cross-domain components create emergent behaviors not predictable from individual components",
  prediction: "Cyber-biological combinations will produce 2-3 emergent behaviors",
  experimentalDesign: {
    controlGroup: "Single-domain components only",
    experimentalGroup: "Cross-domain component combinations",
    sampleSize: 10, // Multiple trials for statistical validity
    randomization: "Random component selection and ordering"
  }
};

// Run controlled experiment
const controlResults = engine.runInteractionStudy({
  components: ["BIOLOGICAL_INFECTION"], // Single domain
  trials: 10,
  measurements: ["emergentBehaviors", "interactionStrength", "unpredictabilityScore"]
});

const experimentalResults = engine.runInteractionStudy({
  components: ["BIOLOGICAL_INFECTION", "NETWORK_PROPAGATION"], // Cross-domain
  trials: 10,
  measurements: ["emergentBehaviors", "interactionStrength", "unpredictabilityScore"]
});

// Statistical analysis
const statisticalAnalysis = engine.analyzeInteractionData({
  control: controlResults,
  experimental: experimentalResults,
  test: "mannWhitneyU", // Non-parametric test for small samples
  significanceLevel: 0.05
});
```

#### Stage 3: Complex System Analysis
**Learning Objectives:**
- Analyze multi-component systems using systems thinking
- Identify feedback loops and cascading effects
- Predict system-level behaviors from component interactions

**Systems Thinking Framework:**
```typescript
// Complex system analysis tools
const systemAnalysis = {
  componentInventory: "Catalog all system components",
  interactionMapping: "Map all pairwise interactions",
  feedbackLoopIdentification: "Identify reinforcing and balancing loops",
  emergencePrediction: "Predict system-level behaviors",
  validationTesting: "Test predictions against observations"
};

// Multi-domain synthesis experiment
const complexSystemExperiment = engine.designComplexSystemStudy({
  researchQuestion: "How do quantum, biological, and cyber domains interact to create unprecedented threat behaviors?",
  systemComponents: [
    "QUANTUM_ENTANGLEMENT",
    "BIOLOGICAL_INFECTION", 
    "AI_LEARNING",
    "NETWORK_INFRASTRUCTURE"
  ],
  investigationMethods: [
    "componentInteractionAnalysis",
    "emergentBehaviorIdentification",
    "systemDynamicsModeling",
    "predictiveValidation"
  ],
  successCriteria: {
    minEmergentBehaviors: 3,
    unpredictabilityThreshold: 0.7,
    crossDomainInteractions: ">50%",
    reproducibility: ">80%"
  }
});
```

### Educational Assessment and Validation

#### Knowledge Assessment Framework
```typescript
interface LearningAssessment {
  preAssessment: KnowledgeBaseline;
  formativeAssessment: ProgressCheckpoint[];
  summativeAssessment: ComprehensiveEvaluation;
  retentionTesting: LongTermRetentionStudy;
  transferAssessment: SkillTransferEvaluation;
}

class ScientificLearningAssessment {
  assessKnowledgeGains(learnerId: string, learningPath: LearningStage[]): AssessmentResult {
    const baseline = this.establishBaseline(learnerId);
    const progress = this.trackProgress(learnerId, learningPath);
    const finalAssessment = this.conductFinalAssessment(learnerId);
    
    return {
      knowledgeGain: this.calculateKnowledgeGain(baseline, finalAssessment),
      skillDevelopment: this.evaluateSkillProgression(progress),
      scientificThinking: this.assessScientificMethodApplication(learnerId),
      retentionRate: this.measureRetention(learnerId, "30-day"),
      transferSuccess: this.evaluateLearningTransfer(learnerId)
    };
  }
}
```

#### Real-World Connection Activities
```typescript
// Connect learning to real-world applications
const realWorldConnections = {
  epidemiology: "Apply component thinking to disease outbreak analysis",
  cybersecurity: "Use cross-domain thinking for advanced persistent threat analysis",
  climateScience: "Apply emergence concepts to climate system modeling",
  economics: "Use interaction analysis for market behavior prediction",
  artificialIntelligence: "Apply emergence principles to AI safety research"
};

// Career skill development
const careerSkills = {
  systemsThinking: "Analyze complex interconnected problems",
  scientificMethod: "Apply hypothesis-driven problem solving",
  dataAnalysis: "Use statistical methods for decision making",
  crossDomainExpertise: "Work effectively across disciplinary boundaries",
  emergentThinking: "Predict and manage unexpected system behaviors"
};
```

### Entertainment Through Discovery

#### Gamified Learning Mechanics
```typescript
// Discovery-based achievements
const discoveryAchievements = {
  firstEmergence: "Discover your first emergent behavior",
  crossDomainMaster: "Create threats spanning 3+ domains",
  unpredictabilityExpert: "Achieve >90% unpredictability score",
  scientificMethod: "Complete full hypothesis-testing cycle",
  reproducibilityChampion: "Reproduce 10 emergent behaviors"
};

// Competitive discovery challenges
const discoveryChallenges = {
  speedDiscovery: "Find 5 emergent behaviors in shortest time",
  complexityMaster: "Create threat with highest complexity score",
  innovationChallenge: "Discover completely new interaction pattern",
  efficiencyExpert: "Achieve learning objectives with minimal resources",
  teachingChallenge: "Help another learner discover emergent behavior"
};
```

This enhanced educational framework transforms the quick start guide into a comprehensive scientific learning experience that develops genuine expertise in complex systems analysis while maintaining engagement through discovery-based learning and gamification.