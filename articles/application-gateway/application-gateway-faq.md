---
title: "aaaFrequently zadawane pytania dotyczące usługi Azure Application Gateway | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera odpowiedzi toofrequently zadawane pytania dotyczące bramy aplikacji Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d54ee7ec-4d6b-4db7-8a17-6513fda7e392
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: b2df3a82a71a3264d3d34d317d08e4b4f72c6e3e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a>Często zadawane pytania dotyczące bramy aplikacji

## <a name="general"></a>Ogólne

**Q. Co to jest brama aplikacji?**

Bramy aplikacji Azure jest kontrolera dostarczania aplikacji (ADC) jako usługa, oferty różne obciążenia warstwy 7 równoważenia możliwości dla aplikacji. Zapewnia wysoką dostępność i skalowalność usługi, która jest w pełni zarządzana przez Azure.

**Q. Jakie funkcje obsługuje bramy aplikacji?**

Brama aplikacji w obsługuje SSL Odciążanie i na końcu tooend SSL, Zapora aplikacji sieci Web, koligacji na podstawie plików cookie sesji, adres url na podstawie ścieżki routingu, wielu lokacji hosting i inne. Aby uzyskać pełną listę obsługiwanych funkcji, odwiedź stronę [tooApplication wprowadzenie bramy](application-gateway-introduction.md)

**Q. Jaka jest różnica hello między bramą aplikacji i usługi równoważenia obciążenia Azure?**

Brama aplikacji jest modułem równoważenia obciążenia warstwy 7, co oznacza, że w przypadku ruchu w sieci web tylko (WebSocket-HTTP/HTTPS). Obsługuje ona możliwości, takie jak zakończenie protokołu SSL, koligacji na podstawie plików cookie sesji i okrężnego dla ruchu równoważenia obciążenia. Moduł równoważenia obciążenia, załadowanie salda ruchu na poziomie warstwy 4 (TCP/UDP).

**Q. Jakie protokoły obsługuje bramy aplikacji?**

Brama aplikacji w obsługuje HTTP, HTTPS i protokołu WebSocket.

**Q. Jakie zasoby są obsługiwane obecnie częścią puli wewnętrznej bazy danych?**

Pul zaplecza może składać się z kart sieciowych, zestawy skalowania maszyny wirtualnej, publiczne adresy IP, wewnętrzny adresów IP, w pełni kwalifikowaną nazwę (FQDN) i zapleczy wielodostępne takich jak aplikacje sieci Web platformy Azure. Brama aplikacji, elementy członkowskie puli wewnętrznej bazy danych nie są powiązane tooan zestawu dostępności. Elementami członkowskimi pul zaplecza może być między klastrami i centrami danych, lub poza platformą Azure, jak długo mają połączenia IP.

**Q. Jakich regionach jest dostępna w hello usługi?**

