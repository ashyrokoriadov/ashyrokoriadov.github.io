---
title: Histogramy i wykresy 3D - wideo Matplotlib 7 7
subtitle: Tekst do wideo Matplotlib 7 7 na kanale YouTube
layout: page
show_sidebar: false
menubar: example_menu
author: andrew
category: Matplotlib
categories: matplotlib
---

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/om881WvEYSo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

Witam na moim kanale. W poprzednim wideo dokładnie omówiłem wykres liniowy oraz wykres z pseudokolorami z biblioteki **Matplotlib**. Tematem dzisiejszego wideo są histogramy oraz wykresy 3D. Szczególną uwagę chciałbym zwrócić na wykres 3D dlatego, że jest on poniekąd związany z wykresem z pseudokolorami. Wykres 3D, który zbudujemy w ramach dzisiejszego wideo, będzie 3D reprezentacją wykresu z pseudokolorami z poprzedniego wideo, a więc zachęcam do oglądania również poprzedniego nagrania.

#### **Histogramy**

**Histogram** – jeden z graficznych sposobów przedstawiania rozkładu empirycznego cechy. Składa się z szeregu prostokątów umieszczonych na osi współrzędnych. 

Na początku tworzymy dane do wizualizacji na histogramie, używając metod dostępnych w bibliotece numpy. Wywołanie **np.random.seed(19680801)** określa, że za każdym wywołaniem funkcji **np.random.randn** dostaniemy ten sam wynik i wygląd wykresu się nie zmieni. Parametry przekazane do funkcji **np.random.randn** określają rozmiar zwróconej tablicy. Pozostałe parametry to:
-	**mu** - wartość oczekiwana
-	**sigma** - odchylenie standardowe

Tworzymy dwa zestawy danych x i x2, które zostaną zwizualizowane na histogramie. W ramach przykładu utworzymy 4 histogramy, każdy o nieco innych parametrach, aby zaprezentować jak poszczególne wartości parametrów wpływają na wizualizację histogramu. 

Rysunek wykresu oraz poszczególne histogramy zostaną dodane przy użyciu już znanych nam funkcji figure i subplot. Funkcję figure wywołujemy z parametrem **figsize**.

Parametry funkcji **hist** użyte w przykładzie poniżej to:
-	**x** - dane do wizualizacji
-	**bins** - szerokość słupków histogramu, im mniejsza wartość, tym słupek jest szerszy
-	**density** - należy ustawić na True, aby histogram przedstawiał gęstość prawdopodobieństwa
-	**histtype** - rodzaj histogramu: możliwe wartości: 'bar', 'barstacked', 'step', 'stepfilled'
-	**alfa** - przezroczystość wizualizacji
-	**cumulative** -jest to wartość typu bool określająca czy każda kolejna wartość ma być sumą poprzednich wartości

Dodatkowo dla każdego wykresu ustawiamy ograniczenie wartości na osiach X i Y, nazwę wykresu oraz flagę czy ma być widoczna siatka wykresu przez użycie funkcji **grid**. Od razu powiem, że w ramach prezentacji jak działa ta funkcja, zabraknie siatki na drugim histogramie w dzisiejszym przykładzie.

Tak, jak już wspominałem zostaną narysowane 4 wykresy – każdy wykres o nieco zmienionych parametrach.

Wykres 1 – jest to reprezentacja podwójnego zestawu danych z typem histogramu **‘barstacked’** czyli słupki dla tej samej wartości X będą ułożone w stosie. Wartość parametru **bins** to 50, parametru **alpha** = 0.75.

Wykres 2 – jest to reprezentacja zestawu danych z parametrem **bins** równym 25 czyli słupki będą bardziej szerokie, wartość parametru **alpha** to 0.50. Dodatkowo zostanie usunięta siatka wykresu używając funkcji **grid** z parametrem _False_.

Wykres 3 – jest to reprezentacja zestawu danych w poziomie przez ustawienie parametru **„orientation”**. Jest ważne, aby pamiętać o odpowiedniej zmianie ograniczeń na osiach X i Y, ustawiając odpowiednie znaczenie przez wywołanie funkcji **xlim** i **ylim**. Wartość parametru **bins** to 75, parametru **alpha** = 0.25.

Wykres 4 – jest to reprezentacja zestawu danych z efektem kumulacyjnym, który jest osiągalny przez ustawienie flagi „**cumulative**”. Wartość parametru **bins** to 50, parametru **alpha** = 0.75.

Dodatkowa informacja o <a href="https://matplotlib.org/api/_as_gen/matplotlib.pyplot.hist.html" target="_blank">histogramach</a>.

#### **Wykresy 3D**

Aby zwizualizować trójwymiarowe dane należy takie dane posiadać oraz użyć parameteru **projection='3d'** w wywołaniu funkcji **fig.gca**. **GCA** to **get current access** - jeżeli figura nie posiada żadnej z osi, to automatycznie zostanie utworzona jedna oś.

W przykładzie z wykresem 3D będziemy używać kilka nowych funkcji, które zaraz omówię po kolei.

Wywołanie **ax.plot_surface** tworzy trójwymiarową powierzchnie na podstawie danych 3D.

Wywołanie **set_major_locator(LinearLocator(10))** określa ilość oznaczeń na osi, w tym przypadku będziemy mieli 10 oznaczeń.

Wywołanie **set_major_formatter(FormatStrFormatter('%.02f'))** określa format oznaczeń na osi, w tym przypadku będzie to wartość z dwoma znakami po przecinku.

Parametry wywołania **fig.colorbar** (mapowanie wartości Z do koloru):
-	**surf** - powierzcznia, która została użyta w wykresie 3D
-	**shrink** - współczynnik, o który zostaną pomnożone wymiary paska kolorów
-	**aspect** - współczynnik wysokości do szerokości paska kolorów

Jeżeli porównać kod od wywołania funkcji **gca** do wywołania funkcji **plot_surface**, to można zauważyć że jest on bardzo podobny do kodu z przykładu z wykresem w pseudokolorach w poprzednim wideo. Po zbudowaniu wykresu 3D zachęcam do porównania wizualizacji wykresu z pseudokolorami z wykresem 3D.

Dodatkowa informacja o <a href="https://matplotlib.org/tutorials/toolkits/mplot3d.html#toolkit-mplot3d-tutorial" target="_blank">wykresach 3D</a>.

To był ostatni przykład na dziś. Dziękuję za uwagę. W kolejnym wideo zaprezentuję wykres strumieni i wykres słupkowy. Jeżeli wideo było pomocne i dowiedziałeś się czegoś nowego to proszę zlajkuj go. Jeżeli wciąż masz pytania, to proszę zadaj je w komentarzu do wideo. A jeżeli chcesz być na bieżąco i dowiadywać się jako pierwszy o nowych wideo to subskrybuj na kanał i kliknij dzwonek. Tekst do tego wideo oraz przykłady kodu są dostępne na mojej stronie internetowej – link w opisie do wideo. Dziękuję.

Kod z przykładami w wideo w formacie Jupyter Notebook jest dostępny <a href="/assets/code/code_script_matplotlib_wideo_7.ipynb" download>tu</a>.

