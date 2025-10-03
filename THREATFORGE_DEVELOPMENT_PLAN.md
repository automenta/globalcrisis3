# ThreatForge: Development Plan

## 1. Executive Summary

ThreatForge is an entertaining educational simulation game designed for the browser. It leverages a component-based architecture to model complex, emergent phenomena in a fully destructible, unified 3D world. Players will interact with a rich ecosystem of "threats" (weapons) and "threatenables" (assets), where the composition of granular components leads to unpredictable and educational gameplay.

The technical target is a performant, offline-first Progressive Web App (PWA) utilizing JavaScript and WebGL for broad accessibility.

## 2. Core Philosophy: Emergent Gameplay by Decomposition

The central design principle is the decomposition of complex phenomena into simple, granular components. A traditional simulation might define a "virus" as a monolithic object with hardcoded properties. ThreatForge, in contrast, defines a virus by composing atomic components:

-   A `Propagation` component (e.g., `AirbornePropagation`)
-   An `Effect` component (e.g., `CellularDamage`)
-   A `Resistance` component (e.g., `HeatSusceptibility`)
-   An `Evolution` component (e.g., `RandomMutation`)

By combining these fundamental building blocks, the simulation enables **emergent gameplay**. The interaction between simple, predictable components creates complex, unpredictable, and realistic system-level behaviors that are discovered by the player, not pre-scripted by the developer.

## 3. Technical Architecture

### Target Platform
-   **Language:** JavaScript (ES2020+)
-   **Environment:** Browser
-   **Rendering:** WebGL 2.0 (via Three.js)
-   **Architecture:** Offline-first Progressive Web App (PWA)

### The Unified 3D World Engine

The game world is a continuous, seamless 3D planet rendered using a voxel engine. This approach allows for a fully destructible and modifiable environment, which is central to the gameplay.

-   **Engine Loop:** A unified game loop manages simulation updates, component interactions, and rendering.
-   **Contextual UI:** The primary user interface is the world itself. Players interact directly with objects in the 3D space to view information and take actions, similar to the contextual menus in games like SimCity. There are minimal abstract UI panels; the simulation is the interface.

## 4. The Component Ecosystem

The entire simulation is built upon a unified component ecosystem. Every object in the world, whether a weapon or a target, is a composition of atomic components.

### Definitions

-   **Component:** The smallest, indivisible unit of behavior or property. A component is a simple, reusable building block (e.g., `Flammability`, `NetworkConnectivity`, `ElectricalConductivity`).
-   **Threat (Weapon):** An entity composed of components designed to apply effects to other entities. A "bomb" is not a thing in itself, but a composition of `ExplosivePayload`, `ProximityTrigger`, and `Shrapnel` components.
-   **Threatenable (Asset):** An entity composed of components that define its properties, vulnerabilities, and resistances. In ThreatForge, **everything is a threatenable**. A building, a computer network, a population, an ecosystem, and even a planet are all assets defined by their components.

### Component-Based Design

This architecture replaces rigid, monolithic object definitions with a flexible, compositional model.

**The Old, Monolithic Approach (To Be Replaced):**

```typescript
// ANTI-PATTERN: A rigid, hardcoded interface for every possible threat.
interface MonolithicThreat {
  id: string;
  domain: 'CYBER' | 'BIO' | 'GEO';
  // Numerous optional, domain-specific properties
  cyberProperties?: {
    attackVector?: "NETWORK" | "PHYSICAL";
    zeroDay?: boolean;
  };
  biologicalProperties?: {
    transmissionVectors: ("AIRBORNE" | "WATERBORNE")[];
    mutationRate: number;
  };
  // ...and so on for every domain, becoming unmanageable.
}
```

**The New, Compositional Approach:**

```typescript
// The core entity in the simulation.
interface Entity {
  id: string;
  name: string;
  components: Map<ComponentType, Component>;
}

// A component is a simple, focused piece of data or logic.
interface Component {
  type: ComponentType;
  properties: Record<string, any>;
}

// Example Components:
const propagation = { type: 'PROPAGATION', properties: { medium: 'AIRBORNE', speed: 10 } };
const vulnerability = { type: 'VULNERABILITY', properties: { damageType: 'FIRE', multiplier: 2.0 } };
const resistance = { type: 'RESISTANCE', properties: { damageType: 'FIRE', multiplier: 0.5 } };
```

### Interaction and Emergence

Emergent behavior arises from the **Interaction Engine**, which processes the interactions between components based on a defined set of rules.

-   **Direct Interactions:** A `Fire` effect component interacts with a `Flammability` vulnerability component.
-   **Indirect Interactions:** A `NetworkOutage` component on a power grid entity might indirectly affect a `WaterPump` entity that has an `ElectricalPower` dependency component.
-   **Cross-Domain Emergence:** A `Cyber` threat composed of a `NetworkPropagation` component could infect the control system of a `Biological` lab (a threatenable asset), which then causes the release of an entity with a `Biohazard` component. This creates a complex, multi-domain event that was not explicitly scripted.

### Rich Set of Threats and Threatenables

The goal is to create a vast library of components, allowing for a near-infinite variety of threats and assets.

-   **Threat Examples:**
    -   **Virus:** `AirbornePropagation` + `CellularDamage` + `Mutation`
    -   **Ransomware:** `NetworkPropagation` + `DataEncryption` + `FinancialDemand`
    -   **EMP Bomb:** `AreaOfEffect` + `ElectromagneticPulse` + `DetonationTrigger`

