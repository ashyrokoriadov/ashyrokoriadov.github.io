---
title: Ключевое слово static - вопрос №22 на собеседование C# / .NET
subtitle: Текст к видео "Ключевое слово static" на канале YouTube
layout: page
show_sidebar: false
menubar: example_menu
author: andrew
category: c_sharp_questions
categories: c_sharp_questions
---

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/0H2WBSBySCU" 
frameborder="0" allow="accelerometer; autoplay; 
encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

При программировании на языке C# иногда можно оказаться в ситуации, когда класс, определяющий функциональности, не имеет собственного состоянии. То есть в классе нет 
ни полей, ни свойств специфичных для каждого отдельного экземпляра класса. И несколько созданных объектов такого класса, по сути, не будут ничем отличаться. 
Создание таких объектов было бы расходованием доступных ресурсов. Было бы неплохо чтобы такой класс без специфического внутреннего состояния был доступен из 
каждого места в коде и не было бы необходимости создавать экземпляры данного класса. Язык C# предоставляет такую возможность.

Если во время программирования, вы создали класс, в котором нет внутреннего состояния, то самое время задуматься, а не сделать ли этот класс **статическим**. Примером такого 
класса может быть класс для валидации строк, который имеет несколько методов:

```javascript
class StringValidator
{
	public bool ValidateLength(string data){}
	public bool ValidateSymbols(string data) {}
}
```

По этому коду можно сделать вывод, что в этом классе нет внутреннего состояния: каждый метод принимает строку в качестве аргумента и на основании внутренней 
логики возвращается значение типа bool в зависимости от результата валидации. Однако в текущей имплементации для использования функционала класса необходимо 
создавать его объект, то есть

```javascript
	var validator = new StringValidator();
```

Валидация строк может происходить в разных частях кода и каждый раз необходимо создавать экземпляр данного класса. Согласитесь это не очень удобно, а дополнительно 
мы знаем, что данный класс не имеет внутреннего состояния. Если класс не имеет внутреннего состояния для каждого конкретного объекта, то его можно сделать **статическим**. 
Класс StringValidator в своей статической версии будет выглядеть следующим образом:

```javascript
static class StringValidator
{
	public static bool ValidateLength(string data){}
	public static bool ValidateSymbols(string data) {}
}
```

Что изменилось? Перед декларацией класса и декларациями методов появилось **ключевое слово static**. Вообще ключевое слово static можно использовать с классами, методами, 
свойствами, полями, конструкторами. Об использовании слова **static** с каждым из этих членов будет сказано несколько слов чуть позже. Вернемся к нашему классу, теперь уже 
в статической версии. Теперь чтобы вызвать методы класса нам нет необходимости создавать объект данного класса, более того если мы попытаемся это сделать компилятор 
выдаст ошибку. Создавать объекты статических классов нельзя. Итак, как вызывать методы статического класса? Очень просто – данные методы должны быть вызваны ни с 
уровня объекта (данный уровень не существует вообще), а с уровня класса, то есть:

```javascript
	StringValidator.ValidateLength(someString);
	StringValidator.ValidateSymbols (someString);
```

Обратите внимание, что методы в статическом классе также обозначены **ключевым словом static**. Так как это статический класс, то он не имеет членов, то есть методов, свойств, 
полей на уровне экземпляра – объекта. Это значит, что каждый член статического класса должен быть на уровне класса, то есть обозначен **ключевом словом static**. Также из этого 
объяснения следует, что в статическом классе **нельзя использовать** ключевое слово **this**. Ключевое слов this в классе определяет конкретный данный объект рассматриваемого класса, 
однако мы не можем создать объект статического класса, а значит ключевое слово this не имеет смысла в статическом классе.

Статический класс создается при первом обращении к одному из его публичных членов. Вы с большой долей вероятности уже использовали статические классы, которые определены в 
среде разработки .Net. Начнем с самого простого – *Console*. Вы выводите текст на экран консоли вызывая статически метод *WriteLine*. Также при математических операциях вы, 
наверное, использовали класс *Math* и его разные статические методы: *Round*, *Pow*, *Abs* и другие. При рассмотрении темы управления памятью и работы сборщика мусора, я также 
упоминал класс *GC* (Garbage Collector) – данный класс также является статическим. Как видите, статические классы, не такое уже и редкое явление. Как правило в виде статических 
классов создают различные вспомогательные классы, их иногда еще называют **Helper классы**.

Возникает вопрос – может ли обычный нестатический класс иметь статические члены. Если коротко, то ответ утвердительный. Обычный нестатический класс может иметь статические члены. 
Доступ к таким членам может осуществляться с уровня объекта класса и с уровня класса. Очень важное замечание – такой статический член, поле или свойство, будет расположено в одном 
месте в памяти и все объекты нашего класса будут иметь доступ к данному члену в памяти. То есть статический член будет для всех объектов одинаков. Из этого следует, что если мы 
в одном из объектов данного класса изменим значение статического поля или свойства, то такое изменение произойдет и в других объектах данного класса. В видео посвященному 
синхронизации потоков и использованию ключевого слова lock, я указывал, что использование в качестве объекта синхронизации статического объекта является очень плохой идеей. 
Теперь вы знаете почему. Статический объект в классе является общим объектом синхронизации для всех объектов и скорость работы приложения снизится в следствии увеличение 
время ожидания на освобождение lock’а статического объекта синхронизации.

Использование статических членов хорошо рассматривать на конкретных примерах. Далее я покажу несколько примеров в коде, а также на примере небольшого приложения мы рассмотрим 
как работает статический конструктор.

**Пример кода:**

