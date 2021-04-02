---
title: Многопоточность - deadlock, livelock, starvation - вопрос №21 на собеседование C# / .NET
subtitle: Текст к видео "Многопоточность - deadlock, livelock, starvation" на канале YouTube
layout: page
show_sidebar: false
menubar: example_menu
author: andrew
category: c_sharp_questions
categories: c_sharp_questions
---

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/PLQsnBo3Z4E"  
frameborder="0" allow="accelerometer; autoplay; 
encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

В многопоточном программировании поиск ошибок и багов может быть проблематичным по сравнению с синхронным однопоточным программированием. И среди всех множества возможных ошибок 
отдельной группой являются ошибки типа **live-lock**, **dead-lock** и **starvation**. Симптомом этих ошибок является якобы зависание приложения и невозможность выполнения программной 
логики после определенной точки в коде. Рассмотрим каждую из этих ситуаций и попытаемся их понять.

**Deadlock** рассмотрим на примере 2 потоков: *А* и *Б*. Потоку *А* для выполнение своих заданий необходимо выполнение некоторых заданий в потоке *Б*. С другой стороны потоку *Б* 
для выполнения некоторых своих заданий необходимо выполнение некоторых заданий в потоке *А*. Получается что в некоторых ситуациях поток *А* ждет поток *Б*, а поток *Б* в свою очередь 
ожидает поток *А*. Иногда такое ожидание может наступать одновременно:

 - поток А ждет поток Б;
 - поток Б ждет поток А;
 
Во время ожидания ничего не происходит, это просто ожидание, однако в текущей ситуации такое ожидание будет продолжаться бесконечно: поток *А* никогда не дождется окончания операций 
потока *Б*, потому что поток *Б* не может дождаться окончания операций потока *А*. Это был классический пример **dealock**’а. Далее в видео будет представлен практический пример 
как *dealock* выглядит в коде.

**Livelock** – очень похож на deadlock, с той лишь разницей, что во время *livelock*’а потоки во время ожидания выполняют какие-то операции. Однако эти операции не имеют практического 
смысла, так как потоки несмотря на выполняемые операции и так не могут завершить свои задания. Также далее в видео будет практический пример *livelock*’а.

**Starvation** – то есть «голод» - описывает ситуацию, когда несмотря на отсутствие deadlock’ов и livelock’ов, поток не может получить доступ к определенному ресурсу и завершить свою 
работу. Например, есть поток, который очень часто получает доступ к эксклюзивному ресурсу и долго выполняет свои операции используя эксклюзивный ресурс. Другие потоки, несмотря 
на отсутствие lock’ов не могут получить доступ к эксклюзивному ресурсу и выполнить свою работу. В этом случае имеет место явление старвации, то есть «голода ресурсов».

**Пример кода:**

```javascript
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.Threading.Tasks;

namespace LockExample
{
    class Program
    {
        static void Main(string[] args)
        {
		/*
		var syncObject1 = new object();
		var syncObject2 = new object();
	
		var a = new A();
		var b = new B();

		Task.Run(() => a.PerformOperation(syncObject1, syncObject2));
		Task.Run(() => b.PerformOperation(syncObject1, syncObject2));
		*/

		/*
		var c = new C();
		var d = new D();
		var e = new E();

		Task.Run(() => c.PerformOperation(e));
		Task.Run(() => d.PerformOperation(e));
		*/
			
		Console.ReadLine();

		/*
		 * Класс А
		 * лок 1
		 * лок 2
		 * 
		 * Класс В
		 * лок 2
		 * лок 1
		 * 
		 * Класс С
		 * условие Е1
		 * условие Е2 - если не выполняется подожди и попрбуй еще раз
		 * 
		 * Класс D
		 * условие Е2
		 * условие Е1 - если не выполняется подожди и попрбуй еще раз
		 * 
		 * Класс Е - класс с условиями 
		 */
        }
    }

    class A
    {
        public void PerformOperation(object syncObject1, object syncObject2)
        {
            Console.WriteLine("Класс А, перед lock 1");
            lock (syncObject1)
            {
                Console.WriteLine("Класс А, lock 1");

                //симуляция выполнения какого-то задания
                Thread.Sleep(1000);

                Console.WriteLine("Класс А, перед lock 2");
                lock(syncObject2)
                {
                    Console.WriteLine("Класс А, lock 2");

                    //симуляция выполнения какого-то задания
                    Thread.Sleep(1000);
                }
                Console.WriteLine("Класс А, после lock 2");
            }
            Console.WriteLine("Класс А, после lock 1");
        }
    }

    class B
    {
        public void PerformOperation(object syncObject1, object syncObject2)
        {
            Console.WriteLine("Класс B, перед lock 2");
            lock(syncObject2)
            {
                Console.WriteLine("Класс B, lock 2");

                //симуляция выполнения какого-то задания
                Thread.Sleep(1000);

                Console.WriteLine("Класс B, перед lock 1");
                lock(syncObject1)
                {
                    Console.WriteLine("Класс B, lock 1");

                    //симуляция выполнения какого-то задания
                    Thread.Sleep(1000);
                }
                Console.WriteLine("Класс B, после lock 1");
            }
            Console.WriteLine("Класс B, после lock 2");
        }
    }

    class C
    {
        public void PerformOperation(E e)
        {
            while (true)
            {
                Console.WriteLine("Класс C, перед can procceed 1");
                if (e.CanProcceed1)
                {
                    Console.WriteLine("Класс C, can procceed 1");

                    e.CanProcceed1 = false;

                    //симуляция выполнения какого-то задания
                    Thread.Sleep(1000);

                    while (true)
                    {
                        //симуляция выполнения какого-то задания
                        Thread.Sleep(1000);

                        Console.WriteLine("Класс C, перед can procceed 2");
                        if (e.CanProcceed2)
                        {
                            e.CanProcceed2 = false;
                            Console.WriteLine("Класс C, can procceed 2");

                            break;                            
                        }
                        Console.WriteLine("Класс C, после can procceed 2");
                    }

                    e.CanProcceed2 = true;
                }
                Console.WriteLine("Класс C, после can procceed 1");

                if (e.CanProcceed2)
                {
                    e.CanProcceed1 = true;
                    break;
                }
            }
            Console.WriteLine("Класс C, конец");
        }
    }

    class D
    {
        public void PerformOperation(E e)
        {
            while (true)
            {
                Console.WriteLine("Класс D, перед can procceed 2");
                if (e.CanProcceed2)
                {
                    Console.WriteLine("Класс D, can procceed 2");

                    e.CanProcceed2 = false;

                    //симуляция выполнения какого-то задания
                    Thread.Sleep(1000);

                    while (true)
                    {
                        //симуляция выполнения какого-то задания
                        Thread.Sleep(1000);

                        Console.WriteLine("Класс D, перед can procceed 1");
                        if (e.CanProcceed1)
                        {
                            e.CanProcceed1 = false;
                            Console.WriteLine("Класс D, can procceed 1");

                            break;
                        }
                        Console.WriteLine("Класс D, после can procceed 1");
                    }

                    e.CanProcceed1 = true;
                }
                Console.WriteLine("Класс D, после can procceed 2");

                if (e.CanProcceed1)
                {
                    e.CanProcceed2 = true;
                    break;
                }
            }
            Console.WriteLine("Класс D, конец");
        }        
    }

    class E
    {
        public bool CanProcceed1 { get; set; } = true;
        public bool CanProcceed2 { get; set; } = true;
    }
}
```