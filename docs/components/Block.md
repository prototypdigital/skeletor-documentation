---
sidebar_position: 2
---

# Block

This is a flexible and customizable React Native component that can be used as either a `View` or a `ScrollView`. The `Block` component allows you to add paddings, margins, sizes, alignments, and borders to your layout. Can be turned into a ScrollView by passing in `scrollable`. ScrollView props can be updated through `scrollProps`.

:::tip[Animatable!]

This component can be animated via the provided animation helpers. Check the [guide here](/docs/animations.md).

:::

## Usage

```jsx
<Block
  paddings={{ paddingHorizontal: 20, paddingVertical: 12 }}
  flexDirection="row"
  justify="space-between"
  align="center"
  gap={[0, 12]}
>
  ... ...
</Block>
```

```jsx
<Block
  absolute
  offsets={[0, 0, 0, 0]}
  zIndex={1}
  align="center"
  justify="center"
  paddings={{ paddingHorizontal: 20 }}
>
  ... ...
</Block>
```

```jsx
<Block
  gap={12}
  scrollable
  scrollProps={{ showsVerticalScrollIndicator: true }}
  margins={{ marginBottom: 20 }}
>
  ... ...
</Block>
```

... and many more variations

## Configuration

```javascript
/** Determine if Block is scrollable or not.*/
scrollable?: boolean;
/** If scrollable, used to control ScrollView props. Some default props are applied, check JSDOC of component by hovering over it in your IDE. */
scrollProps?: ScrollViewProps
/** Sets the opacity of the element directly. This will be applied to children too. */
opacity?: ViewStyle["opacity"];
/** Animations from the provided animation utilities */
animations?: Partial<ViewStyle>;
/** Can either be a component or a colour value (string) */
background?: JSX.Element | string;
/** Is this element absolutely positioned on screen or not */
absolute?: boolean;
/** The position offsets for absolutely positioned elements. */
offsets?: Offsets;
/** Z-axis ordering. Works as you'd expect */
zIndex?: number;
/** Display or hide content overflow */
overflow?: ViewStyle["overflow"];
/** Align children */
align?: ViewStyle["alignItems"];
/** Align self within container */
alignSelf?: ViewStyle["alignSelf"];
/** Justify children */
justify?: ViewStyle["justifyContent"];
flexDirection?: ViewStyle["flexDirection"];
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
/** Define border styles, ie: { borderWidth: 1, borderColor: "red" } */
border?: BorderStyles;
```
