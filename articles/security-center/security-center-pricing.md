---
title: "Cennik Centrum zabezpieczeń | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 367b8f38cb9fcf3dc36db83641cb1696710608ef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-security-center-pricing"></a>Cennik Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure ułatwia zapobieganie zagrożeniom, ich wykrywanie i reagowanie na nie, a przy tym zapewnia lepszy wgląd i większą kontrolę w zakresie bezpieczeństwa zasobów na platformie Azure. Zapewnia zintegrowane monitorowanie zabezpieczeń i zarządzanie zasadami subskrypcji platformy Azure, pomaga wykrywać zagrożenia, które w przeciwnym razie mogłyby pozostać niezauważone, a także współpracuje z szerokim ekosystemem rozwiązań z zakresu zabezpieczeń.

## <a name="pricing-tiers"></a>Warstwy cenowe
Centrum zabezpieczeń jest oferowana w dwóch warstw:

* **Warstwę bezpłatna** jest automatycznie włączona dla wszystkich subskrypcji platformy Azure. Warstwa bezpłatna zapewnia wgląd w stan zabezpieczeń zasobów platformy Azure, zasady zabezpieczeń podstawowych, zalecenia dotyczące zabezpieczeń i integracja z produktów i usług zabezpieczeń z partnerami.
* **Warstwy standardowa** dodaje zagrożeń zaawansowane możliwości wykrywania, takie jak zagrożenia analizy, analizy behawioralnej, wykrywania anomalii, zdarzeń i raporty oceny zagrożeń. Warstwa Standardowa jest oferowana za darmo przez pierwsze 60 dni.

