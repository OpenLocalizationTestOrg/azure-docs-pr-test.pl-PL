---
title: "aaaLoad danych do usługi Azure SQL Data Warehouse — fabryki danych | Dokumentacja firmy Microsoft"
description: "W tym samouczku ładuje dane do usługi Azure SQL Data Warehouse przy użyciu fabryki danych Azure i korzysta z bazy danych programu SQL Server jako hello źródła danych."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse;azure-data-factory
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: loading
ms.date: 02/08/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 471871d3ee00ab34cc84bb63fbd13a323d14c2b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a>Ładowanie danych do usługi SQL Data Warehouse z fabryką danych

Fabryka danych Azure tooload danych można użyć do magazynu danych SQL Azure za pomocą dowolnego hello [obsługiwane magazyny danych źródła](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats). Na przykład można ładowania danych z bazy danych Azure SQL lub z bazą danych programu Oracle do magazynu danych SQL przy użyciu fabryki danych. Samouczek, w tym artykule przedstawiono sposób tooload danych z lokalnego serwera SQL bazy danych do magazynu danych SQL.

**Szacowanie czasu**: tego samouczka trwa około 10 – 15 minut toocomplete, po spełnieniu wymagań wstępnych hello.

## <a name="prerequisites"></a>Wymagania wstępne

- Należy **bazy danych programu SQL Server** z tabel zawierających dane hello toobe kopiowane toohello usługi SQL data warehouse.  

- Należy online **SQL Data Warehouse**. Jeśli nie masz już magazyn danych, Dowiedz się, jak za[Utwórz magazyn danych SQL Azure](sql-data-warehouse-get-started-provision.md).

- Należy **konta magazynu Azure**. Jeśli nie masz już konto magazynu, Dowiedz się, jak za[Utwórz konto magazynu](../storage/common/storage-create-storage-account.md). Aby uzyskać najlepszą wydajność, Znajdź konto magazynu hello i hello magazynu danych w hello sam region platformy Azure.

