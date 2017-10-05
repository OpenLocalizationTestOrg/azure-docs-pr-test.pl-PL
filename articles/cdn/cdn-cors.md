---
title: "Przy użyciu usługi Azure CDN z CORS | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać usługi Azure sieci dostarczania zawartości (CDN) do z udostępniania zasobów między źródłami (CORS)."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 86740a96-4269-4060-aba3-a69f00e6f14e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 7070397f6e69b21add75bad8220f0b8ebe36d266
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-cdn-with-cors"></a><span data-ttu-id="1e7ae-103">Przy użyciu usługi Azure CDN z CORS</span><span class="sxs-lookup"><span data-stu-id="1e7ae-103">Using Azure CDN with CORS</span></span>
## <a name="what-is-cors"></a><span data-ttu-id="1e7ae-104">Co to jest CORS?</span><span class="sxs-lookup"><span data-stu-id="1e7ae-104">What is CORS?</span></span>
<span data-ttu-id="1e7ae-105">CORS (Cross źródła Resource Sharing) to funkcja HTTP, która umożliwia aplikacja sieci web w jednej domenie dostęp do zasobów w innej domenie.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-105">CORS (Cross Origin Resource Sharing) is an HTTP feature that enables a web application running under one domain to access resources in another domain.</span></span> <span data-ttu-id="1e7ae-106">Aby zmniejszyć ryzyko ataków skryptów między witrynami, wszystkie nowoczesne przeglądarki zaimplementować ograniczenia zabezpieczeń znany jako [zasad samego pochodzenia](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span><span class="sxs-lookup"><span data-stu-id="1e7ae-106">In order to reduce the possibility of cross-site scripting attacks, all modern web browsers implement a security restriction known as [same-origin policy](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span></span>  <span data-ttu-id="1e7ae-107">Zapobiega to strony sieci web na podstawie wywoływania interfejsów API w innej domenie.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-107">This prevents a web page from calling APIs in a different domain.</span></span>  <span data-ttu-id="1e7ae-108">Mechanizm CORS zapewnia bezpieczny sposób umożliwić jedno źródło (domeny pochodzenia) do wywoływania interfejsów API w inny początek.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-108">CORS provides a secure way to allow one origin (the origin domain) to call APIs in another origin.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="1e7ae-109">Jak to działa</span><span class="sxs-lookup"><span data-stu-id="1e7ae-109">How it works</span></span>
<span data-ttu-id="1e7ae-110">Istnieją dwa typy żądań CORPS *prostych żądań* i *złożonych żądań.*</span><span class="sxs-lookup"><span data-stu-id="1e7ae-110">There are two types of CORS requests, *simple requests* and *complex requests.*</span></span>

### <a name="for-simple-requests"></a><span data-ttu-id="1e7ae-111">Proste żądań:</span><span class="sxs-lookup"><span data-stu-id="1e7ae-111">For simple requests:</span></span>

1. <span data-ttu-id="1e7ae-112">Przeglądarka wysyła żądanie CORS z dodatkowymi **pochodzenia** nagłówek żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-112">The browser sends the CORS request with an additional **Origin** HTTP request header.</span></span> <span data-ttu-id="1e7ae-113">Wartość tego nagłówka jest punkt początkowy, który obsłużył Strona nadrzędna, który jest zdefiniowany jako kombinacja *protokołu,* *domeny,* i *portu.*</span><span class="sxs-lookup"><span data-stu-id="1e7ae-113">The value of this header is the origin that served the parent page, which is defined as the combination of *protocol,* *domain,* and *port.*</span></span>  <span data-ttu-id="1e7ae-114">Jeśli strony z https://www.contoso.com próbuje uzyskać dostęp do danych użytkownika ze źródłem fabrikam.com, następujący nagłówek żądania wysłania do fabrikam.com:</span><span class="sxs-lookup"><span data-stu-id="1e7ae-114">When a page from https://www.contoso.com attempts to access a user's data in the fabrikam.com origin, the following request header would be sent to fabrikam.com:</span></span>

   `Origin: https://www.contoso.com`

