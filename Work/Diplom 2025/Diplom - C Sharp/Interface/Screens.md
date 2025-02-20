
___
App: [[Application - C Sharp|Application - C Sharp]]
___

- Home (Домашний экран с навигацией и дочерними окнами; Access: All) 

##### **Navigation screens:**

###### **Authorization** (Авторизация; Access: Guest):
- SIgn-in (Экран входа) 
- Sign-up (Экран регистрации)  

###### **Work** (Работа):
- Create ticket (Экран создания заявки; Access: Client, Admin, ASU_staff)
- My tickets (Экран моих созданных заявок; Access: Client, Admin, ASU_staff) 
- Available  tickets (Экран с новыми заявками и принятие их; Access: ASU_staff, Admin) 
- My assigned tickets (Экран с принятыми заявками; Access: ASU_staff, Admin)

###### **Reports** (Отчеты; Access: ASU_staff, Admin):
- Create reports (Экран создания отчетов)
- My reports (Экран с созданными мной отчетами и кнопка перехода к их редактированию)
- All reports (Экран со всеми отчетами и фильтрами; если пользователь является админом, то включить кнопку управления отчетами)

###### **Administration** (Администрирование; Access: Admin):
- Users (Управление пользователями, навигация и дочернии окна):
	- All users (Экран с пользователями и кнопка перехода к редактированию) 
	- Create user  (Экран создания пользователя) 
- Roles (Управление ролями, навигация и дочернии окна):
	- All roles (Экран с ролями и кнопка перехода к редактированию) 
	- Create roles  (Экран создания роли) 
- Tickets (Управление заявками, навигация и дочернии окна):
	- All tickets (Экран с заявками и фильтрами и кнопка перехода к редактированию)
- Statuses (Управление статусами, навигация и дочернии окна):
	- Create statuses  (Экран создания статусов)
	- View, update and delete statuses (Экран редактирования и удаления статусов)
- Priorities (Управление приоритетами, навигация и дочернии окна):
	- Create priorities  (Экран создания приоритетов)
	- View, update and delete priorities (Экран редактирования и удаления приоритетов)
- Comments (Управление коментариями, навигация и дочернии окна):
	- All comments (Экран с коментариями и фильтры и кнопка перехода к редактированию)
- Departments (Управление отделами, навигация и дочернии окна):
	- Create Departments  (Экран создания отделов) 
	- All departments (Экран с отделами и кнопка перехода к редактированию) 

##### **Not navigation screens:**

- My ticket and comments for tickets (Экран с заявкой, с коментариями и  создание коментариев; Access: Client, Admin, ASU_staff)
- Update roles (Экран редактирования ролей; Access: Admin) 
- Update users (Экран редактирования пользователей; Access: Admin) 
- Edit my profile (Изменение моего профиля; Access: Client, ASU_staff, Admin) 
- Update department (Экран редактирования отделов; Access: ASU_staff, Admin) 
- Update reports (Экран редактирования отчетов; Access: ASU_staff, Admin)
- My statistics (Моя статистика; Access: Client, ASU_staff, Admin)
- Settings DB (Настройка БД; Access: Guest) 
- Update ticket (Редактирование заявок работниками; Access: ASU_staff, Admin)
- Dialog (Окно вывода уведомлений; Access: All)