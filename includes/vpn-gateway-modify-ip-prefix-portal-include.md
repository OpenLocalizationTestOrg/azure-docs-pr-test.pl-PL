### <a name="noconnection"></a>prefiksy adresów brama IP toomodify sieci lokalnej — Brak połączenia bramy

#### <a name="tooadd-additional-address-prefixes"></a>tooadd dodatkowe prefiksy adresów:

1. Na powitania zasobu bramy sieci lokalnej w hello **ustawienia** kliknij **konfiguracji**.
2. Dodawanie przestrzeni adresów IP hello w hello *Dodaj dodatkowy zakres adresów* pole.
3. Kliknij przycisk **zapisać** toosave ustawień.

#### <a name="tooremove-address-prefixes"></a>tooremove prefiksy adresów:

1. Na powitania zasobu bramy sieci lokalnej w hello **ustawienia** kliknij **konfiguracji**.
2. Kliknij przycisk hello **"..."** na powitania wiersz zawierający prefiks hello ma tooremove.
3. Kliknij przycisk **Usuń**.
4. Kliknij przycisk **zapisać** toosave ustawień.

### <a name="withconnection"></a>toomodify sieci lokalnej bramy prefiksów adresów IP - istniejące połączenie z bramą

Połączenie bramy i mają tooadd lub usunąć prefiksy adresów IP hello zawarte w bramie sieci lokalnej, należy najpierw hello toodo następujące kroki w kolejności. Spowoduje to pewien przestój połączenia sieci VPN. Podczas modyfikowania prefiksów adresów IP, nie potrzebujesz bramy sieci VPN hello toodelete. Wystarczy tooremove hello połączenia.

#### <a name="1-remove-hello-connection"></a>1. Usuń połączenie hello.

1. Na powitania zasobu bramy sieci lokalnej w hello **ustawienia** kliknij **połączenia**.
2. Kliknij przycisk hello **...**  hello wiersza dla każdego połączenia, następnie kliknij przycisk **usunąć**.
3. Kliknij przycisk **zapisać** toosave ustawień.

#### <a name="2-modify-hello-address-prefixes"></a>2. Zmodyfikuj prefiksy adresów hello.

tooadd dodatkowe prefiksy adresów:

1. Na powitania zasobu bramy sieci lokalnej w hello **ustawienia** kliknij **konfiguracji**.
2. Dodawanie przestrzeni adresów IP hello.
3. Kliknij przycisk **zapisać** toosave ustawień.

tooremove prefiksy adresów:

1. Na powitania zasobu bramy sieci lokalnej w hello **ustawienia** kliknij **konfiguracji**.
2. Kliknij przycisk hello **...**  na powitania wiersz zawierający prefiks hello ma tooremove.
3. Kliknij przycisk **Usuń**.
4. Kliknij przycisk **zapisać** toosave ustawień.

#### <a name="3-recreate-hello-connection"></a>3. Utwórz ponownie połączenie hello.

1. Przejdź toohello Brama sieci wirtualnej sieci wirtualnej. (Nie hello bramy sieci lokalnej.)
2. Na powitania Brama sieci wirtualnej w hello **ustawienia** kliknij **połączenia**.
3. Kliknij przycisk hello **+ Dodaj** tooopen hello **Dodaj połączenie** bloku.
4. Utwórz ponownie połączenie.
5. Kliknij przycisk **OK** toocreate hello połączenia.
