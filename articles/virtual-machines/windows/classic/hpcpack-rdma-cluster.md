---
title: aaaSet zapasowe Windows RDMA klastra toorun MPI aplikacji | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate klastra systemu Windows HPC Pack z toouse H16r H16mr, A8 i A9 maszyn wirtualnych rozmiar hello Azure RDMA sieci toorun MPI aplikacji."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 7d9f5bc8-012f-48dd-b290-db81c7592215
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 23bc8740dbd05a7c7ab3f998489a41d0df4520a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-rdma-cluster-with-hpc-pack-toorun-mpi-applications"></a>Konfigurowanie klastra Windows RDMA HPC Pack toorun MPI aplikacji
Konfigurowanie klastra RDMA systemu Windows na platformie Azure z [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) i [wysokiej wydajności obliczeniowe rozmiarów maszyn wirtualnych](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun równoległych aplikacji komunikat interfejsu (Passing Interface). Po skonfigurowaniu z funkcją RDMA, opartych na systemie Windows Server węzłów w klastrze HPC Pack aplikacji MPI wydajnie komunikacji za pośrednictwem nieznaczne opóźnienia, uzyskać wysoką przepustowość sieci na platformie Azure, oparty na technologii dostępu do (pamięci RDMA) zdalnego pamięci.

Jeśli chcesz toorun MPI obciążeń na maszynach wirtualnych systemu Linux Azure RDMA hello dostępu do sieci, zobacz [skonfigurowanie Linux RDMA klastra toorun MPI aplikacji](../../linux/classic/rdma-cluster.md).

## <a name="hpc-pack-cluster-deployment-options"></a>Opcje wdrażania klastra HPC Pack
Microsoft HPC Pack to narzędzie w toocreate nie dodatkowych kosztów HPC klastrów lokalnej lub w Azure toorun systemu Windows lub Linux HPC aplikacji. HPC Pack zawiera środowisko uruchomieniowe dla implementacji Microsoft hello hello komunikat przekazywanie interfejsu dla systemu Windows (MS-MPI). W przypadku użycia z funkcją RDMA wystąpień uruchomiony obsługiwany system operacyjny Windows Server, HPC Pack wydajne opcja toorun MPI systemu Windows daje aplikacjom możliwość dostępu do sieci Azure RDMA hello. 

W tym artykule przedstawiono dwa scenariusze i łączy tooset wskazówki toodetailed zapasowej klastra RDMA systemu Windows z pakietem Microsoft HPC. 

* Scenariusz 1. Wdrażanie wystąpień roli procesu roboczego obliczeniowych (PaaS)
* Scenariusz 2. Wdrażanie węzłów obliczeniowych w obliczeniowych maszyn wirtualnych (IaaS)

Ogólne wymagania wstępne toouse obliczeniowych wystąpień z systemem Windows, temacie [wysokiej wydajności obliczeniowe rozmiarów maszyn wirtualnych](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="scenario-1-deploy-compute-intensive-worker-role-instances-paas"></a>Scenariusz 1: Wdrażanie wystąpień roli procesu roboczego obliczeniowych (PaaS)
Z istniejącego klastra HPC Pack należy dodać zasoby obliczeniowe dodatkowe w wystąpień roli procesu roboczego platformy Azure (Azure węzłów) w chmurze usługa (PaaS). Ta funkcja, nazywane również "tooAzure serii" z HPC Pack obsługuje zakres rozmiarów dla wystąpień roli procesu roboczego hello. Podczas dodawania hello węzły platformy Azure, należy określić jeden z rozmiary hello z funkcją RDMA.

Poniżej przedstawiono zagadnienia i czynności tooburst obsługą tooRDMA wystąpieniach platformy Azure z istniejącego (zwykle w siedzibie firmy) klastra. Za pomocą podobne procedury tooadd procesu roboczego roli wystąpień tooan HPC Pack głównego węzła wdrożonej w maszynie Wirtualnej platformy Azure.

> [!NOTE]
> Aby tooAzure tooburst samouczka pakietem HPC, zobacz [Konfigurowanie klastra hybrydowego pakietem HPC](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md). Należy zwrócić uwagę zagadnienia hello w hello następujące kroki, które są stosowane w szczególności obsługą tooRDMA węzły platformy Azure.
> 
> 

![TooAzure serii][burst]

### <a name="steps"></a>Kroki
1. **Wdrażanie i konfigurowanie węzłem głównym HPC Pack 2012 R2**
   
    Pobierz najnowszy pakiet instalacyjny HPC Pack hello z hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49922). Aby tooprepare wymagania i instrukcje dotyczące wdrażania serii Azure, zobacz [serii tooAzure wystąpień procesów roboczych z pakietem Microsoft HPC](https://technet.microsoft.com/library/gg481749.aspx).
2. **Konfigurowanie certyfikatu zarządzania w hello subskrypcji platformy Azure**
   
    Skonfiguruj połączenie hello toosecure certyfikatu, między węzłem głównym hello i platformą Azure. Opcje i procedury, zobacz [scenariusze tooConfigure hello certyfikat zarządzania platformy Azure dla HPC Pack](http://technet.microsoft.com/library/gg481759.aspx). W przypadku wdrożeń testowych HPC Pack instaluje domyślne Microsoft HPC certyfikat zarządzania platformy Azure możesz szybko przekazać tooyour subskrypcji platformy Azure.
3. **Utwórz nową usługę w chmurze i konto magazynu**
   
    Użyj hello Azure toocreate portalu usługi w chmurze i konto magazynu dla wdrożenia hello w regionie, w której są dostępne wystąpienia hello z funkcją RDMA.
4. **Tworzenie szablonu Azure węzła**
   
    Użyj Kreatora szablonu węzła tworzenia hello w Menedżerze klastra HPC. Aby uzyskać instrukcje, zobacz [utworzyć szablon Azure węzła](http://technet.microsoft.com/library/gg481758.aspx#BKMK_Templ) w "Kroki tooDeploy węzłów Azure za pomocą programu Microsoft HPC Pack".
   
    Dla testów wstępnych zaleca się Konfigurowanie zasad ręczne dostępności w szablonie hello.
5. **Dodaj węzły klastra toohello**
   
    Użyj Kreatora dodawania węzła hello w Menedżerze klastra HPC. Aby uzyskać więcej informacji, zobacz [toohello Dodawanie węzłów Azure klastra HPC systemu Windows](http://technet.microsoft.com/library/gg481758.aspx#BKMK_Add).
   
    Podczas określania rozmiaru hello hello węzłów, wybierz jedną z hello z funkcją RDMA rozmiary wystąpienia.
   
   > [!NOTE]
   > W każdym wdrożeniu tooAzure serii wystąpieniami obliczeniowych hello HPC Pack automatycznie wdraża co najmniej dwa wystąpienia z funkcją RDMA (na przykład A8) jako węzły serwera proxy, oprócz wystąpień roli procesu roboczego platformy Azure toohello określisz. węzły serwera proxy Hello używają rdzeni, które są przydzielane toohello subskrypcji i spowodować naliczenie opłat wraz z wystąpień roli procesu roboczego platformy Azure hello.
   > 
   > 
6. **Start (zainicjować obsługi administracyjnej) węzły hello i objęte zadania online toorun**
   
    Wybierz węzeł hello i użyj hello **Start** akcji w Menedżerze klastra HPC. Po ukończeniu inicjowania obsługi administracyjnej zaznacz węzły hello i używać hello **przejdź do trybu Online** akcji w Menedżerze klastra HPC. Witaj węzły są gotowe toorun zadania.
7. **Przesyłanie zadań toohello klastra**
   
   Użyj HPC Pack zadania przesyłania narzędzia toorun klastra zadania. Zobacz [Microsoft HPC Pack: Zarządzanie zadaniami](http://technet.microsoft.com/library/jj899585.aspx).
8. **Zatrzymaj węzłów hello (deprovision)**
   
   Po zakończeniu uruchomionych zadań węzłów hello Przełącz do trybu offline i użyć hello **zatrzymać** akcji w Menedżerze klastra HPC.

## <a name="scenario-2-deploy-compute-nodes-in-compute-intensive-vms-iaas"></a>Scenariusz 2: Wdrażanie obliczeniowe węzłów obliczeniowych maszyn wirtualnych (IaaS)
W tym scenariuszu wdrażania węzłem głównym HPC Pack hello i węzły obliczeniowe klastra na maszynach wirtualnych w sieci wirtualnej platformy Azure. HPC Pack udostępnia wiele [opcje wdrażania na maszynach wirtualnych Azure](../../linux/hpcpack-cluster-options.md), włącznie z automatycznego wdrażania skryptów i szablonów Szybki Start Azure. Przykład Witaj następujące zagadnienia i kroków przewodnik toouse hello [skrypt wdrożenia HPC Pack IaaS](hpcpack-cluster-powershell-script.md) do automatyzowania wdrażania hello klastra HPC Pack 2012 R2 na platformie Azure.

![Klaster maszyny wirtualne platformy Azure][iaas]

### <a name="steps"></a>Kroki
1. **Tworzenie węzła głównego klastra i obliczeniowe węzła maszyn wirtualnych, uruchamiając skrypt wdrożenia HPC Pack IaaS hello na komputerze klienckim**
   
    Pobierz skrypt wdrożenia IaaS pakietu HPC hello z hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49922).
   
    komputer kliencki hello tooprepare, Utwórz hello Konfiguracja pliku i wykonywania hello skryptu, zobacz [utworzyć klaster HPC z hello skrypt wdrożenia HPC Pack IaaS](hpcpack-cluster-powershell-script.md). 
   
    węzły obliczeniowe toodeploy z funkcją RDMA, hello Uwaga następujące dodatkowe zagadnienia:
   
   * **Sieć wirtualna**: Określ nową sieć wirtualną w regionie, w którym hello z funkcją RDMA rozmiar wystąpienia mają toouse jest dostępna.
   * **System operacyjny Windows Server**: toosupport RDMA połączenie, określ system operacyjny Windows Server 2012 R2 lub Windows Server 2012 dla węzła obliczeń hello maszyn wirtualnych.
   * **Usługi w chmurze**: zalecamy wdrożenie z węzła głównego w usłudze w chmurze jednego i węzłów obliczeniowych w innej usługi chmury.
   * **HEAD rozmiaru węzła**: W tym scenariuszu należy wziąć pod uwagę o rozmiarze co najmniej A4 (bardzo duży) dla węzła głównego hello.
   * **Rozszerzenie HpcVmDrivers**: hello skrypt wdrożenia instaluje hello Agent maszyny Wirtualnej i hello rozszerzenia HpcVmDrivers automatycznie podczas wdrażania rozmiar A8 i A9 węzły obliczeniowe z systemem operacyjnym Windows Server. HpcVmDrivers instaluje sterowniki w węźle obliczeń hello maszyn wirtualnych, aby umożliwić im połączenie sieciowe RDMA toohello. Na maszynach wirtualnych z funkcją RDMA H-series należy zainstalować ręcznie hello HpcVmDrivers rozszerzenia. Zobacz [wysokiej wydajności obliczeniowe rozmiarów maszyn wirtualnych](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
   * **Konfiguracja sieci klastra**: skrypt wdrożenia hello automatycznie konfiguruje klastra HPC Pack hello w topologii 5 (we wszystkich węzłach w sieci przedsiębiorstwa hello). Ta topologia jest wymagany dla wszystkich wdrożeń klastrów HPC Pack na maszynach wirtualnych. Nie należy zmieniać topologii sieci klastra hello później.
2. **Przełącz węzły obliczeniowe hello zadania online toorun**
   
    Wybierz węzeł hello i użyj hello **przejdź do trybu Online** akcji w Menedżerze klastra HPC. Witaj węzły są gotowe toorun zadania.
3. **Przesyłanie zadań toohello klastra**
   
    Połącz toohello węzła głównego toosubmit zadania, lub skonfiguruj toodo komputera lokalnego, to. Aby uzyskać informacje, zobacz [tooan przesyłania zadań HPC klastra w systemie Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
4. **Podejmij hello węzłów w trybie offline i stop (deallocate) je**
   
    Gdy wszystko będzie gotowe wykonywanych zadań, należy podjąć hello węzły w tryb offline w Menedżerze klastra HPC. Następnie należy użyć tooshut narzędzi zarządzania systemem Azure je w dół.

## <a name="run-mpi-applications-on-hello-cluster"></a>Uruchamianie aplikacji MPI na powitania klastra
### <a name="example-run-mpipingpong-on-an-hpc-pack-cluster"></a>Przykład: Uruchom mpipingpong w klastrze HPC Pack
Wdrażanie pakietu HPC wystąpień hello z funkcją RDMA, uruchom tooverify hello HPC Pack **mpipingpong** na powitania klastra. **mpipingpong** wysyła pakiety danych między węzłami sparowanego wielokrotnie toocalculate pomiarów opóźnienia i przepływności oraz statystyki hello sieci aplikacji z obsługą funkcji RDMA. W tym przykładzie przedstawiono typowy wzorzec do uruchamiania zadań MPI (w tym przypadku **mpipingpong**) przy użyciu klastra hello **mpiexec** polecenia.

W tym przykładzie przyjęto założenie, dodać węzły platformy Azure w ramach konfiguracji "serii tooAzure" ([scenariusz 1](#scenario-1.-deploy-compute-intensive-worker-role-instances-\(PaaS\) in this article). Jeśli wdrożono HPC Pack w klastrze maszynach wirtualnych platformy Azure, będzie konieczne toomodify hello polecenia składni toospecify grupę na inny węzeł i ustaw dodatkowe zmienne toodirect sieci ruchu toohello RDMA sieci.

mpipingpong toorun w klastrze hello:

1. W węźle głównym hello lub na komputerze klienckim poprawnie skonfigurowane Otwórz wiersz polecenia.
2. tooestimate opóźnienia między parami węzłów we wdrożeniu serii Azure z czterech węzłów hello wpisz następujące polecenie toosubmit mpipingpong toorun zadania, rozmiar pakietu małe i dużo iteracji:
   
    ```Command
    job submit /nodegroup:azurenodes /numnodes:4 mpiexec -c 1 -affinity mpipingpong -p 1:100000 -op -s nul
    ```
   
    polecenie Hello zwraca identyfikator hello zadania hello, w której zostało przesłane.
   
    Jeśli wdrożono klastra HPC Pack hello wdrożonych na maszynach wirtualnych Azure, określ grupy węzła, który zawiera compute węzła maszyn wirtualnych wdrożonych w usłudze w chmurze pojedynczego i zmodyfikować hello **mpiexec** polecenia w następujący sposób:
   
    ```Command
    job submit /nodegroup:vmcomputenodes /numnodes:4 mpiexec -c 1 -affinity -env MSMPI_DISABLE_SOCK 1 -env MSMPI_PRECONNECT all -env MPICH_NETMASK 172.16.0.0/255.255.0.0 mpipingpong -p 1:100000 -op -s nul
    ```
3. Po ukończeniu zadania hello tooview hello danych wyjściowych (w tym przypadku dane wyjściowe hello zadanie 1 hello zadania), typ powitania po
   
    ```Command
    task view <JobID>.1
    ```
   
    gdzie &lt; *JobID* &gt; jest Identyfikatorem hello hello zadania, które zostało przesłane.
   
    dane wyjściowe Hello obejmują następujące toohello podobne wyniki opóźnienia.
   
    ![Czas oczekiwania na polecenie ping pong][pingpong1]
4. Przepływność tooestimate między parami Azure serii węzłów, typ hello następujące polecenie toosubmit toorun zadania **mpipingpong** rozmiar dużych pakietów i kilka iteracji:
   
    ```Command
    job submit /nodegroup:azurenodes /numnodes:4 mpiexec -c 1 -affinity mpipingpong -p 4000000:1000 -op -s nul
    ```
   
    polecenie Hello zwraca identyfikator hello zadania hello, w której zostało przesłane.
   
    W klastrze HPC Pack wdrożonych na maszynach wirtualnych Azure należy zmodyfikować polecenie hello zgodnie z opisem w kroku 2.
5. Po ukończeniu zadania hello tooview hello wyjściowych (w tym przypadku dane wyjściowe hello zadanie 1 hello zadania), typ powitania po:
   
    ```Command
    task view <JobID>.1
    ```
   
   Hello dane wyjściowe obejmują następujące toohello podobne wyniki przepływności.
   
   ![Przepływność pong ping][pingpong2]

### <a name="mpi-application-considerations"></a>Zagadnienia dotyczące aplikacji MPI
Poniżej przedstawiono zagadnienia dotyczące uruchamiania aplikacji MPI pakietem HPC na platformie Azure. Niektóre są stosowane tylko toodeployments węzły platformy Azure (wystąpienia roli procesu roboczego dodane w ramach konfiguracji "tooAzure serii").

* Wystąpienia roli procesu roboczego w usłudze w chmurze są okresowo ponownie udostępnić bez uprzedzenia przez platformę Azure (na przykład do konserwacji systemu lub w przypadku wystąpienia awarii). Jeśli wystąpienie jest udostępnienia, gdy jest uruchomione zadanie MPI, wystąpienie hello utracie danych i zwraca stan toohello podczas jej pierwszego wdrożenia, co może spowodować toofail zadań MPI hello. Witaj więcej węzłów, można użyć w jednym zadaniu MPI, które hello już hello zadanie jest uruchamiane, hello bardziej prawdopodobne, że jedną z wystąpień hello jest ponownie udostępnić podczas wykonywania zadania. Należy również rozważyć to wyznaczeniu jednego węzła w hello wdrożenia jako serwer plików.
* zadań MPI toorun na platformie Azure, nie masz toouse hello z funkcją RDMA wystąpień. Możesz użyć dowolnej wielkości wystąpienia, która jest obsługiwana przez HPC Pack. Jednak wystąpień z funkcją RDMA hello są zalecane dla uruchomionych zadań MPI stosunkowo dużej skali, opóźnienia toohello poufnych i hello przepustowości sieci hello, łączącej węzły hello. Jeśli używasz innych zadań MPI rozmiary toorun liter przepustowości i opóźnień, zalecamy uruchamiania małych zadań, w których pojedyncze zadanie działa na tylko kilku węzłów.
* Aplikacje wdrożone tooAzure wystąpienia są skojarzone z aplikacją hello umowy licencyjnej toohello podmiotu. Skontaktuj się z dostawcą hello dowolnej aplikacji komercyjnych licencjonowania lub inne ograniczenia dotyczące uruchamiania w chmurze hello. Nie wszyscy dostawcy oferują licencjonowanie oparte na płatności zgodnie z rzeczywistym użyciem.
* Wystąpieniach platformy Azure konieczne dalsze Instalator tooaccess lokalnymi węzłów, udziałów i serwerów licencji. Na przykład tooenable hello Azure węzłów tooaccess lokalnego serwera licencji, można skonfigurować do lokacji sieci wirtualnej platformy Azure.
* aplikacje MPI toorun w wystąpieniach platformy Azure, zarejestrować każda aplikacja MPI Zapora systemu Windows w wystąpieniach hello uruchamiając hello **hpcfwutil** polecenia. Dzięki temu MPI komunikacji tootake miejsce na porcie, który jest przypisywany dynamicznie przez zaporę Windows hello.
  
  > [!NOTE]
  > Wdrożeń tooAzure serii można również skonfigurować toorun polecenia wyjątek zapory automatycznie na wszystkie nowe Azure węzły, które są dodawane tooyour klastra. Po uruchomieniu hello **hpcfwutil** polecenia i sprawdź, czy Twoje działania aplikacji Dodaj hello polecenia tooa uruchamiania skryptu węzły platformy Azure. Aby uzyskać więcej informacji, zobacz [użycie skryptu uruchamiania dla węzłów Azure](https://technet.microsoft.com/library/jj899632.aspx).
  > 
  > 
* HPC Pack korzysta hello CCP_MPI_NETMASK klastra środowiska zmiennej toospecify zakres adresów dopuszczalne komunikacji MPI. Począwszy od HPC Pack 2012 R2 zmiennej środowiskowej klastra CCP_MPI_NETMASK hello wpływa tylko na MPI komunikacji między węzły obliczeń przyłączonych do domeny klastra (lokalnie lub w maszynach wirtualnych platformy Azure). Zmienna Hello jest ignorowana przez węzłów dodanych w konfiguracji tooAzure serii.
* Zadań MPI nie można uruchomić w wystąpieniach platformy Azure, które zostały wdrożone w różnych usług w chmurze (na przykład w przypadku wdrożeń tooAzure serii z szablonów inny węzeł lub węzły obliczeniowe maszyny Wirtualnej Azure wdrożyć w wielu usług w chmurze). Jeśli masz wielu wdrożeń węzła Azure, które są uruchamiane z szablonami inny węzeł hello MPI zadań należy uruchomić na tylko jeden zestaw węzłów Azure.
* Podczas dodawania węzłów Azure tooyour klastra i objęte hello online, usługa harmonogramu zadań HPC natychmiast podejmie toostart zadań na węzłach hello. Jeśli tylko część obciążenia można uruchomić na platformie Azure, upewnij się, zaktualizować, lub utworzyć zadania szablonów toodefine zadania, jakie typy, można uruchomić na platformie Azure. Na przykład tooensure, że zadania przekazane za pomocą szablonu zadania, uruchomić tylko na węzły platformy Azure, Dodaj hello węzła grupy właściwości toohello zadania szablon i wybierz AzureNodes jako hello wymagane wartości. toocreate grup niestandardowych do węzłów Azure, użyj polecenia cmdlet środowiska PowerShell klastra HPC HpcGroup Dodaj hello.

## <a name="next-steps"></a>Następne kroki
* Jako alternatywne toousing HPC Pack opracowywania toorun usługi partia zadań Azure hello MPI aplikacji na zarządzana pula węzły obliczeniowe na platformie Azure. Zobacz [użycie wielu wystąpień zadań toorun komunikat interfejsu (Passing Interface) aplikacji w partii zadań Azure](../../../batch/batch-mpi.md).
* Jeśli chcesz, aby toorun Linux MPI aplikacje, które uzyskują dostęp do sieci Azure RDMA hello, zobacz [skonfigurowanie aplikacji MPI Linux RDMA klastra toorun](../../linux/classic/rdma-cluster.md).

<!--Image references-->
[burst]:media/hpcpack-rdma-cluster/burst.png
[iaas]:media/hpcpack-rdma-cluster/iaas.png
[pingpong1]:media/hpcpack-rdma-cluster/pingpong1.png
[pingpong2]:media/hpcpack-rdma-cluster/pingpong2.png
