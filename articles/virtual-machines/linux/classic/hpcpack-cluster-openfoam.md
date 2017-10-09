---
title: aaaRun OpenFOAM pakietem HPC na maszynach wirtualnych systemu Linux | Dokumentacja firmy Microsoft
description: "Wdrażanie klastra Microsoft HPC Pack na platformie Azure, a następnie uruchom zadanie OpenFOAM na wielu węzłach obliczeniowych Linux przez sieć RDMA."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: c0bb1637-bb19-48f1-adaa-491808d3441f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 07/22/2016
ms.author: danlep
ms.openlocfilehash: 1a51ffe6804abb5156f01d580c9b7a4a9649377a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a>Uruchamianie oprogramowania OpenFoam przy użyciu pakietu Microsoft HPC w węzłach RDMA systemu Linux na platformie Azure
W tym artykule przedstawiono jednokierunkowej toorun OpenFoam w maszynach wirtualnych platformy Azure. W tym miejscu, w przypadku wdrażania klastra Microsoft HPC Pack z węzłami obliczeniowymi systemu Linux na platformie Azure i uruchom [OpenFoam](http://openfoam.com/) zadania z Intel MPI. Tak, aby węzły obliczeniowe hello komunikują się za pośrednictwem sieci Azure RDMA hello, można użyć z funkcją RDMA maszynach wirtualnych platformy Azure dla węzłów obliczeniowych hello. Inne toorun opcje OpenFoam na platformie Azure zawierają w pełni skonfigurowany komercyjnych obrazy dostępne w hello Marketplace, takie jak jego UberCloud [2.3 OpenFoam na CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/)i uruchamianych [partii zadań Azure](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/). 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

OpenFOAM (dla operacji Otwórz pole i manipulowania) to pakiet oprogramowania open source obliczeniową płynu dynamics (CFD), który jest powszechnie używany w inżynieryjne i naukowe w organizacjach użytku komercyjnego i academic. Obejmuje narzędzia do meshing, szczególnie snappyHexMesh zrównoleglone mesher złożonych CAD mają geometrię oraz wstępne i przetwarzania końcowego. Prawie wszystkie procesy wykonywane równolegle, włączanie użytkowników tootake pełne wykorzystanie sprzętu komputera za pośrednictwem interfejsu LINQ.  

Microsoft HPC Pack udostępnia funkcje toorun HPC na dużą skalę i równoległych aplikacji, w tym aplikacji MPI w klastrach maszyny wirtualne Microsoft Azure. HPC Pack obsługuje również uruchomione HPC systemu Linux węzła, maszyn wirtualnych wdrożonych w klastrze HPC Pack obliczeniowego aplikacji w systemie Linux. Zobacz [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](hpcpack-cluster.md) dla toousing wprowadzenie Linux obliczeniowe węzłów o HPC Pack.

> [!NOTE]
> W tym artykule przedstawiono sposób toorun obciążenia Linux MPI bez HPC Pack. Zakłada się, że masz pewną znajomość z Administracja systemu Linux i systemem obciążeń MPI klastry z systemem Linux. Jeśli używasz wersji MPI oraz OpenFOAM inny niż hello te wyświetlane w tym artykule, może być toomodify niektóre kroki instalacji i konfiguracji. 
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
* **Węzły obliczeniowe HPC Pack klastra z systemem Linux z funkcją RDMA** — wdrożenie klastra HPC Pack o rozmiarze A8, A9, H16r, lub H16rm Linux obliczeniowe węzłów za pomocą [szablonu usługi Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) lub [skrypt programu PowerShell Azure](hpcpack-cluster-powershell-script.md). Zobacz [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](hpcpack-cluster.md) hello wymagania wstępne i kroki dla każdej opcji. Jeśli wybierzesz hello opcji wdrażania skryptu programu PowerShell, zobacz hello przykładowy plik konfiguracyjny w hello przykładowych plików na końcu hello w tym artykule. Użyj tej konfiguracji klastra HPC Pack toodeploy bazującej na platformie Azure składające się z węzłem głównym A8 systemu Windows Server 2012 R2 rozmiar i węzły obliczeniowe 2 rozmiar A8 SUSE Linux Enterprise Server 12. Zastąp wartości odpowiednie dla Twojej subskrypcji i usługi nazw. 
  
  **Tooknow dodatkowe elementy**
  
  * Dla systemu Linux RDMA sieci wymagań wstępnych na platformie Azure, zobacz [wysokiej wydajności obliczeniowe rozmiarów maszyn wirtualnych](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  * Użycie hello opcji wdrażania skryptu programu Powershell, należy wdrożyć wszystkie węzły obliczeniowe Linux hello w ramach połączenia sieciowego RDMA hello toouse usługi jednej chmury.
  * Po wdrożeniu hello węzłów Linux należy połączyć SSH tooperform wszelkie dodatkowe zadania administracyjne. Znajdź szczegóły połączenia SSH powitania dla każdej maszyny Wirtualnej systemu Linux w hello portalu Azure.  
* **Intel MPI** -toorun OpenFOAM na SLES 12 HPC obliczeniowe węzłów na platformie Azure, konieczne tooinstall hello Intel MPI biblioteki 5 runtime ze hello [lokacji Intel.com](https://software.intel.com/en-us/intel-mpi-library/). (Intel MPI 5 jest preinstalowany na podstawie CentOS HPC obrazy).  W kolejnym kroku w razie potrzeby zainstaluj Intel MPI na systemie Linux węzłów obliczeniowych. tooprepare dla tego kroku po zarejestrowaniu się Intel, łącza hello hello potwierdzenie e-mail toohello powiązane strony sieci web. Następnie hello kopiowania Pobierz łącze do pliku .tgz hello hello odpowiednią wersję Intel MPI. W tym artykule jest oparta na Intel MPI wersji 5.0.3.048.
* **OpenFOAM źródła pakietu** — Pobierz hello OpenFOAM źródła pakietu oprogramowania dla systemu Linux z hello [lokacji OpenFOAM Foundation](http://openfoam.org/download/2-3-1-source/). Ten artykuł jest oparty na wersja źródła pakietu 2.3.1 dostępny do pobrania jako OpenFOAM 2.3.1.tgz. Postępuj zgodnie z instrukcjami hello w dalszej części tego artykułu toounpack i skompiluj OpenFOAM na węzły obliczeniowe hello systemu Linux.
* **EnSight** (opcjonalnie) - toosee hello wyniki symulacji OpenFOAM, Pobierz i zainstaluj hello [EnSight](https://www.ceisoftware.com/download/) program wizualizacji i analizy. Informacje licencyjne i pobierania znajdują się w lokacji EnSight hello.

## <a name="set-up-mutual-trust-between-compute-nodes"></a>Konfigurowanie wzajemnego zaufania między węzły obliczeń
Uruchomienie zadania między węzłami na wielu węzłach Linux wymaga tootrust węzłów hello wzajemnie (przez **rsh** lub **ssh**). Po utworzeniu klastra HPC Pack hello z hello Microsoft HPC Pack IaaS skrypt wdrożenia skryptu hello automatycznie konfiguruje stałe wzajemnego zaufania dla konta administratora hello, które określisz. Dla użytkowników niebędących administratorami utworzonych w domenie hello klaster dostępne są tooset tymczasowego relacji wzajemnego zaufania między węzłami hello zadania został przydzielony toothem i zniszcz relacji powitania po zakończeniu zadania hello. tooestablish zaufania dla każdego użytkownika, podaj klastra toohello parę kluczy RSA, używającego HPC Pack hello relacji zaufania.

### <a name="generate-an-rsa-key-pair"></a>Generowanie pary kluczy RSA
Łatwe toogenerate parę kluczy RSA, który zawiera klucz publiczny i klucz prywatny, uruchamiając hello Linux **ssh-keygen** polecenia.

1. Zaloguj się na tooa komputera z systemem Linux.
2. Uruchom następujące polecenie hello:
   
   ```
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > Naciśnij klawisz **Enter** toouse hello domyślne ustawienia ukończenie hello polecenia. Nie należy wprowadzać hasło tutaj; Po wyświetleniu monitu o podanie hasła, wystarczy nacisnąć klawisz **Enter**.
   > 
   > 
   
   ![Generowanie pary kluczy RSA][keygen]
3. Zmień katalog ~/.ssh toohello katalogu. Witaj klucz prywatny jest przechowywany w id_rsa i hello klucz publiczny w id_rsa.pub.
   
   ![Klucze prywatne i publiczne][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a>Dodaj klaster HPC Pack toohello pary kluczy hello
1. Należy pulpitu zdalnego połączenia tooyour węzła głównego z konta administratora HPC Pack (hello konta administratora, które można skonfigurować po uruchomieniu skryptu wdrażania hello).
2. Używanie standardowych systemu Windows Server toocreate procedury konto użytkownika domeny w domenie usługi Active Directory hello klastra. Na przykład użyć hello użytkowników usługi Active Directory i narzędzia komputerów na powitania węzła głównego. Przykłady Hello w tym artykule przyjęto założenie, że utworzenie użytkownika domeny o nazwie hpclab\hpcuser.
3. Utwórz plik o nazwie C:\cred.xml i skopiuj hello RSA danych klucza do niego. Przykładowy plik cred.xml znajduje się na końcu hello tego artykułu.
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. Otwórz wiersz polecenia i wpisz następujące polecenia, które tooset hello poświadczenia danych dla konta hpclab\hpcuser hello hello. Użyj hello **extendeddata** toopass parametru hello nazwę pliku C:\cred.xml utworzony hello danych.
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   To polecenie zakończy się pomyślnie bez danych wyjściowych. Po ustawieniu hello poświadczeń dla kont użytkowników hello potrzebne toorun zadania, przechowuj plik cred.xml hello w bezpiecznej lokalizacji lub usuń go.
5. Wygenerowany hello parę kluczy RSA w jednym z węzłów z systemem Linux Pamiętaj klucze hello toodelete po zakończeniu korzystania z nich. Jeśli HPC Pack znajdzie istniejący plik id_rsa lub plik id_rsa.pub, nie ustawia relacji wzajemnego zaufania.

> [!IMPORTANT]
> Nie zaleca się uruchamiania zadania Linux jako administrator klastra w klastrze udostępniony, ponieważ przesłane przez administratora zadania działa w ramach konta głównego hello na powitania Linux węzłów. Jednak zadanie przesłane przez użytkownika z systemem innym niż administrator uruchamia się przy użyciu lokalnego konta użytkownika systemu Linux hello takie same nazwy jako użytkownik zadania hello. W takim przypadku HPC Pack konfiguruje wzajemnego zaufania dla tego użytkownika w systemie Linux w węzłach hello przydzielone toohello zadania. Przed uruchomieniem zadania hello można skonfigurować ręcznie na węzłach Linux hello użytkownika w systemie Linux hello lub HPC Pack hello użytkownika automatycznie tworzy po przesłaniu zadania hello. Jeśli HPC Pack tworzy hello użytkownika, HPC Pack usuwa je po zakończeniu zadania hello. zagrożenia bezpieczeństwa tooreduce, HPC Pack usuwa klucze powitania po zakończeniu zadania.
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a>Konfigurowanie udziału plików dla węzłów systemu Linux
Teraz należy skonfigurować standardowe udziału SMB do folderu na powitania węzła głównego. tooallow hello Linux węzłów tooaccess pliki aplikacji za pomocą wspólnej ścieżki, hello instalacji węzłów Linux hello folderze udostępnionym. Jeśli chcesz, możesz użyć innego pliku opcji, takich jak udział plików Azure — zalecane dla wielu scenariuszy - lub udziału NFS do udostępniania. Znajduje się w pliku hello udostępniania informacji i szczegółowy opis kroków w [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](hpcpack-cluster.md).

1. Utwórz folder na powitania węzła głównego i udostępnić go tooEveryone ustawiając uprawnienia odczytu/zapisu. Na przykład udostępnić C:\OpenFOAM na powitania węzła głównego jako \\ \\SUSE12RDMA HN\OpenFOAM. W tym miejscu *SUSE12RDMA HN* jest nazwą hosta hello hello węzła głównego.
2. Otwórz okno programu Windows PowerShell i uruchom hello następującego polecenia:
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

pierwsze polecenie Hello tworzy folder o nazwie /openfoam we wszystkich węzłach grupy LinuxNodes hello. drugie polecenie Hello instaluje hello udostępnionego folderu //SUSE12RDMA-HN/OpenFOAM na węzłach Linux hello z dir_mode i file_mode too777 zestawu usługi bits. Witaj *username* i *hasło* hello polecenia powinien być hello poświadczeń użytkownika na powitania węzła głównego.

> [!NOTE]
> Witaj "\`" symbol w hello drugie polecenie jest symbolem ucieczki dla środowiska PowerShell. "\`,"hello "oznacza, że" (przecinek znak) jest częścią polecenia hello.
> 
> 

## <a name="install-mpi-and-openfoam"></a>Zainstaluj MPI i OpenFOAM
toorun OpenFOAM jako zadanie MPI sieci RDMA hello należy toocompile OpenFOAM z bibliotekami Intel MPI hello. 

Najpierw uruchom kilka **clusrun** polecenia tooinstall Intel MPI bibliotek (Jeśli nie jest jeszcze zainstalowany) i OpenFOAM na węzły systemu Linux. Użyj hello węzła głównego udział wcześniej skonfigurowany plików instalacyjnych hello tooshare między węzłami Linux hello.

> [!IMPORTANT]
> Te instalacji i kroki kompilacji to przykłady. Należy pewna znajomość tooensure administracji systemu Linux czy kompilatory zależne i biblioteki są prawidłowo zainstalowane. Może być konieczne toomodify niektórych zmiennych środowiskowych lub inne ustawienia dla Twojej wersji Intel MPI i OpenFOAM. Aby uzyskać więcej informacji, zobacz [Intel MPI biblioteki dla systemu Linux Przewodnik instalacji](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) i [OpenFOAM źródła pakietu instalacji](http://openfoam.org/download/2-3-1-source/) dla danego środowiska.
> 
> 

### <a name="install-intel-mpi"></a>Zainstaluj Intel MPI
Zapisz na powitania węzła głównego hello pobranego pakietu instalacyjnego MPI firmy Intel (l_mpi_p_5.0.3.048.tgz w tym przykładzie) w C:\OpenFoam, tak, aby węzły Linux hello mogą uzyskać dostęp do tego pliku z /openfoam. Następnie uruchom **clusrun** tooinstall Intel MPI biblioteki we wszystkich węzłach Linux hello.

1. następujące Hello poleceń pakietu instalacyjnego hello kopiowania i wyodrębnij go za/opt/intel w każdym węźle.
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. tooinstall Intel MPI biblioteki w trybie dyskretnym, użyj pliku silent.cfg. Przykład można znaleźć w hello przykładowych plików na końcu hello w tym artykule. Miejsce tego pliku w hello udostępnionego folderu /openfoam. Aby uzyskać szczegółowe informacje o pliku silent.cfg hello, zobacz [Intel MPI biblioteki dla systemu Linux Przewodnik instalacji - instalacji dyskretnej](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).
   
   > [!TIP]
   > Upewnij się, że możesz zapisać plik silent.cfg jako plik tekstowy z systemem Linux zakończenia (tylko LF, nie CR LF) wierszy. Ten krok zapewnia, że działa prawidłowo w węzłach Linux hello.
   > 
   > 
3. Zainstaluj biblioteki MPI Intel w trybie dyskretnym.
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a>Skonfiguruj MPI
Do testowania, należy dodać następujące wiersze toohello /etc/security/limits.conf na każdym z węzłów Linux hello hello:

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


Po zaktualizowaniu hello limits.conf pliku, należy ponownie uruchomić hello Linux węzłów. Na przykład użyć następujących hello **clusrun** polecenia:

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

Po ponownym uruchomieniu, upewnij się, że ten folder udostępniony hello jest zainstalowany jako /openfoam.

### <a name="compile-and-install-openfoam"></a>Kompilowanie i zainstalować OpenFOAM
W węźle głównym hello należy zapisać hello pobranego pakietu instalacyjnego dla hello tooC:\OpenFoam OpenFOAM źródła pakietu (w tym przykładzie OpenFOAM-2.3.1.tgz), dzięki czemu hello Linux węzły mogą uzyskać dostęp do tego pliku z /openfoam. Następnie uruchom **clusrun** polecenia toocompile OpenFOAM na wszystkich hello węzłów systemu Linux.

1. Utwórz /opt/OpenFOAM folderu w każdym węźle Linux folderu toothis kopiowania hello źródła pakietu i wyodrębnij go brak.
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. toocompile OpenFOAM z hello biblioteki MPI firmy Intel, należy najpierw skonfigurować niektóre zmienne środowiskowe Intel MPI i OpenFOAM. Użyj skryptu bash o nazwie settings.sh tooset hello zmiennych. Przykład można znaleźć w hello przykładowych plików na końcu hello w tym artykule. Umieść ten plik (zapisane przy użyciu zakończenia wierszy w systemie Linux) w hello udostępnionego folderu /openfoam. Ten plik zawiera także ustawienia hello MPI i OpenFOAM środowisk uruchomieniowych użycie nowszej toorun OpenFOAM zadania.
3. Instalowanie pakietów zależnych potrzebne toocompile OpenFOAM. W zależności od dystrybucji systemu Linux należy najpierw tooadd repozytorium. Uruchom **clusrun** podobne toohello następujące polecenia:
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    W razie potrzeby SSH tooeach Linux węzła toorun hello polecenia tooconfirm, które działają prawidłowo.
4. Uruchom następujące polecenie toocompile OpenFOAM hello. Proces kompilacji Hello przyjmuje niektórych toocomplete czasu i generuje dużą ilość danych wyjściowych toostandard informacji dziennika, należy więc hello **/ przeplatana** opcję przeplatana hello toodisplay w danych wyjściowych.
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > Witaj "\`" symbol w poleceniu hello jest symbolem ucieczki dla środowiska PowerShell. "\`&" oznacza hello "&" jest częścią polecenia hello.
   > 
   > 

## <a name="prepare-toorun-an-openfoam-job"></a>Przygotowanie zadania OpenFOAM toorun
Teraz get gotowe toorun zadań MPI wywołano sloshingTank3D, które jest jednym z przykładów OpenFoam hello, dwa węzły systemu Linux. 

### <a name="set-up-hello-runtime-environment"></a>Konfigurowanie środowiska uruchomieniowego hello
tooset się środowiska wykonawcze hello MPI i OpenFOAM w węzłach Linux hello, uruchom następujące polecenie w oknie programu Windows PowerShell na powitania węzła głównego hello. (To polecenie jest prawidłowe w systemie SUSE Linux.)

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a>Przygotowanie danych przykładowych
Użyj hello węzła głównego udziału skonfigurowane wcześniej tooshare plików między węzłami Linux hello (zainstalowany jako /openfoam).

1. Węzły obliczeniowe SSH tooone Twojego systemu Linux.
2. Uruchom hello następujące polecenie tooset się środowisko uruchomieniowe OpenFOAM hello, jeśli jeszcze nie zostało to zrobione.
   
   ```
   $ source /openfoam/settings.sh
   ```
3. Skopiuj folder udostępniony przykładowy toohello hello sloshingTank3D i przejdź tooit.
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. Użycie hello parametry domyślne tego przykładu, może potrwać dziesiątki toorun minut, dlatego może być toomodify niektórych toomake parametry szybsze wykonywanie. Jeden prosty wybór jest toomodify hello czasu krok zmienne deltaT i writeInterval w pliku system/controlDict hello. Ten plik przechowuje wszystkie dane wejściowe dotyczące kontroli toohello czasu i odczytywania i zapisywania danych rozwiązania. Na przykład można zmienić wartość hello deltaT z too0.5 0,05 i wartość hello writeInterval z 0,05 too0.5.
   
   ![Modyfikuj zmienne w kroku][step_variables]
5. Podaj odpowiednie wartości zmiennych hello w pliku system/decomposeParDict hello. W tym przykładzie użyto dwóch Linux węzłów każdego z 8 rdzeni, a więc Ustaw numberOfSubdomains too16 i n hierarchicalCoeffs too(1 1 16), co oznacza, że równolegle OpenFOAM z 16 procesów. Aby uzyskać więcej informacji, zobacz [Podręcznik użytkownika OpenFOAM: 3.4 aplikacji działa równolegle](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).
   
   ![Rozłóż procesów][decompose]
6. Uruchom hello poniższych poleceń z hello sloshingTank3D katalogu tooprepare hello przykładowych danych.
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. W węźle głównym hello powinien pojawić się pliki danych przykładowych hello są kopiowane do C:\OpenFoam\sloshingTank3D. (C:\OpenFoam jest hello folderu udostępnionego na powitania węzła głównego).
   
   ![Pliki danych na powitania węzła głównego][data_files]

### <a name="host-file-for-mpirun"></a>Plik hosta dla mpirun
W tym kroku utwórz plik hostów (listy węzłów obliczeniowych) które hello **mpirun** polecenia zastosowań.

1. W jednym z węzłów Linux hello Utwórz plik o nazwie hostfile w obszarze /openfoam, więc ten plik jest osiągalny w /openfoam/hostfile we wszystkich węzłach systemu Linux.
2. Zapis nazwy węzła Linux do tego pliku. W tym przykładzie hello plik zawiera hello następujące nazwy:
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > Można też utworzyć ten plik na C:\OpenFoam\hostfile na powitania węzła głównego. Jeśli wybierzesz tę opcję, zapisz go jako plik tekstowy z systemem Linux zakończenia wierszy (tylko LF, nie CR LF). Dzięki temu, że działa prawidłowo w węzłach Linux hello.
   > 
   > 
   
   **Bash skryptu otoki**
   
   Jeśli masz wiele węzłów systemu Linux i chcesz toorun Twojego zadania na tylko niektóre z nich, nie jest toouse dobrym rozwiązaniem, stałe hosta pliku, ponieważ nie wiadomo, węzły, które zostaną przydzielone tooyour zadania. W takim przypadku zapisu otoka skryptu bash dla **mpirun** toocreate hello automatycznie pliku hosta. Można znaleźć przykład otoki skryptu bash o nazwie hpcimpirun.sh na końcu hello w tym artykule i zapisz go jako /openfoam/hpcimpirun.sh. Ten przykładowy skrypt hello następujące:
   
   1. Konfiguruje hello zmiennych środowiskowych dla **mpirun**i dodanie polecenia parametrów toorun hello MPI zadanie wywołujące za pośrednictwem sieci RDMA hello. W takim przypadku ustawia hello następujące zmienne:
      
      * I_MPI_FABRICS = shm:dapl
      * I_MPI_DAPL_PROVIDER = ib0-v2 — ustawienia
      * I_MPI_DYNAMIC_CONNECTION = 0
   2. Tworzy plik hostów zgodnie z toohello $ zmiennej środowiskowej CCP_NODES_CORES, co jest ustawieniem węzłem głównym HPC powitania po aktywowaniu hello zadania.
      
      format Hello $CCP_NODES_CORES następujące tego wzorca:
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      gdzie
      
      * `<Number of nodes>`-toothis zadania przydzielone hello liczba węzłów.  
      * `<Name of node_n_...>`-toothis zadania przydzielone hello nazwę każdego węzła.
      * `<Cores of node_n_...>`-hello liczba rdzeni na powitania węzła toothis przydzielonego zadania.
      
      Na przykład jeśli zadanie hello wymaga dwóch węzłów toorun, $CCP_NODES_CORES jest podobny do
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. Wywołania hello **mpirun** polecenie i dołącza dwa wiersza polecenia toohello parametrów.
      
      * `--hostfile <hostfilepath>: <hostfilepath>`-tworzy ścieżki hello hello hosta pliku hello skryptu
      * `-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}`-zmienną środowiskową ustawione przez hello HPC Pack węzła głównego, który przechowuje hello liczba całkowita liczba rdzeni przydzielone toothis zadania. W takim przypadku określa hello liczbę procesów dla **mpirun**.

## <a name="submit-an-openfoam-job"></a>Prześlij zadanie OpenFOAM
Teraz można przesłać zadania w Menedżerze klastra HPC. Należy toopass hello skryptu hpcimpirun.sh w wiersze polecenia hello niektórych hello zadania.

1. Połącz tooyour węzła głównego klastra i uruchom Menedżera klastra HPC.
2. **W przystawce Zarządzanie zasobów**, upewnij się, że węzły obliczeniowe Linux hello w hello **Online** stanu. Jeśli nie, zaznacz je i kliknij przycisk **przejdź do trybu Online**.
3. W **zadania zarządzania**, kliknij przycisk **nowe zadanie**.
4. Wprowadź nazwę dla zadania, takie jak *sloshingTank3D*.
   
   ![Szczegóły zadania][job_details]
5. W **zadania zasoby**, wybierz typ zasobu jako "Węzła" hello i ustaw hello Minimum too2. Ta konfiguracja uruchamia zadanie hello na dwa węzły Linux, z których każdy ma osiem rdzeni w tym przykładzie.
   
   ![Zadanie zasobów][job_resources]
6. Kliknij przycisk **Edycja zadań** w hello nawigacji po lewej stronie, a następnie kliknij przycisk **Dodaj** tooadd zadania toohello zadań. Dodaj cztery zadania toohello zadania o hello następujące wiersze poleceń i ustawień.
   
   > [!NOTE]
   > Uruchomiona `source /openfoam/settings.sh` konfiguruje hello OpenFOAM MPI środowiska wykonawczego środowiska i, więc każdy hello następujące zadania wywołuje przed hello OpenFOAM polecenia.
   > 
   > 
   
   * **Zadanie 1**. Uruchom **decomposePar** toogenerate plików danych do uruchomienia **interDyMFoam** równolegle.
     
     * Przypisz jedno zadanie toohello węzła
     * **Wiersz polecenia** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`
     * **Katalog roboczy** -/ openfoam/sloshingTank3D
     
     Zobacz powitania po rysunku. Podobnie można skonfigurować hello pozostałych zadań.
     
     ![Szczegóły zadania 1][task_details1]
   * **Zadanie 2**. Uruchom **interDyMFoam** w przykładowym hello toocompute równoległych.
     
     * Przypisz dwa węzły toohello zadań
     * **Wiersz polecenia** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`
     * **Katalog roboczy** -/ openfoam/sloshingTank3D
   * **Zadanie 3**. Uruchom **reconstructPar** toomerge hello ustawia czas katalogów z każdego katalogu processor_N_ w pojedynczy zestaw.
     
     * Przypisz jedno zadanie toohello węzła
     * **Wiersz polecenia** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`
     * **Katalog roboczy** -/ openfoam/sloshingTank3D
   * **Zadanie 4**. Uruchom **foamToEnsight** w tooconvert równoległych plików wyników OpenFOAM hello do EnSight formatowania i umieścić w katalogu o nazwie Ensight w przypadku katalogu hello hello EnSight pliki.
     
     * Przypisz dwa węzły toohello zadań
     * **Wiersz polecenia** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`
     * **Katalog roboczy** -/ openfoam/sloshingTank3D
7. Dodaj zależności toothese zadania rosnąco zadań.
   
   ![Zależności zadań][task_dependencies]
8. Kliknij przycisk **przesyłania** toorun tego zadania.
   
   Domyślnie HPC Pack przesyła zadanie hello jako konta zalogowanego użytkownika. Po kliknięciu **przesyłania**, może być wyświetlone okno dialogowe z monitem tooenter hello nazwę i hasło użytkownika.
   
   ![Poświadczenia zadania][creds]
   
   W niektórych warunkach HPC Pack pamięta hello wejściowych przed i nie pokazuj tego okna dialogowego informacje o użytkowniku. toomake HPC Pack ponownie wyświetlić, wprowadź hello następujące polecenie w wierszu polecenia, a następnie przesłać zadania hello.
   
   ```
   hpccred delcreds
   ```
9. pobiera zadanie Hello dziesiątki minut tooseveral godzin zgodnie z parametrów toohello, ustawione przez hello próbki. Mapa cieplna hello jest widoczny hello zadania uruchomione w węzłach Linux hello. 
   
   ![Mapa cieplna][heat_map]
   
   W każdym węźle osiem procesy są uruchomione.
   
   ![Procesy systemu Linux][linux_processes]
10. Po zakończeniu zadania hello, Znajdź foldery w C:\OpenFoam\sloshingTank3D i plików dzienników hello C:\OpenFoam hello wyniki zadania.

## <a name="view-results-in-ensight"></a>Wyświetl wyniki w EnSight
Opcjonalnie użyj [EnSight](https://www.ceisoftware.com/) toovisualize i Analizuj wyniki hello hello OpenFOAM zadania. Więcej informacji o wizualizacji i animacji EnSight, zobacz [przewodnik wideo](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).

1. Po zainstalowaniu EnSight na powitania węzła głównego, należy ją uruchomić.
2. Otwórz C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.
   
   Zostanie wyświetlony zbiornika w podglądzie hello.
   
   ![Zbiornik w EnSight][tank]
3. Utwórz **Isosurface** z **internalMesh**, a następnie wybierz pozycję zmienna hello **alpha_water**.
   
   ![Utwórz isosurface][isosurface]
4. Ustawianie koloru hello **Isosurface_part** utworzony w poprzednim kroku hello. Na przykład ustawić go toowater niebieski.
   
   ![Edytuj isosurface kolorów][isosurface_color]
5. Utwórz **woluminu Iso** z **ściany** wybierając **ściany** w hello **części** panelu i kliknij hello **Isosurfaces**  przycisk hello w pasku narzędzi.
6. Okno dialogowe hello, wybierz **typu** jako **Isovolume** i ustaw hello Min z **zakres Isovolume** too0.5. toocreate hello isovolume, kliknij przycisk **Utwórz z zaznaczonych części**.
7. Ustawianie koloru hello **Iso_volume_part** utworzony w poprzednim kroku hello. Na przykład ustawić limitu górnego toodeep niebieski.
8. Ustawianie koloru hello **ściany**. Na przykład ustawić go tootransparent białym znakiem.
9. Teraz kliknij **odtwarzanie** toosee hello wyniki hello symulacji.
   
    ![Wynik zbiornika][tank_result]

## <a name="sample-files"></a>Przykładowe pliki
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a>Przykładowy plik konfiguracyjny XML dla wdrożenia klastra za pomocą skryptu programu PowerShell
 ```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>suse12rdmavnet</VNetName>
    <SubnetName>SUSE12RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>SUSE12RDMA-HN</VMName>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>SUSE12RDMA-LN%1%</VMNamePattern>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <NodeCount>2</NodeCount>
      <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

### <a name="sample-credxml-file"></a>Przykładowy plik cred.xml
```
<ExtendedData>
  <PrivateKey>-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAxJKBABhnOsE9eneGHvsjdoXKooHUxpTHI1JVunAJkVmFy8JC
qFt1pV98QCtKEHTC6kQ7tj1UT2N6nx1EY9BBHpZacnXmknpKdX4Nu0cNlSphLpru
lscKPR3XVzkTwEF00OMiNJVknq8qXJF1T3lYx3rW5EnItn6C3nQm3gQPXP0ckYCF
Jdtu/6SSgzV9kaapctLGPNp1Vjf9KeDQMrJXsQNHxnQcfiICp21NiUCiXosDqJrR
AfzePdl0XwsNngouy8t0fPlNSngZvsx+kPGh/AKakKIYS0cO9W3FmdYNW8Xehzkc
VzrtJhU8x21hXGfSC7V0ZeD7dMeTL3tQCVxCmwIDAQABAoIBAQCve8Jh3Wc6koxZ
qh43xicwhdwSGyliZisoozYZDC/ebDb/Ydq0BYIPMiDwADVMX5AqJuPPmwyLGtm6
9hu5p46aycrQ5+QA299g6DlF+PZtNbowKuvX+rRvPxagrTmupkCswjglDUEYUHPW
05wQaNoSqtzwS9Y85M/b24FfLeyxK0n8zjKFErJaHdhVxI6cxw7RdVlSmM9UHmah
wTkW8HkblbOArilAHi6SlRTNZG4gTGeDzPb7fYZo3hzJyLbcaNfJscUuqnAJ+6pT
iY6NNp1E8PQgjvHe21yv3DRoVRM4egqQvNZgUbYAMUgr30T1UoxnUXwk2vqJMfg2
Nzw0ESGRAoGBAPkfXjjGfc4HryqPkdx0kjXs0bXC3js2g4IXItK9YUFeZzf+476y
OTMQg/8DUbqd5rLv7PITIAqpGs39pkfnyohPjOe2zZzeoyaXurYIPV98hhH880uH
ZUhOxJYnlqHGxGT7p2PmmnAlmY4TSJrp12VnuiQVVVsXWOGPqHx4S4f9AoGBAMn/
vuea7hsCgwIE25MJJ55FYCJodLkioQy6aGP4NgB89Azzg527WsQ6H5xhgVMKHWyu
Q1snp+q8LyzD0i1veEvWb8EYifsMyTIPXOUTwZgzaTTCeJNHdc4gw1U22vd7OBYy
nZCU7Tn8Pe6eIMNztnVduiv+2QHuiNPgN7M73/x3AoGBAOL0IcmFgy0EsR8MBq0Z
ge4gnniBXCYDptEINNBaeVStJUnNKzwab6PGwwm6w2VI3thbXbi3lbRAlMve7fKK
B2ghWNPsJOtppKbPCek2Hnt0HUwb7qX7Zlj2cX/99uvRAjChVsDbYA0VJAxcIwQG
TxXx5pFi4g0HexCa6LrkeKMdAoGAcvRIACX7OwPC6nM5QgQDt95jRzGKu5EpdcTf
g4TNtplliblLPYhRrzokoyoaHteyxxak3ktDFCLj9eW6xoCZRQ9Tqd/9JhGwrfxw
MS19DtCzHoNNewM/135tqyD8m7pTwM4tPQqDtmwGErWKj7BaNZARUlhFxwOoemsv
R6DbZyECgYEAhjL2N3Pc+WW+8x2bbIBN3rJcMjBBIivB62AwgYZnA2D5wk5o0DKD
eesGSKS5l22ZMXJNShgzPKmv3HpH22CSVpO0sNZ6R+iG8a3oq4QkU61MT1CfGoMI
a8lxTKnZCsRXU1HexqZs+DSc+30tz50bNqLdido/l5B4EJnQP03ciO0=
-----END RSA PRIVATE KEY-----</PrivateKey>
  <PublicKey>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDEkoEAGGc6wT16d4Ye+yN2hcqigdTGlMcjUlW6cAmRWYXLwkKoW3WlX3xAK0oQdMLqRDu2PVRPY3qfHURj0EEellpydeaSekp1fg27Rw2VKmEumu6Wxwo9HddXORPAQXTQ4yI0lWSerypckXVPeVjHetbkSci2foLedCbeBA9c/RyRgIUl227/pJKDNX2Rpqly0sY82nVWN/0p4NAyslexA0fGdBx+IgKnbU2JQKJeiwOomtEB/N492XRfCw2eCi7Ly3R8+U1KeBm+zH6Q8aH8ApqQohhLRw71bcWZ1g1bxd6HORxXOu0mFTzHbWFcZ9ILtXRl4Pt0x5Mve1AJXEKb username@servername;</PublicKey>
</ExtendedData>
```
### <a name="sample-silentcfg-file-tooinstall-mpi"></a>Przykładowe silent.cfg pliku tooinstall MPI
```
# Patterns used toocheck silent configuration file
#
# anythingpat - any string
# filepat     - hello file location pattern (/file/location/to/license.lic)
# lspat       - hello license server address pattern (0123@hostname)
# snpat       - hello serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components tooinstall, valid values are: {ALL, DEFAULTS, anythingpat}
COMPONENTS=DEFAULTS

# installation mode, valid values are: {install, modify, repair, uninstall}
PSET_MODE=install

# directory for non-RPM database, valid values are: {filepat}
#NONRPM_DB_DIR=filepat

# Serial number, valid values are: {snpat}
#ACTIVATION_SERIAL_NUMBER=snpat

# License file or license server, valid values are: {lspat, filepat}
#ACTIVATION_LICENSE_FILE=

# Activation type, valid values are: {exist_lic, license_server, license_file, trial_lic, serial_number}
ACTIVATION_TYPE=trial_lic

# Path toohello cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes tooenable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes tooupdate ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a>Przykładowy skrypt settings.sh
```
#!/bin/bash

# impi
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# openfoam
export FOAM_INST_DIR=/opt/OpenFOAM
source /opt/OpenFOAM/OpenFOAM-2.3.1/etc/bashrc
export WM_MPLIB=INTELMPI
```


### <a name="sample-hpcimpirunsh-script"></a>Przykładowy skrypt hpcimpirun.sh
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"

# Set mpirun runtime evironment
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# mpirun command
MPIRUN=mpirun
# Argument of "--hostfile"
NODELIST_OPT="--hostfile"
# Argument of "-np"
NUMPROCESS_OPT="-np"

# Get node information from ENVs
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # CCP_NODES_CORES is not found or is empty, just run hello mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into hello hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello mpirun with hostfile arg
    ${MPIRUN} ${NUMPROCESS_OPT} ${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}

```





<!--Image references-->
[keygen]:media/hpcpack-cluster-openfoam/keygen.png
[keys]:media/hpcpack-cluster-openfoam/keys.png
[step_variables]:media/hpcpack-cluster-openfoam/step_variables.png
[data_files]:media/hpcpack-cluster-openfoam/data_files.png
[decompose]:media/hpcpack-cluster-openfoam/decompose.png
[job_details]:media/hpcpack-cluster-openfoam/job_details.png
[job_resources]:media/hpcpack-cluster-openfoam/job_resources.png
[task_details1]:media/hpcpack-cluster-openfoam/task_details1.png
[task_dependencies]:media/hpcpack-cluster-openfoam/task_dependencies.png
[creds]:media/hpcpack-cluster-openfoam/creds.png
[heat_map]:media/hpcpack-cluster-openfoam/heat_map.png
[tank]:media/hpcpack-cluster-openfoam/tank.png
[tank_result]:media/hpcpack-cluster-openfoam/tank_result.png
[isosurface]:media/hpcpack-cluster-openfoam/isosurface.png
[isosurface_color]:media/hpcpack-cluster-openfoam/isosurface_color.png
[linux_processes]:media/hpcpack-cluster-openfoam/linux_processes.png
