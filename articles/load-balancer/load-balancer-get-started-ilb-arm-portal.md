---
title: "aaaCreate wewnętrznego modułu równoważenia obciążenia - portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate wewnętrznego modułu równoważenia w Menedżerze zasobów przy użyciu portalu Azure hello obciążenia"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ac14fb9-8d14-4892-bfe6-8bc74c48ae2c
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 80124217a84857b542eb41cb814ec97234176dd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-in-hello-azure-portal"></a><span data-ttu-id="b7223-103">Utworzyć wewnętrznego modułu równoważenia obciążenia w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b7223-103">Create an Internal load balancer in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b7223-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b7223-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="b7223-105">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="b7223-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="b7223-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b7223-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="b7223-107">Szablon</span><span class="sxs-lookup"><span data-stu-id="b7223-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="b7223-108">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b7223-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="b7223-109">W tym artykule omówiono przy użyciu modelu wdrażania Menedżera zasobów hello, który firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello [klasycznego modelu wdrażania](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b7223-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a><span data-ttu-id="b7223-110">Rozpoczęcie tworzenia wewnętrznego modułu równoważenia obciążenia w witrynie Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b7223-110">Get started creating an Internal load balancer using Azure portal</span></span>

<span data-ttu-id="b7223-111">Użyj hello poniższych kroków toocreate wewnętrznego modułu równoważenia obciążenia z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b7223-111">Use hello following steps toocreate an internal load balancer from hello Azure Portal.</span></span>

