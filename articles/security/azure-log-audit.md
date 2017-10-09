---
title: aaaAzure rejestrowanie i inspekcja | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat korzystania z rejestrowania danych toogain szczegółowych informacji o aplikacji."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: d0e817b071962ad9bef6250267092b5f9282bc7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-logging-and-auditing"></a>Rejestrowanie platformy Azure i inspekcji
## <a name="introduction"></a>Wprowadzenie
### <a name="overview"></a>Omówienie
tooassist aktualnych i potencjalnych klientów platformy Azure zrozumienia i używania hello różnych funkcjach zabezpieczeń dostępnych w i otaczającego hello platformy Azure, firma Microsoft wprowadziła serii oficjalne dokumenty, omówienie zabezpieczeń, najlepsze rozwiązania i listy kontrolne. Tematy Hello zakresu pod względem szerokości i głębokość i są okresowo aktualizowane. Ten dokument jest częścią tej serii, zgodnie z opisem w powitania po sekcji abstrakcyjny.
### <a name="azure-platform"></a>Platformy Azure
Azure to platforma usługi chmury Otwórz i elastyczne, która obsługuje hello wybór najszerszych systemów operacyjnych, programowania języków, struktury, narzędzia, baz danych i urządzeń.

Można na przykład:
-   Uruchom kontenery Linux z integracją rozwiązania Docker.

-   Tworzenie aplikacji za pomocą języka JavaScript, Python, .NET, PHP, Java i Node.js

-   Kompilacja zapleczy dla systemu iOS, Android i Windows urządzeń.

Usługi w chmurze publicznej Azure obsługuje hello już polegać na tej samej technologii miliony deweloperów i specjalistów IT i zaufania.

Podczas tworzenia lub migracji zasobów informatycznych do dostawcy usług w chmurze, są zależne tooprotect możliwości organizacji w aplikacji i danych za pomocą hello kontroli usług i hello zapewniają bezpieczeństwo hello toomanage zasobów opartych na chmurze.

Zaprojektowano infrastruktury platformy Azure z tooapplications zakładzie hello jednocześnie hostingu miliony klientów i zapewnia foundation godne zaufania, na którym firmy mogą ich potrzeb zabezpieczeń. Ponadto Azure zapewnia szereg zabezpieczeń można skonfigurować opcje i hello toocontrol możliwości ich, dzięki czemu można dostosować toomeet hello unikatowe wymagania dotyczące zabezpieczeń wdrożeń. Ten dokument zostanie pomaga spełnić te wymagania.

### <a name="abstract"></a>Abstrakcyjny
Inspekcja i rejestrowanie zdarzeń związanych z zabezpieczeniami i powiązanych alertów, to ważne składniki danych skutecznej strategii ochrony. Dzienniki zabezpieczeń i raporty umożliwiają elektronicznych rekordu podejrzanych działań i wykrywać wzorce wskazujące i nieudane próby zewnętrznych penetracji sieci hello, a także atakami wewnętrznymi pomocy. Możesz użyć inspekcji toomonitor aktywności użytkownika, zgodność z przepisami dokumentu, wykonywać analizy śledczej i inne. Alerty udostępniają natychmiastowego wysłania powiadomienia w przypadku wystąpienia zdarzeń zabezpieczeń.

Usług Microsoft Azure i produktów zapewniają inspekcji zabezpieczeń można konfigurować i rejestrowanie toohelp opcje zidentyfikować luki w Twojej zasad i mechanizmów zabezpieczeń i rozwiązać te luki toohelp zapobiec naruszeń. Oferty usług firmy Microsoft, niektóre (i w niektórych przypadkach wszystkie) z hello następujące opcje: scentralizowane monitorowanie, rejestrowanie i systemy tooprovide ciągłego widoczność analizy; alerty odpowiednim; i toohelp raporty zarządzania hello dużej ilości informacji generowany przez urządzenia i usługi.

Dane dziennika Microsoft Azure może być eksportowany tooSecurity systemów zdarzenia i zdarzeń zarządzania (SIEM) do analizy i integruje się z rozwiązaniami inspekcji innych firm.

Ten dokument zawiera wprowadzenie do generowania, zbierania i analizowania dzienniki zabezpieczeń z usługi hostowanej na platformie Azure, a może pomóc wgląd zabezpieczeń Azure wdrożeń. zakres Hello ten dokument jest ograniczona tooapplications i usług wbudowanych i wdrożonych na platformie Azure.

> [!Note]
> Zastosowanie niektórych zaleceń zamieszczonych w niniejszym dokumencie może spowodować danych, sieci i użycia zasobów obliczeniowych i zwiększyć koszty licencji lub subskrypcji.

## <a name="types-of-logs-in-azure"></a>Typy dzienników na platformie Azure
Aplikacje w chmurze są złożonych z wielu części ruchu. Dzienniki Podaj tooensure danych, która aplikacja pozostaje w górę i uruchomiony w dobrej kondycji. Pomaga również należy toostave wyłączone potencjalne problemy lub Rozwiązywanie problemów z przeszłości te. Ponadto można użyć rejestrowania danych toogain szczegółowych informacji o aplikacji. Wiedzy może pomóc tooimprove wydajność aplikacji lub utrzymania lub automatyzować czynności, które w przeciwnym razie wymagają ręcznej interwencji.

Azure tworzy szczegółowe rejestrowanie dla każdej usługi Azure. Te dzienniki są podzielone według rodzaju główne:
-   **Dzienniki sterowania i zarządzania nimi** zapewniają wgląd w hello operacje tworzenia Menedżera zasobów Azure, UPDATE i DELETE. [Azure Dzienniki aktywności](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) przykładem tego typu dziennika.

-   **Dane płaszczyzny dzienniki** zapewniają wgląd w zdarzenia hello zgłoszone jako część hello użycie zasobów platformy Azure. Przykładem tego typu dziennika są hello zdarzeń systemu Windows systemu zabezpieczeń, i dzienniki aplikacji na maszynie wirtualnej i hello [dzienników diagnostycznych](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) skonfigurowane za pośrednictwem Monitora Azure


-   **Przetworzonych zdarzeń** informacje o analizowanych zdarzenia/alerty, które zostały przetworzone w Twoim imieniu. Przykładem tego typu są [alerty Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) gdzie [Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) jest przetwarzane i analizowane subskrypcji i zawiera alerty zabezpieczeń zwięzły

Witaj poniższej tabeli najważniejszych typu listy dzienników dostępnych w systemie Azure.

