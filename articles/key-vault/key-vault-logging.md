---
title: aaaAzure rejestrowanie Key Vault | Dokumentacja firmy Microsoft
description: "Użyj tego samouczka toohelp Rozpoczynanie pracy z usługą Azure Key Vault rejestrowania."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 43f96a2b-3af8-4adc-9344-bc6041fface8
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 38a173297948748bef45e3d857c06b50b3e21e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-logging"></a><span data-ttu-id="36d15-103">Funkcja rejestrowania usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="36d15-103">Azure Key Vault Logging</span></span>
<span data-ttu-id="36d15-104">Usługa Azure Key Vault jest dostępna w większości regionów.</span><span class="sxs-lookup"><span data-stu-id="36d15-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="36d15-105">Aby uzyskać więcej informacji, zobacz hello [cennik usługi Key Vault](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="36d15-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="36d15-106">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="36d15-106">Introduction</span></span>
<span data-ttu-id="36d15-107">Po utworzeniu co najmniej jednego magazynu kluczy, prawdopodobnie będzie toomonitor, jak i kiedy klucz magazyny są używane i przez kogo.</span><span class="sxs-lookup"><span data-stu-id="36d15-107">After you have created one or more key vaults, you will likely want toomonitor how and when your key vaults are accessed, and by whom.</span></span> <span data-ttu-id="36d15-108">W tym celu możesz włączyć funkcję rejestrowania dla usługi Key Vault, która zapisuje informacje na podanym przez Ciebie koncie magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="36d15-108">You can do this by enabling logging for Key Vault, which saves information in an Azure storage account that you provide.</span></span> <span data-ttu-id="36d15-109">Nowy kontener o nazwie **insights-logs-auditevent** jest tworzony automatycznie dla określonego konta magazynu. Tego samego konta magazynu możesz używać do zbierania dzienników dla wielu magazynów kluczy.</span><span class="sxs-lookup"><span data-stu-id="36d15-109">A new container named **insights-logs-auditevent** is automatically created for your specified storage account, and you can use this same storage account for collecting logs for multiple key vaults.</span></span>

<span data-ttu-id="36d15-110">Możesz uzyskać co najwyżej dostęp do informacji rejestrowania, 10 minut po klucz hello wykonanej operacji magazynu.</span><span class="sxs-lookup"><span data-stu-id="36d15-110">You can access your logging information at most, 10 minutes after hello key vault operation.</span></span> <span data-ttu-id="36d15-111">W większości przypadków czas będzie krótszy.</span><span class="sxs-lookup"><span data-stu-id="36d15-111">In most cases, it will be quicker than this.</span></span>  <span data-ttu-id="36d15-112">Jest tooyou toomanage dzienniki na koncie magazynu:</span><span class="sxs-lookup"><span data-stu-id="36d15-112">It's up tooyou toomanage your logs in your storage account:</span></span>

* <span data-ttu-id="36d15-113">Użyj toosecure metod kontroli dostępu na platformie Azure standardowe dzienniki przez ograniczenie, kto ma dostęp do nich.</span><span class="sxs-lookup"><span data-stu-id="36d15-113">Use standard Azure access control methods toosecure your logs by restricting who can access them.</span></span>
* <span data-ttu-id="36d15-114">Usuń dzienniki nie są już potrzebne tookeep na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="36d15-114">Delete logs that you no longer want tookeep in your storage account.</span></span>

<span data-ttu-id="36d15-115">Użyj tego samouczka toohelp Rozpoczynanie pracy z usługą Azure Key Vault rejestrowanie toocreate Twojego konta magazynu, włączanie rejestrowania i zinterpretować zebrane informacje rejestrowania hello.</span><span class="sxs-lookup"><span data-stu-id="36d15-115">Use this tutorial toohelp you get started with Azure Key Vault logging, toocreate your storage account, enable logging, and interpret hello logging information collected.</span></span>  

