---
title: Page with tabs
subtitle: Demo page with tabs
layout: page
show_sidebar: false
menubar: example_menu
author: ted
category: Matplotlib
categories: matplotlib
---

### Anatomia wykresu
Każdy wykres, nie ważne czy jest narysowany od ręki czy przy pomocy jakiegoś narzędzia, posiada zdefiniowane elementy bez których wykres nie mógłby być wykresem. Do tych elementów należą:
- osie (*axes*)
- wykresy (*lines / line plot*)
- markery (*markers / scatter plot*)
- podpisy osi (*axis labels*)
- nagłówek całego rysunku (*title*)
- siatka (*grid*)
- legenda (*legend*)

Do tego należy dotać kilka elementów używanych przez bibliotekę Matplotlib:

- duże oznaczenie osi (*major tick*)
- małe oznaczenie osi (*minor tick*)
- podpis dużego oznaczenia osi (*major tick label*)
- podpis małego oznaczenia osi (*minor tick label*)
- obiekt wykresu w całości (*figure*)

<img src="https://matplotlib.org/_images/anatomy.png" alt="Typowe elementy przykładowego wykresu w Matplotlib" width="550" height="550"/>

> **Osie** - reprezuntują wymiary danych. Naprzykład mając zbiór danych składających się z dwóch wymiarów ([1,1], [5,3]) będziemy mieli wykres z 2 osiami. Zwykle oś pozioma ma oznaczenie X, oś pionowa ma oznaczenie Y, oś trzeciego wymiaru ma oznaczenie Z. 
>
> **Wykres** - jest to graficzna reprezentacja danych
>
> **Markery** - służy do zaznaczania danych lub wydzielenia okrślonego zestawu danych
>
> **Podpisy osi i nagłówek całego rysunku** - ułatwia czytanie wykresu dla odbiorców
>
> **Siatka** - ułatwia określenie wielkości poszczególnych elementów wykresu
>
> **Legenda** - pozwala opisać dane reprezentowane na wykresie
> 
> **Oznaczenia osi** - pokazuje skalę danych
> 
> **Podpisy oznaczeń osi** - określa skalę danych
> 
> **Obiekt wykresu** - obiekt w sensie programistycznym używany przez Matplotlib

Wszystkie elementy wykresu Matplotlib są przyporządkowane określonej hierarchii. Na górze hierarchii jest obiekt wykresu w całości (*figure*) do którego są dodawana pozostałe elementy, między innymi osie. Wykres może zawirać dowolną liczbę osie, ale żeby być pożytecznym przyda się przynajmniej jedna oś.

Najłatwiejszy sposób utworzenia wykresu w Matplotlib jest przedstawiony poniżej.

{% highlight python %}
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(0, 2, 100) #utworzenie tablicy jednowymiarowej o rozmiarze 100 zawierającej elementy w przedziale [0:2]

plt.plot(x, x, label='linowa') #dodanie funkcji liniowej, wartość *label* zostanie użyta w legendzie 
plt.plot(x, x**2, label='kwadratowa') #dodanie funkcji kwadratowej, wartość *label* zostanie użyta w legendzie 
plt.plot(x, x**3, label='sześcienna') #dodanie funkcji x do potęgi 3, wartość *label* zostanie użyta w legendzie 

#dodawanie podpisów osi
plt.xlabel('podpis osi x')
plt.ylabel('podpis osi y')

#dodawanie nagłówku całego rysunku
plt.title("Trzy funkcje")

#dodawanie legendy
plt.legend()

#wyświetlenie wykresu
plt.show()
{% endhighlight %}

W ramach jednego obiektu *figure* można narysować kilka wykresów z różnym zestawem danych o różnym typie. Szczególnie jest to pomocne przy rysowaniu wykresów danych wielowymairowych.

{% highlight python %}
import matplotlib.pyplot as plt #importowanie biblioteki Matplotlib
import numpy as np

