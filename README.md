# React fundamental

## React.createElement()

- ```react
  <script>
    const root = document.getElementById('root');
    const Span = React.createElement(
      'span',
      {
        id: 'title',
        onMouseEnter: () => console.log('mouse enter')
      },
      'Hello I\'m a span.'
    );
    const Btn = React.createElement(
      'button',
      {
        onClick: () => console.log('I\'m clicked!'),
        style: { backgroundColor: 'tomato' }
      },
      'Click me'
    );
    const container = React.createElement('div', null, [Span, Btn]);
    ReactDOM.render(container, root);
  </script>
  ```

## By using JSX

- ```jsx
  <script type="text/babel">
    const root = document.getElementById('root');
    const Span = () => {
      return (
      <span id="title" onMouseEnter={() => console.log('mouse enter')}>Hello I'm a span.</span>
    )};
    const Btn = () => {
      return (
      <button
        style={{
          backgroundColor: 'tomato'
        }}
        onClick={() => console.log('I\'m clicked!')}
      >
      Click me
      </button>
    )};
    const container = (
      <div>
        <Span />
        <Btn />
      </div>
    );
    ReactDOM.render(container, root);
  </script>
  ```

- differences with html
  - `<label for=` to `<label htmlFor=`
  - `<div class=` to `<div className=`
  - `onclick` to `onClick` - camelCase

## State

- ```jsx
  <script type="text/babel">
    const root = document.getElementById('root');
    let counter = 0;

    const countUp = () => {
      counter++;
      // render to apply changed state
      render();
    }

    const render = () => {
      // React renders only changed parts. In this case, the counter
      ReactDOM.render(<Container />, root);
    }

    const Container = () => {
      return (
      <div>
        <h3>Total count: {counter}</h3>
        <button onClick={countUp}>Click Me</button>
      </div>
    )};

    render();
  </script>
  ```

## State Hook (`React.useState()`)

- ```jsx
  <script type="text/babel">
    const root = document.getElementById('root');
    const App = () => {
      // Declare a new state variable, which we'll cal "counter"
      // const data = React.useState(0); // [0, f]
      // const counter = data[0];
      // const setCounter = data[1];
      const [counter, setCounter] = React.useState(0);
      const onClick = () => {
        // the modifier function changes the state and re-render
        // setCounter(counter + 1);
        // to calculate next state from the current state, it's safer
        setCounter((counter) => counter + 1);
      }
      return (
      <div>
        <h3>Total count: {counter}</h3>
        <button onClick={onClick}>Click Me</button>
      </div>
    )};

    ReactDOM.render(<App />, root);
  </script>
  ```

