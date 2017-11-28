---
title: "Jak zmienić okres istnienia tokenu domyślnie rozwinięte niestandardowych aplikacji | Dokumentacja firmy Microsoft"
description: "Jak aktualizować zasady okres istnienia tokenu aplikacji, które tworzysz usługi Azure AD"
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
ms.openlocfilehash: a28eacd820ed28a6470992ce86b060e886c00bcb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-change-the-token-lifetime-defaults-for-a-custom-developed-application"></a><span data-ttu-id="0b03f-103">Jak zmienić domyślne okres istnienia tokenu dla aplikacji utworzonych niestandardowych</span><span class="sxs-lookup"><span data-stu-id="0b03f-103">How to change the token lifetime defaults for a custom-developed application</span></span>

<span data-ttu-id="0b03f-104">Azure AD Premium umożliwia deweloperom aplikacji i administratorów dzierżawy, aby skonfigurować okres istnienia tokenów wystawionych dla klientów z systemem innym niż poufne.</span><span class="sxs-lookup"><span data-stu-id="0b03f-104">Azure AD Premium allows app developers and tenant admins to configure the lifetime of tokens issued for non-confidential clients.</span></span> <span data-ttu-id="0b03f-105">Okres istnienia tokenu zasady są skonfigurowane na poziomie dzierżawy lub zasobów, do której uzyskuje dostęp.</span><span class="sxs-lookup"><span data-stu-id="0b03f-105">Token lifetime policies are set on a tenant-wide basis or the resources being accessed.</span></span>

 * <span data-ttu-id="0b03f-106">Aby skonfigurować zasady okres istnienia tokenu, należy pobrać [modułu Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureADPreview).</span><span class="sxs-lookup"><span data-stu-id="0b03f-106">To set a token lifetime policy, you need to download the [Azure AD PowerShell Module](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>

 * <span data-ttu-id="0b03f-107">Uruchom **Connect AzureAD-Potwierdź** polecenia.</span><span class="sxs-lookup"><span data-stu-id="0b03f-107">Run the **Connect-AzureAD -Confirm** command.</span></span>

 * <span data-ttu-id="0b03f-108">Oto przykład zasad, która ustawia token odświeżania pojedynczy czynnik maksymalny wiek.</span><span class="sxs-lookup"><span data-stu-id="0b03f-108">Here’s an example policy that sets the max age single factor refresh token.</span></span> <span data-ttu-id="0b03f-109">Tworzenie zasad:```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span><span class="sxs-lookup"><span data-stu-id="0b03f-109">Create the policy: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span></span>

 * <span data-ttu-id="0b03f-110">Wyewidencjonowanie [okres istnienia tokenu Konfigurowanie](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes) dokumentu, aby dowiedzieć się, jak utworzyć inne niestandardowe.</span><span class="sxs-lookup"><span data-stu-id="0b03f-110">Checkout the [Configuring token lifetime](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)   document to learn how to create other custom.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b03f-111">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0b03f-111">Next steps</span></span>
[<span data-ttu-id="0b03f-112">Konfigurowanie okres istnienia tokenu</span><span class="sxs-lookup"><span data-stu-id="0b03f-112">Configuring Token Lifetime</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[<span data-ttu-id="0b03f-113">Odwołanie do tokenu usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b03f-113">Azure AD Token Reference</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

