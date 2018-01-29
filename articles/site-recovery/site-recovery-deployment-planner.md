---
title: "Planista wdrożenia usługi Azure Site Recovery dla oprogramowania VMware na platformie Azure | Microsoft Docs"
description: "Jest to podręcznik użytkownika planisty wdrożenia usługi Azure Site Recovery."
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
ms.date: 12/04/2017
ms.author: nisoneji
ms.openlocfilehash: 2985ed0b4bf5d9525bc2274d71b703922524f5a8
ms.sourcegitcommit: 176c575aea7602682afd6214880aad0be6167c52
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/09/2018
---
# <a name="azure-site-recovery-deployment-planner-for-vmware-to-azure"></a>Planista wdrażania usługi Azure Site Recovery dla oprogramowania VMware na platformie Azure
Ten artykuł to podręcznik użytkownika planisty wdrożenia usługi Azure Site Recovery dla wdrożeń produkcyjnych oprogramowania VMware na platformie Azure.

## <a name="overview"></a>Przegląd

Zanim zaczniesz chronić maszyny wirtualne oprogramowania VMware za pomocą usługi Site Recovery, przydziel odpowiednią przepustowość zgodnie z częstotliwością dziennych zmian danych, aby osiągnąć założony cel punktu odzyskiwania. Pamiętaj o lokalnym wdrożeniu odpowiedniej liczby serwerów konfiguracji i serwerów przetwarzania.

Musisz także utworzyć właściwą liczbę kont magazynów platformy Azure odpowiedniego typu. Możesz utworzyć konta magazynu w warstwie Standardowa lub Premium, biorąc pod uwagę wzrost w zakresie źródłowych serwerów produkcyjnych z powodu zwiększania użycia w czasie. Wybierz typ magazynu dla maszyny wirtualnej w oparciu o charakterystyki obciążenia (np. operacje we/wy odczytu/zapisu na sekundę (IOPS) lub współczynnik zmian danych) oraz limity usługi Site Recovery.

Planista wdrażania usługi Azure Site Recovery to narzędzie wiersza polecenia na potrzeby scenariuszy odzyskiwania po awarii z funkcji Hyper-V do platformy Azure i z oprogramowania VMware do platformy Azure. To narzędzie pozwala zdalnie profilować maszyny wirtualne oprogramowania VMware (bez żadnego wpływu na środowisko produkcyjne), aby poznać wymagania dotyczące przepustowości i magazynu Azure Storage dla udanej replikacji oraz testu pracy w trybie failover. Narzędzie możesz uruchomić bez instalowania składników usługi Site Recovery w środowisku lokalnym. Jednak w celu uzyskania dokładnych wyników osiągniętej przepływności zaleca się uruchomienie planisty na serwerze z systemem Windows Server spełniającym minimalne wymagania dotyczące serwera konfiguracji usługi Site Recovery, który trzeba będzie wdrożyć na początku procesu wdrażania w środowisku produkcyjnym.

Narzędzie udostępnia następujące szczegóły:

**Ocena zgodności**

* Ocena uprawnień maszyny wirtualnej na podstawie liczby dysków, rozmiaru dysku, liczby operacji we/wy na sekundę, współczynnika zmian, typu rozruchu (EFI/BIOS) i wersji systemu operacyjnego
 
**Zapotrzebowanie na przepustowość sieci w porównaniu z oceną celu punktu odzyskiwania**

* Szacowana przepustowość sieci wymagana na potrzeby replikacji przyrostowej
* Przepływność, którą usługa Site Recovery może uzyskać między środowiskiem lokalnym i platformą Azure
* Liczba maszyn wirtualnych do przetworzenia wsadowego na podstawie szacowanej przepustowości wymagana do ukończenia replikacji początkowej w określonym czasie
* Cel punktu odzyskiwania, który można osiągnąć przy danej przepustowości
* Wpływ na wymagany cel punktu odzyskiwania w przypadku zapewnienia mniejszej przepustowości.