2. <span data-ttu-id="1e7ae-115">Serwer może odpowiadać za pomocą dowolnego z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="1e7ae-115">The server may respond with any of the following:</span></span>

   * <span data-ttu-id="1e7ae-116">**Access-Control-Allow-Origin** nagłówka w swojej odpowiedzi wskazujący lokacji pochodzenia, do której jest dozwolona.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-116">An **Access-Control-Allow-Origin** header in its response indicating which origin site is allowed.</span></span> <span data-ttu-id="1e7ae-117">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="1e7ae-117">For example:</span></span>

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * <span data-ttu-id="1e7ae-118">Kod błędu HTTP, takie jak 403, jeśli serwer nie zezwala na żądania cross-origin po sprawdzeniu nagłówka źródła</span><span class="sxs-lookup"><span data-stu-id="1e7ae-118">An HTTP error code such as 403 if the server does not allow the cross-origin request after checking the Origin header</span></span>

   * <span data-ttu-id="1e7ae-119">**Access-Control-Allow-Origin** nagłówka z symbolem wieloznacznym, który zezwala na wszystkie pochodzenia:</span><span class="sxs-lookup"><span data-stu-id="1e7ae-119">An **Access-Control-Allow-Origin** header with a wildcard that allows all origins:</span></span>

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a><span data-ttu-id="1e7ae-120">Złożonych żądań:</span><span class="sxs-lookup"><span data-stu-id="1e7ae-120">For complex requests:</span></span>

<span data-ttu-id="1e7ae-121">Złożone żądanie jest żądaniem CORS, w którym przeglądarki jest wymagany do wysłania *żądania wstępnego* (tj. wstępne badanie) przed wysłaniem rzeczywiste żądanie CORS.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-121">A complex request is a CORS request where the browser is required to send a *preflight request* (i.e. a preliminary probe) before sending the actual CORS request.</span></span> <span data-ttu-id="1e7ae-122">Żądania wstępnego żąda uprawnienia serwera, jeśli oryginalny CORS żądanie może kontynuować i jest `OPTIONS` żądania do tego samego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-122">The preflight request asks the server permission if the original CORS request can proceed and is an `OPTIONS` request to the same URL.</span></span>

