---
title: Wprowadzenie do wykresów Matplotlib - wideo Matplotlib 1 1
subtitle: Tekst do wideo Matplotlib 1 1 na kanale YouTube
layout: page
show_sidebar: false
menubar: example_menu
author: andrew
category: Matplotlib
categories: matplotlib
---

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/gypYRaPuzhU" 
frameborder="0" 
allow="accelerometer; 
autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

Witam wszystkich na moim kanale. Mam na imię Andriej i pochodzę z Ukrainy. Programowaniem
interesuję się hobistycznie od wieku 11 lat, a od kilku lat jest to moje głowne źródło dochodu.
Programuję w językach C# i Python. To wideo jest pierwszym wideo szkoleniowym z zakresu
biblioteki Matplot lib.

Przypomnijmy sobie trochę z zajęć z matematyki. Najprostszym wykres jest wykres **2D** i składa się z
dwóch osi współrzędnych: osi X zwaną **osią odciętych** i osi Y zwaną **osią rzędnych**.
Na wykresie 2D można zwizualizować dane charakteryzujące się dwoma parametrami. Nazwy osi X i Y
są dość umowne. Na przykład oś X może być osią czasu, a oś Y może być osią temperatury. W tym
przypadku dane charakteryzujące zależność temperatury od czasu można zwizualizować na wykresie
2D.

Załóżmy że mamy zestaw danych z 2 punktów: (1,1) i (2,3). Dodajmy te punkty do wykresu.
Po dodaniu punktów otrzymaliśmy tak zwany wykres punktowy. Gdy połączymy te 2 punkty
otrzymamy inny rodzaj wykresu – wykres liniowy.

Inną powszechną formą wykresu jest wykres **3D**. Taki wykres służy do wizualizacji danych
charakteryzujących się trzema parametrami. Do już istniejących osi X i Y dodajemy **trzecią oś Z zwaną
kotą**.

Dodajmy do wykresu 3D 2 punkty (1,1,1) i (2,1,2). Rysowanie wykresów 3D jest nieco bardziej
skomplikowane. Wartości x i y należy odmierzyć na odpowiednich osiach tak samo jak w przypadku
wykresu 2D, natomiast wartość Z jest mierzona na osi wychodzącej z punktu (x, y) na płaszczyźnie
tworzoną przez osie X i Y i równoległej do osi Z.

W przypadku danych wielowymiarowych sprawy się komplikują. Załóżmy, że mamy dane, które
charakteryzują się czterema parametrami czyli są to dane **4D**. W tym przypadku korzystanie z
wykresu 3D nas nie urządza, dlatego że jeden wymiar pozostanie bez wizualizacji. Najczęściej dane
wielowymiarowe wizualizowane są przy pomocy kilku wykresów. Wykresy te mogą być różnego
rodzaju. Najważniejsze żeby były o tej samej skali, w celu łatwego czytania danych przez odbiorcę
wykresu.

W tym wideo do wizualizacji danych 4D użyjemy 2 wykresów. Jako przykładowy punkt 4D użyjemy
danych o następujących parametrach (x = 1, y = 3, z = 4, x1 = 2). Pierwszy wykres to wykres 3D na
którym zwizualizujemy zależność zmiennych y i z od zmiennej x. Drugi wykres, będzie to wykres 2D z
wizualizacją zależności zmiennej x1 od zmiennej x. Zachowanie skali w tym przykładzie jest dość
umowne, ale należy pamiętać, że przy rysowaniu wykresów przy pomocy narzędzi programistycznych
jest to łatwe do osiągnięcia.

Rysowanie drugiego wykresu 2D z osiami x i x1 najlepiej rozpocząć na tym samym poziomie co osie x i
y wykresu 3D. W takim układzie osoba czytająca wykres będzie mogła łatwo przełączać swoją uwagę
pomiędzy wykresami. Wybierając typy wykresów do wizualizacji danych wielowymairowych musimy
pamiętać o osobach, które będą z tych wykresów korzytać. Musimy być empatyczni i spojrzeć na
naszą wizualizację z perspektywy innego człowieka, któremu ta wizualizacja ma pomóc zrozumieć
reprezentowane dane. Być może warto spróbować poeksperymentować z różnymi typami wykresów:
na przykład użyć wykresu słupkowego zamiast histogramu i odwrotnie, albo użyć wykresu
punktowego zamiast liniowego.

O typach wykresów, które możemy narysować korzystając z biblioteki **Matplot lib** będziemy
rozmawawiać w kolejnych wideo szkoleniowych. Znajomość z biblioteką Matplot lib należy rozpocząć
od omówienia, z czego tak naprawdę składa się wykres w Matplot libie.

Każdy wykres, nie ważne czy jest narysowany od ręki czy przy pomocy jakiegoś narzędzia, posiada zdefiniowane elementy, bez których wykres nie mógłby być wykresem. Do tych elementów należą:
 - osie (*axes*)
 - linie (*lines / line plot*)
 - markery (*markers / scatter plot*)
 - nazwy osi (*axis labels*)
 - tytuł wykresu (*title*)
 - siatka (*grid*)
 - legenda (*legend*)
 
Do tego należy dodać kilka elementów używanych przez bibliotekę Matplotlib:

 - duże oznaczenie osi (*major tick*)
 - małe oznaczenie osi (*minor tick*)
 - podpis dużego oznaczenia osi (*major tick label*)
 - podpis małego oznaczenia osi (*minor tick label*)
 - obiekt wykresu w całości (*figure*)
 
 <img src="https://matplotlib.org/_images/anatomy.png" alt="Typowe elementy przykładowego wykresu w Matplotlib" width="550" height="550"/>

