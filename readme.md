1) установить ORACLE_11G_R2 
2) подключиться к СУБД ( например под пользователем SYS )
3) добавить пользователей : SOME, RTL_A, RTL_B
4) открыть файл \DB_install.sql
5) выполнить секцию "/* --== SET UP PRIVILEGE ==-- */" 
6) залогиниться RTL_A, выполнить секцию "/* BEFORE create user 'SOME' AFTER => */", аналогично для RTL_B
7) подключаемся под SOME, выполняем в пакетном режиме секции "/* DROP ALL */" и "/* --== SET UP DDL ==-- */"
8) в секции "/* --==TRIGGER==-- */" каждый запрос выполняем по одному
9) Проверяем что нет invalid объекто СУБД, если есть то начинаем с первого пункта
10) открываем \add_data.sql, выполняем в пакетном режиме
11) открываем \TRANSMIT_CUSTOMER_TO_A.sql, выполняем
12) теперь у нас есть процедура, и есть тестовый набор, смотрим содержимое таблиц :
SELECT * FROM rtl_b.customer;
SELECT * FROM rtl_a.customer;
13) делаем 
SQL> EXEC TRANSMIT_CUSTOMER_TO_A
если всё хорпошо то получаем : 
PL/SQL procedure successfully completed
14) снова смотрим :
SELECT * FROM rtl_b.customer;
SELECT * FROM rtl_a.customer;
15) Профит ! ( из rtl_b в rtl_a передался Печкин);
16) можно посмотреть 
SELECT * FROM RTL_B.CUSTOMER_SYNCHRONIZE
для Почтальон видим статус "SUCCESS".