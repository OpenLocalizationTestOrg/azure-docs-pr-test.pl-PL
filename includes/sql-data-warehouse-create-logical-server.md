### <a name="create-a-new-logical-sql-server-in-the-azure-portal"></a><span data-ttu-id="76d7f-101">Tworzenie nowego serwera logicznego SQL w witrynie Azure Portal</span><span class="sxs-lookup"><span data-stu-id="76d7f-101">Create a new logical SQL server in the Azure portal</span></span>

1. <span data-ttu-id="76d7f-102">Kliknij pozycję **Nowy**, wyszukaj **serwer logiczny**, a następnie naciśnij klawisz **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="76d7f-102">Click **New**, search **logical server**, and then hit **ENTER**.</span></span>

    ![wyszukiwanie serwera logicznego](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. <span data-ttu-id="76d7f-104">Wybierz pozycję **SQL Server (serwer logiczny)**.</span><span class="sxs-lookup"><span data-stu-id="76d7f-104">Select **SQL server (logical server)**</span></span> 

    ![wybieranie serwera logicznego](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. <span data-ttu-id="76d7f-106">Kliknij pozycję **Utwórz**, aby otworzyć nowy blok SQL Server (serwer logiczny).</span><span class="sxs-lookup"><span data-stu-id="76d7f-106">Click **Create** to open the new SQL Server (logical server) blade.</span></span>

   <span data-ttu-id="76d7f-107"><kbd>![Otwórz blok serwera logicznego](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![blok serwera logicznego](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd></span><span class="sxs-lookup"><span data-stu-id="76d7f-107"><kbd> ![open logical server blade](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd>![logical server blade](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png) </kbd></span></span>
  
3. <span data-ttu-id="76d7f-108">W polu tekstowym nazwy serwera w bloku SQL Server (serwer logiczny) podaj prawidłową nazwę nowego serwera logicznego.</span><span class="sxs-lookup"><span data-stu-id="76d7f-108">In the SQL Server (logical server) blade's server name text box, provide a valid name for the new logical server.</span></span> <span data-ttu-id="76d7f-109">Zielony znacznik wyboru wskazuje, czy podana nazwa jest poprawna.</span><span class="sxs-lookup"><span data-stu-id="76d7f-109">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![nazwa nowego serwera](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > <span data-ttu-id="76d7f-111">W pełni kwalifikowana nazwa nowego serwera to <Twoja_nazwa_serwera>.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="76d7f-111">The fully qualified name for your new server will be <your_server_name>.database.windows.net.</span></span>
    >
    
4. <span data-ttu-id="76d7f-112">W polu tekstowym Identyfikator logowania administratora serwera podaj nazwę użytkownika na potrzeby logowania w celu uwierzytelniania SQL dla tego serwera.</span><span class="sxs-lookup"><span data-stu-id="76d7f-112">In the Server admin login text box, provide a user name for the SQL authentication login for this server.</span></span> <span data-ttu-id="76d7f-113">Ta nazwa logowania jest nazywana główną nazwą logowania serwera.</span><span class="sxs-lookup"><span data-stu-id="76d7f-113">This login is known as the server principal login.</span></span> <span data-ttu-id="76d7f-114">Zielony znacznik wyboru wskazuje, czy podana nazwa jest poprawna.</span><span class="sxs-lookup"><span data-stu-id="76d7f-114">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![identyfikator logowania administratora SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. <span data-ttu-id="76d7f-116">W polach tekstowych **Hasło** i **Potwierdź hasło** podaj hasło do głównego konta logowania serwera.</span><span class="sxs-lookup"><span data-stu-id="76d7f-116">In the **Password** and **Confirm password** text boxes, provide a password for the server principal login account.</span></span> <span data-ttu-id="76d7f-117">Zielony znacznik wyboru wskazuje, czy podane hasło jest poprawne.</span><span class="sxs-lookup"><span data-stu-id="76d7f-117">A green check mark indicates that you have provided a valid password.</span></span>
    
    ![Hasło administratora SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. <span data-ttu-id="76d7f-119">Wybierz subskrypcję, w której masz uprawnienia do tworzenia obiektów.</span><span class="sxs-lookup"><span data-stu-id="76d7f-119">Select a subscription in which you have permission to create objects.</span></span>

    ![subskrypcja](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. <span data-ttu-id="76d7f-121">W polu tekstowym Grupa zasobów wybierz opcję **Utwórz nową**, a następnie w polu tekstowym Grupa zasobów podaj prawidłową nazwę nowej grupy (możesz także użyć istniejącej grupy zasobów, jeśli masz już taką utworzoną na własne potrzeby).</span><span class="sxs-lookup"><span data-stu-id="76d7f-121">In the Resource group text box, select **Create new** and then, in the resource group text box, provide a valid name for the new resource group (you can also use an existing resource group if you have already created one for yourself).</span></span> <span data-ttu-id="76d7f-122">Zielony znacznik wyboru wskazuje, czy podana nazwa jest poprawna.</span><span class="sxs-lookup"><span data-stu-id="76d7f-122">A green check mark indicates that you have provided a valid name.</span></span>

    ![nowa grupa zasobów](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. <span data-ttu-id="76d7f-124">W polu tekstowym **Lokalizacja** wybierz centrum danych odpowiednie dla danej lokalizacji — np. „Australia Wschodnia”.</span><span class="sxs-lookup"><span data-stu-id="76d7f-124">In the **Location** text box, select a data center appropriate to your location - such as "Australia East".</span></span>
    
    ![lokalizacja serwera](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > <span data-ttu-id="76d7f-126">W tym bloku nie można zmienić pola wyboru dla opcji **Zezwalaj usługom platformy Azure na dostęp do serwera**.</span><span class="sxs-lookup"><span data-stu-id="76d7f-126">The checkbox for **Allow azure services to access server** cannot be changed on this blade.</span></span> <span data-ttu-id="76d7f-127">To ustawienie można zmienić w bloku zapory serwera.</span><span class="sxs-lookup"><span data-stu-id="76d7f-127">You can change this setting on the server firewall blade.</span></span> <span data-ttu-id="76d7f-128">Aby uzyskać więcej informacji, zobacz artykuł [Wprowadzenie do zabezpieczeń](../articles/sql-database/sql-database-manage-servers-portal.md).</span><span class="sxs-lookup"><span data-stu-id="76d7f-128">For more information, see [Get started with security](../articles/sql-database/sql-database-manage-servers-portal.md).</span></span>
    >
    
9. <span data-ttu-id="76d7f-129">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="76d7f-129">Click **Create**.</span></span>

    ![przycisk Utwórz](./media/sql-data-warehouse-create-logical-server/create.png)

