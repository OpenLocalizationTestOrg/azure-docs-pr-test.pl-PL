---
title: "aaaSet zapasowej Azure Key Vault z rotacją kluczy end-to-end i inspekcji | Dokumentacja firmy Microsoft"
description: "Użyj tego jak tootoohelp, Pobierz skonfigurowane z rotacją kluczy i monitorowania dzienniki magazynu kluczy."
services: key-vault
documentationcenter: 
author: swgriffith
manager: mbaldwin
tags: 
ms.assetid: 9cd7e15e-23b8-41c0-a10a-06e6207ed157
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: jodehavi;stgriffi
ms.openlocfilehash: e0c393873077e3b91adc9fa7f39128bc1b6abe26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a><span data-ttu-id="720ee-103">Konfigurowanie kompleksowej wymiany i inspekcji kluczy w usłudze Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="720ee-103">Set up Azure Key Vault with end-to-end key rotation and auditing</span></span>
## <a name="introduction"></a><span data-ttu-id="720ee-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="720ee-104">Introduction</span></span>
<span data-ttu-id="720ee-105">Po utworzeniu magazynu kluczy, będzie możliwe toostart przy użyciu tego toostore magazynu kluczy i kluczy tajnych.</span><span class="sxs-lookup"><span data-stu-id="720ee-105">After creating your key vault, you will be able toostart using that vault toostore your keys and secrets.</span></span> <span data-ttu-id="720ee-106">Aplikacje nie muszą już toopersist Twojego kluczy ani kluczy tajnych, ale raczej zażąda je z magazynu kluczy hello zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="720ee-106">Your applications no longer need toopersist your keys or secrets, but rather will request them from hello key vault as needed.</span></span> <span data-ttu-id="720ee-107">Dzięki temu można tooupdate kluczy i kluczy tajnych bez wpływu na powitania zachowanie aplikacji, która otwiera szerokości możliwości wokół klucza, a tajny zarządzania.</span><span class="sxs-lookup"><span data-stu-id="720ee-107">This allows you tooupdate keys and secrets without affecting hello behavior of your application, which opens up a breadth of possibilities around your key and secret management.</span></span>

<span data-ttu-id="720ee-108">W tym artykule przedstawiono przykład użycia usługi Azure Key Vault toostore klucz tajny, w tym przypadku klucz konta magazynu Azure, który jest dostępny przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="720ee-108">This article walks through an example of using Azure Key Vault toostore a secret, in this case an Azure Storage Account key that is accessed by an application.</span></span> <span data-ttu-id="720ee-109">Ilustruje też implementacji zaplanowane obrotu tego klucza konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="720ee-109">It also demonstrates implementation of a scheduled rotation of that storage account key.</span></span> <span data-ttu-id="720ee-110">Na koniec przeprowadzi przez Pokaz sposobu toomonitor hello dzienników inspekcji magazynu kluczy i zgłaszanie alertów po nieoczekiwany żądań.</span><span class="sxs-lookup"><span data-stu-id="720ee-110">Finally, it walks through a demonstration of how toomonitor hello key vault audit logs and raise alerts when unexpected requests are made.</span></span>

