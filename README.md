# Animating React Apps

This project is a practice project from [React - The Complete Guide (incl Hooks, React Router, Redux)](https://www.udemy.com/course/react-the-complete-guide-incl-redux/)

## Key Concepts

display: block/none on two different classes on an element will block any animation

css-animation with `@keyframes`
```css
@keyframes openModal {
  0% {
    // state at 0%
  }
  50% {
    // state at 50%
  }
  100% {
    // state at 100%
  }
}
```
this approach will show lots of elements in the dom at all times which can slow it down a little and is not really React-ish

removing happens instantly so the behavior of animating out react elements doesn't work correctly

### Transition component from 'react-transition-group'

Renders a function with state argument it gives
has 4 states:
- entering
- entered
- exiting
- exited
```js
<Transition
  in={this.state.someState}
  timeout={1000} // time in ms
  mountOnEnter   // add to DOM on enter
  unmountOnExit  // remove from DOM when done exiting
>
  {(state) => (
    <JSX_to_render 
      style={{// custom styles including transitions}}
    >
  )}
</Transition>
```
`timeout` set on Transition component sets how long the 'entering' and 'exiting' states are

returns callbacks during animation:
- onEnter
- onEntering
- onEntered
- onExit
- onExiting
- onExited


### CSSTransition

doesn't use any function in-between tags
use `classNames` property to merge new classes on animations
- can pass a string as a 'trunk' name or a JS object

#### With the Trunk
```js
<CSSTransition
  // ...otherProps,
  classNames="fade-slide"
>
  <JSX>
</CSSTransition>
```
```css
.fade-slide-enter {}

.fade-slide-enter-active {
  animation: openModal 0.4s ease-out forwards;
}

.fade-slide-exit {}

.fade-slide-exit-active {
  animation: closeModal 1s ease-out forwards;
}

```

#### As a JS Object
```js
<CSSTransition
  // ...otherProps,
  classNames={{
    enter: '',
    enterActive: 'ModalOpen',
    exit: '',
    exitActive: 'ModalClosed',
  }}
>
  <JSX>
</CSSTransition>
```
```css
.ModalOpen {
  animation: openModal 0.4s ease-out forwards;
}

.ModalClosed {
  animation: closeModal 1s ease-out forwards;
}
```

