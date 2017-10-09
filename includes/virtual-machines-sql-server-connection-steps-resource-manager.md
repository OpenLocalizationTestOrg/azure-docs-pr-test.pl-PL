### <a name="configure-a-dns-label-for-hello-public-ip-address"></a><span data-ttu-id="6295e-101">Konfigurowanie etykiety DNS dla publicznego adresu IP hello</span><span class="sxs-lookup"><span data-stu-id="6295e-101">Configure a DNS Label for hello public IP address</span></span>

<span data-ttu-id="6295e-102">tooconnect toohello aparatu bazy danych programu SQL Server z hello Internet, należy wziąć pod uwagę tworzenia etykiety DNS dla publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="6295e-102">tooconnect toohello SQL Server Database Engine from hello Internet, consider creating a DNS Label for your public IP address.</span></span> <span data-ttu-id="6295e-103">Możesz połączyć za pomocą adresu IP, ale hello Etykieta DNS tworzy rekord A, który jest łatwiejsze tooidentify i streszczenia hello podstawowej publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="6295e-103">You can connect by IP address, but hello DNS Label creates an A Record that is easier tooidentify and abstracts hello underlying public IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="6295e-104">Etykiety DNS nie są wymagane, jeśli plan tooonly połączyć toohello programu SQL Server wystąpienie w ramach hello sam sieci wirtualnej lub tylko lokalnie.</span><span class="sxs-lookup"><span data-stu-id="6295e-104">DNS Labels are not required if you plan tooonly connect toohello SQL Server instance within hello same Virtual Network or only locally.</span></span>

<span data-ttu-id="6295e-105">Najpierw wybierz etykietę DNS toocreate **maszyn wirtualnych** w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="6295e-105">toocreate a DNS Label, first select **Virtual machines** in hello portal.</span></span> <span data-ttu-id="6295e-106">Wybierz sieci maszyny Wirtualnej programu SQL Server toobring jej właściwości.</span><span class="sxs-lookup"><span data-stu-id="6295e-106">Select your SQL Server VM toobring up its properties.</span></span>

1. <span data-ttu-id="6295e-107">Omówienie maszyny wirtualnej hello, wybierz użytkownika **publicznego adresu IP**.</span><span class="sxs-lookup"><span data-stu-id="6295e-107">In hello virtual machine overview, select your **Public IP address**.</span></span>

    ![publiczny adres IP](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. <span data-ttu-id="6295e-109">W właściwości hello publicznego adresu IP, rozwiń węzeł **konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="6295e-109">In hello properties for your Public IP address, expand **Configuration**.</span></span>

1. <span data-ttu-id="6295e-110">Wprowadź nazwę etykiety DNS.</span><span class="sxs-lookup"><span data-stu-id="6295e-110">Enter a DNS Label name.</span></span> <span data-ttu-id="6295e-111">Ta nazwa jest rekord A, które mogą być używane tooconnect tooyour maszyny Wirtualnej programu SQL Server przy użyciu nazwy za pomocą adresu IP bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="6295e-111">This name is an A Record that can be used tooconnect tooyour SQL Server VM by name instead of by IP Address directly.</span></span>

1. <span data-ttu-id="6295e-112">Kliknij przycisk hello **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6295e-112">Click hello **Save** button.</span></span>

    ![etykieta DNS](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a><span data-ttu-id="6295e-114">Połącz toohello aparatu bazy danych z innego komputera</span><span class="sxs-lookup"><span data-stu-id="6295e-114">Connect toohello Database Engine from another computer</span></span>

1. <span data-ttu-id="6295e-115">Na komputerze połączone toohello internet, Otwórz program SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="6295e-115">On a computer connected toohello internet, open SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="6295e-116">Jeśli nie masz programu SQL Server Management Studio, możesz pobrać go [tutaj](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="6295e-116">If you do not have SQL Server Management Studio, you can download it [here](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>

1. <span data-ttu-id="6295e-117">W hello **połączyć tooServer** lub **połączyć tooDatabase aparat** okno dialogowe, Edytuj hello **nazwy serwera** wartość.</span><span class="sxs-lookup"><span data-stu-id="6295e-117">In hello **Connect tooServer** or **Connect tooDatabase Engine** dialog box, edit hello **Server name** value.</span></span> <span data-ttu-id="6295e-118">Wprowadź adres IP hello lub pełną nazwę DNS hello maszyny wirtualnej (określoną w poprzednim zadaniu hello).</span><span class="sxs-lookup"><span data-stu-id="6295e-118">Enter hello IP address or full DNS name of hello virtual machine (determined in hello previous task).</span></span> <span data-ttu-id="6295e-119">Możesz także dodać przecinek i podać port TCP programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6295e-119">You can also add a comma and provide SQL Server's TCP port.</span></span> <span data-ttu-id="6295e-120">Na przykład `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span><span class="sxs-lookup"><span data-stu-id="6295e-120">For example, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span></span>

1. <span data-ttu-id="6295e-121">W hello **uwierzytelniania** wybierz opcję **uwierzytelniania programu SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="6295e-121">In hello **Authentication** box, select **SQL Server Authentication**.</span></span>

1. <span data-ttu-id="6295e-122">W hello **logowania** okno, nazwa typu hello umożliwiające prawidłowe logowanie SQL.</span><span class="sxs-lookup"><span data-stu-id="6295e-122">In hello **Login** box, type hello name of a valid SQL login.</span></span>

1. <span data-ttu-id="6295e-123">W hello **hasło** okno, wpisz hasło hello hello logowania.</span><span class="sxs-lookup"><span data-stu-id="6295e-123">In hello **Password** box, type hello password of hello login.</span></span>

1. <span data-ttu-id="6295e-124">Kliknij przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="6295e-124">Click **Connect**.</span></span>

    ![nawiązywanie połączenia w programie ssms](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)