**Wymagania dotyczące infrastruktury platformy Azure**

* Wymagania dotyczące typu magazynu (konta w warstwie Standardowa lub Premium) dla poszczególnych maszyn wirtualnych
* Łączna liczba kont magazynu w warstwie Standardowa i Premium do skonfigurowania na potrzeby replikacji
* Propozycje nazw kont magazynu oparte na wskazówkach usługi Azure Storage
* Rozmieszczanie konta magazynu dla wszystkich maszyn wirtualnych
* Liczba rdzeni platformy Azure do skonfigurowania przed rozpoczęciem pracy w trybie failover lub testu pracy w trybie failover w ramach subskrypcji
* Zalecany rozmiar poszczególnych maszyn wirtualnych platformy Azure

**Wymagania dotyczące infrastruktury lokalnej**
* Wymagana liczba serwerów konfiguracji i serwerów przetwarzania do wdrożenia w środowisku lokalnym

**Szacowany koszt odzyskiwania po awarii do platformy Azure**
* Szacowany łączny koszt odzyskiwania po awarii do platformy Azure: koszt obliczeń, magazynu, sieci i licencji usługi Azure Site Recovery
* Szczegółowa analiza kosztów dla maszyny wirtualnej


>[!IMPORTANT]
>
>Ponieważ obciążenie będzie prawdopodobnie zwiększać się wraz z upływem czasu, wszystkie poprzednie obliczenia narzędzia są wykonywane przy założeniu 30-procentowego współczynnika wzrostu wartości charakterystyk obciążenia i przy użyciu wartości 95. percentyla wszystkich metry profilowania (operacje we/wy odczytu/zapisu na sekundę, współczynnik zmian danych itd.). Oba te elementy (współczynnik wzrostu i obliczenie wartości percentyla) można konfigurować. Więcej informacji na temat współczynnika wzrostu można znaleźć w sekcji „Zagadnienia związane ze współczynnikiem wzrostu”. Więcej informacji na temat wartości percentyla można znaleźć w sekcji „Wartość percentyla użyta w obliczeniach”.
>

## <a name="support-matrix"></a>Tabela obsługi

| | **Z programu VMware do platformy Azure** |**Z funkcji Hyper-V do platformy Azure**|**Z platformy Azure do platformy Azure**|**Z funkcji Hyper-V do lokacji dodatkowej**|**Z oprogramowania VMware do lokacji dodatkowej**
--|--|--|--|--|--
Obsługiwane scenariusze |Yes|Yes|Nie|Tak*|Nie
Obsługiwana wersja | vCenter 6.5, 6.0 lub 5.5| Windows Server 2016, Windows Server 2012 R2 | Nie dotyczy |Windows Server 2016, Windows Server 2012 R2|Nie dotyczy
Obsługiwana konfiguracja|vCenter, ESXi| Klaster funkcji Hyper-V, host funkcji Hyper-V|Nie dotyczy|Klaster funkcji Hyper-V, host funkcji Hyper-V|Nie dotyczy|
Liczba serwerów, które mogą być profilowane, na uruchomione wystąpienie planisty wdrażania usługi Azure Site Recovery |Jeden (w tym samym czasie można profilować maszyny wirtualne należące do jednego serwera vCenter lub jednego serwera ESXi)|Wiele (w tym samym czasie można profilować maszyny wirtualne należące do wielu hostów lub klastrów hostów)| Nie dotyczy |Wiele (w tym samym czasie można profilować maszyny wirtualne należące do wielu hostów lub klastrów hostów)| Nie dotyczy

