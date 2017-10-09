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
# <a name="how-toouse-blitline-with-azure-and-azure-storage"></a><span data-ttu-id="515d0-103">Jak toouse Blitline z platformy Azure i magazynem Azure</span><span class="sxs-lookup"><span data-stu-id="515d0-103">How toouse Blitline with Azure and Azure Storage</span></span>
<span data-ttu-id="515d0-104">W tym przewodniku objaśniają jak tooaccess Blitline usług i jak toosubmit zadania tooBlitline.</span><span class="sxs-lookup"><span data-stu-id="515d0-104">This guide will explain how tooaccess Blitline services and how toosubmit jobs tooBlitline.</span></span>

## <a name="what-is-blitline"></a><span data-ttu-id="515d0-105">Co to jest Blitline?</span><span class="sxs-lookup"><span data-stu-id="515d0-105">What is Blitline?</span></span>
<span data-ttu-id="515d0-106">Blitline to obraz oparte na chmurze usługa, która zapewnia przetwarzania obrazu poziomu przedsiębiorstwa w ułamku hello ceny czy koszt toobuild przetwarzania go samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="515d0-106">Blitline is a cloud-based image processing service that provides enterprise level image processing at a fraction of hello price that it would cost toobuild it yourself.</span></span>

<span data-ttu-id="515d0-107">fakt Hello jest, że przetwarzania obrazów przeprowadzono wielokrotnie, zwykle ponownie skompilowany od hello podstaw z myślą o każdym witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="515d0-107">hello fact is that image processing has been done over and over again, usually rebuilt from hello ground up for each and every website.</span></span> <span data-ttu-id="515d0-108">Zdajemy sobie sprawę, to ponieważ już budujemy ich milionów razy zbyt.</span><span class="sxs-lookup"><span data-stu-id="515d0-108">We realize this because we’ve built them a million times too.</span></span> <span data-ttu-id="515d0-109">Jeden dzień, który zdecydowaliśmy się, że prawdopodobnie nadszedł czas, tak jak go dla wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="515d0-109">One day we decided that perhaps it‘s time we just do it for everyone.</span></span> <span data-ttu-id="515d0-110">Wiemy, jak toodo on toodo on szybkiego i efektywnego i Zapisz wszyscy działać w hello czasu.</span><span class="sxs-lookup"><span data-stu-id="515d0-110">We know how toodo it, toodo it fast and efficiently, and save everyone work in hello meantime.</span></span>

