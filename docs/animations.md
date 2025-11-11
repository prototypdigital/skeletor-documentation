# Animations

## Overview

The concept behind this approach is to:

1. Define element animations and how they are triggered via `useAnimateParallel`, `useAnimateSequence` or `useAnimateStagger`.
2. Place compiled element animations on an animation timeline OR trigger element animations separately.

Use these methods to construct <b>element</b> animations in a super simple way. Create these animations outside the component body to avoid unnecessary re-renders and other lifecycle related issues. All animations are done via native driver, <i>except if the animation loops to avoid issues with the animation itself.</i>

## Parallel

`useAnimateParallel` will animate all of the defined element styles in parallel (meaning they will all start animating at the same time). In the example below, this means that opacity, translateY and translateX will all start animating at once. Additional configuration is possible as a second parameter, where you can define the animation `duration` and `easing`. The default configuration is `{ duration = 400, easing = Easing.inOut(Easing.ease), native = true, }`.

### Usage

```javascript
const element1 = useAnimateParallel({
  opacity: [0, 1],
  translateX: [20, 0],
  translateY: [20, 0],
});
```

## Sequence

`useAnimateSequence` will animate all of the defined element styles in sequence (meaning every property will start animating only when the previous property has finished animating). In the example below, that means that opacity, translateY and translateX will animate in sequence as they are defined - opacity first, translateX second, translateY last. Additional configuration is possible as a second parameter, where you can define the animation `duration` and `easing`. The default configuration is `{ duration = 400, easing = Easing.inOut(Easing.ease), native = true, }`.

### Usage

```javascript
const element1 = useAnimateSequence({
  opacity: [0, 1],
  translateX: [20, 0],
  translateY: [20, 0],
});
```

## Stagger

`useAnimateStagger` will animate all of the defined elements in the order they are defined at a staggered pace defined in the configuration object (meaning every property will start animating after an X amount of miliseconds between animation starts, in the order they are defined in). In the example below, that means that opacity, translateY and translateX will animate in sequence with a 400ms delay between them. Additional configuration is possible as a second parameter, where you can define the animation `duration`, `stagger` and `easing`. The default configuration is `{ duration = 400, stagger = 200, easing = Easing.inOut(Easing.ease), native = true, }`.

### Usage

```javascript
const element1 = useAnimateStagger({
  opacity: [0, 1],
  translateX: [20, 0],
  translateY: [20, 0],
});
```

## Defining element animation timeline

Once defined, the animations can be layed out on a timeline using the `useAnimationTimeline` function. The return value of the `useAnimationTimeline` is an `Animated.CompositeAnimation` wrapping all defined animations on the timeline, giving you a single start/stop function to trigger all animations wrapped in the timeline.

The configuration object is of type `{ [ms: number]: ElementAnimation<K>[]; }`, with the key of the object representing the point-in-time in ms when the associated animation array will trigger. In the following example, this means that, once started, at 0ms (without delay) the `element1` animation set will start, and at 2000ms the `element2` animation will start.

## Everything combined

### Usage

```javascript

export const Component: React.FC = () => {
  const element1 = useAnimateParallel({ opacity: [0, 1] }, { duration: 400 });
  const element2 = useAnimateStagger(
    {
      opacity: [0, 1],
      translateX: [20, 0],
      translateY: [20, 0],
    },
    { stagger: 1200, duration: 800 },
  );

  const timeline = useAnimationTimeline({
    0: [element1],
    2000: [element2],
  });

	...
	useEffect(() => {
		if(startAnimation) {
			timeline.start();
		} else {
			timeline.reset();
		}
	}, [startAnimation])

	return <Block animations={element1.animations}>...</Block>
}
```

## Reversing element animations.

Instead of just reseting the animation, which does not play the animation back in reverse, the utility also exposes a `reverse` function which will animate the element back to it's initial values.
Instead of `element.reset()`, use `element.reverse()`. This can also be used on timelines.

### Usage

```javascript
const element = useAnimateStagger(
  {
    opacity: [0, 1],
    translateX: [20, 0],
    translateY: [20, 0],
  },
  { stagger: 1200, duration: 800 },
);

...

useEffect(() => {
  if (startAnimation) {
    element.start();
  } else {
    element.reverse();
  }
}, [startAnimation]);
```

## Looping animations

Loop animations allow you to continuously repeat an animation sequence indefinitely. This is perfect for creating loading spinners, rotating elements, pulsing effects, or any other animation that needs to run continuously. The `useLoopAnimation` hook wraps any animation sequence and automatically restarts it when it completes.

You can pass either a predefined sequence or create the sequence inline:

```javascript
export const Component: React.FC = () => {
  // Option 1: Define the sequence separately
  const sequence = useAnimateSequence(
    { rotation: ["0deg", "360deg"] },
    { duration: 1000, easing: Easing.linear }
  );
  const rotate = useLoopAnimation(sequence);

  // Option 2: Create the sequence inline
  const rotate = useLoopAnimation(
    animateSequence(
      { rotation: ["0deg", "360deg"] },
      { duration: 1000, easing: Easing.linear }
    )
  );

  useEffect(() => {
    rotate.start();
  }, []);

  return <Block animations={rotate.animations}>...</Block>;
};
```

:::note

The `useAnimationStagger`, `useAnimationParallel`, `useAnimationSequence`, `useAnimationTimeline` and `useLoopAnimation` hooks are basically just `useRef` wrappers around the `animateStagger`, `animateParallel`, `animateSequence`, `createAnimationTimeline` and `loopAnimation` animation utilities to make sure the animated value isn' reset between renders and to provide an easier to use syntax.

You can still use the utilities directly when created outside the component, but the suggested approach is to create animations per component instance, not globally.
:::
