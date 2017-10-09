### <a name="configure-a-dns-label-for-hello-public-ip-address"></a>Konfigurowanie etykiety DNS dla publicznego adresu IP hello

tooconnect toohello aparatu bazy danych programu SQL Server z hello Internet, należy wziąć pod uwagę tworzenia etykiety DNS dla publicznego adresu IP. Możesz połączyć za pomocą adresu IP, ale hello Etykieta DNS tworzy rekord A, który jest łatwiejsze tooidentify i streszczenia hello podstawowej publicznego adresu IP.

> [!NOTE]
> Etykiety DNS nie są wymagane, jeśli plan tooonly połączyć toohello programu SQL Server wystąpienie w ramach hello sam sieci wirtualnej lub tylko lokalnie.

Najpierw wybierz etykietę DNS toocreate **maszyn wirtualnych** w portalu hello. Wybierz sieci maszyny Wirtualnej programu SQL Server toobring jej właściwości.

1. Omówienie maszyny wirtualnej hello, wybierz użytkownika **publicznego adresu IP**.

    ![publiczny adres IP](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. W właściwości hello publicznego adresu IP, rozwiń węzeł **konfiguracji**.

1. Wprowadź nazwę etykiety DNS. Ta nazwa jest rekord A, które mogą być używane tooconnect tooyour maszyny Wirtualnej programu SQL Server przy użyciu nazwy za pomocą adresu IP bezpośrednio.

1. Kliknij przycisk hello **zapisać** przycisku.

    ![etykieta DNS](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a>Połącz toohello aparatu bazy danych z innego komputera

1. Na komputerze połączone toohello internet, Otwórz program SQL Server Management Studio (SSMS). Jeśli nie masz programu SQL Server Management Studio, możesz pobrać go [tutaj](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

1. W hello **połączyć tooServer** lub **połączyć tooDatabase aparat** okno dialogowe, Edytuj hello **nazwy serwera** wartość. Wprowadź adres IP hello lub pełną nazwę DNS hello maszyny wirtualnej (określoną w poprzednim zadaniu hello). Możesz także dodać przecinek i podać port TCP programu SQL Server. Na przykład `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.

1. W hello **uwierzytelniania** wybierz opcję **uwierzytelniania programu SQL Server**.

1. W hello **logowania** okno, nazwa typu hello umożliwiające prawidłowe logowanie SQL.

1. W hello **hasło** okno, wpisz hasło hello hello logowania.

1. Kliknij przycisk **Połącz**.

    ![nawiązywanie połączenia w programie ssms](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)