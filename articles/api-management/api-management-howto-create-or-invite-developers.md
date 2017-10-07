---
title: "aaaHow Zarządzanie kontami użytkowników w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate lub zaprosić użytkowników w usłudze Azure API Management"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 078abfa5-1e4f-4c9d-b9c7-a172bd19c1a2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3966f4454e29621d7c615beefee352ec91b48b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-user-accounts-in-azure-api-management"></a><span data-ttu-id="1f7f7-103">Jak konta użytkowników toomanage w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="1f7f7-103">How toomanage user accounts in Azure API Management</span></span>
<span data-ttu-id="1f7f7-104">W usłudze API Management Deweloperzy są użytkownikami hello hello interfejsów API, które można udostępnić przy użyciu interfejsu API zarządzania.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-104">In API Management, developers are hello users of hello APIs that you expose using API Management.</span></span> <span data-ttu-id="1f7f7-105">Ten przewodnik przedstawia toohow toocreate i zaproszenia deweloperzy toouse hello interfejsów API i produktów należy toothem dostępne z wystąpieniem usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-105">This guide shows toohow toocreate and invite developers toouse hello APIs and products that you make available toothem with your API Management instance.</span></span> <span data-ttu-id="1f7f7-106">Uzyskać informacji o programowe zarządzanie kontami użytkowników, zobacz hello [jednostki użytkownika](https://msdn.microsoft.com/library/azure/dn776330.aspx) dokumentacji w hello [interfejsu API REST zarządzania](https://msdn.microsoft.com/library/azure/dn776326.aspx) odwołania.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-106">For information on managing user accounts programmatically, see hello [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in hello [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span>

## <span data-ttu-id="1f7f7-107"><a name="create-developer"></a>Tworzenie nowych developer</span><span class="sxs-lookup"><span data-stu-id="1f7f7-107"><a name="create-developer"> </a>Create a new developer</span></span>
<span data-ttu-id="1f7f7-108">toocreate nowych deweloperów, kliknij przycisk **portal wydawcy** w hello portalu Azure usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-108">toocreate a new developer, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="1f7f7-109">Trwa toohello zarządzanie interfejsami API wydawcy portalu.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-109">This takes you toohello API Management publisher portal.</span></span> <span data-ttu-id="1f7f7-110">Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Portal wydawcy][api-management-management-console]

<span data-ttu-id="1f7f7-112">Kliknij przycisk **użytkowników** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij **dodać użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-112">Click **Users** from hello **API Management** menu on hello left, and then click **add user**.</span></span>

![Utwórz developer][api-management-create-developer]

<span data-ttu-id="1f7f7-114">Wprowadź hello **E-mail**, **hasło**, i **nazwa** hello nowych deweloperów, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-114">Enter hello **Email**, **Password**, and **Name** for hello new developer and click **Save**.</span></span>

![Utwórz developer][api-management-add-new-user]

<span data-ttu-id="1f7f7-116">Domyślnie developer nowo utworzonego konta są **Active**wraz ze skojarzonymi z hello **deweloperzy** grupy.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-116">By default, newly created developer accounts are **Active**, and associated with hello **Developers** group.</span></span>

![Nowe developer][api-management-new-developer]

<span data-ttu-id="1f7f7-118">Konta dewelopera, które znajdują się w **active** stanu mogą być używane tooaccess wszystkie interfejsy API hello, do którego mają zostać subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-118">Developer accounts that are in an **active** state can be used tooaccess all of hello APIs for which they have subscriptions.</span></span> <span data-ttu-id="1f7f7-119">tooassociate dewelopera hello nowo utworzone przy użyciu dodatkowych grup, zobacz [jak tooassociate grup z deweloperami][How tooassociate groups with developers].</span><span class="sxs-lookup"><span data-stu-id="1f7f7-119">tooassociate hello newly created developer with additional groups, see [How tooassociate groups with developers][How tooassociate groups with developers].</span></span>

## <span data-ttu-id="1f7f7-120"><a name="invite-developer"></a>Zaprosić dewelopera</span><span class="sxs-lookup"><span data-stu-id="1f7f7-120"><a name="invite-developer"> </a>Invite a developer</span></span>
<span data-ttu-id="1f7f7-121">tooinvite dewelopera, kliknij przycisk **użytkowników** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij **zaprosić użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-121">tooinvite a developer, click **Users** from hello **API Management** menu on hello left, and then click **Invite User**.</span></span>

![Zaproś developer][api-management-invite-developer]

<span data-ttu-id="1f7f7-123">Wprowadź nazwę i adres e-mail adres hello dewelopera hello, a następnie kliknij przycisk **zaprosić**.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-123">Enter hello name and email address of hello developer, and click **Invite**.</span></span>

![Zaproś developer][api-management-invite-developer-window]

<span data-ttu-id="1f7f7-125">Zostanie wyświetlony komunikat potwierdzenia, ale Deweloper hello nowo zaproszenie nie ma listy hello do po zaakceptowaniu zaproszenia hello.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-125">A confirmation message is displayed, but hello newly invited developer does not appear in hello list until after they accept hello invitation.</span></span> 

![Zaproś potwierdzenia][api-management-invite-developer-confirmation]

