---
title: aaaCreate i przekazywanie wirtualna FreeBSD obrazu | Dokumentacja firmy Microsoft
description: "Dowiedz się toocreate i przekazywanie wirtualnego dysku twardego (VHD) zawierający hello FreeBSD systemu operacyjnego toocreate maszyny wirtualnej platformy Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kyliel
ms.openlocfilehash: f3bd155e496f1a2713d36bb66ea9824ed4c210ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-freebsd-vhd-tooazure"></a>Tworzenie i przekazywanie tooAzure FreeBSD wirtualnego dysku twardego
W tym artykule opisano, jak toocreate i przekazywanie wirtualnego dysku twardego (VHD) zawierający hello FreeBSD systemu operacyjnego. Po wysłaniu, można użyć jej jako toocreate własny obraz maszyny wirtualnej (VM) na platformie Azure.

> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Aby dowiedzieć się, jak przekazywanie wirtualnego dysku twardego za pomocą modelu Resource Manager hello, zobacz [tutaj](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="prerequisites"></a>Wymagania wstępne
W tym artykule założono, że hello następujące elementy:

* **Subskrypcja platformy Azure**— Jeśli nie masz konta, możesz utworzyć jedną w zaledwie kilka minut. Jeśli masz subskrypcję MSDN, zobacz [Azure miesięczne środki dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/). W przeciwnym razie Dowiedz się, jak za[utworzyć bezpłatne konto próbne](https://azure.microsoft.com/pricing/free-trial/).  
* **Narzędzia programu PowerShell Azure**--modułu Azure PowerShell hello musi być zainstalowana i skonfigurowana toouse subskrypcji platformy Azure. Moduł hello toodownload, zobacz [Azure pobiera](https://azure.microsoft.com/downloads/). Samouczek, który opisuje sposób tooinstall i skonfigurować moduł hello jest dostępnych tutaj. Użyj hello [Azure pobiera](https://azure.microsoft.com/downloads/) polecenia cmdlet tooupload hello wirtualnego dysku twardego.
* **FreeBSD zainstalowanego systemu operacyjnego w pliku VHD**--obsługiwany system operacyjny FreeBSD musi być zainstalowany tooa wirtualnego dysku twardego. Wiele narzędzi istnieje toocreate pliki VHD. Można na przykład, takich jak plik VHD hello toocreate funkcji Hyper-V za pomocą rozwiązania wirtualizacji i zainstaluj system operacyjny hello. Aby uzyskać instrukcje dotyczące sposobu tooinstall i użyj funkcji Hyper-V, zobacz [Instalowanie funkcji Hyper-V i tworzenie maszyny wirtualnej](http://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Witaj nowszy format VHDX nie jest obsługiwane na platformie Azure. Można przekonwertować format tooVHD dysku hello przy użyciu Menedżera funkcji Hyper-V lub polecenia cmdlet hello [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx). Ponadto istnieje [samouczek w witrynie MSDN temat toouse FreeBSD z funkcją Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).
>
>

To zadanie obejmuje następujące kroki pięć hello:

## <a name="step-1-prepare-hello-image-for-upload"></a>Krok 1: Przygotowanie obrazu hello przekazywania
Na maszynie wirtualnej hello, w którym zainstalowano system operacyjny FreeBSD hello wykonaj hello następujące procedury:

1. Włącz protokół DHCP.

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. Włącz SSH.

    Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu. Domyślnie jest włączone po instalacji z dysku FreeBSD. 
3. Konfigurowanie konsoli szeregowej.

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. Zainstaluj plik sudo.

    konta głównego Hello jest wyłączona w systemie Azure. Oznacza to, że należy tooutilize sudo z poleceniami toorun nieuprawnionego użytkownika z podniesionymi uprawnieniami.

        # pkg install sudo
   
5. Wymagania wstępne dotyczące agenta platformy Azure.

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. Zainstaluj agenta platformy Azure.

    Witaj najnowszej wersji hello Azure agenta zawsze można znaleźć w [github](https://github.com/Azure/WALinuxAgent/releases). Witaj wersji 2.0.10 + oficjalnie obsługuje FreeBSD 10 & 10.1 i wersji hello 2.1.4 + (w tym 2.2.x) oficjalnie obsługuje FreeBSD 10.2 i jego nowszych wersjach.

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    2.0 Użyjmy 2.0.16 na przykład:

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    2.1 możemy użyć 2.1.4 na przykład:

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > Po zainstalowaniu agenta platformy Azure jest tooverify dobrym rozwiązaniem, czy działa:
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. Anulowanie zastrzeżenia hello systemu.

    Deprovision hello tooclean systemu go i udostępnić go odpowiednie dla reprovisioning. Witaj następujące polecenie spowoduje również usunięcie hello ostatnie konto użytkownika elastycznie i hello skojarzone dane:

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    Teraz można zamknąć maszyny Wirtualnej.

## <a name="step-2-create-a-storage-account-in-azure"></a>Krok 2: Utwórz konto magazynu na platformie Azure
Należy korzystać z konta magazynu w Azure tooupload pliku VHD, może być używane toocreate maszyny wirtualnej. Możesz użyć hello klasycznego portalu Azure toocreate konta magazynu.

1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Na pasku poleceń hello, wybierz **nowy**.
3. Wybierz **usług danych** > **magazynu** > **szybkie tworzenie**.

    ![Szybkie tworzenie konta magazynu](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. Wypełnij pola hello w następujący sposób:

   * W hello **adres URL** wpisz adres URL konta magazynu hello toouse nazwę domeny podrzędnej. wpis Hello może zawierać od 3 do 24 cyfry i małe litery. Ta nazwa staje się nazwa hosta hello w hello adresu URL magazynu obiektów Blob platformy Azure używana tooaddress, magazynu kolejek Azure lub zasobów magazynu tabel Azure hello subskrypcji.
   * W hello **grupa lokalizacji/koligacji** menu rozwijanego wybierz hello **lokalizacja lub grupa koligacji** dla konta magazynu hello. Grupa koligacji pozwala umieścić usługi w chmurze i magazynu w hello tym samym centrum danych.
   * W hello **replikacji** określ czy toouse **geograficznie nadmiarowego** replikacji dla konta magazynu hello. Replikacja geograficzna jest domyślnie włączona. Ta opcja replikuje Twoje dane tooa dodatkowej lokalizacji, nie tooyou kosztów, tak, aby Magazyn awaryjnie toothat lokalizacji, jeżeli poważnej awarii występuje w lokalizacji głównej hello. Lokalizacja dodatkowej Hello jest przypisywany automatycznie i nie można zmienić. Jeśli potrzebujesz większej kontroli nad hello lokalizacji magazynu oparte na chmurze wymagania toolegal lub zasady organizacji, można wyłączyć replikacji geograficznej. Należy jednak pamiętać, że jeśli później włączyć replikację geograficzną zostanie naliczona jednorazowego transferu danych opłata tooreplicate Twojego istniejącej lokalizacji dodatkowej toohello danych. Usługi magazynu bez — replikacja geograficzna jest oferowany z rabatem. Więcej informacji o zarządzaniu — replikacja geograficzna kont magazynu można znaleźć tutaj: [replikacja usługi Azure Storage](../../../storage/common/storage-redundancy.md).

     ![Wprowadź szczegóły konta magazynu](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. Wybierz **utworzyć konto magazynu**. Witaj konto zostanie wyświetlone w obszarze **magazynu**.

    ![Pomyślnie utworzono konto magazynu](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. Następnie należy utworzyć kontener dla plików VHD przekazane. Wybierz nazwę konta magazynu hello, a następnie wybierz **kontenery**.

    ![Szczegóły konta magazynu](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. Wybierz **utworzyć kontener**.

    ![Szczegóły konta magazynu](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. W hello **nazwa** wpisz nazwę użytkownika kontenera. Następnie w hello **dostępu** menu rozwijanego, wybierz typ zasad dostępu ma.

    ![Nazwa kontenera](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > Domyślnie hello kontener jest prywatny i jest dostępny tylko przez właściciela konta hello. tooallow publiczny dostęp do odczytu toohello BLOB w kontenerach hello, ale nie toohello właściwości kontenera i metadanych, użyj hello **publicznego obiektu Blob** opcji. tooallow publicznego pełny dostęp do odczytu dla hello kontenera i obiektów blob, użyj hello **publicznego kontenera** opcji.
   >
   >

## <a name="step-3-prepare-hello-connection-tooazure"></a>Krok 3: Przygotowanie hello tooAzure połączenia
Zanim można przekazać pliku VHD, należy tooestablish bezpiecznego połączenia między komputerem i Twojej subskrypcji platformy Azure. Możesz użyć hello Azure Active Directory (Azure AD) metoda lub hello toodo metody certyfikatu go.

### <a name="use-hello-azure-ad-method-tooupload-a-vhd-file"></a>Użyj hello Azure AD — metoda tooupload pliku VHD
1. Hello Otwórz konsolę programu Azure PowerShell.
2. Wpisz następujące polecenie hello:  
    `Add-AzureAccount`

    To polecenie powoduje otwarcie okna logowania której możesz zalogować się przy użyciu konta służbowego.

    ![Okno programu PowerShell](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. Azure uwierzytelnia i zapisanie informacji o poświadczeniach hello. Następnie zamyka okno hello.

### <a name="use-hello-certificate-method-tooupload-a-vhd-file"></a>Użyj hello certyfikatu metody tooupload pliku VHD
1. Hello Otwórz konsolę programu Azure PowerShell.
2. Typ: `Get-AzurePublishSettingsFile`.
3. Oknie przeglądarki zostanie otwarty i wyświetla monit o możesz toodownload hello .publishsettings pliku. Ten plik zawiera informacje i certyfikatu dla Twojej subskrypcji platformy Azure.

    ![Strona pobierania przeglądarki](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. Zapisz plik .publishsettings hello.
5. Typ: `Import-AzurePublishSettingsFile <PathToFile>`, gdzie `<PathToFile>` jest hello pełną ścieżkę toohello .publishsettings pliku.

   Aby uzyskać więcej informacji, zobacz [wprowadzenie do poleceń cmdlet systemu Azure](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).

   Aby uzyskać więcej informacji na temat instalowania i konfigurowania programu PowerShell, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

## <a name="step-4-upload-hello-vhd-file"></a>Krok 4: Przekaż plik VHD hello
Podczas przekazywania pliku VHD hello, możesz go umieścić w dowolnym w ramach usługi magazynu obiektów Blob. Poniżej przedstawiono niektóre warunki, które będą używane podczas przekazywania pliku hello:

* **BlobStorageURL** jest adres URL hello hello konta magazynu, który został utworzony w kroku 2.
* **YourImagesFolder** jest hello kontenera w magazynie obiektów Blob w miejscu toostore obrazów.
* **VHDName** jest etykietę hello, pojawiającą hello Azure classic portal tooidentify hello wirtualnym dysku twardym.
* **PathToVHDFile** jest hello Pełna ścieżka i nazwa pliku VHD hello.

Okno programu Azure PowerShell hello używanego w poprzednim kroku hello wpisz:

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-hello-uploaded-vhd-file"></a>Krok 5: Tworzenie maszyny Wirtualnej z pliku VHD przekazane hello
Po przekazaniu pliku VHD hello, należy dodać go jako listy obrazów toohello niestandardowych obrazów, które są skojarzone z subskrypcją i Utwórz maszynę wirtualną z tego obrazu niestandardowego.

1. Okno programu Azure PowerShell hello używanego w poprzednim kroku hello wpisz:

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of hello VHD> -OS <Type of hello OS on hello VHD>

   > [!NOTE]
   > Użyj systemu Linux jako hello typ systemu operacyjnego. Bieżąca wersja programu Azure PowerShell Hello akceptuje tylko "Linux" lub "Windows" jako parametr.
   >
   >
2. Po wykonaniu poprzednich kroków hello nowy obraz powitania znajduje się po wybraniu hello **obrazów** kartę na powitania klasycznego portalu Azure.  

    ![Wybierz obraz](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. Utwórz maszynę wirtualną z galerii hello. Ten nowy obraz jest teraz dostępna w obszarze **Moje obrazy**.
4. Wybierz nowy obraz powitania. Następnie należy przejść przez tooset monity hello nazwy hosta, hasła, klucz SSH i tak dalej.

    ![Obraz niestandardowy](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. Po ukończeniu inicjowania obsługi administracyjnej hello, zobaczysz maszyny Wirtualnej FreeBSD działające na platformie Azure.

    ![Obraz FreeBSD na platformie azure](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
