---
title: "toouse aaaHow magazynu obiektów Blob w oprogramowaniu Node.js | Dokumentacja firmy Microsoft"
description: "Przechowuj dane niestrukturalne w chmurze hello z magazynu obiektów Blob platformy Azure (obiekt magazynu)."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 8b0df222-1ca8-4967-8248-6d6d720947b8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: e405eecdc60cd1eaa77510e7b29b41269372b65e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-nodejs"></a>Jak toouse magazynu obiektów Blob w oprogramowaniu Node.js
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a>Omówienie
W tym artykule opisano sposób tooperform typowych scenariuszy przy użyciu magazynu obiektów Blob. Przykłady Hello są zapisywane przez hello interfejsu API środowiska Node.js. omówione scenariusze Hello obejmują jak tooupload, listy, pobieranie i usuwanie obiektów blob.

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a>Tworzenie aplikacji w języku Node.js
Aby uzyskać instrukcje dotyczące toocreate aplikacji Node.js, zobacz [tworzenie aplikacji sieci web Node.js w usłudze Azure App Service], [tworzenie i wdrażanie tooan aplikacji Node.js usługi w chmurze Azure] — za pomocą środowiska Windows PowerShell , lub [tworzenie i wdrażanie tooAzure aplikacji sieci web Node.js za pomocą macierzy sieci Web].

## <a name="configure-your-application-tooaccess-storage"></a>Konfigurowanie magazynu tooaccess aplikacji
toouse magazynu Azure, należy hello zestawu SDK usługi Magazyn Azure dla środowiska Node.js, w tym zestaw wygody bibliotek, które komunikują się z usługi REST magazynu hello.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Użyj pakietu hello tooobtain węzeł Menedżera pakietów (NPM)
1. Użyj interfejsu wiersza polecenia, takich jak **środowiska PowerShell** (system Windows), **terminali** (Mac), lub **Bash** (Unix), toonavigate toohello folder, w którym utworzono przykładu aplikacja.
2. Typ **magazyn azure instalacji narzędzia npm** w oknie polecenia hello. Dane wyjściowe polecenia hello jest toohello podobnie poniższy przykład kodu.

        azure-storage@0.5.0 node_modules\azure-storage
        +-- extend@1.2.1
        +-- xmlbuilder@0.4.3
        +-- mime@1.2.11
        +-- node-uuid@1.4.3
        +-- validator@3.22.2
        +-- underscore@1.4.4
        +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
        +-- xml2js@0.2.7 (sax@0.5.2)
        +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. Możesz ręcznie uruchomić hello **ls** tooverify polecenia który **węzła\_modułów** folder został utworzony. W tym folderze, Znajdź hello **magazyn azure** pakiet, który zawiera biblioteki hello konieczność tooaccess magazynu.

### <a name="import-hello-package"></a>Importowanie pakietu hello
Za pomocą Notatnika lub innego edytora tekstu, dodać powitania od góry toohello hello **server.js** pliku aplikacji hello, w którym ma toouse magazynu:

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a>Konfigurowanie połączenia z magazynem Azure
Hello Azure modułu odczyta zmiennych środowiskowych hello `AZURE_STORAGE_ACCOUNT` i `AZURE_STORAGE_ACCESS_KEY`, lub `AZURE_STORAGE_CONNECTION_STRING`, informacje wymagane tooconnect tooyour konto magazynu Azure. Jeśli te zmienne środowiskowe nie są skonfigurowane, należy określić informacje o koncie hello podczas wywoływania metody **createBlobService**.

