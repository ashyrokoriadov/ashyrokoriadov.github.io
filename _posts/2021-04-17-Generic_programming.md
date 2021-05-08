---
title: Обобщенное программирование - вопрос №23 на собеседование C# / .NET
subtitle: Текст к видео "Обобщенное программирование в языке C#" на канале YouTube
layout: page
show_sidebar: false
menubar: example_menu
author: andrew
category: c_sharp_questions
categories: c_sharp_questions
---

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/PnMRa9WQkXg" 
frameborder="0" allow="accelerometer; autoplay; 
encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

Иногда в практике программирования можно столкнуться с ситуацией, когда несколько классов имплементируют подобную функциональность и единственное, чем отличаются эти классы – 
это различные типы аргументов и возвращаемых значений. Рассмотрим эту ситуацию на примере двух классов, которые имплементируют алгоритм сложения.
```javascript
class CalculatorInt
{
	public int Add(int x, int y) => x + y;
} 

class CalculatorDouble
{
	public double Add(double x, double y) => x + y;
} 
```
По сути, это одинаковые классы с одинаковой функциональностью и одинаковым алгоритмом за исключением типа используемых значений. Этот пример достаточно простой, но если мы 
представим реальные приложения, которые состоят не из нескольких строчек, а из несколько сотен тысяч строчек кода, то обслуживание такого кода, который дублирует свою 
функциональность будет очень проблематичным. Лучшим решением этой ситуации будет избавиться от этого когда. Давайте рассмотрим какие варианты нам дает язык C# и среда 
программирования .Net.

**1.	Использование аргументов и возвращаемых значений типа object**

Если мы используем этот подход, то наш класс будет выглядеть следующим образом:
```javascript
class Calculator
{
	public object Add(object x, object y, bool isDouble) 
	{
		if(isDouble)
			return  (double) x + (double) y 
		else
			return (int) x + (int) y
	}
} 
```
Стоит признать, что это не идеальное решение, но оно работает. У нас было 2 класса, а теперь 1 и в этом преимущество данного решения. Однако кроме видимых недостатков, 
таких как необходимость передавать третий аргумент isDouble, это решение имеет недостатки, которые могут быть незаметны на первый взгляд.

Давайте еще раз проанализируем наш код. Вместо стандартных значений значимых типов мы используем объект, то есть ссылочный тип. Как вы уже знаете из моего видео на канале о 
значимых и ссылочных типах, данные типы хранятся в памяти по-разному. Ссылка на данное видео будет в верхнем правом углу. Чтобы воспользоваться методом Add мы должны привести 
аргументы x и y к типу object. То есть взять значимые типы x и y из стека и упаковать их в ссылочный тип object, то есть положить переменные x и y на кучу в памяти. Данная 
процедура называется в программировании **boxing**’ом. А процедура обратного получения наших переменных из объекта называется **unboxing**’ом. Именно это и происходит в коде, когда 
мы получаем наши значения x и y для сложения из переменной типа object. В данной процедуре есть еще один недостаток – при **unboxing**’е мы всегда должны указать тип, к которому 
мы приводим результат. Если переменная, которая хранится в типе object, будет иметь другой тип, то мы получим исключение типа **InvalidCastException** и стоит заметить, что это 
исключение появится слишком поздно – уже когда программа будет работать. При компиляции наша среда программирования (например, Visual Studio) не сообщит нам о потенциальной 
ошибке. На это всегда следует обращать внимание. Кроме того, операции **boxing** и **unboxing** затратны для ресурсов компьютера. Конечно, если вы делаете одну такую операцию в 
минуту, то вы ничего не заметите, но, если ваше приложение будет выполнять тысячи операций связанных с boxing и unboxing — это явно отразится на производительности приложения. 
Какой отсюда следует вывод? Метод с использованием объекта типа object для решения задачи, поставленной в начале урока, нам не подходит. 

**2.	Использование ключевого слова is**

