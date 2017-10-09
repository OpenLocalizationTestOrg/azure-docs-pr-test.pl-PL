1. Podczas połączenia toohello maszyny wirtualnej przy użyciu pulpitu zdalnego, wyszukaj **programu Configuration Manager**:

    ![Otwieranie Menedżera konfiguracji programu SQL Server](./media/virtual-machines-sql-server-connection-tcp-protocol/sql-server-configuration-manager.png)

1. W programie SQL Server Configuration Manager w okienku konsoli hello rozwiń **konfigurację sieci programu SQL Server**.

1. W okienku konsoli powitania kliknij **protokoły dla elementu MSSQLSERVER** (nazwa wystąpienia domyślnego hello). W okienku szczegółów hello, kliknij prawym przyciskiem myszy **TCP** i kliknij przycisk **włączyć** Jeśli nie jest już włączona.

    ![Włączanie protokołu TCP](./media/virtual-machines-sql-server-connection-tcp-protocol/enable-tcp.png)

1. W okienku konsoli powitania kliknij **usług SQL Server**. W okienku szczegółów hello, kliknij prawym przyciskiem myszy  **programu SQL Server (*nazwa wystąpienia*) ** (wystąpienie domyślne hello jest **programu SQL Server (MSSQLSERVER)**), a następnie kliknij przycisk **ponownego uruchomienia** , toostop i ponownie uruchom hello wystąpienie programu SQL Server.

    ![Ponowne uruchamianie aparatu bazy danych](./media/virtual-machines-sql-server-connection-tcp-protocol/restart-sql-server.png)

1. Zamknij Menedżera konfiguracji programu SQL Server.

Aby uzyskać więcej informacji na temat włączania protokołów hello aparatu bazy danych programu SQL Server, zobacz [włączyć lub wyłączyć protokół sieciowy serwera](http://msdn.microsoft.com/library/ms191294.aspx).
