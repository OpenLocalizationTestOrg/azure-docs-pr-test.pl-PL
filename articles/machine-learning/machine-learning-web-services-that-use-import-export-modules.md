---
title: "aaaUsing importowania i eksportowania danych w usługach sieci web Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello toosend moduły danych importowanie i eksportowanie danych i odbierać dane z usługi sieci web."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3a7ac351-ebd3-43a1-8c5d-18223903d08e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 176380259b15cb338ede61c7f28ba2296b35dd52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a>Wdrażanie usług sieci Web Azure ML używających modułów importu i eksportu danych

Po utworzeniu eksperyment predykcyjny zazwyczaj są dodawane usługi sieci web w danych wejściowych i wyjściowych. Podczas wdrażania eksperymentu hello konsumentów może wysyłać i odbierać dane z usługi sieci web hello za pośrednictwem hello wejścia i wyjścia. Dla pewnych aplikacji danych klientów mogą być dostępne ze strumieniowego źródła danych lub już znajdują się w źródle danych zewnętrznych, takie jak magazyn obiektów Blob platformy Azure. W takich przypadkach nie potrzebują oni odczytywanie i zapisywanie danych przy użyciu sieci web usługi wejścia i wyjścia. Mogą, zamiast tego użyj hello usługi wykonywania wsadowego (BES) tooread danych ze źródła danych hello za pomocą modułu i zaimportuj dane i zapisać hello oceniania wyników tooa różnych danych lokalizacji za pomocą modułu eksportu danych.

Hello importowanie danych i moduły danych eksportu, można odczytywać i zapisać dane toovarious, na przykład adres URL sieci Web za pośrednictwem protokołu HTTP, zapytanie Hive, bazy danych Azure SQL, Magazyn tabel Azure, magazynu obiektów Blob platformy Azure, strumieniowego źródła danych zawierają lub lokalną bazą danych SQL.

W tym temacie używa hello "próbki 5: Evaluate pociągu, testu, klasyfikacji binarnej: dla dorosłych zestawu danych" przykładowe i zakłada hello zestaw danych został już załadowany do tabeli Azure SQL o nazwie censusdata.

## <a name="create-hello-training-experiment"></a>Tworzenie eksperymentu uczenia hello
Po otwarciu hello "próbki 5: Evaluate pociągu, testu, klasyfikacji binarnej: dla dorosłych zestawu danych" Przykładowe go używa hello próbki dla dorosłych klasyfikacji binarnej dochodu spisu w zestawie danych. I eksperymentu hello kanwie hello będzie wyglądać podobnie toohello po obrazu:

![Wstępna konfiguracja hello eksperymentu.](./media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

tooread hello danych z tabeli Azure SQL hello:

1. Usuń hello modułu zestawu danych.
2. W polu wyszukiwania składników hello wpisz importu.
3. Z listy wyników hello, Dodaj *i zaimportuj dane* kanwy eksperymentu toohello modułu.
4. Połącz dane wyjściowe hello *i zaimportuj dane* danych wejściowych hello modułu hello *Clean Missing Data* modułu.
5. W okienku właściwości, wybierz **bazy danych SQL Azure** w hello **źródła danych** listy rozwijanej.
6. W hello **nazwę serwera bazy danych**, **Nazwa bazy danych**, **nazwy użytkownika**, i **hasło** wprowadź odpowiednie informacje powitalnych dla bazy danych.
7. W polu kwerendy bazy danych hello wprowadzić hello następującego zapytania.
   
     Wybierz [wieku]
   
        [workclass],
        [fnlwgt],
        [education],
        [education-num],
        [marital-status],
        [occupation],
        [relationship],
        [race],
        [sex],
        [capital-gain],
        [capital-loss],
        [hours-per-week],
        [native-country],
        [income]
     z dbo.censusdata;
8. U dołu hello hello roboczego eksperymentu, kliknij przycisk **Uruchom**.

## <a name="create-hello-predictive-experiment"></a>Utworzyć eksperyment predykcyjny hello
Następnie możesz skonfigurować eksperyment predykcyjny hello, z którego można wdrożyć usługi sieci web.

1. U dołu hello hello roboczego eksperymentu, kliknij przycisk **ustawić usługę sieci Web** i wybierz **predykcyjnej usługi sieci Web [zalecane]**.
2. Usuń hello *wprowadzania usługi sieci Web* i *modułów wyjście usługi sieci Web* z eksperyment predykcyjny hello. 
3. W polu wyszukiwania składników hello wpisz eksportu.
4. Z listy wyników hello, Dodaj *eksportowanie danych* kanwy eksperymentu toohello modułu.
5. Połącz dane wyjściowe hello *Score Model* danych wejściowych hello modułu hello *eksportowanie danych* modułu. 
6. W okienku właściwości, wybierz **bazy danych SQL Azure** w hello dane miejsce docelowe z listy rozwijanej.
7. W hello **nazwę serwera bazy danych**, **Nazwa bazy danych**, **nazwę konta użytkownika serwera**, i **hasło konta użytkownika serwera** wprowadź Witaj odpowiednie informacje dla bazy danych.
8. W hello **rozdzielana przecinkami lista kolumn toobe zapisane** wpisz oceniane etykiety.
9. W hello **pole Nazwa tabeli danych**, wpisz dbo. ScoredLabels. Jeśli nie istnieje tabela hello, utworzeniu po uruchomieniu eksperymentu hello lub usługi sieci web hello jest wywoływana.
10. W hello **rozdzielana przecinkami lista kolumn datatable** wpisz ScoredLabels.

Podczas pisania aplikacji czy wywołania hello usługi końcowego sieci web, możesz toospecify innej wejściowe tabeli zapytania lub docelowego w czasie wykonywania. tooconfigure te wejściach i wyjściach, użyj hello parametry usługi sieci Web funkcji tooset hello *i zaimportuj dane* modułu *źródła danych* właściwości i hello *eksportowanie danych* tryb Właściwość docelowego danych.  Aby uzyskać więcej informacji o parametry usługi sieci Web, zobacz hello [wpis parametry usługi sieci Web uczenie maszynowe Azure](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) na powitania Cortana Intelligence i Machine Learning blogu.

Witaj tooconfigure parametry usługi sieci Web hello importu zapytania i tabela docelowa hello:

1. W okienku właściwości hello hello *i zaimportuj dane* modułu, kliknij ikonę hello na powitania górnego prawego hello **zapytanie bazy danych** i wybierz pozycję **ustawić jako parametr usługi sieci web**.
2. W okienku właściwości hello hello *eksportowanie danych* modułu, kliknij ikonę hello na powitania górnego prawego hello **Nazwa tabeli danych** i wybierz pozycję **ustawić jako parametr usługi sieci web**.
3. U dołu hello hello *eksportowanie danych* okienka właściwości modułu, w hello **parametry usługi sieci Web** sekcji, kliknij przycisk zapytanie bazy danych i zmień jego nazwę zapytania.
4. Kliknij przycisk **Nazwa tabeli danych** i zmień jego nazwę **tabeli**.

Gdy wszystko będzie gotowe, eksperymentu powinien wyglądać podobnie toohello po obrazu:

![Końcowe wygląd eksperymentu.](./media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

Teraz można wdrożyć hello eksperymentu jako usługę sieci web.

## <a name="deploy-hello-web-service"></a>Wdrażanie usługi sieci web hello
Można wdrożyć tooeither Classic lub Nowa usługa sieci web.

### <a name="deploy-a-classic-web-service"></a>Wdrażanie usługi sieci Web klasycznego
toodeploy w trybie klasycznym usługi sieci Web i utworzyć tooconsume aplikacji go:

1. U dołu hello hello roboczego eksperymentu kliknij przycisk Uruchom.
2. Po zakończeniu uruchom powitania kliknij **wdrażanie usługi sieci Web** i wybierz **wdrażanie usługi sieci Web [klasyczny]**.
3. Na pulpicie nawigacyjnym usługi sieci web hello zlokalizuj klucz interfejsu API. Skopiuj i zapisz go toouse później.
4. W hello **domyślny punkt końcowy** tabeli, kliknij przycisk hello **Batch Execution** łącze tooopen hello strona pomocy interfejsu API.
5. W programie Visual Studio Utwórz aplikację konsoli języka C#: **nowy** > **projektu** > **Visual C#** > **systemu Windows Klasyczny pulpit** > **konsoli aplikacji (.NET Framework)**.
6. Na powitania strona pomocy interfejsu API, Znajdź hello **przykładowy kod** sekcji u dołu hello hello strony.
7. Skopiuj i Wklej hello C# przykładowy kod do pliku Program.cs i usunąć wszystkie odwołania toohello obiektu blob magazynu.
8. Zaktualizuj wartość hello hello *apiKey* kluczem interfejsu API hello zapisany wcześniej zmiennej.
9. Zlokalizuj hello żądania deklaracji i aktualizacji hello wartości parametry usługi sieci Web, które są przekazywane toohello *i zaimportuj dane* i *eksportowanie danych* modułów. W takim przypadku używać hello oryginalne zapytanie, ale definiuje nowej nazwy tabeli.
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. Uruchamianie aplikacji hello. 

Po zakończeniu uruchom hello nowej tabeli jest dodawany toohello bazy danych zawierające hello oceniania wyników.

### <a name="deploy-a-new-web-service"></a>Wdrożenie nowej usługi sieci Web

> [!NOTE] 
> toodeploy nową usługę sieci web, należy posiadać odpowiednie uprawnienia w hello toowhich subskrypcji możesz wdrażanie usługi sieci web hello. Aby uzyskać więcej informacji, zobacz [zarządzania usługi sieci Web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

toodeploy jako nową usługę sieci Web i utworzyć tooconsume aplikacji go:

1. U dołu hello hello roboczego eksperymentu, kliknij przycisk **Uruchom**.
2. Po zakończeniu uruchom powitania kliknij **wdrażanie usługi sieci Web** i wybierz **wdrażanie usługi sieci Web [New]**.
3. Na stronie eksperymentu wdrażanie hello, wprowadź nazwę usługi sieci web i wybrać planu cenowego, a następnie kliknij przycisk **Wdróż**.
4. Na powitania **szybkiego startu** kliknij przycisk **Consume**.
5. W hello **przykładowy kod** kliknij **partii**.
6. W programie Visual Studio Utwórz aplikację konsoli języka C#: **nowy** > **projektu** > **Visual C#** > **systemu Windows Klasyczny pulpit** > **konsoli aplikacji (.NET Framework)**.
7. Skopiuj i Wklej hello C# przykładowy kod w pliku Program.cs.
8. Zaktualizuj wartość hello hello *apiKey* zmiennej z hello **klucza podstawowego** znajduje się w hello **zużycie podstawowe informacje o** sekcji.
9. Zlokalizuj hello *scoreRequest* deklaracji i aktualizacji wartości hello parametry usługi sieci Web, które są przekazywane toohello *i zaimportuj dane* i *eksportowanie danych* modułów. W takim przypadku używać hello oryginalne zapytanie, ale definiuje nowej nazwy tabeli.
   
        var scoreRequest = new
        {       
            Inputs = new Dictionary<string, StringTable>()
            {
            },
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable3" },
            }
        };
10. Uruchamianie aplikacji hello. 

