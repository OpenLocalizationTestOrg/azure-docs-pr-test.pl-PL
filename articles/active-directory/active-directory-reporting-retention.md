---
title: "zasady przechowywania raportów usługi Active Directory aaaAzure | Dokumentacja firmy Microsoft"
description: "Zasady przechowywania danych raportu w usłudze Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 183e53b0-0647-42e7-8abe-3e9ff424de12
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c46a68198cb34e9c92662b2f8461010745392c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-report-retention-policies"></a>Zasady przechowywania raportów w usłudze Azure Active Directory


W tym temacie przedstawiono odpowiedzi toohello często zadawane pytania w połączeniu z przechowywaniem danych hello hello raportów innej aktywności w usłudze Azure Active Directory. 

**Pytanie: jak uzyskać hello gromadzenia danych dotyczących działalności uruchomiona?**

**ODP.:**

| Wersja usługi Azure AD | Początkowy kolekcji |
| :--              | :--   |
| Usługa Azure AD — warstwa Premium P1 <br /> Usługa Azure AD — warstwa Premium P2 | Jeśli możesz przystąpić do subskrypcji |
| Usługa Azure AD — warstwa Bezpłatna | Witaj pierwszym otwarciu hello [bloku usługi Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) lub użyj hello [raportowania interfejsów API](https://aka.ms/aadreports)  |

---
**Pytanie: kiedy dane o aktywności jest dostępne w portalu Azure hello**

**ODP.:**

- **Natychmiast** — Jeśli już pracy z raportami w hello klasycznego portalu Azure
- **W ciągu 2 godzin** — Jeśli nie włączono raportowania w hello klasycznego portalu Azure

---
**Pytanie: jak uzyskać hello kolekcja sygnałów zabezpieczeń uruchomić?**  

**Odpowiedź:** dla sygnałów zabezpieczeń hello proces zbierania rozpoczyna się, gdy użytkownik uczestnictwa w Centrum ochrony tożsamości hello toouse. 


---
**Pytanie: jak długo ma hello zebrane dane przechowywane?**

**ODP.:**

**Raporty dotyczące działań**    

| Raport                 | Usługa Azure AD — warstwa Bezpłatna | Usługa Azure AD — warstwa Premium P1 | Usługa Azure AD — warstwa Premium P2 |
| :--                    | :--           | :--                 | :--                 |
| Inspekcja katalogu        | 7 dni        | 30 dni             | 30 dni             |
| Aktywność związana z logowaniem       | 7 dni        | 30 dni             | 30 dni             |

**Sygnały zabezpieczeń**

| Raport         | Usługa Azure AD — warstwa Bezpłatna | Usługa Azure AD — warstwa Premium P1 | Usługa Azure AD — warstwa Premium P2 |
| :--            | :--           | :--                 | :--                 |
| Narażeni użytkownicy  | 7 dni        | 30 dni             | 90 dni             |
| Ryzykowne logowania | 7 dni        | 30 dni             | 90 dni             |

---