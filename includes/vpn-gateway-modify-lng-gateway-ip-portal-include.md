### <a name="gwipnoconnection"></a>adres IP sieci lokalnej bramy toomodify hello — Brak połączenia bramy

Użyj toomodify przykład hello bramy sieci lokalnej, która nie ma połączenia bramy. Podczas modyfikowania tej wartości, można również zmodyfikować prefiksy adresów hello na powitania tym samym czasie.

1. Na powitania zasobu bramy sieci lokalnej w hello **ustawienia** kliknij **konfiguracji**.
2. W hello **adres IP** zmodyfikuj hello adresu IP.
3. Kliknij przycisk **zapisać** toosave hello ustawienia.

### <a name="gwipwithconnection"></a>toomodify hello sieci lokalnej bramy adres IP bramy - istniejące połączenie z bramą

toomodify bramy sieci lokalnej, która ma połączenie, należy toofirst Usuń hello połączenia. Po usunięciu hello połączenia można zmodyfikować adres IP bramy hello i utworzyć nowe połączenie. Można również zmodyfikować prefiksy adresów hello na powitania tym samym czasie. Spowoduje to pewien przestój połączenia sieci VPN. Podczas modyfikowania adres IP bramy hello, nie potrzebujesz bramy sieci VPN hello toodelete. Wystarczy tooremove hello połączenia.
 
#### <a name="1-remove-hello-connection"></a>1. Usuń połączenie hello.

1. Na powitania zasobu bramy sieci lokalnej w hello **ustawienia** kliknij **połączenia**.
2. Kliknij przycisk hello **...**  w wierszu hello hello połączenia, następnie kliknij przycisk **usunąć**.
3. Kliknij przycisk **zapisać** toosave ustawień.

#### <a name="2-modify-hello-ip-address"></a>2. Zmodyfikuj hello adresu IP.

Można również zmodyfikować prefiksy adresów hello na powitania tym samym czasie.

1. W hello **adres IP** zmodyfikuj hello adresu IP.
2. Kliknij przycisk **zapisać** toosave hello ustawienia.

#### <a name="3-recreate-hello-connection"></a>3. Utwórz ponownie połączenie hello.

1. Przejdź toohello Brama sieci wirtualnej sieci wirtualnej. (Nie hello bramy sieci lokalnej.)
2. Na powitania Brama sieci wirtualnej w hello **ustawienia** kliknij **połączenia**.
3. Kliknij przycisk hello **+ Dodaj** tooopen hello **Dodaj połączenie** bloku.
4. Utwórz ponownie połączenie.
5. Kliknij przycisk **OK** toocreate hello połączenia.
