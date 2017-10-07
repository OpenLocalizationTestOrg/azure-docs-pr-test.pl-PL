---
title: "aaaDesigning wysokiej dostępności aplikacji przy użyciu magazynu geograficznie nadmiarowego Azure dostęp do odczytu (RA-GRS) | Dokumentacja firmy Microsoft"
description: "Jak tooarchitect magazynu Azure RA-GRS toouse aplikacją wysokiej dostępności, elastyczne wystarczającej liczby awarii toohandle."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 8f040b0f-8926-4831-ac07-79f646f31926
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 1/19/2017
ms.author: robinsh
ms.openlocfilehash: e4a9fe7ef33eecd894408b3c1ef59920a248d1bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="designing-highly-available-applications-using-ra-grs"></a>Projektowanie wysokiej dostępności aplikacji przy użyciu RA-GRS

Typową funkcją infrastruktury opartej na chmurze jest zapewniają platformy wysokiej dostępności do obsługi aplikacji. Deweloperzy aplikacji opartych na chmurze należy wziąć pod uwagę dokładnie sposób tooleverage to użytkownicy tootheir platformy toodeliver aplikacje o wysokiej dostępności. Ten artykuł dotyczy w szczególności sposób deweloperzy mogą używać hello Azure magazynu dostęp do odczytu z magazynu geograficznie nadmiarowego magazynu (RA-GRS) toomake ich więcej dostępnych aplikacji.

Istnieją cztery opcje nadmiarowości — LRS (magazyn lokalnie nadmiarowy), ZRS (strefy nadmiarowego magazynu), GRS (magazyn geograficznie nadmiarowy) i RA-GRS (magazyn geograficznie nadmiarowy dostęp do odczytu). Zamierzamy toodiscuss GRS i RA-GRS, w tym artykule. W wypadku magazynu GRS trzy kopie danych są przechowywane w regionie podstawowym hello wybranej podczas konfigurowania hello konta magazynu. Trzy dodatkowe kopie są obsługiwane asynchronicznie w regionie pomocniczym określony przez platformę Azure. RA-GRS jest odpowiednikiem GRS Witaj, z wyjątkiem tego, czy masz dostęp do odczytu toohello pomocniczej kopii. Aby uzyskać więcej informacji na temat hello różnych opcji nadmiarowość magazynu Azure, zobacz [replikacja usługi Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-redundancy). Witaj replikacji artykuł opisuje również skojarzenie hello hello regionów podstawowego i pomocniczego.

Dostępne są zawarte w tym artykule i łącze tooa kompletnego przykładu na końcu hello, który można pobrać i uruchomić wstawki kodu.

## <a name="key-features-of-ra-grs"></a>Najważniejsze funkcje RA-GRS

Przed omawianiu jak toouse magazynu RA-GRS, umożliwia porozmawiać na temat jego właściwości i zachowania.

* Magazyn Azure przechowuje tylko do odczytu kopię hello dane, które są przechowywane w Twoim regionie podstawowym w regionie pomocniczym; jak wspomniano powyżej, usługa Magazyn hello Określa lokalizację hello region pomocniczy hello.

