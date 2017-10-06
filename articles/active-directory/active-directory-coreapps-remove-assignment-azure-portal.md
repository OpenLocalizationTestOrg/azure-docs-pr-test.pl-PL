---
title: "aaaRemove użytkownika lub grupę przypisania z aplikacji przedsiębiorstwa w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak tooremove hello dostępu przypisania użytkownika lub grupy z aplikacji przedsiębiorstwa w usłudze Azure Active Directory"
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
ms.openlocfilehash: c067ecf59b4dedfe8f848357ca8bd545bdc610eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="17dd0-103">Usuń przypisanie użytkownika lub grupy z aplikacji przedsiębiorstwa w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17dd0-103">Remove a user or group assignment from an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="17dd0-104">Jest łatwy tooremove użytkownika lub grupę z przypisaniem tooone dostępu do aplikacji w sieci przedsiębiorstwa w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="17dd0-104">It's easy tooremove a user or a group from being assigned access tooone of your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="17dd0-105">Musi mieć hello odpowiednie uprawnienia toomanage hello przedsiębiorstwa aplikacji, a musi być administratorem globalnym katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="17dd0-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-remove-a-user-or-group-assignment"></a><span data-ttu-id="17dd0-106">Jak usunąć użytkownika lub przypisanie do grupy</span><span class="sxs-lookup"><span data-stu-id="17dd0-106">How do I remove a user or group assignment?</span></span>
1. <span data-ttu-id="17dd0-107">Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="17dd0-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="17dd0-108">Wybierz **więcej usług**, wprowadź **usługi Azure Active Directory** w hello pola tekstowego, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="17dd0-108">Select **More services**, enter **Azure Active Directory** in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="17dd0-109">Na powitania **usługi Azure Active Directory - *directoryname***  bloku (to znaczy bloku hello Azure AD dla katalogu hello są używane do zarządzania), wybierz **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="17dd0-109">On hello **Azure Active Directory - *directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Otwieranie aplikacji przedsiębiorstwa](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="17dd0-111">Na powitania **aplikacje dla przedsiębiorstw** bloku, wybierz opcję **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="17dd0-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="17dd0-112">Zobaczysz listę aplikacji hello, którymi można zarządzać.</span><span class="sxs-lookup"><span data-stu-id="17dd0-112">You'll see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="17dd0-113">Na powitania **aplikacje przedsiębiorstwa — wszystkie aplikacje** bloku, wybierz aplikację.</span><span class="sxs-lookup"><span data-stu-id="17dd0-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="17dd0-114">Na powitania ***appname*** bloku (to znaczy hello bloku o nazwie hello hello wybranej aplikacji w tytule hello) wybierz **użytkownicy i grupy**.</span><span class="sxs-lookup"><span data-stu-id="17dd0-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Users & Groups**.</span></span>

    ![Wybieranie użytkowników lub grup](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. <span data-ttu-id="17dd0-116">Na powitania ***appname*** **— przypisanie do grupy & użytkownika** bloku, wybierz jedną więcej użytkowników lub grup, a następnie wybierz hello **Usuń** polecenia.</span><span class="sxs-lookup"><span data-stu-id="17dd0-116">On hello ***appname*** **- User & Group Assignment** blade, select one of more users or groups and then select hello **Remove** command.</span></span> <span data-ttu-id="17dd0-117">Potwierdź decyzję hello w wierszu.</span><span class="sxs-lookup"><span data-stu-id="17dd0-117">Confirm your decision at hello prompt.</span></span>

    ![Polecenie Usuń hello](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a><span data-ttu-id="17dd0-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="17dd0-119">Next steps</span></span>
* [<span data-ttu-id="17dd0-120">Wyświetl wszystkie moje grupy</span><span class="sxs-lookup"><span data-stu-id="17dd0-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="17dd0-121">Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan</span><span class="sxs-lookup"><span data-stu-id="17dd0-121">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="17dd0-122">Wyłącz logowania użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="17dd0-122">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="17dd0-123">Zmiana nazwy hello lub logo aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="17dd0-123">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
