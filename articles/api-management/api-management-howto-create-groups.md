---
title: "przy użyciu grup w usłudze Azure API Management konta dewelopera aaaManage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak kont przy użyciu narzędzia Projektant toomanage grup w usłudze Azure API Management"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 33660b45-442f-44be-9a4a-1899d7f699b0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: c46e010e41d9705ae161dcd60d734a76d19c9e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-groups-toomanage-developer-accounts-in-azure-api-management"></a><span data-ttu-id="ae60b-103">Jak developer toomanage grup toocreate i używania kont w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="ae60b-103">How toocreate and use groups toomanage developer accounts in Azure API Management</span></span>
<span data-ttu-id="ae60b-104">W usłudze API Management grupy są używane toomanage widoczność hello toodevelopers produktów.</span><span class="sxs-lookup"><span data-stu-id="ae60b-104">In API Management, groups are used toomanage hello visibility of products toodevelopers.</span></span> <span data-ttu-id="ae60b-105">Produkty są pierwszy dokonano toogroups widoczne, a następnie deweloperów w tych grupach można wyświetlić i toohello produktów, które są skojarzone z grupami hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ae60b-105">Products are first made visible toogroups, and then developers in those groups can view and subscribe toohello products that are associated with hello groups.</span></span> 

<span data-ttu-id="ae60b-106">Zarządzanie interfejsami API ma hello następujące grupy systemu niezmienialny.</span><span class="sxs-lookup"><span data-stu-id="ae60b-106">API Management has hello following immutable system groups.</span></span>

* <span data-ttu-id="ae60b-107">**Administratorzy** — do tej grupy należą administratorzy subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ae60b-107">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="ae60b-108">Administratorzy Zarządzanie wystąpieniami usługi Zarządzanie interfejsami API, tworzenie hello interfejsów API, operacje i produktów, które są używane przez deweloperów.</span><span class="sxs-lookup"><span data-stu-id="ae60b-108">Administrators manage API Management service instances, creating hello APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="ae60b-109">**Deweloperzy** — do tej grupy należą uwierzytelnieni użytkownicy portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="ae60b-109">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="ae60b-110">Deweloperzy są hello klientów, którzy tworzyć aplikacje przy użyciu swoje interfejsy API.</span><span class="sxs-lookup"><span data-stu-id="ae60b-110">Developers are hello customers that build applications using your APIs.</span></span> <span data-ttu-id="ae60b-111">Deweloperzy otrzymują dostęp do portalu dla deweloperów toohello i tworzenia aplikacji wywołujących hello operacje interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="ae60b-111">Developers are granted access toohello developer portal and build applications that call hello operations of an API.</span></span>
* <span data-ttu-id="ae60b-112">**Goście** -nieuwierzytelnionych użytkowników portalu deweloperów, na przykład potencjalni klienci odwiedzający hello portalu dla deweloperów programu spadek wystąpienia interfejsu API zarządzania do tej grupy.</span><span class="sxs-lookup"><span data-stu-id="ae60b-112">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting hello developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="ae60b-113">Może zostać przydzielony niektórych dostęp tylko do odczytu, takich jak tooview możliwości hello interfejsów API, ale nie połączeń telefonicznych z nimi.</span><span class="sxs-lookup"><span data-stu-id="ae60b-113">They can be granted certain read-only access, such as hello ability tooview APIs but not call them.</span></span>

<span data-ttu-id="ae60b-114">Dodanie toothese systemu grup, Administratorzy mogą tworzyć niestandardowe grupy lub [korzystać z zewnętrznej grupy w skojarzonych dzierżaw usługi Azure Active Directory][leverage external groups in associated Azure Active Directory tenants].</span><span class="sxs-lookup"><span data-stu-id="ae60b-114">In addition toothese system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants][leverage external groups in associated Azure Active Directory tenants].</span></span> <span data-ttu-id="ae60b-115">Niestandardowe zewnętrznych grup można używać razem grup systemu w zapewniając wgląd w deweloperzy i uzyskują dostęp do tooAPI produktów.</span><span class="sxs-lookup"><span data-stu-id="ae60b-115">Custom and external groups can be used alongside system groups in giving developers visibility and access tooAPI products.</span></span> <span data-ttu-id="ae60b-116">Na przykład można utworzyć jedną grupę niestandardowych dla deweloperów powiązane z konkretną organizacji partnera i zezwolić im dostępu toohello interfejsy API z produktu, zawierający tylko odpowiednich interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="ae60b-116">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access toohello APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="ae60b-117">Użytkownik może należeć do więcej niż jednej grupy.</span><span class="sxs-lookup"><span data-stu-id="ae60b-117">A user can be a member of more than one group.</span></span>

<span data-ttu-id="ae60b-118">W tym przewodniku pokazano, jak Administratorzy wystąpienia interfejsu API zarządzania mogą dodawać nowe grupy i skojarzyć je z produktami i deweloperów.</span><span class="sxs-lookup"><span data-stu-id="ae60b-118">This guide shows how administrators of an API Management instance can add new groups and associate them with products and developers.</span></span>

> [!NOTE]
> <span data-ttu-id="ae60b-119">Ponadto toocreating grup i zarządzanie nimi w portalu wydawcy hello, możesz utworzyć i zarządzanie grupami za pomocą interfejsu API REST zarządzania interfejsu API hello [grupy](https://msdn.microsoft.com/library/azure/dn776329.aspx) jednostki.</span><span class="sxs-lookup"><span data-stu-id="ae60b-119">In addition toocreating and managing groups in hello publisher portal, you can create and manage your groups using hello API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>
> 
> 

## <span data-ttu-id="ae60b-120"><a name="create-group"></a>Utwórz grupę</span><span class="sxs-lookup"><span data-stu-id="ae60b-120"><a name="create-group"> </a>Create a group</span></span>
<span data-ttu-id="ae60b-121">toocreate nową grupę, kliknij przycisk **portal wydawcy** w hello portalu Azure usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="ae60b-121">toocreate a new group, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="ae60b-122">Trwa toohello zarządzanie interfejsami API wydawcy portalu.</span><span class="sxs-lookup"><span data-stu-id="ae60b-122">This takes you toohello API Management publisher portal.</span></span>

![Portal wydawcy][api-management-management-console]

> <span data-ttu-id="ae60b-124">Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.</span><span class="sxs-lookup"><span data-stu-id="ae60b-124">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="ae60b-125">Kliknij przycisk **grup** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij **Dodaj grupę**.</span><span class="sxs-lookup"><span data-stu-id="ae60b-125">Click **Groups** from hello **API Management** menu on hello left, and then click **Add Group**.</span></span>

![Dodaj nową grupę][api-management-add-group]

<span data-ttu-id="ae60b-127">Wprowadź unikatową nazwę grupy hello i opcjonalny opis, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="ae60b-127">Enter a unique name for hello group and an optional description, and click **Save**.</span></span>

![Dodaj nową grupę][api-management-add-group-window]

<span data-ttu-id="ae60b-129">Witaj Nowa grupa zostanie wyświetlona w hello grup kartę tooedit hello **nazwa** lub **opis** hello grupy, kliknij nazwę hello hello grupy na liście hello.</span><span class="sxs-lookup"><span data-stu-id="ae60b-129">hello new group is displayed in hello groups tab. tooedit hello **Name** or **Description** of hello group, click hello name of hello group in hello list.</span></span> <span data-ttu-id="ae60b-130">toodelete hello grupy, kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="ae60b-130">toodelete hello group, click **Delete**.</span></span>

![Grupy dodane][api-management-new-group]

<span data-ttu-id="ae60b-132">Teraz, gdy hello zostanie utworzona grupa, może być skojarzony z produktami i deweloperów.</span><span class="sxs-lookup"><span data-stu-id="ae60b-132">Now that hello group is created, it can be associated with products and developers.</span></span>

## <span data-ttu-id="ae60b-133"><a name="associate-group-product"></a>Skojarzyć grupy z produktem</span><span class="sxs-lookup"><span data-stu-id="ae60b-133"><a name="associate-group-product"> </a>Associate a group with a product</span></span>
<span data-ttu-id="ae60b-134">tooassociate grupy z produktem, kliknij przycisk **produktów** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij hello nazwa produktu żądaną hello.</span><span class="sxs-lookup"><span data-stu-id="ae60b-134">tooassociate a group with a product, click **Products** from hello **API Management** menu on hello left, and then click hello name of hello desired product.</span></span>

![Ustaw widoczność][api-management-add-group-to-product]

<span data-ttu-id="ae60b-136">Wybierz hello **widoczność** karcie tooadd i usuwanie grup oraz tooview hello bieżących grup hello produktu.</span><span class="sxs-lookup"><span data-stu-id="ae60b-136">Select hello **Visibility** tab tooadd and remove groups, and tooview hello current groups for hello product.</span></span> <span data-ttu-id="ae60b-137">tooadd lub Usuń grupy, zaznacz lub usuń zaznaczenie pola wyboru hello, dla żądanego hello grupy i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="ae60b-137">tooadd or remove groups, check or uncheck hello checkboxes for hello desired groups and click **Save**.</span></span>

![Ustaw widoczność][api-management-add-group-to-product-visibility]

> [!NOTE]
> <span data-ttu-id="ae60b-139">tooadd grupy usługi Azure Active Directory, zobacz [jak tooauthorize developer kont przy użyciu narzędzia Azure Active Directory w usłudze Azure API Management](api-management-howto-aad.md).</span><span class="sxs-lookup"><span data-stu-id="ae60b-139">tooadd Azure Active Directory groups, see [How tooauthorize developer accounts using Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span></span>
> 
> <span data-ttu-id="ae60b-140">grupy tooconfigure z hello **widoczność** produktu, kliknij pozycję **Zarządzaj grupami**.</span><span class="sxs-lookup"><span data-stu-id="ae60b-140">tooconfigure groups from hello **Visibility** tab for a product, click **Manage Groups**.</span></span>
> 
> 

<span data-ttu-id="ae60b-141">Jeśli produkt jest skojarzona z grupą, deweloperzy w tej grupie można wyświetlać i subskrybowania toohello produktu.</span><span class="sxs-lookup"><span data-stu-id="ae60b-141">Once a product is associated with a group, developers in that group can view and subscribe toohello product.</span></span>

## <span data-ttu-id="ae60b-142"><a name="associate-group-developer"></a>Kojarzyć grup z deweloperami</span><span class="sxs-lookup"><span data-stu-id="ae60b-142"><a name="associate-group-developer"> </a>Associate groups with developers</span></span>
<span data-ttu-id="ae60b-143">grupy tooassociate z deweloperami, kliknij przycisk **użytkowników** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie hello pole obok hello deweloperzy mają tooassociate z grupy.</span><span class="sxs-lookup"><span data-stu-id="ae60b-143">tooassociate groups with developers, click **Users** from hello **API Management** menu on hello left, and then check hello box beside hello developers you wish tooassociate with a group.</span></span>

![Dodaj developer toogroup][api-management-add-group-to-developer]

<span data-ttu-id="ae60b-145">Po hello pożądane, deweloperzy są zaznaczone, kliknij odpowiednią grupę hello w hello **dodać tooGroup** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="ae60b-145">Once hello desired developers are checked, click hello desired group in hello **Add tooGroup** drop-down.</span></span> <span data-ttu-id="ae60b-146">Deweloperzy mogą zostać usunięte z grup za pomocą hello **Usuń z grupy** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="ae60b-146">Developers can be removed from groups by using hello **Remove from Group** drop-down.</span></span> 

![Deweloperzy][api-management-add-group-to-developer-saved]

<span data-ttu-id="ae60b-148">Po dodaniu skojarzenia hello między hello deweloperów i hello grupy można wyświetlić ją w hello **użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="ae60b-148">Once hello association is added between hello developer and hello group, you can view it in hello **Users** tab.</span></span>

## <span data-ttu-id="ae60b-149"><a name="next-steps"> </a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ae60b-149"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="ae60b-150">Po dodaniu dewelopera tooa grupy mogą wyświetlać i subskrybować produktów toohello skojarzonych z tej grupy.</span><span class="sxs-lookup"><span data-stu-id="ae60b-150">Once a developer is added tooa group, they can view and subscribe toohello products associated with that group.</span></span> <span data-ttu-id="ae60b-151">Aby uzyskać więcej informacji, zobacz [jak tworzyć i publikować w usłudze Azure API Management produktu][How create and publish a product in Azure API Management],</span><span class="sxs-lookup"><span data-stu-id="ae60b-151">For more information, see [How create and publish a product in Azure API Management][How create and publish a product in Azure API Management],</span></span>
* <span data-ttu-id="ae60b-152">Ponadto toocreating grup i zarządzanie nimi w portalu wydawcy hello, możesz utworzyć i zarządzanie grupami za pomocą interfejsu API REST zarządzania interfejsu API hello [grupy](https://msdn.microsoft.com/library/azure/dn776329.aspx) jednostki.</span><span class="sxs-lookup"><span data-stu-id="ae60b-152">In addition toocreating and managing groups in hello publisher portal, you can create and manage your groups using hello API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>

[api-management-management-console]: ./media/api-management-howto-create-groups/api-management-management-console.png
[api-management-add-group]: ./media/api-management-howto-create-groups/api-management-add-group.png
[api-management-add-group-window]: ./media/api-management-howto-create-groups/api-management-add-group-window.png
[api-management-new-group]: ./media/api-management-howto-create-groups/api-management-new-group.png
[api-management-add-group-to-product]: ./media/api-management-howto-create-groups/api-management-add-group-to-product.png
[api-management-add-group-to-product-visibility]: ./media/api-management-howto-create-groups/api-management-add-group-to-product-visibility.png
[api-management-add-group-to-developer]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer.png
[api-management-add-group-to-developer-saved]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer-saved.png

[api-management-]: ./media/api-management-howto-create-groups/api-management-.png

[Create a group]: #create-group
[Associate a group with a product]: #associate-group-product
[Associate groups with developers]: #associate-group-developer
[Next steps]: #next-steps

[How create and publish a product in Azure API Management]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[leverage external groups in associated Azure Active Directory tenants]: api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group
