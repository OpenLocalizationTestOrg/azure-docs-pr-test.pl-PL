---
title: "aaaUsing grupy tooSaaS dostępu toomanage aplikacji | Dokumentacja firmy Microsoft"
description: "Jak toouse grup w usłudze Azure Active Directory — wersja Premium lub podstawowa tooassign dostęp do aplikacji tooSaaS, które są zintegrowane z usługą Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: it-pro;oldportal
ms.openlocfilehash: f45ea4472b3d88e8ea514af3db31b4cc9ea68d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-group-toomanage-access-toosaas-applications"></a><span data-ttu-id="8c53c-103">Przy użyciu aplikacji tooSaaS grupy toomanage dostępu</span><span class="sxs-lookup"><span data-stu-id="8c53c-103">Using a group toomanage access tooSaaS applications</span></span>
<span data-ttu-id="8c53c-104">Za pomocą usługi Azure Active Directory (Azure AD) z licencją Azure AD Premium lub usługi Azure AD podstawowa, można użyć grup tooassign dostępu tooa SaaS aplikacji, która jest zintegrowany z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c53c-104">Using Azure Active Directory (Azure AD) with an Azure AD Premium or Azure AD Basic license, you can use groups tooassign access tooa SaaS application that's integrated with Azure AD.</span></span> <span data-ttu-id="8c53c-105">Na przykład jeśli chcesz tooassign dostępu dla hello marketing działu toouse pięciu różnych aplikacji SaaS, można utworzyć grupę, która zawiera użytkowników hello w dziale marketingu hello i przypisz tej grupy toothese pięć SaaS aplikacje, które są wymagane przez dział marketingu hello.</span><span class="sxs-lookup"><span data-stu-id="8c53c-105">For example, if you want tooassign access for hello marketing department toouse five different SaaS applications, you can create a group that contains hello users in hello marketing department, and then assign that group toothese five SaaS applications that are needed by hello marketing department.</span></span> <span data-ttu-id="8c53c-106">W ten sposób można oszczędzić czas dzięki zarządzaniu hello członkostwa hello marketingu dział w jednym miejscu.</span><span class="sxs-lookup"><span data-stu-id="8c53c-106">This way you can save time by managing hello membership of hello marketing department in one place.</span></span> <span data-ttu-id="8c53c-107">Następnie przypisywania użytkowników aplikacji toohello podczas zostaną dodane jako członkowie grupy marketing hello, i ich przypisania usunięte z aplikacji hello usunięcie z hello marketingu.</span><span class="sxs-lookup"><span data-stu-id="8c53c-107">Users then are assigned toohello application when they are added as members of hello marketing group, and have their assignments removed from hello application when they are removed from hello marketing group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8c53c-108">Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="8c53c-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 

<span data-ttu-id="8c53c-109">Ta możliwość może służyć z setkami aplikacji, które można dodać z wewnątrz hello galerii aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c53c-109">This capability can be used with hundreds of applications that you can add from within hello Azure AD Application Gallery.</span></span>

<span data-ttu-id="8c53c-110">**dostęp tooassign tooa grupy aplikacji SaaS**</span><span class="sxs-lookup"><span data-stu-id="8c53c-110">**tooassign access for a group tooa SaaS application**</span></span>

