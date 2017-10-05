---
title: "Ciągłego dostarczania dla chmury usług za pomocą programu Visual Studio Online | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować ciągłego dostarczania dla aplikacji w chmurze Azure bez zapisania klucza magazynu diagnostyki w plikach konfiguracji usługi"
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 148b2959-c5db-4e4a-a7e9-fccb252e7e8a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: 7e70f92d4d1333ca6cbac5876e5ccbc763bd915c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-to-azure-using-visual-studio-online"></a><span data-ttu-id="14446-103">Securely Zapisz usług diagnostyki klucz magazynu w chmurze i Instalator ciągłą integrację i wdrażanie na platformie Azure przy użyciu programu Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="14446-103">Securely Save Cloud Services Diagnostics Storage Key and Setup Continuous Integration and Deployment to Azure using Visual Studio Online</span></span>
 <span data-ttu-id="14446-104">Jest typowym rozwiązaniem do otwierania projektów źródła dzisiaj.</span><span class="sxs-lookup"><span data-stu-id="14446-104">It is a common practice to open source projects nowadays.</span></span> <span data-ttu-id="14446-105">Zapisywanie w plikach konfiguracji hasła aplikacji nie jest już bezpieczne praktyki jako luk w zabezpieczeniach są widoczne z kluczy tajnych wycieku z kontrolki źródła publicznego.</span><span class="sxs-lookup"><span data-stu-id="14446-105">Saving application secrets in configuration files is no longer safe practice as security vulnerabilities are exposed from secrets being leaked from public source controls.</span></span> <span data-ttu-id="14446-106">Przechowywanie klucza tajnego jako zwykłego tekstu w pliku w potoku ciągłej integracji nie są chronione albo ponieważ serwery kompilacji może być udostępnionych zasobów w środowisku chmury.</span><span class="sxs-lookup"><span data-stu-id="14446-106">Storing secret as plaintext in a file in a Continuous Integration pipeline is not secure either since build servers could be shared resources on the Cloud environment.</span></span> <span data-ttu-id="14446-107">W tym artykule opisano, jak Visual Studio i Visual Studio Online zmniejsza kwestie zabezpieczeń podczas projektowania i proces ciągłej integracji.</span><span class="sxs-lookup"><span data-stu-id="14446-107">This article explains how Visual Studio and Visual Studio Online mitigates the security concerns during development and Continuous Integration process.</span></span>

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a><span data-ttu-id="14446-108">Usuń hasło klucza magazynu diagnostyki w pliku konfiguracji projektu</span><span class="sxs-lookup"><span data-stu-id="14446-108">Remove Diagnostics Storage Key Secret in Project Configuration File</span></span>
<span data-ttu-id="14446-109">Rozszerzenie Diagnostyka usług w chmurze wymaga magazynu Azure do zapisywania wyników diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="14446-109">Cloud Services diagnostics extension requires Azure storage for saving diagnostics results.</span></span> <span data-ttu-id="14446-110">Wcześniej parametry połączenia magazynu jest określona w plikach konfiguracji (cscfg) usługi w chmurze i może zostać zaewidencjonowane do kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="14446-110">Formerly the storage connection string is specified in the Cloud Services configuration (.cscfg) files and could be checked in to source control.</span></span> <span data-ttu-id="14446-111">W najnowszej wersji zestawu Azure SDK możemy zmienić zachowanie, które będzie przechowywać parametry połączenia z częściowa tylko przy użyciu klucza zastępuje token.</span><span class="sxs-lookup"><span data-stu-id="14446-111">In the latest Azure SDK release we changed the behavior to only store a partial connection string with the key replaced by a token.</span></span> <span data-ttu-id="14446-112">W poniższych krokach opisano, jak działa nowych narzędzi usługi w chmurze:</span><span class="sxs-lookup"><span data-stu-id="14446-112">The following steps describe how the new Cloud Services tooling works:</span></span>

### <a name="1-open-the-role-designer"></a><span data-ttu-id="14446-113">1. Otwórz projektanta roli</span><span class="sxs-lookup"><span data-stu-id="14446-113">1. Open the Role designer</span></span>
* <span data-ttu-id="14446-114">Kliknij dwukrotnie lub kliknij prawym przyciskiem myszy rolę usługi w chmurze, aby otworzyć projektanta roli</span><span class="sxs-lookup"><span data-stu-id="14446-114">Double click or right click on a Cloud Services role to open Role designer</span></span>

