---
title: "aaaConfigure wielościeżkowego We/Wy na hoście z systemem StorSimple Linux | Dokumentacja firmy Microsoft"
description: "Konfigurowanie wielościeżkowego wejścia/wyjścia na hoście z systemem Linux tooa StorSimple połączone systemem CentOS 6.6"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: tysonn
ms.assetid: ca289eed-12b7-4e2e-9117-adf7e2034f2f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: alkohli
ms.openlocfilehash: d9f7e02903243494c909313fb2c33ac690764274
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a><span data-ttu-id="673b4-103">Konfigurowanie wielościeżkowego wejścia/wyjścia na hoście StorSimple z systemem CentOS</span><span class="sxs-lookup"><span data-stu-id="673b4-103">Configure MPIO on a StorSimple host running CentOS</span></span>
<span data-ttu-id="673b4-104">W tym artykule opisano hello kroki wymagane tooconfigure Wielościeżkowe We/Wy (MPIO) na serwerze hosta Centos 6.6.</span><span class="sxs-lookup"><span data-stu-id="673b4-104">This article explains hello steps required tooconfigure Multipathing IO (MPIO) on your Centos 6.6 host server.</span></span> <span data-ttu-id="673b4-105">serwer hosta Hello jest tooyour podłączonego urządzenia Microsoft Azure StorSimple wysokiej dostępności za pośrednictwem inicjatorów iSCSI.</span><span class="sxs-lookup"><span data-stu-id="673b4-105">hello host server is connected tooyour Microsoft Azure StorSimple device for high availability via iSCSI initiators.</span></span> <span data-ttu-id="673b4-106">Opisuje w szczegółów hello automatycznego odnajdywania urządzeń wielościeżkowego i hello określonych ustawień tylko dla woluminów StorSimple.</span><span class="sxs-lookup"><span data-stu-id="673b4-106">It describes in detail hello automatic discovery of multipath devices and hello specific setup only for StorSimple volumes.</span></span>

<span data-ttu-id="673b4-107">Ta procedura jest modeli hello tooall dotyczy urządzeń z serii StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="673b4-107">This procedure is applicable tooall hello models of StorSimple 8000 series devices.</span></span>

> [!NOTE]
> <span data-ttu-id="673b4-108">Nie można użyć tej procedury dla urządzenia wirtualnego StorSimple.</span><span class="sxs-lookup"><span data-stu-id="673b4-108">This procedure cannot be used for a StorSimple virtual device.</span></span> <span data-ttu-id="673b4-109">Aby uzyskać więcej informacji zobacz temat jak tooconfigure obsługiwać serwery dla urządzenia wirtualnego.</span><span class="sxs-lookup"><span data-stu-id="673b4-109">For more information, see how tooconfigure host servers for your virtual device.</span></span>
> 
> 

## <a name="about-multipathing"></a><span data-ttu-id="673b4-110">O wiele ścieżek</span><span class="sxs-lookup"><span data-stu-id="673b4-110">About multipathing</span></span>
<span data-ttu-id="673b4-111">Funkcja wielu ścieżek Hello umożliwia tooconfigure wiele ścieżek wejścia/wyjścia między serwerem hosta a urządzeniem magazynującym.</span><span class="sxs-lookup"><span data-stu-id="673b4-111">hello multipathing feature allows you tooconfigure multiple I/O paths between a host server and a storage device.</span></span> <span data-ttu-id="673b4-112">Te ścieżki We/Wy są fizycznych połączeń sieci SAN, które mogą zawierać osobne kable, przełączniki interfejsów sieciowych i kontrolerów.</span><span class="sxs-lookup"><span data-stu-id="673b4-112">These I/O paths are physical SAN connections that can include separate cables, switches, network interfaces, and controllers.</span></span> <span data-ttu-id="673b4-113">Wiele ścieżek agreguje hello ścieżek wejścia/wyjścia, tooconfigure nowe urządzenie, którego jest skojarzony z wszystkich ścieżek hello agregowane.</span><span class="sxs-lookup"><span data-stu-id="673b4-113">Multipathing aggregates hello I/O paths, tooconfigure a new device that is associated with all of hello aggregated paths.</span></span>

<span data-ttu-id="673b4-114">Celem Hello wielu ścieżek jest dwukrotne:</span><span class="sxs-lookup"><span data-stu-id="673b4-114">hello purpose of multipathing is two-fold:</span></span>

* <span data-ttu-id="673b4-115">**Wysoka dostępność**: zapewnia alternatywną ścieżkę, jeśli dowolny element ścieżki hello we/wy (takie jak kabel, przełącznika, interfejsu sieciowego lub kontrolera) zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="673b4-115">**High availability**: It provides an alternate path if any element of hello I/O path (such as a cable, switch, network interface, or controller) fails.</span></span>
* <span data-ttu-id="673b4-116">**Równoważenie obciążenia**: w zależności od konfiguracji hello urządzenia magazynującego, go poprawić wydajność hello przez wykrycie obciążenia w ścieżkach hello We/Wy i dynamicznie ponowne równoważenie obciążenia tych.</span><span class="sxs-lookup"><span data-stu-id="673b4-116">**Load balancing**: Depending on hello configuration of your storage device, it can improve hello performance by detecting loads on hello I/O paths and dynamically rebalancing those loads.</span></span>

### <a name="about-multipathing-components"></a><span data-ttu-id="673b4-117">O wiele ścieżek składników</span><span class="sxs-lookup"><span data-stu-id="673b4-117">About multipathing components</span></span>
<span data-ttu-id="673b4-118">Wiele ścieżek w systemie Linux zawiera składniki jądra i przestrzeń użytkownika jak przedstawione w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="673b4-118">Multipathing in Linux consists of kernel components and user-space components as tabulated below.</span></span>

* <span data-ttu-id="673b4-119">**Jądra**: główny składnik hello jest hello *mapowania urządzenia* zmienia trasę We/Wy i obsługuje tryb failover dla ścieżki i grup ścieżki.</span><span class="sxs-lookup"><span data-stu-id="673b4-119">**Kernel**: hello main component is hello *device-mapper* that reroutes I/O and supports failover for paths and path groups.</span></span>

* <span data-ttu-id="673b4-120">**Przestrzeń użytkownika**: są to *narzędzia wielościeżkowego* który zarządzania multipathed urządzeniami przez poinstruowanie wielościeżkowe moduł mapowania urządzenia hello jakie toodo.</span><span class="sxs-lookup"><span data-stu-id="673b4-120">**User-space**: These are *multipath-tools* that manage multipathed devices by instructing hello device-mapper multipath module what toodo.</span></span> <span data-ttu-id="673b4-121">narzędzia Hello obejmują:</span><span class="sxs-lookup"><span data-stu-id="673b4-121">hello tools consist of:</span></span>
   
   * <span data-ttu-id="673b4-122">**Wielościeżkowe**: zawiera listę i konfiguruje multipathed urządzenia.</span><span class="sxs-lookup"><span data-stu-id="673b4-122">**Multipath**: lists and configures multipathed devices.</span></span>
   * <span data-ttu-id="673b4-123">**Multipathd**: demon wykonujący ścieżki hello wielościeżkowego i monitory.</span><span class="sxs-lookup"><span data-stu-id="673b4-123">**Multipathd**: daemon that executes multipath and monitors hello paths.</span></span>
   * <span data-ttu-id="673b4-124">**Nazwa Devmap**: devmaps zapewnia łatwy do rozpoznania tooudev nazwy urządzenia.</span><span class="sxs-lookup"><span data-stu-id="673b4-124">**Devmap-name**: provides a meaningful device-name tooudev for devmaps.</span></span>
   * <span data-ttu-id="673b4-125">**Kpartx**: mapuje liniowej devmaps toodevice partycje toomake wielościeżkowe mapy partitionable.</span><span class="sxs-lookup"><span data-stu-id="673b4-125">**Kpartx**: maps linear devmaps toodevice partitions toomake multipath maps partitionable.</span></span>
   * <span data-ttu-id="673b4-126">**MultiPath.conf**: plik konfiguracji wielościeżkowe demona, tabela wbudowanych konfiguracji hello toooverwrite używane.</span><span class="sxs-lookup"><span data-stu-id="673b4-126">**Multipath.conf**: configuration file for multipath daemon that is used toooverwrite hello built-in configuration table.</span></span>

### <a name="about-hello-multipathconf-configuration-file"></a><span data-ttu-id="673b4-127">Plik konfiguracji multipath.conf hello — informacje</span><span class="sxs-lookup"><span data-stu-id="673b4-127">About hello multipath.conf configuration file</span></span>
<span data-ttu-id="673b4-128">plik konfiguracji Hello `/etc/multipath.conf` sprawia, że wiele hello funkcji wielu ścieżek do skonfigurowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="673b4-128">hello configuration file `/etc/multipath.conf` makes many of hello multipathing features user-configurable.</span></span> <span data-ttu-id="673b4-129">Witaj `multipath` demon jądra polecenia i hello `multipathd` korzystać z informacji zamieszczonych w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="673b4-129">hello `multipath` command and hello kernel daemon `multipathd` use information found in this file.</span></span> <span data-ttu-id="673b4-130">Plik Hello konsultacji tylko podczas konfiguracji hello hello wielościeżkowe urządzeń.</span><span class="sxs-lookup"><span data-stu-id="673b4-130">hello file is consulted only during hello configuration of hello multipath devices.</span></span> <span data-ttu-id="673b4-131">Upewnij się, że wszystkie zmiany zostały wprowadzone, przed rozpoczęciem powitalne `multipath` polecenia.</span><span class="sxs-lookup"><span data-stu-id="673b4-131">Make sure that all changes are made before you run hello `multipath` command.</span></span> <span data-ttu-id="673b4-132">W przypadku zmodyfikowania pliku hello później, należy toostop a start multipathd ponownie dla efektu tootake zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="673b4-132">If you modify hello file afterwards, you will need toostop and start multipathd again for hello changes tootake effect.</span></span>

<span data-ttu-id="673b4-133">Witaj multipath.conf zawiera pięć sekcje:</span><span class="sxs-lookup"><span data-stu-id="673b4-133">hello multipath.conf has five sections:</span></span>

- <span data-ttu-id="673b4-134">**Poziomu domyślnych ustawień systemowych** *(wartość domyślna)*: można zastąpić poziomu ustawień domyślnych systemu.</span><span class="sxs-lookup"><span data-stu-id="673b4-134">**System level defaults** *(defaults)*: You can override system level defaults.</span></span>
- <span data-ttu-id="673b4-135">**Urządzenia na liście zabronionych numerów** *(czarna lista)*: można określić hello listę urządzeń, które nie powinny być kontrolowane na podstawie mapowania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="673b4-135">**Blacklisted devices** *(blacklist)*: You can specify hello list of devices that should not be controlled by device-mapper.</span></span>
- <span data-ttu-id="673b4-136">**Wyeliminować wyjątki** *(blacklist_exceptions)*: można zidentyfikować traktowane jako wielościeżkowe urządzeń, nawet wtedy, gdy na liście zabronionych hello toobe określonych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="673b4-136">**Blacklist exceptions** *(blacklist_exceptions)*: You can identify specific devices toobe treated as multipath devices even if listed in hello blacklist.</span></span>
- <span data-ttu-id="673b4-137">**Określone ustawienia kontrolera magazynu** *(urządzeń)*: można określić ustawienia konfiguracji, które mają być zastosowane toodevices, zainstalowanego dostawcy i informacje o produkcie.</span><span class="sxs-lookup"><span data-stu-id="673b4-137">**Storage controller specific settings** *(devices)*: You can specify configuration settings that will be applied toodevices that have Vendor and Product information.</span></span>
- <span data-ttu-id="673b4-138">**Określone ustawienia urządzenia** *(multipaths)*: ustawienia konfiguracji tej sekcji strojenia toofine hello można użyć dla poszczególnych jednostek LUN.</span><span class="sxs-lookup"><span data-stu-id="673b4-138">**Device specific settings** *(multipaths)*: You can use this section toofine-tune hello configuration settings for individual LUNs.</span></span>

## <a name="configure-multipathing-on-storsimple-connected-toolinux-host"></a><span data-ttu-id="673b4-139">Konfigurowanie wielu ścieżek na hoście połączonych tooLinux StorSimple</span><span class="sxs-lookup"><span data-stu-id="673b4-139">Configure multipathing on StorSimple connected tooLinux host</span></span>
<span data-ttu-id="673b4-140">Host Linux tooa podłączone urządzenia StorSimple można skonfigurować wysoką dostępność i równoważenie obciążenia.</span><span class="sxs-lookup"><span data-stu-id="673b4-140">A StorSimple device connected tooa Linux host can be configured for high availability and load balancing.</span></span> <span data-ttu-id="673b4-141">Na przykład jeśli hello Linux host ma dwa interfejsy toohello połączonych sieci SAN i hello urządzenie ma dwa interfejsy podłączone toohello SAN hello takie, które te interfejsy są w tej samej podsieci, a następnie będzie 4 ścieżki dostępna.</span><span class="sxs-lookup"><span data-stu-id="673b4-141">For example, if hello Linux host has two interfaces connected toohello SAN and hello device has two interfaces connected toohello SAN such that these interfaces are on hello same subnet, then there will be 4 paths available.</span></span> <span data-ttu-id="673b4-142">Jednak jeśli każdy interfejs danych w interfejsie hello urządzenia i hosta w innej podsieci IP (i nie wzajemnie obsługują routing), to tylko 2 ścieżki będą dostępne.</span><span class="sxs-lookup"><span data-stu-id="673b4-142">However, if each DATA interface on hello device and host interface are on a different IP subnet (and not routable), then only 2 paths will be available.</span></span> <span data-ttu-id="673b4-143">Można skonfigurować wiele ścieżek tooautomatically odnajdywanie wszystkich ścieżek dostępnych hello, wybrać algorytm równoważenia obciążenia dla tych ścieżek, zastosowania określonych ustawień konfiguracyjnych dla woluminów tylko StorSimple, włączyć i sprawdź wielu ścieżek.</span><span class="sxs-lookup"><span data-stu-id="673b4-143">You can configure multipathing tooautomatically discover all hello available paths, choose a load-balancing algorithm for those paths, apply specific configuration settings for StorSimple-only volumes, and then enable and verify multipathing.</span></span>

<span data-ttu-id="673b4-144">Witaj poniższej procedury opisano tooconfigure wielu ścieżek, gdy urządzenie StorSimple z dwoma interfejsami sieciowymi hosta tooa połączonych z dwoma interfejsami sieciowymi.</span><span class="sxs-lookup"><span data-stu-id="673b4-144">hello following procedure describes how tooconfigure multipathing when a StorSimple device with two network interfaces is connected tooa host with two network interfaces.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="673b4-145">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="673b4-145">Prerequisites</span></span>
<span data-ttu-id="673b4-146">Ta sekcja zawiera szczegóły dotyczące wymagań wstępnych dotyczących CentOS serwera oraz urządzenia StorSimple hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="673b4-146">This section details hello configuration prerequisites for CentOS server and your StorSimple device.</span></span>

