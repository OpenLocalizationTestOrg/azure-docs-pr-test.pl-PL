---
title: aaaService sieci szkieletowej kopii zapasowej i przywracania | Dokumentacja firmy Microsoft
description: "Dokumentacja koncepcyjna sieci szkieletowej usługi tworzenia kopii zapasowych i przywracania"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: subramar,jessebenson
ms.assetid: 91ea6ca4-cc2a-4155-9823-dcbd0b996349
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: mcoskun
ms.openlocfilehash: e502b59c84999c3fe825167383f00a5ebd70c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-and-restore-reliable-services-and-reliable-actors"></a>Kopie zapasowe i przywracanie Reliable Services i Reliable Actors
Sieć szkieletowa usług Azure to platforma wysokiej dostępności, która replikuje stanu hello w wielu węzłach toomaintain tego wysokiej dostępności.  W związku z tym nawet w przypadku awarii jednego węzła w klastrze hello, usługi hello nadal toobe dostępne. Dublowanie w wbudowane dostarczane przez platformę hello może być wystarczające dla niektórych, w niektórych przypadkach pożądane jest, aby tooback usługi hello zapasowych (tooan zewnętrznym sklepie).

> [!NOTE]
> Jest krytyczne toobackup i przywracanie danych (i test, który działa zgodnie z oczekiwaniami), można odzyskać z scenariuszy utraty danych.
> 
> 

Na przykład usługa może być tooback zapasowych danych w kolejności tooprotect z hello następujące scenariusze:

- W przypadku hello hello trwałą utratę całego klastra sieci szkieletowej usług.
- Trwałą utratę większości hello replik partycji usługi
- Błędy administracyjne zgodnie z którymi stanu hello przypadkowo pobiera usunięte lub uszkodzony. Na przykład tak zdarzyć, jeśli administrator z uprawnieniami wystarczające błędnego usuwa hello usługę.
- Usterki w usłudze hello, które spowodować uszkodzenie danych. Na przykład może to być spowodowane uaktualnienie kodu usługi uruchamia zapisywania tooa danych błędny niezawodnej kolekcji. W takim przypadku zarówno hello kod i dane hello może mieć toobe przywrócono tooan wcześniej stanu.
- Przetwarzanie danych w trybie offline. Może być w trybie offline przetwarzania danych do analizy biznesowej, wykonywanej oddzielnie z hello usługi, które generuje dane hello toohave wygodne.

Funkcja Kopia zapasowa i przywracanie Hello umożliwia usług oparty na powitania niezawodnej usługi interfejsu API toocreate i przywracania kopii zapasowych. Witaj kopii zapasowej interfejsów API dostarczonych przez platformę hello Zezwalaj na kopie zapasowe stanu partycji usługi, bez blokowania odczytu lub zapisu. przywracania Hello interfejsów API umożliwiają przywrócone z kopii zapasowej wybrany toobe stanu partycji usługi.

## <a name="types-of-backup"></a>Typy kopii zapasowych
Dostępne są dwie opcje tworzenia kopii zapasowej: pełne i przyrostowe.
Pełna kopia zapasowa jest kopii zapasowej, który zawiera wszystkie hello wymagane toorecreate hello stan danych repliki hello: punkty kontrolne i wszystkie rekordy dziennika.
Ponieważ ma ona punkty kontrolne hello i dziennika hello, pełnej kopii zapasowej można przywracać samodzielnie.

Witaj problem z pełnych kopii zapasowych niemożliwości hello punkty kontrolne są duże.
Na przykład repliki, który ma 16 GB pamięci stanu ma punkty kontrolne, składające się z około too16 GB.
Mamy cel punktu odzyskiwania pięciu minut hello replica wymaga toobe kopii zapasowej co pięć minut.
Zawsze zapasową musi toocopy 16 GB pamięci punkty kontrolne dodatkowo too50 MB (można skonfigurować przy użyciu `CheckpointThresholdInMB`), przez jaką dzienniki.

![Przykład pełnej kopii zapasowej.](media/service-fabric-reliable-services-backup-restore/FullBackupExample.PNG)

