---
title: 'Azure Active Directory Domain Services: Tworzenie lub wybieranie sieci wirtualnej | Microsoft Docs'
description: "Włączanie usługi Azure Active Directory Domain Services przy użyciu hello klasycznego portalu Azure"
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
ms.openlocfilehash: 212c741b20e846742d94f70342c4263ce8984153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a><span data-ttu-id="a529a-103">Tworzenie lub wybieranie sieci wirtualnej dla usługi Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="a529a-103">Create or select a virtual network for Azure Active Directory Domain Services</span></span>
## <a name="before-you-begin"></a><span data-ttu-id="a529a-104">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="a529a-104">Before you begin</span></span>
<span data-ttu-id="a529a-105">Odwołuje się zbyt[sieci zagadnienia dotyczące usługi Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="a529a-105">Refer too[Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>

## <a name="task-2-create-an-azure-virtual-network"></a><span data-ttu-id="a529a-106">Zadanie 2. Tworzenie sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a529a-106">Task 2: Create an Azure virtual network</span></span>
<span data-ttu-id="a529a-107">następne zadanie konfiguracji Hello jest toocreate sieci wirtualnej platformy Azure i podsieci w niej.</span><span class="sxs-lookup"><span data-stu-id="a529a-107">hello next configuration task is toocreate an Azure virtual network and a subnet within it.</span></span> <span data-ttu-id="a529a-108">Usługi Azure Active Directory Domain Services w tej podsieci możesz włączyć w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a529a-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="a529a-109">Jeśli masz istniejącą sieć wirtualną wolisz toouse, możesz pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="a529a-109">If you have an existing virtual network that you’d prefer toouse, you can skip this step.</span></span>

> [!NOTE]
> <span data-ttu-id="a529a-110">Upewnij się, że hello Azure sieci wirtualnej, Utwórz lub wybierz toouse z usług domenowych Azure Active Directory należy tooan region platformy Azure, który jest obsługiwany przez usługi Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="a529a-110">Make sure that hello Azure virtual network you create or choose toouse with Azure Active Directory Domain Services belongs tooan Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="a529a-111">tooascertain hello regiony platformy Azure, w których jest dostępna usług domenowych Azure Active Directory, zobacz [usług Azure według regionu](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="a529a-111">tooascertain hello Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
>
><span data-ttu-id="a529a-112">Zanotuj nazwę hello hello tooensure sieci wirtualnej, wybierz hello właściwą sieć, po włączeniu usług domenowych Azure Active Directory w kolejnym kroku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a529a-112">Note hello name of hello virtual network tooensure that you select hello right virtual network when you enable Azure Active Directory Domain Services in a subsequent configuration step.</span></span>


<span data-ttu-id="a529a-113">toocreate sieci wirtualnej platformy Azure w której ma zostać tooenable Azure Active Directory Domain Services, wykonaj te instrukcje konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="a529a-113">toocreate an Azure virtual network in which you want tooenable Azure Active Directory Domain Services, follow these configuration instructions:</span></span>

1. <span data-ttu-id="a529a-114">Przejdź toohello [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a529a-114">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="a529a-115">Wybierz w okienku po lewej stronie powitania **sieci**.</span><span class="sxs-lookup"><span data-stu-id="a529a-115">In hello left pane, select **Networks**.</span></span>

    <span data-ttu-id="a529a-116">![Węzeł sieci](./media/active-directory-domain-services-getting-started/networks-node.png)</span><span class="sxs-lookup"><span data-stu-id="a529a-116">![Networks node](./media/active-directory-domain-services-getting-started/networks-node.png)</span></span>  
    <span data-ttu-id="a529a-117">Witaj **sieci wirtualnych** zostanie otwarte okno.</span><span class="sxs-lookup"><span data-stu-id="a529a-117">hello **Virtual Networks** window opens.</span></span>
3. <span data-ttu-id="a529a-118">W okienku zadań hello u dołu okna hello powitania kliknij **nowy**.</span><span class="sxs-lookup"><span data-stu-id="a529a-118">In hello task pane at hello bottom of hello window, click **New**.</span></span>

    ![Okno Sieci wirtualne](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. <span data-ttu-id="a529a-120">Kliknij opcję **Usługi sieciowe**, a następnie wybierz pozycję **Sieć wirtualna**.</span><span class="sxs-lookup"><span data-stu-id="a529a-120">Click **Network Services**, and then select **Virtual Network**.</span></span>

    ![Sieć wirtualna — szybkie tworzenie](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. <span data-ttu-id="a529a-122">toocreate sieci wirtualnej, kliknij przycisk **szybkie tworzenie**.</span><span class="sxs-lookup"><span data-stu-id="a529a-122">toocreate a virtual network, click **Quick Create**.</span></span>

6. <span data-ttu-id="a529a-123">Określ **nazwa** dla wirtualnej sieci i rozważyć następujący hello:</span><span class="sxs-lookup"><span data-stu-id="a529a-123">Specify a **Name** for your virtual network, and consider doing hello following:</span></span>
    * <span data-ttu-id="a529a-124">Możesz wybrać tooconfigure **przestrzeni adresów** lub **maksymalna liczba maszyn wirtualnych** dla tej sieci.</span><span class="sxs-lookup"><span data-stu-id="a529a-124">You can choose tooconfigure **Address space** or **Maximum VM count** for this network.</span></span>
    * <span data-ttu-id="a529a-125">Możesz pozostawić hello **serwera DNS** ustawienie jako **Brak** teraz.</span><span class="sxs-lookup"><span data-stu-id="a529a-125">You can leave hello **DNS server** setting as **None** for now.</span></span> <span data-ttu-id="a529a-126">Należy zaktualizować ustawienia hello, po włączeniu usług domenowych Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a529a-126">You can update hello setting after you enable Azure Active Directory Domain Services.</span></span>
7. <span data-ttu-id="a529a-127">W hello **lokalizacji** listy rozwijanej wybierz obsługiwany region platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a529a-127">In hello **Location** drop-down list, select a supported Azure region.</span></span>  
    <span data-ttu-id="a529a-128">tooascertain hello regiony platformy Azure, w których jest dostępna usług domenowych Azure Active Directory, zobacz [usług Azure według regionu](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="a529a-128">tooascertain hello Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
8. <span data-ttu-id="a529a-129">toocreate sieci wirtualnej, kliknij przycisk **utworzyć sieć wirtualną**.</span><span class="sxs-lookup"><span data-stu-id="a529a-129">toocreate your virtual network, click **Create a Virtual Network**.</span></span>

    ![Tworzenie sieci wirtualnej dla usługi Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. <span data-ttu-id="a529a-131">Po utworzeniu sieci wirtualnej, wybierz nazwę hello hello sieci wirtualnej, a następnie kliknij hello **Konfiguruj** kartę.</span><span class="sxs-lookup"><span data-stu-id="a529a-131">After you've created a virtual network, select hello name of hello virtual network, and then click hello **Configure** tab.</span></span>

    ![Tworzenie podsieci](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. <span data-ttu-id="a529a-133">W obszarze **przestrzeniami adresów sieci wirtualnej**, kliknij przycisk **Dodaj podsieć**, a następnie określ podsieć o nazwie hello **AaddsSubnet**.</span><span class="sxs-lookup"><span data-stu-id="a529a-133">Under **virtual network address spaces**, click **add subnet**, and then specify a subnet with hello name **AaddsSubnet**.</span></span>

    ![Tworzenie podsieci dla usługi Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. <span data-ttu-id="a529a-135">toocreate hello podsieci, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="a529a-135">toocreate hello subnet, click **Save**.</span></span>


## <a name="next-step"></a><span data-ttu-id="a529a-136">Następny krok</span><span class="sxs-lookup"><span data-stu-id="a529a-136">Next step</span></span>
[<span data-ttu-id="a529a-137">Zadanie 3. Włączanie usług Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="a529a-137">Task 3: enable Azure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-enableaadds.md)
