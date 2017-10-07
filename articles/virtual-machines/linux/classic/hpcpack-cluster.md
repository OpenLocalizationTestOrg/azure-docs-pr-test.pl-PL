---
title: "aaaLinux obliczeń maszyny wirtualne w klastrze HPC Pack | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate i użyj HPC Pack klastra w systemie Azure Linux komputerowych o wysokiej wydajności (HPC) obciążeń"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 4d080fdd-5ffe-4f54-a78d-4c818f6eb3fb
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/12/2016
ms.author: danlep
ms.openlocfilehash: 9ed20d6cd69a6472a00666caf8965e9d022698a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a>Rozpoczynanie pracy z węzłami obliczeniowymi systemu Linux w klastrze pakietu HPC Pack na platformie Azure
Konfigurowanie [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) klastra na platformie Azure, zawierającą węzła głównego z systemem Windows Server i kilka obliczeniowe węzłów z systemem obsługiwanych dystrybucji systemu Linux. Poznaj opcje toomove danych między hello węzłów systemu Linux i Windows hello węzła głównego klastra hello. Dowiedz się, jak toosubmit HPC systemu Linux zadania toohello klastra.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Na wysokim poziomie hello Poniższy diagram przedstawia klastra HPC Pack hello tworzenie i Praca z.

![Klaster HPC Pack z węzłami systemu Linux][scenario]

Dla innych opcji toorun HPC systemu Linux obciążeń na platformie Azure, zobacz [zasobów technicznych partii i wysoką wydajność pracy](../../../batch/big-compute-resources.md).

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a>Wdrożenie klastra HPC Pack z węzłami obliczeniowymi systemu Linux
W tym artykule przedstawiono dwie opcje toodeploy klastra HPC Pack na platformie Azure z węzłami obliczeniowymi systemu Linux. Obie metody użyć obrazu z witryny Marketplace systemu Windows Server z węzłem głównym HPC Pack toocreate hello. 

* **Szablonu usługi Azure Resource Manager** -Użyj szablonu z portalu Azure Marketplace hello, lub w szablonie Szybki Start społeczność hello, tooautomate tworzenia klastra hello w modelu wdrażania usługi Resource Manager hello. Na przykład Witaj [klastra HPC Pack dla systemu Linux obciążeń](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) szablonu w hello Azure Marketplace tworzy pełną infrastruktura klastra HPC Pack dla systemu Linux HPC obciążeń.
* **Skrypt programu PowerShell** -Użyj hello [skrypt wdrożenia Microsoft HPC Pack IaaS](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**HpcIaaSCluster.ps1 nowy**) tooautomate wdrożenia całego klastra w hello klasycznego modelu wdrażania. Ten skrypt programu PowerShell usługi Azure używa obrazu maszyny Wirtualnej programu HPC Pack w hello Azure Marketplace do szybkiego wdrożenia i zapewnia rozbudowany zestaw toodeploy parametry konfiguracji węzły obliczeniowe systemu Linux.

