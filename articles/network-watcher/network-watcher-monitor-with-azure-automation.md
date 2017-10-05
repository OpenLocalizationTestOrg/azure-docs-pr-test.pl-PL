---
title: "Monitorowanie bramy sieci VPN z rozwiązywaniem problemów obserwatora sieciowego Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 55ec52dd0d94a0347cc67a8785b89611da955111
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a><span data-ttu-id="ec54b-103">Monitorowanie bramy sieci VPN z rozwiązywaniem problemów obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="ec54b-103">Monitor VPN gateways with Network Watcher troubleshooting</span></span>

<span data-ttu-id="ec54b-104">Bardzo ważne klientom niezawodne usługi jest uzyskania szczegółowych informacji na wydajność sieci.</span><span class="sxs-lookup"><span data-stu-id="ec54b-104">Gaining deep insights on your network performance is critical to provide reliable services to customers.</span></span> <span data-ttu-id="ec54b-105">Dlatego bardzo ważne jest szybkie wykrywanie warunków awarii sieci i podjąć działania naprawcze w celu złagodzenia warunku awarii.</span><span class="sxs-lookup"><span data-stu-id="ec54b-105">It is therefore critical to detect network outage conditions quickly and take corrective action to mitigate the outage condition.</span></span> <span data-ttu-id="ec54b-106">Automatyzacja Azure umożliwia wdrożenie i uruchom zadanie w sposób programowy za pomocą elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="ec54b-106">Azure Automation enables you to implement and run a task in a programmatic fashion through runbooks.</span></span> <span data-ttu-id="ec54b-107">Przy użyciu automatyzacji Azure tworzy doskonałe przepisu sieci ciągły i aktywnego monitorowania i alertów.</span><span class="sxs-lookup"><span data-stu-id="ec54b-107">Using Azure Automation creates a perfect recipe for performing continuous and proactive network monitoring and alerting.</span></span>

## <a name="scenario"></a><span data-ttu-id="ec54b-108">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="ec54b-108">Scenario</span></span>

<span data-ttu-id="ec54b-109">Scenariusz na poniższej ilustracji jest aplikacją wielowarstwowych z na połączenie lokalne za pomocą bramy sieci VPN i tunelowania.</span><span class="sxs-lookup"><span data-stu-id="ec54b-109">The scenario in the following image is a multi-tiered application, with on premises connectivity established using a VPN Gateway and tunnel.</span></span> <span data-ttu-id="ec54b-110">Zapewnienie, że brama sieci VPN i uruchomiona jest krytyczne znaczenie dla wydajności aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ec54b-110">Ensuring the VPN Gateway is up and running is critical to the applications performance.</span></span>

<span data-ttu-id="ec54b-111">Element runbook jest tworzony przy użyciu skryptu, aby sprawdzić stan połączenia tunelu VPN, aby sprawdzić stan tunelu połączenia przy użyciu interfejsu API Rozwiązywanie problemów z zasobów.</span><span class="sxs-lookup"><span data-stu-id="ec54b-111">A runbook is created with a script to check for connection status of the VPN tunnel, using the Resource Troubleshooting API to check for connection tunnel status.</span></span> <span data-ttu-id="ec54b-112">Jeśli stan nie jest w dobrej kondycji, wyzwalacz poczty e-mail są wysyłane do administratorów.</span><span class="sxs-lookup"><span data-stu-id="ec54b-112">If the status is not healthy, an email trigger is sent to administrators.</span></span>

![Przykładowy scenariusz][scenario]

<span data-ttu-id="ec54b-114">W tym scenariuszu obejmują:</span><span class="sxs-lookup"><span data-stu-id="ec54b-114">This scenario will:</span></span>

