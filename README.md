# Angular

**Angular vs AngularJS**

What is the core conceptual difference between AngularJS and Angular (2+)?



Answer: AngularJS (1.x) is MVC / MVVM and uses controllers + scopes; Angular (2+) is component-based with hierarchical component trees and uses TypeScript.

Which language is used for AngularJS development vs modern Angular development?



Answer: AngularJS uses JavaScript (often ES5/ES6); Angular uses TypeScript (superset of JS with types).

How does change detection differ between AngularJS and Angular?



Answer: AngularJS uses dirty-checking (digest cycle) with $scope.$digest; Angular uses a uni-directional (zone-triggered) change detection with a component tree and optimized checks, plus OnPush strategy.

Does AngularJS support dependency injection (DI)? If yes, how is it different from Angular?



Answer: Yes. AngularJS DI is function-parameter/string-annotated; Angular uses a hierarchical injector with decorators (@Injectable) and types via TypeScript.

Which one is more suitable for large enterprise apps and why?



Answer: Angular (2+) — because of TypeScript, modular architecture, performance, tooling, and maintainability.

How is routing implemented in AngularJS vs Angular?


Answer: AngularJS used ngRoute or ui-router; Angular uses @angular/router with a rich Route configuration, lazy loading, guards, resolvers.

What major performance problem did AngularJS face that Angular improved?


Answer: AngularJS’s digest cycle scales poorly with many watchers; Angular’s change detection and view engine (Ivy) is more efficient.

Can code written for AngularJS run in Angular directly?


Answer: No — they're incompatible. Migration requires rewriting or using ngUpgrade for hybrid apps.

What build tools were common for AngularJS and what is typical for Angular?


Answer: AngularJS used Grunt/Gulp/Webpack custom configs; Angular uses Angular CLI (which uses Webpack under the hood).

What is the recommended way to structure applications in Angular that differs from AngularJS?


Answer: Use NgModules, feature modules, component trees, services injected via DI; avoid global $scope and controllers.

Which one uses TypeScript decorators like @Component?


Answer: Modern Angular uses decorators (@Component, @Injectable, etc.). AngularJS does not.

Which supports Ahead-of-Time (AOT) compilation and why is it important?


Answer: Angular supports AOT (compiles templates to JS at build time) — improves startup and catches template errors early. AngularJS had no native AOT.

How do forms differ between AngularJS and Angular?


Answer: AngularJS had ngModel and directives; Angular offers Template-driven and Reactive (Model-driven) Forms within @angular/forms.

Which has better tooling for testing and why?


Answer: Angular — built-in TestBed, typed services/components, CLI-generated spec files, cleaner DI for unit tests.

Is two-way binding still present in Angular? If so, how is it implemented?


Answer: Yes via [(ngModel)] which combines property and event binding, but Angular encourages unidirectional data flow; it requires FormsModule.

What are components analogous to in AngularJS?


Answer: Components in Angular are analogous to directives with templates (.component API introduced in later AngularJS), but Angular enforces component-first architecture.

How are modules different? (angular.module vs NgModule)


Answer: AngularJS modules group app config/run blocks; NgModule defines declarations, imports, providers, and exports for compilation and DI boundaries.

How does dependency graph / tree-shakability compare between the two?


Answer: Angular (with ES modules + AOT + Ivy) supports tree-shaking and smaller bundles better than AngularJS.

What security improvements does Angular have over AngularJS by default?


Answer: Angular has a built-in DOM sanitizer, stricter template expression rules, and AOT catches template injection patterns; AngularJS relied more on developer discipline.

If asked to modernize an AngularJS app, what is one realistic migration approach?


Answer: Use ngUpgrade to run AngularJS and Angular side-by-side and progressively rewrite parts into Angular components & modules.

***************************************************************************************************************************************************************************************************************



**Components — Basics & Practical**


What decorator marks a class as an Angular component?
Answer: @Component({...}).

Name the three primary metadata properties of @Component.
Answer: selector, templateUrl (or template), and styleUrls (or styles).

How do you define a component selector that can be used as an attribute?
Answer: Use selector: '[appMy]' (square brackets indicate attribute selector).

How would you create a component selector that is element-only?
Answer: Use selector: 'app-my' (dash-separated, used as <app-my>).

Where must a component be declared for the compiler to recognize it?
Answer: In the declarations array of an NgModule.

Can a component be declared in more than one module?
Answer: No — a component must be declared in exactly one NgModule; share via exports.

What is the role of the component class (TS file)?
Answer: Holds data (properties), methods, lifecycle hooks, and business logic for the template.

What is encapsulation in components?
Answer: How styles are applied/scoped: Emulated (default), None, or ShadowDom via encapsulation metadata.

How do you pass data into a child component?
Answer: Using @Input() properties bound from parent: <child [prop]="value"></child>.

How does a child send events/data back to parent?
Answer: Child uses @Output() with an EventEmitter; parent binds (event)="handler($event)".

Give a minimal component class example with an input and output.
Answer:

