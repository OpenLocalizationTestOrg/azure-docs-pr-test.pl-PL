---
title: aaaProvision maszyny wirtualnej programu SQL Server | Dokumentacja firmy Microsoft
description: "Tworzenie i łączenie tooa maszyny wirtualnej programu SQL Server na platformie Azure przy użyciu hello portalu. W tym samouczku używana hello tryb usługi Resource Manager."
services: virtual-machines-windows
documentationcenter: na
author: rothja
editor: 
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 1aff691f-a40a-4de2-b6a0-def1384e086e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: jroth
experimental_id: a641df96-f27d-40
ms.openlocfilehash: aaad422d6ed47f5ca00b1ef484ac270a58e24f99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-in-hello-azure-portal"></a>Aprowizowanie maszyny wirtualnej programu SQL Server w hello portalu Azure
> [!div class="op_single_selector"]
> * [Portal](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
> 
> 

W tym samouczku end-to-end przedstawiono, jak toouse hello tooprovision Azure Portal maszynę wirtualną z programem SQL Server.

Witaj galerii Azure maszyny wirtualnej (VM) zawiera kilka obrazów, które zawierają programu Microsoft SQL Server. Za pomocą kilku kliknięć można wybrać jeden z obrazów maszyny Wirtualnej SQL z galerii hello powitalne i udostępnić go w środowisku platformy Azure.

W tym samouczku zostaną wykonane następujące czynności:

* [Wybierz obraz maszyny Wirtualnej SQL z galerii hello](#select-a-sql-vm-image-from-the-gallery)
* [Konfigurowanie i tworzenie hello maszyny Wirtualnej](#configure-the-vm)
* [Otwórz hello maszyny Wirtualnej przy użyciu pulpitu zdalnego](#open-the-vm-with-remote-desktop)
* [Połącz tooSQL serwera zdalnie](#connect-to-sql-server-remotely)

## <a name="select-a-sql-vm-image-from-hello-gallery"></a>Wybierz obraz maszyny Wirtualnej SQL z galerii hello
1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com) przy użyciu swojego konta.

   > [!NOTE]
   > Jeśli nie masz konta platformy Azure, odwiedź stronę [bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).

2. Na powitania portalu Azure, kliknij przycisk **nowy**. Hello portal otwiera hello **nowy** bloku. zasoby maszyny Wirtualnej programu SQL Server Hello są hello **obliczeniowe** grupy hello Marketplace.
3. W hello **nowy** bloku, kliknij przycisk **obliczeniowe** , a następnie kliknij przycisk **zobaczyć wszystkie**.
4. W hello **filtru** tekstu wpisz programu SQL Server i naciśnij klawisz ENTER hello.

   ![Blok Azure Virtual Machines](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-blade2.png)

5. Przejrzyj hello dostępnych obrazów programu SQL Server. Każdy obraz identyfikuje wersję programu SQL Server i system operacyjny. 
6. Wybierz obraz powitania dla programu SQL Server 2016 z dodatkiem SP1 Developer w systemie Windows Server 2016.

   > [!TIP]
   > Hello Developer edition jest używany w tym samouczku, ponieważ jest to oferujący wszystkie funkcje wydanie programu SQL Server, który jest bezpłatna dla rozwoju testowania. Płacisz tylko za koszt hello hello maszyny Wirtualnej.

   > [!NOTE]
   > Obrazów maszyn wirtualnych SQL dołączać hello koszty licencjonowania programu SQL Server do hello na minutę cen hello maszyny Wirtualnej tworzonej (z wyjątkiem hello wersje dla deweloperów i Express). Z programu SQL Server Developer można korzystać bezpłatnie w środowiskach tworzenia i testowania (nie produkcyjnych). Z programu SQL Express można korzystać bezpłatnie na potrzeby obsługi małych obciążeń (mniej niż 1 GB pamięci i mniej niż 10 GB magazynu).
   > Istnieje inny opcja toobring-your właścicielem licencji (BYOL) i płatności tylko w przypadku hello maszyny Wirtualnej. Nazwy tych obrazów mają prefiks {BYOL}. Aby uzyskać więcej informacji na temat tych opcji, zobacz [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Wskazówki dotyczące cen maszyn wirtualnych platformy Azure z programem SQL Server).

7. W obszarze **Wybierz model wdrożenia** sprawdź, czy pozycja **Resource Manager** została zaznaczona. Menedżer zasobów jest hello zalecane modelu wdrażania nowych maszyn wirtualnych. Kliknij przycisk **Utwórz**.

    ![Tworzenie maszyny wirtualnej SQL przy użyciu usługi Resource Manager](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-sql-deployment-model.png)

## <a name="configure-hello-vm"></a>Skonfiguruj hello maszyny Wirtualnej
Do konfigurowania maszyny wirtualnej programu SQL Server służy pięć bloków.

| Krok | Opis |
| --- | --- |
| **Podstawy** |[Konfigurowanie ustawień podstawowych](#1-configure-basic-settings) |
| **Rozmiar** |[Wybieranie rozmiaru maszyny wirtualnej](#2-choose-virtual-machine-size) |
| **Ustawienia** |[Konfigurowanie funkcji opcjonalnych](#3-configure-optional-features) |
| **Ustawienia programu SQL Server** |[Konfigurowanie ustawień programu SQL Server](#4-configure-sql-server-settings) |
| **Podsumowanie** |[Przejrzyj hello podsumowania](#5-review-the-summary) |

## <a name="1-configure-basic-settings"></a>1. Konfigurowanie ustawień podstawowych
Na powitania **podstawy** bloku, podaj hello następujących informacji:

* Wprowadź unikatową nazwę maszyny wirtualnej w polu **Nazwa**.
* Określ **nazwy użytkownika** hello konta administratora lokalnego na powitania maszyny Wirtualnej. To konto jest także dodawane toohello programu SQL Server **sysadmin** stałej roli serwera.
* Podaj silne hasło w polu **Hasło**.
* Jeśli masz wiele subskrypcji, sprawdź poprawność dla subskrypcji hello hello nowej maszyny Wirtualnej.
* W hello **grupy zasobów** wpisz nazwę nowej grupy zasobów. Alternatywnie toouse istniejącą grupę zasobów kliknij **Użyj istniejącego**. Grupa zasobów to kolekcja powiązanych zasobów platformy Azure (maszyny wirtualne, konta magazynu, sieci wirtualne itp.).
  
  > [!NOTE]
  > Nowa grupa zasobów jest przydatna, jeśli tylko testujesz lub poznajesz wdrożenia programu SQL Server na platformie Azure. Po zakończeniu testu Usuń hello zasobów grupy tooautomatically delete hello maszyny Wirtualnej i wszystkie zasoby skojarzone z danej grupy zasobów. Aby uzyskać więcej informacji na temat grup zasobów, zobacz [Omówienie usługi Azure Resource Manager](../../../azure-resource-manager/resource-group-overview.md).
  > 
  > 
* Wybierz ustawienie **Lokalizacja** dla tego wdrożenia.
* Kliknij przycisk **OK** toosave hello ustawienia.
  
    ![Blok podstawowych ustawień SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-basic.png)

## <a name="2-choose-virtual-machine-size"></a>2. Wybieranie rozmiaru maszyny wirtualnej
Na powitania **rozmiar** kroku, wybierz rozmiar maszyny wirtualnej w hello **wybierz rozmiar** bloku. Witaj bloku początkowo wyświetlane są rozmiary zalecane zgodnie na powitania wybranego obrazu.

> [!IMPORTANT]
> Witaj szacowany miesięczny koszt wyświetlany na powitania **wybierz rozmiar** bloku nie obejmuje koszty licencjonowania programu SQL Server. Ten szacowany koszt miesięcznych jest koszt hello hello samej maszyny Wirtualnej. Hello Express Developer wersje programu SQL Server jest szacowany koszt całkowity hello. W innych wersjach, zobacz hello [cennik maszyn wirtualnych Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) i Wybieranie sieci docelowej wersji programu SQL Server. Zobacz też hello [cennik wskazówki dotyczące maszyn wirtualnych programu SQL Server Azure](virtual-machines-windows-sql-server-pricing-guidance.md).

![Opcje rozmiaru maszyny wirtualnej SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-choose-a-size.png)

W przypadku obciążeń produkcyjnych zalecane jest wybranie rozmiaru maszyny wirtualnej, która obsługuje [usługę Premium Storage](../../../storage/storage-premium-storage.md). Jeśli nie potrzebujesz tego poziomu wydajności, użyj hello **Wyświetl wszystkie** przycisku, który zawiera wszystkie opcje rozmiaru maszyny. Na przykład możesz użyć mniejszego rozmiaru maszyny dla wdrożenia lub środowiska testowego.

> [!NOTE]
> Aby uzyskać więcej informacji na temat rozmiarów maszyny wirtualnej, zobacz artykuł [Sizes for virtual machines](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Rozmiary maszyn wirtualnych). Aby zapoznać się z zagadnieniami związanymi z rozmiarami maszyn wirtualnych programu SQL Server, zobacz [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md) (Najlepsze rozwiązania umożliwiające zwiększenie wydajności programu SQL Server w usłudze Azure Virtual Machines).

Wybierz rozmiar maszyny wirtualnej, a następnie kliknij pozycję **Wybierz**.

## <a name="3-configure-optional-features"></a>3. Konfigurowanie funkcji opcjonalnych
Na powitania **ustawienia** bloku, skonfiguruj magazyn Azure, sieci i monitorowania hello maszyny wirtualnej.

* W obszarze **Usługa Storage** określ wartość **Typ dysku** jako standardowy lub Premium (SSD). Magazyn w warstwie Premium jest zalecany w przypadku obciążeń produkcyjnych.

> [!NOTE]
> Wybranie opcji Premium (SSD) dla rozmiaru maszyny, która nie obsługuje usługi Premium Storage, powoduje automatyczną zmianę rozmiaru maszyny.  
> 
> 

* W obszarze **konta magazynu**, możesz zaakceptować nazwę konta automatycznie aprowizowanego magazynu hello. Możesz również kliknąć **konta magazynu** toochoose istniejące konto i skonfigurować typ konta magazynu hello. Domyślnie platforma Azure tworzy nowe konto magazynu z magazynem lokalnie nadmiarowym. Aby uzyskać więcej informacji na temat opcji magazynu, zobacz [Replikacja usługi Azure Storage](../../../storage/storage-redundancy.md).
* W obszarze **sieci**, może akceptować wartości hello wypełnione automatycznie. Możesz również kliknąć poszczególne funkcje toomanually skonfigurować hello **sieci wirtualnej**, **podsieci**, **publicznego adresu IP**, i **sieciowej grupy zabezpieczeń**. Do celów tego samouczka hello Zachowaj wartości domyślne hello.
* Azure umożliwia **monitorowanie** domyślnie z hello tego samego konta magazynu wyznaczonego dla hello maszyny Wirtualnej. Możesz zmienić te ustawienia tutaj.
* W obszarze **Zestaw dostępności** określ zestaw dostępności. Do celów tego samouczka hello, można wybrać **Brak**. Tooset się zawsze włączonych grup dostępności SQL, należy skonfigurować hello dostępności tooavoid odtwarzanie hello maszyny wirtualnej.  Aby uzyskać więcej informacji, zobacz [hello Zarządzaj dostępność maszyn wirtualnych](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Po zakończeniu konfigurowania tych ustawień kliknij pozycję **OK**.

## <a name="4-configure-sql-server-settings"></a>4. Konfigurowanie ustawień programu SQL Server
Na powitania **ustawienia programu SQL Server** bloku, skonfiguruj określone ustawienia i optymalizacje dla programu SQL Server. Ustawienia Hello, które można skonfigurować dla programu SQL Server obejmują hello następujące ustawienia.

| Ustawienie |
| --- |
| [Łączność](#connectivity) |
| [Uwierzytelnianie](#authentication) |
| [Konfiguracja usługi Storage](#storage-configuration) |
| [Automatyczne stosowanie poprawek](#automated-patching) |
| [Automatyczne kopie zapasowe](#automated-backup) |
| [Integracja z usługą Azure Key Vault](#azure-key-vault-integration) |
| [Usługi języka R](#r-services) |

### <a name="connectivity"></a>Łączność
W obszarze **łączność z serwerem SQL**, określ typ hello dostępu ma toohello wystąpienia programu SQL Server na tej maszynie Wirtualnej. Do celów tego samouczka hello, wybierz **publiczne (internet)** tooallow tooSQL połączenia serwera z komputerów lub usług na hello internet. W przypadku wybrania tej opcji Azure automatycznie skonfiguruje hello zapory i hello sieci zabezpieczeń grupy tooallow ruch na porcie 1433.  

![Opcje łączności z serwerem SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-connectivity-alt.png)

tooconnect tooSQL serwera za pomocą hello internet, należy także włączyć uwierzytelnianie programu SQL Server, który jest opisany w następnej sekcji hello.

> [!NOTE]
> Jego jest możliwe tooadd więcej ograniczeń dla tooyour komunikacji sieciowej hello maszyny Wirtualnej programu SQL Server. Po utworzeniu hello maszyny Wirtualnej, można dodać więcej ograniczeń przez hello edycji grupy zabezpieczeń sieci. Aby uzyskać więcej informacji, zobacz [What is a Network Security Group (NSG)?](../../../virtual-network/virtual-networks-nsg.md) (Co to jest sieciowa grupa zabezpieczeń?).
> 
> 

Jeśli wolisz toonot Włącz połączenia toohello aparatu bazy danych za pośrednictwem hello internet, wybierz jedną z hello następujące opcje:

* **Lokalne (tylko wewnątrz maszyny Wirtualnej)** tooallow połączeń tooSQL Server tylko z wewnątrz hello maszyny Wirtualnej.
* **Prywatne (wewnątrz sieci wirtualnej)** tooallow tooSQL połączenia serwera z komputerów lub usług w hello tej samej sieci wirtualnej.

> [!NOTE]
> Witaj obraz maszyny wirtualnej dla programu SQL Server Express edition nie obsługuje automatycznie protokołu hello TCP/IP. Dotyczy to nawet hello łączności publicznej i prywatnej opcje. Dla wersji Express edition, należy użyć programu SQL Server Configuration Manager za[ręcznie włączyć protokół hello TCP/IP](#configure-sql-server-to-listen-on-the-tcp-protocol) po utworzeniu hello maszyny Wirtualnej.
> 
> 

Ogólnie rzecz biorąc zwiększyć bezpieczeństwo, wybierając łączność najbardziej restrykcyjne hello danym scenariuszu. Jednak wszystkie opcje hello można zabezpieczyć przy użyciu reguł sieciowej grupy zabezpieczeń i uwierzytelniania SQL/Windows.

**Port** domyślne too1433. Możesz określić inny numer portu.
Aby uzyskać więcej informacji, zobacz [połączyć tooa programu SQL Server Virtual Machine (Resource Manager) | Microsoft Azure](virtual-machines-windows-sql-connect.md).

### <a name="authentication"></a>Authentication
Jeśli wymagasz uwierzytelniania programu SQL Server, kliknij pozycję **Włącz** w obszarze **Uwierzytelnianie SQL**.

![Uwierzytelnianie programu SQL Server](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-authentication.png)

> [!NOTE]
> Jeśli planujesz tooaccess programu SQL Server za pośrednictwem hello internet (to znaczy hello opcja łączności publicznej), należy włączyć uwierzytelnianie SQL, w tym miejscu. Toohello dostępu publicznego programu SQL Server wymaga użycia hello uwierzytelniania SQL.
> 
> 

Jeśli włączasz opcję uwierzytelniania programu SQL Server, podaj informacje w polach **Nazwa logowania** i **Hasło**. Ta nazwa użytkownika jest skonfigurowana jako identyfikator logowania uwierzytelniania programu SQL Server i członek hello **sysadmin** stałej roli serwera. Aby uzyskać więcej informacji na temat trybów uwierzytelniana, zobacz artykuł [Choose an Authentication Mode](http://msdn.microsoft.com/library/ms144284.aspx) (Wybieranie trybu uwierzytelniania).

Jeśli uwierzytelnianie programu SQL Server nie jest włączona, można użyć konta administratora lokalnego hello w wystąpieniu serwera SQL hello wirtualna tooconnect toohello.

### <a name="storage-configuration"></a>Konfiguracja usługi Storage
Kliknij przycisk **konfiguracji magazynu** toospecify hello przestrzeni dyskowej jest potrzebne.

![Konfiguracja usługi SQL Storage](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-storage.png)

> [!NOTE]
> Ta opcja jest niedostępna po wybraniu magazynu standardowego. Automatyczna optymalizacja magazynu jest dostępna tylko dla usługi Premium Storage.
> 
> 

Możesz określić wymagania dotyczące na przykład liczby operacji wejścia/wyjścia na sekundę (IOPs), przepustowości w MB/s i całkowitego rozmiaru magazynu. Skonfiguruj te wartości przy użyciu suwaków hello. Witaj portal automatycznie oblicza hello liczba dysków, na podstawie tych wymagań.

Domyślnie platforma Azure optymalizuje hello magazyn dla 5000 IOPs, 200 MB i 1 TB miejsca do magazynowania. Możesz zmienić te ustawienia magazynu zależnie od obciążenia. W obszarze **Storage zoptymalizowana dla**, wybierz jedną z hello następujące opcje:

* **Ogólne** jest ustawienie domyślne hello i obsługujące większość obciążeń.
* **Transakcyjne** przetwarzania optymalizuje hello magazynowania dla obciążeń OLTP tradycyjne bazy danych.
* **Magazynowanie danych** optymalizuje magazyn hello analizą i raportami obciążeń.

> [!NOTE]
> Witaj górne limity na powitania suwaki zależy od użytkownika wybranego rozmiaru maszyny wirtualnej.
> 
> 

### <a name="automated-patching"></a>Automatyczne stosowanie poprawek
Opcja **Automatyczne stosowanie poprawek** jest domyślnie włączona. Automatyczne stosowanie poprawek umożliwia Azure tooautomatically poprawki programu SQL Server i hello systemu operacyjnego. Określ dzień tygodnia hello, czas i czas trwania okna obsługi. Platforma Azure stosuje poprawki w tym oknie obsługi. Harmonogram okna obsługi Hello używa ustawień regionalnych wirtualna hello raz. Jeśli nie chcesz, aby Azure tooautomatically poprawki programu SQL Server i hello systemu operacyjnego, kliknij przycisk **wyłączyć**.  

![Automatyczne stosowanie poprawek SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-patching.png)

Aby uzyskać więcej informacji, zobacz [Automated Patching for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-patching.md) (Automatyczne stosowanie poprawek programu SQL Server w usłudze Azure Virtual Machines).

### <a name="automated-backup"></a>Automatyczne kopie zapasowe
Automatyczną obsługę kopii zapasowych baz danych możesz włączyć dla wszystkich baz danych w obszarze **Automatyczne tworzenie kopii zapasowych**. Opcja Automatyczne kopie zapasowe jest domyślnie wyłączona.

Po włączeniu automatycznej kopii zapasowej SQL, można skonfigurować hello następujące ustawienia:

* Okres przechowywania (dni) kopii zapasowych
* Toouse konta magazynu kopii zapasowych
* Opcja szyfrowania i hasło dla kopii zapasowych
* Bazy danych systemu tworzenia kopii zapasowych
* Konfigurowanie harmonogramu tworzenia kopii zapasowych

kopii zapasowej, kliknij przycisk tooencrypt hello **włączyć**. Następnie określ hello **hasło**. Azure tworzy certyfikat tooencrypt hello tworzenia kopii zapasowych i używa hello określony tooprotect hasło tego certyfikatu.

![Automatyczna usługa Backup SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-autobackup2.png)

 Aby uzyskać więcej informacji, zobacz [Automated Backup for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md) (Automatyczne tworzenie kopii zapasowych dla programu SQL Server w usłudze Azure Virtual Machines).

### <a name="azure-key-vault-integration"></a>Integracja magazynu kluczy Azure
klucze tajne zabezpieczeń toostore na platformie Azure dla celów szyfrowania, kliknij przycisk **Integracja magazynu kluczy Azure** i kliknij przycisk **włączyć**.

![Integracja magazynu kluczy Usług SQL Azure](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-akv.png)

Witaj poniższej tabeli wymieniono hello parametry wymagane tooconfigure integracji magazynu kluczy Azure.

| PARAMETR | OPIS | PRZYKŁAD |
| --- | --- | --- |
| **Adres URL magazynu kluczy** |Lokalizacja Hello hello magazynu kluczy. |https://contosokeyvault.vault.azure.net/ |
| **Nazwa główna** |Nazwa główna usługi Azure Active Directory. Ta nazwa jest również hello tooas określony identyfikator klienta. |fde2b411-33d5-4e11-af04eb07b669ccf2 |
| **Główny klucz tajny** |Główny klucz tajny usługi Azure Active Directory. Ten klucz tajny jest również hello tooas określonego klucza tajnego klienta. |9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM= |
| **Nazwa poświadczenia** |**Nazwa poświadczenia**: integracja powoduje utworzenie poświadczenia w programie SQL Server, dzięki czemu hello wirtualna toohave dostępu toohello klucza magazynu. Wybierz nazwę tego poświadczenia. |moje_poświadczenie_1 |

Aby uzyskać więcej informacji, zobacz [Configure Azure Key Vault Integration for SQL Server on Azure VMs](virtual-machines-windows-ps-sql-keyvault.md) (Konfigurowanie integracji usługi Azure Key Vault dla programu SQL Server na maszynach wirtualnych Azure).

Po zakończeniu konfigurowania tych ustawień programu SQL Server kliknij pozycję **OK**.

### <a name="r-services"></a>Usługi języka R
Można włączyć [usługi języka R programu SQL Server](https://msdn.microsoft.com/library/mt604845.aspx). SQL Server R Services umożliwia toouse zaawansowane analizy w usłudze SQL Server 2016. Kliknij przycisk **włączyć** na powitania **ustawienia programu SQL Server** bloku.

![Włączanie usług języka R programu SQL Server](./media/virtual-machines-windows-portal-sql-server-provision/azure-vm-sql-server-r-services.png)


## <a name="5-review-hello-summary"></a>5. Przejrzyj hello podsumowania
Na powitania **podsumowania** bloku, przejrzyj hello podsumowania i kliknij przycisk **OK** toocreate programu SQL Server, grupy zasobów i zasoby określone dla tej maszyny Wirtualnej.

Można monitorować wdrożenia hello z portalu hello azure. Witaj **powiadomienia** przycisk u góry hello hello ekranu przedstawia podstawowy stan wdrożenia hello.

> [!NOTE]
> tooprovide o pomysł na wdrożenie czasu, regionu wschodnie stany USA toohello maszyny Wirtualnej SQL I wdrażane z ustawieniami domyślnymi. Tego wdrożenia testowego trwało łącznie 26 minut toocomplete. Wdrażanie może jednak trwać krócej lub dłużej zależnie od regionu i wybranych ustawień.
> 
> 

## <a name="open-hello-vm-with-remote-desktop"></a>Otwórz hello maszyny Wirtualnej przy użyciu pulpitu zdalnego
Użyj hello następującej maszyny wirtualnej toohello tooconnect czynności przy użyciu pulpitu zdalnego:

1. Po powitalne utworzeniu maszyny Wirtualnej Azure ikona hello hello maszyny Wirtualnej jest wyświetlana na pulpicie nawigacyjnym platformy Azure. Możesz również znaleźć ją, przeglądając istniejące maszyny wirtualne. Kliknij maszynę wirtualną SQL. W bloku **Maszyna wirtualna** zostaną wyświetlone szczegóły maszyny wirtualnej.
2. U góry hello hello **maszyny wirtualnej** bloku, kliknij przycisk **Connect**.
3. Witaj przeglądarka pobierze plik RDP dla hello maszyny Wirtualnej. Witaj Otwórz plik RDP.
    ![TooSQL pulpitu zdalnego maszyny Wirtualnej](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-remote-desktop.png)
4. Hello Podłączanie pulpitu zdalnego powiadomi tego hello się, że nie można zidentyfikować wydawcy tego połączenia zdalnego. Kliknij przycisk **Connect** toocontinue.
5. W hello **zabezpieczenia systemu Windows** okna dialogowego, kliknij przycisk **Użyj innego konta**.
6. Dla **nazwy użytkownika** typu  **\<nazwa użytkownika >**, gdzie <user name> jest nazwą użytkownika hello określone podczas konfigurowania hello maszyny Wirtualnej. Masz tooadd początkowy ukośnik odwrotny przed nazwą hello.
7. Typ hello **hasło** wcześniej skonfigurowane dla tej maszyny Wirtualnej, a następnie kliknij przycisk **OK** tooconnect.
8. Jeśli inny **Podłączanie pulpitu zdalnego** okna dialogowego pyta, czy tooconnect, kliknij przycisk **tak**.

Po podłączeniu maszyny wirtualnej programu SQL Server toohello można uruchomić programu SQL Server Management Studio i Połącz z uwierzytelnianiem systemu Windows przy użyciu poświadczeń konta administratora lokalnego. Włączenie uwierzytelniania programu SQL Server można również połączyć przy użyciu hello logowania SQL i hasła skonfigurowanego podczas inicjowania obsługi uwierzytelniania SQL.

Maszyna toohello dostępu umożliwia toodirectly zmiany maszyny i ustawień programu SQL Server, w zależności od wymagań. Na przykład można skonfigurować ustawienia zapory hello, lub zmień ustawienia konfiguracji serwera SQL.

## <a name="connect-toosql-server-remotely"></a>Połącz tooSQL serwera zdalnie
W tym samouczku wybrano **publicznego** dostępu dla maszyny wirtualnej hello i **uwierzytelniania programu SQL Server**. Te ustawienia automatycznie skonfigurowana hello maszyny wirtualnej tooallow programu SQL Server połączenia za pomocą dowolnego klienta za pośrednictwem hello Internetu (zakładając, że mają one hello poprawny identyfikator logowania SQL).

> [!NOTE]
> Jeśli nie wybrano publicznego podczas inicjowania obsługi, a następnie dodatkowe kroki są wymagane tooaccess wystąpienia programu SQL Server za pośrednictwem hello internet. Aby uzyskać więcej informacji, zobacz [połączyć tooa maszyny wirtualnej programu SQL Server](virtual-machines-windows-sql-connect.md).
> 
> 

Witaj następujące sekcje pokazują, jak wystąpienie programu SQL Server tooyour tooconnect na maszynie Wirtualnej z innego komputera za pośrednictwem hello internet.

> [!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]
> 
> 

## <a name="next-steps"></a>Następne kroki
Aby uzyskać inne informacje o korzystaniu z programu SQL Server na platformie Azure, zobacz [programu SQL Server na maszynach wirtualnych Azure](virtual-machines-windows-sql-server-iaas-overview.md) i hello [— często zadawane pytania](virtual-machines-windows-sql-server-iaas-faq.md).

Film poglądowy dotyczący programu SQL Server na maszynach wirtualnych platformy Azure, obejrzyj [maszyny Wirtualnej platformy Azure jest najlepszą platformą hello SQL Server 2016](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016).

[Eksploruj hello ścieżka szkoleniowa dotycząca](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) dla programu SQL Server na maszynach wirtualnych Azure.

