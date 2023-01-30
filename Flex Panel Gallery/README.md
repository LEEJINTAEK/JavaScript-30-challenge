# Flex Panel Gallery

<img src="./gallery.PNG" width="500px" height="330px">

## 소개

<br />

**클릭으로 변환 되는 동적 웹 페이지**

[구경하러 바로 가기](https://benevolent-llama-5a7c93.netlify.app/)

<br />

## Study Question

<br />

### CSS

<br />

- **자식 요소 세로축 기준으로 배치 방법**

1. **align-items**

부모 => 컨테이너 -> `display: flex;`
<br />
<img width="574" alt="question1" src="https://user-images.githubusercontent.com/109197023/214037456-d02a189e-6938-40db-b21e-1fd5d39ff662.PNG">
<br />

> 자식 요소가 여러개가 들어가는 순간, 또한 자식 요소의 크기가 어떻느냐에 따라서 items 보다는 content를 사용하는것이 훨씬 편리

<br />

2. **align-content**
   <br />
   1. flex-wrap이 wrap으로 설정되어 있어야 한다.
   1. 한 줄이 아닌 여러 줄일 때 의미가 있다.
   1. justify-content 와 기준 축만 다르다.

<br />
<br />

- **자식 요소 가로축 기준으로 배치 방법**

1. **justify-content**
   <br />
   <img width="566" alt="question2" src="https://user-images.githubusercontent.com/109197023/214039519-aa2a36eb-1de8-4d00-a53b-ca4dabfab90f.PNG">
   <br />
   - flex-wrap이 wrap으로 설정되어 있어야 한다.

<br />
<br />

- **flex-wrap??**
  <br />

1. **flex-wrap: nowrap;**

   - flex는 부모 요소인 컨테이너 스타일 속성 즉, 컨테이너가 블록 속성을 가지게 된다.
   - 이 옵션은 flex 속성의 기본값
   - 부모인 컨테이너 요소에 display: flex 또는 inline-flex가 사용되었다면 자동으로 flex-wrap: nowrap; 이 적용된 상태

1. **자식 요소의 flex 0과 1 차이**

   - 이 옵션은 부모 요소의 전체 영역을 랩으로 감싼다는 개념
   - 따라서 컨테이너 전체를 인식하게 되므로 자식 요소의 가로 사이즈가 완벽하게 유동적으로 움직인다
   - 세부적인 옵션을 통해 자식 요소의 가로 크기를 어떻게 마크업 했느냐에 따라 다이나믹하게 배치 가능
     <br />

   예시

   - **flex: 0 300px; 의 뜻**은 width: 300px;과 같다. 또한 부모 요소가 flex 속성인 상태에서의 자식 요소 width는 완전 고정이 아닌 max-width 상태처럼 적용된다. 그렇기에 최대 300px 까지 늘어나고 브라우저의 가로 사이즈를 줄이면 자식 요소도 덩달아 가로 사이즈가 알아서 줄어든다
   - **flex: 1 300px; 의 뜻**은 각 자식 요소의 가로 사이즈가 브라우저의 가로 사이즈에 맞게 각각 100% 풀사이즈로 적용된다.
   - 즉 0일 땐 최대 사이즈를 고려하고, 1일 땐 부모 사이즈에 따라 가는 것이다.

<br />

## CSS & JavaScript Code

<br />

```css
/*study css*/
.panel {
  background: #6b0f9c;
  box-shadow: inset 0 0 0 5px rgba(255, 255, 255, 0.1);
  color: white;
  text-align: center;
  align-items: center;

  transition: font-size 0.7s cubic-bezier(0.61, -0.19, 0.7, -0.11), flex 0.7s
      cubic-bezier(0.61, -0.19, 0.7, -0.11), background 0.2s;
  font-size: 20px;
  background-size: cover;
  background-position: center;
  flex: 1; /*기본 크기*/
  justify-content: center;
  align-items: center;
  display: flex;
  flex-direction: column;
}

.panel > * {
  margin: 0;
  width: 100%;
  transition: transform 0.5s;
  flex: 1 0 auto; /*기본 크기*/
  display: flex;
  justify-content: center;
  align-items: center;
}

.panel > *:first-child {
  transform: translateY(-100%);
}
.panel.open-active > *:first-child {
  transform: translateY(0);
}
.panel > *:last-child {
  transform: translateY(100%);
}
.panel.open-active > *:last-child {
  transform: translateY(0);
}

.panel.open {
  flex: 5; /*기본 item 크기 보다 크게*/
  font-size: 40px;
}
```

```js

<script>
//js
   const panels = document.querySelectorAll('.panel');

    function toggleOpen() {
      this.classList.toggle('open'); // if visible is set remove it, otherwise add it
    }
    function toggleActive(e){
      // console.log(e.propertyName); //콘솔로 property이름 확인해보기
      if(e.propertyName.includes('flex')){    // Safari transitionend event.propertyName === flex
        this.classList.toggle('open-active'); // Chrome + FF transitionend event.propertyName === flex-grow
      }
    }
    panels.forEach(panel => panel.addEventListener('click',toggleOpen)); //클릭시 함수 실행
    panels.forEach(panel => panel.addEventListener('transitionend',toggleActive)); //css 변환 때마다 함수 실행

</script>
```

<br />

## 출처

> https://flexboxfroggy.com/#ko 👈 게임으로 CSS 연습하기

> https://rgy0409.tistory.com/4814
