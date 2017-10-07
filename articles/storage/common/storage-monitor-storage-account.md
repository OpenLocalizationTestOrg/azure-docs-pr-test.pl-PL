---
title: "toomonitor aaaHow konta usługi Azure Storage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomonitor konta magazynu na platformie Azure przy użyciu hello portalu Azure."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: b83cba7b-4627-4ba7-b5d0-f1039fe30e78
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: marsma
ms.openlocfilehash: 9a939e0b5db687c1b7b7857399321f681df2056a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-storage-account-in-hello-azure-portal"></a>Monitor konta magazynu w hello portalu Azure

[Analizy usługi Azure Storage](../storage-analytics.md) dostarcza metryki dla wszystkich usług magazynu i dzienniki dla obiektów blob, kolejek i tabel. Można użyć hello [portalu Azure](https://portal.azure.com) tooconfigure dzienniki i metryk, które są rejestrowane dla Twojego konta i skonfiguruj wykresy, które zapewniają wizualnej reprezentacji danych metryki.

> [!NOTE]
> Brak kosztów związanych z badanie danych monitorowania w hello portalu Azure. Aby uzyskać więcej informacji, zobacz [analizy magazynu i rozliczeń](/rest/api/storageservices/Storage-Analytics-and-Billing).
>
> Magazyn plików Azure obecnie obsługuje metryki analityka magazynu, ale jeszcze nie obsługuje rejestrowania.
>
> Konta magazynu z typu replikacji z magazynu Strefowo nadmiarowy (ZRS) aktualnie nie masz metryki hello lub włączona funkcja rejestrowania.
> 
> Szczegółowy przewodnik przy użyciu analizy magazynu i inne narzędzia tooidentify, diagnozowanie i rozwiązywanie problemów związanych z usługą Azure Storage, zobacz [monitorowanie, diagnozowanie i rozwiązywanie problemów z usługi Magazyn Microsoft Azure](../storage-monitoring-diagnosing-troubleshooting.md).
>

## <a name="configure-monitoring-for-a-storage-account"></a>Konfigurowanie monitorowania dla konta magazynu

1. W hello [portalu Azure](https://portal.azure.com), wybierz pozycję **kont magazynu**, a następnie hello magazynu konta Nazwa tooopen hello konta pulpitu nawigacyjnego.
1. Wybierz **diagnostyki** w hello **monitorowanie** sekcji hello menu bloku.

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)

1. Wybierz hello **typu** danych metryki dla każdego **usługi** konieczność toomonitor i hello **zasady przechowywania** hello danych. Można również wyłączyć monitorowanie przez ustawienie **stan** za**poza**.

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-01.png)

   Istnieją dwa typy metryk, które można włączyć dla poszczególnych usług, które są domyślnie włączone dla nowego konta magazynu:

   * **Łączny**: umożliwia zbieranie metryk, takich jak wejście/wyjście, dostępności, opóźnienia i Powodzenie wartości procentowe. Te metryki są agregowane dla hello obiektów blob, kolejki, tabeli i usług plików.
   * **Dla interfejsu API**: W dodanie toohello agregacji metryki zbiera hello tego samego zestawu metryki dla każdej operacji magazynu w hello interfejsu API usługi Azure Storage.

   zasady przechowywania danych tooset hello, Przenieś hello **przechowywania (dni)** suwak lub wprowadź hello liczbę dni tooretain danych, z 1 too365. Witaj domyślne dla nowych kont magazynu wynosi siedem dni. Jeśli nie chcesz, aby tooset zasady przechowywania, wprowadź wartość zero. Jeśli nie ma żadnych zasad przechowywania, działa hello toodelete tooyou danych monitorowania.

   > [!WARNING]
   > Są naliczane, gdy należy ręcznie usunąć dane metryk. System hello bezpłatnie usunięcie danych starych analytics (dane starsze niż zasady przechowywania). Firma Microsoft zaleca ustawienie zasady przechowywania oparte na jak długo mają dane analityczne tooretain magazynu dla Twojego konta. Zobacz [co opłat, czy ponosisz, po włączeniu metryk storage?](../common/storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics) Aby uzyskać więcej informacji.
   >

1. Po zakończeniu konfiguracji monitorowania hello wybierz **zapisać**.

