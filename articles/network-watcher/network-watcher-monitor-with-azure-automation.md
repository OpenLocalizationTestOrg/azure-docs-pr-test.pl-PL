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
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a><span data-ttu-id="adb7c-103">Monitorowanie bramy sieci VPN z rozwiązywaniem problemów obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="adb7c-103">Monitor VPN gateways with Network Watcher troubleshooting</span></span>

<span data-ttu-id="adb7c-104">Uzyskania szczegółowych informacji na wydajność sieci jest krytyczne tooprovide toocustomers niezawodne usługi.</span><span class="sxs-lookup"><span data-stu-id="adb7c-104">Gaining deep insights on your network performance is critical tooprovide reliable services toocustomers.</span></span> <span data-ttu-id="adb7c-105">W związku z tym krytycznych toodetect warunki awarii sieci szybko i jest podjąć działania naprawcze toomitigate hello awarii warunku.</span><span class="sxs-lookup"><span data-stu-id="adb7c-105">It is therefore critical toodetect network outage conditions quickly and take corrective action toomitigate hello outage condition.</span></span> <span data-ttu-id="adb7c-106">Automatyzacja Azure pozwala tooimplement i uruchom zadanie w sposób programowy za pomocą elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="adb7c-106">Azure Automation enables you tooimplement and run a task in a programmatic fashion through runbooks.</span></span> <span data-ttu-id="adb7c-107">Przy użyciu automatyzacji Azure tworzy doskonałe przepisu sieci ciągły i aktywnego monitorowania i alertów.</span><span class="sxs-lookup"><span data-stu-id="adb7c-107">Using Azure Automation creates a perfect recipe for performing continuous and proactive network monitoring and alerting.</span></span>

## <a name="scenario"></a><span data-ttu-id="adb7c-108">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="adb7c-108">Scenario</span></span>

<span data-ttu-id="adb7c-109">Scenariusz Hello powitania po obrazu jest aplikacją wielowarstwowych z na połączenie lokalne za pomocą bramy sieci VPN i tunelowania.</span><span class="sxs-lookup"><span data-stu-id="adb7c-109">hello scenario in hello following image is a multi-tiered application, with on premises connectivity established using a VPN Gateway and tunnel.</span></span> <span data-ttu-id="adb7c-110">Zapewnienie powitalne bramy sieci VPN jest uruchomiony i uruchomiona jest krytyczne toohello wydajność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="adb7c-110">Ensuring hello VPN Gateway is up and running is critical toohello applications performance.</span></span>

<span data-ttu-id="adb7c-111">Element runbook jest tworzony z toocheck skryptu, dla stanu połączenia tunelu VPN hello, za pomocą hello toocheck API Rozwiązywanie problemów z zasobów dla stanu połączenia tunelu.</span><span class="sxs-lookup"><span data-stu-id="adb7c-111">A runbook is created with a script toocheck for connection status of hello VPN tunnel, using hello Resource Troubleshooting API toocheck for connection tunnel status.</span></span> <span data-ttu-id="adb7c-112">Jeśli stan hello nie jest w dobrej kondycji, wyzwalacz poczty e-mail jest wysyłane tooadministrators.</span><span class="sxs-lookup"><span data-stu-id="adb7c-112">If hello status is not healthy, an email trigger is sent tooadministrators.</span></span>

![Przykładowy scenariusz][scenario]

<span data-ttu-id="adb7c-114">W tym scenariuszu obejmują:</span><span class="sxs-lookup"><span data-stu-id="adb7c-114">This scenario will:</span></span>

- <span data-ttu-id="adb7c-115">Utwórz hello wywołania elementu runbook `Start-AzureRmNetworkWatcherResourceTroubleshooting` stan połączenia tootroubleshoot polecenia cmdlet</span><span class="sxs-lookup"><span data-stu-id="adb7c-115">Create a runbook calling hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet tootroubleshoot connection status</span></span>
- <span data-ttu-id="adb7c-116">Łączenie elementu runbook toohello harmonogramu</span><span class="sxs-lookup"><span data-stu-id="adb7c-116">Link a schedule toohello runbook</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="adb7c-117">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="adb7c-117">Before you begin</span></span>

<span data-ttu-id="adb7c-118">Przed rozpoczęciem tego scenariusza, musi mieć hello następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="adb7c-118">Before you start this scenario, you must have hello following pre-requisites:</span></span>

