# Как работать с WebSocket client и server events?

> [!NOTE]
> В NestJS gateway может реагировать на подключение, отключение и входящие события клиента. Для этого используют lifecycle interfaces и decorators `@ConnectedSocket`, `@MessageBody`, `@SubscribeMessage`.

## Connection lifecycle

```ts
@WebSocketGateway()
export class ChatGateway implements OnGatewayConnection, OnGatewayDisconnect {
  handleConnection(client: Socket) {
    console.log('connected', client.id);
  }

  handleDisconnect(client: Socket) {
    console.log('disconnected', client.id);
  }
}
```

## Message handler

```ts
@SubscribeMessage('join-room')
handleJoin(
  @ConnectedSocket() client: Socket,
  @MessageBody() roomId: string,
) {
  client.join(roomId);
}
```

## Отправка события

```ts
@WebSocketServer()
server: Server;

notify(roomId: string, payload: unknown) {
  this.server.to(roomId).emit('notification', payload);
}
```

## Мини-шпаргалка

- `handleConnection` вызывается при подключении.
- `handleDisconnect` вызывается при отключении.
- `@ConnectedSocket` дает socket.
- `@WebSocketServer` дает server instance.
- Для auth в WS нужны отдельные решения handshake/token.
