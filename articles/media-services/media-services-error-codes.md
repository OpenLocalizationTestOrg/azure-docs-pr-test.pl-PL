---
title: "Kody błędów w usłudze Azure Media Services | Dokumentacja firmy Microsoft"
description: "Temat zawiera omówienie usługi Azure Media Services kody błędów."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d3a62a64-7608-4b17-8667-479b26ba0d6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 39886a955124429302609dd9d5a7c20ae7f498d9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-media-services-error-codes"></a><span data-ttu-id="8bea5-103">Kody błędów w usłudze Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="8bea5-103">Azure Media Services error codes</span></span>
<span data-ttu-id="8bea5-104">Korzystając z usługi Microsoft Azure Media Services, usługi, w zależności od problemów, takich jak tokeny uwierzytelniania wygasa do akcji, które nie są obsługiwane w usłudze Media Services może zostać wyświetlony kody błędów HTTP.</span><span class="sxs-lookup"><span data-stu-id="8bea5-104">When using Microsoft Azure Media Services, you may receive HTTP error codes from the service depending on issues such as authentication tokens expiring to actions that are not supported in Media Services.</span></span> <span data-ttu-id="8bea5-105">Poniżej przedstawiono listę **kody błędów HTTP** które mogą być zwrócone przez usługi Media Services i możliwe przyczyny dla nich.</span><span class="sxs-lookup"><span data-stu-id="8bea5-105">The following is a list of **HTTP error codes** that may be returned by Media Services and the possible causes for them.</span></span>  

## <a name="400-bad-request"></a><span data-ttu-id="8bea5-106">400 Niewłaściwe żądanie</span><span class="sxs-lookup"><span data-stu-id="8bea5-106">400 Bad Request</span></span>
<span data-ttu-id="8bea5-107">Żądanie zawiera nieprawidłowe informacje i zostało odrzucone z jednego z następujących powodów:</span><span class="sxs-lookup"><span data-stu-id="8bea5-107">The request contains invalid information and is rejected due to one of the following reasons:</span></span>

