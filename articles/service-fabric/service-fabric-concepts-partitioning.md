---
title: "usługi sieci szkieletowej usług aaaPartitioning | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toopartition sieci szkieletowej usług stanowych usług. Partycje umożliwia przechowywanie danych na maszynach lokalne powitania, danych i zasobów obliczeniowych mogą być skalowane razem."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3b7248c8-ea92-4964-85e7-6f1291b5cc7b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: msfussell
ms.openlocfilehash: 6ead48716c08f4212535202ee69d169067d5c6d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="partition-service-fabric-reliable-services"></a>Niezawodne usługi Service Fabric partycji
Ten artykuł zawiera toohello wprowadzenie podstawowe pojęcia partycjonowania niezawodne usługi sieć szkieletowa usług Azure. Witaj używane w artykule hello kod źródłowy jest również dostępna w [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).

## <a name="partitioning"></a>Partycjonowanie
Partycjonowanie nie jest unikatowy tooService sieci szkieletowej. W rzeczywistości jest wzorzec core tworzenie skalowalnych usług. W szerszym znaczeniu możemy pomyśleć o partycjonowania jako koncepcji podziału stanu (dane) i obliczeniowe na mniejsze jednostki dostępne tooimprove skalowalność i wydajność. Dobrze znane formularz partycjonowania [partycjonowanie danych][wikipartition], znanej również jako dzielenia na fragmenty.

### <a name="partition-service-fabric-stateless-services"></a>Usługi bezstanowej partycji sieci szkieletowej usług
W przypadku usług bezstanowych należy zwrócić uwagę partycji trwa jednostki logicznej, która zawiera co najmniej jedno wystąpienie usługi. Rysunek 1 pokazuje usługi bezstanowej wystąpieniami pięć dystrybuowana do klastra przy użyciu jednej partycji.

![Usługi bezstanowej](./media/service-fabric-concepts-partitioning/statelessinstances.png)

Naprawdę są dwa typy rozwiązań usług bezstanowych. Witaj najpierw jeden to usługa, która będzie się powtarzał stanu zewnętrznie, na przykład w bazie danych Azure SQL (np. sieci Web, która przechowuje informacje o sesji hello i danych). Hello drugim jest tylko do obliczenia usług (takich jak obraz lub Kalkulator tworzenie miniatur) nie zarządzających każdy stan trwały.

W przypadku partycjonowania usługi bezstanowej jest bardzo rzadko scenariusza — skalowalność i dostępność zwykle są osiągane przez dodanie więcej wystąpień. czas tylko Hello ma tooconsider jest wiele partycji dla wystąpień usługi bezstanowej, gdy potrzebne są specjalne routingu toomeet żądań.

Na przykład należy wziąć pod uwagę przypadek, w którym użytkownicy z identyfikatorami w pewnym powinien być obsługiwany tylko przez wystąpienie określonej usługi. Innym przykładem po można partycji usługi bezstanowej jest masz naprawdę partycjonowanej wewnętrznej bazy danych (np. podzielony na niezależne fragmenty bazy danych SQL) i ma toocontrol wystąpieniu usługi, z którym należy zapisać toohello niezależnego fragmentu bazy danych — lub wykonywać inne zadania przygotowywania w Witaj usługi bezstanowej, która wymaga hello takie same informacje o partycjach jest używany w hello wewnętrznej bazy danych. Tego typu scenariusze można także rozwiązać na różne sposoby i nie wymagają partycjonowania usługi.

Witaj pozostałej części tego przewodnika koncentruje się na usług stanowych.

### <a name="partition-service-fabric-stateful-services"></a>Usługi stanowej partycji sieci szkieletowej usług
Sieć szkieletowa usług ułatwia skalowalnych usług stanowych łatwe toodevelop oferując najwyższej jakości sposób toopartition stanu (dane). Koncepcyjnie, należy zwrócić uwagę partycji usługi stanowej jako jednostkę skalowania, która jest wysoce niezawodne za pośrednictwem [replik](service-fabric-availability-services.md) rozproszonych, się równoważone hello węzłów w klastrze.

