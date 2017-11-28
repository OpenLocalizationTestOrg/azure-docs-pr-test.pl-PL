### <a name="to-modify-the-local-network-gateway-gatewayipaddress"></a><span data-ttu-id="4700d-101">Aby zmodyfikować element „gatewayIpAddress” bramy sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="4700d-101">To modify the local network gateway 'gatewayIpAddress'</span></span>

<span data-ttu-id="4700d-102">W przypadku zmiany publicznego adresu IP urządzenia sieci VPN, z którym chcesz nawiązać połączenie, musisz zmodyfikować bramę sieci lokalnej w celu odzwierciedlenia tej zmiany.</span><span class="sxs-lookup"><span data-stu-id="4700d-102">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="4700d-103">Adres IP bramy można zmienić bez usuwania istniejącego połączenia bramy sieci VPN (jeśli istnieje).</span><span class="sxs-lookup"><span data-stu-id="4700d-103">The gateway IP address can be changed without removing an existing VPN gateway connection (if you have one).</span></span> <span data-ttu-id="4700d-104">Aby zmodyfikować adres IP bramy, zamień wartości „Site2” i „TestRG1” na własne wartości za pomocą polecenia [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update).</span><span class="sxs-lookup"><span data-stu-id="4700d-104">To modify the gateway IP address, replace the values 'Site2' and 'TestRG1' with your own using the [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update) command.</span></span>

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

<span data-ttu-id="4700d-105">Sprawdź, czy adres IP w danych wyjściowych jest poprawny:</span><span class="sxs-lookup"><span data-stu-id="4700d-105">Verify that the IP address is correct in the output:</span></span>

```
"gatewayIpAddress": "23.99.222.170",
```