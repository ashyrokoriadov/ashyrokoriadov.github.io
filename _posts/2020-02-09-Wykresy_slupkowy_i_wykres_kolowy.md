---
title: Wykres słupkowy i wykres kołowy - wideo Matplotlib 9 9
subtitle: Tekst do wideo Matplotlib 9 9 na kanale YouTube
layout: page
show_sidebar: false
menubar: example_menu
author: andrew
category: Matplotlib
categories: matplotlib
---

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/1AMoeG6QgqI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

Witam wszystkich na moim kanale. Dzisiaj rysujemy wykresy słupkowe i kołowe.

#### **Wykres słupkowy**

Ten rodzaj wykresu używany jest w przypadku prezentacji częstości wystąpienia określonych zjawisk, odpowiedzi, kategorii, charakterystyk lub w przypadku podziału jakieś liczby na kategorie, w tym przypadku każdy słupek odpowiada określonej kategorii, natomiast wysokość słupka odpowiada wartości liczbowej charakteryzującej daną kategorię.

Do ćwiczenia będzie potrzebny zestaw danych: kategorie **X** i odpowiadające kategorii wartości **money**.

Obecnie kategorie **X** to tylko tablica o długości 4 elementów z wartościami od 0 do 3. Tę tablicę otrzymaliśmy używając funkcji **arange** z pakietu numpy, podając jeden argument typu integer, oznaczający liczbę elementów w tablicy wynikowej. 

Wartości w tablice **money** zapisane są w formacie naukowym. Format naukowy to rodzaj formatu, w którym liczby są wyświetlane w notacji wykładniczej, zastępująca część liczby znakiem **e +n**, w której wartość **e**, czyli wykładnik, mnoży poprzednią liczbę o 10 do n-tej potęgi. Na przykład w formacie 2-dziesiętnym w formacie naukowym jest wyświetlana wartość 12345678901 w postaci 1.23 E + 10, co daje 1,23 od 10 do 10 potęgi. Na przykład pierwsza wartość w tablice money to 1.5e5, która oznacza wartość 1.5 * 10^5 lub 150 000.

Zdefiniujemy funkcje **millions**, która zostanie użyta do formatowania wartości na osy Y. Wartości w formacie naukowym zostaną przeformatowane na wartości typu float z dokładnością do pierwszego miejsca po przycinku z dodaniem znaku $ na początku wartości i litery M na końcu. **Funkcja millions** zostanie przekazana jako argument konstruktora obiektu **FuncFormatter**. Ten obiekt, z kolei, zostanie przekazany jako argument do metody **set_major_formatter** obiektu **yaxis**. W taki sposób fukcja millions zostanie użyta do formatowania wartości na osi Y wykresu.

Standardowo tworzymy obszar rysunku z wykresami używając funkcji **subplots**. Tym razem do rysunku dodamy 2 wykresy z podobnymi wartościami. Wykresy będą się różnić formatowaniem osi, właściwie pierwszy wykres będzie miał osie z formatowaniem, a drugi – bez formatowania.

Kategorie w niniejszym przykładzie prezentują ludzi o imionach Bill, Fred, Mary i Sue. Żeby zmapować kategorie 0,1,2,3 na imiona użyjemy funkcji **plt.setp**, która jako parametry przyjmuje:
-	oś, której dotyczy mapowanie nazw
-	dane wejściowe [0,1,2,3]
-	dane wyjściowe [Bill, Fred, Mary, Sue]

Wykres słupkowy rysujemy używając funkcji **bar**, która w naszym przykładzie przyjmuje 2 argumenty: zestaw dany do osi X (tablica x) oraz zestaw danych do osi Y (tablica money). Aby sformatować oś Y wykresu należy użyć funkcji **yaxis.set_major_formatter(formatter)**. 

Wywołanie **plt.xticks(x, x)** przywraca znaczenie podpisów osi X do wartości z tablicy [0,1,2,3].

Korygujemy układ wykresów poleceniem **plt.subplots_adjust** i wyświetlamy rysunek używając polecenia **plt.show**.

#### **Diagram kołowy**

