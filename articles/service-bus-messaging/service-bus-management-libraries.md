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
# <a name="service-bus-management-libraries"></a><span data-ttu-id="40fe1-103">Biblioteki zarządzania usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="40fe1-103">Service Bus management libraries</span></span>

<span data-ttu-id="40fe1-104">biblioteki zarządzania Hello Azure Service Bus można dynamicznie inicjują obsługę przestrzeni nazw usługi Service Bus i jednostek.</span><span class="sxs-lookup"><span data-stu-id="40fe1-104">hello Azure Service Bus management libraries can dynamically provision Service Bus namespaces and entities.</span></span> <span data-ttu-id="40fe1-105">Umożliwia to scenariusze obsługi wiadomości i złożone wdrożenia oraz umożliwia tooprogrammatically ustalić, jakie tooprovision jednostek.</span><span class="sxs-lookup"><span data-stu-id="40fe1-105">This enables complex deployments and messaging scenarios, and makes it possible tooprogrammatically determine what entities tooprovision.</span></span> <span data-ttu-id="40fe1-106">Te biblioteki są obecnie dostępne dla platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="40fe1-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="40fe1-107">Obsługiwane funkcje</span><span class="sxs-lookup"><span data-stu-id="40fe1-107">Supported functionality</span></span>

* <span data-ttu-id="40fe1-108">Namespace tworzenia, aktualizacji, usuwania</span><span class="sxs-lookup"><span data-stu-id="40fe1-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="40fe1-109">Tworzenie kolejek, aktualizacji, usuwania</span><span class="sxs-lookup"><span data-stu-id="40fe1-109">Queue creation, update, deletion</span></span>
* <span data-ttu-id="40fe1-110">Tworzenie tematu, aktualizacji, usuwania</span><span class="sxs-lookup"><span data-stu-id="40fe1-110">Topic creation, update, deletion</span></span>
* <span data-ttu-id="40fe1-111">Tworzenie subskrypcji, aktualizacji i usuwania</span><span class="sxs-lookup"><span data-stu-id="40fe1-111">Subscription creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40fe1-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="40fe1-112">Prerequisites</span></span>

<span data-ttu-id="40fe1-113">tooget uruchomiony przy użyciu biblioteki zarządzania hello usługi Service Bus, wymagane jest uwierzytelnienie przez hello usługi Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="40fe1-113">tooget started using hello Service Bus management libraries, you must authenticate with hello Azure Active Directory (AAD) service.</span></span> <span data-ttu-id="40fe1-114">AAD wymaga, aby uwierzytelniać się jako nazwy głównej usługi, która zapewnia tooyour dostępu do zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="40fe1-114">AAD requires that you authenticate as a service principal, which provides access tooyour Azure resources.</span></span> <span data-ttu-id="40fe1-115">Informacji o tworzeniu usługę podmiotu zabezpieczeń zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="40fe1-115">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="40fe1-116">Użyj aplikacji usługi Active Directory hello toocreate portalu Azure i nazwy głównej usługi, który ma dostęp do zasobów</span><span class="sxs-lookup"><span data-stu-id="40fe1-116">Use hello Azure portal toocreate Active Directory application and service principal that can access resources</span></span>](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [<span data-ttu-id="40fe1-117">Użyj programu Azure PowerShell toocreate zasobów tooaccess głównej usługi</span><span class="sxs-lookup"><span data-stu-id="40fe1-117">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="40fe1-118">Użyj interfejsu wiersza polecenia Azure toocreate zasobów tooaccess głównej usługi</span><span class="sxs-lookup"><span data-stu-id="40fe1-118">Use Azure CLI toocreate a service principal tooaccess resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

<span data-ttu-id="40fe1-119">Te samouczki oferuje `AppId` (identyfikator klienta), `TenantId`, i `ClientSecret` (klucz uwierzytelniania), które są używane do uwierzytelniania przez hello biblioteki zarządzania.</span><span class="sxs-lookup"><span data-stu-id="40fe1-119">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by hello management libraries.</span></span> <span data-ttu-id="40fe1-120">Musi mieć **właściciela** uprawnienia dla grupy zasobów hello, na którym chcesz toorun.</span><span class="sxs-lookup"><span data-stu-id="40fe1-120">You must have **Owner** permissions for hello resource group on which you wish toorun.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="40fe1-121">Wzorzec programowania</span><span class="sxs-lookup"><span data-stu-id="40fe1-121">Programming pattern</span></span>

<span data-ttu-id="40fe1-122">Witaj toomanipulate wzorzec wszystkich zasobów usługi Service Bus następuje wspólny protokół:</span><span class="sxs-lookup"><span data-stu-id="40fe1-122">hello pattern toomanipulate any Service Bus resource follows a common protocol:</span></span>

1. <span data-ttu-id="40fe1-123">Uzyskać token z usługi Azure Active Directory przy użyciu hello **Microsoft.IdentityModel.Clients.ActiveDirectory** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="40fe1-123">Obtain a token from Azure Active Directory using hello **Microsoft.IdentityModel.Clients.ActiveDirectory** library.</span></span>
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. <span data-ttu-id="40fe1-124">Utwórz hello `ServiceBusManagementClient` obiektu.</span><span class="sxs-lookup"><span data-stu-id="40fe1-124">Create hello `ServiceBusManagementClient` object.</span></span>

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. <span data-ttu-id="40fe1-125">Zestaw hello `CreateOrUpdate` tooyour parametry określone wartości.</span><span class="sxs-lookup"><span data-stu-id="40fe1-125">Set hello `CreateOrUpdate` parameters tooyour specified values.</span></span>

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. <span data-ttu-id="40fe1-126">Wykonanie hello wywołania.</span><span class="sxs-lookup"><span data-stu-id="40fe1-126">Execute hello call.</span></span>

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a><span data-ttu-id="40fe1-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="40fe1-127">Next steps</span></span>
* [<span data-ttu-id="40fe1-128">Przykładowe zarządzania .NET</span><span class="sxs-lookup"><span data-stu-id="40fe1-128">.NET management sample</span></span>](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [<span data-ttu-id="40fe1-129">Odwołanie Microsoft.Azure.Management.ServiceBus interfejsu API</span><span class="sxs-lookup"><span data-stu-id="40fe1-129">Microsoft.Azure.Management.ServiceBus API reference</span></span>](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
