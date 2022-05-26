# SCSS 
- css 전처리기 도구이다  
- sass 문법을 통해서 만든 것을 컴파일을 통해서 css로 보내줄 수 있다.  

[scss연습사이트](https://www.sassmeister.com/)

***

## 주석
```
/* background-color: orange; */
   or
// font size : 60px;
```
주의! // 이 방법은 css compiled 되면 사라진다.  

***

## 중첩(Nesting)
- 좀 더 쉽게 선택자를 이용해서 style가능하다

***

## & 상위 선택자
```scss
.btn {
  position:absolute;
  &.active {
    color:red;
  }
}
```
같은내용이다
```css
.btn {
  position:absolute;
}
.btn.active {
  color:red;
}
```
- & 는 상위요소를 참조하고 있다는 뜻  
- & 는 범위 내에 있는 선택자이다  
ex ) 
```css
.fs {
  &-small {font-size:12px;}
  &-medium {font-size:16px;}
  &-large {font-size:20px;}
}

             =

.fs-small {
  font-size:12px;
}
.fs-medium {
  font-size:16px;
}
.fs-large {
  font-size:20px;
}
```

***

## 중첩된 속성
```css
font: {
  weight:bolid;
  size:10px;
  family:sans-serif;
};
```
-중첩된 속성에는 위와 같은 코드로 작성할 수 있다  
-블럭 안에 ;들어가는 것에 주의  
-namespace : 이름을 통해 구분 가능한 범위를 만들어 내는 것으로 일종의 유효범위를 지정하는 방법.  

***

## 변수
```css
$size : 100px;
```
-변수를 지정할 때 달라($)를 이용해서 지정할 수 있다  
-값을 사용할 때에도 $size 를 이용하면 된다 

***

## 연산  
```css
div {
  $size : 30px;
  width:20px+20px;
  height:40px-10px;
  font-size: 10px * 2;
  /* 나누기(/)는 소괄호로 묶어서 사용할 것 */
  /*              or              */
  /* $size/2 변수를 사용하면 묶음처리는 필요없다 */
  margin : (30px / 2); 
  padding : 20px & 7;
}
```
-기본적인 단위가 일정해야 한다  
-calc()함수를 이용하면 다른 단위도 사용이 가능하다
 
 ***

 ## 재활용(mixin)
 ```css
 @mixin center {
   display:flex;
   justify-content:center;
   align-items:center;
 }
 .container {
   @include center;
   .item {
     @include center;
   }
 }
 ```
>@mixin 이라는 것으로 값을 지정해주고 속성값을 넣어주면 된다  
>@include 로 호출한 뒤 값을 사용하면 된다
```css
@mixin box($size) {
  width: $size;
  height: $size;
}
.container {
  @include box(100px);
}
```
>변수를 이용할 수도 있다  
>js함수 매개변수,인수와 비슷하다
```css
@mixin box($size:100px,$color: tomato) {
  width: $size;
  height: $size;
  background-color: $color;
}
.container {
  @include box($color:green);
}
```
>매개변수에 값을 지정해주면 위와 같은 코드로도 사용이 가능하다  
>변수 2개중 한 값만 사용하고 싶다면 키워드 인수를 통해서 한 값만 사용이 가능하다  

***

## 반복문(for)
```css
@for $i from 1 through 10 {
  .box:nth-child(#{i}) {
    width:100px
  }
}
```
- i: index의 약자로 통상적으로 쓴다
- from: 몇부터 시작할지 지정하는 값
- through: 몇까지 반복할지 지정하는 값
- #{}: scss에서는 위와 같은 방법으로 보간을 한다
- tip! : css는 0베이스넘버가 아닌 1부터 시작이다 

***

## 함수(function)
```css
@function ratio ($size, @ratio) {
  @return $size * $ratio
}

.box {
  $width: 100px;
  width: $width;
  height: ratio($width,1/2);
}
 결과값은 {
   width: 100px;
   height: 50px;
 }
```
- 값을 반환하기 위해서 사용한다

***

## 내장함수
```css
.box {
  $color: royalblue;
  width: 200px;
  height: 100px;
  margin: 20px;
  border-radius: 10px;
  background-color: $color;
}
&.built-in {
  background-color: mix($color,red);
  /* mix(color1,color2) : color1,color2를 mix할 때 사용 */
  background-color: lighten($color,10%);
  /* lighten(color,n%) : color를 n%만큼 밝혀주는 역할 */
  background-color: darken($color,10%);
  /* darken(color,n%) : color를 n%만큼 어두워지는 역할 */ 
  background-color: saturate($color,10%);
  /* saturate(color,n%) : color를 n%만큼 채도를 올려주는 역할 */ 
  background-color: desaturate($color,10%);
  /* desaturate(color,n%) : color를 n%만큼 채도를 내려주는 역할 */ 
  background-color: grayscale($color);
  /* grayscale(color) : color를 grayscale로 변경 */ 
  background-color: invert($color);
  /* invert(color) : color를 반전 */ 
  background-color: rgba($color,.5,);
  /* invert(color,.n) : color를 .n만큼 투명도를 올림 */ 
}
```
- scss에 내장된 함수이다
- color 관련 내장함수는 :hover를 이용할 때 용이하다

***

## 가져오기
```css
@import "./sub.scss","./sub2.scss";
```
- @import 를 통해서 가져올 수 있으며 확장자는 생략이 가능하다

***

## 리팩토링(Refactoring)
- 결과의 변경 없이 코드의 구조를 재조정함

***

## 데이터의 종류
```css
$number : 1; // .5 ,100px, 1em
$string : bold; // relative, "../images/a .png"
$color : red; // blue, #FFFF00, rgba(0,0,0,.1)
$boolean : true; // false
$null : null;
$list : orange,royalblue, yellow
$map : (
  o : orange;
  r : royalblue;
  y : yellow;
)
/* 위 코드는 js객체데이터와 달리 ()로 표현한다 */
```

***

## 반복문 @each
```css
@each $c in $list { }
/* @each를 통해서 $list를 반복적으로 $c에 담아서 {}로 처리 */
```

```css
@each $key,$value in $map {
  .box #{$k} {
    color: $v;
  }
}
 
```

***

## 재활용(content)
```css
@mixin font {
  font-size: 15px;
  font-color: red;
  @content
}

.box {
  width: 200px;
  height: 100px;
  @include font {
    font-decoration: solid;
  }
}
```
- @content 는 @mixindp 쓰일 때 추가로 작성할 때 쓰인다
