
1. <span data-ttu-id="a1e1f-101">Aby eskalować uprawnienia, wpisz:</span><span class="sxs-lookup"><span data-stu-id="a1e1f-101">To escalate privileges, type:</span></span>
   
        sudo -s
   
    <span data-ttu-id="a1e1f-102">Wprowadź hasło.</span><span class="sxs-lookup"><span data-stu-id="a1e1f-102">Enter your password.</span></span>
2. <span data-ttu-id="a1e1f-103">Aby zainstalować serwer MySQL Community edition, wpisz:</span><span class="sxs-lookup"><span data-stu-id="a1e1f-103">To install MySQL Community Server edition, type:</span></span>
   
        zypper install mysql-community-server
   
    <span data-ttu-id="a1e1f-104">Zaczekaj, aż MySQL pobiera i instaluje.</span><span class="sxs-lookup"><span data-stu-id="a1e1f-104">Wait while MySQL downloads and installs.</span></span>
3. <span data-ttu-id="a1e1f-105">Aby ustawić MySQL można uruchomić podczas rozruchu systemu, wpisz:</span><span class="sxs-lookup"><span data-stu-id="a1e1f-105">To set MySQL to start when the system boots, type:</span></span>
   
        insserv mysql
4. <span data-ttu-id="a1e1f-106">Ręcznie Uruchom demona MySQL (mysqld) za pomocą tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a1e1f-106">Start the MySQL daemon (mysqld) manually with this command:</span></span>
   
        rcmysql start
   
    <span data-ttu-id="a1e1f-107">Aby sprawdzić stan demona MySQL, wpisz:</span><span class="sxs-lookup"><span data-stu-id="a1e1f-107">To check the status of the MySQL daemon, type:</span></span>
   
        rcmysql status
   
    <span data-ttu-id="a1e1f-108">Aby zatrzymać demona MySQL, wpisz:</span><span class="sxs-lookup"><span data-stu-id="a1e1f-108">To stop the MySQL daemon, type:</span></span>
   
        rcmysql stop
   
   > [!IMPORTANT]
   > <span data-ttu-id="a1e1f-109">Po zakończeniu instalacji MySQL hasła głównego jest domyślnie pusta.</span><span class="sxs-lookup"><span data-stu-id="a1e1f-109">After installation, the MySQL root password is empty by default.</span></span> <span data-ttu-id="a1e1f-110">Zaleca się, że uruchamiasz **mysql\_bezpiecznego\_instalacji**, skrypt, który pomaga bezpiecznego MySQL.</span><span class="sxs-lookup"><span data-stu-id="a1e1f-110">We recommended that you run **mysql\_secure\_installation**, a script that helps secure MySQL.</span></span> <span data-ttu-id="a1e1f-111">Skrypt wyświetli monit o zmianę hasła głównego MySQL, usunąć konta użytkownika anonimowego, wyłącz logowania zdalnego głównego, usunąć bazy danych testu i ponownie załadować tabelę uprawnień.</span><span class="sxs-lookup"><span data-stu-id="a1e1f-111">The script prompts you to change the MySQL root password, remove anonymous user accounts, disable remote root logins, remove test databases, and reload the privileges table.</span></span> <span data-ttu-id="a1e1f-112">Zaleca się odpowiedzieć, tak aby wszystkie te opcje, a następnie zmień hasło główne.</span><span class="sxs-lookup"><span data-stu-id="a1e1f-112">We recommended that you answer yes to all of these options and change the root password.</span></span>
   > 
   > 
5. <span data-ttu-id="a1e1f-113">Wpisz, aby uruchomić skrypt MySQL skrypt instalacji:</span><span class="sxs-lookup"><span data-stu-id="a1e1f-113">Type this to run the script MySQL installation script:</span></span>
   
        mysql_secure_installation
6. <span data-ttu-id="a1e1f-114">Zaloguj się do MySQL:</span><span class="sxs-lookup"><span data-stu-id="a1e1f-114">Log in to MySQL:</span></span>
   
        mysql -u root -p
   
    <span data-ttu-id="a1e1f-115">Wprowadź hasło głównego MySQL (które można zmienić w poprzednim kroku) i zostanie wyświetlony wraz z monitem o których możesz wykonywać instrukcje SQL do interakcji z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="a1e1f-115">Enter the MySQL root password (which you changed in the previous step) and you'll be presented with a prompt where you can issue SQL statements to interact with the database.</span></span>
