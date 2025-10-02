# Metaprogramming and UI Widget System Specification

## Overview
The ThreatForge engine implements a sophisticated metaprogramming system that automatically generates UI widgets, APIs, and data accessors based on TypeScript interfaces and JSON schemas. This minimizes boilerplate code and ensures consistency across the application.

## Core Metaprogramming Concepts

### 1. Schema-Driven UI Generation
The system analyzes data structures and automatically generates appropriate UI controls based on type information, validation rules, and contextual metadata.

```typescript
// Input: TypeScript interface
interface MilitaryUnit {
  id: string
  type: UnitType
  position: [number, number]
  health: number
  energy: number
  autonomyLevel: number
  abilities: UnitAbility[]
}

// Generated: UI Widget Configuration
const unitWidgetConfig = {
  component: 'Form',
  fields: [
    { name: 'id', type: 'text', readonly: true },
    { name: 'type', type: 'select', options: UnitTypeValues },
    { name: 'position', type: 'coordinate', dimensions: 2 },
    { name: 'health', type: 'slider', min: 0, max: 100 },
    { name: 'energy', type: 'slider', min: 0, max: 100 },
    { name: 'autonomyLevel', type: 'slider', min: 0, max: 1, step: 0.1 },
    { name: 'abilities', type: 'array', itemType: 'object' }
  ]
}
```

### 2. Automatic API Generation
Creates type-safe APIs for accessing and manipulating game objects without manual coding.

```typescript
// Generated API methods
class MilitaryUnitAPI {
  getById(id: string): MilitaryUnit | null
  getByFaction(factionId: string): MilitaryUnit[]
  getWithinRadius(center: Vector2, radius: number): MilitaryUnit[]
  updatePosition(id: string, position: [number, number]): boolean
  updateHealth(id: string, health: number): boolean
  addAbility(id: string, ability: UnitAbility): boolean
  removeAbility(id: string, abilityId: string): boolean
}
```

### 3. Dynamic Form Generation
Creates context-sensitive forms based on object state and user permissions.

```typescript
interface FormGeneratorConfig {
  schema: InterfaceSchema
  context: UIContext
  permissions: PermissionSet
  customRenderers?: CustomRendererMap
}

class DynamicFormGenerator {
  generateForm(config: FormGeneratorConfig): FormComponent
  validateInput(value: any, field: FieldSchema): ValidationResult
  createConditionalFields(state: FormState): FieldSchema[]
}
```

## UI Widget System Architecture

### Widget Hierarchy
```
Widget (Base Class)
├── FormWidget
│   ├── TextInput
│   ├── NumberInput
│   ├── Slider
│   ├── Select
│   ├── Checkbox
│   ├── RadioGroup
│   ├── CoordinateInput
│   ├── ArrayInput
│   └── ObjectInput
├── DisplayWidget
│   ├── Label
│   ├── ProgressBar
│   ├── StatusIndicator
│   ├── Chart
│   └── Table
├── InteractiveWidget
│   ├── Button
│   ├── Toggle
│   ├── Dropdown
│   ├── Tabs
│   ├── Accordion
│   └── Modal
└── LayoutWidget
    ├── Container
    ├── Grid
    ├── Flex
    ├── SplitPane
    └── ScrollArea
```

### Widget Configuration Schema
```typescript
interface WidgetSchema {
  type: WidgetType
  id: string
  properties: WidgetProperties
  validation?: ValidationRule[]
  conditional?: ConditionalRule[]
  metadata?: MetadataMap
}

interface WidgetProperties {
  label?: string
  placeholder?: string
  readonly?: boolean
  disabled?: boolean
  visible?: boolean
  width?: number | string
  height?: number | string
  style?: CSSProperties
  className?: string
}

interface ValidationRule {
  type: 'required' | 'min' | 'max' | 'pattern' | 'custom'
  value?: any
  message: string
  validator?: (value: any) => boolean
}

interface ConditionalRule {
  condition: string // JavaScript expression
  action: 'show' | 'hide' | 'enable' | 'disable' | 'update'
  target: string
  value?: any
}
```

## Context-Aware UI Generation

### 1. Faction-Specific Interfaces
Automatically adapts UI based on faction capabilities and perspective.

