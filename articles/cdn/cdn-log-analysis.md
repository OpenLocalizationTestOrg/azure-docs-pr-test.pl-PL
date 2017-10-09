---
title: "Analiza aaaLog dla usługi Azure CDN | Dokumentacja firmy Microsoft"
description: "Klienta można włączyć analizy dziennika dla usługi Azure CDN."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: 56e5a4fec46fd156cf38252732afb4522741d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a>Dzienniki diagnostyczne dla usługi Azure CDN

Po włączeniu sieci CDN w warstwie aplikacji będzie prawdopodobnie mają toomonitor hello CDN użycia, Sprawdź kondycję hello firmy i rozwiązywania potencjalnych problemów. Usługi Azure CDN zapewnia dodatkowe możliwości z [sieci CDN w warstwie podstawowa analiza](cdn-analyze-usage-patterns.md) i [dzienników diagnostycznych](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)

## <a name="cdn-core-analytics"></a>Sieci CDN w warstwie podstawowa analiza
Bieżący użytkownik usługi Azure CDN z Verizon standardowa lub premium profilu masz już możliwe tooview podstawowa analiza w portalu dodatkowym hello dostępny przy użyciu opcji "Manage" hello z hello portalu Azure. 

## <a name="azure-diagnostic-logs"></a>Dzienniki diagnostyczne platformy Azure

