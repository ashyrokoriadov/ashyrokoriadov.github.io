---
title: Продвинутые функции языка C# - вопрос №26 на собеседование C# / .NET
subtitle: Текст к видео "Продвинутые функции языка C#" на канале YouTube
layout: page
show_sidebar: false
menubar: example_menu
author: andrew
category: c_sharp_questions
categories: c_sharp_questions
---

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/kDQNQCcM9iU" 
frameborder="0" allow="accelerometer; autoplay; 
encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

**Язык C#** имеет богатый синтаксис и широкие возможности. Одну и ту же задачу можно решить несколькими способами. Сегодня мы рассмотрим несколько особенностей языка, 
которые могут использованы для решения нестандартных задач. Мы познакомимся с 

 - использованием индексов
 - переопределением операторов
 - продвинутой конверсией типов
 
Как правило, на собеседовании данные вопросы не обсуждаются. Изредка может появиться вопрос о том, что можно указать в **интерфейсе**. Ответ достаточно прост: методы, 
свойства, события и индексы. И обычно после этого вопроса, следуют дополнительные вопросы – пример одного из таких вопросов: **что такое индекс**. Это мы разберем 
сегодня в первой части нашего видео.

На данном этапе все уже знают, что к элементам массива или списка можно обращаться по их порядковому номеру, то есть по аргументу типа int:

```javascript
var array = new [] {"Item A", "Item B", "Item C"};
var item = array[1]; // item = Item B
```

По индексу 1 мы получаем второй элемент таблицы "Item B". Предположим, у нас есть класс, который содержит внутреннюю коллекцию – можем ли мы получить доступ к 
элементам этой коллекции используя индексы? Давай рассмотрим эту ситуацию на конкретном примере.

```javascript
class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("ПРИМЕР 1. Индексы.");

            var x = new NamedValue("X", 2.54M);
            var y = new NamedValue("Y", 3.46M);
            var z = new NamedValue("Z", 3.46M);

            var data = new[] { x, y };

            var typeWithIndex = new TypeWithIndex(data);

          
            Console.WriteLine("\nИспользование индекса по свойству Name.");
            Console.WriteLine(typeWithIndex["X"]); // 2.54
            Console.WriteLine(typeWithIndex["Y"]); // 3.46
            Console.WriteLine(typeWithIndex["Z"]); // 0
          
            Console.WriteLine("\nИспользование индекса по свойству Value.");
            Console.WriteLine(typeWithIndex[2.54M]); // X
            Console.WriteLine(typeWithIndex[3.46M]); // Y
            Console.WriteLine(typeWithIndex[0M]); // Z
              
            Console.WriteLine("\nИспользование метода поиска по свойству Name.");
            Console.WriteLine(typeWithIndex.GetByName("X")); // 2.54
            Console.WriteLine(typeWithIndex.GetByName("Y")); // 3.46
            Console.WriteLine(typeWithIndex.GetByName("Z")); // 0

            Console.WriteLine("\nИспользование метода поиска по свойству Value.");
            Console.WriteLine(typeWithIndex.GetByValue(2.54M)); // X
            Console.WriteLine(typeWithIndex.GetByValue(3.46M)); // Y
            Console.WriteLine(typeWithIndex.GetByValue(0M)); // Z
          

            Console.ReadKey();
        }
    }
	
internal class NamedValue
	{
		public NamedValue(string name, decimal value)
		{
			Name = name;
			Value = value;
		}

		public string Name { get; set; }

		public decimal Value { get; set; }


		public static NamedValue operator +(NamedValue x, NamedValue y) => new NamedValue($"{x.Name} + {y.Name}", x.Value + y.Value);

		public static NamedValue operator -(NamedValue x, NamedValue y) => new NamedValue($"{x.Name} - {y.Name}", x.Value - y.Value);

		public static NamedValue operator *(NamedValue x, NamedValue y) => new NamedValue($"{x.Name} * {y.Name}", x.Value * y.Value);

		public static NamedValue operator /(NamedValue x, NamedValue y) => new NamedValue($"{x.Name} / {y.Name}", x.Value / y.Value);

		public static bool operator ==(NamedValue x, NamedValue y) => x.Value == y.Value;

		public static bool operator !=(NamedValue x, NamedValue y) => x.Value != y.Value;

		public static bool operator <(NamedValue x, NamedValue y) => x.Value < y.Value;

		public static bool operator >(NamedValue x, NamedValue y) => x.Value > y.Value;

		public static bool operator <=(NamedValue x, NamedValue y) => x.Value <= y.Value;

		public static bool operator >=(NamedValue x, NamedValue y) => x.Value >= y.Value;

		public override string ToString() => $"{Name} = {Value}";

		public override int GetHashCode() => ToString().GetHashCode();

		public override bool Equals(object obj) => ToString().GetHashCode() == obj.GetHashCode();
	}

class TypeWithIndex : ITypeWithIndex
	{
		private readonly IEnumerable<NamedValue> _internalCollection;

		public TypeWithIndex(IEnumerable<NamedValue> data)
		{
			_internalCollection = data;
		}

		public decimal this[string index]
		{
			get => _internalCollection.FirstOrDefault(i => i.Name == index)?.Value ?? 0M;
		}

		public string this[decimal index]
		{
			get => _internalCollection.FirstOrDefault(i => i.Value == index)?.Name ?? "[EMPTY]";
		}

		public decimal GetByName(string name) => _internalCollection.FirstOrDefault(i => i.Name == name)?.Value ?? 0M;

		public string GetByValue(decimal value) => _internalCollection.FirstOrDefault(i => i.Value == value)?.Name ?? "[EMPTY]";
	}

interface ITypeWithIndex
	{
		decimal this[string index] { get; }

		string this[decimal index] { get; }

		decimal GetByName(string name);

		string GetByValue(decimal value);
	}
```

