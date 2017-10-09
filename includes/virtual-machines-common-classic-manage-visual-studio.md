Maszyny wirtualne na platformie Azure można utworzyć za pomocą Eksploratora serwera w programie Visual Studio.

## <a name="create-an-azure-virtual-machine-in-server-explorer"></a>Utwórz maszynę wirtualną platformy Azure w Eksploratorze serwera
Maszyny wirtualne można tworzyć w hello [portalu zarządzania Azure](http://go.microsoft.com/fwlink/?LinkID=253103), można również tworzyć maszyny wirtualne na platformie Azure, za pomocą poleceń w Eksploratorze serwera. Maszyny wirtualne mogą być używane, na przykład tooprovide front end za wspólnej równoważeniem obciążenia publiczny punkt końcowy.

### <a name="toocreate-a-new-virtual-machine"></a>toocreate nowej maszyny wirtualnej
1. W Eksploratorze serwera, otwórz hello **Azure** węzeł i kliknij przycisk **maszyn wirtualnych**.
2. W menu kontekstowym hello, kliknij przycisk **Utwórz maszynę wirtualną**.
   
    Witaj **tworzenia nowej maszyny wirtualnej** zostanie wyświetlony Kreator.
   
    ![Witaj polecenia Utwórz maszynę wirtualną](./media/virtual-machines-common-classic-create-manage-visual-studio/IC718342.png)
3. Na powitania **Wybierz subskrypcję** wybierz toouse subskrypcji, podczas tworzenia maszyny wirtualnej hello a następnie kliknij przycisk **dalej**.
   
    Jeśli nie jest obecnie zalogowany tooAzure, kliknij przycisk **logowania** toosign w. Następnie wybierz pole listy rozwijanej hello subskrypcji platformy Azure, jeśli jeszcze nie jest wybrana.
4. Na powitania **Wybieranie obrazu maszyny wirtualnej** wybierz typ obrazu hello **typ obrazu** listy rozwijanej pola listy, a następnie wybierz obrazy maszyny wirtualnej w hello **nazwa obrazu** pole listy. Gdy wszystko będzie gotowe, kliknij przycisk **dalej**.
   
    ![Wybierz stronę obrazu maszyny wirtualnej](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744137.png)
   
    Można wybrać hello następujące typy obrazów.
   
   * **Obrazy publicznego** listy obrazów maszyny wirtualnej, systemy operacyjne i oprogramowanie serwera, takie jak Windows Server i SQL Server.
   * **Obrazów MSDN** listy obrazów maszyny wirtualnej abonentów dostępne tooMSDN oprogramowania, takie jak Visual Studio i Microsoft Dynamics.
   * **Obrazy prywatnego** listy specjalizowany i uogólniony obrazy maszyny wirtualnej, które zostały utworzone.
     
     toolearn o specjalizowany i uogólniony maszyn wirtualnych, zobacz [obrazu maszyny Wirtualnej](https://azure.microsoft.com/blog/2014/04/14/vm-image-blog-post/). Zobacz [jak tooCapture tooUse maszyny wirtualnej systemu Windows, jako szablon](https://azure.microsoft.com/documentation/articles/virtual-machines-capture-image-windows-server/) uzyskać informacji na temat sposobu tooturn maszynę wirtualną do szablonu, których można używać tooquickly utworzyć nowy wstępnie skonfigurowanych maszyn wirtualnych.
     
     Możesz kliknąć maszyny wirtualnej obrazu nazwa toosee informacji o obraz powitania hello prawej strony hello strony.
     
     > [!NOTE]
     > Nie można dodać toohello obrazów maszyny wirtualnej **publicznego obrazy** lub **obrazów MSDN** listy, ponieważ są one tylko do odczytu. Wszystkie maszyny wirtualne tworzone są dodawane toohello **obrazów prywatnego** listy.
     > 
     > 
     
     Jeśli jesteś subskrybentem MSDN z subskrypcją programu Visual Studio na poziomie, można utworzyć wbudowanych Azure maszyny wirtualnej, która zawiera programu Visual Studio, jak również inne obrazy. Aby uzyskać więcej informacji, zobacz [Utwórz maszynę wirtualną w programie Visual Studio za pomocą obrazów programu Visual Studio 2013 galerii obrazu dla subskrybentów MSDN](http://visualstudio2013msdngalleryimage.azurewebsites.net) i [subskrypcji MSDN](https://www.visualstudio.com/products/msdn-subscriptions-vs). |
5. Na powitania **ustawienia podstawowej maszyny wirtualnej** strony, wprowadź nazwę komputera, a następnie dodać specyfikacje hello hello maszyny wirtualnej, w tym rozmiar hello i nazwę użytkownika i hasło. Gdy wszystko będzie gotowe, kliknij przycisk **dalej**.
   
    Użyjesz hello nowej nazwy i zapomni hasła toolog maszynie hello przy użyciu pulpitu zdalnego, tak aby zawierała toowrite dobrym rozwiązaniem, je w dół w przypadku należy. Po utworzeniu maszyny wirtualnej platformy Azure w programie Visual Studio, można zmienić jej rozmiaru i inne ustawienia w hello [portalu zarządzania Azure](http://go.microsoft.com/fwlink/?LinkID=253103).
   
   > [!NOTE]
   > Jeśli wybierzesz dla maszyny wirtualnej hello o większych rozmiarach, mogą stosować dodatkowych opłat. Zobacz [maszyny wirtualne — cennik](https://azure.microsoft.com/pricing/details/virtual-machines/) Aby uzyskać więcej informacji.
   > 
   > 
6. Maszyny wirtualne utworzone w programie Visual Studio wymaga usługi w chmurze. Na powitania **ustawienia usługi w chmurze** wybierz usługę chmury dla maszyny wirtualnej hello lub kliknij przycisk **< Utwórz nowy... >** w listy rozwijanej hello, jeśli nie masz jeszcze chmurze usługa lub mają toouse nowy jeden. Konto magazynu jest również wymagany, dlatego wybierz konto magazynu (lub Utwórz nowe konto magazynu) w hello **konta magazynu** pole listy rozwijanej. Zobacz [tooMicrosoft wprowadzenie usługi Azure Storage](../articles/storage/common/storage-introduction.md) Aby uzyskać więcej informacji.
7. Jeśli chcesz toospecify sieć wirtualną (która jest opcjonalny), wybierz je w hello sieć wirtualna i podsieć listy rozwijanej pola listy.
   
    Maszyny wirtualne, które są członkami zestawu dostępności są wdrożone toodifferent domen błędów. Zobacz [sieci wirtualnej Azure](https://azure.microsoft.com/services/virtual-network/) Aby uzyskać więcej informacji.
8. Maszyna wirtualna toobelong tooan dostępność zestawu (również opcjonalnie), wybierz opcję hello **określ zestaw dostępności** zaznacz pole wyboru, a następnie wybierz pozycję zestawem dostępności w polu listy rozwijanej hello. Gdy wszystko będzie gotowe, wybierz hello **dalej** przycisku.
   
    Dodawanie użytkownika tooan maszyny wirtualnej zestawu dostępności pomaga aplikacji pozostają dostępne podczas awarie sieci, awarie sprzętowe dysku lokalnym oraz wszelkich planowanych przestojów. Należy toouse hello [portalu zarządzania Azure](http://go.microsoft.com/fwlink/?LinkID=253103) dostępności, podsieci i sieci wirtualne toocreate ustawia. Zobacz [hello Zarządzaj dostępność maszyn wirtualnych](https://azure.microsoft.com/documentation/articles/manage-availability-virtual-machines/) Aby uzyskać więcej informacji.
9. Na powitania **punkty końcowe** Określ publiczne punkty końcowe hello, które mają dostępne toousers maszyny wirtualnej. Na przykład można tooenable HTTP (Port 80) dodatkowo toohello pulpitu zdalnego i programu PowerShell punktów końcowych, które są domyślnie włączone. tooadd jako punkt końcowy, wybierz kolejno hello **nazwa portu** pole listy rozwijanej, a następnie wybierz pozycję hello **Dodaj** przycisku. tooremove jako punkt końcowy, wybierz hello red **X** następnej nazwy toohello hello listy punktów końcowych.
   
    ![Strona punkty końcowe Hello hello kreatora maszyn wirtualnych.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC718351.png)
   
    Hello punktów końcowych, które są dostępne są zależne od usługi w chmurze hello wybrany dla maszyny wirtualnej. Zobacz [punktami końcowymi usług Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/) Aby uzyskać więcej informacji.
   
   > [!NOTE]
   > Włączenie publiczne punkty końcowe powoduje usług w sieci maszyny wirtualnej toohello dostępne internet. Należy się tooinstall i poprawnie skonfigurować punkty końcowe hello i usług na maszynie wirtualnej, takich jak kontrola dostępu ustawienie listy (kontroli dostępu ACL) dla punktów końcowych hello. Zobacz [jak tooSet się punkty końcowe tooa maszyny wirtualnej](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/) Aby uzyskać więcej informacji.
   > 
   > 
10. Po zakończeniu konfigurowania ustawień maszyny wirtualnej hello wybierz hello **Utwórz** maszyny wirtualnej hello toocreate przycisku.
    
     Jako platforma Azure tworzy hello maszyny wirtualnej, hello **dziennika aktywności platformy Azure** pokazuje hello postęp operacji tworzenia hello maszyny wirtualnej.
    
     ![Dziennik aktywności maszyny wirtualnej — w toku.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744138.png)
    
     tooview informacji tylko maszynę wirtualną, wybrać hello **maszyn wirtualnych** kartę w hello **dziennika aktywności platformy Azure**.
    
     ![Dziennik aktywności maszyny wirtualnej — ukończone.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744139.png)
    
     Jeśli operacja hello zakończy się pomyślnie, hello nowej maszyny wirtualnej jest wyświetlany w obszarze hello **maszyn wirtualnych** węzła w Eksploratorze serwera. Możesz zalogować się do go, klikając hello **łączyć się przy użyciu pulpitu zdalnego** skrótów.
    
     ![Maszyny wirtualnej znajdujących się w Eksploratorze serwera.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744140.png)

## <a name="manage-your-virtual-machines"></a>Zarządzanie maszyny wirtualne
Na stronie konfiguracji maszyny wirtualnej hello oprócz tooshutting w dół, połączenie odświeżania i dodawanie punktów kontrolnych toohello wybrane maszyny wirtualnej, można również wyświetlić lub zmienić ustawienia hello maszyny wirtualnej. Możesz:

* Zmień rozmiar maszyny wirtualnej hello.
* Toouse z maszyną wirtualną hello zestawu dostępności SELECT hello.
* Dodać, usunąć lub zmienić ustawienia dla publicznych punktów końcowych.
* Dodać, usunąć lub skonfigurować rozszerzenia maszyny wirtualnej.
* Wyświetl informacje o dyskach hello skojarzoną z maszyną wirtualną hello.

### <a name="view-or-change-virtual-machine-settings"></a>Wyświetl lub zmień ustawienia maszyny wirtualnej
1. W Eksploratorze serwera, wybierz maszynę wirtualną hello **maszyny wirtualne Azure** węzła.
2. Menu skrótów hello, wybierz **Konfiguruj** tooview hello na stronie konfiguracji maszyny wirtualnej.
   
    ![Witaj na stronie konfiguracji maszyny wirtualnej platformy Azure](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744141.png)
3. Wyświetlanie informacji o maszynie wirtualnej hello lub je zmienić.

### <a name="save-or-restore-hello-status-of-your-virtual-machine"></a>Zapisz lub Przywróć hello stan maszyny wirtualnej
Skonfiguruj maszynę wirtualną i instalować oprogramowanie na nim, jest tooregularly dobrze, aby zapisać postęp przez utworzenie punktów kontrolnych maszyn wirtualnych. Punkt kontrolny to migawka lub obraz powitania w bieżącym stanie maszyny wirtualnej. Jeśli wystąpią problemy z maszyną wirtualną hello lub ma maszyny wirtualnej hello tooreconfigure, można oszczędzić czas, przywracając jego poprzedniego stanu punktu kontrolnego tooa zamiast Rozpoczynanie od zera.

### <a name="toocreate-a-virtual-machine-checkpoint"></a>toocreate punktu kontrolnego maszyny wirtualnej
1. W Eksploratorze serwera, wybierz maszynę wirtualną hello **maszyny wirtualne Azure** węzła.
2. Menu skrótów hello, wybierz **Konfiguruj** tooview hello na stronie konfiguracji maszyny wirtualnej.
3. Na stronie konfiguracji hello wybierz hello **Przechwyć obraz** przycisku.
   
    ![Przycisku przechwytywania strony konfiguracji platformy Azure](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744142.png)
   
    Witaj **Przechwytywanie maszyny wirtualnej** zostanie wyświetlone okno dialogowe.
   
    ![Okno dialogowe maszyny wirtualnej Azure przechwytywania](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744143.png)
4. Podaj etykietę obrazu i opis. Podano etykiety domyślnej i opis, ale można je zastąpić, jeśli chcesz własnymi.
5. Jeśli program Sysprep zostało już uruchomione na tej maszynie wirtualnej, wybierz hello **program Sysprep został uruchomiony na maszynie wirtualnej hello** pole.
   
    Sysprep to narzędzie, które między innymi usuwa dane specyficzne dla systemów z maszyny wirtualnej hello wersji systemu Windows, dzięki czemu szablonu używanego przez innych użytkowników. Zobacz [jak tooCapture tooUse maszyny wirtualnej systemu Windows, jako szablon](https://azure.microsoft.com/documentation/articles/virtual-machines-capture-image-windows-server/) Aby uzyskać więcej informacji. Utwórz kopię zapasową hello maszyny Wirtualnej przed uruchomieniem programu Sysprep.
6. Po zakończeniu konfigurowania ustawień przechwytywania hello wybierz hello **przechwytywania** punktu kontrolnego hello toocreate przycisku.
   
    Jako platforma Azure tworzy punkt kontrolny hello, hello **dziennika aktywności platformy Azure** pokazuje hello postęp operacji hello.
   
    ![Przechwytywanie punktu kontrolnego maszyny wirtualnej](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744144.png)
   
    Po zakończeniu operacji punktu kontrolnego hello, zobaczysz go w hello **dziennika aktywności platformy Azure**.
   
    ![Zakończono operację punktu kontrolnego](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744145.png)

## <a name="toomanage-virtual-machine-checkpoints"></a>toomanage punktami kontrolnymi maszyny wirtualnej
### <a name="toorestore-a-virtual-machine-tooa-previously-saved-state"></a>toorestore tooa maszyny wirtualnej uprzednio zapisanego stanu
* Wykonaj kroki hello opisane w temacie [krok po kroku: wykonaj chmury przywraca Microsoft maszyn wirtualnych Azure przy użyciu programu PowerShell — część 2](http://blogs.technet.com/b/keithmayer/archive/2014/02/04/step-by-step-perform-cloud-restores-of-windows-azure-virtual-machines-using-powershell-part-2.aspx).

### <a name="toodelete-a-checkpoint"></a>toodelete punkt kontrolny
1. Przejdź toohello [portalu zarządzania Azure](http://go.microsoft.com/fwlink/?LinkID=253103).
2. Na stronie konfiguracji maszyny wirtualnej hello wybierz hello **obrazów** kartę u góry hello hello strony.
3. Wybierz hello punktu kontrolnego, mają toodelete, a następnie wybierz hello **usunąć** przycisk u dołu hello hello strony.

## <a name="shut-down-your-virtual-machine"></a>Zamknij maszynę wirtualną
1. W Eksploratorze serwera, wybierz maszynę wirtualną hello ma tooshut w dół w hello **maszyny wirtualne Azure** węzła.
2. Menu skrótów hello, albo wybierz hello **zamknięcia** polecenie lub wybierz **Konfiguruj** tooview hello na stronie konfiguracji maszyny wirtualnej, a następnie wybierz hello **zamknięcia**przycisku.

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat tworzenia maszyn wirtualnych, zobacz [tworzenia maszyny wirtualnej systemem Linux](../articles/virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) i [Utwórz maszynę wirtualną z systemem Windows w portalu Azure w wersji zapoznawczej hello](../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

