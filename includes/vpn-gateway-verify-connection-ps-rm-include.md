Możesz sprawdzić, czy połączenie powiodło się przy użyciu polecenia cmdlet "Get-AzureRmVirtualNetworkGatewayConnection" hello, lub bez '-Debug ". 

1. Użyj hello poniższy przykład polecenia cmdlet, konfigurowania toomatch wartości hello własne. Po wyświetleniu monitu wybierz "A" w kolejności toorun "All". Przykład Witaj "-Name" odwołuje się nazwa toohello hello połączenia, które mają tootest.

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. Po zakończeniu działania polecenia cmdlet hello wyświetlić hello wartości. W poniższym przykładzie hello stan połączenia hello jest wyświetlany jako "Połączony", aby sprawdzić Bajty przychodzące i wychodzące.
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```