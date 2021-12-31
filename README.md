## Javascript


### Math.abs()
절대값을 반환해줍니다.
```javascript
Math.abs(3);
// return 3
Math.abs(-3);
// return 3
```

### 두 날짜의 일, 시간, 분 차이계산 ()
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

### 날짜 형식 반환 (업데이트중)
날짜형식으로 된 데이터를 값으로 넘기면 자동으로 파라미터값에 따라서 반환해줍니다.
형식 : 2021.12.10 10:25:30 , 21년 12월 10일 10:25:30

```javascript
/*
@params
date : 날짜형식으로 된 날짜 (date)
slice : 21.10.11 에서 . 나누는곳에 추가할 글자 (string)
prefix : 년, 월, 일의 prefix를 추가할지 (boolean)
view : year,month,day,hours,minutes,seconds 각 글자를 , 와 함께 추가하면 반환해준다 (string)
yearHalf : 2021 데이터를 21만 반환하고 싶을때 true 아니면 false를 입력한다 (boolean)
*/
export const dateReturn = (date, slice, prefix, view, yearHalf)=>{
    let getDate = new Date(date);

    let getYear = getDate.getFullYear();
    let getMonth = getDate.getMonth();
    let getDay = getDate.getDate();
    let getHours = getDate.getHours();
    let getMinutes = getDate.getMinutes();
    let getSeconds = getDate.getSeconds();

    function viewCheck(type){
        let getView = view?.split(","), isView = false;
        if(getView?.length > 0){
            for(let i = 0; i < getView.length; i++){
                if(getView[i] === type){ isView = true; break; }else{ isView = false; }
            }
        }else{ isView = true; }
        return isView;
    }
    let yearResult = viewCheck("year") && `${yearHalf && (getYear.toString()[getYear.toString().length-2]+""+getYear.toString()[getYear.toString().length-1]) || getYear}${prefix && "년" || ""}` || '';
    let monthResult = viewCheck("month") && `${getMonth >= 10 && getMonth || "0"+getMonth}${prefix && "월" || ""}` || '';
    let dayResult = viewCheck("day") && `${getDay >= 10 && getDay || "0"+getDay}${prefix && "일" || ""}` || '';
    let hoursResult = viewCheck("hours") && `${getHours >= 10 && getHours || "0"+getHours}${prefix && "시" || ""}` || '';
    let minutesResult = viewCheck("minutes") && `${getMinutes >= 10 && getMinutes || "0"+getMinutes}${prefix && "분" || ""}` || '';
    let secondsResult = viewCheck("seconds") && `${getSeconds >= 10 && getSeconds || "0"+getSeconds}${prefix && "초" || ""}` || '';

    return `${yearResult}${yearResult !== "" && slice || ""}${monthResult}${monthResult !== "" && slice || ""}${dayResult} ${hoursResult}${minutesResult !== "" && ":" || ""}${minutesResult}${secondsResult !== "" && ":" || ""}${secondsResult}`;
  }
```
### 받아온 날짜 계산 (위의 dateReturn과 함께 사용)
형식 :  21년 2월 10일(오늘) 오전 01:25
```javascript
const dateCalc = (date)=>{
    let result = "";
    let cal = "";
    let time = "";
    if(date !== "" && date !== null && date !== undefined){
        cal = dateReturn(date, ". ", false, "year,month,day", true);
        const today = dateReturn(new Date(), ". ", false, "year,month,day", true);
        time = dateReturn(date, "", false, "hours,minutes", true);
        const timeCalc = parseInt(time.split(":")[0]) > 12 ? "오후 " + ( (parseInt(time.split(":")[0]) - 12 < 10 && "0"+parseInt(time.split(":")[0]) - 12 || parseInt(time.split(":")[0]) - 12) ) : parseInt(time.split(":")[0]) <= 12 && parseInt(time.split(":")[0]) !== 0 ? "오전 " + ( ( parseInt(time.split(":")[0]) < 10 && "0"+parseInt(time.split(":")[0]) || parseInt(time.split(":")[0]) ) ) : 12;
        result = cal+"일"+(cal === today && "(오늘) " || " " )+timeCalc+" : "+parseInt(time.split(":")[1]) + " 출발";
    }
    return result;
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

### javascript 주소 parameter 받기
주소창의 파라미터를 받아와야할때 사용합니다.

```javascript
function useParams(name) {
    name = name.replace(/[\[]/, "\\[").replace(/[\]]/, "\\]");
    var regex = new RegExp("[\\?&]" + name + "=([^&#]*)"),
        results = regex.exec(location.search);
    return results === null ? "" : decodeURIComponent(results[1].replace(/\+/g, " "));
}
const getParams = useParams("params");
```

### localstorage 사용
브라우저의 localstorage를 편하게 사용하기 위해 만들어진 함수입니다.

```javascript
// localstorage 지정
function setLocalS(key, value){
    localStorage.setItem(key, value);
}
// localstorage 가져오기 (useRemove true이면 가져오고 해당 값 지우기)
function getLocalS(key, useRemove){
    let result = "";
    if(localStorage.getItem(key) !== null){
        result = localStorage.getItem(key);
        if(useRemove){
            removeLocalS(key);
        }
        return result;
    }else{
        return false;
    }
}
// localstorage 지우기
function removeLocalS(key){
    localStorage.removeItem(key);
}
```


### 달력 생성 
날짜 형식으로 된 string을 파라미터로 넘기면 달력 정보를 받아온다

```javascript
//@param : getDate -> 날짜 정보
const calendarFunc = (getDate)=> {
    const selectDate = new Date(getDate);
    const selectYear = selectDate.getFullYear();
    const selectMonth = selectDate.getMonth() + 1;
    const selectDay = selectDate.getDate();
    setSelect({year:selectYear, month:selectMonth, day:selectDay});
    /* 선택된 지난달 */
    const prevDate = new Date(selectYear, (selectMonth - 1), 0); // 지난달 마지막날
    const prevLastWeek = prevDate.getDay() + 1; // 지난달 마지막 날 요일
    /* 선택된 이번달 */
    const thisDate = new Date(selectYear, selectMonth, 0); // 선택된달 마지막날
    const thisDateLength = thisDate.getDate(); // 선택된달 총 길이

    let dateArr = [];
    const allDateLength = thisDateLength + prevLastWeek;
    const prevProcess = prevLastWeek - 1; 
    for(let i = 0; i < allDateLength; i++){
        let dateObject = {};
        if(i <= prevProcess){ // 이전달
            dateObject = {type:"prev"};
        }else{ // 선택된달
            dateObject = {type:"this", year:selectYear, month:selectMonth, day:i - prevProcess};
        }
        dateArr.push(dateObject);
    }
    setDateInform(dateArr);
}
```
