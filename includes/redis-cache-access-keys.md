wystąpienie pamięci podręcznej Redis Azure tooan tooconnect, klienci pamięci podręcznej potrzebują hello nazwy hosta, portów i kluczy hello pamięci podręcznej. Niektórzy klienci mogą odwoływać się elementy toothese przez nieco innych nazw. Można pobrać te informacje w hello portalu Azure lub za pomocą narzędzia wiersza polecenia, takich jak wiersza polecenia platformy Azure.

### <a name="retrieve-host-name-ports-and-access-keys-using-hello-azure-portal"></a>Pobierz nazwę hosta, portów i klucze dostępu za pomocą hello portalu Azure
tooretrieve host name, porty i klucze dostępu za pomocą hello portalu Azure, [Przeglądaj](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour pamięci podręcznej w hello [portalu Azure](https://portal.azure.com) i kliknij przycisk **klucze dostępu** i  **Właściwości** w hello **zasobów menu**. 

![Ustawienia pamięci podręcznej Redis](media/redis-cache-access-keys/redis-cache-hostname-ports-keys.png)

### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a>Pobieranie nazwy hosta, portów i kluczy dostępu przy użyciu interfejsu wiersza polecenia platformy Azure
Nazwa hosta hello tooretrieve i portów za pomocą 2.0 interfejsu wiersza polecenia platformy Azure można wywołać [Pokaż redis az](https://docs.microsoft.com/cli/azure/redis#show)i kluczy hello tooretrieve można wywołać [az redis listy kluczy](https://docs.microsoft.com/cli/azure/redis#list-keys). Witaj poniższy skrypt wywołuje następujące dwa polecenia i tłumiące echo hello nazwy hosta, portów i kluczy toohello konsoli.

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

Aby uzyskać więcej informacji dotyczących tego skryptu, zobacz [uzyskać hello nazwy hosta, portów i klucze dla pamięci podręcznej Redis Azure](../articles/redis-cache/scripts/cache-keys-ports.md). Aby uzyskać więcej informacji na temat interfejsu wiersza polecenia platformy Azure w wersji 2.0, zobacz [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Instalowanie interfejsu wiersza polecenia platformy Azure w wersji 2.0) i [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) (Rozpoczynanie pracy z interfejsem wiersza polecenia platformy Azure w wersji 2.0).