Na przykład ustawienia zmiennych środowiskowych hello w hello [portalu Azure](https://portal.azure.com) dla aplikacji sieci web platformy Azure, zobacz [aplikacji sieci web Node.js w usłudze hello Azure usługa tabel].

## <a name="create-a-container"></a>Tworzenie kontenera
Witaj **BlobService** obiektu umożliwia pracę z kontenerów i obiektów blob. Witaj poniższy kod tworzy **BlobService** obiektu. Dodaj następujące hello u góry hello **server.js**:

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> Dostęp obiektu blob anonimowo za pomocą **createBlobServiceAnonymous** i podając adres hosta hello. Na przykład użyć `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

Użyj toocreate nowy kontener **createContainerIfNotExists**. Witaj poniższy przykład kodu tworzy nowy kontener o nazwie "mojkontener":

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

Jeśli kontener hello jest nowo utworzony, `result.created` ma wartość true. Jeśli istnieje już hello kontenera, `result.created` ma wartość false. `response`zawiera informacje na temat operacji hello, w tym informacje o ETag hello hello kontenera.

### <a name="container-security"></a>Kontener zabezpieczeń
Domyślnie nowe kontenery są prywatne i nie można uzyskać dostępu do anonimowo. kontener hello toomake publiczna, dzięki czemu można do niego dostęp anonimowo kontenera hello poziom dostępu można ustawić także**obiektu blob** lub **kontenera**.

* **Obiekt blob** — zezwala na zawartość tooblob anonimowy dostęp do odczytu i metadanych, w tym kontenerze, ale nie toocontainer metadane, takie jak wyświetlanie listy wszystkich obiektów blob w kontenerze
* **kontener** — zezwala na zawartość tooblob anonimowy dostęp do odczytu i metadanych, tak jak metadanych kontenera

Witaj poniższy przykład kodu pokazuje poziom dostępu hello ustawienie zbyt**obiektu blob**:

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access tooblob
      // content and metadata within this container
    }
});
```

Alternatywnie można zmodyfikować poziomu dostępu hello kontenera za pomocą **setContainerAcl** poziom dostępu hello toospecify. Witaj poniższy kod toocontainer poziomu dostępu przykład zmiany hello:

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set too'container'
  }
});
```

Witaj wynik zawiera informacje na temat operacji hello, łącznie z bieżącym hello **ETag** hello kontenera.

### <a name="filters"></a>Filtry
Możesz zastosować opcjonalne filtrowania operacji toooperations wykonywane przy użyciu **BlobService**. Filtrowanie operacje mogą obejmować rejestrowania, Automatyczne ponawianie próby itp. Obiekty, które implementują metodę podpisem hello są następujące filtry:

```nodejs
function handle (requestOptions, next)
```

Po wykonaniu przetwarzanie wstępne opcje żądania hello, metoda hello musi toocall "dalej", przekazywanie wywołania zwrotnego z powitania po podpisaniu:

```nodejs
function (returnObject, finalCallback, next)
```

W tym wywołania zwrotnego, a po przetworzeniu hello returnObject (hello odpowiedź z serwera toohello żądania hello), wywołania zwrotnego hello musi tooeither obok wywołać, jeśli istnieje toocontinue przetwarzania inne filtry lub po prostu Wywołaj finalCallback tooend hello usługi wywołania.

Dwa filtry, które implementują logikę ponawiania są dołączone hello Azure SDK dla środowiska Node.js, **ExponentialRetryPolicyFilter** i **LinearRetryPolicyFilter**. tworzy następujące Hello **BlobService** obiekt, który używa hello **ExponentialRetryPolicyFilter**:

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a>Przekazywanie obiektu blob do kontenera
Istnieją trzy typy obiektów blob: blokowe obiekty BLOB, stronicowe i uzupełnialne. Blokowe obiekty BLOB umożliwiają toomore wydajnie Przekaż dużej ilości danych. Dołącz obiekty BLOB są zoptymalizowane pod kątem operacji dołączania. Stronicowe obiekty BLOB są zoptymalizowane pod kątem operacji odczytu/zapisu. Aby uzyskać więcej informacji, zobacz [opis blokowych obiektów blob, Dołącz obiektów blob i stronicowe obiekty BLOB](http://msdn.microsoft.com/library/azure/ee691964.aspx).

### <a name="block-blobs"></a>Obiekty BLOB typu Block
tooupload danych tooa blokowych obiektów blob, użyj hello następujące:

* **createBlockBlobFromLocalFile** — tworzy nowy obiekt blob blokowy i przekazuje hello zawartość pliku
* **createBlockBlobFromStream** — tworzy nowy obiekt blob blokowy i przekazuje hello zawartość strumienia
* **createBlockBlobFromText** — tworzy nowy obiekt blob blokowy i przekazuje ciąg hello zawartość
* **createWriteStreamToBlockBlob** — zapewnia zapisu strumienia tooa blokowego obiektu blob

Witaj poniższy przykład kodu przekazuje zawartość hello hello **test.txt** pliku do **mojblob**.

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

Witaj `result` zwrócony przy użyciu tej metody zawiera informacje na temat operacji hello, takiej jak hello **ETag** hello obiektu blob.

### <a name="append-blobs"></a>Uzupełnialnych obiektów blob
nowe tooa danych tooupload Dołącz obiektów blob, należy użyć następującego hello:

* **createAppendBlobFromLocalFile** — tworzy nowy uzupełnialny obiekt blob i przekazuje hello zawartość pliku
* **createAppendBlobFromStream** — tworzy nowy uzupełnialny obiekt blob i przekazuje hello zawartość strumienia
* **createAppendBlobFromText** — tworzy nowy uzupełnialny obiekt blob i przekazuje ciąg hello zawartość
* **createWriteStreamToNewAppendBlob** — tworzy nowy uzupełnialny obiekt blob, a następnie oferuje tooit toowrite strumienia

Witaj poniższy przykład kodu przekazuje zawartość hello hello **test.txt** pliku do **myappendblob**.

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

tooappend istniejących tooan bloku Dołącz obiektów blob, użyj hello następujące:

* **appendFromLocalFile** -Dołącz zawartość hello tooan pliku istniejących Dołącz obiektów blob
* **appendFromStream** -Dołącz zawartość hello tooan strumienia istniejących Dołącz obiektów blob
* **appendFromText** -Dołącz zawartość hello tooan ciąg istniejących Dołącz obiektów blob
* **appendBlockFromStream** -Dołącz zawartość hello tooan strumienia istniejących Dołącz obiektów blob
* **appendBlockFromText** -Dołącz zawartość hello tooan ciąg istniejących Dołącz obiektów blob

> [!NOTE]
> interfejsy API appendFromXXX wykona niektóre połączenia serwera niepotrzebnych szybkiego tooavoid toofail weryfikacji po stronie klienta. nie będzie appendBlockFromXXX.
>
>

Witaj poniższy przykład kodu przekazuje zawartość hello hello **test.txt** pliku do **myappendblob**.

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text toobe appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a>Stronicowe obiekty blob
tooupload danych tooa stronicowych obiektów blob, użyj hello następujące:

* **createPageBlob** — tworzy nowy stronicowych obiektów blob o określonej długości
* **createPageBlobFromLocalFile** — tworzy nowy stronicowych obiektów blob i przekazuje hello zawartość pliku
* **createPageBlobFromStream** — tworzy nowy stronicowych obiektów blob i przekazuje hello zawartość strumienia
* **createWriteStreamToExistingPageBlob** — zapewnia zapisu strumienia tooan istniejących stronicowy obiekt blob
* **createWriteStreamToNewPageBlob** — tworzy nowy stronicowych obiektów blob, a następnie oferuje tooit toowrite strumienia

Witaj poniższy przykład kodu przekazuje zawartość hello hello **test.txt** pliku do **mypageblob**.

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> Stronicowe obiekty BLOB składać się z 512-bajtowych "stron". Podczas przekazywania danych o rozmiarze, który nie jest wielokrotnością 512, zostanie zwrócony błąd.
>
>

## <a name="list-hello-blobs-in-a-container"></a>Lista hello BLOB w kontenerze
toolist hello BLOB w kontenerze, użyj hello **listBlobsSegmented** metody. Jeśli chcesz obiektów blob tooreturn z określonego prefiksu, użyj **listBlobsSegmentedWithPrefix**.

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains hello entries
      // If not all blobs were returned, result.continuationToken has hello continuation token.
  }
});
```

