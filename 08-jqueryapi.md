# jQuery 속성 제어 API

* element api기능과 비슷한 jquery의 api
~~~
element <- htmlelement <- html~element
~~~

* setAttribute, getAttribute 대응되는 메서드는 `attr`이다.
* removeAttribute에 대응되는 메소드는 `removeAttr`이다.

~~~
<a id="target" href="http://opentutorials.org">opentutorials</a>
<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
<script>
var t = $('#target');
console.log(t.attr('href')); //http://opentutorials.org
t.attr('title', 'opentutorials.org'); // title 속성의 값을 설정한다.
t.removeAttr('title'); // title 속성을 제거한다.
</script>
~~~


![img31](./img/img31.png)

---

# attribute와 property 

* attr은 attribute 방식이다. 태그 속성값에 작성된 그대로 받아들인다. 

* prop은 property 방식이다. 적용된 값이 반환된다.


~~~
<a id="t1" href="./demo.html">opentutorials</a>
<input id="t2" type="checkbox" checked="checked" />
<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
<script>
// 현재 문서의 URL이 아래와 같다고 했을 때
// http://localhost/jQuery_attribute_api/demo2.html
var t1 = $('#t1');
console.log(t1.attr('href')); // ./demo.html 
console.log(t1.prop('href')); // http://localhost/jQuery_attribute_api/demo.html 
 
var t2 = $('#t2');
console.log(t2.attr('checked')); // checked
console.log(t2.prop('checked')); // true
</script>

~~~

* jquery를 이용할 시 이름 형태가 동일하다. 
~~~
<div id="t1">opentutorials</div>
<div id="t2">opentutorials</div>
<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
<script>
$('#t1').prop('className', 'important'); 
$('#t2').prop('class', 'current');  
</script>
~~~

---

# jQuery 조회 범위 제한

* 문서의 전체가 아니라 특정 element의 하위 element만 찾는 방법
* element 객체에서 getElementsBy* 메소드를 사용하면 조회의 범위가 해당 객체의 해당 하위 엘리먼트로 제한되었다.

## selector context

* A 선택자를 가진 element 중에서 B를 선택자로 가지고 있는 element 조회 
~~~
$('A','B')
~~~

* id값이 active인 element의 하위 태그의 makred 클래스명을 가진 element 제어
~~~
<ul>
    <li class="marked">html</li>
    <li>css</li>
    <li id="active">JavaScript
        <ul>
            <li>JavaScript Core</li>
            <li class="marked">DOM</li>
            <li class="marked">BOM</li>
        </ul>
    </li>
</ul>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
<script>
    //$("#active", ".marked").css("background-color", "red"); 와 같은 의미이다.
    $( ".marked", "#active").css( "background-color", "red" );
</script>
~~~

## .find

* jquery 객체 내에서 element를 조회하는 기능
~~~
$( "#active").find('.marked').css( "background-color", "red" );
~~~

* 체인을 끊지 않고 작업의 대상을 변경할 수 있다. -> find에 앞서 적용된 코드들이 동일하게 적용된다. 
~~~
$('#active').css('color','blue').find('.marked').css( "background-color", "red" );
~~~