Aby uzyskać więcej informacji, zobacz temat w Centrum zabezpieczeń [cennikiem](https://azure.microsoft.com/pricing/details/security-center/).

## <a name="try-standard-free-for-60-days"></a>Spróbuj Standard bezpłatnie do 60 dni
Warstwa Standardowa jest oferowana za darmo przez pierwsze 60 dni. Na końcu 60 dni należy wybrać kontynuować korzystanie z usługi możemy zostaną automatycznie uruchomione opłat za zużycie.

Aby wyświetlić warstwy standardowa:

1. Wybierz kafelek **Zasady** w bloku **Centrum zabezpieczeń**.
2. Wybierz subskrypcję, którą chcesz uaktualnić do wersji Standard.
3. Na **zasady zabezpieczeń** bloku, wybierz opcję **warstwa cenowa**.
4. Na **wybierz warstwę cenową** bloku, wybierz opcję **standardowe**.
5. Kliknij pozycję **Wybierz**.


## <a name="why-upgrade-to-standard"></a>Dlaczego uaktualnienie ze standardem?
Planu Standard Centrum zabezpieczeń zapewnia wszystkie funkcje warstwę bezpłatna plus wykrywanie zagrożeń zaawansowane. Wykrywanie zagrożeń zaawansowane ułatwia zidentyfikowanie active zagrożenia przeznaczonych dla zasobów platformy Azure i zawiera szczegółowe informacje, konieczne jest szybko reagować.

Usługa Security Center wykorzystuje zaawansowane narzędzia analizy zabezpieczeń, które wykraczają daleko poza metody bazujące na sygnaturze. Osiągnięć w danych big data oraz technologii uczenia maszynowego są używane do analizowania zdarzeń w sieci szkieletowej chmury całego — wykrywanie zagrożenia, które nie można wysyłać do identyfikacji przy użyciu metod ręcznych i prognozowanie ewolucji ataków.

Analiza zabezpieczeń, które pochodzą z warstwy standardowa są:

* **Analizy zagrożeń** -szuka znanych nieupoważnione osoby za pomocą globalnej analizy zagrożeń z produktów firmy Microsoft i usług, jednostki ds. przestępstw cyfrowych firmy Microsoft, Microsoft Security Response Center i zewnętrznych źródeł danych
* **Analizę behawioralną** — ma zastosowanie znane wzorce do wykrywania złośliwego zachowania
* **Wykrywanie anomalii** -korzysta statystyczne profilowania w celu skompilowania historycznych linii bazowej. Generuje alert w odchylenia od ustalonych linie bazowe, które odpowiadają potencjalnych ataków

W **alerty zabezpieczeń** poniżej, w bloku Centrum zabezpieczeń wykrył zabezpieczeń **zdarzenia**. Zdarzenia zabezpieczeń jest agregacji wszystkich alertów dla zasobu, które są wyrównane z wzorców łańcucha kill. Wybranie zdarzenia zabezpieczeń ujawnia więcej szczegółów dotyczących zdarzenia i wyświetla powiązanych alertów. Wybieranie alertu zawiera więcej informacji na temat tego wystąpienia.

![Zdarzenie naruszenia zabezpieczeń][2]

**Komunikacja sieciowa** alert poniżej zawiera szczegóły dotyczące alertu. Szczegółowe informacje zawiera jego pełny opis, jego ważność, bieżącego stanu (co w tym przypadku jest odrzucane, co oznacza użytkownik miał akcji, aby je zamknąć), zaatakowanych zasobów i czynności korygujące. Istnieje również listę linki do raportów analizy zagrożeń firmy Microsoft. Te raporty może służyć do celów obrony i korygowania zabezpieczeń.

![Szczegóły alertu zabezpieczeń][3]

## <a name="enable-data-collection"></a>Włączanie zbierania danych
Aby włączyć analizy behawioralnej maszyny wirtualnej, musi być włączona funkcja zbierania danych.

Aby sprawdzić, czy włączono zbieranie danych:

1. Wybierz **zasad** kafelka. **Zasady zabezpieczeń** zostanie otwarty blok wyświetlanie subskrypcji platformy Azure.
2. Wybierz subskrypcję.
3. Jeśli **zbierania danych** jest wyłączone, zmień ją na i zapisać zmiany.

> [!NOTE]
> Jeśli używasz bezpłatnej Centrum zabezpieczeń Azure, możesz wyłączyć zbieranie danych z maszyn wirtualnych w zasadach zabezpieczeń. Zbieranie danych jest wymagane dla subskrypcji w warstwie Standardowa.
>
>

Zobacz [Włącz zbieranie danych w Centrum zabezpieczeń Azure](security-center-enable-data-collection.md) Aby uzyskać więcej informacji.

## <a name="next-steps"></a>Następne kroki
* W tym dokumencie zostały wprowadzone do ceny Centrum zabezpieczeń. Aby uzyskać dodatkowe informacje o cenach, zobacz Centrum zabezpieczeń [cennikiem](https://azure.microsoft.com/pricing/details/security-center/).
* Aby dowiedzieć się więcej na temat funkcji Zaawansowane wykrywania Centrum zabezpieczeń, zobacz [funkcji wykrywania Centrum zabezpieczeń Azure](security-center-detection-capabilities.md).
* Aby dowiedzieć się więcej na temat sposobu dane są zarządzane i w Centrum zabezpieczeń, zobacz [bezpieczeństwo danych w Centrum zabezpieczeń Azure](security-center-data-security.md).
* Jeśli masz pytania dotyczące korzystania z usługi Security Center, zobacz [Często zadawane pytania dotyczące usługi Azure Security Center](security-center-faq.md).
* Jeśli nadal masz pytania dotyczące korzystania z Centrum zabezpieczeń lub Azure, odwiedź stronę [fora Azure](https://social.msdn.microsoft.com/Forums/home?forum=AzureSecurityCenter&filter=alltypes&sort=lastpostdesc).

<!--Image references-->
[1]: ./media/security-center-pricing/standard.png
[2]: ./media/security-center-pricing/incident.png
[3]: ./media/security-center-pricing/network-alert.png
