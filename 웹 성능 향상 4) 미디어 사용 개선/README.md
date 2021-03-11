# 성능 향상 방법론 4. 미디어 사용 개선.

## 1. 이미지 스프라이트 사용.

이미지 스프라이트 : 여러개의 이미지를 하나의 이미지로 합쳐서 관리.

### example)

[코딩교육 티씨피스쿨](http://www.tcpschool.com/css/css_basic_imageSprites)

![%E1%84%89%E1%85%A5%E1%86%BC%E1%84%82%E1%85%B3%E1%86%BC%20%E1%84%92%E1%85%A3%E1%86%BC%E1%84%89%E1%85%A1%E1%86%BC%20%E1%84%87%E1%85%A1%E1%86%BC%E1%84%87%E1%85%A5%E1%86%B8%E1%84%85%E1%85%A9%E1%86%AB%204%20%E1%84%86%E1%85%B5%E1%84%83%E1%85%B5%E1%84%8B%E1%85%A5%20%E1%84%89%E1%85%A1%E1%84%8B%E1%85%AD%E1%86%BC%20%E1%84%80%E1%85%A2%E1%84%89%E1%85%A5%E1%86%AB%20a704d91620f64574aec6c57a819c89d5/Untitled.png](%E1%84%89%E1%85%A5%E1%86%BC%E1%84%82%E1%85%B3%E1%86%BC%20%E1%84%92%E1%85%A3%E1%86%BC%E1%84%89%E1%85%A1%E1%86%BC%20%E1%84%87%E1%85%A1%E1%86%BC%E1%84%87%E1%85%A5%E1%86%B8%E1%84%85%E1%85%A9%E1%86%AB%204%20%E1%84%86%E1%85%B5%E1%84%83%E1%85%B5%E1%84%8B%E1%85%A5%20%E1%84%89%E1%85%A1%E1%84%8B%E1%85%AD%E1%86%BC%20%E1%84%80%E1%85%A2%E1%84%89%E1%85%A5%E1%86%AB%20a704d91620f64574aec6c57a819c89d5/Untitled.png)

해당 이미지를 잘라서 사용.

```jsx
<style>
    .up, .down, .right, .left { background: url("/examples/images/img_image_sprites.png") no-repeat; }
    .up { width: 21px; height: 20px; background-position: 0 0; }
    .down { width: 21px; height: 20px; background-position: -21px 0; }
    .right { width: 22px; height: 20px; background-position: -42px 0; }
    .left { width: 22px; height: 20px; background-position: -65px 0; }
</style>
```

- 다운 받기 위한 서버 요청 감소.
- 한정된 자원을 사용하는 플랫폼에서도 효율적.
- 많은 이미지를 한 번에 관리 할 수 있음.

## 2. 실제 이미지 해상도 사용.

실제 이미지와 크기는 다르되, 비율은 그대로 유지.

500 x 400 이라면 5:4의 비율 유지.

→ 이미지를 변환시키는데 시간이 줄어든다.

## 3. CSS 3 활용.

이전 버전들과 완벽히 호환되는 새로운 최신 표준 권고안.

[CSS3](https://developer.mozilla.org/ko/docs/Archive/CSS3)

### 변경 사항.

- Selector
- Media Query
- Color
- namespace

### 모듈

이전 버전의 기능도 포함한 새로운 안정적인 모듈 형태로 구성됨.

- 선택자(Selectors)
- 박스 모델(Box Model)
- 배경(Backgrounds)
- 이미지(Image Values and Replaced Content)
- 텍스트 효과(Text Effects)
- 2D 변형(Transformations)
- 3D 변형(Transformations)
- 애니메이션(Animations)
- 다중 칼럼(Multiple Column) 레이아웃
- 사용자 인터페이스(User Interface)

< 브라우저별 접두어 >

safari, chrome : -webkit-

opera : -o-

IE : -ms-

## 4. 하나, 작은 크기 이미지는 Data URL 사용.

이미지를 로딩하는 방법에는 2가지.

1. Data URL
2. Image File

```jsx
<img src="data:image/png; base64, ..."/>

<img src="image.png"/>
```

### Data URL

장점 :

- 스프라이트 이미지와 같이 HTTP 요청을 절약.
- HTML 파일로 관리.

단점 : 

- 캐시되지 않아 매번 불러와야 함.

    ⇒ 메모리 캐시(브라우저)는 진행되지만, 디스크 캐시 (OS)는 되지 않음.

- 기존 파일보다 용량이 커질 수 있다. base64 인코딩 단계를 거치기 때문.
- 브라우저별 제한, 지원불가가 있음.