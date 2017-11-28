---
title: "aaaNext kroków dla zarządzania dostępem przy użyciu grup | Dokumentacja firmy Microsoft"
description: "Jak zaawansowane — do obiektu dla Zarządzanie grupami zabezpieczeń i w jaki sposób toouse tych grup toomanage dostępu tooa zasobów."
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
ms.openlocfilehash: 4fd55f893290fac3551a130f29bd12709cf551e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-owners-for-a-group"></a><span data-ttu-id="dc044-103">Zarządzanie właścicielami grupy</span><span class="sxs-lookup"><span data-stu-id="dc044-103">Managing owners for a group</span></span>
<span data-ttu-id="dc044-104">Gdy właściciel zasobu przypisana grupy tooan zasobów dostępu tooa w usłudze Azure AD, hello członkostwo grupy hello jest zarządzana przez właściciela grupy hello.</span><span class="sxs-lookup"><span data-stu-id="dc044-104">Once a resource owner has assigned access tooa resource tooan Azure AD group, hello membership of hello group is managed by hello group owner.</span></span> <span data-ttu-id="dc044-105">Witaj właściciel zasobu przekazuje skutecznie hello uprawnienia tooassign użytkowników toohello toohello właściciel zasobu hello grupy.</span><span class="sxs-lookup"><span data-stu-id="dc044-105">hello resource owner effectively delegates hello permission tooassign users toohello resource toohello owner of hello group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dc044-106">Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="dc044-106">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 

## <a name="assigning-group-ownership"></a><span data-ttu-id="dc044-107">Przypisywanie własności grup</span><span class="sxs-lookup"><span data-stu-id="dc044-107">Assigning group ownership</span></span>
<span data-ttu-id="dc044-108">**tooadd tooa grupy**</span><span class="sxs-lookup"><span data-stu-id="dc044-108">**tooadd an owner tooa group**</span></span>

1. <span data-ttu-id="dc044-109">W hello [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **usługi Active Directory**, a następnie otwórz katalogu organizacji.</span><span class="sxs-lookup"><span data-stu-id="dc044-109">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="dc044-110">Wybierz hello **grup** kartę i hello następnie otwórz grupę, tooadd właścicieli.</span><span class="sxs-lookup"><span data-stu-id="dc044-110">Select hello **Groups** tab, and then open hello group that you want tooadd owners to.</span></span>
3. <span data-ttu-id="dc044-111">Wybierz **Dodaj właścicieli**.</span><span class="sxs-lookup"><span data-stu-id="dc044-111">Select **Add Owners**.</span></span>
4. <span data-ttu-id="dc044-112">Na powitania **Dodaj właścicieli** strona, wybierz hello użytkownika mają tooadd jako właściciela hello tej grupy i upewnij się, że ta nazwa jest dodawany toohello **wybrane** okienka.</span><span class="sxs-lookup"><span data-stu-id="dc044-112">On hello **Add owners** page, select hello user that you want tooadd as hello owner of this group, and make sure this name is added toohello **Selected** pane.</span></span>

<span data-ttu-id="dc044-113">**tooremove właściciela z grupy**</span><span class="sxs-lookup"><span data-stu-id="dc044-113">**tooremove an owner from a group**</span></span>

1. <span data-ttu-id="dc044-114">W hello [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **usługi Active Directory**, a następnie otwórz katalogu organizacji.</span><span class="sxs-lookup"><span data-stu-id="dc044-114">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="dc044-115">Wybierz hello **grup** kartę, a następnie otwórz hello grupę, która ma tooremove właściciela.</span><span class="sxs-lookup"><span data-stu-id="dc044-115">Select hello **Groups** tab, and then open hello group that you want tooremove an owner from.</span></span>
3. <span data-ttu-id="dc044-116">Wybierz hello **właścicieli** kartę.</span><span class="sxs-lookup"><span data-stu-id="dc044-116">Select hello **Owners** tab.</span></span>
4. <span data-ttu-id="dc044-117">Wybierz hello właściciela mają tooremove z tej grupy, a następnie wybierz **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="dc044-117">Select hello owner that you want tooremove from this group, and then select **Remove**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="dc044-118">Dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="dc044-118">Additional information</span></span>
<span data-ttu-id="dc044-119">Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dc044-119">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="dc044-120">Zarządzanie tooresources dostępu za pomocą grup usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc044-120">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="dc044-121">Polecenia cmdlet usługi Azure Active Directory służące do konfigurowania ustawień grupy</span><span class="sxs-lookup"><span data-stu-id="dc044-121">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="dc044-122">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc044-122">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="dc044-123">Co to jest usługa Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dc044-123">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="dc044-124">Integrowanie tożsamości lokalnych z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc044-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
