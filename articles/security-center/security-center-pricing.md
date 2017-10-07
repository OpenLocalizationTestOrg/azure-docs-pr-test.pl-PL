---
title: Cennik aaaSecurity Center | Dokumentacja firmy Microsoft
description: "Ten artykuł zawiera informacje o cenach dla Centrum zabezpieczeń Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4d1364cd-7847-425a-bb3a-722cb0779f78
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 93cc284540114b048b7a960891c0e68553b008be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-pricing"></a>Cennik Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure ułatwia zapobieganie, wykrywania i odpowie toothreats lepszy wgląd w i kontroli nad hello zabezpieczeń zasobów platformy Azure. Zapewnia zintegrowane monitorowanie zabezpieczeń i zarządzanie zasadami subskrypcji platformy Azure, pomaga wykrywać zagrożenia, które w przeciwnym razie mogłyby pozostać niezauważone, a także współpracuje z szerokim ekosystemem rozwiązań z zakresu zabezpieczeń.

## <a name="pricing-tiers"></a>Warstwy cenowe
Centrum zabezpieczeń jest oferowana w dwóch warstw:

* Witaj **warstwę bezpłatna** jest automatycznie włączona dla wszystkich subskrypcji platformy Azure. Warstwa bezpłatna Hello zapewnia wgląd w hello stan zabezpieczeń zasobów platformy Azure, zasady zabezpieczeń podstawowych, zalecenia dotyczące zabezpieczeń i integracja z produktów i usług zabezpieczeń partnerów.
* Witaj **warstwy standardowa** dodaje zagrożeń zaawansowane możliwości wykrywania, takie jak zagrożenia analizy, analizy behawioralnej, wykrywania anomalii, zdarzeń i raporty oceny zagrożeń. warstwy standardowa Hello jest oferowane bezpłatnie dla hello pierwsze 60 dni.

