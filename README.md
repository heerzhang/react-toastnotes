<div align="center">
    
# Toasted-notes
  
[![npm package](https://img.shields.io/npm/v/react-toastnotes/latest.svg)](https://www.npmjs.com/package/react-toastnotes)
[![Tweet](https://img.shields.io/twitter/url/http/shields.io.svg?style=social)](https://twitter.com/intent/tweet?text=toasted%20notes%20is%20a%20react%20library%20for%20creating%20simple%2C%20flexible%20toast%20notifications.&url=https://github.com/heerzhang/react-toastnotes&hashtags=react,javascript)
[![Follow on Twitter](https://img.shields.io/twitter/follow/benmcmahen.svg?style=social&logo=twitter)](
https://twitter.com/intent/follow?screen_name=benmcmahen
)

</div>

A simple but flexible implementation of toast style notifications for React extracted from [customize-easy-ui-component](https://github.com/heerzhang/customize-easy-ui-component).
- 原版的包"toasted-notes"无人维护更新，无法适应react-spring v9,依赖有问题，故而只好自建新的包并改名。

[View the demo and documentation](https://toasted-notes.netlify.com/).

## Features

- **An imperative API.** This means that you don't need to set component state or render elements to trigger notifications. Instead, just call a function.
- **Render whatever you want.** Utilize the render callback to create entirely custom notifications.
- **Functional default styles.** Import the provided css for some nice styling defaults or write your own styles.

## Install

Install `react-toastnotes` , using yarn or npm.

```
yarn add react-toastnotes
```

## Example

```jsx
import toaster from "react-toastnotes";
//import "react-toastnotes/src/styles.css"; // optional styles

const HelloWorld = () => (
  <button
    onClick={() => {
      toaster.notify("Hello world", {
        duration: 2000
      });
    }}
  >
    Say hello
  </button>
);
```

## API

The notify function accepts either a string, a react node, or a render callback.

```jsx
// using a string
toaster.notify("With a simple string");

// using jsx
toaster.notify(<div>Hi there</div>);

// using a render callback
toaster.notify(({ onClose }) => (
  <div>
    <span>My custom toaster</span>
    <button onClick={onClose}>Close me please</button>
  </div>
));
```

It also accepts options.

```javascript
toaster.notify("Hello world", {
  position: "bottom-left", // top-left, top, top-right, bottom-left, bottom, bottom-right
  duration: null // This notification will not automatically close
});
```

## Using Context

One downside to the current API is that render callbacks and custom nodes won't get access to any application context, such as theming variables provided by styled-components. To ensure that render callbacks have access to the necessary context, you'll need to supply that context to the callback.

```jsx
const CustomNotification = ({ title }) => {
  const theme = useTheme();
  return <div style={{ color: theme.primary }}>{title}</div>;
};

const CustomNotificationWithTheme = withTheme(CustomNotification);

toaster.notify(() => <CustomNotificationWithTheme title="I am pretty" />);
```

## Contributors

- [Heerzhang](https://github.com/heerzhang)

## License

MIT

## Prior art

Way back, this was originally based on the wonderful implementation of notifications in [evergreen](https://evergreen.segment.com).