> [!NOTE]
> <span data-ttu-id="720ee-111">W tym samouczku nie jest zamierzone tooexplain szczegółów hello początkowej konfiguracji magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="720ee-111">This tutorial is not intended tooexplain in detail hello initial setup of your key vault.</span></span> <span data-ttu-id="720ee-112">Te informacje można znaleźć w temacie [Rozpoczynanie pracy z usługą Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="720ee-112">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="720ee-113">Aby uzyskać instrukcje Międzyplatformowego interfejsu wiersza polecenia, zobacz [Zarządzanie Key Vault przy użyciu interfejsu wiersza polecenia](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="720ee-113">For Cross-Platform Command-Line Interface instructions, see [Manage Key Vault using CLI](key-vault-manage-with-cli2.md).</span></span>
>
>

## <a name="set-up-key-vault"></a><span data-ttu-id="720ee-114">Konfigurowanie usługi Key Vault</span><span class="sxs-lookup"><span data-stu-id="720ee-114">Set up Key Vault</span></span>
<span data-ttu-id="720ee-115">tooenable tooretrieve aplikacji klucza tajnego z magazynu kluczy, należy najpierw utworzyć klucz tajny hello i przekaż go tooyour magazynu.</span><span class="sxs-lookup"><span data-stu-id="720ee-115">tooenable an application tooretrieve a secret from Key Vault, you must first create hello secret and upload it tooyour vault.</span></span> <span data-ttu-id="720ee-116">Można to zrobić przez uruchamianie sesji programu PowerShell systemu Azure i zalogowanie tooyour konto platformy Azure z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="720ee-116">This can be accomplished by starting an Azure PowerShell session and signing in tooyour Azure account with hello following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="720ee-117">W oknie wyskakującym przeglądarki hello wprowadź nazwę użytkownika konta platformy Azure i hasło.</span><span class="sxs-lookup"><span data-stu-id="720ee-117">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="720ee-118">PowerShell pobierze wszystkie subskrypcje hello, które są skojarzone z tym kontem.</span><span class="sxs-lookup"><span data-stu-id="720ee-118">PowerShell will get all hello subscriptions that are associated with this account.</span></span> <span data-ttu-id="720ee-119">Używa programu PowerShell hello pierwszego domyślnie.</span><span class="sxs-lookup"><span data-stu-id="720ee-119">PowerShell uses hello first one by default.</span></span>

<span data-ttu-id="720ee-120">Jeśli masz wiele subskrypcji może być toospecify Witaj, który został użyty toocreate Twojego magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="720ee-120">If you have multiple subscriptions, you might have toospecify hello one that was used toocreate your key vault.</span></span> <span data-ttu-id="720ee-121">Wprowadź powitania po toosee hello subskrypcje dla swojego konta:</span><span class="sxs-lookup"><span data-stu-id="720ee-121">Enter hello following toosee hello subscriptions for your account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="720ee-122">toospecify hello subskrypcji, która jest skojarzona z magazynem kluczy hello, który będziesz rejestrować, wpisz:</span><span class="sxs-lookup"><span data-stu-id="720ee-122">toospecify hello subscription that's associated with hello key vault you will be logging, enter:</span></span>

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

<span data-ttu-id="720ee-123">Ponieważ w tym artykule przedstawiono przechowywania jako klucz tajny klucz konta magazynu, należy pobrać ten klucz konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="720ee-123">Because this article demonstrates storing a storage account key as a secret, you must get that storage account key.</span></span>

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

<span data-ttu-id="720ee-124">Po pobraniu klucz tajny (w tym przypadku klucz konta magazynu), należy przekonwertować tej tooa bezpieczny ciąg, a następnie utwórz klucz tajny z daną wartością, w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="720ee-124">After retrieving your secret (in this case, your storage account key), you must convert that tooa secure string and then create a secret with that value in your key vault.</span></span>

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
<span data-ttu-id="720ee-125">Następnie Pobierz hello identyfikatora URI dla hello klucz tajny, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="720ee-125">Next, get hello URI for hello secret you created.</span></span> <span data-ttu-id="720ee-126">Służy to w kolejnym kroku podczas wywoływania tooretrieve magazynu kluczy hello klucz tajny.</span><span class="sxs-lookup"><span data-stu-id="720ee-126">This is used in a later step when you call hello key vault tooretrieve your secret.</span></span> <span data-ttu-id="720ee-127">Uruchom następujące polecenia programu PowerShell hello i zanotuj wartość Identyfikatora hello, która jest klucz tajny hello identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="720ee-127">Run hello following PowerShell command and make note of hello ID value, which is hello secret URI:</span></span>

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-hello-application"></a><span data-ttu-id="720ee-128">Konfigurowanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="720ee-128">Set up hello application</span></span>
<span data-ttu-id="720ee-129">Teraz, po klucz tajny przechowywane można użyć tooretrieve kodu i użyć go.</span><span class="sxs-lookup"><span data-stu-id="720ee-129">Now that you have a secret stored, you can use code tooretrieve and use it.</span></span> <span data-ttu-id="720ee-130">Istnieje kilka czynności, wymagane tooachieve to.</span><span class="sxs-lookup"><span data-stu-id="720ee-130">There are a few steps required tooachieve this.</span></span> <span data-ttu-id="720ee-131">Witaj pierwszy i Najważniejszy krok jest rejestrowanie aplikacji w usłudze Azure Active Directory i następnie informuje usługi Key Vault informacje o aplikacji, dzięki czemu można zezwolić żądań od aplikacji.</span><span class="sxs-lookup"><span data-stu-id="720ee-131">hello first and most important step is registering your application with Azure Active Directory and then telling Key Vault your application information so that it can allow requests from your application.</span></span>

> [!NOTE]
> <span data-ttu-id="720ee-132">Aplikacja musi być utworzone na powitania takie same dzierżawy usługi Azure Active Directory jako magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="720ee-132">Your application must be created on hello same Azure Active Directory tenant as your key vault.</span></span>
>
>

<span data-ttu-id="720ee-133">Otwórz kartę aplikacji hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="720ee-133">Open hello applications tab of Azure Active Directory.</span></span>

![Otwarte aplikacje w usłudze Azure Active Directory](./media/keyvault-keyrotation/AzureAD_Header.png)

<span data-ttu-id="720ee-135">Wybierz **dodać** tooadd tooyour aplikacji usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="720ee-135">Choose **ADD** tooadd an application tooyour Azure Active Directory.</span></span>

![Wybierz przycisk Dodaj](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

<span data-ttu-id="720ee-137">Pozostaw typ aplikacji hello jako **interfejsu API sieci WEB i/lub aplikacji sieci WEB** i nadaj nazwę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="720ee-137">Leave hello application type as **WEB APPLICATION AND/OR WEB API** and give your application a name.</span></span>

![Nazwa hello aplikacji](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

<span data-ttu-id="720ee-139">Nadaj aplikacji **adres URL logowania** i **identyfikator URI aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="720ee-139">Give your application a **SIGN-ON URL** and an **APP ID URI**.</span></span> <span data-ttu-id="720ee-140">Mogą to być dowolnych znaków dla tego pokazu i mogą zostać zmienione później w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="720ee-140">These can be anything you want for this demo, and they can be changed later if needed.</span></span>

![Podaj wymagane identyfikatorów URI](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

<span data-ttu-id="720ee-142">Po dodaniu aplikacji hello tooAzure usługi Active Directory zostanie wyświetlona na stronie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="720ee-142">After hello application is added tooAzure Active Directory, you will be brought into hello application page.</span></span> <span data-ttu-id="720ee-143">Kliknij przycisk hello **Konfiguruj** karcie, a następnie znajdź i skopiuj hello **identyfikator klienta** wartość.</span><span class="sxs-lookup"><span data-stu-id="720ee-143">Click hello **Configure** tab and then find and copy hello **Client ID** value.</span></span> <span data-ttu-id="720ee-144">Zwróć uwagę na powitania Identyfikatora klienta dla kolejnych krokach.</span><span class="sxs-lookup"><span data-stu-id="720ee-144">Make note of hello client ID for later steps.</span></span>

<span data-ttu-id="720ee-145">Następnie wygeneruj klucz dla aplikacji, może współdziałać z usługą Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="720ee-145">Next, generate a key for your application so it can interact with your Azure Active Directory.</span></span> <span data-ttu-id="720ee-146">Można go utworzyć w obszarze hello **klucze** części hello **konfiguracji** kartę. Zanotuj klucz hello nowo wygenerowane z aplikacji Azure Active Directory do użycia w kolejnym kroku.</span><span class="sxs-lookup"><span data-stu-id="720ee-146">You can create this under hello **Keys** section in hello **Configuration** tab. Make note of hello newly generated key from your Azure Active Directory application for use in a later step.</span></span>

![Klucze aplikacji usługi Azure Active Directory](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

<span data-ttu-id="720ee-148">Zanim zostanie nawiązana wszystkie wywołania z aplikacji do magazynu kluczy hello, musi Poinformuj hello magazyn kluczy o aplikacji i ich uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="720ee-148">Before establishing any calls from your application into hello key vault, you must tell hello key vault about your application and its permissions.</span></span> <span data-ttu-id="720ee-149">Witaj poniższe polecenie pobiera nazwę magazynu hello i hello identyfikator klienta aplikacji usługi Azure Active Directory i przyznaje **uzyskać** magazynu kluczy tooyour dostępu dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="720ee-149">hello following command takes hello vault name and hello client ID from your Azure Active Directory app and grants **Get** access tooyour key vault for hello application.</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

<span data-ttu-id="720ee-150">W tym momencie jest gotowy toostart tworzenia połączeń aplikacji.</span><span class="sxs-lookup"><span data-stu-id="720ee-150">At this point, you are ready toostart building your application calls.</span></span> <span data-ttu-id="720ee-151">W aplikacji należy zainstalować toointeract wymagane pakiety NuGet hello z usługi Azure Key Vault i Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="720ee-151">In your application, you must install hello NuGet packages required toointeract with Azure Key Vault and Azure Active Directory.</span></span> <span data-ttu-id="720ee-152">Za pomocą konsoli Menedżera pakietów programu Visual Studio hello wprowadź hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="720ee-152">From hello Visual Studio Package Manager console, enter hello following commands.</span></span> <span data-ttu-id="720ee-153">Na powitania pisania tego artykułu, hello bieżącej wersji pakietu usługi Azure Active Directory hello jest 3.10.305231913, dzięki czemu może mają tooconfirm hello najnowszej wersji i odpowiednio zaktualizować.</span><span class="sxs-lookup"><span data-stu-id="720ee-153">At hello writing of this article, hello current version of hello Azure Active Directory package is 3.10.305231913, so you might want tooconfirm hello latest version and update accordingly.</span></span>

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

<span data-ttu-id="720ee-154">W kodzie aplikacji Utwórz metodę hello toohold klasy na potrzeby uwierzytelniania usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="720ee-154">In your application code, create a class toohold hello method for your Azure Active Directory authentication.</span></span> <span data-ttu-id="720ee-155">W tym przykładzie tej klasy, nosi **witryny**.</span><span class="sxs-lookup"><span data-stu-id="720ee-155">In this example, that class is called **Utils**.</span></span> <span data-ttu-id="720ee-156">Dodaj następujące hello instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="720ee-156">Add hello following using statement:</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="720ee-157">Następnie dodaj hello poniższych token JWT hello tooretrieve metody z usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="720ee-157">Next, add hello following method tooretrieve hello JWT token from Azure Active Directory.</span></span> <span data-ttu-id="720ee-158">Łatwość utrzymania można toomove hello ustalony ciągami w konfiguracji sieci web lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="720ee-158">For maintainability, you may want toomove hello hard-coded string values into your web or application configuration.</span></span>

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

<span data-ttu-id="720ee-159">Dodaj toocall wymagany kod hello magazyn kluczy i pobrać poufną wartość.</span><span class="sxs-lookup"><span data-stu-id="720ee-159">Add hello necessary code toocall Key Vault and retrieve your secret value.</span></span> <span data-ttu-id="720ee-160">Najpierw należy dodać następujące hello instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="720ee-160">First you must add hello following using statement:</span></span>

```csharp
using Microsoft.Azure.KeyVault;
```

<span data-ttu-id="720ee-161">Dodaj tooinvoke wywołania metody hello magazyn kluczy i pobrać klucz tajny.</span><span class="sxs-lookup"><span data-stu-id="720ee-161">Add hello method calls tooinvoke Key Vault and retrieve your secret.</span></span> <span data-ttu-id="720ee-162">W przypadku tej metody musisz podać hasło hello identyfikator URI, który został zapisany w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="720ee-162">In this method, you provide hello secret URI that you saved in a previous step.</span></span> <span data-ttu-id="720ee-163">Należy zwrócić uwagę użycie hello hello **GetToken** metody z hello **witryny** klasy utworzone wcześniej.</span><span class="sxs-lookup"><span data-stu-id="720ee-163">Note hello use of hello **GetToken** method from hello **Utils** class created previously.</span></span>

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

<span data-ttu-id="720ee-164">Po uruchomieniu aplikacji, użytkownik powinien teraz autoryzowany tooAzure usługi Active Directory i następnie pobierania poufną wartość z usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="720ee-164">When you run your application, you should now be authenticating tooAzure Active Directory and then retrieving your secret value from Azure Key Vault.</span></span>

## <a name="key-rotation-using-azure-automation"></a><span data-ttu-id="720ee-165">Obracanie klucza przy użyciu usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="720ee-165">Key rotation using Azure Automation</span></span>
<span data-ttu-id="720ee-166">Istnieją różne opcje wdrażania strategii obrotu wartości, które są przechowywane jako klucze tajne usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="720ee-166">There are various options for implementing a rotation strategy for values you store as Azure Key Vault secrets.</span></span> <span data-ttu-id="720ee-167">Klucze tajne można obracać jako część ręczny proces, ich może zostać obrócona programowo przy użyciu interfejsu API lub może zostać obrócona i skryptów automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="720ee-167">Secrets can be rotated as part of a manual process, they may be rotated programmatically by using API calls, or they may be rotated by way of an Automation script.</span></span> <span data-ttu-id="720ee-168">Dla celów hello w tym artykule, można za pomocą programu Azure PowerShell połączone z toochange usługi Automatyzacja Azure klucza dostępu konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="720ee-168">For hello purposes of this article, you will be using Azure PowerShell combined with Azure Automation toochange an Azure Storage Account access key.</span></span> <span data-ttu-id="720ee-169">Następnie zaktualizuje klucza tajnego klucza magazynu z tego nowego klucza.</span><span class="sxs-lookup"><span data-stu-id="720ee-169">You will then update a key vault secret with that new key.</span></span>

<span data-ttu-id="720ee-170">tooallow usługi Automatyzacja Azure tooset tajny wartości w magazynie kluczy, należy uzyskać identyfikator klienta hello hello połączenia o nazwie AzureRunAsConnection, który został utworzony podczas ustanawiania wystąpienia usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="720ee-170">tooallow Azure Automation tooset secret values in your key vault, you must get hello client ID for hello connection named AzureRunAsConnection, which was created when you established your Azure Automation instance.</span></span> <span data-ttu-id="720ee-171">Ten identyfikator można znaleźć, wybierając **zasoby** z wystąpieniem usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="720ee-171">You can find this ID by choosing **Assets** from your Azure Automation instance.</span></span> <span data-ttu-id="720ee-172">Z tego miejsca, możesz wybrać **połączeń** , a następnie wybierz hello **AzureRunAsConnection** usługi zasady.</span><span class="sxs-lookup"><span data-stu-id="720ee-172">From there, you choose **Connections** and then select hello **AzureRunAsConnection** service principle.</span></span> <span data-ttu-id="720ee-173">Zwróć uwagę na powitania **identyfikator aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="720ee-173">Take note of hello **Application ID**.</span></span>

![Identyfikator klienta usługi Automatyzacja Azure](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

<span data-ttu-id="720ee-175">W **zasoby**, wybierz **modułów**.</span><span class="sxs-lookup"><span data-stu-id="720ee-175">In **Assets**, choose **Modules**.</span></span> <span data-ttu-id="720ee-176">Z **modułów**, wybierz pozycję **galerii**, a następnie wyszukaj i **importu** zaktualizowane wersje każdego hello następujących modułów:</span><span class="sxs-lookup"><span data-stu-id="720ee-176">From **Modules**, select **Gallery**, and then search for and **Import** updated versions of each of hello following modules:</span></span>

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> <span data-ttu-id="720ee-177">Na powitania pisania tego artykułu, hello toobe wcześniej dostrzeżone modułów potrzebne aktualizowana tylko dla następującego skryptu hello.</span><span class="sxs-lookup"><span data-stu-id="720ee-177">At hello writing of this article, only hello previously noted modules needed toobe updated for hello following script.</span></span> <span data-ttu-id="720ee-178">Jeśli okaże się, że zadanie usługi Automatyzacja nie działa prawidłowo, upewnij się, że został zaimportowany wszystkie niezbędne moduły oraz ich zależności.</span><span class="sxs-lookup"><span data-stu-id="720ee-178">If you find that your automation job is failing, confirm that you have imported all necessary modules and their dependencies.</span></span>
>
>

<span data-ttu-id="720ee-179">Po pobraniu Identyfikatora aplikacji hello połączenia usługi Automatyzacja Azure, należy wskazać magazynu kluczy czy tej aplikacji ma dostęp do kluczy tajnych z tooupdate w magazynie.</span><span class="sxs-lookup"><span data-stu-id="720ee-179">After you have retrieved hello application ID for your Azure Automation connection, you must tell your key vault that this application has access tooupdate secrets in your vault.</span></span> <span data-ttu-id="720ee-180">Można to zrobić z hello następującego polecenia programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="720ee-180">This can be accomplished with hello following PowerShell command:</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

<span data-ttu-id="720ee-181">Następnie wybierz pozycję **Runbook** w wystąpieniu usługi Automatyzacja Azure, a następnie wybierz **Dodaj element Runbook**.</span><span class="sxs-lookup"><span data-stu-id="720ee-181">Next, select **Runbooks** under your Azure Automation instance, and then select **Add a Runbook**.</span></span> <span data-ttu-id="720ee-182">Wybierz pozycję **Szybkie tworzenie**.</span><span class="sxs-lookup"><span data-stu-id="720ee-182">Select **Quick Create**.</span></span> <span data-ttu-id="720ee-183">Nazwa elementu runbook i wybierz **PowerShell** jako hello typ elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="720ee-183">Name your runbook and select **PowerShell** as hello runbook type.</span></span> <span data-ttu-id="720ee-184">Masz hello tooadd opcja opis.</span><span class="sxs-lookup"><span data-stu-id="720ee-184">You have hello option tooadd a description.</span></span> <span data-ttu-id="720ee-185">Na koniec kliknij **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="720ee-185">Finally, click **Create**.</span></span>

![Tworzenie elementu runbook](./media/keyvault-keyrotation/Create_Runbook.png)

<span data-ttu-id="720ee-187">Wklej hello następującego skryptu programu PowerShell w okienku Edytora hello na nowy element runbook:</span><span class="sxs-lookup"><span data-stu-id="720ee-187">Paste hello following PowerShell script in hello editor pane for your new runbook:</span></span>

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get hello connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in tooAzure..."
    Add-AzureRmAccount `
        -ServicePrincipal `
        -TenantId $servicePrincipalConnection.TenantId `
        -ApplicationId $servicePrincipalConnection.ApplicationId `
        -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
    "Login complete."
}
catch {
    if (!$servicePrincipalConnection)
    {
        $ErrorMessage = "Connection $connectionName not found."
        throw $ErrorMessage
    } else{
        Write-Error -Message $_.Exception
        throw $_.Exception
    }
}

#Optionally you may set hello following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for hello storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

<span data-ttu-id="720ee-188">W okienku Edytora hello wybierz **okienku testu** tootest skryptu.</span><span class="sxs-lookup"><span data-stu-id="720ee-188">From hello editor pane, choose **Test pane** tootest your script.</span></span> <span data-ttu-id="720ee-189">Po hello skrypt jest uruchamiany bez błędów, można wybrać **publikowania**, a następnie można zastosować harmonogram dla elementu runbook hello w okienku konfiguracji elementu runbook hello.</span><span class="sxs-lookup"><span data-stu-id="720ee-189">Once hello script is running without error, you can select **Publish**, and then you can apply a schedule for hello runbook back in hello runbook configuration pane.</span></span>

## <a name="key-vault-auditing-pipeline"></a><span data-ttu-id="720ee-190">Potok inspekcji usługi Key Vault</span><span class="sxs-lookup"><span data-stu-id="720ee-190">Key Vault auditing pipeline</span></span>
<span data-ttu-id="720ee-191">Po skonfigurowaniu magazynu kluczy można włączyć inspekcję toocollect dzienniki na żądania dostępu do magazynu kluczy toohello.</span><span class="sxs-lookup"><span data-stu-id="720ee-191">When you set up a key vault, you can turn on auditing toocollect logs on access requests made toohello key vault.</span></span> <span data-ttu-id="720ee-192">Te dzienniki są przechowywane w wyznaczonym konta magazynu Azure i można ściągnąć, monitorowania i analizy.</span><span class="sxs-lookup"><span data-stu-id="720ee-192">These logs are stored in a designated Azure Storage account and can be pulled out, monitored, and analyzed.</span></span> <span data-ttu-id="720ee-193">Hello następujący scenariusz używa usługę Azure functions, aplikacje logiki platformy Azure i toocreate dzienniki inspekcji magazynu kluczy toosend potok wiadomości e-mail w przypadku aplikacji, która pasuje do Identyfikatora aplikacji hello hello aplikacji sieci web pobiera kluczy tajnych z magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="720ee-193">hello following scenario uses Azure functions, Azure logic apps, and key vault audit logs toocreate a pipeline toosend an email when an app that does match hello app ID of hello web app retrieves secrets from hello vault.</span></span>

<span data-ttu-id="720ee-194">Najpierw należy włączyć rejestrowanie w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="720ee-194">First, you must enable logging on your key vault.</span></span> <span data-ttu-id="720ee-195">Można to zrobić za pomocą następujących poleceń programu PowerShell hello (szczegółowe informacje są widoczne w [klucza magazynu rejestrowania](key-vault-logging.md)):</span><span class="sxs-lookup"><span data-stu-id="720ee-195">This can be done via hello following PowerShell commands (full details can be seen at [key-vault-logging](key-vault-logging.md)):</span></span>

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

<span data-ttu-id="720ee-196">Po włączeniu to rozpoczęcia zbierania do konta magazynu wyznaczonego hello dzienniki inspekcji.</span><span class="sxs-lookup"><span data-stu-id="720ee-196">After this is enabled, audit logs start collecting into hello designated storage account.</span></span> <span data-ttu-id="720ee-197">Te dzienniki zawiera zdarzenia o jak i kiedy są dostępne z magazynów kluczy i przez kogo.</span><span class="sxs-lookup"><span data-stu-id="720ee-197">These logs contain events about how and when your key vaults are accessed, and by whom.</span></span>

> [!NOTE]
> <span data-ttu-id="720ee-198">Dostępne informacji rejestrowania 10 minut od hello operacji magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="720ee-198">You can access your logging information 10 minutes after hello key vault operation.</span></span> <span data-ttu-id="720ee-199">Zwykle jest krótszy.</span><span class="sxs-lookup"><span data-stu-id="720ee-199">It will usually be quicker than this.</span></span>
>
>

<span data-ttu-id="720ee-200">Witaj, następnym krokiem jest zbyt[Utwórz kolejkę Azure Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="720ee-200">hello next step is too[create an Azure Service Bus queue](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span> <span data-ttu-id="720ee-201">Jest to, gdzie są usuwane, dzienniki inspekcji magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="720ee-201">This is where key vault audit logs are pushed.</span></span> <span data-ttu-id="720ee-202">Gdy komunikaty dziennika inspekcji hello znajdują się w kolejce hello, aplikację logiki hello przejmuje je i działa na nich.</span><span class="sxs-lookup"><span data-stu-id="720ee-202">When hello audit log messages are in hello queue, hello logic app picks them up and acts on them.</span></span> <span data-ttu-id="720ee-203">Tworzenie usługi service bus z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="720ee-203">Create a service bus with hello following steps:</span></span>

1. <span data-ttu-id="720ee-204">Tworzenie przestrzeni nazw usługi Service Bus (Jeśli masz już konto, które mają toouse w tym celu przejdź tooStep 2).</span><span class="sxs-lookup"><span data-stu-id="720ee-204">Create a Service Bus namespace (if you already have one that you want toouse for this, skip tooStep 2).</span></span>
2. <span data-ttu-id="720ee-205">Przeglądaj toohello usługi service bus w hello portalu Azure i nazw hello wybierz żądane toocreate hello kolejki w.</span><span class="sxs-lookup"><span data-stu-id="720ee-205">Browse toohello service bus in hello Azure portal and select hello namespace you want toocreate hello queue in.</span></span>
3. <span data-ttu-id="720ee-206">Wybierz **nowy** i wybierz polecenie **usługi Service Bus > kolejki** i wprowadź szczegóły hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="720ee-206">Select **New** and choose **Service Bus > Queue** and enter hello required details.</span></span>
4. <span data-ttu-id="720ee-207">Wybierz informacje o połączeniu usługi Service Bus hello Wybieranie hello przestrzeni nazw, a następnie klikając polecenie **informacje o połączeniu**.</span><span class="sxs-lookup"><span data-stu-id="720ee-207">Select hello Service Bus connection information by choosing hello namespace and clicking **Connection Information**.</span></span> <span data-ttu-id="720ee-208">Informacje te będą potrzebne dla hello następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="720ee-208">You will need this information for hello next section.</span></span>

<span data-ttu-id="720ee-209">Następnie [Tworzenie funkcji platformy Azure](../azure-functions/functions-create-first-azure-function.md) dzienniki magazynu kluczy toopoll poziomu hello konta magazynu i odebrania nowych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="720ee-209">Next, [create an Azure function](../azure-functions/functions-create-first-azure-function.md) toopoll key vault logs within hello storage account and pick up new events.</span></span> <span data-ttu-id="720ee-210">Jest to funkcja, która zostanie wywołany zgodnie z harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="720ee-210">This will be a function that is triggered on a schedule.</span></span>

<span data-ttu-id="720ee-211">toocreate funkcji platformy Azure, wybierz **nowy > aplikacji funkcji** w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="720ee-211">toocreate an Azure function, choose **New > Function App** in hello Azure portal.</span></span> <span data-ttu-id="720ee-212">Podczas tworzenia można użyć istniejącego planu obsługi lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="720ee-212">During creation, you can use an existing hosting plan or create a new one.</span></span> <span data-ttu-id="720ee-213">Można również wybrać do obsługi dynamicznej.</span><span class="sxs-lookup"><span data-stu-id="720ee-213">You could also opt for dynamic hosting.</span></span> <span data-ttu-id="720ee-214">Więcej informacji na temat funkcji hosting opcje można znaleźć w folderze [jak tooscale usługi Azure Functions](../azure-functions/functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="720ee-214">More details on Function hosting options can be found at [How tooscale Azure Functions](../azure-functions/functions-scale.md).</span></span>

<span data-ttu-id="720ee-215">Po utworzeniu hello funkcji platformy Azure, przejdź tooit i wybierz czasomierz funkcji i C\#.</span><span class="sxs-lookup"><span data-stu-id="720ee-215">When hello Azure function is created, navigate tooit and choose a timer function and C\#.</span></span> <span data-ttu-id="720ee-216">Następnie kliknij przycisk **tworzenia tej funkcji**.</span><span class="sxs-lookup"><span data-stu-id="720ee-216">Then click **Create this function**.</span></span>

![Blok funkcji Start Azure](./media/keyvault-keyrotation/Azure_Functions_Start.png)

<span data-ttu-id="720ee-218">Na powitania **opracowanie** karcie, Zastąp kod run.csx hello hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="720ee-218">On hello **Develop** tab, replace hello run.csx code with hello following:</span></span>

```csharp
#r "Newtonsoft.Json"

using System;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.ServiceBus.Messaging;
using System.Text;

public static void Run(TimerInfo myTimer, TextReader inputBlob, TextWriter outputBlob, TraceWriter log)
{
    log.Info("Starting");

    CloudStorageAccount sourceStorageAccount = new CloudStorageAccount(new StorageCredentials("<STORAGE_ACCOUNT_NAME>", "<STORAGE_ACCOUNT_KEY>"), true);

    CloudBlobClient sourceCloudBlobClient = sourceStorageAccount.CreateCloudBlobClient();

    var connectionString = "<SERVICE_BUS_CONNECTION_STRING>";
    var queueName = "<SERVICE_BUS_QUEUE_NAME>";

    var sbClient = QueueClient.CreateFromConnectionString(connectionString, queueName);

    DateTime dtPrev = DateTime.UtcNow;
    if(inputBlob != null)
    {
        var txt = inputBlob.ReadToEnd();

        if(!string.IsNullOrEmpty(txt))
        {
            dtPrev = DateTime.Parse(txt);
            log.Verbose($"SyncPoint: {dtPrev.ToString("O")}");
        }
        else
        {
            dtPrev = DateTime.UtcNow;
            log.Verbose($"Sync point file didnt have a date. Setting toonow.");
        }
    }

    var now = DateTime.UtcNow;

    string blobPrefix = "insights-logs-auditevent/resourceId=/SUBSCRIPTIONS/<SUBSCRIPTION_ID>/RESOURCEGROUPS/<RESOURCE_GROUP_NAME>/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/<KEY_VAULT_NAME>/y=" + now.Year +"/m="+now.Month.ToString("D2")+"/d="+ (now.Day).ToString("D2")+"/h="+(now.Hour).ToString("D2")+"/m=00/";

    log.Info($"Scanning:  {blobPrefix}");

    IEnumerable<IListBlobItem> blobs = sourceCloudBlobClient.ListBlobs(blobPrefix, true);

    log.Info($"found {blobs.Count()} blobs");

    foreach(var item in blobs)
    {
        if (item is CloudBlockBlob)
        {
            CloudBlockBlob blockBlob = (CloudBlockBlob)item;

            log.Info($"Syncing: {item.Uri}");

            string sharedAccessUri = GetContainerSasUri(blockBlob);

            CloudBlockBlob sourceBlob = new CloudBlockBlob(new Uri(sharedAccessUri));

            string text;
            using (var memoryStream = new MemoryStream())
            {
                sourceBlob.DownloadToStream(memoryStream);
                text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
            }

            dynamic dynJson = JsonConvert.DeserializeObject(text);

            //required tooorder by time as they may not be in hello file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending tooServiceBus, use hello payloadStream and set keeporiginal tootrue
                    var message = new BrokeredMessage(payloadStream, true);
                    sbClient.Send(message);
                    dtPrev = dt;
                }
            }
        }
    }
    outputBlob.Write(dtPrev.ToString("o"));
}

static string GetContainerSasUri(CloudBlockBlob blob)
{
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();

    sasConstraints.SharedAccessStartTime = DateTime.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> <span data-ttu-id="720ee-219">Utwórz zmienne hello tooreplace się, że w hello poprzedzających konta magazynu tooyour toopoint kodu, w której zapisywane są dzienniki magazynu kluczy hello, hello usługi service bus, który został utworzony wcześniej, a hello dzienniki magazynu magazynu kluczy toohello określonej ścieżki.</span><span class="sxs-lookup"><span data-stu-id="720ee-219">Make sure tooreplace hello variables in hello preceding code toopoint tooyour storage account where hello key vault logs are written, hello service bus you created earlier, and hello specific path toohello key vault storage logs.</span></span>
>
>

<span data-ttu-id="720ee-220">Funkcja Hello przejmuje hello najnowszego pliku dziennika z konta magazynu hello gdzie hello magazynu kluczy dziennikach, chwyty hello najnowsze zdarzenia z tego pliku i umieszcza je tooa kolejki usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="720ee-220">hello function picks up hello latest log file from hello storage account where hello key vault logs are written, grabs hello latest events from that file, and pushes them tooa Service Bus queue.</span></span> <span data-ttu-id="720ee-221">Ponieważ pojedynczy plik może mieć wiele zdarzeń, należy utworzyć plik sync.txt funkcja hello również analizuje toodetermine hello sygnaturę czasową ostatniego zdarzenia hello, która została pobrana.</span><span class="sxs-lookup"><span data-stu-id="720ee-221">Since a single file could have multiple events, you should create a sync.txt file that hello function also looks at toodetermine hello time stamp of hello last event that was picked up.</span></span> <span data-ttu-id="720ee-222">Dzięki temu, że nie push hello tego samego zdarzenia wiele razy.</span><span class="sxs-lookup"><span data-stu-id="720ee-222">This ensures that you don't push hello same event multiple times.</span></span> <span data-ttu-id="720ee-223">Ten plik sync.txt zawiera sygnaturę czasową dla ostatniego zdarzenia napotkano hello.</span><span class="sxs-lookup"><span data-stu-id="720ee-223">This sync.txt file contains a timestamp for hello last encountered event.</span></span> <span data-ttu-id="720ee-224">Hello dzienniki, gdy załadowano, mieć toobe sortowane oparte na powitania sygnatury czasowej tooensure są uporządkowane poprawnie.</span><span class="sxs-lookup"><span data-stu-id="720ee-224">hello logs, when loaded, have toobe sorted based on hello timestamp tooensure they are ordered correctly.</span></span>

<span data-ttu-id="720ee-225">Dla tej funkcji możemy odwoływać kilka dodatkowych bibliotek, które nie są dostępne fabrycznej hello w usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="720ee-225">For this function, we reference a couple of additional libraries that are not available out of hello box in Azure Functions.</span></span> <span data-ttu-id="720ee-226">tooinclude, potrzebujemy toopull usługi Azure Functions je przy użyciu narzędzia NuGet.</span><span class="sxs-lookup"><span data-stu-id="720ee-226">tooinclude these, we need Azure Functions toopull them using NuGet.</span></span> <span data-ttu-id="720ee-227">Wybierz hello **Wyświetl pliki** opcji.</span><span class="sxs-lookup"><span data-stu-id="720ee-227">Choose hello **View Files** option.</span></span>

![Wyświetlanie plików](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

<span data-ttu-id="720ee-229">I Dodaj plik o nazwie project.json o następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="720ee-229">And add a file called project.json with following content:</span></span>

```json
    {
      "frameworks": {
        "net46":{
          "dependencies": {
                "WindowsAzure.Storage": "7.0.0",
                "WindowsAzure.ServiceBus":"3.2.2"
          }
        }
       }
    }
```
<span data-ttu-id="720ee-230">Po **zapisać**, usługi Azure Functions pobierze hello wymagane pliki binarne.</span><span class="sxs-lookup"><span data-stu-id="720ee-230">Upon **Save**, Azure Functions will download hello required binaries.</span></span>

<span data-ttu-id="720ee-231">Przełącz toohello **integracji** karcie i nadaj hello czasomierza parametru toouse zrozumiałej nazwy, w obrębie hello funkcji.</span><span class="sxs-lookup"><span data-stu-id="720ee-231">Switch toohello **Integrate** tab and give hello timer parameter a meaningful name toouse within hello function.</span></span> <span data-ttu-id="720ee-232">W hello poprzedzających kodu, oczekuje hello toobe czasomierza o nazwie *myTimer*.</span><span class="sxs-lookup"><span data-stu-id="720ee-232">In hello preceding code, it expects hello timer toobe called *myTimer*.</span></span> <span data-ttu-id="720ee-233">Określ [wyrażenie CRON](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) w następujący sposób: 0 \* \* \* \* \* dla czasomierza hello, który spowoduje, że toorun funkcja hello raz na minutę.</span><span class="sxs-lookup"><span data-stu-id="720ee-233">Specify a [CRON expression](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) as follows: 0 \* \* \* \* \* for hello timer that will cause hello function toorun once a minute.</span></span>

<span data-ttu-id="720ee-234">Takie same na hello **integracji** , Dodaj danych wejściowych typu hello **magazyn obiektów Blob Azure**.</span><span class="sxs-lookup"><span data-stu-id="720ee-234">On hello same **Integrate** tab, add an input of hello type **Azure Blob Storage**.</span></span> <span data-ttu-id="720ee-235">Spowoduje to punktu toohello sync.txt pliku, który zawiera hello sygnatura czasowa ostatniego zdarzenia hello przeglądał przez funkcję hello.</span><span class="sxs-lookup"><span data-stu-id="720ee-235">This will point toohello sync.txt file that contains hello timestamp of hello last event looked at by hello function.</span></span> <span data-ttu-id="720ee-236">Będzie dostępna w ramach funkcji hello według nazwy parametru hello.</span><span class="sxs-lookup"><span data-stu-id="720ee-236">This will be available within hello function by hello parameter name.</span></span> <span data-ttu-id="720ee-237">W hello poprzedzających kodu, wprowadzania magazynu obiektów Blob Azure hello oczekuje toobe nazwę parametru hello *inputBlob*.</span><span class="sxs-lookup"><span data-stu-id="720ee-237">In hello preceding code, hello Azure Blob Storage input expects hello parameter name toobe *inputBlob*.</span></span> <span data-ttu-id="720ee-238">Wybierz konto magazynu hello której będą znajdować się plik sync.txt hello (może być hello tej samej lub innego konta magazynu).</span><span class="sxs-lookup"><span data-stu-id="720ee-238">Choose hello storage account where hello sync.txt file will reside (it could be hello same or a different storage account).</span></span> <span data-ttu-id="720ee-239">W polu Ścieżka hello Podaj ścieżkę hello, w którym znajduje się plik hello w formacie hello {container-name}/path/to/sync.txt.</span><span class="sxs-lookup"><span data-stu-id="720ee-239">In hello path field, provide hello path where hello file lives in hello format {container-name}/path/to/sync.txt.</span></span>

<span data-ttu-id="720ee-240">Dodaj dane wyjściowe typu hello *magazyn obiektów Blob Azure* danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="720ee-240">Add an output of hello type *Azure Blob Storage* output.</span></span> <span data-ttu-id="720ee-241">Spowoduje to punktu toohello sync.txt pliku, który zdefiniowano w danych wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="720ee-241">This will point toohello sync.txt file you defined in hello input.</span></span> <span data-ttu-id="720ee-242">To jest używany przez hello funkcja toowrite hello sygnatura czasowa ostatniego zdarzenia hello przeglądał.</span><span class="sxs-lookup"><span data-stu-id="720ee-242">This is used by hello function toowrite hello timestamp of hello last event looked at.</span></span> <span data-ttu-id="720ee-243">Witaj poprzedni kod oczekuje tego toobe parametr o nazwie *Blob_wyj*.</span><span class="sxs-lookup"><span data-stu-id="720ee-243">hello preceding code expects this parameter toobe called *outputBlob*.</span></span>

<span data-ttu-id="720ee-244">W tym momencie funkcja hello jest gotowy.</span><span class="sxs-lookup"><span data-stu-id="720ee-244">At this point, hello function is ready.</span></span> <span data-ttu-id="720ee-245">Upewnij się tooswitch toohello Wstecz **opracowanie** karcie i Zapisz hello kodu.</span><span class="sxs-lookup"><span data-stu-id="720ee-245">Make sure tooswitch back toohello **Develop** tab and save hello code.</span></span> <span data-ttu-id="720ee-246">Sprawdź okno danych wyjściowych hello występują błędy kompilacji i odpowiednio je poprawić.</span><span class="sxs-lookup"><span data-stu-id="720ee-246">Check hello output window for any compilation errors and correct them accordingly.</span></span> <span data-ttu-id="720ee-247">Jeśli kompiluje kod hello, hello kodu powinny teraz być sprawdzenie dzienniki magazynu kluczy hello co minutę i wypychanie żadnych nowych zdarzeń na powitania zdefiniowano kolejki usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="720ee-247">If hello code compiles, then hello code should now be checking hello key vault logs every minute and pushing any new events onto hello defined Service Bus queue.</span></span> <span data-ttu-id="720ee-248">Informacje o rejestrowaniu zapisać okno Dziennik toohello każdym wyzwoleniu hello funkcja powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="720ee-248">You should see logging information write out toohello log window every time hello function is triggered.</span></span>

### <a name="azure-logic-app"></a><span data-ttu-id="720ee-249">Aplikacja logiki platformy Azure</span><span class="sxs-lookup"><span data-stu-id="720ee-249">Azure logic app</span></span>
<span data-ttu-id="720ee-250">Następnie należy utworzyć aplikację logiki platformy Azure, która przejmuje hello zdarzeń czy funkcja hello wypycha toohello kolejki usługi Service Bus, analizuje hello zawartości i wysyła wiadomość e-mail na podstawie warunku filtrowanego.</span><span class="sxs-lookup"><span data-stu-id="720ee-250">Next you must create an Azure logic app that picks up hello events that hello function is pushing toohello Service Bus queue, parses hello content, and sends an email based on a condition being matched.</span></span>

<span data-ttu-id="720ee-251">[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md) przechodząc zbyt**nowy > aplikacji logiki**.</span><span class="sxs-lookup"><span data-stu-id="720ee-251">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) by going too**New > Logic App**.</span></span>

<span data-ttu-id="720ee-252">Po utworzeniu aplikacji logiki hello Przejdź tooit i wybierz polecenie **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="720ee-252">Once hello logic app is created, navigate tooit and choose **edit**.</span></span> <span data-ttu-id="720ee-253">Edytora hello logikę aplikacji, wybierz **kolejką usługi Service Bus** , a następnie wprowadź tooconnect poświadczeń użytkownika usługi Service Bus go toohello kolejki.</span><span class="sxs-lookup"><span data-stu-id="720ee-253">Within hello logic app editor, choose **Service Bus Queue** and enter your Service Bus credentials tooconnect it toohello queue.</span></span>

![Magistrala usług aplikacji logiki platformy Azure](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

<span data-ttu-id="720ee-255">Następnie wybierz **Dodaj warunek**.</span><span class="sxs-lookup"><span data-stu-id="720ee-255">Next choose **Add a condition**.</span></span> <span data-ttu-id="720ee-256">W warunku hello Przełącz toohello Zaawansowany edytor i wprowadź powitania po kod, zastępując APP_ID hello rzeczywiste APP_ID aplikacji sieci web:</span><span class="sxs-lookup"><span data-stu-id="720ee-256">In hello condition, switch toohello advanced editor and enter hello following code, replacing APP_ID with hello actual APP_ID of your web app:</span></span>

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

<span data-ttu-id="720ee-257">To wyrażenie zasadniczo zwraca **false** Jeśli hello *appid* z hello zdarzenia przychodzącego (czyli hello treści wiadomości powitania usługi Service Bus) nie jest hello *appid* z hello aplikacja.</span><span class="sxs-lookup"><span data-stu-id="720ee-257">This expression essentially returns **false** if hello *appid* from hello incoming event (which is hello body of hello Service Bus message) is not hello *appid* of hello app.</span></span>

<span data-ttu-id="720ee-258">Teraz utworzymy działania na podstawie **Jeśli nie, nic nie rób**.</span><span class="sxs-lookup"><span data-stu-id="720ee-258">Now, create an action under **If no, do nothing**.</span></span>

![Azure aplikacji logiki, wybierz akcję](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

<span data-ttu-id="720ee-260">Dla akcji hello wybierz **usługi Office 365 — wysyłanie wiadomości e-mail**.</span><span class="sxs-lookup"><span data-stu-id="720ee-260">For hello action, choose **Office 365 - send email**.</span></span> <span data-ttu-id="720ee-261">Wypełnianie toocreate pola hello toosend wiadomości e-mail podczas hello zdefiniowany warunek zwraca **false**.</span><span class="sxs-lookup"><span data-stu-id="720ee-261">Fill out hello fields toocreate an email toosend when hello defined condition returns **false**.</span></span> <span data-ttu-id="720ee-262">Jeśli nie masz usługi Office 365, może wyglądać na alternatyw tooachieve hello takie same wyniki.</span><span class="sxs-lookup"><span data-stu-id="720ee-262">If you do not have Office 365, you could look at alternatives tooachieve hello same results.</span></span>

<span data-ttu-id="720ee-263">W tym momencie masz potok tooend zakończenia, który wyszukuje nowe dzienniki inspekcji magazynu kluczy raz na minutę.</span><span class="sxs-lookup"><span data-stu-id="720ee-263">At this point, you have an end tooend pipeline that looks for new key vault audit logs once a minute.</span></span> <span data-ttu-id="720ee-264">Umieszcza on nowe dzienniki znajdzie tooa kolejką usługi service bus.</span><span class="sxs-lookup"><span data-stu-id="720ee-264">It pushes new logs it finds tooa service bus queue.</span></span> <span data-ttu-id="720ee-265">Aplikacja logiki Hello jest wyzwalane, gdy nowy komunikat znajdzie się w kolejce hello.</span><span class="sxs-lookup"><span data-stu-id="720ee-265">hello logic app is triggered when a new message lands in hello queue.</span></span> <span data-ttu-id="720ee-266">Jeśli hello *appid* w hello zdarzeń nie jest zgodna identyfikator aplikacji hello wywoływania aplikacji hello, wysyła wiadomość e-mail.</span><span class="sxs-lookup"><span data-stu-id="720ee-266">If hello *appid* within hello event does not match hello app ID of hello calling application, it sends an email.</span></span>
