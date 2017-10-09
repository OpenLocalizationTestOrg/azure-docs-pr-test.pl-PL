#### <a name="toostop-and-start-a-cloud-appliance"></a>toostop i rozpocząć urządzenia chmury

1. toostop urządzenia chmury, przejdź toohello maszyny Wirtualnej dla urządzenia chmury.
    ![Maszyna wirtualna urządzenia StorSimple w chmurze](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)

2. Na pasku poleceń hello, kliknij **zatrzymać**.

    ![Maszyna wirtualna urządzenia StorSimple w chmurze](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. Po wyświetleniu monitu o potwierdzenie kliknij przycisk **Tak**.

    ![Maszyna wirtualna urządzenia StorSimple w chmurze](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. Po zatrzymaniu maszyny wirtualnej następuje cofnięcie jej przydziału. Gdy urządzenia chmury hello jest zatrzymywana, jego stan jest **Deallocating**. Po wyłączeniu urządzenia chmury hello jego stan jest **zatrzymane (cofnięciu przydziału)**.

    ![Maszyna wirtualna urządzenia StorSimple w chmurze](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. Po zatrzymaniu maszyny Wirtualnej, kliknij przycisk **Start** (przycisk jest dostępny) hello toostart maszyny Wirtualnej. Po uruchomieniu urządzenia chmury hello, jego stan jest **uruchomiono**.

    ![Maszyna wirtualna urządzenia StorSimple w chmurze](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

Użyj następującego polecenia cmdlet toostop hello i uruchomić urządzenia chmury.

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-cloud-appliance"></a>toorestart urządzenia chmury

toorestart urządzenia chmury, przejdź toohello maszyny Wirtualnej dla urządzenia chmury. Na pasku poleceń hello, kliknij **ponownego uruchomienia**. Po wyświetleniu monitu Potwierdź hello ponownego uruchomienia komputera. Gdy urządzenia chmury hello jest gotowy do możesz toouse, jego stan jest **systemem**.

![Maszyna wirtualna urządzenia StorSimple w chmurze](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

Użyj następującego polecenia cmdlet toorestart urządzenia chmury hello.

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

