---
title: Kilka wykresów Matplotlib na jednym rysunku - wideo Matplotlib 2 2
subtitle: Tekst do wideo Matplotlib 2 2 na kanale YouTube
layout: page
show_sidebar: false
menubar: example_menu
author: andrew
category: Matplotlib
categories: matplotlib
---

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/Ab5MoQWJUA8" 
frameborder="0" allow="accelerometer; autoplay; 
encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

Witam wszystkich na moim kanale. Mam na imię Andriej i pochodzę z Ukrainy. Programowaniem interesuję się hobistycznie od wieku 11 lat, a od kilku lat jest to moje głowne źródło dochodu. Programuję w językach C# i Python. To wideo jest drugim wideo szkoleniowym z zakresu biblioteki Matplot lib. W tym wideo pokażę jak na jednym rysunku zamieścić kilka wykresów  używając osobne osie dla każdego wykresu.

Poprzednio pokazałem jak utworzyć prosty wykres przy pomocy biblioteki **Matplotlib**. Ten przykład opierał się na założeniu, że wszystkie wykresy będą budowane w ramach tego samego systemu osi czyli wykresy będą krzyrzować się i mieć tę samą skalę. Czasem do wizualizacji danych wielowymiarowych nie jest to porządane i chcielibyśmy rozdzielić wizualizacje jednocześnie pozostawiąjąc je na tym samym rysunku.

Nowy rysunek z kilkoma wykresami utworzymy korzystając z tego samego pliki Jupyter notebook co poprzednio. Na początek skopiujemy już instniejące importy niezbędnych bibliotek. Dalej będziemy potrzebowali danych do wizualizacji. Do wygenerowania tych danych skorzystamy z funkcji linspace użytej w poprzednim wideo. Funkcja ta jest dostępna w bibliotece **numpy**. W odórżnieniu od poprzedniego wideo utworzymy 2 zakresy danych po jednym dla każdej osi. Zakres dla osi x będzie w przedziale od -2 do 2, zaś zakres dla osi y będzie w przedziale od -5 do 5. Liczba elementów w obu zakresach równa się 100.

Do budowy wykresu użyjemy funkcji **figure**. Ta funkcja zwraca nam obiekt całego rysunku z którym możemy pracować. W tym przykładzie wywołujemy funkcje **figure** bez argumentów na potrzeby uproszczenia przykładu, natomiast w kolejnych wideo będziemy omawiać argumenty funkcji **figure** bardziej szczegółowo. Do obiektu rysunku który został zwrócony przez funkcję **figure** możemy dodać wykresy podrzędne tzw. **subplots**. Z kolei każdy wykres podrzędny będzie zajmował swoje określone miejsce na rysunku ogólnym.

Wywołujemy funkcje **subplots** używając 2 argumentów typu integer. Pierwszy argument to liczba wierszy na rysunku ogólnym w których mogą mieścić się wykresy podrzędne. Drugim argumentem jest liczba kolumn na rysunku ogólnym w których możemy umieścić wykresy podrzędne. A więc aby odwołać się do konkretnego wykresu podrzędnego będziemy używać numeru wiersza i kolumny na rysunku ogólnym. Należy pamiętać że numeracja wierszy i kolumn zaczyna się od 0.

Ustawiamy odstępy pomiędzy wykresami podrzędnymi funkcją **subplots_adjust**. Domyślne znaczenia argumentów funkcji *subplots_adjust* to
* *left* = 0.125  - lewa strona wykresu podrzędnego
* *right* = 0.9   - prawa strona wykresu podrzędnego
* *bottom* = 0.1  - dół wykresu podrzędnego
* *top* = 0.9     - góra wykresu podrzędnego
* *wspace* = 0.2  - odstęp w poziomie pomiędzy wykresami podrzędnymi, jako odsetek średniej długości osi poziomej
* *hspace* = 0.2  - odstęp w pionie pomiędzy wykresami podrzędnymi, jako odsetek średniej długości osi pionowej

Należy pamiętać że wartość *left* ma być mniejsza od wartości *right* oraz wartość *bottom* ma być mniejsza od wartości *top*

Aby wyjaśnić bardziej dokładnie jak należy rozumieć wierszy i kolumny rysunku ogólnego, narysuję prosty przykład w aplikacji Paint. Jest to zwykły prostokąt podzielony na 4 cześci. Możemy umówić się, że każda z czterech części ma swoje własne koordynaty. Koordynaty do prostokątów będą nadawane w taki sam sposób jak bibilioteka **Matplotlib** nadaje koordynaty do wykresów podrzędnych na rysunku ogólnym. 