Podział na partycje w kontekście hello usługi sieć szkieletowa usług stanowych odwołuje się toohello proces określania, czy partycja określonej usługi jest odpowiedzialny za część hello stan ukończenia hello usługi. (Jak wspomniano wcześniej, partycji jest zestawem [replik](service-fabric-availability-services.md)). Największą zaletą sieci szkieletowej usług jest umieszczenie hello partycji, w różnych węzłach. Dzięki temu są limit zasobów toogrow tooa węzła. Potrzeb danych hello powiększania, partycje wzrostu i sieci szkieletowej usług rebalances partycji w węzłach. Dzięki temu hello nadal efektywne wykorzystanie zasobów sprzętowych.

toogive możesz przykład powiedzieć możesz rozpoczyna się od 5 węzłów klastra i usługi, która jest skonfigurowany toohave 10 partycji i elementem docelowym trzy repliki. W takim przypadku sieci szkieletowej usług może równoważyć i rozpowszechniają replik hello klastra hello — i pojawiłyby się dwóch podstawowych [replik](service-fabric-availability-services.md) na węzeł.
Teraz tooscale limit hello too10 węzłach, należy sieci szkieletowej usług będzie ponowne zrównoważenie podstawowy hello [replik](service-fabric-availability-services.md) we wszystkich węzłach 10. Podobnie skalowania wstecz too5 węzłów, sieci szkieletowej usług będzie ponowne zrównoważenie wszystkie repliki hello węzłów hello 5.  

Rysunek 2 przedstawia dystrybucji hello 10 partycji przed i po skalowanie hello klastra.

![Usługi stanowej](./media/service-fabric-concepts-partitioning/partitions.png)

W związku z tym uzyskuje się hello skalowalnego w poziomie, ponieważ żądania klientów są rozproszone na komputerach, poprawia ogólną wydajność aplikacji hello i zmniejsza się rywalizacji toochunks dostępu do danych.

## <a name="plan-for-partitioning"></a>Planowanie podziału na partycje
Przed wdrożeniem usługi, zawsze należy rozważyć hello partycjonowania strategii, która jest wymagana tooscale wychodzących. Istnieją różne sposoby, ale ich wszystkich skupić się na jakie aplikacja hello musi tooachieve. Dla kontekstu hello w tym artykule zastanówmy się niektóre hello aspekty większe znaczenie.

Dobrym rozwiązaniem jest toothink informacje o strukturze hello hello stanu, który wymaga toobe podzielona na partycje, jako pierwszy krok hello.

Spójrzmy prosty przykład. Gdyby toobuild usługę countywide sondowania, można utworzyć partycji każdemu miastu w hello województwo. Następnie można przechowywać hello głosów dla każdej osoby w mieście hello w hello partycji, która odpowiada toothat miasta. Rysunek 3 przedstawia zestaw miasta osoby i hello, w którym znajdują się.

![Proste partycji](./media/service-fabric-concepts-partitioning/cities.png)

Jako różni populacji hello miast, może to spowodować niektóre partycje, które zawierają dużą ilość danych (np. Seattle) i innych partycji z bardzo mało stanu (np. Kirkland). Co to jest wpływ hello partycji z nierówna ilości stan?

Jeśli myślisz o przykład Witaj ponownie, można łatwo zobaczyć, czy hello partycji, która przetrzymuje hello głosami Seattle otrzymają więcej ruchu niż Kirkland hello, co. Domyślnie usługa sieć szkieletowa sprawia, że upewnić się, że o hello tej samej liczby podstawowych i pomocniczych replik w każdym węźle. Dlatego użytkownik może pozostać z węzłami zawierających repliki obsługujących więcej ruchu oraz inne osoby, które obsługiwać mniej ruchu. Najlepiej warto tooavoid gorących i zimnych miejsc, takich jak to w klastrze.

W celu tooavoid to, z punktu widzenia partycjonowania należy wykonać dwie czynności:

* Spróbuj toopartition hello stanu, dzięki czemu jest rozmieszczana równomiernie wzdłuż wszystkie partycje.
* Załaduj raport z każdej repliki hello hello usługi. (Aby uzyskać informacje na temat, zapoznaj się w tym artykule na [metryki i obciążenia](service-fabric-cluster-resource-manager-metrics.md)). Usługi Service Fabric zawiera obciążenia tooreport możliwości hello wykorzystanych w ramach usług, takich jak ilość pamięci lub liczbę rekordów. Oparte na powitania metryki zgłoszone, sieci szkieletowej usług wykryje, że niektóre partycje służy obciążeń wyższe niż inne i rebalances hello klastra przez przenoszenie replik toomore odpowiedniego węzły tak, aby ogólna żaden węzeł nie jest przeciążona.

