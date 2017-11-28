---
title: "Sposób użycia właściwości w ramach zasad usługi Azure API Management"
description: "Dowiedz się, jak używać właściwości w ramach zasad usługi Azure API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f39b00f-cf6e-4cef-9bf2-1f89202c0bc0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3b0fe2a300038e13cc488bdb4f50f8be270ea8f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-properties-in-azure-api-management-policies"></a><span data-ttu-id="c33cd-103">Sposób użycia właściwości w ramach zasad usługi Azure API Management</span><span class="sxs-lookup"><span data-stu-id="c33cd-103">How to use properties in Azure API Management policies</span></span>
<span data-ttu-id="c33cd-104">Zarządzanie interfejsami API zasady są zaawansowanych możliwości systemu, który umożliwia wydawcy, aby zmienić zachowanie interfejsu API za pomocą konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c33cd-104">API Management policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="c33cd-105">Zasady to zbiór instrukcji, które są wykonywane sekwencyjnie podczas żądania lub odpowiedzi interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="c33cd-105">Policies are a collection of statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="c33cd-106">Deklaracji zasad może być skonstruowany przy użyciu wartości tekstowe literału, wyrażenie zasad i właściwości.</span><span class="sxs-lookup"><span data-stu-id="c33cd-106">Policy statements can be constructed using literal text values, policy expressions, and properties.</span></span> 

<span data-ttu-id="c33cd-107">Każde wystąpienie usługi Zarządzanie interfejsami API ma zbiór właściwości pary klucz wartość, które są globalne do wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="c33cd-107">Each API Management service instance has a properties collection of key/value pairs that are global to the service instance.</span></span> <span data-ttu-id="c33cd-108">Te właściwości mogą służyć do zarządzania stałych wartości ciągów we wszystkich Konfiguracja interfejsu API i zasady.</span><span class="sxs-lookup"><span data-stu-id="c33cd-108">These properties can be used to manage constant string values across all API configuration and policies.</span></span> <span data-ttu-id="c33cd-109">Każda właściwość ma następujące atrybuty.</span><span class="sxs-lookup"><span data-stu-id="c33cd-109">Each property has the following attributes.</span></span>

| <span data-ttu-id="c33cd-110">Atrybut</span><span class="sxs-lookup"><span data-stu-id="c33cd-110">Attribute</span></span> | <span data-ttu-id="c33cd-111">Typ</span><span class="sxs-lookup"><span data-stu-id="c33cd-111">Type</span></span> | <span data-ttu-id="c33cd-112">Opis</span><span class="sxs-lookup"><span data-stu-id="c33cd-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c33cd-113">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c33cd-113">Name</span></span> |<span data-ttu-id="c33cd-114">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c33cd-114">string</span></span> |<span data-ttu-id="c33cd-115">Nazwa właściwości.</span><span class="sxs-lookup"><span data-stu-id="c33cd-115">The name of the property.</span></span> <span data-ttu-id="c33cd-116">Może zawierać tylko litery, cyfry, okres, łączniki i znaki podkreślenia.</span><span class="sxs-lookup"><span data-stu-id="c33cd-116">It may contain only letters, digits, period, dash, and underscore characters.</span></span> |
| <span data-ttu-id="c33cd-117">Wartość</span><span class="sxs-lookup"><span data-stu-id="c33cd-117">Value</span></span> |<span data-ttu-id="c33cd-118">Ciąg</span><span class="sxs-lookup"><span data-stu-id="c33cd-118">string</span></span> |<span data-ttu-id="c33cd-119">Wartość właściwości.</span><span class="sxs-lookup"><span data-stu-id="c33cd-119">The value of the property.</span></span> <span data-ttu-id="c33cd-120">Nie może być pusta ani zawierać tylko odstępu.</span><span class="sxs-lookup"><span data-stu-id="c33cd-120">It may not be empty or consist only of whitespace.</span></span> |
| <span data-ttu-id="c33cd-121">Wpis tajny</span><span class="sxs-lookup"><span data-stu-id="c33cd-121">Secret</span></span> |<span data-ttu-id="c33cd-122">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="c33cd-122">boolean</span></span> |<span data-ttu-id="c33cd-123">Określa, czy wartość jest klucz tajny i powinny być szyfrowane, czy nie.</span><span class="sxs-lookup"><span data-stu-id="c33cd-123">Determines whether the value is a secret and should be encrypted or not.</span></span> |
| <span data-ttu-id="c33cd-124">Tagi</span><span class="sxs-lookup"><span data-stu-id="c33cd-124">Tags</span></span> |<span data-ttu-id="c33cd-125">Tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="c33cd-125">array of string</span></span> |<span data-ttu-id="c33cd-126">Opcjonalnie tagi, które udostępniane może służyć do filtrowania listy właściwości.</span><span class="sxs-lookup"><span data-stu-id="c33cd-126">Optional tags that when provided can be used to filter the property list.</span></span> |