- <span data-ttu-id="ec54b-115">Tworzenie wywołania elementu runbook `Start-AzureRmNetworkWatcherResourceTroubleshooting` polecenia cmdlet, aby rozwiązać stan połączenia</span><span class="sxs-lookup"><span data-stu-id="ec54b-115">Create a runbook calling the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet to troubleshoot connection status</span></span>
- <span data-ttu-id="ec54b-116">Połącz harmonogram do elementu runbook</span><span class="sxs-lookup"><span data-stu-id="ec54b-116">Link a schedule to the runbook</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ec54b-117">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="ec54b-117">Before you begin</span></span>

<span data-ttu-id="ec54b-118">Przed rozpoczęciem tego scenariusza, musi mieć następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="ec54b-118">Before you start this scenario, you must have the following pre-requisites:</span></span>

- <span data-ttu-id="ec54b-119">Konto usługi Automatyzacja Azure w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="ec54b-119">An Azure automation account in Azure.</span></span> <span data-ttu-id="ec54b-120">Sprawdź, czy konto automatyzacji ma najnowszą modułów i ma również modułu AzureRM.Network.</span><span class="sxs-lookup"><span data-stu-id="ec54b-120">Ensure that the automation account has the latest modules and also has the AzureRM.Network module.</span></span> <span data-ttu-id="ec54b-121">Moduł AzureRM.Network jest dostępny w galerii modułu, jeśli konieczne jest dodanie go do Twojego konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="ec54b-121">The AzureRM.Network module is available in the module gallery if you need to add it to your automation account.</span></span>
- <span data-ttu-id="ec54b-122">Musi mieć zestaw poświadczeń, skonfiguruj w automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="ec54b-122">You must have a set of credentials configure in Azure Automation.</span></span> <span data-ttu-id="ec54b-123">Dowiedz się więcej o [zabezpieczeń usługi Automatyzacja Azure](../automation/automation-security-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ec54b-123">Learn more at [Azure Automation security](../automation/automation-security-overview.md)</span></span>
- <span data-ttu-id="ec54b-124">Prawidłowy adres serwera SMTP (Office 365, poczty e-mail lokalnego lub innej) i poświadczeń określonych w automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="ec54b-124">A valid SMTP server (Office 365, your on-premises email or another) and credentials defined in Azure Automation</span></span>
- <span data-ttu-id="ec54b-125">Skonfigurowana brama sieci wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ec54b-125">A configured Virtual Network Gateway in Azure.</span></span>
- <span data-ttu-id="ec54b-126">Istniejące konto magazynu z istniejącego kontenera do przechowywania dzienników w.</span><span class="sxs-lookup"><span data-stu-id="ec54b-126">An existing storage account with an existing container to store the logs in.</span></span>

> [!NOTE]
> <span data-ttu-id="ec54b-127">Infrastruktura opisany w poprzednim obrazu jest w celach ilustracyjnych i nie są tworzone z kroki zawarte w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="ec54b-127">The infrastructure depicted in the preceding image is for illustration purposes and are not created with the steps contained in this article.</span></span>

### <a name="create-the-runbook"></a><span data-ttu-id="ec54b-128">Tworzenie elementu runbook</span><span class="sxs-lookup"><span data-stu-id="ec54b-128">Create the runbook</span></span>

<span data-ttu-id="ec54b-129">Pierwszym krokiem do konfigurowania w przykładzie jest można utworzyć elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="ec54b-129">The first step to configuring the example is to create the runbook.</span></span> <span data-ttu-id="ec54b-130">W tym przykładzie użyto konta Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="ec54b-130">This example uses a run-as account.</span></span> <span data-ttu-id="ec54b-131">Więcej informacji o kontach Uruchom jako można znaleźć [uwierzytelniania elementy Runbook za pomocą konta Uruchom jako platformy Azure](../automation/automation-sec-configure-azure-runas-account.md)</span><span class="sxs-lookup"><span data-stu-id="ec54b-131">To learn about run-as accounts, visit [Authenticate Runbooks with Azure Run As account](../automation/automation-sec-configure-azure-runas-account.md)</span></span>

### <a name="step-1"></a><span data-ttu-id="ec54b-132">Krok 1</span><span class="sxs-lookup"><span data-stu-id="ec54b-132">Step 1</span></span>

<span data-ttu-id="ec54b-133">Przejdź do usługi Automatyzacja Azure w [portalu Azure](https://portal.azure.com) i kliknij przycisk **elementów Runbook**</span><span class="sxs-lookup"><span data-stu-id="ec54b-133">Navigate to Azure Automation in the [Azure portal](https://portal.azure.com) and click **Runbooks**</span></span>

![Przegląd konta automatyzacji][1]

### <a name="step-2"></a><span data-ttu-id="ec54b-135">Krok 2</span><span class="sxs-lookup"><span data-stu-id="ec54b-135">Step 2</span></span>

<span data-ttu-id="ec54b-136">Kliknij przycisk **Dodaj element runbook** do rozpoczęcia procesu tworzenia elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="ec54b-136">Click **Add a runbook** to start the creation process of the runbook.</span></span>

![elementy runbook bloku][2]

### <a name="step-3"></a><span data-ttu-id="ec54b-138">Krok 3</span><span class="sxs-lookup"><span data-stu-id="ec54b-138">Step 3</span></span>

<span data-ttu-id="ec54b-139">W obszarze **szybkie tworzenie**, kliknij przycisk **Utwórz nowy element runbook** można utworzyć elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="ec54b-139">Under **Quick Create**, click **Create a new runbook** to create the runbook.</span></span>

![Dodawanie bloku elementu runbook][3]

### <a name="step-4"></a><span data-ttu-id="ec54b-141">Krok 4</span><span class="sxs-lookup"><span data-stu-id="ec54b-141">Step 4</span></span>

<span data-ttu-id="ec54b-142">W tym kroku będziemy nazwę elementu runbook, w tym przykładzie jest to **Get-VPNGatewayStatus**.</span><span class="sxs-lookup"><span data-stu-id="ec54b-142">In this step, we give the runbook a name, in the example it is called **Get-VPNGatewayStatus**.</span></span> <span data-ttu-id="ec54b-143">Jest ważne, aby dać nazwę opisową elementu runbook i zalecane nadanie mu nazwę zgodną z standard standardy nazewnictwa programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ec54b-143">It is important to give the runbook a descriptive name, and recommended giving it a name that follows standard PowerShell naming standards.</span></span> <span data-ttu-id="ec54b-144">Typ elementu runbook w tym przykładzie jest **PowerShell**, graficzne, przepływ pracy programu PowerShell, są inne opcje i przepływ pracy programu PowerShell graficznego.</span><span class="sxs-lookup"><span data-stu-id="ec54b-144">The runbook type for this example is **PowerShell**, the other options are Graphical, PowerShell workflow, and Graphical PowerShell workflow.</span></span>

![bloku elementu runbook][4]

### <a name="step-5"></a><span data-ttu-id="ec54b-146">Krok 5</span><span class="sxs-lookup"><span data-stu-id="ec54b-146">Step 5</span></span>

<span data-ttu-id="ec54b-147">W tym kroku tworzone elementu runbook w poniższym przykładzie kodu zawiera całego kodu, które są potrzebne w przykładzie.</span><span class="sxs-lookup"><span data-stu-id="ec54b-147">In this step the runbook is created, the following code example provides all the code needed for the example.</span></span> <span data-ttu-id="ec54b-148">Elementy w kodzie, które zawierają \<wartość\> należy zastąpić wartościami z subskrypcją.</span><span class="sxs-lookup"><span data-stu-id="ec54b-148">The items in the code that contain \<value\> need to be replaced with the values from your subscription.</span></span>

<span data-ttu-id="ec54b-149">Użyj następującego kodu jako kliknij **Zapisz**</span><span class="sxs-lookup"><span data-stu-id="ec54b-149">Use the following code as click **Save**</span></span>

```PowerShell
# Set these variables to the proper values for your environment
$o365AutomationCredential = "<Office 365 account>"
$fromEmail = "<from email address>"
$toEmail = "<to email address>"
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

# Get the connection "AzureRunAsConnection "
$servicePrincipalConnection=Get-AutomationConnection -Name $runAsConnectionName

"Logging in to Azure..."
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $servicePrincipalConnection.TenantId `
    -ApplicationId $servicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
"Setting context to a specific subscription"
Set-AzureRmContext -SubscriptionId $subscriptionId

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $region }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name $vpnConnectionName -ResourceGroupName $vpnConnectionResourceGroup
$sa = Get-AzureRmStorageAccount -Name $storageAccountName -ResourceGroupName $storageAccountResourceGroup 
$storagePath = "$($sa.PrimaryEndpoints.Blob)$($storageAccountContainer)"
$result = Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath $storagePath

if($result.code -ne "Healthy")
    {
        $body = "Connection for $($connection.name) is: $($result.code) `n$($result.results[0].summary) `nView the logs at $($storagePath) to learn more."
        Write-Output $body
        $subject = "$($connection.name) Status"
        Send-MailMessage `
        -To $toEmail `
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

### <a name="step-6"></a><span data-ttu-id="ec54b-150">Krok 6</span><span class="sxs-lookup"><span data-stu-id="ec54b-150">Step 6</span></span>

<span data-ttu-id="ec54b-151">Po zapisaniu elementu runbook harmonogramu musi być połączony na początku elementu runbook automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="ec54b-151">Once the runbook is saved, a schedule must be linked to it to automate the start of the runbook.</span></span> <span data-ttu-id="ec54b-152">Aby uruchomić proces, kliknij przycisk **harmonogram**.</span><span class="sxs-lookup"><span data-stu-id="ec54b-152">To start the process, click **Schedule**.</span></span>

![Krok 6][6]

## <a name="link-a-schedule-to-the-runbook"></a><span data-ttu-id="ec54b-154">Połącz harmonogram do elementu runbook</span><span class="sxs-lookup"><span data-stu-id="ec54b-154">Link a schedule to the runbook</span></span>

<span data-ttu-id="ec54b-155">Należy utworzyć nowy harmonogram.</span><span class="sxs-lookup"><span data-stu-id="ec54b-155">A new schedule must be created.</span></span> <span data-ttu-id="ec54b-156">Kliknij przycisk **Połącz harmonogram z elementem runbook**.</span><span class="sxs-lookup"><span data-stu-id="ec54b-156">Click **Link a schedule to your runbook**.</span></span>

![Krok 7][7]

### <a name="step-1"></a><span data-ttu-id="ec54b-158">Krok 1</span><span class="sxs-lookup"><span data-stu-id="ec54b-158">Step 1</span></span>

<span data-ttu-id="ec54b-159">Na **harmonogram** bloku, kliknij przycisk **Utwórz nowy harmonogram**</span><span class="sxs-lookup"><span data-stu-id="ec54b-159">On the **Schedule** blade, click **Create a new schedule**</span></span>

![Krok 8][8]

### <a name="step-2"></a><span data-ttu-id="ec54b-161">Krok 2</span><span class="sxs-lookup"><span data-stu-id="ec54b-161">Step 2</span></span>

<span data-ttu-id="ec54b-162">Na **nowy harmonogram** bloku Wypełnij informacje tego harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="ec54b-162">On the **New Schedule** blade fill out the schedule information.</span></span> <span data-ttu-id="ec54b-163">Są wartości, które można ustawić na poniższej liście:</span><span class="sxs-lookup"><span data-stu-id="ec54b-163">The values that can be set are in the following list:</span></span>

- <span data-ttu-id="ec54b-164">**Nazwa** -przyjazną nazwę harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="ec54b-164">**Name** - The friendly name of the schedule.</span></span>
- <span data-ttu-id="ec54b-165">**Opis elementu** — opis harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="ec54b-165">**Description** - A description of the schedule.</span></span>
- <span data-ttu-id="ec54b-166">**Uruchamia** — ta wartość jest kombinacją datę, godzinę i strefę czasową, wchodzące w skład czas wyzwalaczy harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="ec54b-166">**Starts** - This value is a combination of date, time, and time zone that make up the time the schedule triggers.</span></span>
- <span data-ttu-id="ec54b-167">**Cykl** — ta wartość określa powtarzania harmonogramów.</span><span class="sxs-lookup"><span data-stu-id="ec54b-167">**Recurrence** - This value determines the schedules repetition.</span></span>  <span data-ttu-id="ec54b-168">Prawidłowe wartości to **raz** lub **cykliczny**.</span><span class="sxs-lookup"><span data-stu-id="ec54b-168">Valid values are **Once** or **Recurring**.</span></span>
- <span data-ttu-id="ec54b-169">**Powtarzanie co** — interwał cyklu harmonogramu w godziny, dni, tygodnie lub miesiące.</span><span class="sxs-lookup"><span data-stu-id="ec54b-169">**Recur every** - The recurrence interval of the schedule in hours, days, weeks, or months.</span></span>
- <span data-ttu-id="ec54b-170">**Ustawienia okresu ważności** — wartość określa, czy harmonogram wygaśnięcia lub nie.</span><span class="sxs-lookup"><span data-stu-id="ec54b-170">**Set Expiration** - The value determines if the schedule should expire or not.</span></span> <span data-ttu-id="ec54b-171">Można ustawić **tak** lub **nr**.</span><span class="sxs-lookup"><span data-stu-id="ec54b-171">Can be set to **Yes** or **No**.</span></span> <span data-ttu-id="ec54b-172">Prawidłową datę i godzinę mają zostać podany, jeśli tak jest wybrany.</span><span class="sxs-lookup"><span data-stu-id="ec54b-172">A valid date and time are to be provided if yes is chosen.</span></span>

> [!NOTE]
> <span data-ttu-id="ec54b-173">Jeśli potrzebujesz częściej niż co godzinę uruchomienia elementu runbook, wiele harmonogramów musi zostać utworzony w różnych odstępach czasu (to znaczy, 15, 30, 45 minut po pełnej godzinie)</span><span class="sxs-lookup"><span data-stu-id="ec54b-173">If you need to have a runbook run more often than every hour, multiple schedules must be created at different intervals (that is, 15, 30, 45 minutes after the hour)</span></span>

![Krok 9][9]

### <a name="step-3"></a><span data-ttu-id="ec54b-175">Krok 3</span><span class="sxs-lookup"><span data-stu-id="ec54b-175">Step 3</span></span>

<span data-ttu-id="ec54b-176">Kliknij przycisk Zapisz, aby zapisać harmonogram do elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="ec54b-176">Click Save to save the schedule to the runbook.</span></span>

![Krok 10][10]

## <a name="next-steps"></a><span data-ttu-id="ec54b-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ec54b-178">Next steps</span></span>

<span data-ttu-id="ec54b-179">Teraz wiedzę na temat integracji obserwatora sieciowego Rozwiązywanie problemów z usługi Automatyzacja Azure, Dowiedz się, jak można wyzwolić przechwytywania pakietów na alerty maszyny Wirtualnej po przejściu na stronę [utworzyć przechwytywania alertów wyzwalanych pakietów z obserwatora sieciowego Azure](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="ec54b-179">Now that you have an understanding on how to integrate Network Watcher troubleshooting with Azure Automation, learn how to trigger packet captures on VM alerts by visiting [Create an alert triggered packet capture with Azure Network Watcher](network-watcher-alert-triggered-packet-capture.md).</span></span>

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
