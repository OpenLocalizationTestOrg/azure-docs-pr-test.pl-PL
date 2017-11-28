---
title: "Replikowanie maszyn wirtualnych funkcji Hyper-V w chmurach VMM do platformy Azure z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera omówienie replikowania maszyn wirtualnych funkcji Hyper-V w chmurach programu VMM na platformie Azure przy użyciu usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: af68d21184c137b2b0f1bb4c1afb9bf507e8332d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-azure-using-site-recovery-in-the-azure-portal"></a><span data-ttu-id="0b673-103">Replikowanie maszyn wirtualnych funkcji Hyper-V w chmurach programu VMM do platformy Azure przy użyciu usługi Site Recovery w witrynie Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0b673-103">Replicate Hyper-V virtual machines in VMM clouds to Azure using Site Recovery in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0b673-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0b673-104">Azure portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="0b673-105">Klasyczny portal Azure</span><span class="sxs-lookup"><span data-stu-id="0b673-105">Azure classic</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="0b673-106">Program PowerShell — model usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0b673-106">PowerShell Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="0b673-107">PowerShell — model klasyczny</span><span class="sxs-lookup"><span data-stu-id="0b673-107">PowerShell classic</span></span>](site-recovery-deploy-with-powershell.md)


<span data-ttu-id="0b673-108">Ten artykuł zawiera omówienie kroków wymaganych do replikowania maszyn wirtualnych funkcji Hyper-V lokalnymi (VM) zarządzane w programie System Center Virtual Machine Manager (VMM) chmury Azure, przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md) w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0b673-108">This article provides an overview of the steps required to replicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="0b673-109">Po przeczytaniu tego artykułu zamieść wszelkie komentarze u dołu lub na [forum usług Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="0b673-109">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-the-scenario-architecture"></a><span data-ttu-id="0b673-110">Krok 1: Przejrzyj architektura scenariusza</span><span class="sxs-lookup"><span data-stu-id="0b673-110">Step 1: Review the scenario architecture</span></span>

<span data-ttu-id="0b673-111">Przed rozpoczęciem wdrażania, przejrzyj architektura scenariusza i upewnij się, że znasz wszystkie składniki potrzebne do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="0b673-111">Before you start deployment, review the scenario architecture, and make sure that you understand all the components you need to deploy.</span></span>

