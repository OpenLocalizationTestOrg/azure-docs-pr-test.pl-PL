---
title: "aaaOverview model programowania usług sieci szkieletowej niezawodnej usługi hello | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o modelu programowania niezawodnej usługi Service Fabric i rozpocząć pisanie własnych usług."
services: Service-Fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: vturecek; mani-ramaswamy
ms.assetid: 0c88a533-73f8-4ae1-a939-67d17456ac06
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: masnider;
ms.openlocfilehash: 41d1826df902b1f1845c4702bf2567e6b9ca1f1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-overview"></a>Omówienie usług Reliable Services
Sieć szkieletowa usług Azure upraszcza zapisywanie i bezstanowe i stanowe niezawodne usługi zarządzania. W tym temacie omówiono:

* Witaj niezawodne usługi programowania modelu dla usług bezstanowych i stanowych.
* Opcje Hello masz toomake podczas zapisywania niezawodnej usługi.
* Niektóre scenariusze i przykłady sytuacji, w których toouse niezawodny usług i jak są one napisane.

Niezawodne usługi jest jednym z hello programowania modele dostępne w sieci szkieletowej usług. Witaj innych jest hello niezawodnego aktora programowania modelu, który zapewnia wirtualnego model programowania aktora na powitania niezawodne usługi modelu. Aby uzyskać więcej informacji o modelu programowania Reliable Actors hello, zobacz [tooService wprowadzenie sieci szkieletowej Reliable Actors](service-fabric-reliable-actors-introduction.md).

Usługa Service Fabric zarządza istnienia hello usług, od aprowizacji i wdrożenia w ramach uaktualniania i usuwania, za pomocą [zarządzania aplikacjami sieci szkieletowej usług](service-fabric-deploy-remove-applications.md).

## <a name="what-are-reliable-services"></a>Co to są niezawodne usługi?
Niezawodne usługi udostępnia prostą, zaawansowane, najwyższego poziomu, express, co jest ważne tooyour aplikacji toohelp modelu programowania. Model programowania usług niezawodnej hello otrzymasz:

* Pozostałe toohello dostępu hello programowania interfejsów API sieci szkieletowej usług. W przeciwieństwie do usługi sieci szkieletowej usług formę [pliki wykonywalne gościa](service-fabric-deploy-existing-app.md), niezawodne usługi bezpośrednio uzyskać toouse hello reszty hello interfejsów API usługi Service Fabric. Dzięki temu usługi do:
  * system hello zapytania
  * Raport kondycji temat jednostek w klastrze hello
  * odbieranie powiadomień o zmianach dotyczących konfiguracji i kod
  * Wyszukiwanie i komunikowanie się z innymi usługami
  * (opcjonalnie) użyć hello [niezawodnej kolekcje](service-fabric-reliable-services-reliable-collections.md)
  * .. .a, zapewniając im dostępu toomany innych funkcji, wszystkie z pierwszej klasie model programowania w wielu językach programowania.
* Prostego modelu do uruchamiania z własnego kodu, który wygląda jak modeli, które są używane do programowania. Kod ma punktu wejścia dobrze zdefiniowany i łatwe do zarządzania cyklem życia.
* Model podłączany komunikacji. Użyj transportu hello wybranych przez użytkownika, takich jak HTTP z [interfejsu API sieci Web](service-fabric-reliable-services-communication-webapi.md), Websocket, niestandardowe protokoły TCP lub innych elementów. Niezawodne usługi zapewniają dużą niektóre opcje poza pole można użyć lub Podaj własny.
* Dla stanowych usług modelu programowania usług niezawodnej hello pozwala tooconsistently i niezawodne przechowywanie swój stan wewnątrz usługi przy użyciu [niezawodnej kolekcje](service-fabric-reliable-services-reliable-collections.md). Niezawodne kolekcje są prostym zestawem klasy wysokiej dostępności i niezawodne kolekcji, które mają być znane tooanyone, który został użyty kolekcje C#. Tradycyjnie usług niezbędnych systemów zewnętrznych dla zarządzania stanem niezawodne. Z kolekcjami niezawodne, można przechowywać stanu obliczeniowych tooyour dalej z hello tego samego wysoka dostępność i niezawodność znasz tooexpect dostarczanych ze sklepów zewnętrznych wysokiej dostępności. Ten model również poprawia czas oczekiwania, ponieważ kolokacja hello obliczeniowych i musi on toofunction stanu.

