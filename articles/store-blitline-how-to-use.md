---
title: "Jak używać Blitline obrazu przetwarzania - Azure funkcji Przewodnik"
description: "Dowiedz się, jak używać usługi Blitline przetwarzania obrazów w aplikacji Azure."
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
ms.openlocfilehash: 1d90599e028b3407a513b04b878e3aefc39928a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-blitline-with-azure-and-azure-storage"></a><span data-ttu-id="32e25-103">Jak używać Blitline z platformy Azure i usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="32e25-103">How to use Blitline with Azure and Azure Storage</span></span>
<span data-ttu-id="32e25-104">W tym przewodniku objaśnia sposób uzyskiwać dostęp do usług Blitline i przesyłanie zadań do Blitline.</span><span class="sxs-lookup"><span data-stu-id="32e25-104">This guide will explain how to access Blitline services and how to submit jobs to Blitline.</span></span>

## <a name="what-is-blitline"></a><span data-ttu-id="32e25-105">Co to jest Blitline?</span><span class="sxs-lookup"><span data-stu-id="32e25-105">What is Blitline?</span></span>
<span data-ttu-id="32e25-106">Blitline to usługa, która zapewnia przetwarzania obrazu poziomu przedsiębiorstwa w ułamku cen, który może kosztować kompilacji samodzielnie przetwarzania obraz oparte na chmurze.</span><span class="sxs-lookup"><span data-stu-id="32e25-106">Blitline is a cloud-based image processing service that provides enterprise level image processing at a fraction of the price that it would cost to build it yourself.</span></span>

<span data-ttu-id="32e25-107">Fakt jest, że przetwarzania obrazów przeprowadzono wielokrotnie, zwykle ponownie skompilowany od podstaw z myślą o każdym witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="32e25-107">The fact is that image processing has been done over and over again, usually rebuilt from the ground up for each and every website.</span></span> <span data-ttu-id="32e25-108">Zdajemy sobie sprawę, to ponieważ już budujemy ich milionów razy zbyt.</span><span class="sxs-lookup"><span data-stu-id="32e25-108">We realize this because we’ve built them a million times too.</span></span> <span data-ttu-id="32e25-109">Jeden dzień, który zdecydowaliśmy się, że prawdopodobnie nadszedł czas, tak jak go dla wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="32e25-109">One day we decided that perhaps it‘s time we just do it for everyone.</span></span> <span data-ttu-id="32e25-110">Wiemy, jak to zrobić, to szybkie i wydajne i zapisania wszyscy pracy w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="32e25-110">We know how to do it, to do it fast and efficiently, and save everyone work in the meantime.</span></span>

