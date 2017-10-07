---
title: "aaaIoT strumieni danych w czasie rzeczywistym i usługi Azure Stream Analytics | Dokumentacja firmy Microsoft"
description: "Używanie tagów czujników IoT i strumieni danych z analizą strumieni i przetwarzaniem danych w czasie rzeczywistym"
keywords: "rozwiązanie iot, wprowadzenie do iot"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 3e829055-75ed-469f-91f5-f0dc95046bdb
ms.service: stream-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 422e6b719d0289880aa7f17fdc585e2b768c63d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-stream-analytics-tooprocess-data-from-iot-devices"></a>Wprowadzenie do usługi Azure Stream Analytics tooprocess danych z urządzeń IoT
W tym samouczku przedstawiono sposób toocreate strumienia przetwarzania logiki toogather danych z urządzeń Internetu rzeczy (IoT). Używamy rzeczywistych, toodemonstrate przypadków użycia Internetu rzeczy (IoT) jak toobuild rozwiązania do szybkiego i ekonomicznego.

## <a name="prerequisites"></a>Wymagania wstępne
* [Subskrypcja platformy Azure](https://azure.microsoft.com/pricing/free-trial/)
* Przykładowe pliki zapytań i danych do pobrania z serwisu [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot)

## <a name="scenario"></a>Scenariusz
Contoso, czyli firmy w obszarze automatyzacji przemysłowej hello, ma całkowicie zautomatyzować jego proces produkcji. Hello maszyny w tym zakładzie mają czujniki, z możliwością emitujące strumienie danych w czasie rzeczywistym. W tym scenariuszu Menedżer warsztatu produkcyjnego chce toohave wgląd w czasie rzeczywistym z toolook danych czujnika hello wzorców i podejmowania działań na nich. Używamy hello strumienia Analytics Query Language (SAQL) za pośrednictwem hello czujnik danych toofind interesujących wzorców z hello przychodzącego strumienia danych.

W tym przykładzie dane są generowane z urządzenia Texas Instruments Sensor Tag.

![Urządzenie Texas Instruments Sensor Tag](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-01.jpg)

Witaj ładunku danych hello jest w formacie JSON i wygląda hello:

    {
        "time": "2016-01-26T20:47:53.0000000",  
        "dspl": "sensorE",  
        "temp": 123,  
        "hmdt": 34  
    }  

W rzeczywistym scenariuszu mogą istnieć setki takich czujników generujących zdarzenia jako strumień. Najlepiej, jeśli urządzenie bramy może działać toopush kodu te zdarzenia zbyt[Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) lub [centra IoT Azure](https://azure.microsoft.com/services/iot-hub/). Zadanie Stream Analytics będzie pozyskiwania te zdarzenia z usługi Event Hubs i wykonywania kwerend analiz w czasie rzeczywistym do strumieni hello. Następnie można wysłać hello tooone wyników z hello [obsługiwane dane wyjściowe](stream-analytics-define-outputs.md).

W celu ułatwienia pracy w tym przewodniku z wprowadzeniem udostępniono przykładowy plik danych przechwycony z rzeczywistych urządzeń Sensor Tag. Można uruchomić zapytania na powitania przykładowych danych i wyświetlić wyniki. W kolejnych samouczkach dowiesz się jak tooconnect Twojego zadania tooinputs i danych wyjściowych, a następnie wdrożyć je toohello usługi Azure.

## <a name="create-a-stream-analytics-job"></a>Tworzenie zadania usługi Stream Analytics
1. W hello [portalu Azure](http://portal.azure.com), kliknij znak plus hello, a następnie wpisz **STREAM ANALYTICS** na powitania tekst okna toohello prawo. Następnie wybierz **zadanie usługi Stream Analytics** hello listy wyników.
   
    ![Tworzenie nowego zadania usługi Stream Analytics](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-02.png)
2. Wprowadź nazwę zadania unikatowy i sprawdź subskrypcji hello jest hello właściwy dla zadania. Następnie utwórz nową grupę zasobów lub wybierz istniejącą w subskrypcji.
3. Następnie wybierz lokalizację dla zadania. Szybkość przetwarzania i zmniejszenie kosztów transferu danych, wybierając hello tej samej lokalizacji co konta magazynu zamierzone i grupy zasobów hello jest zalecane.
   
    ![Tworzenie szczegółów nowego zadania usługi Stream Analytics](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03.png)
   
   > [!NOTE]
   > W każdym regionie utwórz to konto magazynu tylko raz. Ten magazyn zostanie udostępniony wszystkim zadaniom usługi Stream Analytics tworzonym w danym regionie.
   > 
   > 
4. Sprawdź tooplace pole hello zadania na pulpicie nawigacyjnym, a następnie kliknij przycisk **Utwórz**.
   
    ![trwa tworzenie zadania](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03a.png)
5. Powinny pojawić się "Wdrażanie rozpoczęte..." wyświetlany w prawym górnym hello okna przeglądarki. Wkrótce zostanie on zmieniony okna tooa ukończone w sposób przedstawiony poniżej.
   
    ![trwa tworzenie zadania](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03b.png)

### <a name="create-an-azure-stream-analytics-query"></a>Tworzenie zapytania usługi Azure Stream Analytics
Gdy zadanie jest utworzony tooopen czas jego i kompilacji zapytania. Zadanie mogli łatwo uzyskiwać dostęp przez kliknięcie kafelka hello go.

![Kafelek zadania](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-04.png)

W hello **topologii zadania** powitania kliknij okienko **zapytania** polu toohello toogo edytora zapytań. Witaj **zapytania** Edytor umożliwia zapytania tooenter T-SQL, które wykonuje przekształcenie hello za pośrednictwem hello danych zdarzeń przychodzących.

![Pole Zapytanie](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-05.png)

### <a name="query-archive-your-raw-data"></a>Zapytanie: archiwizowanie danych pierwotnych
Najprostszą postacią zapytania Hello jest przekazujący zapytanie, które archiwa wszystkich tooits danych wejściowych wyznaczona w danych wyjściowych. Pobierz przykładowy plik danych z hello [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot) tooa lokalizacji na komputerze. 

1. Wklej zapytanie hello z hello PassThrough.txt pliku. 
   
    ![Testowy strumień wejściowy](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06.png)
2. Kliknij przycisk Dalej wejście tooyour hello trzy kropki i wybierz **przekazać dane przykładowe z pliku** pole.
   
    ![Testowy strumień wejściowy](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06a.png)
3. Okienko zostanie otwarty na powitania jako wynik, w ramach tego pliku z lokalizacji pobranego danych wybierz hello HelloWorldASA-InputStream.json i kliknij polecenie **OK** u dołu okienka hello hello.
   
    ![Testowy strumień wejściowy](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06b.png)
4. Następnie kliknij przycisk hello **Test** narzędzi u góry hello hello okna w lewo i przetworzyć zapytania testowego przed hello przykładowego zestawu danych. Okno wyników spowoduje otwarcie poniżej zapytanie przetwarzania hello jest pełny.
   
    ![Wyniki testu](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-07.png)

### <a name="query-filter-hello-data-based-on-a-condition"></a>Zapytanie: Filtrowanie danych hello na podstawie warunku
Spróbujmy toofilter hello wyniki na podstawie warunku. Chcielibyśmy tooshow wyniki tylko te zdarzenia, które pochodzą z czujnika "sensorA". Zapytanie Hello jest hello Filtering.txt pliku.

![Filtrowanie strumienia danych](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-08.png)

Należy pamiętać, że hello zapytania z uwzględnieniem wielkości liter porównuje wartości ciągu. Kliknij przycisk hello **testu** narzędzi ponownie tooexecute hello zapytania. Witaj zapytanie powinno zwrócić 389 wierszy z 1860 zdarzeń.

![Drugi zestaw danych wyjściowych z testu zapytania](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-09.png)

### <a name="query-alert-tootrigger-a-business-workflow"></a>Zapytanie: Alertu tootrigger biznesowego przepływu pracy
Zwiększmy szczegółowość naszego zapytania. Dla każdego typu czujnika firma Microsoft ma toomonitor średnią temperaturę okna 30 sekund i wyświetlać wyniki tylko wtedy, gdy hello średnia temperatura przekracza ona 100 stopni. Firma Microsoft będzie zapisywać hello następujące zapytanie, a następnie kliknij przycisk **testu** toosee hello wyników. Zapytanie Hello jest hello ThresholdAlerting.txt pliku.

![Zapytanie z filtrowaniem co 30 sekund](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-10.png)

Powinna zostać wyświetlona wyniki, które zawierają tylko 245 wierszy i nazwy czujników, w których hello średnia temperatura jest większa niż 100. To zapytanie grup hello strumienia zdarzeń przez **wartości dspl**, powyżej czyli nazwy czujnika hello, **okno wirowania** 30 sekund. Czasowych zapytań musi sposób wyrażania tooprogress czasu. Za pomocą hello **TIMESTAMP BY** klauzuli została określona hello **OUTPUTTIME** kolumny tooassociate czasów wszystkich obliczeń czasowych. Aby uzyskać szczegółowe informacje, zapoznaj się z hello MSDN artykułami o [zarządzanie czasem](https://msdn.microsoft.com/library/azure/mt582045.aspx) i [funkcje okien](https://msdn.microsoft.com/library/azure/dn835019.aspx).

### <a name="query-detect-absence-of-events"></a>Zapytanie: wykrywanie braku zdarzeń
Jak możemy pisać toofind zapytania braku zdarzenia wejściowe? Spróbujmy hello ostatniego czy czujnik wysłał dane, a następnie nie może wysłać zdarzenia hello następnej minuty. Zapytanie Hello jest hello AbsenseOfEvent.txt pliku.

![Wykrywanie braku zdarzeń](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-11.png)

W tym miejscu użyjemy **LEFT OUTER** join toohello strumienia tych samych danych (samosprzężenie). W przypadku sprzężenia **INNER** wynik jest zwracany tylko wtedy, gdy zostanie znalezione dopasowanie.  Aby uzyskać **LEFT OUTER** sprzężenia, jeśli zdarzenie z powitania po lewej stronie powitania sprzężenia jest niedopasowane, wiersza, który ma wartość NULL dla hello wszystkich kolumn prawego hello jest zwracany. Ta technika jest bardzo przydatny toofind braku zdarzeń. Aby uzyskać więcej informacji na temat sprzężenia [JOIN](https://msdn.microsoft.com/library/azure/dn835026.aspx), zobacz dokumentację w witrynie MSDN.

## <a name="conclusion"></a>Podsumowanie
Celem Hello tego samouczka jest toodemonstrate jak toowrite inny język zapytań usługi analiza strumienia zapytania i zobacz powoduje hello przeglądarki. Jest to jednak tylko początek. Za pomocą usługi Stream Analytics można zrobić dużo więcej. Analiza strumienia obsługuje różne wejściami i wyjściami i może nawet Użyj funkcji w usłudze Azure Machine Learning toomake niezawodnego narzędzia do analizy strumieni danych. Więcej informacji na temat usługi Stream Analytics tooexplore można uruchomić za pomocą naszych [mapą nauki](https://azure.microsoft.com/documentation/learning-paths/stream-analytics/). Aby uzyskać więcej informacji o tym, jak toowrite zapytań, przeczytaj artykuł hello o [typowych wzorców zapytań](stream-analytics-stream-analytics-query-patterns.md).

