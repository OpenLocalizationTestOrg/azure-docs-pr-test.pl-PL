---
title: Kopia zapasowa HANA Azure aaaSAP oparte na magazynu migawek | Dokumentacja firmy Microsoft
description: "Istnieją dwa główne kopii zapasowej możliwości SAP HANA na maszynach wirtualnych Azure, w tym artykule omówiono SAP HANA kopię zapasową pamięci masowej migawki"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ums.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 3/13/2017
ms.author: rclaus
ms.openlocfilehash: 32bb80f5a928a2cf63699bfe4f4cf5bbad81e6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-backup-based-on-storage-snapshots"></a>Kopie zapasowe oprogramowania SAP HANA na podstawie migawek magazynu

## <a name="introduction"></a>Wprowadzenie

To jest częścią serii trzyczęściowej pokrewne artykuły kopii zapasowej SAP HANA. [Podręcznik tworzenia kopii zapasowej programu SAP HANA na maszynach wirtualnych Azure](sap-hana-backup-guide.md) zawiera omówienie i informacje wprowadzające, i [SAP HANA kopia zapasowa Azure na poziomie plików](sap-hana-backup-file-level.md) obejmuje hello opcję tworzenia kopii zapasowych opartych na plikach.

W przypadku używania funkcji Kopia zapasowa maszyny Wirtualnej dla systemu jednego wystąpienia w jednym demonstracyjnej, co należy rozważyć, wykonanie kopii zapasowej maszyny Wirtualnej, zamiast zarządzania HANA tworzenia kopii zapasowych na powitania poziomu systemu operacyjnego. Alternatywą jest tootake obiektów blob platformy Azure migawki toocreate kopie poszczególnych dysków wirtualnych, które są dołączone tooa maszyny wirtualnej, a także zapewnić hello HANA dane plików. Ale punktu krytycznego spójności aplikacji podczas tworzenia migawki kopii zapasowej lub dysku maszyny Wirtualnej, gdy hello system jest uruchomiony i uruchomiony. Zobacz _spójność danych SAP HANA podejmując magazynu migawek_ w artykule pokrewne hello [Podręcznik tworzenia kopii zapasowej programu SAP HANA na maszynach wirtualnych Azure](sap-hana-backup-guide.md). SAP HANA jest funkcją, która obsługuje następujące rodzaje pamięci masowej migawki.

## <a name="sap-hana-snapshots"></a>SAP HANA migawki

