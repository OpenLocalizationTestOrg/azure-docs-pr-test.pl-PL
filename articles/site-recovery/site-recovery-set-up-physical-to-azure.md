---
title: "Konfigurowanie środowiska źródłowego hello (tooAzure serwerów fizycznych) | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tooset się toostart środowiska użytkownika lokalnego, replikowania serwerów fizycznych z systemem Windows lub Linux na platformie Azure."
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
ms.openlocfilehash: d4702265bf36910015685d2bba99d6e577531bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-physical-server-tooazure"></a><span data-ttu-id="b2b8e-103">Konfigurowanie środowiska źródłowego hello (tooAzure serwera fizycznego)</span><span class="sxs-lookup"><span data-stu-id="b2b8e-103">Set up hello source environment (physical server tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b2b8e-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="b2b8e-104">VMware tooAzure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="b2b8e-105">TooAzure fizycznych</span><span class="sxs-lookup"><span data-stu-id="b2b8e-105">Physical tooAzure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="b2b8e-106">W tym artykule opisano sposób tooset się toostart środowiska użytkownika lokalnego, replikowania serwerów fizycznych z systemem Windows lub Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b2b8e-106">This article describes how tooset up your on-premises environment toostart replicating physical servers running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2b8e-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b2b8e-107">Prerequisites</span></span>

