---
sidebar_position: 2
label: Using Skeletor outside Skeletor components
---

# Using Skeletor outside Skeletor components

To get access to the skeletor styles in other components, you can use the provided `useSkeletor` hook that will return the entire Skeletor configuration object. For instance:

```javascript
const skeletor = useSkeletor();
return <SomeComponent style={{ fontFamily: skeletor.defaultFont }} />;
```

:::tip[Proper nesting]
You cannot use this hook outside the `SkeletorProvider` tree.
:::
