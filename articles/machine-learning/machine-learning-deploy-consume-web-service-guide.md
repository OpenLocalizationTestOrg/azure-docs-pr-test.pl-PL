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
ms.openlocfilehash: 18edabe267ec06c08074d7a7a6d71435cedc8489
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a>Usługi sieci Web Azure Machine Learning: wdrażanie i korzystanie
Azure Machine Learning umożliwia wdrażanie przepływów pracy i modele jako usługi sieci web usługi machine learning. Wywoływanie modeli uczenia maszynowego z aplikacji przez Internet w celu prognoz w czasie rzeczywistym lub w trybie wsadowym można następnie te usługi sieci web. Ponieważ usługi sieci web RESTful, można ich wywołać z różnych języków programowania i platform, takich jak .NET i Java i z aplikacji, takich jak program Excel.

Następne sekcje zawierają łącza do wskazówki, kodu i dokumentacji, aby ułatwić rozpoczęcie.

## <a name="deploy-a-web-service"></a>Wdrażanie usługi internetowej
### <a name="with-azure-machine-learning-studio"></a>Za pomocą usługi Azure Machine Learning Studio
Usługa Machine Learning Studio i portalu usługi sieci Web Microsoft Azure Machine Learning ułatwiające wdrażanie i zarządzanie usługi sieci web bez konieczności pisania kodu.

Poniższe łącza zawierają ogólne informacje dotyczące sposobu wdrażania nową usługę sieci web:

* Aby uzyskać ogólne informacje o sposobie wdrażania nową usługę sieci web, która jest oparta na usłudze Azure Resource Manager, zobacz [wdrożenie nowej usługi sieci web](machine-learning-webservice-deploy-a-web-service.md).
* Aby uzyskać wskazówki dotyczące wdrażania usługi sieci web, zobacz [wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).
* Aby pełna wskazówki dotyczące sposobu tworzenia i wdrażania usługi sieci web, zobacz [wskazówki krok 1: tworzenie obszaru roboczego uczenia maszynowego](machine-learning-walkthrough-1-create-ml-workspace.md).
* Aby uzyskać szczegółowe przykłady, które wdrażanie usługi sieci web zobacz:

  * [Wskazówki krok 5: Wdrażanie usługi sieci web uczenie maszynowe Azure](machine-learning-walkthrough-5-publish-web-service.md)
  * [Jak wdrożyć usługę sieci web w wielu regionach](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a>Z dostawcy zasobów usługi sieci web API (interfejsów API usługi Azure Resource Manager)
Dostawcy zasobów usługi Azure Machine Learning dla usług sieci web umożliwia wdrażanie i zarządzanie usługami sieci web przy użyciu wywołania interfejsu API REST. Aby uzyskać więcej informacji, zobacz [maszyny Learning Web Service (REST)](/rest/api/machinelearning/index) odwołania.

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a>Polecenia cmdlet programu PowerShell
Dostawca zasobów usługi Azure Machine Learning dla usług sieci web umożliwia wdrażanie i zarządzanie usługami sieci web przy użyciu poleceń cmdlet programu PowerShell.

Aby używać poleceń cmdlet, należy najpierw zalogować się do konta z platformy Azure w środowisku PowerShell przy użyciu [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) polecenia cmdlet. Jeśli znasz sposób wywoływania polecenia programu PowerShell, które są oparte na Resource Manager, zobacz temat [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).

Aby wyeksportować predykcyjnej eksperymentu, należy użyć [ten przykładowy kod](https://github.com/ritwik20/AzureML-WebServices). Po utworzeniu pliku .exe z kodu można wpisać:

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

Uruchamianie aplikacji powoduje utworzenie szablonu JSON usługi sieci web. Aby użyć szablonu, aby wdrożyć usługę sieci web, należy dodać następujące informacje:

* Nazwa konta magazynu i klucz

    Nazwa konta magazynu i klucza można uzyskać z dowolnej [portalu Azure](https://portal.azure.com/) lub [klasycznego portalu Azure](http://manage.windowsazure.com/).
* Identyfikator planu zobowiązań

    Otrzymasz identyfikator planu z [usługi sieci Web systemu Azure Machine Learning](https://services.azureml.net) portalu, rejestrując się i klikając nazwę planu.

Dodaj je do formatu JSON szablonu jako elementy podrzędne *właściwości* węzłów na tym samym poziomie jako *MachineLearningWorkspace* węzła.

Oto przykład:

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

Zobacz następujące artykuły i przykładowy kod, aby uzyskać dodatkowe szczegóły:

* [Polecenia cmdlet systemu Azure Learning maszyny](https://msdn.microsoft.com/library/azure/mt767952.aspx) odwołania w witrynie MSDN
* Przykładowe [wskazówki](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) w witrynie GitHub

## <a name="consume-the-web-services"></a>Korzystanie z usług sieci web
### <a name="from-the-azure-machine-learning-web-services-ui-testing"></a>Z usług sieci Web Azure Machine Learning interfejsu użytkownika (testowanie)
Można przetestować usługi sieci web z portalu usługi sieci Web systemu Azure Machine Learning. Dotyczy to również testowania usługi żądań i odpowiedzi (RR) i interfejsy usługę wykonywania wsadowego (BES).

* [Wdrażanie nowej usługi sieci Web](machine-learning-webservice-deploy-a-web-service.md)
* [Wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md)
* [Wskazówki krok 5: Wdrażanie usługi sieci web uczenie maszynowe Azure](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a>Z programu Excel
Można pobrać szablonu programu Excel, który wykorzystuje usługę sieci web:

* [Korzystanie z usługi sieci web uczenie maszynowe Azure z programu Excel](machine-learning-consuming-from-excel.md)
* [Dodatek programu Excel do usługi sieci Web systemu Azure Machine Learning](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a>W kliencie opartego na interfejsie REST
Usługi sieci Web uczenie w usłudze Azure Machine są interfejsy API RESTful. Będzie można korzystać z poniższych interfejsów API z różnych platform, takich jak .NET, Python, R, Java, itp. **Consume** strony usługi sieci web na [portal usługi sieci Web Microsoft Azure Machine Learning](https://services.azureml.net) zawiera przykładowy kod, który może pomóc Ci rozpocząć. Aby uzyskać więcej informacji, zobacz [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md) (Jak korzystać z usługi internetowej Azure Machine Learning).