Czasami nie wiedzieć, jak dużo danych będzie w danej partycji. Dzięki ogólne zalecenie jest toodo zarówno — najpierw, przyjmując strategii partycjonowania które rozprzestrzeniają się hello danych równomiernie między hello partycji i sekundę, przez raportowania obciążenia.  Pierwsza metoda Hello zapobiega sytuacji opisanych w hello głosowania przykład, gdy hello drugi pomaga smooth różnic tymczasowego dostępu lub obciążenia wraz z upływem czasu.

Innym aspektem planowania partycji jest toochoose hello poprawną liczbę partycji toobegin z.
Z punktu widzenia usługi sieć szkieletowa nie ma nic uniemożliwiający uruchamiania o większej liczby partycji niż zakładano dla danego scenariusza.
W rzeczywistości przy założeniu hello maksymalną liczbę partycji jest prawidłowy podejście.

W rzadkich przypadkach może to spowodować wymagające partycje więcej niż początkowo wybrana. Liczba partycji hello nie można zmienić po hello fakt, będzie potrzebny tooapply podejścia niektórych zaawansowanych partycji, takich jak tworzenie nowego wystąpienia usługi hello sam typ usługi. Musisz także tooimplement niektórych logiki po stronie klienta, który przekierowuje hello żądań wystąpienie usługi poprawne toohello, na podstawie wiedzy po stronie klienta, który musi obsługiwać kodu klienta.

Inną ważną kwestią dotyczącą partycjonowania planowania jest hello komputera dostępne zasoby. Stan hello potrzeb toobe dostępne i przechowywane, jest powiązane toofollow:

* Limity przepustowości sieci
* Limity pamięci systemu
* Limity magazynu na dysku

Dlatego co się stanie po uruchomieniu na ograniczenia zasobów w klastrze uruchomione? odpowiedź Hello jest, może po prostu skalowanie w poziomie hello klastra tooaccommodate hello nowe wymagania.

[Przewodnik planowania pojemności Hello](service-fabric-capacity-planning.md) zawiera wskazówki dotyczące toodetermine liczbę węzłów klastra musi.

## <a name="get-started-with-partitioning"></a>Wprowadzenie do partycjonowania
W tej sekcji opisano, jak tooget pracę z usługą partycjonowania.

Sieć szkieletowa usług oferuje możliwość wyboru trzy schemat partycji:

* W granicach partycjonowanie (znany także jako UniformInt64Partition).
* O nazwie partycjonowania. Aplikacje zazwyczaj przy użyciu tego modelu istnieją dane, które można bucketed w ramach ograniczonego zestawu. Typowe przykłady pola danych używane jako klucze partycji o nazwie będzie regionów, kodów pocztowych, grupy odbiorców lub granice innych firm.
* Pojedyncze partycjonowania. Pojedyncze partycje są zazwyczaj używane do usługi hello nie wymaga żadnych dodatkowych routingu. Na przykład usług bezstanowych Użyj ten schemat partycjonowania domyślnie.

O nazwie i schematy partycjonowania Singleton to specjalne rodzaje ranged partycji. Domyślnie hello szablony Visual Studio do użytku w sieci szkieletowej usług w granicach partycje, ponieważ jest on hello najczęstszych i najbardziej przydatnych jeden. Witaj dalszej części tego artykułu koncentruje się na powitania ranged schemat partycjonowania.

### <a name="ranged-partitioning-scheme"></a>Schemat partycjonowania w granicach
Jest to używane toospecify całkowitą zakresu (określone przez niska wartość klucza i wysoka wartość klucza) i liczba partycji (n). Tworzy partycje n, każdy odpowiedzialny za nienakładający tekst Podzakres hello zakresem kluczy partycji: Ogólne. Na przykład ranged schemat partycjonowania kluczem niski 0, wysoka wartość klucza 99 oraz liczbę 4 utworzyć cztery partycje, jak pokazano poniżej.

![Zakres partycji](./media/service-fabric-concepts-partitioning/range-partitioning.png)

Typowym podejściem jest toocreate skrót oparte na zestawie danych hello Unikatowy klucz. Typowe przykłady klucze będą numer identyfikacyjny (VIN), identyfikator pracownika i unikatowym ciągiem. Za pomocą tego Unikatowy klucz, czy następnie wygenerować skrótu, modulo hello klucza zakresu, toouse jako klucz. Można określić hello górne i dolne granice hello dopuszczalny zakres klucza.