1. <span data-ttu-id="b7223-112">Otwórz przeglądarkę, przejdź toohello [portalu Azure](http://portal.azure.com)i zaloguj się przy użyciu konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b7223-112">Open a browser, navigate toohello [Azure portal](http://portal.azure.com), and sign in with your Azure account.</span></span>
2. <span data-ttu-id="b7223-113">Lewy górny powitania po stronie powitania ekranu, kliknij przycisk **nowy** > **sieci** > **modułu równoważenia obciążenia**.</span><span class="sxs-lookup"><span data-stu-id="b7223-113">In hello upper left hand side of hello screen, click **New** > **Networking** > **Load balancer**.</span></span>
3. <span data-ttu-id="b7223-114">W hello **modułu równoważenia obciążenia Utwórz** bloku, wprowadź **nazwa** dla Twojej usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="b7223-114">In hello **Create load balancer** blade, enter a **Name** for your load balancer.</span></span>
4. <span data-ttu-id="b7223-115">W obszarze **Schemat** kliknij pozycję **Wewnętrzny**.</span><span class="sxs-lookup"><span data-stu-id="b7223-115">Under **Scheme**, click **Internal**.</span></span>
5. <span data-ttu-id="b7223-116">Kliknij przycisk **sieci wirtualnej**, a następnie wybierz hello miejscu modułu równoważenia obciążenia hello toocreate sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b7223-116">Click **Virtual network**, and then select hello virtual network where you want toocreate hello load balancer.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b7223-117">Jeśli nie ma sieci wirtualnej hello ma toouse, sprawdź hello **lokalizacji** dla usługi równoważenia obciążenia hello jest używany i odpowiednio je zmienić.</span><span class="sxs-lookup"><span data-stu-id="b7223-117">If you do not see hello virtual network you want toouse, check hello **Location** you are using for hello load balancer, and change it accordingly.</span></span>

6. <span data-ttu-id="b7223-118">Kliknij przycisk **podsieci**, a następnie wybierz miejsce modułu równoważenia obciążenia hello toocreate podsieci hello.</span><span class="sxs-lookup"><span data-stu-id="b7223-118">Click **Subnet**, and then select hello subnet where you want toocreate hello load balancer.</span></span>
7. <span data-ttu-id="b7223-119">W obszarze **przypisywania adresów IP**, kliknij opcję **dynamiczne** lub **statycznych**, w zależności od tego, czy chcesz hello adresu IP dla hello obciążenia równoważenia toobe stałej (statyczny) lub nie.</span><span class="sxs-lookup"><span data-stu-id="b7223-119">Under **IP address assignment**, click either **Dynamic** or **Static**, depending on whether you want hello IP address for hello load balancer toobe fixed (static) or not.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b7223-120">W przypadku wybrania toouse statycznego adresu IP, konieczne będzie tooprovide adres usługi równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="b7223-120">If you select toouse a static IP address, you will have tooprovide an address for hello load balancer.</span></span>

8. <span data-ttu-id="b7223-121">W obszarze **grupy zasobów** Określ hello nazwę nowej grupy zasobów dla usługi równoważenia obciążenia hello, lub kliknij przycisk **wybierz istniejącą** i wybierz istniejącą grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="b7223-121">Under **Resource group** either specify hello name of a new resource group for hello load balancer, or click **select existing** and select an existing resource group.</span></span>
9. <span data-ttu-id="b7223-122">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b7223-122">Click **Create**.</span></span>

## <a name="configure-load-balancing-rules"></a><span data-ttu-id="b7223-123">Konfigurowanie reguł równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="b7223-123">Configure load balancing rules</span></span>

<span data-ttu-id="b7223-124">Po hello załadować tworzenia równoważenia, przejdź tooconfigure zasobów usługi równoważenia obciążenia toohello go.</span><span class="sxs-lookup"><span data-stu-id="b7223-124">After hello load balancer creation, navigate toohello load balancer resource tooconfigure it.</span></span>
<span data-ttu-id="b7223-125">Należy tooconfigure najpierw puli adresów zaplecza i badanie przed rozpoczęciem konfigurowania reguły równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="b7223-125">You need tooconfigure first a back-end address pool and a probe before configuring a load balancing rule.</span></span>

### <a name="step-1-configure-a-back-end-pool"></a><span data-ttu-id="b7223-126">Krok 1. Konfigurowanie puli zaplecza</span><span class="sxs-lookup"><span data-stu-id="b7223-126">Step 1: Configure a back-end pool</span></span>

1. <span data-ttu-id="b7223-127">W portalu Azure hello, kliknij przycisk **Przeglądaj** > **usługi równoważenia obciążenia**, a następnie kliknij przycisk modułu równoważenia obciążenia hello utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="b7223-127">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="b7223-128">W hello **ustawienia** bloku, kliknij przycisk **pul zaplecza**.</span><span class="sxs-lookup"><span data-stu-id="b7223-128">In hello **Settings** blade, click **Backend pools**.</span></span>
3. <span data-ttu-id="b7223-129">W hello **pul adresów zaplecza** bloku, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="b7223-129">In hello **Backend address pools** blade, click **Add**.</span></span>
4. <span data-ttu-id="b7223-130">W hello **Dodaj pulę zaplecza** bloku, wprowadź **nazwa** hello puli zaplecza, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="b7223-130">In hello **Add backend pool** blade, enter a **Name** for hello backend pool, and then click **OK**.</span></span>

### <a name="step-2-configure-a-probe"></a><span data-ttu-id="b7223-131">Krok 2. Konfigurowanie sondy</span><span class="sxs-lookup"><span data-stu-id="b7223-131">Step 2: Configure a probe</span></span>

1. <span data-ttu-id="b7223-132">W portalu Azure hello, kliknij przycisk **Przeglądaj** > **usługi równoważenia obciążenia**, a następnie kliknij przycisk modułu równoważenia obciążenia hello utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="b7223-132">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="b7223-133">W hello **ustawienia** bloku, kliknij przycisk **sondy**.</span><span class="sxs-lookup"><span data-stu-id="b7223-133">In hello **Settings** blade, click **Probes**.</span></span>
3. <span data-ttu-id="b7223-134">W hello **sondy** bloku, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="b7223-134">In hello **Probes**  blade, click **Add**.</span></span>
4. <span data-ttu-id="b7223-135">W hello **sondowania Dodaj** bloku, wprowadź **nazwa** hello sondy.</span><span class="sxs-lookup"><span data-stu-id="b7223-135">In hello **Add probe** blade, enter a **Name** for hello probe.</span></span>
5. <span data-ttu-id="b7223-136">W obszarze **Protokół** wybierz pozycję **HTTP** (w przypadku witryn sieci Web) lub **TCP** (w przypadku innych aplikacji działających w oparciu o protokół TCP).</span><span class="sxs-lookup"><span data-stu-id="b7223-136">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="b7223-137">W obszarze **portu**, określ hello portu toouse podczas uzyskiwania dostępu do badania hello.</span><span class="sxs-lookup"><span data-stu-id="b7223-137">Under **Port**, specify hello port toouse when accessing hello probe.</span></span>
7. <span data-ttu-id="b7223-138">W obszarze **ścieżki** (dla protokołu HTTP sondy tylko), określ toouse ścieżka hello jako badanie.</span><span class="sxs-lookup"><span data-stu-id="b7223-138">Under **Path** (for HTTP probes only), specify hello path toouse as a probe.</span></span>
8. <span data-ttu-id="b7223-139">W obszarze **interwał** Określ, jak często tooprobe hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b7223-139">Under **Interval** specify how frequently tooprobe hello application.</span></span>
9. <span data-ttu-id="b7223-140">W obszarze **próg złej kondycji**, określ liczbę prób powinna zakończyć się niepowodzeniem przed maszyny wirtualnej hello wewnętrznej bazy danych jest oznaczona jako w złej kondycji.</span><span class="sxs-lookup"><span data-stu-id="b7223-140">Under **Unhealthy threshold**, specify how many attempts should fail before hello backend virtual machine is marked as unhealthy.</span></span>
10. <span data-ttu-id="b7223-141">Kliknij przycisk **OK** toocreate sondowania.</span><span class="sxs-lookup"><span data-stu-id="b7223-141">Click **OK** toocreate probe.</span></span>

### <a name="step-3-configure-load-balancing-rules"></a><span data-ttu-id="b7223-142">Krok 3. Konfigurowanie reguł równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="b7223-142">Step 3: Configure load balancing rules</span></span>

1. <span data-ttu-id="b7223-143">W portalu Azure hello, kliknij przycisk **Przeglądaj** > **usługi równoważenia obciążenia**, a następnie kliknij przycisk modułu równoważenia obciążenia hello utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="b7223-143">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="b7223-144">W hello **ustawienia** bloku, kliknij przycisk **reguły równoważenia obciążenia**.</span><span class="sxs-lookup"><span data-stu-id="b7223-144">In hello **Settings** blade, click **Load balancing rules**.</span></span>
3. <span data-ttu-id="b7223-145">W hello **reguły równoważenia obciążenia** bloku, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="b7223-145">In hello **Load balancing rules** blade, click **Add**.</span></span>
4. <span data-ttu-id="b7223-146">W hello **reguły równoważenia obciążenia Dodaj** bloku, wprowadź **nazwa** hello reguły.</span><span class="sxs-lookup"><span data-stu-id="b7223-146">In hello **Add load balancing rule** blade, enter a **Name** for hello rule.</span></span>
5. <span data-ttu-id="b7223-147">W obszarze **Protokół** wybierz pozycję **HTTP** (w przypadku witryn sieci Web) lub **TCP** (w przypadku innych aplikacji działających w oparciu o protokół TCP).</span><span class="sxs-lookup"><span data-stu-id="b7223-147">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="b7223-148">W obszarze **portu**, określ hello portu klienci łączą się moduł równoważenia obciążenia hello tooin.</span><span class="sxs-lookup"><span data-stu-id="b7223-148">Under **Port**, specify hello port clients connect tooin hello load balancer.</span></span>
7. <span data-ttu-id="b7223-149">W obszarze **portu zaplecza**, określ hello toobe port używany w puli zaplecza hello (zazwyczaj port usługi równoważenia obciążenia hello i port zaplecza hello są hello sam).</span><span class="sxs-lookup"><span data-stu-id="b7223-149">Under **Backend port**, specify hello port toobe used in hello backend pool (usually, hello load balancer port and hello backend port are hello same).</span></span>
8. <span data-ttu-id="b7223-150">W obszarze **puli zaplecza**, wybierz pozycję zaplecza hello puli utworzonego powyżej.</span><span class="sxs-lookup"><span data-stu-id="b7223-150">Under **Backend pool**, select hello backend pool you created above.</span></span>
9. <span data-ttu-id="b7223-151">W obszarze **trwałości sesji**, wybierz sposób toopersist sesji.</span><span class="sxs-lookup"><span data-stu-id="b7223-151">Under **Session persistence**, select how you want sessions toopersist.</span></span>
10. <span data-ttu-id="b7223-152">W obszarze **limit czasu bezczynności (w minutach)**, określ hello limit czasu bezczynności.</span><span class="sxs-lookup"><span data-stu-id="b7223-152">Under **Idle timeout (minutes)**, specify hello idle timeout.</span></span>
11. <span data-ttu-id="b7223-153">W obszarze **Zmienny adres IP (bezpośredni zwrot serwera)** kliknij pozycję **Wyłączony** lub **Włączony**.</span><span class="sxs-lookup"><span data-stu-id="b7223-153">Under **Floating IP (direct server return)**, click **Disabled** or **Enabled**.</span></span>
12. <span data-ttu-id="b7223-154">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="b7223-154">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7223-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b7223-155">Next steps</span></span>

<span data-ttu-id="b7223-156">[Configure a load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="b7223-156">[Configure a load balancer distribution mode](load-balancer-distribution-mode.md)</span></span>

<span data-ttu-id="b7223-157">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="b7223-157">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md)</span></span>

