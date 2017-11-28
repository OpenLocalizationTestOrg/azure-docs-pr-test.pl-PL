---
title: zasoby konta wsadowego aaaManage z powitania klienta biblioteki dla platformy .NET - Azure | Dokumentacja firmy Microsoft
description: "Tworzenie, usuwanie i modyfikowanie zasobów konta partii zadań Azure przy użyciu biblioteki zarządzania partiami platformy .NET hello."
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
ms.openlocfilehash: 638d8129f3841ffcfb2e10f5d531a319bcbb7701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-accounts-and-quotas-with-hello-batch-management-client-library-for-net"></a><span data-ttu-id="9391e-103">Zarządzanie kontami partii i przydziały hello biblioteki klienta usługi zarządzania partii dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="9391e-103">Manage Batch accounts and quotas with hello Batch Management client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9391e-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9391e-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="9391e-105">Batch Management .NET</span><span class="sxs-lookup"><span data-stu-id="9391e-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
> 
> 

<span data-ttu-id="9391e-106">Można obniżyć konserwacji nakładów pracy w aplikacji partii zadań Azure za pomocą hello [zarządzania partiami platformy .NET] [ api_mgmt_net] Tworzenie konta usługi partia zadań tooautomate biblioteki, usuwanie, zarządzania kluczami i odnajdywania przydziału.</span><span class="sxs-lookup"><span data-stu-id="9391e-106">You can lower maintenance overhead in your Azure Batch applications by using hello [Batch Management .NET][api_mgmt_net] library tooautomate Batch account creation, deletion, key management, and quota discovery.</span></span>

* <span data-ttu-id="9391e-107">**Tworzenie i usuwanie konta usługi partia zadań** w dowolnym regionie.</span><span class="sxs-lookup"><span data-stu-id="9391e-107">**Create and delete Batch accounts** within any region.</span></span> <span data-ttu-id="9391e-108">Jeśli niezależnego dostawcy oprogramowania (ISV) na przykład można udostępnić usługi dla klientów, w których każdy jest przypisywana oddzielne konta usługi partia zadań do celów rozliczeń, możesz dodać tworzenie i usuwanie funkcji tooyour klienta portalu konta.</span><span class="sxs-lookup"><span data-stu-id="9391e-108">If, as an independent software vendor (ISV) for example, you provide a service for your clients in which each is assigned a separate Batch account for billing purposes, you can add account creation and deletion capabilities tooyour customer portal.</span></span>
* <span data-ttu-id="9391e-109">**Pobierz i ponownie wygenerować kluczy konta** programowo dla każdego konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="9391e-109">**Retrieve and regenerate account keys** programmatically for any of your Batch accounts.</span></span> <span data-ttu-id="9391e-110">Może to pomóc w przestrzegania zasad zabezpieczeń, które wymuszają okresowe przerzucania lub wygaśnięcia klucze konta.</span><span class="sxs-lookup"><span data-stu-id="9391e-110">This can help you comply with security policies that enforce periodic rollover or expiry of account keys.</span></span> <span data-ttu-id="9391e-111">Jeśli masz kilka kont usługi partia zadań w różnych regionach platformy Azure, automatyzacji tego procesu przerzucania zwiększa wydajność rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="9391e-111">When you have several Batch accounts in various Azure regions, automation of this rollover process increases your solution's efficiency.</span></span>
* <span data-ttu-id="9391e-112">**Sprawdź konto przydziały** i wykonać czynności prób i błędów hello poza określania kont usługi partia zadań, które mają jakie limity.</span><span class="sxs-lookup"><span data-stu-id="9391e-112">**Check account quotas** and take hello trial-and-error guesswork out of determining which Batch accounts have what limits.</span></span> <span data-ttu-id="9391e-113">Sprawdzając przydziałami konta przed uruchomieniem zadania, tworzenia pul, lub dodawanie węzłów obliczeniowych, gdzie można dostosować aktywnego lub gdy obliczeniowe te zasoby są tworzone.</span><span class="sxs-lookup"><span data-stu-id="9391e-113">By checking your account quotas before starting jobs, creating pools, or adding compute nodes, you can proactively adjust where or when these compute resources are created.</span></span> <span data-ttu-id="9391e-114">Można określić konta, które wymagają przydziału zwiększa przed przydzielania dodatkowych zasobów w tych kont.</span><span class="sxs-lookup"><span data-stu-id="9391e-114">You can determine which accounts require quota increases before allocating additional resources in those accounts.</span></span>
* <span data-ttu-id="9391e-115">**Łączenie funkcji z innymi usługami Azure** środowisko oferujący wszystkie funkcje zarządzania — za pomocą zarządzania partiami platformy .NET, [usługi Azure Active Directory][aad_about]i hello [Azure Menedżer zasobów] [ resman_overview] w hello tej samej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9391e-115">**Combine features of other Azure services** for a full-featured management experience--by using Batch Management .NET, [Azure Active Directory][aad_about], and hello [Azure Resource Manager][resman_overview] together in hello same application.</span></span> <span data-ttu-id="9391e-116">Przy użyciu tych funkcji i ich interfejsów API, można zapewnić środowisko frictionless uwierzytelniania, hello toocreate możliwości i usuwania grup zasobów i hello możliwości, które są opisane powyżej, aby to rozwiązanie do zarządzania end-to-end.</span><span class="sxs-lookup"><span data-stu-id="9391e-116">By using these features and their APIs, you can provide a frictionless authentication experience, hello ability toocreate and delete resource groups, and hello capabilities that are described above for an end-to-end management solution.</span></span>

