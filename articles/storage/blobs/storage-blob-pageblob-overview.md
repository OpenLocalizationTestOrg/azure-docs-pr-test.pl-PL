---
title: "Rozwiązanie Azure stronicowych obiektów blob | Dokumentacja firmy Microsoft"
description: "Omówienie o Azure stronicowe, korzyści i przypadki użycia z przykładowe skrypty."
services: storage
documentationcenter: 
author: anasouma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2018
ms.author: wielriac
ms.openlocfilehash: 019b793f6d2b4cb70514d867b78c9501240baeda
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/23/2018
---
# <a name="unique-features-of-azure-page-blobs"></a>Unikatowe funkcje Azure stronicowych obiektów blob

Usługa Azure Storage udostępnia trzy typy magazynu obiektów blob: blokowe obiekty BLOB, Dołącz obiektów blob i stronicowe obiekty BLOB. Blokowych obiektów blob jest złożony z bloków i idealnie nadają się do przechowywania tekstu lub plików binarnych i efektywnie wysyłania dużych plików. Dołącz obiekty BLOB są również składają się z bloków, ale zoptymalizowane do operacji uzupełnialnych, nadawania idealne w scenariuszach logowania. Stronicowe obiekty BLOB składają się z 512-bajtowych stron do 8 TB w całkowity rozmiar i są bardziej wydajne operacjach częste losowego odczytu/zapisu. Stronicowe obiekty BLOB są foundation dysków IaaS platformy Azure. Ten artykuł dotyczy wyjaśniający, funkcje i korzyści stronicowych obiektów blob.

## <a name="overview"></a>Przegląd
Stronicowe obiekty BLOB są to zbiór stron 512-bajtowych, które oferują możliwość odczytu/zapisu dowolnego zakresów bajtów. W związku z tym stronicowe obiekty BLOB idealnie nadają się do przechowywania struktury opartego na indeksie i rozrzedzone danych, takich jak systemu operacyjnego i dysków z danymi dla maszyn wirtualnych i baz danych. Na przykład bazy danych SQL Azure używa stronicowych obiektów blob jako podstawowej magazynu trwałego dla jej baz danych. Ponadto stronicowe obiekty BLOB są również często używane dla plików z opartej na zakresie aktualizacji.  

Najważniejsze funkcje Azure stronicowe obiekty BLOB są interfejsie REST, trwałości powiązany magazyn oraz możliwości łatwego migracji na platformie Azure. Omówimy te funkcje bardziej szczegółowo w następnej sekcji. Ponadto Azure stronicowe obiekty BLOB są obecnie obsługiwane na dwa typy magazynu: Magazyn w warstwie Premium i standardowa magazynu. Magazyn w warstwie Premium jest zaprojektowany specjalnie z myślą obciążeń wymagających wysoką wydajność i małe opóźnienia wprowadzania premium stronicowe obiekty BLOB nadaje się doskonale dla bazy danych magazynu danych wysokiej wydajności.  Standard Storage jest bardziej ekonomiczne dla niezależnych od opóźnienia obciążeniami.

## <a name="sample-use-cases"></a>Przykładowe przypadki użycia

