W tym kroku ręcznie utworzyć hello odbiornika grupy dostępności w Menedżerze klastra trybu Failover i SQL Server Management Studio.

1. Otwórz Menedżera klastra pracy awaryjnej z węzła hello, który obsługuje replikę podstawową hello.

2. Wybierz hello **sieci** węzła i nazwa sieciowa klastra hello Uwaga. Ta nazwa jest używana w zmiennej hello $ClusterNetworkName w hello skrypt programu PowerShell.

3. Rozwiń nazwę klastra hello, a następnie kliknij przycisk **ról**.

4. W hello **ról** okienku, kliknij prawym przyciskiem myszy hello grupy dostępności nazwy, a następnie wybierz **dodawania zasobów** > **punktu dostępu klienta**.
   
    ![Dodaj punkt dostępu klienta dla grupy dostępności](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. W hello **nazwa** , Utwórz nazwę dla tego nowego odbiornika kliknij pozycję **dalej** dwa razy, a następnie kliknij przycisk **Zakończ**.  
    Nie powodują odbiornika hello lub zasób w tryb online w tym momencie.

6. Kliknij przycisk hello **zasobów** karcie, a następnie rozwiń punktu dostępu klienta na powitania właśnie utworzony. 
    zostanie wyświetlony Hello zasobu adresu IP dla każdej sieci klastra w klastrze. Jeśli jest to rozwiązanie tylko do platformy Azure, zostanie wyświetlony tylko jeden zasób adres IP.

7. Wykonaj jedną z następujących hello:
   
   * tooconfigure hybrydowego rozwiązania:
     
        a. Kliknij prawym przyciskiem myszy zasób adresu IP hello odpowiadający tooyour podsieci lokalnej, a następnie wybierz **właściwości**. Zanotuj nazwę adresów IP hello i nazwa sieci.
   
        b. Wybierz **statyczny adres IP**Przypisz nieużywany adres IP, a następnie kliknij przycisk **OK**.
 
   * tooconfigure rozwiązania tylko do platformy Azure:

        a. Kliknij prawym przyciskiem myszy zasób hello adresu IP, który odpowiada tooyour podsieci platformy Azure, a następnie wybierz **właściwości**.
       
       > [!NOTE]
       > Jeśli odbiornik hello później nie toocome online ze względu na konflikt adresu IP wybrana przez serwer DHCP, w tym oknie właściwości można skonfigurować statyczny adres IP.
       > 
       > 

       b. W hello sam **adres IP** okna właściwości, zmień hello **nazwa adresu IP**.  
        Ta nazwa jest używana zmienna hello $IPResourceName hello skrypt programu PowerShell. Jeśli rozwiązanie obejmuje wiele sieci wirtualnych platformy Azure, powtórz ten krok dla każdego zasobu adresu IP.