<span data-ttu-id="515d0-111">Aby uzyskać więcej informacji, zobacz [http://www.blitline.com](http://www.blitline.com).</span><span class="sxs-lookup"><span data-stu-id="515d0-111">For more information, see [http://www.blitline.com](http://www.blitline.com).</span></span>

## <a name="what-blitline-is-not"></a><span data-ttu-id="515d0-112">Co Blitline nie...</span><span class="sxs-lookup"><span data-stu-id="515d0-112">What Blitline is NOT...</span></span>
<span data-ttu-id="515d0-113">tooclarify co Blitline jest przydatne dla jest często łatwiejsze tooidentify co Blitline, które nie są przed przeniesieniem do przodu.</span><span class="sxs-lookup"><span data-stu-id="515d0-113">tooclarify what Blitline is useful for, it is often easier tooidentify what Blitline does NOT do before moving forward.</span></span>

* <span data-ttu-id="515d0-114">Blitline nie ma obrazów tooupload elementy widget HTML.</span><span class="sxs-lookup"><span data-stu-id="515d0-114">Blitline does NOT have HTML widgets tooupload images.</span></span> <span data-ttu-id="515d0-115">Obrazy dostępne musi mieć publiczną lub z ograniczonymi uprawnieniami dostępne dla Blitline tooreach.</span><span class="sxs-lookup"><span data-stu-id="515d0-115">You must have images available publicly or with restricted permissions available for Blitline tooreach.</span></span>
* <span data-ttu-id="515d0-116">Blitline nie działa na żywo przetwarzania obrazu, takich jak Aviary.com</span><span class="sxs-lookup"><span data-stu-id="515d0-116">Blitline does NOT do live image processing, like Aviary.com</span></span>
* <span data-ttu-id="515d0-117">Blitline nie akceptuje przekazywania obrazów, nie można wypchnąć tooBlitline Twojego obrazy bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="515d0-117">Blitline does NOT accept image uploads, you cannot push your images tooBlitline directly.</span></span> <span data-ttu-id="515d0-118">Należy wypchniesz tooAzure magazynu lub innych miejsc, który obsługuje Blitline i następnie poinformuj Blitline gdzie toogo uzyskać je.</span><span class="sxs-lookup"><span data-stu-id="515d0-118">You must push them tooAzure Storage or other places Blitline supports and then tell Blitline where toogo get them.</span></span>
* <span data-ttu-id="515d0-119">Blitline jest równoległemu i nie wykonuje żadnych przetwarzania synchronicznego.</span><span class="sxs-lookup"><span data-stu-id="515d0-119">Blitline is massively parallel and does NOT do any synchronous processing.</span></span> <span data-ttu-id="515d0-120">Co oznacza Podaj nam postback_url i możemy pomagają stwierdzić, gdy firma Microsoft gotowe przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="515d0-120">Meaning you must give us a postback_url and we can tell you when we are done processing.</span></span>

## <a name="create-a-blitline-account"></a><span data-ttu-id="515d0-121">Utwórz konto Blitline</span><span class="sxs-lookup"><span data-stu-id="515d0-121">Create a Blitline account</span></span>
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-toocreate-a-blitline-job"></a><span data-ttu-id="515d0-122">Jak toocreate zadania Blitline</span><span class="sxs-lookup"><span data-stu-id="515d0-122">How toocreate a Blitline job</span></span>
<span data-ttu-id="515d0-123">Blitline używa JSON toodefine hello akcje, które mają tootake na obrazie.</span><span class="sxs-lookup"><span data-stu-id="515d0-123">Blitline uses JSON toodefine hello actions you want tootake on an image.</span></span> <span data-ttu-id="515d0-124">Ten kod JSON składa się z kilku prostych pól.</span><span class="sxs-lookup"><span data-stu-id="515d0-124">This JSON is composed of a few simple fields.</span></span>

<span data-ttu-id="515d0-125">Najprostsza przykład Witaj wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="515d0-125">hello simplest example is as follows:</span></span>

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

<span data-ttu-id="515d0-126">W tym miejscu mamy JSON, który zajmie obrazu "src" "... boys.jpeg", a następnie zmień rozmiar tego obrazu too240x140.</span><span class="sxs-lookup"><span data-stu-id="515d0-126">Here we have JSON that will take a "src" image "...boys.jpeg" and then resize that image too240x140.</span></span>

<span data-ttu-id="515d0-127">Identyfikator aplikacji Hello to element znajduje się w sieci **informacje o połączeniu** lub **ZARZĄDZAJ** kartę na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="515d0-127">hello Application ID is something you can find in your **CONNECTION INFO** or **MANAGE** tab on Azure.</span></span> <span data-ttu-id="515d0-128">Jest identyfikatorem tajny umożliwiająca zadania toorun na Blitline.</span><span class="sxs-lookup"><span data-stu-id="515d0-128">It is your secret identifier that allows you toorun jobs on Blitline.</span></span>

<span data-ttu-id="515d0-129">Witaj przycisk Zapisz, parametr identyfikuje informacji o miejscu tooput obraz powitania po możemy zostały przetworzone go.</span><span class="sxs-lookup"><span data-stu-id="515d0-129">hello "save" parameter identifies information about where you want tooput hello image once we have processed it.</span></span> <span data-ttu-id="515d0-130">W tym przypadku trivial możemy jeszcze zdefiniowana.</span><span class="sxs-lookup"><span data-stu-id="515d0-130">In this trivial case, we haven't defined one.</span></span> <span data-ttu-id="515d0-131">Jeśli lokalizacja nie jest zdefiniowany Blitline zapisze ją lokalnie (i tymczasowo) w lokalizacji unikatowy chmury.</span><span class="sxs-lookup"><span data-stu-id="515d0-131">If no location is defined Blitline will store it locally (and temporarily) at a unique cloud location.</span></span> <span data-ttu-id="515d0-132">Będzie możliwe tooget, który lokalizacji z hello JSON zwrócony przez Blitline po wprowadzeniu hello Blitline.</span><span class="sxs-lookup"><span data-stu-id="515d0-132">You will be able tooget that location from hello JSON returned by Blitline when you make hello Blitline.</span></span> <span data-ttu-id="515d0-133">Identyfikator "obrazu" Hello jest wymagana i zwracany jest tooyou tooidentify zapisać tego określonego obrazu.</span><span class="sxs-lookup"><span data-stu-id="515d0-133">hello "image" identifier is required and is returned tooyou when tooidentify this particular saved image.</span></span>

<span data-ttu-id="515d0-134">Można znaleźć więcej informacji na temat hello *funkcje* obsługujemy tutaj: <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="515d0-134">You can find more information about hello *functions* we support here: <http://www.blitline.com/docs/functions></span></span>

<span data-ttu-id="515d0-135">Możesz również znaleźć dokumentację dotyczącą hello Opcje zadania tutaj: <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="515d0-135">You can also find documentation about hello job options here: <http://www.blitline.com/docs/api></span></span>

<span data-ttu-id="515d0-136">Po określeniu, czy kod JSON toodo wystarczy **POST** on zbyt`http://api.blitline.com/job`</span><span class="sxs-lookup"><span data-stu-id="515d0-136">Once you have your JSON all you need toodo is **POST** it too`http://api.blitline.com/job`</span></span>

<span data-ttu-id="515d0-137">Otrzymasz wstecz JSON, który wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="515d0-137">You will get JSON back that looks something like this:</span></span>

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


<span data-ttu-id="515d0-138">Oznacza to, Blitline odebrał żądanie, ma umieszcza je w kolejce przetwarzania i po zakończeniu hello obrazu będzie dostępna w: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_aplikacji\_ID /CK3f0xBF_2bV6wf7gEZE8w.jpg**</span><span class="sxs-lookup"><span data-stu-id="515d0-138">This tells you that Blitline has recieved your request, it has put it in a processing queue, and when it has completed hello image will be available at: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg**</span></span>

## <a name="how-toosave-an-image-tooyour-azure-storage-account"></a><span data-ttu-id="515d0-139">Jak toosave tooyour obraz konta magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="515d0-139">How toosave an image tooyour Azure Storage account</span></span>
<span data-ttu-id="515d0-140">Jeśli masz konto usługi Azure Storage, mogą być Blitline wypychania hello przetwarzania obrazów do Twojej kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="515d0-140">If you have an Azure Storage account, you can easily have Blitline push hello processed images into your Azure container.</span></span> <span data-ttu-id="515d0-141">Dodając "azure_destination" należy zdefiniować hello lokalizacji i uprawnienia do toopush Blitline do.</span><span class="sxs-lookup"><span data-stu-id="515d0-141">By adding an "azure_destination" you define hello location and permissions for Blitline toopush to.</span></span>

<span data-ttu-id="515d0-142">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="515d0-142">Here is an example:</span></span>

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


<span data-ttu-id="515d0-143">Wypełniając hello CAPITALIZED wartości własnymi, można przesłać ten toohttp://api.blitline.com/job JSON i hello obrazu "src" będą przetwarzane z filtru rozmycia i następnie wypychana tooyou docelowej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="515d0-143">By filling in hello CAPITALIZED values with your own, you can submit this JSON toohttp://api.blitline.com/job and hello "src" image will be processed with a blur filter and then pushed tooyou Azure destination.</span></span>

### <a name="please-note"></a><span data-ttu-id="515d0-144">Uwaga:</span><span class="sxs-lookup"><span data-stu-id="515d0-144">Please note:</span></span>
<span data-ttu-id="515d0-145">Witaj SAS musi zawierać hello cały adres url SAS, włączając hello nazwa pliku docelowego hello.</span><span class="sxs-lookup"><span data-stu-id="515d0-145">hello SAS must contain hello entire SAS url, including hello filename of hello destination file.</span></span>

<span data-ttu-id="515d0-146">Przykład:</span><span class="sxs-lookup"><span data-stu-id="515d0-146">Example:</span></span>

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


<span data-ttu-id="515d0-147">Możesz przeczytać hello najnowszych wersji dokumentów usługi Azure Storage w Blitline [tutaj](http://www.blitline.com/docs/azure_storage).</span><span class="sxs-lookup"><span data-stu-id="515d0-147">You can also read hello latest edition of Blitline's Azure Storage docs [here](http://www.blitline.com/docs/azure_storage).</span></span>

## <a name="next-steps"></a><span data-ttu-id="515d0-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="515d0-148">Next Steps</span></span>
<span data-ttu-id="515d0-149">Odwiedź tooread blitline.com o wszystkich naszych innych funkcji:</span><span class="sxs-lookup"><span data-stu-id="515d0-149">Visit blitline.com tooread about all our other features:</span></span>

* <span data-ttu-id="515d0-150">Dokumentacja interfejsu API punktu końcowego Blitline <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="515d0-150">Blitline API Endpoint Docs <http://www.blitline.com/docs/api></span></span>
* <span data-ttu-id="515d0-151">Funkcje interfejsu API Blitline <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="515d0-151">Blitline API Functions <http://www.blitline.com/docs/functions></span></span>
* <span data-ttu-id="515d0-152">Przykłady Blitline interfejsu API <http://www.blitline.com/docs/examples></span><span class="sxs-lookup"><span data-stu-id="515d0-152">Blitline API Examples <http://www.blitline.com/docs/examples></span></span>
* <span data-ttu-id="515d0-153">Trzeci część biblioteki Nuget <http://nuget.org/packages/Blitline.Net></span><span class="sxs-lookup"><span data-stu-id="515d0-153">Third Part Nuget Library <http://nuget.org/packages/Blitline.Net></span></span>

