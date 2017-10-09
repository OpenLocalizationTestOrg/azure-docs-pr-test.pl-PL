---
title: "rejestruje działanie Azure aaaView z analizy dzienników | Dokumentacja firmy Microsoft"
description: "Można użyć hello tooanalyze rozwiązania Azure Dzienniki aktywności i dziennik aktywności platformy Azure hello wyszukiwania wszystkich subskrypcji platformy Azure."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: dbac4c73-0058-4191-a906-e59aca8e2ee0
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.openlocfilehash: 171d0d604d03a5714a9599cc0b448fc5f6471f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="view-azure-activity-logs"></a>Wyświetl dzienniki aktywności platformy Azure

![Symbol Dzienniki aktywności platformy Azure](./media/log-analytics-activity/activity-log-analytics.png)

Witaj rozwiązania analizy dziennika aktywności ułatwiają analizowanie i wyszukaj hello [dziennik aktywności platformy Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) wszystkich subskrypcji platformy Azure. Witaj dziennika aktywności platformy Azure jest dziennika, który oferuje wgląd w operacji hello zasobów w subskrypcji. Witaj dziennik aktywności była wcześniej znana jako *dzienników inspekcji* lub *operacyjne dzienniki* ponieważ raporty zdarzeń dla subskrypcji.

Korzystając z hello dziennik aktywności, można określić hello *co*, *kto*, i *podczas* dla żadnego zapisu (PUT, POST, DELETE) dotyczące hello zasobów w ramach subskrypcji. Można także zrozumieć hello stanu operacji hello i inne odpowiednie właściwości. Hello dziennik aktywności nie obejmuje odczytu (GET) operacje lub operacje dla zasobów korzystających z hello klasycznego modelu wdrożenia.

Podczas łączenia z działanie Azure dzienniki tooLog Analytics można:

- Analizowanie dzienników działania hello ze wstępnie zdefiniowanych widoków
- Analizowanie i dzienniki wyszukiwania i działania z wieloma subskrypcjami platformy Azure
- Zachowaj dzienniki aktywności przez czas dłuższy niż 90 dni<sup>1</sup>
- Dzienniki aktywności jest skorelowany z innych Azure danych platformy i aplikacji
- Zobacz działań operacyjnych w stan
- Wyświetlanie trendów działania wykonywane na każdej z usługami Azure
- Raport dotyczący zmiany autoryzacji na wszystkich zasobów na platformie Azure
- Określenie awarii lub usługa zagadnień dotyczących kondycji wpływu na zasoby
- Użyj aktywności użytkowników toocorrelate wyszukiwania dziennika, wykonanie operacji skalowania automatycznego, zmiany autoryzacji i dzienniki tooother kondycji usługi lub metryk ze środowiska

<sup>1</sup>domyślnie analizy dzienników zachowuje Dzienniki aktywności platformy Azure przez 90 dni, nawet jeśli są w warstwie bezpłatna hello. Lub, jeśli masz obszar roboczy ustawienia przechowywania mniej niż 90 dni. Jeśli obszar roboczy ma przechowywania, która jest dłuższa niż 90 dni, dzienniki aktywności hello są przechowywane przez okres przechowywania hello obszaru roboczego.

Analiza dzienników zbiera Dzienniki aktywności bezpłatne i przechowuje dzienniki hello bezpłatne 90 dni. Jeśli przechowujesz dzienniki przez czas dłuższy niż 90 dni spowoduje naliczenie opłaty przechowywania danych dla danych hello przechowywane dłużej niż 90 dni.

Jeśli jesteś na powitania bezpłatnej warstwy cenowej, dzienniki aktywności nie mają zastosowania do tooyour dzienne zużycie danych.

## <a name="connected-sources"></a>Połączone źródła

W przeciwieństwie do większości innych rozwiązań analizy dzienników danych nie jest zbierane o Dzienniki aktywności przez agentów. Wszystkie dane używane przez rozwiązanie hello pochodzi bezpośrednio z platformy Azure.

| Połączone źródło | Obsługiwane | Opis |
| --- | --- | --- |
| [Agenci dla systemu Windows](log-analytics-windows-agents.md) | Nie | rozwiązanie Hello nie zbiera informacje z agentów systemu Windows. |
| [Agenci dla systemu Linux](log-analytics-linux-agents.md) | Nie | rozwiązanie Hello nie zbiera informacje z agentów systemu Linux. |
| [Grupa zarządzania programu SCOM](log-analytics-om-agents.md) | Nie | rozwiązanie Hello nie zbiera informacje z agentów w podłączonej grupy zarządzania SCOM. |
| [Konto usługi Azure Storage](log-analytics-azure-storage.md) | Nie | rozwiązanie Hello nie zbiera informacje z usługi Azure storage. |

## <a name="prerequisites"></a>Wymagania wstępne

- tooaccess informacje dziennika aktywności platformy Azure, musi mieć subskrypcję platformy Azure.

## <a name="configuration"></a>Konfiguracja

Wykonaj następujące kroki tooconfigure hello analizy dzienników działania rozwiązania dla obszarów roboczych hello.

