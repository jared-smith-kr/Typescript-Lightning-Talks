# Talk \#6 React

* [CodeSandbox]()
* [Recording \[talk starts at \]]()

## How to use ur types good on React things

There are a few general rules of thumb to working with React in Typescript. **OPINION WARNING**

* Be judicious in your use of inline types (prefer interfaces and declared types)
* *Most* of the React types are generic. Don't be afraid to explicitly pass type params.
* Always check to see if React itself has a type for a thing before making a one-off declaration.
* DRY

Lets look at each of those. And by that I mean some code that violates all of them:

```typescript
const MyAwesomeComponent: React.FC<{
    someThing: string,
    onClick: (evt: React.SyntheticEvent) => void,
    user: {
        userName?: string,
        userID?: string,
        avatar?: string,
        reputation?: number
    },
    children?: React.ReactNode,
}> = (props: {
    someThing: string,
    onClick: (evt: React.SyntheticEvent) => void,
    user: {
        userName?: string,
        userID?: string,
        avatar?: string,
        reputation?: number
    },
    children?: React.ReactNode,
}): React.Element => {
    const [someState, setSomeState] = useState(null);
    return (<div onClick={React.useCallback((evt: React.SyntheticEvent) => { setSomeState('clicked'); props.onClick(evt); }, [])}>
        {props.user.userName + someState}
        {props.children}
    </div>);
}
```

If you put that in production, I hate you (just kidding). Lets look at it again with the passive-aggressive linter turned on in the editor:

```typescript
const MyAwesomeComponent: React.FC<{
    someThing: string,
    onClick: (evt: React.SyntheticEvent) => void,
    user: {
        userName?: string,              // <- Nested inline definitions in a generic parameter!
        userID?: string,
        avatar?: string,
        reputation?: number
    },
    children?: React.ReactNode,  // <- React already has a generic helper type for this
}> = (props: {
    someThing: string,
    onClick: (evt: React.SyntheticEvent) => void,
    user: {
        userName?: string,
        userID?: string,                // <- Exactly the same as the generic parameter above
        avatar?: string,
        reputation?: number
    },
    children?: React.ReactNode,
}): React.Element => { // <- This is implied by the FC annotation on MyAwesomeComponent
    const [someState, setSomeState] = useState(null);  // <- useState is generic, no need to pre-seed with null and will fail on set
    return (<div onClick={React.useCallback((evt: React.SyntheticEvent)) => { setSomeState('clicked'); props.onClick(evt); }, [])}>
        {props.user.userName + ' ' + someState} // <- user sees 'null' FOUC
        {props.children}
    </div>);
}
```

Do note that the above code is *technically* correct except for the issue with the state being of type `null`. It's just horrible from a readability standpoint: there's *soooo* much noise. So lets fix it:

```typescript
import React, {
    FC,
    PropsWithChildren,
    SyntheticEvent,
    useCallback,
    useState,
} from 'react';

interface User {
    userName?: string;
    userID?: string;
    avatar?: string;
    reputation?: number;
}

interface MyAwesomeComponentProps {
    someThing: string;
    onClick: (evt: SyntheticEvent) => void;
    user: User;
}

// N.B. the type of props and the return type of the function
// are covered by the FC annotation, no need to repeat.
export const MyAwesomeComponent: FC<PropsWithChildren<MyAwesomeComponentProps>> = ({
    someThing,
    onClick,
    user,
    children,
}) => {
    // could also use empty string as default
    const [someState, setSomeState] = useState<string>();
    const clickHandler = useCallback((evt: Event) => {
        setSomeState('clicked');
        props.onClick(evt);
    }, []);
    
    return <div onClick={clickHandler}>{children}</div>;
};
```

We'll dig into each of these different aspects:

## Components Components Components

The main types relating to components are:

* `React.Component` remember classes also define a type. This is the base type of class components.
* `React.FC` a.k.a. `React.FunctionComponent` the type of React function components.
* `React.ComponentType` Covers both function and class components, **use this type for component *arguments***.
* `React.ReactElement` the *return type* of e.g. function components. 

### Props

The main types relating to props are:

