

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

1. Для выполнения задания создаю отдельный Namespace. Пишу манифест Deployment приложения _frontend_ из образа nginx с количеством реплик 3 шт и Service для него, а также пишу манифест Deployment приложения _backend_ из образа multitool и Service для него, применяю созданные манифесты:

![image](https://github.com/user-attachments/assets/7d07cb28-10eb-4751-8106-cbd25abb2e87)

Проверю созданные поды:

![image](https://github.com/user-attachments/assets/9ebce3cf-a00a-45c8-829b-b5d4c48e1f3b)


Поды созданы, количество реплик соответствуют заданию.

3. Используя curl, проверю, видят ли приложения друг друга через созданные сервисы из подов frontend'а и backend'а:

![image](https://github.com/user-attachments/assets/8ae48ec6-cb60-423f-aa1e-a00ed9c1e13f)

Приложения видят друг друга.

5. Манифест - [Deployment c frontend и service](https://github.com/PatKolzin/kuber-1.5/blob/main/src/front-deploy.yaml)

   Манифест - [Deployment c backend и service](https://github.com/PatKolzin/kuber-1.5/blob/main/src/back-deploy.yaml)

------

### 2. Создать Ingress и обеспечить доступ к приложениям снаружи кластера

1. Включаю Ingress-controller в MicroK8S. Проверю его состояние:

![image](https://github.com/user-attachments/assets/51376222-0347-4512-9c9a-b6d0d712c70c)

Ingress-controller запущен.

2. Пишу манифест Ingress, обеспечивающий доступ снаружи по IP-адресу кластера MicroK8S так, чтобы при запросе только по адресу открывался _frontend_ а при добавлении /api - _backend_.

Применю манифест и проверю результат:

![image](https://github.com/user-attachments/assets/81d01aae-c99e-4866-a8ae-71ad98005c7e)

Ingress создан.

3. Для проверки доступа с помощью браузера или `curl` с локального компьютера, добавлю в DNS соответствующую запись так, чтобы примененный в Ingress адрес myingress.com ссылался на IP адрес кластера MicroK8S.

Проверяю доступ к приложениям через Ingress с помощью браузера или `curl` с локального компьютера:

![image](https://github.com/user-attachments/assets/da7d8b9d-aec5-4140-93b0-7e4ef7de0abe)
![image](https://github.com/user-attachments/assets/75d29668-7df2-4da1-9ed2-27e2b1263893)
![image](https://github.com/user-attachments/assets/82b74554-754d-43ff-824d-b1fd776e52ff)

При обращении к http://172.19.211.199 - получаю ответ от Nginx, при обращении к http://172.19.211.199/api получаю ответ от Multitool.

4. Манифест - [Ingress](https://github.com/PatKolzin/kuber-1.5/blob/main/src/ingress.yaml)
