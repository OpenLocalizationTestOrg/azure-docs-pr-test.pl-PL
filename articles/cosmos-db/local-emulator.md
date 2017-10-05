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
# <a name="use-the-azure-cosmos-db-emulator-for-local-development-and-testing"></a><span data-ttu-id="5d23a-104">Użyj emulatora usługi Azure rozwiązania Cosmos bazy danych dla lokalnych projektowania i testowania</span><span class="sxs-lookup"><span data-stu-id="5d23a-104">Use the Azure Cosmos DB Emulator for local development and testing</span></span>

<table>
<tr>
  <td><span data-ttu-id="5d23a-105"><strong>Pliki binarne</strong></span><span class="sxs-lookup"><span data-stu-id="5d23a-105"><strong>Binaries</strong></span></span></td>
  <td>[<span data-ttu-id="5d23a-106">Pobieranie pliku MSI</span><span class="sxs-lookup"><span data-stu-id="5d23a-106">Download MSI</span></span>](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><span data-ttu-id="5d23a-107"><strong>Docker</strong></span><span class="sxs-lookup"><span data-stu-id="5d23a-107"><strong>Docker</strong></span></span></td>
  <td>[<span data-ttu-id="5d23a-108">Centrum docker</span><span class="sxs-lookup"><span data-stu-id="5d23a-108">Docker Hub</span></span>](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><span data-ttu-id="5d23a-109"><strong>Źródło docker</strong></span><span class="sxs-lookup"><span data-stu-id="5d23a-109"><strong>Docker source</strong></span></span></td>
  <td>[<span data-ttu-id="5d23a-110">Github</span><span class="sxs-lookup"><span data-stu-id="5d23a-110">Github</span></span>](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
<span data-ttu-id="5d23a-111">Emulator DB rozwiązania Cosmos Azure zapewnia środowisko lokalne, które emuluje usługę Azure DB rozwiązania Cosmos do celów programistycznych.</span><span class="sxs-lookup"><span data-stu-id="5d23a-111">The Azure Cosmos DB Emulator provides a local environment that emulates the Azure Cosmos DB service for development purposes.</span></span> <span data-ttu-id="5d23a-112">Przy użyciu emulatora usługi Azure DB rozwiązania Cosmos, mogą tworzyć i przetestować aplikację lokalnie, bez tworzenia subskrypcji platformy Azure lub ponoszenia kosztów.</span><span class="sxs-lookup"><span data-stu-id="5d23a-112">Using the Azure Cosmos DB Emulator, you can develop and test your application locally, without creating an Azure subscription or incurring any costs.</span></span> <span data-ttu-id="5d23a-113">Po zakończeniu jak aplikacja działa w emulatorze DB rozwiązania Cosmos Azure, możesz przełączyć się do korzystania z konta bazy danych Azure rozwiązania Cosmos w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5d23a-113">When you're satisfied with how your application is working in the Azure Cosmos DB Emulator, you can switch to using an Azure Cosmos DB account in the cloud.</span></span>

<span data-ttu-id="5d23a-114">W tym artykule opisano następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="5d23a-114">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="5d23a-115">Instalowanie w emulatorze</span><span class="sxs-lookup"><span data-stu-id="5d23a-115">Installing the Emulator</span></span>
> * <span data-ttu-id="5d23a-116">Uruchomiony Emulator na Docker dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="5d23a-116">Running the Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="5d23a-117">Uwierzytelniania żądania</span><span class="sxs-lookup"><span data-stu-id="5d23a-117">Authenticating requests</span></span>
> * <span data-ttu-id="5d23a-118">Za pomocą Eksploratora danych w emulatorze</span><span class="sxs-lookup"><span data-stu-id="5d23a-118">Using the Data Explorer in the Emulator</span></span>
> * <span data-ttu-id="5d23a-119">Eksportowanie certyfikatów SSL</span><span class="sxs-lookup"><span data-stu-id="5d23a-119">Exporting SSL certificates</span></span>
> * <span data-ttu-id="5d23a-120">Wywoływanie Emulator z wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="5d23a-120">Calling the Emulator from the command line</span></span>
> * <span data-ttu-id="5d23a-121">Zbieranie plików śledzenia</span><span class="sxs-lookup"><span data-stu-id="5d23a-121">Collecting trace files</span></span>

<span data-ttu-id="5d23a-122">Zalecamy rozpoczęcie pracy od obejrzenia poniższego klipu wideo, w którym Kirill Gavrylyuk pokazano, jak rozpocząć pracę z emulatora usługi Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5d23a-122">We recommend getting started by watching the following video, where Kirill Gavrylyuk shows how to get started with the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="5d23a-123">Należy pamiętać, że wideo odwołuje się do emulatora jako Emulator usługi DocumentDB, ale samo narzędzie została zmieniona od Tynkowanie wideo emulatora usługi Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5d23a-123">Note that the video refers to the emulator as the DocumentDB Emulator, but the tool itself has been renamed the Azure Cosmos DB Emulator since taping the video.</span></span> <span data-ttu-id="5d23a-124">Wszystkie informacje w wideo są nadal aktualne dla emulatora usługi Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5d23a-124">All information in the video is still accurate for the Azure Cosmos DB Emulator.</span></span> 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-the-emulator-works"></a><span data-ttu-id="5d23a-125">Jak działa Emulator</span><span class="sxs-lookup"><span data-stu-id="5d23a-125">How the Emulator works</span></span>
<span data-ttu-id="5d23a-126">Emulator DB rozwiązania Cosmos Azure udostępnia emulacji o wysokiej wierności, usługi Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5d23a-126">The Azure Cosmos DB Emulator provides a high-fidelity emulation of the Azure Cosmos DB service.</span></span> <span data-ttu-id="5d23a-127">Obsługuje ona identyczną funkcjonalność jako rozwiązania Cosmos bazy danych Azure, w tym obsługa tworzenia i badania dokumentów JSON, inicjowania obsługi administracyjnej i skalowanie kolekcje i wykonywania procedury składowane i wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="5d23a-127">It supports identical functionality as Azure Cosmos DB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers.</span></span> <span data-ttu-id="5d23a-128">Mogą tworzyć i testowanie aplikacji przy użyciu emulatora usługi Azure DB rozwiązania Cosmos i wdrożyć je na platformie Azure w skali globalnej przez tylko jednego Konfiguracja punktu końcowego połączenia dla bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5d23a-128">You can develop and test applications using the Azure Cosmos DB Emulator, and deploy them to Azure at global scale by just making a single configuration change to the connection endpoint for Azure Cosmos DB.</span></span>

<span data-ttu-id="5d23a-129">Podczas utworzyliśmy emulacji lokalnej o wysokiej wierności, rzeczywista usługi bazy danych Azure rozwiązania Cosmos implementacja emulatora usługi Azure DB rozwiązania Cosmos jest inne niż w przypadku usługi.</span><span class="sxs-lookup"><span data-stu-id="5d23a-129">While we created a high-fidelity local emulation of the actual Azure Cosmos DB service, the implementation of the Azure Cosmos DB Emulator is different than that of the service.</span></span> <span data-ttu-id="5d23a-130">Na przykład emulatora usługi Azure DB rozwiązania Cosmos używa standardowe składniki systemu operacyjnego, takie jak lokalnego systemu plików dla stanu trwałego i stosu protokołu HTTPS dla łączności.</span><span class="sxs-lookup"><span data-stu-id="5d23a-130">For example, the Azure Cosmos DB Emulator uses standard OS components such as the local file system for persistence, and HTTPS protocol stack for connectivity.</span></span> <span data-ttu-id="5d23a-131">Oznacza to, że niektóre funkcje, która zależy od infrastruktury platformy Azure, takich jak globalnej replikacji, jednocyfrowej milisekundy opóźnienia odczytuje i zapisuje i dostosowywalne poziomy spójności nie są dostępne za pośrednictwem emulatora usługi Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5d23a-131">This means that some functionality that relies on Azure infrastructure like global replication, single-digit millisecond latency for reads/writes, and tunable consistency levels are not available via the Azure Cosmos DB Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="5d23a-132">W tej chwili w emulatorze Eksploratora danych obsługuje tylko tworzenie kolekcji interfejsu API usługi DocumentDB i kolekcji bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="5d23a-132">At this time the Data Explorer in the emulator only supports the creation of DocumentDB API collections and MongoDB collections.</span></span> <span data-ttu-id="5d23a-133">Eksplorator danych w emulatorze nie obsługuje obecnie Tworzenie tabel i wykresów.</span><span class="sxs-lookup"><span data-stu-id="5d23a-133">The Data Explorer in the emulator does not currently support the creation of tables and graphs.</span></span> 

## <a name="system-requirements"></a><span data-ttu-id="5d23a-134">Wymagania systemowe</span><span class="sxs-lookup"><span data-stu-id="5d23a-134">System requirements</span></span>
<span data-ttu-id="5d23a-135">Emulator DB rozwiązania Cosmos Azure ma następujące wymagania dotyczące sprzętu i oprogramowania:</span><span class="sxs-lookup"><span data-stu-id="5d23a-135">The Azure Cosmos DB Emulator has the following hardware and software requirements:</span></span>

* <span data-ttu-id="5d23a-136">Wymagania dotyczące oprogramowania</span><span class="sxs-lookup"><span data-stu-id="5d23a-136">Software requirements</span></span>
  * <span data-ttu-id="5d23a-137">Windows Server 2012 R2, Windows Server 2016 lub Windows 10</span><span class="sxs-lookup"><span data-stu-id="5d23a-137">Windows Server 2012 R2, Windows Server 2016, or Windows 10</span></span>
*   <span data-ttu-id="5d23a-138">Minimalne wymagania sprzętowe</span><span class="sxs-lookup"><span data-stu-id="5d23a-138">Minimum Hardware requirements</span></span>
  * <span data-ttu-id="5d23a-139">2 GB PAMIĘCI RAM</span><span class="sxs-lookup"><span data-stu-id="5d23a-139">2 GB RAM</span></span>
  * <span data-ttu-id="5d23a-140">10 GB dostępnego miejsca na dysku</span><span class="sxs-lookup"><span data-stu-id="5d23a-140">10 GB available hard disk space</span></span>

## <a name="installation"></a><span data-ttu-id="5d23a-141">Instalacja</span><span class="sxs-lookup"><span data-stu-id="5d23a-141">Installation</span></span>
<span data-ttu-id="5d23a-142">Można pobrać i zainstalować Emulator usługi Azure rozwiązania Cosmos bazy danych z [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="5d23a-142">You can download and install the Azure Cosmos DB Emulator from the [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span></span> 

> [!NOTE]
> <span data-ttu-id="5d23a-143">Aby zainstalować, skonfigurować i uruchomić emulatora usługi Azure rozwiązania Cosmos bazy danych, musi mieć uprawnienia administratora na komputerze.</span><span class="sxs-lookup"><span data-stu-id="5d23a-143">To install, configure, and run the Azure Cosmos DB Emulator, you must have administrative privileges on the computer.</span></span>

## <a name="running-on-docker-for-windows"></a><span data-ttu-id="5d23a-144">Systemem Docker dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="5d23a-144">Running on Docker for Windows</span></span>

<span data-ttu-id="5d23a-145">Emulator DB rozwiązania Cosmos Azure może działać w Docker dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="5d23a-145">The Azure Cosmos DB Emulator can be run on Docker for Windows.</span></span> <span data-ttu-id="5d23a-146">Emulator nie działają w Docker dla Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="5d23a-146">The Emulator does not work on Docker for Oracle Linux.</span></span>

<span data-ttu-id="5d23a-147">Po utworzeniu [Docker dla systemu Windows](https://www.docker.com/docker-windows) zainstalowana, można umieścić obraz emulatora z Centrum Docker, uruchamiając następujące polecenie z ulubionych powłoki (cmd.exe, programu PowerShell, itp.).</span><span class="sxs-lookup"><span data-stu-id="5d23a-147">Once you have [Docker for Windows](https://www.docker.com/docker-windows) installed, you can pull the Emulator image from Docker Hub by running the following command from your favorite shell (cmd.exe, PowerShell, etc.).</span></span>

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
<span data-ttu-id="5d23a-148">Aby uruchomić obrazu, uruchom następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="5d23a-148">To start the image, run the following commands.</span></span>

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

<span data-ttu-id="5d23a-149">Odpowiedź jest podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="5d23a-149">The response looks similar to the following:</span></span>

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

<span data-ttu-id="5d23a-150">Zamykanie powłoki interakcyjne po Emulator uruchomiony spowoduje zamknięcie kontenera emulatora.</span><span class="sxs-lookup"><span data-stu-id="5d23a-150">Closing the interactive shell once the Emulator has been started will shutdown the Emulator’s container.</span></span>

<span data-ttu-id="5d23a-151">Przy użyciu punktu końcowego i klucz główny w z odpowiedzi na kliencie, a następnie zaimportowanie certyfikatu SSL do hosta.</span><span class="sxs-lookup"><span data-stu-id="5d23a-151">Use the endpoint and master key in from the response in your client and import the SSL certificate into your host.</span></span> <span data-ttu-id="5d23a-152">Aby zaimportować certyfikat protokołu SSL, wykonaj następujące polecenie w wierszu polecenia administratora:</span><span class="sxs-lookup"><span data-stu-id="5d23a-152">To import the SSL certificate, do the following from an admin command prompt:</span></span>

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-the-emulator"></a><span data-ttu-id="5d23a-153">Uruchom Emulator</span><span class="sxs-lookup"><span data-stu-id="5d23a-153">Start the Emulator</span></span>

<span data-ttu-id="5d23a-154">Aby uruchomić emulatora usługi Azure DB rozwiązania Cosmos, kliknij przycisk Start, lub naciśnij klawisz systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="5d23a-154">To start the Azure Cosmos DB Emulator, select the Start button or press the Windows key.</span></span> <span data-ttu-id="5d23a-155">Rozpocznij wpisywanie **Azure rozwiązania Cosmos DB emulatora**i wybierz z listy aplikacji emulator.</span><span class="sxs-lookup"><span data-stu-id="5d23a-155">Begin typing **Azure Cosmos DB Emulator**, and select the emulator from the list of applications.</span></span> 

![Kliknij przycisk Start lub naciśnij klawisz systemu Windows, rozpocznij wpisywanie ** Azure rozwiązania Cosmos DB emulatora **, a następnie wybierz z listy aplikacji jest to emulator](./media/local-emulator/database-local-emulator-start.png)

<span data-ttu-id="5d23a-157">Po uruchomieniu emulatora będzie widoczna ikona w obszarze powiadomień paska zadań systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="5d23a-157">When the emulator is running, you'll see an icon in the Windows taskbar notification area.</span></span> ![Azure DB rozwiązania Cosmos emulatora lokalnym obszarze powiadomień paska zadań](./media/local-emulator/database-local-emulator-taskbar.png)

<span data-ttu-id="5d23a-159">Emulator usługi Azure rozwiązania Cosmos DB domyślnie uruchamiane na komputerze lokalnym ("localhost") nasłuchuje na porcie 8081.</span><span class="sxs-lookup"><span data-stu-id="5d23a-159">The Azure Cosmos DB Emulator by default runs on the local machine ("localhost") listening on port 8081.</span></span>

<span data-ttu-id="5d23a-160">Emulatora usługi Azure DB rozwiązania Cosmos jest instalowana domyślnie `C:\Program Files\Azure Cosmos DB Emulator` katalogu.</span><span class="sxs-lookup"><span data-stu-id="5d23a-160">The Azure Cosmos DB Emulator is installed by default to the `C:\Program Files\Azure Cosmos DB Emulator` directory.</span></span> <span data-ttu-id="5d23a-161">Można również uruchomić i zatrzymać emulatora z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="5d23a-161">You can also start and stop the emulator from the command-line.</span></span> <span data-ttu-id="5d23a-162">Zobacz [odwołanie do narzędzia wiersza polecenia](#command-line) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="5d23a-162">See [command-line tool reference](#command-line) for more information.</span></span>

## <a name="start-data-explorer"></a><span data-ttu-id="5d23a-163">Uruchom Eksploratora danych</span><span class="sxs-lookup"><span data-stu-id="5d23a-163">Start Data Explorer</span></span>

<span data-ttu-id="5d23a-164">Po uruchomieniu emulatora bazy danych Azure rozwiązania Cosmos w przeglądarce zostanie otwarty automatycznie Eksploratora danych Azure rozwiązania Cosmos bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5d23a-164">When the Azure Cosmos DB emulator launches it will automatically open the Azure Cosmos DB Data Explorer in your browser.</span></span> <span data-ttu-id="5d23a-165">Adres będzie wyświetlany jako [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span><span class="sxs-lookup"><span data-stu-id="5d23a-165">The address will appear as [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span></span> <span data-ttu-id="5d23a-166">Zamknij Eksploratora, aby otworzyć go ponownie później możesz otworzyć adresu URL w przeglądarce lub uruchomić go z emulatora usługi Azure rozwiązania Cosmos bazy danych w ikonie na pasku zadań systemu Windows, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="5d23a-166">If you close the explorer and would like to re-open it later, you can either open the URL in your browser or launch it from the Azure Cosmos DB Emulator in the Windows Tray Icon as shown below.</span></span>

![Azure uruchamiania Eksploratora danych lokalnych emulatora DB rozwiązania Cosmos](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a><span data-ttu-id="5d23a-168">Sprawdzanie dostępności aktualizacji</span><span class="sxs-lookup"><span data-stu-id="5d23a-168">Checking for updates</span></span>
<span data-ttu-id="5d23a-169">Eksplorator danych wskazuje, czy jest nowe aktualizacje dostępne do pobrania.</span><span class="sxs-lookup"><span data-stu-id="5d23a-169">Data Explorer indicates if there is a new update available for download.</span></span> 

> [!NOTE]
> <span data-ttu-id="5d23a-170">Dane utworzone w jednej wersji emulatora usługi Azure rozwiązania Cosmos bazy danych nie jest gwarantowana była dostępna, gdy w innej wersji.</span><span class="sxs-lookup"><span data-stu-id="5d23a-170">Data created in one version of the Azure Cosmos DB Emulator is not guaranteed to be accessible when using a different version.</span></span> <span data-ttu-id="5d23a-171">Jeśli musisz utrwalić danych długoterminowym, zaleca się przechowywania tych danych w ramach konta bazy danych rozwiązania Cosmos Azure, a nie w emulatorze Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5d23a-171">If you need to persist your data for the long term, it is recommended that you store that data in an Azure Cosmos DB account, rather than in the Azure Cosmos DB Emulator.</span></span> 

## <a name="authenticating-requests"></a><span data-ttu-id="5d23a-172">Uwierzytelniania żądania</span><span class="sxs-lookup"><span data-stu-id="5d23a-172">Authenticating requests</span></span>
<span data-ttu-id="5d23a-173">Podobnie jak Azure DB rozwiązania Cosmos w chmurze, każde żądanie, wprowadzone przed emulatora usługi Azure DB rozwiązania Cosmos musi zostać uwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="5d23a-173">Just as with Azure Cosmos DB in the cloud, every request that you make against the Azure Cosmos DB Emulator must be authenticated.</span></span> <span data-ttu-id="5d23a-174">Emulator DB rozwiązania Cosmos Azure obsługuje jednego stałego konta i klucz uwierzytelniania dobrze znanego uwierzytelniania klucza głównego.</span><span class="sxs-lookup"><span data-stu-id="5d23a-174">The Azure Cosmos DB Emulator supports a single fixed account and a well-known authentication key for master key authentication.</span></span> <span data-ttu-id="5d23a-175">Tego konta i klucz są tylko poświadczenia do użycia z emulatora usługi Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5d23a-175">This account and key are the only credentials permitted for use with the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="5d23a-176">Są to:</span><span class="sxs-lookup"><span data-stu-id="5d23a-176">They are:</span></span>

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> <span data-ttu-id="5d23a-177">Klucz główny obsługiwane przez Emulator usługi Azure DB rozwiązania Cosmos jest przeznaczony do użytku z emulatora.</span><span class="sxs-lookup"><span data-stu-id="5d23a-177">The master key supported by the Azure Cosmos DB Emulator is intended for use only with the emulator.</span></span> <span data-ttu-id="5d23a-178">Nie można używać swojego konta bazy danych Azure rozwiązania Cosmos produkcyjnych i klucz emulatora usługi Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5d23a-178">You cannot use your production Azure Cosmos DB account and key with the Azure Cosmos DB Emulator.</span></span> 

> [!NOTE] 
> <span data-ttu-id="5d23a-179">Jeśli emulator została uruchomiona z opcją następujący/key, użyj wygenerowany klucz zamiast "obiektów relacyjnych C2y6yDjf5 + ob0N8A7Cgv30VRDJIWEHLM 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw =="</span><span class="sxs-lookup"><span data-stu-id="5d23a-179">If you have started the emulator with the /Key option, then use the generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="5d23a-180">Ponadto po prostu co w usłudze Azure DB rozwiązania Cosmos emulatora usługi Azure DB rozwiązania Cosmos obsługuje tylko bezpiecznej komunikacji za pośrednictwem protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="5d23a-180">Additionally, just as the Azure Cosmos DB service, the Azure Cosmos DB Emulator supports only secure communication via SSL.</span></span>

## <a name="running-the-emulator-on-a-local-network"></a><span data-ttu-id="5d23a-181">Uruchomiony emulator w sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="5d23a-181">Running the emulator on a local network</span></span>

<span data-ttu-id="5d23a-182">W sieci lokalnej, możesz uruchomić emulatora.</span><span class="sxs-lookup"><span data-stu-id="5d23a-182">You can run the emulator on a local network.</span></span> <span data-ttu-id="5d23a-183">Aby włączyć dostęp do sieci, należy określić opcję /AllowNetworkAccess w [wiersza polecenia](#command-line-syntax), które również wymaga określenia następujący/key = key_string lub/KeyFile = nazwa_pliku.</span><span class="sxs-lookup"><span data-stu-id="5d23a-183">To enable network access, specify the /AllowNetworkAccess option at the [command line](#command-line-syntax), which also requires that you specify /Key=key_string or /KeyFile=file_name.</span></span> <span data-ttu-id="5d23a-184">Można użyć /GenKeyFile = nazwa_pliku, aby wygenerować plik z wyprzedzeniem losowy klucz.</span><span class="sxs-lookup"><span data-stu-id="5d23a-184">You can use /GenKeyFile=file_name to generate a file with a random key upfront.</span></span>  <span data-ttu-id="5d23a-185">Następnie można przekazać, że/KeyFile = nazwa_pliku lub następujący/key = contents_of_file.</span><span class="sxs-lookup"><span data-stu-id="5d23a-185">Then you can pass that to /KeyFile=file_name or /Key=contents_of_file.</span></span>

<span data-ttu-id="5d23a-186">Aby włączyć dostęp do sieci po raz pierwszy użytkownik powinien zamknięcia emulatora i usunąć katalog danych emulatora (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span><span class="sxs-lookup"><span data-stu-id="5d23a-186">To enable network access for the first time the user should shutdown the emulator and delete the emulator’s data directory (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span></span>

## <a name="developing-with-the-emulator"></a><span data-ttu-id="5d23a-187">Tworzenie w emulatorze</span><span class="sxs-lookup"><span data-stu-id="5d23a-187">Developing with the Emulator</span></span>
<span data-ttu-id="5d23a-188">Po utworzeniu emulatora DB rozwiązania Cosmos Azure uruchomiony na pulpicie, można użyć dowolnego obsługiwane [zestawu SDK usługi Azure rozwiązania Cosmos DB](documentdb-sdk-dotnet.md) lub [interfejsu API REST Azure rozwiązania Cosmos DB](/rest/api/documentdb/) wchodzić w interakcje z emulatora.</span><span class="sxs-lookup"><span data-stu-id="5d23a-188">Once you have the Azure Cosmos DB Emulator running on your desktop, you can use any supported [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) or the [Azure Cosmos DB REST API](/rest/api/documentdb/) to interact with the Emulator.</span></span> <span data-ttu-id="5d23a-189">Emulator DB rozwiązania Cosmos Azure obejmuje również wbudowane Eksploratora danych, który umożliwia tworzenie kolekcji usługi DocumentDB, bazy danych MongoDB interfejsów API i widoku i edycji dokumentów bez pisania żadnego kodu.</span><span class="sxs-lookup"><span data-stu-id="5d23a-189">The Azure Cosmos DB Emulator also includes a built-in Data Explorer that lets you create collections for the DocumentDB and MongoDB APIs, and view and edit documents without writing any code.</span></span>   

    // Connect to the Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

<span data-ttu-id="5d23a-190">Jeśli używasz [obsługą protokołu bazy danych Azure rozwiązania Cosmos bazy danych mongodb](mongodb-introduction.md), użyj następujący ciąg połączenia:</span><span class="sxs-lookup"><span data-stu-id="5d23a-190">If you're using [Azure Cosmos DB protocol support for MongoDB](mongodb-introduction.md), please use the following connection string:</span></span>

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

<span data-ttu-id="5d23a-191">Można użyć istniejących narzędzi, takich jak [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) nawiązać emulatora usługi Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5d23a-191">You can use existing tools like [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) to connect to the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="5d23a-192">Można również migrację danych między emulatora DB rozwiązania Cosmos Azure i przy użyciu usługi Azure DB rozwiązania Cosmos [narzędzia migracji danych DB rozwiązania Cosmos Azure](https://github.com/azure/azure-documentdb-datamigrationtool).</span><span class="sxs-lookup"><span data-stu-id="5d23a-192">You can also migrate data between the Azure Cosmos DB Emulator and the Azure Cosmos DB service using the [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).</span></span>

> [!NOTE] 
> <span data-ttu-id="5d23a-193">Jeśli emulator została uruchomiona z opcją następujący/key, użyj wygenerowany klucz zamiast "obiektów relacyjnych C2y6yDjf5 + ob0N8A7Cgv30VRDJIWEHLM 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw =="</span><span class="sxs-lookup"><span data-stu-id="5d23a-193">If you have started the emulator with the /Key option, then use the generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="5d23a-194">Domyślnie przy użyciu emulatora usługi Azure DB rozwiązania Cosmos, można utworzyć maksymalnie 25 kolekcje z jedną partycją lub 1 kolekcji podzielone na partycje.</span><span class="sxs-lookup"><span data-stu-id="5d23a-194">Using the Azure Cosmos DB emulator, by default, you can create up to 25 single partition collections or 1 partitioned collection.</span></span> <span data-ttu-id="5d23a-195">Aby uzyskać więcej informacji na temat Zmiana tej wartości, zobacz [ustawienie wartości PartitionCount](#set-partitioncount).</span><span class="sxs-lookup"><span data-stu-id="5d23a-195">For more information about changing this value, see [Setting the PartitionCount value](#set-partitioncount).</span></span>

## <a name="export-the-ssl-certificate"></a><span data-ttu-id="5d23a-196">Wyeksportuj certyfikat protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="5d23a-196">Export the SSL certificate</span></span>

<span data-ttu-id="5d23a-197">Języków .NET i środowiska uruchomieniowego umożliwia bezpieczne łączenie z emulatora lokalnej bazy danych Azure rozwiązania Cosmos magazynu certyfikatów systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="5d23a-197">.NET languages and runtime use the Windows Certificate Store to securely connect to the Azure Cosmos DB local emulator.</span></span> <span data-ttu-id="5d23a-198">Inne języki ma swoje własne metody przy użyciu certyfikatów oraz zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="5d23a-198">Other languages have their own method of managing and using certificates.</span></span> <span data-ttu-id="5d23a-199">Java używa własnego [magazyn certyfikatów](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) natomiast używa języka Python [gniazda otoki](https://docs.python.org/2/library/ssl.html).</span><span class="sxs-lookup"><span data-stu-id="5d23a-199">Java uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) whereas Python uses [socket wrappers](https://docs.python.org/2/library/ssl.html).</span></span>

<span data-ttu-id="5d23a-200">Aby uzyskać certyfikat do użycia z języków i środowisk uruchomieniowych, który nie jest integrowana z magazynu certyfikatów systemu Windows należy wyeksportować go przy użyciu Menedżera certyfikatów systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="5d23a-200">In order to obtain a certificate to use with languages and runtimes that do not integrate with the Windows Certificate Store you will need to export it using the Windows Certificate Manager.</span></span> <span data-ttu-id="5d23a-201">Można go uruchomić, uruchamiając certlm.msc lub postępuj zgodnie z instrukcjami krok po kroku [wyeksportowanie certyfikatów emulatora DB rozwiązania Cosmos Azure](./local-emulator-export-ssl-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="5d23a-201">You can start it by running certlm.msc or follow the step by step instructions in [Export the Azure Cosmos DB Emulator Certificates](./local-emulator-export-ssl-certificates.md).</span></span> <span data-ttu-id="5d23a-202">Po uruchomieniu Menedżera certyfikatów, otwórz certyfikatów osobistych, jak pokazano poniżej i wyeksportować certyfikat o przyjaznej nazwie "DocumentDBEmulatorCertificate", zgodnie z algorytmem BASE-64 pliku X.509 (.cer).</span><span class="sxs-lookup"><span data-stu-id="5d23a-202">Once the certificate manager is running, open the Personal Certificates as shown below and export the certificate with the friendly name "DocumentDBEmulatorCertificate" as a BASE-64 encoded X.509 (.cer) file.</span></span>

![Azure certyfikat SSL lokalnym emulatorze DB rozwiązania Cosmos](./media/local-emulator/database-local-emulator-ssl_certificate.png)

<span data-ttu-id="5d23a-204">Certyfikat X.509 można zaimportować do magazynu certyfikatów Java zgodnie z instrukcjami w [Dodawanie certyfikatu do magazynu certyfikatów urzędu certyfikacji Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span><span class="sxs-lookup"><span data-stu-id="5d23a-204">The X.509 certificate can be imported into the Java certificate store by following the instructions in [Adding a Certificate to the Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span></span> <span data-ttu-id="5d23a-205">Po zaimportowaniu certyfikatu do magazynu certyfikatów aplikacji Java i bazy danych MongoDB będzie można nawiązać połączenia z emulatora usługi Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5d23a-205">Once the certificate is imported into the certificate store, Java and MongoDB applications will be able to connect to the Azure Cosmos DB Emulator.</span></span>

<span data-ttu-id="5d23a-206">Podczas łączenia z emulatora, Python i Node.js SDK, weryfikacji SSL jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="5d23a-206">When connecting to the emulator from Python and Node.js SDKs, SSL verification is disabled.</span></span>

## <span data-ttu-id="5d23a-207"><a id="command-line"></a>Odwołanie do narzędzia wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="5d23a-207"><a id="command-line"></a>Command-line tool reference</span></span>
<span data-ttu-id="5d23a-208">Z lokalizacji instalacji możesz użyć wiersza polecenia do uruchamiania i zatrzymywania emulator, skonfiguruj opcje i wykonywać inne operacje.</span><span class="sxs-lookup"><span data-stu-id="5d23a-208">From the installation location, you can use the command-line to start and stop the emulator, configure options, and perform other operations.</span></span>

### <a name="command-line-syntax"></a><span data-ttu-id="5d23a-209">Składnia wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="5d23a-209">Command-line Syntax</span></span>

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

<span data-ttu-id="5d23a-210">Aby wyświetlić listę opcji, należy wpisać `CosmosDB.Emulator.exe /?` w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="5d23a-210">To view the list of options, type `CosmosDB.Emulator.exe /?` at the command prompt.</span></span>

<table>
<tr>
  <td><span data-ttu-id="5d23a-211"><strong>Opcja</strong></span><span class="sxs-lookup"><span data-stu-id="5d23a-211"><strong>Option</strong></span></span></td>
  <td><span data-ttu-id="5d23a-212"><strong>Opis</strong></span><span class="sxs-lookup"><span data-stu-id="5d23a-212"><strong>Description</strong></span></span></td>
  <td><span data-ttu-id="5d23a-213"><strong>Polecenie</strong></span><span class="sxs-lookup"><span data-stu-id="5d23a-213"><strong>Command</strong></span></span></td>
  <td><span data-ttu-id="5d23a-214"><strong>Argumenty</strong></span><span class="sxs-lookup"><span data-stu-id="5d23a-214"><strong>Arguments</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5d23a-215">[Brak argumentów]</span><span class="sxs-lookup"><span data-stu-id="5d23a-215">[No arguments]</span></span></td>
  <td><span data-ttu-id="5d23a-216">Uruchamiania emulatora usługi Azure rozwiązania Cosmos bazy danych przy użyciu ustawień domyślnych.</span><span class="sxs-lookup"><span data-stu-id="5d23a-216">Starts up the Azure Cosmos DB Emulator with default settings.</span></span></td>
  <td><span data-ttu-id="5d23a-217">CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="5d23a-217">CosmosDB.Emulator.exe</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="5d23a-218">[Pomoc]</span><span class="sxs-lookup"><span data-stu-id="5d23a-218">[Help]</span></span></td>
  <td><span data-ttu-id="5d23a-219">Wyświetla listę obsługiwanych argumentów wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="5d23a-219">Displays the list of supported command-line arguments.</span></span></td>
  <td><span data-ttu-id="5d23a-220">CosmosDB.Emulator.exe /?</span><span class="sxs-lookup"><span data-stu-id="5d23a-220">CosmosDB.Emulator.exe /?</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="5d23a-221">Zamknięcie</span><span class="sxs-lookup"><span data-stu-id="5d23a-221">Shutdown</span></span></td>
  <td><span data-ttu-id="5d23a-222">Zamyka emulatora usługi Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5d23a-222">Shuts down the Azure Cosmos DB Emulator.</span></span></td>
  <td><span data-ttu-id="5d23a-223">/ Shutdown CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="5d23a-223">CosmosDB.Emulator.exe /Shutdown</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="5d23a-224">Ścieżki danych</span><span class="sxs-lookup"><span data-stu-id="5d23a-224">DataPath</span></span></td>
  <td><span data-ttu-id="5d23a-225">Określa ścieżkę, w której chcesz przechowywać pliki danych.</span><span class="sxs-lookup"><span data-stu-id="5d23a-225">Specifies the path in which to store data files.</span></span> <span data-ttu-id="5d23a-226">Domyślnie jest to % LocalAppdata%\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="5d23a-226">Default is %LocalAppdata%\CosmosDBEmulator.</span></span></td>
  <td><span data-ttu-id="5d23a-227">CosmosDB.Emulator.exe /DataPath =&lt;ścieżki danych&gt;</span><span class="sxs-lookup"><span data-stu-id="5d23a-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span></span></td>
  <td><span data-ttu-id="5d23a-228">&lt;ścieżki danych&gt;: dostępną ścieżkę</span><span class="sxs-lookup"><span data-stu-id="5d23a-228">&lt;datapath&gt;: An accessible path</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5d23a-229">Port</span><span class="sxs-lookup"><span data-stu-id="5d23a-229">Port</span></span></td>
  <td><span data-ttu-id="5d23a-230">Określa numer portu używany dla emulatora.</span><span class="sxs-lookup"><span data-stu-id="5d23a-230">Specifies the port number to use for the emulator.</span></span>  <span data-ttu-id="5d23a-231">Domyślnie jest 8081.</span><span class="sxs-lookup"><span data-stu-id="5d23a-231">Default is 8081.</span></span></td>
  <td><span data-ttu-id="5d23a-232">/ CosmosDB.Emulator.exe port =&lt;portu&gt;</span><span class="sxs-lookup"><span data-stu-id="5d23a-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span></span></td>
  <td><span data-ttu-id="5d23a-233">&lt;port&gt;: numer pojedynczego portu</span><span class="sxs-lookup"><span data-stu-id="5d23a-233">&lt;port&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5d23a-234">MongoPort</span><span class="sxs-lookup"><span data-stu-id="5d23a-234">MongoPort</span></span></td>
  <td><span data-ttu-id="5d23a-235">Określa numer portu na potrzeby zgodności bazy danych MongoDB interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="5d23a-235">Specifies the port number to use for MongoDB compatibility API.</span></span> <span data-ttu-id="5d23a-236">Domyślnie jest 10255.</span><span class="sxs-lookup"><span data-stu-id="5d23a-236">Default is 10255.</span></span></td>
  <td><span data-ttu-id="5d23a-237">CosmosDB.Emulator.exe /MongoPort =&lt;mongoport&gt;</span><span class="sxs-lookup"><span data-stu-id="5d23a-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span></span></td>
  <td><span data-ttu-id="5d23a-238">&lt;mongoport&gt;: numer pojedynczego portu</span><span class="sxs-lookup"><span data-stu-id="5d23a-238">&lt;mongoport&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5d23a-239">DirectPorts</span><span class="sxs-lookup"><span data-stu-id="5d23a-239">DirectPorts</span></span></td>
  <td><span data-ttu-id="5d23a-240">Określa portów na potrzeby połączeń bezpośrednich.</span><span class="sxs-lookup"><span data-stu-id="5d23a-240">Specifies the ports to use for direct connectivity.</span></span> <span data-ttu-id="5d23a-241">Wartości domyślne są 10251,10252,10253,10254.</span><span class="sxs-lookup"><span data-stu-id="5d23a-241">Defaults are 10251,10252,10253,10254.</span></span></td>
  <td><span data-ttu-id="5d23a-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span><span class="sxs-lookup"><span data-stu-id="5d23a-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span></span></td>
  <td><span data-ttu-id="5d23a-243">&lt;directports&gt;: rozdzielana przecinkami lista portów 4</span><span class="sxs-lookup"><span data-stu-id="5d23a-243">&lt;directports&gt;: Comma-delimited list of 4 ports</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5d23a-244">Klucz</span><span class="sxs-lookup"><span data-stu-id="5d23a-244">Key</span></span></td>
  <td><span data-ttu-id="5d23a-245">Klucz autoryzacji dla emulatora.</span><span class="sxs-lookup"><span data-stu-id="5d23a-245">Authorization key for the emulator.</span></span> <span data-ttu-id="5d23a-246">Klucz musi być kodowanie base-64 wektor 64 bajtów.</span><span class="sxs-lookup"><span data-stu-id="5d23a-246">Key must be the base-64 encoding of a 64-byte vector.</span></span></td>
  <td><span data-ttu-id="5d23a-247">CosmosDB.Emulator.exe następujący/key:&lt;klucza&gt;</span><span class="sxs-lookup"><span data-stu-id="5d23a-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span></span></td>
  <td><span data-ttu-id="5d23a-248">&lt;klucz&gt;: klucz musi być kodowanie base-64 wektor 64 bajtów</span><span class="sxs-lookup"><span data-stu-id="5d23a-248">&lt;key&gt;: Key must be the base-64 encoding of a 64-byte vector</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5d23a-249">EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="5d23a-249">EnableRateLimiting</span></span></td>
  <td><span data-ttu-id="5d23a-250">Określa, że ta stawka żądania ograniczanie zachowanie jest włączona.</span><span class="sxs-lookup"><span data-stu-id="5d23a-250">Specifies that request rate limiting behavior is enabled.</span></span></td>
  <td><span data-ttu-id="5d23a-251">CosmosDB.Emulator.exe /EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="5d23a-251">CosmosDB.Emulator.exe /EnableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="5d23a-252">DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="5d23a-252">DisableRateLimiting</span></span></td>
  <td><span data-ttu-id="5d23a-253">Określa, że tej liczby żądań ograniczanie zachowania jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="5d23a-253">Specifies that request rate limiting behavior is disabled.</span></span></td>
  <td><span data-ttu-id="5d23a-254">CosmosDB.Emulator.exe /DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="5d23a-254">CosmosDB.Emulator.exe /DisableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="5d23a-255">NoUI</span><span class="sxs-lookup"><span data-stu-id="5d23a-255">NoUI</span></span></td>
  <td><span data-ttu-id="5d23a-256">Nie pokazuj emulator interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5d23a-256">Do not show the emulator user interface.</span></span></td>
  <td><span data-ttu-id="5d23a-257">/ Noui CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="5d23a-257">CosmosDB.Emulator.exe /NoUI</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="5d23a-258">NoExplorer</span><span class="sxs-lookup"><span data-stu-id="5d23a-258">NoExplorer</span></span></td>
  <td><span data-ttu-id="5d23a-259">Nie pokazuj Eksploratora dokumentów przy uruchamianiu.</span><span class="sxs-lookup"><span data-stu-id="5d23a-259">Don't show document explorer on startup.</span></span></td>
  <td><span data-ttu-id="5d23a-260">CosmosDB.Emulator.exe /NoExplorer</span><span class="sxs-lookup"><span data-stu-id="5d23a-260">CosmosDB.Emulator.exe /NoExplorer</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="5d23a-261">Liczba partycji</span><span class="sxs-lookup"><span data-stu-id="5d23a-261">PartitionCount</span></span></td>
  <td><span data-ttu-id="5d23a-262">Określa maksymalną liczbę kolekcji partycjonowanych.</span><span class="sxs-lookup"><span data-stu-id="5d23a-262">Specifies the maximum number of partitioned collections.</span></span> <span data-ttu-id="5d23a-263">Zobacz [zmienić liczby kolekcji](#set-partitioncount) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="5d23a-263">See [Change the number of collections](#set-partitioncount) for more information.</span></span></td>
  <td><span data-ttu-id="5d23a-264">CosmosDB.Emulator.exe /PartitionCount =&lt;liczba partycji&gt;</span><span class="sxs-lookup"><span data-stu-id="5d23a-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span></span></td>
  <td><span data-ttu-id="5d23a-265">&lt;Liczba partycji&gt;: Maksymalna liczba dozwolonych kolekcje z jedną partycją.</span><span class="sxs-lookup"><span data-stu-id="5d23a-265">&lt;partitioncount&gt;: Maximum number of allowed single partition collections.</span></span> <span data-ttu-id="5d23a-266">Domyślna to 25.</span><span class="sxs-lookup"><span data-stu-id="5d23a-266">Default is 25.</span></span> <span data-ttu-id="5d23a-267">Maksymalna dozwolona wartość to 250.</span><span class="sxs-lookup"><span data-stu-id="5d23a-267">Maximum allowed is 250.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5d23a-268">DefaultPartitionCount</span><span class="sxs-lookup"><span data-stu-id="5d23a-268">DefaultPartitionCount</span></span></td>
  <td><span data-ttu-id="5d23a-269">Określa domyślny numer partycji dla kolekcji partycjonowanych.</span><span class="sxs-lookup"><span data-stu-id="5d23a-269">Specifies the default number of partitions for a partitioned collection.</span></span></td>
  <td><span data-ttu-id="5d23a-270">CosmosDB.Emulator.exe /DefaultPartitionCount =&lt;defaultpartitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="5d23a-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span></span></td>
  <td><span data-ttu-id="5d23a-271">&lt;defaultpartitioncount&gt; domyślna to 25.</span><span class="sxs-lookup"><span data-stu-id="5d23a-271">&lt;defaultpartitioncount&gt; Default is 25.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5d23a-272">AllowNetworkAccess</span><span class="sxs-lookup"><span data-stu-id="5d23a-272">AllowNetworkAccess</span></span></td>
  <td><span data-ttu-id="5d23a-273">Zapewnia dostęp do emulatora za pośrednictwem sieci.</span><span class="sxs-lookup"><span data-stu-id="5d23a-273">Enables access to the emulator over a network.</span></span> <span data-ttu-id="5d23a-274">Należy także podać następujący/key =&lt;key_string&gt; lub/KeyFile =&lt;nazwa_pliku&gt; umożliwiające dostęp do sieci.</span><span class="sxs-lookup"><span data-stu-id="5d23a-274">You must also pass /Key=&lt;key_string&gt; or /KeyFile=&lt;file_name&gt; to enable network access.</span></span></td>
  <td><span data-ttu-id="5d23a-275">CosmosDB.Emulator.exe AllowNetworkAccess następujący/key =&lt;key_string&gt;</span><span class="sxs-lookup"><span data-stu-id="5d23a-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span></span><br><br><span data-ttu-id="5d23a-276">lub</span><span class="sxs-lookup"><span data-stu-id="5d23a-276">or</span></span><br><br><span data-ttu-id="5d23a-277">/ KeyFile /AllowNetworkAccess CosmosDB.Emulator.exe =&lt;nazwa_pliku&gt;</span><span class="sxs-lookup"><span data-stu-id="5d23a-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="5d23a-278">NoFirewall</span><span class="sxs-lookup"><span data-stu-id="5d23a-278">NoFirewall</span></span></td>
  <td><span data-ttu-id="5d23a-279">Nie należy dostosować reguły zapory, gdy /AllowNetworkAccess jest używany.</span><span class="sxs-lookup"><span data-stu-id="5d23a-279">Don't adjust firewall rules when /AllowNetworkAccess is used.</span></span></td>
  <td><span data-ttu-id="5d23a-280">/ Nofirewall CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="5d23a-280">CosmosDB.Emulator.exe /NoFirewall</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="5d23a-281">GenKeyFile</span><span class="sxs-lookup"><span data-stu-id="5d23a-281">GenKeyFile</span></span></td>
  <td><span data-ttu-id="5d23a-282">Wygeneruj nowy klucz autoryzacji i Zapisz do określonego pliku.</span><span class="sxs-lookup"><span data-stu-id="5d23a-282">Generate a new authorization key and save to the specified file.</span></span> <span data-ttu-id="5d23a-283">Przy użyciu opcji następujący/key lub/KeyFile można użyć wygenerowanego klucza.</span><span class="sxs-lookup"><span data-stu-id="5d23a-283">The generated key can be used with the /Key or /KeyFile options.</span></span></td>
  <td><span data-ttu-id="5d23a-284">CosmosDB.Emulator.exe /GenKeyFile =&lt;ścieżka do pliku klucza&gt;</span><span class="sxs-lookup"><span data-stu-id="5d23a-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;path to key file&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="5d23a-285">Spójność</span><span class="sxs-lookup"><span data-stu-id="5d23a-285">Consistency</span></span></td>
  <td><span data-ttu-id="5d23a-286">Ustaw domyślny poziom spójności dla konta.</span><span class="sxs-lookup"><span data-stu-id="5d23a-286">Set the default consistency level for the account.</span></span></td>
  <td><span data-ttu-id="5d23a-287">CosmosDB.Emulator.exe /Consistency =&lt;spójności&gt;</span><span class="sxs-lookup"><span data-stu-id="5d23a-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span></span></td>
  <td><span data-ttu-id="5d23a-288">&lt;spójność&gt;: wartość musi być jedną z następujących [poziomy spójności](consistency-levels.md): sesja, silne, Eventual lub BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="5d23a-288">&lt;consistency&gt;: Value must be one of the following [consistency levels](consistency-levels.md): Session, Strong, Eventual, or BoundedStaleness.</span></span>  <span data-ttu-id="5d23a-289">Wartość domyślna to sesji.</span><span class="sxs-lookup"><span data-stu-id="5d23a-289">The default value is Session.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5d23a-290">?</span><span class="sxs-lookup"><span data-stu-id="5d23a-290">?</span></span></td>
  <td><span data-ttu-id="5d23a-291">Pokaż komunikat pomocy.</span><span class="sxs-lookup"><span data-stu-id="5d23a-291">Show the help message.</span></span></td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-the-azure-cosmos-db-emulator-and-azure-cosmos-db"></a><span data-ttu-id="5d23a-292">Różnice między emulatora usługi Azure rozwiązania Cosmos bazy danych i bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="5d23a-292">Differences between the Azure Cosmos DB Emulator and Azure Cosmos DB</span></span> 
<span data-ttu-id="5d23a-293">Ponieważ Emulator DB rozwiązania Cosmos Azure udostępnia środowisko emulowanej uruchomione na stacji roboczej developer lokalnego, istnieją pewne różnice w działaniu między emulatora i konto bazy danych Azure rozwiązania Cosmos w chmurze:</span><span class="sxs-lookup"><span data-stu-id="5d23a-293">Because the Azure Cosmos DB Emulator provides an emulated environment running on a local developer workstation, there are some differences in functionality between the emulator and an Azure Cosmos DB account in the cloud:</span></span>

* <span data-ttu-id="5d23a-294">Emulatora usługi Azure DB rozwiązania Cosmos obsługuje tylko jedno konto stałych i dobrze znane klucza głównego.</span><span class="sxs-lookup"><span data-stu-id="5d23a-294">The Azure Cosmos DB Emulator supports only a single fixed account and a well-known master key.</span></span>  <span data-ttu-id="5d23a-295">Ponowne generowanie klucza nie jest możliwe w emulatorze Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5d23a-295">Key regeneration is not possible in the Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="5d23a-296">Emulatora usługi Azure rozwiązania Cosmos bazy danych nie jest skalowalna usługi i nie będzie obsługiwać dużą liczbę kolekcji.</span><span class="sxs-lookup"><span data-stu-id="5d23a-296">The Azure Cosmos DB Emulator is not a scalable service and will not support a large number of collections.</span></span>
* <span data-ttu-id="5d23a-297">Emulatora usługi Azure DB rozwiązania Cosmos nie symulować różne [poziomy spójności bazy danych Azure rozwiązania Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="5d23a-297">The Azure Cosmos DB Emulator does not simulate different [Azure Cosmos DB consistency levels](consistency-levels.md).</span></span>
* <span data-ttu-id="5d23a-298">Emulator usługi Azure DB rozwiązania Cosmos nie zasymulować [replikacji w przypadku](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="5d23a-298">The Azure Cosmos DB Emulator does not simulate [multi-region replication](distribute-data-globally.md).</span></span>
* <span data-ttu-id="5d23a-299">Emulator DB rozwiązania Cosmos Azure nie obsługuje zastąpienia przydziału usługi, które są dostępne w usłudze Azure DB rozwiązania Cosmos (np. limity rozmiaru dokumentu, zwiększenie kolekcji partycjonowanych magazynu).</span><span class="sxs-lookup"><span data-stu-id="5d23a-299">The Azure Cosmos DB Emulator does not support the service quota overrides that are available in the Azure Cosmos DB service (e.g. document size limits, increased partitioned collection storage).</span></span>
* <span data-ttu-id="5d23a-300">Jako kopię emulatora usługi Azure DB rozwiązania Cosmos mogą nie być aktualne informacje o najnowszych zmian w usłudze Azure DB rozwiązania Cosmos, użyj [planistę wydajności bazy danych Azure rozwiązania Cosmos](https://www.documentdb.com/capacityplanner) Aby dokładnie oszacować produkcyjnym wymagania dotyczące przepływności (RUs) aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5d23a-300">As your copy of the Azure Cosmos DB Emulator might not be up to date with the most recent changes with the Azure Cosmos DB service, please [Azure Cosmos DB capacity planner](https://www.documentdb.com/capacityplanner) to accurately estimate production throughput (RUs) needs of your application.</span></span>

## <span data-ttu-id="5d23a-301"><a id="set-partitioncount"></a>Zmiana liczby kolekcji</span><span class="sxs-lookup"><span data-stu-id="5d23a-301"><a id="set-partitioncount"></a>Change the number of collections</span></span>

<span data-ttu-id="5d23a-302">Domyślnie można utworzyć maksymalnie 25 kolekcje z jedną partycją lub 1 kolekcji podzielone na partycje przy użyciu emulatora usługi Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5d23a-302">By default, you can create up to 25 single partition collections, or 1 partitioned collection using the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="5d23a-303">Zmieniając **PartitionCount** wartości, możesz utworzyć maksymalnie 250 kolekcje z jedną partycją lub 10 kolekcji partycjonowanych lub dowolną kombinację dwa niezawierającą więcej niż 250 jednej partycji (gdzie 1 na partycje kolekcji = 25 Kolekcja jednej partycji).</span><span class="sxs-lookup"><span data-stu-id="5d23a-303">By modifying the **PartitionCount** value, you can create up to 250 single partition collections or 10 partitioned collections, or any combination of the two that does not exceed 250 single partitions (where 1 partitioned collection = 25 single partition collection).</span></span>

<span data-ttu-id="5d23a-304">Jeśli próbujesz utworzyć kolekcję po bieżąca liczba partycji została przekroczona, emulator zgłasza wyjątek ServiceUnavailable, następujący komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="5d23a-304">If you attempt to create a collection after the current partition count has been exceeded, the emulator throws a ServiceUnavailable exception, with the following message.</span></span>

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    to bring more and more capacity online, and encourage you to try again. 
    Please do not hesitate to email docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

<span data-ttu-id="5d23a-305">Aby zmienić liczby kolekcji dostępne emulatora usługi Azure rozwiązania Cosmos bazy danych, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5d23a-305">To change the number of collections available to the Azure Cosmos DB Emulator, do the following:</span></span>

1. <span data-ttu-id="5d23a-306">Usunięcie wszystkich lokalnych danych Azure rozwiązania Cosmos DB emulatora klikając prawym przyciskiem myszy **Azure rozwiązania Cosmos DB emulatora** ikonę na pasku zadań, a następnie klikając **zresetować danych...** .</span><span class="sxs-lookup"><span data-stu-id="5d23a-306">Delete all local Azure Cosmos DB Emulator data by right-clicking the **Azure Cosmos DB Emulator** icon on the system tray, and then clicking **Reset Data…**.</span></span>
2. <span data-ttu-id="5d23a-307">Usunięcie wszystkich danych emulatora w tym folderze C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="5d23a-307">Delete all emulator data in this folder C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span></span>
3. <span data-ttu-id="5d23a-308">Zamknij wszystkie otwarte wystąpienia, klikając prawym przyciskiem myszy **Azure rozwiązania Cosmos DB emulatora** ikonę na pasku zadań, a następnie klikając **zakończenia**.</span><span class="sxs-lookup"><span data-stu-id="5d23a-308">Exit all open instances by right-clicking the **Azure Cosmos DB Emulator** icon on the system tray, and then clicking **Exit**.</span></span> <span data-ttu-id="5d23a-309">Może upłynąć kilka minut dla wszystkich wystąpień zakończyć.</span><span class="sxs-lookup"><span data-stu-id="5d23a-309">It may take a minute for all instances to exit.</span></span>
4. <span data-ttu-id="5d23a-310">Zainstaluj najnowszą wersję pakietu [Azure rozwiązania Cosmos DB emulatora](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="5d23a-310">Install the latest version of the [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).</span></span>
5. <span data-ttu-id="5d23a-311">Uruchom emulator z flagą PartitionCount przez ustawienie wartości < = 250.</span><span class="sxs-lookup"><span data-stu-id="5d23a-311">Launch the emulator with the PartitionCount flag by setting a value <= 250.</span></span> <span data-ttu-id="5d23a-312">Na przykład: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span><span class="sxs-lookup"><span data-stu-id="5d23a-312">For example: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5d23a-313">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="5d23a-313">Troubleshooting</span></span>

<span data-ttu-id="5d23a-314">Do rozwiązywania problemów związanych z emulatora bazy danych Azure rozwiązania Cosmos, należy użyć następujących wskazówek:</span><span class="sxs-lookup"><span data-stu-id="5d23a-314">Use the following tips to help troubleshoot issues you encounter with the Azure Cosmos DB emulator:</span></span>

- <span data-ttu-id="5d23a-315">Jeśli po zainstalowaniu nowej wersji emulatora występują błędy, upewnij się, że możesz zresetować danych.</span><span class="sxs-lookup"><span data-stu-id="5d23a-315">If you installed a new version of the Emulator and are experiencing errors, ensure you reset your data.</span></span> <span data-ttu-id="5d23a-316">Dane można zresetować prawym przyciskiem myszy ikonę emulatora DB rozwiązania Cosmos Azure na pasku zadań, a następnie klikając pozycję Zresetuj danych...</span><span class="sxs-lookup"><span data-stu-id="5d23a-316">You can reset your data by right-clicking the Azure Cosmos DB Emulator icon on the system tray, and then clicking Reset Data….</span></span> <span data-ttu-id="5d23a-317">Jeśli to nie rozwiąże błędy, możesz odinstalować i ponownie zainstalować aplikację.</span><span class="sxs-lookup"><span data-stu-id="5d23a-317">If that does not fix the errors, you can uninstall and reinstall the app.</span></span> <span data-ttu-id="5d23a-318">Zobacz [odinstalować lokalnym emulatorze](#uninstall) instrukcje.</span><span class="sxs-lookup"><span data-stu-id="5d23a-318">See [Uninstall the local emulator](#uninstall) for instructions.</span></span>

- <span data-ttu-id="5d23a-319">Jeśli emulator usługi Azure DB rozwiązania Cosmos ulegnie awarii, zbieranie plików zrzutu z folderu c:\Users\user_name\AppData\Local\CrashDumps kompresować i dołącz je do wiadomości e-mail do [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="5d23a-319">If the Azure Cosmos DB emulator crashes, collect dump files from c:\Users\user_name\AppData\Local\CrashDumps folder, compress them, and attach them to an email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="5d23a-320">Jeśli występują awarie w CosmosDB.StartupEntryPoint.exe, uruchom następujące polecenie z wiersza polecenia z uprawnieniami administratora:`lodctr /R`</span><span class="sxs-lookup"><span data-stu-id="5d23a-320">If you experience crashes in CosmosDB.StartupEntryPoint.exe, run the following command from an admin command prompt: `lodctr /R`</span></span> 

- <span data-ttu-id="5d23a-321">Jeśli wystąpi problem z łącznością [zbierać pliki śledzenia](#trace-files)kompresować i dołącz je do wiadomości e-mail do [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="5d23a-321">If you encounter a connectivity issue, [collect trace files](#trace-files), compress them, and attach them to an email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="5d23a-322">Jeśli zostanie wyświetlony **Usługa niedostępna** wiadomości, emulator może nie można zainicjować stos sieciowy.</span><span class="sxs-lookup"><span data-stu-id="5d23a-322">If you receive a **Service Unavailable** message, the emulator might be failing to initialize the network stack.</span></span> <span data-ttu-id="5d23a-323">Sprawdź, czy masz klienta bezpiecznym impulsu lub Juniper sieci zainstalowanego klienta, zgodnie z ich sterowniki filtrów sieci może spowodować problem.</span><span class="sxs-lookup"><span data-stu-id="5d23a-323">Check to see if you have the Pulse secure client or Juniper networks client installed, as their network filter drivers may cause the problem.</span></span> <span data-ttu-id="5d23a-324">Odinstalowywanie sterowników filtrów innej sieci zazwyczaj rozwiązuje problem.</span><span class="sxs-lookup"><span data-stu-id="5d23a-324">Uninstalling third party network filter drivers typically fixes the issue.</span></span>

### <span data-ttu-id="5d23a-325"><a id="trace-files"></a>Zbierz pliki śledzenia</span><span class="sxs-lookup"><span data-stu-id="5d23a-325"><a id="trace-files"></a>Collect trace files</span></span>

<span data-ttu-id="5d23a-326">Aby zbierać dane śledzenia debugowania, uruchom następujące polecenia z wiersza polecenia z uprawnieniami administracyjnymi:</span><span class="sxs-lookup"><span data-stu-id="5d23a-326">To collect debugging traces, run the following commands from an administrative command prompt:</span></span>

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. <span data-ttu-id="5d23a-327">`CosmosDB.Emulator.exe /shutdown`.</span><span class="sxs-lookup"><span data-stu-id="5d23a-327">`CosmosDB.Emulator.exe /shutdown`.</span></span> <span data-ttu-id="5d23a-328">Obejrzyj pasku zadań, aby upewnić się, że program został zamknięty, może upłynąć kilka minut.</span><span class="sxs-lookup"><span data-stu-id="5d23a-328">Watch the system tray to make sure the program has shut down, it may take a minute.</span></span> <span data-ttu-id="5d23a-329">Można także po prostu kliknij **zakończenia** w interfejsie użytkownika emulatora bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5d23a-329">You can also just click **Exit** in the Azure Cosmos DB emulator user interface.</span></span>
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. <span data-ttu-id="5d23a-330">Odtwórz problem.</span><span class="sxs-lookup"><span data-stu-id="5d23a-330">Reproduce the problem.</span></span> <span data-ttu-id="5d23a-331">Jeśli Eksplorator danych nie działa, wystarczy poczekać przeglądarkę, aby otworzyć catch błąd kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="5d23a-331">If Data Explorer is not working, you only need to wait for the browser to open for a few seconds to catch the error.</span></span>
5. `CosmosDB.Emulator.exe /stoptraces`
6. <span data-ttu-id="5d23a-332">Przejdź do `%ProgramFiles%\Azure Cosmos DB Emulator` i Znajdź plik docdbemulator_000001.etl.</span><span class="sxs-lookup"><span data-stu-id="5d23a-332">Navigate to `%ProgramFiles%\Azure Cosmos DB Emulator` and find the docdbemulator_000001.etl file.</span></span>
7. <span data-ttu-id="5d23a-333">Wyślij plik ETL oraz reprodukcja kroki umożliwiające [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com) do debugowania.</span><span class="sxs-lookup"><span data-stu-id="5d23a-333">Send the .etl file along with repro steps to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) for debugging.</span></span>

### <span data-ttu-id="5d23a-334"><a id="uninstall"></a>Odinstaluj lokalnym emulatorze</span><span class="sxs-lookup"><span data-stu-id="5d23a-334"><a id="uninstall"></a>Uninstall the local Emulator</span></span>

1. <span data-ttu-id="5d23a-335">Zamknij wszystkie otwarte wystąpienia lokalnego emulatora prawym przyciskiem myszy ikonę emulatora DB rozwiązania Cosmos Azure na pasku zadań, a następnie klikając przycisk Zakończ.</span><span class="sxs-lookup"><span data-stu-id="5d23a-335">Exit all open instances of the local Emulator by right-clicking the Azure Cosmos DB Emulator icon on the system tray, and then clicking Exit.</span></span> <span data-ttu-id="5d23a-336">Może upłynąć kilka minut dla wszystkich wystąpień zakończyć.</span><span class="sxs-lookup"><span data-stu-id="5d23a-336">It may take a minute for all instances to exit.</span></span>
2. <span data-ttu-id="5d23a-337">W polu wyszukiwania systemu Windows wpisz **aplikacje i funkcje** i wybierz polecenie **aplikacje i funkcje (ustawienia systemowe)** wynik.</span><span class="sxs-lookup"><span data-stu-id="5d23a-337">In the Windows search box, type **Apps & features** and click on the **Apps & features (System settings)** result.</span></span>
3. <span data-ttu-id="5d23a-338">Na liście aplikacji, przewiń do **Azure rozwiązania Cosmos DB emulatora**, zaznacz go, kliknij przycisk **Odinstaluj**, upewnij się i kliknij przycisk **Odinstaluj** ponownie.</span><span class="sxs-lookup"><span data-stu-id="5d23a-338">In the list of apps, scroll to **Azure Cosmos DB Emulator**, select it, click **Uninstall**, then confirm and click **Uninstall** again.</span></span>
4. <span data-ttu-id="5d23a-339">Gdy aplikacja zostanie odinstalowana, przejdź do C:\Users\<użytkownika > \AppData\Local\CosmosDBEmulator i usuwania folderu.</span><span class="sxs-lookup"><span data-stu-id="5d23a-339">When the app is uninstalled, navigate to C:\Users\<user>\AppData\Local\CosmosDBEmulator and delete the folder.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5d23a-340">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5d23a-340">Next steps</span></span>

<span data-ttu-id="5d23a-341">W tym samouczku wykonaniu następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="5d23a-341">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5d23a-342">Zainstalowane lokalne emulatora</span><span class="sxs-lookup"><span data-stu-id="5d23a-342">Installed the local Emulator</span></span>
> * <span data-ttu-id="5d23a-343">RAND Emulator na Docker dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="5d23a-343">Rand the Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="5d23a-344">Uwierzytelnionego żądania.</span><span class="sxs-lookup"><span data-stu-id="5d23a-344">Authenticated requests</span></span>
> * <span data-ttu-id="5d23a-345">Używane w emulatorze Eksploratora danych</span><span class="sxs-lookup"><span data-stu-id="5d23a-345">Used the Data Explorer in the Emulator</span></span>
> * <span data-ttu-id="5d23a-346">Wyeksportowane certyfikaty SSL</span><span class="sxs-lookup"><span data-stu-id="5d23a-346">Exported SSL certificates</span></span>
> * <span data-ttu-id="5d23a-347">Wywołuje się, Emulator z wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="5d23a-347">Called the Emulator from the command line</span></span>
> * <span data-ttu-id="5d23a-348">Pliki śledzenia zebranych</span><span class="sxs-lookup"><span data-stu-id="5d23a-348">Collected trace files</span></span>

<span data-ttu-id="5d23a-349">W tym samouczku kiedy znasz już sposób użycia lokalnego emulatora wolnego rozwoju lokalnych.</span><span class="sxs-lookup"><span data-stu-id="5d23a-349">In this tutorial, you've learned how to use the local Emulator for free local development.</span></span> <span data-ttu-id="5d23a-350">Możesz teraz przejść do następnego samouczek i informacje o sposobie eksportowania certyfikatów SSL emulatora.</span><span class="sxs-lookup"><span data-stu-id="5d23a-350">You can now proceed to the next tutorial and learn how to export Emulator SSL certificates.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="5d23a-351">Wyeksportowanie certyfikatów emulatora DB rozwiązania Cosmos Azure</span><span class="sxs-lookup"><span data-stu-id="5d23a-351">Export the Azure Cosmos DB Emulator certificates</span></span>](local-emulator-export-ssl-certificates.md)
