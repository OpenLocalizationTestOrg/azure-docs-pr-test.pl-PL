---
title: "rozwiązania do zarządzania aaaCreating w Operations Management Suite (OMS) | Dokumentacja firmy Microsoft"
description: "Rozwiązania do zarządzania rozszerzyć funkcjonalność hello z Operations Management Suite (OMS), zapewniając scenariusze zarządzania spakowanych dodać obszar roboczy OMS tootheir klientów.  Ten artykuł zawiera szczegóły dotyczące tworzenia toobe rozwiązań zarządzania używane we własnym środowisku lub wprowadzone dostępne tooyour klientów."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/30/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f408df1b21f519fd1eb2cbeb19cca18f6c4161f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a>Tworzenie pliku rozwiązania zarządzania w Operations Management Suite (OMS) (wersja zapoznawcza)
> [!NOTE]
> To jest wstępna dokumentacji do tworzenia rozwiązań do zarządzania w OMS, które są obecnie w wersji zapoznawczej. Żadnego schematu opisanych poniżej jest toochange podmiotu.  

Rozwiązania do zarządzania w Operations Management Suite (OMS) są zaimplementowane jako [szablonów Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md).  głównym zadaniem Hello się dowiedzieć, jak learning tooauthor rozwiązania do zarządzania w sposób zbyt[Tworzenie szablonu](../azure-resource-manager/resource-group-authoring-templates.md).  W tym artykule przedstawiono szczegóły unikatowy szablony używane dla rozwiązań i w jaki sposób tooconfigure rozwiązania typowych zasobów.


## <a name="tools"></a>Narzędzia

Można użyć dowolnego toowork Edytor tekstu z plików rozwiązania, ale zaleca się wykorzystaniu hello funkcje zawarte w Visual Studio lub Visual Studio Code, zgodnie z opisem w hello następujące artykuły.

