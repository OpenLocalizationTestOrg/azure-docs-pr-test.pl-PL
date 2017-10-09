---
title: "Tworzenie rozwiązań partii z szablony projektu Visual Studio - Azure aaaStart | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak szablony projektu Visual Studio może pomóc w implementacji i uruchamiania obciążeń obliczeniowych w partii zadań Azure."
services: batch
documentationcenter: .net
author: fayora
manager: timlt
editor: 
ms.assetid: 5e041ae2-25af-4882-a79e-3aa63c4bfb20
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a61c480ddc4dffd66c01220a137a3e852e39c338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-project-templates-toojump-start-batch-solutions"></a>Użyj rozwiązań toojump start szablony programu Visual Studio projektu w partii

Hello **Menedżer zadań** i **szablony zadań procesora Visual Studio** dla partii Podaj kod toohelp możesz tooimplement i uruchom obciążeń obliczeniowych w partii o hello najmniej wysiłku. Ten dokument zawiera opis tych szablonów i zawiera wskazówki dotyczące toouse je.

> [!IMPORTANT]
> W tym artykule opisano tylko informacje o odpowiednich toothese dwa szablony i przyjęto założenie, że czytelnik zna hello usługa partia zadań i tooit powiązane kluczowe założenia: pule, obliczeniowe węzłów, zadań i zadań, zadania Menedżer zadania, zmienne środowiskowe i innych istotne informacje. Więcej informacji można znaleźć [partii podstawy usługi Azure](batch-technical-overview.md), [Przegląd funkcji partii dla deweloperów](batch-api-basics.md), i [wprowadzenie hello biblioteki partii zadań Azure dla platformy .NET](batch-dotnet-get-started.md).
> 
> 

## <a name="high-level-overview"></a>Ogólne omówienie
Szablony Hello Menedżer zadań i zadań procesora może być używane toocreate dwa składniki przydatne:

* Zadanie Menedżer zadania, które implementuje podziału zadania, które można podzielić zadania na wielu zadań, które można uruchomić osobno, równolegle.
* Procesor zadania, które mogą być używane tooperform przetwarzanie wstępne i przetwarzania końcowego wokół wiersza polecenia aplikacji.

Na przykład w przypadku renderowania film, podziału zadania hello czy przekształcić zadania pojedynczego filmu setek lub tysięcy oddzielnych zadań, które będzie przetwarzać osobno poszczególne ramki. Odpowiednio hello zadań procesora może wywołać hello renderowanie aplikacji i wszystkie procesy zależne, które są potrzebne toorender każdej ramce, a także wszelkie dodatkowe akcje (na przykład kopiowanie hello renderowane ramki tooa lokalizacji magazynu).

> [!NOTE]
> Hello szablonów Menedżer zadań i zadań procesora są niezależne od siebie, więc możesz wybrać toouse obie lub tylko jeden z nich, w zależności od wymagań hello zadania obliczeniowych i na swoje preferencje.
> 
> 

Jak pokazano na poniższym diagramie hello, zadanie obliczeniowe, które korzysta z tych szablonów będzie przejście przez trzech etapów:

1. Kod klienta Hello (np. aplikacji, usługi sieci web, itp.) przesyła toohello zadania usługa partia zadań Azure, określając jako jego program zadania Menedżer zadania hello zadania menedżera.
2. Hello usługa partia zadań uruchamia zadanie Menedżer zadania hello w węźle obliczeń i hello hello powoduje uruchomienie podziału zadania określone liczba zadań procesora zadań, na jako wiele węzły obliczeniowe zgodnie z potrzebami, na podstawie parametrów hello i specyfikacje hello zadania podziału kodu.
3. Witaj zadań procesora zadania są uruchamiane niezależnie, równoległe, tooprocess hello danych wejściowych i generowanie danych wyjściowych hello.

![Diagram pokazujący, jak kod klienta współdziała z hello usługa partia zadań][diagram01]

## <a name="prerequisites"></a>Wymagania wstępne
Szablony partii hello toouse, będą potrzebne następujące hello:

* Komputer z programu Visual Studio 2015. Szablony usługi partia zadań są obecnie obsługiwane tylko dla programu Visual Studio 2015.
* Witaj partii szablonów, które nie są dostępne z hello [galerii programu Visual Studio] [ vs_gallery] jako rozszerzenia programu Visual Studio. Istnieją dwa sposoby tooget hello szablonów:
  
  * Zainstaluj hello szablonów przy użyciu hello **rozszerzenia i aktualizacje** okno dialogowe w programie Visual Studio (Aby uzyskać więcej informacji, zobacz [Znajdowanie i rozszerzenia przy użyciu programu Visual Studio][vs_find_use_ext]). W hello **rozszerzenia i aktualizacje** okno dialogowe, wyszukiwanie i pobieranie hello następujące dwa rozszerzenia:
    
    * Azure Menedżer zadania wsadowego z rozdzielaczem zadania
    * Procesor zadania usługa partia zadań Azure
  * Pobieranie hello z galerii online hello for Visual Studio: [szablony projektów programu Microsoft Azure partii][vs_gallery_templates]
