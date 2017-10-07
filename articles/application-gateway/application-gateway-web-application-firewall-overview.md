---
title: Zapora aplikacji tooweb aaaIntroduction (WAF) dla bramy aplikacji Azure | Dokumentacja firmy Microsoft
description: "Ta strona zawiera omówienie zapory aplikacji sieci Web (WAF) w usłudze Application Gateway"
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 04b362bc-6653-4765-86f6-55ee8ec2a0ff
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: amsriva
ms.openlocfilehash: 5a42ce0fb2bd12a391844099e2de8fa2571195e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="web-application-firewall-waf"></a>Zapora aplikacji sieci Web

Zapora aplikacji sieci Web (WAF) to funkcja usługi Application Gateway, która zapewnia scentralizowaną ochronę aplikacji sieci Web przed typowymi programami wykorzystującymi luki i lukami w zabezpieczeniach. 

Zapora aplikacji sieci Web jest na podstawie reguł z hello [zestawów reguł core OWASP](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project) 3.0 lub 2.2.9. Aplikacje sieci Web coraz częściej stają się obiektami złośliwych ataków wykorzystujących znane luki w zabezpieczeniach. Typowe te luki w zabezpieczeniach ataki, skryptów krzyżowych ataków tooname kilka. Zapobieganie takich ataków w kodzie aplikacji może być trudne i może wymagać rygorystyczne konserwacji, monitorowanie w wielu warstw Topologia aplikacji hello i stosowanie poprawek. Zapora aplikacji sieci web scentralizowane ułatwia zarządzanie zabezpieczeniami znacznie prostsza i zapewnia lepsze zapewnienia administratorom tooapplication przed zagrożeniami lub wtargnięcia. Rozwiązanie zapory aplikacji sieci Web można reagować zagrożeniem bezpieczeństwa tooa szybsze przez stosowanie poprawek znane luki w zabezpieczeniach w centralnej lokalizacji i zabezpieczanie wszystkich aplikacji sieci web indywidualnych. Brama aplikacji w włączona jest Zapora aplikacji sieci web przekonwertowanego tooa można łatwo istniejącej bramy aplikacji.

![imageURLroute](./media/application-gateway-web-application-firewall-overview/WAF1.png)

Brama aplikacji w działa jako aplikacji dostarczania kontrolera i oferty kończenia żądań SSL, koligacji na podstawie pliku cookie sesji, rozkład obciążenia okrężnego, routing na podstawie zawartości, możliwość toohost wiele ulepszeń witryn sieci Web i zabezpieczeń. Ulepszenia zabezpieczeń oferowanych przez bramę aplikacji obejmują zarządzanie zasadami protokołu SSL, tooend zakończenia obsługi protokołu SSL. Zabezpieczenia aplikacji jest teraz wzmocniona zapory aplikacji sieci Web (Zapora aplikacji sieci web) bezpośrednio zintegrowane hello ADC oferty. To zapewnia łatwe tooconfigure toomanage centralnej lokalizacji i chronić aplikacje sieci web przed lukami w typowych sieci web.

## <a name="benefits"></a>Korzyści

hello core korzyści, które zapewniają zapory aplikacji sieci web i aplikacji bramy są następujące Hello:

### <a name="protection"></a>Ochrona

* Ochrona aplikacji sieci web przed atakami bez modyfikacji kodu toobackend i luk w zabezpieczeniach sieci web.

* Ochrona wielu sieci web aplikacji hello sam czas za bramy aplikacji. Brama aplikacji w obsługuje hosting się too20 witryn sieci Web za jednym bramy, która może być wszystkie chronione przed atakami opartymi na sieci web z zapory aplikacji sieci Web.

### <a name="monitoring"></a>Monitorowanie

* Monitoruj aplikacje sieci Web pod kątem ataków przy użyciu dziennika zapory aplikacji sieci Web w czasie rzeczywistym. Ten dziennik jest zintegrowany z [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview.md) tootrack zapory aplikacji sieci Web, alerty i dzienniki i ułatwia monitorowanie trendów.

* Zapora aplikacji sieci Web zostanie wkrótce zintegrowana z usługą Azure Security Center. Centrum zabezpieczeń Azure umożliwia centralnej w widoku stanu zabezpieczeń hello wszystkich zasobów platformy Azure.

### <a name="customization"></a>Dostosowywanie

* reguły zapory aplikacji sieci Web toocustomize możliwości Hello reguły grupy toosuit wymagań aplikacji i wyeliminować fałszywych alarmów.

