#### <a name="toocreate-public-endpoints-on-hello-cloud-appliance"></a>toocreate publiczne punkty końcowe na powitania urządzenia chmury

1. Zaloguj się toohello portalu Azure.
2. Przejdź za**maszyn wirtualnych**, a następnie wybierz opcję i kliknij hello maszyny wirtualnej, która jest używana jako urządzenia chmury.
    
3. Należy toocreate sieci zabezpieczeń grupy (NSG) reguły toocontrol hello przepływu ruchu do i z maszyny wirtualnej. Wykonaj następujące kroki toocreate reguły NSG hello.
    1. Wybierz pozycję **Sieciowa grupa zabezpieczeń**.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. Kliknij przycisk grupy zabezpieczeń sieci domyślne hello, które są prezentowane.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. W obszarze **Reguły zabezpieczeń dla ruchu przychodzącego**.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. Kliknij przycisk **+ Dodaj** toocreate reguły zabezpieczeń dla ruchu przychodzącego.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        W bloku zasady zabezpieczeń dla ruchu przychodzącego Dodaj hello:

        1. Dla hello **nazwa**, typ hello następujące nazwy dla punktu końcowego hello: WinRMHttps.
        
        2. Dla hello **priorytet**, wybierz numer wcześniejsza niż 1000 (czyli hello priorytet reguły domyślnej hello). Wyższa wartość hello, niższy priorytet hello.

        3. Zestaw hello **źródła** za**żadnych**.

        4. Dla hello **usługi**, wybierz pozycję **WinRM**. Witaj **protokołu** jest automatycznie ustawiana za**TCP** i hello **zakres portów** ustawiono zbyt**5986**.

        5. Kliknij przycisk **OK** toocreate hello reguły.

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. Z ostatnim krokiem jest tooassociate grupy zabezpieczeń sieci z podsiecią lub w konkretnym interfejsie sieciowym. Wykonaj następujące kroki tooassociate hello sieciową grupę zabezpieczeń z podsiecią.
    1. Przejdź za**podsieci**.
    2. Kliknij pozycję **+ Skojarz**.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. Wybierz sieci wirtualnej, a następnie wybierz hello odpowiedniej podsieci.
    4. Kliknij przycisk **OK** toocreate hello reguły.

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

Po utworzeniu reguły hello można wyświetlić adres publiczny wirtualnego adresu IP (VIP) hello toodetermine szczegóły. Zapisz ten adres.