* Jeśli planujesz toouse hello [pakietów aplikacji](batch-application-packages.md) Menedżer zadań hello toodeploy funkcji i toohello procesor zadania wsadowego węzły obliczeniowe, należy toolink tooyour konta magazynu konta usługi partia zadań.

## <a name="preparation"></a>Przygotowanie
Zaleca się tworzenia rozwiązania, które mogą zawierać Menedżera zadań, a także zadań procesora, ponieważ to może być łatwiejsze kodu tooshare między Menedżer zadań i zadań procesora programy. toocreate to rozwiązanie, wykonaj następujące kroki:

1. Otwórz program Visual Studio i wybierz **pliku** > **nowy** > **projektu**.
2. W obszarze **szablony**, rozwiń węzeł **inne typy projektów**, kliknij przycisk **rozwiązań programu Visual Studio**, a następnie wybierz **puste rozwiązanie**.
3. Wpisz nazwę, która opisuje z aplikacji i hello celem tego rozwiązania (np. "LitwareBatchTaskPrograms").
4. toocreate hello nowe rozwiązanie, kliknij przycisk **OK**.

## <a name="job-manager-template"></a>Menedżer zadań szablonu
Szablon Menedżer zadań Hello pomaga tooimplement zadanie Menedżer zadania, które można wykonać następujące akcje hello:

* Podziel zadania na wielu zadań.
* Przedstawia toorun tych zadań w partii.

