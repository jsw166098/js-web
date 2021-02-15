# Node 객체
* DOM의 가장 최상위 객체이다. 모든 DOM의 객체는 Node 객체를 상속받는다. Node의 모든 프로퍼티를 상속받는다. 

![img32](./img/img32.png)

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
Node.nodeType, Node.nodeName 메서드를 통해 하위 element에 접근하여 함수를 작성

body 부터 시작해서 element 하나하나를 접근한다.
~~~
traverse(document.getElementById('start'), function(elemn){
    console.log(elem);
})
~~~

~~~
traverse(document.getElementById('start'), function(elemn){
    if(elem.nodeName === 'A'){
        elem.style.backgroundColor = 'blue';    
    }
})
~~~