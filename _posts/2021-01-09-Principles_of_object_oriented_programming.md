---
title: Принципы ООП - вопрос №3 на собеседование C# / .NET
subtitle: Текст к видео "Принципы объектно-ориентированного программирования" на канале YouTube
layout: page
show_sidebar: false
menubar: example_menu
author: andrew
category: c_sharp_questions
categories: c_sharp_questions
---

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/EcLdg15t9pI" 
frameborder="0" allow="accelerometer; autoplay; 
encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

Прежде чем отвечать на вопрос о 3 **принципах объектно-ориентированного программирования (ООП)** необходимо объяснить, что из себя представляет **ООП**. 
Объяснение уже заложено в определении – программирование, которое ориентировано на объекты. Развивая эту мысль, мы можем сказать, что это такой способ программирования, 
при котором наша работа сконцентрирована на объектах и работе с ними. Хорошо, понятно. То есть чтобы закрыть для себя вопрос, что есть **ООП** необходимо выяснить, 
что понимается под определением «объект». Под *объектом* в ООП понимается некая сущность (иногда называемая инстанцией класса), которая является представителем 
определенного класса. То есть, *все объекты являются представителями определенных классов*. Например, телевизор — это представитель класса бытовая техника, 
а лев – это представитель класса животные. На данном этапе возникает справедливый вопрос, а чем является класс? Класс — это совокупность параметров, 
которые характеризуются и описывают объект – представитель класса. Исходя из этого в **объектно-ориентированном программировании** мы работаем с объектами 
представителями определенных классов, мы можем использовать уже готовые классы и создавать объекты, которые их представляют ли создавать свои собственные 
классы и использовать их в нашей работе. То есть, по сути, взаимодействие в нашей программе является взаимодействием объектов – представителей различных классов.

Отвечая очень кратко и скупо на вопрос о 3 принципах ООП можно назвать 3 термина: **инкапсуляция**, **наследование**, **полиморфизм**. Рассмотрим каждый их этих терминов в деталях.

Начнем с **инкапсуляции**, которая сводится к сокрытию специфики кода класса. Почему некоторые детали класса необходимо скрывать от конечного пользователя класса? 
Ответ очень прост – конечного пользователя интересует конкретная функциональность, а не детали её работы. **Инкапсуляция** позволяет показать 
конечному пользователю класса функциональность и данные, которые действительно ему будут необходимы для выполнения определенных задач. Также скрывая детали имплементации
 класса, мы защищаем объекты нашего класса от несанкционированного изменения их состояния, что могло бы повлиять на их функциональность. В видео, посвященном разнице между 
 объектами и классами, я использовал пример телевизора и его внутреннего устройства. Инкапсуляция сводится к тому, что нас не интересует некоторые детали конструкции телевизора, 
 чтобы пользоваться телевизором. Какие были использованы конденсаторы и резисторы в телевизоре не влияет на то, как мы будем использовать телевизор. Так и в **ООП**, используя 
 инкапсуляцию, мы выставляем на внешний мир только то, что действительно необходимо пользователям нашего класса.
 
Вторым принципом ООП является **наследование**. Давайте на секундочку подумаем, что может называться **наследованием** вообще и наследование в программировании в частности. 
Наследованием вообще может называться переход определенных свойств от родителя к наследнику, то есть ребенку. При наследовании в программировании имеет место подобная 
ситуация – имея определенный класс - родитель мы можем создать новый класс - наследник, который унаследует всё свойства класса-родителя и который может (но не должен) иметь 
дополнительные свойства и функциональность. В данном случае возникает отношение **«B является А»**, если класс В наследует по классу А. По сути класс В получает всё свойства 
класса А. Также возможно существование другого отношения между классами А и В - «В имеет А». В этом случае класс В не наследует по классу А, а только содержит в себе 
объект класса А. Отношении «В имеет А» не имеет ничего общего с наследованием и им не является.

 Для лучшего понимания наследования и вариантов различных отношений, которые могут выстраиваться между классов, приведу два примера. Класс «Телевизор» может наследовать 
 класс «Бытовая техника», так же, как и класс «Холодильник» может наследовать класс «Бытовая техника». Справедливыми будут утверждения «Телевизор является бытовой техникой» 
 и «Холодильник является бытовой техникой». В классе «Холодильник» может быть, но не обязательно, функциональность «Морозильная камера». Как можно догадаться «Морозильная 
 камера» это отдельный класс. Если в классе «Холодильник» есть объект «Морозильная камера», то справедливо будет утверждение «Холодильник имеет морозильную камеру». 
 Естественно, в данном случае класс «Холодильник» не наследует класс «Морозильная камера», а только имеет в своем определении объект класса «Морозильная камера», и это не 
 является наследованием.
 