7. <span data-ttu-id="a1e1f-116">Aby utworzyć nowy użytkownik MySQL, uruchom następujące polecenie w **mysql >** wiersza:</span><span class="sxs-lookup"><span data-stu-id="a1e1f-116">To create a new MySQL user, run the following at the **mysql>** prompt:</span></span>
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="a1e1f-117">Uwaga: średnikami (;) na końcu wiersza, które są istotne dla zakończenia polecenia.</span><span class="sxs-lookup"><span data-stu-id="a1e1f-117">Note, the semi-colons (;) at the end of the lines are crucial for ending the commands.</span></span>
8. <span data-ttu-id="a1e1f-118">Aby utworzyć bazę danych i udzielić `mysqluser` uprawnienia użytkownika do niego, wydawać następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="a1e1f-118">To create a database and grant the `mysqluser` user permissions on it, issue the following commands:</span></span>
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* TO 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="a1e1f-119">Należy pamiętać, że bazy danych, nazwy użytkownika i hasła są używane tylko przez skrypty łączenia z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="a1e1f-119">Note that database user names and passwords are only used by scripts connecting to the database.</span></span>  <span data-ttu-id="a1e1f-120">Nazwy kont użytkowników bazy danych nie przedstawiają niekoniecznie konta użytkowników w systemie.</span><span class="sxs-lookup"><span data-stu-id="a1e1f-120">Database user account names do not necessarily represent actual user accounts on the system.</span></span>
9. <span data-ttu-id="a1e1f-121">Aby zalogować się na innym komputerze, wpisz:</span><span class="sxs-lookup"><span data-stu-id="a1e1f-121">To log in from another computer, type:</span></span>
   
        GRANT ALL ON testdatabase.* TO 'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    <span data-ttu-id="a1e1f-122">gdzie `ip-address` to adres IP komputera, z którym połączy się MySQL.</span><span class="sxs-lookup"><span data-stu-id="a1e1f-122">where `ip-address` is the IP address of the computer from which you will connect to MySQL.</span></span>
10. <span data-ttu-id="a1e1f-123">Aby zamknąć narzędzie administracyjne bazy danych MySQL, wpisz:</span><span class="sxs-lookup"><span data-stu-id="a1e1f-123">To exit the MySQL database administration utility, type:</span></span>
    
        quit

## <a name="add-an-endpoint"></a><span data-ttu-id="a1e1f-124">Dodawanie punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="a1e1f-124">Add an endpoint</span></span>
1. <span data-ttu-id="a1e1f-125">Po zainstalowaniu MySQL, musisz skonfigurować punkt końcowy do zdalnego dostępu MySQL.</span><span class="sxs-lookup"><span data-stu-id="a1e1f-125">After MySQL is installed, you'll need to configure an endpoint to access MySQL remotely.</span></span> <span data-ttu-id="a1e1f-126">Zaloguj się do [klasycznego portalu Azure][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="a1e1f-126">Log in to the [Azure  classic portal][AzurePortal].</span></span> <span data-ttu-id="a1e1f-127">Kliknij przycisk **maszyn wirtualnych**, kliknij nazwę nowej maszyny wirtualnej, a następnie kliknij przycisk **punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="a1e1f-127">Click **Virtual Machines**, click the name of your new virtual machine, and then click **Endpoints**.</span></span>
2. <span data-ttu-id="a1e1f-128">Kliknij przycisk **Dodaj** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="a1e1f-128">Click **Add** at the bottom of the page.</span></span>
3. <span data-ttu-id="a1e1f-129">Dodawanie punktu końcowego o nazwie "MySQL" z protokołem **TCP**, i **publicznego** i **prywatnej** porty ustawioną wartość "3306".</span><span class="sxs-lookup"><span data-stu-id="a1e1f-129">Add an endpoint named "MySQL" with protocol **TCP**, and **Public** and **Private** ports set to "3306".</span></span>
4. <span data-ttu-id="a1e1f-130">Zdalne połączenia z maszyną wirtualną z komputera, wpisz:</span><span class="sxs-lookup"><span data-stu-id="a1e1f-130">To remotely connect to the virtual machine from your computer, type:</span></span>
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    <span data-ttu-id="a1e1f-131">Na przykład przy użyciu maszyny wykorzystanie wirtualnej utworzone w tym samouczku, wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="a1e1f-131">For example, using the virual machine we created in this tutorial, type this command:</span></span>
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
