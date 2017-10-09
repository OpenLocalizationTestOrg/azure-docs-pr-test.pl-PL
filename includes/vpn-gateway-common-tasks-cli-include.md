### <a name="tooview-local-network-gateways"></a><span data-ttu-id="673a1-101">tooview bramy sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="673a1-101">tooview local network gateways</span></span>

<span data-ttu-id="673a1-102">tooview listę hello bramy sieci lokalnej, użyj hello [lista bramy lokalnej sieci az](https://docs.microsoft.com/cli/azure/network/local-gateway#list) polecenia.</span><span class="sxs-lookup"><span data-stu-id="673a1-102">tooview a list of hello local network gateways, use hello [az network local-gateway list](https://docs.microsoft.com/cli/azure/network/local-gateway#list) command.</span></span>

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="tooverify-hello-shared-key-values"></a><span data-ttu-id="673a1-103">Witaj tooverify udostępnionych wartości klucza</span><span class="sxs-lookup"><span data-stu-id="673a1-103">tooverify hello shared key values</span></span>

<span data-ttu-id="673a1-104">Sprawdź, czy wartość klucza hello udostępnionych hello tę samą wartość, który został użyty do konfiguracji urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="673a1-104">Verify that hello shared key value is hello same value that you used for your VPN device configuration.</span></span> <span data-ttu-id="673a1-105">Jeśli nie, uruchom ponownie, używając wartości hello z urządzenia hello połączenia hello lub aktualizacji hello urządzenia przy użyciu wartości hello z hello zwracany.</span><span class="sxs-lookup"><span data-stu-id="673a1-105">If it is not, either run hello connection again using hello value from hello device, or update hello device with hello value from hello return.</span></span> <span data-ttu-id="673a1-106">Witaj wartości muszą być zgodne.</span><span class="sxs-lookup"><span data-stu-id="673a1-106">hello values must match.</span></span> <span data-ttu-id="673a1-107">Witaj tooview wspólny klucz, użyj hello [az sieci vpn połączenia listy](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span><span class="sxs-lookup"><span data-stu-id="673a1-107">tooview hello shared key, use hello [az network vpn-connection-list](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span></span>

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="tooview-hello-vpn-gateway-public-ip-address"></a><span data-ttu-id="673a1-108">Brama sieci VPN hello tooview publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="673a1-108">tooview hello VPN gateway Public IP address</span></span>

<span data-ttu-id="673a1-109">toofind hello publicznego adresu IP bramy sieci wirtualnej, użyj hello [az sieci ip publicznego listy](https://docs.microsoft.com/cli/azure/network/public-ip#list) polecenia.</span><span class="sxs-lookup"><span data-stu-id="673a1-109">toofind hello public IP address of your virtual network gateway, use hello [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="673a1-110">Czytelnej, dane wyjściowe hello w tym przykładzie jest sformatowany toodisplay hello lista publicznych adresów IP w formacie tabeli.</span><span class="sxs-lookup"><span data-stu-id="673a1-110">For easy reading, hello output for this example is formatted toodisplay hello list of public IPs in table format.</span></span>

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
