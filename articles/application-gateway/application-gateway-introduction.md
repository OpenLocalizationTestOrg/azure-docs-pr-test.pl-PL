---
title: tooAzure aaaIntroduction bramy aplikacji | Dokumentacja firmy Microsoft
description: "Ta strona zawiera omówienie usługi bramy aplikacji hello do równoważenia obciążenia warstwy 7 tym rozmiary bramy, koligacji sesji opartego na pliku cookie, równoważenia obciążenia HTTP i odciążanie protokołu SSL."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: b37a2473-4f0e-496b-95e7-c0594e96f83e
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: c40c9dba64ab03d9f6f81b3cb8f26c6562ac26c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-application-gateway"></a>Omówienie usługi Application Gateway

Usługa Microsoft Azure Application Gateway to dedykowane urządzenie wirtualne udostępniające kontroler dostarczania aplikacji (ADC, Application Delivery Controller) jako usługę. Oferuje różnorodne możliwości równoważenia obciążenia warstwy 7 dla Twojej aplikacji. Pozwala ona klientom wydajność kolektywu serwerów sieci web toooptimize dzięki przeniesieniu Procesora znacznym SSL zakończenia toohello bramy aplikacji. Udostępnia również inne funkcje routingu warstwy 7 tym działanie okrężne dystrybucję ruchu przychodzącego, koligacji na podstawie plików cookie sesji, routingu adresów URL na podstawie ścieżki i toohost możliwości hello wiele witryn sieci Web za pojedyncza brama aplikacji. Zapora aplikacji sieci web (WAF) jest również udostępniany w ramach bramy aplikacji hello SKU zapory aplikacji sieci Web. Zapewnia on ochronę aplikacje tooweb wspólnej luk w zabezpieczeniach sieci web i luki w zabezpieczeniach. Usługę Application Gateway można skonfigurować jako bramę umożliwiającą dostęp do Internetu, bramę tylko wewnętrzną lub jako kombinację obu tych opcji. 

![scenariusz](./media/application-gateway-introduction/scenario.png)

## <a name="features"></a>Funkcje

Brama aplikacji w obecnie udostępnia hello następujące możliwości:


* **[Zapora aplikacji sieci Web](application-gateway-webapplicationfirewall-overview.md)**  -hello zapory aplikacji sieci web (WAF) brama aplikacji w usłudze Azure chroni aplikacje sieci web przed wspólnej ataków opartych na sieci web takich jak iniekcja kodu SQL, ataki skryptów między witrynami i hijacks sesji.
* **Równoważenie obciążenia HTTP** — usługa Application Gateway zapewnia okrężne równoważenie obciążenia. Równoważenie obciążenia jest wykonywane na warstwie 7 i jest używane tylko na potrzeby ruchu HTTP(S).
* **Koligacji na podstawie plików cookie sesji** -funkcji koligacji na podstawie plików cookie sesji hello jest przydatne, gdy chcesz tookeep sesji użytkownika na powitania tego samego zaplecza. Za pomocą zarządzanych przez bramę plików cookie, hello bramy aplikacji jest możliwe toodirect kolejnych ruch toohello sesji użytkownika tego samego zaplecza do przetwarzania. Ta funkcja jest ważne w przypadkach, gdy stan sesji jest zapisywany lokalnie na serwerze zaplecza hello sesji użytkownika.
* **[Bezpieczne odciążania Sockets Layer (SSL)](application-gateway-ssl-arm.md)**  — ta funkcja przyjmuje hello kosztowne zadania odszyfrowywania ruchu HTTPS, wyłącz serwerów sieci web. Przez hello zakończenia połączenia SSL na powitania bramy aplikacji i przekazywania serwer toohello żądania hello bez szyfrowania serwer sieci web hello jest unburdened przez odszyfrowywania.  Brama aplikacji w ponownie szyfruje hello odpowiedzi przed wysłaniem wstecz toohello klienta. Ta funkcja jest przydatne w scenariuszach, w którym znajduje się hello zaplecza w hello takie same zabezpieczonej sieci wirtualnej jako hello brama aplikacji w usłudze Azure.
* **[Zakończenie tooEnd SSL](application-gateway-backend-ssl.md)**  -Application Gateway obsługuje zakończenia tooend szyfrowania ruchu. Brama aplikacji w następującym cechom zakończenie połączenia SSL hello na powitania bramy aplikacji. Witaj bramy następnie stosuje hello reguły routingu ruchu toohello ponownie szyfruje pakietów hello i przekazuje hello pakietów toohello odpowiedniej wewnętrznej bazy danych na podstawie reguł routingu hello zdefiniowane. Odpowiedzi z serwera sieci web hello przechodzi przez hello tego samego procesu wstecz toohello użytkownika końcowego.
* **[Adres URL routingu opartego na protokole zawartości](application-gateway-url-route-overview.md)**  — ta funkcja zapewnia możliwość hello toouse różnych serwerów zaplecza innego ruchu sieciowego. Ruchu dla folderu na serwerze sieci web hello lub CDN może być kierowany tooa różnych zaplecza. Ta funkcja zmniejsza niepotrzebne obciążenie zapleczy, które nie obsługują określonej zawartości.
* **[Obejmujący wiele lokacji routingu](application-gateway-multi-site-overview.md)**  -bramy aplikacji umożliwia tooconsolidate się too20 witryn sieci Web w bramie pojedynczej aplikacji.
* **[Obsługa protokołu Websocket](application-gateway-websocket.md)**  -inna funkcja wspaniałych aplikacji bramy jest hello macierzystą obsługę protokołu Websocket.
* **[Monitorowanie kondycji](application-gateway-probe-overview.md)**  -bramy aplikacji umożliwia domyślne monitorowanie kondycji zasobów w wewnętrznej bazie danych i niestandardowych sondy toomonitor dla bardziej konkretnych scenariuszy.
* **[Zasady protokołu SSL i szyfrów](application-gateway-ssl-policy-overview.md)**  — ta funkcja umożliwia określenie hello wersji protokołu SSL hello toolimit i szyfrów hello mechanizmy, które są obsługiwane i hello kolejności, w jakiej są przetwarzane.
* **[Żądanie przekierowania](application-gateway-redirect-overview.md)**  — ta funkcja zapewnia odbiornik HTTPS tooan hello możliwości tooredirect HTTP żądania.
* **[Obsługa wielodostępnego zaplecza](application-gateway-web-app-overview.md)** — usługa Application Gateway obsługuje konfigurowanie wielodostępnych usług zaplecza, takich jak usługa Azure Web Apps i API Gateway, jako elementów członkowskich puli zaplecza. 
* **[Zaawansowana diagnostyka](application-gateway-diagnostics.md)** — aplikacja Application Gateway oferuje kompletne dzienniki dostępu i diagnostyki. Dzienniki zapory są dostępne dla zasobów usługi Application Gateway z włączoną zaporą aplikacji sieci Web.

