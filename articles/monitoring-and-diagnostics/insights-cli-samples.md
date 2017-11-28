---
title: "Przykłady szybki start aaaAzure Monitor CLI w wersji 1.0. | Microsoft Docs"
description: "Przykładowe polecenia 1.0 interfejsu wiersza polecenia dla funkcji Azure monitora. Azure Monitor jest usługa Microsoft Azure, dzięki czemu można toosend powiadomień o alertach, wywołanie adresu URL sieci web na podstawie wartości danych telemetrycznych skonfigurowany, a automatycznego skalowania usługi w chmurze, maszyn wirtualnych i aplikacji sieci Web."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1653aa81-0ee6-4622-9c65-d4801ed9006f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6cd9cd62b3a1977276563f5e43f5384ccca66247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a><span data-ttu-id="bd453-105">Przykładów dla platformy Azure CLI wieloplatformowych Monitor 1.0 szybki start</span><span class="sxs-lookup"><span data-stu-id="bd453-105">Azure Monitor  Cross-platform CLI 1.0 quick start samples</span></span>
<span data-ttu-id="bd453-106">Ten artykuł przedstawia przykładowe toohelp polecenia interfejsu wiersza polecenia (CLI) możesz uzyskiwać dostęp do funkcji monitorowania Azure.</span><span class="sxs-lookup"><span data-stu-id="bd453-106">This article shows you sample command-line interface (CLI) commands toohelp you access Azure Monitor features.</span></span> <span data-ttu-id="bd453-107">Azure Monitor umożliwia tooAutoScale usługi w chmurze, maszyn wirtualnych i aplikacji sieci Web i toosend powiadomień o alertach lub na podstawie wartości dane telemetryczne skonfigurowanych adresów URL sieci web wywołania.</span><span class="sxs-lookup"><span data-stu-id="bd453-107">Azure Monitor allows you tooAutoScale Cloud Services, Virtual Machines, and Web Apps and toosend alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="bd453-108">Azure Monitor jest nową nazwę hello proponowaną "Azure Insights" do 25 września 2016 r.</span><span class="sxs-lookup"><span data-stu-id="bd453-108">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="bd453-109">Jednak hello przestrzeni nazw, dlatego poniższe polecenia hello nadal zawierać hello "insights".</span><span class="sxs-lookup"><span data-stu-id="bd453-109">However, hello namespaces and thus hello commands below still contain hello "insights".</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="bd453-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bd453-110">Prerequisites</span></span>
<span data-ttu-id="bd453-111">Jeśli nie została jeszcze zainstalowana hello wiersza polecenia platformy Azure, zobacz [hello instalowanie interfejsu wiersza polecenia Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="bd453-111">If you haven't already installed hello Azure CLI, see [Install hello Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="bd453-112">Jeśli masz doświadczenia w pracy z wiersza polecenia platformy Azure, możesz uzyskać więcej informacji o [Użyj hello Azure CLI for Mac, Linux i Windows za pomocą Menedżera zasobów Azure](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="bd453-112">If you're unfamiliar with Azure CLI, you can read more about it at [Use hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span></span>

<span data-ttu-id="bd453-113">W systemie Windows, należy zainstalować npm z hello [witryny sieci Web Node.js](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="bd453-113">In Windows, install npm from hello [Node.js website](https://nodejs.org/).</span></span> <span data-ttu-id="bd453-114">Po ukończeniu instalacji hello przy użyciu CMD.exe z uprawnieniami Uruchom jako Administrator, wykonaj następujące hello z zainstalowanym npm folderu hello:</span><span class="sxs-lookup"><span data-stu-id="bd453-114">After you complete hello installation, using CMD.exe with Run As Administrator privileges, execute hello following from hello folder where npm is installed:</span></span>

```console
npm install azure-cli --global
```

<span data-ttu-id="bd453-115">Następnie przejdź tooany/lokalizacja folderu mają i wpisz w hello wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="bd453-115">Next, navigate tooany folder/location you want and type at hello command-line:</span></span>

```console
azure help
```

## <a name="log-in-tooazure"></a><span data-ttu-id="bd453-116">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="bd453-116">Log in tooAzure</span></span>
<span data-ttu-id="bd453-117">pierwszym krokiem Hello jest tooyour toologin konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bd453-117">hello first step is toologin tooyour Azure account.</span></span>

```console
azure login
```

<span data-ttu-id="bd453-118">Po uruchomieniu tego polecenia, należy mieć toosign w za pomocą instrukcji hello na ekranie powitania.</span><span class="sxs-lookup"><span data-stu-id="bd453-118">After running this command, you have toosign in via hello instructions on hello screen.</span></span> <span data-ttu-id="bd453-119">Później Zobacz Twoje konto, identyfikatora dzierżawcy i domyślnego identyfikatora subskrypcji. Wszystkie polecenia działają w kontekście hello subskrypcji domyślne.</span><span class="sxs-lookup"><span data-stu-id="bd453-119">Afterward, you see your Account, TenantId, and default Subscription Id. All commands work in hello context of your default subscription.</span></span>

<span data-ttu-id="bd453-120">Szczegóły hello toolist Twojej bieżącej subskrypcji hello Użyj następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="bd453-120">toolist hello details of your current subscription, use hello following command.</span></span>

```console
azure account show
```

<span data-ttu-id="bd453-121">toochange pracy kontekstu tooa inną subskrypcję, hello Użyj następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="bd453-121">toochange working context tooa different subscription, use hello following command.</span></span>

```console
azure account set "subscription ID or subscription name"
```

<span data-ttu-id="bd453-122">toouse usługa Azure Resource Manager i Azure Monitor poleceń, należy toobe w trybie Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bd453-122">toouse Azure Resource Manager and Azure Monitor commands, you need toobe in Azure Resource Manager mode.</span></span>

```console
azure config mode arm
```

<span data-ttu-id="bd453-123">tooview listę wszystkich obsługiwanych poleceń Azure Monitor, wykonaj następujące hello.</span><span class="sxs-lookup"><span data-stu-id="bd453-123">tooview a list of all supported Azure Monitor commands, perform hello following.</span></span>

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a><span data-ttu-id="bd453-124">Wyświetl dziennik aktywności dla subskrypcji</span><span class="sxs-lookup"><span data-stu-id="bd453-124">View activity log for a subscription</span></span>
<span data-ttu-id="bd453-125">tooview listę zdarzeń dziennika aktywności, wykonaj następujące hello.</span><span class="sxs-lookup"><span data-stu-id="bd453-125">tooview a list of activity log events, perform hello following.</span></span>

```console
azure insights logs list [options]
```

<span data-ttu-id="bd453-126">Spróbuj powitania po tooview wszystkich dostępnych opcji.</span><span class="sxs-lookup"><span data-stu-id="bd453-126">Try hello following tooview all available options.</span></span>

```console
azure insights logs list -help
```

<span data-ttu-id="bd453-127">Oto przykład toolist dzienniki w grupie zasobów</span><span class="sxs-lookup"><span data-stu-id="bd453-127">Here is an example toolist logs by a resourceGroup</span></span>

```console
azure insights logs list --resourceGroup "myrg1"
```

<span data-ttu-id="bd453-128">Przykład toolist dzienniki przez obiekt wywołujący</span><span class="sxs-lookup"><span data-stu-id="bd453-128">Example toolist logs by caller</span></span>

```console
azure insights logs list --caller "myname@company.com"
```

<span data-ttu-id="bd453-129">Przykład toolist dzienniki przez obiekt wywołujący na typu zasobu w ciągu daty rozpoczęcia i zakończenia</span><span class="sxs-lookup"><span data-stu-id="bd453-129">Example toolist logs by caller on a resource type, within a start and end date</span></span>

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a><span data-ttu-id="bd453-130">Praca z alertami</span><span class="sxs-lookup"><span data-stu-id="bd453-130">Work with alerts</span></span>
<span data-ttu-id="bd453-131">Można użyć hello informacji w hello toowork sekcji z alertami.</span><span class="sxs-lookup"><span data-stu-id="bd453-131">You can use hello information in hello section toowork with alerts.</span></span>

### <a name="get-alert-rules-in-a-resource-group"></a><span data-ttu-id="bd453-132">Pobierz reguły alertów w grupie zasobów</span><span class="sxs-lookup"><span data-stu-id="bd453-132">Get alert rules in a resource group</span></span>
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a><span data-ttu-id="bd453-133">Utwórz metryki regułę alertu</span><span class="sxs-lookup"><span data-stu-id="bd453-133">Create a metric alert rule</span></span>
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a><span data-ttu-id="bd453-134">Utwórz regułę alertu w teście sieci Web</span><span class="sxs-lookup"><span data-stu-id="bd453-134">Create webtest alert rule</span></span>
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a><span data-ttu-id="bd453-135">Usuń regułę alertu</span><span class="sxs-lookup"><span data-stu-id="bd453-135">Delete an alert rule</span></span>
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a><span data-ttu-id="bd453-136">Profile dziennika</span><span class="sxs-lookup"><span data-stu-id="bd453-136">Log profiles</span></span>
<span data-ttu-id="bd453-137">Użyj informacji hello w tej sekcji toowork przy użyciu profilów dziennika.</span><span class="sxs-lookup"><span data-stu-id="bd453-137">Use hello information in this section toowork with log profiles.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="bd453-138">Pobierz profil dziennika</span><span class="sxs-lookup"><span data-stu-id="bd453-138">Get a log profile</span></span>
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a><span data-ttu-id="bd453-139">Dodawanie profilu dziennika bez przechowywania</span><span class="sxs-lookup"><span data-stu-id="bd453-139">Add a log profile without retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="bd453-140">Usuń profil dziennika</span><span class="sxs-lookup"><span data-stu-id="bd453-140">Remove a log profile</span></span>
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a><span data-ttu-id="bd453-141">Dodawanie profilu dziennika z przechowywaniem</span><span class="sxs-lookup"><span data-stu-id="bd453-141">Add a log profile with retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="bd453-142">Dodawanie profilu dziennika z przechowywania i EventHub</span><span class="sxs-lookup"><span data-stu-id="bd453-142">Add a log profile with retention and EventHub</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a><span data-ttu-id="bd453-143">Diagnostyka</span><span class="sxs-lookup"><span data-stu-id="bd453-143">Diagnostics</span></span>
<span data-ttu-id="bd453-144">Użyj informacji hello w tej sekcji toowork z ustawień diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="bd453-144">Use hello information in this section toowork with diagnostic settings.</span></span>

### <a name="get-a-diagnostic-setting"></a><span data-ttu-id="bd453-145">Pobierz ustawienia diagnostyki</span><span class="sxs-lookup"><span data-stu-id="bd453-145">Get a diagnostic setting</span></span>
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a><span data-ttu-id="bd453-146">Wyłącz ustawienie diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="bd453-146">Disable a diagnostic setting</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a><span data-ttu-id="bd453-147">Włącz ustawienie diagnostyczne bez przechowywania</span><span class="sxs-lookup"><span data-stu-id="bd453-147">Enable a diagnostic setting without retention</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a><span data-ttu-id="bd453-148">Automatyczne skalowanie</span><span class="sxs-lookup"><span data-stu-id="bd453-148">Autoscale</span></span>
<span data-ttu-id="bd453-149">Użyj informacji hello w tej sekcji toowork z ustawieniami automatycznego skalowania.</span><span class="sxs-lookup"><span data-stu-id="bd453-149">Use hello information in this section toowork with autoscale settings.</span></span> <span data-ttu-id="bd453-150">Należy toomodify tych przykładów.</span><span class="sxs-lookup"><span data-stu-id="bd453-150">You need toomodify these examples.</span></span>

### <a name="get-autoscale-settings-for-a-resource-group"></a><span data-ttu-id="bd453-151">Pobierz ustawienia skalowania automatycznego dla grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="bd453-151">Get autoscale settings for a resource group</span></span>
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a><span data-ttu-id="bd453-152">Pobierz ustawienia skalowania automatycznego według nazwy w grupie zasobów</span><span class="sxs-lookup"><span data-stu-id="bd453-152">Get autoscale settings by name in a resource group</span></span>
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a><span data-ttu-id="bd453-153">Ustawienia auotoscale</span><span class="sxs-lookup"><span data-stu-id="bd453-153">Set auotoscale settings</span></span>
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
