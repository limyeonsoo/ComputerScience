# Web 성능 향상 방법론 3. 효율적인 마크업 구조

## 1. 레거시 IE 모드는 HTTP 헤더 사용.

### Page Meta Tag

```jsx
<meta http-equiv="X-UA-Compatible" content="IE=EmulateIE7">
```

### HTTP Header

```jsx
HTTP/1.1 200 OK
Date: Sun, 14 Mar 2010 21:30:46 GMT
X-UA-Compatible: IE=EmulateIE7
```

## 2. @import 사용 피하기.

@import 는 직렬 방식을 사용하고 있다. → 병렬 방식에 비해 많이 느릴 수 있음. ⇒ 로딩 속도 저하.

IE에서는 다운로드 순서가 다르게 작동할 수도 있다.

**⇒ 권장 : HTML <link> 요소를 이용하여 호출하는 방법.**

## 3. inline 스타일 & embedded 스타일 피하기.

### CSS 적용 방법.

1. in-line 방식.

    HTML 태그에 직접 기술하는 방법

    `<p style="color:red"></p>`

2. embedded 방식.

    HTML 태그 <head> 안에 직접 기술하는 방법

    ```jsx
    <html>
    	<head>
    		<style>
    			p {color : red; }
    		</style>
    	</head>
    </html>
    ```

3. @import 방식.

    `<style> @import url(style.css); </style>`

4. **link 방식.**

    <link ref="style.css" rel=stylesheet" type="text/css" />

## 중복되는 코드 최소화.

## 단일 프레임워크 사용하기

## 서드파티 최소화.