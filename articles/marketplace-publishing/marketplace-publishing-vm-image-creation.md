---
title: aaaCreating obrazu maszyny wirtualnej dla hello Azure Marketplace | Dokumentacja firmy Microsoft
description: "Szczegółowe instrukcje dotyczące sposobu toocreate maszynę wirtualną obraz dla hello Azure Marketplace innym toopurchase."
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5c937b8e-e28d-4007-9fef-624046bca2ae
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio; v-divte
ms.openlocfilehash: 65e1c0530bb050fb379a52544e36c55faacd84df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-virtual-machine-image-for-hello-azure-marketplace"></a>Przewodnik toocreate obrazu maszyny wirtualnej dla hello Azure Marketplace
W tym artykule **krok 2**, przeprowadzi Cię przez przygotowanie hello wirtualnych dysków twardych (VHD) wdroży toohello portalu Azure Marketplace. Dyski VHD są hello podstawę sieci jednostki SKU. Witaj proces jest różny w zależności od tego, czy udostępniasz SKU opartych na systemie Linux lub z systemem Windows. W tym artykule przedstawiono oba scenariusze. Ten proces można przeprowadzić równolegle z [o tworzeniu konta i rejestracji][link-acct-creation].

## <a name="1-define-offers-and-skus"></a>1. Zdefiniuj oferty i jednostki SKU
W tej sekcji dowiesz się toodefine hello oferty i ich skojarzonych jednostki SKU.

Oferta jest tooall "elementu nadrzędnego", z jego jednostki SKU. Można określić wiele ofert. Jak określić toostructure oferty działa tooyou. Gdy oferta zostanie przeniesiona toostaging, spoczywa oraz wszystkie jego jednostki SKU. Zastanów się uważnie z identyfikatorów jednostki SKU, ponieważ będą one widoczne w adresie URL hello:

* Witryny Azure.com: http://azure.microsoft.com/marketplace/partners/ {PartnerNamespace} / {OfferIdentifier}-{SKUidentifier}
* Portal Azure w wersji zapoznawczej: https://portal.azure.com/#gallery/ {PublisherNamespace}. {OfferIdentifier} {SKUIDdentifier}  

Jednostka SKU jest hello komercyjnych nazwę obrazu maszyny Wirtualnej. Obraz maszyny Wirtualnej zawiera jeden system operacyjny dysku oraz zero lub więcej dysków z danymi. Jest zasadniczo hello profilu pełną magazynu dla maszyny wirtualnej. Jeden wirtualny dysk twardy jest wymagany na dysku. Dyski danych nawet puste wymagają toobe wirtualnego dysku twardego, utworzony.

Niezależnie od systemu operacyjnego można użyć należy dodać tylko hello minimalna liczba dysków danych wymaganych przez hello jednostki SKU. Nie można usunąć dysków, które są częścią obrazu w czasie hello wdrożenia klientów, ale można dodać dysków podczas lub po wdrożeniu, jeśli to konieczne.

> [!IMPORTANT]
> **Nie należy zmieniać liczba dysków w nowej wersji obrazu.** Jeśli należy zmienić konfigurację dysków z danymi w obrazie hello, należy zdefiniować nowe jednostki SKU. Publikowania nowej wersji obrazu z liczbą inny dysk będzie miał potencjalnych hello złamanie nowe wdrożenie oparte na nowej wersji obraz powitania w przypadku wdrożeń automatyczne skalowanie, automatyczne rozwiązań za pomocą szablonów ARM i innych scenariuszy.
>
>

### <a name="11-add-an-offer"></a>1.1. Dodaj ofertę
1. Zaloguj się toohello [Portal publikowania] [ link-pubportal] przy użyciu konta sprzedaży.
2. Wybierz hello **maszyn wirtualnych** kartę hello Portal publikowania. W polu wpis zostanie wyświetlony monit o hello wprowadź nazwę oferty. Nazwa oferty Hello jest zwykle nazwa hello hello produktu lub usługi, czy planujesz toosell w hello Azure Marketplace.
3. Wybierz pozycję **Utwórz**.

### <a name="12-define-a-sku"></a>1.2 zdefiniować jednostki SKU
Po dodaniu oferty muszą toodefine i identyfikacji użytkownika jednostki SKU. Może mieć wielu ofert, a każdy oferta może mieć wiele jednostek SKU w nim. Gdy oferta zostanie przeniesiona toostaging, spoczywa oraz wszystkie jego jednostki SKU.

1. **Dodaj jednostki SKU.** Witaj SKU wymaga identyfikatora, który jest używany w adresie URL hello. Identyfikator Hello muszą być unikatowe w profilu publikowania, ale nie występuje ryzyko kolizji identyfikator z innych wydawców.

   > [!NOTE]
   > Oferta Hello i identyfikatory SKU są wyświetlane w adresie URL oferta hello w hello Marketplace.
   >
   >
2. **Dodaj opis podsumowujący dla Twojej wersji produktu.** Podsumowanie opisy są widoczne toocustomers, dlatego należy utworzyć je łatwo odczytać. Te informacje toobe zablokowany do momentu fazy "Wypychania tooStaging" hello nie jest konieczne. Do tego czasu są wolne tooedit go.
3. Jeśli używasz systemu Windows jednostki SKU, skorzystaj z linków sugerowane hello tooacquire hello zatwierdzone wersji systemu Windows Server.

