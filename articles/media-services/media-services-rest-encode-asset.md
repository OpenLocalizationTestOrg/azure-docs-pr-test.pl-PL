---
title: "tooencode aaaHow zasobów platformy Azure przy użyciu standardu Media Encoder Standard | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Media Encoder Standard tooencode nośnika zawartości w usłudze Azure Media Services. Przykłady kodu za pomocą interfejsu API REST."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2a7273c6-8a22-4f82-9bfe-4509ff32d4a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b766bafded7ee98eda3e6ef149c31d5d8fe406fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencode-an-asset-by-using-media-encoder-standard"></a>Jak tooencode zasobów przy użyciu standardu Media Encoder Standard
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [REST](media-services-rest-encode-asset.md)
> * [Portal](media-services-portal-encode.md)
>
>

## <a name="overview"></a>Omówienie
toodeliver wideo za pośrednictwem hello Internet, trzeba skompresować hello nośnika. Cyfrowe pliki wideo większych i może być zbyt duży toodeliver za pośrednictwem Internetu hello, lub dla klientów urządzeń toodisplay poprawnie. Kodowanie jest procesem hello kompresji audio i wideo, więc klienci mogą wyświetlać multimediów.

Zadania kodowania są jednym z najbardziej typowych operacji przetwarzania hello w usłudze Azure Media Services. Utworzysz kodowania plików multimedialnych tooconvert zadań z jednego tooanother kodowania. Podczas kodowania, można użyć hello Media Services wbudowanych kodera (Media Encoder Standard). Umożliwia także kodera świadczonych przez partnera usługi Media Services. Kodery innych firm są dostępne za pośrednictwem hello Azure Marketplace. Można określić szczegółów hello kodowania zadań za pomocą ciągi ustawień wstępnych zdefiniowane dla kodera lub za pomocą plików konfiguracji wstępnie zdefiniowane. typy hello toosee ustawień, które są dostępne, zobacz [ustawień wstępnych zadań dla standardu Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).

Każde zadanie może zawierać jeden lub więcej zadań, w zależności od typu hello przetwarzania, które mają tooaccomplish. Za pomocą interfejsu API REST hello można utworzyć zadania i ich zadania pokrewne w jeden z dwóch sposobów:

* Zadania mogą być zdefiniowano w tekście za pośrednictwem właściwości nawigacji zadania hello na jednostkach zadania.
* Użyj przetwarzanie wsadowe OData.

Firma Microsoft zaleca zawsze kodowanie plików źródłowych do adaptacyjnej szybkości bitowej MP4 zestawu, a następnie wykonać konwersję hello zestaw toohello pożądany format przy użyciu [dynamicznego tworzenia pakietów](media-services-dynamic-packaging-overview.md).

Jeśli dane wyjściowe zawartości jest szyfrowany w magazynie, musisz skonfigurować zasady dostarczania elementu zawartości hello. Aby uzyskać więcej informacji, zobacz [Konfigurowanie zasad dostarczania elementów zawartości](media-services-rest-configure-asset-delivery-policy.md).

## <a name="considerations"></a>Zagadnienia do rozważenia

Podczas uzyskiwania dostępu do obiektów w usłudze Media Services, należy ustawić określonych pól nagłówka i wartości w Twoich żądań HTTP. Aby uzyskać więcej informacji, zobacz [ustawień dla rozwoju interfejsu API REST usługi Media](media-services-rest-how-to-use.md).

Przed rozpoczęciem odwołujące się do procesory multimediów, sprawdź, czy ma hello identyfikator prawidłowy nośnik procesora. Aby uzyskać więcej informacji, zobacz [uzyskać procesory multimediów](media-services-rest-get-media-processor.md).

## <a name="connect-toomedia-services"></a>Połączenie usług tooMedia

