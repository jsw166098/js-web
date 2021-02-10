# Object Model
자바스크립트로 웹브라우저를 제어할 때 객체를 대상으로 제어를 하게 된다. 브라우저는 브라우저의 여러 구성요소들을 자바스크립트로 제어할 수 있도록 객체로 만들어서 제공한다. 브라우저는 웹 페이지를 읽을 때 각각의 태그를 객체화 시켜 놓는다. 자바스크립트는 각 태그를 객체화 시킨 객체를 제어하는 것이다. 특정 객체를 제어하게 되면 해당 태그가 제어되는 것이다. 

## 객체 제어 
~~~
<html>
    <head></head>
        <body>
            <img src="~~~~">

        </body>
</html>
~~~

img 태그를 제어할 때  브라우저는 해당 태그의 객체를 찾아내야 한다. 브라우저는 document라는 객체를 미리 만들어 놨으며 해당 메서드인 getElementsByTagName()이 존재한다. 
~~~
// 태그의 이름을 가진 요소를 가져온다. -> 태그가 여러개 이다. 배열을 사용한다. 
var imgs = document.getElementsByTagName('img')
imgs[0]  //여러개의 요소를 가져오기 때문에 배열 안에 들어있다. 이는 이미지 태그에 해당하는 객체인 것이다. 
imgs[0].style.width='300px';
~~~

화면에 이미 출력된 웹페이지를 html으로 변경할 수 없다. 이미 렌더링이 끝난 웹 페이지를 동적으로 수정하기 위해서는 웹 브라우저가 만들어 놓은 객체를 대상으로 자바스크립트를 활용해 변경해야 한다. 태그를 의미하는 객체를 찾아내어야 한다. 

---

## 객체 모델(Object Model)

브라우저는 다음과 같은 객체 모델을 가지고 있다.

![img3](./img/img3.png)

출처: <https://learn.javascript.ru/browser-environment>

### window 객체
* 전역 객체 -> 생략해도 된다. -> 생략시 window 객체의 속성 내의 객체라는 의미이다. 
* window, frame 제어하기 위한 객체
* 다음과 같은 3가지 주요 property를 객체 형태로 가지고 있다.
~~~
JavaScript Core(JSC)
DOM(Document Object Model)
BOM(Browser Object Model)
~~~

### DOM 객체

* 웹 페이지의 문서와 관련된 태그를 제어한다.
* body, img 등의 태그를 제어한다. 
* document 객체가 가지고 있는 모들은 document object model 이다. 
* window의 객체에 속성으로 저장되어 있는 객체이다. 접근 방법은 다음과 같다. 
~~~
window.document
~~~

### BOM 객체
* browser object model
* 현재 웹 브라우저가 가리키고 있는 url 알아낼 때 
* 현재 웹 바르우저가 표시하고 있는 페이지를 reload 할 때 
* 경고창을 띄울때 
* window 객체의 property 로 저장되어 있다. 

### JSC 객체
* 자바스크립트 자체적으로 가지고 있는 객체들... 어떤 호스트 환경에서도 사용할 수 있다. (BW, GAS, node.js)

