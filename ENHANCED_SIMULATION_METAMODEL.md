# Enhanced Simulation Metamodel: A Unified Component Ecosystem

## 1. Executive Summary

This document presents the definitive, enhanced simulation metamodel for ThreatForge. It establishes a complete, scientifically-grounded ecosystem by unifying **Threats** and **Threatenables** under a single, component-based architecture. This model integrates advanced concepts such as co-evolution, scientific validation, and performance-aware design to enable highly realistic and emergent gameplay. It supersedes and consolidates previous architectural documents.

## 2. Core Principle: The Unified Ecosystem

The simulation is a complete ecosystem where threats and threatenables co-exist and co-evolve. Both are first-class citizens, composed from the same pool of atomic, scientifically-grounded components.

```
[ Threat Components ] <--- Interaction ---> [ Threatenable Components ]
        ^                                           ^
        | Co-evolution                              | Co-evolution
        |                                           |
        +------------------[ Environment ]----------+
```

-   **Emergence:** Complex, unpredictable behaviors arise from the interaction of simple, predictable components.
-   **Realism:** Component properties and interactions are based on scientific principles and real-world data.
-   **Balance:** The simulation is not just about attack, but also about defense, adaptation, and resilience.

## 3. The Enhanced Component Architecture

Every object in the simulation is an `Entity` composed of `Components`. This section defines the enhanced interfaces for these core building blocks.

### 3.1. Enhanced Threat Component

A Threat Component represents an active element or "attack vector."

```typescript
interface EnhancedThreatComponent {
  id: string;
  type: string; // e.g., 'BIOLOGICAL_INFECTION', 'NETWORK_PROPAGATION'
  
  // Scientific Classification
  scientific: {
    domain: ScientificDomain; // e.g., 'MOLECULAR_BIOLOGY', 'COMPUTER_SCIENCE'
    theoreticalBasis: string[]; // Foundational principles, e.g., ['GermTheory', 'GraphTheory']
    empiricalSupport: number; // 0-1 scale of real-world evidence
  };
  
  // Dynamic Properties
  temporal: {
    activationDelay: number; // Time before component becomes active
    decayFunction: 'EXPONENTIAL' | 'LINEAR'; // How effect diminishes over time
    persistence: number; // Resistance to decay
  };
  spatial: {
    propagationModel: 'DIFFUSION' | 'NETWORK' | 'VECTOR';
    range: (context: any) => number; // Range can be dynamic
  };
  
  // Performance Profile
  performance: {
    computationalComplexity: 'O(1)' | 'O(n)' | 'O(n²)';
    memoryFootprintMB: number;
    qualityScaling: boolean; // Can this component be simplified under load?
  };
  
  // Validation & Testing Data
  validation: {
    statisticalConfidence: number; // p-value or similar metric
    reproducibilityScore: number; // 0-1 scale
    realWorldCaseStudies: string[]; // e.g., ['Stuxnet', 'COVID-19']
  };
}
```

### 3.2. Enhanced Threatenable Component

A Threatenable Component represents a passive property of an entity, defining its vulnerabilities, resistances, and adaptive capabilities.

```typescript
interface EnhancedThreatenableComponent {
  id:string;
  type: 'VULNERABILITY' | 'RESISTANCE' | 'ADAPTIVE_BEHAVIOR';
  
  // Scientific Classification
  scientific: {
    domain: ScientificDomain;
    theoreticalBasis: string[];
  };

  // Component-specific properties
  properties: Record<string, any>; // e.g., { damageType: 'FIRE', multiplier: 2.0 }
  
  // Behavior & Interaction Logic
  // Defines how this component reacts to a threat interaction
  onInteraction: (interaction: ScientificInteraction) => InteractionResult;
  
  // Performance Profile
  performance: {
    computationalComplexity: 'O(1)' | 'O(n)';
    memoryFootprintMB: number;
  };
}
```

**Example Threatenable Components:**

-   **Vulnerability:** `{ type: 'VULNERABILITY', properties: { damageType: 'CYBER', exploitability: 0.8 } }`
-   **Resistance:** `{ type: 'RESISTANCE', properties: { damageType: 'BIOLOGICAL', effectiveness: 0.9 } }`
-   **Adaptive Behavior:** `{ type: 'ADAPTIVE_BEHAVIOR', properties: { learningRate: 0.1, responseType: 'QUARANTINE' } }`

## 4. The Scientific Interaction Model

Interactions are the heart of the simulation. The outcome of an interaction is not hardcoded but calculated based on the scientific properties of the participating components.

```typescript
interface ScientificInteraction {
  id: string;
  sourceComponent: EnhancedThreatComponent;
  targetComponent: EnhancedThreatenableComponent;
  
  // Calculated Interaction Properties
  intensity: number; // 0-1 scale, calculated strength of the interaction
  mechanism: InteractionMechanism; // e.g., 'CONTACT_TRANSMISSION', 'CASCADE_FAILURE'
  
  // Bidirectional Effects
  // The outcome of the interaction
  effects: {
    onThreat: ThreatModification[]; // Threat may evolve
    onThreatenable: ThreatenableModification[]; // Threatenable may be damaged/adapt
  };
  
  // Validation of the interaction itself
  validation: {
    statisticalSignificance: number;
    realWorldAnalogue: string; // e.g., 'Ransomware encrypting hospital network'
  };
}
```

