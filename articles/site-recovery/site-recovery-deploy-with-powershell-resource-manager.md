---
title: "Replikowanie maszyn wirtualnych funkcji Hyper-V z programu PowerShell i usługa Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Automatyzowanie replikacji maszyn wirtualnych funkcji Hyper-V do platformy Azure z usługą Azure Site Recovery przy użyciu programu PowerShell i Menedżera zasobów Azure."
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
ms.openlocfilehash: dbd562b73b0caecd0feb993bd6fb796dddb0438c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="431ac-103">Replikowanie między maszynami wirtualnymi funkcji Hyper-V lokalnymi i Azure przy użyciu programu PowerShell i usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="431ac-103">Replicate between on-premises Hyper-V virtual machines and Azure by using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="431ac-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="431ac-104">Azure Portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="431ac-105">Program PowerShell — model usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="431ac-105">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
> * [<span data-ttu-id="431ac-106">Klasyczny portal</span><span class="sxs-lookup"><span data-stu-id="431ac-106">Classic Portal</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a><span data-ttu-id="431ac-107">Omówienie</span><span class="sxs-lookup"><span data-stu-id="431ac-107">Overview</span></span>
<span data-ttu-id="431ac-108">Usługa Azure Site Recovery przyczynia się do strategii biznesowej ciągłości i odzyskiwaniem po awarii odzyskiwania poprzez organizowanie replikacji, trybu failover i odzyskiwania maszyn wirtualnych w różnych scenariuszy wdrażania.</span><span class="sxs-lookup"><span data-stu-id="431ac-108">Azure Site Recovery contributes to your business continuity and disaster recovery strategy by orchestrating replication, failover, and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="431ac-109">Aby uzyskać pełną listę scenariuszy wdrażania, zobacz [Omówienie usługi Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="431ac-109">For a full list of deployment scenarios, see the [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="431ac-110">Program Azure PowerShell jest moduł, który udostępnia polecenia cmdlet do zarządzania za pomocą środowiska Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="431ac-110">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="431ac-111">Może współpracować z dwóch typów modułów: moduł profilu Azure lub w module usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="431ac-111">It can work with two types of modules: the Azure Profile module, or the Azure Resource Manager module.</span></span>

<span data-ttu-id="431ac-112">Lokacji odzyskiwania poleceń cmdlet programu PowerShell, dostępna przy użyciu programu Azure PowerShell dla usługi Azure Resource Manager pomóc chronić i odzyskiwać serwerów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="431ac-112">Site Recovery PowerShell cmdlets, available with Azure PowerShell for Azure Resource Manager, help you protect and recover your servers in Azure.</span></span>

<span data-ttu-id="431ac-113">W tym artykule opisano sposób wdrażania usługi Site Recovery do konfigurowania i organizowania ochrony serwera na platformie Azure za pomocą programu Windows PowerShell, wraz z usługą Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="431ac-113">This article describes how to use Windows PowerShell, together with Azure Resource Manager, to deploy Site Recovery to configure and orchestrate server protection to Azure.</span></span> <span data-ttu-id="431ac-114">W przykładzie używane w tym artykule przedstawiono do ochrony, tryb failover i odzyskiwania maszyn wirtualnych na hoście funkcji Hyper-V do platformy Azure, przy użyciu programu Azure PowerShell z usługą Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="431ac-114">The example used in this article shows you how to protect, fail over, and recover virtual machines on a Hyper-V host to Azure, by using Azure PowerShell with Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="431ac-115">Polecenia cmdlet programu PowerShell odzyskiwania lokacji pozwalają obecnie skonfiguruj następujące opcje: jedna lokacja programu Virtual Machine Manager do innej lokacji programu Virtual Machine Manager na platformie Azure i lokacji funkcji Hyper-V do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="431ac-115">The Site Recovery PowerShell cmdlets currently allow you to configure the following: one Virtual Machine Manager site to another, a Virtual Machine Manager site to Azure, and a Hyper-V site to Azure.</span></span>
>
>

<span data-ttu-id="431ac-116">Nie trzeba być ekspertów PowerShell, aby użyć tego artykułu, ale należy zrozumieć podstawowe pojęcia, takie jak moduły, polecenia cmdlet i sesje.</span><span class="sxs-lookup"><span data-stu-id="431ac-116">You don't need to be a PowerShell expert to use this article, but you do need to understand the basic concepts, such as modules, cmdlets, and sessions.</span></span> <span data-ttu-id="431ac-117">Aby uzyskać więcej informacji na temat programu Windows PowerShell, zobacz [Wprowadzenie do programu Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span><span class="sxs-lookup"><span data-stu-id="431ac-117">For more information about Windows PowerShell, see [Getting Started with Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span></span>

<span data-ttu-id="431ac-118">Można również uzyskać więcej informacji [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="431ac-118">You can also read more about [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

> [!NOTE]
> <span data-ttu-id="431ac-119">Partnerzy firmy Microsoft, które są częścią programu Cloud Solution Provider (CSP) można konfigurować i zarządzać ochrony serwerów swoich klientów do ich klientom odpowiednich subskrypcji dostawcy usług Kryptograficznych (subskrypcje dzierżawy).</span><span class="sxs-lookup"><span data-stu-id="431ac-119">Microsoft partners that are part of the Cloud Solution Provider (CSP) program can configure and manage protection of their customers' servers to their customers' respective CSP subscriptions (tenant subscriptions).</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="431ac-120">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="431ac-120">Before you start</span></span>
<span data-ttu-id="431ac-121">Upewnij się, że te wymagania wstępne zostały spełnione:</span><span class="sxs-lookup"><span data-stu-id="431ac-121">Make sure you have these prerequisites in place:</span></span>

* <span data-ttu-id="431ac-122">A [Microsoft Azure](https://azure.microsoft.com/) konta.</span><span class="sxs-lookup"><span data-stu-id="431ac-122">A [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="431ac-123">Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="431ac-123">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="431ac-124">Ponadto możesz przeczytać temat [cennik usługi Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="431ac-124">In addition, you can read about [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="431ac-125">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="431ac-125">Azure PowerShell 1.0.</span></span> <span data-ttu-id="431ac-126">Informacje o tej wersji i sposobu jego instalacji, zobacz [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="431ac-126">For information about this release and how to install it, see [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span></span>
* <span data-ttu-id="431ac-127">[AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) i [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modułów.</span><span class="sxs-lookup"><span data-stu-id="431ac-127">The [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) and [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modules.</span></span> <span data-ttu-id="431ac-128">Możesz uzyskać najnowsze wersje tych modułów [galerii programu PowerShell](https://www.powershellgallery.com/)</span><span class="sxs-lookup"><span data-stu-id="431ac-128">You can get the latest versions of these modules from the [PowerShell gallery](https://www.powershellgallery.com/)</span></span>

<span data-ttu-id="431ac-129">W tym artykule przedstawiono sposób korzystania z usługi Azure Resource Manager programu Azure Powershell do konfigurowania i ochrony serwerów zarządzania.</span><span class="sxs-lookup"><span data-stu-id="431ac-129">This article illustrates how to use Azure Powershell with Azure Resource Manager to configure and manage protection of your servers.</span></span> <span data-ttu-id="431ac-130">Przykład używane w tym artykule przedstawiono sposób ochrony maszyny wirtualnej, uruchomiona na hoście funkcji Hyper-V do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="431ac-130">The example used in this article shows you how to protect a virtual machine, running on a Hyper-V host, to Azure.</span></span> <span data-ttu-id="431ac-131">Następujące wymagania wstępne są specyficzne dla tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="431ac-131">The following prerequisites are specific to this example.</span></span> <span data-ttu-id="431ac-132">Dla bardziej złożonego zestawu wymagania dla różnych scenariuszy odzyskiwania lokacji zapoznaj się z dokumentacją, dotyczące tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="431ac-132">For a more comprehensive set of requirements for the various Site Recovery scenarios, refer to the documentation pertaining to that scenario.</span></span>

* <span data-ttu-id="431ac-133">Hosta funkcji Hyper-V z systemem Windows Server 2012 R2 lub Microsoft Hyper-V Server 2012 R2 zawierającego co najmniej jednej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="431ac-133">A Hyper-V host running Windows Server 2012 R2 or Microsoft Hyper-V Server 2012 R2 containing one or more virtual machines.</span></span>
* <span data-ttu-id="431ac-134">Serwery funkcji Hyper-V jest połączony z Internetem bezpośrednio lub za pośrednictwem serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="431ac-134">Hyper-V servers connected to the Internet, either directly or through a proxy.</span></span>
* <span data-ttu-id="431ac-135">Maszyny wirtualne, które chcesz chronić powinna być zgodna z [wymagania wstępne dotyczące maszyny wirtualnej](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="431ac-135">The virtual machines you want to protect should conform with [Virtual Machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

## <a name="step-1-sign-in-to-your-azure-account"></a><span data-ttu-id="431ac-136">Krok 1: Zaloguj się do konta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="431ac-136">Step 1: Sign in to your Azure account</span></span>
1. <span data-ttu-id="431ac-137">Otwórz konsolę programu PowerShell i uruchom to polecenie, aby zalogować się do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="431ac-137">Open a PowerShell console and run this command to sign in to your Azure account.</span></span> <span data-ttu-id="431ac-138">Polecenie cmdlet powoduje wyświetlenie strony sieci web, która spowoduje wyświetlenie monitu o podanie poświadczeń konta.</span><span class="sxs-lookup"><span data-stu-id="431ac-138">The cmdlet brings up a web page that will prompt you for your account credentials.</span></span>

        Login-AzureRmAccount

    <span data-ttu-id="431ac-139">Alternatywnie możesz także dołączyć poświadczeń konta jako parametr `Login-AzureRmAccount` polecenia cmdlet, za pomocą `-Credential` parametru.</span><span class="sxs-lookup"><span data-stu-id="431ac-139">Alternately, you could also include your account credentials as a parameter to the `Login-AzureRmAccount` cmdlet, by using the `-Credential` parameter.</span></span>

    <span data-ttu-id="431ac-140">W przypadku dostawcy usług Kryptograficznych partnera pracy imieniu dzierżawcy określenia klienta dzierżawcy, przy użyciu nazwy domeny głównej dla identyfikatora dzierżawcy lub dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="431ac-140">If you are CSP partner working on behalf of a tenant, specify the customer as a tenant, by using their tenantID or tenant primary domain name.</span></span>

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. <span data-ttu-id="431ac-141">Konto może zawierać kilka subskrypcji, więc należy skojarzyć subskrypcję, której chcesz użyć przy użyciu konta.</span><span class="sxs-lookup"><span data-stu-id="431ac-141">An account can have several subscriptions, so you should associate the subscription you want to use with the account.</span></span>

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. <span data-ttu-id="431ac-142">Sprawdź, czy subskrypcja jest zarejestrowane do używania Azure dostawców usług odzyskiwania i lokacji odzyskiwania, za pomocą następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="431ac-142">Verify that your subscription is registered to use the Azure providers for Recovery Services and Site Recovery, by using the following commands:</span></span>

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   <span data-ttu-id="431ac-143">W danych wyjściowych polecenia Jeśli **RegistrationState** ustawiono **zarejestrowanej**, możesz przejść do kroku 2.</span><span class="sxs-lookup"><span data-stu-id="431ac-143">In the output of these commands, if the **RegistrationState** is set to **Registered**, you can proceed to Step 2.</span></span> <span data-ttu-id="431ac-144">Jeśli nie, należy zarejestrować dostawcę Brak w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="431ac-144">If not, you should register the missing provider in your subscription.</span></span>

   <span data-ttu-id="431ac-145">Aby zarejestrować dostawcę usługi Azure Site Recovery i usług odzyskiwania, uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="431ac-145">To register the Azure provider for Site Recovery and Recovery Services, run the following commands:</span></span>

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   <span data-ttu-id="431ac-146">Sprawdź, czy dostawców pomyślnie zarejestrowane za pomocą następujących poleceń: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` i `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span><span class="sxs-lookup"><span data-stu-id="431ac-146">Verify that the providers registered successfully by using the following commands: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` and `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span></span>

## <a name="step-2-set-up-the-recovery-services-vault"></a><span data-ttu-id="431ac-147">Krok 2: Konfigurowanie magazyn usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="431ac-147">Step 2: Set up the Recovery Services vault</span></span>
1. <span data-ttu-id="431ac-148">Utwórz grupę zasobów usługi Azure Resource Manager, w którym można będzie utworzyć magazyn, lub użyj istniejącej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="431ac-148">Create an Azure Resource Manager resource group in which you'll create the vault, or use an existing resource group.</span></span> <span data-ttu-id="431ac-149">Można utworzyć nową grupę zasobów za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="431ac-149">You can create a new resource group by using the following command:</span></span>

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    <span data-ttu-id="431ac-150">gdzie zmienna $ResourceGroupName zawiera nazwę grupy zasobów, które chcesz utworzyć, a zmienna $Geo region platformy Azure, w którym można utworzyć grupy zasobów (na przykład "Brazylia Południowa").</span><span class="sxs-lookup"><span data-stu-id="431ac-150">where the $ResourceGroupName variable contains the name of the resource group you want to create, and the $Geo variable contains the Azure region in which to create the resource group (for example, "Brazil South").</span></span>

    <span data-ttu-id="431ac-151">Można uzyskać listy grup zasobów w ramach subskrypcji, za pomocą `Get-AzureRmResourceGroup` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="431ac-151">You can obtain a list of resource groups in your subscription by using the `Get-AzureRmResourceGroup` cmdlet.</span></span>
2. <span data-ttu-id="431ac-152">Utwórz nowy magazyn usług odzyskiwania Azure w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="431ac-152">Create a new Azure Recovery Services vault as follows:</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    <span data-ttu-id="431ac-153">Można pobrać listy istniejących magazynów za pomocą `Get-AzureRmRecoveryServicesVault` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="431ac-153">You can retrieve a list of existing vaults by using the `Get-AzureRmRecoveryServicesVault` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="431ac-154">Jeśli chcesz wykonywać operacje na magazynów usługi Site Recovery utworzony przy użyciu klasycznego portalu lub moduł programu PowerShell do zarządzania usługi Azure, można pobrać listę takich magazynów za pomocą `Get-AzureRmSiteRecoveryVault` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="431ac-154">If you wish to perform operations on Site Recovery vaults created using the classic portal or the Azure Service Management PowerShell module, you can retrieve a list of such vaults by using the `Get-AzureRmSiteRecoveryVault` cmdlet.</span></span> <span data-ttu-id="431ac-155">Należy utworzyć nowy magazyn usług odzyskiwania dla wszystkich nowych operacji.</span><span class="sxs-lookup"><span data-stu-id="431ac-155">You should create a new Recovery Services vault for all new operations.</span></span> <span data-ttu-id="431ac-156">Magazynów usługi Site Recovery, utworzony wcześniej są obsługiwane, ale nie ma najnowszych funkcji.</span><span class="sxs-lookup"><span data-stu-id="431ac-156">The Site Recovery vaults you've created earlier are supported, but don't have the latest features.</span></span>
>
>

## <a name="step-3-set-the-recovery-services-vault-context"></a><span data-ttu-id="431ac-157">Krok 3: Ustaw kontekst magazynu usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="431ac-157">Step 3: Set the Recovery Services vault context</span></span>
1. <span data-ttu-id="431ac-158">Ustaw kontekst magazynu, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="431ac-158">Set the vault context by running the following command:</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-the-site"></a><span data-ttu-id="431ac-159">Krok 4: Tworzenie lokacji funkcji Hyper-V i wygenerowanie nowego klucza rejestracji magazynu dla tej lokacji.</span><span class="sxs-lookup"><span data-stu-id="431ac-159">Step 4: Create a Hyper-V site and generate a new vault registration key for the site.</span></span>
1. <span data-ttu-id="431ac-160">Utwórz nową witrynę funkcji Hyper-V w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="431ac-160">Create a new Hyper-V site as follows:</span></span>

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    <span data-ttu-id="431ac-161">To polecenie cmdlet uruchomi zadanie odzyskiwania lokacji, aby utworzyć lokację i zwraca obiekt zadania usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="431ac-161">This cmdlet starts a Site Recovery job to create the site, and returns a Site Recovery job object.</span></span> <span data-ttu-id="431ac-162">Poczekaj na zakończenie i sprawdź, czy zadania zadanie zostało ukończone pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="431ac-162">Wait for the job to complete and verify that the job completed successfully.</span></span>

    <span data-ttu-id="431ac-163">Można pobrać obiektu zadania, a tym samym sprawdzić bieżący stan zadania, za pomocą polecenia cmdlet Get-AzureRmSiteRecoveryJob.</span><span class="sxs-lookup"><span data-stu-id="431ac-163">You can retrieve the job object, and thereby check the current status of the job, by using the Get-AzureRmSiteRecoveryJob cmdlet.</span></span>
2. <span data-ttu-id="431ac-164">Generowanie i Pobierz klucz rejestracji dla lokacji, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="431ac-164">Generate and download a registration key for the site, as follows:</span></span>

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    <span data-ttu-id="431ac-165">Skopiuj pobrany klucz do hosta funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="431ac-165">Copy the downloaded key to the Hyper-V host.</span></span> <span data-ttu-id="431ac-166">Należy klawisz, aby zarejestrować hosta funkcji Hyper-V do lokacji.</span><span class="sxs-lookup"><span data-stu-id="431ac-166">You need the key to register the Hyper-V host to the site.</span></span>

## <a name="step-5-install-the-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a><span data-ttu-id="431ac-167">Krok 5: Instalowanie dostawcy usługi Azure Site Recovery i Agent usług odzyskiwania Azure na hoście funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="431ac-167">Step 5: Install the Azure Site Recovery provider and Azure Recovery Services Agent on your Hyper-V host</span></span>
1. <span data-ttu-id="431ac-168">Pobierz Instalatora, aby uzyskać najnowszą wersję dostawcy z [Microsoft](https://aka.ms/downloaddra).</span><span class="sxs-lookup"><span data-stu-id="431ac-168">Download the installer for the latest version of the provider from [Microsoft](https://aka.ms/downloaddra).</span></span>
2. <span data-ttu-id="431ac-169">Uruchom Instalator na hoście funkcji Hyper-V, a na końcu instalacji przejdź do kroku rejestracji.</span><span class="sxs-lookup"><span data-stu-id="431ac-169">Run the installer on your Hyper-V host, and at the end of the installation continue to the registration step.</span></span>
3. <span data-ttu-id="431ac-170">Po wyświetleniu monitu podaj klucza rejestracji pobranego lokacji i zakończyć rejestrację hosta funkcji Hyper-V do lokacji.</span><span class="sxs-lookup"><span data-stu-id="431ac-170">When prompted, provide the downloaded site registration key, and complete registration of the Hyper-V host to the site.</span></span>
4. <span data-ttu-id="431ac-171">Sprawdź, czy host funkcji Hyper-V jest zarejestrowana do witryny za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="431ac-171">Verify that the Hyper-V host is registered to the site by using the following command:</span></span>

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-the-protection-container"></a><span data-ttu-id="431ac-172">Krok 6: Tworzenie zasad replikacji i powiązać ją z kontenera ochrony</span><span class="sxs-lookup"><span data-stu-id="431ac-172">Step 6: Create a replication policy and associate it with the protection container</span></span>
1. <span data-ttu-id="431ac-173">Utwórz zasady replikacji w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="431ac-173">Create a replication policy as follows:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify the number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    <span data-ttu-id="431ac-174">Sprawdź zadanie zwrócone, aby upewnić się, że tworzenie zasad replikacji powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="431ac-174">Check the returned job to ensure that the replication policy creation succeeds.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="431ac-175">Określone konto magazynu musi należeć do tego samego regionu Azure co magazyn usług odzyskiwania i ma włączoną replikację geograficzną.</span><span class="sxs-lookup"><span data-stu-id="431ac-175">The storage account specified should be in the same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="431ac-176">Jeśli określone konto magazynu odzyskiwania jest typu usługi Azure Storage (klasyczny), trybu failover chronionych maszyn odzyskać maszyny do IaaS platformy Azure (klasyczne).</span><span class="sxs-lookup"><span data-stu-id="431ac-176">If the specified Recovery storage account is of type Azure Storage (Classic), failover of the protected machines recover the machine to Azure IaaS (Classic).</span></span>
   > * <span data-ttu-id="431ac-177">Jeśli określone konto magazynu odzyskiwania jest typu magazynu Azure (Azure Resource Manager), trybu failover chronionych maszyn odzyskać maszyny do IaaS platformy Azure (Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="431ac-177">If the specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of the protected machines recover the machine to Azure IaaS (Azure Resource Manager).</span></span>
   >
   >
2. <span data-ttu-id="431ac-178">Pobierz kontener ochrony odpowiadający danej lokacji, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="431ac-178">Get the protection container corresponding to the site, as follows:</span></span>

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. <span data-ttu-id="431ac-179">Uruchom skojarzenie kontenera ochrony z zasadami replikacji w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="431ac-179">Start the association of the protection container with the replication policy, as follows:</span></span>

     <span data-ttu-id="431ac-180">$Policy = get-AzureRmSiteRecoveryPolicy - FriendlyName $PolicyName $associationJob = Start AzureRmSiteRecoveryPolicyAssociationJob-$Policy zasad - PrimaryProtectionContainer $protectionContainer</span><span class="sxs-lookup"><span data-stu-id="431ac-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span></span>

   <span data-ttu-id="431ac-181">Poczekaj na ukończenie zadania skojarzenie i upewnij się, czy zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="431ac-181">Wait for the association job to complete, and ensure that it completed successfully.</span></span>

## <a name="step-7-enable-protection-for-virtual-machines"></a><span data-ttu-id="431ac-182">Krok 7: Włączanie ochrony dla maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="431ac-182">Step 7: Enable protection for virtual machines</span></span>
1. <span data-ttu-id="431ac-183">Pobierz jednostki ochrony odpowiadający maszyny Wirtualnej, który chcesz chronić w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="431ac-183">Get the protection entity corresponding to the VM you want to protect, as follows:</span></span>

        $VMFriendlyName = "Fabrikam-app"                    #Name of the VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. <span data-ttu-id="431ac-184">Rozpocznij ochronę maszyny wirtualnej, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="431ac-184">Start protecting the virtual machine, as follows:</span></span>

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > <span data-ttu-id="431ac-185">Określone konto magazynu musi należeć do tego samego regionu Azure co magazyn usług odzyskiwania i ma włączoną replikację geograficzną.</span><span class="sxs-lookup"><span data-stu-id="431ac-185">The storage account specified should be in the same Azure region as your Recovery Services vault, and should have geo-replication enabled.</span></span>
   >
   > * <span data-ttu-id="431ac-186">Jeśli określone konto magazynu odzyskiwania jest typu usługi Azure Storage (klasyczny), trybu failover chronionych maszyn odzyskać maszyny do IaaS platformy Azure (klasyczne).</span><span class="sxs-lookup"><span data-stu-id="431ac-186">If the specified Recovery storage account is of type Azure Storage (Classic), failover of the protected machines recover the machine to Azure IaaS (Classic).</span></span>
   > * <span data-ttu-id="431ac-187">Jeśli określone konto magazynu odzyskiwania jest typu magazynu Azure (Azure Resource Manager), trybu failover chronionych maszyn odzyskać maszyny do IaaS platformy Azure (Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="431ac-187">If the specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of the protected machines recover the machine to Azure IaaS (Azure Resource Manager).</span></span>
   >
   > <span data-ttu-id="431ac-188">Jeśli chronisz maszyny Wirtualnej ma więcej niż jeden dysk dołączony do niej, określ dysk systemu operacyjnego za pomocą *OSDiskName* parametru.</span><span class="sxs-lookup"><span data-stu-id="431ac-188">If the VM you are protecting has more than one disk attached to it, specify the operating system disk by using the *OSDiskName* parameter.</span></span>
   >
   >
3. <span data-ttu-id="431ac-189">Poczekaj, aż do przejścia chronionych po replikacji początkowej maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="431ac-189">Wait for the virtual machines to reach a protected state after the initial replication.</span></span> <span data-ttu-id="431ac-190">Może to potrwać kilka minut, w zależności od czynników, takich jak ilość danych, które powinny być replikowane i dostępnej przepustowości nadrzędnego na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="431ac-190">This can take a while, depending on factors such as the amount of data to be replicated and the available upstream bandwidth to Azure.</span></span> <span data-ttu-id="431ac-191">Stan zadania i StateDescription są aktualizowane, po osiągnięciu chronionych stan maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="431ac-191">The job State and StateDescription are updated as follows, upon the VM reaching a protected state.</span></span>

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. <span data-ttu-id="431ac-192">Zaktualizuj właściwości odzyskiwania, na przykład rozmiaru roli maszyny Wirtualnej i sieci platformy Azure można dołączyć maszyny wirtualnej kart interfejsu sieciowego do podczas pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="431ac-192">Update recovery properties, such as the VM role size, and the Azure network to attach the virtual machine's network interface cards to upon failover.</span></span>

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
        DisplayName      : Update the virtual machine
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



## <a name="step-8-run-a-test-failover"></a><span data-ttu-id="431ac-193">Krok 8: Uruchom test trybu failover</span><span class="sxs-lookup"><span data-stu-id="431ac-193">Step 8: Run a test failover</span></span>
1. <span data-ttu-id="431ac-194">Uruchom zadania testowego trybu failover, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="431ac-194">Run a test failover job, as follows:</span></span>

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. <span data-ttu-id="431ac-195">Sprawdź, czy test zostanie utworzona maszyna wirtualna na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="431ac-195">Verify that the test VM is created in Azure.</span></span> <span data-ttu-id="431ac-196">(Test trybu failover zadanie zostanie zawieszone, po utworzeniu testowej maszyny Wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="431ac-196">(The test failover job is suspended, after creating the test VM in Azure.</span></span> <span data-ttu-id="431ac-197">Zadanie zostało ukończone przez czyszczenie utworzony artefaktów po wznowieniu zadania, jak pokazano w następnym kroku.)</span><span class="sxs-lookup"><span data-stu-id="431ac-197">The job completes by cleaning up the created artefacts upon resuming the job, as illustrated in the next step.)</span></span>
3. <span data-ttu-id="431ac-198">Testowy tryb failover, należy wykonać w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="431ac-198">Complete the test failover, as follows:</span></span>

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a><span data-ttu-id="431ac-199">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="431ac-199">Next Steps</span></span>
<span data-ttu-id="431ac-200">[Dowiedz się więcej](https://msdn.microsoft.com/library/azure/mt637930.aspx) dotyczące usługi Azure Site Recovery za pomocą poleceń cmdlet programu PowerShell usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="431ac-200">[Read more](https://msdn.microsoft.com/library/azure/mt637930.aspx) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
