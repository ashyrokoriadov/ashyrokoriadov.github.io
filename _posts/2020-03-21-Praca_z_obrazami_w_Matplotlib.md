---
title: Praca z obrazami w bibliotece Matplot lib - wideo Matplotlib 12 12
subtitle: Tekst do wideo Matplotlib 12 12 na kanale YouTube
layout: page
show_sidebar: false
menubar: example_menu
author: andrew
category: Matplotlib
categories: matplotlib
---

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/Vhw7w6AdHGM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

Witam wszystkich na moim kanale. Witam wszystkich na moim kanale. Dzisiaj rozmawiamy o obrazach w bibliotece Matplotlib.

#### **Obrazy w bibliotece Matplot lib**

Praca z obrazami w **Matplot lib** jest możliwa dzięki bibliotece **Pillow**. Biblioteka **Matplot lib** sama w sobie wspiera tylko obrazy w formacie **PNG**. Przykłady użyte w tym materiale będą korzystać z biblioteki Pillow jeżeli **Matplot lib** nie będzie w stanie odczytać obrazu. W przykładach będzie wykorzystany obraz w formacie PNG, ale należy pamiętać, że jeżeli planujecie używać innych formatów obrazów, to zapoznanie się z wymaganiemi Pillow jest konieczne.

Spróbujemy wczytać obraz, używając polecenia **mpimg.imread**. Dalej zobaczymy co udało nam się odczytać, używając polecenia **print**. Jak można zauważyć obraz to tablica 3D, w tym konkretnym przypadku o wymiarach **1224 x 1632 x 4** Pierwsze dwie wartości to rozmiar obrazu w pixelach. Trzecia wartość określa kolor punktu na obrazie. 

**Matplot lib** zmienił kolor z każdego kanału na wartość typu **float** w przedziale od 0.0 do 1.0. Każda lista wewnętrzna reprezentuje pixel. Jest to kolorowy obraz czyli obraz RGBA (A to wartość **alpha**, inaczej przezroczystość: 1 - nie przezroczysty, 0 - przezroczysty). Obraz czarno-biały będzie miał 3 (trzy) jednakowe wartości bez wartości **alpha**. Obraz, który będzie charakteryzował się tylko jasnością powierzchniową (**luminance image**), będzie miał tylko jedną wartość. 

**Matplot lib** wspiera tylko typy **float32** i **uint8** dla obrazów **RGB** i **RGBA**. W przypadku obrazów czarno-białych **Matplot lib** wspiera tylko **float32**. Jeżeli twoje dane nie spełniają tych wymagań, prawdopodobnie będziesz musiał zmienić format twoich danych.

Mamy nasze dane w postaci tablicy **numpy**. Trzeba je zwizualizować. W tym celu użyjemy biblioteki **Matplot lib** i polecenia **imshow()**. W wyniku wywołania tego polecenia dostajemy obiekt rysunku. Używając tego obiektu, możemy w łatwy sposób manipulować rysunkiem. 

#### **Pseudokolor na wykresach z obrazami**

**Pseudokolor** może być użyteczny do podkreślenia kontrastu i łatwiejszej wizualizacji danych. To jest szczególnie użyteczne w trakcie przeprowadzenia prezentacji danych z użyciem rzutników - zazwyczaj ich kontrast jest słaby. Pseudokolor może być zastosowany tylko w obrazach jednokanałowych czyli takich, które charakteryzują się tylko jasnością powierzchniową (**luminance image**).

Do przykładu używamy zdjęcia **RGB**. Aby zastosować pseudokolor należy wziąć tylko jeden kolor. Jak zaobserwujemy na poniższym przykładzie - nie jest ważne (lub mało ważne) jaki kanał weźmiemy. 

-	Do trzech zmiennych **lum_img_channel** przypisujemy wartości każdego kanału. 

-	Dodajemy rysunek z trzema wykresami o wymiarach **15 x 15**, używając funkcji **subplot**, zwracając obiekty rysunku i osi.

-	Do każdej osi reprezentującej miejsce na rysunku dodajemi rysunek z pseudokolorami, używając jednej z trzech zmiennych z pseudokolorami. Dodanie rysunku realizujemy poprzez wywołanie metody **imshow** obiektu osi. Jako parametry metody przekazujemy dane kanału czyli odpowiednia zmienna **lum_img_channel** oraz nazwa mapy kolorów, którą chcemy użyć. W naszym przykładzie będziemy używać mapy **„summer”**, **„winter”** i **„hot”**.

Można zmieniać mapy kolorów na istniejącym wykresie, używając metody **set_cmap()**. Link do listy dostępnych map kolorów zostanie umieszczony w opisie do wideo.

Czasem może okazać się pomocne dla zrozumienia wizualizacji jakie wartości reprezentuje kolor. Do wyświetlania panelu kolorów służy metoda **plt.colorbar**. Warto sobie przypomnieć, że panel kolorów nie zaktualizuje się automatycznie, jeżeli zmienimy mapę kolorów. W celu aktualizacji panelu kolorów należy ponownie narysować wykres i dodać jeszcze raz panel kolorów.

#### **Sprawdzenie specyficznych zakresów danych obrazu**

W niektórych rozwiązaniach biznesowych może pojawić się zadanie zwiększenia kontrastu w konkretnym regionie obrazu, nie zwracając uwagi na pogorszenie kontrastu w innych regionach. W tym celu najlepszym narzędziem będzie histogram czyli użycie metody **hist()**.

Wszystko "najciekawsze" będzie w okolicach szczytów histogramu. Można dodać extra kontrast do określonego regionu, określając jego górną i/lub dolną granicę.

Zawsze można ustawić wartość **clim** na zwróconym obiekcie.

#### **Schematy interpolacji**

Interpolacja oblicza na podstawie różnych algorytmów matematycznych, jaki kolor lub wartość pixela "powinna być" użyta. To się zdarza, kiedy wymiary obrazów są zmieniane. Liczba pixeli zmienia się, ale nadal chcemy pozyskać tą samą informację. Obraz to zestaw danych dyskretnych, czyli przy zmianie rozmiaru powstają brakujące miejsca. Interpolacja służy do tego, aby te miejsca wypełnić.

W poniższym przykładzie używamy biblioteli **Pillow** do załadowania obrazu i zmniejszenia jego wymiarów. Jeżeli nie podamy argumentu interpolation zostanie użyta wartość domyślna - **bilinear**. Na wykresie są również przykłady z interpolacjami typu **nearest** i **bicubic**. Interpolacja **nearest** w zasadzie nie robi interpolacji, a **bicubic** tworzy rozmyte obrazy. Jeżeli chodzi o interpolacje **bicubic**, to użytkownicy preferują mieć rozmyte obrazy, a nie z dużymi pixelami.

To był ostatni przykład na dziś. Dziękuję za uwagę. Jeżeli wideo było pomocne i dowiedziałeś się czegoś nowego to proszę zlajkuj go. Jeżeli wciąż masz pytania, to proszę zadaj je w komentarzu do wideo. A jeżeli chcesz być na bieżąco i dowiadywać się jako pierwszy o nowych wideo to subskrybuj na kanał i kliknij dzwonek. Tekst do tego wideo oraz przykłady kodu są dostępne na mojej stronie internetowej – link w opisie do wideo. Dziękuję.

Kod z przykładami w wideo w formacie Jupyter Notebook jest dostępny <a href="/assets/code/code_script_matplotlib_wideo_12.ipynb" download>tu</a>.