---
title: "aaaViews w rozwiązaniach do zarządzania Operations Management Suite (OMS) | Dokumentacja firmy Microsoft"
description: "Rozwiązania do zarządzania w Operations Management Suite (OMS) zwykle zawiera jeden lub więcej danych toovisualize widoków.  W tym artykule opisano, jak tooexport widok tworzony przez hello Widok projektanta i dołączyć go w rozwiązaniu do zarządzania. "
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 570b278c-2d47-4e5a-9828-7f01f31ddf8c
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 303861465014a27289f831332b3d95925c0ae66d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a>Widoki w rozwiązaniach do zarządzania Operations Management Suite (OMS) (wersja zapoznawcza)
> [!NOTE]
> To jest wstępna dokumentacji do tworzenia rozwiązań do zarządzania w OMS, które są obecnie w wersji zapoznawczej. Żadnego schematu opisanych poniżej jest toochange podmiotu.    
>
>

[Rozwiązania do zarządzania w Operations Management Suite (OMS)](operations-management-suite-solutions.md) zwykle zawiera co najmniej jeden danych toovisualize widoków.  W tym artykule opisano, jak tooexport widok tworzony przez hello [Widok projektanta](../log-analytics/log-analytics-view-designer.md) i uwzględnić go w rozwiązaniu do zarządzania.  

> [!NOTE]
> cześć przykłady w tym artykule Użyj parametry i zmienne, które są albo toomanagement wymagane lub typowych rozwiązań i opisane w [tworzenia rozwiązań do zarządzania w Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)
>
>

## <a name="prerequisites"></a>Wymagania wstępne
W tym artykule przyjęto założenie, że znasz już jak zbyt[tworzenie rozwiązania do zarządzania](operations-management-suite-solutions-creating.md) i hello struktury pliku rozwiązania.

## <a name="overview"></a>Omówienie
tooinclude widoku w rozwiązaniu do zarządzania, tworzenia **zasobów** dla niego w hello [plik rozwiązania](operations-management-suite-solutions-creating.md).  Hello dane JSON, które opisano konfigurację szczegółowy widok hello jest zwykle złożone jednak i nie coś że autor rozwiązania typowych ręcznie będą mogli toocreate.  Witaj najczęściej spotykaną metodą jest toocreate hello widoku przy użyciu hello [Widok projektanta](../log-analytics/log-analytics-view-designer.md), go wyeksportować, a następnie Dodaj rozwiązanie toohello szczegółową konfigurację.

dostępne są następujące Hello tooadd podstawowe kroki rozwiązania tooa widoku.  Każdy krok jest opisany bardziej szczegółowo w poniższych sekcjach hello.

1. Eksportuj plik tooa widoku hello.
2. Utwórz zasób widoku hello w rozwiązaniu hello.
3. Dodawanie hello widoku szczegółów.

## <a name="export-hello-view-tooa-file"></a>Eksportuj plik tooa widoku hello
Postępuj zgodnie z instrukcjami hello w [Projektant widoków analizy dziennika](../log-analytics/log-analytics-view-designer.md) tooexport plik tooa widoku.  Witaj wyeksportowany plik będzie można w formacie JSON z hello sam [elementów jako plik rozwiązania hello](operations-management-suite-solutions-solution-file.md).  

Witaj **zasobów** element hello widoku pliku będzie mieć zasobu o typie **Microsoft.OperationalInsights/workspaces** czy reprezentuje hello obszarem roboczym pakietu OMS.  Ten element będzie mieć podelement typu **widoków** który reprezentuje widok hello i zawiera szczegółowe konfiguracji.  Zostanie Kopiuj szczegóły hello tego elementu, a następnie skopiować go do rozwiązania.

## <a name="create-hello-view-resource-in-hello-solution"></a>Utwórz zasób widoku hello w rozwiązaniu hello
Dodaj powitania po widok zasobów toohello **zasobów** element pliku rozwiązania.  Używa zmiennych, które są opisane poniżej, że należy również dodać.  Należy pamiętać, że hello **pulpitu nawigacyjnego** i **OverviewTile** właściwości symboli zastępczych, które spowoduje zastąpienie hello odpowiednie właściwości z hello widoku eksportowanego pliku.

    {
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
        "type": "Microsoft.OperationalInsights/workspaces/views",
        "location": "[parameters('workspaceregionId')]",
        "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
        "dependson": [
            ],
        "properties": {
            "Id": "[variables('ViewName')]",
            "Name": "[variables('ViewName')]",
            "DisplayName": "[variables('ViewName')]",
            "Description": "",
            "Author": "[variables('ViewAuthor')]",
            "Source": "Local",
            "Dashboard": ,
            "OverviewTile":
        }
    }

