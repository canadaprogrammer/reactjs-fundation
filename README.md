# React Fundamental

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

- using JSX

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

- state

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
