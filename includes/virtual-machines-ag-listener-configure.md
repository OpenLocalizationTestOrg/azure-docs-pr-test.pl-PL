odbiornik grupy dostępności Hello jest adresu IP i sieci nazwy który hello nasłuchuje grupy dostępności programu SQL Server. odbiornik grupy dostępności hello toocreate hello następujące:

1. <a name="getnet"></a>Pobierz nazwę zasobu sieciowego klastra hello hello.

    a. Za pomocą protokołu RDP tooconnect toohello maszyny wirtualnej platformy Azure, który obsługuje replikę podstawową hello. 

    b. Otwórz Menedżera klastra pracy awaryjnej.

    c. Wybierz hello **sieci** węzeł i nazwa sieciowa klastra hello Uwaga. Ta nazwa jest używana w hello `$ClusterNetworkName` zmiennej w hello skrypt programu PowerShell. W hello następujące nazwy sieciowej klastra hello obrazu jest **1 sieci klastra**:

   ![Nazwa sieciowa klastra](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <a name="addcap"></a>Dodaj punkt dostępu klienta hello.  
    punkt dostępu klienta Hello jest nazwą sieci hello czy aplikacje używają tooconnect toohello z baz danych w grupie dostępności. Utwórz punkt dostępu klienta hello w Menedżerze klastra trybu Failover.

    a. Rozwiń nazwę klastra hello, a następnie kliknij przycisk **ról**.

    b. W hello **ról** okienku, kliknij prawym przyciskiem myszy hello grupy dostępności nazwy, a następnie wybierz **dodawania zasobów** > **punktu dostępu klienta**.

   ![Punkt dostępu klienta](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    c. W hello **nazwa** Utwórz nazwę dla tego nowego odbiornika. 
   Nazwa Hello odbiornika nowe hello jest nazwa sieciowa hello czy aplikacje używają tooconnect toodatabases w grupie dostępności programu SQL Server hello.
   
    d. Tworzenie odbiornika hello toofinish, kliknij przycisk **dalej** dwa razy, a następnie kliknij przycisk **Zakończ**. Nie powodują odbiornika hello lub zasób w tryb online w tym momencie.

3. <a name="congroup"></a>Skonfiguruj hello IP zasobu dla grupy dostępności hello.

    a. Kliknij przycisk hello **zasobów** karcie, a następnie rozwiń punktu dostępu klienta na powitania został utworzony.  
    punkt dostępu klienta Hello jest w trybie offline.

   ![Punkt dostępu klienta](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    b. Kliknij prawym przyciskiem myszy hello IP zasobu, a następnie kliknij polecenie Właściwości. Zanotuj nazwę hello hello adresu IP i używać go w hello `$IPResourceName` zmiennej w hello skrypt programu PowerShell.

    c. W obszarze **adres IP**, kliknij przycisk **statyczny adres IP**. Ustaw adres IP hello hello sama adresu użyto po ustawieniu adres usługi równoważenia obciążenia hello na powitania portalu Azure.

   ![Zasób IP](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <a name = "dependencyGroup"></a>Skonfiguruj zasób grupy dostępności programu SQL Server hello zależał od punktu dostępu klienta hello.

    a. W Menedżerze klastra trybu Failover kliknij **ról**, a następnie kliknij przycisk grupy dostępności.

    b. Na powitania **zasobów** , w obszarze **inne zasoby**, kliknij prawym przyciskiem myszy grupę zasobów hello dostępności, a następnie kliknij przycisk **właściwości**. 

    c. Na karcie zależności hello Dodaj nazwę hello powitania klienta dostępu punktu (hello odbiornika) zasobu.

   ![Zasób IP](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    d. Kliknij przycisk **OK**.

5. <a name="listname"></a>Powitania klienta z dostępu do zasobów zależnych od adresu IP hello punktu.

    a. W Menedżerze klastra trybu Failover kliknij **ról**, a następnie kliknij przycisk grupy dostępności. 

    b. Na powitania **zasobów** karcie, kliknij prawym przyciskiem myszy powitania klienta dostępu punktu zasobów w obszarze **nazwy serwera**, a następnie kliknij przycisk **właściwości**. 

   ![Zasób IP](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    c. Kliknij przycisk hello **zależności** kartę. Sprawdź, czy adres IP hello zależności. Jeśli nie, należy ustawić zależność hello adresu IP. Jeśli istnieje wiele zasobów na liście, należy sprawdzić, czy adresy IP hello mają lub nie oraz zależności. Kliknij przycisk **OK**. 

   ![Zasób IP](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    d. Kliknij prawym przyciskiem myszy nazwę odbiornika hello, a następnie kliknij przycisk **przejdź do trybu Online**. 

    >[!TIP]
    >Można sprawdzić poprawność tej hello zależności są poprawnie skonfigurowane. W Menedżerze klastra trybu Failover Przejdź tooRoles, kliknij prawym przyciskiem myszy hello grupy dostępności, kliknij przycisk **więcej akcji**, a następnie kliknij przycisk **Pokaż raport zależności**. Po hello zależności są poprawnie skonfigurowane, grupa dostępności hello jest zależna od nazwy sieciowej hello i nazwa sieciowa hello jest zależny od adresu IP hello. 


6. <a name="setparam"></a>Ustaw parametry klastra hello w programie PowerShell.
    
    a. Skopiuj powitania po tooone skrypt programu PowerShell z wystąpień programu SQL Server. Zaktualizuj zmienne hello w danym środowisku.     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
    $IPResourceName = "<IPResourceName>" # hello IP Address resource name
    $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    b. Ustaw parametry klastra hello uruchamiając hello skrypt programu PowerShell na jednym z węzłów klastra hello.  

    > [!NOTE]
    > Wystąpienia programu SQL Server znajdują się w oddzielnych regionach, należy najpierw skrypt programu PowerShell hello toorun dwa razy. Witaj po raz pierwszy, należy użyć hello `$ILBIP` i `$ProbePort` z hello pierwszy regionu. Witaj po raz drugi, użyj hello `$ILBIP` i `$ProbePort` z hello drugi regionu. Nazwa sieciowa klastra Hello i nazwa zasobu IP klastra hello są hello tego samego. 
