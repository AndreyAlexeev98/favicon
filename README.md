__Необходимо дополнение кейса по статье - https://habr.com/ru/articles/672844/__

# Кейс подключения favicon к проекту.

- Файл favicon.ico лежащий в корне проекта, будет автоматически подключен браузерам в проекте как favorite icon (иконка для избранного). Браузеры делают запрос в корень сайта и пытаются найти там файл в формате .ico. Чтобы переопределить это дефолтное поведение браузера, в `<head>` html документа необходимо указать ссылку на favicon -  `<link rel="icon" href="/assets/favicon.ico">`
- apple в первом айфоне выпустили свой браузер - safari. Они перестали искать жутко неоптимизированный файл в формате .ico, и добавили возможность использовать png. Данный файл необходимо положить в конень сайта с названием - apple-touch-icon. Данную иконку видно в избранном, и при добавлении на домашний экран. Все нюансы по использовани favicon на touch устройствах описаны в кусоводстке Матиаса Беннеса- https://mathiasbynens.be/notes/touch-icons.
- В HTML5 ввели стандарт link rel="icon" - `<link rel="icon" href="/assets/favicon.png" sizes="16x16" type="image/png">`, этот способ имеет расширенное описание, влючает в себя `sizes` для указания размера файла и `type` для формата. Еслт ico с несколькими иконками внутри, то все размеры нужно указать через пробел в sizes="16x16 32x32". Если иконка векторная - `<link rel="icon" href="/assets/favicon.svg" sizes="any" type="image/svg+xml">` - то размер `any`.
- Чтобы собрать все описания fav иконок проекта, используют файл manifest.webmanifest. Подключается - `<link rel="manifest" href="/manifest.webmanifest">`. Это простой JSON файл, в котором можно указать помимо всех иконок, их размеры и форматы, но и полностью описать ваше приложение (фирменный цвет, цвет фона, язык и направление письма, полное и краткое название, ориентация, режим запуска и прочее). Но webmanifest - это пока больше мобильная история, для андроидов. 
- `<link rel="mask-icon" href="mask.svg" color="tomato">` - для закрепленных вкладок в сафари и кнопок на touch bar макбуков - указывается монохромная векторная маска и цвет, для анведения.

## Резюме
### Необходимый минимум для большинства устройств:
1. Забываем про формат ico (если не поддерживаем IE10)
2. Для браузерных строк и закладок на ПК -  подключаем линком 2 иконки - для обычных мониторов:
`<link rel="icon" href="/assets/16x16.png" sizes="16x16" type="image/png">`
 и ретины: 
`<link rel="icon" href="/assets/32x32.png" sizes="32x32" type="image/png">`
3. Для apple touch устройств - из корня сайта подключаем `<link rel="apple-touch-icon" href="/apple-touch-icon.png">` размером исходника 180×180.
4. Для андроидов подключаем webmanifest - `<link rel="manifest" href="/manifest.webmanifest">`. В самом файле (Тут важная иконка 192-192px. И тут же можно задать цвета, название. Всё равно пригодится.)