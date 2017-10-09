## <a name="install-hello-prerequisites"></a><span data-ttu-id="df9c7-101">Instalowanie wymagań wstępnych hello</span><span class="sxs-lookup"><span data-stu-id="df9c7-101">Install hello prerequisites</span></span>

<span data-ttu-id="df9c7-102">Hello krokach tego samouczka przyjęto założenie, że używasz Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="df9c7-102">hello steps in this tutorial assume you are running Ubuntu Linux.</span></span>

<span data-ttu-id="df9c7-103">Otwórz powłokę i uruchom następujące polecenia tooinstall hello wymagań wstępnych pakietów hello:</span><span class="sxs-lookup"><span data-stu-id="df9c7-103">Open a shell and run hello following commands tooinstall hello prerequisite packages:</span></span>

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

<span data-ttu-id="df9c7-104">W powłoce hello Uruchom hello następujące polecenia tooclone hello Azure IoT krawędzi GitHub repozytorium tooyour komputera lokalnego:</span><span class="sxs-lookup"><span data-stu-id="df9c7-104">In hello shell, run hello following command tooclone hello Azure IoT Edge GitHub repository tooyour local machine:</span></span>

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-toobuild-hello-sample"></a><span data-ttu-id="df9c7-105">Jak toobuild hello próbki</span><span class="sxs-lookup"><span data-stu-id="df9c7-105">How toobuild hello sample</span></span>

<span data-ttu-id="df9c7-106">Hello krawędzi IoT można teraz tworzyć środowiska uruchomieniowego i przykłady, na komputerze lokalnym:</span><span class="sxs-lookup"><span data-stu-id="df9c7-106">You can now build hello IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="df9c7-107">Otwórz powłokę.</span><span class="sxs-lookup"><span data-stu-id="df9c7-107">Open a shell.</span></span>

1. <span data-ttu-id="df9c7-108">Przejdź do folderu głównego toohello w lokalnej kopii hello **krawędzi iot** repozytorium.</span><span class="sxs-lookup"><span data-stu-id="df9c7-108">Navigate toohello root folder in your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="df9c7-109">Uruchom skrypt kompilacji w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="df9c7-109">Run the build script as follows:</span></span>

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

<span data-ttu-id="df9c7-110">Ten skrypt używa **cmake** toocreate narzędzie folder o nazwie **kompilacji** w folderze głównym hello lokalną kopię **krawędzi iot** repozytorium i generowanie pliku reguł programu make.</span><span class="sxs-lookup"><span data-stu-id="df9c7-110">This script uses the **cmake** utility toocreate a folder called **build** in hello root folder of your local copy of the **iot-edge** repository and generate a makefile.</span></span> <span data-ttu-id="df9c7-111">skrypt Hello następnie buduje rozwiązanie hello, pomijanie testów jednostkowych i tooend zakończenia.</span><span class="sxs-lookup"><span data-stu-id="df9c7-111">hello script then builds hello solution, skipping unit tests and end tooend tests.</span></span> <span data-ttu-id="df9c7-112">Toobuild i uruchom testy jednostkowe hello, Dodaj hello `--run-unittests` parametru.</span><span class="sxs-lookup"><span data-stu-id="df9c7-112">If you want toobuild and run hello unit tests, add hello `--run-unittests` parameter.</span></span> <span data-ttu-id="df9c7-113">Toobuild i uruchom testy tooend zakończenia hello, Dodaj hello `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="df9c7-113">If you want toobuild and run hello end tooend tests, add hello `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="df9c7-114">Każdym uruchomieniu hello **build.sh** skryptu, usuwa, a następnie tworzy ponownie hello **kompilacji** folderu w folderze głównym hello kopii lokalnej hello **krawędzi iot** repozytorium.</span><span class="sxs-lookup"><span data-stu-id="df9c7-114">Every time you run hello **build.sh** script, it deletes and then recreates hello **build** folder in hello root folder of your local copy of hello **iot-edge** repository.</span></span>
