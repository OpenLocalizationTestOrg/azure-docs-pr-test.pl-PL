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
ms.date: 08/28/2017
ms.author: maheshu
ms.openlocfilehash: 79cbb21c4a50194f5ad8ca1a4a8493ee4a260a9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="940ae-103">Włączanie usługi Azure Active Directory Domain Services przy użyciu hello portalu Azure (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="940ae-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>
<span data-ttu-id="940ae-104">W tym artykule opisano, jak tooenable Azure usług domenowych Active Directory (Azure AD DS) za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="940ae-104">This article shows how tooenable Azure Active Directory Domain Services (Azure AD DS) using hello Azure portal.</span></span>


<span data-ttu-id="940ae-105">Witaj toolaunch **usług włączyć domenowych Azure AD** pełną, Kreator hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="940ae-105">toolaunch hello **Enable Azure AD Domain Services** wizard, complete hello following steps:</span></span>

1. <span data-ttu-id="940ae-106">Przejdź toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="940ae-106">Go toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="940ae-107">W okienku po lewej stronie powitania kliknij **nowy**.</span><span class="sxs-lookup"><span data-stu-id="940ae-107">In hello left pane, click on **New**.</span></span>
3. <span data-ttu-id="940ae-108">W hello **nowy** bloku, typ **usług domenowych w usłudze** na powitania pasek wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="940ae-108">In hello **New** blade, type **Domain Services** into hello search bar.</span></span>

    ![Wyszukaj usług domenowych w usłudze](./media/getting-started/search-domain-services.png)

4. <span data-ttu-id="940ae-110">Kliknij przycisk tooselect **usług domenowych Azure AD** z listy hello sugestie dotyczące wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="940ae-110">Click tooselect **Azure AD Domain Services** from hello list of search suggestions.</span></span> <span data-ttu-id="940ae-111">Na powitania **usług domenowych Azure AD** bloku, kliknij przycisk hello **Utwórz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="940ae-111">On hello **Azure AD Domain Services** blade, click hello **Create** button.</span></span>

    ![Blok usług domenowych](./media/getting-started/domain-services-blade.png)

5. <span data-ttu-id="940ae-113">Witaj **usług włączyć domenowych Azure AD** uruchomić kreatora.</span><span class="sxs-lookup"><span data-stu-id="940ae-113">hello **Enable Azure AD Domain Services** wizard is launched.</span></span>


## <a name="task-1-configure-basic-settings"></a><span data-ttu-id="940ae-114">Zadanie 1: Konfigurowanie ustawień podstawowych</span><span class="sxs-lookup"><span data-stu-id="940ae-114">Task 1: configure basic settings</span></span>
<span data-ttu-id="940ae-115">W hello **podstawy** strony kreatora hello, można określić hello domeny DNS dla domeny zarządzanej hello.</span><span class="sxs-lookup"><span data-stu-id="940ae-115">In hello **Basics** page of hello wizard, you can specify hello DNS domain name for hello managed domain.</span></span> <span data-ttu-id="940ae-116">Możesz również hello grupy zasobów i powinny zostać wdrożone domeny zarządzanej hello toowhich lokalizacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="940ae-116">You can also choose hello resource group and Azure location toowhich hello managed domain should be deployed.</span></span>

![Skonfiguruj podstawy](./media/getting-started/domain-services-blade-basics.png)

1. <span data-ttu-id="940ae-118">Wybierz hello **nazwy domeny DNS** dla domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="940ae-118">Choose hello **DNS domain name** for your managed domain.</span></span>

   * <span data-ttu-id="940ae-119">Domyślna nazwa domeny Hello hello katalogu (z **. onmicrosoft.com** sufiks) jest określony, domyślnie.</span><span class="sxs-lookup"><span data-stu-id="940ae-119">hello default domain name of hello directory (with a **.onmicrosoft.com** suffix) is specified by default.</span></span>

   * <span data-ttu-id="940ae-120">Możesz również wpisać w niestandardowej nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="940ae-120">You can also type in a custom domain name.</span></span> <span data-ttu-id="940ae-121">W tym przykładzie hello niestandardowa nazwa domeny jest *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="940ae-121">In this example, hello custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="940ae-122">Prefiks nazwy domeny określonej Hello (na przykład *contoso100* w hello *contoso100.com* nazwa domeny) musi zawierać więcej niż 15 znaków.</span><span class="sxs-lookup"><span data-stu-id="940ae-122">hello prefix of your specified domain name (for example, *contoso100* in hello *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="940ae-123">Nie można utworzyć domeny zarządzanej z prefiksem dłuższa niż 15 znaków.</span><span class="sxs-lookup"><span data-stu-id="940ae-123">You cannot create a managed domain with a prefix longer than 15 characters.</span></span>
     >
     >

2. <span data-ttu-id="940ae-124">Upewnij się, tym hello domeny DNS wybrana dla hello zarządzane domeny nie istnieje już w sieci wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="940ae-124">Ensure that hello DNS domain name you have chosen for hello managed domain does not already exist in hello virtual network.</span></span> <span data-ttu-id="940ae-125">W szczególności, sprawdź, czy:</span><span class="sxs-lookup"><span data-stu-id="940ae-125">Specifically, check whether:</span></span>

   * <span data-ttu-id="940ae-126">Masz już domenę z hello tą samą nazwą domeny DNS w sieci wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="940ae-126">You already have a domain with hello same DNS domain name on hello virtual network.</span></span>

   * <span data-ttu-id="940ae-127">Hello sieci wirtualnej, w którym planujesz domeny zarządzanej hello tooenable ma połączenie VPN z siecią lokalną.</span><span class="sxs-lookup"><span data-stu-id="940ae-127">hello virtual network where you plan tooenable hello managed domain has a VPN connection with your on-premises network.</span></span> <span data-ttu-id="940ae-128">W tym scenariuszu, upewnij się, nie masz domenę z hello tą samą nazwą domeny DNS w sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="940ae-128">In this scenario, ensure you don't have a domain with hello same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="940ae-129">Masz istniejącą usługę w chmurze o tej nazwie na powitania sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="940ae-129">You have an existing cloud service with that name on hello virtual network.</span></span>

3. <span data-ttu-id="940ae-130">Wybierz hello **sieć wirtualna typu**.</span><span class="sxs-lookup"><span data-stu-id="940ae-130">Choose hello **type of virtual network**.</span></span> <span data-ttu-id="940ae-131">Domyślnie program hello **Resource Manager** wybrano typ sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="940ae-131">By default, hello **Resource Manager** virtual network type is selected.</span></span> <span data-ttu-id="940ae-132">Zaleca się używanie tego typu sieci wirtualnej dla wszystkich nowo utworzony domen zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="940ae-132">We recommend using this type of virtual network for all newly created managed domains.</span></span>

4. <span data-ttu-id="940ae-133">Wybierz hello Azure **subskrypcji** w którym chcesz domeny zarządzanej hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="940ae-133">Select hello Azure **Subscription** in which you would like toocreate hello managed domain.</span></span>

5. <span data-ttu-id="940ae-134">Wybierz hello **grupy zasobów** domeny zarządzanej hello toowhich powinna należeć.</span><span class="sxs-lookup"><span data-stu-id="940ae-134">Select hello **Resource group** toowhich hello managed domain should belong.</span></span> <span data-ttu-id="940ae-135">Można wybrać obu hello **Utwórz nowy** lub **Użyj istniejącego** grupy zasobów hello tooselect opcje.</span><span class="sxs-lookup"><span data-stu-id="940ae-135">You can choose either hello **Create new** or **Use existing** options tooselect hello resource group.</span></span>

6. <span data-ttu-id="940ae-136">Wybierz hello Azure **lokalizacji** w hello, które można utworzyć domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="940ae-136">Choose hello Azure **Location** in which hello managed domain should be created.</span></span> <span data-ttu-id="940ae-137">Na powitania **sieci** strony kreatora hello Zobacz sieci tylko wirtualne, które należy lokalizacji toohello wybrano.</span><span class="sxs-lookup"><span data-stu-id="940ae-137">On hello **Network** page of hello wizard, you see only virtual networks that belong toohello location you have selected.</span></span>

7. <span data-ttu-id="940ae-138">Gdy wszystko będzie gotowe, kliknij przycisk **OK** toomove na toohello **sieci** hello kreatora.</span><span class="sxs-lookup"><span data-stu-id="940ae-138">When you are done, click **OK** toomove on toohello **Network** page of hello wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="940ae-139">Następny krok</span><span class="sxs-lookup"><span data-stu-id="940ae-139">Next step</span></span>
[<span data-ttu-id="940ae-140">Task 2: configure network settings (Zadanie 2. Konfigurowanie ustawień sieciowych)</span><span class="sxs-lookup"><span data-stu-id="940ae-140">Task 2: configure network settings</span></span>](active-directory-ds-getting-started-network.md)
