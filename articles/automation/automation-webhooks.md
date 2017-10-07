---
title: "Element runbook usługi Automatyzacja Azure z elementu webhook aaaStarting | Dokumentacja firmy Microsoft"
description: "Element webhook umożliwiający toostart klienta elementu runbook automatyzacji Azure z wywołania HTTP.  W tym artykule opisano sposób toocreate elementu webhook i w jaki sposób toocall toostart jednego elementu runbook."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9b20237c-a593-4299-bbdc-35c47ee9e55d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: ca6cde66b3784ceb5d0bc5921cee87aea74cb150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a>Uruchamianie elementu runbook usługi Automatyzacja Azure z elementu webhook
A *webhook* pozwala toostart określonego elementu runbook automatyzacji Azure za pomocą pojedynczego żądania HTTP. Pozwala to usług zewnętrznych, takich jak Visual Studio Team Services, GitHub, analizy dzienników Microsoft Operations Management Suite lub niestandardowych aplikacji toostart elementów runbook bez wdrażania przy użyciu interfejsu API usługi Automatyzacja Azure hello pełnego rozwiązania.  
![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)

Można porównać elementów webhook tooother metod uruchamiania elementu runbook [uruchamianie elementu runbook automatyzacji Azure](automation-starting-a-runbook.md)

## <a name="details-of-a-webhook"></a>Szczegóły elementu webhook
Witaj poniższej tabeli opisano właściwości hello, które należy skonfigurować dla elementu webhook.

| Właściwość | Opis |
|:--- |:--- |
| Nazwa |Możesz podać dowolną nazwę wybranego dla elementu webhook, ponieważ jest to nie jest uwidaczniana toohello klienta.  Jest używana tylko dla możesz tooidentify hello elementu runbook automatyzacji Azure. <br>  Najlepszym rozwiązaniem, należy nadać webhook powitania klienta toohello powiązane nazwy, który zostanie użyty. |
| ADRES URL |adres URL elementu webhook hello Hello jest unikatowy adres hello, że klient wywołuje z elementem runbook HTTP POST toostart hello połączone toohello elementu webhook.  Jest ona generowana automatycznie podczas tworzenia elementu webhook hello.  Nie można określić niestandardowy adres URL. <br> <br>  Witaj adres URL zawiera token zabezpieczający, który umożliwia hello toobe runbook wywoływany przez system innej firmy bez dalszego uwierzytelniania. Z tego powodu powinny być traktowane jak hasło.  Ze względów bezpieczeństwa możesz tylko hello widoku, adres URL w portalu Azure na powitania czasu hello webhook hello jest tworzona. Należy zauważyć, adres URL hello w bezpiecznej lokalizacji do użytku w przyszłości. |
| Data wygaśnięcia |Takie jak certyfikat każdy element webhook ma datę wygaśnięcia, które go można już używać.  Ta data wygaśnięcia można zmodyfikować po utworzeniu elementu webhook hello. |
| Enabled (Włączony) |Elementu webhook jest domyślnie włączona po jego utworzeniu.  Jeśli jest on ustawiany tooDisabled, a następnie nie klient nie będzie możliwe toouse go.  Można ustawić hello **włączone** podczas tworzenia elementu webhook hello lub w każdej chwili po jego utworzeniu. |

### <a name="parameters"></a>Parametry
Elementu webhook można zdefiniować wartości parametrów elementu runbook, które są używane przy uruchamianiu elementu runbook hello przez tego elementu webhook. Element webhook Hello muszą zawierać wartości parametrów obowiązkowych hello runbook i może zawierać wartości parametrów opcjonalnych. Po utworzeniu hello webhoook można zmodyfikować elementu webhook tooa skonfigurowana wartość parametru. Każdy z wielu elementów webhook połączone tooa jednego elementu runbook można użyć wartości innym parametrem.

Po uruchomieniu elementu runbook za pomocą elementu webhook klient go nie może zastąpić hello wartości parametrów zdefiniowane w hello elementu webhook.  dane tooreceive od powitania klienta, hello runbook może akceptować jeden parametr o nazwie **$WebhookData** typu [object], która będzie zawierać dane powitania klienta obejmuje hello wysłanie żądania POST.

