<!--author=SharS last changed: 9/17/15-->

W tej procedurze obejmują:

1. [Przygotuj plik wykonywalny Element utrzymujący hello toorun](#to-prepare-to-run-the-maintainer) .
2. [Przygotowanie bazy danych zawartości hello i Kosza do natychmiastowego usunięcia obiektów blob oddzielone](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).
3. [Uruchom Maintainer.exe](#to-run-the-maintainer).
4. [Przywrócenie bazy danych zawartości hello i ustawień Kosza](#to-revert-the-content-database-and-recycle-bin-settings).

#### <a name="tooprepare-toorun-hello-maintainer"></a>Witaj toorun tooprepare Element utrzymujący
1. Na serwerze frontonu sieci Web hello Otwórz hello powłoki zarządzania programu SharePoint 2013 jako administrator.
2. Przejdź do folderu toohello *dysk rozruchowy*: \Program Files\Microsoft 10.50\Maintainer zdalnego magazynu obiektów Blob SQL\.
3. Zmień nazwę **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** za**web.config**.
4. Użyj `aspnet_regiis -pdf connectionStrings` pliku web.config hello toodecrypt.
5. W pliku web.config odszyfrowane hello, w obszarze hello `connectionStrings` węzła, Dodaj hello ciąg połączenia dla wystąpienia programu SQL server i hello Nazwa bazy danych zawartości. Zobacz poniższy przykład hello.
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. Użyj `aspnet_regiis –pef connectionStrings` toore-szyfrowania hello pliku web.config. 
7. Zmień nazwę pliku web.config tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config. 

#### <a name="tooprepare-hello-content-database-and-recycle-bin-tooimmediately-delete-orphaned-blobs"></a>bazy danych zawartości hello tooprepare i tooimmediately Kosza usuwanie osieroconych obiektów blob
1. Uruchom powitania po aktualizacji kwerendy dla bazy danych zawartości docelowy hello na powitania programu SQL Server w programie SQL Management Studio: 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. Na powitania serwera sieci web frontonu, w obszarze **administracji centralnej**, Edytuj hello **ustawienia ogólne aplikacji sieci Web** dla hello potrzeby bazy danych zawartości tootemporarily Wyłącz hello Kosza. Ta akcja spowoduje również pusty hello Kosza dla dowolnej kolekcji powiązaną lokacją. toodo tego, kliknij **administracji centralnej** -> **Zarządzanie aplikacjami** -> **aplikacji sieci Web (Zarządzaj aplikacji sieci web)**  ->  **SharePoint — 80** -> **ogólne aplikacji ustawienia**. Zestaw hello **Odtwórz stan Bin** za**OFF**.
   
    ![Ustawienia ogólne aplikacji sieci Web](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="toorun-hello-maintainer"></a>Witaj toorun Element utrzymujący
* Na serwerze frontonu sieci web hello w hello powłoki zarządzania programu SharePoint 2013, uruchom hello Element utrzymujący w następujący sposób:
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > Tylko hello `GarbageCollection` operacja jest obsługiwana dla urządzenia StorSimple w tej chwili. Należy również zauważyć, że parametry hello wystawiony dla Microsoft.Data.SqlRemoteBlobs.Maintainer.exe jest uwzględniana wielkość liter. 
  > 
  > 

#### <a name="toorevert-hello-content-database-and-recycle-bin-settings"></a>Baza danych zawartości hello toorevert i ustawień Kosza
1. Uruchom powitania po aktualizacji kwerendy dla bazy danych zawartości docelowy hello na powitania programu SQL Server w programie SQL Management Studio:
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. Na serwerze frontonu sieci web hello w **administracji centralnej**, Edytuj hello **ustawienia ogólne aplikacji sieci Web** dla hello potrzeby bazy danych zawartości hello toore Włączanie Kosza. toodo tego, kliknij **administracji centralnej** -> **Zarządzanie aplikacjami** -> **aplikacji sieci Web (Zarządzaj aplikacji sieci web)**  ->  **SharePoint — 80** -> **ogólne aplikacji ustawienia**. Ustaw hello Odtwórz stan Bin zbyt**ON**.

