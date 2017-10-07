---
title: "aaaUse obliczeniowych maszyn wirtualnych platformy Azure z instancją | Dokumentacja firmy Microsoft"
description: "Jak rozmiary tootake zaletą maszyny Wirtualnej z funkcją RDMA lub włączone procesora GPU w pulach partii zadań Azure"
services: batch
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: 
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: danlep
ms.openlocfilehash: 6a462a5f2a44ddcec8bf4e5c200d444cac8fafe6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-rdma-capable-or-gpu-enabled-instances-in-batch-pools"></a>Użyj wystąpień z funkcją RDMA lub włączone procesora GPU w pulach partii

toorun niektórych zadań wsadowych może być tootake zaletą rozmiary maszyn wirtualnych Azure przeznaczone do obliczeń na dużą skalę. Na przykład toorun wielowystąpieniowy [obciążeń MPI](batch-mpi.md), można wybrać A8 i A9, lub rozmiary H-series, które sieci interfejsu dla zdalnego bezpośredniego pamięci Access (RDMA). Rozmiary połączenia sieciowe InfiniBand tooan do komunikacji między węzłami, która umożliwia przyspieszanie MPI aplikacji. W przypadku aplikacji CUDA. można też rozmiary N-series, które obejmują grafiki tesla — NVIDIA przetwarzania kart jednostkę GPU.

Ten artykuł zawiera wskazówki i przykłady toouse niektóre rozmiary specjalne platformy Azure w pulach partii. Aby uzyskać dane techniczne i tło Zobacz:

* Wysoka wydajność obliczeniowe rozmiarów maszyn wirtualnych ([Linux](../virtual-machines/linux/sizes-hpc.md), [Windows](../virtual-machines/windows/sizes-hpc.md)) 

* Rozmiary maszyn wirtualnych z obsługą procesora GPU ([Linux](../virtual-machines/linux/sizes-gpu.md), [Windows](../virtual-machines/windows/sizes-gpu.md)) 


## <a name="subscription-and-account-limits"></a>Subskrypcja oraz limity konta

