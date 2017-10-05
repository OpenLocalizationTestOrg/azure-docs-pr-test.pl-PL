---
title: "Zarządzanie zasobami konta usługi partia zadań za pomocą biblioteki klienta dla platformy .NET - Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie, usuwanie i modyfikowanie zasobów konta partii zadań Azure przy użyciu biblioteki zarządzania partiami platformy .NET."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 16279b23-60ff-4b16-b308-5de000e4c028
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/24/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eafde9258222a2ab09ade2e366f9cc595a303dec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-batch-accounts-and-quotas-with-the-batch-management-client-library-for-net"></a><span data-ttu-id="7c429-103">Zarządzanie kontami partii i przydziały z biblioteki klienta usługi partia zadań zarządzania dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="7c429-103">Manage Batch accounts and quotas with the Batch Management client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7c429-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7c429-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="7c429-105">Batch Management .NET</span><span class="sxs-lookup"><span data-stu-id="7c429-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
> 
> 

<span data-ttu-id="7c429-106">Można obniżyć konserwacji nakładów pracy w aplikacji partii zadań Azure za pomocą [zarządzania partiami platformy .NET] [ api_mgmt_net] biblioteki można zautomatyzować tworzenie konta usługi partia zadań, usuwanie, zarządzania kluczami i odnajdywania przydziału.</span><span class="sxs-lookup"><span data-stu-id="7c429-106">You can lower maintenance overhead in your Azure Batch applications by using the [Batch Management .NET][api_mgmt_net] library to automate Batch account creation, deletion, key management, and quota discovery.</span></span>

* <span data-ttu-id="7c429-107">**Tworzenie i usuwanie konta usługi partia zadań** w dowolnym regionie.</span><span class="sxs-lookup"><span data-stu-id="7c429-107">**Create and delete Batch accounts** within any region.</span></span> <span data-ttu-id="7c429-108">Jeśli niezależnego dostawcy oprogramowania (ISV) na przykład można udostępnić usługi dla klientów, w których każdy jest przypisywana oddzielne konta usługi partia zadań do celów rozliczeń, możliwości tworzenia i usuwania konta można dodać do portalu klienta.</span><span class="sxs-lookup"><span data-stu-id="7c429-108">If, as an independent software vendor (ISV) for example, you provide a service for your clients in which each is assigned a separate Batch account for billing purposes, you can add account creation and deletion capabilities to your customer portal.</span></span>
* <span data-ttu-id="7c429-109">**Pobierz i ponownie wygenerować kluczy konta** programowo dla każdego konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="7c429-109">**Retrieve and regenerate account keys** programmatically for any of your Batch accounts.</span></span> <span data-ttu-id="7c429-110">Może to pomóc w przestrzegania zasad zabezpieczeń, które wymuszają okresowe przerzucania lub wygaśnięcia klucze konta.</span><span class="sxs-lookup"><span data-stu-id="7c429-110">This can help you comply with security policies that enforce periodic rollover or expiry of account keys.</span></span> <span data-ttu-id="7c429-111">Jeśli masz kilka kont usługi partia zadań w różnych regionach platformy Azure, automatyzacji tego procesu przerzucania zwiększa wydajność rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="7c429-111">When you have several Batch accounts in various Azure regions, automation of this rollover process increases your solution's efficiency.</span></span>
* <span data-ttu-id="7c429-112">**Sprawdź konto przydziały** i wykonać czynności prób i błędów poza określania kont usługi partia zadań, które mają jakie limity.</span><span class="sxs-lookup"><span data-stu-id="7c429-112">**Check account quotas** and take the trial-and-error guesswork out of determining which Batch accounts have what limits.</span></span> <span data-ttu-id="7c429-113">Sprawdzając przydziałami konta przed uruchomieniem zadania, tworzenia pul, lub dodawanie węzłów obliczeniowych, gdzie można dostosować aktywnego lub gdy obliczeniowe te zasoby są tworzone.</span><span class="sxs-lookup"><span data-stu-id="7c429-113">By checking your account quotas before starting jobs, creating pools, or adding compute nodes, you can proactively adjust where or when these compute resources are created.</span></span> <span data-ttu-id="7c429-114">Można określić konta, które wymagają przydziału zwiększa przed przydzielania dodatkowych zasobów w tych kont.</span><span class="sxs-lookup"><span data-stu-id="7c429-114">You can determine which accounts require quota increases before allocating additional resources in those accounts.</span></span>
* <span data-ttu-id="7c429-115">**Łączenie funkcji z innymi usługami Azure** środowisko oferujący wszystkie funkcje zarządzania — za pomocą zarządzania partiami platformy .NET, [usługi Azure Active Directory][aad_about]i [usługi Azure Resource Manager] [ resman_overview] razem w tej samej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7c429-115">**Combine features of other Azure services** for a full-featured management experience--by using Batch Management .NET, [Azure Active Directory][aad_about], and the [Azure Resource Manager][resman_overview] together in the same application.</span></span> <span data-ttu-id="7c429-116">Korzystając z tych funkcji i ich interfejsów API, można zapewnić środowisko frictionless uwierzytelniania, możliwość tworzenia i usuwania grup zasobów i możliwości, które są opisane powyżej rozwiązania do zarządzania end-to-end.</span><span class="sxs-lookup"><span data-stu-id="7c429-116">By using these features and their APIs, you can provide a frictionless authentication experience, the ability to create and delete resource groups, and the capabilities that are described above for an end-to-end management solution.</span></span>