Brama aplikacji jest dostępna we wszystkich regionach Azure globalnego. Jest również dostępna w [chińskiej wersji platformy Azure](https://www.azure.cn/) i [Azure dla instytucji rządowych](https://azure.microsoft.com/en-us/overview/clouds/government/)

**Q. Jest to dedykowane wdrożenia dla mojej subskrypcji lub jest on udostępniony przez klientów?**

Brama aplikacji jest dedykowany wdrażania w sieci wirtualnej.

**Q. Jest HTTP -> obsługiwanych przekierowanie protokołu HTTPS**

Przekierowanie jest obsługiwane. Odwiedź stronę [omówienie przekierowania aplikacji bramy](application-gateway-redirect-overview.md) toolearn więcej.

**Q. W jakiej kolejności odbiorników przetwarzania?**

Obiekty nasłuchujące są przetwarzane w kolejności hello są wyświetlane. Dlatego jeśli odbiornik podstawowe pasuje do przychodzącego żądania przetwarza je najpierw.  Odbiorniki obejmujący wiele lokacji należy skonfigurować przed ruchu tooensure odbiornika podstawowa jest kierowany toohello poprawne zaplecza.

**Q. Gdzie znaleźć adresów IP i DNS bramy aplikacji**

Korzystając z publicznym adresem IP jako punktu końcowego, te informacje można znaleźć na powitania zasobu publicznego adresu IP lub na stronie Przegląd hello na powitania brama aplikacji w portalu hello. Dla adresów IP to można znaleźć na stronie Przegląd hello.

**Q. Czy hello adres IP lub DNS zmienia się na okres istnienia hello hello bramy aplikacji?**

Witaj VIP można zmienić bramy hello jest zatrzymana i uruchomiona przez powitania klienta. nie zmienia DNS skojarzone z bramą aplikacji Hello cyklem hello hello bramy. Z tego powodu jest zalecane toouse aliasu CNAME, aby wskazywał adresu DNS toohello hello Application Gateway.

**Q. Brama aplikacji w obsługuje statyczny adres IP?**

Nie, bramy aplikacji nie obsługuje statyczne publiczne adresy IP, ale obsługuje statyczne wewnętrzne adresy IP.

**Q. Brama aplikacji w obsługuje wiele publicznych adresów IP dla bramy hello?**

Dotyczy tylko jeden publiczny adres IP bramy aplikacji.

**Q. Brama aplikacji w obsługuje x przekazywane dla nagłówków?**

Tak, bramy aplikacji wstawia x przekazywane do, x przekazywane — protokół i nagłówki x przekazywane — port do żądania hello przekazywane toohello wewnętrznej bazy danych. format Hello x przekazywane do nagłówka jest rozdzielana przecinkami lista IP:Port. Prawidłowe wartości x przekazywane proto Hello to http lub https. X-przekazywane — port Określa hello portu, na którym żądania hello na powitania bramy aplikacji.

**Q. Jak długo trwa toodeploy bramę aplikacji? Brama mojej aplikacji nadal działa podczas aktualizowana?**

Nowe wdrożenia bramy aplikacji może potrwać too20 tooprovision minut. Tooinstance zmiany rozmiaru/liczby nie są zakłócenie i bramy hello pozostaje aktywna w tym czasie.

## <a name="configuration"></a>Konfiguracja

**Q. Brama aplikacji zawsze wdrożonej w sieci wirtualnej?**

Tak, bramy aplikacji zawsze jest wdrażana w podsieci sieci wirtualnej. Ta podsieć może zawierać tylko bramy aplikacji.

**Q. Brama aplikacji można rozmawiać tooinstances poza jego sieci wirtualnej?**

Brama aplikacji można rozmawiać tooinstances poza hello sieci wirtualnej jest tak długo, jak brak połączenia IP. Jeśli planujesz toouse wymaga wewnętrznych adresów IP jako elementy członkowskie puli wewnętrznej bazy danych, a następnie go [sieci Wirtualnej komunikacji równorzędnej](../virtual-network/virtual-network-peering-overview.md) lub [bramy sieci VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).

**Q. Można wdrożyć niczego więcej w podsieci bramy aplikacji hello?**

Nie, ale można wdrożyć inne bramy aplikacji w podsieci hello.

**Q. Sieciowe grupy zabezpieczeń są obsługiwane w podsieci bramy aplikacji hello?**

Sieciowe grupy zabezpieczeń są obsługiwane w podsieci bramy aplikacji hello z hello następujące ograniczenia:

* Wyjątki musi znajdować się w dla ruchu przychodzącego na porty 65503 65534 wewnętrznej bazy danych kondycji toowork poprawnie.

* Wychodzące połączenie z Internetem nie mogą zostać zablokowane.

* Wymagane jest zezwolenie ruch z hello znacznik AzureLoadBalancer.

**Q. Jakie są limity hello na bramie aplikacji? Można zwiększyć te limity?**

Odwiedź stronę [limitów bramy aplikacji](../azure-subscription-service-limits.md#application-gateway-limits) tooview hello limity.

**Q. Czy można użyć bramy aplikacji wewnętrznych i zewnętrznych ruchu równocześnie?**

Tak, Application Gateway obsługuje jeden adres IP wewnętrzny i jeden zewnętrznego adresu IP dla bramy aplikacji.

**Q. Czy sieci wirtualnej komunikacji równorzędnej obsługiwane?**

Tak, w sieci wirtualnej komunikacji równorzędnej jest obsługiwany i jest przydatne w przypadku ruchu w innych sieciach wirtualnych równoważenia obciążenia.

**Q. Serwery lokalne tooon można rozmawiać po nawiązaniu przez tunele ExpressRoute lub sieci VPN?**

Tak, jak długo ruch jest dozwolony.

**Q. Czy można mieć jedną pulę zaplecza obsługujący wiele aplikacji w różnych portów**

Architektura usługi Micro jest obsługiwana. Będzie potrzebny wielu tooprobe skonfigurowane ustawienia http na różnych portów.

**Q. Niestandardowe sond obsługują symboli wieloznacznych/regex na odpowiedź na żądanie danych?**

Niestandardowe sond nie obsługują symboli wieloznacznych i wyrażeń regularnych na dane odpowiedzi. 

**Q. Jak są przetwarzane reguły**

Reguły są przetwarzane w kolejności hello są skonfigurowane. Zaleca się, że obejmujący wiele lokacji skonfigurowanych reguł przed podstawowych reguł tooreduce hello ryzyko, że ruch jest kierowane toohello nieodpowiednie wewnętrznej bazy danych jako hello podstawowe reguły będzie zgodny z ruchu na podstawie reguły obejmujący wiele lokacji toohello poprzedniego portu oceniane.

**Q. Jak są przetwarzane reguły**

Reguły są przetwarzane w kolejności hello, które zostały utworzone. Zaleca się, że przed podstawowych reguł skonfigurowanych reguł obejmujący wiele lokacji. Konfigurując odbiorników obejmujący wiele lokacji najpierw, ta konfiguracja ogranicza hello prawdopodobieństwo, że ruch jest kierowany toohello nieodpowiednie wewnętrznej bazy danych. Ten problem routingu mogą występować hello podstawowe reguły spowoduje dopasowanie ruchu na podstawie reguły obejmujący wiele lokacji toohello poprzedniego portu oceniane.

**Q. Co to oznaczającego hello hosta pola niestandardowe sond?**

Określa hello nazwa toosend hello sondy do hosta. Dotyczy tylko wtedy, gdy obejmujący wiele lokacji jest skonfigurowany dla bramy aplikacji, w przeciwnym razie użyj '127.0.0.1'. Ta wartość jest inna niż nazwa hosta maszyny Wirtualnej i jest w formacie \<protokołu\>://\<hosta\>:\<portu\>\<ścieżki\>.

**Q. Czy mogę tooa dostępu bramy aplikacji dozwolonych kilku źródłowych adresów IP?**

W tym scenariuszu można zrobić za pomocą grup NSG podsieci bramy aplikacji. następujące ograniczenia Hello należy umieścić w podsieci hello hello wymienionych według priorytetu:

* Zezwalaj na ruch przychodzący z zakresu adresów IP/IP źródła.

* Zezwalaj na przychodzące żądania z wszystkich źródeł tooports 65503 65534 dla [zaplecza kondycji komunikacji](application-gateway-diagnostics.md).

* Zezwalaj na przychodzące sondy modułu równoważenia obciążenia Azure (znacznik AzureLoadBalancer) i ruch przychodzący sieci wirtualnych (znacznik VirtualNetwork) na powitania [NSG](../virtual-network/virtual-networks-nsg.md).

* Blokuj wszystkie pozostałe ruch przychodzący z odmowy wszystkie reguły.

* Zezwalaj na ruch wychodzący toohello internet dla wszystkich miejsc docelowych.

## <a name="performance"></a>Wydajność

**Q. Jak bramy aplikacji obsługuje wysoką dostępność i skalowalność?**

Brama aplikacji w obsługuje realizację scenariuszy wysokiej dostępności, jeśli masz co najmniej dwa wystąpienia wdrożone. Azure rozdziela te wystąpienia wiele aktualizacji i odporność tooensure domen, że wszystkie wystąpienia nie kończyć się niepowodzeniem na powitania tym samym czasie. Brama aplikacji w obsługuje skalowalność, dodając hello wiele wystąpień tego samego obciążenia hello tooshare bramy.

**Q. Jak uzyskać scenariusza odzyskiwania po awarii między centrami danych z bramą aplikacji?**

Klienci mogą użyć Menedżera ruchu toodistribute ruchu między wiele bram aplikacji w różnych centrach danych.

**Q. Czy automatyczne skalowanie obsługiwane?**

Nie, ale brama aplikacji ma Metryka przepływności, które mogą być używane tooalert należy po osiągnięciu progu. Ręcznie Dodawanie wystąpień lub zmiana rozmiaru nie jest ponownie uruchamiany hello bramy i nie ma wpływu na istniejące ruchu.

**Q. Czy ręczne skalowania w górę/dół Przyczyna Przestój?**

Nie istnieje bez przestojów, wystąpienia są rozproszone na uaktualnienia domen i domen błędów.

**Q. Czy można zmienić rozmiar wystąpienia z średnia toolarge bez zakłóceń**

Tak, Azure rozdziela wystąpień wiele aktualizacji i odporność tooensure domen, że wszystkie wystąpienia nie kończyć się niepowodzeniem na powitania tym samym czasie. Aplikacja obsługuje bramy skalowania, dodając wiele wystąpień hello tej samej bramy tooshare hello obciążenia.

## <a name="ssl-configuration"></a>Konfiguracja protokołu SSL

**Q. Jakie certyfikaty są obsługiwane w bramie aplikacji?**

Z podpisem własnym certyfikatami, certyfikaty urzędu certyfikacji i certyfikatów — symbol wieloznaczny są obsługiwane. Weryfikacją certyfikaty nie są obsługiwane.

**Q. Co to są hello bieżącego mechanizmów szyfrowania obsługiwanych przez bramę aplikacji?**

Oto Hello hello bieżącego mechanizmów szyfrowania obsługiwanych przez bramę aplikacji. Odwiedź stronę: [Konfigurowanie SSL wersji zasad i mechanizmów szyfrowania w bramie aplikacji](application-gateway-configure-ssl-policy-powershell.md) toolearn jak toocustomize opcje protokołu SSL.

- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
- TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_256_GCM_SHA384
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_3DES_EDE_CBC_SHA
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA

**Q. Brama aplikacji w również obsługuje ponownego szyfrowania ruchu toohello wewnętrznej bazy danych?**

Tak, Application Gateway obsługuje SSL odciążania i tooend końcowych SSL, który szyfruje ponownie hello ruchu toohello wewnętrznej bazy danych.

**Q. Można skonfigurować wersji protokołu SSL toocontrol zasad SSL?**

Tak, można skonfigurować bramy aplikacji toodeny TLS1.0, TLS1.1 i TLS1.2. Protokół SSL 2.0 i 3.0 już są domyślnie wyłączone i nie są konfigurowalne.

**Q. Można skonfigurować mechanizmów szyfrowania i kolejność zasad?**

Tak, [konfiguracji mechanizmów szyfrowania](application-gateway-ssl-policy-overview.md) jest obsługiwana. Podczas definiowania zasad niestandardowych, należy włączyć co najmniej jeden z hello następujące mechanizmy szyfrowania. Brama aplikacji w używa SHA256 toofor wewnętrznej bazy danych zarządzania.

* TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 
* TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
* TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
* TLS_RSA_WITH_AES_128_GCM_SHA256
* TLS_RSA_WITH_AES_256_CBC_SHA256
* TLS_RSA_WITH_AES_128_CBC_SHA256

**Q. Jak wiele certyfikatów SSL są obsługiwane?**

Zapasowej too20 SSL certyfikaty są obsługiwane.

**Q. Jak wiele certyfikatów uwierzytelniania w celu ponownego szyfrowania wewnętrznej bazy danych są obsługiwane?**

Zapasowej too10 certyfikatów uwierzytelniania są obsługiwane z domyślną 5.

**Q. Czy brama aplikacji można zintegrować z usługą Azure Key Vault natywnie?**

Nie, nie jest zintegrowany z usługą Azure Key Vault.

## <a name="web-application-firewall-waf-configuration"></a>Konfiguracja zapory (WAF) dla aplikacji sieci Web

**Q. Witaj SKU zapory aplikacji sieci Web oferuje wszystkie funkcje hello dostępne hello standardowy SKU?**

Tak, zapory aplikacji sieci Web obsługuje wszystkie funkcje hello hello standardowy SKU.

**Q. Co to jest hello CRS wersji, która obsługuje bramy aplikacji?**

Brama aplikacji w obsługuje znaki CR [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) i CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).

**Q. Jak monitorować zapory aplikacji sieci Web?**

Zapory aplikacji sieci Web jest monitorowany za pośrednictwem rejestrowania diagnostycznego, więcej informacji na temat rejestrowania diagnostycznego można znaleźć w folderze [rejestrowania diagnostyki i metryki bramy aplikacji](application-gateway-diagnostics.md)

**Q. Tryb wykrywania blokowania ruchu?**

Nie, Tryb wykrywania rejestruje tylko ruch, który jest wyzwalana reguła zapory aplikacji sieci Web.

**Q. Jak dostosować reguły zapory aplikacji sieci Web?**

Tak, można dostosowywać, aby uzyskać więcej informacji na jak toocustomize ich odwiedź są reguły zapory aplikacji sieci Web [grup reguł zapory aplikacji sieci Web dostosować i reguł](application-gateway-customize-waf-rules-portal.md)

**Q. Jakie reguły są obecnie dostępne?**

Zapory aplikacji sieci Web obsługuje obecnie CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) i [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), które zapewniają planu bazowego zabezpieczeń przed większość hello 10 pierwszych luk w zabezpieczeniach przez hello Otwórz sieci Web aplikacji zabezpieczeń projektu (OWASP) znaleźć tutaj [OWASP pierwszych 10 luk w zabezpieczeniach](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)

