# NodeJSOrganization
NodeJS를 정리하는 저장소입니다.

# Modeuls

## URL Module

https://www.google.co.kr/search?newwindow=1&dcr=0&source=hp&ei=ceoLWoiRPISu8QWg-on4BQ&q=node&oq=node

* protocol: https
* host: www.google.co.kr/search
* query: newwindow=1&dcr=0&source=hp&ei=ceoLWoiRPISu8QWg-on4BQ&q=node&oq=node

| Method | Description |
| --- | --- |
| `parse()` | 주소 문자열을 파싱하여 URL 객체를 만들어 리턴
| `format()` | URL객체를 주소 문자열로 변환

```javascript
var url = require('url');

var googleURL = url.parse('https://www.google.co.kr/search?newwindow=1&dcr=0&source=hp&ei=ceoLWoiRPISu8QWg-on4BQ&q=node&oq=node');

var googleURLString = url.format(googleURL);
```

## File Module

### 파일을 읽거나 파일에 쓰기

| Method | Description |
| --- | --- |
| `readFile(filename, [encoding], [callback])` | Async IO로 파일을 읽어 들입니다.
| `readFileSync(filename, [encoding])` | Sync IO로 파일을 읽어 들입니다.
| `writeFile(filename, data, encoding='utf8', [callback])` | Async IO로 파일을 씁니다.
| `writeFileSync(filename, data, encoding='utf8')` | Sync IO로 파일을 씁니다.

```javascript
var fs = require('fs');

fs.readFile('./file', 'utf8', (err, data) => {
  if (err) {
   // error
  } else {
   // success
  }
});

let data = 'Hello ~!';
fs.writeFile('./file.txt', data, (err) => {
  if (err) {
    // error
  } else {
    // success
  }
});
```
### 파일을 직접 열고, 닫으면서 읽거나 쓰기

| Method | Description |
| --- | --- |
| `open(path, flags, [mode], [callback])` | 파일을 엽니다. |
| `read(fd, buffer, offset, length, position, [callback])` | 지정한 부분의 파일 내용을 읽어 들입니다. |
| `write(fd, buffer, offset, length, position, [callback])` | 파일의 지정한 부분에 데이터를 씁니다. |
| `close(fd, [callback])` | 파일을 닫아 줍니다. |

| Flags | Description |
| --- | --- |
| `w` | 읽기에 사용하는 flag, 파일이 없으면 예외가 발생됩니다. |
| `r` | 쓰기에 사용하는 flag, 파일이 없으면 만들어지고, 파일이 있으면 이전 내용을 모두 삭제합니다. |
| `w+` | 읽기와 쓰기에 모두 사용하는 flag, 파일이 없으면 만들어지고, 파일이 있으면 이전 내용을 모두 삭제합니다. |
| `a+` | 읽기와 추가에 모두 사용하는 flag, 파일이 없으면 만들어지고, 파일이 있으면 이전 내용에 새로운 내용을 추가합니다. |


```javascript
// 읽기
var fs = require('fs');

fs.open('./file.txt', 'r', (err, fd) => {
  if (err) throw err;
  
  var buffer = new Buffer(30);
  fs.read(fd, buffer, 0, buffer.length, null, (err, bytesRead, buf) => {
    if (err) throw err;
    let string = buffer.toString('utf8', 0, bytesRead);
    fs.close(fd);
  });
});

```

```javascript
// 쓰기
var fs = require('fs');

fs.open('./file.txt', 'w', (err, fd) => {
  if (err) throw err;
  
  var buffer = new Buffer('Hello');
  fs.write(fd, buffer, 0, buffer.length, null, (err, written, buf) => {
    if (err) throw err;
    fs.close(fd);
  });
});

```

### 스트림 단위로 파일 읽고 쓰기

stream은 데이터가 전달되는 통로같은 개념.

| Method | Description |
| --- | --- |
| `createReadStream(path, [options]` | 파일을 읽기 위한 stream 객체를 만듬 |
| `createWriteStream(path, [options]` | 파일을 쓰기 위한 stream 객체를 만듬 |

```javascript
// 쓰기
var fs = require('fs');

var inputStream = fs.createReadStream('./infile.txt', { flag: 'r' });
var outputStream = fs.createWriteStream('./outfile.txt', { flag: 'w' });

inputStream.on('data', (data) => {
 outputStream.write(data);
});

inputStream.on('end', () => {
 outputStream.end(() => {
   // end
 })
});


// == inputStream.pipe(outputStream);

```

### 새로운 디렉토리 생성, 삭제

```javascript

// 생성
var fs = require('fs');
fs.mkdir('./foler', 0666, (err) => {
 if (err) throw err;
});

```

```javascript

// 삭제
var fs = require('fs');
fs.rmdir('./folder', (err) => {
 if (err) throw error;
});

```