* `React.ReactChild` either an `React.ReactElement`, string, or number.
* `React.ReactNode` this is the **correct type for `children`**: includes `React.ReactChild` but can also be null, undefined, a fragment, or a portal.
* `React.PropsWithChildren` a helper type for adding children to your props.
* `React.PropsWithRef` same thing for `ref`s.

If you have some special case that would necessitate using something other than the above where one would normally use one of those, *please document why in a comment*.

### FCs

Defining FCs is usually pretty simple, but exercise good taste in coding similar to the example code above **OPINION ALERT**:

1. The `FC` type annotation on the variable is sufficient: you do not need to inline specify the type of props or the return type and doing so just clutters the code.
2. Don't define the type of your props inline (including as the generic argument to FC) unless they are *extremely* simple, and if you do this please make good use of whitespace in formatting.
3. Use the correct types from the lists above for React things.

## Hooks

Hooks deserve their own special mention. Hooks are *generic* (see talk #4), so they will infer the type of the thing(s) you pass them. The way I see this *usually* tripping people up especially when porting Javascript code to Typescript is that they provide no default or a bad default to `useState`, just like in the example above. Espescially if you have an object in state:

```typescript
const MyComponent = () => {
    const [state, setState] = useState({});
    const clicker = (evt: Event) => {
        setState({ clicked: true }); // <-- Error! property 'clicked' not compatible with type '{}'
    };
    return <button onClick={clicker}>Click Me!</button>;
};
```

Bad: empty object, empty array, null, undefined. If you don't have a good default value and find yourself tempted to reach for one of these, you can pass the type argument explicitly:

```typescript
const MyComponent = () => {
    const [state, setState] = useState<{ clicked?: boolean }>({});
    const clicker = (evt: Event) => {
        setState({ clicked: true }); // <-- now ok
    };
    return <button onClick={clicker}>Click Me!</button>;
};
```

Similarly, `useReducer` takes arguments for reducers:

```typescript
enum StateChange {
    CLICK,
    EMPTY,
    INPUT,
}

interface BaseReducerAction {
    type: StateChange;
}

interface ClickAction extends BaseReducerAction {
    type: StateChange.CLICK;
}

interface ResetAction extends BaseReducerAction {
    type: StateChange.EMPTY;
}

interface InputAction extends BaseReducerAction {
    type: StateChange.INPUT;
    clicked: boolean;
    inputValue: string;
}

type ReducerAction = ClickAction
    | ResetAction
    | InputAction;

interface MyCompnentState {
    clicked?: boolean;
    inputValue?: string;
}

interface MyComponentProps {
    initialValue?: string;
}

const reducer = (state: MyComponentState, action: ReducerAction): MyComponentState => {
    switch (action.type) {
        case StateChange.CLICK: return { ...state, clicked: true };
        case StateChange.EMPTY: return {};
        case StateChange.INPUT: return { ...state, inputValue: action.inputValue };
        default throw new Error('Unknown Action dispatch');
    }
}

const MyComplicatedComponent: FC<MyComponentProps> = ({ initialValue }) => {
    const [{
        clicked,
        inputValue,
    }, dispatch] = useReducer(reducer, { inputValue: initialValue || '' });

    const handleChange = (evt: InputEvent) => {
        dispatch({
            type: StateChange.INPUT,
            inputValue: evt.target.value,
        });
    }

    return (<>
        <button onClick={(_: Event) => dispatch({ type: StateChange.CLICK })}>
            {clicked ? 'Clicked' : 'Click Me!'}
        </button>
        <input value={inputValue} onChange={handleChange} />
    </>);
};
```

Again, `useReducer` should pick up the correct types here but if it doesn't you can explicitly pass them:

```typescript
const [{
  clicked,
  inputValue,
}, dispatch] = useReducer<MyComponentState, ReducerAction>(
    reducer,
    { inputValue: initialValue || '' },
);
```

When troubleshooting React typing issues verify that the thing has the inferred generic type you think it should!

## Go To Definition is your friend

If you want to see what the definition of a React type is, be sure to use whatever your editor's version of 'Go To Definition' is. This has the advantage of checking the definition for the *specific* version of React you're using.