Aby uzyskać informacje dotyczące tooconnect toohello AMS interfejsu API, zobacz temat [hello dostępu do interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Po pomyślnym połączeniu toohttps://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów. Należy wykonać kolejne wywołania toohello nowy identyfikator URI.

## <a name="create-a-job-with-a-single-encoding-task"></a>Utwórz zadanie z jednego zadania kodowania
> [!NOTE]
> Podczas pracy z hello interfejsu API REST usług Media hello następujące kwestie:
>
> Podczas uzyskiwania dostępu do obiektów w usłudze Media Services, należy ustawić określonych pól nagłówka i wartości w Twoich żądań HTTP. Aby uzyskać więcej informacji, zobacz [ustawień dla rozwoju interfejsu API REST usług Media](media-services-rest-how-to-use.md).
>
> Po pomyślnym połączeniu toohttps://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów. Należy wykonać kolejne wywołania toohello nowy identyfikator URI. Aby uzyskać informacje dotyczące tooconnect toohello AMS interfejsu API, zobacz temat [hello dostępu do interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md).
>
> Gdy przy użyciu formatu JSON i określając toouse hello **__metadata** — słowo kluczowe w żądaniu hello (na przykład tooreferences obiektu połączonego), należy ustawić hello **Zaakceptuj** nagłówka zbyt[format trybu informacji pełnej JSON ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Zaakceptuj: application/json; odata = pełne.
>
>

Hello poniższy przykład przedstawia toocreate i post zadania jednego zadania konfiguracji tooencode wideo w określonej rozdzielczości i jakości. Podczas kodowania przy użyciu Media Encoder Standard, można użyć ustawienia konfiguracji zadania określony [tutaj](http://msdn.microsoft.com/library/mt269960).

Żądanie:

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net

    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aaab7f15b-3136-4ddf-9962-e9ecb28fb9d2')"}}],  "Tasks" : [{"Configuration" : "Adaptive Streaming", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",  "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"}]}

Odpowiedź:

    HTTP/1.1 201 Created

    . . .

### <a name="set-hello-output-assets-name"></a>Ustaw nazwę zawartości wyjściowej hello
Witaj poniższy przykład pokazuje, jak tooset hello assetName atrybutu:

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a>Zagadnienia do rozważenia
* Taskbody — właściwości należy użyć literału XML toodefine hello numer wejściowego lub wyjściowego zasobów, które są używane przez zadanie hello. temat zadania Hello zawiera hello definicji schematu XML dla hello XML.
* W definicji taskbody — Witaj, wartość każdego wewnętrzny <inputAsset> i <outputAsset> musi być ustawiona jako JobInputAsset(value) lub JobOutputAsset(value).
* Zadanie może mieć wielu zasobów danych wyjściowych. Jako dane wyjściowe zadania w ramach zadania jeden JobOutputAsset(x) można można użyć tylko raz.
* JobInputAsset lub JobOutputAsset można określić jako zasób wprowadzania zadania.
* Zadania musi nie tworzą cyklu.
* parametr wartość Hello przekazujesz tooJobInputAsset lub JobOutputAsset reprezentuje hello wartość indeksu dla zasobu. zasoby rzeczywiste hello są definiowane w hello InputMediaAssets i OutputMediaAssets właściwości nawigacji na powitania definicję jednostki.
* Ponieważ usługi Media Services jest oparty na OData v3, hello poszczególne zasoby w hello InputMediaAssets i kolekcje właściwości nawigacji OutputMediaAssets są przywoływane przez "__metadata: identyfikator uri" pary nazwa wartość.
* InputMediaAssets mapuje tooone lub więcej zasobów, które zostały utworzone w usłudze Media Services. OutputMediaAssets są tworzone przez hello system. Nie odwołujących się do istniejącego zasobu.
* OutputMediaAssets może nosić przy użyciu atrybutu assetName hello. Jeśli ten atrybut nie jest obecny, a następnie nazwę hello hello OutputMediaAsset jest niezależnie od wartości tekst wewnętrzny hello hello <outputAsset> element jest z sufiksem hello Nazwa zadania wartość lub wartość identyfikatora zadania hello (w przypadku hello, w których właściwość Name hello nie jest zdefiniowana). Na przykład jeśli zostanie ustawiona wartość assetName zbyt "Test", a następnie hello nazwa OutputMediaAsset właściwość jest ustawiona zbyt "Sample." Jednak jeśli nie zostały ustawione na wartość assetName, ale ustawiona nazwa zadania hello zbyt "NewJob", a następnie hello nazwa OutputMediaAsset się "_NewJob JobOutputAsset (wartość)".

## <a name="create-a-job-with-chained-tasks"></a>Utwórz zadanie z zadaniami łańcuchowa
W wielu scenariuszach aplikacji deweloperzy mają toocreate szereg przetwarzania zadań. W usłudze Media Services można utworzyć serię zadań łańcuchowych. Każde zadanie wykonuje kroki przetwarzania różnych i używać procesorów innego nośnika. zadania Hello łańcuchowej oddać zasobów z jednego zadania tooanother, wykonywanie liniowej sekwencji zadań na powitania zasobów. Jednak hello zadania wykonywane w ramach zadania nie są wymagane toobe w sekwencji. Podczas tworzenia zadania łańcuchowa hello łańcuchowej **ITask** obiekty są tworzone w jednej **IJob** obiektu.

> [!NOTE]
> Obecnie istnieje limit 30 zadań dla zadania. Jeśli potrzebujesz toochain ponad 30 zadań, należy utworzyć więcej niż jedno zadanie toocontain hello zadania.
>
>

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://testrest.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A910ffdc1-2e25-4b17-8a42-61ffd4b8914c')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          },
          {  
             "Configuration":"H264 Smooth Streaming 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-16\"?><taskBody><inputAsset>JobOutputAsset(0)</inputAsset><outputAsset>JobOutputAsset(1)</outputAsset></taskBody>"
          }
       ]
    }


### <a name="considerations"></a>Zagadnienia do rozważenia
Tworzenie łańcuchów tooenable zadań:

* Zadanie musi mieć co najmniej dwa zadania.
* Musi istnieć co najmniej jedno zadanie, którego dane wejściowe są dane wyjściowe hello inne zadanie w zadaniu hello.

## <a name="use-odata-batch-processing"></a>Przetwarzanie wsadowe OData
Witaj poniższy przykład pokazuje, jak toouse OData partii toocreate przetwarzania zadania i zadania. Informacje dotyczące przetwarzania wsadowego znajdują się w temacie [przetwarzanie wsadowe Open Data Protocol (OData)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).

    POST https://media.windows.net/api/$batch HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: multipart/mixed; boundary=batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Accept: multipart/mixed
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net


    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Content-Type: multipart/mixed; boundary=changeset_122fb0a4-cd80-4958-820f-346309967e4d

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-ID: 1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {"Name" : "NewTestJob", "InputMediaAssets@odata.bind":["https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A2a22445d-1500-80c6-4b34-f1e5190d33c6')"]}

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/$1/Tasks HTTP/1.1
    Content-ID: 2
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
       "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
       "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"Custom output name\">JobOutputAsset(0)</outputAsset></taskBody>"
    }

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d--
    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e--



