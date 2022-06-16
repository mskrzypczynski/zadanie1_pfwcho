# zadanie1_pfwcho
Zadanie1 z przedmiotu Programowanie Fullstack w Chmurze Obliczeniowej
#### Repozytorium DockerHub: https://hub.docker.com/repository/docker/mikczynski/zadanie1_pfwcho


## Programowanie Fullstack w Chmurze Obliczeniowej
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
    
    kod źródłowy strony:
    ![image](https://user-images.githubusercontent.com/49763989/174055007-00341db9-713e-4971-bac4-682ff79812fc.png)

2. Opracować plik Dockerfile, który pozwoli na zbudowanie obrazu kontenera realizującego funkcjonalność opisaną w punkcie 1. Przy ocenie brane będzie sposób opracowania tego pliku (dobór obrazu bazowego, wieloetapowe budowanie obrazu, ewentualne wykorzystanie warstwy scratch, optymalizacja pod kątem funkcjonowania cache-a w procesie budowania). Dockerfile powinien również zawierać informację o autorze tego pliku (ponownie imię i nazwisko studenta).

    Plik Dockerfile:  
    ![image](https://user-images.githubusercontent.com/49763989/174055270-84b3c355-9f1e-46e6-8d5b-667a6eaa81e0.png)

    Plik docker-compose.yml:  
    ![image](https://user-images.githubusercontent.com/49763989/174055419-428325f8-f64a-4e28-9206-20d0df02033d.png)
    
 3. Należy podać polecenia niezbędne do:

    a) zbudowania opracowanego obrazu kontenera,
    ```bash
    docker-compose build
    ```  
    ![image](https://user-images.githubusercontent.com/49763989/174056312-ce42974d-ed92-4eb5-91fe-a51ec11c4e81.png)

    b) uruchomienia kontenera na podstawie zbudowanego obrazu,

    ```bash
    docker-compose up -d
    ```  
    ![image](https://user-images.githubusercontent.com/49763989/174056436-749049fd-700c-4cc9-abd4-b4adfd3238d3.png)
    
    c) sposobu uzyskania informacji, które wygenerował serwer w trakcie uruchamiana kontenera (patrz: punkt 1a),

    ```bash
    docker logs -f zadanie1_pfwcho_web_1
    ```
    ![image](https://user-images.githubusercontent.com/49763989/174056747-c0918403-7689-44b7-be4f-7df9de837048.png)

    d) sprawdzenia, ile warstw posiada zbudowany obraz.
    
    ```bash
    docker history zadanie1_pfwcho:v1
    ```

    ![image](https://user-images.githubusercontent.com/49763989/174057062-3e9bd64e-93b0-4936-85de-4525671359db.png)

4. Zbudować obrazy kontenera z aplikacją opracowaną w punkcie nr 1, które będą pracował na
architekturach: linux/arm/v7, linux/arm64/v8 oraz linux/amd64. Obrazy te należy przesłać do
swojego repozytorium na DockerHub. W sprawozdaniu należy podać wykorzystane instrukcje wraz
z wynikiem ich działania I ewentualnymi komentarzami.

Do zbudowania obrazów na podane architektury użyto docker buildx, kontenera multiarch/qemu-user-static.

Polecenia:
```bash
#uruchomienie kontenera z qemu
docker run --rm --privileged multiarch/qemu-user-static --reset -p yes
#utworzenie buildera
docker buildx create --name zadanie1_builder
#wybranie buildera do budowania obrazu
docker buildx use zadanie1_builder
#zbudowanie obrazu na 3 architektury i wysłanie do repozytorium
docker buildx build -f Dockerfile -t mikczynski/zadanie1_pfwcho:v1 --platform linux/amd64,linux/arm/v7,linux/arm/v8 --push .
#sprawdzenie czy obrazy zostały utworzone
docker buildx imagetools inspect mikczynski/zadanie1_pfwchho:1
```

![image](https://user-images.githubusercontent.com/49763989/174058679-74c2f590-70c2-46c6-9cdf-bc537df6b2a6.png)
![image](https://user-images.githubusercontent.com/49763989/174057656-48136de9-ae59-461e-8211-96c14317aec9.png)
![image](https://user-images.githubusercontent.com/49763989/174058613-1346a4cd-59a3-48aa-9693-c2e231d2a05e.png)

Widok z repozytorium dockerhub:
![image](https://user-images.githubusercontent.com/49763989/174062032-1f6ce70d-1c51-4180-bf38-b32ab8cc10f4.png)


### CZĘŚĆ DODATKOWA

- z wykorzystaniem GitHubActions

plik .yml w katalogu .github/workflows

![image](https://user-images.githubusercontent.com/49763989/174062636-6a8e7842-d9ba-4a01-ae06-6aca776fc70a.png)