В этом методе мы попробуем избавиться от потенциального **InvalidCastException**, однако по-прежнему будем использовать в качестве типа аргумента и возвращаемого значения тип object. 
Наш класс будет выглядеть следующим образом:
```javascript
class Calculator
{
	public object Add(object x, object y)
	{
		if (x is double xDouble && y is double yDouble)
			return xDouble + yDouble;

		if (x is int xInt && y is int yInt)
			return xInt + yInt;

		return 0;
	}
}
```
В данной имплементации мы нивелировали возможность возникновения InvalidCastException. Если в качестве аргумента будет передано значения типа отличного от double или int, 
то метод просто возвратит значение 0, но ошибки не будет. Теперь давайте проанализируем как мы это достигли. Мы использовали ключевое слово **is** – использование данного 
ключевого слова похоже на вопрос на английском языке: является ли переменная Х типа Y. Данный вопрос имеет только 2 варианта ответа: да или нет, то есть по программному: 
true или false. Поскольку данный оператор возвращает значение типа bool, мы можем использовать его в операторе if. Также у оператора **is** есть еще одно полезное свойство: 
если оператор возвращает значение true, то мы сразу можем привести значение переменной к типу, который мы проверяли. Именно поэтому новые переменные xDouble и yDouble 
являются переменными типа double, а xInt и yInt переменными типа int.

Иногда оператор **is** путают с оператором **as**, который имеют подобную функцию, но его синтаксис немного другой по сравнению с оператором is. **Оператор as** используется 
следующим образом:
```javascript
var SomeClassValue = someUnknownTypeObject as SomeClass;
```
Что здесь происходит – у нас есть некоторый объект someUnknownTypeObject и мы хотели бы привести его к типу SomeClass, чтобы в результате получить переменную SomeClassValue 
типа SomeClass. Если объект someUnknownTypeObject действительно является объектом типа SomeClass, то переменной SomeClassValue будет приписано значение, приведенное 
к типу SomeClass. Однако если объект someUnknownTypeObject не является объектом типа SomeClass, то переменная SomeClassValue будет null. Важное замечание – 
с оператором **as** может использоваться тип, который может иметь значение null, то есть **оператор as** работает со ссылочными типами. В нашем примере выше он не применим, 
так как и double, и int являются значимыми типами. 

Давайте подведём итог того, что мы уже знаем об операторах **as** и **is**.
 - Оператор is может использоваться с любимыми типами, а оператор as только со значимыми типами;
 - Оператор is возвращает значение типа bool, а также если возвращаемое значение – true, может создать переменную проверяемого типа и приписать ей значение, а оператор as 
если привидение удачно, возвращает объект приведённого типа с определенным значением или, если приведение не удалось, то возвращает null;

Метод с оператором **is** не плохой: мы избавились от потенциального исключения **InvalidCastException**, а также у нас нет видимых проблем с производительностью приложения, 
cвязанных с операциями **boxing** / **unboxing**. Можно было бы на этом остановится, но есть в инструментарии языка C# еще одна особенность, которая идеально подходит для решения 
задачи, которую мы себе поставили.

**3. Обобщенное программирование**

Давайте еще раз посмотрим на первый пример кода и задумаемся, что в этих классах одинаково, а что изменяется. В этих классах одинаков алгоритм – мы берем 2 величины некоторого 
типа и их складываем, возвращаем значение заданного типа. А разным является тип данных, который используется в этих классах. Если мы будем относиться к типу как к переменной, 
то мы сможем записать один из представленных классов следующим образом:
```javascript
class Calculator<T>
{
	public T Add(T x, T y) => x + y;
} 
 ```
В этот момент мы создали с вами **обобщенный класс**, который определяет конкретный алгоритм, не привязанный к какому-либо типу. Сразу стоит оговорится, что если вы скопируете 
этот код в Visual Studio, то он не сработает – компилятор не знает, как складывать 2 обобщённых типа Т и ему необходимо немножко помочь. Как? Я покажу чуть позже. Целью 
данного конкретного примера является показать принцип обобщенного программирования – вы пишите код, где для вас важен алгоритм работы, а не конкретный используемый тип, 
теоретически ваш код может использоваться с любым типом. Чтобы код из предыдущего примера заработал его необходимо немного изменить:
```javascript
class CalculatorGeneric<T>
{
	public T Add(T x, T y)
	{
		dynamic x1 = x;
		dynamic y1 = y;
		return (T)(x1 + y1);
	}
}
 ```
Об использовании **ключевого слова dynamic**, а также **перегрузке математических операторов** у меня будет снято отдельное видео, так что не забывайтесь подписываться на канал и 
нажимать колокольчик, чтобы не пропустить обновления. 

Как использовать этот класс? Также как и обычный класс, единственное что, то при создании класса с ключевым словом new необходимо указать аргумент типа T:
```javascript
var calculator = new CalculatorGeneric<double>();
 ```
