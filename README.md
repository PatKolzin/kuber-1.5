

# Домашнее задание к занятию «Сетевое взаимодействие в K8S. Часть 2»


### Задание 1. Создать Deployment приложений backend и frontend

1. Создать Deployment приложения _frontend_ из образа nginx с количеством реплик 3 шт.
2. Создать Deployment приложения _backend_ из образа multitool.
3. Добавить Service, которые обеспечат доступ к обоим приложениям внутри кластера. 
4. Продемонстрировать, что приложения видят друг друга с помощью Service.
5. Предоставить манифесты Deployment и Service в решении, а также скриншоты или вывод команды п.4.

------

### Задание 2. Создать Ingress и обеспечить доступ к приложениям снаружи кластера

1. Включить Ingress-controller в MicroK8S.
2. Создать Ingress, обеспечивающий доступ снаружи по IP-адресу кластера MicroK8S так, чтобы при запросе только по адресу открывался _frontend_ а при добавлении /api - _backend_.
3. Продемонстрировать доступ с помощью браузера или `curl` с локального компьютера.
4. Предоставить манифесты и скриншоты или вывод команды п.2.

------

### Задание 1. Создать Deployment приложений backend и frontend

1. Для выполнения задания создам отдельный Namespace. Пишу манифест Deployment приложения _frontend_ из образа nginx с количеством реплик 3 шт:

![2](https://github.com/user-attachments/assets/6b07818d-877e-49a9-bdf5-09767a19e476)

2. Пишу манифест Deployment приложения _backend_ из образа multitool:

![3](https://github.com/user-attachments/assets/c0338ee4-93c8-4aa5-a4cc-ef35011c6d1a)

Проверю созданные поды:

![4](https://github.com/user-attachments/assets/1f7ad226-8feb-415a-847d-f5e530bbe037)

Поды созданы, количество реплик соответствуют заданию.

3. Пишу манифест Service, который обеспечит доступ к обоим приложениям внутри кластера:

![6](https://github.com/user-attachments/assets/66109f73-039e-4760-a757-21f751ad245f)

4. Используя curl, проверю, видят ли приложения друг друга через созданный сервис из пода backend:

![7](https://github.com/user-attachments/assets/afdda067-27f2-464a-8d8e-59d574952c7a)

Приложения видят друг друга.

5. [Манифест Deployment c frontend](https://github.com/PatKolzin/kuber-1.5/blob/main/src/deploy_front.yaml)

   [Манифест Deployment c backend](https://github.com/PatKolzin/kuber-1.5/blob/main/src/deploy_back.yaml)

   [Манифест Service](https://github.com/PatKolzin/kuber-1.5/blob/main/src/service.yaml)

------