> [!NOTE]
> <span data-ttu-id="7c429-117">Chociaż ten artykuł dotyczy programowe zarządzanie konta wsadowego, kluczy i przydziały, mogą wykonywać wiele z tych działań za pomocą [portalu Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="7c429-117">While this article focuses on the programmatic management of your Batch accounts, keys, and quotas, you can perform many of these activities by using the [Azure portal][azure_portal].</span></span> <span data-ttu-id="7c429-118">Aby uzyskać więcej informacji, zobacz [utworzyć konto partii zadań Azure za pomocą portalu Azure](batch-account-create-portal.md) i [przydziały i limity dla usługi partia zadań Azure](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="7c429-118">For more information, see [Create an Azure Batch account using the Azure portal](batch-account-create-portal.md) and [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span>
> 
> 

## <a name="create-and-delete-batch-accounts"></a><span data-ttu-id="7c429-119">Tworzenie i usuwanie konta usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="7c429-119">Create and delete Batch accounts</span></span>
<span data-ttu-id="7c429-120">Jak wspomniano, co główne funkcje interfejsu API zarządzania partii jest do tworzenia i usuwania konta usługi partia zadań w regionie platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7c429-120">As mentioned, one of the primary features of the Batch Management API is to create and delete Batch accounts in an Azure region.</span></span> <span data-ttu-id="7c429-121">Aby to zrobić, użyj [BatchManagementClient.Account.CreateAsync] [ net_create] i [DeleteAsync][net_delete], lub ich odpowiedniki synchronicznego.</span><span class="sxs-lookup"><span data-stu-id="7c429-121">To do so, use [BatchManagementClient.Account.CreateAsync][net_create] and [DeleteAsync][net_delete], or their synchronous counterparts.</span></span>

<span data-ttu-id="7c429-122">Poniższy fragment kodu tworzy konto, uzyskuje nowo utworzonych kont z usługi partia zadań i usuwa go.</span><span class="sxs-lookup"><span data-stu-id="7c429-122">The following code snippet creates an account, obtains the newly created account from the Batch service, and then deletes it.</span></span> <span data-ttu-id="7c429-123">Ta Wstawka kodu i innych użytkowników, w tym artykule `batchManagementClient` jest całkowicie zainicjowany wystąpieniem [BatchManagementClient][net_mgmt_client].</span><span class="sxs-lookup"><span data-stu-id="7c429-123">In this snippet and the others in this article, `batchManagementClient` is a fully initialized instance of [BatchManagementClient][net_mgmt_client].</span></span>

```csharp
// Create a new Batch account
await batchManagementClient.Account.CreateAsync("MyResourceGroup",
    "mynewaccount",
    new BatchAccountCreateParameters() { Location = "West US" });

// Get the new account from the Batch service
AccountResource account = await batchManagementClient.Account.GetAsync(
    "MyResourceGroup",
    "mynewaccount");

// Delete the account
await batchManagementClient.Account.DeleteAsync("MyResourceGroup", account.Name);
```

> [!NOTE]
> <span data-ttu-id="7c429-124">Aplikacje korzystające z biblioteki zarządzania partiami platformy .NET i jego klasa BatchManagementClient wymagają **administratora usługi** lub **coadministrator** dostępu do subskrypcji, która jest właścicielem konta usługi partia zadań, które mają być zarządzane.</span><span class="sxs-lookup"><span data-stu-id="7c429-124">Applications that use the Batch Management .NET library and its BatchManagementClient class require **service administrator** or **coadministrator** access to the subscription that owns the Batch account to be managed.</span></span> <span data-ttu-id="7c429-125">Aby uzyskać więcej informacji, zobacz [usługi Azure Active Directory](#azure-active-directory) sekcji i [AccountManagement] [ acct_mgmt_sample] przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="7c429-125">For more information, see the [Azure Active Directory](#azure-active-directory) section and the [AccountManagement][acct_mgmt_sample] code sample.</span></span>
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a><span data-ttu-id="7c429-126">Pobierz i ponownie wygenerować kluczy konta</span><span class="sxs-lookup"><span data-stu-id="7c429-126">Retrieve and regenerate account keys</span></span>
<span data-ttu-id="7c429-127">Uzyskaj klucze podstawowe i pomocnicze konta z dowolnego konta usługi partia zadań w ramach subskrypcji, za pomocą [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="7c429-127">Obtain primary and secondary account keys from any Batch account within your subscription by using [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="7c429-128">Można ponownie wygenerować te klucze za pomocą [RegenerateKeyAsync][net_regenerate_keys].</span><span class="sxs-lookup"><span data-stu-id="7c429-128">You can regenerate those keys by using [RegenerateKeyAsync][net_regenerate_keys].</span></span>

```csharp
// Get and print the primary and secondary keys
BatchAccountListKeyResult accountKeys =
    await batchManagementClient.Account.ListKeysAsync(
        "MyResourceGroup",
        "mybatchaccount");
Console.WriteLine("Primary key:   {0}", accountKeys.Primary);
Console.WriteLine("Secondary key: {0}", accountKeys.Secondary);

// Regenerate the primary key
BatchAccountRegenerateKeyResponse newKeys =
    await batchManagementClient.Account.RegenerateKeyAsync(
        "MyResourceGroup",
        "mybatchaccount",
        new BatchAccountRegenerateKeyParameters() {
            KeyName = AccountKeyType.Primary
            });
```

> [!TIP]
> <span data-ttu-id="7c429-129">Można utworzyć połączenia prostsze przepływu pracy dla aplikacji do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="7c429-129">You can create a streamlined connection workflow for your management applications.</span></span> <span data-ttu-id="7c429-130">Najpierw uzyskać klucz konta dla konta usługi partia zadań, mają być zarządzane za pomocą [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="7c429-130">First, obtain an account key for the Batch account you wish to manage with [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="7c429-131">Następnie należy użyć tego klucza podczas inicjowania biblioteki partiami platformy .NET [BatchSharedKeyCredentials] [ net_sharedkeycred] klasy, która jest używana podczas inicjowania [BatchClient][net_batch_client].</span><span class="sxs-lookup"><span data-stu-id="7c429-131">Then, use this key when initializing the Batch .NET library's [BatchSharedKeyCredentials][net_sharedkeycred] class, which is used when initializing [BatchClient][net_batch_client].</span></span>
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a><span data-ttu-id="7c429-132">Sprawdź subskrypcję platformy Azure i przydziały konta usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="7c429-132">Check Azure subscription and Batch account quotas</span></span>
<span data-ttu-id="7c429-133">Subskrypcje platformy Azure i poszczególnych usług Azure, takich jak partii wszystkie mają przydziałów domyślnych, które ograniczają liczbę niektórych jednostek w nich.</span><span class="sxs-lookup"><span data-stu-id="7c429-133">Azure subscriptions and the individual Azure services like Batch all have default quotas that limit the number of certain entities within them.</span></span> <span data-ttu-id="7c429-134">Aby uzyskać przydziałów domyślnych dla subskrypcji platformy Azure, zobacz [subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="7c429-134">For the default quotas for Azure subscriptions, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="7c429-135">Aby przydziałów domyślnych usługa partia zadań, zobacz [przydziały i limity dla usługi partia zadań Azure](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="7c429-135">For the default quotas of the Batch service, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="7c429-136">Przy użyciu biblioteki zarządzania partiami platformy .NET, te przydziały można sprawdzić w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7c429-136">By using the Batch Management .NET library, you can check these quotas in your applications.</span></span> <span data-ttu-id="7c429-137">Umożliwia podjęcie decyzji alokacji, przed dodać konta lub zasobów, takich jak pule obliczeniowe i węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="7c429-137">This enables you to make allocation decisions before you add accounts or compute resources like pools and compute nodes.</span></span>

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a><span data-ttu-id="7c429-138">Sprawdź subskrypcję platformy Azure dla przydziały konta usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="7c429-138">Check an Azure subscription for Batch account quotas</span></span>
<span data-ttu-id="7c429-139">Przed utworzeniem konta usługi partia zadań w regionie, można sprawdzić subskrypcji platformy Azure, aby zobaczyć, czy jesteś w stanie w celu dodania konta w tym regionie.</span><span class="sxs-lookup"><span data-stu-id="7c429-139">Before creating a Batch account in a region, you can check your Azure subscription to see whether you are able to add an account in that region.</span></span>

<span data-ttu-id="7c429-140">W poniższym fragmencie kodu, najpierw używamy [BatchManagementClient.Account.ListAsync] [ net_mgmt_listaccounts] uzyskać zbiór wszystkich kont usługi partia zadań, które są w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7c429-140">In the code snippet below, we first use [BatchManagementClient.Account.ListAsync][net_mgmt_listaccounts] to get a collection of all Batch accounts that are within a subscription.</span></span> <span data-ttu-id="7c429-141">Gdy mamy już tej kolekcji, możemy określić liczbę kont region docelowy.</span><span class="sxs-lookup"><span data-stu-id="7c429-141">Once we've obtained this collection, we determine how many accounts are in the target region.</span></span> <span data-ttu-id="7c429-142">Następnie użyjemy [BatchManagementClient.Subscriptions] [ net_mgmt_subscriptions] uzyskać limit przydziału kont usługi partia zadań i określić, ile kont (jeśli istnieją) można tworzyć w tym regionie.</span><span class="sxs-lookup"><span data-stu-id="7c429-142">Then we use [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] to obtain the Batch account quota and determine how many accounts (if any) can be created in that region.</span></span>

```csharp
// Get a collection of all Batch accounts within the subscription
BatchAccountListResponse listResponse =
        await batchManagementClient.Account.ListAsync(new AccountListParameters());
IList<AccountResource> accounts = listResponse.Accounts;
Console.WriteLine("Total number of Batch accounts under subscription id {0}:  {1}",
    creds.SubscriptionId,
    accounts.Count);

// Get a count of all accounts within the target region
string region = "westus";
int accountsInRegion = accounts.Count(o => o.Location == region);

// Get the account quota for the specified region
SubscriptionQuotasGetResponse quotaResponse = await batchManagementClient.Subscriptions.GetSubscriptionQuotasAsync(region);
Console.WriteLine("Account quota for {0} region: {1}", region, quotaResponse.AccountQuota);

// Determine how many accounts can be created in the target region
Console.WriteLine("Accounts in {0}: {1}", region, accountsInRegion);
Console.WriteLine("You can create {0} accounts in the {1} region.", quotaResponse.AccountQuota - accountsInRegion, region);
```

<span data-ttu-id="7c429-143">We fragmencie powyżej `creds` jest wystąpieniem [TokenCloudCredentials][azure_tokencreds].</span><span class="sxs-lookup"><span data-stu-id="7c429-143">In the snippet above, `creds` is an instance of [TokenCloudCredentials][azure_tokencreds].</span></span> <span data-ttu-id="7c429-144">Aby zapoznać się z przykładem tworzenia tego obiektu, zobacz [AccountManagement] [ acct_mgmt_sample] przykładowy kod w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="7c429-144">To see an example of creating this object, see the [AccountManagement][acct_mgmt_sample] code sample on GitHub.</span></span>

### <a name="check-a-batch-account-for-compute-resource-quotas"></a><span data-ttu-id="7c429-145">Sprawdź konto usługi partia zadań dla przydziały zasobów obliczeniowych</span><span class="sxs-lookup"><span data-stu-id="7c429-145">Check a Batch account for compute resource quotas</span></span>
<span data-ttu-id="7c429-146">Przed zwiększeniem zasobów obliczeniowych w rozwiązaniu partii, można sprawdzić, upewnij się, zasoby, które mają zostać przydzielone nie przekracza limity przydziału dla konta.</span><span class="sxs-lookup"><span data-stu-id="7c429-146">Before increasing compute resources in your Batch solution, you can check to ensure the resources you want to allocate won't exceed the account's quotas.</span></span> <span data-ttu-id="7c429-147">We fragmencie kodu poniżej, firma Microsoft wydrukować informacje o limicie przydziału dla konta usługi partia zadań o nazwie `mybatchaccount`.</span><span class="sxs-lookup"><span data-stu-id="7c429-147">In the code snippet below, we print the quota information for the Batch account named `mybatchaccount`.</span></span> <span data-ttu-id="7c429-148">W aplikacji można użyć tych informacji do określenia, czy konto może obsłużyć dodatkowe zasoby do utworzenia.</span><span class="sxs-lookup"><span data-stu-id="7c429-148">In your own application, you could use such information to determine whether the account can handle the additional resources to be created.</span></span>

```csharp
// First obtain the Batch account
BatchAccountGetResponse getResponse =
    await batchManagementClient.Account.GetAsync("MyResourceGroup", "mybatchaccount");
AccountResource account = getResponse.Resource;

// Now print the compute resource quotas for the account
Console.WriteLine("Core quota: {0}", account.Properties.CoreQuota);
Console.WriteLine("Pool quota: {0}", account.Properties.PoolQuota);
Console.WriteLine("Active job and job schedule quota: {0}", account.Properties.ActiveJobAndJobScheduleQuota);
```

> [!IMPORTANT]
> <span data-ttu-id="7c429-149">Gdy istnieją przydziałów domyślnych dla subskrypcji platformy Azure i usługi, wiele z tych limitów może być zgłaszany przez żądania w [portalu Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="7c429-149">While there are default quotas for Azure subscriptions and services, many of these limits can be raised by issuing a request in the [Azure portal][azure_portal].</span></span> <span data-ttu-id="7c429-150">Na przykład, zobacz [przydziały i limity dla usługi partia zadań Azure](batch-quota-limit.md) instrukcje dotyczące zwiększenie przydziałami konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="7c429-150">For example, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for instructions on increasing your Batch account quotas.</span></span>
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a><span data-ttu-id="7c429-151">Usługi Azure AD za pomocą zarządzania partii .NET</span><span class="sxs-lookup"><span data-stu-id="7c429-151">Use Azure AD with Batch Management .NET</span></span>

<span data-ttu-id="7c429-152">Biblioteka zarządzania partiami platformy .NET jest klientem dostawcy zasobów platformy Azure i jest używany razem z [usługi Azure Resource Manager] [ resman_overview] programowo zarządzać zasobami konta.</span><span class="sxs-lookup"><span data-stu-id="7c429-152">The Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] to manage account resources programmatically.</span></span> <span data-ttu-id="7c429-153">Usługi Azure AD jest wymagany do uwierzytelniania żądań wysyłanych za pomocą dowolnego klienta dostawcy zasobów platformy Azure, w tym biblioteki zarządzania partiami platformy .NET i za pośrednictwem [usługi Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="7c429-153">Azure AD is required to authenticate requests made through any Azure resource provider client, including the Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span> <span data-ttu-id="7c429-154">Aby uzyskać informacje o korzystaniu z usługi Azure AD z biblioteki zarządzania partiami platformy .NET, zobacz [użycia usługi Azure Active Directory do uwierzytelniania rozwiązań partii](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="7c429-154">For information about using Azure AD with the Batch Management .NET library, see [Use Azure Active Directory to authenticate Batch solutions](batch-aad-auth.md).</span></span> 

## <a name="sample-project-on-github"></a><span data-ttu-id="7c429-155">Przykładowy projekt w witrynie GitHub</span><span class="sxs-lookup"><span data-stu-id="7c429-155">Sample project on GitHub</span></span>

<span data-ttu-id="7c429-156">Aby wyświetlić zarządzania partiami platformy .NET w akcji, zapoznaj się [AccountManagment] [ acct_mgmt_sample] przykładowy projekt w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="7c429-156">To see Batch Management .NET in action, check out the [AccountManagment][acct_mgmt_sample] sample project on GitHub.</span></span> <span data-ttu-id="7c429-157">Przykładowa aplikacja AccountManagment przedstawiono następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="7c429-157">The AccountManagment sample application demonstrates the following operations:</span></span>

1. <span data-ttu-id="7c429-158">Uzyskanie tokenu zabezpieczającego z usługi Azure AD przy użyciu [ADAL][aad_adal].</span><span class="sxs-lookup"><span data-stu-id="7c429-158">Acquire a security token from Azure AD by using [ADAL][aad_adal].</span></span> <span data-ttu-id="7c429-159">Jeśli użytkownik nie jest już zalogowany, są monitowani o podanie poświadczeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7c429-159">If the user is not already signed in, they are prompted for their Azure credentials.</span></span>
2. <span data-ttu-id="7c429-160">Token zabezpieczający uzyskane z usługi Azure AD, tworzenie [SubscriptionClient] [ resman_subclient] zapytania Azure listę subskrypcji skojarzonych z kontem.</span><span class="sxs-lookup"><span data-stu-id="7c429-160">With the security token obtained from Azure AD, create a [SubscriptionClient][resman_subclient] to query Azure for a list of subscriptions associated with the account.</span></span> <span data-ttu-id="7c429-161">Użytkownik może wybrać subskrypcję z listy, jeśli zawiera więcej niż jedną subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="7c429-161">The user can select a subscription from the list if it contains more than one subscription.</span></span>
3. <span data-ttu-id="7c429-162">Uzyskiwanie poświadczeń skojarzonych z wybraną subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="7c429-162">Get credentials associated with the selected subscription.</span></span>
4. <span data-ttu-id="7c429-163">Utwórz [element ResourceManagementClient] [ resman_client] obiektu przy użyciu poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="7c429-163">Create a [ResourceManagementClient][resman_client] object by using the credentials.</span></span>
5. <span data-ttu-id="7c429-164">Użyj [element ResourceManagementClient] [ resman_client] obiekt, aby utworzyć grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="7c429-164">Use a [ResourceManagementClient][resman_client] object to create a resource group.</span></span>
6. <span data-ttu-id="7c429-165">Użyj [BatchManagementClient] [ net_mgmt_client] obiektu w celu wykonania kilku operacji konto usługi partia zadań:</span><span class="sxs-lookup"><span data-stu-id="7c429-165">Use a [BatchManagementClient][net_mgmt_client] object to perform several Batch account operations:</span></span>
   * <span data-ttu-id="7c429-166">Utwórz konto wsadowe w nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="7c429-166">Create a Batch account in the new resource group.</span></span>
   * <span data-ttu-id="7c429-167">Pobierz nowo utworzonych kont z usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="7c429-167">Get the newly created account from the Batch service.</span></span>
   * <span data-ttu-id="7c429-168">Drukowanie klucze konta dla nowego konta.</span><span class="sxs-lookup"><span data-stu-id="7c429-168">Print the account keys for the new account.</span></span>
   * <span data-ttu-id="7c429-169">Ponowne generowanie klucza podstawowego dla konta.</span><span class="sxs-lookup"><span data-stu-id="7c429-169">Regenerate a new primary key for the account.</span></span>
   * <span data-ttu-id="7c429-170">Drukowanie informacje o limicie przydziału dla konta.</span><span class="sxs-lookup"><span data-stu-id="7c429-170">Print the quota information for the account.</span></span>
   * <span data-ttu-id="7c429-171">Drukowanie informacje o limicie przydziału dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7c429-171">Print the quota information for the subscription.</span></span>
   * <span data-ttu-id="7c429-172">Wydrukowanie wszystkich kont w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7c429-172">Print all accounts within the subscription.</span></span>
   * <span data-ttu-id="7c429-173">Usuń nowo utworzonego konta.</span><span class="sxs-lookup"><span data-stu-id="7c429-173">Delete newly created account.</span></span>
7. <span data-ttu-id="7c429-174">Usuń grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="7c429-174">Delete the resource group.</span></span>

<span data-ttu-id="7c429-175">Przed usunięciem nowo utworzona grupa kont i zasobów usługi partia zadań, można wyświetlić je w [portalu Azure][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="7c429-175">Before deleting the newly created Batch account and resource group, you can view them in the [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="7c429-176">Aby pomyślnie uruchomić przykładową aplikację, najpierw musisz zarejestrować go z dzierżawy usługi Azure AD w portalu Azure i udzielić uprawnień do interfejsu API Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7c429-176">To run the sample application successfully, you must first register it with your Azure AD tenant in the Azure portal and grant permissions to the Azure Resource Manager API.</span></span> <span data-ttu-id="7c429-177">Postępuj zgodnie z krokami opisanymi w [rozwiązań do zarządzania partii uwierzytelniania z usługi Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="7c429-177">Follow the steps provided in [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span>


<span data-ttu-id="7c429-178">[aad_about]: ../active-directory/active-directory-whatis.md "Co to jest usługa Azure Active Directory?"</span><span class="sxs-lookup"><span data-stu-id="7c429-178">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="7c429-179">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Scenariusze uwierzytelniania dla usługi Azure AD"</span><span class="sxs-lookup"><span data-stu-id="7c429-179">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="7c429-180">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrowanie aplikacji z usługą Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="7c429-180">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_mgmt_net]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[azure_portal]: http://portal.azure.com
[azure_storage]: https://azure.microsoft.com/services/storage/
[azure_tokencreds]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.tokencloudcredentials.aspx
[batch_explorer_project]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_list_keys]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.listkeysasync.aspx
[net_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.createasync.aspx
[net_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.deleteasync.aspx
[net_regenerate_keys]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.regeneratekeyasync.aspx
[net_sharedkeycred]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.auth.batchsharedkeycredentials.aspx
[net_mgmt_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.batchmanagementclient.aspx
[net_mgmt_subscriptions]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.batchmanagementclient.subscriptions.aspx
[net_mgmt_listaccounts]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.iaccountoperations.listasync.aspx
[resman_api]: https://msdn.microsoft.com/library/azure/mt418626.aspx
[resman_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.resources.resourcemanagementclient.aspx
[resman_subclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.subscriptions.subscriptionclient.aspx
[resman_overview]: ../azure-resource-manager/resource-group-overview.md

[1]: ./media/batch-management-dotnet/portal-01.png
[2]: ./media/batch-management-dotnet/portal-02.png
[3]: ./media/batch-management-dotnet/portal-03.png
