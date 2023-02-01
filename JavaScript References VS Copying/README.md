# JS References VS Copying

<br />

## 소개

<br />

**Array, Object의 참조, 복사에 방법에 대한 공부**

<br />

## Deep Copy 방법?!

`얕은 복사와 깊은 복사 차이는 Study_Note 참조`
<br />

1. **Array**

```js
//1차원 값 복사
const players = ["Wes", "Sarah", "Ryan", "Poppy"];
//방법 1
const team2 = players.slice();
//방법 2
const team3 = [].concat(players);
//방법 3
const team4 = [...players];
//방법 4
const team5 = Array.from(players);
```

<br />

2. **Object**

```js
const person = {
  name: "Wes Bos",
  age: 80,
};

//방법 1
const captain2 = Object.assign({}, person, { number: 99, age: 12 });

const wes = {
  name: "Wes",
  age: 100,
  social: {
    twitter: "@wesbos",
    facebook: "wesbos.developer",
  },
};
console.log(wes);
//위 방법과 동일 (1차원 값 복사)
const dev = Object.assign({}, wes);

//방법 2
//2차원 값 복사(lodash Clonedeep 이용할 것)
const dev2 = JSON.parse(JSON.stringify(wes));
```

<br />

## JavaScript Code

<br />

```js

<script>
    //밑에 모두 1차원 값들만 복사

    // start with strings, numbers and booleans
    let age = 20;
    let age2 = age;
    console.log(age, age2) //20 20
    age = 100;
    console.log(age, age2) //100 20

    // Let's say we have an array
    const players = ['Wes', 'Sarah', 'Ryan', 'Poppy'];

    // and we want to make a copy of it.
    const team = players;
    console.log(team, players); //['Wes', 'Sarah', 'Ryan', 'Poppy']  ['Wes', 'Sarah', 'Ryan', 'Poppy']

    // You might think we can just do something like this:
    // team[3] = 'jin';
    // console.log(team); // ['Wes', 'Sarah', 'Ryan', 'jin']
    // console.log(players); // ['Wes', 'Sarah', 'Ryan', 'jin']
    //복사후 사용할것

    // however what happens when we update that array?
    // now here is the problem!
    // oh no - we have edited the original array too!
    // Why? It's because that is an array reference, not an array copy. They both point to the same array!
    // So, how do we fix this? We take a copy instead!
    const team2 = players.slice();
    console.log(team2); //['Wes', 'Sarah', 'Ryan', 'Poppy']

    // one way
    // or create a new array and concat the old one in
    const team3 = [].concat(players);
    console.log(team3); //['Wes', 'Sarah', 'Ryan', 'Poppy']
    // or use the new ES6 Spread
    const team4 = [...players];
    team4[3] = 'omg';
    console.log(team4); //['Wes', 'Sarah', 'Ryan', 'omg']

    const team5 = Array.from(players);
    team5[3] = 'god';
    console.log(team5); //['Wes', 'Sarah', 'Ryan', 'god']

    // now when we update it, the original one isn't changed

    // The same thing goes for objects, let's say we have a person object

    // with Objects
    const person = {
      name: 'Wes Bos',
      age: 80
    };

    // and think we make a copy:
    // const captain = person;
    // captain.number = 99;
    // console.log(captain);

    // how do we take a copy instead?
    const captain2 = Object.assign({}, person, {number:99,age:12});
    console.log(captain2); //age: 12, name: "Wes Bos", number: 99

    // We will hopefully soon see the object ...spread
    const cap3 = {...person}
    console.log(cap3);

    // Things to note - this is only 1 level deep - both for Arrays and Objects. lodash has a cloneDeep method, but you should think twice before using it.
    const wes = {
      name: 'Wes',
      age: 100,
      social: {
        twitter: '@wesbos',
        facebook: 'wesbos.developer'
      }
    }
    console.log(wes);

    const dev = Object.assign({},wes);

    //2차원 값 복사(lodash Clonedeep 이용할 것)
    const dev2 = JSON.parse(JSON.stringify(wes));

    console.log(dev);
    console.log(dev2);
  </script>

```

<br />
