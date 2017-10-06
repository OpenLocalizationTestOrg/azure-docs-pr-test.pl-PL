---
title: aaaAssign grup aplikacji tooAzure AD | Dokumentacja firmy Microsoft
description: Jak tooimplement grupy przypisania dla aplikacji platformy Azure.
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
ms.openlocfilehash: 086619df09c13bf259afc3128d45ed804b99e519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-azure-active-directory-groups-tooan-application"></a><span data-ttu-id="cd813-103">Przypisywanie grup usługi Azure Active Directory tooan aplikacji</span><span class="sxs-lookup"><span data-stu-id="cd813-103">Assign Azure Active Directory groups tooan application</span></span>
<span data-ttu-id="cd813-104">Przed przypisaniem użytkowników i grup tooan aplikacji może wymagać przypisanie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cd813-104">Before you can assign users and groups tooan application, you must require user assignment.</span></span> <span data-ttu-id="cd813-105">toolearn jak toorequire przypisanie użytkownika, zobacz hello [wymagające przypisanie użytkownika](active-directory-applications-guiding-developers-requiring-user-assignment.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="cd813-105">toolearn how toorequire user assignment, see hello [Requiring User Assignment](active-directory-applications-guiding-developers-requiring-user-assignment.md) article.</span></span>

<span data-ttu-id="cd813-106">W tym artykule przyjęto założenie, że utworzono już grup w usłudze active directory hello używanego dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cd813-106">This article assumes that you have already created groups in hello active directory you are using for this application.</span></span>

## <a name="assigning-groups-tooan-application"></a><span data-ttu-id="cd813-107">Przypisywanie tooan grup aplikacji</span><span class="sxs-lookup"><span data-stu-id="cd813-107">Assigning Groups tooan Application</span></span>
1. <span data-ttu-id="cd813-108">Zaloguj się za toohello portalu Azure przy użyciu konta administratora.</span><span class="sxs-lookup"><span data-stu-id="cd813-108">Log in toohello Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="cd813-109">Polecenie hello **wszystkie elementy** element w menu głównym hello.</span><span class="sxs-lookup"><span data-stu-id="cd813-109">Click on hello **All Items** item in hello main menu.</span></span>
3. <span data-ttu-id="cd813-110">Wybierz katalog hello, używanego dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="cd813-110">Choose hello directory you are using for hello application.</span></span>
4. <span data-ttu-id="cd813-111">Polecenie hello **aplikacji** kartę.</span><span class="sxs-lookup"><span data-stu-id="cd813-111">Click on hello **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="cd813-112">Wybierz aplikację hello z hello listy aplikacji skojarzonych z tym katalogiem.</span><span class="sxs-lookup"><span data-stu-id="cd813-112">Select hello application from hello list of applications associated with this directory.</span></span>
6. <span data-ttu-id="cd813-113">Kliknij przycisk hello **użytkowników i grup** kartę.</span><span class="sxs-lookup"><span data-stu-id="cd813-113">Click hello **USERS AND GROUPS** tab.</span></span>
7. <span data-ttu-id="cd813-114">Lista hello filtrów grup w usłudze active directory przy użyciu hello **grup** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="cd813-114">Filter hello list of groups in your active directory by using hello **Groups** dropdown list.</span></span>
8. <span data-ttu-id="cd813-115">Wybierz grupę hello.</span><span class="sxs-lookup"><span data-stu-id="cd813-115">Select hello group.</span></span>
9. <span data-ttu-id="cd813-116">Kliknij przycisk **PRZYPISAĆ**.</span><span class="sxs-lookup"><span data-stu-id="cd813-116">Click **ASSIGN**.</span></span>
10. <span data-ttu-id="cd813-117">Kliknij przycisk **tak** po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="cd813-117">Click **yes** when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd813-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cd813-118">Next Steps</span></span>
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
