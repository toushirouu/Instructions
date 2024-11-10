# Instrukcja instalacji i konfiguracji Jenkinsa na kontenerze LXC
## Stworzenie kontenera LXC
1. Stwórz kontener LXC o nazwie ubuntu_jenkins, na którym będzie hostowana owa usługa
    ```bash
    lxc-create --name ubuntu_jenkins --template download -- --dist ubuntu --release focal --arch amd64
    ```
2. Wystartuj kontener ubuntu_jenkins
    ```bash
    lxc-start ubuntu_jenkins
    ```
3. Podłącz się pod kontener ubuntu_jenkins
    ```bash
    lxc-attach ubuntu_jenkins
    ```
4. Korzystając z [Instrukcji](https://www.jenkins.io/doc/book/installing/linux/) zainstaluj na kontenerze Jenkinsa w wersji *Long Term Support release* - do wykonania opisanych kroków najpierw trzeba zainstalować program **wget**, który jest użyty w krokach instalacyjnych oraz Javy, która jest wymagana przez Jenkinsa. Czyli najpierw
    ```bash
    apt update
    apt install wget fontconfig openjdk-17-jre
    ```
    Następnie przejść przez [Instrukcję](https://www.jenkins.io/doc/book/installing/linux/) dla wersji *Long Term Support release*

5. Po instalacji można sprawdzić czy Jenkins jest uruchomiony
    ```bash
    systemctl status jenkins
    ```
    Jeśli jest "Active: active (running)" to jest git
6. Wychodzimy z kontenera za pomocą *exit*
    ```bash
    exit
    ```
    I sprawdzamy ip kontenera, aby podłączyć sie do Jenkinsa (patrzymy na kolumnę **IPV4**)
    ```bash
    lxc-ls -f 
    ```
## Konfiguracja Jenkinsa
1. Wklejamy ip do przeglądarki i dopisujemy :8080, gdyż na takim porcie defaultowo uruchamiany jest Jenkins, np.
    ```
    10.0.3.196:8080
    ```
2. Pokaże nam się strona, w której trzeba wpisać wygenerowane hasło administratora, aby dokończyć konfigurację Jenkinsa. Wchodzimy na kontener i w lokalizacji */var/lib/jenkins/secrets/initialAdminPassword* odczytujemy hasło
    - Podłączamy się pod kontener
        ```bash
        lxc-attach ubuntu_jenkins
        ```
    - Odczytujemy hasło i wklejamy je w pole w przeglądarce
        ```bash
        cat /var/lib/jenkins/secrets/initialAdminPassword
        ```
3. Wybierając pluginy, które mają zostać zainstalowane (np. obsługa gita na Jenkinsie, wysyłanie emaili z powiadomieniami), klikamy w *Install suggested plugins*
4. Tworzymy użytkownika admina - podajemy fake Full name i E-mail address
5. Jenkins URL pozostawiamy bez zmian
