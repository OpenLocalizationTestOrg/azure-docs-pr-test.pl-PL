---
title: "aaaDisable logowania użytkowników dla aplikacji przedsiębiorstwa w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak toodisable aplikacji przedsiębiorstwa, aby użytkownicy nie mogą zalogować tooit w usłudze Azure Active Directory"
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
ms.openlocfilehash: 4c560b59359d433b0852a7606cc2cc0204866234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="25c9e-103">Wyłącz logowania użytkowników dla aplikacji przedsiębiorstwa w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25c9e-103">Disable user sign-ins for an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="25c9e-104">Jest łatwy toodisable aplikacji dla przedsiębiorstw, dzięki czemu użytkownicy nie mogą zalogować tooit w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="25c9e-104">It's easy toodisable an enterprise application so that no users may sign in tooit in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="25c9e-105">Musi mieć hello odpowiednie uprawnienia toomanage hello przedsiębiorstwa aplikacji, a musi być administratorem globalnym katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="25c9e-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-disable-user-sign-ins"></a><span data-ttu-id="25c9e-106">Jak wyłączyć logowania użytkowników?</span><span class="sxs-lookup"><span data-stu-id="25c9e-106">How do I disable user sign-ins?</span></span>
1. <span data-ttu-id="25c9e-107">Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="25c9e-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="25c9e-108">Wybierz **więcej usług**, wprowadź **usługi Azure Active Directory** w hello pola tekstowego, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="25c9e-108">Select **More services**, enter **Azure Active Directory** in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="25c9e-109">Na powitania **usługi Azure Active Directory** -  ***directoryname*** bloku (to znaczy bloku hello Azure AD dla katalogu hello są używane do zarządzania), wybierz **aplikacjedlaprzedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="25c9e-109">On hello **Azure Active Directory** -  ***directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Otwieranie aplikacji przedsiębiorstwa](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="25c9e-111">Na powitania **aplikacje dla przedsiębiorstw** bloku, wybierz opcję **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="25c9e-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="25c9e-112">Zostanie wyświetlona lista aplikacji hello, którymi można zarządzać.</span><span class="sxs-lookup"><span data-stu-id="25c9e-112">You see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="25c9e-113">Na powitania **aplikacje przedsiębiorstwa — wszystkie aplikacje** bloku, wybierz aplikację.</span><span class="sxs-lookup"><span data-stu-id="25c9e-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="25c9e-114">Na powitania ***appname*** bloku (to znaczy hello bloku o nazwie hello hello wybranej aplikacji w tytule hello) wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="25c9e-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Properties**.</span></span>

    ![Wybieranie hello wszystkie polecenia aplikacji](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. <span data-ttu-id="25c9e-116">Na powitania ***appname*** - **właściwości** bloku, wybierz opcję **nr** dla **dostępny dla użytkowników w toosign?**.</span><span class="sxs-lookup"><span data-stu-id="25c9e-116">On hello ***appname*** - **Properties** blade, select **No** for **Enabled for users toosign-in?**.</span></span>
8. <span data-ttu-id="25c9e-117">Wybierz hello **zapisać** polecenia.</span><span class="sxs-lookup"><span data-stu-id="25c9e-117">Select hello **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25c9e-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="25c9e-118">Next steps</span></span>
* [<span data-ttu-id="25c9e-119">Zobacz wszystkie moje grupy</span><span class="sxs-lookup"><span data-stu-id="25c9e-119">See all my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="25c9e-120">Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan</span><span class="sxs-lookup"><span data-stu-id="25c9e-120">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="25c9e-121">Usuń przypisanie użytkownika lub grupy z aplikacjami</span><span class="sxs-lookup"><span data-stu-id="25c9e-121">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="25c9e-122">Zmiana nazwy hello lub logo aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="25c9e-122">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
