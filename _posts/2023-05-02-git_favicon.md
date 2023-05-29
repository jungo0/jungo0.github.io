---
title:  "[Github Blog] 파비콘(Favicon) 설정하기"
excerpt: "Github 블로그 커스타마이징, 파비콘(Favicon) 설정하기 파비콘(Favicon)이란, 인터넷 웹 브라우저의 주소창에 표시되는 대표 아이콘입니다."
categories: Github
tag: [Github_Blog, Favicon]
toc: true
author_profile: false


sidebar:
    nav: "counts"
---

## <span style='color:RGB(135, 203, 206)'>파비콘(Favicon)

>파비콘(Favicon)이란, 인터넷 웹 브라우저의 주소창에 표시되는 대표 아이콘입니다.

기본적으로 세팅해두지 않으면,


![](/assets/images/2023-05-09-git_favicon/nav.png)

다음과 같은 아이콘으로 나타나게 됩니다.
자신의 블로그를 나타내기 위해서는 기본 값 보다는 원하는 모양으로 바꾸는게 좋을거 같아서 알아보겠습니다!

### 원하는 이미지 찾기
이미지는 직접 만들어도 되고, 다음과 같은 사이트에서 찾아도 됩니다. 저는 `favicon`에서 이미지 파일을 다운받아 활용했습니다.

- [flaction](https://www.flaticon.com/)
- [Icooon-mono](https://icooon-mono.com/)
- [Thenounproject](https://thenounproject.com/)
- [Iconfinder](https://www.iconfinder.com/)
- [Freepik](https://www.freepik.com/)
- [FreeVectors](https://www.freevectors.net/)
- [favicon](https://favicon.io/)

저는 이 아이콘을 선택했습니다.
(다운로드 -> zip파일)
![](/assets/images/2023-05-09-git_favicon/peach.png)

### favicon icon 만들기
다운로드한 이미지를 파비콘으로 만들어야 합니다.
https://www.favicon-generator.org/
![](/assets/images/2023-05-09-git_favicon/generator.png)

1. 파일선택
2. Create Favicon

#### 파비콘 생성
파비콘을 생성하면 다음과 같은 HTML code를 생성합니다.
이 코드를 활용해서 블로그에 적용할 수 있습니다.

![](/assets/images/2023-05-09-git_favicon/generator2.png)

### custom,html 수정
- 수정 파일 : github.io 폴더 > _includes 폴더 > _head 폴더 > custom.html


최종적으로 업데이트 된 코드는 이와 같습니다.
처음 받은 코드와 다른 내용은 href의 영역 즉 상세 링크입니다.
파일 이름 앞에 /assets/logo.ico 를 추가해주시면 됩니다.
html에서 변수를 호출하기 위해서는 중괄호가 꼭 이중으로 있어야 합니다.

#### 적용된 모습
![](/assets/images/2023-05-09-git_favicon/nav2.png)

❖ 주의할점 : 파비콘 생성한 코드를 적용할때 assets 폴더 아래에 정확한 링크를 입력해줘야 적용됩니다.
+ 시간이 좀 지나야 적용됩니다.