![Właściwości Webhookdata](media/automation-webhooks/webhook-data-properties.png)

Witaj **$WebhookData** obiekt będzie miał hello następujące właściwości:

| Właściwość | Opis |
|:--- |:--- |
| WebhookName |Nazwa elementu webhook hello Hello. |
| RequestHeader |Tabela skrótów zawierająca nagłówki hello hello przychodzącego żądania POST. |
| requestBody |Treść Hello hello przychodzącego żądania POST.  To zachowują formatowania, takiego jak ciąg formatu JSON, XML, lub postać zakodowanych danych. Hello runbook musi być napisana toowork z hello format danych jest oczekiwany. |

Nie jest żadna konfiguracja hello toosupport wymaganego elementu webhook hello **$WebhookData** parametru i hello elementu runbook nie jest wymagane tooaccept go.  Jeśli element runbook hello nie definiuje parametru hello, żadnych szczegółów żądania hello wysłanych z klienta hello jest ignorowana.

Jeśli określisz wartości dla $WebhookData podczas tworzenia elementu webhook hello, że wartość będzie zastąpiona uruchomienia elementu webhook hello hello runbook hello danymi z żądania POST powitania klienta, nawet wtedy, gdy w treści żądania hello powitania klienta nie zawiera żadnych danych.  Po uruchomieniu elementu runbook, który ma $WebhookData przy użyciu innej metody niż elementu webhook można podać wartość dla $Webhookdata rozpoznane zostaną przez element runbook hello.  Ta wartość powinna być obiektu z hello tego samego [właściwości](#details-of-a-webhook) jako $Webhookdata tak hello elementu runbook właściwie pracę z nią tak, jakby jego pracy z rzeczywistego WebhookData przekazany przez elementu webhook.

Na przykład Jeśli rozpoczynasz hello następującego elementu runbook z hello portalu Azure i chcesz toopass niektóre przykładowe WebhookData do testowania, ponieważ obiekt jest WebhookData, jego powinien zostać przekazany jako JSON w hello interfejsu użytkownika.

![Parametr WebhookData z poziomu interfejsu użytkownika](media/automation-webhooks/WebhookData-parameter-from-UI.png)

Dla hello powyżej elementu runbook, jeśli masz następujące właściwości dla parametru WebhookData hello hello:

1. WebhookName: *MyWebhook*
2. RequestHeader: *z = użytkownika testowego*
3. RequestBody: *["VM1", "Maszyny VM2"]*

Następnie przejdzie hello następujące wartości JSON w hello interfejsu użytkownika dla parametru WebhookData hello:  

* {"WebhookName": "MyWebhook", "RequestHeader": {"Od": "Użytkownik testowy"}, "RequestBody": "[\"VM1\",\"maszyny VM2\"]"}

![Uruchom parametr WebhookData z interfejsu użytkownika](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> Witaj wartości wszystkich parametrów wejściowych są rejestrowane przy hello zadanie elementu runbook.  Oznacza to, że wszelkie danych wejściowych dostarczonych przez klienta hello w żądaniu webhook hello będą rejestrowane i dostępne tooanyone z zadanie usługi Automatyzacja toohello dostępu.  Z tego powodu należy zachować ostrożność w wywołaniach elementu webhook w tym poufne informacje.
>

## <a name="security"></a>Bezpieczeństwo
Hello bezpieczeństwa elementu webhook polega na prywatność hello adresu URL, który zawiera token zabezpieczający, który pozwala toobe wywoływane. Automatyzacja Azure nie wykonuje żadnego uwierzytelniania na powitania żądanie tak długo, jak staje się toohello poprawny adres URL. Z tego powodu nie można używać elementów webhook dla elementów runbook funkcji wysoce poufnymi bez używania alternatywnej metody sprawdzania poprawności żądania hello.

Można uwzględnić logiki w ramach hello toodetermine elementu runbook, czy została wywołana przez elementu webhook, sprawdzając hello **WebhookName** właściwość parametru hello $WebhookData. Witaj runbook można wykonać dalsze weryfikacji przez wyszukiwanie szczegółowych informacji w hello **RequestHeader** lub **RequestBody** właściwości.

Toohave jest kolejną strategią hello runbook weryfikowania niektórych warunku zewnętrznych podczas odebrała żądanie elementu webhook.  Rozważmy na przykład element runbook, który jest wywoływany przez GitHub, gdy istnieje nowe repozytorium GitHub tooa zatwierdzania.  Witaj runbook może się połączyć toovalidate tooGitHub, nowe zatwierdzenia rzeczywista właśnie miał wystąpił przed kontynuowaniem.

## <a name="creating-a-webhook"></a>Tworzenie elementu webhook
Użyj hello następujące procedury toocreate nowy element runbook tooa połączonego elementu webhook w hello portalu Azure.

1. Z hello **bloku elementów Runbook** w hello portalu Azure, kliknij przycisk runbook hello hello elementu webhook rozpocznie tooview bloku jej szczegółów.
2. Kliknij przycisk **Webhook** u góry hello hello bloku tooopen hello **Dodawanie elementu Webhook** bloku. <br>
   ![Przycisk elementów Webhook](media/automation-webhooks/webhooks-button.png)
3. Kliknij przycisk **tworzenia nowego elementu webhook** tooopen hello **bloku Utwórz elementu webhook**.
4. Określ **nazwa**, **Data wygaśnięcia** dla elementu webhook hello i określa, czy powinno być włączone. Zobacz [szczegóły elementu webhook](#details-of-a-webhook) Aby uzyskać więcej informacji tych właściwości.
5. Kliknij ikonę kopiowania hello i naciśnij klawisze Ctrl + C toocopy hello adres URL elementu webhook hello.  Następnie zapisz go w bezpiecznym miejscu.  **Po utworzeniu elementu webhook hello hello adresu URL nie można pobrać ponownie.** <br>
   ![Adres URL elementu Webhook](media/automation-webhooks/copy-webhook-url.png)
6. Kliknij przycisk **parametry** tooprovide wartości parametrów elementu runbook hello.  Jeśli hello runbook ma parametry obowiązkowe, następnie nie będzie możliwe toocreate hello webhook ile wartości.
7. Kliknij przycisk **Utwórz** toocreate hello webhook.

## <a name="using-a-webhook"></a>Przy użyciu elementu webhook
toouse elementu webhook po jego utworzeniu aplikacji klienta należy wygenerować HTTP POST z adresem URL hello hello elementu webhook.  Składnia elementu webhook hello Hello będą hello zgodny z formatem.

    http://<Webhook Server>/token?=<Token Value>

powitania klienta zostanie wyświetlony jeden z poniższych kody powrotu z żądania POST hello hello.  

| Kod | Tekst | Opis |
|:--- |:--- |:--- |
| 202 |Zaakceptowane |Witaj żądanie zostało zaakceptowane, a hello runbook pomyślnie zostało umieszczone w kolejce. |
| 400 |Nieprawidłowe żądanie |Nie zaakceptowano żądanie Hello jednego hello z następujących powodów. <ul> <li>Witaj webhook wygasł.</li> <li>Element webhook Hello jest wyłączona.</li> <li>token Hello w adresie URL hello jest nieprawidłowy.</li>  </ul> |
| 404 |Nie można odnaleźć |Nie zaakceptowano żądanie Hello jednego hello z następujących powodów. <ul> <li>Nie można odnaleźć elementu webhook Hello.</li> <li>Nie znaleziono elementu runbook Hello.</li> <li>Nie znaleziono konta Hello.</li>  </ul> |
| 500 |Wewnętrzny błąd serwera |adres URL Hello jest prawidłowy, ale wystąpił błąd.  Prześlij żądanie hello. |

Przy założeniu, że Żądanie hello zakończy się pomyślnie, odpowiedź hello elementu webhook zawiera hello identyfikator zadania w formacie JSON w następujący sposób. Będzie zawierać identyfikator pojedyncze zadanie, ale umożliwia formatu JSON hello potencjalne przyszłe ulepszenia.

    {"JobIds":["<JobId>"]}  

Po zakończeniu wykonywania hello zadanie elementu runbook lub jego stanie ukończenia z elementu webhook hello, nie można ustalić powitania klienta.  Można określić te informacje przy użyciu identyfikatora zadania hello z innej metody takie jak [programu Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) lub hello [interfejsu API usługi Automatyzacja Azure](https://msdn.microsoft.com/library/azure/mt163826.aspx).

### <a name="example"></a>Przykład
Poniższy przykład Hello używa środowiska Windows PowerShell toostart elementu runbook z elementu webhook.  Można użyć dowolnego języka, który może zgłaszać żądania HTTP elementu webhook; Środowisko Windows PowerShell jest używany po prostu poniższym przykładzie.

Hello runbook oczekuje listę zapisany w formacie JSON w treści żądania hello hello maszyn wirtualnych. Możemy również są wraz z informacjami dotyczącymi który uruchamia hello runbook oraz hello Data i godzina się, że jest uruchamiana w nagłówku hello hello żądania.      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


Witaj poniższy obraz przedstawia informacje o nagłówku hello (przy użyciu [Fiddler](http://www.telerik.com/fiddler) śledzenia) z tego żądania. Obejmuje standardowych nagłówków żądania HTTP w toohello dodanie niestandardowa data i z nagłówków, które dodano.  Każdy z tych wartości jest runbook toohello dostępne w hello **RequestHeaders** właściwość **WebhookData**.

![Przycisk elementów Webhook](media/automation-webhooks/webhook-request-headers.png)

Witaj poniższy obraz przedstawia hello treści żądania hello (przy użyciu [Fiddler](http://www.telerik.com/fiddler) śledzenia) czyli dostępne toohello runbook w programie hello **RequestBody** właściwość **WebhookData**. To jest w formacie JSON powodu hello formatu, który został uwzględniony w treści hello hello żądania.     

![Przycisk elementów Webhook](media/automation-webhooks/webhook-request-body.png)

Witaj poniższy obraz przedstawia hello żądania wysyłane z programu Windows PowerShell i hello wynikowy odpowiedzi.  Identyfikator zadania Hello jest wyodrębniana z hello odpowiedzi i tooa skonwertowany ciąg.

![Przycisk elementów Webhook](media/automation-webhooks/webhook-request-response.png)

Witaj następujący przykładowy element runbook akceptuje hello poprzednie przykładowe żądanie i uruchamia określony w treści żądania hello maszyn wirtualnych hello.

    workflow Test-StartVirtualMachinesFromWebhook
    {
        param (
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {

            # Collect properties of WebhookData
            $WebhookName     =     $WebhookData.WebhookName
            $WebhookHeaders =     $WebhookData.RequestHeader
            $WebhookBody     =     $WebhookData.RequestBody

            # Collect individual headers. VMList converted from JSON.
            $From = $WebhookHeaders.From
            $VMList = ConvertFrom-Json -InputObject $WebhookBody
            Write-Output "Runbook started from webhook $WebhookName by $From."

            # Authenticate tooAzure resources
            $Cred = Get-AutomationPSCredential -Name 'MyAzureCredential'
            Add-AzureAccount -Credential $Cred

            # Start each virtual machine
            foreach ($VM in $VMList)
            {
                $VMName = $VM.Name
                Write-Output "Starting $VMName"
                Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName
            }
        }
        else {
            Write-Error "Runbook mean toobe started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-tooazure-alerts"></a>Uruchamianie elementów runbook w odpowiedzi tooAzure alertów
Włączone elementu Webhook elementów runbook mogą być używane tooreact zbyt[Azure alerty](../monitoring-and-diagnostics/insights-receive-alert-notifications.md). Zasobami na platformie Azure mogą być monitorowane przez zbieranie statystyk hello, takich jak wydajności, dostępności i użyciu za pomocą hello Azure alertów. Otrzymasz alert w oparciu metryki monitorowania lub zdarzenia dla zasobów platformy Azure, obecnie kont automatyzacji obsługuje tylko metryki. Gdy wartość hello określonej metryki przekracza próg hello przypisane lub jeśli hello skonfigurowane zdarzenie zostanie wyzwolone powiadomienie jest wysyłane toohello usługi administratora lub współadministratorzy tooresolve hello alertu, aby uzyskać więcej informacji na temat metryki i zdarzenia można znaleźć zbyt[ Alerty Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

Oprócz za pomocą usługi Azure alerty jako system powiadomień, należy również rozpocząć się poza elementów runbook w tooalerts odpowiedzi. Automatyzacja Azure udostępnia hello możliwości toorun włączone elementu webhook elementów runbook z alertami platformy Azure. Gdy przekracza metrykę hello skonfigurowany wartość progowa reguły alertu hello staje się aktywny i wyzwalaczy hello webhook usługi Automatyzacja, który z kolei wykonuje hello elementu runbook.

![elementów webhook](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a>Kontekst alertu
Należy rozważyć zasobów platformy Azure, takich jak maszyny wirtualnej, użycie procesora CPU tego komputera jest jednym z hello metryki wydajności. Jeśli hello wykorzystanie procesora CPU jest 100% lub po upływie pewnego przez długi czas, możesz toorestart hello maszyny wirtualnej toofix hello problem. To będzie możliwe przez skonfigurowanie maszyny wirtualnej toohello reguły alertów i procent użycia procesora CPU, jako jego metryka ma ta reguła. Procent użycia procesora CPU w tym miejscu jest po prostu wykonywanej na przykład, ale istnieje wiele innych metryk, że możesz skonfigurować tooyour Azure zasobów i ponowne uruchamianie maszyny wirtualnej hello jest akcja, która jest poświęcony toofix ten problem, hello tootake elementu runbook można skonfigurować inne akcje.

Tę regułę alertów hello staje się aktywny i wyzwalaczy hello włączone elementu webhook elementu runbook, wysyła hello kontekst alertu toohello runbook. [Kontekst alertu](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) zawiera szczegółowe informacje, łącznie z **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** i **sygnatury czasowej** jest wymagane dla hello runbook tooidentify hello zasobu na którym on być podejmowania działań. Alert kontekstu jest osadzony w części treści hello hello **WebhookData** obiektu wysłane toohello runbook i jest dostępny z **Webhook.RequestBody** właściwości

### <a name="example"></a>Przykład
Utwórz maszynę wirtualną platformy Azure w subskrypcji i powiąż [alertów Metryka procent toomonitor Procesora](../monitoring-and-diagnostics/insights-receive-alert-notifications.md). Podczas tworzenia alertu hello upewnij się, że wypełnić pole elementu webhook hello z adresem URL elementu webhook hello, który został wygenerowany podczas tworzenia elementu webhook hello hello.

Witaj następujący przykładowy element runbook jest wyzwalane, gdy reguły alertu hello staje się aktywny i zbiera hello parametrów kontekstu alertu, które są wymagane, na którym będzie biorąc pod akcji hello runbook tooidentify hello zasobu.

    workflow Invoke-RunbookUsingAlerts
    {
        param (      
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {   
            # Collect properties of WebhookData.
            $WebhookName    =   $WebhookData.WebhookName
            $WebhookBody    =   $WebhookData.RequestBody
            $WebhookHeaders =   $WebhookData.RequestHeader

            # Outputs information on hello webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain hello WebhookBody containing hello AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain hello AlertContext     
            $AlertContext = [object]$WebhookBody.context

            # Some selected AlertContext information
            Write-Output "`nALERT CONTEXT DATA"
            Write-Output "==================="
            Write-Output $AlertContext.name
            Write-Output $AlertContext.subscriptionId
            Write-Output $AlertContext.resourceGroupName
            Write-Output $AlertContext.resourceName
            Write-Output $AlertContext.resourceType
            Write-Output $AlertContext.resourceId
            Write-Output $AlertContext.timestamp

            # Act on hello AlertContext data, in our case restarting hello VM.
            # Authenticate tooyour Azure subscription using Organization ID toobe able toorestart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check hello status property of hello VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart hello VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant tooonly be started from a webhook."  
        }  
    }



## <a name="next-steps"></a>Następne kroki
* Aby uzyskać więcej informacji na różne sposoby toostart elementu runbook, zobacz [uruchamianie elementu Runbook](automation-starting-a-runbook.md).
* Informacje dotyczące hello wyświetlanie stanu zadania elementu Runbook, można znaleźć zbyt[wykonanie elementu Runbook automatyzacji Azure](automation-runbook-execution.md).
* toolearn toouse akcji tootake usługi Automatyzacja Azure alerty Azure, zobacz temat [skorygować alerty maszyny Wirtualnej Azure z elementu Runbook usługi automatyzacja](automation-azure-vm-alert-integration.md).