Korzystając z tego schematu zaczynamy liczyć koordynaty od górnego lewego rogu. W taki sposób możemy określić koordynaty każdego z czterech prostokątów. Lewy górny prostokąt ma koordynaty 0,0. Prawy górny - ma koordynaty 0,1. Lewy dolny prostokąt ma koordynaty 1,0, a ostatni prawy dolny prostokąt ma koordynaty 1,1.

Wywołanie funkcji **subplots** zwraca oprócz obiektu **figure**, obiekt **axes**. Jest to tablica dwuwymiarowa zawierająca koordynaty wykresów podrzędnych. Przy pomocy tej tablicy odwolujemy się do poszczegónych wykresów podrzędnych.

Ustawiamy parametry dla pierwszego wykresu podrzędnego. Na elemencie o indeksie 0,0 w tablice **axes** wywolujemy następujęce metody:
 - **plot** – czyli dodawanie wykresu podrzędnego. Pierwszym wykresem będzie wykres liniowy o kącie nachylenia 45 stopnie w kolorze czerwonym. Parametr **c** to kolor linii wykresu i w tym przypadku jest on ustawiony na ‘r’ czyli „red”;
 - **set_xlabel** i **set_ylabel** – dodawanie podpisów do osi wykresu podrzędnego; 
 - wywołanie **set_text** na obiekcie **title** – to jest dodawanie nagłówku wykresu podrzędnego;
 - **legend** – dodawanie legendy;
 
Wyświetlamy wykres funkcją **show**. Jak widzimy na rysunku ogólnym nasz wykres podrzędny pojawił się w tym miejscu gdzie oczekiwaliśmy – na miejscu o koordynatach 0,0. Zostały wyświetlone również i inne miejsca przygotowane do wykresów podrzędnych.

Dodajmy teraz drugi wykres na miejscu o koordynatach 0,1. Będzie to funkcja kwadratowa o kolorze żółtym. Do dodania  wykresu możemy posłużyć się kodem już użytym do dodawania pierwszego wykresu podrzędnego. W celu uproszczenia tego przykładu skopiujemy i wkleimy podobny kod, natomiast gdyby to był kod produkcyjny zalecane jest napisanie funkcji która będzie zawierać w sobie całą funkcjonalność dodawania wykresu podrzędnego. Napisanie takiej funkcji nie jest celem tego przykładu i dlatego ten krok pominiemy. 

Zwróćmy uwagę na to w jaki sposób została dodana legenda do drugiego wykresu podrzędnego i porównajmy rozmieszczenie legendy na dwóch wykresach podrzędnych. Ta obserwacja nasuwa wniosek, że jeżeli nie podamy żadnych argumentów w wywołaniu funkcji legend, biblioteka Matplot lib wybierze najbardziej optymalne miejsce rozmieszczenie legendy wykresu.

Dodajemy trzeci i czwarty wykresy podrzędne na miejsca o koordynatach 1,0 i 1,1 odpowiednio. Trzeci wykres będzie wykresem funkcji sześciennej o kolorze zielonym, natomiast czwarty wykres to prosta linia równoległa do osi odciętych o kolorze niebieskim. Zwóćmy uwagę że w wywołaniu funkcji plot dla czwartego wykresu nie podajemy koloru. Kolor niebieski jest kolorem domyślnym w bibliotece **Matplotlib**.

W tym wideo do jednego rysunku dodaliśmy 4 wykresy podrzędne. Taka wizualziacja jest przydatna do analizy danych wielowymiarowych. W kolejnych wideo przejrzymy się bardziej dokładnie jak działa funkcja **plot** i jakich argumentów należy używać do maksymalnie efektywnego i efektownego wykorzystania funkcji **plot** w bibliotece **Matplotlib**.

Dziękuję za uwagę. Jeżeli wideo było pomocne i dowiedziałeś się czegoś nowego to proszę go zlajkować. Jeżeli wciąż masz pytania, to proszę zadaj ich w komentarzu do wideo. A jeżeli chcesz być na bierząco i dowiadywać się pierwszym o nowych wideo to subskrybuj na kanał i kliknij dzwonek.

Tekst do tego wideo oraz przykłady kodu są dostępne na mojej stronie internetowej – link w opisie do wideo. Dziękuję.

Kod z przykładami w wideo w formacie Jupyter Notebook jest dostępny <a href="/assets/code/code_script_matplotlib_wideo_2.ipynb" download>tu</a>.