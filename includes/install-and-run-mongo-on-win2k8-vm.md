<span data-ttu-id="dabaa-101">Wykonaj te kroki tooinstall i uruchomić bazy danych MongoDB na maszynie wirtualnej z systemem Windows Server.</span><span class="sxs-lookup"><span data-stu-id="dabaa-101">Follow these steps tooinstall and run MongoDB on a virtual machine running Windows Server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dabaa-102">Funkcje zabezpieczeń bazy danych MongoDB, takich jak uwierzytelnianie i powiązanie adresu IP, nie są domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="dabaa-102">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="dabaa-103">Funkcje zabezpieczeń powinny być włączone przed wdrożeniem w środowisku produkcyjnym tooa bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="dabaa-103">Security features should be enabled before deploying MongoDB tooa production environment.</span></span>  <span data-ttu-id="dabaa-104">Aby uzyskać więcej informacji, zobacz [zabezpieczeń i uwierzytelniania](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span><span class="sxs-lookup"><span data-stu-id="dabaa-104">For more information, see [Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>
>
>

1. <span data-ttu-id="dabaa-105">Po nawiązaniu połączenia toohello maszyny wirtualnej za pomocą pulpitu zdalnego, Otwórz program Internet Explorer z hello **Start** menu hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dabaa-105">After you've connected toohello virtual machine using Remote Desktop, open Internet Explorer from hello **Start** menu on hello virtual machine.</span></span>
2. <span data-ttu-id="dabaa-106">Wybierz hello **narzędzia** przycisk w prawym górnym rogu hello.</span><span class="sxs-lookup"><span data-stu-id="dabaa-106">Select hello **Tools** button in hello upper right corner.</span></span>  <span data-ttu-id="dabaa-107">W **Opcje internetowe**, wybierz pozycję hello **zabezpieczeń** , a następnie wybierz hello **Zaufane witryny** ikonę, a na koniec kliknij hello **witryny** przycisk.</span><span class="sxs-lookup"><span data-stu-id="dabaa-107">In **Internet Options**, select hello **Security** tab, and then select hello **Trusted Sites** icon, and finally click hello **Sites** button.</span></span> <span data-ttu-id="dabaa-108">Dodaj *https://\*. mongodb.org* toohello listy zaufanych witryn.</span><span class="sxs-lookup"><span data-stu-id="dabaa-108">Add *https://\*.mongodb.org* toohello list of trusted sites.</span></span>
3. <span data-ttu-id="dabaa-109">Przejdź za[pobiera — bazy danych MongoDB](https://www.mongodb.com/download-center#community).</span><span class="sxs-lookup"><span data-stu-id="dabaa-109">Go too[Downloads - MongoDB](https://www.mongodb.com/download-center#community).</span></span>
4. <span data-ttu-id="dabaa-110">Znajdź hello **bieżącej wersji stabilnej** z **Community Server**, wybierz pozycję hello najnowszych **64-bitowych** wersji w kolumnie Windows hello.</span><span class="sxs-lookup"><span data-stu-id="dabaa-110">Find hello **Current Stable Release** of **Community Server**, select hello latest **64-bit** version in hello Windows column.</span></span> <span data-ttu-id="dabaa-111">Pobierz, a następnie uruchom Instalatora MSI hello.</span><span class="sxs-lookup"><span data-stu-id="dabaa-111">Download, then run hello MSI installer.</span></span>
5. <span data-ttu-id="dabaa-112">Bazy danych MongoDB zazwyczaj jest zainstalowany w C:\Program Files\MongoDB.</span><span class="sxs-lookup"><span data-stu-id="dabaa-112">MongoDB is typically installed in C:\Program Files\MongoDB.</span></span> <span data-ttu-id="dabaa-113">Wyszukiwanie zmiennych środowiskowych na pulpicie hello i dodać zmiennej PATH toohello ścieżki plików binarnych hello bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="dabaa-113">Search for Environment Variables on hello desktop and add hello MongoDB binaries path toohello PATH variable.</span></span> <span data-ttu-id="dabaa-114">Może na przykład znaleźć plików binarnych hello na C:\Program Files\MongoDB\Server\3.4\bin na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="dabaa-114">For example, you might find hello binaries at C:\Program Files\MongoDB\Server\3.4\bin on your machine.</span></span>
6. <span data-ttu-id="dabaa-115">Tworzenie katalogów danych i dziennika bazy danych MongoDB hello dysku danych (takich jak dysk **F:**) utworzone w poprzednich krokach hello.</span><span class="sxs-lookup"><span data-stu-id="dabaa-115">Create MongoDB data and log directories in hello data disk (such as drive **F:**) you created in hello preceding steps.</span></span> <span data-ttu-id="dabaa-116">Z **Start**, wybierz pozycję **wiersza polecenia** tooopen okno wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="dabaa-116">From **Start**, select **Command Prompt** tooopen a command prompt window.</span></span>  <span data-ttu-id="dabaa-117">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="dabaa-117">Type:</span></span>

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. <span data-ttu-id="dabaa-118">toorun hello bazy danych, uruchom:</span><span class="sxs-lookup"><span data-stu-id="dabaa-118">toorun hello database, run:</span></span>

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    <span data-ttu-id="dabaa-119">Wszystkie komunikaty dziennika są ukierunkowanej toohello *F:\MongoLogs\mongolog.log* plików serwera mongod.exe rozpoczęciu i preallocates plików dziennika.</span><span class="sxs-lookup"><span data-stu-id="dabaa-119">All log messages are directed toohello *F:\MongoLogs\mongolog.log* file as mongod.exe server starts and preallocates journal files.</span></span> <span data-ttu-id="dabaa-120">Może potrwać kilka minut dla bazy danych MongoDB toopreallocate hello plików dziennika i rozpocząć nasłuchiwania dla połączenia.</span><span class="sxs-lookup"><span data-stu-id="dabaa-120">It may take several minutes for MongoDB toopreallocate hello journal files and start listening for connections.</span></span> <span data-ttu-id="dabaa-121">Wiersz polecenia Hello pozostaje koncentruje się na to zadanie uruchomionej wystąpienia bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="dabaa-121">hello command prompt stays focused on this task while your MongoDB instance is running.</span></span>
8. <span data-ttu-id="dabaa-122">toostart hello powłoki administracyjne bazy danych MongoDB, otwiera inne okno polecenia z **Start** i hello wpisz następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="dabaa-122">toostart hello MongoDB administrative shell, open another command window from **Start** and type hello following commands:</span></span>

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

    <span data-ttu-id="dabaa-123">Witaj baza danych została utworzona przez hello insert.</span><span class="sxs-lookup"><span data-stu-id="dabaa-123">hello database is created by hello insert.</span></span>
9. <span data-ttu-id="dabaa-124">Alternatywnie możesz zainstalować mongod.exe jako usługa:</span><span class="sxs-lookup"><span data-stu-id="dabaa-124">Alternatively, you can install mongod.exe as a service:</span></span>

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    <span data-ttu-id="dabaa-125">Zainstalowano usługę o nazwie bazy danych MongoDB z opisem "BD o Mongo".</span><span class="sxs-lookup"><span data-stu-id="dabaa-125">A service is installed named MongoDB with a description of "Mongo DB".</span></span> <span data-ttu-id="dabaa-126">Witaj `--logpath` opcja musi być używane toospecify pliku dziennika, od hello usługi nie ma danych wyjściowych toodisplay okna poleceń.</span><span class="sxs-lookup"><span data-stu-id="dabaa-126">hello `--logpath` option must be used toospecify a log file, since hello running service does not have a command window toodisplay output.</span></span>  <span data-ttu-id="dabaa-127">Witaj `--logappend` opcja określa, czy ponowne uruchomienie usługi hello powoduje, że dane wyjściowe tooappend toohello istniejący plik dziennika.</span><span class="sxs-lookup"><span data-stu-id="dabaa-127">hello `--logappend` option specifies that a restart of hello service causes output tooappend toohello existing log file.</span></span>  <span data-ttu-id="dabaa-128">Witaj `--dbpath` opcji określa lokalizację hello hello danych katalogu.</span><span class="sxs-lookup"><span data-stu-id="dabaa-128">hello `--dbpath` option specifies hello location of hello data directory.</span></span> <span data-ttu-id="dabaa-129">Aby bardziej związane z usługą opcji wiersza polecenia, zobacz [opcje wiersza polecenia związane z usługą][MongoWindowsSvcOptions].</span><span class="sxs-lookup"><span data-stu-id="dabaa-129">For more service-related command-line options, see [Service-related command-line options][MongoWindowsSvcOptions].</span></span>

    <span data-ttu-id="dabaa-130">toostart hello usługi, uruchom to polecenie:</span><span class="sxs-lookup"><span data-stu-id="dabaa-130">toostart hello service, run this command:</span></span>

        C:\> net start MongoDB
10. <span data-ttu-id="dabaa-131">Bazy danych MongoDB jest zainstalowana i uruchomiona, należy tooopen port w Zaporze systemu Windows można zdalnie więc połączenie tooMongoDB.</span><span class="sxs-lookup"><span data-stu-id="dabaa-131">Now that MongoDB is installed and running, you need tooopen a port in Windows Firewall so you can remotely connect tooMongoDB.</span></span>  <span data-ttu-id="dabaa-132">Z hello **Start** menu, wybierz opcję **narzędzia administracyjne** , a następnie **Zapora systemu Windows z zabezpieczeniami zaawansowanymi**.</span><span class="sxs-lookup"><span data-stu-id="dabaa-132">From hello **Start** menu, select **Administrative Tools** and then **Windows Firewall with Advanced Security**.</span></span>
11. <span data-ttu-id="dabaa-133">() w okienku po lewej stronie powitania, wybierz **reguły ruchu przychodzącego**.</span><span class="sxs-lookup"><span data-stu-id="dabaa-133">a) In hello left pane, select **Inbound Rules**.</span></span>  <span data-ttu-id="dabaa-134">W hello **akcje** okienku na powitania po prawej, wybierz opcję **nową regułę...** .</span><span class="sxs-lookup"><span data-stu-id="dabaa-134">In hello **Actions** pane on hello right, select **New Rule...**.</span></span>

    ![Zapora systemu Windows][Image1]

    <span data-ttu-id="dabaa-136">(b) w hello **Kreatora nowej reguły przychodzącej**, wybierz pozycję **portu** , a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="dabaa-136">b) In hello **New Inbound Rule Wizard**, select **Port** and then click **Next**.</span></span>

    ![Zapora systemu Windows][Image2]

    <span data-ttu-id="dabaa-138">c) wybierz **TCP** , a następnie **określone porty lokalne**.</span><span class="sxs-lookup"><span data-stu-id="dabaa-138">c) Select **TCP** and then **Specific local ports**.</span></span>  <span data-ttu-id="dabaa-139">Określ port "27017" (port domyślny hello nasłuchuje bazy danych MongoDB), a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="dabaa-139">Specify a port of "27017" (hello default port MongoDB listens on) and click **Next**.</span></span>

    ![Zapora systemu Windows][Image3]

    <span data-ttu-id="dabaa-141">d) wybierz **przyłączenia hello** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="dabaa-141">d) Select **Allow hello connection** and click **Next**.</span></span>

    ![Zapora systemu Windows][Image4]

    <span data-ttu-id="dabaa-143">e) kliknij **dalej** ponownie.</span><span class="sxs-lookup"><span data-stu-id="dabaa-143">e) Click **Next** again.</span></span>

    ![Zapora systemu Windows][Image5]

    <span data-ttu-id="dabaa-145">f) określ nazwę reguły hello, takie jak "MongoPort", a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="dabaa-145">f) Specify a name for hello rule, such as "MongoPort", and click **Finish**.</span></span>

    ![Zapora systemu Windows][Image6]

