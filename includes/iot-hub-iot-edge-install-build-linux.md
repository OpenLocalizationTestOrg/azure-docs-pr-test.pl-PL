## <a name="install-the-prerequisites"></a><span data-ttu-id="eb6ae-101">Zainstaluj wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="eb6ae-101">Install the prerequisites</span></span>

<span data-ttu-id="eb6ae-102">Kroki opisane w tym samouczku przyjęto założenie, że używasz Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="eb6ae-102">The steps in this tutorial assume you are running Ubuntu Linux.</span></span>

<span data-ttu-id="eb6ae-103">Otwórz powłokę i uruchom następujące polecenia, aby zainstalować wstępnie wymagane pakiety:</span><span class="sxs-lookup"><span data-stu-id="eb6ae-103">Open a shell and run the following commands to install the prerequisite packages:</span></span>

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

<span data-ttu-id="eb6ae-104">W powłoce, uruchom następujące polecenie, można sklonować repozytorium GitHub krawędzi IoT Azure na komputerze lokalnym:</span><span class="sxs-lookup"><span data-stu-id="eb6ae-104">In the shell, run the following command to clone the Azure IoT Edge GitHub repository to your local machine:</span></span>

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-to-build-the-sample"></a><span data-ttu-id="eb6ae-105">Jak skompilować przykład</span><span class="sxs-lookup"><span data-stu-id="eb6ae-105">How to build the sample</span></span>

<span data-ttu-id="eb6ae-106">Krawędź IoT można teraz tworzyć środowiska uruchomieniowego i przykłady, na komputerze lokalnym:</span><span class="sxs-lookup"><span data-stu-id="eb6ae-106">You can now build the IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="eb6ae-107">Otwórz powłokę.</span><span class="sxs-lookup"><span data-stu-id="eb6ae-107">Open a shell.</span></span>

1. <span data-ttu-id="eb6ae-108">Przejdź do folderu głównego w lokalnej kopii repozytorium **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="eb6ae-108">Navigate to the root folder in your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="eb6ae-109">Uruchom skrypt kompilacji w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="eb6ae-109">Run the build script as follows:</span></span>

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

<span data-ttu-id="eb6ae-110">Ten skrypt używa narzędzia **cmake** do utworzenia folderu o nazwie **build** w folderze głównym lokalnej kopii repozytorium **iot-edge** i wygenerowania pliku reguł programu make.</span><span class="sxs-lookup"><span data-stu-id="eb6ae-110">This script uses the **cmake** utility to create a folder called **build** in the root folder of your local copy of the **iot-edge** repository and generate a makefile.</span></span> <span data-ttu-id="eb6ae-111">Skrypt następnie kompiluje rozwiązanie, pomijając testy jednostkowe i testy kompleksowe.</span><span class="sxs-lookup"><span data-stu-id="eb6ae-111">The script then builds the solution, skipping unit tests and end to end tests.</span></span> <span data-ttu-id="eb6ae-112">Jeśli chcesz tworzenia i uruchamiania testów jednostkowych, dodać `--run-unittests` parametru.</span><span class="sxs-lookup"><span data-stu-id="eb6ae-112">If you want to build and run the unit tests, add the `--run-unittests` parameter.</span></span> <span data-ttu-id="eb6ae-113">Aby tworzenie i Uruchamianie testów kompleksowe, dodać `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="eb6ae-113">If you want to build and run the end to end tests, add the `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="eb6ae-114">Za każdym razem, gdy zostanie uruchomiony skrypt **build.sh**, folder **build** jest usuwany i tworzony ponownie w folderze głównym lokalnej kopii repozytorium **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="eb6ae-114">Every time you run the **build.sh** script, it deletes and then recreates the **build** folder in the root folder of your local copy of the **iot-edge** repository.</span></span>