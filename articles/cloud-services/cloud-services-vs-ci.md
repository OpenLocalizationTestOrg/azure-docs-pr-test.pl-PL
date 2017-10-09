---
title: "dostarczanie aaaContinuous chmury usług za pomocą programu Visual Studio Online | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset się ciągłego dostarczania dla platformy Azure aplikacji w chmurze bez zapisywania plików konfiguracyjnych usługi toohello klucza magazynu diagnostyki"
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
ms.openlocfilehash: dc87d049e46daf8b8a26ee4450ebd9b7910f287b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-tooazure-using-visual-studio-online"></a><span data-ttu-id="3f4d7-103">Securely Zapisz usług diagnostyki klucz magazynu w chmurze i tooAzure Instalatora ciągłej integracji i wdrażania przy użyciu programu Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="3f4d7-103">Securely Save Cloud Services Diagnostics Storage Key and Setup Continuous Integration and Deployment tooAzure using Visual Studio Online</span></span>
 <span data-ttu-id="3f4d7-104">Wspólne projekty źródła tooopen rozwiązaniem jest obecnie.</span><span class="sxs-lookup"><span data-stu-id="3f4d7-104">It is a common practice tooopen source projects nowadays.</span></span> <span data-ttu-id="3f4d7-105">Zapisywanie w plikach konfiguracji hasła aplikacji nie jest już bezpieczne praktyki jako luk w zabezpieczeniach są widoczne z kluczy tajnych wycieku z kontrolki źródła publicznego.</span><span class="sxs-lookup"><span data-stu-id="3f4d7-105">Saving application secrets in configuration files is no longer safe practice as security vulnerabilities are exposed from secrets being leaked from public source controls.</span></span> <span data-ttu-id="3f4d7-106">Przechowywanie klucza tajnego jako zwykłego tekstu w pliku w potoku ciągłej integracji nie są chronione albo ponieważ serwery kompilacji może być udostępnionych zasobów w środowisku chmury hello.</span><span class="sxs-lookup"><span data-stu-id="3f4d7-106">Storing secret as plaintext in a file in a Continuous Integration pipeline is not secure either since build servers could be shared resources on hello Cloud environment.</span></span> <span data-ttu-id="3f4d7-107">W tym artykule opisano, jak Visual Studio i Visual Studio Online zmniejsza hello bezpieczeństwo podczas procesu ciągłej integracji i rozwoju.</span><span class="sxs-lookup"><span data-stu-id="3f4d7-107">This article explains how Visual Studio and Visual Studio Online mitigates hello security concerns during development and Continuous Integration process.</span></span>

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a><span data-ttu-id="3f4d7-108">Usuń hasło klucza magazynu diagnostyki w pliku konfiguracji projektu</span><span class="sxs-lookup"><span data-stu-id="3f4d7-108">Remove Diagnostics Storage Key Secret in Project Configuration File</span></span>
<span data-ttu-id="3f4d7-109">Rozszerzenie Diagnostyka usług w chmurze wymaga magazynu Azure do zapisywania wyników diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="3f4d7-109">Cloud Services diagnostics extension requires Azure storage for saving diagnostics results.</span></span> <span data-ttu-id="3f4d7-110">Wcześniej parametry połączenia magazynu hello jest określona w plikach konfiguracji (cscfg) hello usługi w chmurze i można sprawdzić w formancie toosource.</span><span class="sxs-lookup"><span data-stu-id="3f4d7-110">Formerly hello storage connection string is specified in hello Cloud Services configuration (.cscfg) files and could be checked in toosource control.</span></span> <span data-ttu-id="3f4d7-111">W najnowszej wersji zestawu Azure SDK hello możemy zmienić magazynu tooonly zachowanie hello parametrów połączenia częściowe kluczem hello zastępuje token.</span><span class="sxs-lookup"><span data-stu-id="3f4d7-111">In hello latest Azure SDK release we changed hello behavior tooonly store a partial connection string with hello key replaced by a token.</span></span> <span data-ttu-id="3f4d7-112">Hello następujące kroki opisano, jak działa hello nowych narzędzi usługi w chmurze:</span><span class="sxs-lookup"><span data-stu-id="3f4d7-112">hello following steps describe how hello new Cloud Services tooling works:</span></span>