> [!NOTE]
> <span data-ttu-id="9391e-117">Chociaż ten artykuł dotyczy hello programowe zarządzanie konta wsadowego, kluczy i przydziały, mogą wykonywać wiele z tych działań za pomocą hello [portalu Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="9391e-117">While this article focuses on hello programmatic management of your Batch accounts, keys, and quotas, you can perform many of these activities by using hello [Azure portal][azure_portal].</span></span> <span data-ttu-id="9391e-118">Aby uzyskać więcej informacji, zobacz [utworzyć konto partii zadań Azure za pomocą portalu Azure hello](batch-account-create-portal.md) i [przydziały i limity dla usługi partia zadań Azure hello](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="9391e-118">For more information, see [Create an Azure Batch account using hello Azure portal](batch-account-create-portal.md) and [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span>
> 
> 

## <a name="create-and-delete-batch-accounts"></a><span data-ttu-id="9391e-119">Tworzenie i usuwanie konta usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="9391e-119">Create and delete Batch accounts</span></span>
<span data-ttu-id="9391e-120">Jak wspomniano, jedną z podstawowej funkcji hello interfejs API zarządzania partii hello jest toocreate i usuwanie konta usługi partia zadań w regionie platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9391e-120">As mentioned, one of hello primary features of hello Batch Management API is toocreate and delete Batch accounts in an Azure region.</span></span> <span data-ttu-id="9391e-121">tak, użyj toodo [BatchManagementClient.Account.CreateAsync] [ net_create] i [DeleteAsync][net_delete], lub ich odpowiedniki synchronicznego.</span><span class="sxs-lookup"><span data-stu-id="9391e-121">toodo so, use [BatchManagementClient.Account.CreateAsync][net_create] and [DeleteAsync][net_delete], or their synchronous counterparts.</span></span>

<span data-ttu-id="9391e-122">Witaj poniższy fragment kodu tworzy konto, uzyskuje hello nowo utworzone konto z hello usługa partia zadań i usuwa go.</span><span class="sxs-lookup"><span data-stu-id="9391e-122">hello following code snippet creates an account, obtains hello newly created account from hello Batch service, and then deletes it.</span></span> <span data-ttu-id="9391e-123">W tym fragment i hello innych użytkowników w tym artykule `batchManagementClient` jest całkowicie zainicjowany wystąpieniem [BatchManagementClient][net_mgmt_client].</span><span class="sxs-lookup"><span data-stu-id="9391e-123">In this snippet and hello others in this article, `batchManagementClient` is a fully initialized instance of [BatchManagementClient][net_mgmt_client].</span></span>

```csharp
// Create a new Batch account
await batchManagementClient.Account.CreateAsync("MyResourceGroup",
    "mynewaccount",
    new BatchAccountCreateParameters() { Location = "West US" });

// Get hello new account from hello Batch service
AccountResource account = await batchManagementClient.Account.GetAsync(
    "MyResourceGroup",
    "mynewaccount");

// Delete hello account
await batchManagementClient.Account.DeleteAsync("MyResourceGroup", account.Name);
```

> [!NOTE]
> <span data-ttu-id="9391e-124">Aplikacje korzystające z biblioteki zarządzania partiami platformy .NET hello i jego klasa BatchManagementClient wymagają **administratora usługi** lub **coadministrator** toohello subskrypcji, która jest właścicielem hello dostępu Zarządzane toobe konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="9391e-124">Applications that use hello Batch Management .NET library and its BatchManagementClient class require **service administrator** or **coadministrator** access toohello subscription that owns hello Batch account toobe managed.</span></span> <span data-ttu-id="9391e-125">Aby uzyskać więcej informacji, zobacz hello [usługi Azure Active Directory](#azure-active-directory) sekcji i hello [AccountManagement] [ acct_mgmt_sample] przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="9391e-125">For more information, see hello [Azure Active Directory](#azure-active-directory) section and hello [AccountManagement][acct_mgmt_sample] code sample.</span></span>
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a><span data-ttu-id="9391e-126">Pobierz i ponownie wygenerować kluczy konta</span><span class="sxs-lookup"><span data-stu-id="9391e-126">Retrieve and regenerate account keys</span></span>
<span data-ttu-id="9391e-127">Uzyskaj klucze podstawowe i pomocnicze konta z dowolnego konta usługi partia zadań w ramach subskrypcji, za pomocą [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="9391e-127">Obtain primary and secondary account keys from any Batch account within your subscription by using [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="9391e-128">Można ponownie wygenerować te klucze za pomocą [RegenerateKeyAsync][net_regenerate_keys].</span><span class="sxs-lookup"><span data-stu-id="9391e-128">You can regenerate those keys by using [RegenerateKeyAsync][net_regenerate_keys].</span></span>

```csharp
// Get and print hello primary and secondary keys
BatchAccountListKeyResult accountKeys =
    await batchManagementClient.Account.ListKeysAsync(
        "MyResourceGroup",
        "mybatchaccount");
Console.WriteLine("Primary key:   {0}", accountKeys.Primary);
Console.WriteLine("Secondary key: {0}", accountKeys.Secondary);

// Regenerate hello primary key
BatchAccountRegenerateKeyResponse newKeys =
    await batchManagementClient.Account.RegenerateKeyAsync(
        "MyResourceGroup",
        "mybatchaccount",
        new BatchAccountRegenerateKeyParameters() {
            KeyName = AccountKeyType.Primary
            });
```

> [!TIP]
> <span data-ttu-id="9391e-129">Można utworzyć połączenia prostsze przepływu pracy dla aplikacji do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="9391e-129">You can create a streamlined connection workflow for your management applications.</span></span> <span data-ttu-id="9391e-130">Najpierw uzyskać klucz konta dla konta wsadowego hello mają toomanage z [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="9391e-130">First, obtain an account key for hello Batch account you wish toomanage with [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="9391e-131">Następnie należy użyć tego klucza podczas inicjowania biblioteki partiami platformy .NET hello [BatchSharedKeyCredentials] [ net_sharedkeycred] klasy, która jest używana podczas inicjowania [BatchClient] [net_batch_client].</span><span class="sxs-lookup"><span data-stu-id="9391e-131">Then, use this key when initializing hello Batch .NET library's [BatchSharedKeyCredentials][net_sharedkeycred] class, which is used when initializing [BatchClient][net_batch_client].</span></span>
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a><span data-ttu-id="9391e-132">Sprawdź subskrypcję platformy Azure i przydziały konta usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="9391e-132">Check Azure subscription and Batch account quotas</span></span>
<span data-ttu-id="9391e-133">Subskrypcje platformy Azure i hello poszczególnych usług Azure tak jak wszystkie partii ma przydziałów domyślnych, które ograniczają liczbę hello niektórych jednostek w nich.</span><span class="sxs-lookup"><span data-stu-id="9391e-133">Azure subscriptions and hello individual Azure services like Batch all have default quotas that limit hello number of certain entities within them.</span></span> <span data-ttu-id="9391e-134">Aby hello przydziałów domyślnych dla subskrypcji platformy Azure, zobacz [subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="9391e-134">For hello default quotas for Azure subscriptions, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="9391e-135">Aby hello domyślne przydziały hello usługa partia zadań, zobacz [przydziały i limity dla usługi partia zadań Azure hello](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="9391e-135">For hello default quotas of hello Batch service, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="9391e-136">Przy użyciu biblioteki zarządzania partiami platformy .NET hello, te przydziały można sprawdzić w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9391e-136">By using hello Batch Management .NET library, you can check these quotas in your applications.</span></span> <span data-ttu-id="9391e-137">Dzięki temu możesz toomake alokacji decyzje przed dodać konta lub zasobów, takich jak pule obliczeniowe i węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="9391e-137">This enables you toomake allocation decisions before you add accounts or compute resources like pools and compute nodes.</span></span>

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a><span data-ttu-id="9391e-138">Sprawdź subskrypcję platformy Azure dla przydziały konta usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="9391e-138">Check an Azure subscription for Batch account quotas</span></span>
<span data-ttu-id="9391e-139">Przed utworzeniem konta usługi partia zadań w regionie, toosee Twojej subskrypcji platformy Azure można sprawdzić, czy jest możliwe tooadd konta w tym regionie.</span><span class="sxs-lookup"><span data-stu-id="9391e-139">Before creating a Batch account in a region, you can check your Azure subscription toosee whether you are able tooadd an account in that region.</span></span>

<span data-ttu-id="9391e-140">W poniższym fragmencie kodu hello, najpierw używamy [BatchManagementClient.Account.ListAsync] [ net_mgmt_listaccounts] tooget zbiór wszystkich kont usługi partia zadań, które są w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9391e-140">In hello code snippet below, we first use [BatchManagementClient.Account.ListAsync][net_mgmt_listaccounts] tooget a collection of all Batch accounts that are within a subscription.</span></span> <span data-ttu-id="9391e-141">Gdy mamy już tej kolekcji, możemy określić liczbę kont hello region docelowy.</span><span class="sxs-lookup"><span data-stu-id="9391e-141">Once we've obtained this collection, we determine how many accounts are in hello target region.</span></span> <span data-ttu-id="9391e-142">Następnie użyjemy [BatchManagementClient.Subscriptions] [ net_mgmt_subscriptions] tooobtain hello limit przydziału kont usługi partia zadań i określić, ile kont (jeśli istnieją) można tworzyć w tym regionie.</span><span class="sxs-lookup"><span data-stu-id="9391e-142">Then we use [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] tooobtain hello Batch account quota and determine how many accounts (if any) can be created in that region.</span></span>

```csharp
// Get a collection of all Batch accounts within hello subscription
BatchAccountListResponse listResponse =
        await batchManagementClient.Account.ListAsync(new AccountListParameters());
IList<AccountResource> accounts = listResponse.Accounts;
Console.WriteLine("Total number of Batch accounts under subscription id {0}:  {1}",
    creds.SubscriptionId,
    accounts.Count);

// Get a count of all accounts within hello target region
string region = "westus";
int accountsInRegion = accounts.Count(o => o.Location == region);

// Get hello account quota for hello specified region
SubscriptionQuotasGetResponse quotaResponse = await batchManagementClient.Subscriptions.GetSubscriptionQuotasAsync(region);
Console.WriteLine("Account quota for {0} region: {1}", region, quotaResponse.AccountQuota);

// Determine how many accounts can be created in hello target region
Console.WriteLine("Accounts in {0}: {1}", region, accountsInRegion);
Console.WriteLine("You can create {0} accounts in hello {1} region.", quotaResponse.AccountQuota - accountsInRegion, region);
```

<span data-ttu-id="9391e-143">We fragmencie hello powyżej `creds` jest wystąpieniem [TokenCloudCredentials][azure_tokencreds].</span><span class="sxs-lookup"><span data-stu-id="9391e-143">In hello snippet above, `creds` is an instance of [TokenCloudCredentials][azure_tokencreds].</span></span> <span data-ttu-id="9391e-144">toosee przykład tworzenia tego obiektu, zobacz hello [AccountManagement] [ acct_mgmt_sample] przykładowy kod w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="9391e-144">toosee an example of creating this object, see hello [AccountManagement][acct_mgmt_sample] code sample on GitHub.</span></span>

### <a name="check-a-batch-account-for-compute-resource-quotas"></a><span data-ttu-id="9391e-145">Sprawdź konto usługi partia zadań dla przydziały zasobów obliczeniowych</span><span class="sxs-lookup"><span data-stu-id="9391e-145">Check a Batch account for compute resource quotas</span></span>
<span data-ttu-id="9391e-146">Przed zwiększeniem zasobów obliczeniowych w rozwiązaniu partii, można sprawdzić tooensure hello zasobów, że tooallocate nie może przekraczać przydziały hello konta.</span><span class="sxs-lookup"><span data-stu-id="9391e-146">Before increasing compute resources in your Batch solution, you can check tooensure hello resources you want tooallocate won't exceed hello account's quotas.</span></span> <span data-ttu-id="9391e-147">W poniższym fragmencie kodu hello, firma Microsoft drukowania hello informacje o limicie przydziału dla konta usługi partia zadań o nazwie hello `mybatchaccount`.</span><span class="sxs-lookup"><span data-stu-id="9391e-147">In hello code snippet below, we print hello quota information for hello Batch account named `mybatchaccount`.</span></span> <span data-ttu-id="9391e-148">Czy konto hello może obsłużyć hello toobe dodatkowe zasoby utworzone w swojej aplikacji, można użyć toodetermine takich informacji.</span><span class="sxs-lookup"><span data-stu-id="9391e-148">In your own application, you could use such information toodetermine whether hello account can handle hello additional resources toobe created.</span></span>

```csharp
// First obtain hello Batch account
BatchAccountGetResponse getResponse =
    await batchManagementClient.Account.GetAsync("MyResourceGroup", "mybatchaccount");
AccountResource account = getResponse.Resource;

// Now print hello compute resource quotas for hello account
Console.WriteLine("Core quota: {0}", account.Properties.CoreQuota);
Console.WriteLine("Pool quota: {0}", account.Properties.PoolQuota);
Console.WriteLine("Active job and job schedule quota: {0}", account.Properties.ActiveJobAndJobScheduleQuota);
```

> [!IMPORTANT]
> <span data-ttu-id="9391e-149">Gdy istnieją przydziałów domyślnych dla subskrypcji platformy Azure i usługi, wiele z tych limitów może być zgłaszany przez żądania w hello [portalu Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="9391e-149">While there are default quotas for Azure subscriptions and services, many of these limits can be raised by issuing a request in hello [Azure portal][azure_portal].</span></span> <span data-ttu-id="9391e-150">Na przykład, zobacz [przydziały i limity dla usługi partia zadań Azure hello](batch-quota-limit.md) instrukcje dotyczące zwiększenie przydziałami konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="9391e-150">For example, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for instructions on increasing your Batch account quotas.</span></span>
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a><span data-ttu-id="9391e-151">Usługi Azure AD za pomocą zarządzania partii .NET</span><span class="sxs-lookup"><span data-stu-id="9391e-151">Use Azure AD with Batch Management .NET</span></span>

<span data-ttu-id="9391e-152">Biblioteka zarządzania partiami platformy .NET Hello jest klientem dostawcy zasobów platformy Azure i jest używany razem z [usługi Azure Resource Manager] [ resman_overview] toomanage konta zasobów programowo.</span><span class="sxs-lookup"><span data-stu-id="9391e-152">hello Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] toomanage account resources programmatically.</span></span> <span data-ttu-id="9391e-153">Usługi Azure AD jest żądań tooauthenticate wymagane przez dowolnego klienta dostawcy zasobów platformy Azure, w tym hello biblioteki zarządzania partiami platformy .NET oraz [usługi Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="9391e-153">Azure AD is required tooauthenticate requests made through any Azure resource provider client, including hello Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span> <span data-ttu-id="9391e-154">Aby dowiedzieć się, jak za pomocą usługi Azure AD z hello biblioteki zarządzania partiami platformy .NET, zobacz [rozwiązań partii tooauthenticate użycia usługi Azure Active Directory](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="9391e-154">For information about using Azure AD with hello Batch Management .NET library, see [Use Azure Active Directory tooauthenticate Batch solutions](batch-aad-auth.md).</span></span> 

## <a name="sample-project-on-github"></a><span data-ttu-id="9391e-155">Przykładowy projekt w witrynie GitHub</span><span class="sxs-lookup"><span data-stu-id="9391e-155">Sample project on GitHub</span></span>

<span data-ttu-id="9391e-156">toosee zarządzania partiami platformy .NET w akcji, zapoznaj się z hello [AccountManagment] [ acct_mgmt_sample] przykładowy projekt w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="9391e-156">toosee Batch Management .NET in action, check out hello [AccountManagment][acct_mgmt_sample] sample project on GitHub.</span></span> <span data-ttu-id="9391e-157">AccountManagment Przykładowa aplikacja Hello przedstawiono hello następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="9391e-157">hello AccountManagment sample application demonstrates hello following operations:</span></span>

1. <span data-ttu-id="9391e-158">Uzyskanie tokenu zabezpieczającego z usługi Azure AD przy użyciu [ADAL][aad_adal].</span><span class="sxs-lookup"><span data-stu-id="9391e-158">Acquire a security token from Azure AD by using [ADAL][aad_adal].</span></span> <span data-ttu-id="9391e-159">Witaj użytkownik nie jest już zalogowany, są monitowani o podanie poświadczeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9391e-159">If hello user is not already signed in, they are prompted for their Azure credentials.</span></span>
2. <span data-ttu-id="9391e-160">Token zabezpieczający hello uzyskane z usługi Azure AD, tworzenie [SubscriptionClient] [ resman_subclient] tooquery Azure, aby uzyskać listę subskrypcji skojarzonych z kontem hello.</span><span class="sxs-lookup"><span data-stu-id="9391e-160">With hello security token obtained from Azure AD, create a [SubscriptionClient][resman_subclient] tooquery Azure for a list of subscriptions associated with hello account.</span></span> <span data-ttu-id="9391e-161">Witaj użytkownik może wybrać subskrypcję z listy hello, jeśli zawiera więcej niż jedną subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="9391e-161">hello user can select a subscription from hello list if it contains more than one subscription.</span></span>
3. <span data-ttu-id="9391e-162">Uzyskiwanie poświadczeń skojarzonych z subskrypcją hello wybrane.</span><span class="sxs-lookup"><span data-stu-id="9391e-162">Get credentials associated with hello selected subscription.</span></span>
4. <span data-ttu-id="9391e-163">Utwórz [element ResourceManagementClient] [ resman_client] obiektu przy użyciu poświadczeń hello.</span><span class="sxs-lookup"><span data-stu-id="9391e-163">Create a [ResourceManagementClient][resman_client] object by using hello credentials.</span></span>
5. <span data-ttu-id="9391e-164">Użyj [element ResourceManagementClient] [ resman_client] obiekt toocreate grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="9391e-164">Use a [ResourceManagementClient][resman_client] object toocreate a resource group.</span></span>
6. <span data-ttu-id="9391e-165">Użyj [BatchManagementClient] [ net_mgmt_client] obiekt tooperform kilka operacji konto usługi partia zadań:</span><span class="sxs-lookup"><span data-stu-id="9391e-165">Use a [BatchManagementClient][net_mgmt_client] object tooperform several Batch account operations:</span></span>
   * <span data-ttu-id="9391e-166">Utwórz konto wsadowe w hello nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="9391e-166">Create a Batch account in hello new resource group.</span></span>
   * <span data-ttu-id="9391e-167">Pobierz hello nowo utworzone konto z hello usługa partia zadań.</span><span class="sxs-lookup"><span data-stu-id="9391e-167">Get hello newly created account from hello Batch service.</span></span>
   * <span data-ttu-id="9391e-168">Klucze konta wydruku hello hello nowego konta.</span><span class="sxs-lookup"><span data-stu-id="9391e-168">Print hello account keys for hello new account.</span></span>
   * <span data-ttu-id="9391e-169">Ponowne generowanie klucza podstawowego dla konta hello.</span><span class="sxs-lookup"><span data-stu-id="9391e-169">Regenerate a new primary key for hello account.</span></span>
   * <span data-ttu-id="9391e-170">Informacje o limicie przydziału wydruku hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="9391e-170">Print hello quota information for hello account.</span></span>
   * <span data-ttu-id="9391e-171">Informacje o limicie przydziału wydruku hello hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9391e-171">Print hello quota information for hello subscription.</span></span>
   * <span data-ttu-id="9391e-172">Wydrukowanie wszystkich kont w ramach subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="9391e-172">Print all accounts within hello subscription.</span></span>
   * <span data-ttu-id="9391e-173">Usuń nowo utworzonego konta.</span><span class="sxs-lookup"><span data-stu-id="9391e-173">Delete newly created account.</span></span>
7. <span data-ttu-id="9391e-174">Usuń grupę zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="9391e-174">Delete hello resource group.</span></span>

<span data-ttu-id="9391e-175">Przed usunięciem partii hello nowo utworzona grupa kont i zasobów, można je przeglądać w hello [portalu Azure][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="9391e-175">Before deleting hello newly created Batch account and resource group, you can view them in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="9391e-176">aplikacja przykładowa hello toorun pomyślnie, najpierw należy zarejestrować go z dzierżawy usługi Azure AD w hello Azure portal i przyznać uprawnienia toohello interfejsu API usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9391e-176">toorun hello sample application successfully, you must first register it with your Azure AD tenant in hello Azure portal and grant permissions toohello Azure Resource Manager API.</span></span> <span data-ttu-id="9391e-177">Procedura hello w [rozwiązań do zarządzania partii uwierzytelniania z usługi Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="9391e-177">Follow hello steps provided in [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span>


[aad_about]: ../active-directory/active-directory-whatis.md "Co to jest usługa Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Scenariusze uwierzytelniania dla usługi Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrowanie aplikacji z usługą Azure Active Directory"
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
