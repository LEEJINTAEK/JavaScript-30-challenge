# Mouse Move Shadow

<img src="./shadow.PNG" width="450px" height="330px">
<br />

## 소개

<br />

**마우스 움직임에 따라 Shadow Effect**

[구경하러 바로 가기](https://magenta-sunshine-21ffd6.netlify.app/)

<br />

## JavaScript Code

<br />

```js
<script>

const hero = document.querySelector('.hero');
const text = hero.querySelector('h1');

let walk = 100;

function shadow(e){
  //  const width = hero.offsetWidth;
  //  const height = hero.offsetHeight;
   const { offsetWidth: width, offsetHeight: height } = hero;
   let { offsetX: x, offsetY: y } = e;
  //  console.log(this, e.target);
  //원래 x,y가 h1쪽에서 0,0이였다. 늘려줘야함
  if(this !== e.target){
    x = x + e.target.offsetLeft;
    y = y + e.target.offsetTop;
  }
  // console.log(x,y);
  //기존 0,0 => -50,-50
  const xWalk = Math.round((x / width * walk) - (walk / 2));
  const yWalk = Math.round((y / width * walk) - (walk / 2));
  // console.log(xWalk,yWalk)
  //거리 넓히기
  walk += 1;
  if(walk >= 800) { walk =100; }
/* offset-x | offset-y | blur-radius | color */
      text.style.textShadow = `
      ${xWalk}px ${yWalk}px 0 rgba(255,0,255,0.7),
      ${xWalk * -1}px ${yWalk}px 0 rgba(0,255,255,0.7),
      ${yWalk}px ${xWalk * -1}px 0 rgba(0,255,0,0.7),
      ${yWalk * -1}px ${xWalk}px 0 rgba(0,0,255,0.7)`;

}

hero.addEventListener('mousemove',shadow);

</script>
```
