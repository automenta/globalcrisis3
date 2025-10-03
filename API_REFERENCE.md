# API Reference 📚

## Overview

Complete API documentation for the ThreatForge game engine. For implementation examples, see [Code Examples](CODE_EXAMPLES.md).

## Core Engine API

### GameEngine Class

Main entry point for the ThreatForge engine.

```typescript
class GameEngine {
  constructor(config: EngineConfig)
  
  // Core Methods
  composeThreat(components: ComponentConfig[], options?: ThreatOptions): ComposedThreat
  createThreat(type: string, properties: Record<string, any>): Threat
  update(deltaTime: number): void
  destroy(): void
  
  // Component Management
  registerComponent(type: string, component: ComponentConstructor): void
  getComponentRegistry(): ComponentRegistry
  
  // Performance Management
  setQuality(quality: QualityLevel): void
  getPerformanceMetrics(): PerformanceMetrics
  optimizePerformance(options: OptimizationOptions): void
  
  // Event System
  on(event: string, callback: Function): void
  off(event: string, callback: Function): void
}
```

#### EngineConfig Interface

```typescript
interface EngineConfig {
  canvas?: HTMLCanvasElement
  enableDevTools?: boolean
  performance?: PerformanceConfig
  rendering?: RenderingConfig
  multiplayer?: MultiplayerConfig
}
```

#### PerformanceConfig Interface

```typescript
interface PerformanceConfig {
  quality?: QualityLevel                    // 'minimal' | 'low' | 'balanced' | 'high' | 'ultra' | 'adaptive'
  targetFPS?: number                        // Target frame rate (default: 60)
  maxEmergentBehaviors?: number             // Max emergent behaviors
  memoryLimit?: number | 'adaptive'         // Memory limit in MB
  enableAutoAdjustment?: boolean            // Enable auto-adjustment
}
```

### Component System API

#### ThreatComponent Interface

```typescript
interface ThreatComponent {
  id: string
  type: ComponentType
  properties: Record<string, any>
  behaviors: Behavior[]
  emergencePotential: number
  domain: ThreatDomain
  quality: QualityLevel
  
  // Methods
  update(deltaTime: number, context: BehaviorContext): void
  validate(): boolean
  getEmergentPotential(): number
  getPerformanceImpact(): PerformanceImpact
}
```

#### ComponentType Enum

```typescript
enum ComponentType {
  // Transmission Components
  AIRBORNE_TRANSMISSION = 'AIRBORNE_TRANSMISSION',
  NETWORK_PROPAGATION = 'NETWORK_PROPAGATION',
  VECTOR_BORNE = 'VECTOR_BORNE',
  QUANTUM_ENTANGLEMENT = 'QUANTUM_ENTANGLEMENT',
  
  // Effect Components
  HEALTH_IMPACT = 'HEALTH_IMPACT',
  ECONOMIC_DISRUPTION = 'ECONOMIC_DISRUPTION',
  INFRASTRUCTURE_DAMAGE = 'INFRASTRUCTURE_DAMAGE',
  
  // Evolution Components
  MUTATION_ENGINE = 'MUTATION_ENGINE',
  ADAPTATION_LEARNING = 'ADAPTATION_LEARNING',
  
  // Special Components
  QUANTUM_COHERENCE = 'QUANTUM_COHERENCE',
  AI_LEARNING_SYSTEM = 'AI_LEARNING_SYSTEM',
  SYNTHETIC_BIOLOGY = 'SYNTHETIC_BIOLOGY'
}
```

#### ThreatDomain Enum

```typescript
enum ThreatDomain {
  BIOLOGICAL = 'BIOLOGICAL',
  CYBER = 'CYBER',
  ENVIRONMENTAL = 'ENVIRONMENTAL',
  QUANTUM = 'QUANTUM',
  RADIOLOGICAL = 'RADIOLOGICAL',
  ROBOTIC = 'ROBOTIC'
}
```

#### Behavior Interface

```typescript
interface Behavior {
  update(deltaTime: number, context: BehaviorContext): void
  validate(): boolean
  getEmergentPotential(): number
  getPerformanceImpact(): PerformanceImpact
}
```

#### BehaviorContext Interface

```typescript
interface BehaviorContext {
  world: WorldState
  threat: ComposedThreat
  environment: EnvironmentalFactors
  time: number
  deltaTime: number
  
  // Helper Methods
  getComponent(type: ComponentType): ThreatComponent | undefined
  emitEmergentEvent(type: string, data: any): void
}
```

