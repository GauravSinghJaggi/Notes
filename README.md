# 📘 Angular Beginner Deep-Dive- Questions & Answers

> A curated **Angular fundamentals interview/practice guide** focused on:
>
> * Angular vs AngularJS
> * Components
> * Templates
> * `templateUrl`
> * Nested Components
>
> Designed for **beginners preparing for interviews or strengthening Angular fundamentals**.

---

# 📚 Table of Contents

* [Angular vs AngularJS](#angular-vs-angularjs)
* [Angular Components](#angular-components)
* [Angular Templates](#angular-templates)
* [templateUrl](#templateurl)
* [Nested Components](#nested-components)

---

# Angular vs AngularJS

<details>
<summary>Questions & Answers</summary>

### 1. What is the core difference between AngularJS and Angular?

AngularJS uses **controllers and scopes**, while Angular uses a **component-based architecture**.

### 2. Which language is mainly used in Angular development?

Angular uses **TypeScript**.

### 3. Which language did AngularJS primarily use?

AngularJS used **JavaScript**.

### 4. Why did Google rewrite AngularJS into Angular?

To improve **performance, maintainability, and scalability**.

### 5. What is the basic building block in AngularJS?

Controllers and directives.

### 6. What is the basic building block in Angular?

Components.

### 7. What architecture does AngularJS follow?

MVC / MVVM.

### 8. What architecture does Angular follow?

Component-based architecture.

### 9. Which framework supports TypeScript by default?

Angular.

### 10. What major performance issue existed in AngularJS?

The **digest cycle with watchers** caused performance issues.

### 11. What compilation approach does Angular support?

Ahead-of-Time (AOT) compilation.

### 12. What is SPA?

Single Page Application where the page **does not reload fully**.

### 13. Is AngularJS still recommended for new projects?

No.

### 14. Does AngularJS support dependency injection?

Yes, but it is simpler compared to Angular.

### 15. How is routing handled in Angular?

Using **Angular Router**.

### 16. What build tool is commonly used with Angular?

Angular CLI.

### 17. Does Angular support tree-shaking?

Yes.

### 18. Which version introduced component architecture?

Angular 2+.

### 19. Can AngularJS code run directly inside Angular?

No.

### 20. Which framework is better for enterprise apps?

Angular.

</details>

---

# Angular Components

<details>
<summary>Questions & Answers</summary>

### 21. What is a component?

A **self-contained UI block** containing logic, template, and styling.

### 22. Which decorator defines a component?

`@Component`

### 23. What does the selector property define?

The **HTML tag used to render the component**.

### 24. Example selector usage

```
selector: 'app-header'
```

Used as:

```
<app-header></app-header>
```

### 25. What does the component class contain?

Application logic and variables.

### 26. What does the HTML file contain?

UI structure.

### 27. What does the CSS file contain?

Styling.

### 28. What happens if a component is not declared in a module?

Angular throws an error.

### 29. Can multiple components share the same selector?

No.

### 30. What is the root component?

`AppComponent`

### 31. Where is the root component defined?

`app.component.ts`

### 32. Where is it rendered?

Inside `index.html`

### 33. Example root rendering

```
<app-root></app-root>
```

### 34. Can a component have multiple CSS files?

Yes.

### 35. What is the role of `styleUrls`?

Attach styles to a component.

### 36. What is component encapsulation?

Styles are scoped to the component.

### 37. Can a component exist without styles?

Yes.

### 38. Can a component exist without template?

No.

### 39. What naming convention is recommended?

`feature.component.ts`

### 40. What principle should components follow?

Single Responsibility Principle.

### 41. What lifecycle hook runs after initialization?

`ngOnInit`

### 42. What decorator allows data input?

`@Input`

### 43. What decorator emits events to parent?

`@Output`

### 44. What object emits events?

`EventEmitter`

### 45. What Angular CLI command creates a component?

```
ng generate component component-name
```

### 46. Can a component contain other components?

Yes.

### 47. What is component reusability?

Using the same component multiple times.

### 48. Why should components be small?

Improves maintainability.

### 49. What file contains component metadata?

`.ts`

### 50. What file contains UI layout?

`.html`

</details>

---

# Angular Templates

<details>
<summary>Questions & Answers</summary>

### 51. What is interpolation?

Displaying data using

```
{{ variable }}
```

### 52. Example

```
<h1>{{ title }}</h1>
```

### 53. What is property binding?

```
<img [src]="imageUrl">
```

### 54. What is event binding?

```
<button (click)="submit()"></button>
```

### 55. What does `$event` represent?

The event object.

### 56. What is two-way binding?

```
[(ngModel)]
```

### 57. Example

```
<input [(ngModel)]="name">
```

### 58. Which module enables ngModel?

FormsModule.

### 59. What directive loops through data?

`*ngFor`

### 60. Example

```
<div *ngFor="let item of items"></div>
```

### 61. What directive shows conditional content?

`*ngIf`

### 62. Example

```
<div *ngIf="isLoggedIn"></div>
```

### 63. What is a template reference variable?

```
<input #name>
```

### 64. Accessing template variable

```
{{name.value}}
```

### 65. What is `ng-container`?

A logical wrapper that **does not render DOM**.

### 66. What is `ng-template`?

Defines template content not rendered immediately.

### 67. Why avoid complex logic in templates?

Performance issues.

### 68. What pipe handles async data?

`async pipe`.

### 69. Example

```
{{ user$ | async }}
```

### 70. What directive switches cases?

`ngSwitch`

### 71. Example

```
<div [ngSwitch]="role">
```

### 72. What directive binds classes?

`ngClass`

### 73. Example

```
<div [ngClass]="{active: isActive}">
```

### 74. What directive binds styles?

`ngStyle`

### 75. Example

```
<div [ngStyle]="{color:'red'}">
```

</details>

---

# templateUrl

<details>
<summary>Questions & Answers</summary>

### 76. What is `templateUrl`?

It links an **external HTML file to the component**.

### 77. Example

```
@Component({
 templateUrl: './app.component.html'
})
```

### 78. Why use templateUrl instead of inline template?

Cleaner code structure.

### 79. When might inline template be used?

Small components.

### 80. What happens if the path is wrong?

Angular throws a template loading error.

### 81. Does Angular load templates at runtime?

No, they are compiled during build.

### 82. Does templateUrl support AOT compilation?

Yes.

### 83. Are template files bundled in production?

Yes.

### 84. Can templateUrl reference remote URLs?

No.

### 85. What path style is recommended?

Relative paths.

</details>

---

# Nested Components

<details>
<summary>Questions & Answers</summary>

### 86. What are nested components?

Components inside other components.

### 87. Example

```
<app-navbar></app-navbar>
```

Inside

```
app.component.html
```

### 88. What is parent component?

The component containing another component.

### 89. What is child component?

The component being used inside another component.

### 90. How does parent send data to child?

Using `@Input`.

### 91. Example

```
<child [data]="value"></child>
```

### 92. How does child send data to parent?

Using `@Output`.

### 93. Example

```
@Output() notify = new EventEmitter()
```

### 94. What is content projection?

Passing HTML from parent to child.

### 95. Directive used for projection?

`ng-content`

### 96. Example

```
<ng-content></ng-content>
```

### 97. What is ViewChild used for?

Access child component instance.

### 98. Example

```
@ViewChild(ChildComponent)
```

### 99. What lifecycle hook ensures child is available?

`ngAfterViewInit`

### 100. Why are nested components important?

They help build **modular and reusable UI structures**.

</details>

---

# 🚀 How to Use This Repo

You can use this guide to:

* Prepare for **Angular interviews**
* Review **Angular fundamentals**
* Practice **conceptual questions**
* Teach beginners Angular basics

---

# ⭐ Recommended Learning Flow

1️⃣ Angular Fundamentals
2️⃣ Components
3️⃣ Templates
4️⃣ Component Communication
5️⃣ Services & Dependency Injection
6️⃣ Routing
7️⃣ Forms
8️⃣ RxJS

---

# 👨‍💻 Author

Prepared as a **beginner-friendly Angular practice README** for learning and interview preparation.

---

⭐ If this helps you, consider starring the repository!
