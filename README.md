# POPUP 띄우고 없애기

## html 코드

```html
    <div class="wrap">
        <a class="thisBtn" href="#">click</a>
        <div class="showBox">
            <a class="sns" href="http://naver.com" target="_blank">facebook</a>
            <a class="sns" href="http://naver.com" target="_blank">instagram</a>
            <a class="sns" href="http://naver.com" target="_blank">blog</a>
        </div>
    </div>
```
먼저 `div class = "wrap"` 로 감싸줬습니다. <br>
그리고 팝업을 띄워 줄 버튼을 `a class = "thisBtn"` a 태그를 사용하여 만들었고, <br> 팝업레이어를 `div class = "showBox"` 로 만들었습니다.  
그리고 그 안에는 a 태그를 사용하여 클릭하면 테스트로 네이버를 띄우게 만들었습니다.

## css 코드

```css
        .wrap{position: relative;}
        .thisBtn{position: absolute; right: 10px; top: 10px; padding: 0.5em 3em; background-color: royalblue; color: #fff; border-radius: 20px;}
        .showBox{position: absolute; right: 0; top: 50px; box-shadow: 0 3px 15px rgba(0, 0, 0, 0.3); padding: 2em; display: none; animation: on 0.3s ease-in-out;
        }
        
        @keyframes on {
                from {opacity: 0;}
                to {opacity: 1;}
            }
        .showBox.on{display: flex; flex-direction: column;}
        .showBox a{display:inline-block; padding: 0.5em 3em; background-color: salmon; color: #fff; border-radius: 20px; margin-bottom: 3%; text-align: center;}
```
css는 일단 버튼을 눈에 뜨게 만들기 위해서 `background-color` 를 사용하였고,  
팝업레이어 또한 `box-shadow` 를 적용하여 배경과 분간이 되도록 만들었습니다.  
그리고 그 안에 있는 `a class = "sns"` 태그는 `background-color: salmon` 을 사용하여 눈에 잘 띄도록 만들었습니다.  
위치는 `position: absolute` 로 잡은 뒤 `showBox` 를 `display: none` 해주었습니다.  
이제 js 를 통해서 팝업레이어를 띄워보겠습니다.
## js 코드

```js
    <script>
        const thisBtn = document.querySelector('.thisBtn');
        const showBox = document.querySelector('.showBox');
        const sns = document.querySelectorAll('.sns');
        
        document.addEventListener('click', function(e) {
            // e.preventDefault();
            if(e.target.classList.contains("thisBtn")) {
                showBox.classList.toggle("on");
            } else if(e.target.classList.contains("showBox") || e.target.classList.contains("sns")) {
                return 
            } else {
                if(showBox.classList.contains("on")) {
                    showBox.classList.remove("on");
                }
            }
        })
    </script>
```

```js 
const thisBtn = document.querySelector('.thisBtn');
        const showBox = document.querySelector('.showBox');
```
먼저 `const` 변수로 위의 태그들을 가져왔습니다.  
```js 
document.addEventListener('click', function(e) {
            // e.preventDefault();
            if(e.target.classList.contains("thisBtn")) {
                showBox.classList.toggle("on");
            } else if(e.target.classList.contains("showBox") || e.target.classList.contains("sns")) {
                return 
            } else {
                if(showBox.classList.contains("on")) {
                    showBox.classList.remove("on");
                }
            }
        })
```
그리고 `document.addEventListener` 클릭 이벤트를 통해서 실행이 되도록 만들었습니다.  
먼저 클릭을 했을 때 `if`를 사용하여 클릭 된 타깃의 `classList.contains` 를 활용하여 각각의 태그들을 