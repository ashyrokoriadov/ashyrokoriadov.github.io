---
title: Wykres z wypełnieniem i wykres w układzie współrzędnych biegunowych - wideo Matplotlib 11 11
subtitle: Tekst do wideo Matplotlib 11 11 na kanale YouTube
layout: page
show_sidebar: false
menubar: example_menu
author: andrew
category: Matplotlib
categories: matplotlib
---

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/TrXNatB5SNM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

Witam wszystkich na moim kanale. Dzisiaj rysujemy wykres z wypełnieniem i wykres w układzie współrzędnych biegunowych.

#### **Wykres z wypełnieniem**

Do demonstracji wykresu z wypełnienim użyjemy wykresu okręgu, a dokładniej narysujemy 3 półokrągi o średnicy 1.00, 0.75 i 0.50. Półokrągi będą wypełnione kolorami:
-	okrąg o średnicy 1.00 - **kolor czerwony**
-	okrąg o średnicy 0.75 - **kolor niebieski**
-	okrąg o średnicy 0.50 - **kolor biały**

W tym ćwiczeniu bardziej wymagające jest określenie koordynat wykresu niż samo rysowanie. W tym celu została utworzona funkcja **get_coordinates** przujmująca jeden parametr **size**. 
-	Do wygenerowania wartości **x** użyjemy funkcji **np.arrange** z pakietu **NumPy**. Zakres wartości zależy od średnicy okęgu. Wybór kroku (w naszym przypadku to 0.001) zależy od tego, na ile płynny ma być nasz wykres.
-	Ostatni element o wartości **size** nie jest dodawany do tablicy przez funkcję **np.arrange**, dlatego dadamy ten element poprzez wywołanie polecenia **x = np.append(x, size)**.
-	Fromuła okręgu to **x^2 + y^2 = R^2** czyli do obliczenia wartości y należy użyć formuły **math.sqrt(size^2-value^2)**. 

Obiekt rysunku o rozmiarach **8 x 8** standardowo dodajemy poleceniem **plt.figure** z parametrem **figsize**. Ważne jest, aby koordynaty **X** i **Y** były równe, dlatego wywołujemy polecenie **plt.axis** z parametrem **„equal”**.
Im później jest rysowany wykres, tym wyżej **"leży"** on na płaszczyźnie, dlatego rysujemy mniejsze półokrągi później w kodzie, używając polecenia **plt.fill()**, podając 3 parametry: wartości **X** i **Y** oraz kolor wypełnienia **c**. W kodzie będą 3 wywołania metody **get_coordinates** i **plt.fill()**.
Wyświetlamy wykres poleceniem **plt.show()**.

Dodatkowa informacja o <a href="https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.fill.html#matplotlib.pyplot.fill" target="_blank">wykresach z wypełnieniem</a>.

#### **Wykres w układzie współrzędnych biegunowych**

W zasadzie rysowanie wykresu w układzie współrzędnych biegunowych nie róźni się od rysowania zwykłych wykresów. 

Do wygenerowania wartości kąta **fi** (w kodzie tablica **xs**) użyjemy funkcji **np.arrange** z pakietu **NumPy**. Zakres wartości od 0 do 20. Wybór kroku (w naszym przypadku to 0.01) zależy od tego na ile płynny ma być nasz wykres. W celu ułatwienia przykładu wartości **r** będą zależać od wartości kąta **fi**. Formuła do obliczenia **r** to fi do potęgi 2.

Obiekt rysunku o rozmiarach 5 x 5 standardowo dodajemy poleceniem **plt.figure** z parametrem **figsize**.

Jako parametry funkcji **plt.polar()** są przekazywane wartości kąta **fi**, odłegłości **r**, kolor linii (niebieski czyli wartość parametru to ‘b’) oraz grubość linii wykresu (w naszym przykładzie to 3). 

Dodatkowa informacja o <a href="https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.polar.html#matplotlib.pyplot.polar" target="_blank">wykresi w układzie współrzędnych biegunowych</a>.

To był ostatni przykład na dziś. Dziękuję za uwagę. Jeżeli wideo było pomocne i dowiedziałeś się czegoś nowego to proszę zlajkuj go. Jeżeli wciąż masz pytania, to proszę zadaj je w komentarzu do wideo. A jeżeli chcesz być na bieżąco i dowiadywać się jako pierwszy o nowych wideo to subskrybuj na kanał i kliknij dzwonek. Tekst do tego wideo oraz przykłady kodu są dostępne na mojej stronie internetowej – link w opisie do wideo. Dziękuję.

Kod z przykładami w wideo w formacie Jupyter Notebook jest dostępny <a href="/assets/code/code_script_matplotlib_wideo_11.ipynb" download>tu</a>.