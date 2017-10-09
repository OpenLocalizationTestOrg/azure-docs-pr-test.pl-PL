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
# <a name="how-toochange-hello-token-lifetime-defaults-for-a-custom-developed-application"></a>Jak okres istnienia tokenu hello toochange ustawienia domyślne dla aplikacji utworzonych niestandardowych

Azure AD Premium umożliwia deweloperom aplikacji i dzierżawca Administratorzy tooconfigure hello okres istnienia tokenów wystawionych dla klientów z systemem innym niż poufne. Okres istnienia tokenu zasady są skonfigurowane na poziomie dzierżawy lub hello zasobów, do której uzyskuje dostęp.

 * tooset zasad okres istnienia tokenu należy toodownload hello [modułu Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureADPreview).

 * Uruchom hello **Connect AzureAD-Potwierdź** polecenia.

 * Oto przykład zasad, która ustawia token odświeżania pojedynczy czynnik maksymalny wiek hello. Utwórz zasadę hello:```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```

 * Wyewidencjonowanie hello [okres istnienia tokenu Konfigurowanie](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes) jak dokument toolearn toocreate inne niestandardowe.

## <a name="next-steps"></a>Następne kroki
[Konfigurowanie okres istnienia tokenu](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[Odwołanie do tokenu usługi Azure AD](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