### <a name="1-open-hello-role-designer"></a><span data-ttu-id="3f4d7-113">1. Otwórz projektanta roli hello</span><span class="sxs-lookup"><span data-stu-id="3f4d7-113">1. Open hello Role designer</span></span>
* <span data-ttu-id="3f4d7-114">Kliknij dwukrotnie lub kliknij prawym przyciskiem myszy Projektanta roli tooopen roli usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="3f4d7-114">Double click or right click on a Cloud Services role tooopen Role designer</span></span>

![Otwórz rolę projektanta][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a><span data-ttu-id="3f4d7-116">2. W sekcji Diagnostyka nowe pole wyboru "nie usuwaj magazynu klucz tajny z projektu" zostanie dodany.</span><span class="sxs-lookup"><span data-stu-id="3f4d7-116">2. Under diagnostics section, a new check box “Don’t remove storage key secret from project” is added</span></span>
* <span data-ttu-id="3f4d7-117">Jeśli używasz emulatora magazynu lokalne powitania to pole wyboru jest wyłączona, ponieważ nie istnieje żadne tajny toomanage dla parametrów połączenia lokalne powitania, czyli UseDevelopmentStorage = true.</span><span class="sxs-lookup"><span data-stu-id="3f4d7-117">If you are using hello local storage emulator, this checkbox is disabled because there is no secret toomanage for hello local connection string, which is UseDevelopmentStorage=true.</span></span>

![Parametry połączenia emulatora magazynu lokalnego nie jest tajny][1]

* <span data-ttu-id="3f4d7-119">W przypadku tworzenia nowego projektu, domyślnie to pole wyboru jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="3f4d7-119">If you are creating a new project, by default this checkbox is unchecked.</span></span> <span data-ttu-id="3f4d7-120">Powoduje to hello magazynu kluczy części parametrów połączenia magazynu hello wybrane zastępowane z tokenem.</span><span class="sxs-lookup"><span data-stu-id="3f4d7-120">This results in hello storage key section of hello selected storage connection string being replaced with a token.</span></span> <span data-ttu-id="3f4d7-121">Witaj wartość tokenu hello zostaną znalezione w folderze roamingu AppData hello bieżącego użytkownika, na przykład: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span><span class="sxs-lookup"><span data-stu-id="3f4d7-121">hello value of hello token will be found under hello current user’s AppData Roaming folder, for example: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span></span>

> <span data-ttu-id="3f4d7-122">Należy pamiętać, ten folder user\AppData hello jest kontrolowany dostęp przez logowania użytkownika i jest uznawany za kluczy tajnych programowanie dla toostore w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="3f4d7-122">Note that hello user\AppData folder is Access Controlled by user sign-in and is considered a secure place toostore development secrets.</span></span>
> 
> 

![Klucz magazynu jest zapisywany w folderze profilu użytkownika][2]

### <a name="3-select-a-diagnostics-storage-account"></a><span data-ttu-id="3f4d7-124">3. Wybierz konto magazynu diagnostyki</span><span class="sxs-lookup"><span data-stu-id="3f4d7-124">3. Select a diagnostics storage account</span></span>
* <span data-ttu-id="3f4d7-125">Wybierz konto magazynu z okna dialogowego hello uruchomić, klikając pozycję "..." hello</span><span class="sxs-lookup"><span data-stu-id="3f4d7-125">Select a storage account from hello dialog launched by clicking hello “…”</span></span> <span data-ttu-id="3f4d7-126">Dodaj...</span><span class="sxs-lookup"><span data-stu-id="3f4d7-126">button.</span></span> <span data-ttu-id="3f4d7-127">Zwróć uwagę, jak parametry połączenia magazynu hello wygenerowany nie będzie miał klucz konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="3f4d7-127">Notice how hello storage connection string generated will not have hello storage account key.</span></span>
* <span data-ttu-id="3f4d7-128">Na przykład: DefaultEndpointsProtocol = https; AccountName = contosostorage; AccountKey = $(*clouddiagstrg.key*)</span><span class="sxs-lookup"><span data-stu-id="3f4d7-128">For example: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span></span>

### <a name="4----debugging-hello-project"></a><span data-ttu-id="3f4d7-129">4.    Debugowanie projektu hello</span><span class="sxs-lookup"><span data-stu-id="3f4d7-129">4.    Debugging hello project</span></span>
* <span data-ttu-id="3f4d7-130">Toostart F5 debugowania w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3f4d7-130">F5 toostart debugging in Visual Studio.</span></span> <span data-ttu-id="3f4d7-131">Wszystko, co powinny działać w hello sam sposób jak wcześniej.</span><span class="sxs-lookup"><span data-stu-id="3f4d7-131">Everything should work in hello same way as before.</span></span>
  <span data-ttu-id="3f4d7-132">![Rozpocznij debugowanie lokalnie][3]</span><span class="sxs-lookup"><span data-stu-id="3f4d7-132">![Start debugging locally][3]</span></span>

### <a name="5-publish-project-from-visual-studio"></a><span data-ttu-id="3f4d7-133">5. Opublikować projekt w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3f4d7-133">5. Publish project from Visual Studio</span></span>
* <span data-ttu-id="3f4d7-134">Uruchom hello okna dialogowego publikowania i kontynuować logowania instrukcje toopublish hello applicaion tooAzure.</span><span class="sxs-lookup"><span data-stu-id="3f4d7-134">Launch hello publish dialog and proceed with sign-in instructions toopublish hello applicaion tooAzure.</span></span>

### <a name="6-additional-information"></a><span data-ttu-id="3f4d7-135">6. Dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="3f4d7-135">6. Additional information</span></span>
> <span data-ttu-id="3f4d7-136">Uwaga: hello panel ustawień w Projektancie roli hello pozostanie, ponieważ jest on obecnie.</span><span class="sxs-lookup"><span data-stu-id="3f4d7-136">Note: hello Settings panel in hello role designer will stay as it is for now.</span></span> <span data-ttu-id="3f4d7-137">Funkcja zarządzania tajny hello toouse diagnostyki, przejdź toohello konfiguracji karty.</span><span class="sxs-lookup"><span data-stu-id="3f4d7-137">If you want toouse hello secret management feature for diagnostics, go toohello Configurations tab.</span></span>
> 
> 

![Dodaj ustawienia][4]

> <span data-ttu-id="3f4d7-139">Uwaga: Włączenie klucza usługi Application Insights hello będą przechowywane jako zwykły tekst.</span><span class="sxs-lookup"><span data-stu-id="3f4d7-139">Note: If enabled, hello Application Insights key will be stored as plain text.</span></span> <span data-ttu-id="3f4d7-140">klucz Hello jest używana tylko do przekazywania zawartości tak będzie żadnych poufnych danych na ryzyko naruszenia bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="3f4d7-140">hello key is only used for upload contents so no sensitive data will be at risk being compromised.</span></span>
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a><span data-ttu-id="3f4d7-141">Tworzenie i publikowanie projektu usługi w chmurze za pomocą programu Visual Studio online szablonów zadań</span><span class="sxs-lookup"><span data-stu-id="3f4d7-141">Build and Publish a Cloud Services Project using Visual Studio online Task Templates</span></span>
* <span data-ttu-id="3f4d7-142">Hello następujące kroki przedstawiono sposób toosetup ciągłej integracji usług w chmurze projektu za pomocą programu Visual Studio online zadań:</span><span class="sxs-lookup"><span data-stu-id="3f4d7-142">hello following steps illustrates how toosetup Continuous Integration for Cloud Services project using Visual Studio online tasks:</span></span>
  ### <a name="1----obtain-a-vso-account"></a><span data-ttu-id="3f4d7-143">1.    Uzyskaj konto usługi VSO</span><span class="sxs-lookup"><span data-stu-id="3f4d7-143">1.    Obtain a VSO account</span></span>
* <span data-ttu-id="3f4d7-144">[Utwórz konto Visual Studio Online] [ Create Visual Studio Online account] Jeśli nie masz już</span><span class="sxs-lookup"><span data-stu-id="3f4d7-144">[Create Visual Studio Online account][Create Visual Studio Online account] if you don’t have one already</span></span>
* <span data-ttu-id="3f4d7-145">[Tworzenie projektu zespołowego] [ Create team project] na koncie online programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3f4d7-145">[Create team project][Create team project] in your Visual Studio online account</span></span>

### <a name="2----setup-source-control-in-visual-studio"></a><span data-ttu-id="3f4d7-146">2.    Ustawienia kontroli wersji w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3f4d7-146">2.    Setup source control in Visual Studio</span></span>
* <span data-ttu-id="3f4d7-147">Połącz tooa projektu zespołowego</span><span class="sxs-lookup"><span data-stu-id="3f4d7-147">Connect tooa team project</span></span>

![Łączenie tooteam projektu][5]

![Wybierz tooconnect projektu zespołowego do][6]

* <span data-ttu-id="3f4d7-150">Dodawanie formantu toosource projektu</span><span class="sxs-lookup"><span data-stu-id="3f4d7-150">Add your project toosource control</span></span>

![Dodawanie formantu toosource projektu][7]

![Mapowania folderu kontroli źródła tooa projektu][8]

* <span data-ttu-id="3f4d7-153">Sprawdź w projekcie z programu Team Explorer</span><span class="sxs-lookup"><span data-stu-id="3f4d7-153">Check in your project from Team Explorer</span></span>

![Sprawdź w formancie toosource projektu][9]

### <a name="3----configure-build-process"></a><span data-ttu-id="3f4d7-155">3.    Konfigurowanie procesu kompilacji</span><span class="sxs-lookup"><span data-stu-id="3f4d7-155">3.    Configure Build process</span></span>
* <span data-ttu-id="3f4d7-156">Przeglądanie projektu zespołowego tooyour i dodać nowe szablony procesu kompilacji</span><span class="sxs-lookup"><span data-stu-id="3f4d7-156">Browse tooyour team project and add a new build process Templates</span></span>

![Dodawanie nowej kompilacji][10]

* <span data-ttu-id="3f4d7-158">Wybierz kompilację zadań</span><span class="sxs-lookup"><span data-stu-id="3f4d7-158">Select build task</span></span>

![Dodaj zadanie kompilacji][11]

![Wybierz szablon zadania kompilacji programu Visual Studio][12]

* <span data-ttu-id="3f4d7-161">Edytuj dane wejściowe zadania kompilacji.</span><span class="sxs-lookup"><span data-stu-id="3f4d7-161">Edit build task input.</span></span> <span data-ttu-id="3f4d7-162">Należy dostosować parametry zgodnie z tooyour wymagają kompilacji hello</span><span class="sxs-lookup"><span data-stu-id="3f4d7-162">Please customize hello build parameters according tooyour need</span></span>

![Skonfiguruj zadania kompilacji][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* <span data-ttu-id="3f4d7-164">Skonfiguruj zmienne kompilacji</span><span class="sxs-lookup"><span data-stu-id="3f4d7-164">Configure build variables</span></span>

![Skonfiguruj zmienne kompilacji][14]

* <span data-ttu-id="3f4d7-166">Dodaj dane wyjściowe kompilacji tooupload zadań</span><span class="sxs-lookup"><span data-stu-id="3f4d7-166">Add a task tooupload build drop</span></span>

![Wybierz publikowania kompilacji listy zadań][15]

![Skonfiguruj publikowanie kompilacji listy zadań][16]

* <span data-ttu-id="3f4d7-169">Uruchom hello kompilacji</span><span class="sxs-lookup"><span data-stu-id="3f4d7-169">Run hello build</span></span>

![Kolejki nowej kompilacji][17]

![Wyświetl podsumowanie kompilacji][18]

* <span data-ttu-id="3f4d7-172">Jeśli hello kompilacja zakończy się pomyślnie zobaczysz toobelow podobne wyników</span><span class="sxs-lookup"><span data-stu-id="3f4d7-172">if hello build is successful you will see a result similar toobelow</span></span>

![Wynik kompilacji][19]

### <a name="4----configure-release-process"></a><span data-ttu-id="3f4d7-174">4.    Konfigurowanie procesu publikacji</span><span class="sxs-lookup"><span data-stu-id="3f4d7-174">4.    Configure Release process</span></span>
* <span data-ttu-id="3f4d7-175">Utwórz nową wersją</span><span class="sxs-lookup"><span data-stu-id="3f4d7-175">Create a new release</span></span>

![Utwórz nową wersją][20]

* <span data-ttu-id="3f4d7-177">Wybierz zadanie wdrażania usługi w chmurze Azure hello</span><span class="sxs-lookup"><span data-stu-id="3f4d7-177">Select hello Azure Cloud Services Deployment task</span></span>

![Wybierz zadania wdrożenia usługi w chmurze Azure][21]

* <span data-ttu-id="3f4d7-179">Ponieważ klucz konta magazynu hello nie jest zaznaczona w formancie toosource, potrzebujemy klucz tajny hello toospecify do ustawiania rozszerzeń diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="3f4d7-179">As hello storage account key is not checked in toosource control, we need toospecify hello secret key for setting diagnostics extensions.</span></span> <span data-ttu-id="3f4d7-180">Rozwiń węzeł hello **zaawansowane opcje tworzenia nowej usługi** sekcji i edytować hello **klucze konta magazynu diagnostyki** parametr wejściowy.</span><span class="sxs-lookup"><span data-stu-id="3f4d7-180">Expand hello **Advanced Options for Creating New Service** section and edit hello **Diagnostics Storage Account Keys** parameter input.</span></span> <span data-ttu-id="3f4d7-181">Pobiera tych danych wejściowych w wielu wierszach para klucz-wartość w formacie hello **[RoleName]:$(StorageAccountKey)**</span><span class="sxs-lookup"><span data-stu-id="3f4d7-181">This input takes in multiple lines of key value pair in hello format of **[RoleName]:$(StorageAccountKey)**</span></span>

> <span data-ttu-id="3f4d7-182">Uwaga: Jeśli diagnostycznej konto magazynu znajduje się w obszarze hello tej samej subskrypcji co którym będą publikowane hello aplikacji usługi w chmurze, nie ma klucza hello tooenter w danych wejściowych zadań wdrażania hello; wdrożenie Hello programowo uzyska hello magazynu informacji z subskrypcji</span><span class="sxs-lookup"><span data-stu-id="3f4d7-182">Note: if your diagnostics storage account is under hello same subscription as where you will publish hello Cloud Services application, you don't have tooenter hello key in hello deployment task input; hello deployment will programmatically obtain hello storage information from your subscription</span></span>
> 
> 

![Skonfiguruj zadania wdrożenia usługi w chmurze][22]

* <span data-ttu-id="3f4d7-184">Użyj klucza tajnego kompilacji toosave zmienne magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="3f4d7-184">Use secret build variables toosave storage Keys.</span></span> <span data-ttu-id="3f4d7-185">toomask zmiennej jako klucza tajnego kliknij ikonę blokady powitania po prawej stronie powitania hello zmienne wejściowe</span><span class="sxs-lookup"><span data-stu-id="3f4d7-185">toomask a variable as secret click on hello lock icon on hello right side of hello Variables input</span></span>

![Zapisywanie magazynu kluczy w zmiennych tajny kompilacji][23]

* <span data-ttu-id="3f4d7-187">Tworzenie zlecenia i wdrażanie tooAzure Twojego projektu</span><span class="sxs-lookup"><span data-stu-id="3f4d7-187">Create a release and deploy your project tooAzure</span></span>

![Utwórz nową wersją][24]

## <a name="next-steps"></a><span data-ttu-id="3f4d7-189">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3f4d7-189">Next steps</span></span>
<span data-ttu-id="3f4d7-190">toolearn więcej informacji na temat ustawiania rozszerzeń diagnostyki dla usług w chmurze Azure, zobacz [Włącz diagnostykę w usług Azure Cloud Services przy użyciu programu PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="3f4d7-190">toolearn more about setting diagnostics extensions for Azure Cloud Services, please see [Enable diagnostics in Azure Cloud Services using PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span></span>

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
