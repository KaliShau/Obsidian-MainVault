
___
Entities: [[Work/Diplom 2025/Diplom - C Sharp/DB/Entities and attributes|Entities and attributes]]
___

- **Users** 1-to-Many **Tickets** (Один клиент может создать много заявок).
- **Users** 1-to-Many **Tickets** (Один сотрудник может выполнять много заявок).
- **Roles** 1-to-Many **Users** (У одной роли может быть много пользователей).
- **Statuses** 1-to-Many **Tickets** (Один статус может быть у многих заявок).
- **Priorities** 1-to-Many **Tickets** (Один приоритет может быть у многих заявок).
- **Tickets** 1-to-Many **Comments** (У одной заявки может быть много комментариев).
- **Users** 1-to-Many **Comments** (Один пользователь может оставить много комментариев).
- **Users** Many-to-Many **Departments** (Связь через таблицу `User_Departments`: один пользователь может быть в нескольких отделах и наоборот)
- **Users** 1-to-Many **Reports** (Один пользователь может создать много отчетов)