
1. <span data-ttu-id="88372-101">tooescalate uprawnień, wpisz:</span><span class="sxs-lookup"><span data-stu-id="88372-101">tooescalate privileges, type:</span></span>
   
        sudo -s
   
    <span data-ttu-id="88372-102">Wprowadź hasło.</span><span class="sxs-lookup"><span data-stu-id="88372-102">Enter your password.</span></span>
2. <span data-ttu-id="88372-103">tooinstall serwer MySQL Community edition, wpisz:</span><span class="sxs-lookup"><span data-stu-id="88372-103">tooinstall MySQL Community Server edition, type:</span></span>
   
        zypper install mysql-community-server
   
    <span data-ttu-id="88372-104">Zaczekaj, aż MySQL pobiera i instaluje.</span><span class="sxs-lookup"><span data-stu-id="88372-104">Wait while MySQL downloads and installs.</span></span>
3. <span data-ttu-id="88372-105">tooset MySQL toostart podczas rozruchu systemu hello, wpisz:</span><span class="sxs-lookup"><span data-stu-id="88372-105">tooset MySQL toostart when hello system boots, type:</span></span>
   
        insserv mysql
4. <span data-ttu-id="88372-106">Ręcznie uruchom hello MySQL demon (mysqld) za pomocą tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="88372-106">Start hello MySQL daemon (mysqld) manually with this command:</span></span>
   
        rcmysql start
   
    <span data-ttu-id="88372-107">Stan hello toocheck hello demona MySQL, wpisz:</span><span class="sxs-lookup"><span data-stu-id="88372-107">toocheck hello status of hello MySQL daemon, type:</span></span>
   
        rcmysql status
   
    <span data-ttu-id="88372-108">Witaj toostop demona MySQL, wpisz:</span><span class="sxs-lookup"><span data-stu-id="88372-108">toostop hello MySQL daemon, type:</span></span>
   
        rcmysql stop
   
   > [!IMPORTANT]
   > <span data-ttu-id="88372-109">Po zainstalowaniu hasła głównego MySQL hello jest domyślnie pusta.</span><span class="sxs-lookup"><span data-stu-id="88372-109">After installation, hello MySQL root password is empty by default.</span></span> <span data-ttu-id="88372-110">Zaleca się, że uruchamiasz **mysql\_bezpiecznego\_instalacji**, skrypt, który pomaga bezpiecznego MySQL.</span><span class="sxs-lookup"><span data-stu-id="88372-110">We recommended that you run **mysql\_secure\_installation**, a script that helps secure MySQL.</span></span> <span data-ttu-id="88372-111">Hello skrypt wyświetli monit o hasła głównego MySQL hello toochange, usunąć konta użytkownika anonimowego wyłączyć głównego zdalnego logowania, usunąć bazy danych testu i ponownie załaduj hello uprawnienia tabeli.</span><span class="sxs-lookup"><span data-stu-id="88372-111">hello script prompts you toochange hello MySQL root password, remove anonymous user accounts, disable remote root logins, remove test databases, and reload hello privileges table.</span></span> <span data-ttu-id="88372-112">Zaleca się odpowiedzieć tooall tak z tych opcji, a następnie zmiany hasła głównego hello.</span><span class="sxs-lookup"><span data-stu-id="88372-112">We recommended that you answer yes tooall of these options and change hello root password.</span></span>
   > 
   > 
5. <span data-ttu-id="88372-113">Wpisz ten skrypt hello toorun MySQL skrypt instalacji:</span><span class="sxs-lookup"><span data-stu-id="88372-113">Type this toorun hello script MySQL installation script:</span></span>
   
        mysql_secure_installation
6. <span data-ttu-id="88372-114">Zaloguj się tooMySQL:</span><span class="sxs-lookup"><span data-stu-id="88372-114">Log in tooMySQL:</span></span>
   
        mysql -u root -p
   
    <span data-ttu-id="88372-115">Wprowadź hasła głównego MySQL hello (które można zmienić w poprzednim kroku hello) i zostanie wyświetlony wraz z monitem o których możesz wykonywać toointeract instrukcje SQL z bazą danych hello.</span><span class="sxs-lookup"><span data-stu-id="88372-115">Enter hello MySQL root password (which you changed in hello previous step) and you'll be presented with a prompt where you can issue SQL statements toointeract with hello database.</span></span>