Aby uzyskać więcej informacji, zobacz temat Centrum zabezpieczeń hello [cennikiem](https://azure.microsoft.com/pricing/details/security-center/).

## <a name="try-standard-free-for-60-days"></a>Spróbuj Standard bezpłatnie do 60 dni
warstwy standardowa Hello jest oferowane bezpłatnie dla hello pierwsze 60 dni. Na końcu hello 60 dni należy wybrać toocontinue przy użyciu usługi hello, firma Microsoft automatycznie rozpocznie opłat za zużycie.

tooget hello warstwy standardowa:

1. Wybierz hello **zasad** Kafelek na powitania **Centrum zabezpieczeń** bloku.
2. Wybierz subskrypcję hello, które mają tooupgrade tooStandard.
3. Na powitania **zasady zabezpieczeń** bloku, wybierz opcję **warstwa cenowa**.
4. Na powitania **wybierz warstwę cenową** bloku, wybierz opcję **standardowe**.
5. Kliknij pozycję **Wybierz**.


## <a name="why-upgrade-toostandard"></a>Dlaczego uaktualnienie tooStandard?
warstwy standardowa Hello Centrum zabezpieczeń zapewnia wszystkie funkcje warstwę bezpłatna hello plus wykrywanie zagrożeń zaawansowane. Zaawansowane zagrożenia wykrywania ułatwia identyfikowanie active zagrożenia przeznaczonych dla zasobów platformy Azure i zapewnia wgląd hello potrzebne toorespond szybko.

Usługa Security Center wykorzystuje zaawansowane narzędzia analizy zabezpieczeń, które wykraczają daleko poza metody bazujące na sygnaturze. Osiągnięć w danych big data oraz technologii uczenia maszynowego to zdarzenia tooevaluate używanych w sieci szkieletowej chmury całego hello — wykrywanie zagrożeń, które byłoby niemożliwe tooidentify przy użyciu metod ręcznych i prognozowanie ewolucji hello ataków.

Analiza zabezpieczeń, dołączone do warstwy standardowa hello są:

* **Analizy zagrożeń** -wygląda dla znanych nieupoważnione osoby za pomocą globalnej analizy zagrożeń ze swoich produktów i usług, hello Microsoft jednostki, hello Microsoft Security Response Center i zewnętrznych źródeł danych
* **Analizę behawioralną** — ma zastosowanie znane wzorce toodiscover złośliwego zachowania
* **Wykrywanie anomalii** -używa statystyczne profilowania toobuild historycznych linii bazowej. Generuje alert w odchylenia od ustalonych linii bazowych, zgodnych ze standardami tooa potencjalnych ataków

W hello **alerty zabezpieczeń** poniżej, w bloku Centrum zabezpieczeń wykrył zabezpieczeń **zdarzenia**. Zdarzenia zabezpieczeń jest agregacji wszystkich alertów dla zasobu, które są wyrównane z wzorców łańcucha kill. Wybór naruszające hello ujawnia więcej szczegółów na temat hello zdarzenia i list hello powiązanych alertów. Wybieranie alertu zawiera więcej informacji na temat tego wystąpienia.

![Zdarzenie naruszenia zabezpieczeń][2]

Witaj **komunikacja sieciowa** alert poniżej szczegółowe informacje na temat hello alertu. Szczegółowe informacje zawiera jego pełny opis, jego ważność, jego bieżący stan (który w tym przypadku jest odrzucane, znaczenie hello użytkownik przejął toodismiss akcji go), hello zaatakowany zasób i czynności korygujące. Istnieje również listę tooMicrosoft łącza, które raporty analizy zagrożeń. Te raporty może służyć do celów obrony i korygowania zabezpieczeń.

![Szczegóły alertu zabezpieczeń][3]

## <a name="enable-data-collection"></a>Włączanie zbierania danych
tooenable analizy behawioralnej maszyny wirtualnej, zbierania danych musi być włączona.

czy włączono zbieranie danych toovalidate:

1. Wybierz hello **zasad** kafelka. Witaj **zasady zabezpieczeń** zostanie otwarty blok wyświetlanie subskrypcji platformy Azure.
2. Wybierz subskrypcję.
3. Jeśli **zbierania danych** jest wyłączone, zmień ją tooon i Zapisz zmiany hello.

> [!NOTE]
> Jeśli używasz bezpłatnej Centrum zabezpieczeń Azure, możesz wyłączyć zbieranie danych z maszyn wirtualnych w hello zasady zabezpieczeń. Zbieranie danych jest wymagane dla subskrypcji w warstwie standardowa hello.
>
>

Zobacz [Włącz zbieranie danych w Centrum zabezpieczeń Azure](security-center-enable-data-collection.md) Aby uzyskać więcej informacji.

## <a name="next-steps"></a>Następne kroki
* W tym dokumencie możesz zostały wprowadzone toopricing dla Centrum zabezpieczeń. Aby uzyskać dodatkowe informacje o cenach, zobacz hello Centrum zabezpieczeń [cennikiem](https://azure.microsoft.com/pricing/details/security-center/).
* Zaawansowane możliwości wykrywania toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz [funkcji wykrywania Centrum zabezpieczeń Azure](security-center-detection-capabilities.md).
* toolearn więcej informacji na temat jak dane są zarządzane i w Centrum zabezpieczeń, zobacz [bezpieczeństwo danych w Centrum zabezpieczeń Azure](security-center-data-security.md).
* Jeśli masz pytania dotyczące korzystania z Centrum zabezpieczeń, zobacz hello [często zadawane pytania dotyczące usługi Azure Security Center](security-center-faq.md).
* Jeśli nadal masz pytania dotyczące korzystania z Centrum zabezpieczeń lub Azure, odwiedź stronę hello [fora Azure](https://social.msdn.microsoft.com/Forums/home?forum=AzureSecurityCenter&filter=alltypes&sort=lastpostdesc).

<!--Image references-->
[1]: ./media/security-center-pricing/standard.png
[2]: ./media/security-center-pricing/incident.png
[3]: ./media/security-center-pricing/network-alert.png
