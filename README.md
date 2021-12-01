# React Practice

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

## State Hook

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
        ...
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
        ...
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
