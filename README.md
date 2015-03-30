# React NavigationController

[![Build Status][travis-image]][travis-url]
[![NPM version][npm-image]][npm-url]

A React view manager similar to [UINavigationController][ios-controller]

## Instalation

```bash
npm install react-navigation-controller
```

## Demo

<http://aputinski.github.io/react-navigation-controller/examples/>

## Usage

```jsx
const React = require('react');
const NavigationController = require('react-navigation-controller');

class LoginView extends React.Component {
  onLogin() {
    this.props.navigationController.pushView(
      <div>Welcome to the app!</div>
    );
  },
  render() {
    return (
      <div>
        <button onClick={this.onLogin.bind(this)}>
          Login
        </button>
      </div>
    );
  }
}

class App extends React.Component {
  render() {
    const props = {
      // The views to place in the stack. The front-to-back order
      // of the views in this array represents the new bottom-to-top
      // order of the navigation stack. Thus, the last item added to
      // the array becomes the top item of the navigation stack.
      // NOTE: This can only be updated via `setViews()`
      views: [
        <LoginView />
      ],

      // If set to true, the navigation will save the state of each view that
      // pushed onto the stack. When `popView()` is called, the navigationController
      // will rehydrate the state of the view before it is shown.
      // Defaults to false
      // NOTE: This can only be updated via `setViews()`
      preserveState: true,

      // The spring tension for transitions
      // http://facebook.github.io/rebound-js/docs/rebound.html
      // Defaults to 10
      transitionTension: 12,
      
      // The spring friction for transitions
      // Defaults to 6
      transitionFriction: 5
    };
    return (
      <NavigationController {...props} />
    );
  }
}
```

## API

Once a view is pushed onto the stack, it will recieve a `navigationController` prop
with the following methods:

### `pushView(view, [options])`

Push a new view onto the stack

**Arguments**

##### `view` `{ReactElement}`

Any valid React element (`React.PropTypes.element`)

##### `options` `{object}` <a name="push-options"></a>

Addtional options

##### `options.transiton` `{number|function}` `default=Transition.type.PUSH_LEFT`

Specify the type of transition:

```js
NavigationController.Transition.type = {
  NONE: 0,
  PUSH_LEFT: 1,
  PUSH_RIGHT: 2,
  PUSH_UP: 3,
  PUSH_DOWN: 4,
  COVER_LEFT: 5,
  COVER_RIGHT: 6,
  COVER_UP: 7,
  COVER_DOWN: 8,
  REVEAL_LEFT: 9,
  REVEAL_RIGHT: 10,
  REVEAL_UP: 11,
  REVEAL_DOWN: 12
};
```

A function can be used to perform custom transitions:

```jsx
navigationController.pushView(<MyView />, {
  transition(prevElement, nextElement, done) {
    // Do some sort of animation on the views
    prevElement.style.transform = 'translate3d(100%, 0, 0)';
    nextElement.style.transform = 'translate3d(0, 0, 0)';
    // Tell the navigationController when the animation is complete
    setTimeout(done, 500);
  }
});
```

##### `options.onComplete` `{function}`

Called once the transition has completed

***

### `popView([options])`

Pop the last view off the stack

**Arguments**

##### `options` `{object}`

Addtional options - see [Push()](#push-options)

##### `options.transiton` `{number|function}` `default=Transition.type.PUSH_RIGHT`

***

### `setViews(views, [options])`

Replaces the views currently managed by the navigationController
with the specified views

**Arguments**

##### `views` `{[ReactElement]}`

The views to place in the stack. The front-to-back order of the
views in this array represents the new bottom-to-top order of the views
in the navigation stack. Thus, the last view added to the array
becomes the top item of the navigation stack.

##### `options` `{object}`

Addtional options - see [Push()](#push-options)

##### `options.preserveState` `{boolean}` `default=false`

If set to `true`, the navigationController will save the state
of each view that gets pushed onto the stack. When `popView()` is called,
the navigationController will rehydrate the state of the view before it is shown.

## Styling

No default styles are provided, but classes are added for custom styling:

```html
<div class="ReactNavigationController">
  <!-- This is the element that gets animated -->
  <div class="ReactNavigationControllerView">
    <!-- CURRENT <VIEW /> -->
  </div>
</div>
```

Check out the examples for some basic CSS.

## Dev

```bash
npm install
npm start
```

Visit [http://localhost:3000/index.dev.html]()

[ios-controller]: https://developer.apple.com/library/ios/documentation/UIKit/Reference/UINavigationController_Class/

[npm-url]: https://npmjs.org/package/react-navigation-controller
[npm-image]: http://img.shields.io/npm/v/react-navigation-controller.svg

[travis-url]: https://travis-ci.org/aputinski/react-navigation-controller
[travis-image]: http://img.shields.io/travis/aputinski/react-navigation-controller.svg

