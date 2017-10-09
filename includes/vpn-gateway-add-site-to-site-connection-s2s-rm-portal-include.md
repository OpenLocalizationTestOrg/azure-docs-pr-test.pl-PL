1. Przejdź tooand hello Otwórz blok dla bramy sieci wirtualnej. Istnieje wiele sposobów toonavigate. W naszym przykładzie mamy przejście bramy toohello "VNet1GW" przechodząc zbyt**TestVNet1 -> Przegląd -> połączone urządzenia -> VNet1GW**.
2. W bloku hello VNet1GW, kliknij **połączenia**. U góry hello hello połączeń bloku, kliknij przycisk **+ Dodaj** tooopen hello **Dodaj połączenie** bloku.

    ![Utwórz połączenie lokacja-lokacja](./media/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include/connection1.png)

3. Na powitania **Dodaj połączenie** bloku, wypełnij hello wartości toocreate połączenia.

  - **Nazwa:** nazwij połączenie. W tym przykładzie użyto nazwy **VNet1toSite2**.
  - **Typ połączenia:** wybierz pozycję **lokacja-lokacja(IPSec)**.
  - **Brama sieci wirtualnej:** hello wartość jest ustalona, ponieważ jest nawiązywane z tej bramy.
  - **Brama sieci lokalnej:** kliknij **wybierz bramę sieci lokalnej** i wybierz hello bramy sieci lokalnej, które mają toouse. W tym przykładzie użyto bramy **Site2**.
  - **Klucz współużytkowany:** hello wartość musi odpowiadać wartości hello używasz lokalnych lokalnego urządzenia sieci VPN. Przykład Witaj użyliśmy "abc123", ale można i powinien używasz bardziej złożonych. Witaj ważne, czy element jest daną hello określone w tym miejscu musi być powitalne samą wartość, że zostało określone podczas konfigurowania urządzenia sieci VPN.
  - Witaj pozostałych wartości **subskrypcji**, **grupy zasobów**, i **lokalizacji** zostały usunięte.

4. Kliknij przycisk **OK** toocreate połączenia. Zobaczysz *Tworzenie połączenia* flash na ekranie powitania.
5. Witaj połączenia można wyświetlić w hello **połączeń** bloku hello bramy sieci wirtualnej. Witaj stan zmieni się z *nieznany* za*łączenie*, a następnie zbyt*zakończyło się pomyślnie*.
