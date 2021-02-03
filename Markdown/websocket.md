# Web Socket

- 一种在单个TCP连接上进行全双工通信的协议.
- 有需求需要我们在客户端不发起通信的时候，由服务器端发送，此时就需要websocket.

## readyState 属性返回实例对象的当前状态

- CONNECTING：值为0，表示正在连接。
- OPEN：值为1，表示连接成功，可以通信了。
- CLOSING：值为2，表示连接正在关闭。
- CLOSED：值为3，表示连接已经关闭，或者打开连接失败。

## onopen 用于指定连接成功后的回调函数

## onclose 用于指定连接关闭后的回调函数

## onmessage 用于指定收到服务器数据后的回调函数

```js
var ws = new WebSocket("wss://echo.websocket.org");

ws.onopen = function(evt) { 
  console.log("Connection open ..."); 
  ws.send("Hello WebSockets!");
};

ws.onmessage = function(evt) {
  console.log( "Received Message: " + evt.data);
  ws.close();
};

ws.onclose = function(evt) {
  console.log("Connection closed.");
};
ws.onerror = function() {
console.log('Connection error')
}
```

## vue中使用

```js
init() {
    let url = 'wss://finance.allhome.com.cn/scanCodeLogin'
    // 创建websocket连接
    this.websock = new WebSocket(url);
    // 监听打开
    this.websock.onopen= this.websockOpen;
    // 监听关闭
    this.websock.onclose = this.websockClose;
    //监听异常
    this.websock.onerror = this.websockError;
    //监听服务器发送的消息
    this.websock.onmessage = this.websockMessage;
},
websockOpen() {
    console.log('监听打开')
},
websockClose() {
	console.log('监听关闭)
},
websockError() {
	console.log('监听异常')
},
websockMessage（e） {
	console.log('监听服务器发送的消息'，e.data)
}

```

## send 实例对象的send()方法用于向服务器发送数据

- 遇见的坑: 长连接 在长时间不发送消息的时候，会自动断开。原因是运维那块使用了nginx服务,会配置一个时间段， 在这个时间里，如果一直灭有数据的传输，连接就会在这个时间之后自动关闭。因为我们无法控制用户什么时候去触发websocket消息的推送。：

- 解决方案: **心跳保持连接**:实现心跳检测的思路是： 每隔固定的时间，发送一个数据到服务器，服务器接收之后，返回一个数据给客户端。如果客户端onmessage事件能监听到返回的数据，则表示连接未断开。否则，表示连接断开，需要客户端去重新发送请求进行连接。

```js
start() {
    // 发送心跳
    clearInterval(this.timeoutObj)
    this.timeoutObj = setInterval(() => {
        let date = new Date()
        this.webSocket.send(`发送心跳给后端${date}`)
    }, 2 * 60 * 1000)
}
```