## <a name="features"></a>Funkcje

Zapora aplikacji sieci Web ma wstępnie skonfigurowane z CRS 3.0 domyślnie lub możesz wybrać toouse 2.2.9. Zestaw CRS 3.0 oferuje mniejszą liczbę wyników fałszywie dodatnich niż wersja 2.2.9. Witaj możliwości zbyt[dostosować zasady toosuit potrzeb](application-gateway-customize-waf-rules-portal.md) jest dostępne. Niektóre hello zapory aplikacji sieci web, która chroni przed znanych luk w sieci web obejmuje:

* Ochrona przed atakami polegającymi na iniekcji SQL
* Ochrona przed atakami z użyciem skryptów wykorzystywanych w obrębie wielu witryn
* Częste ataki w ramach sieci Web polegające na iniekcji poleceń, przemycaniu żądań HTTP, rozdzielaniu odpowiedzi HTTP i zdalnym dołączaniu plików
* Ochrona przed naruszeniami protokołu HTTP
* Ochrona przed nieprawidłowościami protokołu HTTP, takimi jak brakujące powiązania agenta i użytkownika hosta oraz akceptowanie nagłówków
* Zapobieganie atakom z użyciem robotów, przeszukiwarek i skanerów
* Wykrywanie typowych błędów konfiguracji aplikacji (np. Apache, usługi IIS itp.)

