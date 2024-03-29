# Задание 1 — найди ошибки

В этом репозитории находятся материалы тестового задания "Найди ошибки" для [14-й Школы разработки интерфейсов](https://academy.yandex.ru/events/frontend/shri_msk-2018-2) (осень 2018, Москва, Санкт-Петербург, Симферополь).

Для работы тестового приложения нужен Node.JS v9. В проекте используются [Yandex Maps API](https://tech.yandex.ru/maps/doc/jsapi/2.1/quick-start/index-docpage/) и [ChartJS](http://www.chartjs.org).

## Задание

Код содержит ошибки разной степени критичности. Некоторые из них — стилистические, а другие — даже не позволят вам запустить приложение. Вам нужно найти все ошибки и исправить их.

Пункты для самопроверки:

1. Приложение должно успешно запускаться.
1. По адресу http://localhost:9000 должна открываться карта с метками.
1. Должна правильно работать вся функциональность, перечисленная в условиях задания.
1. Не должно быть лишнего кода.
1. Все должно быть в едином codestyle.

## Запуск

```
npm i
npm start
```

При каждом запуске тестовые данные генерируются заново случайным образом.


Описание задания
BUG#1: не правильный импорт в файле index.js
    Проект не запускался, в консоле выводилась ошибка.
    варианты решения либо изменить запись импорта либо добавить default кдюч к экспортируемой фунции из map.js
BUG#2: задал ширину #map-элемента(карта не отображалась)
    Открыл браузер глянул в консоль, ошибок не было глянул в html-разметку выявил что элемент 0 на 0 пикселей, в аттрибуте style прописал размеры элемента
    (При описании решения перенест стили в index.css)
BUG#3: не отображались 'балуны'
    Просматривая примеры работы с менеджером объектов (objectManager) понял что не хватает функции добавляющей объекты на карту.
    После добавления геоОбъектов на карте все равно ничего не отображалось, подставил фейковые данные, работает -> ошибка в данных -> поменял долготу и широту в маппере местами -> РАБОТАЕТ!
BUG#4: не отображались доли в 'балунах'
    Закоментировал строку которая устанавливат цвет для круговой диаграммы кластера
BUG#5: проблема с отображением подсказки
    не окрывалась подсказка, в консоли была ошибка.
    поставил брейкпоинты в методах build и clear
    код валился на строке
    ```BalloonContentLayout.superclass.build.call(this);```
    указатель this был undefined, после исправил стрелочные функции на обычное функциональное выражение
BUG#6: не правильная настройка графика нагруженности
    При открытии детальной информации графики были путые
    Просмотрел данные для конкретной станции, выявил что они выше максимально допустимой точки в настройках карты, после чего убрал настройку.