problem toothis rozwiązania Hello jest przyrostowych kopii zapasowych, gdzie kopii zapasowej zawiera tylko rekordów dziennika hello zmienione od czasu ostatniej kopii zapasowej hello.

![Przyrostowej kopii zapasowej przykład.](media/service-fabric-reliable-services-backup-restore/IncrementalBackupExample.PNG)

Ponieważ przyrostowe kopie zapasowe są tylko zmiany od ostatniej kopii zapasowej hello (nie zawiera punktów kontrolnych hello), toobe mają zwykle szybsze, ale nie można przywrócić na ich własnych.
toorestore przyrostowej kopii zapasowej całego łańcucha kopii zapasowej hello jest wymagana.
Łańcuch kopii zapasowych łańcuch kopii zapasowych w programie pełnej kopii zapasowej i następuje numer ciągłe przyrostowych kopii zapasowych.

## <a name="backup-reliable-services"></a>Niezawodne usługi tworzenia kopii zapasowej
Witaj autor usługi ma pełną kontrolę nad tym, kiedy toomake kopii zapasowych i przechowywania kopii zapasowych.

toostart kopii zapasowej, usługa hello musi funkcji członkowskiej hello dziedziczone tooinvoke `BackupAsync`.  
Tworzenie kopii zapasowych może być utworzona tylko z repliki podstawowej i wymagają podania zapisu stanu toobe przyznane.

Jak pokazano poniżej, `BackupAsync` przyjmuje `BackupDescription` obiektu, w którym można określić pełny lub przyrostowej kopii zapasowej, a także funkcję wywołania zwrotnego, `Func<< BackupInfo, CancellationToken, Task<bool>>>` który wywoływane, gdy hello folderu kopii zapasowej został utworzony lokalnie i jest gotowy toobe przenieść się toosome magazynu zewnętrznego.

```csharp

BackupDescription myBackupDescription = new BackupDescription(backupOption.Incremental,this.BackupCallbackAsync);

await this.BackupAsync(myBackupDescription);

```

Żądanie tootake przyrostowej kopii zapasowej może zakończyć się niepowodzeniem z `FabricMissingFullBackupException`. Ten wyjątek wskazuje jeden hello następujące czynności wykonywane:

- repliki Hello nigdy nie miało pełnej kopii zapasowej, ponieważ jest on podstawowym,
- Niektóre hello rekordów dziennika, ponieważ hello ostatniej kopii zapasowej został obcięty lub
- repliki przekazany hello `MaxAccumulatedBackupLogSizeInMB` limit.

Użytkownicy mogą zwiększyć prawdopodobieństwo hello jest możliwe toodo przyrostowych kopii zapasowych przez skonfigurowanie `MinLogSizeInMB` lub `TruncationThresholdFactor`.
Należy pamiętać, że te wartości po zwiększeniu hello na użycie dysku repliki.
Aby uzyskać więcej informacji, zobacz [niezawodnej usługi konfiguracji](service-fabric-reliable-services-configuration.md)

`BackupInfo`zawiera informacje dotyczące tworzenia kopii zapasowej hello hello lokalizacja folderu hello, gdzie środowiska uruchomieniowego hello zapisywane hello kopii zapasowej (`BackupInfo.Directory`). Funkcja wywołania zwrotnego Hello można przenieść hello `BackupInfo.Directory` tooan zewnętrznym sklepie lub w innej lokalizacji.  Ta funkcja zwraca również wartość logiczną wskazującą, czy był lokalizacji docelowej tooits toosuccessfully stanie przenoszenia hello folderu kopii zapasowej.

Witaj poniższy kod przedstawia sposób hello `BackupCallbackAsync` metoda może być używana tooupload hello kopii zapasowej tooAzure magazynu:

```csharp
private async Task<bool> BackupCallbackAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
{
    var backupId = Guid.NewGuid();

    await externalBackupStore.UploadBackupFolderAsync(backupInfo.Directory, backupId, cancellationToken);

    return true;
}
```

Przykład Witaj poprzedzających `ExternalBackupStore` jest hello przykładowe klasy, która jest używana toointerface z magazynu obiektów Blob platformy Azure i `UploadBackupFolderAsync` to metoda hello kompresuje hello folderu i umieszcza je w magazynie obiektów Blob platformy Azure hello.