Obejrzyj ten film Microsoft Virtual Academy omówienie niezawodne usługi:<center>
<a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=HhD9566yC_4106218965">
<img src="./media/service-fabric-reliable-services-introduction/ReliableServicesVid.png" WIDTH="360" HEIGHT="244" />
</a>
</center>

## <a name="what-makes-reliable-services-different"></a>Niezawodne usługi dzięki czemu różne?
Niezawodne usługi w sieci szkieletowej usług różnią się od usługi, które zostały zapisane przed. Usługa Service Fabric realizuje niezawodności, dostępności, spójność i skalowalność.

* **Niezawodność** — Twoja usługa pozostaje się nawet w środowiskach zawodnych gdzie maszynach się nie powieść lub kliknij przycisk problemy z siecią lub w przypadkach, gdy hello usług wystąpienia błędów i awarii lub się nie powieść. Dla stanowych usług swój stan jest zachowywana nawet w obecności hello sieci lub inne błędy.
* **Dostępność** -usługa jest osiągalny i szybko reagowały. Sieć szkieletowa usług przechowuje żądaną liczbę kopii uruchomiona.
* **Skalowalność** — usługi są całkowicie niezależna od konkretnego sprzętu i ich można zwiększać i zmniejszać w razie potrzeby za pośrednictwem hello Dodawanie lub usuwanie sprzętu lub inne zasoby. Usługi są tooensure łatwo partycjonowanej (szczególnie w przypadku stanowego hello), który można skalować usługi hello i dojście błędy częściowe. Usługi mogą być tworzone i usuwane dynamicznie za pośrednictwem kodu, włączanie więcej toobe wystąpień przejścia w razie potrzeby, powiedz w żądaniach toocustomer odpowiedzi. Ponadto usługi sieć szkieletowa zachęca lightweight toobe usług. Sieć szkieletowa usług umożliwia tysiące toobe usługi udostępniane w ramach jednego procesu, zamiast konieczności lub przypisywanie całego wystąpień systemu operacyjnego lub procesów tooa pojedynczego wystąpienia usługi.
* **Spójność** -wszystkie informacje przechowywane w tej usłudze można zagwarantować toobe spójne. Dotyczy to nawet przez wiele kolekcji niezawodnej w ramach usługi. Zmiany w kolekcjach, w ramach usługi można podjąć w sposób transakcyjnie atomic.

## <a name="service-lifecycle"></a>Usługi cyklu życia
Czy usługa jest stanowego lub bezstanowego, niezawodne usługi zapewniają prosty cykl pozwala szybko podłączenia w kodzie i rozpocząć pracę.  Istnieje tylko jeden lub dwa metod należy tooimplement tooget usługi do pracy.

* **CreateServiceReplicaListeners/CreateServiceInstanceListeners** — ta metoda jest, gdzie usługa hello definiuje stack(s) komunikacji hello chce toouse. Witaj stosu komunikacji, takie jak [interfejsu API sieci Web](service-fabric-reliable-services-communication-webapi.md), jest definiuje co hello punktu końcowego nasłuchiwania lub punktów końcowych dla hello service (jak klienci dotarcia hello usługi). Definiuje także interakcję wiadomości powitania, które są wyświetlane z hello reszty hello kodu usługi.
* **RunAsync** — ta metoda jest usługą, w którym odbywa się jej logiki biznesowej i gdzie może rozpocząć Wyłącz wszystkie zadania w tle, które powinny być uruchamiane dla okresu istnienia hello hello usługi. token anulowania Hello, który został dostarczony jest sygnał dla podczas pracy ma zostać zatrzymana. Na przykład jeśli usługa hello musi wiadomości toopull poza kolejka niezawodnych i przetwarzanie ich, to gdzie się stanie, które działają.

Jeśli zapoznawania się o usługach reliable services dla powitania po raz pierwszy, przeczytaj na! Jeśli szukasz szczegółowe wskazówki dotyczące cyklu życia hello niezawodnych usług można potrzebny przez zbyt[w tym artykule](service-fabric-reliable-services-lifecycle.md).

