<!--author=SharS last changed: 9/17/15-->

<span data-ttu-id="896e7-101">W tej procedurze obejmują:</span><span class="sxs-lookup"><span data-stu-id="896e7-101">In this procedure, you will:</span></span>

1. <span data-ttu-id="896e7-102">[Przygotuj plik wykonywalny Element utrzymujący hello toorun](#to-prepare-to-run-the-maintainer) .</span><span class="sxs-lookup"><span data-stu-id="896e7-102">[Prepare toorun hello Maintainer executable](#to-prepare-to-run-the-maintainer) .</span></span>
2. <span data-ttu-id="896e7-103">[Przygotowanie bazy danych zawartości hello i Kosza do natychmiastowego usunięcia obiektów blob oddzielone](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span><span class="sxs-lookup"><span data-stu-id="896e7-103">[Prepare hello content database and Recycle Bin for immediate deletion of orphaned BLOBs](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span></span>
3. <span data-ttu-id="896e7-104">[Uruchom Maintainer.exe](#to-run-the-maintainer).</span><span class="sxs-lookup"><span data-stu-id="896e7-104">[Run Maintainer.exe](#to-run-the-maintainer).</span></span>
4. <span data-ttu-id="896e7-105">[Przywrócenie bazy danych zawartości hello i ustawień Kosza](#to-revert-the-content-database-and-recycle-bin-settings).</span><span class="sxs-lookup"><span data-stu-id="896e7-105">[Revert hello content database and Recycle Bin settings](#to-revert-the-content-database-and-recycle-bin-settings).</span></span>

#### <a name="tooprepare-toorun-hello-maintainer"></a><span data-ttu-id="896e7-106">Witaj toorun tooprepare Element utrzymujący</span><span class="sxs-lookup"><span data-stu-id="896e7-106">tooprepare toorun hello Maintainer</span></span>
1. <span data-ttu-id="896e7-107">Na serwerze frontonu sieci Web hello Otwórz hello powłoki zarządzania programu SharePoint 2013 jako administrator.</span><span class="sxs-lookup"><span data-stu-id="896e7-107">On hello Web front-end server, open hello SharePoint 2013 Management Shell as an administrator.</span></span>
2. <span data-ttu-id="896e7-108">Przejdź do folderu toohello *dysk rozruchowy*: \Program Files\Microsoft 10.50\Maintainer zdalnego magazynu obiektów Blob SQL\.</span><span class="sxs-lookup"><span data-stu-id="896e7-108">Navigate toohello folder *boot drive*:\Program Files\Microsoft SQL Remote Blob Storage 10.50\Maintainer\.</span></span>
3. <span data-ttu-id="896e7-109">Zmień nazwę **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** za**web.config**.</span><span class="sxs-lookup"><span data-stu-id="896e7-109">Rename **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** too**web.config**.</span></span>
4. <span data-ttu-id="896e7-110">Użyj `aspnet_regiis -pdf connectionStrings` pliku web.config hello toodecrypt.</span><span class="sxs-lookup"><span data-stu-id="896e7-110">Use `aspnet_regiis -pdf connectionStrings` toodecrypt hello web.config file.</span></span>
5. <span data-ttu-id="896e7-111">W pliku web.config odszyfrowane hello, w obszarze hello `connectionStrings` węzła, Dodaj hello ciąg połączenia dla wystąpienia programu SQL server i hello Nazwa bazy danych zawartości.</span><span class="sxs-lookup"><span data-stu-id="896e7-111">In hello decrypted web.config file, under hello `connectionStrings` node, add hello connection string for your SQL server instance and hello content database name.</span></span> <span data-ttu-id="896e7-112">Zobacz poniższy przykład hello.</span><span class="sxs-lookup"><span data-stu-id="896e7-112">See hello following example.</span></span>
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. <span data-ttu-id="896e7-113">Użyj `aspnet_regiis –pef connectionStrings` toore-szyfrowania hello pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="896e7-113">Use `aspnet_regiis –pef connectionStrings` toore-encrypt hello web.config file.</span></span> 
7. <span data-ttu-id="896e7-114">Zmień nazwę pliku web.config tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config.</span><span class="sxs-lookup"><span data-stu-id="896e7-114">Rename web.config tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config.</span></span> 

#### <a name="tooprepare-hello-content-database-and-recycle-bin-tooimmediately-delete-orphaned-blobs"></a><span data-ttu-id="896e7-115">bazy danych zawartości hello tooprepare i tooimmediately Kosza usuwanie osieroconych obiektów blob</span><span class="sxs-lookup"><span data-stu-id="896e7-115">tooprepare hello content database and Recycle Bin tooimmediately delete orphaned BLOBs</span></span>
1. <span data-ttu-id="896e7-116">Uruchom powitania po aktualizacji kwerendy dla bazy danych zawartości docelowy hello na powitania programu SQL Server w programie SQL Management Studio:</span><span class="sxs-lookup"><span data-stu-id="896e7-116">On hello SQL Server, in SQL Management Studio, run hello following update queries for hello target content database:</span></span> 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. <span data-ttu-id="896e7-117">Na powitania serwera sieci web frontonu, w obszarze **administracji centralnej**, Edytuj hello **ustawienia ogólne aplikacji sieci Web** dla hello potrzeby bazy danych zawartości tootemporarily Wyłącz hello Kosza.</span><span class="sxs-lookup"><span data-stu-id="896e7-117">On hello web front-end server, under **Central Administration**, edit hello **Web Application General Settings** for hello desired content database tootemporarily disable hello Recycle Bin.</span></span> <span data-ttu-id="896e7-118">Ta akcja spowoduje również pusty hello Kosza dla dowolnej kolekcji powiązaną lokacją.</span><span class="sxs-lookup"><span data-stu-id="896e7-118">This action will also empty hello Recycle Bin for any related site collections.</span></span> <span data-ttu-id="896e7-119">toodo tego, kliknij **administracji centralnej** -> **Zarządzanie aplikacjami** -> **aplikacji sieci Web (Zarządzaj aplikacji sieci web)**  ->  **SharePoint — 80** -> **ogólne aplikacji ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="896e7-119">toodo this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="896e7-120">Zestaw hello **Odtwórz stan Bin** za**OFF**.</span><span class="sxs-lookup"><span data-stu-id="896e7-120">Set hello **Recycle Bin Status** too**OFF**.</span></span>
   
    ![Ustawienia ogólne aplikacji sieci Web](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="toorun-hello-maintainer"></a><span data-ttu-id="896e7-122">Witaj toorun Element utrzymujący</span><span class="sxs-lookup"><span data-stu-id="896e7-122">toorun hello Maintainer</span></span>
* <span data-ttu-id="896e7-123">Na serwerze frontonu sieci web hello w hello powłoki zarządzania programu SharePoint 2013, uruchom hello Element utrzymujący w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="896e7-123">On hello web front-end server, in hello SharePoint 2013 Management Shell, run hello Maintainer as follows:</span></span>
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > <span data-ttu-id="896e7-124">Tylko hello `GarbageCollection` operacja jest obsługiwana dla urządzenia StorSimple w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="896e7-124">Only hello `GarbageCollection` operation is supported for StorSimple at this time.</span></span> <span data-ttu-id="896e7-125">Należy również zauważyć, że parametry hello wystawiony dla Microsoft.Data.SqlRemoteBlobs.Maintainer.exe jest uwzględniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="896e7-125">Also note that hello parameters issued for Microsoft.Data.SqlRemoteBlobs.Maintainer.exe are case sensitive.</span></span> 
  > 
  > 

#### <a name="toorevert-hello-content-database-and-recycle-bin-settings"></a><span data-ttu-id="896e7-126">Baza danych zawartości hello toorevert i ustawień Kosza</span><span class="sxs-lookup"><span data-stu-id="896e7-126">toorevert hello content database and Recycle Bin settings</span></span>
1. <span data-ttu-id="896e7-127">Uruchom powitania po aktualizacji kwerendy dla bazy danych zawartości docelowy hello na powitania programu SQL Server w programie SQL Management Studio:</span><span class="sxs-lookup"><span data-stu-id="896e7-127">On hello SQL Server, in SQL Management Studio, run hello following update queries for hello target content database:</span></span>
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. <span data-ttu-id="896e7-128">Na serwerze frontonu sieci web hello w **administracji centralnej**, Edytuj hello **ustawienia ogólne aplikacji sieci Web** dla hello potrzeby bazy danych zawartości hello toore Włączanie Kosza.</span><span class="sxs-lookup"><span data-stu-id="896e7-128">On hello web front-end server, in **Central Administration**, edit hello **Web Application General Settings** for hello desired content database toore-enable hello Recycle Bin.</span></span> <span data-ttu-id="896e7-129">toodo tego, kliknij **administracji centralnej** -> **Zarządzanie aplikacjami** -> **aplikacji sieci Web (Zarządzaj aplikacji sieci web)**  ->  **SharePoint — 80** -> **ogólne aplikacji ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="896e7-129">toodo this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="896e7-130">Ustaw hello Odtwórz stan Bin zbyt**ON**.</span><span class="sxs-lookup"><span data-stu-id="896e7-130">Set hello Recycle Bin Status too**ON**.</span></span>

