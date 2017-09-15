<!--author=SharS last changed: 9/17/15-->

<span data-ttu-id="f8595-101">W tej procedurze obejmują:</span><span class="sxs-lookup"><span data-stu-id="f8595-101">In this procedure, you will:</span></span>

1. <span data-ttu-id="f8595-102">[Przygotowanie do uruchomienia pliku wykonywalnego Element utrzymujący](#to-prepare-to-run-the-maintainer) .</span><span class="sxs-lookup"><span data-stu-id="f8595-102">[Prepare to run the Maintainer executable](#to-prepare-to-run-the-maintainer) .</span></span>
2. <span data-ttu-id="f8595-103">[Przygotowanie bazy danych zawartości i Kosza do natychmiastowego usunięcia obiektów blob oddzielone](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span><span class="sxs-lookup"><span data-stu-id="f8595-103">[Prepare the content database and Recycle Bin for immediate deletion of orphaned BLOBs](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span></span>
3. <span data-ttu-id="f8595-104">[Uruchom Maintainer.exe](#to-run-the-maintainer).</span><span class="sxs-lookup"><span data-stu-id="f8595-104">[Run Maintainer.exe](#to-run-the-maintainer).</span></span>
4. <span data-ttu-id="f8595-105">[Przywróć bazę danych zawartości i ustawienia Kosza](#to-revert-the-content-database-and-recycle-bin-settings).</span><span class="sxs-lookup"><span data-stu-id="f8595-105">[Revert the content database and Recycle Bin settings](#to-revert-the-content-database-and-recycle-bin-settings).</span></span>

#### <a name="to-prepare-to-run-the-maintainer"></a><span data-ttu-id="f8595-106">Aby przygotować się do uruchomienia Element utrzymujący</span><span class="sxs-lookup"><span data-stu-id="f8595-106">To prepare to run the Maintainer</span></span>
1. <span data-ttu-id="f8595-107">Na serwerze frontonu sieci Web Otwórz powłokę zarządzania programu SharePoint 2013 jako administrator.</span><span class="sxs-lookup"><span data-stu-id="f8595-107">On the Web front-end server, open the SharePoint 2013 Management Shell as an administrator.</span></span>
2. <span data-ttu-id="f8595-108">Przejdź do folderu *dysk rozruchowy*: \Program Files\Microsoft 10.50\Maintainer zdalnego magazynu obiektów Blob SQL\.</span><span class="sxs-lookup"><span data-stu-id="f8595-108">Navigate to the folder *boot drive*:\Program Files\Microsoft SQL Remote Blob Storage 10.50\Maintainer\.</span></span>
3. <span data-ttu-id="f8595-109">Zmień nazwę **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** do **web.config**.</span><span class="sxs-lookup"><span data-stu-id="f8595-109">Rename **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** to **web.config**.</span></span>
4. <span data-ttu-id="f8595-110">Użyj `aspnet_regiis -pdf connectionStrings` do odszyfrowywania pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="f8595-110">Use `aspnet_regiis -pdf connectionStrings` to decrypt the web.config file.</span></span>
5. <span data-ttu-id="f8595-111">W pliku web.config odszyfrowane w obszarze `connectionStrings` węzła, Dodaj parametry połączenia dla wystąpienia programu SQL server i nazwę bazy danych zawartości.</span><span class="sxs-lookup"><span data-stu-id="f8595-111">In the decrypted web.config file, under the `connectionStrings` node, add the connection string for your SQL server instance and the content database name.</span></span> <span data-ttu-id="f8595-112">Zobacz poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="f8595-112">See the following example.</span></span>
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. <span data-ttu-id="f8595-113">Użyj `aspnet_regiis –pef connectionStrings` zaszyfrowanie pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="f8595-113">Use `aspnet_regiis –pef connectionStrings` to re-encrypt the web.config file.</span></span> 
7. <span data-ttu-id="f8595-114">Zmień nazwę pliku web.config na Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config.</span><span class="sxs-lookup"><span data-stu-id="f8595-114">Rename web.config to Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config.</span></span> 

#### <a name="to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs"></a><span data-ttu-id="f8595-115">Aby przygotować zawartość bazy danych i Kosza można natychmiast usunąć oddzielone obiektów blob</span><span class="sxs-lookup"><span data-stu-id="f8595-115">To prepare the content database and Recycle Bin to immediately delete orphaned BLOBs</span></span>
1. <span data-ttu-id="f8595-116">Na serwerze SQL w programie SQL Management Studio, uruchomić następujące kwerendy aktualizacji dla docelowej bazy danych zawartości:</span><span class="sxs-lookup"><span data-stu-id="f8595-116">On the SQL Server, in SQL Management Studio, run the following update queries for the target content database:</span></span> 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. <span data-ttu-id="f8595-117">Na serwerze frontonu sieci web w obszarze **administracji centralnej**, Edytuj **ustawienia ogólne aplikacji sieci Web** dla żądanej zawartości bazy danych można tymczasowo wyłączyć Kosza.</span><span class="sxs-lookup"><span data-stu-id="f8595-117">On the web front-end server, under **Central Administration**, edit the **Web Application General Settings** for the desired content database to temporarily disable the Recycle Bin.</span></span> <span data-ttu-id="f8595-118">Ta akcja spowoduje usunięcie również zawartości Kosza na wszystkie powiązane zbiorach witryn.</span><span class="sxs-lookup"><span data-stu-id="f8595-118">This action will also empty the Recycle Bin for any related site collections.</span></span> <span data-ttu-id="f8595-119">Aby to zrobić, kliknij przycisk **administracji centralnej** -> **Zarządzanie aplikacjami** -> **aplikacji sieci Web (Zarządzaj aplikacji sieci web)**  ->  **SharePoint — 80** -> **ogólne aplikacji ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="f8595-119">To do this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="f8595-120">Ustaw **stan Kosza** do **OFF**.</span><span class="sxs-lookup"><span data-stu-id="f8595-120">Set the **Recycle Bin Status** to **OFF**.</span></span>
   
    ![Ustawienia ogólne aplikacji sieci Web](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="to-run-the-maintainer"></a><span data-ttu-id="f8595-122">Aby uruchomić Element utrzymujący</span><span class="sxs-lookup"><span data-stu-id="f8595-122">To run the Maintainer</span></span>
* <span data-ttu-id="f8595-123">Na serwerze frontonu sieci web w powłoce zarządzania programu SharePoint 2013, uruchom Element utrzymujący w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f8595-123">On the web front-end server, in the SharePoint 2013 Management Shell, run the Maintainer as follows:</span></span>
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > <span data-ttu-id="f8595-124">Tylko `GarbageCollection` operacja jest obsługiwana dla urządzenia StorSimple w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="f8595-124">Only the `GarbageCollection` operation is supported for StorSimple at this time.</span></span> <span data-ttu-id="f8595-125">Należy również zauważyć, że parametry wystawiony dla Microsoft.Data.SqlRemoteBlobs.Maintainer.exe jest uwzględniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="f8595-125">Also note that the parameters issued for Microsoft.Data.SqlRemoteBlobs.Maintainer.exe are case sensitive.</span></span> 
  > 
  > 

#### <a name="to-revert-the-content-database-and-recycle-bin-settings"></a><span data-ttu-id="f8595-126">Aby przywrócić bazę danych zawartości i ustawienia Kosza</span><span class="sxs-lookup"><span data-stu-id="f8595-126">To revert the content database and Recycle Bin settings</span></span>
1. <span data-ttu-id="f8595-127">Na serwerze SQL w programie SQL Management Studio, uruchomić następujące kwerendy aktualizacji dla docelowej bazy danych zawartości:</span><span class="sxs-lookup"><span data-stu-id="f8595-127">On the SQL Server, in SQL Management Studio, run the following update queries for the target content database:</span></span>
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. <span data-ttu-id="f8595-128">Na serwerze frontonu sieci web w **administracji centralnej**, Edytuj **ustawienia ogólne aplikacji sieci Web** dla żądanej zawartości bazy danych do ponownego włączania Kosza.</span><span class="sxs-lookup"><span data-stu-id="f8595-128">On the web front-end server, in **Central Administration**, edit the **Web Application General Settings** for the desired content database to re-enable the Recycle Bin.</span></span> <span data-ttu-id="f8595-129">Aby to zrobić, kliknij przycisk **administracji centralnej** -> **Zarządzanie aplikacjami** -> **aplikacji sieci Web (Zarządzaj aplikacji sieci web)**  ->  **SharePoint — 80** -> **ogólne aplikacji ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="f8595-129">To do this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="f8595-130">Ustaw stan Bin odtworzenia **ON**.</span><span class="sxs-lookup"><span data-stu-id="f8595-130">Set the Recycle Bin Status to **ON**.</span></span>