## <a name="benefits"></a>Korzyści

Usługa Application Gateway ma następujące zastosowania:

* Aplikacje, które wymagają żądań z hello tego samego użytkownika/klienta sesji tooreach hello tej samej maszyny wirtualnej zaplecza. Przykładami takich aplikacji są aplikacje koszyka zakupów i serwery poczty sieci Web.
* Eliminowanie nakładu pracy związanego z kończeniem żądań SSL dla farm serwerów sieci Web.
* Aplikacje, takie jak sieci dostarczania zawartości, która wymaga wielu żądań HTTP na powitania tego samego toobe połączenia protokołu TCP długotrwałe trasę lub serwerami zaplecza toodifferent równoważeniem obciążenia.
* Aplikacje, które obsługują ruch w ramach protokołu Websocket.
* Ochrona aplikacji sieci Web przed typowymi atakami internetowymi, takimi jak iniekcja SQL, ataki z użyciem skryptów wykorzystywanych w obrębie wielu witryn i przejęcia sesji.
* Logiczna dystrybucja ruchu na podstawie różnych kryteriów routingu, takich jak ścieżka adresu URL lub nagłówki domeny.

Usługa Application Gateway jest w pełni zarządzana przez platformę Azure, skalowalna i wysoko dostępna. Zapewnia ona bogaty zestaw funkcji diagnostyki i rejestrowania, aby uprościć zarządzanie. Utworzenie bramy aplikacji powoduje powiązanie punktu końcowego (publicznego adresu VIP lub wewnętrznego adresu IP modułu równoważenia obciążenia) i używanie go na potrzeby ruchu sieciowego danych przychodzących. Tego adresu VIP lub ILB IP są udostępniane przez moduł równoważenia obciążenia Azure na poziomie transportu hello (TCP/UDP) i cały ruch przychodzący ruch sieciowy jest brama aplikacji w toohello równoważeniem obciążenia wystąpień procesów roboczych. Witaj bramy aplikacji, a następnie trasy hello ruchu HTTP/HTTPS na podstawie konfiguracji czy jest ono maszynę wirtualną w chmurze usługi, wewnętrzny lub zewnętrzny adres IP.

Brama aplikacji w Równoważenie obciążenia jak usługi zarządzane Azure pozwala na powitania inicjowania obsługi usługi równoważenia obciążenia warstwy 7 za usługą równoważenia obciążenia Azure oprogramowania hello. Menedżera ruchu może być używane toocomplete hello scenariusz w powitania po obrazu, w którym Menedżera ruchu zapewnia przekierowania i dostępności ruchu toomultiple zasobów brama aplikacji w różnych regionach, a dostarcza bramy aplikacji krzyżowe równoważenia obciążenia warstwy 7 regionu. Przykładem tego scenariusza można znaleźć w folderze: [równoważenia usług w hello chmury Azure obciążenia Using](../traffic-manager/traffic-manager-load-balancing-azure.md)

![scenariusz dla usług traffic manager i application gateway](./media/application-gateway-introduction/tm-lb-ag-scenario.png)

[!INCLUDE [load-balancer-compare-tm-ag-lb-include.md](../../includes/load-balancer-compare-tm-ag-lb-include.md)]

## <a name="gateway-sizes-and-instances"></a>Wystąpienia i rozmiary usługi Application Gateway

