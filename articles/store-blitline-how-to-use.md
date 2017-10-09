---
title: "aaaHow toouse Blitline przetwarzania obrazu — Przewodnik po funkcji Azure"
description: "Dowiedz się, jak toouse hello Blitline usługi tooprocess obrazów w aplikacji Azure."
services: 
documentationcenter: .net
author: blitline-dev
manager: jason@blitline.com
editor: jason@blitline.com
ms.assetid: 6c711248-0e52-4895-ba9e-8395628de924
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2014
ms.author: support@blitline.com
ms.openlocfilehash: 328fd177e25f45f29f8ad8e142d02b46017a858e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blitline-with-azure-and-azure-storage"></a>Jak toouse Blitline z platformy Azure i magazynem Azure
W tym przewodniku objaśniają jak tooaccess Blitline usług i jak toosubmit zadania tooBlitline.

## <a name="what-is-blitline"></a>Co to jest Blitline?
Blitline to obraz oparte na chmurze usługa, która zapewnia przetwarzania obrazu poziomu przedsiębiorstwa w ułamku hello ceny czy koszt toobuild przetwarzania go samodzielnie.

fakt Hello jest, że przetwarzania obrazów przeprowadzono wielokrotnie, zwykle ponownie skompilowany od hello podstaw z myślą o każdym witryny sieci Web. Zdajemy sobie sprawę, to ponieważ już budujemy ich milionów razy zbyt. Jeden dzień, który zdecydowaliśmy się, że prawdopodobnie nadszedł czas, tak jak go dla wszystkich użytkowników. Wiemy, jak toodo on toodo on szybkiego i efektywnego i Zapisz wszyscy działać w hello czasu.

Aby uzyskać więcej informacji, zobacz [http://www.blitline.com](http://www.blitline.com).

## <a name="what-blitline-is-not"></a>Co Blitline nie...
tooclarify co Blitline jest przydatne dla jest często łatwiejsze tooidentify co Blitline, które nie są przed przeniesieniem do przodu.

* Blitline nie ma obrazów tooupload elementy widget HTML. Obrazy dostępne musi mieć publiczną lub z ograniczonymi uprawnieniami dostępne dla Blitline tooreach.
* Blitline nie działa na żywo przetwarzania obrazu, takich jak Aviary.com
* Blitline nie akceptuje przekazywania obrazów, nie można wypchnąć tooBlitline Twojego obrazy bezpośrednio. Należy wypchniesz tooAzure magazynu lub innych miejsc, który obsługuje Blitline i następnie poinformuj Blitline gdzie toogo uzyskać je.
* Blitline jest równoległemu i nie wykonuje żadnych przetwarzania synchronicznego. Co oznacza Podaj nam postback_url i możemy pomagają stwierdzić, gdy firma Microsoft gotowe przetwarzania.

## <a name="create-a-blitline-account"></a>Utwórz konto Blitline
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-toocreate-a-blitline-job"></a>Jak toocreate zadania Blitline
Blitline używa JSON toodefine hello akcje, które mają tootake na obrazie. Ten kod JSON składa się z kilku prostych pól.

Najprostsza przykład Witaj wygląda następująco:

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

W tym miejscu mamy JSON, który zajmie obrazu "src" "... boys.jpeg", a następnie zmień rozmiar tego obrazu too240x140.

Identyfikator aplikacji Hello to element znajduje się w sieci **informacje o połączeniu** lub **ZARZĄDZAJ** kartę na platformie Azure. Jest identyfikatorem tajny umożliwiająca zadania toorun na Blitline.

Witaj przycisk Zapisz, parametr identyfikuje informacji o miejscu tooput obraz powitania po możemy zostały przetworzone go. W tym przypadku trivial możemy jeszcze zdefiniowana. Jeśli lokalizacja nie jest zdefiniowany Blitline zapisze ją lokalnie (i tymczasowo) w lokalizacji unikatowy chmury. Będzie możliwe tooget, który lokalizacji z hello JSON zwrócony przez Blitline po wprowadzeniu hello Blitline. Identyfikator "obrazu" Hello jest wymagana i zwracany jest tooyou tooidentify zapisać tego określonego obrazu.

Można znaleźć więcej informacji na temat hello *funkcje* obsługujemy tutaj: <http://www.blitline.com/docs/functions>

Możesz również znaleźć dokumentację dotyczącą hello Opcje zadania tutaj: <http://www.blitline.com/docs/api>

Po określeniu, czy kod JSON toodo wystarczy **POST** on zbyt`http://api.blitline.com/job`

Otrzymasz wstecz JSON, który wygląda następująco:

    {
     "results":
         {"images":
            [{
              "image_identifier":"external_sample_1",
              "s3_url":"https://s3.amazonaws.com/dev.blitline/2011110722/YOUR_APP_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg"
            }],
          "job_id":"4eb8c9f72a50ee2a9900002f"
         }
    }


Oznacza to, Blitline odebrał żądanie, ma umieszcza je w kolejce przetwarzania i po zakończeniu hello obrazu będzie dostępna w: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_aplikacji\_ID /CK3f0xBF_2bV6wf7gEZE8w.jpg**

## <a name="how-toosave-an-image-tooyour-azure-storage-account"></a>Jak toosave tooyour obraz konta magazynu Azure
Jeśli masz konto usługi Azure Storage, mogą być Blitline wypychania hello przetwarzania obrazów do Twojej kontenera platformy Azure. Dodając "azure_destination" należy zdefiniować hello lokalizacji i uprawnienia do toopush Blitline do.

Oto przykład:

    job : '{
      "application_id": "YOUR_APP_ID",
      "src" : "http://www.google.com/logos/2011/houdini11-hp.jpg",
         "functions" : [{
         "name": "blur",
         "save" : {
             "image_identifier" : "YOUR_IMAGE_IDENTIFIER",
             "azure_destination" : {
                 "account_name" : "YOUR_AZURE_CONTAINER_NAME",
                 "shared_access_signature" : "SAS_THAT_GIVES_BLITLINE_PERMISSION_TO_WRITE_THIS_OBJECT_TO_CONTAINER",
               }
           }
         }]
       }'


Wypełniając hello CAPITALIZED wartości własnymi, można przesłać ten toohttp://api.blitline.com/job JSON i hello obrazu "src" będą przetwarzane z filtru rozmycia i następnie wypychana tooyou docelowej platformy Azure.

### <a name="please-note"></a>Uwaga:
Witaj SAS musi zawierać hello cały adres url SAS, włączając hello nazwa pliku docelowego hello.

Przykład:

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


Możesz przeczytać hello najnowszych wersji dokumentów usługi Azure Storage w Blitline [tutaj](http://www.blitline.com/docs/azure_storage).

## <a name="next-steps"></a>Następne kroki
Odwiedź tooread blitline.com o wszystkich naszych innych funkcji:

* Dokumentacja interfejsu API punktu końcowego Blitline <http://www.blitline.com/docs/api>
* Funkcje interfejsu API Blitline <http://www.blitline.com/docs/functions>
* Przykłady Blitline interfejsu API <http://www.blitline.com/docs/examples>
* Trzeci część biblioteki Nuget <http://nuget.org/packages/Blitline.Net>