```typescript
class FactionUIGenerator {
  generateDashboard(faction: Faction): DashboardConfig {
    const capabilities = faction.capabilities
    
    return {
      widgets: [
        ...(capabilities.threatDeployment ? [this.createThreatPanel()] : []),
        ...(capabilities.investigation ? [this.createInvestigationPanel()] : []),
        ...(capabilities.cyberOperations ? [this.createCyberConsole()] : []),
        ...(capabilities.quantumOperations ? [this.createQuantumInterface()] : [])
      ],
      layout: this.optimizeLayout(capabilities),
      theme: this.getFactionTheme(faction.type)
    }
  }
}
```

### 2. Threat-Contextual Controls
Shows relevant controls based on active threats and game state.

```typescript
class ContextualUIGenerator {
  generateThreatControls(threats: Threat[]): WidgetConfig[] {
    return threats.map(threat => {
      switch (threat.domain) {
        case 'CYBER':
          return this.generateCyberControls(threat)
        case 'BIO':
          return this.generateBioControls(threat)
        case 'QUANTUM':
          return this.generateQuantumControls(threat)
        default:
          return this.generateGenericControls(threat)
      }
    })
  }
}
```

### 3. Development Mode UI
Special UI elements for debugging and development.

```typescript
class DevelopmentUIGenerator {
  generateInspectorPanel(object: any): FormConfig {
    return {
      title: `${object.constructor.name} Inspector`,
      fields: this.generateFieldsFromObject(object),
      actions: [
        { label: 'Edit', action: 'enableEditing' },
        { label: 'Clone', action: 'cloneObject' },
        { label: 'Delete', action: 'deleteObject' },
        { label: 'Export', action: 'exportObject' }
      ]
    }
  }

  generateTimeControls(): WidgetConfig {
    return {
      type: 'TimeControl',
      properties: {
        currentTime: this.gameState.currentTime,
        playbackSpeed: this.gameState.playbackSpeed,
        isPaused: this.gameState.isPaused
      },
      actions: [
        { label: 'Play', action: 'resume' },
        { label: 'Pause', action: 'pause' },
        { label: 'Step', action: 'step' },
        { label: 'Reset', action: 'reset' }
      ]
    }
  }
}
```

## Metaprogramming Implementation

### 1. TypeScript Interface Analysis
```typescript
class InterfaceAnalyzer {
  analyzeInterface<T>(interfaceName: string): InterfaceSchema {
    // Uses TypeScript compiler API to extract type information
    const typeInfo = this.getTypeInfo<T>()
    
    return {
      name: interfaceName,
      properties: this.extractProperties(typeInfo),
      methods: this.extractMethods(typeInfo),
      decorators: this.extractDecorators(typeInfo),
      generics: this.extractGenerics(typeInfo)
    }
  }

  private extractProperties(typeInfo: TypeInfo): PropertySchema[] {
    return typeInfo.properties.map(prop => ({
      name: prop.name,
      type: this.mapType(prop.type),
      optional: prop.optional,
      readonly: prop.readonly,
      decorators: prop.decorators,
      validation: this.extractValidation(prop)
    }))
  }
}
```

### 2. Code Generation Engine
```typescript
class CodeGenerator {
  generateAPIClass(schema: InterfaceSchema): string {
    const className = `${schema.name}API`
    const methods = this.generateAPIMethods(schema)
    
    return `
      export class ${className} {
        ${methods.join('\n')}
        
        constructor(private store: DataStore) {}
        
        ${this.generateGetterMethods(schema)}
        ${this.generateSetterMethods(schema)}
        ${this.generateQueryMethods(schema)}
      }
    `
  }

  generateUIComponent(schema: InterfaceSchema, context: UIContext): string {
    const componentName = `${schema.name}Widget`
    
    return `
      export const ${componentName} = ({ data, onChange, context }) => {
        const fields = useMemo(() => this.generateFields(schema, context), [context])
        
        return (
          <DynamicForm
            fields={fields}
            data={data}
            onChange={onChange}
            validation={this.generateValidation(schema)}
          />
        )
      }
    `
  }
}
```

