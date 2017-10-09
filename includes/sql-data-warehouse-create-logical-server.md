### <a name="create-a-new-logical-sql-server-in-hello-azure-portal"></a><span data-ttu-id="5cdf4-101">Utwórz nowy serwer logiczny SQL w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5cdf4-101">Create a new logical SQL server in hello Azure portal</span></span>

1. <span data-ttu-id="5cdf4-102">Kliknij pozycję **Nowy**, wyszukaj **serwer logiczny**, a następnie naciśnij klawisz **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="5cdf4-102">Click **New**, search **logical server**, and then hit **ENTER**.</span></span>

    ![wyszukiwanie serwera logicznego](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. <span data-ttu-id="5cdf4-104">Wybierz pozycję **SQL Server (serwer logiczny)**.</span><span class="sxs-lookup"><span data-stu-id="5cdf4-104">Select **SQL server (logical server)**</span></span> 

    ![wybieranie serwera logicznego](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. <span data-ttu-id="5cdf4-106">Kliknij przycisk **Utwórz** tooopen hello nowy blok programu SQL Server (serwer logiczny).</span><span class="sxs-lookup"><span data-stu-id="5cdf4-106">Click **Create** tooopen hello new SQL Server (logical server) blade.</span></span>

   <span data-ttu-id="5cdf4-107"><kbd>![Otwórz blok serwera logicznego](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![blok serwera logicznego](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd></span><span class="sxs-lookup"><span data-stu-id="5cdf4-107"><kbd> ![open logical server blade](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd>![logical server blade](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png) </kbd></span></span>
  
3. <span data-ttu-id="5cdf4-108">W polu tekstowym Nazwa serwera bloku hello programu SQL Server (serwer logiczny) Podaj prawidłową nazwę dla nowego serwera logicznego hello.</span><span class="sxs-lookup"><span data-stu-id="5cdf4-108">In hello SQL Server (logical server) blade's server name text box, provide a valid name for hello new logical server.</span></span> <span data-ttu-id="5cdf4-109">Zielony znacznik wyboru wskazuje, czy podana nazwa jest poprawna.</span><span class="sxs-lookup"><span data-stu-id="5cdf4-109">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![nazwa nowego serwera](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > <span data-ttu-id="5cdf4-111">Witaj pełni kwalifikowaną nazwę dla nowego serwera będą < your_server_name >. database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="5cdf4-111">hello fully qualified name for your new server will be <your_server_name>.database.windows.net.</span></span>
    >
    
4. <span data-ttu-id="5cdf4-112">W polu tekstowym powitania serwera admin logowania Podaj nazwę użytkownika logowania uwierzytelniania SQL powitania dla tego serwera.</span><span class="sxs-lookup"><span data-stu-id="5cdf4-112">In hello Server admin login text box, provide a user name for hello SQL authentication login for this server.</span></span> <span data-ttu-id="5cdf4-113">Tę nazwę logowania jest określany jako powitania serwera głównego identyfikatora logowania.</span><span class="sxs-lookup"><span data-stu-id="5cdf4-113">This login is known as hello server principal login.</span></span> <span data-ttu-id="5cdf4-114">Zielony znacznik wyboru wskazuje, czy podana nazwa jest poprawna.</span><span class="sxs-lookup"><span data-stu-id="5cdf4-114">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![identyfikator logowania administratora SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. <span data-ttu-id="5cdf4-116">W hello **hasło** i **Potwierdź hasło** pola tekstowe, podaj hasło dla konta głównego identyfikatora logowania serwera hello.</span><span class="sxs-lookup"><span data-stu-id="5cdf4-116">In hello **Password** and **Confirm password** text boxes, provide a password for hello server principal login account.</span></span> <span data-ttu-id="5cdf4-117">Zielony znacznik wyboru wskazuje, czy podane hasło jest poprawne.</span><span class="sxs-lookup"><span data-stu-id="5cdf4-117">A green check mark indicates that you have provided a valid password.</span></span>
    
    ![Hasło administratora SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. <span data-ttu-id="5cdf4-119">Wybierz subskrypcję, w której masz uprawnienia toocreate obiektów.</span><span class="sxs-lookup"><span data-stu-id="5cdf4-119">Select a subscription in which you have permission toocreate objects.</span></span>

    ![subskrypcja](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. <span data-ttu-id="5cdf4-121">W polu tekstowym grupy zasobów hello wybierz **Utwórz nowy** , a następnie w polu tekstowym grupy zasobów hello, podaj prawidłową nazwę dla nowej grupy zasobów hello, (umożliwia także istniejącą grupę zasobów, jeśli został już utworzony dla siebie).</span><span class="sxs-lookup"><span data-stu-id="5cdf4-121">In hello Resource group text box, select **Create new** and then, in hello resource group text box, provide a valid name for hello new resource group (you can also use an existing resource group if you have already created one for yourself).</span></span> <span data-ttu-id="5cdf4-122">Zielony znacznik wyboru wskazuje, czy podana nazwa jest poprawna.</span><span class="sxs-lookup"><span data-stu-id="5cdf4-122">A green check mark indicates that you have provided a valid name.</span></span>

    ![nowa grupa zasobów](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. <span data-ttu-id="5cdf4-124">W hello **lokalizacji** pole tekstowe, wybierz danych Centrum lokalizacji odpowiednie tooyour — takie jak "Australia Wschodnia".</span><span class="sxs-lookup"><span data-stu-id="5cdf4-124">In hello **Location** text box, select a data center appropriate tooyour location - such as "Australia East".</span></span>
    
    ![lokalizacja serwera](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > <span data-ttu-id="5cdf4-126">Witaj wyboru **Zezwalaj usługom platformy azure tooaccess serwera** nie można zmienić tego bloku.</span><span class="sxs-lookup"><span data-stu-id="5cdf4-126">hello checkbox for **Allow azure services tooaccess server** cannot be changed on this blade.</span></span> <span data-ttu-id="5cdf4-127">Można zmienić to ustawienie na powitania serwera zapory bloku.</span><span class="sxs-lookup"><span data-stu-id="5cdf4-127">You can change this setting on hello server firewall blade.</span></span> <span data-ttu-id="5cdf4-128">Aby uzyskać więcej informacji, zobacz artykuł [Wprowadzenie do zabezpieczeń](../articles/sql-database/sql-database-manage-servers-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5cdf4-128">For more information, see [Get started with security](../articles/sql-database/sql-database-manage-servers-portal.md).</span></span>
    >
    
9. <span data-ttu-id="5cdf4-129">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5cdf4-129">Click **Create**.</span></span>

    ![przycisk Utwórz](./media/sql-data-warehouse-create-logical-server/create.png)

