---
title: Podpisy, teksty i skale na wykresach Matplotlib - wideo Matplotlib 5 5
subtitle: Tekst do wideo Matplotlib 5 5 na kanale YouTube
layout: page
show_sidebar: false
menubar: example_menu
author: andrew
category: Matplotlib
categories: matplotlib
---

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/dBeJJkGaO-8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

Witam wszystkich na moim kanale. Dzisiaj będziemy rozmawiać o podpisach i tekstach, które możemy dodać do naszego wykresu, ulepszając jego czytelność i zrozumiałość dla odbiorców.

#### **Praca z tekstem na wykresie**

Funkcja **text()**, z którą dzisiaj się zapoznamy, może być wykorzystana do dodania tekstu w dowolnym miejscu na wykresie, podobnie jak funkcje **xlabel()**, **ylabel()** i **title()** są używane do dodania tekstu w określonych miejscach na wykresie.

**Matplotlib** przyjmuje wyrażenia **TeX** w każdym miejscu, gdzie jest dozwolone przekazanie tekstu. Na przykład: **σi=15** w nagłówku może zostać przekazane jako **plt.title(r'$\sigma_i=15$')**. Litera r na początku nagłówka jest ważna - wskazuje ona, że jest to zwykły string i nie należy traktować \ jako escape symbol.

W ramach przykładu utworzymy histogram danych, który będzie reprezentował zestaw danych o określonej wartości oczekiwanej i odchyleniu standardowym. Wartość oczekiwana zostanie oznaczona jako „mu”, odchylenie standardowe – jako „sigma”; wartości danych zostaną umieszczone w zmiennej „x”.

W naszym przykładzie funkcja hist przyjmuje kilka argumentów. Wśród nich:
- argument **„facecolor”** – argument określający kolor histogramu; w naszym przykładzie to ‘g’ czyli ‘green’;
- argument **„alpha”** – argument, który określa przezroczystość wykresu; w naszym przykładzie przezroczystość wynosi 75% czyli wartość argumentu alpha powinna być 0.75.

Standardowo podpisujemy wykres używając funkcji **xlabel**, **ylabel**, **title**. Ograniczymy zakres osi x od 40 do 160 jednostek, zaś zakres osi y od 0 do 0.03 jednostek. Dodatkowo dodamy siatkę na wykresie wywołując funkcję grid z argumentem True.

W celu dodania podpisu na wykresie użyjemy funkcji **text**. W naszym przykładzie funkcja **text** przyjmuje 3 argumenty:
-	pierwszy argument to koordynata x – w przykładzie to 60;
-	drugi argument to koordynata y – w przykładzie to 0.025;
-	trzeci argument to **text**, który chcemy umieścić na wykresie. Tak jak już wspominałem wcześniej może to być **tekst** w formacie **Tex**. Link z dodatkowymi informacjami na temat format **Tex** zostanie umieszczony w opisie wideo.

W opisie wideo znajdzie się również link do strony z tekstem do niniejszego wideo oraz przykłady w **Jupyter Notebook**. Zachęcam do zapoznania się z tymi materiałami i uruchomienia przykładów lokalnie na swoim komputerze. W ramach nauki można trochę poeksperymentować z przekazywanymi wartościami i zobaczyć jak będzie się zmieniać widok tekstu na wykresie po zmianie argumentów funkcji **text**.

#### **Praca z adnotacjami**

Wykorzystywanie podstawowej funkcji **text()** w opisie powyżej pozwala na umieszczenie tekstu w dowolnym miejscu na wykresie. Najbardziej rozpowszechnionym użyciem tekstu na wykresie jest adnotacja jakiejś właściwości zamieszczonej na rysunku. W tym przypadku funkcja **annotate()** wprowadza dodatkową funkcjonalność w celu ułatwienia dodania adnotacji. 

W adnotacjach należy rozważyć dwa argumenty: rozmieszczenie właściwości, która jest adnotowana i rozmieszczenie tekstu. Oba argumenty mają postać krotności (x,y).

W ramach przykładu narysujemy wykres funkcji cosinus. Jako źródło danych x posłuży tablica utworzona przez funkcję **np.arange**. Tablica będzie zawierać elementy w przedziale od 0 do 5 z krokiem 0.01 czyli sumarycznie 500 wartości. Wartości tablicy użyjemy jako argumentów funkcji **np.cos**.

