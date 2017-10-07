---
title: "Samouczek: Tworzenie potoku przy użyciu Kreatora kopiowania | Microsoft Docs"
description: "W tym samouczku utworzysz potok fabryki danych Azure z działaniem kopiowania za pomocą hello obsługiwane przez fabrykę danych Kreatora kopiowania"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b87afb8e-53b7-4e1b-905b-0343dd096198
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 567b89e7a54c245c134cd0674690e6f3499b46d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a>Samouczek: tworzenie potoku za pomocą działania kopiowania przy użyciu Kreatora kopiowania usługi Fabryka danych
> [!div class="op_single_selector"]
> * [Przegląd i wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Kreator kopiowania](data-factory-copy-data-wizard-tutorial.md)
> * [Witryna Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Program Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [Program PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Szablon usługi Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [Interfejs API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [Interfejs API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)

W tym samouczku przedstawiono sposób toouse hello **kreatora kopiowania** toocopy dane z bazy danych Azure SQL tooan magazynu obiektów blob platformy Azure. 

Witaj fabryki danych Azure **kreatora kopiowania** pozwala tooquickly utworzyć potok danych, które kopiuje dane z magazynu danych obsługiwane źródła danych magazynu tooa obsługiwane docelowego. Dlatego zaleca się, użyj Kreatora hello jako pierwszy toocreate krok potoku próbki dla danego scenariusza przepływu danych. Aby zapoznać się z listą magazynów danych obsługiwanych jako źródła i lokalizacje docelowe, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats).  

Ten samouczek pokazuje, jak toocreate fabryki danych Azure, hello uruchamiania kreatora kopiowania, przejdź na kolejnych kroków tooprovide szczegóły danego scenariusza wprowadzanie/przepływu danych. Po zakończeniu czynności w Kreatorze hello hello Kreator automatycznie tworzy potoku z toocopy działanie kopiowania danych z bazy danych Azure SQL tooan magazynu obiektów blob platformy Azure. Więcej informacji o Działaniu kopiowania znajduje się w temacie [Działania związane z przenoszeniem danych](data-factory-data-movement-activities.md).

## <a name="prerequisites"></a>Wymagania wstępne
Wymagania wstępne wymienione w hello ukończyć [— samouczek Przegląd](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artykuł przed wykonaniem tego samouczka.

## <a name="create-data-factory"></a>Tworzenie fabryki danych
W tym kroku użyjesz hello Azure toocreate portalu fabryki danych Azure o nazwie **ADFTutorialDataFactory**.

1. Zaloguj się za[portalu Azure](https://portal.azure.com).
2. Kliknij przycisk **+ nowy** hello lewym górnym rogu kliknij **dane i analiza**i kliknij przycisk **fabryki danych**. 
   
   ![Nowy-> Fabryka danych](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. W hello **nowa fabryka danych** bloku:
   
   1. Wprowadź **ADFTutorialDataFactory** dla hello **nazwa**.
       Nazwa fabryki danych Azure hello Hello musi być globalnie unikatowe. Jeśli wystąpi błąd hello: `Data factory name “ADFTutorialDataFactory” is not available`, Zmień nazwę hello hello fabryki danych (na przykład yournameADFTutorialDataFactoryYYYYMMDD) i spróbuj ponownie utworzyć. Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.  
      
       ![Nazwa fabryki danych jest niedostępna](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. Wybierz swoją **subskrypcję** platformy Azure.
   3. Dla grupy zasobów wykonaj jedną z hello następujące kroki: 
      
      - Wybierz **Użyj istniejącego** tooselect istniejącą grupę zasobów.
      - Wybierz **Utwórz nowy** tooenter nazwę grupy zasobów.
          
        Niektóre kroki hello w tym samouczku Załóżmy, że nazwa hello: **ADFTutorialResourceGroup** hello grupy zasobów. toolearn temat grup zasobów, zobacz [toomanage przy użyciu zasobów grup zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md).
   4. Wybierz **lokalizacji** hello fabryki danych.
   5. Wybierz **toodashboard numeru Pin** pole wyboru u dołu hello hello bloku.  
   6. Kliknij przycisk **Utwórz**.
      
       ![Blok Nowa fabryka danych](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. Po zakończeniu tworzenia hello Zobacz hello **fabryki danych** bloku, jak pokazano w powitania po obrazu:
   
   ![Strona główna fabryki danych](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a>Uruchamianie Kreatora kopiowania
1. W bloku fabryki danych hello, kliknij **kopiowanie danych [Podgląd]** toolaunch hello **kreatora kopiowania**. 
   
   > [!NOTE]
   > Jeśli widzisz tej przeglądarki sieci web hello jest zablokowany na "Autoryzowanie...", wyłącz/Usuń zaznaczenie pola wyboru **zablokować pliki cookie innych firm, a dane lokacji** w ustawieniach przeglądarki hello (lub) Zachowaj ona włączona i utworzyć wyjątek  **Login.microsoftonline.com** , a następnie spróbuj ponownie uruchomić Kreatora hello.
2. W hello **właściwości** strony:
   
   1. Wprowadź wartość **CopyFromBlobToAzureSql** w polu **Nazwa zadania**
   2. Wprowadź **opis** (opcjonalnie).
   3. Zmień hello **Data i godzina rozpoczęcia** i hello **Data i godzina zakończenia** tak, aby data zakończenia hello jest ustawić tootoday i uruchomić Data toofive dni wcześniej.  
   4. Kliknij przycisk **Dalej**.  
      
      ![Narzędzie kopiowania — strona Właściwości](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. Na powitania **magazynu danych źródła** kliknij przycisk **magazyn obiektów Blob Azure** kafelka. Zadanie kopiowania hello są używane magazynu tej strony toospecify hello źródła danych. 
   
    ![Narzędzie kopiowania — strona magazynu danych źródłowych](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. Na powitania **Określ konto magazynu obiektów Blob platformy Azure hello** strony:
   
   1. Wprowadź wartość **AzureStorageLinkedService** w polu **Nazwa połączonej usługi**.
   2. Upewnij się, że wybrano opcję **Z subskrypcji Azure** dla ustawienia **Metoda wyboru konta**.
   3. Wybierz swoją **subskrypcję** platformy Azure.  
   4. Wybierz **konto magazynu Azure** z hello konta dostępne w ramach subskrypcji hello wybrane listy magazynu Azure. Można także tooenter ustawienia konta magazynu ręcznie, wybierając **ręcznie wprowadzić** opcję hello **konta metodę wyboru**, a następnie kliknij przycisk **dalej**. 
      
      ![Skopiuj narzędzie — Określ konto magazynu obiektów Blob platformy Azure hello](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. Na **wybierz hello wejściowy plik lub folder** strony:
   
   1. Kliknij dwukrotnie pozycję **adftutorial** (folder).
   2. Zaznacz plik **emp.txt** i kliknij przycisk **Wybierz**.
      
      ![Skopiuj narzędzie — Wybierz hello wejściowego pliku lub folderu](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. Na powitania **wybierz hello wejściowy plik lub folder** kliknij przycisk **dalej**. Nie wybieraj opcji **Kopia binarna**. 
   
    ![Skopiuj narzędzie — Wybierz hello wejściowego pliku lub folderu](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. Na powitania **ustawienia formatu pliku** strony, zobacz ograniczniki hello i hello schemat, który jest automatycznie wykrywane przez kreatora hello podczas analizowania pliku hello. Możesz też wprowadzić ograniczniki hello ręcznie hello kopiowania kreatora toostop auto wykrywania lub toooverride. Kliknij przycisk **dalej** po Przejrzyj ograniczniki hello i wyświetlić podgląd danych. 
   
    ![Narzędzie kopiowania — ustawienia formatu pliku](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. Na powitania docelowego dane przechowywane strony, wybierz **bazy danych SQL Azure**i kliknij przycisk **dalej**.
   
    ![Narzędzie kopiowania — wybieranie magazynu docelowego](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. Na **bazy danych Azure SQL hello określ** strony:
   
   1. Wprowadź **AzureSqlLinkedService** dla hello **nazwa połączenia** pola.
   2. Upewnij się, że wybrano opcję **Z subskrypcji Azure** dla ustawienia **Metoda wyboru serwera/bazy danych**.
   3. Wybierz swoją **subskrypcję** platformy Azure.  
   4. Wybierz opcje **Nazwa serwera** i **Baza danych**.
   5. Wypełnij pola **Nazwa użytkownika** i **Hasło**.
   6. Kliknij przycisk **Dalej**.  
      
      ![Narzędzie kopiowania — określanie bazy danych Azure SQL Database](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. Na powitania **mapowania tabeli** wybierz pozycję **pustych elementów** dla hello **docelowego** pola z listy rozwijanej hello, kliknij przycisk **Strzałka w dół** (opcjonalnie) toosee hello schematu i toopreview hello danych.
    
     ![Narzędzie kopiowania — mapowanie tabeli](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. Na powitania **mapowanie schematu** kliknij przycisk **dalej**.
    
    ![Narzędzie kopiowania — mapowanie schematu](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. Na powitania **ustawienia wydajności** kliknij przycisk **dalej**. 
    
    ![Narzędzie kopiowania — ustawienia wydajności](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. Przejrzyj informacje w hello **Podsumowanie** , a następnie kliknij przycisk **Zakończ**. Kreator Hello tworzy dwa połączone usługi, dwóch zestawów danych (dane wejściowe i wyjściowe) i jeden potok w fabryce danych hello (z którego uruchamiana jest hello kreatora kopiowania). 
    
    ![Narzędzie kopiowania — ustawienia wydajności](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a>Uruchamianie aplikacji do monitorowania i zarządzania
1. Na powitania **wdrożenia** strony, kliknij łącze hello: `Click here toomonitor copy pipeline`.
   
   ![Narzędzie kopiowania — wdrażanie zakończyło się pomyślnie](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. monitorowanie aplikacji Hello jest uruchamiana w osobnej karcie w przeglądarce sieci web.   
   
   ![Aplikacja do monitorowania](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. toosee hello najnowszy stan wycinków co godzinę, kliknij przycisk **Odśwież** przycisku na powitania **okien działania** listy u dołu hello. Pięć okien działania zostanie wyświetlony przez pięć dni od czasu rozpoczęcia i zakończenia dla potoku hello. listy Hello nie zostanie automatycznie odświeżony, więc możesz muszą tooclick Odśwież kilka razy, zanim zostaną wyświetlone wszystkie okna działania hello w stanie gotowe hello. 
4. Wybierz okno działania hello listy. Zobacz szczegóły hello o nim w hello **działania okna Eksploratora** na powitania prawo.

    ![Szczegóły okna działania](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    Należy zauważyć, że są daty hello 11, 12, 13, 14 do 15 w kolorze zielonym, co oznacza, że już zostały wyprodukowane hello dzienne dane wyjściowe wycinków tymi datami. Również Zobacz kolor kodowania na powitania potoku i hello wyjściowy zestaw danych w widoku diagramu hello. W poprzednim kroku hello Zwróć uwagę, wycinków dwóch zostały już utworzone, jeden wycinek jest obecnie przetwarzana i hello pozostałe dwa oczekują toobe przetworzone (w oparciu kodowanie kolorami hello). 

    Aby uzyskać więcej informacji na temat używania tej aplikacji, zobacz artykuł [Monitor and manage pipeline using Monitoring App](data-factory-monitor-manage-app.md) (Monitorowanie potoku i zarządzanie nim przy użyciu aplikacji do monitorowania).

## <a name="next-steps"></a>Następne kroki
W tym samouczku użyto magazynu obiektów blob platformy Azure jako magazynu danych źródła oraz bazy danych SQL na platformie Azure jako magazynu danych docelowych w operacji kopiowania. Witaj Poniższa tabela zawiera listę magazynów danych obsługiwane jako źródeł i miejsc docelowych przez działanie kopiowania hello: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

Aby uzyskać więcej informacji o pola/właściwości, które widać w kreatorze kopiowania hello magazynu danych kliknij łącze hello hello magazynu danych w tabeli hello. 
