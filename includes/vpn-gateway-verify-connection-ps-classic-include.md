Aby sprawdzić, czy połączenie powiodło się, używając polecenia cmdlet "Get-AzureVNetConnection" hello.

1. Użyj hello poniższy przykład polecenia cmdlet, konfigurowania toomatch wartości hello własne. Nazwa Hello hello sieć wirtualna musi być w cudzysłowie, jeśli zawiera spacje.

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. Po zakończeniu działania polecenia cmdlet hello wyświetlić hello wartości. W poniższym przykładzie hello stan łączności hello jest pokazywana jako "Połączony", aby zobaczyć Bajty przychodzące i wychodzące.

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : hello connectivity state for hello local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal