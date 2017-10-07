---
title: "Samouczek: Tworzenie potoku toomove danych przy użyciu programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Ten samouczek zawiera instrukcje tworzenia potoku usługi Azure Data Factory za pomocą działania kopiowania przy użyciu programu Azure PowerShell."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 71087349-9365-4e95-9847-170658216ed8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 21406d7dfaa0c555b2538fbb52839d761c140fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a>Samouczek: tworzenie potoku usługi Data Factory przenoszącego dane przy użyciu programu Azure PowerShell
> [!div class="op_single_selector"]
> * [Przegląd i wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Kreator kopiowania](data-factory-copy-data-wizard-tutorial.md)
> * [Witryna Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Program Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [Program PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Szablon usługi Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [Interfejs API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [Interfejs API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)
>
>

W tym artykule dowiesz się, jak toouse PowerShell toocreate fabryki danych z potok, który kopiuje dane z bazy danych Azure SQL tooan magazynu obiektów blob platformy Azure. Jeśli nowy tooAzure fabryki danych, zapoznaj się z artykułem hello [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) artykuł przed wykonaniem tego samouczka.   

W tym samouczku opisano tworzenie potoku z jednym działaniem (Działanie kopiowania). działanie kopiowania Hello kopiuje dane z magazynu danych obsługiwanych ujścia magazynu tooa obsługiwane dane. Aby zapoznać się z listą magazynów danych obsługiwanych jako źródła i ujścia, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats). działanie Hello jest obsługiwany przez ogólnie dostępna usługa, która można skopiować dane między różnych magazynach danych w sposób bezpieczny, niezawodny i skalowalności. Aby uzyskać więcej informacji na temat hello działanie kopiowania, zobacz [działań przepływu danych](data-factory-data-movement-activities.md).

Potok może obejmować więcej niż jedno działanie. I tworzenia łańcucha dwa działania (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań. Aby uzyskać więcej informacji, zobacz sekcję dotyczącą [wielu działań w potoku](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

> [!NOTE]
> W tym artykule nie opisano wszystkich poleceń cmdlet fabryki danych hello. Pełna dokumentacja dotycząca tych poleceń cmdlet znajduje się w artykule [Dokumentacja dotycząca poleceń cmdlet usługi Data Factory](/powershell/module/azurerm.datafactories).
> 
> Witaj potoku danych w tym samouczku kopiuje dane z magazynu danych źródła danych magazynu tooa docelowego. Samouczek na temat danych tootransform przy użyciu fabryki danych Azure, zobacz [samouczek: Tworzenie danych tootransform potoku, przy użyciu klastra usługi Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Wymagania wstępne
- Wymagania wstępne wymienione w hello ukończyć [wymagania wstępne dotyczące samouczka](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artykułu.
- Zainstaluj program **Azure PowerShell**. Postępuj zgodnie z instrukcjami hello [jak tooinstall i konfigurowanie programu Azure PowerShell](../powershell-install-configure.md).

## <a name="steps"></a>Kroki
Poniżej przedstawiono kroki hello, które należy wykonać w ramach tego samouczka:

1. Utworzenie **fabryki danych** na platformie Azure. W tym kroku jest tworzona fabryka danych o nazwie ADFTutorialDataFactoryPSH. 
2. Utwórz **połączone usługi** w fabryce danych hello. Ten krok polega na utworzeniu dwóch połączonych usług: Azure Storage i Azure SQL Database. 
    
    Witaj AzureStorageLinkedService łączy fabrykę danych toohello konta magazynu platformy Azure. Utworzono kontener i przekazany w ramach konta magazynu danych toothis [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

    AzureSqlLinkedService łączy fabrykę danych toohello bazy danych Azure SQL. dane Hello, który jest skopiowany z magazynu obiektów blob hello są przechowywane w tej bazie danych. W ramach [wymagań wstępnych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) w tej bazie danych została utworzona tabela SQL.   
3. Utwórz dane wejściowe i wyjściowe **zestawów danych** w fabryce danych hello.  
    
    Hello Azure połączoną usługą magazynu określa parametry połączenia hello, która używa usługi fabryka danych w czasie wykonywania tooconnect tooyour kontem magazynu platformy Azure. I zestawu danych wejściowych obiektu blob hello określa hello kontenera i folderu hello, który zawiera hello danych wejściowych.  

    Podobnie hello usługi baza danych SQL Azure połączone określa hello parametry połączenia, które korzysta z usługi fabryka danych w czasie wykonywania tooconnect tooyour — bazy danych Azure SQL. I tabeli hello hello bazy danych toowhich hello danych z magazynu obiektów blob hello jest kopiowany określa hello danych wyjściowych SQL tabeli dataset.
4. Utwórz **potoku** w fabryce danych hello. W tym kroku jest tworzony potok za pomocą działania kopiowania.   
    
    działanie kopiowania Hello kopiuje dane z obiektu blob w tabeli tooa magazynu obiektów blob platformy Azure hello w bazie danych Azure SQL hello. Działanie kopiowania służy w potoku danych toocopy z dowolnego miejsca docelowego tooany obsługiwane obsługiwanej źródłowej. Listę obsługiwanych magazynów danych można znaleźć w artykule [Działania związane z przenoszeniem danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats). 
5. Monitor hello potoku. W tym kroku zostanie **monitor** hello wycinków wejściowych i wyjściowych zestawów danych przy użyciu programu PowerShell.

## <a name="create-a-data-factory"></a>Tworzenie fabryki danych
> [!IMPORTANT]
> Pełne [wymagania wstępne dotyczące samouczka hello](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) Jeśli jeszcze tego nie zrobiono.   

Fabryka danych może obejmować jeden lub wiele potoków. Potok może obejmować jedno lub wiele działań. Na przykład toocopy działanie kopiowania danych z magazynu danych docelowy tooa źródłowego i HDInsight Hive działania toorun tootransform skryptu Hive wejściowe dane wyjściowe tooproduct danych. Zacznijmy od utworzenia hello fabryki danych w tym kroku.

1. Uruchom program **PowerShell**. Nie zamykaj programu Azure PowerShell do momentu zakończenia hello tego samouczka. Zamknij i otwórz ponownie, należy najpierw polecenia hello toorun ponownie.

    Uruchom następujące polecenie hello i wprowadź hello nazwę użytkownika i hasło, użyj toosign w toohello portalu Azure:

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    Uruchom następujące polecenie tooview hello wszystkie subskrypcje powitania dla tego konta:

    ```PowerShell
    Get-AzureRmSubscription
    ```

    Uruchom następujące polecenie tooselect hello subskrypcję, która ma toowork z hello. Zastąp  **&lt;NameOfAzureSubscription** &gt; o nazwie hello subskrypcji platformy Azure:

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. Tworzenie grupy zasobów platformy Azure o nazwie **ADFTutorialResourceGroup** , uruchamiając następujące polecenie hello:

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    Niektóre kroki hello w tym samouczku Załóżmy, że hello grupy zasobów o nazwie **ADFTutorialResourceGroup**. Jeśli używasz innej grupie zasobów, należy toouse go zamiast ADFTutorialResourceGroup w tym samouczku.
3. Uruchom hello **AzureRmDataFactory nowy** toocreate polecenia cmdlet fabryki danych o nazwie **ADFTutorialDataFactoryPSH**:  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    Ta nazwa może już być używana. W związku z tym upewnić hello nazwa fabryki danych hello unikatowy przez dodanie prefiksu lub sufiksu (na przykład: ADFTutorialDataFactoryPSH05152017) i uruchom ponownie polecenie hello.  

Należy zwrócić uwagę hello następujące punkty:

* Nazwa fabryki danych Azure hello Hello musi być globalnie unikatowe. Jeśli zostanie wyświetlony następujący błąd hello, Zmień nazwę hello (na przykład yournameADFTutorialDataFactoryPSH). Użyj tej nazwy zamiast ADFTutorialFactoryPSH podczas wykonywania kroków w tym samouczku. Aby uzyskać informacje o artefaktach usługi Data Factory, zobacz artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Data Factory — reguły nazewnictwa).

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* toocreate wystąpienia fabryki danych, musi być współautora lub administratora hello subskrypcji platformy Azure.
* Nazwa fabryki danych hello Hello mogą być zarejestrowana jako nazwa DNS w przyszłości hello i dlatego stać się publicznie widoczna.
* Może pojawić się hello następujący błąd: "**Ta subskrypcja nie jest zarejestrowany toouse przestrzeni nazw Microsoft.DataFactory.**" Wykonaj jedną z następujących hello, a następnie spróbuj opublikować ponownie:

  * W programie Azure PowerShell Uruchom hello następujące polecenia tooregister hello fabryki danych dostawcy:

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    Uruchom następujące polecenie tooconfirm hello tej fabryki danych w zarejestrowany dostawca hello:

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Zaloguj się przy użyciu hello toohello subskrypcji platformy Azure [portalu Azure](https://portal.azure.com). Przejdź do bloku fabryki danych tooa lub tworzenie fabryki danych w hello portalu Azure. Ta akcja rejestruje automatycznie hello dostawcy dla Ciebie.

## <a name="create-linked-services"></a>Tworzenie połączonych usług
Połączone usługi są tworzone w toolink fabryki danych dane są przechowywane i obliczeniowe fabryki danych toohello usług. W tym samouczku nie przedstawiono korzystania z żadnych usług obliczeniowych, takich jak Azure HDInsight czy Azure Data Lake Analytics. Zostają użyte dwa magazyny danych typu Azure Storage (źródło) i Azure SQL Database (lokalizacja docelowa). 

W związku z tym tworzy się dwie połączone usługi o nazwie AzureStorageLinkedService i AzureSqlLinkedService typu: AzureStorage i AzureSqlDatabase.  

Witaj AzureStorageLinkedService łączy fabrykę danych toohello konta magazynu platformy Azure. To konto magazynu jest hello jedną w którym utworzono kontener i hello dane przekazane jako część [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

AzureSqlLinkedService łączy fabrykę danych toohello bazy danych Azure SQL. dane Hello, który jest skopiowany z magazynu obiektów blob hello są przechowywane w tej bazie danych. Utworzono hello pustych elementów tabeli w tej bazie danych jako część [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a>Tworzenie połączonej usługi dla konta magazynu Azure
W tym kroku możesz połączyć fabrykę danych tooyour konta magazynu platformy Azure.

1. Utwórz plik JSON o nazwie **AzureStorageLinkedService.json** w **C:\ADFGetStartedPSH** folder o hello następującej zawartości: (Utwórz hello folder ADFGetStartedPSH, jeśli jeszcze nie istnieje).

    > [!IMPORTANT]
    > Zastąp &lt;accountname&gt; i &lt;accountkey&gt; z nazwy i klucza konta magazynu Azure przed zapisaniem pliku hello. 

    ```json
    {
        "name": "AzureStorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        }
     }
    ``` 
2. W **programu Azure PowerShell**, Przełącz toohello **ADFGetStartedPSH** folderu.
4. Uruchom hello **AzureRmDataFactoryLinkedService nowy** hello toocreate polecenia cmdlet połączonej usługi: **AzureStorageLinkedService**. To polecenie cmdlet i innych poleceń cmdlet z fabryki danych użycia w ramach tego samouczka wymaga wartości toopass dla hello **ResourceGroupName** i **DataFactoryName** parametrów. Alternatywnie można przekazać obiektu DataFactory hello zwróconych przez polecenie cmdlet New-AzureRmDataFactory hello bez wprowadzania ResourceGroupName i DataFactoryName każdorazowo po uruchomieniu polecenia cmdlet. 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    Oto hello przykładowe dane wyjściowe:

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    Inny sposób tworzenia tej połączonej usługi jest nazwa grupy zasobów toospecify i nazwa fabryki danych zamiast określania obiektu DataFactory hello.  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a>Tworzenie połączonej usługi dla bazy danych SQL Azure
W tym kroku możesz połączyć fabrykę danych tooyour bazy danych Azure SQL.

1. Utwórz plik JSON o nazwie AzureSqlLinkedService.json w folderze C:\ADFGetStartedPSH z hello następującej zawartości:

    > [!IMPORTANT]
    > Zastąp wartości &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt; oraz &lt;password&gt; nazwą serwera SQL Azure, nazwą bazy danych, nazwą użytkownika i hasłem.
    
    ```json
    {
        "name": "AzureSqlLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": "Server=tcp:<server>.database.windows.net,1433;Database=<databasename>;User ID=<user>@<server>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        }
     }
    ```
2. Uruchom następujące polecenie toocreate hello połączonej usługi:

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    Oto hello przykładowe dane wyjściowe:

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   Upewnij się, że **dostęp do usług tooAzure** opcja jest włączona dla Twojej bazy danych programu SQL server. tooverify i włącz ją, hello następujące kroki:

    1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com)
    2. Kliknij przycisk **więcej usług >** na powitania po lewej, a następnie kliknij **serwerów SQL** w hello **baz danych** kategorii.
    3. Wybierz serwer, na liście hello programu SQL Server.
    4. W bloku serwera SQL hello, kliknij polecenie **Pokaż ustawienia zapory** łącza.
    5. W hello **ustawienia zapory** bloku, kliknij przycisk **ON** dla **dostęp do usług tooAzure**.
    6. Kliknij przycisk **zapisać** na powitania narzędzi. 

## <a name="create-datasets"></a>Tworzenie zestawów danych
W poprzednim kroku hello utworzono toolink połączone usługi konta magazynu Azure i fabryki danych tooyour bazy danych Azure SQL. W tym kroku należy zdefiniować dwa zestawy danych o nazwie InputDataset i OutputDataset reprezentujące danych wejściowych i wyjściowych danych przechowywanych w magazynach danych hello odwołuje się AzureStorageLinkedService i AzureSqlLinkedService odpowiednio.

Hello Azure połączoną usługą magazynu określa parametry połączenia hello, która używa usługi fabryka danych w czasie wykonywania tooconnect tooyour kontem magazynu platformy Azure. I zestawu danych wejściowych obiektu blob hello (InputDataset) określa hello kontenera i folderu hello, który zawiera hello danych wejściowych.  

Podobnie hello usługi baza danych SQL Azure połączone określa hello parametry połączenia, które korzysta z usługi fabryka danych w czasie wykonywania tooconnect tooyour — bazy danych Azure SQL. I hello danych wyjściowych SQL tabeli dataset (OututDataset) określa hello tabeli w hello bazy danych toowhich powitalne dane z magazynu obiektów blob hello są kopiowane. 

### <a name="create-an-input-dataset"></a>Tworzenie wejściowego zestawu danych
W tym kroku utworzysz zestaw danych o nazwie InputDataset, który wskazuje plik obiektu blob tooa (emp.txt) w folderze głównym hello kontenera obiektów blob (adftutorial) w hello reprezentowany przez hello AzureStorageLinkedService połączone usługi Magazyn Azure. Brak określić wartość dla nazwy pliku hello (lub Pomiń je), danych z wszystkich obiektów blob w folderze wejściowych hello są skopiowanych toohello docelowego. W tym samouczku należy określić wartość dla hello fileName.  

1. Utwórz plik JSON o nazwie **InputDataset.json** w hello **C:\ADFGetStartedPSH** folder z hello następującej zawartości:

    ```json
    {
        "name": "InputDataset",
        "properties": {
            "structure": [
                {
                    "name": "FirstName",
                    "type": "String"
                },
                {
                    "name": "LastName",
                    "type": "String"
                }
            ],
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "emp.txt",
                "folderPath": "adftutorial/",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```

    Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:

    | Właściwość | Opis |
    |:--- |:--- |
    | type | Właściwość type Hello ustawiono zbyt**AzureBlob** ponieważ danych znajduje się w magazynie obiektów blob platformy Azure. |
    | linkedServiceName | Odwołuje się toohello **AzureStorageLinkedService** utworzony wcześniej. |
    | folderPath | Określa obiekt blob hello **kontenera** i hello **folderu** zawiera obiekty BLOB wejściowego. W tym samouczku adftutorial jest hello kontenera obiektów blob i hello folderu głównego. | 
    | fileName | Ta właściwość jest opcjonalna. W przypadku pominięcia tej właściwości, pobierane są wszystkie pliki z hello folderPath. W tym samouczku **emp.txt** określona dla hello nazwę pliku, tak aby plik zostaje pobrana do przetwarzania. |
    | format -> type |Plik wejściowy Hello jest w formacie tekstowym hello, więc używamy **TextFormat**. |
    | columnDelimiter | Witaj kolumn w pliku wejściowym hello są rozdzielane **przecinka (`,`)**. |
    | frequency/interval | częstotliwość Hello ustawiono zbyt**godzina** i interwał jest ustawiany za**1**, co oznacza, że hello wejściowych dostępnych wycinków **co godzinę**. Innymi słowy, hello usługi fabryka danych sprawdza dane wejściowe co godzinę w folderze głównym hello kontenera obiektów blob (**adftutorial**) określone. Wyszukuje hello danych w ramach hello potoku rozpoczęcia i zakończenia godzin, nie przed lub po tych godzinach.  |
    | external | Ta właściwość jest ustawiona zbyt**true** czy hello danych nie jest generowany przez tego potoku. Witaj danych wejściowych w tym samouczku jest hello emp.txt pliku, który nie jest generowany w tym potoku, możemy ustawić tootrue tej właściwości. |

    Aby uzyskać więcej informacji o tych właściwościach JSON, zobacz [artykuł dotyczący łącznika obiektu blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties).
2. Uruchom hello następujące polecenia toocreate hello fabryki danych w zestawie danych.

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    Oto hello przykładowe dane wyjściowe:

    ```
    DatasetName       : InputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureBlobDataset
    Policy            : Microsoft.Azure.Management.DataFactories.Common.Models.Policy
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

### <a name="create-an-output-dataset"></a>Tworzenie wyjściowego zestawu danych
W tej części krok hello utworzyć wyjściowy zestaw danych o nazwie **OutputDataset**. Ten zestaw danych wskazuje tooa tabeli SQL w bazie danych Azure SQL hello reprezentowany przez **AzureSqlLinkedService**. 

1. Utwórz plik JSON o nazwie **OutputDataset.json** w hello **C:\ADFGetStartedPSH** folder o hello następującej zawartości:

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "structure": [
                {
                    "name": "FirstName",
                    "type": "String"
                },
                {
                    "name": "LastName",
                    "type": "String"
                }
            ],
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

    Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:

    | Właściwość | Opis |
    |:--- |:--- |
    | type | Właściwość type Hello ustawiono zbyt**AzureSqlTable** , ponieważ dane są kopiowane tooa tabeli w bazie danych Azure SQL. |
    | linkedServiceName | Odwołuje się toohello **AzureSqlLinkedService** utworzony wcześniej. |
    | tableName | Określony hello **tabeli** toowhich hello dane są kopiowane. | 
    | frequency/interval | Witaj częstotliwość ustawiono zbyt**godzina** i interwał **1**, co oznacza, że wycinki danych wyjściowych hello są produkowane **co godzinę** między hello potoku rozpoczęcia i zakończenia godzin przed nie lub Po tych godzinach.  |

    Istnieją trzy kolumny — **identyfikator**, **imię**, i **nazwisko** — Witaj pustych elementów tabeli w bazie danych hello. Identyfikator jest kolumny tożsamości, więc musisz tylko toospecify **imię** i **nazwisko** tutaj.

    Aby uzyskać więcej informacji o tych właściwościach JSON, zobacz [artykuł dotyczący łącznika usługi Azure SQL](data-factory-azure-sql-connector.md#dataset-properties).
2. Hello uruchom następujące polecenie toocreate hello data factory w zestawie danych.

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    Oto hello przykładowe dane wyjściowe:

    ```
    DatasetName       : OutputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureSqlTableDataset
    Policy            :
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

## <a name="create-a-pipeline"></a>Tworzenie potoku
W tym kroku opisano tworzenie potoku za pomocą **działania kopiowania**, w którym parametr **InputDataset** jest używany jako dane wejściowe, a parametr **OutputDataset** jako dane wyjściowe.

Wyjściowy zestaw danych jest obecnie, jakie dysków hello harmonogramu. W tym samouczku wyjściowy zestaw danych jest skonfigurowane tooproduce wycinek godzinę. potok Hello ma czas rozpoczęcia i godzina zakończenia, będące w ciągu jednego dnia od siebie, który wynosi 24 godziny. W związku z tym 24 wycinków wyjściowy zestaw danych są produkowane przez hello potoku. 


1. Utwórz plik JSON o nazwie **ADFTutorialPipeline.json** w hello **C:\ADFGetStartedPSH** folder z hello następującej zawartości:

    ```json   
    {
      "name": "ADFTutorialPipeline",
      "properties": {
        "description": "Copy data from a blob tooAzure SQL table",
        "activities": [
          {
            "name": "CopyFromBlobToSQL",
            "type": "Copy",
            "inputs": [
              {
                "name": "InputDataset"
              }
            ],
            "outputs": [
              {
                "name": "OutputDataset"
              }
            ],
            "typeProperties": {
              "source": {
                "type": "BlobSource"
              },
              "sink": {
                "type": "SqlSink",
                "writeBatchSize": 10000,
                "writeBatchTimeout": "60:00:00"
              }
            },
            "Policy": {
              "concurrency": 1,
              "executionPriorityOrder": "NewestFirst",
              "retry": 0,
              "timeout": "01:00:00"
            }
          }
        ],
        "start": "2017-05-11T00:00:00Z",
        "end": "2017-05-12T00:00:00Z"
      }
    } 
    ```
    Należy zwrócić uwagę hello następujące punkty:
   
    - W sekcji działania hello jest tylko jedno działanie którego **typu** ustawiono zbyt**kopiowania**. Aby uzyskać więcej informacji o działaniu kopiowania hello, zobacz [działań przepływu danych](data-factory-data-movement-activities.md). W rozwiązaniach usługi Data Factory można również użyć [działań dotyczących przekształcania danych](data-factory-data-transformation-activities.md).
    - Dane wejściowe dla działania hello jest ustawiony za**InputDataset** i danych wyjściowych dla działania hello jest ustawiony za**OutputDataset**. 
    - W hello **typeProperties** sekcji **BlobSource** jest określony jako typ źródła hello i **SqlSink** jest określony jako typ ujścia hello. Aby uzyskać pełną listę obsługiwanych przez działanie kopiowania hello jako źródła i wychwytywanie magazyny danych, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats). toolearn jak przechowywać toouse określonych danych obsługiwane jako źródło/ujście, kliknij łącze hello hello tabeli.  
     
    Zastąp wartość hello hello **start** właściwość o hello bieżącego dnia i **zakończenia** wartości z hello następnego dnia. Można określić tylko część daty hello i Pomiń hello czas część hello Data i godzina. Na przykład "2016-02-03", która odpowiada za "2016-02-03T00:00:00Z"
     
    Zarówno data/godzina rozpoczęcia, jak i data/godzina zakończenia muszą być w [formacie ISO](http://en.wikipedia.org/wiki/ISO_8601). Przykładowo: 2016-10-14T16:32:41Z. Witaj **zakończenia** czasu jest opcjonalne, ale możemy użyć w tym samouczku. 
     
    Jeśli nie określisz wartości hello **zakończenia** właściwości, jest on obliczany jako "**start + 48 godzin**". potok hello toorun przez czas nieokreślony, określ **9999-09-09** jako wartość hello hello **zakończenia** właściwości.
     
    W hello poprzedzających przykład istnieją 24 wycinków danych, jak każdy wycinek danych jest tworzone co godzinę.

    Opisy właściwości JSON w definicji potoku znajdują się w artykule dotyczącym [tworzenia potoków](data-factory-create-pipelines.md). Opisy właściwości JSON w definicji działania kopiowania znajdują się w artykule dotyczącym [działań związanych z przenoszeniem danych](data-factory-data-movement-activities.md). Opisy właściwości JSON obsługiwanych przez BlobSource można znaleźć w [artykule dotyczącym łącznika usługi Azure Blob](data-factory-azure-blob-connector.md). Opisy właściwości JSON obsługiwanych przez SqlSink można znaleźć w artykule [dotyczącym łącznika usługi Azure SQL Database](data-factory-azure-sql-connector.md).
2. Witaj uruchom następujące polecenie tabeli fabryki danych hello toocreate.

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    Oto hello przykładowe dane wyjściowe: 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

**Gratulacje!** Pomyślnie utworzono fabryki danych Azure z potoku toocopy danych z bazy danych Azure SQL tooan magazynu obiektów blob platformy Azure. 

## <a name="monitor-hello-pipeline"></a>Monitor hello potoku
W tym kroku użyjesz programu Azure PowerShell toomonitor co się dzieje w fabryce danych Azure.

1. Zastąp &lt;DataFactoryName&gt; o nazwie hello fabryki danych i uruchom **Get-AzureRmDataFactory**i przypisz tooa dane wyjściowe hello $df zmiennej.

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    Na przykład:
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    Następnie uruchom hello drukowania zawartości hello toosee $df następujące dane wyjściowe: 
    
    ```
    PS C:\ADFGetStartedPSH> $df
    
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DataFactoryId     : 6f194b34-03b3-49ab-8f03-9f8a7b9d3e30
    ResourceGroupName : ADFTutorialResourceGroup
    Location          : West US
    Tags              : {}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DataFactoryProperties
    ProvisioningState : Succeeded
    ```
2. Uruchom **Get-AzureRmDataFactorySlice** tooget szczegóły wszystkie fragmenty hello **OutputDataset**, która jest hello wyjściowego zestawu danych potoku hello.  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   To ustawienie powinno być zgodne hello **Start** wartość w potoku hello JSON. Powinna zostać wyświetlona 24 wycinków, po jednej dla każdej godziny od 00: 00 z too12 bieżącego dnia hello UŻYWAM programu hello następnego dnia.

   Poniżej przedstawiono trzy wycinków próbki z danych wyjściowych hello: 

    ``` 
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 11:00:00 PM
    End               : 5/12/2017 12:00:00 AM
    RetryCount        : 0
    State             : Ready
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 9:00:00 PM
    End               : 5/11/2017 10:00:00 PM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0   

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 8:00:00 PM
    End               : 5/11/2017 9:00:00 PM
    RetryCount        : 0
    State             : Waiting
    SubState          : ConcurrencyLimit
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. Uruchom **Get-AzureRmDataFactoryRun** tooget hello szczegółów działania trwający **określonych** wycinka. Skopiuj wartość daty i godziny hello z danych wyjściowych hello hello poprzednie polecenie toospecify hello wartości dla parametru StartDateTime hello. 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   Oto hello przykładowe dane wyjściowe: 

    ```
    Id                  : c0ddbd75-d0c7-4816-a775-704bbd7c7eab_636301332000000000_636301368000000000_OutputDataset
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : ADFTutorialDataFactoryPSH0516
    DatasetName         : OutputDataset
    ProcessingStartTime : 5/16/2017 8:00:33 PM
    ProcessingEndTime   : 5/16/2017 8:01:36 PM
    PercentComplete     : 100
    DataSliceStart      : 5/11/2017 9:00:00 PM
    DataSliceEnd        : 5/11/2017 10:00:00 PM
    Status              : Succeeded
    Timestamp           : 5/16/2017 8:00:33 PM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : CopyFromBlobToSQL
    PipelineName        : ADFTutorialPipeline
    Type                : Copy  
    ```

Pełną dokumentację poleceń cmdlet można znaleźć w artykule [Dokumentacja poleceń cmdlet usługi Data Factory](/powershell/module/azurerm.datafactories).

## <a name="summary"></a>Podsumowanie
W tym samouczku danych toocopy fabryki danych Azure została utworzona z bazy danych Azure SQL tooan obiektów blob platformy Azure. Użyto fabryki danych hello toocreate programu PowerShell, połączone usługi, zestawy danych i potoku. Poniżej przedstawiono ogólne kroki hello, wykonane w tym samouczku:  

1. Tworzenie **fabryki danych** Azure.
2. Tworzenie **połączonych usług**:

   a. **Usługi Azure Storage** połączone konta magazynu Azure, która przechowuje dane wejściowe toolink usługi.     
   b. **Azure SQL** połączone usługi toolink Twojej bazy danych SQL, która przechowuje dane wyjściowe hello.
3. Tworzenie **zestawów danych** opisujących dane wejściowe i wyjściowe dla potoków.
4. Utworzony **potoku** z **działanie kopiowania**, z **BlobSource** jako źródło hello i **SqlSink** jako hello ujścia.

## <a name="next-steps"></a>Następne kroki
W tym samouczku użyto magazynu obiektów blob platformy Azure jako magazynu danych źródła oraz bazy danych SQL na platformie Azure jako magazynu danych docelowych w operacji kopiowania. Witaj Poniższa tabela zawiera listę magazynów danych obsługiwane jako źródeł i miejsc docelowych przez działanie kopiowania hello: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn o jak magazyn danych toocopy z danych, kliknij łącze hello hello magazynu danych w tabeli hello. 

