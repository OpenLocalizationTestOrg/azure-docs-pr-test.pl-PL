---
title: aaaSchema aktualizuje czerwca-1-2016 - Azure Logic Apps | Dokumentacja firmy Microsoft
description: "Utworzenie definicji JSON dla usługi Azure Logic Apps z wersją schematu 2016-06-01"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 349d57e8-f62b-4ec6-a92f-a6e0242d6c0e
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/25/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: b0347fbbd692a93b63a2f8b741402a225450b35a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a><span data-ttu-id="40102-103">Aktualizacje schematu dla usługi Azure Logic Apps — 1 czerwca 2016 r.</span><span class="sxs-lookup"><span data-stu-id="40102-103">Schema updates for Azure Logic Apps - June 1, 2016</span></span>

<span data-ttu-id="40102-104">Tego nowego schematu i interfejsu API w wersji dla usługi Azure Logic Apps zawiera kluczowe ulepszenia lepiej aplikacje logiki niezawodnych i łatwiejsze toouse:</span><span class="sxs-lookup"><span data-stu-id="40102-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier toouse:</span></span>

* <span data-ttu-id="40102-105">[Zakresy](#scopes) można zagnieździć działania jako zbiór akcji lub grupy.</span><span class="sxs-lookup"><span data-stu-id="40102-105">[Scopes](#scopes) let you group or nest actions as a collection of actions.</span></span>
* <span data-ttu-id="40102-106">[Warunkach i pętlach](#conditions-loops) są teraz akcje najwyższej jakości.</span><span class="sxs-lookup"><span data-stu-id="40102-106">[Conditions and loops](#conditions-loops) are now first-class actions.</span></span>
* <span data-ttu-id="40102-107">Bardziej dokładne kolejności uruchamianie działań z hello `runAfter` właściwości, zastępując`dependsOn`</span><span class="sxs-lookup"><span data-stu-id="40102-107">More precise ordering for running actions with hello `runAfter` property, replacing `dependsOn`</span></span>

<span data-ttu-id="40102-108">tooupgrade aplikacji logiki z hello 1 sierpnia 2015 preview schematu 1 czerwca 2016 toohello schematu, [wyewidencjonować sekcja uaktualnienie hello](##upgrade-your-schema).</span><span class="sxs-lookup"><span data-stu-id="40102-108">tooupgrade your logic apps from hello August 1, 2015 preview schema toohello June 1, 2016 schema, [check out hello upgrade section](##upgrade-your-schema).</span></span>

<a name="scopes"></a>
## <a name="scopes"></a><span data-ttu-id="40102-109">Zakresy</span><span class="sxs-lookup"><span data-stu-id="40102-109">Scopes</span></span>

<span data-ttu-id="40102-110">Ten schemat zawiera zakresy, które pozwalają grupy razem lub zagnieżdżania operacje wewnątrz siebie.</span><span class="sxs-lookup"><span data-stu-id="40102-110">This schema includes scopes, which let you group actions together, or nest actions inside each other.</span></span> <span data-ttu-id="40102-111">Na przykład warunek może zawierać inny warunek.</span><span class="sxs-lookup"><span data-stu-id="40102-111">For example, a condition can contain another condition.</span></span> <span data-ttu-id="40102-112">Dowiedz się więcej o [zakres składni](../logic-apps/logic-apps-loops-and-scopes.md), lub przejrzyj w tym przykładzie zakres podstawowe:</span><span class="sxs-lookup"><span data-stu-id="40102-112">Learn more about [scope syntax](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic scope example:</span></span>

```
{
    "actions": {
        "My_Scope": {
            "type": "scope",
            "actions": {                
                "Http": {
                    "inputs": {
                        "method": "GET",
                        "uri": "http://www.bing.com"
                    },
                    "runAfter": {},
                    "type": "Http"
                }
            }
        }
    }
}
```

<a name="conditions-loops"></a>
## <a name="conditions-and-loops-changes"></a><span data-ttu-id="40102-113">Zmiany w warunkach i pętlach</span><span class="sxs-lookup"><span data-stu-id="40102-113">Conditions and loops changes</span></span>

<span data-ttu-id="40102-114">W schemacie poprzedniej wersji, warunkach i pętlach zostały parametrów skojarzonych z jednej akcji.</span><span class="sxs-lookup"><span data-stu-id="40102-114">In previous schema versions, conditions and loops were parameters associated with a single action.</span></span> <span data-ttu-id="40102-115">Ten schemat podnosi to ograniczenie, więc warunkach i pętlach są teraz wyświetlane jako typów akcji.</span><span class="sxs-lookup"><span data-stu-id="40102-115">This schema lifts this limitation, so conditions and loops now appear as action types.</span></span> <span data-ttu-id="40102-116">Dowiedz się więcej o [pętli i zakresy](../logic-apps/logic-apps-loops-and-scopes.md), lub przejrzyj to prosty przykład dla warunku akcji:</span><span class="sxs-lookup"><span data-stu-id="40102-116">Learn more about [loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic example for a condition action:</span></span>

```
{
    "If_trigger_is_some-trigger": {
        "type": "If",
        "expression": "@equals(triggerBody(), 'some-trigger')",
        "runAfter": { },
        "actions": {
            "Http_2": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://www.bing.com"
                },
                "runAfter": {},
                "type": "Http"
            }
        },
        "else": 
        {
            "if_trigger_is_another-trigger": "..."
        }      
    }
}
```

<a name="run-after"></a>
## <a name="runafter-property"></a><span data-ttu-id="40102-117">Właściwość "runAfter"</span><span class="sxs-lookup"><span data-stu-id="40102-117">'runAfter' property</span></span>

<span data-ttu-id="40102-118">Witaj `runAfter` zamienia właściwość `dependsOn`, zapewniających większą dokładność po określeniu kolejności hello uruchomienia dla akcji na podstawie hello stanu z poprzedniej akcji.</span><span class="sxs-lookup"><span data-stu-id="40102-118">hello `runAfter` property replaces `dependsOn`, providing more precision when you specify hello run order for actions based on hello status of previous actions.</span></span>

<span data-ttu-id="40102-119">Witaj `dependsOn` właściwości synonimem "hello akcji uruchomienie i było pomyślne", niezależnie od tego, ile razy chciał tooexecute działania oparte na czy hello poprzedniej akcji zakończyło się powodzeniem, nie powiodło się lub pominięte.</span><span class="sxs-lookup"><span data-stu-id="40102-119">hello `dependsOn` property was synonymous with "hello action ran and was successful", no matter how many times you wanted tooexecute an action, based on whether hello previous action was successful, failed, or skipped.</span></span> <span data-ttu-id="40102-120">Witaj `runAfter` właściwości zapewnia elastyczność, że jako obiekt, który określa hello wszystkie nazwy akcji, po których hello obiektu działa.</span><span class="sxs-lookup"><span data-stu-id="40102-120">hello `runAfter` property provides that flexibility as an object that specifies all hello action names after which hello object runs.</span></span> <span data-ttu-id="40102-121">Ta właściwość definiuje również tablicę stany, które są akceptowane jako wyzwalacze.</span><span class="sxs-lookup"><span data-stu-id="40102-121">This property also defines an array of statuses that are acceptable as triggers.</span></span> <span data-ttu-id="40102-122">Na przykład, jeśli chce toorun po krok zakończy się pomyślnie, a także po kroku B pomyślnym lub niepomyślnym, możesz utworzyć to `runAfter` właściwości:</span><span class="sxs-lookup"><span data-stu-id="40102-122">For example, if you wanted toorun after step A succeeds and also after step B succeeds or fails, you construct this `runAfter` property:</span></span>

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a><span data-ttu-id="40102-123">Uaktualnienia schematu do</span><span class="sxs-lookup"><span data-stu-id="40102-123">Upgrade your schema</span></span>

<span data-ttu-id="40102-124">Uaktualnianie toohello nowego schematu trwa tylko kilka kroków.</span><span class="sxs-lookup"><span data-stu-id="40102-124">Upgrading toohello new schema only takes a few steps.</span></span> <span data-ttu-id="40102-125">Witaj procesu uaktualniania zawiera uruchomienie skryptu uaktualniania hello, zapisywanie jako nową aplikację logiki, a jeśli chcesz, prawdopodobnie zastępowanie hello poprzedniej aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="40102-125">hello upgrade process includes running hello upgrade script, saving as a new logic app, and if you want, possibly overwriting hello previous logic app.</span></span>

1. <span data-ttu-id="40102-126">Hello portalu Azure Otwórz aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="40102-126">In hello Azure portal, open your logic app.</span></span>

2. <span data-ttu-id="40102-127">Przejdź za**omówienie**.</span><span class="sxs-lookup"><span data-stu-id="40102-127">Go too**Overview**.</span></span> <span data-ttu-id="40102-128">Na pasku narzędzi aplikacji logiki hello, wybierz **Aktualizuj schemat**.</span><span class="sxs-lookup"><span data-stu-id="40102-128">On hello logic app toolbar, choose **Update Schema**.</span></span>
   
    ![Wybierz pozycję Aktualizuj schemat][1]
   
    <span data-ttu-id="40102-130">Witaj uaktualnionego definicji jest zwracany, który możesz skopiować i wkleić do definicji zasobu, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="40102-130">hello upgraded definition is returned, which you can copy and paste into a resource definition if necessary.</span></span> 
    <span data-ttu-id="40102-131">Jednak firma Microsoft **zdecydowanie zaleca się** wybierzesz **Zapisz jako** toomake się, że wszystkie odwołania połączenia są prawidłowe w hello uaktualnienia aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="40102-131">However, we **strongly recommend** you choose **Save As** toomake sure that all connection references are valid in hello upgraded logic app.</span></span>

3. <span data-ttu-id="40102-132">Hello uaktualnienia bloku narzędzi wybierz **Zapisz jako**.</span><span class="sxs-lookup"><span data-stu-id="40102-132">In hello upgrade blade toolbar, choose **Save As**.</span></span>

4. <span data-ttu-id="40102-133">Wprowadź nazwę logiki hello i stanu.</span><span class="sxs-lookup"><span data-stu-id="40102-133">Enter hello logic name and status.</span></span> <span data-ttu-id="40102-134">toodeploy aplikację logiki uaktualnionego wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="40102-134">toodeploy your upgraded logic app, choose **Create**.</span></span>

5. <span data-ttu-id="40102-135">Upewnij się, że aplikację logiki uaktualnionego działa zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="40102-135">Confirm that your upgraded logic app works as expected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="40102-136">Jeśli używasz wyzwalacz ręczny lub żądanie adresu URL wywołania zwrotnego hello zmiany w nowej aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="40102-136">If you are using a manual or request trigger, hello callback URL changes in your new logic app.</span></span> <span data-ttu-id="40102-137">Testu hello nowego adresu URL toomake się hello end-to-end środowisko działa.</span><span class="sxs-lookup"><span data-stu-id="40102-137">Test hello new URL toomake sure hello end-to-end experience works.</span></span> <span data-ttu-id="40102-138">adresy URL poprzedniej toopreserve, można sklonować za pośrednictwem istniejących aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="40102-138">toopreserve previous URLs, you can clone over your existing logic app.</span></span>

6. <span data-ttu-id="40102-139">*Opcjonalne* toooverwrite poprzedniej aplikacji logiki z hello nowej wersji schematu, na pasku narzędzi hello, wybierz **klonowania**, dalej zbyt**Aktualizuj schemat**.</span><span class="sxs-lookup"><span data-stu-id="40102-139">*Optional* toooverwrite your previous logic app with hello new schema version, on hello toolbar, choose **Clone**, next too**Update Schema**.</span></span> <span data-ttu-id="40102-140">Ten krok jest niezbędny, jeśli nie chcesz tookeep hello tego samego Identyfikatora lub żądania wyzwalacza adresu URL zasobu aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="40102-140">This step is necessary only if you want tookeep hello same resource ID or request trigger URL of your logic app.</span></span>

### <a name="upgrade-tool-notes"></a><span data-ttu-id="40102-141">Narzędzie uaktualniania uwagi</span><span class="sxs-lookup"><span data-stu-id="40102-141">Upgrade tool notes</span></span>

#### <a name="mapping-conditions"></a><span data-ttu-id="40102-142">Mapowanie warunków</span><span class="sxs-lookup"><span data-stu-id="40102-142">Mapping conditions</span></span>

<span data-ttu-id="40102-143">W definicji hello uaktualnić narzędzie hello sprawia, że optymalnego na grupowanie akcji gałęzi true i false jako zakres.</span><span class="sxs-lookup"><span data-stu-id="40102-143">In hello upgraded definition, hello tool makes a best effort at grouping true and false branch actions together as a scope.</span></span> <span data-ttu-id="40102-144">W szczególności hello projektanta wzorzec `@equals(actions('a').status, 'Skipped')` powinny się wyświetlać jako `else` akcji.</span><span class="sxs-lookup"><span data-stu-id="40102-144">Specifically, hello designer pattern of `@equals(actions('a').status, 'Skipped')` should appear as an `else` action.</span></span> <span data-ttu-id="40102-145">Jeśli jednak narzędzie hello wykryje nierozpoznawalną wzorców, narzędzie hello może utworzyć osobne warunki hello true i gałąź fałszu hello.</span><span class="sxs-lookup"><span data-stu-id="40102-145">However, if hello tool detects unrecognizable patterns, hello tool might create separate conditions for both hello true and hello false branch.</span></span> <span data-ttu-id="40102-146">W razie potrzeby można ponownie zamapować akcje po uaktualnieniu.</span><span class="sxs-lookup"><span data-stu-id="40102-146">You can remap actions after upgrading, if necessary.</span></span>

#### <a name="foreach-loop-with-condition"></a><span data-ttu-id="40102-147">Pętla "foreach" z warunkiem</span><span class="sxs-lookup"><span data-stu-id="40102-147">'foreach' loop with condition</span></span>

<span data-ttu-id="40102-148">W nowym schematem hello, można użyć hello filtru akcji tooreplicate hello wzorzec `foreach` pętli z warunkiem dla każdego elementu, ale ta zmiana automatycznie powinno się zdarzyć w przypadku uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="40102-148">In hello new schema, you can use hello filter action tooreplicate hello pattern of a `foreach` loop with a condition per item, but this change should automatically happen when you upgrade.</span></span> <span data-ttu-id="40102-149">warunek Hello jest akcję filtru przed hello pętli foreach dla tylko tablicę elementów spełniających warunek hello i tablicy jest przekazywany do akcji foreach hello.</span><span class="sxs-lookup"><span data-stu-id="40102-149">hello condition becomes a filter action before hello foreach loop for returning only an array of items that match hello condition, and that array is passed into hello foreach action.</span></span> <span data-ttu-id="40102-150">Na przykład zobacz [pętli i zakresy](../logic-apps/logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="40102-150">For an example, see [Loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md).</span></span>

#### <a name="resource-tags"></a><span data-ttu-id="40102-151">Tagi zasobów</span><span class="sxs-lookup"><span data-stu-id="40102-151">Resource tags</span></span>

<span data-ttu-id="40102-152">Po uaktualnieniu, tagi zasobów są usuwane, dlatego należy je zresetować hello uaktualnione przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="40102-152">After you upgrade, resource tags are removed, so you must reset them for hello upgraded workflow.</span></span>

## <a name="other-changes"></a><span data-ttu-id="40102-153">Inne zmiany</span><span class="sxs-lookup"><span data-stu-id="40102-153">Other changes</span></span>

### <a name="renamed-manual-trigger-toorequest-trigger"></a><span data-ttu-id="40102-154">Zmieniono jego nazwę wyzwalacza "manual" too'request "wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="40102-154">Renamed 'manual' trigger too'request' trigger</span></span>

<span data-ttu-id="40102-155">Witaj `manual` typ wyzwalacza została zastąpiona i zmienić jej nazwy zbyt`request` z typem `http`.</span><span class="sxs-lookup"><span data-stu-id="40102-155">hello `manual` trigger type was deprecated and renamed too`request` with type `http`.</span></span> <span data-ttu-id="40102-156">Ta zmiana tworzy więcej spójności hello rodzaj wzorzec, który hello wyzwalacza jest używane toobuild.</span><span class="sxs-lookup"><span data-stu-id="40102-156">This change creates more consistency for hello kind of pattern that hello trigger is used toobuild.</span></span>

### <a name="new-filter-action"></a><span data-ttu-id="40102-157">Nowa akcja "filtr.</span><span class="sxs-lookup"><span data-stu-id="40102-157">New 'filter' action</span></span>

<span data-ttu-id="40102-158">toofilter dużą tablicę dół tooa mniejszy zestaw elementów, nowych hello `filter` typu akceptuje tablicy i warunku, ocenia hello warunek dla każdego elementu i zwraca tablicę z elementami spełniających warunek hello.</span><span class="sxs-lookup"><span data-stu-id="40102-158">toofilter a large array down tooa smaller set of items, hello new `filter` type accepts an array and a condition, evaluates hello condition for each item, and returns an array with items meeting hello condition.</span></span>

### <a name="restrictions-for-foreach-and-until-actions"></a><span data-ttu-id="40102-159">Ograniczenia dla "foreach" i "do" Akcje</span><span class="sxs-lookup"><span data-stu-id="40102-159">Restrictions for 'foreach' and 'until' actions</span></span>

<span data-ttu-id="40102-160">Witaj `foreach` i `until` pętli są ograniczone tooa jednej akcji.</span><span class="sxs-lookup"><span data-stu-id="40102-160">hello `foreach` and `until` loop are restricted tooa single action.</span></span>

### <a name="new-trackedproperties-for-actions"></a><span data-ttu-id="40102-161">Nowy "trackedProperties" dla akcji</span><span class="sxs-lookup"><span data-stu-id="40102-161">New 'trackedProperties' for actions</span></span>

<span data-ttu-id="40102-162">Akcje teraz może zawierać dodatkowe właściwości o nazwie `trackedProperties`, która jest element równorzędny toohello `runAfter` i `type` właściwości.</span><span class="sxs-lookup"><span data-stu-id="40102-162">Actions can now have an additional property called `trackedProperties`, which is sibling toohello `runAfter` and `type` properties.</span></span> <span data-ttu-id="40102-163">Ten obiekt określa niektórych danych wejściowych działania lub danych wyjściowych, które mają tooinclude w hello Azure diagnostycznych telemetrii, emitowane w ramach przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="40102-163">This object specifies certain action inputs or outputs that you want tooinclude in hello Azure Diagnostic telemetry, emitted as part of a workflow.</span></span> <span data-ttu-id="40102-164">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="40102-164">For example:</span></span>

```
{                
    "Http": {
        "inputs": {
            "method": "GET",
            "uri": "http://www.bing.com"
        },
        "runAfter": {},
        "type": "Http",
        "trackedProperties": {
            "responseCode": "@action().outputs.statusCode",
            "uri": "@action().inputs.uri"
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="40102-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="40102-165">Next Steps</span></span>
* [<span data-ttu-id="40102-166">Tworzenie definicji przepływu pracy dla usługi logic apps</span><span class="sxs-lookup"><span data-stu-id="40102-166">Create workflow definitions for logic apps</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="40102-167">Utwórz szablony wdrażania dla usługi logic apps</span><span class="sxs-lookup"><span data-stu-id="40102-167">Create deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
