# Reactjs tips

## Use interact params between Container and Child 
```
// Define Container
const Container = ({children})=>{
    const [paramA, setParamA] = useState(false);

    const changeParamA = ()=>{
        setParamA(!paramA);
    }

    return children({paramA, changeParamA});
};


/// In main
<Container>
{
    (paramA, changeParamA)=>{
        return <Div>
            <div>Param status: {paramA}</div>
            <div onClick={changeParamA}>A</div>
        </Div>
    }
}
</Container>
```

## Pass refs as a prop
```
function CustomTextInput(props) {
  return (
    <div>
      <input ref={props.inputRef} />
    </div>
  );
}

class Parent extends React.Component {
  render() {
    return (
      <CustomTextInput
        inputRef={el => this.inputElement = el}
      />
    );
  }
}
```

## Use HOCs for adding some logics
```
function withMouse(Component) {
  return class extends React.Component {
    render() {
      return (
        <Mouse render={mouse => (
          <Component {...this.props} mouse={mouse} />
        )}/>
      );
    }
  }
}

// And the component Mouse
<Mouse>
  {mouse => (
    <p>The mouse position is {mouse.x}, {mouse.y}</p>
  )}
</Mouse>
```

## Avoid use arrow and create function when render. Should define the prop as an instance method
### This is bad
```
class Mouse extends React.PureComponent {
  // Same implementation as above...
}

class MouseTracker extends React.Component {
  render() {
    return (
      <div>
        <h1>Move the mouse around!</h1>

        {/*
          This is bad! The value of the `render` prop will
          be different on each render.
        */}
        <Mouse render={mouse => (
          <Cat mouse={mouse} />
        )}/>
      </div>
    );
  }
}
```
### This is good
```
class MouseTracker extends React.Component {
  // Defined as an instance method, `this.renderTheCat` always
  // refers to *same* function when we use it in render
  renderTheCat(mouse) {
    return <Cat mouse={mouse} />;
  }

  render() {
    return (
      <div>
        <h1>Move the mouse around!</h1>
        <Mouse render={this.renderTheCat} />
      </div>
    );
  }
}
```

## memo
```
  function MyComponent(props) {
    /* render using props */
  }
  function areEqual(prevProps, nextProps) {
    /*
    return true if passing nextProps to render would return
    the same result as passing prevProps to render,
    otherwise return false
    */
  }
  export default React.memo(MyComponent, areEqual);
```

## React forwardRef
```
  const FancyButton = React.forwardRef((props, ref) => (
    <button ref={ref} className="FancyButton">
      {props.children}
    </button>
  ));

  // You can now get a ref directly to the DOM button:
  const ref = React.createRef();
  <FancyButton ref={ref}>Click me!</FancyButton>;
```


## Optimization for Select: with the same input will memorize the same output, dont repeat select func although the output was change by adding some data in array
```
  // https://github.com/reduxjs/reselect

  import { createSelector } from 'reselect'

  const selectShopItems = state => state.shop.items

  const selectSubtotal = createSelector(selectShopItems, items =>
    items.reduce((subtotal, item) => subtotal + item.value, 0)
  )
```

## Rendering large data
```
Using react-window to avoid laggy while rendering large data
```
## Only pass object itself to child component. Do not pass big object and not relative field of object to child => it might be rerender cause by not relative field change.
```
```

## Only create new callback function in the final child component => will not rerender when callback function was created for everychild
```
```

## Always add key when map a list
```
```
## Hooks

## UseContext

##