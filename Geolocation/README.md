# Geolocation

## 소개

<br />

**SPEED METAR 기록**

<br />

## JavaScript Code

<br />

```js
  <script>
    const arrow = document.querySelector('.arrow');
    const speed = document.querySelector('.speed-value');

    navigator.geolocation.watchPosition((data)=>{
      console.log(data);
      speed.textContent = data.coords.speed;
      arrow.style.transform = `rotate(${data.coords.heading}deg)`;
    },(err)=>{
      console.log(err);
      alert('Hey!');
    })
  </script>
```
