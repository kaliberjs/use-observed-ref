# useObservedRef
This is an internal library to facilitate the use of Observers in hooks

## Installation
You typically don't install this library directly.

## Usage
```jsx
import { useObservedRef } from './use-observed-ref'

export function useObserver() { 
  const [state, setState] = React.useState(null)
  const createObserver = React.useCallback(
    () => {
      // @ts-ignore
      return new window.Observer(([entry]) => {
        setState(entry)
      })
    },
    []
  );

  const reset = React.useCallback(() => { setState(null) }, [])
  const ref = useObservedRef({ createObserver, reset, disabled: false })

  return { state, ref }
}
```

You can use the disabled option if you want to disable the Observer entirely after a successful callback. E.g.: you want to test if something enters the viewport, but don't to know when it leaves again.

![](https://media.giphy.com/media/3orieUe6ejxSFxYCXe/giphy.gif)

## Disclaimer
This library is intended for internal use, we provide __no__ support, use at your own risk. It does not import React, but expects it to be provided, which [@kaliber/build](https://kaliberjs.github.io/build/) can handle for you.

This library is not transpiled.
