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
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a>Aktualizacje schematu dla usługi Azure Logic Apps — 1 czerwca 2016 r.

Tego nowego schematu i interfejsu API w wersji dla usługi Azure Logic Apps zawiera kluczowe ulepszenia lepiej aplikacje logiki niezawodnych i łatwiejsze toouse:

* [Zakresy](#scopes) można zagnieździć działania jako zbiór akcji lub grupy.
* [Warunkach i pętlach](#conditions-loops) są teraz akcje najwyższej jakości.
* Bardziej dokładne kolejności uruchamianie działań z hello `runAfter` właściwości, zastępując`dependsOn`

tooupgrade aplikacji logiki z hello 1 sierpnia 2015 preview schematu 1 czerwca 2016 toohello schematu, [wyewidencjonować sekcja uaktualnienie hello](##upgrade-your-schema).

<a name="scopes"></a>
## <a name="scopes"></a>Zakresy

Ten schemat zawiera zakresy, które pozwalają grupy razem lub zagnieżdżania operacje wewnątrz siebie. Na przykład warunek może zawierać inny warunek. Dowiedz się więcej o [zakres składni](../logic-apps/logic-apps-loops-and-scopes.md), lub przejrzyj w tym przykładzie zakres podstawowe:

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
## <a name="conditions-and-loops-changes"></a>Zmiany w warunkach i pętlach

W schemacie poprzedniej wersji, warunkach i pętlach zostały parametrów skojarzonych z jednej akcji. Ten schemat podnosi to ograniczenie, więc warunkach i pętlach są teraz wyświetlane jako typów akcji. Dowiedz się więcej o [pętli i zakresy](../logic-apps/logic-apps-loops-and-scopes.md), lub przejrzyj to prosty przykład dla warunku akcji:

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
## <a name="runafter-property"></a>Właściwość "runAfter"

Witaj `runAfter` zamienia właściwość `dependsOn`, zapewniających większą dokładność po określeniu kolejności hello uruchomienia dla akcji na podstawie hello stanu z poprzedniej akcji.

Witaj `dependsOn` właściwości synonimem "hello akcji uruchomienie i było pomyślne", niezależnie od tego, ile razy chciał tooexecute działania oparte na czy hello poprzedniej akcji zakończyło się powodzeniem, nie powiodło się lub pominięte. Witaj `runAfter` właściwości zapewnia elastyczność, że jako obiekt, który określa hello wszystkie nazwy akcji, po których hello obiektu działa. Ta właściwość definiuje również tablicę stany, które są akceptowane jako wyzwalacze. Na przykład, jeśli chce toorun po krok zakończy się pomyślnie, a także po kroku B pomyślnym lub niepomyślnym, możesz utworzyć to `runAfter` właściwości:

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a>Uaktualnienia schematu do

Uaktualnianie toohello nowego schematu trwa tylko kilka kroków. Witaj procesu uaktualniania zawiera uruchomienie skryptu uaktualniania hello, zapisywanie jako nową aplikację logiki, a jeśli chcesz, prawdopodobnie zastępowanie hello poprzedniej aplikacji logiki.

1. Hello portalu Azure Otwórz aplikację logiki.

2. Przejdź za**omówienie**. Na pasku narzędzi aplikacji logiki hello, wybierz **Aktualizuj schemat**.
   
    ![Wybierz pozycję Aktualizuj schemat][1]
   
    Witaj uaktualnionego definicji jest zwracany, który możesz skopiować i wkleić do definicji zasobu, jeśli to konieczne. 
    Jednak firma Microsoft **zdecydowanie zaleca się** wybierzesz **Zapisz jako** toomake się, że wszystkie odwołania połączenia są prawidłowe w hello uaktualnienia aplikacji logiki.

3. Hello uaktualnienia bloku narzędzi wybierz **Zapisz jako**.

4. Wprowadź nazwę logiki hello i stanu. toodeploy aplikację logiki uaktualnionego wybierz **Utwórz**.

5. Upewnij się, że aplikację logiki uaktualnionego działa zgodnie z oczekiwaniami.
   
   > [!NOTE]
   > Jeśli używasz wyzwalacz ręczny lub żądanie adresu URL wywołania zwrotnego hello zmiany w nowej aplikacji logiki. Testu hello nowego adresu URL toomake się hello end-to-end środowisko działa. adresy URL poprzedniej toopreserve, można sklonować za pośrednictwem istniejących aplikacji logiki.

6. *Opcjonalne* toooverwrite poprzedniej aplikacji logiki z hello nowej wersji schematu, na pasku narzędzi hello, wybierz **klonowania**, dalej zbyt**Aktualizuj schemat**. Ten krok jest niezbędny, jeśli nie chcesz tookeep hello tego samego Identyfikatora lub żądania wyzwalacza adresu URL zasobu aplikacji logiki.

### <a name="upgrade-tool-notes"></a>Narzędzie uaktualniania uwagi

#### <a name="mapping-conditions"></a>Mapowanie warunków

W definicji hello uaktualnić narzędzie hello sprawia, że optymalnego na grupowanie akcji gałęzi true i false jako zakres. W szczególności hello projektanta wzorzec `@equals(actions('a').status, 'Skipped')` powinny się wyświetlać jako `else` akcji. Jeśli jednak narzędzie hello wykryje nierozpoznawalną wzorców, narzędzie hello może utworzyć osobne warunki hello true i gałąź fałszu hello. W razie potrzeby można ponownie zamapować akcje po uaktualnieniu.

#### <a name="foreach-loop-with-condition"></a>Pętla "foreach" z warunkiem

W nowym schematem hello, można użyć hello filtru akcji tooreplicate hello wzorzec `foreach` pętli z warunkiem dla każdego elementu, ale ta zmiana automatycznie powinno się zdarzyć w przypadku uaktualnienia. warunek Hello jest akcję filtru przed hello pętli foreach dla tylko tablicę elementów spełniających warunek hello i tablicy jest przekazywany do akcji foreach hello. Na przykład zobacz [pętli i zakresy](../logic-apps/logic-apps-loops-and-scopes.md).

#### <a name="resource-tags"></a>Tagi zasobów

Po uaktualnieniu, tagi zasobów są usuwane, dlatego należy je zresetować hello uaktualnione przepływu pracy.

## <a name="other-changes"></a>Inne zmiany

### <a name="renamed-manual-trigger-toorequest-trigger"></a>Zmieniono jego nazwę wyzwalacza "manual" too'request "wyzwalacza

Witaj `manual` typ wyzwalacza została zastąpiona i zmienić jej nazwy zbyt`request` z typem `http`. Ta zmiana tworzy więcej spójności hello rodzaj wzorzec, który hello wyzwalacza jest używane toobuild.

### <a name="new-filter-action"></a>Nowa akcja "filtr.

toofilter dużą tablicę dół tooa mniejszy zestaw elementów, nowych hello `filter` typu akceptuje tablicy i warunku, ocenia hello warunek dla każdego elementu i zwraca tablicę z elementami spełniających warunek hello.

### <a name="restrictions-for-foreach-and-until-actions"></a>Ograniczenia dla "foreach" i "do" Akcje

Witaj `foreach` i `until` pętli są ograniczone tooa jednej akcji.

### <a name="new-trackedproperties-for-actions"></a>Nowy "trackedProperties" dla akcji

Akcje teraz może zawierać dodatkowe właściwości o nazwie `trackedProperties`, która jest element równorzędny toohello `runAfter` i `type` właściwości. Ten obiekt określa niektórych danych wejściowych działania lub danych wyjściowych, które mają tooinclude w hello Azure diagnostycznych telemetrii, emitowane w ramach przepływu pracy. Na przykład:

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

## <a name="next-steps"></a>Następne kroki
* [Tworzenie definicji przepływu pracy dla usługi logic apps](../logic-apps/logic-apps-author-definitions.md)
* [Utwórz szablony wdrażania dla usługi logic apps](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