<span data-ttu-id="1f7f7-127">Gdy poproszeni dewelopera toohello developer zostanie wysłana wiadomość e-mail.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-127">When a developer is invited, an email is sent toohello developer.</span></span> <span data-ttu-id="1f7f7-128">Ten adres e-mail jest generowana z użyciem szablonu i można dostosowywać.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-128">This email is generated using a template and is customizable.</span></span> <span data-ttu-id="1f7f7-129">Aby uzyskać więcej informacji, zobacz [Konfigurowanie szablonów wiadomości e-mail][Configure email templates].</span><span class="sxs-lookup"><span data-stu-id="1f7f7-129">For more information, see [Configure email templates][Configure email templates].</span></span>

<span data-ttu-id="1f7f7-130">Po zaakceptowaniu zaproszenia hello konta hello staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-130">Once hello invitation is accepted, hello account becomes active.</span></span>

## <span data-ttu-id="1f7f7-131"><a name="block-developer"></a> Dezaktywuj lub ponownym uaktywnieniem konta dewelopera</span><span class="sxs-lookup"><span data-stu-id="1f7f7-131"><a name="block-developer"> </a> Deactivate or reactivate a developer account</span></span>
<span data-ttu-id="1f7f7-132">Domyślnie są konta dewelopera nowo utworzone lub zaproszonych **Active**.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-132">By default, newly created or invited developer accounts are **Active**.</span></span> <span data-ttu-id="1f7f7-133">Kliknij konto dewelopera toodeactivate **bloku**.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-133">toodeactivate a developer account, click **Block**.</span></span> <span data-ttu-id="1f7f7-134">Kliknij konto dewelopera zablokowanych tooreactivate **Aktywuj**.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-134">tooreactivate a blocked developer account, click **Activate**.</span></span> <span data-ttu-id="1f7f7-135">Konto dewelopera zablokowanych nie można uzyskać dostępu do portalu dla deweloperów hello lub zadzwoń wszystkie interfejsy API.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-135">A blocked developer account can not access hello developer portal or call any APIs.</span></span> <span data-ttu-id="1f7f7-136">toodelete konta użytkownika, kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-136">toodelete a user account, click **Delete**.</span></span>

![Blok developer][api-management-new-developer]

## <a name="reset-a-user-password"></a><span data-ttu-id="1f7f7-138">Resetowanie hasła użytkownika</span><span class="sxs-lookup"><span data-stu-id="1f7f7-138">Reset a user password</span></span>
<span data-ttu-id="1f7f7-139">tooreset hello hasło dla konta użytkownika, kliknij nazwę hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-139">tooreset hello password for a user account, click hello name of hello account.</span></span>

![Resetowanie hasła][api-management-view-developer]

<span data-ttu-id="1f7f7-141">Kliknij przycisk **resetowania hasła** toosend łącze toohello użytkownika tooreset swoje hasło.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-141">Click **Reset password** toosend a link toohello user tooreset their password.</span></span>

![Resetowanie hasła][api-management-reset-password]

<span data-ttu-id="1f7f7-143">tooprogrammatically pracy z kontami użytkowników, zobacz hello [jednostki użytkownika](https://msdn.microsoft.com/library/azure/dn776330.aspx) dokumentacji w hello [interfejsu API REST zarządzania](https://msdn.microsoft.com/library/azure/dn776326.aspx) odwołania.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-143">tooprogrammatically work with user accounts, see hello [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in hello [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span> <span data-ttu-id="1f7f7-144">tooreset użytkownika konta hasło tooa określoną wartość, można użyć hello [zaktualizowania użytkownika](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operację i określ hello wymagane hasło.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-144">tooreset a user account password tooa specific value, you can use hello [Update a user](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operation and specify hello desired password.</span></span>

## <a name="pending-verification"></a><span data-ttu-id="1f7f7-145">Oczekujące weryfikacji</span><span class="sxs-lookup"><span data-stu-id="1f7f7-145">Pending verification</span></span>
![Oczekujące weryfikacji][api-management-pending-verification]

## <span data-ttu-id="1f7f7-147"><a name="next-steps"> </a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1f7f7-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="1f7f7-148">Po utworzeniu konta dewelopera, można ją skojarzyć z rolami i subskrybowania go tooproducts i interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="1f7f7-148">Once a developer account is created, you can associate it with roles and subscribe it tooproducts and APIs.</span></span> <span data-ttu-id="1f7f7-149">Aby uzyskać więcej informacji, zobacz [jak toocreate i używania grup][How toocreate and use groups].</span><span class="sxs-lookup"><span data-stu-id="1f7f7-149">For more information, see [How toocreate and use groups][How toocreate and use groups].</span></span>

[api-management-management-console]: ./media/api-management-howto-create-or-invite-developers/api-management-management-console.png
[api-management-add-new-user]: ./media/api-management-howto-create-or-invite-developers/api-management-add-new-user.png
[api-management-create-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-create-developer.png
[api-management-invite-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer.png
[api-management-new-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-new-developer.png
[api-management-invite-developer-window]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-window.png
[api-management-invite-developer-confirmation]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-confirmation.png
[api-management-pending-verification]: ./media/api-management-howto-create-or-invite-developers/api-management-pending-verification.png
[api-management-view-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-view-developer.png
[api-management-reset-password]: ./media/api-management-howto-create-or-invite-developers/api-management-reset-password.png


[Create a new developer]: #create-developer
[Invite a developer]: #invite-developer
[Deactivate or reactivate a developer account]: #block-developer
[Next steps]: #next-steps
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