## <a name="example-services"></a>Przykład usług
Znajomość tego modelu programowania, Spójrzmy szybki w dwóch różnych usług toosee, jak te dopasowania.

### <a name="stateless-reliable-services"></a>Bezstanowej niezawodnej usługi
Usługi bezstanowej jest jeden, gdy stan jest niedostępny przechowywanych w usłudze hello w wielu wywołań. Stan jest obecny jest całkowicie jednorazowe i nie wymaga synchronizacji, replikacji, trwałości i wysokiej dostępności.

Rozważmy na przykład Kalkulator, Brak pamięci i odbiera wszystkie tooperform warunków i operacji na raz.

W takim przypadku hello `RunAsync()` (C#) lub `runAsync()` (Java) hello usługi może być pusta, ponieważ nie istnieje żadne tła przetwarzania zadań usługi hello musi toodo. Po utworzeniu usługi Kalkulator hello zwraca `ICommunicationListener` (C#) lub `CommunicationListener` (Java) (na przykład [interfejsu API sieci Web](service-fabric-reliable-services-communication-webapi.md)) która otwiera punktu końcowego nasłuchiwania na porcie niektórych. Przechwytuje tego punktu końcowego nasłuchiwania toohello innej obliczania metod (przykład: "Dodaj (n1, n2)") definiującą Kalkulator hello publiczny interfejs API.

Gdy wywołanie z klienta hello odpowiednia metoda jest wywoływana, i usługi Kalkulator hello wykonuje operacje hello na powitania danych pod warunkiem i zwraca wynik hello. Go nie przechowuje jakikolwiek stan.

Nie są przechowywane wszystkie stan wewnętrzny upraszcza Kalkulator tego przykładu. Jednak większość usług nie są naprawdę bezstanowych. Zamiast tego należy ich oddzielenie toosome ich stanu innym magazynie. (Na przykład dowolnej aplikacji sieci web, która opiera się na przechowywanie stanu sesji w sklepie zapasowy lub w pamięci podręcznej nie jest bezstanowych.)

Typowym przykładem bezstanowego jak usług są używane w sieci szkieletowej usług jest jako fronton czy ujawnia hello publicznych API dla aplikacji sieci web. Usługa frontonu Hello komunikuje następnie toostateful usług toocomplete żądania użytkownika. W takim przypadku wywołania z klientów są ukierunkowanej tooa znane portem, np. 80, którym nasłuchuje usługa bezstanowa hello. Odbiera hello wywołania tej usługi bezstanowej i określa, czy wywołanie hello pochodzi z zaufanego firm i której usługi jest przeznaczony do.  Następnie usługi bezstanowej hello przekazuje hello wywołania toohello poprawne partycji usługi stanowej hello i czeka na odpowiedź. Gdy usługa bezstanowa hello odbiera odpowiedź, odpowiedzi klienta oryginalnym toohello. Przykładem takiej usługi znajduje się w naszej próbki [C#](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started) / [Java](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Actors/VisualObjectActor/VisualObjectWebService). To jest tylko jeden przykład tego wzorca w próbkach hello, inne osoby w istnieją także inne przykłady.

### <a name="stateful-reliable-services"></a>Stanowe niezawodne usługi
Usługi stanowej to taki, który musi mieć część stanu zachowana spójne i znajdują się w kolejności dla hello toofunction usługi. Należy wziąć pod uwagę to usługa, która stale oblicza średnią kroczącą pewnej wartości na podstawie aktualizacji, który odbiera. toodo, musi mieć hello bieżącego zestawu żądań przychodzących, musi on tooprocess i hello bieżącego średnia. Wszystkie usługi, która pobiera, procesów i zapisuje informacje w zewnętrznym sklepie (np. Azure blob lub tabeli magazynu dzisiaj) jest obiektem stanowym. Śledzi tylko jego stanu w magazynie stanów zewnętrznych hello.

Większość usług dzisiaj przechowywane zewnętrznie, ich stanie, ponieważ zewnętrznym sklepie hello jest, co zapewnia niezawodność, dostępność, skalowalność i spójności dla tego stanu. W sieci szkieletowej usług, usług nie są wymagane toostore zewnętrznie ich stan. Te wymagania dla kodu usługi hello i stan usługi hello odpowiada on za sieci szkieletowej usług.

> [!NOTE]
> Obsługa stanowych usług Reliable Services nie jest dostępna w systemie Linux jeszcze (dla C# lub języka Java).
>

Załóżmy, że chcemy toowrite usługa, która przetwarza obrazów. toodo to hello usługi powoduje obrazu i hello serii tooperform konwersje w tym obrazie. Ta usługa zwraca odbiornik komunikacji (teraz załóżmy, że jest WebAPI) czy ujawnia interfejs API, takich jak `ConvertImage(Image i, IList<Conversion> conversions)`. Po odebraniu żądania usługa hello przechowuje je w `IReliableQueue`i zwraca niektórych identyfikator toohello klienta, więc można śledzić hello żądania.

W tej usłudze `RunAsync()` może być bardziej złożonych. Usługa Hello ma pętlę w jego `RunAsync()` który ściąga żądań z `IReliableQueue` i wykonuje konwersje hello żądanie. wyniki Hello pobrać przechowywane w `IReliableDictionary` tak, aby po wróci powitania klienta może uzyskać przekonwertowanego obrazów. tooensure, że nawet jeśli coś nie powiedzie się obraz powitania nie zostanie utracony, ta usługa niezawodnej czy ściągnięcia poza hello kolejki, wykonywania konwersji hello i przechowywać wynik hello w ramach pojedynczej transakcji. W takim przypadku wiadomość hello zostanie usunięta z kolejki hello i hello wyniki są przechowywane w słowniku wynik hello, tylko wtedy, gdy konwersje hello są spełnione. Alternatywnie usługa hello można ściągnąć obraz powitania poza hello kolejki i natychmiast przechowywania w magazynie zdalnym. Zmniejsza to hello ilość usługa hello stanu ma toomanage, ale zwiększa złożoności, ponieważ usługa hello ma tookeep hello metadane potrzebne toomanage hello zdalnego magazynu. Albo podejście jeśli coś nie powiodła się w hello środkowej hello żądania nie będzie w toobe oczekiwania kolejki hello przetworzone.

Jeden element toonote o tej usługi jest wydaje, takich jak usługi .NET w normalnym! Witaj jedyna różnica polega na że struktury danych hello używana (`IReliableQueue` i `IReliableDictionary`) są dostarczane przez sieć szkieletowa usług i są wysoce niezawodnych, dostępna i spójne.

## <a name="when-toouse-reliable-services-apis"></a>Gdy toouse niezawodnej usługi interfejsów API
Jedną z następujących przyczyn hello scharakteryzowania wymagań usługi aplikacji, należy rozważyć niezawodnej usługi interfejsów API:

* Kod z usługą (i opcjonalnie stanu) toobe wysokiej dostępności i niezawodnych
* Należy transakcyjne gwarancje w wielu jednostkach stanu (na przykład zleceń i kolejność pozycji).
* Stan aplikacji mogą być naturalnie modelowane jako wiarygodnych słowniki i kolejek.
* Stan lub kodu aplikacji musi toobe wysokiej dostępności z niskim opóźnieniem odczyty i zapisy.
* Aplikacja wymaga współbieżności hello toocontrol lub szczegółowości Operacje transakcyjne na co najmniej jednej kolekcji niezawodnej.
* Potrzebujesz komunikacji hello toomanage lub hello kontroli partycjonowania schematu dla usługi.
* Kod wymaga środowiska uruchomieniowego bezwątkowy.
* Aplikacja wymaga toodynamically tworzenia lub usuwania słowników niezawodnej lub kolejek lub całej usługi w czasie wykonywania.
* Należy tooprogrammatically wprowadzone do usługi Service Fabric i przywracania kopii zapasowej funkcje kontroli stanu usługi.
* Aplikacja wymaga toomaintain historii zmian dla jednostki jego stanu.
* Mają toodevelop lub korzystać z dostawców innych firm — rozwinięte, niestandardowe stanu.

## <a name="next-steps"></a>Następne kroki
* [Niezawodne usługi szybki start](service-fabric-reliable-services-quick-start.md)
* [Niezawodne usługi advanced użycia](service-fabric-reliable-services-advanced-usage.md)
* [Witaj modelu programowania Reliable Actors](service-fabric-reliable-actors-introduction.md)
