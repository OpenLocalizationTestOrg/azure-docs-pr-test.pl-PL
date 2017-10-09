---
title: "Brama zarządzania danymi w informacjach o aaaRelease | Dokumentacja firmy Microsoft"
description: "Informacje o wersji tory zarządzania bramy danych"
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 14762e82-76d9-41c4-ba9f-14a54da29c36
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 3165d7537410a0531e0bb7f7fe584767f9155574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-data-management-gateway"></a><span data-ttu-id="43c9e-103">Informacje o wersji bramy zarządzania danymi</span><span class="sxs-lookup"><span data-stu-id="43c9e-103">Release notes for Data Management Gateway</span></span>
<span data-ttu-id="43c9e-104">Jest jednym z wyzwań hello integracji danych nowoczesnych toomove tooand danych z lokalnego toocloud.</span><span class="sxs-lookup"><span data-stu-id="43c9e-104">One of hello challenges for modern data integration is toomove data tooand from on-premises toocloud.</span></span> <span data-ttu-id="43c9e-105">Fabryka danych powoduje, że integracja z brama zarządzania danymi, które jest zainstalowanie przenoszenia danych hybrydowego tooenable lokalnego agenta.</span><span class="sxs-lookup"><span data-stu-id="43c9e-105">Data Factory makes this integration with Data Management Gateway, which is an agent that you can install on-premises tooenable hybrid data movement.</span></span>

<span data-ttu-id="43c9e-106">Zobacz następujące artykuły, aby uzyskać szczegółowe informacje na temat bramy zarządzania danymi hello i w jaki sposób toouse go:</span><span class="sxs-lookup"><span data-stu-id="43c9e-106">See hello following articles for detailed information about Data Management Gateway and how toouse it:</span></span>

