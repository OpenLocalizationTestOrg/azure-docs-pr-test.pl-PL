---
title: aaaMigrate tooSQL Twojej danych hurtowni danych | Dokumentacja firmy Microsoft
description: "Wskazówki dotyczące migrowania tooAzure Twojego danych usługi SQL Data Warehouse związane z opracowywaniem rozwiązań."
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
ms.openlocfilehash: fe4c6b7e82094c59c45e06be6da225fee1b707ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data"></a><span data-ttu-id="fda9b-103">Migrowanie danych</span><span class="sxs-lookup"><span data-stu-id="fda9b-103">Migrate Your Data</span></span>
<span data-ttu-id="fda9b-104">Można przenieść dane z różnych źródeł do magazynu danych SQL przy użyciu różnych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="fda9b-104">Data can be moved from different sources into your SQL Data Warehouse with a variety tools.</span></span>  <span data-ttu-id="fda9b-105">Kopiuj ADF, SSIS i może bcp wszystkie można tooachieve używanych w tym celu.</span><span class="sxs-lookup"><span data-stu-id="fda9b-105">ADF Copy, SSIS, and bcp can all be used tooachieve this goal.</span></span> <span data-ttu-id="fda9b-106">Jednak miarę wzrostu hello ilości danych możesz pomyśleć o podziału hello proces migracji danych do kroków.</span><span class="sxs-lookup"><span data-stu-id="fda9b-106">However, as hello amount of data increases you should think about breaking down hello data migration process into steps.</span></span> <span data-ttu-id="fda9b-107">Dzięki temu hello toooptimize okazji każdego kroku zarówno wydajności i odporności tooensure migracji smooth danych.</span><span class="sxs-lookup"><span data-stu-id="fda9b-107">This affords you hello opportunity toooptimize each step both for performance and for resilience tooensure a smooth data migration.</span></span>

<span data-ttu-id="fda9b-108">W tym artykule omówiono najpierw scenariusze migracji prostego powitania ADF kopiowania, SSIS i bcp.</span><span class="sxs-lookup"><span data-stu-id="fda9b-108">This article first discusses hello simple migration scenarios of ADF Copy, SSIS, and bcp.</span></span> <span data-ttu-id="fda9b-109">Następnie wygląda bardziej szczegółowe w sposób mogą być optymalizowane hello migracji.</span><span class="sxs-lookup"><span data-stu-id="fda9b-109">It then look a little deeper into how hello migration can be optimized.</span></span>

