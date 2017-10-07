---
title: aaaSQL Server Business Intelligence | Dokumentacja firmy Microsoft
description: "W tym temacie używa zasobów utworzone za pomocą hello klasycznego modelu wdrażania i opisuje hello Business Intelligence (BI) funkcje dostępne dla programu SQL Server uruchomionego na maszynach wirtualnych Azure (VM)."
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: c681e7a7-eeda-48aa-bc35-6277f4828244
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/30/2017
ms.author: asaxton
ms.openlocfilehash: e3288f0835d6c4a19baeeea5f6b65fec16cd751f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-business-intelligence-in-azure-virtual-machines"></a>Analiza biznesowa programu SQL Server w usłudze Azure Virtual Machines
> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.

Galeria maszyny wirtualnej platformy Microsoft Azure Hello obejmuje obrazów, które zawierają instalacje programu SQL Server. Witaj programu SQL Server są obsługiwane w przypadku obrazów Galeria hello wersje hello tych samych plików instalacji można zainstalować komputerów lokalnych tooon i maszyny wirtualne. Ten temat zawiera podsumowanie hello programu SQL Server Business Intelligence (BI) funkcji zainstalowanych na powitania obrazów i czynności konfiguracyjnych wymaganych po udostępnieniu maszyny wirtualnej. W tym temacie opisano obsługiwane topologie wdrażania funkcji analizy Biznesowej i najlepsze rozwiązania.

## <a name="license-considerations"></a>Uwagi dotyczące licencji
Istnieją dwa sposoby toolicense programu SQL Server w maszynach wirtualnych platformy Azure firmy Microsoft:

