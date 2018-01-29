---
title: "Usługa Azure Active Directory raportowania — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Raportowanie często zadawane pytania dotyczące usługi Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: mtillman
ms.assetid: 534da0b1-7858-4167-9986-7a62fbd10439
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/05/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: a39183e65306ddc7cb81825b7abf27677339a3ba
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="azure-active-directory-reporting-faq"></a>Usługa Azure Active Directory raportowania — często zadawane pytania

Ten artykuł zawiera odpowiedzi na często zadawane pytania dotyczące usługi Azure Active Directory (Azure AD) i raportowania. Aby uzyskać więcej informacji, zobacz [Raporty w usłudze Azure Active Directory](active-directory-reporting-azure-portal.md). 

**Pytanie: używam https://graph.windows.net/&lt;nazwa dzierżawcy&gt;punktu końcowego /reports/ raporty do naszej raportowania systemów programowo interfejsy API w celu ściągania usługi Azure AD inspekcji i użycie zintegrowanej aplikacji. Co należy przełączyć?**

**A:** odszukać naszych [dokumentacji interfejsu API](https://developer.microsoft.com/graph/) aby zobaczyć, jak można użyć nowych interfejsów API dostępu do [raporty aktywności](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started-azure-portal). Ten punkt końcowy ma dwa raporty (inspekcji i logowania), które zawierają wszystkie dane, które uzyskano w starym punkt końcowy interfejsu API. Ten nowy punkt końcowy ma również logowania raportu z licencji Azure AD Premium, która umożliwia pobieranie użycia aplikacji, użycie urządzeń i informacje logowania dla użytkownika.


--- 

**Pytanie: używam https://graph.windows.net/&lt;nazwa dzierżawcy&gt;/reports/ punktu końcowego API, aby pobierać raporty dotyczące zabezpieczeń usługi Azure AD (określone typy wykrywania, takie jak lub ujawnione poświadczenia logowania z anonimowych adresów IP) naszym systemy raportowania programowo. Co należy przełączyć?**

**A:** można użyć [zdarzenia o podwyższonym ryzyku Identity Protection API](active-directory-identityprotection-graph-getting-started.md) aby wykryć zabezpieczeń dostępu za pomocą programu Microsoft Graph. Ten nowy format zapewnia większą elastyczność w sposób można badać danych, za pomocą zaawansowane filtrowanie, pole wyboru i inne, a standaryzuje zdarzenia ryzyka do jednego typu ułatwia integrację z rozwiązaniem Siem i innych narzędzi do zbierania danych. Ponieważ dane są w innym formacie, nie może zastąpić nowe zapytanie stara zapytań. Jednak [nowy interfejs API korzysta z programu Microsoft Graph](https://developer.microsoft.com/graph/docs/api-reference/beta/resources/identityriskevent), który jest standardem Microsoft tych interfejsów API usługi Office 365 lub Azure AD. Dzięki pracy wymagane można rozszerzyć albo dotychczasowych inwestycji MS Graph Pomoc systemu lub rozpoczęciem przejście do ta nowa platforma standardowa.

--- 

**Pytanie: co to jest przechowywanie danych o Dzienniki aktywności (inspekcji i logowania) w portalu Azure?** 

**Odpowiedź:** udostępniamy 7 dni danych dla naszych klientów wolnego lub dostępnych danych przez maksymalnie 30 dni po zakupie usługi Azure AD Premium 1 lub Premium 2 licencji. Aby uzyskać więcej informacji na przechowywania raportów, zobacz [zasady przechowywania raportów usługi Azure Active Directory](active-directory-reporting-retention.md).

--- 

**Pytanie: jak długo trwa do momentu mogę zobaczyć dane o aktywności, po zakończeniu I Moje zadania?**

**Odpowiedź:** dzienników inspekcji działania mają opóźnienia, począwszy od 15 minut do godziny. Dzienniki aktywności logowania może potrwać od 15 minut do maksymalnie 2 godziny dla niektórych rekordów.

---

**Pytanie: czy muszę być administratorem globalnym, aby zobaczyć działanie logowania do portalu Azure lub uzyskać danych za pomocą interfejsu API?**

**Odpowiedź:** Nie. Musi być **czytnika zabezpieczeń**, **administratora zabezpieczeń**, lub **administratora globalnego** do pobrania danych w portalu Azure lub za pośrednictwem interfejsu API raportowania.

---

**Pytanie: czy można uzyskać informacji dziennika aktywności usługi Office 365 za pomocą portalu Azure?**

**Odpowiedź:** mimo że działania usługi Office 365 i Azure AD działania dzienniki udziału dużej ilości zasobów katalogu, jeśli chcesz pełnego widoku Dzienniki aktywności usługi Office 365, należy przejść do Centrum administracyjne usługi Office 365, aby uzyskać informacje dziennika Office 365 działania.

---


**Pytanie: które interfejsów API należy używać można pobrać informacji o dziennikach Office 365 działania?**

**Odpowiedź:** uzyskiwać dostęp do interfejsów API usługi Office 365 Management [Office 365 działanie logowania za pośrednictwem interfejsu API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).

---

**Pytanie: jak wiele rekordów I można pobrać z portalu Azure?**

**Odpowiedź:** maksymalnie 120 rekordów K można pobrać z portalu Azure. Rekordy są sortowane według *najnowszych* i domyślnie uzyskać najnowsze rekordy 120 K. 

---

**Pytanie: jak wiele rekordów można zbadać za pomocą działania interfejsu API?**

**Odpowiedź:** można zbadać 1 milion rekordy (Jeśli nie jest używany operator top sortuje rekordu przez większość ostatnie). Użycie operatora "top" można badać się do rekordów 500 KB. Przykładowe zapytania można znaleźć na temat korzystania z interfejsu API w tym miejscu [tutaj](active-directory-reporting-api-getting-started.md).

---

**Pytanie: jak uzyskać licencję premium?**

**Odpowiedź:** zobacz [wprowadzenie do korzystania z usługi Azure Active Directory Premium](active-directory-get-started-premium.md) dla odpowiedzi na to pytanie.

---

**Pytanie: jak najszybciej Zobacz dane działań po otrzymaniu licencji premium?**

**Odpowiedź:** Jeśli masz już dane działań jako wolne licencji, a następnie można zobaczyć te same dane. Jeśli nie masz żadnych danych, ich może zająć jeden lub dwa dni.

---

**Pytanie: wyświetlane dane z ostatniego miesiąca po otrzymaniu licencji usługi Azure AD premium?**

**Odpowiedź:** Jeśli włączono ostatnio do wersji Premium (w tym wersja próbna), można wyświetlić danych się do 7 dni początkowo. Gromadzi dane, zobaczysz maksymalnie 30 dni.

---

**Pytanie: Brak zdarzeń ryzyko w ochronę tożsamości, ale nie widzę odpowiedniego logowania w wszystkie sesje logowania. Jest to oczekiwane?**

**Odpowiedź:** tak, Identity Protection ocenia ryzyko dla wszystkich przepływów uwierzytelniania czy jeśli interakcyjnego lub nieinterakcyjnym. Jednak wszystkie sesje logowania tylko przedstawia tylko interakcyjnego logowania.

---

**Pytanie: jak można pobrać raportu "Użytkownicy oflagowani ryzyka" w portalu Azure**

**A:** opcję, aby pobrać *użytkownicy oflagowani ryzyka* raportu zostanie dodany wkrótce.

---

**Pytanie: jak dowiedzieć, dlaczego logowania lub użytkownikiem zostało oznaczone ryzykowne w portalu Azure**

**Odpowiedź:** klienci wersji Premium można dowiedzieć się więcej o podstawowym zdarzenia o podwyższonym ryzyku, klikając na użytkownika w "Użytkownicy oflagowani ryzyka" lub klikając na "ryzykowne logowania". Klienci bezpłatne i podstawowych wydanie uzyskać zagrożonych użytkowników i logowanie bez podstawowych informacji o zdarzeniu ryzyka.

---

**Pytanie: jak adresy IP są obliczane w logowania i logowania ryzykowne raport?**

**Odpowiedź:** adresy IP są przydzielane w taki sposób, że istnieje połączenie ostateczne między adresu IP i gdzie fizycznie znajduje się komputer o tym adresie. Skomplikowany czynników, takich jak przenośnych dostawców i sieci VPN często bardzo wydawania adresów IP z puli centralnej daleko od których urządzenie klienckie będzie faktycznie używana. Mając na uwadze powyższe, konwertowania adresu IP do fizycznej lokalizacji jest starań, na podstawie danych śledzenia, dane rejestru, odwrotnej wyszukiwań i inne informacje. 

---

**Pytanie: co to jest zdarzenie ryzyka "Zaloguj się przy dodatkowe ryzyko wykryto" oznaczają?**

**Odpowiedź:** zapewniające wgląd wszystkich ryzykowne logowania w środowisku zostanie przedstawiony zdarzeń ryzyka "Zaloguj się przy dodatkowe ryzyko wykryto" logowania z powodu wykrycia uważane za ryzykowne wyłączności do subskrybentów usługi Azure AD Identity Protection.

---