Теперь объект класса CalculatorGeneric можно использовать с типом double. Например:
```javascript
double result = calculator.Add(1.4444, 2.6666);
 ```
Тот же объект нельзя использовать с другими типами, например попытка вызвать метод Add с типом decimal обречена на провал: decimal result = calculator.Add(1.4444M, 2.6666M); 
Буква М за каждым из аргументов означает что это величина типа decimal, а не double. Для типа decimal необходимо создать отдельный объект класса CalculatorGeneric, но с 
типом decimal:
```javascript
var calculatorDecimal = new CalculatorGeneric<decimal>();
 ```
Как видите, нам не пришлось создавать новый класс для типа decimal, мы просто создали новый объект того же класса, но с другим параметром типа. Наша задача здесь решена 
полностью: мы уменьшили количество кода (1 класс вместо 2), нет проблем с приведением типов и производительностью, наш код удобен в использовании и обслуживании.

Что следует помнить при использовании обобщенных классов:
 - параметров типа может быть более одного – в нашем конкретном примере мы использовали один параметр для простоты, но нам ничего не мешает создать класс который использует 
несколько параметров типа **SomeGenericClass<T1,T2,T3>**;
 - мы можем оказывать влияние на то, как типы могут использоваться с нашим классом и об этом мы поговорим более подробно далее.

Что касается количества обобщённых типов в классе, то чем их больше тем тяжелее читать и обслуживать код, поэтому совет от программиста – практика: не стоит злоупотреблять 
количество обобщенных типов. Например, если в вашем классе более 3 обобщенных типов, то стоит подумать, как этот класс можно изменить, чтобы уменьшить количество этих типов.

Как мы можем повлиять на используемые обобщенные типы в нашем классе – необходимо использовать специальный синтаксис при декларации класса, например в последнем примере мы 
могли бы написать следующее:
```javascript
class CalculatorGeneric<T> where T : struct
 ```
Новое здесь **where T : struct** – это ограничение типа. В данном случает мы указываем, что типом Т может быть только значимый тип. Как мы уже знаем из одного из видео на моем 
канале, структура – это значимый тип.

У нас может быть обратное ограничение – тип Т должен быть ссылочным. Для этого следует использовать синтаксис со словом **class**:
```javascript
class CalculatorGeneric<T> where T : class
 ```
Иногда может возникать потребность создавать класс типа Т внутри нашего обобщенного класса и при этом один из конструкторов класса типа Т должен быть без параметров, то 
есть что то в стиле **var someObject = new SomeClass()**. В этом случае необходимо использовать ограничение **new()**:
```javascript
class CalculatorGeneric<T> where T : new()
 ```
Но кроме конструктора без параметров, было бы неплохо иметь доступ к каким-либо свойствам или методам объекта типа Т. По факту, если вы попытаетесь проверить, что есть в типе Т, 
то там будут только 4 метода: *Equals*, *ToString*, *GetType*, *GetHashCode* – эти методы доступны наследникам класса Object, то есть всем типам, в том числе и типу Т. Чтобы тип 
Т имел больший функционал, чем только вышеперечисленные 4 метода необходимо указывать ограничение наследования какого-то класса или имплементации како-то конкретного интерфейса. В 
коде это выглядит следующим образом:
```javascript
class CalculatorGeneric<T> where T : IDisposable <имя интерфейса>
class CalculatorGeneric<T> where T : SomeBaseClass <имя класса>
 ```
Также в обобщённых класса можно добавлять ограничения типов от друг друга, например
```javascript
class GenericClass<T, U> where T : U
 ```
Тут мы имеем дело с обобщенным классом с двумя обобщенными параметрами типа и один тип Т должен наследовать другой тип U.

Иногда можно встретиться с вопросом на собеседовании – как имплементировать **метод Dispose** в обобщенном классе. Давайте подумаем вместе.
 - метод **void Dispose()** является единственным членом интерфейса **IDisposable**, значит наш обобщенный класс должен имплементировать данный интерфейс;
 - если мы имплементируем метод Dispose, то наверное надо попробовать вызвать этот метод на каждом из объектов обобщенного типа, если это имеет смысл, например если данный 
объект отражает состояние. Как мы можем это достичь – например наложить ограничение чтобы каждый тип Т используемый в нашем обобщенном классе должен имплементировать 
интерфейс IDisposable, то есть **where T : IDisposable**.