---
title: "Usług domenowych Azure Active Directory: Wprowadzenie | Dokumentacja firmy Microsoft"
description: "Włączanie usługi Azure Active Directory Domain Services przy użyciu portalu Azure (wersja zapoznawcza)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 7f420d60862adf61e4f21e5abac2932a742bd55d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="ae007-103">Włączanie usługi Azure Active Directory Domain Services przy użyciu portalu Azure (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="ae007-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="ae007-104">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="ae007-104">Before you begin</span></span>
<span data-ttu-id="ae007-105">Zapoznaj się z tematem [Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md) (Zagadnienia dotyczące sieci w usłudze Azure Active Directory Domain Services).</span><span class="sxs-lookup"><span data-stu-id="ae007-105">Refer to [Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>


## <a name="task-2-configure-network-settings"></a><span data-ttu-id="ae007-106">Zadanie 2: Konfigurowanie ustawień sieciowych</span><span class="sxs-lookup"><span data-stu-id="ae007-106">Task 2: configure network settings</span></span>
<span data-ttu-id="ae007-107">Następne zadanie konfiguracji to aby utworzyć sieć wirtualną platformy Azure i dedykowanych podsieci w niej.</span><span class="sxs-lookup"><span data-stu-id="ae007-107">The next configuration task is to create an Azure virtual network and a dedicated subnet within it.</span></span> <span data-ttu-id="ae007-108">Usługi Azure Active Directory Domain Services w tej podsieci możesz włączyć w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ae007-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="ae007-109">Może również wybierają istniejącej sieci wirtualnej i Utwórz dedykowane podsieć w niej.</span><span class="sxs-lookup"><span data-stu-id="ae007-109">You may also pick an existing virtual network and create the dedicated subnet within it.</span></span>

1. <span data-ttu-id="ae007-110">Kliknij przycisk **sieci wirtualnej** do wybrania sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ae007-110">Click **Virtual network** to select a virtual network.</span></span>
2. <span data-ttu-id="ae007-111">Na **sieci wirtualnej wybierz** bloku, zobacz wszystkie istniejące sieci wirtualne.</span><span class="sxs-lookup"><span data-stu-id="ae007-111">On the **Choose virtual network** blade, you see all existing virtual networks.</span></span> <span data-ttu-id="ae007-112">Zostanie wyświetlony tylko sieci wirtualnych, które należą do grupy zasobów i lokalizacja platformy Azure, wybranego na **podstawy** strony kreatora.</span><span class="sxs-lookup"><span data-stu-id="ae007-112">You see only the virtual networks that belong to the resource group and Azure location you have selected on the **Basics** wizard page.</span></span>

3. <span data-ttu-id="ae007-113">Wybierz sieć wirtualną, w którym można włączyć usługi domenowe Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae007-113">Choose the virtual network in which Azure AD Domain Services should be enabled.</span></span> <span data-ttu-id="ae007-114">Kliknij przycisk **Utwórz nowy**, aby utworzyć nową sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="ae007-114">Click **Create new**, if you prefer to create a new virtual network.</span></span> <span data-ttu-id="ae007-115">Zdecydowanie zaleca się za pomocą dedykowanego podsieci dla usług domenowych Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae007-115">We highly recommend using a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="ae007-116">W przypadku wybrania istniejącej sieci wirtualnej, [Utwórz dedykowane podsieć przy użyciu rozszerzenia sieci wirtualnych](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) , a następnie wybierz tej podsieci.</span><span class="sxs-lookup"><span data-stu-id="ae007-116">If you pick an existing virtual network, [create a dedicated subnet using the virtual networks extension](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) and then pick that subnet.</span></span> 

    ![Wybierz sieć wirtualną](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. <span data-ttu-id="ae007-118">Kliknij przycisk **podsieci** pobrania dedykowanych podsieci w tej sieci wirtualnej, w którym można włączyć nowe domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="ae007-118">Click **Subnet** to pick the dedicated subnet in this virtual network, within which to enable your new managed domain.</span></span> <span data-ttu-id="ae007-119">W **Utwórz podsieć** bloku, określ nazwę dla tej podsieci, a następnie kliknij przycisk **OK** po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="ae007-119">In the **Create subnet** blade, specify a name for the subnet, and click **OK** when you're done.</span></span> <span data-ttu-id="ae007-120">Na przykład utworzyć podsieć o nazwie "DomainServices", dzięki czemu można łatwo dla innych administratorów zrozumieć, co jest wdrażana w obrębie podsieci.</span><span class="sxs-lookup"><span data-stu-id="ae007-120">For example, create a subnet with the name 'DomainServices', making it easy for other administrators to understand what is deployed within the subnet.</span></span>

    ![Wybierz podsieć w sieci wirtualnej](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > <span data-ttu-id="ae007-122">**Wskazówki dotyczące wybierania podsieci**</span><span class="sxs-lookup"><span data-stu-id="ae007-122">**Guidelines for selecting a subnet**</span></span>
  > 1. <span data-ttu-id="ae007-123">Użyj dedykowanych podsieci dla usług domenowych Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae007-123">Use a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="ae007-124">Nie należy wdrażać innych maszyn wirtualnych do tej podsieci.</span><span class="sxs-lookup"><span data-stu-id="ae007-124">Do not deploy any other virtual machines to this subnet.</span></span> <span data-ttu-id="ae007-125">Ta konfiguracja umożliwia konfigurowanie grup zabezpieczeń sieci (NSG) dla maszyn wirtualnych/obciążeń bez przerywania Twojej domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="ae007-125">This configuration enables you to configure network security groups (NSGs) for your workloads/virtual machines without disrupting your managed domain.</span></span> <span data-ttu-id="ae007-126">Aby uzyskać więcej informacji, zobacz [sieci zagadnienia dotyczące usługi Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="ae007-126">For details, see [networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>
  2. <span data-ttu-id="ae007-127">Nie zaznaczaj podsieci bramy do wdrażania usług domenowych Azure AD, ponieważ nie jest obsługiwana konfiguracja.</span><span class="sxs-lookup"><span data-stu-id="ae007-127">Do not select the Gateway subnet for deploying Azure AD Domain Services, because it is not a supported configuration.</span></span>
  3. <span data-ttu-id="ae007-128">Upewnij się, że wybrane podsieci ma wystarczającą ilość miejsca dostępnego adresu — co najmniej 3 – 5 dostępnych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="ae007-128">Ensure that the subnet you've selected has sufficient available address space - at least 3-5 available IP addresses.</span></span>
  >

5. <span data-ttu-id="ae007-129">Gdy wszystko będzie gotowe, kliknij przycisk **OK** można przenieść do **grupy administratorów** stronie kreatora.</span><span class="sxs-lookup"><span data-stu-id="ae007-129">When you are done, click **OK** to move on to the **Administrator group** page of the wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="ae007-130">Następny krok</span><span class="sxs-lookup"><span data-stu-id="ae007-130">Next step</span></span>
[<span data-ttu-id="ae007-131">Zadanie 3: Konfigurowanie grupy administracyjnej i włączyć usługi domenowe Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae007-131">Task 3: configure administrative group and enable Azure AD Domain Services</span></span>](active-directory-ds-getting-started-admingroup.md)
