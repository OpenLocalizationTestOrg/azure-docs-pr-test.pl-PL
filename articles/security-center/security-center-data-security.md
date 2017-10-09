---
title: "aaaAzure danych Centrum zabezpieczeń | Dokumentacja firmy Microsoft"
description: "W tym dokumencie wyjaśniono, jak zarządzane i chronione są dane w usłudze Azure Security Center."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 33f2c9f4-21aa-4f0c-9e5e-4cd1223e39d7
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: yurid
ms.openlocfilehash: 30f8b11272dc5df6d485608abdaa62ba57e63f23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-data-security"></a>Azure Security Center — bezpieczeństwo danych
Klienci toohelp zapobiegania, wykrywania i odpowiadać toothreats, Centrum zabezpieczeń Azure zbiera i przetwarza dane związane z zabezpieczeniami, w tym informacje o konfiguracji, metadane, dzienniki zdarzeń i pliki zrzutu awaryjnego. Microsoft zgodnego toostrict wytycznych dotyczących zgodności i zabezpieczeń — od kodowania toooperating usługi.

W tym artykule wyjaśniono, jak zarządzane i chronione są dane w usłudze Azure Security Center.

>[!NOTE] 
>Począwszy od początku czerwca 2017, Centrum zabezpieczeń użyj toocollect Microsoft Monitoring Agent hello i przechowywania danych. Zobacz [migracji Platform Centrum zabezpieczeń Azure](security-center-platform-migration.md) toolearn więcej. Witaj informacje w tym artykule reprezentuje funkcji Centrum zabezpieczeń po toohello przejścia programu Microsoft Monitoring Agent.
>


## <a name="data-sources"></a>Źródła danych
Centrum zabezpieczeń Azure analizuje dane z powitania po widoczność tooprovide źródeł do Twojej stan zabezpieczeń, identyfikowanie luk w zabezpieczeniach i zaleca środki zaradcze oraz wykrywać zagrożenia active:

- Usług Azure: Używa informacji o konfiguracji hello usług platformy Azure została wdrożona, komunikując się z dostawcą zasobów tej usługi.
- Ruch sieciowy: używa próbkowanych metadanych ruchu sieciowego z infrastruktury firmy Microsoft, takich jak źródłowy i docelowy adres IP, źródłowy i docelowy port, rozmiar pakietu i protokół sieciowy.
- Rozwiązania partnerów: używa alertów zabezpieczeń z rozwiązań zintegrowanych partnerów, takich jak zapory i rozwiązania do ochrony przed złośliwym oprogramowaniem. 
- Maszyny wirtualne i serwery: używa pochodzących z maszyn wirtualnych informacji dotyczących konfiguracji oraz zdarzeń związanych z zabezpieczeniami, takich jak dzienniki inspekcji i zdarzeń systemu Windows, dzienniki usługi IIS, komunikaty programu Syslog oraz pliki zrzutu awaryjnego. Ponadto podczas tworzenia alertu Centrum zabezpieczeń Azure może wygenerować migawkę dysku maszyny Wirtualnej hello wpływ i Wyodrębnij alertu powiązane toohello artefaktów maszyny z hello dysku maszyny Wirtualnej, takie jak plik rejestru do celów dowodowe.


## <a name="data-protection"></a>Ochrona danych
**Podział danych**: dane są przechowywane logicznie oddzielnie dla każdego składnika w całym hello usługi. Wszystkie dane są otagowane informacjami o organizacji. Znakowanie ten będzie nadal występował w całym cyklu życia danych hello i są wymuszane w każdej warstwie hello usługi.

**Dostęp do danych**: W celu tooprovide zalecenia dotyczące zabezpieczeń i Zbadaj możliwe zagrożenia bezpieczeństwa, personel firmy Microsoft może uzyskać dostępu do informacji zbieranych lub przeanalizowane przez usługi Azure, w tym pliki zrzutu awaryjnego, przetworzyć zdarzenia tworzenia maszyny Wirtualnej Migawki dysków i artefaktów, które mogą przypadkowo obejmować dane klienta lub dane osobowe z maszyn wirtualnych. Firma Microsoft jest zgodna toohello [warunki dotyczące usług Online firmy Microsoft i zasady zachowania poufności informacji](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31), którego stan Microsoft zostanie nie korzystanie z danych klienta lub interpretowania go do celów reklamowych lub podobne komercyjnego. Tylko używamy danych klienta jako tooprovide potrzebne, możesz z platformy Azure, usług, łącznie z celów jest zgodny z dostarczanie tych usług. Możesz zachować wszystkie prawa tooCustomer danych.

**Użyj danych**: Firma Microsoft wykorzystuje wzorce i analizy zagrożeń widoczne w wielu dzierżawy tooenhance naszych możliwości wykrywania i zapobiegania; że odbywa się zgodnie z opisem w temacie zobowiązaniami prywatności hello naszych [prywatności Instrukcja](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).

