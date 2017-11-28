---
title: "aaaAzure zaawansowane zasady zarządzania interfejsu API | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat hello zaawansowane zasady dostępne do użycia w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 8a13348b-7856-428f-8e35-9e4273d94323
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 8245e7a4c9d432b7b4d362192e357829fcabad55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-advanced-policies"></a><span data-ttu-id="1227b-103">Zarządzanie interfejsami API zaawansowane zasady</span><span class="sxs-lookup"><span data-stu-id="1227b-103">API Management advanced policies</span></span>
<span data-ttu-id="1227b-104">W tym temacie znajdują się informacje na następujące zasady usługi API Management hello.</span><span class="sxs-lookup"><span data-stu-id="1227b-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="1227b-105">Aby uzyskać informacje dotyczące dodawania i konfigurowania zasad, zobacz [zasad w usłudze API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="1227b-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="1227b-106"><a name="AdvancedPolicies"></a>Zaawansowane zasady</span><span class="sxs-lookup"><span data-stu-id="1227b-106"><a name="AdvancedPolicies"></a> Advanced policies</span></span>  
  
-   <span data-ttu-id="1227b-107">[Przepływ kontroli](api-management-advanced-policies.md#choose) — warunkowo stosuje deklaracji zasad, na podstawie wyników hello oceny hello Boolean [wyrażenia](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="1227b-107">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on hello results of hello evaluation of Boolean [expressions](api-management-policy-expressions.md).</span></span>  
  
-   <span data-ttu-id="1227b-108">[Przekazanie żądania](#ForwardRequest) -przekazuje hello żądania toohello wewnętrznej bazy danych usługi.</span><span class="sxs-lookup"><span data-stu-id="1227b-108">[Forward request](#ForwardRequest) - Forwards hello request toohello backend service.</span></span>

-   <span data-ttu-id="1227b-109">[Ogranicz współbieżności](#LimitConcurrency) — uniemożliwia ujęta zasady wykonania przez więcej niż hello określonej liczby żądań w czasie.</span><span class="sxs-lookup"><span data-stu-id="1227b-109">[Limit concurrency](#LimitConcurrency) - Prevents enclosed policies from executing by more than hello specified number of requests at a time.</span></span>
  
-   <span data-ttu-id="1227b-110">[Zaloguj się tooEvent Centrum](#log-to-eventhub) — wysyła wiadomości powitania określony format tooan Centrum zdarzeń zdefiniowanych przez podmiot rejestratora.</span><span class="sxs-lookup"><span data-stu-id="1227b-110">[Log tooEvent Hub](#log-to-eventhub) - Sends messages in hello specified format tooan Event Hub defined by a Logger entity.</span></span> 

-   <span data-ttu-id="1227b-111">[Mock odpowiedzi](#mock-response) -przerwań potoku wykonywania i zwraca odpowiedź mocked bezpośrednio toohello wywołującego.</span><span class="sxs-lookup"><span data-stu-id="1227b-111">[Mock response](#mock-response) - Aborts pipeline execution and returns a mocked response directly toohello caller.</span></span>
  
-   <span data-ttu-id="1227b-112">[Spróbuj ponownie](#Retry) -ponownych prób wykonania hello ujęta deklaracji zasad, jeśli i dopóki nie zostanie spełniony warunek hello.</span><span class="sxs-lookup"><span data-stu-id="1227b-112">[Retry](#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="1227b-113">Wykonanie jest powtarzany w hello w określonych odstępach czasu i zapasowej toohello określona liczba ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="1227b-113">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>  
  
-   <span data-ttu-id="1227b-114">[Odpowiedź zwrócona](#ReturnResponse) -przerwań potoku wykonywania i zwraca hello określona odpowiedź bezpośrednio toohello wywołującego.</span><span class="sxs-lookup"><span data-stu-id="1227b-114">[Return response](#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span> 
  
-   <span data-ttu-id="1227b-115">[Wyślij żądanie jednokierunkowej](#SendOneWayRequest) — wysyła toohello żądania określony adres URL bez oczekiwania na odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="1227b-115">[Send one way request](#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>  
  
-   <span data-ttu-id="1227b-116">[Wyślij żądanie](#SendRequest) — wysyła toohello żądania określonego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="1227b-116">[Send request](#SendRequest) - Sends a request toohello specified URL.</span></span>  

-   <span data-ttu-id="1227b-117">[Ustaw serwer proxy HTTP](#SetHttpProxy) — pozwala żądań tooroute przekazywane za pośrednictwem serwera proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="1227b-117">[Set HTTP proxy](#SetHttpProxy) - Allows you tooroute forwarded requests via an HTTP proxy.</span></span>  

-   <span data-ttu-id="1227b-118">[Ustawia metodę żądania](#SetRequestMethod) — pozwala toochange metody hello HTTP dla żądania.</span><span class="sxs-lookup"><span data-stu-id="1227b-118">[Set request method](#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>  
  
-   <span data-ttu-id="1227b-119">[Ustaw kod stanu](#SetStatus) -toohello kod stanu hello HTTP zmiany określona wartość.</span><span class="sxs-lookup"><span data-stu-id="1227b-119">[Set status code](#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>  
  
-   <span data-ttu-id="1227b-120">[Ustaw zmienną](api-management-advanced-policies.md#set-variable) -będzie się powtarzał wartości w nazwanym [kontekstu](api-management-policy-expressions.md#ContextVariables) zmiennej nowsze dostępu.</span><span class="sxs-lookup"><span data-stu-id="1227b-120">[Set variable](api-management-advanced-policies.md#set-variable) - Persists a value in a named [context](api-management-policy-expressions.md#ContextVariables) variable for later access.</span></span>  

-   <span data-ttu-id="1227b-121">[Śledzenia](#Trace) -dodaje ciąg do hello [inspektora interfejsu API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="1227b-121">[Trace](#Trace) - Adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
-   <span data-ttu-id="1227b-122">[Poczekaj](#Wait) -oczekuje dla ujęta [żądanie wysłania](api-management-advanced-policies.md#SendRequest), [pobrać wartości z pamięci podręcznej](api-management-caching-policies.md#GetFromCacheByKey), lub [sterowania przepływem](api-management-advanced-policies.md#choose) toocomplete zasad przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="1227b-122">[Wait](#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies toocomplete before proceeding.</span></span>  
  
##  <span data-ttu-id="1227b-123"><a name="choose"></a>Przepływ sterowania</span><span class="sxs-lookup"><span data-stu-id="1227b-123"><a name="choose"></a> Control flow</span></span>  
 <span data-ttu-id="1227b-124">Witaj `choose` zasad stosuje objętego zasady oparte na powitania wynik oceny wyrażeń logicznych, podobne tooan if to inaczej lub przełącznika instrukcje tworzenia w języku programowania.</span><span class="sxs-lookup"><span data-stu-id="1227b-124">hello `choose` policy applies enclosed policy statements based on hello outcome of evaluation of Boolean expressions, similar tooan if-then-else or a switch construct in a programming language.</span></span>  
  
###  <span data-ttu-id="1227b-125"><a name="ChoosePolicyStatement"></a>Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="1227b-125"><a name="ChoosePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<choose>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <otherwise>   
        <!— one or more policy statements toobe applied if none of hello above conditions are true  -->  
</otherwise>   
</choose>  
```  
  
 <span data-ttu-id="1227b-126">Witaj zasady kontroli przepływu musi zawierać co najmniej jeden `<when/>` elementu.</span><span class="sxs-lookup"><span data-stu-id="1227b-126">hello control flow policy must contain at least one `<when/>` element.</span></span> <span data-ttu-id="1227b-127">Witaj `<otherwise/>` element jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="1227b-127">hello `<otherwise/>` element is optional.</span></span> <span data-ttu-id="1227b-128">Warunki w `<when/>` elementy są oceniane w kolejności ich wyglądu w ramach zasad hello.</span><span class="sxs-lookup"><span data-stu-id="1227b-128">Conditions in `<when/>` elements are evaluated in order of their appearance within hello policy.</span></span> <span data-ttu-id="1227b-129">Instrukcji zasad ujętą w nawiasy klamrowe hello najpierw `<when/>` element z równą atrybut warunku `true` zostaną zastosowane.</span><span class="sxs-lookup"><span data-stu-id="1227b-129">Policy statement(s) enclosed within hello first `<when/>` element with condition attribute equals `true` will be applied.</span></span> <span data-ttu-id="1227b-130">Zasady ujętą w nawiasy klamrowe hello `<otherwise/>` elementu, jeśli jest obecny, zostaną zastosowane, jeśli wszystkie z hello `<when/>` są atrybuty warunku elementu `false`.</span><span class="sxs-lookup"><span data-stu-id="1227b-130">Policies enclosed within hello `<otherwise/>` element, if present, will be applied if all of hello `<when/>` element condition attributes are `false`.</span></span>  
  
### <a name="examples"></a><span data-ttu-id="1227b-131">Przykłady</span><span class="sxs-lookup"><span data-stu-id="1227b-131">Examples</span></span>  
  
####  <span data-ttu-id="1227b-132"><a name="ChooseExample"></a>Przykład</span><span class="sxs-lookup"><span data-stu-id="1227b-132"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="1227b-133">Witaj poniższym przykładzie pokazano [set-variable](api-management-advanced-policies.md#set-variable) zasad i dwie zasady przepływu sterowania.</span><span class="sxs-lookup"><span data-stu-id="1227b-133">hello following example demonstrates a [set-variable](api-management-advanced-policies.md#set-variable) policy and two control flow policies.</span></span>  
  
 <span data-ttu-id="1227b-134">Hello Ustaw zasady zmiennej jest hello sekcji ruchu przychodzącego i tworzy `isMobile` logiczna [kontekstu](api-management-policy-expressions.md#ContextVariables) zmiennej, która ma wartość tootrue, jeśli hello `User-Agent` żądania nagłówek zawiera tekst hello `iPad` lub `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="1227b-134">hello set variable policy is in hello inbound section and creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set tootrue if hello `User-Agent` request header contains hello text `iPad` or `iPhone`.</span></span>  
  
 <span data-ttu-id="1227b-135">Hello pierwszy kontroli przepływu zasad jest również w hello sekcji ruchu przychodzącego i warunkowo stosuje się jeden z dwóch [ustawić parametr ciągu zapytania](api-management-transformation-policies.md#SetQueryStringParameter) zasad w zależności od wartości hello hello `isMobile` zmiennej kontekstu.</span><span class="sxs-lookup"><span data-stu-id="1227b-135">hello first control flow policy is also in hello inbound section, and conditionally applies one of two [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policies depending on hello value of hello `isMobile` context variable.</span></span>  
  
 <span data-ttu-id="1227b-136">drugie zasady przepływu sterowania Hello znajduje się w sekcji wychodzącego hello i warunkowo stosuje hello [tooJSON przekonwertować XML](api-management-transformation-policies.md#ConvertXMLtoJSON) zasad podczas `isMobile` ustawiono zbyt`true`.</span><span class="sxs-lookup"><span data-stu-id="1227b-136">hello second control flow policy is in hello outbound section and conditionally applies hello [Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) policy when `isMobile` is set too`true`.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <set-variable name="isMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
        <base />  
        <choose>  
            <when condition="@(context.Variables.GetValueOrDefault<bool>("isMobile"))">  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>true</value>  
                </set-query-parameter>  
            </when>  
            <otherwise>  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>false</value>  
                </set-query-parameter>  
            </otherwise>  
        </choose>  
    </inbound>  
    <outbound>  
        <base />  
        <choose>  
            <when condition="@(context.GetValueOrDefault<bool>("isMobile"))">  
                <xml-to-json kind="direct" apply="always" consider-accept-header="false"/>  
            </when>  
        </choose>  
    </outbound>  
</policies>  
```  
  
#### <a name="example"></a><span data-ttu-id="1227b-137">Przykład</span><span class="sxs-lookup"><span data-stu-id="1227b-137">Example</span></span>  
 <span data-ttu-id="1227b-138">W tym przykładzie pokazano, jak tooperform filtrowanie zawartości przez usunięcie elementów danych z hello odpowiedzi otrzymanych od hello usługi wewnętrznej bazy danych przy użyciu hello `Starter` produktu.</span><span class="sxs-lookup"><span data-stu-id="1227b-138">This example shows how tooperform content filtering by removing data elements from hello response received from hello backend service when using hello `Starter` product.</span></span> <span data-ttu-id="1227b-139">Aby demonstracyjne konfigurowania i korzystania z tych zasad, zobacz [177 epizodu obejmują chmury: więcej funkcji zarządzania interfejsu API z Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybko przewinąć do przodu too34:30.</span><span class="sxs-lookup"><span data-stu-id="1227b-139">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too34:30.</span></span> <span data-ttu-id="1227b-140">Rozpocznij od 31:50 toosee omówienie [hello ciemny niebo prognozy API](https://developer.forecast.io/) używane na potrzeby tego pokazu.</span><span class="sxs-lookup"><span data-stu-id="1227b-140">Start  at 31:50 toosee an overview of [hello Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into hello outbound section tooremove a number of data elements from hello response received from hello backend service based on hello name of hello api product -->  
<choose>  
  <when condition="@(context.Response.StatusCode == 200 && context.Product.Name.Equals("Starter"))">  
    <set-body>@{  
        var response = context.Response.Body.As<JObject>();  
        foreach (var key in new [] {"minutely", "hourly", "daily", "flags"}) {  
          response.Property (key).Remove ();  
        }  
        return response.ToString();  
      }  
    </set-body>  
  </when>  
</choose>  
```  
  
### <a name="elements"></a><span data-ttu-id="1227b-141">Elementy</span><span class="sxs-lookup"><span data-stu-id="1227b-141">Elements</span></span>  
  
|<span data-ttu-id="1227b-142">Element</span><span class="sxs-lookup"><span data-stu-id="1227b-142">Element</span></span>|<span data-ttu-id="1227b-143">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-143">Description</span></span>|<span data-ttu-id="1227b-144">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-144">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1227b-145">Wybierz pozycję</span><span class="sxs-lookup"><span data-stu-id="1227b-145">choose</span></span>|<span data-ttu-id="1227b-146">Element główny.</span><span class="sxs-lookup"><span data-stu-id="1227b-146">Root element.</span></span>|<span data-ttu-id="1227b-147">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-147">Yes</span></span>|  
|<span data-ttu-id="1227b-148">Kiedy</span><span class="sxs-lookup"><span data-stu-id="1227b-148">when</span></span>|<span data-ttu-id="1227b-149">Witaj toouse warunek dla hello `if` lub `ifelse` części hello `choose` zasad.</span><span class="sxs-lookup"><span data-stu-id="1227b-149">hello condition toouse for hello `if` or `ifelse` parts of hello `choose` policy.</span></span> <span data-ttu-id="1227b-150">Jeśli hello `choose` zasad ma wiele `when` sekcje są oceniane po kolei.</span><span class="sxs-lookup"><span data-stu-id="1227b-150">If hello `choose` policy has multiple `when` sections, they are evaluated sequentially.</span></span> <span data-ttu-id="1227b-151">Raz hello `condition` z o tym, kiedy element ocenia zbyt`true`, nie musisz `when` oceny warunków.</span><span class="sxs-lookup"><span data-stu-id="1227b-151">Once hello `condition` of a when element evaluates too`true`, no further `when` conditions are evaluated.</span></span>|<span data-ttu-id="1227b-152">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-152">Yes</span></span>|  
|<span data-ttu-id="1227b-153">w przeciwnym razie</span><span class="sxs-lookup"><span data-stu-id="1227b-153">otherwise</span></span>|<span data-ttu-id="1227b-154">Zawiera toobe fragment zasad hello używane, jeśli żaden z hello `when` warunki oceny zbyt`true`.</span><span class="sxs-lookup"><span data-stu-id="1227b-154">Contains hello policy snippet toobe used if none of hello `when` conditions evaluate too`true`.</span></span>|<span data-ttu-id="1227b-155">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-155">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1227b-156">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="1227b-156">Attributes</span></span>  
  
|<span data-ttu-id="1227b-157">Atrybut</span><span class="sxs-lookup"><span data-stu-id="1227b-157">Attribute</span></span>|<span data-ttu-id="1227b-158">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-158">Description</span></span>|<span data-ttu-id="1227b-159">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-159">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="1227b-160">warunek = "wyrażenie warunkowe & #124; Wartość logiczna stała"</span><span class="sxs-lookup"><span data-stu-id="1227b-160">condition="Boolean expression &#124; Boolean constant"</span></span>|<span data-ttu-id="1227b-161">wyrażenie warunkowe Hello lub tooevaluated stałej, gdy hello zawierający `when` oceny deklaracji zasad.</span><span class="sxs-lookup"><span data-stu-id="1227b-161">hello Boolean expression or constant tooevaluated when hello containing `when` policy statement is evaluated.</span></span>|<span data-ttu-id="1227b-162">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-162">Yes</span></span>|  
  
###  <span data-ttu-id="1227b-163"><a name="ChooseUsage"></a>Użycie</span><span class="sxs-lookup"><span data-stu-id="1227b-163"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="1227b-164">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1227b-164">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1227b-165">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="1227b-165">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1227b-166">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="1227b-166">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="1227b-167"><a name="ForwardRequest"></a>Przekazanie żądania</span><span class="sxs-lookup"><span data-stu-id="1227b-167"><a name="ForwardRequest"></a> Forward request</span></span>  
 <span data-ttu-id="1227b-168">Witaj `forward-request` zasad przekazuje hello przychodzącego żądania toohello usługi wewnętrznej bazy danych określony w żądaniu hello [kontekstu](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="1227b-168">hello `forward-request` policy forwards hello incoming request toohello backend service specified in hello request [context](api-management-policy-expressions.md#ContextVariables).</span></span> <span data-ttu-id="1227b-169">Witaj adres URL usługi wewnętrznej bazy danych jest określona w hello interfejsu API [ustawienia](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) i można zmieniać za pomocą hello [Ustaw usługę zaplecza](api-management-transformation-policies.md) zasad.</span><span class="sxs-lookup"><span data-stu-id="1227b-169">hello backend service URL is specified in hello API  [settings](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) and can be changed using hello [set backend service](api-management-transformation-policies.md) policy.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="1227b-170">Usunięcie tego wyników zasad w żądaniu hello nie przesyłane dalej toohello zasady hello i usługi wewnętrznej bazy danych w sekcji wychodzącego hello są oceniane natychmiast na pomyślne zakończenie zasad hello w hello hello ruchu przychodzącego sekcji.</span><span class="sxs-lookup"><span data-stu-id="1227b-170">Removing this policy results in hello request not being forwarded toohello backend service and hello policies in hello outbound section are evaluated immediately upon hello successful completion of hello policies in hello inbound section.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1227b-171">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="1227b-171">Policy statement</span></span>  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a><span data-ttu-id="1227b-172">Przykłady</span><span class="sxs-lookup"><span data-stu-id="1227b-172">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="1227b-173">Przykład</span><span class="sxs-lookup"><span data-stu-id="1227b-173">Example</span></span>  
 <span data-ttu-id="1227b-174">Witaj następujące zasady na poziomie interfejsu API przekazuje wszystkie żądania toohello usługi wewnętrznej bazy danych z limit czasu 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="1227b-174">hello following API level policy forwards all requests toohello backend service with a timeout interval of 60 seconds.</span></span>  
  
```xml  
<!-- api level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="60"/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="1227b-175">Przykład</span><span class="sxs-lookup"><span data-stu-id="1227b-175">Example</span></span>  
 <span data-ttu-id="1227b-176">Zasady na poziomie tej operacji używa hello `base` elementu tooinherit hello zaplecza zasady z poziomu zakresu nadrzędnego interfejsu API hello.</span><span class="sxs-lookup"><span data-stu-id="1227b-176">This operation level policy uses hello `base` element tooinherit hello backend policy from hello parent API level scope.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <base/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="1227b-177">Przykład</span><span class="sxs-lookup"><span data-stu-id="1227b-177">Example</span></span>  
 <span data-ttu-id="1227b-178">Tej zasady na poziomie operacji jawnie przekazuje wszystkie usługi wewnętrznej bazy danych z limitem czasu 120 żądań toohello i nie dziedziczy nadrzędnego hello zasad poziomu zaplecza interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="1227b-178">This operation level policy explicitly forwards all requests toohello backend service with a timeout of 120 and does not inherit hello parent API level backend policy.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="120"/>   
        <!-- effective policy. note hello absence of <base/> -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="1227b-179">Przykład</span><span class="sxs-lookup"><span data-stu-id="1227b-179">Example</span></span>  
 <span data-ttu-id="1227b-180">Zasady na poziomie tej operacji nie przekazuje żądania toohello usługi wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1227b-180">This operation level policy does not forward requests toohello backend service.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <!-- no forwarding toobackend -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="1227b-181">Elementy</span><span class="sxs-lookup"><span data-stu-id="1227b-181">Elements</span></span>  
  
|<span data-ttu-id="1227b-182">Element</span><span class="sxs-lookup"><span data-stu-id="1227b-182">Element</span></span>|<span data-ttu-id="1227b-183">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-183">Description</span></span>|<span data-ttu-id="1227b-184">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-184">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1227b-185">żądanie do przodu</span><span class="sxs-lookup"><span data-stu-id="1227b-185">forward-request</span></span>|<span data-ttu-id="1227b-186">Element główny.</span><span class="sxs-lookup"><span data-stu-id="1227b-186">Root element.</span></span>|<span data-ttu-id="1227b-187">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-187">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1227b-188">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="1227b-188">Attributes</span></span>  
  
|<span data-ttu-id="1227b-189">Atrybut</span><span class="sxs-lookup"><span data-stu-id="1227b-189">Attribute</span></span>|<span data-ttu-id="1227b-190">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-190">Description</span></span>|<span data-ttu-id="1227b-191">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-191">Required</span></span>|<span data-ttu-id="1227b-192">Domyślne</span><span class="sxs-lookup"><span data-stu-id="1227b-192">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="1227b-193">limit czasu = "int"</span><span class="sxs-lookup"><span data-stu-id="1227b-193">timeout="integer"</span></span>|<span data-ttu-id="1227b-194">Witaj — interwał limitu czasu w sekundach przed hello wywołania toohello wewnętrznej bazy danych usługi nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="1227b-194">hello timeout interval in seconds before hello call toohello backend service fails.</span></span>|<span data-ttu-id="1227b-195">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-195">No</span></span>|<span data-ttu-id="1227b-196">Brak limitu czasu</span><span class="sxs-lookup"><span data-stu-id="1227b-196">No timeout</span></span>|  
|<span data-ttu-id="1227b-197">Wykonaj przekierowania = "true & #124; false"</span><span class="sxs-lookup"><span data-stu-id="1227b-197">follow-redirects="true &#124; false"</span></span>|<span data-ttu-id="1227b-198">Określa, czy przekierowań z usługi zaplecza hello są następuje hello bramy lub zwrócił toohello wywołującego.</span><span class="sxs-lookup"><span data-stu-id="1227b-198">Specifies whether redirects from hello backend service are followed by hello gateway or returned toohello caller.</span></span>|<span data-ttu-id="1227b-199">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-199">No</span></span>|<span data-ttu-id="1227b-200">wartość false</span><span class="sxs-lookup"><span data-stu-id="1227b-200">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1227b-201">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="1227b-201">Usage</span></span>  
 <span data-ttu-id="1227b-202">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1227b-202">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1227b-203">**Sekcje zasad:** wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="1227b-203">**Policy sections:** backend</span></span>  
  
-   <span data-ttu-id="1227b-204">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="1227b-204">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="1227b-205"><a name="LimitConcurrency"></a>Limit współbieżności</span><span class="sxs-lookup"><span data-stu-id="1227b-205"><a name="LimitConcurrency"></a> Limit concurrency</span></span>  
 <span data-ttu-id="1227b-206">Witaj `limit-concurrency` zasad uniemożliwia objętego zasad wykonywania przez więcej niż hello określonej liczby żądań w danym momencie.</span><span class="sxs-lookup"><span data-stu-id="1227b-206">hello `limit-concurrency` policy prevents enclosed policies from executing by more than hello specified number of requests at a given time.</span></span> <span data-ttu-id="1227b-207">Po przekroczeniu progu hello, nowe żądania są dodawane kolejki tooa do hello kolejki maksymalną długość.</span><span class="sxs-lookup"><span data-stu-id="1227b-207">Upon exceeding hello threshold, new requests are added tooa queue, until hello maximum queue length is achieved.</span></span> <span data-ttu-id="1227b-208">Po wyczerpania kolejki nowe żądania nie powiedzie się natychmiast.</span><span class="sxs-lookup"><span data-stu-id="1227b-208">Upon queue exhaustion, new requests will fail immediately.</span></span>
  
###  <span data-ttu-id="1227b-209"><a name="LimitConcurrencyStatement"></a>Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="1227b-209"><a name="LimitConcurrencyStatement"></a> Policy statement</span></span>  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a><span data-ttu-id="1227b-210">Przykłady</span><span class="sxs-lookup"><span data-stu-id="1227b-210">Examples</span></span>  
  
####  <span data-ttu-id="1227b-211"><a name="ChooseExample"></a>Przykład</span><span class="sxs-lookup"><span data-stu-id="1227b-211"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="1227b-212">Witaj poniższym przykładzie pokazano, jak toolimit liczba żądań dalej tooa wewnętrznej bazy danych na podstawie wartości hello zmiennej kontekstu.</span><span class="sxs-lookup"><span data-stu-id="1227b-212">hello following example demonstrates how toolimit number of requests forwarded tooa backend based on hello value of a context variable.</span></span>
 
```xml  
<policies>
  <inbound>…</inbound>
  <backend>
    <limit-concurrency key="@((string)context.Variables["connectionId"])" max-count="3" timeout="60">
      <forward-request timeout="120"/>
    <limit-concurrency/>
  </backend>
  <outbound>…</outbound>
</policies>
```

### <a name="elements"></a><span data-ttu-id="1227b-213">Elementy</span><span class="sxs-lookup"><span data-stu-id="1227b-213">Elements</span></span>  
  
|<span data-ttu-id="1227b-214">Element</span><span class="sxs-lookup"><span data-stu-id="1227b-214">Element</span></span>|<span data-ttu-id="1227b-215">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-215">Description</span></span>|<span data-ttu-id="1227b-216">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-216">Required</span></span>|  
|-------------|-----------------|--------------|    
|<span data-ttu-id="1227b-217">limit współbieżności</span><span class="sxs-lookup"><span data-stu-id="1227b-217">limit-concurrency</span></span>|<span data-ttu-id="1227b-218">Element główny.</span><span class="sxs-lookup"><span data-stu-id="1227b-218">Root element.</span></span>|<span data-ttu-id="1227b-219">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1227b-220">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="1227b-220">Attributes</span></span>  
  
|<span data-ttu-id="1227b-221">Atrybut</span><span class="sxs-lookup"><span data-stu-id="1227b-221">Attribute</span></span>|<span data-ttu-id="1227b-222">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-222">Description</span></span>|<span data-ttu-id="1227b-223">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-223">Required</span></span>|<span data-ttu-id="1227b-224">Domyślne</span><span class="sxs-lookup"><span data-stu-id="1227b-224">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="1227b-225">key</span><span class="sxs-lookup"><span data-stu-id="1227b-225">key</span></span>|<span data-ttu-id="1227b-226">Ciąg.</span><span class="sxs-lookup"><span data-stu-id="1227b-226">A string.</span></span> <span data-ttu-id="1227b-227">Wyrażenie jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="1227b-227">Expression allowed.</span></span> <span data-ttu-id="1227b-228">Określa zakres współbieżności hello.</span><span class="sxs-lookup"><span data-stu-id="1227b-228">Specifies hello concurrency scope.</span></span> <span data-ttu-id="1227b-229">Może być współużytkowane przez wiele zasad.</span><span class="sxs-lookup"><span data-stu-id="1227b-229">Can be shared by multiple policies.</span></span>|<span data-ttu-id="1227b-230">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-230">Yes</span></span>|<span data-ttu-id="1227b-231">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="1227b-231">N/A</span></span>|  
|<span data-ttu-id="1227b-232">Maksymalna liczba</span><span class="sxs-lookup"><span data-stu-id="1227b-232">max-count</span></span>|<span data-ttu-id="1227b-233">Liczba całkowita.</span><span class="sxs-lookup"><span data-stu-id="1227b-233">An integer.</span></span> <span data-ttu-id="1227b-234">Określa maksymalną liczbę żądań, które mogą tooenter hello zasad.</span><span class="sxs-lookup"><span data-stu-id="1227b-234">Specifies a maximum number of requests that are allowed tooenter hello policy.</span></span>|<span data-ttu-id="1227b-235">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-235">Yes</span></span>|<span data-ttu-id="1227b-236">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="1227b-236">N/A</span></span>|  
|<span data-ttu-id="1227b-237">timeout</span><span class="sxs-lookup"><span data-stu-id="1227b-237">timeout</span></span>|<span data-ttu-id="1227b-238">Liczba całkowita.</span><span class="sxs-lookup"><span data-stu-id="1227b-238">An integer.</span></span> <span data-ttu-id="1227b-239">Wyrażenie jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="1227b-239">Expression allowed.</span></span> <span data-ttu-id="1227b-240">Określa hello liczbę sekund, żądanie powinno czekać tooenter zakresu przed niepowodzeniem z "403 zbyt wiele żądań"</span><span class="sxs-lookup"><span data-stu-id="1227b-240">Specifies hello number of seconds a request should wait tooenter a scope before failing with "403 Too Many Requests"</span></span>|<span data-ttu-id="1227b-241">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-241">No</span></span>|<span data-ttu-id="1227b-242">Infinity</span><span class="sxs-lookup"><span data-stu-id="1227b-242">Infinity</span></span>|  
|<span data-ttu-id="1227b-243">Maksymalna kolejki</span><span class="sxs-lookup"><span data-stu-id="1227b-243">max-queue-length</span></span>|<span data-ttu-id="1227b-244">Liczba całkowita.</span><span class="sxs-lookup"><span data-stu-id="1227b-244">An integer.</span></span> <span data-ttu-id="1227b-245">Wyrażenie jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="1227b-245">Expression allowed.</span></span> <span data-ttu-id="1227b-246">Określa hello kolejki maksymalną długość.</span><span class="sxs-lookup"><span data-stu-id="1227b-246">Specifies hello maximum queue length.</span></span> <span data-ttu-id="1227b-247">Żądań przychodzących w trakcie tooenter ta zasada zostanie zakończone z "403 zbyt wiele żądań" natychmiast po wyczerpaniu hello kolejki.</span><span class="sxs-lookup"><span data-stu-id="1227b-247">Incoming requests trying tooenter this policy will be terminated with “403 Too Many Requests” immediately when hello queue is exhausted.</span></span>|<span data-ttu-id="1227b-248">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-248">No</span></span>|<span data-ttu-id="1227b-249">Infinity</span><span class="sxs-lookup"><span data-stu-id="1227b-249">Infinity</span></span>|  
  
###  <span data-ttu-id="1227b-250"><a name="ChooseUsage"></a>Użycie</span><span class="sxs-lookup"><span data-stu-id="1227b-250"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="1227b-251">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1227b-251">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1227b-252">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="1227b-252">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1227b-253">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="1227b-253">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="1227b-254"><a name="log-to-eventhub"></a>Dziennik tooEvent Centrum</span><span class="sxs-lookup"><span data-stu-id="1227b-254"><a name="log-to-eventhub"></a> Log tooEvent Hub</span></span>  
 <span data-ttu-id="1227b-255">Witaj `log-to-eventhub` zasad wysyła wiadomości powitania określony format tooan Centrum zdarzeń zdefiniowanych przez podmiot rejestratora.</span><span class="sxs-lookup"><span data-stu-id="1227b-255">hello `log-to-eventhub` policy sends messages in hello specified format tooan Event Hub defined by a Logger entity.</span></span> <span data-ttu-id="1227b-256">Jak jego nazwa wskazuje, hello zasad służy do zapisywania wybrane informacje kontekstu żądania lub odpowiedzi do analizy w trybie online lub offline.</span><span class="sxs-lookup"><span data-stu-id="1227b-256">As its name implies, hello policy is used for saving selected request or response context information for online or offline analysis.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="1227b-257">Przewodnik krok po kroku dotyczące konfigurowania Centrum zdarzeń i rejestrowania zdarzeń dla [jak toolog zdarzenia interfejsu API zarządzania za pomocą usługi Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="1227b-257">For a step-by-step guide on configuring an event hub and logging events, see [How toolog API Management events with Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1227b-258">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="1227b-258">Policy statement</span></span>  
  
```xml  
<log-to-eventhub logger-id="id of hello logger entity" partition-id="index of hello partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string toobe logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a><span data-ttu-id="1227b-259">Przykład</span><span class="sxs-lookup"><span data-stu-id="1227b-259">Example</span></span>  
 <span data-ttu-id="1227b-260">Dowolny ciąg może służyć jako toobe wartość hello rejestrowane w usłudze Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="1227b-260">Any string can be used as hello value toobe logged in Event Hubs.</span></span> <span data-ttu-id="1227b-261">W tym przykładzie hello Data i godzina wdrożenia, nazwę usługi, identyfikator żądania adresu ip i nazwy operacji dla wszystkich połączeń przychodzących są Centrum zdarzeń zarejestrowanych toohello rejestratora zarejestrowany hello `contoso-logger` identyfikator.</span><span class="sxs-lookup"><span data-stu-id="1227b-261">In this example hello date and time, deployment service name, request id, ip address, and operation name for all inbound calls are logged toohello event hub Logger registered with hello `contoso-logger` id.</span></span>  
  
```xml  
<policies>  
  <inbound>  
    <log-to-eventhub logger-id ='contoso-logger'>  
      @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name) )   
    </log-to-eventhub>  
  </inbound>  
  <outbound>          
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="1227b-262">Elementy</span><span class="sxs-lookup"><span data-stu-id="1227b-262">Elements</span></span>  
  
|<span data-ttu-id="1227b-263">Element</span><span class="sxs-lookup"><span data-stu-id="1227b-263">Element</span></span>|<span data-ttu-id="1227b-264">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-264">Description</span></span>|<span data-ttu-id="1227b-265">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-265">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1227b-266">dziennika do Centrum eventhub</span><span class="sxs-lookup"><span data-stu-id="1227b-266">log-to-eventhub</span></span>|<span data-ttu-id="1227b-267">Element główny.</span><span class="sxs-lookup"><span data-stu-id="1227b-267">Root element.</span></span> <span data-ttu-id="1227b-268">wartość Hello tego elementu jest Centrum zdarzeń tooyour toolog ciąg hello.</span><span class="sxs-lookup"><span data-stu-id="1227b-268">hello value of this element is hello string toolog tooyour event hub.</span></span>|<span data-ttu-id="1227b-269">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-269">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1227b-270">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="1227b-270">Attributes</span></span>  
  
|<span data-ttu-id="1227b-271">Atrybut</span><span class="sxs-lookup"><span data-stu-id="1227b-271">Attribute</span></span>|<span data-ttu-id="1227b-272">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-272">Description</span></span>|<span data-ttu-id="1227b-273">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-273">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="1227b-274">identyfikator rejestratora</span><span class="sxs-lookup"><span data-stu-id="1227b-274">logger-id</span></span>|<span data-ttu-id="1227b-275">Identyfikator Hello hello rejestratora zarejestrowana przy użyciu usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="1227b-275">hello id of hello Logger registered with your API Management service.</span></span>|<span data-ttu-id="1227b-276">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-276">Yes</span></span>|  
|<span data-ttu-id="1227b-277">Identyfikator partycji</span><span class="sxs-lookup"><span data-stu-id="1227b-277">partition-id</span></span>|<span data-ttu-id="1227b-278">Określa indeks hello partycji hello wysyłania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="1227b-278">Specifies hello index of hello partition where messages are sent.</span></span>|<span data-ttu-id="1227b-279">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="1227b-279">Optional.</span></span> <span data-ttu-id="1227b-280">Ten atrybut nie może być używany, jeśli `partition-key` jest używany.</span><span class="sxs-lookup"><span data-stu-id="1227b-280">This attribute may not be used if `partition-key` is used.</span></span>|  
|<span data-ttu-id="1227b-281">Klucz partycji</span><span class="sxs-lookup"><span data-stu-id="1227b-281">partition-key</span></span>|<span data-ttu-id="1227b-282">Określa wartość hello używany do przypisania partycji podczas wysyłania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="1227b-282">Specifies hello value used for partition assignment when messages are sent.</span></span>|<span data-ttu-id="1227b-283">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="1227b-283">Optional.</span></span> <span data-ttu-id="1227b-284">Ten atrybut nie może być używany, jeśli `partition-id` jest używany.</span><span class="sxs-lookup"><span data-stu-id="1227b-284">This attribute may not be used if `partition-id` is used.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1227b-285">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="1227b-285">Usage</span></span>  
 <span data-ttu-id="1227b-286">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1227b-286">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1227b-287">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="1227b-287">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1227b-288">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="1227b-288">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="1227b-289"><a name="mock-response"></a>Zasymulować odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1227b-289"><a name="mock-response"></a> Mock response</span></span>  
<span data-ttu-id="1227b-290">Witaj `mock-response`, jako nazwa hello oznacza, że jest używana toomock interfejsów API i operacji.</span><span class="sxs-lookup"><span data-stu-id="1227b-290">hello `mock-response`, as hello name implies, is used toomock APIs and operations.</span></span> <span data-ttu-id="1227b-291">Przerywa wykonywanie normalny potok, a zwraca obiekt wywołujący toohello mocked odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="1227b-291">It aborts normal pipeline execution and returns a mocked response toohello caller.</span></span> <span data-ttu-id="1227b-292">zasady Hello zawsze próbuje odpowiedzi tooreturn wierności najwyższy.</span><span class="sxs-lookup"><span data-stu-id="1227b-292">hello policy always tries tooreturn responses of highest fidelity.</span></span> <span data-ttu-id="1227b-293">Preferuje go przykłady zawartości odpowiedzi, gdy dostępne.</span><span class="sxs-lookup"><span data-stu-id="1227b-293">It prefers response content examples, whenever available.</span></span> <span data-ttu-id="1227b-294">Generuje on przykładowe odpowiedzi ze schematów, gdy znajdują się schematów i przykłady nie.</span><span class="sxs-lookup"><span data-stu-id="1227b-294">It generates sample responses from schemas, when schemas are provided and examples are not.</span></span> <span data-ttu-id="1227b-295">W przypadku znalezienia przykłady ani schematów odpowiedzi z zawartością, nie są zwracane.</span><span class="sxs-lookup"><span data-stu-id="1227b-295">If neither examples or schemas are found, responses with no content are returned.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="1227b-296">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="1227b-296">Policy statement</span></span>  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="1227b-297">Przykłady</span><span class="sxs-lookup"><span data-stu-id="1227b-297">Examples</span></span>  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, hello content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, hello content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a><span data-ttu-id="1227b-298">Elementy</span><span class="sxs-lookup"><span data-stu-id="1227b-298">Elements</span></span>  
  
|<span data-ttu-id="1227b-299">Element</span><span class="sxs-lookup"><span data-stu-id="1227b-299">Element</span></span>|<span data-ttu-id="1227b-300">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-300">Description</span></span>|<span data-ttu-id="1227b-301">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-301">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1227b-302">makiety odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1227b-302">mock-response</span></span>|<span data-ttu-id="1227b-303">Element główny.</span><span class="sxs-lookup"><span data-stu-id="1227b-303">Root element.</span></span>|<span data-ttu-id="1227b-304">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-304">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1227b-305">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="1227b-305">Attributes</span></span>  
  
|<span data-ttu-id="1227b-306">Atrybut</span><span class="sxs-lookup"><span data-stu-id="1227b-306">Attribute</span></span>|<span data-ttu-id="1227b-307">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-307">Description</span></span>|<span data-ttu-id="1227b-308">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-308">Required</span></span>|<span data-ttu-id="1227b-309">Domyślne</span><span class="sxs-lookup"><span data-stu-id="1227b-309">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="1227b-310">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="1227b-310">status-code</span></span>|<span data-ttu-id="1227b-311">Określa kod stanu odpowiedzi i jest używane tooselect odpowiedni przykład lub schematu.</span><span class="sxs-lookup"><span data-stu-id="1227b-311">Specifies response status code and is used tooselect corresponding example or schema.</span></span>|<span data-ttu-id="1227b-312">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-312">No</span></span>|<span data-ttu-id="1227b-313">200</span><span class="sxs-lookup"><span data-stu-id="1227b-313">200</span></span>|  
|<span data-ttu-id="1227b-314">Typ zawartości</span><span class="sxs-lookup"><span data-stu-id="1227b-314">content-type</span></span>|<span data-ttu-id="1227b-315">Określa `Content-Type` wartość nagłówka odpowiedzi i jest używane tooselect odpowiedni przykład lub schematu.</span><span class="sxs-lookup"><span data-stu-id="1227b-315">Specifies `Content-Type` response header value and is used tooselect corresponding example or schema.</span></span>|<span data-ttu-id="1227b-316">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-316">No</span></span>|<span data-ttu-id="1227b-317">Brak</span><span class="sxs-lookup"><span data-stu-id="1227b-317">None</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1227b-318">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="1227b-318">Usage</span></span>  
 <span data-ttu-id="1227b-319">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1227b-319">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1227b-320">**Sekcje zasad:** przychodzące, wychodzące, na błąd</span><span class="sxs-lookup"><span data-stu-id="1227b-320">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="1227b-321">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="1227b-321">**Policy scopes:** all scopes</span></span>

##  <span data-ttu-id="1227b-322"><a name="Retry"></a>Spróbuj ponownie</span><span class="sxs-lookup"><span data-stu-id="1227b-322"><a name="Retry"></a> Retry</span></span>  
 <span data-ttu-id="1227b-323">Witaj `retry` zasad jego zasad podrzędnych jest wykonywana raz i ponowi próbę ich realizacji do ponawiania hello `condition` staje się `false` lub ponów próbę `count` jest wyczerpana.</span><span class="sxs-lookup"><span data-stu-id="1227b-323">hello             `retry` policy executes its child policies once and then retries their execution until hello retry `condition` becomes            `false` or retry            `count` is exhausted.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1227b-324">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="1227b-324">Policy statement</span></span>  
  
```xml  
  
<retry  
    condition="boolean expression or literal"  
    count="number of retry attempts"  
    interval="retry interval in seconds"  
    max-interval="maximum retry interval in seconds"  
    delta="retry interval delta in seconds"  
    first-fast-retry="boolean expression or literal">  
        <!-- One or more child policies. No restrictions -->  
</retry>  
  
```  
  
### <a name="example"></a><span data-ttu-id="1227b-325">Przykład</span><span class="sxs-lookup"><span data-stu-id="1227b-325">Example</span></span>  
 <span data-ttu-id="1227b-326">W hello następujące przykładowe żądanie forewarding próba zostanie ponowiona się tooten użyciu algorytm wykładnicze ponów próbę.</span><span class="sxs-lookup"><span data-stu-id="1227b-326">In hello following example request forewarding is retried up tooten times using exponential retry algorithm.</span></span> <span data-ttu-id="1227b-327">Ponieważ `first-fast-retry` ustawiono toofalse, Algorytm ponownych prób exponsntial toohello podmiotu są wszystkie ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="1227b-327">Since                    `first-fast-retry` is set toofalse, all retry attempts are subject toohello exponsntial retry algorithm.</span></span>  
  
```xml  
  
<retry  
    condition="@(context.Response.StatusCode == 500)"  
    count="10"  
    interval="10"  
    max-interval="100"  
    delta="10"  
    first-fast-retry="false">  
        <forward-request />  
</retry>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="1227b-328">Elementy</span><span class="sxs-lookup"><span data-stu-id="1227b-328">Elements</span></span>  
  
|<span data-ttu-id="1227b-329">Element</span><span class="sxs-lookup"><span data-stu-id="1227b-329">Element</span></span>|<span data-ttu-id="1227b-330">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-330">Description</span></span>|<span data-ttu-id="1227b-331">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-331">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1227b-332">retry</span><span class="sxs-lookup"><span data-stu-id="1227b-332">retry</span></span>|<span data-ttu-id="1227b-333">Element główny.</span><span class="sxs-lookup"><span data-stu-id="1227b-333">Root element.</span></span> <span data-ttu-id="1227b-334">Może zawierać inne zasady jako jego elementy podrzędne.</span><span class="sxs-lookup"><span data-stu-id="1227b-334">May contain any other policies as its child elements.</span></span>|<span data-ttu-id="1227b-335">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-335">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1227b-336">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="1227b-336">Attributes</span></span>  
  
|<span data-ttu-id="1227b-337">Atrybut</span><span class="sxs-lookup"><span data-stu-id="1227b-337">Attribute</span></span>|<span data-ttu-id="1227b-338">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-338">Description</span></span>|<span data-ttu-id="1227b-339">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-339">Required</span></span>|<span data-ttu-id="1227b-340">Domyślne</span><span class="sxs-lookup"><span data-stu-id="1227b-340">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="1227b-341">Warunek</span><span class="sxs-lookup"><span data-stu-id="1227b-341">condition</span></span>|<span data-ttu-id="1227b-342">Logiczna literał lub [wyrażenie](api-management-policy-expressions.md) określenie ponownych prób powinna zostać zatrzymana (`false`) lub nadal (`true`).</span><span class="sxs-lookup"><span data-stu-id="1227b-342">A boolean literal or [expression](api-management-policy-expressions.md) specifying if retries should be stopped (`false`) or continued (`true`).</span></span>|<span data-ttu-id="1227b-343">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-343">Yes</span></span>|<span data-ttu-id="1227b-344">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="1227b-344">N/A</span></span>|  
|<span data-ttu-id="1227b-345">Liczba</span><span class="sxs-lookup"><span data-stu-id="1227b-345">count</span></span>|<span data-ttu-id="1227b-346">Liczba dodatnia określająca maksymalną liczbę ponownych prób tooattempt hello.</span><span class="sxs-lookup"><span data-stu-id="1227b-346">A positive number specifying hello maximum number of retries tooattempt.</span></span>|<span data-ttu-id="1227b-347">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-347">Yes</span></span>|<span data-ttu-id="1227b-348">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="1227b-348">N/A</span></span>|  
|<span data-ttu-id="1227b-349">interval</span><span class="sxs-lookup"><span data-stu-id="1227b-349">interval</span></span>|<span data-ttu-id="1227b-350">Liczba dodatnia, w sekundach, określając hello interwału oczekiwania między hello ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="1227b-350">A positive number in seconds specifying hello wait interval between hello retry attempts.</span></span>|<span data-ttu-id="1227b-351">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-351">Yes</span></span>|<span data-ttu-id="1227b-352">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="1227b-352">N/A</span></span>|  
|<span data-ttu-id="1227b-353">Maksymalny interwał</span><span class="sxs-lookup"><span data-stu-id="1227b-353">max-interval</span></span>|<span data-ttu-id="1227b-354">Liczba dodatnia, w sekundach, określając hello oczekiwania maksymalny interwał hello ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="1227b-354">A positive number in seconds specifying hello maximum wait interval between hello retry attempts.</span></span> <span data-ttu-id="1227b-355">Jest używana tooimplement algorytm wykładnicze ponów próbę.</span><span class="sxs-lookup"><span data-stu-id="1227b-355">It is used tooimplement an exponential retry algorithm.</span></span>|<span data-ttu-id="1227b-356">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-356">No</span></span>|<span data-ttu-id="1227b-357">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="1227b-357">N/A</span></span>|  
|<span data-ttu-id="1227b-358">delta</span><span class="sxs-lookup"><span data-stu-id="1227b-358">delta</span></span>|<span data-ttu-id="1227b-359">Liczba dodatnia, w sekundach, określając przyrostu interwału oczekiwania hello.</span><span class="sxs-lookup"><span data-stu-id="1227b-359">A positive number in seconds specifying hello wait interval increment.</span></span> <span data-ttu-id="1227b-360">Jest używane tooimplement hello liniowej i wykładniczej ponownych prób algorytmów.</span><span class="sxs-lookup"><span data-stu-id="1227b-360">It is used tooimplement hello linear and exponential retry algorithms.</span></span>|<span data-ttu-id="1227b-361">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-361">No</span></span>|<span data-ttu-id="1227b-362">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="1227b-362">N/A</span></span>|  
|<span data-ttu-id="1227b-363">pierwszy ponownej próby fast</span><span class="sxs-lookup"><span data-stu-id="1227b-363">first-fast-retry</span></span>|<span data-ttu-id="1227b-364">Jeśli ustawiona zbyt `true` , hello pierwszy ponowienia próby jest wykonywane bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="1227b-364">If set too                                   `true` , hello first retry attempt is performed immediately.</span></span>|<span data-ttu-id="1227b-365">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-365">No</span></span>|`false`|  
  
> [!NOTE]
>  <span data-ttu-id="1227b-366">Gdy tylko hello `interval` jest określony, **stałej** Interwał ponownych prób są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="1227b-366">When only hello `interval` is specified, **fixed** interval retries are performed.</span></span>  
>  <span data-ttu-id="1227b-367">Gdy tylko hello `interval` i `delta` są określone, **liniowej** interwału ponawiania algorytm jest używany, gdy czas oczekiwania między kolejnymi próbami jest obliczeniowej hello zgodnie z następującej formuły — `interval + (count - 1)*delta`.</span><span class="sxs-lookup"><span data-stu-id="1227b-367">When only hello `interval` and `delta` are specified, a **linear** interval retry algorithm is used, where wait time between retries is calculated according hello following formula - `interval + (count - 1)*delta`.</span></span>  
>  <span data-ttu-id="1227b-368">Gdy hello `interval`, `max-interval` i `delta` są określone, **wykładniczej** interwału ponawiania algorytm jest stosowana, gdy czas oczekiwania hello między kolejnymi próbami hello rośnie wykładniczo od wartości hello `interval`wartość toohello `max-interval` zgodnie z następujących toohello forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span><span class="sxs-lookup"><span data-stu-id="1227b-368">When hello `interval`, `max-interval` and `delta` are specified, **exponential** interval retry algorithm is applied, where hello wait time between hello retries is growing exponentially from hello value of `interval` toohello value `max-interval` according toohello following forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span></span>  
  
### <a name="usage"></a><span data-ttu-id="1227b-369">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="1227b-369">Usage</span></span>  
 <span data-ttu-id="1227b-370">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="1227b-370">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span> <span data-ttu-id="1227b-371">Należy pamiętać, że ograniczenia użycia zasad podrzędne będą dziedziczone przez te zasady.</span><span class="sxs-lookup"><span data-stu-id="1227b-371">Note that child policy usage restrictions will be inherited by this policy.</span></span>  
  
-   <span data-ttu-id="1227b-372">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="1227b-372">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1227b-373">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="1227b-373">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="1227b-374"><a name="ReturnResponse"></a>Odpowiedź zwrócona</span><span class="sxs-lookup"><span data-stu-id="1227b-374"><a name="ReturnResponse"></a> Return response</span></span>  
 <span data-ttu-id="1227b-375">Witaj `return-response` zasad przerwanie wykonywania potoku i zwraca domyślnych lub niestandardowych odpowiedzi toohello wywołującego.</span><span class="sxs-lookup"><span data-stu-id="1227b-375">hello `return-response` policy aborts pipeline execution and returns either a default or custom response toohello caller.</span></span> <span data-ttu-id="1227b-376">Domyślny jest `200 OK` nie jednostki.</span><span class="sxs-lookup"><span data-stu-id="1227b-376">Default response is `200 OK` with no body.</span></span> <span data-ttu-id="1227b-377">Za pomocą instrukcji kontekstu zmiennej lub zasad można określić niestandardową odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="1227b-377">Custom response can be specified via a context variable or policy statements.</span></span> <span data-ttu-id="1227b-378">Zarówno udostępniane hello zawartych w zmiennej kontekstu hello modyfikacja odpowiedzi przez deklaracji zasad hello przed zwróceniem toohello wywołującego.</span><span class="sxs-lookup"><span data-stu-id="1227b-378">When both are provided, hello response contained within hello context variable is modified by hello policy statements before being returned toohello caller.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1227b-379">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="1227b-379">Policy statement</span></span>  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a><span data-ttu-id="1227b-380">Przykład</span><span class="sxs-lookup"><span data-stu-id="1227b-380">Example</span></span>  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="1227b-381">Elementy</span><span class="sxs-lookup"><span data-stu-id="1227b-381">Elements</span></span>  
  
|<span data-ttu-id="1227b-382">Element</span><span class="sxs-lookup"><span data-stu-id="1227b-382">Element</span></span>|<span data-ttu-id="1227b-383">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-383">Description</span></span>|<span data-ttu-id="1227b-384">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-384">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1227b-385">odpowiedź Return</span><span class="sxs-lookup"><span data-stu-id="1227b-385">return-response</span></span>|<span data-ttu-id="1227b-386">Element główny.</span><span class="sxs-lookup"><span data-stu-id="1227b-386">Root element.</span></span>|<span data-ttu-id="1227b-387">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-387">Yes</span></span>|  
|<span data-ttu-id="1227b-388">set — nagłówek</span><span class="sxs-lookup"><span data-stu-id="1227b-388">set-header</span></span>|<span data-ttu-id="1227b-389">A [nagłówka set](api-management-transformation-policies.md#SetHTTPheader) deklaracji zasad.</span><span class="sxs-lookup"><span data-stu-id="1227b-389">A [set-header](api-management-transformation-policies.md#SetHTTPheader) policy statement.</span></span>|<span data-ttu-id="1227b-390">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-390">No</span></span>|  
|<span data-ttu-id="1227b-391">zestaw treści</span><span class="sxs-lookup"><span data-stu-id="1227b-391">set-body</span></span>|<span data-ttu-id="1227b-392">A [treści zestaw](api-management-transformation-policies.md#SetBody) deklaracji zasad.</span><span class="sxs-lookup"><span data-stu-id="1227b-392">A [set-body](api-management-transformation-policies.md#SetBody) policy statement.</span></span>|<span data-ttu-id="1227b-393">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-393">No</span></span>|  
|<span data-ttu-id="1227b-394">Ustaw stan</span><span class="sxs-lookup"><span data-stu-id="1227b-394">set-status</span></span>|<span data-ttu-id="1227b-395">A [Ustaw stan](api-management-advanced-policies.md#SetStatus) deklaracji zasad.</span><span class="sxs-lookup"><span data-stu-id="1227b-395">A [set-status](api-management-advanced-policies.md#SetStatus) policy statement.</span></span>|<span data-ttu-id="1227b-396">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-396">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1227b-397">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="1227b-397">Attributes</span></span>  
  
|<span data-ttu-id="1227b-398">Atrybut</span><span class="sxs-lookup"><span data-stu-id="1227b-398">Attribute</span></span>|<span data-ttu-id="1227b-399">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-399">Description</span></span>|<span data-ttu-id="1227b-400">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-400">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="1227b-401">Nazwa zmiennej odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1227b-401">response-variable-name</span></span>|<span data-ttu-id="1227b-402">Witaj nazwa zmiennej kontekstu hello odwołuje się do z, na przykład nadrzędnym [żądanie wysłania](api-management-advanced-policies.md#SendRequest) zasad i zawierający `Response` obiektu</span><span class="sxs-lookup"><span data-stu-id="1227b-402">hello name of hello context variable referenced from, for example, an upstream [send-request](api-management-advanced-policies.md#SendRequest) policy and containing a `Response` object</span></span>|<span data-ttu-id="1227b-403">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="1227b-403">Optional.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1227b-404">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="1227b-404">Usage</span></span>  
 <span data-ttu-id="1227b-405">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1227b-405">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1227b-406">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="1227b-406">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1227b-407">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="1227b-407">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="1227b-408"><a name="SendOneWayRequest"></a>Wyślij żądanie jednokierunkowej</span><span class="sxs-lookup"><span data-stu-id="1227b-408"><a name="SendOneWayRequest"></a> Send one way request</span></span>  
 <span data-ttu-id="1227b-409">Witaj `send-one-way-request` zasad wysyła żądanie hello podany adres URL określony toohello bez oczekiwania na odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="1227b-409">hello `send-one-way-request` policy sends hello provided request toohello specified URL without waiting for a response.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1227b-410">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="1227b-410">Policy statement</span></span>  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="1227b-411">Przykład</span><span class="sxs-lookup"><span data-stu-id="1227b-411">Example</span></span>  
 <span data-ttu-id="1227b-412">Ta zasada przykładowych pokazano przykład przy użyciu hello `send-one-way-request` zasad toosend komunikat tooa Slack pokoju rozmów Jeśli hello kod odpowiedzi HTTP jest większa niż lub równa too500.</span><span class="sxs-lookup"><span data-stu-id="1227b-412">This sample policy shows an example of using hello `send-one-way-request` policy toosend a message tooa Slack chat room if hello HTTP response code is greater than or equal too500.</span></span> <span data-ttu-id="1227b-413">Aby uzyskać więcej informacji na ten przykład, zobacz [za pomocą usług zewnętrznych z usługi Azure API Management hello](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="1227b-413">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="1227b-414">Elementy</span><span class="sxs-lookup"><span data-stu-id="1227b-414">Elements</span></span>  
  
|<span data-ttu-id="1227b-415">Element</span><span class="sxs-lookup"><span data-stu-id="1227b-415">Element</span></span>|<span data-ttu-id="1227b-416">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-416">Description</span></span>|<span data-ttu-id="1227b-417">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-417">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1227b-418">sposób żądania, Wyślij co w-</span><span class="sxs-lookup"><span data-stu-id="1227b-418">send-one-way-request</span></span>|<span data-ttu-id="1227b-419">Element główny.</span><span class="sxs-lookup"><span data-stu-id="1227b-419">Root element.</span></span>|<span data-ttu-id="1227b-420">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-420">Yes</span></span>|  
|<span data-ttu-id="1227b-421">adres URL</span><span class="sxs-lookup"><span data-stu-id="1227b-421">url</span></span>|<span data-ttu-id="1227b-422">adres URL Hello hello żądania.</span><span class="sxs-lookup"><span data-stu-id="1227b-422">hello URL of hello request.</span></span>|<span data-ttu-id="1227b-423">Jeśli nie trybu = kopiowania; tak, w przeciwnym razie wartość.</span><span class="sxs-lookup"><span data-stu-id="1227b-423">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="1227b-424">— Metoda</span><span class="sxs-lookup"><span data-stu-id="1227b-424">method</span></span>|<span data-ttu-id="1227b-425">Metoda HTTP dla żądania hello Hello.</span><span class="sxs-lookup"><span data-stu-id="1227b-425">hello HTTP method for hello request.</span></span>|<span data-ttu-id="1227b-426">Jeśli nie trybu = kopiowania; tak, w przeciwnym razie wartość.</span><span class="sxs-lookup"><span data-stu-id="1227b-426">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="1227b-427">nagłówek</span><span class="sxs-lookup"><span data-stu-id="1227b-427">header</span></span>|<span data-ttu-id="1227b-428">Nagłówek żądania.</span><span class="sxs-lookup"><span data-stu-id="1227b-428">Request header.</span></span> <span data-ttu-id="1227b-429">Użyj wielu elementów nagłówka dla wielu nagłówków żądania.</span><span class="sxs-lookup"><span data-stu-id="1227b-429">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="1227b-430">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-430">No</span></span>|  
|<span data-ttu-id="1227b-431">Treści</span><span class="sxs-lookup"><span data-stu-id="1227b-431">body</span></span>|<span data-ttu-id="1227b-432">Witaj treści żądania.</span><span class="sxs-lookup"><span data-stu-id="1227b-432">hello request body.</span></span>|<span data-ttu-id="1227b-433">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-433">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1227b-434">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="1227b-434">Attributes</span></span>  
  
|<span data-ttu-id="1227b-435">Atrybut</span><span class="sxs-lookup"><span data-stu-id="1227b-435">Attribute</span></span>|<span data-ttu-id="1227b-436">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-436">Description</span></span>|<span data-ttu-id="1227b-437">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-437">Required</span></span>|<span data-ttu-id="1227b-438">Domyślne</span><span class="sxs-lookup"><span data-stu-id="1227b-438">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="1227b-439">tryb = "string"</span><span class="sxs-lookup"><span data-stu-id="1227b-439">mode="string"</span></span>|<span data-ttu-id="1227b-440">Określa, czy jest to nowe żądanie lub kopię hello bieżącego żądania.</span><span class="sxs-lookup"><span data-stu-id="1227b-440">Determines whether this is a new request or a copy of hello current request.</span></span> <span data-ttu-id="1227b-441">W trybie wychodzących tryb = kopiowania nie inicjuje hello treści żądania.</span><span class="sxs-lookup"><span data-stu-id="1227b-441">In outbound mode, mode=copy does not initialize hello request body.</span></span>|<span data-ttu-id="1227b-442">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-442">No</span></span>|<span data-ttu-id="1227b-443">Nowy</span><span class="sxs-lookup"><span data-stu-id="1227b-443">New</span></span>|  
|<span data-ttu-id="1227b-444">name</span><span class="sxs-lookup"><span data-stu-id="1227b-444">name</span></span>|<span data-ttu-id="1227b-445">Określa nazwę hello hello nagłówka toobe zestawu.</span><span class="sxs-lookup"><span data-stu-id="1227b-445">Specifies hello name of hello header toobe set.</span></span>|<span data-ttu-id="1227b-446">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-446">Yes</span></span>|<span data-ttu-id="1227b-447">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="1227b-447">N/A</span></span>|  
|<span data-ttu-id="1227b-448">istnieje akcja</span><span class="sxs-lookup"><span data-stu-id="1227b-448">exists-action</span></span>|<span data-ttu-id="1227b-449">Określa jaki tootake akcji, gdy nagłówek hello został już określony.</span><span class="sxs-lookup"><span data-stu-id="1227b-449">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="1227b-450">Ten atrybut musi mieć jedną z hello następujące wartości.</span><span class="sxs-lookup"><span data-stu-id="1227b-450">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="1227b-451">-- zastępuje hello wartość zastępczą hello istniejący nagłówek.</span><span class="sxs-lookup"><span data-stu-id="1227b-451">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="1227b-452">-skip — nie zastępuje istniejącą wartość nagłówka hello.</span><span class="sxs-lookup"><span data-stu-id="1227b-452">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="1227b-453">-dołączania - dołącza hello wartość toohello istniejącą wartość nagłówka.</span><span class="sxs-lookup"><span data-stu-id="1227b-453">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="1227b-454">-Usunięcie — usuwa hello nagłówek z żądania hello.</span><span class="sxs-lookup"><span data-stu-id="1227b-454">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="1227b-455">Gdy ustawiona zbyt`override` rejestrowanie wiele wpisów z hello sama nazwa wyniki w nagłówku hello jest zestaw zgodnie z tooall zapisów (które zostaną wyświetlone wiele razy); w wyniku hello zostanie ustawiona tylko wartości wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="1227b-455">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="1227b-456">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-456">No</span></span>|<span data-ttu-id="1227b-457">zastąpienie</span><span class="sxs-lookup"><span data-stu-id="1227b-457">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1227b-458">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="1227b-458">Usage</span></span>  
 <span data-ttu-id="1227b-459">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1227b-459">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1227b-460">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="1227b-460">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1227b-461">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="1227b-461">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="1227b-462"><a name="SendRequest"></a>Wyślij żądanie</span><span class="sxs-lookup"><span data-stu-id="1227b-462"><a name="SendRequest"></a> Send request</span></span>  
 <span data-ttu-id="1227b-463">Witaj `send-request` zasad wysyła żądanie hello podane toohello określony adres URL, nie jest już oczekujące niż hello ustawić wartość limitu czasu.</span><span class="sxs-lookup"><span data-stu-id="1227b-463">hello `send-request` policy sends hello provided request toohello specified URL, waiting no longer than hello set timeout value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1227b-464">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="1227b-464">Policy statement</span></span>  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="1227b-465">Przykład</span><span class="sxs-lookup"><span data-stu-id="1227b-465">Example</span></span>  
 <span data-ttu-id="1227b-466">Ten przykład przedstawia jednokierunkowej tooverify token odwołania z serwera autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="1227b-466">This example shows one way tooverify a reference token with an authorization server.</span></span> <span data-ttu-id="1227b-467">Aby uzyskać więcej informacji na ten przykład, zobacz [za pomocą usług zewnętrznych z usługi Azure API Management hello](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="1227b-467">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<inbound>  
  <!-- Extract Token from Authorization header parameter -->  
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />  
  
  <!-- Send request tooToken Server toovalidate token (see RFC 7662) -->  
  <send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">  
    <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>  
    <set-method>POST</set-method>  
    <set-header name="Authorization" exists-action="override">  
      <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>  
    </set-header>  
    <set-header name="Content-Type" exists-action="override">  
      <value>application/x-www-form-urlencoded</value>  
    </set-header>  
    <set-body>@($"token={(string)context.Variables["token"]}")</set-body>  
  </send-request>  
  
  <choose>  
        <!-- Check active property in response -->  
        <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
            <!-- Return 401 Unauthorized with http-problem payload -->  
            <return-response response-variable-name="existing response variable">  
                <set-status code="401" reason="Unauthorized" />  
                <set-header name="WWW-Authenticate" exists-action="override">  
                    <value>Bearer error="invalid_token"</value>  
                </set-header>  
            </return-response>  
        </when>  
    </choose>  
  <base />  
</inbound>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="1227b-468">Elementy</span><span class="sxs-lookup"><span data-stu-id="1227b-468">Elements</span></span>  
  
|<span data-ttu-id="1227b-469">Element</span><span class="sxs-lookup"><span data-stu-id="1227b-469">Element</span></span>|<span data-ttu-id="1227b-470">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-470">Description</span></span>|<span data-ttu-id="1227b-471">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-471">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1227b-472">Żądanie wysłania</span><span class="sxs-lookup"><span data-stu-id="1227b-472">send-request</span></span>|<span data-ttu-id="1227b-473">Element główny.</span><span class="sxs-lookup"><span data-stu-id="1227b-473">Root element.</span></span>|<span data-ttu-id="1227b-474">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-474">Yes</span></span>|  
|<span data-ttu-id="1227b-475">adres URL</span><span class="sxs-lookup"><span data-stu-id="1227b-475">url</span></span>|<span data-ttu-id="1227b-476">adres URL Hello hello żądania.</span><span class="sxs-lookup"><span data-stu-id="1227b-476">hello URL of hello request.</span></span>|<span data-ttu-id="1227b-477">Jeśli nie trybu = kopiowania; tak, w przeciwnym razie wartość.</span><span class="sxs-lookup"><span data-stu-id="1227b-477">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="1227b-478">— Metoda</span><span class="sxs-lookup"><span data-stu-id="1227b-478">method</span></span>|<span data-ttu-id="1227b-479">Metoda HTTP dla żądania hello Hello.</span><span class="sxs-lookup"><span data-stu-id="1227b-479">hello HTTP method for hello request.</span></span>|<span data-ttu-id="1227b-480">Jeśli nie trybu = kopiowania; tak, w przeciwnym razie wartość.</span><span class="sxs-lookup"><span data-stu-id="1227b-480">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="1227b-481">nagłówek</span><span class="sxs-lookup"><span data-stu-id="1227b-481">header</span></span>|<span data-ttu-id="1227b-482">Nagłówek żądania.</span><span class="sxs-lookup"><span data-stu-id="1227b-482">Request header.</span></span> <span data-ttu-id="1227b-483">Użyj wielu elementów nagłówka dla wielu nagłówków żądania.</span><span class="sxs-lookup"><span data-stu-id="1227b-483">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="1227b-484">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-484">No</span></span>|  
|<span data-ttu-id="1227b-485">Treści</span><span class="sxs-lookup"><span data-stu-id="1227b-485">body</span></span>|<span data-ttu-id="1227b-486">Witaj treści żądania.</span><span class="sxs-lookup"><span data-stu-id="1227b-486">hello request body.</span></span>|<span data-ttu-id="1227b-487">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-487">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1227b-488">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="1227b-488">Attributes</span></span>  
  
|<span data-ttu-id="1227b-489">Atrybut</span><span class="sxs-lookup"><span data-stu-id="1227b-489">Attribute</span></span>|<span data-ttu-id="1227b-490">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-490">Description</span></span>|<span data-ttu-id="1227b-491">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-491">Required</span></span>|<span data-ttu-id="1227b-492">Domyślne</span><span class="sxs-lookup"><span data-stu-id="1227b-492">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="1227b-493">tryb = "string"</span><span class="sxs-lookup"><span data-stu-id="1227b-493">mode="string"</span></span>|<span data-ttu-id="1227b-494">Określa, czy jest to nowe żądanie lub kopię hello bieżącego żądania.</span><span class="sxs-lookup"><span data-stu-id="1227b-494">Determines whether this is a new request or a copy of hello current request.</span></span> <span data-ttu-id="1227b-495">W trybie wychodzących tryb = kopiowania nie inicjuje hello treści żądania.</span><span class="sxs-lookup"><span data-stu-id="1227b-495">In outbound mode, mode=copy does not initialize hello request body.</span></span>|<span data-ttu-id="1227b-496">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-496">No</span></span>|<span data-ttu-id="1227b-497">Nowy</span><span class="sxs-lookup"><span data-stu-id="1227b-497">New</span></span>|  
|<span data-ttu-id="1227b-498">Nazwa zmiennej odpowiedzi = "string"</span><span class="sxs-lookup"><span data-stu-id="1227b-498">response-variable-name="string"</span></span>|<span data-ttu-id="1227b-499">Jeśli nie istnieje `context.Response` jest używany.</span><span class="sxs-lookup"><span data-stu-id="1227b-499">If not present, `context.Response` is used.</span></span>|<span data-ttu-id="1227b-500">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-500">No</span></span>|<span data-ttu-id="1227b-501">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="1227b-501">N/A</span></span>|  
|<span data-ttu-id="1227b-502">limit czasu = "int"</span><span class="sxs-lookup"><span data-stu-id="1227b-502">timeout="integer"</span></span>|<span data-ttu-id="1227b-503">Witaj — interwał limitu czasu w sekundach przed wywołaniem hello toohello adres URL nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="1227b-503">hello timeout interval in seconds before hello call toohello URL fails.</span></span>|<span data-ttu-id="1227b-504">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-504">No</span></span>|<span data-ttu-id="1227b-505">60</span><span class="sxs-lookup"><span data-stu-id="1227b-505">60</span></span>|  
|<span data-ttu-id="1227b-506">Ignoruj błąd</span><span class="sxs-lookup"><span data-stu-id="1227b-506">ignore-error</span></span>|<span data-ttu-id="1227b-507">Jeśli true, a hello żądania powoduje błąd:</span><span class="sxs-lookup"><span data-stu-id="1227b-507">If true and hello request results in an error:</span></span><br /><br /> <span data-ttu-id="1227b-508">— Jeśli nazwa zmiennej odpowiedzi został określony, będzie zawierać wartości null.</span><span class="sxs-lookup"><span data-stu-id="1227b-508">-   If response-variable-name was specified it will contain a null value.</span></span><br /><span data-ttu-id="1227b-509">— Jeśli nie określono odpowiedzi zmienna nazwy, kontekstu. Żądanie nie zostanie zaktualizowany.</span><span class="sxs-lookup"><span data-stu-id="1227b-509">-   If response-variable-name was not specified, context.Request will not be updated.</span></span>|<span data-ttu-id="1227b-510">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-510">No</span></span>|<span data-ttu-id="1227b-511">wartość false</span><span class="sxs-lookup"><span data-stu-id="1227b-511">false</span></span>|  
|<span data-ttu-id="1227b-512">name</span><span class="sxs-lookup"><span data-stu-id="1227b-512">name</span></span>|<span data-ttu-id="1227b-513">Określa nazwę hello hello nagłówka toobe zestawu.</span><span class="sxs-lookup"><span data-stu-id="1227b-513">Specifies hello name of hello header toobe set.</span></span>|<span data-ttu-id="1227b-514">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-514">Yes</span></span>|<span data-ttu-id="1227b-515">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="1227b-515">N/A</span></span>|  
|<span data-ttu-id="1227b-516">istnieje akcja</span><span class="sxs-lookup"><span data-stu-id="1227b-516">exists-action</span></span>|<span data-ttu-id="1227b-517">Określa jaki tootake akcji, gdy nagłówek hello został już określony.</span><span class="sxs-lookup"><span data-stu-id="1227b-517">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="1227b-518">Ten atrybut musi mieć jedną z hello następujące wartości.</span><span class="sxs-lookup"><span data-stu-id="1227b-518">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="1227b-519">-- zastępuje hello wartość zastępczą hello istniejący nagłówek.</span><span class="sxs-lookup"><span data-stu-id="1227b-519">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="1227b-520">-skip — nie zastępuje istniejącą wartość nagłówka hello.</span><span class="sxs-lookup"><span data-stu-id="1227b-520">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="1227b-521">-dołączania - dołącza hello wartość toohello istniejącą wartość nagłówka.</span><span class="sxs-lookup"><span data-stu-id="1227b-521">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="1227b-522">-Usunięcie — usuwa hello nagłówek z żądania hello.</span><span class="sxs-lookup"><span data-stu-id="1227b-522">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="1227b-523">Gdy ustawiona zbyt`override` rejestrowanie wiele wpisów z hello sama nazwa wyniki w nagłówku hello jest zestaw zgodnie z tooall zapisów (które zostaną wyświetlone wiele razy); w wyniku hello zostanie ustawiona tylko wartości wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="1227b-523">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="1227b-524">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-524">No</span></span>|<span data-ttu-id="1227b-525">zastąpienie</span><span class="sxs-lookup"><span data-stu-id="1227b-525">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1227b-526">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="1227b-526">Usage</span></span>  
 <span data-ttu-id="1227b-527">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1227b-527">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1227b-528">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="1227b-528">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1227b-529">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="1227b-529">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="1227b-530"><a name="SetHttpProxy"></a>Serwer proxy HTTP zestawu</span><span class="sxs-lookup"><span data-stu-id="1227b-530"><a name="SetHttpProxy"></a> Set HTTP proxy</span></span>  
 <span data-ttu-id="1227b-531">Witaj `proxy` zasad umożliwia tooroute toobackends przekazywania żądań za pośrednictwem serwera proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="1227b-531">hello `proxy` policy allows you tooroute requests forwarded toobackends via an HTTP proxy.</span></span> <span data-ttu-id="1227b-532">HTTP (a nie HTTPS) jest obsługiwana między hello bramy i serwera proxy hello.</span><span class="sxs-lookup"><span data-stu-id="1227b-532">Only HTTP (not HTTPS) is supported between hello gateway and hello proxy.</span></span> <span data-ttu-id="1227b-533">Podstawowe i tylko z uwierzytelniania NTLM.</span><span class="sxs-lookup"><span data-stu-id="1227b-533">Basic and NTLM authentication only.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="1227b-534">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="1227b-534">Policy statement</span></span>  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="1227b-535">Przykład</span><span class="sxs-lookup"><span data-stu-id="1227b-535">Example</span></span>  
<span data-ttu-id="1227b-536">Należy zwrócić uwagę użycie hello [właściwości](api-management-howto-properties.md) jako wartości tooavoid nazwy użytkownika i hasła hello poufne informacje są przechowywane w dokumencie zasady hello.</span><span class="sxs-lookup"><span data-stu-id="1227b-536">Note hello use of [properties](api-management-howto-properties.md) as values of hello username and password tooavoid storing sensitive information in hello policy document.</span></span>  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a><span data-ttu-id="1227b-537">Elementy</span><span class="sxs-lookup"><span data-stu-id="1227b-537">Elements</span></span>  
  
|<span data-ttu-id="1227b-538">Element</span><span class="sxs-lookup"><span data-stu-id="1227b-538">Element</span></span>|<span data-ttu-id="1227b-539">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-539">Description</span></span>|<span data-ttu-id="1227b-540">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-540">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1227b-541">Serwer proxy</span><span class="sxs-lookup"><span data-stu-id="1227b-541">proxy</span></span>|<span data-ttu-id="1227b-542">Element główny</span><span class="sxs-lookup"><span data-stu-id="1227b-542">Root element</span></span>|<span data-ttu-id="1227b-543">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-543">Yes</span></span>|  

### <a name="attributes"></a><span data-ttu-id="1227b-544">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="1227b-544">Attributes</span></span>  
  
|<span data-ttu-id="1227b-545">Atrybut</span><span class="sxs-lookup"><span data-stu-id="1227b-545">Attribute</span></span>|<span data-ttu-id="1227b-546">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-546">Description</span></span>|<span data-ttu-id="1227b-547">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-547">Required</span></span>|<span data-ttu-id="1227b-548">Domyślne</span><span class="sxs-lookup"><span data-stu-id="1227b-548">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="1227b-549">adres URL = "string"</span><span class="sxs-lookup"><span data-stu-id="1227b-549">url="string"</span></span>|<span data-ttu-id="1227b-550">Adres URL serwera proxy w formie hello http://host:port.</span><span class="sxs-lookup"><span data-stu-id="1227b-550">Proxy URL in hello form of http://host:port.</span></span>|<span data-ttu-id="1227b-551">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-551">Yes</span></span>|<span data-ttu-id="1227b-552">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="1227b-552">N/A</span></span>|  
|<span data-ttu-id="1227b-553">Nazwa użytkownika = "string"</span><span class="sxs-lookup"><span data-stu-id="1227b-553">username="string"</span></span>|<span data-ttu-id="1227b-554">Używany do uwierzytelniania przy użyciu serwera proxy hello toobe nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1227b-554">Username toobe used for authentication with hello proxy.</span></span>|<span data-ttu-id="1227b-555">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-555">No</span></span>|<span data-ttu-id="1227b-556">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="1227b-556">N/A</span></span>|  
|<span data-ttu-id="1227b-557">hasło = "string"</span><span class="sxs-lookup"><span data-stu-id="1227b-557">password="string"</span></span>|<span data-ttu-id="1227b-558">Używany do uwierzytelniania przy użyciu serwera proxy hello toobe hasła.</span><span class="sxs-lookup"><span data-stu-id="1227b-558">Password toobe used for authentication with hello proxy.</span></span>|<span data-ttu-id="1227b-559">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-559">No</span></span>|<span data-ttu-id="1227b-560">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="1227b-560">N/A</span></span>|  

### <a name="usage"></a><span data-ttu-id="1227b-561">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="1227b-561">Usage</span></span>  
 <span data-ttu-id="1227b-562">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1227b-562">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1227b-563">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="1227b-563">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="1227b-564">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="1227b-564">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="1227b-565"><a name="SetRequestMethod"></a>Set, Metoda żądania</span><span class="sxs-lookup"><span data-stu-id="1227b-565"><a name="SetRequestMethod"></a> Set request method</span></span>  
 <span data-ttu-id="1227b-566">Witaj `set-method` zasad umożliwia toochange metoda żądania hello HTTP dla żądania.</span><span class="sxs-lookup"><span data-stu-id="1227b-566">hello `set-method` policy allows you toochange hello HTTP request method for a request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1227b-567">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="1227b-567">Policy statement</span></span>  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a><span data-ttu-id="1227b-568">Przykład</span><span class="sxs-lookup"><span data-stu-id="1227b-568">Example</span></span>  
 <span data-ttu-id="1227b-569">Przykładowe zasady używa hello `set-method` zasad przedstawiono przykład wysyłanie komunikatu tooa Slack pokoju rozmów, jeśli kod odpowiedzi HTTP hello jest większa niż lub równe too500.</span><span class="sxs-lookup"><span data-stu-id="1227b-569">This sample policy that uses hello `set-method` policy shows an example of sending a message tooa Slack chat room if hello HTTP response code is greater than or equal too500.</span></span> <span data-ttu-id="1227b-570">Aby uzyskać więcej informacji na ten przykład, zobacz [za pomocą usług zewnętrznych z usługi Azure API Management hello](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="1227b-570">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="1227b-571">Elementy</span><span class="sxs-lookup"><span data-stu-id="1227b-571">Elements</span></span>  
  
|<span data-ttu-id="1227b-572">Element</span><span class="sxs-lookup"><span data-stu-id="1227b-572">Element</span></span>|<span data-ttu-id="1227b-573">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-573">Description</span></span>|<span data-ttu-id="1227b-574">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-574">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1227b-575">set, metoda</span><span class="sxs-lookup"><span data-stu-id="1227b-575">set-method</span></span>|<span data-ttu-id="1227b-576">Element główny.</span><span class="sxs-lookup"><span data-stu-id="1227b-576">Root element.</span></span> <span data-ttu-id="1227b-577">wartość Hello elementu hello określa metodę HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="1227b-577">hello value of hello element specifies hello HTTP method.</span></span>|<span data-ttu-id="1227b-578">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-578">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1227b-579">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="1227b-579">Usage</span></span>  
 <span data-ttu-id="1227b-580">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1227b-580">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1227b-581">**Sekcje zasad:** dla ruchu przychodzącego, na błąd</span><span class="sxs-lookup"><span data-stu-id="1227b-581">**Policy sections:** inbound, on-error</span></span>  
  
-   <span data-ttu-id="1227b-582">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="1227b-582">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="1227b-583"><a name="SetStatus"></a>Kod stanu zestawu</span><span class="sxs-lookup"><span data-stu-id="1227b-583"><a name="SetStatus"></a> Set status code</span></span>  
 <span data-ttu-id="1227b-584">Witaj `set-status` zasad zestawy hello HTTP status kodu toohello określona wartość.</span><span class="sxs-lookup"><span data-stu-id="1227b-584">hello `set-status` policy sets hello HTTP status code toohello specified value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1227b-585">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="1227b-585">Policy statement</span></span>  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a><span data-ttu-id="1227b-586">Przykład</span><span class="sxs-lookup"><span data-stu-id="1227b-586">Example</span></span>  
 <span data-ttu-id="1227b-587">W tym przykładzie pokazano sposób tooreturn odpowiedzi 401, jeśli token autoryzacji hello jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="1227b-587">This example shows how tooreturn a 401 response if hello authorization token is invalid.</span></span> <span data-ttu-id="1227b-588">Aby uzyskać więcej informacji, zobacz [za pomocą usług zewnętrznych z hello usługi Zarządzanie interfejsami API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span><span class="sxs-lookup"><span data-stu-id="1227b-588">For more information, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span></span>  
  
```xml  
<choose>  
  <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
    <return-response response-variable-name="existing response variable">  
      <set-status code="401" reason="Unauthorized" />  
      <set-header name="WWW-Authenticate" exists-action="override">  
        <value>Bearer error="invalid_token"</value>  
      </set-header>  
    </return-response>  
  </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="1227b-589">Elementy</span><span class="sxs-lookup"><span data-stu-id="1227b-589">Elements</span></span>  
  
|<span data-ttu-id="1227b-590">Element</span><span class="sxs-lookup"><span data-stu-id="1227b-590">Element</span></span>|<span data-ttu-id="1227b-591">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-591">Description</span></span>|<span data-ttu-id="1227b-592">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-592">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1227b-593">Ustaw stan</span><span class="sxs-lookup"><span data-stu-id="1227b-593">set-status</span></span>|<span data-ttu-id="1227b-594">Element główny.</span><span class="sxs-lookup"><span data-stu-id="1227b-594">Root element.</span></span>|<span data-ttu-id="1227b-595">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-595">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1227b-596">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="1227b-596">Attributes</span></span>  
  
|<span data-ttu-id="1227b-597">Atrybut</span><span class="sxs-lookup"><span data-stu-id="1227b-597">Attribute</span></span>|<span data-ttu-id="1227b-598">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-598">Description</span></span>|<span data-ttu-id="1227b-599">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-599">Required</span></span>|<span data-ttu-id="1227b-600">Domyślne</span><span class="sxs-lookup"><span data-stu-id="1227b-600">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="1227b-601">Kod = "int"</span><span class="sxs-lookup"><span data-stu-id="1227b-601">code="integer"</span></span>|<span data-ttu-id="1227b-602">tooreturn kod stanu Hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="1227b-602">hello HTTP status code tooreturn.</span></span>|<span data-ttu-id="1227b-603">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-603">Yes</span></span>|<span data-ttu-id="1227b-604">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="1227b-604">N/A</span></span>|  
|<span data-ttu-id="1227b-605">Przyczyna = "string"</span><span class="sxs-lookup"><span data-stu-id="1227b-605">reason="string"</span></span>|<span data-ttu-id="1227b-606">Opis Przyczyna hello zwróciło kod stanu hello.</span><span class="sxs-lookup"><span data-stu-id="1227b-606">A description of hello reason for returning hello status code.</span></span>|<span data-ttu-id="1227b-607">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-607">Yes</span></span>|<span data-ttu-id="1227b-608">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="1227b-608">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1227b-609">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="1227b-609">Usage</span></span>  
 <span data-ttu-id="1227b-610">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1227b-610">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1227b-611">**Sekcje zasad:** wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="1227b-611">**Policy sections:** outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1227b-612">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="1227b-612">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="1227b-613"><a name="set-variable"></a>Ustaw zmienną</span><span class="sxs-lookup"><span data-stu-id="1227b-613"><a name="set-variable"></a> Set variable</span></span>  
 <span data-ttu-id="1227b-614">Witaj `set-variable` deklaruje zasad [kontekstu](api-management-policy-expressions.md#ContextVariables) zmiennej i przypisuje go za pośrednictwem określoną wartość [wyrażenie](api-management-policy-expressions.md) lub literałem ciągu.</span><span class="sxs-lookup"><span data-stu-id="1227b-614">hello `set-variable` policy declares a [context](api-management-policy-expressions.md#ContextVariables) variable and assigns it a value specified via an [expression](api-management-policy-expressions.md) or a string literal.</span></span> <span data-ttu-id="1227b-615">Jeśli wyrażenie hello zawiera właściwość literal, zostanie on przekonwertowany typ string i hello tooa hello wartości będzie `System.String`.</span><span class="sxs-lookup"><span data-stu-id="1227b-615">if hello expression contains a literal it will be converted tooa string and hello type of hello value will be `System.String`.</span></span>  
  
###  <span data-ttu-id="1227b-616"><a name="set-variablePolicyStatement"></a>Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="1227b-616"><a name="set-variablePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <span data-ttu-id="1227b-617"><a name="set-variableExample"></a>Przykład</span><span class="sxs-lookup"><span data-stu-id="1227b-617"><a name="set-variableExample"></a> Example</span></span>  
 <span data-ttu-id="1227b-618">Witaj poniższym przykładzie pokazano Ustaw zasady zmiennej w hello ruchu przychodzącego sekcji.</span><span class="sxs-lookup"><span data-stu-id="1227b-618">hello following example demonstrates a set variable policy in hello inbound section.</span></span> <span data-ttu-id="1227b-619">Ta zasada zmiennej zestaw tworzy `isMobile` logiczna [kontekstu](api-management-policy-expressions.md#ContextVariables) zmiennej, która ma wartość tootrue, jeśli hello `User-Agent` hello tekst zawiera nagłówek żądania `iPad` lub `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="1227b-619">This set variable policy creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set tootrue if hello `User-Agent` request header contains hello text `iPad` or `iPhone`.</span></span>  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a><span data-ttu-id="1227b-620">Elementy</span><span class="sxs-lookup"><span data-stu-id="1227b-620">Elements</span></span>  
  
|<span data-ttu-id="1227b-621">Element</span><span class="sxs-lookup"><span data-stu-id="1227b-621">Element</span></span>|<span data-ttu-id="1227b-622">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-622">Description</span></span>|<span data-ttu-id="1227b-623">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-623">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1227b-624">Ustaw zmienną</span><span class="sxs-lookup"><span data-stu-id="1227b-624">set-variable</span></span>|<span data-ttu-id="1227b-625">Element główny.</span><span class="sxs-lookup"><span data-stu-id="1227b-625">Root element.</span></span>|<span data-ttu-id="1227b-626">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-626">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1227b-627">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="1227b-627">Attributes</span></span>  
  
|<span data-ttu-id="1227b-628">Atrybut</span><span class="sxs-lookup"><span data-stu-id="1227b-628">Attribute</span></span>|<span data-ttu-id="1227b-629">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-629">Description</span></span>|<span data-ttu-id="1227b-630">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-630">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="1227b-631">name</span><span class="sxs-lookup"><span data-stu-id="1227b-631">name</span></span>|<span data-ttu-id="1227b-632">Nazwa Hello hello zmiennej.</span><span class="sxs-lookup"><span data-stu-id="1227b-632">hello name of hello variable.</span></span>|<span data-ttu-id="1227b-633">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-633">Yes</span></span>|  
|<span data-ttu-id="1227b-634">wartość</span><span class="sxs-lookup"><span data-stu-id="1227b-634">value</span></span>|<span data-ttu-id="1227b-635">wartość Hello hello zmiennej.</span><span class="sxs-lookup"><span data-stu-id="1227b-635">hello value of hello variable.</span></span> <span data-ttu-id="1227b-636">Może to być wyrażenie lub ciągiem literałowym.</span><span class="sxs-lookup"><span data-stu-id="1227b-636">This can be an expression or a literal value.</span></span>|<span data-ttu-id="1227b-637">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-637">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1227b-638">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="1227b-638">Usage</span></span>  
 <span data-ttu-id="1227b-639">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1227b-639">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1227b-640">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="1227b-640">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1227b-641">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="1227b-641">**Policy scopes:** all scopes</span></span>  
  
###  <span data-ttu-id="1227b-642"><a name="set-variableAllowedTypes"></a>Dozwolonymi typami</span><span class="sxs-lookup"><span data-stu-id="1227b-642"><a name="set-variableAllowedTypes"></a> Allowed types</span></span>  
 <span data-ttu-id="1227b-643">Wyrażenia używane w hello `set-variable` zasad musi zwracać jedną z hello następujące typy podstawowe.</span><span class="sxs-lookup"><span data-stu-id="1227b-643">Expressions used in hello `set-variable` policy must return one of hello following basic types.</span></span>  
  
-   <span data-ttu-id="1227b-644">System.Boolean</span><span class="sxs-lookup"><span data-stu-id="1227b-644">System.Boolean</span></span>  
  
-   <span data-ttu-id="1227b-645">System.SByte</span><span class="sxs-lookup"><span data-stu-id="1227b-645">System.SByte</span></span>  
  
-   <span data-ttu-id="1227b-646">System.Byte</span><span class="sxs-lookup"><span data-stu-id="1227b-646">System.Byte</span></span>  
  
-   <span data-ttu-id="1227b-647">System.UInt16</span><span class="sxs-lookup"><span data-stu-id="1227b-647">System.UInt16</span></span>  
  
-   <span data-ttu-id="1227b-648">System.UInt32</span><span class="sxs-lookup"><span data-stu-id="1227b-648">System.UInt32</span></span>  
  
-   <span data-ttu-id="1227b-649">System.UInt64</span><span class="sxs-lookup"><span data-stu-id="1227b-649">System.UInt64</span></span>  
  
-   <span data-ttu-id="1227b-650">System.Int16</span><span class="sxs-lookup"><span data-stu-id="1227b-650">System.Int16</span></span>  
  
-   <span data-ttu-id="1227b-651">System.Int32</span><span class="sxs-lookup"><span data-stu-id="1227b-651">System.Int32</span></span>  
  
-   <span data-ttu-id="1227b-652">System.Int64</span><span class="sxs-lookup"><span data-stu-id="1227b-652">System.Int64</span></span>  
  
-   <span data-ttu-id="1227b-653">System.Decimal</span><span class="sxs-lookup"><span data-stu-id="1227b-653">System.Decimal</span></span>  
  
-   <span data-ttu-id="1227b-654">System.Single</span><span class="sxs-lookup"><span data-stu-id="1227b-654">System.Single</span></span>  
  
-   <span data-ttu-id="1227b-655">System.Double</span><span class="sxs-lookup"><span data-stu-id="1227b-655">System.Double</span></span>  
  
-   <span data-ttu-id="1227b-656">System.Guid</span><span class="sxs-lookup"><span data-stu-id="1227b-656">System.Guid</span></span>  
  
-   <span data-ttu-id="1227b-657">System.String</span><span class="sxs-lookup"><span data-stu-id="1227b-657">System.String</span></span>  
  
-   <span data-ttu-id="1227b-658">System.Char</span><span class="sxs-lookup"><span data-stu-id="1227b-658">System.Char</span></span>  
  
-   <span data-ttu-id="1227b-659">System.DateTime</span><span class="sxs-lookup"><span data-stu-id="1227b-659">System.DateTime</span></span>  
  
-   <span data-ttu-id="1227b-660">Obiekt System.TimeSpan</span><span class="sxs-lookup"><span data-stu-id="1227b-660">System.TimeSpan</span></span>  
  
-   <span data-ttu-id="1227b-661">System.Byte?</span><span class="sxs-lookup"><span data-stu-id="1227b-661">System.Byte?</span></span>  
  
-   <span data-ttu-id="1227b-662">System.UInt16?</span><span class="sxs-lookup"><span data-stu-id="1227b-662">System.UInt16?</span></span>  
  
-   <span data-ttu-id="1227b-663">System.UInt32?</span><span class="sxs-lookup"><span data-stu-id="1227b-663">System.UInt32?</span></span>  
  
-   <span data-ttu-id="1227b-664">System.UInt64?</span><span class="sxs-lookup"><span data-stu-id="1227b-664">System.UInt64?</span></span>  
  
-   <span data-ttu-id="1227b-665">System.Int16?</span><span class="sxs-lookup"><span data-stu-id="1227b-665">System.Int16?</span></span>  
  
-   <span data-ttu-id="1227b-666">System.Int32?</span><span class="sxs-lookup"><span data-stu-id="1227b-666">System.Int32?</span></span>  
  
-   <span data-ttu-id="1227b-667">System.Int64?</span><span class="sxs-lookup"><span data-stu-id="1227b-667">System.Int64?</span></span>  
  
-   <span data-ttu-id="1227b-668">System.Decimal?</span><span class="sxs-lookup"><span data-stu-id="1227b-668">System.Decimal?</span></span>  
  
-   <span data-ttu-id="1227b-669">System.Single?</span><span class="sxs-lookup"><span data-stu-id="1227b-669">System.Single?</span></span>  
  
-   <span data-ttu-id="1227b-670">System.Double?</span><span class="sxs-lookup"><span data-stu-id="1227b-670">System.Double?</span></span>  
  
-   <span data-ttu-id="1227b-671">System.Guid?</span><span class="sxs-lookup"><span data-stu-id="1227b-671">System.Guid?</span></span>  
  
-   <span data-ttu-id="1227b-672">System.String?</span><span class="sxs-lookup"><span data-stu-id="1227b-672">System.String?</span></span>  
  
-   <span data-ttu-id="1227b-673">System.Char?</span><span class="sxs-lookup"><span data-stu-id="1227b-673">System.Char?</span></span>  
  
-   <span data-ttu-id="1227b-674">System.DateTime?</span><span class="sxs-lookup"><span data-stu-id="1227b-674">System.DateTime?</span></span>  

##  <span data-ttu-id="1227b-675"><a name="Trace"></a>Śledzenia</span><span class="sxs-lookup"><span data-stu-id="1227b-675"><a name="Trace"></a> Trace</span></span>  
 <span data-ttu-id="1227b-676">Witaj `trace` zasad dodaje ciąg do hello [inspektora interfejsu API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="1227b-676">hello             `trace` policy adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span> <span data-ttu-id="1227b-677">Witaj zasad będą wykonywane tylko gdy śledzenie jest wyzwalane, tj. `Ocp-Apim-Trace` nagłówek żądania jest obecny i ustaw zbyt`true` i `Ocp-Apim-Subscription-Key` nagłówek żądania jest obecny i ma prawidłowy klucz skojarzony z kontem administratora hello.</span><span class="sxs-lookup"><span data-stu-id="1227b-677">hello policy will execute only when tracing is triggered, i.e. `Ocp-Apim-Trace` request header is present and set too`true` and `Ocp-Apim-Subscription-Key` request header is present and holds a valid key associated with hello admin account.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1227b-678">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="1227b-678">Policy statement</span></span>  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="1227b-679">Elementy</span><span class="sxs-lookup"><span data-stu-id="1227b-679">Elements</span></span>  
  
|<span data-ttu-id="1227b-680">Element</span><span class="sxs-lookup"><span data-stu-id="1227b-680">Element</span></span>|<span data-ttu-id="1227b-681">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-681">Description</span></span>|<span data-ttu-id="1227b-682">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-682">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1227b-683">śledzenia</span><span class="sxs-lookup"><span data-stu-id="1227b-683">trace</span></span>|<span data-ttu-id="1227b-684">Element główny.</span><span class="sxs-lookup"><span data-stu-id="1227b-684">Root element.</span></span>|<span data-ttu-id="1227b-685">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-685">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1227b-686">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="1227b-686">Attributes</span></span>  
  
|<span data-ttu-id="1227b-687">Atrybut</span><span class="sxs-lookup"><span data-stu-id="1227b-687">Attribute</span></span>|<span data-ttu-id="1227b-688">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-688">Description</span></span>|<span data-ttu-id="1227b-689">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-689">Required</span></span>|<span data-ttu-id="1227b-690">Domyślne</span><span class="sxs-lookup"><span data-stu-id="1227b-690">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="1227b-691">Źródło</span><span class="sxs-lookup"><span data-stu-id="1227b-691">source</span></span>|<span data-ttu-id="1227b-692">Przeglądarka śledzenia toohello znaczący literału ciągu i Określanie źródła hello wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="1227b-692">String literal meaningful toohello trace viewer and specifying hello source of hello message.</span></span>|<span data-ttu-id="1227b-693">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-693">Yes</span></span>|<span data-ttu-id="1227b-694">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="1227b-694">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1227b-695">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="1227b-695">Usage</span></span>  
 <span data-ttu-id="1227b-696">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="1227b-696">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="1227b-697">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="1227b-697">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1227b-698">**Zakresy zasad:** wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="1227b-698">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="1227b-699"><a name="Wait"></a>Oczekiwania</span><span class="sxs-lookup"><span data-stu-id="1227b-699"><a name="Wait"></a> Wait</span></span>  
 <span data-ttu-id="1227b-700">Witaj `wait` zasad wykonuje jego zasadami bezpośrednio podrzędne równolegle i czeka na wszystkich lub jednego z jego toocomplete zasad bezpośrednio podrzędne przed zakończeniem działania.</span><span class="sxs-lookup"><span data-stu-id="1227b-700">hello `wait` policy executes its immediate child policies in parallel, and waits for either all or one of its immediate child policies toocomplete before it completes.</span></span> <span data-ttu-id="1227b-701">Hello oczekiwania zasad może mieć jako jego zasadami bezpośrednio podrzędne [żądanie wysłania](api-management-advanced-policies.md#SendRequest), [pobrać wartości z pamięci podręcznej](api-management-caching-policies.md#GetFromCacheByKey), i [sterowania przepływem](api-management-advanced-policies.md#choose) zasad.</span><span class="sxs-lookup"><span data-stu-id="1227b-701">hello wait policy can have as its immediate child policies [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), and [Control flow](api-management-advanced-policies.md#choose) policies.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1227b-702">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="1227b-702">Policy statement</span></span>  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a><span data-ttu-id="1227b-703">Przykład</span><span class="sxs-lookup"><span data-stu-id="1227b-703">Example</span></span>  
 <span data-ttu-id="1227b-704">W hello poniższy przykład występują dwa `choose` zasad jako zasady bezpośrednio podrzędne hello `wait` zasad.</span><span class="sxs-lookup"><span data-stu-id="1227b-704">In hello following example there are two `choose` policies as immediate child policies of hello `wait` policy.</span></span> <span data-ttu-id="1227b-705">Każdy z tych `choose` zasad wykonywane równolegle.</span><span class="sxs-lookup"><span data-stu-id="1227b-705">Each of these `choose` policies executes in parallel.</span></span> <span data-ttu-id="1227b-706">Każdy `choose` zasad prób tooretrieve wartość w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="1227b-706">Each `choose` policy attempts tooretrieve a cached value.</span></span> <span data-ttu-id="1227b-707">W przypadku Chybienie pamięci podręcznej usługi wewnętrznej bazy danych jest nazywany tooprovide hello wartość.</span><span class="sxs-lookup"><span data-stu-id="1227b-707">If there is a cache miss, a backend service is called tooprovide hello value.</span></span> <span data-ttu-id="1227b-708">W tym hello przykład `wait` zasad nie zostanie zakończone do czasu ukończenia wszystkich swoich zasad bezpośrednio podrzędne, ponieważ hello `for` zbyt ustawiono atrybut`all`.</span><span class="sxs-lookup"><span data-stu-id="1227b-708">In this example hello `wait` policy does not complete until all of its immediate child policies complete, because hello `for` attribute is set too`all`.</span></span>   <span data-ttu-id="1227b-709">W tym przykład hello kontekstu zmiennych (`execute-branch-one`, `value-one`, `execute-branch-two`, i `value-two`) są deklarowane jako poza zakres hello ten przykład zasad.</span><span class="sxs-lookup"><span data-stu-id="1227b-709">In this example hello context variables (`execute-branch-one`, `value-one`, `execute-branch-two`, and `value-two`) are declared outside of hello scope of this example policy.</span></span>  
  
```xml  
<wait for="all">  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-one="])">  
      <cache-lookup-value key="key-one" variable-name="value-one" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-one="))">  
          <send-request mode="new" response-variable-name="value-one">  
            <set-url>https://backend-one</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-two="])">  
      <cache-lookup-value key="key-two" variable-name="value-two" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-two="))">  
          <send-request mode="new" response-variable-name="value-two">  
            <set-url>https://backend-two</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
</wait>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="1227b-710">Elementy</span><span class="sxs-lookup"><span data-stu-id="1227b-710">Elements</span></span>  
  
|<span data-ttu-id="1227b-711">Element</span><span class="sxs-lookup"><span data-stu-id="1227b-711">Element</span></span>|<span data-ttu-id="1227b-712">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-712">Description</span></span>|<span data-ttu-id="1227b-713">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-713">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1227b-714">oczekiwania</span><span class="sxs-lookup"><span data-stu-id="1227b-714">wait</span></span>|<span data-ttu-id="1227b-715">Element główny.</span><span class="sxs-lookup"><span data-stu-id="1227b-715">Root element.</span></span> <span data-ttu-id="1227b-716">Może zawierać jako elementy podrzędne tylko `send-request`, `cache-lookup-value`, i `choose` zasad.</span><span class="sxs-lookup"><span data-stu-id="1227b-716">May contain as child elements only `send-request`, `cache-lookup-value`, and `choose` policies.</span></span>|<span data-ttu-id="1227b-717">Tak</span><span class="sxs-lookup"><span data-stu-id="1227b-717">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1227b-718">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="1227b-718">Attributes</span></span>  
  
|<span data-ttu-id="1227b-719">Atrybut</span><span class="sxs-lookup"><span data-stu-id="1227b-719">Attribute</span></span>|<span data-ttu-id="1227b-720">Opis</span><span class="sxs-lookup"><span data-stu-id="1227b-720">Description</span></span>|<span data-ttu-id="1227b-721">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1227b-721">Required</span></span>|<span data-ttu-id="1227b-722">Domyślne</span><span class="sxs-lookup"><span data-stu-id="1227b-722">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="1227b-723">dla</span><span class="sxs-lookup"><span data-stu-id="1227b-723">for</span></span>|<span data-ttu-id="1227b-724">Określa, czy hello `wait` zasad czeka na wszystkich toobe zasad bezpośrednio podrzędne ukończona lub jest tylko jeden.</span><span class="sxs-lookup"><span data-stu-id="1227b-724">Determines whether hello `wait` policy waits for all immediate child policies toobe completed or just one.</span></span> <span data-ttu-id="1227b-725">Dozwolone wartości to:</span><span class="sxs-lookup"><span data-stu-id="1227b-725">Allowed values are:</span></span><br /><br /> <span data-ttu-id="1227b-726">-   `all`-Poczekaj, aż wszystkie toocomplete zasad bezpośrednio podrzędne</span><span class="sxs-lookup"><span data-stu-id="1227b-726">-   `all` - wait for all immediate child policies toocomplete</span></span><br /><span data-ttu-id="1227b-727">-żadnego - poczekaj, aż wszystkie toocomplete zasad bezpośrednio podrzędne.</span><span class="sxs-lookup"><span data-stu-id="1227b-727">-   any - wait for any immediate child policy toocomplete.</span></span> <span data-ttu-id="1227b-728">Po zakończeniu pierwszej zasady bezpośrednio podrzędne hello hello `wait` kończy zasad i wykonywania innych zasad bezpośrednio podrzędne zostanie zakończony.</span><span class="sxs-lookup"><span data-stu-id="1227b-728">Once hello first immediate child policy has completed, hello `wait` policy completes and execution of any other immediate child policies is terminated.</span></span>|<span data-ttu-id="1227b-729">Nie</span><span class="sxs-lookup"><span data-stu-id="1227b-729">No</span></span>|<span data-ttu-id="1227b-730">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="1227b-730">all</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1227b-731">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="1227b-731">Usage</span></span>  
 <span data-ttu-id="1227b-732">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1227b-732">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1227b-733">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="1227b-733">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="1227b-734">**Zakresy zasad:**wszystkich zakresów</span><span class="sxs-lookup"><span data-stu-id="1227b-734">**Policy scopes:**all scopes</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="1227b-735">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1227b-735">Next steps</span></span>
<span data-ttu-id="1227b-736">Aby uzyskać więcej informacji, Praca z zasad Zobacz:</span><span class="sxs-lookup"><span data-stu-id="1227b-736">For more information working with policies, see:</span></span>
-   [<span data-ttu-id="1227b-737">Zasady w usłudze API Management</span><span class="sxs-lookup"><span data-stu-id="1227b-737">Policies in API Management</span></span>](api-management-howto-policies.md) 
-   [<span data-ttu-id="1227b-738">Wyrażenia zasad</span><span class="sxs-lookup"><span data-stu-id="1227b-738">Policy expressions</span></span>](api-management-policy-expressions.md)
