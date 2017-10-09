<!--author=alkohli last changed: 9/17/15-->

#### <a name="tooadd-a-storage-account-in-storsimple-8000-series-update-10"></a>tooadd konta magazynu w StorSimple 8000 Series Update 1.0
1. Na stronie początkowej usługi Menedżer StorSimple hello wybierz usługę i kliknij ją dwukrotnie. Spowoduje to przejście toohello **Szybki Start** strony. Wybierz hello **Konfiguruj** strony.
2. Kliknij przycisk **Dodaj/edytuj konto magazynu**.
3. W hello **Dodaj/Edytuj konto magazynu** okno dialogowe, kliknij przycisk **Dodaj nowe**.
4. W hello **dostawcy** hello wybierz opcję odpowiednią chmurę usługodawcy. dostawcy Hello obsługiwane są Azure, Amazon S3, Amazon S3 z RRS, HP i OpenStack. Określ poświadczenia hello i lokalizacji hello skojarzonej z konta magazynu hello dostawcom usług w chmurze. Witaj pola wyświetlone dla poświadczeń będą różne w zależności od dostawcy usług w chmurze hello określona. 
   
   * Jeśli jako dostawcę usługi w chmurze wybrano platformę Azure, podaj hello **nazwa** i hello podstawowego **klucz dostępu** dla konta magazynu Microsoft Azure. Konta platformy Azure hello lokalizacja zostanie wypełniona automatycznie.
     
        ![Dodawanie konta usługi Azure Storage](./media/storsimple-configure-new-storage-account-u1/AddAzureStorageaccount-include.png)
   * W przypadku wybrania dostawcy Amazon S3 lub Amazon S3 z RRS wpisz przyjazną nazwę w polu **Nazwa konta magazynu** oraz wypełnij pola **Klucz dostępu** i **Klucz tajny**. Dla dostawców Amazon S3 i Amazon S3 z RRS obsługiwane są hello następujących lokalizacji:
     
     * USA — standardowa
     * Zachodnie stany USA (Oregon)
     * Zachodnie stany USA (Kalifornia Północna)
     * UE (Irlandia)
     * Azja i Pacyfik (Singapur)
     * Azja i Pacyfik (Sydney)
     * Azja i Pacyfik (Tokio)
     * Ameryka Południowa (Sao Paulo)
       
       ![Dodawanie konta magazynu Amazon](./media/storsimple-configure-new-storage-account-u1/AddAmazonStorageaccount-include.png)
   * W przypadku wybrania HP jako dostawcy usługi w chmurze wpisz przyjazną nazwę w polu **Nazwa konta magazynu** oraz wypełnij pola **Identyfikator dzierżawcy**, **Nazwa użytkownika** i **Hasło**. Dla dostawcy HP obsługiwane są hello następujących lokalizacji:
     
     * Wschodnie stany USA
     * Zachodnie stany USA
       
       ![Dodawanie konta magazynu HP](./media/storsimple-configure-new-storage-account-u1/AddHPStorageaccount-include.png)
   * Jeśli jako dostawcę usługi w chmurze wybrano **Openstack**, wypełnij pola **Nazwa hosta**, **Klucz dostępu** i **Klucz tajny**.
     
     > [!NOTE]
     > Dla wszystkich hello dostawcom usług w chmurze, z wyjątkiem platformy Azure dozwolone są przyjazne nazwy. Można użyć różnych przyjaznych nazw i utworzyć więcej niż jedno konto magazynu z hello sam zestaw poświadczeń.
     > 
     > 
     
        ![Dodawanie konta magazynu Openstack](./media/storsimple-configure-new-storage-account-u1/AddOpenstackStorageaccount-include.png)
5. Wybierz **Włącz tryb SSL** toocreate bezpiecznego kanału komunikacji sieciowej między urządzeniami i hello chmury. Wyczyść hello **Włącz tryb SSL** pola wyboru tylko wtedy, gdy pracujesz w chmurze prywatnej.
   
   > [!NOTE]
   > Jeśli używanym dostawcą jest HP, protokół SSL będzie zawsze włączony.
   > 
   > 
6. Kliknij ikonę znacznika wyboru hello ![ikona znacznika wyboru](./media/storsimple-configure-new-storage-account/HCS_CheckIcon-include.png). Po pomyślnym utworzeniu konta magazynu hello, otrzymasz powiadomienie.
7. Witaj nowo utworzone konto magazynu będzie wyświetlana na powitania **Konfiguruj** w obszarze **kont magazynu**. Kliknij przycisk **zapisać** toosave hello nowe konto magazynu. Po wyświetleniu monitu o potwierdzenie kliknij przycisk **OK**.

