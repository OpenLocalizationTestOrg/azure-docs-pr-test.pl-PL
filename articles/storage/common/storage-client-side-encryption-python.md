---
title: "Szyfrowanie po stronie aaaClient języka Python dla usługi Magazyn Microsoft Azure | Dokumentacja firmy Microsoft"
description: "Witaj biblioteki klienta usługi Azure Storage dla języka Python obsługuje szyfrowanie po stronie klienta dla zapewnienia maksymalnego poziomu bezpieczeństwa dla aplikacji usługi Azure Storage."
services: storage
documentationcenter: python
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: f9bf7981-9948-4f83-8931-b15679a09b8a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/11/2017
ms.author: lakasa
ms.openlocfilehash: 3a52b64f93daf85a55308f8a4bee9c98b2315d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-with-python-for-microsoft-azure-storage"></a>Szyfrowanie po stronie klienta z języka Python dla magazynu Microsoft Azure
[!INCLUDE [storage-selector-client-side-encryption-include](../../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a>Omówienie
Witaj [biblioteki klienta usługi Azure Storage dla języka Python](https://pypi.python.org/pypi/azure-storage) obsługuje szyfrowanie danych w aplikacjach klienckich przed przekazaniem tooAzure magazynu i odszyfrowywania danych podczas pobierania toohello klienta.

> [!NOTE]
> biblioteka języka Python magazynu Azure Hello jest w wersji zapoznawczej.
> 
> 

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a>Szyfrowanie i odszyfrowywanie za pomocą techniki koperty hello
procesy Hello szyfrowania i odszyfrowywania wykonaj hello koperty techniki.

### <a name="encryption-via-hello-envelope-technique"></a>Szyfrowanie za pomocą techniki koperty hello
Szyfrowanie za pomocą techniki koperty hello działa w następujący sposób hello:

1. Biblioteka klienta magazynu Azure Hello generuje klucz szyfrowania zawartości (CEK), jest jeden jednorazowej użycia klucza symetrycznego.
2. Dane użytkownika są szyfrowane przy użyciu tego CEK.
3. Witaj CEK jest następnie opakowane (zaszyfrowane) przy użyciu hello klucza szyfrowania klucza (KEK). Hello KEK jest identyfikowany przez identyfikator klucza i może być parę klucza asymetrycznego lub klucza symetrycznego, które jest zarządzane lokalnie.
   Biblioteka klienta usługi storage Hello się nigdy nie tooKEK dostępu. Biblioteka Hello wywołuje klucza hello zawijania algorytmu, który jest zapewniana przez hello KEK. Użytkownicy mogą wybrać toouse niestandardowego dostawcy dla kluczy zawijania/odkodowywania w razie potrzeby.
4. Witaj zaszyfrowane dane są następnie przekazywane toohello usługi Magazyn Azure. Hello opakowana klucz wraz ze niektóre metadane dodatkowego szyfrowania jest przechowywane jako metadanych (dla obiektu blob) albo interpolowane z hello zaszyfrowane dane (wiadomości w kolejce i jednostek tabeli).

### <a name="decryption-via-hello-envelope-technique"></a>Odszyfrowywanie przy użyciu techniki koperty hello
Odszyfrowywanie przy użyciu techniki koperty hello działa w hello w następujący sposób:

1. Biblioteka klienta Hello przyjęto założenie, że użytkownik hello Zarządzanie lokalnie hello klucza szyfrowania klucza (KEK). Witaj, użytkownik nie musi tooknow hello określonego klucza używanego do szyfrowania. Zamiast tego klucza rozpoznawania nazw, która rozwiązuje tookeys różne identyfikatory klucza, można skonfigurować i używane.
2. Biblioteka klienta Hello pobiera hello zaszyfrowanych danych wraz z materiał szyfrowania, który jest przechowywany w usłudze hello.
3. klucz szyfrowania zawartości opakowanej Hello (CEK) znajduje się przy użyciu (odszyfrowane) bez otoki hello klucza szyfrowania klucza (KEK). W tym miejscu ponownie powitania klienta biblioteki nie ma tooKEK dostępu. Wywołuje po prostu hello niestandardowego dostawcy odszyfrowania algorytmu.
4. Hello zawartości klucza szyfrowania (CEK) jest następnie używane dane użytkownika toodecrypt hello szyfrowane.

## <a name="encryption-mechanism"></a>Mechanizm szyfrowania
Biblioteka klienta usługi storage Hello używa [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) w kolejności tooencrypt użytkownika danych. W szczególności [Cipher Block Chaining (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) trybu z użyciem standardu AES. Każdy usługi działa nieco inaczej, dlatego omówimy każdego z nich w tym miejscu.

### <a name="blobs"></a>Obiekty blob
Biblioteka klienta Hello obecnie obsługuje szyfrowanie tylko całe obiektów blob. W szczególności, szyfrowanie jest obsługiwane, gdy użytkownicy używają hello **utworzyć*** metody. Obsługiwane są pliki do pobrania, zarówno pełne i pobieranie zakresu, i paralelizacja przekazywania i pobierania jest dostępna.

Podczas szyfrowania powitania klienta biblioteki generowania losowego inicjowania wektora (IV) 16 bajtów oraz klucz szyfrowania zawartości (CEK) 32 bajtów i wykonać koperty szyfrowanie danych obiektów blob hello, korzystając z tych informacji. Witaj opakowana CEK i niektóre metadane szyfrowania dodatkowe są następnie przechowywane, jak metadanych oraz hello blob zaszyfrowane na powitania usługi blob.

> [!WARNING]
> Jeśli edytujesz lub przekazywania metadanych dla obiektu blob hello, konieczne jest zachowywanie tych metadanych tooensure. Podczas przesyłania nowych metadanych bez takich metadanych, hello opakowana CEK, IV i inne metadane zostaną utracone i zawartości obiektu blob hello nigdy nie zostać pobieranie.
> 
> 

Pobieranie zaszyfrowanej blob polega na pobraniu zawartości hello całego obiektu blob hello przy użyciu hello **uzyskać*** podręczne metody. Hello opakowana CEK następnie rozpakować i używać razem z hello IV (przechowywane jako metadane obiektu blob w tym przypadku) tooreturn hello odszyfrować danych toohello użytkowników.

Pobieranie dowolnego zakresu (**uzyskać*** przekazano metody z parametrami zakresu) w hello zaszyfrowany obiekt blob obejmuje hello zakresu zapewnionego przez użytkowników w kolejności tooget niewielkie dodatkowych danych, które mogą być używane do dostosowywania Witaj odszyfrowywania toosuccessfully zażądała zakresu.

Blokowe i stronicowe obiekty BLOB tylko może być szyfrowane/odszyfrować za pomocą tego systemu. Obecnie nie jest obsługiwane dla szyfrowania uzupełnialnych obiektów blob.

### <a name="queues"></a>Kolejki
Ponieważ wiadomości w kolejce może być dowolnym formacie, powitania klienta biblioteki definiuje niestandardowego formatu, który zawiera tekst wiadomości powitania hello wektor inicjowania (IV) i klucz szyfrowania zaszyfrowanej zawartości hello (CEK).

Podczas szyfrowania powitania klienta biblioteki generuje losowe IV 16 bajtów wraz z losowe CEK 32 bajtów i wykonuje szyfrowanie koperty hello kolejki wiadomości tekstu, korzystając z tych informacji. Witaj opakowana CEK i niektóre metadane dodatkowego szyfrowania jest następnie dodawana toohello zaszyfrowanych kolejki wiadomości. Ten komunikat modyfikacji (pokazana poniżej) są przechowywane na powitania usługi.

```
<MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>
```

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
3. Witaj opakowana CEK i niektóre metadane szyfrowania dodatkowe następnie są przechowywane jako dwa dodatkowe właściwości zastrzeżone. Witaj najpierw zastrzeżone właściwości (\_ClientEncryptionMetadata1) jest właściwością ciągu, która zawiera informacje hello IV, wersji i klucz opakowana. Witaj drugi zarezerwowanej właściwości (\_ClientEncryptionMetadata2) jest właściwość binarną, która zawiera informacje hello hello właściwości, które są szyfrowane. Witaj informacji w tej drugiej właściwości (\_ClientEncryptionMetadata2) jest zaszyfrowany.
4. Powodu toothese dodatkowe właściwości zastrzeżone wymagana na potrzeby szyfrowania użytkownicy mogą teraz mieć tylko 250 właściwości niestandardowych zamiast 252. Całkowity rozmiar Hello hello jednostki musi być mniejszy niż 1MB.
   
   Należy pamiętać, że tylko właściwości parametrów mogą być szyfrowane. Jeśli inne typy właściwości toobe zaszyfrowane, muszą być toostrings przekonwertowany. ciągi Hello szyfrowane są przechowywane w usłudze hello jako właściwości binarnych, a dokonywana jest ich konwersja wstecz toostrings (nieprzetworzone ciągi, nie EntityProperties z typem EdmType.STRING) po odszyfrowywania.
   
   W przypadku tabel Ponadto toohello zasady szyfrowania, użytkownicy muszą określić toobe właściwości hello szyfrowane. To może odbywać się przez zapisanie tych właściwości w obiektach TableEntity z tooEdmType.STRING zestawu typu hello i szyfrowania encryption_resolver_function zestawu tootrue lub ustawienie hello hello tableservice obiektu. Rozwiązywanie problemów z szyfrowania to funkcja, która przyjmuje klucza partycji, klucz wiersza i nazwy właściwości i zwraca wartość boolean wskazującą, czy ma być szyfrowana tej właściwości. Podczas szyfrowania powitania klienta biblioteki użyje tego toodecide informacji czy właściwość powinny być szyfrowane podczas przesyłania toohello zapisu. Delegat Hello udostępnia także możliwość hello logiki wokół jak właściwości są szyfrowane. (Na przykład, jeśli X, następnie szyfrować właściwości A; w przeciwnym razie szyfrowania właściwości A i B.) Należy pamiętać, że jest niekonieczne tooprovide te informacje podczas odczytywania lub zapytanie jednostki.

### <a name="batch-operations"></a>Operacje w trybie wsadowym
Jedne zasady szyfrowania stosuje tooall wierszy w partii hello. powitania klienta biblioteki wewnętrznie wygeneruje nowy losowych IV i losowe CEK wierszu w partii hello. Użytkownicy mogą także wybrać tooencrypt inne właściwości dla każdej operacji w partii hello, definiując to zachowanie w hello szyfrowania programu rozpoznawania nazw.
Jeśli partii jest tworzony jako menedżera kontekstu za pomocą metody batch() tableservice hello, zasady szyfrowania hello tableservice zostanie automatycznie zastosowane toohello partii. Jeśli partii jest jawnie utworzona przez wywołanie konstruktora hello, zasady szyfrowania hello musi zostać przekazany jako parametr i lewej strony, nie mają być modyfikowane, czas ich istnienia hello hello partii.
Należy pamiętać, że jednostki są szyfrowane, ponieważ są one wstawiane do partii hello za pomocą zasad szyfrowania hello partii (jednostek nie są szyfrowane w czasie zatwierdzania partii hello za pomocą zasad szyfrowania hello tableservice hello).

### <a name="queries"></a>Zapytania
Operacje kwerend tooperform, należy określić klucza programu rozpoznawania nazw, będącą w stanie tooresolve hello wszystkie klucze w zestawie wyników hello. Jeśli jednostka zawarte w wyniku zapytania hello nie można rozpoznać tooa dostawcy, powitania klienta biblioteki zgłosi błąd. Dla dowolnego zapytania, który wykonuje projekcje po stronie serwera, powitania klienta biblioteki spowoduje dodanie właściwości metadanych szyfrowania specjalne hello (\_ClientEncryptionMetadata1 i \_ClientEncryptionMetadata2) przez domyślny toohello wybrane kolumny .

> [!IMPORTANT]
> Należy pamiętać o tych punktów ważne przy użyciu szyfrowania po stronie klienta:
> 
> * Podczas odczytywania lub pisania tooan szyfrowane obiektów blob, użyj całego obiektu blob przekazywania oraz zakres/całość obiektu blob pobierania poleceń. Unikać pisania tooan blob zaszyfrowane za pomocą protokołu operacji, takich jak Put bloku, umieść listy zablokowanych, zapisu stron lub wyczyść stron. w przeciwnym razie możesz uszkodzony obiekt blob zaszyfrowany hello i stał się niemożliwe do odczytania.
> * W przypadku tabel istnieje ograniczenie podobne. Należy uważać toonot aktualizacji zaszyfrowane właściwości bez aktualizowania metadanych szyfrowania hello.
> * Jeśli ustawisz metadanych dla obiektu blob zaszyfrowane hello może zastąpić metadane związane z szyfrowaniem hello wymaganych do odszyfrowania, ponieważ ustawienie metadanych nie jest dodatek. Dotyczy to również migawki; Unikaj określania metadanych podczas tworzenia migawki obiektu blob zaszyfrowane. Jeśli metadane muszą być ustawione, należy się hello toocall **get_blob_metadata** tooget pierwszy — metoda hello bieżących metadanych szyfrowania i uniknąć równoczesnych zapisów podczas ustawiania metadanych.
> * Włącz hello **require_encryption** flagi na powitania obiektu usługi dla użytkowników, którzy powinien działać wyłącznie z zaszyfrowanych danych. Aby uzyskać więcej informacji, zobacz poniżej.
> 
> 

Biblioteka klienta usługi storage Hello oczekuje hello pod warunkiem KEK i rozpoznawania nazw kluczy hello tooimplement po interfejsu. [Usługa Azure Key Vault](https://azure.microsoft.com/services/key-vault/) obsługę zarządzania Python KEK oczekuje i będzie można zintegrować z tej biblioteki, po zakończeniu.

## <a name="client-api--interface"></a>Interfejs API klienta / interfejsu
Po utworzeniu obiektu usługi Magazyn (tj. blockblobservice) hello użytkownika może przypisać wartości pola toohello, które tworzą zasadę szyfrowania: key_encryption_key, key_resolver_function i require_encryption. Użytkownicy mogą podać tylko KEK tylko program rozpoznawania nazw, lub obie. key_encryption_key jest hello podstawowy typ klucza który jest identyfikowany przy użyciu identyfikatora klucza i zapewnia logiki hello zawijania/odkodowywania. key_resolver_function jest używane tooresolve klucza podczas odszyfrowywania hello. Zwraca prawidłową KEK, podany identyfikator klucza. Zapewnia to użytkownikom hello możliwości toochoose między wiele kluczy, które są zarządzane na wiele lokalizacji.

Witaj KEK musi implementować następujące hello toosuccessfully metody szyfrowania danych:

* wrap_key(cek): hello zawija określony przy użyciu algorytmu wybór użytkownika hello CEK (w bajtach). Zwraca hello opakowana klucza.
* get_key_wrap_algorithm(): zwraca hello algorytm używany toowrap kluczy.
* get_kid(): zwraca hello ciąg klucza identyfikatora dla tego KEK.
  Witaj KEK musi implementować następujące metody toosuccessfully odszyfrowywania danych hello:
* unwrap_key (cek, algorytm): zwraca hello nie opakowanych formę hello określony przy użyciu algorytmu określony ciąg hello CEK.
* get_kid(): zwraca ciąg identyfikatora klucza dla tego KEK.

Program rozpoznawania nazw kluczy Hello co najmniej musi implementować metodę, która podany identyfikator klucza, zwraca hello odpowiedniego KEK implementującej hello interfejsu powyżej. Tylko ta metoda jest toobe toohello key_resolver_function właściwości w obiekcie usługi hello przypisane.

* Dla celów szyfrowania zawsze jest używany klucz hello i hello Brak klucza spowoduje błąd.
* Do odszyfrowywania:
  
  * Program rozpoznawania nazw kluczy Hello jest wywoływana, jeśli określony klucz hello tooget. Jeśli hello programu rozpoznawania nazw jest określony, ale nie ma mapowania dla identyfikatora klucza hello, jest zgłaszany błąd.
  * Jeśli nie określono programu rozpoznawania nazw, ale nie określono klucza, klucz hello zostanie użyty, jeśli jego identyfikator odpowiada hello wymagany identyfikator klucza. Jeśli identyfikator hello nie jest zgodny, jest zgłaszany błąd.
    
    Witaj próbek szyfrowania w azure.storage.samples <fix URL>zaprezentowania bardziej szczegółowe scenariusza end-to-end dla obiektów blob, kolejek i tabel.
      Przykładowe implementacje hello KEK i rozpoznawania nazw kluczy są zawarte w hello przykładowych plików jako KeyWrapper i KeyResolver odpowiednio.

### <a name="requireencryption-mode"></a>Tryb RequireEncryption
Użytkownicy mogą opcjonalnie włączyć tryb działania, w której wszystkie przekazywania i pobierania muszą być szyfrowane. W tym trybie prób tooupload danych bez szyfrowania zasad lub pobrać dane, które nie są szyfrowane na powitania usługi zakończy się niepowodzeniem na powitania klienta. Witaj **require_encryption** Flaga formantów obiektu usługi hello to zachowanie.

### <a name="blob-service-encryption"></a>Szyfrowanie usługi blob
Ustawić pól zasad szyfrowania hello hello blockblobservice obiektu. Wszystkie inne będzie obsługiwany przez bibliotekę klienta hello wewnętrznie.

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_block_blob_service.key_encryption_key = kek
my_block_blob_service.key_resolver_funcion = key_resolver.resolve_key

# Upload hello encrypted contents toohello blob.
my_block_blob_service.create_blob_from_stream(container_name, blob_name, stream)

# Download and decrypt hello encrypted contents from hello blob.
blob = my_block_blob_service.get_blob_to_bytes(container_name, blob_name)
```

### <a name="queue-service-encryption"></a>Szyfrowanie usługi kolejki
Ustawić pól zasad szyfrowania hello hello queueservice obiektu. Wszystkie inne będzie obsługiwany przez bibliotekę klienta hello wewnętrznie.

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_queue_service.key_encryption_key = kek
my_queue_service.key_resolver_funcion = key_resolver.resolve_key

# Add message
my_queue_service.put_message(queue_name, content)

# Retrieve message
retrieved_message_list = my_queue_service.get_messages(queue_name)
```

### <a name="table-service-encryption"></a>Szyfrowanie usługi tabel
Ponadto toocreating zasady szyfrowania i ustawienie jej na żądanie opcji, należy określić **encryption_resolver_function** na powitania **tableservice**, lub zaszyfrować atrybutu na powitania zestawu Witaj EntityProperty.

### <a name="using-hello-resolver"></a>Za pomocą mechanizmu rozpoznawania hello

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Define hello encryption resolver_function.
def my_encryption_resolver(pk, rk, property_name):
        if property_name == 'foo':
                return True
        return False

# Set hello KEK and key resolver on hello service object.
my_table_service.key_encryption_key = kek
my_table_service.key_resolver_funcion = key_resolver.resolve_key
my_table_service.encryption_resolver_function = my_encryption_resolver

# Insert Entity
my_table_service.insert_entity(table_name, entity)

# Retrieve Entity
# Note: No need toospecify an encryption resolver for retrieve, but it is harmless tooleave hello property set.
my_table_service.get_entity(table_name, entity['PartitionKey'], entity['RowKey'])
```

### <a name="using-attributes"></a>Przy użyciu atrybutów
Jak wspomniano powyżej, właściwość może być oznaczony do szyfrowania przez zapisanie go w obiekcie EntityProperty i ustawienie hello szyfrowania pola.

```python
encrypted_property_1 = EntityProperty(EdmType.STRING, value, encrypt=True)
```

## <a name="encryption-and-performance"></a>Szyfrowanie i wydajności
Należy pamiętać, że szyfrowania z magazynu danych spowoduje zmniejszenie wydajności. Witaj zawartości musi zostać wygenerowany klucz i IV samej zawartości hello muszą być szyfrowane i dodatkowe metadane muszą być sformatowane i przekazać. Ten narzut będą się różnić w zależności od ilości hello dane są zaszyfrowane. Zaleca się, że klienci zawsze testują wydajności w czasie projektowania.

## <a name="next-steps"></a>Następne kroki
* Pobierz hello [biblioteki klienta usługi Azure Storage dla języka Java PyPi pakietu](https://pypi.python.org/pypi/azure-storage)
* Pobierz hello [biblioteki klienta magazynu Azure do kodu źródłowego języka Python z witryny GitHub](https://github.com/Azure/azure-storage-python)
