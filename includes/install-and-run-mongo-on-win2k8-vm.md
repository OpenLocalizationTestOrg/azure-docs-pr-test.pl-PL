<span data-ttu-id="e5a22-101">Wykonaj następujące kroki, aby zainstalować i uruchomić bazy danych MongoDB na maszynie wirtualnej z systemem Windows Server.</span><span class="sxs-lookup"><span data-stu-id="e5a22-101">Follow these steps to install and run MongoDB on a virtual machine running Windows Server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e5a22-102">Funkcje zabezpieczeń bazy danych MongoDB, takich jak uwierzytelnianie i powiązanie adresu IP, nie są domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="e5a22-102">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="e5a22-103">Funkcje zabezpieczeń powinny być włączone przed wdrożeniem w środowisku produkcyjnym bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e5a22-103">Security features should be enabled before deploying MongoDB to a production environment.</span></span>  <span data-ttu-id="e5a22-104">Aby uzyskać więcej informacji, zobacz [zabezpieczeń i uwierzytelniania](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span><span class="sxs-lookup"><span data-stu-id="e5a22-104">For more information, see [Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>
>
>

1. <span data-ttu-id="e5a22-105">Po nawiązaniu połączenia z maszyną wirtualną przy użyciu pulpitu zdalnego, Otwórz program Internet Explorer z **Start** menu na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5a22-105">After you've connected to the virtual machine using Remote Desktop, open Internet Explorer from the **Start** menu on the virtual machine.</span></span>
2. <span data-ttu-id="e5a22-106">Wybierz **narzędzia** przycisk w prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="e5a22-106">Select the **Tools** button in the upper right corner.</span></span>  <span data-ttu-id="e5a22-107">W **Opcje internetowe**, wybierz pozycję **zabezpieczeń** , a następnie wybierz **Zaufane witryny** ikonę, a na koniec kliknij **witryny** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e5a22-107">In **Internet Options**, select the **Security** tab, and then select the **Trusted Sites** icon, and finally click the **Sites** button.</span></span> <span data-ttu-id="e5a22-108">Dodaj *https://\*. mongodb.org* do listy zaufanych witryn.</span><span class="sxs-lookup"><span data-stu-id="e5a22-108">Add *https://\*.mongodb.org* to the list of trusted sites.</span></span>
3. <span data-ttu-id="e5a22-109">Przejdź do [pobiera — bazy danych MongoDB](https://www.mongodb.com/download-center#community).</span><span class="sxs-lookup"><span data-stu-id="e5a22-109">Go to [Downloads - MongoDB](https://www.mongodb.com/download-center#community).</span></span>
4. <span data-ttu-id="e5a22-110">Znajdź **bieżącej wersji stabilnej** z **Community Server**, wybierz najnowszą **64-bitowych** wersji w kolumnie systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="e5a22-110">Find the **Current Stable Release** of **Community Server**, select the latest **64-bit** version in the Windows column.</span></span> <span data-ttu-id="e5a22-111">Pobierz, a następnie uruchom Instalatora MSI.</span><span class="sxs-lookup"><span data-stu-id="e5a22-111">Download, then run the MSI installer.</span></span>
5. <span data-ttu-id="e5a22-112">Bazy danych MongoDB zazwyczaj jest zainstalowany w C:\Program Files\MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e5a22-112">MongoDB is typically installed in C:\Program Files\MongoDB.</span></span> <span data-ttu-id="e5a22-113">Wyszukaj zmiennych środowiskowych na pulpicie, a następnie dodaj ścieżkę danych binarnych bazy danych MongoDB do zmiennej PATH.</span><span class="sxs-lookup"><span data-stu-id="e5a22-113">Search for Environment Variables on the desktop and add the MongoDB binaries path to the PATH variable.</span></span> <span data-ttu-id="e5a22-114">Na przykład może znaleźć plików binarnych w C:\Program Files\MongoDB\Server\3.4\bin na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e5a22-114">For example, you might find the binaries at C:\Program Files\MongoDB\Server\3.4\bin on your machine.</span></span>
6. <span data-ttu-id="e5a22-115">Tworzenie katalogów danych i dziennika bazy danych MongoDB dysku danych (takich jak dysk **F:**) utworzone w poprzednich krokach.</span><span class="sxs-lookup"><span data-stu-id="e5a22-115">Create MongoDB data and log directories in the data disk (such as drive **F:**) you created in the preceding steps.</span></span> <span data-ttu-id="e5a22-116">Z **Start**, wybierz pozycję **wiersza polecenia** aby otworzyć okno wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="e5a22-116">From **Start**, select **Command Prompt** to open a command prompt window.</span></span>  <span data-ttu-id="e5a22-117">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="e5a22-117">Type:</span></span>

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. <span data-ttu-id="e5a22-118">Aby uruchomić bazy danych, uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="e5a22-118">To run the database, run:</span></span>

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    <span data-ttu-id="e5a22-119">Wszystkie komunikaty dziennika są kierowane do *F:\MongoLogs\mongolog.log* plików serwera mongod.exe rozpoczęciu i preallocates plików dziennika.</span><span class="sxs-lookup"><span data-stu-id="e5a22-119">All log messages are directed to the *F:\MongoLogs\mongolog.log* file as mongod.exe server starts and preallocates journal files.</span></span> <span data-ttu-id="e5a22-120">Może upłynąć kilka minut dla bazy danych MongoDB do przydzielenia plików dziennika i rozpocząć nasłuchiwania dla połączenia.</span><span class="sxs-lookup"><span data-stu-id="e5a22-120">It may take several minutes for MongoDB to preallocate the journal files and start listening for connections.</span></span> <span data-ttu-id="e5a22-121">Wiersz polecenia pozostaje koncentruje się na to zadanie jest uruchomiona wystąpienia bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e5a22-121">The command prompt stays focused on this task while your MongoDB instance is running.</span></span>
8. <span data-ttu-id="e5a22-122">Aby uruchomić powłoki administracyjne bazy danych MongoDB, otwiera inne okno polecenia z **Start** i wpisz następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="e5a22-122">To start the MongoDB administrative shell, open another command window from **Start** and type the following commands:</span></span>

        C:\> cd \my_mongo_dir\bin  
        C:\my_mongo_dir\bin> mongo  
        >db  
        test
        > db.foo.insert( { a : 1 } )  
        > db.foo.find()  
        { _id : ..., a : 1 }  
        > show dbs  
        ...  
        > show collections  
        ...  
        > help  

    <span data-ttu-id="e5a22-123">Baza danych została utworzona przez insert.</span><span class="sxs-lookup"><span data-stu-id="e5a22-123">The database is created by the insert.</span></span>
9. <span data-ttu-id="e5a22-124">Alternatywnie możesz zainstalować mongod.exe jako usługa:</span><span class="sxs-lookup"><span data-stu-id="e5a22-124">Alternatively, you can install mongod.exe as a service:</span></span>

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    <span data-ttu-id="e5a22-125">Zainstalowano usługę o nazwie bazy danych MongoDB z opisem "BD o Mongo".</span><span class="sxs-lookup"><span data-stu-id="e5a22-125">A service is installed named MongoDB with a description of "Mongo DB".</span></span> <span data-ttu-id="e5a22-126">`--logpath` Opcji należy używać, aby określić plik dziennika, ponieważ uruchomiona usługa ma okno polecenia, aby wyświetlić dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="e5a22-126">The `--logpath` option must be used to specify a log file, since the running service does not have a command window to display output.</span></span>  <span data-ttu-id="e5a22-127">`--logappend` Opcja określa, czy ponowne uruchomienie usługi powoduje, że dane wyjściowe do dołączenia do istniejącego pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="e5a22-127">The `--logappend` option specifies that a restart of the service causes output to append to the existing log file.</span></span>  <span data-ttu-id="e5a22-128">`--dbpath` Opcji określa lokalizację katalogu danych.</span><span class="sxs-lookup"><span data-stu-id="e5a22-128">The `--dbpath` option specifies the location of the data directory.</span></span> <span data-ttu-id="e5a22-129">Aby bardziej związane z usługą opcji wiersza polecenia, zobacz [opcje wiersza polecenia związane z usługą][MongoWindowsSvcOptions].</span><span class="sxs-lookup"><span data-stu-id="e5a22-129">For more service-related command-line options, see [Service-related command-line options][MongoWindowsSvcOptions].</span></span>

    <span data-ttu-id="e5a22-130">Aby uruchomić usługę, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e5a22-130">To start the service, run this command:</span></span>

        C:\> net start MongoDB
10. <span data-ttu-id="e5a22-131">Bazy danych MongoDB jest zainstalowana i uruchomiona, należy otworzyć port w Zaporze systemu Windows, więc możesz zdalnie nawiązać połączenie bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e5a22-131">Now that MongoDB is installed and running, you need to open a port in Windows Firewall so you can remotely connect to MongoDB.</span></span>  <span data-ttu-id="e5a22-132">Z **Start** menu, wybierz opcję **narzędzia administracyjne** , a następnie **Zapora systemu Windows z zabezpieczeniami zaawansowanymi**.</span><span class="sxs-lookup"><span data-stu-id="e5a22-132">From the **Start** menu, select **Administrative Tools** and then **Windows Firewall with Advanced Security**.</span></span>
11. <span data-ttu-id="e5a22-133">() w okienku po lewej stronie wybierz **reguły ruchu przychodzącego**.</span><span class="sxs-lookup"><span data-stu-id="e5a22-133">a) In the left pane, select **Inbound Rules**.</span></span>  <span data-ttu-id="e5a22-134">W **akcje** okienko po prawej stronie wybierz **nową regułę...** .</span><span class="sxs-lookup"><span data-stu-id="e5a22-134">In the **Actions** pane on the right, select **New Rule...**.</span></span>

    ![Zapora systemu Windows][Image1]

    <span data-ttu-id="e5a22-136">(b) w **Kreatora nowej reguły przychodzącej**, wybierz pozycję **portu** , a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="e5a22-136">b) In the **New Inbound Rule Wizard**, select **Port** and then click **Next**.</span></span>

    ![Zapora systemu Windows][Image2]

    <span data-ttu-id="e5a22-138">c) wybierz **TCP** , a następnie **określone porty lokalne**.</span><span class="sxs-lookup"><span data-stu-id="e5a22-138">c) Select **TCP** and then **Specific local ports**.</span></span>  <span data-ttu-id="e5a22-139">Określ port "27017" (domyślny port bazy danych MongoDB nasłuchuje), a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="e5a22-139">Specify a port of "27017" (the default port MongoDB listens on) and click **Next**.</span></span>

    ![Zapora systemu Windows][Image3]

    <span data-ttu-id="e5a22-141">d) wybierz **zezwalały na połączenie** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="e5a22-141">d) Select **Allow the connection** and click **Next**.</span></span>

    ![Zapora systemu Windows][Image4]

    <span data-ttu-id="e5a22-143">e) kliknij **dalej** ponownie.</span><span class="sxs-lookup"><span data-stu-id="e5a22-143">e) Click **Next** again.</span></span>

    ![Zapora systemu Windows][Image5]

    <span data-ttu-id="e5a22-145">f) określ nazwę reguły, takie jak "MongoPort", a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="e5a22-145">f) Specify a name for the rule, such as "MongoPort", and click **Finish**.</span></span>

    ![Zapora systemu Windows][Image6]

