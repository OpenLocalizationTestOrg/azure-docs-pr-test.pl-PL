### <a name="to-view-local-network-gateways"></a><span data-ttu-id="86280-101">Aby wyświetlić bramy sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="86280-101">To view local network gateways</span></span>

<span data-ttu-id="86280-102">Aby wyświetlić listę bram sieci lokalnej, użyj polecenia [az network local-gateway list](https://docs.microsoft.com/cli/azure/network/local-gateway#list).</span><span class="sxs-lookup"><span data-stu-id="86280-102">To view a list of the local network gateways, use the [az network local-gateway list](https://docs.microsoft.com/cli/azure/network/local-gateway#list) command.</span></span>

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="to-verify-the-shared-key-values"></a><span data-ttu-id="86280-103">Aby sprawdzić wartości klucza współużytkowanego</span><span class="sxs-lookup"><span data-stu-id="86280-103">To verify the shared key values</span></span>

<span data-ttu-id="86280-104">Sprawdź, czy wartość klucza współużytkowanego jest taka sama jak wartość użyta do konfiguracji urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="86280-104">Verify that the shared key value is the same value that you used for your VPN device configuration.</span></span> <span data-ttu-id="86280-105">Jeśli nie, ponownie uruchom połączenie przy użyciu wartości z urządzenia lub zaktualizuj urządzenie wartością ze zwracanych danych.</span><span class="sxs-lookup"><span data-stu-id="86280-105">If it is not, either run the connection again using the value from the device, or update the device with the value from the return.</span></span> <span data-ttu-id="86280-106">Wartości muszą być zgodne.</span><span class="sxs-lookup"><span data-stu-id="86280-106">The values must match.</span></span> <span data-ttu-id="86280-107">Aby wyświetlić klucz współużytkowany, użyj polecenia [az network vpn-connection-list](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span><span class="sxs-lookup"><span data-stu-id="86280-107">To view the shared key, use the [az network vpn-connection-list](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span></span>

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="to-view-the-vpn-gateway-public-ip-address"></a><span data-ttu-id="86280-108">Aby wyświetlić publiczny adres IP bramy sieci VPN</span><span class="sxs-lookup"><span data-stu-id="86280-108">To view the VPN gateway Public IP address</span></span>

<span data-ttu-id="86280-109">Aby znaleźć publiczny adres IP swojej bramy sieci wirtualnej, użyj polecenia [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list).</span><span class="sxs-lookup"><span data-stu-id="86280-109">To find the public IP address of your virtual network gateway, use the [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="86280-110">W celu poprawienia czytelności dane wyjściowe tego polecenia zostały sformatowane do wyświetlania listy publicznych adresów IP w formacie tabeli.</span><span class="sxs-lookup"><span data-stu-id="86280-110">For easy reading, the output for this example is formatted to display the list of public IPs in table format.</span></span>

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