Usługa Application Gateway jest obecnie oferowana w trzech rozmiarach: małym (**Small**), średnim (**Medium**) i dużym (**Large**). Rozmiary małych wystąpień są przeznaczone na potrzeby programowania i scenariuszy testowania.

Utworzeniem too50 bram aplikacji dla subskrypcji i każdej bramy aplikacji może zawierać maksymalnie too10 wystąpień. Każda brama aplikacji może składać się z 20 odbiorników HTTP. Pełna lista limitów usługi Application Gateway znajduje się na stronie [ograniczeń usługi Application Gateway](../azure-subscription-service-limits.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#application-gateway-limits).

Witaj w poniższej tabeli przedstawia przepływności średniej wydajności dla każdego wystąpienia bramy aplikacji z włączone odciążanie protokołu SSL:

| Odpowiedź strony zaplecza | Small | Medium | Large |
| --- | --- | --- | --- |
| 6000 |7,5 Mb/s |13 Mb/s |50 Mb/s |
| 100 000 |35 Mb/s |100 Mb/s |200 Mb/s |

> [!NOTE]
> Są to przybliżone wartości przepływności bramy aplikacji. Przepływność rzeczywiste hello zależy od środowiska szczegółowe informacje, takie jak rozmiar strony, lokalizacja wystąpień zaplecza i tooserve czas przetwarzania strony. Aby uzyskać dokładne wartości wydajności, należy przeprowadzić własne testy. Te wartości są podane tylko jako wskazówki na potrzeby planowania pojemności.

## <a name="health-monitoring"></a>Monitorowanie kondycji

Brama aplikacji Azure automatycznie monitoruje kondycję hello hello wystąpień zaplecza za pośrednictwem sond kondycji podstawowego lub niestandardowego. Za pomocą sondy kondycji, zapewnia to, że tylko w dobrej kondycji hostów odpowiadać tootraffic. Aby uzyskać więcej informacji, zobacz [Application Gateway health monitoring overview](application-gateway-probe-overview.md) (Monitorowanie kondycji usługi Application Gateway — omówienie).

## <a name="configuring-and-managing"></a>Konfigurowanie i zarządzanie

Punktem końcowym bramy aplikacji, jeśli został skonfigurowany, może być publiczny adres IP, prywatny adres IP lub obydwa te adresy. Usługa Application Gateway jest konfigurowana wewnątrz sieci wirtualnej we własnej podsieci. podsieci Hello utworzone lub używana przez bramę aplikacji nie może zawierać innych typów zasobów, hello tylko zasoby, które są dozwolone w podsieci hello są inne bramy aplikacji. toosecure zasobami zaplecza hello serwerów wewnętrznej bazy danych może być zawarty w innej podsieci w hello tej samej sieci wirtualnej co brama aplikacji hello. Tej podsieci, który nie jest wymagane dla aplikacji zaplecza hello. Tak długo, jak bramy aplikacji hello można uzyskać dostęp do adresu ip hello, bramy aplikacji jest możliwe tooprovide możliwości ADC hello serwerów wewnętrznej bazy danych. 

Możesz utworzyć bramę aplikacji i zarządzać nią, używając interfejsów API REST, poleceń cmdlet programu PowerShell, interfejsu wiersza polecenia Azure lub witryny [Azure Portal](https://portal.azure.com/). Dodatkowe pytania dotyczące aplikacji bramy można znaleźć [— często zadawane pytania dla bramy aplikacji](application-gateway-faq.md) tooview listę typowe często zadawane pytania.

## <a name="pricing"></a>Cennik

Ceny zależą od opłaty godzinnej za wystąpienie bramy i opłaty za przetwarzanie danych. Na godzinę bramy ceny hello SKU zapory aplikacji sieci Web różni się od wersji Standard opłat. Informacje o cenach można znaleźć na stronie [szczegółowego cennika usługi Application Gateway](https://azure.microsoft.com/pricing/details/application-gateway/). Przetwarzanie danych, pozostaną opłat hello takie same.

## <a name="faq"></a>Często zadawane pytania

Aby zapoznać się z często zadawanymi pytaniami dotyczącymi usługi Application Gateway, zobacz [Application Gateway FAQ](application-gateway-faq.md) (Często zadawane pytania dotyczące usługi Application Gateway).

## <a name="next-steps"></a>Następne kroki

Po zapoznać się z usługą bramy aplikacji, możesz [Utwórz bramę aplikacji](application-gateway-create-gateway-portal.md) lub [Utwórz bramę aplikacji odciążanie protokołu SSL](application-gateway-ssl-arm.md) tooload saldo połączeń HTTPS.

toolearn jak toocreate bramę aplikacji przy użyciu adresu URL routingu opartego na protokole zawartości, przejdź zbyt[Utwórz bramę aplikacji przy użyciu routingu opartego na adres URL](application-gateway-create-url-route-arm-ps.md) Aby uzyskać więcej informacji.

toolearn o pewnych hello innego klucza sieci możliwości platformy Azure, zobacz [sieci Azure](../networking/networking-overview.md).
