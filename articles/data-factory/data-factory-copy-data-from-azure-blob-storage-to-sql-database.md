---
title: "aaaCopy danych z magazynu obiektów Blob tooSQL bazy danych - Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek pokazuje, jak toouse działanie kopiowania w fabryce danych Azure potoku toocopy danych z bazy danych tooSQL magazynu obiektów Blob."
keywords: "Obiekt blob sql magazynu obiektów blob, kopiowanie danych"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e4035060-93bf-4e8d-bf35-35e2d15c51e0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: a2c3fb8a4ddd63b0b6b3e75903b7a7eaf188fda4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-copy-data-from-blob-storage-toosql-database-using-data-factory"></a>Samouczek: Kopiowanie danych z magazynu obiektów Blob tooSQL bazy danych przy użyciu fabryki danych
> [!div class="op_single_selector"]
> * [Przegląd i wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Kreator kopiowania](data-factory-copy-data-wizard-tutorial.md)
> * [Witryna Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Program Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [Program PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Szablon usługi Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [Interfejs API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [Interfejs API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)

W tym samouczku utworzysz fabryki danych danymi toocopy potoku z bazy danych tooSQL magazynu obiektów Blob.

Witaj działanie kopiowania wykonuje hello przenoszenia danych w fabryce danych Azure. Jest obsługiwane przez globalnie dostępną usługę, która może kopiować dane między różnymi magazynami danych w sposób bezpieczny, niezawodny i skalowalny. Zobacz [działań przepływu danych](data-factory-data-movement-activities.md) artykułu szczegółowe informacje o hello działanie kopiowania.  

> [!NOTE]
> Szczegółowe omówienie hello usługi fabryka danych, zobacz hello [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) artykułu.
>
>

## <a name="prerequisites-for-hello-tutorial"></a>Wymagania wstępne dotyczące samouczka hello
Przed rozpoczęciem tego samouczka, musi mieć hello następujące wymagania wstępne:

* **Subskrypcja platformy Azure**.  Jeśli nie masz subskrypcji, możesz utworzyć konto bezpłatnej wersji próbnej w zaledwie kilka minut. Zobacz hello [bezpłatnej wersji próbnej](http://azure.microsoft.com/pricing/free-trial/) artykułu, aby uzyskać szczegółowe informacje.
* **Konto magazynu Azure**. Użyj magazynu obiektów blob hello **źródła** magazynu danych, w tym samouczku. Jeśli nie masz konta magazynu platformy Azure, zobacz hello [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) artykuł, aby toocreate kroki, jeden.
* **Usługa Azure SQL Database**. Użyj bazy danych Azure SQL jako **docelowego** magazynu danych, w tym samouczku. Jeśli nie masz bazy danych Azure SQL można używać w samouczku hello, zobacz [jak toocreate i skonfiguruj bazę danych SQL Azure](../sql-database/sql-database-get-started.md) toocreate jeden.
* **2014 programu SQL Server 2012 lub Visual Studio 2013**. Używasz programu SQL Server Management Studio lub Visual Studio toocreate przykładowej bazy danych i dane wynikowe hello tooview hello bazy danych.  

## <a name="collect-blob-storage-account-name-and-key"></a>Zbierać nazwy konta magazynu obiektów blob i kluczy
Musisz mieć konto hello toodo konta nazwy i klucza konta magazynu Azure, w tym samouczku. Należy zanotować **nazwa konta** i **klucz konta** dla konta magazynu Azure.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).
2. Kliknij przycisk **więcej usług** na powitania lewego menu i wybierz **kont magazynu**.

    ![Przeglądaj - kont magazynu](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. W hello **kont magazynu** bloku, wybierz hello **konto magazynu Azure** mają toouse w tym samouczku.
4. Wybierz **klucze dostępu** łącze w obszarze **ustawienia**.
5. Kliknij przycisk **kopiowania** (obraz) obok przycisku zbyt**nazwy konta magazynu** tekst pola i Zapisz/wklej go innym (na przykład: w pliku tekstowym).
6. Powtórz poprzednie toocopy krok hello lub zanotuj hello **klucz1**.

    ![Klucz dostępu do magazynu](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. Zamknij wszystkie bloki hello klikając **X**.

## <a name="collect-sql-server-database-user-names"></a>Zbieraj programu SQL server, bazy danych, nazwy użytkowników
Należy hello nazwy serwera Azure SQL, bazy danych i toodo użytkownika w tym samouczku. Zanotuj nazwy **serwera**, **bazy danych**, i **użytkownika** bazy danych Azure SQL.

1. W hello **portalu Azure**, kliknij przycisk **więcej usług** na powitania po lewej stronie i wybierz pozycję **baz danych SQL**.
2. W hello **bloku bazy danych SQL**, wybierz pozycję hello **bazy danych** mają toouse w tym samouczku. Zanotuj hello **Nazwa bazy danych**.  
3. W hello **bazy danych SQL** bloku, kliknij przycisk **właściwości** w obszarze **ustawienia**.
4. Zanotuj wartości hello **nazwy serwera** i **identyfikator logowania administratora serwera**.
5. Zamknij wszystkie bloki hello klikając **X**.

## <a name="allow-azure-services-tooaccess-sql-server"></a>Zezwalaj usługom platformy Azure tooaccess programu SQL server
Upewnij się, że **dostęp do usług tooAzure** ustawienie włączenia **ON** serwera Azure SQL, że hello usługi fabryka danych można uzyskiwać dostęp do serwera Azure SQL. tooverify i włącz to ustawienie hello następujące kroki:

1. Kliknij przycisk **więcej usług** koncentratora na powitania po lewej i kliknij przycisk **serwerów SQL**.
2. Wybierz swój serwer, a następnie kliknij przycisk **Zapora** w obszarze **USTAWIENIA**.
3. W hello **ustawienia zapory** bloku, kliknij przycisk **ON** dla **dostęp do usług tooAzure**.
4. Zamknij wszystkie bloki hello klikając **X**.

## <a name="prepare-blob-storage-and-sql-database"></a>Przygotowanie magazynu obiektów Blob i bazy danych SQL
Teraz Przygotuj magazyn obiektów blob platformy Azure i bazy danych Azure SQL hello samouczek, wykonując następujące kroki hello:  

1. Uruchom program Notatnik. Skopiuj następujące tekst hello i zapisz go jako **emp.txt** za**C:\ADFGetStarted** folderu na dysku twardym.

    ```
    John, Doe
    Jane, Doe
    ```
2. Użyj narzędzia takiego jak [Eksploratora usługi Storage Azure](http://storageexplorer.com/) toocreate hello **adftutorial** hello kontenera i tooupload **emp.txt** kontenera toohello plików.

    ![Eksplorator usługi Storage platformy Azure. Kopiowanie danych z bazy danych tooSQL magazynu obiektów Blob](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. Użyj powitania po hello toocreate skryptu SQL **pustych elementów** tabeli w bazie danych SQL Azure.  

    ```SQL
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

    **Jeśli masz programu SQL Server 2012/2014 zainstalowanej na komputerze:** postępuj zgodnie z instrukcjami [Zarządzanie bazą danych SQL Azure przy użyciu programu SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooyour tooconnect Azure SQL server i uruchom hello skryptu SQL. W tym artykule wykorzystano hello [klasycznego portalu Azure](http://manage.windowsazure.com), nie hello [nowego portalu Azure](https://portal.azure.com), tooconfigure zapory dla serwera Azure SQL.

    Jeśli klient nie jest dozwolona tooaccess hello Azure SQL server, należy tooconfigure zapory dla programu access tooallow serwera Azure SQL z komputera (adres IP). Zobacz [w tym artykule](../sql-database/sql-database-configure-firewall-settings.md) kroki tooconfigure hello zapory serwera Azure SQL.

## <a name="create-a-data-factory"></a>Tworzenie fabryki danych
Witaj wymagań wstępnych została ukończona. Można utworzyć fabryki danych przy użyciu jednej z hello następujące sposoby. Kliknij jedną z opcji hello na liście rozwijanej hello góry hello lub hello samouczka hello tooperform łącza.     

* [Kreator kopiowania](data-factory-copy-data-wizard-tutorial.md)
* [Witryna Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [Program Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [Program PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
* [Szablon usługi Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [Interfejs API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
* [Interfejs API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> Witaj potoku danych w tym samouczku kopiuje dane z magazynu danych źródła danych magazynu tooa docelowego. Przekształca dane wyjściowe tooproduce danych wejściowych. Samouczek na temat danych tootransform przy użyciu fabryki danych Azure, zobacz [samouczek: Tworzenie pierwszego potoku dane tootransform przy użyciu klastra usługi Hadoop](data-factory-build-your-first-pipeline.md).
> 
> Powiązane z dwóch działań (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań. Szczegółowe informacje znajdują się w artykule [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) (Planowanie i wykonywanie w usłudze Data Factory). 