x = np.linspace(-2, 2, 100) 
y = np.linspace(5, 5, 100) 

fig = plt.figure()  
fig, axes = plt.subplots(2, 2)  

plt.subplots_adjust(left=0.125, bottom=0.1, right=2, top=2.2, wspace=0.2, hspace=0.2)

axes[0, 0].plot(x, x, label='linowa', c='r') 
axes[0, 0].set_xlabel('subplot 1 axis x')
axes[0, 0].set_ylabel('subplot 1 axis y')
axes[0, 0].title.set_text('Funkcja liniowa')
axes[0, 0].legend()

axes[0, 1].plot(x, x**2, label='kwadratowa', c='y') 
axes[0, 1].set_xlabel('subplot 2 axis x')
axes[0, 1].set_ylabel('subplot 2 axis y')
axes[0, 1].title.set_text('Funkcja kwadratowa')
axes[0, 1].legend()

axes[1, 0].plot(x, x**3, label='sześcienna', c='g') 
axes[1, 0].set_xlabel('subplot 3 axis x')
axes[1, 0].set_ylabel('subplot 3 axis y')
axes[1, 0].title.set_text('Funkcja sześcienna')
axes[1, 0].legend()

axes[1, 1].plot(x, y, label='prosta') 
axes[1, 1].set_xlabel('subplot 4 axis x')
axes[1, 1].set_ylabel('subplot 4 axis y')
axes[1, 1].title.set_text('Funkcja prosta')
axes[1, 1].legend()

plt.show()
{% endhighlight %}
<img src="/assets/images/00000.png" alt="4 wykresy w jednym" />

W kodzie powyżej najpierw dodajemy dane, które będą użyte w wykresach czyli
{% highlight python %}
x = np.linspace(-2, 2, 100) 
y = np.linspace(5, 5, 100) 
{% endhighlight %}
Dalej tworzymy wykres i dodajemy wykresy podrzędne
{% highlight python %}
fig = plt.figure()  
fig, axes = plt.subplots(2, 2)
{% endhighlight %}
Ustawiamy odstępy pomiędzy wykresami podrzędnymi
{% highlight python %}
plt.subplots_adjust(left=0.125, bottom=0.1, right=2, top=2.2, wspace=0.2, hspace=0.2)
{% endhighlight %}
Domyślne znaczenia argumentów metody *subplots_adjust* to
* *left* = 0.125  - lewa strona wykresu podrzędnego
* *right* = 0.9   - prawa strona wykresu podrzędnego
* *bottom* = 0.1  - dół wykresu podrzędnego
* *top* = 0.9     - góra wykresu podrzędnego
* *wspace* = 0.2  - odstęp w poziomie pomiędzy wykresami podrzędnymi, jako odsetek średniej długości osi poziomej
* *hspace* = 0.2  - odstęp w pionie pomiędzy wykresami podrzędnymi, jako odsetek średniej długości osi pionowej
Należy pamiętać żę wartość *left* ma być mniejsza od wartości *right* oraz wartość *bottom* ma być mniejsza od wartości *top*

Ustawiamy parametry dla pierwszego wykresu podrzędnego:
{% highlight python %}
axes[0, 0].plot(x, x, label='linowa', c='r') 
axes[0, 0].set_xlabel('subplot 1 axis x')
axes[0, 0].set_ylabel('subplot 1 axis y')
axes[0, 0].title.set_text('Funkcja liniowa')
axes[0, 0].legend()
{% endhighlight %}
* *axes[0, 0].plot* - dodawanie wykresu, parametr c to kolor linii wykresu
* *axes[0, 0].set_xlabel* i *axes[0, 0].set_ylabel* - podpisy osi wykresu podrzędnego
* *axes[0, 0].title.set_text* - dodawanie nagłówku wykresu podrzędnego
* *axes[0, 0].legend* - dodawanie legentu

W każdym wykresie podrzędnym te parametry powinny być ustawione osobne dlatego warto rozważyć napisanie funkcji aby pozbyć się powtarzającego kodu.

