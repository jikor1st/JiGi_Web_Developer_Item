# STUDY_javascript


## 엑셀 다운로드
for vanilla javascript

```javascript
  
function exportTableToExcel(tableId, filename) {
      let dataType = 'application/vnd.ms-excel';
      let extension = '.xls';

      let base64 = function(s) {
          return window.btoa(unescape(encodeURIComponent(s)))
      };

      let template = '<html xmlns:o="urn:schemas-microsoft-com:office:office" xmlns:x="urn:schemas-microsoft-com:office:excel" xmlns="http://www.w3.org/TR/REC-html40"><head><!--[if gte mso 9]><xml><x:ExcelWorkbook><x:ExcelWorksheets><x:ExcelWorksheet><x:Name>{worksheet}</x:Name><x:WorksheetOptions><x:DisplayGridlines/></x:WorksheetOptions></x:ExcelWorksheet></x:ExcelWorksheets></x:ExcelWorkbook></xml><![endif]--></head><body><table>{table}</table></body></html>';
      let render = function(template, content) {
          return template.replace(/{(\w+)}/g, function(m, p) { return content[p]; });
      };

      let tableElement = document.getElementById(tableId);

      let tableExcel = render(template, {
          worksheet: filename,
          table: tableElement.innerHTML
      });

      filename = filename + extension;

      if (navigator.msSaveOrOpenBlob)
      {
          let blob = new Blob(
              [ '\ufeff', tableExcel ],
              { type: dataType }
          );

          navigator.msSaveOrOpenBlob(blob, filename);
      } else {
          let downloadLink = document.createElement("a");

          document.body.appendChild(downloadLink);

          downloadLink.href = 'data:' + dataType + ';base64,' + base64(tableExcel);

          downloadLink.download = filename;

          downloadLink.click();
      }
  }


```

### sheet.js 사용한 엑셀표 다운

```javascript
function excelFileExport() {
      // step 1. workbook 생성
      let wb = window.XLSX.utils.book_new();

      // step 2. 시트 만들기
      let newWorksheet = excelHandler.getWorksheet();

      // step 3. workbook에 새로만든 워크시트에 이름을 주고 붙인다.
      window.XLSX.utils.book_append_sheet(wb, newWorksheet, excelHandler.getSheetName());

      // step 4. 엑셀 파일 만들기
      let wbout = window.XLSX.write(wb, {bookType:'xlsx',  type: 'binary'});

      // step 5. 엑셀 파일 내보내기
      window.saveAs(new Blob([s2ab(wbout)],{type:"application/octet-stream"}), excelHandler.getExcelFileName());
  }

  const excelHandler = {
      getExcelFileName : function(){
          return 'table_'+'test.xlsx';
      },
      getSheetName : function(){
          return 'test-1';
      },
      getExcelData : function(){
          return document.getElementById('testTbl');
      },
      getWorksheet : function(){
          return window.XLSX.utils.table_to_sheet(this.getExcelData());
      }
  }

  function s2ab(s) {
      let buf = new ArrayBuffer(s.length); //convert s to arrayBuffer
      let view = new Uint8Array(buf);  //create uint8array as viewer
      for (let i=0; i<s.length; i++) view[i] = s.charCodeAt(i) & 0xFF; //convert to octet
      return buf;
  }
```
