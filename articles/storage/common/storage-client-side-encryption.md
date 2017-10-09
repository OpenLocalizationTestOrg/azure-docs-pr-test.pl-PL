---
title: "Szyfrowanie po stronie aaaClient z platformą .NET dla magazynu Microsoft Azure | Dokumentacja firmy Microsoft"
description: "Witaj biblioteki klienta magazynu Azure dla platformy .NET obsługuje szyfrowanie po stronie klienta i integracja z usługą Azure Key Vault dla zapewnienia maksymalnego poziomu bezpieczeństwa dla aplikacji usługi Azure Storage."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: becfccca-510a-479e-a798-2044becd9a64
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: c09246f43801e17aff96ea453182d11ffbf5e420
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-and-azure-key-vault-for-microsoft-azure-storage"></a>Magazyn kluczy szyfrowania po stronie klienta i Azure dla magazynu Microsoft Azure
[!INCLUDE [storage-selector-client-side-encryption-include](../../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a>Omówienie
Witaj [biblioteki klienta magazynu Azure dla pakietu Nuget programu .NET](https://www.nuget.org/packages/WindowsAzure.Storage) obsługuje szyfrowanie danych w aplikacjach klienckich przed przekazaniem tooAzure magazynu i odszyfrowywania danych podczas pobierania toohello klienta. Biblioteka Hello obsługuje również integrację z [usługi Azure Key Vault](https://azure.microsoft.com/services/key-vault/) zarządzania kluczami konta magazynu.

Samouczek krok po kroku, który poprowadzi Cię przez proces hello szyfrowania obiektów blob za pomocą szyfrowania po stronie klienta i usługi Azure Key Vault, zobacz [szyfrowanie i odszyfrowywanie obiektów blob w magazynie platformy Microsoft Azure przy użyciu usługi Azure Key Vault](../blobs/storage-encrypt-decrypt-blobs-key-vault.md).

Szyfrowanie po stronie klienta z językiem Java, zobacz [szyfrowania po stronie klienta z językiem Java dla magazynu Microsoft Azure](storage-client-side-encryption-java.md).

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a>Szyfrowanie i odszyfrowywanie za pomocą techniki koperty hello
procesy Hello szyfrowania i odszyfrowywania wykonaj hello koperty techniki.

### <a name="encryption-via-hello-envelope-technique"></a>Szyfrowanie za pomocą techniki koperty hello
Szyfrowanie za pomocą techniki koperty hello działa w następujący sposób hello:

1. Biblioteka klienta magazynu Azure Hello generuje klucz szyfrowania zawartości (CEK), jest jeden jednorazowej użycia klucza symetrycznego.
2. Dane użytkownika są szyfrowane przy użyciu tego CEK.
3. Witaj CEK jest następnie opakowane (zaszyfrowane) przy użyciu hello klucza szyfrowania klucza (KEK). Hello KEK jest identyfikowany przez identyfikator klucza i można parę klucza asymetrycznego lub klucza symetrycznego i może być zarządzane lokalnie lub przechowywane w magazynach klucza usługi Azure.
   
    Biblioteka klienta usługi storage Hello się nigdy nie tooKEK dostępu. Biblioteka Hello wywołuje algorytm klucza zawijania hello są udostępniane przez usługi Key Vault. Użytkownicy mogą wybrać toouse niestandardowego dostawcy dla kluczy zawijania/odkodowywania w razie potrzeby.

4. Witaj zaszyfrowane dane są następnie przekazywane toohello usługi Magazyn Azure. Hello opakowana klucz wraz ze niektóre metadane dodatkowego szyfrowania jest przechowywane jako metadanych (dla obiektu blob) albo interpolowane z hello zaszyfrowane dane (wiadomości w kolejce i jednostek tabeli).

### <a name="decryption-via-hello-envelope-technique"></a>Odszyfrowywanie przy użyciu techniki koperty hello
Odszyfrowywanie przy użyciu techniki koperty hello działa w hello w następujący sposób:

1. Biblioteka klienta Hello przyjęto założenie, że użytkownik hello zarządza hello klucza szyfrowania klucza (KEK) lokalnie lub w magazynach klucza usługi Azure. Witaj, użytkownik nie musi tooknow hello określonego klucza używanego do szyfrowania. Zamiast tego klucza programu rozpoznawania nazw, która rozwiązuje tookeys różne identyfikatory klucza można skonfigurować i używane.
2. Biblioteka klienta Hello pobiera hello zaszyfrowanych danych wraz z materiał szyfrowania, który jest przechowywany w usłudze hello.
3. klucz szyfrowania zawartości opakowanej Hello (CEK) znajduje się przy użyciu (odszyfrowane) bez otoki hello klucza szyfrowania klucza (KEK). W tym miejscu ponownie powitania klienta biblioteki nie ma tooKEK dostępu. Wywołuje po prostu hello niestandardowych lub dostawcy magazynu kluczy odszyfrowania algorytmu.
4. Hello zawartości klucza szyfrowania (CEK) jest następnie używane dane użytkownika toodecrypt hello szyfrowane.

## <a name="encryption-mechanism"></a>Mechanizm szyfrowania
Biblioteka klienta usługi storage Hello używa [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) w kolejności tooencrypt użytkownika danych. W szczególności [Cipher Block Chaining (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) trybu z użyciem standardu AES. Każdy usługi działa nieco inaczej, dlatego omówimy każdego z nich w tym miejscu.

### <a name="blobs"></a>Obiekty blob
Biblioteka klienta Hello obecnie obsługuje szyfrowanie tylko całe obiektów blob. W szczególności, szyfrowanie jest obsługiwane, gdy użytkownicy używają hello **UploadFrom*** metod lub hello **OpenWrite** metody. Obsługiwane są pliki do pobrania, zarówno pełne i pobieranie zakresu.

Podczas szyfrowania powitania klienta biblioteki generowania losowego inicjowania wektora (IV) 16 bajtów oraz klucz szyfrowania zawartości (CEK) 32 bajtów i wykonać koperty szyfrowanie danych obiektów blob hello, korzystając z tych informacji. Witaj opakowana CEK i niektóre metadane szyfrowania dodatkowe są następnie przechowywane, jak metadanych oraz hello blob zaszyfrowane na powitania usługi blob.

> [!WARNING]
> Jeśli edytujesz lub przekazywania metadanych dla obiektu blob hello, konieczne jest zachowywanie tych metadanych tooensure. Jeśli przekazywanie nowe metadane bez takich metadanych, hello opakowana CEK, IV i inne metadane zostaną utracone i zawartości obiektu blob hello nigdy nie będzie można ponownie pobrać.
> 
> 

Pobieranie zaszyfrowanej blob polega na pobraniu zawartości hello całego obiektu blob hello przy użyciu hello **DownloadTo***/**BlobReadStream** wygody metody. Hello opakowana CEK następnie rozpakować i używać razem z hello IV (przechowywane jako metadane obiektu blob w tym przypadku) tooreturn hello odszyfrować danych toohello użytkowników.

Pobieranie z dowolnego zakresu (**DownloadRange*** metody) w hello zaszyfrowany obiekt blob obejmuje dostosowania zakresu hello dostarczane przez użytkowników w kolejności tooget niewielkie dodatkowych danych, które mogą być używane toosuccessfully odszyfrować hello żądany zakres.

Wszystkie typy obiektu blob (blokowe obiekty BLOB, stronicowe i uzupełnialne) mogły być szyfrowane/odszyfrowane przy użyciu tego systemu.

### <a name="queues"></a>Kolejki
Ponieważ wiadomości w kolejce może być dowolnym formacie, powitania klienta biblioteki definiuje niestandardowego formatu, który zawiera tekst wiadomości powitania hello wektor inicjowania (IV) i klucz szyfrowania zaszyfrowanej zawartości hello (CEK).

Podczas szyfrowania powitania klienta biblioteki generuje losowe IV 16 bajtów wraz z losowe CEK 32 bajtów i wykonuje szyfrowanie koperty hello kolejki wiadomości tekstu, korzystając z tych informacji. Witaj opakowana CEK i niektóre metadane dodatkowego szyfrowania jest następnie dodawana toohello zaszyfrowanych kolejki wiadomości. Ten komunikat modyfikacji (pokazana poniżej) są przechowywane na powitania usługi.

    <MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>

Podczas odszyfrowywania klucz opakowana hello zostaje wyodrębniony z komunikatu w kolejce hello i nie opakowanych. Hello IV jest również wyodrębniony z komunikatu w kolejce hello i używać razem z danymi o hello nie opakowanych klucza toodecrypt hello kolejki wiadomości. Należy pamiętać, że metadane szyfrowania hello to mały (w bajtach 500), więc podczas jego wliczane limit 64 KB hello komunikatu w kolejce, wpływ hello powinno być łatwe w zarządzaniu.

### <a name="tables"></a>Tabele
Witaj klienta biblioteki obsługuje szyfrowanie właściwości obiektów w operacjach wstawiania i zamienianie operacji.

> [!NOTE]
> Scalanie nie jest obecnie obsługiwane. Ponieważ podzbiór właściwości może być zaszyfrowany wcześniej za pomocą innego klucza, po prostu scalanie hello nowe właściwości i aktualizowania metadanych hello spowoduje utratę danych. Scalanie albo wymaga wprowadzania dodatkowych usługi wywołuje tooread hello istniejące jednostki z usługi hello lub przy użyciu nowego klucza dla właściwości, które nie są odpowiednie ze względu na wydajność.
> 
> 

Szyfrowanie danych tabeli działa w następujący sposób:  

1. Użytkownicy określić toobe właściwości hello szyfrowane.
2. Biblioteka klienta Hello generuje losowe inicjowania wektora (IV) 16 bajtów oraz klucza szyfrowania zawartości (CEK) 32 bajtów dla każdej jednostki i wykonuje szyfrowanie koperty na powitania poszczególnych właściwości toobe zaszyfrowane przez nowy IV na wyprowadzanie Właściwość. Właściwość Hello szyfrowane są przechowywane jako dane binarne.
3. Witaj opakowana CEK i niektóre metadane szyfrowania dodatkowe następnie są przechowywane jako dwa dodatkowe właściwości zastrzeżone. pierwszą właściwością zarezerwowane (_ClientEncryptionMetadata1) Hello jest właściwości ciągu, która zawiera informacje hello IV, wersji i klucz opakowana. Druga właściwość zastrzeżone (_ClientEncryptionMetadata2) Hello jest właściwość binarną, która zawiera informacje hello hello właściwości, które są szyfrowane. Witaj informacji w tej drugiej właściwości (_ClientEncryptionMetadata2) jest zaszyfrowany.
4. Powodu toothese dodatkowe właściwości zastrzeżone wymagana na potrzeby szyfrowania użytkownicy mogą teraz mieć tylko 250 właściwości niestandardowych zamiast 252. Całkowity rozmiar Hello hello jednostki musi być mniejszy niż 1 MB.

Należy pamiętać, że tylko właściwości parametrów mogą być szyfrowane. Jeśli inne typy właściwości toobe zaszyfrowane, muszą być toostrings przekonwertowany. ciągi Hello szyfrowane są przechowywane w usłudze hello jako właściwości binarnych, a zostaną one przetworzone toostrings wstecz po odszyfrowywania.

W przypadku tabel Ponadto toohello zasady szyfrowania, użytkownicy muszą określić toobe właściwości hello szyfrowane. Można to zrobić, określając atrybutu [EncryptProperty] (dla jednostki POCO, które pochodzą z TableEntity) lub szyfrowania, program rozpoznawania nazw w opcjach żądania. Rozwiązywanie problemów z szyfrowania jest delegata, który ma klucz partycji, klucz wiersza i nazwy właściwości i zwraca wartość Boolean wskazującą, czy ma być szyfrowana tej właściwości. Podczas szyfrowania powitania klienta biblioteki użyje tego toodecide informacji czy właściwość powinny być szyfrowane podczas przesyłania toohello zapisu. Delegat Hello udostępnia także możliwość hello logiki wokół jak właściwości są szyfrowane. (Na przykład, jeśli X, następnie szyfrować właściwości A; w przeciwnym razie szyfrowania właściwości A i B.) Należy pamiętać, że jest niekonieczne tooprovide te informacje podczas odczytywania lub zapytanie jednostki.

### <a name="batch-operations"></a>Operacje w trybie wsadowym
W operacji wsadowych hello KEK tego samego zostanie użyty przez wszystkie wiersze hello w tej operacji zbiorczej ponieważ powitania klienta biblioteki umożliwia tylko jeden obiekt opcje (i dlatego jednej zasady/KEK) dla operacji zbiorczej. Jednak biblioteka klienta hello wewnętrznie wygeneruje nowy losowych IV i losowe CEK w wierszu w partii hello. Użytkownicy mogą także wybrać tooencrypt inne właściwości dla każdej operacji w partii hello, definiując to zachowanie w hello szyfrowania programu rozpoznawania nazw.

### <a name="queries"></a>Zapytania
Operacje kwerend tooperform, należy określić klucza programu rozpoznawania nazw, będącą w stanie tooresolve hello wszystkie klucze w zestawie wyników hello. Jeśli jednostka zawarte w wyniku zapytania hello nie można rozpoznać tooa dostawcy, powitania klienta biblioteki zgłosi błąd. Dla dowolnego zapytania, który wykonuje projekcje po stronie serwera powitania klienta biblioteki doda hello właściwości metadanych szyfrowania specjalne (_ClientEncryptionMetadata1 i _ClientEncryptionMetadata2) przez domyślne toohello wybrane kolumny.

## <a name="azure-key-vault"></a>W usłudze Azure Key Vault
Usługa Azure Key Vault ułatwia ochronę kluczy kryptograficznych i kluczy tajnych używanych przez aplikacje i usługi w chmurze. Za pomocą usługi Azure Key Vault, użytkownicy mogą szyfrować klucze i klucze tajne (takie jak klucze uwierzytelniania, klucze konta magazynu, klucze szyfrowania danych. Pliki PFX oraz hasła) przy użyciu kluczy chronionych przez sprzętowe moduły zabezpieczeń (HSM). Aby uzyskać więcej informacji, zobacz [co to jest usługa Azure Key Vault?](../../key-vault/key-vault-whatis.md).

Biblioteka klienta usługi storage Hello używa hello Key Vault podstawowej biblioteki w kolejności tooprovide wspólnej struktury wszystkich Azure do zarządzania kluczami. Użytkownicy otrzymują również hello dodatkową korzyścią z używania biblioteki rozszerzenia usługi Key Vault hello. Biblioteka rozszerzeń Hello zawiera przydatne funkcje wokół łatwego i Symmetric/RSA lokalnych i chmurze dostawców klucza, a także z agregacji i buforowania.

### <a name="interface-and-dependencies"></a>Interfejs i zależności
Istnieją trzy pakiety usługi Key Vault:

* Microsoft.Azure.KeyVault.Core zawiera hello IKey i IKeyResolver. Jest mała pakietu bez zależności. Witaj biblioteki klienta usługi storage dla platformy .NET definiuje ją jako zależności.
* Microsoft.Azure.KeyVault zawiera powitania klienta Key Vault REST.
* Microsoft.Azure.KeyVault.Extensions zawiera kod rozszerzenia, która obejmuje implementacje algorytmów kryptograficznych i RSAKey i SymmetricKey. Zależy od hello Core i KeyVault przestrzeni nazw, a zapewnia toodefine funkcji agregujących rozpoznawania nazw (gdy użytkownicy mają toouse wielu dostawców klucza) i buforowania rozpoznawania klucza. Mimo że biblioteki klienta usługi storage hello bezpośrednio niezależnie od tego pakietu, jeśli użytkownicy mają toostore usługi Azure Key Vault toouse ich kluczy lub toouse hello Key Vault rozszerzenia tooconsume hello lokalnych i w chmurze dostawców usług kryptograficznych, potrzebują tego pakietu.

Key Vault jest zaprojektowana dla kluczy głównych wysokiej wartości i ograniczania przepustowości limity dla usługi Key Vault zostały zaprojektowane z tym pamiętać. Podczas wykonywania szyfrowania po stronie klienta z magazynu kluczy, model preferowany hello jest toouse głównego kluczy symetrycznych przechowywane jako kluczy tajnych w magazynie kluczy i buforowane lokalnie. Użytkownicy muszą wykonać następujące hello:

1. Utwórz klucz tajny w trybie offline i przekaż go tooKey magazynu.
2. Za pomocą identyfikatora podstawowej hello secret tooresolve parametru hello bieżącej wersji hello hasło do szyfrowania i pamięci podręcznej te informacje lokalnie. Użyj CachingKeyResolver do buforowania; Użytkownicy są tooimplement nie oczekiwano własne buforowanie logiki.
3. Użyj programu rozpoznawania nazw buforowania hello jako dane wejściowe podczas tworzenia zasady szyfrowania hello.

Więcej informacji na temat użycia usługi Key Vault znajdują się w hello [przykłady kodu szyfrowania](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples).

## <a name="best-practices"></a>Najlepsze praktyki
Obsługa szyfrowania jest dostępna tylko w hello biblioteki klienta usługi storage dla platformy .NET. Windows Phone i środowiska wykonawczego systemu Windows aktualnie nie obsługuje szyfrowania.

> [!IMPORTANT]
> Należy pamiętać o tych punktów ważne przy użyciu szyfrowania po stronie klienta:
> 
> * Podczas odczytywania lub pisania tooan szyfrowane obiektów blob, użyj całego obiektu blob przekazywania oraz zakres/całość obiektu blob pobierania poleceń. Unikać pisania tooan blob zaszyfrowane za pomocą protokołu operacji, takich jak Put bloku, umieść listy zablokowanych, zapisu stron, wyczyść strony lub Dołącz bloku; w przeciwnym razie możesz uszkodzony obiekt blob zaszyfrowany hello i stał się niemożliwe do odczytania.
> * W przypadku tabel istnieje ograniczenie podobne. Należy uważać toonot aktualizacji zaszyfrowane właściwości bez aktualizowania metadanych szyfrowania hello.
> * Jeśli ustawisz metadanych dla obiektu blob zaszyfrowane hello może zastąpić metadane związane z szyfrowaniem hello wymaganych do odszyfrowania, ponieważ ustawienie metadanych nie jest dodatek. Dotyczy to również migawki; Unikaj określania metadanych podczas tworzenia migawki obiektu blob zaszyfrowane. Jeśli metadane muszą być ustawione, należy się hello toocall **FetchAttributes** tooget pierwszy — metoda hello bieżących metadanych szyfrowania i uniknąć równoczesnych zapisów podczas ustawiania metadanych.
> * Włącz hello **RequireEncryption** właściwości w hello domyślne opcje żądania użytkowników, którzy powinien działać wyłącznie z zaszyfrowanych danych. Aby uzyskać więcej informacji, zobacz poniżej.
> 
> 

## <a name="client-api--interface"></a>Interfejs API klienta / interfejsu
Podczas tworzenia obiektu EncryptionPolicy, użytkownicy mogą podać tylko klucz (Implementowanie IKey), tylko program rozpoznawania nazw (Implementowanie IKeyResolver) lub obie. IKey jest hello podstawowy typ klucza który jest identyfikowany przy użyciu identyfikatora klucza i zapewnia logiki hello zawijania/odkodowywania. IKeyResolver jest używane tooresolve klucza podczas odszyfrowywania hello. Definiuje metodę ResolveKey, która zwraca IKey podany identyfikator klucza. Zapewnia to użytkownikom hello możliwości toochoose między wiele kluczy, które są zarządzane na wiele lokalizacji.

* Dla celów szyfrowania zawsze jest używany klucz hello i hello Brak klucza spowoduje błąd.
* Do odszyfrowywania:
  * Program rozpoznawania nazw kluczy Hello jest wywoływana, jeśli określony klucz hello tooget. Jeśli hello programu rozpoznawania nazw jest określony, ale nie ma mapowania dla identyfikatora klucza hello, jest zgłaszany błąd.
  * Jeśli nie określono programu rozpoznawania nazw, ale nie określono klucza, klucz hello zostanie użyty, jeśli jego identyfikator odpowiada hello wymagany identyfikator klucza. Jeśli identyfikator hello nie jest zgodny, jest zgłaszany błąd.

Witaj [przykłady szyfrowania](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples) pokazują scenariusza bardziej szczegółowe end-to-end dla obiektów blob, kolejek i tabel, wraz z Integracja magazynu kluczy.

### <a name="requireencryption-mode"></a>Tryb RequireEncryption
Użytkownicy mogą opcjonalnie włączyć tryb działania, w której wszystkie przekazywania i pobierania muszą być szyfrowane. W tym trybie prób tooupload danych bez szyfrowania zasad lub pobrać dane, które nie są szyfrowane na powitania usługi zakończy się niepowodzeniem na powitania klienta. Witaj **RequireEncryption** właściwości obiektu opcje żądania hello kontroluje to zachowanie. Jeśli aplikacja będzie szyfrowania wszystkich obiektów przechowywanych w usłudze Azure Storage, a następnie można ustawić hello **RequireEncryption** właściwość hello domyślne żądanie opcje dla obiekt klienta usługi hello. Na przykład ustawić **CloudBlobClient.DefaultRequestOptions.RequireEncryption** za**true** wykonać toorequire szyfrowania dla wszystkich operacji obiektów blob za pośrednictwem tego obiektu klienta.

### <a name="blob-service-encryption"></a>Szyfrowanie usługi blob
Utwórz **BlobEncryptionPolicy** obiektu i ustaw go w opcji żądania hello (dla interfejsu API lub na poziomie klienta za pomocą **DefaultRequestOptions**). Wszystkie inne będzie obsługiwany przez bibliotekę klienta hello wewnętrznie.

```csharp
// Create hello IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create hello encryption policy toobe used for upload and download.
 BlobEncryptionPolicy policy = new BlobEncryptionPolicy(key, null);

 // Set hello encryption policy on hello request options.
 BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

 // Upload hello encrypted contents toohello blob.
 blob.UploadFromStream(stream, size, null, options, null);

 // Download and decrypt hello encrypted contents from hello blob.
 MemoryStream outputStream = new MemoryStream();
 blob.DownloadToStream(outputStream, null, options, null);
```

### <a name="queue-service-encryption"></a>Szyfrowanie usługi kolejki
Utwórz **QueueEncryptionPolicy** obiektu i ustaw go w opcji żądania hello (dla interfejsu API lub na poziomie klienta za pomocą **DefaultRequestOptions**). Wszystkie inne będzie obsługiwany przez bibliotekę klienta hello wewnętrznie.

```csharp
// Create hello IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create hello encryption policy toobe used for upload and download.
 QueueEncryptionPolicy policy = new QueueEncryptionPolicy(key, null);

 // Add message
 QueueRequestOptions options = new QueueRequestOptions() { EncryptionPolicy = policy };
 queue.AddMessage(message, null, null, options, null);

 // Retrieve message
 CloudQueueMessage retrMessage = queue.GetMessage(null, options, null);
```

### <a name="table-service-encryption"></a>Szyfrowanie usługi tabel
Ponadto toocreating zasady szyfrowania i ustawienie jej na żądanie opcji, należy określić **EncryptionResolver** w **TableRequestOptions**, lub ustaw atrybut hello [EncryptProperty] na Witaj jednostki.

#### <a name="using-hello-resolver"></a>Za pomocą mechanizmu rozpoznawania hello

```csharp
// Create hello IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create hello encryption policy toobe used for upload and download.
 TableEncryptionPolicy policy = new TableEncryptionPolicy(key, null);

 TableRequestOptions options = new TableRequestOptions()
 {
    EncryptionResolver = (pk, rk, propName) =>
     {
        if (propName == "foo")
         {
            return true;
         }
         return false;
     },
     EncryptionPolicy = policy
 };

 // Insert Entity
 currentTable.Execute(TableOperation.Insert(ent), options, null);

 // Retrieve Entity
 // No need toospecify an encryption resolver for retrieve
 TableRequestOptions retrieveOptions = new TableRequestOptions()
 {
    EncryptionPolicy = policy
 };

 TableOperation operation = TableOperation.Retrieve(ent.PartitionKey, ent.RowKey);
 TableResult result = currentTable.Execute(operation, retrieveOptions, null);
```

#### <a name="using-attributes"></a>Przy użyciu atrybutów
Jak wspomniano powyżej, gdy jednostka hello implementuje TableEntity, następnie może korzystać hello właściwości z atrybutem hello [EncryptProperty] zamiast określania hello **EncryptionResolver**.

```csharp
[EncryptProperty]
 public string EncryptedProperty1 { get; set; }
```

## <a name="encryption-and-performance"></a>Szyfrowanie i wydajności
Należy pamiętać, że szyfrowania z magazynu danych spowoduje zmniejszenie wydajności. Witaj zawartości musi zostać wygenerowany klucz i IV samej zawartości hello muszą być szyfrowane i dodatkowe metadane muszą być sformatowane i przekazać. Ten narzut będą się różnić w zależności od ilości hello dane są zaszyfrowane. Zaleca się, że klienci zawsze testują wydajności w czasie projektowania.

## <a name="next-steps"></a>Następne kroki
* [Samouczek: Szyfrowanie i odszyfrowywanie obiektów blob w magazynie platformy Microsoft Azure przy użyciu usługi Azure Key Vault](../blobs/storage-encrypt-decrypt-blobs-key-vault.md)
* Pobierz hello [biblioteki klienta magazynu Azure dla pakietu NuGet programu .NET](https://www.nuget.org/packages/WindowsAzure.Storage)
* Pobierz hello Azure Key Vault NuGet [Core](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core/), [klienta](http://www.nuget.org/packages/Microsoft.Azure.KeyVault/), i [rozszerzenia](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions/) pakietów  
* Odwiedź hello [dokumentacji magazynu kluczy Azure](../../key-vault/key-vault-whatis.md)
