---
title: "Ciągłego dostarczania dla chmury usługi z programem TFS na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować ciągłego dostarczania dla aplikacji w chmurze Azure. Przykłady kodu dla instrukcji wiersza polecenia programu MSBuild i skryptów programu PowerShell."
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
ms.openlocfilehash: 0979722b9ec715e91825c7aba74657451df6e83f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a><span data-ttu-id="a4d3e-104">Ciągłego dostarczania dla usług w chmurze na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="a4d3e-104">Continuous Delivery for Cloud Services in Azure</span></span>
<span data-ttu-id="a4d3e-105">Proces opisany w tym artykule pokazano, jak skonfigurować ciągłego dostarczania dla aplikacji w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-105">The process described in this article shows you how to set up continuous delivery for Azure cloud apps.</span></span> <span data-ttu-id="a4d3e-106">Ten proces umożliwia automatyczne tworzenie pakietów i wdrożenie pakietu w systemie Azure po każdym zaewidencjonowaniu kodu.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-106">This process enables you to automatically create packages and deploy the package to Azure after every code check-in.</span></span> <span data-ttu-id="a4d3e-107">Proces kompilacji pakietu, które są opisane w tym artykule jest odpowiednikiem **pakietu** polecenie w programie Visual Studio i kroki publikowania są równoważne **publikowania** polecenia w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-107">The package build process described in this article is equivalent to the **Package** command in Visual Studio, and the publishing steps are equivalent to the **Publish** command in Visual Studio.</span></span>
<span data-ttu-id="a4d3e-108">Artykuł obejmuje metody ma zostać użyty do utworzenia serwera kompilacji MSBuild instrukcje wiersza polecenia i skryptów programu Windows PowerShell, a on również pokazano, jak opcjonalnie skonfigurować Visual Studio Team Foundation Server - Team Build definicje do użycia MSBuild poleceń i skryptów programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-108">The article covers the methods you would use to create a build server with MSBuild command-line statements and Windows PowerShell scripts, and it also demonstrates how to optionally configure Visual Studio Team Foundation Server - Team Build definitions to use the MSBuild commands and PowerShell scripts.</span></span> <span data-ttu-id="a4d3e-109">Ten proces jest można dostosować do własnego środowiska kompilacji i środowisk docelowej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-109">The process is customizable for your build environment and Azure target environments.</span></span>

<span data-ttu-id="a4d3e-110">Można również użyć programu Visual Studio Team Services, wersji programu TFS, która jest hostowana na platformie Azure, aby łatwiej.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-110">You can also use Visual Studio Team Services, a version of TFS that is hosted in Azure, to do this more easily.</span></span> 

<span data-ttu-id="a4d3e-111">Przed rozpoczęciem należy opublikować aplikacji z programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-111">Before you start, you should publish your application from Visual Studio.</span></span>
<span data-ttu-id="a4d3e-112">Zapewni to, że wszystkie zasoby są dostępne i została zainicjowana przy próbie zautomatyzować proces publikacji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-112">This will ensure that all the resources are available and initialized when you attempt to automate the publication process.</span></span>

## <a name="1-configure-the-build-server"></a><span data-ttu-id="a4d3e-113">1: Konfigurowanie serwera kompilacji</span><span class="sxs-lookup"><span data-stu-id="a4d3e-113">1: Configure the Build Server</span></span>
<span data-ttu-id="a4d3e-114">Przed utworzeniem pakietu Azure przy użyciu programu MSBuild, należy zainstalować wymaganego oprogramowania i narzędzi na serwerze kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-114">Before you can create an Azure package by using MSBuild, you must install the required software and tools on the build server.</span></span>

<span data-ttu-id="a4d3e-115">Program Visual Studio nie jest wymagane do zainstalowania na serwerze kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-115">Visual Studio is not required to be installed on the build server.</span></span> <span data-ttu-id="a4d3e-116">Jeśli chcesz użyć do zarządzania serwerem kompilacji usługi kompilacji programu Team Foundation, postępuj zgodnie z instrukcjami [usługi kompilacji programu Team Foundation] [ Team Foundation Build Service] dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-116">If you want to use Team Foundation Build Service to manage your build server, follow the instructions in the [Team Foundation Build Service][Team Foundation Build Service] documentation.</span></span>

