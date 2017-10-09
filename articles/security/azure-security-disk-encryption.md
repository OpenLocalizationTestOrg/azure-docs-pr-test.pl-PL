---
title: "Szyfrowanie dysków systemu Windows i maszyn wirtualnych systemu Linux IaaS aaaAzure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie programu Microsoft Azure dysku szyfrowanie dla systemu Windows i maszyn wirtualnych systemu Linux IaaS."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: d3fac8bb-4829-405e-8701-fa7229fb1725
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: kakhan
ms.openlocfilehash: b685abdcc908e66d2352ec5ac2d9996aa75af1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a>Szyfrowanie dysków Azure dla systemu Windows i maszyn wirtualnych systemu Linux IaaS
Microsoft Azure jest silnie zatwierdzone tooensuring prywatności danych suwerenności danych i umożliwia toocontrol platformy Azure hostowanej danych za pomocą wielu zaawansowanych technologii tooencrypt, sterowania i zarządzania kluczami szyfrowania, inspekcji i kontroli dostępu do danych. Zapewnia to użytkownikom Azure hello elastyczność toochoose hello rozwiązania, która najlepiej spełnia ich potrzeb biznesowych. W tym dokumencie, możemy przedstawiono nowe rozwiązanie technologii tooa "Szyfrowania dysków Azure dla systemu Windows i Linux IaaS VM" toohelp ochrony i chronić Twoje toomeet danych Twojej organizacji zobowiązań zabezpieczeń i zgodności. dokument Hello znajdują się szczegółowe wskazówki dotyczące jak toouse hello Azure dysku szyfrowania funkcje takie jak hello obsługiwane scenariusze i hello środowiska użytkownika.

> [!NOTE]
> Zastosowanie niektórych zaleceń zamieszczonych może zwiększyć danych, sieci i użycia zasobów obliczeniowych, co powoduje dodatkowych kosztów licencji lub subskrypcji.

