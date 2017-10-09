---
title: aaaNAMD z pakietem Microsoft HPC na maszynach wirtualnych systemu Linux | Dokumentacja firmy Microsoft
description: "Wdrażanie klastra Microsoft HPC Pack na platformie Azure i uruchom symulacji NAMD z charmrun na wielu węzłach obliczeniowych systemu Linux"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 76072c6b-ac35-4729-ba67-0d16f9443bd7
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/13/2016
ms.author: danlep
ms.openlocfilehash: 90c722f66b494335a62c0613079366ae99002076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a>Uruchamianie oprogramowania NAMD przy użyciu pakietu Microsoft HPC w węzłach obliczeniowych systemu Linux na platformie Azure
W tym artykule przedstawiono jednokierunkowej toorun Linux wysokiej wydajności (HPC) obciążenia na maszynach wirtualnych Azure. W tym miejscu można skonfigurować [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) klaster na platformie Azure z węzłami obliczeniowymi systemu Linux i uruchamianie [NAMD](http://www.ks.uiuc.edu/Research/namd/) toocalculate symulacji i wizualizację struktury hello dużych biomolekularnych systemu.  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* **NAMD** (dla programu Dynamics molekularnej Nanoscale) jest pakiet równoległych dynamics molekularnej przeznaczone do symulacji wysokiej wydajności dużych biomolekularnych systemów zawierający się toomillions atomami. Przykładami tych systemów wirusy, komórki struktury i białek duże. NAMD skaluje toohundreds rdzeniami dla typowych symulacje i toomore niż 500 000 rdzeniami dla symulacje największy hello.
* **Microsoft HPC Pack** udostępnia funkcje toorun HPC na dużą skalę i aplikacje równoległe w klastrach komputerów lokalnych lub maszyn wirtualnych platformy Azure. Pierwotnie opracowany jako rozwiązaniem w przypadku obciążeń HPC systemu Windows HPC Pack obsługuje teraz aplikacje HPC systemu Linux w systemie Linux obliczeniowe węzła maszyn wirtualnych wdrożonych w klastrze HPC Pack. Zobacz [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](hpcpack-cluster.md) wprowadzenie.

Dla innych opcji toorun HPC systemu Linux obciążeń na platformie Azure, zobacz [zasobów technicznych partii i wysoką wydajność pracy](../../../batch/batch-hpc-solutions.md).

## <a name="prerequisites"></a>Wymagania wstępne
* **Węzły obliczeniowe HPC Pack klastra z systemem Linux** — wdrożenie klastra HPC Pack z węzłami obliczeniowymi systemu Linux na platformie Azure przy użyciu [szablonu usługi Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) lub [skrypt programu PowerShell Azure](hpcpack-cluster-powershell-script.md) . Zobacz [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](hpcpack-cluster.md) hello wymagania wstępne i kroki dla każdej opcji. Jeśli wybierzesz hello opcji wdrażania skryptu programu PowerShell, zobacz hello przykładowy plik konfiguracyjny w hello przykładowych plików na końcu hello w tym artykule. Ten plik służy do konfigurowania klastra bazujących na platformie Azure HPC Pack składające się z węzłem głównym systemu Windows Server 2012 R2 i cztery węzły obliczeniowe 6.6 CentOS duży rozmiar. Ten plik należy dostosować zgodnie z wymaganiami środowiska.
* **Pliki oprogramowania i samouczek NAMD** — Pobierz NAMD oprogramowania dla systemu Linux z hello [NAMD](http://www.ks.uiuc.edu/Research/namd/) lokacji (rejestracja wymagane). W tym artykule jest oparta na NAMD wersji 2.10 i używa hello [Linux-x86_64 (64-bit Intel/AMD z Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archiwum. Również pobrać hello [plików samouczka NAMD](http://www.ks.uiuc.edu/Training/Tutorials/#namd). Pobieranie Hello są pliki tar i trzeba plików systemu Windows hello tooextract narzędzia na powitania węzła głównego klastra. tooextract hello pliki, wykonaj instrukcje hello w dalszej części tego artykułu. 
* **VMD** (opcjonalnie) — toosee hello wyników zadania NAMD, Pobierz i zainstaluj program molekularnej wizualizacji hello [VMD](http://www.ks.uiuc.edu/Research/vmd/) na wybranym komputerze. Bieżąca wersja Hello jest 1.9.2. Zobacz hello VMD Pobierz tooget lokacji uruchomiona.  

## <a name="set-up-mutual-trust-between-compute-nodes"></a>Konfigurowanie wzajemnego zaufania między węzły obliczeń
Uruchomienie zadania między węzłami na wielu węzłach Linux wymaga tootrust węzłów hello wzajemnie (przez **rsh** lub **ssh**). Po utworzeniu klastra HPC Pack hello z hello Microsoft HPC Pack IaaS skrypt wdrożenia skryptu hello automatycznie konfiguruje stałe wzajemnego zaufania dla konta administratora hello, które określisz. Dla użytkowników niebędących administratorami utworzonych w domenie hello klastra masz tooset tymczasowego relacji wzajemnego zaufania między węzłami hello gdy zadanie jest przydzielany toothem. Następnie należy zniszczyć hello relacji po zakończeniu zadania hello. toodo to dla każdego użytkownika, podaj klastra toohello parę kluczy RSA które HPC Pack korzysta z relacji zaufania hello tooestablish. Postępuj zgodnie z instrukcjami.

### <a name="generate-an-rsa-key-pair"></a>Generowanie pary kluczy RSA
Łatwe toogenerate parę kluczy RSA, który zawiera klucz publiczny i klucz prywatny, uruchamiając hello Linux **ssh-keygen** polecenia.

1. Zaloguj się na tooa komputera z systemem Linux.
2. Uruchom następujące polecenie hello:
   
   ```bash
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
1. [Połącz przez pulpit zdalny](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello węzła głównego maszynę Wirtualną przy użyciu hello poświadczeń domeny podana podczas wdrażania klastra hello (na przykład hpc\clusteradmin). Witaj klastra można zarządzać z węzła głównego hello.
2. Używanie standardowych systemu Windows Server toocreate procedury konto użytkownika domeny w domenie usługi Active Directory hello klastra. Na przykład użyć hello użytkowników usługi Active Directory i narzędzia komputerów na powitania węzła głównego. Przykłady Hello w tym artykule przyjęto założenie, że utworzenie użytkownika domeny o nazwie hpcuser w domenie hpclab hello (hpclab\hpcuser).
3. Dodawanie hello domeny użytkownika toohello HPC Pack klastra jako użytkownika klastra. Aby uzyskać instrukcje, zobacz [Dodaj lub usuń użytkowników klastra](https://technet.microsoft.com/library/ff919330.aspx).
4. Utwórz plik o nazwie C:\cred.xml i skopiuj hello RSA danych klucza do niego. Przykład można znaleźć w hello przykładowych plików na końcu hello w tym artykule.
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. Otwórz wiersz polecenia i wpisz następujące polecenia, które tooset hello poświadczenia danych dla konta hpclab\hpcuser hello hello. Użyj hello **extendeddata** toopass parametru hello nazwę pliku C:\cred.xml hello utworzony hello danych.
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   To polecenie zakończy się pomyślnie bez danych wyjściowych. Po ustawieniu hello poświadczeń dla kont użytkowników hello potrzebne toorun zadania, przechowuj plik cred.xml hello w bezpiecznej lokalizacji lub usuń go.
6. Wygenerowany hello parę kluczy RSA w jednym z węzłów z systemem Linux Pamiętaj klucze hello toodelete po zakończeniu korzystania z nich. HPC Pack nie konfiguruje wzajemnego zaufania w przypadku odnalezienia istniejącego pliku id_rsa lub id_rsa.pub pliku.

> [!IMPORTANT]
> Nie zaleca się uruchamiania zadania Linux jako administrator klastra w klastrze udostępniony, ponieważ przesłane przez administratora zadania działa w ramach konta głównego hello na powitania Linux węzłów. Zadania zostało przesłane przez użytkownika bez uprawnień administratora jest uruchamiany przy użyciu lokalnego konta użytkownika systemu Linux, hello takie same nazwy jako hello zadania użytkownika. W takim przypadku HPC Pack konfiguruje wzajemnego zaufania dla tego użytkownika w systemie Linux we wszystkich węzłach hello przydzielone toohello zadania. Przed uruchomieniem zadania hello można skonfigurować ręcznie na węzłach Linux hello użytkownika w systemie Linux hello lub HPC Pack hello użytkownika automatycznie tworzy po przesłaniu zadania hello. Jeśli HPC Pack tworzy hello użytkownika, HPC Pack usuwa je po zakończeniu zadania hello. tooreduce zagrożeniem bezpieczeństwa, powitalne klucze są usuwane po zakończeniu zadania hello na węzłach hello.
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a>Konfigurowanie udziału plików dla węzłów systemu Linux
Teraz skonfigurować udział plików SMB i instalacji hello folderu udostępnionego na wszystkie Linux węzłów tooallow hello Linux węzłów tooaccess NAMD pliki z wspólnej ścieżki. Poniżej przedstawiono kroki toomount folderu udostępnionego na powitania węzła głównego. Takie jak CentOS 6.6 dystrybucji, które aktualnie nie obsługują usługę Azure plików hello udział jest zalecane. Jeśli węzły Linux obsługują udziału plików platformy Azure, zobacz [jak toouse magazyn plików Azure z systemem Linux](../../../storage/files/storage-how-to-use-files-linux.md). W przypadku pliku dodatkowe opcje udostępniania pakietem HPC, zobacz [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](hpcpack-cluster.md).

1. Utwórz folder na powitania węzła głównego i udostępnić go tooEveryone ustawiając uprawnienia odczytu/zapisu. W tym przykładzie \\ \\CentOS66HN\Namd jest nazwą hello hello folderu, gdzie CentOS66HN jest nazwą hosta hello hello węzła głównego.
2. Utwórz podfolder o nazwie namd2 w folderze udostępnionym hello. W namd2 należy utworzyć inny podfolder o nazwie namdsample.
3. Wyodrębnij pliki NAMD hello w folderze hello przy użyciu wersji systemu Windows z **tar** lub innego narzędzia systemu Windows, który operuje na archiwa tar. 
   
   * Wyodrębnij hello NAMD tar archiwum zbyt\\\\CentOS66HN\Namd\namd2.
   * Wyodrębnij pliki samouczka hello w obszarze \\ \\CentOS66HN\Namd\namd2\namdsample.
4. Otwórz okno programu Windows PowerShell i uruchom następujące polecenia toomount hello folderu udostępnionego na węzłach Linux hello hello.
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

pierwsze polecenie Hello tworzy folder o nazwie /namd2 we wszystkich węzłach grupy LinuxNodes hello. drugie polecenie Hello instaluje hello udostępnionego folderu //CentOS66HN/Namd/namd2 na powitania folder o dir_mode i file_mode too777 zestawu usługi bits. Witaj *username* i *hasło* hello polecenia powinien być hello poświadczeń użytkownika na powitania węzła głównego.

> [!NOTE]
> Witaj "\`" symbol w hello drugie polecenie jest symbolem ucieczki dla środowiska PowerShell. "\`,"hello "oznacza, że" (przecinek znak) jest częścią polecenia hello.
> 
> 

## <a name="create-a-bash-script-toorun-a-namd-job"></a>Utwórz zadanie NAMD toorun skryptu Bash
Zadanie NAMD musi *wstawienia* plik **charmrun** toodetermine hello liczba węzłów toouse podczas uruchamiania procesów NAMD. Możesz użyć skryptu Bash, który generuje plik wstawienia hello i uruchamia **charmrun** z tym plikiem wstawienia. Następnie można przesłać zadania NAMD w Menedżer klastra HPC, który wywołuje ten skrypt.

Za pomocą dowolnego edytora tekstu, utworzyć skrypt Bash w hello /namd2 folderu zawierającego pliki programów NAMD hello i nadaj mu nazwę hpccharmrun.sh. W przypadku szybkiego Weryfikacja koncepcji, skopiuj hello skrypt hpccharmrun.sh podana na końcu hello w tym artykule i przejść za[przesłać zadania NAMD](#submit-a-namd-job).

> [!TIP]
> Zapisz skrypt jako plik tekstowy z systemem Linux zakończenia (tylko LF, nie CR LF) wierszy. Dzięki temu, że działa prawidłowo w węzłach Linux hello.
> 
> 

Poniżej przedstawiono szczegółowe informacje o czego ten skrypt bash. 

1. Zdefiniuj niektóre zmienne.
   
   ```bash
   #!/bin/bash
   
   # hello path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. Pobierz informacje węzła z hello zmiennych środowiskowych. $NODESCORES przechowuje listę słów podziału z $CCP_NODES_CORES. $COUNT jest rozmiarem hello $NODESCORES.
   
   ```
   # Get node information from hello environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   format Hello zmiennej CCP_NODES_CORES $ hello jest następujący:
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   Ta zmienna wymieniono hello łączna liczba węzłów, nazwy węzła i liczba rdzeni w każdym węźle przydzielonych toohello zadania. Na przykład jeśli zadanie hello musi 10 toorun rdzeni, wartość hello $CCP_NODES_CORES jest podobny do:
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. Jeśli nie ustawiono zmiennej CCP_NODES_CORES $ hello, uruchom **charmrun** bezpośrednio. (Ten może występować tylko po uruchomieniu tego skryptu bezpośrednio na węzły systemu Linux.)
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. Lub Utwórz plik wstawienia **charmrun**.
   
   ```
   else
     # Create hello nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write hello head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into hello nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. Uruchom **charmrun** z plikiem wstawienia hello, Pobierz stanu powrotu, a następnie usuń plik wstawienia hello na końcu hello.
   
   ${CCP_NUMCPUS} jest ustawiony przez węzłem głównym HPC Pack hello innej zmiennej środowiskowej. Przechowuje hello liczba całkowita liczba rdzeni przydzielone toothis zadania. Będziemy używać go toospecify hello liczba procesów charmrun.
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. Wyjście z hello **charmrun** stan powrotu.
   
   ```
   exit ${RTNSTS}
   ```

Poniżej przedstawiono informacje hello w pliku wstawienia hello, w którym skrypt hello generuje:

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

Na przykład:

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a>Prześlij zadanie NAMD
Teraz wszystko jest gotowe toosubmit NAMD zadania w Menedżerze klastra HPC.

1. Połącz tooyour węzła głównego klastra i uruchom Menedżera klastra HPC.
2. W **zarządzanie zasobami**, upewnij się, że węzły obliczeniowe Linux hello w hello **Online** stanu. Jeśli nie, zaznacz je i kliknij przycisk **przejdź do trybu Online**.
3. W **zadania zarządzania**, kliknij przycisk **nowe zadanie**.
4. Wprowadź nazwę dla zadania, takie jak *hpccharmrun*.
   
   ![Nowe zadanie HPC][namd_job]
5. Na powitania **szczegóły zadania** w obszarze **zasobów zadania**, wybierz typ hello zasobu jako **węzła** i zestaw hello **Minimum** too3. , możemy uruchomić zadania hello na trzy węzły systemu Linux i każdy węzeł ma cztery rdzenie.
   
   ![Zadanie zasobów][job_resources]
6. Kliknij przycisk **Edycja zadań** w hello nawigacji po lewej stronie, a następnie kliknij przycisk **Dodaj** tooadd zadania toohello zadań.    
7. Na powitania **szczegółów zadań i Przekierowanie We/Wy** strony hello ustaw następujące wartości:
   
   * **Wiersz polecenia**-
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`
     
     > [!TIP]
     > Witaj poprzedniego wiersza polecenia jest jednego polecenia bez podziałów wierszy. W wielu wierszach, w obszarze jest zawijana tooappear **wiersza polecenia**.
     > 
     > 
   * **Katalog roboczy** -/namd2
   * **Co najmniej** — 3
     
     ![Szczegóły zadania][task_details]
     
     > [!NOTE]
     > W tym miejscu ustawić katalogu roboczego hello ponieważ **charmrun** próbuje toonavigate toohello tego samego katalogu roboczego w każdym węźle. Jeśli nie ustawiono katalogu roboczego hello, HPC Pack uruchamia polecenie hello w losowo wybranej nazwie folder utworzony w jednym z węzłów Linux hello. Powoduje to hello następujący błąd na powitania innych węzłów: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid ten problem, określ ścieżkę folderu, które są dostępne przez wszystkie węzły hello katalog roboczy.
     > 
     > 
8. Kliknij przycisk **OK** , a następnie kliknij przycisk **przesyłania** toorun tego zadania.
   
   Domyślnie HPC Pack przesyła zadanie hello jako konta zalogowanego użytkownika. Okno dialogowe może monitować tooenter hello nazwę i hasło użytkownika po kliknięciu **przesyłania**.
   
   ![Poświadczenia zadania][creds]
   
   W niektórych warunkach HPC Pack pamięta hello wejściowych przed i nie pokazuj tego okna dialogowego informacje o użytkowniku. toomake HPC Pack ponownie wyświetlić, wprowadź hello następujące polecenie w wierszu polecenia, a następnie przesłać zadania hello.
   
   ```command
   hpccred delcreds
   ```
9. zadanie Hello zajmuje kilka minut toofinish.
10. Znajdź dziennik zadań hello na \\ <headnodeName>pliki wyjściowe \Namd\namd2\namd2_hpccharmrun.log i hello \\ <headnodeName>\Namd\namd2\namdsample\1-2-sphere\.
11. Opcjonalnie można uruchomić VMD tooview wyniki zadania. kroki Hello do wizualizacji pliki wyjściowe NAMD hello (w tym przypadku związku białka ubiquitin, w zakresie limitu górnego) są poza zakres tego artykułu hello. Zobacz [samouczek NAMD](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) szczegółowe informacje.
    
    ![Wyniki zadania][vmd_view]

## <a name="sample-files"></a>Przykładowe pliki
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a>Przykładowy plik konfiguracyjny XML dla wdrożenia klastra za pomocą skryptu programu PowerShell
```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
      <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS66HN</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS66LN-%00%</VMNamePattern>
    <ServiceName>MyLnxCNService</ServiceName>
     <VMSize>Large</VMSize>
     <NodeCount>4</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-66-20150325</ImageName>
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

### <a name="sample-hpccharmrunsh-script"></a>Przykładowy skrypt hpccharmrun.sh
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
# Charmrun command
CHARMRUN=${SCRIPT_PATH}/charmrun
# Argument of ++nodelist
NODELIST_OPT="++nodelist"
# Argument of ++p
NUMPROCESS="+p"

# Get node information from ENVs
# CCP_NODES_CORES=3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 4
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # If CCP_NODES_CORES is not found or is empty, just run hello charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create hello nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write hello head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into hello nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello charmrun with nodelist arg
    #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
    ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}
```

 

<!--Image references-->
[keygen]:media/hpcpack-cluster-namd/keygen.png
[keys]:media/hpcpack-cluster-namd/keys.png
[namd_job]:media/hpcpack-cluster-namd/namd_job.png
[job_resources]:media/hpcpack-cluster-namd/job_resources.png
[creds]:media/hpcpack-cluster-namd/creds.png
[task_details]:media/hpcpack-cluster-namd/task_details.png
[vmd_view]:media/hpcpack-cluster-namd/vmd_view.png
