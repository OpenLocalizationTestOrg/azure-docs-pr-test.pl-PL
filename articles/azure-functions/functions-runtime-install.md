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
# <a name="install-hello-azure-functions-runtime-preview"></a>Zainstaluj hello Azure funkcje środowiska wykonawczego w wersji zapoznawczej

Jeśli chcesz tooinstall hello środowisko uruchomieniowe Functions Azure w wersji zapoznawczej, wykonaj następujące kroki:

1. Upewnij się, że komputer przekazuje hello minimalne wymagania
1. Pobierz hello [Azure funkcje środowiska wykonawczego w wersji zapoznawczej Instalatora](https://aka.ms/azafr). 
1. Zainstaluj hello środowisko uruchomieniowe Functions Azure w wersji zapoznawczej
1. Konfiguracja pełną hello hello środowisko uruchomieniowe Functions Azure w wersji zapoznawczej

## <a name="prerequisites"></a>Wymagania wstępne

Przed zainstalowaniem hello środowisko uruchomieniowe Functions Azure w wersji zapoznawczej, musi mieć następujące hello:

1. Maszynie z systemem Microsoft Windows Server 2016 lub Microsoft Windows 10 twórców aktualizacji (Professional lub Enterprise Edition).
1. Wystąpienie programu SQL Server działających w sieci.  Minimalna wersja wymaganie to SQL Server Express.

## <a name="install-hello-azure-functions-runtime-preview"></a>Zainstaluj hello Azure funkcje środowiska wykonawczego w wersji zapoznawczej

Instalatora w wersji zapoznawczej środowisko uruchomieniowe Functions Azure Hello przeprowadzi Cię przez instalację hello hello środowisko uruchomieniowe Functions Azure w wersji zapoznawczej zarządzania i roli proces roboczy.  Witaj tooinstall możliwości zarządzania i roli proces roboczy na powitania jest tym samym komputerze.  Jednak podczas dodawania więcej funkcji, należy wdrożyć jedną rolę procesu roboczego w stanie tooscale toobe dodatkowych maszyn funkcji na wielu pracowników.

## <a name="install-hello-management-and-worker-role-on-hello-same-machine"></a>Zainstaluj hello zarządzania i roli proces roboczy na powitania tym samym komputerze

1. Uruchom hello Azure funkcje środowiska wykonawczego w wersji zapoznawczej Instalatora.

    ![Środowisko Azure Functions środowiska wykonawczego w wersji zapoznawczej Instalatora][1]

1. **Kliknij przycisk Dalej** zaliczki poza hello pierwszego etapu hello Instalatora
1. Po zapoznaniu się z warunkami hello hello **umowy licencyjnej**, **hello pole wyboru** tooaccept hello warunki i **kliknij przycisk Dalej** tooadvance.
1. Teraz wybierz hello ról ma tooinstall na tym komputerze **funkcje zarządzania roli** i/lub **roli procesu roboczego funkcji** i **, kliknij przycisk Dalej**

    ![Azure Functions środowiska wykonawczego w wersji zapoznawczej Instalator — Wybór roli][3]

    > [!NOTE]
    > Można zainstalować hello **roli procesu roboczego funkcji** na inne toodo maszyny, wykonaj te instrukcje i wybierz tylko **roli procesu roboczego funkcji** w Instalatorze hello.

1. **Kliknij przycisk Dalej** toohave hello **Azure funkcji środowiska uruchomieniowego Instalator** zainstalować na komputerze.
1. Po pełną hello Instalator uruchomi hello **narzędzia do konfiguracji środowiska uruchomieniowego funkcji Azure**.

    ![Azure Functions środowiska wykonawczego w wersji zapoznawczej Instalatora pełną][5]

    > [!NOTE]
    > Jeśli instalujesz na **systemu Windows 10** i hello **kontenera** funkcji nie został wcześniej włączony, hello **środowisko uruchomieniowe Functions Azure** Instalator monituje tooreboot Zainstaluj hello toocomplete Twojego komputera.

## <a name="configure-hello-azure-functions-runtime"></a>Skonfiguruj hello środowisko uruchomieniowe Functions Azure

Witaj toocomplete środowisko uruchomieniowe Functions Azure instalacji należy wykonać hello konfiguracji.

1. Witaj **narzędzie konfiguracji środowiska wykonawczego funkcji Azure** pokazuje role są zainstalowane na tym komputerze.

    ![Środowisko Azure Functions narzędzia do konfiguracji podglądu środowiska wykonawczego][6]

1. Kliknij przycisk hello **bazy danych** wprowadź hello **szczegóły połączenia dla wystąpienia programu SQL Server** i **kliknij przycisk Zastosuj**.  Jest to wymagane w kolejności toohello toocreate środowisko uruchomieniowe Functions Azure hello toosupport bazy danych środowiska wykonawczego.
    
    ![Środowisko Azure Functions środowiska uruchomieniowego Podgląd bazy danych konfiguracji][7]

1. Kliknij przycisk hello **poświadczenia** kartę.  Na tym ekranie należy utworzyć dwa nowe poświadczenia do użycia z udziałem plików do obsługi wszystkich funkcji platformy Azure.  **Określ nazwę użytkownika i hasło** kombinacji hello **właściciela udziału pliku** i hello **użytkownika udziału pliku** i kliknij przycisk **Zastosuj**.

    ![Środowisko Azure Functions środowiska wykonawczego w wersji zapoznawczej poświadczenia][8]

1. Kliknij przycisk hello **udziału plików** kartę.  Na tym ekranie Podaj szczegóły hello hello **lokalizację udziału pliku**.  Można go utworzyć dla Ciebie lub można użyć istniejącego udziału plików i kliknij przycisk **Zastosuj**.  W przypadku wybrania nowej lokalizacji udziału plików, należy określić katalog dla przez hello środowisko uruchomieniowe Functions Azure.
    
    ![Udział pliku podglądu środowiska uruchomieniowego usługę Azure Functions][9]

1. Kliknij przycisk hello **IIS** kartę.  Ta karta przedstawia szczegóły hello hello witryn sieci Web w usługach IIS tego powitalne Azure funkcji środowiska uruchomieniowego instalacji zostanie utworzona.  **Kliknij przycisk Zastosuj** toocomplete.

    ![Środowisko Azure Functions środowiska wykonawczego w wersji zapoznawczej usług IIS][10]

1. Kliknij przycisk hello **usług** kartę.  Ta karta przedstawia hello stanu usług hello w środowisku uruchomieniowym funkcji Azure instalacji.  Jeżeli po początkowej konfiguracji hello **usługi aktywacji hosta funkcji Azure** nie działa kliknij **Uruchom usługę**

    ![Środowisko Azure Functions środowiska wykonawczego w wersji zapoznawczej Configruation pełną][11]

1. Na koniec Przeglądaj toohello **portalu środowisko uruchomieniowe Functions Azure** jako`https://<machinename>/`

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