<span data-ttu-id="32e25-111">Aby uzyskać więcej informacji, zobacz [http://www.blitline.com](http://www.blitline.com).</span><span class="sxs-lookup"><span data-stu-id="32e25-111">For more information, see [http://www.blitline.com](http://www.blitline.com).</span></span>

## <a name="what-blitline-is-not"></a><span data-ttu-id="32e25-112">Co Blitline nie...</span><span class="sxs-lookup"><span data-stu-id="32e25-112">What Blitline is NOT...</span></span>
<span data-ttu-id="32e25-113">Wyjaśnienie, co jest przydatne w przypadku Blitline, często jest łatwiej zidentyfikować co Blitline, które nie są przed przeniesieniem do przodu.</span><span class="sxs-lookup"><span data-stu-id="32e25-113">To clarify what Blitline is useful for, it is often easier to identify what Blitline does NOT do before moving forward.</span></span>

* <span data-ttu-id="32e25-114">Blitline nie ma elementów widget HTML do przekazywania obrazów.</span><span class="sxs-lookup"><span data-stu-id="32e25-114">Blitline does NOT have HTML widgets to upload images.</span></span> <span data-ttu-id="32e25-115">Obrazy dostępne musi mieć publiczną lub z ograniczonymi uprawnieniami dostępne dla Blitline nawiązać połączenie.</span><span class="sxs-lookup"><span data-stu-id="32e25-115">You must have images available publicly or with restricted permissions available for Blitline to reach.</span></span>
* <span data-ttu-id="32e25-116">Blitline nie działa na żywo przetwarzania obrazu, takich jak Aviary.com</span><span class="sxs-lookup"><span data-stu-id="32e25-116">Blitline does NOT do live image processing, like Aviary.com</span></span>
* <span data-ttu-id="32e25-117">Blitline nie akceptuje przekazywania obrazów, nie można wypchnąć obrazów do Blitline bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="32e25-117">Blitline does NOT accept image uploads, you cannot push your images to Blitline directly.</span></span> <span data-ttu-id="32e25-118">Należy wypychanie ich do usługi Azure Storage lub innych miejsc obsługuje Blitline, a następnie informują Blitline, skąd można je pobrać.</span><span class="sxs-lookup"><span data-stu-id="32e25-118">You must push them to Azure Storage or other places Blitline supports and then tell Blitline where to go get them.</span></span>
* <span data-ttu-id="32e25-119">Blitline jest równoległemu i nie wykonuje żadnych przetwarzania synchronicznego.</span><span class="sxs-lookup"><span data-stu-id="32e25-119">Blitline is massively parallel and does NOT do any synchronous processing.</span></span> <span data-ttu-id="32e25-120">Co oznacza Podaj nam postback_url i możemy pomagają stwierdzić, gdy firma Microsoft gotowe przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="32e25-120">Meaning you must give us a postback_url and we can tell you when we are done processing.</span></span>

## <a name="create-a-blitline-account"></a><span data-ttu-id="32e25-121">Utwórz konto Blitline</span><span class="sxs-lookup"><span data-stu-id="32e25-121">Create a Blitline account</span></span>
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-to-create-a-blitline-job"></a><span data-ttu-id="32e25-122">Jak utworzyć zadanie Blitline</span><span class="sxs-lookup"><span data-stu-id="32e25-122">How to create a Blitline job</span></span>
<span data-ttu-id="32e25-123">Blitline używa JSON w celu zdefiniowania akcje, które ma być wykonywana na obrazie.</span><span class="sxs-lookup"><span data-stu-id="32e25-123">Blitline uses JSON to define the actions you want to take on an image.</span></span> <span data-ttu-id="32e25-124">Ten kod JSON składa się z kilku prostych pól.</span><span class="sxs-lookup"><span data-stu-id="32e25-124">This JSON is composed of a few simple fields.</span></span>

<span data-ttu-id="32e25-125">Najprostszy przykład następująco:</span><span class="sxs-lookup"><span data-stu-id="32e25-125">The simplest example is as follows:</span></span>

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

<span data-ttu-id="32e25-126">W tym miejscu mamy JSON, który zajmie obrazu "src" "... boys.jpeg", a następnie zmień rozmiar obrazu do 240 x 140.</span><span class="sxs-lookup"><span data-stu-id="32e25-126">Here we have JSON that will take a "src" image "...boys.jpeg" and then resize that image to 240x140.</span></span>

<span data-ttu-id="32e25-127">Identyfikator aplikacji jest element znajduje się w sieci **informacje o połączeniu** lub **ZARZĄDZAJ** kartę na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="32e25-127">The Application ID is something you can find in your **CONNECTION INFO** or **MANAGE** tab on Azure.</span></span> <span data-ttu-id="32e25-128">Jest identyfikatora tajny, który umożliwia uruchamianie zadań na Blitline.</span><span class="sxs-lookup"><span data-stu-id="32e25-128">It is your secret identifier that allows you to run jobs on Blitline.</span></span>

<span data-ttu-id="32e25-129">Parametr "Zapisz" identyfikuje informacji o którym chcesz umieścić obraz po możemy zostały przetworzone go.</span><span class="sxs-lookup"><span data-stu-id="32e25-129">The "save" parameter identifies information about where you want to put the image once we have processed it.</span></span> <span data-ttu-id="32e25-130">W tym przypadku trivial możemy jeszcze zdefiniowana.</span><span class="sxs-lookup"><span data-stu-id="32e25-130">In this trivial case, we haven't defined one.</span></span> <span data-ttu-id="32e25-131">Jeśli lokalizacja nie jest zdefiniowany Blitline zapisze ją lokalnie (i tymczasowo) w lokalizacji unikatowy chmury.</span><span class="sxs-lookup"><span data-stu-id="32e25-131">If no location is defined Blitline will store it locally (and temporarily) at a unique cloud location.</span></span> <span data-ttu-id="32e25-132">Będzie można pobrać lokalizacji z zwrócony przez Blitline po wprowadzeniu Blitline JSON.</span><span class="sxs-lookup"><span data-stu-id="32e25-132">You will be able to get that location from the JSON returned by Blitline when you make the Blitline.</span></span> <span data-ttu-id="32e25-133">Identyfikator "obrazu" jest wymagana i jest zwracane po do identyfikowania tego określonego zapisać obrazu.</span><span class="sxs-lookup"><span data-stu-id="32e25-133">The "image" identifier is required and is returned to you when to identify this particular saved image.</span></span>

<span data-ttu-id="32e25-134">Więcej informacji można znaleźć o *funkcje* obsługujemy tutaj: <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="32e25-134">You can find more information about the *functions* we support here: <http://www.blitline.com/docs/functions></span></span>

<span data-ttu-id="32e25-135">Możesz również znaleźć dokumentację dotyczącą Opcje zadania tutaj: <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="32e25-135">You can also find documentation about the job options here: <http://www.blitline.com/docs/api></span></span>

<span data-ttu-id="32e25-136">Po określeniu, czy kod JSON jest wszystko co należy zrobić **POST** go do`http://api.blitline.com/job`</span><span class="sxs-lookup"><span data-stu-id="32e25-136">Once you have your JSON all you need to do is **POST** it to `http://api.blitline.com/job`</span></span>

<span data-ttu-id="32e25-137">Otrzymasz wstecz JSON, który wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="32e25-137">You will get JSON back that looks something like this:</span></span>

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


<span data-ttu-id="32e25-138">Oznacza to, Blitline odebrał żądanie, ma umieszcza je w kolejce przetwarzania i po zakończeniu obrazu będzie dostępna w: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_aplikacji\_identyfikator / CK3f0xBF_2bV6wf7gEZE8w.jpg**</span><span class="sxs-lookup"><span data-stu-id="32e25-138">This tells you that Blitline has recieved your request, it has put it in a processing queue, and when it has completed the image will be available at: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg**</span></span>

## <a name="how-to-save-an-image-to-your-azure-storage-account"></a><span data-ttu-id="32e25-139">Jak zapisać obrazu do konta magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="32e25-139">How to save an image to your Azure Storage account</span></span>
<span data-ttu-id="32e25-140">Jeśli masz konto usługi Azure Storage, mogą być Blitline wypchnąć przetworzonych obrazów do Twojej kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="32e25-140">If you have an Azure Storage account, you can easily have Blitline push the processed images into your Azure container.</span></span> <span data-ttu-id="32e25-141">Dodając "azure_destination" należy zdefiniować lokalizacji i uprawnienia do Blitline do.</span><span class="sxs-lookup"><span data-stu-id="32e25-141">By adding an "azure_destination" you define the location and permissions for Blitline to push to.</span></span>

<span data-ttu-id="32e25-142">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="32e25-142">Here is an example:</span></span>

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


<span data-ttu-id="32e25-143">Wypełniając CAPITALIZED wartości własnymi, mogą przesyłać dane JSON do http://api.blitline.com/job i obraz "src" zostanie przetworzyć filtru rozmycia i następnie przypisany do usługi Azure docelowego.</span><span class="sxs-lookup"><span data-stu-id="32e25-143">By filling in the CAPITALIZED values with your own, you can submit this JSON to http://api.blitline.com/job and the "src" image will be processed with a blur filter and then pushed to you Azure destination.</span></span>

### <a name="please-note"></a><span data-ttu-id="32e25-144">Uwaga:</span><span class="sxs-lookup"><span data-stu-id="32e25-144">Please note:</span></span>
<span data-ttu-id="32e25-145">Sygnatury dostępu Współdzielonego musi zawierać cały adres url SAS, łącznie z nazwą pliku, plik docelowy.</span><span class="sxs-lookup"><span data-stu-id="32e25-145">The SAS must contain the entire SAS url, including the filename of the destination file.</span></span>

<span data-ttu-id="32e25-146">Przykład:</span><span class="sxs-lookup"><span data-stu-id="32e25-146">Example:</span></span>

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


<span data-ttu-id="32e25-147">Możesz przeczytać najnowszych wersji dokumentów usługi Azure Storage w Blitline [tutaj](http://www.blitline.com/docs/azure_storage).</span><span class="sxs-lookup"><span data-stu-id="32e25-147">You can also read the latest edition of Blitline's Azure Storage docs [here](http://www.blitline.com/docs/azure_storage).</span></span>

## <a name="next-steps"></a><span data-ttu-id="32e25-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="32e25-148">Next Steps</span></span>
<span data-ttu-id="32e25-149">Odwiedź stronę blitline.com, aby uzyskać informacje dotyczące wszystkich naszych innych funkcji:</span><span class="sxs-lookup"><span data-stu-id="32e25-149">Visit blitline.com to read about all our other features:</span></span>

* <span data-ttu-id="32e25-150">Dokumentacja interfejsu API punktu końcowego Blitline <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="32e25-150">Blitline API Endpoint Docs <http://www.blitline.com/docs/api></span></span>
* <span data-ttu-id="32e25-151">Funkcje interfejsu API Blitline <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="32e25-151">Blitline API Functions <http://www.blitline.com/docs/functions></span></span>
* <span data-ttu-id="32e25-152">Przykłady Blitline interfejsu API <http://www.blitline.com/docs/examples></span><span class="sxs-lookup"><span data-stu-id="32e25-152">Blitline API Examples <http://www.blitline.com/docs/examples></span></span>
* <span data-ttu-id="32e25-153">Trzeci część biblioteki Nuget <http://nuget.org/packages/Blitline.Net></span><span class="sxs-lookup"><span data-stu-id="32e25-153">Third Part Nuget Library <http://nuget.org/packages/Blitline.Net></span></span>

