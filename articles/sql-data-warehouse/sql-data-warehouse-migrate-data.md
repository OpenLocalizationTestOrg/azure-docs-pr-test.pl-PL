---
title: "Migrowanie danych do usługi SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Wskazówki dotyczące migrowania danych Azure SQL Data Warehouse związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: d78f954a-f54c-4aa4-9040-919bc6414887
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/29/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: dbdf1696cd169aa7e5e23f116027a1170347f4ea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="migrate-your-data"></a><span data-ttu-id="77002-103">Migrowanie danych</span><span class="sxs-lookup"><span data-stu-id="77002-103">Migrate Your Data</span></span>
<span data-ttu-id="77002-104">Można przenieść dane z różnych źródeł do magazynu danych SQL przy użyciu różnych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="77002-104">Data can be moved from different sources into your SQL Data Warehouse with a variety tools.</span></span>  <span data-ttu-id="77002-105">Kopiuj ADF, SSIS i bcp wszystkie umożliwia osiągnięcie tego celu.</span><span class="sxs-lookup"><span data-stu-id="77002-105">ADF Copy, SSIS, and bcp can all be used to achieve this goal.</span></span> <span data-ttu-id="77002-106">Jako ilość danych zwiększa należy traktować o podziału na etapy procesu migracji danych.</span><span class="sxs-lookup"><span data-stu-id="77002-106">However, as the amount of data increases you should think about breaking down the data migration process into steps.</span></span> <span data-ttu-id="77002-107">Daje to możliwość optymalizacji każdy krok, wydajności i odporności zapewnić migrację danych smooth.</span><span class="sxs-lookup"><span data-stu-id="77002-107">This affords you the opportunity to optimize each step both for performance and for resilience to ensure a smooth data migration.</span></span>

<span data-ttu-id="77002-108">W tym artykule omówiono najpierw scenariusze migracji prostego kopiowania ADF SSIS i bcp.</span><span class="sxs-lookup"><span data-stu-id="77002-108">This article first discusses the simple migration scenarios of ADF Copy, SSIS, and bcp.</span></span> <span data-ttu-id="77002-109">Następnie wygląda bardziej szczegółowe w sposób mogą być optymalizowane migracji.</span><span class="sxs-lookup"><span data-stu-id="77002-109">It then look a little deeper into how the migration can be optimized.</span></span>

