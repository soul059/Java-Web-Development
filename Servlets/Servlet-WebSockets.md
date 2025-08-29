# WebSockets in Java

WebSockets provide a full-duplex communication channel over a single TCP connection, allowing for real-time, bidirectional communication between a client and a server. The Java API for WebSocket (`JSR 356`) provides a standard way to create WebSocket endpoints in Java applications.

## Creating a WebSocket Endpoint

To create a WebSocket endpoint, you need to create a class and annotate it with `@ServerEndpoint`. This annotation specifies the URL at which the endpoint will be available.

```java
@ServerEndpoint("/websocket")
public class MyWebSocket {
    // ...
}
```

## WebSocket Lifecycle

The lifecycle of a WebSocket endpoint is managed through a set of annotations:

-   `@OnOpen`: Called when a new WebSocket connection is established.
-   `@OnMessage`: Called when a message is received from the client.
-   `@OnClose`: Called when the WebSocket connection is closed.
-   `@OnError`: Called when an error occurs.

### Example: Echo Endpoint

This example demonstrates a simple WebSocket endpoint that echoes messages back to the client.

```java
import javax.websocket.OnClose;
import javax.websocket.OnError;
import javax.websocket.OnMessage;
import javax.websocket.OnOpen;
import javax.websocket.Session;
import javax.websocket.server.ServerEndpoint;

@ServerEndpoint("/echo")
public class EchoEndpoint {

    @OnOpen
    public void onOpen(Session session) {
        System.out.println("WebSocket opened: " + session.getId());
    }

    @OnMessage
    public void onMessage(String message, Session session) {
        System.out.println("Message received: " + message);
        try {
            session.getBasicRemote().sendText("Echo: " + message);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    @OnClose
    public void onClose(Session session) {
        System.out.println("WebSocket closed: " + session.getId());
    }

    @OnError
    public void onError(Throwable error) {
        error.printStackTrace();
    }
}
```
