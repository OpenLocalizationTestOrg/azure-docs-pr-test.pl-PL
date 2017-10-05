---
title: "Zasady przechowywania raportów w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: ffeba8a6c32a21c75af21f948bbd6ea88dd9278c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-report-retention-policies"></a>Zasady przechowywania raportów w usłudze Azure Active Directory


W tym temacie przedstawiono odpowiedzi na często zadawane pytania w połączeniu z przechowywaniem danych dla raportów innej aktywności w usłudze Azure Active Directory. 

**Pytanie: jak możesz uzyskać zbierania danych działania uruchomiona?**

**ODP.:**

| Wersja usługi Azure AD | Początkowy kolekcji |
| :--              | :--   |
| Usługa Azure AD — warstwa Premium P1 <br /> Usługa Azure AD — warstwa Premium P2 | Jeśli możesz przystąpić do subskrypcji |
| Usługa Azure AD — warstwa Bezpłatna | Przy pierwszym otwarciu [bloku usługi Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) lub użyj [raportowania interfejsów API](https://aka.ms/aadreports)  |

---
**Pytanie: kiedy dane działanie jest dostępne w portalu Azure**

**ODP.:**

- **Natychmiast** — Jeśli już pracy z raportami w klasycznym portalu Azure
- **W ciągu 2 godzin** — Jeśli nie włączono raportowania w klasycznym portalu Azure

---
**Pytanie: jak uzyskać kolekcja sygnałów zabezpieczeń uruchomić?**  

**Odpowiedź:** dla sygnałów zabezpieczeń procesu zbierania rozpoczyna się, gdy należy wyrazić zgodę na Użyj Centrum ochrony tożsamości. 


---
**Pytanie: na jak długo są zebrane dane przechowywane?**

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