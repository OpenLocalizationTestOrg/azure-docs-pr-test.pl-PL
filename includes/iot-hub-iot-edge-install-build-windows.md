## <a name="install-hello-prerequisites"></a><span data-ttu-id="0d7b2-101">Instalowanie wymagań wstępnych hello</span><span class="sxs-lookup"><span data-stu-id="0d7b2-101">Install hello prerequisites</span></span>

1. <span data-ttu-id="0d7b2-102">Zainstaluj [programu Visual Studio 2015 lub 2017](https://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="0d7b2-102">Install [Visual Studio 2015 or 2017](https://www.visualstudio.com).</span></span> <span data-ttu-id="0d7b2-103">Można użyć hello, które spełniają wymagania licencyjne hello w warstwie bezpłatna wersja Community.</span><span class="sxs-lookup"><span data-stu-id="0d7b2-103">You can use hello free Community Edition if you meet hello licensing requirements.</span></span> <span data-ttu-id="0d7b2-104">Należy się tooinclude Visual C++ i Menedżer pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="0d7b2-104">Be sure tooinclude Visual C++ and NuGet Package Manager.</span></span>

1. <span data-ttu-id="0d7b2-105">Zainstaluj [git](http://www.git-scm.com) i upewnij się, że git.exe można uruchomić z wiersza polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="0d7b2-105">Install [git](http://www.git-scm.com) and make sure you can run git.exe from hello command line.</span></span>

1. <span data-ttu-id="0d7b2-106">Zainstaluj [CMake](https://cmake.org/download/) i upewnij się, że cmake.exe można uruchomić z wiersza polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="0d7b2-106">Install [CMake](https://cmake.org/download/) and make sure you can run cmake.exe from hello command line.</span></span> <span data-ttu-id="0d7b2-107">CMake wersji 3.7.2 lub nowszy jest zalecane.</span><span class="sxs-lookup"><span data-stu-id="0d7b2-107">CMake version 3.7.2 or later is recommended.</span></span> <span data-ttu-id="0d7b2-108">Witaj **.msi** Instalator jest najłatwiejsza opcja hello w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="0d7b2-108">hello **.msi** installer is hello easiest option on Windows.</span></span> <span data-ttu-id="0d7b2-109">Dodaj CMake toohello po wyświetleniu monitu Instalatora hello ścieżki dla co najmniej hello bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0d7b2-109">Add CMake toohello PATH for at least hello current user when hello installer prompts you.</span></span>

1. <span data-ttu-id="0d7b2-110">Zainstaluj [Python 2.7](https://www.python.org/downloads/release/python-27).</span><span class="sxs-lookup"><span data-stu-id="0d7b2-110">Install [Python 2.7](https://www.python.org/downloads/release/python-27).</span></span> <span data-ttu-id="0d7b2-111">Upewnij się, że możesz dodać Python tooyour `PATH` zmiennej środowiskowej w **Panel sterowania -> System -> Zaawansowane zmiennych środowiskowych -> Ustawienia systemu**.</span><span class="sxs-lookup"><span data-stu-id="0d7b2-111">Make sure you add Python tooyour `PATH` environment variable in **Control Panel -> System -> Advanced system settings -> Environment Variables**.</span></span>

1. <span data-ttu-id="0d7b2-112">W wierszu polecenia Uruchom hello następujące polecenia tooclone hello Azure IoT krawędzi GitHub repozytorium tooyour komputera lokalnego:</span><span class="sxs-lookup"><span data-stu-id="0d7b2-112">At a command prompt, run hello following command tooclone hello Azure IoT Edge GitHub repository tooyour local machine:</span></span>

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-toobuild-hello-sample"></a><span data-ttu-id="0d7b2-113">Jak toobuild hello próbki</span><span class="sxs-lookup"><span data-stu-id="0d7b2-113">How toobuild hello sample</span></span>

<span data-ttu-id="0d7b2-114">Hello krawędzi IoT można teraz tworzyć środowiska uruchomieniowego i przykłady, na komputerze lokalnym:</span><span class="sxs-lookup"><span data-stu-id="0d7b2-114">You can now build hello IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="0d7b2-115">Otwórz **wiersz polecenia dla programu VS 2015 deweloperów** lub **wiersz polecenia dla programu VS 2017 deweloperów** wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="0d7b2-115">Open a **Developer Command Prompt for VS 2015** or **Developer Command Prompt for VS 2017** command prompt.</span></span>

1. <span data-ttu-id="0d7b2-116">Przejdź do folderu głównego toohello w lokalnej kopii hello **krawędzi iot** repozytorium.</span><span class="sxs-lookup"><span data-stu-id="0d7b2-116">Navigate toohello root folder in your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="0d7b2-117">Uruchom skrypt kompilacji w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="0d7b2-117">Run the build script as follows:</span></span>

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

<span data-ttu-id="0d7b2-118">Ten skrypt tworzy plik rozwiązania Visual Studio i tworzy hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="0d7b2-118">This script creates a Visual Studio solution file and builds hello solution.</span></span> <span data-ttu-id="0d7b2-119">Witaj rozwiązania Visual Studio można znaleźć w hello **kompilacji** folderu w lokalnej kopii hello **krawędzi iot** repozytorium.</span><span class="sxs-lookup"><span data-stu-id="0d7b2-119">You can find hello Visual Studio solution in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="0d7b2-120">Toobuild i uruchom testy jednostkowe hello, Dodaj hello `--run-unittests` parametru.</span><span class="sxs-lookup"><span data-stu-id="0d7b2-120">If you want toobuild and run hello unit tests, add hello `--run-unittests` parameter.</span></span> <span data-ttu-id="0d7b2-121">Toobuild i uruchom testy tooend zakończenia hello, Dodaj hello `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="0d7b2-121">If you want toobuild and run hello end tooend tests, add hello `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="0d7b2-122">Każdym uruchomieniu hello **build.cmd** skryptu, usuwa, a następnie tworzy ponownie hello **kompilacji** folderu w folderze głównym hello kopii lokalnej hello **krawędzi iot** repozytorium.</span><span class="sxs-lookup"><span data-stu-id="0d7b2-122">Every time you run hello **build.cmd** script, it deletes and then recreates hello **build** folder in hello root folder of your local copy of hello **iot-edge** repository.</span></span>
