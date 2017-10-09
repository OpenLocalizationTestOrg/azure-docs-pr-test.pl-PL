
<!--
includes/sql-database-create-new-server-firewall-portal.md

Latest Freshness check:  2016-11-28 , rickbyh.

As of circa 2016-04-11, hello following topics might include this include:
articles/sql-database/sql-database-get-started.md
articles/sql-database/sql-database-configure-firewall-settings
articles/sql-data-warehouse-get-started-provision.md

-->
### <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Utworzyć regułę zapory poziomu serwera w hello portalu Azure

1. W bloku serwera SQL hello, w obszarze Ustawienia, kliknij polecenie **zapory** tooopen hello zapory bloku dla hello programu SQL server.

    <!-- ![sql server firewall](../articles/sql-database/media/sql-database-get-started/sql-server-firewall.png) -->

2. Przejrzyj wyświetlony adres IP powitania klienta i sprawdzić, czy jest to adres IP na powitania Internet za pomocą przeglądarki wybranych przez użytkownika (zapytaj "co to jest adresu IP). Czasami te adresy nie zgadzają się z różnych powodów.

    <!-- ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png) -->

3. Przy założeniu, że adresy IP hello zgodne, kliknij przycisk **Dodaj adres IP klienta** na powitania narzędzi.

    ![dodawanie adresu IP klienta](../articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/add-client-ip.png)

    > [!NOTE]
    > Można otworzyć zapory bazy danych SQL hello na powitania tooa pojedynczy adres IP serwera lub całego zakresu adresów. Otwieranie hello zapory umożliwia administratorom SQL i bazy danych tooany toologin użytkowników na hello toowhich serwera mają prawidłowe poświadczenia.
    >

4. Kliknij przycisk **zapisać** na hello toosave narzędzi tę regułę zapory poziomu serwera, a następnie kliknij przycisk **OK**.

    ![dodawanie adresu IP klienta](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png)

> [!Tip]
> Aby zapoznać się z samouczkiem, zobacz artykuł [Samouczek usługi SQL Database: tworzenie serwera, reguły zapory na poziomie serwera, przykładowej bazy danych i reguły zapory na poziomie bazy danych oraz nawiązywanie połączenia z programem SQL Server](../articles/sql-database/sql-database-get-started.md).    
>
