---
title: "metadane aplikacji interfejsu API usługi aaaApp generacji odnajdywania i kodu interfejsu API | Dokumentacja firmy Microsoft"
description: "Dowiedz się, sposobu używania generowania metadanych struktury Swagger toofacilitate interfejsu API odnajdywania i kodu w aplikacji interfejsu API w usłudze Azure App Service."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: c7f8e33a-61cc-486f-89df-4a97dc3c71d4
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: alkarche
ms.openlocfilehash: b27e70b7dd6bd97f5b0b490b496320befe7442c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-api-apps-metadata-for-api-discovery-and-code-generation"></a>Metadane aplikacji interfejsu API usługi aplikacji do generowania odnajdywania i kodu interfejsu API
Obsługa [Swagger 2.0](http://swagger.io/) metadanych interfejsu API jest wbudowana w aplikacji interfejsu API usługi aplikacji. Nie masz toouse struktury Swagger, ale jeśli używasz, może korzystać z funkcji aplikacji interfejsu API, które ułatwić odnajdywanie i zużycia.   

## <a name="swagger-endpoint"></a>Punktu końcowego struktury swagger
Można określić punktu końcowego, który udostępnia metadane JSON programu Swagger 2.0 dla aplikacji interfejsu API we właściwości hello aplikacji interfejsu API. punkt końcowy Hello może być względna toohello podstawowy adres URL aplikacji interfejsu API hello lub bezwzględny adres URL. Bezwzględnych adresów URL może wskazywać poza hello aplikacji interfejsu API. 

Wielu klientów podrzędnych (na przykład generowania kodu programu Visual Studio i rozwiązanie PowerApps "Dodaj interfejsu API" przepływu), hello adres URL musi być dostępny publicznie (nie był chroniony przez użytkownika lub uwierzytelnianie usługi). Oznacza to, że jeśli używasz uwierzytelniania usługi aplikacji i mają definicji interfejsu API hello tooexpose z samej aplikacji, należy toouse opcja uwierzytelniania umożliwia anonimowego ruchu tooreach interfejsu API. Aby uzyskać więcej informacji, zobacz [uwierzytelniania i autoryzacji dla aplikacji usługi API Apps](app-service-api-authentication.md).

### <a name="portal-blade"></a>Blok portalu
W hello [portalu Azure](https://portal.azure.com/) hello punkt końcowy adres URL może być widoczne i zmienić na powitania **definicji interfejsu API** bloku.

![](./media/app-service-api-metadata/apidefblade.png)

### <a name="azure-resource-manager-property"></a>Właściwości Menedżera zasobów Azure
Adres URL definicji interfejsu API powitania dla aplikacji interfejsu API można również skonfigurować za pomocą [Eksploratora zasobów](https://resources.azure.com/) lub [szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) narzędzi wiersza polecenia, takich jak [programu Azure PowerShell](/powershell/azureps-cmdlets-docs)i hello [interfejsu wiersza polecenia Azure](../cli-install-nodejs.md). 

W **Eksploratora zasobów**, przejdź zbyt**subskrypcji > {subskrypcji} > resourceGroups > {grupie zasobów} > dostawców > Microsoft.Web > witryn > {witryny} > konfiguracji > sieci web**, i zobaczysz hello `apiDefinition` właściwości:

        "apiDefinition": {
          "url": "https://contactslistapi.azurewebsites.net/swagger/docs/v1"
        }

Na przykład szablonu usługi Azure Resource Manager, który ustawia hello `apiDefinition` właściwości, otwórz hello [plik azuredeploy.json w listy zadań do wykonania Przykładowa aplikacja hello](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json). Znajdź sekcję hello hello szablonu, który wygląda jak przykładowy kod JSON hello przedstawionych powyżej.

### <a name="default-value"></a>Wartość domyślna
Gdy używasz programu Visual Studio toocreate aplikacji interfejsu API punktu końcowego definicji interfejsu API hello jest ustawiany automatycznie toohello podstawowy adres URL aplikacji hello interfejsu API oraz `/swagger/docs/v1`. Jest to hello domyślny adres URL tego hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) pakiet NuGet korzysta metadanych struktury Swagger generowane dynamicznie tooserve w projekcie interfejsu API sieci Web platformy ASP.NET. 

## <a name="code-generation"></a>Generowanie kodu
Jedną z zalet integracji programu Swagger interfejsu API Azure aplikacji hello jest automatyczne generowanie kodu. Wygenerowane klasy klienta umożliwiają łatwiejsze toowrite kodu, który wywołuje aplikację interfejsu API.

Istnieje możliwość wygenerowania kodu klienta dla aplikacji interfejsu API, za pomocą programu Visual Studio lub z wiersza polecenia hello. Aby dowiedzieć się jak klient toogenerate klas w programie Visual Studio dla projektu interfejsu API sieci Web platformy ASP.NET, zobacz [wprowadzenie do platformy ASP.NET i aplikacji API Apps](app-service-api-dotnet-get-started.md#codegen). Aby uzyskać informacje dotyczące sposobu toodo z polecenia hello wiersz dla wszystkich obsługiwanych języków, zobacz plik readme hello z hello [Azure/autorest](https://github.com/azure/autorest) repozytorium w witrynie GitHub.com.

## <a name="next-steps"></a>Następne kroki
Samouczek krok po kroku, który przeprowadzi Cię przez proces tworzenia, wdrażania i korzystanie z aplikacji interfejsu API, zobacz [Rozpoczynanie pracy z aplikacjami interfejsu API w usłudze Azure App Service](app-service-api-dotnet-get-started.md).

Jeśli używasz usługi Azure API Management w aplikacjach interfejsu API, można użyć tooimport metadanych struktury Swagger interfejsu API do interfejsu API zarządzania. Aby uzyskać więcej informacji, zobacz [jak tooimport hello definicji interfejsu API z operacjami w usłudze Azure API Management](../api-management/api-management-howto-import-api.md). 

