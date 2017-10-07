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
# <a name="manage-batch-accounts-and-quotas-with-hello-batch-management-client-library-for-net"></a>Zarządzanie kontami partii i przydziały hello biblioteki klienta usługi zarządzania partii dla platformy .NET

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](batch-account-create-portal.md)
> * [Batch Management .NET](batch-management-dotnet.md)
> 
> 

Można obniżyć konserwacji nakładów pracy w aplikacji partii zadań Azure za pomocą hello [zarządzania partiami platformy .NET] [ api_mgmt_net] Tworzenie konta usługi partia zadań tooautomate biblioteki, usuwanie, zarządzania kluczami i odnajdywania przydziału.

* **Tworzenie i usuwanie konta usługi partia zadań** w dowolnym regionie. Jeśli niezależnego dostawcy oprogramowania (ISV) na przykład można udostępnić usługi dla klientów, w których każdy jest przypisywana oddzielne konta usługi partia zadań do celów rozliczeń, możesz dodać tworzenie i usuwanie funkcji tooyour klienta portalu konta.
* **Pobierz i ponownie wygenerować kluczy konta** programowo dla każdego konta usługi partia zadań. Może to pomóc w przestrzegania zasad zabezpieczeń, które wymuszają okresowe przerzucania lub wygaśnięcia klucze konta. Jeśli masz kilka kont usługi partia zadań w różnych regionach platformy Azure, automatyzacji tego procesu przerzucania zwiększa wydajność rozwiązania.
* **Sprawdź konto przydziały** i wykonać czynności prób i błędów hello poza określania kont usługi partia zadań, które mają jakie limity. Sprawdzając przydziałami konta przed uruchomieniem zadania, tworzenia pul, lub dodawanie węzłów obliczeniowych, gdzie można dostosować aktywnego lub gdy obliczeniowe te zasoby są tworzone. Można określić konta, które wymagają przydziału zwiększa przed przydzielania dodatkowych zasobów w tych kont.
* **Łączenie funkcji z innymi usługami Azure** środowisko oferujący wszystkie funkcje zarządzania — za pomocą zarządzania partiami platformy .NET, [usługi Azure Active Directory][aad_about]i hello [Azure Menedżer zasobów] [ resman_overview] w hello tej samej aplikacji. Przy użyciu tych funkcji i ich interfejsów API, można zapewnić środowisko frictionless uwierzytelniania, hello toocreate możliwości i usuwania grup zasobów i hello możliwości, które są opisane powyżej, aby to rozwiązanie do zarządzania end-to-end.

> [!NOTE]
> Chociaż ten artykuł dotyczy hello programowe zarządzanie konta wsadowego, kluczy i przydziały, mogą wykonywać wiele z tych działań za pomocą hello [portalu Azure][azure_portal]. Aby uzyskać więcej informacji, zobacz [utworzyć konto partii zadań Azure za pomocą portalu Azure hello](batch-account-create-portal.md) i [przydziały i limity dla usługi partia zadań Azure hello](batch-quota-limit.md).
> 
> 

## <a name="create-and-delete-batch-accounts"></a>Tworzenie i usuwanie konta usługi partia zadań
Jak wspomniano, jedną z podstawowej funkcji hello interfejs API zarządzania partii hello jest toocreate i usuwanie konta usługi partia zadań w regionie platformy Azure. tak, użyj toodo [BatchManagementClient.Account.CreateAsync] [ net_create] i [DeleteAsync][net_delete], lub ich odpowiedniki synchronicznego.

