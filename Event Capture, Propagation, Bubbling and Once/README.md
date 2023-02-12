# Event Capture, Bubbling

<img src="./캡쳐링.PNG" width="500px" height="330px">

## 소개

<br />

**버블링 캡처링 Study**

<br />

## Study

<br />

**1. 버블링**

- 한 요소에 이벤트가 발생하면, 이 요소에 할당된 핸들러가 동작하고, 이어서 부모 요소의 핸들러가 동작
- 가장 최상단의 조상 요소를 만날 때까지 이 과정이 반복되면서 요소 각각에 할당된 핸들러가 동작

```html
<div class="one">
  <div class="two">
    <div class="three"></div>
  </div>
</div>
```

<br />

<img width="503" alt="캡처" src="https://user-images.githubusercontent.com/109197023/218294037-80aa25e6-7392-4cb1-b804-d4dae9766dc7.PNG">

<br />

☝️ 위에 처럼 겹치는 부분 최하단(주황) 눌렀을 때 value값 three two one 값이 나온다.

<br />

**거의** 모든 이벤트(focus와 같은 이벤트들 제외) 는 버블링 되는데, 이를 중단하기 위해서는 <br />
`'stopPropagation() //캡처링 버블링 단계에서 더이상 전파 X'` 이를 사용한다.

<br />

코드 예제

```js
function logText(e) {
  e.stopPropagation();
}
```

<br />

`stopPropagation`

<img width="372" alt="ad" src="https://user-images.githubusercontent.com/109197023/218294971-c2954201-0c69-4912-a9f7-e50647dc9ae3.PNG">

<br />

### 정리

<br />

'Event Bubbling'

- 즉, 맨 아래에 three, 그 위에 two, 그 위에 one 클래스를 가진 div가 차례차례로 쌓여있고 <br />
  특정 div에서 발생한 이벤트가 물방울처럼 위로 타고 올라가면서 전달된다고 생각하면 된다.
- div끼리만 일어나는 게 아니고, 문서의 최상층까지 계속해서 타고 올라간다.
- 하지만 여기서는 세 개의 div들에만 이벤트 리스너를 달아놨기 때문에 그 위에 위치한 요소들까지 전달된 이벤트는 감지되지 않는다.

<br />

'stopPropagation'

- Stop bubbling'과 동일한 의미라고 생각하면 된다.
- 이벤트가 차례차례 위로 올라가면서 부모에까지 이벤트 발생시키는 것을 멈춘다.
- 정확하게 이벤트가 처음 발생한 그 자리에서만 이벤트가 발생하도록 한다.

<br />
<br />

**2. 캡처링**

<br />

**표준 DOM 이벤트에서 정의한 이벤트 흐름엔 3가지 단계 존재**

1. 캡처링 단계 – 이벤트가 하위 요소로 전파되는 단계
2. 타깃 단계 – 이벤트가 실제 타깃 요소에 전달되는 단계
3. 버블링 단계 – 이벤트가 상위 요소로 전파되는 단계

<br />

캡처링은 버블링 반대라고 생각하면 된다.(거의 사용 X)

<br />

<img width="602" alt="버블캡처" src="https://user-images.githubusercontent.com/109197023/218294341-b6ec69ca-1a1f-4c7a-9c29-1226d3ee6367.PNG">

- td 클릭하면 이벤트가 최상위 조상에서 시작해 아래로 전파되고(캡처링 단계), 이벤트가 타깃 요소에 도착해 실행된 후(타깃 단계), 다시 위로 전파(버블링 단계). 이런 과정을 통해 요소에 할당된 이벤트 핸들러가 호출.

<br />

```js
divs.forEach((div) =>
  div.addEventListener("click", logText, {
    capture: true,
    //false이면(default 값) 핸들러는 버블링 단계에서 동작
    //true이면 핸들러는 캡처링 단계에서 동작
  })
);
```

<br />

<img width="577" height="250" alt="ddf" src="https://user-images.githubusercontent.com/109197023/218294493-ac4565bf-5631-4b5b-b59c-022a43714de9.PNG">

<br />

☝️ 버블링과 다르게 console에 뜨는 것을 확인할 수 있다.

<br />

### 정리

<br />

'Event Capture'

- 즉, 맨 처음에 three를 클릭하면, 우선 클릭을 감지(capture) 해야한다.
- 이 때, 맨 위(one)에서부터 아래(three)로 내려가면서 차례차례 클릭을 captrue한다. (one => two => three 순으로)
- 아직 이벤트는 발생하지 않았고, 클릭을 감지하기만 한 상태이다.
- 각 div는 클릭이 발생했다는 정보를 저장해놓는다.
- 반대로 맨 아래에서부터 차례차례 올라가면서 이벤트를 발생시킨다.
- three => two => one 순으로 올라가면서 이벤트를 발생시킨다.

<br />

<img width="358" alt="a" src="https://user-images.githubusercontent.com/109197023/218295254-a4a75328-12c3-4e36-af36-2e6bbc7c966b.PNG">

<br />

'stopPropagation'

- 어느 곳을 클릭해도 'one'이 나온다
- 이벤트가 위에서부터 발생해서 아래로 전달되는데, 이벤트 전달을 하지 말라고 했기 때문에 <br />
  가장 위에 있는 div에서만 이벤트가 발생하고 이후에는 이벤트가 전달되지 않는다.

<br />
<br />

**3. once 옵션**

<br />

```js
divs.forEach((div) =>
  div.addEventListener("click", logText, {
    capture: false,
    once: true,
  })
);
```

- 이벤트 리스너에 달아놓으면, 그 이벤트 리스너는 단 한 번만 이벤트를 감지하고, 자기를 스스로 unbind해버린다.
- 즉, 이벤트 리스너가 한 번만 동작하고 removeEventListener를 하는 것과 동일한 효과이다.

<br />
<br />

## JavaScript Code

<br />

```js

<script>

  const divs = document.querySelectorAll('div');
  const button = document.querySelector('button');

  function logText(e) {
    console.log(this.classList.value);
    // e.stopPropagation(); //캡처링 버블링 단계에서 더이상 전파 X (once사용)
  }

  divs.forEach(div => div.addEventListener('click',logText, {
    capture: false, //three two one ...   true-> one two three.. first num is one (캡쳐링 사용 X 버블링 단계에서 동작)
    once: true //값당 한번씩
  }));

  button.addEventListener('click',()=> {
    console.log('click!');
  }, {
    once: true //한번
  });

</script>
```

<br />
<br />

## 출처

> https://ko.javascript.info/bubbling-and-capturing

> https://iborymagic.tistory.com/50
