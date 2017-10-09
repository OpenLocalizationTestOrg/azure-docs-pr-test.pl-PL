
<!--
includes/sql-database-create-new-server-firewall-portal.md

Latest Freshness check:  2016-11-28 , rickbyh.

As of circa 2016-04-11, hello following topics might include this include:
articles/sql-database/sql-database-get-started.md
articles/sql-database/sql-database-configure-firewall-settings
articles/sql-data-warehouse-get-started-provision.md

-->
### <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="908c6-101">Utworzyć regułę zapory poziomu serwera w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="908c6-101">Create a server-level firewall rule in hello Azure portal</span></span>

1. <span data-ttu-id="908c6-102">W bloku serwera SQL hello, w obszarze Ustawienia, kliknij polecenie **zapory** tooopen hello zapory bloku dla hello programu SQL server.</span><span class="sxs-lookup"><span data-stu-id="908c6-102">On hello SQL server blade, under Settings, click **Firewall** tooopen hello Firewall blade for hello SQL server.</span></span>

    <!-- ![sql server firewall](../articles/sql-database/media/sql-database-get-started/sql-server-firewall.png) -->

2. <span data-ttu-id="908c6-103">Przejrzyj wyświetlony adres IP powitania klienta i sprawdzić, czy jest to adres IP na powitania Internet za pomocą przeglądarki wybranych przez użytkownika (zapytaj "co to jest adresu IP).</span><span class="sxs-lookup"><span data-stu-id="908c6-103">Review hello client IP address displayed and validate that this is your IP address on hello Internet using a browser of your choice (ask "what is my IP address).</span></span> <span data-ttu-id="908c6-104">Czasami te adresy nie zgadzają się z różnych powodów.</span><span class="sxs-lookup"><span data-stu-id="908c6-104">Occasionally they do not match for a various reasons.</span></span>

    <!-- ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png) -->

3. <span data-ttu-id="908c6-105">Przy założeniu, że adresy IP hello zgodne, kliknij przycisk **Dodaj adres IP klienta** na powitania narzędzi.</span><span class="sxs-lookup"><span data-stu-id="908c6-105">Assuming that hello IP addresses match, click **Add client IP** on hello toolbar.</span></span>

    ![dodawanie adresu IP klienta](../articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/add-client-ip.png)

    > [!NOTE]
    > <span data-ttu-id="908c6-107">Można otworzyć zapory bazy danych SQL hello na powitania tooa pojedynczy adres IP serwera lub całego zakresu adresów.</span><span class="sxs-lookup"><span data-stu-id="908c6-107">You can open hello SQL Database firewall on hello server tooa single IP address or an entire range of addresses.</span></span> <span data-ttu-id="908c6-108">Otwieranie hello zapory umożliwia administratorom SQL i bazy danych tooany toologin użytkowników na hello toowhich serwera mają prawidłowe poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="908c6-108">Opening hello firewall enables SQL administrators and users toologin tooany database on hello server toowhich they have valid credentials.</span></span>
    >

4. <span data-ttu-id="908c6-109">Kliknij przycisk **zapisać** na hello toosave narzędzi tę regułę zapory poziomu serwera, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="908c6-109">Click **Save** on hello toolbar toosave this server-level firewall rule and then click **OK**.</span></span>

    ![dodawanie adresu IP klienta](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png)

> [!Tip]
> <span data-ttu-id="908c6-111">Aby zapoznać się z samouczkiem, zobacz artykuł [Samouczek usługi SQL Database: tworzenie serwera, reguły zapory na poziomie serwera, przykładowej bazy danych i reguły zapory na poziomie bazy danych oraz nawiązywanie połączenia z programem SQL Server](../articles/sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="908c6-111">For a tutorial, see [SQL Database tutorial: Create a server, a server-level firewall rule, a sample database, a database-level firewall rule and connect with SQL Server](../articles/sql-database/sql-database-get-started.md).</span></span>    
>