7. <span data-ttu-id="88372-116">toocreate nowego użytkownika MySQL, uruchom następujące hello na powitania **mysql >** wiersza:</span><span class="sxs-lookup"><span data-stu-id="88372-116">toocreate a new MySQL user, run hello following at hello **mysql>** prompt:</span></span>
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="88372-117">Uwaga: hello średnikami (;) na końcu hello hello wiersze są kluczowe znaczenie dla końcowy hello poleceń.</span><span class="sxs-lookup"><span data-stu-id="88372-117">Note, hello semi-colons (;) at hello end of hello lines are crucial for ending hello commands.</span></span>
8. <span data-ttu-id="88372-118">toocreate hello bazy danych i przyznać `mysqluser` uprawnienia użytkownika na nim hello problem następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="88372-118">toocreate a database and grant hello `mysqluser` user permissions on it, issue hello following commands:</span></span>
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* too'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="88372-119">Należy pamiętać, że bazy danych, nazwy użytkownika i hasła są używane tylko przez skrypty łączenie toohello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="88372-119">Note that database user names and passwords are only used by scripts connecting toohello database.</span></span>  <span data-ttu-id="88372-120">Nazwy kont użytkowników bazy danych nie przedstawiają niekoniecznie konta użytkowników w systemie hello.</span><span class="sxs-lookup"><span data-stu-id="88372-120">Database user account names do not necessarily represent actual user accounts on hello system.</span></span>
9. <span data-ttu-id="88372-121">toolog w innym komputerze, wpisz:</span><span class="sxs-lookup"><span data-stu-id="88372-121">toolog in from another computer, type:</span></span>
   
        GRANT ALL ON testdatabase.* too'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    <span data-ttu-id="88372-122">gdzie `ip-address` jest adresem IP hello hello komputera, z którego ma zostać nawiązane połączenie tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="88372-122">where `ip-address` is hello IP address of hello computer from which you will connect tooMySQL.</span></span>
10. <span data-ttu-id="88372-123">Witaj tooexit narzędzie administracyjne bazy danych MySQL, wpisz:</span><span class="sxs-lookup"><span data-stu-id="88372-123">tooexit hello MySQL database administration utility, type:</span></span>
    
        quit

## <a name="add-an-endpoint"></a><span data-ttu-id="88372-124">Dodawanie punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="88372-124">Add an endpoint</span></span>
1. <span data-ttu-id="88372-125">Po zainstalowaniu MySQL, konieczne będzie tooconfigure tooaccess punktu końcowego MySQL zdalnie.</span><span class="sxs-lookup"><span data-stu-id="88372-125">After MySQL is installed, you'll need tooconfigure an endpoint tooaccess MySQL remotely.</span></span> <span data-ttu-id="88372-126">Zaloguj się za toohello [klasycznego portalu Azure][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="88372-126">Log in toohello [Azure  classic portal][AzurePortal].</span></span> <span data-ttu-id="88372-127">Kliknij przycisk **maszyn wirtualnych**, kliknij nazwę hello nowej maszyny wirtualnej, a następnie kliknij przycisk **punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="88372-127">Click **Virtual Machines**, click hello name of your new virtual machine, and then click **Endpoints**.</span></span>
2. <span data-ttu-id="88372-128">Kliknij przycisk **Dodaj** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="88372-128">Click **Add** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="88372-129">Dodawanie punktu końcowego o nazwie "MySQL" z protokołem **TCP**, i **publicznego** i **prywatnej** porty zestaw zbyt "3306".</span><span class="sxs-lookup"><span data-stu-id="88372-129">Add an endpoint named "MySQL" with protocol **TCP**, and **Public** and **Private** ports set too"3306".</span></span>
4. <span data-ttu-id="88372-130">tooremotely połączenie toohello maszynę wirtualną z komputera, wpisz:</span><span class="sxs-lookup"><span data-stu-id="88372-130">tooremotely connect toohello virtual machine from your computer, type:</span></span>
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    <span data-ttu-id="88372-131">Na przykład za pomocą wykorzystanie hello wirtualnej maszyny utworzone z tego samouczka, wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="88372-131">For example, using hello virual machine we created in this tutorial, type this command:</span></span>
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