* Ochrona przed atakami polegającymi na iniekcji SQL

* Ochrona przed atakami z użyciem skryptów wykorzystywanych w obrębie wielu witryn

* Częste ataki w ramach sieci Web polegające na iniekcji poleceń, przemycaniu żądań HTTP, rozdzielaniu odpowiedzi HTTP i zdalnym dołączaniu plików

* Ochrona przed naruszeniami protokołu HTTP

* Ochrona przed nieprawidłowościami protokołu HTTP, takimi jak brakujące powiązania agenta i użytkownika hosta oraz akceptowanie nagłówków

* Zapobieganie atakom z użyciem robotów, przeszukiwarek i skanerów

* Wykrycie typowych błędów konfiguracji aplikacji (czyli Apache usług IIS, itp.)

**Q. Czy zapory aplikacji sieci Web obsługuje również zapobiegania DDoS?**

Nie, zapory aplikacji sieci Web nie ma DDoS zapobiegania.

## <a name="diagnostics-and-logging"></a>Rejestrowanie i Diagnostyka

**Q. Jakie rodzaje dzienniki są dostępne z bramy aplikacji?**

Istnieją trzy dzienniki dostępne dla bramy aplikacji. Aby uzyskać więcej informacji na te dzienniki i inne funkcje diagnostyczne, odwiedź stronę [zaplecza kondycji, dzienników diagnostyki i metryki bramy aplikacji](application-gateway-diagnostics.md).

