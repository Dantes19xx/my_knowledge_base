#ИБ

Структура [[LDAP]]-каталога выглядит так:

![](https://pictures.s3.yandex.net/resources/image_6_1730839536.png)

Данные здесь представлены в виде иерархии объектов. Каждый объект — это запись. Древовидная структура, которую образуют объекты, называется «информационным деревом каталога» (Data Information Tree, DIT).

- **Корневой элемент (Root)** — это наивысший уровень иерархии, который представляет всю директорию.
- **DC (Domain Component)** — это компоненты домена, которые указывают на доменные имена. Например, `dc=example` и `dc=com`.
- **OU (Organizational Unit)** — это организационные единицы, которые используют для группировки объектов внутри домена. Например, `ou=sale, dc=example, dc=com` может представлять отдел продаж в домене `example.com`. Обратите внимание: организационные единицы могут быть вложенными друг в друга. Например, `ou=Developers,ou=IT,ou=Staff`.
- **CN (Common Name)** — это общие имена, которые используют для идентификации объектов в каталоге. Обычно за ними скрываются пользователи или ресурсы. Например, в записи `cn=John Doe, ou=marketing, dc=example, dc=com` общее имя — это `cn=John Doe`.
- **DN (Distinguished Name)** — это полный путь к объекту. Например, `cn=John Smith,ou=Developers,ou=IT,dc=example,dc=com`. Порядок компонентов в полном пути имеет значение. Ещё важно знать, что DN всегда уникален в рамках дерева — такой полный путь один на всю директорию.
- **RDN (Relative Distinguished Name)** — это относительное имя объекта. Оно является частью DN (полного пути к объекту). RDN уникален только в рамках родительского элемента.
- **Атрибуты (Attributes)** — это характеристики объекта. Например, имя, email, телефон. Регистр для атрибутов не имеет значения. Поэтому `dc=example` эквивалентно `DC=example`. Список атрибутов, которые используют чаще всего:

```
Идентификация
uid: уникальный идентификатор
cn: общее имя
sn: фамилия
givenName: имя
displayName: отображаемое имя

Контактная информация:
mail: email адрес
telephoneNumber: телефон
mobile: мобильный телефон
postalAddress: почтовый адрес

Организационная информация:
title: должность
manager: DN руководителя
departmentNumber: номер отдела
employeeNumber: табельный номер
employeeType: тип сотрудника
```

- **Объектные классы** — это шаблоны с набором атрибутов. Они определяют, какие атрибуты может или должен иметь объект.

```
Например, основные объектные классы:

person:
  - обязательные: cn, sn
  - опциональные: userPassword, telephoneNumber, seeAlso, description

organizationalPerson (наследует person):
  + title, street, postalCode, postOfficeBox

inetOrgPerson (наследует organizationalPerson):
  + mail, givenName, uid, manager, departmentNumber

groupOfNames:
  - обязательные: cn, member
  - опциональные: description, owner

organization:
  - обязательные: o
  - опциональные: description, postalAddress, telephoneNumber
```

Пример информационного дерева каталога для `example.com`:

![](https://pictures.s3.yandex.net/resources/image_7_1730839566.png)

Для RDN можно использовать разные атрибуты. Не только `cn`, `ou` и `dc`.

