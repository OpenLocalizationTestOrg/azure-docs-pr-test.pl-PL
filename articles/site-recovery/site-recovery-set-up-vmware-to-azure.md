---
title: "Konfigurowanie środowiska źródłowego hello (VMware tooAzure) | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooset się z toostart środowiska lokalnego replikowanie wirtualnych VMware maszyny tooAzure."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: cbeeffc1061b11223e12ff3e237fa7e55b999aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-vmware-tooazure"></a><span data-ttu-id="24337-103">Konfigurowanie środowiska źródłowego hello (VMware tooAzure)</span><span class="sxs-lookup"><span data-stu-id="24337-103">Set up hello source environment (VMware tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="24337-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="24337-104">VMware tooAzure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="24337-105">TooAzure fizycznych</span><span class="sxs-lookup"><span data-stu-id="24337-105">Physical tooAzure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="24337-106">W tym artykule opisano, jak tooset się z toostart środowiska lokalnego replikowanie wirtualnych maszyn uruchomiona na VMware tooAzure.</span><span class="sxs-lookup"><span data-stu-id="24337-106">This article describes how tooset up your on-premises environment toostart replicating virtual machines running on VMware tooAzure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24337-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="24337-107">Prerequisites</span></span>

<span data-ttu-id="24337-108">Hello artykule przyjęto założenie, że utworzono już:</span><span class="sxs-lookup"><span data-stu-id="24337-108">hello article assumes that you have already created:</span></span>
- <span data-ttu-id="24337-109">W magazynie usług odzyskiwania w hello [portalu Azure](http://portal.azure.com "portalu Azure").</span><span class="sxs-lookup"><span data-stu-id="24337-109">A Recovery Services Vault in hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="24337-110">Dedykowane konto w oprogramowaniu VMware vCenter sieci używanej do [automatyczne odnajdowanie](./site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="24337-110">A dedicated account in your VMware vCenter that can be used for [automatic discovery](./site-recovery-vmware-to-azure.md).</span></span>
- <span data-ttu-id="24337-111">Maszynę wirtualną, na którym serwerze tooinstall hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="24337-111">A virtual machine on which tooinstall hello configuration server.</span></span>

## <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="24337-112">Minimalne wymagania dotyczące konfiguracji serwera</span><span class="sxs-lookup"><span data-stu-id="24337-112">Configuration server minimum requirements</span></span>
<span data-ttu-id="24337-113">oprogramowanie serwera konfiguracji Hello powinny zostać wdrożone na maszynie wirtualnej VMware wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="24337-113">hello configuration server software should be deployed on a highly available VMware virtual machine.</span></span> <span data-ttu-id="24337-114">Witaj w poniższej tabeli wymieniono hello minimalne wymagania dotyczące sprzętu, oprogramowania i wymagania sieciowe dotyczące serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="24337-114">hello following table lists hello minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="24337-115">Serwery proxy oparty na protokole HTTPS nie są obsługiwane przez serwer konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="24337-115">HTTPS-based proxy servers are not supported by hello configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="24337-116">Wybranie celów ochrony</span><span class="sxs-lookup"><span data-stu-id="24337-116">Choose your protection goals</span></span>

1. <span data-ttu-id="24337-117">W hello portalu Azure, przejdź do pozycji toohello **usług odzyskiwania** magazyn bloku i wybierz magazyn.</span><span class="sxs-lookup"><span data-stu-id="24337-117">In hello Azure portal, go toohello **Recovery Services** vault blade and select your vault.</span></span>
2. <span data-ttu-id="24337-118">Menu hello zasobów magazynu hello Przejdź zbyt**wprowadzenie** > **usługi Site Recovery** > **krok 1: Przygotowanie infrastruktury**  >  **Cel ochrony**.</span><span class="sxs-lookup"><span data-stu-id="24337-118">On hello resource menu of hello vault, go too**Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Wybieranie celów](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. <span data-ttu-id="24337-120">W **cel ochrony**, wybierz pozycję **tooAzure**i wybierz polecenie **tak, z programem VMware vSphere Hypervisor**.</span><span class="sxs-lookup"><span data-stu-id="24337-120">In **Protection goal**, select **tooAzure**, and choose **Yes, with VMware vSphere Hypervisor**.</span></span> <span data-ttu-id="24337-121">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="24337-121">Then click **OK**.</span></span>

    ![Wybieranie celów](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a><span data-ttu-id="24337-123">Konfigurowanie środowiska źródłowego hello</span><span class="sxs-lookup"><span data-stu-id="24337-123">Set up hello source environment</span></span>
<span data-ttu-id="24337-124">Konfigurowanie środowiska źródłowego hello obejmuje dwa działania głównego:</span><span class="sxs-lookup"><span data-stu-id="24337-124">Setting up hello source environment involves two main activities:</span></span>

- <span data-ttu-id="24337-125">Zainstaluj i Zarejestruj serwer konfiguracji z usługą Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="24337-125">Install and register a configuration server with Site Recovery.</span></span>
- <span data-ttu-id="24337-126">Odnajdywanie maszyn wirtualnych lokalnie łącząc usługi Site Recovery tooyour lokalnymi VMware vCenter lub vSphere EXSi hostów.</span><span class="sxs-lookup"><span data-stu-id="24337-126">Discover your on-premises virtual machines by connecting Site Recovery tooyour on-premises VMware vCenter or vSphere EXSi hosts.</span></span>

### <a name="step-1-install-and-register-a-configuration-server"></a><span data-ttu-id="24337-127">Krok 1: Zainstaluj i Zarejestruj serwer konfiguracji</span><span class="sxs-lookup"><span data-stu-id="24337-127">Step 1: Install and register a configuration server</span></span>

1. <span data-ttu-id="24337-128">Kliknij przycisk **krok 1: Przygotowanie infrastruktury** > **źródła**.</span><span class="sxs-lookup"><span data-stu-id="24337-128">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span> <span data-ttu-id="24337-129">W **Przygotuj źródło**, jeśli nie masz serwera konfiguracji, kliknij przycisk **+ serwer konfiguracji** tooadd jeden.</span><span class="sxs-lookup"><span data-stu-id="24337-129">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** tooadd one.</span></span>

    ![Konfiguracja źródła](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. <span data-ttu-id="24337-131">Na powitania **Dodaj serwer** bloku, sprawdź, czy **serwera konfiguracji** pojawia się w **typ serwera**.</span><span class="sxs-lookup"><span data-stu-id="24337-131">On hello **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="24337-132">Pobierz plik instalacyjny instalacja Unified usługi Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="24337-132">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="24337-133">Pobierz klucz rejestracji magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="24337-133">Download hello vault registration key.</span></span> <span data-ttu-id="24337-134">Po uruchomieniu Instalatora Unified muszą się hello klucza rejestracji.</span><span class="sxs-lookup"><span data-stu-id="24337-134">You need hello registration key when you run Unified Setup.</span></span> <span data-ttu-id="24337-135">klucz Hello jest ważny przez pięć dni po jego wygenerowaniu.</span><span class="sxs-lookup"><span data-stu-id="24337-135">hello key is valid for five days after you generate it.</span></span>

    ![Konfiguracja źródła](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. <span data-ttu-id="24337-137">Na komputerze hello używasz jako hello konfiguracji serwera, uruchom **Unified instalacja usługi Azure Site Recovery** tooinstall hello konfiguracji serwera, powitania serwera przetwarzania i główny hello docelowego serwera.</span><span class="sxs-lookup"><span data-stu-id="24337-137">On hello machine you’re using as hello configuration server, run **Azure Site Recovery Unified Setup** tooinstall hello configuration server, hello process server, and hello master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="24337-138">Uruchom usługi Azure Site Recovery Unified Instalatora</span><span class="sxs-lookup"><span data-stu-id="24337-138">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="24337-139">Rejestracja serwera konfiguracji kończy się niepowodzeniem, jeśli hello godziną zegara systemowego różni się od czasu lokalnego przez ponad pięć minut.</span><span class="sxs-lookup"><span data-stu-id="24337-139">Configuration server registration fails if hello time on your computer's system clock differs from local time by more than five minutes.</span></span> <span data-ttu-id="24337-140">Synchronizowanie zegara systemowego z [serwer czasu](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) przed rozpoczęciem powitalne instalacji.</span><span class="sxs-lookup"><span data-stu-id="24337-140">Synchronize your system clock with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting hello installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="24337-141">Serwer konfiguracji Hello można zainstalować za pomocą wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="24337-141">hello configuration server can be installed via command line.</span></span> <span data-ttu-id="24337-142">Aby uzyskać więcej informacji, zobacz [serwera konfiguracji hello instalowanie przy użyciu narzędzia wiersza polecenia](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="24337-142">For more information, see [Installing hello configuration server using Command-line tools](http://aka.ms/installconfigsrv).</span></span>

#### <a name="add-hello-vmware-account-for-automatic-discovery"></a><span data-ttu-id="24337-143">Dodaj konto VMware hello automatycznego wykrywania</span><span class="sxs-lookup"><span data-stu-id="24337-143">Add hello VMware account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a><span data-ttu-id="24337-144">Krok 2: Dodaj vCenter</span><span class="sxs-lookup"><span data-stu-id="24337-144">Step 2: Add a vCenter</span></span>
<span data-ttu-id="24337-145">tooallow usługi Azure Site Recovery toodiscover maszyn wirtualnych działających w środowisku lokalnym, potrzebujesz tooconnect Twojego programu VMware vCenter Server lub hostach ESXi vSphere z usługą Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="24337-145">tooallow Azure Site Recovery toodiscover virtual machines running in your on-premises environment, you need tooconnect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span>

<span data-ttu-id="24337-146">Wybierz **+ vCenter** toostart łączenie programu VMware vCenter server lub VMware vSphere ESXi hosta.</span><span class="sxs-lookup"><span data-stu-id="24337-146">Select **+vCenter** toostart connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a><span data-ttu-id="24337-147">Typowe problemy</span><span class="sxs-lookup"><span data-stu-id="24337-147">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="24337-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="24337-148">Next steps</span></span>
<span data-ttu-id="24337-149">[Konfigurowanie środowiska docelowego](./site-recovery-prepare-target-vmware-to-azure.md) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="24337-149">[Set up your target environment](./site-recovery-prepare-target-vmware-to-azure.md) in Azure.</span></span>