### 3. Runtime Code Compilation
```typescript
class RuntimeCompiler {
  private moduleCache = new Map<string, any>()

  async compileAndExecute(code: string, context: any): Promise<any> {
    const hash = this.hashCode(code)
    
    if (this.moduleCache.has(hash)) {
      return this.moduleCache.get(hash)
    }

    // Use dynamic import or eval for runtime compilation
    const module = await this.compileModule(code, context)
    this.moduleCache.set(hash, module)
    
    return module
  }

  private async compileModule(code: string, context: any): Promise<any> {
    // Implementation depends on environment (browser vs Node.js)
    if (typeof window !== 'undefined') {
      return this.compileInBrowser(code, context)
    } else {
      return this.compileInNode(code, context)
    }
  }
}
```

## Advanced UI Features

### 1. Adaptive Layout System
```typescript
class AdaptiveLayoutEngine {
  calculateLayout(widgets: WidgetConfig[], container: ContainerConfig): LayoutConfig {
    const screenSize = this.getScreenSize()
    const widgetPriorities = this.calculateWidgetPriorities(widgets)
    
    return {
      type: 'adaptive',
      breakpoints: this.generateBreakpoints(screenSize),
      widgetPositions: this.optimizeWidgetPositions(widgets, container),
      responsiveRules: this.generateResponsiveRules(widgets, screenSize)
    }
  }

  private optimizeWidgetPositions(widgets: WidgetConfig[], container: ContainerConfig): PositionMap {
    // Use constraint satisfaction algorithm
    const constraints = this.extractConstraints(widgets, container)
    return this.solveConstraintProblem(constraints)
  }
}
```

### 2. Gesture Recognition
```typescript
class GestureRecognizer {
  recognizeGesture(events: PointerEvent[]): Gesture | null {
    const pattern = this.extractPattern(events)
    
    if (this.isPinchGesture(pattern)) {
      return { type: 'pinch', scale: this.calculateScale(pattern) }
    }
    
    if (this.isSwipeGesture(pattern)) {
      return { type: 'swipe', direction: this.calculateDirection(pattern) }
    }
    
    if (this.isTapGesture(pattern)) {
      return { type: 'tap', position: this.calculatePosition(pattern) }
    }
    
    return null
  }
}
```

### 3. Voice Control Integration
```typescript
class VoiceControlSystem {
  async initialize(): Promise<void> {
    this.recognition = new SpeechRecognition()
    this.recognition.onresult = this.handleVoiceCommand.bind(this)
  }

  handleVoiceCommand(event: SpeechRecognitionEvent): void {
    const command = this.parseCommand(event.results[0][0].transcript)
    
    switch (command.type) {
      case 'show':
        this.showWidget(command.target)
        break
      case 'hide':
        this.hideWidget(command.target)
        break
      case 'update':
        this.updateWidget(command.target, command.value)
        break
    }
  }

  private parseCommand(transcript: string): VoiceCommand {
    // Natural language processing for voice commands
    return this.nlpProcessor.process(transcript)
  }
}
```

## Data Binding and State Management

### Reactive Data Binding
```typescript
class ReactiveDataBinding {
  bindData(widget: Widget, dataPath: string): Unsubscribe {
    const getter = this.createGetter(dataPath)
    const setter = this.createSetter(dataPath)
    
    // Initial value
    widget.value = getter(this.state)
    
    // Subscribe to changes
    return this.state.subscribe(path => {
      if (this.pathMatches(path, dataPath)) {
        widget.value = getter(this.state)
      }
    })
  }

  createTwoWayBinding(widget: Widget, dataPath: string): Unsubscribe {
    const unsubscribeFromState = this.bindData(widget, dataPath)
    
    const unsubscribeFromWidget = widget.onChange(value => {
      this.state.set(dataPath, value)
    })
    
    return () => {
      unsubscribeFromState()
      unsubscribeFromWidget()
    }
  }
}
```

### State Validation
```typescript
class StateValidator {
  validateStateChange(path: string, newValue: any, oldValue: any): ValidationResult {
    const schema = this.getSchemaForPath(path)
    const rules = this.getValidationRules(schema)
    
    for (const rule of rules) {
      const result = rule.validate(newValue, oldValue)
      if (!result.isValid) {
        return result
      }
    }
    
    return { isValid: true }
  }

  createValidationMiddleware(): Middleware {
    return (store) => (next) => (action) => {
      if (action.type === 'SET_VALUE') {
        const result = this.validateStateChange(
          action.payload.path,
          action.payload.value,
          this.getCurrentValue(action.payload.path)
        )
        
        if (!result.isValid) {
          this.showValidationError(result)
          return
        }
      }
      
      return next(action)
    }
  }
}
```

