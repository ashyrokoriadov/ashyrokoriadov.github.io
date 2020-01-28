---
title: Wykres liniowy oraz wykres z pseudokolorami - wideo Matplotlib 6 6
subtitle: Tekst do wideo Matplotlib 6 6 na kanale YouTube
layout: page
show_sidebar: false
menubar: example_menu
author: andrew
category: Matplotlib
categories: matplotlib
---

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/LbVQpWmuaC8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

Witam na moim kanale. Temat dzisiejszego wideo oraz kilku kolejnych filmów będzie dokładne omówienie wszystkich najważniejszych typów wykresów dostępnych w bibliotece Matplotlib. W tym wideo zaprezentuję 2 typy wykresów ze wszystkimi szczegółami: wykres linowy oraz wykres z pseudokolorami.

#### **Wykres liniowy**

Jest najprostszym typem wykresu w bibliotece **Matplotlib**. Do narysowania prostego wykresu potrzebne są 2 tablice danych liczbowych, reprezentujących dane na osi X i na osi Y. Czasem w celach ćwiczenia potrzebujemy szybko wygenerować zestaw danych o określonych parametrach takich jak wartość minimalna, wartość maksymalna, odstęp pomiędzy wartościami. W takich przypadkach należy użyć biblioteki **numpy** do wygenerowania zestawów funkcją **arange**.

Przed narysowaniem każdego wykresu dobrą praktyką jest określenie rozmiarów rysunku wykresu. Podając parametr **figsize**, w calach, możemy dopasować wielkość wykresu do naszych potrzeb.

Czasem w ramach jednego rysunku będziemy chcieli wyświetlić kilka wykresów. To się przyda w przypadku wizualizacji danych wielowymiarowych, z ilością wymiarów powyżej 3. Również jest to pomocne, kiedy chcemy zwizualizować te same dane na różne sposoby. Do określenia pozycji wykresu używamy funkcji **subplot**.

Rysując wykres liniowy, używając funkcji **plot** w najprostszym wywołaniu musimy podać 3 parametry:
-	tablica wartości X
-	tablica wartości Y
-	kolor i formatowanie linii

W bieżącym przykładzie robimy 3 wizualizacji tego samego zestawu danych używając 3 różnych wywołań funkcji **plot**. Wykresami będą sinusoida i cosinusoida. Funkcja plot jest dość elastyczna i może przyjmować parametry o różnej postaci i o różnym typie. Można to zauważyć w wywołaniach 2 i 3:
1.	najprostsze wywołanie funkcji **plot** opisane wyżej - **plt.plot(x, y, 'r')**.
2.	do funkcji plot zostały podane minimalne 3 parametry 2 razy - **plt.plot(x, y, 'r--', x, z, 'g--')**.
3.	trochę przypomina wywołanie 1, jednak przekazaliśmy tutaj jeden wymiar tablicy 2-wymiarowej - **plt.plot(dataSin[0], dataSin[1], 'r*')**.

Rozmieszczając na rysunku kilka wykresów musimy zadbać o to, żeby poszczególne wykresy nie nachodziły na siebie. Kontrolowanie odstępów jest realizowane w bibliotece przez funkcję **subplots_adjust**.

Dodatkowa informacja o <a href="https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.plot.html#matplotlib.pyplot.plot" target="_blank">wykresach liniowych</a>. 

#### **Wykres z pseudokolorami**

Wykres z pseudokolorami przydaje się w sytuacjach kiedy trzeba zwizualizować dane 3D na płaszczyźnie 2D. W tym przypadku pierwsze 2 wymiary będą reprezentowały osie X i Y, natomiast 3 wymiar będzie reprezentowany przez odpowiedni kolor na wykresie.

Przed narysowaniem wykresu z pseudokolorami należy zdefiniować siatkę wykresu. Siatka wykresu jest 2D i składa się z wartości X i Y. W przykładzie poniżej do tworzenia siatki używamy metody **np.mgrid**. Jako element trzeciego wymiaru używamy dowolnej formuły - obecnie będzie to formula trygonometryczna **cos(x)^2 + sin(y)^2**. W ramach ćwiczenia polecam spróbować użyć formuł funkcji liniowej, kwadratowej, sześciennej i ocenić wizualizację.

Maksymalne wartości X i Y są granicami siatki. Wszystkie wartości Z powinny być obliczone na podstawie wartości X i Y w ramach granic siatki. To znaczy że nie możemy użyć na wykresie wartości Z obliczonej dla maksymalnych wartości X i Y czyli wartości granicznych X i Y. W tym celu usuwamy ostatni element tablicy Z.

Wartość Z na wykresie jest reprezentowana przez kolor. Do prawidłowej reprezentacji kolorów należy określić minimalną i maksymalną wartości tablicy Z oraz liczbę progów kolorów. Jest to parametr **nbins**. Im większa liczba progów tym bardziej płynne są przejścia pomiędzy kolorami, natomiast ze zwiększeniem liczby progów rysowanie wykresu jest mniej wydajne. Duża liczba progów nie jest zalecana w przypadku stosunkowo słabych komputerów.

W bieżącym przykładzie zostaną narysowane 2 wykresy z pseudokolorami z wartościami nbins 15 i 75, aby można było zobaczyć jak wpływa ten parametr na wizualizację.

Jako kolor wartości użyta została tak zwana mapa kolorów. Dostępne mapy kolorów są przedstawione na stronie dokumentacji biblioteki Matplotlib. Link jest w tekście do wideo, który jest dostępny na mojej stronie internetowej – link do strony w opisie do wideo. Każda z dostępnych map kolorów posiada odpowiednią odwróconą mapę kolorów. Na przykład domyślnie mapa kolorów Spectral pokazuje mniejsze wartości kolorem czerwonym, a większe wartości są granatowe. Załóżmy, że używamy tej mapy do wizualizacji temperatur i w zasadzie nie ma to zbytnio sensu gdyż wyższe temperature są granatowe. W tym przypadku należy użyć odwróconej mapy kolorów dla **Spectral**. Jest to bardzo proste - **odwrócona mapa kolorów to "nazwa mapy" + "_r"** czyli w naszym przypadku to będzie **Spectral_r**. 

Trzecim wykresem w bieżącym przykładzie będzie wykres z pseudokolorami narysowany przy pomocy metody **contourf**. Proszę porównać wynik działania tej funkcji z funkcją **pcolormesh**.

Dodatkowa informacja o <a href="https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.pcolormesh.html#matplotlib.pyplot.pcolormesh" target="_blank">wykresach z pseudokolorami</a>. 

To był ostatni przykład na dziś. Dziękuję za uwagę. Jeżeli wideo było pomocne i dowiedziałeś się czegoś nowego to proszę zlajkuj go. Jeżeli wciąż masz pytania, to proszę zadaj je w komentarzu do wideo. A jeżeli chcesz być na bieżąco i dowiadywać się jako pierwszy o nowych wideo to subskrybuj na kanał i kliknij dzwonek. Tekst do tego wideo oraz przykłady kodu są dostępne na mojej stronie internetowej – link w opisie do wideo. Dziękuję.

Kod z przykładami w wideo w formacie Jupyter Notebook jest dostępny <a href="/assets/code/code_script_matplotlib_wideo_6.ipynb" download>tu</a>.