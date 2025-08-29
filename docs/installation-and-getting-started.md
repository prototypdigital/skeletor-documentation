---
sidebar_position: 1
---

# Installation & Getting started

## Installation

Installing skeletor is straightforward straightforward:

```bash
 yarn add @prototyp/skeletor
```

Skeletor has <b>no external dependencies</b> and is built exclusively with what React-Native ships with.

## Getting started

### Provider component

Add the SkeletorProvider component as the (or one of) top wrapper of your application like in the following example:

```jsx
/// index.js
const App = () => {
  return (
    <SkeletorProvider>
      <StoreProvider>
        <... />
      </StoreProvider>
    </SkeletorProvider>
  );
};
```

### Provider configuration

The list of available configuration options for SkeletorProvider is as follows:

```javascript
interface SkeletorConfig {
  /** This is the default font applied to the Text component */
  defaultFont: Font | undefined;
  /** This is the default font size + line height applied to the Text component. Format is either [fontSize, lineHeight] or a number that applies as both fontSize and lineHeight. */
  defaultFontSize: [number, number] | number;
  /** Default text color applied to the Text component */
  defaultTextColor: ColorValue;
  /** When set to true, font size will scale based on the user's device settings.
   * Defaults to false */
  allowFontScaling: boolean;
  /** Clamp the maximum font size multiplier that can be applied to the original scale. */
  defaultMaxFontSizeMultiplier?: number;
  /** Determines how the status bar icons are coloured (battery percentage, signal etc.). Can either be light-content or dark-content.
   * Can be overriden via the Screen component per-screen */
  defaultStatusBarType: StatusBarStyle;
  /** Defaults to transparent if not set.
   * Can be overriden via the Screen component per-screen. */
  defaultStatusBarBackground?: ColorValue;
  /** When set to true, the application will draw under the status bar.
   * Defaults to false if not set.
   * Can be overriden via the Screen component per-screen. */
  defaultStatusBarTranslucent?: boolean;
}
```

### Font type declaration

Add the following type declaration for font family type inferrence. Font names must correspond to the font's <u>PostScript name</u> for iOS and the font file name for Android. Suggestion: Rename the font asset file to the PostScript name to support both platforms easily.

```javascript
/// @types/Font.d.ts
type Font = "Helvetica" | "Roboto" | "San Francisco";
```

:::tip[Fonts & their names]
Font names must correspond to the font's <u>PostScript name</u> for iOS and the font file name for Android. Change the font asset file name to the PostScript name to support both platforms easily.

Example: `PostScript name: "MagnatHead-Light" --> assets/fonts/MagnatHead-Light.otf`.
:::

This provides you with proper font names in Intellisense when used, like in the following examples:

```jsx
// Sets the default font in the Text component to Helvetica
<SkeletorProvider defaultFont="Helvetica">...</SkeletorProvider>

// Then this overrides the default Helvetica font and uses Roboto instead
<Text font="Roboto">...</Text>
```