*  [<span data-ttu-id="43c9e-107">Brama zarządzania danymi</span><span class="sxs-lookup"><span data-stu-id="43c9e-107">Data Management Gateway</span></span>](data-factory-data-management-gateway.md)
*  [<span data-ttu-id="43c9e-108">Przenoszenie danych między lokalnymi i w chmurze przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="43c9e-108">Move data between on-premises and cloud using Azure Data Factory</span></span>](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a><span data-ttu-id="43c9e-109">BIEŻĄCA WERSJA (2.10.6347.7)</span><span class="sxs-lookup"><span data-stu-id="43c9e-109">CURRENT VERSION (2.10.6347.7)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="43c9e-110">Ulepszenia-</span><span class="sxs-lookup"><span data-stu-id="43c9e-110">Enhancements-</span></span>
- <span data-ttu-id="43c9e-111">Można dodać magistrali usług toowhitelist wpisy DNS, a nie listę dozwolonych podobnej wszystkie adresy IP platformy Azure z zapory (w razie potrzeby).</span><span class="sxs-lookup"><span data-stu-id="43c9e-111">You can add DNS entries toowhitelist service bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="43c9e-112">Odpowiedni wpis DNS można znaleźć w portalu Azure (fabryka danych -> "Utwórz i wdróż" -> "Bramy" -> "serviceUrls" (w formacie JSON)</span><span class="sxs-lookup"><span data-stu-id="43c9e-112">You can find respective DNS entry on Azure portal (Data Factory -> ‘Author and Deploy’ -> ‘Gateways’ -> "serviceUrls" (in JSON)</span></span>
- <span data-ttu-id="43c9e-113">System plików HDFS łącznik obsługuje teraz publicznego certyfikatu z podpisem własnym można pominąć weryfikacji protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="43c9e-113">HDFS connector now supports self-signed public certificate by letting you skip SSL validation.</span></span>
- <span data-ttu-id="43c9e-114">Rozwiązany: Problem z bramą w trybie offline podczas aktualizacji (powodu tooclock zegara)</span><span class="sxs-lookup"><span data-stu-id="43c9e-114">Fixed: Issue with gateway offline during update (due tooclock skew)</span></span>



## <a name="earlier-versions"></a><span data-ttu-id="43c9e-115">Starszych wersji</span><span class="sxs-lookup"><span data-stu-id="43c9e-115">Earlier versions</span></span>

## <a name="2963132"></a><span data-ttu-id="43c9e-116">2.9.6313.2</span><span class="sxs-lookup"><span data-stu-id="43c9e-116">2.9.6313.2</span></span>
### <a name="enhancements-"></a><span data-ttu-id="43c9e-117">Ulepszenia-</span><span class="sxs-lookup"><span data-stu-id="43c9e-117">Enhancements-</span></span>
-   <span data-ttu-id="43c9e-118">Można dodać toowhitelist wpisy DNS usługi Service Bus, a nie listę dozwolonych podobnej wszystkie adresy IP platformy Azure z zapory (w razie potrzeby).</span><span class="sxs-lookup"><span data-stu-id="43c9e-118">You can add DNS entries toowhitelist Service Bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="43c9e-119">Więcej informacji w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="43c9e-119">More details here.</span></span>
-   <span data-ttu-id="43c9e-120">Teraz można skopiować danych z jednego blokowego obiektu blob się too4.75 TB, czyli hello maksymalny obsługiwany rozmiar blokowych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="43c9e-120">You can now copy data to/from a single block blob up too4.75 TB, which is hello max supported size of block blob.</span></span> <span data-ttu-id="43c9e-121">(limit wcześniej była 195 GB).</span><span class="sxs-lookup"><span data-stu-id="43c9e-121">(earlier limit was 195 GB).</span></span>
-   <span data-ttu-id="43c9e-122">Stałych: Za mało pamięci problem podczas rozpakować kilka małych plików podczas działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="43c9e-122">Fixed: Out of memory issue while unzipping several small files during copy activity.</span></span>
-   <span data-ttu-id="43c9e-123">Stały: Indeks poza zakresem problem podczas kopiowania z tooan bazie danych dokumentów lokalnego programu SQL Server z funkcją idempotency.</span><span class="sxs-lookup"><span data-stu-id="43c9e-123">Fixed: Index out of range issue while copying from Document DB tooan on-premises SQL Server with idempotency feature.</span></span>
-   <span data-ttu-id="43c9e-124">Stały: Skrypt czyszczący SQL nie działa z lokalnym programem SQL Server z Kreatora kopiowania.</span><span class="sxs-lookup"><span data-stu-id="43c9e-124">Fixed: SQL cleanup script doesn't work with on-premises SQL Server from Copy Wizard.</span></span>
-   <span data-ttu-id="43c9e-125">Stały: Nazwa kolumny z miejsca na końcu hello nie działa w przypadku działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="43c9e-125">Fixed: Column name with space at hello end does not work in copy activity.</span></span>

## <a name="28662833"></a><span data-ttu-id="43c9e-126">2.8.66283.3</span><span class="sxs-lookup"><span data-stu-id="43c9e-126">2.8.66283.3</span></span>
### <a name="enhancements-"></a><span data-ttu-id="43c9e-127">Ulepszenia-</span><span class="sxs-lookup"><span data-stu-id="43c9e-127">Enhancements-</span></span>
- <span data-ttu-id="43c9e-128">Rozwiązany: Problem z brakującymi poświadczeń na ponowny rozruch maszyny bramy.</span><span class="sxs-lookup"><span data-stu-id="43c9e-128">Fixed: Issue with missing credentials on gateway machine reboot.</span></span>
- <span data-ttu-id="43c9e-129">Stały: Problem z rejestracją podczas bramy przywracania przy użyciu pliku kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="43c9e-129">Fixed: Issue with registration during gateway restore using a backup file.</span></span>


## <a name="2762401"></a><span data-ttu-id="43c9e-130">2.7.6240.1</span><span class="sxs-lookup"><span data-stu-id="43c9e-130">2.7.6240.1</span></span>
### <a name="enhancements-"></a><span data-ttu-id="43c9e-131">Ulepszenia-</span><span class="sxs-lookup"><span data-stu-id="43c9e-131">Enhancements-</span></span>
- <span data-ttu-id="43c9e-132">Stały: Niepoprawna odczytu dziesiętne wartości null z bazy danych Oracle jako źródło.</span><span class="sxs-lookup"><span data-stu-id="43c9e-132">Fixed: Incorrect read of Decimal null value from Oracle as source.</span></span>

## <a name="2661922"></a><span data-ttu-id="43c9e-133">2.6.6192.2</span><span class="sxs-lookup"><span data-stu-id="43c9e-133">2.6.6192.2</span></span>
### <a name="whats-new"></a><span data-ttu-id="43c9e-134">Co nowego</span><span class="sxs-lookup"><span data-stu-id="43c9e-134">What’s new</span></span>
- <span data-ttu-id="43c9e-135">Klienci mogą wyrazić swoją opinię na rejestrowanie obsługi bramy.</span><span class="sxs-lookup"><span data-stu-id="43c9e-135">Customers can provide feedback on gateway registering experience.</span></span>
- <span data-ttu-id="43c9e-136">Obsługuje nowy format kompresji: ZIP (Deflate)</span><span class="sxs-lookup"><span data-stu-id="43c9e-136">Support a new compression format: ZIP (Deflate)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="43c9e-137">Ulepszenia-</span><span class="sxs-lookup"><span data-stu-id="43c9e-137">Enhancements-</span></span>
- <span data-ttu-id="43c9e-138">Zwiększenie wydajności dla Oracle Sink źródłowy system plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="43c9e-138">Performance improvement for Oracle Sink, HDFS source.</span></span>
- <span data-ttu-id="43c9e-139">Poprawka błędu dla bramy automatycznie zaktualizować bramy wydajności przetwarzania równoległego.</span><span class="sxs-lookup"><span data-stu-id="43c9e-139">Bug fix for gateway auto update, gateway parallel processing capacity.</span></span>


## <a name="2561641"></a><span data-ttu-id="43c9e-140">2.5.6164.1</span><span class="sxs-lookup"><span data-stu-id="43c9e-140">2.5.6164.1</span></span>
### <a name="enhancements"></a><span data-ttu-id="43c9e-141">Ulepszenia</span><span class="sxs-lookup"><span data-stu-id="43c9e-141">Enhancements</span></span>
- <span data-ttu-id="43c9e-142">Ulepszone bardziej niezawodne i bramy rejestracji środowisko — teraz można śledzić postęp całej procedury podczas procesu rejestracji bramy hello, dzięki czemu usprawnia rejestracji hello wystąpić.</span><span class="sxs-lookup"><span data-stu-id="43c9e-142">Improved and more robust Gateway registration experience- Now you can track progress status during hello Gateway registration process, which makes hello registration experience more responsive.</span></span>
- <span data-ttu-id="43c9e-143">Poprawy bramy przywrócić procesu — możesz można jednak nadal odzyskać bramy, nawet jeśli nie masz plik kopii zapasowej hello bramy z tej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="43c9e-143">Improvement in Gateway Restore Process- You can still recover gateway even if you do not have hello gateway backup file with this update.</span></span> <span data-ttu-id="43c9e-144">To wymagałyby tooreset połączonej usługi poświadczeń w portalu.</span><span class="sxs-lookup"><span data-stu-id="43c9e-144">This would require you tooreset Linked Service credentials in Portal.</span></span>
- <span data-ttu-id="43c9e-145">Poprawka błędu.</span><span class="sxs-lookup"><span data-stu-id="43c9e-145">Bug fix.</span></span>

## <a name="2461511"></a><span data-ttu-id="43c9e-146">2.4.6151.1</span><span class="sxs-lookup"><span data-stu-id="43c9e-146">2.4.6151.1</span></span>

### <a name="whats-new"></a><span data-ttu-id="43c9e-147">Co nowego</span><span class="sxs-lookup"><span data-stu-id="43c9e-147">What’s new</span></span>

- <span data-ttu-id="43c9e-148">Teraz można przechowywać lokalnie poświadczenia źródła danych.</span><span class="sxs-lookup"><span data-stu-id="43c9e-148">You can now store data source credentials locally.</span></span> <span data-ttu-id="43c9e-149">Witaj poświadczenia są szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="43c9e-149">hello credentials are encrypted.</span></span> <span data-ttu-id="43c9e-150">poświadczenia źródła danych Hello mogą zostać odzyskane i przywrócony przy użyciu hello plik kopii zapasowej można eksportować z hello istniejącej bramy, wszystkie dostępne lokalnie.</span><span class="sxs-lookup"><span data-stu-id="43c9e-150">hello data source credentials can be recovered and restored using hello backup file that can be exported from hello existing Gateway, all on-premises.</span></span>

### <a name="enhancements-"></a><span data-ttu-id="43c9e-151">Ulepszenia-</span><span class="sxs-lookup"><span data-stu-id="43c9e-151">Enhancements-</span></span>

- <span data-ttu-id="43c9e-152">Ulepszone i bardziej niezawodne środowisko rejestracji bramy.</span><span class="sxs-lookup"><span data-stu-id="43c9e-152">Improved and more robust Gateway registration experience.</span></span>
- <span data-ttu-id="43c9e-153">Obsługuje automatyczne wykrywanie QuoteChar Konfiguracja formatu tekstu w kreatorze kopiowania i ulepszania hello ogólny format dokładność wykrywania.</span><span class="sxs-lookup"><span data-stu-id="43c9e-153">Support auto detection of QuoteChar configuration for Text format in copy wizard, and improve hello overall format detection accuracy.</span></span>

## <a name="2361002"></a><span data-ttu-id="43c9e-154">2.3.6100.2</span><span class="sxs-lookup"><span data-stu-id="43c9e-154">2.3.6100.2</span></span>

- <span data-ttu-id="43c9e-155">Obsługuje firstRowAsHeader i SkipLineCount automatyczne wykrywanie w kreatorze kopiowania plików tekstowych w lokalnym systemie plików i system plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="43c9e-155">Support firstRowAsHeader and SkipLineCount auto detection in copy wizard for text files in on-premises File system and HDFS.</span></span>
- <span data-ttu-id="43c9e-156">Poprawić stabilność hello połączenie sieciowe między bramą i usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="43c9e-156">Enhance hello stability of network connection between gateway and Service Bus</span></span>
- <span data-ttu-id="43c9e-157">Kilka poprawek błędów</span><span class="sxs-lookup"><span data-stu-id="43c9e-157">A few bug fixes</span></span>


## <a name="2260721"></a><span data-ttu-id="43c9e-158">2.2.6072.1</span><span class="sxs-lookup"><span data-stu-id="43c9e-158">2.2.6072.1</span></span>

*  <span data-ttu-id="43c9e-159">Obsługuje ustawienie serwera proxy HTTP dla bramy hello przy użyciu hello Menedżera konfiguracji bramy.</span><span class="sxs-lookup"><span data-stu-id="43c9e-159">Supports setting HTTP proxy for hello gateway using hello Gateway Configuration Manager.</span></span> <span data-ttu-id="43c9e-160">Jeśli skonfigurowana, obiektów Blob platformy Azure, tabel Azure, usługa Azure Data Lake i bazie danych dokumentów są dostępne za pośrednictwem serwera proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="43c9e-160">If configured, Azure Blob, Azure Table, Azure Data Lake, and Document DB are accessed through HTTP proxy.</span></span>
*  <span data-ttu-id="43c9e-161">Nagłówek obsługuje obsługi TextFormat podczas kopiowania danych z / tooAzure obiektu Blob Azure Data Lake Store, lokalnego systemu plików i lokalnego systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="43c9e-161">Supports header handling for TextFormat when copying data from/tooAzure Blob, Azure Data Lake Store, on-premises File System, and on-premises HDFS.</span></span>
*  <span data-ttu-id="43c9e-162">Kopiowanie danych z Dołącz obiektów Blob i stronicowych obiektów Blob oraz hello już obsługuje obsługiwane blokowych obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="43c9e-162">Supports copying data from Append Blob and Page Blob along with hello already supported Block Blob.</span></span>
*  <span data-ttu-id="43c9e-163">Wprowadzono nowy stan bramy **Online (ograniczony)**, co oznacza funkcja main hello hello bramy działa z wyjątkiem hello interakcyjne operacji obsługę kreatora kopiowania.</span><span class="sxs-lookup"><span data-stu-id="43c9e-163">Introduces a new gateway status **Online (Limited)**, which indicates that hello main functionality of hello gateway works except hello interactive operation support for Copy Wizard.</span></span>
*  <span data-ttu-id="43c9e-164">Zwiększa niezawodność hello rejestracji bramy przy użyciu klucza rejestracji.</span><span class="sxs-lookup"><span data-stu-id="43c9e-164">Enhances hello robustness of gateway registration using registration key.</span></span>

## <a name="216040"></a><span data-ttu-id="43c9e-165">2.1.6040.</span><span class="sxs-lookup"><span data-stu-id="43c9e-165">2.1.6040.</span></span>

*  <span data-ttu-id="43c9e-166">Sterownik bazy danych DB2 znajduje się w pakiet instalacyjny bramy hello teraz.</span><span class="sxs-lookup"><span data-stu-id="43c9e-166">DB2 driver is included in hello gateway installation package now.</span></span> <span data-ttu-id="43c9e-167">Nie trzeba tooinstall go osobno.</span><span class="sxs-lookup"><span data-stu-id="43c9e-167">You do not need tooinstall it separately.</span></span>
*  <span data-ttu-id="43c9e-168">Sterownik bazy danych DB2 obsługuje teraz z/OS i bazy danych DB2 dla i (AS / 400) wraz z platform hello już obsługiwane (Linux, Unix i z systemem Windows).</span><span class="sxs-lookup"><span data-stu-id="43c9e-168">DB2 driver now supports z/OS and DB2 for i (AS/400) along with hello platforms already supported (Linux, Unix, and Windows).</span></span>
*  <span data-ttu-id="43c9e-169">Umożliwia używanie bazy danych rozwiązania Cosmos Azure jako źródła lub miejsca docelowego dla lokalnych magazynów danych</span><span class="sxs-lookup"><span data-stu-id="43c9e-169">Supports using Azure Cosmos DB as a source or destination for on-premises data stores</span></span>
*  <span data-ttu-id="43c9e-170">Kopiowanie danych z/toocold/hot magazynu obiektów blob oraz hello już obsługuje obsługiwane konta magazynu ogólnego przeznaczenia.</span><span class="sxs-lookup"><span data-stu-id="43c9e-170">Supports copying data from/toocold/hot blob storage along with hello already supported general-purpose storage account.</span></span>
*  <span data-ttu-id="43c9e-171">Pozwala tooconnect tooon lokalnego programu SQL Server za pośrednictwem bramy z uprawnieniami logowania zdalnego.</span><span class="sxs-lookup"><span data-stu-id="43c9e-171">Allows you tooconnect tooon-premises SQL Server via gateway with remote login privileges.</span></span>  

## <a name="2060131"></a><span data-ttu-id="43c9e-172">2.0.6013.1</span><span class="sxs-lookup"><span data-stu-id="43c9e-172">2.0.6013.1</span></span>

*  <span data-ttu-id="43c9e-173">Możesz wybrać toobe języka i kultury hello używany przez bramę podczas instalacji ręcznej.</span><span class="sxs-lookup"><span data-stu-id="43c9e-173">You can select hello language/culture toobe used by a gateway during manual installation.</span></span>

*  <span data-ttu-id="43c9e-174">Brama nie działa zgodnie z oczekiwaniami, możesz toosend dzienniki bramy z ostatnich siedmiu dni tooMicrosoft toofacilitate rozwiązywania problemów z hello problem.</span><span class="sxs-lookup"><span data-stu-id="43c9e-174">When gateway does not work as expected, you can choose toosend gateway logs of last seven days tooMicrosoft toofacilitate troubleshooting of hello issue.</span></span> <span data-ttu-id="43c9e-175">Jeśli brama nie jest podłączony toohello usługi w chmurze, można wybrać toosave oraz archiwum dzienniki bramy.</span><span class="sxs-lookup"><span data-stu-id="43c9e-175">If gateway is not connected toohello cloud service, you can choose toosave and archive gateway logs.</span></span>  

*  <span data-ttu-id="43c9e-176">Ulepszenia interfejsu użytkownika dla Menedżera konfiguracji bramy:</span><span class="sxs-lookup"><span data-stu-id="43c9e-176">User interface improvements for gateway configuration manager:</span></span>

    *  <span data-ttu-id="43c9e-177">Wyświetlaj stan bramy więcej na karcie Strona główna hello.</span><span class="sxs-lookup"><span data-stu-id="43c9e-177">Make gateway status more visible on hello Home tab.</span></span>

    *  <span data-ttu-id="43c9e-178">Formanty reorganizowane po kolei i uproszczone.</span><span class="sxs-lookup"><span data-stu-id="43c9e-178">Reorganized and simplified controls.</span></span>

    *  <span data-ttu-id="43c9e-179">Można skopiować danych z magazynu przy użyciu hello [narzędzia Podgląd niekorzystające z kodu kopiowania](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="43c9e-179">You can copy data from a storage using hello [code-free copy preview tool](data-factory-copy-data-wizard-tutorial.md).</span></span> <span data-ttu-id="43c9e-180">Zobacz [przemieszczane kopiowania](data-factory-copy-activity-performance.md#staged-copy) szczegółowe informacje o tej funkcji w zasadzie.</span><span class="sxs-lookup"><span data-stu-id="43c9e-180">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details about this feature in general.</span></span>
*  <span data-ttu-id="43c9e-181">Brama zarządzania danymi tooingress dane bezpośrednio z lokalną bazą danych programu SQL Server można użyć do usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="43c9e-181">You can use Data Management Gateway tooingress data directly from an on-premises SQL Server database into Azure Machine Learning.</span></span>

*  <span data-ttu-id="43c9e-182">Ulepszenia wydajności</span><span class="sxs-lookup"><span data-stu-id="43c9e-182">Performance improvements</span></span>

    * <span data-ttu-id="43c9e-183">Zwiększyć wydajność o wyświetlaniu schematu/Preview dla programu SQL Server w narzędziu Podgląd kopiowania niekorzystające z kodu.</span><span class="sxs-lookup"><span data-stu-id="43c9e-183">Improve performance on viewing Schema/Preview against SQL Server in code-free copy preview tool.</span></span>

## <a name="11259531"></a><span data-ttu-id="43c9e-184">1.12.5953.1</span><span class="sxs-lookup"><span data-stu-id="43c9e-184">1.12.5953.1</span></span>

*  <span data-ttu-id="43c9e-185">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="43c9e-185">Bug fixes</span></span>

## <a name="11159181"></a><span data-ttu-id="43c9e-186">1.11.5918.1</span><span class="sxs-lookup"><span data-stu-id="43c9e-186">1.11.5918.1</span></span>

*  <span data-ttu-id="43c9e-187">Maksymalny rozmiar hello w dzienniku zdarzeń bramy został zwiększony rozmiar od 1 MB too40 MB.</span><span class="sxs-lookup"><span data-stu-id="43c9e-187">Maximum size of hello gateway event log has been increased from 1 MB too40 MB.</span></span>

*  <span data-ttu-id="43c9e-188">Okno dialogowe ostrzeżenia jest wyświetlany w przypadku, gdy wymagane jest ponowne uruchomienie podczas automatyczną aktualizację bramy.</span><span class="sxs-lookup"><span data-stu-id="43c9e-188">A warning dialog is displayed in case a restart is needed during gateway auto-update.</span></span> <span data-ttu-id="43c9e-189">Prawo toorestart można następnie lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="43c9e-189">You can choose toorestart right then or later.</span></span>

*  <span data-ttu-id="43c9e-190">W przypadku, gdy aktualizacje automatyczne nie powiedzie się, Instalator bramy ponowi próbę automatycznego aktualizowania maksymalnie trzy razy w.</span><span class="sxs-lookup"><span data-stu-id="43c9e-190">In case auto-update fails, gateway installer retries auto-updating three times at maximum.</span></span>

*  <span data-ttu-id="43c9e-191">Ulepszenia wydajności</span><span class="sxs-lookup"><span data-stu-id="43c9e-191">Performance improvements</span></span>

    * <span data-ttu-id="43c9e-192">Zwiększenia wydajności w przypadku ładowania dużych tabel z lokalnego serwera w scenariuszu kopiowania niekorzystające z kodu.</span><span class="sxs-lookup"><span data-stu-id="43c9e-192">Improve performance for loading large tables from on-premises server in code-free copy scenario.</span></span>

*  <span data-ttu-id="43c9e-193">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="43c9e-193">Bug fixes</span></span>

## <a name="11058921"></a><span data-ttu-id="43c9e-194">1.10.5892.1</span><span class="sxs-lookup"><span data-stu-id="43c9e-194">1.10.5892.1</span></span>

*  <span data-ttu-id="43c9e-195">Ulepszenia wydajności</span><span class="sxs-lookup"><span data-stu-id="43c9e-195">Performance improvements</span></span>

*  <span data-ttu-id="43c9e-196">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="43c9e-196">Bug fixes</span></span>

## <a name="1958652"></a><span data-ttu-id="43c9e-197">1.9.5865.2</span><span class="sxs-lookup"><span data-stu-id="43c9e-197">1.9.5865.2</span></span>

*  <span data-ttu-id="43c9e-198">Zero touch automatycznej aktualizacji możliwości</span><span class="sxs-lookup"><span data-stu-id="43c9e-198">Zero touch auto update capability</span></span>
*  <span data-ttu-id="43c9e-199">Nowa ikona na pasku zadań z wskaźniki stanu bramy</span><span class="sxs-lookup"><span data-stu-id="43c9e-199">New tray icon with gateway status indicators</span></span>
*  <span data-ttu-id="43c9e-200">Możliwość zbyt "Aktualizuj" z powitania klienta</span><span class="sxs-lookup"><span data-stu-id="43c9e-200">Ability too“Update now” from hello client</span></span>
*  <span data-ttu-id="43c9e-201">Możliwość tooset aktualizacji zaplanowany termin</span><span class="sxs-lookup"><span data-stu-id="43c9e-201">Ability tooset update schedule time</span></span>
*  <span data-ttu-id="43c9e-202">Skrypt programu PowerShell dla automatycznej aktualizacji lub wyłącza przełączanie</span><span class="sxs-lookup"><span data-stu-id="43c9e-202">PowerShell script for toggling auto-update on/off</span></span>
*  <span data-ttu-id="43c9e-203">Obsługa formatu JSON</span><span class="sxs-lookup"><span data-stu-id="43c9e-203">Support for JSON format</span></span>  
*  <span data-ttu-id="43c9e-204">Ulepszenia wydajności</span><span class="sxs-lookup"><span data-stu-id="43c9e-204">Performance improvements</span></span>
*  <span data-ttu-id="43c9e-205">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="43c9e-205">Bug fixes</span></span>

## <a name="1858221"></a><span data-ttu-id="43c9e-206">1.8.5822.1</span><span class="sxs-lookup"><span data-stu-id="43c9e-206">1.8.5822.1</span></span>

*  <span data-ttu-id="43c9e-207">Udoskonalanie rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="43c9e-207">Improve troubleshooting experience</span></span>
*  <span data-ttu-id="43c9e-208">Ulepszenia wydajności</span><span class="sxs-lookup"><span data-stu-id="43c9e-208">Performance improvements</span></span>
*  <span data-ttu-id="43c9e-209">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="43c9e-209">Bug fixes</span></span>

### <a name="1757951"></a><span data-ttu-id="43c9e-210">1.7.5795.1</span><span class="sxs-lookup"><span data-stu-id="43c9e-210">1.7.5795.1</span></span>

*  <span data-ttu-id="43c9e-211">Ulepszenia wydajności</span><span class="sxs-lookup"><span data-stu-id="43c9e-211">Performance improvements</span></span>
*  <span data-ttu-id="43c9e-212">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="43c9e-212">Bug fixes</span></span>

### <a name="1757641"></a><span data-ttu-id="43c9e-213">1.7.5764.1</span><span class="sxs-lookup"><span data-stu-id="43c9e-213">1.7.5764.1</span></span>

*  <span data-ttu-id="43c9e-214">Ulepszenia wydajności</span><span class="sxs-lookup"><span data-stu-id="43c9e-214">Performance improvements</span></span>
*  <span data-ttu-id="43c9e-215">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="43c9e-215">Bug fixes</span></span>

### <a name="1657351"></a><span data-ttu-id="43c9e-216">1.6.5735.1</span><span class="sxs-lookup"><span data-stu-id="43c9e-216">1.6.5735.1</span></span>

*  <span data-ttu-id="43c9e-217">Obsługa lokalnego systemu plików HDFS źródło/ujście</span><span class="sxs-lookup"><span data-stu-id="43c9e-217">Support on-premises HDFS Source/Sink</span></span>
*  <span data-ttu-id="43c9e-218">Ulepszenia wydajności</span><span class="sxs-lookup"><span data-stu-id="43c9e-218">Performance improvements</span></span>
*  <span data-ttu-id="43c9e-219">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="43c9e-219">Bug fixes</span></span>

### <a name="1656961"></a><span data-ttu-id="43c9e-220">1.6.5696.1</span><span class="sxs-lookup"><span data-stu-id="43c9e-220">1.6.5696.1</span></span>

*  <span data-ttu-id="43c9e-221">Ulepszenia wydajności</span><span class="sxs-lookup"><span data-stu-id="43c9e-221">Performance improvements</span></span>
*  <span data-ttu-id="43c9e-222">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="43c9e-222">Bug fixes</span></span>

### <a name="1656761"></a><span data-ttu-id="43c9e-223">1.6.5676.1</span><span class="sxs-lookup"><span data-stu-id="43c9e-223">1.6.5676.1</span></span>

*  <span data-ttu-id="43c9e-224">Narzędzia diagnostyczne pomocy technicznej programu Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="43c9e-224">Support diagnostic tools on Configuration Manager</span></span>
*  <span data-ttu-id="43c9e-225">Kolumny tabeli pomocy technicznej dla źródeł danych tabelarycznych dla fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="43c9e-225">Support table columns for tabular data sources for Azure Data Factory</span></span>
*  <span data-ttu-id="43c9e-226">Obsługa magazynu danych SQL dla fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="43c9e-226">Support SQL DW for Azure Data Factory</span></span>
*  <span data-ttu-id="43c9e-227">Obsługa Reclusive BlobSource i FileSource fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="43c9e-227">Support Reclusive in BlobSource and FileSource for Azure Data Factory</span></span>
*  <span data-ttu-id="43c9e-228">Obsługa CopyBehavior — MergeFiles, PreserveHierarchy i FlattenHierarchy w BlobSink i FileSink kopią binarne dla fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="43c9e-228">Support CopyBehavior – MergeFiles, PreserveHierarchy, and FlattenHierarchy in BlobSink and FileSink with Binary Copy for Azure Data Factory</span></span>
*  <span data-ttu-id="43c9e-229">Obsługuje działanie kopiowania raportowania postępu dla fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="43c9e-229">Support Copy Activity reporting progress for Azure Data Factory</span></span>
*  <span data-ttu-id="43c9e-230">Walidacja łączności źródła danych pomocy technicznej dla fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="43c9e-230">Support Data Source Connectivity Validation for Azure Data Factory</span></span>
*  <span data-ttu-id="43c9e-231">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="43c9e-231">Bug fixes</span></span>

### <a name="1656721"></a><span data-ttu-id="43c9e-232">1.6.5672.1</span><span class="sxs-lookup"><span data-stu-id="43c9e-232">1.6.5672.1</span></span>

*  <span data-ttu-id="43c9e-233">Nazwa tabeli pomocy technicznej dla źródła danych ODBC dla fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="43c9e-233">Support table name for ODBC data source for Azure Data Factory</span></span>
*  <span data-ttu-id="43c9e-234">Ulepszenia wydajności</span><span class="sxs-lookup"><span data-stu-id="43c9e-234">Performance improvements</span></span>
*  <span data-ttu-id="43c9e-235">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="43c9e-235">Bug fixes</span></span>

### <a name="1656581"></a><span data-ttu-id="43c9e-236">1.6.5658.1</span><span class="sxs-lookup"><span data-stu-id="43c9e-236">1.6.5658.1</span></span>

*  <span data-ttu-id="43c9e-237">Plik pomocy technicznej Sink dla fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="43c9e-237">Support File Sink for Azure Data Factory</span></span>
*  <span data-ttu-id="43c9e-238">Obsługa zachowania hierarchii kopii binarne dla fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="43c9e-238">Support preserving hierarchy in binary copy for Azure Data Factory</span></span>
*  <span data-ttu-id="43c9e-239">Obsługuje Idempotency działania kopiowania dla fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="43c9e-239">Support Copy Activity Idempotency for Azure Data Factory</span></span>
*  <span data-ttu-id="43c9e-240">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="43c9e-240">Bug fixes</span></span>

### <a name="1656401"></a><span data-ttu-id="43c9e-241">1.6.5640.1</span><span class="sxs-lookup"><span data-stu-id="43c9e-241">1.6.5640.1</span></span>

*  <span data-ttu-id="43c9e-242">Obsługa 3 więcej źródeł danych dla fabryki danych Azure (ODBC, OData, system plików HDFS)</span><span class="sxs-lookup"><span data-stu-id="43c9e-242">Support 3 more data sources for Azure Data Factory (ODBC, OData, HDFS)</span></span>
*  <span data-ttu-id="43c9e-243">Obsługa znaku cudzysłowu w analizatorze składni csv fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="43c9e-243">Support quote character in csv parser for Azure Data Factory</span></span>
*  <span data-ttu-id="43c9e-244">Obsługa kompresji (BZip2)</span><span class="sxs-lookup"><span data-stu-id="43c9e-244">Compression support (BZip2)</span></span>
*  <span data-ttu-id="43c9e-245">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="43c9e-245">Bug fixes</span></span>

### <a name="1556121"></a><span data-ttu-id="43c9e-246">1.5.5612.1</span><span class="sxs-lookup"><span data-stu-id="43c9e-246">1.5.5612.1</span></span>

*  <span data-ttu-id="43c9e-247">Obsługuje pięć relacyjnych baz danych dla fabryki danych Azure (MySQL, PostgreSQL bazy danych DB2, Teradata i Sybase)</span><span class="sxs-lookup"><span data-stu-id="43c9e-247">Support five relational databases for Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata, and Sybase)</span></span>
*  <span data-ttu-id="43c9e-248">Obsługa kompresji (Gzip i Deflate)</span><span class="sxs-lookup"><span data-stu-id="43c9e-248">Compression support (Gzip and Deflate)</span></span>
*  <span data-ttu-id="43c9e-249">Ulepszenia wydajności</span><span class="sxs-lookup"><span data-stu-id="43c9e-249">Performance improvements</span></span>
*  <span data-ttu-id="43c9e-250">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="43c9e-250">Bug fixes</span></span>

### <a name="1455491"></a><span data-ttu-id="43c9e-251">1.4.5549.1</span><span class="sxs-lookup"><span data-stu-id="43c9e-251">1.4.5549.1</span></span>

*  <span data-ttu-id="43c9e-252">Dodaj obsługę źródła danych programu Oracle dla fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="43c9e-252">Add Oracle data source support for Azure Data Factory</span></span>
*  <span data-ttu-id="43c9e-253">Ulepszenia wydajności</span><span class="sxs-lookup"><span data-stu-id="43c9e-253">Performance improvements</span></span>
*  <span data-ttu-id="43c9e-254">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="43c9e-254">Bug fixes</span></span>

### <a name="1454921"></a><span data-ttu-id="43c9e-255">1.4.5492.1</span><span class="sxs-lookup"><span data-stu-id="43c9e-255">1.4.5492.1</span></span>

*  <span data-ttu-id="43c9e-256">Ujednolicone pliku binarnego, który obsługuje zarówno fabryki danych Microsoft Azure i usługi Office 365 Power BI</span><span class="sxs-lookup"><span data-stu-id="43c9e-256">Unified binary that supports both Microsoft Azure Data Factory and Office 365 Power BI services</span></span>
*  <span data-ttu-id="43c9e-257">Dostosuj hello procesu interfejsu użytkownika konfiguracji i rejestracji</span><span class="sxs-lookup"><span data-stu-id="43c9e-257">Refine hello Configuration UI and registration process</span></span>
*  <span data-ttu-id="43c9e-258">Fabryka danych Azure — przychodzące i wychodzące Azure obsługuje dla źródła danych programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="43c9e-258">Azure Data Factory – Azure Ingress and Egress support for SQL Server data source</span></span>

### <a name="1253031"></a><span data-ttu-id="43c9e-259">1.2.5303.1</span><span class="sxs-lookup"><span data-stu-id="43c9e-259">1.2.5303.1</span></span>

*  <span data-ttu-id="43c9e-260">Usuń limit czasu toosupport problem bardziej czasochłonnym połączeń ze źródłem danych.</span><span class="sxs-lookup"><span data-stu-id="43c9e-260">Fix timeout issue toosupport more time-consuming data source connections.</span></span>

### <a name="1155268"></a><span data-ttu-id="43c9e-261">1.1.5526.8</span><span class="sxs-lookup"><span data-stu-id="43c9e-261">1.1.5526.8</span></span>

*  <span data-ttu-id="43c9e-262">Instalator wymaga programu .NET Framework 4.5.1 jako warunek wstępny.</span><span class="sxs-lookup"><span data-stu-id="43c9e-262">Requires .NET Framework 4.5.1 as a prerequisite during setup.</span></span>

### <a name="1051442"></a><span data-ttu-id="43c9e-263">1.0.5144.2</span><span class="sxs-lookup"><span data-stu-id="43c9e-263">1.0.5144.2</span></span>

*  <span data-ttu-id="43c9e-264">Brak zmian, które mają wpływ na scenariusze fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="43c9e-264">No changes that affect Azure Data Factory scenarios.</span></span>
