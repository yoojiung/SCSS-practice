# SCSS 
-css 전처리기 도구이다  
-sass 문법을 통해서 만든 것을 컴파일을 통해서 css로 보내줄 수 있다.  

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
-& 는 상위요소를 참조하고 있다는 뜻  
-& 는 범위 내에 있는 선택자이다  
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


