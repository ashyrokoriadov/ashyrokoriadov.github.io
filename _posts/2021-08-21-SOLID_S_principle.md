---
title: Принципы SOLID - вопрос №2 на собеседование по программированию
subtitle: Текст к видео "SOLID - принцип единственной ответственности" на канале YouTube
layout: page
show_sidebar: false
menubar: example_menu
author: andrew
category: programming_questions
categories: programming_questions
---

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/t1cB-Jegfig" 
frameborder="0" allow="accelerometer; autoplay; 
encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

В предыдущем видео мы рассматривали **шаблон проектирования** «**Стратегия**». В качестве практического примера был использован класс «Калькулятор» с 4 основными математическими 
операциями, который зависит от интерфейса «ILoggingStrategy». Данный интерфейс отвечает за логирование математических операций. Давайте подумаем, а почему, собственно, 
мы написали наш код именно таким образом – класс «Калькулятор» с отдельной зависимостью для логирования. Ведь можно было логику логирования добавить в класс «Калькулятор». 
Да, это было можно сделать. Давайте проанализируем к чему это могло привести.

Итак, у нас есть класс «Калькулятор» с логикой логирования. Пусть это будет логика связанная с логированием в базу данных. В итоге калькулятор работает, считает, а также 
логирует посчитанные операции в базу данных. Вроде бы всё нормально. До поры, до времени. Через какое-то время нашему отделу, который отвечает за класс «Калькулятор» 
поступило 2 требования: одно от бизнесс – аналитиков, а второе от технического отдела.

Рассмотрим требование от бизнесс-аналитков – необходимо немного изменить логику умножения. Теперь необходимо каждое произведение двух чисел умножать на 2. Не проблема. 
Метод Multiply в классе «Калькулятор» был изменен. 

Второе требование было от технического отдела – теперь мы логируем математические операции не в базу данных, а в файл. Логика логирования была изменена в классе «Калькулятор». 
Теперь выполняя математические операции, данные о таких операций попадают не в базу данных, а в файл.

После выполнения этих 2 требований поступило замечание от отдела тестирования – данные не всегда попадают в файл, а иногда результат умножения не увеличивается в 2 раза. 
Для того чтобы развеять все сомнения наш отдел принял решение написать юнит-тесты. Вообще-то с этого стоило начать еще перед написание класса «Калькулятор», но это уже 
друга история, которая называется «**TDD**» или «**Test Driven Development**», о которой будет отдельное видео.

Начали мы писать юнит-тесты, но оказалось следующее. В данный момент логирование происходит в файл. Если приложение, которое запускает тесты, имеет доступ к пути 
файла логов, то тесты проходят – так сказать «тесты зеленые», однако если приложение не имеет доступа к пути файла логов, то тесты светятся красным цветом, не проходят. 
Есть проблема – результат теста зависит не только от правильности операций, но и от наличия или отсутствия доступа к файлу логов. Одно из требований к юнит-тестам это 
изоляция, то есть тест не должен от чего-то зависеть, а в данном случае он зависит от доступа к пути файла лога. Ситуация не была лучше до изменений – тогда результат 
теста зависел бы от наличия доступа к базе данных. То есть получается нормальных юнит-тестов при такой имплементации мы не напишем.

Вот в такую ситуацию мы попали:
 - юнит тесты написать нельзя, точнее можно, но они не будут отвечать требованию изоляции;
 - во время изменения логики умножения мы возможно что-то испортили с логикой логирования;
 - или во время изменения логирования с базы данных на файл, мы что-то испортили в логике умножения

Этот пример прекрасно описывает, что бывает, когда не соблюдается **первый принцип SOLID** – **принцип S** или **принцип единственной ответственности** «**Single Responsibility**». 
Как сформулирован этот принцип – «У вас должен быть только один повод для изменения класса».

Давай посмотрим еще раз на текущее состояние класса «Калькулятор» - он выполняет математические операции и записывает данные в лог. У этого класса 2 ответственности: 
расчеты и логирование. У этого класса соответственно 2 повода для внесения изменений: либо изменение калькуляций, либо изменение логики логирования. **Принцип S** нарушен, 
а следствия нарушения данного принципа описаны ранее:
 - трудности в написании качественных юнит-тестов
 - изменения одной функциональности могут повлиять на другие функциональности, определенные в данном классе.

Если вы видите очень большой класс, где происходят разные вещи, то есть реализованы разные функциональности, то скорей всего этот класс нарушает принцип «единственной 
ответственности» и скорей всего изменение чего-либо в данном классе может привести к ошибкам. К тому же скорей всего данный класс не имеет юнит-тестов, а если они есть, 
то скорей всего, их качество оставляет желать лучшего. Это частая проблема если вы работает со старым кодом, так сказать «legacy» кодом. Раньше на соблюдение принципов 
SOLID особо не обращали внимание, хотя некоторые из этих принципов были сформулированы в конце 80-х годов. 

Вообще **принципы SOLID** это обязательное условие качественного кода, но, к сожалению, к этому утверждению многие программисты и команды программистов приходят через метод 
проб и ошибок. **SOLID** – это аббревиатура, которая состоит из первых букв принципов качественного программного обеспечения. В этом видео мы знакомимся с первый принципом – 
принципом единственной ответственности. В последующих видео будут раскрыты остальные принципы. 

Принципы SOLID хорошо описывать вместе с конкретными шаблонами проектирования. И именно этой возможностью я сейчас пользуюсь. В предыдущем видео мы увидели шаблон 
«Стратегия» в действии и вы, наверное, уже догадались, что данный шаблон проектирования активно эксплуатирует принцип единственной ответственности. Напомню – у нас 
есть калькулятор, который отвечает только за математические операции, и есть классы стратегий логирования, которые отвечают только за логирования. Каждый из этих 
классов имеет только один повод для изменений. Изменения в одном из этих классов не влияют на работу других классов – наши изменения изолированы и не генерируют 
побочных ошибок.

К тому же благодаря именно такой реализации **примера шаблона** «**Стратегия**» мы можем легко написать юнит-тесты. Для класса «Калькулятор» мы проверяем правильность 
вычислений, в качества стратегии логирования передаётся Mock-объект, который не влияет на результат теста. Также можно легко написать тесты для каждой из 
стратегий.

Итого, благодаря **принципу S** у нас есть следующие преимущества:
 - классы легко протестировать заменив зависимости Mock-объектами;
 - изменения в классах с единственной ответственностью изолированы друг от друга, а значит такие изменения легче выполнить;
 - изменения в конкретном классе можно протестировать юнит-тестами;

Стоит также сказать, что соблюдение принципа единственной ответственности имеет один минус. У вас может появиться много маленьких классов в коде и на первый взгляд 
ваш код может показаться громоздким с большим количеством файлов. Однако важно понимать – лучше много маленьких классов, чем один большой класс.

Подводя итог можно сказать, что сегодня мы познакомились с **первым принципом SOLID**, а также повторили **шаблон проектирования** «**Стратегия**», что даже очень неплохо.

Благодарю вас за внимание!