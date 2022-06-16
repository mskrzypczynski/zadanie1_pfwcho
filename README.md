# zadanie1_pfwcho
Zadanie1 z przedmiotu Programowanie Fullstack w Chmurze Obliczeniowej

##Programowanie Fullstack w Chmurze Oblczeniowej
### Sprawozdanie z Zadania 1

### CZĘŚĆ OBOWIĄZKOWA

1. Proszę napisać program serwera (dowolny język programowania), który realizować będzie
następującą funkcjonalność:

    a) po uruchomieniu kontenera, serwer pozostawia w logach informację o dacie uruchomienia, imieniu i nazwisku autora serwera (imię i nazwisko studenta) oraz porcie TCP, na którym serwer nasłuchuje na zgłoszenia klienta.
    ```bash
    docker-compose up --build
    ```
    ![image](https://user-images.githubusercontent.com/49763989/174054190-f37de31b-67a3-4756-a859-1070e8d24342.png)
    
    wyświetlenie logów z kontenera:
    ```bash
     docker logs -f zadanie1_pfwcho_web_1
    ```
    
    ![image](https://user-images.githubusercontent.com/49763989/174054498-8650c146-c246-4eb3-8ea0-c4da46f9ea32.png)


    b) na podstawie adresu IP klienta łączącego się z serwerem, w przeglądarce powinna zostać wyświetlona strona informująca o adresie IP klienta i na podstawie tego adresu IP, o dacie i godzinie w jego strefie czasowej.
    ![image](https://user-images.githubusercontent.com/49763989/174054892-8ae2947d-db80-45df-83cf-e50dd8bee533.png)

    
