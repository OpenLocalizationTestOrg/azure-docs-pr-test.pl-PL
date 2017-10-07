---
title: aaaSet zapasowe Linux RDMA klastra toorun MPI aplikacji | Dokumentacja firmy Microsoft
description: Tworzenie klastra rozmiar toouse H16r H16mr, A8 i A9 maszyn wirtualnych systemu Linux hello Azure RDMA sieci toorun MPI aplikacji
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 01834bad-c8e6-48a3-b066-7f1719047dd2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.openlocfilehash: 3199317a37b095e80718d6724954687d30aea3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-linux-rdma-cluster-toorun-mpi-applications"></a>Skonfiguruj aplikacje MPI toorun Linux RDMA klastra
Dowiedz się, jak klastra tooset się RDMA systemu Linux na platformie Azure z [wysokiej wydajności obliczeniowe rozmiarów maszyn wirtualnych](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun równoległych aplikacji komunikat interfejsu (Passing Interface). W tym artykule przedstawiono kroki tooprepare toorun obrazu HPC systemu Linux Intel MPI w klastrze. Po przygotowaniu można wdrożyć klaster maszyn wirtualnych przy użyciu tego obrazu i jeden rozmiary maszyny Wirtualnej platformy Azure z funkcją RDMA hello (obecnie H16r H16mr, A8 i A9). Użyj hello klastra toorun MPI aplikacji, które skutecznie komunikacji za pośrednictwem małe opóźnienia, wysokiej przepustowości sieci na podstawie zdalnego bezpośredniego dostępu do pamięci technologii (RDMA).

> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager](../../../resource-manager-deployment-model.md) i klasycznym. W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.

## <a name="cluster-deployment-options"></a>Opcje wdrażania klastra
Poniżej przedstawiono metod toocreate klastra Linux RDMA z lub bez harmonogramu zadań.

* **Skrypty interfejsu wiersza polecenia platformy Azure**: jak pokazano w dalszej części tego artykułu, należy użyć hello [interfejsu wiersza polecenia platformy Azure](../../../cli-install-nodejs.md) (CLI) tooscript hello wdrożenia klastra maszyn wirtualnych z funkcją RDMA. Hello interfejsu wiersza polecenia w trybie usługi zarządzania tworzy hello węzły klastra kolejno w hello klasycznego modelu wdrażania, tak wiele węzłów obliczeniowych wdrażanie może potrwać kilka minut. tooenable hello połączenia sieciowego RDMA, gdy używasz hello klasycznego modelu wdrażania, wdrażanie maszyn wirtualnych hello w hello sama usługa w chmurze.
* **Szablony usługi Azure Resource Manager**: umożliwia także hello Resource Manager deployment model toodeploy klastra maszyny wirtualne z funkcją RDMA, który łączy sieciowych RDMA toohello. Możesz [utworzyć własny szablon](../../../resource-group-authoring-templates.md), lub sprawdź hello [szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates/) zamieszczone przez Microsoft lub hello społeczności toodeploy hello rozwiązanie ma szablonów. Szablony Menedżera zasobów zapewniają toodeploy szybki i niezawodny sposób klaster systemu Linux. Witaj tooenable połączenia sieciowego RDMA, korzystając z modelu wdrażania usługi Resource Manager hello, wdrażanie maszyn wirtualnych hello w hello tego samego zestawu dostępności.
* **HPC Pack**: Tworzenie klastra Microsoft HPC Pack na platformie Azure i Dodaj węzły obliczeniowe z funkcją RDMA, systemem obsługiwanych Linux tooaccess hello RDMA sieci dystrybucji. Aby uzyskać więcej informacji, zobacz [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](hpcpack-cluster.md).

## <a name="sample-deployment-steps-in-hello-classic-model"></a>Przykładowe wdrożenie kroki w klasycznym modelu hello
Witaj poniższej procedurze pokazano, jak dostosować go toouse hello Azure CLI toodeploy maszyny Wirtualnej HPC z dodatkiem SP1 SUSE Linux Enterprise Server (SLES) 12 z hello Azure Marketplace i utworzyć niestandardowy obraz maszyny Wirtualnej. Następnie można użyć wdrożenia hello tooscript obrazu hello klastra maszyn wirtualnych z funkcją RDMA.

