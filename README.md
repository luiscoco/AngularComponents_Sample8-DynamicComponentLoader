# dynamic-component-loader

https://angular.io/guide/dynamic-component-loader

https://stackblitz.com/~/github.com/luiscoco/AngularComponents_Sample8-DynamicComponentLoader

In Angular, the Dynamic Component Loader (also known as Dynamic Component Creation or Dynamic Component Injection) is a feature that allows you to dynamically load and render components at runtime. It provides a way to create components programmatically and add them to the view hierarchy dynamically, rather than having them defined statically in the template.

The dynamic component loader is useful when you want to load components dynamically based on certain conditions or user interactions, or when you need to create components dynamically in response to data fetched from an API.

Here's a step-by-step explanation of how the dynamic component loader works in Angular:

## Create a dynamic component: 
First, you need to define a component that you want to load dynamically. This component should implement the Component interface and have its own template, styles, and logic.

## Create a dynamic component container: 
Next, create a container component that will serve as the placeholder for the dynamically loaded component. This container component will have a placeholder in its template where the dynamic component will be inserted.

## Use the ComponentFactoryResolver: 
The ComponentFactoryResolver is a service provided by Angular that allows you to create instances of components dynamically. Inject the ComponentFactoryResolver in the component where you want to load the dynamic component.

## Resolve the component factory: 
Use the ComponentFactoryResolver to resolve the factory for the dynamic component you want to load. The factory provides a way to create instances of the component.

## Create and insert the component: 
Once you have the component factory, you can use it to create an instance of the dynamic component. Then, you can insert this component into the container component's view using the ViewContainerRef and createComponent method.

Here's an example that demonstrates how to use the dynamic component loader in Angular:

```typescript
import { Component, ComponentFactoryResolver, ViewChild, ViewContainerRef } from '@angular/core';

@Component({
  selector: 'app-dynamic-component-loader',
  template: `
    <div>
      <button (click)="loadComponent()">Load Dynamic Component</button>
      <ng-template #dynamicComponentContainer></ng-template>
    </div>
  `,
})
export class DynamicComponentLoaderComponent {
  @ViewChild('dynamicComponentContainer', { read: ViewContainerRef })
  container!: ViewContainerRef;

  constructor(private componentFactoryResolver: ComponentFactoryResolver) {}

  loadComponent() {
    // Resolve the component factory for the dynamic component
    const componentFactory = this.componentFactoryResolver.resolveComponentFactory(DynamicComponent);

    // Create an instance of the dynamic component
    const componentRef = this.container.createComponent(componentFactory);

    // You can pass inputs to the component instance
    componentRef.instance.title = 'Dynamic Component Title';
  }
}

@Component({
  selector: 'app-dynamic-component',
  template: '<p>{{ title }}</p>',
})
export class DynamicComponent {
  title: string;
}
```

In the above example, the DynamicComponentLoaderComponent has a button that triggers the loading of the dynamic component. The ViewContainerRef is used to access the container element where the dynamic component will be inserted. The ComponentFactoryResolver is used to resolve the factory for the DynamicComponent. Once the factory is obtained, the createComponent method is used to create an instance of the dynamic component and insert it into the container.

When you click the "Load Dynamic Component" button, an instance of the DynamicComponent will be created and rendered inside the DynamicComponentLoaderComponent.

Note: Don't forget to add the DynamicComponent to the entryComponents array in the module where the DynamicComponentLoaderComponent is declared, as it is required for dynamic component loading to work properly.


