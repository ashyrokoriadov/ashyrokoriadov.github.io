---
title: Wykres z tabelą danych i wykres punktowy - wideo Matplotlib 10 10
subtitle: Tekst do wideo Matplotlib 10 10 na kanale YouTube
layout: page
show_sidebar: false
menubar: example_menu
author: andrew
category: Matplotlib
categories: matplotlib
---

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/e3CKpsTHmCo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

Witam wszystkich na moim kanale. Dzisiaj rysujemy wykres z tabelą danych i wykres punktowy.

#### **Wykres z tabelą danych**

Do wykresu utworzonego w bibliotece **Matplotlib** możliwe jest dodanie tablicy z danymi, które są zwizualizowane na wykresie. Zwiększa to czytelność i zrozumiałość wykresu dla odbiorców. Dodanie tabeli do wykresu jest celem ćwiczenia zaprezentowanego w tym wideo.  W tym ćwiczeniu utworzymy wykres strat spowodowanych żywiołami. 

1.	Do wykresu będziemy potrzebowali danych:
-	**data** - właściwe dane: wiersze reprezentują dane dla poszczególnych przedziałów czasów (5, 10, 20, 50, 100), na przykład pierwsza tablica w tablicy **data** **[66386, 174296,  75131, 577908,  32015]** odnosi się do danych 5-letnich. W tabeli na wykresie te dane będą zaokrąglone do pierwszego znaku po przecinku;
-	**rows** - nazwy wierszy w tabeli: przedziały czasowe z formatowaniem, które dodaje słowo ‘lat’ po każdej wartości liczbowej;
-	**columns** - nazwy kolumn w tabeli, która będzie dodana pod wykresem: jest to tablica stringów  z nazwami żywiołów;
2.	Określamy podpisy **skali Y** na wykresie, ustawiając wartości zmiennych **values** przez użyciu funkcji arange z biblioteki **numpy** i **value_increment**.
3.	Pobieramy kolory do wykresu z odpowiedniej mapy kolorów **YlGn** i ustawiamy wartość zmiennej **colors**. Jako argument metody **YlGn** przekazujemy tablicę wartości typu **float** w przedziale od 0 do 0,75, odpowiadających wartościam w tablice **rows** czyli (5, 10, 20, 50, 100). Wartość typu **float** posłuży do określenia koloru każdej wartości w tablice **rows**.
4.	Wartości zmiennej **n_rows** będziemy potrzebowali do pętli, która pobiera dane do tablicy **cell_text**. Z kolei dane w tablicy **cell_text**  będą użyte do uzupełnienia tabeli pod wykresem.
5.	Zmienna **y_offset** przechowuje odstęp pionowy dla kolejnych wartości w słupku wykresu. To znaczy wartości z poszczegolnych kategorii będą dodane do tego samego słupka. Wartości dla określonego przedziału od 5 do 100 lat będą odpowiadać segmentom słupka o określonej wysokości i kolorze.
6.	W pętli dla każdej kategorii dodajemy wykres słupkowy poprzez wywołanie funkcji **bar**, określamy nową wartość zmiennej **y_offset** do wyświetlenia kolejnej wartości (tzn. kolejnego segmentu słupka) oraz dodajemy text do tablicy **cell_text** z formatowaniem. Formatowanie polega na podzieleniu przez 1000 z zaokrągleniem do pierwszego znaku po przecinku.
7.	Odwracamy kolory i dane w komórkach tabeli żeby najmniejsza wartość była na dole. W tym celu wywołujemy polecenie **colors[::-1]** i przypisujemy zwróconą tablicę do zmiennej **colors** oraz metodę **reverse()** na tablicy **cell_text**.
8.	Dodajemy tabelę do wykresu wywołując metodę **plt.table**: 
-	**cellText** - dane do tabeli
-	**rowLabels** - nazwy wierszy
-	**rowColours** - kolory wierszy
-	**colLabels** - nazwy kolumn
-	**loc** - miejsce rozmieszczenia wykresu odnośnie wykresu; możliwymi wartościami są: „top”, „bottom”, „left”, „right”.
8.	Używając polecenia **plt.subplots_adjust(left=0.1, bottom=0.1)** robimy miejsce na tabelę.
9.	Dodajemy i formatujemy podpisy na osiach, dodajemy nagłówek do całego rysunku. Polecenie **plt.xticks([])** usuwa jednostki z osi X, dodana tabela perfekcyjnie pełni rolę wyjaśnienia, czym są dane reprezentowane na wykresie.

Dodatkowa informacja o <a href="https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.table.html#matplotlib.pyplot.table" target="_blank">wykresach z tabelą danych</a>.

#### **Wykres punktowy**

Wykres punktowy służy do wizualizacji danych, które charakteryzują się przynajmniej 2 zmiennymi. Tłumacząc nazwę tego wykresu z języka angielskiego **scatter plot** dowiadujemy się, że jest to wykres rozproszenia. Faktycznie wykresy tego typu nadają się do wizualizacji grupowania danych i analizy klastrów.

Do ćwiczenia z wykresem będziemy potrzebowali danych: **X** i **Y**. Dane te wygenerujemy losowo używającą funkcji **random.rand** z biblioteki **numpy**. Wielkość zestawu danych to 50 elementów.  Przed wywołaniem funkcji **random.rand** dodamy wywołanie funkcji **random.seed**, podając jako argument jakąś stałą typu **integer**. To wywołanie zagwarantuje, że każde wywołanie **np.random.rand** wygeneruje zawsze taki sam zestaw danych. Bez wywołania funkcji seed, każdy nowy rysunek wykresu wyglądałby inaczej.

Tworzymy i uzupełniamy tablicę kolorów **colors**. Do tablicy **colors** wartości będą obliczone na podstawie mapy kolorów, w naszym przykładzie będzie to mapa ciepło-zimno. Jako argument metody coolwarm przekazujemy tablicę wartości typu float w przedziale od 0 do 1 o długości 50, odpowiadającą parom wartości w tablicach X i Y.

Wielkość punktów zostanie zapisana w tablicy **area**. Wartości tablicy będą obliczone na podstawie wzoru: losowa liczba jest mnożona przez 30 i podnoszona do potęgi 2 (drugiej).

Oprócz danych podstawowych na wykresie poniżej podajemy następujące parametry:
-	**c** - kolory punktów
-	**s** - wielkość punktów
-	**alpha** - przezroczystość

Dodatkowa informacja o <a href="https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.scatter.html#matplotlib.pyplot.scatter" target="_blank">wykresi punktowym</a>.

To był ostatni przykład na dziś. Dziękuję za uwagę. Jeżeli wideo było pomocne i dowiedziałeś się czegoś nowego to proszę zlajkuj go. Jeżeli wciąż masz pytania, to proszę zadaj je w komentarzu do wideo. A jeżeli chcesz być na bieżąco i dowiadywać się jako pierwszy o nowych wideo to subskrybuj na kanał i kliknij dzwonek. Tekst do tego wideo oraz przykłady kodu są dostępne na mojej stronie internetowej – link w opisie do wideo. Dziękuję.

Kod z przykładami w wideo w formacie Jupyter Notebook jest dostępny <a href="/assets/code/code_script_matplotlib_wideo_9.ipynb" download>tu</a>.