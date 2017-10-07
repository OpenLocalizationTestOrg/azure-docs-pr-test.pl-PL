---
title: "aaaMonitor bramy sieci VPN z rozwiązywaniem problemów obserwatora sieciowego Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób diagnozowania lokalnymi łączności z usługi Automatyzacja Azure i obserwatora sieciowego"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a607d0c862ea1be63c687717f0c5dc137db58a43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a>Monitorowanie bramy sieci VPN z rozwiązywaniem problemów obserwatora sieciowego

Uzyskania szczegółowych informacji na wydajność sieci jest krytyczne tooprovide toocustomers niezawodne usługi. W związku z tym krytycznych toodetect warunki awarii sieci szybko i jest podjąć działania naprawcze toomitigate hello awarii warunku. Automatyzacja Azure pozwala tooimplement i uruchom zadanie w sposób programowy za pomocą elementów runbook. Przy użyciu automatyzacji Azure tworzy doskonałe przepisu sieci ciągły i aktywnego monitorowania i alertów.

## <a name="scenario"></a>Scenariusz

Scenariusz Hello powitania po obrazu jest aplikacją wielowarstwowych z na połączenie lokalne za pomocą bramy sieci VPN i tunelowania. Zapewnienie powitalne bramy sieci VPN jest uruchomiony i uruchomiona jest krytyczne toohello wydajność aplikacji.

Element runbook jest tworzony z toocheck skryptu, dla stanu połączenia tunelu VPN hello, za pomocą hello toocheck API Rozwiązywanie problemów z zasobów dla stanu połączenia tunelu. Jeśli stan hello nie jest w dobrej kondycji, wyzwalacz poczty e-mail jest wysyłane tooadministrators.

![Przykładowy scenariusz][scenario]

W tym scenariuszu obejmują:

- Utwórz hello wywołania elementu runbook `Start-AzureRmNetworkWatcherResourceTroubleshooting` stan połączenia tootroubleshoot polecenia cmdlet
- Łączenie elementu runbook toohello harmonogramu

## <a name="before-you-begin"></a>Przed rozpoczęciem

Przed rozpoczęciem tego scenariusza, musi mieć hello następujące wymagania wstępne:

- Konto usługi Automatyzacja Azure w systemie Azure. Sprawdź, czy konto automatyzacji hello ma modułów najnowszego hello i ma również hello AzureRM.Network modułu. Witaj AzureRM.Network moduł jest dostępny w galerii modułu hello Jeśli potrzebujesz tooadd on tooyour konta automatyzacji.
- Musi mieć zestaw poświadczeń, skonfiguruj w automatyzacji Azure. Dowiedz się więcej o [zabezpieczeń usługi Automatyzacja Azure](../automation/automation-security-overview.md)
- Prawidłowy adres serwera SMTP (Office 365, poczty e-mail lokalnego lub innej) i poświadczeń określonych w automatyzacji Azure
- Skonfigurowana brama sieci wirtualnej na platformie Azure.
- Loguje istniejącego konta magazynu z istniejących hello toostore kontenera.

> [!NOTE]
> Infrastruktura Hello pokazana na powitania poprzedzających obrazu jest w celach ilustracyjnych i nie są tworzone z hello kroki zawarte w tym artykule.

### <a name="create-hello-runbook"></a>Tworzenie elementu runbook hello

przykład Witaj tooconfiguring pierwszy krok Hello jest toocreate hello runbook. W tym przykładzie użyto konta Uruchom jako. toolearn informacji o kontach Uruchom jako, odwiedź stronę [uwierzytelniania elementy Runbook za pomocą konta Uruchom jako platformy Azure](../automation/automation-sec-configure-azure-runas-account.md)

### <a name="step-1"></a>Krok 1

Przejdź tooAzure automatyzacji w hello [portalu Azure](https://portal.azure.com) i kliknij przycisk **elementów Runbook**

![Przegląd konta automatyzacji][1]

### <a name="step-2"></a>Krok 2

Kliknij przycisk **Dodaj element runbook** procesu tworzenia hello toostart hello elementu runbook.

![elementy runbook bloku][2]

### <a name="step-3"></a>Krok 3

W obszarze **szybkie tworzenie**, kliknij przycisk **Utwórz nowy element runbook** toocreate hello runbook.

![Dodawanie bloku elementu runbook][3]

### <a name="step-4"></a>Krok 4

W tym kroku będziemy nadaj hello runbook nazwę, w przykładzie hello jest nazywany **Get-VPNGatewayStatus**. Jest to opisowa nazwa elementu runbook hello toogive ważne i zalecane nadanie mu nazwę zgodną z standard standardy nazewnictwa programu PowerShell. Typ elementu runbook Hello w tym przykładzie jest **PowerShell**, hello inne opcje są graficzny, przepływ pracy programu PowerShell i przepływ pracy programu PowerShell graficznego.

![bloku elementu runbook][4]

### <a name="step-5"></a>Krok 5

W tym kroku hello element runbook został utworzony, wszystkie hello kod potrzebny na przykład hello zapewnia hello poniższy przykład kodu. Witaj w kodzie hello elementów, które zawierają \<wartość\> muszą toobe zastąpione wartościami hello z subskrypcji.

Użyj hello poniższy kod jako kliknij **Zapisz**

```PowerShell
# Set these variables toohello proper values for your environment
$o365AutomationCredential = "<Office 365 account>"
$fromEmail = "<from email address>"
$toEmail = "<tooemail address>"
$smtpServer = "<smtp.office365.com>"
$smtpPort = 587
$runAsConnectionName = "<AzureRunAsConnection>"
$subscriptionId = "<subscription id>"
$region = "<Azure region>"
$vpnConnectionName = "<vpn connection name>"
$vpnConnectionResourceGroup = "<resource group name>"
$storageAccountName = "<storage account name>"
$storageAccountResourceGroup = "<resource group name>"
$storageAccountContainer = "<container name>"

# Get credentials for Office 365 account
$cred = Get-AutomationPSCredential -Name $o365AutomationCredential

# Get hello connection "AzureRunAsConnection "
$servicePrincipalConnection=Get-AutomationConnection -Name $runAsConnectionName

"Logging in tooAzure..."
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $servicePrincipalConnection.TenantId `
    -ApplicationId $servicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
"Setting context tooa specific subscription"
Set-AzureRmContext -SubscriptionId $subscriptionId

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $region }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name $vpnConnectionName -ResourceGroupName $vpnConnectionResourceGroup
$sa = Get-AzureRmStorageAccount -Name $storageAccountName -ResourceGroupName $storageAccountResourceGroup 
$storagePath = "$($sa.PrimaryEndpoints.Blob)$($storageAccountContainer)"
$result = Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath $storagePath

