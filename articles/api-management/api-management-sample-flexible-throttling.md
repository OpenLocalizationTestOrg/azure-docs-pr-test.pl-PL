---
title: "Zaawansowane żądanie ograniczania z usługą Azure API Management"
description: "Dowiedz się, jak utworzyć i zastosować wskaźnik, ograniczając zasad z usługą Azure API Management i elastyczny przydział."
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: fc813a65-7793-4c17-8bb9-e387838193ae
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 35375e599891a9443a91c4c3a8657e8c9c48c7b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-request-throttling-with-azure-api-management"></a><span data-ttu-id="c2e54-103">Zaawansowane żądanie ograniczania z usługą Azure API Management</span><span class="sxs-lookup"><span data-stu-id="c2e54-103">Advanced request throttling with Azure API Management</span></span>
<span data-ttu-id="c2e54-104">Możliwość ograniczania żądań przychodzących jest kluczową rolę usługi Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="c2e54-104">Being able to throttle incoming requests is a key role of Azure API Management.</span></span> <span data-ttu-id="c2e54-105">Albo kontrolując współczynnika żądań lub całkowita liczba żądań/transferu danych, zarządzanie interfejsami API umożliwia dostawcom usług interfejsu API ochrony ich interfejsów API z nadużyć i utworzyć wartości dla różnych warstw produktu interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="c2e54-105">Either by controlling the rate of requests or the total requests/data transferred, API Management allows API providers to protect their APIs from abuse and create value for different API product tiers.</span></span>

## <a name="product-based-throttling"></a><span data-ttu-id="c2e54-106">Ograniczanie produktu w oparciu</span><span class="sxs-lookup"><span data-stu-id="c2e54-106">Product based throttling</span></span>
<span data-ttu-id="c2e54-107">Data, szybkość ograniczenie możliwości zostały ograniczone do ograniczone do określonej subskrypcji produktu (zasadniczo klucza), zdefiniowane w portalu zarządzania interfejsu API wydawcy.</span><span class="sxs-lookup"><span data-stu-id="c2e54-107">To date, the rate throttling capabilities have been limited to being scoped to a particular Product subscription (essentially a key), defined in the API Management publisher portal.</span></span> <span data-ttu-id="c2e54-108">Jest to przydatne w przypadku dostawcy interfejsu API w celu zastosowania ograniczeń na deweloperów, którzy utworzyli konto do użycia interfejsu API, jednak nie pomaga, na przykład w ograniczania indywidualnych użytkowników końcowych interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="c2e54-108">This is useful for the API provider to apply limits on the developers who have signed up to use their API, however, it does not help, for example, in throttling individual end-users of the API.</span></span> <span data-ttu-id="c2e54-109">Jest to możliwe, że dla pojedynczego użytkownika dewelopera aplikacji, aby korzystać z całego przydziału, a następnie uniemożliwić dewelopera innych klientów do korzystania z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c2e54-109">It is possible that for single user of the developer's application to consume the entire quota and then prevent other customers of the developer from being able to use the application.</span></span> <span data-ttu-id="c2e54-110">Ponadto wielu klientów, którzy mogą generować dużą liczbę żądań może ograniczyć dostęp do okazjonalne użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c2e54-110">Also, several customers who might generate a high volume of requests may limit access to occasional users.</span></span>