### Threat Composition API

#### ComposedThreat Class

```typescript
class ComposedThreat implements Threat {
  id: string
  components: ThreatComponent[]
  emergentBehaviors: EmergentBehavior[]
  domain: ThreatDomain
  intensity: number
  spread: number
  position: Vector3
  performanceMetrics: PerformanceMetrics
  
  // Methods
  update(deltaTime: number): void
  addComponent(component: ThreatComponent): void
  removeComponent(componentId: string): void
  getComponent(type: ComponentType): ThreatComponent | undefined
  analyzeInteractions(): InteractionAnalysis
  predictEvolution(cycles: number): ThreatEvolution
  optimizeForPerformance(options: OptimizationOptions): void
  destroy(): void
}
```

#### Threat Interface

```typescript
interface Threat {
  id: string
  type: string
  domain: ThreatDomain
  severity: number
  visibility: number
  spreadRate: number
  effects: ThreatEffect[]
  position: Vector3
  performanceMetrics: PerformanceMetrics
}
```

#### EmergentBehavior Interface

```typescript
interface EmergentBehavior {
  id: string
  name: string
  description: string
  impactLevel: 'LOW' | 'MEDIUM' | 'HIGH' | 'CRITICAL'
  complexity: number
  predictability: number
  discoveryMethod: string
  conditions: EmergentCondition[]
  effects: ThreatEffect[]
  
  activate(context: BehaviorContext): void
  update(deltaTime: number, context: BehaviorContext): void
  getPerformanceImpact(): PerformanceImpact
}
```

### Component Registry API

#### ComponentRegistry Class

```typescript
class ComponentRegistry {
  private components: Map<ComponentType, ComponentDefinition>
  private interactions: InteractionMatrix
  
  // Registration
  register(type: string, constructor: ComponentConstructor, profile?: PerformanceProfile): void
  unregister(type: string): void
  registerPlugin(plugin: ComponentPlugin): void
  
  // Discovery
  composeThreat(components: ComponentConfig[]): ComposedThreat
  discoverEmergentBehaviors(components: ThreatComponent[]): EmergentBehavior[]
  getInteractionMatrix(): ComponentInteractionMatrix
  
  // Queries
  getComponent(type: ComponentType): ComponentDefinition | undefined
  getComponentsByDomain(domain: ThreatDomain): ComponentDefinition[]
  getCompatibleComponents(component: ThreatComponent): ComponentDefinition[]
  
  // Optimization
  optimizeForHardware(components: ThreatComponent[], hardware: HardwareProfile): OptimizedComponents
  filterByPerformance(components: ThreatComponent[], target: PerformanceTarget): ThreatComponent[]
}
```

#### ComponentPlugin Interface

```typescript
interface ComponentPlugin {
  name: string
  version: string
  components: ComponentDefinition[]
  interactions: ComponentInteraction[]
  metadata: PluginMetadata
}

interface PluginMetadata {
  author: string
  description: string
  domains: ThreatDomain[]
  dependencies?: string[]
  compatibility: string
}
```

## Performance API

### PerformanceMetrics Interface

```typescript
interface PerformanceMetrics {
  currentFPS: number
  averageFPS: number
  minFPS: number
  maxFPS: number
  frameTime: number
  memoryUsage: MemoryMetrics
  componentCount: number
  emergentBehaviorCount: number
  renderTime: number
  physicsTime: number
  updateTime: number
  qualityLevel: QualityLevel
  optimizationLevel: string
}
```

### MemoryMetrics Interface

```typescript
interface MemoryMetrics {
  usedJSHeapSize: number
  totalJSHeapSize: number
  jsHeapSizeLimit: number
  componentMemory: number
  textureMemory: number
  bufferMemory: number
  objectPoolUsage: number
}
```

### PerformanceImpact Interface

```typescript
interface PerformanceImpact {
  cpu: number        // 0-1 scale
  memory: number     // 0-1 scale
  render: number     // 0-1 scale
  network?: number   // 0-1 scale (optional)
}
```

## Event System API

### Event Types

