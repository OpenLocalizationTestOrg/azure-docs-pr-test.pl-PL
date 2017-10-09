---
title: "pulpit nawigacyjny usługi BI aaaPower na platformie Azure Stream Analytics | Dokumentacja firmy Microsoft"
description: "Użyj w czasie rzeczywistym przesyłania strumieniowego usługi Power BI pulpitu nawigacyjnego toogather analizy biznesowej i analizować dane dużych zadania usługi analiza strumienia."
keywords: pulpitu nawigacyjnego Analytics, pulpit nawigacyjny w czasie rzeczywistym
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: fe8db732-4397-4e58-9313-fec9537aa2ad
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: jeffstok
ms.openlocfilehash: cb9127576230e9d327b437b674f31cc23869bfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a>Strumienia analizy i usługi Power BI: pulpitu nawigacyjnego analytics w czasie rzeczywistym do strumieniowego przesyłania danych
Usługa Azure Stream Analytics umożliwia tootake zaletą jedną hello wiodące narzędzia do analizy biznesowej, [Microsoft Power BI](https://powerbi.com/). W tym artykule dowiesz się, jak utworzyć przy użyciu usługi Power BI jako dane wyjściowe dla Twojego zadania usługi analiza strumienia Azure narzędzia do analizy biznesowej. Możesz także dowiedzieć się, jak toocreate i pulpit nawigacyjny w czasie rzeczywistym.

Ten artykuł stanowi kontynuację hello Stream Analytics [wykrywanie oszustw w czasie rzeczywistym](stream-analytics-real-time-fraud-detection.md) samouczka. Jego oparty na powitania przepływu pracy utworzone w tym samouczku i dodaje dane wyjściowe, dzięki czemu można zwizualizować fałszywych połączeń telefonicznych, które są wykrywane przez zadanie analizy przesyłania strumieniowego usługi Power BI. 

Możesz obserwować [wideo](https://www.youtube.com/watch?v=SGUpT-a99MA) przedstawiający tego scenariusza.


## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem upewnij się, że masz następujące hello:

* Konto platformy Azure.
* Konto usługi Power BI. Można użyć konta służbowego lub konta służbowego.
* Ukończoną wersję hello [wykrywanie oszustw w czasie rzeczywistym](stream-analytics-real-time-fraud-detection.md) samouczka. Samouczek Hello zawiera aplikację, która generuje metadanych fikcyjne połączeń telefonicznych. W samouczku hello tworzenia Centrum zdarzeń i wysłać hello przesyłania strumieniowego Centrum zdarzeń toohello danych połączenia telefonicznego. Możesz napisać zapytanie wykrywające fałszywych wywołania (wywołania z hello tę samą liczbę na powitania sam czas w różnych lokalizacjach). 


## <a name="add-power-bi-output"></a>Dodawanie danych wyjściowych usługi Power BI
W samouczku wykrywanie oszustw w czasie rzeczywistym hello hello wyjściowe są wysyłane tooAzure magazynu obiektów Blob. W tej sekcji możesz dodać dane wyjściowe, które wysyła informacje tooPower BI.

1. Hello portalu Azure Otwórz hello zadanie analizy przesyłania strumieniowego, utworzony wcześniej. Jeśli używasz hello sugerowana nazwa zadania hello nosi nazwę `sa_frauddetection_job_demo`.

2. Wybierz hello **dane wyjściowe** polu w środku hello hello zadania w pulpicie nawigacyjnym, a następnie wybierz **+ Dodaj**.

3. Aby uzyskać **Alias wyjściowy**, wprowadź `CallStream-PowerBI`. Można użyć innej nazwy. Jeśli to zrobisz, zanotuj, ponieważ potrzebna nazwa hello później. 

4. W obszarze **Sink**, wybierz pozycję **usługi Power BI**.

   ![Utworzenie danych wyjściowych dla usługi Power BI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. Kliknij przycisk **autoryzować**.

    Otwiera okno, w którym można podać poświadczenia platformy Azure dla konta firmowego lub szkolnego. 

    ![Wprowadź poświadczenia dla dostępu tooPower analizy Biznesowej](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. Wprowadź swoje poświadczenia. Należy pamiętać, a następnie wprowadź swoje poświadczenia, użytkownik jest również nadanie tooaccess zadanie analizy przesyłania strumieniowego toohello uprawnień obszaru usługi Power BI.

7. Gdy nastąpi powrót toohello **nowe dane wyjściowe** bloku, wprowadź hello następujących informacji:

    * **Obszar roboczy grupy**: Wybierz obszar roboczy w dzierżawie usługi Power BI miejscu toocreate hello dataset.
    * **Nazwa zestawu danych**: wprowadź `sa-dataset`. Można użyć innej nazwy. Jeśli to zrobisz, zanotuj jej na później.
    * **Nazwa tabeli**: wprowadź `fraudulent-calls`. Obecnie usługa Power BI dane wyjściowe zadania usługi analiza strumienia może mieć tylko jedną tabelę w zestawie danych.

    ![Obszar roboczy PBI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > Usługa Power BI udostępnia zestaw danych hello tabeli, które mają takie same nazwy jako hello te, które określisz w zadaniu Stream Analytics hello, zostaną zastąpione hello istniejące grupy.
    > Zaleca się, że nie jawnie utworzysz ten zestaw danych i tabeli na koncie usługi Power BI. Są one tworzone automatycznie podczas uruchamiania zadania usługi analiza strumienia i hello zadanie uruchamia pompującego dane wyjściowe do usługi Power BI. Jeśli zadania kwerenda nie zwróciła żadnych wyników, hello zestawu danych i tabeli nie są tworzone.
    >

8. Kliknij przycisk **Utwórz**.

zestaw danych Hello jest utworzona z hello następujące ustawienia:

* **defaultRetentionPolicy: BasicFIFO**: dane są FIFO, używając maksymalnie 200 000 wierszy.
* **właściwości defaultMode: pushStreaming**: hello zestawu danych obsługuje przesyłania strumieniowego Kafelki i tradycyjnych elementy wizualne na podstawie raportu () Push).

Obecnie nie można utworzyć zestawy danych z innych flagi.

Aby uzyskać więcej informacji na temat zestawów danych usługi Power BI, zobacz hello [API REST usługi Power BI](https://msdn.microsoft.com/library/mt203562.aspx) odwołania.


## <a name="write-hello-query"></a>Pisanie zapytań hello

1. Zamknij hello **dane wyjściowe** bloku i zwracany toohello bloku zadania.

2. Kliknij przycisk hello **zapytania** pole. 

3. Wprowadź hello następującego zapytania. To zapytanie jest podobne toohello samosprzężenie utworzona kwerenda hello wykrywanie oszustw samouczka. Hello różnicą jest to zapytanie i wysyła wyniki toohello nowe dane wyjściowe utworzonego (`CallStream-PowerBI`). 

    >[!NOTE]
    >Jeśli hello dane wejściowe nie nazwy `CallStream` w samouczku wykrywanie oszustw hello, należy zastąpić nazwę `CallStream` w hello **FROM** i **JOIN** klauzule hello zapytania.

        /* Our criteria for fraud:
        Calls made from hello same caller tootwo phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where hello caller is hello same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where hello switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. Kliknij pozycję **Zapisz**.


## <a name="test-hello-query"></a>Zapytanie hello testu
Ta sekcja jest opcjonalna, ale zalecana. 

1. Jeżeli hello TelcoStreaming aplikacji nie jest obecnie uruchomiona, należy ją uruchomić, wykonując następujące czynności:

    * Otwórz okno poleceń.
    * Przejdź toohello folder zawierający hello telcogenerator.exe i telcodatagen.exe.config zmodyfikowane pliki.
    * Uruchom następujące polecenie hello:

            telcodatagen.exe 1000 .2 2

2. W hello **zapytania** bloku, kliknij przycisk Dalej toohello punktów hello `CallStream` danych wejściowych, a następnie wybierz **przykładowe dane z danych wejściowych**.

3. Określ wartość trzy minuty danych i kliknij przycisk **OK**. Poczekaj, aż zostanie wyświetlone powiadomienie, że hello dane uzyskane podczas próbkowania.

4. Kliknij przycisk **testu** i upewnij się, że otrzymywanie wyników.


## <a name="run-hello-job"></a>Uruchom zadanie hello

1. Upewnij się, że jest uruchomiona, aplikacja TelcoStreaming hello.

2. Zamknij hello **zapytania** bloku.

3. W bloku zadania powitania kliknij **Start**.

    ![Uruchom zadanie usługi Stream Analytics hello](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

Zadanie analizy przesyłania strumieniowego uruchamia wyszukiwanie fałszywych wywołań hello strumienia przychodzącego. zadanie Hello również tworzy hello zestawu danych i tabeli w usłudze Power BI i rozpoczyna wysyłanie danych dotyczących hello toothem fałszywych wywołania.


## <a name="create-hello-dashboard-in-power-bi"></a>Utwórz pulpit nawigacyjny hello w usłudze Power BI

1. Przejdź za[witryny Powerbi.com](https://powerbi.com) i zaloguj się przy użyciu konta służbowego. Jeśli zapytanie zadania usługi analiza strumienia hello zapisuje wyniki, zobacz zestawu danych jest już utworzony:

    ![Zestawu danych przesyłania strumieniowego w usłudze Power BI](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. W obszarze roboczym, kliknij przycisk  **+ &nbsp;Utwórz**.

    ![przycisk Utwórz Hello w obszarze roboczym usługi Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. Utwórz nowy pulpit nawigacyjny i nadaj mu nazwę `Fraudulent Calls`.

    ![Utwórz pulpit nawigacyjny i nadaj mu nazwę w obszarze roboczym usługi Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. U góry okna hello hello, kliknij przycisk **kafelka Dodaj**, wybierz pozycję **danych przesyłania STRUMIENIOWEGO NIESTANDARDOWYCH**, a następnie kliknij przycisk **dalej**.

    ![Niestandardowe przesyłania strumieniowego zestawu danych](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. W obszarze **YOUR DATSETS**, wybierz zestaw danych, a następnie kliknij przycisk **dalej**.

    ![Zestaw danych przesyłania strumieniowego](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. W obszarze **typ wizualizacji**, wybierz pozycję **karty**, a następnie w hello **pola** listy, wybierz **fraudulentcalls**.

    ![Wizualizacja szczegółów dotyczących nowego kafelka](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. Kliknij przycisk **Dalej**.

8. Wprowadź szczegóły kafelka, takie jak tytuł i pomocniczą.

    ![Tytuł i podtytuł dotyczących nowego kafelka](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. Kliknij przycisk **Zastosuj**.

    Teraz masz licznika oszustw.

    ![Licznik oszustwa](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. Witaj wykonaj kroki ponownie tooadd kafelka (począwszy od krok 4). Tym razem hello następujące:

    * Gdy pojawi się zbyt**typ wizualizacji**, wybierz pozycję **wykres liniowy**. 
    * Dodawanie osi i wybierz **windowend**. 
    * Dodaj wartość i wybrać **fraudulentcalls**.
    * Aby uzyskać **toodisplay okno czasu**, wybierz pozycję hello ostatnich 10 minut.

    ![Utwórz Kafelek wykres liniowy](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. Kliknij przycisk **dalej**, Dodaj tytuł i podtytuł i kliknij przycisk **Zastosuj**.

    pulpit nawigacyjny usługi Power BI Hello teraz oferuje dwa widoki danych o wywołaniach fałszywych wykryciu hello strumienia danych.

    ![Zakończono pulpit nawigacyjny usługi Power BI przedstawiający dwa Kafelki dla fałszywych wywołań](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a>Dowiedz się więcej o usłudze Power BI

W tym samouczku przedstawiono sposób toocreate tylko kilka rodzajów wizualizacji dla zestawu danych. Usługa Power BI może pomóc tworzyć inne narzędzia analizy biznesowej odbiorcy w Twojej organizacji. Aby uzyskać więcej informacji zobacz hello następujące zasoby:

* Na przykład innego pulpitu nawigacyjnego usługi Power BI Obejrzyj hello [wprowadzenie do korzystania z usługi Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) wideo.
* Aby uzyskać więcej informacji o konfigurowaniu analizy strumienia zadania tooPower dane wyjściowe BI i przy użyciu usługi Power BI grup, przejrzyj hello [usługi Power BI](stream-analytics-define-outputs.md#power-bi) sekcji hello [analiza strumienia danych wyjściowych](stream-analytics-define-outputs.md) artykułu. 
* Aby dowiedzieć się, jak przy użyciu usługi Power BI, ogólnie rzecz biorąc, zobacz [pulpitów nawigacyjnych w usłudze Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).


## <a name="learn-about-limitations-and-best-practices"></a>Dowiedz się więcej o ograniczeniach oraz najlepsze rozwiązania
Obecnie usługa Power BI można wywołać około raz na sekundę. Elementy wizualne przesyłania strumieniowego obsługuje pakietów 15 KB. Ponadto niepowodzeniem przesyłania strumieniowego elementy wizualne (ale wypychania nadal toowork). Ze względu na ograniczenia te usługi Power BI pozwalają najbardziej naturalnie toocases gdzie Azure Stream Analytics jest zmniejszenie obciążenia dużej ilości danych. Zalecamy używanie okno wirowania lub Hopping okna tooensure czy wypychanie danych jest co najwyżej jeden wypychania na sekundę i czy zapytanie wyładowuje w hello przepływności wymagania.

Program hello po równości toocompute hello wartość toogive okna w sekundach:

![Equation1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

Na przykład:

* Masz 1000 urządzeń wysyłanie danych na sekundę.
* Używasz hello Power BI Pro SKU obsługującego 1 000 000 wierszy na godzinę.
* Ma toopublish hello ilość uśrednianie danych na urządzeniu tooPower BI.

W związku z tym staje się równania hello:

![Equation2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

W takiej konfiguracji można zmienić hello oryginalnego zapytania toohello poniżej:

    SELECT
        MAX(hmdt) AS hmdt,
        MAX(temp) AS temp,
        System.TimeStamp AS time,
        dspl
    INTO "CallStream-PowerBI"
    FROM
        Input TIMESTAMP BY time
    GROUP BY
        TUMBLINGWINDOW(ss,4),
        dspl


### <a name="renew-authorization"></a>Odnów autoryzacji
Jeśli hasło hello uległ zmianie od czasu utworzenia lub ostatniej uwierzytelniony zadania, należy tooreauthenticate Twojego konta usługi Power BI. Jeśli uwierzytelnianie wieloskładnikowe Azure został skonfigurowany w dzierżawie usługi Azure Active Directory (Azure AD), należy również autoryzacji usługi Power BI toorenew co dwa tygodnie. Jeśli nie odnowisz, można zauważyć objawy, takich jak brakujące dane wyjściowe zadania lub `Authenticate user error` w hello dzienników operacji.

Podobnie jeśli zadanie rozpoczyna się po wygaśnięciu tokenu hello, występuje błąd, a zadanie hello zakończy się niepowodzeniem. tooresolve ten problem, Zatrzymaj zadanie hello, którym jest uruchomiony i przejdź tooyour, które dane wyjściowe usługi Power BI. tooavoid utraty danych, wybierz opcję hello **odnowić autoryzacji** połączyć, a następnie uruchom ponownie zadanie z hello **czas ostatniego zatrzymania**.

Po odświeżeniu hello autoryzacji przy użyciu usługi Power BI, zielony alertu pojawi się w tooreflect obszar autoryzacji hello hello problem został rozwiązany.

## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Dokumentacja języka zapytań usługi Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Odwołania API REST zarządzania usługi analiza strumienia Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)