1. <span data-ttu-id="a4d3e-117">Zainstalować na serwerze kompilacji [.NET Framework 4.5.2][.NET Framework 4.5.2], która obejmuje MSBuild.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-117">On the build server, install the [.NET Framework 4.5.2][.NET Framework 4.5.2], which includes MSBuild.</span></span>
2. <span data-ttu-id="a4d3e-118">Zainstaluj najnowszą [Azure Authoring Tools dla programu .NET](https://azure.microsoft.com/develop/net/).</span><span class="sxs-lookup"><span data-stu-id="a4d3e-118">Install the latest [Azure Authoring Tools for .NET](https://azure.microsoft.com/develop/net/).</span></span>
3. <span data-ttu-id="a4d3e-119">Zainstaluj [bibliotek platformy Azure dla platformy .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span><span class="sxs-lookup"><span data-stu-id="a4d3e-119">Install the [Azure Libraries for .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span></span>
4. <span data-ttu-id="a4d3e-120">Skopiuj plik Microsoft.WebApplication.targets z instalacją programu Visual Studio do serwera kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-120">Copy the Microsoft.WebApplication.targets file from a Visual Studio installation to the build server.</span></span>

   <span data-ttu-id="a4d3e-121">Na komputerze z programem Visual Studio zainstalowany, ten plik znajduje się w katalogu C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\14.0\\WebApplications.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-121">On a computer with Visual Studio installed, this file is located in the directory C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span></span> <span data-ttu-id="a4d3e-122">Skopiuj go do tego samego katalogu na serwerze kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-122">You should copy it to the same directory on the build server.</span></span>
5. <span data-ttu-id="a4d3e-123">Zainstaluj [Azure Tools dla Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4d3e-123">Install the [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span></span>

## <a name="2-build-a-package-using-msbuild-commands"></a><span data-ttu-id="a4d3e-124">2: Tworzenie pakietu przy użyciu polecenia programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="a4d3e-124">2: Build a Package using MSBuild Commands</span></span>
<span data-ttu-id="a4d3e-125">Ta sekcja opisuje sposób tworzenia polecenie MSBuild, która tworzy pakiet Azure.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-125">This section describes how to construct an MSBuild command that builds an Azure package.</span></span> <span data-ttu-id="a4d3e-126">Wykonaj ten krok, na serwerze kompilacji, aby sprawdzić, czy wszystko jest poprawnie skonfigurowany i czy wykonywanie polecenia programu MSBuild, co ma wykonania.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-126">Run this step on the build server to verify that everything is configured correctly and that the MSBuild command does what you want it to do.</span></span> <span data-ttu-id="a4d3e-127">Można dodać ten wiersz polecenia do istniejących skryptów kompilacji na serwerze kompilacji lub użyć wiersza polecenia w definicji kompilacji TFS, zgodnie z opisem w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-127">You can either add this command line to existing build scripts on the build server, or you can use the command line in a TFS Build Definition, as described in the next section.</span></span> <span data-ttu-id="a4d3e-128">Aby uzyskać więcej informacji na temat parametrów wiersza polecenia i MSBuild, zobacz [informacje w wierszu polecenia programu MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4d3e-128">For more information about command-line parameters and MSBuild, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>

1. <span data-ttu-id="a4d3e-129">Jeśli program Visual Studio jest zainstalowany na serwerze kompilacji, Znajdź i wybierz **wiersz polecenia programu Visual Studio** w **programu Visual Studio Tools** folderu systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-129">If Visual Studio is installed on the build server, locate and choose **Visual Studio Command Prompt** in the **Visual Studio Tools** folder in Windows.</span></span>

   <span data-ttu-id="a4d3e-130">Jeśli program Visual Studio nie jest zainstalowany na serwerze kompilacji, otwórz wiersz polecenia i upewnij się, że MSBuild.exe jest dostępny w ścieżce.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-130">If Visual Studio is not installed on the build server, open a command prompt and make sure that MSBuild.exe is accessible on the path.</span></span> <span data-ttu-id="a4d3e-131">Platformy .NET Framework w ścieżce % WINDIR % jest zainstalowany program MSBuild\\Microsoft.NET\\Framework\\*wersji*.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-131">MSBuild is installed with the .NET Framework in the path %WINDIR%\\Microsoft.NET\\Framework\\*Version*.</span></span> <span data-ttu-id="a4d3e-132">Na przykład aby dodać MSBuild.exe do zmiennej środowiskowej PATH, jeśli masz zainstalowany program .NET Framework 4, wpisz następujące polecenie w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="a4d3e-132">For example, to add MSBuild.exe to the PATH environment variable when you have .NET Framework 4 installed, type the following command at the command prompt:</span></span>

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. <span data-ttu-id="a4d3e-133">W wierszu polecenia przejdź do folderu zawierającego plik projektu platformy Azure, który chcesz utworzyć.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-133">At the command prompt, navigate to the folder containing the Azure project file that you want to build.</span></span>
3. <span data-ttu-id="a4d3e-134">Uruchom program MSBuild z opcji/target: publikowanie opcja jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="a4d3e-134">Run MSBuild with the /target:Publish option as in the following example:</span></span>

       MSBuild /target:Publish

   <span data-ttu-id="a4d3e-135">Tej opcji można stosować skrót /t: publikowania.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-135">This option can be abbreviated as /t:Publish.</span></span> <span data-ttu-id="a4d3e-136">Opcja /t:Publish w programie MSBuild nie należy mylić z polecenia Opublikuj dostępne w programie Visual Studio, jeśli masz zainstalowany zestaw SDK usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-136">The /t:Publish option in MSBuild should not be confused with the Publish commands available in Visual Studio when you have the Azure SDK installed.</span></span> <span data-ttu-id="a4d3e-137">/T: publikowanie tylko kompilacje opcji Azure pakietów.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-137">The /t:Publish option only builds the Azure packages.</span></span> <span data-ttu-id="a4d3e-138">Nie wdrażać pakiety jak polecenia Opublikuj w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-138">It does not deploy the packages as the Publish commands in Visual Studio do.</span></span>

   <span data-ttu-id="a4d3e-139">Opcjonalnie można określić nazwę projektu jako parametr MSBuild.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-139">Optionally, you can specify the project name as an MSBuild parameter.</span></span> <span data-ttu-id="a4d3e-140">Jeśli nie zostanie określony, używany jest bieżący katalog.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-140">If not specified, the current directory is used.</span></span> <span data-ttu-id="a4d3e-141">Aby uzyskać więcej informacji na temat opcji wiersza polecenia programu MSBuild, zobacz [informacje w wierszu polecenia programu MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4d3e-141">For more information about MSBuild command line options, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>
4. <span data-ttu-id="a4d3e-142">Znajdź dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-142">Locate the output.</span></span> <span data-ttu-id="a4d3e-143">Domyślnie to polecenie tworzy katalog w odniesieniu do folderu głównego dla projektu, takie jak *ProjectDir*\\bin\\*konfiguracji*\\app.publish \\.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-143">By default, this command creates a directory in relation to the root folder for the project, such as *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span></span> <span data-ttu-id="a4d3e-144">Podczas tworzenia projektu platformy Azure, generowanie dwóch plików, sam plik pakietu i towarzyszący plik konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="a4d3e-144">When you build an Azure project, you generate two files, the package file itself and the accompanying configuration file:</span></span>

   * <span data-ttu-id="a4d3e-145">Project.cspkg</span><span class="sxs-lookup"><span data-stu-id="a4d3e-145">Project.cspkg</span></span>
   * <span data-ttu-id="a4d3e-146">Element ServiceConfiguration. *TargetProfile*.cscfg</span><span class="sxs-lookup"><span data-stu-id="a4d3e-146">ServiceConfiguration.*TargetProfile*.cscfg</span></span>

   <span data-ttu-id="a4d3e-147">Domyślnie każdy projekt Azure zawiera jeden usługi konfiguracji pliku (cscfg) lokalne kompilacje (debugowanie) i drugi dla kompilacji chmury (tymczasowym czy produkcyjnym), ale można dodać lub usunąć pliki konfiguracji usługi, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-147">By default, each Azure project includes one service configuration file (.cscfg file) for local (debugging) builds and another for cloud (staging or production) builds, but you can add or remove service configuration files as needed.</span></span> <span data-ttu-id="a4d3e-148">Podczas tworzenia pakietu w programie Visual Studio, użytkownik zostanie poproszony które pliku konfiguracji usługi, aby uwzględnić obok pakietu.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-148">When you build a package within Visual Studio, you will be asked which service configuration file to include alongside the package.</span></span>
5. <span data-ttu-id="a4d3e-149">Określ plik konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-149">Specify the service configuration file.</span></span> <span data-ttu-id="a4d3e-150">Podczas tworzenia pakietu przy użyciu programu MSBuild, domyślnie znajduje się plik konfiguracji Usługa lokalna.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-150">When you build a package by using MSBuild, the local service configuration file is included by default.</span></span> <span data-ttu-id="a4d3e-151">Aby dołączyć plik konfiguracji innej usługi, należy ustawić właściwość TargetProfile polecenia programu MSBuild, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="a4d3e-151">To include a different service configuration file, set the TargetProfile property of the MSBuild command, as in the following example:</span></span>

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. <span data-ttu-id="a4d3e-152">Określ lokalizację dla danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-152">Specify the location for the output.</span></span> <span data-ttu-id="a4d3e-153">Ustawianie ścieżki przy użyciu /p:PublishDir =*katalogu* \\ opcji, w tym końcowe separatora ukośnik odwrotny, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="a4d3e-153">Set the path by using the /p:PublishDir=*Directory*\\ option, including the trailing backslash separator, as in the following example:</span></span>

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   <span data-ttu-id="a4d3e-154">Po utworzone i przetestowane odpowiedni wiersz polecenia programu MSBuild do tworzenia projektów i połączyć je w pakiecie Azure, można dodać ten wiersz polecenia do skrypty kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-154">Once you've constructed and tested an appropriate MSBuild command line to build your projects and combine them into an Azure package, you can add this command line to your build scripts.</span></span> <span data-ttu-id="a4d3e-155">Jeśli serwer kompilacji obsługuje skrypty niestandardowe, ten proces będzie zależeć od specyfiki procesu kompilacji niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-155">If your build server uses custom scripts, this process will depend on the specifics of your custom build process.</span></span> <span data-ttu-id="a4d3e-156">Jeśli używasz TFS jako środowiska kompilacji, można postępuj zgodnie z instrukcjami w następnym kroku, aby dodać pakiet Azure kompilacji do procesu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-156">If you are using TFS as a build environment, then you can follow the instructions in the next step to add the Azure package build to your build process.</span></span>

## <a name="3-build-a-package-using-tfs-team-build"></a><span data-ttu-id="a4d3e-157">3: Tworzenie pakietu za pomocą kompilacji TFS zespołu</span><span class="sxs-lookup"><span data-stu-id="a4d3e-157">3: Build a Package using TFS Team Build</span></span>
<span data-ttu-id="a4d3e-158">Jeśli masz skonfigurowany jako kontroler kompilacji i serwer kompilacji Team Foundation Server (TFS), skonfigurować jako maszyna kompilacji TFS, a następnie możesz opcjonalnie skonfigurować automatyczne kompilacji pakietu Azure.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-158">If you have Team Foundation Server (TFS) set up as a build controller and the build server set up as a TFS build machine, then you can optionally set up an automated build for your Azure package.</span></span> <span data-ttu-id="a4d3e-159">Aby uzyskać informacje na temat sposobu konfigurowania i używania jako system kompilacji Team Foundation server, zobacz [skalowania w poziomie system kompilacji][Scale out your build system].</span><span class="sxs-lookup"><span data-stu-id="a4d3e-159">For information on how to set up and use Team Foundation server as a build system, see [Scale out your build system][Scale out your build system].</span></span> <span data-ttu-id="a4d3e-160">W szczególności w poniższej procedurze przyjęto, że na serwerze kompilacji zostało skonfigurowane zgodnie z opisem w [Wdróż i skonfiguruj serwer kompilacji][Deploy and configure a build server], i utworzyć projektu zespołowego, należy utworzyć chmury projekt usługi w projekcie zespołowym.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-160">In particular, the following procedure assumes that you have configured your build server as described in [Deploy and configure a build server][Deploy and configure a build server], and that you have created a team project, created a cloud service project in the team project.</span></span>

<span data-ttu-id="a4d3e-161">Aby skonfigurować TFS do tworzenia pakietów platformy Azure, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a4d3e-161">To configure TFS to build Azure packages, perform the following steps:</span></span>

1. <span data-ttu-id="a4d3e-162">W programie Visual Studio na komputerze deweloperskim, w menu Widok wybierz polecenie **Team Explorer**, lub wybierz polecenie Ctrl +\\, Ctrl + M.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-162">In Visual Studio on your development computer, on the View menu, choose **Team Explorer**, or choose Ctrl+\\, Ctrl+M.</span></span> <span data-ttu-id="a4d3e-163">W oknie programu Team Explorer rozwiń **kompilacje** węzła lub wybierz **kompilacje** stronie, a następnie wybierz **nową definicję kompilacji**.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-163">In the Team Explorer window, expand the **Builds** node or choose the **Builds** page, and choose **New Build Definition**.</span></span>

   ![Nowa opcja definicji kompilacji][0]
2. <span data-ttu-id="a4d3e-165">Wybierz **wyzwalacza** , a następnie określić żądaną warunki, gdy chcesz pakietu, który ma zostać utworzony.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-165">Choose the **Trigger** tab, and specify the desired conditions for when you want the package to be built.</span></span> <span data-ttu-id="a4d3e-166">Na przykład określić **ciągłej integracji** do utworzenia pakietu przy każdym kontroli źródła zaewidencjonowania występuje.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-166">For example, specify **Continuous Integration** to build the package whenever a source control check-in occurs.</span></span>
3. <span data-ttu-id="a4d3e-167">Wybierz **ustawienia źródła** karcie i upewnij się, że folder projektu jest wymieniony w **folderu kontroli źródła** kolumny, a stan ma **Active**.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-167">Choose the **Source Settings** tab, and make sure your project folder is listed in the **Source Control Folder** column, and the status is **Active**.</span></span>
4. <span data-ttu-id="a4d3e-168">Wybierz **kompilacji domyślne** , a następnie w obszarze kontroler kompilacji, sprawdź nazwę serwera kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-168">Choose the **Build Defaults** tab, and under Build controller, verify the name of the build server.</span></span>  <span data-ttu-id="a4d3e-169">Ponadto wybierz opcję **Kopiuj dane wyjściowe kompilacji do następującego folderu docelowego** i określ lokalizację docelową żądany.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-169">Also, choose the option **Copy build output to the following drop folder** and specify the desired drop location.</span></span>
5. <span data-ttu-id="a4d3e-170">Wybierz **procesu** kartę. Na karcie procesu wybierz szablon domyślny, w obszarze **kompilacji**, wybierz projekt, jeśli nie została jeszcze wybrana, a rozwiń **zaawansowane** sekcji **kompilacji** sekcji siatki.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-170">Choose the **Process** tab. On the Process tab, choose the default template, under **Build**, choose the project if it is not already selected, and expand the **Advanced** section in the **Build** section of the grid.</span></span>
6. <span data-ttu-id="a4d3e-171">Wybierz **argumenty programu MSBuild**i ustaw odpowiednie argumenty wiersza polecenia programu MSBuild, zgodnie z opisem w kroku 2. powyżej.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-171">Choose **MSBuild Arguments**, and set the appropriate MSBuild command line arguments as described in Step 2 above.</span></span> <span data-ttu-id="a4d3e-172">Na przykład wprowadź **/t: publikowanie /p:PublishDir =\\\\MójSerwer\\porzuca\\**  do tworzenia pakietu i skopiuj pliki pakietu do lokalizacji \\ \\ MójSerwer\\porzuca\\:</span><span class="sxs-lookup"><span data-stu-id="a4d3e-172">For example, enter **/t:Publish /p:PublishDir=\\\\myserver\\drops\\** to build a package and copy the package files to the location \\\\myserver\\drops\\:</span></span>

   ![Argumenty programu MSBuild][2]

   > [!NOTE]
   > <span data-ttu-id="a4d3e-174">Kopiowanie plików do udziału publicznego ułatwia ręcznie wdrażania pakietów na komputerze projektowym.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-174">Copying the files to a public share makes it easier to manually deploy the packages from your development computer.</span></span>
7. <span data-ttu-id="a4d3e-175">Testowanie Powodzenie z kroku kompilacji sprawdzając w przypadku zmiany do projektu lub kolejki nowej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-175">Test the success of your build step by checking in a change to your project, or queue up a new build.</span></span> <span data-ttu-id="a4d3e-176">Do kolejki z nowej kompilacji w programie Team Explorer, kliknij prawym przyciskiem myszy **wszystkie definicje kompilacji,** , a następnie wybierz **Tworzenie nowej kolejki**.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-176">To queue up a new build, in the Team Explorer, right-click **All Build Definitions,** and then choose **Queue New Build**.</span></span>

## <a name="4-publish-a-package-using-a-powershell-script"></a><span data-ttu-id="a4d3e-177">4: publikowanie pakietu przy użyciu skryptu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4d3e-177">4: Publish a Package using a PowerShell Script</span></span>
<span data-ttu-id="a4d3e-178">Ta sekcja opisuje sposób tworzenia skryptu programu Windows PowerShell, która będzie publikować dane wyjściowe pakietu aplikacji chmurze na platformie Azure przy użyciu parametrów opcjonalnych.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-178">This section describes how to construct a Windows PowerShell script that will publish the Cloud app package output to Azure using optional parameters.</span></span> <span data-ttu-id="a4d3e-179">Ten skrypt można wywołać po wykonaniu kroku kompilacji w Twojej automatyzacji niestandardowej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-179">This script can be called after the build step in your custom build automation.</span></span> <span data-ttu-id="a4d3e-180">Można również nadać mu z szablonu procesu działania przepływu pracy w Visual Studio TFS Team Build.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-180">It can also be called from Process Template workflow activities in Visual Studio TFS Team Build.</span></span>

1. <span data-ttu-id="a4d3e-181">Zainstaluj [poleceń cmdlet programu Azure PowerShell] [ Azure PowerShell cmdlets] (v0.6.1 lub nowszej).</span><span class="sxs-lookup"><span data-stu-id="a4d3e-181">Install the [Azure PowerShell cmdlets][Azure PowerShell cmdlets] (v0.6.1 or higher).</span></span>
   <span data-ttu-id="a4d3e-182">Podczas fazy instalacji polecenia cmdlet należy wybrać opcję instalacji jako przystawki.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-182">During the cmdlet setup phase, choose to install as a snap-in.</span></span> <span data-ttu-id="a4d3e-183">Należy zwrócić uwagę, czy tego oficjalnie obsługiwana wersja zastępuje starszej wersji oferowane za pośrednictwem portalu CodePlex, chociaż poprzednie wersje zostały numerowane 2.x.x.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-183">Note that this officially supported version replaces the older version offered through CodePlex, although the previous versions were numbered 2.x.x.</span></span>
2. <span data-ttu-id="a4d3e-184">Uruchom program Azure PowerShell przy użyciu Start menu lub strony początkowej.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-184">Start Azure PowerShell using the Start menu or Start page.</span></span> <span data-ttu-id="a4d3e-185">Jeśli uruchamiasz w ten sposób, poleceń cmdlet programu Azure PowerShell zostanie załadowany.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-185">If you start in this way, the Azure PowerShell cmdlets will be loaded.</span></span>
3. <span data-ttu-id="a4d3e-186">W wierszu polecenia programu PowerShell, sprawdź, czy polecenia cmdlet programu PowerShell są załadowane przez wprowadzenie polecenia częściowe `Get-Azure` , a następnie naciśnięcie klawisza Tab do uzupełniania instrukcji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-186">At the PowerShell prompt, verify that the PowerShell cmdlets are loaded by entering the partial command `Get-Azure` and then pressing the Tab key for statement completion.</span></span>

   <span data-ttu-id="a4d3e-187">Po naciśnięciu klawisza Tab wielokrotnie, powinny pojawić różne polecenia programu PowerShell systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-187">If you press the Tab key repeatedly, you should see various Azure PowerShell commands.</span></span>
4. <span data-ttu-id="a4d3e-188">Sprawdź, czy możesz nawiązać subskrypcji platformy Azure, przez zaimportowanie informacji o subskrypcji z pliku .publishsettings.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-188">Verify that you can connect to your Azure subscription by importing your subscription information from the .publishsettings file.</span></span>

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   <span data-ttu-id="a4d3e-189">Następnie wprowadź polecenie</span><span class="sxs-lookup"><span data-stu-id="a4d3e-189">Then enter the command</span></span>

   `Get-AzureSubscription`

   <span data-ttu-id="a4d3e-190">Oznacza to, informacje o Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-190">This shows information about your subscription.</span></span> <span data-ttu-id="a4d3e-191">Sprawdź, czy wszystkie ustawienia są poprawne.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-191">Verify that everything is correct.</span></span>
5. <span data-ttu-id="a4d3e-192">Zapisz szablon skryptu podana na końcu tego artykułu w folderze skryptów jako c:\\skryptów\\WindowsAzure\\**PublishCloudService.ps1**.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-192">Save the script template provided at the end of this article to your scripts folder as c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span></span>
6. <span data-ttu-id="a4d3e-193">Zapoznaj się z sekcją Parametry skryptu.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-193">Review the parameters section of the script.</span></span> <span data-ttu-id="a4d3e-194">Dodaj lub zmodyfikuj wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-194">Add or modify any default values.</span></span> <span data-ttu-id="a4d3e-195">Te wartości zawsze może być zastąpiona przez przekazywanie parametrów jawnych.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-195">These values can always be overridden by passing in explicit parameters.</span></span>
7. <span data-ttu-id="a4d3e-196">Upewnij się, są prawidłową chmurą konta usługi i Magazyn tworzone w ramach subskrypcji, która może być celem skryptu publikowania.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-196">Ensure there are valid cloud service and storage accounts created in your subscription that can be targeted by the publish script.</span></span> <span data-ttu-id="a4d3e-197">Konto magazynu (magazynu obiektów blob) będzie używany do przekazywania i tymczasowe przechowywanie wdrożenia pakietu i pliku konfiguracji podczas tworzenia wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-197">The storage account (blob storage) will be used to upload and temporarily store the deployment package and config file while the deployment is being created.</span></span>

   * <span data-ttu-id="a4d3e-198">Aby utworzyć nową usługę w chmurze, można wywołać tego skryptu lub użyć [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a4d3e-198">To create a new cloud service, you can call this script or use the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a4d3e-199">Nazwa usługi w chmurze będzie służyć jako prefiksu w pełni kwalifikowaną nazwę domeny i dlatego musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-199">The cloud service name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span>

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * <span data-ttu-id="a4d3e-200">Aby utworzyć nowe konto magazynu, można wywołać tego skryptu lub użyć [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a4d3e-200">To create a new storage account, you can call this script or use the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a4d3e-201">Nazwa konta magazynu będzie służyć jako prefiksu w pełni kwalifikowaną nazwę domeny i dlatego musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-201">The storage account name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span> <span data-ttu-id="a4d3e-202">Można spróbować użyć takiej samej nazwie jako usługa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-202">You can try using the same name as the cloud service.</span></span>

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. <span data-ttu-id="a4d3e-203">Wywołanie skryptu bezpośrednio z programu Azure PowerShell lub połączenie się tego skryptu do kompilacji hosta automatyzacji wystąpić po kompilacji pakietu.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-203">Call the script directly from Azure PowerShell, or wire up this script to your host build automation to occur after the package build.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="a4d3e-204">Skrypt będzie zawsze usunąć lub zamienić istniejący wdrożeń domyślnie, jeśli ich wykrycia.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-204">The script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="a4d3e-205">Jest to niezbędne do włączenia ciągłego dostarczania automatyzacji, jeśli to możliwe nie monitowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-205">This is necessary to enable continuous delivery from automation where no user prompting is possible.</span></span>
   >
   >

   <span data-ttu-id="a4d3e-206">**Przykładowy scenariusz 1:** ciągłe wdrażanie w środowisku przemieszczania usługi:</span><span class="sxs-lookup"><span data-stu-id="a4d3e-206">**Example scenario 1:** continuous deployment to the staging environment of a service:</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="a4d3e-207">To jest zazwyczaj następuje testu weryfikacji i wymiany wirtualnych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-207">This is typically followed up by test run verification and a VIP swap.</span></span> <span data-ttu-id="a4d3e-208">Wymiany wirtualnych adresów IP może odbywać się za pośrednictwem [portalu Azure](https://portal.azure.com) lub za pomocą polecenia cmdlet Move-wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-208">The VIP swap can be done via the [Azure portal](https://portal.azure.com) or by using the Move-Deployment cmdlet.</span></span>

   <span data-ttu-id="a4d3e-209">**Przykładowy scenariusz 2:** ciągłego wdrażania do środowiska produkcyjnego usługi dedykowanych testu</span><span class="sxs-lookup"><span data-stu-id="a4d3e-209">**Example scenario 2:** continuous deployment to the production environment of a dedicated test service</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="a4d3e-210">**Pulpit zdalny:**</span><span class="sxs-lookup"><span data-stu-id="a4d3e-210">**Remote Desktop:**</span></span>

   <span data-ttu-id="a4d3e-211">Włączenie pulpitu zdalnego w projekcie platformy Azure, konieczne będzie wykonanie dodatkowych kroków jednorazowe, aby upewnić się, że przekazano poprawny certyfikat usługi chmury do wszystkich usług w chmurze celem tego skryptu.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-211">If Remote Desktop is enabled in your Azure project you will need to perform additional one-time steps to ensure the correct Cloud Service Certificate is uploaded to all cloud services targeted by this script.</span></span>

   <span data-ttu-id="a4d3e-212">Znajdź wartości odcisku palca certyfikatu oczekiwany przez poszczególnych ról.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-212">Locate the certificate thumbprint values expected by your roles.</span></span> <span data-ttu-id="a4d3e-213">Wartości odcisku palca są widoczne w sekcji certyfikaty w pliku konfiguracji chmury (tj. ServiceConfiguration.Cloud.cscfg).</span><span class="sxs-lookup"><span data-stu-id="a4d3e-213">The thumbprint values are visible in the Certificates section of the cloud config file (i.e. ServiceConfiguration.Cloud.cscfg).</span></span> <span data-ttu-id="a4d3e-214">Istnieje również wyświetlane w oknie dialogowym Konfiguracja usług pulpitu zdalnego w programie Visual Studio po wyświetleniu opcji i wyświetlanie wybranego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-214">It is also visible in the Remote Desktop Configuration dialog in Visual Studio when you Show Options and view the selected certificate.</span></span>

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   <span data-ttu-id="a4d3e-215">Przekaż certyfikaty pulpitu zdalnego krokiem jednorazowej konfiguracji za pomocą następującego skryptu apletu polecenia:</span><span class="sxs-lookup"><span data-stu-id="a4d3e-215">Upload Remote Desktop certificates as a one-time setup step using the following cmdlet script:</span></span>

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   <span data-ttu-id="a4d3e-216">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="a4d3e-216">For example:</span></span>

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   <span data-ttu-id="a4d3e-217">Możesz też wyeksportować plik PFX certyfikatu z kluczem prywatnym i przekaż certyfikaty do każdej docelowej chmury usługi za pomocą [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a4d3e-217">Alternatively you can export the certificate file PFX with private key and upload certificates to each target cloud service using the [Azure portal](https://portal.azure.com).</span></span>

   <!---
   Fixing broken links for Azure content migration from ACOM to DOCS. I'm unable to find a replacement links, so I'm commenting out this reference for now. The author can investigate in the future. "Read the following article to learn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   <span data-ttu-id="a4d3e-218">**Uaktualnienie a wdrożenia. Usunięcie wdrożenia —\> nowego wdrożenia**</span><span class="sxs-lookup"><span data-stu-id="a4d3e-218">**Upgrade Deployment vs. Delete Deployment -\> New Deployment**</span></span>

   <span data-ttu-id="a4d3e-219">Skrypt będzie domyślnie wykonywać uaktualniania wdrożenia ($enableDeploymentUpgrade = 1) gdy brak parametru jest przekazano lub nie została jawnie przekazana wartość 1.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-219">The script will by default perform an Upgrade Deployment ($enableDeploymentUpgrade = 1) when no parameter is passed in or the value 1 is passed explicitly.</span></span> <span data-ttu-id="a4d3e-220">Dla pojedynczego wystąpienia to zaletą jest mniej czasu niż pełne wdrożenie.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-220">For single instances this has the advantage of taking less time than a full deployment.</span></span> <span data-ttu-id="a4d3e-221">Dla wystąpień, które wymagają wysokiej dostępności to również zaletą jest pozostawienie niektórych wystąpień uruchomiona, podczas gdy inne uaktualnienia (przejście domenę aktualizacji), a także Twojego adresu VIP, nie zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-221">For instances that require high availability this also has the advantage of leaving some instances running while others are upgraded (walking your update domain), plus your VIP will not be deleted.</span></span>

   <span data-ttu-id="a4d3e-222">Wdrożenia uaktualnienia można wyłączyć w skrypcie ($enableDeploymentUpgrade = 0) lub przez przekazanie *- enableDeploymentUpgrade 0* jako parametru, która zmienia zachowanie skryptu, najpierw usuń wszystkie istniejące wdrożenia, a następnie utworzyć nowy wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-222">Upgrade Deployment can be disabled in the script ($enableDeploymentUpgrade = 0) or by passing *-enableDeploymentUpgrade 0* as a parameter, which alters the script behavior to first delete any existing deployment and then create a new deployment.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="a4d3e-223">Skrypt będzie zawsze usunąć lub zamienić istniejący wdrożeń domyślnie, jeśli ich wykrycia.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-223">The script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="a4d3e-224">Jest to niezbędne do włączenia ciągłego dostarczania automatyzacji, jeśli to możliwe nie monitowania użytkownika / — operator.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-224">This is necessary to enable continuous delivery from automation where no user/operator prompting is possible.</span></span>
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a><span data-ttu-id="a4d3e-225">5: publikowanie pakietu za pomocą kompilacji TFS zespołu</span><span class="sxs-lookup"><span data-stu-id="a4d3e-225">5: Publish a Package using TFS Team Build</span></span>
<span data-ttu-id="a4d3e-226">Ten opcjonalny krok łączy TFS Team Build do skryptu utworzonego w kroku 4, która obsługuje publikowanie kompilacji pakietu Azure.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-226">This optional step connects TFS Team Build to the script created in step 4, which handles publishing of the package build to Azure.</span></span> <span data-ttu-id="a4d3e-227">Dzięki temu modyfikowania szablonu procesu, używany przez definicję kompilacji, wykonywania działań publikowania na końcu przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-227">This entails modifying the Process Template used by your build definition so that it runs a Publish activity at the end of the workflow.</span></span> <span data-ttu-id="a4d3e-228">Działanie publikowania zostanie wykonane polecenie programu PowerShell przekazywanie parametrów z kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-228">The Publish activity will execute your PowerShell command passing in parameters from the build.</span></span> <span data-ttu-id="a4d3e-229">Dane wyjściowe programu MSBuild elementów docelowych i opublikować skrypt będzie przekazywany w potoku do wyjścia standardowego kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-229">Output of the MSBuild targets and publish script will be piped into the standard build output.</span></span>

1. <span data-ttu-id="a4d3e-230">Edytowanie definicji kompilacji odpowiedzialny za ciągłego wdrażania.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-230">Edit the Build Definition responsible for continuous deploy.</span></span>
2. <span data-ttu-id="a4d3e-231">Wybierz **procesu** kartę.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-231">Select the **Process** tab.</span></span>
3. <span data-ttu-id="a4d3e-232">Postępuj zgodnie z [tych instrukcji](http://msdn.microsoft.com/library/dd647551.aspx) można dodać projektu działania dla szablonu procesu kompilacji, Pobierz domyślny szablon, dodaj go do projektu i jego zaewidencjonowania.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-232">Follow [these instructions](http://msdn.microsoft.com/library/dd647551.aspx) to add an Activity project for the build process template, download the default template, add it to the project and check it in.</span></span> <span data-ttu-id="a4d3e-233">Nadaj nazwę nowej, takich jak AzureBuildProcessTemplate szablonu procesu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-233">Give the build process template a new name, such as AzureBuildProcessTemplate.</span></span>
4. <span data-ttu-id="a4d3e-234">Wróć do **procesu** , a następnie użyć **Pokaż szczegóły** wyświetlić listę szablonów procesu kompilacji dostępne.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-234">Return to the **Process** tab, and use **Show Details** to show a list of available build process templates.</span></span> <span data-ttu-id="a4d3e-235">Wybierz **nowych...**  przycisk, a następnie przejdź do projektu po prostu dodane i zaewidencjonowane.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-235">Choose the **New...** button, and navigate to the project you just added and checked in.</span></span> <span data-ttu-id="a4d3e-236">Znajdź szablon, który został utworzony i wybierz polecenie **OK**.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-236">Locate the template you just created and choose **OK**.</span></span>
5. <span data-ttu-id="a4d3e-237">Otwórz wybrany szablon procesu do edycji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-237">Open the selected Process Template for editing.</span></span> <span data-ttu-id="a4d3e-238">Możesz otworzyć bezpośrednio w Projektancie przepływów pracy lub w edytorze XML, aby pracować z XAML.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-238">You can open directly in the Workflow designer or in the XML editor to work with the XAML.</span></span>
6. <span data-ttu-id="a4d3e-239">Dodaj poniższą listę nowych argumentów jako oddzielne pozycje w karcie argumenty projektanta przepływów pracy.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-239">Add the following list of new arguments as separate line items in the arguments tab of the workflow designer.</span></span> <span data-ttu-id="a4d3e-240">Wszystkie argumenty powinny posiadać kierunek = w i wpisz = ciąg.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-240">All arguments should have direction=In and type=String.</span></span> <span data-ttu-id="a4d3e-241">Te posłuży do parametry przepływu z definicji kompilacji do przepływu pracy, które następnie Uzyskaj używane do wywoływania skryptu publikowania.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-241">These will be used to flow parameters from the build definition into the workflow, which then get used to call the publish script.</span></span>

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![Lista argumentów][3]

   <span data-ttu-id="a4d3e-243">Odpowiednie XAML wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="a4d3e-243">The corresponding XAML looks like this:</span></span>

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
7. <span data-ttu-id="a4d3e-244">Dodaj nową sekwencję na koniec uruchom na agenta:</span><span class="sxs-lookup"><span data-stu-id="a4d3e-244">Add a new sequence at the end of Run On Agent:</span></span>

   1. <span data-ttu-id="a4d3e-245">Rozpocznij od dodania działanie Jeśli instrukcji, aby sprawdzić prawidłowym plikiem skryptu.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-245">Start by adding an If Statement activity to check for a valid script file.</span></span> <span data-ttu-id="a4d3e-246">Warunek tej wartości:</span><span class="sxs-lookup"><span data-stu-id="a4d3e-246">Set the condition to this value:</span></span>

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. <span data-ttu-id="a4d3e-247">Następnie przypadek Jeśli instrukcji, Dodaj nowe działanie w sekwencji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-247">In the Then case of the If Statement, add a new Sequence activity.</span></span> <span data-ttu-id="a4d3e-248">Ustaw nazwę wyświetlaną na "publish Start"</span><span class="sxs-lookup"><span data-stu-id="a4d3e-248">Set the display name to 'Start publish'</span></span>
   3. <span data-ttu-id="a4d3e-249">Z początkiem publikowania sekwencji nadal wybrane, należy dodać na następującej liście nowe zmienne jako oddzielne pozycje w karcie Zmienne projektanta przepływów pracy.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-249">With the Start publish sequence still selected, add the following list of new variables as separate line items in the variables tab of the workflow designer.</span></span> <span data-ttu-id="a4d3e-250">Wszystkie zmienne powinny mieć typ zmiennej = ciągu i zakres = rozpoczęcie publikowania.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-250">All variables should have Variable type =String and Scope=Start publish.</span></span> <span data-ttu-id="a4d3e-251">Te posłuży do parametry przepływu z definicji kompilacji do przepływu pracy, które następnie Uzyskaj używane do wywoływania skryptu publikowania.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-251">These will be used to flow parameters from the build definition into the workflow, which then get used to call the publish script.</span></span>

      * <span data-ttu-id="a4d3e-252">SubscriptionDataFilePath typu String</span><span class="sxs-lookup"><span data-stu-id="a4d3e-252">SubscriptionDataFilePath, of type String</span></span>
      * <span data-ttu-id="a4d3e-253">PublishScriptFilePath typu String</span><span class="sxs-lookup"><span data-stu-id="a4d3e-253">PublishScriptFilePath, of type String</span></span>

        ![Nowe zmienne][4]
   4. <span data-ttu-id="a4d3e-255">Jeśli używasz programu TFS 2012 lub starszy, Dodaj działanie ConvertWorkspaceItem na początku nowego sekwencji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-255">If you are using TFS 2012 or earlier, add a ConvertWorkspaceItem activity at the beginning of the new Sequence.</span></span> <span data-ttu-id="a4d3e-256">Jeśli używasz programu TFS 2013 lub nowszy, Dodaj działanie GetLocalPath na początku nowego sekwencji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-256">If you are using TFS 2013 or later, add a GetLocalPath activity at the beginning of the new sequence.</span></span> <span data-ttu-id="a4d3e-257">Dla ConvertWorkspaceItem, ustaw właściwości w następujący sposób: kierunek = ServerToLocal, nazwa wyświetlana = 'Convert opublikować nazwę pliku skryptu', dane wejściowe = "PublishScriptLocation", wynik = "PublishScriptFilePath", obszar roboczy = "Obszar roboczy".</span><span class="sxs-lookup"><span data-stu-id="a4d3e-257">For a ConvertWorkspaceItem, set the properties as follows: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="a4d3e-258">Dla działania GetLocalPath ustaw właściwość IncomingPath do "PublishScriptLocation" i "PublishScriptFilePath" wynik.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-258">For a GetLocalPath activity, set the property IncomingPath to 'PublishScriptLocation', and the Result to 'PublishScriptFilePath'.</span></span> <span data-ttu-id="a4d3e-259">To działanie konwertuje ścieżka skryptu publikowania z TFS lokalizacji serwera (jeśli dotyczy) do ścieżki standardowe dysku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-259">This activity converts the path to the publish script from TFS server locations (if applicable) to a standard local disk path.</span></span>
   5. <span data-ttu-id="a4d3e-260">Jeśli używasz programu TFS 2012 lub starszy, należy dodać innego działania ConvertWorkspaceItem na końcu nowej sekwencji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-260">If you are using TFS 2012 or earlier, add another ConvertWorkspaceItem activity at the end of the new Sequence.</span></span> <span data-ttu-id="a4d3e-261">Kierunek = ServerToLocal, nazwa wyświetlana = "Dokonać konwersji subskrypcji nazwa_pliku", dane wejściowe = "SubscriptionDataFileLocation", wynik = "SubscriptionDataFilePath", obszar roboczy = "Obszar roboczy".</span><span class="sxs-lookup"><span data-stu-id="a4d3e-261">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="a4d3e-262">Jeśli używasz programu TFS 2013 lub nowszy, Dodaj inny GetLocalPath.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-262">If you are using TFS 2013 or later, add another GetLocalPath.</span></span> <span data-ttu-id="a4d3e-263">IncomingPath = "SubscriptionDataFileLocation", a wynik = "SubscriptionDataFilePath."</span><span class="sxs-lookup"><span data-stu-id="a4d3e-263">IncomingPath='SubscriptionDataFileLocation', and Result='SubscriptionDataFilePath.'</span></span>
   6. <span data-ttu-id="a4d3e-264">Dodaj działanie InvokeProcess na końcu nowej sekwencji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-264">Add an InvokeProcess activity at the end of the new Sequence.</span></span>
      <span data-ttu-id="a4d3e-265">To działanie wywołuje PowerShell.exe z argumentami przekazany przez definicję kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-265">This activity calls PowerShell.exe with the arguments passed in by the Build Definition.</span></span>

      + <span data-ttu-id="a4d3e-266">Argumenty = String.Format ("-""{0}" "- serviceName {1} - storageAccountName {2} tabelę packageLocation —""{3}" "- cloudConfigLocation""{4}" "- subscriptionDataFile""{5}" "- selectedSubscription {6} pliku-środowiska""{7}" "",  PublishScriptFilePath, ServiceName, StorageAccountName, tabelę PackageLocation, CloudConfigLocation, SubscriptionDataFilePath, Nazwa subskrypcji, środowisko)</span><span class="sxs-lookup"><span data-stu-id="a4d3e-266">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span></span>
      + <span data-ttu-id="a4d3e-267">Nazwa wyświetlana = Execute publikowania skryptu</span><span class="sxs-lookup"><span data-stu-id="a4d3e-267">DisplayName = Execute publish script</span></span>
      + <span data-ttu-id="a4d3e-268">Nazwa pliku = "PowerShell" (m.in. cudzysłowy)</span><span class="sxs-lookup"><span data-stu-id="a4d3e-268">FileName = "PowerShell" (include the quotes)</span></span>
      + <span data-ttu-id="a4d3e-269">OutputEncoding = System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span><span class="sxs-lookup"><span data-stu-id="a4d3e-269">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span></span>
   7. <span data-ttu-id="a4d3e-270">W **Obsługa standardowego wyjścia** sekcji textbox InvokeProcess, ustaw wartość pola tekstowego "dane".</span><span class="sxs-lookup"><span data-stu-id="a4d3e-270">In the **Handle Standard Output** section textbox of the InvokeProcess, set the textbox value to 'data'.</span></span> <span data-ttu-id="a4d3e-271">To jest zmienną do przechowywania dane wyjścia standardowego.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-271">This is a variable to store the standard output data.</span></span>
   8. <span data-ttu-id="a4d3e-272">Dodaj działanie WriteBuildMessage tylko poniżej **Obsługa standardowego wyjścia** sekcji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-272">Add a WriteBuildMessage activity just below the **Handle Standard Output** section.</span></span> <span data-ttu-id="a4d3e-273">Ustaw ważność = "Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High" i komunikatem = "dane".</span><span class="sxs-lookup"><span data-stu-id="a4d3e-273">Set the Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' and the Message='data'.</span></span> <span data-ttu-id="a4d3e-274">Dzięki temu standardowe dane wyjściowe skryptu zostanie zapisana w danych wyjściowych kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-274">This ensures the standard output of the script will get written to the build output.</span></span>
   9. <span data-ttu-id="a4d3e-275">W **obsługi błędów wyjścia** sekcji textbox InvokeProcess, ustaw wartość pola tekstowego "dane".</span><span class="sxs-lookup"><span data-stu-id="a4d3e-275">In the **Handle Error Output** section textbox of the InvokeProcess, set the textbox value to 'data'.</span></span> <span data-ttu-id="a4d3e-276">To jest zmienną do przechowywania danych błędów.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-276">This is a variable to store the standard error data.</span></span>
   10. <span data-ttu-id="a4d3e-277">Dodaj działanie WriteBuildError tylko poniżej **obsługi błędów wyjścia** sekcji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-277">Add a WriteBuildError activity just below the **Handle Error Output** section.</span></span> <span data-ttu-id="a4d3e-278">Ustaw komunikat = "dane".</span><span class="sxs-lookup"><span data-stu-id="a4d3e-278">Set the Message='data'.</span></span> <span data-ttu-id="a4d3e-279">Dzięki temu, że błędy standardowe skryptu zostanie zapisana w danych wyjściowych błędu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-279">This ensures the standard errors of the script will get written to the build error output.</span></span>
   11. <span data-ttu-id="a4d3e-280">Popraw błędy wskazywanym przez niebieski znaczniki wykrzyknika.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-280">Correct any errors, indicated by blue exclamation marks.</span></span> <span data-ttu-id="a4d3e-281">Umieść kursor nad znaczników wykrzyknik, aby uzyskać wskazówki dotyczące błędu.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-281">Hover over the exclamation marks to get a hint about the error.</span></span> <span data-ttu-id="a4d3e-282">Zapisywanie przepływu pracy, aby usunąć błędy.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-282">Save the workflow to clear errors.</span></span>

   <span data-ttu-id="a4d3e-283">Wynik końcowy publikowania działań przepływu pracy będzie wyglądać następująco w Projektancie:</span><span class="sxs-lookup"><span data-stu-id="a4d3e-283">The final result of the publish workflow activities will look like this in the designer:</span></span>

   ![Działania przepływu pracy][5]

   <span data-ttu-id="a4d3e-285">Wynik końcowy publikowania działań przepływu pracy będzie wyglądać następująco w języku XAML:</span><span class="sxs-lookup"><span data-stu-id="a4d3e-285">The final result of the publish workflow activities will look like this in XAML:</span></span>

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
8. <span data-ttu-id="a4d3e-286">Zapisywanie przepływu pracy szablonu procesu kompilacji i zaewidencjonuj tego pliku.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-286">Save the build process template workflow and Check In this file.</span></span>
9. <span data-ttu-id="a4d3e-287">Edytowanie definicji kompilacji (je zamknąć, jeżeli jest już otwarty) i wybierz **nowy** przycisku, jeśli nie ma jeszcze nowego szablonu na liście szablonów procesów.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-287">Edit the build definition (close it if it is already open), and select the **New** button if you do not yet see the new template in the list of Process Templates.</span></span>
10. <span data-ttu-id="a4d3e-288">Ustaw dla parametru wartości właściwości w sekcji różne w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a4d3e-288">Set the parameter property values in the Misc section as follows:</span></span>

    1. <span data-ttu-id="a4d3e-289">CloudConfigLocation = "c:\\porzuca\\app.publish\\ServiceConfiguration.Cloud.cscfg" *ta wartość jest określana na podstawie: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span><span class="sxs-lookup"><span data-stu-id="a4d3e-289">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *This value is derived from: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span></span>
    2. <span data-ttu-id="a4d3e-290">Tabelę PackageLocation = "c:\\porzuca\\app.publish\\ContactManager.Azure.cspkg" *ta wartość jest określana na podstawie: (cspkg)($ProjectName) $PublishDir*</span><span class="sxs-lookup"><span data-stu-id="a4d3e-290">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *This value is derived from: ($PublishDir)($ProjectName).cspkg*</span></span>
    3. <span data-ttu-id="a4d3e-291">PublishScriptLocation = "c:\\skryptów\\WindowsAzure\\PublishCloudService.ps1"</span><span class="sxs-lookup"><span data-stu-id="a4d3e-291">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span></span>
    4. <span data-ttu-id="a4d3e-292">ServiceName = "mycloudservicename" *nazwa usługi w chmurze odpowiednie w tym miejscu użyć*</span><span class="sxs-lookup"><span data-stu-id="a4d3e-292">ServiceName = 'mycloudservicename' *Use the appropriate cloud service name here*</span></span>
    5. <span data-ttu-id="a4d3e-293">Środowisko = "Tymczasowe"</span><span class="sxs-lookup"><span data-stu-id="a4d3e-293">Environment = 'Staging'</span></span>
    6. <span data-ttu-id="a4d3e-294">StorageAccountName = "mystorageaccountname" *Użyj nazwy konta magazynu odpowiednie tutaj*</span><span class="sxs-lookup"><span data-stu-id="a4d3e-294">StorageAccountName = 'mystorageaccountname' *Use the appropriate storage account name here*</span></span>
    7. <span data-ttu-id="a4d3e-295">SubscriptionDataFileLocation = "c:\\skryptów\\WindowsAzure\\Subscription.xml"</span><span class="sxs-lookup"><span data-stu-id="a4d3e-295">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span></span>
    8. <span data-ttu-id="a4d3e-296">Nazwa subskrypcji = "default"</span><span class="sxs-lookup"><span data-stu-id="a4d3e-296">SubscriptionName = 'default'</span></span>

    ![Wartości właściwości parametru][6]
11. <span data-ttu-id="a4d3e-298">Zapisz zmiany w definicji kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-298">Save the changes to the Build Definition.</span></span>
12. <span data-ttu-id="a4d3e-299">Kolejka kompilacji do wykonywania kompilacji pakietu i publikowania.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-299">Queue a Build to execute both the package build and publish.</span></span> <span data-ttu-id="a4d3e-300">Jeśli masz ustawioną ciągłej integracji wyzwalacz wykona to zachowanie na każdym zaewidencjonowania.</span><span class="sxs-lookup"><span data-stu-id="a4d3e-300">If you have a trigger set to Continuous Integration, you will execute this behavior on every check-in.</span></span>

### <a name="publishcloudserviceps1-script-template"></a><span data-ttu-id="a4d3e-301">PublishCloudService.ps1 skrypt szablonu</span><span class="sxs-lookup"><span data-stu-id="a4d3e-301">PublishCloudService.ps1 script template</span></span>
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy to $servicename",
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
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according to $alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
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

#main driver - publish & write progress to activity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a><span data-ttu-id="a4d3e-302">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a4d3e-302">Next steps</span></span>
<span data-ttu-id="a4d3e-303">Aby włączyć debugowanie zdalne, korzystając z ciągłego dostarczania, zobacz [Włączanie debugowania zdalnego, gdy publikowanie na platformie Azure przy użyciu ciągłego dostarczania](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span><span class="sxs-lookup"><span data-stu-id="a4d3e-303">To enable remote debugging when using continuous delivery, see [Enable remote debugging when using continuous delivery to publish to Azure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span></span>

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[the .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
