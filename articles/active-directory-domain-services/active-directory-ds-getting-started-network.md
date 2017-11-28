---
title: "Usług domenowych Azure Active Directory: Wprowadzenie | Dokumentacja firmy Microsoft"
description: "Włączanie usługi Azure Active Directory Domain Services przy użyciu hello portalu Azure (wersja zapoznawcza)"
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
ms.openlocfilehash: 7695dabb11df8d9dcfdac24996edf021af2e7f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="87755-103">Włączanie usługi Azure Active Directory Domain Services przy użyciu hello portalu Azure (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="87755-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="87755-104">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="87755-104">Before you begin</span></span>
<span data-ttu-id="87755-105">Odwołuje się zbyt[sieci zagadnienia dotyczące usługi Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="87755-105">Refer too[Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>


## <a name="task-2-configure-network-settings"></a><span data-ttu-id="87755-106">Zadanie 2: Konfigurowanie ustawień sieciowych</span><span class="sxs-lookup"><span data-stu-id="87755-106">Task 2: configure network settings</span></span>
<span data-ttu-id="87755-107">następne zadanie konfiguracji Hello jest toocreate sieci wirtualnej platformy Azure i dedykowanych podsieci w niej.</span><span class="sxs-lookup"><span data-stu-id="87755-107">hello next configuration task is toocreate an Azure virtual network and a dedicated subnet within it.</span></span> <span data-ttu-id="87755-108">Usługi Azure Active Directory Domain Services w tej podsieci możesz włączyć w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="87755-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="87755-109">Może również wybierają istniejącej sieci wirtualnej i Utwórz podsieć hello dedykowanego w niej.</span><span class="sxs-lookup"><span data-stu-id="87755-109">You may also pick an existing virtual network and create hello dedicated subnet within it.</span></span>

1. <span data-ttu-id="87755-110">Kliknij przycisk **sieci wirtualnej** tooselect sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="87755-110">Click **Virtual network** tooselect a virtual network.</span></span>
2. <span data-ttu-id="87755-111">Na powitania **sieci wirtualnej wybierz** bloku, zobacz wszystkie istniejące sieci wirtualne.</span><span class="sxs-lookup"><span data-stu-id="87755-111">On hello **Choose virtual network** blade, you see all existing virtual networks.</span></span> <span data-ttu-id="87755-112">Zostanie wyświetlony tylko hello sieci wirtualne, które należy toohello lokalizacji i grupy zasobów platformy Azure wybranego na powitania **podstawy** strony kreatora.</span><span class="sxs-lookup"><span data-stu-id="87755-112">You see only hello virtual networks that belong toohello resource group and Azure location you have selected on hello **Basics** wizard page.</span></span>

3. <span data-ttu-id="87755-113">Wybierz sieć wirtualną hello, w którym można włączyć usługi domenowe Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87755-113">Choose hello virtual network in which Azure AD Domain Services should be enabled.</span></span> <span data-ttu-id="87755-114">Kliknij przycisk **Utwórz nowy**, jeśli wolisz toocreate nowej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="87755-114">Click **Create new**, if you prefer toocreate a new virtual network.</span></span> <span data-ttu-id="87755-115">Zdecydowanie zaleca się za pomocą dedykowanego podsieci dla usług domenowych Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87755-115">We highly recommend using a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="87755-116">W przypadku wybrania istniejącej sieci wirtualnej, [Utwórz dedykowane podsieć przy użyciu rozszerzenia sieci wirtualnych hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) , a następnie wybierz tej podsieci.</span><span class="sxs-lookup"><span data-stu-id="87755-116">If you pick an existing virtual network, [create a dedicated subnet using hello virtual networks extension](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) and then pick that subnet.</span></span> 

    ![Wybierz sieć wirtualną](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. <span data-ttu-id="87755-118">Kliknij przycisk **podsieci** toopick hello dedykowanych podsieci w tej sieci wirtualnej w ramach których tooenable nowego zarządzanego domeny.</span><span class="sxs-lookup"><span data-stu-id="87755-118">Click **Subnet** toopick hello dedicated subnet in this virtual network, within which tooenable your new managed domain.</span></span> <span data-ttu-id="87755-119">W hello **Utwórz podsieć** bloku, określ nazwę hello podsieci, a następnie kliknij przycisk **OK** po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="87755-119">In hello **Create subnet** blade, specify a name for hello subnet, and click **OK** when you're done.</span></span> <span data-ttu-id="87755-120">Na przykład utworzyć podsieć o nazwie hello "DomainServices", dzięki czemu toounderstand innych administratorów co to jest wdrażana w obrębie podsieci hello.</span><span class="sxs-lookup"><span data-stu-id="87755-120">For example, create a subnet with hello name 'DomainServices', making it easy for other administrators toounderstand what is deployed within hello subnet.</span></span>

    ![Wybierz podsieć w sieci wirtualnej hello](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > <span data-ttu-id="87755-122">**Wskazówki dotyczące wybierania podsieci**</span><span class="sxs-lookup"><span data-stu-id="87755-122">**Guidelines for selecting a subnet**</span></span>
  > 1. <span data-ttu-id="87755-123">Użyj dedykowanych podsieci dla usług domenowych Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87755-123">Use a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="87755-124">Nie należy wdrażać innych podsieci toothis maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="87755-124">Do not deploy any other virtual machines toothis subnet.</span></span> <span data-ttu-id="87755-125">Taka konfiguracja pozwala tooconfigure sieciowych grup zabezpieczeń (NSG) dla maszyn wirtualnych/obciążeń bez przerywania Twojej domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="87755-125">This configuration enables you tooconfigure network security groups (NSGs) for your workloads/virtual machines without disrupting your managed domain.</span></span> <span data-ttu-id="87755-126">Aby uzyskać więcej informacji, zobacz [sieci zagadnienia dotyczące usługi Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="87755-126">For details, see [networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>
  2. <span data-ttu-id="87755-127">Nie zaznaczaj hello podsieci bramy do wdrażania usług domenowych Azure AD, ponieważ nie jest obsługiwana konfiguracja.</span><span class="sxs-lookup"><span data-stu-id="87755-127">Do not select hello Gateway subnet for deploying Azure AD Domain Services, because it is not a supported configuration.</span></span>
  3. <span data-ttu-id="87755-128">Upewnij się, że wybrane podsieci hello jest wystarczająca ilość miejsca dostępnego adresu — co najmniej 3 – 5 dostępnych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="87755-128">Ensure that hello subnet you've selected has sufficient available address space - at least 3-5 available IP addresses.</span></span>
  >

5. <span data-ttu-id="87755-129">Gdy wszystko będzie gotowe, kliknij przycisk **OK** toomove na toohello **grupy administratorów** hello kreatora.</span><span class="sxs-lookup"><span data-stu-id="87755-129">When you are done, click **OK** toomove on toohello **Administrator group** page of hello wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="87755-130">Następny krok</span><span class="sxs-lookup"><span data-stu-id="87755-130">Next step</span></span>
[<span data-ttu-id="87755-131">Zadanie 3: Konfigurowanie grupy administracyjnej i włączyć usługi domenowe Azure AD</span><span class="sxs-lookup"><span data-stu-id="87755-131">Task 3: configure administrative group and enable Azure AD Domain Services</span></span>](active-directory-ds-getting-started-admingroup.md)
