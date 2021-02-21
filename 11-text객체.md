# Text 객체
* 텍스트 정보를 프로그래밍적으로 제어할 수 있는 객체이다.
* `Document`, `Element` 두 다 아닌 객체이다. 
* `CharacterData`의 기능을 상속받는 객체이다. 이때 CharacterData는 문서상에 드러나지 않으면 텍스트 노드 값을 조작할 수 있는 기능들을 제공한다. 
* 텍스트 노드는 DOM에서 실질적인 데이터가 저장되는 객체이다. 

~~~
<p>생활코딩</p>
-> <p></p> 부분은 Element이다. 이 속에 포함된 텍스트부분인 Text 객체이다. 
~~~

![img52](./img/img52.png)

출처: [생활코딩](https://opentutorials.org/course/1375/6744)

## DOM 에서의 공백
DOM에서는 공백도 객체에 매핑되어 있다. 

~~~
<p id="target1"><span>Hello world</span></p>  // p 태그와 span 태그 사이의 공백 존재하지 않음
<p id="target2">  // p 태그와 span 태그 사이의 공백 존재한다. 
    <span>Hello world</span>
</p>
<script>
var t1 = document.getElementById('target1').firstChild;
var t2 = document.getElementById('target2').firstChild;
 
console.log(t1.firstChild.nodeValue);
try{
    console.log(t2.firstChild.nodeValue);   
} catch(e){
    console.log(e);
}
console.log(t2.nextSibling.firstChild.nodeValue);
 
</script>
~~~

~~~
// p 태그 -> span 태그 -> text ("Hello world")
var t1 = document.getElementById('target1');
t1  //<p id = "target1">...</p>
t1.firstChild  //<span>Hello world</span>
t1.firstChild.firstChild  //"Hello world"

// p 태그 -> text element(공백에 해당되는 텍스트 element) -> span 태그 -> text ("Hello world")
var t2 = document.getElementById('target2');
t2  //<p id = "target2">...</p>

~~~

## Text 객체 API

### 값
* data
* nodeValue

### 조작
* appendData()
* deleteData()
* insertData()
* replaceData()
* subStringData()

### 생성
* document.createTextNode()

---

## 값 API
텍스트 노드는 DOM에서 실질적인 데이터가 저장되는 객체이므로 텍스트 노드는 값과 관련된 여러 기능들을 제공한다. 값을 알아오는 메서드는 다음과 같다.

* nodeValue : 값을 읽어오며 변경 또한 가능하다.
* data : 값을 읽어온다. 

~~~
<ul>
    <li id="target">html</li> 
    <li>css</li>
    <li>JavaScript</li>
</ul>
<script>
    var t = document.getElementById('target').firstChild;  // html 이란 text 객체
    console.log(t.nodeValue);  
    console.log(t.data);
</script>
~~~

![img53.png](./img/img53.png)

## 조작 API

택스트 노드가 상속 받은 `CharacterData` 객체는 다음과 같은 API를 제공한다.
* appendData()
* deleteData()
* insertData()
* replaceData()
* substringData(): 일부의 정보를 가공하는 기능, 일부 정보를 반환한다.

~~~
<!DOCTYPE html>
<html>
<head>
    <style>
    #target{
        font-size:77px;
        font-family: georgia;
        border-bottom:1px solid black;
        padding-bottom:10px;
    }
    p{
        margin:5px;
    }
    </style>
</head>
<body>
<p id="target">Cording everybody!</p>
<p> data : <input type="text" id="datasource" value="JavaScript" /></p>
<p>   start :<input type="text" id="start" value="5" /></p>
<p> end : <input type="text" id="end" value="5" /></p>
<p><input type="button" value="appendData(data)" onclick="callAppendData()" />
<input type="button" value="deleteData(start,end)" onclick="callDeleteData()" />
<input type="button" value="insertData(start,data)" onclick="callInsertData()" />
<input type="button" value="replaceData(start,end,data)" onclick="callReplaceData()" />
<input type="button" value="substringData(start,end)" onclick="callSubstringData()" /></p>
<script>
    var target = document.getElementById('target').firstChild;
    var data = document.getElementById('datasource');
    var start = document.getElementById('start');
    var end = document.getElementById('end');
    function callAppendData(){
        target.appendData(data.value);
    }
    function callDeleteData(){
        target.deleteData(start.value, end.value);
    }
    function callInsertData(){
        target.insertData(start.value, data.value); 
    }
    function callReplaceData(){
        target.replaceData(start.value, end.value, data.value);
    }
    function callSubstringData(){
        alert(target.substringData(start.value, end.value));
    }
</script>
</body>
</html>
~~~

![img54.png](./img/img54.png)


