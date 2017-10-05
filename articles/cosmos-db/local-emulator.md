---
title: "Opracowywanie lokalnie w emulatorze DB rozwiązania Cosmos Azure | Dokumentacja firmy Microsoft"
description: "Przy użyciu emulatora usługi Azure DB rozwiązania Cosmos, mogą tworzyć i testować aplikację lokalnie darmo, bez tworzenia subskrypcji platformy Azure."
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
ms.openlocfilehash: a0f6a845a345ebd4ef0a58abf4934ce400103109
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-azure-cosmos-db-emulator-for-local-development-and-testing"></a>Użyj emulatora usługi Azure rozwiązania Cosmos bazy danych dla lokalnych projektowania i testowania

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
  
Emulator DB rozwiązania Cosmos Azure zapewnia środowisko lokalne, które emuluje usługę Azure DB rozwiązania Cosmos do celów programistycznych. Przy użyciu emulatora usługi Azure DB rozwiązania Cosmos, mogą tworzyć i przetestować aplikację lokalnie, bez tworzenia subskrypcji platformy Azure lub ponoszenia kosztów. Po zakończeniu jak aplikacja działa w emulatorze DB rozwiązania Cosmos Azure, możesz przełączyć się do korzystania z konta bazy danych Azure rozwiązania Cosmos w chmurze.

W tym artykule opisano następujące zadania: 

> [!div class="checklist"]
> * Instalowanie w emulatorze
> * Uruchomiony Emulator na Docker dla systemu Windows
> * Uwierzytelniania żądania
> * Za pomocą Eksploratora danych w emulatorze
> * Eksportowanie certyfikatów SSL
> * Wywoływanie Emulator z wiersza polecenia
> * Zbieranie plików śledzenia

Zalecamy rozpoczęcie pracy od obejrzenia poniższego klipu wideo, w którym Kirill Gavrylyuk pokazano, jak rozpocząć pracę z emulatora usługi Azure DB rozwiązania Cosmos. Należy pamiętać, że wideo odwołuje się do emulatora jako Emulator usługi DocumentDB, ale samo narzędzie została zmieniona od Tynkowanie wideo emulatora usługi Azure DB rozwiązania Cosmos. Wszystkie informacje w wideo są nadal aktualne dla emulatora usługi Azure DB rozwiązania Cosmos. 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-the-emulator-works"></a>Jak działa Emulator
Emulator DB rozwiązania Cosmos Azure udostępnia emulacji o wysokiej wierności, usługi Azure DB rozwiązania Cosmos. Obsługuje ona identyczną funkcjonalność jako rozwiązania Cosmos bazy danych Azure, w tym obsługa tworzenia i badania dokumentów JSON, inicjowania obsługi administracyjnej i skalowanie kolekcje i wykonywania procedury składowane i wyzwalaczy. Mogą tworzyć i testowanie aplikacji przy użyciu emulatora usługi Azure DB rozwiązania Cosmos i wdrożyć je na platformie Azure w skali globalnej przez tylko jednego Konfiguracja punktu końcowego połączenia dla bazy danych Azure rozwiązania Cosmos.

Podczas utworzyliśmy emulacji lokalnej o wysokiej wierności, rzeczywista usługi bazy danych Azure rozwiązania Cosmos implementacja emulatora usługi Azure DB rozwiązania Cosmos jest inne niż w przypadku usługi. Na przykład emulatora usługi Azure DB rozwiązania Cosmos używa standardowe składniki systemu operacyjnego, takie jak lokalnego systemu plików dla stanu trwałego i stosu protokołu HTTPS dla łączności. Oznacza to, że niektóre funkcje, która zależy od infrastruktury platformy Azure, takich jak globalnej replikacji, jednocyfrowej milisekundy opóźnienia odczytuje i zapisuje i dostosowywalne poziomy spójności nie są dostępne za pośrednictwem emulatora usługi Azure DB rozwiązania Cosmos.

> [!NOTE]
> W tej chwili w emulatorze Eksploratora danych obsługuje tylko tworzenie kolekcji interfejsu API usługi DocumentDB i kolekcji bazy danych MongoDB. Eksplorator danych w emulatorze nie obsługuje obecnie Tworzenie tabel i wykresów. 

## <a name="system-requirements"></a>Wymagania systemowe
Emulator DB rozwiązania Cosmos Azure ma następujące wymagania dotyczące sprzętu i oprogramowania:

* Wymagania dotyczące oprogramowania
  * Windows Server 2012 R2, Windows Server 2016 lub Windows 10
*   Minimalne wymagania sprzętowe
  * 2 GB PAMIĘCI RAM
  * 10 GB dostępnego miejsca na dysku

## <a name="installation"></a>Instalacja
Można pobrać i zainstalować Emulator usługi Azure rozwiązania Cosmos bazy danych z [Microsoft Download Center](https://aka.ms/cosmosdb-emulator). 

> [!NOTE]
> Aby zainstalować, skonfigurować i uruchomić emulatora usługi Azure rozwiązania Cosmos bazy danych, musi mieć uprawnienia administratora na komputerze.

## <a name="running-on-docker-for-windows"></a>Systemem Docker dla systemu Windows

Emulator DB rozwiązania Cosmos Azure może działać w Docker dla systemu Windows. Emulator nie działają w Docker dla Oracle Linux.

Po utworzeniu [Docker dla systemu Windows](https://www.docker.com/docker-windows) zainstalowana, można umieścić obraz emulatora z Centrum Docker, uruchamiając następujące polecenie z ulubionych powłoki (cmd.exe, programu PowerShell, itp.).

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
Aby uruchomić obrazu, uruchom następujące polecenia.

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

Odpowiedź jest podobny do następującego:

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import the SSL certificate from an administrator command prompt on the host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

Zamykanie powłoki interakcyjne po Emulator uruchomiony spowoduje zamknięcie kontenera emulatora.

Przy użyciu punktu końcowego i klucz główny w z odpowiedzi na kliencie, a następnie zaimportowanie certyfikatu SSL do hosta. Aby zaimportować certyfikat protokołu SSL, wykonaj następujące polecenie w wierszu polecenia administratora:

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-the-emulator"></a>Uruchom Emulator

Aby uruchomić emulatora usługi Azure DB rozwiązania Cosmos, kliknij przycisk Start, lub naciśnij klawisz systemu Windows. Rozpocznij wpisywanie **Azure rozwiązania Cosmos DB emulatora**i wybierz z listy aplikacji emulator. 

![Kliknij przycisk Start lub naciśnij klawisz systemu Windows, rozpocznij wpisywanie ** Azure rozwiązania Cosmos DB emulatora **, a następnie wybierz z listy aplikacji jest to emulator](./media/local-emulator/database-local-emulator-start.png)

Po uruchomieniu emulatora będzie widoczna ikona w obszarze powiadomień paska zadań systemu Windows. ![Azure DB rozwiązania Cosmos emulatora lokalnym obszarze powiadomień paska zadań](./media/local-emulator/database-local-emulator-taskbar.png)

Emulator usługi Azure rozwiązania Cosmos DB domyślnie uruchamiane na komputerze lokalnym ("localhost") nasłuchuje na porcie 8081.

Emulatora usługi Azure DB rozwiązania Cosmos jest instalowana domyślnie `C:\Program Files\Azure Cosmos DB Emulator` katalogu. Można również uruchomić i zatrzymać emulatora z wiersza polecenia. Zobacz [odwołanie do narzędzia wiersza polecenia](#command-line) Aby uzyskać więcej informacji.

## <a name="start-data-explorer"></a>Uruchom Eksploratora danych

Po uruchomieniu emulatora bazy danych Azure rozwiązania Cosmos w przeglądarce zostanie otwarty automatycznie Eksploratora danych Azure rozwiązania Cosmos bazy danych. Adres będzie wyświetlany jako [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html). Zamknij Eksploratora, aby otworzyć go ponownie później możesz otworzyć adresu URL w przeglądarce lub uruchomić go z emulatora usługi Azure rozwiązania Cosmos bazy danych w ikonie na pasku zadań systemu Windows, jak pokazano poniżej.

![Azure uruchamiania Eksploratora danych lokalnych emulatora DB rozwiązania Cosmos](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a>Sprawdzanie dostępności aktualizacji
Eksplorator danych wskazuje, czy jest nowe aktualizacje dostępne do pobrania. 

> [!NOTE]
> Dane utworzone w jednej wersji emulatora usługi Azure rozwiązania Cosmos bazy danych nie jest gwarantowana była dostępna, gdy w innej wersji. Jeśli musisz utrwalić danych długoterminowym, zaleca się przechowywania tych danych w ramach konta bazy danych rozwiązania Cosmos Azure, a nie w emulatorze Azure DB rozwiązania Cosmos. 

## <a name="authenticating-requests"></a>Uwierzytelniania żądania
Podobnie jak Azure DB rozwiązania Cosmos w chmurze, każde żądanie, wprowadzone przed emulatora usługi Azure DB rozwiązania Cosmos musi zostać uwierzytelniony. Emulator DB rozwiązania Cosmos Azure obsługuje jednego stałego konta i klucz uwierzytelniania dobrze znanego uwierzytelniania klucza głównego. Tego konta i klucz są tylko poświadczenia do użycia z emulatora usługi Azure DB rozwiązania Cosmos. Są to:

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> Klucz główny obsługiwane przez Emulator usługi Azure DB rozwiązania Cosmos jest przeznaczony do użytku z emulatora. Nie można używać swojego konta bazy danych Azure rozwiązania Cosmos produkcyjnych i klucz emulatora usługi Azure DB rozwiązania Cosmos. 

> [!NOTE] 
> Jeśli emulator została uruchomiona z opcją następujący/key, użyj wygenerowany klucz zamiast "obiektów relacyjnych C2y6yDjf5 + ob0N8A7Cgv30VRDJIWEHLM 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw =="

Ponadto po prostu co w usłudze Azure DB rozwiązania Cosmos emulatora usługi Azure DB rozwiązania Cosmos obsługuje tylko bezpiecznej komunikacji za pośrednictwem protokołu SSL.

## <a name="running-the-emulator-on-a-local-network"></a>Uruchomiony emulator w sieci lokalnej

W sieci lokalnej, możesz uruchomić emulatora. Aby włączyć dostęp do sieci, należy określić opcję /AllowNetworkAccess w [wiersza polecenia](#command-line-syntax), które również wymaga określenia następujący/key = key_string lub/KeyFile = nazwa_pliku. Można użyć /GenKeyFile = nazwa_pliku, aby wygenerować plik z wyprzedzeniem losowy klucz.  Następnie można przekazać, że/KeyFile = nazwa_pliku lub następujący/key = contents_of_file.

Aby włączyć dostęp do sieci po raz pierwszy użytkownik powinien zamknięcia emulatora i usunąć katalog danych emulatora (C:\Users\user_name\AppData\Local\CosmosDBEmulator).

## <a name="developing-with-the-emulator"></a>Tworzenie w emulatorze
Po utworzeniu emulatora DB rozwiązania Cosmos Azure uruchomiony na pulpicie, można użyć dowolnego obsługiwane [zestawu SDK usługi Azure rozwiązania Cosmos DB](documentdb-sdk-dotnet.md) lub [interfejsu API REST Azure rozwiązania Cosmos DB](/rest/api/documentdb/) wchodzić w interakcje z emulatora. Emulator DB rozwiązania Cosmos Azure obejmuje również wbudowane Eksploratora danych, który umożliwia tworzenie kolekcji usługi DocumentDB, bazy danych MongoDB interfejsów API i widoku i edycji dokumentów bez pisania żadnego kodu.   

    // Connect to the Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

Jeśli używasz [obsługą protokołu bazy danych Azure rozwiązania Cosmos bazy danych mongodb](mongodb-introduction.md), użyj następujący ciąg połączenia:

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

Można użyć istniejących narzędzi, takich jak [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) nawiązać emulatora usługi Azure DB rozwiązania Cosmos. Można również migrację danych między emulatora DB rozwiązania Cosmos Azure i przy użyciu usługi Azure DB rozwiązania Cosmos [narzędzia migracji danych DB rozwiązania Cosmos Azure](https://github.com/azure/azure-documentdb-datamigrationtool).

> [!NOTE] 
> Jeśli emulator została uruchomiona z opcją następujący/key, użyj wygenerowany klucz zamiast "obiektów relacyjnych C2y6yDjf5 + ob0N8A7Cgv30VRDJIWEHLM 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw =="

Domyślnie przy użyciu emulatora usługi Azure DB rozwiązania Cosmos, można utworzyć maksymalnie 25 kolekcje z jedną partycją lub 1 kolekcji podzielone na partycje. Aby uzyskać więcej informacji na temat Zmiana tej wartości, zobacz [ustawienie wartości PartitionCount](#set-partitioncount).

## <a name="export-the-ssl-certificate"></a>Wyeksportuj certyfikat protokołu SSL

Języków .NET i środowiska uruchomieniowego umożliwia bezpieczne łączenie z emulatora lokalnej bazy danych Azure rozwiązania Cosmos magazynu certyfikatów systemu Windows. Inne języki ma swoje własne metody przy użyciu certyfikatów oraz zarządzania nimi. Java używa własnego [magazyn certyfikatów](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) natomiast używa języka Python [gniazda otoki](https://docs.python.org/2/library/ssl.html).

Aby uzyskać certyfikat do użycia z języków i środowisk uruchomieniowych, który nie jest integrowana z magazynu certyfikatów systemu Windows należy wyeksportować go przy użyciu Menedżera certyfikatów systemu Windows. Można go uruchomić, uruchamiając certlm.msc lub postępuj zgodnie z instrukcjami krok po kroku [wyeksportowanie certyfikatów emulatora DB rozwiązania Cosmos Azure](./local-emulator-export-ssl-certificates.md). Po uruchomieniu Menedżera certyfikatów, otwórz certyfikatów osobistych, jak pokazano poniżej i wyeksportować certyfikat o przyjaznej nazwie "DocumentDBEmulatorCertificate", zgodnie z algorytmem BASE-64 pliku X.509 (.cer).

![Azure certyfikat SSL lokalnym emulatorze DB rozwiązania Cosmos](./media/local-emulator/database-local-emulator-ssl_certificate.png)

Certyfikat X.509 można zaimportować do magazynu certyfikatów Java zgodnie z instrukcjami w [Dodawanie certyfikatu do magazynu certyfikatów urzędu certyfikacji Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store). Po zaimportowaniu certyfikatu do magazynu certyfikatów aplikacji Java i bazy danych MongoDB będzie można nawiązać połączenia z emulatora usługi Azure DB rozwiązania Cosmos.

Podczas łączenia z emulatora, Python i Node.js SDK, weryfikacji SSL jest wyłączona.

## <a id="command-line"></a>Odwołanie do narzędzia wiersza polecenia
Z lokalizacji instalacji możesz użyć wiersza polecenia do uruchamiania i zatrzymywania emulator, skonfiguruj opcje i wykonywać inne operacje.

### <a name="command-line-syntax"></a>Składnia wiersza polecenia

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

Aby wyświetlić listę opcji, należy wpisać `CosmosDB.Emulator.exe /?` w wierszu polecenia.

<table>
<tr>
  <td><strong>Opcja</strong></td>
  <td><strong>Opis</strong></td>
  <td><strong>Polecenie</strong></td>
  <td><strong>Argumenty</strong></td>
</tr>
<tr>
  <td>[Brak argumentów]</td>
  <td>Uruchamiania emulatora usługi Azure rozwiązania Cosmos bazy danych przy użyciu ustawień domyślnych.</td>
  <td>CosmosDB.Emulator.exe</td>
  <td></td>
</tr>
<tr>
  <td>[Pomoc]</td>
  <td>Wyświetla listę obsługiwanych argumentów wiersza polecenia.</td>
  <td>CosmosDB.Emulator.exe /?</td>
  <td></td>
</tr>
<tr>
  <td>Zamknięcie</td>
  <td>Zamyka emulatora usługi Azure DB rozwiązania Cosmos.</td>
  <td>/ Shutdown CosmosDB.Emulator.exe</td>
  <td></td>
</tr>
<tr>
  <td>Ścieżki danych</td>
  <td>Określa ścieżkę, w której chcesz przechowywać pliki danych. Domyślnie jest to % LocalAppdata%\CosmosDBEmulator.</td>
  <td>CosmosDB.Emulator.exe /DataPath =&lt;ścieżki danych&gt;</td>
  <td>&lt;ścieżki danych&gt;: dostępną ścieżkę</td>
</tr>
<tr>
  <td>Port</td>
  <td>Określa numer portu używany dla emulatora.  Domyślnie jest 8081.</td>
  <td>/ CosmosDB.Emulator.exe port =&lt;portu&gt;</td>
  <td>&lt;port&gt;: numer pojedynczego portu</td>
</tr>
<tr>
  <td>MongoPort</td>
  <td>Określa numer portu na potrzeby zgodności bazy danych MongoDB interfejsu API. Domyślnie jest 10255.</td>
  <td>CosmosDB.Emulator.exe /MongoPort =&lt;mongoport&gt;</td>
  <td>&lt;mongoport&gt;: numer pojedynczego portu</td>
</tr>
<tr>
  <td>DirectPorts</td>
  <td>Określa portów na potrzeby połączeń bezpośrednich. Wartości domyślne są 10251,10252,10253,10254.</td>
  <td>CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</td>
  <td>&lt;directports&gt;: rozdzielana przecinkami lista portów 4</td>
</tr>
<tr>
  <td>Klucz</td>
  <td>Klucz autoryzacji dla emulatora. Klucz musi być kodowanie base-64 wektor 64 bajtów.</td>
  <td>CosmosDB.Emulator.exe następujący/key:&lt;klucza&gt;</td>
  <td>&lt;klucz&gt;: klucz musi być kodowanie base-64 wektor 64 bajtów</td>
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
  <td>Nie pokazuj emulator interfejsu użytkownika.</td>
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
  <td>Określa maksymalną liczbę kolekcji partycjonowanych. Zobacz [zmienić liczby kolekcji](#set-partitioncount) Aby uzyskać więcej informacji.</td>
  <td>CosmosDB.Emulator.exe /PartitionCount =&lt;liczba partycji&gt;</td>
  <td>&lt;Liczba partycji&gt;: Maksymalna liczba dozwolonych kolekcje z jedną partycją. Domyślna to 25. Maksymalna dozwolona wartość to 250.</td>
</tr>
<tr>
  <td>DefaultPartitionCount</td>
  <td>Określa domyślny numer partycji dla kolekcji partycjonowanych.</td>
  <td>CosmosDB.Emulator.exe /DefaultPartitionCount =&lt;defaultpartitioncount&gt;</td>
  <td>&lt;defaultpartitioncount&gt; domyślna to 25.</td>
</tr>
<tr>
  <td>AllowNetworkAccess</td>
  <td>Zapewnia dostęp do emulatora za pośrednictwem sieci. Należy także podać następujący/key =&lt;key_string&gt; lub/KeyFile =&lt;nazwa_pliku&gt; umożliwiające dostęp do sieci.</td>
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
  <td>Wygeneruj nowy klucz autoryzacji i Zapisz do określonego pliku. Przy użyciu opcji następujący/key lub/KeyFile można użyć wygenerowanego klucza.</td>
  <td>CosmosDB.Emulator.exe /GenKeyFile =&lt;ścieżka do pliku klucza&gt;</td>
  <td></td>
</tr>
<tr>
  <td>Spójność</td>
  <td>Ustaw domyślny poziom spójności dla konta.</td>
  <td>CosmosDB.Emulator.exe /Consistency =&lt;spójności&gt;</td>
  <td>&lt;spójność&gt;: wartość musi być jedną z następujących [poziomy spójności](consistency-levels.md): sesja, silne, Eventual lub BoundedStaleness.  Wartość domyślna to sesji.</td>
</tr>
<tr>
  <td>?</td>
  <td>Pokaż komunikat pomocy.</td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-the-azure-cosmos-db-emulator-and-azure-cosmos-db"></a>Różnice między emulatora usługi Azure rozwiązania Cosmos bazy danych i bazy danych Azure rozwiązania Cosmos 
Ponieważ Emulator DB rozwiązania Cosmos Azure udostępnia środowisko emulowanej uruchomione na stacji roboczej developer lokalnego, istnieją pewne różnice w działaniu między emulatora i konto bazy danych Azure rozwiązania Cosmos w chmurze:

* Emulatora usługi Azure DB rozwiązania Cosmos obsługuje tylko jedno konto stałych i dobrze znane klucza głównego.  Ponowne generowanie klucza nie jest możliwe w emulatorze Azure DB rozwiązania Cosmos.
* Emulatora usługi Azure rozwiązania Cosmos bazy danych nie jest skalowalna usługi i nie będzie obsługiwać dużą liczbę kolekcji.
* Emulatora usługi Azure DB rozwiązania Cosmos nie symulować różne [poziomy spójności bazy danych Azure rozwiązania Cosmos](consistency-levels.md).
* Emulator usługi Azure DB rozwiązania Cosmos nie zasymulować [replikacji w przypadku](distribute-data-globally.md).
* Emulator DB rozwiązania Cosmos Azure nie obsługuje zastąpienia przydziału usługi, które są dostępne w usłudze Azure DB rozwiązania Cosmos (np. limity rozmiaru dokumentu, zwiększenie kolekcji partycjonowanych magazynu).
* Jako kopię emulatora usługi Azure DB rozwiązania Cosmos mogą nie być aktualne informacje o najnowszych zmian w usłudze Azure DB rozwiązania Cosmos, użyj [planistę wydajności bazy danych Azure rozwiązania Cosmos](https://www.documentdb.com/capacityplanner) Aby dokładnie oszacować produkcyjnym wymagania dotyczące przepływności (RUs) aplikacji.

## <a id="set-partitioncount"></a>Zmiana liczby kolekcji

Domyślnie można utworzyć maksymalnie 25 kolekcje z jedną partycją lub 1 kolekcji podzielone na partycje przy użyciu emulatora usługi Azure DB rozwiązania Cosmos. Zmieniając **PartitionCount** wartości, możesz utworzyć maksymalnie 250 kolekcje z jedną partycją lub 10 kolekcji partycjonowanych lub dowolną kombinację dwa niezawierającą więcej niż 250 jednej partycji (gdzie 1 na partycje kolekcji = 25 Kolekcja jednej partycji).

Jeśli próbujesz utworzyć kolekcję po bieżąca liczba partycji została przekroczona, emulator zgłasza wyjątek ServiceUnavailable, następujący komunikat o błędzie.

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    to bring more and more capacity online, and encourage you to try again. 
    Please do not hesitate to email docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

Aby zmienić liczby kolekcji dostępne emulatora usługi Azure rozwiązania Cosmos bazy danych, wykonaj następujące czynności:

1. Usunięcie wszystkich lokalnych danych Azure rozwiązania Cosmos DB emulatora klikając prawym przyciskiem myszy **Azure rozwiązania Cosmos DB emulatora** ikonę na pasku zadań, a następnie klikając **zresetować danych...** .
2. Usunięcie wszystkich danych emulatora w tym folderze C:\Users\user_name\AppData\Local\CosmosDBEmulator.
3. Zamknij wszystkie otwarte wystąpienia, klikając prawym przyciskiem myszy **Azure rozwiązania Cosmos DB emulatora** ikonę na pasku zadań, a następnie klikając **zakończenia**. Może upłynąć kilka minut dla wszystkich wystąpień zakończyć.
4. Zainstaluj najnowszą wersję pakietu [Azure rozwiązania Cosmos DB emulatora](https://aka.ms/cosmosdb-emulator).
5. Uruchom emulator z flagą PartitionCount przez ustawienie wartości < = 250. Na przykład: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.

## <a name="troubleshooting"></a>Rozwiązywanie problemów

Do rozwiązywania problemów związanych z emulatora bazy danych Azure rozwiązania Cosmos, należy użyć następujących wskazówek:

- Jeśli po zainstalowaniu nowej wersji emulatora występują błędy, upewnij się, że możesz zresetować danych. Dane można zresetować prawym przyciskiem myszy ikonę emulatora DB rozwiązania Cosmos Azure na pasku zadań, a następnie klikając pozycję Zresetuj danych... Jeśli to nie rozwiąże błędy, możesz odinstalować i ponownie zainstalować aplikację. Zobacz [odinstalować lokalnym emulatorze](#uninstall) instrukcje.

- Jeśli emulator usługi Azure DB rozwiązania Cosmos ulegnie awarii, zbieranie plików zrzutu z folderu c:\Users\user_name\AppData\Local\CrashDumps kompresować i dołącz je do wiadomości e-mail do [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com).

- Jeśli występują awarie w CosmosDB.StartupEntryPoint.exe, uruchom następujące polecenie z wiersza polecenia z uprawnieniami administratora:`lodctr /R` 

- Jeśli wystąpi problem z łącznością [zbierać pliki śledzenia](#trace-files)kompresować i dołącz je do wiadomości e-mail do [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com).

- Jeśli zostanie wyświetlony **Usługa niedostępna** wiadomości, emulator może nie można zainicjować stos sieciowy. Sprawdź, czy masz klienta bezpiecznym impulsu lub Juniper sieci zainstalowanego klienta, zgodnie z ich sterowniki filtrów sieci może spowodować problem. Odinstalowywanie sterowników filtrów innej sieci zazwyczaj rozwiązuje problem.

### <a id="trace-files"></a>Zbierz pliki śledzenia

Aby zbierać dane śledzenia debugowania, uruchom następujące polecenia z wiersza polecenia z uprawnieniami administracyjnymi:

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. `CosmosDB.Emulator.exe /shutdown`. Obejrzyj pasku zadań, aby upewnić się, że program został zamknięty, może upłynąć kilka minut. Można także po prostu kliknij **zakończenia** w interfejsie użytkownika emulatora bazy danych Azure rozwiązania Cosmos.
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. Odtwórz problem. Jeśli Eksplorator danych nie działa, wystarczy poczekać przeglądarkę, aby otworzyć catch błąd kilka sekund.
5. `CosmosDB.Emulator.exe /stoptraces`
6. Przejdź do `%ProgramFiles%\Azure Cosmos DB Emulator` i Znajdź plik docdbemulator_000001.etl.
7. Wyślij plik ETL oraz reprodukcja kroki umożliwiające [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com) do debugowania.

### <a id="uninstall"></a>Odinstaluj lokalnym emulatorze

1. Zamknij wszystkie otwarte wystąpienia lokalnego emulatora prawym przyciskiem myszy ikonę emulatora DB rozwiązania Cosmos Azure na pasku zadań, a następnie klikając przycisk Zakończ. Może upłynąć kilka minut dla wszystkich wystąpień zakończyć.
2. W polu wyszukiwania systemu Windows wpisz **aplikacje i funkcje** i wybierz polecenie **aplikacje i funkcje (ustawienia systemowe)** wynik.
3. Na liście aplikacji, przewiń do **Azure rozwiązania Cosmos DB emulatora**, zaznacz go, kliknij przycisk **Odinstaluj**, upewnij się i kliknij przycisk **Odinstaluj** ponownie.
4. Gdy aplikacja zostanie odinstalowana, przejdź do C:\Users\<użytkownika > \AppData\Local\CosmosDBEmulator i usuwania folderu. 

## <a name="next-steps"></a>Następne kroki

W tym samouczku wykonaniu następujących czynności:

> [!div class="checklist"]
> * Zainstalowane lokalne emulatora
> * RAND Emulator na Docker dla systemu Windows
> * Uwierzytelnionego żądania.
> * Używane w emulatorze Eksploratora danych
> * Wyeksportowane certyfikaty SSL
> * Wywołuje się, Emulator z wiersza polecenia
> * Pliki śledzenia zebranych

W tym samouczku kiedy znasz już sposób użycia lokalnego emulatora wolnego rozwoju lokalnych. Możesz teraz przejść do następnego samouczek i informacje o sposobie eksportowania certyfikatów SSL emulatora. 

> [!div class="nextstepaction"]
> [Wyeksportowanie certyfikatów emulatora DB rozwiązania Cosmos Azure](local-emulator-export-ssl-certificates.md)
