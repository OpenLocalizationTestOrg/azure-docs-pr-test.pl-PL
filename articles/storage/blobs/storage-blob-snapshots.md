---
title: "aaaCreate migawki tylko do odczytu obiektów blob w usłudze Azure Storage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate migawkę tooback obiektów blob, zapasową danych obiektów blob w danym momencie w czasie. Zrozumienie, jak migawki są rozliczane i jak toouse ich toominimize pojemności opłat."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 3710705d-e127-4b01-8d0f-29853fb06d0d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: marsma
ms.openlocfilehash: 57f2e76b8899b8a513688bf148dd13673141d5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-blob-snapshot"></a>Tworzenie migawki obiektu blob

Migawka jest tylko do odczytu wersji obiektu blob, która jest wykonywana w punkcie w czasie. Migawki są przydatne w przypadku tworzenia kopii zapasowej obiektów blob. Po utworzeniu migawki, odczytu, skopiuj lub usuń go, ale nie można go modyfikować.

Migawki obiektu blob jest identyczne tooits podstawowego obiektu blob, z wyjątkiem tego obiektu blob hello identyfikator URI ma **DateTime** wartość dołączona toohello obiektu blob identyfikatora URI tooindicate hello czas na które hello migawki. Na przykład jeśli identyfikator URI obiektu blob strony jest `http://storagesample.core.blob.windows.net/mydrives/myvhd`, hello migawki identyfikatora URI jest zbyt podobne`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.

> [!NOTE]
> Wszystkie migawki mają hello podstawowej przez identyfikator URI obiektu blob. Witaj różnicy między hello podstawowej obiektów blob i migawki hello jest dołączany hello tylko **DateTime** wartość.
>

Obiekt blob może mieć dowolną liczbę migawek. Migawki zachować, dopóki nie zostaną jawnie usunięte. Migawka nie outlive jego podstawowego obiektu blob. Można wyliczyć hello migawki skojarzone z hello tootrack podstawowego obiektu blob z bieżącej migawki.

Po utworzeniu migawki obiektu blob hello właściwości systemu obiektu blob są takie same wartości migawki toohello skopiowanych z hello. Metadane obiektu blob Hello podstawowy jest również skopiowanych toohello migawki, chyba że zostanie oddzielne metadanych dla hello migawki podczas jego tworzenia.

Wszystkie dzierżawy skojarzonego z obiektem blob podstawowej hello nie wpływają na powitania migawki. Nie można pobrać dzierżawy na migawki.

Plik VHD jest używane toostore hello aktualne informacje i stan dysku maszyny Wirtualnej. Można odłączyć dysku od wewnątrz hello maszyny Wirtualnej lub zamknąć hello maszyny Wirtualnej, a następnie Utwórz migawkę jego plik VHD. Możesz użyć tego pliku migawki nowsze hello tooretrieve wirtualnego dysku twardego plików w danym momencie i Utwórz ponownie hello maszyny Wirtualnej.

Jeśli włączono szyfrowanie usługi Magazyn (SSE) dla konta magazynu hello w których hello znajduje się obiekt blob, a następnie magazynowane zostaną zaszyfrowane wszystkie migawki wziąć pod uwagę tego obiektu blob.

## <a name="create-a-snapshot"></a>Utwórz migawkę
Witaj Poniższy przykładowy kod przedstawia sposób hello toocreate migawki za pomocą [biblioteki klienta magazynu Azure dla platformy .NET](https://www.nuget.org/packages/WindowsAzure.Storage/). W tym przykładzie określa dodatkowe metadane dla migawki hello podczas jego tworzenia.

```csharp
private static async Task CreateBlockBlobSnapshot(CloudBlobContainer container)
{
    // Create a new block blob in hello container.
    CloudBlockBlob baseBlob = container.GetBlockBlobReference("sample-base-blob.txt");

    // Add blob metadata.
    baseBlob.Metadata.Add("ApproxBlobCreatedDate", DateTime.UtcNow.ToString());

    try
    {
        // Upload hello blob toocreate it, with its metadata.
        await baseBlob.UploadTextAsync(string.Format("Base blob: {0}", baseBlob.Uri.ToString()));

        // Sleep 5 seconds.
        System.Threading.Thread.Sleep(5000);

        // Create a snapshot of hello base blob.
        // Specify metadata at hello time that hello snapshot is created toospecify unique metadata for hello snapshot.
        // If no metadata is specified when hello snapshot is created, hello base blob's metadata is copied toohello snapshot.
        Dictionary<string, string> metadata = new Dictionary<string, string>();
        metadata.Add("ApproxSnapshotCreatedDate", DateTime.UtcNow.ToString());
        await baseBlob.CreateSnapshotAsync(metadata, null, null, null);
    }
    catch (StorageException e)
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}
```

## <a name="copy-snapshots"></a>Kopiowanie migawek
Operacje kopiowania obejmujące obiekty BLOB i migawek wykonać następujące czynności:

* Możesz skopiować migawki za pośrednictwem jego podstawowego obiektu blob. Promowanie pozycji toohello migawki obiektu blob podstawowej hello, można przywrócić wcześniejszą wersję obiektu blob. Witaj pozostaje migawki, ale hello podstawowego obiektu blob jest zastępowany kopię zapisu hello migawki.
* Można skopiować obiektu blob migawki tooa docelowy o innej nazwie. Hello wynikowy docelowego obiektu blob jest zapisywalny obiektów blob i nie migawki.
* Po skopiowaniu źródłowego obiektu blob wszystkie migawki hello źródłowego obiektu blob nie są toohello skopiowanych docelowego. Gdy docelowego obiektu blob jest zastępowany kopii, wszystkie migawki skojarzone z hello oryginalnego docelowego obiektu blob pozostaną nienaruszone.
* Po utworzeniu migawki blokowych obiektów blob zablokowanych zatwierdzone hello blob jest również skopiowanych toohello migawki. Niezatwierdzone bloków nie są kopiowane.

## <a name="specify-an-access-condition"></a>Określ warunek dostępu
Podczas wywoływania [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], można określić warunki dostępu, dzięki czemu hello migawki jest tworzony tylko wtedy, gdy warunek jest spełniony. toospecify warunki dostępu, użyj hello [AccessCondition] [ dotnet_AccessCondition] parametru. Jeśli hello określony warunek nie jest spełniony, nie jest utworzona migawka hello i hello usługa Blob zwraca kod stanu [HTTPStatusCode][dotnet_HTTPStatusCode]. PreconditionFailed.

## <a name="delete-snapshots"></a>Usuń migawki
Nie można usunąć obiektu blob z migawkami, chyba że hello migawek, również zostaną usunięte. Możesz usunąć migawkę indywidualnie lub określ, że wszystkie migawki usunięte po usunięciu hello źródłowego obiektu blob. Jeśli próba toodelete obiektu blob, które nadal istnieją migawki, powoduje błąd.

Witaj, jak po przedstawia przykładowy kod toodelete obiektu blob i jego migawek w środowisku .NET, gdzie `blockBlob` jest obiektem typu [CloudBlockBlob][dotnet_CloudBlockBlob]:

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a>Migawki z magazynem Azure — warstwa Premium
Korzystając z migawki z magazyn w warstwie Premium, zastosuj hello następujące reguły:

* Maksymalna liczba migawek na stronicowych obiektów blob na koncie magazynu premium Hello to 100. Zwraca kod błędu 409, po przekroczeniu tego limitu hello migawki obiektu Blob operacji (`SnapshotCountExceeded`).
* Można utworzyć migawkę stronicowych obiektów blob na koncie magazynu premium co 10 minut. Zwraca kod błędu 409, po przekroczeniu tego kursu hello migawki obiektu Blob operacji (`SnapshotOperationRateExceeded`).
* tooread migawki, można użyć toocopy operacji kopiowania obiektu Blob hello tooanother migawki stronicowy obiekt blob na koncie hello. Hello docelowego obiektu blob dla operacji kopiowania hello nie może mieć żadnych istniejących migawki. Jeśli hello docelowego obiektu blob migawki, a następnie zwraca kod błędu 409, hello operacji kopiowania obiektów Blob (`SnapshotsPresent`).

## <a name="return-hello-absolute-uri-tooa-snapshot"></a>Zwraca hello bezwzględny identyfikator URI tooa migawki
W tym przykładzie kodu C# tworzy migawkę i zapisuje się hello bezwzględny identyfikator URI dla hello lokalizacji głównej.

```csharp
//Create hello blob service client object.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";

CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();

//Get a reference tooa blob.
CloudBlockBlob blob = container.GetBlockBlobReference("sampleblob.txt");
blob.UploadText("This is a blob.");

//Create a snapshot of hello blob and write out its primary URI.
CloudBlockBlob blobSnapshot = blob.CreateSnapshot();
Console.WriteLine(blobSnapshot.SnapshotQualifiedStorageUri.PrimaryUri);
```

## <a name="understand-how-snapshots-accrue-charges"></a>Zrozumienie sposobu migawki naliczania opłat
Tworzenie migawek, która jest tylko do odczytu kopię obiektu blob, może spowodować konta tooyour opłaty za magazyn dodatkowe dane. Podczas projektowania aplikacji, jest ważne toobe uwagę sposobu naliczania może tych opłat, dzięki czemu można zminimalizować koszty.

### <a name="important-billing-considerations"></a>Istotne zagadnienia dotyczące rozliczeń
następujące listy Hello obejmuje tooconsider klucz wskazuje podczas tworzenia migawki.

* Konta magazynu ponosi opłaty za bloki unikatowy lub stron, czy znajdują się w obiekcie blob hello lub w migawce hello. Twoje konto nie spowodować naliczenie dodatkowych opłat za migawki skojarzone z obiektu blob, dopóki nie zostanie zaktualizowany hello obiektów blob, na którym są one oparte na. Po zaktualizowaniu obiektu blob podstawowej hello diverges go z jego migawek. W takim przypadku są naliczane opłaty za bloki unikatowy hello lub strony w poszczególnych obiektów blob lub migawki.
* Podczas zastępowania blok w ramach blokowych obiektów blob tego bloku jest następnie rozliczany jako unikatowy bloku. Dotyczy to nawet wtedy, gdy blok hello ma hello sam identyfikator blokowania i hello na tym samym ma dane w postaci w migawce hello. Po bloku hello dba ponownie, diverges go z jego odpowiednikiem w dowolnym migawki i zostanie naliczona danych. powitalne samo dla strony w stronicowych obiektów blob, która jest aktualizowana mają identyczne dane.
* Zastępowanie blokowych obiektów blob przez wywołanie hello [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream] [ dotnet_UploadFromStream], lub [UploadFromByteArray] [ dotnet_UploadFromByteArray] metoda zastępuje wszystkie bloki w obiekcie blob hello. Jeśli masz migawki skojarzone z tego obiektu blob, teraz odchodzenia wszystkich bloków blob podstawowej hello i migawki, a zostanie naliczona dla wszystkich bloków hello w obu obiektów blob. Dotyczy to nawet wtedy, gdy dane hello hello podstawowej obiektów blob i migawki hello pozostać identyczne.
* Hello usługi obiektów Blob platformy Azure nie ma toodetermine oznacza, czy dwa bloki zawierają identyczne dane. Każdy blok przekazane i zatwierdzone jest traktowany jako unikatowy, nawet wtedy, gdy ma ona hello tych samych danych i hello zablokować sam identyfikator. Ponieważ Naliczanie opłat dla bloków unikatowe, jest ważne tooconsider, który aktualizowania obiektów blob, który ma migawkę powoduje dodatkowe bloki unikatowy i dodatkowych opłat.

### <a name="minimize-cost-with-snapshot-management"></a>Minimalizuje koszt z zarządzania migawkami

Zaleca się zarządzanie z migawki dokładnie tooavoid dodatkowych opłat. Możesz wykonać następujące najlepsze rozwiązania toohelp zminimalizować hello kosztów ponoszonych przez hello magazynu migawek sieci:

* Usunięcie i ponowne utworzenie migawki skojarzone z obiektu blob po zaktualizowaniu hello obiektów blob, nawet jeśli aktualizujesz mają identyczne dane, chyba że projektu aplikacji wymaga, aby zachować migawki. Przez usunięcie i ponowne utworzenie migawki obiektu blob hello, możesz upewnij się, że hello obiektów blob i migawek nie odbiegają.
* Jeśli obsługujesz migawek dla obiekt blob, należy unikać wywoływania [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], lub [UploadFromByteArray] [ dotnet_UploadFromByteArray] tooupdate hello blob. Te metody Zamień wszystkie bloki hello w obiekcie blob hello, znacznie powoduje sieci podstawowej obiektów blob i jego toodiverge migawki. Zamiast tego aktualizacji hello najmniejszą możliwą liczbę bloków przy użyciu hello [PutBlock] [ dotnet_PutBlock] i [metoda PutBlockList] [ dotnet_PutBlockList] metody.

### <a name="snapshot-billing-scenarios"></a>Migawki rozliczeń scenariuszy
następujące scenariusze Hello pokazują, jak Naliczanie opłat dla blokowych obiektów blob i jego migawek.

**Scenariusz 1**

W scenariuszu 1 hello podstawowego obiektu blob nie został zaktualizowany po hello migawki, więc jest obciążany tylko dla bloków unikatowy 1, 2 i 3.

![Zasoby usługi Azure Storage](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

**Scenariusz 2**

W scenariuszu 2 podstawowego obiektu blob hello zostały zaktualizowane, ale hello migawka nie ma. Blok 3 został zaktualizowany, a nawet, jeśli zawiera ona hello tych samych danych i hello na tym samym identyfikatorze, jest taki sam, jak zablokować 3 w migawce hello nie hello. W związku z tym kontem hello jest pobierana cztery bloków.

![Zasoby usługi Azure Storage](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

**Scenariusz 3**

W scenariuszu 3 podstawowego obiektu blob hello zostały zaktualizowane, ale hello migawka nie ma. 3 blokowych zamieniono bloku 4 w obiekcie blob podstawowej hello, ale migawki hello nadal odzwierciedla blok 3. W związku z tym kontem hello jest pobierana cztery bloków.

![Zasoby usługi Azure Storage](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

**Scenariusz 4**

W scenariuszu 4 hello podstawowego obiektu blob została całkowicie zaktualizowana i zawiera żaden z jego oryginalnych bloków. W związku z tym rozliczany hello konta dla wszystkich osiem bloków unikatowy. Ten scenariusz może wystąpić, jeśli używasz metody aktualizacji takich jak [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], lub [UploadFromByteArray][dotnet_UploadFromByteArray], ponieważ metody te Zastąp całą zawartość hello obiektu blob.

![Zasoby usługi Azure Storage](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a>Następne kroki

* Można znaleźć więcej informacji na temat pracy z migawek dysków maszyny wirtualnej (VM) w [kopia zapasowa Azure niezarządzane dysków maszyny Wirtualnej z migawkami przyrostowe](../../virtual-machines/windows/incremental-snapshots.md)

* Dla dodatkowych przykładów kodu przy użyciu magazynu obiektów Blob, zobacz [przykłady kodu Azure](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob). Można pobrać przykładową aplikację i uruchom go lub Przeglądaj hello kodu w witrynie GitHub.

[dotnet_AccessCondition]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.accesscondition.aspx
[dotnet_CloudBlockBlob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.aspx
[dotnet_CreateSnapshotAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.createsnapshotasync.aspx
[dotnet_HTTPStatusCode]: https://msdn.microsoft.com/library/system.net.httpstatuscode(v=vs.110).aspx
[dotnet_PutBlockList]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblocklist.aspx
[dotnet_PutBlock]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblock.aspx
[dotnet_UploadFromByteArray]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfrombytearray.aspx
[dotnet_UploadFromFile]: https://msdn.microsoft.com/library/azure/mt705654.aspx
[dotnet_UploadFromStream]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfromstream.aspx
[dotnet_UploadText]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadtext.aspx