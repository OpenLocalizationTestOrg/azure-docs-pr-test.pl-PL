---
title: "Jak zarządzać kontami użytkowników w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć lub zaprosić użytkowników w usłudze Azure API Management"
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
ms.openlocfilehash: d3a50f6d22cbf1797f580078bc0d2cc9cefe5064
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-user-accounts-in-azure-api-management"></a><span data-ttu-id="dfcd4-103">Jak zarządzać kontami użytkowników w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="dfcd4-103">How to manage user accounts in Azure API Management</span></span>
<span data-ttu-id="dfcd4-104">W usłudze API Management Deweloperzy są użytkownicy interfejsów API, które można udostępnić przy użyciu interfejsu API zarządzania.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-104">In API Management, developers are the users of the APIs that you expose using API Management.</span></span> <span data-ttu-id="dfcd4-105">Ten przewodnik przedstawia sposobu tworzenia i zapraszanie deweloperów do korzystania z interfejsów API i produktów czy należy udostępnić je z wystąpieniem usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-105">This guide shows to how to create and invite developers to use the APIs and products that you make available to them with your API Management instance.</span></span> <span data-ttu-id="dfcd4-106">Informacje na programowe zarządzanie kontami użytkowników, zobacz [jednostki użytkownika](https://msdn.microsoft.com/library/azure/dn776330.aspx) dokumentacji w [interfejsu API REST zarządzania](https://msdn.microsoft.com/library/azure/dn776326.aspx) odwołania.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-106">For information on managing user accounts programmatically, see the [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span>

## <span data-ttu-id="dfcd4-107"><a name="create-developer"></a>Tworzenie nowych developer</span><span class="sxs-lookup"><span data-stu-id="dfcd4-107"><a name="create-developer"> </a>Create a new developer</span></span>
<span data-ttu-id="dfcd4-108">Aby utworzyć nowy developer, kliknij przycisk **portal wydawcy** w portalu Azure usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-108">To create a new developer, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="dfcd4-109">Spowoduje to przejście do portalu wydawcy usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-109">This takes you to the API Management publisher portal.</span></span> <span data-ttu-id="dfcd4-110">Jeśli jeszcze nie masz utworzonego wystąpienia usługi API Management, zobacz [Tworzenie wystąpienia usługi API Management][Create an API Management service instance] w samouczku [Wprowadzenie do usługi Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="dfcd4-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Portal wydawcy][api-management-management-console]

<span data-ttu-id="dfcd4-112">Kliknij przycisk **użytkowników** z **zarządzanie interfejsami API** menu po lewej stronie, a następnie kliknij przycisk **dodać użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-112">Click **Users** from the **API Management** menu on the left, and then click **add user**.</span></span>

![Utwórz developer][api-management-create-developer]

<span data-ttu-id="dfcd4-114">Wprowadź **E-mail**, **hasło**, i **nazwa** developer nowy i kliknij **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-114">Enter the **Email**, **Password**, and **Name** for the new developer and click **Save**.</span></span>

![Utwórz developer][api-management-add-new-user]

<span data-ttu-id="dfcd4-116">Domyślnie developer nowo utworzonego konta są **Active**wraz ze skojarzonymi z **deweloperzy** grupy.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-116">By default, newly created developer accounts are **Active**, and associated with the **Developers** group.</span></span>

![Nowe developer][api-management-new-developer]

<span data-ttu-id="dfcd4-118">Konta dewelopera, które znajdują się w **active** stanu można uzyskać dostęp do wszystkich interfejsów API, do którego mają zostać subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-118">Developer accounts that are in an **active** state can be used to access all of the APIs for which they have subscriptions.</span></span> <span data-ttu-id="dfcd4-119">Aby skojarzyć developer nowo utworzony z dodatkowych grup, zobacz [sposobu kojarzenia grupy z deweloperami][How to associate groups with developers].</span><span class="sxs-lookup"><span data-stu-id="dfcd4-119">To associate the newly created developer with additional groups, see [How to associate groups with developers][How to associate groups with developers].</span></span>

## <span data-ttu-id="dfcd4-120"><a name="invite-developer"></a>Zaprosić dewelopera</span><span class="sxs-lookup"><span data-stu-id="dfcd4-120"><a name="invite-developer"> </a>Invite a developer</span></span>
<span data-ttu-id="dfcd4-121">Aby zaprosić dewelopera, kliknij przycisk **użytkowników** z **zarządzanie interfejsami API** menu po lewej stronie, a następnie kliknij przycisk **zaprosić użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-121">To invite a developer, click **Users** from the **API Management** menu on the left, and then click **Invite User**.</span></span>

![Zaproś developer][api-management-invite-developer]

<span data-ttu-id="dfcd4-123">Wprowadź nazwę i adres e-mail dewelopera, a następnie kliknij przycisk **zaprosić**.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-123">Enter the name and email address of the developer, and click **Invite**.</span></span>

![Zaproś developer][api-management-invite-developer-window]

<span data-ttu-id="dfcd4-125">Zostanie wyświetlony komunikat potwierdzenia, ale Deweloper nowo zaproszonych nie znajdują się na liście dopiero po ich zaakceptowaniu zaproszenia.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-125">A confirmation message is displayed, but the newly invited developer does not appear in the list until after they accept the invitation.</span></span> 

![Zaproś potwierdzenia][api-management-invite-developer-confirmation]

<span data-ttu-id="dfcd4-127">Gdy Projektant jest zaproszenie, zostanie wysłana wiadomość e-mail do deweloperów.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-127">When a developer is invited, an email is sent to the developer.</span></span> <span data-ttu-id="dfcd4-128">Ten adres e-mail jest generowana z użyciem szablonu i można dostosowywać.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-128">This email is generated using a template and is customizable.</span></span> <span data-ttu-id="dfcd4-129">Aby uzyskać więcej informacji, zobacz [Konfigurowanie szablonów wiadomości e-mail][Configure email templates].</span><span class="sxs-lookup"><span data-stu-id="dfcd4-129">For more information, see [Configure email templates][Configure email templates].</span></span>

<span data-ttu-id="dfcd4-130">Po zaakceptowaniu zaproszenia konto staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-130">Once the invitation is accepted, the account becomes active.</span></span>

## <span data-ttu-id="dfcd4-131"><a name="block-developer"></a> Dezaktywuj lub ponownym uaktywnieniem konta dewelopera</span><span class="sxs-lookup"><span data-stu-id="dfcd4-131"><a name="block-developer"> </a> Deactivate or reactivate a developer account</span></span>
<span data-ttu-id="dfcd4-132">Domyślnie są konta dewelopera nowo utworzone lub zaproszonych **Active**.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-132">By default, newly created or invited developer accounts are **Active**.</span></span> <span data-ttu-id="dfcd4-133">Aby zdezaktywować konta dewelopera, kliknij przycisk **bloku**.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-133">To deactivate a developer account, click **Block**.</span></span> <span data-ttu-id="dfcd4-134">Aby ponownie uaktywnić konto dewelopera zablokowanych, kliknij przycisk **Aktywuj**.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-134">To reactivate a blocked developer account, click **Activate**.</span></span> <span data-ttu-id="dfcd4-135">Konto dewelopera zablokowanych nie można uzyskać dostępu do portalu dla deweloperów lub zadzwoń wszystkie interfejsy API.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-135">A blocked developer account can not access the developer portal or call any APIs.</span></span> <span data-ttu-id="dfcd4-136">Aby usunąć konto użytkownika, kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-136">To delete a user account, click **Delete**.</span></span>

![Blok developer][api-management-new-developer]

## <a name="reset-a-user-password"></a><span data-ttu-id="dfcd4-138">Resetowanie hasła użytkownika</span><span class="sxs-lookup"><span data-stu-id="dfcd4-138">Reset a user password</span></span>
<span data-ttu-id="dfcd4-139">Aby zresetować hasło do konta użytkownika, kliknij nazwę konta.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-139">To reset the password for a user account, click the name of the account.</span></span>

![Resetowanie hasła][api-management-view-developer]

<span data-ttu-id="dfcd4-141">Kliknij przycisk **resetowania hasła** wysłać łącze do użytkownika, aby zresetować swoje hasło.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-141">Click **Reset password** to send a link to the user to reset their password.</span></span>

![Resetowanie hasła][api-management-reset-password]

<span data-ttu-id="dfcd4-143">Aby programowo pracować z kontami użytkowników, zobacz [jednostki użytkownika](https://msdn.microsoft.com/library/azure/dn776330.aspx) dokumentacji w [interfejsu API REST zarządzania](https://msdn.microsoft.com/library/azure/dn776326.aspx) odwołania.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-143">To programmatically work with user accounts, see the [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span> <span data-ttu-id="dfcd4-144">Aby zresetować hasło do konta użytkownika na określoną wartość, można użyć [zaktualizowania użytkownika](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operację i określ odpowiednie hasło.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-144">To reset a user account password to a specific value, you can use the [Update a user](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operation and specify the desired password.</span></span>

## <a name="pending-verification"></a><span data-ttu-id="dfcd4-145">Oczekujące weryfikacji</span><span class="sxs-lookup"><span data-stu-id="dfcd4-145">Pending verification</span></span>
![Oczekujące weryfikacji][api-management-pending-verification]

## <span data-ttu-id="dfcd4-147"><a name="next-steps"> </a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dfcd4-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="dfcd4-148">Po utworzeniu konta dewelopera, można ją skojarzyć z rolami i subskrybowania produktów i interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="dfcd4-148">Once a developer account is created, you can associate it with roles and subscribe it to products and APIs.</span></span> <span data-ttu-id="dfcd4-149">Aby uzyskać więcej informacji, zobacz [sposobu tworzenia i używania grup][How to create and use groups].</span><span class="sxs-lookup"><span data-stu-id="dfcd4-149">For more information, see [How to create and use groups][How to create and use groups].</span></span>

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
[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
