---
title: "aaaConfigure ciąg połączenia dla usługi Azure Storage | Dokumentacja firmy Microsoft"
description: "Skonfiguruj parametry połączenia dla konta magazynu platformy Azure. Parametry połączenia zawierają informacje hello wymagany tooauthenticate dostępu konta magazynu tooa z aplikacji w czasie wykonywania."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: ecb0acb5-90a9-4eb2-93e6-e9860eda5e53
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: marsma
ms.openlocfilehash: ac1d7d9bf11fa6f44243cda0c40d8faee12e513b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-storage-connection-strings"></a>Konfiguracja parametrów połączenia usługi Azure Storage

Ciąg połączenia zawiera informacje dotyczące uwierzytelniania hello wymagane dla danych aplikacji tooaccess na koncie magazynu Azure w czasie wykonywania. Można skonfigurować parametry połączenia do:

* Połącz toohello emulatora magazynu Azure.
* Dostęp do konta magazynu na platformie Azure.
* Dostęp do określonych zasobów na platformie Azure za pomocą sygnatury dostępu współdzielonego (SAS).

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a>Przechowywanie parametrów połączenia
Aplikacja wymaga parametrów połączenia hello tooaccess w tooAzure żądań tooauthenticate środowiska uruchomieniowego magazynu. Istnieje kilka opcji do przechowywania parametrów połączenia:

