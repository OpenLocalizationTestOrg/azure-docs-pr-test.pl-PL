## <a name="install-hello-prerequisites"></a>Instalowanie wymagań wstępnych hello

Hello krokach tego samouczka przyjęto założenie, że używasz Ubuntu Linux.

Otwórz powłokę i uruchom następujące polecenia tooinstall hello wymagań wstępnych pakietów hello:

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

W powłoce hello Uruchom hello następujące polecenia tooclone hello Azure IoT krawędzi GitHub repozytorium tooyour komputera lokalnego:

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-toobuild-hello-sample"></a>Jak toobuild hello próbki

Hello krawędzi IoT można teraz tworzyć środowiska uruchomieniowego i przykłady, na komputerze lokalnym:

1. Otwórz powłokę.

1. Przejdź do folderu głównego toohello w lokalnej kopii hello **krawędzi iot** repozytorium.

1. Uruchom skrypt kompilacji w następujący sposób:

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

Ten skrypt używa **cmake** toocreate narzędzie folder o nazwie **kompilacji** w folderze głównym hello lokalną kopię **krawędzi iot** repozytorium i generowanie pliku reguł programu make. skrypt Hello następnie buduje rozwiązanie hello, pomijanie testów jednostkowych i tooend zakończenia. Toobuild i uruchom testy jednostkowe hello, Dodaj hello `--run-unittests` parametru. Toobuild i uruchom testy tooend zakończenia hello, Dodaj hello `--run-e2e-tests`.

> [!NOTE]
> Każdym uruchomieniu hello **build.sh** skryptu, usuwa, a następnie tworzy ponownie hello **kompilacji** folderu w folderze głównym hello kopii lokalnej hello **krawędzi iot** repozytorium.
