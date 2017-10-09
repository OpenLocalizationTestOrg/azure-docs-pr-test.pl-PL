---
title: "aaaOperations zabezpieczeń pakietu zarządzania i bezpieczeństwo danych rozwiązania inspekcji | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób zarządzania danymi i ich ochrony w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 9cdf7deb-2a30-4672-b89f-71179ee8326a
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 9c4181b3b491e4f7f0c57d7252eca78a819722d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a>Bezpieczeństwo danych w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite
Klienci toohelp zapobiegania, wykrywania i odpowiadać toothreats, [zabezpieczeń Operations Management Suite (OMS) i rozwiązania inspekcji](operations-management-suite-overview.md) zbiera i przetwarza dane dotyczące zasobów, w tym:

* Dziennik zdarzeń zabezpieczeń
* Zdarzenia funkcji Śledzenie zdarzeń systemu Windows (ETW)
* Zdarzenia inspekcji funkcji AppLocker
* Dziennik zapory systemu Windows
* Zdarzenia rozwiązania Advanced Threat Analytics
* Wyniki oceny linii bazowej
* Wyniki oceny oprogramowania chroniącego przed złośliwym kodem
* Wyniki oceny aktualizacji/poprawek
* Strumienie audyt dzienników systemowych, które są jawnie włączone w agencie hello

Firma Microsoft wprowadzać silne zobowiązań tooprotect hello prywatności i bezpieczeństwa tych danych. Microsoft zgodnego toostrict wytycznych dotyczących zgodności i zabezpieczeń — od kodowania toooperating usługi.
Ten artykuł przedstawia sposób zarządzania danymi i ich ochrony w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie OMS.

## <a name="data-sources"></a>Źródła danych
Zabezpieczenia OMS i rozwiązanie inspekcji analizować dane z maszyn wirtualnych i fizycznych komputerów z zainstalowanym hello Agent pakietu OMS. Rozwiązanie Zabezpieczenia i inspekcja w pakiecie OMS może zbierać informacje o konfiguracji dotyczące zdarzeń zabezpieczeń, takich jak zdarzenia systemu Windows, dzienniki inspekcji, dzienniki usług IIS i komunikaty dziennika systemowego. Przykłady takich danych to: typ i wersja systemu operacyjnego, uruchomione procesy, nazwa maszyny, adresy IP, zalogowany użytkownik i identyfikator dzierżawy.  

## <a name="data-protection"></a>Ochrona danych
**Podział danych**: dane są przechowywane logicznie oddzielnie dla każdego składnika w całym hello usługi. Wszystkie dane są otagowane informacjami o organizacji. Znakowanie ten będzie nadal występował w całym cyklu życia danych hello i są wymuszane w każdej warstwie hello usługi. 

**Dostęp do danych**: tooprovide zalecenia dotyczące zabezpieczeń i Zbadaj możliwe zagrożenia bezpieczeństwa, personel firmy Microsoft może uzyskać dostępu do informacji zbieranych lub przeanalizowane przez usługi. Firma Microsoft jest zgodna toohello [warunki dotyczące usług Online firmy Microsoft](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) i [zasady zachowania poufności informacji](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), którego stan czy Microsoft będą używane dane klienta lub nie pochodzi informacji z niego anonsowaniu lub podobne do celów komercyjnych. zalecenia dotyczące zabezpieczeń tooprovide i Zbadaj możliwe zagrożenia bezpieczeństwa, personel firmy Microsoft może uzyskać dostępu do informacji zbieranych lub przeanalizowane przez usługi. Tylko używamy danych klienta jako tooprovide potrzebne, możesz z platformy Azure, usług, łącznie z celów jest zgodny z dostarczanie tych usług. Można zachować wszystkie prawa tooyour własnych danych.

**Użyj danych**: Firma Microsoft wykorzystuje wzorce i analizy zagrożeń widoczne w wielu dzierżawy tooenhance naszych możliwości wykrywania i zapobiegania; że odbywa się zgodnie z opisem w temacie zobowiązaniami prywatności hello naszych [prywatności Instrukcja](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).

> [!NOTE]
> Lokalizacja danych jest skonfigurowana na poziomie obszar roboczy OMS hello, podczas tworzenia obszaru roboczego hello, która jest częścią hello początkowej OMS zabezpieczeń i inspekcji procesu konfiguracji.
> 
> 

## <a name="see-also"></a>Zobacz też
W tym dokumencie przedstawiono sposób zarządzania danymi i ich ochrony w pakiecie OMS. toolearn więcej informacji na temat zabezpieczeń OMS i inspekcji rozwiązania, zobacz:

* [Omówienie pakietu Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Monitorowanie i alerty tooSecurity odpowiada Operations Management Suite zabezpieczeń i rozwiązanie inspekcji](oms-security-responding-alerts.md)
* [Monitorowanie zasobów w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite](oms-security-monitoring-resources.md)

