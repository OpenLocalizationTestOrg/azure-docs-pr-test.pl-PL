---
title: 'Azure Active Directory Domain Services: Tworzenie lub wybieranie sieci wirtualnej | Microsoft Docs'
description: "Włączanie usług Azure Active Directory Domain Services przy użyciu klasycznej witryny Azure Portal"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 13ab1608-e3d8-40de-9f7b-9b5b42199af4
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 457519b00b65b0157effe2d4aba033a1c99852e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a><span data-ttu-id="a4cbb-103">Tworzenie lub wybieranie sieci wirtualnej dla usługi Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="a4cbb-103">Create or select a virtual network for Azure Active Directory Domain Services</span></span>
## <a name="before-you-begin"></a><span data-ttu-id="a4cbb-104">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="a4cbb-104">Before you begin</span></span>
<span data-ttu-id="a4cbb-105">Zapoznaj się z tematem [Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md) (Zagadnienia dotyczące sieci w usłudze Azure Active Directory Domain Services).</span><span class="sxs-lookup"><span data-stu-id="a4cbb-105">Refer to [Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>

## <a name="task-2-create-an-azure-virtual-network"></a><span data-ttu-id="a4cbb-106">Zadanie 2. Tworzenie sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a4cbb-106">Task 2: Create an Azure virtual network</span></span>
<span data-ttu-id="a4cbb-107">Kolejnym zadaniem konfiguracji jest utworzenie sieci wirtualnej platformy Azure oraz podsieci w tej sieci.</span><span class="sxs-lookup"><span data-stu-id="a4cbb-107">The next configuration task is to create an Azure virtual network and a subnet within it.</span></span> <span data-ttu-id="a4cbb-108">Usługi Azure Active Directory Domain Services w tej podsieci możesz włączyć w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a4cbb-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="a4cbb-109">Jeśli masz istniejącą sieć wirtualną, której chcesz użyć, możesz pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="a4cbb-109">If you have an existing virtual network that you’d prefer to use, you can skip this step.</span></span>

> [!NOTE]
> <span data-ttu-id="a4cbb-110">Upewnij się, że sieć wirtualna platformy Azure utworzona lub wybrana do użycia z usługami Azure Active Directory Domain Services należy do regionu świadczenia usługi Azure, który jest obsługiwany przez usługi Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="a4cbb-110">Make sure that the Azure virtual network you create or choose to use with Azure Active Directory Domain Services belongs to an Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="a4cbb-111">Zobacz [Usługi platformy Azure uporządkowane według regionów](https://azure.microsoft.com/regions/#services/), aby upewnić się co do regionów świadczenia usługi Azure, w których usługa Azure Active Directory Domain Services jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="a4cbb-111">To ascertain the Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
>
><span data-ttu-id="a4cbb-112">Zapamiętaj nazwę sieci wirtualnej, aby podczas włączania usług Azure Active Directory Domain Services w kolejnym kroku konfiguracji wybrać właściwą sieć.</span><span class="sxs-lookup"><span data-stu-id="a4cbb-112">Note the name of the virtual network to ensure that you select the right virtual network when you enable Azure Active Directory Domain Services in a subsequent configuration step.</span></span>


<span data-ttu-id="a4cbb-113">Aby utworzyć sieć wirtualną platformy Azure, w której chcesz włączyć usługi Azure Active Directory Domain Services, wykonaj następujące instrukcje dotyczące konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="a4cbb-113">To create an Azure virtual network in which you want to enable Azure Active Directory Domain Services, follow these configuration instructions:</span></span>

1. <span data-ttu-id="a4cbb-114">Przejdź do [klasycznej witryny Azure Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a4cbb-114">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="a4cbb-115">W lewym okienku wybierz opcję **Sieci**.</span><span class="sxs-lookup"><span data-stu-id="a4cbb-115">In the left pane, select **Networks**.</span></span>

    <span data-ttu-id="a4cbb-116">![Węzeł sieci](./media/active-directory-domain-services-getting-started/networks-node.png)</span><span class="sxs-lookup"><span data-stu-id="a4cbb-116">![Networks node](./media/active-directory-domain-services-getting-started/networks-node.png)</span></span>  
    <span data-ttu-id="a4cbb-117">Zostanie otwarte okno **Sieci wirtualne**.</span><span class="sxs-lookup"><span data-stu-id="a4cbb-117">The **Virtual Networks** window opens.</span></span>
3. <span data-ttu-id="a4cbb-118">Na pasku zadań u dołu okna kliknij opcję **Nowy**.</span><span class="sxs-lookup"><span data-stu-id="a4cbb-118">In the task pane at the bottom of the window, click **New**.</span></span>

    ![Okno Sieci wirtualne](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. <span data-ttu-id="a4cbb-120">Kliknij opcję **Usługi sieciowe**, a następnie wybierz pozycję **Sieć wirtualna**.</span><span class="sxs-lookup"><span data-stu-id="a4cbb-120">Click **Network Services**, and then select **Virtual Network**.</span></span>

    ![Sieć wirtualna — szybkie tworzenie](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. <span data-ttu-id="a4cbb-122">Kliknij pozycję **Szybkie tworzenie** w celu utworzenia sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a4cbb-122">To create a virtual network, click **Quick Create**.</span></span>

6. <span data-ttu-id="a4cbb-123">Określ nazwę sieci wirtualnej w polu **Nazwa** i rozważ wykonanie następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="a4cbb-123">Specify a **Name** for your virtual network, and consider doing the following:</span></span>
    * <span data-ttu-id="a4cbb-124">Możesz skonfigurować wartości **Przestrzeń adresowa** lub **Maksymalna liczba maszyn wirtualnych** dla sieci.</span><span class="sxs-lookup"><span data-stu-id="a4cbb-124">You can choose to configure **Address space** or **Maximum VM count** for this network.</span></span>
    * <span data-ttu-id="a4cbb-125">Na razie dla ustawienia **Serwer DNS** można zostawić wartość **Brak**.</span><span class="sxs-lookup"><span data-stu-id="a4cbb-125">You can leave the **DNS server** setting as **None** for now.</span></span> <span data-ttu-id="a4cbb-126">Ustawienia możesz zaktualizować po włączeniu usług Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="a4cbb-126">You can update the setting after you enable Azure Active Directory Domain Services.</span></span>
7. <span data-ttu-id="a4cbb-127">Na liście rozwijanej **Lokalizacja** wybierz obsługiwany region świadczenia usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="a4cbb-127">In the **Location** drop-down list, select a supported Azure region.</span></span>  
    <span data-ttu-id="a4cbb-128">Zobacz [Usługi platformy Azure uporządkowane według regionów](https://azure.microsoft.com/regions/#services/), aby upewnić się co do regionów świadczenia usługi Azure, w których usługa Azure Active Directory Domain Services jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="a4cbb-128">To ascertain the Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
8. <span data-ttu-id="a4cbb-129">Kliknij przycisk **Utwórz sieć wirtualną**, aby utworzyć sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="a4cbb-129">To create your virtual network, click **Create a Virtual Network**.</span></span>

    ![Tworzenie sieci wirtualnej dla usługi Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. <span data-ttu-id="a4cbb-131">Po utworzeniu sieci wirtualnej wybierz nazwę sieci wirtualnej, a następnie kliknij kartę **Konfiguracja**.</span><span class="sxs-lookup"><span data-stu-id="a4cbb-131">After you've created a virtual network, select the name of the virtual network, and then click the **Configure** tab.</span></span>

    ![Tworzenie podsieci](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. <span data-ttu-id="a4cbb-133">W części **Przestrzenie adresowe sieci wirtualnych** kliknij pozycję **Dodaj podsieć**, a następnie określ podsieć o nazwie **AaddsSubnet**.</span><span class="sxs-lookup"><span data-stu-id="a4cbb-133">Under **virtual network address spaces**, click **add subnet**, and then specify a subnet with the name **AaddsSubnet**.</span></span>

    ![Tworzenie podsieci dla usługi Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. <span data-ttu-id="a4cbb-135">Kliknij przycisk **Zapisz**, aby utworzyć podsieć.</span><span class="sxs-lookup"><span data-stu-id="a4cbb-135">To create the subnet, click **Save**.</span></span>


## <a name="next-step"></a><span data-ttu-id="a4cbb-136">Następny krok</span><span class="sxs-lookup"><span data-stu-id="a4cbb-136">Next step</span></span>
[<span data-ttu-id="a4cbb-137">Zadanie 3. Włączanie usług Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="a4cbb-137">Task 3: enable Azure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-enableaadds.md)
