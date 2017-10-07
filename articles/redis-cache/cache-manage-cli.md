---
title: "pamięć podręczna Redis Azure za pomocą interfejsu wiersza polecenia Azure aaaManage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooinstall hello Azure CLI na dowolnej platformie, jak toouse go tooyour tooconnect konto platformy Azure i w jaki sposób toocreate oraz zarządzania nimi pamięci podręcznej Redis z hello wiersza polecenia platformy Azure."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 964ff245-859d-4bc1-bccf-62e4b3c1169f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: e8ee30090133e6b4edea93dcd13fd171e75989bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-azure-redis-cache-using-hello-azure-command-line-interface-azure-cli"></a>Jak toocreate i zarządzania pamięcią podręczną Redis Azure za pomocą hello interfejsu wiersza polecenia platformy Azure (Azure CLI)
> [!div class="op_single_selector"]
> * [PowerShell](cache-howto-manage-redis-cache-powershell.md)
> * [Interfejs wiersza polecenia platformy Azure](cache-manage-cli.md)
>
>

Hello Azure CLI jest toomanage doskonały sposób infrastruktury platformy Azure z dowolną platformą. W tym artykule opisano sposób toocreate i zarządzanie nimi z wystąpień pamięci podręcznej Redis Azure za pomocą hello wiersza polecenia platformy Azure.

> [!NOTE]
> Ten artykuł dotyczy tooa poprzedniej wersji interfejsu wiersza polecenia Azure. Dla hello najnowsze Azure CLI 2.0 przykładowe skrypty, zobacz [przykłady pamięci podręcznej Azure CLI Redis](cli-samples.md).
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
toocreate i Zarządzanie wystąpieniami usługi pamięć podręczna Redis Azure za pomocą interfejsu wiersza polecenia Azure, należy wykonać następujące kroki hello.

* Musi mieć konto platformy Azure. Jeśli nie masz, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/) za kilka minut.
* [Instalowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md).
* Połącz instalacji wiersza polecenia platformy Azure z osobistego konta Azure lub służbowy lub Azure konta służbowego i logowania z hello interfejsu wiersza polecenia platformy Azure przy użyciu hello `azure login` polecenia. toounderstand hello różnic oraz wybrać, zobacz [połączyć tooan subskrypcji platformy Azure z hello interfejsu wiersza polecenia platformy Azure (Azure CLI)](../xplat-cli-connect.md).
* Przed uruchomieniem żadnego hello następujące polecenia, Przełącz hello wiersza polecenia platformy Azure w trybie Menedżera zasobów, uruchamiając hello `azure config mode arm` polecenia. Aby uzyskać więcej informacji, zobacz [Użyj toomanage interfejsu wiersza polecenia Azure hello Azure zasobów i grup zasobów](../xplat-cli-azure-resource-manager.md).

## <a name="redis-cache-properties"></a>Właściwości pamięci podręcznej redis
Witaj następujące właściwości są używane podczas tworzenia i aktualizowania wystąpienia pamięci podręcznej Redis.

| Właściwość | Przełącznik | Opis |
| --- | --- | --- |
| name |-n, — nazwa |Nazwa hello pamięci podręcznej Redis. |
| grupa zasobów |-g,--grupy zasobów |Nazwa hello grupy zasobów. |
| location |-l, — lokalizacja |Pamięć podręczna toocreate lokalizacji. |
| Rozmiar |-z, — rozmiar |Rozmiar hello pamięci podręcznej Redis. Prawidłowe wartości: [C0 C1, C2, C3, C4, C5, C6, P1, P2, P3, P4] |
| Jednostka SKU |-x - sku |W pamięci podręcznej redis jednostki SKU. Powinien być jednym z: [Basic, Standard, Premium] |
| EnableNonSslPort |-e, - enable bez protokołu ssl portu |Właściwość EnableNonSslPort hello pamięci podręcznej Redis. Dodać tę flagę Port SSL nie hello tooenable dla pamięci podręcznej |
| Redis konfiguracji |-c,--konfiguracja pamięci podręcznej redis |W pamięci podręcznej redis konfiguracji. Wprowadź ciąg w formacie JSON konfiguracji kluczy i wartości w tym miejscu. Format: "{" ":""," ":" "}" |
| Redis konfiguracji |-f, — plik w przypadku konfiguracji pamięci podręcznej redis |W pamięci podręcznej redis konfiguracji. Wprowadź ścieżkę hello plik zawierający konfigurację kluczy i wartości w tym miejscu. Format wpis pliku hello: {"": "","": ""} |
| Liczba niezależnych |-r--niezależnego fragmentu-, count, liczba |Liczba fragmentów toocreate na pamięć podręczna Premium klastrowania z klastra. |
| Virtual Network |-v, — sieci wirtualnej |Podczas obsługi pamięci podręcznej w sieci Wirtualnej, określa pamięci podręcznej w redis hello dokładnie ARM identyfikator zasobu Witaj Witaj toodeploy sieci wirtualnej. Przykładowy format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1 |
| Typ klucza |-t, — typ klucza |Typ klucza toorenew. Prawidłowe wartości: [podstawową, dodatkowej] |
| StaticIP |-p,--static ip < static ip > |Podczas obsługi pamięci podręcznej w sieci Wirtualnej, określa unikatowy adres IP w podsieci hello hello pamięci podręcznej. Jeśli nie zostanie podana, co jest wybrany dla Ciebie z hello podsieci. |
| Podsieć |t,--podsieci<subnet> |Podczas obsługi pamięci podręcznej w sieci Wirtualnej, określa nazwę hello hello podsieci, w których pamięci podręcznej hello toodeploy. |
| VirtualNetwork |-v, — sieci wirtualnej <-sieci wirtualnej > |Podczas obsługi pamięci podręcznej w sieci Wirtualnej, określa pamięci podręcznej w redis hello dokładnie ARM identyfikator zasobu Witaj Witaj toodeploy sieci wirtualnej. Przykładowy format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1 |
| Subskrypcja |-s, - subskrypcji |Identyfikator subskrypcji Hello. |

