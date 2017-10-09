---
title: "aaaClient i serwer przechowywanie wersji zestawu SDK w usługach Mobile i aplikacje mobilne | Dokumentacja firmy Microsoft"
description: "Lista zestawów SDK klienta i zgodności serwera wersje zestawu SDK usług Mobile Services i usługi Azure Mobile Apps"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 35b19672-c9d6-49b5-b405-a6dcd1107cd5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5874b7455ea407ca8c77fb1bd03d97d0767ebb47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a><span data-ttu-id="9c87d-103">Przechowywanie wersji klienta i serwera w usługach Mobile i aplikacje mobilne</span><span class="sxs-lookup"><span data-stu-id="9c87d-103">Client and server versioning in Mobile Apps and Mobile Services</span></span>
<span data-ttu-id="9c87d-104">najnowszą wersję usług Azure Mobile Services Hello jest hello **Mobile Apps** funkcji Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="9c87d-104">hello latest version of Azure Mobile Services is hello **Mobile Apps** feature of Azure App Service.</span></span>

<span data-ttu-id="9c87d-105">Witaj klienta aplikacji mobilnych i zestawów SDK serwera są początkowo na podstawie usług Mobile Services, ale są one *nie* zgodne ze sobą.</span><span class="sxs-lookup"><span data-stu-id="9c87d-105">hello Mobile Apps client and server SDKs are originally based on those in Mobile Services, but they are *not* compatible with each other.</span></span>
<span data-ttu-id="9c87d-106">Oznacza to, należy użyć *Mobile Apps* zestawu SDK klienta z *Mobile Apps* serwera zestawu SDK i podobnie dla *usług Mobile Services*.</span><span class="sxs-lookup"><span data-stu-id="9c87d-106">That is, you must use a *Mobile Apps* client SDK with a *Mobile Apps* server SDK and similarly for *Mobile Services*.</span></span> <span data-ttu-id="9c87d-107">Niniejsza Umowa jest wymuszane za pośrednictwem wartość nagłówka specjalnych używanych przez powitania klienta i serwera zestawów SDK, `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="9c87d-107">This contract is enforced through a special header value used by hello client and server SDKs, `ZUMO-API-VERSION`.</span></span>

<span data-ttu-id="9c87d-108">Uwaga: po każdej zmianie tego dokumentu dotyczy tooa *usług Mobile Services* wewnętrznej bazy danych, nie zawsze musi toobe hostowanych w usłudze Mobile Services.</span><span class="sxs-lookup"><span data-stu-id="9c87d-108">Note: whenever this document refers tooa *Mobile Services* backend, it does not necessarily need toobe hosted on Mobile Services.</span></span> <span data-ttu-id="9c87d-109">Teraz jest możliwe toomigrate toorun usługi mobilnej w usłudze aplikacji bez wprowadzania żadnych zmian kodu, ale usługa hello będą nadal stosowane *usług Mobile Services* wersji zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="9c87d-109">It is now possible toomigrate a mobile service toorun on App Service without any code changes, but hello service would still be using *Mobile Services*  SDK versions.</span></span>

<span data-ttu-id="9c87d-110">więcej informacji o toolearn migracji tooApp usługi bez wprowadzania żadnych zmian kodu zawiera artykuł hello [migracji tooAzure usługi Mobile App Service].</span><span class="sxs-lookup"><span data-stu-id="9c87d-110">toolearn more about migrating tooApp Service without any code changes, see hello article [Migrate a Mobile Service tooAzure App Service].</span></span>

## <a name="header-specification"></a><span data-ttu-id="9c87d-111">Specyfikacja nagłówka</span><span class="sxs-lookup"><span data-stu-id="9c87d-111">Header specification</span></span>
<span data-ttu-id="9c87d-112">klucz Hello `ZUMO-API-VERSION` można określić nagłówka hello HTTP lub hello ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="9c87d-112">hello key `ZUMO-API-VERSION` may be specified in either hello HTTP header or hello query string.</span></span> <span data-ttu-id="9c87d-113">wartość Hello jest ciąg wersji w postaci hello **x.y.z**.</span><span class="sxs-lookup"><span data-stu-id="9c87d-113">hello value is a version string in hello form **x.y.z**.</span></span>

<span data-ttu-id="9c87d-114">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="9c87d-114">For example:</span></span>

<span data-ttu-id="9c87d-115">Pobierz https://service.azurewebsites.net/tables/TodoItem</span><span class="sxs-lookup"><span data-stu-id="9c87d-115">GET https://service.azurewebsites.net/tables/TodoItem</span></span>

<span data-ttu-id="9c87d-116">NAGŁÓWKI: ZUMO-API-VERSION: 2.0.0</span><span class="sxs-lookup"><span data-stu-id="9c87d-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span></span>

<span data-ttu-id="9c87d-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span><span class="sxs-lookup"><span data-stu-id="9c87d-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span></span>

## <a name="opting-out-of-version-checking"></a><span data-ttu-id="9c87d-118">Rezygnacja z kontroli wersji</span><span class="sxs-lookup"><span data-stu-id="9c87d-118">Opting out of version checking</span></span>
<span data-ttu-id="9c87d-119">Można zrezygnować z wersji sprawdzanie przez ustawienie wartości **true** dla ustawienia aplikacji hello **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="9c87d-119">You can opt out of version checking by setting a value of **true** for hello app setting **MS_SkipVersionCheck**.</span></span> <span data-ttu-id="9c87d-120">Określ, w pliku web.config albo w hello sekcji Ustawienia aplikacji hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9c87d-120">Specify this either in your web.config or in hello Application Settings section of hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="9c87d-121">Istnieje wiele zmian zachowania między usług Mobile Services i aplikacji mobilnych, zwłaszcza w obszarach hello synchronizacji w trybie offline, uwierzytelniania i powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="9c87d-121">There are a number of behavior changes between Mobile Services and Mobile Apps, particularly in hello areas of offline sync, authentication, and push notifications.</span></span> <span data-ttu-id="9c87d-122">Należy tylko opcja rezygnacji z wersji sprawdzania po pełną tooensure testowych, czy te zmiany zachowania nie dzielone funkcjonalności aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c87d-122">You should only opt out of version checking after complete testing tooensure that these behavioral changes do not break your app's functionality.</span></span>
>
>

## <a name="summary-of-compatibility-for-all-versions"></a><span data-ttu-id="9c87d-123">Podsumowanie zgodności dla wszystkich wersji</span><span class="sxs-lookup"><span data-stu-id="9c87d-123">Summary of compatibility for all versions</span></span>
<span data-ttu-id="9c87d-124">Wykres Hello poniżej przedstawia zgodność hello wszystkie typy klienta i serwera.</span><span class="sxs-lookup"><span data-stu-id="9c87d-124">hello chart below shows hello compatibility between all client and server types.</span></span> <span data-ttu-id="9c87d-125">Wewnętrznej bazie danych zostanie sklasyfikowany jako albo Mobile **usług** lub Mobile **aplikacji** oparte na powitania serwera zestawu SDK, który go używa.</span><span class="sxs-lookup"><span data-stu-id="9c87d-125">A backend is classified as either Mobile **Services** or Mobile **Apps** based on hello server SDK that it uses.</span></span>

|  | <span data-ttu-id="9c87d-126">**Usługi mobilne** Node.js lub .NET</span><span class="sxs-lookup"><span data-stu-id="9c87d-126">**Mobile Services** Node.js or .NET</span></span> | <span data-ttu-id="9c87d-127">**Aplikacje mobilne** Node.js lub .NET</span><span class="sxs-lookup"><span data-stu-id="9c87d-127">**Mobile Apps** Node.js or .NET</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9c87d-128">[Klienci usług Mobile Services]</span><span class="sxs-lookup"><span data-stu-id="9c87d-128">[Mobile Services clients]</span></span> |<span data-ttu-id="9c87d-129">Ok</span><span class="sxs-lookup"><span data-stu-id="9c87d-129">Ok</span></span> |<span data-ttu-id="9c87d-130">Błąd\*</span><span class="sxs-lookup"><span data-stu-id="9c87d-130">Error\*</span></span> |
| <span data-ttu-id="9c87d-131">[Aplikacje mobilne klientów]</span><span class="sxs-lookup"><span data-stu-id="9c87d-131">[Mobile Apps clients]</span></span> |<span data-ttu-id="9c87d-132">Błąd\*</span><span class="sxs-lookup"><span data-stu-id="9c87d-132">Error\*</span></span> |<span data-ttu-id="9c87d-133">Ok</span><span class="sxs-lookup"><span data-stu-id="9c87d-133">Ok</span></span> |

<span data-ttu-id="9c87d-134">\*Może to być kontrolowane przez określenie **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="9c87d-134">\*This can be controlled by specifying **MS_SkipVersionCheck**.</span></span>

<!-- IMPORTANT!  hello anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: hello fwlink toothis document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <span data-ttu-id="9c87d-135"><a name="1.0.0"></a>Usługi mobilne klienta i serwera</span><span class="sxs-lookup"><span data-stu-id="9c87d-135"><a name="1.0.0"></a>Mobile Services client and server</span></span>
<span data-ttu-id="9c87d-136">powitania klienta zestawów SDK w poniższej tabeli hello są zgodne z **usług Mobile Services**.</span><span class="sxs-lookup"><span data-stu-id="9c87d-136">hello client SDKs in hello table below are compatible with **Mobile Services**.</span></span>

<span data-ttu-id="9c87d-137">Uwaga: hello zestawów SDK klienta usługi Mobile Services *nie* wysyłania wartości nagłówka `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="9c87d-137">Note: hello Mobile Services client SDKs *do not* send a header value for `ZUMO-API-VERSION`.</span></span> <span data-ttu-id="9c87d-138">Jeśli usługa hello odbiera ten nagłówek lub ciąg zapytania zostanie zwrócony błąd, chyba że jawnie użytkownik zgodził się zgodnie z powyższym opisem.</span><span class="sxs-lookup"><span data-stu-id="9c87d-138">If hello service receives this header or query string value, an error will be returned, unless you have explicitly opted out as described above.</span></span>

