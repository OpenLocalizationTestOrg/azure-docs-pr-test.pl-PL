---
title: aaaTroubleshoot problemy aktywacji maszyny wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Udostępnia hello Rozwiązywanie problemów z kroki rozwiązywania problemów aktywacji maszyny wirtualnej systemu Windows na platformie Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 4ebdac66166e80dcd68cd9e2931b30a29ac01eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a><span data-ttu-id="6835c-103">Rozwiązywanie problemów aktywacji maszyny wirtualnej systemu Windows Azure</span><span class="sxs-lookup"><span data-stu-id="6835c-103">Troubleshoot Azure Windows virtual machine activation problems</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="6835c-104">Jeśli masz problemy podczas aktywacji maszyny wirtualnej systemu Windows Azure (VM), która jest tworzona na podstawie obrazu niestandardowego, można użyć hello informacji dostępnych w problem hello tootroubleshoot tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="6835c-104">If you have trouble when activating Azure Windows virtual machine (VM) that is created from a custom image, you can use hello information provided in this document tootroubleshoot hello issue.</span></span> 

## <a name="symptom"></a><span data-ttu-id="6835c-105">Objaw</span><span class="sxs-lookup"><span data-stu-id="6835c-105">Symptom</span></span>

<span data-ttu-id="6835c-106">Podczas próby tooactivate maszyny Wirtualnej systemu Windows Azure, komunikat o błędzie podobny do wiadomość hello następujące przykładowe:</span><span class="sxs-lookup"><span data-stu-id="6835c-106">When you try tooactivate an Azure Windows VM, you receive an error message resembles hello following sample:</span></span>

<span data-ttu-id="6835c-107">**Błąd: hello 0xC004F074 LicensingService oprogramowania zgłosił, że nie można aktywować komputera hello. Można się skontaktować z nie ManagementService kluczami (KMS). Zobacz dziennik zdarzeń aplikacji hello, aby uzyskać dodatkowe informacje.**</span><span class="sxs-lookup"><span data-stu-id="6835c-107">**Error: 0xC004F074 hello Software LicensingService reported that hello computer could not be activated. No Key ManagementService (KMS) could be contacted. Please see hello Application Event Log for additional information.**</span></span>

## <a name="cause"></a><span data-ttu-id="6835c-108">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="6835c-108">Cause</span></span>
<span data-ttu-id="6835c-109">Ogólnie rzecz biorąc problemy dotyczące aktywacji maszyny Wirtualnej Azure wystąpić, jeśli hello maszyny Wirtualnej systemu Windows nie jest skonfigurowany przy użyciu hello odpowiedni klucz instalacji klienta usługi KMS lub hello maszyny Wirtualnej systemu Windows ma toohello problem łączności usługi Azure KMS (kms.core.windows.net, port 1668).</span><span class="sxs-lookup"><span data-stu-id="6835c-109">Generally, Azure VM activation issues occur if hello Windows VM is not configured by using hello appropriate KMS client setup key, or hello Windows VM has a connectivity problem toohello Azure KMS service (kms.core.windows.net, port 1668).</span></span> 

## <a name="solution"></a><span data-ttu-id="6835c-110">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="6835c-110">Solution</span></span>