```typescript
// Engine Events
interface EngineEvents {
  'engine:initialized': { timestamp: number }
  'engine:destroyed': { timestamp: number }
  'engine:error': { error: Error, context: string }
  'engine:warning': { message: string, context: string }
}

// Component Events
interface ComponentEvents {
  'component:registered': { type: ComponentType, domain: ThreatDomain }
  'component:unregistered': { type: ComponentType }
  'component:updated': { component: ThreatComponent, deltaTime: number }
  'component:interaction': { source: ThreatComponent, target: ThreatComponent, interaction: ComponentInteraction }
}

// Threat Events
interface ThreatEvents {
  'threat:composed': { threat: ComposedThreat, components: ThreatComponent[] }
  'threat:updated': { threat: ComposedThreat, deltaTime: number }
  'threat:destroyed': { threatId: string }
  'threat:emergent': { threat: ComposedThreat, behavior: EmergentBehavior }
}

// Performance Events
interface PerformanceEvents {
  'performance:warning': { fps: number, metrics: PerformanceMetrics }
  'performance:critical': { fps: number, metrics: PerformanceMetrics }
  'performance:optimized': { fps: number, metrics: PerformanceMetrics }
  'performance:degraded': { fps: number, metrics: PerformanceMetrics }
}
```

### EventEmitter Methods

```typescript
interface EventEmitter {
  on<T>(event: string, callback: (data: T) => void): void
  off<T>(event: string, callback: (data: T) => void): void
  once<T>(event: string, callback: (data: T) => void): void
  emit<T>(event: string, data: T): void
  removeAllListeners(event?: string): void
  listenerCount(event: string): number
}
```

## Rendering API

### RenderingEngine Class

```typescript
class RenderingEngine {
  constructor(canvas: HTMLCanvasElement, config: RenderingConfig)
  
  // Scene Management
  createScene(): THREE.Scene
  destroyScene(scene: THREE.Scene): void
  addObject(object: THREE.Object3D): void
  removeObject(object: THREE.Object3D): void
  
  // Threat Visualization
  createThreatVisualization(threat: ComposedThreat, quality: QualityLevel): THREE.Group
  updateThreatVisualization(threat: ComposedThreat, deltaTime: number): void
  createEmergentVisualization(behavior: EmergentBehavior, context: RenderContext): THREE.Object3D
  
  // Quality Management
  setQuality(quality: QualityLevel): void
  getQuality(): QualityLevel
  adjustQuality(settings: QualitySettings): void
  
  // Performance
  getRenderingStats(): RenderingStats
  optimizeRendering(options: RenderingOptimizationOptions): void
}
```

### RenderingConfig Interface

```typescript
interface RenderingConfig {
  quality?: QualityLevel
  enableShadows?: boolean
  enablePostProcessing?: boolean
  enableAntialiasing?: boolean
  textureQuality?: 'low' | 'medium' | 'high' | 'ultra'
  maxLights?: number
  shadowQuality?: 'low' | 'medium' | 'high'
  lodDistances?: number[]
  enableInstancing?: boolean
  enableTextureStreaming?: boolean
}
```

### QualitySettings Interface

```typescript
interface QualitySettings {
  renderQuality: QualityLevel
  textureQuality: 'low' | 'medium' | 'high' | 'ultra'
  shadowQuality: 'low' | 'medium' | 'high'
  effectQuality: 'minimal' | 'low' | 'medium' | 'high'
  physicsAccuracy: 'low' | 'medium' | 'high'
  maxParticleCount: number
  enablePostProcessing: boolean
  enableShadows: boolean
}
```

## Multiplayer API

### MultiplayerManager Class

```typescript
class MultiplayerManager {
  constructor(config: MultiplayerConfig)
  
  // Connection Management
  connect(url: string): Promise<void>
  disconnect(): void
  getConnectionState(): ConnectionState
  
  // Room Management
  createRoom(options: RoomOptions): Promise<Room>
  joinRoom(roomId: string): Promise<Room>
  leaveRoom(): void
  getCurrentRoom(): Room | null
  
  // Player Management
  getLocalPlayer(): Player
  getPlayers(): Player[]
  getPlayerById(id: string): Player | null
  
  // State Synchronization
  syncThreat(threat: ComposedThreat): void
  syncWorldState(state: WorldState): void
  requestStateSync(): void
  
  // Events
  on(event: string, callback: Function): void
  off(event: string, callback: Function): void
}
```

### MultiplayerConfig Interface

```typescript
interface MultiplayerConfig {
  enableCompression?: boolean
  compressionLevel?: number                    // 1-9
  enableDeltaCompression?: boolean
  updateRate?: number                          // Hz
  maxUpdateSize?: number                       // bytes
  interpolationDelay?: number                  // milliseconds
  enablePrediction?: boolean
  maxPredictionTime?: number                   // milliseconds
  smoothingFactor?: number                     // 0-1
  enableEncryption?: boolean
  quantumSecurity?: boolean                    // Quantum key distribution
}
```

