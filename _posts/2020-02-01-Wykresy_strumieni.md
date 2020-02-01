---
title: Wykresy strumieni - wideo Matplotlib 8 8
subtitle: Tekst do wideo Matplotlib 8 8 na kanale YouTube
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

Witam wszystkich na moim kanale. Dzisiaj będziemy rozmawiać o **wykresach strumieni**, które są używane do wizualizacji wektorów 2D.

#### **Wykres strumieni**

**Wykres strumieni** jest rodzajem dwuwymiarowego wykresu pokazującego przepływ cieczy lub innych materiałów. 

Wygenerujemy dane do naszego przykładu z **wykresem strumieni**. W porównaniu z dotychczasowym przykładami będziemy potrzebowali trochę więcej różnych powiązanych zestawów danych. Będziemy potrzebowali 4 zestawy danych: 2 tablice jednowymiarowe, które będą określały siatkę przestrzeni wykresu oraz 2 tablice dwuwymiarowe, które będą określały prędkość na osiach x i y. W naszym przykładzie tablice jednowymiarowe oznaczymy dużymi literami **X** i **Y** zaś tablice dwuwymiarowe będą oznaczone dużymi literami **U** i **V**. Wartości **U** i **V** zależą od wartości **X** i **Y**, dlatego musimy wygenerować tylko wartości **X** i **Y**, a wartości **U** i **V** zostaną obliczone automatycznie. Do wygenerowania niezbędnych wartości zostanie użyta funkcja mgrid z pakietu **numpy**. Polecenie **np.mgrid**[-w:w:100j, -w:w:100j] wygeneruje 2 tablice jednowymiarowe o wymiarze 100, gdzie elementem tablicy będzie tablica o wymiarze 100 z elementami o wartościach od -w do w. Tak naprawdę **X** i **Y** są tablicami dwuwymiarowymi lub macierzą dwuwymiarową o rozmiarze 100 x 100, przy czym macierz **X** jest matrycą transponowaną do macierzy **Y**. Wartości tablic **U** i **V** zostaną obliczone przy pomocy prostych operacji matematycznych na tablicach **X** i **Y**. Oprócz zestawów **X**, **Y**, **U** i **V** będziemy potrzebowali jeszcze jednego parametru – nazwałem go **speed**. Zostanie on użyty do określania grubości linii w jednym z przykładów. Wartość parametru **speed** zostanie obliczona jako pierwiastek sumy kwadratów **X** i **Y**.

Standardowo dodajemy rysunek, używając polecenia **figure** o wymiarach 7 x 9 cali. Tym razem do podziału rysunku na poszczególne wykresy nie będziemy używać  funkcji **subplot**, tylko zostosujemy trochę inne podejście. Wywołanie funkcji **gridspec.GridSpec(nrows=3, ncols=2, height_ratios=[1, 1, 2])** definiuje układ wszystkich wykresów na rysunku:
 - 3 rzędy
 - 2 kolumny
 - wysokość 3 (trzeciego) rzędu równa się wysokości (pierwszego i drugiego rzędu) 1 i 2
 
Dodajemy pierwszy wykres strumieniowy na pozycji 0,0 rysunku. W wykresach strumieniowych ważnym parametrem jest gęstość (**density**). Ten parametr określa jak linie wykresu będą blisko siebie i jak często (gęsto) będą rysowane obok siebie. Właśnie, na pierwszym wykresie użyjemy tego parametru o wartości 0.25, 1. Na mojej stronie internetowej będzie dostępny tekst do tego wideo oraz przykłady kodu – zachęcam do eksperymentowania z tymi przykładami przez zmianę parametrów i obserwowanie wpływu zmian parametrów na wynik końcowy. Dodatkowo ustawiamy parametr **color** do pierwszego wykresu: literal ‘g’ znaczy ‘green’ czyli ‘zielony’.

Drugi wykres zostanie dodany na pozycji 0,1 rysunku. Na przykładzie tego wykresu zademonstruję rozwiązanie, w którym jako koloru wykresu wykorzystam mapę kolorów. Dodatkowo użyjemy parametru **linewidth** do określenia grubości linii na wykresie strumieniowym. Jako mapa kolorów zostanie użyta moja ulubiona mapa czyli **Spectral**. Jako wartość koloru użyjemy wartości tablicy **U**, która zostanie przekazana jako parametr ‘color’. W ramach ćwiczenia można sprawdzić jaki wygląd będzie miał wykres przy ustawieniu parametru ‘color’ na wartości **X**, **Y**, **V**. Jeżeli używamy mapy kolorów na wykresie, to dobrą praktyką jest dodawanie słupka kolorów, który określa mapowanie koloru do konkretnej wartości. Taki słupek można dodać przez wywołanie funkcji **fig.colorbar(strm.lines)** na obiekcie rusynku (**fig**), przekazując jako argument właściwość lines obiektu wykresu strumieniowego **strm**.

