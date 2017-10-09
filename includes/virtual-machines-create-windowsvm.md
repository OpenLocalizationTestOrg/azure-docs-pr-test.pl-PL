1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).

2. Począwszy od lewego górnego rogu powitania kliknij **nowy > obliczeniowe > systemu Windows Server Datacenter 2016**.

    ![Przejdź toohello obrazy maszyn wirtualnych Azure w portalu hello](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. Na powitania systemu Windows Server 2016 w centrum danych wybierz hello klasycznego modelu wdrożenia. Kliknij pozycję Utwórz.

    ![Zrzut ekranu pokazujący dostępne w portalu hello obrazy maszyn wirtualnych Azure hello](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a>1. Blok Podstawowe

Blok podstawowych ustawień Hello żąda informacji administracyjnych hello maszyny wirtualnej.

1. Wprowadź **nazwa** hello maszyny wirtualnej. Przykład Witaj _HeroVM_ jest nazwą hello hello maszyny wirtualnej. Nazwa Hello musi być 1 – 15 znaków i nie może zawierać znaków specjalnych.

2. Wprowadź **nazwy użytkownika** i silne **hasło** , które są używane toocreate kontem lokalnym na powitania maszyny Wirtualnej. Witaj konto lokalne jest używane toosign w tooand Zarządzanie hello maszyny Wirtualnej. Przykład Witaj _azureuser_ jest hello nazwą użytkownika.

 Witaj hasło musi być 8 do 123 znaków i spełniają trzy poza hello cztery następujące wymagania dotyczące złożoności: mała litera, Wielka litera, cyfra i znak specjalny. Więcej informacji na temat [wymagań dotyczących nazwy użytkownika i hasła](../articles/virtual-machines/windows/faq.md).

3. Witaj **subskrypcji** jest opcjonalna. Często używaną opcją jest „Płatność zgodnie z rzeczywistym użyciem”.

4. Wybierz istniejący **grupy zasobów** lub nazwa typu hello nowej. Przykład Witaj _HeroVMRG_ jest nazwą hello hello grupy zasobów.

5. Wybierz centrum danych Azure **lokalizacji** miejscu hello toorun maszyny Wirtualnej. Przykład Witaj **wschodnie stany USA** jest hello lokalizacji.

6. Gdy wszystko będzie gotowe, kliknij przycisk **dalej** toocontinue toohello dalej bloku.

    ![Zrzut ekranu pokazujący ustawienia hello na powitania bloku podstawowe służące do konfigurowania maszyny Wirtualnej platformy Azure](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a>2. Blok Rozmiar

Witaj rozmiar bloku identyfikuje szczegóły konfiguracji hello hello maszyny Wirtualnej i wyświetla listę różnych opcji, które obejmują systemu operacyjnego, liczbę procesorów, typ dysku magazynu i szacowane koszty miesięcznego użycia.  

Wybierz rozmiar maszyny Wirtualnej, a następnie kliknij przycisk **wybierz** toocontinue. W tym przykładzie _DS1_\__V2 standardowe_ jest hello rozmiar maszyny Wirtualnej.

  ![Zrzut ekranu bloku rozmiar hello, pokazujący hello rozmiary maszyn wirtualnych Azure, które można wybrać](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a>3. Blok Ustawienia

Blok ustawień Hello żądań opcje magazynu i sieci. Można zaakceptować ustawienia domyślne hello. Platforma Azure utworzy odpowiednie wpisy tam, gdzie to konieczne.

Jeśli został wybrany rozmiar maszyny wirtualnej, który obsługuję tę funkcję, możesz wypróbować usługę Azure Premium Storage, wybierając opcję Premium (SSD) w obszarze Typ dysku.

Po zakończeniu wprowadzania zmian kliknij przycisk **OK**.

## <a name="4-summary-blade"></a>4. Blok Podsumowanie

Podsumowanie bloku Hello wymieniono ustawienia hello określone w poprzedniej bloków hello. Kliknij przycisk **OK** gdy wszystko będzie gotowe toomake hello obrazu.

 ![Raport podsumowania bloku określonych ustawień hello maszyny wirtualnej](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

Po utworzeniu maszyny wirtualnej hello hello portal Wyświetla hello nowej maszyny wirtualnej w obszarze **wszystkie zasoby**i wyświetla na pulpicie nawigacyjnym hello kafelka hello maszyny wirtualnej. Witaj odpowiedniej chmury usługi i konto magazynu również są tworzone i wyświetlane. Witaj maszyny wirtualnej i usługi w chmurze są uruchamiane automatycznie i ich stan jest wyświetlany jako **systemem**.

 ![Skonfiguruj punkty końcowe agenta maszyny Wirtualnej i hello hello maszyny wirtualnej](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
