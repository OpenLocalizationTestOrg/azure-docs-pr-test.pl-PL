---
title: "Usługa Azure Active Directory raportowania opóźnienia | Dokumentacja firmy Microsoft"
description: "Ilość czasu, jaki zajmuje zdarzenia do raportowania w usłudze Azure Active Directory"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 346b14f8-d16d-4b07-8211-e6c5eec07062
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 9443a00232420d58dea52ed01f31a4ef964a1620
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-report-latencies"></a>Opóźnienia raportów usługi Azure Active Directory
*Ta dokumentacja jest częścią [Przewodnika po raportach usługi Azure Active Directory](active-directory-reporting-guide.md).*

| Raport | Minimalne | Średnia | Maksymalna |
| --- | --- | --- | --- |
| **Raporty dotyczące zabezpieczeń** | | | |
| Nieregularne działania związane z logowaniem |2 godziny |4 godziny |8 godzin |
| Logowania z nieznanych źródeł |2 godziny |4 godziny |8 godzin |
| Logowania po wielokrotnych niepowodzeniach |2 godziny |4 godziny |8 godzin |
| Logowania z wielu lokalizacji geograficznych |2 godziny |4 godziny |8 godzin |
| Logowania z adresów IP związanych z podejrzanymi działaniami |2 godziny |4 godziny |8 godzin |
| Logowania z urządzeń, które mogą być zainfekowane |2 godziny |4 godziny |8 godzin |
| Nietypowe działania użytkowników związane z logowaniem |2 godziny |4 godziny |8 godzin |
| Użytkownicy z ujawnionymi poświadczeniami |2 godziny |4 godziny |8 godzin |
| Wszystkich działań logowania użytkownika |2 godziny |4 godziny |8 godzin |
| **Raporty aplikacji** | | | |
| Działanie aprowizacji kont |2 godziny |4 godziny |8 godzin |
| Błędy aprowizacji kont |2 godziny |4 godziny |8 godzin |
| Użycie aplikacji |2 godziny |4 godziny |8 godzin |
| Stan przerzucania hasła |2 godziny |4 godziny |8 godzin |
| **Inspekcja i raporty dotyczące działań** | | | |
| Raport dotyczący inspekcji |1 minuta |15 minut |30 minut |
| (Azure AD) aktywność resetowania haseł |2 godziny |4 godziny |8 godzin |
| (Identity Manager) aktywność resetowania haseł |2 godziny |4 godziny |8 godzin |
| Działanie rejestracji (Azure AD) resetowania hasła |2 godziny |4 godziny |8 godzin |
| Działanie rejestracji (Identity Manager) resetowania hasła |2 godziny |4 godziny |8 godzin |
| Samoobsługowego raport aktywności grup (Azure AD) |2 godziny |4 godziny |8 godzin |
| Samoobsługowego raport aktywności grup (Identity Manager) |2 godziny |4 godziny |8 godzin |
| **Raporty usługi RMS** | | | |
| Najbardziej aktywni użytkownicy usługi RMS |2 godziny |4 godziny |8 godzin |
| Użycie usługi RMS |2 godziny |4 godziny |8 godzin |
| Użycie urządzeń usługi RMS |2 godziny |4 godziny |8 godzin |
| Użycie aplikacji z obsługą usług RMS |2 godziny |4 godziny |8 godzin |