Witaj `result` zawiera `entries` kolekcji, która jest Tablica obiektów, które opisują każdy obiekt blob. Jeśli nie można zwrócić wszystkie obiekty BLOB, hello `result` udostępnia również `continuationToken`, którego można użyć jako hello drugi parametr tooretrieve dodatkowe wpisy.

## <a name="download-blobs"></a>Pobieranie obiektów blob
toodownload danych z obiektu blob, użyj następujących hello:

* **getBlobToLocalFile** -zapisuje toofile zawartość obiektu blob hello
* **getBlobToStream** -zapisuje strumienia tooa zawartość obiektu blob hello
* **getBlobToText** -zapisuje zawartość obiektu blob hello tooa ciąg
* **createReadStream** — zapewnia tooread strumień z obiektu blob hello

Hello poniższy przykład kodu pokazuje przy użyciu **getBlobToStream** toodownload zawartość hello hello **mojblob** obiektu blob i zapisz go w toohello **output.txt** plików za pomocą Strumień:

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

Witaj `result` zawiera informacje dotyczące obiektów blob hello, w tym **ETag** informacji.

## <a name="delete-a-blob"></a>Usuwanie obiektu blob
Na koniec wywołania toodelete obiektu blob **deleteBlob**. Witaj, poniższy przykład kodu usuwa hello obiektu blob o nazwie **mojblob**.

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a>Współbieżny dostęp
toosupport współbieżny dostęp tooa dużego obiektu binarnego z wielu klientów lub wielu wystąpień procesu, można użyć **elementy etag** lub **dzierżawy**.

