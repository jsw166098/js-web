# WEB

WEB은 DOM, BOM, JavaScript 3가지 요소로 이루어진 객체 모델이다.

# DOM
DOM은 객체 형태로 설계되어 있다. 따라서 객체 단위로 제어 대상을 찾아 해당 객체가 가지고 있는 메서드를 적절하게 사용하여 웹 문서를 다루게 된다. 
~~~
1. 제어 대상 찾기
2. 제어 대상
3. ELEMENT API
4. NODE API
5. Jquery
~~~

## 1. 제어 대상 찾기
* document.getElementsByTagName
* document.getElementsByClassName
* document.getElementById
* document.querySelector
* document.querySelectorAll

## 2. 제어 대상
* 제어 대상의 중요성 -> 대상에 따라 사용가능한 메서드가 다르다.

## 3. ELEMENT API
### 식별자 api
* Element.tagName
* Element.id
* Element.className
* Element.classList
### 조회 api
* document.getElementBy*
* Element.getElementBy*
### 속성 api
* Element.getAttribute()
* Element.setAttribute()
* Element.hasAttribute()
* Element.removeAttribute()

`(총정리_00, 총정리_01)`

## 4. NODE API
### 노드 관계 api
* Node.childNodes : 자식노드들을 유사배열에 담아서 리턴
* Node.firstChild : 첫번째 자식노드
* Node.lastChild : 두번째 자식노드
* Node.nextSibling : 다음 형제 노드
* Node.preivousSibling : 이전 형제 노드
### 노드 종류 api
* Node.nodeType
* Node.nodeName
### 노드 변경 api
* appendChild
* insertBefore
* removeChild
* replaceChild

### 문자열로 노드 제어
* innerHTML
* outerHTML
* innerText, outerText
* insertAdjacentHTML()

`(09-Node객체)`

---

# 노드의 각 요소

![img32](./img/img32.png)
출처: [생활코딩](https://opentutorials.org/course/1375/6698)

~~~
document 노드
text 노드
~~~

## document 노드
ㅂ

## text 노드

---
## 출처

생활코딩의 클라이언트의 자바스크립트에서 웹브라우저 자바스크립트를 학습하고 복습하는 내용을 정리한 자료들 입니다.

[생활코딩-웹브라우저자바스크립트](https://opentutorials.org/course/1375)