<span data-ttu-id="b2b8e-108">Hello artykule przyjęto założenie, że masz już:</span><span class="sxs-lookup"><span data-stu-id="b2b8e-108">hello article assumes that you already have:</span></span>
1. <span data-ttu-id="b2b8e-109">Magazyn usług odzyskiwania w hello [portalu Azure](http://portal.azure.com "portalu Azure").</span><span class="sxs-lookup"><span data-stu-id="b2b8e-109">A Recovery Services vault in hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
3. <span data-ttu-id="b2b8e-110">Komputer fizyczny, na którym serwerze tooinstall hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b2b8e-110">A physical computer on which tooinstall hello configuration server.</span></span>

### <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="b2b8e-111">Minimalne wymagania dotyczące konfiguracji serwera</span><span class="sxs-lookup"><span data-stu-id="b2b8e-111">Configuration server minimum requirements</span></span>
<span data-ttu-id="b2b8e-112">Witaj w poniższej tabeli wymieniono hello minimalne wymagania dotyczące sprzętu, oprogramowania i wymagania sieciowe dotyczące serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b2b8e-112">hello following table lists hello minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="b2b8e-113">Serwery proxy oparty na protokole HTTPS nie są obsługiwane przez serwer konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="b2b8e-113">HTTPS-based proxy servers are not supported by hello configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="b2b8e-114">Wybranie celów ochrony</span><span class="sxs-lookup"><span data-stu-id="b2b8e-114">Choose your protection goals</span></span>

1. <span data-ttu-id="b2b8e-115">W hello portalu Azure, przejdź do pozycji toohello **usług odzyskiwania** magazyny bloku, a następnie wybierz magazyn.</span><span class="sxs-lookup"><span data-stu-id="b2b8e-115">In hello Azure portal, go toohello **Recovery Services** vaults blade and select your vault.</span></span>
2. <span data-ttu-id="b2b8e-116">W hello **zasobów** kliknij menu magazynu hello **wprowadzenie** > **usługi Site Recovery** > **krok 1: przygotowanie Infrastruktura** > **cel ochrony**.</span><span class="sxs-lookup"><span data-stu-id="b2b8e-116">In hello **Resource** menu of hello vault, click **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Wybieranie celów](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. <span data-ttu-id="b2b8e-118">W **cel ochrony**, wybierz pozycję **tooAzure** i **nie zwirtualizowanych/inne**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="b2b8e-118">In **Protection goal**, select **tooAzure** and **Not virtualized/Other**, and then click **OK**.</span></span>

    ![Wybieranie celów](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-hello-source-environment"></a><span data-ttu-id="b2b8e-120">Konfigurowanie środowiska źródłowego hello</span><span class="sxs-lookup"><span data-stu-id="b2b8e-120">Set up hello source environment</span></span>

1. <span data-ttu-id="b2b8e-121">W **Przygotuj źródło**, jeśli nie masz serwera konfiguracji, kliknij przycisk **+ serwer konfiguracji** tooadd jeden.</span><span class="sxs-lookup"><span data-stu-id="b2b8e-121">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** tooadd one.</span></span>

  ![Konfiguracja źródła](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. <span data-ttu-id="b2b8e-123">W hello **Dodaj serwer** bloku, sprawdź, czy **serwera konfiguracji** pojawia się w **typ serwera**.</span><span class="sxs-lookup"><span data-stu-id="b2b8e-123">In hello **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="b2b8e-124">Pobierz plik instalacyjny instalacja Unified usługi Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="b2b8e-124">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="b2b8e-125">Pobierz klucz rejestracji magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="b2b8e-125">Download hello vault registration key.</span></span> <span data-ttu-id="b2b8e-126">Po uruchomieniu Instalatora Unified muszą się hello klucza rejestracji.</span><span class="sxs-lookup"><span data-stu-id="b2b8e-126">You need hello registration key when you run Unified Setup.</span></span> <span data-ttu-id="b2b8e-127">klucz Hello jest ważny przez pięć dni po jego wygenerowaniu.</span><span class="sxs-lookup"><span data-stu-id="b2b8e-127">hello key is valid for five days after you generate it.</span></span>

    ![Konfiguracja źródła](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. <span data-ttu-id="b2b8e-129">Na komputerze hello używasz jako hello konfiguracji serwera, uruchom **Unified instalacja usługi Azure Site Recovery** tooinstall hello konfiguracji serwera, powitania serwera przetwarzania i główny hello docelowego serwera.</span><span class="sxs-lookup"><span data-stu-id="b2b8e-129">On hello machine you’re using as hello configuration server, run **Azure Site Recovery Unified Setup** tooinstall hello configuration server, hello process server, and hello master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="b2b8e-130">Uruchom usługi Azure Site Recovery Unified Instalatora</span><span class="sxs-lookup"><span data-stu-id="b2b8e-130">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="b2b8e-131">Rejestracja serwera konfiguracji kończy się niepowodzeniem, jeśli czas hello na zegara systemowego jest więcej niż pięć minut wylogowuje na czas lokalny.</span><span class="sxs-lookup"><span data-stu-id="b2b8e-131">Configuration server registration fails if hello time on your computer's system clock is more than five minutes off of local time.</span></span> <span data-ttu-id="b2b8e-132">Synchronizowanie zegara systemowego z [serwer czasu](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) przed rozpoczęciem powitalne instalacji.</span><span class="sxs-lookup"><span data-stu-id="b2b8e-132">Synchronize your system clock with a [time server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting hello installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="b2b8e-133">Serwer konfiguracji Hello można zainstalować za pomocą wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="b2b8e-133">hello configuration server can be installed via a command line.</span></span> <span data-ttu-id="b2b8e-134">Aby uzyskać więcej informacji, zobacz [Instalowanie serwera konfiguracji za pomocą narzędzia wiersza polecenia](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="b2b8e-134">For more information, see [Installing configuration server using command-line tools](http://aka.ms/installconfigsrv).</span></span>


## <a name="common-issues"></a><span data-ttu-id="b2b8e-135">Typowe problemy</span><span class="sxs-lookup"><span data-stu-id="b2b8e-135">Common issues</span></span>

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="b2b8e-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b2b8e-136">Next steps</span></span>

<span data-ttu-id="b2b8e-137">Następny krok polega na [Konfigurowanie środowiska docelowego](./site-recovery-prepare-target-physical-to-azure.md) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b2b8e-137">Next step involves [setting up your target environment](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span></span>
