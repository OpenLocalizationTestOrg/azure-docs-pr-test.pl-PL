---
title: "Usługa Azure Active Directory B2C: Rozwiązywanie problemów z dzierżawcom tworzenie | Dokumentacja firmy Microsoft"
description: "Problemy i rozwiązania do tworzenia dzierżawy usługi Azure Active Directory lub Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 7ba4c6b2-161b-45b5-b3bd-ccb662f5d7a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 81af4536fc223319369aff262d42149cfbf1a1e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-an-azure-active-directory-or-azure-active-directory-b2c-tenant"></a><span data-ttu-id="44725-103">Rozwiązywanie problemów z tworzenie dzierżawy usługi Azure Active Directory lub Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="44725-103">Troubleshoot creating an Azure Active Directory or Azure Active Directory B2C tenant</span></span> 

## <a name="create-an-azure-ad-tenant"></a><span data-ttu-id="44725-104">Tworzenie dzierżawy usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="44725-104">Create an Azure AD tenant</span></span>
<span data-ttu-id="44725-105">Jeśli dzierżawa usługi Azure Active Directory (Azure AD) nie można utworzyć przy pierwszej próbie, spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="44725-105">If you can't create an Azure Active Directory (Azure AD) tenant on the first attempt, try again.</span></span> <span data-ttu-id="44725-106">Jeśli problem będzie się powtarzać, skontaktuj się z pomocą techniczną platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="44725-106">If the problem persists, contact Azure Support.</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="44725-107">Tworzenie dzierżawy usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="44725-107">Create an Azure AD B2C tenant</span></span>
<span data-ttu-id="44725-108">Jeśli wystąpią problemy podczas możesz [Tworzenie usługi Azure Active Directory B2C dzierżawy (Azure AD B2C)](active-directory-b2c-get-started.md), spróbuj następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="44725-108">If you encounter issues when you [create an Azure Active Directory B2C (Azure AD B2C) tenant](active-directory-b2c-get-started.md), try the following options:</span></span>

* <span data-ttu-id="44725-109">Jeśli dzierżawy usługi Azure AD B2C nie widać na liście dzierżawcy, spróbuj ponownie utworzyć dzierżawcę.</span><span class="sxs-lookup"><span data-stu-id="44725-109">If the Azure AD B2C tenant doesn't show up in your list of tenants, try again to create the tenant.</span></span>
* <span data-ttu-id="44725-110">Jeśli zostanie wyświetlony następujący komunikat o błędzie dzierżawy usługi Azure AD B2C jest wyświetlany na liście dzierżawcy, Usuń dzierżawcy i utwórz go ponownie:</span><span class="sxs-lookup"><span data-stu-id="44725-110">If the Azure AD B2C tenant does show up in your list of tenants and you see the following  error message, delete the tenant and create it again:</span></span>

    <span data-ttu-id="44725-111">"Nie można ukończyć tworzenia dzierżawy B2C"contosob2c".</span><span class="sxs-lookup"><span data-stu-id="44725-111">"Could not complete the creation of the B2C tenant 'contosob2c'.</span></span> <span data-ttu-id="44725-112">Odwiedź stronę to [łącze](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) Aby uzyskać więcej pomocy. "</span><span class="sxs-lookup"><span data-stu-id="44725-112">Please visit this [link](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) for more guidance."</span></span>
* <span data-ttu-id="44725-113">Istnieją znane problemy podczas usuwania istniejącej dzierżawy usługi Azure AD B2C i utwórz go ponownie przy użyciu tej samej nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="44725-113">There are known issues when you delete an existing Azure AD B2C tenant and re-create it by using the same domain name.</span></span> <span data-ttu-id="44725-114">Podczas tworzenia nowej dzierżawy usługi Azure AD B2C, należy użyć nazwy innej domeny.</span><span class="sxs-lookup"><span data-stu-id="44725-114">When you create a new Azure AD B2C tenant, you must use a different domain name.</span></span>
* <span data-ttu-id="44725-115">Jeśli te rozwiązania nie pomoże, skontaktuj się z pomocą techniczną platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="44725-115">If these resolutions don't work, contact Azure Support.</span></span> <span data-ttu-id="44725-116">Aby uzyskać więcej informacji, zobacz [pliku żądania pomocy technicznej usługi Azure AD B2C](active-directory-b2c-support.md).</span><span class="sxs-lookup"><span data-stu-id="44725-116">For more information, see [File support requests for Azure AD B2C](active-directory-b2c-support.md).</span></span>