Parametr *c* może przyjmować następujące wartości:

<table>
<tr><th>character</th><th>color</th></tr>
<tr><td>b</td><td>blue</td></tr>
<tr><td>g</td><td>green</td></tr>
<tr><td>r</td><td>red</td></tr>
<tr><td>c</td><td>cyan</td></tr>
<tr><td>m</td><td>magenta</td></tr>
<tr><td>y</td><td>yellow</td></tr>
<tr><td>k</td><td>black</td></tr>
<tr><td>w</td><td>white</td></tr>
</table>

Dodatkowo kolory można podawać używając kilku innych formatów:
* pełna nazwa koloru, np. 'green'
* ciąg znaków hex, np. '#008000'
* krotki RGB lub RGBA, np. ((0,1,0,1))
* intensywność skali szarości, np. '0.8'

### Rysowanie wykresów używając pyplot

Ogólnie rzeczbiorąc rysowanie wykresów w pyplot jest bardzo proste. Używamy różnych funkcji do dodawanie do wykresu różnych obiektów (dane, napisy, legendy) lub zmieniając ich stan. 
{% highlight python %}
import matplotlib.pyplot as plt
plt.plot([1, 2, 3, 4])
plt.ylabel('Liczby')
plt.show()
{% endhighlight %}
<img src="/assets/images/00010.png" alt="Funkcja kwadratowa" />

Dla każdej pary *x* i *y* można podać trzeci nie wymagany argument określający kolor i typ linii na wykresie. Domyślna wartość tego argumentu to 'b-' co znaczy że będzie to stała linia(*-*) o kolorze niebieskim (*b*). Wartości tego arhumentu pochodzą z MATLAB oraz są dostępne w dokumentacji funkcji <a href='https://matplotlib.org/2.1.1/api/_as_gen/matplotlib.pyplot.plot.html' target='_blank'>plot()</a>

Gdybyśmy chcieli narysować wykres składający się z zielonych markerów w krztalcie gwiazdki, to należało by użyć następującego kodu:
{% highlight python %}
import matplotlib.pyplot as plt
plt.plot([0, 1, 2, 3, 4, 5], 
         [0, 1, 4, 9, 16, 25],
        'g*')
plt.show()
{% endhighlight %}
<img src="/assets/images/00020.png"  />

Możemy określić minimalne i maksymalne wartości na osiach *x* i *y* używając funkcji <a href='https://matplotlib.org/api/_as_gen/matplotlib.pyplot.axis.html#matplotlib.pyplot.axis' target='_blank'>axis()</a>. Funkcja ta przyjmuje 4 argumenty [xmin, xmax, ymin, ymax]. W ramachach przykładu dodajmy ograniczenie do poprzedniego wykresu.
{% highlight python %}
import matplotlib.pyplot as plt
plt.plot([0, 1, 2, 3, 4, 5], 
         [0, 1, 4, 9, 16, 25],
        'g*')
plt.axis([0,6,0,30])
plt.show()
{% endhighlight %}
<img src="/assets/images/00030.png"  />

Jako parametry liczbowe najlepie używać tablic numpy array. De facto wszystkie tablicy przekazywane do funkcji *plot()* wewnętrzenie są konwertowane do numpy array. Przykład poniżej przedstawia użycie tablicy numpy do rysowania kilku wykresów o różnych stylach.
{% highlight python %}
import numpy as np

# 0. - wartość początkowa tablicy
# 5. - wartość końcowa tablicy
# 0.2 - wartość kroku
t = np.arange(0., 5., 0.2) #tablica o wymiarze 1 x 25 ((5 - 0)/0.2 = 25)

# żółte pięciokąty, czerwone sześciokąty i zielone romby
plt.plot(t, t, 'yp', t, t**2, 'rH', t, t**3, 'gD')
plt.show()
{% endhighlight %}
<img src="/assets/images/00040.png"  />