Należy pamiętać, że:

  - Może istnieć tylko jedna operacja tworzenia kopii zapasowej aktywny na replice w danym momencie. Więcej niż jeden `BackupAsync` zgłosi wywołanie naraz `FabricBackupInProgressException` tooone kopii zapasowych porządkowych toolimit.
  - Jeśli replika nie powiedzie się za pośrednictwem w trakcie kopii zapasowej, hello kopia zapasowa może nie zostały zakończone. W związku z tym po zakończeniu trybu failover hello jest usługi hello odpowiedzialność toorestart hello w kopii zapasowej za pomocą `BackupAsync` odpowiednio do potrzeb.

## <a name="restore-reliable-services"></a>Przywróć niezawodne usługi
Ogólnie rzecz biorąc hello przypadku tooperform operacji przywracania może być konieczne należą do jednej z tych kategorii:

  - Usługa Hello partycji utraty danych. Na przykład dysku Witaj dwie z trzech replik dla partycji (łącznie z repliki podstawowej hello) pobiera uszkodzony lub wyczyszczone. Witaj nową podstawową może być konieczne toorestore dane z kopii zapasowej.
  - Witaj całej usługi zostaną utracone. Na przykład administrator usuwa hello całej usługi, i w związku z tym usługa hello i danych hello wymagają toobe przywrócona.
  - Usługa Hello zreplikowanych danych błędy aplikacji (np. z powodu błędów aplikacji). W takim przypadku usługa hello ma toobe uaktualniony lub Przyczyna hello przywróconego tooremove hello uszkodzenia i-uszkodzenie danych ma toobe przywrócona.

Mimo że wiele metod jest możliwe, firma Microsoft oferuje kilka przykładów przy użyciu `RestoreAsync` toorecover z hello powyżej scenariuszy.

## <a name="partition-data-loss-in-reliable-services"></a>Utrata danych partycji w niezawodne usługi
W takim przypadku hello środowiska uruchomieniowego może automatycznie wykryć hello utraty danych i wywołać hello `OnDataLossAsync` interfejsu API.

Autor usługi Hello musi hello tooperform po toorecover:

  - Metoda wirtualna klasa podstawowa hello musi zostać zastąpiona `OnDataLossAsync`.
  - Znajdź hello najnowszej kopii zapasowej w lokalizacji zewnętrznych hello, która zawiera hello usługi tworzenia kopii zapasowych.
  - Pobieranie najnowszej kopii zapasowej hello (i zdekompresować hello kopii zapasowej do folderu kopii zapasowej hello, jeśli został poddany kompresji).
  - Witaj `OnDataLossAsync` metoda zapewnia `RestoreContext`. Wywołaj hello `RestoreAsync` interfejsu API na powitania podane `RestoreContext`.
  - Zwraca wartość true, jeśli przywrócenie hello został pomyślnie.

Poniżej przedstawiono przykład stosowania hello `OnDataLossAsync` metody:

```csharp
protected override async Task<bool> OnDataLossAsync(RestoreContext restoreCtx, CancellationToken cancellationToken)
{
    var backupFolder = await this.externalBackupStore.DownloadLastBackupAsync(cancellationToken);

    var restoreDescription = new RestoreDescription(backupFolder);

    await restoreCtx.RestoreAsync(restoreDescription);

    return true;
}
```

`RestoreDescription`Przekazano toohello `RestoreContext.RestoreAsync` wywołanie zawiera element członkowski o nazwie `BackupFolderPath`.
Podczas przywracania pojedynczego pełnej kopii zapasowej, to `BackupFolderPath` powinna być ustawiona ścieżka lokalna toohello hello folderu, który zawiera z pełnej kopii zapasowej.
Podczas przywracania pełnej kopii zapasowej i liczba przyrostowe kopie zapasowe, `BackupFolderPath` powinien być ustawiony toohello ścieżki lokalnej folderu hello, która zawiera nie tylko pełna kopia zapasowa hello, ale również wszystkie hello przyrostowe kopie zapasowe.
`RestoreAsync`Wywołanie może zgłosić `FabricMissingFullBackupException` Jeśli hello `BackupFolderPath` podane nie zawiera pełnej kopii zapasowej.
Można również zgłosić `ArgumentException` Jeśli `BackupFolderPath` został przerwany łańcuch przyrostowych kopii zapasowych.
Na przykład jeśli zawiera on hello pełnej kopii zapasowej, najpierw hello przyrostowych i hello trzeci przyrostowej kopii zapasowej, ale nie hello drugi przyrostowej kopii zapasowej.

