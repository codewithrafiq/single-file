# Global state By Only React


## Reducet and InitialState

```javascript
  export const initialState = {
    profile: null,
  };

  const reducer = (state, action) => {
    console.log(action.type);
    switch (action.type) {
      case "ADD_PROFILE":
        return {
          ...state,
          profile: action.profile,
        };

      default:
        return state;
    }
  };

  export default reducer;
```

## State Provider


```javascript
  import React from "react";
import { createContext, useContext, useReducer } from "react";

export const Context = createContext();

export const StateProvider = ({ reducer, initialState, children }) => {
  return (
    <Context.Provider value={useReducer(reducer, initialState)}>
      {children}
    </Context.Provider>
  );
};

export const useStateValue = () => useContext(Context);
```
## Send State by Header
```javascript
  import React from "react";
import ReactDOM from "react-dom";
import "./index.css";
import App from "./App";
import { StateProvider } from "./State/StateProvider";
import reducer, { initialState } from "./State/raducer";

ReactDOM.render(
  <StateProvider reducer={reducer} initialState={initialState}>
    <App />
  </StateProvider>,

  document.getElementById("root")
);
```
## Get or update global state
```javascript
    const [{ cartproductf_uncomplit }, dispatch] = useStateValue()
    dispatch({
      type:"<str>",
      <name>:<data>
    })
```
