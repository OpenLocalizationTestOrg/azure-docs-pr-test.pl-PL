---
title: "Magazyn usług odzyskiwania Azure tooan aaaUpgrade magazynu usługi Site Recovery"
description: "Dowiedz się, jak tooupgrade magazynie usługi Azure Site Recovery tooa magazyn usług odzyskiwania"
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/31/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: a18a923ee3bad91873e654c9b9b5bf8b83acc123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-site-recovery-vault-tooan-azure-resource-manager-based-recovery-services-vault"></a><span data-ttu-id="8cf4f-103">Uaktualnij magazynu usług odzyskiwania Azure Resource Manager tooan magazynu usługi Site Recovery</span><span class="sxs-lookup"><span data-stu-id="8cf4f-103">Upgrade a Site Recovery vault tooan Azure Resource Manager-based Recovery Services vault</span></span>

<span data-ttu-id="8cf4f-104">W tym artykule opisano, jak tooupgrade usługi Azure Site Recovery magazyny Magazyny usług odzyskiwania Resource Manager tooAzure bez wpływu na trwającej replikacji.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-104">This article describes how tooupgrade Azure Site Recovery vaults tooAzure Resource Manager-based Recovery Service vaults without any impact on ongoing replication.</span></span> <span data-ttu-id="8cf4f-105">Aby uzyskać więcej informacji na temat usługi Azure Resource Manager funkcje i korzyści, zobacz [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8cf4f-105">For more information about Azure Resource Manager features and benefits, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="8cf4f-106">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="8cf4f-106">Introduction</span></span>
<span data-ttu-id="8cf4f-107">Magazyn usług odzyskiwania jest zasobem usługi Azure Resource Manager do zarządzania kopii zapasowej i odzyskiwanie po awarii w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-107">A Recovery Services vault is an Azure Resource Manager resource for managing backup and disaster recovery natively in hello cloud.</span></span> <span data-ttu-id="8cf4f-108">Jest ujednoliconego magazyn, którego można użyć w hello nowego portalu Azure, i zastępuje hello zapasową magazynów usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-108">It is a unified vault that you can use in hello new Azure portal, and it replaces hello classic backup and Site Recovery vaults.</span></span>

<span data-ttu-id="8cf4f-109">Magazyny usług odzyskiwania oferują tablicę funkcje, takie jak:</span><span class="sxs-lookup"><span data-stu-id="8cf4f-109">Recovery Services vaults offer an array of features, including:</span></span>

* <span data-ttu-id="8cf4f-110">Pomoc techniczna platformy Azure Resource Manager: można chronić i pracy awaryjnej z maszyn wirtualnych i maszyn fizycznych do stosu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-110">Azure Resource Manager support: You can protect and fail over your virtual machines and physical machines into an Azure Resource Manager stack.</span></span>

* <span data-ttu-id="8cf4f-111">Wykluczanie dysku: Jeśli masz pliki tymczasowe lub wiele zmian danych, że nie chcesz toouse Twojego przepustowości dla woluminów można wykluczyć z replikacji.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-111">Exclude disk: If you have temp files or high churn data that you don’t want toouse all your bandwidth for, you can exclude volumes from replication.</span></span> <span data-ttu-id="8cf4f-112">Ta funkcja została włączona w obecnie *VMware tooAzure* i *tooAzure funkcji Hyper-V* i rozszerzeniu również tooother scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-112">This capability has been enabled currently in *VMware tooAzure* and *Hyper-V tooAzure* and is extended tooother scenarios as well.</span></span>

* <span data-ttu-id="8cf4f-113">Obsługa premium i Magazyn lokalnie nadmiarowy: mogą teraz chronić serwery w magazynie premium konta, które umożliwiają klientom wyższy tooprotect aplikacji za pomocą operacji wejścia/wyjścia na sekundę (IOPS).</span><span class="sxs-lookup"><span data-stu-id="8cf4f-113">Support for premium and locally redundant storage: You can now protect servers in premium storage accounts that allow customers tooprotect applications with higher input/output operations per second (IOPS).</span></span> <span data-ttu-id="8cf4f-114">Ta funkcja jest obecnie włączona w *VMware tooAzure*.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-114">This capability is currently enabled in *VMware tooAzure*.</span></span>

* <span data-ttu-id="8cf4f-115">Uproszczone środowisko — wprowadzenie: hello rozszerzone — wprowadzenie środowisko zostało zaprojektowane Instalator odzyskiwania po awarii toomake łatwe.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-115">Streamlined getting-started experience: hello enhanced getting-started experience has been designed toomake disaster-recovery setup easy.</span></span>

* <span data-ttu-id="8cf4f-116">Kopii zapasowych i odzyskiwania lokacji zarządzania z tym samym magazynie hello: można teraz chronić serwerów na potrzeby odzyskiwania po awarii lub wykonaj kopię zapasową z hello tego samego magazynu, co może zmniejszyć nakłady znacznie z zarządzania.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-116">Backup and Site Recovery management from hello same vault: You can now protect servers for disaster recovery or perform backup from hello same vault, which can reduce your management overhead significantly.</span></span>

<span data-ttu-id="8cf4f-117">Aby uzyskać więcej informacji na temat funkcji i doświadczeń uaktualniony hello Zobacz hello [blogu magazynu kopii zapasowej i odzyskiwania](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span><span class="sxs-lookup"><span data-stu-id="8cf4f-117">For more information about hello upgraded experience and features, see hello [Storage, Backup, and Recovery blog](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span></span>

## <a name="salient-features"></a><span data-ttu-id="8cf4f-118">Najważniejsze funkcje</span><span class="sxs-lookup"><span data-stu-id="8cf4f-118">Salient features</span></span>

* <span data-ttu-id="8cf4f-119">Bez wpływu na trwająca replikacja: trwającej replikacji kontynuować bez przerwy podczas i po uaktualnieniu.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-119">No impact on ongoing replication: Ongoing replications continue without any interruption during and post upgrade.</span></span>

* <span data-ttu-id="8cf4f-120">Bez dodatkowych kosztów: Pobierz całego zestawu funkcji zaktualizowane bez ponoszenia dodatkowych kosztów.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-120">No additional cost: Get an entire set of updated capabilities at no additional cost.</span></span>

* <span data-ttu-id="8cf4f-121">Brak utraty danych: ponieważ ten proces jest uaktualnienie i nie migracji, istniejących punktów odzyskiwania replikacji i ustawienia pozostaną nienaruszone podczas i po uaktualnieniu hello.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-121">No data loss: Because this process is an upgrade and not a migration, existing replication recovery points and settings remain intact during and after hello upgrade.</span></span>


## <a name="what-happens-during-hello-vault-upgrade"></a><span data-ttu-id="8cf4f-122">Co się dzieje podczas uaktualniania magazynu hello?</span><span class="sxs-lookup"><span data-stu-id="8cf4f-122">What happens during hello vault upgrade?</span></span>

<span data-ttu-id="8cf4f-123">Podczas uaktualniania hello nie można wykonać operacji, takich jak rejestrowanie nowego serwera oraz włączania replikacji dla maszyny wirtualnej (VM).</span><span class="sxs-lookup"><span data-stu-id="8cf4f-123">During hello upgrade, you cannot perform operations such as registering a new server or enabling replication for a virtual machine (VM).</span></span> <span data-ttu-id="8cf4f-124">Operacje, które wymagają Odczyt danych z lub zapisywania w magazynie toohello danych, takich jak trwającej replikacji magazynu toohello chronione elementy, nadal przerwana.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-124">Operations that involve reading data from or writing data toohello vault, such as ongoing replication of protected items toohello vault, continue uninterrupted.</span></span>

### <a name="changes-tooautomation-and-tooling-after-hello-upgrade"></a><span data-ttu-id="8cf4f-125">Zmienia tooautomation i narzędzi po uaktualnieniu hello</span><span class="sxs-lookup"><span data-stu-id="8cf4f-125">Changes tooautomation and tooling after hello upgrade</span></span>
<span data-ttu-id="8cf4f-126">Po uaktualnieniu hello magazynu typ z modelu wdrażania usługi Resource Manager toohello hello wdrażania klasycznego modelu aktualizacji istniejącej automatyzacji hello lub nadal toowork, po uaktualnieniu hello tooensure narzędzi.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-126">As you upgrade hello vault type from hello classic deployment model toohello Resource Manager deployment model, update hello existing automation or tooling tooensure that it continues toowork after hello upgrade.</span></span>

### <a name="prepare-your-environment-for-hello-upgrade"></a><span data-ttu-id="8cf4f-127">Przygotowywanie środowiska dla uaktualnienia hello</span><span class="sxs-lookup"><span data-stu-id="8cf4f-127">Prepare your environment for hello upgrade</span></span>

* [<span data-ttu-id="8cf4f-128">Instalowanie programu PowerShell lub ją uaktualnić tooversion 5 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="8cf4f-128">Install PowerShell or upgrade it tooversion 5 or later</span></span>](https://www.microsoft.com/download/details.aspx?id=50395)
* [<span data-ttu-id="8cf4f-129">Zainstaluj najnowszą wersję hello Azure PowerShell msi</span><span class="sxs-lookup"><span data-stu-id="8cf4f-129">Install hello latest version of Azure PowerShell MSI</span></span>](https://github.com/Azure/azure-powershell/releases)
* [<span data-ttu-id="8cf4f-130">Pobierz hello skryptów uaktualniania magazynu usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="8cf4f-130">Download hello Recovery Services vault upgrade script</span></span>](https://aka.ms/vaultupgradescript)

### <a name="prerequisites"></a><span data-ttu-id="8cf4f-131">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8cf4f-131">Prerequisites</span></span>
<span data-ttu-id="8cf4f-132">Magazyny usług odzyskiwania Resource Manager tooAzure magazyny tooupgrade z usługi Site Recovery, musi spełniać następujące wymagania hello:</span><span class="sxs-lookup"><span data-stu-id="8cf4f-132">tooupgrade from Site Recovery vaults tooAzure Resource Manager-based Recovery Service vaults, you must meet hello following requirements:</span></span>

* <span data-ttu-id="8cf4f-133">Wersja minimalna agenta: hello Azure dostawcy usługi Site Recovery na serwerze musi być 5.1.1700.0 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-133">Minimum agent version: hello version of Azure Site Recovery Provider installed on your server must be 5.1.1700.0 or later.</span></span>

* <span data-ttu-id="8cf4f-134">Obsługiwana konfiguracja: nie można skonfigurować Magazyn sieci magazynowania (SAN) lub grup dostępności AlwaysOn programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-134">Supported configuration: You cannot configure your vault with storage area network (SAN) or SQL Server AlwaysOn Availability Groups.</span></span> <span data-ttu-id="8cf4f-135">Inne konfiguracje są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-135">All other configurations are supported.</span></span>

    >[!NOTE]
    ><span data-ttu-id="8cf4f-136">Po uaktualnieniu hello można zarządzać mapowania przechowywania tylko przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-136">After hello upgrade, you can manage storage mapping only via PowerShell.</span></span>

* <span data-ttu-id="8cf4f-137">Scenariusz wdrażania obsługiwanych: Magazyn nie powinien być hello *VMware tooAzure* modelu wdrażania starszej wersji.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-137">Supported deployment scenario: Your vault shouldn’t be hello *VMware tooAzure* legacy deployment model.</span></span> <span data-ttu-id="8cf4f-138">Aby kontynuować, należy najpierw przenieść toohello wdrożenia rozszerzonego modelu.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-138">Before you proceed, first move toohello enhanced deployment model.</span></span>

* <span data-ttu-id="8cf4f-139">Operacje płaszczyzny żadnych aktywnych działań zainicjowane przez użytkownika, które obejmują zarządzanie: ponieważ płaszczyzny zarządzania toohello dostęp jest ograniczony podczas uaktualniania, wykonanie wszystkich akcji płaszczyzny zarządzania przed wyzwoleniem hello uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-139">No active user-initiated jobs that involve management plane operations: Because access toohello management plane is restricted during upgrade, complete all your management plane actions before you trigger hello upgrade.</span></span> <span data-ttu-id="8cf4f-140">Ten proces nie zawiera trwającej replikacji.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-140">This process doesn’t include ongoing replication.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="8cf4f-141">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="8cf4f-141">Frequently asked questions</span></span>

<span data-ttu-id="8cf4f-142">**To uaktualnienie wpływa na mój trwającej replikacji?**</span><span class="sxs-lookup"><span data-stu-id="8cf4f-142">**Does this upgrade affect my ongoing replication?**</span></span>

<span data-ttu-id="8cf4f-143">Nie.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-143">No.</span></span> <span data-ttu-id="8cf4f-144">Twoje bieżące replikacja jest kontynuowana przerwana podczas i po uaktualnieniu hello.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-144">Your ongoing replication continues uninterrupted during and after hello upgrade.</span></span>

<span data-ttu-id="8cf4f-145">**Co się stanie toonetwork ustawienia, takie jak ustawienia IP i sieci VPN typu lokacja lokacja?**</span><span class="sxs-lookup"><span data-stu-id="8cf4f-145">**What happens toonetwork settings such as site-to-site VPN and IP settings?**</span></span>

<span data-ttu-id="8cf4f-146">uaktualnienie Hello nie wpływa na powitania ustawienia sieciowe.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-146">hello upgrade doesn't affect hello network settings.</span></span> <span data-ttu-id="8cf4f-147">Wszystkie połączenia Azure do lokalne pozostaną nienaruszone.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-147">All Azure-to-on-premises connections remain intact.</span></span>

<span data-ttu-id="8cf4f-148">**Co w przypadku magazynów toomy nie należy zaplanować tooupgrade w hello niemal przyszłości?**</span><span class="sxs-lookup"><span data-stu-id="8cf4f-148">**What happens toomy vaults if I don’t plan tooupgrade in hello near future?**</span></span>

<span data-ttu-id="8cf4f-149">Obsługa magazynu usługi Site Recovery w portalu Azure starego hello zostaną wycofane uruchamianie września 2017 r.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-149">Support for Site Recovery vault in hello old Azure portal will be deprecated starting September 2017.</span></span> <span data-ttu-id="8cf4f-150">Zdecydowanie zaleca się użycie hello funkcja uaktualnienia toomove toohello nowego portalu.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-150">We strongly recommend that you use hello upgrade feature toomove toohello new portal.</span></span>

<span data-ttu-id="8cf4f-151">**Co oznacza ten plan migracji dla moich istniejących narzędzi?**</span><span class="sxs-lookup"><span data-stu-id="8cf4f-151">**What does this migration plan mean for my existing tooling?**</span></span>  

<span data-ttu-id="8cf4f-152">Aktualizowanie modelu wdrażania usługi Resource Manager toohello narzędzi jest jednym z hello najważniejszych zmian, które należy uwzględnić w planów uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-152">Updating your tooling toohello Resource Manager deployment model is one of hello most important changes that you must account for in your upgrade plans.</span></span> <span data-ttu-id="8cf4f-153">Magazyny usług odzyskiwania Hello są oparte na modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-153">hello Recovery Services vaults are based on hello Resource Manager deployment model.</span></span> 

<span data-ttu-id="8cf4f-154">**Jak długo hello przestoju płaszczyzny zarządzania ostatnio?**</span><span class="sxs-lookup"><span data-stu-id="8cf4f-154">**How long does hello management-plane downtime last?**</span></span>

<span data-ttu-id="8cf4f-155">uaktualnienie Hello zwykle trwa około 15 minut too30 i może potrwać tooa maksymalnie jedną godzinę.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-155">hello upgrade ordinarily takes about 15 too30 minutes, and it could take up tooa maximum of one hour.</span></span>

<span data-ttu-id="8cf4f-156">**I przywrócić po uaktualnieniu?**</span><span class="sxs-lookup"><span data-stu-id="8cf4f-156">**Can I roll back after upgrading?**</span></span>

<span data-ttu-id="8cf4f-157">Nie.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-157">No.</span></span> <span data-ttu-id="8cf4f-158">Wycofanie nie jest obsługiwana po hello zasoby zostały pomyślnie uaktualnione.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-158">Rollback is not supported after hello resources have been successfully upgraded.</span></span>

<span data-ttu-id="8cf4f-159">**Można sprawdzania poprawności mojej subskrypcji lub toosee zasobów czy można uaktualnić?**</span><span class="sxs-lookup"><span data-stu-id="8cf4f-159">**Can I validate my subscription or resources toosee whether they can be upgraded?**</span></span>

<span data-ttu-id="8cf4f-160">Tak.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-160">Yes.</span></span> <span data-ttu-id="8cf4f-161">W hello obsługiwane platformy opcję uaktualniania hello pierwszym krokiem podczas uaktualnienia hello jest toovalidate czy hello zasoby są w stanie uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-161">In hello platform-supported upgrade option, hello first step in hello upgrade is toovalidate that hello resources are capable of an upgrade.</span></span> <span data-ttu-id="8cf4f-162">W przypadku niepowodzenia weryfikacji hello otrzymasz odpowiednie komunikaty o błędach i ostrzeżenia.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-162">If hello validation fails, you will receive appropriate error messages or warnings.</span></span>

<span data-ttu-id="8cf4f-163">**Jak zgłosić problem związany z uaktualnieniem hello?**</span><span class="sxs-lookup"><span data-stu-id="8cf4f-163">**How do I report an issue with hello upgrade?**</span></span>

<span data-ttu-id="8cf4f-164">Jeśli wystąpią zakończą się niepowodzeniem podczas uaktualniania hello, należy pamiętać, identyfikator operacji hello wyświetlanej na liście błędów hello.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-164">If you experience any failures during hello upgrade, note hello operation ID that's listed in hello error.</span></span> <span data-ttu-id="8cf4f-165">Microsoft Support aktywnego będą działać na rozwiązanie problemu hello.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-165">Microsoft Support will proactively work on resolving hello issue.</span></span> <span data-ttu-id="8cf4f-166">Może także kontaktować z zespołem pomocy technicznej hello z Identyfikatorem subskrypcji, nazwę magazynu, a identyfikator operacji.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-166">You can also contact hello Support team with your subscription ID, vault name, and operation ID.</span></span> <span data-ttu-id="8cf4f-167">Obsługa będzie działać możliwie jak najszybciej tooresolve hello problem.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-167">Support will work tooresolve hello issue as quickly as possible.</span></span> <span data-ttu-id="8cf4f-168">Nie próbuj ponownie operację hello o ile nie zostaną jawnie instrukcją toodo tak przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-168">Do not retry hello operation unless you are explicitly instructed toodo so by Microsoft.</span></span>

## <a name="run-hello-script"></a><span data-ttu-id="8cf4f-169">Uruchom skrypt hello</span><span class="sxs-lookup"><span data-stu-id="8cf4f-169">Run hello script</span></span>

<span data-ttu-id="8cf4f-170">W programie PowerShell uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="8cf4f-170">In PowerShell, run hello following command:</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionID <subscriptionID>  -VaultName <vaultname> -Location <location> -ResourceType HyperVRecoveryManagerVault -TargetResourceGroupName <rgname>

* <span data-ttu-id="8cf4f-171">Identyfikator subskrypcji: hello identyfikator subskrypcji, który został skojarzony z magazynem hello, że w przypadku uaktualniania.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-171">SubscriptionID: hello subscription ID that's associated with hello vault that you're upgrading.</span></span>

* <span data-ttu-id="8cf4f-172">VaultName: Nazwa hello hello magazynu, który w przypadku uaktualniania.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-172">VaultName: hello name of hello vault that you're upgrading.</span></span>

* <span data-ttu-id="8cf4f-173">Lokalizacja: hello lokalizacja magazynu hello, że w przypadku uaktualniania.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-173">Location: hello location of hello vault that you're upgrading.</span></span>

* <span data-ttu-id="8cf4f-174">Typ zasobu: Magazyny HyperVRecoveryManagerVault Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-174">ResourceType: HyperVRecoveryManagerVault for Site Recovery vaults.</span></span>

* <span data-ttu-id="8cf4f-175">TargetResourceGroupName: hello grupy zasobów, do której ma zostać hello uaktualnione umieszczone toobe magazynu.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-175">TargetResourceGroupName: hello resource group into which you want hello upgraded vault toobe placed.</span></span> <span data-ttu-id="8cf4f-176">TargetResourceGroupName może być istniejącej grupy zasobów w usłudze Azure Resource Manager lub nowy.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-176">TargetResourceGroupName can be an existing resource group in Azure Resource Manager or a new one.</span></span> <span data-ttu-id="8cf4f-177">Jeśli hello TargetResourceGroupName, która jest dostarczana nie istnieje, go jest tworzony w ramach uaktualnienia hello w hello sam lokalizacji co magazyn hello.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-177">If hello TargetResourceGroupName that's supplied does not exist, it is created as part of hello upgrade in hello same location as hello vault.</span></span> <span data-ttu-id="8cf4f-178">Aby uzyskać więcej informacji, zobacz sekcję "Grupy zasobów" hello [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="8cf4f-178">For more information, see hello "Resource groups" section of [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

    >[!NOTE]
    ><span data-ttu-id="8cf4f-179">Nazwy grupy zasobów jest ograniczenia toocertain podmiotu.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-179">Resource group naming is subject toocertain constraints.</span></span> <span data-ttu-id="8cf4f-180">Magazyn tooprevent uaktualnić awarii, należy starannie czy hello tooobserve konwencji nazewnictwa.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-180">tooprevent vault upgrade failure, be sure tooobserve hello naming convention carefully.</span></span>
    >
    ><span data-ttu-id="8cf4f-181">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="8cf4f-181">For example:</span></span>
    >
    ><span data-ttu-id="8cf4f-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 SubscriptionId - 1234-54123-354354-56416-8645 - VaultName gen2dr — lokalizacja "Europa Północna" hypervrecoverymanagervault - ResourceType - TargetResourceGroupName abc</span><span class="sxs-lookup"><span data-stu-id="8cf4f-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span></span>

<span data-ttu-id="8cf4f-183">Alternatywnie możesz uruchomić hello następującego skryptu.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-183">Alternatively, you can run hello following script.</span></span> <span data-ttu-id="8cf4f-184">Wprowadź wartości hello hello wymaganych parametrów.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-184">Enter hello values for hello required parameters.</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1
    cmdlet RecoveryServicesVaultUpgrade-1.0.0.ps1 at command pipeline position 1

    Supply values for hello following parameters:
    SubscriptionId:
    VaultName:
    Location:
    ResourceType:
    TargetResourceGroupName:

1. <span data-ttu-id="8cf4f-185">Hello skrypt programu PowerShell wyświetli monit możesz tooenter swoje poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-185">hello PowerShell script prompts you tooenter your credentials.</span></span> <span data-ttu-id="8cf4f-186">Wprowadź je dwukrotnie raz hello wdrażania klasycznego modelu oraz raz hello konta usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-186">Enter them twice, once for hello classic deployment model account and once for hello Azure Resource Manager account.</span></span>

2. <span data-ttu-id="8cf4f-187">Po wprowadzeniu poświadczeń hello skrypt jest uruchamiany toodetermine Sprawdź, czy Twoje hello spełnia instalacji infrastruktury powyżej wymagań.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-187">After you've entered your credentials, hello script runs a check toodetermine whether your infrastructure setup meets hello previously mentioned requirements.</span></span>

3. <span data-ttu-id="8cf4f-188">Po hello wymagania wstępne zostały sprawdzone i potwierdzone, jest monitem tooproceed hello uaktualniania magazynu.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-188">After hello prerequisites have been checked and confirmed, you are prompted tooproceed with hello vault upgrade.</span></span> <span data-ttu-id="8cf4f-189">rozpocznie się proces uaktualniania Hello uaktualniania magazynu.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-189">hello upgrade process starts upgrading your vault.</span></span> <span data-ttu-id="8cf4f-190">Hello całego uaktualnienia może zająć 15 toocomplete minut too30.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-190">hello entire upgrade can take 15 too30 minutes toocomplete.</span></span>

4. <span data-ttu-id="8cf4f-191">Po uaktualnieniu hello pomyślnie, można uzyskać dostępu do hello uaktualnionego magazynu w hello nowego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-191">After hello upgrade has been completed successfully, you can access hello upgraded vault in hello new Azure portal.</span></span>

## <a name="post-upgrade-vault-management"></a><span data-ttu-id="8cf4f-192">Zarządzanie magazynem po uaktualnieniu</span><span class="sxs-lookup"><span data-stu-id="8cf4f-192">Post-upgrade vault management</span></span>

### <a name="replicate-by-using-azure-site-recovery-in-hello-recovery-services-vault"></a><span data-ttu-id="8cf4f-193">Replikacja za pomocą usługi Azure Site Recovery w hello magazyn usług odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="8cf4f-193">Replicate by using Azure Site Recovery in hello Recovery Services vault</span></span>

* <span data-ttu-id="8cf4f-194">Maszyny wirtualne Azure mogą teraz chronić z jednego regionu tooanother.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-194">You can now protect your Azure VMs from one region tooanother.</span></span> <span data-ttu-id="8cf4f-195">Aby uzyskać więcej informacji, zobacz [replikowanie maszyn wirtualnych platformy Azure między regionami z usługą Azure Site Recovery](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="8cf4f-195">For more information, see [Replicate Azure VMs between regions with Azure Site Recovery](site-recovery-azure-to-azure.md).</span></span>

* <span data-ttu-id="8cf4f-196">Aby uzyskać więcej informacji na temat replikowania maszyn wirtualnych VMware tooAzure, zobacz [tooAzure replikowanie maszyn wirtualnych VMware z usługą Site Recovery](vmware-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8cf4f-196">For more information about replicating VMware VMs tooAzure, see [Replicate VMware VMs tooAzure with Site Recovery](vmware-walkthrough-overview.md).</span></span>

* <span data-ttu-id="8cf4f-197">Aby uzyskać więcej informacji na temat replikowania maszyn wirtualnych funkcji Hyper-V (bez VMM) tooAzure, zobacz [tooAzure maszyn wirtualnych (bez VMM) replikacji funkcji Hyper-V](hyper-v-site-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8cf4f-197">For more information about replicating Hyper-V VMs (without VMM) tooAzure, see [Replicate Hyper-V virtual machines (without VMM) tooAzure](hyper-v-site-walkthrough-overview.md).</span></span>

* <span data-ttu-id="8cf4f-198">Aby uzyskać więcej informacji o replikacji tooAzure maszyn wirtualnych funkcji Hyper-V (w programie VMM), zobacz [maszyn wirtualnych funkcji Hyper-V replikacji w tooAzure chmur programu VMM przy użyciu usługi Site Recovery w hello portalu Azure](vmm-to-azure-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8cf4f-198">For more information about replicating Hyper-V VMs (with VMM) tooAzure, see [Replicate Hyper-V virtual machines in VMM clouds tooAzure using Site Recovery in hello Azure portal](vmm-to-azure-walkthrough-overview.md).</span></span>

* <span data-ttu-id="8cf4f-199">Aby uzyskać więcej informacji o replikacji lokacji dodatkowej tooa funkcji Hyper-VMs (w programie VMM), zobacz [replikacji funkcji Hyper-V maszyn wirtualnych VMM chmur tooa dodatkowej VMM lokacji przy użyciu hello portalu Azure](site-recovery-vmm-to-vmm.md).</span><span class="sxs-lookup"><span data-stu-id="8cf4f-199">For more information about replicating Hyper-VMs (with VMM) tooa secondary site, see [Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site using hello Azure portal](site-recovery-vmm-to-vmm.md).</span></span>

* <span data-ttu-id="8cf4f-200">Aby uzyskać więcej informacji o replikacji lokacji dodatkowej tooa maszyn wirtualnych VMware, zobacz [Replikowanie lokalnych maszyn wirtualnych VMware lub serwerów fizycznych tooa lokacji dodatkowej w klasycznym portalu Azure hello](site-recovery-vmware-to-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="8cf4f-200">For more information about replicating VMware VMs tooa secondary site, see [Replicate on-premises VMware virtual machines or physical servers tooa secondary site in hello classic Azure portal](site-recovery-vmware-to-vmware.md).</span></span>

### <a name="view-your-replicated-items"></a><span data-ttu-id="8cf4f-201">Wyświetl elementy replikowane</span><span class="sxs-lookup"><span data-stu-id="8cf4f-201">View your replicated items</span></span>

<span data-ttu-id="8cf4f-202">Witaj poniższy obraz przedstawia hello usług odzyskiwania magazynu pulpitu nawigacyjnego strona, wyświetlająca kluczy jednostek hello magazynu.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-202">hello following image shows hello Recovery Services vault dashboard page that displays key entities for hello vault.</span></span> <span data-ttu-id="8cf4f-203">Wybierz tooview listę chronionych jednostki w magazynie hello **usługi Site Recovery** > **elementy replikowane**.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-203">tooview a list of protected entities in hello vault, select **Site Recovery** > **Replicated items**.</span></span>


![Zreplikowanych elementów](./media/upgrade-site-recovery-vaults/replicateditems.png)

<span data-ttu-id="8cf4f-205">Witaj Poniższa ilustracja przedstawia przykładowy przepływ pracy hello wyświetlanie Twoich zreplikowanych elementów i hello **pracy awaryjnej** polecenia inicjowania pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-205">hello following image shows hello workflow for viewing your replicated items and hello **Failover** command for initiating a failover.</span></span>

![Zreplikowanych elementów](./media/upgrade-site-recovery-vaults/failover.png)

### <a name="view-your-replication-settings"></a><span data-ttu-id="8cf4f-207">Wyświetl ustawienia replikacji</span><span class="sxs-lookup"><span data-stu-id="8cf4f-207">View your replication settings</span></span>

<span data-ttu-id="8cf4f-208">W magazynie usługi Site Recovery hello każdej grupy ochrony jest konfigurowana częstotliwość kopiowania, przechowywania punktu odzyskiwania, częstotliwość migawek spójności aplikacji i innych ustawień replikacji.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-208">In hello Site Recovery vault, each protection group is configured with copy frequency, recovery point retention, frequency of application consistent snapshots, and other replication settings.</span></span> <span data-ttu-id="8cf4f-209">W magazynie usług odzyskiwania hello te ustawienia są skonfigurowane jako zasady replikacji.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-209">In hello Recovery Services vault, these settings are configured as a replication policy.</span></span> <span data-ttu-id="8cf4f-210">Nazwa Hello zasad hello jest hello hello grupy ochrony lub hello *primarycloud_Policy*.</span><span class="sxs-lookup"><span data-stu-id="8cf4f-210">hello name of hello policy is hello name of hello protection group or hello *primarycloud_Policy*.</span></span>

<span data-ttu-id="8cf4f-211">Aby uzyskać więcej informacji na temat zasad replikacji, zobacz [zarządzać zasadami replikacji VMware tooAzure](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="8cf4f-211">For more information about replication policy, see [Manage replication policy for VMware tooAzure](site-recovery-setup-replication-settings-vmware.md).</span></span>