## <a name="2-create-an-azure-compatible-vhd-linux-based"></a>2. Tworzenie wirtualnego dysku twardego zgodnego Azure (opartych na systemie Linux)
Ta sekcja dotyczy przede wszystkim najlepsze rozwiązania dotyczące tworzenia obrazu maszyny Wirtualnej opartych na systemie Linux dla hello Azure Marketplace. Przewodnik krok po kroku, można znaleźć w następującej dokumentacji toohello: [tworząc i przekazując wirtualny dysk twardy zawierający System operacyjny Linux hello](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="3-create-an-azure-compatible-vhd-windows-based"></a>3. Tworzenie wirtualnego dysku twardego zgodnego Azure (z systemem Windows)
W tej sekcji koncentruje się na powitania kroki toocreate SKU, oparte na systemie Windows Server dla hello Azure Marketplace.

### <a name="31-ensure-that-you-are-using-hello-correct-base-vhds"></a>3.1 Upewnij się, że używasz hello Popraw podstawowy wirtualne dyski twarde
system operacyjny Hello wirtualnego dysku twardego dla obrazu maszyny Wirtualnej musi być oparta na obrazu podstawową zatwierdzony Azure zawierającego systemu Windows Server lub SQL Server.

toobegin, utwórz maszynę Wirtualną z jednego z hello następujące obrazy znajdujące się na powitania [portalu Microsoft Azure][link-azure-portal]:

* Windows Server ([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 z dodatkiem SP1][link-datactr-2008-r2])
* Program SQL Server 2014 ([Enterprise][link-sql-2014-ent], [standardowe][link-sql-2014-std], [Web][link-sql-2014-web])
* SQL Server 2012 z dodatkiem SP2 ([Enterprise][link-sql-2012-ent], [standardowe][link-sql-2012-std], [Web][link-sql-2012-web])

Te linki znajdują się również w hello Portal publikowania w obszarze strony SKU hello.

> [!TIP]
> Jeśli używasz hello bieżącego portalu platformy Azure lub programu PowerShell są zatwierdzane obrazów systemu Windows Server, opublikowane w 8 września 2014 lub nowszy.
>
>

### <a name="32-create-your-windows-based-vm"></a>3.2 Tworzenie maszyny Wirtualnej z systemem Windows
W portalu Microsoft Azure hello można utworzyć maszyny Wirtualnej na podstawie zatwierdzonych obrazu podstawowego w kilku prostych krokach. Witaj poniżej przedstawiono omówienie procesu hello:

1. Ze strony podstawowy obraz powitania, wybierz **Utwórz maszynę wirtualną** toobe skierowane toohello nowe [portalu Microsoft Azure][link-azure-portal].

    ![Rysowanie][img-acom-1]
2. Zaloguj się w portalu toohello z hello konta Microsoft i hasło dla hello ma toouse subskrypcji platformy Azure.
3. Wykonaj hello monity toocreate Maszynę wirtualną za pomocą hello podstawowy obraz, który wybrano. Należy tooprovide nazwy hosta (nazwa komputera hello), nazwę użytkownika (zarejestrowane jako administrator) i hasło dla hello maszyny Wirtualnej.

    ![Rysowanie][img-portal-vm-create]
4. Wybierz rozmiar hello hello toodeploy maszyny Wirtualnej:

    a.    Jeśli planujesz toodevelop hello wirtualnego dysku twardego lokalnymi rozmiar hello nie ma znaczenia. Należy wziąć pod uwagę przy użyciu jednej z hello mniejszych maszyn wirtualnych.

    b.    Jeśli planujesz toodevelop hello obrazu na platformie Azure, należy rozważyć przy użyciu jednej z hello zalecane rozmiary maszyn wirtualnych dla hello wybranego obrazu.

    c.    Aby uzyskać informacje o cenach, zobacz toohello **zalecana warstwa cenowa** wyświetlane w portalu hello selektora. Będzie on zawierał hello trzy zalecane rozmiary podał hello wydawcy. (W tym przypadku wydawcy hello jest firmy Microsoft).

    ![Rysowanie][img-portal-vm-size]
5. Ustaw właściwości:

    a.    Do szybkiego wdrożenia, można pozostawić hello domyślne wartości dla właściwości hello w obszarze **konfiguracji opcjonalnej** i **grupy zasobów**.

    b.    W obszarze **konta magazynu**, opcjonalnie można wybrać hello konta magazynu, w którym hello systemu operacyjnego będą przechowywane wirtualnego dysku twardego.

    c.    W obszarze **grupy zasobów**, opcjonalnie można wybrać grupę logiczną hello, w których tooplace hello maszyny Wirtualnej.
6. Wybierz hello **lokalizacji** wdrożenia:

    a.    Jeśli planujesz toodevelop hello wirtualnego dysku twardego lokalnymi hello lokalizacji nie ma znaczenia, ponieważ spowoduje przekazanie tooAzure obrazu hello później.

    b.    Jeśli planujesz toodevelop hello obrazu na platformie Azure, należy rozważyć użycie regionów amerykańskiej Microsoft Azure powitania od początku hello. Przyspiesza hello wirtualnego dysku twardego procesu kopiowania wykonująca firmy Microsoft w imieniu użytkownika podczas przesyłania obrazu do certyfikacji.

    ![Rysowanie][img-portal-vm-location]
7. Kliknij przycisk **Utwórz**. Witaj maszyna wirtualna uruchamia toodeploy. W ciągu minut będzie miał pomyślne wdrożenie i rozpocząć obraz powitania toocreate Twojego jednostki SKU.

### <a name="33-develop-your-vhd-in-hello-cloud"></a>3.3 opracowanie dysk VHD w chmurze hello
Zdecydowanie zaleca się tworzenie dysk VHD w chmurze hello za pomocą protokołu RDP (Remote Desktop). TooRDP należy połączyć z hello nazwę użytkownika i hasło określone podczas inicjowania obsługi.

> [!IMPORTANT]
> W przypadku tworzenia dysk VHD lokalnymi (co nie jest zalecane), zobacz [Tworzenie obrazu maszyny wirtualnej z lokalnymi](marketplace-publishing-vm-image-creation-on-premise.md). Pobieranie dysk VHD nie jest konieczne, jeśli tworzysz hello chmury.
>
>

**Łączenie za pośrednictwem protokołu RDP za pomocą hello [portalu Microsoft Azure][link-azure-portal]**

1. Wybierz **Przeglądaj** > **maszyn wirtualnych**.
2. zostanie otwarty blok maszyn wirtualnych Hello. Upewnij się, że hello maszynę Wirtualną, która ma tooconnect z działa, a następnie wybierz z listy hello wdrożonych maszyn wirtualnych.
3. Otwiera bloku, które opisano hello zaznaczone maszyny Wirtualnej. U góry hello kliknij **Connect**.
4. Jesteś tooenter zostanie wyświetlony monit o hello użytkownika nazwę i hasło, które zostały określone podczas inicjowania obsługi administracyjnej.

**Łączenie za pośrednictwem protokołu RDP przy użyciu programu PowerShell**

toodownload komputera lokalnego tooa pliku pulpitu zdalnego, użyj hello [polecenia cmdlet Get-AzureRemoteDesktopFile][link-technet-2]. W kolejności toouse tego polecenia cmdlet, potrzebna nazwa hello tooknow hello usługi i nazwę hello maszyny Wirtualnej. Jeśli utworzono hello maszyny Wirtualnej z hello [portalu Microsoft Azure][link-azure-portal], można znaleźć te informacje w obszarze właściwości maszyny Wirtualnej:

1. W portalu Microsoft Azure hello, wybierz **Przeglądaj** > **maszyn wirtualnych**.
2. zostanie otwarty blok maszyn wirtualnych Hello. Wybierz hello maszyny Wirtualnej, która została wdrożona.
3. Otwiera bloku, które opisano hello zaznaczone maszyny Wirtualnej.
4. Kliknij pozycję **Właściwości**.
5. Pierwsza część nazwy domeny hello Hello jest hello nazwy usługi. Nazwa hosta Hello jest hello nazwę maszyny Wirtualnej.

    ![Rysowanie][img-portal-vm-rdp]
6. Hello polecenia cmdlet toodownload hello plik RDP dla pulpitu lokalnego administratora hello utworzona maszyna wirtualna toohello ma następującą składnię.

        Get‐AzureRemoteDesktopFile ‐ServiceName “baseimagevm‐6820cq00” ‐Name “BaseImageVM” –LocalPath “C:\Users\Administrator\Desktop\BaseImageVM.rdp”

Więcej informacji na temat protokołu RDP można znaleźć w witrynie MSDN w artykule hello [połączyć tooan maszyny Wirtualnej platformy Azure z protokołu RDP lub SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx).

**Skonfiguruj Maszynę wirtualną i Utwórz użytkownika jednostki SKU**

Po hello system operacyjny, który jest pobierany wirtualnego dysku twardego Użyj funkcji Hyper-v i skonfiguruj toobegin maszyny Wirtualnej, tworzenie użytkownika jednostki SKU. Szczegółowy opis kroków można znaleźć na powitania następującego łącza w witrynie TechNet: [Instalowanie funkcji Hyper-v i konfigurowanie maszyny Wirtualnej](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="34-choose-hello-correct-vhd-size"></a>3.4, wybierz odpowiedni rozmiar wirtualnego dysku twardego hello
system operacyjny Windows Hello wirtualnego dysku twardego w obrazie maszyny Wirtualnej należy utworzyć jako 128 GB stały format wirtualnego dysku twardego.  

Jeśli rozmiar fizycznej hello jest mniejsza niż 128 GB, powinna być rozrzedzony hello wirtualnego dysku twardego. Witaj podstawowej systemu Windows i program SQL Server obrazy podane już spełnia te wymagania, tak nie należy zmieniać rozmiar formatu lub hello hello hello uzyskane wirtualnego dysku twardego.  

Dyski danych może być większy niż 1 TB. Podczas podejmowania decyzji o hello rozmiaru dysku, należy pamiętać, że klientów nie można zmienić rozmiaru wirtualnych dysków twardych w obrębie obrazu w czasie hello wdrożenia. Wirtualne dyski twarde dysku danych należy utworzyć jako stały format wirtualnego dysku twardego. Powinny być również rozrzedzone. Dyski z danymi mogą zawierać dane lub mogą być puste.

### <a name="35-install-hello-latest-windows-patches"></a>3.5 zainstalować najnowsze poprawki systemu Windows hello
Witaj podstawowej obrazy zawierają hello najnowszych poprawek się tootheir Data opublikowania. Przed opublikowaniem systemu operacyjnego hello dysków VHD zostały utworzone, upewnij się, uruchomieniu usługi Windows Update, a wszystkie hello najnowsze krytyczne a zabezpieczeń ważne aktualizacje zostały zainstalowane.

### <a name="36-perform-additional-configuration-and-schedule-tasks-as-necessary"></a>3,6 wykonanie dodatkowych zadań konfiguracji i harmonogram, zgodnie z potrzebami
Jeśli potrzebne są dodatkowe czynności konfiguracyjne, należy rozważyć użycie zaplanowane zadanie, które jest uruchamiane w toomake uruchomienia wszelkich końcowych zmian toohello maszyny Wirtualnej po jej wdrożeniu:

* To zadanie hello toohave najlepsze praktyki usunąć po pomyślnym wykonaniu.
* Konfiguracja nie polegać na dyskach, niż dyski C lub D, ponieważ są one hello tylko dwie stacje, które są zawsze gwarantowane tooexist. Dysk C jest hello dysku systemu operacyjnego i dysku D jest hello tymczasowego dysku lokalnym.

### <a name="37-generalize-hello-image"></a>3.7 obraz powitania generalize
Wszystkie obrazy w portalu Azure Marketplace hello musi być wielokrotnego użytku w sposób ogólny. Innymi słowy musi być uogólniony systemu operacyjnego hello wirtualnego dysku twardego:

* W systemie Windows hello obraz powinien być "Sysprep" i nie ma żadnych konfiguracji ma się odbywać nieobsługujących hello **sysprep** polecenia.
* Możesz uruchomić następujące polecenie z hello katalogu % windir%\System32\Sysprep hello.

        sysprep.exe /generalize /oobe /shutdown

  Wskazówki dotyczące sposobu systemu operacyjnego hello toosysprep znajduje się w kroku hello następujących artykuł w witrynie MSDN: [tworzenie i przekazywanie wirtualnego dysku twardego z systemem Windows Server tooAzure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="4-deploy-a-vm-from-your-vhds"></a>4. Wdrożenie maszyny Wirtualnej z sieci wirtualnych dysków twardych
Po zostały przekazane z wirtualnych dysków twardych (systemu operacyjnego hello uogólniony wirtualny dysk twardy i zero lub więcej danych na dysku VHD) tooan kontem magazynu platformy Azure, można je zarejestrować jako obraz użytkownika maszyny Wirtualnej. Następnie można przetestować tego obrazu. Należy pamiętać, ponieważ uogólniony wirtualny dysk twardy systemu operacyjnego nie może bezpośrednio wdrożenie hello maszyny Wirtualnej przez zapewnienie hello adres URL dysku VHD.

toolearn więcej informacji na temat obrazów maszyn wirtualnych hello Przejrzyj następujące wpisy na blogu:

* [Obraz maszyny Wirtualnej](https://azure.microsoft.com/blog/vm-image-blog-post/)
* [Jak PowerShell obrazu maszyny Wirtualnej](https://azure.microsoft.com/blog/vm-image-powershell-how-to-blog-post/)
* [Informacje o obrazach maszyny Wirtualnej na platformie Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)

### <a name="set-up-hello-necessary-tools-powershell-and-azure-cli"></a>Konfigurowanie hello niezbędne narzędzia programu PowerShell i interfejsu wiersza polecenia Azure
* [Jak toosetup środowiska PowerShell](/powershell/azure/overview)
* [Jak toosetup wiersza polecenia platformy Azure](../cli-install-nodejs.md)

### <a name="41-create-a-user-vm-image"></a>4.1 tworzenia obrazu użytkownika maszyny Wirtualnej
#### <a name="capture-vm"></a>Przechwytywanie maszyny Wirtualnej
Przeczytaj hello łączy podanych poniżej w celu uzyskania wskazówek dotyczących Przechwytywanie hello maszyny Wirtualnej przy użyciu interfejsu wiersza polecenia Azure-API/programu PowerShell.

* [Interfejs API](https://msdn.microsoft.com/library/mt163560.aspx)
* [PowerShell](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Interfejs wiersza polecenia platformy Azure](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="generalize-image"></a>Obraz
Przeczytaj hello łączy podanych poniżej w celu uzyskania wskazówek dotyczących Przechwytywanie hello maszyny Wirtualnej przy użyciu interfejsu wiersza polecenia Azure-API/programu PowerShell.

* [Interfejs API](https://msdn.microsoft.com/library/mt269439.aspx)
* [PowerShell](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Interfejs wiersza polecenia platformy Azure](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="42-deploy-a-vm-from-a-user-vm-image"></a>4.2 wdrożyć maszynę Wirtualną z obrazu użytkownika maszyny Wirtualnej
toodeploy maszyny Wirtualnej z obrazu użytkownika maszyny Wirtualnej, można użyć bieżącej hello [portalu Azure](https://manage.windowsazure.com) lub programu PowerShell.

**Wdrażanie maszyny Wirtualnej z bieżącego portalu platformy Azure hello**

1. Przejdź za**nowy** > **obliczeniowe** > **maszyny wirtualnej** > **z galerii**.

    ![Rysowanie][img-manage-vm-new]
2. Przejdź za**Moje obrazy**, a następnie wybierz hello obrazu maszyny Wirtualnej, z których toodeploy maszyny Wirtualnej:

   1. Obraz toowhich szczególną uwagę płatności zostanie wybrana, ponieważ hello **Moje obrazy** widoku są wyszczególnione zarówno obrazy systemu operacyjnego i obrazy maszyny Wirtualnej.
   2. Spojrzenie na powitania liczba dysków może pomóc w określają wdrażasz rodzaju obrazu, ponieważ większość hello obrazów maszyn wirtualnych ma więcej niż jeden dysk. Jest jednak nadal możliwe toohave obraz maszyny Wirtualnej z tylko jednego systemu operacyjnego dysku, który będzie zmuszony **liczba dysków** ustawić too1.

      ![Rysowanie][img-manage-vm-select]
3. Postępuj zgodnie z Kreatora tworzenia maszyny Wirtualnej hello i określ nazwę maszyny Wirtualnej hello, rozmiar maszyny Wirtualnej, lokalizacji, nazwę użytkownika i hasło.

**Wdróż Maszynę wirtualną z programu PowerShell**

toodeploy dużych maszyny Wirtualnej z hello uogólniony obraz maszyny Wirtualnej właśnie utworzony, można użyć hello następującego polecenia cmdlet.

    $img = Get-AzureVMImage -ImageName "myVMImage"
    $user = "user123"
    $pass = "adminPassword123"
    $myVM = New-AzureVMConfig -Name "VMImageVM" -InstanceSize "Large" -ImageName $img.ImageName | Add-AzureProvisioningConfig -Windows -AdminUsername $user -Password $pass
    New-AzureVM -ServiceName "VMImageCloudService" -VMs $myVM -Location "West US" -WaitForBoot

> [!IMPORTANT]
> Aby uzyskać dodatkową pomoc, zapoznaj się z [Rozwiązywanie typowych problemów napotykanych podczas tworzenia dysku VHD].
>
>

## <a name="5-obtain-certification-for-your-vm-image"></a>5. Uzyskaj certyfikacji dla obrazu maszyny Wirtualnej
następnym krokiem Hello w celu przygotowania obrazu maszyny Wirtualnej do hello Azure Marketplace jest toohave, który go certyfikowane.

Proces ten obejmuje uruchomione narzędzie certyfikacji specjalne, przekazywanie toohello wyniki weryfikacji hello kontenera platformy Azure, w którym znajdują się dyski VHD, dodanie propozycją Definiowanie sieci jednostki SKU i przesyłanie maszyny Wirtualnej obrazów do certyfikacji.

### <a name="51-download-and-run-hello-certification-test-tool-for-azure-certified"></a>5.1 Pobierz i uruchom narzędzie Test certyfikacji hello do certyfikowanych Azure
Uruchamia narzędzie certyfikacji Hello na uruchomionej maszynie Wirtualnej z obrazu użytkownika maszyny Wirtualnej, tooensure, który hello obrazu maszyny Wirtualnej jest zgodna z Microsoft Azure. Zweryfikuje, że zostały spełnione hello wskazówki i wymagań dotyczących przygotowywania dysk VHD. Witaj dane wyjściowe narzędzia hello jest raport zgodności, które należy przesłać na powitania Portal publikowania podczas żądania certyfikacji.

Narzędzie certyfikacji Hello służy w systemach Windows i maszyn wirtualnych systemu Linux. Łączy z maszyn wirtualnych w tooWindows za pomocą programu PowerShell, a łączy maszyn wirtualnych tooLinux za pośrednictwem SSH.Net:

1. Po pierwsze, Pobierz narzędzie certyfikacji hello na powitania [witryny pobierania firmy Microsoft][link-msft-download].
2. Otwórz narzędzie certyfikacji hello, a następnie kliknij przycisk hello **uruchomienia nowego testu** przycisku.
3. Z hello **testowanie informacji** ekranu, wprowadź nazwę dla uruchomienia testu hello.
4. Wybierz system operacyjny maszyny wirtualnej (Linux lub Windows). W zależności od tego, która zostanie wybrana wybierz opcje kolejnych hello.

### <a name="connect-hello-certification-tool-tooa-linux-vm-image"></a>**Połącz tooa narzędzie certyfikacji hello obrazu maszyny Wirtualnej systemu Linux**
1. Tryb uwierzytelniania SSH wybierz hello: plik hasła lub klucza.
2. Jeśli przy użyciu uwierzytelniania opartego na hasłach, wprowadź hello nazwy systemu nazw domen (DNS, Domain Name System), nazwę użytkownika i hasło.
3. Jeśli przy użyciu pliku klucza uwierzytelniania, wprowadź hello nazwy DNS, nazwy użytkownika i lokalizacji klucza prywatnego.

   ![Uwierzytelnianie hasła z obrazu maszyny Wirtualnej systemu Linux][img-cert-vm-pswd-lnx]

   ![Plik klucza uwierzytelniania obrazu maszyny Wirtualnej systemu Linux][img-cert-vm-key-lnx]

### <a name="connect-hello-certification-tool-tooa-windows-based-vm-image"></a>**Połącz hello certyfikacji narzędzia tooa opartych na systemie Windows obrazu maszyny Wirtualnej**
1. Wprowadź hello w pełni kwalifikowana nazwa DNS maszyny Wirtualnej (na przykład MyVMName.Cloudapp.net).
2. Wprowadź hello nazwy użytkownika i hasła.

   ![Uwierzytelnianie hasła obrazu maszyny Wirtualnej systemu Windows][img-cert-vm-pswd-win]

Po wybraniu odpowiednich opcji hello zostały wybrane dla obrazu systemu Linux lub maszyny Wirtualnej z systemem Windows, wybierz **Testuj połączenie** tooensure czy SSH.Net lub programu PowerShell ma prawidłową połączenie do celów testowych. Po nawiązaniu połączenia wybierz **dalej** toostart hello testu.

Po zakończeniu testu hello otrzymasz hello wyników (przebiegu błąd/ostrzeżenie) dla każdego elementu testu.

![Przypadków testowych dla obrazu maszyny Wirtualnej systemu Linux][img-cert-vm-test-lnx]

![Przypadki testowe dla obrazu maszyny Wirtualnej systemu Windows][img-cert-vm-test-win]

Jeśli którykolwiek z testów hello zakończą się niepowodzeniem, obraz nie będzie certyfikat. W takim przypadku zapoznać się z wymaganiami hello i wprowadź wymagane zmiany.

Po hello automatycznego testu, zostanie wyświetlona prośba tooprovide dodatkowych danych wejściowych w obrazie maszyny Wirtualnej za pośrednictwem ekranu kwestionariusz.  Ukończyć powitalnych pytania, a następnie wybierz **dalej**.

![Kwestionariusz narzędzie certyfikacji][img-cert-vm-questionnaire]

![Kwestionariusz narzędzie certyfikacji][img-cert-vm-questionnaire-2]

Po wykonaniu kwestionariusz hello, możesz podać dodatkowe informacje, takie jak SSH dostęp do informacji o hello obrazu maszyny Wirtualnej systemu Linux i wyjaśnienie ocen nie powiodło się. Można pobrać wyników testu hello i pliki dziennika dla przypadków testowych hello wykonywane w dodanie tooyour odpowiedzi toohello kwestionariusz. Zapisz wyniki hello w hello tym samym kontenerze co dyski VHD.

![Zapisz certyfikacji wyników testu][img-cert-vm-results]

### <a name="52-get-hello-shared-access-signature-uri-for-your-vm-images"></a>5.2 pobrać sygnatury dostępu współdzielonego hello identyfikatora URI dla obrazów maszyny Wirtualnej
Podczas procesu publikowania hello możesz określić hello uniform resource identifier (URI) prowadzących tooeach hello wirtualne dyski twarde zostały utworzone dla Twojego jednostki SKU. Firma Microsoft będzie potrzebowała podczas procesu certyfikacji hello toothese dostępu do dysków VHD. W związku z tym należy toocreate identyfikator URI sygnatury dostępu współdzielonego dla każdego wirtualnego dysku twardego. Jest to hello identyfikator URI, który powinny być wprowadzane w **obrazów** kartę w hello Portal publikowania.

sygnatury dostępu współdzielonego Hello identyfikator URI utworzony przestrzegać toohello następujące wymagania:

* Podczas generowania sygnatury dostępu współdzielonego identyfikatorów URI dla dyski VHD, listy i Odczyt uprawnienia są wystarczające. Nie należy przydzielać uprawnień do zapisywania ani usuwania.
* czas trwania Hello dostęp powinien być co najmniej trzech (3) tygodni od, podczas tworzenia sygnatury dostępu współdzielonego hello identyfikatora URI.
* toosafeguard dla czasu UTC, wybierz hello dzień przed hello bieżącą datę. Na przykład jeśli hello jest data bieżąca 6 października 2014 r., wybierz 2014-10-5.

Adres URL SAS mogą być generowane w wielu tooshare sposoby dysk VHD do portalu Azure Marketplace.
Poniżej są hello 3 narzędzia zalecane:

1.  Eksplorator usługi Azure Storage
2.  Eksplorator usługi Storage firmy Microsoft
3.  Interfejs wiersza polecenia platformy Azure

**Eksplorator usługi Storage platformy Azure (zalecane w przypadku użytkowników systemu Windows)**

Poniżej przedstawiono kroki hello podczas generowania adresu URL SAS za pomocą Eksploratora usługi Storage platformy Azure

1. Pobierz [Explorer 6 magazynu Azure w wersji zapoznawczej 3](https://azurestorageexplorer.codeplex.com/) w witrynie CodePlex. Przejdź za[Podgląd 6 Eksploratora magazynu Azure](https://azurestorageexplorer.codeplex.com/) i kliknij przycisk **"Pobieranie"**.

    ![Rysowanie](media/marketplace-publishing-vm-image-creation/img5.2_01.png)

2. Pobierz [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668) i zainstalować po rozpakować go.

    ![Rysowanie](media/marketplace-publishing-vm-image-creation/img5.2_02.png)

3. Po zakończeniu instalacji, Otwórz aplikację hello.
4. Kliknij przycisk **Dodaj konto**.

    ![Rysowanie](media/marketplace-publishing-vm-image-creation/img5.2_03.png)

5. Określ nazwę konta magazynu hello, klucz konta magazynu i magazynu punkty końcowe domeny. To jest hello konta magazynu w ramach subskrypcji platformy Azure, gdzie dysk VHD mają być przechowywane w portalu Azure.

    ![Rysowanie](media/marketplace-publishing-vm-image-creation/img5.2_04.png)

6. Po połączeniu się Eksploratora usługi Storage Azure tooyour magazynu określonego konta, zostanie ona rozpoczęta przedstawiający zawiera wszystkie hello w ramach konta magazynu hello. Wybierz kontener hello został skopiowany plik VHD dysku systemu operacyjnego hello (także dysków danych, jeśli są one odpowiednie dla danego scenariusza).

    ![Rysowanie](media/marketplace-publishing-vm-image-creation/img5.2_05.png)

7. Po wybraniu hello kontenera obiektów blob, Eksploratora usługi Storage Azure rozpoczyna przedstawiający hello pliki w kontenerze hello. Wybierz plik obrazu hello (VHD), który wymaga toobe przesłane.

    ![Rysowanie](media/marketplace-publishing-vm-image-creation/img5.2_06.png)

8.  Po wybraniu pliku VHD hello w kontenerze powitania kliknij pozycję hello **zabezpieczeń** kartę.

    ![Rysowanie](media/marketplace-publishing-vm-image-creation/img5.2_07.png)

9.  W hello **zabezpieczeń kontenera obiektów Blob** okno dialogowe, pozostaw domyślne hello na powitania **poziom dostępu** , a następnie kliknij pozycję **sygnatury dostępu współdzielonego** kartę.

    ![Rysowanie](media/marketplace-publishing-vm-image-creation/img5.2_08.png)

10. Wykonaj kroki hello poniżej toogenerate identyfikator URI sygnatury dostępu współdzielonego dla obrazu vhd hello:

    ![Rysowanie](media/marketplace-publishing-vm-image-creation/img5.2_09.png)

    a. **Zezwala na dostęp:** toosafeguard dla czasu UTC, wybierz hello dzień przed hello bieżącą datę. Na przykład jeśli hello jest data bieżąca 6 października 2014 r., wybierz 2014-10-5.

    b. **Dozwolony dostęp do:** wybierz datę, która jest co najmniej 3 tygodni po hello **zezwala na dostęp** daty.

    c. **Akcje dozwolone:** wybierz hello **listy** i **odczytu** uprawnienia.

    d. Jeśli wybrano plik VHD poprawnie, a następnie plik zostanie wyświetlony w **tooaccess nazwa obiektu Blob** z rozszerzenie VHD.

    e. Kliknij przycisk **generowania podpisu**.

    f. W **wygenerowany udostępnionego dostępu podpisu identyfikator URI tego kontenera**, sprawdź, czy powitania po jak wyróżniono powyżej:

       - Upewnij się, że nazwa pliku obrazu i **"VHD"** w hello identyfikatora URI.
       - Upewnij się, że na końcu hello hello podpisu, **"= rl"** pojawi się. Oznacza to, że dostęp do odczytu i listy podano pomyślnie.
       - Upewnij się, że w środku hello podpisu, **"sr = c"** pojawi się. Oznacza to, czy masz dostęp na poziomie kontenera

11. tooensure, który hello wygenerowany udostępnione działania identyfikator URI sygnatury dostępu, kliknij przycisk **testu w przeglądarce**. Należy ją uruchomić procesu pobierania hello.

12. Skopiuj sygnatury dostępu współdzielonego hello identyfikatora URI. Jest to hello toopaste identyfikator URI do hello Portal publikowania.

13. Powtórz kroki od 6-10 dla każdego wirtualnego dysku twardego w hello jednostki SKU.

**Eksplorator usługi Storage platformy Microsoft Azure (systemem Windows lub MAC/Linux)**

Poniżej przedstawiono kroki hello podczas generowania adresu URL SAS za pomocą Eksploratora usługi Microsoft Azure Storage

1.  Pobierz formularza Eksploratora usługi Microsoft Azure Storage [http://storageexplorer.com/](http://storageexplorer.com/) witryny sieci Web. Przejdź za[Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/releasenotes.html) i kliknij przycisk **"Pobierz dla systemu Windows"**.

    ![Rysowanie](media/marketplace-publishing-vm-image-creation/img5.2_10.png)

2.  Po zakończeniu instalacji, Otwórz aplikację hello.

3.  Kliknij przycisk **Dodaj konto**.

4.  Konfigurowanie subskrypcji tooyour Eksploratora magazynu Microsoft Azure przez logowania na koncie tooyour

    ![Rysowanie](media/marketplace-publishing-vm-image-creation/img5.2_11.png)

5.  Przejdź toostorage konta i wybierz hello kontenera

6.  Wybierz **"Get podpisu dostępu do udziału."** za pomocą kliknij prawym przyciskiem myszy elementu hello **kontenera**

    ![Rysowanie](media/marketplace-publishing-vm-image-creation/img5.2_12.png)

7.  Godzina rozpoczęcia aktualizacji, czas wygaśnięcia i uprawnienia, zgodnie z harmonogramem poniżej

    ![Rysowanie](media/marketplace-publishing-vm-image-creation/img5.2_13.png)

    a.  **Czas rozpoczęcia:** toosafeguard dla czasu UTC, wybierz hello dzień przed hello bieżącą datę. Na przykład jeśli hello jest data bieżąca 6 października 2014 r., wybierz 2014-10-5.

    b.  **Czas wygaśnięcia:** wybierz datę, która jest co najmniej 3 tygodni po hello **czas rozpoczęcia** daty.

    c.  **Uprawnienia:** wybierz hello **listy** i **odczytu** uprawnień

8.  Skopiuj sygnatury dostępu współdzielonego kontenera identyfikatora URI

    ![Rysowanie](media/marketplace-publishing-vm-image-creation/img5.2_14.png)

    Wygenerowany adres URL SAS do kontenera poziom i teraz należy tooadd Nazwa wirtualnego dysku twardego w nim.

    Format adresu URL SAS poziomu kontenera:`https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    Wstaw nazwę dysku VHD po nazwie kontenera hello w adresie URL SAS, jak pokazano poniżej`https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    Przykład:

    ![Rysowanie](media/marketplace-publishing-vm-image-creation/img5.2_15.png)

    TestRGVM201631920152.vhd jest hello Nazwa wirtualnego dysku twardego będzie adres URL SAS wirtualnego dysku twardego`https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    - Upewnij się, że nazwa pliku obrazu i **"VHD"** w hello identyfikatora URI.
    - Upewnij się, że w środku hello podpisu, **"sp = rl"** pojawi się. Oznacza to, że dostęp do odczytu i listy podano pomyślnie.
    - Upewnij się, że w środku hello podpisu, **"sr = c"** pojawi się. Oznacza to, czy masz dostęp na poziomie kontenera

9.  tooensure, który hello działa identyfikator URI sygnatury wygenerowanego dostępu współdzielonego, przetestować go w przeglądarce. Należy uruchomić procesu pobierania hello

10. Skopiuj sygnatury dostępu współdzielonego hello identyfikatora URI. Jest to hello toopaste identyfikator URI do hello Portal publikowania.

11. Powtórz te kroki dla każdego wirtualnego dysku twardego w hello jednostki SKU.

**Interfejs wiersza polecenia platformy Azure (zalecane w przypadku integracji z systemem innym niż Windows & ciągłe)**

Poniżej przedstawiono kroki hello podczas generowania adresu URL sygnatury dostępu Współdzielonego przy użyciu wiersza polecenia platformy Azure

1.  Pobierz program Microsoft Azure CLI z [tutaj](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/). Możesz również znaleźć różnych łączy dla  **[Windows](http://aka.ms/webpi-azure-cli)**  i  **[systemu MAC OS](http://aka.ms/mac-azure-cli)**.

2.  Po pobraniu jej Zainstaluj

3.  Utwórz plik programu PowerShell zawierający następujący kod i zapisz go w lokalnym

          $conn="DefaultEndpointsProtocol=https;AccountName=<StorageAccountName>;AccountKey=<Storage Account Key>"
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl <Permission End Date> -c $conn --start <Permission Start Date>  

    Zaktualizuj następujące hello parametrów w powyżej

    a. **`<StorageAccountName>`**: Nadaj nazwę konta magazynu

    b. **`<Storage Account Key>`**: Podać klucz konta magazynu

    c. **`<Permission Start Date>`**: toosafeguard dla czasu UTC, wybierz hello dzień przed hello bieżącą datę. Na przykład, jeśli hello bieżąca data jest 26 października 2016, wartość powinna być 2016-10-25

    d. **`<Permission End Date>`**: Wybierz datę, która jest co najmniej 3 tygodni po hello **Data rozpoczęcia**. Wartość musi być **2016-11-02**.

    Poniżej przedstawiono hello przykładowy kod po zaktualizowaniu odpowiednie parametry

          $conn="DefaultEndpointsProtocol=https;AccountName=st20151;AccountKey=TIQE5QWMKHpT5q2VnF1bb+NUV7NVMY2xmzVx1rdgIVsw7h0pcI5nMM6+DVFO65i4bQevx21dmrflA91r0Vh2Yw=="
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl 11/02/2016 -c $conn --start 10/25/2016  

4.  Otwórz Edytor programu Powershell w trybie "Uruchom jako Administrator", a następnie otwórz plik w kroku #3.

5.  Witaj wykonywania skryptów i umożliwi hello adres URL SAS dla kontenera poziom dostępu

    Następujące zostanie zapisany hello części hello podpisu sygnatury dostępu Współdzielonego i skopiuj hello wyróżniane w Notatniku

    ![Rysowanie](media/marketplace-publishing-vm-image-creation/img5.2_16.png)

6.  Teraz otrzymasz poziom kontenera adres URL SAS i należy tooadd Nazwa wirtualnego dysku twardego w nim.

    Adres URL SAS poziomu kontenera #

    `https://st20151.blob.core.windows.net/vhds?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

7.  Wstaw nazwę dysku VHD po nazwie kontenera hello w adresie URL SAS, jak pokazano poniżej`https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    Przykład:

    TestRGVM201631920152.vhd jest hello Nazwa wirtualnego dysku twardego będzie adres URL SAS wirtualnego dysku twardego

    `https://st20151.blob.core.windows.net/vhds/ TestRGVM201631920152.vhd?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    - Upewnij się, że nazwa pliku obrazu i "VHD" są w hello identyfikatora URI.
    -   Upewnij się, że w środku podpisu Witaj, "sp = rl" pojawia się. Oznacza to, że dostęp do odczytu i listy podano pomyślnie.
    -   Upewnij się, że w środku podpisu Witaj, "sr = c" pojawia się. Oznacza to, czy masz dostęp na poziomie kontenera

8.  tooensure, który hello działa identyfikator URI sygnatury wygenerowanego dostępu współdzielonego, przetestować go w przeglądarce. Należy uruchomić procesu pobierania hello

9.  Skopiuj sygnatury dostępu współdzielonego hello identyfikatora URI. Jest to hello toopaste identyfikator URI do hello Portal publikowania.

10. Powtórz te kroki dla każdego wirtualnego dysku twardego w hello jednostki SKU.


### <a name="53-provide-information-about-hello-vm-image-and-request-certification-in-hello-publishing-portal"></a>5.3 zawierają informacje o obrazie maszyny Wirtualnej hello i żądanie certyfikacji w hello Portal publikowania
Po utworzeniu oferty i wersji produktu, należy wprowadzić szczegóły obraz powitania skojarzone z tej wersji produktu:

1. Przejdź toohello [Portal publikowania][link-pubportal], a następnie zaloguj się przy użyciu konta sprzedawcy.
2. Wybierz hello **obrazów maszyn wirtualnych** kartę.
3. Identyfikator Hello wyświetlane u góry strony hello hello jest identyfikator oferty hello i nie identyfikator jednostki SKU hello.
4. Wypełnianie właściwości hello w obszarze hello **jednostki SKU** sekcji.
5. W obszarze **rodziny systemów operacyjnych**, kliknij przycisk hello typu systemu operacyjnego skojarzonego z systemu operacyjnego hello wirtualnego dysku twardego.
6. W hello **systemu operacyjnego** pozycję opisują hello systemu operacyjnego. Należy wziąć pod uwagę format jak rodziny systemów operacyjnych, typ, wersja i aktualizacje. Przykładem jest "Windows Server Datacenter 2014 R2".
7. Wybierz się toosix zalecane rozmiary maszyn wirtualnych. Są to zalecenia pobierające klienta toohello wyświetlane w bloku warstwa cenowa hello w hello portalu Azure, gdy zdecydować toopurchase i wdrożyć obraz. **Są to tylko zalecenia. Klient Hello jest możliwe tooselect żadnych rozmiar maszyny Wirtualnej, uwzględniający hello dysków określona w obrazie.**
8. Wprowadź hello wersji. pole wersji Hello hermetyzuje hello tooidentify wersję produktu i jego aktualizacje:
   * Wersje muszą mieć format hello X.Y.Z, gdzie X, Y i Z są liczbami całkowitymi.
   * Obrazy w różne jednostki magazynowe mogą mieć różne wersje główne i pomocnicze.
   * Wersje w jednostce SKU powinien mieć tylko zmiany przyrostowe, które zwiększają hello wersji poprawki (Z z X.Y.Z).
9. W hello **adres URL dysku VHD systemu operacyjnego** wprowadź sygnatury dostępu współdzielonego hello identyfikator URI utworzony dla systemu operacyjnego hello wirtualnego dysku twardego.
10. W przypadku dysków z danymi skojarzonego z tym jednostki SKU wybierz hello jednostki logicznej numer (LUN) toowhich chcesz toobe dysku danych, to zainstalowane po wdrożeniu.
11. W hello **adres URL dysku VHD X LUN** wprowadź sygnatury dostępu współdzielonego hello identyfikator URI utworzony dla hello pierwsze dane wirtualnego dysku twardego.

    ![Rysowanie](media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-3.png)


## <a name="common-sas-url-issues--fixes"></a>Typowe problemy adres URL SAS i poprawki

|Problem|Komunikat o błędzie|Poprawka|Łącze dokumentacji|
|---|---|---|---|
|Błąd podczas kopiowania obrazy — "?" nie znajduje się w adresie url SAS|Błąd: Kopiowanie obrazów. Przy użyciu obiektu blob toodownload nie można podać identyfikatora Uri połączenia SAS.|Przy użyciu adresu Url SAS hello aktualizacji zalecane narzędzia|[https://Azure.microsoft.com/en-us/Documentation/articles/Storage-DotNet-Shared-Access-Signature-Part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Błąd podczas kopiowania obrazy — parametry "st" i "se", nie w SAS url|Błąd: Kopiowanie obrazów. Przy użyciu obiektu blob toodownload nie można podać identyfikatora Uri połączenia SAS.|Aktualizacja hello adres Url SAS z dat rozpoczęcia i zakończenia na nim|[https://Azure.microsoft.com/en-us/Documentation/articles/Storage-DotNet-Shared-Access-Signature-Part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Błąd podczas kopiowania obrazów — "sp = rl" nie znajduje się w adres url SAS|Błąd: Kopiowanie obrazów. Przy użyciu obiektu blob toodownload nie można podać identyfikatora Uri połączenia SAS|Aktualizacja hello adres Url SAS z uprawnienia "Odczyt" & "Lista jako|[https://Azure.microsoft.com/en-us/Documentation/articles/Storage-DotNet-Shared-Access-Signature-Part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Błąd podczas kopiowania obrazów — adres url SAS ma białe znaki w nazwie wirtualnego dysku twardego|Błąd: Kopiowanie obrazów. Przy użyciu obiektu blob toodownload nie można podać identyfikatora Uri połączenia SAS.|Aktualizacja hello adres Url SAS, bez spacji|[https://Azure.microsoft.com/en-us/Documentation/articles/Storage-DotNet-Shared-Access-Signature-Part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Błąd podczas kopiowania obrazów — błąd autoryzacji adresów Url SAS|Błąd: Kopiowanie obrazów. Obiekt blob nie jest w stanie toodownload ze względu na błąd tooauthorization|Wygeneruj ponownie hello adres Url SAS|[https://Azure.microsoft.com/en-us/Documentation/articles/Storage-DotNet-Shared-Access-Signature-Part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|


## <a name="next-step"></a>Następny krok
Po wykonaniu szczegóły jednostki SKU hello, możesz przejść do przodu toohello [marketing przewodnik zawartości portalu Azure Marketplace][link-pushstaging]. W tym kroku procesu publikowania hello, podaj hello marketingu zawartość, ceny i innych informacji przed niezbędne zbyt**krok 3: testowanie maszyny Wirtualnej oferują tymczasowych**, który testować różne scenariusze przypadek użycia przed wdrożeniem Witaj toohello oferta portalu Azure Marketplace widoczności publicznej i zakupu.  

## <a name="see-also"></a>Zobacz też
* [Wprowadzenie: jak toopublish toohello oferta portalu Azure Marketplace](marketplace-publishing-getting-started.md)

[img-acom-1]:media/marketplace-publishing-vm-image-creation/vm-image-acom-datacenter.png
[img-portal-vm-size]:media/marketplace-publishing-vm-image-creation/vm-image-portal-size.png
[img-portal-vm-create]:media/marketplace-publishing-vm-image-creation/vm-image-portal-create-vm.png
[img-portal-vm-location]:media/marketplace-publishing-vm-image-creation/vm-image-portal-location.png
[img-portal-vm-rdp]:media/marketplace-publishing-vm-image-creation/vm-image-portal-rdp.png
[img-azstg-add]:media/marketplace-publishing-vm-image-creation/vm-image-storage-add.png
[img-manage-vm-new]:media/marketplace-publishing-vm-image-creation/vm-image-manage-new.png
[img-manage-vm-select]:media/marketplace-publishing-vm-image-creation/vm-image-manage-select.png
[img-cert-vm-key-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-keyfile-linux.png
[img-cert-vm-pswd-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-linux.png
[img-cert-vm-pswd-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-win.png
[img-cert-vm-test-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-linux.png
[img-cert-vm-test-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-win.png
[img-cert-vm-results]:media/marketplace-publishing-vm-image-creation/vm-image-certification-results.png
[img-cert-vm-questionnaire]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire.png
[img-cert-vm-questionnaire-2]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire-2.png
[img-pubportal-vm-skus]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus.png
[img-pubportal-vm-skus-2]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-2.png

[link-pushstaging]:marketplace-publishing-push-to-staging.md
[link-github-waagent]:https://github.com/Azure/WALinuxAgent
[link-azure-codeplex]:https://azurestorageexplorer.codeplex.com/
[link-azure-2]:../storage/blobs/storage-dotnet-shared-access-signature-part-2.md
[link-azure-1]:../storage/common/storage-dotnet-shared-access-signature-part-1.md
[link-msft-download]:http://www.microsoft.com/download/details.aspx?id=44299
[link-technet-3]:https://technet.microsoft.com/library/hh846766.aspx
[link-technet-2]:https://msdn.microsoft.com/library/dn495261.aspx
[link-azure-portal]:https://portal.azure.com
[link-pubportal]:https://publish.windowsazure.com
[link-sql-2014-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014enterprisewindowsserver2012r2/
[link-sql-2014-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014standardwindowsserver2012r2/
[link-sql-2014-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014webwindowsserver2012r2/
[link-sql-2012-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2enterprisewindowsserver2012/
[link-sql-2012-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2standardwindowsserver2012/
[link-sql-2012-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2webwindowsserver2012/
[link-datactr-2012-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012r2datacenter/
[link-datactr-2012]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012datacenter/
[link-datactr-2008-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2008r2sp1/
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-technet-1]:https://technet.microsoft.com/library/hh848454.aspx
[link-azure-vm-2]:./virtual-machines-linux-agent-user-guide/
[link-openssl]:https://www.openssl.org/
[link-intsvc]:http://www.microsoft.com/download/details.aspx?id=41554
[link-python]:https://www.python.org/
