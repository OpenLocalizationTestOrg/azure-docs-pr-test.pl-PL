### <a name="determine-hello-dns-name-of-hello-virtual-machine"></a>Określić nazwy DNS hello hello maszyny wirtualnej
tooconnect toohello aparatu bazy danych programu SQL Server z innego komputera, musisz znać hello systemu nazw domen (DNS, Domain Name System) nazwa hello maszyny wirtualnej. (Jest to hello nazwa hello internet używa tooidentify hello wirtualnej maszyny. Możesz użyć adresu IP hello, ale hello adresu IP mogą ulec zmianie, gdy Azure przenosi zasoby nadmiarowość lub konserwacji. Nazwa DNS Hello będzie stabilny, ponieważ może być przekierowywane tooa nowego adresu IP.)  

1. W portalu Azure hello (lub hello w poprzednim kroku), wybierz **maszyn wirtualnych (klasyczne)**.
2. Wybierz maszynę Wirtualną programu SQL.
3. Na powitania **maszyny wirtualnej** bloku, hello kopiowania **nazwy DNS** hello maszyny wirtualnej.
   
    ![Nazwa DNS](./media/virtual-machines-sql-server-connection-steps/sql-vm-dns-name.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a>Połącz toohello aparatu bazy danych z innego komputera
1. Na komputerze połączone toohello internet, Otwórz program SQL Server Management Studio.
2. W hello **połączyć tooServer** lub **połączyć tooDatabase aparat** okno dialogowe, w hello **nazwy serwera** wpisz nazwę DNS hello hello maszyny wirtualnej (określoną w hello poprzednie zadanie) i numer portu publicznego punktu końcowego w formacie hello *DNSName, numer_portu* takich jak **mysqlvm.cloudapp.net,57500**.
   
    ![Połącz przy użyciu narzędzia SSMS](./media/virtual-machines-sql-server-connection-steps/33Connect-SSMS.png)
   
    Jeśli nie pamiętasz numeru portu publicznego punktu końcowego hello wcześniej utworzony, można go znaleźć w hello **punkty końcowe** obszaru hello **maszyny wirtualnej** bloku.
   
    ![Port publiczny](./media/virtual-machines-sql-server-connection-steps/sql-vm-port-number.png)
3. W hello **uwierzytelniania** wybierz opcję **uwierzytelniania programu SQL Server**.
4. W hello **logowania** okno, nazwa typu hello logowania, utworzony w starszej zadań.
5. W hello **hasło** okno, wpisz hasło hello hello logowania, utworzone w wcześniejszych zadań.
6. Kliknij przycisk **Połącz**.

