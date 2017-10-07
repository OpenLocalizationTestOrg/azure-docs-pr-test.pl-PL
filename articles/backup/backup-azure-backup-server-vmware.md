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
# <a name="back-up-a-vmware-server-tooazure"></a><span data-ttu-id="98a93-104">Wykonaj kopię zapasową tooAzure serwer VMware</span><span class="sxs-lookup"><span data-stu-id="98a93-104">Back up a VMware server tooAzure</span></span>

<span data-ttu-id="98a93-105">W tym artykule opisano, jak toohelp serwer kopii zapasowej Azure tooconfigure chronić obciążeń serwera VMware.</span><span class="sxs-lookup"><span data-stu-id="98a93-105">This article explains how tooconfigure Azure Backup Server toohelp protect VMware server workloads.</span></span> <span data-ttu-id="98a93-106">W tym artykule przyjęto założenie, że masz już zainstalowany serwer kopii zapasowej Azure.</span><span class="sxs-lookup"><span data-stu-id="98a93-106">This article assumes you already have Azure Backup Server installed.</span></span> <span data-ttu-id="98a93-107">Jeśli nie masz zainstalowany serwer kopii zapasowej Azure, zobacz [przygotowanie tooback dużych obciążeń, za pomocą serwera usługi Kopia zapasowa Azure](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="98a93-107">If you don't have Azure Backup Server installed, see [Prepare tooback up workloads using Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span></span>

<span data-ttu-id="98a93-108">Serwer kopii zapasowej systemu Azure można utworzyć kopię zapasową lub lepiej chronić VMware vCenter Server w wersji 6.5, 6.0 i 5.5.</span><span class="sxs-lookup"><span data-stu-id="98a93-108">Azure Backup Server can back up, or help protect, VMware vCenter Server version 6.5, 6.0 and 5.5.</span></span>


## <a name="create-a-secure-connection-toohello-vcenter-server"></a><span data-ttu-id="98a93-109">Tworzenie serwera vCenter toohello bezpiecznego połączenia</span><span class="sxs-lookup"><span data-stu-id="98a93-109">Create a secure connection toohello vCenter Server</span></span>

<span data-ttu-id="98a93-110">Domyślnie serwer kopii zapasowej Azure komunikuje się z każdym vCenter Server za pośrednictwem kanału HTTPS.</span><span class="sxs-lookup"><span data-stu-id="98a93-110">By default, Azure Backup Server communicates with each vCenter Server via an HTTPS channel.</span></span> <span data-ttu-id="98a93-111">tooturn na powitania bezpiecznej komunikacji, zalecamy zainstalowanie hello VMware urzędu certyfikacji certyfikatu na serwerze kopii zapasowej Azure.</span><span class="sxs-lookup"><span data-stu-id="98a93-111">tooturn on hello secure communication, we recommend that you install hello VMware Certificate Authority (CA) certificate on Azure Backup Server.</span></span> <span data-ttu-id="98a93-112">Jeśli nie wymagają bezpiecznej komunikacji i wolisz toodisable hello HTTPS wymagania, zobacz [wyłączanie bezpiecznej komunikacji protokołu](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span><span class="sxs-lookup"><span data-stu-id="98a93-112">If you don't require secure communication, and would prefer toodisable hello HTTPS requirement, see [Disable secure communication protocol](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span></span> <span data-ttu-id="98a93-113">toocreate bezpiecznego połączenia między serwerem kopia zapasowa Azure i hello vCenter Server, zaimportuj hello zaufanego certyfikatu na serwerze kopii zapasowej Azure.</span><span class="sxs-lookup"><span data-stu-id="98a93-113">toocreate a secure connection between Azure Backup Server and hello vCenter Server, import hello trusted certificate on Azure Backup Server.</span></span>

<span data-ttu-id="98a93-114">Zazwyczaj użytkownik korzysta z przeglądarki na powitania serwera usługi Kopia zapasowa Azure maszyny tooconnect toohello vCenter Server za pośrednictwem vSphere powitania klienta sieci Web.</span><span class="sxs-lookup"><span data-stu-id="98a93-114">Typically, you use a browser on hello Azure Backup Server machine tooconnect toohello vCenter Server via hello vSphere Web Client.</span></span> <span data-ttu-id="98a93-115">Witaj po raz pierwszy używasz hello serwer kopii zapasowej Azure przeglądarki tooconnect toohello vCenter Server, hello połączenia nie jest zabezpieczone.</span><span class="sxs-lookup"><span data-stu-id="98a93-115">hello first time you use hello Azure Backup Server browser tooconnect toohello vCenter Server, hello connection isn't secure.</span></span> <span data-ttu-id="98a93-116">powitania po obraz pokazuje hello niezabezpieczone połączenie.</span><span class="sxs-lookup"><span data-stu-id="98a93-116">hello following image shows hello unsecured connection.</span></span>

![Przykład serwera tooVMware niezabezpieczone połączenie](./media/backup-azure-backup-server-vmware/unsecure-url.png)

<span data-ttu-id="98a93-118">toofix ten problem i utworzenia bezpiecznego połączenia, Pobierz hello zaufanych certyfikatów głównego urzędu certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="98a93-118">toofix this issue, and create a secure connection, download hello trusted root CA certificates.</span></span>

1. <span data-ttu-id="98a93-119">W przeglądarce hello na serwerze kopii zapasowej Azure wprowadź vSphere toohello adres URL powitania klienta sieci Web.</span><span class="sxs-lookup"><span data-stu-id="98a93-119">In hello browser on Azure Backup Server, enter hello URL toohello vSphere Web Client.</span></span> <span data-ttu-id="98a93-120">zostanie wyświetlona strona logowania klienta sieci Web vSphere Hello.</span><span class="sxs-lookup"><span data-stu-id="98a93-120">hello vSphere Web Client login page appears.</span></span>

    ![vSphere klienta sieci Web](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    <span data-ttu-id="98a93-122">U dołu hello hello informacje dla administratorów i deweloperów, zlokalizuj hello **pobierania zaufane certyfikaty głównego urzędu certyfikacji** łącza.</span><span class="sxs-lookup"><span data-stu-id="98a93-122">At hello bottom of hello information for administrators and developers, locate hello **Download trusted root CA certificates** link.</span></span>

    ![Łącze toodownload hello zaufanego głównego urzędu certyfikacji](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  <span data-ttu-id="98a93-124">Jeśli widzisz stronę logowania klienta sieci Web vSphere hello, sprawdź ustawienia serwera proxy przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="98a93-124">If you don't see hello vSphere Web Client login page, check your browser's proxy settings.</span></span>

2. <span data-ttu-id="98a93-125">Kliknij przycisk **pobierania zaufane certyfikaty głównego urzędu certyfikacji**.</span><span class="sxs-lookup"><span data-stu-id="98a93-125">Click **Download trusted root CA certificates**.</span></span>

    <span data-ttu-id="98a93-126">Serwer vCenter Hello pliki do pobrania na komputerze lokalnym tooyour pliku.</span><span class="sxs-lookup"><span data-stu-id="98a93-126">hello vCenter Server downloads a file tooyour local computer.</span></span> <span data-ttu-id="98a93-127">Witaj nazwę pliku o nazwie **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="98a93-127">hello file's name is named **download**.</span></span> <span data-ttu-id="98a93-128">W zależności od przeglądarki, zostanie wyświetlony komunikat z pytaniem, czy tooopen lub zapisać plik hello.</span><span class="sxs-lookup"><span data-stu-id="98a93-128">Depending on your browser, you receive a message that asks whether tooopen or save hello file.</span></span>

    ![Pobierz wiadomość, gdy są pobierane certyfikaty](./media/backup-azure-backup-server-vmware/download-certs.png)

3. <span data-ttu-id="98a93-130">Zapisz hello pliku tooa lokalizacji na serwerze kopii zapasowej Azure.</span><span class="sxs-lookup"><span data-stu-id="98a93-130">Save hello file tooa location on Azure Backup Server.</span></span> <span data-ttu-id="98a93-131">Podczas zapisywania pliku hello dodać rozszerzenie nazwy pliku zip hello.</span><span class="sxs-lookup"><span data-stu-id="98a93-131">When you save hello file, add hello .zip file name extension.</span></span>

    <span data-ttu-id="98a93-132">Plik Hello jest plik zip zawierający hello informacji o certyfikatach hello.</span><span class="sxs-lookup"><span data-stu-id="98a93-132">hello file is a .zip file that contains hello information about hello certificates.</span></span> <span data-ttu-id="98a93-133">Z rozszerzeniem .zip hello można użyć narzędzia wyodrębniania hello.</span><span class="sxs-lookup"><span data-stu-id="98a93-133">With hello .zip extension, you can use hello extraction tools.</span></span>

4. <span data-ttu-id="98a93-134">Kliknij prawym przyciskiem myszy **download.zip**, a następnie wybierz **Wyodrębnij wszystkie** tooextract hello zawartość.</span><span class="sxs-lookup"><span data-stu-id="98a93-134">Right-click **download.zip**, and then select **Extract All** tooextract hello contents.</span></span>

    <span data-ttu-id="98a93-135">plik zip Hello wyodrębnia jego zawartość folderów tooa o nazwie **certyfikaty**.</span><span class="sxs-lookup"><span data-stu-id="98a93-135">hello .zip file extracts its contents tooa folder named **certs**.</span></span> <span data-ttu-id="98a93-136">W folderze Certyfikaty hello są wyświetlane dwa typy plików.</span><span class="sxs-lookup"><span data-stu-id="98a93-136">Two types of files appear in hello certs folder.</span></span> <span data-ttu-id="98a93-137">plik certyfikatu głównego Hello ma rozszerzenie, który rozpoczyna się od numeru sekwencji.0 i.1.</span><span class="sxs-lookup"><span data-stu-id="98a93-137">hello root certificate file has an extension that begins with a numbered sequence like .0 and .1.</span></span>
    
    <span data-ttu-id="98a93-138">Witaj listy CRL plik ma rozszerzenie, rozpoczynający się od sekwencji, takich jak .r0 lub .r1.</span><span class="sxs-lookup"><span data-stu-id="98a93-138">hello CRL file has an extension that begins with a sequence like .r0 or .r1.</span></span> <span data-ttu-id="98a93-139">Plik listy CRL Hello jest skojarzony z certyfikatem.</span><span class="sxs-lookup"><span data-stu-id="98a93-139">hello CRL file is associated with a certificate.</span></span>

    ![<span data-ttu-id="98a93-140">Pobierz plik wyodrębnione lokalnie</span><span class="sxs-lookup"><span data-stu-id="98a93-140">Download file extracted locally</span></span> ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. <span data-ttu-id="98a93-141">W hello **certyfikaty** folderu, kliknij prawym przyciskiem myszy plik certyfikatu głównego hello, a następnie kliknij przycisk **zmienić**.</span><span class="sxs-lookup"><span data-stu-id="98a93-141">In hello **certs** folder, right-click hello root certificate file, and then click **Rename**.</span></span>

    ![<span data-ttu-id="98a93-142">Zmień nazwę certyfikatu głównego</span><span class="sxs-lookup"><span data-stu-id="98a93-142">Rename root certificate</span></span> ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    <span data-ttu-id="98a93-143">Zmienianie certyfikatu głównego hello too.crt rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="98a93-143">Change hello root certificate's extension too.crt.</span></span> <span data-ttu-id="98a93-144">Pytanie, jeśli masz pewności, mają rozszerzenie hello toochange, kliknij przycisk **tak** lub **OK**.</span><span class="sxs-lookup"><span data-stu-id="98a93-144">When you're asked if you're sure you want toochange hello extension, click **Yes** or **OK**.</span></span> <span data-ttu-id="98a93-145">W przeciwnym razie możesz zmienić funkcji hello pliku.</span><span class="sxs-lookup"><span data-stu-id="98a93-145">Otherwise, you change hello file's intended function.</span></span> <span data-ttu-id="98a93-146">Ikona Hello hello pliku zmiany tooan ikonę, która reprezentuje certyfikatu głównego.</span><span class="sxs-lookup"><span data-stu-id="98a93-146">hello icon for hello file changes tooan icon that represents a root certificate.</span></span>

6. <span data-ttu-id="98a93-147">Kliknij prawym przyciskiem myszy certyfikat główny hello i wybierz z menu podręcznego hello **Zainstaluj certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="98a93-147">Right-click hello root certificate and from hello pop-up menu, select **Install Certificate**.</span></span>

    <span data-ttu-id="98a93-148">Witaj **Kreatora importu certyfikatów** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="98a93-148">hello **Certificate Import Wizard** dialog box appears.</span></span>

7. <span data-ttu-id="98a93-149">W hello **Kreatora importu certyfikatów** okno dialogowe, wybierz opcję **komputera lokalnego** jako miejsce docelowe hello hello certyfikatu, a następnie kliknij przycisk **dalej** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="98a93-149">In hello **Certificate Import Wizard** dialog box, select **Local Machine** as hello destination for hello certificate, and then click **Next** toocontinue.</span></span>

    ![<span data-ttu-id="98a93-150">Opcje docelowy magazyn certyfikatów</span><span class="sxs-lookup"><span data-stu-id="98a93-150">Certificate storage destination options</span></span> ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    <span data-ttu-id="98a93-151">Jeśli pojawi się monit Jeśli chcesz tooallow zmiany toohello komputer, kliknij przycisk **tak** lub **OK**, tooall hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="98a93-151">If you're asked if you want tooallow changes toohello computer, click **Yes** or **OK**, tooall hello changes.</span></span>

8. <span data-ttu-id="98a93-152">Na powitania **magazyn certyfikatów** wybierz pozycję **Umieść wszystkie certyfikaty w powitania po magazynu**, a następnie kliknij przycisk **Przeglądaj** magazynu certyfikatów hello toochoose.</span><span class="sxs-lookup"><span data-stu-id="98a93-152">On hello **Certificate Store** page, select **Place all certificates in hello following store**, and then click **Browse** toochoose hello certificate store.</span></span>

    ![Umieść w miejscu określonego magazynu certyfikatów](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    <span data-ttu-id="98a93-154">Witaj **wybierz magazyn certyfikatów** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="98a93-154">hello **Select Certificate Store** dialog box appears.</span></span>

    ![Hierarchia folderów magazyn certyfikatów](./media/backup-azure-backup-server-vmware/cert-store.png)

9. <span data-ttu-id="98a93-156">Wybierz **zaufane główne urzędy certyfikacji** jako folder docelowy hello hello certyfikatów, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="98a93-156">Select **Trusted Root Certification Authorities** as hello destination folder for hello certificates, and then click **OK**.</span></span>

    ![Folder docelowy certyfikatu](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    <span data-ttu-id="98a93-158">Witaj **zaufane główne urzędy certyfikacji** folder został potwierdzony jako hello magazynu certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="98a93-158">hello **Trusted Root Certification Authorities** folder is confirmed as hello certificate store.</span></span> <span data-ttu-id="98a93-159">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="98a93-159">Click **Next**.</span></span>

    ![Folder magazynu certyfikatów](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. <span data-ttu-id="98a93-161">Na powitania **hello Kończenie pracy Kreatora importu certyfikatów** zweryfikować certyfikat hello znajduje się w folderze żądaną hello, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="98a93-161">On hello **Completing hello Certificate Import Wizard** page, verify that hello certificate is in hello desired folder, and then click **Finish**.</span></span>

    ![Sprawdź, czy certyfikat znajduje się w folderze prawidłowego hello](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    <span data-ttu-id="98a93-163">Zostanie wyświetlone okno dialogowe, importu certyfikatów pomyślnie hello został potwierdzony.</span><span class="sxs-lookup"><span data-stu-id="98a93-163">A dialog box appears, hello successful certificate import is confirmed.</span></span>

11. <span data-ttu-id="98a93-164">Zaloguj się toohello vCenter Server tooconfirm, że połączenie jest bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="98a93-164">Sign in toohello vCenter Server tooconfirm that your connection is secure.</span></span>

  <span data-ttu-id="98a93-165">Jeśli hello certyfikat import zakończy się niepowodzeniem i nie można ustanowić bezpiecznego połączenia, w dokumentacji hello VMware vSphere na [uzyskiwanie certyfikatów serwera](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span><span class="sxs-lookup"><span data-stu-id="98a93-165">If hello certificate import is not successful, and you cannot establish a secure connection, consult hello VMware vSphere documentation on [obtaining server certificates](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span></span>

  <span data-ttu-id="98a93-166">Jeśli masz bezpiecznych granic w ramach danej organizacji, a nie mają tooturn na powitania protokołu HTTPS, należy użyć hello następujące procedury toodisable hello bezpieczną komunikację.</span><span class="sxs-lookup"><span data-stu-id="98a93-166">If you have secure boundaries within your organization, and don't want tooturn on hello HTTPS protocol, use hello following procedure toodisable hello secure communications.</span></span>

### <a name="disable-secure-communication-protocol"></a><span data-ttu-id="98a93-167">Wyłącz protokół bezpiecznej komunikacji</span><span class="sxs-lookup"><span data-stu-id="98a93-167">Disable secure communication protocol</span></span>

<span data-ttu-id="98a93-168">Jeśli Twoja organizacja nie wymaga hello protokołu HTTPS, należy użyć hello następujące kroki toodisable HTTPS.</span><span class="sxs-lookup"><span data-stu-id="98a93-168">If your organization doesn't require hello HTTPS protocol, use hello following steps toodisable HTTPS.</span></span> <span data-ttu-id="98a93-169">toodisable hello domyślne zachowanie, należy utworzyć klucz rejestru, który ignoruje hello domyślne zachowanie.</span><span class="sxs-lookup"><span data-stu-id="98a93-169">toodisable hello default behavior, create a registry key that ignores hello default behavior.</span></span>

1. <span data-ttu-id="98a93-170">Skopiuj i Wklej powitania po tekstu do pliku txt.</span><span class="sxs-lookup"><span data-stu-id="98a93-170">Copy and paste hello following text into a .txt file.</span></span>

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. <span data-ttu-id="98a93-171">Zapisz hello pliku tooyour serwer kopii zapasowej Azure komputera.</span><span class="sxs-lookup"><span data-stu-id="98a93-171">Save hello file tooyour Azure Backup Server computer.</span></span> <span data-ttu-id="98a93-172">Nazwa pliku hello Użyj DisableSecureAuthentication.reg.</span><span class="sxs-lookup"><span data-stu-id="98a93-172">For hello file name, use DisableSecureAuthentication.reg.</span></span>

3. <span data-ttu-id="98a93-173">Kliknij dwukrotnie wpis rejestru hello hello pliku tooactivate.</span><span class="sxs-lookup"><span data-stu-id="98a93-173">Double-click hello file tooactivate hello registry entry.</span></span>


## <a name="create-a-role-and-user-account-on-hello-vcenter-server"></a><span data-ttu-id="98a93-174">Utwórz konto rolę i użytkownika na powitania vCenter Server</span><span class="sxs-lookup"><span data-stu-id="98a93-174">Create a role and user account on hello vCenter Server</span></span>

<span data-ttu-id="98a93-175">Witaj programie vcenter Server Rola to wstępnie zdefiniowane uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="98a93-175">On hello vCenter Server, a role is a predefined set of privileges.</span></span> <span data-ttu-id="98a93-176">Administrator serwera vCenter tworzy hello ról.</span><span class="sxs-lookup"><span data-stu-id="98a93-176">A vCenter Server administrator creates hello roles.</span></span> <span data-ttu-id="98a93-177">uprawnienia tooassign administratora hello pary kont użytkowników z roli.</span><span class="sxs-lookup"><span data-stu-id="98a93-177">tooassign permissions, hello administrator pairs user accounts with a role.</span></span> <span data-ttu-id="98a93-178">tooestablish hello niezbędnych poświadczeń tooback hello komputera serwera vCenter, utworzyć rolę z określone uprawnienia, a następnie skojarzyć hello konta użytkownika z rolą hello.</span><span class="sxs-lookup"><span data-stu-id="98a93-178">tooestablish hello necessary user credentials tooback up hello vCenter Server computer, create a role with specific privileges, and then associate hello user account with hello role.</span></span>

<span data-ttu-id="98a93-179">Serwer kopii zapasowej systemu Azure używa tooauthenticate nazwę użytkownika i hasło z hello vCenter Server.</span><span class="sxs-lookup"><span data-stu-id="98a93-179">Azure Backup Server uses a username and password tooauthenticate with hello vCenter Server.</span></span> <span data-ttu-id="98a93-180">Serwer kopii zapasowej systemu Azure używa tych poświadczeń uwierzytelniania dla wszystkich operacji tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="98a93-180">Azure Backup Server uses these credentials as authentication for all backup operations.</span></span>

<span data-ttu-id="98a93-181">tooadd vCenter roli serwera i jego uprawnień administratora kopii zapasowych:</span><span class="sxs-lookup"><span data-stu-id="98a93-181">tooadd a vCenter Server role and its privileges for a backup administrator:</span></span>

1. <span data-ttu-id="98a93-182">Zaloguj się w toohello vCenter Server, a następnie w programie hello vCenter Server **Nawigator** panelu, kliknij przycisk **administracji**.</span><span class="sxs-lookup"><span data-stu-id="98a93-182">Sign in toohello vCenter Server, and then in hello vCenter Server **Navigator** panel, click **Administration**.</span></span>

    ![Opcja administracji w panelu Nawigator serwera vCenter](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. <span data-ttu-id="98a93-184">W **administracji** wybierz **ról**, a następnie w hello **ról** kliknij panel hello dodać ikona roli (hello + symbol).</span><span class="sxs-lookup"><span data-stu-id="98a93-184">In **Administration** select **Roles**, and then in hello **Roles** panel click hello add role icon (hello + symbol).</span></span>

    ![Dodaj rolę](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    <span data-ttu-id="98a93-186">Witaj **Utwórz rolę** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="98a93-186">hello **Create Role** dialog box appears.</span></span>

    ![Tworzenie roli](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. <span data-ttu-id="98a93-188">W hello **Utwórz rolę** okno dialogowe, w hello **nazwy roli** wprowadź *BackupAdminRole*.</span><span class="sxs-lookup"><span data-stu-id="98a93-188">In hello **Create Role** dialog box, in hello **Role name** box, enter *BackupAdminRole*.</span></span> <span data-ttu-id="98a93-189">Nazwa roli Hello może być dowolne, ale powinien być rozpoznawalną w celu hello roli.</span><span class="sxs-lookup"><span data-stu-id="98a93-189">hello role name can be whatever you like, but it should be recognizable for hello role's purpose.</span></span>

4. <span data-ttu-id="98a93-190">Wybierz uprawnienia hello hello odpowiedniej wersji programu vCenter, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="98a93-190">Select hello privileges for hello appropriate version of vCenter, and then click **OK**.</span></span> <span data-ttu-id="98a93-191">w poniższej tabeli Hello identyfikuje hello wymagane uprawnienia dla vCenter 6.0 i vCenter 5.5.</span><span class="sxs-lookup"><span data-stu-id="98a93-191">hello following table identifies hello required privileges for vCenter 6.0 and vCenter 5.5.</span></span>

  <span data-ttu-id="98a93-192">Po wybraniu hello uprawnień, kliknij przycisk hello ikona dalej toohello nadrzędny etykiety tooexpand hello nadrzędne i widoku hello podrzędnych uprawnień.</span><span class="sxs-lookup"><span data-stu-id="98a93-192">When you select hello privileges, click hello icon next toohello parent label tooexpand hello parent and view hello child privileges.</span></span> <span data-ttu-id="98a93-193">tooselect hello VirtualMachine uprawnień, należy toogo kilka poziomów do hello nadrzędnego hierarchii podrzędnej.</span><span class="sxs-lookup"><span data-stu-id="98a93-193">tooselect hello VirtualMachine privileges, you need toogo several levels into hello parent child hierarchy.</span></span> <span data-ttu-id="98a93-194">Nie trzeba tooselect wszystkie uprawnienia podrzędnego w obrębie uprawnienie nadrzędne.</span><span class="sxs-lookup"><span data-stu-id="98a93-194">You don't need tooselect all child privileges within a parent privilege.</span></span>

  ![Uprawnienie hierarchii nadrzędny-podrzędny](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  <span data-ttu-id="98a93-196">Po kliknięciu **OK**, hello nową rolę pojawia się na liście hello na panelu ról hello.</span><span class="sxs-lookup"><span data-stu-id="98a93-196">After you click **OK**, hello new role appears in hello list on hello Roles panel.</span></span>

|<span data-ttu-id="98a93-197">Uprawnienia dla serwera vCenter 6.0</span><span class="sxs-lookup"><span data-stu-id="98a93-197">Privileges for vCenter 6.0</span></span>| <span data-ttu-id="98a93-198">Uprawnienia dla serwera vCenter 5,5</span><span class="sxs-lookup"><span data-stu-id="98a93-198">Privileges for vCenter 5.5</span></span>|
|--------------------------|---------------------------|
|<span data-ttu-id="98a93-199">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="98a93-199">Datastore.AllocateSpace</span></span>   | <span data-ttu-id="98a93-200">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="98a93-200">Datastore.AllocateSpace</span></span>|
|<span data-ttu-id="98a93-201">Global.ManageCustomFields</span><span class="sxs-lookup"><span data-stu-id="98a93-201">Global.ManageCustomFields</span></span> | <span data-ttu-id="98a93-202">Global.ManageCustomerFields</span><span class="sxs-lookup"><span data-stu-id="98a93-202">Global.ManageCustomerFields</span></span>|
|<span data-ttu-id="98a93-203">Global.SetCustomFields</span><span class="sxs-lookup"><span data-stu-id="98a93-203">Global.SetCustomFields</span></span>    |   |
|<span data-ttu-id="98a93-204">Host.Local.CreateVM</span><span class="sxs-lookup"><span data-stu-id="98a93-204">Host.Local.CreateVM</span></span>       | <span data-ttu-id="98a93-205">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="98a93-205">Network.Assign</span></span> |
|<span data-ttu-id="98a93-206">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="98a93-206">Network.Assign</span></span>            |  |
|<span data-ttu-id="98a93-207">Resource.AssignVMToPool</span><span class="sxs-lookup"><span data-stu-id="98a93-207">Resource.AssignVMToPool</span></span>   |  |
|<span data-ttu-id="98a93-208">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="98a93-208">VirtualMachine.Config.AddNewDisk</span></span>  | <span data-ttu-id="98a93-209">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="98a93-209">VirtualMachine.Config.AddNewDisk</span></span>   |
|<span data-ttu-id="98a93-210">VirtualMachine.Config.AdvanceConfig</span><span class="sxs-lookup"><span data-stu-id="98a93-210">VirtualMachine.Config.AdvanceConfig</span></span>| <span data-ttu-id="98a93-211">VirtualMachine.Config.AdvancedConfig</span><span class="sxs-lookup"><span data-stu-id="98a93-211">VirtualMachine.Config.AdvancedConfig</span></span>|
|<span data-ttu-id="98a93-212">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="98a93-212">VirtualMachine.Config.ChangeTracking</span></span>| <span data-ttu-id="98a93-213">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="98a93-213">VirtualMachine.Config.ChangeTracking</span></span> |
|<span data-ttu-id="98a93-214">VirtualMachine.Config.HostUSBDevice</span><span class="sxs-lookup"><span data-stu-id="98a93-214">VirtualMachine.Config.HostUSBDevice</span></span>||
|<span data-ttu-id="98a93-215">VirtualMachine.Config.QueryUnownedFiles</span><span class="sxs-lookup"><span data-stu-id="98a93-215">VirtualMachine.Config.QueryUnownedFiles</span></span>|    |
|<span data-ttu-id="98a93-216">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="98a93-216">VirtualMachine.Config.SwapPlacement</span></span>| <span data-ttu-id="98a93-217">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="98a93-217">VirtualMachine.Config.SwapPlacement</span></span> |
|<span data-ttu-id="98a93-218">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="98a93-218">VirtualMachine.Interact.PowerOff</span></span>| <span data-ttu-id="98a93-219">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="98a93-219">VirtualMachine.Interact.PowerOff</span></span> |
|<span data-ttu-id="98a93-220">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="98a93-220">VirtualMachine.Inventory.Create</span></span>| <span data-ttu-id="98a93-221">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="98a93-221">VirtualMachine.Inventory.Create</span></span> |
|<span data-ttu-id="98a93-222">VirtualMachine.Provisioning.DiskRandomAccess</span><span class="sxs-lookup"><span data-stu-id="98a93-222">VirtualMachine.Provisioning.DiskRandomAccess</span></span>| |
|<span data-ttu-id="98a93-223">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="98a93-223">VirtualMachine.Provisioning.DiskRandomRead</span></span>|<span data-ttu-id="98a93-224">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="98a93-224">VirtualMachine.Provisioning.DiskRandomRead</span></span> |
|<span data-ttu-id="98a93-225">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="98a93-225">VirtualMachine.State.CreateSnapshot</span></span>| <span data-ttu-id="98a93-226">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="98a93-226">VirtualMachine.State.CreateSnapshot</span></span>|
|<span data-ttu-id="98a93-227">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="98a93-227">VirtualMachine.State.RemoveSnapshot</span></span>|<span data-ttu-id="98a93-228">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="98a93-228">VirtualMachine.State.RemoveSnapshot</span></span> |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a><span data-ttu-id="98a93-229">Tworzenie konta użytkownika serwera vCenter i uprawnień</span><span class="sxs-lookup"><span data-stu-id="98a93-229">Create a vCenter Server user account and permissions</span></span>

<span data-ttu-id="98a93-230">Po skonfigurowaniu roli hello z uprawnieniami, Utwórz konto użytkownika.</span><span class="sxs-lookup"><span data-stu-id="98a93-230">After hello role with privileges is set up, create a user account.</span></span> <span data-ttu-id="98a93-231">konto użytkownika Hello ma nazwę i hasło, które udostępnia hello poświadczenia, które są używane do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="98a93-231">hello user account has a name and password, which provides hello credentials that are used for authentication.</span></span>

1. <span data-ttu-id="98a93-232">konto użytkownika w programie hello vCenter Server toocreate **Nawigator** panelu, kliknij przycisk **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="98a93-232">toocreate a user account, in hello vCenter Server **Navigator** panel, click **Users and Groups**.</span></span>

    ![Opcja użytkowników i grup](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    <span data-ttu-id="98a93-234">Witaj **vCenter użytkowników i grup** pojawi się panel.</span><span class="sxs-lookup"><span data-stu-id="98a93-234">hello **vCenter Users and Groups** panel appears.</span></span>

    ![panel vCenter użytkowników i grup](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. <span data-ttu-id="98a93-236">W hello **vCenter użytkowników i grup** panelu, wybierz opcję hello **użytkowników** , a następnie kliknij pozycję hello dodać ikonę użytkowników (hello + symbol).</span><span class="sxs-lookup"><span data-stu-id="98a93-236">In hello **vCenter Users and Groups** panel, select hello **Users** tab, and then click hello add users icon (hello + symbol).</span></span>

    <span data-ttu-id="98a93-237">Witaj **nowego użytkownika** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="98a93-237">hello **New User** dialog box appears.</span></span>

3. <span data-ttu-id="98a93-238">W hello **nowego użytkownika** okna dialogowego, Dodaj informacje o użytkowniku hello a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="98a93-238">In hello **New User** dialog box, add hello user's information and then click **OK**.</span></span> <span data-ttu-id="98a93-239">W tej procedurze hello username jest BackupAdmin.</span><span class="sxs-lookup"><span data-stu-id="98a93-239">In this procedure, hello username is BackupAdmin.</span></span>

    ![Okno dialogowe Nowy użytkownik](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    <span data-ttu-id="98a93-241">Hello nowe konto użytkownika zostanie wyświetlony na liście hello.</span><span class="sxs-lookup"><span data-stu-id="98a93-241">hello new user account appears in hello list.</span></span>

4. <span data-ttu-id="98a93-242">konto użytkownika hello tooassociate z roli hello w hello **Nawigator** panelu, kliknij przycisk **uprawnień globalnych**.</span><span class="sxs-lookup"><span data-stu-id="98a93-242">tooassociate hello user account with hello role, in hello **Navigator** panel, click **Global Permissions**.</span></span> <span data-ttu-id="98a93-243">W hello **uprawnień globalnych** panelu, wybierz opcję hello **Zarządzaj** , a następnie kliknij pozycję hello dodać ikonę (hello + symbol).</span><span class="sxs-lookup"><span data-stu-id="98a93-243">In hello **Global Permissions** panel, select hello **Manage** tab, and then click hello add icon (hello + symbol).</span></span>

    ![Panel uprawnień globalnych](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    <span data-ttu-id="98a93-245">Witaj **globalnych uprawnień Root - Dodaj uprawnienie** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="98a93-245">hello **Global Permissions Root - Add Permission** dialog box appears.</span></span>

5. <span data-ttu-id="98a93-246">W hello **globalnych uprawnień Root - Dodaj uprawnienie** okno dialogowe, kliknij przycisk **Dodaj** toochoose hello użytkownika lub grupy.</span><span class="sxs-lookup"><span data-stu-id="98a93-246">In hello **Global Permission Root - Add Permission** dialog box, click **Add** toochoose hello user or group.</span></span>

    ![Wybierz użytkownika lub grupy](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    <span data-ttu-id="98a93-248">Witaj **użytkowników/grupy wybierz** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="98a93-248">hello **Select Users/Groups** dialog box appears.</span></span>

6. <span data-ttu-id="98a93-249">W hello **użytkowników/grupy wybierz** oknie dialogowym wybierz **BackupAdmin** , a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="98a93-249">In hello **Select Users/Groups** dialog box, choose **BackupAdmin** and then click **Add**.</span></span>

    <span data-ttu-id="98a93-250">W **użytkowników**, hello *domena azwa_użytkownika* format jest używany dla hello konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="98a93-250">In **Users**, hello *domain\username* format is used for hello user account.</span></span> <span data-ttu-id="98a93-251">Jeśli chcesz toouse inną domenę, wybierz go z hello **domeny** listy.</span><span class="sxs-lookup"><span data-stu-id="98a93-251">If you want toouse a different domain, choose it from hello **Domain** list.</span></span>

    ![Dodaj użytkownika BackupAdmin](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    <span data-ttu-id="98a93-253">Kliknij przycisk **OK** tooadd hello wybrane toohello użytkowników **dodać uprawnienia** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="98a93-253">Click **OK** tooadd hello selected users toohello **Add Permission** dialog box.</span></span>

7. <span data-ttu-id="98a93-254">Teraz, gdy wyłaniają hello użytkownika, należy przypisać rolę toohello użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="98a93-254">Now that you've identified hello user, assign hello user toohello role.</span></span> <span data-ttu-id="98a93-255">W **przypisana rola**, wybierz z listy rozwijanej hello **BackupAdminRole**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="98a93-255">In **Assigned Role**, from hello drop-down list, select **BackupAdminRole**, and then click **OK**.</span></span>

    ![Przypisz toorole użytkownika](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  <span data-ttu-id="98a93-257">Na powitania **Zarządzaj** kartę w hello **uprawnień globalnych** panelu, hello nowego konta użytkownika i roli hello skojarzone są wyświetlane na liście hello.</span><span class="sxs-lookup"><span data-stu-id="98a93-257">On hello **Manage** tab in hello **Global Permissions** panel, hello new user account and hello associated role appear in hello list.</span></span>


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a><span data-ttu-id="98a93-258">Ustanowić poświadczenia serwera vCenter na serwerze kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="98a93-258">Establish vCenter Server credentials on Azure Backup Server</span></span>

<span data-ttu-id="98a93-259">Przed dodaniem hello VMware server tooAzure kopii zapasowej serwera należy zainstalować [aktualizacji 1 dla serwera usługi Kopia zapasowa Azure](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span><span class="sxs-lookup"><span data-stu-id="98a93-259">Before you add hello VMware server tooAzure Backup Server, install [Update 1 for Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span></span>

1. <span data-ttu-id="98a93-260">tooopen serwer kopii zapasowej Azure, kliknij dwukrotnie ikonę hello na powitania serwera usługi Kopia zapasowa Azure pulpitu.</span><span class="sxs-lookup"><span data-stu-id="98a93-260">tooopen Azure Backup Server, double-click hello icon on hello Azure Backup Server desktop.</span></span>

    ![Ikona serwera kopia zapasowa Azure](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    <span data-ttu-id="98a93-262">Jeśli nie możesz znaleźć hello ikony na pulpicie hello, należy otworzyć serwer kopii zapasowej Azure z hello listę zainstalowanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="98a93-262">If you can't find hello icon on hello desktop, open Azure Backup Server from hello list of installed apps.</span></span> <span data-ttu-id="98a93-263">Nazwa aplikacji Hello serwer kopii zapasowej Azure jest nazywany kopia zapasowa Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="98a93-263">hello Azure Backup Server app name is called Microsoft Azure Backup.</span></span>

2. <span data-ttu-id="98a93-264">W hello Azure Utwórz kopię zapasową serwera konsoli, kliknij **zarządzania**, kliknij przycisk **serwerów produkcyjnych**, a następnie na wstążce narzędzi hello, kliknij przycisk **Zarządzanie VMware**.</span><span class="sxs-lookup"><span data-stu-id="98a93-264">In hello Azure Backup Server console, click **Management**, click **Production Servers**, and then on hello tool ribbon, click **Manage VMware**.</span></span>

    ![Konsoli serwera kopii zapasowej platformy Azure](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    <span data-ttu-id="98a93-266">Witaj **poświadczenia zarządzania** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="98a93-266">hello **Manage Credentials** dialog box appears.</span></span>

    ![Okno dialogowe poświadczenia zarządzania serwera kopii zapasowej systemu Azure](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. <span data-ttu-id="98a93-268">W hello **poświadczenia zarządzania** okno dialogowe, kliknij przycisk **Dodaj** tooopen hello **Dodaj poświadczenie** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="98a93-268">In hello **Manage Credentials** dialog box, click **Add** tooopen hello **Add Credential** dialog box.</span></span>

4. <span data-ttu-id="98a93-269">W hello **Dodaj poświadczenie** okna dialogowego wprowadź nazwę i opis dla hello nowe poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="98a93-269">In hello **Add Credential** dialog box, enter a name and a description for hello new credential.</span></span> <span data-ttu-id="98a93-270">Następnie określ hello nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="98a93-270">Then specify hello username and password.</span></span> <span data-ttu-id="98a93-271">Nazwa Hello *poświadczeń Contoso Vcenter* służy tooidentify hello poświadczenia w następnej procedurze hello.</span><span class="sxs-lookup"><span data-stu-id="98a93-271">hello name, *Contoso Vcenter credential* is used tooidentify hello credential in hello next procedure.</span></span> <span data-ttu-id="98a93-272">Użyj hello takie same nazwy użytkownika i hasło, które jest używane dla hello vCenter Server.</span><span class="sxs-lookup"><span data-stu-id="98a93-272">Use hello same username and password that is used for hello vCenter Server.</span></span> <span data-ttu-id="98a93-273">Jeśli hello programu vCenter Server i serwer kopii zapasowej Azure nie znajdują się w hello w tej samej domenie, **nazwy użytkownika**, określ hello domeny.</span><span class="sxs-lookup"><span data-stu-id="98a93-273">If hello vCenter Server and Azure Backup Server are not in hello same domain, in **User name**, specify hello domain.</span></span>

    ![Okno dialogowe poświadczeń dodawania serwera kopii zapasowej platformy Azure](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    <span data-ttu-id="98a93-275">Kliknij przycisk **Dodaj** tooadd hello nowych poświadczeń tooAzure Utwórz kopię zapasową serwera.</span><span class="sxs-lookup"><span data-stu-id="98a93-275">Click **Add** tooadd hello new credential tooAzure Backup Server.</span></span> <span data-ttu-id="98a93-276">nowe poświadczenie Hello jest widoczna na liście hello w hello **poświadczenia zarządzania** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="98a93-276">hello new credential appears in hello list in hello **Manage Credentials** dialog box.</span></span>
    
    ![Okno dialogowe poświadczenia zarządzania serwera kopii zapasowej systemu Azure](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. <span data-ttu-id="98a93-278">Witaj tooclose **poświadczenia zarządzania** okna dialogowego kliknij hello **X** w prawym górnym rogu hello.</span><span class="sxs-lookup"><span data-stu-id="98a93-278">tooclose hello **Manage Credentials** dialog box, click hello **X** in hello upper-right corner.</span></span>


## <a name="add-hello-vcenter-server-tooazure-backup-server"></a><span data-ttu-id="98a93-279">Dodaj hello vCenter Server tooAzure kopii zapasowej serwera</span><span class="sxs-lookup"><span data-stu-id="98a93-279">Add hello vCenter Server tooAzure Backup Server</span></span>

<span data-ttu-id="98a93-280">Kreator dodawania serwera produkcyjnego jest używane tooadd hello vCenter Server tooAzure Utwórz kopię zapasową serwera.</span><span class="sxs-lookup"><span data-stu-id="98a93-280">Production Server Addition Wizard is used tooadd hello vCenter Server tooAzure Backup Server.</span></span>

<span data-ttu-id="98a93-281">tooopen Kreator dodawania serwera produkcji, pełną hello następujące procedury:</span><span class="sxs-lookup"><span data-stu-id="98a93-281">tooopen Production Server Addition Wizard, complete hello following procedure:</span></span>

1. <span data-ttu-id="98a93-282">W konsoli serwera usługi Kopia zapasowa Azure powitania kliknij **zarządzania**, kliknij przycisk **serwerów produkcyjnych**, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="98a93-282">In hello Azure Backup Server console, click **Management**, click **Production Servers**, and then click **Add**.</span></span>

    ![Kreator dodawania serwera Otwórz produkcji](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    <span data-ttu-id="98a93-284">Witaj **Kreator dodawania serwera produkcyjnego** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="98a93-284">hello **Production Server Addition Wizard** dialog box appears.</span></span>

    ![Kreator dodawania serwera produkcyjnego](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. <span data-ttu-id="98a93-286">Na powitania **typu wybierz serwer produkcyjny** wybierz **serwerów VMware**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="98a93-286">On hello **Select Production Server type** page, select **VMware Servers**, and then click **Next**.</span></span>

3. <span data-ttu-id="98a93-287">W **adres IP/nazwa serwera**, określ hello pełną nazwę domeny (FQDN) lub adres IP serwera VMware hello.</span><span class="sxs-lookup"><span data-stu-id="98a93-287">In **Server Name/IP Address**, specify hello fully qualified domain name (FQDN) or IP address of hello VMware server.</span></span> <span data-ttu-id="98a93-288">Jeśli wszystkie serwery ESXi hello są zarządzane przez hello sam program vCenter, można użyć nazwy vCenter hello.</span><span class="sxs-lookup"><span data-stu-id="98a93-288">If all hello ESXi servers are managed by hello same vCenter, you can use hello vCenter name.</span></span>

    ![Określ adres FQDN lub adres IP serwera VMware](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. <span data-ttu-id="98a93-290">W **SSL Port**, wprowadź port hello toocommunicate używane z serwerem VMware hello.</span><span class="sxs-lookup"><span data-stu-id="98a93-290">In **SSL Port**, enter hello port that is used toocommunicate with hello VMware server.</span></span> <span data-ttu-id="98a93-291">Korzysta z portu 443, czyli hello domyślny port, jeśli nie wiadomo, że inny port jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="98a93-291">Use port 443, which is hello default port, unless you know that a different port is required.</span></span>

5. <span data-ttu-id="98a93-292">W **Określ poświadczenia**, wybierz hello poświadczeń, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="98a93-292">In **Specify Credential**, select hello credential that you created earlier.</span></span>

    ![Określ poświadczenia](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. <span data-ttu-id="98a93-294">Kliknij przycisk **Dodaj** tooadd hello VMware toohello listy serwerów **dodane serwery VMware**, a następnie kliknij przycisk **dalej** toomove toohello następnej strony kreatora hello.</span><span class="sxs-lookup"><span data-stu-id="98a93-294">Click **Add** tooadd hello VMware server toohello list of **Added VMware Servers**, and then click **Next** toomove toohello next page in hello wizard.</span></span>

    ![Dodawanie serwera VMWare i poświadczenia](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. <span data-ttu-id="98a93-296">W hello **Podsumowanie** kliknij przycisk **Dodaj** tooadd hello określony tooAzure serwera VMware Utwórz kopię zapasową serwera.</span><span class="sxs-lookup"><span data-stu-id="98a93-296">In hello **Summary** page, click **Add** tooadd hello specified VMware server tooAzure Backup Server.</span></span>

    ![Dodaj tooAzure serwera VMware kopii zapasowej serwera](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  <span data-ttu-id="98a93-298">Kopia zapasowa serwera VMware Hello jest bez agenta kopii zapasowej i natychmiast jest dodawany nowy serwer hello.</span><span class="sxs-lookup"><span data-stu-id="98a93-298">hello VMware server backup is an agentless backup, and hello new server is added immediately.</span></span> <span data-ttu-id="98a93-299">Witaj **Zakończ** strony pokazuje hello wyników.</span><span class="sxs-lookup"><span data-stu-id="98a93-299">hello **Finish** page shows you hello results.</span></span>

  ![Zakończ strony](./media/backup-azure-backup-server-vmware/summary-screen.png)

  <span data-ttu-id="98a93-301">tooadd wiele wystąpień programu vCenter Server tooAzure Utwórz kopię zapasową serwera hello Powtórz poprzednie kroki w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="98a93-301">tooadd multiple instances of vCenter Server tooAzure Backup Server, repeat hello previous steps in this section.</span></span>

<span data-ttu-id="98a93-302">Po dodaniu hello vCenter Server tooAzure Utwórz kopię zapasową serwera hello następnym krokiem jest toocreate grupy ochrony.</span><span class="sxs-lookup"><span data-stu-id="98a93-302">After you add hello vCenter Server tooAzure Backup Server, hello next step is toocreate a protection group.</span></span> <span data-ttu-id="98a93-303">grupy ochrony Hello określa hello różne szczegóły dotyczące krótki i długoterminowego przechowywania i gdzie Zdefiniuj i zastosowania zasad tworzenia kopii zapasowej hello jest.</span><span class="sxs-lookup"><span data-stu-id="98a93-303">hello protection group specifies hello various details for short or long-term retention, and it is where you define and apply hello backup policy.</span></span> <span data-ttu-id="98a93-304">zasady tworzenia kopii zapasowej Hello jest harmonogram hello gdy kopie zapasowe są wykonywane, i kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="98a93-304">hello backup policy is hello schedule for when backups occur, and what is backed up.</span></span>


## <a name="configure-a-protection-group"></a><span data-ttu-id="98a93-305">Skonfiguruj grupę ochrony</span><span class="sxs-lookup"><span data-stu-id="98a93-305">Configure a protection group</span></span>

<span data-ttu-id="98a93-306">Jeśli nie używasz programu System Center Data Protection Manager lub serwer kopii zapasowej Azure przed, zobacz [Planowanie kopii zapasowych na dyskach](https://technet.microsoft.com/library/hh758026.aspx) tooprepare środowiska sprzętowego.</span><span class="sxs-lookup"><span data-stu-id="98a93-306">If you have not used System Center Data Protection Manager or Azure Backup Server before, see [Plan for disk backups](https://technet.microsoft.com/library/hh758026.aspx) tooprepare your hardware environment.</span></span> <span data-ttu-id="98a93-307">Po sprawdzeniu, czy masz odpowiednie magazynu, należy użyć Kreatora tworzenia nowej grupy ochrony hello tooadd maszyny wirtualne VMware.</span><span class="sxs-lookup"><span data-stu-id="98a93-307">After you check that you have proper storage, use hello Create New Protection Group wizard tooadd VMware virtual machines.</span></span>

1. <span data-ttu-id="98a93-308">W konsoli serwera usługi Kopia zapasowa Azure powitania kliknij **ochrony**, a hello wstążce narzędzia, kliknij przycisk **nowy** Kreatora tworzenia nowej grupy ochrony hello tooopen.</span><span class="sxs-lookup"><span data-stu-id="98a93-308">In hello Azure Backup Server console, click **Protection**, and in hello tool ribbon, click **New** tooopen hello Create New Protection Group wizard.</span></span>

    ![Witaj Otwórz Kreatora tworzenia nowej grupy ochrony](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    <span data-ttu-id="98a93-310">Witaj **tworzenia nowej grupy ochrony** zostanie wyświetlone okno dialogowe Kreator.</span><span class="sxs-lookup"><span data-stu-id="98a93-310">hello **Create New Protection Group** wizard dialog box appears.</span></span>

    ![Okno dialogowe Kreator tworzenia nowej grupy ochrony](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    <span data-ttu-id="98a93-312">Kliknij przycisk **dalej** tooadvance toohello **wybierz typ grupy ochrony** strony.</span><span class="sxs-lookup"><span data-stu-id="98a93-312">Click **Next** tooadvance toohello **Select protection group type** page.</span></span>

2. <span data-ttu-id="98a93-313">Na powitania **typ grupy ochrony wybierz** wybierz **serwerów** , a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="98a93-313">On hello **Select Protection group type** page, select **Servers** and then click **Next**.</span></span> <span data-ttu-id="98a93-314">Witaj **Wybierz członków grupy** zostanie wyświetlona strona.</span><span class="sxs-lookup"><span data-stu-id="98a93-314">hello **Select group members** page appears.</span></span>

3. <span data-ttu-id="98a93-315">Na powitania **Wybierz członków grupy** strony, hello dostępnych elementów członkowskich i elementów członkowskich hello wybrane są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="98a93-315">On hello **Select group members** page, hello available members and hello selected members appear.</span></span> <span data-ttu-id="98a93-316">Wybierz członków hello mają tooprotect, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="98a93-316">Select hello members that you want tooprotect, and then click **Next**.</span></span>

    ![Wybierz członków grupy](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    <span data-ttu-id="98a93-318">Po wybraniu członka, w przypadku wybrania folderu zawierającego inne foldery lub maszyn wirtualnych, wybrane zostaną także te foldery i maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="98a93-318">When you select a member, if you select a folder that contains other folders or VMs, those folders and VMs are also selected.</span></span> <span data-ttu-id="98a93-319">Włączenie Hello hello folderów i maszyn wirtualnych w folderze nadrzędnym hello jest nazywany ochrony na poziomie folderu.</span><span class="sxs-lookup"><span data-stu-id="98a93-319">hello inclusion of hello folders and VMs in hello parent folder is called folder-level protection.</span></span> <span data-ttu-id="98a93-320">tooremove folder lub maszyny Wirtualnej, hello wyczyść pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="98a93-320">tooremove a folder or VM, clear hello check box.</span></span>

    <span data-ttu-id="98a93-321">Jeśli maszyny Wirtualnej lub folder zawierający maszyny Wirtualnej, jest już chronione tooAzure, nie możesz wybrać tej maszyny Wirtualnej ponownie.</span><span class="sxs-lookup"><span data-stu-id="98a93-321">If a VM, or a folder containing a VM, is already protected tooAzure, you cannot select that VM again.</span></span> <span data-ttu-id="98a93-322">Oznacza to po maszyny Wirtualnej jest tooAzure chronionych, nie można go chronić ponownie, która zapobiega utworzeniu dla jednej maszyny Wirtualnej przez punkty odzyskiwania zduplikowane.</span><span class="sxs-lookup"><span data-stu-id="98a93-322">That is, after a VM is protected tooAzure, it cannot be protected again, which prevents duplicate recovery points from being created for one VM.</span></span> <span data-ttu-id="98a93-323">Jeśli chcesz toosee, którego wystąpienia serwera usługi Kopia zapasowa Azure chroni już elementu członkowskiego, punkt toohello nazwa elementu członkowskiego toosee hello hello chroni serwer.</span><span class="sxs-lookup"><span data-stu-id="98a93-323">If you want toosee which Azure Backup Server instance already protects a member, point toohello member toosee hello name of hello protecting server.</span></span>

4. <span data-ttu-id="98a93-324">Na powitania **wybierz metodę ochrony danych** strony, wprowadź nazwę grupy ochrony hello.</span><span class="sxs-lookup"><span data-stu-id="98a93-324">On hello **Select Data Protection Method** page, enter a name for hello protection group.</span></span> <span data-ttu-id="98a93-325">Wybrano krótkoterminowej ochrony (toodisk) i ochrony w trybie online.</span><span class="sxs-lookup"><span data-stu-id="98a93-325">Short-term protection (toodisk) and online protection are selected.</span></span> <span data-ttu-id="98a93-326">Jeśli chcesz toouse ochrony w trybie online (tooAzure), należy użyć krótkoterminowej ochrony toodisk.</span><span class="sxs-lookup"><span data-stu-id="98a93-326">If you want toouse online protection (tooAzure), you must use short-term protection toodisk.</span></span> <span data-ttu-id="98a93-327">Kliknij przycisk **dalej** tooproceed toohello krótkoterminowej ochrony zakresu.</span><span class="sxs-lookup"><span data-stu-id="98a93-327">Click **Next** tooproceed toohello short-term protection range.</span></span>

    ![Wybierz metodę ochrony danych](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. <span data-ttu-id="98a93-329">Na powitania **Określ cele krótkoterminowe** strony, dla **zakres przechowywania**, określ hello liczbę dni, które mają punkty odzyskiwania tooretain, które są *przechowywane toodisk*.</span><span class="sxs-lookup"><span data-stu-id="98a93-329">On hello **Specify Short-Term Goals** page, for **Retention Range**, specify hello number of days that you want tooretain recovery points that are *stored toodisk*.</span></span> <span data-ttu-id="98a93-330">Toochange hello godziny i dni przy woluminów punktów odzyskiwania, kliknij przycisk **Modyfikuj**.</span><span class="sxs-lookup"><span data-stu-id="98a93-330">If you want toochange hello time and days when recovery points are taken, click **Modify**.</span></span> <span data-ttu-id="98a93-331">punkty odzyskiwania krótkoterminowego Hello są pełne kopie zapasowe.</span><span class="sxs-lookup"><span data-stu-id="98a93-331">hello short-term recovery points are full backups.</span></span> <span data-ttu-id="98a93-332">Nie są one przyrostowych kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="98a93-332">They are not incremental backups.</span></span> <span data-ttu-id="98a93-333">Po zakończeniu krótkoterminowych celów w zakresie powitania kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="98a93-333">When you are satisfied with hello short-term goals, click **Next**.</span></span>

    ![Określanie celów krótkoterminowych](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. <span data-ttu-id="98a93-335">Na powitania **Przejrzyj przydział dysku** Przejrzyj i w razie potrzeby zmodyfikuj hello miejsca na dysku dla hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="98a93-335">On hello **Review Disk Allocation** page, review and if necessary, modify hello disk space for hello VMs.</span></span> <span data-ttu-id="98a93-336">Witaj zalecane przydziały dysku są oparte na powitania zakres przechowywania, określonego w hello **Określ cele krótkoterminowe** strony, hello typu obciążenia i rozmiaru hello hello chronionych danych (określoną w kroku 3).</span><span class="sxs-lookup"><span data-stu-id="98a93-336">hello recommended disk allocations are based on hello retention range that is specified in hello **Specify Short-Term Goals** page, hello type of workload, and hello size of hello protected data (identified in step 3).</span></span>  

  - <span data-ttu-id="98a93-337">**Rozmiar danych:** rozmiar hello danych w grupie ochrony hello.</span><span class="sxs-lookup"><span data-stu-id="98a93-337">**Data size:** Size of hello data in hello protection group.</span></span>
  - <span data-ttu-id="98a93-338">**Miejsce na dysku:** hello zalecana ilość miejsca na dysku dla grupy ochrony hello.</span><span class="sxs-lookup"><span data-stu-id="98a93-338">**Disk space:** hello recommended amount of disk space for hello protection group.</span></span> <span data-ttu-id="98a93-339">Jeśli chcesz toomodify to ustawienie, należy przydzielić całkowita ilość miejsca nieznacznie przekraczającą kwota hello oceniasz, że rozwoju każdego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="98a93-339">If you want toomodify this setting, you should allocate total space that is slightly larger than hello amount that you estimate each data source grows.</span></span>
  - <span data-ttu-id="98a93-340">**Przekazywanie danych do wspólnej lokalizacji:** po włączeniu kolokacji wiele źródeł danych w hello ochrony można mapować tooa pojedynczą replikę i wolumin punktu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="98a93-340">**Colocate data:** If you turn on colocation, multiple data sources in hello protection can map tooa single replica and recovery point volume.</span></span> <span data-ttu-id="98a93-341">Kolokacja nie jest obsługiwana dla wszystkich obciążeń.</span><span class="sxs-lookup"><span data-stu-id="98a93-341">Colocation isn't supported for all workloads.</span></span>
  - <span data-ttu-id="98a93-342">**Automatycznie rozszerzaj:** po włączeniu tego ustawienia, jeśli dane w grupie hello chronione przekroczy początkową alokacji hello, System Center Data Protection Manager próbuje rozmiar dysku hello tooincrease o 25 procent.</span><span class="sxs-lookup"><span data-stu-id="98a93-342">**Automatically grow:** If you turn on this setting, if data in hello protected group outgrows hello initial allocation, System Center Data Protection Manager tries tooincrease hello disk size by 25 percent.</span></span>
  - <span data-ttu-id="98a93-343">**Szczegóły puli magazynu:** pokazuje stan hello hello puli magazynu, tym całkowity rozmiar dysku i wolnego.</span><span class="sxs-lookup"><span data-stu-id="98a93-343">**Storage pool details:** Shows hello status of hello storage pool, including total and remaining disk size.</span></span>

    ![Przejrzyj przydział dysku](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    <span data-ttu-id="98a93-345">Po zakończeniu przydzielenie miejsca na powitania kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="98a93-345">When you are satisfied with hello space allocation, click **Next**.</span></span>

7. <span data-ttu-id="98a93-346">Na powitania **wybierz metodę tworzenia repliki** strony, należy określić sposób kopii początkowej hello toogenerate lub replika hello chronionych danych na serwerze kopii zapasowej Azure.</span><span class="sxs-lookup"><span data-stu-id="98a93-346">On hello **Choose Replica Creation Method** page, specify how you want toogenerate hello initial copy, or replica, of hello protected data on Azure Backup Server.</span></span>

    <span data-ttu-id="98a93-347">Domyślnie Hello **automatycznie przez sieć hello** i **teraz**.</span><span class="sxs-lookup"><span data-stu-id="98a93-347">hello default is **Automatically over hello network** and **Now**.</span></span> <span data-ttu-id="98a93-348">Jeśli używasz domyślnego hello, zaleca się określenie poza godzinami szczytu.</span><span class="sxs-lookup"><span data-stu-id="98a93-348">If you use hello default, we recommend that you specify an off-peak time.</span></span> <span data-ttu-id="98a93-349">Wybierz **później** i określ dzień i godzinę.</span><span class="sxs-lookup"><span data-stu-id="98a93-349">Choose **Later** and specify a day and time.</span></span>

    <span data-ttu-id="98a93-350">Dla dużych ilości danych lub mniej niż optymalnych warunkach sieci należy wziąć pod uwagę replikację danych hello w trybie offline przy użyciu nośnika wymiennego.</span><span class="sxs-lookup"><span data-stu-id="98a93-350">For large amounts of data or less-than-optimal network conditions, consider replicating hello data offline by using removable media.</span></span>

    <span data-ttu-id="98a93-351">Po dokonaniu wybrane opcje, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="98a93-351">After you have made your choices, click **Next**.</span></span>

    ![Wybierz metodę tworzenia repliki](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. <span data-ttu-id="98a93-353">Na powitania **opcje sprawdzania spójności** wybierz, jak i kiedy sprawdzania spójności hello tooautomate.</span><span class="sxs-lookup"><span data-stu-id="98a93-353">On hello **Consistency Check Options** page, select how and when tooautomate hello consistency checks.</span></span> <span data-ttu-id="98a93-354">Można uruchomić sprawdzania spójności, gdy dane są niespójne, lub zgodnie z ustalonym harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="98a93-354">You can run consistency checks when replica data becomes inconsistent, or on a set schedule.</span></span>

    <span data-ttu-id="98a93-355">Jeśli nie chcesz, aby sprawdzanie spójności automatyczne tooconfigure, można uruchomić sprawdzanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="98a93-355">If you don't want tooconfigure automatic consistency checks, you can run a manual check.</span></span> <span data-ttu-id="98a93-356">W obszarze ochrony hello hello Azure Utwórz kopię zapasową serwera konsoli, kliknij prawym przyciskiem myszy hello grupy ochrony, a następnie wybierz **Przeprowadź Sprawdzanie spójności**.</span><span class="sxs-lookup"><span data-stu-id="98a93-356">In hello protection area of hello Azure Backup Server console, right-click hello protection group and then select **Perform Consistency Check**.</span></span>

    <span data-ttu-id="98a93-357">Kliknij przycisk **dalej** toomove toohello następnej strony.</span><span class="sxs-lookup"><span data-stu-id="98a93-357">Click **Next** toomove toohello next page.</span></span>

9. <span data-ttu-id="98a93-358">Na powitania **Określ dane chronione Online** wybierz co najmniej jedno źródło danych, które mają tooprotect.</span><span class="sxs-lookup"><span data-stu-id="98a93-358">On hello **Specify Online Protection Data** page, select one or more data sources that you want tooprotect.</span></span> <span data-ttu-id="98a93-359">Wybierz członków hello indywidualnie lub kliknij przycisk **Zaznacz wszystko** toochoose wszystkie elementy członkowskie.</span><span class="sxs-lookup"><span data-stu-id="98a93-359">You can select hello members individually, or click **Select All** toochoose all members.</span></span> <span data-ttu-id="98a93-360">Po wybraniu hello członków, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="98a93-360">After you choose hello members, click **Next**.</span></span>

    ![Określ dane chronione w trybie online](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. <span data-ttu-id="98a93-362">Na powitania **określić harmonogram tworzenia kopii zapasowych Online** określ punkty odzyskiwania toogenerate harmonogram hello z hello kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="98a93-362">On hello **Specify Online Backup Schedule** page, specify hello schedule toogenerate recovery points from hello disk backup.</span></span> <span data-ttu-id="98a93-363">Po wygenerowaniu hello punkt odzyskiwania, jest magazyn usług odzyskiwania toohello przeniesione na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="98a93-363">After hello recovery point is generated, it is transferred toohello Recovery Services vault in Azure.</span></span> <span data-ttu-id="98a93-364">Po zakończeniu hello harmonogram tworzenia kopii zapasowej online, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="98a93-364">When you are satisfied with hello online backup schedule, click **Next**.</span></span>

    ![Określ harmonogram tworzenia kopii zapasowej online](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. <span data-ttu-id="98a93-366">Na powitania **Określanie zasad przechowywania Online** wskaż, jak długo mają tooretain hello kopii zapasowej danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="98a93-366">On hello **Specify Online Retention Policy** page, indicate how long you want tooretain hello backup data in Azure.</span></span> <span data-ttu-id="98a93-367">Po zdefiniowaniu zasad powitania kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="98a93-367">After hello policy is defined, click **Next**.</span></span>

    ![Określ zasady przechowywania danych online](./media/backup-azure-backup-server-vmware/retention-policy.png)

    <span data-ttu-id="98a93-369">Nie ma żadnego limitu czasu na jak długo dane można zachować na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="98a93-369">There is no time limit for how long you can keep data in Azure.</span></span> <span data-ttu-id="98a93-370">Gdy dane punktu odzyskiwania są przechowywane na platformie Azure, hello tylko limit wynosi że nie może mieć więcej niż 9999 punkty odzyskiwania dla każdego chronionego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="98a93-370">When you store recovery point data in Azure, hello only limit is that you cannot have more than 9999 recovery points per protected instance.</span></span> <span data-ttu-id="98a93-371">W tym przykładzie wystąpienie chronionych hello jest powitania serwera VMware.</span><span class="sxs-lookup"><span data-stu-id="98a93-371">In this example, hello protected instance is hello VMware server.</span></span>

12. <span data-ttu-id="98a93-372">Na powitania **Podsumowanie** , przejrzyj szczegóły powitania dla członków grupy ochrony i ustawienia, a następnie kliknij przycisk **Utwórz grupę**.</span><span class="sxs-lookup"><span data-stu-id="98a93-372">On hello **Summary** page, review hello details for your protection group members and settings, and then click **Create Group**.</span></span>

    ![Członka grupy ochrony i ustawienia — podsumowanie](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a><span data-ttu-id="98a93-374">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="98a93-374">Next steps</span></span>
<span data-ttu-id="98a93-375">Jeśli używasz serwera usługi Kopia zapasowa Azure tooprotect VMware obciążeń, może Cię zainteresować przy użyciu serwera kopii zapasowej Azure chronić toohelp [programu Microsoft Exchange server](./backup-azure-exchange-mabs.md), [farmy Microsoft SharePoint](./backup-azure-backup-sharepoint-mabs.md), lub [Bazy danych programu SQL Server](./backup-azure-sql-mabs.md).</span><span class="sxs-lookup"><span data-stu-id="98a93-375">If you use Azure Backup Server tooprotect VMware workloads, you may be interested in using Azure Backup Server toohelp protect a [Microsoft Exchange server](./backup-azure-exchange-mabs.md), a [Microsoft SharePoint farm](./backup-azure-backup-sharepoint-mabs.md), or a [SQL Server database](./backup-azure-sql-mabs.md).</span></span>

<span data-ttu-id="98a93-376">Informacji dotyczących problemów z rejestrowaniem hello agenta, konfigurowania grupy ochrony hello lub tworzenie kopii zapasowych zadań, zobacz [Rozwiązywanie problemów z serwera usługi Kopia zapasowa Azure](./backup-azure-mabs-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="98a93-376">For information on problems with registering hello agent, configuring hello protection group, or backing up jobs, see [Troubleshoot Azure Backup Server](./backup-azure-mabs-troubleshoot.md).</span></span>
