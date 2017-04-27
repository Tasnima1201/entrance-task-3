# Задание 3

Мобилизация.Гифки – сервис для поиска гифок в перерывах между занятиями.

Сервис написан с использованием [bem-components](https://ru.bem.info/platform/libs/bem-components/5.0.0/).

Работа избранного в оффлайне реализована с помощью технологии [Service Worker](https://developer.mozilla.org/ru/docs/Web/API/Service_Worker_API/Using_Service_Workers).

Для поиска изображений используется [API сервиса Giphy](https://github.com/Giphy/GiphyAPI).

В браузерах, не поддерживающих сервис-воркеры, приложение так же должно корректно работать, 
за исключением возможности работы в оффлайне.

## Структура проекта

  * `gifs.html` – точка входа
  * `assets` – статические файлы проекта
  * `vendor` –  статические файлы внешних библиотек
  * `service-worker.js` – скрипт сервис-воркера

Открывать `gifs.html` нужно с помощью локального веб-сервера – не как файл. 
Это можно сделать с помощью встроенного в WebStorm/Idea веб-сервера, с помощью простого сервера
из состава PHP или Python. Можно воспользоваться и любым другим способом.

## Ответы на вопросы
Вопрос 1. self.skipWaiting() позволяет перейти к этапу активации, оставив остальные запросы в установке выполняться асинхронно. После того, как мы внесли в кэш все необходимое, можно перейти к этапу активации, и теперь не будут возникать ошибки с доступом к кэшу.
Вопрос 2. self.clientsClaim(): клиентские страницы не нуждается в перезагрузке прежде чем могут быть использованы сервис воркером.
Вопрос 5. Так как объекты Response могут быть использованы только один раз.


## Внесенные изменения

По заданию после последнего рефакторинга "ServiceWorker перестал обрабатывать запросы за ресурсами приложения: HTML-страницей, скриптами и стилями из каталогов vendor и assets". Так как скрипт сервис-воркера `service-worker.js` находился в папке `assets`, то под контролем сервис-воркера оказалась только эта папка, и ресурсы вне ее не обрабатывались. При переносе скрипта в общую папку ресурсы стали правильно кэшироваться и отображаться в оффлайн режиме.
Также была обнаружена проблема: при переходе на главную страницу после добавления гифки в favorites и отключения интернета, добавленные файлы не кэшировались. В `blogs.js` был подправлен метод отправки сообщения сервис-воркеру. 
