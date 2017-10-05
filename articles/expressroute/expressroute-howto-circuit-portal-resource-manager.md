---
title: "Tworzenie i modyfikowanie obwodu usługi ExpressRoute: portalu Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tworzenia, obsługi administracyjnej, sprawdź, aktualizacji, usuwania i anulowanie zastrzeżenia obwodu usługi ExpressRoute."
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
ms.openlocfilehash: e3721cd3c031622788f553e71a6555b844f3f7dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a><span data-ttu-id="e551d-103">Tworzenie i modyfikowanie obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e551d-103">Create and modify an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e551d-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e551d-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="e551d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e551d-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="e551d-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e551d-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="e551d-107">Video - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e551d-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="e551d-108">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="e551d-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="e551d-109">W tym artykule opisano sposób tworzenia obwodu usługi Azure ExpressRoute przy użyciu portalu Azure i modelu wdrażania usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e551d-109">This article describes how to create an Azure ExpressRoute circuit by using the Azure portal and the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="e551d-110">Poniższe kroki przedstawiają także sposób Sprawdź stan obwodu, zaktualizować lub usunąć i anulowanie zastrzeżenia go.</span><span class="sxs-lookup"><span data-stu-id="e551d-110">The following steps also show you how to check the status of the circuit, update it, or delete and deprovision it.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="e551d-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="e551d-111">Before you begin</span></span>
* <span data-ttu-id="e551d-112">Przegląd [wymagania wstępne](expressroute-prerequisites.md) i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="e551d-112">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="e551d-113">Upewnij się, że masz dostęp do [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e551d-113">Ensure that you have access to the [Azure portal](https://portal.azure.com).</span></span>
* <span data-ttu-id="e551d-114">Upewnij się, że masz uprawnienia do tworzenia nowych zasobów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="e551d-114">Ensure that you have permissions to create new networking resources.</span></span> <span data-ttu-id="e551d-115">Jeśli nie masz odpowiednich uprawnień, skontaktuj się z administratorem konta.</span><span class="sxs-lookup"><span data-stu-id="e551d-115">Contact your account administrator if you do not have the right permissions.</span></span>
* <span data-ttu-id="e551d-116">Możesz [wyświetlanie wideo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) przed rozpoczęciem, aby lepiej zrozumieć kroki.</span><span class="sxs-lookup"><span data-stu-id="e551d-116">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) before beginning in order to better understand the steps.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="e551d-117">Tworzenie i przydzielanie obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e551d-117">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-to-the-azure-portal"></a><span data-ttu-id="e551d-118">1. Logowanie się do witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e551d-118">1. Sign in to the Azure portal</span></span>
<span data-ttu-id="e551d-119">Przejdź w przeglądarce do witryny [Azure Portal](http://portal.azure.com) i zaloguj się przy użyciu konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e551d-119">From a browser, navigate to the [Azure portal](http://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="2-create-a-new-expressroute-circuit"></a><span data-ttu-id="e551d-120">2. Utwórz nowy obwód usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e551d-120">2. Create a new ExpressRoute circuit</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e551d-121">Od momentu jego wygenerowaniu klucza usługi będą naliczane obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e551d-121">Your ExpressRoute circuit will be billed from the moment a service key is issued.</span></span> <span data-ttu-id="e551d-122">Upewnij się, gdy dostawca łączności jest gotowy do udostępniania obwodu podczas wykonywania tej operacji.</span><span class="sxs-lookup"><span data-stu-id="e551d-122">Ensure that you perform this operation when the connectivity provider is ready to provision the circuit.</span></span>
> 
> 

1. <span data-ttu-id="e551d-123">Można utworzyć obwodu usługi ExpressRoute, wybierając opcję, aby utworzyć nowy zasób.</span><span class="sxs-lookup"><span data-stu-id="e551d-123">You can create an ExpressRoute circuit by selecting the option to create a new resource.</span></span> <span data-ttu-id="e551d-124">Kliknij przycisk **nowy** > **sieci** > **ExpressRoute**, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="e551d-124">Click **New** > **Networking** > **ExpressRoute**, as shown in the following image:</span></span>
   
    ![Create an ExpressRoute circuit (Tworzenie obwodu usługi ExpressRoute)](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. <span data-ttu-id="e551d-126">Po kliknięciu **ExpressRoute**, zobaczysz **obwodu ExpressRoute utworzyć** bloku.</span><span class="sxs-lookup"><span data-stu-id="e551d-126">After you click **ExpressRoute**, you'll see the **Create ExpressRoute circuit** blade.</span></span> <span data-ttu-id="e551d-127">Po jest wypełnianie wartości w tym bloku, upewnij się, że podajesz prawidłowe jednostki SKU warstwy i pomiaru danych.</span><span class="sxs-lookup"><span data-stu-id="e551d-127">When you're filling in the values on this blade, make sure that you specify the correct SKU tier and data metering.</span></span>
   
   * <span data-ttu-id="e551d-128">**Warstwa** Określa, czy włączone jest standardem ExpressRoute lub dodatek usługi ExpressRoute w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="e551d-128">**Tier** determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="e551d-129">Można określić **standardowe** można pobrać wersji standard lub **Premium** dla dodatku premium.</span><span class="sxs-lookup"><span data-stu-id="e551d-129">You can specify **Standard** to get the standard SKU or **Premium** for the premium add-on.</span></span>
   * <span data-ttu-id="e551d-130">**Pomiaru danych** Określa typ rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="e551d-130">**Data metering** determines the billing type.</span></span> <span data-ttu-id="e551d-131">Można określić **Metered** planu dane naliczane i **nieograniczone** planu nieograniczone danych.</span><span class="sxs-lookup"><span data-stu-id="e551d-131">You can specify **Metered** for a metered data plan and **Unlimited** for an unlimited data plan.</span></span> <span data-ttu-id="e551d-132">Zmiana rozliczeń typu z **Metered** do **bez ograniczeń**, ale nie można zmienić typu z **bez ograniczeń** do **Metered**.</span><span class="sxs-lookup"><span data-stu-id="e551d-132">Note that you can change the billing type from **Metered** to **Unlimited**, but you can't change the type from **Unlimited** to **Metered**.</span></span>
     
     ![Skonfiguruj warstwy jednostki SKU i pomiaru danych](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> <span data-ttu-id="e551d-134">Należy pamiętać, że wskazuje lokalizacji elementu równorzędnego [lokalizacji fizycznej](expressroute-locations.md) gdzie są komunikacji równorzędnej z firmą Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e551d-134">Please be aware that the Peering Location indicates the [physical location](expressroute-locations.md) where you are peering with Microsoft.</span></span> <span data-ttu-id="e551d-135">Jest to **nie** połączone z właściwością "Lokalizacja", która odwołuje się do lokalizacji geograficznej, w którym znajduje się dostawcy zasobów sieciowych Azure.</span><span class="sxs-lookup"><span data-stu-id="e551d-135">This is **not** linked to "Location" property, which refers to the geography where the Azure Network Resource Provider is located.</span></span> <span data-ttu-id="e551d-136">Gdy nie są powiązane, jest dobrym rozwiązaniem, aby wybrać dostawcy zasobów sieciowych w lokalizacji geograficznej blisko lokalizacji elementu równorzędnego obwodu.</span><span class="sxs-lookup"><span data-stu-id="e551d-136">While they are not related, it is a good practice to choose a Network Resource Provider geographically close to the Peering Location of the circuit.</span></span> 
> 
> 

### <a name="3-view-the-circuits-and-properties"></a><span data-ttu-id="e551d-137">3. Wyświetl obwody i właściwości</span><span class="sxs-lookup"><span data-stu-id="e551d-137">3. View the circuits and properties</span></span>
<span data-ttu-id="e551d-138">**Wyświetlanie wszystkich obwodów**</span><span class="sxs-lookup"><span data-stu-id="e551d-138">**View all the circuits**</span></span>

<span data-ttu-id="e551d-139">Można wyświetlić wszystkich obwodów, które zostały utworzone przez wybranie **wszystkie zasoby** w menu po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="e551d-139">You can view all the circuits that you created by selecting **All resources** on the left-side menu.</span></span>

![Obwody widoku](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

<span data-ttu-id="e551d-141">**Wyświetl właściwości**</span><span class="sxs-lookup"><span data-stu-id="e551d-141">**View the properties**</span></span>

    You can view the properties of the circuit by selecting it. On this blade, note the service key for the circuit. You must copy the circuit key for your circuit and pass it down to the service provider to complete the provisioning process. The circuit key is specific to your circuit.

![Wyświetl właściwości](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="e551d-143">4. Wyślij klucz usługi do dostawcą połączenia do inicjowania obsługi</span><span class="sxs-lookup"><span data-stu-id="e551d-143">4. Send the service key to your connectivity provider for provisioning</span></span>
<span data-ttu-id="e551d-144">W tym bloku **stan dostawcy** zawiera informacje o bieżącym stanie inicjowania obsługi administracyjnej po stronie dostawcy usług.</span><span class="sxs-lookup"><span data-stu-id="e551d-144">On this blade, **Provider status** provides information on the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="e551d-145">**Stan obwodu** zapewnia stanu po stronie firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e551d-145">**Circuit status** provides the state on the Microsoft side.</span></span> <span data-ttu-id="e551d-146">Aby uzyskać więcej informacji na temat obwodu inicjowania obsługi administracyjnej stanów zobacz [przepływy pracy](expressroute-workflows.md#expressroute-circuit-provisioning-states) artykułu.</span><span class="sxs-lookup"><span data-stu-id="e551d-146">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="e551d-147">Podczas tworzenia nowego obwodu ExpressRoute obwodu będą w następującym stanie:</span><span class="sxs-lookup"><span data-stu-id="e551d-147">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span></span>

<span data-ttu-id="e551d-148">Stan dostawcy: nie zainicjowano obsługę administracyjną</span><span class="sxs-lookup"><span data-stu-id="e551d-148">Provider status: Not provisioned</span></span><BR>
<span data-ttu-id="e551d-149">Stan obwodu: włączone</span><span class="sxs-lookup"><span data-stu-id="e551d-149">Circuit status: Enabled</span></span>

![Zainicjuj proces inicjowania obsługi administracyjnej](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

<span data-ttu-id="e551d-151">Obwodu zmieni się na następujący stan, gdy trwa jej włączanie dostawca połączenia:</span><span class="sxs-lookup"><span data-stu-id="e551d-151">The circuit will change to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

<span data-ttu-id="e551d-152">Stan dostawcy: Inicjowanie obsługi administracyjnej</span><span class="sxs-lookup"><span data-stu-id="e551d-152">Provider status: Provisioning</span></span><BR>
<span data-ttu-id="e551d-153">Stan obwodu: włączone</span><span class="sxs-lookup"><span data-stu-id="e551d-153">Circuit status: Enabled</span></span>

<span data-ttu-id="e551d-154">Dla Ciebie można było używać obwodu usługi ExpressRoute musi być w następującym stanie:</span><span class="sxs-lookup"><span data-stu-id="e551d-154">For you to be able to use an ExpressRoute circuit, it must be in the following state:</span></span>

<span data-ttu-id="e551d-155">Stan dostawcy: zainicjowano obsługę administracyjną</span><span class="sxs-lookup"><span data-stu-id="e551d-155">Provider status: Provisioned</span></span><BR>
<span data-ttu-id="e551d-156">Stan obwodu: włączone</span><span class="sxs-lookup"><span data-stu-id="e551d-156">Circuit status: Enabled</span></span>

### <a name="5-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="e551d-157">5. Okresowo sprawdzać stan i stan klucz obwodu</span><span class="sxs-lookup"><span data-stu-id="e551d-157">5. Periodically check the status and the state of the circuit key</span></span>
<span data-ttu-id="e551d-158">Można wyświetlić właściwości obwodu, w którym są zainteresowani przez zaznaczenie go.</span><span class="sxs-lookup"><span data-stu-id="e551d-158">You can view the properties of the circuit that you're interested in by selecting it.</span></span> <span data-ttu-id="e551d-159">Sprawdź **stan dostawcy** i upewnij się, że została przeniesiona do **obsługiwane administracyjnie** przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="e551d-159">Check the **Provider status** and ensure that it has moved to **Provisioned** before you continue.</span></span>

![Stan obwodu i dostawcy](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a><span data-ttu-id="e551d-161">6. Tworzenie konfiguracji routingu</span><span class="sxs-lookup"><span data-stu-id="e551d-161">6. Create your routing configuration</span></span>
<span data-ttu-id="e551d-162">Aby uzyskać instrukcje, zapoznaj się [obwodu ExpressRoute konfiguracji routingu](expressroute-howto-routing-portal-resource-manager.md) artykułu do tworzenia i modyfikowania obwodu komunikacji równorzędnych.</span><span class="sxs-lookup"><span data-stu-id="e551d-162">For step-by-step instructions, refer to the [ExpressRoute circuit routing configuration](expressroute-howto-routing-portal-resource-manager.md) article to create and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e551d-163">Te instrukcje dotyczą tylko obwody, które zostały utworzone z dostawców usług, które oferują warstwy 2 łączności usługi.</span><span class="sxs-lookup"><span data-stu-id="e551d-163">These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="e551d-164">Jeśli używasz usługodawcy, który oferuje zarządzanych warstwy 3 usługi (zazwyczaj IP sieci VPN, takie jak MPLS), dostawca połączenia będzie Konfigurowanie i zarządzanie nimi routingu dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="e551d-164">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="7-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="e551d-165">7. Łączenie sieci wirtualnej z obwodem usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e551d-165">7. Link a virtual network to an ExpressRoute circuit</span></span>
<span data-ttu-id="e551d-166">Następnie połączyć sieć wirtualną obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e551d-166">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="e551d-167">Użyj [łączenia sieci wirtualne obwody usługi ExpressRoute](expressroute-howto-linkvnet-arm.md) artykuł podczas pracy z modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e551d-167">Use the [Linking virtual networks to ExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with the Resource Manager deployment model.</span></span>

## <a name="getting-the-status-of-an-expressroute-circuit"></a><span data-ttu-id="e551d-168">Pobieranie stanu obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e551d-168">Getting the status of an ExpressRoute circuit</span></span>
<span data-ttu-id="e551d-169">Stan obwodu można wyświetlić, wybierając go.</span><span class="sxs-lookup"><span data-stu-id="e551d-169">You can view the status of a circuit by selecting it.</span></span> 

![Stan obwodu usługi ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="e551d-171">Modyfikowanie obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e551d-171">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="e551d-172">Można zmodyfikować niektórych właściwości obwodu usługi ExpressRoute, bez wywierania wpływu na łączność.</span><span class="sxs-lookup"><span data-stu-id="e551d-172">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="e551d-173">Można wykonać następujące czynności bez przestojów:</span><span class="sxs-lookup"><span data-stu-id="e551d-173">You can do the following with no downtime:</span></span>

* <span data-ttu-id="e551d-174">Włącz lub Wyłącz dodatek premium usługi ExpressRoute dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e551d-174">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="e551d-175">Zwiększyć przepustowość obwodu ExpressRoute dostarczane na port jest dostępna pojemność.</span><span class="sxs-lookup"><span data-stu-id="e551d-175">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="e551d-176">Należy pamiętać, że przepustowość obwodu zmiana wersji na starszą nie jest obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="e551d-176">Note that downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="e551d-177">Zmiana zliczania planu naliczane danych nieograniczone danych.</span><span class="sxs-lookup"><span data-stu-id="e551d-177">Change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="e551d-178">Należy pamiętać, że zmiana zliczania planu z dane nieograniczone naliczane danych nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="e551d-178">Note that changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="e551d-179">Można włączyć lub wyłączyć *operacje klasycznego*.</span><span class="sxs-lookup"><span data-stu-id="e551d-179">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="e551d-180">Aby uzyskać więcej informacji na limity i ograniczenia dotyczą [ExpressRoute — często zadawane pytania](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="e551d-180">For more information on limits and limitations, refer to the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

<span data-ttu-id="e551d-181">Aby zmodyfikować obwodu usługi ExpressRoute, wybierz polecenie **konfiguracji** jak pokazano na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="e551d-181">To modify an ExpressRoute circuit, click on the **Configuration** as shown in the figure below.</span></span>

![Modyfikowanie obwodu](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

<span data-ttu-id="e551d-183">Można modyfikować przepustowości, jednostka SKU, modelu rozliczeń i zezwala na klasycznym operacji w ramach bloku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e551d-183">You can modify the bandwidth, SKU, billing model and allow classic operations within the configuration blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e551d-184">Może być konieczne ponowne utworzenie obwodu usługi expressroute w przypadku niewystarczającego pojemności na istniejącego portu.</span><span class="sxs-lookup"><span data-stu-id="e551d-184">You may have to recreate the ExpressRoute circuit if there is inadequate capacity on the existing port.</span></span> <span data-ttu-id="e551d-185">Nie można uaktualnić obwodu, jeśli nie bez dodatkowej pojemności dostępnej w tej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="e551d-185">You cannot upgrade the circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="e551d-186">Nie można zmniejszyć przepustowość obwodu usługi ExpressRoute bez zakłóceń.</span><span class="sxs-lookup"><span data-stu-id="e551d-186">You cannot reduce the bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="e551d-187">Zmiana wersji na starszą przepustowości wymaga anulowanie zastrzeżenia obwodu ExpressRoute, a następnie Udostępnij ponownie nowy obwód usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e551d-187">Downgrading bandwidth requires you to deprovision the ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> <span data-ttu-id="e551d-188">Wyłączenie dodatku premium operacja może zakończyć się niepowodzeniem, jeśli używasz zasobów, które są większe niż co to jest dozwolone dla standardowych obwodu.</span><span class="sxs-lookup"><span data-stu-id="e551d-188">Disable premium add-on operation can fail if you're using resources that are greater than what is permitted for the standard circuit.</span></span>
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="e551d-189">Anulowania obsługi i usuwania obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e551d-189">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="e551d-190">Można usunąć obwodu usługi ExpressRoute, wybierając **usunąć** ikony.</span><span class="sxs-lookup"><span data-stu-id="e551d-190">You can delete your ExpressRoute circuit by selecting the **delete** icon.</span></span> <span data-ttu-id="e551d-191">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="e551d-191">Note the following:</span></span>

* <span data-ttu-id="e551d-192">Należy odłączyć wszystkie sieci wirtualne z obwodem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e551d-192">You must unlink all virtual networks from the ExpressRoute circuit.</span></span> <span data-ttu-id="e551d-193">Jeśli ta operacja nie powiedzie się, sprawdź, czy wszystkie sieci wirtualne są połączone z obwodem.</span><span class="sxs-lookup"><span data-stu-id="e551d-193">If this operation fails, check whether any virtual networks are linked to the circuit.</span></span>
* <span data-ttu-id="e551d-194">Jeśli dostawca usługi obwodu ExpressRoute stan inicjowania obsługi jest **inicjowania obsługi administracyjnej** lub **obsługiwane administracyjnie** należy skontaktować się z dostawcą usług na anulowanie zastrzeżenia obwód w bok.</span><span class="sxs-lookup"><span data-stu-id="e551d-194">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="e551d-195">Firma Microsoft będzie zarezerwować zasobów i obciążać Cię do czasu dostawcy usług wykonuje anulowania obsługi obwodu i powiadomienia NAS.</span><span class="sxs-lookup"><span data-stu-id="e551d-195">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="e551d-196">Jeśli usługodawca została anulowana obwodu (ustawiono dostawcę usługi stan inicjowania obsługi **nieudostępniane**) następnie można usunąć obwodu.</span><span class="sxs-lookup"><span data-stu-id="e551d-196">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span></span> <span data-ttu-id="e551d-197">Spowoduje to zatrzymanie rozliczeń dla obwodu</span><span class="sxs-lookup"><span data-stu-id="e551d-197">This will stop billing for the circuit</span></span>

## <a name="next-steps"></a><span data-ttu-id="e551d-198">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e551d-198">Next steps</span></span>
<span data-ttu-id="e551d-199">Po utworzeniu obwodu, upewnij się, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e551d-199">After you create your circuit, make sure that you do the following:</span></span>

* [<span data-ttu-id="e551d-200">Tworzenie i modyfikowanie routingu dla obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e551d-200">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-portal-resource-manager.md)
* [<span data-ttu-id="e551d-201">Link sieci wirtualnej do obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e551d-201">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

