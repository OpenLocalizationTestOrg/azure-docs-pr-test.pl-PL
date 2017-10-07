---
title: "aaaMonitor i zarządzanie nimi zadania usługi analiza strumienia przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse toomonitor programu Azure PowerShell i polecenia cmdlet zadania usługi analiza strumienia i zarządzać nimi."
keywords: "Program Azure powershell, poleceń cmdlet programu azure powershell, polecenia programu powershell skryptów środowiska powershell"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 514f454e-d18c-4081-8304-ab48577e15e8
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 44abc82f1c44a5ebc1701badd6547b84dac239b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a>Monitorowanie i zarządzanie nimi zadania usługi analiza strumienia za pomocą poleceń cmdlet programu Azure PowerShell
Dowiedz się, jak toomonitor i zarządzanie zasobami usługi Stream Analytics za pomocą poleceń cmdlet programu Azure PowerShell i skryptów programu powershell, które wykonywać podstawowe zadania usługi analiza strumienia.

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a>Wymagania wstępne dotyczące uruchamiania poleceń cmdlet programu Azure PowerShell dla usługi analiza strumienia
* Utwórz grupy zasobów platformy Azure w ramach subskrypcji. Witaj poniżej znajduje się przykładowy skrypt programu PowerShell systemu Azure. Informacje programu Azure PowerShell, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview);  

Program Azure PowerShell 0.9.8:  

         # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

Program Azure PowerShell 1.0:  

         # Log in tooyour Azure account
        Login-AzureRmAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> Zadania usługi analiza strumienia utworzone programowo monitorowania, domyślnie nie jest konieczne.  Można ręcznie włączyć monitorowanie hello portalu Azure, przechodząc na stronę Monitor toohello zadania i kliknięcie przycisku Włącz hello, lub możesz to zrobić programowo, wykonując kroki hello znajdujący się w [Azure Stream Analytics — Monitor strumienia Analiza zadania programowo](stream-analytics-monitor-jobs.md).
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a>Azure poleceń cmdlet programu PowerShell dla usługi analiza strumienia
Hello następującego polecenia cmdlet programu Azure PowerShell można toomonitor używane i zarządzanie zadania usługi analiza strumienia Azure. Należy pamiętać, że programu Azure PowerShell ma różne wersje. 
**W przykładach hello pierwsze polecenie wymienionych hello jest przeznaczony dla programu Azure PowerShell 0.9.8 hello drugie polecenie jest Azure PowerShell 1.0.** polecenia Hello Azure PowerShell 1.0 zawsze będą mieć "AzureRM" hello polecenia.

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a>Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob
Wyświetla listę wszystkich zadań usługi Stream Analytics zdefiniowanej w hello subskrypcji platformy Azure lub określonej grupy zasobów lub pobiera informacje o zadaniu o konkretnym zadaniu w grupie zasobów.

**Przykład 1**

Program Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob

Program Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsJob

To polecenie programu PowerShell zwraca informacje o wszystkich zadań usługi Stream Analytics hello w hello subskrypcji platformy Azure.

**Przykład 2**

Program Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

Program Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

To polecenie programu PowerShell zwraca informacje o wszystkich zadań usługi Stream Analytics hello w grupie zasobów hello StreamAnalytics domyślne-centralnego-US.

**Przykład 3**

Program Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

Program Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

To polecenie programu PowerShell zwraca informacje o zadaniu Stream Analytics hello StreamingJob w grupie zasobów hello StreamAnalytics domyślne-centralnego-US.

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a>Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput
Wyświetla listę wszystkich danych wejściowych hello, które są zdefiniowane w określonym zadaniu Stream Analytics lub pobiera informacje o określone dane wejściowe.

**Przykład 1**

Program Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Program Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

To polecenie programu PowerShell zwraca informacje o wszystkich zdefiniowanych w zadaniu hello StreamingJob danych wejściowych hello.

**Przykład 2**

Program Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

Program Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

