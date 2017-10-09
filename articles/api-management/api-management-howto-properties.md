---
title: "właściwości toouse aaaHow w ramach zasad usługi Azure API Management"
description: "Dowiedz się, jak właściwości toouse w ramach zasad usługi Azure API Management."
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
ms.openlocfilehash: 1ff096deeb97543b48dcf1f40be9dbfcbcd09542
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-properties-in-azure-api-management-policies"></a><span data-ttu-id="7a378-103">Jak właściwości toouse w ramach zasad usługi Azure API Management</span><span class="sxs-lookup"><span data-stu-id="7a378-103">How toouse properties in Azure API Management policies</span></span>
<span data-ttu-id="7a378-104">Zarządzanie interfejsami API zasady są zaawansowanych możliwości hello system, który umożliwia zachowanie hello toochange hello interfejsu API za pomocą konfiguracji hello wydawcy.</span><span class="sxs-lookup"><span data-stu-id="7a378-104">API Management policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="7a378-105">Zasady są zbiór instrukcji, które są wykonywane sekwencyjnie na powitania żądania lub odpowiedzi interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="7a378-105">Policies are a collection of statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="7a378-106">Deklaracji zasad może być skonstruowany przy użyciu wartości tekstowe literału, wyrażenie zasad i właściwości.</span><span class="sxs-lookup"><span data-stu-id="7a378-106">Policy statements can be constructed using literal text values, policy expressions, and properties.</span></span> 

<span data-ttu-id="7a378-107">Każde wystąpienie usługi Zarządzanie interfejsami API ma kolekcję właściwości par klucz/wartość, które są globalne toohello wystąpienie usługi.</span><span class="sxs-lookup"><span data-stu-id="7a378-107">Each API Management service instance has a properties collection of key/value pairs that are global toohello service instance.</span></span> <span data-ttu-id="7a378-108">Te właściwości mogą być używane toomanage stałych wartości ciągów we wszystkich Konfiguracja interfejsu API i zasady.</span><span class="sxs-lookup"><span data-stu-id="7a378-108">These properties can be used toomanage constant string values across all API configuration and policies.</span></span> <span data-ttu-id="7a378-109">Każda właściwość ma hello następujące atrybuty.</span><span class="sxs-lookup"><span data-stu-id="7a378-109">Each property has hello following attributes.</span></span>

| <span data-ttu-id="7a378-110">Atrybut</span><span class="sxs-lookup"><span data-stu-id="7a378-110">Attribute</span></span> | <span data-ttu-id="7a378-111">Typ</span><span class="sxs-lookup"><span data-stu-id="7a378-111">Type</span></span> | <span data-ttu-id="7a378-112">Opis</span><span class="sxs-lookup"><span data-stu-id="7a378-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7a378-113">Nazwa</span><span class="sxs-lookup"><span data-stu-id="7a378-113">Name</span></span> |<span data-ttu-id="7a378-114">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7a378-114">string</span></span> |<span data-ttu-id="7a378-115">Nazwa Hello hello właściwości.</span><span class="sxs-lookup"><span data-stu-id="7a378-115">hello name of hello property.</span></span> <span data-ttu-id="7a378-116">Może zawierać tylko litery, cyfry, okres, łączniki i znaki podkreślenia.</span><span class="sxs-lookup"><span data-stu-id="7a378-116">It may contain only letters, digits, period, dash, and underscore characters.</span></span> |
| <span data-ttu-id="7a378-117">Wartość</span><span class="sxs-lookup"><span data-stu-id="7a378-117">Value</span></span> |<span data-ttu-id="7a378-118">Ciąg</span><span class="sxs-lookup"><span data-stu-id="7a378-118">string</span></span> |<span data-ttu-id="7a378-119">wartość Hello hello właściwości.</span><span class="sxs-lookup"><span data-stu-id="7a378-119">hello value of hello property.</span></span> <span data-ttu-id="7a378-120">Nie może być pusta ani zawierać tylko odstępu.</span><span class="sxs-lookup"><span data-stu-id="7a378-120">It may not be empty or consist only of whitespace.</span></span> |
| <span data-ttu-id="7a378-121">Wpis tajny</span><span class="sxs-lookup"><span data-stu-id="7a378-121">Secret</span></span> |<span data-ttu-id="7a378-122">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="7a378-122">boolean</span></span> |<span data-ttu-id="7a378-123">Określa, czy wartość hello jest klucz tajny i powinny być szyfrowane, czy nie.</span><span class="sxs-lookup"><span data-stu-id="7a378-123">Determines whether hello value is a secret and should be encrypted or not.</span></span> |
| <span data-ttu-id="7a378-124">Tagi</span><span class="sxs-lookup"><span data-stu-id="7a378-124">Tags</span></span> |<span data-ttu-id="7a378-125">Tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="7a378-125">array of string</span></span> |<span data-ttu-id="7a378-126">Opcjonalnie tagi, które udostępniane mogą być używane toofilter hello właściwości listy.</span><span class="sxs-lookup"><span data-stu-id="7a378-126">Optional tags that when provided can be used toofilter hello property list.</span></span> |

