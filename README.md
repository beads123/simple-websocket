# simple-websocket
This repo  is a simple websocket server written by Node.js.As you konws,HTML5 websocket provide us another new way that client side
communicate with server side. In the past,all the clients(browsers) exchange messages with server via HTTP which offer an undirectional
way.For the sake of developing real-time web applicaitons, we created `polling`,`long-polling` and `comet`.However, they are inefficient 
in the present.The good news is that `websocket` is coming!

This repo implemented a websocket server side in Node.js according to the [websocket spec](http://datatracker.ietf.org/doc/rfc6455/?include_text=1).
You can use it with the raw [HTML5 websocket API](https://w3c.github.io/websockets/) such as `ws.onopen`,`ws.onmessage`.It is convinient 
for you to start a websocket app or demo.

#Usage
At first,you must have a [Node](https://nodejs.org/) enviroment in your machine.Then run the following code

    mkdir test
    cd  test
    touch demo.js
in the demo.js,you shoud write the following code
```javascript
var websocket=require("../server");
       websocket.listen(9999,"localhost",function(conn){
       console.log("connection opend");
       conn.on('data',function(opcode,data){
        console.log("message:",data);
        conn.send(data);
     });
    conn.on('close',function(code,reason){
        console.log("connection closed:",code,reason);
      });
});
```
the next step is run this code by typing

    node demo.js
now the websocket server is started in the [localhost:9999](http://localhost:9999),you can use a websocket instance in the client to
communicate with the server.Making a long story short,the `server.js` provide you two methods and two events:

#API
`method1#listen(port,ipaddress,function(conn){})`,the third argument is callback function,its arguments is the socket connection with client.

`method2#send(data)`,this method is called by a connection instance which is the `listen` method 's third argument offer like `conn` in the above

`event#data#conn.on('data',function(opcode,data){})`,in the function,`opcode` is the websocket operation code ,`data` is the incoming
data.

`event#close#conn.on('close',function(cdoe,reason){})`,`code` shows you why this connection is closed, `reason` explain it.
#Test
    cd test
    node demo-server.js
then open the `index.html` in your browser, type data in the input and send it.The server side will print the data and send it back. 





    


