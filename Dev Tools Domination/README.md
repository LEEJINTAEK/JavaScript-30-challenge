# Console Study

## 소개

<br />

**JS Console 에 대해 학습**

<br />

## JavaScript Code

<br />

```js
  <script>

    // Regular
    console.log('hello');

    // Interpolated
    console.log('Hello i`m a %s string', '💩');

    // Styled
    console.log('%c I am some great text','font-size:50px; background:red; text-shadow:10px 10px 0 blue');

    // warning!
    console.warn('Oh NOOOO');

    // Error :|
    console.error('SShit');

    // Info
    console.info('practice');

    // Testing
    const p = document.querySelector('p');
    console.assert(p.classList.contains('ouch'), 'That is wrong');
    // console.assert(1===1, 'good'); // Nope, This is true

    // clearing
    // console.clear();

    // Viewing DOM Elements
    console.log(p);
    console.dir(p);

    // Grouping together
    const dogs = [{ name: 'Snickers', age: 2 }, { name: 'hugo', age: 8 }];

    dogs.forEach(dog=> {
      console.group(`${dog.name}`);
      console.log(`this is ${dog.name}`);
      console.log(`${dog.name} is ${dog.age} years old`);
      console.log(`${dog.name} is ${dog.age*7} years old`);
      console.groupEnd(`${dog.name}`);
    });

    // counting
    console.count('Wes');
    console.count('Wes');
    console.count('Steve');
    console.count('Wes');
    console.count('Steve');

    // timing
    console.time('fetching data');
    fetch('https://api.github.com/users/wesbos')
      .then(data => data.json())
      .then(data => {
        console.timeEnd('fetching data');
        console.log(data);
      });

     //table
     console.table(dogs);

  </script>
```
