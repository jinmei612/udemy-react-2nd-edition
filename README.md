# udemy-react-2nd-edition
notes for Udemy course 

### Set up dev env:

- To install [Babel](https://babeljs.io/repl#?browsers=defaults%2C%20not%20ie%2011%2C%20not%20ie_mob%2011&build=&builtIns=false&spec=false&loose=false&code_lz=MYewdgziA2CmB00QHMAUAiALrCn0EoAoQgNwEMAnAAmwFsAHaM7KgXioB56A-GnTDgHoeQA&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=false&fileSize=false&timeTravel=false&sourceType=module&lineWrap=true&presets=env%2Creact%2Cstage-2%2Cenv&prettier=false&targets=&version=7.11.6&externalPlugins=)
: `yarn global add babel-cli@6.24.1`

- Install preset:
`yarn add babel-preset-react@6.24.1 babel-preset-env@1.5.2`

- `yarn.lock` and `node_modules` got auto generated, don't edit directly: https://a.cl.ly/o0umbzLL


- compile
`babel src/app.js --out-file=public/scripts/app.js --presets=env,react` (We are writing react code in `src/app.js`, and `public/scripts/app.js` will be used in html which contains `React.createElement()` )


- `yarn global add live-server` # install live-server
- `live-server public` # to start the server, `public` is where I saved my code (html and app.js - the one returned by babel)
- `babel src/app.js --out-file=public/scripts/app.js --presets=env,react --watch` # babel will watch for changes in src/app.js and compile, and browser should reload everytime we update and save src/app.js

- Text editor: Visual Studio + Extension: ESLint

-------------------

### Start coding:

- Load react and react-dom in `index.html`

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>Indecision App</title>
    </head>
    <body>
        <div id="app"></div>
        <script src="https://unpkg.com/react@16.0.0/umd/react.development.js"></script>
        <script src="https://unpkg.com/react-dom@16.0.0/umd/react-dom.development.js"></script>
        <script src="/scripts/app.js"></script>
    </body>
</html>
```


Note: 
In app.js, to have 2 tags under a var, wrap them with `<div>` tag. e.g.
```
var template = (
    <div>
        <h1>Indecision App</h1>
        <p>This is JSX from app.js</p>
    </div>
);
```


#### render

in `app.js`

`ReactDOM.render(template,appRoot)` 
where `template` is the variable that contains xml code. e.g
```
var template = (
    <div>
        <h1>{app.title}</h1>
        <p>{app.subtitle}</p>
        <ol>
            <li>Item one</li>
            <li>Iteam Two</li>
        </ol>
    </div>
);
```



and the 2nd parameter:  `var appRoot = document.getElementById("app")`, you can add `<div id="app"></div>` in index.html to use it.

#### logic operator 

`user.name ? user.name : 'Anonymous'` 
= if user.name, return user.name, else return 'Anonymous'

`{app.subtitle && <p>{app.subtitle}</p>}`
= if app.subtitle, return app.subtitle, else do nothing

#### var, let, const
- when using `var`, you can redefine the same variable without noticing that the name has also already been define before
- `let`, doesn't allow redefine, but can reassign
- `const`, cannot redefine, cannot reassign

#### arrow function
(anonymous function in es6, similar to lambda function in Python)
e.g.
```
//es5
const square = function (x) {
    return x * x;
}

function squareTwo (x) {
    return x * x;
}

//es6
const squareArrow = (x) => {
    return x * x;
}
const squareArrowTwo = (x) => x * x;
console.log(squareArrow(9))
```

How to convert?
1 - remove `function` keyword
2 - add `=>` after (arguments)


**Playground**
```
const render = () => {
    const jsx = (
        <div>
            <h1>Header</h1>
        </div>

    );
    ReactDOM.render(jsx, document.getElementById('app'))
};
render();
```

#### Class
`constructor` -

`extends` - 

`super` -


```
class Person {
    constructor(name = 'N/A', id = 0) {
        this.name = name;
        this.id = id;
    }
    Somefunction() {
        return `Hi. I am ${this.name}`;
}
```

```
class SE extends Person {
    constructor(name = 'N/A', id = 0, currentSpec, pastSpec, ticketToday, thresholdToday) {
        super(name, id);
        this.currentSpec = currentSpec;
        this.pastSpec = pastSpec;
        this.ticketToday = ticketToday;
        this.thresholdToday = thresholdToday;
    }
    metThreshold() {
        return this.ticketToday - this.thresholdToday >= 0;
    }
}
```

### Props vs. State

Props 
- An object
- Can be used when rendering
- Changes (from parent) cause re-renders
- Comes from above (parent)
- Can't be changed by component itself

State
- An object
- Can be used when rendering
- Changes cause re-renders
- Defined in component itself
- Can be changed by component itself

### Stateless function

The below 2 code blocks do the same job:

- use class if you need to use state

```
class Header extends React.Component {
    render() {
        return (
            <div>
                <h1>{this.props.title}</h1>
                <h2>{this.props.subtitle}</h2>
            </div>
        );
    }
}
```

- otherwise, use this method, it will be faster

```
const Header = (props) => {
    return (
        <div>
            <h1>{props.title}</h1>
            <h2>{props.subtitle}</h2>
        </div>
    );
};
```

### react component lifecycle
https://reactjs.org/docs/react-component.html
