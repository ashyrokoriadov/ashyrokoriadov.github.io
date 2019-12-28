---
title: Różne sposoby wywołania funkcji plot() - wideo Matplotlib 3 3
subtitle: Tekst do wideo Matplotlib 3 3 na kanale YouTube
layout: page
show_sidebar: false
menubar: example_menu
author: andrew
category: Matplotlib
categories: matplotlib
---

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/KpGpyvqHHEM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

Witam wszystkich na moim kanale. To wideo jest trzecim wideo szkoleniowym z zakresu biblioteki **Matplotlib**. W tym wideo pokażę  w jaki sposób i z jakimi argumentami możemy wywołać funkcję plot(). 

Ogólnie rzecz biorąc rysowanie wykresów w **Matplotlib** jest bardzo proste. Używamy różnych funkcji do dodawania do wykresu różnych obiektów (dane, opisy, legendy) lub zmieniając ich stan.

W pierwszym przykładzie jako argument funkcji **plot** przekażemy tablicę zawierającą 4 elementy. Pewnie patrząc na kod i wynik jego działania, zastanawiacie się nad kilkoma kwestiami:
-	Jak działa funkcja plot? 
-Jak jest interpretowana tablica *[1, 2, 3, 4]* przez plot? 

W przypadku podanym powyżej każdy element tablicy *[1, 2, 3, 4]* został potraktowany jako wartość na osi y. Wartości na osi x zostały dopasowane automatycznie do każdego elementu tablicy. W języku Python pierwszy index to 0. Stąd wartości osi x to *[0, 1, 2, 3]*.

Funkcja **plot** jest dość uniwersalna i może przyjmować dowolną liczbę argumentów. Na przykład można podać 2 tablice reprezentujące wartości x i y równocześnie. W przykładzie 2 przekazujemy  dwie tablicy jako argumenty do funkcji **plot**: pierwsza tablica z wartościami x w zakresie od -5 do 5 oraz druga tablica z wartościami y które są kwadratami wartości x.

Jak widzimy na rysunku z przykładu 2 wartości pierwszej tablicy znalazły się na osi X oraz wartości drugiej tablicy są na osi Y.

Dla każdej pary X i Y można podać trzeci nie wymagany argument określający kolor i typ linii na wykresie. Domyślna wartość tego argumentu to 'b-' co znacza, że będzie to linia ciągła (-) o kolorze niebieskim (b). Wartości tego argumentu pochodzą z **MATLAB** oraz są dostępne w dokumentacji funkcji **plot()**.

Gdybyśmy chcieli narysować wykres składający się z zielonych markerów w kształcie gwiazdki, to należałoby użyć następującego kodu w którym trzeci argument to „g*”.

Biblioteka **Matplotlib** pozwala na określenie minimalnej i maksymalnej wartości na osiach X i Y używając funkcji **axis()**. Funkcja ta przyjmuje 4 argumenty *[xmin, xmax, ymin, ymax]*. W ramach przykładu dodajmy ograniczenie do poprzedniego wykresu.

Przy próbie uruchomienia kodu z bieżącego przykładu pojawił się błąd. Komunikat o błędzie jednoznacznie określa co było przyczyną blędu – jest nią nieprawidłowa deklaracja import. Po poprawce wszystko powinno działać jak należy.

W ramach przykładu dodaliśmy ograniczenie na oś X w zakresie od 0 do 6 i na oś Y w zakresie od 0 do 30.

Jako parametry liczbowe najlepiej używać tablic **numpy array**. De facto wszystkie tablice przekazywane do funkcji **plot()** wewnętrzenie są konwertowane do **numpy array**. Następny przykład przedstawia użycie tablicy numpy do rysowania kilku wykresów o różnych stylach.

Do generowania danych użyjemy funkcji arange z biblioteki numpy. Tę funkcję użyjemy z trzema argumentami:
-	0. - wartość początkowa tablicy
-	5. - wartość końcowa tablicy
-	0.2 - wartość kroku

W wyniku otrzymamy tablicę jednowymiarową o długości 25.

Tym razem do funkcji **plot** przekazujemy 9 argumentów. Te 9 argumentów można podzielić na 3 grupy. Każda grupa składa się z trzech arumentów: wartości x, wartości y oraz parametr określający kolor i styl linii wykresu. Po przekazaniu 9 argumentów możemy spodziewać się 3 wykresów na rysunku. 

Przy próbie uruchomienai kodu powstał błąd – problemem był nieprawidłowy argument w funkcji **plot**. Drugim problemem była literówka w nazwie funkcji **arange**.

W dzisiejszym wideo poznaliśmy niektóre argumenty i sposoby wywołania funkcji **plot**. W kolejnych wideo będziemy zajmować się pracą z różnymi typami danych w bibliotece **Matplotlib**.

Dziękuję za uwagę. Jeżeli wideo było pomocne i dowiedziałeś się czegoś nowego, to proszę go zlajkować. Przypominam że pomocne linki wspomniane w wideo zostały dodane do opisu na dole. Jeżeli wciąż masz pytania, to proszę zadaj je w komentarzu do wideo. A jeżeli chcesz być na bieżąco i dowiadywać się jako pierwszy o nowych wideo to subskrybuj ten kanał i kliknij dzwonek.
Tekst do niniejszego wideo oraz przykłady kodu są dostępne na mojej stronie internetowej – link w opisie do wideo. Dziękuję.

Kod z przykładami w wideo w formacie Jupyter Notebook jest dostępny <a href="/assets/code/code_script_matplotlib_wideo_3.ipynb" download>tu</a>.