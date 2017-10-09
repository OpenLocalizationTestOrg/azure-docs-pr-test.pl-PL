## <a name="install-hello-prerequisites"></a>Instalowanie wymagań wstępnych hello

1. Zainstaluj [programu Visual Studio 2015 lub 2017](https://www.visualstudio.com). Można użyć hello, które spełniają wymagania licencyjne hello w warstwie bezpłatna wersja Community. Należy się tooinclude Visual C++ i Menedżer pakietów NuGet.

1. Zainstaluj [git](http://www.git-scm.com) i upewnij się, że git.exe można uruchomić z wiersza polecenia hello.

1. Zainstaluj [CMake](https://cmake.org/download/) i upewnij się, że cmake.exe można uruchomić z wiersza polecenia hello. CMake wersji 3.7.2 lub nowszy jest zalecane. Witaj **.msi** Instalator jest najłatwiejsza opcja hello w systemie Windows. Dodaj CMake toohello po wyświetleniu monitu Instalatora hello ścieżki dla co najmniej hello bieżącego użytkownika.

1. Zainstaluj [Python 2.7](https://www.python.org/downloads/release/python-27). Upewnij się, że możesz dodać Python tooyour `PATH` zmiennej środowiskowej w **Panel sterowania -> System -> Zaawansowane zmiennych środowiskowych -> Ustawienia systemu**.

1. W wierszu polecenia Uruchom hello następujące polecenia tooclone hello Azure IoT krawędzi GitHub repozytorium tooyour komputera lokalnego:

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-toobuild-hello-sample"></a>Jak toobuild hello próbki

Hello krawędzi IoT można teraz tworzyć środowiska uruchomieniowego i przykłady, na komputerze lokalnym:

1. Otwórz **wiersz polecenia dla programu VS 2015 deweloperów** lub **wiersz polecenia dla programu VS 2017 deweloperów** wiersza polecenia.

1. Przejdź do folderu głównego toohello w lokalnej kopii hello **krawędzi iot** repozytorium.

1. Uruchom skrypt kompilacji w następujący sposób:

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

Ten skrypt tworzy plik rozwiązania Visual Studio i tworzy hello rozwiązania. Witaj rozwiązania Visual Studio można znaleźć w hello **kompilacji** folderu w lokalnej kopii hello **krawędzi iot** repozytorium. Toobuild i uruchom testy jednostkowe hello, Dodaj hello `--run-unittests` parametru. Toobuild i uruchom testy tooend zakończenia hello, Dodaj hello `--run-e2e-tests`.

> [!NOTE]
> Każdym uruchomieniu hello **build.cmd** skryptu, usuwa, a następnie tworzy ponownie hello **kompilacji** folderu w folderze głównym hello kopii lokalnej hello **krawędzi iot** repozytorium.
