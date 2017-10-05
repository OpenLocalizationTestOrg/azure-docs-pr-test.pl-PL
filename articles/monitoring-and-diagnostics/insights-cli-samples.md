---
title: "Przykłady szybki start Azure Monitor CLI w wersji 1.0. | Microsoft Docs"
description: "Przykładowe polecenia 1.0 interfejsu wiersza polecenia dla funkcji Azure monitora. Azure Monitor jest usługą Microsoft Azure, co pozwala na wysyłanie powiadomień o alertach, wywołaj adresu URL sieci web na podstawie wartości danych telemetrycznych skonfigurowany, a automatycznego skalowania usługi w chmurze, maszyn wirtualnych i aplikacji sieci Web."
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
ms.openlocfilehash: ec4512500dc3c77a40d2ebd1e6b460d5bb005811
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a><span data-ttu-id="e1de1-105">Przykładów dla platformy Azure CLI wieloplatformowych Monitor 1.0 szybki start</span><span class="sxs-lookup"><span data-stu-id="e1de1-105">Azure Monitor  Cross-platform CLI 1.0 quick start samples</span></span>
<span data-ttu-id="e1de1-106">W tym artykule przedstawiono przykład się, że polecenia interfejsu wiersza polecenia (CLI) ułatwiają dostęp do funkcji Azure monitora.</span><span class="sxs-lookup"><span data-stu-id="e1de1-106">This article shows you sample command-line interface (CLI) commands to help you access Azure Monitor features.</span></span> <span data-ttu-id="e1de1-107">Azure Monitor pozwala automatycznego skalowania usługi w chmurze, maszyn wirtualnych i aplikacji sieci Web, jak i do wysyłania powiadomień o alertach lub zadzwoń na podstawie wartości dane telemetryczne skonfigurowanych adresów URL sieci web.</span><span class="sxs-lookup"><span data-stu-id="e1de1-107">Azure Monitor allows you to AutoScale Cloud Services, Virtual Machines, and Web Apps and to send alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="e1de1-108">Azure Monitor to nowa nazwa dla proponowaną "Azure Insights" do 25 września 2016 r.</span><span class="sxs-lookup"><span data-stu-id="e1de1-108">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="e1de1-109">Jednak przestrzenie nazw, dlatego poniższe polecenia nadal zawierają "insights".</span><span class="sxs-lookup"><span data-stu-id="e1de1-109">However, the namespaces and thus the commands below still contain the "insights".</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="e1de1-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e1de1-110">Prerequisites</span></span>
<span data-ttu-id="e1de1-111">Jeśli nie została jeszcze zainstalowana wiersza polecenia platformy Azure, zobacz [instalowanie interfejsu wiersza polecenia Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e1de1-111">If you haven't already installed the Azure CLI, see [Install the Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="e1de1-112">Jeśli masz doświadczenia w pracy z wiersza polecenia platformy Azure, możesz uzyskać więcej informacji na [użyć wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows za pomocą Menedżera zasobów Azure](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e1de1-112">If you're unfamiliar with Azure CLI, you can read more about it at [Use the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span></span>

<span data-ttu-id="e1de1-113">W systemie Windows, należy zainstalować npm z [witryny sieci Web Node.js](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="e1de1-113">In Windows, install npm from the [Node.js website](https://nodejs.org/).</span></span> <span data-ttu-id="e1de1-114">Po zakończeniu instalacji, używając CMD.exe z uprawnieniami Uruchom jako Administrator, wykonaj następujące czynności, z folderu, w którym zainstalowano npm:</span><span class="sxs-lookup"><span data-stu-id="e1de1-114">After you complete the installation, using CMD.exe with Run As Administrator privileges, execute the following from the folder where npm is installed:</span></span>

```console
npm install azure-cli --global
```

<span data-ttu-id="e1de1-115">Następnie przejdź do dowolnego folderu/lokalizację a wpisz w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="e1de1-115">Next, navigate to any folder/location you want and type at the command-line:</span></span>

```console
azure help
```

## <a name="log-in-to-azure"></a><span data-ttu-id="e1de1-116">Zaloguj się do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e1de1-116">Log in to Azure</span></span>
<span data-ttu-id="e1de1-117">Pierwszym krokiem jest logowania do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e1de1-117">The first step is to login to your Azure account.</span></span>

```console
azure login
```

<span data-ttu-id="e1de1-118">Po uruchomieniu tego polecenia, musisz zalogować się za pośrednictwem zgodnie z instrukcjami na ekranie.</span><span class="sxs-lookup"><span data-stu-id="e1de1-118">After running this command, you have to sign in via the instructions on the screen.</span></span> <span data-ttu-id="e1de1-119">Później Zobacz Twoje konto, identyfikatora dzierżawcy i domyślnego identyfikatora subskrypcji. Wszystkie polecenia działają w kontekście subskrypcji domyślne.</span><span class="sxs-lookup"><span data-stu-id="e1de1-119">Afterward, you see your Account, TenantId, and default Subscription Id. All commands work in the context of your default subscription.</span></span>

<span data-ttu-id="e1de1-120">Aby wyświetlić szczegółowe informacje o Twojej bieżącej subskrypcji, użyj następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="e1de1-120">To list the details of your current subscription, use the following command.</span></span>

```console
azure account show
```

<span data-ttu-id="e1de1-121">Aby zmienić kontekst pracy do innej subskrypcji, użyj następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="e1de1-121">To change working context to a different subscription, use the following command.</span></span>

```console
azure account set "subscription ID or subscription name"
```

<span data-ttu-id="e1de1-122">Aby używać poleceń usługi Azure Resource Manager i Azure Monitor, należy być w trybie Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e1de1-122">To use Azure Resource Manager and Azure Monitor commands, you need to be in Azure Resource Manager mode.</span></span>

```console
azure config mode arm
```

<span data-ttu-id="e1de1-123">Aby wyświetlić listę wszystkich obsługiwanych poleceń Azure Monitor, należy wykonać następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="e1de1-123">To view a list of all supported Azure Monitor commands, perform the following.</span></span>

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a><span data-ttu-id="e1de1-124">Wyświetl dziennik aktywności dla subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e1de1-124">View activity log for a subscription</span></span>
<span data-ttu-id="e1de1-125">Aby wyświetlić listę zdarzeń dziennika aktywności, wykonaj następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="e1de1-125">To view a list of activity log events, perform the following.</span></span>

```console
azure insights logs list [options]
```

<span data-ttu-id="e1de1-126">Spróbuj wykonać następujące czynności, aby wyświetlić wszystkie dostępne opcje.</span><span class="sxs-lookup"><span data-stu-id="e1de1-126">Try the following to view all available options.</span></span>

```console
azure insights logs list -help
```

<span data-ttu-id="e1de1-127">Oto przykład listy dzienniki w grupie zasobów</span><span class="sxs-lookup"><span data-stu-id="e1de1-127">Here is an example to list logs by a resourceGroup</span></span>

```console
azure insights logs list --resourceGroup "myrg1"
```

<span data-ttu-id="e1de1-128">Przykład listy dzienniki przez obiekt wywołujący</span><span class="sxs-lookup"><span data-stu-id="e1de1-128">Example to list logs by caller</span></span>

```console
azure insights logs list --caller "myname@company.com"
```

<span data-ttu-id="e1de1-129">Przykład listy dzienniki przez obiekt wywołujący na typu zasobu w ciągu daty rozpoczęcia i zakończenia</span><span class="sxs-lookup"><span data-stu-id="e1de1-129">Example to list logs by caller on a resource type, within a start and end date</span></span>

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a><span data-ttu-id="e1de1-130">Praca z alertami</span><span class="sxs-lookup"><span data-stu-id="e1de1-130">Work with alerts</span></span>
<span data-ttu-id="e1de1-131">Informacje przedstawione w sekcji służy do pracy z alertami.</span><span class="sxs-lookup"><span data-stu-id="e1de1-131">You can use the information in the section to work with alerts.</span></span>

### <a name="get-alert-rules-in-a-resource-group"></a><span data-ttu-id="e1de1-132">Pobierz reguły alertów w grupie zasobów</span><span class="sxs-lookup"><span data-stu-id="e1de1-132">Get alert rules in a resource group</span></span>
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a><span data-ttu-id="e1de1-133">Utwórz metryki regułę alertu</span><span class="sxs-lookup"><span data-stu-id="e1de1-133">Create a metric alert rule</span></span>
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a><span data-ttu-id="e1de1-134">Utwórz regułę alertu w teście sieci Web</span><span class="sxs-lookup"><span data-stu-id="e1de1-134">Create webtest alert rule</span></span>
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a><span data-ttu-id="e1de1-135">Usuń regułę alertu</span><span class="sxs-lookup"><span data-stu-id="e1de1-135">Delete an alert rule</span></span>
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a><span data-ttu-id="e1de1-136">Profile dziennika</span><span class="sxs-lookup"><span data-stu-id="e1de1-136">Log profiles</span></span>
<span data-ttu-id="e1de1-137">Skorzystaj z informacji w tej sekcji, aby pracować przy użyciu profilów dziennika.</span><span class="sxs-lookup"><span data-stu-id="e1de1-137">Use the information in this section to work with log profiles.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="e1de1-138">Pobierz profil dziennika</span><span class="sxs-lookup"><span data-stu-id="e1de1-138">Get a log profile</span></span>
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a><span data-ttu-id="e1de1-139">Dodawanie profilu dziennika bez przechowywania</span><span class="sxs-lookup"><span data-stu-id="e1de1-139">Add a log profile without retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="e1de1-140">Usuń profil dziennika</span><span class="sxs-lookup"><span data-stu-id="e1de1-140">Remove a log profile</span></span>
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a><span data-ttu-id="e1de1-141">Dodawanie profilu dziennika z przechowywaniem</span><span class="sxs-lookup"><span data-stu-id="e1de1-141">Add a log profile with retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="e1de1-142">Dodawanie profilu dziennika z przechowywania i EventHub</span><span class="sxs-lookup"><span data-stu-id="e1de1-142">Add a log profile with retention and EventHub</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a><span data-ttu-id="e1de1-143">Diagnostyka</span><span class="sxs-lookup"><span data-stu-id="e1de1-143">Diagnostics</span></span>
<span data-ttu-id="e1de1-144">Skorzystaj z informacji w tej sekcji, aby pracować z ustawień diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="e1de1-144">Use the information in this section to work with diagnostic settings.</span></span>

### <a name="get-a-diagnostic-setting"></a><span data-ttu-id="e1de1-145">Pobierz ustawienia diagnostyki</span><span class="sxs-lookup"><span data-stu-id="e1de1-145">Get a diagnostic setting</span></span>
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a><span data-ttu-id="e1de1-146">Wyłącz ustawienie diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="e1de1-146">Disable a diagnostic setting</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a><span data-ttu-id="e1de1-147">Włącz ustawienie diagnostyczne bez przechowywania</span><span class="sxs-lookup"><span data-stu-id="e1de1-147">Enable a diagnostic setting without retention</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a><span data-ttu-id="e1de1-148">Automatyczne skalowanie</span><span class="sxs-lookup"><span data-stu-id="e1de1-148">Autoscale</span></span>
<span data-ttu-id="e1de1-149">Skorzystaj z informacji w tej sekcji, aby pracować z ustawieniami automatycznego skalowania.</span><span class="sxs-lookup"><span data-stu-id="e1de1-149">Use the information in this section to work with autoscale settings.</span></span> <span data-ttu-id="e1de1-150">Należy modyfikować tych przykładów.</span><span class="sxs-lookup"><span data-stu-id="e1de1-150">You need to modify these examples.</span></span>

### <a name="get-autoscale-settings-for-a-resource-group"></a><span data-ttu-id="e1de1-151">Pobierz ustawienia skalowania automatycznego dla grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="e1de1-151">Get autoscale settings for a resource group</span></span>
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a><span data-ttu-id="e1de1-152">Pobierz ustawienia skalowania automatycznego według nazwy w grupie zasobów</span><span class="sxs-lookup"><span data-stu-id="e1de1-152">Get autoscale settings by name in a resource group</span></span>
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a><span data-ttu-id="e1de1-153">Ustawienia auotoscale</span><span class="sxs-lookup"><span data-stu-id="e1de1-153">Set auotoscale settings</span></span>
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