> [!NOTE]
> Witaj RestorePolicy jest domyślnie tooSafe.  Oznacza to, że hello `RestoreAsync` interfejsu API zakończy się niepowodzeniem z ArgumentException rozpoznaje tego folderu kopii zapasowej hello zawiera informacje o stanie, które jest zawarte w tej replice stanu toohello starsze niż lub równe.  `RestorePolicy.Force`może być używane tooskip ta kontrola bezpieczeństwa. To jest określony jako część `RestoreDescription`.
> 

## <a name="deleted-or-lost-service"></a>Usunięte i utracone usługi
Jeśli usługa zostanie usunięty, należy najpierw ponownie utworzyć hello usługi przed przywróceniem hello danych.  Jest ważne toocreate hello usługi o tej samej konfiguracji, np. schemat, partycjonowania, który hello dane można przywrócić bezproblemowo powitalne.  Po skonfigurowaniu usługi hello hello danych toorestore interfejsu API (`OnDataLossAsync` powyżej) ma toobe wywoływane na każdej partycji tej usługi. Jednym ze sposobów osiągnięcia jest przy użyciu `[FabricClient.TestManagementClient.StartPartitionDataLossAsync](https://msdn.microsoft.com/library/mt693569.aspx)` na każdej partycji.  

Z tego punktu implementacji jest hello taki sam jak hello powyżej scenariusza. Każda partycja musi toorestore hello najnowszych odpowiednich kopii zapasowej z magazynu zewnętrznego hello. Jedno zastrzeżenie: jest tej partycji hello, którego identyfikator może teraz zmieniono, ponieważ środowisko uruchomieniowe hello dynamicznie tworzy identyfikatorów partycji. W związku z tym usługa hello musi toostore hello partycji odpowiednie informacje i usługi nazwa tooidentify hello poprawne najnowszej kopii zapasowej toorestore z dla każdej partycji.

> [!NOTE]
> Nie zaleca się toouse `FabricClient.ServiceManager.InvokeDataLossAsync` na każdej partycji toorestore hello całej usługi, ponieważ, który może doprowadzić do uszkodzenia sieci klastra.
> 

## <a name="replication-of-corrupt-application-data"></a>Replikacja danych aplikacji uszkodzony
Uaktualniania aplikacji hello nowo wdrożone zawiera usterkę, która może spowodować uszkodzenie danych. Na przykład uaktualnienie aplikacji może uruchomić tooupdate każdego rekordu numeru telefonu w niezawodnej słownik zawiera nieprawidłowy kod obszaru.  W takim przypadku hello nieprawidłowych numerach telefonów będą replikowane od sieci szkieletowej usług nie został powiadomiony o rodzaju hello hello danych, które są przechowywane.

Witaj po pierwsze toodo po wykrywania takich rażące usterkę, która spowoduje uszkodzenie danych toofreeze hello usługa na poziomie aplikacji hello i, jeśli to możliwe, uaktualnienie wersji toohello hello kodu aplikacji, który nie ma błędów hello.  Jednak nawet po hello kodu usługi został rozwiązany, hello danych nadal może być uszkodzony i dlatego może być konieczne toobe przywrócić dane.  W takim przypadku nie można wystarczające toorestore hello najnowszej kopii zapasowej, ponieważ hello najnowszej kopii zapasowych również może być uszkodzony.  W związku z tym należy toofind hello ostatniej kopii zapasowej utworzonej przed hello danych został uszkodzony.