### <span data-ttu-id="9c87d-139"><a name="MobileServicesClients"></a>Mobile *usług* zestawów SDK klienta</span><span class="sxs-lookup"><span data-stu-id="9c87d-139"><a name="MobileServicesClients"></a> Mobile *Services* client SDKs</span></span>
| <span data-ttu-id="9c87d-140">Platforma klienta</span><span class="sxs-lookup"><span data-stu-id="9c87d-140">Client platform</span></span> | <span data-ttu-id="9c87d-141">Wersja</span><span class="sxs-lookup"><span data-stu-id="9c87d-141">Version</span></span> | <span data-ttu-id="9c87d-142">Wartość nagłówka wersji</span><span class="sxs-lookup"><span data-stu-id="9c87d-142">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9c87d-143">Klient zarządzany (z systemem Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="9c87d-143">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="9c87d-144">1.3.2</span><span class="sxs-lookup"><span data-stu-id="9c87d-144">1.3.2</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |<span data-ttu-id="9c87d-145">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="9c87d-145">n/a</span></span> |
| <span data-ttu-id="9c87d-146">iOS</span><span class="sxs-lookup"><span data-stu-id="9c87d-146">iOS</span></span> |[<span data-ttu-id="9c87d-147">2.2.2</span><span class="sxs-lookup"><span data-stu-id="9c87d-147">2.2.2</span></span>](http://aka.ms/gc6fex) |<span data-ttu-id="9c87d-148">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="9c87d-148">n/a</span></span> |
| <span data-ttu-id="9c87d-149">Android</span><span class="sxs-lookup"><span data-stu-id="9c87d-149">Android</span></span> |[<span data-ttu-id="9c87d-150">2.0.3</span><span class="sxs-lookup"><span data-stu-id="9c87d-150">2.0.3</span></span>](https://go.microsoft.com/fwLink/?LinkID=280126) |<span data-ttu-id="9c87d-151">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="9c87d-151">n/a</span></span> |
| <span data-ttu-id="9c87d-152">HTML</span><span class="sxs-lookup"><span data-stu-id="9c87d-152">HTML</span></span> |[<span data-ttu-id="9c87d-153">1.2.7</span><span class="sxs-lookup"><span data-stu-id="9c87d-153">1.2.7</span></span>](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |<span data-ttu-id="9c87d-154">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="9c87d-154">n/a</span></span> |

### <a name="mobile-services-server-sdks"></a><span data-ttu-id="9c87d-155">Mobile *usług* server SDK</span><span class="sxs-lookup"><span data-stu-id="9c87d-155">Mobile *Services* server SDKs</span></span>
| <span data-ttu-id="9c87d-156">Platforma serwera</span><span class="sxs-lookup"><span data-stu-id="9c87d-156">Server platform</span></span> | <span data-ttu-id="9c87d-157">Wersja</span><span class="sxs-lookup"><span data-stu-id="9c87d-157">Version</span></span> | <span data-ttu-id="9c87d-158">Zaakceptowana wersja nagłówka</span><span class="sxs-lookup"><span data-stu-id="9c87d-158">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9c87d-159">.NET</span><span class="sxs-lookup"><span data-stu-id="9c87d-159">.NET</span></span> |[<span data-ttu-id="9c87d-160">Wersja WindowsAzure.MobileServices.Backend.* 1.0.x</span><span class="sxs-lookup"><span data-stu-id="9c87d-160">WindowsAzure.MobileServices.Backend.* Version 1.0.x</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |<span data-ttu-id="9c87d-161">** Bez nagłówka wersji **</span><span class="sxs-lookup"><span data-stu-id="9c87d-161">**No version header **</span></span> |
| <span data-ttu-id="9c87d-162">Node.js</span><span class="sxs-lookup"><span data-stu-id="9c87d-162">Node.js</span></span> |<span data-ttu-id="9c87d-163">(wkrótce)</span><span class="sxs-lookup"><span data-stu-id="9c87d-163">(coming soon)</span></span> |<span data-ttu-id="9c87d-164">**Brak nagłówka wersji**</span><span class="sxs-lookup"><span data-stu-id="9c87d-164">**No version header**</span></span> |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a><span data-ttu-id="9c87d-165">Zachowanie zapleczy usług mobilnych</span><span class="sxs-lookup"><span data-stu-id="9c87d-165">Behavior of Mobile Services backends</span></span>
| <span data-ttu-id="9c87d-166">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="9c87d-166">ZUMO-API-VERSION</span></span> | <span data-ttu-id="9c87d-167">Wartość MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="9c87d-167">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="9c87d-168">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="9c87d-168">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9c87d-169">Nie określono</span><span class="sxs-lookup"><span data-stu-id="9c87d-169">Not specified</span></span> |<span data-ttu-id="9c87d-170">Dowolne</span><span class="sxs-lookup"><span data-stu-id="9c87d-170">Any</span></span> |<span data-ttu-id="9c87d-171">200 - OK</span><span class="sxs-lookup"><span data-stu-id="9c87d-171">200 - OK</span></span> |
| <span data-ttu-id="9c87d-172">Dowolna wartość</span><span class="sxs-lookup"><span data-stu-id="9c87d-172">Any value</span></span> |<span data-ttu-id="9c87d-173">True</span><span class="sxs-lookup"><span data-stu-id="9c87d-173">True</span></span> |<span data-ttu-id="9c87d-174">200 - OK</span><span class="sxs-lookup"><span data-stu-id="9c87d-174">200 - OK</span></span> |
| <span data-ttu-id="9c87d-175">Dowolna wartość</span><span class="sxs-lookup"><span data-stu-id="9c87d-175">Any value</span></span> |<span data-ttu-id="9c87d-176">Określona wartość false nie</span><span class="sxs-lookup"><span data-stu-id="9c87d-176">False/Not Specified</span></span> |<span data-ttu-id="9c87d-177">400 - Niewłaściwe żądanie</span><span class="sxs-lookup"><span data-stu-id="9c87d-177">400 - Bad Request</span></span> |

## <span data-ttu-id="9c87d-178"><a name="2.0.0"></a>Azure Mobile Apps klienta i serwera</span><span class="sxs-lookup"><span data-stu-id="9c87d-178"><a name="2.0.0"></a>Azure Mobile Apps client and server</span></span>
### <span data-ttu-id="9c87d-179"><a name="MobileAppsClients"></a>Mobile *aplikacji* zestawów SDK klienta</span><span class="sxs-lookup"><span data-stu-id="9c87d-179"><a name="MobileAppsClients"></a> Mobile *Apps* client SDKs</span></span>
<span data-ttu-id="9c87d-180">Sprawdzanie wersji wprowadzono począwszy hello następujące wersje klienta hello zestawu SDK dla **Azure Mobile Apps**:</span><span class="sxs-lookup"><span data-stu-id="9c87d-180">Version checking was introduced starting with hello following versions of hello client SDK for **Azure Mobile Apps**:</span></span>

| <span data-ttu-id="9c87d-181">Platforma klienta</span><span class="sxs-lookup"><span data-stu-id="9c87d-181">Client platform</span></span> | <span data-ttu-id="9c87d-182">Wersja</span><span class="sxs-lookup"><span data-stu-id="9c87d-182">Version</span></span> | <span data-ttu-id="9c87d-183">Wartość nagłówka wersji</span><span class="sxs-lookup"><span data-stu-id="9c87d-183">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9c87d-184">Klient zarządzany (z systemem Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="9c87d-184">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="9c87d-185">2.0.0</span><span class="sxs-lookup"><span data-stu-id="9c87d-185">2.0.0</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |<span data-ttu-id="9c87d-186">2.0.0</span><span class="sxs-lookup"><span data-stu-id="9c87d-186">2.0.0</span></span> |
| <span data-ttu-id="9c87d-187">iOS</span><span class="sxs-lookup"><span data-stu-id="9c87d-187">iOS</span></span> |[<span data-ttu-id="9c87d-188">3.0.0</span><span class="sxs-lookup"><span data-stu-id="9c87d-188">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=529823) |<span data-ttu-id="9c87d-189">2.0.0</span><span class="sxs-lookup"><span data-stu-id="9c87d-189">2.0.0</span></span> |
| <span data-ttu-id="9c87d-190">Android</span><span class="sxs-lookup"><span data-stu-id="9c87d-190">Android</span></span> |[<span data-ttu-id="9c87d-191">3.0.0</span><span class="sxs-lookup"><span data-stu-id="9c87d-191">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |<span data-ttu-id="9c87d-192">3.0.0</span><span class="sxs-lookup"><span data-stu-id="9c87d-192">3.0.0</span></span> |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a><span data-ttu-id="9c87d-193">Mobile *aplikacji* server SDK</span><span class="sxs-lookup"><span data-stu-id="9c87d-193">Mobile *Apps* server SDKs</span></span>
<span data-ttu-id="9c87d-194">Sprawdzanie wersji znajduje się w następujących wersjach zestawu SDK serwera:</span><span class="sxs-lookup"><span data-stu-id="9c87d-194">Version checking is included in following server SDK versions:</span></span>

| <span data-ttu-id="9c87d-195">Platforma serwera</span><span class="sxs-lookup"><span data-stu-id="9c87d-195">Server platform</span></span> | <span data-ttu-id="9c87d-196">SDK</span><span class="sxs-lookup"><span data-stu-id="9c87d-196">SDK</span></span> | <span data-ttu-id="9c87d-197">Zaakceptowana wersja nagłówka</span><span class="sxs-lookup"><span data-stu-id="9c87d-197">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9c87d-198">.NET</span><span class="sxs-lookup"><span data-stu-id="9c87d-198">.NET</span></span> |[<span data-ttu-id="9c87d-199">Microsoft.Azure.Mobile.Server</span><span class="sxs-lookup"><span data-stu-id="9c87d-199">Microsoft.Azure.Mobile.Server</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |<span data-ttu-id="9c87d-200">2.0.0</span><span class="sxs-lookup"><span data-stu-id="9c87d-200">2.0.0</span></span> |
| <span data-ttu-id="9c87d-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="9c87d-201">Node.js</span></span> |[<span data-ttu-id="9c87d-202">aplikacje Azure-mobile)</span><span class="sxs-lookup"><span data-stu-id="9c87d-202">azure-mobile-apps)</span></span>](https://www.npmjs.com/package/azure-mobile-apps) |<span data-ttu-id="9c87d-203">2.0.0</span><span class="sxs-lookup"><span data-stu-id="9c87d-203">2.0.0</span></span> |

### <a name="behavior-of-mobile-apps-backends"></a><span data-ttu-id="9c87d-204">Zachowanie zapleczy aplikacji mobilnych</span><span class="sxs-lookup"><span data-stu-id="9c87d-204">Behavior of Mobile Apps backends</span></span>
| <span data-ttu-id="9c87d-205">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="9c87d-205">ZUMO-API-VERSION</span></span> | <span data-ttu-id="9c87d-206">Wartość MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="9c87d-206">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="9c87d-207">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="9c87d-207">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9c87d-208">x.y.z ani mieć wartości Null</span><span class="sxs-lookup"><span data-stu-id="9c87d-208">x.y.z or Null</span></span> |<span data-ttu-id="9c87d-209">True</span><span class="sxs-lookup"><span data-stu-id="9c87d-209">True</span></span> |<span data-ttu-id="9c87d-210">200 - OK</span><span class="sxs-lookup"><span data-stu-id="9c87d-210">200 - OK</span></span> |
| <span data-ttu-id="9c87d-211">Wartość null</span><span class="sxs-lookup"><span data-stu-id="9c87d-211">Null</span></span> |<span data-ttu-id="9c87d-212">Określona wartość false nie</span><span class="sxs-lookup"><span data-stu-id="9c87d-212">False/Not Specified</span></span> |<span data-ttu-id="9c87d-213">400 - Niewłaściwe żądanie</span><span class="sxs-lookup"><span data-stu-id="9c87d-213">400 - Bad Request</span></span> |
| <span data-ttu-id="9c87d-214">1.x.y</span><span class="sxs-lookup"><span data-stu-id="9c87d-214">1.x.y</span></span> |<span data-ttu-id="9c87d-215">Określona wartość false nie</span><span class="sxs-lookup"><span data-stu-id="9c87d-215">False/Not Specified</span></span> |<span data-ttu-id="9c87d-216">400 - Niewłaściwe żądanie</span><span class="sxs-lookup"><span data-stu-id="9c87d-216">400 - Bad Request</span></span> |
| <span data-ttu-id="9c87d-217">2.0.0-2.x.y</span><span class="sxs-lookup"><span data-stu-id="9c87d-217">2.0.0-2.x.y</span></span> |<span data-ttu-id="9c87d-218">Określona wartość false nie</span><span class="sxs-lookup"><span data-stu-id="9c87d-218">False/Not Specified</span></span> |<span data-ttu-id="9c87d-219">200 - OK</span><span class="sxs-lookup"><span data-stu-id="9c87d-219">200 - OK</span></span> |
| <span data-ttu-id="9c87d-220">3.0.0-3.x.y</span><span class="sxs-lookup"><span data-stu-id="9c87d-220">3.0.0-3.x.y</span></span> |<span data-ttu-id="9c87d-221">Określona wartość false nie</span><span class="sxs-lookup"><span data-stu-id="9c87d-221">False/Not Specified</span></span> |<span data-ttu-id="9c87d-222">400 - Niewłaściwe żądanie</span><span class="sxs-lookup"><span data-stu-id="9c87d-222">400 - Bad Request</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9c87d-223">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9c87d-223">Next Steps</span></span>
* <span data-ttu-id="9c87d-224">[migracji tooAzure usługi Mobile App Service]</span><span class="sxs-lookup"><span data-stu-id="9c87d-224">[Migrate a Mobile Service tooAzure App Service]</span></span>

[Klienci usług Mobile Services]: #MobileServicesClients
[Aplikacje mobilne klientów]: #MobileAppsClients


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[migracji tooAzure usługi Mobile App Service]: app-service-mobile-migrating-from-mobile-services.md
