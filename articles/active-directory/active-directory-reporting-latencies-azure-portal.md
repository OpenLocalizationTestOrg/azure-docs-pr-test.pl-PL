---
title: "opóźnienia raportowania usługi Active Directory aaaAzure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o hello ilość czasu, jaki zajmuje raporty tooshow zdarzenia w portalu Azure"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi;dhanyahk
ms.reviewer: dhanyahk
ms.openlocfilehash: eee959331262ba59b313dd038cb54699dbef48a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-latencies"></a>Usługa Azure Active Directory opóźnienia raportowania

Z [raportowania](active-directory-preview-explainer.md) w hello Azure Active Directory, możesz uzyskać wszystkie informacje hello należy toodetermine jak robi środowiska. Hello ilość czasu, jaki zajmuje raportowania danych tooshow się w portalu Azure hello jest także znana jako czas oczekiwania. 

Ten temat zawiera informacje opóźnienia hello hello wszystkie kategorie raportowania hello portalu Azure. 


## <a name="activity-reports"></a>Raporty dotyczące działań

Istnieją dwa obszary działania raportowania:

- **Działania logowania** — informacje na temat użycia hello zarządzanych aplikacji i aktywności logowania użytkowników
- **Dzienniki inspekcji** — informacje o aktywności systemu obejmujące zarządzanie użytkownikami i grupami oraz zarządzane aplikacje i działania dotyczące katalogu

w poniższej tabeli Hello zawiera informacje opóźnienia hello raporty aktywności.

| Raport | Minimalne | Średnia | Maksymalna |
| :-- | --- | --- | --- |
| Dzienniki inspekcji             | 30 minut  | 45 minut | 1 godzina     |
| Logowania               | 15 minut  | 15 minut | 2 godziny *   |

>[!NOTE]
> W przypadku niektórych danych działania logowania pochodzące z aplikacji starszej wersji pakietu office może potrwać too8 godzin hello raporty tooshow danych. 


## <a name="security-reports"></a>Raporty dotyczące zabezpieczeń

Istnieją dwa obszary raportowania zabezpieczeń:

- **Ryzykowne logowania** -ryzykowne logowanie jest wskaźnik prób logowania, które mogły zostać wykonane przez osobę, która nie jest właścicielem uzasadnionych hello konta użytkownika. 
- **Użytkownicy oflagowani w związku z ryzykiem** — ryzykowny użytkownik jest wskaźnikiem konta użytkownika, którego bezpieczeństwo mogło zostać naruszone. 

Witaj w poniższej tabeli znajdują się informacje opóźnienia hello zabezpieczeń raportów.

| Raport | Minimalne | Średnia | Maksymalna |
| :-- | --- | --- | --- |
| Narażeni użytkownicy          | 5 minut   | 15 minut  | 2 godziny  |
| Ryzykowne logowania         | 5 minut   | 15 minut  | 2 godziny  |

## <a name="risk-events"></a>Zdarzenia ryzyka

Usługa Azure Active Directory korzysta z adaptacyjną machine learning algorytmów i heurystyki toodetect podejrzane akcji, które są powiązane tooyour kont użytkowników. Każdy wykryty podejrzane działania są przechowywane w zdarzenia o nazwie ryzyko rekordu.

Witaj w poniższej tabeli znajdują się informacje opóźnienia hello dla zdarzeń o podwyższonym ryzyku.

| Raport | Minimalne | Średnia | Maksymalna |
| :-- | --- | --- | --- |
| Logowania z anonimowych adresów IP |5 minut |15 minut |2 godziny |
| Logowania z nieznanych lokalizacji |5 minut |15 minut |2 godziny |
| Użytkownicy z ujawnionymi poświadczeniami |2 godziny |4 godziny |8 godzin |
| Niemożliwa podróż tooatypical lokalizacji |5 minut |1 godzina |8 godzin  |
| Logowania z zainfekowanych urządzeń |2 godziny |4 godziny |8 godzin  |
| Logowania z adresów IP związanych z podejrzanymi działaniami |2 godziny |4 godziny |8 godzin  |



## <a name="next-steps"></a>Następne kroki

Jeśli chcesz tooknow więcej informacji na temat hello raporty aktywności w hello portalu Azure, zobacz:

- [Raporty aktywności logowania w portalu usługi Azure Active Directory hello](active-directory-reporting-activity-sign-ins.md)
- [Raporty dotyczące działań w portalu usługi Azure Active Directory hello inspekcji](active-directory-reporting-activity-audit-logs.md)

Więcej informacji na temat hello raporty dotyczące zabezpieczeń w portalu Azure hello tooknow, zobacz:

- [Użytkownicy ryzyka raport zabezpieczeń w portalu usługi Azure Active Directory hello](active-directory-reporting-security-user-at-risk.md)
- [Raport ryzykowne logowania w portalu usługi Azure Active Directory hello](active-directory-reporting-security-risky-sign-ins.md)

Aby uzyskać więcej informacji na temat zdarzeń o podwyższonym ryzyku tooknow zobacz [zdarzenia o podwyższonym ryzyku usługi Azure Active Directory](active-directory-reporting-risk-events.md).
