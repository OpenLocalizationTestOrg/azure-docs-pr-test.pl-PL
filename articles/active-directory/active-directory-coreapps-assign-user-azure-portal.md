---
title: "aaaAssign użytkownika lub grupę tooan przedsiębiorstwa aplikacji w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak tooselect tooassign aplikacji organizacji użytkownika lub grupę tooit w usłudze Azure Active Directory"
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
ms.openlocfilehash: 86c11f19892b9c947a5331677c17759178ed2806
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-or-group-tooan-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="e62da-103">Przypisywanie użytkownikowi lub grupie tooan przedsiębiorstwa aplikacji w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e62da-103">Assign a user or group tooan enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="e62da-104">Jest łatwy tooassign użytkownika lub grupy tooyour przedsiębiorstwa aplikacji w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e62da-104">It's easy tooassign a user or a group tooyour enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="e62da-105">Musi mieć hello odpowiednie uprawnienia toomanage hello przedsiębiorstwa aplikacji, a musi być administratorem globalnym katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="e62da-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-assign-user-access-tooan-enterprise-app"></a><span data-ttu-id="e62da-106">Jak przypisać aplikację przedsiębiorstwa tooan dostępu użytkownika?</span><span class="sxs-lookup"><span data-stu-id="e62da-106">How do I assign user access tooan enterprise app?</span></span>
1. <span data-ttu-id="e62da-107">Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="e62da-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="e62da-108">Wybierz **więcej usług**, wprowadź w polu tekstowym hello Azure Active Directory, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="e62da-108">Select **More services**, enter Azure Active Directory in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="e62da-109">Na powitania **usługi Azure Active Directory - *directoryname***  bloku (to znaczy bloku hello Azure AD dla katalogu hello są używane do zarządzania), wybierz **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e62da-109">On hello **Azure Active Directory - *directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Otwieranie aplikacji przedsiębiorstwa](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="e62da-111">Na powitania **aplikacje dla przedsiębiorstw** bloku, wybierz opcję **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e62da-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="e62da-112">Zobaczysz listę aplikacji hello, którymi można zarządzać.</span><span class="sxs-lookup"><span data-stu-id="e62da-112">You'll see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="e62da-113">Na powitania **aplikacje przedsiębiorstwa — wszystkie aplikacje** bloku, wybierz aplikację.</span><span class="sxs-lookup"><span data-stu-id="e62da-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="e62da-114">Na powitania ***appname*** bloku (to znaczy hello bloku o nazwie hello hello wybranej aplikacji w tytule hello) wybierz **użytkownicy i grupy**.</span><span class="sxs-lookup"><span data-stu-id="e62da-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Users & Groups**.</span></span>

    ![Wybieranie hello wszystkie polecenia aplikacji](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. <span data-ttu-id="e62da-116">Na powitania ***appname*** **— przypisanie do grupy & użytkownika** bloku, wybierz hello **Dodaj** polecenia.</span><span class="sxs-lookup"><span data-stu-id="e62da-116">On hello ***appname*** **- User & Group Assignment** blade, select hello **Add** command.</span></span>
8. <span data-ttu-id="e62da-117">Na powitania **Dodaj przydziału** bloku, wybierz opcję **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e62da-117">On hello **Add Assignment** blade, select **Users and groups**.</span></span>

    ![Przypisywanie użytkownikowi lub grupie aplikacji toohello](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. <span data-ttu-id="e62da-119">Na powitania **użytkowników i grup** bloku, wybierz jeden lub więcej użytkowników lub grup z hello listy, a następnie wybierz hello **wybierz** przycisk u dołu hello hello bloku.</span><span class="sxs-lookup"><span data-stu-id="e62da-119">On hello **Users and groups** blade, select one or more users or groups from hello list and then select hello **Select** button at hello bottom of hello blade.</span></span>
10. <span data-ttu-id="e62da-120">Na powitania **Dodaj przydziału** bloku, wybierz opcję **roli**.</span><span class="sxs-lookup"><span data-stu-id="e62da-120">On hello **Add Assignment** blade, select **Role**.</span></span> <span data-ttu-id="e62da-121">Następnie na powitania **wybierz rolę** bloku, wybierz toohello tooapply roli wybrane użytkowników lub grup, a następnie wybierz hello **OK** przycisk u dołu hello hello bloku.</span><span class="sxs-lookup"><span data-stu-id="e62da-121">Then, on hello **Select Role** blade, select a role tooapply toohello selected users or groups, and then select hello **OK** button at hello bottom of hello blade.</span></span>
11. <span data-ttu-id="e62da-122">Na powitania **Dodaj przydziału** bloku, wybierz hello **przypisać** przycisk u dołu hello hello bloku.</span><span class="sxs-lookup"><span data-stu-id="e62da-122">On hello **Add Assignment** blade, select hello **Assign** button at hello bottom of hello blade.</span></span> <span data-ttu-id="e62da-123">Witaj przypisać użytkowników lub grupy będą mieli uprawnienia hello zdefiniowane przez hello wybranej roli dla tej aplikacji przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="e62da-123">hello assigned users or groups will have hello permissions defined by hello selected role for this enterprise app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e62da-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e62da-124">Next steps</span></span>
* [<span data-ttu-id="e62da-125">Wyświetl wszystkie moje grupy</span><span class="sxs-lookup"><span data-stu-id="e62da-125">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="e62da-126">Usuń przypisanie użytkownika lub grupy z aplikacjami</span><span class="sxs-lookup"><span data-stu-id="e62da-126">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="e62da-127">Wyłącz logowania użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="e62da-127">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="e62da-128">Zmiana nazwy hello lub logo aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="e62da-128">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