Jeśli nie masz pewności, których kopie zapasowe są uszkodzone, można wdrożyć nowy klaster sieci szkieletowej usług i przywracać kopie zapasowe powitalnych wykorzystywanych partycji, podobnie jak hello powyżej "Usunięte lub usługa utracone" scenariusza.  Dla każdej partycji uruchomić przywracanie kopii zapasowych hello z najnowszych toohello hello najmniej. Po znalezieniu kopii zapasowej, która nie ma uszkodzenie hello Przenieś/Usuń wszystkie kopie zapasowe tej partycji, które były nowsza (od tej kopii zapasowej). Powtórz ten proces dla każdej partycji. Teraz, gdy `OnDataLossAsync` jest wywoływana na powitania partycji w klastra produkcyjnego hello, hello ostatniej kopii zapasowej znaleziono w hello zewnętrznych magazynu będzie hello jedną pobrane hello powyżej procesu.

Teraz, hello etapami Witaj, "Usunięte lub usługa utracone" sekcji może być używana toorestore stanie hello hello usługi toohello stanu, zanim kod buggy hello uszkodzony hello stanu.

Należy pamiętać, że:

  - Podczas przywracania, jest stosowany hello kopii zapasowej przywrócić jest starsza niż stan hello hello partycji przed hello dane zostały utracone. W związku z tym należy przywrócić tylko jako ostatni toorecover możliwości jak najwięcej danych jak to możliwe.
  - Witaj ciąg, który reprezentuje ścieżkę folderu kopii zapasowej hello i hello ścieżki plików w folderze kopii zapasowej hello może być większa niż 255 znaków, w zależności od ścieżki zmiennej FabricDataRoot hello i długość nazwy typu aplikacji. Może to spowodować niektóre metody .NET, takie jak `Directory.Move`, toothrow hello `PathTooLongException` wyjątku. Jednym z rozwiązań jest toodirectly wywołania interfejsów API kernel32, takich jak `CopyFile`.

## <a name="backup-and-restore-reliable-actors"></a>Kopia zapasowa i przywracanie Reliable Actors


Niezawodne Framework złośliwych użytkowników jest oparty na niezawodne usługi. Witaj ActorService obsługującego hello actor(s) jest stanowe niezawodnej usługi. W związku z tym wszystkie hello kopii zapasowej i przywracania funkcji dostępnych w usługach niezawodnej jest również dostępna tooReliable podmiotów (z wyjątkiem zachowania, które są właściwe dla dostawcy stanu). Ponieważ kopie zapasowe zostaną wykonane na podstawie na partycji, Stany wszystkich podmiotów partycji zostaną umieszczone w kopii (i przywracania jest podobny i nastąpi na podstawie na partycji). tooperform wykonywania kopii zapasowej/przywracania, hello Właściciel usługi należy utworzyć niestandardowe aktora klasy usługi, która pochodzi z klasy ActorService i następnie wykonywania kopii zapasowej/przywracania tooReliable podobnych usług zgodnie z powyższym opisem w poprzedniej sekcji.

```csharp
class MyCustomActorService : ActorService
{
     public MyCustomActorService(StatefulServiceContext context, ActorTypeInformation actorTypeInfo)
            : base(context, actorTypeInfo)
     {                  
     }
    
    //
   // Method overrides and other code.
    //
}
```

Podczas tworzenia klasy usługi aktora niestandardowe, należy to również tooregister, podczas rejestrowania hello aktora.

```csharp
ActorRuntime.RegisterActorAsync<MyActor>(
   (context, typeInfo) => new MyCustomActorService(context, typeInfo)).GetAwaiter().GetResult();
```

Witaj domyślnego stanu dostawcy dla elementów Reliable Actors jest `KvsActorStateProvider`. Przyrostowa kopia zapasowa nie jest włączona domyślnie dla `KvsActorStateProvider`. Można włączyć przyrostowej kopii zapasowej, tworząc `KvsActorStateProvider` z hello odpowiednie ustawienie w swoich konstruktorach i następnie przekazanie jej przez konstruktora tooActorService, jak pokazano w poniższym fragmencie kodu:

