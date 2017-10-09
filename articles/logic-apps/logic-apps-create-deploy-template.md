---
title: "Szablony wdrażania aaaCreate dla usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Tworzenie szablonów usługi Azure Resource Manager dla usługi logic apps Zarządzanie wdrożenia i wersji"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 85928ec6-d7cb-488e-926e-2e5db89508ee
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 2f09445f10a376a745d6acbba94ca29d5f79fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-templates-for-logic-apps-deployment-and-release-management"></a>Tworzenie szablonów dla usługi logic apps Zarządzanie wdrożenia i wersji

Po utworzeniu aplikacji logiki możesz toocreate go jako szablonu usługi Azure Resource Manager.
W ten sposób możesz łatwo wdrożyć środowiska tooany aplikacji logiki hello lub grupy zasobów może być konieczne jego.
Aby uzyskać więcej informacji o szablonach usługi Resource Manager, zobacz [tworzenia szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) i [wdrażanie zasobów przy użyciu szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="logic-app-deployment-template"></a>Szablon wdrożenia aplikacji logiki

Aplikacja logiki ma trzy podstawowe składniki:

* **Zasobów aplikacji logiki**: zawiera informacje dotyczące np. cennik planu, lokalizacji i hello definicji przepływu pracy.
* **Definicji przepływu pracy**: opisano kroki przepływu pracy i jak aparat Logic Apps hello powinien zostać wykonany hello przepływu pracy aplikacji logiki.
Ta definicja można wyświetlić w aplikacji logiki **widoku kodu** okna.
W hello zasobów aplikacji logiki, można znaleźć tej definicji w hello `definition` właściwości.
* **Połączenia**: odwołuje się tooseparate zasobów, których bezpiecznie przechowywane metadane dotyczące połączeń łącznika, takie jak ciąg połączenia i token dostępu.
W hello zasobów aplikacji logiki, aplikację logiki odwołuje się do tych zasobów hello `parameters` sekcji.

Wszystkie te elementy istniejących aplikacji logiki można wyświetlić przy użyciu narzędzia, takiego jak [Eksploratora zasobów Azure](http://resources.azure.com).

toomake szablonu dla toouse aplikacji logiki z wdrożeniami grup zasobów, należy zdefiniować hello zasobów i parametryzacja zgodnie z potrzebami.
Na przykład w przypadku instalowania rozwoju tooa, badanie i środowiska produkcyjnego, prawdopodobnie chcesz toouse innego połączenia ciągów tooa bazy danych SQL w każdym środowisku.
Lub może być toodeploy w ramach różnych subskrypcji lub grupy zasobów.  

## <a name="create-a-logic-app-deployment-template"></a>Tworzenie szablonu wdrożenia aplikacji logiki

Hello Najprostszym sposobem toohave logiki prawidłowy szablon wdrożenia aplikacji jest toouse [Visual Studio Tools dla aplikacji logiki](logic-apps-deploy-from-vs.md).
Narzędzia programu Visual Studio Hello Generowanie prawidłowe wdrożenie szablonu, który można używać w dowolnym subskrypcji lub lokalizacji.

Jak utworzyć szablon wdrożenia aplikacji logiki może pomóc kilka innych narzędzi.
Można tworzyć ręcznie, oznacza to, za pomocą hello zasobów już omówione w tym miejscu parametry toocreate zgodnie z potrzebami.
Innym rozwiązaniem jest toouse [twórcy szablon aplikacji logiki](https://github.com/jeffhollan/LogicAppTemplateCreator) modułu programu PowerShell. Ten moduł open source najpierw ocenia aplikacji logiki hello i wszystkie połączenia go używa, a następnie generuje zasobów szablonu z hello parametry niezbędne do wdrożenia.
Na przykład jeśli masz aplikację logiki, który odbiera komunikat z kolejki usługi Azure Service Bus i dodaje bazy danych Azure SQL tooan danych narzędzie hello zachowuje całą logikę aranżacji hello i parameterizes hello SQL i parametry połączenia magistrali usług, dzięki czemu mogą być ustawione na wdrożenie.

> [!NOTE]
> Połączenia muszą być w hello tej samej grupie zasobów co hello aplikacji logiki.
>
>

### <a name="install-hello-logic-app-template-powershell-module"></a>Zainstaluj moduł PowerShell szablon aplikacji logiki hello
Witaj Najprostszym sposobem tooinstall hello modułu odbywa się za pośrednictwem hello [galerii programu PowerShell](https://www.powershellgallery.com/packages/LogicAppTemplate/0.1), za pomocą polecenia hello `Install-Module -Name LogicAppTemplate`.  

Można też zainstalować moduł PowerShell hello ręcznie:

1. Pobierz najnowszą wersję hello hello [twórcy szablon aplikacji logiki](https://github.com/jeffhollan/LogicAppTemplateCreator/releases).  
2. Wyodrębnij hello folderu w folderze modułu programu PowerShell (zazwyczaj `%UserProfile%\Documents\WindowsPowerShell\Modules`).

Dla toowork modułu hello dowolnej dzierżawy i subskrypcji dostęp tokenu, firma Microsoft zaleca korzystanie z hello [ARMClient](https://github.com/projectkudu/ARMClient) narzędzia wiersza polecenia.  To [wpis w blogu](http://blog.davidebbo.com/2015/01/azure-resource-manager-client.html) omówiono bardziej szczegółowo ARMClient.

### <a name="generate-a-logic-app-template-by-using-powershell"></a>Generuj szablon aplikacji logiki przy użyciu programu PowerShell
Po zainstalowaniu programu PowerShell, można wygenerować szablonu przy użyciu hello następujące polecenie:

`armclient token $SubscriptionId | Get-LogicAppTemplate -LogicApp MyApp -ResourceGroup MyRG -SubscriptionId $SubscriptionId -Verbose | Out-File C:\template.json`

`$SubscriptionId`jest identyfikatorem hello subskrypcji platformy Azure. Ten wiersz najpierw pobiera token za pośrednictwem ARMClient, dostępu, a następnie powoduje przekazanie w potoku go za pośrednictwem toohello skrypt programu PowerShell, a następnie tworzy szablon hello w pliku JSON.

## <a name="add-parameters-tooa-logic-app-template"></a>Dodaj szablon aplikacji logiki tooa parametrów
Po utworzeniu szablonu aplikacji logiki możesz kontynuować tooadd lub zmodyfikować parametrów, które mogą wymagać. Na przykład jeśli definicja zawiera tooan identyfikator zasobu funkcji platformy Azure lub zagnieżdżony przepływ pracy, że planujesz toodeploy w ramach jednego wdrożenia, można dodać więcej zasobów tooyour szablon i parametryzacja identyfikatory zgodnie z potrzebami. Witaj dotyczy to również tooany odwołania toocustom interfejsów API i struktury Swagger punktów końcowych oczekiwać toodeploy z każdą grupą zasobów.

## <a name="deploy-a-logic-app-template"></a>Wdróż szablon aplikacji logiki

Szablonu można wdrożyć przy użyciu dowolnego narzędzia, takie jak środowiska PowerShell, interfejsu API REST, [programu Visual Studio Team Services Release Management](#team-services)i Szablon wdrożenia za pomocą hello portalu Azure.
Ponadto toostore hello wartości parametrów, zalecamy utworzenie [pliku parametrów](../azure-resource-manager/resource-group-template-deploy.md#parameter-files).
Dowiedz się, jak za[wdrażanie zasobów przy użyciu szablonów usługi Azure Resource Manager i programu PowerShell](../azure-resource-manager/resource-group-template-deploy.md) lub [wdrażanie zasobów przy użyciu szablonów usługi Azure Resource Manager i portalu Azure hello](../azure-resource-manager/resource-group-template-deploy-portal.md).

### <a name="authorize-oauth-connections"></a>Autoryzowania połączeń OAuth

Po wdrożeniu aplikacji logiki hello działa end-to-end z prawidłowe parametry.
Jednak nadal musi zezwolić toogenerate połączeń OAuth tokenem dostępu prawidłowe.
tooauthorize OAuth połączenia, Otwórz aplikację logiki hello w hello projektanta aplikacji logiki i autoryzowania tych połączeń. Lub dla automatycznego wdrażania, można użyć skryptu tooconsent tooeach połączenia OAuth.
Przykładowy skrypt jest w witrynie GitHub pod [LogicAppConnectionAuth](https://github.com/logicappsio/LogicAppConnectionAuth) projektu.

<a name="team-services"></a>
## <a name="visual-studio-team-services-release-management"></a>Visual Studio Team Services Release Management

Typowy scenariusz wdrażania i zarządzania nimi w środowisku jest toouse narzędzia, takiego jak zarządzania zleceniami w programie Visual Studio Team Services za pomocą szablonu wdrożenia aplikacji logiki. Visual Studio Team Services zawiera [wdrażanie grupy zasobów platformy Azure](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/DeployAzureResourceGroup) zadań można dodać tooany kompilacji lub zwolnij potoku. Należy toohave [nazwy głównej usługi](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/) autoryzacji toodeploy, a następnie można wygenerować hello wersji definicji.

1. Release Management wybierz **pusty** tak, aby utworzyć pustą definicję.

    ![Utwórz pustą definicję][1]

2. Wybierz wszystkie zasoby niezbędne do tego, najprawdopodobniej tym hello logiki aplikacji szablonu, który jest generowany ręcznie lub jako część hello proces kompilacji.
3. Dodaj **wdrożenie grupy zasobów Azure** zadań.
4. Konfigurowanie przy użyciu [nazwy głównej usługi](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/)i referencyjne hello plików szablonu i parametrów szablonu.
5. Nadal toobuild czynności w procesie wersji hello dowolnego środowiska, testów automatycznych lub osób zatwierdzających zgodnie z potrzebami.

<!-- Image References -->
[1]: ./media/logic-apps-create-deploy-template/emptyreleasedefinition.png
