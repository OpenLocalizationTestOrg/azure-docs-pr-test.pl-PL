---
title: "Wyłącz logowania użytkowników dla aplikacji przedsiębiorstwa w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak wyłączyć aplikację przedsiębiorstwa, dzięki czemu użytkownicy nie mogą Zaloguj się do niego w usłudze Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a27562f9-18dc-42e8-9fee-5419566f8fd7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 5d27046370eada0c371c94fb573fa1bcf536f7cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="3a7df-103">Wyłącz logowania użytkowników dla aplikacji przedsiębiorstwa w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3a7df-103">Disable user sign-ins for an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="3a7df-104">To proste wyłączyć aplikację przedsiębiorstwa, dzięki czemu użytkownicy nie mogą Zaloguj się do niego w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3a7df-104">It's easy to disable an enterprise application so that no users may sign in to it in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="3a7df-105">Musi mieć odpowiednie uprawnienia do zarządzania aplikacjami przedsiębiorstwa, a musi być administratorem globalnym katalogu.</span><span class="sxs-lookup"><span data-stu-id="3a7df-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-disable-user-sign-ins"></a><span data-ttu-id="3a7df-106">Jak wyłączyć logowania użytkowników?</span><span class="sxs-lookup"><span data-stu-id="3a7df-106">How do I disable user sign-ins?</span></span>
1. <span data-ttu-id="3a7df-107">Zaloguj się do [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu.</span><span class="sxs-lookup"><span data-stu-id="3a7df-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="3a7df-108">Wybierz **więcej usług**, wprowadź **usługi Azure Active Directory** w polu tekstowym, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3a7df-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="3a7df-109">Na **usługi Azure Active Directory** -  ***directoryname*** bloku (to znaczy usługi Azure AD bloku katalogu zarządzasz), wybierz **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="3a7df-109">On the **Azure Active Directory** -  ***directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Otwieranie aplikacji przedsiębiorstwa](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="3a7df-111">Na **aplikacje dla przedsiębiorstw** bloku, wybierz opcję **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="3a7df-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="3a7df-112">Możesz wyświetlić listę aplikacji, którymi można zarządzać.</span><span class="sxs-lookup"><span data-stu-id="3a7df-112">You see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="3a7df-113">Na **aplikacje przedsiębiorstwa — wszystkie aplikacje** bloku, wybierz aplikację.</span><span class="sxs-lookup"><span data-stu-id="3a7df-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="3a7df-114">Na ***appname*** bloku (to znaczy bloku o nazwie wybranej aplikacji w tytule), wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="3a7df-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Properties**.</span></span>

    ![Polecenie wszystkie aplikacje](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. <span data-ttu-id="3a7df-116">Na ***appname*** - **właściwości** bloku, wybierz opcję **nr** dla **dostępny dla użytkowników do logowania?**.</span><span class="sxs-lookup"><span data-stu-id="3a7df-116">On the ***appname*** - **Properties** blade, select **No** for **Enabled for users to sign-in?**.</span></span>
8. <span data-ttu-id="3a7df-117">Wybierz **zapisać** polecenia.</span><span class="sxs-lookup"><span data-stu-id="3a7df-117">Select the **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a7df-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3a7df-118">Next steps</span></span>
* [<span data-ttu-id="3a7df-119">Zobacz wszystkie moje grupy</span><span class="sxs-lookup"><span data-stu-id="3a7df-119">See all my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="3a7df-120">Przypisanie użytkownika lub grupę do aplikacji w przedsiębiorstwie</span><span class="sxs-lookup"><span data-stu-id="3a7df-120">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="3a7df-121">Usuń przypisanie użytkownika lub grupy z aplikacjami</span><span class="sxs-lookup"><span data-stu-id="3a7df-121">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="3a7df-122">Zmiana nazwy lub logo aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="3a7df-122">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
