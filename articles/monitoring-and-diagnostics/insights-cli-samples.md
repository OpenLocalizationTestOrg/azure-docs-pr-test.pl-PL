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
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a>Przykładów dla platformy Azure CLI wieloplatformowych Monitor 1.0 szybki start
Ten artykuł przedstawia przykładowe toohelp polecenia interfejsu wiersza polecenia (CLI) możesz uzyskiwać dostęp do funkcji monitorowania Azure. Azure Monitor umożliwia tooAutoScale usługi w chmurze, maszyn wirtualnych i aplikacji sieci Web i toosend powiadomień o alertach lub na podstawie wartości dane telemetryczne skonfigurowanych adresów URL sieci web wywołania.

> [!NOTE]
> Azure Monitor jest nową nazwę hello proponowaną "Azure Insights" do 25 września 2016 r. Jednak hello przestrzeni nazw, dlatego poniższe polecenia hello nadal zawierać hello "insights".
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
Jeśli nie została jeszcze zainstalowana hello wiersza polecenia platformy Azure, zobacz [hello instalowanie interfejsu wiersza polecenia Azure](../cli-install-nodejs.md). Jeśli masz doświadczenia w pracy z wiersza polecenia platformy Azure, możesz uzyskać więcej informacji o [Użyj hello Azure CLI for Mac, Linux i Windows za pomocą Menedżera zasobów Azure](../xplat-cli-azure-resource-manager.md).

W systemie Windows, należy zainstalować npm z hello [witryny sieci Web Node.js](https://nodejs.org/). Po ukończeniu instalacji hello przy użyciu CMD.exe z uprawnieniami Uruchom jako Administrator, wykonaj następujące hello z zainstalowanym npm folderu hello:

```console
npm install azure-cli --global
```

Następnie przejdź tooany/lokalizacja folderu mają i wpisz w hello wiersza polecenia:

```console
azure help
```

## <a name="log-in-tooazure"></a>Zaloguj się za tooAzure
pierwszym krokiem Hello jest tooyour toologin konto platformy Azure.

```console
azure login
```

Po uruchomieniu tego polecenia, należy mieć toosign w za pomocą instrukcji hello na ekranie powitania. Później Zobacz Twoje konto, identyfikatora dzierżawcy i domyślnego identyfikatora subskrypcji. Wszystkie polecenia działają w kontekście hello subskrypcji domyślne.

Szczegóły hello toolist Twojej bieżącej subskrypcji hello Użyj następującego polecenia.

```console
azure account show
```

toochange pracy kontekstu tooa inną subskrypcję, hello Użyj następującego polecenia.

```console
azure account set "subscription ID or subscription name"
```

toouse usługa Azure Resource Manager i Azure Monitor poleceń, należy toobe w trybie Azure Resource Manager.

```console
azure config mode arm
```

tooview listę wszystkich obsługiwanych poleceń Azure Monitor, wykonaj następujące hello.

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a>Wyświetl dziennik aktywności dla subskrypcji
tooview listę zdarzeń dziennika aktywności, wykonaj następujące hello.

```console
azure insights logs list [options]
```

Spróbuj powitania po tooview wszystkich dostępnych opcji.

```console
azure insights logs list -help
```

Oto przykład toolist dzienniki w grupie zasobów

```console
azure insights logs list --resourceGroup "myrg1"
```

Przykład toolist dzienniki przez obiekt wywołujący

```console
azure insights logs list --caller "myname@company.com"
```

Przykład toolist dzienniki przez obiekt wywołujący na typu zasobu w ciągu daty rozpoczęcia i zakończenia

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a>Praca z alertami
Można użyć hello informacji w hello toowork sekcji z alertami.

### <a name="get-alert-rules-in-a-resource-group"></a>Pobierz reguły alertów w grupie zasobów
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a>Utwórz metryki regułę alertu
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a>Utwórz regułę alertu w teście sieci Web
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a>Usuń regułę alertu
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a>Profile dziennika
Użyj informacji hello w tej sekcji toowork przy użyciu profilów dziennika.

### <a name="get-a-log-profile"></a>Pobierz profil dziennika
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a>Dodawanie profilu dziennika bez przechowywania
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a>Usuń profil dziennika
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a>Dodawanie profilu dziennika z przechowywaniem
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a>Dodawanie profilu dziennika z przechowywania i EventHub
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a>Diagnostyka
Użyj informacji hello w tej sekcji toowork z ustawień diagnostycznych.

### <a name="get-a-diagnostic-setting"></a>Pobierz ustawienia diagnostyki
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a>Wyłącz ustawienie diagnostyczne
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a>Włącz ustawienie diagnostyczne bez przechowywania
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a>Automatyczne skalowanie
Użyj informacji hello w tej sekcji toowork z ustawieniami automatycznego skalowania. Należy toomodify tych przykładów.

### <a name="get-autoscale-settings-for-a-resource-group"></a>Pobierz ustawienia skalowania automatycznego dla grupy zasobów.
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a>Pobierz ustawienia skalowania automatycznego według nazwy w grupie zasobów
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a>Ustawienia auotoscale
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