> [!NOTE]
> Aby uzyskać więcej informacji na temat zadania Menedżera zadań, zobacz [Przegląd funkcji partii dla deweloperów](batch-api-basics.md#job-manager-task).
> 
> 

### <a name="create-a-job-manager-using-hello-template"></a>Tworzenie przy użyciu szablonu hello Menedżer zadania
tooadd rozwiązania toohello Menedżer zadania utworzone wcześniej, wykonaj następujące kroki:

1. Otwórz istniejącego rozwiązania programu Visual Studio.
2. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy rozwiązanie hello, kliknij przycisk **Dodaj** > **nowy projekt**.
3. W obszarze **Visual C#**, kliknij przycisk **chmury**, a następnie kliknij przycisk **Menedżer zadań wsadowych Azure z rozdzielaczem zadania**.
4. Wpisz nazwę opisującą aplikacji i identyfikuje tego projektu jako Menedżer zadań hello (np. "LitwareJobManager").
5. toocreate hello projektu, kliknij przycisk **OK**.
6. Na koniec kompilacji hello projektu tooforce Visual Studio tooload wszystkie odwołania do pakietów NuGet i tooverify, który hello projektu jest prawidłowa, przed rozpoczęciem modyfikowania jej.

### <a name="job-manager-template-files-and-their-purpose"></a>Pliki szablonów Menedżer zadań i ich przeznaczenie
Podczas tworzenia projektu za pomocą szablonu Menedżer zadań hello generuje trzech grup plików kodu:

* plik główny program Hello (Program.cs). Zawiera punkt wejścia program hello i obsługa wyjątków najwyższego poziomu. Nie powinien zwykle toomodify to konieczne.
* Witaj katalogu Framework. Zawiera pliki hello odpowiedzialny za hello "standardowy" pracy przez program Menedżer zadania hello — rozpakowywania parametrów, Dodawanie zadania wsadowego zadania toohello itp. Nie powinien zwykle należy toomodify tych plików.
* Plik podziału zadania Hello (JobSplitter.cs). Jest to, gdzie należy umieścić specyficzne dla aplikacji logiki do dzielenia zadania do zadania.

Oczywiście można dodać dodatkowe pliki jako wymagany toosupport kodu podziału zadania, w zależności od złożoności hello zadania hello dzielenia logiki.

Szablon Hello generuje również standardowe pliki projektu .NET pliku .csproj app.config, packages.config, np.

Hello pozostałej części tej sekcji przedstawiono hello różnych plików i ich struktury kodu oraz opisano, co oznacza każdej klasy.

![Visual Studio Solution Explorer przedstawiający hello Menedżer zadań szablon rozwiązania][solution_explorer01]

**Pliki Framework**

* `Configuration.cs`: Hermetyzuje hello ładowanie danych konfiguracji zadania, takie jak szczegóły konta wsadowego, poświadczenia konta magazynu połączone, informacje i zadań i parametrów zadania. Umożliwia również dostęp zmienne środowiskowe zdefiniowane tooBatch (Zobacz ustawienia środowiska dla zadań, w dokumentacji partii hello) za pomocą klasy Configuration.EnvironmentVariable hello.
* `IConfiguration.cs`: Abstract hello implementacji hello klasa konfiguracji, tak aby można było z podziału zadania przy użyciu obiektu fałszywych lub zasymulować konfiguracji testu jednostkowego.
* `JobManager.cs`: Organizuje hello składniki programu Menedżer zadania hello. Jest odpowiedzialny za hello inicjowanie podziału zadania hello, wywoływania hello podziału zadania, oraz wysyłania zadań hello zwrócona przez hello obiekt przesyłający zadania toohello podziału zadania.
* `JobManagerException.cs`: Błąd, który wymaga hello zadania Menedżera tooterminate reprezentuje. JobManagerException jest używane toowrap błędy "Oczekiwano" gdzie określone informacje diagnostyczne można podać jako część rozwiązania.
* `TaskSubmitter.cs`: Ta klasa jest zadania odpowiada tooadding zwrócony przez zadanie wsadowe toohello hello zadania podziału. Klasa JobManager Hello agreguje hello sekwencji zadań w partie dodanie wydajne, ale odpowiednim toohello zadania, a następnie wywołuje TaskSubmitter.SubmitTasks wątku w tle dla każdej partii.

**Zadanie podziału**

`JobSplitter.cs`: Ta klasa zawiera specyficzne dla aplikacji logiki do dzielenia hello zadania do zadania. Witaj framework wywołuje hello JobSplitter.Split metody tooobtain sekwencji zadań, które dodaje zadania toohello metodą hello zwraca je. Jest klasa hello, gdzie będzie wstrzyknąć logiki hello zadania. Implementuje hello podziału metody tooreturn sekwencję wystąpień CloudTask przedstawiających hello zadania, do których mają toopartition hello zadania.

**Standardowe pliki projektu wiersza polecenia platformy .NET**

* `App.config`: Standardowego pliku konfiguracji aplikacji .NET.
* `Packages.config`: Standardowy plik zależności pakietu NuGet.
* `Program.cs`: Zawiera punkt wejścia program hello oraz wyjątków najwyższego poziomu.

### <a name="implementing-hello-job-splitter"></a>Implementowanie hello zadania podziału
Po otwarciu projektu szablonu Menedżer zadań hello hello projektu zostanie otworzył pliku JobSplitter.cs hello domyślnie. Można zaimplementować hello dzielenie logikę zadań hello w obciążenia przy użyciu hello Split() metody wyświetlane poniżej:

```csharp
/// <summary>
/// Gets hello tasks into which toosplit hello job. This is where you inject
/// your application-specific logic for decomposing hello job into tasks.
///
/// hello job manager framework invokes hello Split method for you; you need
/// only tooimplement it, not toocall it yourself. Typically, your
/// implementation should return tasks lazily, for example using a C#
/// iterator and hello "yield return" statement; this allows tasks toobe added
/// and toostart running while splitting is still in progress.
/// </summary>
/// <returns>hello tasks toobe added toohello job. Tasks are added automatically
/// by hello job manager framework as they are returned by this method.</returns>
public IEnumerable<CloudTask> Split()
{
    // Your code for hello split logic goes here.
    int startFrame = Convert.ToInt32(_parameters["StartFrame"]);
    int endFrame = Convert.ToInt32(_parameters["EndFrame"]);

    for (int i = startFrame; i <= endFrame; i++)
    {
        yield return new CloudTask("myTask" + i, "cmd /c dir");
    }
}
```

> [!NOTE]
> Witaj adnotacji części hello `Split()` metoda jest hello tylko części hello Menedżer zadań szablonu kod, który jest przeznaczony dla toomodify możesz, dodając toosplit logiki hello zadaniach do różnych zadań. Jeśli chcesz toomodify różnych części szablonu hello, sprawdź, czy są zapoznaniu z działania partii i wypróbować kilka hello [partii przykłady kodu][github_samples].
> 
> 

Implementacji Split() ma dostęp do:

* Witaj parametrów zadania przy użyciu hello `_parameters` pola.
* Witaj CloudJob obiektów reprezentująca zadania hello, za pośrednictwem hello `_job` pola.
* Witaj CloudTask obiektów reprezentująca zadania Menedżer zadania hello, za pomocą hello `_jobManagerTask` pola.

Twoje `Split()` implementacji nie jest konieczne tooadd zadania toohello zadania bezpośrednio. Zamiast tego kod powinien zwrócić sekwencji CloudTask obiektów, a te zostaną dodane zadania toohello automatycznie przez hello framework klasy, które wywołują hello podziału zadania. Jest typowe iteratora toouse C# w (`yield return`) funkcji tooimplement rozdzielaczy zadania, ponieważ dzięki temu hello toostart zadania uruchomione tak szybko, jak to możliwe, zamiast oczekiwania dla wszystkich zadań toobe obliczane.

**Niepowodzenie zadania podziału**

Jeśli Twoje podziału zadań wystąpi błąd, powinno być:

* Zakończenie sekwencji hello za pomocą hello C# `yield break` instrukcji, w którym Menedżer zadań wielkość hello będą traktowane jako pomyślnie; lub
* Zgłoś wyjątek, w którym Menedżer zadań wielkość hello będą traktowane jako nieudane i może podjęta w zależności od tego, jak powitania klienta skonfigurował go).

W obu przypadkach żadnych zadań już zwracane przez podziału zadań hello, a zadanie wsadowe dodano toohello będzie toorun kwalifikujących się. Jeśli nie chcesz tego toohappen, następnie możesz:

