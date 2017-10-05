---
title: "Zasady w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie tworzenia, edytowania i konfigurowania zasad w usłudze API Management."
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
ms.openlocfilehash: 7c1f235343074ec11c635097f2b094a10f3fe781
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="policies-in-azure-api-management"></a><span data-ttu-id="3c91d-103">Zasady w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="3c91d-103">Policies in Azure API Management</span></span>
<span data-ttu-id="3c91d-104">W usłudze Azure API Management zasady są zaawansowanych możliwości systemu, który umożliwia wydawcy, aby zmienić zachowanie interfejsu API za pomocą konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3c91d-104">In Azure API Management, policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="3c91d-105">Zasady są zbiór instrukcji, które są wykonywane sekwencyjnie na żądanie lub odpowiedź interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="3c91d-105">Policies are a collection of Statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="3c91d-106">Popularne instrukcje obejmują Konwersja formatu z pliku XML do formatu JSON i Wywołaj szybkość ograniczenie, aby ograniczyć ilość przychodzących od dewelopera.</span><span class="sxs-lookup"><span data-stu-id="3c91d-106">Popular Statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer.</span></span> <span data-ttu-id="3c91d-107">Wiele zasad są dostępne poza pole.</span><span class="sxs-lookup"><span data-stu-id="3c91d-107">Many more policies are available out of the box.</span></span>

<span data-ttu-id="3c91d-108">Zobacz [informacje o zasadach] [ Policy Reference] pełną listę deklaracji zasad i ich ustawienia.</span><span class="sxs-lookup"><span data-stu-id="3c91d-108">See the [Policy Reference][Policy Reference] for a full list of policy statements and their settings.</span></span>

<span data-ttu-id="3c91d-109">Zasady są stosowane wewnątrz bramy, która znajduje się pomiędzy konsumenta interfejsu API i zarządzanego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="3c91d-109">Policies are applied inside the gateway which sits between the API consumer and the managed API.</span></span> <span data-ttu-id="3c91d-110">Brama odbiera wszystkie żądania i zwykle przekazuje je niezmieniony do podstawowej interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="3c91d-110">The gateway receives all requests and usually forwards them unaltered to the underlying API.</span></span> <span data-ttu-id="3c91d-111">Jednak zasady można zastosować zmiany do żądania przychodzące i wychodzące odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="3c91d-111">However a policy can apply changes to both the inbound request and outbound response.</span></span>

<span data-ttu-id="3c91d-112">Wyrażenia zasad mogą służyć jako wartości atrybutów lub wartości tekstowe w dowolnej z zasad usługi API Management, o ile w zasadach nie określono inaczej.</span><span class="sxs-lookup"><span data-stu-id="3c91d-112">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="3c91d-113">Niektóre zasady, takie jak [sterowania przepływem] [ Control flow] i [zmiennej zestaw] [ Set variable] zasady są oparte na wyrażeniach zasad.</span><span class="sxs-lookup"><span data-stu-id="3c91d-113">Some policies such as the [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="3c91d-114">Aby uzyskać więcej informacji, zobacz [zaawansowane zasady] [ Advanced policies] i [wyrażenie zasad][Policy expressions].</span><span class="sxs-lookup"><span data-stu-id="3c91d-114">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions].</span></span>

## <span data-ttu-id="3c91d-115"><a name="scopes"></a>Sposobu konfigurowania zasad</span><span class="sxs-lookup"><span data-stu-id="3c91d-115"><a name="scopes"> </a>How to configure policies</span></span>
<span data-ttu-id="3c91d-116">Zasady można skonfigurować globalnie lub w zakresie [produktu][Product], [interfejsu API] [ API] lub [operacji] [Operation].</span><span class="sxs-lookup"><span data-stu-id="3c91d-116">Policies can be configured globally or at the scope of a [Product][Product], [API][API] or [Operation][Operation].</span></span> <span data-ttu-id="3c91d-117">Aby skonfigurować zasadę, przejdź do edytora zasad w portalu wydawcy.</span><span class="sxs-lookup"><span data-stu-id="3c91d-117">To configure a policy, navigate to the Policies editor in the publisher portal.</span></span>

![Menu zasad][policies-menu]

