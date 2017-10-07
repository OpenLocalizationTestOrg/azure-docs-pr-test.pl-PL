---
title: "aaaSet hello źródła i celu tooAzure replikacji serwerze fizycznym z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Podsumowanie tooset kroki hello źródłowa i docelowa ustawień replikacji magazynu tooAzure serwery fizyczne z hello usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 2e3d03bc-4e53-4590-8a01-f702d3cc9500
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: e75ef23174d77509bf54380eba8f251a7337a45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-hello-source-and-target-for-physical-server-replication-tooazure"></a><span data-ttu-id="5c395-103">Krok 7: Konfigurowanie hello źródłowa i docelowa dla tooAzure replikacji serwera fizycznego</span><span class="sxs-lookup"><span data-stu-id="5c395-103">Step 7: Set up hello source and target for physical server replication tooAzure</span></span>

<span data-ttu-id="5c395-104">W tym artykule opisano sposób tooconfigure źródłowa i docelowa ustawień podczas replikowania lokalnie tooAzure serwerów fizycznych za pomocą hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5c395-104">This article describes how tooconfigure source and target settings when replicating on-premises physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="5c395-105">Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="5c395-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="5c395-106">Konfigurowanie środowiska źródłowego hello</span><span class="sxs-lookup"><span data-stu-id="5c395-106">Set up hello source environment</span></span>

<span data-ttu-id="5c395-107">Konfigurowanie serwera konfiguracji hello, zarejestruj go w magazynie hello i Odkryj maszyny.</span><span class="sxs-lookup"><span data-stu-id="5c395-107">Set up hello configuration server, register it in hello vault, and discover machines.</span></span>

1. <span data-ttu-id="5c395-108">Kliknij przycisk **lokacji odzyskiwania** > **krok 1: Przygotowanie infrastruktury** > **źródła**.</span><span class="sxs-lookup"><span data-stu-id="5c395-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="5c395-109">Jeśli nie masz serwera konfiguracji, kliknij przycisk **+ serwer konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="5c395-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="5c395-110">W **Dodaj serwer**, sprawdź, czy **serwera konfiguracji** pojawia się w **typ serwera**.</span><span class="sxs-lookup"><span data-stu-id="5c395-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="5c395-111">Pobierz plik instalacyjny instalacja Unified usługi Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="5c395-111">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="5c395-112">Pobierz klucz rejestracji magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="5c395-112">Download hello vault registration key.</span></span> <span data-ttu-id="5c395-113">Należy to po uruchomieniu Instalatora Unified.</span><span class="sxs-lookup"><span data-stu-id="5c395-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="5c395-114">klucz Hello jest ważny przez pięć dni po jego wygenerowaniu.</span><span class="sxs-lookup"><span data-stu-id="5c395-114">hello key is valid for five days after you generate it.</span></span>

   ![Konfiguracja źródła](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a><span data-ttu-id="5c395-116">Zarejestruj serwer konfiguracji hello w magazynie hello</span><span class="sxs-lookup"><span data-stu-id="5c395-116">Register hello configuration server in hello vault</span></span>

<span data-ttu-id="5c395-117">Następujące hello przed start, a następnie uruchom serwer konfiguracji hello tooinstall Unified instalacji, powitania serwera przetwarzania i hello główny serwer docelowy.</span><span class="sxs-lookup"><span data-stu-id="5c395-117">Do hello following before you start, then run Unified Setup tooinstall hello configuration server, hello process server, and hello master target server.</span></span> <span data-ttu-id="5c395-118">Witaj wideo Opisuje konfigurowanie składników hello replikacji tooAzure maszyny Wirtualnej VMware.</span><span class="sxs-lookup"><span data-stu-id="5c395-118">hello video describes setting up hello components for VMware VM tooAzure replication.</span></span> <span data-ttu-id="5c395-119">Jednak hello sam proces jest prawidłowa dla replikacji tooAzure serwera fizycznego.</span><span class="sxs-lookup"><span data-stu-id="5c395-119">However, hello same process is valid for physical server tooAzure replication.</span></span>

- <span data-ttu-id="5c395-120">Upewnij się, że hello zegar systemowy jest zsynchronizowany z na powitania serwera konfiguracji maszyny Wirtualnej, [serwer czasu](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="5c395-120">On hello configuration server VM, make sure that hello system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="5c395-121">Powinna być zgodna.</span><span class="sxs-lookup"><span data-stu-id="5c395-121">It should match.</span></span> <span data-ttu-id="5c395-122">Jeśli jest 15 minut przed lub za, Instalator może zakończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="5c395-122">If it's 15 minutes in front or behind, setup might fail.</span></span>
- <span data-ttu-id="5c395-123">Uruchom Instalatora jako Administrator lokalny na komputerze z serwerem konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="5c395-123">Run setup as a Local Administrator on hello configuration server machine.</span></span>
- <span data-ttu-id="5c395-124">Upewnij się, że włączono protokołu TLS 1.0 na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5c395-124">Make sure TLS 1.0 is enabled on hello VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="5c395-125">można również zainstalować serwer konfiguracji Hello [z wiersza polecenia hello](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="5c395-125">hello configuration server can also be installed [from hello command line](http://aka.ms/installconfigsrv).</span></span>




## <a name="set-up-hello-target-environment"></a><span data-ttu-id="5c395-126">Konfigurowanie środowiska docelowego hello</span><span class="sxs-lookup"><span data-stu-id="5c395-126">Set up hello target environment</span></span>

<span data-ttu-id="5c395-127">Aby skonfigurować środowisko docelowe hello, upewnij się, że masz konto magazynu Azure i konfigurowanie sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5c395-127">Before you set up hello target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="5c395-128">Kliknij przycisk **przygotowanie infrastruktury** > **docelowego**, i wybierz hello ma toouse subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5c395-128">Click **Prepare infrastructure** > **Target**, and select hello Azure subscription you want toouse.</span></span>
2. <span data-ttu-id="5c395-129">Określ, czy docelowy modelu wdrażania jest oparte na Menedżera zasobów albo klasycznego.</span><span class="sxs-lookup"><span data-stu-id="5c395-129">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="5c395-130">Usługa Site Recovery sprawdza, czy masz co najmniej jedno zgodne konto magazynu Azure i co najmniej jedną sieć platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5c395-130">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![docelowy](./media/physical-walkthrough-source-target/gs-target.png)

4. <span data-ttu-id="5c395-132">Jeśli nie utworzono konta magazynu lub sieci, kliknij przycisk **+ konto magazynu** lub **+ sieć**, toocreate wbudowanego konta lub sieci Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="5c395-132">If you haven't created a storage account or network, click **+Storage account** or **+Network**, toocreate a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c395-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5c395-133">Next steps</span></span>

<span data-ttu-id="5c395-134">Przejdź do zbyt[krok 8: Konfigurowanie zasad replikacji](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="5c395-134">Go too[Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>