Osie 
: reprezuntują wymiary danych. Na przykład mając zbiór danych, składających się z dwóch wymiarów ([1,1], [5,3]) będziemy mieli wykres z 2 osiami. Zwykle oś pozioma ma oznaczenie X, oś pionowa ma oznaczenie Y, oś trzeciego wymiaru ma oznaczenie Z. 

Wykres 
: jest to graficzna reprezentacja danych

Markery 
: służą do zaznaczania danych lub wydzielenia okrślonego zestawu danych

Nazwy osi i tytuł całego wykresu 
: ułatwia czytanie wykresu dla odbiorców

Siatka 
: ułatwia określenie wielkości poszczególnych elementów wykresu

Legenda 
: pozwala opisać dane reprezentowane na wykresie

Oznaczenia osi 
: pokazuje skalę danych

Podpisy oznaczeń osi 
: określa skalę danych

Obiekt wykresu 
: obiekt w sensie programistycznym używany przez Matplotlib

Wszystkie elementy wykresu Matplotlib są przyporządkowane określonej hierarchii. Na górze hierarchii znajduje się obiekt wykresu w całości (*figure*), do którego są dodawane pozostałe elementy, między innymi osie. Wykres może zawierać dowolną liczbę osi, ale aby być użytecznym potrzebuje przynajmniej jednej osi.

Do pokazania przykładów **Matplot lib** użyjemy narzędzia **Jupyter Notebook** (link do narzędzia
znajduje się w opisie do wideo). To narzędzie służy do natychmiastowego wykonywania poleceń
Python i prezentacji wyników poleceń. Narzędzie to może zostać zainstalowane na komputerze lub
można z niego korzystać online.

Aby korzystać z biblioteki **Matplot lib**, musimy ją importować w kodzie Python.
Również do rysowania wykresów będziemy potrzebowali danych. Do generowania danych użyjemy
bibliteki numpy (link do dokumentacji biblioteki numpy znajduje się w opisie do wideo). Jest to
świetne narzędzie do korzystania z zestawów danych i tablic.

Używając funkcji **linspace** (x = np.linspace(0, 2, 100)) utworzymy tablicę jednowymiarową o rozmiarze
100 zawierającą elementy w przedziale [0:2]. Jak można się domyśleć, pierwszym argumentem
funkcji **linspace** jest wartość minimalna w generowanej tablicy, drugimy argumentem funkcji jest
wartość maksymalna tablicy, a trzeci argument jest długością wygenerowanej tablicy.
Jeżeli użyjemy polecenia **print(x)** możemy sprawdzić jaka tablica została wygenerowana przez
polecenie **linspace**. Jak widać wszystko zostało wygenerowano zgodnie z naszymi oczekiwaniami,
minimalny i maksymalny elementy to 0 i 2 odpowiednio, oraz długość tablicy mniej więcej wynosi
100 elementów.

Utworzymy wykres prostej fukcji liniowej o wzorze y = x. W tym celu zostanie wykorzystana funkcja z
biblioteki Matplot lib o nazwie **plot** z trzema argumentami. Pierwszy argument to zestaw wartości x,
drugim agrumentem jest zestaw wartości y, ale skoro y = x, to możemy znów użyć zestawu wartości
x, trzeci argument w tym konkretnym przykładzie to argument nazwany „label” – jego wartość
zastanie użyta przy tworzeniu legendy na wykresie.

W tym momencie do wykresu dodamy jeszcze 2 elementy: tytuł wykresu oraz legendę. Ułatwi to
odbiorcom naszego wykresu zrozumienie wizualizacji naszych danych. Tytuł jest dodawany przez
wykorzystanie polecenie title, a legenda – przez wywołanie polecenia legend. Do wyświetlenia
wykresu użyjemy funkcji show.

Domyślnym kolorem wykresu jest *kolor niebieski*. Zmiana domyślnego koloru będzie omawiana w
kolejnych wideo. Narysowaliśmy przy pomocy biblioteki Matplotlib nasz pierwszy wykres. Nie było to
zbyt skomplikowane.

Dodajmy teraz jeszcze 2 wykresy do naszego rysunku. Będą to wykresy funkcji kwadratowej i
sześciennej. Użyjemy już istniejącego kodu. Skopiujemy go i trochę zmienimy. Zmienimy również
wartość argumentu label w każdym z trzech wywołań funkcji plot, aby podpisy na legendzie
dokładnie opisywały wykresy.

Jak widać na jednej płaszczyżnie mamy 3 wykresy. Każde wywołanie funkcji **plot** dodaje wykres do
rysunku, a polecenie **show** tylko wyświetla rysunek na ekranie. Nie określaliśmy w jakim kolorze mają
być wykresy. Zostały one wybrane z domyślnej mapy kolorów. Na rysunku również mamy legendę,
która prawidłowo opisuje nasze dane. Ten prosty przykład jest pierwszym i ostatnim na dziś
przykładem rysowania wykresu przy użyciu biblioteki **Matplot lib**.

Dziękuję za uwagę. Jeżeli wideo było pomocne i dowiedziałeś się czegoś nowego, to proszę go
zlajkować. Przypominam że pomocne linki wspomniane w wideo zostały dodane do opisu na dole.
Jeżeli wciąż masz pytania, to proszę zadaj je w komentarzu do wideo. A jeżeli chcesz być na bieżąco i
dowiadywać się jako pierwszy o nowych wideo to subskrybuj ten kanał i kliknij dzwonek.

Tekst do niniejszego wideo oraz przykłady kodu są dostępne na mojej stronie internetowej – link w
opisie do wideo. Dziękuję.

Kod z przykładami w wideo w formacie Jupyter Notebook jest dostępny <a href="/assets/code/Code_script_matplotlib_wideo_1.ipynb">tu</a>.

<img src="/assets/test-page-image-1.jpg">