W trzecim przykładzie pokażę jak można sterować grubością linii i użyć tego parametru w swoich wizualizacjach. Na początku obliczymy grubość na podstawie parametru **speed**, który został wyliczony wcześniej. Formuła do obliczenia to **5 \* speed / speed.max()**. Przy pomocy parametru linewidth można określić grubość linii. Jeżeli ten parametr będzie zmieniał się stopniowo, można osiągnąć ciekawy efekt wizualny. Ten wykres zostanie dodany do rysunku na pozycji 1,0.

Czwarty przykład na pozycji 1,1 posłuży do demonstracji użycia punktów startowych. Używając parametru **start_points** możemy zdefiniować punkty, w których będą zaczynać się linie wykresu. Jako punkty startowe utworzymy tablicę dwuwymiarową o rozmiarze 2 x 6. Wymiar 0 to koordynata na osi X, wymiar 1 to koordynata na osi Y. Kiedy przekazujemy naszą tablicę jako argument do funkcji **streamplot**, robimy to z właściwością **T**. Ta właściwość oznacza, że zostanie przekazana macierz transponowana czyli przekazując tablicę, a właściwie macierz, o rozmiarze 2 x 6, zostanie przekazana macierz o wymiarze 6 x 2 czyli 6 punktów o koordynatach [x, y]. Oprócz tego argumentu przekazujemy również parametr grubości linii **linewidth** o wartości 2, parametr  mapy kolorów **cmap** o wartości **„autumn”** oraz parametr koloru **color** ustawiony na wartości tablicy **U**. 

Punkty startowe dodajemy do wykresu zwykłym wywołaniem funkcji **plot**. Jako trzeci argument przekazaliśmy wartość ‘bo’ czyli niebieskie punkty. Właśnie w taki sposób będą wyświetlone nasze punkty startowe na wykresie. Również ograniczamy zakres danych na osiach x i y wykres, używając funkcji **set** i ustawijając „**hurtowo**” kilka parametrów na raz – w tym przypadku ustawiam **xlim** i **ylim**. Wynikiem działania funkcji **streamplot** o takim zestawie argumentów jest wykres z 6 punktami startowymi i 6 liniami. Zwiększając liczbę punktów startowych zwiększamy proporcjonalnie liczbę linii na wykresie strumieniowym.

Ostatnim przykładem w tym wideo jest tworzenie maski czyli „przykrycia” na wykresie strumieniowym. 

- na początku należy utworzyć pustą tablicę o odpowiednim rozmiarze z danymi typu **bool**  przez wywołanie funkcji **np.zeros** z parametrem o wartości **U.shape**, czyli rozmiar tablicy odpowiadający rozmiarowi tablicy **U** oraz z argumentem nazwanym **dtype** o wartości **bool**;  
- część maski, która będzie służyła do ukrycia wykresu należy wypełnić wartością "True". W ramachach ćwieczenia można wypełnić część tablicy wartościam **NaN** i porównać efekt z efektem o wartości "True". W tym przykładzie wypełniamy środkową część przez wywołanie polecenia **mask[40:60, 40:60] = True** i początkową część wypełniamy wartościamy **NaN** przez wywołanie polecenia **U[:20, :20] = np.nan**;
- łączymy oryginalne dane z maską przez wywołanie polecenia **U = np.ma.array(U, mask=mask)**

Piąty wykres zostanie dodany na pozycji 2,0 rysunku. Standardowo dodajemy wykres poprzez polecenie **streamplot** i ustawimy jego nagłówek poprzez polecenie **set_title**. Do wykresu również dodamy maskę o skonfigurowanym wyglądzie. Obecnie w miejscu, gdzie mają pojawić się maski będą tylko puste białe miejsca. Maska technicznie, z punktu widzenia biblioteki Matplotlib, jest rysunkiem, dlatego żeby ją dodać i w jakiś sposób skonfigurować używamy funkcji **imshow**. O wyświetlaniu obrazków i pracy z nimi będziemy rozmawiać w jednym z kolejnych wideo. Na tę chwilą możemy tylko ograniczyć się do informacji, że będzie to szary kwadrat w środku wykresu. Aby nasz wykres miał kształt kwadratu i jego osie były w tej same skali musimy wywołać funkcję **set_aspect('equal')**. Innymi wartościami parametru funkcji **set_aspect** mogą być **'auto'** i **'number'**.

Ogólnie, żeby  wszystkie wykresy ładnie się ułożyły na rysunku, wywołujemy funkcję **tight_layout**.

To był ostatni przykład na dziś. Dziękuję za uwagę. Jeżeli wideo było pomocne i dowiedziałeś się czegoś nowego to proszę zlajkuj go. Jeżeli wciąż masz pytania, to proszę zadaj je w komentarzu do wideo. A jeżeli chcesz być na bieżąco i dowiadywać się jako pierwszy o nowych wideo to subskrybuj na kanał i kliknij dzwonek. Tekst do tego wideo oraz przykłady kodu są dostępne na mojej stronie internetowej – link w opisie do wideo. Dziękuję.

Kod z przykładami w wideo w formacie Jupyter Notebook jest dostępny <a href="/assets/code/code_script_matplotlib_wideo_8.ipynb" download>tu</a>.