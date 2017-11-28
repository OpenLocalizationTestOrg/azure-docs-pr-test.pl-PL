<span data-ttu-id="6ebd9-101">Możesz również sprawdzić, czy połączenie zostało pomyślnie nawiązane, używając polecenia cmdlet „Get-AzureRmVirtualNetworkGatewayConnection” z opcją „-Debug” lub bez niej.</span><span class="sxs-lookup"><span data-stu-id="6ebd9-101">You can verify that your connection succeeded by using the 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet, with or without '-Debug'.</span></span> 

1. <span data-ttu-id="6ebd9-102">Można skorzystać z następującego przykładu użycia polecenia cmdlet, dopasowując wartości do własnych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="6ebd9-102">Use the following cmdlet example, configuring the values to match your own.</span></span> <span data-ttu-id="6ebd9-103">Po wyświetleniu monitu wybierz „A”, aby uruchomić wszystko.</span><span class="sxs-lookup"><span data-stu-id="6ebd9-103">If prompted, select 'A' in order to run 'All'.</span></span> <span data-ttu-id="6ebd9-104">W podanym przykładzie opcja „-Name” odnosi się do nazwy połączenia, które ma zostać przetestowane.</span><span class="sxs-lookup"><span data-stu-id="6ebd9-104">In the example, '-Name' refers to the name of the connection that you want to test.</span></span>

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. <span data-ttu-id="6ebd9-105">Po zakończeniu działania polecenia cmdlet sprawdź wartości.</span><span class="sxs-lookup"><span data-stu-id="6ebd9-105">After the cmdlet has finished, view the values.</span></span> <span data-ttu-id="6ebd9-106">W poniższym przykładzie stan połączenia jest wyświetlany jako „Połączone” i można zobaczyć bajty przychodzące i wychodzące.</span><span class="sxs-lookup"><span data-stu-id="6ebd9-106">In the example below, the connection status shows as 'Connected' and you can see ingress and egress bytes.</span></span>
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```