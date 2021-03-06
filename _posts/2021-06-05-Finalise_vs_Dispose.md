---
title: Разница между Finalize и Dispose в C# - вопрос №30 на собеседование C# / .NET
subtitle: Текст к видео "Разница между Finalize и Dispose в C#" на канале YouTube
layout: page
show_sidebar: false
menubar: example_menu
author: andrew
category: c_sharp_questions
categories: c_sharp_questions
---

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/ZSVXmb_K4F0" 
frameborder="0" allow="accelerometer; autoplay; 
encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

В одном из предыдущих видео, выпущенных на канале посвященных работе **Garbage Collector** в среде программирования .Net мы познакомились как происходит очистка памяти от 
неиспользованных объектов. **Garbage Collector** идеально работает, когда речь идет о ресурсах в управляемом коде. Однако если речь идет о неуправляемом коде, то освобождать 
такие ресурсы необходимо явно, без надежды на какие-то волшебные механизмы, которые выполнят данную полезную работу за нас. К неуправляемым ресурсам можно отнести 
соединения с базами данных, сетевые соединения, файлы, а также прочие элементы, которые мы используем в программирования .Net, но которые не являются частью .Net.

Для того, чтобы решить данную проблему в языке C# введено понятие **финализации**. В общем виде финализации позволяет объекту освободить ресурсы, которые он использует 
перед тем, как он будет очищен **Garbage Collector’ом**.  **Декларирование финализатора** похоже на декларирование конструктора, но перед названием необходимо добавить знак 
«тильда»:

```javascript
public class ClassWithFinalizer
{
	~ ClassWithFinalizer()
	{
		// освобождение ресурсов
	}
}
```
Одним из недостатков использования финализаторов является то, что мы не знаем точно, когда он будет вызван. То есть мы знаем, что **финализатор** будет вызван, когда 
**Garbage Collector** будет удалять наш объект из памяти, но опять-таки, мы не можем сказать, когда это произойдёт. Конечно, некоторые могут сказать – вызови статический 
метод **GC.Collect()** и дело сделано, однако Garbage Collector это доработанный и проверенный временем механизм и если у нас есть возможность не вмешиваться в его работу, 
то лучше конечно этой возможностью воспользоваться.

Если всё-таки нам пришлось воспользоваться методом **GC.Collect()**, то не будет лишним после вызова этого метода, вызвать метод **GC.WaitForPendingFinalizers()** чтобы все 
финализаторы закончили свою работу.

Вторым недостатком финализатора является то, что **объект с финализатором** помещается в специальную **очередь финализации**. Что это значит? Это значит, что на наш объект будет 
существовать ссылка в памяти в некоторой очереди, а как мы уже знаем Garbage Collector чистит память от объектов, на которые нет ссылок. Отсюда следует вывод – использование 
финализаторов и размещение объектов в очереди финализации увеличивает жизненный цикл объекта и откладывает удаление объекта из памяти.

Давайте рассмотрим некоторый пример. Есть объект, который работает с файлом. В объекте есть финализатор, который закрывает файл и освобождает данный ресурс. В итоге если 
мы работаем с файлом при помощи нашего объекта, то ожидание пока в системе не будет вызван Garbage Collector чтобы закрыть файл, является не идеальным и очень слабым техническим 
решением.

Естественное в среде программирования .Net уже есть решение данной проблемы. Решение тривиально – оно сводится к имплементации интерфейса **IDisposable**. Интерфейс **IDisposable** 
содержит декларацию только одного метода: **Dispose**, который не принимает ни одного аргумента и не возвращает значений. В рамках данного метода можно освободить неуправляемые 
ресурсы немедленно и это метод может быть вызван каждым пользователем вашего класса.

С использованием интерфейса **IDisposable** не всё идеально, как могло бы быть. Если во время вызова метода **Dispose** и далее во время его работы возникнет ошибка и будет выброшено 
исключение могут возникнуть проблемы – некоторый ресурс не будет освобожден. Чтобы этого избежать все типы, которые имплементируют **IDisposable** должны быть вызваны с обработкой 
исключений **try/finally** – об обработке исключение у меня снято видео на канале, ссылка будет в правом верхнем углу. Так как такой синтаксис является, по сути, обязательным 
создатели языка C# предоставили нам специальный синтаксис для решение данной задачи – использование ключевого слова **using** в контексте объектов, которые имплементируют интерфейс 
**IDisposable**, например:

```javascript
using (var connection = new SqlConenction())
{
	//операции с объектом connection
}
```

Ключевое слово **using** в этом случае гарантирует, что после использования данного объекта будет вызван метод **Dispose**, а в случае исключений они будут обработаны соответствующим 
образом. Использование **using** автоматически добавляет к коду инструкции **try/finally**. Если программист хотел бы расширить этот синтаксис и использовать блок **catch**, то связку 
**try/catch/finally** необходимо будет написать самостоятельно.

На собеседовании может появиться вопрос – *какая разница между использованием финализаторов и использованием интерфейса IDisposable*. Принимая во внимание всю информацию, которую 
вы узнали в данном видео, можно ответить, что финализаторы вызываются Garbage Collector’ом и у нас нет особых рычагов влияния, когда это произойдет, с другой стороны, если 
объект имплементирует IDisposable, то после использования объекта, мы можем явно освободить ресурсы из кода, вызывая метод Dispose, когда объект, по нашему мнению, уже 
не нужен.

В данном видео мы уделили достаточно внимания вопросу управления памятью. Я бы хотел сказать еще пару слов об одном аспекте связанным с памятью, который важен настолько, 
чтобы о нём сказать, но не настолько, чтобы о нём снимать отдельное видео. Речь идет о слабых ссылках или на языке оригинала – **WeakReference**. По умолчанию ссылки в памяти 
на наши объекты являются строгими или сильными (кому какое название нравится). Некоторые объекты могут занимать в памяти достаточно большое количество места, и, хотя, в 
коде на них будут строгие ссылки, данные объекты могут не использоваться очень часто. Если мы обнаружили такой объект, большой и не часто используемый, то это наш кандидат 
**для слабой ссылки**. Если на объект указывает слабая ссылка, то такой объект может быть удален Garbage Collector’ом, несмотря на наличие ссылки, пусть даже и слабой. 
Дополнительным условием для объекта со слабой ссылкой является то, чтобы такой объект можно было быстро и легко создать. В этом случае алгоритм работы приложения с 
объектами со слабыми ссылками будет выглядеть следующим образом:

1. Нужен большой объект – создай его со слабой ссылкой.
1. Используй данный объект.
1. Через некоторое время – если объект не был удален Garbage Collector’ом, то используй существующий объект, а если объект был удален – создай его повторно.
Таким образом у нас есть доступ к объекту, и мы оптимально расходуем ресурсы памяти. С другой стороны, это половинчатое решение – есть и другие механизмы работы с 
памятью, например использование кэша, однако данная логика должны быть создана программистом самостоятельно.