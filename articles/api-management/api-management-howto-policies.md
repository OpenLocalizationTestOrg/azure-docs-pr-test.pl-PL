---
title: "aaaPolicies w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate, edytować i konfigurowania zasad w usłudze API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 537e5caf-708b-430e-a83f-72b70af28aa9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 9ab0f884a655004cb10c05085034df1795f512e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="policies-in-azure-api-management"></a><span data-ttu-id="a8e4d-103">Zasady w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="a8e4d-103">Policies in Azure API Management</span></span>
<span data-ttu-id="a8e4d-104">W usłudze Azure API Management zasady są zaawansowanych możliwości hello system, który umożliwia zachowanie hello toochange hello interfejsu API za pomocą konfiguracji hello wydawcy.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-104">In Azure API Management, policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="a8e4d-105">Zasady są zbiór instrukcji, które są wykonywane sekwencyjnie na powitania żądania lub odpowiedzi interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-105">Policies are a collection of Statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="a8e4d-106">Popularne instrukcje obejmują Konwersja formatu XML tooJSON i Wywołaj tempa ograniczania toorestrict hello ilość przychodzących od dewelopera.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-106">Popular Statements include format conversion from XML tooJSON and call rate limiting toorestrict hello amount of incoming calls from a developer.</span></span> <span data-ttu-id="a8e4d-107">Wiele zasad są dostępne fabrycznej hello.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-107">Many more policies are available out of hello box.</span></span>

<span data-ttu-id="a8e4d-108">Zobacz hello [informacje o zasadach] [ Policy Reference] pełną listę deklaracji zasad i ich ustawienia.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-108">See hello [Policy Reference][Policy Reference] for a full list of policy statements and their settings.</span></span>

<span data-ttu-id="a8e4d-109">Zasady są stosowane wewnątrz hello bramy, która znajduje się pomiędzy powitania klienta interfejsu API i hello zarządzanego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-109">Policies are applied inside hello gateway which sits between hello API consumer and hello managed API.</span></span> <span data-ttu-id="a8e4d-110">Hello Brama odbiera wszystkie żądania i zwykle przekazuje je niezmieniony toohello podstawowy interfejs API.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-110">hello gateway receives all requests and usually forwards them unaltered toohello underlying API.</span></span> <span data-ttu-id="a8e4d-111">Jednak zasady można zastosować zmian tooboth hello przychodzącego żądania i odpowiedzi wychodzących.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-111">However a policy can apply changes tooboth hello inbound request and outbound response.</span></span>

<span data-ttu-id="a8e4d-112">Wyrażenie zasad może służyć jako wartości atrybutu lub tekst w żadnym z zasad interfejsu API zarządzania hello, chyba że zasady hello Określa, w przeciwnym razie wartość.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-112">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="a8e4d-113">Niektóre zasady, takie jak hello [sterowania przepływem] [ Control flow] i [zmiennej zestaw] [ Set variable] zasady są oparte na wyrażeniach zasad.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-113">Some policies such as hello [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="a8e4d-114">Aby uzyskać więcej informacji, zobacz [zaawansowane zasady] [ Advanced policies] i [wyrażenie zasad][Policy expressions].</span><span class="sxs-lookup"><span data-stu-id="a8e4d-114">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions].</span></span>

## <span data-ttu-id="a8e4d-115"><a name="scopes"></a>Jak tooconfigure zasad</span><span class="sxs-lookup"><span data-stu-id="a8e4d-115"><a name="scopes"> </a>How tooconfigure policies</span></span>
<span data-ttu-id="a8e4d-116">Zasady można skonfigurować globalnie lub w zakresie hello [produktu][Product], [interfejsu API] [ API] lub [operacji] [Operation].</span><span class="sxs-lookup"><span data-stu-id="a8e4d-116">Policies can be configured globally or at hello scope of a [Product][Product], [API][API] or [Operation][Operation].</span></span> <span data-ttu-id="a8e4d-117">tooconfigure zasadę, przejdź toohello edytora zasad w portalu wydawcy hello.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-117">tooconfigure a policy, navigate toohello Policies editor in hello publisher portal.</span></span>

![Menu zasad][policies-menu]