Azure przy użyciu tej nowej funkcji, można teraz wyświetlić podstawowa analiza i zapisać je w co najmniej jednego miejsca docelowe, w tym:

 - Konto usługi Azure Storage
 - Azure Event Hubs
 - [Repozytorium OMS analizy dzienników](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 Ta funkcja jest dostępna dla wszystkich punktów końcowych usługi CDN należące tooVerizon (Standard i Premium) oraz profilów usługi CDN Akamai (Standard).

Dzienniki diagnostyczne Zezwalaj metryki użycia podstawowe tooexport z sieci CDN punktu końcowego tooa różnych źródeł, dzięki czemu będzie można korzystać dostosowany sposób. Na przykład można wykonać hello następujące typy eksportu danych:

- Eksportuj tooblob pamięci masowej, Eksportuj tooCSV i Generuj wykresy w programie excel.
- Eksportowanie danych tooevent koncentratorów i skorelowania danych z innych usług azure.
- Eksportowanie danych toolog analytics i dane widoku w własne obszar roboczy OMS

Witaj rysunku poniżej przedstawiono typowe przeglądanie sieci CDN w warstwie podstawowa analiza danych.

![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/01_OMS-workspace.png)

*Rysunek 1 — widok sieci CDN w warstwie podstawowa analiza*

następujące wskazówki Hello przechodzi przez schemat hello hello core analizy danych, etapy włączenie funkcji hello dostarczania ich toovarious miejsc docelowych i korzystanie z tych miejsc docelowych.

## <a name="enable-logging-with-azure-portal"></a>Włącz rejestrowanie z portalu Azure

> [!NOTE]
> Witaj dzienników diagnostycznych są włączone **poza** domyślnie. 

Wykonaj kroki hello poniżej rejestrowanie tooenable z sieci CDN w warstwie podstawowa analiza:

Zaloguj się toohello [portalu Azure](http://portal.azure.com). Jeśli nie masz już włączone dla przepływu pracy, w sieci CDN [włączyć usługi Azure CDN](cdn-create-new-endpoint.md) przed kontynuowaniem.

1. W portalu hello Przejdź zbyt**profilu CDN**.
2. Wybierz profil CDN, a następnie wybierz punkt końcowy CDN hello, które mają tooenable **dzienników diagnostycznych**.

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. Przejdź za**dzienników diagnostycznych** bloku w obszarze **monitorowanie** sekcji, a następnie zmień stan hello zbyt**na**.

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a>Włącz rejestrowanie z usługą Azure Storage
    
toouse dzienniki hello toostore magazynu Azure, wybierz **archiwum konta magazynu tooa**, wybierz dni przechowywania i kliknij przycisk **CoreAnalytics** w obszarze **dziennika**.

![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

*Rysunek 2 — rejestrowanie z usługą Azure Storage*

### <a name="logging-with-oms-log-analytics"></a>Rejestrowanie z OMS analizy dzienników

toouse analizy dzienników OMS toostore hello dzienniki, wykonaj następujące kroki:

1. Z hello **dzienników diagnostycznych** bloku w obszarze **monitorowanie**, wybierz pozycję **wysyłania tooLog Analytics** z 

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. Konfiguruj rejestrowanie analizy dzienników hello, klikając polecenie Konfiguruj. Zostanie wyświetlone okno dialogowe tooa, gdzie poprzedniej obszaru roboczego wybierz lub Utwórz nową.

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. Kliknij przycisk **Utwórz nowy obszar roboczy**.

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/07_Create-new.png)

4. Następnie musisz wybrać nową nazwę obszaru roboczego, istniejącej subskrypcji, grupy zasobów (Nowa lub istniejąca), lokalizacji i warstwę cenową. Dostępna jest opcja hello przypinanie ten pulpit nawigacyjny tooyour konfiguracji. Kliknij przycisk OK toocomplete hello konfigurację.

    Obok obszaru roboczego powinna zostać wyświetlona z nazwami grup obszarem roboczym pakietu OMS i zasobów. Nazwy musi być unikatowa i można używać tylko litery, cyfry i łączniki. Spacje i znaki podkreślenia są niedozwolone. 

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. Następnie Pobierz krótki komunikat informujący, że obszar roboczy użytkownika został utworzony i są zwracane tooyour rejestrowania ekranu konfiguracji. Można potwierdzić hello nazwę obszaru roboczego analizy dzienników.

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    Po skonfigurowaniu hello konfiguracji analizy dzienników upewnij się, że zaznaczysz pola CoreAnalytics hello rejestrowania w sieci CDN.

6. Jeśli wszystko jest preferencjom tooyour, kliknij hello **zapisać** u góry okna dialogowego konfiguracji hello hello.

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/10_Save-me.png)

    Witaj **zapisać** przycisk nie jest już aktywne i że hello na/wyłączanie przycisku jest teraz ON, ale blue zamiast purpurowy.

7. Toosee nowy obszar roboczy OMS, przejdź tooyour portalu Azure pulpitu nawigacyjnego, kliknij nazwę hello obszaru roboczego analizy dzienników. Następnie zostanie wyświetlony obszar roboczy (Upewnij się, że obszar roboczy OMS jest wyróżnione po lewej stronie powitania). Polecenie hello portalu OMS kafelka toosee obszaru roboczego w repozytorium OMS hello. 

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    Repozytorium OMS jest teraz gotowy toolog danych. W celu tooconsume danych, należy użyć [rozwiązania OMS](#consuming-oms-log-analytics-data), wymienionych w dalszej części tego artykułu.

Więcej informacji na temat opóźnienia danych dziennika [tutaj](#log-data-delays).

## <a name="enable-logging-with-powershell"></a>Włącz rejestrowanie przy użyciu programu PowerShell

Poniżej znajduje się przykład w sposób tooenable i Pobierz dzienniki diagnostyczne za pośrednictwem hello polecenia cmdlet programu PowerShell usługi Azure.

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a>Włączanie diagnostyki logowania na koncie magazynu

Zaloguj się najpierw, a następnie wybierz subskrypcję:

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


tooEnable dzienników diagnostycznych na koncie magazynu, użyj tego polecenia:

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
tooEnable dzienników diagnostyki w obszarze roboczym pakietu OMS, użyj tego polecenia:

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a>Korzystanie z dzienników diagnostycznych z usługi Azure Storage
W tej sekcji opisano schemat hello hello sieci CDN w warstwie podstawowa analiza, w jaki sposób te są zorganizowane w ramach konta magazynu platformy Azure i zawiera przykładowy kod toodownload hello rejestruje się w pliku CSV tooa.

### <a name="using-microsoft-azure-storage-explorer"></a>Za pomocą Eksploratora usługi Storage platformy Microsoft Azure
Przed są dostępne dane analityczne core hello hello konta magazynu Azure, musisz najpierw narzędzie tooaccess hello zawartość na koncie magazynu. Mimo że rynku hello dostępnych jest kilka narzędzi, hello, który firma Microsoft zaleca jest hello Eksploratora magazynu Microsoft Azure. Możesz pobrać narzędzie hello [tutaj](http://storageexplorer.com/). Po pobieranie i instalowanie oprogramowania hello, skonfiguruj ją toouse hello tego samego konta magazynu Azure, które zostały skonfigurowane jako docelowy toohello dzienników Diagnostyka sieci CDN.

1.  Otwórz **Eksploratora usługi Storage platformy Microsoft Azure**
2.  Zlokalizuj konto magazynu hello
3.  Przejdź toohello **"Kontenerów obiektów Blob"** węźle tego magazynu konta, a następnie rozwiń węzeł hello
4.  Wybierz hello kontener o nazwie **"insights dzienniki coreanalytics"** i kliknij ją dwukrotnie
5.  Wyniki Pokaż się na powitania prawym okienku począwszy hello najpierw poziomu, który wygląda podobnie **"resourceId ="**. Klikaj końca hello aż zostanie wyświetlony plik hello **PT1H.json**. Zobacz powitania po Uwaga wyjaśnienie hello ścieżki.
6.  Każdy obiekt blob **PT1H.json** reprezentuje hello analizy dzienników dla jednej godziny dla określonego punktu końcowego CDN lub jego domeny niestandardowej.
7.  Schemat Hello hello zawartość tego pliku JSON zostało opisane w sekcji hello schematu z hello Core analizy dzienników


> [!NOTE]
> **Format ścieżki obiektu blob**
> 
> Dzienniki Analytics Core są generowane co godzinę. Wszystkie dane przez godzinę są zbierane i przechowywane wewnątrz pojedynczego obiektu Blob Azure jako ładunek JSON. toothis ścieżka Hello obiektów Blob platformy Azure pojawi się tak, jakby to hierarchiczna struktura. Jest ponieważ interpretuje narzędzia Eksplorator magazynu hello "/" jako separatora katalogu, pokazuje hello hierarchii dla wygody. W rzeczywistości hello pełną ścieżkę reprezentuje tylko hello nazwa obiektu blob. Następuje to nazwa obiektu blob hello hello następującą konwencją 
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

**Opis pola:**

|wartość|description|
|-------|---------|
|Identyfikator subskrypcji    |Identyfikator hello subskrypcji platformy Azure. To jest w formacie Guid hello.|
|Zasób |Nazwa grupy zasobów CDN hello toowhich, grupy zasobów hello należą.|
|Nazwa profilu |Nazwa hello profilu CDN|
|Nazwa punktu końcowego |Nazwa hello punktu końcowego CDN|
|Roku|  Reprezentacja 4-cyfrowego roku hello na przykład 2017 r.|
|Miesiąc| Reprezentacja 2-cyfrowy numer miesiąca hello. 01 stycznia =... 12 grudnia =|
|Dzień|   Reprezentacja 2 cyfry hello dzień miesiąca hello|
|PT1H.JSON| Rzeczywisty plik JSON, których są przechowywane dane analizy hello|

### <a name="exporting-hello-core-analytics-data-tooa-csv-file"></a>Eksportowanie hello podstawowe dane analityczne tooa pliku CSV

toomake it łatwe tooaccess hello podstawowa analiza, firma Microsoft udostępnia przykładowy kod dla narzędzia, która umożliwia pobieranie hello pliki w formacie JSON na format pliku płaskim oddzielone przecinkami, które mogą być używane tooeasily Tworzenie wykresów lub innych agregacji.

Oto, jak można użyć narzędzia hello:

1.  Odwiedź hello github łącza: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )
2.  Pobierz kod hello
3.  Postępuj zgodnie z instrukcjami toocompile i skonfigurować
4.  Uruchom narzędzie hello
5.  Wynikowy plik CSV zawiera hello analizy danych w prostych płaskiej hierarchii.

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a>Korzystanie z dzienników diagnostycznych z repozytorium OMS analizy dzienników
Analiza dzienników jest usługą w operacji pakietu zarządzania (OMS), obejmujący z chmury i lokalnych środowiskach toomaintain ich dostępności i wydajności. Zbiera dane generowane przez zasobów w swoich środowiskach w chmurze i lokalnie i z innych monitorowania analizy tooprovide narzędzi w wielu źródeł. 

toouse analizy dzienników, należy najpierw [włączyć rejestrowanie](#enable-logging-with-azure-storage) toohello Analiza dzienników Azure OMS repozytorium, co zostało omówione w tym artykule.

### <a name="using-hello-oms-repository"></a>Przy użyciu hello repozytorium OMS

 diagram przedstawia hello architektura hello danych wejściowych i wyjściowych repozytorium hello Hello:

![Repozytorium analizy dziennika OMS](./media/cdn-diagnostics-log/12_Repo-overview.png)

*Rysunek 3 – repozytorium analizy dzienników*

Można wyświetlić dane hello na różne sposoby, za pomocą rozwiązania do zarządzania. Rozwiązania do zarządzania można uzyskać z hello [portalu Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).

Rozwiązania do zarządzania można zainstalować z portalu Azure marketplace, klikając hello **Pobierz teraz** łącze u dołu hello poszczególnych rozwiązań.

### <a name="adding-an-oms-cdn-management-solution"></a>Dodawanie rozwiązania do zarządzania OMS CDN

Wykonaj te kroki tooadd rozwiązania do zarządzania:

1.   Jeśli jeszcze tego nie zrobiono, zaloguj się toohello portalu Azure przy użyciu subskrypcji platformy Azure i przejdź tooyour pulpitu nawigacyjnego.
    ![Pulpit nawigacyjny platformy Azure](./media/cdn-diagnostics-log/13_Azure-dashboard.png)

2. W hello **nowy** bloku w obszarze **Marketplace**, wybierz pozycję **monitorowanie i zarządzanie**.

    ![Portal Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. W hello **monitorowanie i zarządzanie** bloku, kliknij przycisk **zobaczyć wszystkie**.

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/15_See-all.png)

4.  Wyszukiwanie CDN hello pola wyszukiwania.

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/16_Search-for.png)

5.  Wybierz **usługi Azure CDN podstawowa analiza**. 

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  Po kliknięciu przycisku **Utwórz**, będzie zadawane toocreate nowy obszar roboczy OMS lub użyć istniejącego. 

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  Wybierz obszar roboczy hello utworzone przed. Następnie należy tooadd konto automatyzacji.

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/19_Add-automation.png)

8. Witaj następujący ekran pokazuje hello formularz konta automatyzacji, który musisz wypełnić. 

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/20_Automation.png)

9. Po utworzeniu konta automatyzacji hello są gotowe tooadd rozwiązania. Kliknij przycisk hello **Utwórz** przycisku.

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/21_Ready.png)