## <a name="create-a-job-by-using-a-jobtemplate"></a>Utwórz zadanie przy użyciu obiekt JobTemplate
Podczas przetwarzania wielu zasobów za pomocą zbiór typowych zadań, użyj ustawienia zadania domyślny obiekt JobTemplate toospecify hello lub tooset hello kolejność zadań.

Witaj poniższy przykład pokazuje, jak obiekt JobTemplate z TaskTemplate, który jest toocreate zdefiniowanymi w tekście. Witaj TaskTemplate używa hello Media Encoder Standard jako hello MediaProcessor tooencode hello zawartości pliku. Jednak inne MediaProcessors może służyć także.

    POST https://media.windows.net/API/JobTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewJobTemplate25", "JobTemplateBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><jobTemplate><taskBody taskTemplateId=\"nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789\"><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody></jobTemplate>", "TaskTemplates" : [{"Id" : "nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789", "Configuration" : "H264 Smooth Streaming 720p", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56", "Name" : "SampleTaskTemplate2", "NumberofInputAssets" : 1, "NumberofOutputAssets" : 1}] }


> [!NOTE]
> W przeciwieństwie do innych jednostek usługi Media Services musi Zdefiniuj nowy identyfikator GUID dla każdego TaskTemplate i umieścić w hello taskTemplateId i właściwość identyfikatora w treści na żądanie. Schemat identyfikacji zawartości Hello wykonaj schematu hello opisanego w zidentyfikować Azure Media Services jednostek. Ponadto nie można zaktualizować JobTemplates. Zamiast tego należy utworzyć nową zaktualizowanych zmian.
>
>

W przypadku powodzenia powitania po odpowiedzi jest zwracany:

    HTTP/1.1 201 Created

    . . .


powitania po przykładzie pokazano, jak toocreate zadania, który odwołuje się do identyfikatora obiekt JobTemplate:

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


W przypadku powodzenia powitania po odpowiedzi jest zwracany:

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Następne kroki
Teraz, znając toocreate tooencode zadania usługi zasobów, zobacz temat [jak toocheck zadania postępu za pomocą usługi Media Services](media-services-rest-check-job-progress.md).

## <a name="see-also"></a>Zobacz też
[Pobierz procesory multimediów](media-services-rest-get-media-processor.md)