<span data-ttu-id="3c91d-119">Edytor zasad składa się z trzech głównych sekcji: zakres zasad (u góry), definicji zasad, gdy zasady są edytowane (lewych) i instrukcje listy (po prawej):</span><span class="sxs-lookup"><span data-stu-id="3c91d-119">The policies editor consists of three main sections: the policy scope (top), the policy definition where policies are edited (left) and the statements list (right):</span></span>

![Edytor zasad][policies-editor]

<span data-ttu-id="3c91d-121">Aby rozpocząć konfigurowanie zasad, musisz najpierw wybrać zakres, w którym mają dotyczyć zasady.</span><span class="sxs-lookup"><span data-stu-id="3c91d-121">To begin configuring a policy you must first select the scope at which the policy should apply.</span></span> <span data-ttu-id="3c91d-122">Na poniższym zrzucie ekranu **Starter** produkt jest zaznaczony.</span><span class="sxs-lookup"><span data-stu-id="3c91d-122">In the screenshot below the **Starter** product is selected.</span></span> <span data-ttu-id="3c91d-123">Należy pamiętać, że kwadratowy symbol obok nazwy zasad wskazuje, że zasady jest już stosowane na tym poziomie.</span><span class="sxs-lookup"><span data-stu-id="3c91d-123">Note that the square symbol next to the policy name indicates that a policy is already applied at this level.</span></span>

![Zakres][policies-scope]

<span data-ttu-id="3c91d-125">Ponieważ zasady zostały już zastosowane, konfiguracji jest wyświetlany w definicji widoku.</span><span class="sxs-lookup"><span data-stu-id="3c91d-125">Since a policy has already been applied, the configuration is shown in the definition view.</span></span>

![Konfigurowanie][policies-configure]

<span data-ttu-id="3c91d-127">Zasady zostaną wyświetlone tylko do odczytu na początku.</span><span class="sxs-lookup"><span data-stu-id="3c91d-127">The policy is displayed read-only at first.</span></span> <span data-ttu-id="3c91d-128">Aby edytować kliknij definicji **Konfiguruj zasady** akcji.</span><span class="sxs-lookup"><span data-stu-id="3c91d-128">In order to edit the definition click the **Configure Policy** action.</span></span>

![Edytuj][policies-edit]

<span data-ttu-id="3c91d-130">Definicja zasad jest proste dokument XML, który opisuje sekwencji instrukcji dla ruchu przychodzącego i wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="3c91d-130">The policy definition is a simple XML document that describes a sequence of inbound and outbound statements.</span></span> <span data-ttu-id="3c91d-131">Plik XML można edytować bezpośrednio w oknie definicji.</span><span class="sxs-lookup"><span data-stu-id="3c91d-131">The XML can be edited directly in the definition window.</span></span> <span data-ttu-id="3c91d-132">Lista instrukcji znajduje się po prawej stronie i instrukcje mające zastosowanie do bieżącego zakresu są włączone i wyróżniony; jak dowodzą **Limit szybkości wywołać** instrukcji na zrzucie ekranu powyżej.</span><span class="sxs-lookup"><span data-stu-id="3c91d-132">A list of statements is provided to the right and statements applicable to the current scope are enabled and highlighted; as demonstrated by the **Limit Call Rate** statement in the screenshot above.</span></span>

<span data-ttu-id="3c91d-133">Kliknięcie instrukcji włączone spowoduje dodanie odpowiednich XML w lokalizacji kursora w definicji widoku.</span><span class="sxs-lookup"><span data-stu-id="3c91d-133">Clicking an enabled statement will add the appropriate XML at the location of the cursor in the definition view.</span></span> 

