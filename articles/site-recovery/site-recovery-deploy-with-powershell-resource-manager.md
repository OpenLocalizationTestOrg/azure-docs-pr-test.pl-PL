---
title: "aaaReplicate maszyn wirtualnych funkcji Hyper-V z programu PowerShell i usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Zautomatyzować hello replikacji maszyn wirtualnych funkcji Hyper-V tooAzure z usługą Azure Site Recovery przy użyciu programu PowerShell i Menedżera zasobów Azure."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: 
ms.assetid: 05e0d76e-c3f5-4845-8052-094019b6d102
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: 4fb15ce2e9ad54f1dd6f54ff769eb912aa4b0272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="4c7b0-103">Replikowanie między maszynami wirtualnymi funkcji Hyper-V lokalnymi i Azure przy użyciu programu PowerShell i usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4c7b0-103">Replicate between on-premises Hyper-V virtual machines and Azure by using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4c7b0-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4c7b0-104">Azure Portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="4c7b0-105">Program PowerShell — model usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4c7b0-105">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
> * [<span data-ttu-id="4c7b0-106">Klasyczny portal</span><span class="sxs-lookup"><span data-stu-id="4c7b0-106">Classic Portal</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a><span data-ttu-id="4c7b0-107">Omówienie</span><span class="sxs-lookup"><span data-stu-id="4c7b0-107">Overview</span></span>
<span data-ttu-id="4c7b0-108">Usługa Azure Site Recovery przyczynia się tooyour ciągłości i awaryjnego odzyskiwania strategii biznesowej poprzez organizowanie replikacji, trybu failover i odzyskiwania maszyn wirtualnych w różnych scenariuszy wdrażania.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-108">Azure Site Recovery contributes tooyour business continuity and disaster recovery strategy by orchestrating replication, failover, and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="4c7b0-109">Aby uzyskać pełną listę scenariuszy wdrażania, zobacz hello [Omówienie usługi Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4c7b0-109">For a full list of deployment scenarios, see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="4c7b0-110">Program Azure PowerShell jest moduł, który udostępnia polecenia cmdlet toomanage Azure za pomocą programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-110">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="4c7b0-111">Może współpracować z dwóch typów modułów: hello modułu Azure profilu lub hello moduł usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-111">It can work with two types of modules: hello Azure Profile module, or hello Azure Resource Manager module.</span></span>

<span data-ttu-id="4c7b0-112">Lokacji odzyskiwania poleceń cmdlet programu PowerShell, dostępna przy użyciu programu Azure PowerShell dla usługi Azure Resource Manager pomóc chronić i odzyskiwać serwerów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-112">Site Recovery PowerShell cmdlets, available with Azure PowerShell for Azure Resource Manager, help you protect and recover your servers in Azure.</span></span>

<span data-ttu-id="4c7b0-113">W tym artykule opisano sposób toouse środowiska Windows PowerShell razem z usługą Azure Resource Manager, toodeploy tooconfigure usługi Site Recovery i organizowania tooAzure ochrony serwera.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-113">This article describes how toouse Windows PowerShell, together with Azure Resource Manager, toodeploy Site Recovery tooconfigure and orchestrate server protection tooAzure.</span></span> <span data-ttu-id="4c7b0-114">przykład Witaj używane w tym artykule przedstawiono sposób tooprotect, tryb failover i odzyskiwanie maszyn wirtualnych na tooAzure hosta funkcji Hyper-V za pomocą programu Azure PowerShell z usługą Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-114">hello example used in this article shows you how tooprotect, fail over, and recover virtual machines on a Hyper-V host tooAzure, by using Azure PowerShell with Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="4c7b0-115">Witaj poleceń cmdlet programu PowerShell odzyskiwania lokacji obecnie pozwalają hello tooconfigure następujące: jeden tooanother witryny programu Virtual Machine Manager, tooAzure witryny programu Virtual Machine Manager i tooAzure lokacji funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-115">hello Site Recovery PowerShell cmdlets currently allow you tooconfigure hello following: one Virtual Machine Manager site tooanother, a Virtual Machine Manager site tooAzure, and a Hyper-V site tooAzure.</span></span>
>
>

<span data-ttu-id="4c7b0-116">Nie ma potrzeby toobe toouse ekspertów programu PowerShell w tym artykule, ale trzeba toounderstand hello podstawowe pojęcia, takie jak moduły, polecenia cmdlet i sesje.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-116">You don't need toobe a PowerShell expert toouse this article, but you do need toounderstand hello basic concepts, such as modules, cmdlets, and sessions.</span></span> <span data-ttu-id="4c7b0-117">Aby uzyskać więcej informacji na temat programu Windows PowerShell, zobacz [Wprowadzenie do programu Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span><span class="sxs-lookup"><span data-stu-id="4c7b0-117">For more information about Windows PowerShell, see [Getting Started with Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span></span>

<span data-ttu-id="4c7b0-118">Można również uzyskać więcej informacji [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="4c7b0-118">You can also read more about [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4c7b0-119">Partnerzy firmy Microsoft, które są częścią programu Cloud Solution Provider (CSP) hello można konfigurować i zarządzać ochrony serwerów ich klientom odpowiednich klientów tootheir subskrypcje dostawcy usług Kryptograficznych (subskrypcje dzierżawy).</span><span class="sxs-lookup"><span data-stu-id="4c7b0-119">Microsoft partners that are part of hello Cloud Solution Provider (CSP) program can configure and manage protection of their customers' servers tootheir customers' respective CSP subscriptions (tenant subscriptions).</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="4c7b0-120">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="4c7b0-120">Before you start</span></span>
<span data-ttu-id="4c7b0-121">Upewnij się, że te wymagania wstępne zostały spełnione:</span><span class="sxs-lookup"><span data-stu-id="4c7b0-121">Make sure you have these prerequisites in place:</span></span>

* <span data-ttu-id="4c7b0-122">A [Microsoft Azure](https://azure.microsoft.com/) konta.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-122">A [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="4c7b0-123">Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4c7b0-123">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="4c7b0-124">Ponadto możesz przeczytać temat [cennik usługi Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="4c7b0-124">In addition, you can read about [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="4c7b0-125">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-125">Azure PowerShell 1.0.</span></span> <span data-ttu-id="4c7b0-126">Aby uzyskać informacje na temat tej wersji i w jaki sposób tooinstall, zobacz [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="4c7b0-126">For information about this release and how tooinstall it, see [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span></span>
* <span data-ttu-id="4c7b0-127">Witaj [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) i [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modułów.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-127">hello [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) and [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modules.</span></span> <span data-ttu-id="4c7b0-128">Możesz pobrać najnowsze wersje tych modułów hello ze hello [galerii programu PowerShell](https://www.powershellgallery.com/)</span><span class="sxs-lookup"><span data-stu-id="4c7b0-128">You can get hello latest versions of these modules from hello [PowerShell gallery](https://www.powershellgallery.com/)</span></span>

<span data-ttu-id="4c7b0-129">W tym artykule przedstawiono sposób toouse programu Azure Powershell z tooconfigure usługi Azure Resource Manager i zarządzania ochroną serwerów.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-129">This article illustrates how toouse Azure Powershell with Azure Resource Manager tooconfigure and manage protection of your servers.</span></span> <span data-ttu-id="4c7b0-130">przykład Witaj używane w tym artykule przedstawiono sposób tooprotect maszynę wirtualną na hoście funkcji Hyper-V, tooAzure uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-130">hello example used in this article shows you how tooprotect a virtual machine, running on a Hyper-V host, tooAzure.</span></span> <span data-ttu-id="4c7b0-131">Witaj następujące wymagania wstępne są określone toothis przykładów.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-131">hello following prerequisites are specific toothis example.</span></span> <span data-ttu-id="4c7b0-132">Wyczerpujący zestaw wymagań dotyczących hello różne scenariusze odzyskiwania lokacji, zapoznaj się z dokumentacją toohello dotyczące toothat scenariusza.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-132">For a more comprehensive set of requirements for hello various Site Recovery scenarios, refer toohello documentation pertaining toothat scenario.</span></span>

* <span data-ttu-id="4c7b0-133">Hosta funkcji Hyper-V z systemem Windows Server 2012 R2 lub Microsoft Hyper-V Server 2012 R2 zawierającego co najmniej jednej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-133">A Hyper-V host running Windows Server 2012 R2 or Microsoft Hyper-V Server 2012 R2 containing one or more virtual machines.</span></span>
* <span data-ttu-id="4c7b0-134">Serwery funkcji Hyper-V połączony toohello Internetu, bezpośrednio lub za pośrednictwem serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-134">Hyper-V servers connected toohello Internet, either directly or through a proxy.</span></span>
* <span data-ttu-id="4c7b0-135">Witaj maszyn wirtualnych, które mają tooprotect powinna być zgodna z [wymagania wstępne dotyczące maszyny wirtualnej](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="4c7b0-135">hello virtual machines you want tooprotect should conform with [Virtual Machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

## <a name="step-1-sign-in-tooyour-azure-account"></a><span data-ttu-id="4c7b0-136">Krok 1: Zaloguj się tooyour konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4c7b0-136">Step 1: Sign in tooyour Azure account</span></span>
1. <span data-ttu-id="4c7b0-137">Otwórz konsolę programu PowerShell i uruchom to polecenie toosign w tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-137">Open a PowerShell console and run this command toosign in tooyour Azure account.</span></span> <span data-ttu-id="4c7b0-138">polecenia cmdlet Hello powoduje wyświetlenie strony sieci web, która spowoduje wyświetlenie monitu o podanie poświadczeń konta.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-138">hello cmdlet brings up a web page that will prompt you for your account credentials.</span></span>

        Login-AzureRmAccount

    <span data-ttu-id="4c7b0-139">Alternatywnie możesz także dołączyć poświadczeń konta jako toohello parametru `Login-AzureRmAccount` polecenia cmdlet, za pomocą hello `-Credential` parametru.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-139">Alternately, you could also include your account credentials as a parameter toohello `Login-AzureRmAccount` cmdlet, by using hello `-Credential` parameter.</span></span>

    <span data-ttu-id="4c7b0-140">W przypadku dostawcy usług Kryptograficznych partnera pracy imieniu dzierżawcy Określ powitania klienta dzierżawcy, przy użyciu nazwy domeny głównej dla identyfikatora dzierżawcy lub dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-140">If you are CSP partner working on behalf of a tenant, specify hello customer as a tenant, by using their tenantID or tenant primary domain name.</span></span>

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. <span data-ttu-id="4c7b0-141">Konta może mieć kilka subskrypcji, więc należy skojarzyć hello subskrypcję toouse hello konta.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-141">An account can have several subscriptions, so you should associate hello subscription you want toouse with hello account.</span></span>

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. <span data-ttu-id="4c7b0-142">Sprawdź, czy subskrypcja jest zarejestrowanych toouse hello Azure dostawców dla usług odzyskiwania i Site Recovery przy użyciu następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="4c7b0-142">Verify that your subscription is registered toouse hello Azure providers for Recovery Services and Site Recovery, by using hello following commands:</span></span>

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   <span data-ttu-id="4c7b0-143">W hello dane wyjściowe tych poleceń, jeśli hello **RegistrationState** ustawiono zbyt**zarejestrowanej**, możesz przejść tooStep 2.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-143">In hello output of these commands, if hello **RegistrationState** is set too**Registered**, you can proceed tooStep 2.</span></span> <span data-ttu-id="4c7b0-144">Jeśli nie, należy zarejestrować dostawcę Brak hello w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-144">If not, you should register hello missing provider in your subscription.</span></span>

   <span data-ttu-id="4c7b0-145">Witaj tooregister dostawca usługi Azure Site Recovery i usług odzyskiwania, uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="4c7b0-145">tooregister hello Azure provider for Site Recovery and Recovery Services, run hello following commands:</span></span>

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   <span data-ttu-id="4c7b0-146">Sprawdź, czy dostawców hello pomyślnie zarejestrowane za pomocą następującego polecenia hello: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` i `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-146">Verify that hello providers registered successfully by using hello following commands: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` and `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span></span>

## <a name="step-2-set-up-hello-recovery-services-vault"></a><span data-ttu-id="4c7b0-147">Krok 2: Konfigurowanie powitalne magazyn usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="4c7b0-147">Step 2: Set up hello Recovery Services vault</span></span>
1. <span data-ttu-id="4c7b0-148">Utwórz grupę zasobów usługi Azure Resource Manager, w którym można będzie utworzyć magazyn hello, lub użyj istniejącej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-148">Create an Azure Resource Manager resource group in which you'll create hello vault, or use an existing resource group.</span></span> <span data-ttu-id="4c7b0-149">Można utworzyć nową grupę zasobów, przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4c7b0-149">You can create a new resource group by using hello following command:</span></span>

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    <span data-ttu-id="4c7b0-150">w przypadku, gdy zmienna hello $ResourceGroupName zawiera hello nazwę grupy zasobów hello ma toocreate, a zmienna hello $Geo zawiera hello Azure regionu, w których grupa zasobów hello toocreate (na przykład "Brazylia Południowa").</span><span class="sxs-lookup"><span data-stu-id="4c7b0-150">where hello $ResourceGroupName variable contains hello name of hello resource group you want toocreate, and hello $Geo variable contains hello Azure region in which toocreate hello resource group (for example, "Brazil South").</span></span>

    <span data-ttu-id="4c7b0-151">Można uzyskać listy grup zasobów w ramach subskrypcji, za pomocą hello `Get-AzureRmResourceGroup` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-151">You can obtain a list of resource groups in your subscription by using hello `Get-AzureRmResourceGroup` cmdlet.</span></span>
2. <span data-ttu-id="4c7b0-152">Utwórz nowy magazyn usług odzyskiwania Azure w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4c7b0-152">Create a new Azure Recovery Services vault as follows:</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    <span data-ttu-id="4c7b0-153">Można pobrać listy istniejących magazynów za pomocą hello `Get-AzureRmRecoveryServicesVault` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-153">You can retrieve a list of existing vaults by using hello `Get-AzureRmRecoveryServicesVault` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="4c7b0-154">Jeśli chcesz, aby operacje tooperform magazynów usługi Site Recovery utworzony przy użyciu klasycznego portalu hello lub hello modułu programu PowerShell do zarządzania usługi Azure, można pobrać listę takich magazynów za pomocą hello `Get-AzureRmSiteRecoveryVault` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-154">If you wish tooperform operations on Site Recovery vaults created using hello classic portal or hello Azure Service Management PowerShell module, you can retrieve a list of such vaults by using hello `Get-AzureRmSiteRecoveryVault` cmdlet.</span></span> <span data-ttu-id="4c7b0-155">Należy utworzyć nowy magazyn usług odzyskiwania dla wszystkich nowych operacji.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-155">You should create a new Recovery Services vault for all new operations.</span></span> <span data-ttu-id="4c7b0-156">Witaj magazynów usługi Site Recovery, utworzony wcześniej są obsługiwane, ale nie ma hello najnowszych funkcji.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-156">hello Site Recovery vaults you've created earlier are supported, but don't have hello latest features.</span></span>
>
>

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="4c7b0-157">Krok 3: Ustawianie hello kontekst magazynu usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="4c7b0-157">Step 3: Set hello Recovery Services vault context</span></span>
1. <span data-ttu-id="4c7b0-158">Ustaw kontekst magazynu hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="4c7b0-158">Set hello vault context by running hello following command:</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-hello-site"></a><span data-ttu-id="4c7b0-159">Krok 4: Tworzenie lokacji funkcji Hyper-V i wygenerowanie nowego klucza rejestracji magazynu hello witryny.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-159">Step 4: Create a Hyper-V site and generate a new vault registration key for hello site.</span></span>
1. <span data-ttu-id="4c7b0-160">Utwórz nową witrynę funkcji Hyper-V w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4c7b0-160">Create a new Hyper-V site as follows:</span></span>

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    <span data-ttu-id="4c7b0-161">To polecenie cmdlet uruchamia lokacji hello toocreate zadania usługi Site Recovery i zwraca obiekt zadania usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-161">This cmdlet starts a Site Recovery job toocreate hello site, and returns a Site Recovery job object.</span></span> <span data-ttu-id="4c7b0-162">Poczekaj, aż hello toocomplete zadania i Sprawdź zadania hello zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-162">Wait for hello job toocomplete and verify that hello job completed successfully.</span></span>

    <span data-ttu-id="4c7b0-163">Można pobrać obiektu zadania hello i tym samym sprawdź bieżący stan zadania hello hello za pomocą polecenia cmdlet Get-AzureRmSiteRecoveryJob hello.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-163">You can retrieve hello job object, and thereby check hello current status of hello job, by using hello Get-AzureRmSiteRecoveryJob cmdlet.</span></span>
2. <span data-ttu-id="4c7b0-164">Generowanie i Pobierz klucz rejestracji dla lokacji hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4c7b0-164">Generate and download a registration key for hello site, as follows:</span></span>

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    <span data-ttu-id="4c7b0-165">Kopia hello pobrane hosta klucza toohello funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-165">Copy hello downloaded key toohello Hyper-V host.</span></span> <span data-ttu-id="4c7b0-166">Należy hello klucza tooregister hello funkcji Hyper-V host toohello lokacji.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-166">You need hello key tooregister hello Hyper-V host toohello site.</span></span>

## <a name="step-5-install-hello-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a><span data-ttu-id="4c7b0-167">Krok 5: Instalowanie dostawcy usługi Azure Site Recovery hello i Agent usług odzyskiwania Azure na hoście funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="4c7b0-167">Step 5: Install hello Azure Site Recovery provider and Azure Recovery Services Agent on your Hyper-V host</span></span>
1. <span data-ttu-id="4c7b0-168">Pobierz Instalator hello hello najnowsza wersja dostawcy hello z [Microsoft](https://aka.ms/downloaddra).</span><span class="sxs-lookup"><span data-stu-id="4c7b0-168">Download hello installer for hello latest version of hello provider from [Microsoft](https://aka.ms/downloaddra).</span></span>
2. <span data-ttu-id="4c7b0-169">Hello uruchom Instalator na hoście funkcji Hyper-V, a na końcu instalacji hello hello nadal toohello kroku rejestracji.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-169">Run hello installer on your Hyper-V host, and at hello end of hello installation continue toohello registration step.</span></span>
3. <span data-ttu-id="4c7b0-170">Po wyświetleniu monitu podaj hello pobranych klucz rejestracji lokacji i zakończyć rejestrację witryny toohello hosta funkcji Hyper-V hello.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-170">When prompted, provide hello downloaded site registration key, and complete registration of hello Hyper-V host toohello site.</span></span>
4. <span data-ttu-id="4c7b0-171">Sprawdź, czy hostujących hello funkcji Hyper-V jest zarejestrowany toohello lokacji za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="4c7b0-171">Verify that hello Hyper-V host is registered toohello site by using hello following command:</span></span>

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-hello-protection-container"></a><span data-ttu-id="4c7b0-172">Krok 6: Tworzenie zasad replikacji i powiązać ją z kontenera ochrony hello</span><span class="sxs-lookup"><span data-stu-id="4c7b0-172">Step 6: Create a replication policy and associate it with hello protection container</span></span>
1. <span data-ttu-id="4c7b0-173">Utwórz zasady replikacji w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4c7b0-173">Create a replication policy as follows:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    <span data-ttu-id="4c7b0-174">Witaj wyboru zwrócił tooensure zadania, które tworzenia zasad replikacji hello zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-174">Check hello returned job tooensure that hello replication policy creation succeeds.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4c7b0-175">Witaj określone konto magazynu powinna być w hello tego samego regionu Azure co magazyn usług odzyskiwania i ma włączoną replikację geograficzną.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-175">hello storage account specified should be in hello same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="4c7b0-176">Jeśli hello określony odzyskiwania konta magazynu jest typu usługi Azure Storage (klasyczny), pracy w trybie failover hello chronione maszyny Odzyskaj hello maszyny tooAzure IaaS (klasyczny).</span><span class="sxs-lookup"><span data-stu-id="4c7b0-176">If hello specified Recovery storage account is of type Azure Storage (Classic), failover of hello protected machines recover hello machine tooAzure IaaS (Classic).</span></span>
   > * <span data-ttu-id="4c7b0-177">Jeśli hello określono konto magazynu odzyskiwania jest typu magazynu Azure (Azure Resource Manager), pracy w trybie failover hello chronione maszyny Odzyskaj hello maszyny tooAzure IaaS (usługi Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="4c7b0-177">If hello specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of hello protected machines recover hello machine tooAzure IaaS (Azure Resource Manager).</span></span>
   >
   >
2. <span data-ttu-id="4c7b0-178">Pobierz hello ochrony kontenera odpowiedniej toohello lokacji, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4c7b0-178">Get hello protection container corresponding toohello site, as follows:</span></span>

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. <span data-ttu-id="4c7b0-179">Uruchom skojarzenia hello kontenera ochrony hello hello zasady replikacji, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4c7b0-179">Start hello association of hello protection container with hello replication policy, as follows:</span></span>

     <span data-ttu-id="4c7b0-180">$Policy = get-AzureRmSiteRecoveryPolicy - FriendlyName $PolicyName $associationJob = Start AzureRmSiteRecoveryPolicyAssociationJob-$Policy zasad - PrimaryProtectionContainer $protectionContainer</span><span class="sxs-lookup"><span data-stu-id="4c7b0-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span></span>

   <span data-ttu-id="4c7b0-181">Poczekaj, aż hello skojarzenia zadania toocomplete i upewnij się, czy zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-181">Wait for hello association job toocomplete, and ensure that it completed successfully.</span></span>

## <a name="step-7-enable-protection-for-virtual-machines"></a><span data-ttu-id="4c7b0-182">Krok 7: Włączanie ochrony dla maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="4c7b0-182">Step 7: Enable protection for virtual machines</span></span>
1. <span data-ttu-id="4c7b0-183">Pobierz odpowiedni toohello jednostki ochrony hello maszyna wirtualna ma tooprotect, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4c7b0-183">Get hello protection entity corresponding toohello VM you want tooprotect, as follows:</span></span>

        $VMFriendlyName = "Fabrikam-app"                    #Name of hello VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. <span data-ttu-id="4c7b0-184">Start ochrona powitalnych maszyny wirtualnej, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4c7b0-184">Start protecting hello virtual machine, as follows:</span></span>

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > <span data-ttu-id="4c7b0-185">Witaj określone konto magazynu powinna być w hello tego samego regionu Azure co magazyn usług odzyskiwania i ma włączoną replikację geograficzną.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-185">hello storage account specified should be in hello same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="4c7b0-186">Jeśli hello określony odzyskiwania konta magazynu jest typu usługi Azure Storage (klasyczny), pracy w trybie failover hello chronione maszyny Odzyskaj hello maszyny tooAzure IaaS (klasyczny).</span><span class="sxs-lookup"><span data-stu-id="4c7b0-186">If hello specified Recovery storage account is of type Azure Storage (Classic), failover of hello protected machines recover hello machine tooAzure IaaS (Classic).</span></span>
   > * <span data-ttu-id="4c7b0-187">Jeśli hello określono konto magazynu odzyskiwania jest typu magazynu Azure (Azure Resource Manager), pracy w trybie failover hello chronione maszyny Odzyskaj hello maszyny tooAzure IaaS (usługi Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="4c7b0-187">If hello specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of hello protected machines recover hello machine tooAzure IaaS (Azure Resource Manager).</span></span>
   >
   > <span data-ttu-id="4c7b0-188">Jeśli hello chronisz maszyny Wirtualnej ma więcej niż jedną tooit dołączony na dysku, określ dysk systemu operacyjnego hello przy użyciu hello *OSDiskName* parametru.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-188">If hello VM you are protecting has more than one disk attached tooit, specify hello operating system disk by using hello *OSDiskName* parameter.</span></span>
   >
   >
3. <span data-ttu-id="4c7b0-189">Poczekaj na powitania tooreach maszyn wirtualnych chronionych stanu po replikacji początkowej hello.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-189">Wait for hello virtual machines tooreach a protected state after hello initial replication.</span></span> <span data-ttu-id="4c7b0-190">Może to potrwać kilka minut w zależności od czynników, takich jak hello ilość danych toobe replikowane. i hello tooAzure dostępną przepustowość nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-190">This can take a while, depending on factors such as hello amount of data toobe replicated and hello available upstream bandwidth tooAzure.</span></span> <span data-ttu-id="4c7b0-191">Stan zadania Hello i StateDescription zaktualizowano następujące na powitania osiągnięcia chronionych stan maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-191">hello job State and StateDescription are updated as follows, upon hello VM reaching a protected state.</span></span>

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. <span data-ttu-id="4c7b0-192">Właściwości odzyskiwania, takich jak hello rozmiaru roli maszyny Wirtualnej i pracy awaryjnej hello sieć platformy Azure tooattach hello maszyny wirtualnej sieci interfejsu karty tooupon aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-192">Update recovery properties, such as hello VM role size, and hello Azure network tooattach hello virtual machine's network interface cards tooupon failover.</span></span>

        PS C:\> $nw1 = Get-AzureRmVirtualNetwork -Name "FailoverNw" -ResourceGroupName "MyRG"

        PS C:\> $VMFriendlyName = "Fabrikam-App"

        PS C:\> $VM = Get-AzureRmSiteRecoveryVM -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName

        PS C:\> $UpdateJob = Set-AzureRmSiteRecoveryVM -VirtualMachine $VM -PrimaryNic $VM.NicDetailsList[0].NicId -RecoveryNetworkId $nw1.Id -RecoveryNicSubnetName $nw1.Subnets[0].Name

        PS C:\> $UpdateJob = Get-AzureRmSiteRecoveryJob -Job $UpdateJob

        PS C:\> $UpdateJob

        Name             : b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        ID               : /Subscriptions/a731825f-4bf2-4f81-a611-c331b272206e/resourceGroups/MyRG/providers/Microsoft.RecoveryServices/vault
                           s/MyVault/replicationJobs/b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        Type             : Microsoft.RecoveryServices/vaults/replicationJobs
        JobType          : UpdateVmProperties
        DisplayName      : Update hello virtual machine
        ClientRequestId  : 805a22a3-be86-441c-9da8-f32685673112-2015-12-10 17:55:51Z-P
        State            : Succeeded
        StateDescription : Completed
        StartTime        : 10-12-2015 17:55:53 +00:00
        EndTime          : 10-12-2015 17:55:54 +00:00
        TargetObjectId   : 289682c6-c5e6-42dc-a1d2-5f9621f78ae6
        TargetObjectType : ProtectionEntity
        TargetObjectName : Fabrikam-App
        AllowedActions   : {Restart}
        Tasks            : {UpdateVmPropertiesTask}
        Errors           : {}



## <a name="step-8-run-a-test-failover"></a><span data-ttu-id="4c7b0-193">Krok 8: Uruchom test trybu failover</span><span class="sxs-lookup"><span data-stu-id="4c7b0-193">Step 8: Run a test failover</span></span>
1. <span data-ttu-id="4c7b0-194">Uruchom zadania testowego trybu failover, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4c7b0-194">Run a test failover job, as follows:</span></span>

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. <span data-ttu-id="4c7b0-195">Sprawdź test hello utworzenia maszyny Wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-195">Verify that hello test VM is created in Azure.</span></span> <span data-ttu-id="4c7b0-196">(hello test pracy awaryjnej zadanie zostanie zawieszone, po utworzeniu hello testowej maszyny Wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-196">(hello test failover job is suspended, after creating hello test VM in Azure.</span></span> <span data-ttu-id="4c7b0-197">Witaj zadanie zostało ukończone przez czyszczenie artefaktów hello utworzona po wznowieniu zadania hello, jak pokazano w następnym kroku hello.)</span><span class="sxs-lookup"><span data-stu-id="4c7b0-197">hello job completes by cleaning up hello created artefacts upon resuming hello job, as illustrated in hello next step.)</span></span>
3. <span data-ttu-id="4c7b0-198">Hello pełny test trybu failover, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4c7b0-198">Complete hello test failover, as follows:</span></span>

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a><span data-ttu-id="4c7b0-199">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4c7b0-199">Next Steps</span></span>
<span data-ttu-id="4c7b0-200">[Dowiedz się więcej](https://msdn.microsoft.com/library/azure/mt637930.aspx) dotyczące usługi Azure Site Recovery za pomocą poleceń cmdlet programu PowerShell usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4c7b0-200">[Read more](https://msdn.microsoft.com/library/azure/mt637930.aspx) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
