---
title: "aaaDevelop lokalnie z hello Azure rozwiązania Cosmos DB emulatora | Dokumentacja firmy Microsoft"
description: "Przy użyciu hello Azure rozwiązania Cosmos DB emulatora, mogą tworzyć i testować aplikację lokalnie darmo, bez tworzenia subskrypcji platformy Azure."
services: cosmos-db
documentationcenter: 
keywords: "Emulator usługi Azure rozwiązania Cosmos bazy danych"
author: arramac
manager: jhubbard
editor: 
ms.assetid: 90b379a6-426b-4915-9635-822f1a138656
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: arramac
ms.openlocfilehash: fb5449489e5f71664e72d8e11e583315be371bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cosmos-db-emulator-for-local-development-and-testing"></a>Użyj dla lokalnego projektowania i testowania hello Azure rozwiązania Cosmos DB emulatora

<table>
<tr>
  <td><strong>Pliki binarne</strong></td>
  <td>[Pobieranie pliku MSI](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><strong>Docker</strong></td>
  <td>[Centrum docker](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><strong>Źródło docker</strong></td>
  <td>[Github](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
Hello Azure rozwiązania Cosmos DB emulatora zapewnia środowisko lokalne, które emuluje hello Azure DB rozwiązania Cosmos usługi do celów programistycznych. Przy użyciu hello Azure rozwiązania Cosmos DB emulatora, mogą tworzyć i przetestować aplikację lokalnie, bez tworzenia subskrypcji platformy Azure lub ponoszenia kosztów. Po zakończeniu jak aplikacja działa na platformie hello Azure rozwiązania Cosmos DB emulatora, możesz przełączyć toousing konto bazy danych Azure rozwiązania Cosmos w chmurze hello.

W tym artykule omówiono hello następujące zadania: 

> [!div class="checklist"]
> * Instalowanie hello emulatora
> * Uruchomiony hello Emulator na Docker dla systemu Windows
> * Uwierzytelniania żądania
> * Przy użyciu hello Eksploratora danych w hello emulatora
> * Eksportowanie certyfikatów SSL
> * Wywoływanie z wiersza polecenia hello hello emulatora
> * Zbieranie plików śledzenia

Zalecamy rozpoczęcie pracy od obejrzenia powitania po wideo, w którym Kirill Gavrylyuk pokazuje, jak tooget pracę z hello Azure rozwiązania Cosmos DB emulatora. Uwaga wideo hello stosowany jest wspólny termin emulatora toohello hello emulatora usługi DocumentDB, że zmieniono nazwę samego narzędzia hello hello Azure rozwiązania Cosmos DB emulatora od Tynkowanie hello wideo. Wszystkie informacje w hello wideo są nadal aktualne dla hello Azure rozwiązania Cosmos DB emulatora. 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-hello-emulator-works"></a>Jak działa hello emulatora
Hello emulatora DB rozwiązania Cosmos Azure udostępnia emulację o wysokiej wierności hello usługi bazy danych Azure rozwiązania Cosmos. Obsługuje ona identyczną funkcjonalność jako rozwiązania Cosmos bazy danych Azure, w tym obsługa tworzenia i badania dokumentów JSON, inicjowania obsługi administracyjnej i skalowanie kolekcje i wykonywania procedury składowane i wyzwalaczy. Mogą tworzyć i testowanie aplikacji za pomocą hello Azure rozwiązania Cosmos DB emulatora i wdrażać je tooAzure w skali globalnej poprzez tylko pojedynczą konfiguracją zmienić toohello punktu końcowego połączenia dla bazy danych Azure rozwiązania Cosmos.

Gdy utworzyliśmy emulacji lokalnej o wysokiej wierności, rzeczywista usługi bazy danych Azure rozwiązania Cosmos hello hello implementacja hello Azure rozwiązania Cosmos DB emulatora różni się od hello usługi. Na przykład hello Azure rozwiązania Cosmos DB emulatora używa standardowych składniki systemu operacyjnego, takie jak hello lokalnego systemu plików dla stanu trwałego i stosu protokołu HTTPS dla łączności. Oznacza to, że niektóre funkcje, która zależy od infrastruktury platformy Azure, takich jak globalnej replikacji, jednocyfrowej milisekundy opóźnienia odczytuje i zapisuje i dostosowywalne poziomy spójności nie są dostępne za pośrednictwem hello Azure rozwiązania Cosmos DB emulatora.

> [!NOTE]
> W tym hello czasu Eksploratora danych w hello emulatora obsługuje tylko tworzenie hello kolekcji interfejsu API usługi DocumentDB i kolekcji bazy danych MongoDB. Witaj Eksploratora danych w emulatorze hello nie obsługuje obecnie hello Tworzenie tabel i wykresów. 

## <a name="system-requirements"></a>Wymagania systemowe
Hello Azure rozwiązania Cosmos DB Emulator ma następujące wymagania sprzętowe i programowe hello:

* Wymagania dotyczące oprogramowania
  * Windows Server 2012 R2, Windows Server 2016 lub Windows 10
*   Minimalne wymagania sprzętowe
  * 2 GB PAMIĘCI RAM
  * 10 GB dostępnego miejsca na dysku

## <a name="installation"></a>Instalacja
Można pobrać i zainstalować hello Azure rozwiązania Cosmos DB emulatora z hello [Microsoft Download Center](https://aka.ms/cosmosdb-emulator). 

> [!NOTE]
> tooinstall, konfigurowania i uruchamiania hello Azure rozwiązania Cosmos DB emulatora, musisz mieć uprawnienia administracyjne na komputerze hello.

## <a name="running-on-docker-for-windows"></a>Systemem Docker dla systemu Windows

Witaj emulatora DB rozwiązania Cosmos Azure może działać w Docker dla systemu Windows. Witaj emulatora nie działają w Docker dla Oracle Linux.

Po utworzeniu [Docker dla systemu Windows](https://www.docker.com/docker-windows) zainstalowana, można umieścić obraz emulatora hello z Centrum Docker, uruchamiając następujące polecenie z ulubionych powłoki hello (cmd.exe, programu PowerShell, itp.).

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
Obraz powitania toostart, uruchom następujące polecenia hello.

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

odpowiedź Hello wygląda podobnie toohello następujące:

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import hello SSL certificate from an administrator command prompt on hello host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

Zamykanie powłoki interakcyjne hello po hello, który został uruchomiony Emulator będzie emulatora hello zamknięcie kontenera.

Przy użyciu hello punktu końcowego i klucz główny w z hello odpowiedzi na kliencie, a następnie zaimportowanie certyfikatu SSL hello do hosta. Witaj tooimport certyfikat SSL hello poniższych z wiersza polecenia z uprawnieniami administratora:

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-hello-emulator"></a>Uruchom hello emulatora

toostart hello Azure rozwiązania Cosmos DB emulatora, kliknij przycisk Start hello lub naciśnij klawisz systemu Windows hello. Rozpocznij wpisywanie **Azure rozwiązania Cosmos DB emulatora**i emulatora hello wybierz z listy aplikacji hello. 

![Wybierz hello Start przycisk lub naciśnij przycisk hello klawisz systemu Windows, rozpocznij wpisywanie ** Azure rozwiązania Cosmos DB emulatora ** i emulatora hello wybierz z listy aplikacji hello](./media/local-emulator/database-local-emulator-start.png)

Po uruchomieniu emulatora hello będzie widoczna ikona w obszarze powiadomień paska zadań systemu Windows hello. ![Azure DB rozwiązania Cosmos emulatora lokalnym obszarze powiadomień paska zadań](./media/local-emulator/database-local-emulator-taskbar.png)

Hello Azure rozwiązania Cosmos DB emulatora domyślnie działa na komputerze lokalnym hello ("localhost") nasłuchuje na porcie 8081.

Hello Azure rozwiązania Cosmos DB emulatora jest instalowany przez domyślny toohello `C:\Program Files\Azure Cosmos DB Emulator` katalogu. Można również uruchomić i zatrzymać emulatora hello z hello wiersza polecenia. Zobacz [odwołanie do narzędzia wiersza polecenia](#command-line) Aby uzyskać więcej informacji.

## <a name="start-data-explorer"></a>Uruchom Eksploratora danych

Po uruchomieniu emulatora bazy danych Azure rozwiązania Cosmos hello w przeglądarce zostanie otwarty automatycznie hello Eksploratora danych DB rozwiązania Cosmos Azure. Witaj adres będzie wyświetlany jako [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html). Jeśli są Zamknij Eksploratora hello i chcesz toore otwórz go później, możesz otworzyć hello adresu URL w przeglądarce lub uruchomić go z hello Azure rozwiązania Cosmos DB emulatora w hello ikona na pasku zadań systemu Windows, jak pokazano poniżej.

![Azure uruchamiania Eksploratora danych lokalnych emulatora DB rozwiązania Cosmos](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a>Sprawdzanie dostępności aktualizacji
Eksplorator danych wskazuje, czy jest nowe aktualizacje dostępne do pobrania. 

> [!NOTE]
> Dane utworzone w jednej wersji hello Azure rozwiązania Cosmos DB emulatora nie jest gwarantowana toobe dostępny przy użyciu innej wersji. Jeśli potrzebujesz toopersist danych dla długoterminowej hello, zaleca się przechowywania tych danych w ramach konta bazy danych Azure rozwiązania Cosmos, a nie w hello Azure rozwiązania Cosmos DB emulatora. 

## <a name="authenticating-requests"></a>Uwierzytelniania żądania
Podobnie jak Azure DB rozwiązania Cosmos w chmurze hello każde żądanie, wprowadzone przed hello Azure rozwiązania Cosmos DB emulatora musi zostać uwierzytelniony. Hello Azure rozwiązania Cosmos DB emulatora obsługuje jednego stałego konta i klucz uwierzytelniania dobrze znanego uwierzytelniania klucza głównego. Tego konta i klucz są hello poświadczenia tylko do użytku z hello Azure rozwiązania Cosmos DB emulatora. Są to:

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> obsługiwane przez hello Azure rozwiązania Cosmos DB emulatora klucza głównego Hello jest przeznaczony do użytku z emulatora hello. Nie można używać swojego konta bazy danych Azure rozwiązania Cosmos produkcyjnych i klucz hello Azure rozwiązania Cosmos DB emulatora. 

> [!NOTE] 
> Jeśli hello emulator została uruchomiona z hello opcja następujący/key, użyj hello wygenerowany klucz zamiast "obiektów relacyjnych C2y6yDjf5 + ob0N8A7Cgv30VRDJIWEHLM 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw =="

Ponadto, podobnie jak hello Azure DB rozwiązania Cosmos usługi, hello Azure rozwiązania Cosmos DB emulatora obsługuje tylko bezpiecznej komunikacji za pośrednictwem protokołu SSL.

## <a name="running-hello-emulator-on-a-local-network"></a>Uruchomiony hello emulator w sieci lokalnej

Można uruchomić emulatora hello w sieci lokalnej. tooenable dostępu do sieci, należy określić opcję /AllowNetworkAccess hello na powitania [wiersza polecenia](#command-line-syntax), które również wymaga określenia następujący/key = key_string lub/KeyFile = nazwa_pliku. Można użyć /GenKeyFile = toogenerate nazwa_pliku pliku z wyprzedzeniem losowy klucz.  Następnie można przekazać tego zbyt/KeyFile = nazwa_pliku lub następujący/key = contents_of_file.

tooenable dostępu do sieci dla hello pierwszego czasu hello użytkownika powinien zamknięcia hello emulatora i Usuń katalog danych hello emulatora (C:\Users\user_name\AppData\Local\CosmosDBEmulator).

## <a name="developing-with-hello-emulator"></a>Programowania z użyciem hello emulatora
Po ma hello Azure Emulator rozwiązania Cosmos DB uruchomiony na pulpicie, można użyć dowolnego obsługiwane [zestawu SDK usługi Azure rozwiązania Cosmos DB](documentdb-sdk-dotnet.md) lub hello [interfejsu API REST Azure rozwiązania Cosmos DB](/rest/api/documentdb/) toointeract z hello emulatora. Hello Azure rozwiązania Cosmos DB emulatora obejmuje również wbudowane Eksploratora danych, który umożliwia tworzenie kolekcji hello usługi DocumentDB, bazy danych MongoDB interfejsów API i widoku i edycji dokumentów bez pisania żadnego kodu.   

    // Connect toohello Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

Jeśli używasz [obsługą protokołu bazy danych Azure rozwiązania Cosmos bazy danych mongodb](mongodb-introduction.md), użyj hello następujące parametry połączenia:

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

Można użyć istniejących narzędzi, takich jak [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) toohello tooconnect emulatora DB rozwiązania Cosmos Azure. Można również migrację danych między hello Azure rozwiązania Cosmos DB emulatora i usługę Azure DB rozwiązania Cosmos hello za pomocą hello [narzędzia migracji danych DB rozwiązania Cosmos Azure](https://github.com/azure/azure-documentdb-datamigrationtool).

> [!NOTE] 
> Jeśli hello emulator została uruchomiona z hello opcja następujący/key, użyj hello wygenerowany klucz zamiast "obiektów relacyjnych C2y6yDjf5 + ob0N8A7Cgv30VRDJIWEHLM 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw =="

Przy użyciu emulatora usługi Azure DB rozwiązania Cosmos hello, domyślnie, można utworzyć kolekcje z jedną partycją too25 lub 1 kolekcji podzielone na partycje. Aby uzyskać więcej informacji na temat Zmiana tej wartości, zobacz [ustawienie wartości PartitionCount hello](#set-partitioncount).

## <a name="export-hello-ssl-certificate"></a>Wyeksportuj certyfikat SSL hello

Języków .NET i toosecurely magazynu certyfikatów systemu Windows hello Użyj środowiska wykonawczego łączą emulatora lokalnej bazy danych Azure rozwiązania Cosmos toohello. Inne języki ma swoje własne metody przy użyciu certyfikatów oraz zarządzania nimi. Java używa własnego [magazyn certyfikatów](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) natomiast używa języka Python [gniazda otoki](https://docs.python.org/2/library/ssl.html).

W kolejności tooobtain toouse certyfikatu, języki i środowisk uruchomieniowych, który nie zintegrować z magazynu certyfikatów systemu Windows hello można będzie potrzebny tooexport przy użyciu Menedżera certyfikatów systemu Windows hello. Można go uruchomić, uruchamiając certlm.msc lub wykonaj te instrukcje krok po kroku hello [wyeksportowanie hello Azure rozwiązania Cosmos DB emulatora certyfikatów](./local-emulator-export-ssl-certificates.md). Po uruchomieniu Menedżera certyfikatów hello certyfikaty osobiste Otwórz hello w sposób przedstawiony poniżej i eksportowanie hello certyfikat o przyjaznej nazwie hello "DocumentDBEmulatorCertificate", zgodnie z algorytmem BASE-64 pliku X.509 (.cer).

![Azure certyfikat SSL lokalnym emulatorze DB rozwiązania Cosmos](./media/local-emulator/database-local-emulator-ssl_certificate.png)

Certyfikat X.509 Hello można zaimportować do magazynu certyfikatów Java hello wykonując instrukcje hello w [Dodawanie toohello certyfikatów, w magazynie certyfikatów urzędu certyfikacji Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store). Po hello certyfikat został zaimportowany do magazynu certyfikatów hello, aplikacji Java i bazy danych MongoDB będą mogli tooconnect toohello emulatora DB rozwiązania Cosmos Azure.

Podczas łączenia z emulatora toohello Python i Node.js SDK, weryfikacji SSL jest wyłączona.

## <a id="command-line"></a>Odwołanie do narzędzia wiersza polecenia
Z lokalizacji instalacji hello można użyć wiersza polecenia toostart hello i Zatrzymaj emulatora hello, skonfiguruj opcje, a także wykonywanie innych operacji.

### <a name="command-line-syntax"></a>Składnia wiersza polecenia

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

tooview hello listę opcji, typ `CosmosDB.Emulator.exe /?` hello wiersza polecenia.

<table>
<tr>
  <td><strong>Opcja</strong></td>
  <td><strong>Opis</strong></td>
  <td><strong>Polecenie</strong></td>
  <td><strong>Argumenty</strong></td>
</tr>
<tr>
  <td>[Brak argumentów]</td>
  <td>Uruchamiany hello Azure rozwiązania Cosmos DB emulatora z ustawieniami domyślnymi.</td>
  <td>CosmosDB.Emulator.exe</td>
  <td></td>
</tr>
<tr>
  <td>[Pomoc]</td>
  <td>Wyświetla hello listę obsługiwanych argumentów wiersza polecenia.</td>
  <td>CosmosDB.Emulator.exe /?</td>
  <td></td>
</tr>
<tr>
  <td>Zamknięcie</td>
  <td>Zamyka hello Azure rozwiązania Cosmos DB emulatora.</td>
  <td>/ Shutdown CosmosDB.Emulator.exe</td>
  <td></td>
</tr>
<tr>
  <td>Ścieżki danych</td>
  <td>Określa ścieżkę hello w toostore plików danych. Domyślnie jest to % LocalAppdata%\CosmosDBEmulator.</td>
  <td>CosmosDB.Emulator.exe /DataPath =&lt;ścieżki danych&gt;</td>
  <td>&lt;ścieżki danych&gt;: dostępną ścieżkę</td>
</tr>
<tr>
  <td>Port</td>
  <td>Określa toouse numer portu hello hello emulatora.  Domyślnie jest 8081.</td>
  <td>/ CosmosDB.Emulator.exe port =&lt;portu&gt;</td>
  <td>&lt;port&gt;: numer pojedynczego portu</td>
</tr>
<tr>
  <td>MongoPort</td>
  <td>Określa hello toouse numer portu bazy danych MongoDB zgodności interfejsu API. Domyślnie jest 10255.</td>
  <td>CosmosDB.Emulator.exe /MongoPort =&lt;mongoport&gt;</td>
  <td>&lt;mongoport&gt;: numer pojedynczego portu</td>
</tr>
<tr>
  <td>DirectPorts</td>
  <td>Określa toouse porty hello bezpośrednie połączenie z. Wartości domyślne są 10251,10252,10253,10254.</td>
  <td>CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</td>
  <td>&lt;directports&gt;: rozdzielana przecinkami lista portów 4</td>
</tr>
<tr>
  <td>Klucz</td>
  <td>Klucz autoryzacji hello emulatora. Klucz musi być hello kodowanie base-64 wektora 64 bajtów.</td>
  <td>CosmosDB.Emulator.exe następujący/key:&lt;klucza&gt;</td>
  <td>&lt;klucz&gt;: klucz musi być hello wektora 64-bajtowych kodowanie base-64</td>
</tr>
<tr>
  <td>EnableRateLimiting</td>
  <td>Określa, że ta stawka żądania ograniczanie zachowanie jest włączona.</td>
  <td>CosmosDB.Emulator.exe /EnableRateLimiting</td>
  <td></td>
</tr>
<tr>
  <td>DisableRateLimiting</td>
  <td>Określa, że tej liczby żądań ograniczanie zachowania jest wyłączone.</td>
  <td>CosmosDB.Emulator.exe /DisableRateLimiting</td>
  <td></td>
</tr>
<tr>
  <td>NoUI</td>
  <td>Nie pokazuj emulatora hello interfejsu użytkownika.</td>
  <td>/ Noui CosmosDB.Emulator.exe</td>
  <td></td>
</tr>
<tr>
  <td>NoExplorer</td>
  <td>Nie pokazuj Eksploratora dokumentów przy uruchamianiu.</td>
  <td>CosmosDB.Emulator.exe /NoExplorer</td>
  <td></td>
</tr>
<tr>
  <td>Liczba partycji</td>
  <td>Określa maksymalną liczbę kolekcji partycjonowanych hello. Zobacz [zmiany hello liczby kolekcji](#set-partitioncount) Aby uzyskać więcej informacji.</td>
  <td>CosmosDB.Emulator.exe /PartitionCount =&lt;liczba partycji&gt;</td>
  <td>&lt;Liczba partycji&gt;: Maksymalna liczba dozwolonych kolekcje z jedną partycją. Domyślna to 25. Maksymalna dozwolona wartość to 250.</td>
</tr>
<tr>
  <td>DefaultPartitionCount</td>
  <td>Określa hello domyślny numer partycji dla kolekcji partycjonowanych.</td>
  <td>CosmosDB.Emulator.exe /DefaultPartitionCount =&lt;defaultpartitioncount&gt;</td>
  <td>&lt;defaultpartitioncount&gt; domyślna to 25.</td>
</tr>
<tr>
  <td>AllowNetworkAccess</td>
  <td>Umożliwia dostęp do emulatora toohello za pośrednictwem sieci. Należy także podać następujący/key =&lt;key_string&gt; lub/KeyFile =&lt;nazwa_pliku&gt; tooenable dostępu do sieci.</td>
  <td>CosmosDB.Emulator.exe AllowNetworkAccess następujący/key =&lt;key_string&gt;<br><br>lub<br><br>/ KeyFile /AllowNetworkAccess CosmosDB.Emulator.exe =&lt;nazwa_pliku&gt;</td>
  <td></td>
</tr>
<tr>
  <td>NoFirewall</td>
  <td>Nie należy dostosować reguły zapory, gdy /AllowNetworkAccess jest używany.</td>
  <td>/ Nofirewall CosmosDB.Emulator.exe</td>
  <td></td>
</tr>
<tr>
  <td>GenKeyFile</td>
  <td>Wygeneruj nowy klucz autoryzacji i Zapisz toohello określonego pliku. można użyć klucza Hello wygenerowane z opcji/KeyFile lub hello następujący/key.</td>
  <td>CosmosDB.Emulator.exe /GenKeyFile =&lt;ścieżki pliku tookey&gt;</td>
  <td></td>
</tr>
<tr>
  <td>Spójność</td>
  <td>Ustaw poziom spójności domyślne hello hello konta.</td>
  <td>CosmosDB.Emulator.exe /Consistency =&lt;spójności&gt;</td>
  <td>&lt;spójność&gt;: wartość musi być jedną z następujących hello [poziomy spójności](consistency-levels.md): sesja, silne, Eventual lub BoundedStaleness.  Wartość domyślna Hello jest sesja.</td>
</tr>
<tr>
  <td>?</td>
  <td>Pokaż komunikat pomocy hello.</td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-hello-azure-cosmos-db-emulator-and-azure-cosmos-db"></a>Różnice między hello Azure rozwiązania Cosmos DB emulatora i bazy danych Azure rozwiązania Cosmos 
Ponieważ hello emulatora DB rozwiązania Cosmos Azure udostępnia środowisko emulowanej uruchomione na stacji roboczej developer lokalnego, istnieją pewne różnice w działaniu między hello emulatora i konto bazy danych Azure rozwiązania Cosmos w chmurze hello:

* Hello Azure rozwiązania Cosmos DB emulatora obsługuje tylko jedno konto stałych i dobrze znane klucza głównego.  Ponowne generowanie klucza nie jest możliwe w hello Azure rozwiązania Cosmos DB emulatora.
* Hello Azure rozwiązania Cosmos DB emulatora nie jest skalowalna usługi i nie będzie obsługiwać dużą liczbę kolekcji.
* Hello Azure rozwiązania Cosmos DB emulatora nie symulować różne [poziomy spójności bazy danych Azure rozwiązania Cosmos](consistency-levels.md).
* Hello Azure rozwiązania Cosmos DB emulatora nie zasymulować [replikacji w przypadku](distribute-data-globally.md).
* Hello Azure rozwiązania Cosmos DB emulatora nie obsługuje hello zastąpienia przydziału usługi, które są dostępne w usłudze Azure DB rozwiązania Cosmos hello (limity rozmiaru dokumentu, zwiększenie kolekcji partycjonowanych magazynu).
* Jako kopię hello Azure rozwiązania Cosmos DB emulatora może nie być w górę toodate z hello najnowszych zmian w usłudze Azure DB rozwiązania Cosmos hello, użyj [planistę wydajności bazy danych Azure rozwiązania Cosmos](https://www.documentdb.com/capacityplanner) tooaccurately szacowania produkcji przepływności (RUs) wymagania dotyczące aplikacji.

## <a id="set-partitioncount"></a>Zmień hello liczby kolekcji

Domyślnie można utworzyć kolekcje z jedną partycją too25 lub 1 kolekcji podzielone na partycje przy użyciu hello Azure rozwiązania Cosmos DB emulatora. Zmieniając hello **PartitionCount** wartości, możesz utworzyć kolekcje z jedną partycją too250 lub 10 kolekcji partycjonowanych lub dowolną kombinację hello dwa niezawierającą więcej niż 250 pojedynczej partycji (gdzie 1 na partycje Kolekcja = 25 Kolekcja jednej partycji).

Jeśli toocreate kolekcji po hello bieżąca liczba partycji została przekroczona, emulatora hello zgłasza wyjątek ServiceUnavailable z następującą wiadomości powitania.

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    toobring more and more capacity online, and encourage you tootry again. 
    Please do not hesitate tooemail docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

toohello dostępne kolekcje emulatora usługi Azure rozwiązania Cosmos bazy danych, liczba hello toochange hello następujące:

1. Usunięcie wszystkich lokalnych danych Azure rozwiązania Cosmos DB emulatora klikając prawym przyciskiem myszy hello **Azure rozwiązania Cosmos DB emulatora** na powitania na pasku zadań, a następnie klikając ikonę **zresetować danych...** .
2. Usunięcie wszystkich danych emulatora w tym folderze C:\Users\user_name\AppData\Local\CosmosDBEmulator.
3. Zamknij wszystkie otwarte wystąpienia, klikając prawym przyciskiem myszy hello **Azure rozwiązania Cosmos DB emulatora** na powitania na pasku zadań, a następnie klikając ikonę **zakończenia**. Może upłynąć kilka minut dla wszystkich wystąpień tooexit.
4. Zainstaluj najnowszą wersję hello hello [Azure rozwiązania Cosmos DB emulatora](https://aka.ms/cosmosdb-emulator).
5. Uruchamianie emulatora hello z hello PartitionCount flagi, ustawiając wartość < = 250. Na przykład: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.

## <a name="troubleshooting"></a>Rozwiązywanie problemów

Użyj hello następujące porady toohelp Rozwiązywanie problemów związanych z emulatora bazy danych Azure rozwiązania Cosmos hello:

- Jeśli po zainstalowaniu nowej wersji hello emulatora występują błędy, upewnij się, że możesz zresetować danych. Dane można zresetować prawym przyciskiem myszy ikonę emulatora DB rozwiązania Cosmos Azure hello na powitania na pasku zadań, a następnie klikając polecenie resetowania danych... Jeśli to nie rozwiąże hello błędy, możesz odinstalować i ponowne zainstalowanie aplikacji hello. Zobacz [odinstalować emulatora lokalne powitania](#uninstall) instrukcje.

- Jeśli emulator usługi Azure DB rozwiązania Cosmos hello ulegnie awarii, zbieranie plików zrzutu z folderu c:\Users\user_name\AppData\Local\CrashDumps, kompresować i dołącz je tooan poczty e-mail zbyt[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

- Jeśli występują awarie w CosmosDB.StartupEntryPoint.exe, uruchom następujące polecenie w wierszu polecenia administratora z hello:`lodctr /R` 

- Jeśli wystąpi problem z łącznością [zbierać pliki śledzenia](#trace-files)kompresować i dołącz je tooan poczty e-mail zbyt[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

- Jeśli zostanie wyświetlony **Usługa niedostępna** komunikatów, hello emulatora może być niepowodzenie stos sieciowy hello tooinitialize. Toosee wyboru Jeśli masz hello Pulse secure klienta lub Juniper sieci zainstalowanego klienta, zgodnie z ich sterowniki filtrów sieci może spowodować hello problem. Odinstalowywanie sterowników filtrów innej sieci zazwyczaj rozwiązuje problem hello.

### <a id="trace-files"></a>Zbierz pliki śledzenia

toocollect debugowanie ślady, uruchom następujące polecenia z wiersza polecenia z uprawnieniami administracyjnymi hello:

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. `CosmosDB.Emulator.exe /shutdown`. Obejrzyj hello systemu na pasku zadań toomake czy hello program został zamknięty, może upłynąć kilka minut. Można także po prostu kliknij **zakończenia** w interfejsie użytkownika emulatora bazy danych Azure rozwiązania Cosmos hello.
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. Odtwórz hello problem. Jeśli Eksplorator danych nie działa, wystarczy toowait dla tooopen przeglądarki hello kilka sekund toocatch hello błędu.
5. `CosmosDB.Emulator.exe /stoptraces`
6. Przejdź do zbyt`%ProgramFiles%\Azure Cosmos DB Emulator` i Znajdź hello docdbemulator_000001.etl pliku.
7. Wyślij plik etl hello wraz z Opisz kroki zbyt[ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com) do debugowania.

### <a id="uninstall"></a>Odinstaluj hello emulatora lokalnego

1. Zamknij wszystkie otwarte wystąpienia hello lokalnym emulatorze prawym przyciskiem myszy ikonę emulatora DB rozwiązania Cosmos Azure hello na powitania na pasku zadań, a następnie klikając przycisk Zakończ. Może upłynąć kilka minut dla wszystkich wystąpień tooexit.
2. W polu wyszukiwania systemu Windows hello wpisz **aplikacje i funkcje** i kliknij na powitania **aplikacje i funkcje (ustawienia systemowe)** wynik.
3. W hello listę aplikacji, przewiń zbyt**Azure rozwiązania Cosmos DB emulatora**, zaznacz go, kliknij przycisk **Odinstaluj**, upewnij się i kliknij przycisk **Odinstaluj** ponownie.
4. Po odinstalowaniu aplikacji hello Przejdź tooC:\Users\<użytkownika > folderu hello \AppData\Local\CosmosDBEmulator i delete. 

## <a name="next-steps"></a>Następne kroki

W tym samouczku wykonaniu hello następujące czynności:

> [!div class="checklist"]
> * Zainstalowane hello emulatora lokalnego
> * RAND hello Emulator na Docker dla systemu Windows
> * Uwierzytelnionego żądania.
> * Używane hello Eksploratora danych w hello emulatora
> * Wyeksportowane certyfikaty SSL
> * Wywoływana z wiersza polecenia hello hello emulatora
> * Pliki śledzenia zebranych

W tym samouczku kiedy znasz już jak toouse hello lokalnego Emulator wolnego rozwoju lokalnych. Można teraz kontynuować toohello następny samouczek i Dowiedz się, jak certyfikaty SSL emulatora tooexport. 

> [!div class="nextstepaction"]
> [Eksportowanie hello Azure rozwiązania Cosmos DB emulatora certyfikatów](local-emulator-export-ssl-certificates.md)
