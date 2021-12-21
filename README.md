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

### input의 커서 위치 제어
input type의 타이핑을 칠 수 있는 박스의 커서 위치를 제어합니다.
여기서 unit.length는 prefix로 붙여줄 텍스트의 길이를 의미합니다.
리엑트 hook 기준으로 작성하였습니다.
```javascript
const inputRef = useRef();
    useEffect(()=>{
        if(inputRef.current !== undefined){
            if(!onlyInput){
                let current = inputRef.current;
                let valueLength = current.value.length - unit.length;
                if(current.setSelectionRange){
                    current.focus();
                    current.setSelectionRange(valueLength, valueLength);
                }else if(current.createTextRange){
                    // IE8 and below 대비
                    let range = current.createTextRange();
                    range.collapse(true);
                    range.moveEnd('chracter', valueLength);
                    range.moveStart('chracter', valueLength);
                    range.select();
                }
            }
        }
    },[value?.state, inputRef]);
```

### 날짜와 알파벳을 활용한 난수 생성
현재의 날짜 + 알파벳 랜덤(사용자 설정갯수)을 합쳐 난수를 생성합니다.
함수의 parameter값 lengthCha의 갯수에 따라 랜덤으로 나오는 알파벳의 갯수가 다릅니다.
```javascript
const createPayOid = (lengthCha)=> { // 난수 생성
        const ranPlusNum = lengthCha, cha = ["a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n", "o", "p", "q", "r", "s", "t", "u", "v", "w", "x", "y", "z"];
        let chaResult = "";
        const dateGet = new Date(), year = dateGet.getFullYear(), month = dateGet.getMonth() + 1, day = dateGet.getDate(), hours = dateGet.getHours(), minutes = dateGet.getMinutes(), seconds = dateGet.getSeconds();
        const dateReulst = year + "" + (month < 10 && ("0"+month) || month) + "" + (day < 10 && ("0"+day) || day) + "" + (hours < 10 && ("0"+hours) || hours) + (minutes < 10 && ("0"+minutes) || minutes) + (seconds < 10 && ("0"+seconds) || seconds);
        Array(ranPlusNum).fill().map(()=>{ chaResult += cha[Math.floor(Math.random() * cha.length-1) + 1]; });
        return dateReulst+chaResult;
    }
```

### 리엑트 jsx 컴포넌트 텍스트 반환
리엑트 컴포넌트로 만들어져있는 Array에 해당 텍스트가 있는지 판별해줍니다.
\n이 들어가있는것을 지워주기위해 replace,정규표현식이 사용되었고 
핵심은 map함수와 findIndex 함수입니다.

```javascript
const HandWorkDegree = [<span>리스트 1</span>,<span>리스트 2<PcBr/>(설명 텍스트)</span>,<span>리스트 3</span>]
let stringList = [];
HandWorkDegree.map((item)=>{ 
    let string = ""; 
    if(item.props.children.length > 0 && typeof item.props.children === "object"){
        item.props.children.map((item, index, arr)=>{
            if(typeof item === "string"){
                if(index !== arr.length - 1){
                    string += item + " ";
                }else{
                    string += item;
                }
            }
        })
    }else{
        string = item.props.children;
    }
    stringList.push(string);
    string = "";
});
setSelectHandWork(stringList.findIndex((item)=>handWork.replace(/(\r\n|\n|\r)/gm, " ") === item));

```