Brak funkcji w SAP HANA, który obsługuje tworzenie migawki magazynu. Jednak począwszy od grudnia 2016 r. istnieje ograniczenie systemów toosingle kontenera. Konfiguracje wielodostępnym kontenera nie obsługują tego rodzaju migawki bazy danych (zobacz [tworzenia magazynu migawek (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm)).

Działa on w następujący sposób:

- Przygotowanie do migawki magazynu inicjując hello SAP HANA migawki
- Uruchom hello magazynu migawek (Azure blob migawki, na przykład)
- Potwierdź hello SAP HANA migawki

![Ten zrzut ekranu pokazuje, że migawki danych SAP HANA można tworzyć za pomocą instrukcji SQL](media/sap-hana-backup-storage-snapshots/image011.png)

Ten zrzut ekranu pokazuje, że migawki danych SAP HANA można tworzyć za pomocą instrukcji SQL.

![następnie migawki Hello jest także wyświetlany w katalogu kopii zapasowej hello w SAP HANA Studio](media/sap-hana-backup-storage-snapshots/image012.png)

następnie migawki Hello jest także wyświetlany w katalogu kopii zapasowej hello w SAP HANA Studio.

![Na dysku hello migawki zostaną wyświetlone w katalogu danych SAP HANA hello](media/sap-hana-backup-storage-snapshots/image013.png)

Na dysku hello migawki zostaną wyświetlone w katalogu danych SAP HANA hello.

Jeden ma tooensure, który spójności systemu plików hello jest gwarantowana przed uruchomieniem hello pamięci masowej migawki podczas w trybie przygotowania migawki hello SAP HANA. Zobacz _spójność danych SAP HANA podejmując magazynu migawek_ w artykule pokrewne hello [Podręcznik tworzenia kopii zapasowej programu SAP HANA na maszynach wirtualnych Azure](sap-hana-backup-guide.md).

Po zakończeniu hello pamięci masowej migawki jest krytyczne tooconfirm hello SAP HANA migawki. Brak odpowiedniego toorun instrukcji SQL: Zamknij MIGAWKI danych kopii zapasowej (zobacz [danych zamknij MIGAWKI instrukcji BACKUP (kopii zapasowych i odzyskiwania)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/9739966f7f4bd5818769ad4ce6a7f8/content.htm)).

> [!IMPORTANT]
> Potwierdź hello HANA migawki. Z powodu zbyt&quot;kopii przy zapisie,&quot; SAP HANA mogą wymagać dodatkowego miejsca na dysku w migawki — przygotowanie trybu i nie jest możliwe toostart nowych kopii zapasowych do momentu hello SAP HANA migawki został potwierdzony.

## <a name="hana-vm-backup-via-azure-backup-service"></a>Maszyna wirtualna HANA tworzenia kopii zapasowej za pomocą usługi Kopia zapasowa Azure

Począwszy od grudnia 2016 r. hello agenta kopii zapasowej hello usługi Kopia zapasowa Azure nie jest dostępna dla maszyn wirtualnych systemu Linux. toomake korzystanie z platformy Azure kopii zapasowej na poziomie pliku/katalogu hello, czy jeden skopiuj SAP HANA tooa pliki kopii zapasowej maszyny Wirtualnej systemu Windows i następnie użyj hello agenta kopii zapasowej. W przeciwnym razie tylko pełna kopia maszyny Wirtualnej systemu Linux jest możliwe za pomocą usługi Kopia zapasowa Azure hello. Zobacz [omówienie hello funkcji w usłudze Kopia zapasowa Azure](../../../backup/backup-introduction-to-azure-backup.md) toofind się więcej.

Witaj usługi Kopia zapasowa Azure zapewnia tooback opcji i przywracania maszyny Wirtualnej. Więcej informacji na temat tej usługi oraz sposób jej działania można znaleźć w artykule hello [Zaplanuj infrastrukturę kopii zapasowej maszyny Wirtualnej na platformie Azure](../../../backup/backup-azure-vms-introduction.md).

Istnieją dwa istotne kwestie, zgodnie z artykułem toothat:

_&quot;Dla maszyn wirtualnych systemu Linux tylko plik spójne kopie zapasowe są możliwe, ponieważ systemu Linux nie ma tooVSS równoważnej platformy.&quot;_

_&quot;Aplikacje muszą tooimplement własnych &quot;konfigurowania&quot; mechanizmu na powitania przywrócić dane.&quot;_

W związku z tym jeden ma toomake się, że SAP HANA jest spójna na dysku, po uruchomieniu hello kopii zapasowej. Zobacz _migawki SAP HANA_ opisem we wcześniejszej części hello dokumentu. Potencjalny problem występuje, gdy SAP HANA pozostaje w tym trybie przygotowania migawki Zobacz [tworzenia magazynu migawek (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm) Aby uzyskać więcej informacji.

Ten artykuł stanowi:

_&quot;Zdecydowanie zaleca się tooconfirm lub Porzuć migawki magazynu jak najszybciej po jego utworzeniu. Podczas hello pamięci masowej migawki są przygotowywane lub utworzone, hello migawkę odpowiednich danych jest zablokowana. Gdy hello migawkę odpowiednich danych jest zablokowany, nadal zmian w hello bazy danych. Takie zmiany nie spowoduje hello zablokowane zmienić toobe migawkę odpowiednich danych. Zamiast tego zmiany hello są zapisywane toopositions w obszarze danych hello, które są niezależne od hello pamięci masowej migawki. Zmiany są także zapisywane toohello dziennika. Jednak hello dłużej hello migawkę odpowiednich danych jest przechowywana zablokowane, hello więcej powitalne może zwiększyć ilość danych.&quot;_

Kopia zapasowa Azure zapewnia obsługę hello spójności systemu plików za pośrednictwem rozszerzenia maszyny Wirtualnej platformy Azure. Rozszerzenia te nie są dostępne autonomicznej i działa tylko w połączeniu z usługą kopia zapasowa Azure. Niemniej jednak nadal jest wymaganie toomanage SAP HANA migawki tooguarantee aplikacji spójności.

Kopia zapasowa Azure ma dwa główne fazy:

- Utwórz migawkę
- Transfer danych toovault

Dlatego można potwierdzić hello SAP HANA migawki po zakończeniu hello kopia zapasowa Azure usługa fazy wykonywania migawki. Może upłynąć kilka minut toosee w hello portalu Azure.

![Na poniższym rysunku pokazano hello zadanie tworzenia kopii zapasowej listy usługi Kopia zapasowa Azure](media/sap-hana-backup-storage-snapshots/image014.png)

Na poniższym rysunku pokazano hello zadanie tworzenia kopii zapasowej listy usługi Kopia zapasowa Azure, która była używana tooback się hello HANA testowej maszyny Wirtualnej.

![Szczegóły zadania hello tooshow, kliknij przycisk hello zadanie tworzenia kopii zapasowej w hello portalu Azure](media/sap-hana-backup-storage-snapshots/image015.png)

tooshow hello szczegóły zadania, kliknij zadanie tworzenia kopii zapasowej hello w hello portalu Azure. Tutaj jedną zobaczyć Witaj dwie fazy. Może upłynąć kilka minut, aż fazy migawki hello będzie wyświetlana jako ukończone. W większości przypadków hello jest poświęcony na etapie hello transferu danych.

## <a name="hana-vm-backup-automation-via-azure-backup-service"></a>Maszyna wirtualna HANA automatyzacji tworzenia kopii zapasowej za pomocą usługi Kopia zapasowa Azure

Jeden można potwierdzić ręcznie hello SAP HANA migawki po kopia zapasowa Azure faza migawki hello jest zakończona, jak opisano wcześniej, ale jest automatyzacji tooconsider przydatne, ponieważ administrator nie może monitorować zadanie tworzenia kopii zapasowej hello na liście hello portalu Azure.

W tym miejscu jest wyjaśnienie, jak można można zrealizować przy użyciu poleceń cmdlet programu Azure PowerShell.

![Usługa Kopia zapasowa Azure została utworzona przy hello nazwa hana magazynu kopii zapasowej —](media/sap-hana-backup-storage-snapshots/image016.png)

Usługa Kopia zapasowa Azure została utworzona o nazwie hello &quot;hana-kopii zapasowej-magazynu.&quot; hello polecenia PS **Get AzureRmRecoveryServicesVault-nazwa magazynu w przypadku kopii zapasowych hana** pobiera hello odpowiedni obiekt. Ten obiekt jest następnie używane tooset hello kontekstu kopii zapasowych, jak pokazano na rysunku dalej hello.

![Jeden sprawdzaj hello zadanie tworzenia kopii zapasowej w toku](media/sap-hana-backup-storage-snapshots/image017.png)

Po ustawienie hello poprawny kontekst jedna Sprawdź, czy zadanie tworzenia kopii zapasowej hello w toku i poszukaj jego szczegóły zadania. Lista podzadanie Hello zawiera, jeśli fazy migawki hello hello Azure zadanie tworzenia kopii zapasowej jest już ukończone:

```
$ars = Get-AzureRmRecoveryServicesVault -Name hana-backup-vault
Set-AzureRmRecoveryServicesVaultContext -Vault $ars
$jid = Get-AzureRmRecoveryServicesBackupJob -Status InProgress | select -ExpandProperty jobid
Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
```

![Wartość hello sondowania w pętli do momentu Monitor przechodzi w stan tooCompleted](media/sap-hana-backup-storage-snapshots/image018.png)

Po hello szczegóły zadania są przechowywane w zmiennej, to po prostu PS składni tooget toohello pierwszy wpisem w tablicy i pobrać wartość stanu hello. skrypt automatyzacji hello toocomplete, wartość hello sondowania w pętli, dopóki powoduje zbyt&quot;ukończone.&quot;

```
$st = Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
$st[0] | select -ExpandProperty status
```

## <a name="hana-license-key-and-vm-restore-via-azure-backup-service"></a>Klucz licencji HANA i wirtualna przywrócić za pomocą usługi Kopia zapasowa Azure

Witaj usługi Kopia zapasowa Azure jest zaprojektowana toocreate nowej maszyny Wirtualnej podczas przywracania. Brak nie plan prawym teraz toodo &quot;w miejscu&quot; przywracania istniejącej maszyny Wirtualnej platformy Azure.

![Na poniższym rysunku pokazano opcji przywracania hello hello usługi Azure w portalu Azure hello](media/sap-hana-backup-storage-snapshots/image019.png)

Na poniższym rysunku pokazano opcji przywracania hello hello usługi Azure w hello portalu Azure. Można między tworzenia maszyny Wirtualnej podczas przywracania lub przywracanie hello dysków. Po przywróceniu hello dysków, jest nadal konieczne toocreate nowej maszyny Wirtualnej znajdujący się na nim. Po każdej zmianie nowej maszyny Wirtualnej jest tworzony na Azure hello Unikatowy identyfikator maszyny Wirtualnej zmiany (zobacz [dostęp i przy użyciu usługi Azure VM Unikatowy identyfikator](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/)).

![Na poniższym rysunku pokazano Unikatowy identyfikator maszyny Wirtualnej Azure hello przed i po przywróceniu hello za pomocą usługi Kopia zapasowa Azure](media/sap-hana-backup-storage-snapshots/image020.png)

Na poniższym rysunku pokazano Unikatowy identyfikator maszyny Wirtualnej Azure hello przed i po przywróceniu hello za pomocą usługi Kopia zapasowa Azure. Witaj SAP sprzętu klucz, który jest używany do licencjonowania SAP, używa to unikatowy identyfikator maszyny Wirtualnej. W konsekwencji nowej licencji SAP ma toobe zainstalowane po przywróceniu maszyn wirtualnych.

Nowa funkcja Kopia zapasowa Azure został przedstawiony w wersji zapoznawczej podczas tworzenia hello niniejszego przewodnika tworzenia kopii zapasowej. Umożliwia przywrócenie poziomu pliku oparte na powitania migawki maszyny Wirtualnej, która została wykonana dla maszyny Wirtualnej hello kopii zapasowej. Dzięki temu można uniknąć toodeploy potrzeby hello nowej maszyny Wirtualnej i w związku z tym hello Unikatowy identyfikator maszyny Wirtualnej pozostaje hello takie same i jest wymagane nie nowy klucz licencji SAP HANA. Więcej dokumentacji na ta funkcja będzie dostępna po został w pełni przetestowany.

Kopia zapasowa Azure ostatecznie umożliwi kopii zapasowej poszczególnych dysków wirtualnych platformy Azure, a także pliki i katalogi z wewnątrz hello maszyny Wirtualnej. Główną zaletą usługi Kopia zapasowa Azure jest jego zarządzania wszystkie kopie zapasowe hello, zapisywanie powitania klienta z konieczności toodo go. Jeśli niezbędne przywracania kopii zapasowej Azure wybierze hello poprawne toouse kopii zapasowej.

## <a name="sap-hana-vm-backup-via-manual-disk-snapshot"></a>Kopia zapasowa maszyny Wirtualnej programu SAP HANA za pomocą migawki ręczne dysku

Zamiast przy użyciu usługi Kopia zapasowa Azure hello, co może skonfigurować poszczególnych tworzenia kopii zapasowych przez tworzenie migawek obiektów blob Azure wirtualne dyski twarde ręcznie za pomocą programu PowerShell. Zobacz [migawki obiektu blob korzystanie z programu PowerShell](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/) opis kroków hello.

Zapewnia większą elastyczność, ale nie rozwiązuje problemy hello wyjaśniono wcześniej w tym dokumencie:

- Jeden nadal należy się upewnić, że SAP HANA jest spójne
- Nie można zastąpić Hello dysk systemu operacyjnego, nawet jeśli istnieje powitalne cofnięciu ze względu na komunikat o błędzie informujący, że dzierżawy. Działa tylko po usunięcie hello maszynę Wirtualną, co może spowodować tooa nowy unikatowy identyfikator maszyny Wirtualnej i hello potrzeby tooinstall nowej licencji SAP.

![Jest możliwe toorestore tylko hello danych dyski maszyny Wirtualnej platformy Azure](media/sap-hana-backup-storage-snapshots/image021.png)

Jest możliwe toorestore tylko dyski danych hello maszyny Wirtualnej platformy Azure, unikając problem hello pobierania nowy unikatowy identyfikator maszyny Wirtualnej i, w związku z tym unieważnienie licencji SAP hello:

- Dla testu hello dwóch dysków danych Azure zostały dołączone tooa maszyny Wirtualnej i oprogramowaniem RAID został zdefiniowany oparte na nich 
- Funkcja migawki SAP HANA potwierdzono, że SAP HANA była w spójnym stanie
- Zablokuj systemu plików (zobacz _spójność danych SAP HANA podejmując magazynu migawek_ w artykule pokrewne hello [Podręcznik tworzenia kopii zapasowej programu SAP HANA na maszynach wirtualnych Azure](sap-hana-backup-guide.md))
- Migawki obiektu blob zostały pobrane z obu dysków z danymi
- Odblokuj systemu plików
- Potwierdzenie migawki SAP HANA
- dyski danych hello toorestore, hello maszyny Wirtualnej został zamknięty i obydwa dyski odłączone
- Po odłączanie hello dysków, zostały zastąpione z migawkami wcześniejsze blob hello
- Zostały dołączone dyski wirtualne hello przywrócone, a następnie ponownie toohello maszyny Wirtualnej
- Po początkowej hello maszyny Wirtualnej, wszystko na powitania oprogramowania RAID działał prawidłowo i został ponownie ustawiony toohello obiektu blob migawki czasu
- HANA ustawiono ponownie toohello HANA migawki

Jeśli jest możliwe tooshut dół SAP HANA przed migawki obiektu blob hello procedura hello jest mniej złożona. W takim przypadku jeden można pominąć hello HANA migawki i, jeśli nic dzieje się w systemie hello też pominąć blokowanie system plików hello. Dodano złożoności wejścia obraz powitania, gdy jest konieczne toodo migawki podczas, gdy wszystko jest w trybie online. Zobacz _spójność danych SAP HANA podejmując magazynu migawek_ w artykule pokrewne hello [Podręcznik tworzenia kopii zapasowej programu SAP HANA na maszynach wirtualnych Azure](sap-hana-backup-guide.md).

## <a name="next-steps"></a>Następne kroki
* [Podręcznik tworzenia kopii zapasowej programu SAP HANA na maszynach wirtualnych Azure](sap-hana-backup-guide.md) zapewnia przegląd oraz informacje o wprowadzenie.
* [Kopia zapasowa SAP HANA oparte na poziomie plików](sap-hana-backup-file-level.md) obejmuje hello opcję tworzenia kopii zapasowych opartych na plikach.
* toolearn jak tooestablish wysokiej dostępności i planu odzyskiwania po awarii programu SAP HANA na platformie Azure (wystąpienia duże), zobacz [SAP HANA (duże wystąpień) wysokiej dostępności i odzyskiwania po awarii na platformie Azure](hana-overview-high-availability-disaster-recovery.md).
