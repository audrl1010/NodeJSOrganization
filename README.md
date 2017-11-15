# NodeJSOrganization
NodeJS를 정리하는 저장소입니다.

# Modeuls

## File Module


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






