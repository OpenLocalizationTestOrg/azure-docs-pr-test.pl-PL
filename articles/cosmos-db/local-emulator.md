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
# <a name="use-hello-azure-cosmos-db-emulator-for-local-development-and-testing"></a><span data-ttu-id="49dad-104">Użyj dla lokalnego projektowania i testowania hello Azure rozwiązania Cosmos DB emulatora</span><span class="sxs-lookup"><span data-stu-id="49dad-104">Use hello Azure Cosmos DB Emulator for local development and testing</span></span>

<table>
<tr>
  <td><span data-ttu-id="49dad-105"><strong>Pliki binarne</strong></span><span class="sxs-lookup"><span data-stu-id="49dad-105"><strong>Binaries</strong></span></span></td>
  <td>[<span data-ttu-id="49dad-106">Pobieranie pliku MSI</span><span class="sxs-lookup"><span data-stu-id="49dad-106">Download MSI</span></span>](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><span data-ttu-id="49dad-107"><strong>Docker</strong></span><span class="sxs-lookup"><span data-stu-id="49dad-107"><strong>Docker</strong></span></span></td>
  <td>[<span data-ttu-id="49dad-108">Centrum docker</span><span class="sxs-lookup"><span data-stu-id="49dad-108">Docker Hub</span></span>](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><span data-ttu-id="49dad-109"><strong>Źródło docker</strong></span><span class="sxs-lookup"><span data-stu-id="49dad-109"><strong>Docker source</strong></span></span></td>
  <td>[<span data-ttu-id="49dad-110">Github</span><span class="sxs-lookup"><span data-stu-id="49dad-110">Github</span></span>](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
<span data-ttu-id="49dad-111">Hello Azure rozwiązania Cosmos DB emulatora zapewnia środowisko lokalne, które emuluje hello Azure DB rozwiązania Cosmos usługi do celów programistycznych.</span><span class="sxs-lookup"><span data-stu-id="49dad-111">hello Azure Cosmos DB Emulator provides a local environment that emulates hello Azure Cosmos DB service for development purposes.</span></span> <span data-ttu-id="49dad-112">Przy użyciu hello Azure rozwiązania Cosmos DB emulatora, mogą tworzyć i przetestować aplikację lokalnie, bez tworzenia subskrypcji platformy Azure lub ponoszenia kosztów.</span><span class="sxs-lookup"><span data-stu-id="49dad-112">Using hello Azure Cosmos DB Emulator, you can develop and test your application locally, without creating an Azure subscription or incurring any costs.</span></span> <span data-ttu-id="49dad-113">Po zakończeniu jak aplikacja działa na platformie hello Azure rozwiązania Cosmos DB emulatora, możesz przełączyć toousing konto bazy danych Azure rozwiązania Cosmos w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="49dad-113">When you're satisfied with how your application is working in hello Azure Cosmos DB Emulator, you can switch toousing an Azure Cosmos DB account in hello cloud.</span></span>

<span data-ttu-id="49dad-114">W tym artykule omówiono hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="49dad-114">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="49dad-115">Instalowanie hello emulatora</span><span class="sxs-lookup"><span data-stu-id="49dad-115">Installing hello Emulator</span></span>
> * <span data-ttu-id="49dad-116">Uruchomiony hello Emulator na Docker dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="49dad-116">Running hello Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="49dad-117">Uwierzytelniania żądania</span><span class="sxs-lookup"><span data-stu-id="49dad-117">Authenticating requests</span></span>
> * <span data-ttu-id="49dad-118">Przy użyciu hello Eksploratora danych w hello emulatora</span><span class="sxs-lookup"><span data-stu-id="49dad-118">Using hello Data Explorer in hello Emulator</span></span>
> * <span data-ttu-id="49dad-119">Eksportowanie certyfikatów SSL</span><span class="sxs-lookup"><span data-stu-id="49dad-119">Exporting SSL certificates</span></span>
> * <span data-ttu-id="49dad-120">Wywoływanie z wiersza polecenia hello hello emulatora</span><span class="sxs-lookup"><span data-stu-id="49dad-120">Calling hello Emulator from hello command line</span></span>
> * <span data-ttu-id="49dad-121">Zbieranie plików śledzenia</span><span class="sxs-lookup"><span data-stu-id="49dad-121">Collecting trace files</span></span>

<span data-ttu-id="49dad-122">Zalecamy rozpoczęcie pracy od obejrzenia powitania po wideo, w którym Kirill Gavrylyuk pokazuje, jak tooget pracę z hello Azure rozwiązania Cosmos DB emulatora.</span><span class="sxs-lookup"><span data-stu-id="49dad-122">We recommend getting started by watching hello following video, where Kirill Gavrylyuk shows how tooget started with hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="49dad-123">Uwaga wideo hello stosowany jest wspólny termin emulatora toohello hello emulatora usługi DocumentDB, że zmieniono nazwę samego narzędzia hello hello Azure rozwiązania Cosmos DB emulatora od Tynkowanie hello wideo.</span><span class="sxs-lookup"><span data-stu-id="49dad-123">Note that hello video refers toohello emulator as hello DocumentDB Emulator, but hello tool itself has been renamed hello Azure Cosmos DB Emulator since taping hello video.</span></span> <span data-ttu-id="49dad-124">Wszystkie informacje w hello wideo są nadal aktualne dla hello Azure rozwiązania Cosmos DB emulatora.</span><span class="sxs-lookup"><span data-stu-id="49dad-124">All information in hello video is still accurate for hello Azure Cosmos DB Emulator.</span></span> 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-hello-emulator-works"></a><span data-ttu-id="49dad-125">Jak działa hello emulatora</span><span class="sxs-lookup"><span data-stu-id="49dad-125">How hello Emulator works</span></span>
<span data-ttu-id="49dad-126">Hello emulatora DB rozwiązania Cosmos Azure udostępnia emulację o wysokiej wierności hello usługi bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="49dad-126">hello Azure Cosmos DB Emulator provides a high-fidelity emulation of hello Azure Cosmos DB service.</span></span> <span data-ttu-id="49dad-127">Obsługuje ona identyczną funkcjonalność jako rozwiązania Cosmos bazy danych Azure, w tym obsługa tworzenia i badania dokumentów JSON, inicjowania obsługi administracyjnej i skalowanie kolekcje i wykonywania procedury składowane i wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="49dad-127">It supports identical functionality as Azure Cosmos DB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers.</span></span> <span data-ttu-id="49dad-128">Mogą tworzyć i testowanie aplikacji za pomocą hello Azure rozwiązania Cosmos DB emulatora i wdrażać je tooAzure w skali globalnej poprzez tylko pojedynczą konfiguracją zmienić toohello punktu końcowego połączenia dla bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="49dad-128">You can develop and test applications using hello Azure Cosmos DB Emulator, and deploy them tooAzure at global scale by just making a single configuration change toohello connection endpoint for Azure Cosmos DB.</span></span>

<span data-ttu-id="49dad-129">Gdy utworzyliśmy emulacji lokalnej o wysokiej wierności, rzeczywista usługi bazy danych Azure rozwiązania Cosmos hello hello implementacja hello Azure rozwiązania Cosmos DB emulatora różni się od hello usługi.</span><span class="sxs-lookup"><span data-stu-id="49dad-129">While we created a high-fidelity local emulation of hello actual Azure Cosmos DB service, hello implementation of hello Azure Cosmos DB Emulator is different than that of hello service.</span></span> <span data-ttu-id="49dad-130">Na przykład hello Azure rozwiązania Cosmos DB emulatora używa standardowych składniki systemu operacyjnego, takie jak hello lokalnego systemu plików dla stanu trwałego i stosu protokołu HTTPS dla łączności.</span><span class="sxs-lookup"><span data-stu-id="49dad-130">For example, hello Azure Cosmos DB Emulator uses standard OS components such as hello local file system for persistence, and HTTPS protocol stack for connectivity.</span></span> <span data-ttu-id="49dad-131">Oznacza to, że niektóre funkcje, która zależy od infrastruktury platformy Azure, takich jak globalnej replikacji, jednocyfrowej milisekundy opóźnienia odczytuje i zapisuje i dostosowywalne poziomy spójności nie są dostępne za pośrednictwem hello Azure rozwiązania Cosmos DB emulatora.</span><span class="sxs-lookup"><span data-stu-id="49dad-131">This means that some functionality that relies on Azure infrastructure like global replication, single-digit millisecond latency for reads/writes, and tunable consistency levels are not available via hello Azure Cosmos DB Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="49dad-132">W tym hello czasu Eksploratora danych w hello emulatora obsługuje tylko tworzenie hello kolekcji interfejsu API usługi DocumentDB i kolekcji bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="49dad-132">At this time hello Data Explorer in hello emulator only supports hello creation of DocumentDB API collections and MongoDB collections.</span></span> <span data-ttu-id="49dad-133">Witaj Eksploratora danych w emulatorze hello nie obsługuje obecnie hello Tworzenie tabel i wykresów.</span><span class="sxs-lookup"><span data-stu-id="49dad-133">hello Data Explorer in hello emulator does not currently support hello creation of tables and graphs.</span></span> 

## <a name="system-requirements"></a><span data-ttu-id="49dad-134">Wymagania systemowe</span><span class="sxs-lookup"><span data-stu-id="49dad-134">System requirements</span></span>
<span data-ttu-id="49dad-135">Hello Azure rozwiązania Cosmos DB Emulator ma następujące wymagania sprzętowe i programowe hello:</span><span class="sxs-lookup"><span data-stu-id="49dad-135">hello Azure Cosmos DB Emulator has hello following hardware and software requirements:</span></span>

* <span data-ttu-id="49dad-136">Wymagania dotyczące oprogramowania</span><span class="sxs-lookup"><span data-stu-id="49dad-136">Software requirements</span></span>
  * <span data-ttu-id="49dad-137">Windows Server 2012 R2, Windows Server 2016 lub Windows 10</span><span class="sxs-lookup"><span data-stu-id="49dad-137">Windows Server 2012 R2, Windows Server 2016, or Windows 10</span></span>
*   <span data-ttu-id="49dad-138">Minimalne wymagania sprzętowe</span><span class="sxs-lookup"><span data-stu-id="49dad-138">Minimum Hardware requirements</span></span>
  * <span data-ttu-id="49dad-139">2 GB PAMIĘCI RAM</span><span class="sxs-lookup"><span data-stu-id="49dad-139">2 GB RAM</span></span>
  * <span data-ttu-id="49dad-140">10 GB dostępnego miejsca na dysku</span><span class="sxs-lookup"><span data-stu-id="49dad-140">10 GB available hard disk space</span></span>

## <a name="installation"></a><span data-ttu-id="49dad-141">Instalacja</span><span class="sxs-lookup"><span data-stu-id="49dad-141">Installation</span></span>
<span data-ttu-id="49dad-142">Można pobrać i zainstalować hello Azure rozwiązania Cosmos DB emulatora z hello [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="49dad-142">You can download and install hello Azure Cosmos DB Emulator from hello [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span></span> 

> [!NOTE]
> <span data-ttu-id="49dad-143">tooinstall, konfigurowania i uruchamiania hello Azure rozwiązania Cosmos DB emulatora, musisz mieć uprawnienia administracyjne na komputerze hello.</span><span class="sxs-lookup"><span data-stu-id="49dad-143">tooinstall, configure, and run hello Azure Cosmos DB Emulator, you must have administrative privileges on hello computer.</span></span>

## <a name="running-on-docker-for-windows"></a><span data-ttu-id="49dad-144">Systemem Docker dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="49dad-144">Running on Docker for Windows</span></span>

<span data-ttu-id="49dad-145">Witaj emulatora DB rozwiązania Cosmos Azure może działać w Docker dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="49dad-145">hello Azure Cosmos DB Emulator can be run on Docker for Windows.</span></span> <span data-ttu-id="49dad-146">Witaj emulatora nie działają w Docker dla Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="49dad-146">hello Emulator does not work on Docker for Oracle Linux.</span></span>

<span data-ttu-id="49dad-147">Po utworzeniu [Docker dla systemu Windows](https://www.docker.com/docker-windows) zainstalowana, można umieścić obraz emulatora hello z Centrum Docker, uruchamiając następujące polecenie z ulubionych powłoki hello (cmd.exe, programu PowerShell, itp.).</span><span class="sxs-lookup"><span data-stu-id="49dad-147">Once you have [Docker for Windows](https://www.docker.com/docker-windows) installed, you can pull hello Emulator image from Docker Hub by running hello following command from your favorite shell (cmd.exe, PowerShell, etc.).</span></span>

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
<span data-ttu-id="49dad-148">Obraz powitania toostart, uruchom następujące polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="49dad-148">toostart hello image, run hello following commands.</span></span>

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

<span data-ttu-id="49dad-149">odpowiedź Hello wygląda podobnie toohello następujące:</span><span class="sxs-lookup"><span data-stu-id="49dad-149">hello response looks similar toohello following:</span></span>

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

<span data-ttu-id="49dad-150">Zamykanie powłoki interakcyjne hello po hello, który został uruchomiony Emulator będzie emulatora hello zamknięcie kontenera.</span><span class="sxs-lookup"><span data-stu-id="49dad-150">Closing hello interactive shell once hello Emulator has been started will shutdown hello Emulator’s container.</span></span>

<span data-ttu-id="49dad-151">Przy użyciu hello punktu końcowego i klucz główny w z hello odpowiedzi na kliencie, a następnie zaimportowanie certyfikatu SSL hello do hosta.</span><span class="sxs-lookup"><span data-stu-id="49dad-151">Use hello endpoint and master key in from hello response in your client and import hello SSL certificate into your host.</span></span> <span data-ttu-id="49dad-152">Witaj tooimport certyfikat SSL hello poniższych z wiersza polecenia z uprawnieniami administratora:</span><span class="sxs-lookup"><span data-stu-id="49dad-152">tooimport hello SSL certificate, do hello following from an admin command prompt:</span></span>

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-hello-emulator"></a><span data-ttu-id="49dad-153">Uruchom hello emulatora</span><span class="sxs-lookup"><span data-stu-id="49dad-153">Start hello Emulator</span></span>

<span data-ttu-id="49dad-154">toostart hello Azure rozwiązania Cosmos DB emulatora, kliknij przycisk Start hello lub naciśnij klawisz systemu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="49dad-154">toostart hello Azure Cosmos DB Emulator, select hello Start button or press hello Windows key.</span></span> <span data-ttu-id="49dad-155">Rozpocznij wpisywanie **Azure rozwiązania Cosmos DB emulatora**i emulatora hello wybierz z listy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="49dad-155">Begin typing **Azure Cosmos DB Emulator**, and select hello emulator from hello list of applications.</span></span> 

![Wybierz hello Start przycisk lub naciśnij przycisk hello klawisz systemu Windows, rozpocznij wpisywanie ** Azure rozwiązania Cosmos DB emulatora ** i emulatora hello wybierz z listy aplikacji hello](./media/local-emulator/database-local-emulator-start.png)

<span data-ttu-id="49dad-157">Po uruchomieniu emulatora hello będzie widoczna ikona w obszarze powiadomień paska zadań systemu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="49dad-157">When hello emulator is running, you'll see an icon in hello Windows taskbar notification area.</span></span> ![Azure DB rozwiązania Cosmos emulatora lokalnym obszarze powiadomień paska zadań](./media/local-emulator/database-local-emulator-taskbar.png)

<span data-ttu-id="49dad-159">Hello Azure rozwiązania Cosmos DB emulatora domyślnie działa na komputerze lokalnym hello ("localhost") nasłuchuje na porcie 8081.</span><span class="sxs-lookup"><span data-stu-id="49dad-159">hello Azure Cosmos DB Emulator by default runs on hello local machine ("localhost") listening on port 8081.</span></span>

<span data-ttu-id="49dad-160">Hello Azure rozwiązania Cosmos DB emulatora jest instalowany przez domyślny toohello `C:\Program Files\Azure Cosmos DB Emulator` katalogu.</span><span class="sxs-lookup"><span data-stu-id="49dad-160">hello Azure Cosmos DB Emulator is installed by default toohello `C:\Program Files\Azure Cosmos DB Emulator` directory.</span></span> <span data-ttu-id="49dad-161">Można również uruchomić i zatrzymać emulatora hello z hello wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="49dad-161">You can also start and stop hello emulator from hello command-line.</span></span> <span data-ttu-id="49dad-162">Zobacz [odwołanie do narzędzia wiersza polecenia](#command-line) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="49dad-162">See [command-line tool reference](#command-line) for more information.</span></span>

## <a name="start-data-explorer"></a><span data-ttu-id="49dad-163">Uruchom Eksploratora danych</span><span class="sxs-lookup"><span data-stu-id="49dad-163">Start Data Explorer</span></span>

<span data-ttu-id="49dad-164">Po uruchomieniu emulatora bazy danych Azure rozwiązania Cosmos hello w przeglądarce zostanie otwarty automatycznie hello Eksploratora danych DB rozwiązania Cosmos Azure.</span><span class="sxs-lookup"><span data-stu-id="49dad-164">When hello Azure Cosmos DB emulator launches it will automatically open hello Azure Cosmos DB Data Explorer in your browser.</span></span> <span data-ttu-id="49dad-165">Witaj adres będzie wyświetlany jako [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span><span class="sxs-lookup"><span data-stu-id="49dad-165">hello address will appear as [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span></span> <span data-ttu-id="49dad-166">Jeśli są Zamknij Eksploratora hello i chcesz toore otwórz go później, możesz otworzyć hello adresu URL w przeglądarce lub uruchomić go z hello Azure rozwiązania Cosmos DB emulatora w hello ikona na pasku zadań systemu Windows, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="49dad-166">If you close hello explorer and would like toore-open it later, you can either open hello URL in your browser or launch it from hello Azure Cosmos DB Emulator in hello Windows Tray Icon as shown below.</span></span>

![Azure uruchamiania Eksploratora danych lokalnych emulatora DB rozwiązania Cosmos](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a><span data-ttu-id="49dad-168">Sprawdzanie dostępności aktualizacji</span><span class="sxs-lookup"><span data-stu-id="49dad-168">Checking for updates</span></span>
<span data-ttu-id="49dad-169">Eksplorator danych wskazuje, czy jest nowe aktualizacje dostępne do pobrania.</span><span class="sxs-lookup"><span data-stu-id="49dad-169">Data Explorer indicates if there is a new update available for download.</span></span> 

> [!NOTE]
> <span data-ttu-id="49dad-170">Dane utworzone w jednej wersji hello Azure rozwiązania Cosmos DB emulatora nie jest gwarantowana toobe dostępny przy użyciu innej wersji.</span><span class="sxs-lookup"><span data-stu-id="49dad-170">Data created in one version of hello Azure Cosmos DB Emulator is not guaranteed toobe accessible when using a different version.</span></span> <span data-ttu-id="49dad-171">Jeśli potrzebujesz toopersist danych dla długoterminowej hello, zaleca się przechowywania tych danych w ramach konta bazy danych Azure rozwiązania Cosmos, a nie w hello Azure rozwiązania Cosmos DB emulatora.</span><span class="sxs-lookup"><span data-stu-id="49dad-171">If you need toopersist your data for hello long term, it is recommended that you store that data in an Azure Cosmos DB account, rather than in hello Azure Cosmos DB Emulator.</span></span> 

## <a name="authenticating-requests"></a><span data-ttu-id="49dad-172">Uwierzytelniania żądania</span><span class="sxs-lookup"><span data-stu-id="49dad-172">Authenticating requests</span></span>
<span data-ttu-id="49dad-173">Podobnie jak Azure DB rozwiązania Cosmos w chmurze hello każde żądanie, wprowadzone przed hello Azure rozwiązania Cosmos DB emulatora musi zostać uwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="49dad-173">Just as with Azure Cosmos DB in hello cloud, every request that you make against hello Azure Cosmos DB Emulator must be authenticated.</span></span> <span data-ttu-id="49dad-174">Hello Azure rozwiązania Cosmos DB emulatora obsługuje jednego stałego konta i klucz uwierzytelniania dobrze znanego uwierzytelniania klucza głównego.</span><span class="sxs-lookup"><span data-stu-id="49dad-174">hello Azure Cosmos DB Emulator supports a single fixed account and a well-known authentication key for master key authentication.</span></span> <span data-ttu-id="49dad-175">Tego konta i klucz są hello poświadczenia tylko do użytku z hello Azure rozwiązania Cosmos DB emulatora.</span><span class="sxs-lookup"><span data-stu-id="49dad-175">This account and key are hello only credentials permitted for use with hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="49dad-176">Są to:</span><span class="sxs-lookup"><span data-stu-id="49dad-176">They are:</span></span>

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> <span data-ttu-id="49dad-177">obsługiwane przez hello Azure rozwiązania Cosmos DB emulatora klucza głównego Hello jest przeznaczony do użytku z emulatora hello.</span><span class="sxs-lookup"><span data-stu-id="49dad-177">hello master key supported by hello Azure Cosmos DB Emulator is intended for use only with hello emulator.</span></span> <span data-ttu-id="49dad-178">Nie można używać swojego konta bazy danych Azure rozwiązania Cosmos produkcyjnych i klucz hello Azure rozwiązania Cosmos DB emulatora.</span><span class="sxs-lookup"><span data-stu-id="49dad-178">You cannot use your production Azure Cosmos DB account and key with hello Azure Cosmos DB Emulator.</span></span> 

> [!NOTE] 
> <span data-ttu-id="49dad-179">Jeśli hello emulator została uruchomiona z hello opcja następujący/key, użyj hello wygenerowany klucz zamiast "obiektów relacyjnych C2y6yDjf5 + ob0N8A7Cgv30VRDJIWEHLM 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw =="</span><span class="sxs-lookup"><span data-stu-id="49dad-179">If you have started hello emulator with hello /Key option, then use hello generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="49dad-180">Ponadto, podobnie jak hello Azure DB rozwiązania Cosmos usługi, hello Azure rozwiązania Cosmos DB emulatora obsługuje tylko bezpiecznej komunikacji za pośrednictwem protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="49dad-180">Additionally, just as hello Azure Cosmos DB service, hello Azure Cosmos DB Emulator supports only secure communication via SSL.</span></span>

## <a name="running-hello-emulator-on-a-local-network"></a><span data-ttu-id="49dad-181">Uruchomiony hello emulator w sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="49dad-181">Running hello emulator on a local network</span></span>

<span data-ttu-id="49dad-182">Można uruchomić emulatora hello w sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="49dad-182">You can run hello emulator on a local network.</span></span> <span data-ttu-id="49dad-183">tooenable dostępu do sieci, należy określić opcję /AllowNetworkAccess hello na powitania [wiersza polecenia](#command-line-syntax), które również wymaga określenia następujący/key = key_string lub/KeyFile = nazwa_pliku.</span><span class="sxs-lookup"><span data-stu-id="49dad-183">tooenable network access, specify hello /AllowNetworkAccess option at hello [command line](#command-line-syntax), which also requires that you specify /Key=key_string or /KeyFile=file_name.</span></span> <span data-ttu-id="49dad-184">Można użyć /GenKeyFile = toogenerate nazwa_pliku pliku z wyprzedzeniem losowy klucz.</span><span class="sxs-lookup"><span data-stu-id="49dad-184">You can use /GenKeyFile=file_name toogenerate a file with a random key upfront.</span></span>  <span data-ttu-id="49dad-185">Następnie można przekazać tego zbyt/KeyFile = nazwa_pliku lub następujący/key = contents_of_file.</span><span class="sxs-lookup"><span data-stu-id="49dad-185">Then you can pass that too/KeyFile=file_name or /Key=contents_of_file.</span></span>

<span data-ttu-id="49dad-186">tooenable dostępu do sieci dla hello pierwszego czasu hello użytkownika powinien zamknięcia hello emulatora i Usuń katalog danych hello emulatora (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span><span class="sxs-lookup"><span data-stu-id="49dad-186">tooenable network access for hello first time hello user should shutdown hello emulator and delete hello emulator’s data directory (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span></span>

## <a name="developing-with-hello-emulator"></a><span data-ttu-id="49dad-187">Programowania z użyciem hello emulatora</span><span class="sxs-lookup"><span data-stu-id="49dad-187">Developing with hello Emulator</span></span>
<span data-ttu-id="49dad-188">Po ma hello Azure Emulator rozwiązania Cosmos DB uruchomiony na pulpicie, można użyć dowolnego obsługiwane [zestawu SDK usługi Azure rozwiązania Cosmos DB](documentdb-sdk-dotnet.md) lub hello [interfejsu API REST Azure rozwiązania Cosmos DB](/rest/api/documentdb/) toointeract z hello emulatora.</span><span class="sxs-lookup"><span data-stu-id="49dad-188">Once you have hello Azure Cosmos DB Emulator running on your desktop, you can use any supported [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) or hello [Azure Cosmos DB REST API](/rest/api/documentdb/) toointeract with hello Emulator.</span></span> <span data-ttu-id="49dad-189">Hello Azure rozwiązania Cosmos DB emulatora obejmuje również wbudowane Eksploratora danych, który umożliwia tworzenie kolekcji hello usługi DocumentDB, bazy danych MongoDB interfejsów API i widoku i edycji dokumentów bez pisania żadnego kodu.</span><span class="sxs-lookup"><span data-stu-id="49dad-189">hello Azure Cosmos DB Emulator also includes a built-in Data Explorer that lets you create collections for hello DocumentDB and MongoDB APIs, and view and edit documents without writing any code.</span></span>   

    // Connect toohello Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

<span data-ttu-id="49dad-190">Jeśli używasz [obsługą protokołu bazy danych Azure rozwiązania Cosmos bazy danych mongodb](mongodb-introduction.md), użyj hello następujące parametry połączenia:</span><span class="sxs-lookup"><span data-stu-id="49dad-190">If you're using [Azure Cosmos DB protocol support for MongoDB](mongodb-introduction.md), please use hello following connection string:</span></span>

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

<span data-ttu-id="49dad-191">Można użyć istniejących narzędzi, takich jak [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) toohello tooconnect emulatora DB rozwiązania Cosmos Azure.</span><span class="sxs-lookup"><span data-stu-id="49dad-191">You can use existing tools like [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="49dad-192">Można również migrację danych między hello Azure rozwiązania Cosmos DB emulatora i usługę Azure DB rozwiązania Cosmos hello za pomocą hello [narzędzia migracji danych DB rozwiązania Cosmos Azure](https://github.com/azure/azure-documentdb-datamigrationtool).</span><span class="sxs-lookup"><span data-stu-id="49dad-192">You can also migrate data between hello Azure Cosmos DB Emulator and hello Azure Cosmos DB service using hello [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).</span></span>

> [!NOTE] 
> <span data-ttu-id="49dad-193">Jeśli hello emulator została uruchomiona z hello opcja następujący/key, użyj hello wygenerowany klucz zamiast "obiektów relacyjnych C2y6yDjf5 + ob0N8A7Cgv30VRDJIWEHLM 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw =="</span><span class="sxs-lookup"><span data-stu-id="49dad-193">If you have started hello emulator with hello /Key option, then use hello generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="49dad-194">Przy użyciu emulatora usługi Azure DB rozwiązania Cosmos hello, domyślnie, można utworzyć kolekcje z jedną partycją too25 lub 1 kolekcji podzielone na partycje.</span><span class="sxs-lookup"><span data-stu-id="49dad-194">Using hello Azure Cosmos DB emulator, by default, you can create up too25 single partition collections or 1 partitioned collection.</span></span> <span data-ttu-id="49dad-195">Aby uzyskać więcej informacji na temat Zmiana tej wartości, zobacz [ustawienie wartości PartitionCount hello](#set-partitioncount).</span><span class="sxs-lookup"><span data-stu-id="49dad-195">For more information about changing this value, see [Setting hello PartitionCount value](#set-partitioncount).</span></span>

## <a name="export-hello-ssl-certificate"></a><span data-ttu-id="49dad-196">Wyeksportuj certyfikat SSL hello</span><span class="sxs-lookup"><span data-stu-id="49dad-196">Export hello SSL certificate</span></span>

<span data-ttu-id="49dad-197">Języków .NET i toosecurely magazynu certyfikatów systemu Windows hello Użyj środowiska wykonawczego łączą emulatora lokalnej bazy danych Azure rozwiązania Cosmos toohello.</span><span class="sxs-lookup"><span data-stu-id="49dad-197">.NET languages and runtime use hello Windows Certificate Store toosecurely connect toohello Azure Cosmos DB local emulator.</span></span> <span data-ttu-id="49dad-198">Inne języki ma swoje własne metody przy użyciu certyfikatów oraz zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="49dad-198">Other languages have their own method of managing and using certificates.</span></span> <span data-ttu-id="49dad-199">Java używa własnego [magazyn certyfikatów](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) natomiast używa języka Python [gniazda otoki](https://docs.python.org/2/library/ssl.html).</span><span class="sxs-lookup"><span data-stu-id="49dad-199">Java uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) whereas Python uses [socket wrappers](https://docs.python.org/2/library/ssl.html).</span></span>

<span data-ttu-id="49dad-200">W kolejności tooobtain toouse certyfikatu, języki i środowisk uruchomieniowych, który nie zintegrować z magazynu certyfikatów systemu Windows hello można będzie potrzebny tooexport przy użyciu Menedżera certyfikatów systemu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="49dad-200">In order tooobtain a certificate toouse with languages and runtimes that do not integrate with hello Windows Certificate Store you will need tooexport it using hello Windows Certificate Manager.</span></span> <span data-ttu-id="49dad-201">Można go uruchomić, uruchamiając certlm.msc lub wykonaj te instrukcje krok po kroku hello [wyeksportowanie hello Azure rozwiązania Cosmos DB emulatora certyfikatów](./local-emulator-export-ssl-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="49dad-201">You can start it by running certlm.msc or follow hello step by step instructions in [Export hello Azure Cosmos DB Emulator Certificates](./local-emulator-export-ssl-certificates.md).</span></span> <span data-ttu-id="49dad-202">Po uruchomieniu Menedżera certyfikatów hello certyfikaty osobiste Otwórz hello w sposób przedstawiony poniżej i eksportowanie hello certyfikat o przyjaznej nazwie hello "DocumentDBEmulatorCertificate", zgodnie z algorytmem BASE-64 pliku X.509 (.cer).</span><span class="sxs-lookup"><span data-stu-id="49dad-202">Once hello certificate manager is running, open hello Personal Certificates as shown below and export hello certificate with hello friendly name "DocumentDBEmulatorCertificate" as a BASE-64 encoded X.509 (.cer) file.</span></span>

![Azure certyfikat SSL lokalnym emulatorze DB rozwiązania Cosmos](./media/local-emulator/database-local-emulator-ssl_certificate.png)

<span data-ttu-id="49dad-204">Certyfikat X.509 Hello można zaimportować do magazynu certyfikatów Java hello wykonując instrukcje hello w [Dodawanie toohello certyfikatów, w magazynie certyfikatów urzędu certyfikacji Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span><span class="sxs-lookup"><span data-stu-id="49dad-204">hello X.509 certificate can be imported into hello Java certificate store by following hello instructions in [Adding a Certificate toohello Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span></span> <span data-ttu-id="49dad-205">Po hello certyfikat został zaimportowany do magazynu certyfikatów hello, aplikacji Java i bazy danych MongoDB będą mogli tooconnect toohello emulatora DB rozwiązania Cosmos Azure.</span><span class="sxs-lookup"><span data-stu-id="49dad-205">Once hello certificate is imported into hello certificate store, Java and MongoDB applications will be able tooconnect toohello Azure Cosmos DB Emulator.</span></span>

<span data-ttu-id="49dad-206">Podczas łączenia z emulatora toohello Python i Node.js SDK, weryfikacji SSL jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="49dad-206">When connecting toohello emulator from Python and Node.js SDKs, SSL verification is disabled.</span></span>

## <span data-ttu-id="49dad-207"><a id="command-line"></a>Odwołanie do narzędzia wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="49dad-207"><a id="command-line"></a>Command-line tool reference</span></span>
<span data-ttu-id="49dad-208">Z lokalizacji instalacji hello można użyć wiersza polecenia toostart hello i Zatrzymaj emulatora hello, skonfiguruj opcje, a także wykonywanie innych operacji.</span><span class="sxs-lookup"><span data-stu-id="49dad-208">From hello installation location, you can use hello command-line toostart and stop hello emulator, configure options, and perform other operations.</span></span>

### <a name="command-line-syntax"></a><span data-ttu-id="49dad-209">Składnia wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="49dad-209">Command-line Syntax</span></span>

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

<span data-ttu-id="49dad-210">tooview hello listę opcji, typ `CosmosDB.Emulator.exe /?` hello wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="49dad-210">tooview hello list of options, type `CosmosDB.Emulator.exe /?` at hello command prompt.</span></span>

<table>
<tr>
  <td><span data-ttu-id="49dad-211"><strong>Opcja</strong></span><span class="sxs-lookup"><span data-stu-id="49dad-211"><strong>Option</strong></span></span></td>
  <td><span data-ttu-id="49dad-212"><strong>Opis</strong></span><span class="sxs-lookup"><span data-stu-id="49dad-212"><strong>Description</strong></span></span></td>
  <td><span data-ttu-id="49dad-213"><strong>Polecenie</strong></span><span class="sxs-lookup"><span data-stu-id="49dad-213"><strong>Command</strong></span></span></td>
  <td><span data-ttu-id="49dad-214"><strong>Argumenty</strong></span><span class="sxs-lookup"><span data-stu-id="49dad-214"><strong>Arguments</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="49dad-215">[Brak argumentów]</span><span class="sxs-lookup"><span data-stu-id="49dad-215">[No arguments]</span></span></td>
  <td><span data-ttu-id="49dad-216">Uruchamiany hello Azure rozwiązania Cosmos DB emulatora z ustawieniami domyślnymi.</span><span class="sxs-lookup"><span data-stu-id="49dad-216">Starts up hello Azure Cosmos DB Emulator with default settings.</span></span></td>
  <td><span data-ttu-id="49dad-217">CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="49dad-217">CosmosDB.Emulator.exe</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="49dad-218">[Pomoc]</span><span class="sxs-lookup"><span data-stu-id="49dad-218">[Help]</span></span></td>
  <td><span data-ttu-id="49dad-219">Wyświetla hello listę obsługiwanych argumentów wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="49dad-219">Displays hello list of supported command-line arguments.</span></span></td>
  <td><span data-ttu-id="49dad-220">CosmosDB.Emulator.exe /?</span><span class="sxs-lookup"><span data-stu-id="49dad-220">CosmosDB.Emulator.exe /?</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="49dad-221">Zamknięcie</span><span class="sxs-lookup"><span data-stu-id="49dad-221">Shutdown</span></span></td>
  <td><span data-ttu-id="49dad-222">Zamyka hello Azure rozwiązania Cosmos DB emulatora.</span><span class="sxs-lookup"><span data-stu-id="49dad-222">Shuts down hello Azure Cosmos DB Emulator.</span></span></td>
  <td><span data-ttu-id="49dad-223">/ Shutdown CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="49dad-223">CosmosDB.Emulator.exe /Shutdown</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="49dad-224">Ścieżki danych</span><span class="sxs-lookup"><span data-stu-id="49dad-224">DataPath</span></span></td>
  <td><span data-ttu-id="49dad-225">Określa ścieżkę hello w toostore plików danych.</span><span class="sxs-lookup"><span data-stu-id="49dad-225">Specifies hello path in which toostore data files.</span></span> <span data-ttu-id="49dad-226">Domyślnie jest to % LocalAppdata%\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="49dad-226">Default is %LocalAppdata%\CosmosDBEmulator.</span></span></td>
  <td><span data-ttu-id="49dad-227">CosmosDB.Emulator.exe /DataPath =&lt;ścieżki danych&gt;</span><span class="sxs-lookup"><span data-stu-id="49dad-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span></span></td>
  <td><span data-ttu-id="49dad-228">&lt;ścieżki danych&gt;: dostępną ścieżkę</span><span class="sxs-lookup"><span data-stu-id="49dad-228">&lt;datapath&gt;: An accessible path</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="49dad-229">Port</span><span class="sxs-lookup"><span data-stu-id="49dad-229">Port</span></span></td>
  <td><span data-ttu-id="49dad-230">Określa toouse numer portu hello hello emulatora.</span><span class="sxs-lookup"><span data-stu-id="49dad-230">Specifies hello port number toouse for hello emulator.</span></span>  <span data-ttu-id="49dad-231">Domyślnie jest 8081.</span><span class="sxs-lookup"><span data-stu-id="49dad-231">Default is 8081.</span></span></td>
  <td><span data-ttu-id="49dad-232">/ CosmosDB.Emulator.exe port =&lt;portu&gt;</span><span class="sxs-lookup"><span data-stu-id="49dad-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span></span></td>
  <td><span data-ttu-id="49dad-233">&lt;port&gt;: numer pojedynczego portu</span><span class="sxs-lookup"><span data-stu-id="49dad-233">&lt;port&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="49dad-234">MongoPort</span><span class="sxs-lookup"><span data-stu-id="49dad-234">MongoPort</span></span></td>
  <td><span data-ttu-id="49dad-235">Określa hello toouse numer portu bazy danych MongoDB zgodności interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="49dad-235">Specifies hello port number toouse for MongoDB compatibility API.</span></span> <span data-ttu-id="49dad-236">Domyślnie jest 10255.</span><span class="sxs-lookup"><span data-stu-id="49dad-236">Default is 10255.</span></span></td>
  <td><span data-ttu-id="49dad-237">CosmosDB.Emulator.exe /MongoPort =&lt;mongoport&gt;</span><span class="sxs-lookup"><span data-stu-id="49dad-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span></span></td>
  <td><span data-ttu-id="49dad-238">&lt;mongoport&gt;: numer pojedynczego portu</span><span class="sxs-lookup"><span data-stu-id="49dad-238">&lt;mongoport&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="49dad-239">DirectPorts</span><span class="sxs-lookup"><span data-stu-id="49dad-239">DirectPorts</span></span></td>
  <td><span data-ttu-id="49dad-240">Określa toouse porty hello bezpośrednie połączenie z.</span><span class="sxs-lookup"><span data-stu-id="49dad-240">Specifies hello ports toouse for direct connectivity.</span></span> <span data-ttu-id="49dad-241">Wartości domyślne są 10251,10252,10253,10254.</span><span class="sxs-lookup"><span data-stu-id="49dad-241">Defaults are 10251,10252,10253,10254.</span></span></td>
  <td><span data-ttu-id="49dad-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span><span class="sxs-lookup"><span data-stu-id="49dad-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span></span></td>
  <td><span data-ttu-id="49dad-243">&lt;directports&gt;: rozdzielana przecinkami lista portów 4</span><span class="sxs-lookup"><span data-stu-id="49dad-243">&lt;directports&gt;: Comma-delimited list of 4 ports</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="49dad-244">Klucz</span><span class="sxs-lookup"><span data-stu-id="49dad-244">Key</span></span></td>
  <td><span data-ttu-id="49dad-245">Klucz autoryzacji hello emulatora.</span><span class="sxs-lookup"><span data-stu-id="49dad-245">Authorization key for hello emulator.</span></span> <span data-ttu-id="49dad-246">Klucz musi być hello kodowanie base-64 wektora 64 bajtów.</span><span class="sxs-lookup"><span data-stu-id="49dad-246">Key must be hello base-64 encoding of a 64-byte vector.</span></span></td>
  <td><span data-ttu-id="49dad-247">CosmosDB.Emulator.exe następujący/key:&lt;klucza&gt;</span><span class="sxs-lookup"><span data-stu-id="49dad-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span></span></td>
  <td><span data-ttu-id="49dad-248">&lt;klucz&gt;: klucz musi być hello wektora 64-bajtowych kodowanie base-64</span><span class="sxs-lookup"><span data-stu-id="49dad-248">&lt;key&gt;: Key must be hello base-64 encoding of a 64-byte vector</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="49dad-249">EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="49dad-249">EnableRateLimiting</span></span></td>
  <td><span data-ttu-id="49dad-250">Określa, że ta stawka żądania ograniczanie zachowanie jest włączona.</span><span class="sxs-lookup"><span data-stu-id="49dad-250">Specifies that request rate limiting behavior is enabled.</span></span></td>
  <td><span data-ttu-id="49dad-251">CosmosDB.Emulator.exe /EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="49dad-251">CosmosDB.Emulator.exe /EnableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="49dad-252">DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="49dad-252">DisableRateLimiting</span></span></td>
  <td><span data-ttu-id="49dad-253">Określa, że tej liczby żądań ograniczanie zachowania jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="49dad-253">Specifies that request rate limiting behavior is disabled.</span></span></td>
  <td><span data-ttu-id="49dad-254">CosmosDB.Emulator.exe /DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="49dad-254">CosmosDB.Emulator.exe /DisableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="49dad-255">NoUI</span><span class="sxs-lookup"><span data-stu-id="49dad-255">NoUI</span></span></td>
  <td><span data-ttu-id="49dad-256">Nie pokazuj emulatora hello interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="49dad-256">Do not show hello emulator user interface.</span></span></td>
  <td><span data-ttu-id="49dad-257">/ Noui CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="49dad-257">CosmosDB.Emulator.exe /NoUI</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="49dad-258">NoExplorer</span><span class="sxs-lookup"><span data-stu-id="49dad-258">NoExplorer</span></span></td>
  <td><span data-ttu-id="49dad-259">Nie pokazuj Eksploratora dokumentów przy uruchamianiu.</span><span class="sxs-lookup"><span data-stu-id="49dad-259">Don't show document explorer on startup.</span></span></td>
  <td><span data-ttu-id="49dad-260">CosmosDB.Emulator.exe /NoExplorer</span><span class="sxs-lookup"><span data-stu-id="49dad-260">CosmosDB.Emulator.exe /NoExplorer</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="49dad-261">Liczba partycji</span><span class="sxs-lookup"><span data-stu-id="49dad-261">PartitionCount</span></span></td>
  <td><span data-ttu-id="49dad-262">Określa maksymalną liczbę kolekcji partycjonowanych hello.</span><span class="sxs-lookup"><span data-stu-id="49dad-262">Specifies hello maximum number of partitioned collections.</span></span> <span data-ttu-id="49dad-263">Zobacz [zmiany hello liczby kolekcji](#set-partitioncount) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="49dad-263">See [Change hello number of collections](#set-partitioncount) for more information.</span></span></td>
  <td><span data-ttu-id="49dad-264">CosmosDB.Emulator.exe /PartitionCount =&lt;liczba partycji&gt;</span><span class="sxs-lookup"><span data-stu-id="49dad-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span></span></td>
  <td><span data-ttu-id="49dad-265">&lt;Liczba partycji&gt;: Maksymalna liczba dozwolonych kolekcje z jedną partycją.</span><span class="sxs-lookup"><span data-stu-id="49dad-265">&lt;partitioncount&gt;: Maximum number of allowed single partition collections.</span></span> <span data-ttu-id="49dad-266">Domyślna to 25.</span><span class="sxs-lookup"><span data-stu-id="49dad-266">Default is 25.</span></span> <span data-ttu-id="49dad-267">Maksymalna dozwolona wartość to 250.</span><span class="sxs-lookup"><span data-stu-id="49dad-267">Maximum allowed is 250.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="49dad-268">DefaultPartitionCount</span><span class="sxs-lookup"><span data-stu-id="49dad-268">DefaultPartitionCount</span></span></td>
  <td><span data-ttu-id="49dad-269">Określa hello domyślny numer partycji dla kolekcji partycjonowanych.</span><span class="sxs-lookup"><span data-stu-id="49dad-269">Specifies hello default number of partitions for a partitioned collection.</span></span></td>
  <td><span data-ttu-id="49dad-270">CosmosDB.Emulator.exe /DefaultPartitionCount =&lt;defaultpartitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="49dad-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span></span></td>
  <td><span data-ttu-id="49dad-271">&lt;defaultpartitioncount&gt; domyślna to 25.</span><span class="sxs-lookup"><span data-stu-id="49dad-271">&lt;defaultpartitioncount&gt; Default is 25.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="49dad-272">AllowNetworkAccess</span><span class="sxs-lookup"><span data-stu-id="49dad-272">AllowNetworkAccess</span></span></td>
  <td><span data-ttu-id="49dad-273">Umożliwia dostęp do emulatora toohello za pośrednictwem sieci.</span><span class="sxs-lookup"><span data-stu-id="49dad-273">Enables access toohello emulator over a network.</span></span> <span data-ttu-id="49dad-274">Należy także podać następujący/key =&lt;key_string&gt; lub/KeyFile =&lt;nazwa_pliku&gt; tooenable dostępu do sieci.</span><span class="sxs-lookup"><span data-stu-id="49dad-274">You must also pass /Key=&lt;key_string&gt; or /KeyFile=&lt;file_name&gt; tooenable network access.</span></span></td>
  <td><span data-ttu-id="49dad-275">CosmosDB.Emulator.exe AllowNetworkAccess następujący/key =&lt;key_string&gt;</span><span class="sxs-lookup"><span data-stu-id="49dad-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span></span><br><br><span data-ttu-id="49dad-276">lub</span><span class="sxs-lookup"><span data-stu-id="49dad-276">or</span></span><br><br><span data-ttu-id="49dad-277">/ KeyFile /AllowNetworkAccess CosmosDB.Emulator.exe =&lt;nazwa_pliku&gt;</span><span class="sxs-lookup"><span data-stu-id="49dad-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="49dad-278">NoFirewall</span><span class="sxs-lookup"><span data-stu-id="49dad-278">NoFirewall</span></span></td>
  <td><span data-ttu-id="49dad-279">Nie należy dostosować reguły zapory, gdy /AllowNetworkAccess jest używany.</span><span class="sxs-lookup"><span data-stu-id="49dad-279">Don't adjust firewall rules when /AllowNetworkAccess is used.</span></span></td>
  <td><span data-ttu-id="49dad-280">/ Nofirewall CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="49dad-280">CosmosDB.Emulator.exe /NoFirewall</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="49dad-281">GenKeyFile</span><span class="sxs-lookup"><span data-stu-id="49dad-281">GenKeyFile</span></span></td>
  <td><span data-ttu-id="49dad-282">Wygeneruj nowy klucz autoryzacji i Zapisz toohello określonego pliku.</span><span class="sxs-lookup"><span data-stu-id="49dad-282">Generate a new authorization key and save toohello specified file.</span></span> <span data-ttu-id="49dad-283">można użyć klucza Hello wygenerowane z opcji/KeyFile lub hello następujący/key.</span><span class="sxs-lookup"><span data-stu-id="49dad-283">hello generated key can be used with hello /Key or /KeyFile options.</span></span></td>
  <td><span data-ttu-id="49dad-284">CosmosDB.Emulator.exe /GenKeyFile =&lt;ścieżki pliku tookey&gt;</span><span class="sxs-lookup"><span data-stu-id="49dad-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;path tookey file&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="49dad-285">Spójność</span><span class="sxs-lookup"><span data-stu-id="49dad-285">Consistency</span></span></td>
  <td><span data-ttu-id="49dad-286">Ustaw poziom spójności domyślne hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="49dad-286">Set hello default consistency level for hello account.</span></span></td>
  <td><span data-ttu-id="49dad-287">CosmosDB.Emulator.exe /Consistency =&lt;spójności&gt;</span><span class="sxs-lookup"><span data-stu-id="49dad-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span></span></td>
  <td><span data-ttu-id="49dad-288">&lt;spójność&gt;: wartość musi być jedną z następujących hello [poziomy spójności](consistency-levels.md): sesja, silne, Eventual lub BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="49dad-288">&lt;consistency&gt;: Value must be one of hello following [consistency levels](consistency-levels.md): Session, Strong, Eventual, or BoundedStaleness.</span></span>  <span data-ttu-id="49dad-289">Wartość domyślna Hello jest sesja.</span><span class="sxs-lookup"><span data-stu-id="49dad-289">hello default value is Session.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="49dad-290">?</span><span class="sxs-lookup"><span data-stu-id="49dad-290">?</span></span></td>
  <td><span data-ttu-id="49dad-291">Pokaż komunikat pomocy hello.</span><span class="sxs-lookup"><span data-stu-id="49dad-291">Show hello help message.</span></span></td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-hello-azure-cosmos-db-emulator-and-azure-cosmos-db"></a><span data-ttu-id="49dad-292">Różnice między hello Azure rozwiązania Cosmos DB emulatora i bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="49dad-292">Differences between hello Azure Cosmos DB Emulator and Azure Cosmos DB</span></span> 
<span data-ttu-id="49dad-293">Ponieważ hello emulatora DB rozwiązania Cosmos Azure udostępnia środowisko emulowanej uruchomione na stacji roboczej developer lokalnego, istnieją pewne różnice w działaniu między hello emulatora i konto bazy danych Azure rozwiązania Cosmos w chmurze hello:</span><span class="sxs-lookup"><span data-stu-id="49dad-293">Because hello Azure Cosmos DB Emulator provides an emulated environment running on a local developer workstation, there are some differences in functionality between hello emulator and an Azure Cosmos DB account in hello cloud:</span></span>

* <span data-ttu-id="49dad-294">Hello Azure rozwiązania Cosmos DB emulatora obsługuje tylko jedno konto stałych i dobrze znane klucza głównego.</span><span class="sxs-lookup"><span data-stu-id="49dad-294">hello Azure Cosmos DB Emulator supports only a single fixed account and a well-known master key.</span></span>  <span data-ttu-id="49dad-295">Ponowne generowanie klucza nie jest możliwe w hello Azure rozwiązania Cosmos DB emulatora.</span><span class="sxs-lookup"><span data-stu-id="49dad-295">Key regeneration is not possible in hello Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="49dad-296">Hello Azure rozwiązania Cosmos DB emulatora nie jest skalowalna usługi i nie będzie obsługiwać dużą liczbę kolekcji.</span><span class="sxs-lookup"><span data-stu-id="49dad-296">hello Azure Cosmos DB Emulator is not a scalable service and will not support a large number of collections.</span></span>
* <span data-ttu-id="49dad-297">Hello Azure rozwiązania Cosmos DB emulatora nie symulować różne [poziomy spójności bazy danych Azure rozwiązania Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="49dad-297">hello Azure Cosmos DB Emulator does not simulate different [Azure Cosmos DB consistency levels](consistency-levels.md).</span></span>
* <span data-ttu-id="49dad-298">Hello Azure rozwiązania Cosmos DB emulatora nie zasymulować [replikacji w przypadku](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="49dad-298">hello Azure Cosmos DB Emulator does not simulate [multi-region replication](distribute-data-globally.md).</span></span>
* <span data-ttu-id="49dad-299">Hello Azure rozwiązania Cosmos DB emulatora nie obsługuje hello zastąpienia przydziału usługi, które są dostępne w usłudze Azure DB rozwiązania Cosmos hello (limity rozmiaru dokumentu, zwiększenie kolekcji partycjonowanych magazynu).</span><span class="sxs-lookup"><span data-stu-id="49dad-299">hello Azure Cosmos DB Emulator does not support hello service quota overrides that are available in hello Azure Cosmos DB service (e.g. document size limits, increased partitioned collection storage).</span></span>
* <span data-ttu-id="49dad-300">Jako kopię hello Azure rozwiązania Cosmos DB emulatora może nie być w górę toodate z hello najnowszych zmian w usłudze Azure DB rozwiązania Cosmos hello, użyj [planistę wydajności bazy danych Azure rozwiązania Cosmos](https://www.documentdb.com/capacityplanner) tooaccurately szacowania produkcji przepływności (RUs) wymagania dotyczące aplikacji.</span><span class="sxs-lookup"><span data-stu-id="49dad-300">As your copy of hello Azure Cosmos DB Emulator might not be up toodate with hello most recent changes with hello Azure Cosmos DB service, please [Azure Cosmos DB capacity planner](https://www.documentdb.com/capacityplanner) tooaccurately estimate production throughput (RUs) needs of your application.</span></span>

## <span data-ttu-id="49dad-301"><a id="set-partitioncount"></a>Zmień hello liczby kolekcji</span><span class="sxs-lookup"><span data-stu-id="49dad-301"><a id="set-partitioncount"></a>Change hello number of collections</span></span>

<span data-ttu-id="49dad-302">Domyślnie można utworzyć kolekcje z jedną partycją too25 lub 1 kolekcji podzielone na partycje przy użyciu hello Azure rozwiązania Cosmos DB emulatora.</span><span class="sxs-lookup"><span data-stu-id="49dad-302">By default, you can create up too25 single partition collections, or 1 partitioned collection using hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="49dad-303">Zmieniając hello **PartitionCount** wartości, możesz utworzyć kolekcje z jedną partycją too250 lub 10 kolekcji partycjonowanych lub dowolną kombinację hello dwa niezawierającą więcej niż 250 pojedynczej partycji (gdzie 1 na partycje Kolekcja = 25 Kolekcja jednej partycji).</span><span class="sxs-lookup"><span data-stu-id="49dad-303">By modifying hello **PartitionCount** value, you can create up too250 single partition collections or 10 partitioned collections, or any combination of hello two that does not exceed 250 single partitions (where 1 partitioned collection = 25 single partition collection).</span></span>

<span data-ttu-id="49dad-304">Jeśli toocreate kolekcji po hello bieżąca liczba partycji została przekroczona, emulatora hello zgłasza wyjątek ServiceUnavailable z następującą wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="49dad-304">If you attempt toocreate a collection after hello current partition count has been exceeded, hello emulator throws a ServiceUnavailable exception, with hello following message.</span></span>

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    toobring more and more capacity online, and encourage you tootry again. 
    Please do not hesitate tooemail docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

<span data-ttu-id="49dad-305">toohello dostępne kolekcje emulatora usługi Azure rozwiązania Cosmos bazy danych, liczba hello toochange hello następujące:</span><span class="sxs-lookup"><span data-stu-id="49dad-305">toochange hello number of collections available toohello Azure Cosmos DB Emulator, do hello following:</span></span>

1. <span data-ttu-id="49dad-306">Usunięcie wszystkich lokalnych danych Azure rozwiązania Cosmos DB emulatora klikając prawym przyciskiem myszy hello **Azure rozwiązania Cosmos DB emulatora** na powitania na pasku zadań, a następnie klikając ikonę **zresetować danych...** .</span><span class="sxs-lookup"><span data-stu-id="49dad-306">Delete all local Azure Cosmos DB Emulator data by right-clicking hello **Azure Cosmos DB Emulator** icon on hello system tray, and then clicking **Reset Data…**.</span></span>
2. <span data-ttu-id="49dad-307">Usunięcie wszystkich danych emulatora w tym folderze C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="49dad-307">Delete all emulator data in this folder C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span></span>
3. <span data-ttu-id="49dad-308">Zamknij wszystkie otwarte wystąpienia, klikając prawym przyciskiem myszy hello **Azure rozwiązania Cosmos DB emulatora** na powitania na pasku zadań, a następnie klikając ikonę **zakończenia**.</span><span class="sxs-lookup"><span data-stu-id="49dad-308">Exit all open instances by right-clicking hello **Azure Cosmos DB Emulator** icon on hello system tray, and then clicking **Exit**.</span></span> <span data-ttu-id="49dad-309">Może upłynąć kilka minut dla wszystkich wystąpień tooexit.</span><span class="sxs-lookup"><span data-stu-id="49dad-309">It may take a minute for all instances tooexit.</span></span>
4. <span data-ttu-id="49dad-310">Zainstaluj najnowszą wersję hello hello [Azure rozwiązania Cosmos DB emulatora](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="49dad-310">Install hello latest version of hello [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).</span></span>
5. <span data-ttu-id="49dad-311">Uruchamianie emulatora hello z hello PartitionCount flagi, ustawiając wartość < = 250.</span><span class="sxs-lookup"><span data-stu-id="49dad-311">Launch hello emulator with hello PartitionCount flag by setting a value <= 250.</span></span> <span data-ttu-id="49dad-312">Na przykład: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span><span class="sxs-lookup"><span data-stu-id="49dad-312">For example: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="49dad-313">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="49dad-313">Troubleshooting</span></span>

<span data-ttu-id="49dad-314">Użyj hello następujące porady toohelp Rozwiązywanie problemów związanych z emulatora bazy danych Azure rozwiązania Cosmos hello:</span><span class="sxs-lookup"><span data-stu-id="49dad-314">Use hello following tips toohelp troubleshoot issues you encounter with hello Azure Cosmos DB emulator:</span></span>

- <span data-ttu-id="49dad-315">Jeśli po zainstalowaniu nowej wersji hello emulatora występują błędy, upewnij się, że możesz zresetować danych.</span><span class="sxs-lookup"><span data-stu-id="49dad-315">If you installed a new version of hello Emulator and are experiencing errors, ensure you reset your data.</span></span> <span data-ttu-id="49dad-316">Dane można zresetować prawym przyciskiem myszy ikonę emulatora DB rozwiązania Cosmos Azure hello na powitania na pasku zadań, a następnie klikając polecenie resetowania danych...</span><span class="sxs-lookup"><span data-stu-id="49dad-316">You can reset your data by right-clicking hello Azure Cosmos DB Emulator icon on hello system tray, and then clicking Reset Data….</span></span> <span data-ttu-id="49dad-317">Jeśli to nie rozwiąże hello błędy, możesz odinstalować i ponowne zainstalowanie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="49dad-317">If that does not fix hello errors, you can uninstall and reinstall hello app.</span></span> <span data-ttu-id="49dad-318">Zobacz [odinstalować emulatora lokalne powitania](#uninstall) instrukcje.</span><span class="sxs-lookup"><span data-stu-id="49dad-318">See [Uninstall hello local emulator](#uninstall) for instructions.</span></span>

- <span data-ttu-id="49dad-319">Jeśli emulator usługi Azure DB rozwiązania Cosmos hello ulegnie awarii, zbieranie plików zrzutu z folderu c:\Users\user_name\AppData\Local\CrashDumps, kompresować i dołącz je tooan poczty e-mail zbyt[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="49dad-319">If hello Azure Cosmos DB emulator crashes, collect dump files from c:\Users\user_name\AppData\Local\CrashDumps folder, compress them, and attach them tooan email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="49dad-320">Jeśli występują awarie w CosmosDB.StartupEntryPoint.exe, uruchom następujące polecenie w wierszu polecenia administratora z hello:`lodctr /R`</span><span class="sxs-lookup"><span data-stu-id="49dad-320">If you experience crashes in CosmosDB.StartupEntryPoint.exe, run hello following command from an admin command prompt: `lodctr /R`</span></span> 

- <span data-ttu-id="49dad-321">Jeśli wystąpi problem z łącznością [zbierać pliki śledzenia](#trace-files)kompresować i dołącz je tooan poczty e-mail zbyt[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="49dad-321">If you encounter a connectivity issue, [collect trace files](#trace-files), compress them, and attach them tooan email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="49dad-322">Jeśli zostanie wyświetlony **Usługa niedostępna** komunikatów, hello emulatora może być niepowodzenie stos sieciowy hello tooinitialize.</span><span class="sxs-lookup"><span data-stu-id="49dad-322">If you receive a **Service Unavailable** message, hello emulator might be failing tooinitialize hello network stack.</span></span> <span data-ttu-id="49dad-323">Toosee wyboru Jeśli masz hello Pulse secure klienta lub Juniper sieci zainstalowanego klienta, zgodnie z ich sterowniki filtrów sieci może spowodować hello problem.</span><span class="sxs-lookup"><span data-stu-id="49dad-323">Check toosee if you have hello Pulse secure client or Juniper networks client installed, as their network filter drivers may cause hello problem.</span></span> <span data-ttu-id="49dad-324">Odinstalowywanie sterowników filtrów innej sieci zazwyczaj rozwiązuje problem hello.</span><span class="sxs-lookup"><span data-stu-id="49dad-324">Uninstalling third party network filter drivers typically fixes hello issue.</span></span>

### <span data-ttu-id="49dad-325"><a id="trace-files"></a>Zbierz pliki śledzenia</span><span class="sxs-lookup"><span data-stu-id="49dad-325"><a id="trace-files"></a>Collect trace files</span></span>

<span data-ttu-id="49dad-326">toocollect debugowanie ślady, uruchom następujące polecenia z wiersza polecenia z uprawnieniami administracyjnymi hello:</span><span class="sxs-lookup"><span data-stu-id="49dad-326">toocollect debugging traces, run hello following commands from an administrative command prompt:</span></span>

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. <span data-ttu-id="49dad-327">`CosmosDB.Emulator.exe /shutdown`.</span><span class="sxs-lookup"><span data-stu-id="49dad-327">`CosmosDB.Emulator.exe /shutdown`.</span></span> <span data-ttu-id="49dad-328">Obejrzyj hello systemu na pasku zadań toomake czy hello program został zamknięty, może upłynąć kilka minut.</span><span class="sxs-lookup"><span data-stu-id="49dad-328">Watch hello system tray toomake sure hello program has shut down, it may take a minute.</span></span> <span data-ttu-id="49dad-329">Można także po prostu kliknij **zakończenia** w interfejsie użytkownika emulatora bazy danych Azure rozwiązania Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="49dad-329">You can also just click **Exit** in hello Azure Cosmos DB emulator user interface.</span></span>
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. <span data-ttu-id="49dad-330">Odtwórz hello problem.</span><span class="sxs-lookup"><span data-stu-id="49dad-330">Reproduce hello problem.</span></span> <span data-ttu-id="49dad-331">Jeśli Eksplorator danych nie działa, wystarczy toowait dla tooopen przeglądarki hello kilka sekund toocatch hello błędu.</span><span class="sxs-lookup"><span data-stu-id="49dad-331">If Data Explorer is not working, you only need toowait for hello browser tooopen for a few seconds toocatch hello error.</span></span>
5. `CosmosDB.Emulator.exe /stoptraces`
6. <span data-ttu-id="49dad-332">Przejdź do zbyt`%ProgramFiles%\Azure Cosmos DB Emulator` i Znajdź hello docdbemulator_000001.etl pliku.</span><span class="sxs-lookup"><span data-stu-id="49dad-332">Navigate too`%ProgramFiles%\Azure Cosmos DB Emulator` and find hello docdbemulator_000001.etl file.</span></span>
7. <span data-ttu-id="49dad-333">Wyślij plik etl hello wraz z Opisz kroki zbyt[ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com) do debugowania.</span><span class="sxs-lookup"><span data-stu-id="49dad-333">Send hello .etl file along with repro steps too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) for debugging.</span></span>

### <span data-ttu-id="49dad-334"><a id="uninstall"></a>Odinstaluj hello emulatora lokalnego</span><span class="sxs-lookup"><span data-stu-id="49dad-334"><a id="uninstall"></a>Uninstall hello local Emulator</span></span>

1. <span data-ttu-id="49dad-335">Zamknij wszystkie otwarte wystąpienia hello lokalnym emulatorze prawym przyciskiem myszy ikonę emulatora DB rozwiązania Cosmos Azure hello na powitania na pasku zadań, a następnie klikając przycisk Zakończ.</span><span class="sxs-lookup"><span data-stu-id="49dad-335">Exit all open instances of hello local Emulator by right-clicking hello Azure Cosmos DB Emulator icon on hello system tray, and then clicking Exit.</span></span> <span data-ttu-id="49dad-336">Może upłynąć kilka minut dla wszystkich wystąpień tooexit.</span><span class="sxs-lookup"><span data-stu-id="49dad-336">It may take a minute for all instances tooexit.</span></span>
2. <span data-ttu-id="49dad-337">W polu wyszukiwania systemu Windows hello wpisz **aplikacje i funkcje** i kliknij na powitania **aplikacje i funkcje (ustawienia systemowe)** wynik.</span><span class="sxs-lookup"><span data-stu-id="49dad-337">In hello Windows search box, type **Apps & features** and click on hello **Apps & features (System settings)** result.</span></span>
3. <span data-ttu-id="49dad-338">W hello listę aplikacji, przewiń zbyt**Azure rozwiązania Cosmos DB emulatora**, zaznacz go, kliknij przycisk **Odinstaluj**, upewnij się i kliknij przycisk **Odinstaluj** ponownie.</span><span class="sxs-lookup"><span data-stu-id="49dad-338">In hello list of apps, scroll too**Azure Cosmos DB Emulator**, select it, click **Uninstall**, then confirm and click **Uninstall** again.</span></span>
4. <span data-ttu-id="49dad-339">Po odinstalowaniu aplikacji hello Przejdź tooC:\Users\<użytkownika > folderu hello \AppData\Local\CosmosDBEmulator i delete.</span><span class="sxs-lookup"><span data-stu-id="49dad-339">When hello app is uninstalled, navigate tooC:\Users\<user>\AppData\Local\CosmosDBEmulator and delete hello folder.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="49dad-340">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="49dad-340">Next steps</span></span>

<span data-ttu-id="49dad-341">W tym samouczku wykonaniu hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="49dad-341">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="49dad-342">Zainstalowane hello emulatora lokalnego</span><span class="sxs-lookup"><span data-stu-id="49dad-342">Installed hello local Emulator</span></span>
> * <span data-ttu-id="49dad-343">RAND hello Emulator na Docker dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="49dad-343">Rand hello Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="49dad-344">Uwierzytelnionego żądania.</span><span class="sxs-lookup"><span data-stu-id="49dad-344">Authenticated requests</span></span>
> * <span data-ttu-id="49dad-345">Używane hello Eksploratora danych w hello emulatora</span><span class="sxs-lookup"><span data-stu-id="49dad-345">Used hello Data Explorer in hello Emulator</span></span>
> * <span data-ttu-id="49dad-346">Wyeksportowane certyfikaty SSL</span><span class="sxs-lookup"><span data-stu-id="49dad-346">Exported SSL certificates</span></span>
> * <span data-ttu-id="49dad-347">Wywoływana z wiersza polecenia hello hello emulatora</span><span class="sxs-lookup"><span data-stu-id="49dad-347">Called hello Emulator from hello command line</span></span>
> * <span data-ttu-id="49dad-348">Pliki śledzenia zebranych</span><span class="sxs-lookup"><span data-stu-id="49dad-348">Collected trace files</span></span>

<span data-ttu-id="49dad-349">W tym samouczku kiedy znasz już jak toouse hello lokalnego Emulator wolnego rozwoju lokalnych.</span><span class="sxs-lookup"><span data-stu-id="49dad-349">In this tutorial, you've learned how toouse hello local Emulator for free local development.</span></span> <span data-ttu-id="49dad-350">Można teraz kontynuować toohello następny samouczek i Dowiedz się, jak certyfikaty SSL emulatora tooexport.</span><span class="sxs-lookup"><span data-stu-id="49dad-350">You can now proceed toohello next tutorial and learn how tooexport Emulator SSL certificates.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="49dad-351">Eksportowanie hello Azure rozwiązania Cosmos DB emulatora certyfikatów</span><span class="sxs-lookup"><span data-stu-id="49dad-351">Export hello Azure Cosmos DB Emulator certificates</span></span>](local-emulator-export-ssl-certificates.md)
