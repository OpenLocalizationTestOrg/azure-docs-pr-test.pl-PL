---
title: "skalowanie przy użyciu funkcji usługi Azure Stream Analytics & uczenie maszynowe Azure aaaJob | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooproperly skalowanie zadania usługi analiza strumienia (partycjonowania, ilość SU i inne) przy użyciu funkcji usługi Azure Machine Learning."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 47ce7c5e-1de1-41ca-9a26-b5ecce814743
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3fbdfaf7e8e86896c56f1d18bbde3a10bd3dca04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-stream-analytics-job-with-azure-machine-learning-functions"></a>Skalowanie zadania usługi analiza strumienia z funkcjami usługi Azure Machine Learning
Często jest dość łatwe tooset zadania usługi analiza strumienia i uruchamiania przykładowych danych przy jego użyciu. Co możemy zrobić, gdy będzie trzeba toorun hello same zadania o wyższym ilość danych? Wymaga to nam toounderstand jak tooconfigure hello analiza strumienia zadania, dzięki czemu mogą być skalowane. W tym dokumencie możemy koncentruje się na powitania specjalne aspektów skalowania usługi analiza strumienia zadań z funkcji Machine Learning. Aby uzyskać informacje dotyczące sposobu zadania usługi analiza strumienia tooscale ogólnie artykuł hello [skalowanie zadania](stream-analytics-scale-jobs.md).

