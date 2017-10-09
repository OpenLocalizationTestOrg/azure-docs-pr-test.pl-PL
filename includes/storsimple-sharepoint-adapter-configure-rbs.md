<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> Podczas wprowadzania zmian toohello karty StorSimple konfiguracji SPZ programu SharePoint, użytkownik musi być zalogowany przy użyciu konta użytkownika, który należy do grupy Administratorzy domeny toohello. Ponadto należy dostęp do strony konfiguracji hello przeglądarce uruchomionej na powitania sam hosta jako administracji centralnej.
> 
> 

#### <a name="tooconfigure-rbs"></a>tooconfigure SPZ
1. Otwórz stronę Administracja centralna programu SharePoint hello i przeglądanie za**ustawienia systemu**. 
2. W hello **Azure StorSimple** kliknij **skonfigurować karty StorSimple**.
   
    ![Skonfiguruj hello karty StorSimple](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. Na powitania **skonfigurować karty StorSimple** strony:
   
   1. Upewnij się, że hello **włączyć edycji ścieżki** pole wyboru jest zaznaczone.
   2. W polu tekstowym hello wpisz ścieżkę Universal Naming Convention (UNC) hello hello magazynu obiektów BLOB.
      
      > [!NOTE]
      > wolumin magazynu obiektów BLOB Hello musi być hostowany na woluminie iSCSI skonfigurowane na urządzeniu StorSimple hello.

   3. Kliknij przycisk hello **włączyć** znajdujący się poniżej wszystkich zawartości baz danych hello mają tooconfigure dla zdalnego magazynu.
      
      > [!NOTE]
      > Magazyn obiektów BLOB Hello musi być udostępniony i jest osiągalny przez wszystkie serwery sieci web frontonu (WFE), a hello konta użytkownika, który jest skonfigurowany dla farmy serwerów programu SharePoint hello musi mieć dostęp do udziału toohello.
      
      ![Włącz hello SPZ dostawcy](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      Po włączeniu lub wyłączeniu SPZ, pojawi się także hello następującą wiadomości.
      
      ![Skonfiguruj StorSimple karty włączenia wyłączenia](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. Kliknij przycisk hello **aktualizacji** przycisk tooapply hello konfiguracji. Po kliknięciu hello **aktualizacji** przycisku hello SPZ konfiguracji stan zostanie zaktualizowany na wszystkich serwerach WFE i hello całej farmy zostaną włączone SPZ. zostanie wyświetlone następujące wiadomość Hello.
      
      ![Komunikat adaptera konfiguracji](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > Jeśli konfigurujesz SPZ farmy programu SharePoint o bardzo dużej liczby baz danych (większe niż 200), strony sieci web Administracja centralna programu SharePoint hello może upłynął limit czasu. Jeśli to miejsce, Odśwież stronę hello. Nie dotyczy to proces konfiguracji hello.

4. Sprawdź konfigurację hello:
   
   1. Zaloguj się w witrynie Administracja centralna programu SharePoint toohello i Przeglądaj toohello **skonfigurować karty StorSimple** strony.
   2. Sprawdź toomake szczegóły konfiguracji hello się upewnić, że są one zgodne hello ustawienia, które zostały wprowadzone. 
5. Sprawdź, czy SPZ działa prawidłowo:
   
   1. Przekaż tooSharePoint dokumentu. 
   2. Przeglądaj toohello ścieżkę UNC, który został skonfigurowany. Upewnij się, że struktura katalogów SPZ hello został utworzony i czy zawiera hello przekazany obiekt.
6. (Opcjonalnie) Można użyć hello RBS Microsoft `Migrate()` polecenia cmdlet programu PowerShell dołączony SharePoint toomigrate istniejących obiektów BLOB toohello zawartości urządzenia StorSimple. Aby uzyskać więcej informacji, zobacz [migrowania zawartości do lub wychodzący SPZ w SharePoint 2013] [ 6] lub [migrowania zawartości do lub wychodzący SPZ (SharePoint Foundation 2010)] [7].
7. (Opcjonalnie) W instalacjach testu można sprawdzić, czy obiekty BLOB hello zostały przeniesione z bazy danych zawartości hello w następujący sposób: 
   
   1. Uruchom program SQL Management Studio.
   2. Uruchom zapytanie ListBlobsInDB_2010.sql lub ListBlobsInDB_2013.sql hello w następujący sposób.
      
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
      
      Jeśli SPZ został skonfigurowany prawidłowo, wartości NULL powinny być wyświetlane w kolumnie SizeOfContentInDB powitania dla dowolnego obiektu, który został przekazany pomyślnie externalized z SPZ.
8. (Opcjonalnie) Po skonfigurowaniu SPZ i Przenieś wszystkie zawartości obiektu BLOB toohello urządzenia StorSimple można przenieść hello bazy danych zawartości toohello urządzenia. Jeśli bazy danych zawartości hello toomove, zaleca się konfigurowanie hello magazynu bazy danych zawartości na urządzeniu powitania jako podstawowego wolumin. Następnie użyj ustalona programu SQL Server najlepsze praktyki urządzenia StorSimple toohello toomigrate hello bazy danych zawartości. 
   
   > [!NOTE]
   > Przenoszenie urządzenia toohello bazy danych zawartości hello jest obsługiwana tylko dla serii StorSimple 8000 hello (jest nieobsługiwany dla serii hello 5000 i 7000).
   
   Jeśli obiekty BLOB i bazy danych zawartości hello są przechowywane w oddzielnych woluminach na urządzeniu StorSimple hello, zaleca się skonfigurować je w hello tego samego kontenera woluminów. Dzięki temu one zostanie ono utworzenia kopii zapasowej razem.
   
   > [!WARNING]
   > Jeśli nie włączono SPZ, nie zaleca się przenoszenie urządzenia StorSimple toohello bazy danych zawartości hello. To jest Konfiguracja zastosowaniem.
   
9. Następnym krokiem Przejdź toohello: [skonfigurować wyrzucanie elementów bezużytecznych](#configure-garbage-collection).

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