12. <span data-ttu-id="e5a22-147">Jeśli punkt końcowy nie skonfigurowała bazy danych mongodb, podczas tworzenia maszyny wirtualnej, możesz to zrobić teraz.</span><span class="sxs-lookup"><span data-stu-id="e5a22-147">If you didn't configure an endpoint for MongoDB when you created the virtual machine, you can do it now.</span></span> <span data-ttu-id="e5a22-148">Należy zarówno reguły zapory, jak i punktu końcowego, aby mieć możliwość nawiązania połączenia do bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e5a22-148">You need both the firewall rule and the endpoint to be able to connect to MongoDB remotely.</span></span>

  <span data-ttu-id="e5a22-149">W portalu Azure kliknij **maszyn wirtualnych (klasyczne)**, kliknij nazwę nowej maszyny wirtualnej, a następnie kliknij przycisk **punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="e5a22-149">In the Azure portal, click **Virtual Machines (classic)**, click the name of your new virtual machine, and then click **Endpoints**.</span></span>

    ![Punkty końcowe][Image7]

13. <span data-ttu-id="e5a22-151">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="e5a22-151">Click **Add**.</span></span>

14. <span data-ttu-id="e5a22-152">Dodawanie punktu końcowego o nazwie "Mongo" protokołu **TCP**, a oba **publicznego** i **prywatnej** porty ustawioną wartość "27017".</span><span class="sxs-lookup"><span data-stu-id="e5a22-152">Add an endpoint with name "Mongo", protocol **TCP**, and both **Public** and **Private** ports set to "27017".</span></span> <span data-ttu-id="e5a22-153">Otwarcie tego portu umożliwia bazy danych MongoDB ma być dostępna zdalnie.</span><span class="sxs-lookup"><span data-stu-id="e5a22-153">Opening this port allows MongoDB to be accessed remotely.</span></span>

    ![Punkty końcowe][Image9]