### <a name="on-centos-host"></a><span data-ttu-id="673b4-147">Na hoście CentOS</span><span class="sxs-lookup"><span data-stu-id="673b4-147">On CentOS host</span></span>
1. <span data-ttu-id="673b4-148">Upewnij się, że na hoście CentOS ma włączone 2 interfejsów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="673b4-148">Make sure that your CentOS host has 2 network interfaces enabled.</span></span> <span data-ttu-id="673b4-149">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="673b4-149">Type:</span></span>
   
    `ifconfig`
   
    <span data-ttu-id="673b4-150">Witaj poniższy przykład przedstawia dane wyjściowe powitania po dwa interfejsy sieciowe (`eth0` i `eth1`) znajdują się na hoście hello.</span><span class="sxs-lookup"><span data-stu-id="673b4-150">hello following example shows hello output when two network interfaces (`eth0` and `eth1`) are present on hello host.</span></span>
   
        [root@centosSS ~]# ifconfig
        eth0  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:41  
          inet addr:10.126.162.65  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3341/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3341/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
         RX packets:36536 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6312 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:13994127 (13.3 MiB)  TX bytes:645654 (630.5 KiB)
   
        eth1  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:42  
          inet addr:10.126.162.66  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3342/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3342/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:25962 errors:0 dropped:0 overruns:0 frame:0
          TX packets:11 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:2597350 (2.4 MiB)  TX bytes:754 (754.0 b)
   
        loLink encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:12 errors:0 dropped:0 overruns:0 frame:0
          TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:720 (720.0 b)  TX bytes:720 (720.0 b)
2. <span data-ttu-id="673b4-151">Zainstaluj *iSCSI inicjatora witryny* na serwerze CentOS.</span><span class="sxs-lookup"><span data-stu-id="673b4-151">Install *iSCSI-initiator-utils* on your CentOS server.</span></span> <span data-ttu-id="673b4-152">Wykonaj następujące kroki tooinstall hello *iSCSI inicjatora witryny*.</span><span class="sxs-lookup"><span data-stu-id="673b4-152">Perform hello following steps tooinstall *iSCSI-initiator-utils*.</span></span>
   
   1. <span data-ttu-id="673b4-153">Zaloguj się jako `root` do hosta CentOS.</span><span class="sxs-lookup"><span data-stu-id="673b4-153">Log on as `root` into your CentOS host.</span></span>
   2. <span data-ttu-id="673b4-154">Zainstaluj hello *iSCSI inicjatora witryny*.</span><span class="sxs-lookup"><span data-stu-id="673b4-154">Install hello *iSCSI-initiator-utils*.</span></span> <span data-ttu-id="673b4-155">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="673b4-155">Type:</span></span>
      
       `yum install iscsi-initiator-utils`
   3. <span data-ttu-id="673b4-156">Po hello *iSCSI inicjatora witryny* jest poprawnie zainstalowany, uruchomienie usługi iSCSI hello.</span><span class="sxs-lookup"><span data-stu-id="673b4-156">After hello *iSCSI-Initiator-utils* is successfully installed, start hello iSCSI service.</span></span> <span data-ttu-id="673b4-157">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="673b4-157">Type:</span></span>
      
       `service iscsid start`
      
       <span data-ttu-id="673b4-158">W przypadkach `iscsid` faktycznie nie może uruchomić i hello `--force` opcji mogą być potrzebne.</span><span class="sxs-lookup"><span data-stu-id="673b4-158">On occasions, `iscsid` may not actually start and hello `--force` option may be needed</span></span>
   4. <span data-ttu-id="673b4-159">Włączenie z inicjatora iSCSI w czasie rozruchu, użyj hello tooensure `chkconfig` polecenia tooenable hello usługi.</span><span class="sxs-lookup"><span data-stu-id="673b4-159">tooensure that your iSCSI initiator is enabled during boot time, use hello `chkconfig` command tooenable hello service.</span></span>
      
       `chkconfig iscsi on`
   5. <span data-ttu-id="673b4-160">tooverify, która została prawidłowo Instalatora, uruchom polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="673b4-160">tooverify that that it was properly setup, run hello command:</span></span>
      
       `chkconfig --list | grep iscsi`
      
       <span data-ttu-id="673b4-161">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="673b4-161">A sample output is shown below.</span></span>
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       <span data-ttu-id="673b4-162">Z hello powyżej przykładzie widać, że środowisko iSCSI uruchomi w czasie rozruchu wykonywania poziomu 2, 3, 4 i 5.</span><span class="sxs-lookup"><span data-stu-id="673b4-162">From hello above example, you can see that your iSCSI environment will run on boot time on run levels 2, 3, 4, and 5.</span></span>
3. <span data-ttu-id="673b4-163">Zainstaluj *urządzenia mapowania wielościeżkowego*.</span><span class="sxs-lookup"><span data-stu-id="673b4-163">Install *device-mapper-multipath*.</span></span> <span data-ttu-id="673b4-164">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="673b4-164">Type:</span></span>
   
    `yum install device-mapper-multipath`
   
    <span data-ttu-id="673b4-165">Witaj, instalacja rozpocznie się.</span><span class="sxs-lookup"><span data-stu-id="673b4-165">hello installation will start.</span></span> <span data-ttu-id="673b4-166">Typ **Y** toocontinue po wyświetleniu monitu o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="673b4-166">Type **Y** toocontinue when prompted for confirmation.</span></span>

### <a name="on-storsimple-device"></a><span data-ttu-id="673b4-167">Na urządzeniu StorSimple</span><span class="sxs-lookup"><span data-stu-id="673b4-167">On StorSimple device</span></span>
<span data-ttu-id="673b4-168">Urządzenia StorSimple powinny mieć:</span><span class="sxs-lookup"><span data-stu-id="673b4-168">Your StorSimple device should have:</span></span>