### 4.4 The Threatenable Ecosystem: Everything is Destructible

A core principle of ThreatForge is that there are no invincible objects. Every entity in the world is a "threatenable" asset, defined by a composition of components that describe its vulnerabilities and resistances. This creates a dynamic simulation where any asset can be affected, damaged, or destroyed if subjected to the right combination of threat effects.

**Threatenable Types:**

*   **Physical Infrastructure:** Buildings, bridges, power grids.
*   **Biological Entities:** Populations, ecosystems, crops.
*   **Digital Systems:** Computer networks, data centers, communication satellites.
*   **Economic Systems:** Financial markets, supply chains, corporations.
*   **Social Structures:** Governments, ideologies, social cohesion.

**Threatenable Composition Examples:**

-   **Building:** `StructuralIntegrity` + `Flammability` + `PowerDependency` + `AccessPointVulnerability`
-   **Population:** `SocialCohesion` + `DiseaseSusceptibility` + `InformationVulnerability` + `ResourceDependency`
-   **Power Grid:** `NetworkTopology` + `NodeVulnerability` + `CascadeFailureDependency` + `CybersecurityProtocol`
-   **Financial Market:** `MarketVolatility` + `RegulatoryFramework` + `InvestorConfidence` + `InformationAsymmetry`

By modeling assets with the same component-based system as threats, the simulation can produce realistic and complex chains of cause and effect. A cyber-attack on a power grid can lead to a blackout, which affects a hospital's life support systems, which in turn impacts population health. This systemic interactivity is the foundation of the emergent gameplay experience.

## 5. Educational & Discovery Framework

ThreatForge is designed as a learning platform where players gain an intuitive understanding of complex systems through experimentation. The gameplay loop is modeled on the scientific method.

**The Learning Loop:**
1.  **Hypothesis:** The player forms a hypothesis ("What happens if I combine a `NetworkPropagation` component with a `BiologicalInfection` component?").
2.  **Experimentation:** The player composes the threat and deploys it in the 3D world.
3.  **Observation:** The player observes the outcome. The components interact, creating an "Information Cascade" emergent behavior where disinformation accelerates the biological spread.
4.  **Understanding:** The player learns a new principle about system interactions, internalizing concepts of cross-domain vulnerabilities and feedback loops.

### Learning Progression

The game will guide the player through a structured discovery process:

-   **Stage 1: Atomic Components:** Understanding the predictable behavior of individual components in isolation.
-   **Stage 2: Component Interactions:** Discovering how pairs of components from different domains interact to create simple emergent effects.
-   **Stage 3: Complex System Analysis:** Composing threats with multiple components and analyzing the resulting cascade effects and feedback loops in a complex environment.

This progression allows players to build a mental model of systems thinking from the ground up, moving from simple, linear cause-and-effect to complex, non-linear dynamics.

## 6. Performance & Optimization

To ensure a smooth experience on a wide range of commodity hardware, the engine will be built with performance as a primary consideration.

**Target:** 60 FPS at 1080p on a mid-range system (e.g., Intel i5, GTX 1660, 16GB RAM).

### Adaptive Quality System

The engine will automatically adjust visual and simulation complexity to maintain the target frame rate.

| Quality Level | Target FPS | Simulation Detail | Visuals |
| :------------ | :--------- | :---------------- | :------ |
| **High**      | 60+        | Full component simulation | High-res textures, complex particle effects |
| **Balanced**  | 50-60      | High-level component interaction | Medium textures, simplified effects |
| **Low**       | 30-45      | Abstracted outcomes, fewer particles | Low-res textures, basic effects |

### Memory Management

-   **Component Pooling:** Reusing component instances to avoid frequent memory allocation and garbage collection.
-   **Lazy Loading:** World chunks and assets will be loaded on-demand as the player navigates the world.
-   **Memory Budget:** A target memory footprint of <8GB for the entire simulation.

## 7. High-Level Implementation Plan

This plan outlines the major phases of development, excluding specific time or developer estimates.

### Phase 1: Core Engine Foundation
-   Develop the unified 3D world engine using JavaScript and Three.js.
-   Implement the core voxel system for a destructible environment.
-   Establish the main simulation loop and performance monitoring hooks.
-   Create the foundational `Entity` and `Component` data structures.
-   Set up the Progressive Web App (PWA) shell and service worker for offline-first capability.

### Phase 2: Component Ecosystem & Interaction
-   Build the Component Registry for managing and composing components.
-   Develop the Interaction Engine to process component interactions based on rules.
-   Implement a baseline set of 50+ atomic components across **Physical**, **Biological**, and **Digital** domains.
-   Create the system for dynamically composing entities from components.
-   Build and test the first simple emergent behaviors from cross-domain interactions.

### Phase 3: Gameplay & UI
-   Implement the contextual, world-space UI system (e.g., radial menus on objects).
-   Develop the core gameplay loop: Hypothesis -> Experimentation -> Observation.
-   Create initial "threat" and "threatenable" entity compositions for gameplay testing.
-   Build visualization systems to provide clear, intuitive feedback on component interactions.
-   Implement the educational tooltip and overlay system to explain scientific principles in context.

### Phase 4: Content Expansion & Polish
-   Expand the component library to 200+ components, covering **Economic**, **Social**, and **Environmental** domains.
-   Introduce and validate more complex, multi-stage emergent scenarios.
-   Implement and refine the Adaptive Quality System based on performance testing.
-   Develop the guided discovery progression system and tutorial scenarios.
-   Perform scientific accuracy validation on component behaviors and interactions.