if($result.code -ne "Healthy")
    {
        $body = "Connection for $($connection.name) is: $($result.code) `n$($result.results[0].summary) `nView hello logs at $($storagePath) toolearn more."
        Write-Output $body
        $subject = "$($connection.name) Status"
        Send-MailMessage `
        -too$toEmail `
        -Subject $subject `
        -Body $body `
        -UseSsl `
        -Port $smtpPort `
        -SmtpServer $smtpServer `
        -From $fromEmail `
        -BodyAsHtml `
        -Credential $cred
    }
else
    {
    Write-Output ("Connection Status is: $($result.code)")
    }
```

### <a name="step-6"></a>Krok 6

Po zapisaniu hello runbook harmonogramu musi być połączone tooit tooautomate hello początku hello elementu runbook. proces hello toostart, kliknij przycisk **harmonogram**.

![Krok 6][6]

## <a name="link-a-schedule-toohello-runbook"></a>Łączenie elementu runbook toohello harmonogramu

Należy utworzyć nowy harmonogram. Kliknij przycisk **powiązania elementu runbook tooyour harmonogram**.

![Krok 7][7]

### <a name="step-1"></a>Krok 1

Na powitania **harmonogram** bloku, kliknij przycisk **Utwórz nowy harmonogram**

![Krok 8][8]

### <a name="step-2"></a>Krok 2

Na powitania **nowy harmonogram** bloku wypełniania hello informacje o harmonogramie. Witaj wartości, które można ustawić znajdują się w hello następującej listy:

- **Nazwa** -hello przyjazną nazwę hello harmonogramu.
- **Opis elementu** — opis hello harmonogramu.
- **Uruchamia** — ta wartość jest kombinacją datę, godzinę i strefę czasową, wchodzące w skład hello czasu hello harmonogram wyzwalaczy.
- **Cykl** — ta wartość określa hello harmonogramy powtarzania.  Prawidłowe wartości to **raz** lub **cykliczny**.
- **Powtarzanie co** -hello interwał cyklu harmonogramu hello w godziny, dni, tygodnie lub miesiące.
- **Ustawienia okresu ważności** -hello wartość określa, czy harmonogram hello wygaśnięcia lub nie. Można ustawić także**tak** lub **nr**. Nieprawidłowa data i godzina są toobe podany, jeśli tak jest wybierany.

> [!NOTE]
> Jeśli potrzebujesz toohave częściej niż co godzinę uruchomienia elementu runbook, wiele harmonogramów musi być utworzone na różnych interwałów (to znaczy, 15, 30, 45 minut po godzinie hello)

![Krok 9][9]

### <a name="step-3"></a>Krok 3

Kliknij przycisk Zapisz toosave hello harmonogram toohello runbook.

![Krok 10][10]

## <a name="next-steps"></a>Następne kroki

Teraz, gdy wiedzę na temat toointegrate obserwatora sieciowego rozwiązywania problemów w usłudze Automatyzacja Azure, Dowiedz się, jak przechwytywanie pakietów tootrigger alerty maszyny Wirtualnej, odwiedzając [utworzyć przechwytywania alertów wyzwalanych pakietów z obserwatora sieciowego Azure](network-watcher-alert-triggered-packet-capture.md).

<!-- images -->
[scenario]: ./media/network-watcher-monitor-with-azure-automation/scenario.png
[1]: ./media/network-watcher-monitor-with-azure-automation/figure1.png
[2]: ./media/network-watcher-monitor-with-azure-automation/figure2.png
[3]: ./media/network-watcher-monitor-with-azure-automation/figure3.png
[4]: ./media/network-watcher-monitor-with-azure-automation/figure4.png
[5]: ./media/network-watcher-monitor-with-azure-automation/figure5.png
[6]: ./media/network-watcher-monitor-with-azure-automation/figure6.png
[7]: ./media/network-watcher-monitor-with-azure-automation/figure7.png
[8]: ./media/network-watcher-monitor-with-azure-automation/figure8.png
[9]: ./media/network-watcher-monitor-with-azure-automation/figure9.png
[10]: ./media/network-watcher-monitor-with-azure-automation/figure10.png
