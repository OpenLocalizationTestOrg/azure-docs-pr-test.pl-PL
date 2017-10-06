---
title: "Azure AD Connect: Wystąpienie usługi synchronizacji | Dokumentacja firmy Microsoft"
description: "Ta strona dokumentów uwagi dotyczące wystąpienia usługi Azure AD."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2a0d8a599cf84cd6530bdbb24951156510d2cf3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a>Azure AD Connect: Uwagi dotyczące wystąpienia
Azure AD Connect jest najczęściej używana z Witaj świecie wystąpienia usługi Azure AD i Office 365. Istnieją także inne wystąpienia, ale te mają różne wymagania dotyczące adresów URL i inne uwagi.

## <a name="microsoft-cloud-germany"></a>Microsoft Cloud (Niemcy)
Witaj [Niemcy Microsoft Cloud](http://www.microsoft.de/cloud-deutschland) to chmura suwerennych przez osobę zaufaną niemieckim danych.

| Adresy URL tooopen w serwera proxy |
| --- |
| \*. microsoftonline.de |
| \*.windows.net |
| + Listy odwołania certyfikatów |

Po zarejestrowaniu tooyour dzierżawy usługi Azure AD, należy użyć konta w domenie onmicrosoft.de hello.

Aktualnie nie znajduje się w Niemczech Microsoft Cloud hello funkcje:

* **Azure AD Connect Health** nie jest dostępna.
* **Aktualizacje automatyczne** nie jest dostępna.
* **Zapisywanie zwrotne haseł** jest dostępna w wersji zapoznawczej wersji Azure AD Connect 1.1.570.0 i po.
* Inne usługi Azure AD Premium nie są dostępne.

## <a name="microsoft-azure-government-cloud"></a>Chmury Microsoft Azure dla instytucji rządowych
Witaj [chmury Microsoft Azure dla instytucji rządowych](https://azure.microsoft.com/features/gov/) to chmura dla instytucji rządowych Stanów Zjednoczonych.

Ta chmura obsługiwanego przez wcześniejszych wersjach narzędzia DirSync. Z 1.1.180 kompilacji programu Azure AD Connect hello generacji chmury hello jest obsługiwana. Tej generacji używa USA — tylko do oparte na punktach końcowych i mieć osobne listy adresów URL tooopen w serwera proxy.

| Adresy URL tooopen w serwera proxy |
| --- |
| \*.microsoftonline.com |
| \*. microsoftonline.us |
| \*. gov.us.microsoftonline.com |
| + Listy odwołania certyfikatów |

Azure AD Connect nie jest w stanie tooautomatically wykrywa, że dzierżawy usługi Azure AD znajduje się w chmurze dla instytucji rządowych hello. Zamiast tego należy hello tootake następujące akcje po zainstalowaniu usługi Azure AD Connect.

1. Uruchom hello Azure AD Connect instalacji.
2. Gdy zostanie wyświetlona strona pierwszy hello, gdzie są powinien hello tooaccept umowy licencyjnej, nie należy kontynuować, ale pozostawić Uruchamianie Kreatora instalacji hello.
3. Uruchom regedit i zmienić wartość klucza rejestru hello `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello wartość `2`.
4. Wrócić do poprzedniej strony Kreatora instalacji toohello usługi Azure AD Connect, zaakceptuj umowę licencyjną hello i kontynuować. Podczas instalacji, upewnij się, że hello toouse **konfiguracji niestandardowej** ścieżki instalacji (i nie Instalacja ekspresowa). Następnie kontynuuj instalację hello w zwykły sposób.

Aktualnie nie znajduje się w chmurze Microsoft Azure dla instytucji rządowych hello funkcje:

* **Azure AD Connect Health** nie jest dostępna.
* **Aktualizacje automatyczne** nie jest dostępna.
* **Zapisywanie zwrotne haseł** jest dostępna w wersji zapoznawczej wersji Azure AD Connect 1.1.570.0 i po.
* Inne usługi Azure AD Premium nie są dostępne.

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