### Room Interface

```typescript
interface Room {
  id: string
  name: string
  maxPlayers: number
  currentPlayers: number
  state: RoomState
  settings: RoomSettings
  players: Player[]
  
  // Methods
  send(data: any): void
  broadcast(event: string, data: any): void
  kick(playerId: string): void
  updateSettings(settings: RoomSettings): void
}
```

## Development Tools API

### DevelopmentInspector Class

```typescript
class DevelopmentInspector {
  constructor(config: InspectorConfig)
  
  // Entity Inspection
  inspectThreat(threat: ComposedThreat): ThreatInspectionReport
  inspectComponent(component: ThreatComponent): ComponentInspectionReport
  inspectWorld(world: WorldState): WorldInspectionReport
  
  // Performance Analysis
  analyzePerformance(threat: ComposedThreat): PerformanceAnalysis
  analyzeMemoryUsage(): MemoryAnalysis
  analyzeComponentInteractions(components: ThreatComponent[]): InteractionAnalysis
  
  // Debugging
  enableDebugMode(): void
  disableDebugMode(): void
  setBreakpoint(condition: string): void
  stepThrough(): void
  
  // Visualization
  visualizeThreatGraph(threat: ComposedThreat): GraphVisualization
  visualizeInteractionMatrix(components: ThreatComponent[]): MatrixVisualization
  visualizePerformance(metrics: PerformanceMetrics): PerformanceVisualization
}
```

### InspectorConfig Interface

```typescript
interface InspectorConfig {
  detailLevel?: 'minimal' | 'standard' | 'full'
  enableRealTimeUpdates?: boolean
  performanceImpact?: 'minimal' | 'standard' | 'full'
  enableRemoteDebugging?: boolean
  logLevel?: 'error' | 'warn' | 'info' | 'debug'
}
```

## Utility APIs

### Vector3 Class

```typescript
class Vector3 {
  x: number
  y: number
  z: number
  
  constructor(x?: number, y?: number, z?: number)
  
  // Operations
  add(v: Vector3): Vector3
  subtract(v: Vector3): Vector3
  multiply(scalar: number): Vector3
  divide(scalar: number): Vector3
  normalize(): Vector3
  length(): number
  distanceTo(v: Vector3): number
  clone(): Vector3
}
```

### Random Utility

```typescript
class Random {
  static float(min?: number, max?: number): number
  static int(min: number, max: number): number
  static bool(probability?: number): boolean
  static choice<T>(array: T[]): T
  static shuffle<T>(array: T[]): T[]
  static normal(mean?: number, stdDev?: number): number
  static seed(seed: number): void
}
```

### Math Utility

```typescript
class MathUtils {
  static clamp(value: number, min: number, max: number): number
  static lerp(start: number, end: number, t: number): number
  static smoothstep(edge0: number, edge1: number, x: number): number
  static distance(x1: number, y1: number, x2: number, y2: number): number
  static angle(x1: number, y1: number, x2: number, y2: number): number
  static map(value: number, start1: number, end1: number, start2: number, end2: number): number
}
```

## Configuration APIs

### ConfigurationManager Class

```typescript
class ConfigurationManager {
  // Loading
  loadConfig(config: EngineConfig): void
  loadConfigFromFile(path: string): Promise<EngineConfig>
  loadConfigFromURL(url: string): Promise<EngineConfig>
  
  // Validation
  validateConfig(config: EngineConfig): ValidationResult
  getValidationErrors(): ValidationError[]
  
  // Defaults
  getDefaultConfig(): EngineConfig
  getDefaultPerformanceConfig(): PerformanceConfig
  getDefaultRenderingConfig(): RenderingConfig
  
  // Profiles
  applyProfile(profile: string): void
  createProfile(name: string, config: EngineConfig): void
  getAvailableProfiles(): string[]
}
```

### ValidationResult Interface

```typescript
interface ValidationResult {
  valid: boolean
  errors: ValidationError[]
  warnings: ValidationWarning[]
  suggestions: ConfigurationSuggestion[]
}

interface ValidationError {
  field: string
  message: string
  severity: 'error' | 'warning'
  suggestion?: string
}
```

## Error Handling API

### Error Types

