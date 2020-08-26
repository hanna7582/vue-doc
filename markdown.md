<div id="contents"> 

# 목차
- [접기/펼치기](#1)
- [테이블](#2)
- [제목](#3)
- [링크/이미지](#4)
- [코드블럭](#5)
- [기타](#6)
</div>

<div id="1"> 

<details><summary>CLICK ME</summary>  

```
pythonprint("hello world!")
```
</details>
</div>


<div id="2">

## 테이블 alt+shift+f [위로](#contents)

| 값          |           의미           |      기본값 |
| ---------- | :--------------------: | -------: |
| `static`   |   유형(기준) 없음 / 배치 불가능   | `static` |
| `relative` |     요소 자신을 기준으로 배치     |
| `absolute` | 위치 상 부모(조상)요소를 기준으로 배치 |
| `fixed`    |    브라우저 창을 기준으로 배치     |

**테이블 생성**
Header 1 | Header 2
--------- | ---------
Content 1 | Content 3
Content 2 | Content 4

**테이블정렬**
| Header 1 | Header 2 | Header 3 |
| :-------- | :--------: | --------: |
| Left | Center | Right |

</div>
<div id="3">

# 제목 [위로](#contents)
제목
==
## 제목
제목
--
### 제목
#### 제목
##### 제목
###### 제목

</div>

<div id="4">

## 링크/이미지 [위로](#contents)
ctrl+v  
[네이버가기 텍스트](https://www.naver.com/)  
![네이버이미지](https://ssl.pstatic.net/static/help/img/img_logo_naver_200X200.png "네이버가기")  
[![네이버가기 이미지](https://ssl.pstatic.net/static/help/img/img_logo_naver_200X200.png)](https://www.naver.com/)  

</div>

<div id="5">

## 코드블럭 [위로](#contents)

```javascript
import _ from 'lodash';

function component() {
    var element = document.createElement('div');

    /* lodash is required for the next line to work */
    element.innerHTML = _.join(['Hello', 'webpack'], ' ');

    return element;
}

document.body.appendChild(component());
```

```css
.list > li {
  position: absolute;
  top: 40px;
}
```

```markdown
# 제목
**굵은글씨**
```
</div>


<div id="6">

## 기타 [위로](#contents)

---
라인입니다.
***
`강조`   
**굵은 글자 ctrl+b**  
__굵은 글자__  
~~취소선~~  
*이텔릭*  
_이텔릭_  
<u>밑줄</ul>

체크박스 alt+c
- [x] 체크박스1
- [x] 체크박스2
- [x] 체크박스3

>인용문구
>>중첩 인용


줄바꿈은  
띄어쓰기 두번이나<br>
br태그를 넣는다.

</div>
