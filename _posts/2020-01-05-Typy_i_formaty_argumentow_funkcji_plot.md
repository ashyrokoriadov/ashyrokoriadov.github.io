---
title: Typy i formaty argumentów funkcji plot() - wideo Matplotlib 4 4
subtitle: Tekst do wideo Matplotlib 4 4 na kanale YouTube
layout: page
show_sidebar: false
menubar: example_menu
author: andrew
category: Matplotlib
categories: matplotlib
---

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/tPnA484if_8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

Witam wszystkich na moim  kanale. Dzisiaj będziemy rozmawiać o typach danych i formatach w jakich te dane można przekazać jako argumenty funkcji **plot**.

#### **Praca z atrybutami tekstowymi**

Spotykamy struktury danych, w których dostęp do poszczególnych elementów jest możliwy przy pomocy tekstu, na przykład słowniki **Dictionary** z typem klucza **string**. Są to również struktury danych, które pozwalają na dostęp do elementów przy użyciu atrybutów, na przykład **numpy.recarray** lub **pandas.DataFrame**. Użycie takiego argumentu jest możliwe w **Matplotlib** poprzez podanie argumentu nazwanego data. Jeżeli argument ten został podany, możliwe jest użycie atrybutów do odpowiednich elementów danych jako argumentów funkcji **plot()**.

W ramach przykładu utworzymy strukturę danych o nazwie _data_, która będzie się składać z 4 elementów: a,  b,  c i d.
-	element a zostanie utworzony przez funkcję **np.arrange(i)**, która wygeneruje i liczb w przedziale od 0 do i-1. W naszym przykładzie wartość argumentu i to 50 czyli wynikiem działania funkcji będzie tablica o długości 50 z elementami od 0 do 49;
-	element b zostanie obliczony przez formułę na podstawie wartości odpowiedniego elementu a;
-	element c zostanie utworzony przez funkcję **np.random.randint**. Ta funkcja generuje liczby losowe i w naszym przykładzie przyjmuje 3 argumenty. Pierwszy argument to początek przedziału, drugi argument to koniec przedziału, trzeci argument to liczba wygenerowanych elementów; w naszym przykładzie wywołujemy funkcję **np.random.randint** z argumentami (0,50,50) czyli możemy spodziewać się 50 liczb losowych w przedziale od 0 do 49;
-	element d zostanie utworzony przez funkcję **np.random.randn(i)**. Funkcja ta generuje liczby losowe o rozkładzie normalnym i w naszym przykładzie przyjmuje 1 argument, który jest liczbą wygenerowanych wartości losowych; w naszym przykładzie wywołujemy funkcję **np.random.randn(i)** z argumentem  50 czyli możemy spodziewać się 50 liczb losowych o rozkładzie normalnym.

Do narysowania wykresu użyjemy funkcji **scatter**. W tłumaczeniu z angielskiego słowo _scatter_ znaczy **rozproszenie**. Jak można się domyśleć wykres rozproszenia jest używany do analizy rozproszenia wartości określonych danych.
Jako argumenty funkcji scatter przekazujemy następujące parametry:
-	a - atrybut 'a' struktury danych data, zostanie użyty jako **wartość na osi 'x' wykresu**;
-	b - atrybut 'b' struktury danych data, zostanie użyty jako **wartość na osi 'y' wykresu**;
-	c - atrybut 'c' struktury danych data, zostanie użyty jako **kolor punktu na wykresie**;
-	d - atrybut 'd' struktury danych data, zostanie użyty jako **rozmiar punktu na wykresie**, argument ‘s’ znaczy ‘size’ czyli rozmiar;
-	data - przekazanie struktury danych data jako **źródła danych do wykresu**;

Oprócz tego przy pomocy metod **xlabel** i **ylabel** dodajemy podpisy do osi x i y odpowiednio. Aby wyświetlić wykres użyjemy polecenia **plt.show()**. Wynikiem działania kodu będzie wykres rozproszenia naszych wartości losowych, które wygenerowaliśmy wcześniej.

#### **Praca ze zmiennymi kategorycznymi**

W **Matplotlib** możliwe jest utworzenie wykresu na podstawie zmiennych kategorycznych. Zmienne kategoryczne można przekazywać do wielu funkcji odpowiedzialnych za rysowanie wykresu. W kolejnym przykładzie utworzymy 3 wykresy na podstawie jednego zestawu zmiennych kategorycznych. Typy wykresów które narysujemy, to wykres słupkowy, wykres punktowy oraz wykres linowy.

W tym przykładzie nowością będzie wywołanie funkcji **figure** z parametrem **figsize** oraz przyjrzymy się działaniu funkcji **subplot**.

Parametr **figsize** funkcji **figure** służy do przekazywania rozmiaru rysunku z wykresami w calach – pierwsza liczba oznacza długość wykresu (w naszym przykładzie 12), a druga liczba oznacza wysokość wykresu (w naszym przykładzie to 3).