Работая с любым кодом в большинстве языков программирования, мы имеем доступ к различным операторам над величинами, например **арифметические операторы** или **операторы** 
**сравнения**. Если речь идет о типах int, double, decimal то применение к ним арифметических или логических операторов имеет смысл. Однако давайте подумаем имеет ли 
смысл следующий код:

```javascript
var x = new SomeClass();
var y = new SomeClass();
var z = x + y;

class SomeClass { }
```

Если мы не предпримем никаких действий, то данный код даже не скомпилируется, однако если мы используем переопределение операторов, то ситуация будет выглядеть 
иначе. Рассмотрим эту ситуацию на конкретном примере.

```javascript
Console.WriteLine("\nПРИМЕР 2. Перегрузка операторов.");
            
Console.WriteLine($"\nСумма: {x + y}.");
Console.WriteLine($"Разность: {x - y}.");
Console.WriteLine($"Произведение: {x * y}.");
Console.WriteLine($"Частное: {x / y}.");

Console.WriteLine($"\nРавны: {z == y}."); // TRUE
Console.WriteLine($"Не равны: {x != y}."); // TRUE
Console.WriteLine($"Больше: {x > y}."); //FALSE
Console.WriteLine($"Меньше: {x < y}."); // TRUE
Console.WriteLine($"Больше или равно: {z >= y}."); // TRUE
Console.WriteLine($"Меньше или равно: {z <= y}."); // TRUE
```

В коде различных приложений очень часто можно обнаружить **конверсию одних типов в другие**. О конверсии уже было сказано несколько слов в видео посвящённому обобщенному 
программированию – ссылка будет в правом верхнем углу. Можно ли некоторый объект А привести к некоторому объекту Б? То есть возможен ли следующий синтаксис:

```javascript
var a = new SomeClassA();
var b = (SomeClassB) a;
class SomeClassA { }
class SomeClassB { }
```

Возможен. Однако для этого необходимо написать определенный код. Какой? Давайте рассмотрим на конкретном примере.
 
```javascript
class Program
    {
        static void Main(string[] args)
        {
            
            Console.WriteLine("\nПРИМЕР 3. Конверсия типов.");

            var mobile = new Mobile(5.2M, "Apple IOS");
            Console.WriteLine();
            Console.WriteLine(mobile);
            Console.WriteLine("Конверсия...");
            var tablet = (Tablet)mobile;
            Console.WriteLine(tablet);           

            Console.ReadKey();
        }
    }
	
class Mobile
    {
        public Mobile(decimal size, string operatingSystem)
        {
            DisplaySize = size;
            OperatingSystem = operatingSystem;
        }

        public decimal DisplaySize { get; }

        public string OperatingSystem { get; }

        public override string ToString() => $"Mobile => {DisplaySize}'', {OperatingSystem}";
    }

class Tablet
    {
        public Tablet(decimal size, string operatingSystem, bool supportsGsm)
        {
            DisplaySize = size;
            OperatingSystem = operatingSystem;
            SupportsGsm = supportsGsm;
        }

        public decimal DisplaySize { get; }

        public string OperatingSystem { get; }

        public bool SupportsGsm { get; }

        public override string ToString() => $"Tablet => {DisplaySize}'', {OperatingSystem}, GSM: {SupportsGsm}";

        public static explicit operator Tablet(Mobile mobile)
        {
            return new Tablet(mobile.DisplaySize * 2, mobile.OperatingSystem, true);
        }
    }
```