> [!NOTE]
> <span data-ttu-id="36d15-116">Ten samouczek nie zawiera instrukcje dotyczące sposobu toocreate klucza magazynów kluczy i kluczy tajnych.</span><span class="sxs-lookup"><span data-stu-id="36d15-116">This tutorial does not include instructions for how toocreate key vaults, keys, or secrets.</span></span> <span data-ttu-id="36d15-117">Te informacje można znaleźć w temacie [Rozpoczynanie pracy z usługą Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="36d15-117">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="36d15-118">Instrukcje dotyczące wieloplatformowego interfejsu wiersza polecenia znajdują się w [tym równoważnym samouczku](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="36d15-118">Or, for Cross-Platform Command-Line Interface instructions, see [this equivalent tutorial](key-vault-manage-with-cli2.md).</span></span>
>
> <span data-ttu-id="36d15-119">Obecnie nie można skonfigurować usługi Azure Key Vault w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="36d15-119">Currently, you cannot configure Azure Key Vault in hello Azure portal.</span></span> <span data-ttu-id="36d15-120">Zamiast tego użyj tych instrukcji usługi Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="36d15-120">Instead, use these Azure PowerShell instructions.</span></span>
>
>

<span data-ttu-id="36d15-121">Aby uzyskać ogólne informacje na temat usługi Azure Key Vault, zobacz [Co to jest usługa Azure Key Vault?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="36d15-121">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36d15-122">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="36d15-122">Prerequisites</span></span>
<span data-ttu-id="36d15-123">toocomplete tego samouczka, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="36d15-123">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="36d15-124">Istniejący magazyn kluczy, który był przez Ciebie używany.</span><span class="sxs-lookup"><span data-stu-id="36d15-124">An existing key vault that you have been using.</span></span>  
* <span data-ttu-id="36d15-125">Usługa Azure PowerShell w **minimalnej wersji 1.0.1**.</span><span class="sxs-lookup"><span data-stu-id="36d15-125">Azure PowerShell, **minimum version of 1.0.1**.</span></span> <span data-ttu-id="36d15-126">tooinstall programu Azure PowerShell i skojarzyć go z subskrypcją platformy Azure, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="36d15-126">tooinstall Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="36d15-127">Jeśli jest już zainstalowany program Azure PowerShell, a nie znasz wersji hello z konsoli programu Azure PowerShell hello, wpisz `(Get-Module azure -ListAvailable).Version`.</span><span class="sxs-lookup"><span data-stu-id="36d15-127">If you have already installed Azure PowerShell and do not know hello version, from hello Azure PowerShell console, type `(Get-Module azure -ListAvailable).Version`.</span></span>  
* <span data-ttu-id="36d15-128">Wystarczająca ilość miejsca w magazynie platformy Azure dla dzienników usługi Key Vault.</span><span class="sxs-lookup"><span data-stu-id="36d15-128">Sufficient storage on Azure for your Key Vault logs.</span></span>

## <span data-ttu-id="36d15-129"><a id="connect"></a>Połącz tooyour subskrypcji</span><span class="sxs-lookup"><span data-stu-id="36d15-129"><a id="connect"></a>Connect tooyour subscriptions</span></span>
<span data-ttu-id="36d15-130">Uruchom sesję programu PowerShell Azure i zaloguj się tooyour konto platformy Azure za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="36d15-130">Start an Azure PowerShell session and sign in tooyour Azure account with hello following command:</span></span>  

    Login-AzureRmAccount

<span data-ttu-id="36d15-131">W oknie wyskakującym przeglądarki hello wprowadź nazwę użytkownika konta platformy Azure i hasło.</span><span class="sxs-lookup"><span data-stu-id="36d15-131">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="36d15-132">Azure PowerShell pobierze wszystkie subskrypcje hello, które są skojarzone z tym kontem i domyślnie, używa hello pierwsza z nich.</span><span class="sxs-lookup"><span data-stu-id="36d15-132">Azure PowerShell will get all hello subscriptions that are associated with this account and by default, uses hello first one.</span></span>

<span data-ttu-id="36d15-133">Jeśli masz wiele subskrypcji może być toospecify konkretne konto, które były używane toocreate magazyn kluczy Azure.</span><span class="sxs-lookup"><span data-stu-id="36d15-133">If you have multiple subscriptions, you might have toospecify a specific one that was used toocreate your Azure Key Vault.</span></span> <span data-ttu-id="36d15-134">Wpisz powitania po toosee hello subskrypcje dla swojego konta:</span><span class="sxs-lookup"><span data-stu-id="36d15-134">Type hello following toosee hello subscriptions for your account:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="36d15-135">Następnie toospecify hello subskrypcję skojarzoną z Twoim magazynem kluczy, który będziesz rejestrować, wpisz:</span><span class="sxs-lookup"><span data-stu-id="36d15-135">Then, toospecify hello subscription that's associated with your key vault you will be logging, type:</span></span>

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> <span data-ttu-id="36d15-136">To jest ważny krok, szczególnie przydatny, jeśli masz wiele subskrypcji skojarzonych z Twoim kontem.</span><span class="sxs-lookup"><span data-stu-id="36d15-136">This is an important step and especially helpful if you have multiple subscriptions associated with your account.</span></span> <span data-ttu-id="36d15-137">Jeśli ten krok zostanie pominięty, może zostać wyświetlony błąd tooregister elemencie Microsoft.Insights.</span><span class="sxs-lookup"><span data-stu-id="36d15-137">You may receive an error tooregister Microsoft.Insights if this step is skipped.</span></span>
>   
>

<span data-ttu-id="36d15-138">Aby uzyskać więcej informacji na temat konfigurowania programu Azure PowerShell, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="36d15-138">For more information about configuring Azure PowerShell, see  [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="36d15-139"><a id="storage"></a>Tworzenie nowego konta magazynu dla dzienników</span><span class="sxs-lookup"><span data-stu-id="36d15-139"><a id="storage"></a>Create a new storage account for your logs</span></span>
<span data-ttu-id="36d15-140">Mimo że można użyć istniejącego konta magazynu dla dzienników, utworzymy nowe konto magazynu, który ma być dedykowane tooKey dzienniki magazynu.</span><span class="sxs-lookup"><span data-stu-id="36d15-140">Although you can use an existing storage account for your logs, we'll create a new storage account that will be dedicated tooKey Vault logs.</span></span> <span data-ttu-id="36d15-141">Dla wygody gdy mamy toospecify to później, szczegóły hello będzie są przechowywane w zmiennej o nazwie **sa**.</span><span class="sxs-lookup"><span data-stu-id="36d15-141">For convenience for when we have toospecify this later, we'll store hello details into a variable named **sa**.</span></span>

<span data-ttu-id="36d15-142">W celu ułatwienia zarządzania użyjemy hello tej samej grupie zasobów, jak Witaj, który zawiera nasz magazyn kluczy.</span><span class="sxs-lookup"><span data-stu-id="36d15-142">For additional ease of management, we'll also use hello same resource group as hello one that contains our key vault.</span></span> <span data-ttu-id="36d15-143">Z hello [Wprowadzenie — samouczek](key-vault-get-started.md), nosi nazwę tej grupy zasobów **ContosoResourceGroup** będziemy lokalizacji Azja Wschodnia hello toouse.</span><span class="sxs-lookup"><span data-stu-id="36d15-143">From hello [getting started tutorial](key-vault-get-started.md), this resource group is named **ContosoResourceGroup** and we'll continue toouse hello East Asia location.</span></span> <span data-ttu-id="36d15-144">Zastąp te wartości własnymi, w razie potrzeby:</span><span class="sxs-lookup"><span data-stu-id="36d15-144">Substitute these values for your own, as applicable:</span></span>

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> <span data-ttu-id="36d15-145">Jeśli zdecydujesz się toouse istniejącego konta magazynu, należy użyć hello tej samej subskrypcji, jako magazynu kluczy i użyj modelu wdrażania usługi Resource Manager hello zamiast hello klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="36d15-145">If you decide toouse an existing storage account, it must use hello same subscription as your key vault and it must use hello Resource Manager deployment model, rather than hello Classic deployment model.</span></span>
>
>

## <span data-ttu-id="36d15-146"><a id="identify"></a>Zidentyfikuj hello magazynu kluczy dla dzienników</span><span class="sxs-lookup"><span data-stu-id="36d15-146"><a id="identify"></a>Identify hello key vault for your logs</span></span>
<span data-ttu-id="36d15-147">W naszym samouczku naszych magazyn kluczy został **ContosoKeyVault**, dlatego dalej będziemy toouse nazwy i przechowuj szczegóły hello do zmiennej o nazwie **kv**:</span><span class="sxs-lookup"><span data-stu-id="36d15-147">In our getting started tutorial, our key vault name was **ContosoKeyVault**, so we'll continue toouse that name and store hello details into a variable named **kv**:</span></span>

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <span data-ttu-id="36d15-148"><a id="enable"></a>Włączanie rejestrowania</span><span class="sxs-lookup"><span data-stu-id="36d15-148"><a id="enable"></a>Enable logging</span></span>
<span data-ttu-id="36d15-149">tooenable rejestrowanie dla usługi Key Vault użyjemy polecenia cmdlet Set-AzureRmDiagnosticSetting hello, wraz z zmienne hello utworzyliśmy dla naszego nowego konta magazynu i magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="36d15-149">tooenable logging for Key Vault, we'll use hello Set-AzureRmDiagnosticSetting cmdlet, together with hello variables we created for our new storage account and our key vault.</span></span> <span data-ttu-id="36d15-150">Zaplanujemy też hello **-włączone** Flaga zbyt**$true** i tooAuditEvent kategorii hello (hello jedyna kategoria rejestrowania usługi Key Vault), ustaw:</span><span class="sxs-lookup"><span data-stu-id="36d15-150">We'll also set hello **-Enabled** flag too**$true** and set hello category tooAuditEvent (hello only category for Key Vault logging), :</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

<span data-ttu-id="36d15-151">Witaj dane wyjściowe obejmują:</span><span class="sxs-lookup"><span data-stu-id="36d15-151">hello output for this includes:</span></span>

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


<span data-ttu-id="36d15-152">Potwierdza to, że włączono rejestrowanie dla magazynu kluczy i zapisywania konta magazynu tooyour informacji.</span><span class="sxs-lookup"><span data-stu-id="36d15-152">This confirms that logging is now enabled for your key vault, saving information tooyour storage account.</span></span>

<span data-ttu-id="36d15-153">Opcjonalnie można także ustawić zasady przechowywania dla dzienników tak, aby starsze dzienniki były automatycznie usuwane.</span><span class="sxs-lookup"><span data-stu-id="36d15-153">Optionally you can also set retention policy for your logs such that older logs will be automatically deleted.</span></span> <span data-ttu-id="36d15-154">Na przykład ustawić zasady przechowywania, używając **- RetentionEnabled** Flaga zbyt**$true** i ustaw **- RetentionInDays** parametru zbyt**90** tak czy zostaną automatycznie usunięte dzienniki starsze niż 90 dni.</span><span class="sxs-lookup"><span data-stu-id="36d15-154">For example, set retention policy using **-RetentionEnabled** flag too**$true** and set **-RetentionInDays** parameter too**90** so that logs older than 90 days will be automatically deleted.</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

<span data-ttu-id="36d15-155">Co jest rejestrowane:</span><span class="sxs-lookup"><span data-stu-id="36d15-155">What's logged:</span></span>

* <span data-ttu-id="36d15-156">Wszystkie uwierzytelnione żądania interfejsu API REST są rejestrowane, w tym żądania zakończone niepowodzeniem z powodu uprawnień dostępu, błędów systemu lub błędów w żądaniach.</span><span class="sxs-lookup"><span data-stu-id="36d15-156">All authenticated REST API requests are logged, which includes failed requests as a result of access permissions, system errors or bad requests.</span></span>
* <span data-ttu-id="36d15-157">Operacje na powitania klucza magazynu siebie, łącznie z tworzeniem, usuwaniem, ustawiania zasad dostępu do magazynu kluczy, i aktualizowaniem atrybutów magazynu kluczy, takich jak tagi.</span><span class="sxs-lookup"><span data-stu-id="36d15-157">Operations on hello key vault itself, which includes creation, deletion, setting key vault access policies, and updating key vault attributes such as tags.</span></span>
* <span data-ttu-id="36d15-158">Operacje na kluczach i kluczach tajnych w magazynie kluczy hello, w tym tworzenie, modyfikowanie lub usuwanie tych kluczy lub kluczy tajnych; operacje, takie jak podpisywanie, sprawdź, szyfrowania, odszyfrowywania, zawijać i odpakowywanie kluczy, pobieranie kluczy tajnych, listy kluczy i kluczy tajnych i ich wersje.</span><span class="sxs-lookup"><span data-stu-id="36d15-158">Operations on keys and secrets in hello key vault, which includes creating, modifying, or deleting these keys or secrets; operations such as sign, verify, encrypt, decrypt, wrap and unwrap keys, get secrets, list keys and secrets and their versions.</span></span>
* <span data-ttu-id="36d15-159">Nieuwierzytelnione żądania, które powodują uzyskanie odpowiedzi 401.</span><span class="sxs-lookup"><span data-stu-id="36d15-159">Unauthenticated requests that result in a 401 response.</span></span> <span data-ttu-id="36d15-160">Na przykład żądania, które nie mają tokenu elementu nośnego, są nieprawidłowo sformułowane, wygasły lub mają nieprawidłowy token.</span><span class="sxs-lookup"><span data-stu-id="36d15-160">For example, requests that do not have a bearer token, or are malformed or expired, or have an invalid token.</span></span>  

## <span data-ttu-id="36d15-161"><a id="access"></a>Uzyskiwanie dostępu do dzienników</span><span class="sxs-lookup"><span data-stu-id="36d15-161"><a id="access"></a>Access your logs</span></span>
<span data-ttu-id="36d15-162">Dzienniki magazynu kluczy są przechowywane w hello **insights-logs-auditevent** kontenera na koncie magazynu hello podane.</span><span class="sxs-lookup"><span data-stu-id="36d15-162">Key vault logs are stored in hello **insights-logs-auditevent** container in hello storage account you provided.</span></span> <span data-ttu-id="36d15-163">toolist wszystkie hello obiekty BLOB w tym kontenerze, wpisz:</span><span class="sxs-lookup"><span data-stu-id="36d15-163">toolist all hello blobs in this container, type:</span></span>

<span data-ttu-id="36d15-164">Najpierw Utwórz zmienną hello nazwa kontenera.</span><span class="sxs-lookup"><span data-stu-id="36d15-164">First, create a variable for hello container name.</span></span> <span data-ttu-id="36d15-165">Będą to używane w hello reszty hello krokach związanych z.</span><span class="sxs-lookup"><span data-stu-id="36d15-165">This will be used throughout hello rest of hello walk through.</span></span>

    $container = 'insights-logs-auditevent'

<span data-ttu-id="36d15-166">toolist wszystkie hello obiekty BLOB w tym kontenerze, wpisz:</span><span class="sxs-lookup"><span data-stu-id="36d15-166">toolist all hello blobs in this container, type:</span></span>

    Get-AzureStorageBlob -Container $container -Context $sa.Context
<span data-ttu-id="36d15-167">Hello dane wyjściowe będą wyglądać coś podobnego toothis:</span><span class="sxs-lookup"><span data-stu-id="36d15-167">hello output will look something similar toothis:</span></span>

<span data-ttu-id="36d15-168">**Identyfikator URI kontenera: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span><span class="sxs-lookup"><span data-stu-id="36d15-168">**Container Uri: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span></span>

<span data-ttu-id="36d15-169">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="36d15-169">**Name**</span></span>

- - -
<span data-ttu-id="36d15-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="36d15-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span></span>

<span data-ttu-id="36d15-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="36d15-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span></span>

<span data-ttu-id="36d15-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span><span class="sxs-lookup"><span data-stu-id="36d15-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span></span>

<span data-ttu-id="36d15-173">Jak widać w przedstawionych danych wyjściowych, obiekty BLOB hello zgodne z konwencją nazewnictwa: **resourceId =<ARM resource ID>/y =<year>/m =<month>/d =<day of month>/h =<hour>/m =<minute>/filename.json**</span><span class="sxs-lookup"><span data-stu-id="36d15-173">As you can see from this output, hello blobs follow a naming convention: **resourceId=<ARM resource ID>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json**</span></span>

<span data-ttu-id="36d15-174">Witaj wartości daty i godziny używają czasu UTC.</span><span class="sxs-lookup"><span data-stu-id="36d15-174">hello date and time values use UTC.</span></span>

<span data-ttu-id="36d15-175">Ponieważ hello tego samego konta magazynu mogą być używane toocollect dzienników dla wielu zasobów, hello pełny identyfikator zasobu w nazwie obiektu blob hello jest bardzo przydatne tooaccess lub obiekty BLOB hello tylko pobierania, które należy.</span><span class="sxs-lookup"><span data-stu-id="36d15-175">Because hello same storage account can be used toocollect logs for multiple resources, hello full resource ID in hello blob name is very useful tooaccess or download just hello blobs that you need.</span></span> <span data-ttu-id="36d15-176">Jednak zanim do tego, firma Microsoft, najpierw zostanie omówiony sposób toodownload hello wszystkie obiekty BLOB.</span><span class="sxs-lookup"><span data-stu-id="36d15-176">But before we do that, we'll first cover how toodownload all hello blobs.</span></span>

<span data-ttu-id="36d15-177">Najpierw utwórz hello toodownload folderu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="36d15-177">First, create a folder toodownload hello blobs.</span></span> <span data-ttu-id="36d15-178">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="36d15-178">For example:</span></span>

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

<span data-ttu-id="36d15-179">Następnie uzyskaj listę wszystkich obiektów blob:</span><span class="sxs-lookup"><span data-stu-id="36d15-179">Then get a list of all blobs:</span></span>  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

<span data-ttu-id="36d15-180">Przekaż w potoku tej listy za pośrednictwem obiektów blob hello toodownload "Get-AzureStorageBlobContent" do folderu docelowego:</span><span class="sxs-lookup"><span data-stu-id="36d15-180">Pipe this list through 'Get-AzureStorageBlobContent' toodownload hello blobs into our destination folder:</span></span>

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

<span data-ttu-id="36d15-181">Po uruchomieniu tego drugiego polecenia hello  **/**  ogranicznik w nazwach obiektów blob hello Utwórz pełną strukturę folderów w folderze docelowym hello, a ta struktura będzie używana toodownload i zapisać hello obiekty BLOB jako plików.</span><span class="sxs-lookup"><span data-stu-id="36d15-181">When you run this second command, hello **/** delimiter in hello blob names create a full folder structure under hello destination folder, and this structure will be used toodownload and store hello blobs as files.</span></span>

<span data-ttu-id="36d15-182">tooselectively pobierać obiekty BLOB, użyj symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="36d15-182">tooselectively download blobs, use wildcards.</span></span> <span data-ttu-id="36d15-183">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="36d15-183">For example:</span></span>

* <span data-ttu-id="36d15-184">Jeśli masz wiele magazynów kluczy i chcesz toodownload dzienniki dla tylko jednego magazynu kluczy o nazwie CONTOSOKEYVAULT3:</span><span class="sxs-lookup"><span data-stu-id="36d15-184">If you have multiple key vaults and want toodownload logs for just one key vault, named CONTOSOKEYVAULT3:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* <span data-ttu-id="36d15-185">Jeśli masz wiele grup zasobów i chcesz toodownload dzienniki dla tylko jednej grupy zasobów, użyj `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span><span class="sxs-lookup"><span data-stu-id="36d15-185">If you have multiple resource groups and want toodownload logs for just one resource group, use `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* <span data-ttu-id="36d15-186">Jeśli chcesz toodownload wszystkie dzienniki hello hello miesiącu stycznia 2016, użyj `-Blob '*/year=2016/m=01/*'`:</span><span class="sxs-lookup"><span data-stu-id="36d15-186">If you want toodownload all hello logs for hello month of January 2016, use `-Blob '*/year=2016/m=01/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

<span data-ttu-id="36d15-187">Wszystko jest teraz gotowy toostart wyszukiwanie informacji zawartych w hello dzienników.</span><span class="sxs-lookup"><span data-stu-id="36d15-187">You're now ready toostart looking at what's in hello logs.</span></span> <span data-ttu-id="36d15-188">Jednak zanim który dwoma parametrami polecenia Get-AzureRmDiagnosticSetting trzeba tooknow:</span><span class="sxs-lookup"><span data-stu-id="36d15-188">But before moving onto that, two more parameters for Get-AzureRmDiagnosticSetting that you might need tooknow:</span></span>

* <span data-ttu-id="36d15-189">tooquery hello stan ustawień diagnostycznych dla zasobu magazynu kluczy:`Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span><span class="sxs-lookup"><span data-stu-id="36d15-189">tooquery hello  status of diagnostic settings for your key vault resource: `Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span></span>
* <span data-ttu-id="36d15-190">Rejestrowanie toodisable dla zasobu magazynu kluczy:`Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span><span class="sxs-lookup"><span data-stu-id="36d15-190">toodisable logging for your key vault resource: `Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span></span>

## <span data-ttu-id="36d15-191"><a id="interpret"></a>Interpretowanie dzienników usługi Key Vault</span><span class="sxs-lookup"><span data-stu-id="36d15-191"><a id="interpret"></a>Interpret your Key Vault logs</span></span>
<span data-ttu-id="36d15-192">Poszczególne obiekty blob są przechowywane jako tekst w formacie obiektu blob JSON.</span><span class="sxs-lookup"><span data-stu-id="36d15-192">Individual blobs are stored as text, formatted as a JSON blob.</span></span> <span data-ttu-id="36d15-193">To jest przykładowy wpis dziennika po uruchomieniu polecenia `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span><span class="sxs-lookup"><span data-stu-id="36d15-193">This is an example log entry from running `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span></span>

    {
        "records":
        [
            {
                "time": "2016-01-05T01:32:01.2691226Z",
                "resourceId": "/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSOGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT",
                "operationName": "VaultGet",
                "operationVersion": "2015-06-01",
                "category": "AuditEvent",
                "resultType": "Success",
                "resultSignature": "OK",
                "resultDescription": "",
                "durationMs": "78",
                "callerIpAddress": "104.40.82.76",
                "correlationId": "",
                "identity": {"claim":{"http://schemas.microsoft.com/identity/claims/objectidentifier":"d9da5048-2737-4770-bd64-XXXXXXXXXXXX","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn":"live.com#username@outlook.com","appid":"1950a258-227b-4e31-a9cf-XXXXXXXXXXXX"}},
                "properties": {"clientInfo":"azure-resource-manager/2.0","requestUri":"https://control-prod-wus.vaultcore.azure.net/subscriptions/361da5d4-a47a-4c79-afdd-XXXXXXXXXXXX/resourcegroups/contosoresourcegroup/providers/Microsoft.KeyVault/vaults/contosokeyvault?api-version=2015-06-01","id":"https://contosokeyvault.vault.azure.net/","httpStatusCode":200}
            }
        ]
    }


<span data-ttu-id="36d15-194">Witaj poniższej tabeli wymieniono nazwy pól hello wraz z opisami.</span><span class="sxs-lookup"><span data-stu-id="36d15-194">hello following table lists hello field names and descriptions.</span></span>

| <span data-ttu-id="36d15-195">Nazwa pola</span><span class="sxs-lookup"><span data-stu-id="36d15-195">Field name</span></span> | <span data-ttu-id="36d15-196">Opis</span><span class="sxs-lookup"><span data-stu-id="36d15-196">Description</span></span> |
| --- | --- |
| <span data-ttu-id="36d15-197">time</span><span class="sxs-lookup"><span data-stu-id="36d15-197">time</span></span> |<span data-ttu-id="36d15-198">Data i godzina (UTC).</span><span class="sxs-lookup"><span data-stu-id="36d15-198">Date and time (UTC).</span></span> |
| <span data-ttu-id="36d15-199">resourceId</span><span class="sxs-lookup"><span data-stu-id="36d15-199">resourceId</span></span> |<span data-ttu-id="36d15-200">Identyfikator zasobu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="36d15-200">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="36d15-201">W przypadku dzienników usługi Key Vault jest zawsze identyfikator zasobu usługi Key Vault hello</span><span class="sxs-lookup"><span data-stu-id="36d15-201">For Key Vault logs, this is always hello  Key Vault resource ID.</span></span> |
| <span data-ttu-id="36d15-202">operationName</span><span class="sxs-lookup"><span data-stu-id="36d15-202">operationName</span></span> |<span data-ttu-id="36d15-203">Nazwa operacji hello, zgodnie z opisem w następnej tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="36d15-203">Name of hello operation, as documented in hello next table.</span></span> |
| <span data-ttu-id="36d15-204">operationVersion</span><span class="sxs-lookup"><span data-stu-id="36d15-204">operationVersion</span></span> |<span data-ttu-id="36d15-205">To jest wersja interfejsu API REST hello zażądał powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="36d15-205">This is hello REST API version requested by hello client.</span></span> |
| <span data-ttu-id="36d15-206">category</span><span class="sxs-lookup"><span data-stu-id="36d15-206">category</span></span> |<span data-ttu-id="36d15-207">W przypadku dzienników usługi Key Vault kategoria AuditEvent jest hello jedyną dostępną wartością.</span><span class="sxs-lookup"><span data-stu-id="36d15-207">For Key Vault logs, AuditEvent is hello single, available value.</span></span> |
| <span data-ttu-id="36d15-208">resultType</span><span class="sxs-lookup"><span data-stu-id="36d15-208">resultType</span></span> |<span data-ttu-id="36d15-209">Wynik żądania interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="36d15-209">Result of REST API request.</span></span> |
| <span data-ttu-id="36d15-210">resultSignature</span><span class="sxs-lookup"><span data-stu-id="36d15-210">resultSignature</span></span> |<span data-ttu-id="36d15-211">Stan HTTP.</span><span class="sxs-lookup"><span data-stu-id="36d15-211">HTTP status.</span></span> |
| <span data-ttu-id="36d15-212">resultDescription</span><span class="sxs-lookup"><span data-stu-id="36d15-212">resultDescription</span></span> |<span data-ttu-id="36d15-213">Dodatkowy opis wyniku hello, jeśli jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="36d15-213">Additional description about hello result, when available.</span></span> |
| <span data-ttu-id="36d15-214">durationMs</span><span class="sxs-lookup"><span data-stu-id="36d15-214">durationMs</span></span> |<span data-ttu-id="36d15-215">Czas trwania żądania interfejsu API REST hello tooservice, w milisekundach.</span><span class="sxs-lookup"><span data-stu-id="36d15-215">Time it took tooservice hello REST API request, in milliseconds.</span></span> <span data-ttu-id="36d15-216">Nie obejmuje opóźnienia sieci hello, więc czas zmierzony po stronie klienta hello hello mogą być niezgodne z tym razem.</span><span class="sxs-lookup"><span data-stu-id="36d15-216">This does not include hello network latency, so hello time you measure on hello client side might not match this time.</span></span> |
| <span data-ttu-id="36d15-217">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="36d15-217">callerIpAddress</span></span> |<span data-ttu-id="36d15-218">Adres IP powitania klienta, który wysłał żądanie hello.</span><span class="sxs-lookup"><span data-stu-id="36d15-218">IP address of hello client who made hello request.</span></span> |
| <span data-ttu-id="36d15-219">correlationId</span><span class="sxs-lookup"><span data-stu-id="36d15-219">correlationId</span></span> |<span data-ttu-id="36d15-220">Opcjonalny identyfikator GUID hello klienta można przekazać toocorrelate dzienników po stronie klienta z dziennikami po stronie usługi (Key Vault).</span><span class="sxs-lookup"><span data-stu-id="36d15-220">An optional GUID that hello client can pass toocorrelate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="36d15-221">identity</span><span class="sxs-lookup"><span data-stu-id="36d15-221">identity</span></span> |<span data-ttu-id="36d15-222">Tożsamość z tokenu hello, który został przedstawiony podczas przesyłania żądania interfejsu API REST hello.</span><span class="sxs-lookup"><span data-stu-id="36d15-222">Identity from hello token that was presented when making hello REST API request.</span></span> <span data-ttu-id="36d15-223">Jest to zazwyczaj „użytkownik”, „główna nazwa usługi” lub kombinacja „użytkownik+identyfikator appId”, jak w przypadku żądania wynikającego z polecenia cmdlet usługi Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="36d15-223">This is usually a "user", a "service principal" or a combination "user+appId" as in case of a request resulting from a Azure PowerShell cmdlet.</span></span> |
| <span data-ttu-id="36d15-224">properties</span><span class="sxs-lookup"><span data-stu-id="36d15-224">properties</span></span> |<span data-ttu-id="36d15-225">To pole zawiera różne informacje oparte na powitania operacji (operationName).</span><span class="sxs-lookup"><span data-stu-id="36d15-225">This field will contain different information based on hello operation (operationName).</span></span> <span data-ttu-id="36d15-226">W większości przypadków zawiera informacje o kliencie (hello ciąg agenta użytkownika przekazany przez powitania klienta), hello dokładny identyfikator URI żądania interfejsu API REST i kod stanu HTTP.</span><span class="sxs-lookup"><span data-stu-id="36d15-226">In most cases, contains client information (hello useragent string passed by hello client), hello exact REST API request URI, and HTTP status code.</span></span> <span data-ttu-id="36d15-227">Ponadto gdy obiekt jest zwracany w wyniku żądania (na przykład KeyCreate lub VaultGet) będzie również zawierać hello identyfikator URI klucza (jako "id"), identyfikator URI magazynu lub identyfikator URI klucza tajnego.</span><span class="sxs-lookup"><span data-stu-id="36d15-227">In addition, when an object is returned as a result of a request (for example, KeyCreate or VaultGet) it will also contain hello Key URI (as "id"), Vault URI, or Secret URI.</span></span> |

<span data-ttu-id="36d15-228">Witaj **operationName** wartości pól są w formacie ObjectVerb.</span><span class="sxs-lookup"><span data-stu-id="36d15-228">hello **operationName** field values are in ObjectVerb format.</span></span> <span data-ttu-id="36d15-229">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="36d15-229">For example:</span></span>

* <span data-ttu-id="36d15-230">Wszystkie operacje magazynu kluczy mają hello "magazynu`<action>`" formatu, takiego jak `VaultGet` i `VaultCreate`.</span><span class="sxs-lookup"><span data-stu-id="36d15-230">All key vault operations have hello 'Vault`<action>`' format, such as `VaultGet` and `VaultCreate`.</span></span>
* <span data-ttu-id="36d15-231">Wszystkie operacje kluczy mają hello "klucz`<action>`" formatu, takiego jak `KeySign` i `KeyList`.</span><span class="sxs-lookup"><span data-stu-id="36d15-231">All  key operations have hello 'Key`<action>`' format, such as `KeySign` and `KeyList`.</span></span>
* <span data-ttu-id="36d15-232">Wszystkie operacje kluczy tajnych mają hello "klucz tajny`<action>`" formatu, takiego jak `SecretGet` i `SecretListVersions`.</span><span class="sxs-lookup"><span data-stu-id="36d15-232">All secret operations have hello 'Secret`<action>`' format, such as `SecretGet` and `SecretListVersions`.</span></span>

<span data-ttu-id="36d15-233">Witaj w poniższej tabeli wymieniono hello operationName i odpowiadające jej polecenie interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="36d15-233">hello following table lists hello operationName and corresponding REST API command.</span></span>

| <span data-ttu-id="36d15-234">operationName</span><span class="sxs-lookup"><span data-stu-id="36d15-234">operationName</span></span> | <span data-ttu-id="36d15-235">Polecenie interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="36d15-235">REST API Command</span></span> |
| --- | --- |
| <span data-ttu-id="36d15-236">Authentication</span><span class="sxs-lookup"><span data-stu-id="36d15-236">Authentication</span></span> |<span data-ttu-id="36d15-237">Za pośrednictwem punktu końcowego usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="36d15-237">Via Azure Active Directory endpoint</span></span> |
| <span data-ttu-id="36d15-238">VaultGet</span><span class="sxs-lookup"><span data-stu-id="36d15-238">VaultGet</span></span> |[<span data-ttu-id="36d15-239">Pobierz informacje o magazynie kluczy</span><span class="sxs-lookup"><span data-stu-id="36d15-239">Get information about a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| <span data-ttu-id="36d15-240">VaultPut</span><span class="sxs-lookup"><span data-stu-id="36d15-240">VaultPut</span></span> |[<span data-ttu-id="36d15-241">Utwórz lub zaktualizuj magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="36d15-241">Create or update a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| <span data-ttu-id="36d15-242">VaultDelete</span><span class="sxs-lookup"><span data-stu-id="36d15-242">VaultDelete</span></span> |[<span data-ttu-id="36d15-243">Usuń magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="36d15-243">Delete a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| <span data-ttu-id="36d15-244">VaultPatch</span><span class="sxs-lookup"><span data-stu-id="36d15-244">VaultPatch</span></span> |[<span data-ttu-id="36d15-245">Zaktualizuj magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="36d15-245">Update a key vault</span></span>](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| <span data-ttu-id="36d15-246">VaultList</span><span class="sxs-lookup"><span data-stu-id="36d15-246">VaultList</span></span> |[<span data-ttu-id="36d15-247">Utwórz listę wszystkich magazynów kluczy w grupie zasobów</span><span class="sxs-lookup"><span data-stu-id="36d15-247">List all key vaults in a resource group</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| <span data-ttu-id="36d15-248">KeyCreate</span><span class="sxs-lookup"><span data-stu-id="36d15-248">KeyCreate</span></span> |[<span data-ttu-id="36d15-249">Utwórz klucz</span><span class="sxs-lookup"><span data-stu-id="36d15-249">Create a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| <span data-ttu-id="36d15-250">KeyGet</span><span class="sxs-lookup"><span data-stu-id="36d15-250">KeyGet</span></span> |[<span data-ttu-id="36d15-251">Pobierz informacje o kluczu</span><span class="sxs-lookup"><span data-stu-id="36d15-251">Get information about a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| <span data-ttu-id="36d15-252">KeyImport</span><span class="sxs-lookup"><span data-stu-id="36d15-252">KeyImport</span></span> |[<span data-ttu-id="36d15-253">Importuj klucz do magazynu</span><span class="sxs-lookup"><span data-stu-id="36d15-253">Import a key into a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| <span data-ttu-id="36d15-254">KeyBackup</span><span class="sxs-lookup"><span data-stu-id="36d15-254">KeyBackup</span></span> |<span data-ttu-id="36d15-255">[Wykonaj kopię zapasową klucza](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span><span class="sxs-lookup"><span data-stu-id="36d15-255">[Backup a key](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span></span> |
| <span data-ttu-id="36d15-256">KeyDelete</span><span class="sxs-lookup"><span data-stu-id="36d15-256">KeyDelete</span></span> |[<span data-ttu-id="36d15-257">Usuń klucz</span><span class="sxs-lookup"><span data-stu-id="36d15-257">Delete a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| <span data-ttu-id="36d15-258">KeyRestore</span><span class="sxs-lookup"><span data-stu-id="36d15-258">KeyRestore</span></span> |[<span data-ttu-id="36d15-259">Przywróć klucz</span><span class="sxs-lookup"><span data-stu-id="36d15-259">Restore a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| <span data-ttu-id="36d15-260">KeySign</span><span class="sxs-lookup"><span data-stu-id="36d15-260">KeySign</span></span> |[<span data-ttu-id="36d15-261">Podpisz przy użyciu klucza</span><span class="sxs-lookup"><span data-stu-id="36d15-261">Sign with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| <span data-ttu-id="36d15-262">KeyVerify</span><span class="sxs-lookup"><span data-stu-id="36d15-262">KeyVerify</span></span> |[<span data-ttu-id="36d15-263">Weryfikuj za pomocą klucza</span><span class="sxs-lookup"><span data-stu-id="36d15-263">Verify with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| <span data-ttu-id="36d15-264">KeyWrap</span><span class="sxs-lookup"><span data-stu-id="36d15-264">KeyWrap</span></span> |[<span data-ttu-id="36d15-265">Opakuj klucz</span><span class="sxs-lookup"><span data-stu-id="36d15-265">Wrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| <span data-ttu-id="36d15-266">KeyUnwrap</span><span class="sxs-lookup"><span data-stu-id="36d15-266">KeyUnwrap</span></span> |[<span data-ttu-id="36d15-267">Odpakuj klucz</span><span class="sxs-lookup"><span data-stu-id="36d15-267">Unwrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| <span data-ttu-id="36d15-268">KeyEncrypt</span><span class="sxs-lookup"><span data-stu-id="36d15-268">KeyEncrypt</span></span> |[<span data-ttu-id="36d15-269">Szyfruj za pomocą klucza</span><span class="sxs-lookup"><span data-stu-id="36d15-269">Encrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| <span data-ttu-id="36d15-270">KeyDecrypt</span><span class="sxs-lookup"><span data-stu-id="36d15-270">KeyDecrypt</span></span> |[<span data-ttu-id="36d15-271">Odszyfruj za pomocą klucza</span><span class="sxs-lookup"><span data-stu-id="36d15-271">Decrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| <span data-ttu-id="36d15-272">KeyUpdate</span><span class="sxs-lookup"><span data-stu-id="36d15-272">KeyUpdate</span></span> |[<span data-ttu-id="36d15-273">Zaktualizuj klucz</span><span class="sxs-lookup"><span data-stu-id="36d15-273">Update a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| <span data-ttu-id="36d15-274">KeyList</span><span class="sxs-lookup"><span data-stu-id="36d15-274">KeyList</span></span> |[<span data-ttu-id="36d15-275">Lista hello kluczy w magazynie</span><span class="sxs-lookup"><span data-stu-id="36d15-275">List hello keys in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| <span data-ttu-id="36d15-276">KeyListVersions</span><span class="sxs-lookup"><span data-stu-id="36d15-276">KeyListVersions</span></span> |[<span data-ttu-id="36d15-277">Utwórz listę wersji klucza hello</span><span class="sxs-lookup"><span data-stu-id="36d15-277">List hello versions of a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| <span data-ttu-id="36d15-278">SecretSet</span><span class="sxs-lookup"><span data-stu-id="36d15-278">SecretSet</span></span> |[<span data-ttu-id="36d15-279">Utwórz klucz tajny</span><span class="sxs-lookup"><span data-stu-id="36d15-279">Create a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| <span data-ttu-id="36d15-280">SecretGet</span><span class="sxs-lookup"><span data-stu-id="36d15-280">SecretGet</span></span> |[<span data-ttu-id="36d15-281">Pobierz klucz tajny</span><span class="sxs-lookup"><span data-stu-id="36d15-281">Get secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| <span data-ttu-id="36d15-282">SecretUpdate</span><span class="sxs-lookup"><span data-stu-id="36d15-282">SecretUpdate</span></span> |[<span data-ttu-id="36d15-283">Zaktualizuj klucz tajny</span><span class="sxs-lookup"><span data-stu-id="36d15-283">Update a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| <span data-ttu-id="36d15-284">SecretDelete</span><span class="sxs-lookup"><span data-stu-id="36d15-284">SecretDelete</span></span> |[<span data-ttu-id="36d15-285">Usuń klucz tajny</span><span class="sxs-lookup"><span data-stu-id="36d15-285">Delete a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| <span data-ttu-id="36d15-286">SecretList</span><span class="sxs-lookup"><span data-stu-id="36d15-286">SecretList</span></span> |[<span data-ttu-id="36d15-287">Utwórz listę kluczy tajnych w magazynie</span><span class="sxs-lookup"><span data-stu-id="36d15-287">List secrets in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| <span data-ttu-id="36d15-288">SecretListVersions</span><span class="sxs-lookup"><span data-stu-id="36d15-288">SecretListVersions</span></span> |[<span data-ttu-id="36d15-289">Utwórz listę wersji klucza tajnego</span><span class="sxs-lookup"><span data-stu-id="36d15-289">List versions of a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <span data-ttu-id="36d15-290"><a id="loganalytics"></a>Korzystanie z usługi Log Analytics</span><span class="sxs-lookup"><span data-stu-id="36d15-290"><a id="loganalytics"></a>Use Log Analytics</span></span>

<span data-ttu-id="36d15-291">Za pomocą rozwiązania Azure Key Vault hello w tooreview analizy dzienników, dzienniki usługi Azure Key Vault AuditEvent.</span><span class="sxs-lookup"><span data-stu-id="36d15-291">You can use hello Azure Key Vault solution in Log Analytics tooreview Azure Key Vault AuditEvent logs.</span></span> <span data-ttu-id="36d15-292">Aby uzyskać więcej informacji, łącznie ze sposobem tooset to, zobacz [rozwiązania magazynu kluczy Azure Log Analytics](../log-analytics/log-analytics-azure-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="36d15-292">For more information, including how tooset this up, see [Azure Key Vault solution in Log Analytics](../log-analytics/log-analytics-azure-key-vault.md).</span></span> <span data-ttu-id="36d15-293">Ten artykuł zawiera również instrukcje, jeśli potrzebujesz toomigrate z hello starego magazynu kluczy rozwiązania udostępniona hello analizy dzienników wersji zapoznawczej, którym najpierw kierowane tooan Twojego dzienniki konta magazynu Azure i skonfigurować tooread analizy dzienników z tego miejsca.</span><span class="sxs-lookup"><span data-stu-id="36d15-293">This article also contains instructions if you need toomigrate from hello old Key Vault solution that was offered during hello Log Analytics preview, where you first routed your logs tooan Azure Storage account and configured Log Analytics tooread from there.</span></span>

## <span data-ttu-id="36d15-294"><a id="next"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="36d15-294"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="36d15-295">Aby zapoznać się z samouczkiem, w którym użyto usługi Azure Key Vault w aplikacji sieci Web, zobacz [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md) (Używanie usługi Azure Key Vault za pośrednictwem aplikacji sieci Web).</span><span class="sxs-lookup"><span data-stu-id="36d15-295">For a tutorial that uses Azure Key Vault in a web application, see [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md).</span></span>

<span data-ttu-id="36d15-296">Odwołania dotyczące programowania, zobacz [hello przewodnik dewelopera usługi Azure Key Vault](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="36d15-296">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

<span data-ttu-id="36d15-297">Aby zapoznać się z listą poleceń cmdlet usługi Azure PowerShell 1.0 dla usługi Azure Key Vault, zobacz artykuł [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault) (Polecenia cmdlet w usłudze Azure Key Vault).</span><span class="sxs-lookup"><span data-stu-id="36d15-297">For a list of Azure PowerShell 1.0 cmdlets for Azure Key Vault, see [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).</span></span>

<span data-ttu-id="36d15-298">Samouczek dotyczący rotacją kluczy i dziennika inspekcji w usłudze Azure Key Vault, zobacz [jak toosetup Key Vault z tooend zakończenia klucza obracanie i inspekcji](key-vault-key-rotation-log-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="36d15-298">For a tutorial on key rotation and log auditing with Azure Key Vault, see [How toosetup Key Vault with end tooend key rotation and auditing](key-vault-key-rotation-log-monitoring.md).</span></span>
