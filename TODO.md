# ThreatForge Implementation Plan

## Phase 0: Architecture & Project Setup

-   [ ] **Project Initialization**
    -   [ ] Initialize TypeScript project with Vite.
    -   [ ] Configure ESLint, Prettier, EditorConfig, and `tsconfig.json` for a strict and consistent codebase.
    -   [ ] Establish a scalable project structure: `src/core`, `src/components`, `src/systems`, `src/world`, `src/ui`, `src/assets`.
    -   [ ] Set up a basic CI pipeline (e.g., GitHub Actions) to run linting and type-checking on every commit.

-   [ ] **Core Metamodel Implementation**
    -   [ ] Create `src/core/metamodel.ts` to define the `EnhancedThreatComponent` and `EnhancedThreatenableComponent` interfaces.
    -   [ ] Implement all `ScientificDomain` and `InteractionMechanism` enums.
    -   [ ] Implement the base `Entity` class with a UUID generator and a `components: Map<string, Component>` property.
    -   [ ] Implement a robust `EntityManager` with methods for `createEntity`, `destroyEntity`, `addComponent`, `removeComponent`, and `queryByComponent`.

-   [ ] **Core Systems Foundation**
    -   [ ] Design and implement a generic, type-safe `EventBus` for decoupled system communication.
    -   [ ] Define foundational events: `EntityCreated`, `ComponentAdded`, `InteractionOccurred`, `Tick`.
    -   [ ] Implement a main `Simulation` class to manage the game loop and orchestrate system updates.

-   [ ] **PWA & Application Shell**
    -   [ ] Create the `index.html` shell, web manifest, and a full set of application icons.
    -   [ ] Implement a basic, precaching service worker for full offline availability of the application shell.

-   **Success Criteria:** A bootable application that initializes all core managers and systems, logging a "Ready" state to the console. The project is fully configured for collaborative development.

## Phase 1: Headless Simulation Engine

-   [ ] **Component Registry & Serialization**
    -   [ ] Build the `ComponentRegistry` to load component definitions from static data files (e.g., JSON).
    -   [ ] Implement a `SceneSerializer` to save and load the state of all entities and their components.

-   [ ] **Scientific Interaction Engine**
    -   [ ] Implement the `ScientificInteraction` data structure, including fields for validation and bidirectional effects.
    -   [ ] Build the `InteractionEngine` system.
        -   [ ] Sub-task: Develop a `CompatibilityMatrix` to determine the base `intensity` between component domains.
        -   [ ] Sub-task: Implement logic to apply `Vulnerability` and `Resistance` modifiers.
        -   [ ] Sub-task: Develop the `EffectCalculator` to generate `ThreatModification` and `ThreatenableModification` outcomes.

-   [ ] **Emergence & Co-evolution Engine**
    -   [ ] Build the `EmergenceDiscovery` system to analyze interaction results and identify predefined emergent behavior patterns from a rulebook.
    -   [ ] Implement the co-evolution feedback loop:
        -   [ ] Threat Evolution: Track interaction outcomes and apply property changes to `EnhancedThreatComponent`s that are consistently resisted.
        -   [ ] Threatenable Adaptation: Implement `AdaptiveBehavior` components that can add, remove, or modify other components on their host entity in response to damage.

-   [ ] **Basic Physics Layer**
    -   [ ] Implement a simple physics system for entity position and movement (e.g., velocity, acceleration). This is not for complex simulation but for spatial positioning.

-   **Success Criteria:** A headless simulation that can be run via unit tests. The tests can compose complex entities, run the simulation for N ticks, and verify that interactions produce scientifically-plausible emergent effects and adaptations.

## Phase 2: 3D World & Visualization

-   [ ] **Voxel World Engine**
    -   [ ] Set up the main Three.js scene, renderer, and orbital camera controls.
    -   [ ] Implement a performant voxel engine using Sparse Voxel Octrees (SVOs) for efficient storage and rendering.
    -   [ ] Implement a procedural generation system for the planetoid terrain.
    -   [ ] Implement a chunking system with lazy-loading (on-demand generation) to handle the planetary scale.

-   [ ] **Component Visualization System**
    -   [ ] Design and implement a `Visualizer` system that maps component types to visual representations (e.g., models, shaders, particle systems).
    -   [ ] Map key component properties to shader uniforms for dynamic, state-driven visuals (e.g., `Health` property drives a "damage" shader).
    -   [ ] Implement real-time visual effects for `ScientificInteraction` events.
    -   [ ] Create distinct visual overlays or indicators for emergent behaviors (e.g., a "cascade failure" might show a spreading electrical arc effect).

-   [ ] **Contextual World UI**
    -   [ ] Implement a GPU-based raycasting system for efficient entity selection.
    -   [ ] Develop a data-driven contextual radial menu UI.
    -   [ ] Populate the UI with detailed, real-time information about selected entities, their components, and active interactions.