* **Element etag** — zapewnia toodetect sposób, który hello obiektów blob lub kontener został zmodyfikowany przez inny proces
* **Dzierżawy** — zapewnia zapisu sposób tooobtain wyłączności, może być wznawiane, lub usunąć obiektu blob tooa dostępu w danym okresie czasu

### <a name="etag"></a>Element ETag
Elementy etag należy użyć, jeśli potrzebujesz tooallow wielu klientów lub wystąpień toowrite toohello blokowych obiektów Blob lub strona obiektu Blob jednocześnie. Witaj ETag pozwala toodetermine Jeśli hello kontener lub obiekt blob został zmodyfikowany od czasu początkowo odczytu lub utworzone, dzięki czemu można tooavoid nadpisaniem zmian dokonanych przez innego klienta lub inny proces.

Można ustawić warunki ETag przy użyciu hello opcjonalne `options.accessConditions` parametru. Witaj Poniższy przykładowy kod tylko przekazuje hello **test.txt** pliku, jeśli obiekt blob hello już istnieje i ma wartość ETag hello zawarty w `etagToMatch`.

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

Jeśli używasz elementy etag wzorzec ogólne hello jest:

1. Uzyskaj hello ETag wyniku hello Utwórz, listy lub operacji get.
2. Wykonaj akcję, sprawdzanie tego hello wartość ETag nie został zmodyfikowany.

Jeśli wartość hello został zmodyfikowany, to wskazuje, że innego klienta lub wystąpienia obiektu blob hello lub kontener ponieważ uzyskać wartość ETag hello.

### <a name="lease"></a>Dzierżawy
Możesz uzyskać nową dzierżawę za pomocą hello **acquireLease** metoda określania hello blob lub kontenera, które chcesz tooobtain dzierżawę na. Na przykład powitania po kod uzyskuje dzierżawę na **mojblob**.

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

Kolejne operacje na **mojblob** podać hello `options.leaseId` parametru. dzierżawy Hello identyfikator jest zwracana jako `result.id` z **acquireLease**.

> [!NOTE]
> Domyślnie czas trwania dzierżawy hello jest nieograniczony. Czas trwania — bez ograniczeń czasowych (od 15 do 60 sekund) można określić, zapewniając hello `options.leaseDuration` parametru.
>
>

Użyj tooremove dzierżawę, **releaseLease**. toobreak dzierżawy, ale uniemożliwia innym uzyskaniu nowej dzierżawy, dopóki nie wygasł czas trwania oryginalnego hello, użyj funkcji **breakLease**.

## <a name="work-with-shared-access-signatures"></a>Praca z sygnatury dostępu współdzielonego
Sygnatury dostępu współdzielonego (SAS) są tooblobs bezpieczny sposób tooprovide szczegółowego dostępu i kontenery bez podawania Twojej nazwy konta magazynu i klucze. Sygnatury dostępu współdzielonego są często używane tooprovide ograniczony dostęp tooyour dane, takie jak stosowanie aplikacji mobilnej tooaccess obiektów blob.

> [!NOTE]
> Gdy, możesz również zezwolić tooblobs dostępu anonimowego, sygnatur dostępu współdzielonego pozwalają tooprovide więcej pod kontrolą dostępu, jak należy wygenerować hello sygnatury dostępu Współdzielonego.
>
>