* Uruchomiona aplikacja hello pulpitu lub na urządzeniu mogą być przechowywane w ciągu połączenia hello **app.config** lub **web.config** pliku. Dodaj toohello ciąg połączenia hello **AppSettings** sekcji w tych plikach.
* Aplikacji uruchomionej w usłudze w chmurze platformy Azure można przechowywać parametry połączenia hello w hello [plik schematu (cscfg) konfiguracji usługi Azure](https://msdn.microsoft.com/library/ee758710.aspx). Dodaj toohello ciąg połączenia hello **appSettings** sekcji pliku konfiguracji usługi hello.
* Parametry połączenia można użyć bezpośrednio w kodzie. Firma Microsoft zaleca jednak przechowywanie parametrów połączenia w pliku konfiguracji, w większości przypadków.

Przechowywanie parametrów połączenia w pliku konfiguracji umożliwia łatwe tooupdate hello połączenia ciąg tooswitch między hello emulatora magazynu i konto magazynu platformy Azure w chmurze hello. Wystarczy tylko środowiska docelowego tooyour toopoint ciąg tooedit hello połączenia.

Można użyć hello [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) tooaccess ciągu połączenia w czasie wykonywania, niezależnie od tego, w którym aplikacja jest uruchomiona.

## <a name="create-a-connection-string-for-hello-storage-emulator"></a>Utworzyć parametry połączenia dla emulatora magazynu hello
[!INCLUDE [storage-emulator-connection-string-include](../../../includes/storage-emulator-connection-string-include.md)]

Aby uzyskać więcej informacji na temat hello emulatora magazynu, zobacz [użyć emulatora magazynu Azure hello do projektowania i testowania](storage-use-emulator.md).

## <a name="create-a-connection-string-for-an-azure-storage-account"></a>Utworzyć parametry połączenia dla konta magazynu platformy Azure
toocreate ciąg połączenia dla konta magazynu Azure, użyj następującego hello formatu. Wskazuje, czy konto magazynu toohello tooconnect za pośrednictwem protokołu HTTPS (zalecane), czy HTTP, Zastąp `myAccountName` o nazwie hello swojego konta magazynu i Zastąp `myAccountKey` kluczem dostępu do konta:

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

Na przykład parametry połączenia mogą wyglądać podobnie do:

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

Mimo że usługa Azure Storage obsługuje protokołów HTTP i HTTPS w parametrach połączenia, *HTTPS jest zdecydowanie zalecane*.

> [!TIP]
> Parametry połączenia konta magazynu można znaleźć w hello [portalu Azure](https://portal.azure.com). Przejdź za**ustawienia** > **klucze dostępu** w parametry połączenia toosee bloku menu konta magazynu dla obu kluczy dostępu do podstawowego i pomocniczego.
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a>Utworzyć parametry połączenia przy użyciu sygnatury dostępu współdzielonego
[!INCLUDE [storage-use-sas-in-connection-string-include](../../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a>Utworzyć parametry połączenia dla punktu końcowego magazynu jawne
Punkty końcowe usługi jawne można określić w ciągu połączenia zamiast hello domyślne punkty końcowe. toocreate ciąg połączenia, który określa jawne punktu końcowego, określić dla każdej usługi, w tym hello Specyfikacja protokołu (HTTPS (zalecane) lub HTTP), punkt końcowy usługi pełną hello hello następującego formatu:

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

Jest jeden scenariusz, który może mają toospecify jawne punktu końcowego, gdy Twoje tooa punktu końcowego magazynu obiektów Blob jest zamapowany [domeny niestandardowej](../blobs/storage-custom-domain-name.md). W takim przypadku można określić niestandardowe punktu końcowego magazynu obiektów Blob w ciągu połączenia. Opcjonalnie można określić hello domyślnymi punktami końcowymi hello innych usług, jeśli aplikacja korzysta z nich.

Oto przykład parametrów połączenia, które określa jawne punktu końcowego w celu hello usługa Blob:

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

W tym przykładzie określa jawne punkty końcowe dla wszystkich usług, w tym niestandardową domenę na potrzeby hello usługa Blob:

```
# All service endpoints
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
FileEndpoint=https://myaccount.file.core.windows.net;
QueueEndpoint=https://myaccount.queue.core.windows.net;
TableEndpoint=https://myaccount.table.core.windows.net;
AccountName=storagesample;
AccountKey=<account-key>
```

wartości punktu końcowego Hello w parametrach połączenia są używane tooconstruct hello żądania usług magazynu toohello identyfikatory URI, a hello formę wszystkie identyfikatory URI, które są zwracane tooyour kodu jest wymagane przez.

Jeśli zamapowany magazynu domeny niestandardowej tooa punktu końcowego i pominąć ten punkt końcowy z parametrów połączenia, nie będzie możliwe toouse tego połączenia ciągu tooaccess danych w tej usłudze w kodzie.

> [!IMPORTANT]
> Wartości punktu końcowego usługi w parametry połączenia muszą być poprawnie sformułowanym identyfikatory URI, w tym `https://` (zalecane) lub `http://`. Ponieważ Magazyn Azure nie obsługuje jeszcze HTTPS dla domen niestandardowych można *musi* określ `http://` dla dowolnego punktu końcowego identyfikator URI, który wskazuje tooa domeny niestandardowej.
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a>Utworzyć parametry połączenia z sufiksem punktu końcowego
toocreate parametrów połączenia dla usługi magazynu w regionach lub wystąpień z innym punktem końcowym sufiksów, takich jak dla Chińskiej wersji platformy Azure lub Azure dla instytucji rządowych, hello Użyj następującego formatu ciągu połączenia. Wskazuje, czy konto magazynu toohello tooconnect za pośrednictwem protokołu HTTPS (zalecane), czy HTTP, Zastąp `myAccountName` o nazwie hello konta magazynu, należy zastąpić `myAccountKey` z klucz dostępu do konta i Zastąp `mySuffix` z hello identyfikatora URI sufiks:

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

Oto przykład parametry połączenia dla usług magazynu w chińskiej wersji platformy Azure:

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a>Podczas analizowania parametrów połączenia
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a>Następne kroki
* [Użyj hello emulatora magazynu Azure do programowania i testowania](storage-use-emulator.md)
* [Eksploratory usługi Storage platformy Azure](storage-explorers.md)
* [Przy użyciu sygnatury dostępu współdzielonego (SAS)](storage-dotnet-shared-access-signature-part-1.md)