> [!NOTE]
> <span data-ttu-id="3c91d-134">Zasady, które chcesz dodać nie jest włączona, upewnij się, że jesteś w niewłaściwym zakresie dla tej zasady.</span><span class="sxs-lookup"><span data-stu-id="3c91d-134">If the policy that you want to add is not enabled, ensure that you are in the correct scope for that policy.</span></span> <span data-ttu-id="3c91d-135">Każda instrukcja zasad jest przeznaczony do użytku w określonych zakresach i sekcje zasad.</span><span class="sxs-lookup"><span data-stu-id="3c91d-135">Each policy statement is designed for use in certain scopes and policy sections.</span></span> <span data-ttu-id="3c91d-136">Aby zapoznać się z sekcji zasad i zakresy dla zasady, sprawdź **użycia** sekcji dla tej zasady w [informacje o zasadach][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="3c91d-136">To review the policy sections and scopes for a policy, check the **Usage** section for that policy in the [Policy Reference][Policy Reference].</span></span>
> 
> 

<span data-ttu-id="3c91d-137">Pełna lista deklaracji zasad i ich ustawienia są dostępne w [informacje o zasadach][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="3c91d-137">A full list of policy statements and their settings are available in the [Policy Reference][Policy Reference].</span></span>

<span data-ttu-id="3c91d-138">Na przykład, aby dodać nowe oświadczenie ograniczanie żądań przychodzących do określonych adresów IP, umieść kursor wewnątrz treści `inbound` — element XML i kliknij przycisk **wywołującego Ogranicz adresów IP** instrukcji.</span><span class="sxs-lookup"><span data-stu-id="3c91d-138">For example, to add a new statement to restrict incoming requests to specified IP addresses, place the cursor just inside the content of the `inbound` XML element and click the **Restrict caller IPs** statement.</span></span>

![Zasady ograniczeń][policies-restrict]

<span data-ttu-id="3c91d-140">Spowoduje to dodanie fragment kodu XML dotyczący `inbound` element, który zawiera wskazówki dotyczące sposobu konfigurowania instrukcji.</span><span class="sxs-lookup"><span data-stu-id="3c91d-140">This will add an XML snippet to the `inbound` element that provides guidance on how to configure the statement.</span></span>

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

<span data-ttu-id="3c91d-141">Ogranicza liczby żądań przychodzących i zaakceptować tylko te z adresu IP 1.2.3.4 zmodyfikować kod XML w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="3c91d-141">To limit inbound requests and accept only those from an IP address of 1.2.3.4 modify the XML as follows:</span></span>

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Zapisz][policies-save]

<span data-ttu-id="3c91d-143">Po zakończeniu konfigurowania instrukcje zasad, kliknij przycisk **zapisać** i zmiany będą przekazywane do bramy usługi API Management natychmiast.</span><span class="sxs-lookup"><span data-stu-id="3c91d-143">When complete configuring the statements for the policy, click **Save** and the changes will be propagated to the API Management gateway immediately.</span></span>

## <span data-ttu-id="3c91d-144"><a name="sections"></a>Opis zasad konfiguracji</span><span class="sxs-lookup"><span data-stu-id="3c91d-144"><a name="sections"> </a>Understanding policy configuration</span></span>
<span data-ttu-id="3c91d-145">Zasady zostaną serię instrukcji, które są wykonywane w kolejności na żądania i odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="3c91d-145">A policy is a series of statements that execute in order for a request and a response.</span></span> <span data-ttu-id="3c91d-146">Konfiguracja jest odpowiednio podzielone na `inbound`, `backend`, `outbound`, i `on-error` sekcjach przedstawiono, jak pokazano w poniższej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3c91d-146">The configuration is divided appropriately into `inbound`, `backend`, `outbound`, and `on-error` sections as shown in the following configuration.</span></span>

```xml
<policies>
  <inbound>
    <!-- statements to be applied to the request go here -->
  </inbound>
  <backend>
    <!-- statements to be applied before the request is forwarded to 
         the backend service go here -->
  </backend>
  <outbound>
    <!-- statements to be applied to the response go here -->
  </outbound>
  <on-error>
    <!-- statements to be applied if there is an error condition go here -->
  </on-error>
</policies> 
```

<span data-ttu-id="3c91d-147">Jeśli występuje błąd podczas przetwarzania żądania, wszystkie pozostałe kroki `inbound`, `backend`, lub `outbound` sekcje są pomijane i wykonywania przechodzi do instrukcji w `on-error` sekcji.</span><span class="sxs-lookup"><span data-stu-id="3c91d-147">If there is an error during the processing of a request, any remaining steps in the `inbound`, `backend`, or `outbound` sections are skipped and execution jumps to the statements in the `on-error` section.</span></span> <span data-ttu-id="3c91d-148">Przez umieszczenie deklaracji zasad w `on-error` możesz przejrzeć kod błędu przy użyciu sekcji `context.LastError` właściwość, sprawdzić i dostosować za pomocą odpowiedzi błędu `set-body` zasad i skonfigurować, co się stanie w przypadku wystąpienia błędu.</span><span class="sxs-lookup"><span data-stu-id="3c91d-148">By placing policy statements in the `on-error` section you can review the error by using the `context.LastError` property, inspect and customize the error response using the `set-body` policy, and configure what happens if an error occurs.</span></span> <span data-ttu-id="3c91d-149">Brak kody błędów dla wbudowanych kroków i błędy, które mogą wystąpić podczas przetwarzania zasady.</span><span class="sxs-lookup"><span data-stu-id="3c91d-149">There are error codes for built-in steps and for errors that may occur during the processing of policy statements.</span></span> <span data-ttu-id="3c91d-150">Aby uzyskać więcej informacji, zobacz [obsługi błędów w zasad interfejsu API zarządzania](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span><span class="sxs-lookup"><span data-stu-id="3c91d-150">For more information, see [Error handling in API Management policies](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span></span>

<span data-ttu-id="3c91d-151">Ponieważ zasad można określić na różnych poziomach (globalne, produktu, interfejsu api i operacji) konfiguracji umożliwia określenie kolejności, w którym instrukcji definicji zasad wykonywania względem zasad nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="3c91d-151">Since policies can be specified at different levels (global, product, api and operation) the configuration provides a way for you to specify the order in which the policy definition's statements execute with respect to the parent policy.</span></span> 

<span data-ttu-id="3c91d-152">Zakresy zasad są oceniane w następującej kolejności.</span><span class="sxs-lookup"><span data-stu-id="3c91d-152">Policy scopes are evaluated in the following order.</span></span>

1. <span data-ttu-id="3c91d-153">Globalne</span><span class="sxs-lookup"><span data-stu-id="3c91d-153">Global scope</span></span>
2. <span data-ttu-id="3c91d-154">Zakres produktu</span><span class="sxs-lookup"><span data-stu-id="3c91d-154">Product scope</span></span>
3. <span data-ttu-id="3c91d-155">Zakres interfejsu API</span><span class="sxs-lookup"><span data-stu-id="3c91d-155">API scope</span></span>
4. <span data-ttu-id="3c91d-156">Operacja zakresu</span><span class="sxs-lookup"><span data-stu-id="3c91d-156">Operation scope</span></span>

<span data-ttu-id="3c91d-157">Instrukcje w nich są oceniane według położenia `base` elementu, jeśli jest obecny.</span><span class="sxs-lookup"><span data-stu-id="3c91d-157">The statements within them are evaluated according to the placement of the `base` element, if it is present.</span></span> <span data-ttu-id="3c91d-158">Globalne zasady nie ma nadrzędnego zasad i za pomocą `<base>` element w nim nie ma wpływu.</span><span class="sxs-lookup"><span data-stu-id="3c91d-158">Global policy has no parent policy and using the `<base>` element in it has no effect.</span></span>

<span data-ttu-id="3c91d-159">Na przykład jeśli masz zasady na poziomie globalnym i zasady skonfigurowane dla interfejsu API, następnie każdorazowe użycie tego konkretnego interfejsu API obie zasady zostaną zastosowane.</span><span class="sxs-lookup"><span data-stu-id="3c91d-159">For example, if you have a policy at the global level and a policy configured for an API, then whenever that particular API is used both policies will be applied.</span></span> <span data-ttu-id="3c91d-160">Zarządzanie interfejsami API umożliwia deterministyczne kolejność deklaracji zasad połączonych za pośrednictwem elementu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="3c91d-160">API Management allows for deterministic ordering of combined policy statements via the base element.</span></span> 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

<span data-ttu-id="3c91d-161">W definicji zasad przykład powyżej `cross-domain` instrukcji jest wykonywany przed następować wszystkie wyższej zasady, które z kolei, `find-and-replace` zasad.</span><span class="sxs-lookup"><span data-stu-id="3c91d-161">In the example policy definition above, the `cross-domain` statement would execute before any higher policies which would in turn, be followed by the `find-and-replace` policy.</span></span> 

<span data-ttu-id="3c91d-162">Aby wyświetlić zasady w bieżącym zakresie w edytorze zasad, kliknij **ponownie Oblicz skutecznych zasad dla wybranego zakresu**.</span><span class="sxs-lookup"><span data-stu-id="3c91d-162">To see the policies in the current scope in the policy editor, click **Recalculate effective policy for selected scope**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c91d-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3c91d-163">Next steps</span></span>
<span data-ttu-id="3c91d-164">Zapoznaj się z następującego wideo na wyrażeniach zasad.</span><span class="sxs-lookup"><span data-stu-id="3c91d-164">Check out following video on policy expressions.</span></span>

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
