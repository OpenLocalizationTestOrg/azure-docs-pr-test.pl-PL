---
title: "Zarządzanie dostępem do aplikacji SaaS przy użyciu grupy | Dokumentacja firmy Microsoft"
description: "Jak używać grup w usłudze Azure Active Directory — wersja Premium lub Basic udzielania dostępu do aplikacji SaaS, które są zintegrowane z usługą Azure Active Directory."
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
ms.openlocfilehash: d350011ee9fc5ced9ddb16993f68d3c840a645a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="using-a-group-to-manage-access-to-saas-applications"></a><span data-ttu-id="4d2e2-103">Używanie grupy do zarządzania dostępem do aplikacji SaaS</span><span class="sxs-lookup"><span data-stu-id="4d2e2-103">Using a group to manage access to SaaS applications</span></span>
<span data-ttu-id="4d2e2-104">Za pomocą usługi Azure Active Directory (Azure AD) z licencją Azure AD Premium lub usługi Azure AD podstawowa, można użyć grupy do udzielania dostępu do aplikacji SaaS, który jest zintegrowany z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d2e2-104">Using Azure Active Directory (Azure AD) with an Azure AD Premium or Azure AD Basic license, you can use groups to assign access to a SaaS application that's integrated with Azure AD.</span></span> <span data-ttu-id="4d2e2-105">Na przykład, jeśli ma zostać przypisany dostęp dla działu marketingu do używania pięciu różnych aplikacji SaaS, można utworzyć grupę, która zawiera użytkowników w dziale marketingu i przypisz następujące pięć aplikacji SaaS, które są wymagane przez tę grupę Dział marketingu.</span><span class="sxs-lookup"><span data-stu-id="4d2e2-105">For example, if you want to assign access for the marketing department to use five different SaaS applications, you can create a group that contains the users in the marketing department, and then assign that group to these five SaaS applications that are needed by the marketing department.</span></span> <span data-ttu-id="4d2e2-106">W ten sposób można oszczędzić czas dzięki zarządzaniu członkostwa w dziale marketingu w jednym miejscu.</span><span class="sxs-lookup"><span data-stu-id="4d2e2-106">This way you can save time by managing the membership of the marketing department in one place.</span></span> <span data-ttu-id="4d2e2-107">Następnie przypisywania użytkowników do aplikacji podczas zostaną dodane jako członkowie grupy marketing, i ich przypisania usunięte z aplikacji w przypadku usunięcia ich z grupy marketing.</span><span class="sxs-lookup"><span data-stu-id="4d2e2-107">Users then are assigned to the application when they are added as members of the marketing group, and have their assignments removed from the application when they are removed from the marketing group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d2e2-108">Firma Microsoft zaleca zarządzanie usługą Azure AD przy użyciu [centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w witrynie Azure Portal zamiast korzystania z klasycznej witryny Azure Portal przywołanej w niniejszym artykule.</span><span class="sxs-lookup"><span data-stu-id="4d2e2-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 

<span data-ttu-id="4d2e2-109">Ta możliwość może służyć z setkami aplikacji, które można dodać z w galerii aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d2e2-109">This capability can be used with hundreds of applications that you can add from within the Azure AD Application Gallery.</span></span>

<span data-ttu-id="4d2e2-110">**Aby przypisać dostęp dla grupy do aplikacji SaaS**</span><span class="sxs-lookup"><span data-stu-id="4d2e2-110">**To assign access for a group to a SaaS application**</span></span>

1. <span data-ttu-id="4d2e2-111">W [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **usługi Active Directory** na pasku nawigacyjnym po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="4d2e2-111">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory** on the navigation bar on the left hand side.</span></span>
2. <span data-ttu-id="4d2e2-112">Wybierz **katalogu** karcie, a następnie otwórz katalog, w której ma zostać przypisany dostęp dla grupy do aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="4d2e2-112">Select the **Directory** tab, and then open the directory in which you want to assign access for a group to a SaaS application.</span></span>
3. <span data-ttu-id="4d2e2-113">Wybierz **aplikacji** kartę. Wybierz aplikację, który został dodany w galerii aplikacji, a następnie kliknij przycisk **użytkowników i grup** kartę.</span><span class="sxs-lookup"><span data-stu-id="4d2e2-113">Select the **Applications** tab. Select an application that you added from the Application Gallery, and then click  the **Users and Groups** tab.</span></span>
4. <span data-ttu-id="4d2e2-114">Na **użytkowników i grup** karcie **począwszy** pola, wprowadź nazwę grupy, do której ma zostać przypisany dostęp, a następnie wybierz znacznik wyboru w prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="4d2e2-114">On the **Users and Groups** tab, in the **Starting with** field, enter the name of the group to which you want to assign access, and then select the check mark in the upper right.</span></span> <span data-ttu-id="4d2e2-115">Należy wpisać pierwsza część nazwy grupy.</span><span class="sxs-lookup"><span data-stu-id="4d2e2-115">You only need to type the first part of a group's name.</span></span>
5. <span data-ttu-id="4d2e2-116">Wybierz grupę, a następnie wybierz **przypisywanie dostępu** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4d2e2-116">Select the group, then then select the **Assign Access** button.</span></span> <span data-ttu-id="4d2e2-117">Wybierz **tak** gdy zostanie wyświetlony komunikat potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="4d2e2-117">Select **Yes** when you see the confirmation message.</span></span> <span data-ttu-id="4d2e2-118">Aktualnie w ramach przypisywania do aplikacji na podstawie grup nie jest obsługiwane członkostwo w grupach zagnieżdżonych.</span><span class="sxs-lookup"><span data-stu-id="4d2e2-118">Nested group memberships are not supported for group-based assignment to applications at this time.</span></span>
6. <span data-ttu-id="4d2e2-119">Można również sprawdzić, użytkowników, którzy są przypisane do aplikacji, bezpośrednio lub przez członkostwo w grupie.</span><span class="sxs-lookup"><span data-stu-id="4d2e2-119">You can also see which users are assigned to the application, either directly or by membership in a group.</span></span> <span data-ttu-id="4d2e2-120">Aby to zrobić, należy zmienić **wyświetlenie listy rozwijanej z "Grupy"** do **"Wszyscy użytkownicy"**.</span><span class="sxs-lookup"><span data-stu-id="4d2e2-120">To do this, change the **Show dropdown from 'Groups'** to **'All Users'**.</span></span> <span data-ttu-id="4d2e2-121">Lista zawiera użytkowników w katalogu i czy każdy użytkownik jest przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4d2e2-121">The list shows users in the directory and whether or not each user is assigned to the application.</span></span> <span data-ttu-id="4d2e2-122">Lista zawiera również, czy przypisanych użytkowników przypisanych do aplikacji bezpośrednio (typ przydziału wyświetlane jako "Bezpośrednio") lub na podstawie członkostwa w grupie (typ przydziału wyświetlane jako "Dziedziczonych.")</span><span class="sxs-lookup"><span data-stu-id="4d2e2-122">The list also shows whether the assigned users are assigned to the application directly (assignment type shown as 'Direct'), or by virtue of group membership (assignment type shown as 'Inherited.')</span></span>

> [!NOTE]
> <span data-ttu-id="4d2e2-123">Na karcie użytkowników i grup jest widoczny dopiero po włączeniu usługi Azure AD Premium lub usługi Azure AD podstawowa.</span><span class="sxs-lookup"><span data-stu-id="4d2e2-123">You can see the Users and Groups tab only after you have enabled Azure AD Premium or Azure AD Basic.</span></span>
>
>

### <a name="next-steps"></a><span data-ttu-id="4d2e2-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4d2e2-124">Next steps</span></span>
<span data-ttu-id="4d2e2-125">Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4d2e2-125">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="4d2e2-126">Zarządzanie dostępem do zasobów za pomocą grup usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4d2e2-126">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="4d2e2-127">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4d2e2-127">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="4d2e2-128">Polecenia cmdlet usługi Azure Active Directory służące do konfigurowania ustawień grupy</span><span class="sxs-lookup"><span data-stu-id="4d2e2-128">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="4d2e2-129">Co to jest usługa Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4d2e2-129">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="4d2e2-130">Integrowanie tożsamości lokalnych z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4d2e2-130">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