```typescript
class ThreatForgeError extends Error {
  code: string
  context: string
  timestamp: number
  
  constructor(code: string, message: string, context?: string)
}

class ComponentError extends ThreatForgeError {
  componentType: ComponentType
  
  constructor(componentType: ComponentType, message: string, code?: string)
}

class PerformanceError extends ThreatForgeError {
  metrics: PerformanceMetrics
  
  constructor(message: string, metrics: PerformanceMetrics)
}

class NetworkError extends ThreatForgeError {
  connectionState: ConnectionState
  
  constructor(message: string, connectionState: ConnectionState)
}
```

### Error Codes

```typescript
enum ErrorCode {
  // Component Errors
  COMPONENT_NOT_FOUND = 'COMPONENT_NOT_FOUND',
  COMPONENT_INVALID = 'COMPONENT_INVALID',
  COMPONENT_DEPENDENCY_MISSING = 'COMPONENT_DEPENDENCY_MISSING',
  
  // Performance Errors
  PERFORMANCE_CRITICAL = 'PERFORMANCE_CRITICAL',
  MEMORY_LIMIT_EXCEEDED = 'MEMORY_LIMIT_EXCEEDED',
  RENDERING_ERROR = 'RENDERING_ERROR',
  
  // Network Errors
  CONNECTION_FAILED = 'CONNECTION_FAILED',
  SYNC_ERROR = 'SYNC_ERROR',
  ROOM_NOT_FOUND = 'ROOM_NOT_FOUND',
  
  // Configuration Errors
  CONFIG_INVALID = 'CONFIG_INVALID',
  CONFIG_MISSING = 'CONFIG_MISSING',
  CONFIG_INCOMPATIBLE = 'CONFIG_INCOMPATIBLE'
}
```

## Plugin API

### Plugin Interface

```typescript
interface Plugin {
  name: string
  version: string
  author: string
  description: string
  
  // Lifecycle
  initialize(engine: GameEngine): void
  destroy(): void
  
  // Components
  getComponents(): ComponentDefinition[]
  getInteractions(): ComponentInteraction[]
  
  // Events
  onInstall?(): void
  onUninstall?(): void
  onEnable?(): void
  onDisable?(): void
}
```

### PluginManager Class

```typescript
class PluginManager {
  // Plugin Management
  install(plugin: Plugin): void
  uninstall(pluginName: string): void
  enable(pluginName: string): void
  disable(pluginName: string): void
  
  // Queries
  getPlugin(name: string): Plugin | null
  getInstalledPlugins(): Plugin[]
  getEnabledPlugins(): Plugin[]
  
  // Validation
  validatePlugin(plugin: Plugin): ValidationResult
  checkCompatibility(plugin: Plugin, engineVersion: string): boolean
}
```

## TypeScript Support

### Generic Types

```typescript
// Generic threat composition
function composeThreat<T extends ComponentType>(
  components: Array<{ type: T, properties: ComponentProperties[T] }>
): ComposedThreat

// Generic component creation
function createComponent<T extends ComponentType>(
  type: T,
  properties: ComponentProperties[T]
): ThreatComponent

// Generic event handling
interface TypedEventEmitter<T> {
  on<K extends keyof T>(event: K, callback: (data: T[K]) => void): void
  emit<K extends keyof T>(event: K, data: T[K]): void
}
```

### Type Guards

```typescript
// Component type guards
function isBiologicalComponent(component: ThreatComponent): component is BiologicalComponent
function isCyberComponent(component: ThreatComponent): component is CyberComponent
function isQuantumComponent(component: ThreatComponent): component is QuantumComponent

// Threat type guards
function isComposedThreat(threat: Threat): threat is ComposedThreat
function isSimpleThreat(threat: Threat): threat is SimpleThreat

// Behavior type guards
function isEmergentBehavior(behavior: Behavior): behavior is EmergentBehavior
function isBasicBehavior(behavior: Behavior): behavior is BasicBehavior
```

## Migration Guide

### From v1.x to v2.x

```typescript
// v1.x (deprecated)
const engine = new GameEngine()
const threat = engine.createThreat('BASIC_INFECTION', {
  transmissionRate: 0.5
})

// v2.x (current)
const engine = new GameEngine()
const threat = engine.composeThreat([
  {
    type: 'BIOLOGICAL_INFECTION',
    properties: { transmissionRate: 0.5 }
  }
])
```

### Deprecated APIs

```typescript
// ❌ Deprecated
engine.createSimpleThreat(type, properties)
engine.addComponentManually(threat, component)
engine.calculateThreatComplexity(threat)

// ✅ Recommended
engine.composeThreat([{ type, properties }])
threat.addComponent(component)
threat.analyzeComplexity()
```

## Best Practices

### Error Handling

