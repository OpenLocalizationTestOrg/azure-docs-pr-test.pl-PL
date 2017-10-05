---
title: "Azure Functions instalacji środowiska uruchomieniowego | Dokumentacja firmy Microsoft"
description: "Jak zainstalować usługę Azure Functions środowiska uruchomieniowego"
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
ms.openlocfilehash: 1e4188313a87d07f396e5f8edc8969dd5da2c436
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="install-the-azure-functions-runtime-preview"></a><span data-ttu-id="708f6-103">Zainstaluj usługę Azure Functions podglądu środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="708f6-103">Install the Azure Functions Runtime Preview</span></span>

<span data-ttu-id="708f6-104">Jeśli chcesz zainstalować środowisko uruchomieniowe Functions Azure w wersji zapoznawczej, należy wykonać następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="708f6-104">If you would like to install the Azure Functions Runtime preview, you must follow these steps:</span></span>

1. <span data-ttu-id="708f6-105">Upewnij się, że komputer przekazuje minimalne wymagania</span><span class="sxs-lookup"><span data-stu-id="708f6-105">Ensure your machine passes the minimum requirements</span></span>
1. <span data-ttu-id="708f6-106">Pobierz [Azure Functions środowiska wykonawczego w wersji zapoznawczej Instalatora](https://aka.ms/azafr).</span><span class="sxs-lookup"><span data-stu-id="708f6-106">Download the [Azure Functions Runtime Preview Installer](https://aka.ms/azafr).</span></span> 
1. <span data-ttu-id="708f6-107">Zainstaluj środowisko uruchomieniowe Functions Azure w wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="708f6-107">Install the Azure Functions Runtime preview</span></span>
1. <span data-ttu-id="708f6-108">Zakończ konfigurację podglądu środowiska uruchomieniowego funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="708f6-108">Complete the configuration of the Azure Functions Runtime preview</span></span>

## <a name="prerequisites"></a><span data-ttu-id="708f6-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="708f6-109">Prerequisites</span></span>

<span data-ttu-id="708f6-110">Przed zainstalowaniem podglądu środowiska uruchomieniowego funkcji Azure należy dysponować następującymi elementami:</span><span class="sxs-lookup"><span data-stu-id="708f6-110">Before you install the Azure Functions Runtime preview, you must have the following:</span></span>

1. <span data-ttu-id="708f6-111">Maszynie z systemem Microsoft Windows Server 2016 lub Microsoft Windows 10 twórców aktualizacji (Professional lub Enterprise Edition).</span><span class="sxs-lookup"><span data-stu-id="708f6-111">A machine running Microsoft Windows Server 2016 or Microsoft Windows 10 Creators Update (Professional or Enterprise Edition).</span></span>
1. <span data-ttu-id="708f6-112">Wystąpienie programu SQL Server działających w sieci.</span><span class="sxs-lookup"><span data-stu-id="708f6-112">A SQL Server instance running within your network.</span></span>  <span data-ttu-id="708f6-113">Minimalna wersja wymaganie to SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="708f6-113">Minimum edition requirement is SQL Server Express.</span></span>

## <a name="install-the-azure-functions-runtime-preview"></a><span data-ttu-id="708f6-114">Zainstaluj usługę Azure Functions podglądu środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="708f6-114">Install the Azure Functions Runtime Preview</span></span>

<span data-ttu-id="708f6-115">Środowisko uruchomieniowe Functions Azure Instalatora w wersji zapoznawczej przeprowadzi Cię przez instalację środowisko uruchomieniowe Functions Azure w wersji zapoznawczej zarządzania i roli proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="708f6-115">The Azure Functions Runtime preview installer guides you through the installation of the Azure Functions Runtime preview Management and Worker Roles.</span></span>  <span data-ttu-id="708f6-116">Istnieje możliwość zainstalowania roli zarządzania i proces roboczy na tym samym komputerze.</span><span class="sxs-lookup"><span data-stu-id="708f6-116">It is possible to install the Management and Worker role on the same machine.</span></span>  <span data-ttu-id="708f6-117">Jednak podczas dodawania więcej funkcji, należy wdrożyć jedną rolę procesu roboczego na dodatkowych komputerach możliwość skalowania funkcji na wielu pracowników.</span><span class="sxs-lookup"><span data-stu-id="708f6-117">However, as you add more Functions, you must deploy more worker roles on additional machines to be able to scale your functions onto multiple workers.</span></span>

## <a name="install-the-management-and-worker-role-on-the-same-machine"></a><span data-ttu-id="708f6-118">Zainstaluj na tym samym komputerze zarządzania i roli procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="708f6-118">Install the Management and Worker Role on the same machine</span></span>

1. <span data-ttu-id="708f6-119">Uruchom Instalatora programu Azure Functions środowiska wykonawczego w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="708f6-119">Run the Azure Functions Runtime Preview Installer.</span></span>

    ![Środowisko Azure Functions środowiska wykonawczego w wersji zapoznawczej Instalatora][1]

1. <span data-ttu-id="708f6-121">**Kliknij przycisk Dalej** zaliczki poza pierwszego etapu Instalatora</span><span class="sxs-lookup"><span data-stu-id="708f6-121">**Click Next** advance past the first stage of the installer</span></span>
1. <span data-ttu-id="708f6-122">Po przeczytaniu warunki **umowy licencyjnej**, **zaznacz pole wyboru** akceptacji warunków i **kliknij przycisk Dalej** można poprawić.</span><span class="sxs-lookup"><span data-stu-id="708f6-122">Once you have read the terms of the **EULA**, **check the box** to accept the terms and **click Next** to advance.</span></span>
1. <span data-ttu-id="708f6-123">Teraz wybierz role, którą chcesz zainstalować na tym komputerze **funkcje zarządzania roli** i/lub **roli procesu roboczego funkcji** i **, kliknij przycisk Dalej**</span><span class="sxs-lookup"><span data-stu-id="708f6-123">Now select the roles you want to install on this machine **Functions Management Role** and/or **Functions Worker Role** and **Click Next**</span></span>

    ![Azure Functions środowiska wykonawczego w wersji zapoznawczej Instalator — Wybór roli][3]

    > [!NOTE]
    > <span data-ttu-id="708f6-125">Można zainstalować **roli procesu roboczego funkcji** na wiele innych komputerach, aby to zrobić, wykonaj te instrukcje, a następnie wybrać tylko **roli procesu roboczego funkcji** w Instalatorze.</span><span class="sxs-lookup"><span data-stu-id="708f6-125">You can install the **Functions Worker Role** on many other machines to do so, follow these instructions, and only select **Functions Worker Role** in the installer.</span></span>

1. <span data-ttu-id="708f6-126">**Kliknij przycisk Dalej** mają **Azure funkcji środowiska uruchomieniowego Instalator** zainstalować na komputerze.</span><span class="sxs-lookup"><span data-stu-id="708f6-126">**Click Next** to have the **Azure Functions Runtime Installer** install on your machine.</span></span>
1. <span data-ttu-id="708f6-127">Po wykonaniu tych czynności spowoduje uruchomienie Instalatora **narzędzia do konfiguracji środowiska uruchomieniowego funkcji Azure**.</span><span class="sxs-lookup"><span data-stu-id="708f6-127">Once complete the installer will launch the **Azure Functions Runtime Configuration tool**.</span></span>

    ![Azure Functions środowiska wykonawczego w wersji zapoznawczej Instalatora pełną][5]

    > [!NOTE]
    > <span data-ttu-id="708f6-129">Jeśli instalujesz na **systemu Windows 10** i **kontenera** funkcji nie został wcześniej włączony, **środowisko uruchomieniowe Functions Azure** Instalator wyświetli monit o ponowny rozruch Twojej maszyny, aby zakończyć instalację.</span><span class="sxs-lookup"><span data-stu-id="708f6-129">If you are installing on **Windows 10** and the **Container** feature has not been previously enabled, the **Azure Functions Runtime** Installer prompts you to reboot your machine to complete the install.</span></span>

## <a name="configure-the-azure-functions-runtime"></a><span data-ttu-id="708f6-130">Skonfiguruj usługę Azure Functions środowiska uruchomieniowego</span><span class="sxs-lookup"><span data-stu-id="708f6-130">Configure the Azure Functions Runtime</span></span>

<span data-ttu-id="708f6-131">Aby ukończyć instalację środowisko uruchomieniowe Functions Azure należy wykonać konfigurację.</span><span class="sxs-lookup"><span data-stu-id="708f6-131">To complete the Azure Functions Runtime installation you must complete the configuration.</span></span>

1. <span data-ttu-id="708f6-132">**Narzędzie konfiguracji środowiska wykonawczego funkcji Azure** pokazuje role są zainstalowane na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="708f6-132">The **Azure Functions Runtime Configuration Tool** shows which roles are installed on your machine.</span></span>

    ![Środowisko Azure Functions narzędzia do konfiguracji podglądu środowiska wykonawczego][6]

1. <span data-ttu-id="708f6-134">Kliknij przycisk **bazy danych** wprowadź **szczegóły połączenia dla wystąpienia programu SQL Server** i **kliknij przycisk Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="708f6-134">Click the **Database** tab, enter the **connection details for your SQL Server Instance** and **click Apply**.</span></span>  <span data-ttu-id="708f6-135">Jest to wymagane w celu obsługi funkcji Azure można utworzyć bazy danych do obsługi środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="708f6-135">This is required in order to the Azure Functions Runtime to create a database to support the Runtime.</span></span>
    
    ![Środowisko Azure Functions środowiska uruchomieniowego Podgląd bazy danych konfiguracji][7]

1. <span data-ttu-id="708f6-137">Kliknij przycisk **poświadczenia** kartę.</span><span class="sxs-lookup"><span data-stu-id="708f6-137">Click the **Credentials** tab.</span></span>  <span data-ttu-id="708f6-138">Na tym ekranie należy utworzyć dwa nowe poświadczenia do użycia z udziałem plików do obsługi wszystkich funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="708f6-138">On this screen you must create two new credentials for use with a FileShare for hosting all your Azure Functions.</span></span>  <span data-ttu-id="708f6-139">**Określ nazwę użytkownika i hasło** kombinacji **właściciela udziału pliku** i **użytkownika udziału pliku** i kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="708f6-139">**Specify Username and Password** combinations for the **File Share Owner** and for the **File Share User** and click **Apply**.</span></span>

    ![Środowisko Azure Functions środowiska wykonawczego w wersji zapoznawczej poświadczenia][8]

1. <span data-ttu-id="708f6-141">Kliknij przycisk **udziału plików** kartę.</span><span class="sxs-lookup"><span data-stu-id="708f6-141">Click the **File Share** tab.</span></span>  <span data-ttu-id="708f6-142">Na tym ekranie Podaj szczegóły **lokalizację udziału pliku**.</span><span class="sxs-lookup"><span data-stu-id="708f6-142">In this screen you must specify the details of the **File Share location**.</span></span>  <span data-ttu-id="708f6-143">Można go utworzyć dla Ciebie lub można użyć istniejącego udziału plików i kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="708f6-143">This can be created for you or you can use an existing File Share and click **Apply**.</span></span>  <span data-ttu-id="708f6-144">Wybierz nową lokalizację udziału plików, należy określić katalog do użycia przez środowisko uruchomieniowe Functions Azure.</span><span class="sxs-lookup"><span data-stu-id="708f6-144">If you select a new File Share location, you must specify a directory for use by the Azure Functions Runtime.</span></span>
    
    ![Udział pliku podglądu środowiska uruchomieniowego usługę Azure Functions][9]

1. <span data-ttu-id="708f6-146">Kliknij przycisk **IIS** kartę.</span><span class="sxs-lookup"><span data-stu-id="708f6-146">Click the **IIS** tab.</span></span>  <span data-ttu-id="708f6-147">Ta karta przedstawia szczegóły witryn sieci Web w usługach IIS, który spowoduje utworzenie instalacji czasu wykonywania funkcji Azure.</span><span class="sxs-lookup"><span data-stu-id="708f6-147">This tab shows the details of the websites in IIS that the Azure Functions Runtime Installation will create.</span></span>  <span data-ttu-id="708f6-148">**Kliknij przycisk Zastosuj** do wykonania.</span><span class="sxs-lookup"><span data-stu-id="708f6-148">**Click Apply** to complete.</span></span>

    ![Środowisko Azure Functions środowiska wykonawczego w wersji zapoznawczej usług IIS][10]

1. <span data-ttu-id="708f6-150">Kliknij przycisk **usług** kartę.</span><span class="sxs-lookup"><span data-stu-id="708f6-150">Click the **Services** tab.</span></span>  <span data-ttu-id="708f6-151">Ta karta przedstawia stan usług w środowisku uruchomieniowym funkcji Azure instalacji.</span><span class="sxs-lookup"><span data-stu-id="708f6-151">This tab shows the status of the services in your Azure Functions Runtime installation.</span></span>  <span data-ttu-id="708f6-152">Jeśli po wykonaniu konfiguracji początkowej **usługi aktywacji hosta funkcji Azure** nie działa kliknij **Uruchom usługę**</span><span class="sxs-lookup"><span data-stu-id="708f6-152">If after initial configuration the **Azure Functions Host Activation Service** is not running click **Start Service**</span></span>

    ![Środowisko Azure Functions środowiska wykonawczego w wersji zapoznawczej Configruation pełną][11]

1. <span data-ttu-id="708f6-154">Na koniec przejdź do **portalu środowisko uruchomieniowe Functions Azure** jako`https://<machinename>/`</span><span class="sxs-lookup"><span data-stu-id="708f6-154">Finally browse to the **Azure Functions Runtime Portal** as `https://<machinename>/`</span></span>

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