- [Tworzenie i wdrażanie grup zasobów platformy Azure za pomocą programu Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [Praca z szablony usługi Azure Resource Manager w kodzie programu Visual Studio](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a>Struktura
Podstawowa struktura pliku rozwiązania zarządzania Hello jest hello sam, jak [szablonu usługi Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md#template-format) czyli w następujący sposób.  Każdy z poniższych rozdziałach hello opisano elementy najwyższego poziomu hello i i ich zawartość w rozwiązaniu.  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a>Parametry
[Parametry](../azure-resource-manager/resource-group-authoring-templates.md#parameters) to wartości, które wymagają od użytkownika hello, podczas instalacji hello rozwiązania do zarządzania.  Istnieją standardowe parametry, których wszystkie rozwiązania, a następnie można dodać dodatkowe parametry zgodnie z potrzebami dla określonego rozwiązania.  Jak użytkownicy będą podać wartości parametrów instalacji rozwiązanie będzie zależeć od określonego parametru hello i sposobu rozwiązania hello jest instalowany.

Kiedy użytkownik instaluje rozwiązania do zarządzania za pośrednictwem hello [portalu Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) lub [szablonów Szybki Start Azure](operations-management-suite-solutions.md#finding-and-installing-management-solutions) są zostanie wyświetlony monit o tooselect [OMS obszaru roboczego i konta automatyzacji ](operations-management-suite-solutions.md#oms-workspace-and-automation-account).  Są używane toopopulate hello wartości każdego hello standardowe parametry.  Witaj, użytkownik nie jest monitowany toodirectly Podaj wartości parametrów standardowe hello, ale są one tooprovide zostanie wyświetlony monit o wartości żadnych parametrów.

Po zainstalowaniu przez użytkownika hello rozwiązania [innej metody](operations-management-suite-solutions.md#finding-and-installing-management-solutions), użytkownik musi podać wartość dla wszystkich parametrów standardowe i wszystkie dodatkowe parametry.

Poniżej przedstawiono przykładowe parametru.  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

Witaj w poniższej tabeli opisano atrybuty hello parametru.

| Atrybut | Opis |
|:--- |:--- |
| type |Typ danych parametru hello. kontrolki wprowadzania Hello wyświetlane dla użytkownika hello zależy od typu danych hello.<br><br>bool — menu rozwijane<br>ciąg — pole tekstowe<br>int — pole tekstowe<br>SecureString — pole hasła<br> |
| category |Kategoria opcjonalny parametr hello.  Parametry w tej samej kategorii są zgrupowane hello. |
| Formant |Dodatkowe funkcje dotyczące parametrów ciągu.<br><br>DATETIME — formant daty i godziny są wyświetlane.<br>Identyfikator GUID - wartości identyfikatora Guid jest generowany automatycznie i hello parametru nie jest wyświetlany. |
| description |Opcjonalny opis dla parametru hello.  Wyświetlane informacje dymek dalej toohello parametr. |

### <a name="standard-parameters"></a>Standardowe parametry
Witaj poniższej tabeli wymieniono hello standardowe parametry dla wszystkich rozwiązań zarządzania.  Te wartości zostaną wypełnione dla użytkownika hello zamiast monitowanie o rozwiązania jest zainstalowany za pomocą szablonów hello Azure Marketplace lub Szybki Start.  Witaj użytkownik musi podać wartości dla nich, jeśli rozwiązanie hello jest zainstalowana z innej metody.

> [!NOTE]
> Interfejs użytkownika Hello w szablonach hello Azure Marketplace i szybkiego startu oczekuje nazwy parametrów hello hello tabeli.  Jeśli używasz różne nazwy parametrów następnie hello użytkownik będzie monitowany dla nich, a nie zostaną one automatycznie wypełnione.
>
>

| Parametr | Typ | Opis |
|:--- |:--- |:--- |
| Nazwa konta |Ciąg |Nazwa konta automatyzacji Azure. |
| pricingTier |Ciąg |Warstwa cenowa obszaru roboczego analizy dzienników i konto usługi Automatyzacja Azure. |
| regionId |Ciąg |Region hello konto usługi Automatyzacja Azure. |
| Nazwa rozwiązania |Ciąg |Nazwa rozwiązania hello.  Jeśli wdrażasz rozwiązania za pomocą szablonów Szybki Start, następnie należy zdefiniować Nazwa rozwiązania jako parametr, można zdefiniować zamiast konieczności toospecify użytkownika hello, jeden ciąg. |
| workspaceName |Ciąg |Nazwa obszaru roboczego analizy dzienników. |
| workspaceRegionId |Ciąg |Region hello obszaru roboczego analizy dzienników. |


Poniżej znajduje się hello struktury hello standardowe parametry, które można skopiować i wkleić do pliku rozwiązania.  

    "parameters": {
        "workspaceName": {
            "type": "string",
            "metadata": {
                "description": "A valid Log Analytics workspace name"
            }
        },
        "accountName": {
               "type": "string",
               "metadata": {
                   "description": "A valid Azure Automation account name"
               }
        },
        "workspaceRegionId": {
               "type": "string",
               "metadata": {
                   "description": "Region of hello Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of hello Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


W przypadku odwoływania się wartości tooparameter w innych elementach rozwiązania hello ze składnią hello **(parametr name) parametrów**.  Na przykład tooaccess hello nazwa obszaru roboczego, należy użyć **parameters('workspaceName')**

## <a name="variables"></a>Zmienne
[Zmienne](../azure-resource-manager/resource-group-authoring-templates.md#variables) wartości, które będą używane w rest hello hello rozwiązania do zarządzania.  Te wartości są uwidocznione toohello Użytkownik instalujący hello rozwiązania.  Są one przeznaczone tooprovide hello autora z jednej lokalizacji, w którym można zarządzać wartości, które mogą być używane wielokrotnie w całym rozwiązaniu hello. Żadne rozwiązanie tooyour określonej wartości należy umieścić w zmiennych jako min. toohard generowanie kodu hello **zasobów** elementu.  To czytelność kodu hello i pozwala tooeasily zmiany tych wartości w nowszych wersjach.

Poniżej przedstawiono przykład **zmienne** element z typowych parametrów używanych w rozwiązaniach.

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

Zobacz toovariable wartości za pośrednictwem rozwiązania hello ze składnią hello **zmienne ("Nazwa zmiennej")**.  Na przykład tooaccess hello zmiennej Nazwa rozwiązania, należy użyć **variables('SolutionName')**.

Można również zdefiniować złożone zmienne ustawia wiele wartości.  Są to szczególnie przydatne w rozwiązaniach do zarządzania gdzie definiujesz wiele właściwości dla różnych typów zasobów.  Można na przykład restrukturyzacji zmienne rozwiązania hello pokazanym powyżej toohello poniżej.

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

W takim przypadku można znaleźć wartości toovariable za pośrednictwem rozwiązania hello ze składnią hello **variables('variable name').property**.  Na przykład tooaccess hello zmienna nazwy rozwiązania, należy użyć **variables('Solution'). Nazwa**.

## <a name="resources"></a>Zasoby
[Zasoby](../azure-resource-manager/resource-group-authoring-templates.md#resources) zdefiniuj hello różne zasoby, które zainstaluje i skonfiguruje rozwiązania do zarządzania.  Są to hello największy i najbardziej złożonych część hello szablonu.  Można uzyskać hello struktury i pełny opis elementów zasobów w [szablonów Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md#resources).  Różne zasoby zdefiniowane przez użytkownika będzie zazwyczaj są wyszczególnione w inne artykuły w tej dokumentacji. 


### <a name="dependencies"></a>Zależności
Witaj **dependsOn** określa elementy [zależności](../azure-resource-manager/resource-group-define-dependencies.md) na inny zasób.  Po zainstalowaniu rozwiązania hello zasób nie został utworzony, dopóki wszystkie jego zależności zostały utworzone.  Na przykład może rozwiązania [uruchomienia elementu runbook](operations-management-suite-solutions-resources-automation.md#runbooks) po zainstalowaniu przy użyciu [zadania zasobu](operations-management-suite-solutions-resources-automation.md#automation-jobs).  Hello zasobów zadania będzie zależna od hello runbook zasobów toomake się, że ten element runbook hello został utworzony przed utworzeniem hello zadania.

### <a name="oms-workspace-and-automation-account"></a>Obszar roboczy OMS i konta automatyzacji
Rozwiązania do zarządzania wymagają [obszarem roboczym pakietu OMS](../log-analytics/log-analytics-manage-access.md) toocontain widoki i [konto automatyzacji](../automation/automation-security-overview.md#automation-account-overview) toocontain elementów runbook i powiązanych zasobów.  Muszą być dostępne przed hello zasobów w rozwiązaniu hello są tworzone i nie powinna być zdefiniowana w rozwiązaniu hello do samej siebie.  Witaj użytkownika będzie [Określ obszar roboczy i konta](operations-management-suite-solutions.md#oms-workspace-and-automation-account) podczas ich wdrażania rozwiązania, ale jako autor hello należy rozważyć następujące punkty hello.

## <a name="solution-resource"></a>Rozwiązanie zasobów
Każde rozwiązanie wymaga zapisu zasobów w hello **zasobów** element, który definiuje rozwiązania hello, sama.  Będzie to mieć typu **Microsoft.OperationsManagement/solutions** i mieć hello następujące struktury. Obejmuje to [standardowe parametry](#parameters) i [zmienne](#variables) które są najczęściej używanymi toodefine właściwości hello rozwiązania.


    {
      "name": "[concat(variables('Solution').Name, '[' ,parameters('workspacename'), ']')]",
      "location": "[parameters('workspaceRegionId')]",
      "tags": { },
      "type": "Microsoft.OperationsManagement/solutions",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
        <list-of-resources>
      ],
      "properties": {
        "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
        "referencedResources": [
            <list-of-referenced-resources>
        ],
        "containedResources": [
            <list-of-contained-resources>
        ]
      },
      "plan": {
        "name": "[concat(variables('Solution').Name, '[' ,parameters('workspaceName'), ']')]",
        "Version": "[variables('Solution').Version]",
        "product": "[variables('ProductName')]",
        "publisher": "[variables('Solution').Publisher]",
        "promotionCode": ""
      }
    }




### <a name="dependencies"></a>Zależności
Hello rozwiązania zasobu musi mieć [zależności](../azure-resource-manager/resource-group-define-dependencies.md) na wszystkich innych zasobów w rozwiązaniu hello ponieważ potrzebują tooexist, aby można było utworzyć rozwiązanie hello.  Możesz to zrobić przez dodanie wpisu dla każdego zasobu hello **dependsOn** elementu.

### <a name="properties"></a>Właściwości
Witaj rozwiązania zasób ma właściwości hello w hello w poniższej tabeli.  Obejmują one zasoby hello przywoływany i zawarty w hello rozwiązania, który definiuje sposób zarządzania zasobów powitania po zainstalowaniu hello rozwiązania.  Każdy zasób w rozwiązaniu hello powinien być wyświetlany w obu hello **referencedResources** lub hello **containedResources** właściwości.

| Właściwość | Opis |
|:--- |:--- |
| workspaceResourceId |Identyfikator obszaru roboczego analizy dzienników hello w postaci hello  *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<nazwa obszaru roboczego\>*. |
| referencedResources |Lista zasobów w rozwiązaniu hello, która nie powinna zostać usunięta po usunięciu hello rozwiązania. |
| containedResources |Lista zasobów w rozwiązaniu hello, która powinna zostać usunięta po usunięciu hello rozwiązania. |

w powyższym przykładzie Hello jest rozwiązania z elementu runbook, harmonogram i widoku.  Harmonogram Hello i runbook są *przywoływanego* w hello **właściwości** elementu, więc nie zostaną usunięte po usunięciu hello rozwiązania.  Widok Hello jest *zawarte* , zostanie ono usunięte po usunięciu hello rozwiązania.

### <a name="plan"></a>Planowanie
Witaj **planu** jednostki hello rozwiązania zasobu ma właściwości hello w hello w poniższej tabeli.

| Właściwość | Opis |
|:--- |:--- |
| name |Nazwa rozwiązania hello. |
| Wersja |Wersja rozwiązania hello zgodnie z ustaleniami hello autora. |
| Produktu |Rozwiązanie hello tooidentify unikatowy ciąg. |
| Wydawcy |Wydawca hello rozwiązania. |



## <a name="sample"></a>Przykład
Przykłady pliki rozwiązania z zasobem rozwiązania można przejrzeć hello następujących lokalizacji.

- [Zasoby do automatyzacji](operations-management-suite-solutions-resources-automation.md#sample)
- [Zasoby wyszukiwania i alertów](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a>Następne kroki
* [Dodaj zapisanych wyszukiwań i alerty](operations-management-suite-solutions-resources-searches-alerts.md) tooyour rozwiązania do zarządzania.
* [Dodawanie widoków](operations-management-suite-solutions-resources-views.md) tooyour rozwiązania do zarządzania.
* [Dodawanie elementów runbook i innych zasobów automatyzacji](operations-management-suite-solutions-resources-automation.md) tooyour rozwiązania do zarządzania.
* Szczegóły dotyczące hello [szablonów Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).
* Wyszukiwanie [szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates) przykłady różnych szablonów usługi Resource Manager.