@Component({selector:'app-child', template:`<button (click)="send()">Send</button>`})
export class Child {
  @Input() value!: string;
  @Output() change = new EventEmitter<string>();
  send() { this.change.emit('ok'); }
}

What lifecycle hook runs after inputs are set?
Answer: ngOnChanges(changes: SimpleChanges) runs when inputs change; ngOnInit() runs after first ngOnChanges.

When is ngOnInit called?
Answer: After the first ngOnChanges and before the view is rendered; good for initialization.

Is it okay to perform HTTP calls in the constructor? Why/why not?
Answer: Not recommended — constructor should be lightweight for DI; use ngOnInit for initialization like HTTP calls.

What is ChangeDetectionStrategy.OnPush and why use it?
Answer: It tells Angular to check component only when inputs change or an event occurs — improves performance.

How do you make a component reusable across modules?
Answer: Declare it in one module and export it; import that module where needed.

What is a structural directive and give an example inside a component template?
Answer: Directive that alters DOM structure, e.g., *ngIf, *ngFor: <div *ngIf="show">Hi</div>.

How do you lazy-load a component (basic idea)?
Answer: Use dynamic component loader (ViewContainerRef.createComponent) or load a component via route lazy-loading by module.

What is the difference between providers at component level vs module level?
Answer: Component-level creates a new service instance per component subtree; module-level provides singleton across injector.

Can a component implement multiple lifecycle interfaces?
Answer: Yes (e.g., OnInit, OnDestroy, AfterViewInit), each with its hook method.

What happens to component state when it gets destroyed?
Answer: The instance is garbage-collected (if no external refs). ngOnDestroy can cleanup subscriptions.

How do you access a child component's public method from the parent?
Answer: Use @ViewChild(ChildComponent) child!: ChildComponent; then call this.child.method() after view init.

How can you prevent change detection cycles in long lists?
Answer: Use trackBy in *ngFor and OnPush change detection.

What is the purpose of host metadata in @Component?
Answer: To define host element bindings (class/style/event) e.g., host: {'(click)': 'onClick()'}.

How to style only the host element of a component?
Answer: Use :host { ... } in the component’s CSS.

What is a structural vs attribute selector for components?
Answer: Structural changes DOM (*ngIf) — not a selector type. Attribute selector is component selector syntax [attr], attribute assigned on host.

Can a component template use asynchronous async pipe? Give a small example.
Answer: Yes: <div *ngIf="data$ | async as data">{{data.name}}</div>.

How do you test a component’s template property binding in a unit test? (short)
Answer: Create TestBed, compile component, set property on component instance, call fixture.detectChanges(), then check nativeElement text.

