---
title: "Usługa Azure Active Directory raportowania opóźnienia | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o ilość czasu, jaki zajmuje zdarzeń do raportowania w portalu usługi Azure"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: mtillman
editor: 
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/15/2017
ms.author: markvi;dhanyahk
ms.reviewer: dhanyahk
ms.openlocfilehash: 5ec41817fede495b8262e28d2d614a480d98ff3b
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2017
---
# <a name="azure-active-directory-reporting-latencies"></a>Usługa Azure Active Directory opóźnienia raportowania

Z [raportowania](active-directory-preview-explainer.md) w usłudze Azure Active Directory, możesz uzyskać wszystkie informacje, należy określić, jak robi środowiska. Ilość czasu, jaki zajmuje dane raportowania były wyświetlane w portalu Azure jest nazywana opóźnienia. 

Ten temat zawiera informacje opóźnienia raportowania wszystkie kategorie w portalu Azure. 


## <a name="activity-reports"></a>Raporty dotyczące działań

Istnieją dwa obszary działania raportowania:

- **Działania związane z logowaniem** — informacje na temat użycia zarządzanych aplikacji i działania użytkownika związane z logowaniem
- **Dzienniki inspekcji** — informacje o aktywności systemu obejmujące zarządzanie użytkownikami i grupami oraz zarządzane aplikacje i działania dotyczące katalogu

Poniższa tabela zawiera informacje opóźnienia raporty aktywności.

| Raport | Minimalne | Średnia | Uwagi |
| :-- | --- | --- | :-- |
| Dzienniki inspekcji | 30 minut  | 1 godzina  |W niektórych przypadkach może potrwać maksymalnie 2 godziny dla danych działania inspekcji wyświetlani.|
| Logowania | 15 minut  | 2 godziny |W niektórych przypadkach może potrwać do 24 godzin dla danych logowania działania wyświetlone. W tym dane o aktywności logowania pochodzące z aplikacji starszej wersji pakietu office. |







## <a name="security-reports"></a>Raporty dotyczące zabezpieczeń

Istnieją dwa obszary raportowania zabezpieczeń:

- **Ryzykowne logowania** — ryzykowne logowanie jest wskaźnikiem próby logowania, które mogło zostać wykonane przez osobę, która nie jest prawowitym właścicielem konta użytkownika. 
- **Użytkownicy oflagowani w związku z ryzykiem** — ryzykowny użytkownik jest wskaźnikiem konta użytkownika, którego bezpieczeństwo mogło zostać naruszone. 

Poniższa tabela zawiera informacje opóźnienia raporty dotyczące zabezpieczeń.

| Raport | Minimalne | Średnia | Maksimum |
| :-- | --- | --- | --- |
| Narażeni użytkownicy          | 5 minut   | 15 minut  | 2 godziny  |
| Ryzykowne logowania         | 5 minut   | 15 minut  | 2 godziny  |

## <a name="risk-events"></a>Zdarzenia o podwyższonym ryzyku

Usługi Azure Active Directory korzysta z algorytmów uczenia maszynowego adaptacyjną i heurystyki do wykrycia podejrzanych działań, które są związane z kontami użytkowników. Każdy wykryty podejrzane działania są przechowywane w zdarzenia o nazwie ryzyko rekordu.

W poniższej tabeli wymieniono informacje opóźnienie dla zdarzeń o podwyższonym ryzyku.

| Raport | Minimalne | Średnia | Maksimum |
| :-- | --- | --- | --- |
| Logowania z anonimowych adresów IP |5 minut |15 minut |2 godziny |
| Logowania z nieznanych lokalizacji |5 minut |15 minut |2 godziny |
| Użytkownicy z ujawnionymi poświadczeniami |2 godziny |4 godziny |8 godzin |
| Niemożliwa podróż do nietypowych lokalizacji |5 minut |1 godzina |8 godzin  |
| Logowania z zainfekowanych urządzeń |2 godziny |4 godziny |8 godzin  |
| Logowania z adresów IP związanych z podejrzanymi działaniami |2 godziny |4 godziny |8 godzin  |



## <a name="next-steps"></a>Kolejne kroki

Jeśli chcesz dowiedzieć się więcej na temat raportów działania w portalu Azure, zobacz:

- [Działania logowania raportów w portalu usługi Azure Active Directory](active-directory-reporting-activity-sign-ins.md)
- [Raporty dotyczące działania inspekcji w portalu usługi Azure Active Directory](active-directory-reporting-activity-audit-logs.md)

Jeśli chcesz dowiedzieć się więcej o raporty dotyczące zabezpieczeń w portalu Azure, zobacz:

- [Użytkownicy ryzyka raport zabezpieczeń w portalu usługi Azure Active Directory](active-directory-reporting-security-user-at-risk.md)
- [Raport ryzykowne logowania w portalu usługi Azure Active Directory](active-directory-reporting-security-risky-sign-ins.md)

Jeśli chcesz dowiedzieć się więcej na temat zdarzeń o podwyższonym ryzyku, zobacz [zdarzenia o podwyższonym ryzyku usługi Azure Active Directory](active-directory-reporting-risk-events.md).