- **ApplicationGatewayAccessLog** — dziennik dostępu hello zawiera każdego żądania przesłane toohello frontonu bramy aplikacji. dane Hello obejmują wywołującego hello IP, adres URL żądanego, czas oczekiwania na odpowiedź, i wylogowywanie zwracają kod, bajtów. Dziennik dostępu są gromadzone co 300 sekund. Ten dziennik zawiera jeden rekord dla każdego wystąpienia bramy aplikacji.
- **ApplicationGatewayPerformanceLog** — dziennik wydajności hello przechwytuje informacje o wydajności dla poszczególnych wystąpień całkowita liczba żądań podawana, w tym przepływność w bajtach, całkowita liczba żądań obsłużonych, liczba nieudanych żądań, dobrej kondycji i złej kondycji Liczba wystąpień zaplecza.
- **ApplicationGatewayFirewallLog** — dziennik zapory hello zawiera żądań, które są rejestrowane za pomocą wykrywania i zapobiegania tryb bramę aplikacji, który jest skonfigurowany z zapory aplikacji sieci web.

**Q. Jak sprawdzić, czy Moje elementy członkowskie puli zaplecza są w dobrej kondycji?**

Można użyć polecenia cmdlet programu PowerShell hello `Get-AzureRmApplicationGatewayBackendHealth` lub Sprawdź kondycję za pośrednictwem portalu hello odwiedzając [diagnostyki bramy aplikacji](application-gateway-diagnostics.md)