Aby bardziej szczegółową listę reguł i ich ochrony, zobacz następujące hello [podstawowe zestawy reguł](#core-rule-sets).

### <a name="core-rule-sets"></a>Podstawowe zestawy reguł

Usługa Application Gateway obsługuje dwa zestawy reguł: CRS 3.0 i CRS 2.2.9. Są to kolekcje reguł, które chronią aplikacje sieci Web przed złośliwymi działaniami.

#### <a name="owasp30"></a>OWASP_3.0

zestaw reguł core Hello 3.0 podane ma 13 grupy reguł, jak pokazano w poniższej tabeli hello. Każda z tych grup reguł zawiera wiele reguł, które można wyłączyć.

|Grupa reguł|Opis|
|---|---|
|**[REQUEST-910-IP-REPUTATION](application-gateway-crs-rulegroups-rules.md#crs910)**|Zawiera reguły tooprotect względem znanych nadawcy wiadomości-śmieci lub złośliwych działań.|
|**[REQUEST-911-METHOD-ENFORCEMENT](application-gateway-crs-rulegroups-rules.md#crs911)**|Zawiera reguły toolock metody (PUT, PATCH <..)|
|**[REQUEST-912-DOS-PROTECTION](application-gateway-crs-rulegroups-rules.md#crs912)**| Zawiera reguły tooprotect przed atakami przeprowadzenie ataku typu "odmowa usługi" (DoS).|
|**[REQUEST-913-SCANNER-DETECTION](application-gateway-crs-rulegroups-rules.md#crs913)**| Zawiera reguły tooprotect przed skanery portu i środowiska.|
|**[REQUEST-920-PROTOCOL-ENFORCEMENT](application-gateway-crs-rulegroups-rules.md#crs920)**|Zawiera reguły tooprotect przed protokołu i kodowanie problemy.|
|**[REQUEST-921-PROTOCOL-ATTACK](application-gateway-crs-rulegroups-rules.md#crs921)**|Zawiera reguły tooprotect przed iniekcji nagłówka, smuggling żądania i odpowiedzi dzielenia|
|**[REQUEST-930-APPLICATION-ATTACK-LFI](application-gateway-crs-rulegroups-rules.md#crs930)**|Zawiera reguły tooprotect przed atakami typu pliku i ścieżkę.|
|**[REQUEST-931-APPLICATION-ATTACK-RFI](application-gateway-crs-rulegroups-rules.md#crs931)**|Zawiera reguły tooprotect przed dołączenie pliku zdalnego (RFI)|
|**[REQUEST-932-APPLICATION-ATTACK-RCE](application-gateway-crs-rulegroups-rules.md#crs932)**|Zawiera reguły tooprotect ponownie zdalne wykonywanie kodu.|
|**[REQUEST-933-APPLICATION-ATTACK-PHP](application-gateway-crs-rulegroups-rules.md#crs933)**|Zawiera reguły tooprotect przed atakami iniekcji PHP.|
|**[REQUEST-941-APPLICATION-ATTACK-XSS](application-gateway-crs-rulegroups-rules.md#crs941)**|Zawiera reguły ochrony przed atakami z użyciem skryptów w obrębie wielu witryn.|
|**[REQUEST-942-APPLICATION-ATTACK-SQLI](application-gateway-crs-rulegroups-rules.md#crs942)**|Zawiera reguły ochrony przed atakami polegającymi na iniekcji SQL.|
|**[REQUEST-943-APPLICATION-ATTACK-SESSION-FIXATION](application-gateway-crs-rulegroups-rules.md#crs943)**|Zawiera reguły tooprotect przed atakami opartymi na sesji utrwalania.|

#### <a name="owasp229"></a>OWASP_2.2.9

zestaw reguł core Hello 2.2.9 podane ma 10 grupy reguł, jak pokazano w poniższej tabeli hello. Każda z tych grup reguł zawiera wiele reguł, które można wyłączyć.

|Grupa reguł|Opis|
|---|---|
|**[crs_20_protocol_violations](application-gateway-crs-rulegroups-rules.md#crs20)**|Zawiera reguły tooprotect przed naruszeń protokołu (nieprawidłowe znaki, GET z treści żądania, itd.)|
|**[crs_21_protocol_anomalies](application-gateway-crs-rulegroups-rules.md#crs21)**|Zawiera reguły tooprotect przed informacje o nagłówku niepoprawne.|
|**[crs_23_request_limits](application-gateway-crs-rulegroups-rules.md#crs23)**|Zawiera reguły tooprotect argumentów lub pliki, które wykraczają poza ograniczenia.|
|**[crs_30_http_policy](application-gateway-crs-rulegroups-rules.md#crs30)**|Zawiera reguły tooprotect przed metody ograniczone, nagłówki i typy plików. |
|**[crs_35_bad_robots](application-gateway-crs-rulegroups-rules.md#crs35)**|Zawiera reguły tooprotect przed przeszukiwarki sieci web i skanery.|
|**[crs_40_generic_attacks](application-gateway-crs-rulegroups-rules.md#crs40)**|Zawiera reguły tooprotect przed atakami ogólnego (utrwalanie sesji dołączenie pliku zdalnego, iniekcji PHP, itp.)|
|**[crs_41_sql_injection_attacks](application-gateway-crs-rulegroups-rules.md#crs41sql)**|Zawiera reguły tooprotect przed atakami opartymi na wstrzyknięciu kodu SQL|
|**[crs_41_xss_attacks](application-gateway-crs-rulegroups-rules.md#crs41xss)**|Zawiera reguły tooprotect względem granic lokacji skryptów.|
|**[crs_42_tight_security](application-gateway-crs-rulegroups-rules.md#crs42)**|Zawiera tooprotect reguły, przed atakami przechodzenie ścieżka|
|**[crs_45_trojans](application-gateway-crs-rulegroups-rules.md#crs45)**|Zawiera reguły tooprotect przed to konie trojańskie.|

### <a name="waf-modes"></a>Tryby zapory aplikacji sieci Web

Bramy aplikacji zapory aplikacji sieci Web może być skonfigurowany toorun w następujących dwóch trybów hello:

* **Tryb wykrywania** — po toorun skonfigurowany w trybie wykrywania aplikacji bramy zapory aplikacji sieci Web monitoruje i rejestruje wszystkie alerty zagrożenia w pliku dziennika tooa. Rejestrowania diagnostyki bramy aplikacji powinna być włączona przy użyciu hello **diagnostyki** sekcji. Należy również tooensure, który hello zapory aplikacji sieci Web dziennika jest zaznaczone i włączona. Podczas pracy w trybie wykrywania zapora aplikacji sieci Web nie blokuje żądań przychodzących.
* **Tryb zapobiegania** — blokowaniu toorun skonfigurowany w trybie zapobiegania bramy aplikacji aktywnie wtargnięcia i atakami wykryte przez jego reguły. Osoba atakująca Hello odbiera 403 wyjątek nieautoryzowanego dostępu i hello połączenie zostało zakończone. Tryb zapobiegania nadal toolog takich ataków w dziennikach hello zapory aplikacji sieci Web.

### <a name="application-gateway-waf-reports"></a>Monitorowanie zapory aplikacji sieci Web

Ważne jest monitorowanie kondycji hello bramy aplikacji. Monitorowanie kondycji hello Twojej aplikacji sieci web aplikacji zapory i hello chroni są realizowane za pośrednictwem rejestrowania i integracja z usługą Azure monitora, Centrum zabezpieczeń Azure (wkrótce) i analizy dzienników.

![Diagnostyka](./media/application-gateway-web-application-firewall-overview/diagnostics.png)

#### <a name="azure-monitor"></a>Azure Monitor

Każdy dziennik bramy Application Gateway jest zintegrowany z usługą [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview.md).  Dzięki temu tootrack informacje diagnostyczne, łącznie z alertami zapory aplikacji sieci Web i dzienniki.  Ta funkcja jest dostępne w ramach hello zasobów brama aplikacji w portalu hello w obszarze hello **diagnostyki** karcie lub za pośrednictwem hello Azure monitora usługi bezpośrednio. toolearn więcej na temat włączania dzienników diagnostycznych dla bramy aplikacji można znaleźć [diagnostyki bramy aplikacji](application-gateway-diagnostics.md)

#### <a name="azure-security-center"></a>Azure Security Center

[Centrum zabezpieczeń Azure](../security-center/security-center-intro.md) pomaga zapobiegania, wykrywania i odpowie toothreats lepszy wgląd w i kontroli nad hello zabezpieczeń zasobów platformy Azure. Brama aplikacji jest teraz [zintegrowana z usługą Azure Security Center](application-gateway-integration-security-center.md). Centrum zabezpieczeń Azure skanuje aplikacji sieci web toodetect bez ochrony środowiska. Go teraz zaleca aplikacji bramy zapory aplikacji sieci Web tooprotect te zasoby narażone. Bramy aplikacji zapory aplikacji sieci Web można tworzyć bezpośrednio z hello Centrum zabezpieczeń Azure.  Te wystąpienia zapory aplikacji sieci Web są zintegrowane z Centrum zabezpieczeń Azure i będzie wysyłać alerty i informacje o kondycji ponownie tooAzure Centrum zabezpieczeń dla raportowania.

![rysunek 1](./media/application-gateway-web-application-firewall-overview/figure1.png)

#### <a name="logging"></a>Rejestrowanie

Zapora aplikacji sieci Web w usłudze Application Gateway dostarcza szczegółowe raporty w zakresie każdego wykrytego zagrożenia. Rejestrowanie jest zintegrowane z dziennikami diagnostycznymi platformy Azure, a alerty są zapisywane w formacie json. Te dzienniki można zintegrować z usługą [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).

![imageURLroute](./media/application-gateway-web-application-firewall-overview/waf2.png)

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupId}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{appGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

## <a name="application-gateway-waf-sku-pricing"></a>Cena jednostki SKU zapory aplikacji sieci Web w usłudze Application Gateway

Zapora aplikacji sieci Web jest dostępna w ramach nowej jednostki SKU zapory aplikacji sieci Web. Ta jednostka SKU jest dostępna tylko w modelu inicjowania obsługi usługi Azure Resource Manager i nie w obszarze hello klasycznego modelu wdrażania. Ponadto jednostka SKU zapory aplikacji sieci Web jest oferowana tylko w średnich i dużych rozmiarach wystąpień usługi Application Gateway. Wszystkie limity hello bramy aplikacji mają zastosowanie również toohello SKU zapory aplikacji sieci Web. Ceny zależą od opłaty godzinnej za wystąpienie bramy i opłaty za przetwarzanie danych. Opłata godzinna za bramę w przypadku jednostki SKU zapory aplikacji sieci Web różni się od opłat za standardową jednostkę SKU. Ceny można znaleźć na stronie [szczegółowego cennika usługi Application Gateway](https://azure.microsoft.com/pricing/details/application-gateway/). Przetwarzanie danych, pozostaną opłat hello takie same. Nie ma opłat za regułę lub grupę reguł. Wiele aplikacji sieci web można chronić za hello sama Zapora aplikacji sieci web i nie ma żadnych dodatkowych kosztów obsługi wielu aplikacji. 

Rozliczenia dotyczące zapory aplikacji sieci Web uruchamia skutecznie 5/5/2017 dopiero następnie hello bram SKU zapory aplikacji sieci Web kontynuuje toobe obciążona stawkami standardowymi.

## <a name="next-steps"></a>Następne kroki

Po więcej informacji na temat możliwości hello zapory aplikacji sieci Web, odwiedź stronę [jak Zapora aplikacji na bramie aplikacji sieci web na tooconfigure](application-gateway-web-application-firewall-portal.md).

