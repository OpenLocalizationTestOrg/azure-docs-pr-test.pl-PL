---
title: "Usługi sieci Web uczenie Azure maszyny: Wdrażanie i zużycia | Dokumentacja firmy Microsoft"
description: "Zasoby umożliwiające wdrażanie i korzystanie z usług sieci web."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: 47635376-d1f4-4ea4-a6af-bd1f99f69a69
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 539c2abb053a0f981be0374defe45cf4d96b740b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a>Usługi sieci Web Azure Machine Learning: wdrażanie i korzystanie
Można użyć usługi Azure Machine Learning toodeploy uczenia maszynowego przepływów pracy i modele jako usługi sieci web. Te usługi sieci web może następnie być modeli uczenia maszynowego hello toocall używanych z aplikacji za pośrednictwem hello Internet toodo prognoz w czasie rzeczywistym lub w trybie wsadowym. Ponieważ hello usług sieci web RESTful, można ich wywołać z różnych języków programowania i platform, takich jak .NET i Java i z aplikacji, takich jak program Excel.

Witaj dalej sekcjach znajdują się linki toowalkthroughs, kodu i toohelp dokumentacji ułatwią rozpoczęcie pracy.

## <a name="deploy-a-web-service"></a>Wdrażanie usługi internetowej
### <a name="with-azure-machine-learning-studio"></a>Za pomocą usługi Azure Machine Learning Studio
Witaj usługi sieci Web Microsoft Azure Machine Learning portal i usługa Machine Learning Studio ułatwiające wdrażanie i zarządzanie usługi sieci web bez konieczności pisania kodu.

Witaj poniższe linki udostępniają informacje ogólne o tym, jak toodeploy nową usługę sieci web:

* Omówienie toodeploy nową usługę sieci web, opartą na usłudze Azure Resource Manager, zobacz temat [wdrożenie nowej usługi sieci web](machine-learning-webservice-deploy-a-web-service.md).
* Aby uzyskać wskazówki dotyczące toodeploy usługi sieci web, zobacz [wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).
* Aby uzyskać pełny przewodnik o tym, jak toocreate i wdrażania usługi sieci web, zobacz [wskazówki krok 1: tworzenie obszaru roboczego uczenia maszynowego](machine-learning-walkthrough-1-create-ml-workspace.md).
* Aby uzyskać szczegółowe przykłady, które wdrażanie usługi sieci web zobacz:

  * [Wskazówki krok 5: Wdrażanie usługi sieci web Azure Machine Learning hello](machine-learning-walkthrough-5-publish-web-service.md)
  * [Jak toodeploy sieci web usługi toomultiple regionów](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a>Z dostawcy zasobów usługi sieci web API (interfejsów API usługi Azure Resource Manager)
dostawcy zasobów usługi Azure Machine Learning Hello usług sieci web umożliwia wdrażanie i zarządzanie usługami sieci web przy użyciu wywołania interfejsu API REST. Aby uzyskać więcej informacji, zobacz [maszyny Learning Web Service (REST)](/rest/api/machinelearning/index) odwołania.

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a>Polecenia cmdlet programu PowerShell
Dostawca zasobów usługi Azure Machine Learning dla usług sieci web umożliwia wdrażanie i zarządzanie usługami sieci web przy użyciu poleceń cmdlet programu PowerShell.

toouse hello poleceń cmdlet, musi pierwszy raz logujesz się tooyour konto platformy Azure w środowisku PowerShell hello przy użyciu hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) polecenia cmdlet. Jeśli użytkownik nie zna jak toocall PowerShell poleceń, które są oparte na Menedżera zasobów, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).

tooexport Twojego predykcyjnej eksperymentu, użyj [ten przykładowy kod](https://github.com/ritwik20/AzureML-WebServices). Po utworzeniu pliku .exe hello z kodu hello można wpisać:

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

Uruchomienie aplikacji hello tworzy JSON szablonu usługi sieci web. toouse hello szablonu toodeploy usługi sieci web, należy dodać hello następujących informacji:

* Nazwa konta magazynu i klucz

    Możesz pobrać ze strony hello albo nazwę konta magazynu hello i klucz [portalu Azure](https://portal.azure.com/) lub hello [klasycznego portalu Azure](http://manage.windowsazure.com/).
* Identyfikator planu zobowiązań

    Identyfikator planu hello można uzyskać z hello [usługi sieci Web systemu Azure Machine Learning](https://services.azureml.net) portalu, rejestrując się i klikając nazwę planu.

Dodaj je toohello JSON szablonu jako elementy podrzędne hello *właściwości* węzeł hello sam poziom jako hello *MachineLearningWorkspace* węzła.

Oto przykład:

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

Zobacz następujące artykuły hello i przykładowy kod, aby uzyskać dodatkowe szczegóły:

* [Polecenia cmdlet systemu Azure Learning maszyny](https://msdn.microsoft.com/library/azure/mt767952.aspx) odwołania w witrynie MSDN
* Przykładowe [wskazówki](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) w witrynie GitHub

## <a name="consume-hello-web-services"></a>Stosowanie hello usług sieci web
### <a name="from-hello-azure-machine-learning-web-services-ui-testing"></a>Z hello Azure Machine Learning usług interfejsie użytkownika sieci Web (testowanie)
Można przetestować usługi sieci web z portalu usługi sieci Web systemu Azure Machine Learning hello. Dotyczy to również testowania hello żądań i odpowiedzi usługi (RR) i interfejsy usługę wykonywania wsadowego (BES).

* [Wdrażanie nowej usługi sieci Web](machine-learning-webservice-deploy-a-web-service.md)
* [Wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md)
* [Wskazówki krok 5: Wdrażanie usługi sieci web Azure Machine Learning hello](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a>Z programu Excel
Można pobrać szablonu programu Excel, który wykorzystuje hello usługi sieci web:

* [Korzystanie z usługi sieci web uczenie maszynowe Azure z programu Excel](machine-learning-consuming-from-excel.md)
* [Dodatek programu Excel do usługi sieci Web systemu Azure Machine Learning](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a>W kliencie opartego na interfejsie REST
Usługi sieci Web uczenie w usłudze Azure Machine są interfejsy API RESTful. Będzie można korzystać z poniższych interfejsów API z różnych platform, takich jak .NET, Python, R, Java, hello itp. **Consume** stronę usługi sieci web na powitania [portal usługi sieci Web Microsoft Azure Machine Learning](https://services.azureml.net) ma próbki Kod, który może pomóc rozpocząć pracę. Aby uzyskać więcej informacji, zobacz [jak tooconsume usługi sieci Web Azure Machine Learning](machine-learning-consume-web-services.md).
