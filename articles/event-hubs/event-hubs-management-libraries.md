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
# <a name="event-hubs-management-libraries"></a><span data-ttu-id="98dfe-103">Biblioteki zarządzania centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="98dfe-103">Event Hubs management libraries</span></span>

<span data-ttu-id="98dfe-104">biblioteki zarządzania Hello usługi Event Hubs można dynamicznie inicjują obsługę przestrzeni nazw usługi Event Hubs i jednostek.</span><span class="sxs-lookup"><span data-stu-id="98dfe-104">hello Event Hubs management libraries can dynamically provision Event Hubs namespaces and entities.</span></span> <span data-ttu-id="98dfe-105">Umożliwia to złożone wdrożenia i scenariusze obsługi komunikatów, tak aby programowo można określić, jakie tooprovision jednostek.</span><span class="sxs-lookup"><span data-stu-id="98dfe-105">This enables complex deployments and messaging scenarios, so that you can programmatically determine what entities tooprovision.</span></span> <span data-ttu-id="98dfe-106">Te biblioteki są obecnie dostępne dla platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="98dfe-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="98dfe-107">Obsługiwane funkcje</span><span class="sxs-lookup"><span data-stu-id="98dfe-107">Supported functionality</span></span>

* <span data-ttu-id="98dfe-108">Namespace tworzenia, aktualizacji, usuwania</span><span class="sxs-lookup"><span data-stu-id="98dfe-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="98dfe-109">Tworzenie centra zdarzeń, aktualizacji, usuwania</span><span class="sxs-lookup"><span data-stu-id="98dfe-109">Event Hubs creation, update, deletion</span></span>
* <span data-ttu-id="98dfe-110">Tworzenie grupy konsumentów, aktualizacji, usuwania</span><span class="sxs-lookup"><span data-stu-id="98dfe-110">Consumer Group creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98dfe-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="98dfe-111">Prerequisites</span></span>

<span data-ttu-id="98dfe-112">tooget uruchomiony przy użyciu biblioteki zarządzania hello centra zdarzeń, wymagane jest uwierzytelnienie usłudze Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="98dfe-112">tooget started using hello Event Hubs management libraries, you must authenticate with Azure Active Directory (AAD).</span></span> <span data-ttu-id="98dfe-113">AAD wymaga, aby uwierzytelniać się jako nazwy głównej usługi, która zapewnia tooyour dostępu do zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="98dfe-113">AAD requires that you authenticate as a service principal, which provides access tooyour Azure resources.</span></span> <span data-ttu-id="98dfe-114">Informacji o tworzeniu usługę podmiotu zabezpieczeń zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="98dfe-114">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="98dfe-115">Użyj aplikacji usługi Active Directory hello toocreate portalu Azure i nazwy głównej usługi, który ma dostęp do zasobów</span><span class="sxs-lookup"><span data-stu-id="98dfe-115">Use hello Azure portal toocreate Active Directory application and service principal that can access resources</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="98dfe-116">Użyj programu Azure PowerShell toocreate zasobów tooaccess głównej usługi</span><span class="sxs-lookup"><span data-stu-id="98dfe-116">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="98dfe-117">Użyj interfejsu wiersza polecenia Azure toocreate zasobów tooaccess głównej usługi</span><span class="sxs-lookup"><span data-stu-id="98dfe-117">Use Azure CLI toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

<span data-ttu-id="98dfe-118">Te samouczki oferuje `AppId` (identyfikator klienta), `TenantId`, i `ClientSecret` (klucz uwierzytelniania), które są używane do uwierzytelniania przez hello biblioteki zarządzania.</span><span class="sxs-lookup"><span data-stu-id="98dfe-118">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by hello management libraries.</span></span> <span data-ttu-id="98dfe-119">Musi mieć **właściciela** uprawnienia dla grupy zasobów hello, na którym ma zostać toorun.</span><span class="sxs-lookup"><span data-stu-id="98dfe-119">You must have **Owner** permissions for hello resource group on which you want toorun.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="98dfe-120">Wzorzec programowania</span><span class="sxs-lookup"><span data-stu-id="98dfe-120">Programming pattern</span></span>

<span data-ttu-id="98dfe-121">Witaj toomanipulate wzorzec dowolnego zasobu usługi Event Hubs następuje wspólny protokół:</span><span class="sxs-lookup"><span data-stu-id="98dfe-121">hello pattern toomanipulate any Event Hubs resource follows a common protocol:</span></span>

1. <span data-ttu-id="98dfe-122">Uzyskać token z usługi AAD przy użyciu hello `Microsoft.IdentityModel.Clients.ActiveDirectory` biblioteki.</span><span class="sxs-lookup"><span data-stu-id="98dfe-122">Obtain a token from AAD using hello `Microsoft.IdentityModel.Clients.ActiveDirectory` library.</span></span>
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. <span data-ttu-id="98dfe-123">Utwórz hello `EventHubManagementClient` obiektu.</span><span class="sxs-lookup"><span data-stu-id="98dfe-123">Create hello `EventHubManagementClient` object.</span></span>
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. <span data-ttu-id="98dfe-124">Zestaw hello `CreateOrUpdate` tooyour parametry określone wartości.</span><span class="sxs-lookup"><span data-stu-id="98dfe-124">Set hello `CreateOrUpdate` parameters tooyour specified values.</span></span>
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. <span data-ttu-id="98dfe-125">Wykonanie hello wywołania.</span><span class="sxs-lookup"><span data-stu-id="98dfe-125">Execute hello call.</span></span>
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a><span data-ttu-id="98dfe-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="98dfe-126">Next steps</span></span>
* [<span data-ttu-id="98dfe-127">Przykładowe zarządzania .NET</span><span class="sxs-lookup"><span data-stu-id="98dfe-127">.NET Management sample</span></span>](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [<span data-ttu-id="98dfe-128">Odwołanie Microsoft.Azure.Management.EventHub</span><span class="sxs-lookup"><span data-stu-id="98dfe-128">Microsoft.Azure.Management.EventHub Reference</span></span>](/dotnet/api/Microsoft.Azure.Management.EventHub) 
