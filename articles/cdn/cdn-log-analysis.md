---
title: "Zaloguj się do usługi Azure CDN analizy | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 03ff74ae4e40d3f2279caaf4f73e9b4aac6a2ebb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a>Dzienniki diagnostyczne dla usługi Azure CDN

Po włączeniu sieci CDN w warstwie aplikacji, prawdopodobnie należy do monitorowania użycia sieci CDN w warstwie, Sprawdź kondycję firmy i rozwiązywania potencjalnych problemów. Usługi Azure CDN zapewnia dodatkowe możliwości z [sieci CDN w warstwie podstawowa analiza](cdn-analyze-usage-patterns.md) i [dzienników diagnostycznych](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)

## <a name="cdn-core-analytics"></a>Sieci CDN w warstwie podstawowa analiza
Bieżący użytkownik usługi Azure CDN z Verizon standardowa lub premium profilu masz już możliwość wyświetlania core analytics w portalu uzupełniającym dostępny przy użyciu opcji "Manage" z portalu Azure. 

## <a name="azure-diagnostic-logs"></a>Dzienniki diagnostyczne platformy Azure

Azure przy użyciu tej nowej funkcji, można teraz wyświetlić podstawowa analiza i zapisać je w co najmniej jednego miejsca docelowe, w tym:

 - Konto usługi Azure Storage
 - Azure Event Hubs
 - [Repozytorium OMS analizy dzienników](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 Ta funkcja jest dostępna dla wszystkich punktów końcowych usługi CDN Verizon (Standard i Premium) oraz profilów usługi CDN Akamai (Standard).

Dzienniki diagnostyczne umożliwiają eksportowania metryki użycia podstawowe z punktu końcowego CDN do różnych źródeł, dzięki czemu będzie można korzystać dostosowany sposób. Na przykład można wykonać następujące typy eksportu danych:

- Eksportuj dane do magazynu obiektów blob, Eksportuj do pliku CSV i Generowanie wykresów w formacie programu excel.
- Eksportuj dane do usługi event hubs i skorelowania danych z innymi usługami azure.
- Eksportuj dane do dziennika analizy i wyświetlania danych w własne obszar roboczy OMS

Na poniższej ilustracji przedstawiono typowe przeglądanie sieci CDN w warstwie podstawowa analiza danych.

![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/01_OMS-workspace.png)

*Rysunek 1 — widok sieci CDN w warstwie podstawowa analiza*

Poniższe wskazówki przechodzi przez schemat core analizy danych, etapy włączenie funkcji oraz dostarczania ich do różnych miejsc docelowych i korzystanie z tych miejsc docelowych.

## <a name="enable-logging-with-azure-portal"></a>Włącz rejestrowanie z portalu Azure

> [!NOTE]
> Dzienniki diagnostyczne są włączane **poza** domyślnie. 

Wykonaj poniższe kroki, aby włączyć rejestrowanie z sieci CDN w warstwie podstawowa analiza:

Zaloguj się w witrynie [Azure Portal](http://portal.azure.com). Jeśli nie masz już włączone dla przepływu pracy, w sieci CDN [włączyć usługi Azure CDN](cdn-create-new-endpoint.md) przed kontynuowaniem.

1. W portalu, przejdź do **profilu CDN**.
2. Wybierz profil CDN, a następnie wybierz punkt końcowy CDN, który chcesz włączyć **dzienników diagnostycznych**.

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. Przejdź do **dzienników diagnostycznych** bloku w obszarze **monitorowanie** sekcji, a następnie zmień stan **na**.

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a>Włącz rejestrowanie z usługą Azure Storage
    
Aby używać usługi Azure Storage do przechowywania dzienników, wybierz **archiwum na konto magazynu**, wybierz dni przechowywania i kliknij przycisk **CoreAnalytics** w obszarze **dziennika**.

![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

*Rysunek 2 — rejestrowanie z usługą Azure Storage*

### <a name="logging-with-oms-log-analytics"></a>Rejestrowanie z OMS analizy dzienników

Aby użyć OMS analizy dzienników do przechowywania dzienników, wykonaj następujące kroki:

1. Z **dzienników diagnostycznych** bloku w obszarze **monitorowanie**, wybierz pozycję **wysyłać do analizy dzienników** z 

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. Konfiguruj rejestrowanie analizy dzienników, klikając polecenie Konfiguruj. Zostanie wyświetlone okno dialogowe, w którym poprzedniej obszaru roboczego wybierz lub Utwórz nową.

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. Kliknij przycisk **Utwórz nowy obszar roboczy**.

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/07_Create-new.png)

4. Następnie musisz wybrać nową nazwę obszaru roboczego, istniejącej subskrypcji, grupy zasobów (Nowa lub istniejąca), lokalizacji i warstwę cenową. Dostępna jest opcja kotwiczenia tej konfiguracji do pulpitu nawigacyjnego. Kliknij przycisk OK, aby zakończyć konfigurację.

    Obok obszaru roboczego powinna zostać wyświetlona z nazwami grup obszarem roboczym pakietu OMS i zasobów. Nazwy musi być unikatowa i można używać tylko litery, cyfry i łączniki. Spacje i znaki podkreślenia są niedozwolone. 

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. Otrzymasz obok krótki komunikat informujący, że obszar roboczy użytkownika został utworzony i nastąpi powrót do ekranu Konfiguracja rejestrowania. Można potwierdzić nazwę obszaru roboczego analizy dzienników.

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    Po skonfigurowaniu konfiguracji analizy dzienników upewnij się, że możesz również CoreAnalytics pole wyboru dla rejestracji w sieci CDN.

6. Jeśli wszystko jest Twoim preferencjom, kliknij przycisk **zapisać** przycisk w górnej części okna dialogowego konfiguracji.

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/10_Save-me.png)

    **Zapisać** przycisk nie jest już aktywne i że naciśnięcie przycisku Dalej/OFF jest teraz na, ale blue zamiast purpurowy.

7. Jeśli chcesz wyświetlić nowy obszar roboczy OMS, przejdź do pulpitu nawigacyjnego portalu Azure, kliknij nazwę obszaru roboczego analizy dzienników. Następnie zostanie wyświetlony obszar roboczy (Upewnij się, że obszarem roboczym pakietu OMS są wyróżnione po lewej stronie). Kliknij Kafelek portalu OMS, aby wyświetlić obszar roboczy w repozytorium OMS. 

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    Repozytorium OMS jest teraz gotowy do rejestrowania danych. Aby można było korzystać z tych danych, należy użyć [rozwiązania OMS](#consuming-oms-log-analytics-data), wymienionych w dalszej części tego artykułu.

Więcej informacji na temat opóźnienia danych dziennika [tutaj](#log-data-delays).

## <a name="enable-logging-with-powershell"></a>Włącz rejestrowanie przy użyciu programu PowerShell

Poniżej znajduje się przykład sposobu włączania i pobieranie dzienników diagnostycznych za pomocą poleceń cmdlet programu Azure PowerShell.

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a>Włączanie diagnostyki logowania na koncie magazynu

Zaloguj się najpierw, a następnie wybierz subskrypcję:

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


Aby włączyć dzienniki diagnostyczne na koncie magazynu należy użyć tego polecenia:

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
Aby włączyć dzienniki diagnostyki w obszarze roboczym pakietu OMS należy użyć tego polecenia:

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a>Korzystanie z dzienników diagnostycznych z usługi Azure Storage
W tej sekcji opisano schematu z sieci CDN w warstwie podstawowa analiza, jak te są zorganizowane w ramach konta magazynu platformy Azure i udostępnia przykładowy kod, aby pobrać dzienniki w pliku CSV.

### <a name="using-microsoft-azure-storage-explorer"></a>Za pomocą Eksploratora usługi Storage platformy Microsoft Azure
Przed uzyskujesz dostęp do podstawowych danych analytics z konta magazynu Azure, musisz najpierw narzędzia dostępu do zawartości na koncie magazynu. Gdy brak kilka narzędzi dostępnych na rynku, zaleca się jest Eksploratora magazynu Microsoft Azure. Możesz pobrać narzędzie z [tutaj](http://storageexplorer.com/). Po pobraniu i zainstalowaniu oprogramowania, należy skonfigurować go do używania tego samego konta magazynu Azure, który został skonfigurowany jako miejsce docelowe do dzienników diagnostycznych CDN.

1.  Otwórz **Eksploratora usługi Storage platformy Microsoft Azure**
2.  Zlokalizuj konto magazynu
3.  Przejdź do **"Kontenerów obiektów Blob"** węźle tego magazynu konta, a następnie rozwiń węzeł
4.  Wybierz kontener o nazwie **"insights dzienniki coreanalytics"** i kliknij ją dwukrotnie
5.  Powoduje Pokaż się w okienku po prawej stronie, rozpoczynając od pierwszego poziomu, który wygląda podobnie **"resourceId ="**. Klikaj aż do momentu znajduje się w pliku **PT1H.json**. Zobacz uwagę następujące wyjaśnienie ścieżki.
6.  Każdy obiekt blob **PT1H.json** reprezentuje dzienniki analizy przez godzinę dla określonego punktu końcowego CDN lub jego domeny niestandardowej.
7.  Schemat zawartość tego pliku JSON jest opisany w sekcji schematu Core analizy dzienników


> [!NOTE]
> **Format ścieżki obiektu blob**
> 
> Dzienniki Analytics Core są generowane co godzinę. Wszystkie dane przez godzinę są zbierane i przechowywane wewnątrz pojedynczego obiektu Blob Azure jako ładunek JSON. Ścieżka do tego obiektu Blob Azure jest wyświetlana tak, jakby to hierarchiczna struktura. Jest ponieważ narzędzia Eksplorator magazynu interpretuje "/" jako separatora katalogu, który wyświetla hierarchię jako udogodnienie. W rzeczywistości pełną ścieżkę reprezentuje tylko nazwa obiektu blob. Następuje to nazwa obiektu blob następującej konwencji nazewnictwa   
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

**Opis pola:**

|wartość|Opis elementu|
|-------|---------|
|Identyfikator subskrypcji    |Identyfikator subskrypcji platformy Azure. To jest w formacie Guid.|
|Zasób |Nazwa grupy Nazwa grupy zasobów, do której należą zasoby sieci CDN.|
|Nazwa profilu |Nazwa profilu CDN|
|Nazwa punktu końcowego |Nazwa punktu końcowego CDN|
|Roku|  Reprezentacja 4-cyfrowego roku, na przykład 2017 r.|
|Miesiąc| Reprezentacja 2-cyfrowy numer miesiąca. 01 stycznia =... 12 grudnia =|
|Dzień|   Reprezentacja 2 cyfry dnia miesiąca|
|PT1H.JSON| Rzeczywisty plik JSON, gdzie są przechowywane dane analityczne|

### <a name="exporting-the-core-analytics-data-to-a-csv-file"></a>Eksportowanie danych Analytics Core do pliku CSV

Aby ułatwić dostęp do analizy Core, udostępniamy przykładowy kod dla narzędzia, która umożliwia pobieranie plików JSON na format pliku płaskim przecinkami, który umożliwia łatwe tworzenie wykresów lub innych agregacji.

Oto, jak można użyć narzędzia:

1.  Skorzystaj z łącza github: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )
2.  Pobieranie kodu
3.  Postępuj zgodnie z instrukcjami, aby skompilować i skonfigurować
4.  Uruchom narzędzie
5.  Wynikowy plik CSV zawiera dane analityczne w prosty płaskiej hierarchii.

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a>Korzystanie z dzienników diagnostycznych z repozytorium OMS analizy dzienników
Analiza dzienników jest usługą w operacji pakietu zarządzania (OMS), który monitoruje chmurze i lokalnych środowiskach utrzymywać ich dostępności i wydajności. Zbiera ona dane generowane przez zasoby w środowiskach chmurowych i lokalnych oraz inne narzędzia do monitorowania, aby przeprowadzać analizę na podstawie wielu źródeł. 

Aby korzystać z analizy dzienników, należy najpierw [włączyć rejestrowanie](#enable-logging-with-azure-storage) do repozytorium Analiza dzienników Azure OMS które omówione w tym artykule.

### <a name="using-the-oms-repository"></a>Przy użyciu repozytorium OMS

 Na poniższym diagramie przedstawiono architekturę danych wejściowych i wyjściowych repozytorium:

![Repozytorium analizy dziennika OMS](./media/cdn-diagnostics-log/12_Repo-overview.png)

*Rysunek 3 – repozytorium analizy dzienników*

Dane można wyświetlić w na różne sposoby, za pomocą rozwiązania do zarządzania. Można uzyskać z rozwiązania do zarządzania [portalu Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).

Rozwiązania do zarządzania można zainstalować z portalu Azure marketplace, klikając **Pobierz teraz** łącze u dołu każdego z rozwiązań.

### <a name="adding-an-oms-cdn-management-solution"></a>Dodawanie rozwiązania do zarządzania OMS CDN

Wykonaj następujące kroki, aby dodać rozwiązanie do zarządzania:

1.   Jeśli jeszcze tego nie zrobiono, zaloguj się do portalu Azure przy użyciu subskrypcji platformy Azure i przejdź do pulpitu nawigacyjnego.
    ![Pulpit nawigacyjny platformy Azure](./media/cdn-diagnostics-log/13_Azure-dashboard.png)

2. W **nowy** bloku w obszarze **Marketplace**, wybierz pozycję **monitorowanie i zarządzanie**.

    ![Portal Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. W **monitorowanie i zarządzanie** bloku, kliknij przycisk **zobaczyć wszystkie**.

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/15_See-all.png)

4.  Wyszukiwanie sieci CDN w polu wyszukiwania.

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/16_Search-for.png)

5.  Wybierz **usługi Azure CDN podstawowa analiza**. 

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  Po kliknięciu przycisku **Utwórz**, użytkownik będzie musiał utworzyć nowy obszar roboczy OMS lub użyć istniejącego. 

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  Wybierz obszar roboczy utworzony przed. Następnie należy dodać konto usługi Automatyzacja.

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/19_Add-automation.png)

8. Następujący ekran pokazuje musisz wypełnić formularz konta automatyzacji. 

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/20_Automation.png)

9. Po utworzeniu konta automatyzacji, można przystąpić do dodawania rozwiązania. Kliknij przycisk **Utwórz**.

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/21_Ready.png)

10. Teraz dodano rozwiązania do swojego obszaru roboczego. Wróć do pulpitu nawigacyjnego portalu Azure.

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/22_Dashboard.png)

    Kliknij obszar roboczy analizy dzienników, utworzonego przejdź do obszaru roboczego. 

11. Kliknij przycisk **portalu OMS** Kafelek, aby zobaczyć nowe rozwiązania w portalu OMS.

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/23_workspace.png)

12. Portalu OMS powinna wyglądać tak jak następujący ekran:

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/24_OMS-solution.png)

    Kliknij jeden z fragmentów, aby wyświetlić kilka widoków danych.

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/25_Interior-view.png)

    Po lewej lub prawej strony, aby wyświetlić dalsze Kafelki reprezentujących poszczególnych widoków do danych mogą być przewijane. 

    Kliknij jeden z fragmentów zapewnia szczegółowe informacje o danych.

     ![Zobacz wszystkie](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a>Oferty i warstw cenowych

Możesz wyświetlać oferty i warstw cenowych dla rozwiązań do zarządzania OMS [tutaj](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).

### <a name="customizing-views"></a>Dostosowywanie widoków

Widok danych można dostosować za pomocą **Widok projektanta**. Przejdź do obszaru roboczego OMS i rozpoczęciu projektowania, klikając **Widok projektanta** kafelka.

![Projektant widoków](./media/cdn-diagnostics-log/27_Designer.png)

Można przeciągnąć i upuścić typów wykresów z lewej strony i wypełnij szczegóły danych, które mają być analizowane po lewej stronie.

![Projektant widoków](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a>Opóźnienia dane dziennika

Opóźnienia danych dziennika Verizon | Opóźnienia danych dziennika Akamai
--- | ---
Dane dziennika Verizon 1 godzina opóźnienia i potrwać maksymalnie 2 godziny, aby uruchomić pojawiające się po zakończeniu propagowania punktu końcowego. | Dane dziennika Akamai wynosi 24 godziny, opóźnienia i przejście do 2 godzin Rozpocznij wyświetlaniu, jeśli został on utworzony więcej niż 24 godziny temu. Jeśli niedawno został utworzony, może upłynąć do 25 godzin dzienniki, aby uruchomić wyświetlaniu.

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a>Typy dzienników diagnostycznych do sieci CDN w warstwie podstawowa analiza

Firma Microsoft oferuje obecnie tylko podstawowa Analiza dzienników zawierających metryki wyświetlane statystki odpowiedzi HTTP i statystyki wyjście widziany od obecności CDN/krawędzi.

### <a name="core-analytics-metrics-details"></a>Szczegóły metryki Analytics Core
W poniższej tabeli przedstawiono listę dostępnych w dziennikach podstawowa analiza metryk. Nie wszystkie metryki są dostępne z wszystkich dostawców, choć różnice są minimalne. W poniższej tabeli przedstawiono także, czy dana metryka jest dostępna od dostawcy. Należy pamiętać, że metryki są dostępne tylko tych punktów końcowych usługi CDN których ruchu.


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
| RequestCountCacheHit |Liczba wszystkich żądań, które zakończyły się liczby trafień pamięci podręcznej. Oznacza to, że zasób zostało obsłużone bezpośrednio z punktu obecności do klienta.               | Tak  |Nie   |
| RequestCountCacheMiss | Liczba wszystkich żądań, które spowodowało w Chybienie pamięci podręcznej. Oznacza to zasób nie został znaleziony na POP najbliżej klienta i w związku z tym nie została pobrana z punktu początkowego.              |Tak   | Nie  |
| RequestCountCacheNoCache | Liczba wszystkich żądań do zasobu, uniemożliwiających w pamięci podręcznej z powodu konfiguracji użytkownika na krawędzi.              |Tak   | Nie  |
| RequestCountCacheUncacheable | Liczba wszystkich żądań do zasobów, które uniemożliwiały buforowana przez Cache-Control elementu zawartości i nagłówków wygasa, wskazujące, że go mają nie być buforowane punktu obecności lub przez klienta protokołu HTTP                |Tak   |Nie   |
| RequestCountCacheOthers | Liczba wszystkich żądań o stanie pamięci podręcznej nie jest objęty przez powyżej.              |Tak   | Nie  |
| EgressTotal | Transfer danych wychodzących w GB              |Tak   |Tak   |
| EgressHttpStatus2xx | Danych wychodzących transfer * odpowiedzi z kodów stanu HTTP 2xx w GB            |Tak   |Nie   |
| EgressHttpStatus3xx | Transfer danych wychodzących dla odpowiedzi z kodów stanu HTTP 3xx w GB              |Tak   |Nie   |
| EgressHttpStatus4xx | Transfer danych wychodzących dla odpowiedzi z kodów stanu HTTP 4xx w GB               |Tak   | Nie  |
| EgressHttpStatus5xx | Transfer danych wychodzących dla odpowiedzi z kodów stanu HTTP 5xx w GB               |Tak   |  Nie |
| EgressHttpStatusOthers | Transfer danych wychodzących dla odpowiedzi o innych kodach stanów HTTP w GB                |Tak   |Nie   |
| EgressCacheHit |  Transfer danych wychodzących dla odpowiedzi, które zostały dostarczone bezpośrednio z pamięci podręcznej CDN CDN POP/krawędzi  |Tak   |  Nie |
| EgressCacheMiss | Transfer danych wychodzących dla odpowiedzi, które nie zostały znalezione na najbliższy serwer protokołu POP i pobrać z serwera pochodzenia              |Tak   |  Nie |
| EgressCacheNoCache | Transfer danych wychodzących dla zasobów, które uniemożliwiały pamięci podręcznej z powodu konfiguracji użytkownika na krawędzi.                |Tak   |Nie   |
| EgressCacheUncacheable | Transfer danych wychodzących dla zasobów, które nie będą mogli buforowana przez Cache-Control elementu zawartości i/lub Expires nagłówków, wskazujące, że go mają nie być buforowane punktu obecności lub przez klienta HTTP                    |Tak   | Nie  |
| EgressCacheOthers |  Transfery danych wychodzących w innych sytuacjach pamięci podręcznej.             |Tak   | Nie  |

* Transfer danych wychodzących odwołuje się do ruchu dostarczane z serwerów POP w sieci CDN do klienta.


### <a name="schema-of-the-core-analytics-logs"></a>Schemat Core analizy dzienników 

Wszystkie dzienniki są przechowywane w formacie JSON i każdy wpis ma następujące pola ciągu poniżej schematu:

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of the CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of the domain for which the statistics is reported>",
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

Gdzie "czas" oznacza czas rozpoczęcia granic godzinę, dla którego jest raportowane dane statystyczne. Gdy metryki nie jest obsługiwany przez dostawcę sieci CDN w warstwie, a nie wartość o podwójnej precyzji lub liczba całkowita będzie być wartość null. Tej wartości null wskazuje brak metrykę, a ta różni się od wartości 0. Należy również zauważyć, że będą istnieć jeden zestaw te metryki dla domeny skonfigurowany w punkcie końcowym.

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







