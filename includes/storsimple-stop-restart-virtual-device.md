#### <a name="toostop-and-start-a-virtual-device"></a>toostop i rozpocząć urządzenie wirtualne
toostop urządzenia wirtualnego, kliknij jego nazwę, a następnie kliknij przycisk **zamknięcia**. Gdy urządzenie wirtualne hello jest zamykany, jego stan jest **zatrzymywanie**. Po wyłączeniu urządzenia wirtualnego hello jego stan jest **zatrzymane**.

Użyj następującego polecenia cmdlet toostop hello i uruchamiania urządzenia wirtualnego.

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-virtual-device"></a>toorestart urządzenie wirtualne
Gdy urządzenie wirtualne działa i chcesz toorestart, kliknij jego nazwę, a następnie kliknij **ponownego uruchomienia**. Podczas ponownego uruchamiania urządzenia wirtualnego hello, jego stan jest **ponowne**. Gdy urządzenie wirtualne hello jest gotowy do możesz toouse, jego stan jest **systemem**.

Użyj następującego polecenia cmdlet toorestart urządzenie wirtualne hello.

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

