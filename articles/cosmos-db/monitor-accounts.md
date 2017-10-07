---
title: "aaaMonitor bazy danych Azure rozwiązania Cosmos żądań i magazynu | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomonitor Twojego Azure DB rozwiązania Cosmos konta metryki wydajności, takich jak żądań i błędów serwera i metryki użycia, takie jak wykorzystania magazynu."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 4c6a2e6f-6e78-48e3-8dc6-f4498b235a9e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: mimig
ms.openlocfilehash: aea029d10717236a573a080dab9d06d87f97f318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-cosmos-db-requests-usage-and-storage"></a>Monitorowanie żądań, użycia i magazynu bazy danych Azure rozwiązania Cosmos
Można monitorować swoje konta bazy danych Azure rozwiązania Cosmos w hello [portalu Azure](https://portal.azure.com/). Dla każdego konta bazy danych Azure rozwiązania Cosmos zarówno metryki wydajności, takich jak żądań i błędów serwera i metryki użycia, takie jak użycia magazynu są dostępne.

Metryki można wyświetlić w bloku konta hello, nowy blok metryki hello, lub w monitorze Azure.

## <a name="view-performance-metrics-on-hello-metrics-blade"></a>Metryki wydajności widoku w bloku metryki hello
1. W hello [portalu Azure](https://portal.azure.com/), kliknij przycisk **więcej usług**, przewiń zbyt**baz danych**, kliknij przycisk **bazy danych Azure rozwiązania Cosmos**, a następnie kliknij przycisk hello nazwę hello Konto platformy Azure DB rozwiązania Cosmos dla którego chcesz tooview metryki wydajności.
2. W menu zasobów hello w obszarze **monitorowanie**, kliknij przycisk **metryki**.

zostanie otwarty blok metryki Hello i można wybrać hello tooreview kolekcji. Można przejrzeć metryki dostępności, żądania przepływności i magazynu i porównaj je toohello Azure rozwiązania Cosmos DB SLA.

## <a name="view-performance-metrics-by-using-azure-monitoring"></a>Metryki wydajności widoku przy użyciu monitorowania Azure
1. W hello [portalu Azure](https://portal.azure.com/), kliknij przycisk **Monitor** na powitania przechodzenia.
2. W menu zasobów hello, kliknij przycisk **metryki**.
3. W hello **Monitor — metryki** okna na powitania **grupy zasobów** menu rozwijanego, grupy zasobów wybierz hello skojarzone z kontem usługi Azure DB rozwiązania Cosmos hello chcesz toomonitor. 
4. W hello **zasobów** menu rozwijanego, toomonitor konta bazy danych wybierz hello.
5. Lista hello **dostępne metryki**, wybierz hello toodisplay metryki. Użyj przycisku CTRL hello toomulti — wybierz. 

    Twoje metryki są wyświetlane na w hello **wykreślenia** okna. 

## <a name="view-performance-metrics-on-hello-account-blade"></a>Metryki wydajności widoku w bloku konta hello
1. W hello [portalu Azure](https://portal.azure.com/), kliknij przycisk **więcej usług**, przewiń zbyt**baz danych**, kliknij przycisk **bazy danych Azure rozwiązania Cosmos**, a następnie kliknij przycisk hello nazwę hello Konto platformy Azure DB rozwiązania Cosmos dla którego chcesz tooview metryki wydajności.
2. Witaj **monitorowanie** obiektyw zawiera następujące Kafelki domyślnie hello:
   
   * Całkowita liczba żądań dla hello bieżącego dnia.
   * Magazyn używany.
   
   Jeśli tabela zawiera **Brak dostępnych danych** i jest danych w bazie danych, zobacz hello [Rozwiązywanie problemów](#troubleshooting) sekcji.
   
   ![Zrzut ekranu przedstawiający obiektyw monitorowanie hello, przedstawiającego hello żądań i hello użycie magazynu](./media/monitor-accounts/documentdb-total-requests-and-usage.png)
3. Kliknięcie hello **żądań** lub **przydział użycia** kafelka otwiera szczegółowe **Metryka** bloku.
4. Witaj **Metryka** bloku są wyświetlane szczegóły dotyczące metryk hello wybrano.  Witaj górnej części bloku hello jest wykres żądań na wykresie co godzinę i poniżej jest tabela, która zawiera wartości agregacji dla żądania z ograniczeniem przepustowości i całkowitej.  Witaj metryki bloku również listą hello alerty, które zostały określone, filtrowane toohello metryki, które pojawiają się w bieżącym bloku metryki hello (dzięki temu, jeśli masz wiele alertów, tylko zobaczysz hello znaczenie przedstawionych w tym miejscu).   
   
   ![Zrzut ekranu przedstawiający blok metryki hello, który zawiera ograniczenie żądań](./media/monitor-accounts/documentdb-metric-blade.png)

## <a name="customize-performance-metric-views-in-hello-portal"></a>Dostosowywanie widoków metryki wydajności w portalu hello
1. toocustomize hello metryk, które na wykresie określonego kliknij tooopen wykresu hello w hello **Metryka** bloku, a następnie kliknij przycisk **Edytuj wykres**.  
   ![Zrzut ekranu przedstawiający hello metryki bloku formantów, Edytuj wykres wyróżnione](./media/monitor-accounts/madocdb3.png)
2. Na powitania **Edytuj wykres** bloku są opcje toomodify hello metryki wyświetlane w hello wykresu, a także ich zakresu czasu.  
   ![Zrzut ekranu przedstawiający blok Edytuj wykres hello](./media/monitor-accounts/madocdb4.png)
3. po prostu wybierz toochange hello metryki wyświetlane w części hello, lub wyczyść hello metryki wydajności dostępne, a następnie kliknij **OK** u dołu hello hello bloku.  
4. toochange hello zakres czasu, wybierz inny zakres (na przykład **niestandardowy**), a następnie kliknij przycisk **OK** u dołu hello hello bloku.  
   
   ![Zrzut ekranu przedstawiający hello zakres czasu część hello Edytuj wykres bloku przedstawiający sposób tooenter niestandardowym zakresie czasu](./media/monitor-accounts/madocdb5.png)

## <a name="create-side-by-side-charts-in-hello-portal"></a>Tworzenie wykresów side-by-side, w portalu hello
Witaj Azure Portal umożliwia toocreate side-by-side metryki wykresy.  

1. Po pierwsze, kliknij prawym przyciskiem myszy wykres hello ma toocopy i zaznacz **Dostosuj**.
   
   ![Zrzut ekranu przedstawiający hello całkowita liczba żądań wykres z wyróżnioną opcją Dostosuj hello](./media/monitor-accounts/madocdb6.png)
2. Kliknij przycisk **klonowania** na hello części hello toocopy menu, a następnie kliknij przycisk **gotowe dostosowywanie**.
   
   ![Ekran zrzut hello wykresu całkowita liczba żądań z hello klonowania i przeprowadzić Dostosowywanie opcji wyróżnione](./media/monitor-accounts/madocdb7.png)  

Ta część może teraz traktować jako drugiej strony metryki, dostosowywanie hello metryki i zakres czasu w hello part.  Dzięki temu widać dwóch różnych metryk wykresu po stronie by-side na powitania tym samym czasie.  
    ![Zrzut ekranu przedstawiający hello całkowita liczba żądań wykresu i hello nowe całkowita liczba żądań poza godziny wykresu](./media/monitor-accounts/madocdb8.png)  

## <a name="set-up-alerts-in-hello-portal"></a>Konfigurowanie alertów w portalu hello
1. W hello [portalu Azure](https://portal.azure.com/), kliknij przycisk **więcej usług**, kliknij przycisk **bazy danych Azure rozwiązania Cosmos**, a następnie kliknij nazwę hello hello Azure DB rozwiązania Cosmos konta, dla którego chcesz toosetup alerty metryki wydajności.
2. W menu zasobów hello, kliknij przycisk **reguły alertów** tooopen hello reguły alertów bloku.  
   ![Zrzut ekranu przedstawiający hello Alert zasady wybrane części](./media/monitor-accounts/madocdb10.5.png)
3. W hello **reguły alertów** bloku, kliknij przycisk **Dodaj alert**.  
   ![Zrzut ekranu przedstawiający blok reguły alertów hello, z wyróżnionym przyciskiem Dodaj alertu hello](./media/monitor-accounts/madocdb11.png)
4. W hello **dodać regułę alertu** bloku, określ:
   
   * Nazwa Hello hello reguły alertów, które konfigurujesz.
   * Opis hello nową regułę alertu.
   * Metryka Hello hello reguły alertów.
   * warunek Hello, próg i okres określające, kiedy aktywuje hello alertu. Na przykład błąd serwera liczba większa niż 5 na powitania ostatnich 15 minut.
   * Określa, czy administrator usługi hello i coadministrators pocztą e-mail po zgłoszeniu alertu hello.
   * Adresy e-mail dodatkowych powiadomień o alertach.  
     ![Zrzut ekranu przedstawiający hello Dodaj blok reguły alertu](./media/monitor-accounts/madocdb12.png)

## <a name="monitor-azure-cosmos-db-programatically"></a>Monitorowanie bazy danych Azure rozwiązania Cosmos programowo
Witaj metryki poziomu konta dostępne w portalu hello, takie jak użycie kont magazynu i wszystkich żądań, nie są dostępne za pośrednictwem hello interfejsów API usługi DocumentDB. Jednak można pobrać dane użycia na poziomie zbioru hello przy użyciu hello interfejsów API usługi DocumentDB. tooretrieve zbierania danych na poziomie, hello następujące:

* Witaj toouse interfejsu API REST, [wykonać operację pobierania na powitania kolekcji](https://msdn.microsoft.com/library/mt489073.aspx). Hello limit przydziału i użycie informacje dla kolekcji hello są zwracane w nagłówkach x-ms-resource przydziału i x-ms-resource użycia hello hello odpowiedzi.
* Witaj toouse zestawu .NET SDK, użyj hello [DocumentClient.ReadDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.readdocumentcollectionasync.aspx) metody, która zwraca [ResourceResponse](https://msdn.microsoft.com/library/dn799209.aspx) takich jak zawiera wiele właściwości użycia  **CollectionSizeUsage**, **DatabaseUsage**, **DocumentUsage**itd.

tooaccess dodatkowe metryki, użyj hello [zestawu SDK platformy Azure Monitor](https://www.nuget.org/packages/Microsoft.Azure.Insights). Dostępne metryki definicje można pobranej poprzez wywołanie:

    https://management.azure.com/subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metricDefinitions?api-version=2015-04-08

Zapytania tooretrieve poszczególnych metryk użycia hello następującego formatu:

    https://management.azure.com/subscriptions/{SubecriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metrics?api-version=2015-04-08&$filter=%28name.value%20eq%20%27Total%20Requests%27%29%20and%20timeGrain%20eq%20duration%27PT5M%27%20and%20startTime%20eq%202016-06-03T03%3A26%3A00.0000000Z%20and%20endTime%20eq%202016-06-10T03%3A26%3A00.0000000Z

Aby uzyskać więcej informacji, zobacz [pobieranie zasobu metryki za pośrednictwem interfejsu API REST Monitor Azure hello](https://blogs.msdn.microsoft.com/cloud_solution_architect/2016/02/23/retrieving-resource-metrics-via-the-azure-insights-api/). Należy pamiętać, że zmieniono nazwę "Azure Inights" "Azure Monitor".  Ten wpis w blogu odwołuje się nazwa starsze toohello.

## <a name="troubleshooting"></a>Rozwiązywanie problemów
Jeśli monitorowanie Kafelki hello wyświetlania **Brak dostępnych danych** komunikat, a ostatnio wprowadzone żądania lub dodać bazy danych toohello danych, można edytować hello kafelka tooreflect hello ostatnie informacje o użyciu.

### <a name="edit-a-tile-toorefresh-current-data"></a>Edytowanie danych bieżącej toorefresh kafelków
1. metryki hello toocustomize, wyświetlanych w określonej części, kliknij przycisk hello wykresu tooopen hello **Metryka** bloku, a następnie kliknij przycisk **Edytuj wykres**.  
   ![Zrzut ekranu przedstawiający hello metryki bloku formantów, Edytuj wykres wyróżnione](./media/monitor-accounts/madocdb3.png)
2. Na powitania **Edytuj wykres** bloku w hello **zakres czasu** kliknij **Ostatnia godzina**, a następnie kliknij przycisk **OK**.  
   ![Zrzut ekranu przedstawiający blok Edytuj wykres hello z ostatniej godziny wybrane](./media/monitor-accounts/documentdb-no-available-data-past-hour.png)
3. Kafelka teraz należy odświeżyć przedstawiający bieżące dane i użycia.  
   ![Zrzut ekranu przedstawiający zaktualizowane hello łączna liczba żądań poza godziny kafelka](./media/monitor-accounts/documentdb-no-available-data-fixed.png)

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat bazy danych Azure rozwiązania Cosmos planowania pojemności, zobacz hello [Kalkulator planowania pojemności bazy danych Azure rozwiązania Cosmos](https://www.documentdb.com/capacityplanner).