<span data-ttu-id="0b673-112">Przejdź do [krok 1: Przejrzyj architektury](vmm-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="0b673-112">Go to [Step 1: Review the architecture](vmm-to-azure-walkthrough-architecture.md)</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="0b673-113">Krok 2: Sprawdź wymagania wstępne i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="0b673-113">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="0b673-114">Upewnij się, że rozumiesz wymagania wstępne dotyczące wdrażania i ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="0b673-114">Make sure that you understand the deployment prerequisites and limitations.</span></span>

<span data-ttu-id="0b673-115">**Wymagania wstępne platformy Azure**: wymagane konto Microsoft Azure, sieci platformy Azure i kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="0b673-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
<span data-ttu-id="0b673-116">**Serwery lokalne, VMM i hosty funkcji Hyper-V**: Upewnij się, że serwery VMM i hosty funkcji Hyper-V są zgodne i przygotowania się do wdrażania usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0b673-116">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>
<span data-ttu-id="0b673-117">**Maszyny wirtualne replikowane**: Sprawdź, że maszyny wirtualne mają być replikowane spełniają wymagania dotyczące usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="0b673-117">**Replicated VMs**: Check that VMs you want to replicate comply with Azure requirements.</span></span>

<span data-ttu-id="0b673-118">Przejdź do [krok 2: Sprawdź wymagania wstępne i ograniczenia](vmm-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="0b673-118">Go to [Step 2: Verify prerequisites and limitations](vmm-to-azure-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="0b673-119">Krok 3: Planowanie pojemności</span><span class="sxs-lookup"><span data-stu-id="0b673-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="0b673-120">Jeśli pełne wdrożenie robimy, należy dowiedzieć się, jakie potrzebne zasoby replikacji.</span><span class="sxs-lookup"><span data-stu-id="0b673-120">If you're doing a full deployment, you need to figure out what replication resources you need.</span></span> <span data-ttu-id="0b673-121">Istnieje kilka narzędzi ułatwiających to zrobić.</span><span class="sxs-lookup"><span data-stu-id="0b673-121">There are a couple of tools available to help you do this.</span></span> <span data-ttu-id="0b673-122">Jeśli podczas wykonywania szybkiego skonfigurowany do środowiska testowego, możesz pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="0b673-122">If you're doing a quick set up to test the environment, you can skip this step.</span></span>

<span data-ttu-id="0b673-123">Przejdź do sekcji [Krok 3. Planowanie wydajności](vmm-to-azure-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="0b673-123">Go to [Step 3: Plan capacity](vmm-to-azure-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="0b673-124">Krok 4: Planowanie sieci</span><span class="sxs-lookup"><span data-stu-id="0b673-124">Step 4: Plan networking</span></span>

<span data-ttu-id="0b673-125">Należy wykonać niektóre sieci, planowanie upewnić się, że możesz skonfigurować mapowanie sieci, podczas wdrażania tego scenariusza, że maszyny wirtualne Azure zostaną podłączone do sieci wirtualnych platformy Azure po pracy awaryjnej, oraz że je przypisano odpowiednie IP adresów.</span><span class="sxs-lookup"><span data-stu-id="0b673-125">You need to do some network planning to ensure that you can configure network mapping when you deploy the scenario, that Azure VMs will be connected to Azure virtual networks after failover occurs, and that that they're assigned appropriate IP addresses.</span></span>

<span data-ttu-id="0b673-126">Przejdź do [krok 4: Planowanie sieci](vmm-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="0b673-126">Go to [Step 4: Plan networking](vmm-to-azure-walkthrough-network.md)</span></span>


## <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="0b673-127">Krok 5: Przygotowanie zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0b673-127">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="0b673-128">Konfigurowanie konta platformy Azure, sieci i magazynu.</span><span class="sxs-lookup"><span data-stu-id="0b673-128">Set up an Azure account, networks, and storage.</span></span> <span data-ttu-id="0b673-129">Można to zrobić podczas wdrażania, ale zaleca się, że można to zrobić przed rozpoczęciem.</span><span class="sxs-lookup"><span data-stu-id="0b673-129">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="0b673-130">Przejdź do [krok 5: przygotowanie Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="0b673-130">Go to [Step 5: Prepare Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span></span>

## <a name="step-6-prepare-vmm-and-hyper-v"></a><span data-ttu-id="0b673-131">Krok 6: Przygotowanie VMM i funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="0b673-131">Step 6: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="0b673-132">Przygotuj serwery lokalne, VMM i hosty funkcji Hyper-V do wdrażania usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0b673-132">Prepare the on-premises VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="0b673-133">Przejdź do [krok 6: Przygotowanie serwerów lokalnych](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="0b673-133">Go to [Step 6: Prepare on-premises servers](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="0b673-134">Krok 7: Konfigurowanie magazynu</span><span class="sxs-lookup"><span data-stu-id="0b673-134">Step 7: Set up a vault</span></span>

<span data-ttu-id="0b673-135">Konfigurowanie magazynu usług odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="0b673-135">Set up a Recovery Services vault.</span></span> <span data-ttu-id="0b673-136">Magazyn zawiera ustawienia konfiguracji i aranżuje replikację.</span><span class="sxs-lookup"><span data-stu-id="0b673-136">The vault contains configuration settings, and orchestrates replication.</span></span>

[<span data-ttu-id="0b673-137">Krok 7: Konfigurowanie magazynu</span><span class="sxs-lookup"><span data-stu-id="0b673-137">Step 7: Set up a vault</span></span>](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="0b673-138">Krok 8: Konfigurowanie ustawień źródłowa i docelowa</span><span class="sxs-lookup"><span data-stu-id="0b673-138">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="0b673-139">Konfigurowanie replikacji lokalizacja źródłowa i docelowa.</span><span class="sxs-lookup"><span data-stu-id="0b673-139">Set up the source and target replication locations.</span></span> <span data-ttu-id="0b673-140">Dodaj serwer programu VMM w magazynie i pobierane pliki instalacyjne dla składników usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0b673-140">Add the VMM server to the vault, and download the installation files for Site Recovery components.</span></span> <span data-ttu-id="0b673-141">Uruchom Instalatora dostawcy usługi Azure Site Recovery na serwerze programu VMM.</span><span class="sxs-lookup"><span data-stu-id="0b673-141">Run Azure Site Recovery Provider setup on the VMM server.</span></span> <span data-ttu-id="0b673-142">Instalator instaluje dostawcę na serwerze programu VMM i rejestruje serwer w magazynie.</span><span class="sxs-lookup"><span data-stu-id="0b673-142">Setup installs the Provider on the VMM server, and registers the server in the vault.</span></span> <span data-ttu-id="0b673-143">Agent usług odzyskiwania Microsoft należy zainstalować na każdym hoście funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="0b673-143">You install the Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="0b673-144">Przejdź do [krok 8: Konfigurowanie ustawień źródłowa i docelowa](vmm-to-azure-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="0b673-144">Go to [Step 8: Configure source and target settings](vmm-to-azure-walkthrough-source-target.md)</span></span>

## <a name="step-9-configure-network-mapping"></a><span data-ttu-id="0b673-145">Krok 9: Konfigurowanie mapowania sieci</span><span class="sxs-lookup"><span data-stu-id="0b673-145">Step 9: Configure network mapping</span></span>

<span data-ttu-id="0b673-146">Mapa lokalnych sieci maszyny Wirtualnej VMM do sieci wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0b673-146">Map on-premises VMM VM networks to Azure virtual networks.</span></span> <span data-ttu-id="0b673-147">Po przejściu w tryb failover maszynach wirtualnych platformy Azure są tworzone w sieci platformy Azure, który jest mapowany na lokalnej sieci maszyny Wirtualnej, w którym znajduje się źródło funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="0b673-147">After failover, Azure VMs are created in the Azure network that maps to the on-premises VM network in which the source Hyper-V is located.</span></span>

<span data-ttu-id="0b673-148">Przejdź do [krok 9: Konfigurowanie mapowania sieci](vmm-to-azure-walkthrough-network-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="0b673-148">Go to [Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>


## <a name="step-10-set-up-a-replication-policy"></a><span data-ttu-id="0b673-149">Krok 10: Konfigurowanie zasad replikacji</span><span class="sxs-lookup"><span data-stu-id="0b673-149">Step 10: Set up a replication policy</span></span>

<span data-ttu-id="0b673-150">Określ, jak będą replikowane lokalnych maszyn wirtualnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0b673-150">Specify how on-premises VMs will be replicated to Azure.</span></span>

<span data-ttu-id="0b673-151">Przejdź do [10 kroku: Konfigurowanie zasad replikacji](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="0b673-151">Go to [Step 10: Set up a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>


## <a name="step-11-enable-replication-for-vms"></a><span data-ttu-id="0b673-152">Krok 11: Włączanie replikacji maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="0b673-152">Step 11: Enable replication for VMs</span></span>

<span data-ttu-id="0b673-153">Wybierz maszyny wirtualne mają być replikowane.</span><span class="sxs-lookup"><span data-stu-id="0b673-153">Select the VMs you want to replicate.</span></span> <span data-ttu-id="0b673-154">Włączanie replikacji maszyny Wirtualnej wyzwala replikacji początkowej na platformie Azure, następuje replikacja różnicowa stałe.</span><span class="sxs-lookup"><span data-stu-id="0b673-154">ENabling a VM for replication triggers the initial replication to Azure, followed by ongoing delta replication.</span></span>

<span data-ttu-id="0b673-155">Przejdź do [krok 11: Włączanie replikacji](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="0b673-155">Go to [Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="0b673-156">Krok 12: Uruchom test trybu failover</span><span class="sxs-lookup"><span data-stu-id="0b673-156">Step 12: Run a test failover</span></span>

<span data-ttu-id="0b673-157">Uruchom testowanie trybu failover, aby upewnić się, że wszystko działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="0b673-157">Run a test failover to make sure everything's working as expected.</span></span>

<span data-ttu-id="0b673-158">Przejdź do [krok 12: testować tryb failover](vmm-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="0b673-158">Go to [Step 12: Run a test failover](vmm-to-azure-walkthrough-test-failover.md)</span></span>


