---
title: "Planowanie wdrożenia usługi Site Recovery aaaAzure dla VMware do platformy Azure | Dokumentacja firmy Microsoft"
description: "Jest to hello — Podręcznik użytkownika planowania wdrożenia usługi Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: garavd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/28/2017
ms.author: nisoneji
ms.openlocfilehash: a8c13cd47850575769e0186528807bc525bdeec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-deployment-planner"></a>Planista wdrożenia usługi Azure Site Recovery
W tym artykule jest Podręcznik użytkownika Azure lokacji odzyskiwania wdrożenia Planistę hello wdrożeń produkcyjnych VMware do platformy Azure.

## <a name="overview"></a>Omówienie

Przed rozpoczęciem ochrony dowolnego maszynach wirtualnych VMware (VM) przy użyciu usługi Site Recovery, Przydziel wystarczającą przepustowość, oparte na dziennych zmian danych szybkość, toomeet Twojego cel punktu odzyskiwania odpowiednią (RPO). Można się toodeploy hello prawo liczba konfiguracji serwerów i procesu serwerów lokalnych.

Należy również toocreate hello odpowiedniego typu i numer docelowej kontami magazynu Azure. Możesz utworzyć konta magazynu w warstwie Standardowa lub Premium, biorąc pod uwagę wzrost w zakresie źródłowych serwerów produkcyjnych z powodu zwiększania użycia w czasie. Wybierz typ magazynu hello na maszynie Wirtualnej, na podstawie charakterystyk obciążenia (na przykład operacje odczytu/zapisu We/Wy na sekundę [IOPS] lub przenoszenie danych) i ogranicza usługi Site Recovery.

Hello Site Recovery wdrożenia planistę publicznej wersji zapoznawczej jest narzędziem wiersza polecenia, który jest obecnie dostępny tylko w przypadku scenariusza VMware do platformy Azure hello. Można zdalnie profilu za pomocą tego narzędzia (z produkcji wpływu jakiejkolwiek) toounderstand hello przepustowości i wymagania dotyczące usługi Azure Storage dla pomyślna replikacja maszyny wirtualne VMware i testowanie trybu failover. Narzędzie hello można uruchomić bez konieczności instalowania dowolnej usługi Site Recovery składniki lokalnymi. Jednak tooget dokładne osiągnąć przepływności, zaleca się uruchomienie hello planner w systemie Windows Server, który spełnia minimalne wymagania powitania serwera konfiguracji usługi Site Recovery hello czy ostatecznie musisz toodeploy jako jedną z pierwszych kroków hello w przypadku wdrożenia produkcyjnego.

Narzędzie Hello zapewnia hello poniższe informacje:

**Ocena zgodności**

* Ocena uprawnień maszyny wirtualnej na podstawie liczby dysków, rozmiaru dysku, liczby operacji we/wy na sekundę, współczynnika zmian i typu rozruchu (EFI/BIOS)
* Szacowany Hello przepustowość sieci, które są wymagane dla replikacji różnicowej

**Zapotrzebowanie na przepustowość sieci w porównaniu z oceną celu punktu odzyskiwania**

* Szacowany Hello przepustowość sieci, które są wymagane dla replikacji różnicowej
* Przepływność Hello, który Usługa Site Recovery można pobrać z lokalnego tooAzure
* Liczba Hello toobatch maszyn wirtualnych, oparte na powitania szacowany toocomplete przepustowości replikacji początkowej w określonym czasie

**Wymagania dotyczące infrastruktury platformy Azure**

* Witaj wymaga typu (konto magazynu standard lub premium) dla każdej maszyny Wirtualnej
* Całkowita liczba toobe konta magazynu standard i premium skonfigurowanej na potrzeby replikacji Hello
* Propozycje nazw kont magazynu oparte na wskazówkach usługi Azure Storage
* Witaj umieszczania konta magazynu dla wszystkich maszyn wirtualnych
* Liczba Hello Azure rdzeni toobe przed test trybu failover lub pracy awaryjnej na powitania subskrypcji
* Hello zalecane maszyny Wirtualnej Azure rozmiar dla każdego lokalnej maszyny Wirtualnej

**Wymagania dotyczące infrastruktury lokalnej**
* Witaj wymagane liczby serwerów konfiguracji i procesu toobe serwerów wdrożonych lokalnie

>[!IMPORTANT]
>
>Ponieważ obciążenie jest prawdopodobnie tooincrease wraz z upływem czasu, wszystkie hello poprzedniego narzędzia obliczenia są wykonywane przy założeniu współczynnik wzrostu 30 procent cech obciążenia i przy użyciu 95 wartość percentylu hello wszystkie metryki profilowania (churn — IOPS, odczytu/zapisu i dlatego określonymi). Oba te elementy (współczynnik wzrostu i obliczenie wartości percentyla) można konfigurować. toolearn więcej informacji o wskaźnik wzrostu zawiera sekcja "zagadnienia dotyczące współczynnik wzrostu" hello. toolearn więcej informacji na temat wartość percentylu w sekcji Witaj "Wartość percentylu używany do obliczania hello".
>

## <a name="requirements"></a>Wymagania
Narzędzie Hello ma dwa główne etapy: profilowania i generowanie raportów. Istnieje również trzecia opcja toocalculate przepustowości tylko. Hello wymagania dotyczące serwera hello, z których hello jest inicjowane profilowania i przepływność miary są prezentowane w hello w poniższej tabeli:

| Wymaganie dotyczące serwera | Opis|
|---|---|
|Profilowanie i pomiar przepływności| <ul><li>System operacyjny: Microsoft Windows Server 2012 R2<br>(co najmniej najlepiej pasujące hello [rozmiaru zalecenia dotyczące serwera konfiguracji hello](https://aka.ms/asr-v2a-on-prem-components))</li><li>Konfiguracja maszyny: 8 wirtualnych procesorów CPU, 16 GB pamięci RAM, dysk twardy o rozmiarze 300 GB</li><li>[Microsoft .NET Framework 4.5](https://aka.ms/dotnet-framework-45)</li><li>[VMware vSphere PowerCLI 6.0 R3](https://aka.ms/download_powercli)</li><li>[Pakiet Microsoft Visual C++ Redistributable dla programu Visual Studio 2012](https://aka.ms/vcplusplus-redistributable)</li><li>TooAzure dostęp do Internetu z tego serwera</li><li>Konto magazynu Azure</li><li>Dostęp administratora na powitania serwera</li><li>Minimalnie 100 GB wolnego miejsca na dysku (przy założeniu 1000 maszyn wirtualnych z średnio trzema dyskami na każdej z nich i profilowanych przez 30 dni)</li><li>VMware vCenter statystyki poziomu ustawień powinna być ustawiona, too2 lub wysokiego poziomu</li><li>Zezwalaj na porcie 443: funkcja automatycznego odzyskiwania systemu wdrożenia Planistę używa tego portu tooconnect toovCenter/hoście ESXi</ul></ul>|
| Generowanie raportu | Dowolny komputer z systemem Windows lub Windows Server i programem Microsoft Excel 2013 lub nowszym |
| Uprawnienia użytkowników | Uprawnienia tylko do odczytu dla konta użytkownika hello, który został użyty tooaccess hello VMware vCenter server/vSphere VMware ESXi host podczas profilowania |

> [!NOTE]
>
>Narzędzie Hello można profilu tylko maszyny wirtualne z dyskami VMDK i model RDM. Nie pozwala ono profilować maszyn wirtualnych z dyskami iSCSI ani NFS. Usługa Site Recovery obsługuje iSCSI i dysków systemu plików NFS serwerów VMware, ale ponieważ hello wdrożenia planistę nie znajduje się w hello gościa i jego profili tylko przy użyciu liczników wydajności vCenter, narzędzie hello nie ma wgląd w tych typów dysku.
>

## <a name="download-and-extract-hello-public-preview"></a>Pobierać i wyodrębniać hello publicznej wersji zapoznawczej
1. Pobieranie najnowszej wersji hello hello [publicznej wersji zapoznawczej usługi Site Recovery wdrożenia planistę](https://aka.ms/asr-deployment-planner).  
Narzędzie Hello jest spakowany w folderze pliku zip. Bieżąca wersja narzędzia hello Hello scenariuszu tylko hello VMware do platformy Azure.

2. Skopiuj z którego mają zostać toorun hello narzędzia hello .zip folderu toohello systemu Windows server.  
Jeśli na serwerze hello sieci dostępu tooconnect toohello vCenter server/ESXi hostem vSphere przechowujący toobe maszyn wirtualnych hello profilowane, można uruchomić narzędzie hello z systemu Windows Server 2012 R2. Jednak zaleca się uruchomienie narzędzia hello na serwerze, na których konfiguracja sprzętu spełnia hello [wskazówek dotyczących rozmiaru serwera konfiguracji](https://aka.ms/asr-v2a-on-prem-components). Jeśli wdrożono już usługi Site Recovery składniki lokalnie, należy uruchomić narzędzie hello z powitania serwera konfiguracji.

 Zaleca się, że masz hello tą samą konfiguracją sprzętową jako serwer konfiguracji hello, (mającej serwera przetwarzania w wbudowane) na serwerze hello, w którym należy uruchomić narzędzie hello. Taka konfiguracja zapewnia tego przepływności hello osiągnąć tego hello narzędzie raporty dopasowań hello rzeczywiste przepływność, którą Site Recovery można osiągnąć podczas replikacji. Obliczanie przepływności Hello zależy od dostępnej przepustowości sieci na powitania serwera i konfiguracji sprzętu (procesora CPU, pamięci masowej i tak dalej) powitania serwera. Po uruchomieniu narzędzia hello z innym serwerem przepływności hello jest obliczana na podstawie tego tooMicrosoft serwera Azure. Ponadto ponieważ konfiguracja sprzętu hello powitania serwera może się różnić od hello konfiguracji serwera, hello osiągnięte przepływność, którą hello narzędzie raporty mogą być niedokładne.

3. Wyodrębnij hello folderu zip.  
Hello folder zawiera wiele plików i podfolderów. plik wykonywalny Hello jest ASRDeploymentPlanner.exe w hello folderu nadrzędnego.

    Przykład:  
    Skopiuj tooE pliku zip hello: \ dysków i wyodrębnij go.
   E:\ASR Deployment Planner-Preview_v1.2.zip

    E:\ASR Deployment Planner-Preview_v1.2\ ASR Deployment Planner-Preview_v1.2\ ASRDeploymentPlanner.exe

## <a name="capabilities"></a>Możliwości
Narzędzie wiersza polecenia hello (ASRDeploymentPlanner.exe) można uruchomić w jednym z następujących trzech trybów hello:

1. Profilowanie  
2. Generowanie raportu
3. Uzyskiwanie informacji o przepływności

Najpierw należy uruchomić narzędzie hello profilowania postęp dokonany w trybie toogather wirtualna danych i IOPS. Następnie przeprowadź hello narzędzia toogenerate hello raport toofind hello przepustowości i magazynu wymagania dotyczące sieci.

## <a name="profiling"></a>Profilowanie
W trybie profilowania narzędzi planowania wdrożenia hello łączy toohello vCenter server/vSphere ESXi hosta toocollect danych dotyczących wydajności hello maszyny Wirtualnej.

* Profilowanie nie wpływa na wydajność hello produkcji hello maszyn wirtualnych, ponieważ nie połączenie bezpośrednie jest nawiązywane toothem. Wszystkie dane dotyczące wydajności są zbierane z hello vCenter server/ESXi hostem vSphere.
* tooensure, że istnieje niewielki wpływ na powitania serwera z powodu profilowania hello narzędzia kwerendy hello vCenter server/ESXi hostem vSphere co 15 minut. Ten interwał kwerendy obniżają dokładności profilowania, ponieważ narzędzie hello przechowuje dane licznika wydajności co minutę.

### <a name="create-a-list-of-vms-tooprofile"></a>Utwórz listę tooprofile maszyny wirtualne
Najpierw należy listę toobe maszyn wirtualnych hello profilowaniu. Wszystkie nazwy hello maszyn wirtualnych na hoście ESXi vCenter server/vSphere można uzyskać przy użyciu hello VMware vSphere PowerCLI poleceń w hello procedury. Alternatywnie można wyświetlić w pliku hello przyjaznych nazw lub adresów IP hello maszyn wirtualnych, które mają tooprofile ręcznie.

1. Zaloguj się toohello wirtualna tego VMware vSphere PowerCLI jest zainstalowana w.
2. Otwórz program hello VMware vSphere PowerCLI.
3. Upewnij się, że zasady wykonywania hello jest włączona obsługa hello skryptu. Jeśli jest ono wyłączone, uruchom hello VMware vSphere PowerCLI konsolę w trybie administratora, a następnie włącz ją, uruchamiając następujące polecenie hello:

            Set-ExecutionPolicy –ExecutionPolicy AllSigned

4. Możesz hello toorun optionly potrzeby następujące polecenia, jeżeli Connect VIServer nie został rozpoznany jako hello nazwę polecenia cmdlet.
 
            Add-PSSnapin VMware.VimAutomation.Core 

5. tooget nazwy hello wszystkich maszyn wirtualnych w programie vCenter server/vSphere ESXi hosta i przechowywania listy hello pliku txt, uruchom hello dwa polecenia wymienione w tym miejscu.
Zamień wartości &lsaquo;server name&rsaquo;, &lsaquo;user name&rsaquo;, &lsaquo;password&rsaquo; i &lsaquo;outputfile.txt&rsaquo; na własne wartości.

            Connect-VIServer -Server <server name> -User <user name> -Password <password>

            Get-VM |  Select Name | Sort-Object -Property Name >  <outputfile.txt>

6. Otwórz w Notatniku plik wyjściowy hello, a następnie skopiuj hello nazwy wszystkich maszyn wirtualnych, które mają tooprofile tooanother pliku (na przykład ProfileVMList.txt), co nazwa maszyny Wirtualnej w jednym wierszu. Ten plik jest używany jako wejściowych toohello *- VMListFile* parametru hello narzędzia wiersza polecenia.

    ![Lista nazw maszyn wirtualnych w hello wdrożenia planistę](./media/site-recovery-deployment-planner/profile-vm-list.png)

### <a name="start-profiling"></a>Rozpoczynanie profilowania
Po utworzeniu listy hello profilowane toobe maszyn wirtualnych, można uruchomić narzędzie hello w trybie profilowania. W tym miejscu jest lista hello obowiązkowe i opcjonalne parametry toorun narzędzie hello w trybie profilowania.

ASRDeploymentPlanner.exe -Operation StartProfiling /?

| Nazwa parametru | Opis |
|---|---|
| -Operation | StartProfiling |
| -Server | Witaj w pełni kwalifikowaną nazwę domeny lub adres IP hello vCenter server/ESXi hostem vSphere którego maszyny wirtualne są toobe profilowaniu.|
| -User | Witaj użytkownika nazwa tooconnect toohello vCenter server/ESXi hostem vSphere. Witaj, użytkownik musi toohave dostęp tylko do odczytu, co najmniej.|
| -VMListFile | Plik Hello, który zawiera listę hello profilowane toobe maszyn wirtualnych. Ścieżka pliku Hello może być bezwzględny lub względny. Witaj plik powinien zawierać jeden adres IP/Nazwa maszyny Wirtualnej w jednym wierszu. Nazwa maszyny wirtualnej określona w pliku hello powinien hello w taki sam jak nazwa maszyny Wirtualnej hello na powitania vCenter server/ESXi hostem vSphere.<br>Na przykład plik hello VMList.txt zawiera hello następujące maszyny wirtualne:<ul><li>maszyna_wirtualna_A</li><li>10.150.29.110</li><li>maszyna_wirtualna_B</li><ul> |
| -NoOfDaysToProfile | Uruchom Hello liczbę dni, dla których profilowania jest toobe. Zaleca się uruchamiania profilowania przez ponad 15 dni tooensure, który hello wzorzec obciążenia w danym środowisku za pośrednictwem hello określony okres zaobserwowano i używać tooprovide dokładne zalecenia. |
| -Directory | (Opcjonalnie) hello UNC universal naming convention () lub dane generowane podczas profilowania profilowania toostore ścieżkę katalogu lokalnego. Jeśli nie podano nazwę katalogu, o nazwie "ProfiledData" hello, ścieżka bieżącego katalogu hello będzie używany jako hello domyślny katalog. |
| -Password | (Opcjonalnie) hello hasło toouse tooconnect toohello vCenter server/ESXi hostem vSphere. Jeśli nie określisz teraz, pojawi się monit dla niego po wykonaniu polecenia hello.|
| -StorageAccountName | Nazwy konta magazynu hello (opcjonalnie), która jest używana toofind hello przepływności osiągalne do replikacji danych z lokalnego tooAzure. Narzędzie Hello przekazywania testu danych toothis konta toocalculate przepływności.|
| -StorageAccountKey | Klucz konta magazynu (opcjonalnie) hello używanego konta magazynu hello tooaccess. Przejdź toohello portalu Azure > kont magazynu ><*nazwy konta magazynu*>> Ustawienia > klucze dostępu > klucz1 (lub podstawowy klucz dostępu dla konta magazynu klasycznego). |
| -Environment | (Opcjonalnie) Jest to docelowe środowisko konta usługi Azure Storage. Ten parametr może przyjmować jedną z trzech wartości — AzureCloud, AzureUSGovernment i AzureChinaCloud. Wartością domyślną jest AzureCloud. Użyj parametru hello, gdy urządzenie docelowe region platformy Azure jest chmury Azure instytucji rządowych Stanów Zjednoczonych lub chińskiej wersji platformy Azure. |


Firma Microsoft zaleca profil maszyn wirtualnych dla co najmniej 15 dni too30. Podczas profilowania okres hello ASRDeploymentPlanner.exe kontynuowanie działania. Narzędzie Hello przyjmuje profilowania czasu danych wejściowych w dniach. Jeśli chcesz tooprofile przez kilka godzin lub minut szybkiego testu narzędzia hello w publicznej wersji zapoznawczej hello, konieczne będzie tooconvert hello czas na równoważne miary hello dni. Na przykład tooprofile przez 30 minut, hello dane wejściowe muszą być 30/(60*24) = 0.021 dni. Witaj minimalne dozwolone profilowania czasu wynosi 30 minut.

Podczas profilowania, nazwę konta magazynu i klucza toofind hello przepływność, którą Site Recovery można uzyskać w czasie hello replikacji z serwera konfiguracji hello lub proces serwera tooAzure można przekazać opcjonalnie. Jeśli hello nazwę konta magazynu i klucz nie zostaną przekazane podczas profilowania, narzędzie hello nie oblicza osiągalna przepływność.

Można uruchomić wiele wystąpień narzędzia powitania dla różnych zestawów maszyn wirtualnych. Upewnij się, że hello nazw maszyn wirtualnych nie są powtarzane w żadnym hello profilowania zestawów. Na przykład, jeśli mają profilowane dziesięć maszyn wirtualnych (VM1 za pośrednictwem VM10), a po upływie kilku dni ma tooprofile innego pięciu maszyn wirtualnych (VM11 za pośrednictwem VM15), można uruchomić narzędzie hello z innej konsoli wiersza polecenia dla hello drugi zestaw maszyn wirtualnych (VM11 za pośrednictwem VM15). Upewnij się, że hello drugi zestaw maszyn wirtualnych nie ma żadnych nazw maszyn wirtualnych z pierwszego wystąpienia profilowania hello lub użyć katalogu inny wynik dla hello drugi Uruchom. Jeśli dwa wystąpienia narzędzia hello są używane do profilowania hello tej samej maszyny wirtualne i użycie hello tego samego katalogu wyjściowego, hello wygenerowany raport będzie nieprawidłowa.

Konfiguracje maszyny Wirtualnej są przechwytywane raz na początku hello hello profilowanie operacji i przechowywane w pliku o nazwie VMDetailList.xml. Te informacje są używane podczas generowania raportu hello. Zmiany w konfiguracji maszyny Wirtualnej (na przykład zwiększonej liczby rdzeni, dyski lub kart sieciowych) z hello początku toohello zakończenia profilowania nie są przechwytywane. Jeśli PROFILOWANEGO konfiguracji maszyny Wirtualnej została zmieniona w trakcie hello profilowania w publicznej wersji zapoznawczej hello, w tym miejscu jest hello obejście tooget najnowsze maszyny Wirtualnej szczegóły podczas generowania raportu hello:

* Wykonaj kopię zapasową VMdetailList.xml i usunąć hello pliku z jego bieżącej lokalizacji.
* Argument jest przekazywany - i - hasło użytkownika w czasie generowania raportu hello.

Witaj profilowania polecenie generuje kilka plików w hello profilowania katalogu. Nie usuwaj żadnych plików hello, ponieważ wykonanie tej wpływa na sposób generowania raportów.

#### <a name="example-1-profile-vms-for-30-days-and-find-hello-throughput-from-on-premises-tooazure"></a>Przykład 1: Profil VMs 30 dni i Znajdź hello przepływności z lokalnymi tooAzure
```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  30  -User vCenterUser1 -StorageAccountName  asrspfarm1 -StorageAccountKey Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

#### <a name="example-2-profile-vms-for-15-days"></a>Przykład 2: profilowanie maszyn wirtualnych przez 15 dni

```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  15  -User vCenterUser1
```

#### <a name="example-3-profile-vms-for-1-hour-for-a-quick-test-of-hello-tool"></a>Przykład 3: Profil z maszyn wirtualnych 1 godziny szybkiego testu narzędzia hello
```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  0.04  -User vCenterUser1
```

>[!NOTE]
>
>* Jeśli serwer hello narzędzia hello jest uruchomiona na ponownego rozruchu lub wystąpiła awaria, lub Jeśli zamkniesz hello narzędzie przy użyciu klawiszy Ctrl + C, hello profilowane danych są zachowywane. Istnieje jednak prawdopodobieństwo Brak hello ostatnich 15 minut PROFILOWANEGO danych. W wystąpieniu należy ponownie uruchomić narzędzie hello w trybie profilowania po uruchomieniu powitania serwera.
>* Gdy hello nazwę konta magazynu i klucz są przekazywane, hello narzędzia środki hello przepływności w ostatnim kroku hello profilowania. Jeśli narzędzie hello jest zamknięta przed zakończeniem profilowania, hello przepływności nie jest obliczana. toofind hello przepływności przed wygenerowaniem hello raportu, można uruchomić operacji GetThroughput hello z wiersza polecenia konsoli hello. W przeciwnym razie hello wygenerowany raport nie będzie zawierać informacje o przepływności hello.


## <a name="generate-a-report"></a>Generowanie raportu
Narzędzie Hello generuje pliku programu Microsoft Excel z włączoną obsługą makr (plik XLSM) jako dane wyjściowe raportu hello, który znajduje się podsumowanie wszystkich hello zalecenia dotyczące wdrożenia. Raport Hello nosi nazwę DeploymentPlannerReport_ <*Unikatowy identyfikator liczbowy*> określić xlsm i hello umieszczonych w katalogu.

Po zakończeniu profilowania hello narzędzie można uruchomić w trybie generowania raportów. w poniższej tabeli Hello zawiera listę toorun parametry obowiązkowe i opcjonalne narzędzie w trybie generowania raportu.

`ASRDeploymentPlanner.exe -Operation GenerateReport /?`

|Nazwa parametru | Opis |
|-|-|
| -Operation | GenerateReport |
| -Server |  powitania serwera vCenter/vSphere w pełni kwalifikowana nazwa domeny lub adresu IP (Użyj hello sama nazwa lub adres IP, który jest używany w czasie hello profilowania) gdzie hello profilowane maszyn wirtualnych, których raport jest generowany toobe znajdują się. Należy pamiętać, że jeśli serwer vCenter jest używana w momencie hello profilowania, nie można użyć programu vSphere do generowania raportów i na odwrót.|
| -VMListFile | Witaj pliku, który zawiera listy hello PROFILOWANEGO maszyn wirtualnych, które hello raportu jest toobe wygenerowany dla. Ścieżka pliku Hello może być bezwzględny lub względny. Plik Hello powinien zawierać jedną nazwę maszyny Wirtualnej lub adres IP w każdym wierszu. Witaj nazw maszyn wirtualnych, które są określone w pliku hello powinien hello w taki sam jak hello nazw maszyn wirtualnych na powitania vCenter server/ESXi hostem vSphere i dopasowania, w której był używany podczas profilowania.|
| -Directory | (Opcjonalnie) hello UNC lub ścieżki katalogu lokalnego, w którym hello profilowane danych (pliki generowane podczas profilowania) są przechowywane. Te dane są wymagane do generowania raportów hello. Jeśli nie określisz nazwy, zostanie użyty katalog „ProfiledData”. |
| -GoalToCompleteIR | (Opcjonalnie) hello liczbę godzin, w których hello replikacji początkowej hello profilowane maszyn wirtualnych musi toobe ukończone. Witaj wygenerowany raport zawiera hello liczbę maszyn wirtualnych, dla których można ukończyć początkowej replikacji w hello określony czas. Domyślnie Hello jest 72 godzin. |
| -User | (Opcjonalnie) hello użytkownika toouse tooconnect toohello vCenter/vSphere serwer nazw. Nazwa Hello jest używany toofetch hello najnowsze informacje o konfiguracji hello maszyn wirtualnych, takie jak hello liczba dysków, liczby rdzeni i liczba kart sieciowych, toouse w raporcie hello. Jeśli nie podano nazwy hello, zebrane na początku hello hello profilowania kickoff informacje o konfiguracji hello jest używany. |
| -Password | (Opcjonalnie) hello hasło toouse tooconnect toohello vCenter server/ESXi hostem vSphere. Jeśli hasło hello nie jest określony jako parametru, pojawi się monit dla niego później podczas wykonywania polecenia hello. |
| -DesiredRPO | (Opcjonalnie) hello żądany cel punktu odzyskiwania, w minutach. Witaj domyślna to 15 minut.|
| -Bandwidth | Przepustowość w Mb/s. Witaj parametru toouse toocalculate Witaj cel punktu odzyskiwania, który może zostać osiągnięty dla hello określić przepustowość. |
| -StartDate | (Opcjonalnie) hello Data i godzina rozpoczęcia w formacie MM-DD-YYYY:HH:MM (w formacie 24-godzinnym). Oprócz parametru *StartDate* należy także określić parametr *EndDate*. Jeśli określona jest datą rozpoczęcia hello raport jest generowany dla hello profilowane dane zbierane między datą rozpoczęcia i datą zakończenia. |
| -EndDate | (Opcjonalnie) hello Data i godzina zakończenia w formacie MM-DD-YYYY:HH:MM (w formacie 24-godzinnym). Oprócz parametru *EndDate* należy także określić parametr *StartDate*. W przypadku EndDate hello raport jest generowany dla hello profilowane dane zbierane między datą rozpoczęcia i datą zakończenia. |
| -GrowthFactor | Współczynnik wzrostu hello (opcjonalnie), wyrażone jako procent. Witaj domyślna to 30 procent. |
| -UseManagedDisks | (Opcjonalnie) UseManagedDisks — Yes/No. Wartość domyślna to Yes. Liczba Hello maszyn wirtualnych, które można umieścić pod uwagę pojedynczy magazyn jest obliczana biorąc pod uwagę, czy trybu Failover i testowania pracy w trybie failover maszyny wirtualnej jest wykonywana na dysków zarządzanych zamiast niezarządzane dysku. |

#### <a name="example-1-generate-a-report-with-default-values-when-hello-profiled-data-is-on-hello-local-drive"></a>Przykład 1: Generowanie raportu z wartościami domyślnymi, gdy hello profilowane danych znajduje się na dysku lokalnym hello
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “\\PS1-W2K12R2\vCenter1_ProfiledData” -VMListFile “\\PS1-W2K12R2\vCenter1_ProfiledData\ProfileVMList1.txt”
```

#### <a name="example-2-generate-a-report-when-hello-profiled-data-is-on-a-remote-server"></a>Przykład 2: Generowanie raportu po hello profilowane danych na serwerze zdalnym
Powinien mieć dostęp do odczytu/zapisu na powitania katalog zdalny.
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “\\PS1-W2K12R2\vCenter1_ProfiledData” -VMListFile “\\PS1-W2K12R2\vCenter1_ProfiledData\ProfileVMList1.txt”
```

#### <a name="example-3-generate-a-report-with-a-specific-bandwidth-and-goal-toocomplete-ir-within-specified-time"></a>Przykład 3: Generowanie raportu z określonym przepustowość i celem toocomplete IR w określonym czasie
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -Bandwidth 100 -GoalToCompleteIR 24
```

#### <a name="example-4-generate-a-report-with-a-5-percent-growth-factor-instead-of-hello-default-30-percent"></a>Przykład 4: Generowanie raportu współczynnik wzrostu 5 procent zamiast hello domyślne 30 procent
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -GrowthFactor 5
```

#### <a name="example-5-generate-a-report-with-a-subset-of-profiled-data"></a>Przykład 5: generowanie raportu przy użyciu podzestawu profilowanych danych
Na przykład w ciągu 30 dni danych profilowanych i mają toogenerate raportu tylko 20 dni.
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -StartDate  01-10-2017:12:30 -EndDate 01-19-2017:12:30
```

#### <a name="example-6-generate-a-report-for-5-minute-rpo"></a>Przykład 6: generowanie raportu w przypadku 5-minutowego celu punktu odzyskiwania
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -DesiredRPO 5
```

## <a name="percentile-value-used-for-hello-calculation"></a>Wartość percentylu używany do obliczania hello
**Jakie domyślna wartość percentylu hello metryki wydajności zebrane podczas profilowania ma hello narzędzia do użycia podczas generowania raportu?**

Hello narzędzia domyślne toohello 95. percentyl wartości odczytu/zapisu IOPS, zapisać IOPS i tworzeniem danych, które są zbierane podczas profilowania wszystkich hello maszyn wirtualnych. Ta metryka zapewnia kolekcji percentyl 100 tego hello napotkać maszyn wirtualnych ze względu na tymczasowy zdarzenia jest docelowy wymagania konto magazynu i przepustowości źródła toodetermine nie jest używany. Zdarzenie tymczasowe to na przykład uruchamiane raz dziennie zadanie tworzenia kopii zapasowej, działanie polegające na okresowym indeksowaniu bazy danych lub generowaniu raportu analitycznego albo inne podobne, krótkotrwałe zdarzenia występujące w danym momencie czasowym.

Przy użyciu 95. percentyl wartości oferuje prawdziwy obraz właściwości rzeczywiste obciążenie który umożliwia hello najlepszą wydajność uruchomionej hello obciążeń na platformie Azure. Nie przewidujemy, że będzie potrzebny toochange ten numer. W przypadku zmiany wartości hello (toohello 90-procentowy, na przykład), można zaktualizować pliku konfiguracji hello *ASRDeploymentPlanner.exe.config* w hello domyślny folder i zapisać ją toogenerate nowego raportu na powitania istniejącej profilowaniu dane.
```
<add key="WriteIOPSPercentile" value="95" />      
<add key="ReadWriteIOPSPercentile" value="95" />      
<add key="DataChurnPercentile" value="95" />
```

## <a name="growth-factor-considerations"></a>Zagadnienia związane ze współczynnikiem wzrostu
**Dlaczego podczas planowania wdrożenia warto wziąć pod uwagę współczynnik wzrostu?**

Jest krytyczne tooaccount na wzrost cech obciążenia przy założeniu możliwy wzrost użycia wraz z upływem czasu. Po ochrony znajduje się w miejscu, zmiana właściwości Twoje obciążenie, nie można przełączyć bez wyłączenie i ponowne włączenie ochrony hello tooa innego konta magazynu do ochrony.

Załóżmy na przykład, że dzisiaj maszyna wirtualna mieści się na standardowym koncie replikacji magazynu. Witaj trzy kolejne miesiące kilka zmian są prawdopodobnie toooccur:

* zwiększy Hello liczby użytkowników hello aplikację, która działa na powitania maszyny Wirtualnej.
* Wynikowa przenoszenie zwiększona Hello na powitania maszyny Wirtualnej wymaga hello wirtualna toogo toopremium magazynu, dzięki czemu można bieżąco replikacji usługi Site Recovery.
* W rezultacie będzie mieć toodisable i ponownie włączyć konto magazynu premium tooa ochrony.

Zdecydowanie zaleca się zaplanowanie wzrostu podczas planowania wdrożenia i gdy hello wartość domyślna to 30 procent. Ekspert hello znajdują się na projekcje Twojej aplikacji w sposób użycia wzorca i wzrost i tę liczbę można zmienić odpowiednio podczas generowania raportu. Ponadto możesz generować raporty, wiele z różnych czynników wzrostu z hello sam profilowane danych i ustalić, jakie zalecenia przepustowości docelowym, jak magazyn i źródła Najlepsza.

Raport programu Excel Hello wygenerowany zawiera hello następujących informacji:

* [Dane wejściowe](site-recovery-deployment-planner.md#input)
* [Zalecenia](site-recovery-deployment-planner.md#recommendations-with-desired-rpo-as-input)
* [Zalecenia — dane wejściowe przepustowości](site-recovery-deployment-planner.md#recommendations-with-available-bandwidth-as-input)
* [Rozmieszczenie maszyny wirtualnej względem magazynu](site-recovery-deployment-planner.md#vm-storage-placement)
* [Zgodne maszyny wirtualne](site-recovery-deployment-planner.md#compatible-vms)
* [Niezgodne maszyny wirtualne](site-recovery-deployment-planner.md#incompatible-vms)

![Planista wdrożenia](./media/site-recovery-deployment-planner/dp-report.png)

## <a name="get-throughput"></a>Uzyskiwanie informacji o przepływności

Przepływność hello tooestimate usługi Site Recovery można uzyskać z lokalnymi tooAzure podczas replikacji, uruchom narzędzie hello w trybie GetThroughput. Narzędzie Hello oblicza się, że przepływność hello z serwera hello hello narzędzie działa. Najlepiej, jeśli ten serwer jest oparta na powitania serwera zmiany rozmiaru w podręczniku konfiguracji. Jeśli usługi Site Recovery składniki lokalnej infrastruktury zostały już wdrożone, należy uruchomić narzędzie hello na powitania serwera konfiguracji.

Otwórz konsolę wiersza polecenia i przejdź do folderu Narzędzia do planowania wdrażania usługi Site Recovery toohello. Uruchom program ASRDeploymentPlanner.exe z poniższymi parametrami.

`ASRDeploymentPlanner.exe -Operation GetThroughput /?`

|Nazwa parametru | Opis |
|-|-|
| -Operation | GetThroughput |
| -Directory | (Opcjonalnie) hello UNC lub ścieżki katalogu lokalnego, w którym hello profilowane danych (pliki generowane podczas profilowania) są przechowywane. Te dane są wymagane do generowania raportów hello. Jeśli nie określono nazwy katalogu, jest używany katalog „ProfiledData”. |
| -StorageAccountName | Nazwa konta magazynu Hello został użyty hello przepustowości toofind do replikacji danych z lokalnego tooAzure. Witaj narzędzie przekazywania testu danych toothis magazynu konta toofind hello przepustowości. |
| -StorageAccountKey | klucz konta magazynu Hello, który został użyty konta magazynu hello tooaccess. Przejdź toohello portalu Azure > kont magazynu ><*nazwy konta magazynu*>> Ustawienia > klucze dostępu > klucz1 (lub podstawowy klucz dostępu dla konta magazynu klasycznego). |
| -VMListFile | Plik Hello, który zawiera listę hello profilowane dla obliczania hello przepustowości toobe maszyn wirtualnych. Ścieżka pliku Hello może być bezwzględny lub względny. Witaj plik powinien zawierać jeden adres IP/Nazwa maszyny Wirtualnej w jednym wierszu. nazwy maszyny Wirtualnej Hello określone w pliku hello powinien hello w taki sam jak hello nazw maszyn wirtualnych na powitania vCenter server/ESXi hostem vSphere.<br>Na przykład plik hello VMList.txt zawiera hello następujące maszyny wirtualne:<ul><li>VM_A</li><li>10.150.29.110</li><li>VM_B</li></ul>|
| -Environment | (Opcjonalnie) Jest to docelowe środowisko konta usługi Azure Storage. Ten parametr może przyjmować jedną z trzech wartości — AzureCloud, AzureUSGovernment i AzureChinaCloud. Wartością domyślną jest AzureCloud. Użyj parametru hello, gdy urządzenie docelowe region platformy Azure jest chmury Azure instytucji rządowych Stanów Zjednoczonych lub chińskiej wersji platformy Azure. |

Narzędzie Hello tworzy kilka asrvhdfile 64 MB VHD # <> plików (gdzie "#" jest hello liczbę plików) na powitania określonego katalogu. Narzędzie Hello przekazuje hello pliki toohello konta toofind hello przepływności. Po przepływność hello jest mierzona, narzędzie hello usuwa wszystkie pliki hello z konta magazynu hello i powitania serwera lokalnego. Narzędzie hello jest przerwane przyczyn jest obliczenie przepływności, nie powoduje usunięcia hello pliki z magazynu hello lub powitania serwera lokalnego. Toodelete, należy je ręcznie.

Witaj przepływności jest mierzony w określonym punkcie w czasie i jest hello maksymalną przepływność, którą można osiągnąć usługi Site Recovery, podczas replikacji, pod warunkiem że będą inne czynniki hello takie same. Na przykład, jeśli zaczyna żadnej aplikacji korzystanie z większej przepustowości w tej samej sieci, przepływności rzeczywiste hello zmienia się podczas replikacji powitalne. Hello polecenia GetThroughput korzystający z konfiguracji serwera, narzędzia hello nie rozpoznaje żadnych chronionych maszyn wirtualnych i trwającej replikacji. Hello wynik przepływność mierzoną hello jest inny, jeśli hello GetThroughput operacji jest uruchamiany, gdy hello chronione maszyny wirtualne mają wysokie danych churn —. Zaleca się uruchomienie hello narzędzia w różnych punktach w czasie podczas profilowania toounderstand przepływności, jakie można osiągnąć poziomy w różnym czasie. W raporcie hello hello narzędzie wyświetla hello ostatniego zmierzona przepustowość.

### <a name="example"></a>Przykład
```
ASRDeploymentPlanner.exe -Operation GetThroughput -Directory  E:\vCenter1_ProfiledData -VMListFile E:\vCenter1_ProfiledData\ProfileVMList1.txt  -StorageAccountName  asrspfarm1 -StorageAccountKey by8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

>[!NOTE]
>
> Uruchom narzędzie hello na serwerze, który ma hello tego samego magazynu i procesora CPU właściwości powitania serwera konfiguracji.
>
> W przypadku replikacji hello zestaw zalecane przepustowości toomeet hello RPO 100 procent czasu hello. Po ustawieniu przepustowości prawo hello, jeśli nie widzisz podnieść przepustowość hello osiągnięte zgłoszone przez narzędzie hello hello następujące:
>
>  1. Toodetermine należy sprawdzić, czy istnieje żadnej sieci jakości usług (QoS), który jest ograniczanie przepływności usługi Site Recovery.
>
>  2. Toodetermine należy sprawdzić, czy magazyn usługi Site Recovery jest hello najbliższej fizycznie obsługiwanych opóźnienia sieci toominimize region Microsoft Azure.
>
>  3. Toodetermine właściwości z lokalnego magazynu należy sprawdzić, czy można zwiększyć hello sprzętu (na przykład dysk twardy tooSSD).
>
>  4. Zmienianie ustawień usługi Site Recovery hello w serwera przetwarzania hello zbyt[zwiększyć ilość hello przepustowości sieci używanej w ramach replikacji](./site-recovery-plan-capacity-vmware.md#control-network-bandwidth).

## <a name="recommendations-with-desired-rpo-as-input"></a>Zalecenia dotyczące danych wejściowych w postaci żądanego celu punktu odzyskiwania

### <a name="profiled-data"></a>Profilowane dane

![Widok danych profilowane Hello hello wdrożenia planistę](./media/site-recovery-deployment-planner/profiled-data-period.png)

**Okres danych profilowanych**: hello okres, podczas którego hello profilowanie zostało uruchomione. Domyślnie narzędzie hello obejmuje wszystkie dane PROFILOWANEGO obliczania hello, chyba że generuje raport hello w danym okresie, używając opcji datą rozpoczęcia i datą zakończenia podczas generowania raportu.

**Nazwa serwera**: hello nazwę lub adres IP hello VMware vCenter lub hosta ESXi jest generowany raport którego maszyn wirtualnych.

**Żądany cel punktu odzyskiwania**: hello cel punktu odzyskiwania dla danego wdrożenia. Domyślnie program hello wymagana przepustowość sieci jest obliczana dla wartości RPO 15, 30 i 60 minut. Na podstawie hello zaznaczenia, wartości hello, których to dotyczy zostaną zaktualizowane na powitania arkusza. Jeśli używasz hello *DesiredRPOinMin* parametr podczas generowania raportu hello, wartości podane w hello wynik żądany cel punktu odzyskiwania.

### <a name="profiling-overview"></a>Omówienie profilowania

![Profilowanie powoduje hello wdrożenia planistę](./media/site-recovery-deployment-planner/profiling-overview.png)

**Łączna liczba maszyn wirtualnych profilowane**: hello całkowitą liczbę maszyn wirtualnych, których PROFILOWANEGO dane są dostępne. Jeśli hello VMListFile ma nazw żadnych maszyn wirtualnych, które nie zostały profilowane, te maszyny wirtualne nie są wliczane hello generowania raportu i są wykluczone z liczby całkowitej maszyn wirtualnych PROFILOWANEGO hello.

**Maszyny wirtualne zgodne**: hello liczbę maszyn wirtualnych, które mogą być chronione tooAzure przy użyciu usługi Site Recovery. Jest hello całkowitą liczbę zgodne maszyn wirtualnych, dla których hello są obliczane wymagana przepustowość sieci, liczba kont magazynu, liczba rdzeni Azure i liczby serwerów konfiguracji oraz dodatkowych procesów serwerów. Szczegóły Hello co zgodne maszyny wirtualnej są dostępne w sekcji "Zgodny maszyn wirtualnych" hello.

**Maszyny wirtualne niezgodne**: hello liczbę profilowanych maszyn wirtualnych, które są niezgodne dla ochrony z usługą Site Recovery. powód niezgodności Hello są wymienione w sekcji "Niezgodny maszyn wirtualnych" hello. Jeśli hello VMListFile ma nazw żadnych maszyn wirtualnych, które nie zostały profilowane, te maszyny wirtualne są wykluczone z hello niezgodne liczby maszyn wirtualnych. Te maszyny wirtualne są wyświetlane jako "Nie można odnaleźć danych" na końcu sekcji hello "niezgodny maszyn wirtualnych" hello.

**Żądany cel punktu odzyskiwania**: żądany cel punktu odzyskiwania w minutach. Witaj raport jest generowany dla trzech wartości RPO: 15 (ustawienie domyślne), 30 i 60 minut. zalecenie przepustowości Hello w raporcie hello jest zmieniony w zależności od wybraną z listy hello rozwijanej żądany cel punktu odzyskiwania w prawym górnym hello hello arkusza. Jeśli raport hello zostały wygenerowane za pomocą hello *- DesiredRPO* parametr przy użyciu niestandardowej wartości, to Niestandardowa wartość będą widoczne jako domyślny hello liście hello rozwijanej żądany cel punktu odzyskiwania.

### <a name="required-network-bandwidth-mbps"></a>Wymagana przepustowość sieci (Mb/s)

![Przepustowość wymagana sieć w hello wdrożenia planistę](./media/site-recovery-deployment-planner/required-network-bandwidth.png)

**toomeet RPO 100 procent czasu hello:** hello zalecane przepustowości w MB/s toobe przydzielone toomeet Twojego żądany cel punktu odzyskiwania 100 procent czasu hello. Ta ilość przepustowości, musi być dedykowany replikacji różnicowej stabilnego wszystkie zgodne tooavoid maszyn wirtualnych naruszenie cel punktu odzyskiwania.

**toomeet RPO 90 procent czasu hello**: z powodu cennik połączenia szerokopasmowego lub z innego powodu, jeśli nie można ustawić hello przepustowości potrzebne toomeet Twojego żądany cel punktu odzyskiwania 100 procent czasu hello można wypełnić toogo o mniejszej przepustowości sieci, ustawienia użytkownika żądany cel punktu odzyskiwania 90 procent czasu hello. skutki hello toounderstand ustawienia tej mniejszej przepustowości sieci, hello raport zawiera analizy warunkowej na powitania liczby i czasu trwania tooexpect naruszeń cel punktu odzyskiwania.

**Przepływność osiągnięte:** przepływności hello z hello serwera, na którym uruchomiono hello GetThroughput polecenia toohello Microsoft Azure region, gdzie znajduje się hello konta magazynu. Liczba przepływności wskazuje poziom hello szacowany, który można uzyskać w przypadku ochrony powitalne hello zgodne maszyn wirtualnych przy użyciu usługi Site Recovery, pod warunkiem, że serwer konfiguracji lub właściwości serwera procesów magazynu i sieci pozostają takie same jak Serwer Hello, z którego uruchomiono narzędzie hello.

W przypadku replikacji należy ustawić hello zalecane przepustowości toomeet hello RPO 100 procent czasu hello. Po ustawieniu przepustowości hello, jeśli widzisz zwiększenia przepływności hello osiągnięte zgłoszonej przez narzędzie hello, wykonaj następujące hello:

1. Toosee należy sprawdzić, czy istnieje żadnej sieci jakości usług (QoS), który jest ograniczanie przepływności usługi Site Recovery.

2. Toosee należy sprawdzić, czy magazyn usługi Site Recovery jest hello najbliższej fizycznie obsługiwanych opóźnienia sieci toominimize region Microsoft Azure.

3. Toodetermine właściwości z lokalnego magazynu należy sprawdzić, czy można zwiększyć hello sprzętu (na przykład dysk twardy tooSSD).

4. Zmienianie ustawień usługi Site Recovery hello w serwera przetwarzania hello zbyt[zwiększyć hello ilość przepustowości używanej w ramach replikacji](./site-recovery-plan-capacity-vmware.md#control-network-bandwidth).

Jeśli używasz narzędzia hello na serwerze konfiguracji lub serwer przetwarzania, który już zawiera chronione maszyny wirtualne, należy uruchomić narzędzie hello kilka razy. Witaj osiągnąć przepływności zmiany w zależności od hello ilość danych churn przetwarzane w danym momencie.

W przypadku wszystkich wdrożeń usługi Site Recovery w przedsiębiorstwach zalecamy użycie usługi [ExpressRoute](https://aka.ms/expressroute).

### <a name="required-storage-accounts"></a>Wymagane konta magazynu
powitania po wykresu pokazuje kont hello łączna liczba magazynu (warstwy standardowa i premium), które są wszystkie wymagane tooprotect hello zgodne maszyn wirtualnych. toolearn składowania konta toouse dla każdej maszyny Wirtualnej, zobacz sekcję "umieszczania magazynu maszyny Wirtualnej" hello.

![Kont magazynu wymagana w hello wdrożenia planistę](./media/site-recovery-deployment-planner/required-azure-storage-accounts.png)

### <a name="required-number-of-azure-cores"></a>Wymagana liczba rdzeni platformy Azure
Ten wynik jest hello całkowita liczba rdzeni toobe ustawień przed rozpoczęciem pracy awaryjnej lub test pracy awaryjnej wszystkich hello zgodne maszyn wirtualnych. Jeśli rdzeni za mało dostępnych w subskrypcji hello, odzyskiwania lokacji nie powiedzie się toocreate maszyn wirtualnych w momencie hello testowania trybu failover lub pracy awaryjnej.

![Wymagana liczba rdzeni Azure hello wdrożenia planistę](./media/site-recovery-deployment-planner/required-number-of-azure-cores.png)

### <a name="required-on-premises-infrastructure"></a>Wymagana infrastruktura lokalna
Liczba ta jest hello całkowita liczba serwerów konfiguracji oraz dodatkowych procesów toobe serwery skonfigurowane, które będą wystarczające tooprotect hello wszystkie zgodne maszyn wirtualnych. W zależności od hello obsługiwane [rozmiaru zalecenia dotyczące serwera konfiguracji hello](https://aka.ms/asr-v2a-on-prem-components), narzędzie hello może zalecić dodatkowych serwerów. zalecenie Hello jest oparta na powitania większych hello postęp dokonany w ciągu jednego dnia lub hello maksymalna liczba chronionych maszyn wirtualnych (przy założeniu średnią z trzech dysków dla maszyny Wirtualnej), nastąpi trafienie pierwszy na serwerze konfiguracji hello lub hello dodatkowych procesów. Szczegóły hello łącznej wielkości fragmentów dziennie oraz liczba chronionych dysków można znaleźć w sekcji "Dane wejściowe" hello.

![Infrastruktura lokalna wymagane w hello wdrożenia planistę](./media/site-recovery-deployment-planner/required-on-premises-infrastructure.png)

### <a name="what-if-analysis"></a>Analiza warunkowa
Analiza przedstawia liczbę naruszeń mogłyby wystąpić w trakcie hello profilowania podczas ustawiania okresu mniejszej przepustowości sieci dla toobe RPO hello potrzeby spełnienia tylko 90 procent czasu hello. W danym dniu może wystąpić co najmniej jedno naruszenie. Witaj wykres przedstawia szczytu hello RPO hello dnia.
Oparte na tej analizy, można zdecydować, czy hello liczba naruszeń cel punktu odzyskiwania we wszystkich dni i szczytowego RPO trafień na dzień jest akceptowalne z hello określonym mniejszej przepustowości sieci. W przypadku przyjęcia, możesz przydzielić hello mniejszej przepustowości replikacji else przydzielić hello większej przepustowości, ponieważ hello sugerowane toomeet żądany cel punktu odzyskiwania 100 procent czasu hello.

![Analizy warunkowej w hello wdrożenia planistę](./media/site-recovery-deployment-planner/what-if-analysis.png)

### <a name="recommended-vm-batch-size-for-initial-replication"></a>Zalecany rozmiar partii maszyn wirtualnych na potrzeby replikacji początkowej
W tej sekcji zaleca się, że hello liczbę maszyn wirtualnych, które mogą być chronione w równoległych toocomplete hello początkowej replikacji w ramach 72 godziny z hello sugerowane się, że przepustowość toomeet żądany cel punktu odzyskiwania 100 procent wyznaczonym hello. Tę wartość można konfigurować. toochange go w czasie generowania raportu, użyj hello *GoalToCompleteIR* parametru.

Hello tutaj wykres przedstawia zakres wartości przepustowości i obliczeniowego maszyny Wirtualnej partii rozmiar liczba toocomplete replikacji początkowej w 72 godziny, na podstawie średniej hello wykryto maszyny Wirtualnej rozmiar we wszystkich hello zgodne maszyn wirtualnych.

W publicznej wersji zapoznawczej hello hello raportu nie określa, które maszyn wirtualnych powinny być uwzględnione w partii. Można użyć rozmiar dysku hello pokazano hello "zgodny maszyn wirtualnych" części toofind rozmiar każdej maszyny Wirtualnej i zaznacz je w partii, lub wybrać hello maszyn wirtualnych na podstawie obciążenia znanych charakterystyk. czas ukończenia Hello zmian replikacji początkowej hello proporcjonalnie, oparte na powitania rzeczywisty rozmiar dysku maszyny Wirtualnej, używane miejsce na dysku i przepustowości dostępnej sieci.

![Zalecany rozmiar partii zadań maszyny wirtualnej](./media/site-recovery-deployment-planner/recommended-vm-batch-size.png)

### <a name="growth-factor-and-percentile-values-used"></a>Używane wartości współczynnika wzrostu i percentyla
W tej sekcji u dołu hello hello arkusza wartość percentylu hello pokazuje używane dla wszystkich liczników wydajności hello hello profilowane maszyn wirtualnych (wartość domyślna to 95. percentyl), a współczynnik wzrostu hello (wartość domyślna to 30 procent) używany w obliczeniach hello wszystkie.

![Używane wartości współczynnika wzrostu i percentyla](./media/site-recovery-deployment-planner/max-iops-and-data-churn-setting.png)

## <a name="recommendations-with-available-bandwidth-as-input"></a>Zalecenia dotyczące danych wejściowych w postaci dostępnej przepustowości

![Zalecenia dotyczące danych wejściowych w postaci dostępnej przepustowości](./media/site-recovery-deployment-planner/profiling-overview-bandwidth-input.png)

Może wystąpić sytuacja, w której nie można ustawić przepustowości większej niż x Mb/s na potrzeby replikacji usługi Site Recovery. Narzędzie Hello umożliwia tooinput dostępną przepustowość (przy użyciu hello — parametr przepustowości podczas generowania raportu) i get hello osiągalne cel punktu odzyskiwania w minutach. Z tym osiągalne wartość RPO można zdecydować, czy należy tooset się dodatkowe ograniczenie użycia przepustowości lub są OK z konieczności rozwiązanie odzyskiwania po awarii, ten cel punktu odzyskiwania.

![Osiągalny cel punktu odzyskiwania dla przepustowości wynoszącej 500 Mb/s](./media/site-recovery-deployment-planner/achievable-rpos.png)

## <a name="input"></a>Dane wejściowe
Arkusz danych wejściowych Hello zawiera omówienie hello profilowane środowisku VMware.

![Omówienie hello profilowane środowiska VMware](./media/site-recovery-deployment-planner/Input.png)

**Data rozpoczęcia** i **Data zakończenia**: hello daty rozpoczęcia i zakończenia hello brany pod uwagę podczas generowania raportu danych profilowania. Domyślnie, Data rozpoczęcia hello jest data hello podczas profilowania uruchamiania i Data zakończenia hello jest data hello momentu zatrzymania profilowania. Może to być wartości "EndDate" i "Data_rozpoczęcia" hello, jeśli hello raport jest generowany z tych parametrów.

**Liczba dni profilowania**: hello całkowitej liczby dni profilowania między hello daty rozpoczęcia i zakończenia dla których hello jest generowany raport.

**Liczba maszyn wirtualnych zgodne**: hello łączna liczba zgodne maszyn wirtualnych, dla których hello wymagana przepustowość sieci, wymaganej liczby magazynu kont, rdzeni Microsoft Azure, serwery konfiguracji oraz dodatkowych procesów serwery są obliczone.

**Całkowita liczba dysków dla wszystkich maszyn wirtualnych zgodne**: hello liczba, która jest używana jako jeden hello danych wejściowych toodecide hello liczby serwerów konfiguracji oraz dodatkowych procesów toobe serwerów używanych we wdrożeniu hello.

**Średnia liczba dysków na kompatybilnej maszynie wirtualnej**: hello średnią liczbę dysków obliczane na wszystkich maszynach wirtualnych zgodne.

**Średni rozmiar dysku (GB)**: hello przeciętna ilość obliczyć na wszystkich maszynach wirtualnych zgodne.

**Żądany cel punktu odzyskiwania (w minutach)**: albo hello domyślną wartość punktu odzyskiwania cel lub hello przekazana dla parametru "DesiredRPO" hello w momencie hello tooestimate generowania raportu wymagane przepustowości.

**Wymaganą przepustowość (MB/s)**: hello wartość przekazanego do parametru "Przepustowości" hello w momencie hello tooestimate generowania raportu osiągalne cel punktu odzyskiwania.

**Przenoszenie obserwowanych typowych danych dziennie (GB)**: przenoszenie uśrednianie danych hello zaobserwowane we wszystkich profilowania dni. Numer ten jest używany jako jeden hello wejść toodecide hello liczba konfiguracji serwerów i toobe serwery dodatkowych procesów używanych we wdrożeniu hello.


## <a name="vm-storage-placement"></a>Rozmieszczenie maszyny wirtualnej względem magazynu

![Rozmieszczenie maszyny wirtualnej względem magazynu](./media/site-recovery-deployment-planner/vm-storage-placement.png)

**Typ magazynu dysku**: albo standard lub premium konta magazynu, który jest używany tooreplicate wszystkie hello VMs odpowiedniej wspomnianego hello **tooPlace maszyn wirtualnych** kolumny.

**Sugerowana prefiks**: hello sugerowane trzy znaki prefiks, który może służyć do nazw hello konta magazynu. Można użyć własnych prefiksu, ale narzędzie hello sugestię następuje hello [partycji konwencję nazewnictwa dla kont magazynu](https://aka.ms/storage-performance-checklist).

**Sugerowana nazwa konta**: Nazwa konta magazynu hello po umieszczeniu hello sugerowane prefiks. Zamień nazwę hello w hello nawiasu ostrego (< i >) z niestandardowe dane wejściowe.

**Konto magazynu dziennika**: wszystkie dzienniki replikacji hello są przechowywane na koncie magazynu w warstwie standardowa. Dla maszyn wirtualnych, które są replikowane tooa konta magazynu w warstwie premium, skonfiguruj dodatkowe konto magazynu do przechowywania dziennika. Jedno konto magazynu dzienników w warstwie Standardowa może być używane przez wiele kont magazynu replikacji w warstwie Premium. Maszyny wirtualne, które są replikowane toostandard magazynu kont hello tego samego konta magazynu dla dzienników.

**Sugerowana nazwa konta dziennika**: Nazwa konta dziennika magazynu po umieszczeniu hello sugerowane prefiks. Zamień nazwę hello w hello nawiasu ostrego (< i >) z niestandardowe dane wejściowe.

**Podsumowanie umieszczania**: Podsumowanie hello całkowity obciążenia maszyn wirtualnych na koncie magazynu hello w czasie hello replikacji i testowania trybu failover lub pracy awaryjnej. Obejmuje on hello łączna liczba maszyn wirtualnych zamapowanych toohello konta magazynu, całkowita odczytu/zapisu zapisu IOPS na wszystkich maszynach wirtualnych, które znajdują się na tym koncie magazynu, całkowita (replikacja) IOPS, rozmiar całkowitą instalacji dla wszystkich dysków i całkowitej liczby dysków.

**Maszyny wirtualne tooPlace**: lista wszystkich hello maszyn wirtualnych, które powinny być umieszczane na powitania podane konto magazynu dla uzyskania optymalnej wydajności i użycia.

## <a name="compatible-vms"></a>Zgodne maszyny wirtualne
![Arkusz kalkulacyjny programu Excel zawierający zgodne maszyny wirtualne](./media/site-recovery-deployment-planner/compatible-vms.png)

**Nazwa maszyny Wirtualnej**: hello nazwę maszyny Wirtualnej lub adres IP, który jest używany w hello VMListFile po wygenerowaniu raportu. Ta kolumna zawiera także dysków hello (VMDKs), które są dołączone toohello maszyn wirtualnych. toodistinguish vCenter maszyny wirtualne z zduplikowanych nazw lub adresów IP, nazwy hello zawierają nazwę hosta ESXi hello. Hello wymienionych hosta ESXi jest hello jedną hello maszyna wirtualna została rozmieszczenia gdy narzędzie hello wykryte podczas hello profilowania okresu.

**Zgodność maszyny wirtualnej**: wartości to **Tak** i **Tak**\*. **Tak** \* dla wystąpień, w których hello maszyna wirtualna jest rozwiązaniem dla [Azure Premium Storage](https://aka.ms/premium-storage-workload). W tym miejscu hello profilowane wysokiej zmian lub dysku IOPS mieści się w kategorii P30 lub hello P20, ale hello rozmiar dysku hello powoduje toobe mapować w dół tooa P10 lub P20. Konto magazynu Hello decyduje, który dysk magazynu premium wpisz toomap dysku, na podstawie jego rozmiaru. Na przykład:
* Mniej niż 128 GB — P10.
* 128 GB too512 GB jest P20.
* 512 GB too1024 GB jest P30.
* 1025 GB too2048 GB jest P40.
* 2049 GB too4095 GB jest P50.

Jeśli cechy obciążenia hello dysku umieść ją w hello P20 lub P30 kategorii, ale rozmiar hello mapuje go w dół typ dysku magazynu premium tooa niższe, narzędzie hello oznacza tej maszyny Wirtualnej jako **tak**\*. Narzędzie Hello zaleca również, że albo toofit rozmiar dysku źródłowego hello na powitania zalecane typ dysku magazynu premium lub zmiana hello docelowego dysku typu po pracy w trybie failover.

**Typ magazynu**: dostępne typy magazynu to Standardowa i Premium.

**Sugerowana prefiks**: hello konta magazynu trzy znaki prefiksu.

**Konto magazynu**: hello nazwę, która używa hello prefiksu sugerowane konta magazynu.

**IOPS odczyt/zapis (o wskaźnik wzrostu)**: hello szczytowego obciążenia odczytu/zapisu IOPS na powitania dysku (wartość domyślna to 95. percentyl), w tym hello przyszłych współczynnik wzrostu (wartość domyślna to 30 procent). Należy pamiętać, że hello całkowita odczytu/zapisu IOPS maszyny wirtualnej nie zawsze hello sumę hello wirtualna poszczególnych dysków odczytu/zapisu IOPS, ponieważ hello szczytu odczytu/zapisu IOPS hello maszyny Wirtualnej jest hello piku hello sumę jego poszczególnych dysków odczytu/zapisu IOPS podczas co minutę hello okres profilowania.

**Danych churn — w MB/s (o wskaźnik wzrostu)**: hello szczytowa przenoszenie szybkość na powitania dysku (wartość domyślna to 95. percentyl), w tym hello przyszłych współczynnik wzrostu (wartość domyślna to 30 procent). Należy pamiętać, że hello przenoszenie wszystkich danych z hello maszyny Wirtualnej nie jest zawsze hello sumę tworzeniem danych hello wirtualna poszczególnych dysków, ponieważ tworzeniem danych szczytu hello z hello maszyny Wirtualnej jest szczytu hello hello sumy przenoszenie jego poszczególnych dysków podczas co minutę hello profilowania okresu.

**Rozmiar maszyny Wirtualnej Azure**: hello idealne zmapowane rozmiar maszyny wirtualnej usługi w chmurze Azure dla to lokalnej maszyny Wirtualnej. Mapowanie Hello jest oparty na pamięci VM lokalne powitania, liczbę dysków rdzeni/kart sieciowych i odczytu/zapisu IOPS. zalecenie Hello jest zawsze hello najniższy Azure rozmiar maszyny Wirtualnej odpowiadający wszystkie właściwości maszyny Wirtualnej lokalne powitania.

**Liczba dysków**: hello całkowitej liczby dysków maszyny wirtualnej (VMDKs) na powitania maszyny Wirtualnej.

**Rozmiar (GB) dysku**: hello ustawiony łączny rozmiar wszystkich dysków hello maszyny Wirtualnej. Narzędzie Hello zawiera również hello rozmiar dysku dla poszczególnych dysków hello w hello maszyny Wirtualnej.

**Rdzenie**: hello liczba Procesora rdzenie na powitania maszyny Wirtualnej.

**Pamięć (MB)**: hello pamięci RAM na powitania maszyny Wirtualnej.

**Karty sieciowe**: hello liczbę kart sieciowych na powitania maszyny Wirtualnej.

**Rozruch typu**: jest typu rozruchowego hello maszyny Wirtualnej. Dozwolone wartości to BIOS i EFI. Obecnie usługa Azure Site Recovery obsługuje tylko typ rozruchu BIOS. Wszystkie maszyny wirtualne hello typu rozruchowego EFI są wyświetlane w arkuszu niezgodne maszyn wirtualnych.

**Typ systemu operacyjnego**: hello jest typ systemu operacyjnego hello maszyny Wirtualnej. Dozwolone wartości to Windows, Linux i inny.

## <a name="incompatible-vms"></a>Niezgodne maszyny wirtualne

![Arkusz kalkulacyjny programu Excel zawierający niezgodne maszyny wirtualne](./media/site-recovery-deployment-planner/incompatible-vms.png)

**Nazwa maszyny Wirtualnej**: hello nazwę maszyny Wirtualnej lub adres IP, który jest używany w hello VMListFile po wygenerowaniu raportu. Ta kolumna zawiera również VMDKs hello, które są dołączone toohello maszyn wirtualnych. toodistinguish vCenter maszyny wirtualne z zduplikowanych nazw lub adresów IP, nazwy hello zawierają nazwę hosta ESXi hello. Hello wymienionych hosta ESXi jest hello jedną hello maszyna wirtualna została rozmieszczenia gdy narzędzie hello wykryte podczas hello profilowania okresu.

**Maszyna wirtualna zgodności**: wskazuje, dlaczego hello podanej maszyny Wirtualnej jest niezgodna do użycia z usługą Site Recovery. Witaj przyczyn opisane dla każdego niezgodne dysku hello maszyny Wirtualnej i, na podstawie na opublikowane [limity magazynu](https://aka.ms/azure-storage-scalbility-performance), możesz użyć dowolnej z następujących hello:

* Rozmiar dysku jest większy niż 4095 GB. Usługa Azure Storage obecnie nie obsługuje dysków danych większych niż 4095 GB.
* Rozmiar dysku systemu operacyjnego jest większy niż 2048 GB. Usługa Azure Storage obecnie nie obsługuje dysków systemów operacyjnych większych niż 2048 GB.
* Typ rozruchu to EFI. Obecnie usługa Azure Site Recovery obsługuje tylko maszyny wirtualne o typie rozruchu BIOS.

* Całkowity rozmiar maszyny Wirtualnej (replikacji + TFO) przekracza limit rozmiaru hello obsługiwane konta magazynu (35 TB). Ta niezgodność zwykle występuje, gdy jednego dysku hello maszyna wirtualna ma charakterystyki, przekraczającą hello maksymalną obsługiwaną Azure lub usługi Site Recovery wartością dla magazynu w warstwie standardowa. Takie wystąpienie wypycha hello maszyny Wirtualnej do strefy magazynu premium hello. Jednak hello maksymalny obsługiwany rozmiar konto magazynu w warstwie premium jest 35 TB i jeden chronione maszyny Wirtualnej nie może być chroniony przez wiele kont magazynu. Należy również zauważyć, że podczas testowania trybu failover jest wykonywane na chronionej maszynie Wirtualnej, działa w hello tego samego konta magazynu, w którym postępuje replikacji. W tym wystąpieniu ustawienie 2 x hello rozmiar dysku hello tooprogress replikacji i testowania trybu failover toosucceed równolegle.
* Źródłowe operacje we/wy na sekundę przekraczają obsługiwany limit operacji we/wy na sekundę magazynu wynoszący 5000 operacji na dysk.
* Źródłowe operacje we/wy na sekundę przekraczają obsługiwany limit operacji we/wy na sekundę maszyny wirtualnej wynoszący 80 000 operacji na dysk.
* Przenoszenie uśrednianie danych przekracza obsługiwany limit przenoszenia danych usługi Site Recovery 10 MB/s dla średni rozmiar operacji We/Wy dysku hello.
* Przenoszenie wszystkich danych na wszystkich dyskach na powitania maszyny Wirtualnej przekracza hello maksymalny obsługiwany limit przenoszenie danych usługi Site Recovery 54 Mb/s dla maszyny Wirtualnej.
* Średnia zapisu skuteczne IOPS przekracza limit IOPS odzyskiwania lokacji hello obsługiwane 840 dla dysku.
* Migawki obliczeniowej magazynu przekracza limit pamięci masowej migawki hello obsługiwane 10 TB.

**IOPS odczyt/zapis (o wskaźnik wzrostu)**: hello szczytowego obciążenia IOPS na powitania dysku (wartość domyślna to 95. percentyl), w tym hello przyszłych współczynnik wzrostu (wartość domyślna to 30 procent). Należy pamiętać, że hello całkowita odczytu/zapisu IOPS hello maszyny Wirtualnej nie zawsze hello sumę hello wirtualna poszczególnych dysków odczytu/zapisu IOPS, ponieważ hello szczytu odczytu/zapisu IOPS hello maszyny Wirtualnej jest hello piku hello sumę jego poszczególnych dysków odczytu/zapisu IOPS podczas co minutę hello okres profilowania.

**Danych churn — w MB/s (o wskaźnik wzrostu)**: hello szczytowa przenoszenie szybkość na dysku hello (domyślna 95. percentyl) tym hello przyszłych współczynnik wzrostu (domyślna 30 procent). Należy pamiętać, że hello przenoszenie wszystkich danych z hello maszyny Wirtualnej nie jest zawsze hello sumę tworzeniem danych hello wirtualna poszczególnych dysków, ponieważ tworzeniem danych szczytu hello z hello maszyny Wirtualnej jest szczytu hello hello sumy przenoszenie jego poszczególnych dysków podczas co minutę hello profilowania okresu.

**Liczba dysków**: hello łączna liczba VMDKs na powitania maszyny Wirtualnej.

**Rozmiar (GB) dysku**: hello ustawiony łączny rozmiar wszystkich dysków hello maszyny Wirtualnej. Narzędzie Hello zawiera również hello rozmiar dysku dla poszczególnych dysków hello w hello maszyny Wirtualnej.

**Rdzenie**: hello liczba Procesora rdzenie na powitania maszyny Wirtualnej.

**Pamięć (MB)**: hello ilość pamięci RAM na powitania maszyny Wirtualnej.

**Karty sieciowe**: hello liczbę kart sieciowych na powitania maszyny Wirtualnej.

**Rozruch typu**: jest typu rozruchowego hello maszyny Wirtualnej. Dozwolone wartości to BIOS i EFI. Obecnie usługa Azure Site Recovery obsługuje tylko typ rozruchu BIOS. Wszystkie maszyny wirtualne hello typu rozruchowego EFI są wyświetlane w arkuszu niezgodne maszyn wirtualnych.

**Typ systemu operacyjnego**: hello jest typ systemu operacyjnego hello maszyny Wirtualnej. Dozwolone wartości to Windows, Linux i inny.


## <a name="site-recovery-limits"></a>Limity usługi Site Recovery

**Cel magazynu replikacji** | **Średni rozmiar źródłowych operacji we/wy na dysku** |**Średni źródłowy współczynnik zmian danych na dysku** | **Łączny współczynnik zmian danych na dysku dziennie**
---|---|---|---
Standard Storage | 8 KB | 2 MB/s | 168 GB na dysk
Dysk Premium P10 | 8 KB | 2 MB/s | 168 GB na dysk
Dysk Premium P10 | 16 KB | 4 MB/s | 336 GB na dysk
Dysk Premium P10 | 32 KB lub większy | 8 MB/s | 672 GB na dysk
Dysk Premium P20 lub P30 | 8 KB  | 5 MB/s | 421 GB na dysk
Dysk Premium P20 lub P30 | 16 KB lub większy |10 MB/s | 842 GB na dysk

Są to średnie wartości przy założeniu 30-procentowego nakładania się operacji we/wy. Usługa Site Recovery może obsługiwać większą przepływność na podstawie zakresu nakładania się na siebie, większego rozmiaru operacji zapisu i rzeczywistego zachowania związanego z obciążeniem operacji we/wy. Witaj poprzednich numerów założono typowe zaległości około pięciu minut. Oznacza to, że przekazane dane są przetwarzane i punkt odzyskiwania jest tworzony w ciągu pięciu minut.

Limity te są oparte na naszych testach, ale nie obejmują wszystkich możliwych kombinacji operacji we/wy aplikacji. Rzeczywiste wyniki mogą różnić w zależności od kombinacji operacji we/wy aplikacji. Aby uzyskać najlepsze wyniki nawet po zakończeniu planowania wdrożenia, zawsze zalecamy wykonanie szeroką gamę testowania przy użyciu obraz testowy tryb failover tooget hello true wydajności aplikacji.

## <a name="updating-hello-deployment-planner"></a>Aktualizowanie hello wdrożenia planistę
Planowanie wdrożenia hello tooupdate, hello następujące:

1. Pobieranie najnowszej wersji hello hello [planowania wdrożenia usługi Azure Site Recovery](https://aka.ms/asr-deployment-planner).

2. Kopiuj hello .zip folderu tooa serwera, które mają toorun go.

3. Wyodrębnij hello folderu zip.

4. Wykonaj jedną z następujących hello:
 * Profilowanie jest już w toku na bieżącą wersję hello planner hello najnowszą wersję nie zawiera profilowania poprawkę, nadal hello profilowania.
 * Jeśli hello najnowszej wersji zawierają profilowania poprawkę, zaleca się zatrzymanie profilowania na bieżącą wersję, a następnie ponownie uruchom profilowanie hello hello nowej wersji.

  >[!NOTE]
  >
  >Po uruchomieniu profilowanie z hello nowej wersji, hello przebiegu sam wyjściowy ścieżki katalogu, dzięki czemu hello narzędzia dołącza dane profilu na hello istniejące pliki. Pełny zestaw danych profilowanych zostanie użyty toogenerate hello raport. Jeśli przekazujesz katalogu różne wyniki, są tworzone nowe pliki i starego profilowane danych nie jest używany toogenerate hello raportu.
  >
  >Każdego nowego wdrożenia planistę jest zbiorcza aktualizacja hello pliku zip. Nie trzeba toocopy hello najnowsze pliki toohello poprzedniego folderu. Można utworzyć nowy folder i użyć go.


## <a name="version-history"></a>Historia wersji

### <a name="131"></a>1.3.1
Aktualizacja: 19 lipca 2017 r.

Dodano następującą nową funkcję:

* Dodano obsługę dużych dysków (powyżej 1 TB) na potrzeby generowania raportów. Teraz można użyć wdrożenia planistę tooplan replikację dla maszyn wirtualnych, które mają dysku o rozmiarze przekraczającym 1 TB (maksymalnie 4095 GB).
Dowiedz się więcej na temat [obsługi dużych dysków w usłudze Azure Site Recovery](https://azure.microsoft.com/en-us/blog/azure-site-recovery-large-disks/)


### <a name="13"></a>1.3
Aktualizacja: 9 maja 2017 r.

Dodano następującą nową funkcję:

* Dodano obsługę dysku zarządzanego na potrzeby generowania raportów. Witaj liczbę maszyn wirtualnych można umieścić tooa pojedynczy magazyn konto jest obliczeniowa na podstawie, jeśli zarządzany dysk został wybrany do trybu Failover i testowanie trybu failover.        


### <a name="12"></a>1.2
Zaktualizowano: 7 kwietnia 2017 r.

Dodano następujące poprawki:

* Dodano rozruchu typu wyboru (BIOS lub EFI) dla każdego toodetermine maszyny wirtualnej, jeśli maszyna wirtualna hello jest zgodne lub niezgodne dla ochrona powitalnych.
* Dodano systemu operacyjnego wpisz informacje dla każdej maszyny wirtualnej w hello zgodne maszyn wirtualnych i arkuszy niezgodne maszyn wirtualnych.
* Witaj GetThroughput operacji jest teraz obsługiwany w regionach hello instytucji rządowych Stanów Zjednoczonych i Chin Microsoft Azure.
* Dodano kilka testów wymagań wstępnych dla serwerów vCenter i ESXi.
* Wygenerowano pobierania niepoprawne raportu, gdy ustawienia regionalne jest ustawiona toonon w języku angielskim.


### <a name="11"></a>1.1
Aktualizacja: 9 marca 2017 r.

Stałe hello następujące problemy:

* Narzędzie Hello nie może profilu maszyn wirtualnych, jeśli hello vCenter zawiera dwa lub więcej maszyn wirtualnych o hello tej samej nazwy lub adresu IP na różnych hostach ESXi.
* Kopiuj i wyszukiwania jest wyłączona dla arkuszy hello maszyny wirtualne zgodne i niezgodne maszyn wirtualnych.

### <a name="10"></a>1.0
Aktualizacja: 23 lutego 2017 r.

Azure w lokacji odzyskiwania wdrożenia Planistę publicznej wersji zapoznawczej 1.0 ma hello następujące znane problemy (toobe rozwiązane w kolejnych aktualizacji):

* Narzędzie Hello działa tylko w przypadku scenariuszy VMware do platformy Azure nie we wdrożeniach funkcji Hyper-V-do-platformy Azure. W scenariuszach funkcji Hyper-V-do-platformy Azure, użyj hello [planisty wydajności funkcji Hyper-V](./site-recovery-capacity-planning-for-hyper-v-replication.md).
* Witaj GetThroughput operacji nie jest obsługiwana w regionach hello instytucji rządowych Stanów Zjednoczonych i platformy Microsoft Azure w Chinach.
* Narzędzie Hello nie może profilu maszyn wirtualnych, jeśli serwer vCenter hello ma dwa lub więcej maszyn wirtualnych o hello tej samej nazwy lub adresu IP na różnych hostach ESXi. W tej wersji narzędzia hello pomija profilowania zduplikowanych nazw maszyn wirtualnych lub adresów IP w hello VMListFile. Obejście Hello jest hello tooprofile maszyn wirtualnych przy użyciu hosta ESXi zamiast hello vCenter server. Musisz uruchomić jedno wystąpienie każdego hosta ESXi.
