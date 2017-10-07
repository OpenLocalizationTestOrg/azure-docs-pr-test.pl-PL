---
title: "aaaFind się, kiedy określony użytkownik będą mogli tooaccess aplikacji | Dokumentacja firmy Microsoft"
description: "Jak toofind się, gdy użytkownik niezwykle ważne być tooaccess stanie aplikacji została skonfigurowana dla Inicjowanie obsługi użytkowników z usługą Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: bb9520499dcc8bbbe6fae05c5238c8852815ea0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-tooaccess-an-application"></a><span data-ttu-id="00929-103">Ustalić, kiedy określony użytkownik będzie możliwe tooaccess aplikacji</span><span class="sxs-lookup"><span data-stu-id="00929-103">Find out when a specific user will be able tooaccess an application</span></span>
<span data-ttu-id="00929-104">Używając użytkownika automatycznego inicjowania obsługi administracyjnej za pomocą aplikacji, usługi Azure AD automatycznie udostępniania i aktualizowanie kont użytkowników w aplikacji na podstawie takich elementów, jak [przypisania użytkowników i grup](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) w odstępach zaplanowanego czasu, zazwyczaj co 10 minut.</span><span class="sxs-lookup"><span data-stu-id="00929-104">When using automatic user provisioning with an application, Azure AD automatically provision and update user accounts in an app based on things like [user and group assignment](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) at a regularly scheduled time interval, typically every 10 minutes.</span></span>

## <a name="how-long-does-it-take"></a><span data-ttu-id="00929-105">Jak długo trwa?</span><span class="sxs-lookup"><span data-stu-id="00929-105">How long does it take?</span></span>

<span data-ttu-id="00929-106">Hello czas potrzebny toobe danego użytkownika, udostępnione zależy od głównie czy już wystąpił początkową synchronizację "pełnej".</span><span class="sxs-lookup"><span data-stu-id="00929-106">hello time it takes for a given user toobe provisioned depends mainly on whether or not an initial “full” sync has already occurred.</span></span>

<span data-ttu-id="00929-107">Witaj pierwsza synchronizacja między usługą Azure AD i aplikacji może potrwać od godziny tooseveral 20 minut, w zależności od wielkości hello katalogu hello Azure AD i hello liczbę użytkowników w zakresie obsługi.</span><span class="sxs-lookup"><span data-stu-id="00929-107">hello first sync between Azure AD and an app can take anywhere from 20 minutes tooseveral hours, depending on hello size of hello Azure AD directory and hello number of users in scope for provisioning.</span></span> 

<span data-ttu-id="00929-108">Kolejne synchronizacje po początkowej synchronizacji hello przebiegać szybciej (np. w ciągu 10 minut), jak znaki wodne, przedstawiające stan hello obu systemów po początkowej synchronizacji hello, poprawa wydajności kolejne synchronizacje magazyny hello inicjowania obsługi usługi.</span><span class="sxs-lookup"><span data-stu-id="00929-108">Subsequent syncs after hello initial sync be faster (e.g. within 10 minutes), as hello provisioning service stores watermarks that represent hello state of both systems after hello initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-toocheck-hello-status-of-a-user"></a><span data-ttu-id="00929-109">Jak toocheck hello stanu użytkownika</span><span class="sxs-lookup"><span data-stu-id="00929-109">How toocheck hello status of a user</span></span>

<span data-ttu-id="00929-110">Stan inicjowania obsługi administracyjnej hello toosee dla wybranego użytkownika, należy skontaktować się hello dzienniki inspekcji w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00929-110">toosee hello provisioning status for a selected user, consult hello Audit logs in Azure AD.</span></span>

<span data-ttu-id="00929-111">Hello inicjowania obsługi dzienników inspekcji można uzyskać w portalu Azure w hello hello **usługi Azure Active Directory &gt; aplikacje przedsiębiorstwa &gt; \[Nazwa aplikacji\] &gt; dzienniki inspekcji**kartę. Filtr hello dzienniki na powitania **Inicjowanie obsługi konta** tooonly kategorii Zobacz hello inicjowania obsługi zdarzeń dla danej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="00929-111">hello provisioning audit logs can be accessed in hello Azure portal, in hello **Azure Active Directory &gt; Enterprise Apps &gt; \[Application Name\] &gt; Audit Logs** tab. Filter hello logs on hello **Account Provisioning** category tooonly see hello provisioning events for that app.</span></span> <span data-ttu-id="00929-112">Można wyszukiwać użytkowników na podstawie hello "dopasowania Identyfikatora" skonfigurowanego dla nich w hello atrybutu mapowania.</span><span class="sxs-lookup"><span data-stu-id="00929-112">You can search for users based on hello “matching ID” that was configured for them in hello attribute mappings.</span></span> 

<span data-ttu-id="00929-113">Na przykład, jeśli skonfigurowano hello "główna nazwa użytkownika" lub "adres e-mail" jako hello dopasowanie atrybutu na stronie powitania usługi Azure AD, a użytkownik hello udostępniania nie ma wartość "audrey@contoso.com", następnie dzienniki inspekcji hello wyszukiwania dla"audrey@contoso.com", a następnie przejrzyj zwracane wpisy.</span><span class="sxs-lookup"><span data-stu-id="00929-113">For example, if you configured hello “user principal name” or “email address” as hello matching attribute on hello Azure AD side, and hello user not being provisioning has a value of “audrey@contoso.com”, then search hello audit logs for “audrey@contoso.com” and review then entries returned.</span></span>

<span data-ttu-id="00929-114">Witaj udostępniania inspekcji rejestruje rekord hello wszystkie operacje wykonywane przez hello inicjowania obsługi usługi, w tym:</span><span class="sxs-lookup"><span data-stu-id="00929-114">hello provisioning audit logs record all hello operations performed by hello provisioning service, including:</span></span>

* <span data-ttu-id="00929-115">Podczas badania usługi Azure AD dla przypisanych użytkowników, które znajdują się w zakresie alokacji</span><span class="sxs-lookup"><span data-stu-id="00929-115">Querying Azure AD for assigned users that are in scope for provisioning</span></span>
* <span data-ttu-id="00929-116">Wykonywanie zapytania hello docelowej aplikacji hello istnienia tych użytkowników</span><span class="sxs-lookup"><span data-stu-id="00929-116">Querying hello target app for hello existence of those users</span></span>
* <span data-ttu-id="00929-117">Porównanie obiektów użytkownika hello między hello systemu</span><span class="sxs-lookup"><span data-stu-id="00929-117">Comparing hello user objects between hello system</span></span>
* <span data-ttu-id="00929-118">Dodawanie, aktualizowanie lub wyłączanie hello konta użytkownika w systemie docelowym hello na podstawie porównania hello</span><span class="sxs-lookup"><span data-stu-id="00929-118">Adding, updating, or disabling hello user account in hello target system based on hello comparison</span></span>

## <a name="next-steps"></a><span data-ttu-id="00929-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="00929-119">Next steps</span></span>
<span data-ttu-id="00929-120">[Automatyzowanie Inicjowanie obsługi użytkowników i anulowania zastrzeżenia tooSaaS aplikacji za pomocą usługi Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span><span class="sxs-lookup"><span data-stu-id="00929-120">[Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span></span>
