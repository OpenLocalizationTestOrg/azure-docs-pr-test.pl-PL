---
title: "biblioteki zarządzania usługi Event Hubs aaaAzure | Dokumentacja firmy Microsoft"
description: "Zarządzanie przestrzeni nazw usługi Event Hubs i jednostek z platformy .NET"
services: event-hubs
cloud: na
documentationcenter: na
author: sethmanheim
manager: timlt
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: b7db0077f6f31397ae46e926c3c28630a157824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-management-libraries"></a>Biblioteki zarządzania centra zdarzeń

biblioteki zarządzania Hello usługi Event Hubs można dynamicznie inicjują obsługę przestrzeni nazw usługi Event Hubs i jednostek. Umożliwia to złożone wdrożenia i scenariusze obsługi komunikatów, tak aby programowo można określić, jakie tooprovision jednostek. Te biblioteki są obecnie dostępne dla platformy .NET.

## <a name="supported-functionality"></a>Obsługiwane funkcje

* Namespace tworzenia, aktualizacji, usuwania
* Tworzenie centra zdarzeń, aktualizacji, usuwania
* Tworzenie grupy konsumentów, aktualizacji, usuwania

## <a name="prerequisites"></a>Wymagania wstępne

tooget uruchomiony przy użyciu biblioteki zarządzania hello centra zdarzeń, wymagane jest uwierzytelnienie usłudze Azure Active Directory (AAD). AAD wymaga, aby uwierzytelniać się jako nazwy głównej usługi, która zapewnia tooyour dostępu do zasobów platformy Azure. Informacji o tworzeniu usługę podmiotu zabezpieczeń zobacz następujące artykuły:  

* [Użyj aplikacji usługi Active Directory hello toocreate portalu Azure i nazwy głównej usługi, który ma dostęp do zasobów](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [Użyj programu Azure PowerShell toocreate zasobów tooaccess głównej usługi](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [Użyj interfejsu wiersza polecenia Azure toocreate zasobów tooaccess głównej usługi](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

Te samouczki oferuje `AppId` (identyfikator klienta), `TenantId`, i `ClientSecret` (klucz uwierzytelniania), które są używane do uwierzytelniania przez hello biblioteki zarządzania. Musi mieć **właściciela** uprawnienia dla grupy zasobów hello, na którym ma zostać toorun.

## <a name="programming-pattern"></a>Wzorzec programowania

Witaj toomanipulate wzorzec dowolnego zasobu usługi Event Hubs następuje wspólny protokół:

1. Uzyskać token z usługi AAD przy użyciu hello `Microsoft.IdentityModel.Clients.ActiveDirectory` biblioteki.
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. Utwórz hello `EventHubManagementClient` obiektu.
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. Zestaw hello `CreateOrUpdate` tooyour parametry określone wartości.
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. Wykonanie hello wywołania.
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a>Następne kroki
* [Przykładowe zarządzania .NET](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [Odwołanie Microsoft.Azure.Management.EventHub](/dotnet/api/Microsoft.Azure.Management.EventHub) 