**Diagram kołowy** używany jest w przypadku konieczności reprezentacji proporcji poszczegónych kategorii. Na diagramie kołowym długość łuku każdego wycinka (a także kąt środkowy na którym się opiera i pole powierzchni jaki wyznacza), jest proporcjonalna do ilości jaką przedstawia. Wszystkie wycinki diagramu zawsze tworzą pełne koło.

Jako danych do diagramu kołowego użyjemy 4 kategorii **labels** z odpowiednimi wartościami **sizes** reprezuntująymi proporcje. Suma wszystkch wartości w tablicy sizes równa się 100. Wartościami tablicy labels będą artykuły biurowe.

Cały wykres będzie się składał z 4 mniejszych wykresów.

Do rysowanie wykresu kołowego używamy funkcji **pie**, która ma następujące parametry: 
-	**explode** - tablica o wielkości odpowiadającej liczbie kategorii. Każda wartość w tablicy explode określa o ile ta konkretna kategoria zostanie odsunięta od wykresu. W ramach ćwiczenia można poeksperymentować z różnymi wartościami;
-	**size / labels** - właściwie są to dane, które tworzą diagram: wartości oraz ich podpisy;
-	**autopct** - format wyświetlania wartości na diagramie, brak parametru skutkuje brakiem wyświetlania wartości na poszczególnych częściach diagramu;
-	**shadow** - określa czy diagram ma rzucać cień;
-	**startangle** - kąt początkowy, przy czym za wartość 0 przyjmuje się linia pozioma od środka diagramu w prawo;

Narysujemy 4 wykresy i każdy wykres będzie różnił się przede wszystkim wartościami użytych parametrów. Odwołujemy się do poszczególnych wykresów jak do elementów tablicy dwuwymiarowej.

Pierwszy wykres będzie rysowany z wysuniętą drugą kategorią oraz kątem początkowym o wartości 0. Początkiem wykresu jest linia pomiędzy niebieską kategorią „Pióra” oraz czerwoną kategorią „Markery”. Kąt początkowy jest kątem pomiędzy linią opisaną wcześniej, czyli początkiem wykresu, a wyobrażalną osią X. Dodatkowo dla każdego wykresu przy pomocy metody **axis**, która jest wywoływana z parametrem „**equal**”, zapewniamy, że wykres kołowy będzie miał kształt kręgu.

Drugi wykres cechuje się bardziej wysuniętą kategorią „Ołówki” oraz kątem początkowym o wartości 90. Bardziej wysunięta kategoria „Ołówki” to wynik ustawienia większej wartości w tablicy **explode**. Jeżeli chodzi o kąt początkowy to jeżeli porównamy ułożenie wykresu z wykresem 1, zauważymy, że jest on obrócony o 90 stopni.

W trzecim wykresie wysuwamy już 2 segmenty wykresu przez ustawienie odpowiednich wartości w tablice **explode**. Tradycyjnie zwiększamy kąt początkowy. Tym razem jego wartość wynosi 180 stopni: wykres 3 jest obrócony o 90 stopni w porównaniu z wykresem 2 i o 180 stopni w porównaniu z wykresem 1. Dodatkowo ustawiliśmy parametr **Shadow** na **False**, co usunęło cień na trzecim wykresie w porównaniu z wykresami 1 i 2.

Przez ustawienie wszystkich wartości większych od zera w tablicy **explode** osiągamy ciekawy efekt odsunięcia od siebie wszystkich segmentów wykresu kołowego na wykresie 4. Kąt początkowy jest ustawiony na 270 stopni, co jest równoznaczne z ustawieniem wartości na -90 stopni.

To był ostatni przykład na dziś. Dziękuję za uwagę. Jeżeli wideo było pomocne i dowiedziałeś się czegoś nowego to proszę zlajkuj go. Jeżeli wciąż masz pytania, to proszę zadaj je w komentarzu do wideo. A jeżeli chcesz być na bieżąco i dowiadywać się jako pierwszy o nowych wideo to subskrybuj na kanał i kliknij dzwonek. Tekst do tego wideo oraz przykłady kodu są dostępne na mojej stronie internetowej – link w opisie do wideo. Dziękuję.

Kod z przykładami w wideo w formacie Jupyter Notebook jest dostępny <a href="/assets/code/code_script_matplotlib_wideo_9.ipynb" download>tu</a>.