---
title: aaaBack serwery VMware serwer kopii zapasowej Azure | Dokumentacja firmy Microsoft
description: "Użyj tooback Azure Utwórz kopię zapasową serwera VMware vCenter/ESXi serwerów tooAzure lub dysku. W tym artykule przedstawiono krok = instrukcje krok po kroku dla tworzenia kopii zapasowych (lub ochrony) obciążeń VMware."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
ms.assetid: 6b131caf-de85-4eba-b8e6-d8a04545cd9d
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: markgal;
ms.openlocfilehash: 3edb6880a526ed0b18605fee0fac27196a608e7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-vmware-server-tooazure"></a>Wykonaj kopię zapasową tooAzure serwer VMware

W tym artykule opisano, jak toohelp serwer kopii zapasowej Azure tooconfigure chronić obciążeń serwera VMware. W tym artykule przyjęto założenie, że masz już zainstalowany serwer kopii zapasowej Azure. Jeśli nie masz zainstalowany serwer kopii zapasowej Azure, zobacz [przygotowanie tooback dużych obciążeń, za pomocą serwera usługi Kopia zapasowa Azure](backup-azure-microsoft-azure-backup.md).

Serwer kopii zapasowej systemu Azure można utworzyć kopię zapasową lub lepiej chronić VMware vCenter Server w wersji 6.5, 6.0 i 5.5.


## <a name="create-a-secure-connection-toohello-vcenter-server"></a>Tworzenie serwera vCenter toohello bezpiecznego połączenia

Domyślnie serwer kopii zapasowej Azure komunikuje się z każdym vCenter Server za pośrednictwem kanału HTTPS. tooturn na powitania bezpiecznej komunikacji, zalecamy zainstalowanie hello VMware urzędu certyfikacji certyfikatu na serwerze kopii zapasowej Azure. Jeśli nie wymagają bezpiecznej komunikacji i wolisz toodisable hello HTTPS wymagania, zobacz [wyłączanie bezpiecznej komunikacji protokołu](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol). toocreate bezpiecznego połączenia między serwerem kopia zapasowa Azure i hello vCenter Server, zaimportuj hello zaufanego certyfikatu na serwerze kopii zapasowej Azure.

Zazwyczaj użytkownik korzysta z przeglądarki na powitania serwera usługi Kopia zapasowa Azure maszyny tooconnect toohello vCenter Server za pośrednictwem vSphere powitania klienta sieci Web. Witaj po raz pierwszy używasz hello serwer kopii zapasowej Azure przeglądarki tooconnect toohello vCenter Server, hello połączenia nie jest zabezpieczone. powitania po obraz pokazuje hello niezabezpieczone połączenie.

![Przykład serwera tooVMware niezabezpieczone połączenie](./media/backup-azure-backup-server-vmware/unsecure-url.png)

toofix ten problem i utworzenia bezpiecznego połączenia, Pobierz hello zaufanych certyfikatów głównego urzędu certyfikacji.

