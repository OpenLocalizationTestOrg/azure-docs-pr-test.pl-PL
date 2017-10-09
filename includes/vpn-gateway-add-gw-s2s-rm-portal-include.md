1. W lewej części strony portalu hello hello, kliknij polecenie  **+**  i wpisz "Brama sieci wirtualnej" w wyszukiwaniu. W obszarze **Wyniki** zlokalizuj i kliknij pozycję **Brama sieci wirtualnej**.
2. U dołu hello bloku "Brama sieci wirtualnej" hello, kliknij przycisk **Utwórz**. Spowoduje to otwarcie hello **Utwórz bramę sieci wirtualnej** bloku.

    ![Tworzenie pól bloku bramy sieci wirtualnej](./media/vpn-gateway-add-gw-s2s-rm-portal-include/vnet_gw.png "Nowa brama")

3. Na powitania **Utwórz bramę sieci wirtualnej** bloku, określ hello wartości dla bramy sieci wirtualnej.

  - **Nazwa**: Nadaj nazwę bramie. To jest nie hello taki sam jak nazewnictwa podsieci bramy. Jego imię i nazwisko hello hello bramy obiektu, którego jest tworzony.
  - **Typ bramy**: Wybierz pozycję **Sieć VPN**. Bramy sieci VPN, użyj typu bramy sieci wirtualnej hello **VPN**. 
  - **Typ sieci VPN**: Wybierz hello typ sieci VPN, który jest określony dla danej konfiguracji. Większość konfiguracji wymaga zastosowania typu sieci VPN opartego na trasach.
  - **Jednostka SKU**: jednostka SKU bramy hello wybierz z listy rozwijanej hello. na liście rozwijanej hello SKU Hello są zależne od hello wybranego typu sieci VPN. Więcej informacji o jednostkach SKU bramy zawiera artykuł [Gateway SKUs](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku) (Jednostki SKU bramy).
  - **Lokalizacja**: może być konieczne toosee tooscroll lokalizacji. Dostosuj hello **lokalizacji** pola toopoint toohello lokalizacji, gdzie znajduje się sieci wirtualnej. Jeśli lokalizacja hello nie wskazuje region toohello, gdzie znajduje się sieci wirtualnej, sieci wirtualnej hello nie będą widoczne w hello następnego kroku "Wybierz sieć wirtualną" z listy rozwijanej.
  - **Sieć wirtualna**: Wybierz hello toowhich sieci wirtualnej ma tooadd tej bramy. Kliknij przycisk **sieci wirtualnej** bloku "Wybierz sieć wirtualną" hello tooopen. Wybierz hello sieci wirtualnej. Jeśli nie widzisz sieci wirtualnej, upewnij się, że pole lokalizacji hello wskazuje toohello regionu, w którym znajduje się sieci wirtualnej.
  - **Publiczny adres IP**: bloku "Tworzenie publicznego adresu IP" hello tworzy obiekt publiczny adres IP. Po utworzeniu bramy sieci VPN hello Hello publiczny adres IP jest przypisywane dynamicznie. Brama sieci VPN aktualnie obsługuje tylko *dynamiczne* przypisywanie publicznych adresów IP. Jednak nie oznacza to, że adres IP hello ulegnie zmianie po przypisaniu tooyour bramy sieci VPN. Hello czasu tylko zmiany adresu publicznego adresu IP hello jest po hello bramy zostanie usunięta i utworzona ponownie. Nie zmienia się on w przypadku zmiany rozmiaru, zresetowania ani przeprowadzania innych wewnętrznych czynności konserwacyjnych bądź uaktualnień bramy sieci VPN.

    - Najpierw kliknij **publicznego adresu IP** tooopen hello bloku "Wybierz publiczny adres IP", a następnie kliknij przycisk **+ Utwórz nowe** bloku "Tworzenie publicznego adresu IP" hello tooopen.
    - Następnie wprowadź **nazwa** dla publicznego adresu IP, następnie kliknij przycisk **OK** na hello dolnej części tego bloku toosave zmiany.

      ![Tworzenie publicznego adresu IP](./media/vpn-gateway-add-gw-s2s-rm-portal-include/pip.png "Tworzenie adresu PIP")

4. Sprawdź ustawienia hello. Możesz wybrać **toodashboard numeru Pin** u dołu bloku hello, jeśli chcesz, aby Twoje tooappear bramy na pulpicie nawigacyjnym hello hello. 
5. Kliknij przycisk **Utwórz** toobegin tworzenie hello bramy sieci VPN. Ustawienia Hello zostaną zweryfikowane, i zobaczysz hello Kafelek "Wdrażanie bramy sieci wirtualnej" na powitania pulpitu nawigacyjnego. Tworzenie bramy może potrwać too45 minut. Toorefresh może być konieczne stan ukończyć powitalnych toosee strony portalu.

Po utworzeniu bramy hello wyświetlić hello adres IP, który został przypisany tooit analizując hello sieci wirtualnej w portalu hello. Witaj brama będzie widoczna jako urządzenie podłączone. Możesz kliknąć hello podłączone urządzenia (bramy sieci wirtualnej) tooview więcej informacji.
