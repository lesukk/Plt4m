1) Потрібно скачати і встановити Jenkins: https://jenkins.io/download/. 
2) Поставити на сервер найновішу версію Jmeter: https://jmeter.apache.org/download_jmeter.cgi та у папку lib/ext додати Jar файли Plugin Manager. Без плагін менеджера Jmeter не зможе тягнути цілі массиви, щоб можна було в подальшому розпарсити і тягнути multiple дані та інше. 

![jmeter](https://i.imgur.com/77XMVRm.png)

3) Проставити опцію Discard old builds і обмежити кількість в 100, щоб не забивати пам'ять сервера. 

![jmeter](https://i.imgur.com/eAgL2cq.png)

Також прописати шлях до workspace де знаходиться проект.

![jmeter](https://i.imgur.com/6YJeoqa.png)

4) Прописати shell/bat файл з командою на старт Jmeter у конфізі Build Environment меню настройок. 

Перший параметр - шлях до Jmeter. 

Другий параметр - шлях до тестуємого файлу JXM. 

Третій параметр - шлях та розширення файлу з логами. 

![jmeter](https://i.imgur.com/2xKtXOz.png)

5) В Post-Build Actions додати нотифікатор (емейл, слак, тощо) і законфіжити його. Критично, щоб був сформований аттачмент. 

![jmeter](https://i.imgur.com/9SjjuQE.png)

6) Настройки Jenkins - Manage Plugins - Available, потрібно вибрати Notification Plugin і встановити з перезагрузкою Jenkins. 

![jmeter](https://i.imgur.com/0FjEYrB.png)

7) Після цього у настройках проекту з'явиться вкладка Job notification, яка потрібна, аби обробити вебхук. Потрібно настроїти відповідно до скріншота. 

![jmeter](https://i.imgur.com/2kJncrh.png)

8) Формування вебхука: 

```
http://<USERNAME>:Controller<HOST>/job/<PROJECT_NAME>/build?token=<TOKEN>
```





Весь флоу виглядає так: 

Вебхук триггериться під час рана пайплайна чи тощо, Jenkins отримує команду розпочати білд, надсилає Jmeterу команду заекзекьютитись, після прогонки результат надсилається на почту (чи інше місце) вкладаючи результат виконання. 