<span data-ttu-id="c33cd-127">Właściwości są skonfigurowane w portalu wydawcy na **właściwości** kartę.</span><span class="sxs-lookup"><span data-stu-id="c33cd-127">Properties are configured in the publisher portal on the **Properties** tab.</span></span> <span data-ttu-id="c33cd-128">W poniższym przykładzie trzy właściwości są skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="c33cd-128">In the following example, three properties are configured.</span></span>

![Właściwości][api-management-properties]

<span data-ttu-id="c33cd-130">Wartości właściwości mogą zawierać ciągi literału i [wyrażenie zasad](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span><span class="sxs-lookup"><span data-stu-id="c33cd-130">Property values can contain literal strings and [policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span></span> <span data-ttu-id="c33cd-131">W poniższej tabeli przedstawiono poprzednie trzy przykładowe właściwości i ich atrybutów.</span><span class="sxs-lookup"><span data-stu-id="c33cd-131">The following table shows the previous three sample properties and their attributes.</span></span> <span data-ttu-id="c33cd-132">Wartość `ExpressionProperty` jest wyrażenie zasad, która zwraca ciąg zawierający bieżącą datę i godzinę.</span><span class="sxs-lookup"><span data-stu-id="c33cd-132">The value of `ExpressionProperty` is a policy expression that returns a string containing the current date and time.</span></span> <span data-ttu-id="c33cd-133">Właściwość `ContosoHeaderValue` jest oznaczona jako klucz tajny, więc jego wartość nie jest wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="c33cd-133">The property `ContosoHeaderValue` is marked as a secret, so its value is not displayed.</span></span>

| <span data-ttu-id="c33cd-134">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c33cd-134">Name</span></span> | <span data-ttu-id="c33cd-135">Wartość</span><span class="sxs-lookup"><span data-stu-id="c33cd-135">Value</span></span> | <span data-ttu-id="c33cd-136">Wpis tajny</span><span class="sxs-lookup"><span data-stu-id="c33cd-136">Secret</span></span> | <span data-ttu-id="c33cd-137">Tagi</span><span class="sxs-lookup"><span data-stu-id="c33cd-137">Tags</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c33cd-138">ContosoHeader</span><span class="sxs-lookup"><span data-stu-id="c33cd-138">ContosoHeader</span></span> |<span data-ttu-id="c33cd-139">trackingId</span><span class="sxs-lookup"><span data-stu-id="c33cd-139">TrackingId</span></span> |<span data-ttu-id="c33cd-140">False</span><span class="sxs-lookup"><span data-stu-id="c33cd-140">False</span></span> |<span data-ttu-id="c33cd-141">Contoso</span><span class="sxs-lookup"><span data-stu-id="c33cd-141">Contoso</span></span> |
| <span data-ttu-id="c33cd-142">ContosoHeaderValue</span><span class="sxs-lookup"><span data-stu-id="c33cd-142">ContosoHeaderValue</span></span> |<span data-ttu-id="c33cd-143">••••••••••••••••••••••</span><span class="sxs-lookup"><span data-stu-id="c33cd-143">••••••••••••••••••••••</span></span> |<span data-ttu-id="c33cd-144">True</span><span class="sxs-lookup"><span data-stu-id="c33cd-144">True</span></span> |<span data-ttu-id="c33cd-145">Contoso</span><span class="sxs-lookup"><span data-stu-id="c33cd-145">Contoso</span></span> |
| <span data-ttu-id="c33cd-146">ExpressionProperty</span><span class="sxs-lookup"><span data-stu-id="c33cd-146">ExpressionProperty</span></span> |<span data-ttu-id="c33cd-147">@(DateTime.Now.ToString())</span><span class="sxs-lookup"><span data-stu-id="c33cd-147">@(DateTime.Now.ToString())</span></span> |<span data-ttu-id="c33cd-148">False</span><span class="sxs-lookup"><span data-stu-id="c33cd-148">False</span></span> | |

## <a name="to-use-a-property"></a><span data-ttu-id="c33cd-149">Aby użyć właściwości</span><span class="sxs-lookup"><span data-stu-id="c33cd-149">To use a property</span></span>
<span data-ttu-id="c33cd-150">Aby użyć właściwości w zasadach, umieść nazwą właściwości wewnątrz podwójne pary nawiasów klamrowych, takich jak `{{ContosoHeader}}`, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="c33cd-150">To use a property in a policy, place the property name inside a double pair of braces like `{{ContosoHeader}}`, as shown in the following example.</span></span>

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

<span data-ttu-id="c33cd-151">W tym przykładzie `ContosoHeader` jest używana jako nazwa nagłówka w `set-header` zasad, a `ContosoHeaderValue` jest używany jako wartość nagłówka.</span><span class="sxs-lookup"><span data-stu-id="c33cd-151">In this example, `ContosoHeader` is used as the name of a header in a `set-header` policy, and `ContosoHeaderValue` is used as the value of that header.</span></span> <span data-ttu-id="c33cd-152">Gdy ta zasada jest oceniane podczas żądania lub odpowiedzi na bramie usługi API Management `{{ContosoHeader}}` i `{{ContosoHeaderValue}}` są zamieniane na ich wartości odpowiednich właściwości.</span><span class="sxs-lookup"><span data-stu-id="c33cd-152">When this policy is evaluated during a request or response to the API Management gateway, `{{ContosoHeader}}` and `{{ContosoHeaderValue}}` are replaced with their respective property values.</span></span>

<span data-ttu-id="c33cd-153">Właściwości mogą być używane jako atrybut pełną lub wartości elementów, jak pokazano w poprzednim przykładzie, ale również mogą zostać wstawione do albo połączone z częścią wyrażenia literału tekstu, jak pokazano w poniższym przykładzie:`<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span><span class="sxs-lookup"><span data-stu-id="c33cd-153">Properties can be used as complete attribute or element values as shown in the previous example, but they can also be inserted into or combined with part of a literal text expression as shown in the following example: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span></span>

<span data-ttu-id="c33cd-154">Właściwości może również zawierać wyrażenie zasad.</span><span class="sxs-lookup"><span data-stu-id="c33cd-154">Properties can also contain policy expressions.</span></span> <span data-ttu-id="c33cd-155">W poniższym przykładzie `ExpressionProperty` jest używany.</span><span class="sxs-lookup"><span data-stu-id="c33cd-155">In the following example, the `ExpressionProperty` is used.</span></span>

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

<span data-ttu-id="c33cd-156">W przypadku oceny tych zasad `{{ExpressionProperty}}` zastępuje z wartością: `@(DateTime.Now.ToString())`.</span><span class="sxs-lookup"><span data-stu-id="c33cd-156">When this policy is evaluated, `{{ExpressionProperty}}` is replaced with its value: `@(DateTime.Now.ToString())`.</span></span> <span data-ttu-id="c33cd-157">Ponieważ wartość jest wyrażenie zasad, wyrażenie jest obliczane i zasady kontynuuje jego wykonywania.</span><span class="sxs-lookup"><span data-stu-id="c33cd-157">Since the value is a policy expression, the expression is evaluated and the policy proceeds with its execution.</span></span>

<span data-ttu-id="c33cd-158">Ten limit można sprawdzić w portalu dla deweloperów, wywołując operację, która ma zasady z właściwości w zakresie.</span><span class="sxs-lookup"><span data-stu-id="c33cd-158">You can test this out in the developer portal by calling an operation that has a policy with properties in scope.</span></span> <span data-ttu-id="c33cd-159">W poniższym przykładzie, operacja jest wywoływana z dwóch poprzedni przykład `set-header` zasad przy użyciu właściwości.</span><span class="sxs-lookup"><span data-stu-id="c33cd-159">In the following example, an operation is called with the two previous example `set-header` policies with properties.</span></span> <span data-ttu-id="c33cd-160">Należy pamiętać, że odpowiedź zawiera dwa Nagłówki niestandardowe, które zostały skonfigurowane przy użyciu zasad z właściwościami.</span><span class="sxs-lookup"><span data-stu-id="c33cd-160">Note that the response contains two custom headers that were configured using policies with properties.</span></span>

![Portal dla deweloperów][api-management-send-results]

<span data-ttu-id="c33cd-162">Jeśli przyjrzymy się [inspektora interfejsu API śledzenia](api-management-howto-api-inspector.md) dla wywołaniu, które obejmuje dwie zasady poprzedniej próbki z właściwościami, można wyświetlić dwa `set-header` zasady z wartościami właściwości dodaje oraz ocena wyrażenie zasad dla właściwości, który zawiera wyrażenie zasad.</span><span class="sxs-lookup"><span data-stu-id="c33cd-162">If you look at the [API Inspector trace](api-management-howto-api-inspector.md) for a call that includes the two previous sample policies with properties, you can see the two `set-header` policies with the property values inserted as well as the policy expression evaluation for the property that contained the policy expression.</span></span>

![Interfejs API inspektora śledzenia][api-management-api-inspector-trace]

<span data-ttu-id="c33cd-164">Należy pamiętać, że podczas wartości właściwości mogą zawierać wyrażenia zasad, wartości właściwości nie może zawierać inne właściwości.</span><span class="sxs-lookup"><span data-stu-id="c33cd-164">Note that while property values can contain policy expressions, property values can't contain other properties.</span></span> <span data-ttu-id="c33cd-165">Jeśli tekst zawierający odwołania do właściwości jest używana do wartości właściwości, takie jak `Property value text {{MyProperty}}`, odwołania do tej właściwości nie można zamienić i zostaną zawarte w ramach wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="c33cd-165">If text containing a property reference is used for a property value, such as `Property value text {{MyProperty}}`, that property reference won't be replaced and will be included as part of the property value.</span></span>

## <a name="to-create-a-property"></a><span data-ttu-id="c33cd-166">Aby utworzyć właściwość</span><span class="sxs-lookup"><span data-stu-id="c33cd-166">To create a property</span></span>
<span data-ttu-id="c33cd-167">Aby utworzyć właściwość, kliknij przycisk **Dodaj właściwość** na **właściwości** kartę.</span><span class="sxs-lookup"><span data-stu-id="c33cd-167">To create a property, click **Add property** on the **Properties** tab.</span></span>

![Dodaj właściwość][api-management-properties-add-property-menu]

<span data-ttu-id="c33cd-169">**Nazwa** i **wartość** są wymaganymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="c33cd-169">**Name** and **Value** are required values.</span></span> <span data-ttu-id="c33cd-170">Jeśli wartość tej właściwości jest klucz tajny, sprawdź **jest klucz tajny** wyboru.</span><span class="sxs-lookup"><span data-stu-id="c33cd-170">If this property value is a secret, check the **This is a secret** checkbox.</span></span> <span data-ttu-id="c33cd-171">Wprowadź co najmniej jeden opcjonalny znaczniki, aby ułatwić organizowanie właściwości, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="c33cd-171">Enter one or more optional tags to help with organizing your properties, and click **Save**.</span></span>

![Dodaj właściwość][api-management-properties-add-property]

<span data-ttu-id="c33cd-173">Po zapisaniu nowej właściwości **wyszukiwania właściwości** pole tekstowe jest wypełniane przy użyciu nazwy nowej właściwości i nową właściwość jest wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="c33cd-173">When a new property is saved, the **Search property** textbox is populated with the name of the new property and the new property is displayed.</span></span> <span data-ttu-id="c33cd-174">Aby wyświetlić wszystkie właściwości, wyczyść **wyszukiwania właściwości** pole tekstowe i naciśnij klawisz enter.</span><span class="sxs-lookup"><span data-stu-id="c33cd-174">To display all properties, clear the **Search property** textbox and press enter.</span></span>

![Właściwości][api-management-properties-property-saved]

<span data-ttu-id="c33cd-176">Aby uzyskać informacje dotyczące tworzenia właściwości przy użyciu interfejsu API REST, zobacz [utworzyć właściwość przy użyciu interfejsu API REST](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span><span class="sxs-lookup"><span data-stu-id="c33cd-176">For information on creating a property using the REST API, see [Create a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span></span>

## <a name="to-edit-a-property"></a><span data-ttu-id="c33cd-177">Aby edytować właściwość</span><span class="sxs-lookup"><span data-stu-id="c33cd-177">To edit a property</span></span>
<span data-ttu-id="c33cd-178">Aby edytować właściwości, kliknij przycisk **Edytuj** obok właściwości do edycji.</span><span class="sxs-lookup"><span data-stu-id="c33cd-178">To edit a property, click **Edit** beside the property to edit.</span></span>

![Edytowanie właściwości][api-management-properties-edit]

<span data-ttu-id="c33cd-180">Wprowadź żądane zmiany, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="c33cd-180">Make any desired changes, and click **Save**.</span></span> <span data-ttu-id="c33cd-181">Jeśli zmienisz nazwę właściwości, wszystkie zasady, które odwołują się do tej właściwości są automatycznie aktualizowane do użycia nowej nazwy.</span><span class="sxs-lookup"><span data-stu-id="c33cd-181">If you change the property name, any policies that reference that property are automatically updated to use the new name.</span></span>

![Edytowanie właściwości][api-management-properties-edit-property]

<span data-ttu-id="c33cd-183">Informacje dotyczące edytowania właściwości przy użyciu interfejsu API REST, zobacz [Edytuj właściwości przy użyciu interfejsu API REST](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span><span class="sxs-lookup"><span data-stu-id="c33cd-183">For information on editing a property using the REST API, see [Edit a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span></span>

## <a name="to-delete-a-property"></a><span data-ttu-id="c33cd-184">Aby usunąć właściwość</span><span class="sxs-lookup"><span data-stu-id="c33cd-184">To delete a property</span></span>
<span data-ttu-id="c33cd-185">Aby usunąć właściwość, kliknij przycisk **usunąć** obok właściwości do usunięcia.</span><span class="sxs-lookup"><span data-stu-id="c33cd-185">To delete a property, click **Delete** beside the property to delete.</span></span>

![Usuń właściwość][api-management-properties-delete]

<span data-ttu-id="c33cd-187">Kliknij przycisk **tak, usuń go** o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="c33cd-187">Click **Yes, delete it** to confirm.</span></span>

![Potwierdzenie usunięcia][api-management-delete-confirm]

> [!IMPORTANT]
> <span data-ttu-id="c33cd-189">Jeśli właściwość odwołuje się do niego żadnych zasad, nie można pomyślnie usunąć przed usunięciem właściwości z wszystkich zasad, które go używają.</span><span class="sxs-lookup"><span data-stu-id="c33cd-189">If the property is referenced by any policies, you will be unable to successfully delete it until you remove the property from all policies that use it.</span></span>
> 
> 

<span data-ttu-id="c33cd-190">Aby uzyskać informacje na temat usuwania właściwości przy użyciu interfejsu API REST, zobacz [usunąć właściwości przy użyciu interfejsu API REST](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span><span class="sxs-lookup"><span data-stu-id="c33cd-190">For information on deleting a property using the REST API, see [Delete a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span></span>

## <a name="to-search-and-filter-properties"></a><span data-ttu-id="c33cd-191">Do wyszukiwania i filtrowania właściwości</span><span class="sxs-lookup"><span data-stu-id="c33cd-191">To search and filter properties</span></span>
<span data-ttu-id="c33cd-192">**Właściwości** karta zawiera wyszukiwania i filtrowania funkcje ułatwiające zarządzanie właściwości.</span><span class="sxs-lookup"><span data-stu-id="c33cd-192">The **Properties** tab includes searching and filtering capabilities to help you manage your properties.</span></span> <span data-ttu-id="c33cd-193">Aby filtrować listę właściwości według nazwy właściwości, wpisz wyszukiwany termin w **wyszukiwania właściwości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="c33cd-193">To filter the property list by property name, enter a search term in the **Search property** textbox.</span></span> <span data-ttu-id="c33cd-194">Aby wyświetlić wszystkie właściwości, wyczyść **wyszukiwania właściwości** pole tekstowe i naciśnij klawisz enter.</span><span class="sxs-lookup"><span data-stu-id="c33cd-194">To display all properties, clear the **Search property** textbox and press enter.</span></span>

![Wyszukiwanie][api-management-properties-search]

<span data-ttu-id="c33cd-196">Aby filtrować listę właściwości, według wartości tagów, wprowadź jeden lub więcej tagów do **Filtruj według znaczników** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="c33cd-196">To filter the property list by tag values, enter one or more tags into the **Filter by tags** textbox.</span></span> <span data-ttu-id="c33cd-197">Aby wyświetlić wszystkie właściwości, wyczyść **Filtruj według znaczników** pole tekstowe i naciśnij klawisz enter.</span><span class="sxs-lookup"><span data-stu-id="c33cd-197">To display all properties, clear the **Filter by tags** textbox and press enter.</span></span>

![Filtr][api-management-properties-filter]

## <a name="next-steps"></a><span data-ttu-id="c33cd-199">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c33cd-199">Next steps</span></span>
* <span data-ttu-id="c33cd-200">Dowiedz się więcej o pracy z zasadami</span><span class="sxs-lookup"><span data-stu-id="c33cd-200">Learn more about working with policies</span></span>
  * [<span data-ttu-id="c33cd-201">Zasady w usłudze API Management</span><span class="sxs-lookup"><span data-stu-id="c33cd-201">Policies in API Management</span></span>](api-management-howto-policies.md)
  * [<span data-ttu-id="c33cd-202">Dokumentacja zasad</span><span class="sxs-lookup"><span data-stu-id="c33cd-202">Policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [<span data-ttu-id="c33cd-203">Wyrażenia zasad</span><span class="sxs-lookup"><span data-stu-id="c33cd-203">Policy expressions</span></span>](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="c33cd-204">Obejrzyj film wideo</span><span class="sxs-lookup"><span data-stu-id="c33cd-204">Watch a video overview</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Use-Properties-in-Policies/player]
> 
> 

[api-management-properties]: ./media/api-management-howto-properties/api-management-properties.png
[api-management-properties-add-property]: ./media/api-management-howto-properties/api-management-properties-add-property.png
[api-management-properties-edit-property]: ./media/api-management-howto-properties/api-management-properties-edit-property.png
[api-management-properties-add-property-menu]: ./media/api-management-howto-properties/api-management-properties-add-property-menu.png
[api-management-properties-property-saved]: ./media/api-management-howto-properties/api-management-properties-property-saved.png
[api-management-properties-delete]: ./media/api-management-howto-properties/api-management-properties-delete.png
[api-management-properties-edit]: ./media/api-management-howto-properties/api-management-properties-edit.png
[api-management-delete-confirm]: ./media/api-management-howto-properties/api-management-delete-confirm.png
[api-management-properties-search]: ./media/api-management-howto-properties/api-management-properties-search.png
[api-management-send-results]: ./media/api-management-howto-properties/api-management-send-results.png
[api-management-properties-filter]: ./media/api-management-howto-properties/api-management-properties-filter.png
[api-management-api-inspector-trace]: ./media/api-management-howto-properties/api-management-api-inspector-trace.png

