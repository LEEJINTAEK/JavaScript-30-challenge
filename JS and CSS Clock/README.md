# Web Clock

<img src="./clock.PNG" width="450px" height="330px">

## 소개

<br />

**현재 시간을 보여주는 Web Clock**

[구경하러 바로 가기](https://darling-pothos-057761.netlify.app/)

<br />

## CSS & JavaScript Code

<br />

```css
/*css*/
transform-origin: 100%;
transform: rotate(90deg);
transition: all 0, 05s;
transition-timing-function: cubic-bezier(0.1, 2.7, 0.58, 1);
```

```js

<script>
//js
const secondHand = document.querySelector('.second-hand');
const minHand = document.querySelector('.min-hand');
const hourHand = document.querySelector('.hour-hand');

function setDate(){
    const now = new Date();

    const second = now.getSeconds();
    const secondsDegrees = ((second / 60) * 360) + 90;
    secondHand.style.transform = `rotate(${secondsDegrees}deg)`;

    const min = now.getMinutes();
    const minsDegrees = ((min / 60) * 360) + 90;
    minHand.style.transform = `rotate(${minsDegrees}deg)`;

    const hour = now.getHours();
    const hoursDegrees = ((hour / 12) * 360) + 90;
    hourHand.style.transform = `rotate(${hoursDegrees}deg)`;
}

setInterval(setDate,1000); //1초마다 함수 실행

</script>
```