## <a name="azure-data-factory-adf-copy"></a><span data-ttu-id="fda9b-110">Azure kopiowania fabryki danych (ADF)</span><span class="sxs-lookup"><span data-stu-id="fda9b-110">Azure Data Factory (ADF) copy</span></span>
<span data-ttu-id="fda9b-111">[Kopiuj ADF] [ ADF Copy] jest częścią [fabryki danych Azure][Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="fda9b-111">[ADF Copy][ADF Copy] is part of [Azure Data Factory][Azure Data Factory].</span></span> <span data-ttu-id="fda9b-112">Można użyć tooexport ADF kopiowania plików tooflat danych znajdującej się w magazynie lokalnym plików prostych tooremote przechowywany w magazynie obiektów blob platformy Azure lub bezpośrednio do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="fda9b-112">You can use ADF Copy tooexport your data tooflat files residing on local storage, tooremote flat files held in Azure blob storage or directly into SQL Data Warehouse.</span></span>

<span data-ttu-id="fda9b-113">Jeśli danych rozpoczyna się w płaskiej plików, a następnie należy najpierw tootransfer go tooAzure obiektu blob magazynu przed zainicjowaniem obciążenia go do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="fda9b-113">If your data starts in flat files, then you will first need tootransfer it tooAzure storage blob before initiating a load it into SQL Data Warehouse.</span></span> <span data-ttu-id="fda9b-114">Po hello dane są przesyłane do magazynu obiektów blob platformy Azure można wybrać toouse [kopiowania ADF] [ ADF Copy] ponownie toopush hello danych do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="fda9b-114">Once hello data is transferred into Azure blob storage you can choose toouse [ADF Copy][ADF Copy] again toopush hello data into SQL Data Warehouse.</span></span>

<span data-ttu-id="fda9b-115">Aparat PolyBase zapewnia również opcję wysokiej wydajności dla ładowania danych hello.</span><span class="sxs-lookup"><span data-stu-id="fda9b-115">PolyBase also provides a high-performance option for loading hello data.</span></span> <span data-ttu-id="fda9b-116">Która jednak oznaczają za pomocą dwóch narzędzi, zamiast jednego.</span><span class="sxs-lookup"><span data-stu-id="fda9b-116">However, that does mean using two tools instead of one.</span></span> <span data-ttu-id="fda9b-117">Jeśli konieczne hello najlepszą wydajność, użyj programu PolyBase.</span><span class="sxs-lookup"><span data-stu-id="fda9b-117">If you need hello best performance then use PolyBase.</span></span> <span data-ttu-id="fda9b-118">Jeśli w środowisku jednego narzędzia (co hello danych nie jest bardzo dużej) ADF jest odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="fda9b-118">If you want a single tool experience (and hello data is not massive) then ADF is your answer.</span></span>


> 
> 

<span data-ttu-id="fda9b-119">HEAD za pośrednictwem toohello poniższego artykułu dla niektórych Wielkiej [przykłady ADF][ADF samples].</span><span class="sxs-lookup"><span data-stu-id="fda9b-119">Head over toohello following article for some great [ADF samples][ADF samples].</span></span>

## <a name="integration-services"></a><span data-ttu-id="fda9b-120">Usługi integracji</span><span class="sxs-lookup"><span data-stu-id="fda9b-120">Integration Services</span></span>
<span data-ttu-id="fda9b-121">Integration Services (SSIS) to wydajny i elastyczny wyodrębniania, przekształcania i ładowania (ETL) Narzędzie obsługującego złożone przepływy pracy, przekształcania danych i kilka opcji ładowania danych.</span><span class="sxs-lookup"><span data-stu-id="fda9b-121">Integration Services (SSIS) is a powerful and flexible Extract Transform and Load (ETL) tool that supports complex workflows, data transformation, and several data loading options.</span></span> <span data-ttu-id="fda9b-122">Użyj SSIS toosimply transferu danych tooAzure lub w ramach szerszych migracji.</span><span class="sxs-lookup"><span data-stu-id="fda9b-122">Use SSIS toosimply transfer data tooAzure or as part of a broader migration.</span></span>

> [!NOTE]
> <span data-ttu-id="fda9b-123">SSIS można wyeksportować tooUTF-8 bez hello znacznika kolejności bajtów w pliku hello.</span><span class="sxs-lookup"><span data-stu-id="fda9b-123">SSIS can export tooUTF-8 without hello byte order mark in hello file.</span></span> <span data-ttu-id="fda9b-124">tooconfigure, to należy najpierw użyć hello utworzona kolumna danych znakowych hello tooconvert składnika w hello danych przepływu toouse hello 65001 UTF-8 stronę kodową.</span><span class="sxs-lookup"><span data-stu-id="fda9b-124">tooconfigure this you must first use hello derived column component tooconvert hello character data in hello data flow toouse hello 65001 UTF-8 code page.</span></span> <span data-ttu-id="fda9b-125">Po konwersji kolumny hello zapisu hello danych toohello pliku prostego docelowej karty sprawdzeniu, czy 65001 została również wybrana jako strona kodowa hello hello pliku.</span><span class="sxs-lookup"><span data-stu-id="fda9b-125">Once hello columns have been converted, write hello data toohello flat file destination adapter ensuring that 65001 has also been selected as hello code page for hello file.</span></span>
> 
> 

<span data-ttu-id="fda9b-126">SSIS łączy tooSQL hurtowni danych, tak samo, jak może zostać nawiązane tooa wdrożenie programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fda9b-126">SSIS connects tooSQL Data Warehouse just as it would connect tooa SQL Server deployment.</span></span> <span data-ttu-id="fda9b-127">Jednak połączenia należy toobe za pomocą Menedżera połączenia ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="fda9b-127">However, your connections will need toobe using an ADO.NET connection manager.</span></span> <span data-ttu-id="fda9b-128">Również należy zadbać hello tooconfigure "Jeśli jest dostępna, użyj zostanie wstawiania zbiorczego" ustawienie toomaximize przepływności.</span><span class="sxs-lookup"><span data-stu-id="fda9b-128">You should also take care tooconfigure hello "Use bulk insert when available" setting toomaximize throughput.</span></span> <span data-ttu-id="fda9b-129">Zobacz toohello [ADO.NET docelowy adapter] [ ADO.NET destination adapter] toolearn artykułu więcej informacji na temat tej właściwości</span><span class="sxs-lookup"><span data-stu-id="fda9b-129">Please refer toohello [ADO.NET destination adapter][ADO.NET destination adapter] article toolearn more about this property</span></span>

> [!NOTE]
> <span data-ttu-id="fda9b-130">Łączenie tooAzure SQL Data Warehouse przy użyciu OLEDB nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="fda9b-130">Connecting tooAzure SQL Data Warehouse by using OLEDB is not supported.</span></span>
> 
> 

<span data-ttu-id="fda9b-131">Ponadto istnieje możliwość hello pakietu może zakończyć się niepowodzeniem ze względu na problemy z toothrottling lub sieci.</span><span class="sxs-lookup"><span data-stu-id="fda9b-131">In addition, there is always hello possibility that a package might fail due toothrottling or network issues.</span></span> <span data-ttu-id="fda9b-132">Projekt pakietów, ich można wznawiać na powitania punktu awarii, bez ponawianie pracy, który zakończył się przed awarią hello.</span><span class="sxs-lookup"><span data-stu-id="fda9b-132">Design packages so they can be resumed at hello point of failure, without redoing work that completed before hello failure.</span></span>

<span data-ttu-id="fda9b-133">Aby uzyskać więcej informacji, zapoznaj się hello [dokumentacji SSIS][SSIS documentation].</span><span class="sxs-lookup"><span data-stu-id="fda9b-133">For more information consult hello [SSIS documentation][SSIS documentation].</span></span>

## <a name="bcp"></a><span data-ttu-id="fda9b-134">bcp</span><span class="sxs-lookup"><span data-stu-id="fda9b-134">bcp</span></span>
<span data-ttu-id="fda9b-135">Narzędzie bcp jest narzędziem wiersza polecenia, które jest przeznaczone do pliku prostego importowania i eksportowania danych.</span><span class="sxs-lookup"><span data-stu-id="fda9b-135">bcp is a command-line utility that is designed for flat file data import and export.</span></span> <span data-ttu-id="fda9b-136">Niektóre przekształcania może odbywać się podczas eksportowania danych.</span><span class="sxs-lookup"><span data-stu-id="fda9b-136">Some transformation can take place during data export.</span></span> <span data-ttu-id="fda9b-137">przekształcenia proste tooperform Użyj tooselect zapytania i przekształcania danych hello.</span><span class="sxs-lookup"><span data-stu-id="fda9b-137">tooperform simple transformations use a query tooselect and transform hello data.</span></span> <span data-ttu-id="fda9b-138">Po wyeksportowane, plików prostych hello, następnie mogą być ładowane bezpośrednio do hello docelowej hello magazyn danych SQL z bazy danych.</span><span class="sxs-lookup"><span data-stu-id="fda9b-138">Once exported, hello flat files can then be loaded directly into hello target hello SQL Data Warehouse database.</span></span>

> [!NOTE]
> <span data-ttu-id="fda9b-139">Często jest dobrym rozwiązaniem hello tooencapsulate, transformacje używane podczas danych eksportu w widoku w systemie źródłowym hello.</span><span class="sxs-lookup"><span data-stu-id="fda9b-139">It is often a good idea tooencapsulate hello transformations used during data export in a view on hello source system.</span></span> <span data-ttu-id="fda9b-140">Dzięki temu logika hello jest zachowywana, a proces hello jest powtarzalne.</span><span class="sxs-lookup"><span data-stu-id="fda9b-140">This ensures that hello logic is retained and hello process is repeatable.</span></span>
> 
> 

<span data-ttu-id="fda9b-141">Zalety programu bcp są następujące:</span><span class="sxs-lookup"><span data-stu-id="fda9b-141">Advantages of bcp are:</span></span>

* <span data-ttu-id="fda9b-142">Prostota.</span><span class="sxs-lookup"><span data-stu-id="fda9b-142">Simplicity.</span></span> <span data-ttu-id="fda9b-143">polecenia BCP są proste toobuild i wykonania</span><span class="sxs-lookup"><span data-stu-id="fda9b-143">bcp commands are simple toobuild and execute</span></span>
* <span data-ttu-id="fda9b-144">Proces ładowania jej ponownie uruchomić.</span><span class="sxs-lookup"><span data-stu-id="fda9b-144">Re-startable load process.</span></span> <span data-ttu-id="fda9b-145">Raz wyeksportowanego hello obciążenia mogą być wykonywane dowolną liczbę razy</span><span class="sxs-lookup"><span data-stu-id="fda9b-145">Once exported hello load can be executed any number of times</span></span>

<span data-ttu-id="fda9b-146">Ograniczenia programu bcp są:</span><span class="sxs-lookup"><span data-stu-id="fda9b-146">Limitations of bcp are:</span></span>

* <span data-ttu-id="fda9b-147">Narzędzie bcp działa tylko tabelaryczne plików prostych.</span><span class="sxs-lookup"><span data-stu-id="fda9b-147">bcp works with tabulated flat files only.</span></span> <span data-ttu-id="fda9b-148">Nie działa z plikami, takie jak xml lub JSON</span><span class="sxs-lookup"><span data-stu-id="fda9b-148">It does not work with files such as xml or JSON</span></span>
* <span data-ttu-id="fda9b-149">Funkcje przekształcania danych są ograniczone toohello eksportu tylko przemieszczanie i proste charakteru</span><span class="sxs-lookup"><span data-stu-id="fda9b-149">Data transformation capabilities are limited toohello export stage only and are simple in nature</span></span>
* <span data-ttu-id="fda9b-150">BCP nie został dostosowany toobe niezawodne, podczas ładowania danych za pośrednictwem hello internet.</span><span class="sxs-lookup"><span data-stu-id="fda9b-150">bcp has not been adapted toobe robust when loading data over hello internet.</span></span> <span data-ttu-id="fda9b-151">Niestabilności sieci może spowodować błąd ładowania.</span><span class="sxs-lookup"><span data-stu-id="fda9b-151">Any network instability may cause a load error.</span></span>
* <span data-ttu-id="fda9b-152">Narzędzie bcp zależy od schematu hello są obecne w hello docelowej bazy danych poprzednich toohello obciążenia</span><span class="sxs-lookup"><span data-stu-id="fda9b-152">bcp relies on hello schema being present in hello target database prior toohello load</span></span>

<span data-ttu-id="fda9b-153">Aby uzyskać więcej informacji, zobacz [Użyj narzędzia bcp tooload danych do usługi SQL Data Warehouse][Use bcp tooload data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="fda9b-153">For more information, see [Use bcp tooload data into SQL Data Warehouse][Use bcp tooload data into SQL Data Warehouse].</span></span>

## <a name="optimizing-data-migration"></a><span data-ttu-id="fda9b-154">Optymalizacja migracji danych</span><span class="sxs-lookup"><span data-stu-id="fda9b-154">Optimizing data migration</span></span>
<span data-ttu-id="fda9b-155">Proces migracji danych SQLDW mogą skutecznie podzielone na trzy osobne kroki:</span><span class="sxs-lookup"><span data-stu-id="fda9b-155">A SQLDW data migration process can be effectively broken down into three discrete steps:</span></span>

1. <span data-ttu-id="fda9b-156">Eksport źródła danych</span><span class="sxs-lookup"><span data-stu-id="fda9b-156">Export of source data</span></span>
2. <span data-ttu-id="fda9b-157">Transfer danych tooAzure</span><span class="sxs-lookup"><span data-stu-id="fda9b-157">Transfer of data tooAzure</span></span>
3. <span data-ttu-id="fda9b-158">Ładowanie do hello docelowej SQLDW bazy danych</span><span class="sxs-lookup"><span data-stu-id="fda9b-158">Load into hello target SQLDW database</span></span>

<span data-ttu-id="fda9b-159">Każdy krok można osobno zoptymalizowane toocreate proces migracji niezawodny, będzie można ponownie uruchomić systemu i elastyczne, które pozwala zmaksymalizować wydajność w każdym kroku.</span><span class="sxs-lookup"><span data-stu-id="fda9b-159">Each step can be individually optimized toocreate a robust, re-startable and resilient migration process that maximizes performance at each step.</span></span>

## <a name="optimizing-data-load"></a><span data-ttu-id="fda9b-160">Optymalizacja ładowania danych</span><span class="sxs-lookup"><span data-stu-id="fda9b-160">Optimizing data load</span></span>
<span data-ttu-id="fda9b-161">Spojrzenie na ich w kolejności odwrotnej do chwili; Witaj najszybszy sposób tooload danych odbywa się za pośrednictwem programu PolyBase.</span><span class="sxs-lookup"><span data-stu-id="fda9b-161">Looking at these in reverse order for a moment; hello fastest way tooload data is via PolyBase.</span></span> <span data-ttu-id="fda9b-162">Optymalizacja dla proces ładowania PolyBase umieszcza wymagania wstępne w poprzednich krokach, jest najlepszym toounderstand, to hello góry.</span><span class="sxs-lookup"><span data-stu-id="fda9b-162">Optimizing for a PolyBase load process places prerequisites on hello preceding steps so it's best toounderstand this upfront.</span></span> <span data-ttu-id="fda9b-163">Są to:</span><span class="sxs-lookup"><span data-stu-id="fda9b-163">They are:</span></span>

1. <span data-ttu-id="fda9b-164">Kodowanie plików danych</span><span class="sxs-lookup"><span data-stu-id="fda9b-164">Encoding of data files</span></span>
2. <span data-ttu-id="fda9b-165">Format plików danych</span><span class="sxs-lookup"><span data-stu-id="fda9b-165">Format of data files</span></span>
3. <span data-ttu-id="fda9b-166">Lokalizacja plików danych</span><span class="sxs-lookup"><span data-stu-id="fda9b-166">Location of data files</span></span>

### <a name="encoding"></a><span data-ttu-id="fda9b-167">Encoding</span><span class="sxs-lookup"><span data-stu-id="fda9b-167">Encoding</span></span>
<span data-ttu-id="fda9b-168">Program PolyBase wymaga toobe pliki danych UTF-8 lub UTF-16FE.</span><span class="sxs-lookup"><span data-stu-id="fda9b-168">PolyBase requires data files toobe UTF-8 or UTF-16FE.</span></span> 



### <a name="format-of-data-files"></a><span data-ttu-id="fda9b-169">Format plików danych</span><span class="sxs-lookup"><span data-stu-id="fda9b-169">Format of data files</span></span>
<span data-ttu-id="fda9b-170">Program PolyBase ma terminatora stałym wiersza \n lub nowym wierszem.</span><span class="sxs-lookup"><span data-stu-id="fda9b-170">PolyBase mandates a fixed row terminator of \n or newline.</span></span> <span data-ttu-id="fda9b-171">Pliki danych muszą być zgodne toothis standard.</span><span class="sxs-lookup"><span data-stu-id="fda9b-171">Your data files must conform toothis standard.</span></span> <span data-ttu-id="fda9b-172">Nie ma ograniczeń terminatory parametry lub kolumny.</span><span class="sxs-lookup"><span data-stu-id="fda9b-172">There aren't any restrictions on string or column terminators.</span></span>

<span data-ttu-id="fda9b-173">Konieczne będzie toodefine każdej kolumny w pliku hello jako część tabeli zewnętrznej w PolyBase.</span><span class="sxs-lookup"><span data-stu-id="fda9b-173">You will have toodefine every column in hello file as part of your external table in PolyBase.</span></span> <span data-ttu-id="fda9b-174">Upewnij się, że wymagane są wszystkie kolumny wyeksportowany i typy hello zgodność standardów toohello wymagane.</span><span class="sxs-lookup"><span data-stu-id="fda9b-174">Make sure that all exported columns are required and that hello types conform toohello required standards.</span></span>

<span data-ttu-id="fda9b-175">Można ponownie znaleźć toohello [migracji schemat] artykułu dla szczegółów na obsługiwane typy danych.</span><span class="sxs-lookup"><span data-stu-id="fda9b-175">Please refer back toohello [migrate your schema] article for detail on supported data types.</span></span>

### <a name="location-of-data-files"></a><span data-ttu-id="fda9b-176">Lokalizacja plików danych</span><span class="sxs-lookup"><span data-stu-id="fda9b-176">Location of data files</span></span>
<span data-ttu-id="fda9b-177">Usługa SQL Data Warehouse używany wyłącznie danych tooload PolyBase z magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="fda9b-177">SQL Data Warehouse uses PolyBase tooload data from Azure Blob Storage exclusively.</span></span> <span data-ttu-id="fda9b-178">W rezultacie dane hello musi najpierw przeniesiono do magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="fda9b-178">Consequently, hello data must have been first transferred into blob storage.</span></span>

## <a name="optimizing-data-transfer"></a><span data-ttu-id="fda9b-179">Optymalizacja transferu danych</span><span class="sxs-lookup"><span data-stu-id="fda9b-179">Optimizing data transfer</span></span>
<span data-ttu-id="fda9b-180">Jeden z elementów najwolniejsze hello migracji danych jest hello transferu hello tooAzure danych.</span><span class="sxs-lookup"><span data-stu-id="fda9b-180">One of hello slowest parts of data migration is hello transfer of hello data tooAzure.</span></span> <span data-ttu-id="fda9b-181">Nie tylko przepustowość sieci może być problemem, ale również niezawodność sieci może poważnie utrudniać postępu.</span><span class="sxs-lookup"><span data-stu-id="fda9b-181">Not only can network bandwidth be an issue but also network reliability can seriously hamper progress.</span></span> <span data-ttu-id="fda9b-182">Domyślnie migracja tooAzure danych znajduje się nad hello internet tak hello prawdopodobieństwo wystąpienia, prawdopodobnie rozsądnych błędów transferu.</span><span class="sxs-lookup"><span data-stu-id="fda9b-182">By default migrating data tooAzure is over hello internet so hello chances of transfer errors occurring are reasonably likely.</span></span> <span data-ttu-id="fda9b-183">Jednak te błędy mogą wymagać toobe dane wysyłane ponownie w całości lub częściowo.</span><span class="sxs-lookup"><span data-stu-id="fda9b-183">However, these errors may require data toobe re-sent either in whole or in part.</span></span>

<span data-ttu-id="fda9b-184">Na szczęście masz kilka opcji tooimprove hello szybkość i odporności tego procesu:</span><span class="sxs-lookup"><span data-stu-id="fda9b-184">Fortunately you have several options tooimprove hello speed and resilience of this process:</span></span>

### <a name="expressrouteexpressroute"></a><span data-ttu-id="fda9b-185">[ExpressRoute][ExpressRoute]</span><span class="sxs-lookup"><span data-stu-id="fda9b-185">[ExpressRoute][ExpressRoute]</span></span>
<span data-ttu-id="fda9b-186">Może być za pomocą tooconsider [ExpressRoute] [ ExpressRoute] toospeed się hello transferu.</span><span class="sxs-lookup"><span data-stu-id="fda9b-186">You may want tooconsider using [ExpressRoute][ExpressRoute] toospeed up hello transfer.</span></span> <span data-ttu-id="fda9b-187">[ExpressRoute] [ ExpressRoute] zapewnia o tooAzure ustanowionym połączeniu prywatnej tak hello połączenia nie został przekroczony hello publicznej sieci internet.</span><span class="sxs-lookup"><span data-stu-id="fda9b-187">[ExpressRoute][ExpressRoute] provides you with an established private connection tooAzure so hello connection does not go over hello public internet.</span></span> <span data-ttu-id="fda9b-188">W żadnym wypadku nie jest to krok obowiązkowe.</span><span class="sxs-lookup"><span data-stu-id="fda9b-188">This is by no means a mandatory step.</span></span> <span data-ttu-id="fda9b-189">Jednak go może zwiększyć przepustowość podczas wypychania danych tooAzure z lokalnymi lub wspólnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="fda9b-189">However, it will improve throughput when pushing data tooAzure from an on-premises or co-location facility.</span></span>

<span data-ttu-id="fda9b-190">Witaj korzyści wynikające ze stosowania [ExpressRoute] [ ExpressRoute] są:</span><span class="sxs-lookup"><span data-stu-id="fda9b-190">hello benefits of using [ExpressRoute][ExpressRoute] are:</span></span>

1. <span data-ttu-id="fda9b-191">Zwiększenie niezawodności</span><span class="sxs-lookup"><span data-stu-id="fda9b-191">Increased reliability</span></span>
2. <span data-ttu-id="fda9b-192">Szybsze sieci</span><span class="sxs-lookup"><span data-stu-id="fda9b-192">Faster network speed</span></span>
3. <span data-ttu-id="fda9b-193">Mniejsze opóźnienia sieci</span><span class="sxs-lookup"><span data-stu-id="fda9b-193">Lower network latency</span></span>
4. <span data-ttu-id="fda9b-194">wyższy poziom zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="fda9b-194">higher network security</span></span>

<span data-ttu-id="fda9b-195">[ExpressRoute] [ ExpressRoute] jest przydatne w przypadku różnych scenariuszach; hello nie tylko migracji.</span><span class="sxs-lookup"><span data-stu-id="fda9b-195">[ExpressRoute][ExpressRoute] is beneficial for a number of scenarios; not just hello migration.</span></span>

<span data-ttu-id="fda9b-196">Chcesz spróbować?</span><span class="sxs-lookup"><span data-stu-id="fda9b-196">Interested?</span></span> <span data-ttu-id="fda9b-197">Więcej informacji oraz sprawdź ceny odwiedź hello [dokumentacja usługi ExpressRoute][ExpressRoute documentation].</span><span class="sxs-lookup"><span data-stu-id="fda9b-197">For more information and pricing please visit hello [ExpressRoute documentation][ExpressRoute documentation].</span></span>

### <a name="azure-import-and-export-service"></a><span data-ttu-id="fda9b-198">Azure importu i eksportu usługi</span><span class="sxs-lookup"><span data-stu-id="fda9b-198">Azure Import and Export Service</span></span>
<span data-ttu-id="fda9b-199">Hello Azure importowania i eksportowania usługa jest z procesu transferu danych, przeznaczony dla dużych (GB ++) toomassive (TB ++) transferów danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="fda9b-199">hello Azure Import and Export Service is a data transfer process designed for large (GB++) toomassive (TB++) transfers of data into Azure.</span></span> <span data-ttu-id="fda9b-200">Obejmuje ona zapisywanie toodisks Twojego danych i wysyłania ich tooan centrum danych Azure.</span><span class="sxs-lookup"><span data-stu-id="fda9b-200">It involves writing your data toodisks and shipping them tooan Azure data center.</span></span> <span data-ttu-id="fda9b-201">zawartość dysku Hello zostaną następnie załadowane na obiektach blob magazynu Azure w Twoim imieniu.</span><span class="sxs-lookup"><span data-stu-id="fda9b-201">hello disk contents will then be loaded into Azure Storage Blobs on your behalf.</span></span>

<span data-ttu-id="fda9b-202">Ogólny widok procesu eksportu importowania hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="fda9b-202">A high-level view of hello import export process is as follows:</span></span>

1. <span data-ttu-id="fda9b-203">Konfigurowanie usługi Azure Blob Storage kontenera tooreceive hello danych</span><span class="sxs-lookup"><span data-stu-id="fda9b-203">Configure an Azure Blob Storage container tooreceive hello data</span></span>
2. <span data-ttu-id="fda9b-204">Eksportuj toolocal magazynu danych</span><span class="sxs-lookup"><span data-stu-id="fda9b-204">Export your data toolocal storage</span></span>
3. <span data-ttu-id="fda9b-205">Skopiuj hello danych too3.5 CAL SATA II/III dysków twardych za pomocą hello [narzędzie importu/eksportu Azure]</span><span class="sxs-lookup"><span data-stu-id="fda9b-205">Copy hello data too3.5 inch SATA II/III hard disk drives using hello [Azure Import/Export Tool]</span></span>
4. <span data-ttu-id="fda9b-206">Utwórz zadanie importu za pomocą hello Azure importu i eksportu usługi, zapewniając hello pliki dziennika utworzone przez hello [narzędzie importu/eksportu Azure]</span><span class="sxs-lookup"><span data-stu-id="fda9b-206">Create an Import Job using hello Azure Import and Export Service providing hello journal files produced by hello [Azure Import/Export Tool]</span></span>
5. <span data-ttu-id="fda9b-207">Wyślij centrum danych Azure nominalnym hello dysków</span><span class="sxs-lookup"><span data-stu-id="fda9b-207">Ship hello disks your nominated Azure data center</span></span>
6. <span data-ttu-id="fda9b-208">Twoje dane są przekazanych tooyour kontenera magazynu obiektów Blob Azure</span><span class="sxs-lookup"><span data-stu-id="fda9b-208">Your data is transferred tooyour Azure Blob Storage container</span></span>
7. <span data-ttu-id="fda9b-209">Ładowanie danych hello do SQLDW przy użyciu programu PolyBase</span><span class="sxs-lookup"><span data-stu-id="fda9b-209">Load hello data into SQLDW using PolyBase</span></span>

### <a name="azcopyazcopy-utility"></a><span data-ttu-id="fda9b-210">[Narzędzie AZCopy][Narzędzie AZCopy] narzędzia</span><span class="sxs-lookup"><span data-stu-id="fda9b-210">[AZCopy][AZCopy] utility</span></span>
<span data-ttu-id="fda9b-211">Witaj [Narzędzie AZCopy][Narzędzie AZCopy] narzędzie to doskonałe narzędzie do pobierania danych przesyłanych w obiektach blob magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="fda9b-211">hello [AZCopy][AZCopy] utility is a great tool for getting your data transferred into Azure Storage Blobs.</span></span> <span data-ttu-id="fda9b-212">Jest on przeznaczony dla małych (MB ++) toovery duże (GB ++) transferów danych.</span><span class="sxs-lookup"><span data-stu-id="fda9b-212">It is designed for small (MB++) toovery large (GB++) data transfers.</span></span> <span data-ttu-id="fda9b-213">[Narzędzie AZCopy] również została zaprojektowana tooprovide dobrej przepływności odporne podczas przesyłania danych tooAzure i dlatego jest doskonałym wyborem kroku przeniesienie danych hello.</span><span class="sxs-lookup"><span data-stu-id="fda9b-213">[AZCopy] has also been designed tooprovide good resilient throughput when transferring data tooAzure and so is a great choice for hello data transfer step.</span></span> <span data-ttu-id="fda9b-214">Raz przeniesione, można załadować danych hello przy użyciu programu PolyBase do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="fda9b-214">Once transferred you can load hello data using PolyBase into SQL Data Warehouse.</span></span> <span data-ttu-id="fda9b-215">Narzędzia AZCopy można również zastosować w pakietów SSIS za pomocą zadania "Wykonania procesu".</span><span class="sxs-lookup"><span data-stu-id="fda9b-215">You can also incorporate AZCopy into your SSIS packages using an "Execute Process" task.</span></span>

<span data-ttu-id="fda9b-216">toouse AZCopy, najpierw należy toodownload a go zainstalować.</span><span class="sxs-lookup"><span data-stu-id="fda9b-216">toouse AZCopy you will first need toodownload and install it.</span></span> <span data-ttu-id="fda9b-217">Brak [wersji produkcyjnej] [ production version] i [wersji zapoznawczej] [ preview version] dostępne.</span><span class="sxs-lookup"><span data-stu-id="fda9b-217">There is a [production version][production version] and a [preview version][preview version] available.</span></span>

<span data-ttu-id="fda9b-218">tooupload pliku z systemu plików, które mają być polecenia takie jak hello jedną poniżej:</span><span class="sxs-lookup"><span data-stu-id="fda9b-218">tooupload a file from your file system you will need a command like hello one below:</span></span>

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="fda9b-219">Podsumowanie procesu może być:</span><span class="sxs-lookup"><span data-stu-id="fda9b-219">A high-level process summary could be:</span></span>

1. <span data-ttu-id="fda9b-220">Konfigurowanie magazynu Azure blob kontenera tooreceive hello danych</span><span class="sxs-lookup"><span data-stu-id="fda9b-220">Configure an Azure storage blob container tooreceive hello data</span></span>
2. <span data-ttu-id="fda9b-221">Eksportuj toolocal magazynu danych</span><span class="sxs-lookup"><span data-stu-id="fda9b-221">Export your data toolocal storage</span></span>
3. <span data-ttu-id="fda9b-222">Dane w kontenerze magazynu obiektów Blob Azure hello AZCopy</span><span class="sxs-lookup"><span data-stu-id="fda9b-222">AZCopy your data in hello Azure Blob Storage container</span></span>
4. <span data-ttu-id="fda9b-223">Ładowanie danych hello do usługi SQL Data Warehouse przy użyciu programu PolyBase</span><span class="sxs-lookup"><span data-stu-id="fda9b-223">Load hello data into SQL Data Warehouse using PolyBase</span></span>

<span data-ttu-id="fda9b-224">Pełna dokumentacja: [Narzędzie AZCopy][Narzędzie AZCopy].</span><span class="sxs-lookup"><span data-stu-id="fda9b-224">Full documentation available: [AZCopy][AZCopy].</span></span>

## <a name="optimizing-data-export"></a><span data-ttu-id="fda9b-225">Optymalizowanie eksportowanie danych</span><span class="sxs-lookup"><span data-stu-id="fda9b-225">Optimizing data export</span></span>
<span data-ttu-id="fda9b-226">Ponadto tooensuring czy eksportu hello spełnia wymogi toohello określone przez aparat PolyBase można również można wyszukiwać eksportu hello toooptimize hello danych tooimprove hello procesu dalsze.</span><span class="sxs-lookup"><span data-stu-id="fda9b-226">In addition tooensuring that hello export conforms toohello requirements laid out by PolyBase you can also seek toooptimize hello export of hello data tooimprove hello process further.</span></span>



### <a name="data-compression"></a><span data-ttu-id="fda9b-227">Kompresja danych</span><span class="sxs-lookup"><span data-stu-id="fda9b-227">Data compression</span></span>
<span data-ttu-id="fda9b-228">Program PolyBase mogą odczytywać dane skompresowane gzip.</span><span class="sxs-lookup"><span data-stu-id="fda9b-228">PolyBase can read gzip compressed data.</span></span> <span data-ttu-id="fda9b-229">Jeśli jesteś stanie toocompress pliki toogzip danych, a następnie użytkownik zostanie zminimalizowane hello ilość danych przekazywanej hello sieci.</span><span class="sxs-lookup"><span data-stu-id="fda9b-229">If you are able toocompress your data toogzip files then you will minimize hello amount of data being pushed over hello network.</span></span>

### <a name="multiple-files"></a><span data-ttu-id="fda9b-230">Wiele plików</span><span class="sxs-lookup"><span data-stu-id="fda9b-230">Multiple files</span></span>
<span data-ttu-id="fda9b-231">Podzielenie dużych tabel do wielu plików nie tylko pomaga tooimprove wyeksportować szybkości, ale także z transfer re-startability i hello ogólne możliwości zarządzania danych hello raz w magazynie obiektów blob Azure hello.</span><span class="sxs-lookup"><span data-stu-id="fda9b-231">Breaking up large tables into several files not only helps tooimprove export speed, it also helps with transfer re-startability, and hello overall manageability of hello data once in hello Azure blob storage.</span></span> <span data-ttu-id="fda9b-232">Jeden z hello jest wiele funkcji nieuprzywilejowany PolyBase czy odczytuje wszystkie pliki hello znajduje się w folderze i traktować go jako jedna tabela.</span><span class="sxs-lookup"><span data-stu-id="fda9b-232">One of hello many nice features of PolyBase is that it will read all hello files inside a folder and treat it as one table.</span></span> <span data-ttu-id="fda9b-233">Dlatego jest dobrym rozwiązaniem tooisolate hello plików dla każdej tabeli do własnego folderu.</span><span class="sxs-lookup"><span data-stu-id="fda9b-233">It is therefore a good idea tooisolate hello files for each table into its own folder.</span></span>

<span data-ttu-id="fda9b-234">Aparat PolyBase obsługuje również funkcją znana jako "Przechodzenie folderu cykliczne".</span><span class="sxs-lookup"><span data-stu-id="fda9b-234">PolyBase also supports a feature known as "recursive folder traversal".</span></span> <span data-ttu-id="fda9b-235">Tej funkcji można używać toofurther zwiększenia hello organizacji tooimprove Twojego wyeksportowanych danych z danych zarządzania.</span><span class="sxs-lookup"><span data-stu-id="fda9b-235">You can use this feature toofurther enhance hello organization of your exported data tooimprove your data management.</span></span>

<span data-ttu-id="fda9b-236">toolearn więcej informacji na temat ładowanie danych przy użyciu programu PolyBase, zobacz [Użyj programu PolyBase tooload danych do usługi SQL Data Warehouse][Use PolyBase tooload data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="fda9b-236">toolearn more about loading data with PolyBase, see [Use PolyBase tooload data into SQL Data Warehouse][Use PolyBase tooload data into SQL Data Warehouse].</span></span>

## <a name="next-steps"></a><span data-ttu-id="fda9b-237">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fda9b-237">Next steps</span></span>
<span data-ttu-id="fda9b-238">Aby uzyskać więcej informacji na temat migracji, zobacz [migracji tooSQL Twojego rozwiązania magazynu danych][Migrate your solution tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="fda9b-238">For more about migration, see [Migrate your solution tooSQL Data Warehouse][Migrate your solution tooSQL Data Warehouse].</span></span>
<span data-ttu-id="fda9b-239">Aby uzyskać więcej porad programistycznych, zobacz [omówienie tworzenia][development overview].</span><span class="sxs-lookup"><span data-stu-id="fda9b-239">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Narzędzie AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution tooSQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp tooload data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase tooload data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
