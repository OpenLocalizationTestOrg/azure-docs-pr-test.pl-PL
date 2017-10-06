---
title: "dostarczanie aaaContinuous chmury usługi z programem TFS na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak aplikacji w chmurze tooset się ciągłego dostarczania dla platformy Azure. Przykłady kodu dla instrukcji wiersza polecenia programu MSBuild i skryptów programu PowerShell."
services: cloud-services
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4f3c93c6-5c82-4779-9d19-7404a01e82ca
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/12/2017
ms.author: kraigb
ms.openlocfilehash: c0e5e72ffbd3c05b84ce1733068e92c528bcc4b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a><span data-ttu-id="5522d-104">Ciągłego dostarczania dla usług w chmurze na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="5522d-104">Continuous Delivery for Cloud Services in Azure</span></span>
<span data-ttu-id="5522d-105">Witaj procesu opisanego w tym artykule przedstawiono sposób tooset się ciągłego dostarczania dla aplikacji w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="5522d-105">hello process described in this article shows you how tooset up continuous delivery for Azure cloud apps.</span></span> <span data-ttu-id="5522d-106">Ten proces umożliwia automatyczne tworzenie pakietów i wdrożyć tooAzure pakietu powitania po każdym ewidencjonowania kodu.</span><span class="sxs-lookup"><span data-stu-id="5522d-106">This process enables you to automatically create packages and deploy hello package tooAzure after every code check-in.</span></span> <span data-ttu-id="5522d-107">Witaj procesu kompilacji pakietu opisane w tym artykule jest równoważne toohello **pakietu** polecenie w programie Visual Studio i kroki publikowania są równoważne toohello **publikowania** polecenia w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5522d-107">hello package build process described in this article is equivalent toohello **Package** command in Visual Studio, and the publishing steps are equivalent toohello **Publish** command in Visual Studio.</span></span>
<span data-ttu-id="5522d-108">Hello artykuł obejmuje hello metody toocreate serwera kompilacji będzie korzystać także z MSBuild instrukcje wiersza polecenia i skryptów programu Windows PowerShell i pokazuje, jak toooptionally Konfigurowanie programu Visual Studio Team Foundation Server - Team Build definicje toouse hello MSBuild poleceń i skryptów programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5522d-108">hello article covers hello methods you would use toocreate a build server with MSBuild command-line statements and Windows PowerShell scripts, and it also demonstrates how toooptionally configure Visual Studio Team Foundation Server - Team Build definitions toouse hello MSBuild commands and PowerShell scripts.</span></span> <span data-ttu-id="5522d-109">proces Hello jest można dostosować do własnego środowiska kompilacji i środowisk docelowej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5522d-109">hello process is customizable for your build environment and Azure target environments.</span></span>

<span data-ttu-id="5522d-110">Można również użyć programu Visual Studio Team Services, wersji programu TFS, która jest hostowana na platformie Azure, toodo to łatwiejsze.</span><span class="sxs-lookup"><span data-stu-id="5522d-110">You can also use Visual Studio Team Services, a version of TFS that is hosted in Azure, toodo this more easily.</span></span> 

<span data-ttu-id="5522d-111">Przed rozpoczęciem należy opublikować aplikacji z programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5522d-111">Before you start, you should publish your application from Visual Studio.</span></span>
<span data-ttu-id="5522d-112">Zapewni to, czy wszystkie zasoby hello są dostępne i została zainicjowana usiłujące tooautomate hello publikacji procesu.</span><span class="sxs-lookup"><span data-stu-id="5522d-112">This will ensure that all hello resources are available and initialized when you attempt tooautomate hello publication process.</span></span>

## <a name="1-configure-hello-build-server"></a><span data-ttu-id="5522d-113">1: Konfigurowanie powitania serwera kompilacji</span><span class="sxs-lookup"><span data-stu-id="5522d-113">1: Configure hello Build Server</span></span>
<span data-ttu-id="5522d-114">Przed utworzeniem pakietu Azure przy użyciu programu MSBuild, należy zainstalować hello wymagane oprogramowanie i narzędzi na serwerze kompilacji hello.</span><span class="sxs-lookup"><span data-stu-id="5522d-114">Before you can create an Azure package by using MSBuild, you must install hello required software and tools on hello build server.</span></span>

<span data-ttu-id="5522d-115">Program Visual Studio nie jest wymagane toobe zainstalowane na powitania serwera kompilacji.</span><span class="sxs-lookup"><span data-stu-id="5522d-115">Visual Studio is not required toobe installed on hello build server.</span></span> <span data-ttu-id="5522d-116">Toomanage usługi kompilacji programu Team Foundation toouse serwera kompilacji, należy wykonać instrukcje hello hello [usługi kompilacji programu Team Foundation] [ Team Foundation Build Service] dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="5522d-116">If you want toouse Team Foundation Build Service toomanage your build server, follow hello instructions in hello [Team Foundation Build Service][Team Foundation Build Service] documentation.</span></span>

