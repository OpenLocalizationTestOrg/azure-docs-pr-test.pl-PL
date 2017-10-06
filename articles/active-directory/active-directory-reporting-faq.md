---
title: "aaaAzure Active Directory raportowania — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Raportowanie często zadawane pytania dotyczące usługi Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 534da0b1-7858-4167-9986-7a62fbd10439
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: be65a05574ea3b5b190cd02a96b211c571ba70bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-faq"></a>Usługa Azure Active Directory raportowania — często zadawane pytania

Ten artykuł zawiera odpowiedzi toofrequently zadawane pytania (FAQ) dotyczące raportowania usługi Azure Active Directory.  
Aby uzyskać więcej informacji, zobacz [raportowania usługi Azure Active Directory](active-directory-reporting-azure-portal.md). 

**Pytanie: co to jest hello przechowywanie danych o Dzienniki aktywności (inspekcji i logowania) w portalu Azure hello?** 

**Odpowiedź:** 7 dni danych udostępniamy klientom wolnego i przełączając tooan Azure AD Premium 1 lub Premium 2 licencji, użytkownik może uzyskać dostępu do danych zapasowej too30 dni. Aby uzyskać więcej szczegółów na przechowywania, zobacz [zasady przechowywania raportów usługi Azure Active Directory](active-directory-reporting-retention.md)

--- 

**Pytanie: jak długo trwa do momentu wyświetlane dane o aktywności powitania po zakończeniu I Moje zadania?**

**Odpowiedź:** dzienników inspekcji działania mają opóźnienia, począwszy od godziny tooan w ciągu 15 minut. Dzienniki aktywności logowania ma opóźnienia — od 15 minut większość rekordów oraz too2 godzin do kilku rekordów.

---

**Pytanie: należy toobe działania administratora globalnego toosee hello dzienników hello portalu Azure lub tooget dane za pośrednictwem hello interfejsu API?**

**Odpowiedź:** Nie. Może to być **czytnika zabezpieczeń**, **administratora zabezpieczeń** lub **administratora globalnego** toosee dane w portalu Azure lub dostępu do niego za pośrednictwem hello interfejsu API raportowania.

---

**Pytanie: czy można uzyskać informacji dziennika aktywności usługi Office 365 za pomocą portalu Azure hello?**

**Odpowiedź:** mimo że działania usługi Office 365 i Azure AD działania dzienniki udziału dużej ilości zasobów katalogu hello, jeśli chcesz pełnego widoku hello Dzienniki aktywności usługi Office 365, należy przejść informacje dziennika toohello Centrum administracyjne usługi Office 365 tooget Office 365 działania.

---


**Pytanie: co zrobić interfejsów API używać tooget informacji o dziennikach Office 365 działania?**

**A:** Użyj hello interfejsów API usługi Office 365 Management tooaccess hello [Office 365 działanie logowania za pośrednictwem interfejsu API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).

---

**Pytanie: jak wiele rekordów I można pobrać z portalu Azure?**

**Odpowiedź:** można pobrać too120K rekordów z hello portalu Azure. rekordy Hello są sortowane według *najnowszych* i domyślnie uzyskać rekordów hello najnowszych K 120. 

---

**Pytanie: jak wiele rekordów można zbadać za pomocą działania hello interfejsu API?**

**Odpowiedź:** można zbadać too1 miliony rekordów (Jeśli nie jest używany operator top hello, sortującej rekordu hello przez większość ostatnie). Użyj operatora "top" hello, mogą wysyłać zapytania too500K rekordów. Przykładowe zapytania w sposób toouse hello interfejsu API w tym miejscu można znaleźć [tutaj](active-directory-reporting-api-getting-started.md).

---

**Pytanie: jak uzyskać licencję premium?**

**A:** zobacz [wprowadzenie do korzystania z usługi Azure Active Directory Premium](active-directory-get-started-premium.md) dla toothis odpowiedzi na pytanie.

---

**Pytanie: jak najszybciej Zobacz dane działań po otrzymaniu licencji premium?**

**Odpowiedź:** Jeśli masz już dane działań jako wolne licencji, a następnie widać hello tych samych danych. Jeśli nie masz żadnych danych, ich może zająć jeden lub dwa dni.

---

**Pytanie: wyświetlane dane z ostatniego miesiąca po otrzymaniu licencji usługi Azure AD premium?**

**Odpowiedź:** ostatnio przełączane tooa wersji Premium (w tym wersja próbna) można początkowo Zobacz więcej dni too7 danych. Gdy dane zebrane, zobaczysz too30 dni.

---

**Pytanie: Brak zdarzeń ryzyko w ochronę tożsamości, ale nie widzę odpowiedniego logowania w hello wszystkie sesje logowania. Jest to oczekiwane?**

**Odpowiedź:** tak, Identity Protection ocenia ryzyko dla wszystkich przepływów uwierzytelniania czy jeśli interakcyjnego lub nieinterakcyjnym. Jednak wszystkie sesje logowania tylko przedstawia tylko hello logowania interakcyjnego.

---

**Pytanie: jak można pobrać raportu "Użytkownicy oflagowani ryzyka" hello, w portalu Azure**

**A:** hello opcja toodownload *użytkownicy oflagowani ryzyka* raportu zostanie dodany wkrótce.

---

**Pytanie: jak dowiedzieć, dlaczego logowania lub użytkownikiem zostało oznaczone ryzykowne w hello portalu Azure**

**Odpowiedź:** klienci wersji Premium można dowiedzieć się więcej o hello podstawowy zdarzenia o podwyższonym ryzyku, klikając użytkownika hello w "Użytkownicy oflagowani ryzyka" lub klikając na powitania "Ryzykowne sesje logowania". Klienci bezpłatne i podstawowych wydanie uzyskać toosee hello zagrożonych użytkowników i logowania bez hello podstawowych informacji o zdarzeniu ryzyka.

---

**Pytanie: jak adresy IP są obliczane w hello logowania i logowania ryzykowne raport?**

**Odpowiedź:** adresy IP są przydzielane w taki sposób, że brak ostatecznego połączenia między adresu IP i gdzie fizycznie znajduje się komputer hello przy użyciu tego adresu. Skomplikowany czynników, takich jak przenośnych dostawców i sieci VPN często bardzo wydawania adresów IP z puli centralnej daleko od gdzie powitania klienta urządzenia są rzeczywiście używane. Podana hello powyżej, konwertowanie fizycznej lokalizacji tooa adres IP jest starań, na podstawie danych śledzenia, dane rejestru, odwrotnej wyszukiwań i inne informacje. 

---