10. Rozwiązania teraz dodano tooyour obszaru roboczego. Przejdź wstecz tooyour pulpitu nawigacyjnego portalu Azure.

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/22_Dashboard.png)

    Kliknij obszar roboczy analizy dzienników hello utworzonego obszaru roboczego tooyour toogo. 

11. Kliknij przycisk hello **portalu OMS** Kafelek toosee nowe rozwiązania w portalu OMS hello.

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/23_workspace.png)

12. Portalu OMS powinna wyglądać tak jak po ekranie powitania:

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/24_OMS-solution.png)

    Kliknij jeden z toosee Kafelki hello kilka widoków danych.

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/25_Interior-view.png)

    Można przewijać w lewej lub prawej toosee dalsze Kafelki reprezentujących poszczególnych widoków na powitania dane. 

    Kliknij jeden z fragmentów hello zapewnia szczegółowe informacje o danych.

     ![Zobacz wszystkie](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a>Oferty i warstw cenowych

Możesz wyświetlać oferty i warstw cenowych dla rozwiązań do zarządzania OMS [tutaj](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).

### <a name="customizing-views"></a>Dostosowywanie widoków

Można dostosować widok hello w dane przy użyciu hello **Widok projektanta**. Przejdź tooyour obszarem roboczym pakietu OMS i rozpoczęciu projektowania, klikając hello **Widok projektanta** kafelka.

![Projektant widoków](./media/cdn-diagnostics-log/27_Designer.png)

Można przeciągnij i upuść typów wykresów od lewej hello i wypełnij szczegóły danych hello ma tooanalyze na powitania po lewej.

![Projektant widoków](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a>Opóźnienia dane dziennika

Opóźnienia danych dziennika Verizon | Opóźnienia danych dziennika Akamai
--- | ---
Dane dziennika Verizon jest opóźnione 1 godzina i podjąć toostart godziny too2 pojawiające się po zakończeniu propagowania punktu końcowego. | Dane dziennika Akamai wynosi 24 godziny opóźnienie i zajmuje toostart godziny too2 pojawiające się, jeśli został on utworzony więcej niż 24 godziny temu. Jeśli niedawno został utworzony, może potrwać do godziny too25 toostart dzienniki hello znajdujących się.

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a>Typy dzienników diagnostycznych do sieci CDN w warstwie podstawowa analiza

Firma Microsoft oferuje obecnie tylko podstawowa Analiza dzienników zawierających metryki wyświetlane statystki odpowiedzi HTTP i statystyki wyjście widziany z hello CDN POP/krawędzi.

### <a name="core-analytics-metrics-details"></a>Szczegóły metryki Analytics Core
Hello w poniższej tabeli przedstawiono listę dostępnych w hello podstawowa Analiza dzienników metryk. Nie wszystkie metryki są dostępne z wszystkich dostawców, choć różnice są minimalne. Hello również w poniższej tabeli przedstawiono, czy dana metryka jest dostępna od dostawcy. Należy pamiętać, że metryki hello są dostępne tylko tych punktów końcowych usługi CDN których ruch.


|Metryka                     | Opis   | Verizon  | Akamai 
|---------------------------|---------------|---|---|
| RequestCountTotal         |Całkowita liczba trafień żądania podczas tego okresu.| Tak  |Tak   |
| RequestCountHttpStatus2xx |Liczba wszystkich żądań, które wywołały kod HTTP 2xx (200, 202)              | Tak  |Tak   |
| RequestCountHttpStatus3xx | Liczba wszystkich żądań, które wywołały kod HTTP 3xx (np. 300, 302)              | Tak  |Tak   |
| RequestCountHttpStatus4xx |Liczba wszystkich żądań, które wywołały kod HTTP 4xx (np. 400, 404)               | Tak   |Tak   |
| RequestCountHttpStatus5xx | Liczba wszystkich żądań, które wywołały kod HTTP 5xx (np. 500, 504)              | Tak  |Tak   |
| RequestCountHttpStatusOthers |  Liczba innych kodów HTTP (poza 2xx 5xx) | Tak  |Tak   |
| RequestCountHttpStatus200 | Liczba wszystkich żądań, które spowodowało 200 kod odpowiedzi HTTP              |Nie   |Tak   |
| RequestCountHttpStatus206 | Liczba wszystkich żądań, które wywołały kod odpowiedź HTTP 206              |Nie   |Tak   |
| RequestCountHttpStatus302 | Liczba wszystkich żądań, które spowodowało 302 kod odpowiedzi HTTP              |Nie   |Tak   |
| RequestCountHttpStatus304 |  Liczba wszystkich żądań, które zakończyły się odpowiedź 304 kodu HTTP             |Nie   |Tak   |
| RequestCountHttpStatus404 | Liczba wszystkich żądań, które wywołały kod odpowiedzi HTTP 404              |Nie   |Tak   |
| RequestCountCacheHit |Liczba wszystkich żądań, które zakończyły się liczby trafień pamięci podręcznej. Oznacza to, że zasobów hello zostało obsłużone bezpośrednio z toohello POP powitania klienta.               | Tak  |Nie   |
| RequestCountCacheMiss | Liczba wszystkich żądań, które spowodowało w Chybienie pamięci podręcznej. Oznacza to hello zasobów nie został znaleziony na powitania POP najbliższego toohello klienta i w związku z tym nie została pobrana z hello pochodzenia.              |Tak   | Nie  |
| RequestCountCacheNoCache | Liczba wszystkich żądań zawartości tooan, który uniemożliwił pamięci podręcznej ukończenia konfiguracji użytkownika tooa na powitania krawędzi.              |Tak   | Nie  |
| RequestCountCacheUncacheable | Liczba wszystkich żądań tooassets, który uniemożliwił buforowana przez zasobów hello Cache-Control i wygasa nagłówki, które wskazują, że go mają nie być buforowane punktu obecności lub przez klienta na powitania HTTP                |Tak   |Nie   |
| RequestCountCacheOthers | Liczba wszystkich żądań o stanie pamięci podręcznej nie jest objęty przez powyżej.              |Tak   | Nie  |
| EgressTotal | Transfer danych wychodzących w GB              |Tak   |Tak   |
| EgressHttpStatus2xx | Danych wychodzących transfer * odpowiedzi z kodów stanu HTTP 2xx w GB            |Tak   |Nie   |
| EgressHttpStatus3xx | Transfer danych wychodzących dla odpowiedzi z kodów stanu HTTP 3xx w GB              |Tak   |Nie   |
| EgressHttpStatus4xx | Transfer danych wychodzących dla odpowiedzi z kodów stanu HTTP 4xx w GB               |Tak   | Nie  |
| EgressHttpStatus5xx | Transfer danych wychodzących dla odpowiedzi z kodów stanu HTTP 5xx w GB               |Tak   |  Nie |
| EgressHttpStatusOthers | Transfer danych wychodzących dla odpowiedzi o innych kodach stanów HTTP w GB                |Tak   |Nie   |
| EgressCacheHit |  Transfer danych wychodzących dla odpowiedzi, które zostały dostarczone bezpośrednio z pamięci podręcznej CDN hello na powitania CDN POP/krawędzi  |Tak   |  Nie |
| EgressCacheMiss | Transfer danych wychodzących dla odpowiedzi, które nie zostały znalezione na powitania najbliższy serwer protokołu POP i pobierane z serwera źródłowego hello              |Tak   |  Nie |
| EgressCacheNoCache | Transfer danych wychodzących dla zasobów, które nie będą mogli pamięci podręcznej ukończenia konfiguracji użytkownika tooa na powitania krawędzi.                |Tak   |Nie   |
| EgressCacheUncacheable | Transfer danych wychodzących dla zasobów, które uniemożliwiały buforowana przez Cache-Control hello zasobów i/lub Expires nagłówków, wskazujące, że go mają nie być buforowane punktu obecności lub przez klienta na powitania HTTP                    |Tak   | Nie  |
| EgressCacheOthers |  Transfery danych wychodzących w innych sytuacjach pamięci podręcznej.             |Tak   | Nie  |

* Transfer danych wychodzących odwołuje się tootraffic dostarczone z klienta toohello serwerów POP w sieci CDN.


### <a name="schema-of-hello-core-analytics-logs"></a>Schemat hello Core analizy dzienników 

Wszystkie dzienniki są przechowywane w formacie JSON i każdy wpis ma pól ciągów po hello poniżej schematu:

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of hello CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of hello domain for which hello statistics is reported>",
                "RequestCountTotal": integer value,
                "RequestCountHttpStatus2xx": integer value,
                "RequestCountHttpStatus3xx": integer value,
                "RequestCountHttpStatus4xx": integer value,
                "RequestCountHttpStatus5xx": integer value,
                "RequestCountHttpStatusOthers": integer value,
                "RequestCountHttpStatus200": integer value,
                "RequestCountHttpStatus206": integer value,
                "RequestCountHttpStatus302": integer value,
                "RequestCountHttpStatus304": integer value,
                "RequestCountHttpStatus404": integer value,
                "RequestCountCacheHit": integer value,
                "RequestCountCacheMiss": integer value,
                "RequestCountCacheNoCache": integer value,
                "RequestCountCacheUncacheable": integer value,
                "RequestCountCacheOthers": integer value,
                "EgressTotal": double value,
                "EgressHttpStatus2xx": double value,
                "EgressHttpStatus3xx": double value,
                "EgressHttpStatus4xx": double value,
                "EgressHttpStatus5xx": double value,
                "EgressHttpStatusOthers": double value,
                "EgressCacheHit": double value,
                "EgressCacheMiss": double value,
                "EgressCacheNoCache": double value,
                "EgressCacheUncacheable": double value,
                "EgressCacheOthers": double value,
            }
        }

    ]
}
```

Gdy czas"hello" reprezentuje czas rozpoczęcia hello hello godzina granic, dla którego jest raportowane dane statystyczne hello. Gdy metryki nie jest obsługiwany przez dostawcę sieci CDN w warstwie, a nie wartość o podwójnej precyzji lub liczba całkowita będzie być wartość null. Ta wartość null oznacza braku hello metryki i to różni się od wartości 0. Należy również zauważyć, że będą istnieć jeden zestaw te metryki dla domeny skonfigurowany w punkcie końcowym hello.

Właściwości przykładzie poniżej:

```json
{
     "DomainName": "manlingakamaitest2.azureedge.net",
     "RequestCountTotal": 480,
     "RequestCountHttpStatus2xx": 480,
     "RequestCountHttpStatus3xx": 0,
     "RequestCountHttpStatus4xx": 0,
     "RequestCountHttpStatus5xx": 0,
     "RequestCountHttpStatusOthers": 0,
     "RequestCountHttpStatus200": 480,
     "RequestCountHttpStatus206": 0,
     "RequestCountHttpStatus302": 0,
     "RequestCountHttpStatus304": 0,
     "RequestCountHttpStatus404": 0,
     "RequestCountCacheHit": null,
     "RequestCountCacheMiss": null,
     "RequestCountCacheNoCache": null,
     "RequestCountCacheUncacheable": null,
     "RequestCountCacheOthers": null,
     "EgressTotal": 0.09,
     "EgressHttpStatus2xx": null,
     "EgressHttpStatus3xx": null,
     "EgressHttpStatus4xx": null,
     "EgressHttpStatus5xx": null,
     "EgressHttpStatusOthers": null,
     "EgressCacheHit": null,
     "EgressCacheMiss": null,
     "EgressCacheNoCache": null,
     "EgressCacheUncacheable": null,
     "EgressCacheOthers": null
}

```

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Dzienniki diagnostyczne platformy Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [Podstawowa analiza uzupełniające portalu usługi Azure CDN](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [Analiza dzienników Azure OMS](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [Analiza dzienników Azure interfejsu API REST](https://docs.microsoft.com/en-us/rest/api/loganalytics)