Zaufanych aplikacji, takich jak jest usługą opartą na chmurze generuje sygnatur dostępu współdzielonego przy użyciu hello **generateSharedAccessSignature** z hello **BlobService**i udostępnia go tooan niezaufanych lub częściowo zaufanych aplikacji takich jak aplikacji mobilnej. Dostępu współdzielonego podpisów, zostaną wygenerowane za pomocą zasad, które opisano hello rozpoczęcia i daty zakończenia, podczas których hello sygnatur dostępu współdzielonego są prawidłowe, a także hello dostęp do poziomu nadanego posiadacz sygnatur dostępu współdzielonego toohello.

Witaj poniższy przykład kodu generuje nowe zasady dostępu współdzielonego, które umożliwia tooperform symbol zastępczy sygnatur dostępu hello udostępniony operacje na powitania odczytu **mojblob** obiektu blob i wygasa 100 minut po godzinie hello jest tworzona.

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
};

var blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', 'myblob', sharedAccessPolicy);
var host = blobSvc.host;
```

Należy pamiętać, że informacji o hoście hello należy dostarczyć także zgodnie z wymaganiami podczas posiadacz sygnatur dostępu współdzielonego hello prób tooaccess hello kontenera.

Witaj następnie aplikacja kliencka używa sygnatur dostępu współdzielonego z **BlobServiceWithSAS** tooperform operacji względem hello obiektu blob. Witaj następujące pobiera informacje **mojblob**.

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

Ponieważ sygnatur dostępu hello udostępnione zostały wygenerowane z dostępem tylko do odczytu, jeśli obiekt blob hello toomodify podejmowana jest próba, zostanie zwrócony błąd.

### <a name="access-control-lists"></a>Listy kontroli dostępu
Umożliwia także zasady kontroli dostępu listę kontroli dostępu (ACL) tooset hello dostępu dla sygnatury dostępu Współdzielonego. Jest to przydatne, jeśli chcesz tooallow wielu klientów tooaccess kontener, ale zapewniają różne zasady dostępu dla każdego klienta.

Listy ACL jest zaimplementowana przy użyciu tablicy zasad dostępu w usłudze identyfikator skojarzony z każdej zasady. Witaj poniższy przykład kodu definiuje dwie zasady, jeden dla "Użytkownik1" i jeden dla "uzytkownik2":

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.WRITE,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

powitania po pobiera przykładowy kod hello bieżącej listy ACL dla **mojkontener**, a następnie dodaje nowe zasady hello przy użyciu **setBlobAcl**. Takie podejście umożliwia:

```nodejs
var extend = require('extend');
blobSvc.getBlobAcl('mycontainer', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    blobSvc.setBlobAcl('mycontainer', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Raz hello ustawione listy ACL, następnie można utworzyć na podstawie Identyfikatora hello zasad sygnatur dostępu współdzielonego. Witaj poniższy przykład kodu tworzy nowe sygnatury dostępu współdzielonego dla "uzytkownik2":

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji zobacz następujące zasoby hello.

* [Magazyn Azure SDK dla węzła dokumentacja interfejsu API][Azure Storage SDK for Node API Reference]
* [Blog zespołu usługi Magazyn Azure][Azure Storage Team Blog]
* [Zestaw Azure SDK magazynu dla węzła] [ Azure Storage SDK for Node] repozytorium w witrynie GitHub
* [Centrum deweloperów środowiska Node.js](https://azure.microsoft.com/develop/nodejs/)
* [Transfer danych za pomocą hello wiersza polecenia azcopy](storage-use-azcopy.md)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

[tworzenie aplikacji sieci web Node.js w usłudze Azure App Service]: ../app-service-web/app-service-web-get-started-nodejs.md
[aplikacji sieci web Node.js w usłudze hello Azure usługa tabel]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md
[tworzenie i wdrażanie tooAzure aplikacji sieci web Node.js za pomocą macierzy sieci Web]: ../app-service-web/web-sites-nodejs-use-webmatrix.md
[Using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure portal]: https://portal.azure.com
[tworzenie i wdrażanie tooan aplikacji Node.js usługi w chmurze Azure]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Storage SDK for Node API Reference]: http://dl.windowsazure.com/nodestoragedocs/index.html