* Narzędzie jest przeznaczone głównie dla scenariuszy odzyskiwania po awarii z funkcji Hyper-V do platformy Azure. W przypadku odzyskiwania po awarii z funkcji Hyper-V do lokacji dodatkowej można używać go tylko do sprawdzania zaleceń po stronie źródła, takich jak wymagana przepustowość, wymagana ilość wolnego miejsca na każdym serwerze źródłowym funkcji Hyper-V oraz wartości dzielenia na partie replikacji początkowej i definicje partii.  Zignoruj zalecenia i koszty dotyczące platformy Azure z raportu. Ponadto nie można używać operacji uzyskiwania informacji o przepływności w scenariuszu odzyskiwania po awarii z funkcji Hyper-V do lokacji dodatkowej.

## <a name="prerequisites"></a>Wymagania wstępne
Narzędzie obejmuje dwa główne etapy — profilowanie i generowanie raportu. Jest też dostępny trzeci etap umożliwiający obliczanie tylko przepływności. Wymagania dotyczące serwera, z którego inicjowane jest profilowanie i pomiar przepływności, zostały przedstawione w poniższej tabeli:

| Wymaganie dotyczące serwera | Opis|
|---|---|
|Profilowanie i pomiar przepływności| <ul><li>System operacyjny: Microsoft Windows Server 2016 lub Microsoft Windows Server 2012 R2<br>(w idealnej sytuacji spełniający co najmniej [zalecenia dotyczące rozmiaru serwera konfiguracji](https://aka.ms/asr-v2a-on-prem-components))</li><li>Konfiguracja maszyny: 8 wirtualnych procesorów CPU, 16 GB pamięci RAM, dysk twardy o rozmiarze 300 GB</li><li>[Microsoft .NET Framework 4.5](https://aka.ms/dotnet-framework-45)</li><li>[VMware vSphere PowerCLI 6.0 R3](https://aka.ms/download_powercli)</li><li>[Pakiet Microsoft Visual C++ Redistributable dla programu Visual Studio 2012](https://aka.ms/vcplusplus-redistributable)</li><li>Dostęp do platformy Azure przez Internet z tego serwera</li><li>Konto magazynu Azure</li><li>Dostęp administratora na serwerze</li><li>Minimalnie 100 GB wolnego miejsca na dysku (przy założeniu 1000 maszyn wirtualnych z średnio trzema dyskami na każdej z nich i profilowanych przez 30 dni)</li><li>Ustawienia poziomu statystyk programu VMware vCenter powinny być na poziomie 2 lub wyższym</li><li>Zezwalaj na port 443: planista wdrożenia usługi ASR używa tego portu do nawiązywania połączenia z serwerem vCenter/hostem ESXi</ul></ul>|
| Generowanie raportu | Dowolny komputer z systemem Windows lub Windows Server i programem Microsoft Excel 2013 lub nowszym |
| Uprawnienia użytkowników | Uprawnienia tylko do odczytu dla konta użytkownika używanego do uzyskiwania dostępu do serwera VMware vCenter/hosta VMware vSphere ESXi podczas profilowania |

> [!NOTE]
>
>Narzędzie może profilować tylko maszyny wirtualne z dyskami VMDK i RDM. Nie pozwala ono profilować maszyn wirtualnych z dyskami iSCSI ani NFS. Usługa Site Recovery obsługuje dyski iSCSI i NFS w przypadku serwerów VMware, ponieważ planista wdrożenia nie znajduje się na gościu i profiluje tylko przy użyciu liczników wydajności programu vCenter, jednak narzędzie nie ma wglądu w te typy dysków.
>

## <a name="download-and-extract-the-deployment-planner-tool"></a>Pobieranie i wyodrębnianie narzędzia planisty wdrażania
1. Pobierz najnowszą wersję [planisty wdrożenia usługi Azure Site Recovery](https://aka.ms/asr-deployment-planner).  
Narzędzie jest spakowane w folderze ZIP. Bieżąca wersja narzędzia obsługuje tylko replikację z oprogramowania VMware do platformy Azure.

2. Skopiuj folder ZIP na serwer z systemem Windows, z którego chcesz uruchomić narzędzie.  
Narzędzie można uruchomić z systemu Windows Server 2012 R2, jeśli serwer ma dostęp do sieci umożliwiający połączenie z serwerem vCenter/hostem vSphere ESXi przechowującym maszyny wirtualne do profilowania. Zalecamy jednak uruchamianie narzędzia na serwerze, którego konfiguracja sprzętowa spełnia [wytyczne dotyczące określania rozmiaru serwera konfiguracji](https://aka.ms/asr-v2a-on-prem-components). Jeśli wdrożono już lokalnie składniki usługi Site Recovery, uruchom narzędzie na serwerze konfiguracji.

 Na serwerze, na którym uruchamiasz narzędzie, zalecamy korzystanie z takiej samej konfiguracji sprzętu jak serwer konfiguracji (z wbudowanym serwerem przetwarzania). Dzięki takiej konfiguracji masz pewność, że osiągnięta przepływność zgłaszana przez narzędzie jest zgodna z rzeczywistą przepływnością, którą usługa Site Recovery może osiągnąć podczas replikacji. Obliczanie przepływności zależy od dostępnej przepustowości sieci na serwerze i konfiguracji sprzętu (procesor CPU, magazyn itd.) serwera. Jeśli uruchamiasz narzędzie z innego serwera, obliczana jest przepływność z tego serwera na platformę Microsoft Azure. Ponadto ponieważ konfiguracja sprzętu serwera może różnić się od konfiguracji serwera konfiguracji, dane osiągniętej przepływności zgłaszanej przez narzędzie mogą być niedokładne.

3. Wyodrębnij folder ZIP.  
Folder zawiera wiele plików i podfolderów. Plik wykonywalny nosi nazwę ASRDeploymentPlanner.exe i znajduje się w folderze nadrzędnym.

    Przykład:  
    Skopiuj plik ZIP na dysk E:\ i wyodrębnij go.
   E:\ASR Deployment Planner_v2.1zip

    E:\ASR Deployment Planner_v2.1\ASRDeploymentPlanner.exe

### <a name="updating-to-the-latest-version-of-deployment-planner"></a>Aktualizowanie planisty wdrażania do najnowszej wersji
Jeśli masz wcześniejszą wersję planisty wdrażania, wykonaj jedną z następujących czynności:
 * Jeśli najnowsza wersja nie zawiera poprawki profilowania i profilowanie jest już w toku w bieżącej wersji planisty, kontynuuj profilowanie.
 * Jeśli najnowsza wersja zawiera poprawkę profilowania, zalecamy zatrzymanie profilowania w bieżącej wersji, a następnie jego ponowne uruchomienie w nowej wersji.


 >[!NOTE]
 >
 >W przypadku uruchamiania profilowania w nowej wersji przekaż taką samą ścieżkę katalogu wyjściowego, aby narzędzie dołączało dane profilu do istniejących plików. Do wygenerowania raportu zostanie użyty kompletny zestaw profilowanych danych. Jeśli przekażesz inny katalog danych wyjściowych, zostaną utworzone nowe pliki, a stare profilowane dane nie będą używane podczas generowania raportu.
 >
 >Każdy nowy planista wdrożenia jest aktualizacją zbiorczą pliku ZIP. Nie musisz kopiować najnowszych plików do poprzedniego folderu. Można utworzyć nowy folder i użyć go.


## <a name="version-history"></a>Historia wersji
Najnowszą wersją narzędzia Planista wdrażania usługi ASR jest wersja 2.1.
Informacje na temat poprawek, które zostały dodane w poszczególnych aktualizacjach, możesz znaleźć na stronie [Historia wersji narzędzia Planista wdrażania usługi ASR](https://social.technet.microsoft.com/wiki/contents/articles/51049.asr-deployment-planner-version-history.aspx).

## <a name="next-steps"></a>Następne kroki
* [Uruchamianie planisty wdrażania](site-recovery-vmware-deployment-planner-run.md)
