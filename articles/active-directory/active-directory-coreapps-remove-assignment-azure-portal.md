---
title: "Usuń przypisanie użytkownika lub grupy z aplikacji przedsiębiorstwa w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak usunąć przypisanie dostęp użytkownika lub grupy z aplikacji przedsiębiorstwa w usłudze Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7b2d365b-ae92-477f-9702-353cc6acc5ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 02f122acfb53c2107e2b0af66c6195aa127a2c77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="e2f18-103">Usuń przypisanie użytkownika lub grupy z aplikacji przedsiębiorstwa w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e2f18-103">Remove a user or group assignment from an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="e2f18-104">To proste usunąć użytkownika lub grupy z przypisaniem dostęp do jednej z aplikacji przedsiębiorstwa w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e2f18-104">It's easy to remove a user or a group from being assigned access to one of your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="e2f18-105">Musi mieć odpowiednie uprawnienia do zarządzania aplikacjami przedsiębiorstwa, a musi być administratorem globalnym katalogu.</span><span class="sxs-lookup"><span data-stu-id="e2f18-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-remove-a-user-or-group-assignment"></a><span data-ttu-id="e2f18-106">Jak usunąć użytkownika lub przypisanie do grupy</span><span class="sxs-lookup"><span data-stu-id="e2f18-106">How do I remove a user or group assignment?</span></span>
1. <span data-ttu-id="e2f18-107">Zaloguj się do [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu.</span><span class="sxs-lookup"><span data-stu-id="e2f18-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="e2f18-108">Wybierz **więcej usług**, wprowadź **usługi Azure Active Directory** w polu tekstowym, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="e2f18-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="e2f18-109">Na **usługi Azure Active Directory - *directoryname***  bloku (to znaczy usługi Azure AD bloku katalogu zarządzasz), wybierz **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e2f18-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Otwieranie aplikacji przedsiębiorstwa](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="e2f18-111">Na **aplikacje dla przedsiębiorstw** bloku, wybierz opcję **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e2f18-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="e2f18-112">Zobaczysz listę aplikacji, którymi można zarządzać.</span><span class="sxs-lookup"><span data-stu-id="e2f18-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="e2f18-113">Na **aplikacje przedsiębiorstwa — wszystkie aplikacje** bloku, wybierz aplikację.</span><span class="sxs-lookup"><span data-stu-id="e2f18-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="e2f18-114">Na ***appname*** bloku (to znaczy bloku o nazwie wybranej aplikacji w tytule), wybierz **użytkownicy i grupy**.</span><span class="sxs-lookup"><span data-stu-id="e2f18-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Users & Groups**.</span></span>

    ![Wybieranie użytkowników lub grup](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. <span data-ttu-id="e2f18-116">Na ***appname*** **— przypisanie do grupy & użytkownika** bloku, wybierz jedną więcej użytkowników lub grup, a następnie wybierz **Usuń** polecenia.</span><span class="sxs-lookup"><span data-stu-id="e2f18-116">On the ***appname*** **- User & Group Assignment** blade, select one of more users or groups and then select the **Remove** command.</span></span> <span data-ttu-id="e2f18-117">Potwierdź decyzję w wierszu.</span><span class="sxs-lookup"><span data-stu-id="e2f18-117">Confirm your decision at the prompt.</span></span>

    ![Polecenie Remove](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a><span data-ttu-id="e2f18-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e2f18-119">Next steps</span></span>
* [<span data-ttu-id="e2f18-120">Wyświetl wszystkie moje grupy</span><span class="sxs-lookup"><span data-stu-id="e2f18-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="e2f18-121">Przypisanie użytkownika lub grupę do aplikacji w przedsiębiorstwie</span><span class="sxs-lookup"><span data-stu-id="e2f18-121">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="e2f18-122">Wyłącz logowania użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="e2f18-122">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="e2f18-123">Zmiana nazwy lub logo aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="e2f18-123">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
