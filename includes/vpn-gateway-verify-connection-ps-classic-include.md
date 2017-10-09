<span data-ttu-id="1015d-101">Aby sprawdzić, czy połączenie powiodło się, używając polecenia cmdlet "Get-AzureVNetConnection" hello.</span><span class="sxs-lookup"><span data-stu-id="1015d-101">You can verify that your connection succeeded by using hello 'Get-AzureVNetConnection' cmdlet.</span></span>

1. <span data-ttu-id="1015d-102">Użyj hello poniższy przykład polecenia cmdlet, konfigurowania toomatch wartości hello własne.</span><span class="sxs-lookup"><span data-stu-id="1015d-102">Use hello following cmdlet example, configuring hello values toomatch your own.</span></span> <span data-ttu-id="1015d-103">Nazwa Hello hello sieć wirtualna musi być w cudzysłowie, jeśli zawiera spacje.</span><span class="sxs-lookup"><span data-stu-id="1015d-103">hello name of hello virtual network must be in quotes if it contains spaces.</span></span>

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. <span data-ttu-id="1015d-104">Po zakończeniu działania polecenia cmdlet hello wyświetlić hello wartości.</span><span class="sxs-lookup"><span data-stu-id="1015d-104">After hello cmdlet has finished, view hello values.</span></span> <span data-ttu-id="1015d-105">W poniższym przykładzie hello stan łączności hello jest pokazywana jako "Połączony", aby zobaczyć Bajty przychodzące i wychodzące.</span><span class="sxs-lookup"><span data-stu-id="1015d-105">In hello example below, hello Connectivity State shows as 'Connected' and you can see ingress and egress bytes.</span></span>

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : hello connectivity state for hello local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal