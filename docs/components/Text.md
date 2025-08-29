---
sidebar_position: 3
---

# Text

This component will detect configured Font type, built with the ability to easily customize the font in use, font size, line height, letter spacing and other quick-access props so you do not have to create separate styles. Hint: Wrap Text components into Block components so they wrap correctly within a layout.

:::tip[Animatable!]

This component can be animated via the provided animation helpers. Check the [guide here](/docs/animations.md).

:::

## Usage

To use the Text component, simply import it and pass in the desired props.

```jsx
function MyComponent() {
  return (
    <Text font="Arial" size={[14, 18]} color="#333" textAlign="center">
      Hello World!
    </Text>
  );
}
```

## Configuration

```javascript
/** Inferred from @types/Font.d.ts \*/
font?: Font;
/** Either define [fontSize, lineHeight] or just one size applied to both fontSize and lineHeight \*/
size?: [number, number] | number;
textTransform?: TextStyle["textTransform"];
letterSpacing?: TextStyle["letterSpacing"];
color?: string;
textAlign?: TextStyle["textAlign"];
opacity?: TextStyle["opacity"];
/** Is this element absolutely positioned on screen or not */
absolute?: boolean;
/** The position offsets for absolutely positioned elements. */
offsets?: Offsets;
/** Z-axis ordering. Works as you'd expect */
zIndex?: number;
/** Display or hide content overflow */
overflow?: ViewStyle["overflow"];
flex?: ViewStyle["flex"];
width?: DimensionValue;
height?: DimensionValue;
minHeight?: DimensionValue;
minWidth?: DimensionValue;
maxHeight?: DimensionValue;
maxWidth?: DimensionValue;
/** Can be defined as a css-like rule ([top, left, bottom, right], [vertical, horizontal] etc) or as an object ({ marginHorizontal: 12 }) */
margins?: MarginStyles;
/** Can be defined as a css-like rule ([top, left, bottom, right], [vertical, horizontal] etc) or as an object ({ paddingHorizontal: 12 }) */
paddings?: PaddingStyles;
/** Possible value formats are { col, row }, [col, row] or just a number applied to both column and row gap. */
gap?: GapType;
/** Animations from the provided animation utilities */
animations?: Partial<ViewStyle>;
```
