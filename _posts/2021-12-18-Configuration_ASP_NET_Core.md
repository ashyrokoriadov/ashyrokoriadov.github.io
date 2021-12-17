---
title: №7 Конфигурация приложения Asp.Net Core [#57]. 
subtitle: Текст к видео "Конфигурация Asp.Net Core" на канале YouTube
layout: page
show_sidebar: false
menubar: example_menu
author: andrew
category: asp_net_core_mvc
categories: asp_net_core_mvc
---

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/P1akEAR4JSE" 
frameborder="0" allow="accelerometer; autoplay; 
encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

Приветствую Вас на моем канале. Темой сегодняшнего видео является **конфигурация приложения ASP.Net Core**. Это тема важна, потому что существует достаточно большое 
количество способов настроить приложение ASP.Net Core по сравнению с приложением .Net Framework. В Net Framework мы как правило пользовались стандартными XML 
файлами **App.config** или **Web.config**, а если это было консольное приложение, то можно было передать некоторые опции в виде аргументов командной строки. Конфигурация 
приложения в ASP.Net Core производиться при помощи, так называемых, провайдеров конфигурации или на английском языке – **configuration providers**. Провайдеры 
конфигурации читают конфигурационные опции из пар ключ-значение используя различные источники конфигурации:

 - файлы настроек, например appsettings.json
 - переменные среды
 - хранилище Azure Key Vault
 - Azure App Configuration
 - аргументы командной строки
 - провайдеры, созданные другими программистами
 - файлы
 - объекты .NET загруженные в память

Сегодня мы познакомимся с некоторыми поставщиками конфигурации из списка выше. Прежде чем мы начнем, стоит вспомнить, что в видео на тему хоста приложения 
ASP.Net Core мы говорили о том, что приложение можно настроить по умолчанию. Для этого при создании объекта, который реализует интерфейс **IHostBuilder**, необходимо 
вызвать метод **ConfigureWebHostDefaults**. Данный метод настроит приложение по умолчанию путем добавления провайдеров конфигурации в определенном порядке. Если 2 
провайдера конфигурации содержат одинаковую опцию, то будет использована та опция, которая была добавлена позже.

Начнем рассмотрение с поставщика конфигурации основанном на файлах настроек **appsettings.json**. Такой файл добавляется в проект приложения автоматически при создании 
нового проекта. Файлы конфигурации json имеют стандартный формат файлов json – ничего нового или нестандартного. Сюда вы можете добавить что угодно, главное, чтобы 
данные были в формате **json**.

```javascript
{
  "Polly": {
    "RetriesNumber": 3,
    "IntervalBetweenRetries": 10
  },
  "DeliveryServiceApi":  "www.delivery-api:51082",
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  },
  "AllowedHosts": "*"
}
```

Код, который будет представлен далее использует эти настройки полученные из объекта конфигурации:

```javascript
public class ConfigReader
{
    private readonly IConfiguration Configuration;

    public ConfigReader (IConfiguration configuration)
    {
        Configuration = configuration;
    }

    public void Display()
    {
        var deliveryApi = Configuration["DeliveryServiceApi "];
        var retriesNumber = Configuration["Polly:RetriesNumber"];
        var interval = Configuration["Polly:IntervalBetweenRetries"];

        Console.WriteLine($"deliveryApi: {deliveryApi} \n" +
                       $"retriesNumber: {retriesNumber} \n" +
                       $"interval: {interval}");
    }
}
```

По умолчанию, поставщик конфигурации JSON, т.е. **JsonConfigurationProvider**, загружает конфигурацию в следующем порядке:
1.	**appsettings.json**
1.	**appsettings.Среда.json**: Например, файлы appsettings.Production.json и appsettings.Development.json. Версия файла для конкретной среды загружается на основании 
значения свойства IHostingEnvironment.EnvironmentName. 

**appsettings.Среда.json** переопределяет значения в файле appsettings.json. Например, переопределение происходит по умолчанию следующим образом:

 - При разработке, значения в файле appsettings.Development.json переопределяют значения в файле appsettings.json.
 - В производственной среде, значения в файле appsettings.Production.json переопределяют значения в файле appsettings.json.

Предыдущий пример только считывает значения, и такой способ чтения конфигурации не гарантирует, что в случае отсутствия значения в файле, будет добавлено некоторое 
значение по умолчанию.

При использовании конфигурации по умолчанию файлы appsettings.json и appsettings.Environment.json добавляются с включенной опцией **reloadOnChange: true**. Изменения 
сделанные в данных файлах после запуска приложения будут считаны провайдером конфигурации JSON.

Есть более предпочтительный способ чтения конфигурации из файлов JSON. Предположим, у нас есть файл JSON из предыдущего примера, и мы хотели бы считывать 
конфигурацию библиотеки **Polly**. Прежде всего давайте создаём класс модели для данной конфигурации, который назовём **PollyOptions**.

```javascript
public class PollyOptions
{
    public const string SectionName = "Polly";

    public int RetriesNumber { get; set; }
    public int IntervalBetweenRetries { get; set; }
}
```

К классу – модели, который отражает опции в файле JSON, предъявляют определенные требования:

 - Это должен быть не абстрактный класс с конструктором без параметров.
 - Он должен отражать все опции конфигурации в виде публичных свойств.
 - Поля и константы класса не должны отражать опции конфигурации, так как в любом случае они будут проигнорированы.

После создания класса – модели, который отражает конфигурацию в файле JSON, мы можем использовать данный файл 3 разными способами. 

**Первый способ** – использовать метод **Bind**:

```javascript
public class ConfigReader
{
    private readonly IConfiguration Configuration;

    public ConfigReader (IConfiguration configuration)
    {
        Configuration = configuration;
    }

    public void Display()
    {

	var pollyOptions = new PollyOptions();
        Configuration.GetSection(PollyOptions.SectionName).Bind(PollyOptions);

        var retriesNumber = pollyOptions.RetriesNumber;
        var interval = pollyOptions.IntervalBetweenRetries;

        Console.WriteLine($"retriesNumber: {retriesNumber} \n" +
                       $"interval: {interval}");
    }
}
```

**Второй способ** – использовать метод **Get**:

```javascript
public class ConfigReader
{
    private readonly IConfiguration Configuration;

    public ConfigReader (IConfiguration configuration)
    {
        Configuration = configuration;
    }

    public void Display()
    {

	var pollyOptions = Configuration
.GetSection(PollyOptions.SectionName)
.Get<PollyOptions>();

        var retriesNumber = pollyOptions.RetriesNumber;
        var interval = pollyOptions.IntervalBetweenRetries;

        Console.WriteLine($"retriesNumber: {retriesNumber} \n" +
                       $"interval: {interval}");
    }
}
```

**Третий способ** – зарегистрировать класс с опциями конфигурации в виде зависимости в методе **ConfigureServices** и внедрять его в виде зависимости там, 
где данные опции необходимы.

Регистрация зависимости:

```javascript
public void ConfigureServices(IServiceCollection services)
{
    services.Configure<PollyOptions>(Configuration.GetSection(
                                        PollyOptions.SectionName));
}
```

Использование зависимости:

```javascript
public class ConfigReader
{
    private readonly PollyOptions _pollyOptions;

    public ConfigReader (IOptions<PollyOptions> pollyOptions)
    {
        _pollyOptions = pollyOptions.Value;
    }

    public void Display()
    {
        var retriesNumber = _pollyOptions.RetriesNumber;
        var interval = _pollyOptions.IntervalBetweenRetries;

        Console.WriteLine($"retriesNumber: {retriesNumber} \n" +
                       $"interval: {interval}");
    }
}
```

Из третьего способа чтений опций конфигурации из файла JSON следует, что мы в методе **ConfigureServices** мы можем совмещать регистрацию стандартных зависимостей с 
регистрацией зависимости опций конфигурации.

Связанные по смыслу регистрации можно перенести в метод расширения для регистрации. Например, для регистрации опций конфигурации можно создать отдельный 
метод расширения. Оставшиеся услуги буду зарегистрированы как обычно.

**Переменные среды**.

Используя конфигурацию по умолчанию, поставщик конфигурации из переменных среды, **EnvironmentVariablesConfigurationProvider** загружает конфигурацию из переменных среды, 
которые представляют собой пары ключ-значение после чтений файлов appsettings.json, appsettings.Environment.json и конфиденциальной информации пользователя. Поэтому 
значения полученные из переменных среды надписывают значения из файлов appsettings.json, appsettings.Environment.json и конфиденциальной информации пользователя. 

Следует обратить внимание, что в отличии от чтения данных из файлов JSON, в случае переменных среды сепаратор в виде двоеточия **(«:»)** не работает. В переменных среды 
необходимо использовать двойное подчеркивание **(«__»)**.

Конфигурациям по умолчанию загружает переменные среды и аргументы командной строки с префиксами **DOTNET_** и **ASPNETCORE_**. Префиксы **DOTNET_** и **ASPNETCORE_** используются 
фреймворком ASP.NET Core для конфигурации хостов и приложений. Дополнительная информация на эту тему доступна в моем видео «Хост приложения ASP.NET Core», ссылка 
на которое будет доступна в правом верхнем углу и в описании к данному видео.

Названиях переменных среды отражают структуру файла appsettings.json file. Каждый элемент в иерархии отделен двойным подчеркиванием. Если элемент в иерархии 
включает в себя массив, индексы массива ведут себя как дополнительный элемент иерархии. Я думаю данную информацию легче всего будет понять при рассмотрении примера.

Файл appsettings.json:

```javascript
{
    "WebApiAddress": "www.some-api.com",
    "Logging": [
        {
            "Name": "ToEmail",
            "Level": "Critical",
            "Args": {
                "Name1": "Value1",
                "Name2": "Value2"
            }
        },
        {
            "Name": "ToConsole",
            "Level": "Information"
        }
    ]
}
```

Переменные среды, которые отражают структуру файла выше:

```javascript
setx WebApiAddress =www.some-api.com
setx Logging__0__Name=ToEmail
setx Logging__0__Level=Critical
setx Logging__0__Args__Name1=Value1
setx Logging__0__Args__Name1=Value2
setx Logging__1__Name=ToConsole
setx Logging__1__Level=Information
```
Следующий пример выводит на экран все переменные среды и их значение при старте приложения. Это может быть полезно при дебаге настроек среды выполнения:

```javascript
public static void Main(string[] args)
{
    var host = CreateHostBuilder(args).Build();

    var config = host.Services.GetRequiredService<IConfiguration>();

    foreach (var c in config.AsEnumerable())
    {
        Console.WriteLine(c.Key + " = " + c.Value);
    }
    host.Run();
}
```

**Аргументы командной строки.**

По умолчанию опции конфигурация, которые были переданы, как аргументы командной строки переопределяют опции конфигурации, которые были уже переданы в файлах JSON и 
переменных среды.

Аргументы командной строки передаются в виде пар «ключ - значение» при вызове нашего приложения из командной строки. Данные пары можно определять при помощи знаков 
«равно», «двойной дефис», «слэш».

В качестве ключей аргументов командной строки мы можем использовать длинные и короткие ключи. Например, давайте посмотрим 
на <a href ="https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-run#options" target="_blank">список аргументов командной строки</a><br/> команды 
dotnet run. Мы видим, что в списке для каждого ключа дано короткое название после одного дефиса и длинное название после двойного дефиса. Такой пример используется 
многими приложениями. И такой приём может использоваться каждым приложением ASP.Net Core. На английском языке этот приём называется «**switch mapping**». 
Мне тяжело подобрать аналог этого названия на русском языке, тем более что второе слово на русском языке в моем переводе скорей всего останется без 
изменений, то есть это будет «маппинг». Вопрос только чего. В данном видео будет пользоваться английским названием. Прием «switch mapping» представляет 
собой логику подмены названий аргументов. Для того чтобы его использовать, необходимо подготовить словарь с парами для подмены. Этот словарь передается 
в качестве аргумента в метод **AddCommandLine**. 

Когда мы используем данный словарь, ключе переданные как аргументы командной строки сравниваются с ключами словаря. Если ключ аргумента найден в словаре, 
значение словаря для соответствующего ключа передаётся в конфигурацию приложения. Данный приём будет обязательный для любого аргумента, который передан в 
командной строке с использованием одинарного дефиса. 

Правила приёма «**switch mapping**».:

 - Название аргумента должно начинаться с одинарного или двойного дефиса.
 - Не допускаются двойные названия аргументов, потому что словарь не может содержать элементы с одинаковыми ключами.

```javascript
public static IHostBuilder CreateHostBuilder(string[] args)
    {
        var switchMappings = new Dictionary<string, string>()
         {
             { "--a1", "key1" },
             { "--b1", "key2" },
             { "--c1", "key3" },
             { "--d1", "key4" },
             { "--e1", "key5" },
             { "--f1", "key6" },
         };

        return Host.CreateDefaultBuilder(args)
            .ConfigureAppConfiguration((hostingContext, config) =>
            {
                config.AddCommandLine(args, switchMappings);
            })
            .ConfigureWebHostDefaults(webBuilder =>
            {
                webBuilder.UseStartup<Startup>();
            });
    }
```

К конфигурационным парам ключ-значения применяются следующие правила.

**Ключи**:

 - величина букв в названии ключа не имеет значения.
 - если величина с определенным ключом была приписана несколько раз, то последнее приписанное значение будет использоваться.
 - в зависимости от типа провайдера конфигурации для определения иерархии конфигурационных опций используются различные сепараторы. Например, 
двоеточие работает на всех платформах. Для переменных среды рекомендуется использование двойного знака подчеркивания. Для провайдеров Azure 
рекомендуется использовать двойной дефис.

**Значения**:

 - тип значений – string;
 - значение null не может храниться в конфигурации и быть приписано объекту

Опции конфигурации также можно хранить в памяти. Например, при старте приложения мы можем определить словарь и передать его в качестве аргумента в 
метод **AddInMemoryCollection**. Далее значения в словаре будут использоваться как опции конфигурации. Такой способ добавления конфигурации добавляется 
после файлов JSON, переменных среды и аргументов командной строки.

Стоит сказать пару слов о конфигурации адреса сервера **Kestrel** в файлах **appsettings.json** Данная конфигурация надписывает все остальные конфигурации 
адресов серверов, которые были определены следующими способами

 - использование метода **UseUrls**
 - использование аргумента с названием **–urls** в командной строке
 - переменные среды, которые начинаются с префикса **ASPNETCORE_URLS**

Ниже пример файла конфигурации appsettings.json который используется в веб приложение ASP.NET Core:

```javascript
{
  "Kestrel": {
    "Endpoints": {
      "Https": {
        "Url": "https://localhost:9999"
      }
    }
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  },
  "AllowedHosts": "*"
} 
```

Данный файл используется в веб приложении ASP.NET Core. Если данное приложения запустить из командной строки со следующим аргументом:

```javascript
dotnet run --urls="https://localhost:7777"
```

Kestrel будет использовать адрес указанный в файле appsettings.json (https://localhost:9999), потому что в данном файле указана конфигурация специально 
для сервера **Kestrel**. Аргумент   командной строки будет проигнорирован.

Рассмотрим переменную среды с указанием адреса сервера Kestrel:

```javascript
set Kestrel__Endpoints__Https__Url=https://localhost:8888
```

Данная переменная среды определяет Https адрес сервера Kestrel. Также в файле appsettings.json есть такая же настройка для сервера Https. 
По умолчанию переменные среды вчитываются после файлов appsettings.Environment.json, и поэтому, в качестве адреса сервера Kestrel 
будет использоваться адрес из переменной среды.

<a href ="https://github.com/ashyrokoriadov/youtube-aspnetcore-configuration-example" target="_blank">Пример кода из видео на GitHub</a><br/>

Для открытия файла проекта необходимо Visual Studio 2019.