# HTML_META

## html의 메타 태그를 공부합니다.

### name="format-detection"
> 아이폰 사파리에서 숫자, 주소, 이메일의 형식을 링크로 인식한다고합니다.  
> 따라서 이것을 제거하기 위해 해당 메타 태그를 추가해주면 링크가 제거됩니다.  
> content의 각 속성은 핸드폰, 주소, 이메일을 제거하는 태그들입니다.  
```html
<meta name="format-detection" content="telephone=no, address=no, email=no" />
<meta name="format-detection" content="no" /> // 아이폰 4에서는 작동이 안된다고합니다.

```