Domyślny zestaw miar jest wyświetlany na wykresach w bloku konto magazynu hello, a także hello pojedynczej usługi bloki (obiektu blob, kolejki, tabel i plików). Po aktywowaniu metryki dla usługi może potrwać do godziny tooan tooappear danych w wykresy. Możesz wybrać **Edytuj** na wszystkie metryki wykresu zbyt[skonfiguruj metrykę, które](#how-to-customize-metrics-charts) są wyświetlane na wykresie hello.

Zbieranie metryk i rejestrowania można wyłączyć, ustawiając **stan** za**poza**.

> [!NOTE]
> Usługa Azure Storage korzysta [tabeli magazynu](../common/storage-introduction.md#table-storage) toostore hello metryki dla konta magazynu i magazyny hello metryki tabel na koncie. Aby uzyskać więcej informacji zobacz. [Jak są przechowywane metryki](../common/storage-analytics.md#how-metrics-are-stored).
>

## <a name="customize-metrics-charts"></a>Dostosowanie metryk wykresów

Użyj hello następujące procedury toochoose które tooview metryki magazynu na wykresie metryki. 

1. Rozpocznij od wyświetlanie wykresu metryki magazynu w hello portalu Azure. Można znaleźć wykresów na powitania **bloku konto magazynu** w hello **metryki** bloku dla poszczególnych usług (obiektu blob, kolejki, tabeli, plik).

   W tym przykładzie współpracujemy z powitania po wykresu, który pojawia się na powitania **bloku konto magazynu**:

   ![Wybór wykresu w portalu Azure](./media/storage-monitor-storage-account/stg-customize-chart-00.png)

1. Następnie kliknij w dowolnym miejscu w hello wykresu tooopen hello **Metryka** bloku. Wybierz **Edytuj wykres** tooopen hello **Edytuj wykres** bloku.

   ![Edytuj przycisk Wykres w bloku wykresu](./media/storage-monitor-storage-account/stg-customize-chart-01.png)

1. Na powitania **Edytuj wykres** bloku, wybierz hello **zakres czasu** z toodisplay metryki hello na wykresie hello i hello **usługi** (obiektu blob, kolejek, tabeli, pliku) metryki, którego chcesz toodisplay. W tym miejscu Wybraliśmy hello toodisplay poza tygodnia metryki dla usługi blob hello:

   ![Wybór zakresu i Usługa czasu w bloku Edytuj wykres hello](./media/storage-monitor-storage-account/stg-customize-chart-02.png)

1. Wybierz hello osoba **metryki** można tak samo, jak gdyby wyświetlany na wykresie hello, kliknij przycisk **OK**. Na przykład, w tym miejscu możemy wybraną toodisplay hello *ContainerCount* i *ObjectCount* metryki:

   ![Poszczególne metryki zaznaczenia w bloku Edytuj wykres](./media/storage-monitor-storage-account/stg-customize-chart-03.png)

Ustawienia wykresu nie dotyczy kolekcji hello, agregacji i magazynu danych na koncie magazynu hello monitorowania, tylko hello wyświetlanie danych metryk.

### <a name="metrics-availability-in-charts"></a>Metryki dostępności na wykresach

Hello listy zmian dostępne metryki oparte na usługi, która została wybrana w hello listy rozwijanej, a typ jednostki hello wykresu hello jest edytowany. Na przykład można wybrać procent metryk, takich jak *PercentNetworkError* i *PercentThrottlingError* tylko wtedy, gdy edycji wykres wyświetlający jednostki w procentach:

![Żądanie błąd wartość procentową wykresu w hello portalu Azure](./media/storage-monitor-storage-account/stg-customize-chart-04.png)

### <a name="metrics-resolution"></a>Rozdzielczość metryk

Hello metryk, które wybrano w diagnostyce Określa rozdzielczość hello hello metryki, które są dostępne dla Twojego konta:

* **Łączny** monitorowania udostępnia metryk, takich jak wejście/wyjście, dostępności, opóźnienia i Powodzenie wartości procentowe. Te metryki są agregowane z hello obiektów blob, tabeli, usług plików i kolejki.
* **Dla interfejsu API** zapewnia bardziej precyzyjną rozpoznawania metryk dostępnych dla operacji magazynu dodatkowo toohello agreguje poziomu usług.

## <a name="configure-metrics-alerts"></a>Konfigurowanie alertów metryk

Można tworzyć alerty toonotify podczas osiągnięto progi dla metryki zasobów magazynu.

1. Witaj tooopen **bloku reguły alertów**, przewiń w dół toohello **monitorowanie** sekcji hello **bloku Menu** i wybierz **reguły alertów**.
1. Wybierz **Dodaj alert** tooopen hello **dodać regułę alertu** bloku
1. Wybierz **zasobów** (obiektu blob, plików, kolejka, tabela) z listy rozwijanej Witaj, a następnie wprowadź **nazwa** i **opis** nowej reguły alertów.
1. Wybierz hello **Metryka** dla którego chcesz tooadd alert, alert **warunku**, a **próg**. Witaj próg jednostki typu różnić w zależności od Metryka hello została wybrana. Na przykład "count" jest typem jednostki hello *ContainerCount*, podczas hello jednostki hello *PercentNetworkError* Metryka to wartość procentową.
1. Wybierz hello **okresu**. Metryki, które osiągną lub przekroczą hello próg w ramach wyzwalacza okresu hello alertu.
1. (Opcjonalnie) Skonfiguruj **E-mail** i **Webhook** powiadomienia. Aby uzyskać więcej informacji dotyczących elementów webhook, zobacz [skonfigurować elementu webhook na alert metryki Azure](../../monitoring-and-diagnostics/insights-webhooks-alerts.md). Jeśli nie zostanie skonfigurowane powiadomienia e-mail lub elementu webhook, alerty będą wyświetlane tylko w hello portalu Azure.

!["Dodaj regułę alertu" bloku w hello portalu Azure](./media/storage-monitor-storage-account/stg-alert-rules-01.png)

## <a name="add-metrics-charts-toohello-portal-dashboard"></a>Dodawanie pulpitu nawigacyjnego portalu toohello wykresy metryk

Wykresy metryk usługi Azure Storage można dodać dla dowolnego magazynu kont tooyour portalu pulpitu nawigacyjnego.

1. Kliknij przycisk Wybierz **edycji pulpitu nawigacyjnego** podczas wyświetlania pulpitu nawigacyjnego w hello [portalu Azure](https://portal.azure.com).
1. W hello **galerii kafelka**, wybierz pozycję **Znajdź Kafelki przez** > **typu**.
1. Wybierz **typu** > **kont magazynu**.
1. W **zasobów**, wybierz konto magazynu hello metryki, którego chcesz tooadd toohello z pulpitu nawigacyjnego.
1. Wybierz **kategorii** > **monitorowania**.
1. Przeciągnij i upuść hello wykresu kafelka na pulpicie nawigacyjnym metryki hello, którą chcesz wyświetlić. Powtórz dla wszystkich metryki którego chciałbyś wyświetlane na pulpicie nawigacyjnym hello. W hello po obrazu zostanie wyróżniona wykresu "Obiekty BLOB — łączna liczba żądań" hello, na przykład, ale wszystkie wykresy hello są dostępne do umieszczenia na pulpicie nawigacyjnym.

   ![Galeria kafelka w portalu Azure](./media/storage-monitor-storage-account/stg-customize-dashboard-01.png)
1. Wybierz **gotowe dostosowywanie** górze hello hello pulpitu nawigacyjnego, gdy użytkownik zakończy dodawanie wykresów.

Po dodaniu pulpitu nawigacyjnego tooyour wykresy, można dostosować je zgodnie z opisem w [dostosowanie metryk wykresy](#how-to-customize-metrics-charts).

## <a name="configure-logging"></a>Konfigurowanie rejestrowania

Możesz wydać dzienników diagnostycznych toosave usługi Azure Storage dla odczytu, zapisu i usuwania żądania hello obiektów blob, tabel i usługi kolejkowania. zasady przechowywania danych Hello ustawionych ma również zastosowanie toothese dzienniki.

> [!NOTE]
> Magazyn plików Azure obecnie obsługuje metryki analityka magazynu, ale jeszcze nie obsługuje rejestrowania.
>

1. W hello [portalu Azure](https://portal.azure.com), wybierz pozycję **kont magazynu**, nazwę konta magazynu hello tooopen bloku konto magazynu hello hello.
1. Wybierz **diagnostyki** w hello **monitorowanie** sekcji hello menu bloku.

    ![Diagnostyka elementu menu w obszarze monitorowania w hello portalu Azure.](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)
    
1. Upewnij się, **stan** ustawiono zbyt**na**i wybierz hello **usług** dla którego chcesz tooenable rejestrowania.

    ![Konfigurowanie rejestrowania w hello portalu Azure.](./media/storage-monitor-storage-account/stg-enable-logging-01.png)
1. Kliknij pozycję **Zapisz**.

dzienniki diagnostyczne Hello są zapisywane w kontenerze obiektu blob o nazwie $logs na koncie magazynu. Można wyświetlić dane dziennika hello za pomocą Eksploratora magazynu, takich jak hello [Eksploratora magazynu](http://storageexplorer.com), albo programowo z użyciem biblioteki klienta usługi storage hello lub programu PowerShell.

Informacje dotyczące uzyskiwania dostępu do kontenera hello $logs, zobacz [Włączanie rejestrowania magazynu i uzyskiwanie dostępu do danych dziennika](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data).

## <a name="next-steps"></a>Następne kroki

* Uzyskać więcej informacji na temat [metryki, rejestrowania i rozliczeń](../storage-analytics.md) analizy magazynu.
* [Włącz dane metryk usługi Azure Storage metryki i widoku](../storage-enable-and-view-metrics.md) przy użyciu programu PowerShell i programowo w języku C#.