<span data-ttu-id="a8e4d-119">Edytor zasad Hello składa się z trzech głównych sekcji: hello zasad zakresu (z góry), hello definicji zasad gdzie edycji zasad (lewych) i instrukcje hello listy (po prawej):</span><span class="sxs-lookup"><span data-stu-id="a8e4d-119">hello policies editor consists of three main sections: hello policy scope (top), hello policy definition where policies are edited (left) and hello statements list (right):</span></span>

![Edytor zasad][policies-editor]

<span data-ttu-id="a8e4d-121">toobegin Konfigurowanie zasad, musisz najpierw wybrać zakres hello na powitania, które mają dotyczyć zasady.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-121">toobegin configuring a policy you must first select hello scope at which hello policy should apply.</span></span> <span data-ttu-id="a8e4d-122">Zrzucie ekranu hello poniżej hello **Starter** produkt jest zaznaczony.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-122">In hello screenshot below hello **Starter** product is selected.</span></span> <span data-ttu-id="a8e4d-123">Należy pamiętać, że w tym hello kwadratowy dalej toohello zasad nazwa symbolu wskazuje, że zasady jest już stosowane na tym poziomie.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-123">Note that hello square symbol next toohello policy name indicates that a policy is already applied at this level.</span></span>

![Zakres][policies-scope]

<span data-ttu-id="a8e4d-125">Ponieważ zasady zostały już zastosowane, konfiguracja hello jest wyświetlana w widoku definicji hello.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-125">Since a policy has already been applied, hello configuration is shown in hello definition view.</span></span>

![Konfigurowanie][policies-configure]

<span data-ttu-id="a8e4d-127">zasady Hello są wyświetlane tylko do odczytu na początku.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-127">hello policy is displayed read-only at first.</span></span> <span data-ttu-id="a8e4d-128">W kolejności tooedit definicji powitania kliknij hello **Konfiguruj zasady** akcji.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-128">In order tooedit hello definition click hello **Configure Policy** action.</span></span>

![Edytuj][policies-edit]

<span data-ttu-id="a8e4d-130">Definicja zasad Hello jest proste dokument XML, który opisuje sekwencji instrukcji dla ruchu przychodzącego i wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-130">hello policy definition is a simple XML document that describes a sequence of inbound and outbound statements.</span></span> <span data-ttu-id="a8e4d-131">Witaj XML można edytować bezpośrednio w oknie definicji hello.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-131">hello XML can be edited directly in hello definition window.</span></span> <span data-ttu-id="a8e4d-132">Lista instrukcje są podane toohello prawo i bieżącego zakresu toohello odpowiednie instrukcje są włączone i wyróżniony; jak dowodzą hello **Limit szybkości wywołać** instrukcji na powitania zrzucie ekranu pokazano powyżej.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-132">A list of statements is provided toohello right and statements applicable toohello current scope are enabled and highlighted; as demonstrated by hello **Limit Call Rate** statement in hello screenshot above.</span></span>

<span data-ttu-id="a8e4d-133">Kliknięcie instrukcji włączone spowoduje dodanie hello odpowiednie XML w lokalizacji hello hello kursora w hello definicji widoku.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-133">Clicking an enabled statement will add hello appropriate XML at hello location of hello cursor in hello definition view.</span></span> 