1. Włącz rozwiązania analizy dziennika aktywności hello z hello [witrynę Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureActivityOMS?tab=Overview) lub za pomocą hello procesu opisanego w temacie [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).
2. Konfigurowanie obszaru roboczego analizy dzienników tooyour toogo Dzienniki aktywności.
    1. W portalu Azure Witaj, wybierz obszar roboczy, a następnie kliknij przycisk **dziennik aktywności platformy Azure**.
    2. Dla każdej subskrypcji kliknij nazwę subskrypcji hello.  
        ![Dodaj subskrypcję](./media/log-analytics-activity/add-subscription.png)
    3. W hello *Nazwa subskrypcji* bloku, kliknij przycisk **Connect**.  
        ![Łączenie subskrypcji](./media/log-analytics-activity/subscription-connect.png)

Jeśli dodasz hello rozwiązania przy użyciu portalu OMS hello, zostanie wyświetlone następujące hello kafelka. Zaloguj się toohello tooconnect portalu Azure obszarem roboczym tooyour subskrypcji platformy Azure.  
![zostanie wykonana oceny](./media/log-analytics-activity/tile-performing-assessment.png)

## <a name="using-hello-solution"></a>Za pomocą rozwiązania hello

Po dodaniu roboczym tooyour rozwiązania analizy dzienników działania hello hello **Dzienniki aktywności Azure** kafelka dodaniu tooyour pulpitu nawigacyjnego przeglądu. Dla hello subskrypcji platformy Azure, które rozwiązanie hello ma dostęp do tego kafelka jest wyświetlana liczba hello liczba rekordów działanie Azure.

![Kafelek Dzienniki aktywności platformy Azure](./media/log-analytics-activity/azure-activity-logs-tile.png)

### <a name="view-azure-activity-logs"></a>Rejestruje działanie usługi Azure widoku

Kliknij hello **Dzienniki aktywności Azure** hello tooopen kafelka **Dzienniki aktywności Azure** pulpitu nawigacyjnego. pulpit nawigacyjny Hello zawiera bloki hello hello w poniższej tabeli. Każdy blok wyświetla się too10 elementów pasujących do kryteriów w bloku hello określenia zakresu zakresu i czasu. Można uruchomić wyszukiwania dziennika, który zwraca wszystkie rekordy, klikając **zobaczyć wszystkie** u dołu hello bloku hello lub przez kliknięcie nagłówka bloku hello.

Dane dziennika aktywności jest wyświetlany tylko *po* skonfigurowaniu rozwiązania toohello toogo Dzienniki aktywności, więc nie można wyświetlić danych, przed upływem.

| Blok | Opis |
| --- | --- |
| Wpisy dziennika aktywności platformy Azure | Przedstawia wykres słupkowy TOP hello wpis dziennika aktywności platformy Azure rekordów sumy dla zakresu dat hello wybrany i pokazuje listę hello top wywołań 10 działania. Kliknij hello toorun wykres słupkowy dziennika wyszukiwanie <code>Type=AzureActivity</code>. Kliknij przycisk wyszukiwania dziennika zwracanie wszystkich wpisów dziennika aktywności dla danego elementu toorun elementu wywołującego. |
| Dzienniki aktywności według stanu | Przedstawia wykres pierścieniowy stanu dziennik aktywności platformy Azure dotyczące hello zakres dat, które zostały wybrane. Również listy to lista hello top stan dziesięć rekordów. Kliknij przycisk wyszukiwania dziennika toorun wykresu hello <code>Type=AzureActivity &#124; measure count() by ActivityStatus</code>. Kliknij przycisk wyszukiwania dziennika zwracanie wszystkich wpisów dziennika aktywności dla niego stan toorun elementu stanu. |
| Dzienniki aktywności przez zasób | Zawiera hello łączna liczba zasobów o Dzienniki aktywności i listę hello pierwszych dziesięciu zasobów z rekordem liczniki dla każdego zasobu. Kliknij toorun całkowity obszar hello dziennika wyszukiwanie <code>Type=AzureActivity &#124; measure count() by Resource</code>, który zawiera wszystkie zasoby platformy Azure toohello dostępne rozwiązania. Kliknij przycisk toorun zasobów wyszukiwania dziennika zwracanie wszystkich rekordów działania dla tego zasobu. |
| Dzienniki aktywności przez dostawcę zasobów | Pokazuje hello łączna liczba dostawców zasobów, które powodują powstanie działania rejestruje i wyświetla hello pierwszych dziesięciu. Kliknij toorun całkowity obszar hello dziennika wyszukiwanie <code>Type=AzureActivity &#124; measure count() by ResourceProvider</code>, który wskazuje wszystkich dostawców zasobów platformy Azure. Kliknij przycisk toorun dostawcy zasobów zwracanie wszystkich rekordów działania hello dostawcy wyszukiwania dziennika. |

![Azure Dzienniki aktywności pulpitu nawigacyjnego](./media/log-analytics-activity/activity-log-dash.png)

## <a name="next-steps"></a>Następne kroki

- Utwórz [alert](log-analytics-alerts-creating.md) po sytuacji określonego działania.
- Użyj [wyszukiwania dziennika](log-analytics-log-searches.md) tooview szczegółowych informacji z dzienników działania.