* <span data-ttu-id="8bea5-108">Określono nieobsługiwaną wersję interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="8bea5-108">An unsupported API version is specified.</span></span> <span data-ttu-id="8bea5-109">Aktualna wersja dla [ustawień dla rozwoju interfejsu API REST usługi Media](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="8bea5-109">For the most current version, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="8bea5-110">Nie określono wersji interfejsu API usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="8bea5-110">The API version of Media Services is not specified.</span></span> <span data-ttu-id="8bea5-111">Aby uzyskać informacje dotyczące sposobu określania wersji interfejsu API, zobacz [dokumentacja interfejsu API REST Media Services operacji](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).</span><span class="sxs-lookup"><span data-stu-id="8bea5-111">For information on how to specify the API version, see [Media Services Operations REST API Reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="8bea5-112">Jeśli połączyć z usługą Media Services przy użyciu platformy .NET lub zestawów SDK Java, wersja interfejsu API jest określony dla Ciebie za każdym razem spróbuj i wykonanie akcji dla usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="8bea5-112">If you are using the .NET or Java SDKs to connect to Media Services, the API version is specified for you whenever you try and perform some action against Media Services.</span></span>
  > 
  > 
* <span data-ttu-id="8bea5-113">Niezdefiniowane właściwości został określony.</span><span class="sxs-lookup"><span data-stu-id="8bea5-113">An undefined property has been specified.</span></span> <span data-ttu-id="8bea5-114">Nazwa właściwości jest w komunikacie o błędzie.</span><span class="sxs-lookup"><span data-stu-id="8bea5-114">The property name is in the error message.</span></span> <span data-ttu-id="8bea5-115">Można określić tylko właściwości, które są członkami danej jednostki.</span><span class="sxs-lookup"><span data-stu-id="8bea5-115">Only those properties that are members of a given entity can be specified.</span></span> <span data-ttu-id="8bea5-116">Zobacz [dokumentacja interfejsu API REST usługi Azure Media Services](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference) listę obiektów i ich właściwości.</span><span class="sxs-lookup"><span data-stu-id="8bea5-116">See [Azure Media Services REST API Reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference) for a list of entities and their properties.</span></span>
* <span data-ttu-id="8bea5-117">Określono nieprawidłową wartość właściwości.</span><span class="sxs-lookup"><span data-stu-id="8bea5-117">An invalid property value has been specified.</span></span> <span data-ttu-id="8bea5-118">Nazwa właściwości jest w komunikacie o błędzie.</span><span class="sxs-lookup"><span data-stu-id="8bea5-118">The property name is in the error message.</span></span> <span data-ttu-id="8bea5-119">Zobacz poprzedniej konsolidacji dla typów prawidłowej właściwości i ich wartości.</span><span class="sxs-lookup"><span data-stu-id="8bea5-119">See the previous link for valid property types and their values.</span></span>
* <span data-ttu-id="8bea5-120">Wartość właściwości nie istnieje i jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="8bea5-120">A property value is missing and is required.</span></span>
* <span data-ttu-id="8bea5-121">Część określony adres URL zawiera nieprawidłowe wartości.</span><span class="sxs-lookup"><span data-stu-id="8bea5-121">Part of the URL specified contains a bad value.</span></span>
* <span data-ttu-id="8bea5-122">Nastąpiła próba zaktualizować właściwości WriteOnce.</span><span class="sxs-lookup"><span data-stu-id="8bea5-122">An attempt was made to update a WriteOnce property.</span></span>
* <span data-ttu-id="8bea5-123">Próbowano utworzyć zadanie, które ma wejściowych zasobu z AssetFile głównej, która nie została określona lub nie można określić.</span><span class="sxs-lookup"><span data-stu-id="8bea5-123">An attempt was made to create a Job that has an input Asset with a primary AssetFile that was not specified or could not be determined.</span></span>
* <span data-ttu-id="8bea5-124">Nastąpiła próba aktualizacji lokalizatora SAS.</span><span class="sxs-lookup"><span data-stu-id="8bea5-124">An attempt was made to update a SAS Locator.</span></span> <span data-ttu-id="8bea5-125">Lokalizatory sygnatury dostępu Współdzielonego tylko można utworzyć ani usunąć.</span><span class="sxs-lookup"><span data-stu-id="8bea5-125">SAS locators can only be created or deleted.</span></span> <span data-ttu-id="8bea5-126">Przesyłanie strumieniowe lokalizatorów można aktualizować.</span><span class="sxs-lookup"><span data-stu-id="8bea5-126">Streaming locators can be updated.</span></span> <span data-ttu-id="8bea5-127">Aby uzyskać więcej informacji, zobacz [Lokalizatory](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="8bea5-127">For more information, see [Locators](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>
* <span data-ttu-id="8bea5-128">Nieobsługiwana operacja lub zapytanie zostało przesłane.</span><span class="sxs-lookup"><span data-stu-id="8bea5-128">An unsupported operation or query was submitted.</span></span>

## <a name="401-unauthorized"></a><span data-ttu-id="8bea5-129">401 nieautoryzowane</span><span class="sxs-lookup"><span data-stu-id="8bea5-129">401 Unauthorized</span></span>
<span data-ttu-id="8bea5-130">Nie można uwierzytelnić żądania (przed może być upoważnionych) z jednego z następujących powodów:</span><span class="sxs-lookup"><span data-stu-id="8bea5-130">The request could not be authenticated (before it can be authorized) due to one of the following reasons:</span></span>

* <span data-ttu-id="8bea5-131">Brak nagłówka uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="8bea5-131">Missing authentication header.</span></span>
* <span data-ttu-id="8bea5-132">Wartość nagłówka uwierzytelnienia zła.</span><span class="sxs-lookup"><span data-stu-id="8bea5-132">Bad authentication header value.</span></span>
  * <span data-ttu-id="8bea5-133">Token utracił ważność.</span><span class="sxs-lookup"><span data-stu-id="8bea5-133">The token has expired.</span></span> 
  * <span data-ttu-id="8bea5-134">Token ma nieprawidłowy podpis.</span><span class="sxs-lookup"><span data-stu-id="8bea5-134">The token contains an invalid signature.</span></span>

## <a name="403-forbidden"></a><span data-ttu-id="8bea5-135">403 Zabroniony</span><span class="sxs-lookup"><span data-stu-id="8bea5-135">403 Forbidden</span></span>
<span data-ttu-id="8bea5-136">Żądanie nie jest dozwolone z jednego z następujących powodów:</span><span class="sxs-lookup"><span data-stu-id="8bea5-136">The request is not allowed due to one of the following reasons:</span></span>

* <span data-ttu-id="8bea5-137">Konto usługi Media Services nie można odnaleźć lub została usunięta.</span><span class="sxs-lookup"><span data-stu-id="8bea5-137">The Media Services account cannot be found or has been deleted.</span></span>
* <span data-ttu-id="8bea5-138">Konto usługi Media Services jest wyłączona, a typ żądania nie jest HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="8bea5-138">The Media Services account is disabled and the request type is not HTTP GET.</span></span> <span data-ttu-id="8bea5-139">Operacje usługi zwróci również 403 odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="8bea5-139">Service operations will return a 403 response as well.</span></span>
* <span data-ttu-id="8bea5-140">Token uwierzytelniania nie zawiera informacji o poświadczeniach użytkownika: Nazwa konta i/lub identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8bea5-140">The authentication token does not contain the user’s credential information: AccountName and/or SubscriptionId.</span></span> <span data-ttu-id="8bea5-141">Informacje te można znaleźć w rozszerzeniu interfejsu użytkownika usługi multimediów dla konta usługi Media Services w portalu zarządzania Azure.</span><span class="sxs-lookup"><span data-stu-id="8bea5-141">You can find this information in the Media Services UI extension for your Media Services account in the Azure Management Portal.</span></span>
* <span data-ttu-id="8bea5-142">Nie można uzyskać dostępu do zasobu.</span><span class="sxs-lookup"><span data-stu-id="8bea5-142">The resource cannot be accessed.</span></span>
  
  * <span data-ttu-id="8bea5-143">Próbowano użyć MediaProcessor, który nie jest dostępny dla konta usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="8bea5-143">An attempt was made to use a MediaProcessor that is not available for your Media Services account.</span></span>
  * <span data-ttu-id="8bea5-144">Nastąpiła próba aktualizacji obiekt JobTemplate zdefiniowany przez usługę Media Services.</span><span class="sxs-lookup"><span data-stu-id="8bea5-144">An attempt was made to update a JobTemplate defined by Media Services.</span></span>
  * <span data-ttu-id="8bea5-145">Próbowano zastąpić lokalizatora niektóre inne konta usługi Media Services firmy.</span><span class="sxs-lookup"><span data-stu-id="8bea5-145">An attempt was made to overwrite some other Media Services account's Locator.</span></span>
  * <span data-ttu-id="8bea5-146">Próbowano zastąpić ContentKey niektóre inne konta usługi Media Services firmy.</span><span class="sxs-lookup"><span data-stu-id="8bea5-146">An attempt was made to overwrite some other Media Services account's ContentKey.</span></span>
* <span data-ttu-id="8bea5-147">Nie można utworzyć zasobu z powodu przydziału usługi, który został osiągnięty dla konta usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="8bea5-147">The resource could not be created due to a service quota that was reached for the Media Services account.</span></span> <span data-ttu-id="8bea5-148">Aby uzyskać więcej informacji na przydziały usługi, zobacz [przydziały i ograniczenia](media-services-quotas-and-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="8bea5-148">For more information on the service quotas, see [Quotas and Limitations](media-services-quotas-and-limitations.md).</span></span>

## <a name="404-not-found"></a><span data-ttu-id="8bea5-149">404 — Nie odnaleziono</span><span class="sxs-lookup"><span data-stu-id="8bea5-149">404 Not Found</span></span>
<span data-ttu-id="8bea5-150">Żądanie nie jest dozwolona w zasobie z jednego z następujących powodów:</span><span class="sxs-lookup"><span data-stu-id="8bea5-150">The request is not allowed on a resource due to one of the following reasons:</span></span>

* <span data-ttu-id="8bea5-151">Nastąpiła próba zaktualizować jednostki, która nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="8bea5-151">An attempt was made to update an entity that does not exist.</span></span>
* <span data-ttu-id="8bea5-152">Nastąpiła próba można usunąć jednostki, która nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="8bea5-152">An attempt was made to delete an entity that does not exist.</span></span>
* <span data-ttu-id="8bea5-153">Próbowano utworzyć jednostki prowadzący do jednostki, która nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="8bea5-153">An attempt was made to create an entity that links to an entity that does not exist.</span></span>
* <span data-ttu-id="8bea5-154">Została podjęta próba pobrania jednostki, która nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="8bea5-154">An attempt was made to GET an entity that does not exist.</span></span>
* <span data-ttu-id="8bea5-155">Aby określić konto magazynu, który nie jest skojarzony z kontem usługi Media Services została podjęta próba.</span><span class="sxs-lookup"><span data-stu-id="8bea5-155">An attempt was made to specify a storage account that is not associated with the Media Services account.</span></span>  

## <a name="409-conflict"></a><span data-ttu-id="8bea5-156">409 Konflikt</span><span class="sxs-lookup"><span data-stu-id="8bea5-156">409 Conflict</span></span>
<span data-ttu-id="8bea5-157">Żądanie nie jest dozwolone z jednego z następujących powodów:</span><span class="sxs-lookup"><span data-stu-id="8bea5-157">The request is not allowed due to one of the following reasons:</span></span>

* <span data-ttu-id="8bea5-158">Więcej niż jeden AssetFile ma określoną nazwę, w ramach zasobu.</span><span class="sxs-lookup"><span data-stu-id="8bea5-158">More than one AssetFile has the specified name within the Asset.</span></span>
* <span data-ttu-id="8bea5-159">Próbowano utworzyć drugi AssetFile głównej w ramach zasobu.</span><span class="sxs-lookup"><span data-stu-id="8bea5-159">An attempt was made to create a second primary AssetFile within the Asset.</span></span>
* <span data-ttu-id="8bea5-160">Próbowano utworzyć ContentKey o określonym identyfikatorze już używana.</span><span class="sxs-lookup"><span data-stu-id="8bea5-160">An attempt was made to create a ContentKey with the specified Id already used.</span></span>
* <span data-ttu-id="8bea5-161">Próbowano utworzyć Lokalizator o określonym identyfikatorze już używana.</span><span class="sxs-lookup"><span data-stu-id="8bea5-161">An attempt was made to create a Locator with the specified Id already used.</span></span>
* <span data-ttu-id="8bea5-162">Więcej niż jeden IngestManifestFile ma określoną nazwę w IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="8bea5-162">More than one IngestManifestFile has the specified name within the IngestManifest.</span></span>
* <span data-ttu-id="8bea5-163">Nastąpiła próba połączyć drugi szyfrowanie magazynu ContentKey szyfrowane magazynu trwałego.</span><span class="sxs-lookup"><span data-stu-id="8bea5-163">An attempt was made to link a second storage encryption ContentKey to the storage-encrypted Asset.</span></span>
* <span data-ttu-id="8bea5-164">Nastąpiła próba połączyć ContentKey tego samego zasobu.</span><span class="sxs-lookup"><span data-stu-id="8bea5-164">An attempt was made to link the same ContentKey to the Asset.</span></span>
* <span data-ttu-id="8bea5-165">Próbowano utworzyć trwały, którego kontenera magazynu nie istnieje lub nie jest już skojarzona z trwałym.</span><span class="sxs-lookup"><span data-stu-id="8bea5-165">An attempt was made to create a locator to an Asset whose storage container is missing or is no longer associated with the Asset.</span></span>
* <span data-ttu-id="8bea5-166">Próbowano utworzyć do elementu zawartości, który ma już lokalizatorów 5 w użyciu.</span><span class="sxs-lookup"><span data-stu-id="8bea5-166">An attempt was made to create a locator to an Asset which already has 5 locators in use.</span></span> <span data-ttu-id="8bea5-167">(Usługa azure Storage wymusza limit pięciu zasady dostępu współużytkowanego na jeden kontener magazynu).</span><span class="sxs-lookup"><span data-stu-id="8bea5-167">(Azure Storage enforces the limit of five shared access policies on one storage container.)</span></span>
* <span data-ttu-id="8bea5-168">Łączenie z kontem magazynu trwałego do IngestManifestAsset nie jest taka sama, co konto magazynu używane przez element nadrzędny IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="8bea5-168">Linking storage account of an Asset to an IngestManifestAsset is not the same as the storage account used by the parent IngestManifest.</span></span>  

## <a name="500-internal-server-error"></a><span data-ttu-id="8bea5-169">500 Wewnętrzny błąd serwera</span><span class="sxs-lookup"><span data-stu-id="8bea5-169">500 Internal Server Error</span></span>
<span data-ttu-id="8bea5-170">Podczas przetwarzania żądania usługi Media Services napotka błąd uniemożliwiający przetwarzania przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="8bea5-170">During the processing of the request, Media Services encounters some error that prevents the processing from continuing.</span></span> <span data-ttu-id="8bea5-171">Może to być spowodowane jedną z następujących przyczyn:</span><span class="sxs-lookup"><span data-stu-id="8bea5-171">This could be due to one of the following reasons:</span></span>

* <span data-ttu-id="8bea5-172">Tworzenie zasobu lub zadanie nie powiedzie się, ponieważ informacje o limicie przydziału usługi konta usługi Media Services jest tymczasowo niedostępna.</span><span class="sxs-lookup"><span data-stu-id="8bea5-172">Creating an Asset or Job fails because the Media Services account's service quota information is temporarily unavailable.</span></span>
* <span data-ttu-id="8bea5-173">Tworzenie zasobów lub IngestManifest kontenera magazynu obiektów blob nie powiedzie się, ponieważ informacje o koncie magazynu konta jest tymczasowo niedostępna.</span><span class="sxs-lookup"><span data-stu-id="8bea5-173">Creating an Asset or IngestManifest blob storage container fails because the account's storage account information is temporarily unavailable.</span></span>
* <span data-ttu-id="8bea5-174">Inne wystąpił nieoczekiwany błąd.</span><span class="sxs-lookup"><span data-stu-id="8bea5-174">Other unexpected error.</span></span>

## <a name="503-service-unavailable"></a><span data-ttu-id="8bea5-175">503 Usługa jest niedostępna</span><span class="sxs-lookup"><span data-stu-id="8bea5-175">503 Service Unavailable</span></span>
<span data-ttu-id="8bea5-176">Serwer nie może obecnie odbierać żądań.</span><span class="sxs-lookup"><span data-stu-id="8bea5-176">The server is currently unable to receive requests.</span></span> <span data-ttu-id="8bea5-177">Przyczyną tego błędu może być nadmiernego żądań do usługi.</span><span class="sxs-lookup"><span data-stu-id="8bea5-177">This error may be caused by excessive requests to the service.</span></span> <span data-ttu-id="8bea5-178">Usługa Media Services mechanizm ograniczania ogranicza użycie zasobów dla aplikacji, które należy nadmiernego żądania do usługi.</span><span class="sxs-lookup"><span data-stu-id="8bea5-178">Media Services throttling mechanism restricts the resource usage for applications that make excessive request to the service.</span></span>

> [!NOTE]
> <span data-ttu-id="8bea5-179">Sprawdź komunikat o błędzie i ciąg kodu błędu, aby uzyskać bardziej szczegółowe informacje o przyczynie się, że masz błąd 503.</span><span class="sxs-lookup"><span data-stu-id="8bea5-179">Check the error message and error code string to get more detailed information about the reason you got the 503 error.</span></span> <span data-ttu-id="8bea5-180">Ten błąd nie zawsze oznacza ograniczania.</span><span class="sxs-lookup"><span data-stu-id="8bea5-180">This error does not always mean throttling.</span></span>
> 
> 

<span data-ttu-id="8bea5-181">Opisy stanu możliwe są:</span><span class="sxs-lookup"><span data-stu-id="8bea5-181">Possible status descriptions are:</span></span>

* <span data-ttu-id="8bea5-182">"Serwer jest zajęty.</span><span class="sxs-lookup"><span data-stu-id="8bea5-182">"Server is busy.</span></span> <span data-ttu-id="8bea5-183">Uruchamia poprzedniej tego typu żądania zajęło więcej niż {0} sek."</span><span class="sxs-lookup"><span data-stu-id="8bea5-183">Previous runs of this type of request took more than {0} seconds."</span></span>
* <span data-ttu-id="8bea5-184">"Serwer jest zajęty.</span><span class="sxs-lookup"><span data-stu-id="8bea5-184">"Server is busy.</span></span> <span data-ttu-id="8bea5-185">Więcej niż {0} żądań na sekundę może być ograniczony."</span><span class="sxs-lookup"><span data-stu-id="8bea5-185">More than {0} requests per second can be throttled."</span></span>
* <span data-ttu-id="8bea5-186">"Serwer jest zajęty.</span><span class="sxs-lookup"><span data-stu-id="8bea5-186">"Server is busy.</span></span> <span data-ttu-id="8bea5-187">Więcej niż {0} żądania w ciągu sekund {1} może być ograniczony."</span><span class="sxs-lookup"><span data-stu-id="8bea5-187">More than {0} requests within {1} seconds can be throttled."</span></span>

<span data-ttu-id="8bea5-188">Do obsługi tego błędu, firma Microsoft zaleca używanie Logika ponawiania wykładniczego wycofywania.</span><span class="sxs-lookup"><span data-stu-id="8bea5-188">To handle this error, we recommend using exponential back-off retry logic.</span></span> <span data-ttu-id="8bea5-189">Oznacza to, za pomocą oczekiwania stopniowo dłużej między kolejnymi próbami kolejnych odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="8bea5-189">That means using progressively longer waits between retries for consecutive error responses.</span></span>  <span data-ttu-id="8bea5-190">Aby uzyskać więcej informacji, zobacz [bloku aplikacji obsługi błędów przejściowych](https://msdn.microsoft.com/library/hh680905.aspx).</span><span class="sxs-lookup"><span data-stu-id="8bea5-190">For more information, see [Transient Fault Handling Application Block](https://msdn.microsoft.com/library/hh680905.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="8bea5-191">Jeśli używasz [Azure Media Services SDK dla platformy .net](https://github.com/Azure/azure-sdk-for-media-services/tree/master), logikę ponawiania błąd 503 zostało zaimplementowane przez zestaw SDK.</span><span class="sxs-lookup"><span data-stu-id="8bea5-191">If you are using [Azure Media Services SDK for .Net](https://github.com/Azure/azure-sdk-for-media-services/tree/master), the retry logic for the 503 error has been implemented by the SDK.</span></span>  
> 
> 

## <a name="see-also"></a><span data-ttu-id="8bea5-192">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="8bea5-192">See Also</span></span>
[<span data-ttu-id="8bea5-193">Kody błędów zarządzania usługi multimediów</span><span class="sxs-lookup"><span data-stu-id="8bea5-193">Media Services Management Error Codes</span></span>](http://msdn.microsoft.com/library/windowsazure/dn167016.aspx)

## <a name="next-steps"></a><span data-ttu-id="8bea5-194">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8bea5-194">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8bea5-195">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="8bea5-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

