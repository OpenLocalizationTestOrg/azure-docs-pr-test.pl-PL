---
title: Przypisywanie grup do aplikacji Azure AD | Dokumentacja firmy Microsoft
description: "Jak zaimplementować przypisanie do grupy aplikacji Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: 29b5ba89-a1c7-4f1f-a294-248a40106617
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
robots: noindex
ms.openlocfilehash: e0b0b87a454db96747f024e81882fe83d62fdbe2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="assign-azure-active-directory-groups-to-an-application"></a><span data-ttu-id="e5f0a-103">Przypisywanie grup usługi Azure Active Directory do aplikacji</span><span class="sxs-lookup"><span data-stu-id="e5f0a-103">Assign Azure Active Directory groups to an application</span></span>
<span data-ttu-id="e5f0a-104">Przed przypisaniem użytkowników i grup do aplikacji może wymagać przypisanie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e5f0a-104">Before you can assign users and groups to an application, you must require user assignment.</span></span> <span data-ttu-id="e5f0a-105">Aby dowiedzieć się, jak wymagają przypisania użytkownika, zobacz [wymagające przypisanie użytkownika](active-directory-applications-guiding-developers-requiring-user-assignment.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="e5f0a-105">To learn how to require user assignment, see the [Requiring User Assignment](active-directory-applications-guiding-developers-requiring-user-assignment.md) article.</span></span>

<span data-ttu-id="e5f0a-106">W tym artykule przyjęto założenie, że utworzono już grup w usłudze active directory, używanego dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e5f0a-106">This article assumes that you have already created groups in the active directory you are using for this application.</span></span>

## <a name="assigning-groups-to-an-application"></a><span data-ttu-id="e5f0a-107">Przypisywanie grup do aplikacji</span><span class="sxs-lookup"><span data-stu-id="e5f0a-107">Assigning Groups to an Application</span></span>
1. <span data-ttu-id="e5f0a-108">Zaloguj się do portalu Azure przy użyciu konta administratora.</span><span class="sxs-lookup"><span data-stu-id="e5f0a-108">Log in to the Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="e5f0a-109">Polecenie **wszystkie elementy** elementu w menu głównym.</span><span class="sxs-lookup"><span data-stu-id="e5f0a-109">Click on the **All Items** item in the main menu.</span></span>
3. <span data-ttu-id="e5f0a-110">Wybierz katalog, w używanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e5f0a-110">Choose the directory you are using for the application.</span></span>
4. <span data-ttu-id="e5f0a-111">Polecenie **aplikacji** kartę.</span><span class="sxs-lookup"><span data-stu-id="e5f0a-111">Click on the **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="e5f0a-112">Wybierz aplikację z listy aplikacji skojarzonych z tym katalogiem.</span><span class="sxs-lookup"><span data-stu-id="e5f0a-112">Select the application from the list of applications associated with this directory.</span></span>
6. <span data-ttu-id="e5f0a-113">Kliknij przycisk **użytkowników i grup** kartę.</span><span class="sxs-lookup"><span data-stu-id="e5f0a-113">Click the **USERS AND GROUPS** tab.</span></span>
7. <span data-ttu-id="e5f0a-114">Filtrowanie listy grup w usłudze active directory przy użyciu **grup** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="e5f0a-114">Filter the list of groups in your active directory by using the **Groups** dropdown list.</span></span>
8. <span data-ttu-id="e5f0a-115">Wybierz grupę.</span><span class="sxs-lookup"><span data-stu-id="e5f0a-115">Select the group.</span></span>
9. <span data-ttu-id="e5f0a-116">Kliknij przycisk **PRZYPISAĆ**.</span><span class="sxs-lookup"><span data-stu-id="e5f0a-116">Click **ASSIGN**.</span></span>
10. <span data-ttu-id="e5f0a-117">Kliknij przycisk **tak** po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="e5f0a-117">Click **yes** when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5f0a-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e5f0a-118">Next Steps</span></span>
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