## <a name="overview"></a>Omówienie
Szyfrowanie dysków Azure jest nową możliwość, która pomaga szyfrowania dysków maszyny wirtualnej systemu Windows i Linux IaaS. Szyfrowanie dysków Azure korzysta z branżowymi hello [funkcji BitLocker](https://technet.microsoft.com/library/cc732774.aspx) funkcji systemu Windows i hello [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) funkcji szyfrowania woluminów tooprovide Linux hello systemu operacyjnego i dysków z danymi hello. rozwiązanie Hello jest zintegrowany z [usługi Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp sterowania i zarządzania hello szyfrowanie dysków kluczy i kluczy tajnych w magazynie kluczy subskrypcji. rozwiązanie Hello gwarantuje również, że wszystkie dane na powitania dysków maszyny wirtualnej są szyfrowane, gdy w magazynie Azure.

Szyfrowanie dysków Azure dla systemu Windows i maszyn wirtualnych systemu Linux IaaS, jest teraz w **ogólnej dostępności** we wszystkich regionach publicznej platformy Azure i regiony AzureGov standardowe maszyn wirtualnych i maszyn wirtualnych z magazyn w warstwie premium.

### <a name="encryption-scenarios"></a>Scenariusze szyfrowania
Witaj rozwiązania szyfrowania dysków Azure obsługuje hello następujących scenariuszy:

* Włącz szyfrowanie dla nowych maszyn wirtualnych IaaS utworzone na podstawie wstępnie zaszyfrowany dysk VHD i kluczy szyfrowania
* Włącz szyfrowanie dla nowych maszyn wirtualnych IaaS utworzone na podstawie hello obsługiwane galerii Azure obrazów
* Włącz szyfrowanie dla istniejących maszyn wirtualnych IaaS działające na platformie Azure
* Wyłącz szyfrowanie na maszynach wirtualnych IaaS systemu Windows
* Wyłącz szyfrowanie dysków danych dla maszyn wirtualnych systemu Linux IaaS
* Włącz szyfrowanie dysków zarządzanych maszyn wirtualnych
* Aktualizowanie ustawień szyfrowania istniejących zaszyfrowanych inne niż premium magazynu maszyny Wirtualnej
* Kopia zapasowa i przywracanie zaszyfrowanych maszyn wirtualnych, zaszyfrowane za pomocą klucza szyfrowania

rozwiązanie Hello obsługuje następujące scenariusze dla maszyn wirtualnych IaaS, jeśli są włączone w systemie Microsoft Azure hello:

* Integracja z usługi Azure Key Vault
* Maszyny wirtualne warstwy standardowa: [A, D DS, G, GS, F i itp szeregów maszyn wirtualnych IaaS](https://azure.microsoft.com/pricing/details/virtual-machines/)
* Włącz szyfrowania w systemach Windows i Linux maszyny wirtualne IaaS i dysków zarządzanych maszyn wirtualnych z hello obsługiwane galerii Azure obrazów
* Wyłącz szyfrowanie dysków systemu operacyjnego i danych dla maszyn wirtualnych IaaS systemu Windows i dysków zarządzanych maszyn wirtualnych
* Wyłącz szyfrowanie dysków danych dla maszyn wirtualnych systemu Linux IaaS i dysków zarządzanych maszyn wirtualnych
* Włącz szyfrowanie dla maszyn wirtualnych IaaS systemem kliencki system operacyjny Windows
* Włącz szyfrowanie dla woluminów przy użyciu ścieżki instalacji
* Włącz szyfrowanie dla maszyn wirtualnych systemu Linux skonfigurowany z dysku przy użyciu mdadm zastosowanie rozkładania (RAID)
* Włącz szyfrowanie dla maszyn wirtualnych systemu Linux przy użyciu LVM dla dysków z danymi
* Włącz szyfrowanie dla maszyn wirtualnych systemu Windows skonfigurowane z funkcją miejsca do magazynowania
* Aktualizowanie ustawień szyfrowania istniejących zaszyfrowanych inne niż premium magazynu maszyny Wirtualnej
* Wszystkie publiczne Azure i AzureGov regiony są obsługiwane.

rozwiązanie Hello nie obsługuje następujące scenariusze, funkcje i technologie hello:

* Maszyny wirtualne IaaS warstwa podstawowa
* Wyłączenie szyfrowania na dysku systemu operacyjnego dla maszyn wirtualnych systemu Linux IaaS
* Wyłączenie szyfrowania na dysku danych, jeśli hello dysku systemu operacyjnego jest szyfrowany dla maszyn wirtualnych systemu Linux Iaas
* Maszyny wirtualne IaaS, utworzony przy użyciu hello klasycznego metodę tworzenia maszyny Wirtualnej
* Włącz szyfrowanie dla systemu Windows i maszyn wirtualnych systemu Linux IaaS niestandardowych obrazów klienta nie jest obsługiwana. Włącz enccryption w systemie operacyjnym Linux LVM dysk nie jest obsługiwany obecnie. Ta obsługa rozpocznie się wkrótce.
* Integracja z lokalnej usługi zarządzania kluczami
* Usługa pliki Azure (udostępnionego systemu plików), sieciowego systemu plików (NFS), dynamiczne woluminy i maszyn wirtualnych systemu Windows, które są skonfigurowane przy użyciu systemów opartych na oprogramowaniu RAID
* Kopia zapasowa i przywracanie zaszyfrowanych maszyn wirtualnych, szyfrowane bez klucza szyfrowania.
* Zaktualizuj ustawienia szyfrowania istniejącego magazynu premium zaszyfrowanych maszyny Wirtualnej.

> [!NOTE]
> Kopia zapasowa i przywracanie zaszyfrowanych maszyn wirtualnych jest obsługiwana tylko dla maszyn wirtualnych, które są szyfrowane przy hello KEK konfiguracji. Nie jest obsługiwana na maszynach wirtualnych, które są szyfrowane bez KEK. KEK jest opcjonalnym parametrem, który włącza szyfrowanie maszyny Wirtualnej. Ta obsługa zostanie wkrótce uruchomiona.
> Aktualizuj ustawienia szyfrowania istniejący magazyn w warstwie premium zaszyfrowanych maszyny Wirtualnej nie są obsługiwane. Ta obsługa zostanie wkrótce uruchomiona.

### <a name="encryption-features"></a>Funkcji szyfrowania
Po włączeniu i wdrożeniu szyfrowania dysków Azure dla maszyn wirtualnych IaaS platformy Azure, hello następujące funkcje są włączone, w zależności od konfiguracji hello podane:

* Szyfrowanie woluminu rozruchowego hello systemu operacyjnego woluminu tooprotect hello magazynowane w magazynie
* Szyfrowanie danych woluminów tooprotect hello ilości danych przechowywanych w magazynie
* Wyłączenie szyfrowania na powitania systemu operacyjnego i danych dyski dla maszyn wirtualnych IaaS systemu Windows
* Wyłączenie szyfrowania danych hello dyski dla maszyn wirtualnych systemu Linux IaaS (tylko wtedy, gdy nie jest zaszyfrowany to dysk systemu operacyjnego)
* Ochrona hello szyfrowania kluczy i kluczy tajnych w magazynie kluczy subskrypcji
* Raportowanie stanu szyfrowania hello hello szyfrowane maszyn wirtualnych IaaS
* Usuwanie ustawień konfiguracji szyfrowania dysków z maszyn wirtualnych IaaS hello
* Kopia zapasowa i przywracanie zaszyfrowanych maszyn wirtualnych za pomocą usługi Kopia zapasowa Azure hello

> [!NOTE]
> Kopia zapasowa i przywracanie zaszyfrowanych maszyn wirtualnych jest obsługiwana tylko dla maszyn wirtualnych, które są szyfrowane przy hello KEK konfiguracji. Nie jest obsługiwana na maszynach wirtualnych, które są szyfrowane bez KEK. KEK jest opcjonalnym parametrem, który włącza szyfrowanie maszyny Wirtualnej.

Szyfrowanie dysków Azure maszyny Wirtualne IaaS dla systemu Windows i Linux rozwiązanie obejmuje:

* Witaj rozszerzenie szyfrowanie dysków dla systemu Windows.
* Witaj rozszerzenie szyfrowanie dysków dla systemu Linux.
* Witaj szyfrowanie dysków poleceń cmdlet programu PowerShell.
* Witaj szyfrowania dysku poleceń cmdlet Azure interfejsu wiersza polecenia (CLI).
* Witaj szablonów usługi Azure Resource Manager szyfrowania dysków.

Witaj rozwiązania szyfrowania dysków Azure jest obsługiwana na maszynach wirtualnych IaaS, które korzystają z systemu Windows lub systemu operacyjnego Linux. Aby uzyskać więcej informacji na temat hello obsługiwanych systemów operacyjnych, zobacz hello "wymagania wstępne" sekcji.

> [!NOTE]
> Brak bez dodatkowych opłat szyfrowanie dysków maszyny Wirtualnej przy użyciu szyfrowania dysków Azure.

### <a name="value-proposition"></a>Opis korzyści
Po zastosowaniu rozwiązania hello zarządzania szyfrowania dysków Azure mogą spełniać powitania po potrzeb biznesowych:

* Maszyny wirtualne IaaS są już zabezpieczone w stanie spoczynku, ponieważ mogą używać szyfrowania standardowych technologii tooaddress zabezpieczeń i zgodności wymagań organizacyjnych.
* Maszyny wirtualne IaaS rozruchu w obszarze klucze kontrolowane przez klienta i zasad, a można inspekcji ich użycia w magazynie kluczy.

### <a name="encryption-workflow"></a>Szyfrowanie przepływu pracy
Szyfrowanie dysków tooenable systemu Windows i maszyn wirtualnych systemu Linux, hello następujące:

1. Wybierz scenariusz szyfrowania spośród hello poprzedzających scenariuszy szyfrowania.
2. Włączyć tooenabling szyfrowanie dysków za pomocą szablonu Menedżera zasobów szyfrowania dysków Azure hello, poleceń cmdlet programu PowerShell lub polecenia interfejsu wiersza polecenia, a następnie określ hello konfiguracji szyfrowania.

   * W przypadku hello szyfrowane klienta scenariusz wirtualnego dysku twardego przekazać konto magazynu tooyour wirtualnego dysku twardego hello szyfrowane i hello magazynu kluczy tooyour materiału klucza szyfrowania. Następnie podaj tooenable konfiguracji szyfrowania hello na nowej maszyny Wirtualnej IaaS.
   * Nowe maszyny wirtualne, które są tworzone na podstawie hello Marketplace i istniejących maszyn wirtualnych, które zostały już uruchomione na platformie Azure Podaj tooenable konfiguracji szyfrowania hello na powitania maszyn wirtualnych IaaS.

3. Udziel dostępu toohello platformy Azure tooread hello klucza szyfrowania materiału (klucze szyfrowania funkcji BitLocker dla systemów Windows) i hasło dla systemu Linux z magazynu kluczy szyfrowania tooenable na powitania maszyn wirtualnych IaaS.

4. Podaj hello Azure Active Directory (Azure AD) aplikacji tożsamości toowrite hello szyfrowania tooyour materiału klucza magazynu kluczy. Dzięki temu włącza szyfrowanie na powitania maszyn wirtualnych IaaS dla scenariuszy hello wspomnianego w kroku 2.

5. Azure aktualizuje modelu usługi hello maszyny Wirtualnej przy użyciu szyfrowania i hello konfiguracji magazynu kluczy i konfiguruje zaszyfrowanych maszyny Wirtualnej.

 ![Ochrona przed złośliwym kodem zapewniana przez Microsoft na platformie Azure](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a>Odszyfrowywanie przepływu pracy
Szyfrowanie dysków toodisable dla maszyn wirtualnych IaaS, pełną hello następujące ogólne kroki:

1. Wybierz toodisable szyfrowania (odszyfrowywania) na uruchomionych maszyn wirtualnych IaaS na platformie Azure za pośrednictwem hello szablon Menedżera zasobów szyfrowania dysków Azure lub poleceń cmdlet programu PowerShell i określ hello odszyfrowywania konfiguracji.

 Ten krok powoduje wyłączenie szyfrowania woluminu danych systemu operacyjnego lub hello hello lub obu tych programów na powitania uruchamiania maszyny Wirtualnej systemu Windows IaaS. Jednakże jak wspomniano w poprzedniej sekcji hello, wyłączenie szyfrowania dysku systemu operacyjnego Linux nie jest obsługiwane. krok odszyfrowywania Hello jest dozwolone tylko w przypadku dysków z danymi na maszynach wirtualnych systemu Linux tak długo, jak hello dysk systemu operacyjnego nie jest zaszyfrowany.
2. Aktualizacje Azure hello modelu usług maszyny Wirtualnej, a hello IaaS maszyny Wirtualnej jest oznaczony jako odszyfrowany. zawartość Hello hello maszyny Wirtualnej nie są szyfrowane, gdy.

> [!NOTE]
> Operacja disable szyfrowania Hello nie powoduje usunięcia z magazynu i hello szyfrowania klucza materiału klucza (klucze szyfrowania funkcji BitLocker dla systemów Windows) lub hasło dla systemu Linux.
 > Wyłączenie szyfrowania dysku systemu operacyjnego Linux nie jest obsługiwane. krok odszyfrowywania Hello jest dozwolone tylko w przypadku dysków z danymi na maszynach wirtualnych systemu Linux.
Wyłączenie szyfrowania dysku danych dla systemu Linux nie jest obsługiwane, jeśli hello dysku systemu operacyjnego jest szyfrowany.

## <a name="prerequisites"></a>Wymagania wstępne
Przed włączeniem szyfrowania dysków Azure na maszynach wirtualnych Azure IaaS dla hello obsługiwane scenariusze, które zostały omówione w sekcji "Przegląd" hello, zobacz hello następujące wymagania wstępne:

* Zasoby toocreate prawidłowy aktywną subskrypcją platformy Azure musi mieć na platformie Azure w regionach hello obsługiwane.
* Szyfrowanie dysków Azure jest obsługiwana na powitania następujące wersje systemu Windows Server: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 i Windows Server 2016.
* Szyfrowanie dysków Azure jest obsługiwana w następujących wersjach klientów systemu Windows hello: Windows 10 i Windows 8 klienta.

> [!NOTE]
> Dla systemu Windows Server 2008 R2 musisz mieć zainstalowany przed włączeniem szyfrowania na platformie Azure programu .NET Framework 4.5. Można zainstalować z witryny Windows Update, instalując hello opcjonalną aktualizację programu Microsoft .NET Framework 4.5.2 dla systemów opartych na x64 systemu Windows Server 2008 R2 ([KB2901983](https://support.microsoft.com/kb/2901983)).

* Szyfrowanie dysków Azure jest obsługiwana na powitania po galerii Azure na podstawie dystrybucje systemu Linux serwera oraz wersje:

| Dystrybucja systemu Linux | Wersja | Typ woluminu obsługiwany w przypadku szyfrowania|
| --- | --- |--- |
| Ubuntu | 16.04 — CODZIENNIE LTS | Dysk systemu operacyjnego i danych |
| Ubuntu | 14.04.5-DAILY-LTS | Dysk systemu operacyjnego i danych |
| Ubuntu | 12.10 | Dysk z danymi |
| Ubuntu | 12.04 | Dysk z danymi |
| RHEL | 7.3 | Dysk systemu operacyjnego i danych |
| RHEL | 7.2 | Dysk systemu operacyjnego i danych |
| RHEL | 6.8 | Dysk systemu operacyjnego i danych |
| RHEL | 6.7 | Dysk z danymi |
| CentOS | 7.3 | Dysk systemu operacyjnego i danych |
| CentOS | 7.2n | Dysk systemu operacyjnego i danych |
| CentOS | 6.8 | Dysk systemu operacyjnego i danych |
| CentOS | 7.1 | Dysk z danymi |
| CentOS | 7.0 | Dysk z danymi |
| CentOS | 6.7 | Dysk z danymi |
| CentOS | 6.6 | Dysk z danymi |
| CentOS | 6.5 | Dysk z danymi |
| openSUSE | 13.2 | Dysk z danymi |
| SLES | 12 Z DODATKIEM SP1 | Dysk z danymi |
| SLES | 12 dodatku SP1 (Premium) | Dysk z danymi |
| SLES | HPC 12 | Dysk z danymi |
| SLES | 11-SP4 (Premium) | Dysk z danymi |
| SLES | 11 Z DODATKIEM SP4 | Dysk z danymi |

* Szyfrowanie dysków Azure wymaga, że magazyn kluczy i maszyny wirtualne znajdują się w hello sam region platformy Azure i subskrypcji.

> [!NOTE]
> Konfigurowanie zasobów hello w oddzielnych regionach powoduje to niepowodzenie w włączenie funkcji szyfrowania dysków Azure hello.

* tooset w górę i Konfigurowanie magazynu kluczy do szyfrowania dysków Azure, zobacz sekcję **ustawiony w górę i konfigurowania magazynu kluczy szyfrowania dysków Azure** w hello *wymagania wstępne* sekcji tego artykułu.
* tooset w górę i konfigurowania aplikacji usługi Azure AD w usłudze Azure Active directory szyfrowanie dysków Azure, zobacz sekcję **skonfigurowanie aplikacji hello Azure AD w usłudze Azure Active Directory** w hello *wymagania wstępne* w tym artykule.
* tooset w górę i skonfigurować zasady dostępu magazynu kluczy hello aplikacji hello Azure AD, zobacz sekcję **skonfigurować zasady dostępu magazynu kluczy hello aplikacji hello Azure AD** w hello *wymagania wstępne* sekcji w tym artykule.
* tooprepare wstępnie zaszyfrowanego dysku VHD systemu Windows, zobacz sekcję **przygotować wstępnie zaszyfrowanego dysku VHD systemu Windows** w hello *dodatku*.
* tooprepare wstępnie zaszyfrowanego dysku VHD systemu Linux, zobacz sekcję **przygotować wstępnie zaszyfrowanego dysku VHD systemu Linux** w hello *dodatku*.
* Hello platformy Azure wymaga dostępu toohello szyfrowania kluczy lub kluczy tajnych w toomake Twojego magazynu kluczy ich toohello dostępne maszyny wirtualnej, podczas rozruchu i odszyfrowuje hello wolumin maszyny wirtualnej systemu operacyjnego. toogrant uprawnienia tooAzure platformy, zestaw hello **EnabledForDiskEncryption** właściwość w magazynie kluczy hello. Aby uzyskać więcej informacji, zobacz **ustawiony w górę i konfigurowania magazynu kluczy szyfrowania dysków Azure** w hello dodatku.
* Klucz tajny magazynu kluczy, a adresy URL KEK musi być numerów wersji. Azure wymusza to ograniczenie wersji. Nieprawidłowy klucz tajny i KEK adresów URL zobacz następujące przykłady hello:

  * Przykład prawidłowego adresu URL tajny: *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*
  * Przykład prawidłowy adres URL KEK: *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*

* Szyfrowanie dysków Azure nie obsługuje określania numery portów, jako część adresy URL KEK i kluczy tajnych w magazynie kluczy. Przykłady adresów URL magazynu kluczy obsługiwanych i nieobsługiwanych można znaleźć w następujących hello:

  * Adres URL magazynu kluczy można zaakceptować *https://contosovault.vault.azure.net:443/klucze tajne/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*
  * Adres URL magazynu kluczy dopuszczalne: *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*

* tooenable funkcja szyfrowania dysków Azure hello, hello maszyn wirtualnych IaaS musi spełniać następujące wymagania dotyczące konfiguracji punktu końcowego sieci hello:
  * tooget token tooconnect tooyour magazyn kluczy, hello maszyn wirtualnych IaaS musi być możliwe tooconnect punktu końcowego usługi Azure Active Directory tooan, \[login.microsoftonline.com\].
  * toowrite hello szyfrowania kluczy tooyour magazynu kluczy, hello IaaS maszyny Wirtualnej musi być punktu końcowego magazynu kluczy toohello tooconnect stanie.
  * Hello IaaS maszyny Wirtualnej musi być możliwe tooconnect tooan magazynu Azure punktu końcowego czy hosty hello repozytorium rozszerzenie Azure i konto magazynu Azure, że hosty hello pliki VHD.

  > [!NOTE]
  > Jeśli zasady zabezpieczeń ogranicza dostęp z maszynami wirtualnymi Azure toohello Internet, można rozwiązać hello poprzedzających identyfikatora URI i skonfigurować określonej reguły toohello łączność wychodząca tooallow adresów IP.
  >
  >tooconfigure i dostępu do usługi Azure Key Vault za zaporą (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)

* Użyj hello najnowszą wersję zestawu SDK usługi Azure PowerShell w wersji tooconfigure szyfrowania dysków Azure. Pobieranie hello najnowszej wersji [wersji programu Azure PowerShell](https://github.com/Azure/azure-powershell/releases)

 > [!NOTE]
  > Szyfrowanie dysków Azure nie jest obsługiwana w [zestawu SDK usługi Azure PowerShell w wersji 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016). Jeśli wyświetlany błąd powiązane toousing programu Azure PowerShell 1.1.0, zobacz [tooAzure powiązane błąd szyfrowania dysków Azure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).

* toorun dowolnego polecenia wiersza polecenia platformy Azure i powiązać ją z subskrypcją platformy Azure, należy najpierw zainstalować wiersza polecenia platformy Azure:
  * tooinstall wiersza polecenia platformy Azure i powiązać ją z subskrypcją platformy Azure, zobacz [jak tooinstall i Konfigurowanie interfejsu wiersza polecenia Azure](../cli-install-nodejs.md).
  * Zobacz toouse Azure CLI for Mac, Linux i Windows Azure Resource Manager [polecenia wiersza polecenia platformy Azure w trybie Menedżera zasobów](../virtual-machines/azure-cli-arm-commands.md).

* Podczas szyfrowania dysków zarządzanych, jest obowiązkowy tootake wymagań wstępnych migawkę hello zarządzane dysku lub z kopii zapasowej dysku hello poza szyfrowania przed tooenabling szyfrowania dysków Azure.  Bez kopii zapasowej w miejscu wszelkie nieoczekiwany błąd podczas szyfrowania może spowodować hello dysku i wirtualna niedostępna bez opcji odzyskiwania.  Zestaw AzureRmVMDiskEncryptionExtension nie jest obecnie kopii dysków zarządzanych i będzie błąd, jeśli użyty przed dysków zarządzanych, chyba że został określony parametr - skipVmBackup hello.  Ten parametr jest niebezpieczne toouse, chyba że już wykonano kopię zapasową poza szyfrowania dysków Azure.   Jeśli określono parametr - skipVmBackup hello, hello polecenia cmdlet nie dokona kopii zapasowej tooencryption wcześniejsze dysku hello zarządzane.  Z tego powodu uważa się obowiązkowe toomake wymagań wstępnych się, że należy wykonywać kopii zapasowej dysku zarządzanego hello, maszyna wirtualna znajduje się w miejscu wcześniejsze tooenabling szyfrowania dysków Azure w przypadku odzyskiwania jest nowsza.  
> [!NOTE]
 > Parametr - skipVmBackup Hello nigdy nie powinien być używany, chyba że migawka lub kopia zapasowa została już dokonana poza szyfrowania dysków Azure. 

* Hello rozwiązania szyfrowania dysków Azure używa zewnętrznego ochrony klucza funkcji BitLocker hello maszyn wirtualnych IaaS systemu Windows. Dla domeny dołączonego do maszyn wirtualnych, nie należy wypchnąć żadnych zasad grupy, które wymuszania funkcji ochrony Moduł TPM. Aby uzyskać informacje o zasadach grupy hello "Zezwalaj na funkcję BitLocker bez zgodny moduł TPM", zobacz [dokumentacja zasad grupy funkcji BitLocker](https://technet.microsoft.com/library/ee706521).
* Zasady funkcji BitLocker na maszynach wirtualnych przyłączony do domeny z zasad grupy niestandardowe musi zawierać hello następujące ustawienia: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` szyfrowania dysków Azure zakończy się niepowodzeniem, jeśli ustawienia zasad niestandardowych grup do używania funkcji Bitlocker są niezgodne. Na komputerach, które nie miał hello poprawne ustawienia zasad stosowania nowych zasad hello, wymuszanie hello nowych zasad tooupdate (gpupdate.exe/Force) i ponowne uruchomienie może być wymagane.  
* toocreate aplikację usługi Azure AD tworzenia magazynu kluczy, lub skonfigurować istniejący magazyn kluczy i włączenia szyfrowania, zobacz hello [skrypt programu PowerShell wymagań wstępnych szyfrowania dysków Azure](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).
* wymagań wstępnych szyfrowania dysków tooconfigure przy użyciu hello wiersza polecenia platformy Azure, zobacz [ten skrypt Bash](https://github.com/ejarvi/ade-cli-getting-started).
* toouse hello kopia zapasowa Azure usługa tooback zapasowej i przywracania szyfrowane maszyn wirtualnych, po włączeniu szyfrowania z szyfrowania dysków Azure, szyfrowania maszyn wirtualnych przy użyciu konfiguracji klucza szyfrowania dysków Azure hello. Hello usługi Backup obsługuje maszyny wirtualne, które są szyfrowane za pomocą tylko KEK konfiguracji. Zobacz [jak tooback zapasowej i przywracania szyfrowane maszyn wirtualnych przy użyciu szyfrowania usługi Kopia zapasowa Azure](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).

* Podczas szyfrowania woluminu systemu operacyjnego Linux, należy pamiętać, że ponowne uruchomienie maszyny Wirtualnej jest obecnie wymagane na końcu hello hello procesu. Można to zrobić za pomocą portalu hello, programu powershell lub interfejsu wiersza polecenia.   postęp hello tootrack szyfrowania, okresowo sondować hello stanu komunikat zwrócony przez https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus Get AzureRmVMDiskEncryptionStatus.  Po zakończeniu szyfrowania komunikatu o stanie hello hello zwróconych przez to polecenie będzie tę informację.  Na przykład "postępu: dysk systemu operacyjnego zostały pomyślnie zaszyfrowane, wykonaj ponowny rozruch hello maszyny Wirtualnej" w tym hello punktu maszyny Wirtualnej może być uruchomiona ponownie oraz używane.  

* Azure szyfrowanie dysku dla systemu Linux wymaga toohave dysków danych zainstalowanego w systemie Linux tooencryption uprzedniego

* Rekursywnie dysków zainstalowanych danych nie są obsługiwane przez hello szyfrowania dysków Azure dla systemu Linux. Na przykład jeśli hello system docelowy ma zainstalowany dysk na /foo/bar i następnie w /foo/bar/baz, szyfrowanie hello /foo/bar/baz powiedzie się, ale szyfrowania paska/foo/zakończy się niepowodzeniem. 

* Szyfrowanie dysków Azure jest obsługiwana tylko na obrazach obsługiwane galerii Azure, które spełniają wymagania wstępne wymienione wyżej hello. Niestandardowe obrazy klienta nie są obsługiwane schemat partycji toocustom i zachowania procesu, które mogą występować w tych obrazów. Co więcej, nawet galerii opartej na obrazie maszyny Wirtualnej, która początkowo spełnione wymagania wstępne zostały zmienione po utworzeniu mogą być niezgodne.  Dla czy powodu hello sugerowane procedury do szyfrowania maszyny Wirtualnej systemu Linux jest toostart z czystą galerii, szyfrowania hello maszyny Wirtualnej, a następnie dodaj niestandardowe oprogramowania lub toohello danych maszyny Wirtualnej, zgodnie z potrzebami.  

> [!NOTE]
> Kopia zapasowa i przywracanie zaszyfrowanych maszyn wirtualnych jest obsługiwana tylko dla maszyn wirtualnych, które są szyfrowane przy hello KEK konfiguracji. Nie jest obsługiwana na maszynach wirtualnych, które są szyfrowane bez KEK. KEK jest opcjonalnym parametrem, który umożliwia maszyny Wirtualnej.

#### <a name="set-up-hello-azure-ad-application-in-azure-active-directory"></a>Konfigurowanie hello aplikacji usługi Azure AD w usłudze Azure Active Directory
Jeśli potrzebujesz toobe szyfrowania włączone w przypadku uruchomionej maszyny Wirtualnej na platformie Azure szyfrowania dysków Azure generuje i zapisuje magazynu kluczy tooyour hello szyfrowania kluczy. Zarządzanie kluczy szyfrowania w magazynie kluczy, wymaga uwierzytelniania usługi Azure AD.

W tym celu należy utworzyć aplikację usługi Azure AD. Szczegółowy opis kroków można znaleźć rejestrowania aplikacji hello "Get tożsamości dla aplikacji hello" część hello wpis w blogu [usługi Azure Key Vault - krok po kroku](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx). Ten wpis zawiera również liczbę przykłady przydatne do instalowania i konfigurowania magazynu kluczy. Na potrzeby uwierzytelniania można użyć uwierzytelniania opartego na klucz tajny klienta i uwierzytelnianie klienta oparte na certyfikatach usługi Azure AD.

#### <a name="client-secret-based-authentication-for-azure-ad"></a>Uwierzytelnianie oparte na protokole klucz tajny klienta dla usługi Azure AD
kolejnych sekcjach Hello pomoże Ci skonfigurować uwierzytelnianie oparte na klucz tajny klienta dla usługi Azure AD.

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a>Tworzenie aplikacji usługi Azure AD przy użyciu programu Azure PowerShell
Użyj następującego toocreate polecenia cmdlet programu PowerShell usługi Azure AD aplikacji hello:

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> $azureAdApplication.ApplicationId jest hello Azure AD ClientID i $aadClientSecret jest klucz tajny klienta hello korzystała nowsze tooenable szyfrowania dysków Azure. Chroń klucz tajny klienta usługi Azure AD hello odpowiednio.

##### <a name="setting-up-hello-azure-ad-client-id-and-secret-from-hello-azure-classic-portal"></a>Konfigurowanie hello Azure AD identyfikator klienta i klucz tajny z hello klasycznego portalu Azure
Można również ustawić zapasowej identyfikator klienta usługi Azure AD i klucz tajny przy użyciu hello [klasycznego portalu Azure]( https://manage.windowsazure.com). tooperform to zadanie, hello następujące:

1. Kliknij przycisk hello **usługi Active Directory** kartę.

 ![Usługa Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. Kliknij przycisk **Dodawanie aplikacji**, a następnie wpisz nazwę aplikacji hello.

 ![Usługa Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. Kliknij przycisk strzałki hello, a następnie skonfigurować właściwości aplikacji hello.

 ![Usługa Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. Kliknij znacznik wyboru hello w dolnym toofinish lewym rogu hello. zostanie wyświetlona strona konfiguracji aplikacji Hello, a identyfikator klienta usługi Azure AD hello są wyświetlane u dołu hello strony hello.

 ![Usługa Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. Zapisz klucz tajny klienta hello Azure AD, klikając hello **zapisać** przycisku. Należy pamiętać, klucz tajny klienta hello Azure AD w polu tekstowym hello kluczy. Chroń odpowiednio.

 ![Usługa Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > Witaj poprzedzających przepływu nie jest obsługiwana na powitania klasycznego portalu Azure.

##### <a name="use-an-existing-application"></a>Użyj istniejącej aplikacji
tooexecute hello następujące polecenia, uzyskiwał i wykorzystywał hello [modułu Azure AD PowerShell](https://technet.microsoft.com/library/jj151815.aspx).

> [!NOTE]
> Witaj następujące polecenia musi zostać wykonana z nowe okno programu PowerShell. Nie należy używać programu Azure PowerShell lub hello Azure Resource Manager okna tooexecute hello poleceń. Zalecamy takie podejście, ponieważ te polecenia cmdlet w hello MSOnline module lub Azure AD PowerShell.

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a>Uwierzytelnianie oparte na certyfikatach dla usługi Azure AD
> [!NOTE]
> Uwierzytelnianie oparte na certyfikatach AD Azure aktualnie nie jest obsługiwane na maszynach wirtualnych systemu Linux.

Witaj następnych sekcjach Pokaż jak tooconfigure uwierzytelniania opartego na certyfikatach dla usługi Azure AD.

##### <a name="create-an-azure-ad-application"></a>Tworzenie aplikacji usługi Azure AD
toocreate aplikacji usługi Azure AD, wykonaj hello następującego polecenia cmdlet programu PowerShell:

> [!NOTE]
> Zastąp następujące hello `yourpassword` ciąg bezpieczne hasło, a hasło hello zabezpieczenia.

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

Po zakończeniu tego kroku przekazać magazyn kluczy tooyour pliku PFX i włączyć hello dostępu zasad wymaganych toodeploy tooa tego certyfikatu maszyny Wirtualnej.

##### <a name="use-an-existing-azure-ad-application"></a>Użyj istniejącej aplikacji usługi Azure AD
W przypadku konfigurowania uwierzytelniania opartego na certyfikatach dla istniejącej aplikacji, użyj poleceń cmdlet programu PowerShell hello pokazano poniżej. Tooexecute się, że można je z nowe okno programu PowerShell.

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

Po zakończeniu tego kroku przekazać magazyn kluczy tooyour pliku PFX, aby włączyć zasady dostępu hello potrzebne toodeploy hello certyfikatu tooa maszyny Wirtualnej.

##### <a name="upload-a-pfx-file-tooyour-key-vault"></a>Przekaż magazyn kluczy tooyour pliku PFX
Aby uzyskać szczegółowy opis tego procesu, zobacz [hello oficjalny Blog zespołu usługi Azure Key Vault](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx). Jednak hello następującego polecenia cmdlet programu PowerShell są potrzebne dla hello zadania. Tooexecute się, że można je z konsoli programu Azure PowerShell.

> [!NOTE]
> Zastąp następujące hello `yourpassword` ciąg bezpieczne hasło, a hasło hello zabezpieczenia.

    $certLocalPath = 'C:\certs\myaadapp.pfx'
    $certPassword = "yourpassword"
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’

    $fileContentBytes = get-content $certLocalPath -Encoding Byte
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

    $jsonObject = @"
    {
    "data": "$filecontentencoded",
    "dataType" :"pfx",
    "password": "$certPassword"
    }
    "@

    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

    Switch-AzureMode -Name AzureResourceManager
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    Set-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName -SecretValue $secret
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ResourceGroupName $resourceGroupName –EnabledForDeployment

##### <a name="deploy-a-certificate-in-your-key-vault-tooan-existing-vm"></a>Wdróż certyfikat w tooan Twojego magazynu kluczy, istniejącej maszyny Wirtualnej
Po zakończeniu przekazywania hello PFX, Wdróż certyfikat w istniejącej maszyny Wirtualnej z następujących hello tooan magazynu kluczy hello:
 ```
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’
    $vmName = ‘yourVMName’
    $certUrl = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName).Id
    $sourceVaultId = (Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $resourceGroupName).ResourceId
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore "My" -CertificateUrl $certUrl
    Update-AzureRmVM -VM $vm  -ResourceGroupName $resourceGroupName
 ```

#### <a name="set-up-hello-key-vault-access-policy-for-hello-azure-ad-application"></a>Skonfigurować zasady dostępu magazynu kluczy hello aplikacji hello Azure AD
Aplikacja Azure AD wymaga praw tooaccess hello kluczy ani kluczy tajnych w magazynie hello. Użyj hello [ `Set-AzureKeyVaultAccessPolicy` ](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) polecenia cmdlet toogrant uprawnienia toohello aplikacji przy użyciu Identyfikatora klienta hello (który został wygenerowany, gdy aplikacja hello została zarejestrowana) jako hello _— ServicePrincipalName_ wartość parametru. toolearn więcej, zobacz hello blogu [usługi Azure Key Vault - krok po kroku](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx). Poniżej przedstawiono przykład sposobu tooperform to zadanie za pomocą programu PowerShell:

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> Szyfrowanie dysków Azure wymaga hello tooconfigure po aplikacji klienckiej tooyour usługi Azure AD zasad dostępu: _WrapKey_ i _ustawić_ uprawnienia.

## <a name="terminology"></a>Terminologia
niektóre typowe terminy hello jest używany przez tę technologię, użyj hello w poniższej tabeli terminologii toounderstand:

| Terminologia | Definicja |
| --- | --- |
| Azure AD | Usługa Azure AD [usługi Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/). Konto usługi Azure AD jest wymagane do uwierzytelniania, przechowywania i pobierania kluczy tajnych w magazynie kluczy. |
| W usłudze Azure Key Vault | Key Vault jest usługą zarządzania kryptograficznych, klucza opartego na zweryfikowane FIPS Federal Information Processing standardów sprzętowych modułów zabezpieczeń, które pomagają w ochronie z kluczy kryptograficznych i kluczy tajnych poufnych. Aby uzyskać więcej informacji, zobacz [Key Vault](https://azure.microsoft.com/services/key-vault/) dokumentacji. |
| ARM | Azure Resource Manager |
| Funkcja BitLocker |[Funkcja BitLocker](https://technet.microsoft.com/library/hh831713.aspx) jest branży Windows woluminu szyfrowania technologia, która została użyta tooenable szyfrowania dysków na maszynach wirtualnych IaaS systemu Windows. |
| KSB | Klucze szyfrowania funkcji BitLocker są woluminu rozruchowego używanego tooencrypt hello systemu operacyjnego i woluminów danych. klucze funkcji BitLocker Hello są chronione w magazynie kluczy jako kluczy tajnych. |
| Interfejs wiersza polecenia | Zobacz [interfejsu wiersza polecenia platformy Azure](../cli-install-nodejs.md). |
| DM-Crypt |[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) hello podsystem opartych na systemie Linux lub przezroczystego szyfrowania dysku, który został użyty tooenable szyfrowania dysków na maszyn wirtualnych systemu Linux IaaS. |
| KEK | Klucz szyfrowania jest hello klucza asymetrycznego (RSA 2048) można używać tooprotect lub zawijać hello klucz tajny. Możesz podać zabezpieczeń sprzętowych modułów (HSM)-chronione klucza lub klucza chronionego przez oprogramowanie. Aby uzyskać więcej informacji, zobacz [usługi Azure Key Vault](https://azure.microsoft.com/services/key-vault/) dokumentacji. |
| PS polecenia cmdlet. | Zobacz [poleceń cmdlet programu Azure PowerShell](/powershell/azure/overview). |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a>Instalowanie i Konfigurowanie magazynu kluczy do szyfrowania dysków Azure
Szyfrowanie dysków Azure ułatwia zabezpieczenie hello szyfrowanie dysków kluczy i kluczy tajnych w magazynie kluczy. tooset się magazynu kluczy do szyfrowania dysków Azure, pełną hello kroki w każdym hello następujące sekcje.

#### <a name="create-a-key-vault"></a>Tworzenie magazynu kluczy
toocreate magazyn kluczy, użyj jednej z hello następujące opcje:

* ["101-klucza-magazynu-Create" Szablon usługi Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [Polecenia cmdlet magazynu kluczy Azure programu PowerShell](/powershell/module/azurerm.keyvault/#key_vault)
* Azure Resource Manager
* Jak zbyt[bezpiecznego magazynu kluczy](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)

> [!NOTE]
> Jeśli magazyn kluczy zostały już skonfigurowane dla Twojej subskrypcji, Pomiń toohello następnej sekcji.

![W usłudze Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a>Konfigurowanie klucza szyfrowania (opcjonalnie)
Toouse KEK dla dodatkową warstwę zabezpieczeń dla kluczy szyfrowania hello funkcji BitLocker, należy dodać magazyn kluczy KEK tooyour. Użyj hello [ `Add-AzureKeyVaultKey` ](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) toocreate polecenia cmdlet klucz szyfrowania kluczy w magazynie kluczy hello. Można także zaimportować KEK z lokalnymi Zarządzanie klucza HSM. Aby uzyskać więcej informacji, zobacz [klucza magazynu dokumentacji](https://azure.microsoft.com/documentation/services/key-vault/).

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

Możesz dodać hello KEK przechodząc tooAzure Resource Manager lub przy użyciu interfejsu magazynu kluczy.

![W usłudze Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a>Ustaw uprawnienia magazyn kluczy
Hello platformy Azure wymaga dostępu toohello szyfrowania kluczy lub kluczy tajnych w toomake Twojego magazynu kluczy ich toohello dostępne maszyny Wirtualnej do rozruchu i odszyfrowywania hello woluminów. toogrant uprawnienia toohello platformy Azure, zestawu hello **EnabledForDiskEncryption** właściwości w kluczu hello magazynu za pomocą polecenia cmdlet programu PowerShell magazynu kluczy hello:

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

Można również ustawić hello **EnabledForDiskEncryption** właściwości, przechodząc na stronę hello [Eksploratora zasobów Azure](https://resources.azure.com).

Jak wspomniano wcześniej, musisz ustawić hello **EnabledForDiskEncryption** właściwości magazynu kluczy. W przeciwnym razie hello wdrożenie zakończy się niepowodzeniem.

Jak pokazano poniżej, można skonfigurować zasady dostępu dla aplikacji usługi Azure AD z hello magazynu kluczy interfejsu:

![W usłudze Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![W usłudze Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

Na powitania **zasady dostępu zaawansowane** i upewnij się, że magazynu kluczy jest włączona obsługa szyfrowania dysków Azure:

![Usługi Azure key vault](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a>Scenariusze wdrażania szyfrowanie dysków oraz możliwości użytkowników.
Aby umożliwić wiele scenariuszy szyfrowania dysków i hello kroki mogą się różnić zgodnie z toohello scenariusza. Witaj poniższych częściach omówiono scenariusze hello większej liczby szczegółów.

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-hello-marketplace"></a>Włącz szyfrowanie dla nowych maszyn wirtualnych IaaS, które są tworzone na podstawie hello Marketplace
Można włączyć szyfrowanie dysków na nowej maszyny Wirtualnej systemu Windows IaaS z hello Marketplace na platformie Azure przy użyciu hello [szablonu usługi Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).

1. W szablonie hello Azure szybki start kliknij **wdrażanie tooAzure**, wprowadź konfiguracji szyfrowania hello na powitania **parametry** bloku, a następnie kliknij przycisk **OK**.

2. Wybierz hello subskrypcji, grupy zasobów, lokalizacja grupy zasobów, postanowienia prawne i umowę, a następnie kliknij przycisk **Utwórz** tooenable szyfrowania na nowej maszyny Wirtualnej IaaS.

> [!NOTE]
> Ten szablon umożliwia tworzenie nowych zaszyfrowanych Windows maszynę Wirtualną, która używa obrazu galerii hello systemu Windows Server 2012.

Można włączyć szyfrowanie dysków na nowe IaaS RedHat Linux 7.2 maszynę Wirtualną za pomocą macierzy RAID-0 200 GB, za pomocą tego [szablonu usługi Resource Manager](https://aka.ms/fde-rhel). Po wdrożeniu szablonu hello sprawdzić stanu szyfrowania hello maszyny Wirtualnej za pomocą hello `Get-AzureRmVmDiskEncryptionStatus` polecenia cmdlet, zgodnie z opisem w [OS szyfrowania dysków na uruchomionej maszyny Wirtualnej systemu Linux](#encrypting-os-drive-on-a-running-linux-vm). Gdy maszyna hello zwraca stan _VMRestartPending_, uruchom ponownie hello maszyny Wirtualnej.

Witaj Poniższa tabela zawiera listę parametrów szablonu usługi Resource Manager hello nowych maszyn wirtualnych z scenariusz Marketplace hello przy użyciu Identyfikatora klienta usługi Azure AD:

| Parametr | Opis |
| --- | --- |
| adminUserName | Nazwa użytkownika administratora hello maszyny wirtualnej. |
| adminPassword | Hasło użytkownika administratora hello maszyny wirtualnej. |
| newStorageAccountName | Nazwa toostore konta magazynu hello systemu operacyjnego i danych wirtualne dyski twarde. |
| vmSize | Rozmiar hello maszyny Wirtualnej. Obecnie obsługiwane są tylko standardowe A, D i G serii. |
| virtualNetworkName | Nazwa hello sieć wirtualna tego hello wirtualna karta sieciowa powinna należeć do. |
| subnetName | Nazwa podsieci hello hello sieć wirtualna tego hello wirtualna karta sieciowa powinna należeć do. |
| AADClientID | Identyfikator klienta aplikacji hello Azure AD, która ma uprawnienia toowrite kluczy tajnych tooyour klucza magazynu. |
| AADClientSecret | Klucz tajny klienta aplikacji hello Azure AD, która ma uprawnienia toowrite kluczy tajnych tooyour klucza magazynu. |
| keyVaultURL | Adres URL hello klucza magazynu tego hello klucz należy przekazać do funkcji BitLocker. Możesz pobrać go za pomocą polecenia cmdlet hello `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`. |
| keyEncryptionKeyURL | Adres URL hello klucza szyfrowania klucza, który jest używany tooencrypt hello generowane klucza funkcji BitLocker (opcjonalnie). |
| keyVaultResourceGroup | Grupa zasobów hello magazynu kluczy. |
| vmName | Nazwa hello maszynę Wirtualną, która hello operacji szyfrowania jest wykonywane na toobe. |

> [!NOTE]
> _KeyEncryptionKeyURL_ jest parametrem opcjonalnym. Możesz objąć własne KEK toofurther zabezpieczenie hello klucza szyfrowania danych (klucz tajny hasło) w magazynie kluczy.

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a>Włącz szyfrowanie dla nowych maszyn wirtualnych IaaS, które są tworzone na podstawie klienta systemu szyfrowania plików VHD i kluczy szyfrowania
W tym scenariuszu można włączyć szyfrowanie przy użyciu szablonu usługi Resource Manager hello, poleceń cmdlet programu PowerShell lub polecenia interfejsu wiersza polecenia. Witaj poniższe sekcje zawierają opis większa szablonu usługi Resource Manager hello szczegóły i polecenia interfejsu wiersza polecenia.

Wykonaj instrukcje hello z jednego z tych sekcji przygotowania zaszyfrowane wstępnie obrazy, których można użyć w systemie Azure. Po utworzeniu obrazu hello hello kroki służą w hello następnej sekcji toocreate zaszyfrowanych maszyny Wirtualnej platformy Azure.

* [Przygotowanie wstępnie zaszyfrowanego dysku VHD systemu Windows](#preparing-a-pre-encrypted-windows-vhd)
* [Przygotowanie wstępnie zaszyfrowanego dysku VHD systemu Linux](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-hello-resource-manager-template"></a>Przy użyciu szablonu usługi Resource Manager hello
Można włączyć szyfrowanie dysków na zaszyfrowany dysk VHD za pomocą hello [szablonu usługi Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).

1. W szablonie hello Azure szybki start kliknij **wdrażanie tooAzure**, wprowadź konfiguracji szyfrowania hello na powitania **parametry** bloku, a następnie kliknij przycisk **OK**.

2. Wybierz hello subskrypcji, grupy zasobów, lokalizacja grupy zasobów, postanowienia prawne i umowę, a następnie kliknij przycisk **Utwórz** tooenable szyfrowania na hello nowej maszyny Wirtualnej IaaS.

Witaj Poniższa tabela zawiera listę parametrów szablonu usługi Resource Manager hello zaszyfrowany dysk VHD:

| Parametr | Opis |
| --- | --- |
| newStorageAccountName | Nazwa hello toostore konta magazynu hello szyfrowane wirtualnego dysku twardego systemu operacyjnego. To konto magazynu należy już zostały utworzone w hello same grupy zasobów i tej samej lokalizacji co hello maszyny Wirtualnej. |
| osVhdUri | Identyfikator URI hello wirtualnego dysku twardego systemu operacyjnego z hello konta magazynu. |
| osType | Typ produktu systemu operacyjnego (Windows/Linux). |
| virtualNetworkName | Nazwa hello sieć wirtualna tego hello wirtualna karta sieciowa powinna należeć do. Witaj nazwa powinna już zostały utworzone w hello takie same grupy zasobów i tej samej lokalizacji co hello maszyny Wirtualnej. |
| subnetName | Nazwa podsieci hello na powitania sieć wirtualna tego hello wirtualna karta sieciowa powinna należeć do. |
| vmSize | Rozmiar hello maszyny Wirtualnej. Obecnie obsługiwane są tylko standardowe A, D i G serii. |
| keyVaultResourceID | Witaj ResourceID, który identyfikuje hello zasobu magazynu kluczy Azure Resource Manager. Możesz pobrać go za pomocą polecenia cmdlet programu PowerShell hello `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`. |
| keyVaultSecretUrl | Adres URL klucza szyfrowania dysków hello, który został skonfigurowany w magazynie kluczy hello. |
| keyVaultKekUrl | Adres URL hello klucza szyfrowania klucza szyfrowania hello wygenerowany klucz szyfrowania dysków. |
| vmName | Nazwa hello maszyn wirtualnych IaaS. |

#### <a name="using-powershell-cmdlets"></a>Za pomocą poleceń cmdlet programu PowerShell
Można włączyć szyfrowanie dysków na zaszyfrowany dysk VHD za pomocą polecenia cmdlet programu PowerShell hello [ `Set-AzureRmVMOSDisk` ](/powershell/module/azurerm.compute/set-azurermvmosdisk).  

#### <a name="using-cli-commands"></a>Za pomocą polecenia interfejsu wiersza polecenia
Szyfrowanie dysków tooenable dla tego scenariusza za pomocą polecenia interfejsu wiersza polecenia hello następujące:

1. Ustawianie zasad dostępu w magazynie kluczy:

   * Zestaw hello **EnabledForDiskEncryption** flagi:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * Ustaw uprawnienia tooAzure AD aplikacji toowrite kluczy tajnych tooyour magazynu kluczy:

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. tooenable szyfrowania w przypadku istniejących lub uruchomionej maszyny Wirtualnej, typ:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. Pobierz stan szyfrowania:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. szyfrowanie tooenable na nowej maszyny Wirtualnej z zaszyfrowany dysk VHD, użyj hello następujące parametry hello `azure vm create` polecenia:

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a>Włącz szyfrowanie dla istniejących lub uruchomione maszyny Wirtualnej systemu Windows IaaS na platformie Azure
W tym scenariuszu można włączyć szyfrowanie przy użyciu szablonu usługi Resource Manager hello, poleceń cmdlet programu PowerShell lub polecenia interfejsu wiersza polecenia. Witaj poniższych sekcjach opisano szczegółowo sposób tooenable hello go przy użyciu szablonu usługi Resource Manager i polecenia interfejsu wiersza polecenia.

#### <a name="using-hello-resource-manager-template"></a>Przy użyciu szablonu usługi Resource Manager hello
Można włączyć szyfrowanie dysku na istniejących lub uruchomione maszyny wirtualne IaaS systemu Windows na platformie Azure przy użyciu hello [szablonu usługi Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).

1. W szablonie hello Azure szybki start kliknij **wdrażanie tooAzure**, wprowadź konfiguracji szyfrowania hello na powitania **parametry** bloku, a następnie kliknij przycisk **OK**.

2. Wybierz hello subskrypcji, grupy zasobów, lokalizacja grupy zasobów, postanowienia prawne i umowę, a następnie kliknij przycisk **Utwórz** tooenable szyfrowania na powitania istniejące lub uruchamiania maszyn wirtualnych IaaS.

Witaj Poniższa tabela zawiera listę parametrów szablonu usługi Resource Manager hello istniejących lub działających maszyn wirtualnych, które mają identyfikator klienta usługi Azure AD:

| Parametr | Opis |
| --- | --- |
| AADClientID | Identyfikator klienta aplikacji hello Azure AD, która ma uprawnienia toowrite kluczy tajnych toohello klucza magazynu. |
| AADClientSecret | Klucz tajny klienta aplikacji hello Azure AD, która ma uprawnienia toowrite kluczy tajnych toohello klucza magazynu. |
| Nazwa | Nazwa klucza hello magazynu tego hello klucz należy przekazać do funkcji BitLocker. Możesz pobrać go za pomocą polecenia cmdlet hello `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`. |
|  keyEncryptionKeyURL | Adres URL hello klucza szyfrowania klucza, który jest używany tooencrypt hello generowane klucza funkcji BitLocker. Ten parametr jest opcjonalny w przypadku wybrania **nokek** na liście rozwijanej UseExistingKek hello. W przypadku wybrania **kek** na liście rozwijanej UseExistingKek hello, musisz wprowadzić hello _keyEncryptionKeyURL_ wartości. |
| volumeType | Typ operacji szyfrowania hello jest wykonywana na wolumin. Prawidłowe wartości to _OS_, _danych_, i _wszystkich_. |
| sequenceVersion | Wersja sekwencji hello działania funkcji BitLocker. Zwiększ numer wersji, za każdym razem, gdy operacji szyfrowania dysków odbywa się na powitania tej samej maszyny Wirtualnej. |
| vmName | Nazwa hello maszynę Wirtualną, która hello operacji szyfrowania jest wykonywane na toobe. |

> [!NOTE]
> _KeyEncryptionKeyURL_ jest parametrem opcjonalnym. W magazynie kluczy hello przełączeniem własne KEK toofurther zabezpieczenie hello klucza szyfrowania danych (funkcji BitLocker Szyfrowanie klucz tajny).

#### <a name="using-powershell-cmdlets"></a>Za pomocą poleceń cmdlet programu PowerShell
Aby uzyskać informacje na temat włączania szyfrowania z szyfrowania dysków Azure za pomocą poleceń cmdlet programu PowerShell, zobacz hello blogach [Eksploruj szyfrowania dysków Azure przy użyciu programu Azure PowerShell — część 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) i [Eksploruj szyfrowania dysków Azure przy użyciu programu Azure PowerShell — część 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).

#### <a name="using-cli-commands"></a>Za pomocą polecenia interfejsu wiersza polecenia
szyfrowanie tooenable na istniejących lub uruchomione maszyny Wirtualnej systemu Windows IaaS na platformie Azure przy użyciu polecenia interfejsu wiersza polecenia hello następujące:

1. zasady dostępu tooset w magazynie kluczy hello:
   * Zestaw hello **EnabledForDiskEncryption** flagi:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * Ustaw uprawnienia tooAzure AD aplikacji toowrite kluczy tajnych tooyour magazynu kluczy:

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. tooenable szyfrowania w przypadku istniejących lub uruchomionej maszyny Wirtualnej:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. Stan szyfrowania tooget:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. szyfrowanie tooenable na nowej maszyny Wirtualnej z zaszyfrowany dysk VHD, użyj hello następujące parametry hello `azure vm create` polecenia:

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a>Włącz szyfrowanie dla istniejących lub nie działają IaaS maszyny Wirtualnej systemu Linux na platformie Azure
Można włączyć szyfrowanie dysków na istniejące lub nie działają IaaS maszyny Wirtualnej systemu Linux na platformie Azure przy użyciu hello [szablonu usługi Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).

1. Kliknij przycisk **wdrażanie tooAzure** na szablon hello Azure szybki start, wprowadź konfiguracji szyfrowania hello na powitania **parametry** bloku, a następnie kliknij przycisk **OK**.

2. Wybierz hello subskrypcji, grupy zasobów, lokalizacja grupy zasobów, postanowienia prawne i umowę, a następnie kliknij przycisk **Utwórz** tooenable szyfrowania na powitania istniejące lub uruchamiania maszyn wirtualnych IaaS.

Witaj w poniższej tabeli przedstawiono parametry szablonu usługi Resource Manager dla istniejących lub działających maszyn wirtualnych, które mają identyfikator klienta usługi Azure AD:

| Parametr | Opis |
| --- | --- |
| AADClientID | Identyfikator klienta aplikacji hello Azure AD, która ma uprawnienia toowrite kluczy tajnych toohello klucza magazynu. |
| AADClientSecret | Klucz tajny klienta aplikacji hello Azure AD, która ma uprawnienia toowrite kluczy tajnych tooyour klucza magazynu. |
| Nazwa | Nazwa klucza hello magazynu tego hello klucz należy przekazać do funkcji BitLocker. Możesz pobrać go za pomocą polecenia cmdlet hello `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`. |
|  keyEncryptionKeyURL | Adres URL hello klucza szyfrowania klucza, który jest używany tooencrypt hello generowane klucza funkcji BitLocker. Ten parametr jest opcjonalny w przypadku wybrania **nokek** na liście rozwijanej UseExistingKek hello. W przypadku wybrania **kek** na liście rozwijanej UseExistingKek hello, musisz wprowadzić hello _keyEncryptionKeyURL_ wartości. |
| volumeType | Typ operacji szyfrowania hello jest wykonywana na wolumin. Nieprawidłowy obsługiwane wartości to _OS_ lub _wszystkie_ (dla RHEL 7.2, CentOS 7.2 i Ubuntu 16.04), i _danych_ (dla wszystkich innych dystrybucji). |
| sequenceVersion | Wersja sekwencji hello działania funkcji BitLocker. Zwiększ numer wersji, za każdym razem, gdy operacji szyfrowania dysków odbywa się na powitania tej samej maszyny Wirtualnej. |
| vmName | Nazwa hello maszynę Wirtualną, która hello operacji szyfrowania jest wykonywane na toobe. |
| Hasło | Klucz szyfrowania danych hello wpisz silne hasło. |

> [!NOTE]
> _KeyEncryptionKeyURL_ jest parametrem opcjonalnym. Możesz objąć własne KEK toofurther zabezpieczenie hello klucza szyfrowania danych (klucz tajny hasło) w magazynie kluczy.

#### <a name="cli-commands"></a>Polecenia interfejsu wiersza polecenia
Można włączyć szyfrowanie dysków na zaszyfrowany dysk VHD przez zainstalowanie i używanie hello [polecenia interfejsu wiersza polecenia](../cli-install-nodejs.md). szyfrowanie tooenable na istniejących lub działających maszyn wirtualnych systemu Linux IaaS na platformie Azure przy użyciu polecenia interfejsu wiersza polecenia hello następujące:

1. Ustawianie zasad dostępu w magazynie kluczy hello:

 * Zestaw hello **EnabledForDiskEncryption** flagi:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * Ustaw uprawnienia tooAzure AD aplikacji toowrite kluczy tajnych tooyour magazynu kluczy:

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. tooenable szyfrowania w przypadku istniejących lub uruchomionej maszyny Wirtualnej:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. Pobierz stan szyfrowania:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. szyfrowanie tooenable na nowej maszyny Wirtualnej z zaszyfrowany dysk VHD, użyj hello następujące parametry hello `azure vm create` polecenia:
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-hello-encryption-status-of-an-encrypted-iaas-vm"></a>Pobierz stan szyfrowania hello zaszyfrowanych maszyny wirtualnej IaaS
Przy użyciu usługi Azure Resource Manager można uzyskać stanu szyfrowania hello [poleceń cmdlet programu PowerShell](/powershell/azure/overview), lub polecenia interfejsu wiersza polecenia. Hello w następujących sekcjach wyjaśniono, jak hello toouse klasycznego portalu Azure i tooget polecenia interfejsu wiersza polecenia hello stanu szyfrowania.

#### <a name="get-hello-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a>Uzyskiwanie hello stanu szyfrowania zaszyfrowanej maszyny Wirtualnej systemu Windows przy użyciu usługi Azure Resource Manager
Z usługi Azure Resource Manager można uzyskać stanu szyfrowania hello hello maszyn wirtualnych IaaS hello następujący:

1. Zaloguj się toohello [klasycznego portalu Azure](https://portal.azure.com/), a następnie kliknij przycisk **maszyn wirtualnych** w toosee w okienku po lewej stronie powitania widok podsumowania hello maszyn wirtualnych w ramach subskrypcji. Można filtrować widok maszyn wirtualnych hello wybierając Nazwa subskrypcji hello hello **subskrypcji** listy rozwijanej.

2. U góry hello hello **maszyn wirtualnych** kliknij przycisk **kolumn**.

3. Na powitania **kolumny wybierz** bloku, wybierz opcję **szyfrowanie dysków**, a następnie kliknij przycisk **aktualizacji**. Powinien zostać wyświetlony stan szyfrowania hello przedstawiający hello szyfrowanie dysków kolumny _włączone_ lub _nie włączono_ dla każdej maszyny Wirtualnej, jak pokazano w następującej ilustracji hello:

 ![Ochrona przed złośliwym kodem zapewniana przez Microsoft na platformie Azure](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-hello-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-hello-disk-encryption-powershell-cmdlet"></a>Pobierz stan szyfrowania hello zaszyfrowanych maszyny wirtualnej IaaS (system Windows/Linux) za pomocą polecenia cmdlet programu PowerShell szyfrowanie dysków hello
Można pobrać stanu szyfrowania hello hello maszyn wirtualnych IaaS z polecenia cmdlet programu PowerShell szyfrowanie dysków hello `Get-AzureRmVMDiskEncryptionStatus`. ustawienia szyfrowania hello tooget dla maszyny Wirtualnej, wprowadź następujące hello:

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

Możesz sprawdzić dane wyjściowe hello _Get-AzureRmVMDiskEncryptionStatus_ do szyfrowania klucza adresów URL.

    C:\> $status = Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName
    e $VMName -ExtensionName $ExtensionName
    C:\> $status.OsVolumeEncryptionSettings

    DiskEncryptionKey                                                 KeyEncryptionKey                                               Enabled
    -----------------                                                 ----------------                                               -------
    Microsoft.Azure.Management.Compute.Models.KeyVaultSecretReference Microsoft.Azure.Management.Compute.Models.KeyVaultKeyReference    True


    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey.SecretUrl
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a
    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey

    SecretUrl                                                                                                               SourceVault
    ---------                                                                                                               -----------
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a Microsoft.Azure.Management....

Witaj OSVolumeEncrypted i DataVolumesEncrypted ustawienia wartości są ustawiane too_Encrypted_, który pokazuje, że oba woluminy są szyfrowane za pomocą szyfrowania dysków Azure. Aby uzyskać informacje na temat włączania szyfrowania z szyfrowania dysków Azure za pomocą poleceń cmdlet programu PowerShell, zobacz hello blogach [Eksploruj szyfrowania dysków Azure przy użyciu programu Azure PowerShell — część 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) i [Eksploruj szyfrowania dysków Azure przy użyciu programu Azure PowerShell — część 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).

> [!NOTE]
> Na maszynach wirtualnych systemu Linux, trwa trzy minut toofour hello `Get-AzureRmVMDiskEncryptionStatus` stanu szyfrowania hello tooreport polecenia cmdlet.

#### <a name="get-hello-encryption-status-of-hello-iaas-vm-from-hello-disk-encryption-cli-command"></a>Pobrać stanu szyfrowania hello hello maszyn wirtualnych IaaS z polecenia interfejsu wiersza polecenia szyfrowanie dysków hello
Stan szyfrowania hello hello maszyn wirtualnych IaaS można uzyskać za pomocą polecenia interfejsu wiersza polecenia szyfrowanie dysków hello `azure vm show-disk-encryption-status`. ustawienia szyfrowania hello tooget dla maszyny Wirtualnej, wprowadź sesję wiersza polecenia platformy Azure:

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a>Wyłącz szyfrowanie uruchamiania maszyny Wirtualnej systemu Windows IaaS
Można wyłączyć szyfrowania na uruchomionej maszyny Wirtualnej systemu Linux IaaS lub systemu Windows za pośrednictwem hello szablon Menedżera zasobów szyfrowania dysków Azure lub poleceń cmdlet programu PowerShell i określić hello odszyfrowywania konfiguracji.

##### <a name="windows-vm"></a>Maszyna wirtualna z systemem Windows
krok Wyłącz szyfrowanie Hello wyłącza funkcję szyfrowania hello systemu operacyjnego i/lub ilość danych hello na powitania uruchamiania maszyny Wirtualnej systemu Windows IaaS. Nie można wyłączyć hello woluminu systemu operacyjnego i pozostawić hello ilość danych zaszyfrowanych. Po wykonaniu kroku Wyłącz szyfrowanie hello hello Azure klasycznego modelu wdrażania aktualizacji modelu usługi hello maszyny Wirtualnej, a hello maszyny Wirtualnej systemu Windows IaaS jest oznaczony jako odszyfrowany. zawartość Hello hello maszyny Wirtualnej nie są szyfrowane, gdy. odszyfrowywanie Hello nie powoduje usunięcia z magazynu i hello szyfrowania klucza materiału klucza (klucze szyfrowania funkcji BitLocker dla systemów Windows i hasło dla systemu Linux).

##### <a name="linux-vm"></a>Maszyny Wirtualnej systemu Linux
krok Wyłącz szyfrowanie Hello wyłącza funkcję szyfrowania woluminu danych hello na powitania uruchamiania maszyny Wirtualnej systemu Linux IaaS. Ten krok działa tylko, jeśli hello dysk systemu operacyjnego nie jest zaszyfrowany.

> [!NOTE]
> Wyłączenie szyfrowania na powitania dysk systemu operacyjnego nie jest dozwolona na maszynach wirtualnych systemu Linux.

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a>Wyłącz szyfrowanie na maszynie Wirtualnej IaaS istniejących lub nie działają
Można wyłączyć szyfrowania dysków na uruchomionych maszyn wirtualnych IaaS systemu Windows za pomocą hello [szablonu usługi Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).

1. W szablonie hello Azure szybki start kliknij **wdrażanie tooAzure**, wprowadź konfiguracji odszyfrowywania hello na powitania **parametry** bloku, a następnie kliknij przycisk **OK**.

2. Wybierz hello subskrypcji, grupy zasobów, lokalizacja grupy zasobów, postanowienia prawne i umowę, a następnie kliknij przycisk **Utwórz** tooenable szyfrowania na nowej maszyny Wirtualnej IaaS.

Dla maszyn wirtualnych systemu Linux, można wyłączyć szyfrowania za pomocą hello [wyłączyć szyfrowania na uruchomionej maszyny Wirtualnej systemu Linux](https://aka.ms/decrypt-linuxvm) szablonu.

Witaj Poniższa tabela zawiera listę parametrów szablonu usługi Resource Manager wyłączenie szyfrowania na uruchomionej maszynie Wirtualnej IaaS:

| Parametr | Opis |
| --- | --- |
| vmName | Nazwa hello maszynę Wirtualną, która hello operacji szyfrowania jest wykonywane na toobe.
| volumeType | Typ operacji odszyfrowywania odbywa się na wolumin. Prawidłowe wartości to _OS_, _danych_, i _wszystkich_. Nie można wyłączyć szyfrowania na uruchomienie woluminu systemu operacyjnego maszyny Wirtualnej systemu Windows IaaS/rozruchowego bez wyłączenie szyfrowania na powitania _danych_ woluminu. Należy również zauważyć, że wyłączenie szyfrowania na powitania dysk systemu operacyjnego nie jest dozwolona na maszynach wirtualnych systemu Linux. |
| sequenceVersion | Wersja sekwencji hello działania funkcji BitLocker. Zwiększ numer wersji, za każdym razem, gdy operacji odszyfrowywania dysku jest wykonywana na powitania tej samej maszyny Wirtualnej. |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a>Wyłącz szyfrowanie na maszynie Wirtualnej IaaS istniejących lub nie działają
Zobacz toodisable szyfrowania w przypadku istniejących lub nie działają IaaS maszyny Wirtualnej za pomocą polecenia cmdlet programu PowerShell hello, [ `Disable-AzureRmVMDiskEncryption` ](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption). To polecenie cmdlet obsługuje zarówno systemu Windows, jak i maszyn wirtualnych systemu Linux. szyfrowania toodisable instaluje rozszerzenia w maszynie wirtualnej hello. Jeśli hello _nazwa_ parametr nie zostanie określony, rozszerzenie nazwy domyślnej hello _AzureDiskEncryption za dla maszyn wirtualnych systemu Windows_ jest tworzony.

Na maszynach wirtualnych systemu Linux rozszerzenia AzureDiskEncryptionForLinux hello jest używany.

> [!NOTE]
> To polecenie cmdlet ponowny rozruch hello maszyny wirtualnej.

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a>Włącz szyfrowanie dla zaszyfrowane wstępnie IaaS maszynę Wirtualną za pomocą dysku zarządzanego Azure
Użyj toocreate szablonu Azure ARM zarządzane dysku hello, którego zaszyfrowanych maszyny Wirtualnej z dysku VHD zaszyfrowane wstępnie przy użyciu szablonu ARM hello znajdujący się w   
[Utwórz nowe zaszyfrowanych dysków zarządzanych z zaszyfrowane wstępnie obiektu blob dysku VHD/magazynu] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a>Włącz szyfrowanie dla nowej Linux IaaS maszyny Wirtualnej z dyskiem zarządzane Azure
Użyj toocreate szablonu Azure ARM zarządzane dysku hello szyfrowane nowej maszyny Wirtualnej IaaS systemu Linux przy użyciu szablonu ARM hello znajdujący się w   
[Wdrażanie RHEL 7.2 z pełne szyfrowanie dysków] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a>Włącz szyfrowanie dla nowej maszyny Wirtualnej IaaS systemu Windows z dysku zarządzanego Azure
 Użyj toocreate szablonu Azure ARM zarządzane dysku hello szyfrowane nowej maszyny Wirtualnej IaaS systemu Linux przy użyciu szablonu ARM hello znajdujący się w   
 [Tworzenie nowych zaszyfrowanych systemu Windows IaaS zarządzane dysku maszyny Wirtualnej z obrazu galerii] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)

  > [!NOTE]
  >Obowiązkowe toosnapshot i/lub tworzenia kopii zapasowych dysków zarządzanych i opartych na wystąpienie maszyny Wirtualnej poza wcześniejsze tooenabling szyfrowania dysków Azure.  Migawki dysków zarządzanych w hello może zostać pobrany z portalu hello, lub kopia zapasowa Azure można używać.  Kopie zapasowe upewnij się, że opcji odzyskiwania jest możliwe w przypadku hello żadnych nieoczekiwany błąd podczas szyfrowania.  Po utworzeniu kopii zapasowej polecenia cmdlet hello AzureRmVMDiskEncryptionExtension zestaw może być dysków używanych tooencrypt zarządzane, określając parametr - skipVmBackup hello.  To polecenie zakończy się niepowodzeniem przed dysków zarządzanych, na podstawie maszyny Wirtualnej, dopóki nie wykonano kopii zapasowej i podano tego parametru.    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a>Aktualizowanie ustawień szyfrowania z istniejącej maszyny Wirtualnej z systemem innym niż premium zaszyfrowane
  Używanie hello istniejącego dysku platformy Azure szyfrowania obsługiwane interfejsów do uruchamiania maszyny Wirtualnej [PS poleceń cmdlet, interfejsu wiersza polecenia lub ARM szablonów] tooupdate hello ustawienia szyfrowania, takich jak usługi AAD klienta identyfikator/klucz tajny, klucz szyfrowania klucza [KEK], klucz szyfrowania funkcją BitLocker dla maszyny Wirtualnej systemu Windows lub hasło dla Ustawienie szyfrowania aktualizacji hello itp. maszyny Wirtualnej systemu Linux jest obsługiwana tylko dla maszyn wirtualnych przez inne niż premium magazynu. Jest obsługiwana dla maszyn wirtualnych przez Magazyn w warstwie premium NNOT.

## <a name="appendix"></a>Dodatek
### <a name="connect-tooyour-subscription"></a>Połącz tooyour subskrypcji
Przed kontynuowaniem należy przejrzeć hello *wymagania wstępne* w tym artykule. Po upewnieniu się, że zostały spełnione wszystkie wymagania wstępne, podłącz subskrypcji tooyour hello następujący:

1. Uruchom sesję programu PowerShell Azure i zaloguj się tooyour konto platformy Azure za pomocą następującego polecenia hello:

    `Login-AzureRmAccount`

2. Jeśli masz wiele subskrypcji i chcesz toouse jeden toospecify, wpisz powitania po toosee hello subskrypcje dla swojego konta:

    `Get-AzureRmSubscription`

3. Subskrypcja hello toospecify ma toouse, wpisz:

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. tooverify czy subskrypcję hello jest poprawna, wpisz:

    `Get-AzureRmSubscription`

5. Witaj tooconfirm szyfrowania dysków Azure są zainstalowane polecenia cmdlet, wpisz:

    `Get-command *diskencryption*`

6. następujące dane wyjściowe Hello potwierdza hello Azure PowerShell szyfrowania dysku instalacji:

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a>Przygotowanie wstępnie zaszyfrowanego dysku VHD systemu Windows
kolejnych sekcjach Hello są niezbędne tooprepare zaszyfrowane wstępnie dysku VHD systemu Windows dla wdrożenia jako zaszyfrowanego dysku VHD w programie Azure IaaS. Użyj hello tooprepare informacji i rozruchu świeże systemu Windows maszyny Wirtualnej (VHD) dla usługi Azure Site Recovery lub Azure.

#### <a name="update-group-policy-tooallow-non-tpm-for-os-protection"></a>Aktualizowanie grupy zasad tooallow bez modułu TPM do ochrony systemu operacyjnego
Ustawienia zasad grupy funkcji BitLocker hello **szyfrowania dysków funkcją BitLocker**, które znajdują się w obszarze **lokalnych zasad komputera** > **Konfiguracja komputera**  >  **Szablony administracyjne** > **składniki systemu Windows**. Zmienić to ustawienie zbyt**dyski z systemem operacyjnym** > **wymaga dodatkowego uwierzytelniania przy uruchamianiu** > **Zezwalaj na funkcję BitLocker bez zgodny moduł TPM**, jak pokazano w hello następującej ilustracji:

![Ochrona przed złośliwym kodem zapewniana przez Microsoft na platformie Azure](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a>Zainstaluj składniki funkcji BitLocker
W systemie Windows Server 2012 i nowszych Użyj hello następujące polecenie:

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

Dla systemu Windows Server 2008 R2 należy użyć hello następujące polecenie:

    ServerManagerCmd -install BitLockers

#### <a name="prepare-hello-os-volume-for-bitlocker-by-using-bdehdcfg"></a>Przygotowanie hello woluminu systemu operacyjnego dla funkcji BitLocker przy użyciu`bdehdcfg`
toocompress hello partycji systemu operacyjnego i przygotowanie maszyny hello funkcji BitLocker, należy wykonać hello następujące polecenie:

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-hello-os-volume-by-using-bitlocker"></a>Ochrona powitalnych woluminu systemu operacyjnego za pomocą funkcji BitLocker
Użyj hello [ `manage-bde` ](https://technet.microsoft.com/library/ff829849.aspx) polecenia tooenable szyfrowania na powitania wolumin rozruchowy przy użyciu zewnętrznego funkcji ochrony klucza. Również umieścić klucz zewnętrzny hello (plik .bek) na powitania zewnętrzny dysk lub wolumin. Szyfrowanie jest włączone na wolumin systemowy/rozruchowy powitania po następnym ponownym uruchomieniu hello.

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> Przygotowanie hello maszyny Wirtualnej z oddzielnych danych/zasobów wirtualnego dysku twardego do pobierania klucza zewnętrznego hello za pomocą funkcji BitLocker.

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a>Szyfrowanie dysku systemu operacyjnego na uruchomionej maszyny Wirtualnej systemu Linux
Szyfrowanie dysku systemu operacyjnego na uruchomionej maszyny Wirtualnej systemu Linux jest obsługiwana na powitania po dystrybucji:

* RHEL 7.2
* 7.2 centOS
* Ubuntu 16.04

##### <a name="prerequisites-for-os-disk-encryption"></a>Wymagania wstępne dotyczące szyfrowania dysku systemu operacyjnego

* Witaj maszyny Wirtualnej musi zostać utworzona z obrazu witryny Marketplace hello Azure Resource Manager.
* Maszyna wirtualna platformy Azure z co najmniej 4 GB pamięci RAM (zalecany rozmiar to 7 GB).
* (W przypadku RHEL i CentOS) Wyłącz SELinux. toodisable SELinux, zobacz "4.4.2. Wyłączanie SELinux"w hello [Przewodnik administratora i użytkownika SELinux](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) na powitania maszyny Wirtualnej.
* Po wyłączeniu SELinux co najmniej raz ponowny rozruch hello maszyny Wirtualnej.

##### <a name="steps"></a>Kroki
1. Utwórz maszynę Wirtualną za pomocą jednego z dystrybucji hello określony wcześniej.

 7.2 CentOS szyfrowania dysku systemu operacyjnego jest obsługiwane za pomocą specjalnego obrazu. toouse to obrazów, określ "7.2n" hello SKU podczas tworzenia hello maszyny Wirtualnej:
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. Skonfiguruj zgodnie z potrzebami tooyour hello maszyny Wirtualnej. Jeśli zamierzasz tooencrypt wszystkie dyski hello (systemu operacyjnego i danych), dyski danych hello muszą toobe określonego i instalację z /etc/fstab.

 > [!NOTE]
 > Użyj identyfikatora UUID =... toospecify dysków danych w fstab/etc/zamiast określania nazwy urządzenia bloku hello (na przykład /dev/sdb1). Podczas szyfrowania, kolejność hello zmiany dysków na powitania maszyny Wirtualnej. Jeśli maszyna wirtualna opiera się na określonej kolejności urządzeń bloku, zakończy się niepowodzeniem toomount je po szyfrowania.

3. Wyloguj hello sesji SSH.

4. tooencrypt hello systemu operacyjnego, określ volumeType jako **wszystkie** lub **OS** podczas możesz [włączyć szyfrowanie](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).

 > [!NOTE]
 > Wszystkie procesy przestrzeń użytkownika, które nie są uruchomione jako `systemd` usługi powinny skasowane z `SIGKILL`. Ponowny rozruch hello maszyny Wirtualnej. Po włączeniu szyfrowania dysku systemu operacyjnego na uruchomionej maszynie Wirtualnej, należy zaplanować przestój maszyny Wirtualnej.

5. Okresowo monitorować postęp hello szyfrowania za pomocą instrukcji hello w hello [następnej sekcji](#monitoring-os-encryption-progress).

6. Po Get AzureRmVmDiskEncryptionStatus zawiera "VMRestartPending", należy ponownie uruchomić maszyny Wirtualnej, logując się tooit lub za pomocą portalu hello, programu PowerShell lub interfejsu wiersza polecenia.
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot hello VM
    ```
Przed ponownym, zaleca się zapisanie [diagnostyki rozruchu](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) z hello maszyny Wirtualnej.

#### <a name="monitoring-os-encryption-progress"></a>Monitorowanie postępu szyfrowania systemu operacyjnego
Możesz monitorować postęp szyfrowania systemu operacyjnego na trzy sposoby:

* Użyj hello `Get-AzureRmVmDiskEncryptionStatus` polecenia cmdlet i sprawdzić hello postępu pola:
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 Po hello wirtualna osiągnie "Rozpoczęto szyfrowania dysku systemu operacyjnego", trwa około 40 minutach too50 na magazyn Premium kopii maszyny Wirtualnej.

 Z powodu [wystawiać #388](https://github.com/Azure/WALinuxAgent/issues/388) w WALinuxAgent, `OsVolumeEncrypted` i `DataVolumesEncrypted` wyświetlane jako `Unknown` w niektórych dystrybucji. Z WALinuxAgent wersji 2.1.5 i później, ten problem zostanie rozwiązany automatycznie. Jeśli widzisz `Unknown` w danych wyjściowych hello, można sprawdzić stan szyfrowanie dysków za pomocą hello Eksploratora zasobów Azure.

 Przejdź za[Eksploratora zasobów Azure](https://resources.azure.com/), a następnie rozwiń węzeł tej hierarchii w hello panelu wyboru po lewej stronie:

 ~~~~
 |-- subscriptions
     |-- [Your subscription]
          |-- resourceGroups
               |-- [Your resource group]
                    |-- providers
                         |-- Microsoft.Compute
                              |-- virtualMachines
                                   |-- [Your virtual machine]
                                        |-- InstanceView
~~~~                

 W hello InstanceView przewiń w dół toosee hello stan szyfrowania dysków.

 ![Widok wystąpienia maszyny Wirtualnej](./media/azure-security-disk-encryption/vm-instanceview.png)

* Przyjrzyj się [diagnostyki rozruchu](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/). Wiadomości powitania ADE rozszerzenia musi być poprzedzona ciągiem `[AzureDiskEncryption]`.

* Zaloguj się toohello maszyny Wirtualnej za pośrednictwem SSH i Pobierz dziennik rozszerzenia powitania od:

    /var/log/Azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux

 Zaleca się, że nie podpiszesz w toohello maszyny Wirtualnej w trakcie szyfrowania systemu operacyjnego. Skopiuj dzienniki hello tylko wtedy, gdy hello dwóch innych metod nie powiodło się.

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a>Przygotowanie wstępnie zaszyfrowanego dysku VHD systemu Linux
##### <a name="ubuntu-16"></a>Ubuntu 16
Konfigurowanie szyfrowania podczas instalacji dystrybucji hello hello następujący:

1. Wybierz **skonfigurować zaszyfrowanych woluminach** po partycji dysków hello.

 ![Instalator Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. Utwórz dysk rozruchowy oddzielne, nie muszą być szyfrowane. Szyfrowanie dysku głównym.

 ![Instalator Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. Należy podać hasło. Jest to hasło hello przekazanie toohello magazynu kluczy.

 ![Instalator Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. Zakończ partycjonowania.

 ![Instalator Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. Po rozruchu hello maszyny Wirtualnej i są wyświetlane pytanie o hasło, należy używać hello hasło, podane w kroku 3.

 ![Instalator Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. Przygotowanie hello maszyny Wirtualnej do przekazywania do platformy Azure przy użyciu [tych instrukcji](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/). Nie należy jeszcze uruchamiać hello ostatni krok (hello anulowania obsługi maszyny Wirtualnej).

Skonfiguruj toowork szyfrowania z platformy Azure, wykonując następujące hello:

1. Utwórz plik w obszarze /usr/local/sbin/azure_crypt_key.sh, zawartością hello hello następującego skryptu. Należy zwrócić uwagę toohello KeyFileName, ponieważ jest nazwa pliku hasło hello używana przez platformę Azure.

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint
    modprobe vfat >/dev/null 2>&1
    modprobe ntfs >/dev/null 2>&1
    sleep 2
    OPENED=0
    cd /sys/block
    for DEV in sd*; do

        echo "> Trying device: $DEV ..." >&2
        mount -t vfat -r /dev/${DEV}1 $MountPoint >/dev/null||
        mount -t ntfs -r /dev/${DEV}1 $MountPoint >/dev/null
        if [ -f $MountPoint/$KeyFileName ]; then
                cat $MountPoint/$KeyFileName
                umount $MountPoint 2>/dev/null
                OPENED=1
                break
        fi
        umount $MountPoint 2>/dev/null
    done

      if [ $OPENED -eq 0 ]; then
        echo "FAILED toofind suitable passphrase file ..." >&2
        echo -n "Try tooenter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. Zmienianie konfiguracji crypt hello w */etc/crypttab*. Powinny wyglądać następująco:
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. Jeśli edytujesz *azure_crypt_key.sh* w systemie Windows i skopiować go tooLinux, uruchom `dos2unix /usr/local/sbin/azure_crypt_key.sh`.

4. Dodaj uprawnienia pliku wykonywalnego toohello skryptu:
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. Edytuj */etc/initramfs-tools/modules* przez dołączenie wiersze:
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. Uruchom `update-initramfs -u -k all` tooupdate hello initramfs toomake hello `keyscript` zostały zastosowane.

7. Teraz można anulowanie zastrzeżenia hello maszyny Wirtualnej.

 ![Instalator Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. Kontynuować toohello następnego kroku i [przekazać dysk VHD](#upload-encrypted-vhd-to-an-azure-storage-account) na platformie Azure.

##### <a name="opensuse-132"></a>openSUSE 13.2
szyfrowanie tooconfigure podczas instalacji dystrybucji hello hello następujące:
1. Gdy partycji dysków hello, wybierz **szyfrowania woluminu grupy**, a następnie wprowadź hasło. Jest to hasło hello przekaże tooyour magazynu kluczy.

 ![openSUSE 13.2 Instalatora](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. Witaj rozruchu maszyny Wirtualnej przy użyciu hasła.

 ![openSUSE 13.2 Instalatora](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. Przygotowanie hello maszyny Wirtualnej dla przekazywania tooAzure, wykonując następujące instrukcje hello [przygotowanie SLES lub openSUSE maszyny wirtualnej na platformie Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131). Nie należy jeszcze uruchamiać hello ostatni krok (hello anulowania obsługi maszyny Wirtualnej).

tooconfigure toowork szyfrowania z platformy Azure, hello następujące:
1. Edytuj hello /etc/dracut.conf, a następnie dodaj powitania po wierszu:
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. Komentarz te wiersze końca hello hello pliku /usr/lib/dracut/modules.d/90crypt/module-setup.sh:
 ```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
 ```

3. Dołącz hello następującego wiersza początku hello /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh pliku hello:
 ```
    DRACUT_SYSTEMD=0
 ```
I zmień wszystkich wystąpień:
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
na:
```
    if [ 1 ]; then
```
4. Edytuj /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh i dołącza je za "# Otwórz LUKS urządzenie":

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```
5. Uruchom `/usr/sbin/dracut -f -v` tooupdate hello initrd.

6. Teraz można anulowanie zastrzeżenia hello maszyny Wirtualnej i [przekazać dysk VHD](#upload-encrypted-vhd-to-an-azure-storage-account) na platformie Azure.

##### <a name="centos-7"></a>CentOS 7
szyfrowanie tooconfigure podczas instalacji dystrybucji hello hello następujące:
1. Wybierz **szyfrowania danych** po partycji dysków.

 ![Instalator centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. Upewnij się, że **Szyfruj** jest zaznaczone dla partycji katalogu głównego.

 ![Instalator centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. Należy podać hasło. Jest to hasło hello przekaże tooyour magazynu kluczy.

 ![Instalator centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. Po rozruchu hello maszyny Wirtualnej i są wyświetlane pytanie o hasło, należy używać hello hasło, podane w kroku 3.

 ![Instalator centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. Przygotowanie hello maszyny Wirtualnej do przekazywania na platformie Azure za pomocą instrukcji "CentOS 7.0 +" hello w [przygotowanie maszyny wirtualnej CentOS, oparty na platformie Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70). Nie należy jeszcze uruchamiać hello ostatni krok (hello anulowania obsługi maszyny Wirtualnej).

6. Teraz można anulowanie zastrzeżenia hello maszyny Wirtualnej i [przekazać dysk VHD](#upload-encrypted-vhd-to-an-azure-storage-account) na platformie Azure.

tooconfigure toowork szyfrowania z platformy Azure, hello następujące:

1. Edytuj hello /etc/dracut.conf, a następnie dodaj powitania po wierszu:
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. Komentarz te wiersze końca hello hello pliku /usr/lib/dracut/modules.d/90crypt/module-setup.sh:
```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
```

3. Dołącz hello następującego wiersza początku hello /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh pliku hello:
```
    DRACUT_SYSTEMD=0
```
I zmień wszystkich wystąpień:
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
na
```
    if [ 1 ]; then
```
4. Edytuj /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh i Dołącz po "# Otwórz LUKS urządzenie" hello:
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```    
5. Uruchom hello "/ usr/sbin/dracut - f - v" tooupdate hello initrd.

![Instalator centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-tooan-azure-storage-account"></a>Przekaż zaszyfrowanego dysku VHD tooan konta magazynu Azure
Po włączeniu szyfrowania funkcją BitLocker lub szyfrowania DM-Crypt lokalne powitania szyfrowane konta magazynu wirtualnego dysku twardego musi przekazać toobe tooyour.

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-hello-disk-encryption-secret-for-hello-pre-encrypted-vm-tooyour-key-vault"></a>Przekaż hello hasło szyfrowania dysków dla magazynu kluczy hello zaszyfrowane wstępnie wirtualna tooyour
klucz tajny szyfrowanie dysków hello uzyskany wcześniej, należy przekazać jako klucza tajnego w magazynie kluczy. magazyn kluczy Hello musi toohave szyfrowania dysku i uprawnienia włączona dla klienta usługi Azure AD.

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a>Hasło szyfrowania dysku nie jest zaszyfrowany przy KEK
tooset się klucz tajny hello w magazynie kluczy, użyj [AzureKeyVaultSecret zestawu](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret). Jeśli masz maszyny wirtualnej systemu Windows, plik bek hello został zakodowany jako ciąg base64 i następnie przekazać magazyn kluczy tooyour przy użyciu hello `Set-AzureKeyVaultSecret` polecenia cmdlet. Dla systemu Linux hasło hello został zakodowany jako ciąg w formacie base64, a następnie przekazać magazyn kluczy toohello. Ponadto upewnij się, że ten powitania po tagi są ustawiane podczas tworzenia hello klucza tajnego w magazynie kluczy hello.

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

Użyj hello `$secretUrl` w następnym kroku powitania dla [Trwa dołączanie dysku hello systemu operacyjnego bez użycia KEK](#without-using-a-kek).

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a>Hasło szyfrowania dysku zaszyfrowane za pomocą KEK
Przed przekazaniem magazynu kluczy tajnych toohello hello, można opcjonalnie zaszyfrować przy użyciu klucza szyfrowania. Użyj hello zawijania [interfejsu API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst zaszyfrować klucza tajnego hello przy użyciu klucza szyfrowania klucza hello. Witaj wynik tej operacji zawijania jest base64 ciągu zakodowane w adresie URL, który można następnie przekazać jako klucz tajny przy użyciu hello [ `Set-AzureKeyVaultSecret` ](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) polecenia cmdlet.

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    Add-AzureKeyVaultKey -VaultName $KeyVaultName -Name "keyencryptionkey" -Destination Software
    $KeyEncryptionKey = Get-AzureKeyVaultKey -VaultName $KeyVault.OriginalVault.Name -Name "keyencryptionkey"

    $apiversion = "2015-06-01"

    ##############################
    # Get Auth URI
    ##############################

    $uri = $KeyVault.VaultUri + "/keys"
    $headers = @{}

    $response = try { Invoke-RestMethod -Method GET -Uri $uri -Headers $headers } catch { $_.Exception.Response }

    $authHeader = $response.Headers["www-authenticate"]
    $authUri = [regex]::match($authHeader, 'authorization="(.*?)"').Groups[1].Value

    Write-Host "Got Auth URI successfully"

    ##############################
    # Get Auth Token
    ##############################

    $uri = $authUri + "/oauth2/token"
    $body = "grant_type=client_credentials"
    $body += "&client_id=" + $AadClientId
    $body += "&client_secret=" + [Uri]::EscapeDataString($AadClientSecret)
    $body += "&resource=" + [Uri]::EscapeDataString("https://vault.azure.net")
    $headers = @{}

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $access_token = $response.access_token

    Write-Host "Got Auth Token successfully"

    ##############################
    # Get KEK info
    ##############################

    $uri = $KeyEncryptionKey.Id + "?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token}

    $response = Invoke-RestMethod -Method GET -Uri $uri -Headers $headers

    $keyid = $response.key.kid

    Write-Host "Got KEK info successfully"

    ##############################
    # Encrypt passphrase using KEK
    ##############################

    $passphraseB64 = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($Passphrase))
    $uri = $keyid + "/encrypt?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"alg" = "RSA-OAEP"; "value" = $passphraseB64}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $wrappedSecret = $response.value

    Write-Host "Encrypted passphrase successfully"

    ##############################
    # Store secret
    ##############################

    $secretName = [guid]::NewGuid().ToString()
    $uri = $KeyVault.VaultUri + "/secrets/" + $secretName + "?api-version=" + $apiversion
    $secretAttributes = @{"enabled" = $true}
    $secretTags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"value" = $wrappedSecret; "attributes" = $secretAttributes; "tags" = $secretTags}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method PUT -Uri $uri -Headers $headers -Body $body

    Write-Host "Stored secret successfully"

    $secretUrl = $response.id

Użyj `$KeyEncryptionKey` i `$secretUrl` w następnym kroku powitania dla [Trwa dołączanie dysku hello systemu operacyjnego przy użyciu KEK](#using-a-kek).

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a>Określ adres URL tajne, po podłączeniu dysku systemu operacyjnego
#### <a name="without-using-a-kek"></a>Bez użycia KEK
Podczas dołączania dysku hello systemu operacyjnego, należy toopass `$secretUrl`. adres URL Hello został wygenerowany w sekcji "nie jest zaszyfrowany przy KEK tajny szyfrowanie dysków" hello.

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a>Przy użyciu KEK
Po podłączeniu dysku systemu operacyjnego hello przekazać `$KeyEncryptionKey` i `$secretUrl`. adres URL Hello został wygenerowany w sekcji "nie jest zaszyfrowany przy KEK tajny szyfrowanie dysków" hello.

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $CopiedTemplateBlobUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl `
            -KeyEncryptionKeyVaultId $KeyVault.ResourceId `
            -KeyEncryptionKeyURL $KeyEncryptionKey.Id

## <a name="download-this-guide"></a>Pobierz w tym przewodniku
W tym przewodniku można pobrać z hello [galerii TechNet](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).

## <a name="for-more-information"></a>Aby uzyskać więcej informacji
[Eksploruj szyfrowania dysków Azure przy użyciu programu Azure PowerShell — część 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[Eksploruj szyfrowania dysków Azure przy użyciu programu Azure PowerShell — część 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
