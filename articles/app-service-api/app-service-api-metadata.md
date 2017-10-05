---
title: "Metadane aplikacji interfejsu API usługi aplikacji do generowania odnajdywania i kodu interfejsu API | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak aplikacje interfejsu API w usłudze Azure App Service za pomocą metadanych struktury Swagger ułatwienia generowania odnajdywania i kodu interfejsu API."
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
ms.openlocfilehash: 800bb9df9b957bec2c80abb3edefbaf354b549ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="app-service-api-apps-metadata-for-api-discovery-and-code-generation"></a>Metadane aplikacji interfejsu API usługi aplikacji do generowania odnajdywania i kodu interfejsu API
Obsługa [Swagger 2.0](http://swagger.io/) metadanych interfejsu API jest wbudowana w aplikacji interfejsu API usługi aplikacji. Nie trzeba używać struktury Swagger, ale jeśli używasz, może korzystać z funkcji aplikacji interfejsu API, które ułatwić odnajdywanie i zużycia.   

## <a name="swagger-endpoint"></a>Punktu końcowego struktury swagger
Można określić punktu końcowego, który udostępnia metadane JSON programu Swagger 2.0 dla aplikacji interfejsu API we właściwości w aplikacji interfejsu API. Punkt końcowy może być względem podstawowego adresu URL aplikacji interfejsu API lub bezwzględny adres URL. Bezwzględnych adresów URL może wskazywać poza aplikacji interfejsu API. 

Wielu klientów podrzędnych (na przykład generowania kodu programu Visual Studio i rozwiązanie PowerApps "Dodaj interfejsu API" przepływu), adres URL musi być dostępny publicznie (nie był chroniony przez użytkownika lub uwierzytelnianie usługi). Oznacza to, że jeśli używasz uwierzytelniania usługi aplikacji i udostępnić definicji interfejsu API z samej aplikacji, należy użyć opcji uwierzytelniania, która zezwala na ruch anonimowym do interfejsu API. Aby uzyskać więcej informacji, zobacz [uwierzytelniania i autoryzacji dla aplikacji usługi API Apps](app-service-api-authentication.md).

### <a name="portal-blade"></a>Blok portalu
W [portalu Azure](https://portal.azure.com/) punkt końcowy adres URL może być widoczne i zmieniona **definicji interfejsu API** bloku.

![](./media/app-service-api-metadata/apidefblade.png)

### <a name="azure-resource-manager-property"></a>Właściwości Menedżera zasobów Azure
Adres URL definicji interfejsu API dla aplikacji interfejsu API można również skonfigurować za pomocą [Eksploratora zasobów](https://resources.azure.com/) lub [szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) narzędzi wiersza polecenia, takich jak [programu Azure PowerShell](/powershell/azureps-cmdlets-docs)i [Azure CLI](../cli-install-nodejs.md). 

W **Eksploratora zasobów**, przejdź do **subskrypcji > {subskrypcji} > resourceGroups > {grupie zasobów} > dostawców > Microsoft.Web > Lokacje > {witryny} > config > sieci web** , aby wyświetlić `apiDefinition` właściwości:

        "apiDefinition": {
          "url": "https://contactslistapi.azurewebsites.net/swagger/docs/v1"
        }

Na przykład szablonu usługi Azure Resource Manager, który ustawia `apiDefinition` właściwości, otwórz [plik azuredeploy.json w przykładowej aplikacji listy zadań do wykonania](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json). Znajdź sekcję szablonu, który wygląda jak przykładowego kodu JSON przedstawionych powyżej.

### <a name="default-value"></a>Wartość domyślna
Podczas tworzenia aplikacji interfejsu API za pomocą programu Visual Studio punkt końcowy definicji interfejsu API jest automatycznie ustawiana podstawowy adres URL aplikacji interfejsu API oraz `/swagger/docs/v1`. Jest to domyślny adres URL który [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) używa pakiet NuGet do obsługi dynamicznie generowanym Swagger metadanych w projekcie interfejsu API sieci Web platformy ASP.NET. 

## <a name="code-generation"></a>Generowanie kodu
Jedną z zalet integracji programu Swagger aplikacji interfejsu API Azure jest automatyczne generowanie kodu. Wygenerowane klasy klienta ułatwiają pisanie kodu, który wywołuje aplikację interfejsu API.

Istnieje możliwość wygenerowania kodu klienta dla aplikacji interfejsu API, za pomocą programu Visual Studio lub z wiersza polecenia. Aby uzyskać informacje dotyczące do generowania klasy klienta w programie Visual Studio dla projektu interfejsu API sieci Web platformy ASP.NET, zobacz [wprowadzenie do interfejsu API Apps i platformy ASP.NET](app-service-api-dotnet-get-started.md#codegen). Aby dowiedzieć się, jak to zrobić z poziomu wiersza polecenia dla wszystkich obsługiwanych języków, zobacz plik readme programu [Azure/autorest](https://github.com/azure/autorest) repozytorium w witrynie GitHub.com.

## <a name="next-steps"></a>Następne kroki
Samouczek krok po kroku, który przeprowadzi Cię przez proces tworzenia, wdrażania i korzystanie z aplikacji interfejsu API, zobacz [Rozpoczynanie pracy z aplikacjami interfejsu API w usłudze Azure App Service](app-service-api-dotnet-get-started.md).

Jeśli używasz usługi Azure API Management w aplikacjach interfejsu API służy metadanych struktury Swagger można zaimportować interfejs API do zarządzania interfejsem API. Aby uzyskać więcej informacji, zobacz [sposób importowania definicji interfejsu API z operacjami w usłudze Azure API Management](../api-management/api-management-howto-import-api.md). 

