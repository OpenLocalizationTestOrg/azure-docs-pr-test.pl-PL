<span data-ttu-id="efe3e-101">Możesz sprawdzić, czy połączenie powiodło się przy użyciu polecenia cmdlet "Get-AzureRmVirtualNetworkGatewayConnection" hello, lub bez '-Debug ".</span><span class="sxs-lookup"><span data-stu-id="efe3e-101">You can verify that your connection succeeded by using hello 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet, with or without '-Debug'.</span></span> 

1. <span data-ttu-id="efe3e-102">Użyj hello poniższy przykład polecenia cmdlet, konfigurowania toomatch wartości hello własne.</span><span class="sxs-lookup"><span data-stu-id="efe3e-102">Use hello following cmdlet example, configuring hello values toomatch your own.</span></span> <span data-ttu-id="efe3e-103">Po wyświetleniu monitu wybierz "A" w kolejności toorun "All".</span><span class="sxs-lookup"><span data-stu-id="efe3e-103">If prompted, select 'A' in order toorun 'All'.</span></span> <span data-ttu-id="efe3e-104">Przykład Witaj "-Name" odwołuje się nazwa toohello hello połączenia, które mają tootest.</span><span class="sxs-lookup"><span data-stu-id="efe3e-104">In hello example, '-Name' refers toohello name of hello connection that you want tootest.</span></span>

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. <span data-ttu-id="efe3e-105">Po zakończeniu działania polecenia cmdlet hello wyświetlić hello wartości.</span><span class="sxs-lookup"><span data-stu-id="efe3e-105">After hello cmdlet has finished, view hello values.</span></span> <span data-ttu-id="efe3e-106">W poniższym przykładzie hello stan połączenia hello jest wyświetlany jako "Połączony", aby sprawdzić Bajty przychodzące i wychodzące.</span><span class="sxs-lookup"><span data-stu-id="efe3e-106">In hello example below, hello connection status shows as 'Connected' and you can see ingress and egress bytes.</span></span>
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```