---
title: "Zarządzanie kontami dewelopera przy użyciu grup w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zarządzać kontami dewelopera przy użyciu grup w usłudze Azure API Management"
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
ms.openlocfilehash: b4d71cdfbab535b02542fbb26c7555265e5f9c37
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-use-groups-to-manage-developer-accounts-in-azure-api-management"></a><span data-ttu-id="6d6b4-103">Tworzenie i używanie grup do zarządzania konta dewelopera usługi Azure API Management</span><span class="sxs-lookup"><span data-stu-id="6d6b4-103">How to create and use groups to manage developer accounts in Azure API Management</span></span>
<span data-ttu-id="6d6b4-104">W usłudze API Management grupy służą do zarządzania widocznością produktów dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-104">In API Management, groups are used to manage the visibility of products to developers.</span></span> <span data-ttu-id="6d6b4-105">Produkty są najpierw stają się widoczne dla grup, a następnie deweloperów w tych grupach można wyświetlać i subskrybować produktów, które są skojarzone z grupami.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-105">Products are first made visible to groups, and then developers in those groups can view and subscribe to the products that are associated with the groups.</span></span> 

<span data-ttu-id="6d6b4-106">Usługa API Management ma następujące niezmienne grupy systemowe.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-106">API Management has the following immutable system groups.</span></span>

* <span data-ttu-id="6d6b4-107">**Administratorzy** — do tej grupy należą administratorzy subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-107">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="6d6b4-108">Administratorzy zarządzają wystąpieniami usługi API Management, tworząc interfejsy API, operacje i produkty, które są używane przez deweloperów.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-108">Administrators manage API Management service instances, creating the APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="6d6b4-109">**Deweloperzy** — do tej grupy należą uwierzytelnieni użytkownicy portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-109">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="6d6b4-110">Deweloperzy to klienci, którzy tworzą aplikacje przy użyciu interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-110">Developers are the customers that build applications using your APIs.</span></span> <span data-ttu-id="6d6b4-111">Deweloperzy otrzymują dostęp do portalu dla deweloperów i tworzą aplikacje, które wywołują operacje interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-111">Developers are granted access to the developer portal and build applications that call the operations of an API.</span></span>
* <span data-ttu-id="6d6b4-112">**Goście** — do tej grupy należą nieuwierzytelnieni użytkownicy portalu dla deweloperów, tacy jak potencjalni klienci odwiedzający portal dla deweloperów wystąpienia usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-112">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting the developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="6d6b4-113">Mogą mieć przyznany pewien zakres dostępu tylko do odczytu, czyli np. możliwość wyświetlania interfejsów API, ale nie ich wywoływania.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-113">They can be granted certain read-only access, such as the ability to view APIs but not call them.</span></span>

<span data-ttu-id="6d6b4-114">Oprócz tych grup systemu, Administratorzy mogą tworzyć niestandardowe grupy lub [korzystać z zewnętrznej grupy w skojarzonych dzierżaw usługi Azure Active Directory][leverage external groups in associated Azure Active Directory tenants].</span><span class="sxs-lookup"><span data-stu-id="6d6b4-114">In addition to these system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants][leverage external groups in associated Azure Active Directory tenants].</span></span> <span data-ttu-id="6d6b4-115">Niestandardowe i zewnętrzne grupy mogą być używane razem z grupami systemowymi, zapewniając deweloperom widoczność produktów interfejsu API i dostęp do nich.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-115">Custom and external groups can be used alongside system groups in giving developers visibility and access to API products.</span></span> <span data-ttu-id="6d6b4-116">Można na przykład utworzyć jedną grupę niestandardową dla deweloperów powiązanych z konkretną organizacją partnera i zezwolić im na dostęp do interfejsów API z produktów zawierających tylko odpowiednie interfejsy API.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-116">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access to the APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="6d6b4-117">Użytkownik może należeć do więcej niż jednej grupy.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-117">A user can be a member of more than one group.</span></span>

<span data-ttu-id="6d6b4-118">W tym przewodniku pokazano, jak Administratorzy wystąpienia interfejsu API zarządzania mogą dodawać nowe grupy i skojarzyć je z produktami i deweloperów.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-118">This guide shows how administrators of an API Management instance can add new groups and associate them with products and developers.</span></span>

> [!NOTE]
> <span data-ttu-id="6d6b4-119">Oprócz tworzenia grup i zarządzanie nimi w portalu wydawcy, można tworzyć i zarządzać przy użyciu interfejsu API REST API zarządzania grupami [grupy](https://msdn.microsoft.com/library/azure/dn776329.aspx) jednostki.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-119">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>
> 
> 

## <span data-ttu-id="6d6b4-120"><a name="create-group"></a>Utwórz grupę</span><span class="sxs-lookup"><span data-stu-id="6d6b4-120"><a name="create-group"> </a>Create a group</span></span>
<span data-ttu-id="6d6b4-121">Aby utworzyć nową grupę, kliknij przycisk **portal wydawcy** w portalu Azure usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-121">To create a new group, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="6d6b4-122">Spowoduje to przejście do portalu wydawcy usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-122">This takes you to the API Management publisher portal.</span></span>

![Portal wydawcy][api-management-management-console]

> <span data-ttu-id="6d6b4-124">Jeśli jeszcze nie masz utworzonego wystąpienia usługi API Management, zobacz [Tworzenie wystąpienia usługi API Management][Create an API Management service instance] w samouczku [Wprowadzenie do usługi Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="6d6b4-124">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="6d6b4-125">Kliknij przycisk **grup** z **zarządzanie interfejsami API** menu po lewej stronie, a następnie kliknij przycisk **Dodaj grupę**.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-125">Click **Groups** from the **API Management** menu on the left, and then click **Add Group**.</span></span>

![Dodaj nową grupę][api-management-add-group]

<span data-ttu-id="6d6b4-127">Wprowadź unikatową nazwę grupy i opcjonalny opis, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-127">Enter a unique name for the group and an optional description, and click **Save**.</span></span>

![Dodaj nową grupę][api-management-add-group-window]

<span data-ttu-id="6d6b4-129">Nowa grupa zostanie wyświetlona na karcie grupy.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-129">The new group is displayed in the groups tab.</span></span> <span data-ttu-id="6d6b4-130">Aby edytować **nazwa** lub **opis** grupy, kliknij nazwę grupy na liście.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-130">To edit the **Name** or **Description** of the group, click the name of the group in the list.</span></span> <span data-ttu-id="6d6b4-131">Aby usunąć grupę, kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-131">To delete the group, click **Delete**.</span></span>

![Grupy dodane][api-management-new-group]

<span data-ttu-id="6d6b4-133">Teraz, gdy grupa nie zostanie utworzona, można ją skojarzyć z produktami i deweloperów.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-133">Now that the group is created, it can be associated with products and developers.</span></span>

## <span data-ttu-id="6d6b4-134"><a name="associate-group-product"></a>Skojarzyć grupy z produktem</span><span class="sxs-lookup"><span data-stu-id="6d6b4-134"><a name="associate-group-product"> </a>Associate a group with a product</span></span>
<span data-ttu-id="6d6b4-135">Aby skojarzyć grupy z produktem, kliknij przycisk **produktów** z **zarządzanie interfejsami API** menu po lewej stronie, a następnie kliknij nazwę żądanego produktu.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-135">To associate a group with a product, click **Products** from the **API Management** menu on the left, and then click the name of the desired product.</span></span>

![Ustaw widoczność][api-management-add-group-to-product]

<span data-ttu-id="6d6b4-137">Wybierz **widoczność** kartę, aby dodawać i usuwać grupy i wyświetlić bieżących grup dla produktu.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-137">Select the **Visibility** tab to add and remove groups, and to view the current groups for the product.</span></span> <span data-ttu-id="6d6b4-138">Aby dodać lub usunąć grupy, zaznacz lub usuń zaznaczenie pól wyboru dla żądanej grupy i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-138">To add or remove groups, check or uncheck the checkboxes for the desired groups and click **Save**.</span></span>

![Ustaw widoczność][api-management-add-group-to-product-visibility]

> [!NOTE]
> <span data-ttu-id="6d6b4-140">Aby dodać grupy usługi Azure Active Directory, zobacz [sposób autoryzowania konta dewelopera przy użyciu usługi Azure Active Directory w usłudze Azure API Management](api-management-howto-aad.md).</span><span class="sxs-lookup"><span data-stu-id="6d6b4-140">To add Azure Active Directory groups, see [How to authorize developer accounts using Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span></span>
> 
> <span data-ttu-id="6d6b4-141">Aby skonfigurować grupy z **widoczność** produktu, kliknij pozycję **Zarządzaj grupami**.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-141">To configure groups from the **Visibility** tab for a product, click **Manage Groups**.</span></span>
> 
> 

<span data-ttu-id="6d6b4-142">Jeśli produkt jest skojarzona z grupą, deweloperzy w tej grupie można wyświetlać i subskrybować produktu.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-142">Once a product is associated with a group, developers in that group can view and subscribe to the product.</span></span>

## <span data-ttu-id="6d6b4-143"><a name="associate-group-developer"></a>Kojarzyć grup z deweloperami</span><span class="sxs-lookup"><span data-stu-id="6d6b4-143"><a name="associate-group-developer"> </a>Associate groups with developers</span></span>
<span data-ttu-id="6d6b4-144">Aby skojarzyć grupy z deweloperami, kliknij przycisk **użytkowników** z **zarządzanie interfejsami API** menu po lewej stronie, a następnie zaznacz pole obok deweloperzy chcesz skojarzyć z grupą.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-144">To associate groups with developers, click **Users** from the **API Management** menu on the left, and then check the box beside the developers you wish to associate with a group.</span></span>

![Dodawanie projektanta do grupy][api-management-add-group-to-developer]

<span data-ttu-id="6d6b4-146">Po żądaną Deweloperzy są zaznaczone, kliknij odpowiednią grupę w **dodać do grupy** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-146">Once the desired developers are checked, click the desired group in the **Add to Group** drop-down.</span></span> <span data-ttu-id="6d6b4-147">Deweloperzy mogą zostać usunięte z grup za pomocą **Usuń z grupy** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-147">Developers can be removed from groups by using the **Remove from Group** drop-down.</span></span> 

![Deweloperzy][api-management-add-group-to-developer-saved]

<span data-ttu-id="6d6b4-149">Po dodaniu skojarzenia między projektanta i grupy, możesz je wyświetlić w **użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-149">Once the association is added between the developer and the group, you can view it in the **Users** tab.</span></span>

## <span data-ttu-id="6d6b4-150"><a name="next-steps"> </a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6d6b4-150"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="6d6b4-151">Po dodaniu do grupy Deweloperzy mogą wyświetlać i subskrybować produktów skojarzonych z tej grupy.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-151">Once a developer is added to a group, they can view and subscribe to the products associated with that group.</span></span> <span data-ttu-id="6d6b4-152">Aby uzyskać więcej informacji, zobacz [jak tworzyć i publikować w usłudze Azure API Management produktu][How create and publish a product in Azure API Management],</span><span class="sxs-lookup"><span data-stu-id="6d6b4-152">For more information, see [How create and publish a product in Azure API Management][How create and publish a product in Azure API Management],</span></span>
* <span data-ttu-id="6d6b4-153">Oprócz tworzenia grup i zarządzanie nimi w portalu wydawcy, można tworzyć i zarządzać przy użyciu interfejsu API REST API zarządzania grupami [grupy](https://msdn.microsoft.com/library/azure/dn776329.aspx) jednostki.</span><span class="sxs-lookup"><span data-stu-id="6d6b4-153">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>

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
