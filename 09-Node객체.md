# Node 객체
* DOM의 가장 최상위 객체이다. 모든 DOM의 객체는 Node 객체를 상속받는다. Node의 모든 프로퍼티를 상속받는다. 

![img32](./img/img32.png)
출처: [생활코딩](https://opentutorials.org/course/1375/6698)

## 노드의 관계
각각의 노드 객체에 관계성을 부여하는 api이며 각각의 노드들이 어떤 관계(상속)인지 알아내는 기능을 한다.
* Node.childNodes : 노드 객체의 자식 노드들
* Node.firstChild : 노드 객체의 첫번째 자식 노드
* Node.lastChild : 두번째 자식 노드
* Node.nextSibliing: 같은 상속 레벨에서 다음 노드 객체, 다음 형제
* Node.previousSibling: 같은 상속 레벨에서 이전 노드 객체, 이전 형제 
* Node.contains() 
* Node.hasChildNodes()

## 노드의 종류
* Node.nodeType : 노드 객체가 어떤 카테고리에 속해 있는지
* Node.nodeName : 노드 객체의 이름이 뭔지

## 노드의 값
* Node.nodevalue: 노드 객체가 가지고 있는 값
* Node.textContent: 노드 객체가 가지고 있는 하위 텍스트 값

## 노드의 자식 관리
* Node.appendChild() : 노드 객체를 자식으로 추가
* Node.removeChild() : 노드 객체의 자식을 삭제

---

# Node 관계 API

* Node.childNodes : 자식노드들을 유사배열에 담아서 리턴
* Node.firstChild : 첫번째 자식노드
* Node.lastChild : 두번째 자식노드
* Node.nextSibling : 다음 형제 노드
* Node.preivousSibling : 이전 형제 노드
~~~
<body id="start">
<ul>
    <li><a href="./532">html</a></li> 
    <li><a href="./533">css</a></li>
    <li><a href="./534">JavaScript</a>
        <ul>
            <li><a href="./535">JavaScript Core</a></li>
            <li><a href="./536">DOM</a></li>
            <li><a href="./537">BOM</a></li>
        </ul>
    </li>
</ul>
<script>
var s = document.getElementById('start');
console.log(1, s.firstChild); // #text -> [공백, 줄바꿈]을 가지고 있는 객체

var ul = s.firstChild.nextSibling

console.log(2, ul); // ul

console.log(3, ul.nextSibling); // #text
console.log(4, ul.nextSibling.nextSibling); // script
console.log(5, ul.childNodes); //text, li, text, li, text, li, text
console.log(6, ul.childNodes[1]); // li(html)
console.log(7, ul.parentNode); // body
</script>
</body>
~~~

* element 들의 사이에 존재하는 Node 객체이다. 
~~~
#text
~~~

![img33](./img/img33.png)

---

# Node 종류 API
현재 선택된 노드가 어떤 타입인지 확인한다. 비교 연산자 사용할 수도 있다.
* Node.nodeType: 노드의 타입을 의미한다.
* Node.nodeName: 노드의 이름(태그명)을 의미한다. 

* 노드의 프로퍼티 출력 -> 상수 형태
~~~
for(var name in Node){
   console.log(name, Node[name]);
}
~~~

* 타입 확인
~~~
var body = document.getElementById('start');

body.nodeType  // 1 -> ELEMENT_NODE

body.firstChild.nodeType // 3 -> TEXT_NODE

document.nodeType  // 9 -> DOCUMENT_NODE
~~~

* 타입 체크
~~~
body.firstChild.nodeType === 3  //true
body.firstChild.nodeType === Node.TEXT_NODE  //true
~~~

* 노드 이름
~~~
body.firstChild.nextSibling.nodeName
~~~

[img34](./img/img34.png)

[img35](./img/img35.png)

## 재귀함수 1
* 특정 element 부터 하위 element들을 찾는 메서드 작성

### travers 함수
* 첫번째 인자: 조회하려는 가장 최상위 root element
* 두번째 인자: 현재 탐색하고 있는 element를 첫번째 인자로 가진 함수
~~~
traverse(document.getElementById('start'), function(elemn){

})

//body 부터 시작해서 element 하나하나를 접근한다.
traverse(document.getElementById('start'), function(elemn){
    console.log(elem);
})

// a 태그만 조회
traverse(document.getElementById('start'), function(elemn){
    if(elem.nodeName === 'A'){
        elem.style.backgroundColor = 'blue';    
    }
})
~~~

#### 파라미터를 함수형태로 작성한다.
* 선언된 함수를 사용할 때 매개변수 작성부에 함수 내용을 정의한다. 
~~~
function traverse(target, callback){
    callback(target);
}

traverse(document.getElementById('start'), function(elem)){
    console.log(elem);
}
~~~

#### 하위 태그로 이동할때는 재귀법이 사용된다.
* 자식노드를 조회한 후 모든 자식 노드를 함수 처리한다.  
~~~
function traverse(target, callback){
    callback(target);
    var c = target.childNodes;
    for(var i=0; i<c.length; i++){
        traverse(c[i], callback);
    }
}

traverse(document.getElementById('start'), function(elem)){
    console.log(elem);
}
~~~

~~~
<!DOCTYPE html>
<html>
<body id="start">
<ul>
    <li><a href="./532">html</a></li> 
    <li><a href="./533">css</a></li>
    <li><a href="./534">JavaScript</a>
        <ul>
            <li><a href="./535">JavaScript Core</a></li>
            <li><a href="./536">DOM</a></li>
            <li><a href="./537">BOM</a></li>
        </ul>
    </li>
</ul>
<script>
function traverse(target, callback){
    if(target.nodeType === 1){
        //if(target.nodeName === 'A')
        callback(target);
        var c = target.childNodes;
        for(var i=0; i<c.length; i++){
            traverse(c[i], callback);       
        }   
    }
}
traverse(document.getElementById('start'), function(elem){
    console.log(elem);
});
</script>
</body>
</html>
~~~

---

# Node 변경 API

* 노드 추가
* 노드 제거
* 노드 변경

## Node 추가
* appendChild(child): 매개변수로 주어진 엘리먼트를 노드의 마지막 자식 노드로 추가한다. 
* insertBefore(newElement, referenceElement): 방법은 동일하며 두번째 인자를 통해 해당 노드 바로 뒤의 위치에 자식노드로 추가된다. 

### 노드 생성 api
노드를 추가하기 위해서는 추가할 element를 생성해야 하며 이것은 document 객체의 기능이다.
* document.createElement(tagname): element 노드를 추가하다.
* document.createTextNode(data): 텍스트 노드를 추가한다. 

~~~
<ul id="target">
    <li>HTML</li>
    <li>CSS</li>
</ul>
<input type="button" onclick="callAppendChild();" value="appendChild()" />
<input type="button" onclick="callInsertBefore();" value="insertBefore()" />
<script>
    function callAppendChild(){
        var target = document.getElementById('target');
        var li = document.createElement('li');  //li element 생성만 했다.
        var text = document.createTextNode('JavaScript');  //text element를 생성만 했다. 
        li.appendChild(text);
        target.appendChild(li);
    }
 
    function callInsertBefore(){
        var target = document.getElementById('target');
        var li = document.createElement('li');
        var text = document.createTextNode('jQuery');
        li.appendChild(text);
        target.insertBefore(li, target.firstChild);
    }
</script>
~~~

* target의 firstChild는 text이다.
![img36](./img/img36.png)

## Node 제거
* removeChild(child): 부모객체로 접근하여 해당 element를 제거해야한다. -> 부모 element 접근시 parentNode를 접근한다.
~~~
target.parentNode.removeChild(target);
~~~


## Node 변경
* replaceChild(newChild, oldChild)
~~~
<ul>
    <li>HTML</li>
    <li>CSS</li>
    <li id="target">JavaScript</li>
</ul>
<input type="button" onclick="callReplaceChild();" value="replaceChild()" />
<script>
    function callReplaceChild(){
        var a = document.createElement('a');
        a.setAttribute('href', 'http://opentutorials.org/module/904/6701');
        a.appendChild(document.createTextNode('Web browser JavaScript'));
 
        var target = document.getElementById('target');
        target.replaceChild(a,target.firstChild);
    }
</script>
~~~

---

# JQuery Node 변경 API

## 추가

![img37](./img/img37.png)

출처: [생활코딩](https://opentutorials.org/course/1375/6743)

* 지정된 대상의 모든 element에 적용된다. 
* `before`과 `after`은 target의 형제로 삽입된다.
* `prepend`와 `append`는 target의 자식으로 삽입된다.

~~~
//before
<div class="target">
//prepend
    content1
//append
</div>
//after

 //before
<div class="target">
//prepend
    content2
//append
</div>
//after 

<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
<script>
    $('.target').before('<div>before</div>');
    $('.target').after('<div>after</div>');
    $('.target').prepend('<div>prepend</div>');
    $('.target').append('<div>append</div>');
</script>
~~~

## 제거

* remove: 선택된 엘리먼트가 제거된다.
* empty : 선택된 엘리먼트의 text 엘리먼트가 제거된다.

~~~
<div class="target" id="target1">
    target 1
</div>
 
<div class="target" id="target2">
    target 2
</div>
 
<input type="button" value="remove target 1" id="btn1" />
<input type="button" value="empty target 2" id="btn2" />
<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
<script>
    $('#btn1').click(function(){
        $('#target1').remove();
    })
    $('#btn2').click(function(){
        $('#target2').empty();
    })
</script>
~~~

* id가 target1인 엘리먼트 자체는 삭제되어서 존재하지 않으며 id가 target2인 엘리먼트만 존재한다. 이때 target2 엘리먼트에는 텍스트 내용이 제거되었다.

![img38](./img/img38.png)

## 바꾸기
* replaceAll: 변경할 것(결과) -> 변경될 것(제어 대상자)
* replaceWith: 변경될 것(제어 대상자) -> 변경할 것(결과)

제어 대상과 바꾸고자 하는 것의 위치 


~~~
<div class="target" id="target1">
    target 1
</div>
 
<div class="target" id="target2">
    target 2
</div>
 
<input type="button" value="replaceAll target 1" id="btn1" />
<input type="button" value="replaceWith target 2" id="btn2" />
<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
<script>
    $('#btn1').click(function(){
        $('<div>replaceAll</div>').replaceAll('#target1');
    })
    $('#btn2').click(function(){
        $('#target2').replaceWith('<div>replaceWith</div>');
    })
</script>
~~~

## 복사

* 노드를 복사한다.
* 복사하여 똑같은 것이 만들어진다.

~~~
<div class="target" id="target1">
    target 1
</div>
 
<div class="target" id="target2">
    target 2
</div>
 
<div id="source">source</div>
 
<input type="button" value="clone replaceAll target 1" id="btn1" />
<input type="button" value="clone replaceWith target 2" id="btn2" />
<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
<script>
    $('#btn1').click(function(){
        $('#source').clone().replaceAll('#target1');
    })
    $('#btn2').click(function(){
        $('#target2').replaceWith($('#source').clone());
    })
</script>
~~~

![img39](./img/img39.png)

## 이동
* 노드 이동 -> 노드 단순 추가하는 기능이다.

~~~
<div class="target" id="target1">
    target 1
</div>
 
<div id="source">source</div>
 
<input type="button" value="append source to target 1" id="btn1" />
<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
<script>
    $('#btn1').click(function(){
        $('#target1').append($('#source'));
    })
</script>
~~~

---

# 문자열로 노드 제어

기존의 노드 api를 사용하여 제어하던 복잡한 방식을 편리하게 해주는 방법들이다. 조회 후 변경할 때 문자열 형태로 인자를 전달하면 해당 문자대로 코드를 적용시켜준다.
* innerHTML
* outerHTML
* innerText, outerText
* insertAdjacentHTML()

## innerHTML
* 엘리먼트의 하위 엘리먼트 코드를 조회할 수 있으며 값을 변경할 수도 있다.
~~~
<ul id="target">
    <li>HTML</li>
    <li>CSS</li>
</ul>
<input type="button" onclick="get();" value="get" />
<input type="button" onclick="set();" value="set" />
<script>
    function get(){
        var target = document.getElementById('target');
        alert(target.innerHTML);
    }
    function set(){
        var target = document.getElementById('target');
        target.innerHTML = "<li>JavaScript Core</li><li>BOM</li><li>DOM</li>";
    }
</script>
~~~

* 기존 화면
![img40.png](./img/img40.png)

* get click -> 하위태그의 엘리먼트 표시
![img41.png](./img/img41.png)

* set click -> 하위태그 내용을 변경
![img42.png](./img/img42.png)

## outerHTML
* 자시자신을 포함한 전체 엘리먼트 조회 및 변경 가능
~~~
<ul id="target">
    <li>HTML</li>
    <li>CSS</li>
</ul>
<input type="button" onclick="get();" value="get" />
<input type="button" onclick="set();" value="set" />
<script>
    function get(){
        var target = document.getElementById('target');
        alert(target.outerHTML);
    }
    function set(){
        var target = document.getElementById('target');
        target.outerHTML = "<ol><li>JavaScript Core</li><li>BOM</li><li>DOM</li></ol>";
    }
</script>
~~~

* 기존 화면
![img43.png](./img/img43.png)

* get click -> 자신을 포함한 전체 엘리먼트 표시
![img44.png](./img/img44.png)

* set click -> 자신을 포함한 전체 엘리먼트 값 변경
![img45.png](./img/img45.png)

## innerText, outerText

* 읽기를 하게되면 태그가 제외된 상태로 읽기가 되고
쓰기를 하게 되면 그 태그에 해당되는 내용이 문서에 반영되지않고 태그 내용 그대로 문서에 출력된다.

~~~
<ul id="target">
    <li>HTML</li>
    <li>CSS</li>
</ul>
<input type="button" onclick="get();" value="get" />
<input type="button" onclick="set();" value="set" />
<script>
    function get(){
        var target = document.getElementById('target');
        alert(target.innerText);
    }
    function set(){
        var target = document.getElementById('target');
        target.innerText = "<li>JavaScript Core</li><li>BOM</li><li>DOM</li>";
    }
</script>
~~~

* 기존 화면
![img46.png](./img/img46.png)

* get click -> 태그가 제외된 상태로 출력
![img47.png](./img/img47.png)

* set click -> 반영되지 않고 그대로 출력
![img48.png](./img/img48.png)

## insertAdjacentHTMl()

* 첫번째 인자로 4가지가 올 수 있다. `beforebegin`, `afterbegin`, `beforeend`, `afterend` 각각 `before`, `after`, `prepend`, `append`와 위치가 동일하다. 
* begin으로 끝나는 인자들은 시작되기 전을 의미하므로 해당 태그 바깥을 의미하며 end로 끝나는 인자들은 끝나기 전을 의미하므로 태그 아쪽을 의미한다. 
* 두번째 인자로 html 코드를 전달한다. 

~~~
<ul id="target">
    <li>CSS</li>
</ul>
<input type="button" onclick="beforebegin();" value="beforebegin" />
<input type="button" onclick="afterbegin();" value="afterbegin" />
<input type="button" onclick="beforeend();" value="beforeend" />
<input type="button" onclick="afterend();" value="afterend" />
<script>
    function beforebegin(){
        var target = document.getElementById('target');
        target.insertAdjacentHTML('beforebegin','<h1>Client Side</h1>');
    }
    function afterbegin(){
        var target = document.getElementById('target');
        target.insertAdjacentHTML('afterbegin','<li>HTML</li>');
    }
    function beforeend(){
        var target = document.getElementById('target');
        target.insertAdjacentHTML('beforeend','<li>JavaScript</li>');
    }
    function afterend(){
        var target = document.getElementById('target');
        target.insertAdjacentHTML('afterend','<h1>Server Side</h1>');
    }
</script>
~~~

* 버튼을 전부 click할 시

![img49](./img/img49.png)