---
title: "aaaUse usługi Automatyzacja Azure tootrigger zadanie | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse usługi Automatyzacja Azure służącą do wyzwalania zadania Menedżer StorSimple danych (w podglądzie prywatnym)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 0d9d6e5e6d52ed27ca759ed7e949b5f5dfd319c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-automation-tootrigger-a-job-private-preview"></a>Użyj usługi Automatyzacja Azure tootrigger zadania (podglądzie prywatnym)

W tym artykule opisano sposób toouse usługi Automatyzacja Azure tootrigger zadania Menedżer StorSimple danych.

## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem upewnij się, że masz:

*   Zainstalowany program Azure Powershell. [Pobieranie programu Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
*   Konfiguracja ustawień tooinitialize hello transformacji danych zadania (instrukcje tooobtain te ustawienia są uwzględnione w tym miejscu).
*   Definicji zadania, który został poprawnie skonfigurowany w zasobie danych hybrydowych w grupie zasobów.
*   Pobierz `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) plik z repozytorium github hello.
*   Pobierz `Get-ConfigurationParams.ps1` [skryptu](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) z repozytorium github hello.
*   Pobierz `Trigger-DataTransformation-Job.ps1` [skryptu](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) z repozytorium github hello.

## <a name="step-by-step"></a>Krok po kroku

### <a name="get-azure-active-directory-permissions-for-hello-automation-job-toorun-hello-job-definition"></a>Uzyskać uprawnienia w usłudze Azure Active Directory dla definicji zadania hello toorun hello automatyzacji zadań

1. tooretrieve hello parametry konfiguracji usługi Active Directory, hello następujące kroki:

    1. Otwórz program Windows PowerShell w komputerze lokalnym. Upewnij się, że [programu Azure PowerShell](https://azure.microsoft.com/downloads/) jest zainstalowany.
    1. Uruchom hello `Get-ConfigurationParams.ps1` skryptu (w folderze hello pobrane powyżej). Wpisz następujące polecenie w oknie programu PowerShell hello hello:

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        Witaj ActiveDirectoryKey to hasło, które można użyć później. Wprowadź hasło wybranych przez użytkownika. Nazwa aplikacji może być dowolnym ciągiem.

2. Ten skrypt generuje hello następujące wartości, które mają być używane podczas wyzwalania elementu runbook automatyzacji hello. Zanotuj te wartości.

    - Identyfikator klienta
    - Identyfikator dzierżawy
    - Kluczy Active Directory (taki sam, jak hello jedną wprowadzony powyżej)
    - Identyfikator subskrypcji

### <a name="set-up-hello-automation-account"></a>Konfigurowanie hello konta automatyzacji

1. Zaloguj się na tooAzure i otwórz konto automatyzacji.
2. Kliknij przycisk **zasoby** kafelka tooopen hello Lista zasobów.
3. Kliknij przycisk **modułów** kafelka tooopen hello listy modułów.
4. Kliknij przycisk **+ Dodaj moduł** bloku modułu Dodaj przycisk i hello jest uruchamiana.

    ![Ustawienia konta automatyzacji](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. Po wybraniu hello `DataTransformationApp.zip` plików z komputera lokalnego, kliknij **OK** tooimport hello modułu.

   Automatyzacja Azure importuje konta tooyour modułu, umożliwia wyodrębnianie metadanych dotyczących hello modułu. Ta operacja może potrwać kilka minut.

   ![Ustawienia konta automatyzacji](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. Zostanie wyświetlone powiadomienie tego modułu hello jest wdrażany i kolejne powiadomienie po zakończeniu procesu hello.  Możesz również sprawdzić stan hello **modułów** kafelka.

### <a name="tooimport-hello-runbook-that-triggers-hello-job-definition"></a>tooimport hello runbook, które wyzwala hello definicji zadania

1. Otwórz hello portalu Azure, Twoje konto usługi Automatyzacja.
2. Kliknij przycisk **elementów Runbook** kafelka tooopen hello listy elementów runbook.
3. Kliknij przycisk **+ Dodaj element runbook** , a następnie **importowanie istniejącego elementu runbook**.

   ![Importuj istniejący element runbook](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. Kliknij przycisk **pliku Runbook** i wybierz hello pliku tooimport `Trigger-DataTransformation-Job.ps1`.
5. Kliknij przycisk **Utwórz** tooimport hello runbook. liście hello elementów runbook dla konta automatyzacji hello pojawi się nowy element runbook Hello.
7. Kliknij przycisk **wyzwalacza DataTransformation zadania** runbook, a następnie kliknij przycisk **Edytuj**.
8. Kliknij przycisk **publikowania** , a następnie **tak** po wyświetleniu monitu o potwierdzenie.


### <a name="toorun-hello-runbook"></a>toorun hello elementu runbook:
1. Otwórz hello portalu Azure, Twoje konto usługi Automatyzacja.
2. Kliknij przycisk hello **elementów Runbook** kafelka tooopen hello listy elementów runbook.
3. Kliknij przycisk **wyzwalacza DataTransformation zadania**.
4. Kliknij przycisk **Start** toostart hello runbook.

   ![Uruchamianie elementu Runbook](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. W hello **uruchomić elementu runbook** bloku, wprowadź wszystkie parametry hello. Kliknij przycisk **OK** toosubmit hello transformacji danych zadania.

   ![Uruchamianie elementu Runbook](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a>Następne kroki

[Użyj interfejsu użytkownika Menedżera danych StorSimple tootransform danych](storsimple-data-manager-ui.md).