Dalej użyjemy funkcji **annotate** do dodania 2 strzałek i 2 podpisów. Ze względu na to, że podpisy będą podobne i będą umieszczane w tym samym miejscu, będą one wyglądały jako jeden podpis. Funkcja **annotate** przyjmuje kilka argumentów:
-	pierwszy argument w naszym przykładzie to tekst, który chcemy dodać;
-	drugi argument w naszym przykładzie to **„xy”** – czyli punkt końcowy strzałki, zaś punkt początkowy jest umieszczony w miejscu gdzie jest dodany tekst;
-	trzeci argument w naszym przykładzie to **„xytext”** – jest to koordynata punktu, w którym zostanie umieszczony tekst, równocześnie jest to punkt początkowy strzałki;
-	czwarty argument to **„arrowprops”** czyli właściwości linii – tutaj przekazujemy słownik dict zawierający 2 właściwości – kolor strzałki i zmniejszenie jej rozmiaru;

Dodatkowo ograniczamy zakres osi y wykresu od -2 do 2 używając funkcji **ylim**. Standardowo wyświetlamy wykres używając polecenia **show**.

#### **Praca ze skalą logarytmiczną i innymi rodzajami skal**

**Matplotlib** wspiera nie tylko skale liniowe. Wspiera również skale logarytmiczne i logitowe. Skale te są używane w przypadku bardzo dużych zakresów danych. Zmiana typu skali jest łatwa i jest dokonywana przez użycie funkcji **xscale** lub **yscale**.

W tej części przeanalizujemy przykład składający się z 4 wykresów z podobnymi danymi o różnych skalach. Na początku zrobimy import klasy **NullFormater**. Klasy tej użyjemy do formatowania małych oznaczeń osi Y na puste łańcuchy znaków,  aby uniknąć nałożenia dużej ilości oznaczeń osi na siebie.  

W celu przygotowywania danych do wykresów użyjemy funkcji **np.random.normal** oraz funkcji **np.random.seed** ze stałym argumentem typu **integer**, aby wygenerowane dane losowe zawsze były takie same.

Na rysunku przy użyciu funkcji subplot dodamy 4 wykresy z różnymi skalami:
-	linową
-	logarytmiczną
-	logarytmiczna symetryczną
-	logitową

Czym jest skala liniowa nie wymaga dodatkowego wyjaśnienia, natomiast przyjrzymy się pozostałym trzem skalom. 

**Skala logarytmiczna** jest to rodzaj skali pomiarowej, w której mierzona wartość wielkości fizycznej jest przekształcana za pomocą logarytmu. Skale logarytmiczne są szeroko stosowane w nauce i technice dla odwzorowania wielkości, które przyjmują wartości z szerokiego zakresu.

**Skala logarytmiczna symetryczna** to jest inny rodzaj  logarytmicznej skali pomiarowej. Różnice pomiędzy skalą logarytmiczną a logarytmiczną symetryczną są następujące:
-	skala logarytmiczna pozwala tylko na wartości dodatnie;
-	skala logarytmiczna symetryczna pozwala na wartości dodatnie i ujemne;
-	w skali logarytmicznej symetrycznej można określić zestaw wartości w okolicach 0, który będzie liniowy, a nie logarytmiczny;

**Skala logitowa** jest to rodzaj skali pomiarowej opartej o funkcję logitową, która jest stosowana w statystyce (jako metoda regresji logistycznej) do przekształcania prawdopodobieństwa na logarytm szans.

To był ostatni przykład na dziś. Dziękuję za uwagę. Jeżeli wideo było pomocne i dowiedziałeś się czegoś nowego to proszę zlajkuj go. Jeżeli wciąż masz pytania, to proszę zadaj je w komentarzu do wideo. A jeżeli chcesz być na bieżąco i dowiadywać się jako pierwszy o nowych wideo to subskrybuj na kanał i kliknij dzwonek. Tekst do tego wideo oraz przykłady kodu są dostępne na mojej stronie internetowej – link w opisie do wideo. Dziękuję.

Kod z przykładami w wideo w formacie Jupyter Notebook jest dostępny <a href="/assets/code/code_script_matplotlib_wideo_5.ipynb" download>tu</a>.