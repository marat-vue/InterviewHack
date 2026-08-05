# Как совместить Better Auth с authorization в NestJS?

> [!NOTE]
> Better Auth решает authentication и session management, но бизнес-authorization все равно нужно проектировать в приложении: roles, permissions, ownership checks и policies.

## Authentication vs authorization

Better Auth отвечает на вопрос:

```txt
Кто пользователь и валидна ли его session?
```

Authorization отвечает:

```txt
Может ли этот пользователь выполнить действие?
```

## Проверка владельца ресурса

```ts
@Get('orders/:id')
async findOrder(
  @Param('id') id: string,
  @Session() session: UserSession,
) {
  return this.ordersService.findForUser(id, session.user.id);
}
```

Service должен проверить, что заказ принадлежит пользователю.

## RolesGuard поверх session

```ts
@Roles('admin')
@Get('admin')
getAdminData() {}
```

Guard может читать session user и metadata roles.

## Мини-шпаргалка

- Better Auth дает session.
- Authorization - отдельный слой приложения.
- Ownership checks лучше делать в service/use case.
- Roles подходят для грубых прав.
- Для сложных прав нужны policies/permissions.
