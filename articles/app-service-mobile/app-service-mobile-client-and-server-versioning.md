---
title: "Klient i serwer przechowywanie wersji zestawu SDK w Mobile Apps i usług Mobile Services | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: f79e819b1547f81498ea213858faf3c75e374782
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a><span data-ttu-id="c69a7-103">Przechowywanie wersji klienta i serwera w usługach Mobile i aplikacje mobilne</span><span class="sxs-lookup"><span data-stu-id="c69a7-103">Client and server versioning in Mobile Apps and Mobile Services</span></span>
<span data-ttu-id="c69a7-104">Najnowszą wersję usług Azure Mobile Services **Mobile Apps** funkcji Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="c69a7-104">The latest version of Azure Mobile Services is the **Mobile Apps** feature of Azure App Service.</span></span>

<span data-ttu-id="c69a7-105">Mobile Apps SDK klienta i serwera są początkowo na podstawie usług Mobile Services, ale są one *nie* zgodne ze sobą.</span><span class="sxs-lookup"><span data-stu-id="c69a7-105">The Mobile Apps client and server SDKs are originally based on those in Mobile Services, but they are *not* compatible with each other.</span></span>
<span data-ttu-id="c69a7-106">Oznacza to, należy użyć *Mobile Apps* zestawu SDK klienta z *Mobile Apps* serwera zestawu SDK i podobnie dla *usług Mobile Services*.</span><span class="sxs-lookup"><span data-stu-id="c69a7-106">That is, you must use a *Mobile Apps* client SDK with a *Mobile Apps* server SDK and similarly for *Mobile Services*.</span></span> <span data-ttu-id="c69a7-107">Niniejsza Umowa jest wymuszane za pośrednictwem wartość nagłówka specjalnych używanych przez klienta i serwera zestawów SDK, `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="c69a7-107">This contract is enforced through a special header value used by the client and server SDKs, `ZUMO-API-VERSION`.</span></span>

<span data-ttu-id="c69a7-108">Uwaga: po każdej zmianie tego dokumentu dotyczy *usług Mobile Services* wewnętrznej bazy danych, nie zawsze musi ma być obsługiwana w usłudze Mobile Services.</span><span class="sxs-lookup"><span data-stu-id="c69a7-108">Note: whenever this document refers to a *Mobile Services* backend, it does not necessarily need to be hosted on Mobile Services.</span></span> <span data-ttu-id="c69a7-109">Obecnie istnieje możliwość migracji usługi mobilnej do uruchamiania w usłudze aplikacji bez żadnych zmian w kodzie, ale usługi będą nadal stosowane *usług Mobile Services* wersji zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="c69a7-109">It is now possible to migrate a mobile service to run on App Service without any code changes, but the service would still be using *Mobile Services*  SDK versions.</span></span>

<span data-ttu-id="c69a7-110">Aby dowiedzieć się więcej na temat migracji do usługi aplikacji bez wprowadzania żadnych zmian kodu, zobacz artykuł [migracji usługi mobilnej w usłudze Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="c69a7-110">To learn more about migrating to App Service without any code changes, see the article [Migrate a Mobile Service to Azure App Service].</span></span>

## <a name="header-specification"></a><span data-ttu-id="c69a7-111">Specyfikacja nagłówka</span><span class="sxs-lookup"><span data-stu-id="c69a7-111">Header specification</span></span>
<span data-ttu-id="c69a7-112">Klucz `ZUMO-API-VERSION` mogą być określone w nagłówku HTTP lub ciąg zapytania.</span><span class="sxs-lookup"><span data-stu-id="c69a7-112">The key `ZUMO-API-VERSION` may be specified in either the HTTP header or the query string.</span></span> <span data-ttu-id="c69a7-113">Wartość jest ciąg wersji w postaci **x.y.z**.</span><span class="sxs-lookup"><span data-stu-id="c69a7-113">The value is a version string in the form **x.y.z**.</span></span>

<span data-ttu-id="c69a7-114">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c69a7-114">For example:</span></span>

<span data-ttu-id="c69a7-115">Pobierz https://service.azurewebsites.net/tables/TodoItem</span><span class="sxs-lookup"><span data-stu-id="c69a7-115">GET https://service.azurewebsites.net/tables/TodoItem</span></span>

<span data-ttu-id="c69a7-116">NAGŁÓWKI: ZUMO-API-VERSION: 2.0.0</span><span class="sxs-lookup"><span data-stu-id="c69a7-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span></span>

<span data-ttu-id="c69a7-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span><span class="sxs-lookup"><span data-stu-id="c69a7-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span></span>

## <a name="opting-out-of-version-checking"></a><span data-ttu-id="c69a7-118">Rezygnacja z kontroli wersji</span><span class="sxs-lookup"><span data-stu-id="c69a7-118">Opting out of version checking</span></span>
<span data-ttu-id="c69a7-119">Można zrezygnować z wersji sprawdzanie przez ustawienie wartości **true** dla ustawienia aplikacji **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="c69a7-119">You can opt out of version checking by setting a value of **true** for the app setting **MS_SkipVersionCheck**.</span></span> <span data-ttu-id="c69a7-120">Określ, w pliku web.config lub w sekcji Ustawienia aplikacji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c69a7-120">Specify this either in your web.config or in the Application Settings section of the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="c69a7-121">Istnieje wiele zmian zachowania między usług Mobile Services i aplikacji mobilnych, zwłaszcza w obszarach synchronizacji w trybie offline, uwierzytelniania i powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="c69a7-121">There are a number of behavior changes between Mobile Services and Mobile Apps, particularly in the areas of offline sync, authentication, and push notifications.</span></span> <span data-ttu-id="c69a7-122">Należy tylko opcja rezygnacji z wersji sprawdzania po Ukończ testowanie, aby upewnić się, że te zmiany zachowania nie dzielone funkcjonalności aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c69a7-122">You should only opt out of version checking after complete testing to ensure that these behavioral changes do not break your app's functionality.</span></span>
>
>

## <a name="summary-of-compatibility-for-all-versions"></a><span data-ttu-id="c69a7-123">Podsumowanie zgodności dla wszystkich wersji</span><span class="sxs-lookup"><span data-stu-id="c69a7-123">Summary of compatibility for all versions</span></span>
<span data-ttu-id="c69a7-124">Poniższej tabeli przedstawiono informacje o zgodności między wszystkie typy klienta i serwera.</span><span class="sxs-lookup"><span data-stu-id="c69a7-124">The chart below shows the compatibility between all client and server types.</span></span> <span data-ttu-id="c69a7-125">Wewnętrznej bazie danych zostanie sklasyfikowany jako albo Mobile **usług** lub Mobile **aplikacji** na podstawie zestawu SDK, który używa serwera.</span><span class="sxs-lookup"><span data-stu-id="c69a7-125">A backend is classified as either Mobile **Services** or Mobile **Apps** based on the server SDK that it uses.</span></span>

|  | <span data-ttu-id="c69a7-126">**Usługi mobilne** Node.js lub .NET</span><span class="sxs-lookup"><span data-stu-id="c69a7-126">**Mobile Services** Node.js or .NET</span></span> | <span data-ttu-id="c69a7-127">**Aplikacje mobilne** Node.js lub .NET</span><span class="sxs-lookup"><span data-stu-id="c69a7-127">**Mobile Apps** Node.js or .NET</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c69a7-128">[Klienci usług Mobile Services]</span><span class="sxs-lookup"><span data-stu-id="c69a7-128">[Mobile Services clients]</span></span> |<span data-ttu-id="c69a7-129">Ok</span><span class="sxs-lookup"><span data-stu-id="c69a7-129">Ok</span></span> |<span data-ttu-id="c69a7-130">Błąd\*</span><span class="sxs-lookup"><span data-stu-id="c69a7-130">Error\*</span></span> |
| <span data-ttu-id="c69a7-131">[Aplikacje mobilne klientów]</span><span class="sxs-lookup"><span data-stu-id="c69a7-131">[Mobile Apps clients]</span></span> |<span data-ttu-id="c69a7-132">Błąd\*</span><span class="sxs-lookup"><span data-stu-id="c69a7-132">Error\*</span></span> |<span data-ttu-id="c69a7-133">Ok</span><span class="sxs-lookup"><span data-stu-id="c69a7-133">Ok</span></span> |

<span data-ttu-id="c69a7-134">\*Może to być kontrolowane przez określenie **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="c69a7-134">\*This can be controlled by specifying **MS_SkipVersionCheck**.</span></span>

<!-- IMPORTANT!  The anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: the fwlink to this document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <span data-ttu-id="c69a7-135"><a name="1.0.0"></a>Usługi mobilne klienta i serwera</span><span class="sxs-lookup"><span data-stu-id="c69a7-135"><a name="1.0.0"></a>Mobile Services client and server</span></span>
<span data-ttu-id="c69a7-136">Zestawy SDK klienta w poniższej tabeli są zgodne z **usług Mobile Services**.</span><span class="sxs-lookup"><span data-stu-id="c69a7-136">The client SDKs in the table below are compatible with **Mobile Services**.</span></span>

<span data-ttu-id="c69a7-137">Uwaga: klientem usług Mobile Services SDK *nie* wysyłania wartości nagłówka `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="c69a7-137">Note: the Mobile Services client SDKs *do not* send a header value for `ZUMO-API-VERSION`.</span></span> <span data-ttu-id="c69a7-138">Gdy usługa odbiera ten nagłówek lub ciąg zapytania zostanie zwrócony błąd, chyba że jawnie użytkownik zgodził się zgodnie z powyższym opisem.</span><span class="sxs-lookup"><span data-stu-id="c69a7-138">If the service receives this header or query string value, an error will be returned, unless you have explicitly opted out as described above.</span></span>

