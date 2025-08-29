---
sidebar_position: 1
---

# Screen

Use this as the top-level wrapper for every screen you navigate to. It is not intended to be used as a wrapper for other components, as you may deduce from the name. Think of it as a route-specific Layout component.

## Usage

```jsx
function HomeScreen: React.FC = () => {
  return (
    <Screen
      hideBottomSafeArea
      hideTopSafeArea
      background={background || <GradientTriple />}
      scrollable={scrollable}
      statusBarType={scheme === "dark" ? "light-content" : "dark-content"}
      paddings={{ paddingHorizontal: 20, paddingTop: 12 }}
    >
      {children}
    </Screen>
  )
}
```

## Configuration

Component-specific properties are:

```javascript
  /** Pass a specific background view OR just a background color value. Custom components should be 100% height and width. */
  background?: React.ReactNode | ColorValue;
  /** Hides the SafeAreaView rendered at the top of the screen */
  hideTopSafeArea?: boolean;
  /** Hides the SafeAreaView rendered at the bottom of the screen */
  hideBottomSafeArea?: boolean;
  /** Changes the background color of the bottom SafeAreaView. Only works when hideBottomSafeArea is false / undefined */
  bottomSafeAreaColor?: ColorValue;
  /** Changes the background color of the top SafeAreaView. Only works when hideTopSafeArea is false / undefined */
  topSafeAreaColor?: ColorValue;
  /** Either dark-content or light-content. Overrides global default set through provider */
  statusBarType?: StatusBarStyle;
  /** Sets the background color of the status bar. Defaults to transparent. */
  statusBarBackground?: ColorValue;
  /** When set to true, the application will draw under the status bar. Defaults to false. */
  statusBarTranslucent?: StatusBarProps["translucent"];
```

The component also extends [Block properties](/docs/components/Block.md) for further configuration options.
