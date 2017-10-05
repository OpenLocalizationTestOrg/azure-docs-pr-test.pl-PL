---
title: "Przypisanie użytkownika lub grupę do aplikacji przedsiębiorstwa w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak wybrać aplikację przedsiębiorstwa przypisać użytkownika lub grupę do niego w usłudze Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5817ad48-d916-492b-a8d0-2ade8c50a224
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: ee784704ada9238b5cd048f99aaa4cb192ec7d57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="assign-a-user-or-group-to-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="8be2f-103">Przypisanie użytkownika lub grupę do aplikacji przedsiębiorstwa w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8be2f-103">Assign a user or group to an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="8be2f-104">To proste przypisać użytkownika lub grupę do aplikacji w sieci przedsiębiorstwa w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8be2f-104">It's easy to assign a user or a group to your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="8be2f-105">Musi mieć odpowiednie uprawnienia do zarządzania aplikacjami przedsiębiorstwa, a musi być administratorem globalnym katalogu.</span><span class="sxs-lookup"><span data-stu-id="8be2f-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-assign-user-access-to-an-enterprise-app"></a><span data-ttu-id="8be2f-106">Jak przypisać dostępu użytkownika do aplikacji przedsiębiorstwa?</span><span class="sxs-lookup"><span data-stu-id="8be2f-106">How do I assign user access to an enterprise app?</span></span>
1. <span data-ttu-id="8be2f-107">Zaloguj się do [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu.</span><span class="sxs-lookup"><span data-stu-id="8be2f-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="8be2f-108">Wybierz **więcej usług**wprowadź Azure Active Directory w polu tekstowym, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="8be2f-108">Select **More services**, enter Azure Active Directory in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="8be2f-109">Na **usługi Azure Active Directory - *directoryname***  bloku (to znaczy usługi Azure AD bloku katalogu zarządzasz), wybierz **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="8be2f-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Otwieranie aplikacji przedsiębiorstwa](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="8be2f-111">Na **aplikacje dla przedsiębiorstw** bloku, wybierz opcję **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8be2f-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="8be2f-112">Zobaczysz listę aplikacji, którymi można zarządzać.</span><span class="sxs-lookup"><span data-stu-id="8be2f-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="8be2f-113">Na **aplikacje przedsiębiorstwa — wszystkie aplikacje** bloku, wybierz aplikację.</span><span class="sxs-lookup"><span data-stu-id="8be2f-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="8be2f-114">Na ***appname*** bloku (to znaczy bloku o nazwie wybranej aplikacji w tytule), wybierz **użytkownicy i grupy**.</span><span class="sxs-lookup"><span data-stu-id="8be2f-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Users & Groups**.</span></span>

    ![Polecenie wszystkie aplikacje](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. <span data-ttu-id="8be2f-116">Na ***appname*** **— przypisanie do grupy & użytkownika** bloku, wybierz opcję **Dodaj** polecenia.</span><span class="sxs-lookup"><span data-stu-id="8be2f-116">On the ***appname*** **- User & Group Assignment** blade, select the **Add** command.</span></span>
8. <span data-ttu-id="8be2f-117">Na **Dodaj przydziału** bloku, wybierz opcję **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8be2f-117">On the **Add Assignment** blade, select **Users and groups**.</span></span>

    ![Przypisanie użytkownika lub grupę do aplikacji](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. <span data-ttu-id="8be2f-119">Na **użytkowników i grup** bloku, wybierz jeden lub więcej użytkowników lub grup z listy, a następnie wybierz **wybierz** przycisk w dolnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="8be2f-119">On the **Users and groups** blade, select one or more users or groups from the list and then select the **Select** button at the bottom of the blade.</span></span>
10. <span data-ttu-id="8be2f-120">Na **Dodaj przydziału** bloku, wybierz opcję **roli**.</span><span class="sxs-lookup"><span data-stu-id="8be2f-120">On the **Add Assignment** blade, select **Role**.</span></span> <span data-ttu-id="8be2f-121">Następnie na **wybierz rolę** bloku, wybierz rolę do zastosowania do wybranych użytkowników lub grup, a następnie wybierz **OK** przycisk w dolnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="8be2f-121">Then, on the **Select Role** blade, select a role to apply to the selected users or groups, and then select the **OK** button at the bottom of the blade.</span></span>
11. <span data-ttu-id="8be2f-122">Na **Dodaj przydziału** bloku, wybierz opcję **przypisać** przycisk w dolnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="8be2f-122">On the **Add Assignment** blade, select the **Assign** button at the bottom of the blade.</span></span> <span data-ttu-id="8be2f-123">Przypisanych użytkowników lub grup, będzie mieć uprawnienia określone przez wybraną rolę dla tej aplikacji przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="8be2f-123">The assigned users or groups will have the permissions defined by the selected role for this enterprise app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8be2f-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8be2f-124">Next steps</span></span>
* [<span data-ttu-id="8be2f-125">Wyświetl wszystkie moje grupy</span><span class="sxs-lookup"><span data-stu-id="8be2f-125">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="8be2f-126">Usuń przypisanie użytkownika lub grupy z aplikacjami</span><span class="sxs-lookup"><span data-stu-id="8be2f-126">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="8be2f-127">Wyłącz logowania użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="8be2f-127">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="8be2f-128">Zmiana nazwy lub logo aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="8be2f-128">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