## Testing and Validation

### UI Testing Framework
```typescript
class UITestingFramework {
  async testWidgetGeneration(schema: InterfaceSchema): Promise<TestResult> {
    const generatedUI = this.uiGenerator.generate(schema)
    
    // Test structure
    const structureTest = this.validateWidgetStructure(generatedUI)
    
    // Test functionality
    const functionalityTest = await this.testWidgetFunctionality(generatedUI)
    
    // Test accessibility
    const accessibilityTest = this.validateAccessibility(generatedUI)
    
    return {
      passed: structureTest.passed && functionalityTest.passed && accessibilityTest.passed,
      results: {
        structure: structureTest,
        functionality: functionalityTest,
        accessibility: accessibilityTest
      }
    }
  }

  async testMetaprogrammingOutput(code: string): Promise<CodeValidationResult> {
    // Compile and test the generated code
    const compiled = await this.compiler.compile(code)
    
    // Run unit tests
    const testResults = await this.runUnitTests(compiled)
    
    // Validate type safety
    const typeCheck = await this.validateTypes(compiled)
    
    return {
      compiled: compiled,
      tests: testResults,
      types: typeCheck,
      safeToExecute: testResults.passed && typeCheck.passed
    }
  }
}
```

## Performance Optimization

### Widget Rendering Optimization
```typescript
class WidgetRenderingOptimizer {
  optimizeWidgetTree(widgets: WidgetConfig[]): OptimizedWidgetTree {
    // Virtual scrolling for large lists
    const virtualizedLists = this.virtualizeLists(widgets)
    
    // Memoization for expensive computations
    const memoizedWidgets = this.applyMemoization(virtualizedLists)
    
    // Lazy loading for non-visible widgets
    const lazyLoaded = this.applyLazyLoading(memoizedWidgets)
    
    // Bundle similar widgets for batch rendering
    return this.batchSimilarWidgets(lazyLoaded)
  }

  private virtualizeLists(widgets: WidgetConfig[]): WidgetConfig[] {
    return widgets.map(widget => {
      if (widget.type === 'array' && widget.properties.itemCount > 50) {
        return {
          ...widget,
          properties: {
            ...widget.properties,
            virtualization: true,
            itemHeight: 30,
            viewportHeight: 300
          }
        }
      }
      return widget
    })
  }
}
```

### Code Generation Optimization
```typescript
class CodeGenerationOptimizer {
  optimizeGeneratedCode(code: string): string {
    // Remove unused imports
    const withoutUnusedImports = this.removeUnusedImports(code)
    
    // Minimize bundle size
    const minified = this.minifyCode(withoutUnusedImports)
    
    // Optimize for execution speed
    const optimized = this.optimizeExecution(minified)
    
    return optimized
  }

  private optimizeExecution(code: string): string {
    // Inline small functions
    // Unroll simple loops
    // Replace string concatenation with template literals
    // Optimize object property access
    return this.applyOptimizations(code)
  }
}
```

## Integration with Core Engine

### Event System Integration
```typescript
class UIEventIntegration {
  constructor(private eventBus: EventBus, private uiManager: UIManager) {
    this.setupEventHandlers()
  }

  private setupEventHandlers(): void {
    // Listen to state changes
    this.eventBus.on('state:changed', (event) => {
      this.uiManager.updateWidgets(event.payload.path, event.payload.value)
    })

    // Listen to threat events
    this.eventBus.on('threat:spawned', (event) => {
      this.uiManager.showThreatNotification(event.payload.threat)
    })

    // Listen to selection events
    this.eventBus.on('selection:changed', (event) => {
      this.uiManager.updateContextualWidgets(event.payload.selection)
    })
  }
}
```

### Plugin Integration
```typescript
class PluginUIIntegration {
  registerPluginUI(plugin: Plugin, uiSchema: WidgetSchema[]): void {
    const generatedUI = this.uiGenerator.generateFromSchema(uiSchema)
    
    this.uiManager.registerPluginWidgets(plugin.id, generatedUI)
    
    // Allow plugins to customize their UI
    plugin.on('ui:customize', (customization) => {
      this.uiManager.applyCustomization(plugin.id, customization)
    })
  }
}
```

This metaprogramming system enables rapid development of consistent, accessible, and performant UI components while maintaining type safety and providing extensive customization options for different contexts and user needs.