## <a name="custom-key-based-throttling"></a><span data-ttu-id="c2e54-111">Klucz niestandardowy na podstawie ograniczania przepustowości</span><span class="sxs-lookup"><span data-stu-id="c2e54-111">Custom key based throttling</span></span>
<span data-ttu-id="c2e54-112">Nowy [szybkość limit przez klucz](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) i [limitu przydziału przez klucz](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) udostępniają znacznie bardziej elastyczne rozwiązania do kontroli ruchu.</span><span class="sxs-lookup"><span data-stu-id="c2e54-112">The new [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies provide a significantly more flexible solution to traffic control.</span></span> <span data-ttu-id="c2e54-113">Te nowe zasady umożliwiają definiowanie wyrażenia, aby zidentyfikować klucze, które będą używane do śledzenia użycia ruchu.</span><span class="sxs-lookup"><span data-stu-id="c2e54-113">These new policies allow you to define expressions to identify the keys that will be used to track traffic usage.</span></span> <span data-ttu-id="c2e54-114">To działania easiest przedstawiono przykład.</span><span class="sxs-lookup"><span data-stu-id="c2e54-114">The way this works is easiest illustrated with an example.</span></span> 

## <a name="ip-address-throttling"></a><span data-ttu-id="c2e54-115">Ograniczenia adresów IP</span><span class="sxs-lookup"><span data-stu-id="c2e54-115">IP Address throttling</span></span>
<span data-ttu-id="c2e54-116">Następujące zasady ograniczyć adresów IP jednego klienta do wywołania tylko 10 co minutę, łączna liczba wywołań 1 000 000 i 10 000 kilobajtów przepustowości miesięcznie.</span><span class="sxs-lookup"><span data-stu-id="c2e54-116">The following policies restrict a single client IP address to only 10 calls every minute, with a total of 1,000,000 calls and 10,000 kilobytes of bandwidth per month.</span></span> 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

<span data-ttu-id="c2e54-117">Jeśli wszyscy klienci w Internecie używany unikatowy adres IP, może to być efektywnym sposobem ograniczenia użycia przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c2e54-117">If all clients on the Internet used a unique IP address, this might be an effective way of limiting usage by user.</span></span> <span data-ttu-id="c2e54-118">Jednak jest bardzo prawdopodobne, że wielu użytkowników będzie udostępnianie jeden publiczny adres IP z powodu ich dostęp do Internetu za pośrednictwem urządzenia translatora adresów Sieciowych.</span><span class="sxs-lookup"><span data-stu-id="c2e54-118">However, it is quite likely that multiple users will sharing a single public IP address due to them accessing the Internet via a NAT device.</span></span> <span data-ttu-id="c2e54-119">Mimo to dla interfejsów API, który umożliwia nieuwierzytelnione dostępu `IpAddress` może być najlepszym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="c2e54-119">Despite this, for APIs that allow unauthenticated access the `IpAddress` might be the best option.</span></span>

## <a name="user-identity-throttling"></a><span data-ttu-id="c2e54-120">Ograniczenie tożsamości użytkownika</span><span class="sxs-lookup"><span data-stu-id="c2e54-120">User identity throttling</span></span>
<span data-ttu-id="c2e54-121">Jeśli użytkownik jest uwierzytelniony, ograniczenie klucza mogą być generowane na podstawie informacji, który unikatowo identyfikuje, który użytkownik.</span><span class="sxs-lookup"><span data-stu-id="c2e54-121">If an end user is authenticated then a throttling key can be generated based on information that uniquely identifies an that user.</span></span>

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

<span data-ttu-id="c2e54-122">W tym przykładzie mamy extract nagłówek autoryzacji, przekonwertuj je na `JWT` obiektu i Użyj podmiotu tokenu do identyfikacji użytkownika i używać go jako szybkość ograniczenie klucza.</span><span class="sxs-lookup"><span data-stu-id="c2e54-122">In this example we extract the Authorization header, convert it to `JWT` object and use the subject of the token to identify the user and use that as the rate limiting key.</span></span> <span data-ttu-id="c2e54-123">Jeśli tożsamości użytkownika jest przechowywany w `JWT` zgodnie z jednego z innych oświadczeń następnie czy można użyć wartości w jego miejscu.</span><span class="sxs-lookup"><span data-stu-id="c2e54-123">If the user identity is stored in the `JWT` as one of the other claims then that value could be used in its place.</span></span>

## <a name="combined-policies"></a><span data-ttu-id="c2e54-124">Łączna zasad</span><span class="sxs-lookup"><span data-stu-id="c2e54-124">Combined policies</span></span>
<span data-ttu-id="c2e54-125">Mimo że nowe zasady ograniczania przepustowości zapewniają większą kontrolę niż istniejące zasady ograniczania przepustowości, występuje nadal łączenie możliwości obu wartości.</span><span class="sxs-lookup"><span data-stu-id="c2e54-125">Although the new throttling policies provide more control than the existing throttling policies, there is still value combining both capabilities.</span></span> <span data-ttu-id="c2e54-126">Ograniczanie przez klucz produktu subskrypcji ([Limit szybkości wywołanie przez subskrypcji](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) i [przydział użycia zestawu subskrypcji](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) to dobry sposób, aby umożliwić monetizing interfejsu API, pobierając oparte na poziomy użycia.</span><span class="sxs-lookup"><span data-stu-id="c2e54-126">Throttling by product subscription key ([Limit call rate by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) is a great way to enable monetizing of an API by charging based on usage levels.</span></span> <span data-ttu-id="c2e54-127">Skuteczniejszą kontrolę o możliwość ograniczania przez użytkownika jest uzupełniające i uniemożliwia pogorszenia jakości związku środowisko innego zachowanie jednego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c2e54-127">The finer grained control of being able to throttle by user is complementary and prevents one user's behavior from degrading the experience of another.</span></span> 

## <a name="client-driven-throttling"></a><span data-ttu-id="c2e54-128">Klient zmiennych ograniczania przepustowości</span><span class="sxs-lookup"><span data-stu-id="c2e54-128">Client driven throttling</span></span>
<span data-ttu-id="c2e54-129">Po klucz ograniczania przepustowości jest definiowana za pomocą [wyrażenie zasad](https://msdn.microsoft.com/library/azure/dn910913.aspx), wówczas jest dostawcy interfejsu API, który jest wybranie jak zakres to ograniczenie.</span><span class="sxs-lookup"><span data-stu-id="c2e54-129">When the throttling key is defined using a [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx), then it is the API provider that is choosing how the throttling is scoped.</span></span> <span data-ttu-id="c2e54-130">Jednak dewelopera mogą chcieć kontrolować sposób ich limit szybkości własnych klientów.</span><span class="sxs-lookup"><span data-stu-id="c2e54-130">However, a developer might want to control how they rate limit their own customers.</span></span> <span data-ttu-id="c2e54-131">To może zostać włączona przez dostawcę interfejsu API dzięki zastosowaniu niestandardowy nagłówek umożliwia dewelopera aplikacji klienckiej do komunikowania się klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="c2e54-131">This could be enabled by the API provider by introducing a custom header to allow the developer's client application to communicate the key to the API.</span></span>

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

<span data-ttu-id="c2e54-132">Dzięki temu aplikacja kliencka dewelopera wybierz, jak chcą, aby utworzyć szybkość ograniczenie klucza.</span><span class="sxs-lookup"><span data-stu-id="c2e54-132">This enables the developer's client application to choose how they want to create the rate limiting key.</span></span> <span data-ttu-id="c2e54-133">Z niewielki ingenuity deweloperowi klienta można utworzyć własne warstwy stawki przydzielając zestawy kluczy dla użytkowników i obracanie użycia klucza.</span><span class="sxs-lookup"><span data-stu-id="c2e54-133">With a little bit of ingenuity a client developer could create their own rate tiers by allocating sets of keys to users and rotating the key usage.</span></span>

## <a name="summary"></a><span data-ttu-id="c2e54-134">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="c2e54-134">Summary</span></span>
<span data-ttu-id="c2e54-135">Zarządzanie interfejsami API Azure zapewnia szybkość i oferty ograniczania do ochrony i Dodaj wartość do usług interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="c2e54-135">Azure API Management provides rate and quote throttling to both protect and add value to your API service.</span></span> <span data-ttu-id="c2e54-136">Nowe zasady ograniczania przepustowości przy użyciu niestandardowych reguł zakresu pozwalają skuteczniejszą kontrolę nad tych zasad, aby umożliwić klientom tworzenie jeszcze bardziej poprawić jakość aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c2e54-136">The new throttling policies with custom scoping rules allow you finer grained control over those policies to enable your customers to build even better applications.</span></span> <span data-ttu-id="c2e54-137">Przykłady w tym artykule przedstawiają sposób używania tych nowych zasad przez współczynnik produkcyjnym ograniczanie klucze z adresów IP klientów, tożsamość użytkownika i wartości klientów wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="c2e54-137">The examples in this article demonstrate the use of these new policies by manufacturing rate limiting keys with client IP addresses, user identity, and client generated values.</span></span> <span data-ttu-id="c2e54-138">Istnieją jednak wiele innych części komunikat, który może zostać użyty, takich jak agent użytkownika, adres URL ścieżki fragmenty, rozmiar wiadomości.</span><span class="sxs-lookup"><span data-stu-id="c2e54-138">However, there are many other parts of the message that could be used such as user agent, URL path fragments, message size.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2e54-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c2e54-139">Next steps</span></span>
<span data-ttu-id="c2e54-140">Daj nam swoją opinię w wątku usługi Disqus dla tego tematu.</span><span class="sxs-lookup"><span data-stu-id="c2e54-140">Please give us your feedback in the Disqus thread for this topic.</span></span> <span data-ttu-id="c2e54-141">Jest bardzo otrzymywać informacje o innych potencjalnych wartości kluczy, które zostały logicznej wybór w swoim scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="c2e54-141">It would be great to hear about other potential key values that have been a logical choice in your scenarios.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="c2e54-142">Obejrzyj film poglądowy dotyczący tych zasad</span><span class="sxs-lookup"><span data-stu-id="c2e54-142">Watch a video overview of these policies</span></span>
<span data-ttu-id="c2e54-143">Aby uzyskać więcej informacji na temat [szybkość limit przez klucz](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) i [limitu przydziału przez klucz](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) zasady omówione w tym artykule, obserwuj poniższego klipu wideo.</span><span class="sxs-lookup"><span data-stu-id="c2e54-143">For more information on the [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies covered in this article, please watch the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

