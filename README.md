# Типо ТЗ, но не совсем

## Введение

Action DDB - это mongodb с actions.
Action DDB стала нужна для удобной настройки project/task manager КпЦ.

Задачи (task) - это те же документы, но с полем статуса
выполнения, которое может быть абсолютно разным в зависимости
от настроек системы, плюс функционал project/task manager может часто меняться
от проекта к проекту, поэтому лучше обобщить project/task manager до такой
базы данных.

При этом в Action DDB никаких task-ов не используется.
Project/task manager был упомянут лишь для указания мотивации\актуальности
создания данного продукта (Action DDB).

### Action

Actions - это что-то вроде GitHub Actions.

Actions должны предоставить возможность пользователям, например: ввести
систему рейтинга,
чтобы за каждую выполненную задачу человеку что-то начислялось,
а за плохие действия списывалось; ввести ограничение на время выполнения задач;
ввести последовательность в выполнении задач, позволив образовывать
цепочки задач, то есть обязать выполнить, например, первую задачу перед второй;
встроить какую-ту автоматическую проверку задач; или встроить автоматическое
наполнение описания задач чем-то и т.д.

## Карта документации

[Правила команды разработки](DevRules.md)

## Техническая часть

Action DDB - это CLI программа.

"|" означает "или".

### Вход/регистрация пользователя

`sign up \<user-name> \<user-email>` \<user-password>

`sign in \<user-name>|\<user-email>` \<user-password>

`sign out`

### Collection

`collection in \<collection-id>|\<collection-name>` начинает работу с коллекцией.

`collection out` завершает работу с коллекцией.

`create collection`

`create collection \<collection-name>`

`edit collection description \<edited-collection-description-file>`

`edit collection action \<edited-collection-action-file>`

`run \<command>`

`\<command>` имеет mongodb синтакс, только без db и названия коллекции вначале.
Например, вместо `db.testDb.insertOne...` `insertOne...`.

### Action

filename.action

```yml
before:
# команды zsh, которые выполняются до выполнения команды от пользователя.

after:
# команды zsh, которые выполняются после выполнения команды от пользователя.
```
Каждая строчка содержит одну команду.

Команды action имеют доступ к данным пользователя, отправившего команду,
а также к самой команде.