## <a name="see-all-redis-cache-commands"></a>Zobacz wszystkie polecenia pamięci podręcznej Redis
toosee wszystkie polecenia pamięci podręcznej Redis i ich parametry, użyj hello `azure rediscache -h` polecenia.

    C:\>azure rediscache -h
    help:    Commands toomanage your Azure Redis Cache(s)
    help:
    help:    Create a Redis Cache
    help:      rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Delete an existing Redis Cache
    help:      rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    List all Redis Caches within your Subscription or Resource Group
    help:      rediscache list [options]
    help:
    help:    Show properties of an existing Redis Cache
    help:      rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Change settings of an existing Redis Cache
    help:      rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Renew hello authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a>Tworzenie pamięci podręcznej Redis Cache
toocreate pamięci podręcznej Redis, hello Użyj następującego polecenia:

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

Aby uzyskać więcej informacji na temat tego polecenia, uruchom hello `azure rediscache create -h` polecenia.

    C:\>azure rediscache create -h
    help:    Create a Redis Cache
    help:
    help:    Usage: rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -l, --location <location>                                Location toocreate cache.
    help:      -z, --size <size>                                        Size of hello Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of hello Redis Cache. Add this flag if you want tooenable hello Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here. Format for hello file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards toocreate on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a>Usuń istniejące pamięci podręcznej Redis
toodelete pamięci podręcznej Redis, hello Użyj następującego polecenia:

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

Aby uzyskać więcej informacji na temat tego polecenia, uruchom hello `azure rediscache delete -h` polecenia.

    C:\>azure rediscache delete -h
    help:    Delete an existing Redis Cache
    help:
    help:    Usage: rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which hello cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a>Wyświetl listę wszystkich pamięci podręczne Redis w ramach Twojej subskrypcji lub grupy zasobów
Użyj wszystkich pamięci podręczne Redis w ramach Twojej subskrypcji lub grupy zasobów, toolist hello następujące polecenie:

    azure rediscache list [options]

Aby uzyskać więcej informacji na temat tego polecenia, uruchom hello `azure rediscache list -h` polecenia.

    C:\>azure rediscache list -h
    help:    List all Redis Caches within your Subscription or Resource Group
    help:
    help:    Usage: rediscache list [options]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a>Pokaż właściwości istniejącej pamięci podręcznej Redis
właściwości tooshow istniejącej pamięci podręcznej Redis, hello Użyj następującego polecenia:

    azure rediscache show [--name <name> --resource-group <resource-group>]

Aby uzyskać więcej informacji na temat tego polecenia, uruchom hello `azure rediscache show -h` polecenia.

    C:\>azure rediscache show -h
    help:    Show properties of an existing Redis Cache
    help:
    help:    Usage: rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a>Zmień ustawienia istniejących pamięci podręcznej Redis
Ustawienia toochange istniejącej pamięci podręcznej Redis, hello Użyj następującego polecenia:

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

Aby uzyskać więcej informacji na temat tego polecenia, uruchom hello `azure rediscache set -h` polecenia.

    C:\>azure rediscache set -h
    help:    Change settings of an existing Redis Cache
    help:
    help:    Usage: rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-hello-authentication-key-for-an-existing-redis-cache"></a>Odnawianie klucz uwierzytelniania powitania dla istniejącej pamięci podręcznej Redis
klucz uwierzytelniania hello toorenew dla istniejącej pamięci podręcznej Redis, hello Użyj następującego polecenia:

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

Określ `Primary` lub `Secondary` dla `key-type`.

Aby uzyskać więcej informacji na temat tego polecenia, uruchom hello `azure rediscache renew-key -h` polecenia.

    C:\>azure rediscache renew-key -h
    help:    Renew hello authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key toorenew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a>Lista podstawowe i pomocnicze klucze istniejącej pamięci podręcznej Redis
klucze podstawowe i pomocnicze toolist istniejącej pamięci podręcznej Redis, użyj następującego polecenia hello:

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

Aby uzyskać więcej informacji na temat tego polecenia, uruchom hello `azure rediscache list-keys -h` polecenia.

    C:\>azure rediscache list-keys -h
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:
    help:    Usage: rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)
