---
title: "emulator usługi Azure storage hello aaaUse do projektowania i testowania | Dokumentacja firmy Microsoft"
description: "Hello emulatora magazynu Azure zawiera wolnego lokalne Środowisko deweloperskie do tworzenia i testowania aplikacji usługi Azure Storage. Dowiedz się, jak żądania są uwierzytelniane, jak emulator toohello tooconnect w aplikacji i jak toouse hello narzędzia wiersza polecenia."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: f480b059-df8a-4a63-b05a-7f2f5d1f5c2a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: marsma
ms.openlocfilehash: 42637dcd9f476069e6ecd19ed04e7ed93fe38ff7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-storage-emulator-for-development-and-testing"></a>Użyj hello emulatora magazynu Azure do programowania i testowania

emulator magazynu Microsoft Azure Hello zapewnia środowisko lokalne, które emuluje hello obiektów Blob platformy Azure, kolejki i usługi tabel do celów programistycznych. Przy użyciu emulatora magazynu hello, można przetestować aplikację na powitania usług magazynu lokalnie, bez tworzenia subskrypcji platformy Azure lub ponoszenia kosztów. Po zakończeniu jak aplikacja działa w emulatorze hello, możesz przełączyć toousing konto usługi Azure storage w chmurze hello.

## <a name="get-hello-storage-emulator"></a>Pobierz emulator magazynu hello
Witaj emulator magazynu jest dostępny jako część hello [Microsoft Azure SDK](https://azure.microsoft.com/downloads/). Można także zainstalować emulator magazynu hello przy użyciu hello [Autonomiczny Instalator rozszerzenia](https://go.microsoft.com/fwlink/?linkid=717179&clcid=0x409) (bezpośrednie pobieranie). emulator magazynu hello tooinstall, musi mieć uprawnienia administracyjne na komputerze.

emulator magazynu Hello obecnie działa tylko w systemie Windows. Dla osób, biorąc pod uwagę emulatora magazynu, dla systemu Linux, jedną z opcji jest społeczności hello utrzymywane emulatora magazynu typu open source [Azurite](https://github.com/arafato/azurite).

> [!NOTE]
> Dane utworzone w jednej wersji emulatora magazynu hello nie jest gwarantowana toobe dostępny przy użyciu innej wersji. Jeśli potrzebujesz toopersist danych dla długoterminowej hello, zaleca się przechowywania tych danych na koncie magazynu platformy Azure, a nie w emulatorze magazynu hello.
> <p/>
> emulator magazynu Hello zależy od określonych wersji biblioteki OData hello. Zastępowanie biblioteki DLL OData hello używanego przez emulator magazynu hello z innymi wersjami nie jest obsługiwane i może spowodować nieoczekiwane zachowanie. Jednak dowolnej wersji OData obsługiwany przez usługę magazynu hello może być używane toosend żądań toohello emulatora.
>

## <a name="how-hello-storage-emulator-works"></a>Jak działa hello emulatora magazynu
emulator magazynu Hello używa lokalnego wystąpienia programu Microsoft SQL Server i usług Azure storage tooemulate hello pliku lokalnego systemu. Domyślnie program hello emulator magazynu używa bazy danych w programie Microsoft SQL Server 2012 Express LocalDB. Można wybrać lokalne wystąpienie programu SQL Server zamiast wystąpieniem LocalDB hello tooaccess emulatora magazynu hello tooconfigure. Aby uzyskać więcej informacji, zobacz hello [Start i zainicjować hello emulatora magazynu](#start-and-initialize-the-storage-emulator) sekcji w dalszej części tego artykułu.

emulator magazynu Hello łączy tooSQL serwera lub bazy danych LocalDB przy użyciu uwierzytelniania systemu Windows.

Istnieją pewne różnice w działaniu między hello emulatora magazynu i usług Azure storage. Aby uzyskać więcej informacji na temat tych różnic, zobacz hello [różnice między hello emulatora magazynu i usługi Azure Storage](#differences-between-the-storage-emulator-and-azure-storage) sekcji w dalszej części tego artykułu.

## <a name="start-and-initialize-hello-storage-emulator"></a>Uruchom i zainicjować hello emulatora magazynu
toostart hello emulatora magazynu Azure:
1. Wybierz hello **Start** hello przycisk lub naciśnij przycisk **Windows** klucza.
1. Rozpocznij wpisywanie `Azure Storage Emulator`.
1. Wybierz emulatora hello hello liście wyświetlane aplikacji.

Po uruchomieniu emulatora magazynu hello pojawi się okno wiersza polecenia. Można użyć tej konsoli okna toostart i Zatrzymaj hello emulatora magazynu, wyczyść dane, Pobierz stan i zainicjować hello emulatora. Aby uzyskać więcej informacji, zobacz hello [odwołanie do narzędzia wiersza polecenia emulatora magazynu](#storage-emulator-command-line-tool-reference) sekcji w dalszej części tego artykułu.

Po uruchomieniu emulatora hello będzie widoczna ikona w obszarze powiadomień paska zadań systemu Windows hello.

Po zamknięciu okna wiersza polecenia emulatora magazynu hello hello emulatora magazynu będą nadal toorun. toobring okno konsoli emulatora magazynu hello wykonaj ponownie, hello w poprzednich krokach tak, jakby uruchamianie hello emulatora magazynu.

Witaj po raz pierwszy po uruchomieniu emulatora magazynu hello, hello Magazyn lokalny jest zainicjować środowiska dla Ciebie. Proces inicjowania Hello tworzy bazę danych w LocalDB i rezerwuje port HTTP dla każdej usługi Magazyn lokalny.

emulator magazynu Hello jest instalowany domyślnie zbyt`C:\Program Files (x86)\Microsoft SDKs\Azure\Storage Emulator`.

> [!TIP]
> Można użyć hello [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com) toowork z zasobami emulatora magazynu lokalnego. Wyszukaj "(Programowanie)" w części "Konta magazynu" w drzewie zasobów Eksploratora usługi Storage powitania po po zainstalowaniu i uruchomieniu emulatora magazynu hello.
>

### <a name="initialize-hello-storage-emulator-toouse-a-different-sql-database"></a>Inicjowanie toouse emulatora magazynu hello z inną bazą danych SQL
Możesz użyć hello magazynu emulatora narzędzia wiersza polecenia tooinitialize hello magazynu emulatora toopoint tooa SQL bazy danych wystąpienia innych niż hello domyślne wystąpienie bazy danych LocalDB:

1. Witaj Otwórz okno konsoli emulatora magazynu zgodnie z opisem w hello [Start i zainicjować hello emulatora magazynu](#start-and-initialize-the-storage-emulator) sekcji.
1. W oknie konsoli hello wpisz hello następujące polecenie, gdzie `<SQLServerInstance>` jest nazwą hello hello wystąpienia programu SQL Server. Określ toouse LocalDB, `(localdb)\MSSQLLocalDb` jako hello wystąpienia programu SQL Server.

  `AzureStorageEmulator.exe init /server <SQLServerInstance>`

  Można także użyć hello następujące polecenia, który kieruje hello emulatora toouse hello domyślnego wystąpienia serwera SQL:

  `AzureStorageEmulator.exe init /server .\\`

  Lub służy następujące polecenie, które ponownie inicjuje wystąpienie domyślne toohello hello bazy danych w LocalDB hello:

  `AzureStorageEmulator.exe init /forceCreate`

Aby uzyskać więcej informacji na temat tych poleceń, zobacz [odwołanie do narzędzia wiersza polecenia emulatora magazynu](#storage-emulator-command-line-tool-reference).

> [!TIP]
> Można użyć hello [Microsoft SQL Server Management Studio](/sql/ssms/download-sql-server-management-studio-ssms) wystąpienia programu SQL Server, w tym instalacji LocalDB hello toomanage (SSMS). W hello Menedżer SMSS **połączyć tooServer** okna dialogowego, określ `(localdb)\MSSQLLocalDb` w hello **nazwa serwera:** wystąpieniem LocalDB toohello tooconnect pola.

## <a name="authenticating-requests-against-hello-storage-emulator"></a>Uwierzytelniania żądań dotyczących hello emulatora magazynu
Po zainstalowaniu i uruchomić hello emulatora magazynu, można przetestować kodu na nim. Podobnie jak w przypadku usługi Azure Storage w chmurze hello każde żądanie, wprowadzone dla emulatora magazynu hello musi zostać uwierzytelniony, chyba że jest żądania od użytkowników anonimowych. Może uwierzytelnić żądania względem hello emulatora magazynu przy użyciu uwierzytelniania klucza współużytkowanego lub za pomocą sygnatury dostępu współdzielonego (SAS).

### <a name="authenticate-with-shared-key-credentials"></a>Uwierzytelnianie przy użyciu poświadczeń klucz wstępny
[!INCLUDE [storage-emulator-connection-string-include](../../includes/storage-emulator-connection-string-include.md)]

Aby uzyskać więcej informacji na parametry połączenia, zobacz [parametry połączenia Konfigurowanie usługi Azure Storage](storage-configure-connection-string.md).

### <a name="authenticate-with-a-shared-access-signature"></a>Uwierzytelniania za pomocą sygnatury dostępu współdzielonego
Niektóre biblioteki klienta magazynu Azure, takiej jak biblioteka Xamarin hello, obsługują tylko uwierzytelnianie za pomocą tokenu sygnatury dostępu Współdzielonego dostępu współdzielonego. Możesz utworzyć token sygnatury dostępu Współdzielonego hello przy użyciu narzędzia, takiego jak hello [Eksploratora usługi Storage](http://storageexplorer.com/) lub innej aplikacji, która obsługuje uwierzytelnianie klucza wspólnego.

Można również generować tokenu sygnatury dostępu Współdzielonego przy użyciu programu Azure PowerShell. Witaj poniższy przykład generuje token SAS z kontenera obiektów blob tooa pełne uprawnienia:

1. Instalowanie programu Azure PowerShell, jeśli nie jest jeszcze (przy użyciu najnowszej wersji hello hello poleceń cmdlet programu Azure PowerShell jest zalecane). Aby uzyskać instrukcje instalacji, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/install-azurerm-ps).
2. Otwórz program Azure PowerShell i uruchom hello następujące polecenia, zastępując `ACCOUNT_NAME` i `ACCOUNT_KEY==` przy użyciu własnych poświadczeń i `CONTAINER_NAME` o nazwie wybrane:

```powershell
$context = New-AzureStorageContext -StorageAccountName "ACCOUNT_NAME" -StorageAccountKey "ACCOUNT_KEY=="

New-AzureStorageContainer CONTAINER_NAME -Permission Off -Context $context

$now = Get-Date

New-AzureStorageContainerSASToken -Name CONTAINER_NAME -Permission rwdl -ExpiryTime $now.AddDays(1.0) -Context $context -FullUri
```

Hello wynikowy sygnatury dostępu współdzielonego identyfikatora URI dla nowego kontenera hello powinna być podobna do:

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2015-07-08T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3Dsss
```

sygnatury dostępu współdzielonego Hello utworzone za pomocą w tym przykładzie jest ważny przez jeden dzień. Podpis Hello daje pełny dostęp (Odczyt, zapis, Usuń, listy) tooblobs w kontenerze hello.

Aby uzyskać więcej informacji dotyczących sygnatur dostępu współdzielonego, zobacz [używanie udostępnionych sygnatur dostępu (SAS) w usłudze Azure Storage](storage-dotnet-shared-access-signature-part-1.md).

## <a name="addressing-resources-in-hello-storage-emulator"></a>Adresowania zasobów w emulatorze magazynu hello
punkty końcowe usługi powitania dla emulatora magazynu hello są inne niż konto usługi Azure storage. Witaj różnica polega na ponieważ hello komputer lokalny nie przeprowadza rozpoznawanie nazw domen, wymagających hello magazynu emulatora punkty końcowe toobe lokalnych adresów.

Podczas adresowania zasobów na koncie magazynu platformy Azure, możesz użyć hello następującego schematu. Nazwa konta Hello jest częścią nazwy hosta hello identyfikatora URI i adresowane zasobów hello jest częścią hello ścieżka identyfikatora URI:

`<http|https>://<account-name>.<service-name>.core.windows.net/<resource-path>`

Na przykład hello następujący identyfikator URI jest prawidłowy adres obiektu blob na koncie magazynu Azure:

`https://myaccount.blob.core.windows.net/mycontainer/myblob.txt`

Jednak hello emulatora magazynu, ponieważ hello komputer lokalny nie przeprowadza rozpoznawanie nazw domen, nazwa konta hello część ścieżki identyfikatora URI hello zamiast hello nazwy hosta. Użyj następującego formatu identyfikatora URI zasobu w emulatorze magazynu hello hello:

`http://<local-machine-address>:<port>/<account-name>/<resource-path>`

Na przykład hello następujący adres może służyć do uzyskiwania dostępu do obiektu blob w emulatorze magazynu hello:

`http://127.0.0.1:10000/myaccount/mycontainer/myblob.txt`

punkty końcowe usługi powitania dla emulatora magazynu hello są:

* Usługa blob:`http://127.0.0.1:10000/<account-name>/<resource-path>`
* Usługa kolejki:`http://127.0.0.1:10001/<account-name>/<resource-path>`
* Usługa tabel:`http://127.0.0.1:10002/<account-name>/<resource-path>`

### <a name="addressing-hello-account-secondary-with-ra-grs"></a>Adresy pomocniczego z RA-GRS konta hello
Począwszy od wersji 3.1 hello emulatora magazynu obsługuje dostęp do odczytu Replikacja geograficznie nadmiarowego (RA-GRS). Dla zasobów magazynowania zarówno w chmurze hello, jak i w emulatorze lokalne powitania, można uzyskać dostępu do lokalizacji dodatkowej hello przez dodanie — nazwa konta toohello dodatkowej. Na przykład można użyć dla uzyskiwania dostępu do obiektu blob przy użyciu hello pomocniczy tylko do odczytu w emulatorze magazynu hello hello następującego adresu:

`http://127.0.0.1:10000/myaccount-secondary/mycontainer/myblob.txt`

> [!NOTE]
> W przypadku toohello dostęp programistyczny dodatkowej hello emulatorze magazynu należy użyć hello biblioteki klienta usługi Storage dla platformy .NET w wersji 3.2 lub nowszej. Zobacz hello [Biblioteka klienta usługi Microsoft Azure Storage dla platformy .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx) szczegółowe informacje.
>
>

## <a name="storage-emulator-command-line-tool-reference"></a>Odwołanie do narzędzia wiersza polecenia emulatora magazynu
Począwszy od wersji 3.0 z okna konsoli jest wyświetlany po uruchomieniu hello emulatora magazynu. Użyj wiersza polecenia hello hello konsoli okna toostart i Zatrzymaj hello emulatora, jak również zapytania dotyczące stanu i wykonywać inne operacje.

> [!NOTE]
> Jeśli emulator zainstalowany rozwiązań usługi obliczenia Microsoft Azure hello, pojawi się ikona na pasku zadań systemu podczas uruchamiania hello emulatora magazynu. Kliknij prawym przyciskiem myszy tooreveal ikona hello menu, która zapewnia toostart graficzny i Zatrzymaj hello emulatora magazynu.
>
>

### <a name="command-line-syntax"></a>Składnia wiersza polecenia
`AzureStorageEmulator.exe [start] [stop] [status] [clear] [init] [help]`

### <a name="options"></a>Opcje
tooview hello listę opcji, typ `/help` hello wiersza polecenia.

| Opcja | Opis | Polecenie | Argumenty |
| --- | --- | --- | --- |
| **Rozpocznij** |Emulator magazynu hello jest uruchamiany. |`AzureStorageEmulator.exe start [-inprocess]` |*-inprocess*: Uruchom hello emulator w bieżącym procesie hello zamiast tworzenia nowego procesu. |
| **Zatrzymaj** |Zatrzymuje hello emulatora magazynu. |`AzureStorageEmulator.exe stop` | |
| **Stan** |Drukuje hello stan hello emulatora magazynu. |`AzureStorageEmulator.exe status` | |
| **Wyczyść** |Usuwa dane hello w wszystkie usługi określone w wierszu polecenia hello. |`AzureStorageEmulator.exe clear [blob] [table] [queue] [all]                                                    ` |*Obiekt blob*: Czyści obiektu blob danych. <br/>*kolejka*: usuwa dane kolejki. <br/>*Tabela*: usuwa dane w tabeli. <br/>*wszystkie*: usuwa wszystkie dane w wszystkich usług. |
| **Init** |Przeprowadza jednorazowe inicjowanie tooset się hello emulatora. |<code>AzureStorageEmulator.exe init [-server serverName] [-sqlinstance instanceName] [-forcecreate&#124;-skipcreate] [-reserveports&#124;-unreserveports] [-inprocess]</code> |*-Serwer serverName\instanceName*: Określa powitania serwera obsługującego wystąpienie programu SQL hello. <br/>*-sqlinstance instanceName*: Określa nazwę hello toobe wystąpienia SQL hello używane w hello domyślnego wystąpienia serwera. <br/>*-forcecreate*: wymusza utworzenia hello bazy danych SQL, nawet jeśli już istnieje. <br/>*-skipcreate*: pomija tworzenie hello bazy danych SQL. To ma pierwszeństwo przed - forcecreate.<br/>*-reserveports*: prób porty hello HTTP tooreserve skojarzonych z usługami hello.<br/>*-unreserveports*: prób zastrzeżenia tooremove dla portów hello HTTP związanych z usługami hello. To ma pierwszeństwo przed - reserveports.<br/>*-inprocess*: wykonuje inicjowania w bieżącym procesie hello zamiast dochodzi do uruchamiania nowego procesu. Witaj bieżący proces musi zostać uruchomiona z podwyższonym poziomem uprawnień w przypadku zmiany rezerwacji portu. |

## <a name="differences-between-hello-storage-emulator-and-azure-storage"></a>Różnice między hello emulatora magazynu i usługi Azure Storage
Ponieważ hello emulatora magazynu jest emulowane środowisko uruchomiony w lokalnym wystąpieniu serwera SQL, istnieją różnice w działaniu hello emulatora i konto magazynu platformy Azure w chmurze hello:

* emulator magazynu Hello obsługuje tylko jedno konto stałych i klucz uwierzytelniania dobrze znane.
* emulator magazynu Hello nie jest usługą skalowalności magazynu i nie obsługuje dużej liczby równoczesnych klientów.
* Zgodnie z opisem w [adresowania zasobów w emulatorze magazynu hello](#addressing-resources-in-the-storage-emulator), zasobów objętych inaczej hello emulatora magazynu i konto magazynu platformy Azure. Ta różnica wynika rozpoznania nazwy domeny jest dostępny w chmurze hello, ale nie na komputerze lokalnym hello.
* Począwszy od wersji 3.1, konto emulatora magazynu hello obsługuje dostęp do odczytu Replikacja geograficznie nadmiarowego (RA-GRS). W emulatorze hello wszystkich kont jest włączone RA-GRS, i nigdy nie jest wszelkie opóźnienia między hello podstawowych i pomocniczych replik. operacje uzyskać statystyki usługi obiektów Blob, Pobierz Statystyka usługi kolejki i uzyskać statystyki usługi tabeli Hello są obsługiwane na koncie hello dodatkowej i zawsze zwróci wartość hello hello `LastSyncTime` element odpowiedzi jako hello bieżącej godziny zgodnie z toohello podstawowy Baza danych SQL.
* Witaj usługi plików i punktów końcowych usługi protokołu SMB nie są obsługiwane w emulatorze magazynu hello.
* Jeśli używasz wersji usług magazynu hello nie jest jeszcze obsługiwany przez hello emulator emulatora magazynu hello zwrócą błąd VersionNotSupportedByEmulator (kod stanu HTTP 400 - Niewłaściwe żądanie).

### <a name="differences-for-blob-storage"></a>Różnice dla magazynu obiektów Blob
Witaj następujące różnice zastosować tooBlob magazynu w emulatorze hello:

* emulator magazynu Hello obsługuje tylko rozmiary obiektów blob w górę too2 GB.
* Przyrostowa kopia umożliwia migawek z toobe zastąpione obiekty BLOB kopiowane, która zwraca błąd hello usługi.
* Diff zakresów stron Get nie działa między migawki skopiowane za pomocą przyrostowej kopii obiektu Blob.
* Operacji Put obiektu Blob może się powieść względem obiektu blob, czy istnieje w emulatorze magazynu hello aktywne dzierżawy, nawet jeśli nie określono Identyfikatora dzierżawy hello w żądaniu hello.
* Dołącz operacje nie są obsługiwane przez hello emulator obiektu Blob. Próba operacji na uzupełnialny obiekt blob zwrócą błąd FeatureNotSupportedByEmulator (kod stanu HTTP 400 - Niewłaściwe żądanie).

### <a name="differences-for-table-storage"></a>Różnice dla magazynu tabel
Witaj następujące różnice zastosować tooTable magazynu w emulatorze hello:

* Właściwości daty w hello usługi tabel w emulatorze magazynu hello obsługuje tylko zakres hello obsługiwane przez program SQL Server 2005 (są one wymagane toobe później niż 1 stycznia 1753). Wszystkie daty przed 1 stycznia 1753 są zmieniane toothis wartość. Witaj precyzji daty jest ograniczone toohello dokładności programu SQL Server 2005, co oznacza, że daty są dokładne too1/300th sekundy.
* emulator magazynu Hello obsługuje partycji klucza i wiersza wartości właściwości klucza mniej niż 512 bajtów każdego. Ponadto hello całkowity rozmiar hello nazwa konta oraz nazwę tabeli i nazw właściwości kluczy razem nie może przekraczać 900 bajtów.
* Całkowity rozmiar wiersza w tabeli w emulatorze magazynu hello Hello jest ograniczona tooless niż 1 MB.
* W emulatorze magazynu hello, typ właściwości danych `Edm.Guid` lub `Edm.Binary` obsługi tylko hello `Equal (eq)` i `NotEqual (ne)` operatory porównania w zapytaniu filtru ciągów.

### <a name="differences-for-queue-storage"></a>Różnice dla magazynu kolejek
W emulatorze hello nie ma żadnych różnic tooQueue określonego magazynu.

## <a name="storage-emulator-release-notes"></a>Informacje o wersji emulatora magazynu
### <a name="version-52"></a>W wersji 5.2
* emulator magazynu Hello obsługuje teraz wersji 2017-04-17 usług magazynu hello na punktów końcowych usługi obiektów Blob, kolejki i tabeli.
* Stałe usterki, których wartości właściwości tabeli zostały nie jest poprawnie zaszyfrowana.

### <a name="version-51"></a>W wersji 5.1
* Stałej usterki, gdy emulator magazynu hello został zwracanie hello `DataServiceVersion` nagłówka w niektórych odpowiedzi, gdy usługa hello nie.

### <a name="version-50"></a>W wersji 5.0
* Instalator emulatora magazynu Hello sprawdza już istniejących MSSQL i instaluje .NET Framework.
* Instalator emulatora magazynu Hello już utworzona baza danych hello jako część instalacji. Nadal będzie można utworzyć bazy danych, w razie potrzeby jako część uruchomienia.
* Tworzenie bazy danych nie wymaga podniesienia uprawnień.
* Port rezerwacji nie są już potrzebne do uruchomienia.
* Dodaje następujące opcje zbyt hello`init`: `-reserveports` (wymaga podniesienia uprawnień), `-unreserveports` (wymaga podniesienia uprawnień), `-skipcreate`.
* Interfejs użytkownika emulatora magazynu opcji ikonę na pasku zadań systemu hello Hello uruchamia interfejsu wiersza polecenia hello. Witaj starego graficznego interfejsu użytkownika nie jest już dostępny.
* Niektórych bibliotek DLL zostały usunięte lub zmieniono jego nazwę.

### <a name="version-46"></a>W wersji 4.6
* emulator magazynu Hello obsługuje teraz wersji 2016-05-31 usług magazynu hello na punktów końcowych usługi obiektów Blob, kolejki i tabeli.

### <a name="version-45"></a>W wersji 4.5
* Stałe usterkę, która spowodowane inicjowania i instalacji toofail emulatora magazynu hello hello kopii bazy danych została zmieniona.

### <a name="version-44"></a>Wersja 4.4
* emulator magazynu Hello obsługuje teraz wersji 2015-12-11 usług magazynu hello na punktów końcowych usługi obiektów Blob, kolejki i tabeli.
* Witaj emulatora magazynu wyrzucanie elementów bezużytecznych danych obiektu blob jest teraz efektywniejsze podczas pracy z dużą liczbą obiektów blob.
* Stałe usterkę, która spowodowała kontenera toobe XML listy ACL nieco inaczej walidowana z jak Usługa magazynu hello jest.
* Stałe błąd powodujący czasami maksymalna i toobe wartości daty/godziny min zgłoszone w strefie czasowej niepoprawne hello.

### <a name="version-43"></a>Wersji 4.3
* emulator magazynu Hello obsługuje teraz wersji 2015-07-08 usług magazynu hello na punktów końcowych usługi obiektów Blob, kolejki i tabeli.

### <a name="version-42"></a>W wersji 4.2
* emulator magazynu Hello obsługuje teraz wersji 2015-04-05 usług magazynu hello na punktów końcowych usługi obiektów Blob, kolejki i tabeli.

### <a name="version-41"></a>Wersji 4.1
* emulator magazynu Hello obsługuje teraz wersji 2015-02-21 usług magazynu hello na obiektów Blob, kolejki i tabeli punktów końcowych usług, z wyjątkiem hello nowych funkcji Dołącz obiektu Blob.
* Jeśli używasz wersji usług magazynu hello nie jest jeszcze obsługiwany przez hello emulator emulatora hello zwraca komunikat o błędzie łatwy do rozpoznania. Zalecamy używanie najnowszej wersji emulatora hello hello. Jeśli wystąpi błąd VersionNotSupportedByEmulator (kod stanu HTTP 400 - Niewłaściwe żądanie), Pobierz najnowszą wersję hello hello emulatora magazynu.
* Stałe usterki którym wyścigu spowodowaną tabeli jednostki danych toobe niepoprawne podczas operacji scalania współbieżnych.

### <a name="version-40"></a>W wersji 4.0
* emulator magazynu Hello pliku wykonywalnego zmieniono zbyt*AzureStorageEmulator.exe*.

### <a name="version-32"></a>W wersji 3.2
* emulator magazynu Hello obsługuje teraz wersji 2014-02-14 usług magazynu hello na punktów końcowych usługi obiektów Blob, kolejki i tabeli. Punkty końcowe usługi plików nie są obecnie obsługiwane w emulatorze magazynu hello. Zobacz [przechowywania wersji dla hello usług magazynu Azure](/rest/api/storageservices/Versioning-for-the-Azure-Storage-Services) szczegółowe informacje o wersji 2014-02-14.

### <a name="version-31"></a>W wersji 3.1
* Dostęp do odczytu magazynu geograficznie nadmiarowego (RA-GRS) jest teraz obsługiwane w emulatorze magazynu hello. Statystyka usługi Blob uzyskać Hello, uzyskać statystyki usługi kolejki i pobrać tabeli Statystyka interfejsów API usługi Service są obsługiwane w przypadku konta hello dodatkowej i zawsze zwróci wartość hello hello LastSyncTime odpowiedzi elementu jako hello bieżącego toohello zgodnie z czasu bazowy SQL Baza danych. W przypadku toohello dostęp programistyczny dodatkowej hello emulatorze magazynu należy użyć hello biblioteki klienta usługi Storage dla platformy .NET w wersji 3.2 lub nowszej. Aby uzyskać więcej informacji, zobacz hello biblioteki klienta usługi Microsoft Azure Storage dla odwołania .NET.

### <a name="version-30"></a>W wersji 3.0
* Hello emulatora magazynu Azure nie jest dostarczany w hello same pakiety hello emulatora obliczeń.
* skryptowy interfejs wiersza polecenia jest zastąpiona Hello magazynu emulatora graficznego interfejsu użytkownika. Aby uzyskać szczegółowe informacje na powitania interfejsu wiersza polecenia Zobacz dotyczące narzędzia wiersza polecenia emulatora magazynu. interfejs graficzny Hello będzie kontynuowana toobe w wersji 3.0 lub nowszej, ale jest tylko dostępny po zainstalowaniu hello obliczeniowe emulatora przez kliknięcie prawym przyciskiem myszy ikonę na pasku zadań systemu hello i wybierając polecenie Pokaż magazynu interfejs użytkownika emulatora.
* W wersji 2013-08-15 usług magazynu Azure hello teraz jest w pełni obsługiwany. (Wcześniej tej wersji jest obsługiwana tylko przez Emulator magazynu wersji 2.2.1 wersji zapoznawczej.)

## <a name="next-steps"></a>Następne kroki

* Ocena emulatora magazynu i platform, obsługiwane społeczności typu open source hello [Azurite](https://github.com/arafato/azurite). 
* [Przykładów dla magazynu platformy Azure przy użyciu platformy .NET](storage-samples-dotnet.md) zawiera przykłady kodu tooseveral łącza można używać podczas tworzenia aplikacji.
* Można użyć hello [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com) toowork z zasobami w chmurze konta magazynu, a w emulatorze magazynu hello.