```csharp
class MyCustomActorService : ActorService
{
     public MyCustomActorService(StatefulServiceContext context, ActorTypeInformation actorTypeInfo)
            : base(context, actorTypeInfo, null, null, new KvsActorStateProvider(true)) // Enable incremental backup
     {                  
     }
    
    //
   // Method overrides and other code.
    //
}
```

Po włączeniu przyrostowej kopii zapasowej, biorąc przyrostowej kopii zapasowej może zakończyć się niepowodzeniem z FabricMissingFullBackupException dla jednego z następujących powodów i trzeba będzie tootake pełnej kopii zapasowej przed zmianą przyrostowe kopie zapasowe:

  - repliki Hello nigdy nie został wykonany pełnej kopii zapasowej, ponieważ stał się podstawowym.
  - Niektóre rekordy dziennika hello została obcięta, ponieważ ostatnia kopia zapasowa została wykonana.

Po włączeniu przyrostowej kopii zapasowej `KvsActorStateProvider` nie używa toomanage cyklicznego buforu dziennika rejestruje i okresowo obcina go. Jeśli żadna kopia zapasowa nie zostanie podjęta przez użytkownika w danym okresie 45 minut, hello system automatycznie obcina hello rekordów dziennika. Ten interwał można skonfigurować, określając `logTrunctationIntervalInMinutes` w `KvsActorStateProvider` — Konstruktor (toowhen podobne włączenie przyrostowej kopii zapasowej). rekordów dziennika Hello również może pobrać obcięty, jeśli replika podstawowa potrzebujesz toobuild innej repliki, wysyłając jego dane.

Podczas operacji przywracania z kopii zapasowej łańcucha, podobne usługi tooReliable, hello BackupFolderPath powinien zawierać podkatalogów z podkatalogu co zawierające pełnej kopii zapasowej oraz inne podkatalogi zawierające przyrostowe kopie zapasowe. Interfejs API przywracania Hello zgłosi FabricException z odpowiedni komunikat o błędzie w przypadku niepowodzenia weryfikacji łańcucha kopii zapasowej hello. 

> [!NOTE]
> `KvsActorStateProvider`obecnie ignoruje opcję hello RestorePolicy.Safe. Obsługa tej funkcji jest planowana w nową wersją.
> 

## <a name="testing-backup-and-restore"></a>Testowanie kopii zapasowych i przywracania
Jest ważne tooensure, kluczowych danych jest tworzona kopia zapasowa, którą można przywrócić. Można to zrobić za pomocą hello `Start-ServiceFabricPartitionDataLoss` polecenia cmdlet programu PowerShell, który można wywołać utrata danych w tootest określonej partycji, czy hello danych kopii zapasowej i przywrócenia jej funkcjonalności dla usługi działa zgodnie z oczekiwaniami.  Możliwe jest również możliwe tooprogrammatically wywoływać utraty danych i Przywróć z zdarzenia oraz.

> [!NOTE]
> Można znaleźć przykładowe zastosowanie kopii zapasowej i przywrócenia jej funkcjonalności w hello aplikacji odwołania sieci Web w witrynie GitHub. Zapoznaj się hello `Inventory.Service` usługi, aby uzyskać więcej informacji.
> 
> 

## <a name="under-hello-hood-more-details-on-backup-and-restore"></a>Pod maską hello: więcej informacji na temat tworzenia kopii zapasowych i przywracania
Oto niektóre więcej informacji dotyczących tworzenia kopii zapasowej i przywracania.

### <a name="backup"></a>Tworzenie kopii zapasowych
Witaj niezawodnej Menedżer stanu zawiera hello możliwości toocreate spójne kopie zapasowe bez blokowania dowolne operacje odczytu lub zapisu. toodo tak, jego korzysta z mechanizmu stanu trwałego punktu kontrolnego i dziennika.  Hello niezawodnej Menedżer stanu przyjmuje rozmytego (lekkie) punkty kontrolne w niektórych punktów wykorzystania toorelieve z dziennika transakcyjne hello i skrócić czas odzyskiwania.  Gdy `BackupAsync` jest nazywany hello niezawodnej Menedżer stanu powoduje, że wszystkie obiekty niezawodnej toocopy ich najnowszego punktu kontrolnego pliki tooa lokalnego folderu kopii zapasowej.  Następnie hello niezawodnej Menedżer stanu kopiuje wszystkie rekordy dziennika, zaczynając od hello "wskaźnik start" toohello najnowsze rekordu dziennika do folderu kopii zapasowej hello.  Ponieważ wszystkie rekordy dziennika hello się toohello najnowszego rekordu dziennika są uwzględnione w kopii zapasowej hello i hello niezawodnej Menedżer stanu zachowuje rejestrowania zapisu z wyprzedzeniem, hello niezawodnej Menedżer stanu gwarantuje, że wszystkie transakcje który są zatwierdzone (`CommitAsync` zwrócił pomyślnie) są uwzględniane w kopii zapasowej hello.