- Practice: converter

  - ```jsx
    <script type="text/babel">
      const App = () => {
        const [amount, setAmount] = React.useState(0);
        const [flipped, setFlipped] = React.useState(false);

        const onChangeAmount = (event) => {
          setAmount(event.target.value);
        }
        const reset = () => {
          setAmount(0);
        }
        const flip = () => {
          reset();
          setFlipped((current) => !current);
        }
        return (
        <div>
          <h1>Super Converter</h1>
          <div>
            <label htmlFor="minutes">Minutes</label>
            <input placeholder="Minutes" type="number" id="minutes" min="0" value={flipped ? amount * 60 : amount} onChange={onChangeAmount} disabled={flipped}/>
          </div>
          <div>
            <label htmlFor="hours">Hours</label>
            <input placeholder="Hours" type="number" id="hours" value={flipped ? amount : Math.round((amount / 60) * 1000) / 1000} onChange={onChangeAmount} disabled={!flipped} />
          </div>
          <button onClick={reset}>Reset</button>
          <button onClick={flip}>{flipped ? 'Hours to Minutes' : 'Minutes to Hours'}</button>
        </div>
      )};

      const root = document.getElementById('root');
      ReactDOM.render(<App />, root);
    </script>
    ```

  - ```jsx
    <script type="text/babel">
      const MinutesToHours = () => {
        const [amount, setAmount] = React.useState(0);
        const [flipped, setFlipped] = React.useState(false);

        const onChangeAmount = (event) => {
          setAmount(event.target.value);
        }
        const reset = () => {
          setAmount(0);
        }
        const flip = () => {
          reset();
          setFlipped((current) => !current);
        }
        return (
        <div>
          <div>
            <label htmlFor="minutes">Minutes</label>
            <input placeholder="Minutes" type="number" id="minutes" min="0" value={flipped ? amount * 60 : amount} onChange={onChangeAmount} disabled={flipped}/>
          </div>
          <div>
            <label htmlFor="hours">Hours</label>
            <input placeholder="Hours" type="number" id="hours" value={flipped ? amount : Math.round((amount / 60) * 1000) / 1000} onChange={onChangeAmount} disabled={!flipped} />
          </div>
          <button onClick={reset}>Reset</button>
          <button onClick={flip}>Flip ({flipped ? 'Minutes to Hours' : 'Hours to Minutes'})</button>
        </div>
        )
      };
      const KmToMiles = () => {
        const [amount, setAmount] = React.useState(0);
        const [flipped, setFlipped] = React.useState(false);

        const onChangeAmount = (event) => {
          setAmount(event.target.value);
        }
        const reset = () => {
          setAmount(0);
        }
        const flip = () => {
          reset();
          setFlipped((current) => !current);
        }
        return (
        <div>
          <div>
            <label htmlFor="km">Km</label>
            <input placeholder="km" type="number" id="km" min="0" value={flipped ? amount * 1.609 : amount} onChange={onChangeAmount} disabled={flipped}/>
          </div>
          <div>
            <label htmlFor="miles">Miles</label>
            <input placeholder="miles" type="number" id="miles" value={flipped ? amount : Math.round((amount / 1.609) * 1000) / 1000} onChange={onChangeAmount} disabled={!flipped} />
          </div>
          <button onClick={reset}>Reset</button>
          <button onClick={flip}>Flip ({flipped ? 'Km to Miles' : 'Miles to Km'})</button>
        </div>
        )
      };
      const App = () => {
        const [selected, setSelected] = React.useState('');
        const onSelect = (event) => {
          setSelected(event.target.value);
        }
        return (
        <div>
          <h1>Super Converter</h1>
          <select onChange={onSelect}>
            <option value="">Choose...</option>
            <option value="0">Minutes to Hours</option>
            <option value="1">Km to Miles</option>
          </select>
          {selected === '' ? <div>Select one of the converter</div> : null}
          {selected === '0' ? <MinutesToHours /> : null}
          {selected === '1' ? <KmToMiles /> : null}
        </div>
      )};

      const root = document.getElementById('root');
      ReactDOM.render(<App />, root);
    </script>
    ```

## Prop

- send data from a parent component to a child component

- ```jsx
  <script type="text/babel">
    // props.text, props.changeValue
    const Btn =  ({text, changeValue}) => {
      console.log(`${text} was rendered`);
      return (
        <button
          onClick={changeValue}
          style={{
            backgroundColor: 'tomato',
            color: 'white',
            padding: '10px 20px',
            border: 0,
            borderRadius: 10,
          }}
        >
          {text}
        </button>
      );
    }
    // re-rendering only new components
    const MemorizedBtn = React.memo(Btn);
    const App = () => {
      const [value, setValue] = React.useState('Save Changes');
      const changeValue = () => setValue('Revert Changes');
      return (
      <div>
        <MemorizedBtn text={value} changeValue={changeValue}/>
        <MemorizedBtn text="Continue" />
      </div>
    )};

    const root = document.getElementById('root');
    ReactDOM.render(<App />, root);
  </script>
  ```

## Prop Types

- check what types the props receive

- ```jsx
  <script type="text/babel">
    const Btn = ({text, fontSize = 16}) => {
      return (
        <button
          style={{
            ...
            fontSize,
          }}
        >
          {text}
        </button>
      );
    }
    // check the right type and the existence
    Btn.propTypes = {
      text: PropTypes.string.isRequired,
      fontSize: PropTypes.number
    }
    const App = () => {
      return (
      <div>
        <Btn text="Save Changes" fontSize={18} />
        <Btn text={"Continue"} />
      </div>
    )};

    const root = document.getElementById('root');
    ReactDOM.render(<App />, root);
  </script>
  ```

## Frameworks

### Gatsby

- We pre-generate our pages before we publish our website.

- for interactive, static, pre-generated websites like landing pages or blogs

- Need to learn a little bit of GraphQL in the process

### Remix

- We run the code in the server side on demand when the user wants it.

- Remix needs a server because Remix runs in server and in the browser.

- Remix is going to render a page on the server first. Remix is going to run React.js on the backend and Remix is going to take the output and give that to the user. So, users aren't going to see loading indicators anywhere. When they get the page, it will be 100% fully rendered.

### Next.js

- It allows you to pre-generate pages in your website. It also allows you to choose if you want to render your pages in the server side.