12. <span data-ttu-id="dabaa-147">Jeśli podczas tworzenia maszyny wirtualnej hello nie konfigurowania punktu końcowego dla bazy danych MongoDB, możesz to zrobić teraz.</span><span class="sxs-lookup"><span data-stu-id="dabaa-147">If you didn't configure an endpoint for MongoDB when you created hello virtual machine, you can do it now.</span></span> <span data-ttu-id="dabaa-148">Wymagane zarówno hello regułę zapory i hello punktu końcowego toobe stanie tooconnect tooMongoDB zdalnie.</span><span class="sxs-lookup"><span data-stu-id="dabaa-148">You need both hello firewall rule and hello endpoint toobe able tooconnect tooMongoDB remotely.</span></span>

  <span data-ttu-id="dabaa-149">W portalu Azure hello, kliknij przycisk **maszyn wirtualnych (klasyczne)**, kliknij nazwę hello nowej maszyny wirtualnej, a następnie kliknij przycisk **punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="dabaa-149">In hello Azure portal, click **Virtual Machines (classic)**, click hello name of your new virtual machine, and then click **Endpoints**.</span></span>

    ![Punkty końcowe][Image7]

13. <span data-ttu-id="dabaa-151">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="dabaa-151">Click **Add**.</span></span>

14. <span data-ttu-id="dabaa-152">Dodawanie punktu końcowego o nazwie "Mongo" protokołu **TCP**, a oba **publicznego** i **prywatnej** porty zestaw zbyt "27017".</span><span class="sxs-lookup"><span data-stu-id="dabaa-152">Add an endpoint with name "Mongo", protocol **TCP**, and both **Public** and **Private** ports set too"27017".</span></span> <span data-ttu-id="dabaa-153">Otwierania tego portu umożliwia zdalny dostęp do toobe bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="dabaa-153">Opening this port allows MongoDB toobe accessed remotely.</span></span>

    ![Punkty końcowe][Image9]

> [!NOTE]
> <span data-ttu-id="dabaa-155">Hello port 27017 hello domyślny port jest używany przez bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="dabaa-155">hello port 27017 is hello default port used by MongoDB.</span></span> <span data-ttu-id="dabaa-156">Ten port domyślny można zmienić, określając hello `--port` parametru podczas uruchamiania serwera mongod.exe hello.</span><span class="sxs-lookup"><span data-stu-id="dabaa-156">You can change this default port by specifying hello `--port` parameter when starting hello mongod.exe server.</span></span> <span data-ttu-id="dabaa-157">Upewnij się, że toogive hello tego samego numeru portu w zaporze hello i hello punktu końcowego "Mongo" w hello poprzedzających instrukcji.</span><span class="sxs-lookup"><span data-stu-id="dabaa-157">Make sure toogive hello same port number in hello firewall and hello "Mongo" endpoint in hello preceding instructions.</span></span>
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
