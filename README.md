# NodeJSOrganization
NodeJS를 정리하는 저장소입니다.

# Modeuls

## File Module


| Method | Description |
| --- | --- |
| `readFile(filename, [encoding], [callback]) | Async IO로 파일을 읽어 들입니다.
| `readFileSync(filename, [encoding]) | Sync IO로 파일을 읽어 들입니다.
| `writeFile(filename, data, encoding='utf8', [callback]) | Async IO로 파일을 씁니다.
| `writeFileSync(filename, data, encoding='utf8') | Sync IO로 파일을 씁니다.

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

```javascript

var fs = require('fs');

fs.open('./file.txt', 'w', (err, fd) {
  if (err) throw err;
  
  var buffer = new Buffer('Hello');
  fs.write(fd, buffer, buffer.length, null, (err, written, buf) => {
    if (err) throw err;
      fs.close(fd);
  });
});

```
