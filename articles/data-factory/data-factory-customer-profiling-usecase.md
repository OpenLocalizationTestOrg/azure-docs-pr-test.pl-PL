---
title: Case - aaaUse profilowania klienta
description: "Dowiedz się, jak fabryki danych Azure jest używana toocreate opartego na danych przepływu pracy (potoku) tooprofile gier klientów."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: e07d55cf-8051-4203-9966-bdfa1035104b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 47f5e77242366c80cce2a2db65e3c696505b3e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-case---customer-profiling"></a>Przypadek użycia — profilowanie klientów
Fabryka danych Azure to jedna z wielu usług używanych hello tooimplement pakietu Cortana Intelligence Suite akceleratorów rozwiązania.  Aby uzyskać więcej informacji na temat Cortana Intelligence, odwiedź stronę [pakietu Cortana Intelligence Suite](http://www.microsoft.com/cortanaanalytics). W tym dokumencie opisano toohelp przypadków użycia prostego wprowadzenie zrozumienie, jak fabryki danych Azure można rozwiązywania typowych problemów analytics.

## <a name="scenario"></a>Scenariusz
Contoso to firma gier, która tworzy gry dla wielu platform: gier konsole, ręcznie posiadanych urządzeń i komputerów osobistych (komputery). Jak gry te odtwarzacze, duża ilość danych dziennika jest tworzony wzorce użycia, gier, stylu i preferencje użytkownika hello tekst hello ścieżki.  W połączeniu z demograficznych, regionalnych i danych produktu Contoso mogą wykonywać analizy tooguide ich dotyczących sposobu odtwarzacze tooenhance środowisko i adresować je do uaktualnienia i w grze zakupów. 

Celem firmy Contoso jest tooidentify możliwości up sprzedaje/sprzedaży na podstawie historii gier hello jego odtwarzaczy i Dodaj atrakcyjnych rozwoju firmy toodrive funkcje i zapewnić lepszą toocustomers środowisko. Dla tego przypadku użycia używamy firmy gier na przykład firma. Witaj firma chce toooptimize jego gry, w oparciu o zachowanie graczy. Te zasady stosowane tooany firma chce tooengage klientom wokół jego towarów i usług oraz ulepszanie środowiska swoich klientów.

W tym rozwiązaniu Contoso chce tooevaluate skuteczności hello marketing kampanii, która została ostatnio uruchomiona. Firma Microsoft rozpoczynać hello raw gier dzienniki, proces wzbogacić je z danymi używanie funkcji geolokalizacji, dołączyć go za pomocą anonsowanie danych referencyjnych i w końcu skopiuj je do bazy danych SQL Azure tooanalyze hello kampanii wpływ.

## <a name="deploy-solution"></a>Wdrażanie rozwiązania
Wszystkie potrzebne tooaccess i wypróbowywać ten przypadek użycia prostego jest [subskrypcji platformy Azure](https://azure.microsoft.com/pricing/free-trial/), [konta magazynu obiektów Blob Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)i [bazy danych SQL Azure](../sql-database/sql-database-get-started.md). Wdrażanie klienta hello profilowania potoku z hello **przykładowe potoki** kafelka na stronie głównej hello w fabryce danych.

1. Tworzenie fabryki danych lub Otwórz istniejącą fabrykę danych. Zobacz [kopiowanie danych z magazynu obiektów Blob tooSQL bazy danych przy użyciu fabryki danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla czynności toocreate fabryki danych.
2. W hello **FABRYKI danych** bloku dla fabryki danych hello, kliknij przycisk hello **przykładowe potoki** kafelka.

    ![Przykładowe potoki kafelka](./media/data-factory-samples/SamplePipelinesTile.png)
3. W hello **przykładowe potoki** bloku, kliknij przycisk hello **klienta profilowania** , które mają toodeploy.

    ![Przykład potoki bloku](./media/data-factory-samples/SampleTile.png)
4. Określ ustawienia konfiguracji dla przykładu hello. Na przykład z nazwy konta magazynu Azure i klucza, nazwy serwera Azure SQL bazy danych, identyfikator użytkownika i hasło.

    ![Przykładowe bloku](./media/data-factory-samples/SampleBlade.png)
5. Po wykonaniu Określanie ustawień konfiguracji hello, kliknij przycisk **Utwórz** toocreate/wdrażanie hello potoki próbki i usług/tabel połączonych używane przez hello potoków.
6. Zobacz hello stan wdrożenia na kafelku próbki hello kliknięty wcześniej hello **przykładowe potoki** bloku.

    ![Stan wdrożenia](./media/data-factory-samples/DeploymentStatus.png)
7. Po wyświetleniu hello **wdrożenie zakończyło się pomyślnie** wiadomość hello Kafelek dla przykładu hello, zamknij hello **przykładowe potoki** bloku.  
8. Na **FABRYKI danych** bloku, należy upewnić się, że połączone usługi, zestawy danych i potoki są dodany tooyour fabryki danych.  

    ![Blok Fabryka danych](./media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="solution-overview"></a>Omówienie rozwiązania
Ten przypadek użycia prostego można na przykład jak można użyć tooingest fabryki danych Azure, przygotować, przekształcania, analizowanie i publikować dane.

![Kompletny przepływ pracy](./media/data-factory-customer-profiling-usecase/EndToEndWorkflow.png)

Ilustracja przedstawia, jak potoki danych hello są wyświetlane w hello portalu Azure po ich wdrożeniu.

1. Witaj **PartitionGameLogsPipeline** odczytuje hello raw gier zdarzenia z magazynu obiektów blob i tworzy partycje oparte na rok, miesiąc i dzień.
2. Witaj **EnrichGameLogsPipeline** przyłączy partycjonowanej gier zdarzenia z danych referencyjnych kod: replikacji geograficznej — warstwa i poszerza hello danych mapowania IP adresów toohello odpowiedniego geolokalizacji.
3. Witaj **AnalyzeMarketingCampaignPipeline** potoku wykorzystuje hello wzbogacone danych i przetwarza je z hello anonsowanie danych toocreate hello ostateczne dane wyjściowe zawierający skuteczności kampanii marketingowych.

W tym przykładzie fabryki danych jest używane tooorchestrate działań, które kopiowania danych wejściowych, przekształcanie i przetwarzania danych hello i wyjściowych hello ostateczne dane tooan bazy danych SQL Azure.  Można również wizualizacji hello sieć danych, potoki, zarządzać nimi i monitorowanie ich stan z hello interfejsu użytkownika.

## <a name="benefits"></a>Korzyści
Optymalizacja ich analytics profilu użytkownika i dostosowanie jej cele biznesowe, gier firmy jest w stanie tooquickly wzorców użycia zbieranie i analizowanie hello skuteczności jego kampanii marketingowych.