1. Korzyści mobilności licencji, które są częścią Software Assurance. Aby uzyskać więcej informacji, zobacz [przenośność licencji za pośrednictwem programu Software Assurance na platformie Azure](https://azure.microsoft.com/pricing/license-mobility/).
2. Należy zwrócić na godzinę szybkość maszyn wirtualnych Azure z programem SQL Server zainstalowana. Zobacz hello sekcji "Program SQL Server" w [cennik maszyn wirtualnych](https://azure.microsoft.com/pricing/details/virtual-machines/#Sql).

Aby uzyskać więcej informacji o licencji i bieżącej szybkości, zobacz [często zadawane pytania dotyczące licencjonowania maszyn wirtualnych](https://azure.microsoft.com/pricing/licensing-faq/%20/).

## <a name="sql-server-images-available-in-azure-virtual-machine-gallery"></a>SQL Server dostępnych obrazów w galerii maszyn wirtualnych platformy Azure
Galeria maszyny wirtualnej platformy Microsoft Azure Hello zawiera kilka obrazów, które zawierają programu Microsoft SQL Server. Witaj oprogramowania zainstalowanego na powitania obrazy maszyny wirtualnej zależy od hello hello systemu operacyjnego i hello wersja programu SQL Server. Witaj listę dostępnych obrazów w galerii Azure maszyny wirtualnej hello zmienia się często.

<!--![SQL image in azure VM gallery](./media/virtual-machines-windows-classic-ps-sql-bi/IC741367.png)-->
![Obraz SQL w galerii maszyn wirtualnych Azure](./media/virtual-machines-windows-classic-ps-sql-bi/vm-sql-images.png)

![PowerShell](./media/virtual-machines-windows-classic-ps-sql-bi/IC660119.gif) Hello następujący skrypt programu PowerShell zwraca listę hello Azure obrazów, które zawierają "SQL Server" w hello Nazwa_obrazu:

    # assumes you have already uploaded a management certificate tooyour Microsoft Azure Subscription. View hello thumbprint value from hello "Subscriptions" menu in Azure portal.

    $subscriptionID = ""    # REQUIRED: Provide your subscription ID.
    $subscriptionName = "" # REQUIRED: Provide your subscription name.
    $thumbPrint = "" # REQUIRED: Provide your certificate thumbprint.
    $certificate = Get-Item cert:\currentuser\my\$thumbPrint # REQUIRED: If your certificate is in a different store, provide it here.-Ser  store is hello one specified with hello -ss parameter on MakeCert

    Set-AzureSubscription -SubscriptionName $subscriptionName -Certificate $certificate -SubscriptionID $subscriptionID

    Write-Host -foregroundcolor green "List of available gallery images where imagename contains 2016"
    Write-Host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
    get-azurevmimage | where {$_.ImageName -Like "*SQL-Server-2016*"} | select imagename,category, location, label, description

    Write-Host -foregroundcolor green "List of available gallery images where imagename contains 2014"
    Write-Host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
    get-azurevmimage | where {$_.ImageName -Like "*SQL-Server-2014*"} | select imagename,category, location, label, description

Aby uzyskać więcej informacji o wersji i funkcji obsługiwanych przez program SQL Server zobacz następujące hello:

* [Wersje programu SQL Server](https://www.microsoft.com/server-cloud/products/sql-server-editions/#fbid=Zae0-E6r5oh)
* [Funkcje obsługiwane przez hello wersje programu SQL Server 2016](https://msdn.microsoft.com/library/cc645993.aspx)

### <a name="bi-features-installed-on-hello-sql-server-virtual-machine-gallery-images"></a>BI funkcje zainstalowane na powitania obrazów Galeria maszyny wirtualnej serwera SQL
Witaj Poniższa tabela zawiera podsumowanie funkcji analizy biznesowej hello zainstalowane na powitania wspólnej obrazów Galeria maszyny wirtualnej platformy Microsoft Azure dla programu SQL Server:

* SQL Server 2016 SP1 Enterprise
* SQL Server 2016 z dodatkiem SP1 Standard
* SQL Server 2014 SP2 Enterprise
* SQL Server 2014 z dodatkiem SP2 Standard
* SQL Server 2012 z dodatkiem SP3 Enterprise
* SQL Server 2012 Standard z dodatkiem SP3

| SQL Server BI funkcji | Zainstalować w obrazie galerii hello | Uwagi |
| --- | --- | --- |
| **Tryb macierzysty usług raportowania** |Tak |Zainstalowany, ale wymaga konfiguracji, w tym adres URL Menedżera raportów hello. Zobacz sekcję hello [skonfigurować usługi Reporting Services](#configure-reporting-services). |
| **Usług raportowania w trybie programu SharePoint** |Nie |Witaj galerii maszyny wirtualnej platformy Microsoft Azure nie ma programu SharePoint lub SharePoint plików instalacyjnych. <sup>1</sup> |
| **Wyszukiwania danych i wielowymiarowych usług Analysis Services (OLAP)** |Tak |Hello zainstalowana i skonfigurowana jako domyślne wystąpienie usług Analysis Services |
| **Tabelaryczne usług Analysis Services** |Nie |Obsługiwane w programie SQL Server 2012, 2014 i 2016 obrazów, ale go nie zainstalowano domyślnie. Zainstalować inne wystąpienie usług Analysis Services. Zobacz sekcję hello instalowanie innych usług SQL Server i funkcji w tym temacie. |
| **Dodatek Power Pivot usług analizy dla programu SharePoint** |Nie |Witaj galerii maszyny wirtualnej platformy Microsoft Azure nie ma programu SharePoint lub SharePoint plików instalacyjnych. <sup>1</sup> |

<sup>1</sup> dodatkowe informacje na temat programu SharePoint i maszyn wirtualnych platformy Azure, zobacz [Microsoft Azure architektury programu SharePoint 2013](https://technet.microsoft.com/library/dn635309.aspx) i [wdrożenia programu SharePoint na maszynach wirtualnych Azure Microsoft](https://www.microsoft.com/download/details.aspx?id=34598).

![PowerShell](./media/virtual-machines-windows-classic-ps-sql-bi/IC660119.gif) Uruchom powitania po tooget polecenia programu PowerShell listę zainstalowanych usług, które zawierają "SQL" w nazwie usługi hello.

    get-service | Where-Object{ $_.DisplayName -like '*SQL*' } | Select DisplayName, status, servicetype, dependentservices | format-Table -AutoSize

## <a name="general-recommendations-and-best-practices"></a>Ogólne zalecenia i najlepsze rozwiązania
* Minimalna Hello zalecany rozmiar maszyny wirtualnej jest **A3** przy użyciu programu SQL Server Enterprise Edition. Witaj **A4** rozmiar maszyny wirtualnej jest zalecane w przypadku wdrożeń analizy Biznesowej programu SQL Server Analysis Services i usług Reporting Services.
  
    Informacje na powitania bieżący rozmiar maszyny Wirtualnej, zobacz [rozmiarów maszyn wirtualnych na platformie Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Najlepszym rozwiązaniem do zarządzania dyskami jest inny niż toostore danych, dzienników i pliki kopii zapasowych na dyskach **C**: i **D**:. Na przykład utworzyć dysków z danymi **E**: i **F**:.
  
  * dysk Hello buforowanie zasad dla hello domyślnym dysku **C**: nie są optymalne dla pracy z danymi.
  * Witaj **D**: dysk jest dyskiem tymczasowego, który jest używany głównie w pliku stronicowania hello. Witaj **D**: dysk nie jest trwały i nie są zapisywane w magazynie obiektów blob. Zadania zarządzania, takie jak zmiana rozmiaru maszyny wirtualnej toohello zresetować hello **D**: dysku. Zalecane jest zbyt**nie** Użyj hello **D**: dysku plików bazy danych, takie jak bazy danych tempdb.
    
    Aby uzyskać więcej informacji na temat tworzenia i dołączania dysków, zobacz [jak tooAttach tooa dysku danych maszyny wirtualnej](../classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
* Zatrzymaj lub odinstalowywanie usług nie jest planowana toouse. Przykład jeśli maszyna wirtualna hello jest używany tylko dla usług Reporting Services, Zatrzymaj lub odinstalowanie usług Analysis Services i SQL Server Integration Services. Witaj poniższej ilustracji przedstawiono przykładowy hello usług, które są uruchamiane domyślnie.
  
    ![Usługi programu SQL Server](./media/virtual-machines-windows-classic-ps-sql-bi/IC650107.gif)
  
  > [!NOTE]
  > Aparat bazy danych programu SQL Server Hello jest wymagany w scenariuszach BI hello obsługiwane. Topologia maszyny Wirtualnej na jednym serwerze, hello aparatu bazy danych jest wymagana w tej samej maszyny Wirtualnej hello toobe systemem.
  
    Aby uzyskać więcej informacji, zobacz następujące hello: [odinstalowania usług Reporting Services](https://msdn.microsoft.com/library/hh479745.aspx) i [Odinstalowywanie wystąpienia Analysis Services](https://msdn.microsoft.com/library/ms143687.aspx).
* Sprawdź **usługi Windows Update** nowe "ważne aktualizacje". obrazy maszyny wirtualnej platformy Microsoft Azure Hello często są odświeżane; jednak ważne aktualizacje może stać się dostępne z **usługi Windows Update** po ostatniego odświeżenia hello obrazu maszyny Wirtualnej.

## <a name="example-deployment-topologies"></a>Przykładowe topologie wdrażania
Witaj poniżej przedstawiono przykład wdrożenia, których użyć maszyny wirtualne Microsoft Azure. topologie Hello na diagramach te są tylko niektóre hello topologie możliwe, który za pomocą funkcji analizy Biznesowej programu SQL Server i maszyny wirtualne Microsoft Azure.

### <a name="single-virtual-machine"></a>Jednej maszyny wirtualnej
Analysis Services, usług Reporting Services, aparatu bazy danych programu SQL Server i źródeł danych na jednej maszynie wirtualnej.

![Scenariusz 1 maszynę wirtualną raz analizy biznesowej](./media/virtual-machines-windows-classic-ps-sql-bi/IC650108.gif)

### <a name="two-virtual-machines"></a>Dwie maszyny wirtualne
* Usług Analysis Services, usługi Reporting Services i hello aparatu bazy danych programu SQL Server na jednej maszynie wirtualnej. To wdrożenie obejmuje hello baz danych serwera raportów.
* Źródła danych na drugim maszyny Wirtualnej. Witaj drugiej maszyny Wirtualnej zawiera aparat bazy danych programu SQL Server jako źródła danych.

![Scenariusz 2 maszyn wirtualnych iaas analizy biznesowej](./media/virtual-machines-windows-classic-ps-sql-bi/IC650109.gif)

### <a name="mixed-azure--data-on-azure-sql-database"></a>Mieszane Azure — dane w bazie danych Azure SQL
* Usług Analysis Services, usługi Reporting Services i hello aparatu bazy danych programu SQL Server na jednej maszynie wirtualnej. To wdrożenie obejmuje hello baz danych serwera raportów.
* Źródło danych jest baza danych Azure SQL.

![Maszyna wirtualna scenariusze analizy biznesowej iaas i AzureSQL jako źródło danych](./media/virtual-machines-windows-classic-ps-sql-bi/IC650110.gif)

### <a name="hybrid-data-on-premises"></a>Hybrydowe — danych w sieci lokalnej
* W to Przykładowe wdrożenie usług Analysis Services, usługi Reporting Services i hello aparatu bazy danych programu SQL Server uruchomiony na jednej maszynie wirtualnej. hosty maszyn wirtualnych Hello hello baz danych serwera raportów. Maszyna wirtualna Hello jest tooan przyłączone do domeny lokalnej za pośrednictwem sieci wirtualnej platformy Azure lub innych VPN, tunelowania rozwiązania.
* Źródło danych działa lokalnie.

![iaas analizy biznesowej scenariusze maszyny wirtualnej i lokalnego źródła danych](./media/virtual-machines-windows-classic-ps-sql-bi/IC654384.gif)

## <a name="reporting-services-native-mode-configuration"></a>Konfiguracji usługi raportowania w trybie macierzystym
Hello obraz galerii maszyny wirtualnej dla programu SQL Server zawiera tryb macierzysty usług Reporting zainstalowany, jednak hello serwer raportów nie jest skonfigurowany. kroki Hello w tej sekcji konfigurowania serwera raportów usług Reporting Services hello. Aby uzyskać szczegółowe informacje na temat konfigurowania trybu macierzystego usług raportowania, zobacz [zainstalować Reporting Services macierzysty tryb raportu serwera (SSRS)](https://msdn.microsoft.com/library/ms143711.aspx).

> [!NOTE]
> Podobne zawartości, która korzysta z serwera raportów hello tooconfigure skryptów środowiska Windows PowerShell, zobacz [tooCreate Użyj programu PowerShell Azure maszyny Wirtualnej z macierzysty tryb serwera raportów](../classic/ps-sql-report.md).

### <a name="connect-toohello-virtual-machine-and-start-hello-reporting-services-configuration-manager"></a>Połącz toohello maszynę wirtualną i uruchomić hello Menedżer konfiguracji usług Reporting Services
Istnieją dwie typowe przepływy pracy dla łączenia tooan maszyny wirtualnej platformy Azure:

* tooconnect w hello, kliknij nazwę hello hello maszyny wirtualnej, a następnie kliknij przycisk **Connect**. Otwiera połączeń usług pulpitu zdalnego i nazwa komputera hello jest wypełniane automatycznie.
  
    ![Połącz tooazure maszyny wirtualnej](./media/virtual-machines-windows-classic-ps-sql-bi/IC650112.gif)
* Maszyna wirtualna toohello Uzyskuj dostęp do usługi Podłączanie pulpitu zdalnego systemu Windows. W interfejsie użytkownika hello hello pulpitu zdalnego:
  
  1. Typ hello **nazwa usługi w chmurze** jako hello nazwy komputera.
  2. Wpisz dwukropka (:) a hello numer portu publicznego, który jest skonfigurowany dla hello zdalnego pulpitu punkt końcowy protokołu TCP.
     
      Myservice.cloudapp.NET:63133
     
      Aby uzyskać więcej informacji, zobacz [co to jest usługa w chmurze?](https://azure.microsoft.com/manage/services/cloud-services/what-is-a-cloud-service/).


**Uruchom Menedżera konfiguracji usług raportowania**

W **systemu Windows Server 2012/2016**:

1. Z hello **Start** ekranu, wpisz **usług Reporting Services** toosee listę aplikacji.
2. Kliknij prawym przyciskiem myszy **Reporting Services Configuration Manager** i kliknij przycisk **Uruchom jako Administrator**.

W **systemu Windows Server 2008 R2**:

1. Kliknij przycisk **Start**, a następnie kliknij przycisk **wszystkie programy**.
2. Kliknij przycisk **programu Microsoft SQL Server 2016**.
3. Kliknij przycisk **narzędzia do konfiguracji**.
4. Kliknij prawym przyciskiem myszy **Reporting Services Configuration Manager** i kliknij przycisk **Uruchom jako Administrator**.

Lub:

1. Kliknij przycisk **Start**.
2. W hello **Wyszukaj programy i pliki** typu okna dialogowego **usługi reporting services**. Jeśli hello maszyny Wirtualnej jest uruchomiony system Windows Server 2012, wpisz **usługi reporting services** na ekranie Start systemu Windows Server 2012 hello.
3. Kliknij prawym przyciskiem myszy **Reporting Services Configuration Manager** i kliknij przycisk **Uruchom jako Administrator**.
   
    ![Wyszukaj menedżera konfiguracji usług ssrs](./media/virtual-machines-windows-classic-ps-sql-bi/IC650113.gif)

### <a name="configure-reporting-services"></a>Konfigurowanie usług Reporting Services
**Konto usługi i adres URL usługi sieci web:**

1. Sprawdź hello **nazwy serwera** jest nazwa serwera lokalne powitania i kliknij przycisk **Connect**.
2. Uwaga hello puste **Nazwa bazy danych serwera raportów**. Witaj baza danych została utworzona, po zakończeniu konfiguracji hello.
3. Sprawdź hello **stan serwera raportów** jest **uruchomiono**. Jeśli chcesz, aby usługa hello tooverify w Menedżerze serwera systemu Windows, usługa hello jest hello **programu SQL Server Reporting Services** usługi systemu Windows.
4. Kliknij przycisk **konta usługi** i zmień konto hello zgodnie z potrzebami. Jeśli maszyna wirtualna hello jest używany w środowisku przyłączone do domeny z systemem innym niż, hello wbudowanych **ReportServer** konta jest wystarczająca. Aby uzyskać więcej informacji na koncie usługi hello, zobacz [konta usługi](https://msdn.microsoft.com/library/ms189964.aspx).
5. Kliknij przycisk **adres URL usługi sieci Web** w okienku po lewej stronie powitania.
6. Kliknij przycisk **Zastosuj** tooconfigure hello domyślne wartości.
7. Uwaga hello **adresów URL usługi sieci Web serwera raportów**. Należy zauważyć, hello domyślny port TCP 80 i jest częścią hello adresu URL. W kolejnym kroku utworzysz punkt końcowy maszyny wirtualnej Azure Microsoft hello portu.
8. W hello **wyniki** okienka, sprawdź akcje hello została ukończona pomyślnie.

**Baza danych:**

1. Kliknij przycisk **bazy danych** w okienku po lewej stronie powitania.
2. Kliknij przycisk **zmienić bazę danych**.
3. Sprawdź **Utwórz nową bazę danych serwera raportów** jest zaznaczone, a następnie kliknij przycisk Dalej.
4. Sprawdź **nazwy serwera** i kliknij przycisk **Testuj połączenie**.
5. Jeśli wynik hello jest **pomyślnie nawiązano połączenie testowe**, kliknij przycisk **OK** , a następnie kliknij przycisk **dalej**.
6. Nazwa bazy danych Uwaga hello jest **ReportServer** i hello **tryb serwera raportów** jest **natywnego** kliknięcie **dalej**.
7. Kliknij przycisk **dalej** na powitania **poświadczenia** strony.
8. Kliknij przycisk **dalej** na powitania **Podsumowanie** strony.
9. Kliknij przycisk **dalej** na powitania **postępu i Zakończ** strony.

**Sieci Web portalu adres URL lub adres URL Menedżera raportów 2012 i 2014:**

1. Kliknij przycisk **adres URL portalu sieci Web**, lub **adres URL Menedżera raportów** 2014 i 2012, w okienku po lewej stronie powitania.
2. Kliknij przycisk **Zastosuj**.
3. W hello **wyniki** okienka, sprawdź akcje hello została ukończona pomyślnie.
4. Kliknij przycisk **zakończenia**.

Uzyskać informacji dotyczących uprawnień serwera raportów, zobacz [udzielanie uprawnień na serwerze raportów trybu macierzystego](https://msdn.microsoft.com/library/ms156014.aspx).

### <a name="browse-toohello-local-report-manager"></a>Przeglądaj toohello lokalnego Menedżera raportów
tooverify hello, przeglądania tooreport Menedżera konfiguracji na powitania maszyny Wirtualnej.

1. Na powitania maszyny Wirtualnej Uruchom program Internet Explorer z uprawnieniami administratora.
2. Przeglądaj toohttp://localhost/reports na powitania maszyny Wirtualnej.

### <a name="tooconnect-tooremote-web-portal-or-report-manager-for-2014-and-2012"></a>portal sieci web tooRemote tooConnect lub Menedżera raportów 2014 i 2012
Portal sieci web toohello tooconnect lub Menedżera raportów 2014 i 2012 na maszynie wirtualnej hello z komputera zdalnego, utworzyć nową maszynę wirtualną punktu końcowego TCP. Domyślnie program hello serwer raportów nasłuchuje żądań HTTP na **port 80**. Jeśli konfigurujesz hello raportu serwera adresów URL toouse innego portu, należy określić ten numer portu w hello, postępując zgodnie z instrukcjami.

1. Tworzenie punktu końcowego dla hello maszyny wirtualnej TCP Port 80. Aby uzyskać więcej informacji, zobacz hello [punkty końcowe maszyny wirtualnej i porty zapory](#virtual-machine-endpoints-and-firewall-ports) części tego dokumentu.
2. Otwórz port 80 w zaporze maszyny wirtualnej hello.
3. Przeglądaj toohello portalu sieci web lub Menedżera raportów, przy użyciu maszyny wirtualnej Azure **nazwy DNS** jako hello nazwę serwera w adresie URL hello. Na przykład:
   
    **Serwer raportów**: http://uebi.cloudapp.net/reportserver **portalu sieci Web**: http://uebi.cloudapp.net/reports
   
    [Skonfiguruj zaporę dostępu do serwera raportów](https://msdn.microsoft.com/library/bb934283.aspx)

### <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a>tooCreate i opublikować raporty toohello maszyny wirtualnej platformy Azure
Witaj poniższej tabeli przedstawiono niektóre istniejące raporty toopublish dostępne opcje hello z komputera lokalnego toohello serwera raportów hostowanych na powitania maszyny wirtualnej platformy Microsoft Azure:

* **Report Builder**: hello maszyny wirtualnej zawiera powitania kliknij — raz wersji programu Microsoft SQL Server Report Builder for SQL 2014 i 2012. toostart raport konstruktora powitania po raz pierwszy na maszynie wirtualnej hello SQL 2016:
  
  1. Uruchom przeglądarkę z uprawnieniami administracyjnymi.
  2. Wyszukaj toohello w portalu sieci web na maszynie wirtualnej hello i wybierz hello **Pobierz** ikonę w prawym górnym rogu hello.
  3. Wybierz **Report Builder**.
     
     Aby uzyskać więcej informacji, zobacz [uruchomić program Report Builder](https://msdn.microsoft.com/library/ms159221.aspx).
* **SQL Server Data Tools**: maszyna wirtualna: SQL Server Data Tools jest zainstalowany na maszynie wirtualnej hello i mogą być używane toocreate **projektów serwera raportów** i raporty na powitania maszyny wirtualnej. SQL Server Data Tools można opublikować serwera raportów toohello raporty hello hello maszyny wirtualnej.
* **Program SQL Server Data Tools: Zdalny**: na komputerze lokalnym, Utwórz projekt usług Reporting Services w programie SQL Server Data Tools, który zawiera raporty usług Reporting Services. Skonfiguruj tooconnect projektu hello toohello URL usługi sieci web.
  
    ![Właściwości projektu narzędzia SSDT dla projektu usług SSRS](./media/virtual-machines-windows-classic-ps-sql-bi/IC650114.gif)
* Utwórz. Wirtualny dysk twardy dysk twardy zawiera raporty, a następnie przekaż i dołączyć hello dysku.
  
  1. Utwórz. Dysk VHD na komputerze lokalnym, który zawiera raporty.
  2. Utwórz i zainstaluj certyfikat zarządzania.
  3. Przekaż tooAzure pliku wirtualnego dysku twardego hello przy użyciu polecenia cmdlet Add-AzureVHD hello [tworzenie i przekazywanie wirtualnego dysku twardego z systemem Windows Server tooAzure](../classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
  4. Dołączanie maszyny wirtualnej toohello dysku hello.

## <a name="install-other-sql-server-services-and-features"></a>Instalowanie innych usług SQL Server i funkcji
tooinstall dodatkowe usługi programu SQL Server, takich jak usługi Analysis Services w trybie tabelarycznym, uruchom Kreatora instalacji serwera SQL hello. pliki Instalatora Hello znajdują się na lokalnym dysku maszyny wirtualnej hello.

1. Kliknij przycisk **Start** , a następnie kliknij przycisk **wszystkie programy**.
2. Kliknij przycisk **Microsoft SQL Server 2016**, **programu Microsoft SQL Server 2014** lub **programu Microsoft SQL Server 2012** , a następnie kliknij przycisk **narzędzia do konfiguracji**.
3. Kliknij przycisk **Centrum instalacji programu SQL Server**.

Lub uruchom C:\SQLServer_13.0_full\setup.exe, C:\SQLServer_12.0_full\setup.exe lub C:\SQLServer_11.0_full\setup.exe

> [!NOTE]
> powitania po raz pierwszy po uruchomieniu Instalatora programu SQL Server, Instalator więcej plików może zostać pobrana i wymaga ponownego uruchomienia maszyny wirtualnej hello i ponownie uruchomić Instalatora programu SQL Server.
> 
> Jeśli potrzebujesz toorepeatedly dostosować obraz powitania od hello maszyny wirtualnej platformy Microsoft Azure, rozważ możliwość utworzenia obrazu programu SQL Server. Funkcje programu SysPrep usług analizy został włączony CU2 dodatku SP1 dla programu SQL Server 2012. Aby uzyskać więcej informacji, zobacz [zagadnienia dotyczące instalowania programu SQL Server przy użyciu narzędzia SysPrep](https://msdn.microsoft.com/library/ee210754.aspx) i [Obsługa programu Sysprep dla ról serwera](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).
> 
> 

### <a name="tooinstall-analysis-services-tabular-mode"></a>tooInstall w trybie tabelarycznym Analysis Services
Witaj kroki opisane w tej sekcji **Podsumuj** hello instalacji usług Analysis Services trybie tabelarycznym. Aby uzyskać więcej informacji zobacz następujące hello:

* [Instalowanie usług Analysis Services w trybie tabelarycznym](https://msdn.microsoft.com/library/hh231722.aspx)
* [Tabelaryczne modelowania (samouczek Adventure Works)](https://msdn.microsoft.com/library/140d0b43-9455-4907-9827-16564a904268)

**tooInstall w trybie tabelarycznym Analysis Services:**

1. W Kreatorze instalacji programu SQL Server hello, kliknij przycisk **instalacji** w lewym okienku hello, a następnie kliknij przycisk **Instalacja autonomiczna nowego programu SQL server lub dodać funkcje tooan istniejącej instalacji**.
   
   * Jeśli widzisz hello **przeglądanie w poszukiwaniu folderu**, przejdź tooc:\SQLServer_13.0_full, c:\SQLServer_12.0_full lub c:\SQLServer_11.0_full, a następnie kliknij przycisk **Ok**.
2. Kliknij przycisk **dalej** na stronie aktualizacje produktu hello.
3. Na powitania **typu instalacji** wybierz pozycję **nowej instalacji programu SQL Server** i kliknij przycisk **dalej**.
4. Na powitania **Rola Instalatora** kliknij przycisk **instalacja funkcji programu SQL Server**.
5. Na powitania **wybór funkcji** kliknij przycisk **usług Analysis Services**.
6. Na powitania **Konfiguracja wystąpienia** wpisz nazwę opisową, takich jak **tabelaryczny** do **wystąpienia o nazwie** i **identyfikator wystąpienia** tekstu pola.
7. Na powitania **Konfiguracja usługi Analysis Services** wybierz pozycję **trybie tabelarycznym**. Dodaj hello bieżącego użytkownika toohello uprawnień administracyjnych listy.
8. Wypełnij i zamknąć kreatora instalacji programu SQL Server hello.

## <a name="analysis-services-configuration"></a>Konfiguracja usługi Analysis Services
### <a name="remote-access-tooanalysis-services-server"></a>TooAnalysis dostępu zdalnego serwer usług
Serwer usług Analysis Services obsługuje tylko uwierzytelnianie systemu windows. usługi Analysis Services tooaccess zdalnie za pośrednictwem aplikacji klienckich, takich jak SQL Server Management Studio lub SQL Server Data Tools, maszyna wirtualna hello musi toobe tooyour dołączonego do lokalnej domeny, przy użyciu sieci wirtualnych Azure. Aby uzyskać więcej informacji, zobacz [sieci wirtualnej Azure](../../../virtual-network/virtual-networks-overview.md).

A **domyślnego wystąpienia** usług Analysis Services nasłuchuje na porcie TCP **2383**. Otwórz hello port hello zapory maszyn wirtualnych. Klastrowane nazwane wystąpienie usług Analysis Services również odbiera na porcie **2383**.

Dla **nazwane wystąpienie** usług Analysis Services jest wymagana usługa SQL Server Browser hello toomanage port dostępu. Witaj SQL Server Browser domyślnej konfiguracji jest port **2382**.

Witaj maszyny wirtualne zapory, należy otworzyć port **2382** i utworzyć statyczne Analysis Services o nazwie wystąpienia portu.

1. tooverify portów, które są już hello maszyny Wirtualnej i jakie procesy wykorzystują hello portów w systemie, uruchom następujące polecenia z uprawnieniami administracyjnymi hello:
   
        netstat /ao
2. Użyj programu SQL Server Management Studio toocreate statycznych usług Analysis Services o nazwie wystąpienia portu, aktualizując "Port" wartość w tabelarycznym jako właściwości ogólnych wystąpienia. Aby uzyskać więcej informacji, zobacz Witaj "Stały port używany do domyślne lub nazwane wystąpienie" w [skonfigurować tooAllow zapory systemu Windows hello dostęp do usług analizy](https://msdn.microsoft.com/library/ms174937.aspx#bkmk_fixed).
3. Ponowne uruchomienie wystąpienia tabelarycznym hello programu hello usługi Analysis Services.

Aby uzyskać więcej informacji, zobacz hello **punkty końcowe maszyny wirtualnej i porty zapory** części tego dokumentu.

## <a name="virtual-machine-endpoints-and-firewall-ports"></a>Punkty końcowe maszyny wirtualnej i porty zapory
Ta sekcja zawiera podsumowanie tooopen toocreate i porty punktów końcowych programu Microsoft Azure maszyny wirtualnej w hello zapór maszyny wirtualnej. Witaj Poniższa tabela zawiera podsumowanie hello **TCP** porty punktów końcowych toocreate i hello tooopen portów w zaporze maszyn wirtualnych hello.

* Jeśli korzystasz z jednej maszyny Wirtualnej i hello poniższych dwóch elementów są spełnione, nie trzeba toocreate punktów końcowych z maszyny Wirtualnej i nie trzeba tooopen hello portów w zaporze hello na powitania maszyny Wirtualnej.
  
  * Zdalnie nie połączyć toohello funkcji programu SQL Server na powitania maszyny Wirtualnej. Ustanawianie połączeń usług pulpitu zdalnego toohello maszyny Wirtualnej i uzyskiwania dostępu do funkcji programu SQL Server hello lokalnie na powitania maszyny Wirtualnej nie jest uważana za funkcji programu SQL Server toohello połączenia zdalnego.
  * Nie dołączaj hello wirtualna tooan lokalnej domeny za pośrednictwem sieci wirtualnej platformy Azure lub innego rozwiązania tunelowania sieci VPN.
* Jeśli maszyna wirtualna hello nie jest tooa przyłączone do domeny, ale ma tooremotely połączenie toohello funkcji programu SQL Server na maszynie Wirtualnej:
  
  * Hello Otwieranie portów w zaporze hello na powitania maszyny Wirtualnej.
  * Tworzenie maszyny wirtualnej punktów końcowych hello zauważyć portów (*).
* Jeśli maszyna wirtualna hello jest tooa przyłączone do domeny przy użyciu tunelu VPN, takie jak sieci wirtualnych Azure, hello punkty końcowe nie są wymagane. Jednak Otwórz hello portów w zaporze hello na powitania maszyny Wirtualnej.
  
  | Port | Typ | Opis |
  | --- | --- | --- |
  | **80** |TCP |Serwer raportów dostępu zdalnego (*). |
  | **1433** |TCP |SQL Server Management Studio (*). |
  | **1434** |UDP |SQL Server Browser. Jest to niezbędne, gdy hello maszyny Wirtualnej w ramach tooa przyłączone do domeny. |
  | **2382** |TCP |SQL Server Browser. |
  | **2383** |TCP |Wystąpienie programu SQL Server Analysis Services domyślne i nazwane wystąpienia klastra. |
  | **Zdefiniowane przez użytkownika** |TCP |Utwórz statycznych Analysis Services o nazwie wystąpienia port numer portu, którego możesz wybrać, a następnie odblokuj hello numer portu w zaporze hello. |

Aby uzyskać więcej informacji na temat tworzenia punktów końcowych zobacz następujące hello:

* Utwórz punkty końcowe:[jak tooSet się punkty końcowe tooa maszyny wirtualnej](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
* Program SQL Server: Zobacz sekcję "Cała konfiguracja kroki tooconnect toohello maszyny wirtualnej używanie programu SQL Server Management Studio" hello [inicjowania obsługi maszyny wirtualnej programu SQL Server na platformie Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).

Witaj poniższym diagramie przedstawiono hello tooopen portów w hello toofeatures dostępu zdalnego tooallow zapory maszyny Wirtualnej i składniki na powitania maszyny Wirtualnej.

![porty tooopen analizy biznesowej aplikacji w maszynach wirtualnych platformy Azure](./media/virtual-machines-windows-classic-ps-sql-bi/IC654385.gif)

## <a name="resources"></a>Zasoby
* Przejrzyj zasady udzielania pomocy technicznej hello oprogramowania serwera firmy Microsoft używane w środowisku maszyny wirtualnej Azure hello. Witaj kolejny temat zawiera podsumowanie obsługę funkcji, takich jak funkcja BitLocker, klaster trybu Failover i równoważenia obciążenia sieciowego. [Obsługa oprogramowania serwera firmy Microsoft dla maszyn wirtualnych platformy Azure](http://support.microsoft.com/kb/2721672).
* [Program SQL Server na maszynach wirtualnych platformy Azure — omówienie](../sql/virtual-machines-windows-sql-server-iaas-overview.md)
* [Virtual Machines](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Inicjowanie obsługi administracyjnej maszyny wirtualnej programu SQL Server na platformie Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md)
* [Jak tooAttach tooa dysku danych maszyny wirtualnej](../classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Migrowanie tooSQL bazy danych serwera na maszynie Wirtualnej platformy Azure](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)
* [Określić hello tryb serwera z wystąpieniem usług Analysis](https://msdn.microsoft.com/library/gg471594.aspx)
* [Modelowania wielowymiarowego (samouczek Adventure Works)](https://technet.microsoft.com/library/ms170208.aspx)
* [Centrum dokumentacji platformy Azure](https://azure.microsoft.com/documentation/)
* [Przy użyciu usługi Power BI w środowisku hybrydowym](https://msdn.microsoft.com/library/dn798994.aspx)

> [!NOTE]
> [Prześlij opinię i informacje kontaktowe za pomocą programu Microsoft SQL Server Connect](https://connect.microsoft.com/SQLServer/Feedback)

### <a name="community-content"></a>Zawartość społeczności
* [Zarządzanie bazą danych Azure SQL przy użyciu programu PowerShell](http://blogs.msdn.com/b/windowsazure/archive/2013/02/07/windows-azure-sql-database-management-with-powershell.aspx)

