---
title: aaaUsing Azure CDN z CORS | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse hello Azure sieci dostarczania zawartości (CDN) toowith udostępniania zasobów między źródłami (CORS)."
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
ms.openlocfilehash: 6c743b56c32a2d3aacc9a77094cb87d61b95d2f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-cdn-with-cors"></a><span data-ttu-id="7ade7-103">Przy użyciu usługi Azure CDN z CORS</span><span class="sxs-lookup"><span data-stu-id="7ade7-103">Using Azure CDN with CORS</span></span>
## <a name="what-is-cors"></a><span data-ttu-id="7ade7-104">Co to jest CORS?</span><span class="sxs-lookup"><span data-stu-id="7ade7-104">What is CORS?</span></span>
<span data-ttu-id="7ade7-105">CORS (Cross źródła Resource Sharing) to funkcja HTTP, która umożliwia aplikacja sieci web w jednej domenie tooaccess zasobów w innej domenie.</span><span class="sxs-lookup"><span data-stu-id="7ade7-105">CORS (Cross Origin Resource Sharing) is an HTTP feature that enables a web application running under one domain tooaccess resources in another domain.</span></span> <span data-ttu-id="7ade7-106">W kolejności tooreduce hello możliwości ataków skryptów między witrynami, wszystkie nowoczesne przeglądarki zaimplementować ograniczenia zabezpieczeń znany jako [zasad samego pochodzenia](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span><span class="sxs-lookup"><span data-stu-id="7ade7-106">In order tooreduce hello possibility of cross-site scripting attacks, all modern web browsers implement a security restriction known as [same-origin policy](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span></span>  <span data-ttu-id="7ade7-107">Zapobiega to strony sieci web na podstawie wywoływania interfejsów API w innej domenie.</span><span class="sxs-lookup"><span data-stu-id="7ade7-107">This prevents a web page from calling APIs in a different domain.</span></span>  <span data-ttu-id="7ade7-108">Mechanizm CORS zapewnia bezpieczny sposób tooallow jedno źródło (hello domeny pochodzenia) toocall interfejsów API w innego źródła.</span><span class="sxs-lookup"><span data-stu-id="7ade7-108">CORS provides a secure way tooallow one origin (hello origin domain) toocall APIs in another origin.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="7ade7-109">Jak to działa</span><span class="sxs-lookup"><span data-stu-id="7ade7-109">How it works</span></span>
<span data-ttu-id="7ade7-110">Istnieją dwa typy żądań CORPS *prostych żądań* i *złożonych żądań.*</span><span class="sxs-lookup"><span data-stu-id="7ade7-110">There are two types of CORS requests, *simple requests* and *complex requests.*</span></span>

### <a name="for-simple-requests"></a><span data-ttu-id="7ade7-111">Proste żądań:</span><span class="sxs-lookup"><span data-stu-id="7ade7-111">For simple requests:</span></span>

1. <span data-ttu-id="7ade7-112">Przeglądarka Hello wysyła żądanie CORS hello z dodatkowymi **pochodzenia** nagłówek żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="7ade7-112">hello browser sends hello CORS request with an additional **Origin** HTTP request header.</span></span> <span data-ttu-id="7ade7-113">wartość Hello tego nagłówka jest pochodzenia hello, który obsłużył Strona nadrzędna hello, która jest zdefiniowana jako kombinacja hello *protokołu,* *domeny,* i *portu.*</span><span class="sxs-lookup"><span data-stu-id="7ade7-113">hello value of this header is hello origin that served hello parent page, which is defined as hello combination of *protocol,* *domain,* and *port.*</span></span>  <span data-ttu-id="7ade7-114">Jeśli strony z https://www.contoso.com próbuje tooaccess danych użytkownika w hello fabrikam.com pochodzenia, powitania po nagłówek żądania wysłania toofabrikam.com:</span><span class="sxs-lookup"><span data-stu-id="7ade7-114">When a page from https://www.contoso.com attempts tooaccess a user's data in hello fabrikam.com origin, hello following request header would be sent toofabrikam.com:</span></span>

   `Origin: https://www.contoso.com`

2. <span data-ttu-id="7ade7-115">Serwer Hello mogą odpowiadać za pomocą dowolnego z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="7ade7-115">hello server may respond with any of hello following:</span></span>

   * <span data-ttu-id="7ade7-116">**Access-Control-Allow-Origin** nagłówka w swojej odpowiedzi wskazujący lokacji pochodzenia, do której jest dozwolona.</span><span class="sxs-lookup"><span data-stu-id="7ade7-116">An **Access-Control-Allow-Origin** header in its response indicating which origin site is allowed.</span></span> <span data-ttu-id="7ade7-117">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="7ade7-117">For example:</span></span>

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * <span data-ttu-id="7ade7-118">Błąd HTTP code takich jak 403, jeśli powitania serwera nie zezwala na żądania cross-origin hello po sprawdzeniu hello źródła nagłówka</span><span class="sxs-lookup"><span data-stu-id="7ade7-118">An HTTP error code such as 403 if hello server does not allow hello cross-origin request after checking hello Origin header</span></span>

   * <span data-ttu-id="7ade7-119">**Access-Control-Allow-Origin** nagłówka z symbolem wieloznacznym, który zezwala na wszystkie pochodzenia:</span><span class="sxs-lookup"><span data-stu-id="7ade7-119">An **Access-Control-Allow-Origin** header with a wildcard that allows all origins:</span></span>

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a><span data-ttu-id="7ade7-120">Złożonych żądań:</span><span class="sxs-lookup"><span data-stu-id="7ade7-120">For complex requests:</span></span>

<span data-ttu-id="7ade7-121">Złożonych żądanie jest żądaniem CORS, w których przeglądarka hello jest wymagane toosend *żądania wstępnego* (tj. wstępne badanie) przed wysłaniem hello rzeczywiste żądanie CORS.</span><span class="sxs-lookup"><span data-stu-id="7ade7-121">A complex request is a CORS request where hello browser is required toosend a *preflight request* (i.e. a preliminary probe) before sending hello actual CORS request.</span></span> <span data-ttu-id="7ade7-122">Hello żądania wstępnego żąda uprawnienia serwera hello czy hello oryginalne żądanie CORS można kontynuować i jest `OPTIONS` żądania toohello tego samego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="7ade7-122">hello preflight request asks hello server permission if hello original CORS request can proceed and is an `OPTIONS` request toohello same URL.</span></span>

> [!TIP]
> <span data-ttu-id="7ade7-123">Więcej szczegółów na przepływów mechanizmu CORS i typowych problemów, należy wyświetlić hello [przewodniku tooCORS interfejsów API REST](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span><span class="sxs-lookup"><span data-stu-id="7ade7-123">For more details on CORS flows and common pitfalls, view hello [Guide tooCORS for REST APIs](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span></span>
>
>

## <a name="wildcard-or-single-origin-scenarios"></a><span data-ttu-id="7ade7-124">Symbol wieloznaczny lub scenariuszy pojedynczego źródła</span><span class="sxs-lookup"><span data-stu-id="7ade7-124">Wildcard or single origin scenarios</span></span>
<span data-ttu-id="7ade7-125">CORS w sieci CDN w warstwie Azure będą działać automatycznie bez konieczności dodatkowej konfiguracji, gdy hello **Access-Control-Allow-Origin** ustawiono nagłówka toowildcard (*) lub jednego źródła.</span><span class="sxs-lookup"><span data-stu-id="7ade7-125">CORS on Azure CDN will work automatically with no additional configuration when hello **Access-Control-Allow-Origin** header is set toowildcard (*) or a single origin.</span></span>  <span data-ttu-id="7ade7-126">Hello CDN będą buforowane hello pierwszej odpowiedzi i kolejne żądania użyje hello tego samego nagłówka.</span><span class="sxs-lookup"><span data-stu-id="7ade7-126">hello CDN will cache hello first response and subsequent requests will use hello same header.</span></span>

<span data-ttu-id="7ade7-127">Jeśli żądań zostały już wprowadzone toohello CDN tooCORS wcześniejszego ustawiania hello źródła, konieczne będzie toopurge zawartości na powitania tooreload zawartości z punktu końcowego zawartości z hello **Access-Control-Allow-Origin** nagłówka.</span><span class="sxs-lookup"><span data-stu-id="7ade7-127">If requests have already been made toohello CDN prior tooCORS being set on hello your origin, you will need toopurge content on your endpoint content tooreload hello content with hello **Access-Control-Allow-Origin** header.</span></span>

## <a name="multiple-origin-scenarios"></a><span data-ttu-id="7ade7-128">Wiele scenariuszy źródła</span><span class="sxs-lookup"><span data-stu-id="7ade7-128">Multiple origin scenarios</span></span>
<span data-ttu-id="7ade7-129">Tooallow do określonej listy źródeł toobe dozwolone dla mechanizmu CORS należy rzeczy Pobierz nieco bardziej skomplikowane.</span><span class="sxs-lookup"><span data-stu-id="7ade7-129">If you need tooallow a specific list of origins toobe allowed for CORS, things get a little more complicated.</span></span> <span data-ttu-id="7ade7-130">Witaj problem występuje, gdy hello CDN buforuje hello **Access-Control-Allow-Origin** nagłówek hello pierwsze źródło CORS.</span><span class="sxs-lookup"><span data-stu-id="7ade7-130">hello problem occurs when hello CDN caches hello **Access-Control-Allow-Origin** header for hello first CORS origin.</span></span>  <span data-ttu-id="7ade7-131">Gdy inny źródło CORS sprawia, że kolejne żądania, hello CDN posłuży hello buforowane **Access-Control-Allow-Origin** nagłówek, który nie odpowiada.</span><span class="sxs-lookup"><span data-stu-id="7ade7-131">When a different CORS origin makes a subsequent request, hello CDN will serve hello cached **Access-Control-Allow-Origin** header, which won't match.</span></span>  <span data-ttu-id="7ade7-132">Istnieje kilka sposobów toocorrect to.</span><span class="sxs-lookup"><span data-stu-id="7ade7-132">There are several ways toocorrect this.</span></span>

### <a name="azure-cdn-premium-from-verizon"></a><span data-ttu-id="7ade7-133">Usługa Azure CDN w warstwie Premium firmy Verizon</span><span class="sxs-lookup"><span data-stu-id="7ade7-133">Azure CDN Premium from Verizon</span></span>
<span data-ttu-id="7ade7-134">Najlepszym sposobem tooenable Hello jest toouse **Azure CDN Premium from Verizon**, który ujawnia niektóre zaawansowane funkcje.</span><span class="sxs-lookup"><span data-stu-id="7ade7-134">hello best way tooenable this is toouse **Azure CDN Premium from Verizon**, which exposes some advanced functionality.</span></span> 

<span data-ttu-id="7ade7-135">Będziesz potrzebować zbyt[utworzyć regułę](cdn-rules-engine.md) toocheck hello **pochodzenia** nagłówka w żądaniu hello.</span><span class="sxs-lookup"><span data-stu-id="7ade7-135">You'll need too[create a rule](cdn-rules-engine.md) toocheck hello **Origin** header on hello request.</span></span>  <span data-ttu-id="7ade7-136">Jeśli istnieje prawidłowy punkt początkowy reguły ustawi hello **Access-Control-Allow-Origin** nagłówek z pochodzenia hello podany w żądaniu hello.</span><span class="sxs-lookup"><span data-stu-id="7ade7-136">If it's a valid origin, your rule will set hello **Access-Control-Allow-Origin** header with hello origin provided in hello request.</span></span>  <span data-ttu-id="7ade7-137">Jeśli określono pochodzenia hello hello **pochodzenia** nagłówka nie jest dozwolona, reguła musi pominąć hello **Access-Control-Allow-Origin** nagłówka, co spowoduje hello przeglądarki tooreject hello żądania.</span><span class="sxs-lookup"><span data-stu-id="7ade7-137">If hello origin specified in hello **Origin** header is not allowed, your rule should omit hello **Access-Control-Allow-Origin** header which will cause hello browser tooreject hello request.</span></span> 

<span data-ttu-id="7ade7-138">Istnieją dwa sposoby toodo to hello aparatu reguł.</span><span class="sxs-lookup"><span data-stu-id="7ade7-138">There are two ways toodo this with hello rules engine.</span></span>  <span data-ttu-id="7ade7-139">W obu przypadkach hello **Access-Control-Allow-Origin** nagłówka z serwera pochodzenia pliku hello całkowicie jest ignorowany, aparat reguł hello CDN w pełni zarządza hello dozwolone źródła CORS.</span><span class="sxs-lookup"><span data-stu-id="7ade7-139">In both cases, hello **Access-Control-Allow-Origin** header from hello file's origin server is completely ignored, hello CDN's rules engine completely manages hello allowed CORS origins.</span></span>

#### <a name="one-regular-expression-with-all-valid-origins"></a><span data-ttu-id="7ade7-140">Jednego wyrażenia regularnego z wszystkie prawidłowe źródła</span><span class="sxs-lookup"><span data-stu-id="7ade7-140">One regular expression with all valid origins</span></span>
<span data-ttu-id="7ade7-141">W takim przypadku utworzysz wyrażenie regularne, które zawiera wszystkie źródła hello ma tooallow:</span><span class="sxs-lookup"><span data-stu-id="7ade7-141">In this case, you'll create a regular expression that includes all of hello origins you want tooallow:</span></span> 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> <span data-ttu-id="7ade7-142">**Usługi Azure CDN from Verizon** używa [zgodne wyrażeń regularnych języka Perl](http://pcre.org/) jako jego aparat wyrażeń regularnych.</span><span class="sxs-lookup"><span data-stu-id="7ade7-142">**Azure CDN from Verizon** uses [Perl Compatible Regular Expressions](http://pcre.org/) as its engine for regular expressions.</span></span>  <span data-ttu-id="7ade7-143">Można użyć narzędzia, takiego jak [101 wyrażeń regularnych](https://regex101.com/) toovalidate wyrażenie regularnego.</span><span class="sxs-lookup"><span data-stu-id="7ade7-143">You can use a tool like [Regular Expressions 101](https://regex101.com/) toovalidate your regular expression.</span></span>  <span data-ttu-id="7ade7-144">Należy pamiętać, że Witaj "/" znak jest nieprawidłowe w wyrażeniach regularnych i nie wymaga toobe wyjściowym, jednak anulowanie ten znak jest traktowane jako najlepsze rozwiązanie i jest oczekiwane przez niektóre moduły weryfikacji wyrażenia regularnego.</span><span class="sxs-lookup"><span data-stu-id="7ade7-144">Note that hello "/" character is valid in regular expressions and doesn't need toobe escaped, however, escaping that character is considered a best practice and is expected by some regex validators.</span></span>
> 
> 

<span data-ttu-id="7ade7-145">Jeśli pasuje do wyrażenia regularnego hello, reguły zastąpi hello **Access-Control-Allow-Origin** nagłówka (jeśli istnieją) z hello źródła z pochodzenia hello, który wysłał żądanie hello.</span><span class="sxs-lookup"><span data-stu-id="7ade7-145">If hello regular expression matches, your rule will replace hello **Access-Control-Allow-Origin** header (if any) from hello origin with hello origin that sent hello request.</span></span>  <span data-ttu-id="7ade7-146">Możesz także dodać dodatkowe nagłówki CORS, takich jak **dostępu-formant-Allow-Methods**.</span><span class="sxs-lookup"><span data-stu-id="7ade7-146">You can also add additional CORS headers, such as **Access-Control-Allow-Methods**.</span></span>

![Przykład reguły z wyrażeniem regularnym](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a><span data-ttu-id="7ade7-148">Reguła nagłówka żądania dla każdego źródła.</span><span class="sxs-lookup"><span data-stu-id="7ade7-148">Request header rule for each origin.</span></span>
<span data-ttu-id="7ade7-149">Zamiast wyrażeń regularnych, możesz zamiast tego utworzyć oddzielne reguły dla każdego źródła mają tooallow przy użyciu hello **wieloznaczny nagłówka żądania** [dopasować stan](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="7ade7-149">Rather than regular expressions, you can instead create a separate rule for each origin you wish tooallow using hello **Request Header Wildcard** [match condition](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span></span> <span data-ttu-id="7ade7-150">Jako przy użyciu metody wyrażenia regularnego hello reguły hello aparat samodzielnie ustawia nagłówki CORS hello.</span><span class="sxs-lookup"><span data-stu-id="7ade7-150">As with hello regular expression method, hello rules engine alone sets hello CORS headers.</span></span> 

![Przykład reguły bez wyrażeń regularnych](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> <span data-ttu-id="7ade7-152">W powyższym przykładzie hello, hello Użyj hello wieloznaczny * informuje reguły hello aparat toomatch protokołów HTTP i HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7ade7-152">In hello example above, hello use of hello wildcard character * tells hello rules engine toomatch both HTTP and HTTPS.</span></span>
> 
> 

### <a name="azure-cdn-standard"></a><span data-ttu-id="7ade7-153">Usługi Azure CDN Standard</span><span class="sxs-lookup"><span data-stu-id="7ade7-153">Azure CDN Standard</span></span>
<span data-ttu-id="7ade7-154">Na platformie Azure CDN Standard profile hello tylko tooallow mechanizm dla wielu źródeł bez użycia hello pochodzenia symbolu wieloznacznego hello jest toouse [buforowanie ciągu zapytania](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="7ade7-154">On Azure CDN Standard profiles, hello only mechanism tooallow for multiple origins without hello use of hello wildcard origin is toouse [query string caching](cdn-query-string.md).</span></span>  <span data-ttu-id="7ade7-155">Ustawienie parametrów zapytania tooenable dla punktu końcowego CDN hello a następnie za pomocą ciąg zapytania unikatowy dla żądań z każdej domeny, dozwolone.</span><span class="sxs-lookup"><span data-stu-id="7ade7-155">You need tooenable query string setting for hello CDN endpoint and then use a unique query string for requests from each allowed domain.</span></span> <span data-ttu-id="7ade7-156">W ten sposób spowoduje hello CDN buforowanie oddzielny obiekt dla każdego ciągu zapytania unikatowy.</span><span class="sxs-lookup"><span data-stu-id="7ade7-156">Doing this will result in hello CDN caching a separate object for each unique query string.</span></span> <span data-ttu-id="7ade7-157">Ta metoda nie jest idealnym rozwiązaniem, jednak zgodnie z spowoduje utworzenie wielu kopii hello tego samego pliku pamięci podręcznej na powitania CDN.</span><span class="sxs-lookup"><span data-stu-id="7ade7-157">This approach is not ideal, however, as it will result in multiple copies of hello same file cached on hello CDN.</span></span>  