To polecenie programu PowerShell zwraca informacje o hello danych wejściowych o nazwie EntryStream zdefiniowane w zadaniu hello StreamingJob.

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a>Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput
Wyświetla listę wszystkich hello dane wyjściowe, które są zdefiniowane w określonym zadaniu Stream Analytics lub pobiera informacje o określonych danych wyjściowych.

**Przykład 1**

Program Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Program Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

To polecenie programu PowerShell zwraca informacje o danych wyjściowych hello zdefiniowane w zadaniu hello StreamingJob.

**Przykład 2**

Program Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

Program Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

To polecenie programu PowerShell zwraca informacje o danych wyjściowych hello o nazwie zdefiniowane w zadaniu hello StreamingJob danych wyjściowych.

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a>Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota
Pobiera informacje o przydziału hello przesyłania strumieniowego jednostki w określonym regionie.

**Przykład 1**

Program Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

Program Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

Tego polecenia programu PowerShell zwraca informacje o hello przydziału i użycia jednostek przesyłania strumieniowego w regionie środkowe stany USA hello.

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a>Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation
Pobiera informacje o określonych przekształcenia zdefiniowane w zadaniu Stream Analytics.

**Przykład 1**

Program Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

Program Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

To polecenie programu PowerShell zwraca informacje o transformacji hello o nazwie StreamingJob w zadaniu hello StreamingJob.

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a>Nowe AzureStreamAnalyticsInput | Nowe AzureRMStreamAnalyticsInput
Tworzy nowe dane wejściowe w zadaniu Stream Analytics, lub aktualizuje istniejące określone dane wejściowe.

Witaj danych wejściowych hello można określić w pliku JSON hello lub hello w wierszu polecenia. Jeśli określono oba nazwa hello w wierszu polecenia hello musi hello w taki sam jak jedną hello w pliku hello.

Jeśli Określ dane wejściowe, która już istnieje i nie określaj hello — parametru Force, polecenia cmdlet hello zapyta, czy tooreplace hello istniejących danych wejściowych.

Jeśli określisz hello — parametru Force i określ istniejącą wprowadź nazwę, wprowadzania hello zostaną zastąpione bez potwierdzenia.

