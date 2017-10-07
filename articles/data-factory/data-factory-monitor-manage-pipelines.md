---
title: "aaaMonitor oraz zarządzanie nimi potoki hello portalu Azure i programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello portalu Azure i toomonitor programu Azure PowerShell i zarządzanie hello fabryki danych Azure i potoki, które zostały utworzone."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 9b0fdc59-5bbe-44d1-9ebc-8be14d44def9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: a8d3c7943e79450895ff754f06a37fdad1cbef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-azure-portal-and-powershell"></a>Monitorowanie i zarządzanie nimi potoki fabryki danych Azure przy użyciu programu PowerShell i hello portalu Azure
> [!div class="op_single_selector"]
> * [Przy użyciu portalu Azure/Azure PowerShell](data-factory-monitor-manage-pipelines.md)
> * [Przy użyciu monitorowania i zarządzania aplikacjami](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> Aplikacja Hello monitorowanie i zarządzanie zapewnia lepszą obsługę do monitorowania i zarządzania potoki Twoje dane i rozwiązywania problemów. Aby uzyskać informacje dotyczące korzystania z aplikacji hello, zobacz [monitorować i zarządzać nimi potoki fabryki danych przy użyciu aplikacji hello monitorowanie i zarządzanie](data-factory-monitor-manage-app.md). 


W tym artykule opisano sposób toomonitor, zarządzania i debugowania z potoków przy użyciu portalu Azure i programu PowerShell. Witaj artykuł zawiera również informacje dotyczące sposobu toocreate alertów i pobrać powiadamiany o niepowodzeniach.

## <a name="understand-pipelines-and-activity-states"></a>Potoki i stanów działania
Za pomocą hello portalu Azure, możesz:

* Wyświetl fabrykę danych jako diagram.
* Przeglądanie działań w potoku.
* Umożliwia wyświetlanie zestawów danych wejściowych i wyjściowych.

W tej sekcji opisano również sposób przejścia wycinek zestawu danych z jednego stanu tooanother.   

### <a name="navigate-tooyour-data-factory"></a>Przejdź tooyour fabryki danych
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Kliknij przycisk **fabryki danych** menu hello powitania po lewej stronie. Jeśli nie widzisz, kliknij przycisk **więcej usług >**, a następnie kliknij przycisk **fabryki danych** w obszarze hello **analizy i analiza** kategorii.

   ![Przeglądaj wszystkie > fabryki danych](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. Na powitania **fabryki danych** bloku, wybierz hello fabryki danych, która Cię.

    ![Wybierz usługi fabryka danych](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   Powinna zostać wyświetlona strona główna hello hello fabryki danych.

   ![Blok fabryki danych](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a>Widok diagramu w fabryce danych
Witaj **Diagram** widok fabryki danych zapewnia jeden z toomonitor szkła i zarządzanie hello fabryki danych i jego zasoby. Witaj toosee **Diagram** wyświetlić w fabryce danych, kliknij przycisk **Diagram** na stronie głównej hello hello fabryki danych.

![Widok diagramu](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

Można powiększać, pomniejszyć toofit powiększenia, powiększenia too100%, blokady hello układu diagramu hello i automatycznie rozmieszczaj potoki i zestawów danych. Możesz również sprawdzić hello danych elementy powiązane informacje (to znaczy Pokaż elementy nadrzędne i podrzędne wybranego elementu).

### <a name="activities-inside-a-pipeline"></a>Działania w potoku
1. Kliknij prawym przyciskiem myszy hello potok, a następnie kliknij przycisk **Otwórz potoku** toosee wszystkie działania w hello w potoku, wraz z zestawów danych wejściowych i wyjściowych dla działania hello. Ta funkcja jest przydatna w przypadku potoku sieci zawiera więcej niż jedno działanie toounderstand hello operacyjne elementy powiązane z pojedynczy potok.

    ![Menu Otwórz potok](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. Poniższy przykład hello jest widoczny działanie kopiowania w potoku hello z danych wejściowych i wyjściowych. 

    ![Działania w potoku](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. Strona główna toohello wstecz hello fabryki danych można przejść, klikając hello **fabryki danych** łącze w nadrzędnych hello na powitania lewego górnego rogu.

    ![Przejdź wstecz toodata fabryki](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-hello-state-of-each-activity-inside-a-pipeline"></a>Widok stanu hello każdego działania w potoku
Można wyświetlić hello bieżący stan działania, wyświetlając stan hello dowolnego hello zestawów danych, które są generowane przez działanie hello.

Klikając dwukrotnie hello **OutputBlobTable** w hello **Diagram**, można wyświetlić wszystkie fragmenty hello, które są tworzone przez uruchamia innej aktywności w potoku. Widoczne czy działanie kopiowania hello został uruchomiony pomyślnie na powitania ostatnich ośmiu godzinach i wyprodukowanych hello wycinki hello **gotowe** stanu.  

![Stan potoku hello](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

Witaj wycinków zestaw danych w fabryce danych hello może mieć jeden z hello następujące stany:

<table>
<tr>
    <th align="left">Stan</th><th align="left">Substrat</th><th align="left">Opis</th>
</tr>
<tr>
    <td rowspan="8">Oczekiwanie</td><td>ScheduleTime</td><td>czas Hello nie pochodzą dla hello toorun wycinka.</td>
</tr>
<tr>
<td>DatasetDependencies</td><td>zależności strumienia wychodzącego Hello nie są gotowe.</td>
</tr>
<tr>
<td>ComputeResources</td><td>zasoby obliczeniowe Hello nie są dostępne.</td>
</tr>
<tr>
<td>ConcurrencyLimit</td> <td>Wszystkie wystąpienia działania hello są zajęte uruchamianiem innych wycinków.</td>
</tr>
<tr>
<td>ActivityResume</td><td>działanie Hello jest wstrzymane i nie można uruchomić hello wycinków, dopóki nie zostanie wznowione hello działania.</td>
</tr>
<tr>
<td>Spróbuj ponownie</td><td>Ponawiane wykonania działania.</td>
</tr>
<tr>
<td>Walidacja</td><td>Weryfikacja jeszcze się nie rozpoczął.</td>
</tr>
<tr>
<td>ValidationRetry</td><td>Sprawdzanie poprawności jest ponowione toobe oczekiwania.</td>
</tr>
<tr>
<tr>
<td rowspan="2">W toku</td><td>Sprawdzanie poprawności</td><td>Trwa sprawdzanie poprawności.</td>
</tr>
<td>-</td>
<td>Witaj wycinek jest przetwarzany.</td>
</tr>
<tr>
<td rowspan="4">Nie powiodło się</td><td>Upłynął limit czasu</td><td>Witaj działania wykonywanie trwało dłużej niż jest dozwolonych przez działanie hello.</td>
</tr>
<tr>
<td>Anulowane</td><td>wycinek Hello zostało anulowane przez akcję użytkownika.</td>
</tr>
<tr>
<td>Walidacja</td><td>Weryfikacja nie powiodła się.</td>
</tr>
<tr>
<td>-</td><td>wycinek Hello nie toobe wygenerowany i/lub sprawdzić poprawności.</td>
</tr>
<td>Gotowe</td><td>-</td><td>Witaj wycinek jest gotowy do użycia.</td>
</tr>
<tr>
<td>Pominięto</td><td>Brak</td><td>wycinek Hello nie jest przetwarzane.</td>
</tr>
<tr>
<td>Brak</td><td>-</td><td>Wycinek używane tooexist inny stan, ale został zresetowany.</td>
</tr>
</table>



Szczegóły hello wycinek można wyświetlić, klikając wpisem wycinka na powitania **ostatnio zaktualizowano wycinków** bloku.

![Szczegóły wycinka](./media/data-factory-monitor-manage-pipelines/slice-details.png)

Jeśli wykonano wycinek hello wiele razy, zobacz wielu wierszy hello **odbywa się działanie** listy. Można wyświetlić szczegółowe informacje o działaniu uruchomić, klikając polecenie wpisu hello Uruchom hello **odbywa się działanie** listy. Witaj lista zawiera wszystkie pliki dziennika hello, oraz komunikat o błędzie, jeśli istnieje. Ta funkcja jest przydatna dzienniki tooview i debugowania, bez konieczności tooleave z fabryką danych.

![Szczegóły uruchamiania działania](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

Jeśli nie ma wycinek hello hello **gotowe** stanu, można zobaczyć hello niegotowe wycinki strumienia wychodzącego nie są gotowe i blokuje hello bieżący fragment wykonywanie w hello **wycinków strumienia wychodzącego, które nie są gotowe** listy. Ta funkcja jest przydatna, gdy Twoje wycinka **oczekiwania** stanu, a ma toounderstand hello nadrzędnego zależności, które hello wycinek oczekuje na.

![Niegotowe wycinki strumienia wychodzącego](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a>Diagram stanu zestawu danych
Po wdrożeniu fabryki danych i potoki hello ma nieprawidłowy okres aktywności, zestaw danych hello wycinków przejście od jednego stanu tooanother. Obecnie stanu wycinka hello następujące powitania po diagram stanu:

![Diagram stanu](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

Hello przepływ przejścia stanu zestawu danych w fabryce danych jest następujące hello: oczekiwania -> w toku/w toku (sprawdzania) -> gotowe/nie powiodło się.

wycinek Hello jest uruchamiany w **oczekiwania** stanu oczekiwania na toobe warunki wstępne zostały spełnione przed rozpoczęciem wykonywania. Następnie rozpoczęciem wykonywania działania hello i wycinek hello przechodzi w stan **w toku** stanu. wykonanie działania Hello może powodzenie lub niepowodzenie. wycinek Hello jest oznaczony jako **gotowe** lub **nie powiodło się**, na podstawie wyniku hello hello wykonywania.

Można zresetować toogo wycinka powitania od hello **gotowe** lub **** toohello stanu **oczekiwania** stanu. Można również oznaczyć stanu wycinka hello zbyt**Pomiń**, co uniemożliwia działania hello wykonywania i nie przetwarza hello wycinka.

## <a name="pause-and-resume-pipelines"></a>Wstrzymywanie i wznawianie potoki
Twoje potoki można zarządzać za pomocą programu Azure PowerShell. Na przykład można wstrzymywać i wznawiać potoki przez uruchomienie polecenia cmdlet programu Azure PowerShell przez użytkownika. 

> [!NOTE] 
> Widok diagramu Hello nie obsługuje wstrzymywanie i wznawianie potoków. Toouse interfejsu użytkownika, należy użyć hello monitorowanie i zarządzanie aplikacji. Aby uzyskać informacje dotyczące korzystania z aplikacji hello, zobacz [monitorować i zarządzać nimi potoki fabryki danych przy użyciu aplikacji hello monitorowanie i zarządzanie](data-factory-monitor-manage-app.md) artykułu. 

Można Wstrzymaj/zawiesić potoki przy użyciu hello **Suspend-AzureRmDataFactoryPipeline** polecenia cmdlet programu PowerShell. To polecenie cmdlet jest przydatne, gdy nie chcesz toorun Twojego potoki dopóki problem nie zostanie rozwiązany. 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
Na przykład:

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

Po hello problem został rozwiązany z potoku hello, można wznowić zawieszone hello potoku, uruchamiając następujące polecenia programu PowerShell hello:

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
Na przykład:

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a>Debugowanie potoki
Fabryka danych Azure udostępnia bogate możliwości dla Ciebie toodebug i rozwiązywania problemów z potoków, za pomocą hello portalu Azure i programu Azure PowerShell.

> [! [Uwaga} jest znacznie łatwiejsze tootroubleshot, który błędów za pomocą Witaj, monitorowania i aplikacji do zarządzania. Aby uzyskać informacje dotyczące korzystania z aplikacji hello, zobacz [monitorować i zarządzać nimi potoki fabryki danych przy użyciu aplikacji hello monitorowanie i zarządzanie](data-factory-monitor-manage-app.md) artykułu. 

### <a name="find-errors-in-a-pipeline"></a>Znaleziono błędów w potoku
W przypadku niepowodzenia uruchomienia działania hello w potoku zestawu danych hello, który jest generowany przez potok hello jest w stanie błędu z powodu błędu hello. Można debugować i rozwiązywanie problemów z fabryki danych Azure przy użyciu następujących metod hello.

#### <a name="use-hello-azure-portal-toodebug-an-error"></a>Użyj hello toodebug portalu Azure wystąpił błąd
1. Na powitania **tabeli** bloku, kliknij hello problem wycinek, który ma hello **stan** ustawić także****.

   ![Blok tabeli z wycinka problem](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. Na powitania **wycinka danych** bloku, kliknij działanie hello uruchamiania, która nie powiodła się.

   ![Wycinek danych z powodu błędu](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. Na powitania **szczegóły uruchomienia działania** bloku, możesz pobrać hello pliki, które są skojarzone z hello HDInsight przetwarzania. Kliknij przycisk **Pobierz** dla stanu/stderr toodownload hello pliku dziennika błędów, który zawiera szczegółowe informacje o błędzie hello.

   ![Działanie Uruchom szczegóły blok z powodu błędu](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-toodebug-an-error"></a>Użyj programu PowerShell toodebug błąd
1. Uruchom program **PowerShell**.
2. Uruchom hello **Get-AzureRmDataFactorySlice** polecenia wycinków hello toosee i ich Stany. Powinny pojawić się wycinek ze stanem hello ****.        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   Na przykład:

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   Zastąp **StartDateTime** czas rozpoczęcia z potoku. 
3. Teraz uruchom hello **Get AzureRmDataFactoryRun** Uruchom polecenia cmdlet tooget szczegóły dotyczące działania hello hello wycinka.

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    Na przykład:

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    wartość Hello StartDateTime jest czas rozpoczęcia hello hello błąd/problem wycinek, który zauważyć hello w poprzednim kroku. Witaj daty i godziny należy ująć w podwójny cudzysłów.
4. Powinny pojawić się dane wyjściowe ze szczegółami hello błędu, który jest podobne toohello poniżej:

    ```   
    Id                      : 841b77c9-d56c-48d1-99a3-8c16c3e77d39
    ResourceGroupName       : ADF
    DataFactoryName         : LogProcessingFactory3
    DatasetName               : EnrichedGameEventsTable
    ProcessingStartTime     : 10/10/2014 3:04:52 AM
    ProcessingEndTime       : 10/10/2014 3:06:49 AM
    PercentComplete         : 0
    DataSliceStart          : 5/5/2014 12:00:00 AM
    DataSliceEnd            : 5/6/2014 12:00:00 AM
    Status                  : FailedExecution
    Timestamp               : 10/10/2014 3:04:52 AM
    RetryAttempt            : 0
    Properties              : {}
    ErrorMessage            : Pig script failed with exit code '5'. See wasb://        adfjobs@spestore.blob.core.windows.net/PigQuery
                                    Jobs/841b77c9-d56c-48d1-99a3-
                8c16c3e77d39/10_10_2014_03_04_53_277/Status/stderr' for
                more details.
    ActivityName            : PigEnrichLogs
    PipelineName            : EnrichGameLogsPipeline
    Type                    :
    ```
5. Możesz uruchomić hello **AzureRmDataFactoryLog Zapisz** polecenia cmdlet z hello wartość identyfikatora Zobacz z danych wyjściowych hello i pobierania plików dziennika hello za pomocą hello **- DownloadLogsoption** hello polecenia cmdlet.

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a>Uruchom ponownie błędów w potoku

> [!IMPORTANT]
> Jest łatwiejsze tootroubleshoot błędów i uruchom ponownie zakończone niepowodzeniem wycinków przy użyciu hello monitorowanie & aplikacji do zarządzania. Aby uzyskać informacje dotyczące korzystania z aplikacji hello, zobacz [monitorować i zarządzać nimi potoki fabryki danych przy użyciu aplikacji hello monitorowanie i zarządzanie](data-factory-monitor-manage-app.md). 

### <a name="use-hello-azure-portal"></a>Użyj hello portalu Azure
Po Rozwiązywanie problemów i debugowanie błędów w potoku, należy ponownie uruchomić błędów przechodząc toohello błąd wycinka i klikając hello **Uruchom** przycisk na powitania paska poleceń.

![Uruchom ponownie wycinek nie powiodło się](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

W przypadku wycinek hello Weryfikacja nie powiodła się z powodu błędu zasad (na przykład, jeśli dane są niedostępne), można naprawić błąd hello i ponownie zweryfikować, klikając hello **weryfikacji** przycisk na powitania paska poleceń.

![Usuń błędy i sprawdzania poprawności](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a>Korzystanie z programu Azure PowerShell
Uruchom ponownie błędów przy użyciu hello **AzureRmDataFactorySliceStatus zestaw** polecenia cmdlet. Zobacz hello [AzureRmDataFactorySliceStatus zestaw](https://msdn.microsoft.com/library/mt603522.aspx) temat o składni i inne szczegółowe informacje o hello polecenia cmdlet.

**Przykład:**

Witaj poniższy przykład przedstawia stan wszystkich fragmentów hello tabeli "DAWikiAggregatedData" too'Waiting hello "w fabryce danych Azure hello"WikiADF".

Witaj "Typ aktualizacji" ustawiono too'UpstreamInPipeline ", co oznacza, że stanów każdy wycinek dla tabeli hello i wszystkie hello zależne tabele (nadrzędnego) są ustawione too'Waiting". Witaj inne możliwe wartości tego parametru to "Indywidualny".

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a>Tworzenie alertów
Azure dzienniki zdarzeń użytkownika podczas zasobów platformy Azure (na przykład fabryka danych) jest utworzone, zaktualizować lub usunąć. Alerty można tworzyć na te zdarzenia. Można użyć różnych metryk toocapture fabryki danych i tworzenie alertów na metryki. Firma Microsoft zaleca używanie zdarzeń monitorowania w czasie rzeczywistym i metryki w celach historycznych.

### <a name="alerts-on-events"></a>Alerty dotyczące zdarzeń
Zdarzenia Azure udostępniają przydatne wgląd w działania wykonywane w zasobów platformy Azure. Podczas korzystania z fabryki danych Azure, zdarzenia są generowane, gdy:

* Fabryka danych jest utworzone, zaktualizować lub usunąć.
* Przetwarzanie danych (jako "działa") został uruchomiony lub zakończona.
* Klaster usługi HDInsight na żądanie jest utworzone lub usunięte.

Możesz tworzyć alerty dotyczące tych zdarzeń użytkownika i je skonfigurować, administrator toohello powiadomienia e-mail toosend i coadministrators hello subskrypcji. Ponadto można określić adresy e-mail dodatkowych użytkowników, którzy potrzebują tooreceive powiadomienia e-mail, gdy są spełnione warunki hello. Ta funkcja jest przydatne, gdy mają tooget powiadomienie dotyczące niepowodzeń i nie mają toocontinuously monitor fabrykę danych.

> [!NOTE]
> Obecnie hello portal nie wyświetla alerty dotyczące zdarzeń. Użyj hello [zarządzania i monitorowania aplikacji](data-factory-monitor-manage-app.md) toosee wszystkie alerty.


#### <a name="specify-an-alert-definition"></a>Określ definicję alertu
toospecify definicji alertu, tworzenie pliku JSON, który opisuje hello operacje, które chcesz toobe alerty o. W hello poniższy przykład hello alert wysyła wiadomość e-mail z powiadomieniem do hello RunFinished operacji. toobe określonych, powiadomienie e-mail są wysyłane podczas wykonywania w fabryce danych hello zostało ukończone i hello uruchomienie nie powiodło się (stan = FailedExecution).

```JSON
{
    "contentVersion": "1.0.0.0",
     "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters": {},
    "resources":
    [
        {
            "name": "ADFAlertsSlice",
            "type": "microsoft.insights/alertrules",
            "apiVersion": "2014-04-01",
            "location": "East US",
            "properties":
            {
                "name": "ADFAlertsSlice",
                "description": "One or more of hello data slices for hello Azure Data Factory has failed processing.",
                "isEnabled": true,
                "condition":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.ManagementEventRuleCondition",
                    "dataSource":
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleManagementEventDataSource",
                        "operationName": "RunFinished",
                        "status": "Failed",
                        "subStatus": "FailedExecution"   
                    }
                },
                "action":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails": [ "<your alias>@contoso.com" ]
                }
            }
        }
    ]
}
```

Możesz usunąć **podstanu** z hello definicji JSON, jeśli nie chcesz toobe alerty na określony błąd.

Ten przykład konfiguruje hello alert dla wszystkich fabryki danych w ramach subskrypcji. Jeśli chcesz hello toobe alertów dla fabryki danych, można określić fabryki danych **resourceUri** w hello **źródła danych**:

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

Witaj Poniższa tabela zawiera listę hello dostępne operacje, Stany (i podstany).

| Nazwa operacji | Stan | Podstan |
| --- | --- | --- |
| RunStarted |Rozpoczęto |Uruchamianie |
| RunFinished |Nie powiodło się / powiodło się. |FailedResourceAllocation<br/><br/>Powodzenie<br/><br/>FailedExecution<br/><br/>Upłynął limit czasu<br/><br/>< anulowane<br/><br/>FailedValidation<br/><br/>porzucone |
| OnDemandClusterCreateStarted |Rozpoczęto | |
| OnDemandClusterCreateSuccessful |Powodzenie | |
| OnDemandClusterDeleted |Powodzenie | |

Zobacz [Tworzenie reguły alertu](https://msdn.microsoft.com/library/azure/dn510366.aspx) szczegółowe informacje o hello elementy JSON, które są używane w przykładzie hello.

#### <a name="deploy-hello-alert"></a>Wdrażanie hello alertu
alert hello toodeploy, polecenia cmdlet programu Azure PowerShell służącego do hello **AzureRmResourceGroupDeployment nowy**, jak pokazano w hello poniższy przykład:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

Po wdrożenie grupy zasobów hello zakończyło się pomyślnie, zostanie wyświetlony hello następujące komunikaty:

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - hello StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts tooremove this parameter.
VERBOSE: 7:00:49 PM - Create template deployment 'ADFAlertFailedSlice'.
VERBOSE: 7:00:57 PM - Resource microsoft.insights/alertrules 'ADFAlertsSlice' provisioning status is succeeded

DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

> [!NOTE]
> Można użyć hello [Tworzenie reguły alertu](https://msdn.microsoft.com/library/azure/dn510366.aspx) toocreate interfejsu API REST regułę alertu. ładunek JSON Hello jest podobny przykład JSON toohello.  


#### <a name="retrieve-hello-list-of-azure-resource-group-deployments"></a>Pobieranie listy hello wdrożeń grupy zasobów platformy Azure
Lista hello tooretrieve wdrożone wdrożenia grupy zasobów platformy Azure, użyj polecenia cmdlet hello **Get-AzureRmResourceGroupDeployment**, jak pokazano w hello poniższy przykład:

```powershell
Get-AzureRmResourceGroupDeployment -ResourceGroupName adf
```

```
DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

#### <a name="troubleshoot-user-events"></a>Obsługa zdarzeń użytkownika
1. Można wyświetlić wszystkie zdarzenia hello, które są generowane po kliknięciu przycisku hello **metryki i operacje** kafelka.

    ![Kafelek metryki i operacje](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. Kliknij przycisk hello **zdarzenia** kafelka toosee hello zdarzenia.

    ![Kafelek zdarzenia](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. Na powitania **zdarzenia** bloku można zobaczyć szczegółowe informacje dotyczące zdarzeń, zdarzeń filtrowane i tak dalej.

    ![Blok zdarzenia](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. Kliknij przycisk **operacji** hello operacje listy, które powoduje błąd.

    ![Wybierz operację](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. Kliknij przycisk **błąd** zdarzenia toosee szczegóły błędu hello.

    ![Błąd zdarzenia](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

Zobacz [poleceń cmdlet Azure wglądu](https://msdn.microsoft.com/library/mt282452.aspx) dla poleceń cmdlet programu PowerShell służącego tooadd, pobrać lub usunąć alerty. Oto kilka przykładów użycia hello **Get-AlertRule** polecenia cmdlet:

```powershell
get-alertrule -res $resourceGroup -n ADFAlertsSlice -det
```

```
Properties :
Action      : Microsoft.Azure.Management.Insights.Models.RuleEmailAction
Condition   :
DataSource :
EventName             :
Category              :
Level                 :
OperationName         : RunFinished
ResourceGroupName     :
ResourceProviderName  :
ResourceId            :
Status                : Failed
SubStatus             : FailedExecution
Claims                : Microsoft.Azure.Management.Insights.Models.RuleManagementEventClaimsDataSource
Condition      :
Description : One or more of hello data slices for hello Azure Data Factory has failed processing.
Status      : Enabled
Name:       : ADFAlertsSlice
Tags       :
$type          : Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/ADFAlertsSlice
Location   : West US
Name       : ADFAlertsSlice
```

```powershell
Get-AlertRule -res $resourceGroup
```
```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0

Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest3
Location   : West US
Name       : FailedExecutionRunsWest3
```

```powershell
Get-AlertRule -res $resourceGroup -Name FailedExecutionRunsWest0
```

```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0
```

Uruchom następujące szczegóły toosee polecenia get-help i przykłady dotyczące polecenia cmdlet Get-AlertRule hello hello.

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


Jeśli zostanie wyświetlony na powitania Generowanie alertów zdarzeń hello bloku portalu, ale nie otrzymywać powiadomienia pocztą e-mail, sprawdź, czy określonego adresu e-mail hello ustawiono tooreceive wiadomości e-mail od nadawców zewnętrznych. wiadomości e-mail alertów Hello może zostały zablokowane przez ustawienia poczty e-mail.

### <a name="alerts-on-metrics"></a>Alerty dotyczące metryk
W fabryce danych można przechwytywać różnych metryk i tworzyć alerty na metryki. Można monitorować i tworzyć alerty na powitania po metryki wycinki hello w fabryce danych:

* **Uruchamia nie powiodło się**
* **Uruchamia się pomyślnie**

Te metryki są przydatne i ułatwiają tooget omówienie ogólnej nie powiodło się i pomyślnego uruchomienia w fabryce danych hello. Metryki są emitowane w każdym użyciu uruchomienia wycinka. Na początku hello hello godzinę, te metryki są agregowane i wypychana tooyour konta magazynu. metryki tooenable, skonfiguruj konta magazynu.

#### <a name="enable-metrics"></a>Włączyć metryki
tooenable metryki, kliknij poniżej hello z hello **fabryki danych** bloku:

**Monitorowanie** > **Metryka** > **ustawień diagnostycznych** > **diagnostyki**

![Łącze diagnostyki](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

Na powitania **diagnostyki** bloku, kliknij przycisk **na**, wybierz konto magazynu hello i kliknij przycisk **zapisać**.

![Diagnostyka bloku](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

Może potrwać godzinę tooone toobe metryki hello widoczne na powitania **monitorowanie** bloku ponieważ agregacji metryki się stanie, co godzinę.

### <a name="set-up-an-alert-on-metrics"></a>Konfigurowanie alertu na metryk
Kliknij przycisk hello **fabryki danych metryki** Kafelek:

![Kafelek metryki fabryki danych](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

Na powitania **Metryka** bloku, kliknij przycisk **+ Dodaj alert** na powitania narzędzi.
![Blok metryki fabryki danych > Dodaj alert](./media/data-factory-monitor-manage-pipelines/add-alert.png)

Na powitania **dodać regułę alertu** hello następujące kroki, a kliknij pozycję **OK**.

* Wprowadź nazwę dla alertu hello (przykład: "nie powiodło się alert").
* Wprowadź opis alertu hello (przykład: "Wyślij wiadomość e-mail, gdy wystąpi błąd").
* Wybierz metrykę (vs "Działa nie powiodło się". "Pomyślne uruchomień").
* Określ warunek i wartość progową.   
* Określ hello okres czasu.
* Określ, czy mają być wysyłane wiadomości e-mail, tooowners, współautorzy i czytelnicy.

![Blok metryki fabryki danych > Dodaj regułę alertów](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

Po dodaniu reguły alertu hello pomyślnie, zamyka hello bloku i zostanie wyświetlony nowy alert hello na powitania **Metryka** bloku.

![Blok metryki fabryki danych > Nowy alert dodane](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

Powinno również zostać wyświetlone powitalne liczbę alertów w hello **reguły alertów** kafelka. Kliknij przycisk hello **reguły alertów** kafelka.

![Blok metryki fabryki danych — reguły alertów](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

Na powitania **alerty reguły** bloku, zobacz wszystkie istniejące alerty. tooadd alert, kliknij przycisk **Dodaj alert** na powitania narzędzi.

![Blok reguły alertów](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a>Powiadomienia o alertach
Po hello reguły alertu spełnia warunek hello, należy pobrać wiadomość e-mail z informacją, że hello alert jest aktywny. Po hello problem zostanie rozwiązany i hello warunku alertu nie jest już zgodny, otrzymasz wiadomość e-mail z informacją, że hello alert został rozwiązany.

To zachowanie różni się od zdarzenia wysyłania powiadomienia na każdy błąd, który regułę alertu kwalifikuje się do.

### <a name="deploy-alerts-by-using-powershell"></a>Wdrażanie alerty za pomocą programu PowerShell
Alerty można wdrożyć dla metryki hello sam sposób jak w przypadku zdarzeń.

**Definicja alertu**

```JSON
{
    "contentVersion" : "1.0.0.0",
    "$schema" : "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters" : {},
    "resources" : [
    {
            "name" : "FailedRunsGreaterThan5",
            "type" : "microsoft.insights/alertrules",
            "apiVersion" : "2014-04-01",
            "location" : "East US",
            "properties" : {
                "name" : "FailedRunsGreaterThan5",
                "description" : "Failed Runs greater than 5",
                "isEnabled" : true,
                "condition" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
                    "dataSource" : {
                        "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
                        "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
                        "resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName
>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>",
                        "metricName" : "FailedRuns"
                    },
                    "threshold" : 5.0,
                    "windowSize" : "PT3H",
                    "timeAggregation" : "Total"
                },
                "action" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails" : ["abhinav.gpt@live.com"]
                }
            }
        }
    ]
}
```

Zastąp *subscriptionId*, *resourceGroupName*, i *dataFactoryName* w przykładowym hello z odpowiednie wartości.

*metricName* obecnie obsługuje dwie wartości:

* FailedRuns
* SuccessfulRuns

**Wdrażanie hello alertu**

alert hello toodeploy, polecenia cmdlet programu Azure PowerShell służącego do hello **AzureRmResourceGroupDeployment nowy**, jak pokazano w hello poniższy przykład:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

Powinny pojawić się następujące komunikat po pomyślnym wdrożeniu:

```
VERBOSE: 12:52:47 PM - Template is valid.
VERBOSE: 12:52:48 PM - Create template deployment 'FailedRunsGreaterThan5'.
VERBOSE: 12:52:55 PM - Resource microsoft.insights/alertrules 'FailedRunsGreaterThan5' provisioning status is succeeded


DeploymentName    : FailedRunsGreaterThan5
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 7/27/2015 7:52:56 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           
```

Można również użyć hello **AlertRule Dodaj** toodeploy polecenia cmdlet reguły alertu. Zobacz hello [AlertRule Dodaj](https://msdn.microsoft.com/library/mt282468.aspx) tematu, aby uzyskać szczegółowe informacje i przykłady.  

## <a name="move-a-data-factory-tooa-different-resource-group-or-subscription"></a>Przenoszenie danych fabryki tooa innej grupie zasobów lub subskrypcji
Data factory tooa innej grupie zasobów lub różnych subskrypcji można przenieść za pomocą hello **Przenieś** polecenia paska przycisk na stronie głównej hello w fabryce danych.

![Przenieś fabryki danych](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

Można również przenosić powiązanych zasobów (takich jak alerty, które są skojarzone z fabryką danych hello), wraz z hello fabryki danych.

![Przenoszenie zasobów, okno dialogowe](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