## <a name="configure-a-data-factory"></a>Skonfiguruj fabryki danych
1. Zaloguj się za toohello [portalu Azure][].
2. Znajdź magazynu danych i kliknij przycisk tooopen go.
3. W głównym bloku hello kliknij **danych obciążenia** > **fabryki danych Azure**.

    ![Uruchom Kreatora ładowanie danych](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. Jeśli nie ma fabryki danych w ramach subskrypcji platformy Azure, zobacz **nowa fabryka danych** okno dialogowe w osobnej karcie hello przeglądarki. Wypełnij hello wymagane informacje, a następnie kliknij przycisk **Utwórz**. Po utworzeniu fabryki danych hello hello **nowa fabryka danych** okno dialogowe zostanie zamknięte i zostanie wyświetlony hello **fabryki danych wybierz** okno dialogowe.

    Jeśli masz co najmniej jeden fabryki danych znajdujących się w hello subskrypcji platformy Azure, zobacz hello **fabryki danych wybierz** okno dialogowe. W tym oknie można wybrać istniejącą fabrykę danych lub kliknij przycisk **Utwórz nowy fabryki danych** toocreate nowy.

    ![Konfigurowanie usługi fabryka danych](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. W hello **fabryki danych wybierz** okno dialogowe, hello **ładowanie danych** opcja jest domyślnie zaznaczona. Kliknij przycisk **dalej** toostart Tworzenie danych podczas ładowania zadania.

## <a name="configure-hello-data-factory-properties"></a>Skonfiguruj właściwości fabryki danych hello
Po utworzeniu fabryki danych hello następnym krokiem jest danych hello tooconfigure ładowania harmonogramu.

1. Aby uzyskać **Nazwa zadania**, wprowadź **DWLoadData fromSQLServer**.
2. Użyj domyślnej hello **uruchom raz teraz** kliknij przycisk **dalej**.

    ![Skonfiguruj harmonogram obciążenia](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-hello-source-data-store-and-gateway"></a>Konfigurowanie magazynu danych źródła hello i bramy
Teraz nakaż fabryki danych o hello: lokalną bazą danych programu SQL Server z którego mają zostać tooload danych.

1. Wybierz **programu SQL Server** z hello obsługiwane źródła danych przechowywane w katalogu, a następnie kliknij przycisk **dalej**.

    ![Wybierz źródło programu SQL Server](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. A **Określ hello lokalną bazą danych programu SQL Server** zostanie wyświetlone okno dialogowe. Witaj najpierw **nazwa połączenia** pole jest wypełniane automatycznie. drugie pole Hello poprosi o podanie nazwy hello hello **bramy**. Jeśli korzystasz z istniejącą fabrykę danych, która ma już bramy, można użyć ponownie hello bramy, wybierając ją z listy rozwijanej hello. Kliknij przycisk hello **Tworzenie bramy** link toocreate brama zarządzania danymi.  

    > [!NOTE]
    > Jeśli Magazyn hello źródła danych działa lokalnie lub w maszynie wirtualnej platformy Azure IaaS, jest wymagana brama zarządzania danymi. Brama ma relację 1-1 z fabryką danych. Nie można użyć z innego fabryki danych, ale mogą służyć przez wiele danych podczas ładowania zadania związane z w hello tej samej fabryki danych. Brama może być magazyny danych toomultiple tooconnect używanych podczas uruchamiania zadania ładowania danych.
    >
    > Aby uzyskać szczegółowe informacje na temat bramy hello, zobacz [brama zarządzania danymi](../data-factory/data-factory-data-management-gateway.md) artykułu.

3. A **Tworzenie bramy** zostanie wyświetlone okno dialogowe. Wprowadź nazwę, **GatewayForDWLoading**i kliknij przycisk **Utwórz**.

4. A **konfigurowania bramy** zostanie wyświetlone okno dialogowe. Kliknij przycisk **uruchamiania instalacji ekspresowej na tym komputerze** tooautomatically pobierania, zainstaluj i zarejestruj bramę zarządzania danymi na bieżącym komputerze. Witaj postęp jest wyświetlany w oknie podręcznym. Jeśli maszyna hello nie można połączyć toohello magazynu danych, możesz ręcznie [pobieranie i instalowanie bramy hello](https://www.microsoft.com/download/details.aspx?id=39717) na komputerze, na którym można połączyć toohello danych przechowywania, a następnie użyj hello tooregister klucza.
    > [!NOTE]
    > Instalacja ekspresowa Hello natywnie współpracuje z Microsoft Edge i przeglądarki Internet Explorer. Jeśli używasz przeglądarki Google Chrome, należy najpierw zainstalować rozszerzenie ClickOnce hello ze sklepu Chrome web store.

    ![Uruchamianie instalacji ekspresowej](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. Poczekaj, aż toocomplete instalacji bramy hello. Po hello bramy zostało pomyślnie zarejestrowane i jest w trybie online, zamyka okno podręczne hello i nową bramę hello jest wyświetlana w polu Brama hello. Następnie wypełnij hello rest wymagane pola w następujący sposób, kliknij przycisk **dalej**.
    - **Nazwa serwera**: Nazwa hello lokalnego programu SQL Server.
    - **Nazwa bazy danych**: baza danych SQL Server.
    - **Poświadczeń szyfrowania**: Użyj domyślnej hello "przez przeglądarkę sieci web".
    - **Typ uwierzytelniania**: Wybierz typ hello używasz uwierzytelniania.
    - **Nazwa użytkownika** i **hasło**: Wprowadź hello nazwy użytkownika i hasła dla użytkownika, który ma uprawnienia toocopy hello danych.

    ![Uruchamianie instalacji ekspresowej](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. Witaj następnym krokiem jest toochoose hello tabele, z których dane hello toocopy. Tabele hello można filtrować przy użyciu słów kluczowych. I można wyświetlić podgląd danych i tabeli schematu hello w hello dolny panel. Po zakończeniu wybór, kliknij przycisk **dalej**.

    ![Wybór tabel](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-hello-destination-your-sql-data-warehouse"></a>Skonfigurowane miejsce docelowe hello, Magazyn danych SQL

Teraz nakaż fabryki danych o hello informacji o lokalizacji docelowej.

1. Informacje o połączeniu magazyn danych SQL jest wypełniane automatycznie. Wprowadź hasło hello hello nazwy użytkownika. i kliknij przycisk **dalej**.

    ![Skonfigurowane miejsce docelowe](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. Mapowania tabeli inteligentnego wyświetlany jest mapowany na podstawie tabeli nazw tabel toodestination źródeł. Jeśli hello tabela nie istnieje w docelowym hello, domyślnie ADF utworzy po jednym z hello samej nazwie (dotyczy to tooSQL serwera lub bazy danych SQL Azure jako źródła). Możesz również toomap tooan istniejącej tabeli. Przejrzyj i kliknij przycisk **dalej**.

    ![Mapowanie tabel](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. Przejrzyj hello mapowanie schematu i odszukaj ostrzeżeń i komunikatów o błędach. Mapowanie inteligentnego jest oparta na nazwę kolumny. W przypadku konwersji typu nieobsługiwanych danych między kolumną hello źródłowym i docelowym, zostanie wyświetlony komunikat o błędzie obok odpowiedniej tabeli hello. Jeśli wybierzesz toolet fabryka danych automatycznie Tworzenie tabel hello, konwersja typu danych właściwe może się tak zdarzyć w razie potrzeby toofix hello niezgodności między magazynami źródłowym i docelowym.

    ![Mapowanie schematu](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. Kliknij przycisk **Dalej**.

## <a name="configure-hello-performance-settings"></a>Skonfigurowanie ustawień wydajności hello
W konfiguracji wydajności hello, skonfiguruj konta magazynu platformy Azure używana do przemieszczania danych hello przed załadowaniem do usługi SQL Data Warehouse performantly przy użyciu [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly). Po wykonaniu czynności kopiowania hello hello tymczasowe dane w magazynie zostaną wyczyszczone automatycznie.

Wybierz istniejące konto magazynu Azure, a następnie kliknij przycisk **dalej**.

![Skonfiguruj tymczasowych obiektów blob](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-hello-pipeline"></a>Przejrzyj podsumowanie i wdrażanie hello potoku

Należy przejrzeć konfigurację hello i kliknij przycisk **Zakończ** przycisk toodeploy hello potoku.

![Wdrażanie usługi fabryka danych](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a>Trwa ładowanie danych monitora

Można wyświetlić postęp wdrażania hello i powoduje hello **wdrożenia** strony.

1. Po ukończeniu wdrażania hello, kliknij łącze hello **kliknij tutaj potoku kopiowania toomonitor** danych toomonitor postępu ładowania.

    ![Monitorowanie potoku](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. nowo utworzona Hello **DWLoadData fromSQLServer** potoku podczas ładowania danych zostanie automatycznie wybrany z lewym hello **Eksploratora zasobów**.

    ![Widok procesu](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. Kliknij przycisk potokiem hello w środku hello hello toosee panelu szczegółowy stan dla każdej tabeli, która mapuje tooan działania.

    ![Widok tabeli działania](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. Kliknij dalej do działania i zostaną wyświetlone dane hello ładowania szczegółów prawym panelu hello, takich jak rozmiar danych, wiersze, przepływności, itp.

    ![Wyświetl szczegóły działania tabeli](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. toolaunch tego monitorowania widoku nowsze, przejdź do pozycji tooyour magazyn danych SQL, kliknij przycisk **danych obciążenia > fabryki danych Azure**, wybierz fabryką i wybierz **monitorowanie istniejących podczas ładowania zadania**.

## <a name="next-steps"></a>Następne kroki

toomigrate Twojego tooSQL bazy danych magazynu danych, zobacz [Omówienie migracji](sql-data-warehouse-overview-migrate.md).

toolearn więcej informacji na temat fabryki danych Azure i jego możliwości przepływu danych, zobacz następujące artykuły hello:

- [Wprowadzenie tooAzure fabryki danych](../data-factory/data-factory-introduction.md)
- [Przenoszenie danych za pomocą działania kopiowania](../data-factory/data-factory-data-movement-activities.md)
- [Przenieś tooand danych z magazynu danych SQL Azure przy użyciu fabryki danych Azure](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

tooexplore danych w usłudze SQL Data Warehouse, zobacz hello następujące artykuły:

- [Połączenie tooSQL magazynu danych z programu Visual Studio i narzędzi SSDT](sql-data-warehouse-query-visual-studio.md)
- [Visual danych za pomocą usługi Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).

<!-- Azure references -->
[portalu Azure]: https://portal.azure.com