```typescript
// ✅ Good error handling
try {
  const threat = engine.composeThreat(components)
} catch (error) {
  if (error instanceof ComponentError) {
    console.error(`Component error: ${error.message}`)
    console.error(`Component type: ${error.componentType}`)
  } else if (error instanceof PerformanceError) {
    console.error(`Performance error: ${error.message}`)
    console.error(`Metrics:`, error.metrics)
  }
}

// ✅ Defensive programming
const threat = engine.composeThreat(components, {
  performance: {
    maxEmergentBehaviors: 50,
    complexityThreshold: 0.8
  }
}).catch(error => {
  console.error('Failed to compose threat:', error)
  return engine.createThreat('BASIC_INFECTION', { transmissionRate: 0.5 })
})
```

### Type Safety

```typescript
// ✅ Use TypeScript for type safety
const components: ComponentConfig[] = [
  {
    type: ComponentType.BIOLOGICAL_INFECTION,
    properties: {
      transmissionRate: 0.7,
      severity: 0.4
    }
  }
]

const threat = engine.composeThreat(components)

// ✅ Type-safe event handling
engine.on('threat:composed', (event: ThreatEvents['threat:composed']) => {
  console.log(`Threat composed: ${event.threat.id}`)
})
```

## Examples

### Basic Usage

```typescript
import { GameEngine, ComponentType } from '@threatforge/core'

// Initialize engine
const engine = new GameEngine({
  performance: {
    quality: 'adaptive',
    targetFPS: 60
  }
})

// Compose a threat
const threat = engine.composeThreat([
  {
    type: ComponentType.BIOLOGICAL_INFECTION,
    properties: {
      transmissionRate: 0.7,
      severity: 0.5
    }
  },
  {
    type: ComponentType.AIRBORNE_TRANSMISSION,
    properties: {
      range: 1000,
      seasonalVariation: true
    }
  }
])

console.log(`Created threat with ${threat.emergentBehaviors.length} emergent behaviors`)
```

### Advanced Usage

```typescript
import { 
  GameEngine, 
  ComponentType, 
  QualityLevel,
  PerformanceConfig 
} from '@threatforge/core'

// Advanced configuration
const performanceConfig: PerformanceConfig = {
  quality: QualityLevel.HIGH,
  targetFPS: 60,
  maxEmergentBehaviors: 100,
  memoryLimit: 4096,
  enableAutoAdjustment: true
}

const engine = new GameEngine({
  performance: performanceConfig,
  rendering: {
    quality: QualityLevel.HIGH,
    enableShadows: true,
    textureQuality: 'high'
  }
})

// Complex multi-domain threat
const complexThreat = engine.composeThreat([
  {
    type: ComponentType.QUANTUM_ENTANGLEMENT,
    properties: {
      coherenceTime: 2000,
      entanglementStrength: 0.9
    }
  },
  {
    type: ComponentType.BIOLOGICAL_INFECTION,
    properties: {
      transmissionRate: 0.6,
      mutationPotential: 0.3
    }
  },
  {
    type: ComponentType.AI_LEARNING_SYSTEM,
    properties: {
      learningRate: 0.1,
      creativityFactor: 0.8
    }
  }
])

// Monitor performance
engine.on('performance:warning', (metrics) => {
  console.warn(`Performance warning: ${metrics.fps} FPS`)
  engine.setQuality(QualityLevel.MEDIUM)
})
```

## Changelog

### Version 2.0.0

- **Breaking**: Replaced `createThreat()` with `composeThreat()`
- **Breaking**: Changed component registration API
- **New**: Added adaptive quality system
- **New**: Added comprehensive performance monitoring
- **New**: Added multiplayer framework
- **New**: Added plugin system
- **Improved**: Better TypeScript support
- **Improved**: Enhanced error handling

### Version 1.5.0

- **New**: Added quantum domain components
- **New**: Added neural interface components
- **New**: Added advanced AI learning behaviors
- **Improved**: Better emergence calculation
- **Fixed**: Memory leaks in component pooling

For complete changelog, see [CHANGELOG.md](CHANGELOG.md).

## Support

- **Documentation**: [Full Documentation](DOCUMENTATION_INDEX.md)
- **Examples**: [Code Examples](CODE_EXAMPLES.md)
- **Community**: [GitHub Discussions](https://github.com/threatforge/engine/discussions)
- **Issues**: [GitHub Issues](https://github.com/threatforge/engine/issues)
- **Discord**: [ThreatForge Discord](https://discord.gg/threatforge)

**Happy coding!** 🚀