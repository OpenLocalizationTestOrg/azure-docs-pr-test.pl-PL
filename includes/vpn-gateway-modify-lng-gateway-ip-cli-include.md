### <a name="toomodify-hello-local-network-gateway-gatewayipaddress"></a><span data-ttu-id="fc760-101">Brama sieci lokalnej hello toomodify "gatewayIpAddress"</span><span class="sxs-lookup"><span data-stu-id="fc760-101">toomodify hello local network gateway 'gatewayIpAddress'</span></span>

<span data-ttu-id="fc760-102">Witaj urządzenia sieci VPN, które mają tooconnect toohas zmienić publicznego adresu IP, należy najpierw tooreflect bramy sieci lokalnej hello toomodify, która zmienia.</span><span class="sxs-lookup"><span data-stu-id="fc760-102">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="fc760-103">adres IP bramy Hello można zmienić bez usunięcia istniejącego połączenia bramy sieci VPN (jeśli istnieje).</span><span class="sxs-lookup"><span data-stu-id="fc760-103">hello gateway IP address can be changed without removing an existing VPN gateway connection (if you have one).</span></span> <span data-ttu-id="fc760-104">adres IP bramy hello toomodify, Zastąp wartości hello "Witryna2" i "TestRG1" z własnych przy użyciu hello [aktualizacji bramy lokalnej sieci az](https://docs.microsoft.com/cli/azure/network/local-gateway#update) polecenia.</span><span class="sxs-lookup"><span data-stu-id="fc760-104">toomodify hello gateway IP address, replace hello values 'Site2' and 'TestRG1' with your own using hello [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update) command.</span></span>

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

<span data-ttu-id="fc760-105">Sprawdź poprawność w danych wyjściowych hello hello adres IP:</span><span class="sxs-lookup"><span data-stu-id="fc760-105">Verify that hello IP address is correct in hello output:</span></span>

```
"gatewayIpAddress": "23.99.222.170",
```