Każdej transakcji, które zatwierdza po `BackupAsync` została wywołana może lub nie może być hello kopii zapasowej.  Po hello lokalnego folderu kopii zapasowej zostały wprowadzone przez platformę hello (tj. lokalna kopia zapasowa zostanie zakończony przez środowisko uruchomieniowe hello), hello usługi tworzenia kopii zapasowej wywołania zwrotnego jest wywoływany.  To wywołanie zwrotne jest odpowiedzialny za przeniesienie zewnętrznej lokalizacji tooan folderu kopii zapasowej hello takie jak magazyn Azure.

### <a name="restore"></a>Przywracanie
Witaj niezawodnej Menedżer stanu zawiera hello możliwości toorestore z kopii zapasowej przy użyciu hello `RestoreAsync` interfejsu API.  
Witaj `RestoreAsync` metody na `RestoreContext` można wywołać tylko wewnątrz hello `OnDataLossAsync` metody.
Witaj bool zwrócony przez `OnDataLossAsync` wskazuje, czy usługa hello została przywrócona stanu ze źródła zewnętrznego.
Jeśli hello `OnDataLossAsync` zwraca wartość true, Service Fabric ponownie utworzy wszystkie inne replik z tego serwera podstawowego. Sieć szkieletowa usług gwarantuje, że replik, które otrzymają `OnDataLossAsync` połączeń telefonicznych z pierwszego przejścia toohello podstawową rolą, ale nie są przyznawane odczytać stanu lub zapisać stanu.
To oznacza, że implementacje klasy StatefulService `RunAsync` nie zostanie wywołany, dopóki `OnDataLossAsync` zakończy się pomyślnie.
Następnie `OnDataLossAsync` zostanie wywołana na powitania nową podstawową.
Dopóki usługi zakończeniu działania tego interfejsu API pomyślnie (przez zwrócenie wartości true lub false) i zakończeniu hello istotne zmiany konfiguracji, hello interfejsu API będzie przechowywać wywoływana pojedynczo.

`RestoreAsync`najpierw porzuca wszystkie istniejące stanu w hello replika podstawowa została wywołana w.  
Wszystkie obiekty niezawodnej hello, znajdujące się w folderze kopii zapasowej hello tworzy następnie hello niezawodnej Menedżer stanu.  
Następnie obiekty niezawodnej hello są instrukcją toorestore z ich punkty kontrolne w hello folderu kopii zapasowej.  
Na koniec hello niezawodnej Menedżer stanu odzyskuje własny stan z rekordów dziennika hello hello folderu kopii zapasowej i wykonuje odzyskiwanie.  
W ramach procesu odzyskiwania hello operacji począwszy od hello "punkt początkowy", których zatwierdzania rekordy dziennika w folderze kopii zapasowej hello są obiektami niezawodnej toohello powtórzony.  
Ten krok zapewnia, że hello odzyskane stanu jest spójna.

## <a name="next-steps"></a>Następne kroki
  - [Elementy Reliable Collections](service-fabric-work-with-reliable-collections.md)
  - [Niezawodne usługi szybki start](service-fabric-reliable-services-quick-start.md)
  - [Niezawodne usługi powiadomień](service-fabric-reliable-services-notifications.md)
  - [Niezawodne usługi konfiguracji](service-fabric-reliable-services-configuration.md)
  - [Dokumentacja dla deweloperów niezawodnej kolekcji](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

