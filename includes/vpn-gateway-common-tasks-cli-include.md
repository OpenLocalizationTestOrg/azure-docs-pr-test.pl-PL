### <a name="tooview-local-network-gateways"></a>tooview bramy sieci lokalnej

tooview listę hello bramy sieci lokalnej, użyj hello [lista bramy lokalnej sieci az](https://docs.microsoft.com/cli/azure/network/local-gateway#list) polecenia.

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="tooverify-hello-shared-key-values"></a>Witaj tooverify udostępnionych wartości klucza

Sprawdź, czy wartość klucza hello udostępnionych hello tę samą wartość, który został użyty do konfiguracji urządzenia sieci VPN. Jeśli nie, uruchom ponownie, używając wartości hello z urządzenia hello połączenia hello lub aktualizacji hello urządzenia przy użyciu wartości hello z hello zwracany. Witaj wartości muszą być zgodne. Witaj tooview wspólny klucz, użyj hello [az sieci vpn połączenia listy](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="tooview-hello-vpn-gateway-public-ip-address"></a>Brama sieci VPN hello tooview publicznego adresu IP

toofind hello publicznego adresu IP bramy sieci wirtualnej, użyj hello [az sieci ip publicznego listy](https://docs.microsoft.com/cli/azure/network/public-ip#list) polecenia. Czytelnej, dane wyjściowe hello w tym przykładzie jest sformatowany toodisplay hello lista publicznych adresów IP w formacie tabeli.

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
