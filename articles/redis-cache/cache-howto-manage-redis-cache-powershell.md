---
title: "aaaManage pamięci podręcznej Redis Azure przy użyciu programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooperform zadania administracyjne dla pamięci podręcznej Redis Azure za pomocą programu Azure PowerShell."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1136efe5-1e33-4d91-bb49-c8e2a6dca475
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: 1d526ce65c4bc05345cd6c3ff370211ed562cab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a>Zarządzanie przy użyciu programu Azure PowerShell pamięć podręczna Azure Redis
> [!div class="op_single_selector"]
> * [PowerShell](cache-howto-manage-redis-cache-powershell.md)
> * [Interfejs wiersza polecenia platformy Azure](cache-manage-cli.md)
> 
> 

W tym temacie pokazano, jak tooperform typowych zadań, takich jak tworzenie, aktualizowanie i jak skalować swoich wystąpień pamięci podręcznej Redis Azure tooregenerate klucze dostępu, jak i tooview informacji o pamięci podręczne. Aby uzyskać pełną listę poleceń cmdlet programu PowerShell pamięci podręcznej Redis Azure, zobacz [poleceń cmdlet pamięć podręczna Redis Azure](https://msdn.microsoft.com/library/azure/mt634513.aspx).

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

Aby uzyskać więcej informacji na temat hello klasycznego modelu wdrażania, zobacz [usługi Azure Resource Manager, a wdrożenie klasyczne: zrozumienie modele wdrażania i stan zasobów hello](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).

## <a name="prerequisites"></a>Wymagania wstępne
Jeśli użytkownik zainstalował już programu Azure PowerShell, musi mieć program Azure PowerShell w wersji 1.0.0 lub nowszej. Można sprawdzić wersji hello programu Azure PowerShell, zainstalowanym za pomocą tego polecenia w wierszu polecenia programu Azure PowerShell hello.

    Get-Module azure | format-table version


Po pierwsze należy zalogować się tooAzure za pomocą tego polecenia.

    Login-AzureRmAccount

Określ adres e-mail hello konta platformy Azure i jego hasło w oknie dialogowym hello logowania Microsoft Azure.

Następnie Jeśli masz wiele subskrypcji Azure, należy tooset subskrypcji platformy Azure. toosee listę bieżących subskrypcji, należy uruchomić to polecenie.

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

toospecify hello subskrypcji, uruchom następujące polecenie hello. Poniższy przykład hello, Nazwa subskrypcji hello jest `ContosoSubscription`.

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

Przed użyciem programu Windows PowerShell z usługą Azure Resource Manager, potrzebne są następujące hello:

* Środowiska Windows PowerShell w wersji 3.0 lub 4.0. toofind hello wersji programu Windows PowerShell, wpisz:`$PSVersionTable` i sprawdź wartość hello `PSVersion` 3.0 lub 4.0. tooinstall zgodnej wersji, zobacz [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) lub [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).

tooget szczegółową pomoc dla każdego polecenia cmdlet widocznej w tym samouczku, polecenia cmdlet Get-Help hello użycia.

    Get-Help <cmdlet-name> -Detailed

Na przykład tooget pomocy hello `New-AzureRmRedisCache` polecenia cmdlet, wpisz:

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-tooconnect-tooother-clouds"></a>Jak tooconnect tooother chmur
Domyślne hello Azure to środowisko `AzureCloud`, która reprezentuje hello wystąpienia globalne chmury Azure. tooconnect tooa inne wystąpienie, użyj hello `Add-AzureRmAccount` z hello `-Environment` lub -`EnvironmentName` przełącznik wiersza polecenia o nazwie środowiska lub hello wymagane środowisko.

toosee hello listę dostępnych środowisk, uruchom hello `Get-AzureRmEnvironment` polecenia cmdlet.

### <a name="tooconnect-toohello-azure-government-cloud"></a>toohello tooconnect chmury Azure dla instytucji rządowych
toohello tooconnect Azure dla instytucji rządowych chmury, użyj następującego polecenia hello.

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

lub

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

toocreate pamięci podręcznej w hello Azure dla instytucji rządowych chmury, użyj jednej z następujących lokalizacji hello.

* USGov Virginia
* USGov Iowa

Aby uzyskać więcej informacji na temat hello Azure dla instytucji rządowych chmury zobacz [Microsoft Azure dla instytucji rządowych](https://azure.microsoft.com/features/gov/) i [Podręczniku dewelopera programu Microsoft Azure dla instytucji rządowych](../azure-government-developer-guide.md).

### <a name="tooconnect-toohello-azure-china-cloud"></a>toohello tooconnect Azure Chin chmury
toohello tooconnect chmury Chin Azure, użyj następującego polecenia hello.

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

lub

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

toocreate pamięci podręcznej w hello Azure Chin chmury, użyj jednej z następujących lokalizacji hello.

* Chiny Wschodnie
* Chiny Północne

Aby uzyskać więcej informacji na temat hello Azure Chin chmury zobacz [AzureChinaCloud dla platformy Azure obsługiwane przez 21Vianet w Chinach](http://www.windowsazure.cn/).

### <a name="tooconnect-toomicrosoft-azure-germany"></a>tooMicrosoft tooconnect platformy Azure w Niemczech
tooMicrosoft tooconnect platformy Azure w Niemczech, użyj następującego polecenia hello.

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


lub

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

toocreate pamięci podręcznej w Microsoft Azure Niemczech, użyj jednej z następujących lokalizacji hello.

* Niemcy Środkowe
* Niemcy Północno-Wschodnie

Aby uzyskać więcej informacji o Microsoft platformy Azure w Niemczech, zobacz [Microsoft Azure Niemcy](https://azure.microsoft.com/overview/clouds/germany/).

### <a name="properties-used-for-azure-redis-cache-powershell"></a>Właściwości używanej do pamięci podręcznej Redis Azure PowerShell
w poniższej tabeli Hello zawiera właściwości i opisy parametrów często używane podczas tworzenia i zarządzania nimi z wystąpień pamięci podręcznej Redis Azure za pomocą programu Azure PowerShell.

| Parametr | Opis | Domyślne |
| --- | --- | --- |
| Nazwa |Nazwa hello pamięci podręcznej | |
| Lokalizacja |Lokalizacja pamięci podręcznej hello | |
| Grupy zasobów o nazwie |Nazwa grupy zasobów, w których pamięci podręcznej hello toocreate | |
| Rozmiar |rozmiar Hello hello pamięci podręcznej. Prawidłowe wartości to: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2,5 GB, 6 GB, 13 GB, 26 GB, 53 GB |1 GB |
| ShardCount |Liczba Hello toocreate odłamków podczas tworzenia usługi pamięć podręczna premium z włączoną funkcją klastrowania. Prawidłowe wartości to: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 | |
| SKU |Określa hello SKU hello pamięci podręcznej. Prawidłowe wartości to: Basic, Standard, Premium |Standardowa |
| RedisConfiguration |Określa ustawienia konfiguracji pamięci podręcznej Redis. Aby uzyskać szczegółowe informacje o każdym ustawieniu, zobacz następujące hello [RedisConfiguration właściwości](#redisconfiguration-properties) tabeli. | |
| EnableNonSslPort |Wskazuje, czy włączono port bez protokołu SSL hello. |False |
| MaxMemoryPolicy |Ten parametr jest przestarzały — zamiast tego użyj RedisConfiguration. | |
| StaticIP |Podczas obsługi pamięci podręcznej w sieci Wirtualnej, określa unikatowy adres IP w podsieci hello hello pamięci podręcznej. Jeśli nie zostanie podana, co jest wybrany dla Ciebie z hello podsieci. | |
| Podsieć |Podczas obsługi pamięci podręcznej w sieci Wirtualnej, określa nazwę hello hello podsieci, w których pamięci podręcznej hello toodeploy. | |
| VirtualNetwork |Podczas obsługi pamięci podręcznej w sieci Wirtualnej, określa identyfikator zasobu hello hello sieci Wirtualnej, w których pamięci podręcznej hello toodeploy. | |
| Właściwość KeyType |Określa klucz dostępu, do którego tooregenerate podczas odnawiania klucze dostępu. Prawidłowe wartości to: podstawowej, dodatkowej | |

### <a name="redisconfiguration-properties"></a>Właściwości RedisConfiguration
| Właściwość | Opis | Warstwy cenowe |
| --- | --- | --- |
| włączone kopii zapasowej RDB |Czy [trwałość danych Redis](cache-how-to-premium-persistence.md) jest włączone |Tylko w warstwie Premium |
| RDB magazynu-— parametry połączenia |Witaj konto magazynu toohello ciągu połączenia dla [trwałość danych Redis](cache-how-to-premium-persistence.md) |Tylko w warstwie Premium |
| częstotliwość w przypadku wykonywania kopii zapasowych RDB |Częstotliwość wykonywania kopii zapasowych dla Hello [trwałość danych Redis](cache-how-to-premium-persistence.md) |Tylko w warstwie Premium |
| zastrzeżone maxmemory |Konfiguruje hello [pamięci zarezerwowanej](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) -cache procesów |Standardowa i Premium |
| maxmemory-policy. |Konfiguruje hello [zasady wykluczania](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) hello pamięci podręcznej |Wszystkie warstwy cenowe |
| powiadomienia przestrzeni kluczy zdarzenia |Konfiguruje [powiadomienia przestrzeni kluczy](cache-configure.md#keyspace-notifications-advanced-settings) |Standardowa i Premium |
| Skrót max-ziplist — wpisów |Konfiguruje [optymalizacji pamięci](http://redis.io/topics/memory-optimization) dla typów małych agregowanie danych |Standardowa i Premium |
| max-ziplist — wartość skrótu |Konfiguruje [optymalizacji pamięci](http://redis.io/topics/memory-optimization) dla typów małych agregowanie danych |Standardowa i Premium |
| zestaw max-intset wpisów |Konfiguruje [optymalizacji pamięci](http://redis.io/topics/memory-optimization) dla typów małych agregowanie danych |Standardowa i Premium |
| zset-max-ziplist wpisów |Konfiguruje [optymalizacji pamięci](http://redis.io/topics/memory-optimization) dla typów małych agregowanie danych |Standardowa i Premium |
| zset-max-ziplist-value |Konfiguruje [optymalizacji pamięci](http://redis.io/topics/memory-optimization) dla typów małych agregowanie danych |Standardowa i Premium |
| bazy danych |Konfiguruje hello liczbę baz danych. Tej właściwości można skonfigurować tylko na tworzenie pamięci podręcznej. |Standardowa i Premium |

## <a name="toocreate-a-redis-cache"></a>toocreate pamięci podręcznej Redis
Nowe wystąpienia pamięci podręcznej Redis Azure są tworzone przy użyciu hello [AzureRmRedisCache nowy](https://msdn.microsoft.com/library/azure/mt634517.aspx) polecenia cmdlet.

> [!IMPORTANT]
> Witaj tworzenia pamięci podręcznej Redis w ramach subskrypcji przy użyciu hello portalu Azure po raz pierwszy hello portalu rejestruje hello `Microsoft.Cache` przestrzeni nazw dla tej subskrypcji. Jeśli podjęto toocreate hello najpierw Redis pamięci podręcznej w ramach subskrypcji przy użyciu programu PowerShell, najpierw należy zarejestrować tej przestrzeni nazw przy użyciu następującego polecenia; hello w przeciwnym razie poleceń cmdlet, takich jak `New-AzureRmRedisCache` i `Get-AzureRmRedisCache` się nie powieść.
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

toosee listę dostępnych parametrów i ich opisy `New-AzureRmRedisCache`Uruchom hello następujące polecenia.

    PS C:\> Get-Help New-AzureRmRedisCache -detailed

    NAME
        New-AzureRmRedisCache

    SYNOPSIS
        Creates a new redis cache.


    SYNTAX
        New-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Location <String> [-RedisVersion <String>]
        [-Size <String>] [-Sku <String>] [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort
        <Boolean>] [-ShardCount <Integer>] [-VirtualNetwork <String>] [-Subnet <String>] [-StaticIP <String>]
        [<CommonParameters>]


    DESCRIPTION
        hello New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of hello redis cache toocreate.

        -ResourceGroupName <String>
            Name of resource group in which toocreate hello redis cache.

        -Location <String>
            Location in which toocreate hello redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, hello default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        -VirtualNetwork <String>
            hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

toocreate pamięci podręcznej z parametrów domyślnych, uruchom następujące polecenie hello.

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

`ResourceGroupName`, `Name`, i `Location` są wymagane parametry, ale pozostałe hello są opcjonalne i mają przypisane wartości domyślne. Uruchamianie hello poprzednie polecenie tworzy wystąpienie standardowy SKU pamięć podręczna Redis Azure hello określonej nazwy, lokalizacji i grupy zasobów o rozmiarze z portu bez protokołu SSL hello wyłączone 1 GB.

toocreate pamięć podręczna premium, określ rozmiar P1 (6 GB — 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB), lub P4 (53 GB - 530 GB). tooenable klaster, określić liczbę niezależnych przy użyciu hello `ShardCount` parametru. Witaj poniższy przykład tworzy pamięć podręczna premium P1 z odłamków 3. Pamięć podręczna premium P1 6 GB ma rozmiar, a ponieważ możemy określić trzy odłamków hello całkowity rozmiar jest 18 GB (3 x 6 GB).

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

wartości toospecify hello `RedisConfiguration` parametru, ujmij wartości hello wewnątrz `{}` jako klucza i wartości, takich jak pary `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`. Witaj poniższy przykład tworzy standardowe 1 GB pamięci podręcznej z `allkeys-random` maxmemory zasad i przestrzeni kluczy powiadomienia skonfigurowane z `KEA`. Aby uzyskać więcej informacji, zobacz [powiadomienia przestrzeni kluczy (Zaawansowane ustawienia)](cache-configure.md#keyspace-notifications-advanced-settings) i [zasady pamięci](cache-configure.md#memory-policies).

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="tooconfigure-hello-databases-setting-during-cache-creation"></a>bazy danych hello tooconfigure ustawienie podczas tworzenia pamięci podręcznej
Witaj `databases` ustawienie można skonfigurować tylko podczas tworzenia pamięci podręcznej. Witaj poniższy przykład tworzy — warstwa premium P3 (26 GB) pamięci podręcznej z 48 baz danych przy użyciu hello [AzureRmRedisCache nowy](https://msdn.microsoft.com/library/azure/mt634517.aspx) polecenia cmdlet.

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

Aby uzyskać więcej informacji na temat hello `databases` właściwości, zobacz [konfiguracji serwera domyślna pamięci podręcznej Redis Azure](cache-configure.md#default-redis-server-configuration). Aby uzyskać więcej informacji na temat tworzenia pamięci podręcznej przy użyciu hello [AzureRmRedisCache nowy](https://msdn.microsoft.com/library/azure/mt634517.aspx) polecenia cmdlet, zobacz poprzednie hello [toocreate pamięci podręcznej Redis](#to-create-a-redis-cache) sekcji.

## <a name="tooupdate-a-redis-cache"></a>tooupdate pamięci podręcznej Redis
Wystąpienia pamięci podręcznej Redis Azure są aktualizowane przy użyciu hello [AzureRmRedisCache zestaw](https://msdn.microsoft.com/library/azure/mt634518.aspx) polecenia cmdlet.

toosee listę dostępnych parametrów i ich opisy `Set-AzureRmRedisCache`Uruchom hello następujące polecenia.

    PS C:\> Get-Help Set-AzureRmRedisCache -detailed

    NAME
        Set-AzureRmRedisCache

    SYNOPSIS
        Set redis cache updatable parameters.

    SYNTAX
        Set-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Size <String>] [-Sku <String>]
        [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort <Boolean>] [-ShardCount
        <Integer>] [<CommonParameters>]

    DESCRIPTION
        hello Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooupdate.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. hello default value is null and no change will be made toothe
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

Witaj `Set-AzureRmRedisCache` polecenia cmdlet mogą być używane tooupdate właściwości, takie jak `Size`, `Sku`, `EnableNonSslPort`i hello `RedisConfiguration` wartości. 

Witaj następujące polecenia, które aktualizacje hello maxmemory-policy dla pamięci podręcznej Redis hello o nazwie myCache.

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="tooscale-a-redis-cache"></a>tooscale pamięci podręcznej Redis
`Set-AzureRmRedisCache`może być używane tooscale wystąpienia pamięci podręcznej Azure Redis podczas hello `Size`, `Sku`, lub `ShardCount` są modyfikowane właściwości. 

> [!NOTE]
> Skalowanie pamięci podręcznej przy użyciu programu PowerShell jest toohello podmiotu takie same ograniczenia i wytyczne jako skalowanie pamięci podręcznej z hello portalu Azure. Możesz skalować tooa inną warstwa cenowa z hello następujące ograniczenia.
> 
> * Nie można skalować z wyższej cenową warstwy tooa dolnej warstwy cenowej.
> * Nie można skalować z **Premium** pamięci podręcznej w dół tooa **standardowe** lub **podstawowe** pamięci podręcznej.
> * Nie można skalować z **standardowe** pamięci podręcznej w dół tooa **podstawowe** pamięci podręcznej.
> * Możesz skalować z **podstawowe** pamięci podręcznej tooa **standardowe** pamięci podręcznej, ale nie można zmienić rozmiaru hello na powitania tym samym czasie. Jeśli potrzebujesz zmienić rozmiar należy kolejnych skalowania rozmiar toohello żądaną operację.
> * Nie można skalować z **podstawowe** pamięci podręcznej bezpośrednio tooa **Premium** pamięci podręcznej. Należy skalować z **podstawowe** za**standardowe** w jednej operacji skalowania, a następnie z **standardowe** za**Premium** kolejnych skalowania Operacja.
> * Nie można skalować z większego rozmiaru dół toohello **C0 (250 MB)** rozmiar.
> 
> Aby uzyskać więcej informacji, zobacz [jak tooScale Azure pamięci podręcznej Redis](cache-how-to-scale.md).
> 
> 

Witaj poniższy przykład przedstawia sposób tooscale pamięci podręcznej o nazwie `myCache` tooa 2,5 GB w pamięci podręcznej. Należy pamiętać, że to polecenie działa zarówno Basic lub Standard pamięci podręcznej.

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

Po uruchomieniu tego polecenia, zwracany jest stan hello hello pamięci podręcznej (podobne toocalling `Get-AzureRmRedisCache`). Należy pamiętać, że hello `ProvisioningState` jest `Scaling`.

    PS C:\> Set-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup -Size 2.5GB


    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/mygroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Scaling
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 150], [notify-keyspace-events, KEA],
                         [maxmemory-delta, 150]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : mygroup
    PrimaryKey         : ....
    SecondaryKey       : ....
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

Po zakończeniu operacji skalowania hello hello `ProvisioningState` zmiany zbyt`Succeeded`. Jeśli potrzebujesz toomake kolejnych operacji skalowania, takich jak zmiana z tooStandard podstawowych, a następnie zmienić rozmiar hello, należy zaczekać, aż hello Poprzednia operacja została ukończona lub jest wyświetlany następujący błąd podobny toohello.

    Set-AzureRmRedisCache : Conflict: hello resource '...' is not in a stable state, and is currently unable tooaccept hello update request.

## <a name="tooget-information-about-a-redis-cache"></a>tooget informacji o pamięci podręcznej Redis
Można pobrać informacji o pamięci podręcznej przy użyciu hello [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) polecenia cmdlet.

toosee listę dostępnych parametrów i ich opisy `Get-AzureRmRedisCache`Uruchom hello następujące polecenia.

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in hello specified resource group or all caches in hello current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCache cmdlet gets hello details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in hello specified resource group.

        If no parameters are given than it will return details about all caches hello current subscription.

    PARAMETERS
        -Name <String>
            hello name of hello cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns hello details for hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns hello details of hello cache specified by Name. If only hello ResourceGroup
            parameter is provided, then details for all caches in hello resource group are returned.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

Uruchom tooreturn informacji na temat wszystkich usług pamięć podręczna w bieżącej subskrypcji hello `Get-AzureRmRedisCache` bez żadnych parametrów.

    Get-AzureRmRedisCache

Uruchom tooreturn informacji na temat wszystkich usług pamięć podręczna w grupie zasobów specyficznych `Get-AzureRmRedisCache` z hello `ResourceGroupName` parametru.

    Get-AzureRmRedisCache -ResourceGroupName myGroup

Uruchom tooreturn informacji na temat określonych pamięci podręcznej, `Get-AzureRmRedisCache` z hello `Name` parametr zawierający nazwę hello hello pamięci podręcznej i hello `ResourceGroupName` parametru z grupą zasobów hello zawierającą tej pamięci podręcznej.

    PS C:\> Get-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/myGroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Succeeded
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 62], [notify-keyspace-events, KEA],
                         [maxclients, 1000]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : myGroup
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

## <a name="tooretrieve-hello-access-keys-for-a-redis-cache"></a>tooretrieve hello klucze dostępu pamięci podręcznej Redis
tooretrieve hello klucze dostępu dla pamięci podręcznej, można użyć hello [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) polecenia cmdlet.

toosee listę dostępnych parametrów i ich opisy `Get-AzureRmRedisCacheKey`Uruchom hello następujące polecenia.

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets hello accesskeys for hello specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCacheKey cmdlet gets hello access keys for hello specified cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

tooretrieve hello kluczy dla pamięci podręcznej, wywołanie hello `Get-AzureRmRedisCacheKey` polecenia cmdlet i przekaż nazwę hello pamięć podręczną hello nazwę grupy zasobów hello, która zawiera hello pamięci podręcznej.

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="tooregenerate-access-keys-for-your-redis-cache"></a>tooregenerate klucze dostępu pamięci podręcznej Redis
tooregenerate hello klucze dostępu dla pamięci podręcznej, można użyć hello [AzureRmRedisCacheKey nowy](https://msdn.microsoft.com/library/azure/mt634512.aspx) polecenia cmdlet.

toosee listę dostępnych parametrów i ich opisy `New-AzureRmRedisCacheKey`Uruchom hello następujące polecenia.

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates hello access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        hello New-AzureRmRedisCacheKey cmdlet regenerate hello access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -KeyType <String>
            Specifies whether tooregenerate hello primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When hello Force parameter is provided, hello specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

tooregenerate klucz podstawowy lub pomocniczy hello pamięci podręcznej, wywołanie hello `New-AzureRmRedisCacheKey` polecenia cmdlet i przekaż hello Nazwa grupy zasobów oraz określ `Primary` lub `Secondary` dla hello `KeyType` parametru. W hello poniższy przykład hello pomocniczy klucz dostępu dla pamięci podręcznej zostanie ponownie wygenerowany.

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want tooregenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="toodelete-a-redis-cache"></a>toodelete pamięci podręcznej Redis
toodelete pamięci podręcznej Redis, użyj hello [AzureRmRedisCache Usuń](https://msdn.microsoft.com/library/azure/mt634515.aspx) polecenia cmdlet.

toosee listę dostępnych parametrów i ich opisy `Remove-AzureRmRedisCache`Uruchom hello następujące polecenia.

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        hello Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooremove.

        -ResourceGroupName <String>
            Name of hello resource group of hello cache tooremove.

        -Force
            When hello Force parameter is provided, hello cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes hello cache and does not return any value. If hello PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating hello success of hello operatio

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

W hello poniższy przykład, hello pamięci podręcznej o nazwie `myCache` zostanie usunięta.

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want tooremove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="tooimport-a-redis-cache"></a>tooimport pamięci podręcznej Redis
Dane można importować do wystąpienia pamięci podręcznej Redis Azure za pomocą hello `Import-AzureRmRedisCache` polecenia cmdlet.

> [!IMPORTANT]
> Narzędzie importu/eksportu jest dostępna tylko dla [warstwy premium](cache-premium-tier-intro.md) przechowuje w pamięci podręcznej. Aby uzyskać więcej informacji na temat importowania i eksportowania, zobacz [importować i eksportować dane w pamięci podręcznej Redis Azure](cache-how-to-import-export-data.md).
> 
> 

toosee listę dostępnych parametrów i ich opisy `Import-AzureRmRedisCache`Uruchom hello następujące polecenia.

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs tooAzure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Import-AzureRmRedisCache cmdlet imports data from hello specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into hello cache.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -Force
            When hello Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If hello PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating hello success of the
            operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


Witaj następujące polecenie importuje dane z obiektu blob hello określonego przez identyfikator uri sygnatury dostępu Współdzielonego hello do pamięci podręcznej Redis Azure.

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="tooexport-a-redis-cache"></a>tooexport pamięci podręcznej Redis
Można eksportować dane z wystąpienia pamięci podręcznej Redis Azure za pomocą hello `Export-AzureRmRedisCache` polecenia cmdlet.

> [!IMPORTANT]
> Narzędzie importu/eksportu jest dostępna tylko dla [warstwy premium](cache-premium-tier-intro.md) przechowuje w pamięci podręcznej. Aby uzyskać więcej informacji na temat importowania i eksportowania, zobacz [importować i eksportować dane w pamięci podręcznej Redis Azure](cache-how-to-import-export-data.md).
> 
> 

toosee listę dostępnych parametrów i ich opisy `Export-AzureRmRedisCache`Uruchom hello następujące polecenia.

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache tooa specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache tooa specified container.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Prefix <String>
            Prefix toouse for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


Witaj następujące polecenie eksportuje dane z wystąpienia pamięci podręcznej Redis Azure do kontenera hello określony przez identyfikator uri sygnatury dostępu Współdzielonego hello.

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="tooreboot-a-redis-cache"></a>tooreboot pamięci podręcznej Redis
Ponowne uruchomienie wystąpienia pamięci podręcznej Redis Azure za pomocą hello `Reset-AzureRmRedisCache` polecenia cmdlet.

> [!IMPORTANT]
> Ponowne uruchomienie jest dostępna tylko dla [warstwy premium](cache-premium-tier-intro.md) przechowuje w pamięci podręcznej. Aby uzyskać więcej informacji o ponowne uruchomienie z pamięci podręcznej, zobacz [pamięci podręcznej administracji — ponowny rozruch](cache-administration.md#reboot).
> 
> 

toosee listę dostępnych parametrów i ich opisy `Reset-AzureRmRedisCache`Uruchom hello następujące polecenia.

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Reset-AzureRmRedisCache cmdlet reboots hello specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -RebootType <String>
            Which node tooreboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard tooreboot when rebooting a premium cache with clustering enabled.

        -Force
            When hello Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


Hello następujące polecenie ponownego uruchamiania obu węzłów hello określono pamięci podręcznej.

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat przy użyciu programu Windows PowerShell przy użyciu platformy Azure, zobacz następujące zasoby hello:

* [Azure dokumentację poleceń cmdlet pamięci podręcznej Redis w witrynie MSDN](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* [Polecenia cmdlet Menedżera zasobów systemu Azure](http://go.microsoft.com/fwlink/?LinkID=394765): Omówienie poleceń cmdlet hello toouse w module usługi Azure Resource Manager hello.
* [Toomanage przy użyciu zasobów grup zasobów platformy Azure](../azure-resource-manager/resource-group-template-deploy-portal.md): Dowiedz się, jak toocreate grup zasobów w hello portalu Azure i zarządzanie nimi.
* [Azure blog](http://blogs.msdn.com/windowsazure): więcej informacji na temat nowych funkcji w systemie Azure.
* [Blog dotyczący programu Windows PowerShell](http://blogs.msdn.com/powershell): więcej informacji na temat nowych funkcji w programie Windows PowerShell.
* ["Witaj, Twórco skryptów!" Blog](http://blogs.technet.com/b/heyscriptingguy/): Pobierz rzeczywistych porady i wskazówki związane z hello społeczności programu Windows PowerShell.