- <span data-ttu-id="adb7c-119">Konto usługi Automatyzacja Azure w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="adb7c-119">An Azure automation account in Azure.</span></span> <span data-ttu-id="adb7c-120">Sprawdź, czy konto automatyzacji hello ma modułów najnowszego hello i ma również hello AzureRM.Network modułu.</span><span class="sxs-lookup"><span data-stu-id="adb7c-120">Ensure that hello automation account has hello latest modules and also has hello AzureRM.Network module.</span></span> <span data-ttu-id="adb7c-121">Witaj AzureRM.Network moduł jest dostępny w galerii modułu hello Jeśli potrzebujesz tooadd on tooyour konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="adb7c-121">hello AzureRM.Network module is available in hello module gallery if you need tooadd it tooyour automation account.</span></span>
- <span data-ttu-id="adb7c-122">Musi mieć zestaw poświadczeń, skonfiguruj w automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="adb7c-122">You must have a set of credentials configure in Azure Automation.</span></span> <span data-ttu-id="adb7c-123">Dowiedz się więcej o [zabezpieczeń usługi Automatyzacja Azure](../automation/automation-security-overview.md)</span><span class="sxs-lookup"><span data-stu-id="adb7c-123">Learn more at [Azure Automation security](../automation/automation-security-overview.md)</span></span>
- <span data-ttu-id="adb7c-124">Prawidłowy adres serwera SMTP (Office 365, poczty e-mail lokalnego lub innej) i poświadczeń określonych w automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="adb7c-124">A valid SMTP server (Office 365, your on-premises email or another) and credentials defined in Azure Automation</span></span>
- <span data-ttu-id="adb7c-125">Skonfigurowana brama sieci wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="adb7c-125">A configured Virtual Network Gateway in Azure.</span></span>
- <span data-ttu-id="adb7c-126">Loguje istniejącego konta magazynu z istniejących hello toostore kontenera.</span><span class="sxs-lookup"><span data-stu-id="adb7c-126">An existing storage account with an existing container toostore hello logs in.</span></span>

> [!NOTE]
> <span data-ttu-id="adb7c-127">Infrastruktura Hello pokazana na powitania poprzedzających obrazu jest w celach ilustracyjnych i nie są tworzone z hello kroki zawarte w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="adb7c-127">hello infrastructure depicted in hello preceding image is for illustration purposes and are not created with hello steps contained in this article.</span></span>

### <a name="create-hello-runbook"></a><span data-ttu-id="adb7c-128">Tworzenie elementu runbook hello</span><span class="sxs-lookup"><span data-stu-id="adb7c-128">Create hello runbook</span></span>

<span data-ttu-id="adb7c-129">przykład Witaj tooconfiguring pierwszy krok Hello jest toocreate hello runbook.</span><span class="sxs-lookup"><span data-stu-id="adb7c-129">hello first step tooconfiguring hello example is toocreate hello runbook.</span></span> <span data-ttu-id="adb7c-130">W tym przykładzie użyto konta Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="adb7c-130">This example uses a run-as account.</span></span> <span data-ttu-id="adb7c-131">toolearn informacji o kontach Uruchom jako, odwiedź stronę [uwierzytelniania elementy Runbook za pomocą konta Uruchom jako platformy Azure](../automation/automation-sec-configure-azure-runas-account.md)</span><span class="sxs-lookup"><span data-stu-id="adb7c-131">toolearn about run-as accounts, visit [Authenticate Runbooks with Azure Run As account](../automation/automation-sec-configure-azure-runas-account.md)</span></span>

### <a name="step-1"></a><span data-ttu-id="adb7c-132">Krok 1</span><span class="sxs-lookup"><span data-stu-id="adb7c-132">Step 1</span></span>

