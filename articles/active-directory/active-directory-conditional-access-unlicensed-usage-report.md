---
title: "Raport użycia aaaUnlicensed | Dokumentacja firmy Microsoft"
description: "Witaj raportu użycia licencji, które pomaga zidentyfikować nielicencjonowani użytkownicy, którzy korzystają z płatnej funkcje usługi Azure AD."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92138f43-9528-4c8a-b834-66a47da476e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: c44d1756b4641d7ca88434017eedb6c5e2567cb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="unlicensed-usage-report"></a>Raport użycia licencji
Witaj raportu użycia licencji, które pomaga zidentyfikować nielicencjonowani użytkownicy, którzy korzystają z płatnej funkcje usługi Azure AD. Dzięki temu można lepiej wykorzystać toomake licencji, które zostały zakupione i tooidentify wiedzieć, kiedy użytkownik może być konieczne dodatkowe licencje. 

przedstawia Hello active użycie hello płatnej funkcje w hello w ciągu ostatnich 30 dni. 

## <a name="report-structure"></a>Struktura raportu
| Nazwa kolumny | Opis |
|:--- |:--- |
| Bez licencji użytkownika |Nazwa użytkownika, powitalne |
| Funkcja |Nazwa funkcji Hello. Na przykład: dostępu warunkowego |
| Dostęp do aplikacji |Nazwa Hello aplikacji hello, która jest uzyskiwany za pomocą funkcji hello. Na przykład: usługi Office 365 SharePoint Online |

> [!NOTE]
> Jeśli konto użytkownika zostało usunięte Witaj "Bez licencji użytkownika" zostaną wypełnione kolumny o identyfikatorze, takich jak 1003000090D8B285
> 
> 

## <a name="conditional-access-feature"></a>Funkcja dostępu warunkowego
Nielicencjonowani użytkownicy zostaną oflagowane przy uzyskiwaniu dostępu do usługi, która ma zasady dostępu warunkowego zastosowane, jeśli nie mają licencji usługi Azure AD Premium. 

Dotyczy to tooMFA / zasady lokalizacji, a także urządzenia zasady, które przy użyciu usługi Intune.

## <a name="see-also"></a>Zobacz też
* [Za pomocą dostępu warunkowego z usługą Office 365 i inne usługi Azure Active Directory podłączonego aplikacji](active-directory-conditional-access.md)
* [Wprowadzenie do korzystania z dostępu warunkowego tooAzure AD](active-directory-conditional-access-azuread-connected-apps.md) 