>[!NOTE]
><span data-ttu-id="6835c-111">Jeśli używasz sieci VPN lokacja lokacja i wymuszone tunelowanie, zobacz [Azure Użyj niestandardowych kieruje tooenable aktywacji usługi KMS przy użyciu tunelowania wymuszonego](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span><span class="sxs-lookup"><span data-stu-id="6835c-111">If you are using a site-to-site VPN and forced tunneling, see [Use Azure custom routes tooenable KMS activation with forced tunneling](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span></span> 
>
><span data-ttu-id="6835c-112">Jeśli używasz usługi ExpressRoute i konieczne jest opublikowane trasy domyślnej, zobacz [maszyny Wirtualnej platformy Azure może się nie powieść tooactivate za pośrednictwem usługi ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span><span class="sxs-lookup"><span data-stu-id="6835c-112">If you are using ExpressRoute and you have a default route published, see [Azure VM may fail tooactivate over ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span></span>

### <a name="step-1-configure-hello-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a><span data-ttu-id="6835c-113">Krok 1 Konfiguruj hello odpowiedni klucz klienta usługi KMS instalacji (dla systemu Windows Server 2016 i Windows Server 2012 R2)</span><span class="sxs-lookup"><span data-stu-id="6835c-113">Step 1 Configure hello appropriate KMS client setup key (for Windows Server 2016 and Windows Server 2012 R2)</span></span>

<span data-ttu-id="6835c-114">W przypadku hello maszynę Wirtualną, która jest tworzona na podstawie niestandardowego obrazu systemu Windows Server 2016 lub Windows Server 2012 R2 należy skonfigurować hello odpowiedni klucz klienta usługi KMS instalacji dla hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6835c-114">For hello VM that is created from a custom image of Windows Server 2016 or Windows Server 2012 R2, you must configure hello appropriate KMS client setup key for hello VM.</span></span>

<span data-ttu-id="6835c-115">Ten krok nie obejmuje tooWindows 2012 lub Windows 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="6835c-115">This step does not apply tooWindows 2012 or Windows 2008 R2.</span></span> <span data-ttu-id="6835c-116">Używa hello funkcji automatyzacji Aktywacja maszyny wirtualnej (AVMA), która jest obsługiwana tylko przez system Windows Server 2016 i Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="6835c-116">It uses hello Automation Virtual Machine Activation (AVMA) feature, which is supported only by Windows Server 2016 and Windows Server 2012 R2.</span></span>

1. <span data-ttu-id="6835c-117">Uruchom **slmgr.vbs/DLV** w wierszu polecenia z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="6835c-117">Run **slmgr.vbs /dlv** at an elevated command prompt.</span></span> <span data-ttu-id="6835c-118">Sprawdź hello opis wartość w danych wyjściowych hello, a następnie określ, czy został utworzony z detaliczne (kanał sprzedaży DETALICZNEJ) lub z nośnika licencji zbiorczej (VOLUME_KMSCLIENT):</span><span class="sxs-lookup"><span data-stu-id="6835c-118">Check hello Description value in hello output, and then determine whether it was created from retail (RETAIL channel) or volume (VOLUME_KMSCLIENT) license media:</span></span>
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. <span data-ttu-id="6835c-119">Jeśli **slmgr.vbs/DLV** przedstawia kanał sprzedaży DETALICZNEJ, uruchom następujące polecenia tooset hello hello [klucz instalacji klienta usługi KMS](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) hello wersji systemu Windows Server używana i wymusić tooretry aktywacji:</span><span class="sxs-lookup"><span data-stu-id="6835c-119">If **slmgr.vbs /dlv** shows RETAIL channel, run hello following commands tooset hello [KMS client setup key](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) for hello version of Windows Server being used, and force it tooretry activation:</span></span> 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    <span data-ttu-id="6835c-120">Na przykład dla systemu Windows Server 2016 centrum danych, możesz uruchomić hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6835c-120">For example, for Windows Server 2016 Datacenter, you would run hello following command:</span></span>

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-hello-connectivity-between-hello-vm-and-azure-kms-service"></a><span data-ttu-id="6835c-121">Krok 2 Sprawdź hello łączność między hello maszyny Wirtualnej i usługa Azure KMS</span><span class="sxs-lookup"><span data-stu-id="6835c-121">Step 2 Verify hello connectivity between hello VM and Azure KMS service</span></span>

1. <span data-ttu-id="6835c-122">Pobierać i wyodrębniać hello [narzędzia Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) narzędzie tooa lokalny folder w hello maszynę Wirtualną, która nie jest aktywowany.</span><span class="sxs-lookup"><span data-stu-id="6835c-122">Download and extract hello [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) tool tooa local folder in hello VM that does not activate.</span></span> 

2. <span data-ttu-id="6835c-123">Przejdź tooStart, wyszukiwanie w programie Windows PowerShell, kliknij prawym przyciskiem myszy środowiska Windows PowerShell i wybierz polecenie Uruchom jako administrator.</span><span class="sxs-lookup"><span data-stu-id="6835c-123">Go tooStart, search on Windows PowerShell, right-click Windows PowerShell, and then select Run as administrator.</span></span>

3. <span data-ttu-id="6835c-124">Upewnij się, że hello, że maszyna wirtualna jest skonfigurowana toouse hello właściwym serwerem usługi KMS Azure.</span><span class="sxs-lookup"><span data-stu-id="6835c-124">Make sure that hello VM is configured toouse hello correct Azure KMS server.</span></span> <span data-ttu-id="6835c-125">toodo to uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6835c-125">toodo this, run the following command:</span></span>
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    <span data-ttu-id="6835c-126">polecenie Hello powinna zwracać: Nazwa komputera usługi zarządzania kluczami pomyślnie ustawiono tookms.core.windows.net:1688.</span><span class="sxs-lookup"><span data-stu-id="6835c-126">hello command should return: Key Management Service machine name set tookms.core.windows.net:1688 successfully.</span></span>

4. <span data-ttu-id="6835c-127">Sprawdź przy użyciu narzędzia Psping, że serwer usługi KMS toohello łączności.</span><span class="sxs-lookup"><span data-stu-id="6835c-127">Verify by using Psping that you have connectivity toohello KMS server.</span></span> <span data-ttu-id="6835c-128">Przełącz toohello folder, w którym wyodrębniono hello Pstools.zip pobierania, a następnie uruchom następujące hello:</span><span class="sxs-lookup"><span data-stu-id="6835c-128">Switch toohello folder where you extracted hello Pstools.zip download, and then run hello following:</span></span>
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  <span data-ttu-id="6835c-129">Upewnij się, że jest wyświetlany w hello sekundy do ostatniego wiersza danych wyjściowych hello,: Wysłane = 4, odebrane = 4, utracone = 0 (0% straty).</span><span class="sxs-lookup"><span data-stu-id="6835c-129">In hello second-to-last line of hello output, make sure that you see: Sent = 4, Received = 4, Lost = 0 (0% loss).</span></span>

  <span data-ttu-id="6835c-130">Jeśli utracone jest większa niż 0 (zero), hello maszyny Wirtualnej nie ma serwer usługi KMS toohello łączności.</span><span class="sxs-lookup"><span data-stu-id="6835c-130">If Lost is greater than 0 (zero), hello VM does not have connectivity toohello KMS server.</span></span> <span data-ttu-id="6835c-131">W takiej sytuacji jeśli hello maszyna wirtualna jest w sieci wirtualnej i ma niestandardowy serwer DNS określona, należy się upewnić, że serwer DNS jest kms.core.windows.net tooresolve stanie.</span><span class="sxs-lookup"><span data-stu-id="6835c-131">In this situation, if hello VM is in a virtual network and has a custom DNS server specified, you must make sure that DNS server is able tooresolve kms.core.windows.net.</span></span> <span data-ttu-id="6835c-132">Możesz też zmienić hello tooone serwera DNS, który jest rozpoznawany kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="6835c-132">Or, change hello DNS server tooone that does resolve kms.core.windows.net.</span></span>

  <span data-ttu-id="6835c-133">Należy zauważyć, że po usunięciu wszystkich serwerów DNS z sieci wirtualnej maszyn wirtualnych użyć wewnętrznego usługa DNS platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6835c-133">Notice that if you remove all DNS servers from a virtual network, VMs use Azure’s internal DNS service.</span></span> <span data-ttu-id="6835c-134">Ta usługa może zostać rozwiązany kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="6835c-134">This service can resolve kms.core.windows.net.</span></span>
  
<span data-ttu-id="6835c-135">Sprawdź także zaporą gościa hello nie został skonfigurowany w taki sposób, który może blokować próby aktywacji.</span><span class="sxs-lookup"><span data-stu-id="6835c-135">Also verify that hello guest firewall has not been configured in a manner that would block activation attempts.</span></span>

5. <span data-ttu-id="6835c-136">Po zweryfikowaniu tookms.core.windows.net połączenie powiodło się uruchamianie hello następujące polecenia w tym wierszu środowiska Windows PowerShell z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="6835c-136">After you verify successful connectivity tookms.core.windows.net, run hello following command at that elevated Windows PowerShell prompt.</span></span> <span data-ttu-id="6835c-137">To polecenie podejmuje aktywacji wiele razy.</span><span class="sxs-lookup"><span data-stu-id="6835c-137">This command tries activation multiple times.</span></span>

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

<span data-ttu-id="6835c-138">Pomyślnej aktywacji zwraca informacje podobne następujących hello:</span><span class="sxs-lookup"><span data-stu-id="6835c-138">A successful activation returns information that resembles hello following:</span></span>

<span data-ttu-id="6835c-139">**Aktywowanie Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678)... Produkt aktywowany pomyślnie.**</span><span class="sxs-lookup"><span data-stu-id="6835c-139">**Activating Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) … Product activated successfully.**</span></span>

## <a name="faq"></a><span data-ttu-id="6835c-140">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="6835c-140">FAQ</span></span> 

### <a name="i-created-hello-windows-server-2016-from-azure-marketplace-do-i-need-tooconfigure-kms-key-for-activating-hello-windows-server-2016"></a><span data-ttu-id="6835c-141">Utworzony hello systemu Windows Server 2016 z portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6835c-141">I created hello Windows Server 2016 from Azure Marketplace.</span></span> <span data-ttu-id="6835c-142">Należy tooconfigure klucz usługi KMS do aktywacji systemu Windows Server 2016 hello?</span><span class="sxs-lookup"><span data-stu-id="6835c-142">Do I need tooconfigure KMS key for activating hello Windows Server 2016?</span></span> 
 
<span data-ttu-id="6835c-143">Nie.</span><span class="sxs-lookup"><span data-stu-id="6835c-143">No.</span></span> <span data-ttu-id="6835c-144">Obraz powitania w portalu Azure Marketplace ma hello odpowiedni klucz klienta usługi KMS instalacji już skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="6835c-144">hello image in Azure Marketplace has hello appropriate KMS client setup key already configured.</span></span> 

### <a name="does-windows-activation-work-hello-same-way-regardless-if-hello-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a><span data-ttu-id="6835c-145">Pracy aktywacji systemu Windows hello sam sposób niezależnie od Jeśli hello maszyna wirtualna używa Azure hybrydowego Użyj korzyści (HUB) lub nie?</span><span class="sxs-lookup"><span data-stu-id="6835c-145">Does Windows activation work hello same way regardless if hello VM is using Azure Hybrid Use Benefit (HUB) or not?</span></span> 
 
<span data-ttu-id="6835c-146">Tak.</span><span class="sxs-lookup"><span data-stu-id="6835c-146">Yes.</span></span> 
 
### <a name="what-happens-if-windows-activation-period-expires"></a><span data-ttu-id="6835c-147">Co się stanie, jeśli okres aktywacji systemu Windows?</span><span class="sxs-lookup"><span data-stu-id="6835c-147">What happens if Windows activation period expires?</span></span> 
 
<span data-ttu-id="6835c-148">Gdy upłynął okres prolongaty hello i systemu Windows nadal nie włączono, Windows Server 2008 R2 i nowszych wersjach systemu Windows zostanie wyświetlone dodatkowe powiadomienia dotyczące aktywacji.</span><span class="sxs-lookup"><span data-stu-id="6835c-148">When hello grace period has expired and Windows is still not activated, Windows Server 2008 R2 and later versions of Windows will show additional notifications about activating.</span></span> <span data-ttu-id="6835c-149">tapety pulpitu Hello pozostanie czarne i usługi Windows Update zainstaluje zabezpieczeń i tylko aktualizacje krytyczne, ale nie opcjonalne aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="6835c-149">hello desktop wallpaper remains black, and Windows Update will install security and critical updates only, but not optional updates.</span></span> <span data-ttu-id="6835c-150">Zobacz powiadomień hello sekcji u dołu hello hello [warunki licencyjne](http://technet.microsoft.com/en-us/library/ff793403.aspx) strony.</span><span class="sxs-lookup"><span data-stu-id="6835c-150">See  hello Notifications section at hello bottom of hello [Licensing Conditions](http://technet.microsoft.com/en-us/library/ff793403.aspx) page.</span></span>   

## <a name="need-help-contact-support"></a><span data-ttu-id="6835c-151">Potrzebujesz pomocy?</span><span class="sxs-lookup"><span data-stu-id="6835c-151">Need help?</span></span> <span data-ttu-id="6835c-152">Skontaktuj się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="6835c-152">Contact support.</span></span>
<span data-ttu-id="6835c-153">Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget szybkie rozwiązanie problemu.</span><span class="sxs-lookup"><span data-stu-id="6835c-153">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