## <a name="azure-data-factory-adf-copy"></a><span data-ttu-id="77002-110">Azure kopiowania fabryki danych (ADF)</span><span class="sxs-lookup"><span data-stu-id="77002-110">Azure Data Factory (ADF) copy</span></span>
<span data-ttu-id="77002-111">[Kopiuj ADF] [ ADF Copy] jest częścią [fabryki danych Azure][Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="77002-111">[ADF Copy][ADF Copy] is part of [Azure Data Factory][Azure Data Factory].</span></span> <span data-ttu-id="77002-112">Kopiuj ADF służy do eksportowania danych do plików prostych znajdującej się w magazynie lokalnym do zdalnego plików prostych przechowywane w magazynie obiektów blob Azure lub bezpośrednio do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="77002-112">You can use ADF Copy to export your data to flat files residing on local storage, to remote flat files held in Azure blob storage or directly into SQL Data Warehouse.</span></span>

<span data-ttu-id="77002-113">Jeśli dane rozpoczyna się w płaskiej plików, a następnie należy najpierw przenieść do obiektu blob magazynu Azure przed zainicjowaniem obciążenia go do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="77002-113">If your data starts in flat files, then you will first need to transfer it to Azure storage blob before initiating a load it into SQL Data Warehouse.</span></span> <span data-ttu-id="77002-114">Gdy dane są przesyłane do magazynu obiektów blob platformy Azure mogą być używane [kopiowania ADF] [ ADF Copy] ponownie, aby wypchnąć dane do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="77002-114">Once the data is transferred into Azure blob storage you can choose to use [ADF Copy][ADF Copy] again to push the data into SQL Data Warehouse.</span></span>

<span data-ttu-id="77002-115">Program PolyBase zapewnia również opcję wysokiej wydajności dla ładowania danych.</span><span class="sxs-lookup"><span data-stu-id="77002-115">PolyBase also provides a high-performance option for loading the data.</span></span> <span data-ttu-id="77002-116">Która jednak oznaczają za pomocą dwóch narzędzi, zamiast jednego.</span><span class="sxs-lookup"><span data-stu-id="77002-116">However, that does mean using two tools instead of one.</span></span> <span data-ttu-id="77002-117">Jeśli należy uzyskać najlepszą wydajność, użyj programu PolyBase.</span><span class="sxs-lookup"><span data-stu-id="77002-117">If you need the best performance then use PolyBase.</span></span> <span data-ttu-id="77002-118">Jeśli chcesz, aby w środowisku jednego narzędzia (i danych nie jest bardzo dużej) ADF jest odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="77002-118">If you want a single tool experience (and the data is not massive) then ADF is your answer.</span></span>


> 
> 

<span data-ttu-id="77002-119">HEAD za pośrednictwem w następującym artykule o niektórych dużej [przykłady ADF][ADF samples].</span><span class="sxs-lookup"><span data-stu-id="77002-119">Head over to the following article for some great [ADF samples][ADF samples].</span></span>

## <a name="integration-services"></a><span data-ttu-id="77002-120">Usługi integracji</span><span class="sxs-lookup"><span data-stu-id="77002-120">Integration Services</span></span>
<span data-ttu-id="77002-121">Integration Services (SSIS) to wydajny i elastyczny wyodrębniania, przekształcania i ładowania (ETL) Narzędzie obsługującego złożone przepływy pracy, przekształcania danych i kilka opcji ładowania danych.</span><span class="sxs-lookup"><span data-stu-id="77002-121">Integration Services (SSIS) is a powerful and flexible Extract Transform and Load (ETL) tool that supports complex workflows, data transformation, and several data loading options.</span></span> <span data-ttu-id="77002-122">Umożliwia po prostu transferu danych do platformy Azure lub w ramach szerszych migracji SSIS.</span><span class="sxs-lookup"><span data-stu-id="77002-122">Use SSIS to simply transfer data to Azure or as part of a broader migration.</span></span>

> [!NOTE]
> <span data-ttu-id="77002-123">SSIS można wyeksportować UTF-8 bez znacznika kolejności bajtów w pliku.</span><span class="sxs-lookup"><span data-stu-id="77002-123">SSIS can export to UTF-8 without the byte order mark in the file.</span></span> <span data-ttu-id="77002-124">Aby skonfigurować to należy najpierw użyć składnika kolumny pochodnej można przekonwertować danych znakowych w przepływ danych do użycia strona kodowa 65001 UTF-8.</span><span class="sxs-lookup"><span data-stu-id="77002-124">To configure this you must first use the derived column component to convert the character data in the data flow to use the 65001 UTF-8 code page.</span></span> <span data-ttu-id="77002-125">Po konwersji kolumny zapisać danych do pliku prostego adapter miejsca docelowego, zapewniając, że 65001 została również wybrana jako strony kodowej w pliku.</span><span class="sxs-lookup"><span data-stu-id="77002-125">Once the columns have been converted, write the data to the flat file destination adapter ensuring that 65001 has also been selected as the code page for the file.</span></span>
> 
> 

<span data-ttu-id="77002-126">SSIS łączy do usługi SQL Data Warehouse tak samo, jak może zostać nawiązane połączenie z wdrożeniem programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="77002-126">SSIS connects to SQL Data Warehouse just as it would connect to a SQL Server deployment.</span></span> <span data-ttu-id="77002-127">Jednak połączenia należy używać Menedżera połączeń ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="77002-127">However, your connections will need to be using an ADO.NET connection manager.</span></span> <span data-ttu-id="77002-128">Możesz również należy zwrócić uwagę, aby skonfigurować "Użyj wstawiania zbiorczego dostępne" ustawienie, aby zmaksymalizować przepustowość.</span><span class="sxs-lookup"><span data-stu-id="77002-128">You should also take care to configure the "Use bulk insert when available" setting to maximize throughput.</span></span> <span data-ttu-id="77002-129">Zapoznaj się z [ADO.NET docelowy adapter] [ ADO.NET destination adapter] artykuł, aby dowiedzieć się więcej o tej właściwości</span><span class="sxs-lookup"><span data-stu-id="77002-129">Please refer to the [ADO.NET destination adapter][ADO.NET destination adapter] article to learn more about this property</span></span>

> [!NOTE]
> <span data-ttu-id="77002-130">Dołączanie do usługi Azure SQL Data Warehouse przy użyciu OLEDB nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="77002-130">Connecting to Azure SQL Data Warehouse by using OLEDB is not supported.</span></span>
> 
> 

<span data-ttu-id="77002-131">Ponadto istnieje możliwość, że pakiet może zakończyć się niepowodzeniem ze względu na problemy z ograniczania lub sieci.</span><span class="sxs-lookup"><span data-stu-id="77002-131">In addition, there is always the possibility that a package might fail due to throttling or network issues.</span></span> <span data-ttu-id="77002-132">Projekt pakietów, ich można wznawiać w punkcie awarii bez ponawianie pracy, który zakończył się przed awarią.</span><span class="sxs-lookup"><span data-stu-id="77002-132">Design packages so they can be resumed at the point of failure, without redoing work that completed before the failure.</span></span>

<span data-ttu-id="77002-133">Aby uzyskać więcej informacji, zapoznaj się [dokumentacji SSIS][SSIS documentation].</span><span class="sxs-lookup"><span data-stu-id="77002-133">For more information consult the [SSIS documentation][SSIS documentation].</span></span>

## <a name="bcp"></a><span data-ttu-id="77002-134">bcp</span><span class="sxs-lookup"><span data-stu-id="77002-134">bcp</span></span>
<span data-ttu-id="77002-135">Narzędzie bcp jest narzędziem wiersza polecenia, które jest przeznaczone do pliku prostego importowania i eksportowania danych.</span><span class="sxs-lookup"><span data-stu-id="77002-135">bcp is a command-line utility that is designed for flat file data import and export.</span></span> <span data-ttu-id="77002-136">Niektóre przekształcania może odbywać się podczas eksportowania danych.</span><span class="sxs-lookup"><span data-stu-id="77002-136">Some transformation can take place during data export.</span></span> <span data-ttu-id="77002-137">Do wykonywania prostych transformacji umożliwia zapytania wybierz i przekształcenia danych.</span><span class="sxs-lookup"><span data-stu-id="77002-137">To perform simple transformations use a query to select and transform the data.</span></span> <span data-ttu-id="77002-138">Po wyeksportowane, plików prostych może zostać załadowana bezpośrednio do docelowej bazy danych magazynu danych SQL.</span><span class="sxs-lookup"><span data-stu-id="77002-138">Once exported, the flat files can then be loaded directly into the target the SQL Data Warehouse database.</span></span>

> [!NOTE]
> <span data-ttu-id="77002-139">Często jest warto Hermetyzowanie transformacje używane podczas eksportowania danych w widoku w systemie źródłowym.</span><span class="sxs-lookup"><span data-stu-id="77002-139">It is often a good idea to encapsulate the transformations used during data export in a view on the source system.</span></span> <span data-ttu-id="77002-140">Dzięki temu logika jest zachowywana, a proces jest powtarzalne.</span><span class="sxs-lookup"><span data-stu-id="77002-140">This ensures that the logic is retained and the process is repeatable.</span></span>
> 
> 

<span data-ttu-id="77002-141">Zalety programu bcp są następujące:</span><span class="sxs-lookup"><span data-stu-id="77002-141">Advantages of bcp are:</span></span>

* <span data-ttu-id="77002-142">Prostota.</span><span class="sxs-lookup"><span data-stu-id="77002-142">Simplicity.</span></span> <span data-ttu-id="77002-143">Tworzenie i wykonywanie prostych są polecenia BCP</span><span class="sxs-lookup"><span data-stu-id="77002-143">bcp commands are simple to build and execute</span></span>
* <span data-ttu-id="77002-144">Proces ładowania jej ponownie uruchomić.</span><span class="sxs-lookup"><span data-stu-id="77002-144">Re-startable load process.</span></span> <span data-ttu-id="77002-145">Raz wyeksportowanego obciążenia mogą być wykonywane dowolną liczbę razy</span><span class="sxs-lookup"><span data-stu-id="77002-145">Once exported the load can be executed any number of times</span></span>

<span data-ttu-id="77002-146">Ograniczenia programu bcp są:</span><span class="sxs-lookup"><span data-stu-id="77002-146">Limitations of bcp are:</span></span>

* <span data-ttu-id="77002-147">Narzędzie bcp działa tylko tabelaryczne plików prostych.</span><span class="sxs-lookup"><span data-stu-id="77002-147">bcp works with tabulated flat files only.</span></span> <span data-ttu-id="77002-148">Nie działa z plikami, takie jak xml lub JSON</span><span class="sxs-lookup"><span data-stu-id="77002-148">It does not work with files such as xml or JSON</span></span>
* <span data-ttu-id="77002-149">Funkcje przekształcania danych są ograniczone do etapu eksportu tylko i są z natury</span><span class="sxs-lookup"><span data-stu-id="77002-149">Data transformation capabilities are limited to the export stage only and are simple in nature</span></span>
* <span data-ttu-id="77002-150">Narzędzie bcp nie został zainstalowany być niezawodne podczas ładowania danych za pośrednictwem Internetu.</span><span class="sxs-lookup"><span data-stu-id="77002-150">bcp has not been adapted to be robust when loading data over the internet.</span></span> <span data-ttu-id="77002-151">Niestabilności sieci może spowodować błąd ładowania.</span><span class="sxs-lookup"><span data-stu-id="77002-151">Any network instability may cause a load error.</span></span>
* <span data-ttu-id="77002-152">Narzędzie bcp zależy od schematu jest obecny w docelowej bazie danych przed obciążenia</span><span class="sxs-lookup"><span data-stu-id="77002-152">bcp relies on the schema being present in the target database prior to the load</span></span>

<span data-ttu-id="77002-153">Aby uzyskać więcej informacji, zobacz [bcp umożliwia ładowanie danych do usługi SQL Data Warehouse][Use bcp to load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="77002-153">For more information, see [Use bcp to load data into SQL Data Warehouse][Use bcp to load data into SQL Data Warehouse].</span></span>

## <a name="optimizing-data-migration"></a><span data-ttu-id="77002-154">Optymalizacja migracji danych</span><span class="sxs-lookup"><span data-stu-id="77002-154">Optimizing data migration</span></span>
<span data-ttu-id="77002-155">Proces migracji danych SQLDW mogą skutecznie podzielone na trzy osobne kroki:</span><span class="sxs-lookup"><span data-stu-id="77002-155">A SQLDW data migration process can be effectively broken down into three discrete steps:</span></span>

1. <span data-ttu-id="77002-156">Eksport źródła danych</span><span class="sxs-lookup"><span data-stu-id="77002-156">Export of source data</span></span>
2. <span data-ttu-id="77002-157">Transfer danych do platformy Azure</span><span class="sxs-lookup"><span data-stu-id="77002-157">Transfer of data to Azure</span></span>
3. <span data-ttu-id="77002-158">Ładowanie do docelowej bazy danych SQLDW</span><span class="sxs-lookup"><span data-stu-id="77002-158">Load into the target SQLDW database</span></span>

<span data-ttu-id="77002-159">Każdy krok mogą być optymalizowane indywidualnie można utworzyć procesu migracji niezawodny, będzie można ponownie uruchomić systemu i elastyczne, które pozwala zmaksymalizować wydajność w każdym kroku.</span><span class="sxs-lookup"><span data-stu-id="77002-159">Each step can be individually optimized to create a robust, re-startable and resilient migration process that maximizes performance at each step.</span></span>

## <a name="optimizing-data-load"></a><span data-ttu-id="77002-160">Optymalizacja ładowania danych</span><span class="sxs-lookup"><span data-stu-id="77002-160">Optimizing data load</span></span>
<span data-ttu-id="77002-161">Spojrzenie na ich w kolejności odwrotnej do chwili; jest to najszybszy sposób, aby załadować dane przy użyciu programu PolyBase.</span><span class="sxs-lookup"><span data-stu-id="77002-161">Looking at these in reverse order for a moment; the fastest way to load data is via PolyBase.</span></span> <span data-ttu-id="77002-162">Optymalizacja dla proces ładowania PolyBase umieszcza wymagań wstępnych na powyższych kroków, najlepiej to zrozumieć góry.</span><span class="sxs-lookup"><span data-stu-id="77002-162">Optimizing for a PolyBase load process places prerequisites on the preceding steps so it's best to understand this upfront.</span></span> <span data-ttu-id="77002-163">Są to:</span><span class="sxs-lookup"><span data-stu-id="77002-163">They are:</span></span>

1. <span data-ttu-id="77002-164">Kodowanie plików danych</span><span class="sxs-lookup"><span data-stu-id="77002-164">Encoding of data files</span></span>
2. <span data-ttu-id="77002-165">Format plików danych</span><span class="sxs-lookup"><span data-stu-id="77002-165">Format of data files</span></span>
3. <span data-ttu-id="77002-166">Lokalizacja plików danych</span><span class="sxs-lookup"><span data-stu-id="77002-166">Location of data files</span></span>

### <a name="encoding"></a><span data-ttu-id="77002-167">Encoding</span><span class="sxs-lookup"><span data-stu-id="77002-167">Encoding</span></span>
<span data-ttu-id="77002-168">Program PolyBase wymaga danych plików UTF-8 lub UTF-16FE.</span><span class="sxs-lookup"><span data-stu-id="77002-168">PolyBase requires data files to be UTF-8 or UTF-16FE.</span></span> 



### <a name="format-of-data-files"></a><span data-ttu-id="77002-169">Format plików danych</span><span class="sxs-lookup"><span data-stu-id="77002-169">Format of data files</span></span>
<span data-ttu-id="77002-170">Program PolyBase ma terminatora stałym wiersza \n lub nowym wierszem.</span><span class="sxs-lookup"><span data-stu-id="77002-170">PolyBase mandates a fixed row terminator of \n or newline.</span></span> <span data-ttu-id="77002-171">Pliki danych musi być zgodna z tym standard.</span><span class="sxs-lookup"><span data-stu-id="77002-171">Your data files must conform to this standard.</span></span> <span data-ttu-id="77002-172">Nie ma ograniczeń terminatory parametry lub kolumny.</span><span class="sxs-lookup"><span data-stu-id="77002-172">There aren't any restrictions on string or column terminators.</span></span>

<span data-ttu-id="77002-173">Należy zdefiniować każdej kolumny w pliku jako część tabeli zewnętrznej w PolyBase.</span><span class="sxs-lookup"><span data-stu-id="77002-173">You will have to define every column in the file as part of your external table in PolyBase.</span></span> <span data-ttu-id="77002-174">Upewnij się, że wymagane są wszystkie kolumny wyeksportowany i że typów ze standardami wymagane.</span><span class="sxs-lookup"><span data-stu-id="77002-174">Make sure that all exported columns are required and that the types conform to the required standards.</span></span>

<span data-ttu-id="77002-175">Sprawdź odwołują się do [migracji schemat] artykułu dla szczegółów na obsługiwane typy danych.</span><span class="sxs-lookup"><span data-stu-id="77002-175">Please refer back to the [migrate your schema] article for detail on supported data types.</span></span>

### <a name="location-of-data-files"></a><span data-ttu-id="77002-176">Lokalizacja plików danych</span><span class="sxs-lookup"><span data-stu-id="77002-176">Location of data files</span></span>
<span data-ttu-id="77002-177">Usługa SQL Data Warehouse używa PolyBase wyłącznie ładowania danych z magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="77002-177">SQL Data Warehouse uses PolyBase to load data from Azure Blob Storage exclusively.</span></span> <span data-ttu-id="77002-178">W rezultacie dane musi najpierw przekazane do magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="77002-178">Consequently, the data must have been first transferred into blob storage.</span></span>

## <a name="optimizing-data-transfer"></a><span data-ttu-id="77002-179">Optymalizacja transferu danych</span><span class="sxs-lookup"><span data-stu-id="77002-179">Optimizing data transfer</span></span>
<span data-ttu-id="77002-180">Jedna z części najwolniejsze migracji danych jest przesyłanie danych do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="77002-180">One of the slowest parts of data migration is the transfer of the data to Azure.</span></span> <span data-ttu-id="77002-181">Nie tylko przepustowość sieci może być problemem, ale również niezawodność sieci może poważnie utrudniać postępu.</span><span class="sxs-lookup"><span data-stu-id="77002-181">Not only can network bandwidth be an issue but also network reliability can seriously hamper progress.</span></span> <span data-ttu-id="77002-182">Domyślnie migrację danych do platformy Azure jest za pośrednictwem Internetu, więc rozsądnych prawdopodobnie prawdopodobieństwo wystąpienia błędów transferu.</span><span class="sxs-lookup"><span data-stu-id="77002-182">By default migrating data to Azure is over the internet so the chances of transfer errors occurring are reasonably likely.</span></span> <span data-ttu-id="77002-183">Jednak te błędy mogą wymagać danych ponownego wysyłania w całości lub częściowo.</span><span class="sxs-lookup"><span data-stu-id="77002-183">However, these errors may require data to be re-sent either in whole or in part.</span></span>

<span data-ttu-id="77002-184">Na szczęście masz kilka opcji zwiększenie szybkości i odporności tego procesu:</span><span class="sxs-lookup"><span data-stu-id="77002-184">Fortunately you have several options to improve the speed and resilience of this process:</span></span>

### <a name="expressrouteexpressroute"></a><span data-ttu-id="77002-185">[ExpressRoute][ExpressRoute]</span><span class="sxs-lookup"><span data-stu-id="77002-185">[ExpressRoute][ExpressRoute]</span></span>
<span data-ttu-id="77002-186">Warto rozważyć użycie [ExpressRoute] [ ExpressRoute] celu przyspieszenia transferu.</span><span class="sxs-lookup"><span data-stu-id="77002-186">You may want to consider using [ExpressRoute][ExpressRoute] to speed up the transfer.</span></span> <span data-ttu-id="77002-187">[ExpressRoute] [ ExpressRoute] zawiera nawiązane połączenie prywatne do platformy Azure, połączenie nie przechodzi przez publicznej sieci internet.</span><span class="sxs-lookup"><span data-stu-id="77002-187">[ExpressRoute][ExpressRoute] provides you with an established private connection to Azure so the connection does not go over the public internet.</span></span> <span data-ttu-id="77002-188">W żadnym wypadku nie jest to krok obowiązkowe.</span><span class="sxs-lookup"><span data-stu-id="77002-188">This is by no means a mandatory step.</span></span> <span data-ttu-id="77002-189">Jednak go może zwiększyć przepustowość podczas przekazywanie danych do platformy Azure z lokalnymi lub wspólnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="77002-189">However, it will improve throughput when pushing data to Azure from an on-premises or co-location facility.</span></span>

<span data-ttu-id="77002-190">Korzyści wynikające ze stosowania [ExpressRoute] [ ExpressRoute] są:</span><span class="sxs-lookup"><span data-stu-id="77002-190">The benefits of using [ExpressRoute][ExpressRoute] are:</span></span>

1. <span data-ttu-id="77002-191">Zwiększenie niezawodności</span><span class="sxs-lookup"><span data-stu-id="77002-191">Increased reliability</span></span>
2. <span data-ttu-id="77002-192">Szybsze sieci</span><span class="sxs-lookup"><span data-stu-id="77002-192">Faster network speed</span></span>
3. <span data-ttu-id="77002-193">Mniejsze opóźnienia sieci</span><span class="sxs-lookup"><span data-stu-id="77002-193">Lower network latency</span></span>
4. <span data-ttu-id="77002-194">wyższy poziom zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="77002-194">higher network security</span></span>

<span data-ttu-id="77002-195">[ExpressRoute] [ ExpressRoute] jest przydatne w przypadku różnych scenariuszach; nie tylko migracji.</span><span class="sxs-lookup"><span data-stu-id="77002-195">[ExpressRoute][ExpressRoute] is beneficial for a number of scenarios; not just the migration.</span></span>

<span data-ttu-id="77002-196">Chcesz spróbować?</span><span class="sxs-lookup"><span data-stu-id="77002-196">Interested?</span></span> <span data-ttu-id="77002-197">Więcej informacji i cenach należy znaleźć [dokumentacja usługi ExpressRoute][ExpressRoute documentation].</span><span class="sxs-lookup"><span data-stu-id="77002-197">For more information and pricing please visit the [ExpressRoute documentation][ExpressRoute documentation].</span></span>

### <a name="azure-import-and-export-service"></a><span data-ttu-id="77002-198">Azure importu i eksportu usługi</span><span class="sxs-lookup"><span data-stu-id="77002-198">Azure Import and Export Service</span></span>
<span data-ttu-id="77002-199">Azure importowanie i eksportowanie usługi to proces transferu danych, przeznaczony dla dużych (GB ++) do dużego (TB ++) transferów danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="77002-199">The Azure Import and Export Service is a data transfer process designed for large (GB++) to massive (TB++) transfers of data into Azure.</span></span> <span data-ttu-id="77002-200">Obejmuje ona zapisywania danych na dyskach i wysyłania ich do centrum danych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="77002-200">It involves writing your data to disks and shipping them to an Azure data center.</span></span> <span data-ttu-id="77002-201">Zawartość dysku zostaną następnie załadowane na obiektach blob magazynu Azure w Twoim imieniu.</span><span class="sxs-lookup"><span data-stu-id="77002-201">The disk contents will then be loaded into Azure Storage Blobs on your behalf.</span></span>

<span data-ttu-id="77002-202">Ogólny widok procesu eksportowania importu jest następujący:</span><span class="sxs-lookup"><span data-stu-id="77002-202">A high-level view of the import export process is as follows:</span></span>

1. <span data-ttu-id="77002-203">Skonfiguruj kontener magazynu obiektów Blob Azure do odbioru danych</span><span class="sxs-lookup"><span data-stu-id="77002-203">Configure an Azure Blob Storage container to receive the data</span></span>
2. <span data-ttu-id="77002-204">Eksportuj dane do lokalnego magazynu</span><span class="sxs-lookup"><span data-stu-id="77002-204">Export your data to local storage</span></span>
3. <span data-ttu-id="77002-205">Kopiuj dane do 3,5 cala SATA II/III dysków twardych za pomocą [narzędzie importu/eksportu Azure]</span><span class="sxs-lookup"><span data-stu-id="77002-205">Copy the data to 3.5 inch SATA II/III hard disk drives using the [Azure Import/Export Tool]</span></span>
4. <span data-ttu-id="77002-206">Utwórz zadanie importu za pomocą usługi Azure importu i eksportu usługi, podając pliki dziennika utworzone przez [narzędzie importu/eksportu Azure]</span><span class="sxs-lookup"><span data-stu-id="77002-206">Create an Import Job using the Azure Import and Export Service providing the journal files produced by the [Azure Import/Export Tool]</span></span>
5. <span data-ttu-id="77002-207">Wyślij dyski centrum danych Azure nominalnym</span><span class="sxs-lookup"><span data-stu-id="77002-207">Ship the disks your nominated Azure data center</span></span>
6. <span data-ttu-id="77002-208">Dane są przekazywane do Twojej kontenera magazynu obiektów Blob Azure</span><span class="sxs-lookup"><span data-stu-id="77002-208">Your data is transferred to your Azure Blob Storage container</span></span>
7. <span data-ttu-id="77002-209">Ładowanie danych do SQLDW przy użyciu programu PolyBase</span><span class="sxs-lookup"><span data-stu-id="77002-209">Load the data into SQLDW using PolyBase</span></span>

### <a name="azcopyazcopy-utility"></a><span data-ttu-id="77002-210">[Narzędzie AZCopy][Narzędzie AZCopy] narzędzia</span><span class="sxs-lookup"><span data-stu-id="77002-210">[AZCopy][AZCopy] utility</span></span>
<span data-ttu-id="77002-211">[Narzędzie AZCopy][Narzędzie AZCopy] narzędzie to doskonałe narzędzie do pobierania danych przesyłanych w obiektach blob magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="77002-211">The [AZCopy][AZCopy] utility is a great tool for getting your data transferred into Azure Storage Blobs.</span></span> <span data-ttu-id="77002-212">Jest on przeznaczony dla małych (MB ++) do bardzo dużych transferów danych (GB ++).</span><span class="sxs-lookup"><span data-stu-id="77002-212">It is designed for small (MB++) to very large (GB++) data transfers.</span></span> <span data-ttu-id="77002-213">[Narzędzie AZCopy] została opracowana również w celu zapewnienia dobrej przepływności elastyczne podczas transferu danych do platformy Azure i dlatego jest doskonałym wyborem kroku transferu danych.</span><span class="sxs-lookup"><span data-stu-id="77002-213">[AZCopy] has also been designed to provide good resilient throughput when transferring data to Azure and so is a great choice for the data transfer step.</span></span> <span data-ttu-id="77002-214">Raz przeniesione, można załadować danych do usługi SQL Data Warehouse przy użyciu programu PolyBase.</span><span class="sxs-lookup"><span data-stu-id="77002-214">Once transferred you can load the data using PolyBase into SQL Data Warehouse.</span></span> <span data-ttu-id="77002-215">Narzędzia AZCopy można również zastosować w pakietów SSIS za pomocą zadania "Wykonania procesu".</span><span class="sxs-lookup"><span data-stu-id="77002-215">You can also incorporate AZCopy into your SSIS packages using an "Execute Process" task.</span></span>

<span data-ttu-id="77002-216">Można użyć narzędzia AZCopy najpierw należy pobrać i zainstalować go.</span><span class="sxs-lookup"><span data-stu-id="77002-216">To use AZCopy you will first need to download and install it.</span></span> <span data-ttu-id="77002-217">Brak [wersji produkcyjnej] [ production version] i [wersji zapoznawczej] [ preview version] dostępne.</span><span class="sxs-lookup"><span data-stu-id="77002-217">There is a [production version][production version] and a [preview version][preview version] available.</span></span>

<span data-ttu-id="77002-218">Aby przekazać plik z systemu plików są potrzebne polecenie podobny do poniższego:</span><span class="sxs-lookup"><span data-stu-id="77002-218">To upload a file from your file system you will need a command like the one below:</span></span>

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="77002-219">Podsumowanie procesu może być:</span><span class="sxs-lookup"><span data-stu-id="77002-219">A high-level process summary could be:</span></span>

1. <span data-ttu-id="77002-220">Skonfiguruj kontener obiektu blob magazynu Azure do odbioru danych</span><span class="sxs-lookup"><span data-stu-id="77002-220">Configure an Azure storage blob container to receive the data</span></span>
2. <span data-ttu-id="77002-221">Eksportuj dane do lokalnego magazynu</span><span class="sxs-lookup"><span data-stu-id="77002-221">Export your data to local storage</span></span>
3. <span data-ttu-id="77002-222">Narzędzie AZCopy dane w kontenerze magazynu obiektów Blob Azure</span><span class="sxs-lookup"><span data-stu-id="77002-222">AZCopy your data in the Azure Blob Storage container</span></span>
4. <span data-ttu-id="77002-223">Ładowanie danych do usługi SQL Data Warehouse przy użyciu programu PolyBase</span><span class="sxs-lookup"><span data-stu-id="77002-223">Load the data into SQL Data Warehouse using PolyBase</span></span>

<span data-ttu-id="77002-224">Pełna dokumentacja: [Narzędzie AZCopy][Narzędzie AZCopy].</span><span class="sxs-lookup"><span data-stu-id="77002-224">Full documentation available: [AZCopy][AZCopy].</span></span>

## <a name="optimizing-data-export"></a><span data-ttu-id="77002-225">Optymalizowanie eksportowanie danych</span><span class="sxs-lookup"><span data-stu-id="77002-225">Optimizing data export</span></span>
<span data-ttu-id="77002-226">Oprócz zapewniania, że Eksport spełnia wymagania, którego układ określa się w programie PolyBase mogą również wyszukiwać zoptymalizować eksportowania danych w celu zwiększenia procesu dalsze.</span><span class="sxs-lookup"><span data-stu-id="77002-226">In addition to ensuring that the export conforms to the requirements laid out by PolyBase you can also seek to optimize the export of the data to improve the process further.</span></span>



### <a name="data-compression"></a><span data-ttu-id="77002-227">Kompresja danych</span><span class="sxs-lookup"><span data-stu-id="77002-227">Data compression</span></span>
<span data-ttu-id="77002-228">Program PolyBase mogą odczytywać dane skompresowane gzip.</span><span class="sxs-lookup"><span data-stu-id="77002-228">PolyBase can read gzip compressed data.</span></span> <span data-ttu-id="77002-229">Jeśli będziesz mieć możliwość kompresowania danych do plików gzip będzie zminimalizować ilość danych przekazywanej za pośrednictwem sieci.</span><span class="sxs-lookup"><span data-stu-id="77002-229">If you are able to compress your data to gzip files then you will minimize the amount of data being pushed over the network.</span></span>

### <a name="multiple-files"></a><span data-ttu-id="77002-230">Wiele plików</span><span class="sxs-lookup"><span data-stu-id="77002-230">Multiple files</span></span>
<span data-ttu-id="77002-231">Podzielenie dużych tabel do wielu plików nie tylko pomaga w celu zwiększenia szybkości eksportu, ale także z re-startability transferu, a także ogólne możliwości zarządzania danych raz w magazynie obiektów blob Azure.</span><span class="sxs-lookup"><span data-stu-id="77002-231">Breaking up large tables into several files not only helps to improve export speed, it also helps with transfer re-startability, and the overall manageability of the data once in the Azure blob storage.</span></span> <span data-ttu-id="77002-232">Jest jedną z wielu funkcji nieuprzywilejowany PolyBase, że wszystkie pliki w folderze odczytuje i traktować go jako jedna tabela.</span><span class="sxs-lookup"><span data-stu-id="77002-232">One of the many nice features of PolyBase is that it will read all the files inside a folder and treat it as one table.</span></span> <span data-ttu-id="77002-233">W związku z tym jest dobrym rozwiązaniem, aby wyodrębnić pliki dla każdej tabeli do własnego folderu.</span><span class="sxs-lookup"><span data-stu-id="77002-233">It is therefore a good idea to isolate the files for each table into its own folder.</span></span>

<span data-ttu-id="77002-234">Aparat PolyBase obsługuje również funkcją znana jako "Przechodzenie folderu cykliczne".</span><span class="sxs-lookup"><span data-stu-id="77002-234">PolyBase also supports a feature known as "recursive folder traversal".</span></span> <span data-ttu-id="77002-235">Ta funkcja służy do zwiększenia organizacji wyeksportowane dane, aby poprawić zarządzanie danych.</span><span class="sxs-lookup"><span data-stu-id="77002-235">You can use this feature to further enhance the organization of your exported data to improve your data management.</span></span>

<span data-ttu-id="77002-236">Aby dowiedzieć się więcej na temat ładowanie danych przy użyciu programu PolyBase, zobacz [Użyj PolyBase, aby załadować dane do usługi SQL Data Warehouse][Use PolyBase to load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="77002-236">To learn more about loading data with PolyBase, see [Use PolyBase to load data into SQL Data Warehouse][Use PolyBase to load data into SQL Data Warehouse].</span></span>

## <a name="next-steps"></a><span data-ttu-id="77002-237">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="77002-237">Next steps</span></span>
<span data-ttu-id="77002-238">Aby uzyskać więcej informacji na temat migracji, zobacz [migracja rozwiązania do usługi SQL Data Warehouse][Migrate your solution to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="77002-238">For more about migration, see [Migrate your solution to SQL Data Warehouse][Migrate your solution to SQL Data Warehouse].</span></span>
<span data-ttu-id="77002-239">Aby uzyskać więcej porad programistycznych, zobacz [omówienie tworzenia][development overview].</span><span class="sxs-lookup"><span data-stu-id="77002-239">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Narzędzie AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution to SQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp to load data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase to load data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