* kopia tylko do odczytu Hello jest [ostatecznie spójne](https://en.wikipedia.org/wiki/Eventual_consistency) z danymi hello w regionie podstawowym hello.

* Dla obiektów blob, tabel i kolejek, można zbadać hello region pomocniczy dla *czas ostatniej synchronizacji* wartość, która informuje, wystąpienia hello ostatniej replikacji z regionu pomocniczego hello toohello głównej. (To nie jest obsługiwana dla usługi Magazyn plików Azure, która nie ma RA-GRS nadmiarowości w tej chwili.)

* Z danych hello w regionie podstawowym lub pomocniczym albo hello służy hello toointeract biblioteki klienta usługi Storage. Możesz również przekierować odczytu automatycznie żądań toohello regionu pomocniczego, jeśli upłynie limit czasu żądania odczytu toohello regionu podstawowego.

* Jeśli jest to główna kwestia wpływu na dostępność hello hello danych w regionie podstawowym hello, hello Azure zespołu mogą wyzwalać geograficznie-trybu failover, w takim przypadku hello wpisy DNS wskazujący regionu podstawowego toohello będzie region pomocniczy toohello toopoint zmienione.

* W przypadku awarię replikacji geograficznej — warstwa Azure będzie wybierz nową lokalizację dodatkowej hello danych toothat lokalizację replikację, a następnie punktu hello dodatkowej tooit wpisy DNS. pomocniczy punkt końcowy Hello będą niedostępne do momentu zakończenia konta magazynu hello replikacji. Aby uzyskać więcej informacji, zobacz [jakie toodo w przypadku wystąpienia awarii usługi Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-disaster-recovery-guidance).

## <a name="application-design-considerations-when-using-ra-grs"></a>Zagadnienia dotyczące projektowania aplikacji przy użyciu RA-GRS

głównym celem niniejszego artykułu Hello jest tooshow należy jak toodesign aplikacji, która będzie toofunction (chociaż są w ograniczonym zakresie), nawet w przypadku hello poważnej awarii w danych pierwotnych hello Centrum. W tym celu o problemów długotrwałe lub przejściowy toohandle aplikacji, na których przełączanie tooread z regionu pomocniczego hello, gdy występuje problem, a następnie ponowne włączenie, gdy regionu podstawowego hello jest ponownie dostępna.

### <a name="using-eventually-consistent-data"></a>Przy użyciu ostatecznie spójność danych

To rozwiązanie proponowanych zakłada, że jej zgadzasz tooreturn co może być aplikacja wywołująca toohello stare dane. Ponieważ dane dodatkowej hello jest ostatecznie spójne, jest możliwe, że hello dane zostały zapisane toohello podstawowy, ale toohello aktualizacji hello dodatkowej miał nie zakończyło się replikowanie podczas regionu podstawowego hello stał się niedostępny.

Na przykład klienta można przesłać aktualizacji, który zakończy się pomyślnie, a następnie hello podstawowego można Przejdź w dół, zanim hello aktualizacji jest propagowany toohello dodatkowej. W tym przypadku jeśli powitania klienta następnie prosi tooread hello ponownie danych, on odbiera dane starych hello zamiast hello zaktualizowane dane. Jeśli jest to dopuszczalne, a jeśli tak, należy zdecydować, w jaki sposób będzie wiadomości powitania klienta. Zobaczysz, jak toocheck hello czas ostatniej synchronizacji na powitania danych pomocniczych w dalszej części tego artykułu toosee Jeśli dodatkowej hello jest aktualny.

### <a name="handling-services-separately-or-all-together"></a>Obsługa usług oddzielnie lub wszystkich elementów

Podczas, gdy jest to prawdopodobnie nie jest możliwe dla toobecome jedna usługa jest niedostępna podczas hello inne usługi są nadal pełni funkcjonalne. Użytkownik może dojście hello prób i trybie tylko do odczytu dla każdego obsługi oddzielnie (obiekty BLOB, kolejek, tabel) lub może obsłużyć ponownych prób objęty dla wszystkich usług magazynu hello razem.

Na przykład użycie kolejek i obiektów blob w aplikacji, można wyłączyć tooput błędy powtarzający operację toohandle oddzielny kod dla każdego z nich. Następnie Jeśli ponowna próba możesz pobrać z usługi blob hello, ale nadal działa usługa kolejki hello, jest ograniczona tylko hello część aplikacji, która obsługuje obiekty BLOB. Jeśli zdecydujesz toohandle wszystkie usługi magazynu ponowi próbę objęty i wywołanie usługi blob toohello zwraca błąd powtarzający operację, a następnie żądań tooboth hello obiektu blob usługi i kolejki hello jest ograniczona.

Ostatecznie zależy od stopnia złożoności hello aplikacji. Może się okazać nie toohandle hello błędów przez usługę, ale zamiast tego tooredirect żądania dla wszystkich usług toohello dodatkowej region magazynu odczytu i uruchomienia aplikacji hello w trybie tylko do odczytu, w przypadku wykrycia problemu z dowolnej usługi magazynu w regionie podstawowym hello.

### <a name="other-considerations"></a>Inne zagadnienia

Są one hello innych kwestii, które omówimy hello dalszej części tego artykułu.

*   Obsługa ponownych prób przy użyciu wzorca wyłącznika hello żądań odczytu

*   Po pewnym czasie spójności danych i hello czas ostatniej synchronizacji

*   Testowanie

## <a name="running-your-application-in-read-only-mode"></a>Uruchamiania aplikacji w trybie tylko do odczytu

toouse magazynu RA-GRS, musi być żądaniami odczytu stanie toohandle zarówno nie powiodło się i nieudane żądania aktualizacji (z aktualizacji w takim przypadku oznacza wstawiania, aktualizacji i usunięć). Jeśli hello centrum danych podstawowych kończy się niepowodzeniem, przeczytaj żądania mogą być przekierowane toohello centrum danych dodatkowej, ale nie żądań aktualizacji, ponieważ dodatkowej hello jest tylko do odczytu. Z tego powodu należy niektórych toorun sposób aplikację w trybie tylko do odczytu.

Na przykład można ustawić flagi, który będzie sprawdzany przed przesłaniem usługi magazynu toohello żądania aktualizacji. Jeśli jedno z żądań aktualizacji hello pochodzi za pośrednictwem, możesz pominąć go i zwraca klienta toohello właściwą odpowiedź. Możesz nawet mają toodisable całkowicie niektórych funkcji, dopóki nie zostanie rozwiązany hello problem i Powiadom użytkowników, że te funkcje są tymczasowo niedostępne.

Jeśli zdecydujesz oddzielnie toohandle błędów dla każdej usługi, należy również toohandle hello możliwości toorun aplikację w trybie tylko do odczytu przez usługę. Może mieć flagi tylko do odczytu dla wszystkich usług, które mogą być włączone, a następnie wyłączone, a uchwyt hello odpowiednie flagi w odpowiednich miejscach hello w kodzie.

Trwa toorun stanie aplikacji w trybie tylko do odczytu ma inny korzyści po stronie — udostępnia tooensure możliwości hello ograniczoną funkcjonalność podczas uaktualniania najważniejszych aplikacji. Możesz wyzwolić toorun Twojej aplikacji w trybie tylko do odczytu trybu i toohello punktu dodatkowej centrum danych, zapewnienie, że nikt nie korzysta z hello danych w regionie podstawowym hello podczas nawiązywania uaktualnienia.

## <a name="handling-updates-when-running-in-read-only-mode"></a>Obsługa aktualizacji w trybie tylko do odczytu

Istnieje wiele sposobów aktualizacji toohandle żądań w trybie tylko do odczytu. Firma Microsoft nie obejmuje to kompleksowe, ale ogólnie rzecz biorąc, istnieje kilka wzorców, które należy wziąć pod uwagę.

1.  Można odpowiadać tooyour użytkownika i poinformuj go, że nie są obecnie akceptuje aktualizacje. Na przykład system zarządzania kontaktami można włączyć informacje kontaktowe tooaccess klientów, ale nie aktualizowanie.

2.  Można umieścić w kolejce aktualizacje w innym regionie. W takim przypadku czy zapisu tooa kolejki żądań oczekujących aktualizacji w innym regionie i mieć tooprocess sposób te żądania po centrum danych podstawowych hello przejściu do trybu online ponownie. W tym scenariuszu należy udostępnić powitania klienta aktualizację hello żądanie przebywa w kolejce do późniejszego przetwarzania.

3.  Aktualizacje można napisać tooa konta magazynu w innym regionie. Jeśli centrum danych podstawowych hello wraca do trybu online, możesz korzystać toomerge sposób aktualizacje do danych pierwotnych hello, w zależności od struktury hello hello danych. Na przykład w przypadku tworzenia oddzielnych plików z sygnaturą daty/godziny w nazwie hello, możesz skopiować te pliki regionu podstawowego toohello Wstecz. Działa to w przypadku niektórych obciążeń, takich jak dane rejestrowania i iOT.

## <a name="handling-retries"></a>Obsługa ponownych prób

Jak ustalić, które błędy są powtarzający operację? Jest to określane za pomocą biblioteki klienta usługi storage hello. Na przykład błąd 404 (nie znaleziono zasobu) nie jest powtarzający operację, ponieważ ponawianie próby jego nie jest prawdopodobnie tooresult w Powodzenie. Na powitania drugiej strony, 500 Błąd jest powtarzający operację, ponieważ jest to błąd serwera i po prostu może być to problem przejściowy. Aby uzyskać więcej informacji, zapoznaj się z hello [Otwórz kod źródłowy hello klasy ExponentialRetry](https://github.com/Azure/azure-storage-net/blob/87b84b3d5ee884c7adc10e494e2c7060956515d0/Lib/Common/RetryPolicies/ExponentialRetry.cs) w hello biblioteki klienta usługi storage platformy .NET. (Poszukaj hello metody ShouldRetry).

### <a name="read-requests"></a>Żądań odczytu

Żądań odczytu może być przekierowane toosecondary magazynu, jeśli występuje problem z magazynem podstawowego. Jak zanotowane powyżej w [przy użyciu ostatecznie spójności danych](#using-eventually-consistent-data), musi być akceptowalne dla twojej aplikacji toopotentially odczytu stare dane. Jeśli używasz hello magazynu klienta biblioteki tooaccess danych RA-GRS, można określić zachowanie ponawiania hello żądania odczytu, ustawiając wartość hello **LocationMode** tooone właściwości hello następującego:

*   **PrimaryOnly** (hello domyślne)

*   **PrimaryThenSecondary**

*   **SecondaryOnly**

*   **SecondaryThenPrimary**

Podczas ustawiania hello **LocationMode** za**PrimaryThenSecondary**, jeśli jest to początkowa hello odczytu podstawowy punkt końcowy toohello żądanie zakończy się niepowodzeniem z powodu błędu powtarzającego operację, powitania klienta automatycznie tworzy innego odczytu żądanie toohello dodatkowej punktu końcowego. Jeśli błąd hello jest limit czasu serwera, następnie powitania klienta będzie mieć toowait dla hello tooexpire limitu czasu przed odbierze błąd powtarzający operację z hello usługi.

Istnieją dwa podstawowe scenariusze tooconsider podczas wybierania się jak Błąd powtarzający operację tooa toorespond:

*   Jest to problem izolowane i podstawowy punkt końcowy toohello kolejne żądania nie zwróci błąd powtarzający operację. Przykładem gdy taka sytuacja może wystąpić jest błąd sieci.

    W tym scenariuszu istnieje żadne pogorszenie wydajności znaczących w o **LocationMode** ustawić także**PrimaryThenSecondary** jak tylko dzieje się rzadko.

*   Jest to problem z co najmniej jednym hello usług magazynu w regionie podstawowym hello i wszystkie kolejne żądania toothat w regionie podstawowym hello są błędy powtarzający operację prawdopodobnie tooreturn w danym okresie czasu. Na przykład jest całkowicie niedostępne hello regionu podstawowego.

    W tym scenariuszu istnieje spadek wydajności, ponieważ wszystkich żądań odczytu zostanie najpierw spróbuj hello podstawowy punkt końcowy, poczekaj, aż hello tooexpire limitu czasu, a następnie przełączyć toohello dodatkowej punktu końcowego.

W tych sytuacjach należy zidentyfikować z trwającej problem z punktem końcowym głównej hello i wysłać wszystkich żądań odczytu bezpośrednio hello toohello dodatkowej punktu końcowego, ustawiając **LocationMode** właściwości zbyt **SecondaryOnly**. W tej chwili możesz również zmienić toorun aplikacji hello w trybie tylko do odczytu. Takie podejście jest nazywany hello [wzorzec wyłącznika](https://msdn.microsoft.com/library/dn589784.aspx).

### <a name="update-requests"></a>Żądań aktualizacji

wzorzec wyłącznika Hello może być również zastosowane tooupdate żądań. Jednak żądania aktualizacji nie może być przekierowany toosecondary magazynu, który jest tylko do odczytu. Dla tych wymagań, należy pozostawić hello **LocationMode** właściwość zbyt**PrimaryOnly** (hello domyślną). toohandle te błędy można zastosować żądania metryki toothese — na przykład 10 błędów w wierszu — i po spełnieniu Twojej próg przełączać aplikacji hello w trybie tylko do odczytu. Można użyć tych samych metod dla zwracania tryb tooupdate, jak te opisane poniżej w następnej sekcji hello o wzorcu wyłącznika hello hello.

## <a name="circuit-breaker-pattern"></a>Wzorzec wyłącznika

Przy użyciu wzorca wyłącznika hello w aplikacji może uniemożliwić ich ponowną próbą wykonania operacji, który jest prawdopodobnie toofail wielokrotnie. Dzięki temu toorun toocontinue aplikacji hello, a nie zajmuje czasu podczas operacji hello jest wykładniczo ponowione. Ta funkcja wykrywa także gdy stałe błędów hello, w którym aplikacja hello czasu można hello spróbuj ponownie wykonać operację.

### <a name="how-tooimplement-hello-circuit-breaker-pattern"></a>Jak tooimplement hello wzorzec wyłącznika

tooidentify czy bieżące problem z podstawowy punkt końcowy, można monitorować, jak często klient hello wystąpią błędy powtarzający operację. Ponieważ każdy przypadek jest inny, masz toodecide na powitania próg mają toouse dla hello decyzji tooswitch toohello dodatkowej endpoint i uruchamiania aplikacji hello w trybie tylko do odczytu. Można na przykład określić tooperform hello przełącznika, jeśli występują błędy 10 w wiersz, w którym nie sukcesów. Innym przykładem jest tooswitch, jeśli 90% hello żądań w okresie 2-minutowy nie powiedzie się.

W przypadku hello pierwszego scenariusza może po prostu przechowuje licznika niepowodzeń hello i w przypadku powodzenia przed osiągnięciem hello toozero wstecz liczba maksymalna, ustaw hello. W scenariuszu drugi hello jednokierunkowej tooimplement jest toouse hello MemoryCache obiektu (.NET). Dla każdego żądania dodać pamięć podręczną toohello niż CacheItem., ustawić hello wartość toosuccess (1) lub zakończyć się niepowodzeniem (0) i ustawić minut too2 czas wygaśnięcia powitania od teraz (lub niezależnie od jest Twoje ograniczenia czasu). Po osiągnięciu czas wygaśnięcia wpisu hello wpis zostanie automatycznie usunięta. Zapewni to stopniowe okna 2-minutowy. Zawsze, gdy należy Usługa Magazyn toohello żądania można najpierw za pomocą zapytań Linq między hello MemoryCache obiektu toocalculate hello procent powodzenia sumowanie wartości hello i podział według liczby hello. Jeśli procent powodzenia hello spadnie poniżej progu, niektóre (na przykład 10%), należy skonfigurować hello **LocationMode** właściwości dla żądań odczytu zbyt**SecondaryOnly** i przełączanie aplikacji hello w trybie tylko do odczytu przed kontynuowanie.

Próg Hello błędów użyto toodetermine toomake hello przełącznika może się różnić od usługi tooservice w aplikacji, więc należy rozważyć, dzięki czemu można konfigurować parametry. Jest to również w przypadku, gdy oddzielnie zdecydujesz toohandle błędów powtarzający operację z każdej usługi lub jako jedna, zgodnie z opisem wcześniej.

Kolejnym zagadnieniem są jak toohandle wiele wystąpień aplikacji i jakie toodo podczas wykrywania błędów powtarzający operację w każdym wystąpieniu. Na przykład może być uruchomiony z załadować samego aplikacji hello 20 maszyn wirtualnych. Czy można obsługiwać każde wystąpienie osobno? Jeśli jedno wystąpienie rozpoczyna się problemy, chcesz toolimit hello odpowiedzi toojust tego jedno wystąpienie lub chcesz tootry toohave wszystkich wystąpień odpowiadają w hello sam sposób, jeśli jedno wystąpienie ma problem? Obsługa wystąpień hello oddzielnie jest znacznie prostsze niż w trakcie odpowiedź hello toocoordinate między nimi, ale jak to zrobić zależy od architektury aplikacji.

### <a name="options-for-monitoring-hello-error-frequency"></a>Opcje monitorowania hello częstotliwość błędów

Możliwe są trzy główne monitorowania hello częstotliwość ponownych prób w regionie podstawowym hello w kolejności toodetermine, gdy tooswitch w regionie pomocniczym toohello i zmień hello toorun aplikacji w trybie tylko do odczytu.

*   Dodaj obsługę hello [ **ponawianie** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.operationcontext.retrying.aspx) zdarzeń na powitania [ **elementu OperationContext** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.operationcontext.aspx) obiekt przekazywania żądań magazynu tooyour — jest to hello Metoda wyświetlane w tym artykule i używane w hello towarzyszące próbki. Te zdarzenia wyzwalać zawsze, gdy klient hello ponawia próbę żądania, umożliwiając jak często tootrack powitania klienta napotka powtarzający operację błędów na podstawowy punkt końcowy.

    ```csharp 
    operationContext.Retrying += (sender, arguments) =>
    {
        // Retrying in hello primary region
        if (arguments.Request.Host == primaryhostname)
            ...
    };
    ```

*   W hello [ **Evaluate** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.retrypolicies.iextendedretrypolicy.evaluate.aspx) metody w zasadach niestandardowych ponownych prób, można uruchomić niestandardowego kodu przy każdym ponowna próba ma miejsce. W przypadku dodawania toorecording przypadku ponowna próba takim również zapewnia hello możliwości toomodify Twojego zachowanie ponów próbę.

    ```csharp 
    public RetryInfo Evaluate(RetryContext retryContext,
    OperationContext operationContext)
    {
        var statusCode = retryContext.LastRequestResult.HttpStatusCode;
        if (retryContext.CurrentRetryCount >= this.maximumAttempts
        || ((statusCode &gt;= 300 && statusCode &lt; 500 && statusCode != 408)
        || statusCode == 501 // Not Implemented
        || statusCode == 505 // Version Not Supported
            ))
        {
        // Do not retry
            return null;
        }

        // Monitor retries in hello primary location
        ...

        // Determine RetryInterval and TargetLocation
        RetryInfo info =
            CreateRetryInfo(retryContext.CurrentRetryCount);

        return info;
    }
    ```

*   Witaj trzeci podejście jest tooimplement niestandardowych składnik monitorowania aplikacji, która stale wysyła pakiet usługi ping punktu końcowego podstawowego magazynu z manekina odczytu toodetermine żądań (takich jak odczytywanie małych obiektów blob) jej kondycji. To może potrwać niektórych zasobów, ale nie znacznej ilości. Gdy problem zostanie odnaleziony, który osiągnie Twojej próg, następnie przeprowadza się przełącznika hello zbyt**SecondaryOnly** i w trybie tylko do odczytu.

W pewnym momencie można tooswitch toousing wstecz hello podstawowy punkt końcowy, dzięki czemu aktualizacji. Jeśli przy użyciu jednej z dwóch pierwszych metod hello wymienionych powyżej, może po prostu przełącznika wstecz toohello podstawowy punkt końcowy i włączyć tryb aktualizacji po przeprowadzono dowolnie wybranego przedziału czasu lub liczba operacji. Następnie można pozostawić ją ponownie przejść przez logikę ponawiania hello. Jeśli hello problem został rozwiązany, utworzy kontynuować podstawowy punkt końcowy toouse hello i zezwolić na aktualizacje. Jeżeli problem nadal występuje, go jeszcze raz Przechodzi wstecz toohello dodatkowej punktu końcowego i trybie tylko do odczytu po nieudanym hello kryteria, które zostały ustawione.

Trzeci scenariusz hello, gdy badanie końcowego podstawowego magazynu hello staje się pomyślnie, możesz wyzwolić hello Wróć za**PrimaryOnly** i kontynuować stosowanie aktualizacji.

## <a name="handling-eventually-consistent-data"></a>Obsługa ostatecznie spójność danych

RA-GRS polega na replikowanie transakcji z regionu pomocniczego hello toohello podstawowego. Ten proces replikacji gwarantuje, że hello danych w regionie pomocniczym hello jest *ostatecznie spójne*. Oznacza to, że wszystkie transakcje hello w regionie podstawowym hello ostatecznie pojawią się w regionie pomocniczym hello, ale może wystąpić opóźnienie przed wyświetleniem i że nie ma żadnej gwarancji transakcji hello przychodzą w regionie pomocniczym hello w porządku takie same jak hello czy w jakiej były pierwotnie stosowane w regionie podstawowym hello. Jeśli transakcje przychodzą w regionie pomocniczym hello poza kolejnością, możesz *może* należy wziąć pod uwagę dane toobe region pomocniczy hello w stanie niespójnym, dopóki usługa hello wyrównania.

Witaj poniższej tabeli przedstawiono przykład co może się zdarzyć, gdy aktualizować hello szczegóły toomake pracownika jej członkiem hello *Administratorzy* roli. Dla zapewnienia hello w tym przykładzie, wymaga aktualizacji hello **pracownika** jednostki i aktualizacji **roli administrator** jednostki wraz z liczbą hello łączna liczba administratorów. Zwróć uwagę, jak hello aktualizacji są stosowane poza kolejnością w regionie pomocniczym hello.

| **Czas** | **Transakcji**                                            | **Replikacja**                       | **Czas ostatniej synchronizacji** | **Wynik** |
|----------|------------------------------------------------------------|---------------------------------------|--------------------|------------| 
| T0       | Transakcja A: <br> Wstaw pracownika <br> jednostki w podstawowej |                                   |                    | Transakcja A dodaje tooprimary,<br> nie jeszcze zreplikowane. |
| T1       |                                                            | Transakcja A <br> Replikacja<br> dodatkowej | T1 | Transakcja A replikowane toosecondary. <br>Czas ostatniej synchronizacji aktualizacji.    |
| T2       | Transakcja B:<br>Aktualizacja<br> Jednostka pracownika<br> w podstawowej  |                                | T1                 | Transakcja B zapisywane tooprimary,<br> nie jeszcze zreplikowane.  |
| T3       | Transakcja C:<br> Aktualizacja <br>Administrator<br>Jednostka roli w<br>podstawowy |                    | T1                 | Transakcja zapisywane tooprimary, C<br> nie jeszcze zreplikowane.  |
| *T4*     |                                                       | Transakcja C <br>Replikacja<br> dodatkowej | T1         | Transakcja C replikowane toosecondary.<br>Nie zaktualizowano ponieważ LastSyncTime <br>Transakcja B nie został jeszcze zreplikowany.|
| *T5*     | Odczyt jednostek <br>pomocniczej                           |                                  | T1                 | Hello jest przestarzała wartość dla pracowników <br> jednostki, ponieważ nie transakcji B <br> jeszcze zreplikowane. Pobierz hello nową wartość<br> Administrator roli jednostki, ponieważ ma C<br> zreplikowane. Czas ostatniej synchronizacji nadal nie.<br> zostały zaktualizowane, ponieważ transakcja B<br> nie replikowane. Można określić<br>Jednostka roli administratora jest niespójna <br>ponieważ po hello jednostek daty/godziny <br>Witaj czas ostatniej synchronizacji. |
| *T6*     |                                                      | Transakcja B<br> Replikacja<br> dodatkowej | T6                 | *T6* — wszystkie transakcje za pomocą C <br>zostały zreplikowane, czas ostatniej synchronizacji<br> jest aktualizowana. |

W tym przykładzie założono powitania klienta przełączniki tooreading z regionu pomocniczego hello w T5. Można pomyślnie odczytać hello **roli administrator** jednostki, w tym momencie, ale jednostki hello zawiera wartość dla liczby hello administratorów nie jest zgodna z liczbą hello **pracownika** jednostek oznaczonych jako administratorów w regionie pomocniczym hello w tej chwili. Klient może po prostu wyświetlaj tej wartości, z ryzykiem hello jest niespójne informacje. Alternatywnie powitania klienta może próbować toodetermine tego hello **roli administrator** jest w stanie potencjalnie niespójności, ponieważ aktualizacje hello wystąpiło poza kolejnością, a następnie powiadamia użytkownika hello o tym fakcie.

toorecognize ma potencjalnie niespójne dane, powitania klienta można użyć wartości hello hello *czas ostatniej synchronizacji* czy można uzyskać w dowolnym momencie przez zapytanie do usługi magazynu. Oznacza to, czas hello podczas ostatniego hello danych w regionie pomocniczym hello spójne i miał stosowania usługi hello hello wszystkie transakcje toothat wcześniejszego punktu w czasie. W powyższym po usługi hello wstawia hello przykład Witaj **pracownika** jednostek w regionie pomocniczym hello, hello czas ostatniej synchronizacji jest ustawiona zbyt*T1*. Pozostaje w *T1* dopóki aktualizacje usługi hello hello **pracownika** jednostki w regionie pomocniczym hello, gdy są zbyt*T6*. Jeśli klient hello pobiera hello czas ostatniej synchronizacji, gdy odczytuje hello jednostki w *T5*, można porównać ją ze znacznikiem czasu hello na powitania jednostki. Jeśli znacznik czasu hello jednostki hello jest nowsza niż hello ostatniej synchronizacji czasu, hello jednostka jest w stanie potencjalnie niespójności i może zająć niezależnie od jest hello odpowiednie działanie aplikacji. To pole wymaga znać ukończenia hello ostatniej aktualizacji toohello podstawowego.

## <a name="testing"></a>Testowanie

Jest ważne tootest, która aplikacja działa zgodnie z oczekiwaniami w przypadku wykrycia błędów powtarzający operację. Na przykład należy tootest, który hello dodatkowej toohello przełączniki aplikacji i w trybie tylko do odczytu wykryje problem, a następnie przełącza z powrotem po regionu podstawowego hello staje się dostępna ponownie. toodo, to należy błędy powtarzający operację toosimulate sposób i kontroli, jak często występują.

Można użyć [Fiddler](http://www.telerik.com/fiddler) toointercept i modyfikowania odpowiedzi HTTP w skrypcie. Ten skrypt można zidentyfikować odpowiedzi, które pochodzą od podstawowego punktu końcowego i zmienić tooone kod stanu HTTP hello powitalne tej biblioteki klienta magazynu jest rozpoznawany jako Błąd powtarzający operację. Następujący fragment kodu przedstawiono prosty przykład skryptu Fiddler, który przechwytuje żądania tooread odpowiedzi przed hello **employeedata** tooreturn tabeli 502 stanu:

```java
static function OnBeforeResponse(oSession: Session) {
    ...
    if ((oSession.hostname == "\[yourstorageaccount\].table.core.windows.net")
      && (oSession.PathAndQuery.StartsWith("/employeedata?$filter"))) {
        oSession.responseCode = 502;
    }
}
```

Można rozszerzyć toointercept ten przykład większej liczby żądań i zmieniać tylko hello **responseCode** na niektórych z nich toobetter symulowania rzeczywistych scenariuszy. Aby uzyskać więcej informacji dotyczących dostosowywania Fiddler skryptów, zobacz [modyfikowanie żądania lub odpowiedzi](http://docs.telerik.com/fiddler/KnowledgeBase/FiddlerScript/ModifyRequestOrResponse) w hello dokumentacji Fiddler.

Jeśli wprowadzono przełączanie aplikacji tylko tooread tryb można skonfigurować progi hello będzie ułatwia zachowanie hello tootest z woluminami transakcji nieprodukcyjnych.

## <a name="next-steps"></a>Następne kroki

* Aby uzyskać więcej informacji o dostęp do odczytu-nadmiarowość geograficzna, łącznie z innym przykładem konfiguracji hello LastSyncTime, zobacz [opcje nadmiarowość magazynu Azure dla systemu Windows i dostęp do odczytu z magazynu geograficznie nadmiarowego magazynu](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/).

* Kompletnego przykładu przedstawiający sposób toomake hello przełącznika i z powrotem między punktami końcowymi podstawowe i pomocnicze hello, zobacz [przykłady Azure — przy użyciu hello wyłącznika wzorca z magazynem RA-GRS](https://github.com/Azure-Samples/storage-dotnet-circuit-breaker-pattern-ha-apps-using-ra-grs).
