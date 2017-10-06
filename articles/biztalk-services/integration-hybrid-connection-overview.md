---
title: "Omówienie połączeń aaaHybrid | Dokumentacja firmy Microsoft"
description: "Informacje na temat połączeń hybrydowych, zabezpieczeń, portów TCP i obsługiwanych konfiguracji. MABS, WABS."
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: erikre
editor: 
ms.assetid: 216e4927-6863-46e7-aa7c-77fec575c8a6
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/18/2016
ms.author: ccompy
ms.openlocfilehash: f092c6019aae761e1e73f13d1af8446a896515c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-connections-overview"></a>Połączenia hybrydowe — omówienie

> [!IMPORTANT]
> Połączenia hybrydowe BizTalk zostały wycofane i zastąpione połączeniami hybrydowymi usługi App Service. Aby uzyskać więcej informacji, łącznie ze sposobem toomanage istniejących połączeń hybrydowych BizTalk zobacz [połączeń hybrydowych usługi aplikacji Azure](../app-service/app-service-hybrid-connections.md).

Wprowadzenie tooHybrid połączeń, wyświetla hello obsługiwane konfiguracje oraz list hello wymaganych portów TCP.

## <a name="what-is-a-hybrid-connection"></a>Czym jest połączenie hybrydowe
Połączenia hybrydowe są funkcją usługi Azure BizTalk Services. Połączenia hybrydowe Podaj funkcję łatwy i wygodny sposób tooconnect hello aplikacji Web Apps w usłudze Azure App Service (dawniej witryn sieci Web) i hello funkcji Mobile Apps w usłudze Azure App Service (dawniej Mobile Services) tooon lokalnych zasobach za zaporą.

![Połączenia hybrydowe][HCImage]

Korzyści wynikające z użycia połączeń hybrydowych:

* Funkcje Web Apps i Mobile Apps mogą w bezpieczny sposób uzyskać dostęp do istniejących lokalnych danych i usług.
* Wiele aplikacji sieci Web lub aplikacji mobilnej można udostępniać połączenia hybrydowego tooaccess zasób lokalną.
* Minimalny porty TCP są wymagane tooaccess sieci.
* Aplikacje przy użyciu połączeń hybrydowych dostęp tylko zasobu lokalnego określonych hello, opublikowaną za pośrednictwem hello połączenia hybrydowego.
* Można połączyć zasób lokalną tooany, który korzysta z portu statycznego TCP, takich jak SQL Server, MySQL, interfejsów API sieci Web HTTP i większość niestandardowych usług sieci Web.
  
  > [!NOTE]
  > Usługi oparte na protokole TCP, które używają portów dynamicznych (na przykład FTP w trybie pasywnym lub pasywnym trybie rozszerzonym) nie są obecnie obsługiwane. Protokół LDAP również nie jest obsługiwany. Protokół LDAP używa statycznego portu TCP, ale może również używać protokołu UDP. W związku z tym nie jest obsługiwany.
  > 
  > 
* Można ich używać ze wszystkimi środowiskami obsługiwanymi przez funkcję Web Apps (.NET, PHP, Java, Python, Node.js) oraz funkcję Mobile Apps (Node.js, .NET).
* Aplikacje sieci Web i aplikacje mobilne można uzyskiwać dostęp do zasobów lokalnych w dokładnie hello sam sposób jak gdyby hello sieci Web lub aplikacji mobilnej znajduje się w sieci lokalnej. Na przykład Witaj same parametry połączenia używane w lokalnym można również na platformie Azure.

Połączenia hybrydowe zawierają również Administratorzy przedsiębiorstwa z kontrolą i wgląd w zasoby firmy hello dostęp do aplikacji hybrydowych, w tym:

* Używanie zasad grupy, Administratorzy mogą połączeń hybrydowych w sieci hello i też określić zasoby, które mogą być udostępniane przez hybrydowych aplikacji.
* Dzienniki zdarzeń i inspekcji w sieci firmowej hello zapewniają wgląd w zasoby hello dostęp do połączeń hybrydowych było możliwe.

## <a name="example-scenarios"></a>Przykładowe scenariusze
Połączenia hybrydowe obsługuje hello następujących kombinacji framework i aplikacji:

* .NET framework dostępu tooSQL serwera
* .NET framework dostępu tooHTTP/HTTPS usług z WebClient
* TooSQL PHP dostępu do serwera, MySQL
* Program Java dostępu tooSQL Server, MySQL i Oracle
* Usługi tooHTTP/HTTPS dostęp Java

Za pomocą połączeń hybrydowych tooaccess lokalnego programu SQL Server, należy uwzględnić następujące hello:

* SQL Express o nazwie wystąpienia muszą być statyczne portów skonfigurowanych toouse. Domyślnie nazwane wystąpienia programu SQL Express używają portów dynamicznych.
* Domyślne wystąpienia programu SQL Express używają portu statycznego, ale musi być włączony protokół TCP. Domyślnie protokół TCP nie jest włączony.
* Witaj w przypadku korzystania z klastrowania lub grup dostępności, `MultiSubnetFailover=true` tryb nie jest obecnie obsługiwany.
* Witaj `ApplicationIntent=ReadOnly` nie jest obecnie obsługiwany.
* Uwierzytelnianie SQL może być wymagany jako metoda autoryzacji na trasie hello obsługiwane przez hello aplikacji Azure i hello lokalnego programu SQL server.

## <a name="security-and-ports"></a>Zabezpieczenie i porty
Połączeń hybrydowych było możliwe, użyj połączenia hello toosecure autoryzacji dostępu sygnatury dostępu Współdzielonego z hello Azure aplikacji i hello lokalnego połączenia hybrydowego toohello Menedżera połączeń hybrydowych. Oddzielne połączenie klucze są tworzone dla aplikacji hello i hello lokalnego Menedżera połączeń hybrydowych. Te klucze połączenia można niezależnie przywracać i odwoływać.

Połączenia hybrydowe zapewnić bezproblemową i bezpieczną dystrybucję aplikacji toohello klucze hello i hello lokalnego Menedżera połączeń hybrydowych.

Zobacz temat [Create and Manage Hybrid Connections](integration-hybrid-connection-create-manage.md) (Tworzenie połączeń hybrydowych i zarządzanie nimi).

*Zezwolenie aplikacji jest oddzielony od hello połączenia hybrydowego*. Można użyć dowolnej metody autoryzacji. Metoda autoryzacji Hello zależy od metody end-to-end autoryzacji hello obsługiwane przez hello chmury Azure i składniki lokalne powitania. Na przykład aplikacja Azure uzyskuje dostęp do lokalnego programu SQL Server. W tym scenariuszu autoryzacji SQL może być hello autoryzacji metodę, która jest obsługiwana na całej trasie.

#### <a name="tcp-ports"></a>Porty TCP
Połączenia hybrydowe wymagają tylko łączności wychodzącej za pośrednictwem protokołu TCP lub HTTP z sieci prywatnej. Nie należy tooopen wszystkie porty zapory lub zmień Twojej sieci obwodowej konfiguracji tooallow żadnych przychodzących połączeń do sieci.

następujące porty TCP Hello są używane przez połączeń hybrydowych było możliwe:

| Port | Do czego służy |
| --- | --- |
| 9350 – 9354 |Te porty służą do transmisji danych. Menedżer przekaźnika usługi Service Bus Hello sondy port 9350 toodetermine, jeśli połączenie TCP jest dostępna. Jeśli jest dostępna, menedżer zakłada, że port 9352 jest również dostępny. Ruch w sieci jest przekazywany za pośrednictwem portu 9352. <br/><br/>Zezwalaj na połączenia wychodzące toothese portów. |
| 5671 |W przypadku portu 9352 dla ruchu danych portu 5671 jest używana jako hello kanału kontroli. <br/><br/>Zezwalaj na połączenia wychodzące toothis portu. |
| 80, 443 |Te porty są używane dla niektórych tooAzure żądania danych. Ponadto, jeśli nie są użyteczne, porty 9352 i 5671 *następnie* porty 80 i 443 są porty rezerwowy hello używany do transmisji danych i kanału kontroli hello.<br/><br/>Zezwalaj na połączenia wychodzące toothese portów. <br/><br/>**Uwaga** nie jest zalecane toouse je jako hello rezerwowy porty zamiast hello innych portów TCP. Hello HTTP/WebSocket jest używany jako protokołu hello zamiast natywnego protokołu TCP dla danych kanałów. Może to spowodować obniżenie wydajności. |

## <a name="next-steps"></a>Następne kroki
[Tworzenie połączeń hybrydowych i zarządzanie nimi](integration-hybrid-connection-create-manage.md)<br/>
[Łączenie aplikacji sieci Web Azure tooan zasób lokalną](../app-service-web/web-sites-hybrid-connection-get-started.md)<br/>
[Połącz tooon lokalnego programu SQL Server z aplikacji sieci web platformy Azure](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)<br/>

## <a name="see-also"></a>Zobacz też
[REST API for Managing BizTalk Services on Microsoft Azure](http://msdn.microsoft.com/library/azure/dn232347.aspx) (Interfejs API REST do zarządzania usługą BizTalk Services na platformie Microsoft Azure) 
[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) (BizTalk Services: tabela wersji)<br/>
[Tworzenie usługi BizTalk przy użyciu witryny Azure Portal](biztalk-provision-services.md)<br/>
[BizTalk Services: Dashboard, Monitor and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md) (Usługa BizTalk Services: karty Pulpit nawigacyjny, Monitor i Skalowanie)<br/>

[HCImage]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionImage.png
[HybridConnectionTab]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionManageConn.png
