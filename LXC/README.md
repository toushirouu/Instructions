# Instrukcja tworzenia i podstawowej konfiguracji kontenera LXC pod serwisy
## Wymagania systemowe
- Ubuntu 20.04 (focal) lub nowsze
- Instalacja lxc
    ```bash
    sudo apt install lxc lxc-templates -y
    ```
## Podstawowe komendy
Należy pamiętać, że wszystkie komendy lxc wykonujemy z **sudo**
1. Tworzenie kontenera - *lxc-create*
    ```bash
    lxc-create --name nazwa_nowego_kontenera --template download -- --dist dystrybucja_linuxa_kontenera --release wersja_dystrybucji --arch architektura_np.amd64 
    ```
    - Przykład użycia stworzenia kontenera ubuntu20 (focal):
        ```bash
        lxc-create --name ubuntu_kontener --template download -- --dist ubuntu --release focal --arch amd64
        ```
2. Wyświetlenie statusów kontenerów *lxc-ls -f* (dzięki fladze -f jest widocznych więcej parametrów)
    ```bash
    lxc-ls -f
    ```
3. Startowanie kontenera *lxc-start*
    ```bash
    lxc-start ubuntu_kontener
    ```
4. Podłączanie się do kontenera *lxc-attach*
    ```bash
    lxc-attach ubuntu_kontener
    ```
5. Odłączanie się od kontenera
    ```bash
    exit
    ```
5. Stopowanie kontenera *lxc-stop*
    ```bash
    lxc-stop ubuntu_kontener
    ```
6. Usuwanie kontenera *lxc-destroy*
    ```bash
    lxc-destroy ubuntu_kontener
    ```
## Case tworzenie kontenera ubuntu20 i podstawowej konfiguracja
Po każdym korku można podglądać status kontenera przy użyciu lxc-ls -f
1. Stworzyć kontener
    ```bash
    lxc-create --name ubuntu_kontener --template download -- --dist ubuntu --release focal --arch amd64
    ```
2. Uruchomić kontener
    ```bash
    lxc-start ubuntu_kontener
    ```
3. Podłączyć się pod kontener
    ```bash
    lxc-attach ubuntu_kontener
    ```
4. Na tym etapie jesteśmy już w kontenerze i np. można coś tam zainstalować, np. nano do wygodniejszej edycji plików tekstowych i polski language-pack (przez jego brak czasami pokazują się irytujące warningi)
    ```bash
    apt install nano language-pack-pl -y 
    ```
5. Kończąc pracę na terminalu kontenera możemy z niego wyjść za pomocą komendy *exit*
    ```bash
    exit
    ```
    Opuszczenie terminalu kontenera nie jest jednoznaczne z wyłączeniem go. Kontener pozostanie włączony. Status kontenerów można podejrzeć za pomocą *lxc-ls -f*
