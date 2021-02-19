---
title: Что такое delegate - вопрос №16 на собеседование C# / .NET
subtitle: Текст к видео "Что такое delegate" на канале YouTube
layout: page
show_sidebar: false
menubar: example_menu
author: andrew
category: c_sharp_questions
categories: c_sharp_questions
---

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/lCfxl5pOF-s" 
frameborder="0" allow="accelerometer; autoplay; 
encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

На данном этапе подготовки к собеседованию кандидат уже должен понимать чем является переменная и как приписать ей значение. **Язык C#** явялется языком с сильной типизацией, 
то есть всегда известен тип переменной, а значит известно какие значения мы можем приписать к данной переменной. Работая с переменным может возникнуть ряд вопросов:

1.	Можно ли создать такую переменную, к которой в качестве значения будет приписана ссылка на метод?
2.	Можно ли к такой переменной приписать любой метод?
3.	Можно ли к такой переменной приписать несколько методов?
4.	Как такую переменную можно использовать и что будет являться результатом этого использования?
5.	Существуют ли в языке C# предопределенные переменные такого типа?

Ответим по порядку на каждый из этих вопросов.

**Ответ на вопрос 1.** Да, можно создать переменную, к которой можно приписать ссылку на метод. В языке C# такая переменная будет называться **делегатом**. Расширяя определение делегата, данное в 
предыдущем предложении, стоит сказать что при декларировании делегата необходимо указать сигнатуру метода, который можно будет приписать данному делегату. **Сигнатурой метода** 
называется определенный набор аргументов метода по типу, количеству и порядку. В одном из предыдуших видео, посвященному ключевым словам при наследовании, я ошибся, сказав, 
что в сигнатуру метода входит также и тип возвращаемого значения. Исправляю свою ошибку – в сигнатуру метода тип возвращаемого значения не входит.

```javascript
public delegate void LogMathOperation(int x, int y);

static void Main(string[] args)
{
	LogMathOperation additionWithLogging = AddWithLogging;
	LogMathOperation subtractionWithLogging = SubtractWithLogging;
	LogMathOperation multiplyWithLogging = MultiplyWithLogging;
	LogMathOperation divideWithLogging = DivideWithLogging;

	additionWithLogging(10, 5);
	subtractionWithLogging(10, 5);
	multiplyWithLogging(10, 5);
	divideWithLogging(10, 5);

	Console.ReadKey();
}

static void AddWithLogging(int x, int y) => Console.WriteLine($"{x} + {y} = {x + y}");

static void SubtractWithLogging(int x, int y) => Console.WriteLine($"{x} - {y} = {x - y}");

static void MultiplyWithLogging(int x, int y) => Console.WriteLine($"{x} * {y} = {x * y}");

static void DivideWithLogging(int x, int y) => Console.WriteLine($"{x} / {y} = {(y == 0 ? 0 : x / y)}");
```

Ответ на вопрос 2. Исходя из вышесказанного, к **делегату нельзя приписать** любой метод. К делегату может быть приписан метод, который имеет сигнатуру соответствующую сигнатуре делегата.

Ответ на вопрос 3. Да, к **делегату можно приписать** несколько методов которые имеют соответсвующую сигнатуру. В этой же ситуации некоторые или все методы можно «отписать» от делегата.

```javascript
LogMathOperation allDelegates1 = additionWithLogging + subtractionWithLogging + multiplyWithLogging + divideWithLogging;
allDelegates1(30, 6);

LogMathOperation allDelegates2 = additionWithLogging;
allDelegates2 += subtractionWithLogging;
allDelegates2 += multiplyWithLogging;
allDelegates2 += divideWithLogging;
allDelegates2(30, 6);

//вычитание делегата
allDelegates2 -= divideWithLogging;

//будут выполнены все операции кроме деления
allDelegates2(30, 6); 
```

Ответ на вопрос 4. **Делегат** является переменной, которая содержит указатель на методы или методы. Соответственно используя делегат мы можем вызывать методы, указатели на которые содержит делегат. 
Результатом использования делегата будет выполнение метода и, если необходимо, возвращение результата выполнения метода.

Ответ на вопрос 5. Да, в языке C# существуют **предопределенные делегаты**. Перед их более детальным рассмотрением, подумаем зачем они были созданы. В обычной ситуации созданный делегат будет 
использоваться скорей всего в одном месте в коде, использование его повсеместно будет затруднено в силу его узкой специализации или специфического названия, которое может 
не подходить к некоторым контекстам. В связи с этим часто бывают ситуации, когда имя делегата по сути не важно, но важно чтобы был определенный делегат с определенной 
сигнатурой. С этой целью возникли  предопределенные делегаты – существуют 2 большие группы таких делегатов **Action** и **Func**. Это обобщенные делегаты, которые могут принимать 
до 16-ти типовых параметров. Отличие этих групп состоит в следующем – делегаты **Action** соответствуют методам, которые не возвращают значения (то есть возвращают void), а 
делегаты **Func** соответствуют методам, которые возвращают значение. Последней типовой параметр в делегате **Func** – это тип возвращаемого значения.

```javascript
//Action<int, int> соответствует методу void SomeMethod(int x, int y)
//Func<int, int, int> соответствует методу int SomeAnotherMethod(int x, int y)

static void PerformOperationWithLogging(Action<int, int> operatorWithLogging, int x, int y) 
=> operatorWithLogging(x, y);

static int PerformOperation(Func<int, int, int> operation, int x, int y) => operation (x, y);

static void Main(string[] args)
{
	PerformOperationWithLogging(AddWithLogging, 50, 10);
	Console.WriteLine();
	var addResult = PerformOperation(Add, 60, 5);
	Console.WriteLine(addResult);
	Console.ReadKey();
}
```


 