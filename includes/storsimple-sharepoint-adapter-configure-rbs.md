<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> <span data-ttu-id="26ab0-101">Podczas wprowadzania zmian toohello karty StorSimple konfiguracji SPZ programu SharePoint, użytkownik musi być zalogowany przy użyciu konta użytkownika, który należy do grupy Administratorzy domeny toohello.</span><span class="sxs-lookup"><span data-stu-id="26ab0-101">When making changes toohello StorSimple Adapter for SharePoint RBS configuration, you must be logged on with a user account that belongs toohello Domain Admins group.</span></span> <span data-ttu-id="26ab0-102">Ponadto należy dostęp do strony konfiguracji hello przeglądarce uruchomionej na powitania sam hosta jako administracji centralnej.</span><span class="sxs-lookup"><span data-stu-id="26ab0-102">Additionally, you must access hello configuration page from a browser running on hello same host as Central Administration.</span></span>
> 
> 

#### <a name="tooconfigure-rbs"></a><span data-ttu-id="26ab0-103">tooconfigure SPZ</span><span class="sxs-lookup"><span data-stu-id="26ab0-103">tooconfigure RBS</span></span>
1. <span data-ttu-id="26ab0-104">Otwórz stronę Administracja centralna programu SharePoint hello i przeglądanie za**ustawienia systemu**.</span><span class="sxs-lookup"><span data-stu-id="26ab0-104">Open hello SharePoint Central Administration page, and browse too**System Settings**.</span></span> 
2. <span data-ttu-id="26ab0-105">W hello **Azure StorSimple** kliknij **skonfigurować karty StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="26ab0-105">In hello **Azure StorSimple** section, click **Configure StorSimple Adapter**.</span></span>
   
    ![Skonfiguruj hello karty StorSimple](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. <span data-ttu-id="26ab0-107">Na powitania **skonfigurować karty StorSimple** strony:</span><span class="sxs-lookup"><span data-stu-id="26ab0-107">On hello **Configure StorSimple Adapter** page:</span></span>
   
   1. <span data-ttu-id="26ab0-108">Upewnij się, że hello **włączyć edycji ścieżki** pole wyboru jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="26ab0-108">Make sure that hello **Enable editing path** check box is selected.</span></span>
   2. <span data-ttu-id="26ab0-109">W polu tekstowym hello wpisz ścieżkę Universal Naming Convention (UNC) hello hello magazynu obiektów BLOB.</span><span class="sxs-lookup"><span data-stu-id="26ab0-109">In hello text box, type hello Universal Naming Convention (UNC) path of hello BLOB store.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="26ab0-110">wolumin magazynu obiektów BLOB Hello musi być hostowany na woluminie iSCSI skonfigurowane na urządzeniu StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="26ab0-110">hello BLOB store volume must be hosted on an iSCSI volume configured on hello StorSimple device.</span></span>

   3. <span data-ttu-id="26ab0-111">Kliknij przycisk hello **włączyć** znajdujący się poniżej wszystkich zawartości baz danych hello mają tooconfigure dla zdalnego magazynu.</span><span class="sxs-lookup"><span data-stu-id="26ab0-111">Click hello **Enable** button below each of hello content databases that you want tooconfigure for remote storage.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="26ab0-112">Magazyn obiektów BLOB Hello musi być udostępniony i jest osiągalny przez wszystkie serwery sieci web frontonu (WFE), a hello konta użytkownika, który jest skonfigurowany dla farmy serwerów programu SharePoint hello musi mieć dostęp do udziału toohello.</span><span class="sxs-lookup"><span data-stu-id="26ab0-112">hello BLOB store must be shared and reachable by all web front-end (WFE) servers, and hello user account that is configured for hello SharePoint server farm must have access toohello share.</span></span>
      
      ![Włącz hello SPZ dostawcy](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      <span data-ttu-id="26ab0-114">Po włączeniu lub wyłączeniu SPZ, pojawi się także hello następującą wiadomości.</span><span class="sxs-lookup"><span data-stu-id="26ab0-114">When you enable or disable RBS, you will also see hello following message.</span></span>
      
      ![Skonfiguruj StorSimple karty włączenia wyłączenia](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. <span data-ttu-id="26ab0-116">Kliknij przycisk hello **aktualizacji** przycisk tooapply hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="26ab0-116">Click hello **Update** button tooapply hello configuration.</span></span> <span data-ttu-id="26ab0-117">Po kliknięciu hello **aktualizacji** przycisku hello SPZ konfiguracji stan zostanie zaktualizowany na wszystkich serwerach WFE i hello całej farmy zostaną włączone SPZ.</span><span class="sxs-lookup"><span data-stu-id="26ab0-117">When you click hello **Update** button, hello RBS configuration status will be updated on all WFE servers, and hello entire farm will be RBS-enabled.</span></span> <span data-ttu-id="26ab0-118">zostanie wyświetlone następujące wiadomość Hello.</span><span class="sxs-lookup"><span data-stu-id="26ab0-118">hello following message appears.</span></span>
      
      ![Komunikat adaptera konfiguracji](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > <span data-ttu-id="26ab0-120">Jeśli konfigurujesz SPZ farmy programu SharePoint o bardzo dużej liczby baz danych (większe niż 200), strony sieci web Administracja centralna programu SharePoint hello może upłynął limit czasu. Jeśli to miejsce, Odśwież stronę hello.</span><span class="sxs-lookup"><span data-stu-id="26ab0-120">If you are configuring RBS for a SharePoint farm with a very large number of databases (greater than 200), hello SharePoint Central Administration web page might time out. If that occurs, refresh hello page.</span></span> <span data-ttu-id="26ab0-121">Nie dotyczy to proces konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="26ab0-121">This does not affect hello configuration process.</span></span>

4. <span data-ttu-id="26ab0-122">Sprawdź konfigurację hello:</span><span class="sxs-lookup"><span data-stu-id="26ab0-122">Verify hello configuration:</span></span>
   
   1. <span data-ttu-id="26ab0-123">Zaloguj się w witrynie Administracja centralna programu SharePoint toohello i Przeglądaj toohello **skonfigurować karty StorSimple** strony.</span><span class="sxs-lookup"><span data-stu-id="26ab0-123">Log on toohello SharePoint Central Administration website, and browse toohello **Configure StorSimple Adapter** page.</span></span>
   2. <span data-ttu-id="26ab0-124">Sprawdź toomake szczegóły konfiguracji hello się upewnić, że są one zgodne hello ustawienia, które zostały wprowadzone.</span><span class="sxs-lookup"><span data-stu-id="26ab0-124">Check hello configuration details toomake sure that they match hello settings that you entered.</span></span> 
5. <span data-ttu-id="26ab0-125">Sprawdź, czy SPZ działa prawidłowo:</span><span class="sxs-lookup"><span data-stu-id="26ab0-125">Verify that RBS works correctly:</span></span>
   
   1. <span data-ttu-id="26ab0-126">Przekaż tooSharePoint dokumentu.</span><span class="sxs-lookup"><span data-stu-id="26ab0-126">Upload a document tooSharePoint.</span></span> 
   2. <span data-ttu-id="26ab0-127">Przeglądaj toohello ścieżkę UNC, który został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="26ab0-127">Browse toohello UNC path that you configured.</span></span> <span data-ttu-id="26ab0-128">Upewnij się, że struktura katalogów SPZ hello został utworzony i czy zawiera hello przekazany obiekt.</span><span class="sxs-lookup"><span data-stu-id="26ab0-128">Make sure that hello RBS directory structure was created and that it contains hello uploaded object.</span></span>
6. <span data-ttu-id="26ab0-129">(Opcjonalnie) Można użyć hello RBS Microsoft `Migrate()` polecenia cmdlet programu PowerShell dołączony SharePoint toomigrate istniejących obiektów BLOB toohello zawartości urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="26ab0-129">(Optional) You can use hello Microsoft RBS `Migrate()` PowerShell cmdlet included with SharePoint toomigrate existing BLOB content toohello StorSimple device.</span></span> <span data-ttu-id="26ab0-130">Aby uzyskać więcej informacji, zobacz [migrowania zawartości do lub wychodzący SPZ w SharePoint 2013] [ 6] lub [migrowania zawartości do lub wychodzący SPZ (SharePoint Foundation 2010)] [7].</span><span class="sxs-lookup"><span data-stu-id="26ab0-130">For more information, see [Migrate content into or out of RBS in SharePoint 2013][6] or [Migrate content into or out of RBS (SharePoint Foundation 2010)][7].</span></span>
7. <span data-ttu-id="26ab0-131">(Opcjonalnie) W instalacjach testu można sprawdzić, czy obiekty BLOB hello zostały przeniesione z bazy danych zawartości hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="26ab0-131">(Optional) On test installations, you can verify that hello BLOBs were moved out of hello content database as follows:</span></span> 
   
   1. <span data-ttu-id="26ab0-132">Uruchom program SQL Management Studio.</span><span class="sxs-lookup"><span data-stu-id="26ab0-132">Start SQL Management Studio.</span></span>
   2. <span data-ttu-id="26ab0-133">Uruchom zapytanie ListBlobsInDB_2010.sql lub ListBlobsInDB_2013.sql hello w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="26ab0-133">Run hello ListBlobsInDB_2010.sql or ListBlobsInDB_2013.sql query, as follows.</span></span>
      
      ```
      **ListBlobsInDB_2013.sql**
      
        USE WSS_Content
        GO
      
        SELECT DocStreams.DocId,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               DocStreams.RbsId,
               TimeLastModified
      
        FROM DocStreams
      
             INNER JOIN AllDocs ON DocStreams.DocId = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      
      **ListBlobsInDB_2010.sql**
      
        USE WSS_Content
        GO
      
        SELECT AllDocStreams.Id,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               RbsId,
               TimeLastModified
        FROM AllDocStreams
      
             INNER JOIN AllDocs ON AllDocStreams.Id = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      ```
      
      <span data-ttu-id="26ab0-134">Jeśli SPZ został skonfigurowany prawidłowo, wartości NULL powinny być wyświetlane w kolumnie SizeOfContentInDB powitania dla dowolnego obiektu, który został przekazany pomyślnie externalized z SPZ.</span><span class="sxs-lookup"><span data-stu-id="26ab0-134">If RBS was configured correctly, a NULL value should appear in hello SizeOfContentInDB column for any object that was uploaded and successfully externalized with RBS.</span></span>
8. <span data-ttu-id="26ab0-135">(Opcjonalnie) Po skonfigurowaniu SPZ i Przenieś wszystkie zawartości obiektu BLOB toohello urządzenia StorSimple można przenieść hello bazy danych zawartości toohello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="26ab0-135">(Optional) After you configure RBS and move all BLOB content toohello StorSimple device, you can move hello content database toohello device.</span></span> <span data-ttu-id="26ab0-136">Jeśli bazy danych zawartości hello toomove, zaleca się konfigurowanie hello magazynu bazy danych zawartości na urządzeniu powitania jako podstawowego wolumin.</span><span class="sxs-lookup"><span data-stu-id="26ab0-136">If you choose toomove hello content database, we recommend that you configure hello content database storage on hello device as a primary volume.</span></span> <span data-ttu-id="26ab0-137">Następnie użyj ustalona programu SQL Server najlepsze praktyki urządzenia StorSimple toohello toomigrate hello bazy danych zawartości.</span><span class="sxs-lookup"><span data-stu-id="26ab0-137">Then, use established SQL Server best practices toomigrate hello content database toohello StorSimple device.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="26ab0-138">Przenoszenie urządzenia toohello bazy danych zawartości hello jest obsługiwana tylko dla serii StorSimple 8000 hello (jest nieobsługiwany dla serii hello 5000 i 7000).</span><span class="sxs-lookup"><span data-stu-id="26ab0-138">Moving hello content database toohello device is only supported for hello StorSimple 8000 series (it is not supported for hello 5000 or 7000 series).</span></span>
   
   <span data-ttu-id="26ab0-139">Jeśli obiekty BLOB i bazy danych zawartości hello są przechowywane w oddzielnych woluminach na urządzeniu StorSimple hello, zaleca się skonfigurować je w hello tego samego kontenera woluminów.</span><span class="sxs-lookup"><span data-stu-id="26ab0-139">If you store BLOBs and hello content database in separate volumes on hello StorSimple device, we recommend that you configure them in hello same volume container.</span></span> <span data-ttu-id="26ab0-140">Dzięki temu one zostanie ono utworzenia kopii zapasowej razem.</span><span class="sxs-lookup"><span data-stu-id="26ab0-140">This ensures that they will be backed up together.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="26ab0-141">Jeśli nie włączono SPZ, nie zaleca się przenoszenie urządzenia StorSimple toohello bazy danych zawartości hello.</span><span class="sxs-lookup"><span data-stu-id="26ab0-141">If you have not enabled RBS, we do not recommend moving hello content database toohello StorSimple device.</span></span> <span data-ttu-id="26ab0-142">To jest Konfiguracja zastosowaniem.</span><span class="sxs-lookup"><span data-stu-id="26ab0-142">This is an untested configuration.</span></span>
   
9. <span data-ttu-id="26ab0-143">Następnym krokiem Przejdź toohello: [skonfigurować wyrzucanie elementów bezużytecznych](#configure-garbage-collection).</span><span class="sxs-lookup"><span data-stu-id="26ab0-143">Go toohello next step: [Configure garbage collection](#configure-garbage-collection).</span></span>

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
