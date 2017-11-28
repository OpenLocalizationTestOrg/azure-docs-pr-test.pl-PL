
<!--
includes/sql-database-create-new-server-firewall-portal.md

Latest Freshness check:  2016-11-28 , rickbyh.

As of circa 2016-04-11, the following topics might include this include:
articles/sql-database/sql-database-get-started.md
articles/sql-database/sql-database-configure-firewall-settings
articles/sql-data-warehouse-get-started-provision.md

-->
### <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="45f46-101">Tworzenie reguły zapory na poziomie serwera w witrynie Azure Portal</span><span class="sxs-lookup"><span data-stu-id="45f46-101">Create a server-level firewall rule in the Azure portal</span></span>

1. <span data-ttu-id="45f46-102">W bloku serwera SQL, w obszarze Ustawienia, kliknij pozycję **Zapora**, aby otworzyć blok Zapora dla serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="45f46-102">On the SQL server blade, under Settings, click **Firewall** to open the Firewall blade for the SQL server.</span></span>

    <!-- ![sql server firewall](../articles/sql-database/media/sql-database-get-started/sql-server-firewall.png) -->

2. <span data-ttu-id="45f46-103">Sprawdź wyświetlony adres IP klienta i przy użyciu wybranej przeglądarki zweryfikuj w Internecie, czy jest to Twój adres IP (zadaj pytanie „jaki jest mój adres IP”).</span><span class="sxs-lookup"><span data-stu-id="45f46-103">Review the client IP address displayed and validate that this is your IP address on the Internet using a browser of your choice (ask "what is my IP address).</span></span> <span data-ttu-id="45f46-104">Czasami te adresy nie zgadzają się z różnych powodów.</span><span class="sxs-lookup"><span data-stu-id="45f46-104">Occasionally they do not match for a various reasons.</span></span>

    <!-- ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png) -->

3. <span data-ttu-id="45f46-105">Zakładając, że adresy IP się zgadzają, na pasku narzędzi kliknij pozycję **Dodaj adres IP klienta**.</span><span class="sxs-lookup"><span data-stu-id="45f46-105">Assuming that the IP addresses match, click **Add client IP** on the toolbar.</span></span>

    ![dodawanie adresu IP klienta](../articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/add-client-ip.png)

    > [!NOTE]
    > <span data-ttu-id="45f46-107">Zaporę usługi SQL Database możesz otworzyć na serwerze dla pojedynczego adresu IP lub dla całego zakresu adresów.</span><span class="sxs-lookup"><span data-stu-id="45f46-107">You can open the SQL Database firewall on the server to a single IP address or an entire range of addresses.</span></span> <span data-ttu-id="45f46-108">Otwarcie zapory umożliwia administratorom SQL i użytkownikom logowanie się do dowolnej bazy danych na serwerze, dla którego mają prawidłowe poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="45f46-108">Opening the firewall enables SQL administrators and users to login to any database on the server to which they have valid credentials.</span></span>
    >

4. <span data-ttu-id="45f46-109">Kliknij pozycję **Zapisz** na pasku narzędzi, aby zapisać tę regułę zapory na poziomie serwera, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="45f46-109">Click **Save** on the toolbar to save this server-level firewall rule and then click **OK**.</span></span>

    ![dodawanie adresu IP klienta](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png)

> [!Tip]
> <span data-ttu-id="45f46-111">Aby zapoznać się z samouczkiem, zobacz artykuł [Samouczek usługi SQL Database: tworzenie serwera, reguły zapory na poziomie serwera, przykładowej bazy danych i reguły zapory na poziomie bazy danych oraz nawiązywanie połączenia z programem SQL Server](../articles/sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="45f46-111">For a tutorial, see [SQL Database tutorial: Create a server, a server-level firewall rule, a sample database, a database-level firewall rule and connect with SQL Server](../articles/sql-database/sql-database-get-started.md).</span></span>    
>