* <span data-ttu-id="673b4-169">Co najmniej dwa interfejsy włączone dla interfejsu iSCSI.</span><span class="sxs-lookup"><span data-stu-id="673b4-169">A minimum of two interfaces enabled for iSCSI.</span></span> <span data-ttu-id="673b4-170">tooverify, że dwa interfejsy są włączone iSCSI na urządzeniu StorSimple, wykonaj następujące kroki w portalu klasycznego Azure dla urządzenia StorSimple hello hello:</span><span class="sxs-lookup"><span data-stu-id="673b4-170">tooverify that two interfaces are iSCSI-enabled on your StorSimple device, perform hello following steps in hello Azure classic portal for your StorSimple device:</span></span>
  
  1. <span data-ttu-id="673b4-171">Zaloguj się do klasycznego portalu powitania dla urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="673b4-171">Log into hello classic portal for your StorSimple device.</span></span>
  2. <span data-ttu-id="673b4-172">Wybierz usługę Menedżer StorSimple, kliknij przycisk **urządzeń** i wybierz polecenie hello określonego urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="673b4-172">Select your StorSimple Manager service, click **Devices** and choose hello specific StorSimple device.</span></span> <span data-ttu-id="673b4-173">Kliknij przycisk **Konfiguruj** i sprawdź ustawienia interfejsu sieciowego hello.</span><span class="sxs-lookup"><span data-stu-id="673b4-173">Click **Configure** and verify hello network interface settings.</span></span> <span data-ttu-id="673b4-174">Poniżej przedstawiono zrzut ekranu z dwa interfejsy sieci iSCSI.</span><span class="sxs-lookup"><span data-stu-id="673b4-174">A screenshot with two iSCSI-enabled network interfaces is shown below.</span></span> <span data-ttu-id="673b4-175">Tutaj dane 2 i dane 3, zarówno 10 GbE interfejsy są włączone dla interfejsu iSCSI.</span><span class="sxs-lookup"><span data-stu-id="673b4-175">Here DATA 2 and DATA 3, both 10 GbE interfaces are enabled for iSCSI.</span></span>
     
      ![Konfiguracja MPIO StorsSimple dane 2](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![Wielościeżkowe wejście/wyjście StorSimple dane 3 konfiguracji](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      <span data-ttu-id="673b4-178">W hello **Konfiguruj** strony</span><span class="sxs-lookup"><span data-stu-id="673b4-178">In hello **Configure** page</span></span>
     
     1. <span data-ttu-id="673b4-179">Upewnij się, że oba interfejsy sieciowe są włączone iSCSI.</span><span class="sxs-lookup"><span data-stu-id="673b4-179">Ensure that both network interfaces are iSCSI-enabled.</span></span> <span data-ttu-id="673b4-180">Witaj **iSCSI włączone** pola powinna być ustawiona zbyt**tak**.</span><span class="sxs-lookup"><span data-stu-id="673b4-180">hello **iSCSI enabled** field should be set too**Yes**.</span></span>
     2. <span data-ttu-id="673b4-181">Sprawdź, czy hello interfejsy sieciowe mają hello samej szybkości, powinny być 1 GbE lub 10 GbE.</span><span class="sxs-lookup"><span data-stu-id="673b4-181">Ensure that hello network interfaces have hello same speed, both should be 1 GbE or 10 GbE.</span></span>
     3. <span data-ttu-id="673b4-182">Należy pamiętać, adresy hello IPv4 hello włączono interfejs iSCSI interfejsów i Zapisz do późniejszego użytku na hoście hello.</span><span class="sxs-lookup"><span data-stu-id="673b4-182">Note hello IPv4 addresses of hello iSCSI-enabled interfaces and save for later use on hello host.</span></span>
* <span data-ttu-id="673b4-183">interfejsy iSCSI Hello na urządzeniu StorSimple powinny być dostępne z hello CentOS serwera.</span><span class="sxs-lookup"><span data-stu-id="673b4-183">hello iSCSI interfaces on your StorSimple device should be reachable from hello CentOS server.</span></span>
      <span data-ttu-id="673b4-184">tooverify, należy tooprovide hello adresy IP interfejsów sieci iSCSI StorSimple na serwerze hosta.</span><span class="sxs-lookup"><span data-stu-id="673b4-184">tooverify this, you need tooprovide hello IP addresses of your StorSimple iSCSI-enabled network interfaces on your host server.</span></span> <span data-ttu-id="673b4-185">Witaj polecenia używane i hello odpowiednie dane wyjściowe z dane2 (10.126.162.25) i DATA3 (10.126.162.26) są wyświetlane poniżej:</span><span class="sxs-lookup"><span data-stu-id="673b4-185">hello commands used and hello corresponding output with DATA2 (10.126.162.25) and DATA3 (10.126.162.26) is shown below:</span></span>
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a><span data-ttu-id="673b4-186">Konfiguracja sprzętu</span><span class="sxs-lookup"><span data-stu-id="673b4-186">Hardware configuration</span></span>
<span data-ttu-id="673b4-187">Zaleca się połączyć z hello dwa iSCSI interfejsy sieci na oddzielnych ścieżek nadmiarowości.</span><span class="sxs-lookup"><span data-stu-id="673b4-187">We recommend that you connect hello two iSCSI network interfaces on separate paths for redundancy.</span></span> <span data-ttu-id="673b4-188">na poniższym rysunku Hello przedstawiono hello zalecana konfiguracja sprzętu wysokiej dostępności i równoważenia obciążenia wielu ścieżek dla urządzenia StorSimple i CentOS serwera.</span><span class="sxs-lookup"><span data-stu-id="673b4-188">hello figure below shows hello recommended hardware configuration for high availability and load-balancing multipathing for your CentOS server and StorSimple device.</span></span>

![Konfiguracja sprzętowa wielościeżkowego wejścia/wyjścia dla hosta tooLinux StorSimple](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

<span data-ttu-id="673b4-190">Jak pokazano w powyższej ilustracji hello:</span><span class="sxs-lookup"><span data-stu-id="673b4-190">As shown in hello preceding figure:</span></span>

* <span data-ttu-id="673b4-191">Urządzenia StorSimple znajduje się w konfiguracji aktywny / pasywny z dwóch kontrolerów.</span><span class="sxs-lookup"><span data-stu-id="673b4-191">Your StorSimple device is in an active-passive configuration with two controllers.</span></span>
* <span data-ttu-id="673b4-192">Dwa przełączniki sieci SAN są kontrolery urządzeń podłączonych tooyour.</span><span class="sxs-lookup"><span data-stu-id="673b4-192">Two SAN switches are connected tooyour device controllers.</span></span>
* <span data-ttu-id="673b4-193">Dwa inicjatorów iSCSI są włączone na urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="673b4-193">Two iSCSI initiators are enabled on your StorSimple device.</span></span>
* <span data-ttu-id="673b4-194">Dwa interfejsy sieciowe są włączone na hoście CentOS.</span><span class="sxs-lookup"><span data-stu-id="673b4-194">Two network interfaces are enabled on your CentOS host.</span></span>

<span data-ttu-id="673b4-195">Hello powyżej konfiguracji umożliwia uzyskanie 4 osobnych ścieżek między urządzenia i hello hosta, jeśli hello danych hosta i interfejsy są wzajemnie obsługiwać Routing.</span><span class="sxs-lookup"><span data-stu-id="673b4-195">hello above configuration will yield 4 separate paths between your device and hello host if hello host and data interfaces are routable.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="673b4-196">Zaleca się, że niemieszanie 1 GbE i 10 GbE interfejsów sieciowych do obsługi wielu ścieżek.</span><span class="sxs-lookup"><span data-stu-id="673b4-196">We recommend that you do not mix 1 GbE and 10 GbE network interfaces for multipathing.</span></span> <span data-ttu-id="673b4-197">Korzystając z dwóch interfejsów sieciowych, dotyczą obu interfejsów hello powinna być typu identyczne hello.</span><span class="sxs-lookup"><span data-stu-id="673b4-197">When using two network interfaces, both hello interfaces should be hello identical type.</span></span>
> * <span data-ttu-id="673b4-198">Na urządzeniu StorSimple DATA0, dane1, DATA4 i DATA5 są 1 GbE interfejsy dane2 i DATA3 są 10 GbE interfejsów. |</span><span class="sxs-lookup"><span data-stu-id="673b4-198">On your StorSimple device, DATA0, DATA1, DATA4 and DATA5 are 1 GbE interfaces whereas DATA2 and DATA3 are 10 GbE network interfaces.|</span></span>
> 
> 

## <a name="configuration-steps"></a><span data-ttu-id="673b4-199">Kroki konfiguracji</span><span class="sxs-lookup"><span data-stu-id="673b4-199">Configuration steps</span></span>
<span data-ttu-id="673b4-200">kroki konfiguracji Hello wielu ścieżek obejmują konfigurowanie hello dostępnych ścieżek automatycznego wykrywania, określając hello równoważenia obciążenia algorytmu toouse, włączanie wielu ścieżek i na koniec Weryfikowanie konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="673b4-200">hello configuration steps for multipathing involve configuring hello available paths for automatic discovery, specifying hello load-balancing algorithm toouse, enabling multipathing and finally verifying hello configuration.</span></span> <span data-ttu-id="673b4-201">Każdy z tych kroków omówiono szczegółowo w hello następujące sekcje.</span><span class="sxs-lookup"><span data-stu-id="673b4-201">Each of these steps is discussed in detail in hello following sections.</span></span>

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a><span data-ttu-id="673b4-202">Krok 1: Konfigurowanie wielu ścieżek automatycznego wykrywania</span><span class="sxs-lookup"><span data-stu-id="673b4-202">Step 1: Configure multipathing for automatic discovery</span></span>
<span data-ttu-id="673b4-203">automatycznie odnalezione urządzenia obsługiwane wielościeżkowe Hello i skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="673b4-203">hello multipath-supported devices can be automatically discovered and configured.</span></span>

1. <span data-ttu-id="673b4-204">Inicjowanie `/etc/multipath.conf` pliku.</span><span class="sxs-lookup"><span data-stu-id="673b4-204">Initialize `/etc/multipath.conf` file.</span></span> <span data-ttu-id="673b4-205">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="673b4-205">Type:</span></span>
   
     `mpathconf --enable`
   
    <span data-ttu-id="673b4-206">utworzy Hello powyżej polecenie `sample/etc/multipath.conf` pliku.</span><span class="sxs-lookup"><span data-stu-id="673b4-206">hello above command will create a `sample/etc/multipath.conf` file.</span></span>
2. <span data-ttu-id="673b4-207">Uruchom usługę wielu ścieżek.</span><span class="sxs-lookup"><span data-stu-id="673b4-207">Start multipath service.</span></span> <span data-ttu-id="673b4-208">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="673b4-208">Type:</span></span>
   
    `service multipathd start`
   
    <span data-ttu-id="673b4-209">Zostanie wyświetlony hello następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="673b4-209">You will see hello following output:</span></span>
   
    `Starting multipathd daemon:`
3. <span data-ttu-id="673b4-210">Włącz automatyczne odnajdowanie multipaths.</span><span class="sxs-lookup"><span data-stu-id="673b4-210">Enable automatic discovery of multipaths.</span></span> <span data-ttu-id="673b4-211">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="673b4-211">Type:</span></span>
   
    `mpathconf --find_multipaths y`
   
    <span data-ttu-id="673b4-212">Spowoduje to zmodyfikowanie hello wartości domyślne sekcji z `multipath.conf` w sposób przedstawiony poniżej:</span><span class="sxs-lookup"><span data-stu-id="673b4-212">This will modify hello defaults section of your `multipath.conf` as shown below:</span></span>
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a><span data-ttu-id="673b4-213">Krok 2: Konfigurowanie wielu ścieżek dla woluminów StorSimple</span><span class="sxs-lookup"><span data-stu-id="673b4-213">Step 2: Configure multipathing for StorSimple volumes</span></span>
<span data-ttu-id="673b4-214">Domyślnie wszystkie urządzenia są czarny wymienione w pliku multipath.conf hello i będą pomijane.</span><span class="sxs-lookup"><span data-stu-id="673b4-214">By default, all devices are black listed in hello multipath.conf file and will be bypassed.</span></span> <span data-ttu-id="673b4-215">Należy toocreate zabronionych wyjątki tooallow w wielu ścieżek dla woluminów z urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="673b4-215">You will need toocreate blacklist exceptions tooallow multipathing for volumes from StorSimple devices.</span></span>

1. <span data-ttu-id="673b4-216">Edytuj hello `/etc/mulitpath.conf` pliku.</span><span class="sxs-lookup"><span data-stu-id="673b4-216">Edit hello `/etc/mulitpath.conf` file.</span></span> <span data-ttu-id="673b4-217">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="673b4-217">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="673b4-218">Zlokalizuj hello blacklist_exceptions sekcji w pliku multipath.conf hello.</span><span class="sxs-lookup"><span data-stu-id="673b4-218">Locate hello blacklist_exceptions section in hello multipath.conf file.</span></span> <span data-ttu-id="673b4-219">Urządzenia StorSimple musi toobe wymienione jako wyjątek zabronionych w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="673b4-219">Your StorSimple device needs toobe listed as a blacklist exception in this section.</span></span> <span data-ttu-id="673b4-220">Użytkownik może usuń znaczniki komentarza odpowiednich wierszy w tym toomodify pliku go w sposób przedstawiony poniżej (używana tylko hello określonego modelu hello urządzenia, które są używane):</span><span class="sxs-lookup"><span data-stu-id="673b4-220">You can uncomment relevant lines in this file toomodify it as shown below (use only hello specific model of hello device you are using):</span></span>
   
        blacklist_exceptions {
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8100*"
            }
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8600*"
            }
           }

### <a name="step-3-configure-round-robin-multipathing"></a><span data-ttu-id="673b4-221">Krok 3: Konfigurowanie wielu ścieżek okrężnego</span><span class="sxs-lookup"><span data-stu-id="673b4-221">Step 3: Configure round-robin multipathing</span></span>
<span data-ttu-id="673b4-222">Ten algorytm równoważenia obciążenia używa wszystkich kontrolera active dostępne toohello multipaths hello w sposób zrównoważony, okrężnego.</span><span class="sxs-lookup"><span data-stu-id="673b4-222">This load-balancing algorithm uses all hello available multipaths toohello active controller in a balanced, round-robin fashion.</span></span>

1. <span data-ttu-id="673b4-223">Edytuj hello `/etc/multipath.conf` pliku.</span><span class="sxs-lookup"><span data-stu-id="673b4-223">Edit hello `/etc/multipath.conf` file.</span></span> <span data-ttu-id="673b4-224">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="673b4-224">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="673b4-225">W obszarze hello `defaults` sekcji, ustaw hello `path_grouping_policy` zbyt`multibus`.</span><span class="sxs-lookup"><span data-stu-id="673b4-225">Under hello `defaults` section, set hello `path_grouping_policy` too`multibus`.</span></span> <span data-ttu-id="673b4-226">Witaj `path_grouping_policy` określa hello domyślna ścieżka grupowanie zasady tooapply toounspecified multipaths.</span><span class="sxs-lookup"><span data-stu-id="673b4-226">hello `path_grouping_policy` specifies hello default path grouping policy tooapply toounspecified multipaths.</span></span> <span data-ttu-id="673b4-227">Witaj wartości domyślne sekcji będzie wyglądać jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="673b4-227">hello defaults section will look as shown below.</span></span>
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> <span data-ttu-id="673b4-228">Witaj najbardziej typowe wartości `path_grouping_policy` obejmują:</span><span class="sxs-lookup"><span data-stu-id="673b4-228">hello most common values of `path_grouping_policy` include:</span></span>
> 
> * <span data-ttu-id="673b4-229">tryb failover = 1 ścieżka według priorytetu grupy</span><span class="sxs-lookup"><span data-stu-id="673b4-229">failover = 1 path per priority group</span></span>
> * <span data-ttu-id="673b4-230">multibus = wszystkie prawidłowe ścieżki w grupie o priorytecie 1</span><span class="sxs-lookup"><span data-stu-id="673b4-230">multibus = all valid paths in 1 priority group</span></span>
> 
> 

### <a name="step-4-enable-multipathing"></a><span data-ttu-id="673b4-231">Krok 4: Włącz wielościeżkowe</span><span class="sxs-lookup"><span data-stu-id="673b4-231">Step 4: Enable multipathing</span></span>
1. <span data-ttu-id="673b4-232">Uruchom ponownie hello `multipathd` demon.</span><span class="sxs-lookup"><span data-stu-id="673b4-232">Restart hello `multipathd` daemon.</span></span> <span data-ttu-id="673b4-233">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="673b4-233">Type:</span></span>
   
    `service multipathd restart`
2. <span data-ttu-id="673b4-234">Witaj dane wyjściowe będą mieć, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="673b4-234">hello output will be as shown below:</span></span>
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a><span data-ttu-id="673b4-235">Krok 5: Sprawdzanie wielu ścieżek</span><span class="sxs-lookup"><span data-stu-id="673b4-235">Step 5: Verify multipathing</span></span>
1. <span data-ttu-id="673b4-236">Najpierw upewnij się, że iSCSI jest nawiązywane połączenie z urządzenia StorSimple hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="673b4-236">First make sure that iSCSI connection is established with hello StorSimple device as follows:</span></span>
   
   <span data-ttu-id="673b4-237">a.</span><span class="sxs-lookup"><span data-stu-id="673b4-237">a.</span></span> <span data-ttu-id="673b4-238">Odnajdywanie urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="673b4-238">Discover your StorSimple device.</span></span> <span data-ttu-id="673b4-239">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="673b4-239">Type:</span></span>
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on hello device>:<iSCSI port on StorSimple device>
    ```
    
    <span data-ttu-id="673b4-240">wynik Hello, gdy adres IP dla DATA0 jest 10.126.162.25 i jest otwarty port 3260, na urządzeniu StorSimple powitania dla ruchu wychodzącego iSCSI jest w sposób przedstawiony poniżej:</span><span class="sxs-lookup"><span data-stu-id="673b4-240">hello output when IP address for DATA0 is 10.126.162.25 and port 3260 is opened on hello StorSimple device for outbound iSCSI traffic is as shown below:</span></span>
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    <span data-ttu-id="673b4-241">Kopiuj hello IQN urządzenia StorSimple `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, z hello poprzedzających danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="673b4-241">Copy hello IQN of your StorSimple device, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, from hello preceding output.</span></span>

   <span data-ttu-id="673b4-242">b.</span><span class="sxs-lookup"><span data-stu-id="673b4-242">b.</span></span> <span data-ttu-id="673b4-243">Podłącz urządzenie toohello przy użyciu docelowego IQN.</span><span class="sxs-lookup"><span data-stu-id="673b4-243">Connect toohello device using target IQN.</span></span> <span data-ttu-id="673b4-244">urządzenie StorSimple Hello jest hello obiektu docelowego iSCSI w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="673b4-244">hello StorSimple device is hello iSCSI target here.</span></span> <span data-ttu-id="673b4-245">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="673b4-245">Type:</span></span>

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    <span data-ttu-id="673b4-246">Witaj poniższy przykład przedstawia dane wyjściowe z elementem docelowym IQN z `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span><span class="sxs-lookup"><span data-stu-id="673b4-246">hello following example shows output with a target IQN of `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span></span> <span data-ttu-id="673b4-247">dane wyjściowe Hello wskazuje pomyślnego połączenia toohello dwa interfejsy sieci iSCSI na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="673b4-247">hello output indicates that you have successfully connected toohello two iSCSI-enabled network interfaces on your device.</span></span>

    ```
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    <span data-ttu-id="673b4-248">Jeśli zostanie wyświetlony interfejs tylko jednego hosta i dwóch ścieżek, następnie należy tooenable obu interfejsów hello na hoście dla interfejsu iSCSI.</span><span class="sxs-lookup"><span data-stu-id="673b4-248">If you see only one host interface and two paths here, then you need tooenable both hello interfaces on host for iSCSI.</span></span> <span data-ttu-id="673b4-249">Możesz wykonać hello [szczegółowe instrukcje w dokumentacji systemu Linux](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span><span class="sxs-lookup"><span data-stu-id="673b4-249">You can follow hello [detailed instructions in Linux documentation](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span></span>

2. <span data-ttu-id="673b4-250">Wolumin jest narażonych toohello CentOS serwera z hello urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="673b4-250">A volume is exposed toohello CentOS server from hello StorSimple device.</span></span> <span data-ttu-id="673b4-251">Aby uzyskać więcej informacji, zobacz [krok 6: Tworzenie woluminu](storsimple-deployment-walkthrough.md#step-6-create-a-volume) za pośrednictwem hello klasycznego portalu Azure w urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="673b4-251">For more information, see [Step 6: Create a volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) via hello Azure classic portal on your StorSimple device.</span></span>

3. <span data-ttu-id="673b4-252">Sprawdź hello dostępnych ścieżek.</span><span class="sxs-lookup"><span data-stu-id="673b4-252">Verify hello available paths.</span></span> <span data-ttu-id="673b4-253">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="673b4-253">Type:</span></span>

      ```
      multipath –l
      ```

      <span data-ttu-id="673b4-254">Poniższy przykład Hello przedstawiono dane hello dwa interfejsy sieci w interfejsie sieciowym pojedynczy host tooa podłączonego urządzenia StorSimple z dwóch ścieżek dostępne.</span><span class="sxs-lookup"><span data-stu-id="673b4-254">hello following example shows hello output for two network interfaces on a StorSimple device connected tooa single host network interface with two available paths.</span></span>

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        hello following example shows hello output for two network interfaces on a StorSimple device connected tootwo host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After hello paths are configured, refer toohello specific instructions on your host operating system (Centos 6.6) toomount and format this volume.

## <a name="troubleshoot-multipathing"></a><span data-ttu-id="673b4-255">Rozwiązywanie problemów z wielu ścieżek</span><span class="sxs-lookup"><span data-stu-id="673b4-255">Troubleshoot multipathing</span></span>
<span data-ttu-id="673b4-256">Ta sekcja zawiera wskazówki przydatne, jeśli wystąpiły problemy podczas konfigurowania wielu ścieżek.</span><span class="sxs-lookup"><span data-stu-id="673b4-256">This section provides some helpful tips if you run into any issues during multipathing configuration.</span></span>

<span data-ttu-id="673b4-257">Q.</span><span class="sxs-lookup"><span data-stu-id="673b4-257">Q.</span></span> <span data-ttu-id="673b4-258">Nie ma zmiany hello `multipath.conf` pliku wpływają.</span><span class="sxs-lookup"><span data-stu-id="673b4-258">I do not see hello changes in `multipath.conf` file taking effect.</span></span>

<span data-ttu-id="673b4-259">A.</span><span class="sxs-lookup"><span data-stu-id="673b4-259">A.</span></span> <span data-ttu-id="673b4-260">Jeśli wprowadzono żadnych zmian toohello `multipath.conf` plik, trzeba będzie toorestart hello wielu ścieżek usługi.</span><span class="sxs-lookup"><span data-stu-id="673b4-260">If you have made any changes toohello `multipath.conf` file, you will need toorestart hello multipathing service.</span></span> <span data-ttu-id="673b4-261">Wpisz następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="673b4-261">Type hello following command:</span></span>

    service multipathd restart

<span data-ttu-id="673b4-262">Q.</span><span class="sxs-lookup"><span data-stu-id="673b4-262">Q.</span></span> <span data-ttu-id="673b4-263">Dwa interfejsy sieci na urządzeniu StorSimple hello i dwa interfejsy sieciowe na hoście hello został włączony.</span><span class="sxs-lookup"><span data-stu-id="673b4-263">I have enabled two network interfaces on hello StorSimple device and two network interfaces on hello host.</span></span> <span data-ttu-id="673b4-264">Podczas wyświetlania dostępnych ścieżek hello są widoczne tylko dwie ścieżki.</span><span class="sxs-lookup"><span data-stu-id="673b4-264">When I list hello available paths, I see only two paths.</span></span> <span data-ttu-id="673b4-265">Oczekiwana toosee czterech dostępnych ścieżek.</span><span class="sxs-lookup"><span data-stu-id="673b4-265">I expected toosee four available paths.</span></span>

<span data-ttu-id="673b4-266">A.</span><span class="sxs-lookup"><span data-stu-id="673b4-266">A.</span></span> <span data-ttu-id="673b4-267">Upewnij się, że Witaj dwie ścieżki są na powitania tej samej podsieci i wzajemnie obsługują routing.</span><span class="sxs-lookup"><span data-stu-id="673b4-267">Make sure that hello two paths are on hello same subnet and routable.</span></span> <span data-ttu-id="673b4-268">Jeśli interfejsy sieciowe hello znajdują się na różnych sieci VLAN, a nie obsługuje routingu, wyświetlona zostanie tylko dwie ścieżki.</span><span class="sxs-lookup"><span data-stu-id="673b4-268">If hello network interfaces are on different vLANs and not routable, you will see only two paths.</span></span> <span data-ttu-id="673b4-269">Jednym ze sposobów tooverify jest toomake się upewnić, że może nawiązać połączenie obu interfejsów hosta hello z karty sieciowej na urządzeniu StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="673b4-269">One way tooverify this is toomake sure that you can reach both hello host interfaces from a network interface on hello StorSimple device.</span></span> <span data-ttu-id="673b4-270">Konieczne będzie zbyt[skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) jako weryfikacji jest możliwe tylko za pośrednictwem sesji pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="673b4-270">You will need too[contact Microsoft Support](storsimple-contact-microsoft-support.md) as this verification can only be done via a support session.</span></span>

<span data-ttu-id="673b4-271">Q.</span><span class="sxs-lookup"><span data-stu-id="673b4-271">Q.</span></span> <span data-ttu-id="673b4-272">Podczas wyświetlania dostępnych ścieżek, nie ma żadnych danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="673b4-272">When I list available paths, I do not see any output.</span></span>

<span data-ttu-id="673b4-273">A.</span><span class="sxs-lookup"><span data-stu-id="673b4-273">A.</span></span> <span data-ttu-id="673b4-274">Zazwyczaj nie ma żadnych ścieżek multipathed sugeruje problem z hello demon wielu ścieżek, i jest to najprawdopodobniej wszelkie problemy w tym miejscu znajduje się w hello `multipath.conf` pliku.</span><span class="sxs-lookup"><span data-stu-id="673b4-274">Typically, not seeing any multipathed paths suggests a problem with hello multipathing daemon, and it’s most likely that any problem here lies in hello `multipath.conf` file.</span></span>

<span data-ttu-id="673b4-275">Byłoby warto sprawdzanie, czy rzeczywiście widać niektóre dyski po nawiązaniu połączenia z docelowym toohello jako odpowiedzi z listy wielościeżkowe hello może również oznaczać, że nie ma żadnych dysków.</span><span class="sxs-lookup"><span data-stu-id="673b4-275">It would also be worth checking that you can actually see some disks after connecting toohello target, as no response from hello multipath listings could also mean you don’t have any disks.</span></span>

* <span data-ttu-id="673b4-276">Użyj powitania po magistrali SCSI hello toorescan polecenia:</span><span class="sxs-lookup"><span data-stu-id="673b4-276">Use hello following command toorescan hello SCSI bus:</span></span>
  
    <span data-ttu-id="673b4-277">`$ rescan-scsi-bus.sh `(część pakietu sg3_utils)</span><span class="sxs-lookup"><span data-stu-id="673b4-277">`$ rescan-scsi-bus.sh `(part of sg3_utils package)</span></span>
* <span data-ttu-id="673b4-278">Wpisz następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="673b4-278">Type hello following commands:</span></span>
  
    `$ dmesg | grep sd*`
     
     <span data-ttu-id="673b4-279">Lub</span><span class="sxs-lookup"><span data-stu-id="673b4-279">Or</span></span>
  
    `$ fdisk –l`
  
    <span data-ttu-id="673b4-280">Te będą zwracane szczegóły ostatnio dodane dyski.</span><span class="sxs-lookup"><span data-stu-id="673b4-280">These will return details of recently added disks.</span></span>
* <span data-ttu-id="673b4-281">czy jest to dysk StorSimple toodetermine Użyj hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="673b4-281">toodetermine whether it is a StorSimple disk, use hello following commands:</span></span>
  
    `cat /sys/block/<DISK>/device/model`
  
    <span data-ttu-id="673b4-282">Zwraca ciąg, który określa, czy jest to dysk StorSimple.</span><span class="sxs-lookup"><span data-stu-id="673b4-282">This will return a string, which will determine if it’s a StorSimple disk.</span></span>

<span data-ttu-id="673b4-283">A mniej prawdopodobne, ale możliwa przyczyna może być również starych iscsid identyfikator PID procesu.</span><span class="sxs-lookup"><span data-stu-id="673b4-283">A less likely but possible cause could also be stale iscsid pid.</span></span> <span data-ttu-id="673b4-284">Użyj poniższych poleceń toolog poza z sesji iSCSI hello hello:</span><span class="sxs-lookup"><span data-stu-id="673b4-284">Use hello following command toolog off from hello iSCSI sessions:</span></span>

    iscsiadm -m node --logout -p <Target_IP>

<span data-ttu-id="673b4-285">Powtórz to polecenie dla wszystkich interfejsów sieciowych hello połączony na obiektów docelowych iSCSI hello, czyli urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="673b4-285">Repeat this command for all hello connected network interfaces on hello iSCSI target, which is your StorSimple device.</span></span> <span data-ttu-id="673b4-286">Po wylogowanie ma ze wszystkich sesji iSCSI hello Użyj sesji iSCSI hello tooreestablish IQN hello iSCSI docelowej.</span><span class="sxs-lookup"><span data-stu-id="673b4-286">Once you have logged off from all hello iSCSI sessions, use hello iSCSI target IQN tooreestablish hello iSCSI session.</span></span> <span data-ttu-id="673b4-287">Wpisz następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="673b4-287">Type hello following command:</span></span>

    iscsiadm -m node --login -T <TARGET_IQN>


<span data-ttu-id="673b4-288">Q.</span><span class="sxs-lookup"><span data-stu-id="673b4-288">Q.</span></span> <span data-ttu-id="673b4-289">Nie mam pewności, czy urządzenie jest białej.</span><span class="sxs-lookup"><span data-stu-id="673b4-289">I am not sure if my device is whitelisted.</span></span>

<span data-ttu-id="673b4-290">A.</span><span class="sxs-lookup"><span data-stu-id="673b4-290">A.</span></span> <span data-ttu-id="673b4-291">tooverify, czy urządzenie jest białej, użyj hello następujące polecenie interaktywne rozwiązywania problemów:</span><span class="sxs-lookup"><span data-stu-id="673b4-291">tooverify whether your device is whitelisted, use hello following troubleshooting interactive command:</span></span>

    multipathd –k
    multipathd> show devices
    available block devices:
    ram0 devnode blacklisted, unmonitored
    ram1 devnode blacklisted, unmonitored
    ram2 devnode blacklisted, unmonitored
    ram3 devnode blacklisted, unmonitored
    ram4 devnode blacklisted, unmonitored
    ram5 devnode blacklisted, unmonitored
    ram6 devnode blacklisted, unmonitored
    ram7 devnode blacklisted, unmonitored
    ram8 devnode blacklisted, unmonitored
    ram9 devnode blacklisted, unmonitored
    ram10 devnode blacklisted, unmonitored
    ram11 devnode blacklisted, unmonitored
    ram12 devnode blacklisted, unmonitored
    ram13 devnode blacklisted, unmonitored
    ram14 devnode blacklisted, unmonitored
    ram15 devnode blacklisted, unmonitored
    loop0 devnode blacklisted, unmonitored
    loop1 devnode blacklisted, unmonitored
    loop2 devnode blacklisted, unmonitored
    loop3 devnode blacklisted, unmonitored
    loop4 devnode blacklisted, unmonitored
    loop5 devnode blacklisted, unmonitored
    loop6 devnode blacklisted, unmonitored
    loop7 devnode blacklisted, unmonitored
    sr0 devnode blacklisted, unmonitored
    sda devnode whitelisted, monitored
    dm-0 devnode blacklisted, unmonitored
    dm-1 devnode blacklisted, unmonitored
    dm-2 devnode blacklisted, unmonitored
    sdb devnode whitelisted, monitored
    sdc devnode whitelisted, monitored
    dm-3 devnode blacklisted, unmonitored


<span data-ttu-id="673b4-292">Aby uzyskać więcej informacji, przejdź zbyt[Użyj Rozwiązywanie problemów z interaktywnego polecenia wielu ścieżek](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span><span class="sxs-lookup"><span data-stu-id="673b4-292">For more information, go too[use troubleshooting interactive command for multipathing](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span></span>

## <a name="list-of-useful-commands"></a><span data-ttu-id="673b4-293">Lista poleceń przydatne</span><span class="sxs-lookup"><span data-stu-id="673b4-293">List of useful commands</span></span>
| <span data-ttu-id="673b4-294">Typ</span><span class="sxs-lookup"><span data-stu-id="673b4-294">Type</span></span> | <span data-ttu-id="673b4-295">Polecenie</span><span class="sxs-lookup"><span data-stu-id="673b4-295">Command</span></span> | <span data-ttu-id="673b4-296">Opis</span><span class="sxs-lookup"><span data-stu-id="673b4-296">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="673b4-297">**iSCSI**</span><span class="sxs-lookup"><span data-stu-id="673b4-297">**iSCSI**</span></span> |`service iscsid start` |<span data-ttu-id="673b4-298">Uruchomienie usługi iSCSI</span><span class="sxs-lookup"><span data-stu-id="673b4-298">Start iSCSI service</span></span> |
| &nbsp; |`service iscsid stop` |<span data-ttu-id="673b4-299">Zatrzymaj usługę iSCSI</span><span class="sxs-lookup"><span data-stu-id="673b4-299">Stop iSCSI service</span></span> |
| &nbsp; |`service iscsid restart` |<span data-ttu-id="673b4-300">Ponowne uruchomienie usługi iSCSI</span><span class="sxs-lookup"><span data-stu-id="673b4-300">Restart iSCSI service</span></span> |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |<span data-ttu-id="673b4-301">Odnajdywanie dostępnych elementów docelowych na powitania określony adres</span><span class="sxs-lookup"><span data-stu-id="673b4-301">Discover available targets on hello specified address</span></span> |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |<span data-ttu-id="673b4-302">Zaloguj się za toohello obiektów docelowych iSCSI</span><span class="sxs-lookup"><span data-stu-id="673b4-302">Log in toohello iSCSI target</span></span> |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |<span data-ttu-id="673b4-303">Wyloguj się z hello obiektów docelowych iSCSI</span><span class="sxs-lookup"><span data-stu-id="673b4-303">Log out from hello iSCSI target</span></span> |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |<span data-ttu-id="673b4-304">Nazwa inicjatora iSCSI drukowania</span><span class="sxs-lookup"><span data-stu-id="673b4-304">Print iSCSI initiator name</span></span> |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |<span data-ttu-id="673b4-305">Sprawdź stan hello hello sesji iSCSI i wolumin odnalezionych na hoście hello</span><span class="sxs-lookup"><span data-stu-id="673b4-305">Check hello state of hello iSCSI session and volume discovered on hello host</span></span> |
| &nbsp; |`iscsi –m session` |<span data-ttu-id="673b4-306">Przedstawia wszystkie sesje iSCSI hello między hello hosta i hello urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="673b4-306">Shows all hello iSCSI sessions established between hello host and hello StorSimple device</span></span> |
|  | | |
| <span data-ttu-id="673b4-307">**Wiele ścieżek**</span><span class="sxs-lookup"><span data-stu-id="673b4-307">**Multipathing**</span></span> |`service multipathd start` |<span data-ttu-id="673b4-308">Demon wielościeżkowe Start</span><span class="sxs-lookup"><span data-stu-id="673b4-308">Start multipath daemon</span></span> |
| &nbsp; |`service multipathd stop` |<span data-ttu-id="673b4-309">Zatrzymaj demon wielościeżkowych</span><span class="sxs-lookup"><span data-stu-id="673b4-309">Stop multipath daemon</span></span> |
| &nbsp; |`service multipathd restart` |<span data-ttu-id="673b4-310">Uruchom ponownie demon wielościeżkowych</span><span class="sxs-lookup"><span data-stu-id="673b4-310">Restart multipath daemon</span></span> |
| &nbsp; |`chkconfig multipathd on` </br> <span data-ttu-id="673b4-311">LUB</span><span class="sxs-lookup"><span data-stu-id="673b4-311">OR</span></span> </br> `mpathconf –with_chkconfig y` |<span data-ttu-id="673b4-312">Włącz wielościeżkowe demon toostart w czasie rozruchu</span><span class="sxs-lookup"><span data-stu-id="673b4-312">Enable multipath daemon toostart at boot time</span></span> |
| &nbsp; |`multipathd –k` |<span data-ttu-id="673b4-313">Uruchom konsolę interakcyjne hello do rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="673b4-313">Start hello interactive console for troubleshooting</span></span> |
| &nbsp; |`multipath –l` |<span data-ttu-id="673b4-314">Lista połączeń wielościeżkowe i urządzeń</span><span class="sxs-lookup"><span data-stu-id="673b4-314">List multipath connections and devices</span></span> |
| &nbsp; |`mpathconf --enable` |<span data-ttu-id="673b4-315">Utwórz plik przykładowy mulitpath.conf w`/etc/mulitpath.conf`</span><span class="sxs-lookup"><span data-stu-id="673b4-315">Create a sample mulitpath.conf file in `/etc/mulitpath.conf`</span></span> |
|  | | |

## <a name="next-steps"></a><span data-ttu-id="673b4-316">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="673b4-316">Next steps</span></span>
<span data-ttu-id="673b4-317">Jak skonfigurować wielościeżkowego We/Wy na hoście z systemem Linux, może być również konieczne toohello toorefer po CentoS 6.6 dokumentów:</span><span class="sxs-lookup"><span data-stu-id="673b4-317">As you are configuring MPIO on Linux host, you may also need toorefer toohello following CentoS 6.6 documents:</span></span>

* [<span data-ttu-id="673b4-318">Konfigurowanie wielościeżkowego wejścia/wyjścia na CentOS</span><span class="sxs-lookup"><span data-stu-id="673b4-318">Setting up MPIO on CentOS</span></span>](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [<span data-ttu-id="673b4-319">Przewodnik szkolenia systemu Linux</span><span class="sxs-lookup"><span data-stu-id="673b4-319">Linux Training Guide</span></span>](http://linux-training.be/files/books/LinuxAdm.pdf)

