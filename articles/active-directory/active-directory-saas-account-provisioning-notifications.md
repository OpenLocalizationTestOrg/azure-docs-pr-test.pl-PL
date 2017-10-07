---
title: "aaaAccount inicjowania obsługi powiadomień | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooensure, że użytkownik jest powiadamiany o problemy związane z toouser inicjowania obsługi, które wymagają Twojej uwagi, należy włączyć konta inicjowania obsługi powiadomień."
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
ms.openlocfilehash: e33d1dd806fff43fc96f843a9dcddd7375d2e3c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="account-provisioning-notifications"></a><span data-ttu-id="7996c-103">Powiadomienia związane z aprowizacją kont</span><span class="sxs-lookup"><span data-stu-id="7996c-103">Account Provisioning Notifications</span></span>
<span data-ttu-id="7996c-104">Z Inicjowanie obsługi użytkowników, można zautomatyzować proces hello Zarządzanie użytkownikami w innej aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="7996c-104">With user provisioning, you can automate hello process of managing users in third party SaaS applications.</span></span> <br>
<span data-ttu-id="7996c-105">Jest to zautomatyzowany proces, interakcję z tym procesem jest z tootime czas wymagany.</span><span class="sxs-lookup"><span data-stu-id="7996c-105">While this is an automated process, your interaction with this process is from time tootime required.</span></span> <br>
<span data-ttu-id="7996c-106">Dotyczy, na przykład hello sytuacji, gdy hello hasło konta hello się, że skonfigurowano tooexchange danych z innej strony wygasła aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="7996c-106">This is, for example hello case, when hello password of hello account you have configured tooexchange data with a third party SaaS application has expired.</span></span> 

<span data-ttu-id="7996c-107">Przez włączenie inicjowania obsługi powiadomień konta, możesz upewnij się, że użytkownik jest powiadamiany o udostępniania toouser pokrewne problemy, które wymagają Twojej uwagi.</span><span class="sxs-lookup"><span data-stu-id="7996c-107">By enabling account provisioning notifications, you can ensure that you are notified of issues related toouser provisioning that require your attention.</span></span>

<span data-ttu-id="7996c-108">Aktywować lub dezaktywować inicjowania obsługi powiadomienia użytkownika inicjowania obsługi konfiguracji dla innej aplikacji SaaS w ramach konta.</span><span class="sxs-lookup"><span data-stu-id="7996c-108">You activate or deactivate account provisioning notifications as part of your user provisioning configuration for a third party SaaS application.</span></span>

![Inicjowanie obsługi użytkowników][1] 

<span data-ttu-id="7996c-110">tooactivate konto powiadomień inicjowania obsługi administracyjnej, wybierz hello powiązane pole wyboru na powitania **potwierdzenie** strony okna dialogowego, a następnie aliasów e-mail hello typu hello adresata.</span><span class="sxs-lookup"><span data-stu-id="7996c-110">tooactivate account provisioning notifications, select hello related checkbox on hello **Confirmation** dialog page, and then type hello email alias of hello recipient.</span></span>

![Powiadomienia związane z aprowizacją kont][2]

<span data-ttu-id="7996c-112">Możesz wprowadzić listę dystrybucyjną jako recipient; jest jednak toonote ważne, czy wiadomość e-mail z powiadomieniem hello zawiera tooreports łącza, które są dostępne przez administratorów usługi Azure AD hello jedynie.</span><span class="sxs-lookup"><span data-stu-id="7996c-112">You can enter a distribution list as recipient; however, it is important toonote that hello notification email contains links tooreports that are only accessible by hello Azure AD administrators.</span></span>

<span data-ttu-id="7996c-113">Jeśli masz konto inicjowania obsługi powiadomień włączone, będziesz otrzymywać wiadomości e-mail o krytyczne problemy, które są powiązane toouser inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="7996c-113">If you have account provisioning notifications enabled, you will receive emails about critical issues that are related toouser provisioning.</span></span> <span data-ttu-id="7996c-114">Jednak tooavoid przeciążenia poczty e-mail, otrzymasz tylko jednego powiadomienia e-mail na dzień każdego rozwiązania saas aplikacji hello powiadomienia e-mail jest włączone dla.</span><span class="sxs-lookup"><span data-stu-id="7996c-114">However, tooavoid an email overload, you will only receive one notification email per day for each SaaS application hello notification email is enabled for.</span></span>

## <a name="related-articles"></a><span data-ttu-id="7996c-115">Pokrewne artykuły</span><span class="sxs-lookup"><span data-stu-id="7996c-115">Related Articles</span></span>
* [<span data-ttu-id="7996c-116">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7996c-116">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="7996c-117">Automatyzowanie inicjowania obsługi administracyjnej użytkowników/anulowania zastrzeżenia tooSaaS aplikacji</span><span class="sxs-lookup"><span data-stu-id="7996c-117">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="7996c-118">Dostosowywanie mapowań atrybutów do inicjowania obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="7996c-118">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="7996c-119">Tworzenie wyrażeń na potrzeby mapowań atrybutów</span><span class="sxs-lookup"><span data-stu-id="7996c-119">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="7996c-120">Filtry zakresu dla Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="7996c-120">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="7996c-121">Przy użyciu SCIM tooenable automatyczne Inicjowanie obsługi użytkowników i grup z usługi Azure Active Directory tooapplications</span><span class="sxs-lookup"><span data-stu-id="7996c-121">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="7996c-122">Lista samouczków dotyczących tooIntegrate aplikacji SaaS</span><span class="sxs-lookup"><span data-stu-id="7996c-122">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-account-provisioning-notifications/ic766307.png
[2]: ./media/active-directory-saas-account-provisioning-notifications/ic766308.png
