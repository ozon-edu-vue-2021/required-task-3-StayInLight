# 📝 Чек-лист

1) Ознакомьтесь с материалом лекций недели
2) Ознакомьтесь с материалами воркшопа
3) Ознакомьтесь с заданием
4) Создайте ветку `feature/…` и выполните задание в ней
5) Подготовьте PR из ветки `feature/…` в ветку `master`
6) Найдите в таблице прогресса своего тьютора
7) Отправьте личным сообщением своему тьютору ссылку на созданный PR

-----------------------

# Задание: Карта офиса
## Дано
Даны JSON файлы с данными по подразделениям, местам и сотрудникам и svg-изображения.

JSON хранится в `src/assets/data`

Изображения карты и рабочего места в `src/assets/images`


## Делать всем  🦁:

Самостоятельно реализуем сценарий воркшопа:
- нарисовать прототип, 
- сверстать шаблон, 
- вывести на экран svg-карту, 
- отрисовать места и круговую диаграмму с подразделениями компании и количеством занятых мест на карте, 
- реализуем возможность менять очередность списка подразделения в боковом меню (draggable).

## 💎 Посложнее:

 Внесите в проект изменения:
-  Измените цвет, количество и расположение мест в каждом подразделении (обратите внимание, что изменения в файле `tables.json` должны соответствовать значению counter в файле `legend.json`)
-  Реализуйте в диаграмме Pie измененные вами данные по количеству мест в подразделениях

## 💎💎 Для профи:

Реализуйте обработку клика по столу, при котором из json-файла подтягивается пользователь, а в правом сайдбаре выводится информация о том, кто занимает выбранное место. 
Так же, не забудьте обработать клик вне мест, который будет скрывать информацию о человеке.

Референс: https://imgur.com/a/TxLdaDK

Иконки: https://material.io/