Dodaj następujące zmienne toohello zmienne element pliku rozwiązania hello hello i Zastąp hello toothose wartości dla rozwiązania.

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of hello view."
    "ViewName": "Provide a name for hello view here."


Zauważ, że hello całego widoku zasobów można skopiować z widoku wyeksportowanego pliku, który będzie potrzebny hello toomake następujące zmiany dla niego toowork w rozwiązaniu.  

* Witaj **typu** dla widoku hello zasobu musi toobe zmieniła się z **widoków** za**Microsoft.OperationalInsights/workspaces**.
* Witaj **nazwa** właściwości dla zasobu widoku hello wymaga nazwy obszaru roboczego hello tooinclude toobe zmienione.
* zależności Hello w obszarze roboczym hello musi usunąć, ponieważ hello obszaru roboczego zasobu nie jest zdefiniowany w rozwiązaniu hello toobe.
* **Nazwa wyświetlana** właściwości toobe potrzeb dodane toohello widoku.  Witaj **identyfikator**, **nazwa**, i **DisplayName** musi wszystkie zgodne.
* Należy zmienić nazwy parametrów toomatch hello wymagany zestaw parametrów.
* Zmienne należy określić w rozwiązaniu hello i używane w hello odpowiednie właściwości.

## <a name="add-hello-view-details"></a>Dodawanie hello widoku szczegółów
Hello widok zasobów w hello wyeksportowany plik zawiera dwa elementy w hello widoku **właściwości** elementu o nazwie **pulpitu nawigacyjnego** i **OverviewTile** zawierających hello szczegółową konfigurację hello widoku.  Skopiuj następujące dwa elementy i ich zawartość do hello **właściwości** elementu hello widok zasobów w pliku rozwiązania.

## <a name="example"></a>Przykład
Na przykład następujące przykładowe hello przedstawiono plik prostym rozwiązaniem z widokiem.  Wielokropek (...) są wyświetlane dla hello **pulpitu nawigacyjnego** i **OverviewTile** zawartość ze względów miejsca.

    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspaceName": {
                "type": "string"
            },
            "accountName": {
                "type": "string"
            },
            "workspaceRegionId": {
                "type": "string"
            },
            "regionId": {
                "type": "string"
            },
            "pricingTier": {
                "type": "string"
            }
        },
        "variables": {
            "SolutionVersion": "1.1",
            "SolutionPublisher": "Contoso",
            "SolutionName": "Contoso Solution",
            "LogAnalyticsApiVersion": "2015-11-01-preview",
            "ViewAuthor":  "user@contoso.com",
            "ViewDescription":  "This is a sample view.",
            "ViewName":  "Contoso View"
        },
        "resources": [
            {
                "name": "[concat(variables('SolutionName'), '(' ,parameters('workspacename'), ')')]",
                "location": "[parameters('workspaceRegionId')]",
                "tags": { },
                "type": "Microsoft.OperationsManagement/solutions",
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "dependsOn": [
                    "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspacename'), '/views/', variables('ViewName'))]"
                ],
                "properties": {
                    "workspaceResourceId": "[concat(resourceGroup().id, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspacename'))]",
                    "referencedResources": [
                    ],
                    "containedResources": [
                        "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/views/', variables('ViewName'))]"
                    ]
                },
                "plan": {
                    "name": "[concat(variables('SolutionName'), '(' ,parameters('workspaceName'), ')')]",
                    "Version": "[variables('SolutionVersion')]",
                    "product": "ContosoSolution",
                    "publisher": "[variables('SolutionPublisher')]",
                    "promotionCode": ""
                }
            },
            {
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
                "type": "Microsoft.OperationalInsights/workspaces/views",
                "location": "[parameters('workspaceregionId')]",
                "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
                "dependson": [
                ],
                "properties": {
                    "Id": "[variables('ViewName')]",
                    "Name": "[variables('ViewName')]",
                    "DisplayName": "[variables('ViewName')]",
                    "Description": "[variables('ViewDescription')]",
                    "Author": "[variables('ViewAuthor')]",
                    "Source": "Local",
                    "Dashboard": ...,
                    "OverviewTile": ...
                }
            }
          ]
    }




## <a name="next-steps"></a>Następne kroki
* Dowiedz się, szczegółowe informacje dotyczące tworzenia [rozwiązań do zarządzania](operations-management-suite-solutions-creating.md).
* Obejmują [elementu runbook usługi Automatyzacja w ramach rozwiązania do zarządzania](operations-management-suite-solutions-resources-automation.md).