-   **Success Criteria:** A visible 3D world where entities can be placed and interacted with. Selecting an entity displays its real-time state, and interactions produce clear visual feedback.

## Phase 3: Gameplay & Educational Framework

-   [ ] **Core Gameplay Loop & UI**
    -   [ ] Implement the "Component Lab" UI, featuring a drag-and-drop interface for composing and saving threat entity templates.
    -   [ ] Implement the ability to deploy these composed threats into the 3D world at a chosen location.
    -   [ ] Develop the core gameplay loop: **Hypothesis** -> **Experimentation** -> **Observation**.

-   [ ] **Educational Progression & Content**
    -   [ ] Implement a guided, scenario-based tutorial system based on the three stages of learning (Atomic Components, Interactions, Complex Systems).
    -   [ ] Develop an in-game, dynamic encyclopedia (`Threatpedia`) that logs all discovered components, interactions, and emergent behaviors, linking them to real-world case studies.
    -   [ ] Create a library of 50+ `EnhancedThreatComponent` and 50+ `EnhancedThreatenableComponent` definitions across **Biological, Cyber, and Physical** domains.
    -   [ ] Implement a "Scenario Runner" to load and manage the case-study missions.

-   **Success Criteria:** The project is a playable sandbox. Players can invent and deploy threats, observe the consequences, and learn via a structured tutorial and encyclopedia.

## Phase 4: Content Expansion & Systemic Depth

-   [ ] **Expand Component Library**
    -   [ ] Add 100+ new components focusing on **Economic, Social, and Environmental** domains (e.g., `MarketVolatility`, `SocialCohesion`, `ClimateFeedbackLoop`).
    -   [ ] Implement more complex, multi-stage emergent behaviors that cross these new domains.

-   [ ] **Advanced Simulation Mechanics**
    -   [ ] Fully implement the co-evolutionary "arms race" feedback loop, allowing for multi-generational adaptation.
    -   [ ] Implement a global `Environment` system (e.g., weather grid, climate model) that dynamically influences component interactions.
    -   [ ] Implement a basic AI `Faction` system with agents that can perceive and react to major emergent threats, creating a more dynamic world.

-   [ ] **Scientific Validation**
    -   [ ] Integrate real-world data sets (e.g., CSVs of epidemiological data) to validate the behavior of specific components.
    -   [ ] Refine interaction calculations to ensure they align with documented historical events and case studies.

-   **Success Criteria:** The simulation has significantly more depth, producing complex and realistic results from the interplay of social, economic, and physical systems.

## Phase 5: Performance & Optimization

-   [ ] **Implement Adaptive Quality System**
    -   [ ] Build a real-time, on-screen performance monitor (FPS, memory, sim tick).
    -   [ ] Implement the logic to dynamically scale simulation and visual quality to maintain a target FPS.
    -   [ ] Define and test quality presets (High, Balanced, Low).

-   [ ] **Optimize Simulation Core**
    -   [ ] Offload the `InteractionEngine` and other heavy systems to Web Workers to prevent UI thread blocking.
    -   [ ] Implement a component pooling system to minimize garbage collection.
    -   [ ] Integrate a spatial partitioning system (Octree) to accelerate proximity queries.
    -   [ ] Implement "sleep states" and update throttling for inactive entities.

-   [ ] **Optimize Rendering & Assets**
    -   [ ] Implement a Level of Detail (LOD) system for all voxel meshes and entity models.
    -   [ ] Use instanced rendering for visualizing large-scale component effects.
    -   [ ] Implement texture compression (e.g., Basis Universal) and model optimization (e.g., Draco) for all assets.

-   **Success Criteria:** The simulation runs smoothly on a wide range of hardware, even during large-scale, chaotic emergent events.

## Phase 6: Tooling, Testing & Deployment

-   [ ] **Developer & Modding Tools**
    -   [ ] Create an in-game debug console with commands to spawn entities, modify components, and trigger events.
    -   [ ] Develop a real-time entity inspector that allows for live editing of component properties.
    -   [ ] Build a scenario editor for creating and sharing specific simulation setups with the community.
    -   [ ] Document and expose a clean API for community modding of components and entities.

-   [ ] **Comprehensive Testing**
    -   [ ] Implement a unit testing suite (e.g., Jest) and achieve >90% coverage on core systems.
    -   [ ] Create a suite of "validation scenarios" to test that specific component combinations produce the correct, scientifically-validated emergent outcomes.
    -   [ ] Develop end-to-end playtests (e.g., using Playwright) for the main gameplay and educational loops.

-   [ ] **Multiplayer & Final Deployment**
    -   [ ] Refactor core systems to separate simulation state from presentation, enabling future multiplayer development.
    -   [ ] Finalize PWA features, including full offline asset caching and update notifications.
    -   [ ] Minify, bundle, and deploy the final application to a static hosting provider with a CDN.

-   **Success Criteria:** The project is stable, well-tested, and deployed. It includes robust tools for developers and the community to extend its life.