> [!NOTE]
> <span data-ttu-id="a8e4d-134">Hello zasad, które mają tooadd nie jest włączona, upewnij się, że jesteś w hello poprawny zakres dla tej zasady.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-134">If hello policy that you want tooadd is not enabled, ensure that you are in hello correct scope for that policy.</span></span> <span data-ttu-id="a8e4d-135">Każda instrukcja zasad jest przeznaczony do użytku w określonych zakresach i sekcje zasad.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-135">Each policy statement is designed for use in certain scopes and policy sections.</span></span> <span data-ttu-id="a8e4d-136">sekcje zasad hello tooreview i zakresy dla zasady, sprawdź hello **użycia** sekcji dla tej zasady w hello [informacje o zasadach][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="a8e4d-136">tooreview hello policy sections and scopes for a policy, check hello **Usage** section for that policy in hello [Policy Reference][Policy Reference].</span></span>
> 
> 

<span data-ttu-id="a8e4d-137">Pełna lista deklaracji zasad i ich ustawienia są dostępne w hello [informacje o zasadach][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="a8e4d-137">A full list of policy statements and their settings are available in hello [Policy Reference][Policy Reference].</span></span>

<span data-ttu-id="a8e4d-138">Na przykład tooadd nowe toorestrict instrukcji przychodzących żądań toospecified adresów IP, umieść kursor hello wewnątrz zawartości hello hello `inbound` XML hello element i kliknij przycisk **wywołującego Ogranicz adresów IP** instrukcji.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-138">For example, tooadd a new statement toorestrict incoming requests toospecified IP addresses, place hello cursor just inside hello content of hello `inbound` XML element and click hello **Restrict caller IPs** statement.</span></span>

![Zasady ograniczeń][policies-restrict]

<span data-ttu-id="a8e4d-140">Spowoduje to dodanie toohello fragment kodu XML `inbound` element, który zawiera wskazówki dotyczące sposobu tooconfigure hello instrukcji.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-140">This will add an XML snippet toohello `inbound` element that provides guidance on how tooconfigure hello statement.</span></span>

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

<span data-ttu-id="a8e4d-141">toolimit ruchu przychodzącego żądania i zaakceptować tylko te z adresu IP 1.2.3.4 zmodyfikować hello XML w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a8e4d-141">toolimit inbound requests and accept only those from an IP address of 1.2.3.4 modify hello XML as follows:</span></span>

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Zapisz][policies-save]

<span data-ttu-id="a8e4d-143">Po zakończeniu konfigurowania instrukcje hello hello zasad, kliknij przycisk **zapisać** i hello zmiany zostaną propagowany toohello interfejsu API zarządzania bramy natychmiast.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-143">When complete configuring hello statements for hello policy, click **Save** and hello changes will be propagated toohello API Management gateway immediately.</span></span>

## <span data-ttu-id="a8e4d-144"><a name="sections"></a>Opis zasad konfiguracji</span><span class="sxs-lookup"><span data-stu-id="a8e4d-144"><a name="sections"> </a>Understanding policy configuration</span></span>
<span data-ttu-id="a8e4d-145">Zasady zostaną serię instrukcji, które są wykonywane w kolejności na żądania i odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-145">A policy is a series of statements that execute in order for a request and a response.</span></span> <span data-ttu-id="a8e4d-146">Konfiguracja Hello jest odpowiednio podzielone na `inbound`, `backend`, `outbound`, i `on-error` sekcjach przedstawiono, jak pokazano w powitania po konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-146">hello configuration is divided appropriately into `inbound`, `backend`, `outbound`, and `on-error` sections as shown in hello following configuration.</span></span>

```xml
<policies>
  <inbound>
    <!-- statements toobe applied toohello request go here -->
  </inbound>
  <backend>
    <!-- statements toobe applied before hello request is forwarded too
         hello backend service go here -->
  </backend>
  <outbound>
    <!-- statements toobe applied toohello response go here -->
  </outbound>
  <on-error>
    <!-- statements toobe applied if there is an error condition go here -->
  </on-error>
</policies> 
```

<span data-ttu-id="a8e4d-147">Jeśli występuje błąd podczas przetwarzania żądania hello, wszystkie pozostałe kroki w hello `inbound`, `backend`, lub `outbound` sekcje są pomijane i wykonywania w tę łódź toohello instrukcje w hello `on-error` sekcji.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-147">If there is an error during hello processing of a request, any remaining steps in hello `inbound`, `backend`, or `outbound` sections are skipped and execution jumps toohello statements in hello `on-error` section.</span></span> <span data-ttu-id="a8e4d-148">Zaznaczając deklaracji zasad hello `on-error` sekcji można przejrzeć hello błędu przy użyciu hello `context.LastError` właściwość, sprawdzić i dostosować przy użyciu hello odpowiedzi na błąd hello `set-body` zasad i skonfigurować, co się stanie w przypadku wystąpienia błędu.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-148">By placing policy statements in hello `on-error` section you can review hello error by using hello `context.LastError` property, inspect and customize hello error response using hello `set-body` policy, and configure what happens if an error occurs.</span></span> <span data-ttu-id="a8e4d-149">Brak kody błędów dla wbudowanych kroków i błędy, które mogą wystąpić podczas przetwarzania hello deklaracji zasad.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-149">There are error codes for built-in steps and for errors that may occur during hello processing of policy statements.</span></span> <span data-ttu-id="a8e4d-150">Aby uzyskać więcej informacji, zobacz [obsługi błędów w zasad interfejsu API zarządzania](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8e4d-150">For more information, see [Error handling in API Management policies](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span></span>

<span data-ttu-id="a8e4d-151">Ponieważ zasad można określić na różnych poziomach (globalne, produktu, interfejsu api i operacji) hello konfiguracji umożliwia dla Ciebie toospecify hello kolejność, w którym instrukcje definicji zasad hello wykonywane za pomocą zasad nadrzędnej toohello względem.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-151">Since policies can be specified at different levels (global, product, api and operation) hello configuration provides a way for you toospecify hello order in which hello policy definition's statements execute with respect toohello parent policy.</span></span> 

<span data-ttu-id="a8e4d-152">Zakresy zasad są oceniane w następującej kolejności hello.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-152">Policy scopes are evaluated in hello following order.</span></span>

1. <span data-ttu-id="a8e4d-153">Globalne</span><span class="sxs-lookup"><span data-stu-id="a8e4d-153">Global scope</span></span>
2. <span data-ttu-id="a8e4d-154">Zakres produktu</span><span class="sxs-lookup"><span data-stu-id="a8e4d-154">Product scope</span></span>
3. <span data-ttu-id="a8e4d-155">Zakres interfejsu API</span><span class="sxs-lookup"><span data-stu-id="a8e4d-155">API scope</span></span>
4. <span data-ttu-id="a8e4d-156">Operacja zakresu</span><span class="sxs-lookup"><span data-stu-id="a8e4d-156">Operation scope</span></span>

<span data-ttu-id="a8e4d-157">Witaj instrukcje w nich są oceniane według położenia toohello hello `base` elementu, jeśli jest obecny.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-157">hello statements within them are evaluated according toohello placement of hello `base` element, if it is present.</span></span> <span data-ttu-id="a8e4d-158">Globalne zasady ma żadnych zasad nadrzędny i przy użyciu hello `<base>` element w nim nie ma wpływu.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-158">Global policy has no parent policy and using hello `<base>` element in it has no effect.</span></span>

<span data-ttu-id="a8e4d-159">Na przykład jeśli masz zasady na poziomie globalnym hello i zasady skonfigurowane dla interfejsu API, następnie każdorazowe użycie tego konkretnego interfejsu API obie zasady zostaną zastosowane.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-159">For example, if you have a policy at hello global level and a policy configured for an API, then whenever that particular API is used both policies will be applied.</span></span> <span data-ttu-id="a8e4d-160">Zarządzanie interfejsami API umożliwia deterministyczne kolejność deklaracji zasad połączonych za pośrednictwem hello base element.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-160">API Management allows for deterministic ordering of combined policy statements via hello base element.</span></span> 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

<span data-ttu-id="a8e4d-161">W hello przykład definicji zasad powyżej, hello `cross-domain` instrukcji jest wykonywany przed wszystkie wyższej zasady, które z kolei, następować hello `find-and-replace` zasad.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-161">In hello example policy definition above, hello `cross-domain` statement would execute before any higher policies which would in turn, be followed by hello `find-and-replace` policy.</span></span> 

<span data-ttu-id="a8e4d-162">zasady hello toosee w bieżącym zakresie hello w edytorze zasad hello, kliknij polecenie **ponownie Oblicz skutecznych zasad dla wybranego zakresu**.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-162">toosee hello policies in hello current scope in hello policy editor, click **Recalculate effective policy for selected scope**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8e4d-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a8e4d-163">Next steps</span></span>
<span data-ttu-id="a8e4d-164">Zapoznaj się z następującego wideo na wyrażeniach zasad.</span><span class="sxs-lookup"><span data-stu-id="a8e4d-164">Check out following video on policy expressions.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Policy Reference]: api-management-policy-reference.md
[Product]: api-management-howto-add-products.md
[API]: api-management-howto-add-products.md#add-apis 
[Operation]: api-management-howto-add-operations.md

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx

[policies-menu]: ./media/api-management-howto-policies/api-management-policies-menu.png
[policies-editor]: ./media/api-management-howto-policies/api-management-policies-editor.png
[policies-scope]: ./media/api-management-howto-policies/api-management-policies-scope.png
[policies-configure]: ./media/api-management-howto-policies/api-management-policies-configure.png
[policies-edit]: ./media/api-management-howto-policies/api-management-policies-edit.png
[policies-restrict]: ./media/api-management-howto-policies/api-management-policies-restrict.png
[policies-save]: ./media/api-management-howto-policies/api-management-policies-save.png
