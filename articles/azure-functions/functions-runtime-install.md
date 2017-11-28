---
title: "aaaAzure instalacji środowiska uruchomieniowego funkcje | Dokumentacja firmy Microsoft"
description: "Jak tooInstall hello środowisko uruchomieniowe Functions Azure"
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 67c6d10b5c0ac43e880d29cff0ae7b099f82bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-functions-runtime-preview"></a><span data-ttu-id="dc5cd-103">Zainstaluj hello Azure funkcje środowiska wykonawczego w wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="dc5cd-103">Install hello Azure Functions Runtime Preview</span></span>

<span data-ttu-id="dc5cd-104">Jeśli chcesz tooinstall hello środowisko uruchomieniowe Functions Azure w wersji zapoznawczej, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="dc5cd-104">If you would like tooinstall hello Azure Functions Runtime preview, you must follow these steps:</span></span>

1. <span data-ttu-id="dc5cd-105">Upewnij się, że komputer przekazuje hello minimalne wymagania</span><span class="sxs-lookup"><span data-stu-id="dc5cd-105">Ensure your machine passes hello minimum requirements</span></span>
1. <span data-ttu-id="dc5cd-106">Pobierz hello [Azure funkcje środowiska wykonawczego w wersji zapoznawczej Instalatora](https://aka.ms/azafr).</span><span class="sxs-lookup"><span data-stu-id="dc5cd-106">Download hello [Azure Functions Runtime Preview Installer](https://aka.ms/azafr).</span></span> 
1. <span data-ttu-id="dc5cd-107">Zainstaluj hello środowisko uruchomieniowe Functions Azure w wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="dc5cd-107">Install hello Azure Functions Runtime preview</span></span>
1. <span data-ttu-id="dc5cd-108">Konfiguracja pełną hello hello środowisko uruchomieniowe Functions Azure w wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="dc5cd-108">Complete hello configuration of hello Azure Functions Runtime preview</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc5cd-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dc5cd-109">Prerequisites</span></span>

<span data-ttu-id="dc5cd-110">Przed zainstalowaniem hello środowisko uruchomieniowe Functions Azure w wersji zapoznawczej, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="dc5cd-110">Before you install hello Azure Functions Runtime preview, you must have hello following:</span></span>

1. <span data-ttu-id="dc5cd-111">Maszynie z systemem Microsoft Windows Server 2016 lub Microsoft Windows 10 twórców aktualizacji (Professional lub Enterprise Edition).</span><span class="sxs-lookup"><span data-stu-id="dc5cd-111">A machine running Microsoft Windows Server 2016 or Microsoft Windows 10 Creators Update (Professional or Enterprise Edition).</span></span>
1. <span data-ttu-id="dc5cd-112">Wystąpienie programu SQL Server działających w sieci.</span><span class="sxs-lookup"><span data-stu-id="dc5cd-112">A SQL Server instance running within your network.</span></span>  <span data-ttu-id="dc5cd-113">Minimalna wersja wymaganie to SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="dc5cd-113">Minimum edition requirement is SQL Server Express.</span></span>

## <a name="install-hello-azure-functions-runtime-preview"></a><span data-ttu-id="dc5cd-114">Zainstaluj hello Azure funkcje środowiska wykonawczego w wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="dc5cd-114">Install hello Azure Functions Runtime Preview</span></span>

<span data-ttu-id="dc5cd-115">Instalatora w wersji zapoznawczej środowisko uruchomieniowe Functions Azure Hello przeprowadzi Cię przez instalację hello hello środowisko uruchomieniowe Functions Azure w wersji zapoznawczej zarządzania i roli proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="dc5cd-115">hello Azure Functions Runtime preview installer guides you through hello installation of hello Azure Functions Runtime preview Management and Worker Roles.</span></span>  <span data-ttu-id="dc5cd-116">Witaj tooinstall możliwości zarządzania i roli proces roboczy na powitania jest tym samym komputerze.</span><span class="sxs-lookup"><span data-stu-id="dc5cd-116">It is possible tooinstall hello Management and Worker role on hello same machine.</span></span>  <span data-ttu-id="dc5cd-117">Jednak podczas dodawania więcej funkcji, należy wdrożyć jedną rolę procesu roboczego w stanie tooscale toobe dodatkowych maszyn funkcji na wielu pracowników.</span><span class="sxs-lookup"><span data-stu-id="dc5cd-117">However, as you add more Functions, you must deploy more worker roles on additional machines toobe able tooscale your functions onto multiple workers.</span></span>

## <a name="install-hello-management-and-worker-role-on-hello-same-machine"></a><span data-ttu-id="dc5cd-118">Zainstaluj hello zarządzania i roli proces roboczy na powitania tym samym komputerze</span><span class="sxs-lookup"><span data-stu-id="dc5cd-118">Install hello Management and Worker Role on hello same machine</span></span>

1. <span data-ttu-id="dc5cd-119">Uruchom hello Azure funkcje środowiska wykonawczego w wersji zapoznawczej Instalatora.</span><span class="sxs-lookup"><span data-stu-id="dc5cd-119">Run hello Azure Functions Runtime Preview Installer.</span></span>

    ![Środowisko Azure Functions środowiska wykonawczego w wersji zapoznawczej Instalatora][1]

1. <span data-ttu-id="dc5cd-121">**Kliknij przycisk Dalej** zaliczki poza hello pierwszego etapu hello Instalatora</span><span class="sxs-lookup"><span data-stu-id="dc5cd-121">**Click Next** advance past hello first stage of hello installer</span></span>
1. <span data-ttu-id="dc5cd-122">Po zapoznaniu się z warunkami hello hello **umowy licencyjnej**, **hello pole wyboru** tooaccept hello warunki i **kliknij przycisk Dalej** tooadvance.</span><span class="sxs-lookup"><span data-stu-id="dc5cd-122">Once you have read hello terms of hello **EULA**, **check hello box** tooaccept hello terms and **click Next** tooadvance.</span></span>
1. <span data-ttu-id="dc5cd-123">Teraz wybierz hello ról ma tooinstall na tym komputerze **funkcje zarządzania roli** i/lub **roli procesu roboczego funkcji** i **, kliknij przycisk Dalej**</span><span class="sxs-lookup"><span data-stu-id="dc5cd-123">Now select hello roles you want tooinstall on this machine **Functions Management Role** and/or **Functions Worker Role** and **Click Next**</span></span>

    ![Azure Functions środowiska wykonawczego w wersji zapoznawczej Instalator — Wybór roli][3]

    > [!NOTE]
    > <span data-ttu-id="dc5cd-125">Można zainstalować hello **roli procesu roboczego funkcji** na inne toodo maszyny, wykonaj te instrukcje i wybierz tylko **roli procesu roboczego funkcji** w Instalatorze hello.</span><span class="sxs-lookup"><span data-stu-id="dc5cd-125">You can install hello **Functions Worker Role** on many other machines toodo so, follow these instructions, and only select **Functions Worker Role** in hello installer.</span></span>

1. <span data-ttu-id="dc5cd-126">**Kliknij przycisk Dalej** toohave hello **Azure funkcji środowiska uruchomieniowego Instalator** zainstalować na komputerze.</span><span class="sxs-lookup"><span data-stu-id="dc5cd-126">**Click Next** toohave hello **Azure Functions Runtime Installer** install on your machine.</span></span>
1. <span data-ttu-id="dc5cd-127">Po pełną hello Instalator uruchomi hello **narzędzia do konfiguracji środowiska uruchomieniowego funkcji Azure**.</span><span class="sxs-lookup"><span data-stu-id="dc5cd-127">Once complete hello installer will launch hello **Azure Functions Runtime Configuration tool**.</span></span>

    ![Azure Functions środowiska wykonawczego w wersji zapoznawczej Instalatora pełną][5]

    > [!NOTE]
    > <span data-ttu-id="dc5cd-129">Jeśli instalujesz na **systemu Windows 10** i hello **kontenera** funkcji nie został wcześniej włączony, hello **środowisko uruchomieniowe Functions Azure** Instalator monituje tooreboot Zainstaluj hello toocomplete Twojego komputera.</span><span class="sxs-lookup"><span data-stu-id="dc5cd-129">If you are installing on **Windows 10** and hello **Container** feature has not been previously enabled, hello **Azure Functions Runtime** Installer prompts you tooreboot your machine toocomplete hello install.</span></span>

## <a name="configure-hello-azure-functions-runtime"></a><span data-ttu-id="dc5cd-130">Skonfiguruj hello środowisko uruchomieniowe Functions Azure</span><span class="sxs-lookup"><span data-stu-id="dc5cd-130">Configure hello Azure Functions Runtime</span></span>

<span data-ttu-id="dc5cd-131">Witaj toocomplete środowisko uruchomieniowe Functions Azure instalacji należy wykonać hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="dc5cd-131">toocomplete hello Azure Functions Runtime installation you must complete hello configuration.</span></span>

1. <span data-ttu-id="dc5cd-132">Witaj **narzędzie konfiguracji środowiska wykonawczego funkcji Azure** pokazuje role są zainstalowane na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="dc5cd-132">hello **Azure Functions Runtime Configuration Tool** shows which roles are installed on your machine.</span></span>

    ![Środowisko Azure Functions narzędzia do konfiguracji podglądu środowiska wykonawczego][6]

1. <span data-ttu-id="dc5cd-134">Kliknij przycisk hello **bazy danych** wprowadź hello **szczegóły połączenia dla wystąpienia programu SQL Server** i **kliknij przycisk Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="dc5cd-134">Click hello **Database** tab, enter hello **connection details for your SQL Server Instance** and **click Apply**.</span></span>  <span data-ttu-id="dc5cd-135">Jest to wymagane w kolejności toohello toocreate środowisko uruchomieniowe Functions Azure hello toosupport bazy danych środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="dc5cd-135">This is required in order toohello Azure Functions Runtime toocreate a database toosupport hello Runtime.</span></span>
    
    ![Środowisko Azure Functions środowiska uruchomieniowego Podgląd bazy danych konfiguracji][7]

1. <span data-ttu-id="dc5cd-137">Kliknij przycisk hello **poświadczenia** kartę.  Na tym ekranie należy utworzyć dwa nowe poświadczenia do użycia z udziałem plików do obsługi wszystkich funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dc5cd-137">Click hello **Credentials** tab.  On this screen you must create two new credentials for use with a FileShare for hosting all your Azure Functions.</span></span>  <span data-ttu-id="dc5cd-138">**Określ nazwę użytkownika i hasło** kombinacji hello **właściciela udziału pliku** i hello **użytkownika udziału pliku** i kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="dc5cd-138">**Specify Username and Password** combinations for hello **File Share Owner** and for hello **File Share User** and click **Apply**.</span></span>

    ![Środowisko Azure Functions środowiska wykonawczego w wersji zapoznawczej poświadczenia][8]

1. <span data-ttu-id="dc5cd-140">Kliknij przycisk hello **udziału plików** kartę.  Na tym ekranie Podaj szczegóły hello hello **lokalizację udziału pliku**.</span><span class="sxs-lookup"><span data-stu-id="dc5cd-140">Click hello **File Share** tab.  In this screen you must specify hello details of hello **File Share location**.</span></span>  <span data-ttu-id="dc5cd-141">Można go utworzyć dla Ciebie lub można użyć istniejącego udziału plików i kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="dc5cd-141">This can be created for you or you can use an existing File Share and click **Apply**.</span></span>  <span data-ttu-id="dc5cd-142">W przypadku wybrania nowej lokalizacji udziału plików, należy określić katalog dla przez hello środowisko uruchomieniowe Functions Azure.</span><span class="sxs-lookup"><span data-stu-id="dc5cd-142">If you select a new File Share location, you must specify a directory for use by hello Azure Functions Runtime.</span></span>
    
    ![Udział pliku podglądu środowiska uruchomieniowego usługę Azure Functions][9]

1. <span data-ttu-id="dc5cd-144">Kliknij przycisk hello **IIS** kartę.  Ta karta przedstawia szczegóły hello hello witryn sieci Web w usługach IIS tego powitalne Azure funkcji środowiska uruchomieniowego instalacji zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="dc5cd-144">Click hello **IIS** tab.  This tab shows hello details of hello websites in IIS that hello Azure Functions Runtime Installation will create.</span></span>  <span data-ttu-id="dc5cd-145">**Kliknij przycisk Zastosuj** toocomplete.</span><span class="sxs-lookup"><span data-stu-id="dc5cd-145">**Click Apply** toocomplete.</span></span>

    ![Środowisko Azure Functions środowiska wykonawczego w wersji zapoznawczej usług IIS][10]

1. <span data-ttu-id="dc5cd-147">Kliknij przycisk hello **usług** kartę.  Ta karta przedstawia hello stanu usług hello w środowisku uruchomieniowym funkcji Azure instalacji.</span><span class="sxs-lookup"><span data-stu-id="dc5cd-147">Click hello **Services** tab.  This tab shows hello status of hello services in your Azure Functions Runtime installation.</span></span>  <span data-ttu-id="dc5cd-148">Jeżeli po początkowej konfiguracji hello **usługi aktywacji hosta funkcji Azure** nie działa kliknij **Uruchom usługę**</span><span class="sxs-lookup"><span data-stu-id="dc5cd-148">If after initial configuration hello **Azure Functions Host Activation Service** is not running click **Start Service**</span></span>

    ![Środowisko Azure Functions środowiska wykonawczego w wersji zapoznawczej Configruation pełną][11]

1. <span data-ttu-id="dc5cd-150">Na koniec Przeglądaj toohello **portalu środowisko uruchomieniowe Functions Azure** jako`https://<machinename>/`</span><span class="sxs-lookup"><span data-stu-id="dc5cd-150">Finally browse toohello **Azure Functions Runtime Portal** as `https://<machinename>/`</span></span>

    ![Portal w wersji zapoznawczej usługi Azure Functions środowiska wykonawczego][12]


<!--Image references-->
[1]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer1.png
[2]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer2-EULA.png
[3]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer3-ChooseRoles.png
[4]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer4-Install.png
[5]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer5-InstallComplete.png
[6]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration1.png
[7]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration2_SQL.png
[8]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration3_Credentials.png
[9]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration4_Fileshare.png
[10]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration5_IIS.png
[11]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration6_Services.png
[12]: ./media/functions-runtime-install/AzureFunctionsRuntime_Portal.png