> [!TIP]
> Użyj podobne kroki toodeploy, klaster maszyn wirtualnych z funkcją RDMA oparta na podstawie CentOS HPC obrazów w hello Azure Marketplace. Niektóre kroki różnić się nieznacznie, jak podano. 
>
>

### <a name="prerequisites"></a>Wymagania wstępne
* **Komputer kliencki**: należy Mac, Linux lub Windows klienta komputera toocommunicate z platformy Azure. Tych krokach przyjęto założenie, że używasz klienta systemu Linux.
* **Subskrypcja platformy Azure**: Jeśli nie masz subskrypcji, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/free/) w zaledwie kilka minut. W przypadku dużych klastrów rozważ z subskrypcji lub inne opcje zakupu.
* **Dostępność rozmiar maszyny Wirtualnej**: hello po wystąpieniu rozmiary są funkcją RDMA: H16r, H16mr A8 i A9. Sprawdź [produkty, które są dostępne w regionie](https://azure.microsoft.com/regions/services/) dostępności w regionach platformy Azure.
* **Limit przydziału rdzeni**: może być konieczne tooincrease hello przydziału rdzeni toodeploy klastrów obliczeniowych maszyn wirtualnych. Na przykład należy co najmniej 128 rdzeni Chcąc VMs A9 toodeploy 8, jak pokazano w tym artykule. Subskrypcji może również ograniczać hello liczba rdzeni, którą można wdrożyć w niektórych rodzin rozmiar maszyny Wirtualnej, włączając hello H-series. Zwiększ limit przydziału toorequest [otwarcia żądania pomocy technicznej online klienta](../../../azure-supportability/how-to-create-azure-support-request.md) bez dodatkowych opłat.
* **Azure CLI**: [zainstalować](../../../cli-install-nodejs.md) hello wiersza polecenia platformy Azure i [połączyć tooyour subskrypcji platformy Azure](../../../xplat-cli-connect.md) z komputera klienckiego hello.

### <a name="provision-an-sles-12-sp1-hpc-vm"></a>Zapewnij SLES 12 SP1 HPC maszyny Wirtualnej
Po zalogowaniu się tooAzure z hello wiersza polecenia platformy Azure, uruchom `azure config list` tooconfirm, który hello danych wyjściowych zawiera trybie zarządzania usługami. Jeśli nie, należy ustawić tryb hello, uruchamiając poniższe polecenie:

    azure config mode asm


Wpisz następujące toolist hello wszystkie subskrypcje hello są autoryzowane toouse:

    azure account list

bieżącej subskrypcji active Hello jest oznaczone symbolem `Current` ustawić także`true`. Jeśli ta subskrypcja nie jest hello jeden klaster hello toocreate toouse, Ustaw identyfikator subskrypcji odpowiednie hello jako aktywną subskrypcją hello:

    azure account set <subscription-Id>

toosee hello publicznie dostępnych obrazów SLES 12 SP1 HPC na platformie Azure, uruchom polecenie, takie jak powitania po, zakładając, że obsługuje środowisko z powłoki **grep**:

    azure vm image list | grep "suse.*hpc"

Zapewnij z funkcją RDMA maszyny Wirtualnej z obrazu systemu SLES 12 SP1 HPC, uruchamiając polecenie, takie jak następujące hello:

    azure vm create -g <username> -p <password> -c <cloud-service-name> -l <location> -z A9 -n <vm-name> -e 22 b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824

Gdzie:

* Witaj rozmiaru (A9 w tym przykładzie) jest jednym z funkcją RDMA hello rozmiarów maszyn wirtualnych.
* numer Hello do portu zewnętrznego SSH (22 w tym przykładzie jest hello domyślne SSH) jest dowolny prawidłowy numer portu. numer portu SSH wewnętrzny Hello ustawiono too22.
* Nową usługę w chmurze jest tworzony w hello określony na podstawie lokalizacji hello region platformy Azure. Określ lokalizację, w których hello maszyny Wirtualnej jest dostępna rozmiaru.
* Obsługa SUSE priorytet (która wiąże się z dodatkowych opłat) Nazwa obrazu hello SLES 12 SP1 aktualnie może być jedną z tych dwóch opcji: 

 `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824`

  `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-priority-v20160824`


### <a name="customize-hello-vm"></a>Dostosowywanie hello maszyny Wirtualnej
Po zakończeniu inicjowania obsługi administracyjnej hello wirtualna toohello SSH maszyny Wirtualnej za pomocą hello zewnętrzny adres IP maszyny Wirtualnej (lub nazwa DNS) i hello numer portu zewnętrznego skonfigurowany, a następnie dostosować go. Aby uzyskać informacje dotyczące połączenia, zobacz [jak toolog na tooa maszyny wirtualnej z systemem Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Przeprowadź polecenia hello użytkownika, którego skonfigurowane na powitania maszyny Wirtualnej, chyba że wymagane toocomplete krokiem jest dostęp do konta root.

> [!IMPORTANT]
> Microsoft Azure nie zapewnia dostęp do konta root tooLinux maszyn wirtualnych. dostęp administracyjny toogain podczas połączenia jako toohello użytkownika maszyny Wirtualnej, Uruchom polecenia przy użyciu `sudo`.
>
>

* **Aktualizacje**: Zainstaluj aktualizacje za pomocą zypper. Można także tooinstall narzędzia systemu plików NFS.

  > [!IMPORTANT]
  > SLES 12 SP1 HPC maszynie wirtualnej firma Microsoft zaleca, nie zostaną zastosowane aktualizacje jądra, które mogą powodować problemy hello Linux RDMA sterowniki.
  >
  >
* **Intel MPI**: ukończy instalację hello Intel MPI na powitania wirtualna HPC systemu SLES 12 z dodatkiem SP1, uruchamiając następujące polecenie hello:

        sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
* **Zablokować pamięci**: MPI kody toolock hello pamięci dostępnej dla funkcji RDMA, dodać lub zmienić hello następujące ustawienia w pliku /etc/security/limits.conf hello. Należy głównego tooedit dostępu do tego pliku.

    ```
    <User or group name> hard    memlock <memory required for your application in KB>

    <User or group name> soft    memlock <memory required for your application in KB>
    ```

  > [!NOTE]
  > Do celów testowych można również ustawić memlock toounlimited. Na przykład: `<User or group name>    hard    memlock unlimited`. Aby uzyskać więcej informacji, zobacz [znaną metody ustawienie zablokowane rozmiar pamięci](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).
  >
  >
* **Klucze SSH dla maszyn wirtualnych SLES**: generowanie SSH klucze tooestablish zaufania dla tego konta użytkownika między hello obliczeniowe węzłów w klastrze SLES hello podczas uruchamiania zadań MPI. Jeśli wdrożono maszynę Wirtualną na podstawie CentOS HPC, nie należy wykonać ten krok. Zobacz instrukcje w dalszej części tego artykułu tooset passwordless SSH relacji zaufania między węzłami klastra powitania po przechwyceniu hello obrazu i wdrożenie klastra hello.

    kluczy SSH toocreate, uruchom następujące polecenie hello. Po wyświetleniu monitu o wprowadzenie danych, wybierz **Enter** toogenerate hello kluczy w lokalizacji domyślnej hello bez ustawienia hasła.

        ssh-keygen

    Dołącz plik authorized_keys toohello klucza publicznego hello znane kluczy publicznych.

        cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

    W katalogu ~/.ssh hello Edytuj lub Utwórz hello pliku konfiguracji. Podaj zakres adresów IP hello hello sieci prywatnej czy planujesz toouse na platformie Azure (10.32.0.0/16 w tym przykładzie):

        host 10.32.0.*
        StrictHostKeyChecking no

    Alternatywnie listy adres IP sieci prywatnej hello każdej maszyny Wirtualnej w klastrze w następujący sposób:

    ```
    host 10.32.0.1
     StrictHostKeyChecking no
    host 10.32.0.2
     StrictHostKeyChecking no
    host 10.32.0.3
     StrictHostKeyChecking no
    ```

  > [!NOTE]
  > Konfigurowanie `StrictHostKeyChecking no` można utworzyć potencjalne zagrożenie dla bezpieczeństwa, jeśli nie określono określonego adresu IP lub zakresu.
  >
  >
* **Aplikacje**: Zainstaluj wszystkie aplikacje muszą lub wykonywać inne dostosowania, przed przechwyceniem obrazu hello.

### <a name="capture-hello-image"></a>Przechwyć obraz powitania
Obraz powitania toocapture, najpierw uruchom następujące polecenie na powitania maszyny Wirtualnej systemu Linux hello. To polecenie deprovisions hello maszyny Wirtualnej, ale przechowuje konta użytkowników i kluczy SSH, które zostały zdefiniowane.

```
sudo waagent -deprovision
```

Z komputera klienta Uruchom powitania po obraz powitania toocapture polecenia wiersza polecenia platformy Azure. Aby uzyskać więcej informacji, zobacz [jak toocapture klasyczne maszyny wirtualnej systemu Linux jako obrazu](capture-image.md).  

```
azure vm shutdown <vm-name>

azure vm capture -t <vm-name> <image-name>

```

Po uruchomieniu tych poleceń hello obrazu maszyny Wirtualnej są przechwytywane do użycia i hello maszyna wirtualna zostanie usunięta. Teraz masz z niestandardowego obrazu toodeploy gotowy klaster.

### <a name="deploy-a-cluster-with-hello-image"></a>Wdrażanie klastra z obrazem hello
Modyfikowanie hello następującego skryptu Bash z odpowiednimi wartościami dla środowiska i uruchom go z komputera klienckiego. Ponieważ Azure wdraża hello maszyn wirtualnych, pojedynczo w hello klasycznego modelu wdrażania, zajmuje kilka minut toodeploy hello osiem A9 maszyn wirtualnych sugerowane w tym skrypcie.

```
#!/bin/bash -x
# Script toocreate a compute cluster without a scheduler in a VNet in Azure
# Create a custom private network in Azure
# Replace 10.32.0.0 with your virtual network address space
# Replace <network-name> with your network identifier
# Replace "West US" with an Azure region where hello VM size is available
# See Azure Pricing pages for prices and availability of compute-intensive VMs

azure network vnet create -l "West US" -e 10.32.0.0 -i 16 <network-name>

# Create a cloud service. All hello compute-intensive instances need toobe in hello same cloud service for Linux RDMA toowork across InfiniBand.
# Note: hello current maximum number of VMs in a cloud service is 50. If you need tooprovision more than 50 VMs in hello same cloud service in your cluster, contact Azure Support.

azure service create <cloud-service-name> --location "West US" –s <subscription-ID>

# Define a prefix naming scheme for compute nodes, e.g., cluster11, cluster12, etc.

vmname=cluster

# Define a prefix for external port numbers. If you want tooturn off external ports and use only internal ports toocommunicate between compute nodes via port 22, don’t use this option. Since port numbers up too10000 are reserved, use numbers after 10000. Leave external port on for rank 0 and head node.

portnumber=101

# In this cluster there will be 8 size A9 nodes, named cluster11 toocluster18. Specify your captured image in <image-name>. Specify hello username and password you used when creating hello SSH keys.

for (( i=11; i<19; i++ )); do
        azure vm create -g <username> -p <password> -c <cloud-service-name> -z A9 -n $vmname$i -e $portnumber$i -w <network-name> -b Subnet-1 <image-name>
done

# Save this script with a name like makecluster.sh and run it in your shell environment tooprovision your cluster
```

## <a name="considerations-for-a-centos-hpc-cluster"></a>Zagadnienia dotyczące klastra CentOS HPC
Tooset zapasowej klastra na podstawie jednej z obrazów na podstawie CentOS HPC hello w hello Azure Marketplace zamiast SLES 12 dla HPC, należy wykonać czynności ogólne hello w powyższej sekcji hello. Należy zwrócić uwagę hello następujące różnice, podczas udostępniania i konfigurowania hello maszyny Wirtualnej:

- Intel MPI jest już zainstalowana na maszynie Wirtualnej z obrazu na podstawie CentOS HPC.
- Ustawienia pamięci blokady są już dodana w pliku /etc/security/limits.conf hello maszyny Wirtualnej.
- Generuje klucze SSH na powitania udostępnieniem maszyny Wirtualnej do przechwycenia. Zamiast tego zaleca się skonfigurowanie uwierzytelniania użytkownika po wdrożeniu klastra hello. Aby uzyskać więcej informacji zobacz hello następujących sekcji.  

### <a name="set-up-passwordless-ssh-trust-on-hello-cluster"></a>Konfigurowanie passwordless zaufania SSH w klastrze hello
W klastrze HPC na podstawie CentOS, istnieją dwie metody do ustanawiania relacji zaufania między węzłami obliczeniowymi hello: uwierzytelnianie oparte na hoście i uwierzytelnianie oparte na użytkowniku. Uwierzytelnianie oparte na hoście wykracza poza zakres tego artykułu hello i zazwyczaj muszą być wykonywane przez rozszerzenia skryptów podczas wdrażania. Uwierzytelnianie użytkownika jest wygodną metodą ustanawiania relacji zaufania po wdrożeniu i wymaga generowania hello i udostępniania kluczy SSH między hello obliczeniowe węzłów w klastrze hello. Ta metoda jest często nazywana passwordless logowania SSH i jest wymagany w przypadku uruchamiania zadań MPI.

Przykładowy skrypt przyczyniły się od społeczności hello jest dostępna w [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) tooenable łatwe użytkownika uwierzytelniania w klastrze HPC na podstawie CentOS. Pobranie i użycie tego skryptu za pomocą hello następujące kroki. Można również zmodyfikować tego skryptu lub użyć inne metody tooestablish passwordless SSH uwierzytelniania między węzły obliczeń hello klastra.

    wget https://raw.githubusercontent.com/tanewill/utils/master/ user_authentication.sh

skrypt hello toorun, należy tooknow hello prefiks dla podsieci adresów IP. Pobierz hello prefiksu, uruchamiając następujące polecenie w jednym z węzłów klastra hello hello. Dane wyjściowe powinny wyglądać podobnie 10.1.3.5 i prefiks hello jest hello 10.1.3 części.

    ifconfig eth0 | grep -w inet | awk '{print $2}'

Teraz uruchom skrypt hello przy użyciu trzech parametrów: Nazwa pospolita użytkownika hello na powitania węzły obliczeniowe, hello wspólne hasło dla tego użytkownika na powitania węzły obliczeniowe i prefiksu podsieci hello, który został zwrócony z hello poprzednie polecenie.

    ./user_authentication.sh <myusername> <mypassword> 10.1.3

Ten skrypt hello następujące:

* Tworzy katalog na powitania węzła hosta o nazwie .ssh, co jest niezbędne do logowania passwordless.
* Tworzy plik konfiguracji w katalogu .ssh hello, która sprawia, że logowanie tooallow passwordless logowania z dowolnego węzła w klastrze hello.
* Tworzy pliki zawierające hello nazwy węzła i węzła adresów IP dla wszystkich węzłów hello hello klastra. Te pliki są pozostawiane po uruchomieniu skryptu hello do wykorzystania w późniejszym czasie.
* Tworzy prywatne i publiczne pary kluczy dla każdego węzła klastra (w tym hello węzła hosta) oraz wpisy w pliku authorized_keys hello.

> [!WARNING]
> Uruchomienie tego skryptu można utworzyć potencjalne zagrożenie dla bezpieczeństwa. Upewnij się, że hello informacje o kluczu publicznym w ~/.ssh nie będzie on rozpowszechniany.
>
>

## <a name="configure-intel-mpi"></a>Skonfiguruj Intel MPI
aplikacje MPI toorun na RDMA systemu Linux platformy Azure, należy tooconfigure niektórych tooIntel określonych zmiennych MPI środowiska. Oto przykładowe Bash skryptu tooconfigure hello zmienne potrzebne toorun aplikacji. Zmień hello toompivars.sh ścieżki instalacji programu Intel MPI.

```
#!/bin/bash -x

# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh

export I_MPI_FABRICS=shm:dapl

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB
# Setting hello variable tooshm:dapl gives best performance for some applications
# If your application doesn’t take advantage of shared memory and MPI together, then set only dapl

export I_MPI_DAPL_PROVIDER=ofa-v2-ib0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

export I_MPI_DYNAMIC_CONNECTION=0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

# Command line toorun hello job

mpirun -n <number-of-cores> -ppn <core-per-node> -hostfile <hostfilename>  /path <path toohello application exe> <arguments specific toohello application>

#end
```

Witaj format pliku hosta hello ma następującą składnię. Dodaj jeden wiersz dla każdego węzła w klastrze. Określ prywatnych adresów IP z sieci wirtualnej hello nie zostały zdefiniowane wcześniej, a nie nazw DNS. Na przykład dla dwa hosty z adresami IP 10.32.0.1 i 10.32.0.2 hello plik zawiera następujące hello:

```
10.32.0.1:16
10.32.0.2:16
```

## <a name="run-mpi-on-a-basic-two-node-cluster"></a>Uruchom MPI na podstawowe dwa węzły klastra
Jeśli jeszcze tego nie zrobiono, najpierw skonfigurować środowisko hello do Intel MPI.

```
# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh
```

### <a name="run-an-mpi-command"></a>Uruchom polecenie MPI
Uruchom polecenie MPI na jednym z hello tooshow węzły obliczeniowe, MPI jest poprawnie zainstalowany i może komunikować się między co najmniej dwóch węzłów obliczeniowych. następujące Hello **mpirun** polecenia uruchamiane hello **hostname** na dwa węzły.

```
mpirun -ppn 1 -n 2 -hosts <host1>,<host2> -env I_MPI_FABRICS=shm:dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 hostname
```
Dane wyjściowe powinny zawierać nazw hello wszystkich węzłów hello, które przekazany jako dane wejściowe dla `-hosts`. Na przykład **mpirun** polecenie z dwoma węzłami zwraca dane wyjściowe podobne do następujących hello:

```
cluster11
cluster12
```

### <a name="run-an-mpi-benchmark"></a>Uruchamianie testów porównawczych MPI
następujące polecenie Intel MPI Hello uruchamia pingpong testu porównawczego tooverify hello konfiguracji i połączeń toohello RDMA sieć klastra.

```
mpirun -hosts <host1>,<host2> -ppn 1 -n 2 -env I_MPI_FABRICS=dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 IMB-MPI1 pingpong
```

Powinny zostać wyświetlone dane wyjściowe podobne do następujących hello w klastrze pracy z dwoma węzłami. W sieci Azure RDMA hello oczekiwany czas oczekiwania na poziomie lub poniżej 3 mikrosekundach dla rozmiary wiadomości w górę too512 bajtów.

```
#------------------------------------------------------------
#    Intel (R) MPI Benchmarks 4.0 Update 1, MPI-1 part
#------------------------------------------------------------
# Date                  : Fri Jul 17 23:16:46 2015
# Machine               : x86_64
# System                : Linux
# Release               : 3.12.39-44-default
# Version               : #5 SMP Thu Jun 25 22:45:24 UTC 2015
# MPI Version           : 3.0
# MPI Thread Environment:
# New default behavior from Version 3.2 on:
# hello number of iterations per message size is cut down
# dynamically when a certain run time (per message size sample)
# is expected toobe exceeded. Time limit is defined by variable
# "SECS_PER_SAMPLE" (=> IMB_settings.h)
# or through hello flag => -time

# Calling sequence was:
# /opt/intel/impi_latest/bin64/IMB-MPI1 pingpong
# Minimum message length in bytes:   0
# Maximum message length in bytes:   4194304
#
# MPI_Datatype                   :   MPI_BYTE
# MPI_Datatype for reductions    :   MPI_FLOAT
# MPI_Op                         :   MPI_SUM
#
#
# List of Benchmarks toorun:
# PingPong
#---------------------------------------------------
# Benchmarking PingPong
# #processes = 2
#---------------------------------------------------
       #bytes #repetitions      t[usec]   Mbytes/sec
            0         1000         2.23         0.00
            1         1000         2.26         0.42
            2         1000         2.26         0.85
            4         1000         2.26         1.69
            8         1000         2.26         3.38
           16         1000         2.36         6.45
           32         1000         2.57        11.89
           64         1000         2.36        25.81
          128         1000         2.64        46.19
          256         1000         2.73        89.30
          512         1000         3.09       157.99
         1024         1000         3.60       271.53
         2048         1000         4.46       437.57
         4096         1000         6.11       639.23
         8192         1000         7.49      1043.47
        16384         1000         9.76      1600.76
        32768         1000        14.98      2085.77
        65536          640        25.99      2405.08
       131072          320        50.68      2466.64
       262144          160        80.62      3101.01
       524288           80       145.86      3427.91
      1048576           40       279.06      3583.42
      2097152           20       543.37      3680.71
      4194304           10      1082.94      3693.63

# All processes entering MPI_Finalize

```



## <a name="next-steps"></a>Następne kroki
* Wdrażanie i uruchamianie sieci MPI Linux aplikacji w klastrze systemu Linux.
* Zobacz hello [dokumentację biblioteki MPI Intel](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) wskazówki dotyczące Intel MPI.
* Spróbuj [szablon szybkiego startu](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate połysk Intel klastra przy użyciu obrazu na podstawie CentOS HPC. Aby uzyskać więcej informacji, zobacz [wdrażanie Intel chmury Edition dla połysk w systemie Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).