* Zakończ zadanie hello przed powrotem z hello zadania podziału
* Sformułować hello całe zadanie kolekcji przed jej zwróceniem (oznacza to, zwróć `ICollection<CloudTask>` lub `IList<CloudTask>` zamiast wykonania programu podziału zadania przy użyciu iteratora C#)
* Użyj toomake zależności zadań, wszystkie zadania zależą od hello pomyślne zakończenie hello Menedżer zadań

**Ponowne próby Menedżer zadania**

Jeśli hello Menedżer zadań nie powiedzie się, może zostać powtórzone przez usługi partia zadań hello w zależności od ustawienia ponawiania próby powitania klienta. Ogólnie rzecz biorąc jest bezpieczne, ponieważ hello framework dodaje zadania toohello zadania, ignoruje wszystkie zadania, które już istnieją. Jednak jeśli obliczanie zadania jest kosztowna, nie możesz tooincur hello koszt ponownego obliczenia zadania, które już zostały dodane zadania toohello; z drugiej strony Jeśli Uruchom ponownie hello jest toogenerate nie gwarantuje hello takich samych identyfikatorów zadań zachowanie "Ignoruj duplikaty" hello zostanie nie zaczną działać, a następnie. W takich przypadkach należy zaprojektować jego zadania podziału toodetect hello pracy, które zostało już wykonane i powtarzaj go, na przykład, wykonując CloudJob.ListTasks przed uruchomieniem zadania tooyield.

### <a name="exit-codes-and-exceptions-in-hello-job-manager-template"></a>Zakończ kody i wyjątków w szablonie Menedżer zadań hello
Kody wyjścia i wyjątków udostępniają mechanizm toodetermine hello wyniki działania programu i mogą pomóc tooidentify problemów z wykonywania hello hello programu. Szablon Menedżer zadań Hello implementuje hello kody wyjścia i wyjątków opisanych w tej sekcji.

Zadanie Menedżer zadania, które jest implementowana przy użyciu szablonu Menedżer zadań hello może zwracać trzy kody zakończenia możliwe:

| Kod | Opis |
| --- | --- |
| 0 |Menedżer zadań Hello została ukończona pomyślnie. Toocompletion uruchomiono zadanie kodu podziału, a wszystkie zadania zostały dodane toohello zadania. |
| 1 |Hello zadania Menedżer zadania nie powiodło się z powodu wyjątku w części 'oczekiwano' hello program. Hello wyjątek przetłumaczonego tooa JobManagerException informacji diagnostycznych i, w miarę możliwości sugestie dotyczące rozwiązywania hello awarii. |
| 2 |Hello zadania Menedżer zadania nie powiodło się z powodu wyjątku "nieoczekiwane". Witaj wyjątek toostandard zarejestrowanych danych wyjściowych, ale Menedżer zadań hello był tooadd wszelkie dodatkowe informacje diagnostyczne lub korygowania. |

W przypadku hello niepowodzenie zadania Menedżer zadania niektóre zadania mogą nadal dodano toohello usługi przed hello błąd. Te zadania będą uruchamiane jako standardowe. Omówienie tę ścieżkę kodu w temacie "Niepowodzenie podziału zadania" powyżej.

Wszystkie informacje hello zwrócony przez wyjątki są zapisywane w plikach stdout.txt i stderr.txt. Aby uzyskać więcej informacji, zobacz [obsługi błędu](batch-api-basics.md#error-handling).

### <a name="client-considerations"></a>Uwagi dotyczące klientów
W tej sekcji opisano niektóre wymagania dotyczące wdrażania klienta podczas wywoływania Menedżer zadań, na podstawie tego szablonu. Zobacz [jak toopass parametrów i zmiennych środowiskowych z hello kodu klienta](#pass-environment-settings) szczegółowe informacje na temat przekazywania parametry i ustawienia środowiska.

**Wymagane poświadczenia**

W kolejności tooadd zadania toohello Azure zadania wsadowego hello zadania Menedżer zadania wymaga swój adres URL konta partii zadań Azure i klucz. Należy podać je w zmiennych środowiskowych o nazwie YOUR_BATCH_URL i YOUR_BATCH_KEY. Można ustawić w hello zadania Menedżera zadań ustawienia środowiska. Na przykład w języku C# klienta:

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    new EnvironmentSetting("YOUR_BATCH_URL", "https://account.region.batch.azure.com"),
    new EnvironmentSetting("YOUR_BATCH_KEY", "{your_base64_encoded_account_key}"),
};
```
**Poświadczenia magazynu**

Zazwyczaj hello klient nie potrzebuje tooprovide hello magazynu połączone konta poświadczenia toohello zadania Menedżer zadania, ponieważ () większości menedżerów zadania nie są konta magazynu hello połączone dostępu tooexplicitly i (b) hello połączonym koncie magazynu jest często dostępne zadania tooall jako wspólne ustawienia środowiska hello zadania. Jeśli nie udostępniasz hello połączone konta magazynu za pomocą typowych ustawień środowiska hello i Menedżer zadań hello wymaga dostępu do magazynu toolinked, a następnie, należy określić poświadczenia magazynu hello połączone w następujący sposób:

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    /* other environment settings */
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

**Ustawienia zadania Menedżer zadania**

powitania klienta należy ustawić Menedżer zadań hello *killJobOnCompletion* Flaga zbyt**false**.

Jest zwykle bezpieczne dla powitania klienta tooset *runExclusive* za**false**.

powitania klienta należy używać hello *resourceFiles* lub *applicationPackageReferences* węzeł obliczeniowy toohello wdrożone wykonywalnego Menedżer zadań hello toohave kolekcji (i jego wymaganych bibliotek DLL).

Domyślnie hello Menedżer zadań nie zostanie podjęta, jeśli działanie nie powiodło się. W zależności od logiki Menedżer zadania powitania klienta może być ponownych prób tooenable za pośrednictwem *ograniczenia*/*maxTaskRetryCount*.

**Ustawienia zadania**

Jeśli podziału zadania hello emituje zadania z zależnościami, powitania klienta należy ustawić tootrue usesTaskDependencies hello zadania.

W modelu podziału zadania hello jest rzadko klientów toowish tooadd zadania toojobs poza jakiego podziału zadania hello tworzy. powitania klienta w związku z tym należy zwykle ustawić hello zadania *onAllTasksComplete* za**terminatejob**.

## <a name="task-processor-template"></a>Szablon zadania
Szablon zadań procesora pomaga tooimplement procesor zadania, które można wykonać następujące akcje hello:

* Konfigurowanie hello informacji wymaganych przez każdy toorun zadania wsadowego.
* Wykonanie wszystkich akcji wymagane przez poszczególne zadania wsadowego.
* Zapisz dane wyjściowe zadania toopersistent magazynu.

Procesor zadania nie jest wymagane toorun zadania wsadowego, zaletą hello użycia procesora zadań jest tooimplement otoki wszystkie akcje wykonania zadania w jednej lokalizacji. Na przykład jeśli potrzebujesz toorun kilka aplikacji w kontekście hello każdego zadania lub jeśli potrzebujesz toocopy toopersistent pamięci masowej po zakończeniu poszczególnych zadań.

Witaj akcje wykonywane przez hello zadań procesora może być jako prosty lub złożonych, a wiele lub kilku, co jest wymagane przez obciążenie. Ponadto implementując wszystkie akcje zadania w jednym procesorze zadań, można łatwo zaktualizować lub dodać akcje na podstawie zmiany wymagań tooapplications lub obciążenia. Jednak w niektórych przypadkach procesor zadania może nie być optymalne rozwiązanie hello implementacji można dodać niepotrzebnych złożoności, na przykład podczas uruchamiania zadania, które można szybko uruchomić z wiersza polecenia, proste.

### <a name="create-a-task-processor-using-hello-template"></a>Tworzenie przy użyciu szablonu hello procesor zadania
tooadd rozwiązania toohello procesor zadania utworzone wcześniej, wykonaj następujące kroki:

1. Otwórz istniejącego rozwiązania programu Visual Studio.
2. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy rozwiązanie hello, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **nowy projekt**.
3. W obszarze **Visual C#**, kliknij przycisk **chmury**, a następnie kliknij przycisk **Azure partii zadań procesora**.
4. Wpisz nazwę opisującą aplikacji i identyfikuje tego projektu jako hello zadań procesora (np. "LitwareTaskProcessor").
5. toocreate hello projektu, kliknij przycisk **OK**.
6. Na koniec kompilacji hello projektu tooforce Visual Studio tooload wszystkie odwołania do pakietów NuGet i tooverify, który hello projektu jest prawidłowa, przed rozpoczęciem modyfikowania jej.

### <a name="task-processor-template-files-and-their-purpose"></a>Pliki szablonów zadań procesora i ich przeznaczenie
Podczas tworzenia projektu za pomocą szablonu procesora zadań hello generuje trzech grup plików kodu:

* plik główny program Hello (Program.cs). Zawiera punkt wejścia program hello i obsługa wyjątków najwyższego poziomu. Nie powinien zwykle toomodify to konieczne.
* Witaj katalogu Framework. Zawiera pliki hello odpowiedzialny za hello "standardowy" pracy przez program Menedżer zadania hello — rozpakowywania parametrów, Dodawanie zadania wsadowego zadania toohello itp. Nie powinien zwykle należy toomodify tych plików.
* Witaj zadań procesora pliku (TaskProcessor.cs). Jest to, gdzie należy umieścić specyficzne dla aplikacji logiki wykonywania zadania (zazwyczaj wywołując limit tooan istniejący plik wykonywalny). Wstępne i przetwarzanie końcowe kodu, na przykład pobranie dodatkowych danych lub przekazywania plików wyników również tu jest.

Oczywiście można dodać dodatkowe pliki jako toosupport wymaganych zadań procesora kodu, w zależności od złożoności hello zadania hello dzielenia logiki.

Szablon Hello generuje również standardowe pliki projektu .NET pliku .csproj app.config, packages.config, np.

Hello pozostałej części tej sekcji przedstawiono hello różnych plików i ich struktury kodu oraz opisano, co oznacza każdej klasy.

![Visual Studio Solution Explorer przedstawiający hello zadań procesora szablon rozwiązania][solution_explorer02]

**Pliki Framework**

* `Configuration.cs`: Hermetyzuje hello ładowanie danych konfiguracji zadania, takie jak szczegóły konta wsadowego, poświadczenia konta magazynu połączone, informacje i zadań i parametrów zadania. Umożliwia również dostęp zmienne środowiskowe zdefiniowane tooBatch (Zobacz ustawienia środowiska dla zadań, w dokumentacji partii hello) za pomocą klasy Configuration.EnvironmentVariable hello.
* `IConfiguration.cs`: Abstract hello implementacji hello klasa konfiguracji, tak aby można było z podziału zadania przy użyciu obiektu fałszywych lub zasymulować konfiguracji testu jednostkowego.
* `TaskProcessorException.cs`: Błąd, który wymaga hello zadania Menedżera tooterminate reprezentuje. TaskProcessorException jest używane toowrap błędy "Oczekiwano" gdzie określone informacje diagnostyczne można podać jako część rozwiązania.

**Procesor zadania**

* `TaskProcessor.cs`: Uruchamia zadanie hello. Hello framework wywołuje metodę TaskProcessor.Run hello. Jest klasa hello, gdzie będzie wstrzyknąć logiki specyficzne dla aplikacji hello zadania. Implementuje metody Run hello do:
  * Analizowanie i sprawdź poprawność parametrów zadania
  * Redagowanie hello wiersza polecenia dla dowolnego programu zewnętrznego ma tooinvoke
  * Zaloguj się żadnych informacji diagnostycznych, które mogą wymagać na potrzeby debugowania
  * Rozpocznij proces przy użyciu tego wiersza polecenia
  * Poczekaj, aż hello tooexit procesu
  * Przechwytywanie kod zakończenia hello hello toodetermine procesu, jeśli zakończyło się pomyślnie, lub nie powiodło się
  * Zapisz wszystkie pliki wyjściowe, które mają tookeep toopersistent magazynu

**Standardowe pliki projektu wiersza polecenia platformy .NET**

* `App.config`: Standardowego pliku konfiguracji aplikacji .NET.
* `Packages.config`: Standardowy plik zależności pakietu NuGet.
* `Program.cs`: Zawiera punkt wejścia program hello oraz wyjątków najwyższego poziomu.

## <a name="implementing-hello-task-processor"></a>Implementowanie hello zadań procesora
Po otwarciu projektu szablonu zadań procesora hello hello projektu zostanie otworzył pliku TaskProcessor.cs hello domyślnie. Można zaimplementować logikę hello Uruchom zadania hello w obciążenia przy użyciu metody Run() hello pokazano poniżej:

```csharp
/// <summary>
/// Runs hello task processing logic. This is where you inject
/// your application-specific logic for decomposing hello job into tasks.
///
/// hello task processor framework invokes hello Run method for you; you need
/// only tooimplement it, not toocall it yourself. Typically, your
/// implementation will execute an external program (from resource files or
/// an application package), check hello exit code of that program and
/// save output files toopersistent storage.
/// </summary>
public async Task<int> Run()

{
    try
    {
        //Your code for hello task processor goes here.
        var command = $"compare {_parameters["Frame1"]} {_parameters["Frame2"]} compare.gif";
        using (var process = Process.Start($"cmd /c {command}"))
        {
            process.WaitForExit();
            var taskOutputStorage = new TaskOutputStorage(
            _configuration.StorageAccount,
            _configuration.JobId,
            _configuration.TaskId
            );
            await taskOutputStorage.SaveAsync(
            TaskOutputKind.TaskOutput,
            @"..\stdout.txt",
            @"stdout.txt"
            );
            return process.ExitCode;
        }
    }
    catch (Exception ex)
    {
        throw new TaskProcessorException(
        $"{ex.GetType().Name} exception in run task processor: {ex.Message}",
        ex
        );
    }
}
```
> [!NOTE]
> Witaj adnotacjami części hello metody Run() jest hello tylko sekcja hello zadań procesora szablonu kodu, który jest przeznaczony dla należy toomodify przez dodanie logiki hello uruchamiania zadań hello obciążenie. Jeśli chcesz toomodify różnych części szablonu hello, należy najpierw zapoznać się z działanie wsadowego przez przejrzenie dokumentacji partii hello i wypróbować kilka przykładów kodu hello partii.
> 
> 

Hello metody Run() jest odpowiedzialny za uruchamianie hello wiersza polecenia, uruchamianie procesów z co najmniej jeden oczekiwanie na wszystkich toocomplete procesu, zapisywanie wyników hello i na koniec zwróciło kod zakończenia. Witaj metody Run() polega na tym, gdzie wdrożyć hello przetwarzania logiki dla zadań. Witaj zadań procesora framework wywołuje metodę Run() hello automatycznie; nie trzeba toocall ją samodzielnie.

Implementacji Run() ma dostęp do:

* Witaj parametrów zadania przy użyciu hello `_parameters` pola.
* identyfikatory poleceń i zadań, za pośrednictwem hello Hello `_jobId` i `_taskId` pól.
* Witaj zadań konfiguracji, za pomocą hello `_configuration` pola.

**Niepowodzenie zadania**

W razie awarii wyjściu metody Run() hello Zgłaszanie wyjątku, ale w formancie kodu zakończenia zadania hello spowoduje to pozostawienie hello wyjątek najwyższego poziomu obsługi. Jeśli potrzebujesz kod zakończenia hello toocontrol tak, aby odróżnić różnego rodzaju błąd, na przykład na potrzeby diagnostyki lub ponieważ niektóre rodzaje uszkodzenia należy zakończyć hello zadania i inne osoby nie powinien, a następnie metody Run() hello powinny być kończone zwracając Kod wyjścia równy zero. Staje się on kod zakończenia zadania hello.

### <a name="exit-codes-and-exceptions-in-hello-task-processor-template"></a>Zakończ kody i wyjątków w szablonie zadań procesora hello
Kody wyjścia i wyjątków udostępniają mechanizm toodetermine hello wynik działania programu, a są pomocne w identyfikacji problemów z wykonywania hello hello programu. szablon zadania Hello implementuje hello kody wyjścia i wyjątków opisanych w tej sekcji.

Zadanie procesora zadań, które jest implementowana przy użyciu szablonu zadań procesora hello może zwracać trzy kody zakończenia możliwe:

| Kod | Opis |
| --- | --- |
| [Process.ExitCode][process_exitcode] |Procesor zadania Hello uruchomiono toocompletion. Należy pamiętać, że to nie oznacza, że ten program hello, wywołany zakończyła się pomyślnie — tylko ten procesor zadania hello pomyślnie wywołany i wykonać wszelkie przetwarzania końcowego bez wyjątków. znaczenie Hello kod zakończenia hello zależy program hello wywoływane — zwykle kod zakończenia 0 oznacza, że hello program zakończyło się pomyślnie i inny kod zakończenia oznacza, że hello program nie powiodło się. |
| 1 |Hello zadań procesora nie powiodło się z powodu wyjątku w części 'oczekiwano' hello program. Witaj wyjątek przetłumaczonego tooa `TaskProcessorException` informacji diagnostycznych i, jeśli to możliwe, sugestie dotyczące rozwiązywania hello awarii. |
| 2 |Procesor zadania Hello nie powiodło się z powodu wyjątku "nieoczekiwane". Witaj wyjątek toostandard zarejestrowanych danych wyjściowych, ale hello zadań procesora był tooadd wszelkie dodatkowe informacje diagnostyczne lub korygowania. |

> [!NOTE]
> Jeśli program hello, który wywołuje używa zakończenia kody 1 i 2 tooindicate określony błąd tryby, następnie przy użyciu kodów zakończenia 1 i 2 dla błędów procesor zadania jest niejednoznaczna. Kodów zakończenia toodistinctive kody błędów zadań procesora można zmienić przez edycję przypadków wyjątek hello w pliku Program.cs hello.
> 
> 

Wszystkie informacje hello zwrócony przez wyjątki są zapisywane w plikach stdout.txt i stderr.txt. Aby uzyskać więcej informacji zobacz błąd obsługi, w hello dokumentację partii.

### <a name="client-considerations"></a>Uwagi dotyczące klientów
**Poświadczenia magazynu**

Jeśli procesor zadania używa wyjść toopersist magazynu obiektów blob platformy Azure, na przykład za pomocą hello pliku konwencje pomocnika biblioteki, musi mieć dostęp za*albo* hello poświadczeń konta magazynu w chmurze *lub* kontener adresu URL obiektu blob zawierającego sygnatury dostępu współdzielonego (SAS). Szablon Hello obsługuje podawania poświadczeń za pomocą wspólnych zmiennych środowiskowych. Klient może przekazać hello magazynu poświadczeń w następujący sposób:

```csharp
job.CommonEnvironmentSettings = new [] {
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

Konto magazynu Hello jest dostępna w hello klasy TaskProcessor za pośrednictwem hello `_configuration.StorageAccount` właściwości.

Jeśli wolisz toouse adresu URL kontenera za sygnatury dostępu Współdzielonego, można również przekazać to za pomocą ustawienia środowiska typowe zadania, ale hello zadań procesora szablon nie zawiera wbudowaną obsługę to.

**Konfiguracja magazynu**

Zaleca się zadania powitania klienta lub zadania Menedżera tworzyć żadnych kontenerów wymagane przez zadania przed dodaniem hello zadania toohello zadania. Jest to konieczne, korzystając z adresu URL kontenera do skojarzeń zabezpieczeń, w związku adresu URL nie ma uprawnień toocreate hello kontenera. Zaleca się nawet wtedy, gdy przekazujesz poświadczeń konta magazynu, zgodnie z zapisuje każdego zadania o toocall CloudBlobContainer.CreateIfNotExistsAsync hello kontenera.

## <a name="pass-parameters-and-environment-variables"></a>Przekaż parametry i zmienne środowiskowe
### <a name="pass-environment-settings"></a>Przekaż ustawienia środowiska
Klient może przekazać informacje toohello zadania Menedżera zadań w formie hello ustawienia środowiska. Te informacje można następnie używane przez zadanie Menedżer zadania hello, podczas generowania hello zadań procesora zadań, które zostanie uruchomiony jako część hello obliczeniowe zadania. Przykładami informacji hello, które można przekazać jako ustawienia środowiska są:

* Klucze konta magazynu nazwy i konta
* Adres URL konta usługi partia zadań
* Klucz konta usługi partia zadań

Witaj usługa partia zadań ma prosty mechanizm toopass środowiska ustawienia tooa zadania Menedżer zadania przy użyciu hello `EnvironmentSettings` właściwości w [Microsoft.Azure.Batch.JobManagerTask][net_jobmanagertask].

Na przykład tooget hello `BatchClient` wystąpienia dla konta usługi partia zadań, można przekazać jako zmienne środowiskowe z powitania klienta kodu hello adresu URL i klucza poświadczeń dla konta wsadowego hello udostępnionych. Podobnie tooaccess hello konto magazynu połączone konta usługi partia zadań toohello, nazwa konta magazynu hello i klucz konta magazynu hello można przekazać jako zmienne środowiskowe.

### <a name="pass-parameters-toohello-job-manager-template"></a>Przekazywanie parametrów toohello Menedżer zadań szablonu
W wielu przypadkach jest przydatne toopass-job parametry toohello Menedżera zadanie, albo zadania hello toocontrol podziału procesu lub zadania hello tooconfigure hello zadania. Można to zrobić, przekazując plik JSON o nazwie parameters.JSON następującym kodem jako plik zasobów hello zadania Menedżer zadania. Parametry Hello następnie może stać się dostępne w hello `JobSplitter._parameters` w hello Menedżer zadań szablonu.

> [!NOTE]
> Program obsługi wbudowanych parametru Hello wspiera tylko słowniki ciąg ciąg. Chcąc toopass złożone JSON wartości jako wartości parametrów, będzie konieczne toopass je jako ciągi i analizować je w podziału zadania hello lub modyfikuje hello framework `Configuration.GetJobParameters` metody.
> 
> 

### <a name="pass-parameters-toohello-task-processor-template"></a>Przekazywanie parametrów toohello procesor zadania szablonu
Można również przekazać parametrów zadania tooindividual implementowane przy użyciu szablonu zadań procesora hello. Podobnie jak przy użyciu szablonu Menedżer zadania hello, hello zadań procesora szablon wyszukuje plik zasobów o nazwie

parameters.JSON następującym kodem, a jeśli go znaleziono ładuje go jako słownik parametrów hello. Istnieje kilka opcji dotyczących sposobu toopass toohello parametrów zadania procesora:

* Ponowne użycie parametrów zadania hello JSON. Działa to dobrze, jeśli tylko parametry hello są pokazane na poziomie zadania (na przykład renderowania wysokość i szerokość). toodo, podczas tworzenia CloudTask w podziału zadania hello, dodać odwołanie do obiektu pliku zasobów parameters.JSON następującym kodem toohello z ResourceFiles zadań hello zadania Menedżera (`JobSplitter._jobManagerTask.ResourceFiles`) toohello CloudTask ResourceFiles kolekcji.
* Generowanie przekazania dokumentu parameters.JSON następującym kodem poszczególnych zadań w ramach wykonywania podziału zadań i odwołania do tego obiektu blob w kolekcji plików zasobów hello zadań. Jest to konieczne, jeśli różne zadania mają różne parametry. Przykładem może być scenariusza renderowania 3W, gdzie indeksu ramki hello jest przekazywany toohello zadań jako parametr.

> [!NOTE]
> Program obsługi wbudowanych parametru Hello wspiera tylko słowniki ciąg ciąg. Chcąc toopass złożone JSON wartości jako wartości parametrów, będzie konieczne toopass je jako ciągi i analizować je w procesorze zadań hello lub modyfikuje hello framework `Configuration.GetTaskParameters` metody.
> 
> 

## <a name="next-steps"></a>Następne kroki
### <a name="persist-job-and-task-output-tooazure-storage"></a>Utrwalanie zadań i zadań tooAzure wyjście magazynu
Kolejnym narzędziem pomocne w partii opracowywanie rozwiązań jest [konwencje pliku wsadowego Azure][nuget_package]. Użyj tego Biblioteka klas programu .NET (obecnie w wersji zapoznawczej) w magazynie tooeasily aplikacji partiami platformy .NET i pobieranie tooand dane wyjściowe zadania z usługi Magazyn Azure. [Utrwalić danych wyjściowych i zadań partii zadań Azure](batch-task-output.md) zawiera pełne omówienie hello biblioteki i jej użycia.

### <a name="batch-forum"></a>Forum usługi partia zadań
Witaj [Forum usługi partia zadań Azure] [ forum] w witrynie MSDN jest doskonałym umieścić toodiscuss partii i zadać pytania dotyczące usługi hello. HEAD na za pośrednictwem przydatne Posty "trwałe" i opublikuj swoje pytania powstałych podczas tworzenia własnych rozwiązań partii.

[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[net_jobmanagertask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobmanagertask.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[process_exitcode]: https://msdn.microsoft.com/library/system.diagnostics.process.exitcode.aspx
[vs_gallery]: https://visualstudiogallery.msdn.microsoft.com/
[vs_gallery_templates]: https://go.microsoft.com/fwlink/?linkid=820714
[vs_find_use_ext]: https://msdn.microsoft.com/library/dd293638.aspx

[diagram01]: ./media/batch-visual-studio-templates/diagram01.png
[solution_explorer01]: ./media/batch-visual-studio-templates/solution_explorer01.png
[solution_explorer02]: ./media/batch-visual-studio-templates/solution_explorer02.png