Szczegółowe informacje o zawartości i struktury pliku JSON hello, można znaleźć w temacie toohello [Tworzenie danych wejściowych (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-input] sekcji hello [interfejs API REST zarządzania usługi analiza strumienia Odwołanie do biblioteki][stream.analytics.rest.api.reference].

**Przykład 1**

Program Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

Program Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

To polecenie programu PowerShell tworzy nowe dane wejściowe z hello pliku Input.json. Jeśli istniejące dane wejściowe o nazwie hello określony w pliku definicji wejściowych hello jest już zdefiniowana, polecenia cmdlet hello zapyta, czy tooreplace go.

**Przykład 2**

Program Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

Program Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

To polecenie programu PowerShell tworzy nowe dane wejściowe w zadaniu hello o nazwie EntryStream. Jeśli istniejące dane wejściowe o tej nazwie jest już zdefiniowana, polecenia cmdlet hello zapyta, czy tooreplace go.

**Przykład 3**

Program Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

Program Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

To polecenie programu PowerShell zastępuje definicji hello hello istniejącego źródła danych wejściowych o nazwie EntryStream z hello definicję z pliku hello.

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a>Nowe AzureStreamAnalyticsJob | Nowe AzureRMStreamAnalyticsJob
Tworzy nowe zadanie usługi analiza strumienia w Microsoft Azure lub aktualizacji definicji hello istniejących określonego zadania.

Witaj hello zadania można określić w pliku JSON hello lub hello w wierszu polecenia. Jeśli określono oba nazwa hello w wierszu polecenia hello musi hello w taki sam jak jedną hello w pliku hello.

Jeśli Określ nazwę zadania, która już istnieje i nie określaj hello — parametru Force, polecenia cmdlet hello zapyta, czy tooreplace hello istniejącego zadania.

Jeśli określisz hello — parametru Force, a następnie określ nazwę istniejącego zadania, hello definicji zadania zostaną zastąpione bez potwierdzenia.

Szczegółowe informacje o zawartości i struktury pliku JSON hello, można znaleźć w temacie toohello [utworzyć zadania usługi analiza strumienia] [ msdn-rest-api-create-stream-analytics-job] sekcji hello [dokumentacja interfejsu API REST zarządzania usługi analiza strumienia Biblioteka][stream.analytics.rest.api.reference].

**Przykład 1**

Program Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

Program Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

To polecenie programu PowerShell tworzy nowe zadanie z definicji hello w JobDefinition.json. Jeśli istniejące zadanie o nazwie hello określony w pliku definicji zadania hello jest już zdefiniowana, polecenia cmdlet hello zapyta, czy tooreplace go.

**Przykład 2**

Program Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

Program Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

To polecenie programu PowerShell zastępuje hello definicji zadania dla StreamingJob.

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a>Nowe AzureStreamAnalyticsOutput | Nowe AzureRMStreamAnalyticsOutput
Tworzy nowe dane wyjściowe w zadaniu Stream Analytics, lub aktualizuje istniejące dane wyjściowe.  

Witaj hello danych wyjściowych można określić w pliku JSON hello lub hello w wierszu polecenia. Jeśli określono oba nazwa hello w wierszu polecenia hello musi hello w taki sam jak jedną hello w pliku hello.

Jeśli Określ wyjścia, który już istnieje i nie określaj hello — parametru Force, polecenia cmdlet hello zapyta, czy tooreplace hello istniejących danych wyjściowych.

Jeśli określisz hello — parametru Force i określ istniejącą output nazwy, hello dane wyjściowe zostaną zastąpione bez potwierdzenia.

Szczegółowe informacje o zawartości i struktury pliku JSON hello, można znaleźć w temacie toohello [Tworzenie danych wyjściowych (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-output] sekcji hello [interfejs API REST zarządzania usługi analiza strumienia Odwołanie do biblioteki][stream.analytics.rest.api.reference].

**Przykład 1**

Program Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

Program Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

To polecenie programu PowerShell tworzy nowe dane wyjściowe w zadaniu hello StreamingJob o nazwie "wyjściowej". Jeśli istniejące dane wyjściowe o tej nazwie jest już zdefiniowana, polecenia cmdlet hello zapyta, czy tooreplace go.

**Przykład 2**

Program Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

Program Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

To polecenie programu PowerShell zastępuje hello definicji do "wyjściowej" w zadaniu hello StreamingJob.

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a>Nowe AzureStreamAnalyticsTransformation | Nowe AzureRMStreamAnalyticsTransformation
Tworzy nowy transformacji w zadaniu Stream Analytics lub aktualizuje hello istniejących transformacji.

Witaj transformacji hello można określić w pliku JSON hello lub hello w wierszu polecenia. Jeśli określono oba nazwa hello w wierszu polecenia hello musi hello w taki sam jak jedną hello w pliku hello.

Jeśli Określ transformację, która już istnieje i nie określaj hello — parametru Force, polecenia cmdlet hello zapyta, czy tooreplace hello istniejących transformacji.

Jeśli określisz hello — parametru Force i określ istniejącą nazwę przekształcania, przekształcania hello zostaną zastąpione bez potwierdzenia.

Szczegółowe informacje o zawartości i struktury pliku JSON hello, można znaleźć w temacie toohello [utworzyć transformacji (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-transformation] sekcji hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].

**Przykład 1**

Program Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

Program Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

To polecenie programu PowerShell tworzy nowy przekształcenia o nazwie StreamingJobTransform w zadaniu hello StreamingJob. Jeśli istniejące transformacji jest już zdefiniowany o tej nazwie, polecenia cmdlet hello zapyta, czy tooreplace go.

**Przykład 2**

Program Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

Program Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 To polecenie programu PowerShell zastępuje hello definicji StreamingJobTransform w zadaniu hello StreamingJob.

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a>Usuń AzureStreamAnalyticsInput | Usuń AzureRMStreamAnalyticsInput
Asynchronicznie usuwa określone dane wejściowe z zadania usługi analiza strumienia w Microsoft Azure.  
Jeśli określisz hello — parametru Force, hello danych wejściowych zostaną usunięte bez potwierdzenia.

**Przykład 1**

Program Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

Program Azure PowerShell 1.0:  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

Tego polecenia programu PowerShell, usuwa hello wejściowych EventStream w zadaniu hello StreamingJob.  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a>Usuń AzureStreamAnalyticsJob | Usuń AzureRMStreamAnalyticsJob
Asynchronicznie usuwa określonego zadania usługi analiza strumienia w Microsoft Azure.  
Jeśli określisz hello — parametru Force, hello zadania zostaną usunięte bez potwierdzenia.

**Przykład 1**

Program Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Program Azure PowerShell 1.0:  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

To polecenie programu PowerShell usuwa zadanie hello StreamingJob.  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a>Usuń AzureStreamAnalyticsOutput | Usuń AzureRMStreamAnalyticsOutput
Asynchronicznie usuwa określone dane wyjściowe z zadania usługi analiza strumienia w Microsoft Azure.  
Jeśli określisz hello — parametru Force, hello dane wyjściowe będą usunięte bez potwierdzenia.

**Przykład 1**

Program Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Program Azure PowerShell 1.0:  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Dane wyjściowe dane wyjściowe tego hello usuwa polecenia programu PowerShell w zadaniu hello StreamingJob.  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a>Start AzureStreamAnalyticsJob | Start AzureRMStreamAnalyticsJob
Asynchronicznie wdraża i uruchamia zadanie usługi analiza strumienia w Microsoft Azure.

**Przykład 1**

Program Azure PowerShell 0.9.8:  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

Program Azure PowerShell 1.0:  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

To polecenie programu PowerShell uruchamia hello zadania StreamingJob danych wyjściowych niestandardowego czas rozpoczęcia ustawić tooDecember 12, 2012, 12:12:12 UTC.

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a>Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob
Asynchronicznie Zatrzymuje zadanie usługi analiza strumienia, w programie Microsoft Azure i zwalnia zasoby, które były, które były używane. Witaj definicji zadania i metadanych pozostaną dostępne w ramach subskrypcji za pośrednictwem hello portalu Azure i zarządzanie interfejsów API, tak, aby hello zadania mogą edytować i ponownie uruchomić. Nie zostanie obciążona dla zadania w stanie hello zatrzymana.

**Przykład 1**

Program Azure PowerShell 0.9.8:  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Program Azure PowerShell 1.0:  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

To polecenie programu PowerShell Zatrzymuje zadanie hello StreamingJob.  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a>Test AzureStreamAnalyticsInput | AzureRMStreamAnalyticsInput testu
Zdolność hello testy tooa tooconnect Stream Analytics określone dane wejściowe.

**Przykład 1**

Program Azure PowerShell 0.9.8:  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

Program Azure PowerShell 1.0:  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

Tego programu PowerShell polecenie testy hello status połączenia hello wejściowych EntryStream w StreamingJob.  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a>Test AzureStreamAnalyticsOutput | AzureRMStreamAnalyticsOutput testu
Zdolność hello testy tooa tooconnect Stream Analytics określone dane wyjściowe.

**Przykład 1**

Program Azure PowerShell 0.9.8:  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Program Azure PowerShell 1.0:  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Dane wyjściowe w StreamingJob dane wyjściowe tego środowiska PowerShell polecenie testy hello status połączenia hello.  

## <a name="get-support"></a>Uzyskiwanie pomocy technicznej
Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics). 

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[msdn-switch-azuremode]: http://msdn.microsoft.com/library/dn722470.aspx
[powershell-install]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
[msdn-rest-api-create-stream-analytics-job]: https://msdn.microsoft.com/library/dn834994.aspx
[msdn-rest-api-create-stream-analytics-input]: https://msdn.microsoft.com/library/dn835010.aspx
[msdn-rest-api-create-stream-analytics-output]: https://msdn.microsoft.com/library/dn835015.aspx
[msdn-rest-api-create-stream-analytics-transformation]: https://msdn.microsoft.com/library/dn835007.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

