<span data-ttu-id="9f04b-101">Nie zawsze instalowanie pakietów w sieci Azure przy użyciu programu pip kończy się powodzeniem.</span><span class="sxs-lookup"><span data-stu-id="9f04b-101">Some packages may not install using pip when run on Azure.</span></span>  <span data-ttu-id="9f04b-102">Może się zdarzyć, że pakiet hello nie jest dostępny na powitania indeksu pakietów języka Python.</span><span class="sxs-lookup"><span data-stu-id="9f04b-102">It may simply be that hello package is not available on hello Python Package Index.</span></span>  <span data-ttu-id="9f04b-103">Jest to możliwe, że wymagane jest kompilatora (kompilator nie jest dostępny na powitania maszyny uruchomionych hello aplikacji sieci web w usłudze Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="9f04b-103">It could be that a compiler is required (a compiler is not available on hello machine running hello web app in Azure App Service).</span></span>

<span data-ttu-id="9f04b-104">W tej sekcji wyjaśniono sposób toodeal dotyczącą tego problemu.</span><span class="sxs-lookup"><span data-stu-id="9f04b-104">In this section, we'll look at ways toodeal with this issue.</span></span>

### <a name="request-wheels"></a><span data-ttu-id="9f04b-105">Żądanie plików w formacie Wheel</span><span class="sxs-lookup"><span data-stu-id="9f04b-105">Request wheels</span></span>
<span data-ttu-id="9f04b-106">Jeśli hello instalacja pakietu wymaga kompilatora, możesz spróbować skontaktować się hello toorequest właściciela pakietu, który koła udostępniane hello pakietu.</span><span class="sxs-lookup"><span data-stu-id="9f04b-106">If hello package installation requires a compiler, you should try contacting hello package owner toorequest that wheels be made available for hello package.</span></span>

<span data-ttu-id="9f04b-107">Z hello udostępnieniu [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], jest teraz łatwiejsze pakiety toobuild mający kodu macierzystego języka Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="9f04b-107">With hello recent availability of [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], it is now easier toobuild packages that have native code for Python 2.7.</span></span>

### <a name="build-wheels-requires-windows"></a><span data-ttu-id="9f04b-108">Tworzenie plików w formacie Wheel (wymaga systemu Windows)</span><span class="sxs-lookup"><span data-stu-id="9f04b-108">Build wheels (requires Windows)</span></span>
<span data-ttu-id="9f04b-109">Uwaga: Korzystając z tej opcji, upewnij się, że pakiet hello toocompile przy użyciu środowiska Python, odpowiadający hello platformie/architekturze/wersji, jaka jest używana na powitania aplikacji sieci web w usłudze Azure App Service (Windows/32-bit/2.7 lub 3.4).</span><span class="sxs-lookup"><span data-stu-id="9f04b-109">Note: When using this option, make sure toocompile hello package using a Python environment that matches hello platform/architecture/version that is used on hello web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="9f04b-110">Jeśli pakiet hello nie instaluje, ponieważ wymaga kompilatora, można zainstalować kompilator hello na komputerze lokalnym i kompilacji w formacie wheel hello pakiet, który następnie zostanie dołączony do repozytorium.</span><span class="sxs-lookup"><span data-stu-id="9f04b-110">If hello package doesn't install because it requires a compiler, you can install hello compiler on your local machine and build a wheel for hello package, which you will then include in your repository.</span></span>

<span data-ttu-id="9f04b-111">Użytkownicy systemów Mac/Linux: Jeśli nie masz komputera z systemem Windows tooa dostępu, zobacz [tworzenie maszyny wirtualnej systemem Windows] [ Create a Virtual Machine Running Windows] jak toocreate Maszynę wirtualną na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9f04b-111">Mac/Linux Users: If you don't have access tooa Windows machine, see [Create a Virtual Machine Running Windows][Create a Virtual Machine Running Windows] for how toocreate a VM on Azure.</span></span>  <span data-ttu-id="9f04b-112">Można go użyć koła hello toobuild, je dodać toohello repozytorium i odrzucić hello maszyny Wirtualnej, jeśli chcesz.</span><span class="sxs-lookup"><span data-stu-id="9f04b-112">You can use it toobuild hello wheels, add them toohello repository, and discard hello VM if you like.</span></span> 

<span data-ttu-id="9f04b-113">For Python 2.7 można zainstalować [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].</span><span class="sxs-lookup"><span data-stu-id="9f04b-113">For Python 2.7, you can install [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].</span></span>

<span data-ttu-id="9f04b-114">W przypadku języka Python 3.4 można zainstalować [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].</span><span class="sxs-lookup"><span data-stu-id="9f04b-114">For Python 3.4, you can install [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].</span></span>

<span data-ttu-id="9f04b-115">koła toobuild potrzebne hello pakiet wheel:</span><span class="sxs-lookup"><span data-stu-id="9f04b-115">toobuild wheels, you'll need hello wheel package:</span></span>

    env\scripts\pip install wheel

<span data-ttu-id="9f04b-116">Użyjesz `pip wheel` toocompile zależności:</span><span class="sxs-lookup"><span data-stu-id="9f04b-116">You'll use `pip wheel` toocompile a dependency:</span></span>

    env\scripts\pip wheel azure==0.8.4

<span data-ttu-id="9f04b-117">Spowoduje to utworzenie pliku .whl w folderze \wheelhouse hello.</span><span class="sxs-lookup"><span data-stu-id="9f04b-117">This creates a .whl file in hello \wheelhouse folder.</span></span>  <span data-ttu-id="9f04b-118">Dodaj hello \wheelhouse folder i kółka pliki tooyour repozytorium.</span><span class="sxs-lookup"><span data-stu-id="9f04b-118">Add hello \wheelhouse folder and wheel files tooyour repository.</span></span>

<span data-ttu-id="9f04b-119">Edytuj hello tooadd Twojego pliku requirements.txt `--find-links` opcji u góry hello.</span><span class="sxs-lookup"><span data-stu-id="9f04b-119">Edit your requirements.txt tooadd hello `--find-links` option at hello top.</span></span> <span data-ttu-id="9f04b-120">Ta wartość informuje narzędzie pip toolook dla dokładnego dopasowania w folderze lokalnym hello przed indeksu pakietów języka python toohello będzie.</span><span class="sxs-lookup"><span data-stu-id="9f04b-120">This tells pip toolook for an exact match in hello local folder before going toohello python package index.</span></span>

    --find-links wheelhouse
    azure==0.8.4

<span data-ttu-id="9f04b-121">Jeśli chcesz tooinclude wszystkie zależności w hello \wheelhouse folderze i używaj hello pakiet języka python indeksu na wszystkich indeksu pakietów hello tooignore pip można wymusić przez dodanie `--no-index` toohello góry pliku requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="9f04b-121">If you want tooinclude all your dependencies in hello \wheelhouse folder and not use hello python package index at all, you can force pip tooignore hello package index by adding `--no-index` toohello top of your requirements.txt.</span></span>

    --no-index

### <a name="customize-installation"></a><span data-ttu-id="9f04b-122">Instalacja niestandardowa</span><span class="sxs-lookup"><span data-stu-id="9f04b-122">Customize installation</span></span>
<span data-ttu-id="9f04b-123">Można dostosować hello wdrożenia skryptu tooinstall pakietu w środowisku wirtualnym hello przy użyciu Instalatora alternatywnego, takiego jak easy\_zainstalować.</span><span class="sxs-lookup"><span data-stu-id="9f04b-123">You can customize hello deployment script tooinstall a package in hello virtual environment using an alternate installer, such as easy\_install.</span></span>  <span data-ttu-id="9f04b-124">Zapoznaj się z plikiem deploy.cmd, w którym odpowiedni przykład jest zakomentowany.  Upewnij się, że takie pakiety nie są wymienione w pliku requirements.txt, pip tooprevent z ich instalowania.</span><span class="sxs-lookup"><span data-stu-id="9f04b-124">See deploy.cmd for an example that is commented out.  Make sure that such packages aren't listed in requirements.txt, tooprevent pip from installing them.</span></span>

<span data-ttu-id="9f04b-125">Dodaj ten skrypt wdrażania toohello:</span><span class="sxs-lookup"><span data-stu-id="9f04b-125">Add this toohello deployment script:</span></span>

    env\scripts\easy_install somepackage

<span data-ttu-id="9f04b-126">Może być również toouse można łatwo\_zainstalować tooinstall z Instalatorem exe (niektóre są rozpoznają format zip, dlatego łatwo\_je obsługuje instalację).</span><span class="sxs-lookup"><span data-stu-id="9f04b-126">You may also be able toouse easy\_install tooinstall from an exe installer (some are zip compatible, so easy\_install supports them).</span></span>  <span data-ttu-id="9f04b-127">Dodaj hello Instalator tooyour repozytorium, a następnie Wywołaj program easy\_install, przekazując hello toohello ścieżki pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="9f04b-127">Add hello installer tooyour repository, and invoke easy\_install by passing hello path toohello executable.</span></span>

<span data-ttu-id="9f04b-128">Dodaj ten skrypt wdrażania toohello:</span><span class="sxs-lookup"><span data-stu-id="9f04b-128">Add this toohello deployment script:</span></span>

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-hello-virtual-environment-in-hello-repository-requires-windows"></a><span data-ttu-id="9f04b-129">Zawierają środowisko wirtualne hello hello repozytorium (wymaga systemu Windows)</span><span class="sxs-lookup"><span data-stu-id="9f04b-129">Include hello virtual environment in hello repository (requires Windows)</span></span>
<span data-ttu-id="9f04b-130">Uwaga: Podczas korzystania z tej opcji upewnij się, że toouse środowisku wirtualnym, które odpowiada hello platformie/architekturze/wersji, jaka jest używana na powitania aplikacji sieci web w usłudze Azure App Service (Windows/32-bit/2.7 lub 3.4).</span><span class="sxs-lookup"><span data-stu-id="9f04b-130">Note: When using this option, make sure toouse a virtual environment that matches hello platform/architecture/version that is used on hello web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="9f04b-131">Jeśli dołączysz hello środowiska wirtualnego do repozytorium hello można zapobiec zarządzaniu środowiskiem wirtualnym na platformie Azure, tworząc pusty plik skryptu wdrażania hello:</span><span class="sxs-lookup"><span data-stu-id="9f04b-131">If you include hello virtual environment in hello repository, you can prevent hello deployment script from doing virtual environment management on Azure by creating an empty file:</span></span>

    .skipPythonDeployment

<span data-ttu-id="9f04b-132">Zaleca się usunięcie istniejącego środowiska wirtualnego hello w aplikacji hello, tooprevent pozostawieniu plików z podczas hello środowisko wirtualne było zarządzane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="9f04b-132">We recommend that you delete hello existing virtual environment on hello app, tooprevent leftover files from when hello virtual environment was managed automatically.</span></span>

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949