What is templateRef and when might you use it?
Answer: A reference to an embedded template (<ng-template #tpl>), used for structural directives or dynamic views.

Why keep components small and focused?
Answer: Easier to test, maintain, reuse, and reason about — single responsibility principle.

***************************************************************************************************************************************************************************************************************

**Templates**

What is interpolation and where is it used?
Answer: {{ expression }} — inserts stringified expression result into HTML content.

Can template expressions contain assignments or loops?
Answer: No assignments allowed; expressions should be side-effect-free and simple (ternary, property access, calls permitted but discouraged).

Why avoid calling methods in templates for performance reasons?
Answer: Methods run every change detection cycle; costly computations can run frequently — use pipes or cached values.

How do you bind an element property (e.g., src)?
Answer: Property binding: [src]="imgUrl".

How to bind to an HTML attribute (e.g., aria-label)?
Answer: Use attribute binding: [attr.aria-label]="label".

How would you disable a button conditionally?
Answer: <button [disabled]="isDisabled">Go</button>.

What is event binding? Show click example.
Answer: (event)="handler()" — <button (click)="onClick()">OK</button>.

How to pass the event object to the handler?
Answer: (click)="onClick($event)".

Explain [(ngModel)] in one line.
Answer: Two-way binding combining [ngModel] and (ngModelChange) — requires FormsModule.

How to loop through a list in template and show index?
Answer: <div *ngFor="let item of items; let i = index">{{i}} - {{item}}</div>.

What is a template reference variable and how to use one for an input?
Answer: #ref gives access to element/component. Example: <input #name /><button (click)="save(name.value)">Save</button>.

How to conditionally add a class?
Answer: [class.active]="isActive" or [ngClass]="{active: isActive}".

When should you use ng-template vs a plain div?
Answer: Use ng-template for deferred/structural content that isn't rendered until instantiation (e.g., custom structural directives, portals).

Explain ng-container and why it’s useful.
Answer: Logical container that doesn't render DOM element — useful for grouping directives without extra markup.

What is a pure pipe vs impure pipe and when to use each?
Answer: Pure pipes run only when input refs change; impure run every CD cycle. Use pure for deterministic transforms; impure for mutable data (rare).

How do you bind a style property like width dynamically?
Answer: [style.width.px]="width" or [style.width]="width + 'px'".

How to prevent XSS when interpolating HTML from a string?
Answer: Angular sanitizes by default; for trusted HTML use DomSanitizer.bypassSecurityTrustHtml(...) cautiously.

Can you access component private members in template?
Answer: Yes — TypeScript privacy is compile-time only; templates can read private members (not recommended).

How to show a default value with interpolation if data is null?
Answer: Use nullish coalescing: {{ value ?? 'default' }} (supported in templates).

How do you conditionally render different templates (two branches)?
Answer: Use *ngIf; else with <ng-template>: <div *ngIf="cond; else other">A</div><ng-template #other>B</ng-template>.

What is ngSwitch and when do you use it?
Answer: Structural directive for multi-branch rendering: <div [ngSwitch]="key"><div *ngSwitchCase="'a'">A</div>....

How does async pipe help with observables in templates?
Answer: It subscribes/unsubscribes automatically and gives latest value for rendering.

How to bind to an input element’s value and react to user typing without ngModel?
Answer: [value]="val" (input)="val=$event.target.value".

Why avoid heavy DOM manipulation inside templates?
Answer: Templates should declaratively describe UI; imperative DOM work breaks Angular’s abstraction and can cause change-detection issues.

What happens if a template expression throws an exception?
Answer: It bubbles up and can break change detection rendering; the error is shown in console and may crash view updates.

***************************************************************************************************************************************************************************************************************
**templateUrl**

What does templateUrl accept — relative or absolute paths?
Answer: Typically relative paths (relative to the component file) or absolute from project root depending on build config; conventionally relative.

If templateUrl path is wrong, what error will you see at runtime/build?
Answer: Build or runtime error like Failed to load ... or 404 for template; AOT will fail compilation with error location.

When would you use template (inline) instead of templateUrl?
Answer: Small templates, examples, or when avoiding extra HTTP requests in very small components; templateUrl is preferred for readability.

How does Angular CLI handle templateUrl during production build?
Answer: CLI and AOT inlines or bundles templates into JS (no runtime HTTP fetch) — templates become part of the build.

Can you use template literals (backticks) with template?
Answer: Yes — template: \<div> multiline </div>`` supports multiline inline templates.

How do relative paths with templateUrl resolve in multi-folder projects?
Answer: They resolve relative to the component's TypeScript file location at compile time.

Does templateUrl work with AOT compilation?
Answer: Yes — AOT resolves and compiles template files at build time.

How would you include an external HTML fragment at runtime (not via templateUrl)?
Answer: Use HttpClient to fetch HTML and DomSanitizer + innerHTML or dynamic component creation; not recommended except specific cases.

If you move a component file, what must you update for templateUrl?
Answer: Update the relative path to the template or keep template file in same relative structure.

Can templateUrl refer to a template generated at runtime?
Answer: No — templateUrl is resolved at compile/build time; runtime template injection requires dynamic component creation or innerHTML.

***************************************************************************************************************************************************************************************************************
**Nested Components & Communication**
What is meant by nested components?
Answer: A component used inside another component’s template forming a parent-child relationship.

How do you include a child component in a parent’s template?
Answer: Use the child selector as an element/attribute: <app-child [input]="value"></app-child>.

How do you access a child DOM element or component instance from the parent?
Answer: Use @ViewChild('ref' or ChildComponent) and access after ngAfterViewInit.

How to project content from parent into child (slot-like)?
Answer: Use <ng-content></ng-content> in child template; parent places content between tags.

How to project multiple slots of content?
Answer: Use named <ng-content select="..."> with selectors to route content into different slots.

Can projected content access child component’s context?
Answer: No — projected content is compiled in parent context; it cannot access child's private properties.

How to communicate from parent to deeply nested descendant components without prop drilling?
Answer: Use a shared service provided in a common ancestor or root (singleton) and communicate via Observables/BehaviorSubject.

What is @ContentChild and when to use it?
Answer: It captures a reference to content projected into a component (elements inside <ng-content>). Use when child needs to interact with projected content.

How do you ensure the child receives updated input values when parent updates them?
Answer: Angular automatically propagates inputs — use ngOnChanges in child to react to value changes.

How to avoid unnecessary re-rendering in nested component trees?
Answer: Use OnPush change detection, immutable inputs, trackBy for lists, and minimize template method calls.

How to call a parent method from a child?
Answer: Emit an event via @Output() and let parent handle; or pass a function reference as input (less common).

How to build a reusable modal component that accepts projected header/body/footer? (short idea)
Answer: Child has <ng-content select="[modal-header]"></ng-content> etc.; parent uses <app-modal><div modal-header>...</div>...</app-modal>.

When using @ViewChildren, what type of value do you get and how to iterate?
Answer: You get a QueryList<T> — iterate using .forEach(...) or convert to array with .toArray() after view init.

How do you detect when projected content changes?
Answer: Use @ContentChildren or @ContentChild and subscribe to changes on the returned QueryList.

What is one common pitfall when nesting components with OnPush change detection?
Answer: Forgetting that OnPush only checks on reference changes — mutating an input object won’t trigger update; you need to replace the reference or trigger change detection manually.