> [!TIP]
> <span data-ttu-id="1e7ae-123">Więcej informacji dotyczących przepływów mechanizmu CORS i typowych problemów, można wyświetlić [przewodnik CORS dla interfejsów API REST](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span><span class="sxs-lookup"><span data-stu-id="1e7ae-123">For more details on CORS flows and common pitfalls, view the [Guide to CORS for REST APIs](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span></span>
>
>

## <a name="wildcard-or-single-origin-scenarios"></a><span data-ttu-id="1e7ae-124">Symbol wieloznaczny lub scenariuszy pojedynczego źródła</span><span class="sxs-lookup"><span data-stu-id="1e7ae-124">Wildcard or single origin scenarios</span></span>
<span data-ttu-id="1e7ae-125">Mechanizm CORS w sieci CDN w warstwie Azure będą działać automatycznie bez konieczności dodatkowej konfiguracji po **Access-Control-Allow-Origin** nagłówka jest ustawiony na symbolu wieloznacznego (*) lub jednego źródła.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-125">CORS on Azure CDN will work automatically with no additional configuration when the **Access-Control-Allow-Origin** header is set to wildcard (*) or a single origin.</span></span>  <span data-ttu-id="1e7ae-126">CDN będą buforowane pierwszej odpowiedzi i kolejne żądania będą używały tego samego nagłówka.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-126">The CDN will cache the first response and subsequent requests will use the same header.</span></span>

<span data-ttu-id="1e7ae-127">Jeśli żądań zostały już wprowadzone do sieci CDN przed CORS ustawiania źródła, konieczne będzie przeczyścić zawartości na zawartość ponownie załaduj zawartość z punktu końcowego **Access-Control-Allow-Origin** nagłówka.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-127">If requests have already been made to the CDN prior to CORS being set on the your origin, you will need to purge content on your endpoint content to reload the content with the **Access-Control-Allow-Origin** header.</span></span>

## <a name="multiple-origin-scenarios"></a><span data-ttu-id="1e7ae-128">Wiele scenariuszy źródła</span><span class="sxs-lookup"><span data-stu-id="1e7ae-128">Multiple origin scenarios</span></span>
<span data-ttu-id="1e7ae-129">Jeśli musisz zezwolić określonej listy źródeł, które mogą być dla CORS, rzeczy uzyskać nieco bardziej skomplikowane.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-129">If you need to allow a specific list of origins to be allowed for CORS, things get a little more complicated.</span></span> <span data-ttu-id="1e7ae-130">Problem występuje, gdy sieć CDN ma buforować **Access-Control-Allow-Origin** nagłówek dla pierwszego źródło CORS.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-130">The problem occurs when the CDN caches the **Access-Control-Allow-Origin** header for the first CORS origin.</span></span>  <span data-ttu-id="1e7ae-131">Gdy różne źródło CORS sprawia, że kolejne żądania, sieć CDN będzie służyć zapisane w pamięci podręcznej **Access-Control-Allow-Origin** nagłówek, który nie odpowiada.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-131">When a different CORS origin makes a subsequent request, the CDN will serve the cached **Access-Control-Allow-Origin** header, which won't match.</span></span>  <span data-ttu-id="1e7ae-132">Istnieje kilka sposobów, aby rozwiązać ten problem.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-132">There are several ways to correct this.</span></span>

### <a name="azure-cdn-premium-from-verizon"></a><span data-ttu-id="1e7ae-133">Usługa Azure CDN w warstwie Premium firmy Verizon</span><span class="sxs-lookup"><span data-stu-id="1e7ae-133">Azure CDN Premium from Verizon</span></span>
<span data-ttu-id="1e7ae-134">Najlepszym sposobem, aby je włączyć, jest użycie **Azure CDN Premium from Verizon**, który ujawnia niektóre zaawansowane funkcje.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-134">The best way to enable this is to use **Azure CDN Premium from Verizon**, which exposes some advanced functionality.</span></span> 

<span data-ttu-id="1e7ae-135">Konieczne będzie [utworzyć regułę](cdn-rules-engine.md) do sprawdzenia **pochodzenia** nagłówka w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-135">You'll need to [create a rule](cdn-rules-engine.md) to check the **Origin** header on the request.</span></span>  <span data-ttu-id="1e7ae-136">Jeśli istnieje prawidłowy punkt początkowy reguły ustawi **Access-Control-Allow-Origin** nagłówek z pochodzenia podany w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-136">If it's a valid origin, your rule will set the **Access-Control-Allow-Origin** header with the origin provided in the request.</span></span>  <span data-ttu-id="1e7ae-137">Jeśli punkt początkowy określony w **pochodzenia** nagłówka nie jest dozwolona, należy pominąć reguły **Access-Control-Allow-Origin** nagłówka, co spowoduje przeglądarkę, aby odrzucić żądanie.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-137">If the origin specified in the **Origin** header is not allowed, your rule should omit the **Access-Control-Allow-Origin** header which will cause the browser to reject the request.</span></span> 

<span data-ttu-id="1e7ae-138">Istnieją dwa sposoby, w tym celu z aparatu reguł.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-138">There are two ways to do this with the rules engine.</span></span>  <span data-ttu-id="1e7ae-139">W obu przypadkach **Access-Control-Allow-Origin** nagłówka z serwera pochodzenia pliku całkowicie jest ignorowany, aparat reguł w sieci CDN w pełni zarządza dozwolonych źródeł CORS.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-139">In both cases, the **Access-Control-Allow-Origin** header from the file's origin server is completely ignored, the CDN's rules engine completely manages the allowed CORS origins.</span></span>

#### <a name="one-regular-expression-with-all-valid-origins"></a><span data-ttu-id="1e7ae-140">Jednego wyrażenia regularnego z wszystkie prawidłowe źródła</span><span class="sxs-lookup"><span data-stu-id="1e7ae-140">One regular expression with all valid origins</span></span>
<span data-ttu-id="1e7ae-141">W takim przypadku utworzysz wyrażenie regularne, które zawiera wszystkie źródła, które chcesz zezwolić na:</span><span class="sxs-lookup"><span data-stu-id="1e7ae-141">In this case, you'll create a regular expression that includes all of the origins you want to allow:</span></span> 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> <span data-ttu-id="1e7ae-142">**Usługi Azure CDN from Verizon** używa [zgodne wyrażeń regularnych języka Perl](http://pcre.org/) jako jego aparat wyrażeń regularnych.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-142">**Azure CDN from Verizon** uses [Perl Compatible Regular Expressions](http://pcre.org/) as its engine for regular expressions.</span></span>  <span data-ttu-id="1e7ae-143">Można użyć narzędzia, takiego jak [101 wyrażeń regularnych](https://regex101.com/) do sprawdzania poprawności z wyrażeniem regularnym.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-143">You can use a tool like [Regular Expressions 101](https://regex101.com/) to validate your regular expression.</span></span>  <span data-ttu-id="1e7ae-144">Należy pamiętać, że znak "/" jest nieprawidłowe w wyrażeniach regularnych i nie należy wstawić jednak anulowanie ten znak jest traktowane jako najlepsze rozwiązanie i jest oczekiwane przez niektóre moduły weryfikacji wyrażenia regularnego.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-144">Note that the "/" character is valid in regular expressions and doesn't need to be escaped, however, escaping that character is considered a best practice and is expected by some regex validators.</span></span>
> 
> 

<span data-ttu-id="1e7ae-145">Jeśli pasuje do wyrażenia regularnego, zastąpi reguły **Access-Control-Allow-Origin** nagłówek (jeśli istnieje), od źródła z pochodzenia, który wysłał żądanie.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-145">If the regular expression matches, your rule will replace the **Access-Control-Allow-Origin** header (if any) from the origin with the origin that sent the request.</span></span>  <span data-ttu-id="1e7ae-146">Możesz także dodać dodatkowe nagłówki CORS, takich jak **dostępu-formant-Allow-Methods**.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-146">You can also add additional CORS headers, such as **Access-Control-Allow-Methods**.</span></span>

![Przykład reguły z wyrażeniem regularnym](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a><span data-ttu-id="1e7ae-148">Reguła nagłówka żądania dla każdego źródła.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-148">Request header rule for each origin.</span></span>
<span data-ttu-id="1e7ae-149">Zamiast wyrażeń regularnych, zamiast tego można utworzyć regułę osobne dla każdego źródła mają być dozwolone, za pomocą **wieloznaczny nagłówka żądania** [dopasować stan](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="1e7ae-149">Rather than regular expressions, you can instead create a separate rule for each origin you wish to allow using the **Request Header Wildcard** [match condition](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span></span> <span data-ttu-id="1e7ae-150">Podobnie jak w przypadku metody wyrażenia regularnego samego silnika reguły ustawia nagłówki CORS.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-150">As with the regular expression method, the rules engine alone sets the CORS headers.</span></span> 

![Przykład reguły bez wyrażeń regularnych](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> <span data-ttu-id="1e7ae-152">W przykładzie powyżej stosowania symbol wieloznaczny * informuje aparatu reguł do dopasowania protokołów HTTP i HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-152">In the example above, the use of the wildcard character * tells the rules engine to match both HTTP and HTTPS.</span></span>
> 
> 

### <a name="azure-cdn-standard"></a><span data-ttu-id="1e7ae-153">Usługi Azure CDN Standard</span><span class="sxs-lookup"><span data-stu-id="1e7ae-153">Azure CDN Standard</span></span>
<span data-ttu-id="1e7ae-154">Na profile Azure CDN Standard, jest użycie mechanizmu tylko do obsługi wielu źródeł bez użycia początkowego symbolu wieloznacznego [buforowanie ciągu zapytania](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="1e7ae-154">On Azure CDN Standard profiles, the only mechanism to allow for multiple origins without the use of the wildcard origin is to use [query string caching](cdn-query-string.md).</span></span>  <span data-ttu-id="1e7ae-155">Należy włączyć ustawienie ciągu zapytania dla punktu końcowego CDN, a następnie użyć ciągu zapytania unikatowy dla żądań z każdej domeny, dozwolone.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-155">You need to enable query string setting for the CDN endpoint and then use a unique query string for requests from each allowed domain.</span></span> <span data-ttu-id="1e7ae-156">W ten sposób spowoduje CDN buforowanie oddzielny obiekt dla każdego ciągu zapytania unikatowy.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-156">Doing this will result in the CDN caching a separate object for each unique query string.</span></span> <span data-ttu-id="1e7ae-157">Ta metoda nie jest idealne, jednak zgodnie z spowoduje powstanie wielu kopii tego samego pliku pamięci podręcznej w sieci CDN.</span><span class="sxs-lookup"><span data-stu-id="1e7ae-157">This approach is not ideal, however, as it will result in multiple copies of the same file cached on the CDN.</span></span>  

