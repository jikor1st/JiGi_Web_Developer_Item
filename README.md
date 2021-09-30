## Javascript Math 함수


### Math.abs()
절대값을 반환해줍니다.
```javascript
Math.abs(3);
// return 3
Math.abs(-3);
// return 3
```

### 두 날짜의 일, 시간, 분 차이계산
```javascript
const date1 = new Date();
const date2 = new Date();

const diffDay = Math.ceil((date1- date2) / (1000 * 3600 * 24)); // 일
const diffHours = Math.ceil((date1- date2) / (1000 * 3600)); // 시간
const diffMinutes = Math.ceil((date1- date2) / (1000)); // 분
```