## <a name="data-location"></a>Lokalizacja danych

**Twoje obszarów roboczych**: obszar roboczy jest określony dla powitania po obszarach geograficznych, i dane zbierane z maszyn wirtualnych platformy Azure, tym zrzuty awaryjne, a niektóre typy danych alertów są przechowywane w hello najbliższej obszaru roboczego. 

| Lokalizacja geograficzna maszyny wirtualnej                        | Lokalizacja geograficzna obszaru roboczego |
|-------------------------------|---------------|
| Stany Zjednoczone, Brazylia, Kanada | Stany Zjednoczone |
| Europa, Wielka Brytania        | Europa        |
| Azja i Pacyfik, Japonia, Indie    | Azja i Pacyfik  |
| Australia                     | Australia     |

 
Migawki dysków maszyny Wirtualnej są przechowywane w hello tego samego konta magazynu jako hello dysk maszyny Wirtualnej.
 
Dla maszyn wirtualnych i serwerach w innych środowiskach np. w infrastrukturze lokalnej, można określić obszaru roboczego hello i regionu, w którym są przechowywane dane zebrane. 

**Centrum zabezpieczeń Azure magazynu**: regionalnie przechowywane są informacje o alerty zabezpieczeń, między innymi alertów partnera, zgodnie z lokalizacji toohello hello powiązanych zasobów platformy Azure, natomiast informacje o stanie kondycji zabezpieczeń i zalecenia są przechowywane w USA hello lub Europy zgodnie z jego toocustomer lokalizacji.
Usługa Azure Security Center zbiera efemeryczne kopie plików zrzutu awaryjnego i analizuje je pod kątem dowodów na próby ich naruszenia i pomyślnie przeprowadzonych ataków. Centrum zabezpieczeń Azure wykonuje tę analizę w hello tej samej lokalizacji geograficznej, jak hello obszaru roboczego i usuwa hello tymczasowych kopii po zakończeniu analizy.

Artefakty maszyny są przechowywane w centralnie hello tego samego regionu, jak hello maszyny Wirtualnej. 


## <a name="managing-data-collection-from-virtual-machines"></a>Zarządzanie zbieraniem danych z maszyn wirtualnych

W przypadku włączenia usługi Security Center na platformie Azure zbieranie danych jest włączone dla każdej subskrypcji platformy Azure. Zbieranie danych można również włączyć dla subskrypcji w hello części zasady zabezpieczeń w Centrum zabezpieczeń Azure. Po włączeniu funkcji zbierania danych Centrum zabezpieczeń Azure przepisy hello Microsoft Monitoring Agent na wszystkich istniejących obsługiwanych maszyn wirtualnych platformy Azure i nowe pliki, które są tworzone. Hello program Microsoft Monitoring agent skanowania pod kątem różnych zabezpieczeń związane z konfiguracjami i zdarzeń do [śledzenia zdarzeń dla systemu Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) śladów (ETW). Ponadto hello systemu operacyjnego podczas trwania hello uruchomienie maszyny hello zgłosi zdarzenia z dziennika zdarzeń. Przykłady takich danych to typ systemu operacyjnego i jego wersja, dzienniki systemu operacyjnego (dzienniki zdarzeń systemu Windows), uruchomione procesy, nazwa maszyny, adresy IP, zalogowany użytkownik i identyfikator dzierżawy. Hello Microsoft Monitoring Agent odczytuje wpisy dziennika zdarzeń i śladów ETW i kopiuje je obszarów roboczych tooyour do analizy. Witaj Microsoft Monitoring Agent kopiuje awarii zrzutu pliki tooyour w obszarów roboczych.

Jeśli używasz bezpłatnej Centrum zabezpieczeń Azure, można również wyłączyć zbieranie danych z maszyn wirtualnych w hello zasady zabezpieczeń. Zbieranie danych jest wymagane dla subskrypcji w warstwie standardowa hello. Kolekcja artefaktów i migawki dysków maszyny wirtualnej będzie nadal włączona, nawet jeśli wyłączono zbieranie danych.


## <a name="see-also"></a>Zobacz też
W tym dokumencie wyjaśniono, jak zarządzane i chronione są dane w usłudze Azure Security Center. toolearn więcej informacji na temat Centrum zabezpieczeń Azure, zobacz:

* [Przewodnik planowania Centrum zabezpieczeń Azure i obsługi](security-center-planning-and-operations-guide.md) — Dowiedz się jak tooplan i zrozumieć zagadnienia dotyczące projektowania hello tooadopt Centrum zabezpieczeń Azure.
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się jak alerty toosecurity toomanage i odpowiedź
* [Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź
* [Blog Azure Security](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń i zgodności platformy Azure
