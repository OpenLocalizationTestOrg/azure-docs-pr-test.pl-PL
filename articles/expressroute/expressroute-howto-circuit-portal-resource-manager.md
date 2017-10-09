---
title: "Tworzenie i modyfikowanie obwodu usługi ExpressRoute: portalu Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toocreate, udostępnić, sprawdź aktualizacji, usuwania i anulowanie zastrzeżenia obwodu usługi ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68d59d59-ed4d-482f-9cbc-534ebb090613
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/07/2017
ms.author: cherylmc;ganesr
ms.openlocfilehash: 200418aed6bdebace43a2f57cf532d1c8d13cb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a><span data-ttu-id="06716-103">Tworzenie i modyfikowanie obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="06716-103">Create and modify an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="06716-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="06716-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="06716-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="06716-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="06716-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="06716-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="06716-107">Video - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="06716-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="06716-108">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="06716-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="06716-109">W tym artykule opisano, jak toocreate obwodu Azure ExpressRoute przy użyciu hello Azure portal hello usługi Azure Resource Manager deployment modelu.</span><span class="sxs-lookup"><span data-stu-id="06716-109">This article describes how toocreate an Azure ExpressRoute circuit by using hello Azure portal and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="06716-110">Hello także następujące kroki opisano, jak toocheck hello stanu obwodu hello, zaktualizuj lub usuń i anulowanie zastrzeżenia go.</span><span class="sxs-lookup"><span data-stu-id="06716-110">hello following steps also show you how toocheck hello status of hello circuit, update it, or delete and deprovision it.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="06716-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="06716-111">Before you begin</span></span>
* <span data-ttu-id="06716-112">Przejrzyj hello [wymagania wstępne](expressroute-prerequisites.md) i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="06716-112">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="06716-113">Upewnij się, że masz dostęp do toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="06716-113">Ensure that you have access toohello [Azure portal](https://portal.azure.com).</span></span>
* <span data-ttu-id="06716-114">Upewnij się, że masz uprawnienia toocreate nowych zasobów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="06716-114">Ensure that you have permissions toocreate new networking resources.</span></span> <span data-ttu-id="06716-115">Jeśli nie masz odpowiednich uprawnień hello, skontaktuj się z administratorem konta.</span><span class="sxs-lookup"><span data-stu-id="06716-115">Contact your account administrator if you do not have hello right permissions.</span></span>
* <span data-ttu-id="06716-116">Możesz [wyświetlanie wideo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) przed rozpoczęciem w kolejności toobetter zrozumieć kroki hello.</span><span class="sxs-lookup"><span data-stu-id="06716-116">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) before beginning in order toobetter understand hello steps.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="06716-117">Tworzenie i przydzielanie obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="06716-117">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-toohello-azure-portal"></a><span data-ttu-id="06716-118">1. Zaloguj się toohello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="06716-118">1. Sign in toohello Azure portal</span></span>
<span data-ttu-id="06716-119">W przeglądarce Przejdź toohello [portalu Azure](http://portal.azure.com) i zaloguj się przy użyciu konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="06716-119">From a browser, navigate toohello [Azure portal](http://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="2-create-a-new-expressroute-circuit"></a><span data-ttu-id="06716-120">2. Utwórz nowy obwód usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="06716-120">2. Create a new ExpressRoute circuit</span></span>
> [!IMPORTANT]
> <span data-ttu-id="06716-121">Od momentu hello wygenerowaniu klucza usługi będą naliczane obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="06716-121">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="06716-122">Upewnij się, wykonać tę operację, gdy dostawca połączenia hello jest gotowy tooprovision hello obwodu.</span><span class="sxs-lookup"><span data-stu-id="06716-122">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

1. <span data-ttu-id="06716-123">Można utworzyć obwodu usługi ExpressRoute, wybierając hello opcja toocreate nowy zasób.</span><span class="sxs-lookup"><span data-stu-id="06716-123">You can create an ExpressRoute circuit by selecting hello option toocreate a new resource.</span></span> <span data-ttu-id="06716-124">Kliknij przycisk **nowy** > **sieci** > **ExpressRoute**, jak pokazano w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="06716-124">Click **New** > **Networking** > **ExpressRoute**, as shown in hello following image:</span></span>
   
    ![Create an ExpressRoute circuit (Tworzenie obwodu usługi ExpressRoute)](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. <span data-ttu-id="06716-126">Po kliknięciu **ExpressRoute**, zobaczysz hello **obwodu ExpressRoute utworzyć** bloku.</span><span class="sxs-lookup"><span data-stu-id="06716-126">After you click **ExpressRoute**, you'll see hello **Create ExpressRoute circuit** blade.</span></span> <span data-ttu-id="06716-127">Po jest wypełnianie hello wartości w tym bloku, upewnij się, możesz określić hello prawidłowe jednostki SKU warstwy i pomiaru danych.</span><span class="sxs-lookup"><span data-stu-id="06716-127">When you're filling in hello values on this blade, make sure that you specify hello correct SKU tier and data metering.</span></span>
   
   * <span data-ttu-id="06716-128">**Warstwa** Określa, czy włączone jest standardem ExpressRoute lub dodatek usługi ExpressRoute w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="06716-128">**Tier** determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="06716-129">Można określić **standardowe** tooget hello standardowy SKU lub **Premium** dla hello premium dodatku.</span><span class="sxs-lookup"><span data-stu-id="06716-129">You can specify **Standard** tooget hello standard SKU or **Premium** for hello premium add-on.</span></span>
   * <span data-ttu-id="06716-130">**Pomiaru danych** Określa typ rozliczeń hello.</span><span class="sxs-lookup"><span data-stu-id="06716-130">**Data metering** determines hello billing type.</span></span> <span data-ttu-id="06716-131">Można określić **Metered** planu dane naliczane i **nieograniczone** planu nieograniczone danych.</span><span class="sxs-lookup"><span data-stu-id="06716-131">You can specify **Metered** for a metered data plan and **Unlimited** for an unlimited data plan.</span></span> <span data-ttu-id="06716-132">Zmiana typu rozliczeń hello z **Metered** za**nieograniczone**, ale nie można zmienić typu hello z **nieograniczone** za**Metered**.</span><span class="sxs-lookup"><span data-stu-id="06716-132">Note that you can change hello billing type from **Metered** too**Unlimited**, but you can't change hello type from **Unlimited** too**Metered**.</span></span>
     
     ![Skonfiguruj hello SKU warstwy i pomiaru danych](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> <span data-ttu-id="06716-134">Należy pamiętać, że hello lokalizacja komunikacji równorzędnej wskazuje hello [lokalizacji fizycznej](expressroute-locations.md) gdzie są komunikacji równorzędnej z firmą Microsoft.</span><span class="sxs-lookup"><span data-stu-id="06716-134">Please be aware that hello Peering Location indicates hello [physical location](expressroute-locations.md) where you are peering with Microsoft.</span></span> <span data-ttu-id="06716-135">Jest to **nie** połączone za właściwość "Lokalizacja", która odwołuje się toohello lokalizacji geograficznej, gdzie znajduje się hello dostawcy zasobów sieciowych Azure.</span><span class="sxs-lookup"><span data-stu-id="06716-135">This is **not** linked too"Location" property, which refers toohello geography where hello Azure Network Resource Provider is located.</span></span> <span data-ttu-id="06716-136">Gdy nie są powiązane, jest dobrym rozwiązaniem toochoose dostawcy zasobów sieciowych toohello geograficznie Zamknij lokalizacja komunikacji równorzędnej hello obwodu.</span><span class="sxs-lookup"><span data-stu-id="06716-136">While they are not related, it is a good practice toochoose a Network Resource Provider geographically close toohello Peering Location of hello circuit.</span></span> 
> 
> 

### <a name="3-view-hello-circuits-and-properties"></a><span data-ttu-id="06716-137">3. Widok hello obwody i właściwości</span><span class="sxs-lookup"><span data-stu-id="06716-137">3. View hello circuits and properties</span></span>
<span data-ttu-id="06716-138">**Wyświetlanie wszystkich obwodów hello**</span><span class="sxs-lookup"><span data-stu-id="06716-138">**View all hello circuits**</span></span>

<span data-ttu-id="06716-139">Można wyświetlić wszystkich obwodów hello, które zostały utworzone przez wybranie **wszystkie zasoby** w menu po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="06716-139">You can view all hello circuits that you created by selecting **All resources** on hello left-side menu.</span></span>

![Obwody widoku](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

<span data-ttu-id="06716-141">**Wyświetl właściwości hello**</span><span class="sxs-lookup"><span data-stu-id="06716-141">**View hello properties**</span></span>

    You can view hello properties of hello circuit by selecting it. On this blade, note hello service key for hello circuit. You must copy hello circuit key for your circuit and pass it down toohello service provider toocomplete hello provisioning process. hello circuit key is specific tooyour circuit.

![Wyświetl właściwości](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="06716-143">4. Wyślij łączności hello usługodawcy tooyour klucza do inicjowania obsługi</span><span class="sxs-lookup"><span data-stu-id="06716-143">4. Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="06716-144">W tym bloku **stan dostawcy** zawiera informacje na temat hello bieżący stan inicjowania obsługi administracyjnej po stronie dostawcy usług hello.</span><span class="sxs-lookup"><span data-stu-id="06716-144">On this blade, **Provider status** provides information on hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="06716-145">**Stan obwodu** zawiera stan hello na powitania po stronie firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="06716-145">**Circuit status** provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="06716-146">Aby uzyskać więcej informacji na temat obwodu inicjowania obsługi administracyjnej stanów Zobacz hello [przepływy pracy](expressroute-workflows.md#expressroute-circuit-provisioning-states) artykułu.</span><span class="sxs-lookup"><span data-stu-id="06716-146">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="06716-147">Podczas tworzenia nowego obwodu ExpressRoute obwodu hello będą powitania po stanu:</span><span class="sxs-lookup"><span data-stu-id="06716-147">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

<span data-ttu-id="06716-148">Stan dostawcy: nie zainicjowano obsługę administracyjną</span><span class="sxs-lookup"><span data-stu-id="06716-148">Provider status: Not provisioned</span></span><BR>
<span data-ttu-id="06716-149">Stan obwodu: włączone</span><span class="sxs-lookup"><span data-stu-id="06716-149">Circuit status: Enabled</span></span>

![Zainicjuj proces inicjowania obsługi administracyjnej](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

<span data-ttu-id="06716-151">obwodu Hello ulegnie zmianie po stanu, gdy dostawca łączności hello jest w toku hello włączenie go dla Ciebie toohello:</span><span class="sxs-lookup"><span data-stu-id="06716-151">hello circuit will change toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

<span data-ttu-id="06716-152">Stan dostawcy: Inicjowanie obsługi administracyjnej</span><span class="sxs-lookup"><span data-stu-id="06716-152">Provider status: Provisioning</span></span><BR>
<span data-ttu-id="06716-153">Stan obwodu: włączone</span><span class="sxs-lookup"><span data-stu-id="06716-153">Circuit status: Enabled</span></span>

<span data-ttu-id="06716-154">Możesz toobe stanie toouse obwodu usługi ExpressRoute musi być w powitania po stanu:</span><span class="sxs-lookup"><span data-stu-id="06716-154">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

<span data-ttu-id="06716-155">Stan dostawcy: zainicjowano obsługę administracyjną</span><span class="sxs-lookup"><span data-stu-id="06716-155">Provider status: Provisioned</span></span><BR>
<span data-ttu-id="06716-156">Stan obwodu: włączone</span><span class="sxs-lookup"><span data-stu-id="06716-156">Circuit status: Enabled</span></span>

### <a name="5-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="06716-157">5. Okresowo sprawdzać stan hello i stan hello hello obwodu klucza</span><span class="sxs-lookup"><span data-stu-id="06716-157">5. Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="06716-158">Można wyświetlić właściwości hello obwodu hello są zainteresowani przez zaznaczenie go.</span><span class="sxs-lookup"><span data-stu-id="06716-158">You can view hello properties of hello circuit that you're interested in by selecting it.</span></span> <span data-ttu-id="06716-159">Sprawdź hello **stan dostawcy** i upewnij się, że została przeniesiona za**obsługiwane administracyjnie** przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="06716-159">Check hello **Provider status** and ensure that it has moved too**Provisioned** before you continue.</span></span>

![Stan obwodu i dostawcy](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a><span data-ttu-id="06716-161">6. Tworzenie konfiguracji routingu</span><span class="sxs-lookup"><span data-stu-id="06716-161">6. Create your routing configuration</span></span>
<span data-ttu-id="06716-162">Aby uzyskać instrukcje, zobacz toohello [obwodu ExpressRoute konfiguracji routingu](expressroute-howto-routing-portal-resource-manager.md) artykuł toocreate i modyfikowania obwodu komunikacji równorzędnych.</span><span class="sxs-lookup"><span data-stu-id="06716-162">For step-by-step instructions, refer toohello [ExpressRoute circuit routing configuration](expressroute-howto-routing-portal-resource-manager.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06716-163">Te instrukcje mają zastosowanie tylko toocircuits, które są tworzone za pomocą dostawcy usług, które oferują warstwy 2 łączność usługi.</span><span class="sxs-lookup"><span data-stu-id="06716-163">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="06716-164">Jeśli używasz usługodawcy, który oferuje zarządzanych warstwy 3 usługi (zazwyczaj IP sieci VPN, takie jak MPLS), dostawca połączenia będzie Konfigurowanie i zarządzanie nimi routingu dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="06716-164">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="7-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="06716-165">7. Link sieci wirtualnej tooan obwodu usługi expressroute</span><span class="sxs-lookup"><span data-stu-id="06716-165">7. Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="06716-166">Następnie połącz tooyour sieci wirtualnej obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="06716-166">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="06716-167">Użyj hello [połączenie wirtualnej sieci obwody tooExpressRoute](expressroute-howto-linkvnet-arm.md) artykuł podczas pracy z modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="06716-167">Use hello [Linking virtual networks tooExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with hello Resource Manager deployment model.</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="06716-168">Pobieranie stanu hello obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="06716-168">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="06716-169">Stan hello obwód można wyświetlić, wybierając go.</span><span class="sxs-lookup"><span data-stu-id="06716-169">You can view hello status of a circuit by selecting it.</span></span> 

![Stan obwodu usługi ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="06716-171">Modyfikowanie obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="06716-171">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="06716-172">Można zmodyfikować niektórych właściwości obwodu usługi ExpressRoute, bez wywierania wpływu na łączność.</span><span class="sxs-lookup"><span data-stu-id="06716-172">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="06716-173">Możesz zrobić hello po bez przestojów:</span><span class="sxs-lookup"><span data-stu-id="06716-173">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="06716-174">Włącz lub Wyłącz dodatek premium usługi ExpressRoute dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="06716-174">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="06716-175">Hello zwiększyć przepustowość obwodu ExpressRoute pod warunkiem, że na porcie hello jest dostępna pojemność.</span><span class="sxs-lookup"><span data-stu-id="06716-175">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="06716-176">Należy pamiętać, że zmiany na starszą wersję hello przepustowości obwodu nie jest obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="06716-176">Note that downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="06716-177">Zmień hello planu z danych naliczane tooUnlimited danych pomiaru.</span><span class="sxs-lookup"><span data-stu-id="06716-177">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="06716-178">Należy pamiętać, zmiana planu zliczania hello z tooMetered nieograniczone danych, danych nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="06716-178">Note that changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="06716-179">Można włączyć lub wyłączyć *operacje klasycznego*.</span><span class="sxs-lookup"><span data-stu-id="06716-179">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="06716-180">Aby uzyskać więcej informacji na limity i ograniczenia, można znaleźć toohello [ExpressRoute — często zadawane pytania](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="06716-180">For more information on limits and limitations, refer toohello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

<span data-ttu-id="06716-181">toomodify obwodu usługi ExpressRoute, wybierz polecenie hello **konfiguracji** pokazane na poniższej ilustracji hello.</span><span class="sxs-lookup"><span data-stu-id="06716-181">toomodify an ExpressRoute circuit, click on hello **Configuration** as shown in hello figure below.</span></span>

![Modyfikowanie obwodu](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

<span data-ttu-id="06716-183">Można zmodyfikować hello przepustowości, jednostka SKU, modelu rozliczeń i zezwolić klasycznego operacji w obrębie bloku konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="06716-183">You can modify hello bandwidth, SKU, billing model and allow classic operations within hello configuration blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06716-184">Konieczne może być obwodu ExpressRoute hello toorecreate na powitania istniejącego portu jest nieodpowiedni pojemności.</span><span class="sxs-lookup"><span data-stu-id="06716-184">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="06716-185">Nie można uaktualnić obwodu hello, jeśli nie bez dodatkowej pojemności dostępnej w tej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="06716-185">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="06716-186">Nie można zmniejszyć hello przepustowości obwodu ExpressRoute bez zakłóceń.</span><span class="sxs-lookup"><span data-stu-id="06716-186">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="06716-187">Obniżenie przepustowości wymaga obwodu ExpressRoute hello toodeprovision, a następnie Udostępnij ponownie nowy obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="06716-187">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> <span data-ttu-id="06716-188">Wyłączenie dodatku premium operacja może zakończyć się niepowodzeniem, jeśli używasz zasobów, które są większe niż co to jest dozwolone dla obwodu standardowe hello.</span><span class="sxs-lookup"><span data-stu-id="06716-188">Disable premium add-on operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="06716-189">Anulowania obsługi i usuwania obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="06716-189">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="06716-190">Można usunąć obwodu usługi ExpressRoute, wybierając hello **usunąć** ikony.</span><span class="sxs-lookup"><span data-stu-id="06716-190">You can delete your ExpressRoute circuit by selecting hello **delete** icon.</span></span> <span data-ttu-id="06716-191">Należy uwzględnić następujące hello:</span><span class="sxs-lookup"><span data-stu-id="06716-191">Note hello following:</span></span>

* <span data-ttu-id="06716-192">Należy odłączyć wszystkie sieci wirtualne od hello obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="06716-192">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="06716-193">Jeśli ta operacja nie powiedzie się, sprawdź, czy wszystkie sieci wirtualne są połączone toohello obwodu.</span><span class="sxs-lookup"><span data-stu-id="06716-193">If this operation fails, check whether any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="06716-194">Jeśli stan inicjowania obsługi hello ExpressRoute obwodu usługi Dostawca jest **inicjowania obsługi administracyjnej** lub **obsługiwane administracyjnie** należy skontaktować się z obwodu hello toodeprovision dostawcy usług w bok.</span><span class="sxs-lookup"><span data-stu-id="06716-194">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="06716-195">Firma Microsoft będzie kontynuować tooreserve zasobów i obciążać Cię do momentu dostawcy usług hello kończy obwodu hello anulowania obsługi i powiadamia nam.</span><span class="sxs-lookup"><span data-stu-id="06716-195">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="06716-196">Jeśli dostawcy usług hello została anulowana obwodu hello (stan inicjowania dostawcy usług hello ustawiono zbyt**nieudostępniane**) następnie można usunąć obwodu hello.</span><span class="sxs-lookup"><span data-stu-id="06716-196">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="06716-197">Spowoduje to zatrzymanie rozliczeń dla obwodu hello</span><span class="sxs-lookup"><span data-stu-id="06716-197">This will stop billing for hello circuit</span></span>

## <a name="next-steps"></a><span data-ttu-id="06716-198">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="06716-198">Next steps</span></span>
<span data-ttu-id="06716-199">Po utworzeniu obwodu, upewnij się, że hello następujące:</span><span class="sxs-lookup"><span data-stu-id="06716-199">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="06716-200">Tworzenie i modyfikowanie routingu dla obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="06716-200">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-portal-resource-manager.md)
* [<span data-ttu-id="06716-201">Łączenie z sieci wirtualnej tooyour obwodu usługi expressroute</span><span class="sxs-lookup"><span data-stu-id="06716-201">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

