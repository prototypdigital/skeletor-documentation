# Animations

## Overview

The concept behind this approach is to:

1. Define element animations and how they are triggered via `animateParallel`, `animateSequence` or `animateStagger`.
2. Place compiled element animations on an animation timeline OR trigger element animations separately.

Use these methods to construct <b>element</b> animations in a super simple way. Create these animations outside the component body to avoid unnecessary re-renders and other lifecycle related issues. All animations are done via native driver, <i>except if the animation loops to avoid issues with the animation itself.</i>

## animateParallel

`animateParallel` will animate all of the defined element styles in parallel (meaning they will all start animating at the same time). In the example below, this means that opacity, translateY and translateX will all start animating at once. Additional configuration is possible as a second parameter, where you can define the animation `duration`, `loop` and `easing`. The default configuration is `{ duration = 400, easing = Easing.inOut(Easing.ease), loop = false, native = true, }`.

### Usage

```javascript
const element1 = animateParallel({
  opacity: [0, 1],
  translateX: [20, 0],
  translateY: [20, 0],
});
```

## animateSequence

`animateSequence` will animate all of the defined element styles in sequence (meaning every property will start animating only when the previous property has finished animating). In the example below, that means that opacity, translateY and translateX will animate in sequence as they are defined - opacity first, translateX second, translateY last. Additional configuration is possible as a second parameter, where you can define the animation `duration`, `loop` and `easing`. The default configuration is `{ duration = 400, easing = Easing.inOut(Easing.ease), loop = false, native = true, }`.

### Usage

```javascript
const element1 = animateSequence({
  opacity: [0, 1],
  translateX: [20, 0],
  translateY: [20, 0],
});
```

## animateStagger

`animateStagger` will animate all of the defined elements in the order they are defined at a staggered pace defined in the configuration object (meaning every property will start animating after an X amount of miliseconds between animation starts, in the order they are defined in). In the example below, that means that opacity, translateY and translateX will animate in sequence with a 400ms delay between them. Additional configuration is possible as a second parameter, where you can define the animation `duration`, `stagger`, `loop` and `easing`. The default configuration is `{ duration = 400, stagger = 200, easing = Easing.inOut(Easing.ease), loop = false, native = true, }`.

### Usage

```javascript
const element1 = animateStagger({
  opacity: [0, 1],
  translateX: [20, 0],
  translateY: [20, 0],
});
```

## Defining element animation timeline

Once defined, the animations can be layed out on a timeline using the `createAnimationTimeline` function. The return value of the `createAnimationTimeline` is an `Animated.CompositeAnimation` wrapping all defined animations on the timeline, giving you a single start/stop function to trigger all animations wrapped in the timeline.

The configuration object is of type `{ [ms: number]: ElementAnimation<K>[]; }`, with the key of the object representing the point-in-time in ms when the associated animation array will trigger. In the following example, this means that, once started, at 0ms (without delay) the `element1` animation set will start, and at 2000ms the `element2` animation will start.

## Everything combined

### Usage

```javascript
const element1 = animateParallel({ opacity: [0, 1] }, { duration: 400 });
const element2 = animateStagger(
  {
    opacity: [0, 1],
    translateX: [20, 0],
    translateY: [20, 0],
  },
  { stagger: 1200, duration: 800 },
);

const timeline = createAnimationTimeline({
  0: [element1],
  2000: [element2],
});

export const Component: React.FC = () => {
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
const element = animateStagger(
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

Whatever animation you create, just wrap it in `loopAnimation` and it'll loop itself. You can start it as you would any other animation.

### Usage

```javascript
const element1 = loopAnimation(
  animateParallel({
    opacity: [0, 1],
    translateX: [20, 0],
    translateY: [20, 0],
  })
);
```
