---
title: Принципы SOLID - вопрос №3 на собеседование по программированию
subtitle: Текст к видео "SOLID - принцип инверсии зависимостей" на канале YouTube
layout: page
show_sidebar: false
menubar: example_menu
author: andrew
category: programming_questions
categories: programming_questions
---

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/mmgzCGGAJ9o" 
frameborder="0" allow="accelerometer; autoplay; 
encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

Сегодня мы погорим о том, что было первым – яйцо или курица. А говоря о программировании, необходимо определить, что от чего должно зависеть в коде. Для того чтобы 
разобраться с этой задачей нам поможет **один из принципов SOLID**, **принцип D**. Это сокращение от английского выражения **Dependency inversion principle**, что в русскоязычной 
литературе называется «**принцип инверсии зависимостей**». Мне не очень нравится этот перевод из-за слова «инверсия», которое можно было заменить на слово «преобразование». 
Или модно было даже пойти дальше и слово «инверсию» назвать «разворотом». В итоге мы бы получили «принцип разворота зависимостей». В любом случае в данный момент это 
всё звучит заумно и не понятно, о чем речь.

Давайте подумаем, как можно написать некоторую функциональность.
 - первым делом необходимо написать техническое задание, описывающее функциональность;
 - далее можно написать псевдокод, то есть описание последовательности действий, характеризующее функциональность человеческим языком; например «получаем данные из базы, 
 обрабатываем данные, записываем данные файл, файл отправляем по электронной почте».
 - псевдокод нам помог определить 4 ключевые элемента нашей функциональности; соответственно нам будут необходимы 4 класса: класс для работы с базами данных, 
 класс для обработки данных, класс работы с файлами, класс для отправки электронных сообщений.
 - пишем 4 класса с конкретной реализацией функциональности
 - объединяем все 4 класса в один класс, где последовательно на объекте каждого класса выполняем 4 операции.

Что мы можем сказать об этом классе? Класс WorkerClass определяет архитектуру нашей функциональности. В принципе функциональность класса WorkerClass могла бы быть 
отдельным консольным приложением. 4 отдельных класса предоставляют определенную функциональность. Можно сказать, что класс WorkerClass определяет структуру функциональности 
или приложения, то есть является элементом высокого уровня. С другой стороны, конкретные реализации функциональности являются элементами низкого уровня, спрятанные где-то 
в недрах нашего приложения. Согласитесь, чтобы понять, как работает наше приложение будет достаточно посмотреть на класс WorkerClass, элемент высокого уровня. Видно, 
какие действия выполняются по порядку и, по сути, нас не очень интересует то, что происходит внутри 4 классов низкого уровня. Общая суть работы функциональности нам понятна.

В литературе по программированию определение принципа D иногда даётся в следующей форме – элементы высокого уровня не могут зависеть от элементов низкого уровня. Оба типа 
элементов должны зависеть от абстракций. А что у нас происходит в классе WorkerClass? Ну, если честно, то WorkerClass, элемент высокого уровня, зависит от элементов низкого 
уровня. Что имеется в виду? Если мы поменяем сигнатуру одного из 4 методов в соответствующем классе низкого уровня, то нам придется внести изменения в класс WorkerClass, а 
конкретно немного изменить метод DoWork. То есть DoWork подвержен изменениям, если изменится один из 4 классов. Или даже один из 4 классов будет заменен на какой-то другой 
класс. Такая крепкая связь между элементами высшего и низшего уровней чревата ошибками в процессе изменений. А как мы уже знаем, изменения — это единственная постоянная вещь 
в жизни программиста. Итак, принцип D нарушен. Как это исправить?

Прежде всего необходимо разбить крепкую связь между элементами высокого уровня и низкого уровня. Для это необходимо использовать абстракции – абстрактные классы или интерфейсы. 
Давайте в данном примере попробуем использовать интерфейсы. В результате WorkerClass класс, элемент высокого уровня, зависит от абстракций, а также конкретные классы, 
элементы низкого уровня, на примере класса FileWriter зависят от абстракций. 

То есть произошло следующее:
 - у нас был код с определённым направлением зависимости: элемент верхнего уровня зависел от 4 элементов низкого уровня;
 - мы, если можно так выразиться, «развернули» зависимость на абстракции: и элемент верхнего уровня, и элемент низкого уровня стали зависеть от абстракций

В этом и заключается суть принципа инверсии зависимостей. Всё в нашем коде должно зависеть от абстракций. Никаких зависимостей от конкретных имплементаций, только зависимость 
от абстрактных классов и интерфейсов.

Обратите внимание на предыдущее **видео о шаблоне проектирования** «**Фабрика**», а конкретно, на шаблон «**Абстрактная фабрика**». Там зависимость всего кода основана на 
интерфейсах дабы не нарушать данный принцип **SOLID**. Если бы наши фабрики ингредиентов зависели от конкретных ингредиентов, то наш код был бы скованным и непригодный к изменениям, 
то есть просто плохим. Использование абстракций позволяет добавлять напитки с разнообразным набором ингредиентов.

Благодарю вас за внимание!