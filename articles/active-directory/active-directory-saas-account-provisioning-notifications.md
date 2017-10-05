---
title: "Inicjowanie obsługi administracyjnej powiadomienia konta | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak i upewnij się, że użytkownik jest powiadamiany o problemy związane z Inicjowanie obsługi użytkowników, które wymagają Twojej uwagi, umożliwiając Inicjowanie obsługi administracyjnej powiadomienia konta."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a637aac7-f06b-48ef-a66d-639835a8edec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: b99037fc28eca1a3ebffefb9e99991e74f52c9a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="account-provisioning-notifications"></a><span data-ttu-id="a2c74-103">Powiadomienia związane z aprowizacją kont</span><span class="sxs-lookup"><span data-stu-id="a2c74-103">Account Provisioning Notifications</span></span>
<span data-ttu-id="a2c74-104">Obsługa administracyjna użytkownika, można zautomatyzować proces zarządzania użytkowników w innej aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="a2c74-104">With user provisioning, you can automate the process of managing users in third party SaaS applications.</span></span> <br>
<span data-ttu-id="a2c74-105">Jest to zautomatyzowany proces, interakcję z tym procesem od czasu do czasu jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="a2c74-105">While this is an automated process, your interaction with this process is from time to time required.</span></span> <br>
<span data-ttu-id="a2c74-106">Dotyczy, na przykład, gdy hasło konta, które zostały skonfigurowane w celu wymiany danych z innej strony wygasła aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="a2c74-106">This is, for example the case, when the password of the account you have configured to exchange data with a third party SaaS application has expired.</span></span> 

<span data-ttu-id="a2c74-107">Przez włączenie inicjowania obsługi powiadomień konta, możesz upewnij się, że użytkownik jest powiadamiany o problemy związane z Inicjowanie obsługi użytkowników, które wymagają Twojej uwagi.</span><span class="sxs-lookup"><span data-stu-id="a2c74-107">By enabling account provisioning notifications, you can ensure that you are notified of issues related to user provisioning that require your attention.</span></span>

<span data-ttu-id="a2c74-108">Aktywować lub dezaktywować inicjowania obsługi powiadomienia użytkownika inicjowania obsługi konfiguracji dla innej aplikacji SaaS w ramach konta.</span><span class="sxs-lookup"><span data-stu-id="a2c74-108">You activate or deactivate account provisioning notifications as part of your user provisioning configuration for a third party SaaS application.</span></span>

![Inicjowanie obsługi użytkowników][1] 

<span data-ttu-id="a2c74-110">Aby aktywować konto inicjowania obsługi powiadomień, zaznacz pole wyboru powiązane na **potwierdzenie** strony okna dialogowego, a następnie wpisz alias e-mail odbiorcy.</span><span class="sxs-lookup"><span data-stu-id="a2c74-110">To activate account provisioning notifications, select the related checkbox on the **Confirmation** dialog page, and then type the email alias of the recipient.</span></span>

![Powiadomienia związane z aprowizacją kont][2]

<span data-ttu-id="a2c74-112">Możesz wprowadzić listę dystrybucyjną jako recipient; jest jednak należy pamiętać, że powiadomienie e-mail zawiera linki do raportów dostępnych tylko przez administratorów usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2c74-112">You can enter a distribution list as recipient; however, it is important to note that the notification email contains links to reports that are only accessible by the Azure AD administrators.</span></span>

<span data-ttu-id="a2c74-113">Jeśli masz konto inicjowania obsługi powiadomień włączone, będziesz otrzymywać wiadomości e-mail o krytyczne problemy, które są powiązane z Inicjowanie obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a2c74-113">If you have account provisioning notifications enabled, you will receive emails about critical issues that are related to user provisioning.</span></span> <span data-ttu-id="a2c74-114">Jednak aby uniknąć przeciążenia poczty e-mail, otrzymasz tylko jednego powiadomienia e-mail dziennie dla każdej aplikacji SaaS powiadomienia e-mail jest włączone dla.</span><span class="sxs-lookup"><span data-stu-id="a2c74-114">However, to avoid an email overload, you will only receive one notification email per day for each SaaS application the notification email is enabled for.</span></span>

## <a name="related-articles"></a><span data-ttu-id="a2c74-115">Pokrewne artykuły</span><span class="sxs-lookup"><span data-stu-id="a2c74-115">Related Articles</span></span>
* [<span data-ttu-id="a2c74-116">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2c74-116">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="a2c74-117">Automatyzowanie użytkownika udostępniania/anulowania obsługi do aplikacji SaaS</span><span class="sxs-lookup"><span data-stu-id="a2c74-117">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="a2c74-118">Dostosowywanie mapowań atrybutów do inicjowania obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="a2c74-118">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="a2c74-119">Tworzenie wyrażeń na potrzeby mapowań atrybutów</span><span class="sxs-lookup"><span data-stu-id="a2c74-119">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="a2c74-120">Filtry zakresu dla Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="a2c74-120">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="a2c74-121">Włączanie automatycznej aprowizacji użytkowników i grup z usługi Azure Active Directory do aplikacji przy użyciu SCIM</span><span class="sxs-lookup"><span data-stu-id="a2c74-121">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="a2c74-122">Lista samouczków dotyczących sposobów integracji aplikacji SaaS</span><span class="sxs-lookup"><span data-stu-id="a2c74-122">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-account-provisioning-notifications/ic766307.png
[2]: ./media/active-directory-saas-account-provisioning-notifications/ic766308.png