<span data-ttu-id="7a378-127">Właściwości są skonfigurowane w portalu wydawcy hello na powitania **właściwości** kartę. W hello poniższy przykład trzech właściwości są skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="7a378-127">Properties are configured in hello publisher portal on hello **Properties** tab. In hello following example, three properties are configured.</span></span>

![Właściwości][api-management-properties]

<span data-ttu-id="7a378-129">Wartości właściwości mogą zawierać ciągi literału i [wyrażenie zasad](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span><span class="sxs-lookup"><span data-stu-id="7a378-129">Property values can contain literal strings and [policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span></span> <span data-ttu-id="7a378-130">Witaj poniższej tabeli przedstawiono hello poprzednie trzy przykładowe właściwości i ich atrybutów.</span><span class="sxs-lookup"><span data-stu-id="7a378-130">hello following table shows hello previous three sample properties and their attributes.</span></span> <span data-ttu-id="7a378-131">Witaj wartość `ExpressionProperty` jest hello wyrażenie zasad, która zwraca ciąg zawierający bieżącą datę i godzinę.</span><span class="sxs-lookup"><span data-stu-id="7a378-131">hello value of `ExpressionProperty` is a policy expression that returns a string containing hello current date and time.</span></span> <span data-ttu-id="7a378-132">Witaj właściwości `ContosoHeaderValue` jest oznaczona jako klucz tajny, więc jego wartość nie jest wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="7a378-132">hello property `ContosoHeaderValue` is marked as a secret, so its value is not displayed.</span></span>

| <span data-ttu-id="7a378-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="7a378-133">Name</span></span> | <span data-ttu-id="7a378-134">Wartość</span><span class="sxs-lookup"><span data-stu-id="7a378-134">Value</span></span> | <span data-ttu-id="7a378-135">Wpis tajny</span><span class="sxs-lookup"><span data-stu-id="7a378-135">Secret</span></span> | <span data-ttu-id="7a378-136">Tagi</span><span class="sxs-lookup"><span data-stu-id="7a378-136">Tags</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7a378-137">ContosoHeader</span><span class="sxs-lookup"><span data-stu-id="7a378-137">ContosoHeader</span></span> |<span data-ttu-id="7a378-138">trackingId</span><span class="sxs-lookup"><span data-stu-id="7a378-138">TrackingId</span></span> |<span data-ttu-id="7a378-139">False</span><span class="sxs-lookup"><span data-stu-id="7a378-139">False</span></span> |<span data-ttu-id="7a378-140">Contoso</span><span class="sxs-lookup"><span data-stu-id="7a378-140">Contoso</span></span> |
| <span data-ttu-id="7a378-141">ContosoHeaderValue</span><span class="sxs-lookup"><span data-stu-id="7a378-141">ContosoHeaderValue</span></span> |<span data-ttu-id="7a378-142">••••••••••••••••••••••</span><span class="sxs-lookup"><span data-stu-id="7a378-142">••••••••••••••••••••••</span></span> |<span data-ttu-id="7a378-143">True</span><span class="sxs-lookup"><span data-stu-id="7a378-143">True</span></span> |<span data-ttu-id="7a378-144">Contoso</span><span class="sxs-lookup"><span data-stu-id="7a378-144">Contoso</span></span> |
| <span data-ttu-id="7a378-145">ExpressionProperty</span><span class="sxs-lookup"><span data-stu-id="7a378-145">ExpressionProperty</span></span> |<span data-ttu-id="7a378-146">@(DateTime.Now.ToString())</span><span class="sxs-lookup"><span data-stu-id="7a378-146">@(DateTime.Now.ToString())</span></span> |<span data-ttu-id="7a378-147">False</span><span class="sxs-lookup"><span data-stu-id="7a378-147">False</span></span> | |

## <a name="toouse-a-property"></a><span data-ttu-id="7a378-148">toouse właściwości</span><span class="sxs-lookup"><span data-stu-id="7a378-148">toouse a property</span></span>
<span data-ttu-id="7a378-149">toouse właściwości w zasadach, nazwa właściwości hello miejscu wewnątrz podwójne pary nawiasów klamrowych, takich jak `{{ContosoHeader}}`, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="7a378-149">toouse a property in a policy, place hello property name inside a double pair of braces like `{{ContosoHeader}}`, as shown in hello following example.</span></span>

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

<span data-ttu-id="7a378-150">W tym przykładzie `ContosoHeader` jest używana jako nazwa hello nagłówka w `set-header` zasad, a `ContosoHeaderValue` jest używany jako wartość hello nagłówka.</span><span class="sxs-lookup"><span data-stu-id="7a378-150">In this example, `ContosoHeader` is used as hello name of a header in a `set-header` policy, and `ContosoHeaderValue` is used as hello value of that header.</span></span> <span data-ttu-id="7a378-151">Gdy ta zasada jest oceniane podczas żądania lub odpowiedzi toohello interfejsu API zarządzania bramą, `{{ContosoHeader}}` i `{{ContosoHeaderValue}}` są zamieniane na ich wartości odpowiednich właściwości.</span><span class="sxs-lookup"><span data-stu-id="7a378-151">When this policy is evaluated during a request or response toohello API Management gateway, `{{ContosoHeader}}` and `{{ContosoHeaderValue}}` are replaced with their respective property values.</span></span>

<span data-ttu-id="7a378-152">Właściwości mogą być używane jako atrybut pełną lub wartości elementów, jak pokazano w poprzednim przykładzie hello, ale również mogą zostać wstawione do albo połączone z część wyrażenia literału tekstu, jak pokazano w hello poniższy przykład:`<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span><span class="sxs-lookup"><span data-stu-id="7a378-152">Properties can be used as complete attribute or element values as shown in hello previous example, but they can also be inserted into or combined with part of a literal text expression as shown in hello following example: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span></span>

<span data-ttu-id="7a378-153">Właściwości może również zawierać wyrażenie zasad.</span><span class="sxs-lookup"><span data-stu-id="7a378-153">Properties can also contain policy expressions.</span></span> <span data-ttu-id="7a378-154">W hello poniższy przykład, hello `ExpressionProperty` jest używany.</span><span class="sxs-lookup"><span data-stu-id="7a378-154">In hello following example, hello `ExpressionProperty` is used.</span></span>

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

<span data-ttu-id="7a378-155">W przypadku oceny tych zasad `{{ExpressionProperty}}` zastępuje z wartością: `@(DateTime.Now.ToString())`.</span><span class="sxs-lookup"><span data-stu-id="7a378-155">When this policy is evaluated, `{{ExpressionProperty}}` is replaced with its value: `@(DateTime.Now.ToString())`.</span></span> <span data-ttu-id="7a378-156">Ponieważ wartość hello jest wyrażenie zasad, hello wyrażenie jest obliczane i zasad hello kontynuuje jego wykonywania.</span><span class="sxs-lookup"><span data-stu-id="7a378-156">Since hello value is a policy expression, hello expression is evaluated and hello policy proceeds with its execution.</span></span>

<span data-ttu-id="7a378-157">Można to sprawdzić się w portalu dla deweloperów hello wywołując operację, która ma zasady z właściwości w zakresie.</span><span class="sxs-lookup"><span data-stu-id="7a378-157">You can test this out in hello developer portal by calling an operation that has a policy with properties in scope.</span></span> <span data-ttu-id="7a378-158">W hello poniższy przykład, operacja nosi nazwę Witaj dwie poprzedniego przykładu `set-header` zasad przy użyciu właściwości.</span><span class="sxs-lookup"><span data-stu-id="7a378-158">In hello following example, an operation is called with hello two previous example `set-header` policies with properties.</span></span> <span data-ttu-id="7a378-159">Należy pamiętać, że odpowiedź hello zawiera dwa Nagłówki niestandardowe, które zostały skonfigurowane przy użyciu zasad z właściwościami.</span><span class="sxs-lookup"><span data-stu-id="7a378-159">Note that hello response contains two custom headers that were configured using policies with properties.</span></span>

![Portal dla deweloperów][api-management-send-results]

<span data-ttu-id="7a378-161">Jeśli przyjrzymy się hello [inspektora interfejsu API śledzenia](api-management-howto-api-inspector.md) dla wywołania obejmującej hello dwa poprzednie przykładowe zasady z właściwościami, można wyświetlić hello dwa `set-header` zasady z wartościami właściwości hello dodaje oraz hello wyrażenie zasad Obliczanie dla właściwości hello, który zawiera wyrażenie zasad hello.</span><span class="sxs-lookup"><span data-stu-id="7a378-161">If you look at hello [API Inspector trace](api-management-howto-api-inspector.md) for a call that includes hello two previous sample policies with properties, you can see hello two `set-header` policies with hello property values inserted as well as hello policy expression evaluation for hello property that contained hello policy expression.</span></span>

![Interfejs API inspektora śledzenia][api-management-api-inspector-trace]

<span data-ttu-id="7a378-163">Należy pamiętać, że podczas wartości właściwości mogą zawierać wyrażenia zasad, wartości właściwości nie może zawierać inne właściwości.</span><span class="sxs-lookup"><span data-stu-id="7a378-163">Note that while property values can contain policy expressions, property values can't contain other properties.</span></span> <span data-ttu-id="7a378-164">Jeśli tekst zawierający odwołania do właściwości jest używana do wartości właściwości, takie jak `Property value text {{MyProperty}}`, że odwołania do właściwości nie zostanie zastąpiony i zostanie dołączony hello wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="7a378-164">If text containing a property reference is used for a property value, such as `Property value text {{MyProperty}}`, that property reference won't be replaced and will be included as part of hello property value.</span></span>

## <a name="toocreate-a-property"></a><span data-ttu-id="7a378-165">toocreate właściwości</span><span class="sxs-lookup"><span data-stu-id="7a378-165">toocreate a property</span></span>
<span data-ttu-id="7a378-166">Kliknij toocreate właściwość **Dodaj właściwość** na powitania **właściwości** kartę.</span><span class="sxs-lookup"><span data-stu-id="7a378-166">toocreate a property, click **Add property** on hello **Properties** tab.</span></span>

![Dodaj właściwość][api-management-properties-add-property-menu]

<span data-ttu-id="7a378-168">**Nazwa** i **wartość** są wymaganymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="7a378-168">**Name** and **Value** are required values.</span></span> <span data-ttu-id="7a378-169">Jeśli wartość tej właściwości jest klucz tajny, sprawdź hello **jest klucz tajny** wyboru.</span><span class="sxs-lookup"><span data-stu-id="7a378-169">If this property value is a secret, check hello **This is a secret** checkbox.</span></span> <span data-ttu-id="7a378-170">Wprowadź co najmniej jeden toohelp opcjonalnych tagów z organizowania właściwości, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="7a378-170">Enter one or more optional tags toohelp with organizing your properties, and click **Save**.</span></span>

![Dodaj właściwość][api-management-properties-add-property]

<span data-ttu-id="7a378-172">Po zapisaniu nowej właściwości hello **wyszukiwania właściwości** pole tekstowe jest wypełniane przy użyciu nazwy hello hello nową właściwość i nową właściwość hello jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="7a378-172">When a new property is saved, hello **Search property** textbox is populated with hello name of hello new property and hello new property is displayed.</span></span> <span data-ttu-id="7a378-173">Wyczyść wszystkie właściwości toodisplay hello **wyszukiwania właściwości** pole tekstowe i naciśnij klawisz enter.</span><span class="sxs-lookup"><span data-stu-id="7a378-173">toodisplay all properties, clear hello **Search property** textbox and press enter.</span></span>

![Właściwości][api-management-properties-property-saved]

<span data-ttu-id="7a378-175">Informacje dotyczące tworzenia właściwości przy użyciu hello interfejsu API REST, zobacz [utworzyć właściwość przy użyciu interfejsu API REST hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span><span class="sxs-lookup"><span data-stu-id="7a378-175">For information on creating a property using hello REST API, see [Create a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span></span>

## <a name="tooedit-a-property"></a><span data-ttu-id="7a378-176">tooedit właściwości</span><span class="sxs-lookup"><span data-stu-id="7a378-176">tooedit a property</span></span>
<span data-ttu-id="7a378-177">tooedit właściwości, kliknij przycisk **Edytuj** obok hello tooedit właściwości.</span><span class="sxs-lookup"><span data-stu-id="7a378-177">tooedit a property, click **Edit** beside hello property tooedit.</span></span>

![Edytowanie właściwości][api-management-properties-edit]

<span data-ttu-id="7a378-179">Wprowadź żądane zmiany, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="7a378-179">Make any desired changes, and click **Save**.</span></span> <span data-ttu-id="7a378-180">Jeśli zmienisz nazwę właściwości hello wszystkie zasady, które odwołują się do tej właściwości są automatycznie aktualizowane toouse hello nową nazwę.</span><span class="sxs-lookup"><span data-stu-id="7a378-180">If you change hello property name, any policies that reference that property are automatically updated toouse hello new name.</span></span>

![Edytowanie właściwości][api-management-properties-edit-property]

<span data-ttu-id="7a378-182">Informacje do edycji właściwości przy użyciu hello interfejsu API REST, zobacz [Edytuj właściwości przy użyciu interfejsu API REST hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span><span class="sxs-lookup"><span data-stu-id="7a378-182">For information on editing a property using hello REST API, see [Edit a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span></span>

## <a name="toodelete-a-property"></a><span data-ttu-id="7a378-183">toodelete właściwości</span><span class="sxs-lookup"><span data-stu-id="7a378-183">toodelete a property</span></span>
<span data-ttu-id="7a378-184">toodelete właściwości, kliknij przycisk **usunąć** obok hello toodelete właściwości.</span><span class="sxs-lookup"><span data-stu-id="7a378-184">toodelete a property, click **Delete** beside hello property toodelete.</span></span>

![Usuń właściwość][api-management-properties-delete]

<span data-ttu-id="7a378-186">Kliknij przycisk **tak, usuń go** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="7a378-186">Click **Yes, delete it** tooconfirm.</span></span>

![Potwierdzenie usunięcia][api-management-delete-confirm]

> [!IMPORTANT]
> <span data-ttu-id="7a378-188">Jeśli właściwość hello odwołuje się do niego wszystkie zasady, nie będzie toosuccessfully go usunąć przed usunięciem hello właściwości z wszystkich zasad, które go używają.</span><span class="sxs-lookup"><span data-stu-id="7a378-188">If hello property is referenced by any policies, you will be unable toosuccessfully delete it until you remove hello property from all policies that use it.</span></span>
> 
> 

<span data-ttu-id="7a378-189">Informacje dotyczące usuwania właściwości przy użyciu hello interfejsu API REST, zobacz [usunąć właściwości przy użyciu interfejsu API REST hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span><span class="sxs-lookup"><span data-stu-id="7a378-189">For information on deleting a property using hello REST API, see [Delete a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span></span>

## <a name="toosearch-and-filter-properties"></a><span data-ttu-id="7a378-190">właściwości toosearch i filtru</span><span class="sxs-lookup"><span data-stu-id="7a378-190">toosearch and filter properties</span></span>
<span data-ttu-id="7a378-191">Witaj **właściwości** karta zawiera wyszukiwania i filtrowania toohelp możliwości zarządzania właściwości.</span><span class="sxs-lookup"><span data-stu-id="7a378-191">hello **Properties** tab includes searching and filtering capabilities toohelp you manage your properties.</span></span> <span data-ttu-id="7a378-192">Lista właściwości hello toofilter według nazwy właściwości, wprowadź wyszukiwany termin w hello **wyszukiwania właściwości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="7a378-192">toofilter hello property list by property name, enter a search term in hello **Search property** textbox.</span></span> <span data-ttu-id="7a378-193">Wyczyść wszystkie właściwości toodisplay hello **wyszukiwania właściwości** pole tekstowe i naciśnij klawisz enter.</span><span class="sxs-lookup"><span data-stu-id="7a378-193">toodisplay all properties, clear hello **Search property** textbox and press enter.</span></span>

![Wyszukiwanie][api-management-properties-search]

<span data-ttu-id="7a378-195">Lista właściwości hello toofilter przez wartości tagów wprowadzić jeden lub więcej tagów w hello **Filtruj według znaczników** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="7a378-195">toofilter hello property list by tag values, enter one or more tags into hello **Filter by tags** textbox.</span></span> <span data-ttu-id="7a378-196">Wyczyść wszystkie właściwości toodisplay hello **Filtruj według znaczników** pole tekstowe i naciśnij klawisz enter.</span><span class="sxs-lookup"><span data-stu-id="7a378-196">toodisplay all properties, clear hello **Filter by tags** textbox and press enter.</span></span>

![Filtr][api-management-properties-filter]

## <a name="next-steps"></a><span data-ttu-id="7a378-198">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7a378-198">Next steps</span></span>
* <span data-ttu-id="7a378-199">Dowiedz się więcej o pracy z zasadami</span><span class="sxs-lookup"><span data-stu-id="7a378-199">Learn more about working with policies</span></span>
  * [<span data-ttu-id="7a378-200">Zasady w usłudze API Management</span><span class="sxs-lookup"><span data-stu-id="7a378-200">Policies in API Management</span></span>](api-management-howto-policies.md)
  * [<span data-ttu-id="7a378-201">Dokumentacja zasad</span><span class="sxs-lookup"><span data-stu-id="7a378-201">Policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [<span data-ttu-id="7a378-202">Wyrażenia zasad</span><span class="sxs-lookup"><span data-stu-id="7a378-202">Policy expressions</span></span>](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="7a378-203">Obejrzyj film wideo</span><span class="sxs-lookup"><span data-stu-id="7a378-203">Watch a video overview</span></span>
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