![Otwórz rolę projektanta][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a><span data-ttu-id="14446-116">2. W sekcji Diagnostyka nowe pole wyboru "nie usuwaj magazynu klucz tajny z projektu" zostanie dodany.</span><span class="sxs-lookup"><span data-stu-id="14446-116">2. Under diagnostics section, a new check box “Don’t remove storage key secret from project” is added</span></span>
* <span data-ttu-id="14446-117">Jeśli używasz emulatora magazynu lokalnego, to pole wyboru jest wyłączone, ponieważ nie istnieje żadne klucz tajny, aby zarządzać ciągu połączenia lokalnego, który jest UseDevelopmentStorage = true.</span><span class="sxs-lookup"><span data-stu-id="14446-117">If you are using the local storage emulator, this checkbox is disabled because there is no secret to manage for the local connection string, which is UseDevelopmentStorage=true.</span></span>

![Parametry połączenia emulatora magazynu lokalnego nie jest tajny][1]

* <span data-ttu-id="14446-119">W przypadku tworzenia nowego projektu, domyślnie to pole wyboru jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="14446-119">If you are creating a new project, by default this checkbox is unchecked.</span></span> <span data-ttu-id="14446-120">Powoduje to sekcji klucza magazynu parametry połączenia magazynu wybranego zastępowane z tokenem.</span><span class="sxs-lookup"><span data-stu-id="14446-120">This results in the storage key section of the selected storage connection string being replaced with a token.</span></span> <span data-ttu-id="14446-121">Wartość tokenu zostaną znalezione w folderze roamingu AppData bieżącego użytkownika, na przykład: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span><span class="sxs-lookup"><span data-stu-id="14446-121">The value of the token will be found under the current user’s AppData Roaming folder, for example: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span></span>

> <span data-ttu-id="14446-122">Należy pamiętać, że user\AppData folder jest kontrolowany dostęp przez logowania użytkownika i jest uznawane za bezpieczne miejsce do przechowywania kluczy tajnych programowanie.</span><span class="sxs-lookup"><span data-stu-id="14446-122">Note that the user\AppData folder is Access Controlled by user sign-in and is considered a secure place to store development secrets.</span></span>
> 
> 

![Klucz magazynu jest zapisywany w folderze profilu użytkownika][2]

### <a name="3-select-a-diagnostics-storage-account"></a><span data-ttu-id="14446-124">3. Wybierz konto magazynu diagnostyki</span><span class="sxs-lookup"><span data-stu-id="14446-124">3. Select a diagnostics storage account</span></span>
* <span data-ttu-id="14446-125">Wybierz konto magazynu, w oknie dialogowym uruchomić, klikając pozycję "..."</span><span class="sxs-lookup"><span data-stu-id="14446-125">Select a storage account from the dialog launched by clicking the “…”</span></span> <span data-ttu-id="14446-126">Dodaj...</span><span class="sxs-lookup"><span data-stu-id="14446-126">button.</span></span> <span data-ttu-id="14446-127">Zwróć uwagę, jak parametry połączenia magazynu, które są generowane nie ma klucz konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="14446-127">Notice how the storage connection string generated will not have the storage account key.</span></span>
* <span data-ttu-id="14446-128">Na przykład: DefaultEndpointsProtocol = https; AccountName = contosostorage; AccountKey = $(*clouddiagstrg.key*)</span><span class="sxs-lookup"><span data-stu-id="14446-128">For example: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span></span>

### <a name="4----debugging-the-project"></a><span data-ttu-id="14446-129">4.    Debugowanie projektu</span><span class="sxs-lookup"><span data-stu-id="14446-129">4.    Debugging the project</span></span>
* <span data-ttu-id="14446-130">F5, aby rozpocząć debugowania w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="14446-130">F5 to start debugging in Visual Studio.</span></span> <span data-ttu-id="14446-131">Wszystko, co powinny działać w taki sam sposób jak przed.</span><span class="sxs-lookup"><span data-stu-id="14446-131">Everything should work in the same way as before.</span></span>
  <span data-ttu-id="14446-132">![Rozpocznij debugowanie lokalnie][3]</span><span class="sxs-lookup"><span data-stu-id="14446-132">![Start debugging locally][3]</span></span>

### <a name="5-publish-project-from-visual-studio"></a><span data-ttu-id="14446-133">5. Opublikować projekt w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="14446-133">5. Publish project from Visual Studio</span></span>
* <span data-ttu-id="14446-134">Uruchom okno dialogowe publikowania i kontynuować logowania instrukcjami, aby opublikować applicaion na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="14446-134">Launch the publish dialog and proceed with sign-in instructions to publish the applicaion to Azure.</span></span>

### <a name="6-additional-information"></a><span data-ttu-id="14446-135">6. Dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="14446-135">6. Additional information</span></span>
> <span data-ttu-id="14446-136">Uwaga: Panel ustawień w Projektancie roli pozostanie, ponieważ jest on teraz.</span><span class="sxs-lookup"><span data-stu-id="14446-136">Note: The Settings panel in the role designer will stay as it is for now.</span></span> <span data-ttu-id="14446-137">Jeśli chcesz korzystać z funkcji zarządzania tajny diagnostyki, przejdź do karty konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="14446-137">If you want to use the secret management feature for diagnostics, go to the Configurations tab.</span></span>
> 
> 

![Dodaj ustawienia][4]

> <span data-ttu-id="14446-139">Uwaga: Włączenie klucza usługi Application Insights zostanie zapisana jako zwykły tekst.</span><span class="sxs-lookup"><span data-stu-id="14446-139">Note: If enabled, the Application Insights key will be stored as plain text.</span></span> <span data-ttu-id="14446-140">Klucz służy tylko do przekazywania zawartości, będzie żadnych poufnych danych na ryzyko naruszenia bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="14446-140">The key is only used for upload contents so no sensitive data will be at risk being compromised.</span></span>
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a><span data-ttu-id="14446-141">Tworzenie i publikowanie projektu usługi w chmurze za pomocą programu Visual Studio online szablonów zadań</span><span class="sxs-lookup"><span data-stu-id="14446-141">Build and Publish a Cloud Services Project using Visual Studio online Task Templates</span></span>
* <span data-ttu-id="14446-142">Poniższe kroki pokazano, jak można skonfigurować ciągłej integracji dla projektu usługi w chmurze za pomocą programu Visual Studio online zadań:</span><span class="sxs-lookup"><span data-stu-id="14446-142">The following steps illustrates how to setup Continuous Integration for Cloud Services project using Visual Studio online tasks:</span></span>
  ### <a name="1----obtain-a-vso-account"></a><span data-ttu-id="14446-143">1.    Uzyskaj konto usługi VSO</span><span class="sxs-lookup"><span data-stu-id="14446-143">1.    Obtain a VSO account</span></span>
* <span data-ttu-id="14446-144">[Utwórz konto Visual Studio Online] [ Create Visual Studio Online account] Jeśli nie masz już</span><span class="sxs-lookup"><span data-stu-id="14446-144">[Create Visual Studio Online account][Create Visual Studio Online account] if you don’t have one already</span></span>
* <span data-ttu-id="14446-145">[Tworzenie projektu zespołowego] [ Create team project] na koncie online programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="14446-145">[Create team project][Create team project] in your Visual Studio online account</span></span>

### <a name="2----setup-source-control-in-visual-studio"></a><span data-ttu-id="14446-146">2.    Ustawienia kontroli wersji w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="14446-146">2.    Setup source control in Visual Studio</span></span>
* <span data-ttu-id="14446-147">Połącz z projektem zespołowym</span><span class="sxs-lookup"><span data-stu-id="14446-147">Connect to a team project</span></span>

![Połącz z projektem zespołowym][5]

![Wybierz projekt zespołowy do nawiązania połączenia][6]

* <span data-ttu-id="14446-150">Dodaj projekt do kontroli źródła</span><span class="sxs-lookup"><span data-stu-id="14446-150">Add your project to source control</span></span>

![Dodaj projekt do kontroli źródła][7]

![Mapowanie projektu do folderu kontroli źródła][8]

* <span data-ttu-id="14446-153">Sprawdź w projekcie z programu Team Explorer</span><span class="sxs-lookup"><span data-stu-id="14446-153">Check in your project from Team Explorer</span></span>

![Sprawdź w projekt do kontroli źródła][9]

### <a name="3----configure-build-process"></a><span data-ttu-id="14446-155">3.    Konfigurowanie procesu kompilacji</span><span class="sxs-lookup"><span data-stu-id="14446-155">3.    Configure Build process</span></span>
* <span data-ttu-id="14446-156">Przejdź do projektu zespołowego i dodać nowe szablony procesu kompilacji</span><span class="sxs-lookup"><span data-stu-id="14446-156">Browse to your team project and add a new build process Templates</span></span>

![Dodawanie nowej kompilacji][10]

* <span data-ttu-id="14446-158">Wybierz kompilację zadań</span><span class="sxs-lookup"><span data-stu-id="14446-158">Select build task</span></span>

![Dodaj zadanie kompilacji][11]

![Wybierz szablon zadania kompilacji programu Visual Studio][12]

* <span data-ttu-id="14446-161">Edytuj dane wejściowe zadania kompilacji.</span><span class="sxs-lookup"><span data-stu-id="14446-161">Edit build task input.</span></span> <span data-ttu-id="14446-162">Należy dostosować parametry kompilacji w zależności od potrzeb</span><span class="sxs-lookup"><span data-stu-id="14446-162">Please customize the build parameters according to your need</span></span>

![Skonfiguruj zadania kompilacji][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* <span data-ttu-id="14446-164">Skonfiguruj zmienne kompilacji</span><span class="sxs-lookup"><span data-stu-id="14446-164">Configure build variables</span></span>

![Skonfiguruj zmienne kompilacji][14]

* <span data-ttu-id="14446-166">Dodaj zadanie, aby przekazać dane wyjściowe kompilacji</span><span class="sxs-lookup"><span data-stu-id="14446-166">Add a task to upload build drop</span></span>

![Wybierz publikowania kompilacji listy zadań][15]

![Skonfiguruj publikowanie kompilacji listy zadań][16]

* <span data-ttu-id="14446-169">Uruchom kompilację</span><span class="sxs-lookup"><span data-stu-id="14446-169">Run the build</span></span>

![Kolejki nowej kompilacji][17]

![Wyświetl podsumowanie kompilacji][18]

* <span data-ttu-id="14446-172">Jeśli kompilacja zakończy się pomyślnie zobaczysz wyniku podobnie jak poniżej</span><span class="sxs-lookup"><span data-stu-id="14446-172">if the build is successful you will see a result similar to below</span></span>

![Wynik kompilacji][19]

### <a name="4----configure-release-process"></a><span data-ttu-id="14446-174">4.    Konfigurowanie procesu publikacji</span><span class="sxs-lookup"><span data-stu-id="14446-174">4.    Configure Release process</span></span>
* <span data-ttu-id="14446-175">Utwórz nową wersją</span><span class="sxs-lookup"><span data-stu-id="14446-175">Create a new release</span></span>

![Utwórz nową wersją][20]

* <span data-ttu-id="14446-177">Wybierz zadanie wdrażania usługi w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="14446-177">Select the Azure Cloud Services Deployment task</span></span>

![Wybierz zadania wdrożenia usługi w chmurze Azure][21]

* <span data-ttu-id="14446-179">Jak klucz konta magazynu nie zostanie zaznaczona w celu kontroli źródła, należy określić klucz tajny do ustawiania rozszerzeń diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="14446-179">As the storage account key is not checked in to source control, we need to specify the secret key for setting diagnostics extensions.</span></span> <span data-ttu-id="14446-180">Rozwiń węzeł **zaawansowane opcje tworzenia nowej usługi** sekcji i edytować **klucze konta magazynu diagnostyki** parametr wejściowy.</span><span class="sxs-lookup"><span data-stu-id="14446-180">Expand the **Advanced Options for Creating New Service** section and edit the **Diagnostics Storage Account Keys** parameter input.</span></span> <span data-ttu-id="14446-181">Pobiera tych danych wejściowych w wielu wierszach para klucz-wartość w formacie **[RoleName]:$(StorageAccountKey)**</span><span class="sxs-lookup"><span data-stu-id="14446-181">This input takes in multiple lines of key value pair in the format of **[RoleName]:$(StorageAccountKey)**</span></span>

> <span data-ttu-id="14446-182">Uwaga: w przypadku konta magazynu diagnostyki w ramach tej samej subskrypcji co gdzie opublikuje aplikacji usługi w chmurze, nie trzeba wprowadzić klucz w danych wejściowych zadań wdrażania; wdrożenie programowo uzyska informacji magazynu z subskrypcji</span><span class="sxs-lookup"><span data-stu-id="14446-182">Note: if your diagnostics storage account is under the same subscription as where you will publish the Cloud Services application, you don't have to enter the key in the deployment task input; the deployment will programmatically obtain the storage information from your subscription</span></span>
> 
> 

![Skonfiguruj zadania wdrożenia usługi w chmurze][22]

* <span data-ttu-id="14446-184">Użyj klucza tajnego kompilacji zmienne, aby zapisać magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="14446-184">Use secret build variables to save storage Keys.</span></span> <span data-ttu-id="14446-185">Do zamaskowania zmiennej jako klucza tajnego kliknij ikonę blokady po prawej stronie dane wejściowe zmiennych</span><span class="sxs-lookup"><span data-stu-id="14446-185">To mask a variable as secret click on the lock icon on the right side of the Variables input</span></span>

![Zapisywanie magazynu kluczy w zmiennych tajny kompilacji][23]

* <span data-ttu-id="14446-187">Tworzenie zlecenia i wdrażanie projektu na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="14446-187">Create a release and deploy your project to Azure</span></span>

![Utwórz nową wersją][24]

## <a name="next-steps"></a><span data-ttu-id="14446-189">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="14446-189">Next steps</span></span>
<span data-ttu-id="14446-190">Aby dowiedzieć się więcej na temat ustawiania rozszerzeń diagnostyki dla usług w chmurze Azure, zobacz [Włącz diagnostykę w usług Azure Cloud Services przy użyciu programu PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="14446-190">To learn more about setting diagnostics extensions for Azure Cloud Services, please see [Enable diagnostics in Azure Cloud Services using PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span></span>

[Create Visual Studio Online account]:https://www.visualstudio.com/team-services/
[Create team project]: https://www.visualstudio.com/it-it/docs/setup-admin/team-services/connect-to-visual-studio-team-services
[Enable diagnostics in Azure Cloud Services using PowerShell]:https://azure.microsoft.com/en-us/documentation/articles/cloud-services-diagnostics-powershell/

[0]: ./media/cloud-services-vs-ci/vs-01.png
[1]: ./media/cloud-services-vs-ci/vs-02.png
[2]: ./media/cloud-services-vs-ci/file-01.png
[3]: ./media/cloud-services-vs-ci/vs-03.png
[4]: ./media/cloud-services-vs-ci/vs-04.png
[5]: ./media/cloud-services-vs-ci/vs-05.png
[6]: ./media/cloud-services-vs-ci/vs-06.png
[7]: ./media/cloud-services-vs-ci/vs-07.png
[8]: ./media/cloud-services-vs-ci/vs-08.png
[9]: ./media/cloud-services-vs-ci/vs-09.png
[10]: ./media/cloud-services-vs-ci/vso-01.png
[11]: ./media/cloud-services-vs-ci/vso-02.png
[12]: ./media/cloud-services-vs-ci/vso-03.png
[13]: ./media/cloud-services-vs-ci/vso-04.png
[14]: ./media/cloud-services-vs-ci/vso-05.png
[15]: ./media/cloud-services-vs-ci/vso-06.png
[16]: ./media/cloud-services-vs-ci/vso-07.png
[17]: ./media/cloud-services-vs-ci/vso-08.png
[18]: ./media/cloud-services-vs-ci/vso-09.png
[19]: ./media/cloud-services-vs-ci/vso-10.png
[20]: ./media/cloud-services-vs-ci/vso-11.png
[21]: ./media/cloud-services-vs-ci/vso-12.png
[22]: ./media/cloud-services-vs-ci/vso-13.png
[23]: ./media/cloud-services-vs-ci/vso-14.png
[24]: ./media/cloud-services-vs-ci/vso-15.png
