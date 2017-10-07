---
title: "aaaOptimize MySQL wydajności w systemie Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toooptimize MySQL uruchomionych na maszynie wirtualnej platformy Azure (VM) systemem Linux."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0c1c7fc5-a528-4d84-b65d-2df225f2233f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: ningk
ms.openlocfilehash: 9e6458723233721e06f30b9de33635d403eefcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a>Optymalizowanie MySQL na maszynach wirtualnych systemu Linux platformy Azure
Istnieje wiele czynników, które mają wpływ na wydajność MySQL na platformie Azure, zarówno w wybór sprzęt wirtualny i konfiguracji oprogramowania. Ten artykuł dotyczy Optymalizacja wydajności za pomocą magazynu, systemu i konfiguracje bazy danych.

> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager](../../../resource-manager-deployment-model.md) i klasycznym. W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Informacje o optymalizacji maszyny Wirtualnej systemu Linux z modelu Resource Manager hello, zobacz [optymalizacji sieci maszyny Wirtualnej systemu Linux na platformie Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="utilize-raid-on-an-azure-virtual-machine"></a>Korzystanie z RAID na maszynie wirtualnej platformy Azure
Magazyn jest hello kluczowym czynnikiem wpływającym na wydajność bazy danych w środowisku chmury. Jeden dysk w porównaniu tooa RAID zapewnia szybszy dostęp za pośrednictwem współbieżności. Aby uzyskać więcej informacji, zobacz [poziomy RAID standardowe](http://en.wikipedia.org/wiki/Standard_RAID_levels).   

Można zwiększyć przepływność We/Wy dysku i czas odpowiedzi operacji We/Wy na platformie Azure za pomocą macierzy RAID. Nasze testy laboratorium wskazują, że przepustowość operacji We/Wy dysku może być podwójny i czas odpowiedzi operacji We/Wy, można zmniejszyć o połowę średnio po hello liczba dysków RAID jest podwójny (od toofour dwa, cztery tooeight itp.). Zobacz [dodatek a.](#AppendixA) szczegółowe informacje.  

Ponadto toodisk we/wy, MySQL wydajności poprawia wraz ze zwiększeniem hello poziom RAID.  Zobacz [dodatek B](#AppendixB) szczegółowe informacje.  

Można także rozmiar fragmentu hello tooconsider. Ogólnie rzecz biorąc Jeśli masz większy rozmiar fragmentu otrzymasz niższe nakładów pracy, zwłaszcza w przypadku dużych operacji zapisu. Jednak gdy rozmiar fragmentu hello jest zbyt duży, może dodawać dodatkowe obciążenie, który uniemożliwia wykorzystaniu RAID. Bieżący rozmiar domyślny Hello jest 512 KB, który jest sprawdzone toobe optymalne dla większości środowisk produkcyjnych. Zobacz [dodatku C](#AppendixC) szczegółowe informacje.   

Istnieją ograniczenia liczby dysków dla typów inną maszynę wirtualną można dodać. Te limity wyszczególnione w [maszyny wirtualnej i w chmurze rozmiary usługi Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx). Konieczne będzie cztery danych dołączonych dysków toofollow RAID przykład Witaj w tym artykule, chociaż można wybrać tooset się RAID z mniejszą liczbę dysków.  

W tym artykule przyjęto założenie, zostały już utworzone maszyny wirtualnej systemu Linux i MYSQL zainstalowany i skonfigurowany. Aby uzyskać więcej informacji na wprowadzenie, zobacz temat jak tooinstall MySQL na platformie Azure.  

### <a name="set-up-raid-on-azure"></a>— Konfiguracja RAID na platformie Azure
Witaj poniższej procedurze pokazano, jak RAID toocreate na platformie Azure przy użyciu hello portalu Azure. Można również skonfigurować RAID za pomocą skryptów środowiska Windows PowerShell.
W tym przykładzie będzie skonfigurowanie RAID 0 z czterech dysków.  

#### <a name="add-a-data-disk-tooyour-virtual-machine"></a>Dodaj maszynę wirtualną tooyour dysk danych
W hello portalu Azure przejdź do pulpitu nawigacyjnego toohello i wybierz hello toowhich maszyny wirtualnej ma tooadd dysk z danymi. W tym przykładzie maszyna wirtualna hello jest mysqlnode1.  

<!--![Virtual machines][1]-->

Kliknij przycisk **dysków** , a następnie kliknij przycisk **dołączyć nowy**.

![Maszyny wirtualne, Dodaj dysk](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

Utwórz nowy dysk 500 GB. Upewnij się, że **hosta pamięci podręcznej preferencji** ustawiono zbyt**Brak**.  Po zakończeniu kliknij przycisk **OK**.

![Dołącz pusty dysk](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


Spowoduje to dodanie jednego pusty dysk do maszyny wirtualnej. Powtórz ten krok trzy razy, aby mieć cztery dyski danych macierzy RAID.  

Zostanie wyświetlony hello dodane dyski na maszynie wirtualnej hello analizując hello jądra wiadomości dziennika. Na przykład toosee to na Ubuntu, hello Użyj następującego polecenia:  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-hello-additional-disks"></a>Utwórz RAID z hello dodatkowych dysków
Witaj poniższych krokach opisano sposób zbyt[należy skonfigurować oprogramowanie RAID w systemie Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

> [!NOTE]
> Jeśli używasz systemu plików XFS hello wykonać powitania po utworzeniu RAID wykonaj następujące kroki.
>
>

tooinstall XFS na Debian, Ubuntu lub mennic Linux hello Użyj następującego polecenia:  

    apt-get -y install xfsprogs  

tooinstall XFS na Fedora, CentOS lub RHEL, hello Użyj następującego polecenia:  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a>Konfigurowanie nowej ścieżki do magazynu
Witaj Użyj następującego polecenia tooset ścieżkę nowego magazynu:  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-hello-original-data-toohello-new-storage-path"></a>Skopiuj hello oryginalne dane toohello nowej ścieżki do magazynu
Witaj Użyj następującego polecenia toocopy danych toohello nowej ścieżki do magazynu:  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-hello-data-disk"></a>Modyfikowanie uprawnień dostępu do MySQL (odczytu i zapisu) hello dysk danych
Użyj następujących uprawnień toomodify polecenia hello:  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-hello-disk-io-scheduling-algorithm"></a>Dostosuj planowania algorytm we/wy hello dysku
Linux implementuje cztery typy operacji We/Wy planowania algorytmów:  

* Operacja algorytm (operacja: No)
* Algorytm ostateczny termin (terminu)
* Całkowicie odpowiedniego algorytmu kolejkowania wiadomości (CFQ)
* Algorytm okresu budżetu (Anticipatory)  

Można wybrać różne planiści we/wy w różnych scenariuszy toooptimize wydajności. W środowisku dostępu losowy nie istnieje znacząca różnica między hello CFQ i algorytmy terminu wydajności. Firma Microsoft zaleca ustawienie hello MySQL bazy danych środowiska tooDeadline stabilności. W przypadku partii sekwencyjnych operacji We/Wy, CFQ może zmniejszyć wydajność We/Wy dysku.   

Dysków SSD i innych urządzeń operacja lub ostatecznego terminu można osiągnąć lepszą wydajność niż hello domyślnego harmonogramu.   

Wcześniejsze toohello jądra 2.5, planowania algorytm hello domyślne we/wy jest terminu. Począwszy od jądra hello 2.6.18 CFQ stał się we/wy hello domyślny algorytm planowania.  Można określić tego ustawienia w czasie rozruchu jądra lub dynamicznie zmodyfikować to ustawienie, gdy hello w systemie.  

Witaj poniższy przykład pokazuje, jak domyślny harmonogram toohello operacja algorytm rodziny Debian dystrybucji hello hello toocheck i zestawu.  

### <a name="view-hello-current-io-scheduler"></a>Widok hello bieżącego harmonogramu we/wy
Harmonogram hello tooview Uruchom hello następujące polecenie:  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

Zostaną wyświetlone następujące dane wyjściowe, co oznacza hello bieżącego harmonogramu:  

    noop [deadline] cfq


### <a name="change-hello-current-device-devsda-of-hello-io-scheduling-algorithm"></a>Zmień hello bieżącego urządzenia (/ dev/sda) algorytmu planowania hello we/wy
Uruchom następujące polecenia toochange hello bieżącego urządzenia hello:  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> Ustawienie to dla /dev/sda nie jest użyteczne. Należy ją ustawić na wszystkich dyskach danych lokalizację hello bazy danych.  
>
>

Powinny pojawić się hello następujące dane wyjściowe, wskazując, że grub.cfg został przebudowany pomyślnie i tym hello domyślny harmonogram został zaktualizowany tooNOOP:  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

Dla hello Red Hat dystrybucji rodziny należy tylko hello następujące polecenie:

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a>Skonfiguruj ustawienia operacji pliku systemu
Jeden najlepszym rozwiązaniem jest toodisable hello *atime* funkcji rejestrowania w systemie plików hello. Atime jest hello czas ostatniego dostępu do pliku. Zawsze, gdy plik jest dostępny, rekordy systemu plików hello hello sygnatury czasowej w dzienniku hello. Jednak te informacje jest rzadko używana. Można ją wyłączyć, jeśli nie jest potrzebna, co zmniejsza całkowity czas dostępu do dysku.  

toodisable atime rejestrowanie, należy toomodify hello pliku system konfiguracji plik/etc / fstab i dodać hello **noatime** opcji.  

Na przykład Edytuj plik /etc/fstab vim hello Dodawanie hello noatime, jak pokazano w hello następujące przykładowe:  

    # CLOUD_IMG: This file was created/modified by hello Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add hello “noatime” option below toodisable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

Następnie zainstaluj system plików hello z hello następujące polecenie:  

    mount -o remount /RAID0

Test hello zmodyfikować wyniku. Po zmodyfikowaniu pliku testowego hello hello czas dostępu nie jest aktualizowana. Witaj w następujących przykładach, jaki kod hello wygląda przed i po modyfikacji.

Przed:        

![Kod przed modyfikacją dostępu][5]

Po:

![Kod po modyfikacji dostępu][6]

## <a name="increase-hello-maximum-number-of-system-handles-for-high-concurrency"></a>Zwiększ hello maksymalną liczbę systemu obsługuje dla wysokiej współbieżności
MySQL jest wysoka współbieżności bazy danych. Hello domyślna liczba równoczesnych dojścia jest 1024 dla systemu Linux, które nie zawsze jest wystarczające. Użyj hello następujące kroki tooincrease hello maksymalną równoczesnych uchwyty hello systemu toosupport wysokiej współbieżności MySQL.

### <a name="modify-hello-limitsconf-file"></a>Modyfikowanie pliku limits.conf hello
tooincrease hello maksymalna dozwolona współbieżnych dojść, Dodaj następujące cztery wiersze w pliku /etc/security/limits.conf hello hello. Należy pamiętać, że 65536 hello maksymalną liczbę obsługujących hello systemu.   

    * elastyczne nofile 65536
    * twarde nofile 65536
    * elastyczne nproc 65536
    * twarde nproc 65536

### <a name="update-hello-system-for-hello-new-limits"></a>Zaktualizuj system hello hello nowych limitów
tooupdate hello systemu, uruchom następujące polecenia hello:  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-hello-limits-are-updated-at-boot-time"></a>Upewnij się, że limity hello są aktualizowane w czasie rozruchu
Umieść powitania po uruchamiania poleceń w pliku /etc/rc.local hello tak zacznie obowiązywać w czasie rozruchu.  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a>Optymalizacja bazy danych MySQL
tooconfigure MySQL na platformie Azure, można użyć hello tej samej strategii dostrajania wydajności używany na maszynie lokalnej.  

Witaj głównego we/wy optymalizacji reguły są następujące:   

* Zwiększ rozmiar pamięci podręcznej hello.
* Zmniejsz we/wy, czas odpowiedzi.  

ustawienia serwera MySQL toooptimize, należy zaktualizować hello my.cnf pliku, który jest hello domyślny plik konfiguracji dla komputerów klienckich i serwera.  

Witaj konfiguracji są następujące elementy hello główne czynniki wpływające na wydajność MySQL:  

* **innodb_buffer_pool_size**: hello Pula buforów zawiera buforowane dane i hello indeksu. Jest to zwykle ustawione too70 procent pamięci fizycznej.
* **innodb_log_file_size**: rozmiar dziennika Powtórz hello. Możesz użyć Powtórz tooensure dzienniki, czy operacje zapisu są szybkie, niezawodne i możliwe do odzyskania po awarii. To jest ustawienie too512 MB, co zapewni wystarczająco dużo miejsca do rejestrowania operacji zapisu.
* **max_connections**: czasami aplikacje nie zamykaj połączeń poprawnie. Im większa wartość zapewni powitania serwera więcej czasu toorecycle idled połączenia. Maksymalna liczba połączeń Hello jest 10 000, ale hello zaleca się, że liczba maksymalna to 5000.
* **Innodb_file_per_table**: to ustawienie włącza lub wyłącza możliwość hello InnoDB toostore tabel w oddzielnych plikach. Włącz tooensure opcji hello wydajnie zastosować kilka operacji zaawansowane administracji. Z punktu widzenia wydajności można przyspieszyć hello tabeli miejsca transmisji i optymalizowanie zarządzania pozostałości hello. Witaj zaleca się, że ustawienie dla tej opcji jest włączone.</br></br>
Z MySQL 5.6 hello domyślne ustawienie ma wartość ON, więc nie jest wymagana żadna akcja. We wcześniejszych wersjach hello domyślne ustawienie ma wartość OFF. Ustawienie Hello należy zmienić przed załadowaniem danych, ponieważ dotyczy tylko tabele nowo utworzony.
* **innodb_flush_log_at_trx_commit**: hello wartość domyślna to 1, z hello zakresu Ustaw too0 ~ 2. Wartość domyślna Hello jest hello najbardziej odpowiednią opcją do autonomicznej bazy danych MySQL. Ustawienie Hello 2 umożliwia hello większości integralność danych i nadaje się do głównego w klaster programu MySQL. Ustawienie Hello 0 umożliwia utraty danych, które mogą wpłynąć na niezawodność (w niektórych przypadkach z lepszą wydajność) i nadaje się do podrzędnych w klaster programu MySQL.
* **Innodb_log_buffer_size**: hello dziennika buforu umożliwia toorun transakcji bez konieczności tooflush hello dziennika toodisk przed hello transakcji zatwierdzania. Jednak jeśli istnieje dużego obiektu binarnego lub pola tekstowego, hello pamięci podręcznej będą działały szybko i we/wy dysku częste zostanie wyzwolony. Jest lepiej Zwiększ rozmiar buforu hello, jeśli Innodb_log_waits zmiennej stanu nie jest 0.
* **query_cache_size**: hello najlepszym rozwiązaniem jest toodisable go z początku hello. Ustaw too0 query_cache_size (jest to domyślne ustawienie hello MySQL 5.6) i używać innych metod toospeed się zapytania.  

Zobacz [dodatku D](#AppendixD) porównanie wydajności przed i po hello optymalizacji.

## <a name="turn-on-hello-mysql-slow-query-log-for-analyzing-hello-performance-bottleneck"></a>Włącz dziennik powolne zapytań MySQL hello do analizowania hello wąskie gardło
Dziennik zapytań powolne MySQL Hello pomaga określić hello powolne zapytania dla programu MySQL. Po włączeniu dziennika powolne zapytania MySQL hello, można użyć narzędzia MySQL, takie jak **mysqldumpslow** tooidentify hello wąskie gardło.  

Domyślnie to nie jest włączona. Włączanie dziennika powolne zapytania hello może używać niektórych zasobów Procesora. Zaleca się włączenie to tymczasowo do rozwiązywania problemów wąskich gardeł wydajności. tooturn na dziennik powolne zapytań hello:

1. Zmodyfikuj hello my.cnf przez dodanie hello zakończenia toohello wiersze:

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. Uruchom ponownie serwer MySQL hello.

        service  mysql  restart

3. Sprawdź, czy ustawienie hello jest wpływają przy użyciu hello **Pokaż** polecenia.

![Powolna zapytania dziennika na][7]   

![Powolna zapytania dziennika wyników][8]

W tym przykładzie można zauważyć, że tej funkcji powolne zapytania hello został włączony. Następnie można użyć hello **mysqldumpslow** narzędzia toodetermine wąskich gardeł wydajności i optymalizacji wydajności, takie jak dodanie indeksów.

## <a name="appendices"></a>Dodatki
Witaj poniżej przedstawiono przykładowe wydajności testu dane utworzone w środowisku laboratoryjnym docelowych. Zapewniają ogólne na trend danych wydajności hello z różnych dostrajanie podejścia wydajności. wyniki Hello mogą różnić się w różnych wersjach środowiska lub produkt.

### <a name="AppendixA"></a>Dodatek A  
**Wydajność dysku (IOPS) z różnych poziomów macierzy RAID**

![Dysk IOPS z różnych poziomów macierzy RAID][9]

**Polecenia testu**  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> Obciążenie Hello tego testu używa 64 wątki w trakcie tooreach hello górny limit RAID.
>
>

### <a name="AppendixB"></a>Dodatek B  
**Porównanie wydajności (przepływność) MySQL z różnych poziomów macierzy RAID**   
(XFS w systemie plików)

![Porównanie wydajności MySQL z różnych poziomów macierzy RAID][10]  
![Porównanie wydajności MySQL z różnych poziomów macierzy RAID][11]

**Polecenia testu**

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

**Porównanie wydajności (OLTP) MySQL z różnych poziomów macierzy RAID**  
![Porównanie wydajności (OLTP) MySQL z różnych poziomów macierzy RAID][12]

**Polecenia testu**

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <a name="AppendixC"></a>Dodatek C   
**Dysk porównanie wydajności (IOPS) dla różnych rozmiarach**  
(XFS w systemie plików)

![][13]

**Polecenia testu**  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

rozmiary plików Hello używać do testowania tego 30 GB i 1 GB, odpowiednio, macierz RAID 0 (4 dyski) XFS systemu plików.

### <a name="AppendixD"></a>Dodatek D  
**Porównanie wydajności (przepływność) MySQL przed i po optymalizacji**  
(XFS File System)

![Porównanie wydajności (przepływność) MySQL przed i po optymalizacji][14]

**Polecenia testu**

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

**Ustawienie konfiguracji Hello w domyślnej i optymalizacji wygląda następująco:**

| Parametry | Domyślne | Optymalizacja |
| --- | --- | --- |
| **innodb_buffer_pool_size** |Brak |7 GB |
| **innodb_log_file_size** |5 MB |512 MB |
| **max_connections** |100 |5000 |
| **innodb_file_per_table** |0 |1 |
| **innodb_flush_log_at_trx_commit** |1 |2 |
| **innodb_log_buffer_size** |8 MB |128 MB |
| **query_cache_size** |16 MB |0 |

Aby uzyskać bardziej szczegółowe [parametry konfiguracji optymalizacji](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), można znaleźć toohello [instrukcje oficjalnego MySQL](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).  

  **Środowisko testowe**  

| Sprzęt | Szczegóły |
| --- | --- |
| Procesor CPU |AMD Opteron(tm) procesora 4171 HE / 4 rdzenie |
| Memory (Pamięć) |14 GB |
| Dysk |10 GB/dysku |
| System operacyjny |Ubuntu 14.04.1 LTS |

[1]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-01.png
[2]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-02.png
[3]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-03.png
[4]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-04.png
[5]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-05.png
[6]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-06.png
[7]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-07.png
[8]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-08.png
[9]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-09.png
[10]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-10.png
[11]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-11.png
[12]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-12.png
[13]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-13.png
[14]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-14.png