1. <span data-ttu-id="5522d-117">Na serwerze kompilacji hello Zainstaluj hello [.NET Framework 4.5.2][.NET Framework 4.5.2], która obejmuje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5522d-117">On hello build server, install hello [.NET Framework 4.5.2][.NET Framework 4.5.2], which includes MSBuild.</span></span>
2. <span data-ttu-id="5522d-118">Zainstaluj najnowsze hello [Azure Authoring Tools dla programu .NET](https://azure.microsoft.com/develop/net/).</span><span class="sxs-lookup"><span data-stu-id="5522d-118">Install hello latest [Azure Authoring Tools for .NET](https://azure.microsoft.com/develop/net/).</span></span>
3. <span data-ttu-id="5522d-119">Zainstaluj hello [biblioteki Azure dla platformy .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span><span class="sxs-lookup"><span data-stu-id="5522d-119">Install hello [Azure Libraries for .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span></span>
4. <span data-ttu-id="5522d-120">Serwer kompilacji pliku Microsoft.WebApplication.targets hello kopiowania z toohello instalacji programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5522d-120">Copy hello Microsoft.WebApplication.targets file from a Visual Studio installation toohello build server.</span></span>

   <span data-ttu-id="5522d-121">Na komputerze z programem Visual Studio zainstalowany, ten plik znajduje się w katalogu hello C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\14.0\\WebApplications.</span><span class="sxs-lookup"><span data-stu-id="5522d-121">On a computer with Visual Studio installed, this file is located in hello directory C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span></span> <span data-ttu-id="5522d-122">Należy skopiować toohello tym samym katalogu na powitania serwera kompilacji.</span><span class="sxs-lookup"><span data-stu-id="5522d-122">You should copy it toohello same directory on hello build server.</span></span>
5. <span data-ttu-id="5522d-123">Zainstaluj hello [Azure Tools dla programu Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="5522d-123">Install hello [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span></span>

## <a name="2-build-a-package-using-msbuild-commands"></a><span data-ttu-id="5522d-124">2: Tworzenie pakietu przy użyciu polecenia programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="5522d-124">2: Build a Package using MSBuild Commands</span></span>
<span data-ttu-id="5522d-125">W tej sekcji opisano, jak tooconstruct MSBuild polecenia, który tworzy pakiet Azure.</span><span class="sxs-lookup"><span data-stu-id="5522d-125">This section describes how tooconstruct an MSBuild command that builds an Azure package.</span></span> <span data-ttu-id="5522d-126">Wykonaj ten krok na powitania kompilacji serwera tooverify czy wszystko jest poprawnie skonfigurowana i czy polecenie MSBuild hello wykonuje, co ma toodo.</span><span class="sxs-lookup"><span data-stu-id="5522d-126">Run this step on hello build server tooverify that everything is configured correctly and that hello MSBuild command does what you want it toodo.</span></span> <span data-ttu-id="5522d-127">Można dodać skrypty kompilacji to tooexisting wiersza polecenia na serwerze kompilacji hello lub skorzystać z wiersza polecenia hello w definicji kompilacji TFS, zgodnie z opisem w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="5522d-127">You can either add this command line tooexisting build scripts on hello build server, or you can use hello command line in a TFS Build Definition, as described in hello next section.</span></span> <span data-ttu-id="5522d-128">Aby uzyskać więcej informacji na temat parametrów wiersza polecenia i MSBuild, zobacz [informacje w wierszu polecenia programu MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="5522d-128">For more information about command-line parameters and MSBuild, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>

1. <span data-ttu-id="5522d-129">Jeśli program Visual Studio jest zainstalowany na serwerze kompilacji hello, Znajdź i wybierz **wiersz polecenia programu Visual Studio** w hello **programu Visual Studio Tools** folderu systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="5522d-129">If Visual Studio is installed on hello build server, locate and choose **Visual Studio Command Prompt** in hello **Visual Studio Tools** folder in Windows.</span></span>

   <span data-ttu-id="5522d-130">Jeśli program Visual Studio nie jest zainstalowany na serwerze kompilacji hello, otwórz wiersz polecenia i upewnij się, że MSBuild.exe jest dostępny w ścieżce.</span><span class="sxs-lookup"><span data-stu-id="5522d-130">If Visual Studio is not installed on hello build server, open a command prompt and make sure that MSBuild.exe is accessible on the path.</span></span> <span data-ttu-id="5522d-131">Z hello .NET Framework w hello ścieżki % WINDIR % jest zainstalowany program MSBuild\\Microsoft.NET\\Framework\\*wersji*.</span><span class="sxs-lookup"><span data-stu-id="5522d-131">MSBuild is installed with hello .NET Framework in hello path %WINDIR%\\Microsoft.NET\\Framework\\*Version*.</span></span> <span data-ttu-id="5522d-132">Na przykład aby dodać zmiennej środowiskowej PATH toohello MSBuild.exe, jeśli masz zainstalowany program .NET Framework 4, wpisz następujące polecenie w wierszu polecenia hello hello:</span><span class="sxs-lookup"><span data-stu-id="5522d-132">For example, to add MSBuild.exe toohello PATH environment variable when you have .NET Framework 4 installed, type hello following command at hello command prompt:</span></span>

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. <span data-ttu-id="5522d-133">W wierszu polecenia hello Przejdź toohello folder zawierający plik projektu platformy Azure, które mają toobuild.</span><span class="sxs-lookup"><span data-stu-id="5522d-133">At hello command prompt, navigate toohello folder containing the Azure project file that you want toobuild.</span></span>
3. <span data-ttu-id="5522d-134">Uruchom program MSBuild z hello/target: opcja tak jak hello poniższy przykład publikowania:</span><span class="sxs-lookup"><span data-stu-id="5522d-134">Run MSBuild with hello /target:Publish option as in hello following example:</span></span>

       MSBuild /target:Publish

   <span data-ttu-id="5522d-135">Tej opcji można stosować skrót /t: publikowania.</span><span class="sxs-lookup"><span data-stu-id="5522d-135">This option can be abbreviated as /t:Publish.</span></span> <span data-ttu-id="5522d-136">Opcja /t:Publish Hello w programie MSBuild nie należy mylić z polecenia Opublikuj hello dostępne w programie Visual Studio Jeśli masz hello zainstalowania zestawu Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="5522d-136">hello /t:Publish option in MSBuild should not be confused with hello Publish commands available in Visual Studio when you have hello Azure SDK installed.</span></span> <span data-ttu-id="5522d-137">Witaj /t: opcja publikowania tylko kompilacje hello Azure pakietów.</span><span class="sxs-lookup"><span data-stu-id="5522d-137">hello /t:Publish option only builds hello Azure packages.</span></span> <span data-ttu-id="5522d-138">Nie wdrażać pakietów hello jak hello polecenia Opublikuj w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5522d-138">It does not deploy hello packages as hello Publish commands in Visual Studio do.</span></span>

   <span data-ttu-id="5522d-139">Opcjonalnie można określić nazwę projektu hello jako parametr MSBuild.</span><span class="sxs-lookup"><span data-stu-id="5522d-139">Optionally, you can specify hello project name as an MSBuild parameter.</span></span> <span data-ttu-id="5522d-140">Jeśli nie zostanie określony, używany jest hello bieżący katalog.</span><span class="sxs-lookup"><span data-stu-id="5522d-140">If not specified, hello current directory is used.</span></span> <span data-ttu-id="5522d-141">Aby uzyskać więcej informacji na temat opcji wiersza polecenia programu MSBuild, zobacz [informacje w wierszu polecenia programu MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="5522d-141">For more information about MSBuild command line options, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>
4. <span data-ttu-id="5522d-142">Zlokalizuj hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="5522d-142">Locate hello output.</span></span> <span data-ttu-id="5522d-143">Domyślnie to polecenie tworzy katalog w folderze głównym toohello relacji dla projektu hello, takich jak *ProjectDir*\\bin\\*konfiguracji* \\ App.publish\\.</span><span class="sxs-lookup"><span data-stu-id="5522d-143">By default, this command creates a directory in relation toohello root folder for hello project, such as *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span></span> <span data-ttu-id="5522d-144">Podczas tworzenia projektu platformy Azure, generowanie dwóch plików, sam plik pakietu hello i hello towarzyszącego pliku konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="5522d-144">When you build an Azure project, you generate two files, hello package file itself and hello accompanying configuration file:</span></span>

   * <span data-ttu-id="5522d-145">Project.cspkg</span><span class="sxs-lookup"><span data-stu-id="5522d-145">Project.cspkg</span></span>
   * <span data-ttu-id="5522d-146">Element ServiceConfiguration. *TargetProfile*.cscfg</span><span class="sxs-lookup"><span data-stu-id="5522d-146">ServiceConfiguration.*TargetProfile*.cscfg</span></span>

   <span data-ttu-id="5522d-147">Domyślnie każdy projekt Azure zawiera jeden usługi konfiguracji pliku (cscfg) lokalne kompilacje (debugowanie) i drugi dla kompilacji chmury (tymczasowym czy produkcyjnym), ale można dodać lub usunąć pliki konfiguracji usługi, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="5522d-147">By default, each Azure project includes one service configuration file (.cscfg file) for local (debugging) builds and another for cloud (staging or production) builds, but you can add or remove service configuration files as needed.</span></span> <span data-ttu-id="5522d-148">Podczas tworzenia pakietu w programie Visual Studio, użytkownik zostanie poproszony które tooinclude pliku konfiguracji usługi obok hello pakietu.</span><span class="sxs-lookup"><span data-stu-id="5522d-148">When you build a package within Visual Studio, you will be asked which service configuration file tooinclude alongside hello package.</span></span>
5. <span data-ttu-id="5522d-149">Określ plik konfiguracji usługi hello.</span><span class="sxs-lookup"><span data-stu-id="5522d-149">Specify hello service configuration file.</span></span> <span data-ttu-id="5522d-150">Podczas tworzenia pakietu przy użyciu programu MSBuild w pliku konfiguracji usługi lokalne powitania znajduje się domyślnie.</span><span class="sxs-lookup"><span data-stu-id="5522d-150">When you build a package by using MSBuild, hello local service configuration file is included by default.</span></span> <span data-ttu-id="5522d-151">tooinclude plik konfiguracji innej usługi, ustaw właściwość TargetProfile hello polecenia programu MSBuild, tak jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="5522d-151">tooinclude a different service configuration file, set the TargetProfile property of hello MSBuild command, as in hello following example:</span></span>

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. <span data-ttu-id="5522d-152">Określ lokalizację hello hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="5522d-152">Specify hello location for hello output.</span></span> <span data-ttu-id="5522d-153">Ustaw ścieżkę hello przy użyciu /p:PublishDir =*katalogu* \\ opcji, w tym hello kończyć się separatorem ukośnik odwrotny, tak jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="5522d-153">Set hello path by using the /p:PublishDir=*Directory*\\ option, including hello trailing backslash separator, as in hello following example:</span></span>

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   <span data-ttu-id="5522d-154">Po utworzone i przetestowane MSBuild odpowiednie polecenie wiersza toobuild projektów i połączyć je w pakiecie Azure, istnieje możliwość dodania skryptów kompilacji tooyour tego wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="5522d-154">Once you've constructed and tested an appropriate MSBuild command line toobuild your projects and combine them into an Azure package, you can add this command line tooyour build scripts.</span></span> <span data-ttu-id="5522d-155">Jeśli serwer kompilacji obsługuje skrypty niestandardowe, ten proces będzie zależeć od specyfiki procesu kompilacji niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="5522d-155">If your build server uses custom scripts, this process will depend on the specifics of your custom build process.</span></span> <span data-ttu-id="5522d-156">Jeśli używasz TFS jako środowiska kompilacji, a następnie wykonać instrukcje hello hello następnego kroku procesu kompilacji tooyour tooadd hello Azure pakietu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="5522d-156">If you are using TFS as a build environment, then you can follow hello instructions in hello next step tooadd hello Azure package build tooyour build process.</span></span>

## <a name="3-build-a-package-using-tfs-team-build"></a><span data-ttu-id="5522d-157">3: Tworzenie pakietu za pomocą kompilacji TFS zespołu</span><span class="sxs-lookup"><span data-stu-id="5522d-157">3: Build a Package using TFS Team Build</span></span>
<span data-ttu-id="5522d-158">Jeśli masz Konfigurowanie kontrolera kompilacji i hello serwer kompilacji Team Foundation Server (TFS), skonfigurować jako maszyna kompilacji TFS, a następnie możesz opcjonalnie skonfigurować automatyczne kompilacji pakietu Azure.</span><span class="sxs-lookup"><span data-stu-id="5522d-158">If you have Team Foundation Server (TFS) set up as a build controller and hello build server set up as a TFS build machine, then you can optionally set up an automated build for your Azure package.</span></span> <span data-ttu-id="5522d-159">Aby uzyskać informacje dotyczące sposobu tooset się i użyj Team Foundation server jako system kompilacji, zobacz [skalowania w poziomie system kompilacji][Scale out your build system].</span><span class="sxs-lookup"><span data-stu-id="5522d-159">For information on how tooset up and use Team Foundation server as a build system, see [Scale out your build system][Scale out your build system].</span></span> <span data-ttu-id="5522d-160">W szczególności w poniższej procedurze przyjęto, że na serwerze kompilacji zostało skonfigurowane zgodnie z opisem w [Wdróż i skonfiguruj serwer kompilacji][Deploy and configure a build server], i utworzyć projektu zespołowego, należy utworzyć chmury projekt usługi w projekcie zespołowym hello.</span><span class="sxs-lookup"><span data-stu-id="5522d-160">In particular, the following procedure assumes that you have configured your build server as described in [Deploy and configure a build server][Deploy and configure a build server], and that you have created a team project, created a cloud service project in hello team project.</span></span>

<span data-ttu-id="5522d-161">tooconfigure TFS toobuild Azure pakietów, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="5522d-161">tooconfigure TFS toobuild Azure packages, perform hello following steps:</span></span>

1. <span data-ttu-id="5522d-162">W programie Visual Studio na komputerze dewelopera na powitania menu Widok wybierz polecenie **Team Explorer**, lub wybierz polecenie Ctrl +\\, Ctrl + M.</span><span class="sxs-lookup"><span data-stu-id="5522d-162">In Visual Studio on your development computer, on hello View menu, choose **Team Explorer**, or choose Ctrl+\\, Ctrl+M.</span></span> <span data-ttu-id="5522d-163">W oknie programu Team Explorer rozwiń hello **kompilacje** węzła lub wybierz hello **kompilacje** stronie, a następnie wybierz **nową definicję kompilacji**.</span><span class="sxs-lookup"><span data-stu-id="5522d-163">In the Team Explorer window, expand hello **Builds** node or choose hello **Builds** page, and choose **New Build Definition**.</span></span>

   ![Nowa opcja definicji kompilacji][0]
2. <span data-ttu-id="5522d-165">Wybierz hello **wyzwalacza** , a następnie określ hello potrzeby warunków, dla której ma zostać hello toobe pakiet utworzony.</span><span class="sxs-lookup"><span data-stu-id="5522d-165">Choose hello **Trigger** tab, and specify hello desired conditions for when you want hello package toobe built.</span></span> <span data-ttu-id="5522d-166">Na przykład określić **ciągłej integracji** występuje toobuild hello pakietu przy każdym wyboru w kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="5522d-166">For example, specify **Continuous Integration** toobuild hello package whenever a source control check-in occurs.</span></span>
3. <span data-ttu-id="5522d-167">Wybierz hello **ustawienia źródła** karcie i upewnij się, że folder projektu jest wymieniony w hello **folderu kontroli źródła** kolumny, i jest w stanie hello **Active**.</span><span class="sxs-lookup"><span data-stu-id="5522d-167">Choose hello **Source Settings** tab, and make sure your project folder is listed in hello **Source Control Folder** column, and hello status is **Active**.</span></span>
4. <span data-ttu-id="5522d-168">Wybierz hello **kompilacji domyślne** , a następnie w obszarze kontroler kompilacji, sprawdź nazwę hello powitania serwera kompilacji.</span><span class="sxs-lookup"><span data-stu-id="5522d-168">Choose hello **Build Defaults** tab, and under Build controller, verify hello name of hello build server.</span></span>  <span data-ttu-id="5522d-169">Ponadto wybierz opcję hello **folderu odrzuceń następujące toohello danych wyjściowych kompilacji kopiowania** i określ hello żądaną lokalizację docelową.</span><span class="sxs-lookup"><span data-stu-id="5522d-169">Also, choose hello option **Copy build output toohello following drop folder** and specify hello desired drop location.</span></span>
5. <span data-ttu-id="5522d-170">Wybierz hello **procesu** kartę. Na karcie procesu hello, wybierz szablon domyślny hello, w obszarze **kompilacji**, wybierz projekt hello, jeśli nie została jeszcze wybrana, a rozwiń hello **zaawansowane** części hello **kompilacji**części hello siatki.</span><span class="sxs-lookup"><span data-stu-id="5522d-170">Choose hello **Process** tab. On hello Process tab, choose hello default template, under **Build**, choose hello project if it is not already selected, and expand hello **Advanced** section in hello **Build** section of hello grid.</span></span>
6. <span data-ttu-id="5522d-171">Wybierz **argumenty programu MSBuild**i ustaw odpowiednie argumenty wiersza polecenia programu MSBuild hello zgodnie z opisem w kroku 2. powyżej.</span><span class="sxs-lookup"><span data-stu-id="5522d-171">Choose **MSBuild Arguments**, and set hello appropriate MSBuild command line arguments as described in Step 2 above.</span></span> <span data-ttu-id="5522d-172">Na przykład wprowadź **/t: publikowanie /p:PublishDir =\\\\MójSerwer\\porzuca\\**  toobuild pakietu hello pakietu i skopiuj pliki lokalizacji toohello \\ \\MójSerwer\\porzuca\\:</span><span class="sxs-lookup"><span data-stu-id="5522d-172">For example, enter **/t:Publish /p:PublishDir=\\\\myserver\\drops\\** toobuild a package and copy hello package files toohello location \\\\myserver\\drops\\:</span></span>

   ![Argumenty programu MSBuild][2]

   > [!NOTE]
   > <span data-ttu-id="5522d-174">Kopiowanie tooa pliki hello udziału umożliwia łatwiejsze toomanually wdrażania pakietów hello na komputerze projektowym.</span><span class="sxs-lookup"><span data-stu-id="5522d-174">Copying hello files tooa public share makes it easier toomanually deploy hello packages from your development computer.</span></span>
7. <span data-ttu-id="5522d-175">Testowanie hello Powodzenie z kroku kompilacji sprawdzając w projekcie tooyour zmiany lub kolejki nowej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="5522d-175">Test hello success of your build step by checking in a change tooyour project, or queue up a new build.</span></span> <span data-ttu-id="5522d-176">Kliknij prawym przyciskiem myszy tooqueue zapasowej nowej kompilacji w programie Team Explorer **wszystkie definicje kompilacji,** , a następnie wybierz **Tworzenie nowej kolejki**.</span><span class="sxs-lookup"><span data-stu-id="5522d-176">tooqueue up a new build, in the Team Explorer, right-click **All Build Definitions,** and then choose **Queue New Build**.</span></span>

## <a name="4-publish-a-package-using-a-powershell-script"></a><span data-ttu-id="5522d-177">4: publikowanie pakietu przy użyciu skryptu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="5522d-177">4: Publish a Package using a PowerShell Script</span></span>
<span data-ttu-id="5522d-178">W tej sekcji opisano, jak tooconstruct skrypt programu Windows PowerShell, która będzie publikować pakiet aplikacji hello chmury output tooAzure przy użyciu parametrów opcjonalnych.</span><span class="sxs-lookup"><span data-stu-id="5522d-178">This section describes how tooconstruct a Windows PowerShell script that will publish hello Cloud app package output tooAzure using optional parameters.</span></span> <span data-ttu-id="5522d-179">Ten skrypt można wywołać po wykonaniu kroku kompilacji hello w Twojej automatyzacji niestandardowej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="5522d-179">This script can be called after hello build step in your custom build automation.</span></span> <span data-ttu-id="5522d-180">Można również nadać mu z szablonu procesu działania przepływu pracy w Visual Studio TFS Team Build.</span><span class="sxs-lookup"><span data-stu-id="5522d-180">It can also be called from Process Template workflow activities in Visual Studio TFS Team Build.</span></span>

1. <span data-ttu-id="5522d-181">Zainstaluj hello [poleceń cmdlet programu Azure PowerShell] [ Azure PowerShell cmdlets] (v0.6.1 lub nowszej).</span><span class="sxs-lookup"><span data-stu-id="5522d-181">Install hello [Azure PowerShell cmdlets][Azure PowerShell cmdlets] (v0.6.1 or higher).</span></span>
   <span data-ttu-id="5522d-182">Podczas fazy instalacji polecenia cmdlet hello należy wybrać tooinstall jako przystawki.</span><span class="sxs-lookup"><span data-stu-id="5522d-182">During hello cmdlet setup phase, choose tooinstall as a snap-in.</span></span> <span data-ttu-id="5522d-183">Należy zwrócić uwagę, czy tego oficjalnie obsługiwana wersja zastępuje starszej wersji hello oferowane za pośrednictwem portalu CodePlex, chociaż hello poprzednie wersje zostały numerowane 2.x.x.</span><span class="sxs-lookup"><span data-stu-id="5522d-183">Note that this officially supported version replaces hello older version offered through CodePlex, although hello previous versions were numbered 2.x.x.</span></span>
2. <span data-ttu-id="5522d-184">Uruchom program PowerShell Azure przy użyciu hello Start menu lub strony początkowej.</span><span class="sxs-lookup"><span data-stu-id="5522d-184">Start Azure PowerShell using hello Start menu or Start page.</span></span> <span data-ttu-id="5522d-185">Po uruchomieniu w ten sposób hello poleceń cmdlet programu Azure PowerShell zostanie załadowany.</span><span class="sxs-lookup"><span data-stu-id="5522d-185">If you start in this way, hello Azure PowerShell cmdlets will be loaded.</span></span>
3. <span data-ttu-id="5522d-186">W wierszu polecenia programu PowerShell hello, sprawdź, czy polecenia cmdlet programu PowerShell hello są załadowane przez wprowadzenie polecenia częściowe hello `Get-Azure` , a następnie naciskając klawisz hello klawisza Tab do uzupełniania instrukcji.</span><span class="sxs-lookup"><span data-stu-id="5522d-186">At hello PowerShell prompt, verify that hello PowerShell cmdlets are loaded by entering hello partial command `Get-Azure` and then pressing hello Tab key for statement completion.</span></span>

   <span data-ttu-id="5522d-187">Po naciśnięciu klawisza Tab hello wielokrotnie, powinny pojawić różne polecenia programu PowerShell systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="5522d-187">If you press hello Tab key repeatedly, you should see various Azure PowerShell commands.</span></span>
4. <span data-ttu-id="5522d-188">Sprawdź, czy masz połączenie tooyour subskrypcji platformy Azure przez zaimportowanie informacji o subskrypcji z pliku .publishsettings hello.</span><span class="sxs-lookup"><span data-stu-id="5522d-188">Verify that you can connect tooyour Azure subscription by importing your subscription information from hello .publishsettings file.</span></span>

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   <span data-ttu-id="5522d-189">Następnie wprowadź polecenie hello</span><span class="sxs-lookup"><span data-stu-id="5522d-189">Then enter hello command</span></span>

   `Get-AzureSubscription`

   <span data-ttu-id="5522d-190">Oznacza to, informacje o Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="5522d-190">This shows information about your subscription.</span></span> <span data-ttu-id="5522d-191">Sprawdź, czy wszystkie ustawienia są poprawne.</span><span class="sxs-lookup"><span data-stu-id="5522d-191">Verify that everything is correct.</span></span>
5. <span data-ttu-id="5522d-192">Zapisz szablon skryptu hello podana na końcu tego artykułu w folderze skryptów jako c: hello\\skryptów\\WindowsAzure\\**PublishCloudService.ps1**.</span><span class="sxs-lookup"><span data-stu-id="5522d-192">Save hello script template provided at hello end of this article to your scripts folder as c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span></span>
6. <span data-ttu-id="5522d-193">Przejrzyj sekcję parametry hello hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="5522d-193">Review hello parameters section of hello script.</span></span> <span data-ttu-id="5522d-194">Dodaj lub zmodyfikuj wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="5522d-194">Add or modify any default values.</span></span> <span data-ttu-id="5522d-195">Te wartości zawsze może być zastąpiona przez przekazywanie parametrów jawnych.</span><span class="sxs-lookup"><span data-stu-id="5522d-195">These values can always be overridden by passing in explicit parameters.</span></span>
7. <span data-ttu-id="5522d-196">Upewnij się, istnieją usługi w chmurze prawidłowe i kont magazynu utworzonych w ramach subskrypcji, która może być celem hello publikowanie skryptu.</span><span class="sxs-lookup"><span data-stu-id="5522d-196">Ensure there are valid cloud service and storage accounts created in your subscription that can be targeted by hello publish script.</span></span> <span data-ttu-id="5522d-197">Konto magazynu (magazynu obiektów blob) zostanie użyty tooupload i tymczasowe przechowywanie hello wdrożenia pakietu i pliku konfiguracji podczas tworzenia wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="5522d-197">The storage account (blob storage) will be used tooupload and temporarily store hello deployment package and config file while the deployment is being created.</span></span>

   * <span data-ttu-id="5522d-198">toocreate nową usługę w chmurze, można wywołać tego skryptu lub użyj hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5522d-198">toocreate a new cloud service, you can call this script or use hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="5522d-199">Nazwa usługi w chmurze Hello będzie służyć jako prefiksu w pełni kwalifikowaną nazwę domeny i dlatego musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="5522d-199">hello cloud service name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span>

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * <span data-ttu-id="5522d-200">toocreate nowe konto magazynu, można wywołać tego skryptu lub użyj hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5522d-200">toocreate a new storage account, you can call this script or use hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="5522d-201">Nazwa konta magazynu Hello będzie służyć jako prefiksu w pełni kwalifikowaną nazwę domeny i dlatego musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="5522d-201">hello storage account name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span> <span data-ttu-id="5522d-202">Spróbuj użyć hello takie same nazwy jako usługa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5522d-202">You can try using hello same name as the cloud service.</span></span>

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. <span data-ttu-id="5522d-203">Wywołanie skryptu hello bezpośrednio z programu Azure PowerShell lub okablować się tego skryptu tooyour hosta kompilacji automatyzacji toooccur po hello kompilacji pakietu.</span><span class="sxs-lookup"><span data-stu-id="5522d-203">Call hello script directly from Azure PowerShell, or wire up this script tooyour host build automation toooccur after hello package build.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="5522d-204">skrypt Hello będzie zawsze usunąć lub zamienić istniejący wdrożeń domyślnie, jeśli ich wykrycia.</span><span class="sxs-lookup"><span data-stu-id="5522d-204">hello script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="5522d-205">Jest to niezbędne do włączenia ciągłego dostarczania automatyzacji, jeśli to możliwe nie monitowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5522d-205">This is necessary to enable continuous delivery from automation where no user prompting is possible.</span></span>
   >
   >

   <span data-ttu-id="5522d-206">**Przykładowy scenariusz 1:** toohello ciągłe wdrażanie tymczasowej środowiska usługi:</span><span class="sxs-lookup"><span data-stu-id="5522d-206">**Example scenario 1:** continuous deployment toohello staging environment of a service:</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="5522d-207">To jest zazwyczaj następuje testu weryfikacji i wymiany wirtualnych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="5522d-207">This is typically followed up by test run verification and a VIP swap.</span></span> <span data-ttu-id="5522d-208">swap Hello VIP może odbywać się za pośrednictwem hello [portalu Azure](https://portal.azure.com) lub za pomocą polecenia cmdlet hello przenoszenia wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="5522d-208">hello VIP swap can be done via hello [Azure portal](https://portal.azure.com) or by using hello Move-Deployment cmdlet.</span></span>

   <span data-ttu-id="5522d-209">**Przykładowy scenariusz 2:** środowiska produkcyjnego toohello ciągłego wdrażania usługi dedykowanych testu</span><span class="sxs-lookup"><span data-stu-id="5522d-209">**Example scenario 2:** continuous deployment toohello production environment of a dedicated test service</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="5522d-210">**Pulpit zdalny:**</span><span class="sxs-lookup"><span data-stu-id="5522d-210">**Remote Desktop:**</span></span>

   <span data-ttu-id="5522d-211">Włączenie pulpitu zdalnego w projekcie platformy Azure należy tooperform dodatkowe kroki jednorazowe hello tooensure, który jest poprawny certyfikat usługi w chmurze przekazać usługi w chmurze tooall celem tego skryptu.</span><span class="sxs-lookup"><span data-stu-id="5522d-211">If Remote Desktop is enabled in your Azure project you will need tooperform additional one-time steps tooensure hello correct Cloud Service Certificate is uploaded tooall cloud services targeted by this script.</span></span>

   <span data-ttu-id="5522d-212">Znajdź wartości odcisku palca certyfikatu hello oczekiwany przez poszczególnych ról.</span><span class="sxs-lookup"><span data-stu-id="5522d-212">Locate hello certificate thumbprint values expected by your roles.</span></span> <span data-ttu-id="5522d-213">Wartości odcisku palca są widoczne w sekcji certyfikaty hello pliku konfiguracji chmury (tj. ServiceConfiguration.Cloud.cscfg).</span><span class="sxs-lookup"><span data-stu-id="5522d-213">The thumbprint values are visible in hello Certificates section of the cloud config file (i.e. ServiceConfiguration.Cloud.cscfg).</span></span> <span data-ttu-id="5522d-214">Jest również widoczna w oknie dialogowym Konfiguracja usług pulpitu zdalnego hello w programie Visual Studio, gdy hello Pokaż opcje i widok wybranego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="5522d-214">It is also visible in hello Remote Desktop Configuration dialog in Visual Studio when you Show Options and view hello selected certificate.</span></span>

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   <span data-ttu-id="5522d-215">Przekaż certyfikaty usług pulpitu zdalnego za pomocą następującego polecenia cmdlet skryptu hello krokiem jednorazowej konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="5522d-215">Upload Remote Desktop certificates as a one-time setup step using hello following cmdlet script:</span></span>

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   <span data-ttu-id="5522d-216">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="5522d-216">For example:</span></span>

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   <span data-ttu-id="5522d-217">Alternatywnie można wyeksportować plik certyfikatu PFX hello z kluczem prywatnym i przekazywania certyfikaty tooeach docelowej chmury usługi przy użyciu [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5522d-217">Alternatively you can export hello certificate file PFX with private key and upload certificates tooeach target cloud service using the [Azure portal](https://portal.azure.com).</span></span>

   <!---
   Fixing broken links for Azure content migration from ACOM tooDOCS. I'm unable toofind a replacement links, so I'm commenting out this reference for now. hello author can investigate in hello future. "Read hello following article toolearn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   <span data-ttu-id="5522d-218">**Uaktualnienie a wdrożenia. Usunięcie wdrożenia —\> nowego wdrożenia**</span><span class="sxs-lookup"><span data-stu-id="5522d-218">**Upgrade Deployment vs. Delete Deployment -\> New Deployment**</span></span>

   <span data-ttu-id="5522d-219">skrypt Hello będzie domyślnie wykonywać uaktualniania wdrożenia ($enableDeploymentUpgrade = 1) gdy brak parametru jest przekazano lub nie została jawnie przekazana wartość 1.</span><span class="sxs-lookup"><span data-stu-id="5522d-219">hello script will by default perform an Upgrade Deployment ($enableDeploymentUpgrade = 1) when no parameter is passed in or the value 1 is passed explicitly.</span></span> <span data-ttu-id="5522d-220">Dla pojedynczego wystąpienia to zaletą jest mniej czasu niż pełne wdrożenie.</span><span class="sxs-lookup"><span data-stu-id="5522d-220">For single instances this has the advantage of taking less time than a full deployment.</span></span> <span data-ttu-id="5522d-221">Dla wystąpień, które wymagają wysokiej dostępności ma to również zaletą hello pozostawienie niektórych wystąpień uruchomiona, podczas gdy inne uaktualnienia (przejście domenę aktualizacji), a także Twojego adresu VIP, nie zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="5522d-221">For instances that require high availability this also has hello advantage of leaving some instances running while others are upgraded (walking your update domain), plus your VIP will not be deleted.</span></span>

   <span data-ttu-id="5522d-222">Wdrożenia uaktualnienia można wyłączyć w skrypcie hello ($enableDeploymentUpgrade = 0) lub przez przekazanie *- enableDeploymentUpgrade 0* jako parametr zmienia delete toofirst zachowanie skryptu wszystkie istniejące wdrożenia i utworzyć nowe wdrożenie.</span><span class="sxs-lookup"><span data-stu-id="5522d-222">Upgrade Deployment can be disabled in hello script ($enableDeploymentUpgrade = 0) or by passing *-enableDeploymentUpgrade 0* as a parameter, which alters the script behavior toofirst delete any existing deployment and then create a new deployment.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="5522d-223">skrypt Hello będzie zawsze usunąć lub zamienić istniejący wdrożeń domyślnie, jeśli ich wykrycia.</span><span class="sxs-lookup"><span data-stu-id="5522d-223">hello script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="5522d-224">Jest to niezbędne do włączenia ciągłego dostarczania automatyzacji, jeśli to możliwe nie monitowania użytkownika / — operator.</span><span class="sxs-lookup"><span data-stu-id="5522d-224">This is necessary to enable continuous delivery from automation where no user/operator prompting is possible.</span></span>
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a><span data-ttu-id="5522d-225">5: publikowanie pakietu za pomocą kompilacji TFS zespołu</span><span class="sxs-lookup"><span data-stu-id="5522d-225">5: Publish a Package using TFS Team Build</span></span>
<span data-ttu-id="5522d-226">Ten opcjonalny krok łączy TFS Team Build toohello skryptu utworzonego w kroku 4, który obsługuje publikowanie tooAzure kompilacji pakietu hello.</span><span class="sxs-lookup"><span data-stu-id="5522d-226">This optional step connects TFS Team Build toohello script created in step 4, which handles publishing of hello package build tooAzure.</span></span> <span data-ttu-id="5522d-227">Pociąga za sobą modyfikowanie hello szablonu procesu używanego przez definicję kompilacji, wykonywania działań publikowania na końcu hello hello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="5522d-227">This entails modifying hello Process Template used by your build definition so that it runs a Publish activity at hello end of hello workflow.</span></span> <span data-ttu-id="5522d-228">Witaj Publikuj działania wykona przekazywanie parametrów z kompilacji hello polecenia programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5522d-228">hello Publish activity will execute your PowerShell command passing in parameters from hello build.</span></span> <span data-ttu-id="5522d-229">W danych wyjściowych kompilacji standardowe hello będzie przekazywany w potoku dane wyjściowe hello MSBuild elementów docelowych i opublikuj skryptu.</span><span class="sxs-lookup"><span data-stu-id="5522d-229">Output of hello MSBuild targets and publish script will be piped into hello standard build output.</span></span>

1. <span data-ttu-id="5522d-230">Edytuj hello definicji kompilacji odpowiedzialny za ciągłego wdrażania.</span><span class="sxs-lookup"><span data-stu-id="5522d-230">Edit hello Build Definition responsible for continuous deploy.</span></span>
2. <span data-ttu-id="5522d-231">Wybierz hello **procesu** kartę.</span><span class="sxs-lookup"><span data-stu-id="5522d-231">Select hello **Process** tab.</span></span>
3. <span data-ttu-id="5522d-232">Postępuj zgodnie z [tych instrukcji](http://msdn.microsoft.com/library/dd647551.aspx) tooadd projekt działania hello szablon procesu kompilacji, Pobierz szablon domyślny hello, dodaj go do projektu hello i go zaewidencjonować.</span><span class="sxs-lookup"><span data-stu-id="5522d-232">Follow [these instructions](http://msdn.microsoft.com/library/dd647551.aspx) tooadd an Activity project for hello build process template, download hello default template, add it to hello project and check it in.</span></span> <span data-ttu-id="5522d-233">Nadaj nazwę nowej, takich jak AzureBuildProcessTemplate szablonu procesu kompilacji hello.</span><span class="sxs-lookup"><span data-stu-id="5522d-233">Give hello build process template a new name, such as AzureBuildProcessTemplate.</span></span>
4. <span data-ttu-id="5522d-234">Zwraca toohello **procesu** , a następnie użyć **Pokaż szczegóły** tooshow listę szablonów procesu kompilacji dostępne.</span><span class="sxs-lookup"><span data-stu-id="5522d-234">Return toohello **Process** tab, and use **Show Details** tooshow a list of available build process templates.</span></span> <span data-ttu-id="5522d-235">Wybierz hello **nowy...**  przycisk, a następnie przejdź projektu toohello właśnie dodany i zaewidencjonowane.</span><span class="sxs-lookup"><span data-stu-id="5522d-235">Choose hello **New...** button, and navigate toohello project you just added and checked in.</span></span> <span data-ttu-id="5522d-236">Znajdź właśnie utworzony szablon hello i wybierz polecenie **OK**.</span><span class="sxs-lookup"><span data-stu-id="5522d-236">Locate hello template you just created and choose **OK**.</span></span>
5. <span data-ttu-id="5522d-237">Otwórz hello wybrany szablon procesu do edycji.</span><span class="sxs-lookup"><span data-stu-id="5522d-237">Open hello selected Process Template for editing.</span></span> <span data-ttu-id="5522d-238">Możesz otworzyć bezpośrednio w Projektancie przepływów pracy hello lub toowork edytora XML hello z hello XAML.</span><span class="sxs-lookup"><span data-stu-id="5522d-238">You can open directly in hello Workflow designer or in hello XML editor toowork with hello XAML.</span></span>
6. <span data-ttu-id="5522d-239">Dodaj następujące listy argumentów nowe jako odrębne pozycje hello argumenty karcie projektanta przepływów pracy hello hello.</span><span class="sxs-lookup"><span data-stu-id="5522d-239">Add hello following list of new arguments as separate line items in hello arguments tab of hello workflow designer.</span></span> <span data-ttu-id="5522d-240">Wszystkie argumenty powinny posiadać kierunek = w i wpisz = ciąg.</span><span class="sxs-lookup"><span data-stu-id="5522d-240">All arguments should have direction=In and type=String.</span></span> <span data-ttu-id="5522d-241">Te parametry są parametry używane tooflow z hello definicję kompilacji w przepływie pracy hello, które następnie hello używane toocall get publikowania skryptu.</span><span class="sxs-lookup"><span data-stu-id="5522d-241">These will be used tooflow parameters from hello build definition into hello workflow, which then get used toocall hello publish script.</span></span>

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![Lista argumentów][3]

   <span data-ttu-id="5522d-243">powitalne odpowiedniego XAML wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="5522d-243">hello corresponding XAML looks like this:</span></span>

       <Activity  _ />
         <x:Members>
           <x:Property Name="BuildSettings" Type="InArgument(mtbwa:BuildSettings)" />
           <x:Property Name="TestSpecs" Type="InArgument(mtbwa:TestSpecList)" />
           <x:Property Name="BuildNumberFormat" Type="InArgument(x:String)" />
           <x:Property Name="CleanWorkspace" Type="InArgument(mtbwa:CleanWorkspaceOption)" />
           <x:Property Name="RunCodeAnalysis" Type="InArgument(mtbwa:CodeAnalysisOption)" />
           <x:Property Name="SourceAndSymbolServerSettings" Type="InArgument(mtbwa:SourceAndSymbolServerSettings)" />
           <x:Property Name="AgentSettings" Type="InArgument(mtbwa:AgentSettings)" />
           <x:Property Name="AssociateChangesetsAndWorkItems" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateWorkItem" Type="InArgument(x:Boolean)" />
           <x:Property Name="DropBuild" Type="InArgument(x:Boolean)" />
           <x:Property Name="MSBuildArguments" Type="InArgument(x:String)" />
           <x:Property Name="MSBuildPlatform" Type="InArgument(mtbwa:ToolPlatform)" />
           <x:Property Name="PerformTestImpactAnalysis" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateLabel" Type="InArgument(x:Boolean)" />
           <x:Property Name="DisableTests" Type="InArgument(x:Boolean)" />
           <x:Property Name="GetVersion" Type="InArgument(x:String)" />
           <x:Property Name="PrivateDropLocation" Type="InArgument(x:String)" />
           <x:Property Name="Verbosity" Type="InArgument(mtbw:BuildVerbosity)" />
           <x:Property Name="Metadata" Type="mtbw:ProcessParameterMetadataCollection" />
           <x:Property Name="SupportedReasons" Type="mtbc:BuildReason" />
           <x:Property Name="SubscriptionName" Type="InArgument(x:String)" />
           <x:Property Name="StorageAccountName" Type="InArgument(x:String)" />
           <x:Property Name="CloudConfigLocation" Type="InArgument(x:String)" />
           <x:Property Name="PackageLocation" Type="InArgument(x:String)" />
           <x:Property Name="Environment" Type="InArgument(x:String)" />
           <x:Property Name="SubscriptionDataFileLocation" Type="InArgument(x:String)" />
           <x:Property Name="PublishScriptLocation" Type="InArgument(x:String)" />
           <x:Property Name="ServiceName" Type="InArgument(x:String)" />
         </x:Members>

         <this:Process.MSBuildArguments>
7. <span data-ttu-id="5522d-244">Dodaj nową sekwencję na końcu hello Uruchom na agenta:</span><span class="sxs-lookup"><span data-stu-id="5522d-244">Add a new sequence at hello end of Run On Agent:</span></span>

   1. <span data-ttu-id="5522d-245">Rozpocznij od dodania toocheck działania Jeśli instrukcji dla prawidłowym plikiem skryptu.</span><span class="sxs-lookup"><span data-stu-id="5522d-245">Start by adding an If Statement activity toocheck for a valid script file.</span></span> <span data-ttu-id="5522d-246">Ustaw wartość toothis warunku hello:</span><span class="sxs-lookup"><span data-stu-id="5522d-246">Set hello condition toothis value:</span></span>

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. <span data-ttu-id="5522d-247">W hello następnie przypadku hello Jeśli instrukcji Dodaj nowe działanie w sekwencji.</span><span class="sxs-lookup"><span data-stu-id="5522d-247">In hello Then case of hello If Statement, add a new Sequence activity.</span></span> <span data-ttu-id="5522d-248">Publikowanie zestawu hello wyświetlana nazwa too'Start "</span><span class="sxs-lookup"><span data-stu-id="5522d-248">Set hello display name too'Start publish'</span></span>
   3. <span data-ttu-id="5522d-249">Z hello rozpoczęcia publikowania sekwencji nadal zaznaczony Dodaj na następującej liście nowe zmienne jako oddzielne pozycje w karcie Zmienne hello projektanta przepływów pracy.</span><span class="sxs-lookup"><span data-stu-id="5522d-249">With hello Start publish sequence still selected, add the following list of new variables as separate line items in the variables tab of hello workflow designer.</span></span> <span data-ttu-id="5522d-250">Wszystkie zmienne powinny mieć typ zmiennej = ciągu i zakres = rozpoczęcie publikowania.</span><span class="sxs-lookup"><span data-stu-id="5522d-250">All variables should have Variable type =String and Scope=Start publish.</span></span> <span data-ttu-id="5522d-251">Te parametry są parametry używane tooflow z hello definicji kompilacji do przepływu pracy, które następnie hello używane toocall get publikowania skryptu.</span><span class="sxs-lookup"><span data-stu-id="5522d-251">These will be used tooflow parameters from hello build definition into the workflow, which then get used toocall hello publish script.</span></span>

      * <span data-ttu-id="5522d-252">SubscriptionDataFilePath typu String</span><span class="sxs-lookup"><span data-stu-id="5522d-252">SubscriptionDataFilePath, of type String</span></span>
      * <span data-ttu-id="5522d-253">PublishScriptFilePath typu String</span><span class="sxs-lookup"><span data-stu-id="5522d-253">PublishScriptFilePath, of type String</span></span>

        ![Nowe zmienne][4]
   4. <span data-ttu-id="5522d-255">Jeśli korzystają z programu TFS 2012 lub starszy, Dodaj działanie ConvertWorkspaceItem początku hello hello nowej sekwencji.</span><span class="sxs-lookup"><span data-stu-id="5522d-255">If you are using TFS 2012 or earlier, add a ConvertWorkspaceItem activity at hello beginning of hello new Sequence.</span></span> <span data-ttu-id="5522d-256">Jeśli używasz programu TFS 2013 lub nowszy, Dodaj działanie GetLocalPath początku hello hello nowej sekwencji.</span><span class="sxs-lookup"><span data-stu-id="5522d-256">If you are using TFS 2013 or later, add a GetLocalPath activity at hello beginning of hello new sequence.</span></span> <span data-ttu-id="5522d-257">Dla ConvertWorkspaceItem, ustaw właściwości hello w następujący sposób: kierunek = ServerToLocal, nazwa wyświetlana = 'Convert opublikować nazwę pliku skryptu', dane wejściowe = "PublishScriptLocation", wynik = "PublishScriptFilePath", obszar roboczy = "Obszar roboczy".</span><span class="sxs-lookup"><span data-stu-id="5522d-257">For a ConvertWorkspaceItem, set hello properties as follows: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="5522d-258">Dla działania GetLocalPath, ustaw too'PublishScriptLocation IncomingPath właściwości hello ", a hello too'PublishScriptFilePath wynik".</span><span class="sxs-lookup"><span data-stu-id="5522d-258">For a GetLocalPath activity, set hello property IncomingPath too'PublishScriptLocation', and hello Result too'PublishScriptFilePath'.</span></span> <span data-ttu-id="5522d-259">To działanie konwertuje hello ścieżki toohello publikowania skryptu z lokalizacji serwera TFS (jeśli dotyczy) tooa ścieżka standardowe dysku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="5522d-259">This activity converts hello path toohello publish script from TFS server locations (if applicable) tooa standard local disk path.</span></span>
   5. <span data-ttu-id="5522d-260">Jeśli używasz programu TFS 2012 lub wcześniej, Dodaj kolejne działanie ConvertWorkspaceItem na końcu hello hello nowej sekwencji.</span><span class="sxs-lookup"><span data-stu-id="5522d-260">If you are using TFS 2012 or earlier, add another ConvertWorkspaceItem activity at hello end of hello new Sequence.</span></span> <span data-ttu-id="5522d-261">Kierunek = ServerToLocal, nazwa wyświetlana = "Dokonać konwersji subskrypcji nazwa_pliku", dane wejściowe = "SubscriptionDataFileLocation", wynik = "SubscriptionDataFilePath", obszar roboczy = "Obszar roboczy".</span><span class="sxs-lookup"><span data-stu-id="5522d-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="5522d-262">Jeśli używasz programu TFS 2013 lub nowszy, Dodaj inny GetLocalPath.</span><span class="sxs-lookup"><span data-stu-id="5522d-262">If you are using TFS 2013 or later, add another GetLocalPath.</span></span> <span data-ttu-id="5522d-263">IncomingPath = "SubscriptionDataFileLocation", a wynik = "SubscriptionDataFilePath."</span><span class="sxs-lookup"><span data-stu-id="5522d-263">IncomingPath='SubscriptionDataFileLocation', and Result='SubscriptionDataFilePath.'</span></span>
   6. <span data-ttu-id="5522d-264">Dodawanie działania InvokeProcess na końcu hello hello nowej sekwencji.</span><span class="sxs-lookup"><span data-stu-id="5522d-264">Add an InvokeProcess activity at hello end of hello new Sequence.</span></span>
      <span data-ttu-id="5522d-265">Tego wywołania działania PowerShell.exe z argumentami hello przekazany przez hello definicji kompilacji.</span><span class="sxs-lookup"><span data-stu-id="5522d-265">This activity calls PowerShell.exe with hello arguments passed in by hello Build Definition.</span></span>

      + <span data-ttu-id="5522d-266">Argumenty = String.Format ("-""{0}" "- serviceName {1} - storageAccountName {2} tabelę packageLocation —""{3}" "- cloudConfigLocation""{4}" "- subscriptionDataFile""{5}" "- selectedSubscription {6} pliku-środowiska""{7}" "",  PublishScriptFilePath, ServiceName, StorageAccountName, tabelę PackageLocation, CloudConfigLocation, SubscriptionDataFilePath, Nazwa subskrypcji, środowisko)</span><span class="sxs-lookup"><span data-stu-id="5522d-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span></span>
      + <span data-ttu-id="5522d-267">Nazwa wyświetlana = Execute publikowania skryptu</span><span class="sxs-lookup"><span data-stu-id="5522d-267">DisplayName = Execute publish script</span></span>
      + <span data-ttu-id="5522d-268">Nazwa pliku = "PowerShell" (zawierają hello oferty)</span><span class="sxs-lookup"><span data-stu-id="5522d-268">FileName = "PowerShell" (include hello quotes)</span></span>
      + <span data-ttu-id="5522d-269">OutputEncoding = System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span><span class="sxs-lookup"><span data-stu-id="5522d-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span></span>
   7. <span data-ttu-id="5522d-270">W hello **Obsługa standardowego wyjścia** sekcji textbox InvokeProcess, ustaw too'data wartości tekstowe hello ".</span><span class="sxs-lookup"><span data-stu-id="5522d-270">In hello **Handle Standard Output** section textbox of the InvokeProcess, set hello textbox value too'data'.</span></span> <span data-ttu-id="5522d-271">To dane wyjścia standardowego hello toostore zmiennej.</span><span class="sxs-lookup"><span data-stu-id="5522d-271">This is a variable toostore hello standard output data.</span></span>
   8. <span data-ttu-id="5522d-272">Dodaj działanie WriteBuildMessage poniżej hello **Obsługa standardowego wyjścia** sekcji.</span><span class="sxs-lookup"><span data-stu-id="5522d-272">Add a WriteBuildMessage activity just below hello **Handle Standard Output** section.</span></span> <span data-ttu-id="5522d-273">Ustaw hello znaczenie = "Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High" i wiadomość hello = "dane".</span><span class="sxs-lookup"><span data-stu-id="5522d-273">Set hello Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' and hello Message='data'.</span></span> <span data-ttu-id="5522d-274">Dzięki temu hello standardowe dane wyjściowe skryptu zostanie zapisane dane wyjściowe kompilacji toohello.</span><span class="sxs-lookup"><span data-stu-id="5522d-274">This ensures hello standard output of the script will get written toohello build output.</span></span>
   9. <span data-ttu-id="5522d-275">W hello **obsługi błędów wyjścia** sekcji textbox InvokeProcess, ustaw too'data wartości tekstowe hello ".</span><span class="sxs-lookup"><span data-stu-id="5522d-275">In hello **Handle Error Output** section textbox of the InvokeProcess, set hello textbox value too'data'.</span></span> <span data-ttu-id="5522d-276">To dane błąd standardowy hello toostore zmiennej.</span><span class="sxs-lookup"><span data-stu-id="5522d-276">This is a variable toostore hello standard error data.</span></span>
   10. <span data-ttu-id="5522d-277">Dodaj działanie WriteBuildError poniżej hello **obsługi błędów wyjścia** sekcji.</span><span class="sxs-lookup"><span data-stu-id="5522d-277">Add a WriteBuildError activity just below hello **Handle Error Output** section.</span></span> <span data-ttu-id="5522d-278">Ustaw wiadomość hello = "dane".</span><span class="sxs-lookup"><span data-stu-id="5522d-278">Set hello Message='data'.</span></span> <span data-ttu-id="5522d-279">Dzięki temu, że błędy standardowe hello skryptu hello zostaną zapisane dane wyjściowe błędów kompilacji toohello.</span><span class="sxs-lookup"><span data-stu-id="5522d-279">This ensures hello standard errors of hello script will get written toohello build error output.</span></span>
   11. <span data-ttu-id="5522d-280">Popraw błędy wskazywanym przez niebieski znaczniki wykrzyknika.</span><span class="sxs-lookup"><span data-stu-id="5522d-280">Correct any errors, indicated by blue exclamation marks.</span></span> <span data-ttu-id="5522d-281">Umieść kursor nad tooget znaczniki wykrzyknika wskazówkę o błędzie hello.</span><span class="sxs-lookup"><span data-stu-id="5522d-281">Hover over the exclamation marks tooget a hint about hello error.</span></span> <span data-ttu-id="5522d-282">Zapisz hello przepływu pracy, aby usunąć błędy.</span><span class="sxs-lookup"><span data-stu-id="5522d-282">Save hello workflow to clear errors.</span></span>

   <span data-ttu-id="5522d-283">wynik końcowy Hello hello opublikować przepływu pracy działania będzie wyglądać następująco w Projektancie hello:</span><span class="sxs-lookup"><span data-stu-id="5522d-283">hello final result of hello publish workflow activities will look like this in hello designer:</span></span>

   ![Działania przepływu pracy][5]

   <span data-ttu-id="5522d-285">wynik końcowy Hello hello opublikować działań będzie wyglądać następująco w języku XAML przepływu pracy:</span><span class="sxs-lookup"><span data-stu-id="5522d-285">hello final result of hello publish workflow activities will look like this in XAML:</span></span>

       <If Condition="[Not String.IsNullOrEmpty(PublishScriptLocation)]" sap2010:WorkflowViewState.IdRef="If_1">
           <If.Then>
             <Sequence DisplayName="Start Publish" sap2010:WorkflowViewState.IdRef="Sequence_4">
               <Sequence.Variables>
                 <Variable x:TypeArguments="x:String" Name="SubscriptionDataFilePath" />
                 <Variable x:TypeArguments="x:String" Name="PublishScriptFilePath" />
               </Sequence.Variables>
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert publish script filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_1" Input="[PublishScriptLocation]" Result="[PublishScriptFilePath]" Workspace="[Workspace]" />
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert subscription filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_2" Input="[SubscriptionDataFileLocation]" Result="[SubscriptionDataFilePath]" Workspace="[Workspace]" />
               <mtbwa:InvokeProcess Arguments="[String.Format(&quot; -File &quot;&quot;{0}&quot;&quot; -serviceName {1}&#xD;&#xA;            -storageAccountName {2} -packageLocation &quot;&quot;{3}&quot;&quot;&#xD;&#xA;            -cloudConfigLocation &quot;&quot;{4}&quot;&quot; -subscriptionDataFile &quot;&quot;{5}&quot;&quot;&#xD;&#xA;            -selectedSubscription {6} -environment &quot;&quot;{7}&quot;&quot;&quot;,&#xD;&#xA;            PublishScriptFilePath, ServiceName, StorageAccountName,&#xD;&#xA;            PackageLocation, CloudConfigLocation,&#xD;&#xA;            SubscriptionDataFilePath, SubscriptionName, Environment)]" DisplayName="'Execute Publish Script'" FileName="[PowerShell]" sap2010:WorkflowViewState.IdRef="InvokeProcess_1">
                 <mtbwa:InvokeProcess.ErrorDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildError Message="{x:Null}" sap2010:WorkflowViewState.IdRef="WriteBuildError_1" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.ErrorDataReceived>
                 <mtbwa:InvokeProcess.OutputDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildMessage sap2010:WorkflowViewState.IdRef="WriteBuildMessage_2" Importance="[Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High]" Message="[data]" mva:VisualBasic.Settings="Assembly references and imported namespaces serialized as XML namespaces" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.OutputDataReceived>
               </mtbwa:InvokeProcess>
             </Sequence>
           </If.Then>
         </If>
       </Sequence>
8. <span data-ttu-id="5522d-286">Zapisz hello przepływu pracy szablonu procesu dla kompilacji i zaewidencjonuj tego pliku.</span><span class="sxs-lookup"><span data-stu-id="5522d-286">Save hello build process template workflow and Check In this file.</span></span>
9. <span data-ttu-id="5522d-287">Edytowanie definicji kompilacji hello (je zamknąć, jeżeli jest już otwarty) i wybierz hello **nowy** przycisku, jeśli nie ma jeszcze hello nowego szablonu na liście hello szablonów procesu.</span><span class="sxs-lookup"><span data-stu-id="5522d-287">Edit hello build definition (close it if it is already open), and select hello **New** button if you do not yet see hello new template in hello list of Process Templates.</span></span>
10. <span data-ttu-id="5522d-288">Ustawiania wartości właściwości parametru hello w sekcji różne hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="5522d-288">Set hello parameter property values in hello Misc section as follows:</span></span>

    1. <span data-ttu-id="5522d-289">CloudConfigLocation = "c:\\porzuca\\app.publish\\ServiceConfiguration.Cloud.cscfg" *ta wartość jest określana na podstawie: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span><span class="sxs-lookup"><span data-stu-id="5522d-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *This value is derived from: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span></span>
    2. <span data-ttu-id="5522d-290">Tabelę PackageLocation = "c:\\porzuca\\app.publish\\ContactManager.Azure.cspkg" *ta wartość jest określana na podstawie: (cspkg)($ProjectName) $PublishDir*</span><span class="sxs-lookup"><span data-stu-id="5522d-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *This value is derived from: ($PublishDir)($ProjectName).cspkg*</span></span>
    3. <span data-ttu-id="5522d-291">PublishScriptLocation = "c:\\skryptów\\WindowsAzure\\PublishCloudService.ps1"</span><span class="sxs-lookup"><span data-stu-id="5522d-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span></span>
    4. <span data-ttu-id="5522d-292">ServiceName = "mycloudservicename" *Użyj hello odpowiednie nazwa usługi w chmurze w tym miejscu*</span><span class="sxs-lookup"><span data-stu-id="5522d-292">ServiceName = 'mycloudservicename' *Use hello appropriate cloud service name here*</span></span>
    5. <span data-ttu-id="5522d-293">Środowisko = "Tymczasowe"</span><span class="sxs-lookup"><span data-stu-id="5522d-293">Environment = 'Staging'</span></span>
    6. <span data-ttu-id="5522d-294">StorageAccountName = "mystorageaccountname" *Użyj hello odpowiednie nazwy konta magazynu w tym miejscu*</span><span class="sxs-lookup"><span data-stu-id="5522d-294">StorageAccountName = 'mystorageaccountname' *Use hello appropriate storage account name here*</span></span>
    7. <span data-ttu-id="5522d-295">SubscriptionDataFileLocation = "c:\\skryptów\\WindowsAzure\\Subscription.xml"</span><span class="sxs-lookup"><span data-stu-id="5522d-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span></span>
    8. <span data-ttu-id="5522d-296">Nazwa subskrypcji = "default"</span><span class="sxs-lookup"><span data-stu-id="5522d-296">SubscriptionName = 'default'</span></span>

    ![Wartości właściwości parametru][6]
11. <span data-ttu-id="5522d-298">Zapisz hello toohello zmiany definicji kompilacji.</span><span class="sxs-lookup"><span data-stu-id="5522d-298">Save hello changes toohello Build Definition.</span></span>
12. <span data-ttu-id="5522d-299">Kolejka tooexecute kompilacji, zarówno hello kompilacji pakietu i publikowania.</span><span class="sxs-lookup"><span data-stu-id="5522d-299">Queue a Build tooexecute both hello package build and publish.</span></span> <span data-ttu-id="5522d-300">Jeśli masz wyzwalacz ustawić tooContinuous integracji wykona to zachowanie na każdym zaewidencjonowania.</span><span class="sxs-lookup"><span data-stu-id="5522d-300">If you have a trigger set tooContinuous Integration, you will execute this behavior on every check-in.</span></span>

### <a name="publishcloudserviceps1-script-template"></a><span data-ttu-id="5522d-301">PublishCloudService.ps1 skrypt szablonu</span><span class="sxs-lookup"><span data-stu-id="5522d-301">PublishCloudService.ps1 script template</span></span>
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy too$servicename",
        $timeStampFormat = "g",
        $alwaysDeleteExistingDeployments = 1,
        $enableDeploymentUpgrade = 1,
        $selectedsubscription = "default",
        $subscriptionDataFile = ""
     )


function Publish()
{
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot -ErrorVariable a -ErrorAction silentlycontinue
    if ($a[0] -ne $null)
    {
        Write-Output "$(Get-Date -f $timeStampFormat) - No deployment is detected. Creating a new deployment. "
    }
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according too$alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
    if ($deployment.Name -ne $null)
    {
        switch ($alwaysDeleteExistingDeployments)
        {
            1
            {
                switch ($enableDeploymentUpgrade)
                {
                    1  #Update deployment inplace (usually faster, cheaper, won't destroy VIP)
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Upgrading deployment."
                        UpgradeDeployment
                    }
                    0  #Delete then create new deployment
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Deleting deployment."
                        DeleteDeployment
                        CreateNewDeployment

                    }
                } # switch ($enableDeploymentUpgrade)
            }
            0
            {
                Write-Output "$(Get-Date -f $timeStampFormat) - ERROR: Deployment exists in $servicename.  Script execution cancelled."
                exit
            }
        } #switch ($alwaysDeleteExistingDeployments)
    } else {
            CreateNewDeployment
    }
}

function CreateNewDeployment()
{
    write-progress -id 3 -activity "Creating New Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: In progress"

    $opstat = New-AzureDeployment -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Creating New Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: Complete, Deployment ID: $completeDeploymentID"

    StartInstances
}

function UpgradeDeployment()
{
    write-progress -id 3 -activity "Upgrading Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: In progress"

    # perform Update-Deployment
    $setdeployment = Set-AzureDeployment -Upgrade -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName -Force

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Upgrading Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: Complete, Deployment ID: $completeDeploymentID"
}

function DeleteDeployment()
{

    write-progress -id 2 -activity "Deleting Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: In progress"

    #WARNING - always deletes with force
    $removeDeployment = Remove-AzureDeployment -Slot $slot -ServiceName $serviceName -Force

    write-progress -id 2 -activity "Deleting Deployment: Complete" -completed -Status $removeDeployment
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: Complete"

}

function StartInstances()
{
    write-progress -id 4 -activity "Starting Instances" -status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: In progress"

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $runstatus = $deployment.Status

    if ($runstatus -ne 'Running')
    {
        $run = Set-AzureDeployment -Slot $slot -ServiceName $serviceName -Status Running
    }
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $oldStatusStr = @("") * $deployment.RoleInstanceList.Count

    while (-not(AllInstancesRunning($deployment.RoleInstanceList)))
    {
        $i = 1
        foreach ($roleInstance in $deployment.RoleInstanceList)
        {
            $instanceName = $roleInstance.InstanceName
            $instanceStatus = $roleInstance.InstanceStatus

            if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
            {
                $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
                Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
            }

            write-progress -id (4 + $i) -activity "Starting Instance '$instanceName'" -status "$instanceStatus"
            $i = $i + 1
        }

        sleep -Seconds 1

        $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    }

    $i = 1
    foreach ($roleInstance in $deployment.RoleInstanceList)
    {
        $instanceName = $roleInstance.InstanceName
        $instanceStatus = $roleInstance.InstanceStatus

        if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
        {
            $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
            Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
        }

        $i = $i + 1
    }

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $opstat = $deployment.Status

    write-progress -id 4 -activity "Starting Instances" -completed -status $opstat
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: $opstat"
}

function AllInstancesRunning($roleInstanceList)
{
    foreach ($roleInstance in $roleInstanceList)
    {
        if ($roleInstance.InstanceStatus -ne "ReadyRole")
        {
            return $false
        }
    }

    return $true
}

#configure powershell with Azure 1.7 modules
Import-Module Azure

#configure powershell with publishsettings for your subscription
$pubsettings = $subscriptionDataFile
Import-AzurePublishSettingsFile $pubsettings
Set-AzureSubscription -CurrentStorageAccountName $storageAccountName -SubscriptionName $selectedsubscription
Select-AzureSubscription $selectedsubscription

#set remaining environment variables for Azure cmdlets
$subscription = Get-AzureSubscription $selectedsubscription
$subscriptionname = $subscription.subscriptionname
$subscriptionid = $subscription.subscriptionid
$slot = $environment

#main driver - publish & write progress tooactivity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a><span data-ttu-id="5522d-302">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5522d-302">Next steps</span></span>
<span data-ttu-id="5522d-303">tooenable zdalne debugowanie przy użyciu ciągłego dostarczania, zobacz [Włączanie debugowania zdalnego, korzystając z ciągłego dostarczania toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span><span class="sxs-lookup"><span data-stu-id="5522d-303">tooenable remote debugging when using continuous delivery, see [Enable remote debugging when using continuous delivery toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span></span>

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[hello .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