**Q. Co to jest hello zasady przechowywania dzienników diagnostycznych hello?**

Konto magazynu klientów toohello przepływu dzienniki diagnostyczne i klientów można ustawić zasad przechowywania hello na podstawie swoich preferencji. Dzienniki diagnostyczne mogą być również wysyłane tooan Centrum zdarzeń lub analizy dzienników. Odwiedź stronę [diagnostyki bramy aplikacji](application-gateway-diagnostics.md) więcej szczegółów.

**Q. Jak uzyskać dzienniki inspekcji dla bramy aplikacji?**

Dzienniki inspekcji są dostępne dla bramy aplikacji. W portalu powitania kliknij **dziennik aktywności** w bloku menu hello dziennika inspekcji hello tooaccess Application Gateway. 

**Q. Można ustawić alerty z bramy aplikacji?**

Tak, bramy aplikacji obsługi alertów, alerty są konfigurowane poza metryki.  Brama aplikacji w aktualnie ma metrykę "przepływności", który może być skonfigurowany tooalert. toolearn więcej informacji na temat alertów, odwiedź stronę [otrzymywać powiadomienia o alertach](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

**Q. Kondycja wewnętrznej bazy danych zwraca nieznany stan, w poznaniu przyczyny tego stanu?**

Najczęstszą przyczyną Hello jest toohello dostępu do wewnętrznej bazy danych jest blokowana przez NSG lub niestandardowe DNS. Odwiedź stronę [zaplecza kondycji, rejestrowanie danych diagnostycznych i metryki bramy aplikacji](application-gateway-diagnostics.md) toolearn więcej.

## <a name="next-steps"></a>Następne kroki

można znaleźć więcej informacji na temat bramy aplikacji toolearn [tooApplication wprowadzenie bramy](application-gateway-introduction.md).
