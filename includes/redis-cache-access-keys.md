<span data-ttu-id="cd18c-101">wystąpienie pamięci podręcznej Redis Azure tooan tooconnect, klienci pamięci podręcznej potrzebują hello nazwy hosta, portów i kluczy hello pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="cd18c-101">tooconnect tooan Azure Redis Cache instance, cache clients need hello host name, ports, and keys of hello cache.</span></span> <span data-ttu-id="cd18c-102">Niektórzy klienci mogą odwoływać się elementy toothese przez nieco innych nazw.</span><span class="sxs-lookup"><span data-stu-id="cd18c-102">Some clients may refer toothese items by slightly different names.</span></span> <span data-ttu-id="cd18c-103">Można pobrać te informacje w hello portalu Azure lub za pomocą narzędzia wiersza polecenia, takich jak wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cd18c-103">You can retrieve this information in hello Azure portal or by using command-line tools such as Azure CLI.</span></span>

### <a name="retrieve-host-name-ports-and-access-keys-using-hello-azure-portal"></a><span data-ttu-id="cd18c-104">Pobierz nazwę hosta, portów i klucze dostępu za pomocą hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="cd18c-104">Retrieve host name, ports, and access keys using hello Azure Portal</span></span>
<span data-ttu-id="cd18c-105">tooretrieve host name, porty i klucze dostępu za pomocą hello portalu Azure, [Przeglądaj](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour pamięci podręcznej w hello [portalu Azure](https://portal.azure.com) i kliknij przycisk **klucze dostępu** i  **Właściwości** w hello **zasobów menu**.</span><span class="sxs-lookup"><span data-stu-id="cd18c-105">tooretrieve host name, ports, and access keys using hello Azure Portal, [browse](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour cache in hello [Azure portal](https://portal.azure.com) and click **Access keys** and **Properties** in hello **Resource menu**.</span></span> 

![Ustawienia pamięci podręcznej Redis](media/redis-cache-access-keys/redis-cache-hostname-ports-keys.png)

### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a><span data-ttu-id="cd18c-107">Pobieranie nazwy hosta, portów i kluczy dostępu przy użyciu interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cd18c-107">Retrieve host name, ports, and access keys using Azure CLI</span></span>
<span data-ttu-id="cd18c-108">Nazwa hosta hello tooretrieve i portów za pomocą 2.0 interfejsu wiersza polecenia platformy Azure można wywołać [Pokaż redis az](https://docs.microsoft.com/cli/azure/redis#show)i kluczy hello tooretrieve można wywołać [az redis listy kluczy](https://docs.microsoft.com/cli/azure/redis#list-keys).</span><span class="sxs-lookup"><span data-stu-id="cd18c-108">tooretrieve hello host name and ports using Azure CLI 2.0 you can call [az redis show](https://docs.microsoft.com/cli/azure/redis#show), and tooretrieve hello keys you can call [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#list-keys).</span></span> <span data-ttu-id="cd18c-109">Witaj poniższy skrypt wywołuje następujące dwa polecenia i tłumiące echo hello nazwy hosta, portów i kluczy toohello konsoli.</span><span class="sxs-lookup"><span data-stu-id="cd18c-109">hello following script calls these two commands and echos hello hostname, ports, and keys toohello console.</span></span>

```azurecli
#/bin/bash

# Retrieve hello hostname, ports, and keys for contosoCache located in contosoGroup

# Retrieve hello hostname and ports for an Azure Redis Cache instance
redis=($(az redis show --name contosoCache --resource-group contosoGroup --query [hostName,enableNonSslPort,port,sslPort] --output tsv))

# Retrieve hello keys for an Azure Redis Cache instance
keys=($(az redis list-keys --name contosoCache --resource-group contosoGroup --query [primaryKey,secondaryKey] --output tsv))

# Display hello retrieved hostname, keys, and ports
echo "Hostname:" ${redis[0]}
echo "Non SSL Port:" ${redis[2]}
echo "Non SSL Port Enabled:" ${redis[1]}
echo "SSL Port:" ${redis[3]}
echo "Primary Key:" ${keys[0]}
echo "Secondary Key:" ${keys[1]}
```

<span data-ttu-id="cd18c-110">Aby uzyskać więcej informacji dotyczących tego skryptu, zobacz [uzyskać hello nazwy hosta, portów i klucze dla pamięci podręcznej Redis Azure](../articles/redis-cache/scripts/cache-keys-ports.md).</span><span class="sxs-lookup"><span data-stu-id="cd18c-110">For more information about this script, see [Get hello hostname, ports, and keys for Azure Redis Cache](../articles/redis-cache/scripts/cache-keys-ports.md).</span></span> <span data-ttu-id="cd18c-111">Aby uzyskać więcej informacji na temat interfejsu wiersza polecenia platformy Azure w wersji 2.0, zobacz [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Instalowanie interfejsu wiersza polecenia platformy Azure w wersji 2.0) i [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) (Rozpoczynanie pracy z interfejsem wiersza polecenia platformy Azure w wersji 2.0).</span><span class="sxs-lookup"><span data-stu-id="cd18c-111">For more information on Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>
