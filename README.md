## Javascript


### Math.abs()
절대값을 반환해줍니다.
```javascript
Math.abs(3);
// return 3
Math.abs(-3);
// return 3
```

### 두 날짜의 일, 시간, 분 차이계산
두 날짜의 차이를 계산해줍니다.
```javascript
const date1 = new Date();
const date2 = new Date();

const diffDay = Math.ceil((date1- date2) / (1000 * 3600 * 24)); // 일
const diffHours = Math.ceil((date1- date2) / (1000 * 3600)); // 시간
const diffMinutes = Math.ceil((date1- date2) / (1000)); // 분
```


```javascript
const dateCalc = (dateGet, value, index)=>{
    if(value , index !== undefined){
      const revDate = new window.Date(dateGet.replace(/-/g, "/"));
      /* 기준
      1시간 이전 분표시 : ?분전 / 1일 이전 시간표시 : ?시간전 / 30일 이전 일표시 : ?일전 / 30일 이후 날짜표시 : 21-04-02
      */
     let diffDay =  Math.ceil((MToday.getTime() - revDate.getTime())  / ( 1000 * 3600 * 24 ));
     let diffHours = Math.ceil((MToday.getTime() - revDate.getTime())  / ( 1000 * 3600 ));
     let diffMinutes = Math.ceil((MToday.getTime() - revDate.getTime())  / ( 1000 ));
     
     /* test data */
     
     // if(index === 1){
       //   diffMinutes = 60;
       //   diffHours = 24;
       //   diffDay = 20;
       // }
       
       let result = '';
       
       if(diffMinutes < 60){ // 1시간 이전 판단
        result = diffMinutes + '분전';
      }else if(diffMinutes >= 60 && diffHours < 24){ // 1시간 이상이고 1일 이전 판단
        result = diffHours + '시간전';
      }else if(diffHours >= 24 && diffDay <= 30){ // 1일 이상이고 30일 이하 판단
        result = diffDay + '일전'
      }else{ // 30일 초과 판단
        result = revDate.getFullYear()+'-'+ ( (revDate.getMonth() + 1) < 10 ? "0" + (revDate.getMonth() + 1) : ( revDate.getMonth() + 1 ) ) +'-'+ ( revDate.getDay() < 10 ? "0" +       revDate.getDay() : revDate.getDay() );
      }
      
      return result;
    }
  }
```
