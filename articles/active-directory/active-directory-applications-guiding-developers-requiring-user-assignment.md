---
title: "Wymagaj przypisanie użytkownika — usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Jak wymagają przypisania użytkownika dla aplikacji platformy Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: 30b78cba-1e0f-472f-8314-f2250a9b91c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
robots: noindex
ms.openlocfilehash: 079b806c041a4a21e9350342867aee581c57bf45
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-and-applications-require-user-assignment"></a><span data-ttu-id="3f502-103">Usługi Azure AD i aplikacji: wymagają przypisania użytkownika</span><span class="sxs-lookup"><span data-stu-id="3f502-103">Azure AD and applications: Require user assignment</span></span>
## <a name="requiring-user-assignment"></a><span data-ttu-id="3f502-104">Wymaganie przypisanie użytkownika</span><span class="sxs-lookup"><span data-stu-id="3f502-104">Requiring User Assignment</span></span>
1. <span data-ttu-id="3f502-105">Zaloguj się do portalu Azure przy użyciu konta administratora.</span><span class="sxs-lookup"><span data-stu-id="3f502-105">Log in to the Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="3f502-106">Polecenie **wszystkie elementy** elementu w menu głównym.</span><span class="sxs-lookup"><span data-stu-id="3f502-106">Click on the **All Items** item in the main menu.</span></span>
3. <span data-ttu-id="3f502-107">Wybierz katalog, w używanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3f502-107">Choose the directory you are using for the application.</span></span>
4. <span data-ttu-id="3f502-108">Polecenie **aplikacji** kartę.</span><span class="sxs-lookup"><span data-stu-id="3f502-108">Click on the **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="3f502-109">Wybierz aplikację z listy aplikacji skojarzonych z tym katalogiem.</span><span class="sxs-lookup"><span data-stu-id="3f502-109">Select the application from the list of applications associated with this directory.</span></span>
6. <span data-ttu-id="3f502-110">Kliknij przycisk **Konfiguruj** kartę.</span><span class="sxs-lookup"><span data-stu-id="3f502-110">Click the **CONFIGURE** tab.</span></span>
7. <span data-ttu-id="3f502-111">Zmień **użytkownika przypisania wymagane do dostępu do aplikacji** przełącznik, aby tak.</span><span class="sxs-lookup"><span data-stu-id="3f502-111">Change the **User Assignment Required to Access App** toggle to Yes.</span></span>
8. <span data-ttu-id="3f502-112">Kliknij przycisk **zapisać** u dołu ekranu.</span><span class="sxs-lookup"><span data-stu-id="3f502-112">Click the **Save** button at the bottom of the screen.</span></span>

<span data-ttu-id="3f502-113">Teraz musisz przypisać użytkowników i/lub grup do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3f502-113">You will now have to assign users and/or groups to the application.</span></span> <span data-ttu-id="3f502-114">Zobacz [przypisywania użytkowników do aplikacji](active-directory-applications-guiding-developers-assigning-users.md) i [przypisanie grupy do aplikacji](active-directory-applications-guiding-developers-assigning-groups.md).</span><span class="sxs-lookup"><span data-stu-id="3f502-114">See [Assigning users to an application](active-directory-applications-guiding-developers-assigning-users.md) and [Assigning groups to an application](active-directory-applications-guiding-developers-assigning-groups.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f502-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3f502-115">Next Steps</span></span>
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
