---
title: "Biblioteki zarządzania usługi Azure Service Bus | Dokumentacja firmy Microsoft"
description: "Zarządzanie przestrzeni nazw usługi Service Bus i jednostki z .NET do obsługi komunikatów."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: 1db00dc1f91e8976b622030450445babbe547ad8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="service-bus-management-libraries"></a>Biblioteki zarządzania usługi Service Bus

Biblioteki zarządzania usługi Azure Service Bus można dynamicznie inicjują obsługę przestrzeni nazw usługi Service Bus i jednostek. Włącza scenariusze obsługi wiadomości i złożone wdrożenia i umożliwia programowo ustalić, jakie jednostki do udostępniania. Te biblioteki są obecnie dostępne dla platformy .NET.

## <a name="supported-functionality"></a>Obsługiwane funkcje

* Namespace tworzenia, aktualizacji, usuwania
* Tworzenie kolejek, aktualizacji, usuwania
* Tworzenie tematu, aktualizacji, usuwania
* Tworzenie subskrypcji, aktualizacji i usuwania

## <a name="prerequisites"></a>Wymagania wstępne

Aby rozpocząć korzystanie z bibliotek usługi Service Bus zarządzania musi uwierzytelniać się w usłudze Azure Active Directory (AAD). AAD wymaga, aby uwierzytelniać się jako nazwy głównej usługi, która zapewnia dostęp do zasobów platformy Azure. Informacji o tworzeniu usługę podmiotu zabezpieczeń zobacz następujące artykuły:  

* [Tworzenie aplikacji usługi Active Directory i nazwy głównej usługi, który ma dostęp do zasobów za pomocą portalu Azure](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [Use Azure PowerShell to create a service principal to access resources (Tworzenie jednostki usługi używanej do uzyskiwania dostępu do zasobów przy użyciu programu Azure PowerShell)](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Use Azure CLI to create a service principal to access resources (Tworzenie jednostki usługi używanej do uzyskiwania dostępu do zasobów przy użyciu interfejsu wiersza polecenia platformy Azure)](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

Te samouczki oferuje `AppId` (identyfikator klienta), `TenantId`, i `ClientSecret` (klucz uwierzytelniania), które są używane do uwierzytelniania przez biblioteki zarządzania. Musi mieć **właściciela** uprawnienia dla grupy zasobów, na którym chcesz uruchomić.

## <a name="programming-pattern"></a>Wzorzec programowania

Wzorzec do manipulowania wszystkich zasobów usługi Service Bus obejmuje wspólny protokół:

1. Uzyskać token z usługi Azure Active Directory przy użyciu **Microsoft.IdentityModel.Clients.ActiveDirectory** biblioteki.
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. Utwórz `ServiceBusManagementClient` obiektu.

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. Ustaw `CreateOrUpdate` Twojego podanych wartości parametrów.

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. Wykonać wywołania.

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a>Następne kroki
* [Przykładowe zarządzania .NET](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [Odwołanie Microsoft.Azure.Management.ServiceBus interfejsu API](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