## <a name="what-is-an-azure-machine-learning-function-in-stream-analytics"></a>Co to jest funkcja uczenie maszynowe Azure w Stream Analytics?
Funkcja uczenia maszynowego w Stream Analytics może służyć jak wywołanie funkcji regularne w hello język zapytań usługi Stream Analytics. Za sceny hello hello wywołania funkcji są faktycznie Usługa sieci Web systemu Azure Machine Learning żądania. Machine Learning w sieci web usług pomocy technicznej "przetwarzanie wsadowe" wiele wierszy, nazywanego mini partii, w hello sam sieci web wywołanie interfejsu API usługi, tooimprove ogólną przepustowość. Zobacz następujące artykuły, aby uzyskać więcej informacji; hello [Funkcji uczenia maszynowego azure Stream Analytics](https://blogs.technet.microsoft.com/machinelearning/2015/12/10/azure-ml-now-available-as-a-function-in-azure-stream-analytics/) i [usługi sieci Web systemu Azure Machine Learning](../machine-learning/machine-learning-consume-web-services.md).

## <a name="configure-a-stream-analytics-job-with-machine-learning-functions"></a>Skonfiguruj zadania usługi analiza strumienia z funkcjami uczenia maszynowego
Podczas konfigurowania funkcji Machine Learning zadania usługi analiza strumienia, istnieją dwa parametry tooconsider, rozmiar partii hello wywołania funkcji Machine Learning hello i hello jednostki (SUs) udostępniane zadania usługi analiza strumienia hello przesyłania strumieniowego. toodetermine hello odpowiednie wartości dla nich, najpierw należy podjąć decyzję między opóźnienia i przepływności, oznacza to, opóźnienie zadania usługi analiza strumienia hello i przepływności każdego SU. SUs zawsze można dodać zadania tooa tooincrease przepływność również podzielone na partycje zapytań usługi Stream Analytics, chociaż dodatkowe SUs zwiększa koszt hello wykonywanym zadaniem hello.

Dlatego jest ważne toodetermine hello *tolerancji* opóźnienia w uruchomienia zadania usługi analiza strumienia. Z rozmiar partii, który będzie złożone hello opóźnienie zadania usługi analiza strumienia hello naturalnie zwiększy się opóźnienie dodatkowych z żądaniami obsługi usługi Azure Machine Learning uruchomiony. Na powitania drugiej strony, zwiększyć rozmiar partii umożliwia tooprocess zadania usługi analiza strumienia hello * więcej zdarzeń o hello *tego samego numeru* z usługi Machine Learning web żądania obsługi. Często hello wzrost opóźnienia usługi sieci web uczenie maszynowe jest toohello podrzędna liniowy wzrost rozmiar partii, dlatego jest ważne tooconsider hello najbardziej ekonomiczne rozmiar wsadu dla usługi sieci web uczenie maszynowe w danej sytuacji. Domyślny rozmiar wsadu dla usługi sieci web hello Hello żądań wynosi 1000, a można modyfikować przy użyciu hello [interfejsu API REST usługi analiza strumienia](https://msdn.microsoft.com/library/mt653706.aspx "interfejsu API REST usługi analiza strumienia") lub hello [klienta programu PowerShell dla usługi Stream Analytics](stream-analytics-monitor-and-manage-jobs-use-powershell.md "klienta programu PowerShell dla usługi Stream Analytics").

Po określeniu rozmiar partii ilość hello przesyłania strumieniowego jednostki (SUs) jest to możliwe, na podstawie hello liczby zdarzeń wymagane przez funkcję hello tooprocess na sekundę. Aby uzyskać więcej informacji na temat jednostek przesyłania strumieniowego, zobacz [Stream Analytics skalowanie zadania](stream-analytics-scale-jobs.md).

Ogólnie rzecz biorąc istnieją 20 równoczesnych połączeń usługę sieci web uczenie maszynowe toohello co 6 SUs z tą różnicą, że zadania SU 1 i 3 zadania SU otrzyma 20 równoczesnych połączeń również.  Na przykład jeśli szybkość danych wejściowych hello jest 200 000 zdarzeń na sekundę i pozostanie rozmiar partii hello domyślną toohello 1000 hello wynikowa sieci web usługi opóźnienia z 1000 zdarzeń mini partii jest 200 ms. Oznacza to, że każdy połączenia mogą wysyłać żądania 5 toohello Machine Learning web service na sekundę. W przypadku połączeń 20 hello zadanie usługi analiza strumienia może przetwarzać 20 000 zdarzeń w 200 MS i w związku z tym 100 000 zdarzeń na sekundę. Dlatego tooprocess 200 000 zdarzeń na sekundę, zadanie usługi Stream Analytics hello musi 40 równoczesnych połączeń, który wychodzi too12 SUs. hello żądania zadania usługi analiza strumienia hello toohello końcowy usługi sieci web uczenie maszynowe przedstawiono na poniższym wykresie Hello — co 6 SUs ma 20 równoczesnych połączeń tooMachine Learning usługi sieci web w max.

![Skalowanie usługi Stream Analytics przykładu zadania Machine Learning funkcje 2](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-00.png "skali Stream Analytics, Machine Learning funkcje 2 zadania przykładu")

Ogólnie rzecz biorąc ***B*** dla rozmiaru partii ***L*** dla hello opóźnienia usługi sieci web na rozmiar partii B w milisekundach, hello przepływności zadanie usługi Stream Analytics z ***N*** SUs jest:

![Skalowanie usługi Stream Analytics formułą funkcji Machine Learning](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-02.png "skalowania usługi Stream Analytics formułą funkcji Machine Learning")

Dodatkowego rozważenia może być hello "max równoczesnych wywołań" na powitania po stronie usługi sieci web uczenie maszynowe, zaleca tooset to maksymalna wartość toohello (obecnie 200).

Aby uzyskać więcej informacji na temat tego ustawienia Przejrzyj hello [artykułu skalowanie dla usługi sieci Web usługi Machine Learning](../machine-learning/machine-learning-scaling-webservice.md).

## <a name="example--sentiment-analysis"></a>Przykład — analizy wskaźniki nastrojów klientów
Witaj poniższy przykład zawiera zadania usługi analiza strumienia z analizą wskaźniki nastrojów klientów hello funkcji Machine Learning, zgodnie z opisem w hello [samouczek integracji usługi Stream Analytics Machine Learning](stream-analytics-machine-learning-integration-tutorial.md).

Witaj zapytanie jest proste zapytanie pełni partycjonowanej następuje hello **wskaźniki nastrojów klientów** funkcji, jak pokazano poniżej:

    WITH subquery AS (
        SELECT text, sentiment(text) as result from input
    )

    Select text, result.[Score]
    Into output
    From subquery

Należy wziąć pod uwagę powitania po scenariusz; o przepustowości 10 000 tweetów na sekundę zadanie usługi Stream Analytics należy utworzyć analizy wskaźniki nastrojów klientów tooperform tweetów hello (zdarzeń). Przy użyciu funkcji 1 SU, to zadanie usługi Stream Analytics można toohandle stanie hello ruchu? Przy użyciu hello domyślny rozmiar wsadu 1000 hello zadania powinna być tookeep stanie się przy użyciu hello danych wejściowych. Dalsze hello dodać funkcji Machine Learning powinna generować ma więcej niż 1 sekunda opóźnienia, czyli hello domyślne Ogólne opóźnienie hello wskaźniki nastrojów klientów analizy usługi sieci web uczenie maszynowe (z domyślny rozmiar partii 1000). zadanie Stream Analytics Hello **ogólną** lub czas oczekiwania na trasie będzie zazwyczaj kilka sekund. Zapoznaj się z bardziej szczegółowe do tego zadania usługi analiza strumienia *szczególnie* hello wywołania funkcji Machine Learning. O rozmiar partii hello jako 1000, przepustowości 10 000 zdarzeń potrwa około 10 żądań tooweb usługi. Nawet w przypadku 1 SU są tooaccommodate wystarczającej liczby równoczesnych połączeń wejściowego ruchu.

Ale co w przypadku występowania zdarzeń wejściowych hello zwiększa 100 x i zadania usługi analiza strumienia hello musi teraz tooprocess tweetów 1 000 000 na sekundę? Dostępne są dwie opcje:

1. Zwiększ rozmiar partii hello, lub
2. Partycja hello strumień wejściowy tooprocess hello zdarzenia równolegle

Z pierwszej opcji hello hello zadania **opóźnienia** wzrośnie.

Z drugą opcją hello SUs więcej będzie konieczne toobe obsługi administracyjnej i w związku z tym Generowanie więcej jednoczesnych żądań usług sieci web uczenie maszynowe. Oznacza to, że zadanie hello **koszt** wzrośnie.

Załóżmy, że opóźnienie hello hello wskaźniki nastrojów klientów analizy usługi sieci web uczenie maszynowe jest 200 ms dla partii zdarzeń 1000 lub poniżej, 250ms partii 5000 zdarzeń, 300ms partii 10 000 zdarzeń lub 500 MS. partii 25 000 zdarzeń.

1. Przy użyciu pierwszej opcji hello (**nie** inicjowania obsługi administracyjnej SUs więcej), rozmiar partii hello można zwiększyć za**25 000**. To z kolei umożliwia tooprocess zadania hello 1 000 000 zdarzeń o toohello 20 równoczesnych połączeń usługi sieci web uczenie maszynowe (z opóźnieniem 500 MS. na wywołanie). Dlatego hello dodatkowe opóźnienia zadanie usługi Stream Analytics hello ukończenia żądania funkcji wskaźniki nastrojów klientów toohello hello uczenia maszynowego żądania usługi sieci web może zostać zwiększona z **200 MS** za**500 MS.**. Jednak należy pamiętać, że rozmiar partii **nie** można zwiększyć nieograniczonej hello usług sieci web uczenie maszynowe wymaga hello rozmiar ładunku żądania 4 MB lub mniejsze sieci web limit czasu żądania usługi 100 sekund operacji.
2. Przy użyciu opcji drugi hello, rozmiar partii hello pozostawiono 1000, z opóźnieniem usługi sieci web 200 MS, każda usługa sieci web toohello 20 równoczesnych połączeń będą mogli tooprocess zdarzenia 1000 * 20 * 5 = 100 000 na sekundę. Dlatego tooprocess 1 000 000 zdarzeń na sekundę, zadanie hello potrzebny 60 SUs. W porównaniu toohello pierwsza opcja, analiza strumienia zadania spowodowałoby więcej żądania sieci web usługi partii, z kolei generowania zwiększenie kosztów.

Poniżej znajduje się tabela przepustowości hello hello zadania usługi analiza strumienia dla różnych SUs i rozmiary partii (w liczbie zdarzeń na sekundę).

| rozmiar partii (ML opóźnienia) | 500 (200 ms) | 1000 (200 ms) | 5000 (250ms) | 10 000 (300ms) | 25 000 (500 MS.) |
| --- | --- | --- | --- | --- | --- |
| **1 SU** |2,500 |5,000 |20,000 |30,000 |50,000 |
| **3 SUs** |2,500 |5,000 |20,000 |30,000 |50,000 |
| **6 SUs** |2,500 |5,000 |20,000 |30,000 |50,000 |
| **12 SUs** |5,000 |10 000 |40,000 |60,000 |100,000 |
| **18 SUs** |7,500 |15,000 |60,000 |90,000 |150,000 |
| **24 SUs** |10 000 |20,000 |80,000 |120,000 |200,000 |
| **…** |… |… |… |… |… |
| **60 SUs** |25,000 |50,000 |200,000 |300,000 |500,000 |

W razie ma już dobrą znajomość jak działają funkcje uczenia maszynowego w Stream Analytics. Prawdopodobnie również rozumiesz, że zadania usługi analiza strumienia "pull" danych ze źródeł danych i każdego "wypychania" zwraca partii zdarzeń hello tooprocess zadania usługi analiza strumienia. Sposób ten model ściągania wpływ żądania usługi sieci web uczenie maszynowe hello?

Rozmiar partii hello ustawione dla funkcji Machine Learning dokładnie będzie zazwyczaj podzielna przez hello liczba zdarzeń zwróconych przez każde zadanie usługi analiza strumienia "ściągania". Gdy to występuje hello usługi sieci web uczenie maszynowe zostanie wywołana partie "częściowej". Jest to realizowane toonot pociągnąć za sobą opóźnienie dodatkowych zadań obciążenie w łączącego zdarzenia z toopull ściągania.

## <a name="new-function-related-monitoring-metrics"></a>Nowe związanych z funkcji monitorowania metryki
W hello obszaru Monitor zadania Stream Analytics zostały dodane trzy dodatkowe metryki dotyczące funkcji. Są one ŻĄDANIA funkcji, zdarzenia funkcji i ŻĄDANIA funkcji nie powiodło się, jak pokazano na rysunku hello poniżej.

![Skalowanie analizy strumienia w usłudze Machine Learning funkcje metryki](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-01.png "analizy strumienia w usłudze Machine Learning funkcje metryki skalowania")

Hello są zdefiniowane w następujący sposób:

**Funkcja ŻĄDANIA**: hello liczba żądań funkcji.

**ZDARZENIA funkcji**: hello numerów zdarzeń w hello funkcji żądania.

**Liczba NIEUDANYCH ŻĄDAŃ funkcja**: hello liczba żądań funkcji zakończonych niepowodzeniem.

## <a name="key-takeaways"></a>Takeaways klucza
toosummarize hello głównych punktów, w kolejności tooscale zadanie usługi Stream Analytics za pomocą funkcji Machine Learning hello następujące elementy należy rozważyć:

1. częstotliwość zdarzenia wejściowego Hello
2. Hello dopuszczalne czas oczekiwania na powitania uruchomione zadanie usługi Stream Analytics (i w związku z tym rozmiar partii hello usługi sieci web uczenie maszynowe hello żądań)
3. Witaj zainicjowano obsługę administracyjną, Stream Analytics SUs i hello liczby żądań usług sieci web uczenie maszynowe (hello dodatkowych funkcji koszty związane z)

Pełni partycjonowanej zapytań usługi Stream Analytics została użyta jako przykład. Jeśli potrzebna jest bardziej złożonego zapytania hello [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) jest doskonałą pomocą podczas uzyskiwania pomocy dodatkowej hello przez zespół usługi Stream Analytics.

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat usługi Stream Analytics, zobacz:

* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)
