---
title: "równoważenia obciążenia aaaCreate internetowy - klasycznego portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Internet równoważenia obciążenia przy użyciu modelu wdrażania klasycznego hello klasycznego portalu Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fa3e93c0-968a-472d-a17c-65665c050db2
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 27b0d5af6e7b493fa94a9dfbfa260483ae95a2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-classic-portal"></a><span data-ttu-id="96624-103">Rozpocząć tworzenie internetowy modułu równoważenia obciążenia (klasyczne) w hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="96624-103">Get started creating an Internet facing load balancer (classic) in hello Azure classic portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="96624-104">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="96624-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="96624-105">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="96624-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="96624-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="96624-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="96624-107">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="96624-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="96624-108">Przed rozpoczęciem pracy z zasobów platformy Azure, jest ważne toounderstand, że Azure ma obecnie dwa modele wdrażania: usługi Azure Resource Manager i model klasyczny.</span><span class="sxs-lookup"><span data-stu-id="96624-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="96624-109">Przed rozpoczęciem pracy z dowolnym zasobem Azure należy zapoznać się z [modelami i narzędziami wdrażania](../azure-classic-rm.md).</span><span class="sxs-lookup"><span data-stu-id="96624-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="96624-110">Hello dokumentację dotyczącą różnych narzędzi można wyświetlić, klikając karty hello u góry hello tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="96624-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="96624-111">W tym artykule omówiono hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="96624-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="96624-112">Możesz również [Dowiedz się, jak usługa równoważenia przy użyciu usługi Azure Resource Manager obciążenia toocreate Internetem](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="96624-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a><span data-ttu-id="96624-113">Konfigurowanie dostępnego z Internetu modułu równoważenia obciążenia do maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="96624-113">Set up an Internet-facing load balancer for virtual machines</span></span>

<span data-ttu-id="96624-114">Kolejność tooload równowagi ruchu w sieci z hello Internet między maszynami wirtualnymi hello usługi w chmurze należy utworzyć zestawu z równoważeniem obciążenia.</span><span class="sxs-lookup"><span data-stu-id="96624-114">In order tooload balance network traffic from hello Internet across hello virtual machines of a cloud service, you must create a load-balanced set.</span></span> <span data-ttu-id="96624-115">W tej procedurze założono, że utworzono już hello maszyn wirtualnych oraz czy są one wszystkich w hello sama usługa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="96624-115">This procedure assumes that you have already created hello virtual machines and that they are all within hello same cloud service.</span></span>

<span data-ttu-id="96624-116">**tooconfigure zestaw z równoważeniem obciążenia dla maszyn wirtualnych**</span><span class="sxs-lookup"><span data-stu-id="96624-116">**tooconfigure a load-balanced set for virtual machines**</span></span>

1. <span data-ttu-id="96624-117">W hello klasycznego portalu Azure, kliknij przycisk **maszyn wirtualnych**, a następnie kliknij nazwę hello maszyny wirtualnej w zestawie o zrównoważonym obciążeniu hello.</span><span class="sxs-lookup"><span data-stu-id="96624-117">In hello Azure classic portal, click **Virtual Machines**, and then click hello name of a virtual machine in hello load-balanced set.</span></span>
2. <span data-ttu-id="96624-118">Kliknij kolejno opcje **Punkty końcowe** i **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="96624-118">Click **Endpoints**, and then click **Add**.</span></span>
3. <span data-ttu-id="96624-119">Na powitania **Dodaj maszynę wirtualną punktu końcowego tooa** kliknij strzałkę w prawo hello.</span><span class="sxs-lookup"><span data-stu-id="96624-119">On hello **Add an endpoint tooa virtual machine** page, click hello right arrow.</span></span>
4. <span data-ttu-id="96624-120">Na powitania **Określ szczegóły hello punktu końcowego hello** strony:</span><span class="sxs-lookup"><span data-stu-id="96624-120">On hello **Specify hello details of hello endpoint** page:</span></span>

   * <span data-ttu-id="96624-121">W **nazwa**, wpisz nazwę dla punktu końcowego hello, lub wybierz nazwę hello z hello listy wstępnie zdefiniowanych punktów końcowych dla wspólnych protokołów.</span><span class="sxs-lookup"><span data-stu-id="96624-121">In **Name**, type a name for hello endpoint or select hello name from hello list of predefined endpoints for common protocols.</span></span>
   * <span data-ttu-id="96624-122">W **protokołu**, wybierz protokół hello wymagany przez typ hello punktu końcowego TCP lub UDP, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="96624-122">In **Protocol**, select hello protocol required by hello type of endpoint, either TCP or UDP, as needed.</span></span>
   * <span data-ttu-id="96624-123">W **portu publicznego i prywatnego**, wpisz numery portów hello, który ma hello toouse maszyny wirtualnej, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="96624-123">In **Public Port and Private Port**, type hello port numbers that you want hello virtual machine toouse, as needed.</span></span> <span data-ttu-id="96624-124">Można użyć hello port prywatny i reguły zapory na powitania ruchu tooredirect maszyny wirtualnej w taki sposób, który jest odpowiedni dla twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="96624-124">You can use hello private port and firewall rules on hello virtual machine tooredirect traffic in a way that is appropriate for your application.</span></span> <span data-ttu-id="96624-125">port prywatny Hello można hello w taki sam jak port publiczny hello.</span><span class="sxs-lookup"><span data-stu-id="96624-125">hello private port can be hello same as hello public port.</span></span> <span data-ttu-id="96624-126">Na przykład dla punktu końcowego dla ruchu w sieci web (HTTP), można przypisać portu 80 tooboth hello publicznych i prywatnych portów.</span><span class="sxs-lookup"><span data-stu-id="96624-126">For example, for an endpoint for web (HTTP) traffic, you could assign port 80 tooboth hello public and private port.</span></span>

5. <span data-ttu-id="96624-127">Wybierz **Utwórz zestaw o zrównoważonym obciążeniu**, a następnie kliknij przycisk strzałki w prawo hello.</span><span class="sxs-lookup"><span data-stu-id="96624-127">Select **Create a load-balanced set**, and then click hello right arrow.</span></span>
6. <span data-ttu-id="96624-128">Na powitania **skonfigurować zestaw z równoważeniem obciążenia hello** strony, wpisz nazwę zestawu o zrównoważonym obciążeniu hello, a następnie przypisz wartości hello sondowania zachowanie hello moduł równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="96624-128">On hello **Configure hello load-balanced set** page, type a name for hello load-balanced set, and then assign hello values for probe behavior of hello Azure Load Balancer.</span></span> <span data-ttu-id="96624-129">Witaj moduł równoważenia obciążenia używa toodetermine sond hello maszyn wirtualnych w zestawie o zrównoważonym obciążeniu hello są dostępne tooreceive ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="96624-129">hello Load Balancer uses probes toodetermine if hello virtual machines in hello load-balanced set are available tooreceive incoming traffic.</span></span>
7. <span data-ttu-id="96624-130">Kliknij przycisk endpoint hello znacznik wyboru toocreate hello równoważeniem obciążenia.</span><span class="sxs-lookup"><span data-stu-id="96624-130">Click hello check mark toocreate hello load-balanced endpoint.</span></span> <span data-ttu-id="96624-131">Zobaczysz **tak** w hello **Nazwa zestawu o zrównoważonym obciążeniu** kolumny hello **punkty końcowe** strony hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="96624-131">You will see **Yes** in hello **Load-balanced set name** column of hello **Endpoints** page for hello virtual machine.</span></span>
8. <span data-ttu-id="96624-132">W portalu powitania kliknij **maszyn wirtualnych**, kliknij nazwę hello dodatkowe maszyny wirtualnej w zestawie o zrównoważonym obciążeniu hello, kliknij przycisk **punkty końcowe**, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="96624-132">In hello portal, click **Virtual Machines**, click hello name of an additional virtual machine in hello load-balanced set, click **Endpoints**, and then click **Add**.</span></span>
9. <span data-ttu-id="96624-133">Na powitania **Dodaj maszynę wirtualną punktu końcowego tooa** kliknij przycisk **Dodawanie punktu końcowego tooan równoważeniem obciążenia zestawu**, wybierz nazwę hello hello zestawu z równoważeniem obciążenia, a następnie kliknij strzałkę w prawo hello.</span><span class="sxs-lookup"><span data-stu-id="96624-133">On hello **Add an endpoint tooa virtual machine** page, click **Add endpoint tooan existing load-balanced set**, select hello name of hello load-balanced set, and then click hello right arrow.</span></span>
10. <span data-ttu-id="96624-134">Na powitania **Określ szczegóły hello punktu końcowego hello** , wpisz nazwę dla punktu końcowego hello, a następnie kliknij przycisk znacznika wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="96624-134">On hello **Specify hello details of hello endpoint** page, type a name for hello endpoint, and then click hello check mark.</span></span>

<span data-ttu-id="96624-135">Witaj dodatkowych maszyn wirtualnych w zestawie o zrównoważonym obciążeniu hello Powtórz kroki od 8-10.</span><span class="sxs-lookup"><span data-stu-id="96624-135">For hello additional virtual machines in hello load-balanced set, repeat steps 8-10.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96624-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="96624-136">Next steps</span></span>

<span data-ttu-id="96624-137">[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-ps.md) (Wprowadzenie do konfigurowania wewnętrznego modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="96624-137">[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-ps.md)</span></span>

<span data-ttu-id="96624-138">[Configure a load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="96624-138">[Configure a load balancer distribution mode](load-balancer-distribution-mode.md)</span></span>

<span data-ttu-id="96624-139">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="96624-139">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md)</span></span>
