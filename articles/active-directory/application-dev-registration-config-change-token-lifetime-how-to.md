---
title: "Domyślnie okres istnienia tokenu hello toochange aaaHow dla aplikacji utworzonych niestandardowych | Dokumentacja firmy Microsoft"
description: "Jak tooupdate okres istnienia tokenu zasad aplikacji, które tworzysz usługi Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 6e1aa1f2a7c33c1f55c5fb619c618ad43cd96273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochange-hello-token-lifetime-defaults-for-a-custom-developed-application"></a><span data-ttu-id="c8582-103">Jak okres istnienia tokenu hello toochange ustawienia domyślne dla aplikacji utworzonych niestandardowych</span><span class="sxs-lookup"><span data-stu-id="c8582-103">How toochange hello token lifetime defaults for a custom-developed application</span></span>

<span data-ttu-id="c8582-104">Azure AD Premium umożliwia deweloperom aplikacji i dzierżawca Administratorzy tooconfigure hello okres istnienia tokenów wystawionych dla klientów z systemem innym niż poufne.</span><span class="sxs-lookup"><span data-stu-id="c8582-104">Azure AD Premium allows app developers and tenant admins tooconfigure hello lifetime of tokens issued for non-confidential clients.</span></span> <span data-ttu-id="c8582-105">Okres istnienia tokenu zasady są skonfigurowane na poziomie dzierżawy lub hello zasobów, do której uzyskuje dostęp.</span><span class="sxs-lookup"><span data-stu-id="c8582-105">Token lifetime policies are set on a tenant-wide basis or hello resources being accessed.</span></span>

 * <span data-ttu-id="c8582-106">tooset zasad okres istnienia tokenu należy toodownload hello [modułu Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureADPreview).</span><span class="sxs-lookup"><span data-stu-id="c8582-106">tooset a token lifetime policy, you need toodownload hello [Azure AD PowerShell Module](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>

 * <span data-ttu-id="c8582-107">Uruchom hello **Connect AzureAD-Potwierdź** polecenia.</span><span class="sxs-lookup"><span data-stu-id="c8582-107">Run hello **Connect-AzureAD -Confirm** command.</span></span>

 * <span data-ttu-id="c8582-108">Oto przykład zasad, która ustawia token odświeżania pojedynczy czynnik maksymalny wiek hello.</span><span class="sxs-lookup"><span data-stu-id="c8582-108">Here’s an example policy that sets hello max age single factor refresh token.</span></span> <span data-ttu-id="c8582-109">Utwórz zasadę hello:```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span><span class="sxs-lookup"><span data-stu-id="c8582-109">Create hello policy: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span></span>

 * <span data-ttu-id="c8582-110">Wyewidencjonowanie hello [okres istnienia tokenu Konfigurowanie](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes) jak dokument toolearn toocreate inne niestandardowe.</span><span class="sxs-lookup"><span data-stu-id="c8582-110">Checkout hello [Configuring token lifetime](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)   document toolearn how toocreate other custom.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8582-111">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c8582-111">Next steps</span></span>
[<span data-ttu-id="c8582-112">Konfigurowanie okres istnienia tokenu</span><span class="sxs-lookup"><span data-stu-id="c8582-112">Configuring Token Lifetime</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[<span data-ttu-id="c8582-113">Odwołanie do tokenu usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8582-113">Azure AD Token Reference</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