| Kategoria dziennika | Typ dziennika | Użycia | Integracja |
| ------------ | -------- | ------ | ----------- |
|[Dzienniki aktywności](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)|Zdarzenia płaszczyzny kontroli zasobów usługi Azure Resource Manager| Zapewniają wgląd w operacji hello, wykonywane na zasobów w ramach subskrypcji.|   Interfejs API REST & [Azure monitora](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)|
|[Dzienniki diagnostyczne platformy Azure](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)|często dane dotyczące operacji hello zasobów usługi Azure Resource Manager w subskrypcji| Zapewniają wgląd w działania, zasobu wykonanie samego| Azure Monitor [strumienia](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)|
|[Raportowanie usługi AAD](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-azure-portal)|Dzienników i raportów|Działania logowania użytkowników & informacje o systemie działania dotyczące użytkowników i grupy zarządzania|[Interfejs API programu Graph](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-graph-api-quickstart)|
|[Maszyny wirtualne i usługi w chmurze](https://docs.microsoft.com/en-us/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)|Dziennik zdarzeń systemu Windows i systemu Linux|  Przechwytuje dane systemu i rejestrowanie danych na maszynach wirtualnych hello i przesyła dane do wybranego konta magazynu.| Przy użyciu systemu Windows [WAD](https://docs.microsoft.com/en-us/azure/azure-diagnostics) (magazynu diagnostyki Windows Azure) i Linux w Monitorze systemu Azure|
|[Analityka magazynu](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/storage-analytics)|Rejestrowanie magazynu i udostępnia metryki danych dla konta magazynu|Zapewnia wgląd w żądań śledzenia analizować trendy użycia i diagnozowanie problemów z konta magazynu.|  Interfejs API REST lub hello [biblioteki klienta](https://msdn.microsoft.com/en-us/library/azure/mt347887.aspx)|
|[Dzienniki przepływu NSG (sieciowej grupy zabezpieczeń)](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-nsg-flow-logging-overview)|JSON format i zawiera przepływy ruchu wychodzącego i przychodzącego na podstawie reguł na|Wyświetl informacje o przychodzące i wychodzące ruchu IP za pośrednictwem grupy zabezpieczeń sieci|[Obserwatora sieciowego](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview)|
|[Szczegółowe informacje o aplikacji](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-overview)|Dzienniki, wyjątków i diagnostyki niestandardowej|  Usługa zarządzania wydajności aplikacji przeznaczonych dla deweloperów sieci web na wielu platformach.| Interfejs API REST, [Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-azure-and-power-bi/)|
|Przetwarzaj dane / Alert zabezpieczeń| Centrum zabezpieczeń Azure Alert, OMS Alert| Informacje o zabezpieczeniach i alerty.|   Interfejsy API REST, JSON|

### <a name="activity-log"></a>Dziennik aktywności
Witaj [dziennika aktywności platformy Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs), zapewnia wgląd w operacji hello, wykonywane na zasobów w ramach subskrypcji. Witaj dziennik aktywności była wcześniej znana jako "Dzienników inspekcji" lub "Operacyjne dzienniki", ponieważ zgłasza [zdarzeń formantu płaszczyzny](https://driftboatdave.com/2016/10/13/azure-auditing-options-for-your-custom-reporting-needs/) dla Twojej subskrypcji. Przy użyciu hello dziennik aktywności, można określić hello ", co, kto i kiedy" dla żadnego zapisu (PUT, POST, DELETE) wykonywanych na powitania zasobów w ramach subskrypcji. Można także zrozumieć hello stanu operacji hello i inne odpowiednie właściwości. Hello dziennika aktywności obejmuje operacje odczytu (GET).

PUT, POST, DELETE odnosi się tutaj operacje zapisu hello tooall, które zawiera dziennik aktywności hello zasobów. Na przykład można użyć toofind Dzienniki aktywności hello wystąpił błąd podczas rozwiązywania problemu lub toomonitor jak użytkownik w organizacji zmienić zasobu.

![Dziennik aktywności](./media/azure-log-audit/azure-log-audit-fig1.png)


Można pobrać zdarzenia z dziennika aktywności za pomocą hello portalu Azure, [CLI](https://docs.microsoft.com/azure/storage/storage-azure-cli), poleceń cmdlet programu PowerShell, a [interfejsu API REST Monitor Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-rest-api-walkthrough). Dzienniki aktywności ma 19-dniowy okres przechowywania danych.

Scenariusze integracji
-   [Utwórz alert e-mail lub elementu webhook wyzwala poza zdarzenie dziennika aktywności.](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-auditlog-to-webhook-email)

-   [Strumienia go tooan Centrum zdarzeń](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-stream-activity-logs-event-hubs) dla wprowadzanie przez usługi innej firmy lub rozwiązania analizy niestandardowych, takich jak usługi Power BI.

-   Analizować w usługi Power BI przy użyciu hello [pakiet zawartości usługi Power BI.](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs/)

-   [Zapisz tooa konto magazynu inspekcji archiwizacji lub ręcznie.](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-archive-activity-log) Można określić hello czas przechowywania (w dniach) przy użyciu profilów dziennika.

-   Zapytania i wyświetlać go w portalu Azure hello.

-   Zapytanie go za pomocą polecenia Cmdlet programu PowerShell, interfejsu wiersza polecenia lub interfejsu API REST.

-   Eksportuj hello dziennik aktywności przy użyciu profilów dziennika zbyt[dziennika analizy](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview).

Można użyć konta magazynu lub [przestrzeni nazw zdarzenia koncentratora](https://docs.microsoft.com/azure/event-hubs/event-hubs-resource-manager-namespace-event-hub-enable-archive) nie jest to w hello tej samej subskrypcji, jak hello jeden dziennik emisji. Witaj, użytkownik konfiguruje ustawienie hello musi mieć odpowiednie hello [RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) dostępu tooboth subskrypcji
### <a name="azure-diagnostic-logs"></a>Dzienniki diagnostyczne platformy Azure
Azure dzienników diagnostycznych są emitowane przez zasób zawierają rozbudowane, często dane dotyczące operacji hello tego zasobu. zawartość Hello te dzienniki zależy od typu zasobu (na przykład [dzienniki systemu zdarzeń systemu Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)są jedną kategorię dzienników diagnostycznych dla maszyn wirtualnych i [obiektów blob, tabel i dzienniki kolejki](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account) jest kategorii dzienników diagnostycznych w przypadku kont magazynu) i różnią się od hello dziennik aktywności, który zapewnia wgląd w operacji hello, wykonywane na zasobów w ramach subskrypcji.

![Dzienniki diagnostyczne platformy Azure](./media/azure-log-audit/azure-log-audit-fig2.png)

Dzienniki diagnostyczne Azure oferują wiele opcji konfiguracji, które jest, portalu Azure, przy użyciu programu PowerShell, interfejsu wiersza polecenia (CLI) i interfejsu API REST.

**Scenariusze integracji**
-   Zapisz je tooa [konta magazynu](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-archive-diagnostic-logs) inspekcji inspekcji lub ręcznie. Można określić hello czas przechowywania (w dniach) przy użyciu ustawień diagnostycznych hello.

-   [Strumienia ich koncentratory tooEvent](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs) dla wprowadzanie przez usługi innej firmy lub rozwiązania analizy niestandardowych, takich jak [usługi Power BI.](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

-   Analizuj je za pomocą [OMS Log Analytics.](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)

**Obsługiwane usługi schematu dla dzienników diagnostycznych i kategorie dziennika obsługiwanych na typ zasobu**


| Usługa | Schemat & dokumentów | Typ zasobu | Kategoria |
| ------- | ------------- | ------------- | -------- |
|Moduł równoważenia obciążenia| [Analizy dzienników dla usługi równoważenia obciążenia Azure (wersja zapoznawcza)](https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-monitor-log)|Microsoft.Network/loadBalancers|  LoadBalancerAlertEvent|
|||Microsoft.Network/loadBalancers| LoadBalancerProbeHealthStatus
|Grupy zabezpieczeń sieci|[Usługa Log Analytics dla sieciowych grup zabezpieczeń](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-nsg-manage-log)|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupEvent|
|||Microsoft.Network/networksecuritygroups|NetworkSecurityGroupRuleCounter|
|Bramy Application Gateway|[Rejestrowania diagnostyki bramy aplikacji](https://docs.microsoft.com/en-us/azure/application-gateway/application-gateway-diagnostics)|Microsoft.Network/applicationGateways|ApplicationGatewayAccessLog|
|||Microsoft.Network/applicationGateways|ApplicationGatewayPerformanceLog|
|||Microsoft.Network/applicationGateways|ApplicationGatewayFirewallLog|
|Usługa Key Vault|[Funkcja rejestrowania usługi Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-logging)|Microsoft.KeyVault/vaults|AuditEvent|
|Azure Search|[Włączanie i używanie analizy ruchu wyszukiwania](https://docs.microsoft.com/en-us/azure/search/search-traffic-analytics)|Microsoft.Search/searchServices|OperationLogs|
|Data Lake Store|[Uzyskiwanie dostępu do dzienników diagnostycznych dla usługi Azure Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-diagnostic-logs)|Microsoft.DataLakeStore/accounts|Inspekcja|
|Data Lake Analytics|[Accessing diagnostic logs for Azure Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-diagnostic-logs) (Dostęp do dzienników diagnostycznych usługi Azure Data Lake Analytics)|Microsoft.DataLakeAnalytics/accounts|Inspekcja|
|||Microsoft.DataLakeAnalytics/accounts|Żądania|
|||Microsoft.DataLakeStore/accounts|Żądania|
|Logic Apps|[Logic Apps — niestandardowy schemat śledzenia B2B](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-track-integration-account-custom-tracking-schema)|Microsoft.Logic/workflows|Obiekt WorkflowRuntime|
|||Microsoft.Logic/integrationAccounts|IntegrationAccountTrackingEvents|
|Azure Batch|[Azure rejestrowania diagnostycznego partii](https://docs.microsoft.com/en-us/azure/batch/batch-diagnostics)|Microsoft.Batch/batchAccounts|ServiceLog|
|Azure Automation|[Analizy dzienników dla usługi Automatyzacja Azure](https://docs.microsoft.com/en-us/azure/automation/automation-manage-send-joblogs-log-analytics)|Microsoft.Automation/automationAccounts|JobLogs|
|||Microsoft.Automation/automationAccounts|JobStreams|
|Usługa Event Hubs|[Azure Event Hubs dzienników diagnostycznych](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-diagnostic-logs)|Microsoft.EventHub/namespaces|ArchiveLogs|
|||Microsoft.EventHub/namespaces|OperationalLogs|
|Stream Analytics|[Dzienniki diagnostyczne zadania](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-job-diagnostic-logs)|Microsoft.StreamAnalytics/streamingjobs|Wykonanie|
|||Microsoft.StreamAnalytics/streamingjobs|Tworzenie|
|Service Bus|[Azure Service Bus dzienników diagnostycznych](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-diagnostic-logs)|Microsoft.ServiceBus/namespaces|OperationalLogs|

### <a name="azure-active-directory-reporting"></a>Raportowanie usługi Azure Active Directory
W usłudze Azure Active Directory (Azure AD) uwzględniono raporty dotyczące zabezpieczeń, działań i inspekcji dla katalogu. Witaj [raport dotyczący usługi Azure Active Directory inspekcji](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) pomaga klientom tooidentify uprzywilejowany akcje, które wystąpiły w usłudze Azure Active Directory. Uprzywilejowanych akcji obejmują zmiany podniesienia uprawnień (na przykład tworzenie roli lub resetowanie haseł), zmiana konfiguracji zasad (na przykład zasady haseł) lub zmiany konfiguracji toodirectory (na przykład zmiany toodomain federacyjnego ustawienia).

Witaj raporty zawierają hello rekordu inspekcji dla nazwy zdarzenia hello, aktora hello, który wykonał akcję hello, zasobu docelowego hello wpływ zmiany hello i hello daty i czasu (UTC). Klienci są w stanie tooretrieve hello listę zdarzeń inspekcji dla ich Azure Active Directory za pośrednictwem hello [portalu Azure](https://portal.azure.com/), zgodnie z opisem w [wyświetlanie dzienników inspekcji](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal). Poniżej przedstawiono listę raportów hello uwzględnionych:

| Raporty dotyczące zabezpieczeń | Raporty dotyczące działań | Raporty dotyczące inspekcji |
| :--------------- | :--------------- | :------------ |
|Logowania z nieznanych źródeł| Podsumowanie użycia aplikacji| Raport dotyczący inspekcji katalogu|
|Logowania po wielokrotnych niepowodzeniach|  Szczegóły użycia aplikacji||
|Logowania z wielu lokalizacji geograficznych|    Pulpit nawigacyjny aplikacji||
|Logowania z adresów IP związanych z podejrzanymi działaniami|   Błędy aprowizacji kont||
|Nieregularne działania związane z logowaniem|    Urządzenia indywidualnych użytkowników||
|Logowania z urządzeń, które mogą być zainfekowane|   Działania indywidualnych użytkowników||
|Nietypowe działania użytkowników związane z logowaniem| Raport dotyczący działań grup||
||Raport dotyczący działań związanych z rejestracją resetowania haseł||
||Działania związane z resetowaniem haseł|||

Hello dane z tych raportów mogą być przydatne tooyour aplikacji, takich jak systemów SIEM, inspekcji i narzędzia do analizy biznesowej. interfejsy API zapewniają dostęp programistyczny toohello danych za pomocą zestawu opartego na interfejsie REST API raportowania Hello Azure AD. Możesz wywołać te [interfejsów API](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started) z różnych języków programowania i narzędzi.

Zdarzenia w hello raport dotyczący usługi Azure AD inspekcji są zachowywane na okres 180 dni.

> [!Note]
> Aby uzyskać więcej informacji na temat przechowywania w raportach, zobacz [zasady przechowywania raportów Active Directory platformy Azure.](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-retention)

W przypadku klientów do przechowywania ich zdarzeń inspekcji przez dłuższy czas przechowywania, hello interfejsu API raportowania może być używany ściągania tooregularly [zdarzenia inspekcji](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-audit-events) do magazynu danych.

### <a name="virtual-machine-logs-using-azure-diagnostics"></a>Dzienniki maszyny wirtualnej za pomocą diagnostyki Azure
[Diagnostyka Azure](https://docs.microsoft.com/azure/azure-diagnostics) hello możliwość w ramach platformy Azure, która umożliwia hello zbieranie danych diagnostycznych o wdrożonej aplikacji. Można użyć rozszerzenia diagnostyki hello z różnych źródeł. Obecnie obsługiwane są [Azure Cloud Service w sieci Web i proces roboczy](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me),

![Dzienniki maszyny wirtualnej za pomocą diagnostyki Azure](./media/azure-log-audit/azure-log-audit-fig3.png)

[Maszyny wirtualne platformy Azure](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/) systemu Microsoft Windows i [sieci szkieletowej usług](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview).

Można włączyć diagnostyki Azure na maszynę wirtualną przy użyciu następujących:

-   Przy użyciu programu Visual Studio, zobacz [tootrace program Visual Studio maszynach wirtualnych platformy Azure](https://docs.microsoft.com/azure/vs-azure-tools-debug-cloud-services-virtual-machines)

-   [Konfigurowanie diagnostyki Azure w usłudze Azure Virtual Machine zdalnie](https://docs.microsoft.com/azure/virtual-machines-dotnet-diagnostics)

-   [Użyj programu PowerShell tooset się diagnostyki na maszynach wirtualnych platformy Azure](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-ps-extensions-diagnostics?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

-   [Utwórz maszynę wirtualną systemu Windows z monitorowania i diagnostyki za pomocą szablonu usługi Resource Manager Azure](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-extensions-diagnostics-template?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="storage-analytics"></a>Analityka magazynu
[Analizy usługi Azure Storage](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) wykonuje rejestrowanie i udostępnia metryki danych dla konta magazynu. Można użyć tego żądania tootrace danych, analizować trendy użycia i diagnozowanie problemów z kontem magazynu. Rejestrowanie analityka magazynu jest dostępne dla hello [usług obiektów Blob, kolejki i tabeli.](https://docs.microsoft.com/azure/storage/storage-introduction) Analityka magazynu rejestruje szczegółowe informacje na temat usługi Magazyn tooa udane i nieudane żądania.

Te informacje mogą być używane toomonitor poszczególnych żądań i toodiagnose problemy z usługą magazynu. Żądania są rejestrowane w sposób optymalny. Wpisy dziennika są tworzone tylko w przypadku żądań wysyłanych do punktu końcowego usługi hello. Na przykład jeśli konto magazynu ma aktywności w punktu końcowego obiektu Blob, ale nie w jej tabel lub kolejek punktów końcowych, tylko dzienniki dotyczące toohello usługi obiektów Blob jest tworzony.

toouse analityka magazynu, należy ją włączyć osobno dla każdej usługi ma toomonitor. Możesz je włączyć w hello [portalu Azure](https://portal.azure.com/); Aby uzyskać więcej informacji, zobacz [monitorować konta magazynu w hello portalu Azure.](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account) Można również włączyć analityka magazynu programowo przy użyciu interfejsu API REST hello lub powitania klienta biblioteki. Użyj hello ustawić właściwości usługi operacji tooenable analityka magazynu osobno dla każdej usługi.

Hello zagregowane dane są przechowywane w dobrze znany obiekt blob (w przypadku rejestrowania) i dobrze znanego tabele (dla metryki), które mogą uzyskać dostęp za pomocą usługi Blob hello i tabeli interfejsów API.

Analityka magazynu ma limit 20 TB na powitania ilość przechowywanych danych, która jest niezależna od hello całkowitego limitu konta magazynu. Wszystkie dzienniki są przechowywane w [blokowe obiekty BLOB](https://docs.microsoft.com/azure/storage/storage-analytics) w kontenerze o nazwie $logs, które są automatycznie tworzone podczas analityka magazynu jest włączona dla konta magazynu.

> [!Note]
> Aby uzyskać więcej informacji dotyczących rozliczeń i zasad przechowywania danych, zobacz [analizy magazynu i rozliczeń.](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-and-billing)
>
> [!Note]
> Aby uzyskać więcej informacji o limity konta magazynu, zobacz [cele dotyczące wydajności i skalowalności magazynu Azure.](https://docs.microsoft.com/azure/storage/storage-scalability-targets)

następujące typy żądań uwierzytelnionych i anonimowych Hello są rejestrowane.



| Uwierzytelniony  | Anonimowe|
| :------------- | :-------------|
| Liczba pomyślnych żądań | Liczba pomyślnych żądań |
|Nieudane żądania, w tym limitu czasu, ograniczania przepustowości sieci, autoryzacji i innych błędów | Żądania przy użyciu dostępu sygnatury dostępu Współdzielonego, włącznie z żądaniami nie powiodło się i pomyślne |
| Żądania przy użyciu dostępu sygnatury dostępu Współdzielonego, włącznie z żądaniami nie powiodło się i pomyślne |Błędy limitu czasu dla klienta i serwera |
|   Żądania tooanalytics danych |    Nieudane żądania GET z kodem błędu 304 (nie jest zmodyfikowany) |
| Żądania wysyłane przez analityka magazynu, takich jak dziennika utworzeniu lub usunięciu, nie są rejestrowane. Pełną listę hello zarejestrowane dane są udokumentowane WE hello [operacje rejestrowane analityka magazynu i komunikaty o stanie](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) i [Format dziennika analityka magazynu](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format) tematów. | Inne nieudanych żądań anonimowych nie są rejestrowane. Pełną listę hello zarejestrowane dane są udokumentowane WE hello [operacje rejestrowane analityka magazynu i komunikaty o stanie](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) i [Format dziennika analityka magazynu](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format). |

### <a name="azure-networking-logs"></a>Dzienniki sieci platformy Azure
Sieć rejestrowania i monitorowania na platformie Azure jest kompleksowy i obejmuje dwie szerokie kategorie:

-   [Monitor sieci](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) -monitorowania sieci oparta na scenariuszu jest dostarczana z funkcji hello w obserwatora sieciowego. Ta usługa obejmuje przechwytywania pakietów, następnego przeskoku, przepływ IP Sprawdź widok grupy zabezpieczeń, dzienniki przepływu NSG. Scenariusz poziomu monitorowania udostępnia widok tooend zakończenia zasobów sieciowych w monitorowania zasobów sieciowych tooindividual kontrastu.

-   [Monitorowanie zasobów](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-resource-level-monitoring) -poziomu monitorowania zasobów składa się z czterech funkcji, dzienników diagnostycznych metryki, rozwiązywanie problemów i kondycji zasobów. Te funkcje są tworzone na poziomie zasobów sieciowych hello.

![Dzienniki sieci platformy Azure](./media/azure-log-audit/azure-log-audit-fig4.png)

Obserwatora sieciowego jest usługą regionalnych, która umożliwia toomonitor możesz i diagnozowanie warunki na poziomie sieci scenariusz w, do i z platformy Azure. Diagnostyka sieci i narzędzi wizualizacji dostępnych z obserwatora sieciowego pomagają zrozumieć, diagnozowanie i uzyskać informacje na temat technologii sieci tooyour na platformie Azure.

**Przepływ NSG rejestrowania** — dzienniki przepływu dla grup zabezpieczeń sieci Włącz toocapture dzienniki pokrewne tootraffic, który ma być dozwolony lub odrzucany przez reguły zabezpieczeń hello hello grupy. Te dzienniki przepływu są zapisywane w formacie JSON i Pokaż wychodzących i przepływów przychodzących na podstawie reguł na, hello przepływu hello kart stosuje, 5-elementowej informacji o przepływie hello (źródłowego i docelowego adresu IP, portu źródłowego i docelowego Protocol), a jeśli hello ruchu jest dozwolone, lub Odmowa dostępu.

### <a name="network-security-group-flow-logging"></a>Rejestrowanie przepływu grupy zabezpieczeń sieci

[Grupy zabezpieczeń sieci przepływu dzienniki](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) są funkcją obserwatora sieciowego, który pozwala tooview informacji na temat przychodzące i wychodzące ruchu IP za pośrednictwem grupy zabezpieczeń sieci. Te dzienniki przepływu są zapisywane w formacie JSON i Pokaż wychodzących i przepływów przychodzących na podstawie reguł na, hello przepływu hello kart stosuje, 5-elementowej informacji o przepływie hello (źródłowego i docelowego adresu IP, portu źródłowego i docelowego Protocol), a jeśli hello ruchu jest dozwolone, lub Odmowa dostępu.

Podczas przepływu rejestruje grup zabezpieczeń sieci docelowej, nie są wyświetlane hello takie same jak hello inne dzienniki. Przepływ dzienniki są przechowywane tylko w ramach konta magazynu.

Witaj takie same zasady przechowywania, jak pokazano na inne dzienniki zastosować tooflow dzienników. Dzienniki ma zasady przechowywania, które można ustawić dni too365 1 dzień. Jeśli zasady przechowywania nie jest ustawiona, dzienniki hello są obsługiwane w nieskończoność.

**Dzienniki diagnostyczne**

Okresowe i spontanicznych zdarzenia są tworzone przez zasobów sieciowych i zarejestrowane na kontach magazynu, wysyłane tooan Centrum zdarzeń lub analizy dzienników. Te dzienniki wgląd w kondycję hello zasobu. Te dzienniki można wyświetlać w narzędzi, takich jak Power BI i analizy dzienników. toolearn jak tooview dzienników diagnostycznych, odwiedź stronę [analizy dzienników.](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-networking-analytics)

![Dzienniki diagnostyczne](./media/azure-log-audit/azure-log-audit-fig5.png)

Dzienniki diagnostyczne są dostępne dla [modułu równoważenia obciążenia](https://docs.microsoft.com/azure/load-balancer/load-balancer-monitor-log), [grup zabezpieczeń sieci](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log), trasy i [bramy aplikacji.](https://docs.microsoft.com/azure/application-gateway/application-gateway-diagnostics)

Wyświetl dzienniki diagnostyczne zawiera obserwatora sieciowego. Ten widok zawiera wszystkich zasobów sieciowych, które obsługują rejestrowania diagnostycznego. Z tego widoku można włączyć i wyłączyć zasobów sieciowych, łatwo i szybko.


W funkcji rejestrowania toopreceding dodanie obserwatora sieciowego ma obecnie hello następujące możliwości:
- [Topologia](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) — zapewnia hello przedstawiający widok poziomu sieci różnych połączeń i skojarzenia między zasobami sieci w grupie zasobów.

- [Zmienna przechwytywania pakietów](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview) -przechwytuje pakiet danych do i z maszyny wirtualnej. Zaawansowane opcje filtrowania i dostosować formanty, takie jak trwa stanie tooset ograniczenia czasu i rozmiaru znajdują się dane pakietu versatility.hello mogą być przechowywane w magazynie obiektów blob lub na dysku lokalnym hello w formacie CAP.

-   [Przepływ IP weryfikuje](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview) — sprawdza, czy pakiet jest dozwolony lub niedozwolony na podstawie przepływ informacji 5-elementowej pakietu parametrów (docelowy adres IP, źródłowy adres IP, Port docelowy, Port źródłowy i Protocol). Jeśli pakietów hello jest zabroniony przez grupę zabezpieczeń, hello reguły i grup, które odmowa pakietów hello jest zwracana.

-   [Następny przeskok](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) — określa hello następnego skoku dla pakietów przesyłane w hello Azure sieci szkieletowej, umożliwiając tras toodiagnose any nieprawidłowo zdefiniowane przez użytkownika.

-   [Widok grupy zabezpieczeń](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) -pobiera hello zabezpieczeń skuteczne i zastosowanej reguły, które są stosowane na maszynie Wirtualnej.

-   [Brama sieci wirtualnej i rozwiązywanie problemów z połączenia](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) — zapewnia hello tootroubleshoot możliwości połączenia i bramy sieci wirtualnej.

-   [Limity subskrypcji sieci](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-subscription-limits) — umożliwia użycie zasobów sieciowych tooview ograniczeń.

### <a name="application-insight"></a>Szczegółowe informacje o aplikacji

[Usługa Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview) jest rozszerzalną usługę zarządzania wydajności aplikacji (APM) dla deweloperów sieci web na wielu platformach. Użyj go toomonitor aplikacji sieci web na żywo. Jest automatycznie wykrywania anomalii wydajności. Obejmuje on analytics zaawansowanych narzędzi toohelp diagnozować problemy i toounderstand co użytkownicy faktycznie wykonać za pomocą aplikacji.

 Zaprojektowano go toohelp stale zwiększyć wydajność i użyteczność.

 Działa w przypadku aplikacji na różnych platformach w tym .NET, Node.js i J2EE obsługiwanego lokalnie lub w chmurze hello. Integruje się z procesu opracowywania oprogramowania i zawiera narzędzia do programowania toovarious punkty połączenia.

![Szczegółowe informacje o aplikacji](./media/azure-log-audit/azure-log-audit-fig6.png)

Usługa Application Insights jest celem hello zespół deweloperów, toohelp zrozumieć, jak aplikacja działa prawidłowo, i jak jest używany. Monitoruje ona:

-   **Liczby żądań, czasy reakcji i współczynniki błędów** — dowiedz się, które strony są najbardziej popularne, o jakiej porze dnia i gdzie są Twoi użytkownicy. Zobacz, które strony działają najlepiej. Jeśli Twoje czasy odpowiedzi i częstotliwości awarii są duże, gdy jest więcej żądań, być może masz problem z zasobami.

-   **Współczynniki zależności, czasy reakcji i współczynniki błędów** — dowiedz się, czy usługi zewnętrzne nie spowalniają pracy.

-   **Wyjątki** — analizowania statystyk zagregowane hello, lub wybierz określone wystąpienia i przejść do szczegółów w hello ślad stosu i powiązane żądań. Są zgłaszane zarówno wyjątki serwera, jak i przeglądarki.

-   **Wydajność ładowania i wyświetleń stron** — zgłoszona przez przeglądarki użytkowników.

-   **Wywołania AJAX** ze stron sieci Web — liczba, czasy reakcji i współczynniki błędów.

-   **Liczby użytkowników i sesji**.

-   **Liczniki wydajności** z serwerów systemu Windows lub Linux, takie jak użycie procesora CPU, pamięci i sieci.

-   **Diagnostyka hosta** z platformy Docker lub Azure.

-   **Diagnostyczne dzienniki śledzenia** z Twojej aplikacji — dzięki temu możesz skorelować zdarzenia śledzenia z żądaniami.

-   **Niestandardowe zdarzenia i metryki** napisanie samodzielnie powitania klienta lub serwera kodu tootrack zdarzeń biznesowych takich jak elementy sprzedaży lub gier kupione.

**Listę scenariuszy integracji i opis:**

| Scenariusze integracji | Opis |
| --------------------- | :---------- |
|[Mapowanie aplikacji](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-app-map)|składniki Hello aplikacji, za pomocą kluczowych metryk i alerty.||
|[Diagnostycznych wyszukiwania danych dla wystąpienia](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-diagnostic-search)| Wyszukiwanie i filtrowanie zdarzeń, takich jak żądania, wyjątki, wywołania zależności, dzienniki śledzenia i wyświetlenia stron.||
|[Eksploratora metryk na zastosowanie zagregowanych danych](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-metrics-explorer)|Eksploruj, filtruj i segmentuj zagregowane dane, takie jak liczby żądań, błędów i wyjątków, czasy reakcji, czasy ładowania stron.||
|[Pulpity nawigacyjne](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-dashboards#dashboards)|Połącz dane z wielu zasobów i udostępnij innym osobom. Doskonały dla wielu składnika aplikacji i ciągłe wyświetlaną w pokoju zespołu hello.||
|[Metryki strumień na żywo](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-live-stream)|Podczas wdrażania nowej kompilacji, obejrzyj te wskaźniki wydajności w pobliżu czasie rzeczywistym toomake się, że wszystko działa zgodnie z oczekiwaniami.||
|[Analiza](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics)|Odpowiedz na trudne pytania dotyczące wydajności i użycia Twojej aplikacji za pomocą tego zaawansowanego języka zapytań.||
|[Alerty automatycznej i ręcznej](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-alerts)|Automatyczne alerty dostosowania aplikacji tooyour normalne wzorców telemetrii i wyzwalacza, gdy coś poza wzorzec zwykle hello jest. Możesz też ustawić alerty dla konkretnych poziomów metryk niestandardowych lub standardowych.||
|[Program Visual Studio](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-visual-studio)|Dane wydajności w kodzie hello widoczne. Przechodzenie toocode z śladów stosu.||
|[Power BI](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-power-bi)|Integruje metryki użycia z innymi analizami biznesowymi.||
|[Interfejs API REST](https://dev.applicationinsights.io/)|Napisać kod zapytania toorun nad metryki i dane pierwotne.||
|[Eksport ciągły](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-telemetry)|Zbiorcze eksportu toostorage nieprzetworzone dane po dostarczeniu.||

### <a name="azure-security-center-alerts"></a>Alerty Centrum zabezpieczeń Azure
[Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) automatycznie gromadzi, analizuje i integruje dane dzienników z zasobów platformy Azure, sieci hello i połączonych rozwiązań partnerskich, takich jak zapory i punktu końcowego rozwiązań do ochrony, toodetect prawdziwe zagrożenia i zmniejszyć fałszywych alarmów. Lista alertów zabezpieczeń uporządkowanych według priorytetu jest wyświetlany w Centrum zabezpieczeń oraz hello informacje potrzebne tooquickly Zbadaj hello problem i zalecenia dotyczące tooremediate atak.

Wykrywanie zagrożeń Centrum zabezpieczeń polega na automatyczne zbieranie informacji o zabezpieczeniach z zasobów platformy Azure, hello sieci i rozwiązań partnerskich połączonych. Te informacje, często korelowanie informacji z wielu źródeł, zagrożenia tooidentify analizę. Alerty zabezpieczeń mają pierwszeństwo w Centrum zabezpieczeń wraz z zaleceniami w sposób tooremediate hello zagrożeń.

![Azure Security Center](./media/azure-log-audit/azure-log-audit-fig7.png)

Usługa Security Center wykorzystuje zaawansowane narzędzia analizy zabezpieczeń, które wykraczają daleko poza metody bazujące na sygnaturze. Osiągnięć w dużej ilości danych i [uczenia maszynowego](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) technologii są stosowane tooevaluate zdarzenia w sieci szkieletowej chmury całego hello — wykrywanie zagrożeń, które mogą być niemożliwe tooidentify przy użyciu metod ręcznych i prognozowanie hello rozwój ataków. Do narzędzi analizy zabezpieczeń należą:

-   **Zintegrowane analizy zagrożeń:** wygląda dla znanych nieupoważnione osoby, stosując globalnej analizy zagrożeń ze swoich produktów i usług, hello Microsoft cyfrowego ds. przestępstw jednostki (DCU), hello Microsoft Security odpowiedzi Center (MSRC) i zewnętrznego źródła danych.

-   **Analizy behawioralnej:** stosuje znane wzorce toodiscover złośliwego zachowania.

-   **Wykrywanie anomalii:** używa statystyczne profilowania toobuild historycznych linii bazowej. Generuje alert w odchylenia od ustalonych linii bazowych, zgodnych ze standardami tooa potencjalnego ataku.


Wiele operacji zabezpieczeń i odpowiedzi na zdarzenia zespołów zależne rozwiązania Security Information and Event Management (SIEM) jako hello punkt początkowy dla klasyfikowane i badanie alertów zabezpieczeń. Dzięki integracji dzienników Azure klienci mogą synchronizować alerty Centrum zabezpieczeń i zdarzenia zabezpieczeń maszyny wirtualnej, zebrane przez diagnostyki Azure i dzienników inspekcji platformy Azure, z ich analizy dzienników lub rozwiązania SIEM w najbliższym czasie rzeczywistym.


## <a name="log-analytics"></a>Log Analytics

Analiza dzienników jest usługą [Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) który pomaga zbieranie i analizowanie danych wygenerowanych przez zasobów w chmurze i lokalnych środowiskach. Zapewnia wgląd w czasie rzeczywistym za pomocą wyszukiwanie zintegrowane i niestandardowe pulpity nawigacyjne tooreadily analizowanie miliony rekordów we wszystkich obciążeń i serwerów, niezależnie od ich lokalizacji fizycznej.

![Log Analytics](./media/azure-log-audit/azure-log-audit-fig8.png)

Na powitania center analizy dzienników jest hello OMS repozytorium, która jest hostowana w hello chmury Azure. Dane są zbierane w repozytorium hello z połączonych źródeł Konfigurowanie źródeł danych i dodawania subskrypcji tooyour rozwiązania. Źródła danych i rozwiązania spowoduje utworzenie różnych typów rekordów własnych zbiór właściwości, które mogą być analizowane razem w repozytorium toohello zapytania. Dzięki temu hello toouse tego samego narzędzia i metody toowork z różnych rodzajów danych zbieranych przez różnych źródeł.

Połączone źródła są hello komputery i inne zasoby, które generują dane zebrane przez analizy dzienników. Może to obejmować agentów zainstalowanych na [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) i [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents) komputerów, które łączą się bezpośrednio lub agentów w [podłączonej grupy zarządzania programu System Center Operations Manager.](https://docs.microsoft.com/azure/log-analytics/log-analytics-om-agents) Analiza dzienników może również zbierać dane z [magazynu Azure.](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage)

[Źródła danych](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources) są hello różnych rodzajów zebrane podczas każdego połączenia źródła danych. Obejmuje to zdarzenia i [dane dotyczące wydajności](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-performance-counters) z [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events) i agentów systemu Linux w toosources dodanie, takich jak [dzienniki programu IIS](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-iis-logs), i [dzienniki tekstowe niestandardowych.](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-custom-logs) Możesz skonfigurować dla każdego źródła danych ma toocollect, czy konfiguracja hello jest automatycznie dostarczonego tooeach połączone źródła.

Istnieją cztery różne sposoby [zbieranie dzienników i metryki dla usług Azure:](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage)
1.  Diagnostyka Azure bezpośredniego tooLog Analytics (Diagnostyka w poniższej tabeli hello)

2.  Diagnostyka Azure tooAzure magazynu tooLog Analytics (magazynu w poniższej tabeli hello)

3.  Łączniki dla usług Azure (łączników w poniższej tabeli hello)

4.  Skrypty toocollect, a następnie post danych do analizy dzienników (puste wartości w hello w poniższej tabeli i usług, które nie są wymienione)

| Usługa | Typ zasobu | Dzienniki | Metryki | Rozwiązanie |
| :------ | :------------ | :--- | :------ | :------- |
|Bramy aplikacji|  Microsoft.Network/<br>applicationGateways|  Diagnostyka|Diagnostyka|    [Aplikacja Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-application-gateway-analytics-solution-in-log-analytics) [Gateway Analytics](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-application-gateway-analytics-solution-in-log-analytics)|
|Usługa Application insights||     Łącznik|  Łącznik|  [Usługa Application Insights](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/) [Connector (wersja zapoznawcza)](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/)|
|Konta usługi Automation|   Microsoft.Automation/<br>AutomationAccounts|    Diagnostyka||       [Więcej informacji](https://docs.microsoft.com/en-us/azure/automation/automation-manage-send-joblogs-log-analytics)|
|Konta usługi partia zadań|    Microsoft.Batch/<br>batchAccounts|  Diagnostyka|    Diagnostyka||
|Usługi w chmurze klasycznego||       Magazyn||       [Więcej informacji](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage-iis-table)|
|Usługi poznawcze|    Microsoft.CognitiveServices/<br>accounts|       Diagnostyka|||
|Data Lake analytics|   Microsoft.DataLakeAnalytics/<br>accounts|   Diagnostyka|||
|Data Lake store|   Microsoft.DataLakeStore/<br>accounts|   Diagnostyka|||
|Przestrzeń nazw Centrum zdarzeń|   Microsoft.EventHub/<br>Przestrzenie nazw|  Diagnostyka|    Diagnostyka||
|Centra IoT|  Microsoft.Devices/<br>IotHubs||     Diagnostyka||
|Usługa Key Vault| Microsoft.KeyVault/<br>magazynów|  Diagnostyka  || [KeyVault analityka](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-key-vault)|
|Moduły równoważenia obciążenia|    Microsoft.Network/<br>loadBalancers|    Diagnostyka|||
|Logic Apps|    Microsoft.Logic/<br>Przepływy pracy|  Diagnostyka|    Diagnostyka||
||Microsoft.Logic/<br>integrationAccounts||||
|Grupy zabezpieczeń sieci|   Microsoft.Network/<br>networksecuritygroups|Diagnostyka||   [Grupy zabezpieczeń sieci Azure analityka](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-network-security-group-analytics-solution-in-log-analytics)|
|Magazyny odzyskiwania|   Microsoft.RecoveryServices/<br>magazynów|||[Usługa Azure Recovery usługi Analytics (wersja zapoznawcza)](https://github.com/krnese/AzureDeploy/blob/master/OMS/MSOMS/Solutions/recoveryservices/)|
|Usługi wyszukiwania|   Microsoft.Search/<br>searchServices|    Diagnostyka|    Diagnostyka||
|Przestrzeń nazw magistrali usług| Microsoft.ServiceBus/<br>Przestrzenie nazw|    Diagnostyka|Diagnostyka|    [Analiza magistrali usług (wersja zapoznawcza)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-servicebus-solution)|
|Service Fabric||       Magazyn||    [Usługa sieci szkieletowej Analytics (wersja zapoznawcza)](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-service-fabric)|
|SQL (v12)| Microsoft.Sql/<br>serwery /<br>bazy danych||       Diagnostyka||
||Microsoft.Sql/<br>serwery /<br>elasticPools||||
|Magazyn|||         Skrypt| [Usługa Azure Storage Analytics (wersja zapoznawcza)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-azure-storage-analytics-solution)|
|Maszyny wirtualne|  Microsoft.Compute/<br>maszyn wirtualnych|  Wewnętrzny|  Wewnętrzny||
||||Diagnostyka||
|Zestawy skalowania maszyn wirtualnych|   Microsoft.Compute/<br>maszyn wirtualnych    ||Diagnostyka||
||Microsoft.Compute/<br>virtualMachineScaleSets /<br>maszyn wirtualnych||||
|Farmach serwerów sieci Web|Microsoft.Web/<br>serverfarms||   Diagnostyka
|Witryny sieci Web| Microsoft.Web/<br>Lokacje ||      Diagnostyka|    [Więcej informacji](https://github.com/Azure/azure-quickstart-templates/tree/master/101-webappazure-oms-monitoring)|
||Microsoft.Web/<br>Lokacje /<br>gniazda|||||


## <a name="log-integration-with-on-premises-siem-systems"></a>Dziennik integracji z lokalnymi systemów SIEM
[Integracja z dzienników Azure](https://www.microsoft.com/download/details.aspx?id=53324) pozwala toointegrate nowych dzienników z zasobów platformy Azure w lokalnym tooyour **systemów Security Information and Event Management (SIEM)**.

![Integracja dziennika](./media/azure-log-audit/azure-log-audit-fig9.png)

Integracja z dzienników Azure zbiera diagnostyki Azure z systemem Windows (WAD) maszyn wirtualnych Azure Dzienniki aktywności, alerty Centrum zabezpieczeń Azure i dzienniki dostawcy zasobów platformy Azure. Integracja ta zapewnia jednolity pulpit nawigacyjny dla wszystkich zasobów, lokalnie lub w chmurze hello, dzięki czemu może agregować, skorelowania, analizowanie i alertów zdarzeń zabezpieczeń.



Integracja dzienników Azure obsługuje obecnie integracji Dzienniki aktywności platformy Azure, dziennika zdarzeń systemu Windows z maszyny wirtualnej systemu Windows w Twojej subskrypcji platformy Azure, dzienniki inspekcji alerty Centrum zabezpieczeń Azure, dzienników diagnostycznych platformy Azure i usługi Azure Active Directory.

| Typ dziennika | Obsługa formatu JSON (Splunk, ArcSight, Qradar) analizy dzienników |
| :------- | :-------------------------------------------------------- |
|Dzienniki inspekcji usługi AAD|    Tak|
|Dzienniki aktywności| Tak|
|Alerty ASC |Tak|
|Dzienniki diagnostyczne (Dzienniki zasobów)|  Tak|
|Dzienniki maszyny Wirtualnej|   Tak, za pośrednictwem przekazane zdarzenia, a nie za pośrednictwem JSON|


Witaj poniższej tabeli opisano hello dziennika kategorii i szczegóły integracji SIEM.

[Wprowadzenie do integracji dzienników Azure](https://docs.microsoft.com/azure/security/security-azure-log-integration-get-started) — samouczek przeprowadzi Cię przez kolejne instalacji integracji dzienników Azure i integrowanie dzienniki z magazynu Azure WAD, dzienniki aktywności platformy Azure, alerty Centrum zabezpieczeń Azure i usługi Azure Active Directory dzienniki inspekcji.

Scenariusze integracji

-   [Czynności konfiguracyjnych partnera](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) — ten wpis w blogu pokazuje, jak tooconfigure Azure dziennika toowork integracji z rozwiązań partnerskich Splunk HP ArcSight i IBM QRadar.

-   [Dzienników Azure — często zadawane pytania (FAQ) integracji](https://docs.microsoft.com/azure/security/security-azure-log-integration-faq) — to często zadawane pytania dotyczące odpowiedzi na pytania dotyczące integracji dzienników Azure.

-   [Integrowanie Centrum zabezpieczeń alertów z usługi Azure dziennika integracji](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration) — tym dokumencie przedstawiono, jak alerty Centrum zabezpieczeń toosync, wraz z zebrane przez diagnostyki Azure i dzienników inspekcji platformy Azure, z Twojego analizy dzienników zdarzeń zabezpieczeń maszyny wirtualnej lub Rozwiązania SIEM.

## <a name="next-steps"></a>Następne kroki

- [Inspekcja i rejestrowanie](https://www.microsoft.com/trustcenter/security/auditingandlogging)

Ochrona danych przy zachowaniu widoczności i szybko reagować tootimely alerty zabezpieczeń

- [Rejestrowanie zabezpieczeń i kolekcji dziennika inspekcji w systemie Azure](https://azure.microsoft.com/resources/videos/security-logging-and-audit-log-collection/)

Które ustawienia należy toomake tooenforce się, że Twoje wystąpieniach platformy Azure są zbierane hello poprawnych zabezpieczeń i dzienniki inspekcji.

- [Skonfiguruj ustawienia inspekcji dla zbioru witryn](https://support.office.com/article/Configure-audit-settings-for-a-site-collection-A9920C97-38C0-44F2-8BCB-4CF1E2AE22D2?ui=&rs=&ad=US)

Jako administrator zbioru witryn jeden można pobrać historii hello akcje wykonywane przez określonego użytkownika i może również pobierać hello historię działania podjęte w zakresie określonej daty. 

- [Dziennik inspekcji hello wyszukiwania w hello Office 365 zabezpieczeń & Centrum zgodności](https://support.office.com/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=&rs=&ad=US)

Jeden służy hello Office 365 zabezpieczeń & Centrum zgodności toosearch hello ujednoliconego dziennika tooview użytkownika do inspekcji i działania administratora w organizacji usługi Office 365.