Funkcja **subplot()** przyjmuje 3 argumenty
-	**numrows** - liczba wierszy;
-	**numcols** - liczba kolumn;
-	**plot_number** - numer / indeks / liczba porządkowa wykresu, która leży w przedziale od 1 do numrows x numcols (iloczynu);

Czyli każde wywołanie funkcji **subplot()** w bieżącym przykładzie można przypisać na:
-	plt.subplot(1, 3, 1)
-	plt.subplot(1, 3, 2)
-	plt.subplot(1, 3, 3)

Przecinki w wywołaniu funkcji **subplot()** nie są wymagane jeżeli numrows x numcols < 10. Na przykład wywołanie _subplot(131)_ jest równoznaczne z wywołaniem _subplot(1, 3, 1)_.

Dodajemy nazwę rysunku używając funkcji **suptitle** i wyświetlamy rysunek, używając funkcji **show**. Nazwa rysunku to 'Wykresy oparte o zmienne kategoryczne'. Po wyświetleniu rysunku spójrzmy na układ wykresów i porównajmy z tym, co już wiemy na temat funkcji **subplot**. Układ rysunków można opisać jako układ jednego wiersza i trzech kolumn, każdy wykres jest na swoim miejscu i ma swój indeks zgodnie z wywołaniem funkcji subplot. W opisie do wideo będzie link do strony z tekstem do tego wideo oraz przykłady w Jupyter Notebook. Zachęcam do zapoznania się z tymi materiałami i uruchomienia przykładów lokalnie na swoim komputerze. W ramach nauki można trochę poeksperymentować z przekazywanymi wartościami i zobaczyć jak będzie zmieniać się układ wykresów po zmianie argumentów funkcji **figure** i **subplot**.

Użyjmy danych i typów wykresów z poprzedniego przykładu, ale zmieńmy argumenty wywołania funkcji figure i subplot. Tym razem będzie to mniejszy rysunek o wymiarach 6 na 6, a układ wykresów będzie w kształcie tablicy o wymiarach 2 na 2. Co prawda mamy tylko 3 wykresy, a więc czwarty element tablicy będzie pusty.

W porównaniu z poprzednim przykładem różnica będzie w argumentach funkcji **figure** i **subplot**. Szczególnie proszę zwrócić uwagę na argumenty funkcji **subplot** – są to 221, 222 i 223 czyli liczba wierszy – 2, liczba kolumn – 2 oraz index od 1 do 3 – odpowiedni dla każdego wykresu.

#### **Praca z właściwościami linii**

Linie mają wiele atrybutów, które można ustawić i tym samym zmienić wygląd linii, na przykład:
-	**line width** - szerokość linii;
-	**dash style** - styl linii;
-	**antialiased** - określa czy ma być używane antialiased rendering czyli wygładzenie krawędzi linii, na słabszych komputerach ten atrybut może być przydatny;
-	lista wszystkich atrybutów jest dostępna <a href='https://matplotlib.org/3.1.0/api/_as_gen/matplotlib.lines.Line2D.html#matplotlib.lines.Line2D' target='_blank'>tu</a> – na stronie z dokumentacją **Matplotlib**;

Istnieje kilka możliwości ustawienia właściwości linii:
1.	poprzez użycie argumentów nazwanych;
2.	poprzez użycie metody do ustawiania wartości obiektu **Line2D**. Funkcja **plot()** zwraca listę obiektów o typie *Line2D*, na przykład line1, line2 = plot(x1, y1, x2, y2). W przykładzie poniżej przez funkcję **plot** zostanie zwrócona tylko jedna linia, czyli lista obiektów będzie miała długość 1.
3.	poprzez użycie metody **setp()** - można to rozszyfrować jako set parameter. Metoda **setp()** działa w 2 trybach: w trybie użycia argumentów nazwanych i w trybie podobnym do MATLAB. Szczegóły można zobaczyć w bieżącym przykładzie.

Dostępne właściwości Line2D są podane w <a href='https://matplotlib.org/3.1.0/api/_as_gen/matplotlib.lines.Line2D.html#matplotlib.lines.Line2D' target='_blank'>dokumentacji</a> **Matplotlib**.

Po wygenerowaniu rysunku z trzema wykresami można zauważyć jak każdy parametr użyty przy rysowaniu linii wpłynął na ostateczny wygląd linii.

Dziękuję za uwagę. Jeżeli wideo było pomocne i dowiedziałeś się czegoś nowego to proszę zlajkuj go. Jeżeli wciąż masz pytania, to proszę zadaj je w komentarzu do wideo. A jeżeli chcesz być na bieżąco i dowiadywać się jako pierwszy o nowych wideo to subskrybuj na kanał i kliknij dzwonek.
Tekst do tego wideo oraz przykłady kodu są dostępne na mojej stronie internetowej – link w opisie do wideo. Dziękuję.

Kod z przykładami w wideo w formacie Jupyter Notebook jest dostępny <a href="/assets/code/code_script_matplotlib_wideo_4.ipynb" download>tu</a>.