### <a name="select-a-hash-algorithm"></a>Wybierz algorytm wyznaczania wartości skrótu
Ważnym elementem wyznaczania wartości skrótu jest wybranie sieci algorytmu wyznaczania wartości skrótu. Wchodzi w grę jest czy hello celem jest podobnych kluczy toogroup obok siebie (miejscowości poufnych wyznaczania wartości skrótu)--lub jeśli działanie powinien zostać przekazany szeroko wszystkich partycji (dystrybucji mieszania), która jest najczęściej.

właściwości Hello dobrej algorytmu wyznaczania wartości skrótu są jest łatwe toocompute, składa się z kilku kolizji i rozpowszechnia klucze hello równomiernie. Dobrym przykładem algorytmu wyznaczania wartości skrótu wydajne jest hello [FNV 1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) algorytmu wyznaczania wartości skrótu.

Hello jest dobrym zasobu dla skrótu ogólne kod algorytmu opcji [Wikipedia strony na funkcje skrótu](http://en.wikipedia.org/wiki/Hash_function).

## <a name="build-a-stateful-service-with-multiple-partitions"></a>Tworzenie usługi stanowej z wieloma partycjami
Utwórz pierwszy niezawodnej usługi stanowej z wieloma partycjami. W tym przykładzie utworzysz bardzo prostej aplikacji, w którym ma być toostore wszystkich ostatnich o nazwach zaczynających hello sam list w hello tej samej partycji.

Przed przystąpieniem do napisania kodu, należy toothink dotyczące hello partycji i kluczy partycji. Potrzebne są 26 partycje, (po jednej dla każdej litery alfabetu hello), ale co o hello niski i wysoki klucz?
Ponieważ chcemy dosłownie toohave jedną partycję na literę, możemy użyć 0 jako hello niska wartość klucza i 25 jako hello wysoka wartość klucza, jak litera każdego jest własnego klucza.

> [!NOTE]
> To jest uproszczone scenariusz, w rzeczywistości byłoby nierówna dystrybucja hello. Nazwisk, począwszy od litery hello "S" lub "M" są częściej niż hello te począwszy "X" lub "Y".
> 
> 

1. Otwórz **programu Visual Studio** > **pliku** > **nowe** > **projektu**.
2. W hello **nowy projekt** oknie dialogowym Wybierz hello sieci szkieletowej usług aplikacji.
3. Wywołanie "AlphabetPartitions" hello projektu.
4. W hello **Tworzenie usługi** oknie dialogowym wybierz **Stateful** usługi i wywołać go "Alphabet.Processing", jak pokazano w poniższym obrazie hello.
       ![Okno dialogowe nowej usługi w programie Visual Studio][1]

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. Ustaw numer hello partycji. Otwórz hello pliku Applicationmanifest.xml się w hello folderu ApplicationPackageRoot hello AlphabetPartitions projektu i zaktualizuj hello parametru too26 Processing_PartitionCount, jak pokazano poniżej.
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    Należy również tooupdate hello LowKey i właściwości HighKey elementu klasy StatefulService hello w hello ApplicationManifest.xml, jak pokazano poniżej.
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. Dla toobe usługi hello jest dostępny otwarcie punktu końcowego na porcie przez dodanie elementu punktu końcowego hello ServiceManifest.xml (znajdujący się w folderze elementu PackageRoot hello) dla hello Alphabet.Processing usługi, jak pokazano poniżej:
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    Obecnie usługa hello jest skonfigurowany toolisten tooan wewnętrzny punkt końcowy z partycjami 26.
7. Następnie należy toooverride hello `CreateServiceReplicaListeners()` metody klasy hello przetwarzania.
   
   > [!NOTE]
   > Dla tego przykładu przyjęto założenie, używasz HttpCommunicationListener proste. Aby uzyskać więcej informacji dotyczących komunikacji niezawodnej usługi, zobacz [model komunikacji niezawodnej usługi hello](service-fabric-reliable-services-communication.md).
   > 
   > 
8. Zalecane wzorzec hello adresu URL, który nasłuchuje repliki jest zgodny z formatem hello: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.
    Dlatego ma tooconfigure toolisten odbiornik komunikacji na powitania poprawne punktów końcowych i z tego wzorca.
   
    Wiele replik tej usługi może być hostowana na powitania tym samym komputerze, więc ten adres musi toobe unikatowy toohello repliki. Jest to, dlaczego identyfikator partycji: + identyfikator repliki są w adresie URL hello. HttpListener może nasłuchiwać na wielu adresów w powitalne portu takie same jak prefiksu adresu URL hello jest unikatowa.
   
    Witaj, dodatkowe identyfikator GUID jest przeznaczony dla zaawansowanych case, gdzie również nasłuchiwanie żądań tylko do odczytu replikach pomocniczych. W takim przypadku hello ma toomake się, że nowy unikatowy adres jest używany podczas przejścia z podstawowego toosecondary tooforce klientów toore rozwiązanie hello adresu. jest używany jako adres hello tutaj, aby hello funkcja replica nasłuchuje na wszystkich dostępnych hostów (IP, FQDM, localhost itp.) hello kod poniżej przedstawiono przykład ' +'.
   
    ```CSharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
         return new[] { new ServiceReplicaListener(context => this.CreateInternalListener(context))};
    }
    private ICommunicationListener CreateInternalListener(ServiceContext context)
    {
   
         EndpointResourceDescription internalEndpoint = context.CodePackageActivationContext.GetEndpoint("ProcessingServiceEndpoint");
         string uriPrefix = String.Format(
                "{0}://+:{1}/{2}/{3}-{4}/",
                internalEndpoint.Protocol,
                internalEndpoint.Port,
                context.PartitionId,
                context.ReplicaOrInstanceId,
                Guid.NewGuid());
   
         string nodeIP = FabricRuntime.GetNodeContext().IPAddressOrFQDN;
   
         string uriPublished = uriPrefix.Replace("+", nodeIP);
         return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInternalRequest);
    }
    ```
   
    Warto również zauważyć tego hello opublikowane adres URL jest nieco inne niż hello nasłuchiwania prefiksu adresu URL.
    adres URL nasłuchiwania Hello otrzymuje tooHttpListener. Witaj, opublikowanego adresu URL jest hello adresu URL opublikowanego toohello Usługa nazewnictwa sieci szkieletowej usług, który służy do odnajdywania usługi. Ten adres za pomocą usługi odnajdywania poprosi klientów. adres Hello, że klienci otrzymują potrzeb toohave hello rzeczywisty adres IP lub nazwa FQDN węzła hello tooconnect kolejności. Dlatego należy tooreplace "+" z hello węzła IP lub nazwa FQDN jak pokazano powyżej.
9. ostatni krok Hello jest hello tooadd przetwarzania logiki toohello usługi jak pokazano poniżej.
   
    ```CSharp
    private async Task ProcessInternalRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        string output = null;
        string user = context.Request.QueryString["lastname"].ToString();
   
        try
        {
            output = await this.AddUserAsync(user);
        }
        catch (Exception ex)
        {
            output = ex.Message;
        }
   
        using (HttpListenerResponse response = context.Response)
        {
            if (output != null)
            {
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    private async Task<string> AddUserAsync(string user)
    {
        IReliableDictionary<String, String> dictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<String, String>>("dictionary");
   
        using (ITransaction tx = this.StateManager.CreateTransaction())
        {
            bool addResult = await dictionary.TryAddAsync(tx, user.ToUpperInvariant(), user);
   
            await tx.CommitAsync();
   
            return String.Format(
                "User {0} {1}",
                user,
                addResult ? "sucessfully added" : "already exists");
        }
    }
    ```
   
    `ProcessInternalRequest`Odczyty hello wartości hello zapytania ciąg używany parametr toocall hello partycji i wywołania `AddUserAsync` tooadd hello nazwisko toohello niezawodnej słownika `dictionary`.
10. Dodajmy toosee projektu toohello usługi bezstanowej sposób może wywołać określonej partycji.
    
    Ta usługa służy jako prosty interfejs sieci web akceptuje nazwisko hello jako parametr ciągu zapytania, określa hello klucz partycji i wysyła je toohello Alphabet.Processing usługi do przetwarzania.
11. W hello **Tworzenie usługi** oknie dialogowym wybierz **Stateless** usługi i nadaj mu "Alphabet.Web", jak pokazano poniżej.
    
    ![Zrzut ekranu usługi bezstanowej](./media/service-fabric-concepts-partitioning/createnewstateless.png).
12. Zaktualizuj informacje o punkcie końcowym hello w hello ServiceManifest.xml hello Alphabet.WebApi usługi tooopen zapasowej portu, jak pokazano poniżej.
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. Należy tooreturn kolekcję ServiceInstanceListeners w klasie hello sieci Web. Ponownie możesz wybrać tooimplement HttpCommunicationListener proste.
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is hello node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. Teraz należy tooimplement hello przetwarzania logiki. Witaj wywołania HttpCommunicationListener `ProcessInputRequest` gdy nadejdzie żądanie. Dlatego spróbuj teraz i Dodaj poniższy kod hello.
    
    ```CSharp
    private async Task ProcessInputRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        String output = null;
        try
        {
            string lastname = context.Request.QueryString["lastname"];
            char firstLetterOfLastName = lastname.First();
            ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    
            ResolvedServicePartition partition = await this.servicePartitionResolver.ResolveAsync(alphabetServiceUri, partitionKey, cancelRequest);
            ResolvedServiceEndpoint ep = partition.GetEndpoint();
    
            JObject addresses = JObject.Parse(ep.Address);
            string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
            UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
            primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
            string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    
            output = String.Format(
                    "Result: {0}. <p>Partition key: '{1}' generated from hello first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
                    result,
                    partitionKey,
                    firstLetterOfLastName,
                    lastname,
                    partition.Info.Id,
                    primaryReplicaAddress);
        }
        catch (Exception ex) { output = ex.Message; }
    
        using (var response = context.Response)
        {
            if (output != null)
            {
                output = output + "added tooPartition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    Przejdźmy krok po kroku. Kod Hello odczytuje hello pierwszą literę parametru ciągu zapytania hello `lastname` na wartość typu char. Następnie określa klucz partycji hello na list przez odjęcie wartości szesnastkowej hello `A` z wartości szesnastkowej hello hello nazwisk pierwszą literę.
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    Pamiętaj, że w tym przykładzie używamy 26 partycje z jedną partycję kluczem dla każdej partycji.
    Następnie możemy uzyskać partycji usługi hello `partition` dla tego klucza przy użyciu hello `ResolveAsync` metody na powitania `servicePartitionResolver` obiektu. `servicePartitionResolver`nie zdefiniowano jako
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    Witaj `ResolveAsync` identyfikator URI usługi hello ma metodę, hello klucz partycji i token anulowania jako parametry. Witaj identyfikator URI usługi hello usługę przetwarzania jest `fabric:/AlphabetPartitions/Processing`. Następnie Pobierz punktu końcowego hello hello partycji.
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    Na koniec możemy utworzyć adres URL punktu końcowego hello plus hello querystring i Wywołaj hello usługę przetwarzania.
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    Po zakończeniu przetwarzania hello możemy zapisywać dane wyjściowe hello.
15. ostatni krok Hello jest tootest hello usługi. Visual Studio korzysta parametry aplikacji dla lokalnych i chmurze wdrożenia. Usługa hello tootest z partycjami 26 lokalnie, należy tooupdate hello `Local.xml` plików w folderze ApplicationParameters hello hello AlphabetPartitions projektu, jak pokazano poniżej:
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. Po zakończeniu wdrażania możesz sprawdzić hello usługi i wszystkie jego partycji w hello Service Fabric Explorer.
    
    ![Zrzut ekranu Eksploratora usługi sieć szkieletowa](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. W przeglądarce, należy przetestować hello partycjonowania logiki wprowadzając `http://localhost:8081/?lastname=somename`. Zobaczysz, że każdy nazwisko zaczynającym się znakiem hello tej samej litery są przechowywane w hello tej samej partycji.
    
    ![Zrzut ekranu przeglądarki](./media/service-fabric-concepts-partitioning/samplerunning.png)

Kod źródłowy całego Hello próbki hello jest dostępne na [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).

## <a name="next-steps"></a>Następne kroki
Dla informacji na temat pojęć sieci szkieletowej usług zobacz następujące hello:

* [Dostępność usług sieci szkieletowej usług](service-fabric-availability-services.md)
* [Skalowalność usługi sieci szkieletowej usług](service-fabric-concepts-scalability.md)
* [Planowanie wydajności dla aplikacji sieci szkieletowej usług](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png