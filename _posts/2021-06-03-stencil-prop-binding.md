---
layout: post
title: Stencil Property Binding
--- 
Want to bind to a property in a stencil app / component lib.

This is the class, and the prop t9n, we will bind to.
```tsx

export class SecondComp {

    @Prop()
    userName: string;

    @Prop()
    t9n: Record<string, string> = {
        greeting: 'Hello',
        farewell: 'Goodbye'
    }

    render() {
        return (
            <Host>
                <div>{this.t9n.greeting + ", " + this.userName }</div>
                <div>{this.t9n.farewell + ", " + this.userName }</div>
            </Host>
        );
    }

}
```

In the class where the data should be passed down.
```tsx
export class MyComponent {

    private t9n = {
        greeting: 'Hallo',
        farewell: 'Auf Wiedersehen'
    }

    render() {
        return <second-comp t9n={this.t9n} user-name={'Jana'}></second-comp>;
    }
}
```

Note that in with property binding you can pass all sorts of data (javascript objects), instead of just simple types like in attribute binding. For the difference on attribute vs. property binding see this answer on [stackoverflow](https://stackoverflow.com/a/10673539).

Happy Prop Binding!!!

Eager to see that yourself?

Either check out my example repo on github or follow these steps or checkout the [sample repo](https://github.com/keo9ren/stencil-prop-binding).

```shell
npm init stencil component
```
Enter Project Name e.g. stencil-prop-binding

```shell
cd project
```

```shell
npm install
```

```shell
npm run generate
```

second-comp

except all other settings

Adapt the contents of the two components

```shell
npm run start
```
