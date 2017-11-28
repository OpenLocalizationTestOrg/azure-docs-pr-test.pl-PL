---
title: "Zmiana nazwy lub logo aplikacji przedsiębiorstwa w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak zmienić nazwę lub logo aplikacji niestandardowych przedsiębiorstwa w usłudze Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d01303ce-e6cb-4f3b-a4d6-ec29dfd68146
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 3e44e876dcbac704a9809ae5b3957bf94be21c48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-name-or-logo-of-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="ed9d0-103">Zmiana nazwy lub logo aplikacji przedsiębiorstwa w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ed9d0-103">Change the name or logo of an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="ed9d0-104">To proste zmienić nazwę lub logo dla aplikacji niestandardowych przedsiębiorstwa w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ed9d0-104">It's easy to change the name or logo for a custom enterprise application in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="ed9d0-105">Musi mieć odpowiednie uprawnienia, aby wprowadzić te zmiany, a musi być Twórca aplikacji niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-105">You must have the appropriate permissions to make these changes, and you must be the creator of the custom app.</span></span>

## <a name="how-do-i-change-an-enterprise-apps-name-or-logo"></a><span data-ttu-id="ed9d0-106">Jak zmienić nazwę lub logo aplikacji przedsiębiorstwa?</span><span class="sxs-lookup"><span data-stu-id="ed9d0-106">How do I change an enterprise app's name or logo?</span></span>
1. <span data-ttu-id="ed9d0-107">Zaloguj się do [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="ed9d0-108">Wybierz **więcej usług**, wprowadź **usługi Azure Active Directory** w polu tekstowym, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="ed9d0-109">Na **usługi Azure Active Directory - *directoryname***  bloku (to znaczy usługi Azure AD bloku katalogu zarządzasz), wybierz **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Otwieranie aplikacji przedsiębiorstwa](./media/active-directory-coreapps-change-app-logo-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="ed9d0-111">Na **aplikacje dla przedsiębiorstw** bloku, wybierz opcję **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="ed9d0-112">Zobaczysz listę aplikacji, którymi można zarządzać.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="ed9d0-113">Na **aplikacje przedsiębiorstwa — wszystkie aplikacje** bloku, wybierz aplikację.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="ed9d0-114">Na ***appname*** bloku (to znaczy bloku o nazwie wybranej aplikacji w tytule), wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Properties**.</span></span>

    ![Polecenie Właściwości](./media/active-directory-coreapps-change-app-logo-azure-portal/select-app.png)
7. <span data-ttu-id="ed9d0-116">Na ***appname*** **-właściwości** bloku, przeglądanie w poszukiwaniu pliku do użycia jako nowe logo lub Edytuj nazwę aplikacji, lub obie.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-116">On the ***appname*** **- Properties** blade, browse for a file to use as a new logo, or edit the app name, or both.</span></span>

    ![Zmiana polecenia logo lub nameproperties aplikacji](./media/active-directory-coreapps-change-app-logo-azure-portal/change-logo.png)
8. <span data-ttu-id="ed9d0-118">Wybierz **zapisać** polecenia.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-118">Select the **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed9d0-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ed9d0-119">Next steps</span></span>
* [<span data-ttu-id="ed9d0-120">Wyświetl wszystkie moje grupy</span><span class="sxs-lookup"><span data-stu-id="ed9d0-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="ed9d0-121">Przypisanie użytkownika lub grupę do aplikacji w przedsiębiorstwie</span><span class="sxs-lookup"><span data-stu-id="ed9d0-121">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="ed9d0-122">Usuń przypisanie użytkownika lub grupy z aplikacjami</span><span class="sxs-lookup"><span data-stu-id="ed9d0-122">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="ed9d0-123">Wyłącz logowania użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="ed9d0-123">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
