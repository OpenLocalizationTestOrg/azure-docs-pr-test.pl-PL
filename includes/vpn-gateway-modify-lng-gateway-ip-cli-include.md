### <a name="toomodify-hello-local-network-gateway-gatewayipaddress"></a>Brama sieci lokalnej hello toomodify "gatewayIpAddress"

Witaj urządzenia sieci VPN, które mają tooconnect toohas zmienić publicznego adresu IP, należy najpierw tooreflect bramy sieci lokalnej hello toomodify, która zmienia. adres IP bramy Hello można zmienić bez usunięcia istniejącego połączenia bramy sieci VPN (jeśli istnieje). adres IP bramy hello toomodify, Zastąp wartości hello "Witryna2" i "TestRG1" z własnych przy użyciu hello [aktualizacji bramy lokalnej sieci az](https://docs.microsoft.com/cli/azure/network/local-gateway#update) polecenia.

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

Sprawdź poprawność w danych wyjściowych hello hello adres IP:

```
"gatewayIpAddress": "23.99.222.170",
```