> [!NOTE]
> <span data-ttu-id="e5a22-155">Port 27017 jest domyślny port używany przez bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e5a22-155">The port 27017 is the default port used by MongoDB.</span></span> <span data-ttu-id="e5a22-156">Ten port domyślny można zmienić, określając `--port` parametru podczas uruchamiania serwera mongod.exe.</span><span class="sxs-lookup"><span data-stu-id="e5a22-156">You can change this default port by specifying the `--port` parameter when starting the mongod.exe server.</span></span> <span data-ttu-id="e5a22-157">Upewnij się, że ten sam numer portu w zaporze i punktu końcowego "Mongo" w poprzednich instrukcji.</span><span class="sxs-lookup"><span data-stu-id="e5a22-157">Make sure to give the same port number in the firewall and the "Mongo" endpoint in the preceding instructions.</span></span>
>
>

[MongoDownloads]: http://www.mongodb.org/downloads

[MongoWindowsSvcOptions]: http://www.mongodb.org/display/DOCS/Windows+Service


[Image1]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall1.png
[Image2]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall2.png
[Image3]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall3.png
[Image4]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall4.png
[Image5]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall5.png
[Image6]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall6.png
[Image7]: ./media/install-and-run-mongo-on-win2k8-vm/menusendpointadd.png
<!-- Removed 03/08/2017. Not in new portal. -->
<!-- [Image8]: ./media/install-and-run-mongo-on-win2k8-vm/WinVmAddEndpoint2.png
-->
[Image9]: ./media/install-and-run-mongo-on-win2k8-vm/newendpointdetails.png