Последний в списке, но не последний по значению, принцип ООП – это **полиморфизм**. Что значит это слово? Слово состоит из двух частей греческого происхождения. 
Первая часть «поли» - означает «много», а вторая «морф» - означает «жизнь». То есть мы имеем дело с чем-то, что имеет «много жизней». Надо признать, что это не лучшее объяснение. 
Однако если мы посмотрим на «жизнь», как на поведение объекта и набор его определенных свойств, то можно утверждать, что «полиморфизм» — это свойство объекта определенного класса 
быть использованным как объект другого класса. То есть кроме своих собственных свойств («собственной жизни») объекта, объект может иметь определенные свойства, которые позволят 
относиться к нему, как к объекту другого класса («чужая жизнь»). По моему данному объяснение все еще остается запутанным и для полной ясности осталось понять, что это за другой 
класс в предыдущем предложении. Всё становится ясным, когда мы вспомним предыдущий, второй принцип ООП – наследование. Имеем 2 класса: «А» и «В». «В» наследует «А». То есть 
справедливо утверждение «В является А». Утверждение «В является В» также является справедливым. То есть объект класса «В» может быть использован как объект класса «А» и как 
объект класса «В». В этом свойстве проявляется **полиморфизм** класса «В» - упрощая, объект класса «В» одновременно является объектом класса «А» и объектом класса «В». Итого, у 
объекта «В» есть 2 «жизни» - «А» и «В». Но слово «поли» означает «много», а не «два» («дуо» на греческом языке), где это множество «жизней»? 
Представим ситуацию – появился класс «С» который наследует класс «В». То есть появилась следующая цепочка наследования: класс «С» наследует класс «В», класс «В» наследует класс 
«А». Является ли объект класса «С» объектом класса «А»? Да, является. Почему? Класс «В» унаследовал все характеристики класса «А», а класс «С» унаследовал все характеристики 
класса «В», то есть все характеристики класса «А» и какие-то собственные характеристики класса «В». То есть у объекта «С» есть 3 «жизни» - «А», «В» и собственная «С». Отсюда 
следует вывод – количество жизней, а технически более точно, количество способов использования объекта определенного класса является количество классов в цепочке наследования 
данного класса.

Допустим, с определением **«полиморфизм»** мы разобрались. Но где и как это используется? С инкапсуляцией и наследованием всё понятно – первое укрывает то, что не существенно для 
пользователя, а второе позволяет проще создавать новые классы. А что с **полиморфизмом**? Объясним это на примере. Дано – класс «Животное», который умеет делать только одну вещь – 
двигаться. Класс «Животное» наследуют 3 класса: «Птица», «Рыба», «Сухопутное млекопитающее». Каждый из 3 перечисленных классов получает от своего родителя, класса «Животное», 
функциональность «двигаться», но реализует её по-своему. «Птица» летает, «Рыба» плавает, «Сухопутное млекопитающее» ходит на лапах. Допустим у нас есть набор, состоящий из 
одного объекта каждого класса: «Орел», «Акула» и «Лев». Мы можем заставить двигаться эти объекты обращаясь к каждому из этих объектов и выполняя соответствующую команду «лети», 
«плыви», «беги». Но зная, что каждый из этих объектов является объектом класса «Животное», мы можем упростить задачу и выполнить универсальную команду «двигайся». Нам важно 
чтобы эти объекты начали перемещение, а не то, как эти объекты будут фактически передвигаться (лев побежит, акула поплывёт, а орёл полетит). Использование классов-родителей 
(или, более грамотно, базовых классов) и **полиморфизма** позволяет избежать дублирования кода и даёт возможность упростить код, одновременно улучшая его понимание при чтении кода 
другими программистами.
