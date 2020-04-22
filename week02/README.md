# 作业
### 写一个正则表达式 匹配所有 Number 直接量
```
var reg = /[\d]{1,16}|(?:[1-9]+\.[\d]+)|(NaN)|0[xX][1-9a-f]+/
```

### 写一个正则表达式，匹配所有的字符串直接量
```
var quote = /"([^"] *)"/g
```

### 编写一个UTF8 Encoding函数
```
function utf8(str) {
   return hexString(getUTF8Bytes(str));
}
// 将字节流转换成16进制字符串
function hexString(bytes) {
  var arr = bytes.map(function (code) {
    return (code).toString(16).toUpperCase();
  });
  return arr.join(' ');
}
// 获取字符串的utf8字节流
function getUTF8Bytes(str) {
  var bytes = [];
  var len = str.length;
  for (var i = 0; i &lt; len; ++ i) {
    var code = str.charCodeAt(i);
    if (code >= 0x10000 && code &lt; = 0x10ffff) {
      bytes.push((code >> 18) | 0xf0);                // 第一个字节
      bytes.push(((code >> 12) & 0x3f) | 0x80);
      bytes.push(((code >> 6) & 0x3f) | 0x80);
      bytes.push((code & 0x3f) | 0x80);
    } else if (code >= 0x800 && code &lt; = 0xffff) {
      bytes.push((code >> 12) | 0xe0);
      bytes.push(((code >> 6) & 0x3f) | 0x80);
      bytes.push((code & 0x3f) | 0x80);
    } else if (code >= 0x80 && code &lt; = 0x7ff) {
       bytes.push((code >> 6) | 0xc0);
       bytes.push((code & 0x3f) | 0x80);
    } else {
      bytes.push(code)
    }
  }
 
  return bytes;
}
```