<span data-ttu-id="adb7c-133">Przejdź tooAzure automatyzacji w hello [portalu Azure](https://portal.azure.com) i kliknij przycisk **elementów Runbook**</span><span class="sxs-lookup"><span data-stu-id="adb7c-133">Navigate tooAzure Automation in hello [Azure portal](https://portal.azure.com) and click **Runbooks**</span></span>

![Przegląd konta automatyzacji][1]

### <a name="step-2"></a><span data-ttu-id="adb7c-135">Krok 2</span><span class="sxs-lookup"><span data-stu-id="adb7c-135">Step 2</span></span>

<span data-ttu-id="adb7c-136">Kliknij przycisk **Dodaj element runbook** procesu tworzenia hello toostart hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="adb7c-136">Click **Add a runbook** toostart hello creation process of hello runbook.</span></span>

![elementy runbook bloku][2]

### <a name="step-3"></a><span data-ttu-id="adb7c-138">Krok 3</span><span class="sxs-lookup"><span data-stu-id="adb7c-138">Step 3</span></span>

<span data-ttu-id="adb7c-139">W obszarze **szybkie tworzenie**, kliknij przycisk **Utwórz nowy element runbook** toocreate hello runbook.</span><span class="sxs-lookup"><span data-stu-id="adb7c-139">Under **Quick Create**, click **Create a new runbook** toocreate hello runbook.</span></span>

![Dodawanie bloku elementu runbook][3]

### <a name="step-4"></a><span data-ttu-id="adb7c-141">Krok 4</span><span class="sxs-lookup"><span data-stu-id="adb7c-141">Step 4</span></span>

<span data-ttu-id="adb7c-142">W tym kroku będziemy nadaj hello runbook nazwę, w przykładzie hello jest nazywany **Get-VPNGatewayStatus**.</span><span class="sxs-lookup"><span data-stu-id="adb7c-142">In this step, we give hello runbook a name, in hello example it is called **Get-VPNGatewayStatus**.</span></span> <span data-ttu-id="adb7c-143">Jest to opisowa nazwa elementu runbook hello toogive ważne i zalecane nadanie mu nazwę zgodną z standard standardy nazewnictwa programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="adb7c-143">It is important toogive hello runbook a descriptive name, and recommended giving it a name that follows standard PowerShell naming standards.</span></span> <span data-ttu-id="adb7c-144">Typ elementu runbook Hello w tym przykładzie jest **PowerShell**, hello inne opcje są graficzny, przepływ pracy programu PowerShell i przepływ pracy programu PowerShell graficznego.</span><span class="sxs-lookup"><span data-stu-id="adb7c-144">hello runbook type for this example is **PowerShell**, hello other options are Graphical, PowerShell workflow, and Graphical PowerShell workflow.</span></span>

![bloku elementu runbook][4]

### <a name="step-5"></a><span data-ttu-id="adb7c-146">Krok 5</span><span class="sxs-lookup"><span data-stu-id="adb7c-146">Step 5</span></span>

<span data-ttu-id="adb7c-147">W tym kroku hello element runbook został utworzony, wszystkie hello kod potrzebny na przykład hello zapewnia hello poniższy przykład kodu.</span><span class="sxs-lookup"><span data-stu-id="adb7c-147">In this step hello runbook is created, hello following code example provides all hello code needed for hello example.</span></span> <span data-ttu-id="adb7c-148">Witaj w kodzie hello elementów, które zawierają \<wartość\> muszą toobe zastąpione wartościami hello z subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="adb7c-148">hello items in hello code that contain \<value\> need toobe replaced with hello values from your subscription.</span></span>

<span data-ttu-id="adb7c-149">Użyj hello poniższy kod jako kliknij **Zapisz**</span><span class="sxs-lookup"><span data-stu-id="adb7c-149">Use hello following code as click **Save**</span></span>

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

### <a name="step-6"></a><span data-ttu-id="adb7c-150">Krok 6</span><span class="sxs-lookup"><span data-stu-id="adb7c-150">Step 6</span></span>

<span data-ttu-id="adb7c-151">Po zapisaniu hello runbook harmonogramu musi być połączone tooit tooautomate hello początku hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="adb7c-151">Once hello runbook is saved, a schedule must be linked tooit tooautomate hello start of hello runbook.</span></span> <span data-ttu-id="adb7c-152">proces hello toostart, kliknij przycisk **harmonogram**.</span><span class="sxs-lookup"><span data-stu-id="adb7c-152">toostart hello process, click **Schedule**.</span></span>

![Krok 6][6]

## <a name="link-a-schedule-toohello-runbook"></a><span data-ttu-id="adb7c-154">Łączenie elementu runbook toohello harmonogramu</span><span class="sxs-lookup"><span data-stu-id="adb7c-154">Link a schedule toohello runbook</span></span>

<span data-ttu-id="adb7c-155">Należy utworzyć nowy harmonogram.</span><span class="sxs-lookup"><span data-stu-id="adb7c-155">A new schedule must be created.</span></span> <span data-ttu-id="adb7c-156">Kliknij przycisk **powiązania elementu runbook tooyour harmonogram**.</span><span class="sxs-lookup"><span data-stu-id="adb7c-156">Click **Link a schedule tooyour runbook**.</span></span>

![Krok 7][7]

### <a name="step-1"></a><span data-ttu-id="adb7c-158">Krok 1</span><span class="sxs-lookup"><span data-stu-id="adb7c-158">Step 1</span></span>

<span data-ttu-id="adb7c-159">Na powitania **harmonogram** bloku, kliknij przycisk **Utwórz nowy harmonogram**</span><span class="sxs-lookup"><span data-stu-id="adb7c-159">On hello **Schedule** blade, click **Create a new schedule**</span></span>

![Krok 8][8]

### <a name="step-2"></a><span data-ttu-id="adb7c-161">Krok 2</span><span class="sxs-lookup"><span data-stu-id="adb7c-161">Step 2</span></span>

<span data-ttu-id="adb7c-162">Na powitania **nowy harmonogram** bloku wypełniania hello informacje o harmonogramie.</span><span class="sxs-lookup"><span data-stu-id="adb7c-162">On hello **New Schedule** blade fill out hello schedule information.</span></span> <span data-ttu-id="adb7c-163">Witaj wartości, które można ustawić znajdują się w hello następującej listy:</span><span class="sxs-lookup"><span data-stu-id="adb7c-163">hello values that can be set are in hello following list:</span></span>

- <span data-ttu-id="adb7c-164">**Nazwa** -hello przyjazną nazwę hello harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="adb7c-164">**Name** - hello friendly name of hello schedule.</span></span>
- <span data-ttu-id="adb7c-165">**Opis elementu** — opis hello harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="adb7c-165">**Description** - A description of hello schedule.</span></span>
- <span data-ttu-id="adb7c-166">**Uruchamia** — ta wartość jest kombinacją datę, godzinę i strefę czasową, wchodzące w skład hello czasu hello harmonogram wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="adb7c-166">**Starts** - This value is a combination of date, time, and time zone that make up hello time hello schedule triggers.</span></span>
- <span data-ttu-id="adb7c-167">**Cykl** — ta wartość określa hello harmonogramy powtarzania.</span><span class="sxs-lookup"><span data-stu-id="adb7c-167">**Recurrence** - This value determines hello schedules repetition.</span></span>  <span data-ttu-id="adb7c-168">Prawidłowe wartości to **raz** lub **cykliczny**.</span><span class="sxs-lookup"><span data-stu-id="adb7c-168">Valid values are **Once** or **Recurring**.</span></span>
- <span data-ttu-id="adb7c-169">**Powtarzanie co** -hello interwał cyklu harmonogramu hello w godziny, dni, tygodnie lub miesiące.</span><span class="sxs-lookup"><span data-stu-id="adb7c-169">**Recur every** - hello recurrence interval of hello schedule in hours, days, weeks, or months.</span></span>
- <span data-ttu-id="adb7c-170">**Ustawienia okresu ważności** -hello wartość określa, czy harmonogram hello wygaśnięcia lub nie.</span><span class="sxs-lookup"><span data-stu-id="adb7c-170">**Set Expiration** - hello value determines if hello schedule should expire or not.</span></span> <span data-ttu-id="adb7c-171">Można ustawić także**tak** lub **nr**.</span><span class="sxs-lookup"><span data-stu-id="adb7c-171">Can be set too**Yes** or **No**.</span></span> <span data-ttu-id="adb7c-172">Nieprawidłowa data i godzina są toobe podany, jeśli tak jest wybierany.</span><span class="sxs-lookup"><span data-stu-id="adb7c-172">A valid date and time are toobe provided if yes is chosen.</span></span>

> [!NOTE]
> <span data-ttu-id="adb7c-173">Jeśli potrzebujesz toohave częściej niż co godzinę uruchomienia elementu runbook, wiele harmonogramów musi być utworzone na różnych interwałów (to znaczy, 15, 30, 45 minut po godzinie hello)</span><span class="sxs-lookup"><span data-stu-id="adb7c-173">If you need toohave a runbook run more often than every hour, multiple schedules must be created at different intervals (that is, 15, 30, 45 minutes after hello hour)</span></span>

![Krok 9][9]

### <a name="step-3"></a><span data-ttu-id="adb7c-175">Krok 3</span><span class="sxs-lookup"><span data-stu-id="adb7c-175">Step 3</span></span>

<span data-ttu-id="adb7c-176">Kliknij przycisk Zapisz toosave hello harmonogram toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="adb7c-176">Click Save toosave hello schedule toohello runbook.</span></span>

![Krok 10][10]

## <a name="next-steps"></a><span data-ttu-id="adb7c-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="adb7c-178">Next steps</span></span>

<span data-ttu-id="adb7c-179">Teraz, gdy wiedzę na temat toointegrate obserwatora sieciowego rozwiązywania problemów w usłudze Automatyzacja Azure, Dowiedz się, jak przechwytywanie pakietów tootrigger alerty maszyny Wirtualnej, odwiedzając [utworzyć przechwytywania alertów wyzwalanych pakietów z obserwatora sieciowego Azure](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="adb7c-179">Now that you have an understanding on how toointegrate Network Watcher troubleshooting with Azure Automation, learn how tootrigger packet captures on VM alerts by visiting [Create an alert triggered packet capture with Azure Network Watcher](network-watcher-alert-triggered-packet-capture.md).</span></span>

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