Aby uzyskać więcej informacji dotyczących opcji wdrażania klastrów HPC Pack na platformie Azure, zobacz [opcje toocreate i zarządzać klastrem wysokiej wydajności (HPC) na platformie Azure z pakietem Microsoft HPC](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="prerequisites"></a>Wymagania wstępne
* **Subskrypcja platformy Azure** -subskrypcji można używać w obu hello usługi Azure globalnym, ani w chińskiej wersji platformy Azure. Jeśli nie masz konta, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/) w zaledwie kilka minut.
* **Limit przydziału rdzeni** — może być konieczne tooincrease hello przydziału rdzeni, zwłaszcza jeśli toodeploy kilka węzłów klastra z wielordzeniowych rozmiarów maszyn wirtualnych. tooincrease limit przydziału, otwórz żądanie pomocy technicznej online klienta bez dodatkowych opłat.
* **Dystrybucje systemu Linux** — obecnie HPC Pack obsługuje powitania po dystrybucje systemu Linux dla węzłów obliczeniowych. Użyj wersji Marketplace tych dystrybucji, jeśli jest on dostępny lub Podaj własny.
  
  * **Na podstawie centOS**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC
  * **Red Hat Enterprise Linux**: 6.7, 6.8, 7.2
  * **SUSE Linux Enterprise Server**: SLES 12 SLES 12 (Premium), SLES 12 z dodatkiem SP1, SLES 12 z dodatkiem SP1 (Premium), SLES 12 dla HPC, SLES 12 dla HPC (Premium)
  * **Ubuntu Server**: 14.04 LTS, 16.04 LTS
    
    > [!TIP]
    > toouse hello Azure RDMA sieć z jedną rozmiarów maszyn wirtualnych z funkcją RDMA hello, Określ obraz systemu SUSE Linux Enterprise Server 12 HPC lub na podstawie CentOS HPC z hello Azure Marketplace. Aby uzyskać więcej informacji, zobacz [wysokiej wydajności obliczeniowe rozmiarów maszyn wirtualnych](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
    > 
    > 

Dodatkowe wymagania wstępne toodeploy hello klastra za pomocą skryptu wdrażania HPC Pack IaaS hello:

* **Komputer kliencki** — należy skryptu wdrażania klienta z systemem Windows komputera toorun hello klastra.
* **Program Azure PowerShell** - [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) (wersja 0.8.10 lub nowszego) na komputerze klienckim.
* **Skrypt wdrożenia HPC Pack IaaS** — Pobierz i Rozpakuj hello najnowszą wersję hello skryptu z hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Można sprawdzić wersji hello skryptu hello uruchamiając `.\New-HPCIaaSCluster.ps1 –Version`. Ten artykuł jest oparty na wersji 4.4.1 lub nowszej hello skryptu.

### <a name="deployment-option-1-use-a-resource-manager-template"></a>Opcja wdrażania 1. Użyj szablonu usługi Resource Manager
1. Przejdź toohello [klastra HPC Pack dla systemu Linux obciążeń](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) szablonu w hello Azure Marketplace, a następnie kliknij przycisk **Wdróż**.
2. W portalu Azure hello, przejrzyj informacje hello, a następnie kliknij przycisk **Utwórz**.
   
    ![Tworzenie portalu][portal]
3. Na powitania **podstawy** bloku, wprowadź nazwę klastra hello, który także nazwy węzła głównego hello maszyny Wirtualnej. Możesz wybrać istniejącą grupę zasobów lub Utwórz grupę wdrożenia hello w lokalizacji, która jest dostępna tooyou. Witaj lokalizacji ma wpływ na dostępność hello niektórych rozmiarów maszyn wirtualnych i innymi usługami Azure (zobacz [produkty, które są dostępne w regionie](https://azure.microsoft.com/regions/services/)).
4. Na powitania **przejdź do węzła ustawienia** bloku, w przypadku pierwszego wdrożenia zazwyczaj można zaakceptować ustawienia domyślne hello. 
   
   > [!NOTE]
   > Witaj **adresu URL skryptu pokonfiguracyjnego** jest opcjonalne ustawienie toospecify publicznie dostępnych skrypt programu Windows PowerShell, które mają toorun na powitania węzła głównego maszyny Wirtualnej po jej uruchomieniu. 
   > 
   > 
5. Na powitania **obliczeniowe węzła ustawienia** bloku, wybierz wzorzec nazewnictwa dla węzłów hello, hello liczby i rozmiaru hello węzłów i hello toodeploy dystrybucji systemu Linux.
6. Na powitania **ustawienia infrastruktury** bloku, wprowadź nazwy sieci wirtualnej hello i usługi Active Directory domeny, domeny i poświadczenia administratora maszyny Wirtualnej i wzorzec nazewnictwa hello kont magazynu.
   
   > [!NOTE]
   > HPC Pack używa hello — użytkownicy klastra tooauthenticate domeny usługi Active Directory. 
   > 
   > 
7. Po uruchomieniu testów sprawdzania poprawności hello i przejrzyj hello warunki użytkowania, kliknij przycisk **zakupu**.

### <a name="deployment-option-2-use-hello-iaas-deployment-script"></a>Opcja wdrażania 2. Użyj skryptu wdrożenia IaaS hello
Poniżej przedstawiono dodatkowe wymagania wstępne toodeploy hello klastra za pomocą skryptu wdrażania HPC Pack IaaS hello:

* **Komputer kliencki** — należy skryptu wdrażania klienta z systemem Windows komputera toorun hello klastra.
* **Program Azure PowerShell** - [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) (wersja 0.8.10 lub nowszego) na komputerze klienckim.
* **Skrypt wdrożenia HPC Pack IaaS** — Pobierz i Rozpakuj hello najnowszą wersję hello skryptu z hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Można sprawdzić wersji hello skryptu hello uruchamiając `.\New-HPCIaaSCluster.ps1 –Version`. Ten artykuł jest oparty na wersji 4.4.1 lub nowszej hello skryptu.

**Plik konfiguracji XML**

Hello skrypt wdrożenia HPC Pack IaaS używa pliku konfiguracji XML jako klaster HPC hello toodescribe wejściowego. Witaj następujący przykładowy plik konfiguracyjny określa mały składające się z węzłem głównym HPC Pack i dwa węzły obliczeniowe A7 CentOS 7.0 Linux rozmiar klastra. 

Zmodyfikuj plik hello odpowiednio dla swojego środowiska i konfiguracji klastra, a następnie zapisz plik z nazwą, takich jak HPCDemoConfig.xml. Na przykład należy toosupply nazwę subskrypcji i nazwy konta magazynu unikatowy i nazwa usługi w chmurze. Ponadto można toochoose innej obsługiwane Linux obrazu dla węzłów obliczeniowych hello. Aby uzyskać więcej informacji o elementach hello w pliku konfiguracyjnym hello, zobacz hello Manual.rtf plik w folderze skryptów hello i [utworzyć klaster HPC z hello skrypt wdrożenia HPC Pack IaaS](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>centos7rdmavnetje</VNetName>
    <SubnetName>CentOS7RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS7RDMA-HN</VMName>
    <ServiceName>centos7rdma-je</ServiceName>
  <VMSize>ExtraLarge</VMSize>
  <EnableRESTAPI />
  <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS7RDMA-LN%1%</VMNamePattern>
    <ServiceName>centos7rdma-je</ServiceName>
    <VMSize>A7</VMSize>
    <NodeCount>2</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

**Witaj toorun skrypt wdrożenia HPC Pack IaaS**

1. Otwórz program Windows PowerShell na komputerze klienckim hello jako administrator.
2. Zmień folder toohello katalogu, w którym skrypt hello jest zainstalowany (E:\IaaSClusterScript w tym przykładzie).
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. Uruchom powitania po klastra HPC Pack hello toodeploy polecenia. W tym przykładzie przyjęto założenie, że ten plik konfiguracji hello znajduje się w E:\HPCDemoConfig.xml
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    a. Ponieważ hello **AdminPassword** nie jest określona w hello poprzedzających polecenia, są hello tooenter zostanie wyświetlony monit o hasło użytkownika *MyAdminName*.
   
    b. skrypt Hello następnie uruchamia plik konfiguracji hello toovalidate. Tooseveral minut w zależności od połączenia sieciowego hello może potrwać.
   
    ![Walidacja][validate]
   
    c. Po operacji sprawdzania poprawności przekazać, skrypt hello wymieniono toocreate zasobów klastra hello. Wprowadź *Y* toocontinue.
   
    ![Zasoby][resources]
   
    d. skrypt Hello uruchamia klastra HPC Pack hello toodeploy i zakończeniu konfiguracji hello bez dalszego wymagane ręczne wykonanie czynności. skrypt Hello może trwać kilka minut.
   
    ![Wdrażanie][deploy]
   
   > [!NOTE]
   > W tym przykładzie hello skrypt generuje plik dziennika automatycznie od hello **- LogFile** parametr nie jest określony. Dzienniki Hello nie są zapisywane w czasie rzeczywistym, ale są zbierane na końcu hello hello weryfikacji i hello wdrożenia. Po zatrzymaniu hello proces PowerShell uruchomionej skryptu hello niektórych dzienników zostaną utracone.
   > 
   > 

## <a name="connect-toohello-head-node"></a>Połącz toohello węzła głównego
Po wdrożeniu klastra HPC Pack hello na platformie Azure, [połączenia przez pulpit zdalny](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello węzła głównego maszynę Wirtualną przy użyciu hello podana podczas wdrażania klastra hello poświadczeń domeny (na przykład *hpc\\ clusteradmin*). Witaj klastra można zarządzać z węzła głównego hello.

Na powitania węzła głównego Uruchom Menedżera klastra HPC toocheck hello stan klastra HPC Pack hello. Można zarządzać i monitorować węzły obliczeniowe Linux hello taki sam sposób pracy z systemem Windows węzły obliczeniowe. Na przykład, zobacz hello Linux węzły na liście **zarządzanie zasobami** (te węzły zostały wdrożone za pomocą hello **LinuxNode** szablonu).

![Zarządzanie węzła][management]

Zobacz też węzłów Linux hello hello **Mapa cieplna** widoku.

![Mapa cieplna][heatmap]

## <a name="how-toomove-data-in-a-cluster-with-linux-nodes"></a>Jak dane toomove w klastrze z węzłami systemu Linux
Masz kilka opcji toomove danych między węzłami systemu Linux i Windows hello węzła głównego klastra hello. Poniżej przedstawiono trzy typowe metody opisane bardziej szczegółowo w hello następujące sekcje:

* **Plików na platformę Azure** -ujawnia zarządzanych danych toostore udziałów plików SMB plików w magazynie Azure. Węzłów z systemem Windows i Linux węzłów mogą zainstalować udziały plików platformy Azure jako dysku lub folderu na powitania czasu takie same, nawet jeśli są one wdrożone w różnych sieciach wirtualnych.
* **Udział SMB węzła głównego** — instaluje standardowe folder udostępniony systemu Windows hello węzła głównego w węzłach systemu Linux.
* **Serwer systemu plików NFS węzła HEAD** — zapewnia rozwiązanie do udostępniania plików w środowisku mieszanym Windows i Linux.

### <a name="azure-file-storage"></a>Magazyn plików Azure
Witaj [plików Azure](https://azure.microsoft.com/services/storage/files/) udziałami plików przy użyciu standardowego protokołu SMB 2.1 hello udostępnia usługi. Maszyny wirtualne platformy Azure i usługi w chmurze mogą udostępniać dane między składnikami aplikacji za pośrednictwem zainstalowanych udziałów i lokalnych aplikacji mają dostęp do danych plików w udziale za pośrednictwem hello interfejsu API magazynu plików. 

Aby uzyskać szczegółowy opis kroków toocreate plików Azure udziału i zainstalować go na powitania węzła głównego, zobacz [Rozpoczynanie pracy z magazynem plików Azure w systemie Windows](../../../storage/files/storage-how-to-use-files-windows.md). udział plików Azure hello toomount hello węzłach Linux, zobacz [jak toouse magazyn plików Azure z systemem Linux](../../../storage/files/storage-how-to-use-files-linux.md). Zobacz tooset utrwalanie połączenia [Persisting tooMicrosoft połączenia usługi pliki Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).

W hello poniższy przykład należy utworzyć udział plików Azure na koncie magazynu. Witaj toomount udział na powitania węzła głównego, otwórz wiersz polecenia i wprowadź hello następującego polecenia:

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

W tym przykładzie allvhdsje to nazwa konta magazynu, storageaccountkey jest klucz konta magazynu, a funkcja rdma jest nazwa udziału plików Azure hello. udział plików Azure Hello jest zainstalowany jako Z: hello węzła głównego.

udział plików Azure hello toomount w węzłach Linux, uruchom **clusrun** na powitania węzła głównego. **[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)**  jest przydatne toocarry narzędzie HPC Pack zadania administracyjne na wielu węzłach. (Zobacz też [Clusrun dla systemu Linux węzłów](#Clusrun-for-Linux-nodes) w tym artykule.)

Otwórz okno programu Windows PowerShell i wprowadź hello następującego polecenia:

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

pierwsze polecenie Hello tworzy folder o nazwie /rdma we wszystkich węzłach grupy LinuxNodes hello. drugie polecenie Hello instaluje allvhdsjw.file.core.windows.net/rdma udział plików Azure hello na powitania /rdma folder o dir i plików trybu too777 zestawu usługi bits. W hello drugiego polecenia allvhdsje jest nazwa konta magazynu i storageaccountkey jest klucz konta magazynu.

> [!NOTE]
> Witaj "\`" symbol w hello drugie polecenie jest symbolem ucieczki dla środowiska PowerShell. "\`,"oznacza, że hello"," (przecinek znak) jest częścią polecenia hello.
> 
> 

### <a name="head-node-share"></a>Udział węzła głównego
Można również zainstalować hello węzła głównego folderu udostępnionego na węzłach systemu Linux. Udział zapewnia hello najprostszy sposób tooshare plików, ale hello węzła głównego i na wszystkich węzłach Linux, musi być wdrażana w hello tej samej sieci wirtualnej. Poniżej przedstawiono kroki hello.

1. Utwórz folder na powitania węzła głównego i udostępniać je tooEveryone uprawnienia odczytu/zapisu. Na przykład udostępnić D:\OpenFOAM na powitania węzła głównego jako \\CentOS7RDMA HN\OpenFOAM. W tym miejscu CentOS7RDMA HN jest hostname hello hello węzła głównego.
   
    ![Uprawnienia do udziału plików][fileshareperms]
   
    ![Udostępnianie plików][filesharing]
2. Otwórz okno programu Windows PowerShell i uruchom hello następującego polecenia:
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

pierwsze polecenie Hello tworzy folder o nazwie /openfoam we wszystkich węzłach grupy LinuxNodes hello. drugie polecenie Hello instaluje hello udostępnionego folderu //CentOS7RDMA-HN/OpenFOAM na powitania folder o dir i plików trybu too777 zestawu usługi bits. Witaj nazwę użytkownika i hasło w poleceniu hello powinna być hello nazwę użytkownika i hasło użytkownika klastra na powitania węzła głównego. (Zobacz [Dodaj lub usuń użytkowników klastra](https://technet.microsoft.com/library/ff919330.aspx).)

> [!NOTE]
> Witaj "\`" symbol w hello drugie polecenie jest symbolem ucieczki dla środowiska PowerShell. "\`,"oznacza, że hello"," (przecinek znak) jest częścią polecenia hello.
> 
> 

### <a name="nfs-server"></a>Serwer systemu plików NFS
Witaj usługi systemu plików NFS pozwala tooshare oraz migrację plików na komputerach przy użyciu protokołu SMB hello systemem operacyjnym hello systemu Windows Server 2012 i opartych na systemie Linux przy użyciu protokołu NFS hello. Witaj serwer systemu plików NFS i inne węzły mają toobe wdrożone w hello tej samej sieci wirtualnej. Zapewnia lepszą zgodność z węzłami systemu Linux w porównaniu z udziału SMB. Na przykład obsługuje łącza do plików.

1. tooinstall i skonfigurować serwer NFS, wykonaj kroki hello w [serwera dla systemu pierwszego udziału sieciowego na całej trasie](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).
   
    Na przykład można utworzyć udziału NFS o nazwie systemu plików nfs, ze hello następujące właściwości:
   
    ![Autoryzacja systemu plików NFS][nfsauth]
   
    ![Uprawnienia udziału NFS][nfsshare]
   
    ![Uprawnienia NTFS systemu plików NFS][nfsperm]
   
    ![Właściwości zarządzania systemu plików NFS][nfsmanage]
2. Otwórz okno programu Windows PowerShell i uruchom hello następującego polecenia:
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   pierwsze polecenie Hello tworzy folder o nazwie /nfsshared we wszystkich węzłach grupy LinuxNodes hello. Witaj drugiego polecenia hello instalacji NFS udostępnianie CentOS7RDMA HN: / systemu plików nfs na hello folderu. W tym miejscu CentOS7RDMA HN: / systemu plików nfs jest hello zdalnego ścieżka udziału NFS.

## <a name="how-toosubmit-jobs"></a>Jak toosubmit zadania
Istnieje kilka sposobów toosubmit zadania toohello HPC Pack klastra:

* Menedżer klastrów HPC lub Menedżer zadań klastra HPC graficznego interfejsu użytkownika
* Portalu internetowego HPC
* Interfejs API REST

Przesyłanie zadań do klastra toohello na platformie Azure za pomocą narzędzia HPC Pack graficznego interfejsu użytkownika i portalu internetowego HPC hello są hello takie same jak w przypadku systemu Windows węzłów obliczeniowych. Zobacz [Menedżer zadań klastra HPC Pack](https://technet.microsoft.com/library/ff919691.aspx) i [jak toosubmit zadania z komputera klienckiego lokalnymi](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

zadania toosubmit za pośrednictwem interfejsu API REST, hello odwoływać się za[tworzenie i przesyłanie zadań za pomocą interfejsu API REST w Microsoft HPC Pack hello](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx). zadania toosubmit w kliencie systemu Linux można znaleźć próbki Python toohello w hello [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).

## <a name="clusrun-for-linux-nodes"></a>Clusrun dla węzłów systemu Linux
Witaj HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) narzędzie może być używane tooexecute poleceń w węzłach systemu Linux przy użyciu wiersza polecenia lub Menedżer klastra HPC. Poniżej przedstawiono niektóre podstawowe przykłady.

* Pokaż bieżącej nazwy użytkownika na wszystkich węzłach w klastrze hello.
  
    ```command
    clusrun whoami
    ```
* Zainstaluj hello **gdb** narzędzie debugera z **yum** we wszystkich węzłach hello linuxnodes grupy, a następnie ponownie uruchom węzłów powitania po 10 minutach.
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* Utwórz skrypt powłoki wyświetlania każdej liczby od 1 do 10 sekundy jeden w każdym węźle systemu Linux w klastrze hello, uruchom go i natychmiast wyświetlane dane wyjściowe z węzłów hello.
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> Może być konieczne toouse escape niektórych znaków w **clusrun** poleceń. Jak pokazano w tym przykładzie, użyj ^ w hello tooescape wiersza polecenia ">" symbolu.
> 
> 

## <a name="next-steps"></a>Następne kroki
* Spróbuj skalowaniu hello klastra tooa większą liczbę węzłów lub działających obciążeń systemu Linux na powitania klastra. Na przykład zobacz [Uruchom NAMD z pakietem Microsoft HPC w systemie Linux obliczeniowe węzłów na platformie Azure](hpcpack-cluster-namd.md).
* Spróbuj klaster z [maszyn wirtualnych z funkcją RDMA, obliczeniowych](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun MPI obciążeń. Na przykład zobacz [klastra uruchom OpenFOAM z pakietem Microsoft HPC na RDMA systemu Linux na platformie Azure](hpcpack-cluster-openfoam.md).
* Jeśli interesuje Cię w pracy z Linux węzłów w klastrze HPC Pack lokalnych, zobacz hello [wskazówki TechNet](https://technet.microsoft.com/library/mt595803.aspx).

<!--Image references-->
[scenario]:media/hpcpack-cluster/scenario.png
[portal]:media/hpcpack-cluster/portal.png
[validate]:media/hpcpack-cluster/validate.png
[resources]:media/hpcpack-cluster/resources.png
[deploy]:media/hpcpack-cluster/deploy.png
[management]:media/hpcpack-cluster/management.png
[heatmap]:media/hpcpack-cluster/heatmap.png
[fileshareperms]:media/hpcpack-cluster/fileshare1.png
[filesharing]:media/hpcpack-cluster/fileshare2.png
[nfsauth]:media/hpcpack-cluster/nfsauth.png
[nfsshare]:media/hpcpack-cluster/nfsshare.png
[nfsperm]:media/hpcpack-cluster/nfsperm.png
[nfsmanage]:media/hpcpack-cluster/nfsmanage.png
