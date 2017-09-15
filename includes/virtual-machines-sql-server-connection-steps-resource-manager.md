### <a name="configure-a-dns-label-for-the-public-ip-address"></a><span data-ttu-id="c2a55-101">Konfigurowanie etykiety DNS dla publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="c2a55-101">Configure a DNS Label for the public IP address</span></span>

<span data-ttu-id="c2a55-102">Aby połączyć się z aparatem bazy danych programu SQL Server z Internetu, rozważ utworzenie etykiety DNS dla publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="c2a55-102">To connect to the SQL Server Database Engine from the Internet, consider creating a DNS Label for your public IP address.</span></span> <span data-ttu-id="c2a55-103">Możesz połączyć się przy użyciu adresu IP, ale etykieta DNS tworzy rekord A, który jest łatwiejszy do zidentyfikowania i streszcza podstawowy publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="c2a55-103">You can connect by IP address, but the DNS Label creates an A Record that is easier to identify and abstracts the underlying public IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="c2a55-104">Etykiety DNS nie są wymagane, jeśli planujesz tylko połączenie z wystąpieniem programu SQL Server w ramach tej samej sieci wirtualnej lub połączenie lokalne.</span><span class="sxs-lookup"><span data-stu-id="c2a55-104">DNS Labels are not required if you plan to only connect to the SQL Server instance within the same Virtual Network or only locally.</span></span>

<span data-ttu-id="c2a55-105">Aby utworzyć etykietę DNS, wybierz najpierw **maszyny wirtualne** w portalu.</span><span class="sxs-lookup"><span data-stu-id="c2a55-105">To create a DNS Label, first select **Virtual machines** in the portal.</span></span> <span data-ttu-id="c2a55-106">Wybierz maszynę wirtualną programu SQL Server, aby wyświetlić jej właściwości.</span><span class="sxs-lookup"><span data-stu-id="c2a55-106">Select your SQL Server VM to bring up its properties.</span></span>

1. <span data-ttu-id="c2a55-107">W przeglądzie maszyny wirtualnej wybierz **publiczny adres IP**.</span><span class="sxs-lookup"><span data-stu-id="c2a55-107">In the virtual machine overview, select your **Public IP address**.</span></span>

    ![publiczny adres IP](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. <span data-ttu-id="c2a55-109">We właściwościach publicznego adresu IP rozwiń sekcję **Konfiguracja**.</span><span class="sxs-lookup"><span data-stu-id="c2a55-109">In the properties for your Public IP address, expand **Configuration**.</span></span>

1. <span data-ttu-id="c2a55-110">Wprowadź nazwę etykiety DNS.</span><span class="sxs-lookup"><span data-stu-id="c2a55-110">Enter a DNS Label name.</span></span> <span data-ttu-id="c2a55-111">Ta nazwa to rekord A, którego można użyć do nawiązania połączenia z maszyną wirtualną programu SQL Server przy użyciu nazwy, a nie bezpośrednio adresu IP.</span><span class="sxs-lookup"><span data-stu-id="c2a55-111">This name is an A Record that can be used to connect to your SQL Server VM by name instead of by IP Address directly.</span></span>

1. <span data-ttu-id="c2a55-112">Kliknij przycisk **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="c2a55-112">Click the **Save** button.</span></span>

    ![etykieta DNS](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-to-the-database-engine-from-another-computer"></a><span data-ttu-id="c2a55-114">Nawiązywanie połączenia z aparatem bazy danych z innego komputera</span><span class="sxs-lookup"><span data-stu-id="c2a55-114">Connect to the Database Engine from another computer</span></span>

1. <span data-ttu-id="c2a55-115">Na komputerze podłączonym do Internetu otwórz program SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="c2a55-115">On a computer connected to the internet, open SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="c2a55-116">Jeśli nie masz programu SQL Server Management Studio, możesz pobrać go [tutaj](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="c2a55-116">If you do not have SQL Server Management Studio, you can download it [here](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>

1. <span data-ttu-id="c2a55-117">W oknie dialogowym **Connect to Server** (Łączenie z serwerem) lub **Connect to Database Engine** (Łączenie z aparatem bazy danych) edytuj wartość **Server name** (Nazwa serwera).</span><span class="sxs-lookup"><span data-stu-id="c2a55-117">In the **Connect to Server** or **Connect to Database Engine** dialog box, edit the **Server name** value.</span></span> <span data-ttu-id="c2a55-118">Wprowadź adres IP lub pełną nazwę DNS maszyny wirtualnej (określoną w poprzednim zadaniu).</span><span class="sxs-lookup"><span data-stu-id="c2a55-118">Enter the IP address or full DNS name of the virtual machine (determined in the previous task).</span></span> <span data-ttu-id="c2a55-119">Możesz także dodać przecinek i podać port TCP programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c2a55-119">You can also add a comma and provide SQL Server's TCP port.</span></span> <span data-ttu-id="c2a55-120">Na przykład `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span><span class="sxs-lookup"><span data-stu-id="c2a55-120">For example, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span></span>

1. <span data-ttu-id="c2a55-121">W polu **Authentication** (Uwierzytelnianie) wybierz opcję **SQL Server Authentication** (Uwierzytelnianie programu SQL Server).</span><span class="sxs-lookup"><span data-stu-id="c2a55-121">In the **Authentication** box, select **SQL Server Authentication**.</span></span>

1. <span data-ttu-id="c2a55-122">W polu **Login** (Logowanie) wpisz nazwę prawidłowego identyfikatora logowania SQL.</span><span class="sxs-lookup"><span data-stu-id="c2a55-122">In the **Login** box, type the name of a valid SQL login.</span></span>

1. <span data-ttu-id="c2a55-123">W polu **Password** (Hasło) wpisz hasło logowania.</span><span class="sxs-lookup"><span data-stu-id="c2a55-123">In the **Password** box, type the password of the login.</span></span>

1. <span data-ttu-id="c2a55-124">Kliknij przycisk **Connect** (Połącz).</span><span class="sxs-lookup"><span data-stu-id="c2a55-124">Click **Connect**.</span></span>

    ![nawiązywanie połączenia w programie ssms](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)