Witaj poniższy fragment kodu tworzy konto, uzyskuje hello nowo utworzone konto z hello usługa partia zadań i usuwa go. W tym fragment i hello innych użytkowników w tym artykule `batchManagementClient` jest całkowicie zainicjowany wystąpieniem [BatchManagementClient][net_mgmt_client].

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
> Aplikacje korzystające z biblioteki zarządzania partiami platformy .NET hello i jego klasa BatchManagementClient wymagają **administratora usługi** lub **coadministrator** toohello subskrypcji, która jest właścicielem hello dostępu Zarządzane toobe konta usługi partia zadań. Aby uzyskać więcej informacji, zobacz hello [usługi Azure Active Directory](#azure-active-directory) sekcji i hello [AccountManagement] [ acct_mgmt_sample] przykładowy kod.
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a>Pobierz i ponownie wygenerować kluczy konta
Uzyskaj klucze podstawowe i pomocnicze konta z dowolnego konta usługi partia zadań w ramach subskrypcji, za pomocą [ListKeysAsync][net_list_keys]. Można ponownie wygenerować te klucze za pomocą [RegenerateKeyAsync][net_regenerate_keys].

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
> Można utworzyć połączenia prostsze przepływu pracy dla aplikacji do zarządzania. Najpierw uzyskać klucz konta dla konta wsadowego hello mają toomanage z [ListKeysAsync][net_list_keys]. Następnie należy użyć tego klucza podczas inicjowania biblioteki partiami platformy .NET hello [BatchSharedKeyCredentials] [ net_sharedkeycred] klasy, która jest używana podczas inicjowania [BatchClient] [net_batch_client].
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a>Sprawdź subskrypcję platformy Azure i przydziały konta usługi partia zadań
Subskrypcje platformy Azure i hello poszczególnych usług Azure tak jak wszystkie partii ma przydziałów domyślnych, które ograniczają liczbę hello niektórych jednostek w nich. Aby hello przydziałów domyślnych dla subskrypcji platformy Azure, zobacz [subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](../azure-subscription-service-limits.md). Aby hello domyślne przydziały hello usługa partia zadań, zobacz [przydziały i limity dla usługi partia zadań Azure hello](batch-quota-limit.md). Przy użyciu biblioteki zarządzania partiami platformy .NET hello, te przydziały można sprawdzić w aplikacji. Dzięki temu możesz toomake alokacji decyzje przed dodać konta lub zasobów, takich jak pule obliczeniowe i węzły obliczeniowe.

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a>Sprawdź subskrypcję platformy Azure dla przydziały konta usługi partia zadań
Przed utworzeniem konta usługi partia zadań w regionie, toosee Twojej subskrypcji platformy Azure można sprawdzić, czy jest możliwe tooadd konta w tym regionie.

W poniższym fragmencie kodu hello, najpierw używamy [BatchManagementClient.Account.ListAsync] [ net_mgmt_listaccounts] tooget zbiór wszystkich kont usługi partia zadań, które są w ramach subskrypcji. Gdy mamy już tej kolekcji, możemy określić liczbę kont hello region docelowy. Następnie użyjemy [BatchManagementClient.Subscriptions] [ net_mgmt_subscriptions] tooobtain hello limit przydziału kont usługi partia zadań i określić, ile kont (jeśli istnieją) można tworzyć w tym regionie.

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

We fragmencie hello powyżej `creds` jest wystąpieniem [TokenCloudCredentials][azure_tokencreds]. toosee przykład tworzenia tego obiektu, zobacz hello [AccountManagement] [ acct_mgmt_sample] przykładowy kod w witrynie GitHub.

### <a name="check-a-batch-account-for-compute-resource-quotas"></a>Sprawdź konto usługi partia zadań dla przydziały zasobów obliczeniowych
Przed zwiększeniem zasobów obliczeniowych w rozwiązaniu partii, można sprawdzić tooensure hello zasobów, że tooallocate nie może przekraczać przydziały hello konta. W poniższym fragmencie kodu hello, firma Microsoft drukowania hello informacje o limicie przydziału dla konta usługi partia zadań o nazwie hello `mybatchaccount`. Czy konto hello może obsłużyć hello toobe dodatkowe zasoby utworzone w swojej aplikacji, można użyć toodetermine takich informacji.

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
> Gdy istnieją przydziałów domyślnych dla subskrypcji platformy Azure i usługi, wiele z tych limitów może być zgłaszany przez żądania w hello [portalu Azure][azure_portal]. Na przykład, zobacz [przydziały i limity dla usługi partia zadań Azure hello](batch-quota-limit.md) instrukcje dotyczące zwiększenie przydziałami konta usługi partia zadań.
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a>Usługi Azure AD za pomocą zarządzania partii .NET

Biblioteka zarządzania partiami platformy .NET Hello jest klientem dostawcy zasobów platformy Azure i jest używany razem z [usługi Azure Resource Manager] [ resman_overview] toomanage konta zasobów programowo. Usługi Azure AD jest żądań tooauthenticate wymagane przez dowolnego klienta dostawcy zasobów platformy Azure, w tym hello biblioteki zarządzania partiami platformy .NET oraz [usługi Azure Resource Manager][resman_overview]. Aby dowiedzieć się, jak za pomocą usługi Azure AD z hello biblioteki zarządzania partiami platformy .NET, zobacz [rozwiązań partii tooauthenticate użycia usługi Azure Active Directory](batch-aad-auth.md). 

## <a name="sample-project-on-github"></a>Przykładowy projekt w witrynie GitHub

toosee zarządzania partiami platformy .NET w akcji, zapoznaj się z hello [AccountManagment] [ acct_mgmt_sample] przykładowy projekt w witrynie GitHub. AccountManagment Przykładowa aplikacja Hello przedstawiono hello następujące operacje:

1. Uzyskanie tokenu zabezpieczającego z usługi Azure AD przy użyciu [ADAL][aad_adal]. Witaj użytkownik nie jest już zalogowany, są monitowani o podanie poświadczeń platformy Azure.
2. Token zabezpieczający hello uzyskane z usługi Azure AD, tworzenie [SubscriptionClient] [ resman_subclient] tooquery Azure, aby uzyskać listę subskrypcji skojarzonych z kontem hello. Witaj użytkownik może wybrać subskrypcję z listy hello, jeśli zawiera więcej niż jedną subskrypcję.
3. Uzyskiwanie poświadczeń skojarzonych z subskrypcją hello wybrane.
4. Utwórz [element ResourceManagementClient] [ resman_client] obiektu przy użyciu poświadczeń hello.
5. Użyj [element ResourceManagementClient] [ resman_client] obiekt toocreate grupę zasobów.
6. Użyj [BatchManagementClient] [ net_mgmt_client] obiekt tooperform kilka operacji konto usługi partia zadań:
   * Utwórz konto wsadowe w hello nową grupę zasobów.
   * Pobierz hello nowo utworzone konto z hello usługa partia zadań.
   * Klucze konta wydruku hello hello nowego konta.
   * Ponowne generowanie klucza podstawowego dla konta hello.
   * Informacje o limicie przydziału wydruku hello hello konta.
   * Informacje o limicie przydziału wydruku hello hello subskrypcji.
   * Wydrukowanie wszystkich kont w ramach subskrypcji hello.
   * Usuń nowo utworzonego konta.
7. Usuń grupę zasobów hello.

Przed usunięciem partii hello nowo utworzona grupa kont i zasobów, można je przeglądać w hello [portalu Azure][azure_portal]:

aplikacja przykładowa hello toorun pomyślnie, najpierw należy zarejestrować go z dzierżawy usługi Azure AD w hello Azure portal i przyznać uprawnienia toohello interfejsu API usługi Azure Resource Manager. Procedura hello w [rozwiązań do zarządzania partii uwierzytelniania z usługi Active Directory](batch-aad-auth-management.md).


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