1. W przeglądarce hello na serwerze kopii zapasowej Azure wprowadź vSphere toohello adres URL powitania klienta sieci Web. zostanie wyświetlona strona logowania klienta sieci Web vSphere Hello.

    ![vSphere klienta sieci Web](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    U dołu hello hello informacje dla administratorów i deweloperów, zlokalizuj hello **pobierania zaufane certyfikaty głównego urzędu certyfikacji** łącza.

    ![Łącze toodownload hello zaufanego głównego urzędu certyfikacji](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  Jeśli widzisz stronę logowania klienta sieci Web vSphere hello, sprawdź ustawienia serwera proxy przeglądarki.

2. Kliknij przycisk **pobierania zaufane certyfikaty głównego urzędu certyfikacji**.

    Serwer vCenter Hello pliki do pobrania na komputerze lokalnym tooyour pliku. Witaj nazwę pliku o nazwie **Pobierz**. W zależności od przeglądarki, zostanie wyświetlony komunikat z pytaniem, czy tooopen lub zapisać plik hello.

    ![Pobierz wiadomość, gdy są pobierane certyfikaty](./media/backup-azure-backup-server-vmware/download-certs.png)

3. Zapisz hello pliku tooa lokalizacji na serwerze kopii zapasowej Azure. Podczas zapisywania pliku hello dodać rozszerzenie nazwy pliku zip hello.

    Plik Hello jest plik zip zawierający hello informacji o certyfikatach hello. Z rozszerzeniem .zip hello można użyć narzędzia wyodrębniania hello.

4. Kliknij prawym przyciskiem myszy **download.zip**, a następnie wybierz **Wyodrębnij wszystkie** tooextract hello zawartość.

    plik zip Hello wyodrębnia jego zawartość folderów tooa o nazwie **certyfikaty**. W folderze Certyfikaty hello są wyświetlane dwa typy plików. plik certyfikatu głównego Hello ma rozszerzenie, który rozpoczyna się od numeru sekwencji.0 i.1.
    
    Witaj listy CRL plik ma rozszerzenie, rozpoczynający się od sekwencji, takich jak .r0 lub .r1. Plik listy CRL Hello jest skojarzony z certyfikatem.

    ![Pobierz plik wyodrębnione lokalnie ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. W hello **certyfikaty** folderu, kliknij prawym przyciskiem myszy plik certyfikatu głównego hello, a następnie kliknij przycisk **zmienić**.

    ![Zmień nazwę certyfikatu głównego ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    Zmienianie certyfikatu głównego hello too.crt rozszerzenia. Pytanie, jeśli masz pewności, mają rozszerzenie hello toochange, kliknij przycisk **tak** lub **OK**. W przeciwnym razie możesz zmienić funkcji hello pliku. Ikona Hello hello pliku zmiany tooan ikonę, która reprezentuje certyfikatu głównego.

6. Kliknij prawym przyciskiem myszy certyfikat główny hello i wybierz z menu podręcznego hello **Zainstaluj certyfikat**.

    Witaj **Kreatora importu certyfikatów** zostanie wyświetlone okno dialogowe.

7. W hello **Kreatora importu certyfikatów** okno dialogowe, wybierz opcję **komputera lokalnego** jako miejsce docelowe hello hello certyfikatu, a następnie kliknij przycisk **dalej** toocontinue.

    ![Opcje docelowy magazyn certyfikatów ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    Jeśli pojawi się monit Jeśli chcesz tooallow zmiany toohello komputer, kliknij przycisk **tak** lub **OK**, tooall hello zmiany.

8. Na powitania **magazyn certyfikatów** wybierz pozycję **Umieść wszystkie certyfikaty w powitania po magazynu**, a następnie kliknij przycisk **Przeglądaj** magazynu certyfikatów hello toochoose.

    ![Umieść w miejscu określonego magazynu certyfikatów](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    Witaj **wybierz magazyn certyfikatów** zostanie wyświetlone okno dialogowe.

    ![Hierarchia folderów magazyn certyfikatów](./media/backup-azure-backup-server-vmware/cert-store.png)

9. Wybierz **zaufane główne urzędy certyfikacji** jako folder docelowy hello hello certyfikatów, a następnie kliknij przycisk **OK**.

    ![Folder docelowy certyfikatu](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    Witaj **zaufane główne urzędy certyfikacji** folder został potwierdzony jako hello magazynu certyfikatów. Kliknij przycisk **Dalej**.

    ![Folder magazynu certyfikatów](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. Na powitania **hello Kończenie pracy Kreatora importu certyfikatów** zweryfikować certyfikat hello znajduje się w folderze żądaną hello, a następnie kliknij przycisk **Zakończ**.

    ![Sprawdź, czy certyfikat znajduje się w folderze prawidłowego hello](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    Zostanie wyświetlone okno dialogowe, importu certyfikatów pomyślnie hello został potwierdzony.

11. Zaloguj się toohello vCenter Server tooconfirm, że połączenie jest bezpieczne.

  Jeśli hello certyfikat import zakończy się niepowodzeniem i nie można ustanowić bezpiecznego połączenia, w dokumentacji hello VMware vSphere na [uzyskiwanie certyfikatów serwera](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).

  Jeśli masz bezpiecznych granic w ramach danej organizacji, a nie mają tooturn na powitania protokołu HTTPS, należy użyć hello następujące procedury toodisable hello bezpieczną komunikację.

### <a name="disable-secure-communication-protocol"></a>Wyłącz protokół bezpiecznej komunikacji

Jeśli Twoja organizacja nie wymaga hello protokołu HTTPS, należy użyć hello następujące kroki toodisable HTTPS. toodisable hello domyślne zachowanie, należy utworzyć klucz rejestru, który ignoruje hello domyślne zachowanie.

1. Skopiuj i Wklej powitania po tekstu do pliku txt.

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. Zapisz hello pliku tooyour serwer kopii zapasowej Azure komputera. Nazwa pliku hello Użyj DisableSecureAuthentication.reg.

3. Kliknij dwukrotnie wpis rejestru hello hello pliku tooactivate.


## <a name="create-a-role-and-user-account-on-hello-vcenter-server"></a>Utwórz konto rolę i użytkownika na powitania vCenter Server

Witaj programie vcenter Server Rola to wstępnie zdefiniowane uprawnienia. Administrator serwera vCenter tworzy hello ról. uprawnienia tooassign administratora hello pary kont użytkowników z roli. tooestablish hello niezbędnych poświadczeń tooback hello komputera serwera vCenter, utworzyć rolę z określone uprawnienia, a następnie skojarzyć hello konta użytkownika z rolą hello.

Serwer kopii zapasowej systemu Azure używa tooauthenticate nazwę użytkownika i hasło z hello vCenter Server. Serwer kopii zapasowej systemu Azure używa tych poświadczeń uwierzytelniania dla wszystkich operacji tworzenia kopii zapasowej.

tooadd vCenter roli serwera i jego uprawnień administratora kopii zapasowych:

1. Zaloguj się w toohello vCenter Server, a następnie w programie hello vCenter Server **Nawigator** panelu, kliknij przycisk **administracji**.

    ![Opcja administracji w panelu Nawigator serwera vCenter](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. W **administracji** wybierz **ról**, a następnie w hello **ról** kliknij panel hello dodać ikona roli (hello + symbol).

    ![Dodaj rolę](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    Witaj **Utwórz rolę** zostanie wyświetlone okno dialogowe.

    ![Tworzenie roli](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. W hello **Utwórz rolę** okno dialogowe, w hello **nazwy roli** wprowadź *BackupAdminRole*. Nazwa roli Hello może być dowolne, ale powinien być rozpoznawalną w celu hello roli.

4. Wybierz uprawnienia hello hello odpowiedniej wersji programu vCenter, a następnie kliknij przycisk **OK**. w poniższej tabeli Hello identyfikuje hello wymagane uprawnienia dla vCenter 6.0 i vCenter 5.5.

  Po wybraniu hello uprawnień, kliknij przycisk hello ikona dalej toohello nadrzędny etykiety tooexpand hello nadrzędne i widoku hello podrzędnych uprawnień. tooselect hello VirtualMachine uprawnień, należy toogo kilka poziomów do hello nadrzędnego hierarchii podrzędnej. Nie trzeba tooselect wszystkie uprawnienia podrzędnego w obrębie uprawnienie nadrzędne.

  ![Uprawnienie hierarchii nadrzędny-podrzędny](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  Po kliknięciu **OK**, hello nową rolę pojawia się na liście hello na panelu ról hello.

|Uprawnienia dla serwera vCenter 6.0| Uprawnienia dla serwera vCenter 5,5|
|--------------------------|---------------------------|
|Datastore.AllocateSpace   | Datastore.AllocateSpace|
|Global.ManageCustomFields | Global.ManageCustomerFields|
|Global.SetCustomFields    |   |
|Host.Local.CreateVM       | Network.Assign |
|Network.Assign            |  |
|Resource.AssignVMToPool   |  |
|VirtualMachine.Config.AddNewDisk  | VirtualMachine.Config.AddNewDisk   |
|VirtualMachine.Config.AdvanceConfig| VirtualMachine.Config.AdvancedConfig|
|VirtualMachine.Config.ChangeTracking| VirtualMachine.Config.ChangeTracking |
|VirtualMachine.Config.HostUSBDevice||
|VirtualMachine.Config.QueryUnownedFiles|    |
|VirtualMachine.Config.SwapPlacement| VirtualMachine.Config.SwapPlacement |
|VirtualMachine.Interact.PowerOff| VirtualMachine.Interact.PowerOff |
|VirtualMachine.Inventory.Create| VirtualMachine.Inventory.Create |
|VirtualMachine.Provisioning.DiskRandomAccess| |
|VirtualMachine.Provisioning.DiskRandomRead|VirtualMachine.Provisioning.DiskRandomRead |
|VirtualMachine.State.CreateSnapshot| VirtualMachine.State.CreateSnapshot|
|VirtualMachine.State.RemoveSnapshot|VirtualMachine.State.RemoveSnapshot |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a>Tworzenie konta użytkownika serwera vCenter i uprawnień

Po skonfigurowaniu roli hello z uprawnieniami, Utwórz konto użytkownika. konto użytkownika Hello ma nazwę i hasło, które udostępnia hello poświadczenia, które są używane do uwierzytelniania.

1. konto użytkownika w programie hello vCenter Server toocreate **Nawigator** panelu, kliknij przycisk **użytkowników i grup**.

    ![Opcja użytkowników i grup](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    Witaj **vCenter użytkowników i grup** pojawi się panel.

    ![panel vCenter użytkowników i grup](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. W hello **vCenter użytkowników i grup** panelu, wybierz opcję hello **użytkowników** , a następnie kliknij pozycję hello dodać ikonę użytkowników (hello + symbol).

    Witaj **nowego użytkownika** zostanie wyświetlone okno dialogowe.

3. W hello **nowego użytkownika** okna dialogowego, Dodaj informacje o użytkowniku hello a następnie kliknij przycisk **OK**. W tej procedurze hello username jest BackupAdmin.

    ![Okno dialogowe Nowy użytkownik](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    Hello nowe konto użytkownika zostanie wyświetlony na liście hello.

4. konto użytkownika hello tooassociate z roli hello w hello **Nawigator** panelu, kliknij przycisk **uprawnień globalnych**. W hello **uprawnień globalnych** panelu, wybierz opcję hello **Zarządzaj** , a następnie kliknij pozycję hello dodać ikonę (hello + symbol).

    ![Panel uprawnień globalnych](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    Witaj **globalnych uprawnień Root - Dodaj uprawnienie** zostanie wyświetlone okno dialogowe.

5. W hello **globalnych uprawnień Root - Dodaj uprawnienie** okno dialogowe, kliknij przycisk **Dodaj** toochoose hello użytkownika lub grupy.

    ![Wybierz użytkownika lub grupy](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    Witaj **użytkowników/grupy wybierz** zostanie wyświetlone okno dialogowe.

6. W hello **użytkowników/grupy wybierz** oknie dialogowym wybierz **BackupAdmin** , a następnie kliknij przycisk **Dodaj**.

    W **użytkowników**, hello *domena azwa_użytkownika* format jest używany dla hello konta użytkownika. Jeśli chcesz toouse inną domenę, wybierz go z hello **domeny** listy.

    ![Dodaj użytkownika BackupAdmin](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    Kliknij przycisk **OK** tooadd hello wybrane toohello użytkowników **dodać uprawnienia** okno dialogowe.

7. Teraz, gdy wyłaniają hello użytkownika, należy przypisać rolę toohello użytkownika hello. W **przypisana rola**, wybierz z listy rozwijanej hello **BackupAdminRole**, a następnie kliknij przycisk **OK**.

    ![Przypisz toorole użytkownika](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  Na powitania **Zarządzaj** kartę w hello **uprawnień globalnych** panelu, hello nowego konta użytkownika i roli hello skojarzone są wyświetlane na liście hello.


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a>Ustanowić poświadczenia serwera vCenter na serwerze kopia zapasowa Azure

Przed dodaniem hello VMware server tooAzure kopii zapasowej serwera należy zainstalować [aktualizacji 1 dla serwera usługi Kopia zapasowa Azure](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).

1. tooopen serwer kopii zapasowej Azure, kliknij dwukrotnie ikonę hello na powitania serwera usługi Kopia zapasowa Azure pulpitu.

    ![Ikona serwera kopia zapasowa Azure](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    Jeśli nie możesz znaleźć hello ikony na pulpicie hello, należy otworzyć serwer kopii zapasowej Azure z hello listę zainstalowanych aplikacji. Nazwa aplikacji Hello serwer kopii zapasowej Azure jest nazywany kopia zapasowa Microsoft Azure.

2. W hello Azure Utwórz kopię zapasową serwera konsoli, kliknij **zarządzania**, kliknij przycisk **serwerów produkcyjnych**, a następnie na wstążce narzędzi hello, kliknij przycisk **Zarządzanie VMware**.

    ![Konsoli serwera kopii zapasowej platformy Azure](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    Witaj **poświadczenia zarządzania** zostanie wyświetlone okno dialogowe.

    ![Okno dialogowe poświadczenia zarządzania serwera kopii zapasowej systemu Azure](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. W hello **poświadczenia zarządzania** okno dialogowe, kliknij przycisk **Dodaj** tooopen hello **Dodaj poświadczenie** okno dialogowe.

4. W hello **Dodaj poświadczenie** okna dialogowego wprowadź nazwę i opis dla hello nowe poświadczenia. Następnie określ hello nazwy użytkownika i hasła. Nazwa Hello *poświadczeń Contoso Vcenter* służy tooidentify hello poświadczenia w następnej procedurze hello. Użyj hello takie same nazwy użytkownika i hasło, które jest używane dla hello vCenter Server. Jeśli hello programu vCenter Server i serwer kopii zapasowej Azure nie znajdują się w hello w tej samej domenie, **nazwy użytkownika**, określ hello domeny.

    ![Okno dialogowe poświadczeń dodawania serwera kopii zapasowej platformy Azure](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    Kliknij przycisk **Dodaj** tooadd hello nowych poświadczeń tooAzure Utwórz kopię zapasową serwera. nowe poświadczenie Hello jest widoczna na liście hello w hello **poświadczenia zarządzania** okno dialogowe.
    
    ![Okno dialogowe poświadczenia zarządzania serwera kopii zapasowej systemu Azure](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. Witaj tooclose **poświadczenia zarządzania** okna dialogowego kliknij hello **X** w prawym górnym rogu hello.


## <a name="add-hello-vcenter-server-tooazure-backup-server"></a>Dodaj hello vCenter Server tooAzure kopii zapasowej serwera

Kreator dodawania serwera produkcyjnego jest używane tooadd hello vCenter Server tooAzure Utwórz kopię zapasową serwera.

tooopen Kreator dodawania serwera produkcji, pełną hello następujące procedury:

1. W konsoli serwera usługi Kopia zapasowa Azure powitania kliknij **zarządzania**, kliknij przycisk **serwerów produkcyjnych**, a następnie kliknij przycisk **Dodaj**.

    ![Kreator dodawania serwera Otwórz produkcji](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    Witaj **Kreator dodawania serwera produkcyjnego** zostanie wyświetlone okno dialogowe.

    ![Kreator dodawania serwera produkcyjnego](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. Na powitania **typu wybierz serwer produkcyjny** wybierz **serwerów VMware**, a następnie kliknij przycisk **dalej**.

3. W **adres IP/nazwa serwera**, określ hello pełną nazwę domeny (FQDN) lub adres IP serwera VMware hello. Jeśli wszystkie serwery ESXi hello są zarządzane przez hello sam program vCenter, można użyć nazwy vCenter hello.

    ![Określ adres FQDN lub adres IP serwera VMware](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. W **SSL Port**, wprowadź port hello toocommunicate używane z serwerem VMware hello. Korzysta z portu 443, czyli hello domyślny port, jeśli nie wiadomo, że inny port jest wymagana.

5. W **Określ poświadczenia**, wybierz hello poświadczeń, który został utworzony wcześniej.

    ![Określ poświadczenia](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. Kliknij przycisk **Dodaj** tooadd hello VMware toohello listy serwerów **dodane serwery VMware**, a następnie kliknij przycisk **dalej** toomove toohello następnej strony kreatora hello.

    ![Dodawanie serwera VMWare i poświadczenia](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. W hello **Podsumowanie** kliknij przycisk **Dodaj** tooadd hello określony tooAzure serwera VMware Utwórz kopię zapasową serwera.

    ![Dodaj tooAzure serwera VMware kopii zapasowej serwera](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  Kopia zapasowa serwera VMware Hello jest bez agenta kopii zapasowej i natychmiast jest dodawany nowy serwer hello. Witaj **Zakończ** strony pokazuje hello wyników.

  ![Zakończ strony](./media/backup-azure-backup-server-vmware/summary-screen.png)

  tooadd wiele wystąpień programu vCenter Server tooAzure Utwórz kopię zapasową serwera hello Powtórz poprzednie kroki w tej sekcji.

Po dodaniu hello vCenter Server tooAzure Utwórz kopię zapasową serwera hello następnym krokiem jest toocreate grupy ochrony. grupy ochrony Hello określa hello różne szczegóły dotyczące krótki i długoterminowego przechowywania i gdzie Zdefiniuj i zastosowania zasad tworzenia kopii zapasowej hello jest. zasady tworzenia kopii zapasowej Hello jest harmonogram hello gdy kopie zapasowe są wykonywane, i kopii zapasowej.


## <a name="configure-a-protection-group"></a>Skonfiguruj grupę ochrony

Jeśli nie używasz programu System Center Data Protection Manager lub serwer kopii zapasowej Azure przed, zobacz [Planowanie kopii zapasowych na dyskach](https://technet.microsoft.com/library/hh758026.aspx) tooprepare środowiska sprzętowego. Po sprawdzeniu, czy masz odpowiednie magazynu, należy użyć Kreatora tworzenia nowej grupy ochrony hello tooadd maszyny wirtualne VMware.

1. W konsoli serwera usługi Kopia zapasowa Azure powitania kliknij **ochrony**, a hello wstążce narzędzia, kliknij przycisk **nowy** Kreatora tworzenia nowej grupy ochrony hello tooopen.

    ![Witaj Otwórz Kreatora tworzenia nowej grupy ochrony](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    Witaj **tworzenia nowej grupy ochrony** zostanie wyświetlone okno dialogowe Kreator.

    ![Okno dialogowe Kreator tworzenia nowej grupy ochrony](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    Kliknij przycisk **dalej** tooadvance toohello **wybierz typ grupy ochrony** strony.

2. Na powitania **typ grupy ochrony wybierz** wybierz **serwerów** , a następnie kliknij przycisk **dalej**. Witaj **Wybierz członków grupy** zostanie wyświetlona strona.

3. Na powitania **Wybierz członków grupy** strony, hello dostępnych elementów członkowskich i elementów członkowskich hello wybrane są wyświetlane. Wybierz członków hello mają tooprotect, a następnie kliknij przycisk **dalej**.

    ![Wybierz członków grupy](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    Po wybraniu członka, w przypadku wybrania folderu zawierającego inne foldery lub maszyn wirtualnych, wybrane zostaną także te foldery i maszyn wirtualnych. Włączenie Hello hello folderów i maszyn wirtualnych w folderze nadrzędnym hello jest nazywany ochrony na poziomie folderu. tooremove folder lub maszyny Wirtualnej, hello wyczyść pole wyboru.

    Jeśli maszyny Wirtualnej lub folder zawierający maszyny Wirtualnej, jest już chronione tooAzure, nie możesz wybrać tej maszyny Wirtualnej ponownie. Oznacza to po maszyny Wirtualnej jest tooAzure chronionych, nie można go chronić ponownie, która zapobiega utworzeniu dla jednej maszyny Wirtualnej przez punkty odzyskiwania zduplikowane. Jeśli chcesz toosee, którego wystąpienia serwera usługi Kopia zapasowa Azure chroni już elementu członkowskiego, punkt toohello nazwa elementu członkowskiego toosee hello hello chroni serwer.

4. Na powitania **wybierz metodę ochrony danych** strony, wprowadź nazwę grupy ochrony hello. Wybrano krótkoterminowej ochrony (toodisk) i ochrony w trybie online. Jeśli chcesz toouse ochrony w trybie online (tooAzure), należy użyć krótkoterminowej ochrony toodisk. Kliknij przycisk **dalej** tooproceed toohello krótkoterminowej ochrony zakresu.

    ![Wybierz metodę ochrony danych](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. Na powitania **Określ cele krótkoterminowe** strony, dla **zakres przechowywania**, określ hello liczbę dni, które mają punkty odzyskiwania tooretain, które są *przechowywane toodisk*. Toochange hello godziny i dni przy woluminów punktów odzyskiwania, kliknij przycisk **Modyfikuj**. punkty odzyskiwania krótkoterminowego Hello są pełne kopie zapasowe. Nie są one przyrostowych kopii zapasowych. Po zakończeniu krótkoterminowych celów w zakresie powitania kliknij **dalej**.

    ![Określanie celów krótkoterminowych](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. Na powitania **Przejrzyj przydział dysku** Przejrzyj i w razie potrzeby zmodyfikuj hello miejsca na dysku dla hello maszyn wirtualnych. Witaj zalecane przydziały dysku są oparte na powitania zakres przechowywania, określonego w hello **Określ cele krótkoterminowe** strony, hello typu obciążenia i rozmiaru hello hello chronionych danych (określoną w kroku 3).  

  - **Rozmiar danych:** rozmiar hello danych w grupie ochrony hello.
  - **Miejsce na dysku:** hello zalecana ilość miejsca na dysku dla grupy ochrony hello. Jeśli chcesz toomodify to ustawienie, należy przydzielić całkowita ilość miejsca nieznacznie przekraczającą kwota hello oceniasz, że rozwoju każdego źródła danych.
  - **Przekazywanie danych do wspólnej lokalizacji:** po włączeniu kolokacji wiele źródeł danych w hello ochrony można mapować tooa pojedynczą replikę i wolumin punktu odzyskiwania. Kolokacja nie jest obsługiwana dla wszystkich obciążeń.
  - **Automatycznie rozszerzaj:** po włączeniu tego ustawienia, jeśli dane w grupie hello chronione przekroczy początkową alokacji hello, System Center Data Protection Manager próbuje rozmiar dysku hello tooincrease o 25 procent.
  - **Szczegóły puli magazynu:** pokazuje stan hello hello puli magazynu, tym całkowity rozmiar dysku i wolnego.

    ![Przejrzyj przydział dysku](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    Po zakończeniu przydzielenie miejsca na powitania kliknij **dalej**.

7. Na powitania **wybierz metodę tworzenia repliki** strony, należy określić sposób kopii początkowej hello toogenerate lub replika hello chronionych danych na serwerze kopii zapasowej Azure.

    Domyślnie Hello **automatycznie przez sieć hello** i **teraz**. Jeśli używasz domyślnego hello, zaleca się określenie poza godzinami szczytu. Wybierz **później** i określ dzień i godzinę.

    Dla dużych ilości danych lub mniej niż optymalnych warunkach sieci należy wziąć pod uwagę replikację danych hello w trybie offline przy użyciu nośnika wymiennego.

    Po dokonaniu wybrane opcje, kliknij przycisk **dalej**.

    ![Wybierz metodę tworzenia repliki](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. Na powitania **opcje sprawdzania spójności** wybierz, jak i kiedy sprawdzania spójności hello tooautomate. Można uruchomić sprawdzania spójności, gdy dane są niespójne, lub zgodnie z ustalonym harmonogramem.

    Jeśli nie chcesz, aby sprawdzanie spójności automatyczne tooconfigure, można uruchomić sprawdzanie ręczne. W obszarze ochrony hello hello Azure Utwórz kopię zapasową serwera konsoli, kliknij prawym przyciskiem myszy hello grupy ochrony, a następnie wybierz **Przeprowadź Sprawdzanie spójności**.

    Kliknij przycisk **dalej** toomove toohello następnej strony.

9. Na powitania **Określ dane chronione Online** wybierz co najmniej jedno źródło danych, które mają tooprotect. Wybierz członków hello indywidualnie lub kliknij przycisk **Zaznacz wszystko** toochoose wszystkie elementy członkowskie. Po wybraniu hello członków, kliknij przycisk **dalej**.

    ![Określ dane chronione w trybie online](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. Na powitania **określić harmonogram tworzenia kopii zapasowych Online** określ punkty odzyskiwania toogenerate harmonogram hello z hello kopii zapasowej. Po wygenerowaniu hello punkt odzyskiwania, jest magazyn usług odzyskiwania toohello przeniesione na platformie Azure. Po zakończeniu hello harmonogram tworzenia kopii zapasowej online, kliknij przycisk **dalej**.

    ![Określ harmonogram tworzenia kopii zapasowej online](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. Na powitania **Określanie zasad przechowywania Online** wskaż, jak długo mają tooretain hello kopii zapasowej danych na platformie Azure. Po zdefiniowaniu zasad powitania kliknij **dalej**.

    ![Określ zasady przechowywania danych online](./media/backup-azure-backup-server-vmware/retention-policy.png)

    Nie ma żadnego limitu czasu na jak długo dane można zachować na platformie Azure. Gdy dane punktu odzyskiwania są przechowywane na platformie Azure, hello tylko limit wynosi że nie może mieć więcej niż 9999 punkty odzyskiwania dla każdego chronionego wystąpienia. W tym przykładzie wystąpienie chronionych hello jest powitania serwera VMware.

12. Na powitania **Podsumowanie** , przejrzyj szczegóły powitania dla członków grupy ochrony i ustawienia, a następnie kliknij przycisk **Utwórz grupę**.

    ![Członka grupy ochrony i ustawienia — podsumowanie](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a>Następne kroki
Jeśli używasz serwera usługi Kopia zapasowa Azure tooprotect VMware obciążeń, może Cię zainteresować przy użyciu serwera kopii zapasowej Azure chronić toohelp [programu Microsoft Exchange server](./backup-azure-exchange-mabs.md), [farmy Microsoft SharePoint](./backup-azure-backup-sharepoint-mabs.md), lub [Bazy danych programu SQL Server](./backup-azure-sql-mabs.md).

Informacji dotyczących problemów z rejestrowaniem hello agenta, konfigurowania grupy ochrony hello lub tworzenie kopii zapasowych zadań, zobacz [Rozwiązywanie problemów z serwera usługi Kopia zapasowa Azure](./backup-azure-mabs-troubleshoot.md).
