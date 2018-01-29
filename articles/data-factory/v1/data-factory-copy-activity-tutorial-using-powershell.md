---
title: "Samouczek: tworzenie potoku w celu przeniesienia danych przy użyciu programu Azure PowerShell | Microsoft Docs"
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
ms.date: 01/22/2018
ms.author: spelluru
robots: noindex
ms.openlocfilehash: 66e054aa13c7a3555758268be676e93ff7a3b5d1
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/23/2018
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
> * [Interfejs API programu .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> Ten artykuł dotyczy wersji 1 usługi Data Factory, która jest ogólnie dostępna (GA). Jeśli używasz wersji 2 usługi Data Factory, która jest w wersji zapoznawczej, zapoznaj się z [dokumentacją samouczka działania kopiowania w wersji 2](../quickstart-create-data-factory-powershell.md). 

W tym artykule wyjaśniono, jak używać programu PowerShell w celu utworzenia fabryki danych obejmującej potok, który kopiuje dane z magazynu obiektów blob w usłudze Azure do bazy danych Azure SQL. Jeśli jesteś nowym użytkownikiem usługi Azure Data Factory, przed wykonaniem instrukcji z tego samouczka zapoznaj się z artykułem [Wprowadzenie do usługi Azure Data Factory](data-factory-introduction.md).   

W tym samouczku opisano tworzenie potoku z jednym działaniem (Działanie kopiowania). Działanie kopiowania kopiuje dane z obsługiwanego magazynu danych do obsługiwanego magazynu danych ujścia. Aby zapoznać się z listą magazynów danych obsługiwanych jako źródła i ujścia, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Działanie jest obsługiwane przez globalnie dostępną usługę, która może kopiować dane między różnymi magazynami danych w sposób bezpieczny, niezawodny i skalowalny. Więcej informacji o działaniu kopiowania znajduje się w artykule dotyczącym [działań związanych z przenoszeniem danych](data-factory-data-movement-activities.md).

Potok może obejmować więcej niż jedno działanie. Dwa działania można połączyć w łańcuch (uruchomić jedno działanie po drugim), ustawiając wyjściowy zestaw danych jednego działania jako zestaw wejściowy drugiego. Aby uzyskać więcej informacji, zobacz sekcję dotyczącą [wielu działań w potoku](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

> [!NOTE]
> Ten artykuł nie obejmuje wszystkich poleceń cmdlet dla usługi Fabryka danych. Pełna dokumentacja dotycząca tych poleceń cmdlet znajduje się w artykule [Dokumentacja dotycząca poleceń cmdlet usługi Data Factory](/powershell/module/azurerm.datafactories).
> 
> Potok danych przedstawiony w tym samouczku kopiuje dane ze źródłowego do docelowego magazynu danych. Aby zapoznać się z samouczkiem dotyczącym przekształcania danych za pomocą usługi Azure Data Factory, zobacz [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md) (Samouczek: Tworzenie potoku przekształcającego dane przy użyciu klastra Hadoop).

## <a name="prerequisites"></a>Wymagania wstępne
- Zrealizuj wymagania wstępne podane w artykule dotyczącym [wymagań wstępnych samouczka](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
- Zainstaluj program **Azure PowerShell**. Wykonaj instrukcje podane w temacie [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="steps"></a>Kroki
Poniżej przedstawiono kroki do wykonania w ramach tego samouczka:

1. Utworzenie **fabryki danych** na platformie Azure. W tym kroku jest tworzona fabryka danych o nazwie ADFTutorialDataFactoryPSH. 
2. Utworzenie **połączonych usług** w fabryce danych. Ten krok polega na utworzeniu dwóch połączonych usług: Azure Storage i Azure SQL Database. 
    
    Polecenie AzureStorageLinkedService łączy konto usługi Azure Storage z fabryką danych. W ramach [wymagań wstępnych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) utworzono kontener i przekazano dane na to konto magazynu.   

    Polecenie AzureSqlLinkedService łączy bazę danych SQL na platformie Azure z fabryką danych. W tej bazie danych są przechowywane dane skopiowane z magazynu obiektów blob. W ramach [wymagań wstępnych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) w tej bazie danych została utworzona tabela SQL.   
3. Utworzenie wejściowych i wyjściowych **zestawów danych** w fabryce danych.  
    
    Połączona usługa magazynu Azure określa parametry połączenia, z których korzysta usługa Data Factory w czasie wykonywania, aby połączyć się z kontem magazynu Azure. Natomiast wejściowy zestaw danych obiektów blob określa kontener oraz folder, który zawiera dane wejściowe.  

    W analogiczny sposób połączona usługa Azure SQL Database określa parametry połączenia, z których korzysta usługa Data Factory w czasie wykonywania, aby połączyć się z bazą danych SQL usługi Azure. Wyjściowy zestaw danych tabeli SQL określa tabelę w bazie danych, do której są kopiowane dane z magazynu obiektów blob.
4. Utworzenie **potoku** w fabryce danych. W tym kroku jest tworzony potok za pomocą działania kopiowania.   
    
    Działanie kopiowania kopiuje dane z obiektu blob w magazynie obiektów blob platformy Azure do tabeli w bazie danych SQL na platformie Azure. Działania kopiowania w potoku można użyć do kopiowania danych z dowolnego obsługiwanego źródła do dowolnej obsługiwanej lokalizacji docelowej. Listę obsługiwanych magazynów danych można znaleźć w artykule [Działania związane z przenoszeniem danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats). 
5. Monitorowanie potoku. Ten krok polega na **monitorowaniu** wycinków wejściowych i wyjściowych zestawów danych przy użyciu programu PowerShell.

## <a name="create-a-data-factory"></a>Tworzenie fabryki danych
> [!IMPORTANT]
> Jeśli jeszcze nie zostało to zrobione, spełnij [wymagania wstępne dotyczące samouczka](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

Fabryka danych może obejmować jeden lub wiele potoków. Potok może obejmować jedno lub wiele działań. Na przykład działanie kopiowania może służyć do skopiowania danych ze źródła do docelowego magazynu danych, a działanie programu Hive w usłudze HDInsight do uruchomienia skryptu programu Hive, który przekształci dane wejściowe w dane wyjściowe produktu. Zacznijmy tworzenie fabryki danych w tym kroku.

1. Uruchom program **PowerShell**. Nie zamykaj programu Azure PowerShell, zanim nie wykonasz wszystkich instrukcji z tego samouczka. Jeśli go zamkniesz i otworzysz ponownie, musisz uruchomić te polecenia jeszcze raz.

    Uruchom poniższe polecenie i wprowadź nazwę użytkownika oraz hasło, których używasz do logowania się w witrynie Azure Portal:

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    Uruchom poniższe polecenie, aby wyświetlić wszystkie subskrypcje dla tego konta:

    ```PowerShell
    Get-AzureRmSubscription
    ```

    Uruchom poniższe polecenie, aby wybrać subskrypcję, z którą chcesz pracować. Zastąp ciąg **&lt;NameOfAzureSubscription**&gt; nazwą subskrypcji platformy Azure:

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. Utwórz grupę zasobów platformy Azure o nazwie **ADFTutorialResourceGroup** przez uruchomienie następującego polecenia:

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    W niektórych krokach w tym samouczku zakłada się, że używana jest grupa zasobów o nazwie **ADFTutorialResourceGroup**. Jeśli używasz innej grupy zasobów, podczas wykonywania instrukcji w tym samouczku trzeba będzie wstawić jej nazwę zamiast nazwy ADFTutorialResourceGroup.
3. Uruchom polecenie cmdlet **New-AzureRmDataFactory**, aby utworzyć fabrykę danych o nazwie **ADFTutorialDataFactoryPSH**:  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    Ta nazwa może już być używana. Zapewnij unikatowość nazwy fabryki danych, dodając do niej prefiks lub sufiks (np. ADFTutorialDataFactoryPSH05152017), i uruchom ponownie polecenie.  

Pamiętaj o następujących kwestiach:

* Nazwa fabryki danych Azure musi być globalnie unikatowa. Jeśli wystąpi poniższy błąd, zmień nazwę (np. twojanazwaADFTutorialDataFactoryPSH). Użyj tej nazwy zamiast ADFTutorialFactoryPSH podczas wykonywania kroków w tym samouczku. Aby uzyskać informacje o artefaktach usługi Data Factory, zobacz artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Data Factory — reguły nazewnictwa).

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* Aby tworzyć wystąpienia usługi Data Factory, musisz być współautorem lub administratorem subskrypcji platformy Azure.
* W przyszłości nazwa fabryki danych może zostać zarejestrowana jako nazwa DNS, a wówczas stanie się widoczna publicznie.
* Może zostać wyświetlony następujący komunikat o błędzie: „**Subskrypcja nie jest zarejestrowana w celu używania przestrzeni nazw Microsoft.DataFactory**”. Wykonaj jedną z następujących czynności i spróbuj opublikować ponownie:

  * W programie Azure PowerShell uruchom następujące polecenie, aby zarejestrować dostawcę usługi Data Factory:

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    Uruchom następujące polecenie, aby potwierdzić, że dostawca usługi Data Factory jest zarejestrowany:

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Przy użyciu subskrypcji platformy Azure zaloguj się w witrynie [Azure Portal](https://portal.azure.com). Przejdź do bloku Data Factory lub utwórz fabrykę danych w witrynie Azure Portal. Ta akcja powoduje automatyczne zarejestrowanie dostawcy.

## <a name="create-linked-services"></a>Tworzenie połączonych usług
Połączone usługi tworzy się w fabryce danych w celu połączenia magazynów danych i usług obliczeniowych z fabryką danych. W tym samouczku nie przedstawiono korzystania z żadnych usług obliczeniowych, takich jak Azure HDInsight czy Azure Data Lake Analytics. Zostają użyte dwa magazyny danych typu Azure Storage (źródło) i Azure SQL Database (lokalizacja docelowa). 

W związku z tym tworzy się dwie połączone usługi o nazwie AzureStorageLinkedService i AzureSqlLinkedService typu: AzureStorage i AzureSqlDatabase.  

Polecenie AzureStorageLinkedService łączy konto usługi Azure Storage z fabryką danych. Na tym koncie magazynu utworzono kontener i przekazano na nie dane w ramach [wymagań wstępnych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

Polecenie AzureSqlLinkedService łączy bazę danych SQL na platformie Azure z fabryką danych. W tej bazie danych są przechowywane dane skopiowane z magazynu obiektów blob. Tabelę emp w tej bazie danych utworzono w ramach [wymagań wstępnych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a>Tworzenie połączonej usługi dla konta magazynu Azure
W tym kroku opisano łączenie konta usługi Azure Storage z fabryką danych.

1. Utwórz plik JSON o nazwie **AzureStorageLinkedService.json** w folderze **C:\ADFGetStartedPSH** o następującej zawartości: (Utwórz folder ADFGetStartedPSH, jeśli jeszcze nie istnieje.)

    > [!IMPORTANT]
    > Przed zapisaniem pliku zastąp wartości &lt;accountname&gt; i &lt;accountkey&gt; nazwą i kluczem konta usługi Azure Storage. 

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
2. W programie **Azure PowerShell** przejdź do folderu **ADFGetStartedPSH**.
4. Uruchom polecenie cmdlet **New-AzureRmDataFactoryLinkedService**, aby utworzyć połączoną usługę **AzureStorageLinkedService**. To polecenie cmdlet i inne polecenia cmdlet usługi Data Factory używane w tym samouczku wymagają przekazania wartości dla parametrów **ResourceGroupName** i **DataFactoryName**. Możesz też przekazać obiekt DataFactory zwrócony przez polecenie cmdlet New-AzureRmDataFactory bez wpisywania parametrów ResourceGroupName i DataFactoryName za każdym razem, gdy uruchamiasz polecenie cmdlet. 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    Oto przykładowe dane wyjściowe:

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    Inna metoda tworzenia połączonej usługi polega na określeniu nazwy grupy zasobów i nazwy fabryki danych zamiast określania obiektu DataFactory.  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a>Tworzenie połączonej usługi dla bazy danych SQL Azure
W tym kroku opisano łączenie bazy danych Azure SQL Database z fabryką danych.

1. W folderze C:\ADFGetStartedPSH utwórz plik JSON o nazwie AzureSqlLinkedService.json z następującą zawartością:

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
2. Uruchom poniższe polecenie, aby utworzyć połączoną usługę:

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    Oto przykładowe dane wyjściowe:

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   Upewnij się, że ustawienie **Zezwalaj na dostęp do usług platformy Azure** jest włączone dla serwera baz danych SQL. W celu sprawdzenia i włączenia wykonaj następujące kroki:

    1. Zaloguj się do witryny [Azure Portal](https://portal.azure.com).
    2. Kliknij pozycję **Więcej usług >** po lewej stronie i kliknij **Serwery SQL** w kategorii **BAZY DANYCH**.
    3. Wybierz serwer z listy serwerów SQL.
    4. W bloku serwera SQL kliknij link **Pokaż ustawienia zapory**.
    5. W bloku **Ustawienia zapory** kliknij pozycję **WŁĄCZ** dla ustawienia **Zezwalaj na dostęp do usług Azure**.
    6. Kliknij przycisk **Zapisz** na pasku narzędzi. 

## <a name="create-datasets"></a>Tworzenie zestawów danych
W poprzednim kroku zostały utworzone połączone usługi używane do połączenia konta usługi Azure Storage i bazy danych Azure SQL z fabryką danych. W tym kroku zostaną zdefiniowane dwa zestawy danych o nazwach InputDataset i OutputDataset zawierające dane wejściowe i wyjściowe przechowywane w magazynach danych, do których odwołują się usługi AzureStorageLinkedService i AzureSqlLinkedService.

Połączona usługa magazynu Azure określa parametry połączenia, z których korzysta usługa Data Factory w czasie wykonywania, aby połączyć się z kontem magazynu Azure. Natomiast wejściowy zestaw danych obiektów blob (InputDataset) określa kontener oraz folder, który zawiera dane wejściowe.  

W analogiczny sposób połączona usługa Azure SQL Database określa parametry połączenia, z których korzysta usługa Data Factory w czasie wykonywania, aby połączyć się z bazą danych SQL usługi Azure. Wyjściowy zestaw danych tabeli SQL (OutputDataset) określa tabelę w bazie danych, do której są kopiowane dane z magazynu obiektów blob. 

### <a name="create-an-input-dataset"></a>Tworzenie wejściowego zestawu danych
W tym kroku opisano tworzenie zestawu danych o nazwie InputDataset wskazującego na plik obiektów blob (emp.txt) w katalogu głównym kontenera obiektów blob (adftutorial) w usłudze Azure Storage reprezentowany przez połączoną usługę AzureStorageLinkedService. Jeśli nie określisz wartości obiektu fileName lub ją pominiesz, dane ze wszystkich obiektów blob w folderze wejściowym zostaną skopiowane do lokalizacji docelowej. W tym samouczku wartość obiektu fileName jest określona.  

1. Utwórz plik JSON o nazwie **InputDataset.json** w folderze **C:\ADFGetStartedPSH** o następującej zawartości:

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

    Poniższa tabela zawiera opis właściwości kodu JSON użytych w tym fragmencie kodu:

    | Właściwość | Opis |
    |:--- |:--- |
    | type | Właściwość typu jest ustawiona na wartość **AzureBlob**, ponieważ dane znajdują się w magazynie obiektów blob na platformie Azure. |
    | linkedServiceName | Odnosi się do utworzonego wcześniej elementu **AzureStorageLinkedService**. |
    | folderPath | Określa **kontener** obiektów blob oraz **folder**, który zawiera wejściowe obiekty blob. W tym samouczku kontenerem obiektów blob jest adftutorial, a folderem — katalog główny. | 
    | fileName | Ta właściwość jest opcjonalna. Jeśli pominiesz tę właściwość, zostaną wybrane wszystkie pliki z folderu folderPath. W tym samouczku dla fileName określono plik **emp.txt**, więc tylko on zostanie wybrany do przetwarzania. |
    | format -> type |Plik wejściowy jest w formacie tekstowym, więc należy użyć właściwości **TextFormat**. |
    | columnDelimiter | Kolumny w pliku wejściowym są rozdzielane **przecinkami (`,`)**. |
    | frequency/interval | Właściwość frequency (częstotliwość) jest ustawiona na wartość **Hour** (Godzina), a wartość interwału wynosi **1**, co oznacza, że wycinki wejściowe są dostępne **co godzinę**. Innymi słowy, usługa Data Factory szuka danych wejściowych co godzinę w folderze głównym określonego kontenera obiektów blob (**adftutorial**). Wyszukuje dane między godzinami rozpoczęcia i zakończenia potoku, a nie przed nimi ani po nich.  |
    | external | Ta właściwość ma wartość **true** (prawda), jeśli dane nie są generowane przez ten potok. Dane wejściowe w tym samouczku znajdują się w pliku emp.txt, który nie jest generowany w tym potoku, więc możemy ustawić tę właściwość na true. |

    Aby uzyskać więcej informacji o tych właściwościach JSON, zobacz [artykuł dotyczący łącznika obiektu blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties).
2. Uruchom następujące polecenie, aby utworzyć zestaw danych usługi Fabryka danych.

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    Oto przykładowe dane wyjściowe:

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
W tej części kroku tworzony jest wyjściowy zestaw danych o nazwie **OutputDataset**. Ten zestaw danych wskazuje tabelę SQL w bazie danych SQL Azure reprezentowanej przez usługę **AzureSqlLinkedService**. 

1. Utwórz plik JSON o nazwie **OutputDataset.json** w folderze **C:\ADFGetStartedPSH** o następującej zawartości:

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

    Poniższa tabela zawiera opis właściwości kodu JSON użytych w tym fragmencie kodu:

    | Właściwość | Opis |
    |:--- |:--- |
    | type | Właściwość typu jest ustawiona na **AzureSqlTable**, ponieważ dane są kopiowane do tabeli w bazie danych SQL na platformie Azure. |
    | linkedServiceName | Odnosi się do utworzonego wcześniej elementu **AzureSqlLinkedService**. |
    | tableName | Określa **tabelę** , do której są kopiowane dane. | 
    | frequency/interval | Właściwość frequency (częstotliwość) jest ustawiona na wartość **Hour** (Godzina), a wartość interwału wynosi **1**, co oznacza, że wycinki wyjściowe są tworzone **co godzinę** między godziną rozpoczęcia i zakończenia potoku, a nie przed tą godziną lub po niej.  |

    Tabela emp bazy danych zawiera trzy kolumny — **ID**, **FirstName** i **LastName**. ID to kolumna tożsamości, więc należy określić tylko wartości **FirstName** i **LastName**.

    Aby uzyskać więcej informacji o tych właściwościach JSON, zobacz [artykuł dotyczący łącznika usługi Azure SQL](data-factory-azure-sql-connector.md#dataset-properties).
2. Uruchom następujące polecenie, aby utworzyć zestaw danych fabryki danych.

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    Oto przykładowe dane wyjściowe:

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

Obecnie harmonogram jest prowadzony przy użyciu wyjściowego zestawu danych. W tym samouczku wyjściowy zestaw danych jest konfigurowany do tworzenia wycinka co godzinę. Potok ma godzinę rozpoczęcia i zakończenia, między którymi następuje jeden dzień różnicy (dokładnie 24 godziny). Potok tworzy więc 24 wycinki wyjściowego zestawu danych. 


1. Utwórz plik JSON o nazwie **ADFTutorialPipeline.json** w folderze **C:\ADFGetStartedPSH** o następującej zawartości:

    ```json   
    {
      "name": "ADFTutorialPipeline",
      "properties": {
        "description": "Copy data from a blob to Azure SQL table",
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
    Pamiętaj o następujących kwestiach:
   
    - W sekcji działań jest tylko jedno działanie, którego parametr **type** (typ) został ustawiony na wartość **Copy**. Więcej informacji o działaniu kopiowania znajduje się w artykule dotyczącym [działań związanych z przenoszeniem danych](data-factory-data-movement-activities.md). W rozwiązaniach usługi Data Factory można również użyć [działań dotyczących przekształcania danych](data-factory-data-transformation-activities.md).
    - Dane wejściowe dla działania mają ustawienie **InputDataset**, a dane wyjściowe — **OutputDataset**. 
    - W sekcji **typeProperties** parametr **BlobSource** został określony jako typ źródłowy, a parametr **SqlSink** został określony jako typ ujścia. Aby uzyskać pełną listę magazynów danych obsługiwanych przez działanie kopiowania jako źródła i ujścia, zobacz informacje dotyczące [obsługiwanych magazynów danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Aby dowiedzieć się, jak używać określonego obsługiwanego magazynu danych jako źródła/ujścia, kliknij link w tabeli.  
     
    Zastąp wartość właściwości **start** datą bieżącą, a wartość **end** datą jutrzejszą. Możesz określić tylko część daty i pominąć część godziny parametru data/godzina. Na przykład „2016-02-03” jest odpowiednikiem „2016-02-03T00:00:00Z”.
     
    Zarówno data/godzina rozpoczęcia, jak i data/godzina zakończenia muszą być w [formacie ISO](http://en.wikipedia.org/wiki/ISO_8601). Przykładowo: 2016-10-14T16:32:41Z. Czas **end** jest opcjonalny, ale w tym samouczku zostanie użyty. 
     
    Jeśli nie określisz wartości dla właściwości **end**, zostanie ona obliczona jako „**czas rozpoczęcia + 48 godzin**”. Aby uruchomić potok bezterminowo, określ **9999-09-09** jako wartość właściwości **end**.
     
    W powyższym przykładzie występują 24 wycinki danych, gdyż poszczególne wycinki są generowane co godzinę.

    Opisy właściwości JSON w definicji potoku znajdują się w artykule dotyczącym [tworzenia potoków](data-factory-create-pipelines.md). Opisy właściwości JSON w definicji działania kopiowania znajdują się w artykule dotyczącym [działań związanych z przenoszeniem danych](data-factory-data-movement-activities.md). Opisy właściwości JSON obsługiwanych przez BlobSource można znaleźć w [artykule dotyczącym łącznika usługi Azure Blob](data-factory-azure-blob-connector.md). Opisy właściwości JSON obsługiwanych przez SqlSink można znaleźć w artykule [dotyczącym łącznika usługi Azure SQL Database](data-factory-azure-sql-connector.md).
2. Uruchom następujące polecenie, aby utworzyć tabelę fabryki danych.

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    Oto przykładowe dane wyjściowe: 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

**Gratulacje!** Fabryka danych Azure z potokiem kopiującym dane z usługi Azure Blob Storage do bazy danych Azure SQL została pomyślnie utworzona. 

## <a name="monitor-the-pipeline"></a>Monitorowanie potoku
W tym kroku opisano użycie programu Azure PowerShell do monitorowania tego, co dzieje się w fabryce danych platformy Azure.

1. Zastąp &lt;DataFactoryName&gt; nazwą fabryki danych i uruchom polecenie **Get-AzureRmDataFactory** oraz przypisz dane wyjściowe do zmiennej $df.

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    Na przykład:
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    Następnie uruchom polecenie Drukuj zawartość obszaru $df, aby wyświetlić następujące dane wyjściowe: 
    
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
2. Uruchom polecenie **Get-AzureRmDataFactorySlice**, aby uzyskać szczegółowe informacje na temat wszystkich wycinków elementu **OutputDataset**, który stanowi wyjściowy zestaw danych potoku.  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   To ustawienie powinno być zgodne z wartością właściwości **Start** w kodzie JSON potoku. Powinny zostać wyświetlone 24 wycinki, jeden dla każdej godziny od godz. 12: 00 bieżącego dnia do godz. 12: 00 dnia następnego.

   Poniżej przedstawiono trzy próbki wycinków z danych wyjściowych: 

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
3. Uruchom polecenie **Get-AzureRmDataFactoryRun**, aby uzyskać szczegółowe informacje o uruchomieniach działania dla **określonego** wycinka. Skopiuj wartość daty i godziny z danych wyjściowych poprzedniego polecenia, aby określić wartość dla parametru StartDateTime. 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   Oto przykładowe dane wyjściowe: 

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
W tym samouczku opisano tworzenie fabryki danych Azure w celu kopiowania danych z obiektu blob Azure do bazy danych SQL Azure. Program PowerShell został użyty do utworzenia fabryki danych, połączonych usług, zestawów danych oraz potoku. Główne kroki opisane w tym samouczku:  

1. Tworzenie **fabryki danych** Azure.
2. Tworzenie **połączonych usług**:

   a. Połączona usługa **Azure Storage** w celu połączenia z kontem usługi Azure Storage, na którym przechowywane są dane wejściowe.     
   b. Połączona usługa **SQL Azure** w celu połączenia z bazą danych SQL, w której przechowywane są dane wyjściowe.
3. Tworzenie **zestawów danych** opisujących dane wejściowe i wyjściowe dla potoków.
4. Tworzenie **potoku** za pomocą **działania kopiowania**, w którym źródłem jest element **BlobSource**, a ujściem element **SqlSink**.

## <a name="next-steps"></a>Następne kroki
W tym samouczku użyto magazynu obiektów blob platformy Azure jako magazynu danych źródła oraz bazy danych SQL na platformie Azure jako magazynu danych docelowych w operacji kopiowania. Poniższa tabela zawiera listę magazynów danych obsługiwanych przez działanie kopiowania jako źródła i lokalizacje docelowe: 

[!INCLUDE [data-factory-supported-data-stores](../../../includes/data-factory-supported-data-stores.md)]

Aby uzyskać informacje dotyczące kopiowania danych do/z magazynu danych, kliknij link do magazynu danych w tabeli. 