### Interaction Calculation

The `InteractionEngine` calculates the outcome when a threat encounters a threatenable.

**Example Calculation Flow:**
1.  A `Threat` entity (e.g., a virus) is proximate to a `Threatenable` entity (e.g., a population).
2.  The engine iterates through the threat's components (e.g., `AirbornePropagation`) and the threatenable's components (e.g., `DiseaseSusceptibility`).
3.  For each pair, it calculates an `intensity` based on scientific compatibility. `AirbornePropagation` has high compatibility with `DiseaseSusceptibility`.
4.  It then checks for `Resistance` components on the threatenable (e.g., `VaccinationImmunity`). The resistance's `effectiveness` reduces the final interaction `intensity`.
5.  The final `intensity` determines the `effects`. A high intensity might damage the population's `Health` property.
6.  The interaction may also trigger an `AdaptiveBehavior` component on the population, such as `SocialDistancing`, which adds a temporary `Resistance` component to nearby population entities.

## 5. Co-evolution Mechanics

Threats and threatenables are not static; they adapt to each other over time, creating a dynamic arms race.

-   **Threat Evolution:** If a threat's `effects` are consistently mitigated by a specific `Resistance` (e.g., an antibiotic), its `Mutation` component may trigger, altering its properties to bypass the resistance.
-   **Threatenable Adaptation:** If a threatenable is repeatedly damaged by a specific `Threat` type, its `AdaptiveBehavior` component may activate. For a power grid, this could mean automatically rerouting power to bypass a vulnerable node. For a population, it could mean developing herd immunity.

This co-evolutionary process ensures that the simulation remains dynamic and unpredictable, as new strategies and vulnerabilities emerge organically.

## 6. Metamodel Implementation Examples

### Example 1: Cyber Attack on Infrastructure

**The Threat: AI-Powered Worm**
-   `Entity`: "APT-QuantumLeap"
-   `Components`:
    -   `EnhancedThreatComponent (NetworkPropagation)`: `scientific.domain: 'COMPUTER_SCIENCE'`, `spatial.propagationModel: 'NETWORK'`.
    -   `EnhancedThreatComponent (AILearning)`: `scientific.domain: 'INFORMATION_THEORY'`, `properties: { adaptationSpeed: 0.8 }`.
    -   `EnhancedThreatComponent (Payload)`: `properties: { effect: 'SYSTEM_SHUTDOWN' }`.

**The Threatenable: National Power Grid**
-   `Entity`: "National Power Grid"
-   `Components`:
    -   `EnhancedThreatenableComponent (VULNERABILITY)`: `properties: { damageType: 'CYBER', exposure: 0.9, type: 'LegacySCADASystem' }`.
    -   `EnhancedThreatenableComponent (RESISTANCE)`: `properties: { damageType: 'CYBER', effectiveness: 0.7, type: 'IntrusionDetectionSystem' }`.
    -   `EnhancedThreatenableComponent (ADAPTIVE_BEHAVIOR)`: `properties: { responseType: 'ISOLATE_SUBNET', trigger: 'onAnomalyDetection' }`.

**Emergent Gameplay:**
1.  The worm's `NetworkPropagation` component exploits the grid's `LegacySCADASystem` vulnerability.
2.  The grid's `IntrusionDetectionSystem` resistance mitigates the initial spread, but the worm's `AILearning` component adapts its signature to bypass the IDS.
3.  As the worm spreads, the `Payload` component begins to trigger system shutdowns.
4.  This triggers the grid's `ISOLATE_SUBNET` adaptive behavior, which fights the infection by sacrificing parts of the grid, leading to rolling blackouts. The player must now manage a partially-crippled power grid while trying to contain a constantly evolving AI threat.

### Example 2: Bio-Threat in a Population

**The Threat: Engineered Pathogen**
-   `Entity`: "Hemlock Virus"
-   `Components`:
    -   `EnhancedThreatComponent (AirborneTransmission)`: `spatial.range: (context) => context.isUrban ? 500 : 100`.
    -   `EnhancedThreatComponent (CellularDamage)`: `properties: { severity: 0.8 }`.
    -   `EnhancedThreatComponent (MutationEngine)`: `properties: { rate: 0.05 }`.

**The Threatenable: Urban Population**
-   `Entity`: "City Center Population"
-   `Components`:
    -   `EnhancedThreatenableComponent (VULNERABILITY)`: `properties: { damageType: 'BIOLOGICAL', type: 'HighPopulationDensity' }`.
    -   `EnhancedThreatenableComponent (RESISTANCE)`: `properties: { damageType: 'BIOLOGICAL', effectiveness: 0.4, type: 'BaselineImmunity' }`.
    -   `EnhancedThreatenableComponent (ADAPTIVE_BEHAVIOR)`: `properties: { responseType: 'DevelopVaccine', learningRate: 0.01 }`.

**Emergent Gameplay:**
1.  The virus spreads rapidly due to the `HighPopulationDensity` vulnerability.
2.  The population's `BaselineImmunity` resistance is only partially effective.
3.  The high number of infections gives the `MutationEngine` many opportunities to activate, creating a new, more virulent strain.
4.  The population's `DevelopVaccine` behavior begins, but its slow `learningRate` means it's a race against the mutating virus. The player must implement temporary measures (like social distancing, another adaptive behavior) to slow the spread and buy time for the vaccine to be developed.