### <span data-ttu-id="c69a7-139"><a name="MobileServicesClients"></a>Mobile *usług* zestawów SDK klienta</span><span class="sxs-lookup"><span data-stu-id="c69a7-139"><a name="MobileServicesClients"></a> Mobile *Services* client SDKs</span></span>
| <span data-ttu-id="c69a7-140">Platforma klienta</span><span class="sxs-lookup"><span data-stu-id="c69a7-140">Client platform</span></span> | <span data-ttu-id="c69a7-141">Wersja</span><span class="sxs-lookup"><span data-stu-id="c69a7-141">Version</span></span> | <span data-ttu-id="c69a7-142">Wartość nagłówka wersji</span><span class="sxs-lookup"><span data-stu-id="c69a7-142">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c69a7-143">Klient zarządzany (z systemem Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="c69a7-143">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="c69a7-144">1.3.2</span><span class="sxs-lookup"><span data-stu-id="c69a7-144">1.3.2</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |<span data-ttu-id="c69a7-145">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="c69a7-145">n/a</span></span> |
| <span data-ttu-id="c69a7-146">iOS</span><span class="sxs-lookup"><span data-stu-id="c69a7-146">iOS</span></span> |[<span data-ttu-id="c69a7-147">2.2.2</span><span class="sxs-lookup"><span data-stu-id="c69a7-147">2.2.2</span></span>](http://aka.ms/gc6fex) |<span data-ttu-id="c69a7-148">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="c69a7-148">n/a</span></span> |
| <span data-ttu-id="c69a7-149">Android</span><span class="sxs-lookup"><span data-stu-id="c69a7-149">Android</span></span> |[<span data-ttu-id="c69a7-150">2.0.3</span><span class="sxs-lookup"><span data-stu-id="c69a7-150">2.0.3</span></span>](https://go.microsoft.com/fwLink/?LinkID=280126) |<span data-ttu-id="c69a7-151">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="c69a7-151">n/a</span></span> |
| <span data-ttu-id="c69a7-152">HTML</span><span class="sxs-lookup"><span data-stu-id="c69a7-152">HTML</span></span> |[<span data-ttu-id="c69a7-153">1.2.7</span><span class="sxs-lookup"><span data-stu-id="c69a7-153">1.2.7</span></span>](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |<span data-ttu-id="c69a7-154">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="c69a7-154">n/a</span></span> |

### <a name="mobile-services-server-sdks"></a><span data-ttu-id="c69a7-155">Mobile *usług* server SDK</span><span class="sxs-lookup"><span data-stu-id="c69a7-155">Mobile *Services* server SDKs</span></span>
| <span data-ttu-id="c69a7-156">Platforma serwera</span><span class="sxs-lookup"><span data-stu-id="c69a7-156">Server platform</span></span> | <span data-ttu-id="c69a7-157">Wersja</span><span class="sxs-lookup"><span data-stu-id="c69a7-157">Version</span></span> | <span data-ttu-id="c69a7-158">Zaakceptowana wersja nagłówka</span><span class="sxs-lookup"><span data-stu-id="c69a7-158">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c69a7-159">.NET</span><span class="sxs-lookup"><span data-stu-id="c69a7-159">.NET</span></span> |[<span data-ttu-id="c69a7-160">Wersja WindowsAzure.MobileServices.Backend.* 1.0.x</span><span class="sxs-lookup"><span data-stu-id="c69a7-160">WindowsAzure.MobileServices.Backend.* Version 1.0.x</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |<span data-ttu-id="c69a7-161">** Bez nagłówka wersji **</span><span class="sxs-lookup"><span data-stu-id="c69a7-161">**No version header **</span></span> |
| <span data-ttu-id="c69a7-162">Node.js</span><span class="sxs-lookup"><span data-stu-id="c69a7-162">Node.js</span></span> |<span data-ttu-id="c69a7-163">(wkrótce)</span><span class="sxs-lookup"><span data-stu-id="c69a7-163">(coming soon)</span></span> |<span data-ttu-id="c69a7-164">**Brak nagłówka wersji**</span><span class="sxs-lookup"><span data-stu-id="c69a7-164">**No version header**</span></span> |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a><span data-ttu-id="c69a7-165">Zachowanie zapleczy usług mobilnych</span><span class="sxs-lookup"><span data-stu-id="c69a7-165">Behavior of Mobile Services backends</span></span>
| <span data-ttu-id="c69a7-166">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="c69a7-166">ZUMO-API-VERSION</span></span> | <span data-ttu-id="c69a7-167">Wartość MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="c69a7-167">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="c69a7-168">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="c69a7-168">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c69a7-169">Nie określono</span><span class="sxs-lookup"><span data-stu-id="c69a7-169">Not specified</span></span> |<span data-ttu-id="c69a7-170">Dowolne</span><span class="sxs-lookup"><span data-stu-id="c69a7-170">Any</span></span> |<span data-ttu-id="c69a7-171">200 - OK</span><span class="sxs-lookup"><span data-stu-id="c69a7-171">200 - OK</span></span> |
| <span data-ttu-id="c69a7-172">Dowolna wartość</span><span class="sxs-lookup"><span data-stu-id="c69a7-172">Any value</span></span> |<span data-ttu-id="c69a7-173">True</span><span class="sxs-lookup"><span data-stu-id="c69a7-173">True</span></span> |<span data-ttu-id="c69a7-174">200 - OK</span><span class="sxs-lookup"><span data-stu-id="c69a7-174">200 - OK</span></span> |
| <span data-ttu-id="c69a7-175">Dowolna wartość</span><span class="sxs-lookup"><span data-stu-id="c69a7-175">Any value</span></span> |<span data-ttu-id="c69a7-176">Określona wartość false nie</span><span class="sxs-lookup"><span data-stu-id="c69a7-176">False/Not Specified</span></span> |<span data-ttu-id="c69a7-177">400 - Niewłaściwe żądanie</span><span class="sxs-lookup"><span data-stu-id="c69a7-177">400 - Bad Request</span></span> |

## <span data-ttu-id="c69a7-178"><a name="2.0.0"></a>Azure Mobile Apps klienta i serwera</span><span class="sxs-lookup"><span data-stu-id="c69a7-178"><a name="2.0.0"></a>Azure Mobile Apps client and server</span></span>
### <span data-ttu-id="c69a7-179"><a name="MobileAppsClients"></a>Mobile *aplikacji* zestawów SDK klienta</span><span class="sxs-lookup"><span data-stu-id="c69a7-179"><a name="MobileAppsClients"></a> Mobile *Apps* client SDKs</span></span>
<span data-ttu-id="c69a7-180">Sprawdzanie wersji wprowadzono począwszy od następujących wersji zestawu SDK klienta dla **Azure Mobile Apps**:</span><span class="sxs-lookup"><span data-stu-id="c69a7-180">Version checking was introduced starting with the following versions of the client SDK for **Azure Mobile Apps**:</span></span>

| <span data-ttu-id="c69a7-181">Platforma klienta</span><span class="sxs-lookup"><span data-stu-id="c69a7-181">Client platform</span></span> | <span data-ttu-id="c69a7-182">Wersja</span><span class="sxs-lookup"><span data-stu-id="c69a7-182">Version</span></span> | <span data-ttu-id="c69a7-183">Wartość nagłówka wersji</span><span class="sxs-lookup"><span data-stu-id="c69a7-183">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c69a7-184">Klient zarządzany (z systemem Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="c69a7-184">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="c69a7-185">2.0.0</span><span class="sxs-lookup"><span data-stu-id="c69a7-185">2.0.0</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |<span data-ttu-id="c69a7-186">2.0.0</span><span class="sxs-lookup"><span data-stu-id="c69a7-186">2.0.0</span></span> |
| <span data-ttu-id="c69a7-187">iOS</span><span class="sxs-lookup"><span data-stu-id="c69a7-187">iOS</span></span> |[<span data-ttu-id="c69a7-188">3.0.0</span><span class="sxs-lookup"><span data-stu-id="c69a7-188">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=529823) |<span data-ttu-id="c69a7-189">2.0.0</span><span class="sxs-lookup"><span data-stu-id="c69a7-189">2.0.0</span></span> |
| <span data-ttu-id="c69a7-190">Android</span><span class="sxs-lookup"><span data-stu-id="c69a7-190">Android</span></span> |[<span data-ttu-id="c69a7-191">3.0.0</span><span class="sxs-lookup"><span data-stu-id="c69a7-191">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |<span data-ttu-id="c69a7-192">3.0.0</span><span class="sxs-lookup"><span data-stu-id="c69a7-192">3.0.0</span></span> |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a><span data-ttu-id="c69a7-193">Mobile *aplikacji* server SDK</span><span class="sxs-lookup"><span data-stu-id="c69a7-193">Mobile *Apps* server SDKs</span></span>
<span data-ttu-id="c69a7-194">Sprawdzanie wersji znajduje się w następujących wersjach zestawu SDK serwera:</span><span class="sxs-lookup"><span data-stu-id="c69a7-194">Version checking is included in following server SDK versions:</span></span>

| <span data-ttu-id="c69a7-195">Platforma serwera</span><span class="sxs-lookup"><span data-stu-id="c69a7-195">Server platform</span></span> | <span data-ttu-id="c69a7-196">SDK</span><span class="sxs-lookup"><span data-stu-id="c69a7-196">SDK</span></span> | <span data-ttu-id="c69a7-197">Zaakceptowana wersja nagłówka</span><span class="sxs-lookup"><span data-stu-id="c69a7-197">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c69a7-198">.NET</span><span class="sxs-lookup"><span data-stu-id="c69a7-198">.NET</span></span> |[<span data-ttu-id="c69a7-199">Microsoft.Azure.Mobile.Server</span><span class="sxs-lookup"><span data-stu-id="c69a7-199">Microsoft.Azure.Mobile.Server</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |<span data-ttu-id="c69a7-200">2.0.0</span><span class="sxs-lookup"><span data-stu-id="c69a7-200">2.0.0</span></span> |
| <span data-ttu-id="c69a7-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="c69a7-201">Node.js</span></span> |[<span data-ttu-id="c69a7-202">aplikacje Azure-mobile)</span><span class="sxs-lookup"><span data-stu-id="c69a7-202">azure-mobile-apps)</span></span>](https://www.npmjs.com/package/azure-mobile-apps) |<span data-ttu-id="c69a7-203">2.0.0</span><span class="sxs-lookup"><span data-stu-id="c69a7-203">2.0.0</span></span> |

### <a name="behavior-of-mobile-apps-backends"></a><span data-ttu-id="c69a7-204">Zachowanie zapleczy aplikacji mobilnych</span><span class="sxs-lookup"><span data-stu-id="c69a7-204">Behavior of Mobile Apps backends</span></span>
| <span data-ttu-id="c69a7-205">ZUMO-API-VERSION</span><span class="sxs-lookup"><span data-stu-id="c69a7-205">ZUMO-API-VERSION</span></span> | <span data-ttu-id="c69a7-206">Wartość MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="c69a7-206">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="c69a7-207">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="c69a7-207">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c69a7-208">x.y.z ani mieć wartości Null</span><span class="sxs-lookup"><span data-stu-id="c69a7-208">x.y.z or Null</span></span> |<span data-ttu-id="c69a7-209">True</span><span class="sxs-lookup"><span data-stu-id="c69a7-209">True</span></span> |<span data-ttu-id="c69a7-210">200 - OK</span><span class="sxs-lookup"><span data-stu-id="c69a7-210">200 - OK</span></span> |
| <span data-ttu-id="c69a7-211">Wartość null</span><span class="sxs-lookup"><span data-stu-id="c69a7-211">Null</span></span> |<span data-ttu-id="c69a7-212">Określona wartość false nie</span><span class="sxs-lookup"><span data-stu-id="c69a7-212">False/Not Specified</span></span> |<span data-ttu-id="c69a7-213">400 - Niewłaściwe żądanie</span><span class="sxs-lookup"><span data-stu-id="c69a7-213">400 - Bad Request</span></span> |
| <span data-ttu-id="c69a7-214">1.x.y</span><span class="sxs-lookup"><span data-stu-id="c69a7-214">1.x.y</span></span> |<span data-ttu-id="c69a7-215">Określona wartość false nie</span><span class="sxs-lookup"><span data-stu-id="c69a7-215">False/Not Specified</span></span> |<span data-ttu-id="c69a7-216">400 - Niewłaściwe żądanie</span><span class="sxs-lookup"><span data-stu-id="c69a7-216">400 - Bad Request</span></span> |
| <span data-ttu-id="c69a7-217">2.0.0-2.x.y</span><span class="sxs-lookup"><span data-stu-id="c69a7-217">2.0.0-2.x.y</span></span> |<span data-ttu-id="c69a7-218">Określona wartość false nie</span><span class="sxs-lookup"><span data-stu-id="c69a7-218">False/Not Specified</span></span> |<span data-ttu-id="c69a7-219">200 - OK</span><span class="sxs-lookup"><span data-stu-id="c69a7-219">200 - OK</span></span> |
| <span data-ttu-id="c69a7-220">3.0.0-3.x.y</span><span class="sxs-lookup"><span data-stu-id="c69a7-220">3.0.0-3.x.y</span></span> |<span data-ttu-id="c69a7-221">Określona wartość false nie</span><span class="sxs-lookup"><span data-stu-id="c69a7-221">False/Not Specified</span></span> |<span data-ttu-id="c69a7-222">400 - Niewłaściwe żądanie</span><span class="sxs-lookup"><span data-stu-id="c69a7-222">400 - Bad Request</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c69a7-223">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c69a7-223">Next Steps</span></span>
* <span data-ttu-id="c69a7-224">[migracji usługi mobilnej w usłudze Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="c69a7-224">[Migrate a Mobile Service to Azure App Service]</span></span>

<span data-ttu-id="c69a7-225">[Klienci usług Mobile Services]: #MobileServicesClients</span><span class="sxs-lookup"><span data-stu-id="c69a7-225">[Mobile Services clients]: #MobileServicesClients</span></span>
<span data-ttu-id="c69a7-226">[Aplikacje mobilne klientów]: #MobileAppsClients</span><span class="sxs-lookup"><span data-stu-id="c69a7-226">[Mobile Apps clients]: #MobileAppsClients</span></span>


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
<span data-ttu-id="c69a7-227">[migracji usługi mobilnej w usłudze Azure App Service]: app-service-mobile-migrating-from-mobile-services.md</span><span class="sxs-lookup"><span data-stu-id="c69a7-227">[Migrate a Mobile Service to Azure App Service]: app-service-mobile-migrating-from-mobile-services.md</span></span>
