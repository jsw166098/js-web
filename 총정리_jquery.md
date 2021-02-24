# JQuery
* DOM을 내부에 감추고 보다 쉽게 웹페이지를 조작할 수 있도록 돕는 도구
* `제어 대상자를 찾는 과정`과 `메서드를 적용시키는 과정`을 간단하게 해준다.

## jQuery 객체
* jQuery 객체 형태로 메서드를 사용하며 다룬다.
* 선택된 엘리먼트 전체에 동시 작업이 처리된다. 암시적인 반복이 자동적으로 적용된다.
~~~
var li = $('li');
li  // jQuery Object
~~~

## jQuery 기본 문법

* 항상 `$`로 시작된다. `$()`는 jQuery의 함수이다. 
* 일반적으로 인자값으로는 CSS 선택자가 들어온다. 
* jQuery 객체를 리턴하며 이 객체는 선택자에 해당하는 엘리먼트를 제어하는 다양한 메소드를 가지고 있다. 

~~~
// 태그명
$('li').css('color', 'red')     

// 클래스 명
$('.active').css('color', 'red')

// 아이디 명
$('#active').css('color', 'red').css('textDecoration', 'underline');
~~~

* css 선택자로 접근할 경우 '' 따옴표로 묶어준다.
* DOM 객체로 접근할 경우 해당 객체를 작성한다.
~~~
$('<css selector>'): css 선택자를 통해 jQuery 객체 생성
$(<dom 객체>) : DOM 객체에서 jQuery 메서드를 사용하기 위해 jQuery 메서드로 만든다. !
~~~

### 1. 조회 및 설정
* 값을 설정할 때 모든 엘리먼트 마다 반복해서 적용시켜 준다.
* 두 개의 인자 -> 값 설정
* 하나의 인자 -> 값 조회
~~~
li.css('test-decoration', 'underline');  // 두 개의 인자를 작성하면 설정을 하게 된다.

li.css('test-decoration')  // 하나의 인자를 작성하면 값을 가져온다. 
~~~

### 2. 태그 아래에 추가
* body 태그를 선택한다.
* prepend 명령문을 통해서 body 태그 아래에 뒤의 명령을 추가한다.
~~~
$('body').prepend('<h1>Hello world</h1>');
~~~

### 3. 체이닝 이용
* 체이닝을 통한 선택한 elements 들에 대해서 연속적으로 메소드를 호출해서 작업을 하는 것
~~~
// 첫번째 css 메서드의 리턴값을 그 다음 css 메서드가 받아 적용시킨다. 즉 색이 붉은색으로 변경된 단어 밑에 밑줄이 생긴다. 체이닝!!
$('$active').css('color', 'red').css('textDecoration', 'underline');
~~~

### 4. map 이용
* map 메서드는 엘리먼트를 조회할 때 사용되며 선택한 엘리먼트 모두를 순회하면서 인자로 전달한 함수를 모두 호출한다.
* 인자로 전달한 함수에서 첫번째 파라미터는 인덱스이며 두번째 파라미터는 dom 객체를 의미한다.
* jquery의 암시작 반복을 이용하여 반복을 통해 접근할때 마다 특정 작업 처리 가능하다. 

~~~
<ul>
    <li>html</li>
    <li>css</li>
    <li>JavaScript</li>
</ul>
<script src="http://code.jquery.com/jquery-1.11.0.min.js"></script>
<script>
    var li = $('li');
    li.map(function(index, elem){
        console.log(index, elem);
        $(elem).css('color', 'red');
    })
</script>
~~~

~~~
list = ['red', 'blue', 'green']
$('li').map(function(index, elem){
    console.log(index, elem);
    $(elem).css('color', list[index]);
    
})
~~~


### 유사 배열 형태
* jQuery 객체에는 조회된 엘리먼트가 담겨있으며 해당 모든 엘리먼트가 유사배열 형태고 담겨져 있다.
* 유사배열 형태로 모든 해당 엘리먼트를 가지고 있으므로 메서드 사용시 모두 적용된다. 이는 jqury의 즁요한 특징이며 메서드 사용시 반복적으로 작업이 처리되는 것을 알 수 있다.

---

## jQuery api

### 1. 속성 api
~~~
// 속성값 작성하지 않으면 조회만 발생
$( ).attr('<속성>', '<속성값>');  //작성된 그대로
$( ).prop('<속성>', '<속성값>');  //적용된 값

$( ).removeAttr('<속성>');
~~~

### 2. selector context
* A 선택자를 가진 element 중에서 B를 선택자로 가지고 있는 element 조회 
~~~
$('A', 'B')
~~~

### 3. find api
* jquery 객체 내에서 element를 조회하는 기능
~~~
$( "#active").find('.marked').css( "background-color", "red" );
~~~

