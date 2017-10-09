---
title: "toocontrol kontroli dostępu opartej na rolach (RBAC) aaaAzure toocreate prawa dostępu i zarządzanie żądaniami obsługi | Dokumentacja firmy Microsoft"
description: "Azure toocontrol kontroli dostępu opartej na rolach (RBAC) toocreate prawa dostępu i zarządzanie żądaniami obsługi"
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: c68a699ac870fa6bf371deb8ed0424848f39acf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-based-access-control-rbac-toocontrol-access-rights-toocreate-and-manage-support-requests"></a><span data-ttu-id="9151d-103">Azure toocontrol kontroli dostępu opartej na rolach (RBAC) toocreate prawa dostępu i zarządzanie żądaniami obsługi</span><span class="sxs-lookup"><span data-stu-id="9151d-103">Azure Role-Based Access Control (RBAC) toocontrol access rights toocreate and manage support requests</span></span>

<span data-ttu-id="9151d-104">[Kontrola dostępu oparta na rolach (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) umożliwia precyzyjne zarządzanie dostępem dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9151d-104">[Role-Based Access Control (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) enables fine-grained access management for Azure.</span></span>
<span data-ttu-id="9151d-105">Obsługuje żądania tworzenia w hello portalu Azure, [portal.azure.com](https://portal.azure.com), używa toodefine modelu RBAC platformy Azure, który można utworzyć i zarządzanie żądaniami obsługi.</span><span class="sxs-lookup"><span data-stu-id="9151d-105">Support request creation in hello Azure portal, [portal.azure.com](https://portal.azure.com), uses Azure’s RBAC model toodefine who can create and manage support requests.</span></span>
<span data-ttu-id="9151d-106">Dostęp przez przypisanie hello odpowiednie RBAC roli toousers, grup i aplikacji na niektórych zakresu, który może być subskrypcji, grupy zasobów lub zasobu.</span><span class="sxs-lookup"><span data-stu-id="9151d-106">Access is granted by assigning hello appropriate RBAC role toousers, groups, and applications at a certain scope, which can be a subscription, resource group or a resource.</span></span>

<span data-ttu-id="9151d-107">Spójrzmy na przykład: jako właściciel grupy zasobów z uprawnienia do odczytu w zakresie subskrypcji hello, można zarządzać wszystkie zasoby hello w grupie zasobów hello, takie jak witryny sieci Web, maszyn wirtualnych i podsieci.</span><span class="sxs-lookup"><span data-stu-id="9151d-107">Let’s take an example: As a resource group owner with read permissions at hello subscription scope, you can manage all hello resources under hello resource group, like websites, virtual machines, and subnets.</span></span>
<span data-ttu-id="9151d-108">Jednak podczas toocreate żądania pomocy technicznej przed hello zasobu maszyny wirtualnej, wystąpi następujący błąd hello</span><span class="sxs-lookup"><span data-stu-id="9151d-108">However, when you try toocreate a support request against hello virtual machine resource, you encounter hello following error</span></span>

![Błąd subskrypcji](./media/create-manage-support-requests-using-access-control/subscription-error.png)

<span data-ttu-id="9151d-110">W przystawce Zarządzanie żądania obsługi musisz mieć uprawnienia zapisu lub roli, która ma hello obsługuje akcji Microsoft.Support/* toocreate stanie zakresu toobe hello subskrypcji i zarządzanie żądaniami obsługi.</span><span class="sxs-lookup"><span data-stu-id="9151d-110">In support request management, you need write permission or a role that has hello Support action Microsoft.Support/* at hello Subscription scope toobe able toocreate and manage support requests.</span></span>

<span data-ttu-id="9151d-111">Hello poniższego artykułu wyjaśniono, jak używać niestandardowych toocreate kontroli dostępu opartej na rolach (RBAC) platformy Azure i zarządzanie żądaniami obsługi w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9151d-111">hello following article explains how you can use Azure’s custom Role-Based Access Control (RBAC) toocreate and manage support requests in hello Azure portal.</span></span>

## <a name="getting-started"></a><span data-ttu-id="9151d-112">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="9151d-112">Getting Started</span></span>

<span data-ttu-id="9151d-113">Za pomocą powyższego przykładu hello, będzie możliwe toocreate żądania pomocy technicznej dla zasobu Jeśli niestandardową rolę RBAC subskrypcji hello zostały przypisane przez właściciela subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="9151d-113">Using hello example above, you would be able toocreate a support request for your resource if you were assigned a custom RBAC role on hello subscription by hello subscription owner.</span></span>
<span data-ttu-id="9151d-114">[Niestandardowe role RBAC](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) można tworzyć przy użyciu programu Azure PowerShell, interfejsu wiersza polecenia platformy Azure (CLI) i hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="9151d-114">[Custom RBAC roles](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) can be created using Azure PowerShell, Azure Command-Line Interface (CLI), and hello REST API.</span></span>

<span data-ttu-id="9151d-115">Właściwość Hello akcji niestandardowej roli zabezpieczeń określa hello Azure operacji toowhich hello rola przyznaje dostęp.</span><span class="sxs-lookup"><span data-stu-id="9151d-115">hello actions property of a custom role specifies hello Azure operations toowhich hello role grants access.</span></span>
<span data-ttu-id="9151d-116">toocreate niestandardowej roli zabezpieczeń do zarządzania żądania pomocy technicznej, rola hello musi mieć hello akcji Microsoft.Support/*</span><span class="sxs-lookup"><span data-stu-id="9151d-116">toocreate a custom role for support request management, hello role must have hello action Microsoft.Support/*</span></span>

<span data-ttu-id="9151d-117">Oto przykład niestandardowej roli zabezpieczeń można użyć toocreate i zarządzanie żądaniami obsługi.</span><span class="sxs-lookup"><span data-stu-id="9151d-117">Here’s an example of a custom role you can use toocreate and manage support requests.</span></span>
<span data-ttu-id="9151d-118">Firma Microsoft nazwanego tej roli "Współautor żądania pomocy technicznej" i to, jak firma Microsoft można znaleźć toohello rola niestandardowa w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="9151d-118">We’ve named this role “Support Request Contributor” and that’s how we refer toohello custom role in this article.</span></span>

``` Json
{
    "Name":  "Support Request Contributor",
    "Id":  "1f2aad59-39b0-41da-b052-2fb070bd7942",
    "IsCustom":  true,
    "Description":  "Lets you create and manage support tickets.",
    "Actions":  [
                    "Microsoft.Support/*"
                ],
    "NotActions":  [
                   ],
    "AssignableScopes":  [
                             "/"
                         ]
}
```

<span data-ttu-id="9151d-119">Wykonaj kroki hello opisane w temacie [ten film](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn jak toocreate niestandardowej roli zabezpieczeń dla Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9151d-119">Follow hello steps outlined in [this video](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn how toocreate a custom role for your subscription.</span></span>

## <a name="create-and-manage-support-requests-in-hello-azure-portal"></a><span data-ttu-id="9151d-120">Tworzenie i zarządzanie żądaniami obsługi w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9151d-120">Create and manage support requests in hello Azure portal</span></span>

<span data-ttu-id="9151d-121">Spójrzmy na przykład — Witaj właścicielem subskrypcji "Programu Visual Studio subskrypcji MSDN."</span><span class="sxs-lookup"><span data-stu-id="9151d-121">Let’s take an example – you are hello owner of Subscription "Visual Studio MSDN Subscription."</span></span>
<span data-ttu-id="9151d-122">Jan jest z elementu równorzędnego jest toosome właściciela zasobu, hello grup zasobów w ramach tej subskrypcji, która ma subskrypcji toohello uprawnienia do odczytu.</span><span class="sxs-lookup"><span data-stu-id="9151d-122">Joe is your peer who is a resource owner toosome of hello resource groups in this subscription and has read permission toohello subscription.</span></span>
<span data-ttu-id="9151d-123">Chcesz toogive dostępu tooyour równorzędnej, Jan, hello możliwości toocreate i zarządzanie biletami pomocy technicznej dla hello zasobów w ramach tej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9151d-123">You wish toogive access tooyour peer, Joe, hello ability toocreate and manage support tickets for hello resources under this subscription.</span></span>

1. <span data-ttu-id="9151d-124">pierwszym krokiem Hello jest toogo toohello subskrypcji i w obszarze "Ustawienia" można wyświetlić listę użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9151d-124">hello first step is toogo toohello subscription and under "Settings" you see a list of users.</span></span> <span data-ttu-id="9151d-125">Kliknij hello użytkownika Jan, kto ma dostęp czytnika na powitania subskrypcji i umożliwia przypisanie nowych toohim niestandardowej roli zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="9151d-125">Click hello user Joe who has reader access on hello Subscription and let’s assign a new custom role toohim.</span></span>

    ![Dodaj rolę](./media/create-manage-support-requests-using-access-control/add-role.png)

2. <span data-ttu-id="9151d-127">W bloku "Użytkownicy" hello, kliknij przycisk "Dodaj".</span><span class="sxs-lookup"><span data-stu-id="9151d-127">Click "Add" under hello "Users" blade.</span></span> <span data-ttu-id="9151d-128">Wybierz hello niestandardowej roli "Współautor żądania pomocy technicznej" z listy hello ról</span><span class="sxs-lookup"><span data-stu-id="9151d-128">Select hello custom role "Support Request Contributor" from hello list of roles</span></span>

    ![Dodaj rolę współautora pomocy technicznej](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. <span data-ttu-id="9151d-130">Po wybraniu hello Nazwa roli, kliknij przycisk "Dodaj użytkowników", a następnie wprowadź poświadczenia e-mail hello Jan.</span><span class="sxs-lookup"><span data-stu-id="9151d-130">After selecting hello role name, click "Add users" and enter hello Joe's email credentials.</span></span> <span data-ttu-id="9151d-131">Kliknij przycisk "Wybierz"</span><span class="sxs-lookup"><span data-stu-id="9151d-131">Click "Select"</span></span>

    ![Dodawanie użytkowników](./media/create-manage-support-requests-using-access-control/add-users.png)

4. <span data-ttu-id="9151d-133">Kliknij przycisk "Ok" tooproceed</span><span class="sxs-lookup"><span data-stu-id="9151d-133">Click "Ok" tooproceed</span></span>

    ![Dodaj dostęp](./media/create-manage-support-requests-using-access-control/add-access.png)

5. <span data-ttu-id="9151d-135">Spowoduje to wyświetlenie hello użytkownik z nowo dodanego rola niestandardowa "Obsługa współautora żądanie" w ramach subskrypcji hello, dla którego jesteś właścicielem hello hello</span><span class="sxs-lookup"><span data-stu-id="9151d-135">Now you see hello user with hello newly added custom role "Support Request Contributor" under hello Subscription for which you are hello owner</span></span>

    ![Użytkownik dodany](./media/create-manage-support-requests-using-access-control/user-added.png)

    <span data-ttu-id="9151d-137">Jan rejestruje się w portalu hello, widzi on hello toowhich subskrypcji, który został on dodany.</span><span class="sxs-lookup"><span data-stu-id="9151d-137">When Joe logs in hello portal, he sees hello subscription toowhich he was added.</span></span>

7. <span data-ttu-id="9151d-138">Jan klika w bloku "Pomoc i obsługa" hello "Nowe żądanie pomocy technicznej" i może utworzyć żądania pomocy technicznej dla "Programu Visual Studio Ultimate z subskrypcją MSDN"</span><span class="sxs-lookup"><span data-stu-id="9151d-138">Joe clicks "New Support request" from hello "Help and Support" blade and can create support requests for "Visual Studio Ultimate with MSDN"</span></span>

    ![Nowe żądanie pomocy technicznej](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. <span data-ttu-id="9151d-140">Klikając przycisk "Obsługuje wszystkie żądania" Jan wyświetlana lista żądań pomocy technicznej utworzonych dla tej subskrypcji hello ![przypadku widoku szczegółów](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span><span class="sxs-lookup"><span data-stu-id="9151d-140">Clicking "All support requests" Joe can see hello list of support requests created for this Subscription  ![Case details view](./media/create-manage-support-requests-using-access-control/case-details-view.png)</span></span>

## <a name="remove-support-request-access-in-hello-azure-portal"></a><span data-ttu-id="9151d-141">Usuń dostęp żądania pomocy technicznej w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9151d-141">Remove support request access in hello Azure portal</span></span>

<span data-ttu-id="9151d-142">Tak samo, jak to możliwe toogrant dostępu tooa użytkownika toocreate i zarządzanie żądaniami obsługi, jest możliwe tooremove dostępu dla użytkownika hello również.</span><span class="sxs-lookup"><span data-stu-id="9151d-142">Just as it is possible toogrant access tooa user toocreate and manage support requests, it's possible tooremove access for hello user as well.</span></span>
<span data-ttu-id="9151d-143">tooremove hello toocreate możliwości i zarządzanie żądaniami obsługi, przejdź toohello subskrypcji, kliknij pozycję "Ustawienia" i kliknij przycisk hello użytkownika (w tym przypadku Jan).</span><span class="sxs-lookup"><span data-stu-id="9151d-143">tooremove hello ability toocreate and manage support requests, go toohello Subscription, click "Settings" and click hello user (in this case, Joe).</span></span>
<span data-ttu-id="9151d-144">Kliknij prawym przyciskiem myszy nazwę roli Witaj, "Współautora żądania pomocy technicznej" i kliknij przycisk Usuń,</span><span class="sxs-lookup"><span data-stu-id="9151d-144">Right-click hello role name, "Support Request Contributor" and click "Remove"</span></span>

![Usuń obsługę żądania dostępu](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

<span data-ttu-id="9151d-146">Gdy Jan dzienniki w portalu toohello i próbuje toocreate żądania pomocy technicznej, wykryje on hello następujący błąd</span><span class="sxs-lookup"><span data-stu-id="9151d-146">When Joe logs in toohello portal and tries toocreate a support request, he encounters hello following error</span></span>

![Subskrypcja błąd-2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

<span data-ttu-id="9151d-148">Jan nie widzą żadnych obsługuje żądania, po kliknięciu przycisku "Obsługuje wszystkie żądania"</span><span class="sxs-lookup"><span data-stu-id="9151d-148">Joe cannot see any support requests when he clicks "All support requests"</span></span>

![Wyświetl szczegóły sprawy-2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