```javascript
using System;

namespace StaticSampleApp
{
    class Program
    {
        static void Main(string[] args)
        {
            //var calulator = new Calculator();

            Console.WriteLine($"Static Value: {Calculator.Value}");
            Console.WriteLine($"Static Add 2 + 0.5: {Calculator.Add(2)}");

            Calculator.Value = 2.0M;

            Console.WriteLine("");
            Console.WriteLine($"Static Value: {Calculator.Value}");
            Console.WriteLine($"Static Add 2 + 2: {Calculator.Add(2)}");

            Console.ReadKey();
        }
    }

    class Multiplier
    {
        public static decimal Ratio = 0.5M;

        public decimal Multiply(decimal value) => value * Ratio;
    }

    class Subtractor
    {
        public static decimal Subtrahend { get; set; } = 0.5M;

        public decimal Subtract(decimal minuend) => minuend - Subtrahend;
    }

    class Adder
    {
        public static decimal Value { get; set; } = 0.5M;

        public decimal Add(decimal addValue) => addValue + Value;

        public static decimal AddValue(decimal addValue) => addValue + Value;
    }

    class Divider
    {
        public static decimal Divisor { get; set; }

        public decimal Divide(decimal dividend) => dividend / Divisor;

        public Divider()
        {
            Console.WriteLine("Обычный конструктор");
        }

        public Divider(decimal value)
        {
            Console.WriteLine("Обычный конструктор 2");
        }

        static Divider()
        {
            Console.WriteLine("Статический конструктор");

            //какая-то функциональность имитирующая получение
            //данных из базы данных или сетевой услуги
            Divisor = 0.5M;
        }

        // отсутствие модификаторов доступа
        // отсутствие параметров
        // нельзя перегружать
        // выполняется только раз
        // служит для инициализации статических членов

    }

    static class Calculator
    {
        public static decimal Value { get; set; } = 0.5M;

        //public decimal AddValue(decimal addValue) => addValue + Value;

        public static decimal Add(decimal addValue)
        {
            //var someValue = this.Value;
            var result = addValue + Value;
            return result;
        }
    }

    /*
        var multiplier1 = new Multiplier();
        var multiplier2 = new Multiplier();

        Console.WriteLine($"Static Ratio: {Multiplier.Ratio}");
        Console.WriteLine($"multiplier1 0.5 x 2: {multiplier1.Multiply(2)}");
        Console.WriteLine($"multiplier2 0.5 x 3: {multiplier2.Multiply(3)}");

        Multiplier.Ratio = 2.0M;

        Console.WriteLine("");
        Console.WriteLine($"Static Ratio: {Multiplier.Ratio}");
        Console.WriteLine($"multiplier1 2 x 2: {multiplier1.Multiply(2)}");
        Console.WriteLine($"multiplier2 2 x 3: {multiplier2.Multiply(3)}");
     */

    /*
        var subtractor1 = new Subtractor();
        var subtractor2 = new Subtractor();

        Console.WriteLine($"Static Subtrahend: {Subtractor.Subtrahend}");
        Console.WriteLine($"subtractor1 2 - 0.5: {subtractor1.Subtract(2)}");
        Console.WriteLine($"subtractor2 3 - 0.5: {subtractor2.Subtract(3)}");

        Subtractor.Subtrahend = 2.0M;

        Console.WriteLine("");
        Console.WriteLine($"Static Subtrahend: {Subtractor.Subtrahend}");
        Console.WriteLine($"subtractor1 2 - 2: {subtractor1.Subtract(2)}");
        Console.WriteLine($"subtractor2 3 - 2: {subtractor2.Subtract(3)}");
    */

    /*
        var adder1 = new Adder();
        var adder2 = new Adder();

        Console.WriteLine($"Static Value: {Adder.Value}");
        Console.WriteLine($"adder1 0.5 + 2: {adder1.Add(2)}");
        Console.WriteLine($"adder2 0.5 + 3: {adder1.Add(3)}");
        Console.WriteLine($"adder static 0.5 + 2: {Adder.AddValue(2)}");

        Adder.Value = 2.0M;

        Console.WriteLine("");
        Console.WriteLine($"Static Value: {Adder.Value}");
        Console.WriteLine($"adder1 2 + 2: {adder1.Add(2)}");
        Console.WriteLine($"adder2 2 + 3: {adder2.Add(3)}");
        Console.WriteLine($"adder static 2 + 2: {Adder.AddValue(2)}");
     */

    /*
       var divider1 = new Divider();
       var divider2 = new Divider();

       Console.WriteLine("");
       Console.WriteLine($"Static Divisor: {Divider.Divisor}");
       Console.WriteLine($"divider1 2 / 0.5: {divider1.Divide(2)}");
       Console.WriteLine($"divider2 3 / 0.5: {divider2.Divide(3)}");

       Divider.Divisor = 2.0M;

       Console.WriteLine("");
       Console.WriteLine($"Static Divisor: {Divider.Divisor}");
       Console.WriteLine($"divider1 2 / 2: {divider1.Divide(2)}");
       Console.WriteLine($"divider2 3 / 2: {divider2.Divide(3)}");
    */

    /*
        //var calulator = new Calculator();

        Console.WriteLine($"Static Value: {Calculator.Value}");
        Console.WriteLine($"Static Add 2 + 0.5: {Calculator.Add(2)}");

        Calculator.Value = 2.0M;

        Console.WriteLine("");
        Console.WriteLine($"Static Value: {Calculator.Value}");
        Console.WriteLine($"Static Add 2 + 2: {Calculator.Add(2)}");
     */
}
```