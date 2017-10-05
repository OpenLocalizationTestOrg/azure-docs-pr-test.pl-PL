---
title: "Następne kroki dla zarządzania dostępem przy użyciu grup | Dokumentacja firmy Microsoft"
description: "Jak zaawansowane — do obiektu dla Zarządzanie grupami zabezpieczeń i zarządzanie dostępem do zasobów przy użyciu tych grup."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 44350a3c-8ea1-4da1-aaac-7fc53933dd21
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 82fbeb379e90add09f7c569111053f6e9b1bc9c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="managing-owners-for-a-group"></a><span data-ttu-id="d55e8-103">Zarządzanie właścicielami grupy</span><span class="sxs-lookup"><span data-stu-id="d55e8-103">Managing owners for a group</span></span>
<span data-ttu-id="d55e8-104">Gdy właściciel zasobu ma przypisany dostęp do tego zasobu do grupy usługi Azure AD, członkostwo w grupie jest zarządzana przez właściciela grupy.</span><span class="sxs-lookup"><span data-stu-id="d55e8-104">Once a resource owner has assigned access to a resource to an Azure AD group, the membership of the group is managed by the group owner.</span></span> <span data-ttu-id="d55e8-105">Właściciel zasobu przekazuje skutecznie uprawnienie do przypisywania użytkowników do zasobów do właściciela grupy.</span><span class="sxs-lookup"><span data-stu-id="d55e8-105">The resource owner effectively delegates the permission to assign users to the resource to the owner of the group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d55e8-106">Firma Microsoft zaleca zarządzanie usługą Azure AD przy użyciu [centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w witrynie Azure Portal zamiast korzystania z klasycznej witryny Azure Portal przywołanej w niniejszym artykule.</span><span class="sxs-lookup"><span data-stu-id="d55e8-106">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 

## <a name="assigning-group-ownership"></a><span data-ttu-id="d55e8-107">Przypisywanie własności grup</span><span class="sxs-lookup"><span data-stu-id="d55e8-107">Assigning group ownership</span></span>
<span data-ttu-id="d55e8-108">**Aby dodać właściciela grupy**</span><span class="sxs-lookup"><span data-stu-id="d55e8-108">**To add an owner to a group**</span></span>

1. <span data-ttu-id="d55e8-109">W [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **usługi Active Directory**, a następnie otwórz katalogu organizacji.</span><span class="sxs-lookup"><span data-stu-id="d55e8-109">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="d55e8-110">Wybierz **grup** karcie, a następnie otwórz grupę, którą chcesz dodać właścicieli.</span><span class="sxs-lookup"><span data-stu-id="d55e8-110">Select the **Groups** tab, and then open the group that you want to add owners to.</span></span>
3. <span data-ttu-id="d55e8-111">Wybierz **Dodaj właścicieli**.</span><span class="sxs-lookup"><span data-stu-id="d55e8-111">Select **Add Owners**.</span></span>
4. <span data-ttu-id="d55e8-112">Na **Dodaj właścicieli** wybierz użytkownika, który chcesz dodać jako właściciela tej grupy i upewnij się, że ta nazwa jest dodawana do **wybrane** okienka.</span><span class="sxs-lookup"><span data-stu-id="d55e8-112">On the **Add owners** page, select the user that you want to add as the owner of this group, and make sure this name is added to the **Selected** pane.</span></span>

<span data-ttu-id="d55e8-113">**Aby usunąć właściciela grupy**</span><span class="sxs-lookup"><span data-stu-id="d55e8-113">**To remove an owner from a group**</span></span>

1. <span data-ttu-id="d55e8-114">W [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **usługi Active Directory**, a następnie otwórz katalogu organizacji.</span><span class="sxs-lookup"><span data-stu-id="d55e8-114">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="d55e8-115">Wybierz **grup** karcie, a następnie otwórz grupę, którą chcesz usunąć właściciela.</span><span class="sxs-lookup"><span data-stu-id="d55e8-115">Select the **Groups** tab, and then open the group that you want to remove an owner from.</span></span>
3. <span data-ttu-id="d55e8-116">Wybierz **właścicieli** kartę.</span><span class="sxs-lookup"><span data-stu-id="d55e8-116">Select the **Owners** tab.</span></span>
4. <span data-ttu-id="d55e8-117">Wybierz właściciela, który chcesz usunąć z tej grupy, a następnie wybierz **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="d55e8-117">Select the owner that you want to remove from this group, and then select **Remove**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="d55e8-118">Dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="d55e8-118">Additional information</span></span>
<span data-ttu-id="d55e8-119">Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d55e8-119">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="d55e8-120">Zarządzanie dostępem do zasobów za pomocą grup usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d55e8-120">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="d55e8-121">Polecenia cmdlet usługi Azure Active Directory służące do konfigurowania ustawień grupy</span><span class="sxs-lookup"><span data-stu-id="d55e8-121">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="d55e8-122">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d55e8-122">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="d55e8-123">Co to jest usługa Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d55e8-123">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="d55e8-124">Integrowanie tożsamości lokalnych z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d55e8-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