1. <span data-ttu-id="8c53c-111">W hello [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **usługi Active Directory** na pasku nawigacyjnym hello na powitania lewą stronę.</span><span class="sxs-lookup"><span data-stu-id="8c53c-111">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory** on hello navigation bar on hello left hand side.</span></span>
2. <span data-ttu-id="8c53c-112">Wybierz hello **katalogu** kartę, a następnie otwórz hello katalogu, w której ma dostęp tooassign tooa grupy aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="8c53c-112">Select hello **Directory** tab, and then open hello directory in which you want tooassign access for a group tooa SaaS application.</span></span>
3. <span data-ttu-id="8c53c-113">Wybierz hello **aplikacji** kartę. Wybierz aplikację, która dodaje z hello galerii aplikacji, a następnie kliknij przycisk hello **użytkowników i grup** kartę.</span><span class="sxs-lookup"><span data-stu-id="8c53c-113">Select hello **Applications** tab. Select an application that you added from hello Application Gallery, and then click  hello **Users and Groups** tab.</span></span>
4. <span data-ttu-id="8c53c-114">Na powitania **użytkowników i grup** na karcie hello **począwszy** wprowadź nazwę hello hello grupy toowhich ma tooassign dostępu, a następnie wybierz hello znacznik wyboru w prawym górnym rogu hello.</span><span class="sxs-lookup"><span data-stu-id="8c53c-114">On hello **Users and Groups** tab, in hello **Starting with** field, enter hello name of hello group toowhich you want tooassign access, and then select hello check mark in hello upper right.</span></span> <span data-ttu-id="8c53c-115">Wystarczy tootype hello pierwsza część nazwy grupy.</span><span class="sxs-lookup"><span data-stu-id="8c53c-115">You only need tootype hello first part of a group's name.</span></span>
5. <span data-ttu-id="8c53c-116">Wybierz grupę hello, a następnie wybierz opcję hello **przypisywanie dostępu** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8c53c-116">Select hello group, then then select hello **Assign Access** button.</span></span> <span data-ttu-id="8c53c-117">Wybierz **tak** po wyświetleniu komunikatu potwierdzenia hello.</span><span class="sxs-lookup"><span data-stu-id="8c53c-117">Select **Yes** when you see hello confirmation message.</span></span> <span data-ttu-id="8c53c-118">Członkostwo grup zagnieżdżonych nie są obsługiwane dla tooapplications przypisywania na podstawie grupy w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="8c53c-118">Nested group memberships are not supported for group-based assignment tooapplications at this time.</span></span>
6. <span data-ttu-id="8c53c-119">Można również sprawdzić, użytkowników, którzy są przypisane aplikacji toohello, bezpośrednio lub przez członkostwo w grupie.</span><span class="sxs-lookup"><span data-stu-id="8c53c-119">You can also see which users are assigned toohello application, either directly or by membership in a group.</span></span> <span data-ttu-id="8c53c-120">toodo tego hello zmiany **wyświetlenie listy rozwijanej z "Grupy"** za**"Wszyscy użytkownicy"**.</span><span class="sxs-lookup"><span data-stu-id="8c53c-120">toodo this, change hello **Show dropdown from 'Groups'** too**'All Users'**.</span></span> <span data-ttu-id="8c53c-121">Lista Hello zawiera użytkowników w katalogu hello i czy każdy użytkownik jest przypisany toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8c53c-121">hello list shows users in hello directory and whether or not each user is assigned toohello application.</span></span> <span data-ttu-id="8c53c-122">Lista Hello zawiera również hello przypisane użytkownikami przypisanymi bezpośrednio aplikacji toohello (typ przydziału wyświetlane jako "Bezpośrednio"), czy na podstawie członkostwa w grupie (typ przydziału wyświetlane jako "Dziedziczonych.")</span><span class="sxs-lookup"><span data-stu-id="8c53c-122">hello list also shows whether hello assigned users are assigned toohello application directly (assignment type shown as 'Direct'), or by virtue of group membership (assignment type shown as 'Inherited.')</span></span>

> [!NOTE]
> <span data-ttu-id="8c53c-123">Widać hello użytkownicy i grupy dopiero po włączeniu usługi Azure AD Premium lub usługi Azure AD podstawowa.</span><span class="sxs-lookup"><span data-stu-id="8c53c-123">You can see hello Users and Groups tab only after you have enabled Azure AD Premium or Azure AD Basic.</span></span>
>
>

### <a name="next-steps"></a><span data-ttu-id="8c53c-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8c53c-124">Next steps</span></span>
<span data-ttu-id="8c53c-125">Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8c53c-125">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="8c53c-126">Zarządzanie tooresources dostępu za pomocą grup usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8c53c-126">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="8c53c-127">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8c53c-127">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="8c53c-128">Polecenia cmdlet usługi Azure Active Directory służące do konfigurowania ustawień grupy</span><span class="sxs-lookup"><span data-stu-id="8c53c-128">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="8c53c-129">Co to jest usługa Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8c53c-129">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="8c53c-130">Integrowanie tożsamości lokalnych z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8c53c-130">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
