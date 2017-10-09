<span data-ttu-id="2c838-101">Platforma Azure określi, że aplikacja używa języka Python, **jeśli są spełnione oba te warunki**:</span><span class="sxs-lookup"><span data-stu-id="2c838-101">Azure will determine that your application uses Python **if both of these conditions are true**:</span></span>

* <span data-ttu-id="2c838-102">Plik Requirements.txt znajduje się w folderze głównym hello</span><span class="sxs-lookup"><span data-stu-id="2c838-102">requirements.txt file in hello root folder</span></span>
* <span data-ttu-id="2c838-103">Każdy plik .py w folderze głównym hello lub pliku runtime.txt, który określa języka python</span><span class="sxs-lookup"><span data-stu-id="2c838-103">any .py file in hello root folder OR a runtime.txt that specifies python</span></span>

<span data-ttu-id="2c838-104">W takim przypadku hello użyje skryptu wdrażania języka Python, który wykonuje standardową synchronizację plików, a także dodatkowe operacje języka Python, takie jak hello:</span><span class="sxs-lookup"><span data-stu-id="2c838-104">When that's hello case, it will use a Python specific deployment script, which performs hello standard synchronization of files, as well as additional Python operations such as:</span></span>

* <span data-ttu-id="2c838-105">Automatyczne zarządzanie środowiskiem wirtualnym</span><span class="sxs-lookup"><span data-stu-id="2c838-105">Automatic management of virtual environment</span></span>
* <span data-ttu-id="2c838-106">Instalacja pakietów wymienionych w pliku requirements.txt przy użyciu adresu pip</span><span class="sxs-lookup"><span data-stu-id="2c838-106">Installation of packages listed in requirements.txt using pip</span></span>
* <span data-ttu-id="2c838-107">Tworzenie odpowiedniego pliku web.config hello oparte na powitania wybranej wersji języka Python.</span><span class="sxs-lookup"><span data-stu-id="2c838-107">Creation of hello appropriate web.config based on hello selected Python version.</span></span>
* <span data-ttu-id="2c838-108">Zbieranie plików statycznych dla aplikacji Django</span><span class="sxs-lookup"><span data-stu-id="2c838-108">Collect static files for Django applications</span></span>

<span data-ttu-id="2c838-109">Można kontrolować niektóre aspekty domyślnych kroków wdrażania hello bez konieczności toocustomize hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="2c838-109">You can control certain aspects of hello default deployment steps without having toocustomize hello script.</span></span>

<span data-ttu-id="2c838-110">Jeśli chcesz tooskip wszystkie kroki wdrażania właściwe dla języka Python, możesz utworzyć ten pusty plik:</span><span class="sxs-lookup"><span data-stu-id="2c838-110">If you want tooskip all Python specific deployment steps, you can create this empty file:</span></span>

    \.skipPythonDeployment

<span data-ttu-id="2c838-111">Aby uzyskać większą kontrolę nad wdrażaniem można zastąpić hello domyślny skrypt wdrożenia, tworząc hello następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="2c838-111">For more control over deployment, you can override hello default deployment script by creating hello following files:</span></span>

    \.deployment
    \deploy.cmd

<span data-ttu-id="2c838-112">Można użyć hello [interfejsu wiersza polecenia platformy Azure] [ Azure command-line interface] toocreate hello plików.</span><span class="sxs-lookup"><span data-stu-id="2c838-112">You can use hello [Azure command-line interface][Azure command-line interface] toocreate hello files.</span></span>  <span data-ttu-id="2c838-113">Użyj tego polecenia w folderze projektu:</span><span class="sxs-lookup"><span data-stu-id="2c838-113">Use this command from your project folder:</span></span>

    azure site deploymentscript --python

<span data-ttu-id="2c838-114">Jeśli te pliki nie istnieją, platforma Azure tworzy tymczasowy skrypt wdrażania i uruchamia go.</span><span class="sxs-lookup"><span data-stu-id="2c838-114">When these files don't exist, Azure creates a temporary deployment script and runs it.</span></span>  <span data-ttu-id="2c838-115">Jest identyczne toohello został utworzony za pomocą polecenia hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="2c838-115">It is identical toohello one you create with hello command above.</span></span>

[Azure command-line interface]: http://azure.microsoft.com/downloads/
