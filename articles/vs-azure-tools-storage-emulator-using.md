---
title: "aaaConfiguring i przy użyciu hello emulatora magazynu z programem Visual Studio | Dokumentacja firmy Microsoft"
description: "Konfigurowanie i używanie hello emulatora magazynu z programem Visual Studio"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: c8e7996f-6027-4762-806e-614b93131867
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/17/2017
ms.author: kraigb
ms.openlocfilehash: d590f21146c86bcb7bfa6b6164b92c6df5938d5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-and-using-hello-storage-emulator-with-visual-studio"></a>Konfigurowanie i używanie hello emulatora magazynu z programem Visual Studio
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Omówienie
środowisko projektowe zestawu Azure SDK Hello zawiera hello emulatora magazynu, narzędzia, która symuluje hello obiektów Blob, kolejki i tabeli magazynu usługi dostępnej na platformie Azure na komputerze deweloperskim lokalnego. W przypadku tworzenia usługi w chmurze, która jest stosowana w usług Azure storage hello lub zapisywanie dowolnej aplikacji zewnętrznych, że wywołania hello usług magazynu, należy przetestować Twój kod lokalnie hello emulatora magazynu. Hello Azure Tools dla programu Microsoft Visual Studio zintegrować Zarządzanie emulatora magazynu hello Visual Studio. Hello Azure Tools zainicjować bazy danych emulatora magazynu hello przy pierwszym użyciu, uruchamia hello usługi emulatora magazynu, po uruchomieniu lub debugowanie kodu w programie Visual Studio i zapewnia dostęp tylko do odczytu danych emulatora magazynu toohello za pośrednictwem hello Eksploratora usługi Storage platformy Azure.

Aby uzyskać szczegółowe informacje na powitania emulatora magazynu, takie jak wymagania systemowe i Konfiguracja niestandardowa, zobacz [hello Użyj emulatora magazynu Azure do programowania i testowania](storage/common/storage-use-emulator.md).

> [!NOTE]
> Istnieją pewne różnice w działaniu między Symulacja emulatora magazynu hello i hello usług magazynu platformy Azure. Zobacz [różnice między hello emulatora magazynu i usług magazynu Azure](storage/common/storage-use-emulator.md) w hello informacji na temat różnic określonych hello w dokumentacji zestawu SDK platformy Azure.
> 
> 

## <a name="configuring-a-connection-string-for-hello-storage-emulator"></a>Konfigurowanie parametrów połączenia dla emulatora magazynu hello
emulator magazynu hello tooaccess z kodu w ramach roli, można tooconfigure połączenia ciąg tego emulatora magazynu toohello punktów i które można później zmienione toopoint tooan kontem magazynu platformy Azure. Ciąg połączenia jest ustawienie konfiguracji, który może być odczytany roli użytkownika na konto magazynu tooa tooconnect środowiska wykonawczego. Aby uzyskać więcej informacji o tym, jak toocreate parametry połączenia, zobacz [hello Konfigurowanie aplikacji Azure](https://msdn.microsoft.com/library/azure/2da5d6ce-f74d-45a9-bf6b-b3a60c5ef74e#BK_SettingsPage).

> [!NOTE]
> Możesz powrócić konta emulatora magazynu toohello odwołania w kodzie za pomocą hello **DevelopmentStorageAccount** właściwości. Takie podejście działa prawidłowo, jeśli chcesz tooaccess hello emulatora magazynu w kodzie, ale jeśli planujesz toopublish Twojego tooAzure aplikacji, należy toocreate tooaccess ciąg połączenia konta magazynu Azure, a zmodyfikować toouse Twojego kod który Parametry połączenia przed opublikowaniem. Aby przełączyć między konto emulatora magazynu hello i konto magazynu platformy Azure często, ciąg połączenia upraszcza ten proces.
> 
> 

## <a name="initializing-and-running-hello-storage-emulator"></a>Inicjowanie i uruchomiony emulator magazynu hello
Można określić, że podczas uruchamiania lub debugowania w programie Visual Studio usługi Visual Studio automatycznie uruchamia hello emulatora magazynu. W Eksploratorze rozwiązań Otwórz menu skrótów hello Twojej **Azure** projekt i wybierz pozycję **właściwości**. Na powitania **programowanie** na karcie hello **uruchomić emulatora magazynu Azure** wybierz **True** (Jeśli nie jest już ustawiona wartość toothat).

powitania po raz pierwszy uruchamiania lub debugowania usługi z programu Visual Studio i emulatora magazynu hello uruchamia proces inicjowania. Ten proces rezerwuje portów lokalnych dla emulatora magazynu hello i tworzy bazę danych emulatora magazynu hello. Po zakończeniu tego procesu nie jest konieczne toorun ponownie chyba, że baza danych emulatora magazynu hello jest usuwany.

> [!NOTE]
> Począwszy od wersji czerwca 2012 hello hello narzędzi Azure, emulator magazynu hello działa domyślnie w SQL Express LocalDB. We wcześniejszych wersjach hello narzędzi Azure, emulator magazynu hello jest uruchamiana dla domyślnego wystąpienia programu SQL Express 2005 lub 2008, które należy zainstalować przed można zainstalować hello Azure SDK. Można również uruchomić emulatora magazynu hello względem nazwane wystąpienie programu SQL Express lub nazwanym lub domyślnego wystąpienia programu Microsoft SQL Server. Jeśli potrzebujesz tooconfigure hello magazynu emulatora toorun względem wystąpienia innych niż hello domyślnego wystąpienia, zobacz [hello Użyj emulatora magazynu Azure do programowania i testowania](storage/common/storage-use-emulator.md).
> 
> 

emulator magazynu Hello zawiera stan hello tooview interfejsu użytkownika usług magazynu lokalnego hello i toostart, Zatrzymaj, a ich ponownie. Po rozpoczęciu usługi emulatora magazynu hello można wyświetlić interfejsu użytkownika hello lub uruchomić lub zatrzymywania usługi hello, klikając prawym przyciskiem myszy ikonę w obszarze powiadomień powitania dla hello Microsoft Azure Emulator na pasku zadań systemu Windows hello.

## <a name="viewing-storage-emulator-data-in-server-explorer"></a>Wyświetlanie danych emulatora magazynu w Eksploratorze serwera
Hello węzła usługi Azure Storage w Eksploratorze serwera umożliwia tooview danych i zmiany ustawień dla obiekt blob i danych z tabeli kont magazynu, w tym hello emulatora magazynu. Zobacz [zasobów Zarządzanie magazynu obiektów Blob Azure przy użyciu Eksploratora usługi Storage (wersja zapoznawcza)](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs) Aby uzyskać więcej informacji.

