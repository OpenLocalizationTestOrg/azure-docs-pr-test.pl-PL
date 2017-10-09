---
title: "aaaCreate, tworzenie i wdrażanie aplikacji logiki w Visual Studio — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Tworzenie projektów programu Visual Studio, projektowanie, tworzenie i wdrażanie usługi Azure Logic Apps."
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e484e5ce-77e9-4fa9-bcbe-f851b4eb42a6
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 2/14/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 5154cb05f9a48e9f0f2381a6953947217f7bb114
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a>Projektowanie, tworzenie i wdrażanie usługi Azure Logic Apps w programie Visual Studio

Mimo że hello [portalu Azure](https://portal.azure.com/) zapewnia to dobry sposób możesz toocreate i zarządzania usługi Azure Logic Apps, można użyć programu Visual Studio umożliwiające projektowanie, tworzenie i wdrażanie aplikacji logiki. Program Visual Studio udostępnia zaawansowane narzędzia, takie jak hello projektanta aplikacji logiki dla Ciebie aplikacje logiki toocreate, konfigurować szablony wdrażania i automatyzacji i wdrażania tooany środowiska. 

Dowiedz się tooget wprowadzenie do usługi Azure Logic Apps [jak toocreate pierwszej aplikacji logiki w portalu Azure hello](logic-apps-create-a-logic-app.md).

## <a name="installation-steps"></a>Kroki instalacji

tooinstall i Konfigurowanie narzędzi Visual Studio tools for Azure Logic Apps, wykonaj następujące kroki.

### <a name="prerequisites"></a>Wymagania wstępne

* [Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) lub programu Visual Studio 2015
* [Najnowszy zestaw Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 lub nowszej)
* [Azure PowerShell](https://github.com/Azure/azure-powershell#installation)
* Access toohello w sieci web używając projektanta osadzonych hello

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a>Instalowanie narzędzi Visual Studio tools for Azure Logic Apps

Po zainstalowaniu wymagań wstępnych hello:

1. Otwórz program Visual Studio. Na powitania **narzędzia** menu, wybierz opcję **rozszerzenia i aktualizacje**.
2. Rozwiń węzeł hello **Online** kategorii można wyszukiwać w tryb online.
3. Wyszukaj **Logic Apps** do momentu znalezienia **Azure Logic Apps Tools for Visual Studio**.
4. toodownload i rozszerzenie hello instalacji, kliknij przycisk **Pobierz**.
5. Po zakończeniu instalacji uruchom ponownie program Visual Studio.

> [!NOTE]
> Możesz również pobrać [narzędzia aplikacje logiki platformy Azure dla programu Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) i hello [narzędzia aplikacje logiki platformy Azure dla programu Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) bezpośrednio z hello Visual Studio Marketplace.

Po zakończeniu instalacji, używając hello projektu grupy zasobów platformy Azure za pomocą projektanta aplikacji logiki.

## <a name="create-your-project"></a>Tworzenie projektu

1. Na powitania **pliku** menu przejść za**nowy**i wybierz **projektu**. Lub tooadd Twojego tooan projektu zbyt istniejącego rozwiązania, przejdź**Dodaj**i wybierz **nowy projekt**.

    ![Menu Plik](./media/logic-apps-deploy-from-vs/filemenu.png)

2. W hello **nowy projekt** oknie Znajdź **chmury**i wybierz **grupy zasobów platformy Azure**. Nazwij swój projekt, a następnie kliknij przycisk **OK**.

    ![Dodaj nowy projekt](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. Wybierz hello **aplikacji logiki** szablonu, który utworzy szablon wdrażania aplikacji logiki puste toouse. Po wybraniu szablonu, kliknij przycisk **OK**.

    ![Wybierz szablon aplikacji logiki](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    Teraz dodane rozwiązania tooyour projektu aplikacji logiki. 
    W Eksploratorze rozwiązań hello powinna zostać wyświetlona pliku wdrożenia.

    ![Plik wdrożenia](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a>Tworzenie aplikacji logiki z projektanta aplikacji logiki

Jeśli projekt grupy zasobów platformy Azure, który zawiera aplikację logiki, możesz otworzyć hello projektanta aplikacji logiki w Visual Studio toocreate przepływu pracy. 

> [!NOTE]
> Projektant Hello wymaga połączenia internetowego za zapytania łączniki dla danych i dostępnych właściwości. Na przykład jeśli używany jest łącznik usługi Dynamics CRM Online hello, hello projektanta zapytań programu CRM wystąpienia tooshow dostępne niestandardowe i domyślne właściwości.

1. Kliknij prawym przyciskiem myszy użytkownika `<template>.json` pliku, a następnie wybierz **Otwórz w Projektancie aplikacji logiki**. (`Ctrl+L`)

2. Wybierz subskrypcję platformy Azure, grupy zasobów i lokalizacji szablonu wdrożenia.

    > [!NOTE]
    > Projektowanie aplikacji logiki tworzy połączenie z interfejsem API zasobów zapytania dla właściwości podczas projektowania. Visual Studio będzie korzystać z wybranego zasobu grupy toocreate te połączenia w czasie projektowania. tooview lub Zmień wszystkie połączenia interfejsu API, przejdź toohello portalu Azure i Przeglądaj w poszukiwaniu **połączenia interfejsu API**.

    ![Selektor subskrypcji](./media/logic-apps-deploy-from-vs/designer_picker.png)

    Projektant Hello używa definicji hello hello `<template>.json` pliku do renderowania.

4. Tworzenie i projektowanie aplikacji logiki. Szablon wdrożenia zostanie zaktualizowany z wprowadzonymi zmianami.

    ![Projektant aplikacji logiki w programie Visual Studio](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

Dodaje programu Visual Studio `Microsoft.Web/connections` zbyt zasobu pliku zasobów dla połączeń toofunction wymaga aplikacji logiki. Te właściwości połączenia można ustawić podczas wdrażania i zarządzania po wdrożeniu w **połączenia interfejsu API** w hello portalu Azure.

### <a name="switch-toojson-code-view"></a>Przełącz do widoku kodu tooJSON

Witaj tooshow reprezentacja JSON aplikacji logiki, wybierz hello **widoku kodu** u dołu hello hello projektanta.

tooswitch trybu toohello zasobów pełna JSON, kliknij prawym przyciskiem myszy hello `<template>.json` pliku, a następnie wybierz **Otwórz**.

### <a name="add-references-for-dependent-resources-toovisual-studio-deployment-templates"></a>Dodaj odwołania do zasobów zależnych tooVisual Studio wdrażania szablonów

Należy zasobów zależnych tooreference logikę aplikacji, można użyć [funkcje szablonu usługi Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) w szablonie wdrożenia aplikacji logiki. Na przykład można Twojej tooreference aplikacji logiki konta funkcji platformy Azure lub integracji, które mają toodeploy równolegle z aplikacji logiki. Wykonaj te wskazówki dotyczące jak parametry toouse w szablonie wdrożenia, który hello projektanta aplikacji logiki renderuje poprawnie. 

Można używać parametrów aplikacji logiki w rodzaju wyzwalacze i akcje:

*   Podrzędny przepływ pracy
*   Funkcja aplikacji
*   Wywołanie APIM
*   Adres URL wykonywania połączenia interfejsu API
*   Ścieżka połączenia interfejsu API

I możesz użyć funkcji szablonu, takie jak parametry, zmienne, resourceId, concat itp. Na przykład Oto jak można zastąpić identyfikator zasobu hello funkcji platformy Azure:

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

I użycia parametrów:

```
"MyFunction": {
    "type": "Function",
    "inputs": {
        "body":{},
        "function":{
            "id":"[resourceid('Microsoft.Web/sites/functions','functionApp',parameters('functionName'))]"
        }
    },
    "runAfter":{}
}
```
Innym przykładem mogą parametryzacja hello komunikat operacji wysyłania usługi Service Bus:

```
"Send_message": {
    "type": "ApiConnection",
        "inputs": {
            "host": {
                "connection": {
                    "name": "@parameters('$connections')['servicebus']['connectionId']"
                }
            },
            "method": "post",
            "path": "[concat('/@{encodeURIComponent(''', parameters('queueuname'), ''')}/messages')]",
            "body": {
                "ContentData": "@{base64(triggerBody())}"
            },
            "queries": {
                "systemProperties": "None"
            }
        },
        "runAfter": {}
    }
```
> [!NOTE] 
> host.runtimeUrl jest opcjonalny i może być usunięty z szablonu, jeśli jest obecny.
> 


> [!NOTE] 
> Dla toowork projektanta aplikacji logiki hello użycia parametrów, należy podać wartości domyślnych, na przykład:
> 
> ```
> "parameters": {
>     "IntegrationAccount": {
>     "type":"string",
>     "minLength":1,
>     "defaultValue":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.Logic/integrationAccounts/<integrationAccountName>"
>     }
> },
> ```

### <a name="save-your-logic-app"></a>Zapisywanie aplikacji logiki

toosave aplikację logiki w dowolnym momencie, przejdź zbyt**pliku** > **zapisać**. (`Ctrl+S`) 

Jeśli aplikację logiki ma błędy podczas zapisywania aplikacji, pojawią się one w Visual Studio hello **dane wyjściowe** okna.

## <a name="deploy-your-logic-app-from-visual-studio"></a>Wdrażanie aplikacji logiki w programie Visual Studio

Po skonfigurowaniu aplikacji, można wdrożyć bezpośrednio z programu Visual Studio w zaledwie kilku krokach. 

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt i przejść za**Wdróż** > **nowego wdrożenia...**

    ![Nowe wdrożenie](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. Po wyświetleniu monitu zaloguj się tooyour subskrypcji platformy Azure. 

3. Teraz musisz wybrać szczegóły hello grupy zasobów hello miejscu toodeploy aplikacji logiki. Gdy wszystko będzie gotowe, wybierz **Wdróż**.

    > [!NOTE]
    > Upewnij się, wybierz opcję hello prawidłowego szablonu i pliku parametrów hello grupy zasobów. Na przykład środowiska produkcyjnego tooa toodeploy należy wybrać pliku parametrów hello produkcji.

    ![Wdrożenie grupy tooresource](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    Stan wdrożenia Hello jest wyświetlany w hello **dane wyjściowe** okna. 
    Może być tooselect **inicjowania obsługi usługi Azure** w hello **Pokaż dane wyjściowe z** listy.

    ![Dane wyjściowe stanu wdrożenia](./media/logic-apps-deploy-from-vs/output.png)

W przyszłości hello można edytować aplikację logiki w kontroli źródła i użyj programu Visual Studio toodeploy nowe wersje.

> [!NOTE]
> W przypadku zmiany definicji hello w portalu Azure hello bezpośrednio te zmiany zostaną zastąpione podczas wdrażania w programie Visual Studio następnym razem. 

## <a name="add-your-logic-app-tooan-existing-resource-group-project"></a>Dodawanie logiki aplikacji tooan istniejącej grupy zasobów projektu

Jeśli masz istniejący projekt grupy zasobów, można dodać projektu toothat logiki aplikacji hello okna konspekt pliku JSON. Można również dodać inną aplikację logiki obok aplikacji hello, utworzonych wcześniej.

1. Otwórz hello `<template>.json` pliku.

2. tooopen hello okna konspekt pliku JSON, przejdź zbyt**widoku** > **inne okna** > **konspekt pliku JSON**.

3. Kliknij tooadd plik zasobów toohello szablonu **dodawania zasobów** u góry okna konspekt pliku JSON hello hello. Witaj okna konspekt pliku JSON, kliknij prawym przyciskiem myszy **zasobów**i wybierz **Dodaj nowy zasób**.

    ![Okna konspekt pliku JSON](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. W hello **dodawania zasobów** okno dialogowe, Znajdź i wybierz **aplikacji logiki**. Określ nazwę aplikacji logiki, a następnie wybierz pozycję **Dodaj**.

    ![Dodaj zasób](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a>Następne kroki

* [Zarządzanie logiki aplikacji za pomocą programu Visual Studio Cloud Explorer](logic-apps-manage-from-vs.md)
* [Wyświetlanie typowych przykładów i scenariuszy](logic-apps-examples-and-scenarios.md)
* [Dowiedz się, jak przetwarza tooautomate firm z usługą Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/T694)
* [Dowiedz się, jak toointegrate systemy z usługą Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462)