Omówimy kilka przypadków użycia stronicowych obiektów blob, począwszy od dysków IaaS platformy Azure. Obiekty BLOB platformy Azure strony stanowią szkielet platformy dyski wirtualne IaaS platformy Azure. Zarówno Azure systemu operacyjnego i dyski danych są zaimplementowane jako dyski wirtualne, których dane są trwale utrwalony na platformie Azure Storage i następnie dostarczany do maszyn wirtualnych o maksymalnej wydajności. Dyskach platformy Azure są zachowywane w funkcji Hyper-V [formatu wirtualnego dysku twardego](https://technet.microsoft.com/library/dd979539.aspx) i przechowywane jako [stronicowych obiektów Blob](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs#about-page-blobs) w usłudze Azure Storage. Oprócz dla maszyn wirtualnych IaaS platformy Azure przy użyciu dysków wirtualnych, stronicowe obiekty BLOB również włączyć PaaS i DBaaS scenariuszy, takich jak usługa bazy danych SQL Azure, która aktualnie używa stronicowych obiektów blob do przechowywania danych SQL, umożliwiające szybkie losowe operacje odczytu i zapisu bazy danych. Innym przykładem może być, jeśli masz usługę PaaS udostępnianie multimediów dostępu dla aplikacji do edycji wideo współpracy stronicowe obiekty BLOB Włącz szybki dostęp do losowe lokalizacji na nośniku. Umożliwia również szybkie i wydajne edytowanie i scalanie z tego samego nośnika przez wielu użytkowników. 

Najpierw strony usług firmy Microsoft, takich jak usługi Azure Site Recovery, kopia zapasowa Azure, a także wiele innych firm deweloperzy zostały zaimplementowane innowacje branży przy użyciu interfejsu REST stronicowych obiektów blob. Poniżej przedstawiono niektóre scenariusze unikatowy zaimplementowana na platformie Azure: 
* Zarządzanie skierowane do aplikacji przyrostowe migawki: aplikacje mogą korzystać z migawki obiektu Blob strony i interfejsów API REST do zapisywania aplikacji punkty kontrolne bez ponoszenia kosztowne zduplikowanie danych. Jest to możliwe, ponieważ firma Microsoft obsługuje stronicowych obiektów blob, które nie wymagają Kopiowanie całego danych migawki lokalne. Te migawki publicznych interfejsów API również włączyć dostęp do i kopiowanie delty między migawki.
* Migracja aplikacji i danych z lokalnych do chmury na żywo: kopiowania danych lokalnych i zapisać bezpośrednio do usługi Azure stronicowych obiektów Blob, gdy lokalnego maszyna wirtualna jest nadal uruchomiona za pomocą interfejsów API REST. Gdy element docelowy ma zawiera, można szybko tryb failover maszyny Wirtualnej platformy Azure przy użyciu tych danych. Dzięki temu migracji maszyn wirtualnych i wirtualnych dysków ze środowiska lokalnego do chmury z minimalnym czasem przestojów, ponieważ migracja danych przebiega w tle nadal używać maszyny Wirtualnej i przestoju potrzebnych do pracy awaryjnej będzie krótkich (w minutach).
* [Opartego na SAS](../common/storage-dotnet-shared-access-signature-part-1.md) udostępnionego dostępu, co umożliwia obsługę scenariuszy takich jak czytniki wielu i jednego składnika zapisywania z obsługą do sterowania współbieżnością.

## <a name="page-blob-features"></a>Funkcje stronicowych obiektów Blob

### <a name="rest-api"></a>Interfejs API REST
Zapoznaj się z następującym dokumencie, aby zacząć korzystać z [tworzenie przy użyciu stronicowe obiekty BLOB](storage-dotnet-how-to-use-blobs.md). Na przykład Daj nam Zobacz, jak dostęp stronicowych obiektów blob za pomocą biblioteki klienta usługi Storage dla platformy .NET. 

Na poniższym diagramie przedstawiono ogólny relacje między konta, kontenery i stronicowe obiekty BLOB.

![](./media/storage-blob-pageblob-overview/storage-blob-pageblob-overview-figure1.png)

#### <a name="creating-an-empty-page-blob-of-a-certain-size"></a>Tworzenie pustego obiektu Blob strony o określonym rozmiarze
Aby utworzyć stronicowych obiektów Blob, najpierw utworzymy obiektu CloudBlobClient z podstawowy identyfikator Uri do uzyskiwania dostępu do magazynu obiektów blob dla konta magazynu (pbaccount na rys. 1) wraz z obiektem StorageCredentialsAccountAndKey, jak pokazano poniżej.  W przykładzie pokazano następnie tworzenie odwołania do obiektu CloudBlobContainer, a następnie utworzenie kontenera (testvhds), jeśli jeszcze nie istnieje.  Następnie przy użyciu obiektu CloudBlobContainer można utworzyć odwołanie do obiektu CloudPageBlob, określając nazwę obiektu blob strony (os4.vhd) chcemy, aby uzyskać dostęp. Następnie można utworzyć obiektu blob strony nazywamy [CloudPageBlob.Create](/dotnet/api/microsoft.windowsazure.storage.blob.cloudpageblob.create?view=azure-dotnet#Microsoft_WindowsAzure_Storage_Blob_CloudPageBlob_Create_System_Int64_Microsoft_WindowsAzure_Storage_AccessCondition_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_) przekazując maksymalny rozmiar obiektu blob chcemy utworzyć.  BlobSize musi być wielokrotnością 512 bajtów.

```csharp
using Microsoft.WindowsAzure.StorageClient;
long OneGigabyteAsBytes = 1024 * 1024 * 1024;
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("testvhds");

// Create the container if it doesn't already exist.
container.CreateIfNotExists();

CloudPageBlob pageBlob = container.GetPageBlobReference("os4.vhd");
pageBlob.Create(16 * OneGigabyteAsBytes);
```

#### <a name="resizing-a-page-blob"></a>Zmiana rozmiaru stronicowych obiektów Blob
Aby zmienić rozmiar obiektu Blob strony po utworzeniu, należy użyć [Resize](/dotnet/api/microsoft.windowsazure.storage.blob.cloudpageblob.resize?view=azure-dotnet#Microsoft_WindowsAzure_Storage_Blob_CloudPageBlob_Resize_System_Int64_Microsoft_WindowsAzure_Storage_AccessCondition_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_) interfejsu API. Żądany rozmiar powinna być wielokrotnością 512 bajtów.
```csharp
pageBlob.Resize(32 * OneGigabyteAsBytes); 
```

#### <a name="writing-pages-to-a-page-blob"></a>Tworzenie stron do obiektu Blob strony
Aby zapisać strony, należy użyć [CloudPageBlob.WritePages](/library/microsoft.windowsazure.storageclient.cloudpageblob.writepages.aspx) metody.  Umożliwia to pisanie sekwencyjnych zestaw stron do 4MBs. Przesunięcie zapisywana musi zaczynać się na granicy 512-bajtowe (startingOffset % 512 == 0) i na końcu na granicy 512 - 1.  Poniższy kod przedstawia przykład wywoływania WritePages dla obiekt blob, który firma Microsoft uzyskują dostęp do:
```csharp
pageBlob.WritePages(dataStream, startingOffset); 
```

Żądanie zapisu sekwencyjnego zestaw stron powiedzie się w usłudze obiektów blob, a jest replikowana na potrzeby trwałości i odporności, zapisu została zatwierdzona i Powodzenie jest zwracana do klienta.  

Poniżej przedstawiono diagram 2 osobne operacje zapisu:

![](./media/storage-blob-pageblob-overview/storage-blob-pageblob-overview-figure2.png)

1.  Operacja zapisu, zaczynając od przesunięcia 0 o długości 1024 bajty 
2.  Operacja zapisu, zaczynając od przesunięcia 4096 o długości 1024 

#### <a name="reading-pages-from-a-page-blob"></a>Odczytywanie stron z stronicowych obiektów Blob
Aby czytać strony, należy użyć [CloudPageBlob.DownloadRangeToByteArray](/dotnet/api/microsoft.windowsazure.storage.blob.icloudblob.downloadrangetobytearray?view=azure-dotnet) metody odczytać zakresu bajtów z stronicowych obiektów blob. Dzięki temu można pobrać pełnej obiektów blob lub zakresu bajtów, począwszy od dowolnego przesunięcie w obiekcie blob. Podczas odczytu, przesunięcie nie trzeba uruchomić na wielokrotnością 512. Podczas odczytywania bajtów ze strony NUL, usługa zwraca zero bajtów.
```csharp
byte[] buffer = new byte[rangeSize];
pageBlob.DownloadRangeToByteArray(buffer, bufferOffset, pageBlobOffset, rangeSize); 
```
Na poniższej ilustracji przedstawiono operacja odczytu z BlobOffSet 256 i rangeSize 4352. Dane zwrócone zostanie wyróżniona w kolorze pomarańczowym. Zera są zwracane w przypadku stron NUL

![](./media/storage-blob-pageblob-overview/storage-blob-pageblob-overview-figure3.png)

Jeśli masz słabo wypełnione obiektu blob można wystarczy pobrać regionów prawidłową stroną, aby uniknąć płatność za egressing zero bajtów i zmniejszenia opóźnień pobierania.  Aby określić, które strony są opartym na danych, użyj [CloudPageBlob.GetPageRanges](/dotnet/api/microsoft.windowsazure.storage.blob.cloudpageblob.getpageranges?view=azure-dotnet). Można wyliczyć zwrócony zakresy i pobierania danych z każdego zakresu. 
```csharp
IEnumerable<PageRange> pageRanges = pageBlob.GetPageRanges();

foreach (PageRange range in pageRanges)
{
    // Calculate the rangeSize
    int rangeSize = (int)(range.EndOffset + 1 - range.StartOffset);

    byte[] buffer = new byte[rangeSize];

    // Read from the correct starting offset in the page blob and place the data in the bufferOffset of the buffer byte array
    pageBlob.DownloadRangeToByteArray(buffer, bufferOffset, range.StartOffset, rangeSize); 

    // TODO: use the buffer for the page range just read
} 
```

#### <a name="leasing-a-page-blob"></a>Dzierżawa stronicowych obiektów Blob
Operacji obiektu Blob dzierżawy ustanawia i zarządza blokadą obiektu blob dla zapisu operacji i usuwania. Ta operacja jest bardzo przydatne w scenariuszach, w którym stronicowych obiektów blob jest uzyskiwany z wielu klientów, aby upewnić się, że tylko jeden klient może zapisywać do obiektu blob w czasie. Azure dysków, na przykład wykorzystuje to dzierżawa mechanizm upewnij się, że dysk zarządza tylko jednej maszyny Wirtualnej. Czas trwania blokady może być 15 do 60 sekund lub może być nieskończona. W dokumentacji [tutaj](/rest/api/storageservices/lease-blob) więcej szczegółów.

> Użyj następującego łącza można uzyskać [przykłady kodu](/resources/samples/?service=storage&term=blob&sort=0) w różnych scenariuszach aplikacji. 

Oprócz zaawansowanych interfejsów API REST stronicowych obiektów blob udostępniają dostępu współdzielonego, trwałości i zwiększonych zabezpieczeń. Omówimy tych korzyści bardziej szczegółowo w następnej akapitów. 

### <a name="concurrent-access"></a>Współbieżny dostęp
Dzierżawa jest interfejsu API REST obiekty BLOB strony i mechanizmu umożliwia aplikacjom dostęp do obiektu blob strony z wielu klientów. Załóżmy na przykład, że jest potrzebne do tworzenia usługi w chmurze rozproszonych, który współużytkuje magazyn obiektów z wielu użytkowników. Może to być aplikacji sieci web obsługująca duży zbiór obrazy na kilku użytkowników. Jedną z opcji to implementacja jest Maszynę wirtualną za pomocą dołączonych dysków. Downsides to między innymi (i) ograniczenia, że dysk może zostać dołączona tyko do jednej maszyny Wirtualnej, w związku z tym ograniczenie skalowalność, elastyczność i zwiększenie ryzyka. W przypadku problemu z maszyny Wirtualnej lub usługi uruchomione na maszynie Wirtualnej, następnie z powodu dzierżawy, obraz jest niedostępna do czasu dzierżawy wygaśnie lub jest uszkodzona; i (ii) dodatkowych kosztów o maszyn wirtualnych IaaS. 

Opcja alternatywna jest używa stronicowych obiektów blob bezpośrednio za pośrednictwem interfejsów API REST magazynu Azure. Ta opcja eliminuje potrzebę stosowania kosztowne maszyn wirtualnych IaaS, oferuje pełną elastyczność bezpośredni dostęp z wielu klientów, upraszcza zarządzanie usługami przez wyeliminowanie konieczności dołączania/odłączania dysków i eliminuje to ryzyko problemów na maszynie Wirtualnej. I zapewnia taki sam poziom wydajności dla operacji losowego odczytu/zapisu jako dysk

### <a name="durability-and-high-availability"></a>Trwałości i wysokiej dostępności
Zarówno warstwy standardowa i premium magazynu są trwałego magazynu, gdy dane obiektu blob strony są zawsze replikowane w celu zapewnienia trwałości i wysokiej dostępności. Aby uzyskać więcej informacji na temat nadmiarowość magazynu Azure, zobacz ten [dokumentacji](../common/storage-redundancy.md). Azure spójnie wydał trwałości korporacyjnej IaaS dyski i stronicowe, z branży ZERO % [firmie częstość niepowodzeń](https://en.wikipedia.org/wiki/Annualized_failure_rate). Oznacza to, że Azure nigdy nie utracił danych obiektu blob strony klienta. 

### <a name="seamless-migration-to-azure"></a>Bezproblemowe migracji na platformie Azure
Dla klientów i projektantów zainteresowanych wdrażanie własnych dostosowanych do tworzenia kopii zapasowych system Azure oferuje przyrostowe migawki, które może zawierać tylko. Ta funkcja pozwala uniknąć kosztów kopii początkowej pełne, co znacznie zmniejsza koszt tworzenia kopii zapasowej. Wraz z możliwością wydajnie odczytu i skopiuj dane różnicowe jest inny zaawansowaną możliwością, umożliwiającą jeszcze więcej innowacje deweloperów, co może prowadzić do najlepsze w klasie kopii zapasowych i odzyskiwaniem po awarii (DR) korzystanie z funkcji odzyskiwania na platformie Azure. Należy skonfigurować własne tworzenia kopii zapasowej lub rozwiązanie odzyskiwania po awarii dla maszyn wirtualnych przy użyciu usługi Azure [migawki obiektu Blob](/rest/api/storageservices/snapshot-blob) wraz z [zakresów stron Get](/rest/api/storageservices/get-page-ranges) interfejsu API i [przyrostowej kopii obiektu Blob](/rest/api/storageservices/incremental-copy-blob) interfejsu API, które można Użycie łatwo kopiowania danych pierwotnych do odzyskiwania po awarii. 

Ponadto w wielu przedsiębiorstwach istnieją krytycznych obciążeń już uruchomione w centrach danych lokalnych. Migracji obciążeń do chmury, jednym z głównych problemów będzie czas przestoju potrzebne do kopiowania danych i ryzyko nieprzewidzianych problemów po przełączenie. W wielu przypadkach Przestój może być showstopper do migracji do chmury. Przy użyciu interfejsu API REST obiekty BLOB strony, Azure rozwiązano ten problem, należy włączyć migracja do chmury przy minimalnych przerw w działaniu obciążeniom krytycznym. 

Przykłady sposobu wykonywania migawki i przywracanie z migawki stronicowych obiektów blob, można znaleźć na stronie [instalacji procesu tworzenia kopii zapasowej przy użyciu przyrostowej migawki](../../virtual-machines/windows/incremental-snapshots.md) artykułu.


## <a name="summary"></a>Podsumowanie
Azure dokłada starań, aby dostarczyć środowisko najlepsze w klasie dla naszych klientów. Budujemy platformy magazynu korporacyjnej trwałości danych, więc klientów można ufać Azure z ich kluczowych danych. System Azure oferuje unikatowy interfejsu API pomocy technicznej i deweloperów środowiska stronicowych obiektów blob, co może zapewnić nie platforma chmury publicznej. Spowodowało liczne innowacje 1 firm i firm 3rd jak migracje bezproblemowe chmury, środowisko wyższego poziomu kopii zapasowej i odzyskiwania po awarii, obsługa PaaS i DBaaS, systemów rozproszonych pamięci masowej i innymi technologiami pojawiającymi się dla dysków maszyn wirtualnych IaaS. Ogólnie Azure będą się wśród wszystkich platform chmury publicznej, dzięki takim funkcjom unikatowy i korzyści klientów platformy Azure z tych wartości dodaje zapewniają innych platform chmury.
