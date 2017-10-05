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
# <a name="service-bus-management-libraries"></a><span data-ttu-id="d9e5a-103">Biblioteki zarządzania usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="d9e5a-103">Service Bus management libraries</span></span>

<span data-ttu-id="d9e5a-104">Biblioteki zarządzania usługi Azure Service Bus można dynamicznie inicjują obsługę przestrzeni nazw usługi Service Bus i jednostek.</span><span class="sxs-lookup"><span data-stu-id="d9e5a-104">The Azure Service Bus management libraries can dynamically provision Service Bus namespaces and entities.</span></span> <span data-ttu-id="d9e5a-105">Włącza scenariusze obsługi wiadomości i złożone wdrożenia i umożliwia programowo ustalić, jakie jednostki do udostępniania.</span><span class="sxs-lookup"><span data-stu-id="d9e5a-105">This enables complex deployments and messaging scenarios, and makes it possible to programmatically determine what entities to provision.</span></span> <span data-ttu-id="d9e5a-106">Te biblioteki są obecnie dostępne dla platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="d9e5a-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="d9e5a-107">Obsługiwane funkcje</span><span class="sxs-lookup"><span data-stu-id="d9e5a-107">Supported functionality</span></span>

* <span data-ttu-id="d9e5a-108">Namespace tworzenia, aktualizacji, usuwania</span><span class="sxs-lookup"><span data-stu-id="d9e5a-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="d9e5a-109">Tworzenie kolejek, aktualizacji, usuwania</span><span class="sxs-lookup"><span data-stu-id="d9e5a-109">Queue creation, update, deletion</span></span>
* <span data-ttu-id="d9e5a-110">Tworzenie tematu, aktualizacji, usuwania</span><span class="sxs-lookup"><span data-stu-id="d9e5a-110">Topic creation, update, deletion</span></span>
* <span data-ttu-id="d9e5a-111">Tworzenie subskrypcji, aktualizacji i usuwania</span><span class="sxs-lookup"><span data-stu-id="d9e5a-111">Subscription creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9e5a-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d9e5a-112">Prerequisites</span></span>

<span data-ttu-id="d9e5a-113">Aby rozpocząć korzystanie z bibliotek usługi Service Bus zarządzania musi uwierzytelniać się w usłudze Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="d9e5a-113">To get started using the Service Bus management libraries, you must authenticate with the Azure Active Directory (AAD) service.</span></span> <span data-ttu-id="d9e5a-114">AAD wymaga, aby uwierzytelniać się jako nazwy głównej usługi, która zapewnia dostęp do zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d9e5a-114">AAD requires that you authenticate as a service principal, which provides access to your Azure resources.</span></span> <span data-ttu-id="d9e5a-115">Informacji o tworzeniu usługę podmiotu zabezpieczeń zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="d9e5a-115">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="d9e5a-116">Tworzenie aplikacji usługi Active Directory i nazwy głównej usługi, który ma dostęp do zasobów za pomocą portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d9e5a-116">Use the Azure portal to create Active Directory application and service principal that can access resources</span></span>](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [<span data-ttu-id="d9e5a-117">Use Azure PowerShell to create a service principal to access resources (Tworzenie jednostki usługi używanej do uzyskiwania dostępu do zasobów przy użyciu programu Azure PowerShell)</span><span class="sxs-lookup"><span data-stu-id="d9e5a-117">Use Azure PowerShell to create a service principal to access resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="d9e5a-118">Use Azure CLI to create a service principal to access resources (Tworzenie jednostki usługi używanej do uzyskiwania dostępu do zasobów przy użyciu interfejsu wiersza polecenia platformy Azure)</span><span class="sxs-lookup"><span data-stu-id="d9e5a-118">Use Azure CLI to create a service principal to access resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

<span data-ttu-id="d9e5a-119">Te samouczki oferuje `AppId` (identyfikator klienta), `TenantId`, i `ClientSecret` (klucz uwierzytelniania), które są używane do uwierzytelniania przez biblioteki zarządzania.</span><span class="sxs-lookup"><span data-stu-id="d9e5a-119">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by the management libraries.</span></span> <span data-ttu-id="d9e5a-120">Musi mieć **właściciela** uprawnienia dla grupy zasobów, na którym chcesz uruchomić.</span><span class="sxs-lookup"><span data-stu-id="d9e5a-120">You must have **Owner** permissions for the resource group on which you wish to run.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="d9e5a-121">Wzorzec programowania</span><span class="sxs-lookup"><span data-stu-id="d9e5a-121">Programming pattern</span></span>

<span data-ttu-id="d9e5a-122">Wzorzec do manipulowania wszystkich zasobów usługi Service Bus obejmuje wspólny protokół:</span><span class="sxs-lookup"><span data-stu-id="d9e5a-122">The pattern to manipulate any Service Bus resource follows a common protocol:</span></span>

1. <span data-ttu-id="d9e5a-123">Uzyskać token z usługi Azure Active Directory przy użyciu **Microsoft.IdentityModel.Clients.ActiveDirectory** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="d9e5a-123">Obtain a token from Azure Active Directory using the **Microsoft.IdentityModel.Clients.ActiveDirectory** library.</span></span>
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. <span data-ttu-id="d9e5a-124">Utwórz `ServiceBusManagementClient` obiektu.</span><span class="sxs-lookup"><span data-stu-id="d9e5a-124">Create the `ServiceBusManagementClient` object.</span></span>

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. <span data-ttu-id="d9e5a-125">Ustaw `CreateOrUpdate` Twojego podanych wartości parametrów.</span><span class="sxs-lookup"><span data-stu-id="d9e5a-125">Set the `CreateOrUpdate` parameters to your specified values.</span></span>

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. <span data-ttu-id="d9e5a-126">Wykonać wywołania.</span><span class="sxs-lookup"><span data-stu-id="d9e5a-126">Execute the call.</span></span>

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a><span data-ttu-id="d9e5a-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d9e5a-127">Next steps</span></span>
* [<span data-ttu-id="d9e5a-128">Przykładowe zarządzania .NET</span><span class="sxs-lookup"><span data-stu-id="d9e5a-128">.NET management sample</span></span>](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [<span data-ttu-id="d9e5a-129">Odwołanie Microsoft.Azure.Management.ServiceBus interfejsu API</span><span class="sxs-lookup"><span data-stu-id="d9e5a-129">Microsoft.Azure.Management.ServiceBus API reference</span></span>](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
