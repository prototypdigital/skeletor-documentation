---
sidebar_position: 4
---

# InputFocusScrollView - iOS ONLY

This scroll view will automatically scroll to an active input field rendered inside it, provided you attach the `onInputFocus` callback to the input `onFocus` prop. This is a lambda component, returning a callback which you attach to input fields rendered within it.

:::note

This works on iOS only, Android does this by default with android:windowSoftInputMode

:::

## Usage

```jsx
<InputFocusScrollView  focusPositionOffset={0.1}>
	{(onInputFocus) => (
		...
		<Input
		keyboardType="email-address"
		returnKeyType="next"
		placeholder="Your e-mail address"
		label="E-mail Address"
		emptyMessage="You must enter an e-mail."
		errorMessage="E-mail is invalid."
		value={state.email}
		valid={validation.email}
		onFocus={onInputFocus}
		onChangeText={(text) =>  update("email", text)}
		onSubmitEditing={() =>  passwordRef.current?.focus()}
		/>
		...
	)}
</InputFocusScrollView>
```

## Configuration

```javascript
/** Decimal value of screen height percentage the input will be positioned at. */
/** Defaults to 0.3, just above the keyboard. */
focusPositionOffset?: number;
/** Is the scrollview 100% in height or automatic. Defaults to auto. */
height?: "full" | "auto";
/** Margins are applied to ScrollView style, paddings and gap to contentContainerStyle */
/** Can be defined as a css-like rule ([top, left, bottom, right], [vertical, horizontal] etc) or as an object ({ marginHorizontal: 12 }) */
margins?: MarginStyles;
/** Can be defined as a css-like rule ([top, left, bottom, right], [vertical, horizontal] etc) or as an object ({ paddingHorizontal: 12 }) */
paddings?: PaddingStyles;
/** Possible value formats are { col, row }, [col, row] or just a number applied to both column and row gap. */
gap?: GapType;
/** Define border styles, ie: { borderWidth: 1, borderColor: "red" } */
border?: BorderStyles;
```
