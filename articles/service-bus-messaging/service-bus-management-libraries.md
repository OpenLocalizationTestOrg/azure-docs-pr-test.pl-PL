---
title: "biblioteki zarządzania aaaAzure usługi Service Bus | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 9e4ad91f22815ca0838e6e4647a3606109b2b441
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-management-libraries"></a>Biblioteki zarządzania usługi Service Bus

biblioteki zarządzania Hello Azure Service Bus można dynamicznie inicjują obsługę przestrzeni nazw usługi Service Bus i jednostek. Umożliwia to scenariusze obsługi wiadomości i złożone wdrożenia oraz umożliwia tooprogrammatically ustalić, jakie tooprovision jednostek. Te biblioteki są obecnie dostępne dla platformy .NET.

## <a name="supported-functionality"></a>Obsługiwane funkcje

* Namespace tworzenia, aktualizacji, usuwania
* Tworzenie kolejek, aktualizacji, usuwania
* Tworzenie tematu, aktualizacji, usuwania
* Tworzenie subskrypcji, aktualizacji i usuwania

## <a name="prerequisites"></a>Wymagania wstępne

tooget uruchomiony przy użyciu biblioteki zarządzania hello usługi Service Bus, wymagane jest uwierzytelnienie przez hello usługi Azure Active Directory (AAD). AAD wymaga, aby uwierzytelniać się jako nazwy głównej usługi, która zapewnia tooyour dostępu do zasobów platformy Azure. Informacji o tworzeniu usługę podmiotu zabezpieczeń zobacz następujące artykuły:  

* [Użyj aplikacji usługi Active Directory hello toocreate portalu Azure i nazwy głównej usługi, który ma dostęp do zasobów](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [Użyj programu Azure PowerShell toocreate zasobów tooaccess głównej usługi](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Użyj interfejsu wiersza polecenia Azure toocreate zasobów tooaccess głównej usługi](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

Te samouczki oferuje `AppId` (identyfikator klienta), `TenantId`, i `ClientSecret` (klucz uwierzytelniania), które są używane do uwierzytelniania przez hello biblioteki zarządzania. Musi mieć **właściciela** uprawnienia dla grupy zasobów hello, na którym chcesz toorun.

## <a name="programming-pattern"></a>Wzorzec programowania

Witaj toomanipulate wzorzec wszystkich zasobów usługi Service Bus następuje wspólny protokół:

1. Uzyskać token z usługi Azure Active Directory przy użyciu hello **Microsoft.IdentityModel.Clients.ActiveDirectory** biblioteki.
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. Utwórz hello `ServiceBusManagementClient` obiektu.

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. Zestaw hello `CreateOrUpdate` tooyour parametry określone wartości.

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. Wykonanie hello wywołania.

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a>Następne kroki
* [Przykładowe zarządzania .NET](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [Odwołanie Microsoft.Azure.Management.ServiceBus interfejsu API](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