* **Przydziały** — co najmniej jeden limitach przydziału platformy Azure może ograniczyć liczbę hello lub typ węzłów można dodać puli partii tooa. Użytkownik jest bardziej prawdopodobne toobe ograniczone po wybraniu z funkcją RDMA, GPU jest włączona, czy inne wielordzeniowych rozmiarów maszyn wirtualnych. W zależności od typu hello utworzone konto usługi partia zadań przydziały hello można zastosować samo konto toohello lub tooyour subskrypcji.

    * Jeśli utworzono konto wsadowe w hello **partii usługi** konfiguracji, są ograniczone przez hello [limit przydziału rdzeni dedykowanych na konto usługi partia zadań](batch-quota-limit.md#resource-quotas). Domyślnie ten przydział jest 20 rdzeni. Oddzielne zasoby odnoszą się zbyt[maszyn wirtualnych niskiego priorytetu](batch-low-pri-vms.md), jeśli są używane. 

    * Jeśli utworzono konto hello w hello **subskrypcji użytkownika** konfiguracji subskrypcji ogranicza hello liczba rdzeni maszyny Wirtualnej w regionie. Zobacz [subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](../azure-subscription-service-limits.md). Subskrypcja ma również zastosowanie regionalnych przydziału toocertain rozmiarów maszyn wirtualnych, w tym wystąpienia HPC i procesora GPU. W konfiguracji subskrypcji użytkownika hello nie dodatkowych przydziałach zastosować toohello konta usługi partia zadań. 

  Może być konieczne tooincrease na co najmniej jeden przydziały używając wyspecjalizowany rozmiar maszyny Wirtualnej w partii. toorequest zwiększenia limitu przydziału, otwórz [żądania obsługi online klienta](../azure-supportability/how-to-create-azure-support-request.md) bez dodatkowych opłat.

* **Dostępność w danym regionie** — obliczeniowych maszyn wirtualnych mogą nie być dostępne w regionach hello, w której utworzono konta usługi partia zadań. toocheck, że rozmiar jest dostępny, zobacz [produkty, które są dostępne w regionie](https://azure.microsoft.com/regions/services/).


## <a name="dependencies"></a>Zależności

Witaj RDMA i procesora GPU możliwości obliczeniowych rozmiary są obsługiwane tylko w niektórych systemach operacyjnych. W zależności od systemu operacyjnego może być konieczne tooinstall lub skonfigurować dodatkowe sterowników lub innego oprogramowania. następujące tabele Hello podsumowanie tych zależności. Zobacz połączonych artykułów, aby uzyskać szczegółowe informacje. Dla opcji tooconfigure partii pul zobacz w dalszej części tego artykułu.


### <a name="linux-pools---virtual-machine-configuration"></a>Pule Linux - konfiguracji maszyny wirtualnej

| Rozmiar | Możliwości | Systemy operacyjne | Wymagane oprogramowanie | Ustawienia puli |
| -------- | -------- | ----- |  -------- | ----- |
| [H16r, H16mr, A8, A9](../virtual-machines/linux/sizes-hpc.md#rdma-capable-instances) | DOSTĘP RDMA | SUSE Linux Enterprise Server 12 HPC lub<br/>Na podstawie centOS HPC<br/>(Azure Marketplace) | Intel MPI 5 | Włącz komunikację między węzłami, uniemożliwić wykonywanie zadań jednoczesnych |
| [NC serii *](../virtual-machines/linux/n-series-driver-setup.md#install-cuda-drivers-for-nc-vms) | NVIDIA tesla — K80 procesora GPU | Ubuntu 16.04 LTS.<br/>Red Hat Enterprise Linux 7.3, lub<br/>Oparty na systemie CentOS 7.3<br/>(Azure Marketplace) | Sterowniki NVIDIA CUDA Toolkit 8.0 | Nie dotyczy | 
| [Seria wirtualizacją sieci](../virtual-machines/linux/n-series-driver-setup.md#install-grid-drivers-for-nv-vms) | M60 tesla — NVIDIA GPU | Ubuntu 16.04 LTS<br/>Red Hat Enterprise Linux 7.3<br/>Oparty na systemie CentOS 7.3<br/>(Azure Marketplace) | 4.3 siatki NVIDIA sterowniki | Nie dotyczy |

* Łączność RDMA na maszynach wirtualnych NC24r jest obsługiwana na podstawie CentOS 7.3 HPC z Intel MPI.



### <a name="windows-pools---virtual-machine-configuration"></a>Pule systemu Windows — konfiguracja maszyny wirtualnej

| Rozmiar | Możliwości | Systemy operacyjne | Wymagane oprogramowanie | Ustawienia puli |
| -------- | ------ | -------- | -------- | ----- |
| [H16r, H16mr, A8, A9](../virtual-machines/windows/sizes-hpc.md#rdma-capable-instances) | DOSTĘP RDMA | Windows Server 2012 R2 lub<br/>Windows Server 2012 (Azure Marketplace) | Microsoft MPI 2012 R2 lub nowszym, lub<br/> Intel MPI 5<br/><br/>Rozszerzenia maszyny Wirtualnej Azure HpcVMDrivers | Włącz komunikację między węzłami, uniemożliwić wykonywanie zadań jednoczesnych |
| [NC serii *](../virtual-machines/windows/n-series-driver-setup.md) | NVIDIA tesla — K80 procesora GPU | Windows Server 2016 lub <br/>Windows Server 2012 R2 (Azure Marketplace) | Tesla — NVIDIA sterowników lub sterowników CUDA Toolkit 8.0| Nie dotyczy | 
| [Seria wirtualizacją sieci](../virtual-machines/windows/n-series-driver-setup.md) | M60 tesla — NVIDIA GPU | Windows Server 2016 lub<br/>Windows Server 2012 R2 (Azure Marketplace) | 4.3 siatki NVIDIA sterowniki | Nie dotyczy |

* Łączność RDMA na maszynach wirtualnych NC24r jest obsługiwana w systemie Windows Server 2012 R2 z rozszerzenia HpcVMDrivers i MPI firmy Microsoft lub Intel MPI.

### <a name="windows-pools---cloud-services-configuration"></a>Pule systemu Windows — Konfiguracja usług w chmurze

> [!NOTE]
> Rozmiary serii N nie są obsługiwane w pulach partii z konfiguracją usługi w chmurze hello.
>

| Rozmiar | Możliwości | Systemy operacyjne | Wymagane oprogramowanie | Ustawienia puli |
| -------- | ------- | -------- | -------- | ----- |
| [H16r, H16mr, A8, A9](../virtual-machines/windows/sizes-hpc.md#rdma-capable-instances) | DOSTĘP RDMA | Windows Server 2012 R2<br/>Windows Server 2012, lub<br/>Windows Server 2008 R2 (rodziny systemów operacyjnych gościa) | Microsoft MPI 2012 R2 lub nowszym, lub<br/>Intel MPI 5<br/><br/>Rozszerzenia maszyny Wirtualnej Azure HpcVMDrivers | Włącz komunikację między węzłami<br/> Wyłącz wykonywanie zadań jednoczesnych |





## <a name="pool-configuration-options"></a>Opcje konfiguracji puli

tooconfigure specjalne rozmiar maszyny Wirtualnej w puli partii, hello partii interfejsów API i narzędzia zawierają kilka opcji tooinstall wymaganego oprogramowania lub sterowników, w tym:

* [Uruchom zadanie](batch-api-basics.md#start-task) -przekazać pakietu instalacyjnego jako tooan pliku zasobów konta magazynu Azure w hello tego samego regionu hello konta usługi partia zadań. Trybie dyskretnym Utwórz plik zasobów tooinstall hello rozpoczęcia zadania wiersza polecenia po uruchomieniu puli hello. Aby uzyskać więcej informacji, zobacz hello [dokumentacja interfejsu API REST](/rest/api/batchservice/add-a-pool-to-an-account#bk_starttask).

  > [!NOTE] 
  > Hello rozpoczęcia zadań należy uruchomić z uprawnieniami z podniesionymi uprawnieniami (Administrator) i poczekaj, aż Powodzenie.
  >

* [Pakiet aplikacji](batch-application-packages.md) — Dodawanie tooyour pakietu ZIP instalacji konta usługi partia zadań i konfigurowanie odwołanie do pakietu w puli hello. To ustawienie przekazuje i unzips hello pakiet we wszystkich węzłach w puli hello. Jeśli pakiet hello jest Instalator, Utwórz aplikacji hello instalacji toosilently rozpoczęcia zadań wiersza polecenia na wszystkich węzłach puli. Opcjonalnie należy zainstalować pakiet hello, gdy zadanie jest zaplanowane toorun w węźle.

* [Obraz niestandardowy puli](batch-api-basics.md#pool) — Tworzenie niestandardowych systemu Windows lub obrazu maszyny Wirtualnej systemu Linux, który zawiera sterowników, oprogramowania lub inne ustawienia wymagane dla hello rozmiar maszyny Wirtualnej. Jeśli utworzono konto wsadowe w konfiguracji subskrypcji użytkownika hello określić niestandardowy obraz powitania dla użytkownika puli partii. (Obrazy niestandardowe nie są obsługiwane na kontach w konfiguracji usługi partii hello). Niestandardowe obrazy można używać tylko z pul w konfiguracji maszyny wirtualnej hello.

  > [!IMPORTANT]
  > W puli partii obecnie nie można użyć niestandardowego obrazu utworzone z dysków zarządzanych lub magazyn w warstwie Premium.
  >



* [Partii stoczni](https://github.com/Azure/batch-shipyard) automatycznie konfiguruje hello procesora GPU i dostępu RDMA toowork w sposób niewidoczny dla użytkownika przy użyciu konteneryzowanych obciążeń w partii zadań Azure. Stoczni partii całkowicie wynikają z plikami konfiguracyjnymi. Istnieje wiele przykładowych przepisu konfiguracji dostępne umożliwiających obciążeń procesora GPU i funkcji RDMA, takich jak hello [CNTK GPU przepisu](https://github.com/Azure/batch-shipyard/tree/master/recipes/CNTK-GPU-OpenMPI) co wstępnie konfiguruje wersji sterowników procesora GPU na maszynach wirtualnych N serii i ładuje oprogramowania kognitywnych zestaw narzędzi firmy Microsoft jako obraz Docker.


## <a name="example-microsoft-mpi-on-an-a8-vm-pool"></a>Przykład: Microsoft MPI w puli maszyna wirtualna A8

toorun Windows MPI aplikacji w puli węzłów Azure A8, należy tooinstall obsługiwanych implementacji MPI. Poniżej przedstawiono przykładowe kroki tooinstall [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) na Windows puli przy użyciu pakietu aplikacji partii.

1. Pobierz hello [pakiet instalacyjny](http://go.microsoft.com/FWLink/p/?LinkID=389556) (MSMpiSetup.exe) dla hello najnowszą wersję programu Microsoft MPI.
2. Utwórz plik zip pakietu hello.
3. Przekaż konta usługi partia zadań tooyour pakietu hello. Aby uzyskać instrukcje, zobacz hello [pakietów aplikacji](batch-application-packages.md) wskazówki. Określ identyfikator aplikacji, takich jak *MSMPI*i wersji, takich jak *8.1*. 
4. Za pomocą interfejsów API partii hello lub portalu Azure, Utwórz pulę w konfiguracji usługi w chmurze hello przy użyciu hello żądaną liczbę węzłów i skali. Witaj poniższej tabeli przedstawiono przykładowe ustawienia tooset się MPI w trybie instalacji nienadzorowanej za pomocą zadania uruchamiania:

| Ustawienie | Wartość |
| ---- | ----- | 
| **Typ obrazu** | Cloud Services |
| **Rodzina systemów operacyjnych** | Windows Server 2012 R2 (rodziny systemów operacyjnych 4) |
| **Rozmiaru węzła** | A8 Standard |
| **Włączono komunikację między węzłami** | True |
| **Maksymalna liczba zadań na węzeł** | 1 |
| **Odwołania do pakietu aplikacji** | MSMPI |
| **Uruchom zadanie włączone** | True<br>**Wiersz polecenia** - `"cmd /c %AZ_BATCH_APP_PACKAGE_MSMPI#8.1%\\MSMpiSetup.exe -unattend -force"`<br/>**Tożsamość użytkownika** -autouser puli, administracja<br/>**Poczekaj, aż Powodzenie** — PRAWDA

## <a name="example-nvidia-tesla-drivers-on-nc-vm-pool"></a>Przykład: Tesla — NVIDIA sterowników w puli NC maszyny Wirtualnej

toorun CUDA aplikacji w puli węzłów Linux NC, należy tooinstall CUDA Toolkit 8.0 w węzłach hello. Witaj Toolkit instaluje hello niezbędne sterowniki NVIDIA tesla — GPU. Poniżej przedstawiono przykładowe kroki toodeploy niestandardowego obrazu Ubuntu 16.04 LTS z wersji sterowników procesora GPU hello:

1. Wdrażanie maszyny Wirtualnej platformy Azure NC6 systemem Ubuntu 16.04 LTS. Na przykład utworzyć hello maszyny Wirtualnej w regionie nam Południowa centralnej hello. Upewnij się, że tworzenie hello maszyny Wirtualnej z magazynu w warstwie standardowa, i *bez* dyskach zarządzanych.
2. Wykonaj hello kroki tooconnect toohello maszyny Wirtualnej i [zainstalować sterowniki CUDA](../virtual-machines/linux/n-series-driver-setup.md#install-cuda-drivers-for-nc-vms).
3. Anulowanie zastrzeżenia hello agenta systemu Linux, a następnie przechwycić obraz maszyny Wirtualnej systemu Linux przy użyciu polecenia hello Azure CLI w wersji 1.0. Aby uzyskać instrukcje, zobacz [Przechwytywanie maszyny wirtualnej systemu Linux działających na platformie Azure](../virtual-machines/linux/capture-image-nodejs.md). Zanotuj obraz powitania identyfikatora URI.
  > [!IMPORTANT]
  > Nie należy używać obrazu hello toocapture poleceń Azure CLI 2.0 partii zadań Azure. Obecnie polecenia hello CLI 2.0 przechwytywania maszyny wirtualne utworzone za pomocą dysków zarządzanych.
  >
4. Utwórz konto wsadowe hello konfiguracji subskrypcji użytkownika, w region, który obsługuje NC maszyn wirtualnych.
5. Za pomocą interfejsów API partii hello lub portalu Azure, tworzenie puli przy użyciu niestandardowego obrazu hello i z hello żądaną liczbę węzłów i skali. Witaj poniższej tabeli przedstawiono przykładowe ustawienia puli hello obrazu:

| Ustawienie | Wartość |
| ---- | ---- |
| **Typ obrazu** | Obraz niestandardowy |
| **Obraz niestandardowy** | Identyfikator URI w postaci hello obrazu`https://yourstorageaccountdisks.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd` |
| **Agent węzła jednostki SKU** | Batch.node.ubuntu 16.04 |
| **Rozmiaru węzła** | NC6 Standard |



## <a name="next-steps"></a>Następne kroki

* toorun zadań MPI w puli partii zadań Azure, zobacz hello [Windows](batch-mpi.md) lub [Linux](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/) przykłady.

* Przykłady obciążeń procesora GPU w partii, zobacz hello [stoczni partii](https://github.com/Azure/batch-shipyard/) przepisami.
