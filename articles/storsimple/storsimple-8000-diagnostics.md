---
title: "Narzędzia diagnostycznego do Rozwiązywanie problemów z urządzeniem StorSimple 8000 | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano tryby urządzenia StorSimple i wyjaśniono, jak zmienić tryb urządzenia za pomocą programu Windows PowerShell dla urządzenia StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: 8fae7bb357f8e5e8eff249edfe3a2aaafe04283c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-storsimple-diagnostics-tool-to-troubleshoot-8000-series-device-issues"></a><span data-ttu-id="cb420-103">Użyj narzędzia Diagnostyka StorSimple rozwiązywać problemy dotyczące urządzenia z serii 8000</span><span class="sxs-lookup"><span data-stu-id="cb420-103">Use the StorSimple Diagnostics Tool to troubleshoot 8000 series device issues</span></span>

## <a name="overview"></a><span data-ttu-id="cb420-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="cb420-104">Overview</span></span>

<span data-ttu-id="cb420-105">Narzędzie diagnostyczne StorSimple diagnozuje problemy związane z kondycja składnika systemu, wydajności sieci i sprzętu dla urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cb420-105">The StorSimple Diagnostics tool diagnoses issues related to system, performance, network, and hardware component health for a StorSimple device.</span></span> <span data-ttu-id="cb420-106">Narzędzie diagnostyczne można w różnych scenariuszach.</span><span class="sxs-lookup"><span data-stu-id="cb420-106">The diagnostics tool can be used in various scenarios.</span></span> <span data-ttu-id="cb420-107">Te scenariusze obejmują obciążenia planowania, wdrażania urządzenia StorSimple oceny środowiska sieciowego i określania wydajności działającego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="cb420-107">These scenarios include workload planning, deploying a StorSimple device, assessing the network environment, and determining the performance of an operational device.</span></span> <span data-ttu-id="cb420-108">Ten artykuł zawiera omówienie narzędzia diagnostycznego i opisano, jak można użyć narzędzia z urządzeniem StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cb420-108">This article provides an overview of the diagnostics tool and describes how the tool can be used with a StorSimple device.</span></span>

<span data-ttu-id="cb420-109">Narzędzie diagnostyczne jest przeznaczone głównie dla urządzeń lokalnych, serii StorSimple 8000 (8100 i 8600).</span><span class="sxs-lookup"><span data-stu-id="cb420-109">The diagnostics tool is primarily intended for StorSimple 8000 series on-premises devices (8100 and 8600).</span></span>

## <a name="run-diagnostics-tool"></a><span data-ttu-id="cb420-110">Uruchom narzędzie diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="cb420-110">Run diagnostics tool</span></span>

<span data-ttu-id="cb420-111">To narzędzie można uruchomić za pomocą interfejsu programu Windows PowerShell urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cb420-111">This tool can be run via the Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="cb420-112">Istnieją dwa sposoby dostępu lokalnego interfejsu urządzenia:</span><span class="sxs-lookup"><span data-stu-id="cb420-112">There are two ways to access the local interface of your device:</span></span>

* <span data-ttu-id="cb420-113">[Łączenie z konsolą szeregową urządzenia przy użyciu programu PuTTY](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="cb420-113">[Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
* <span data-ttu-id="cb420-114">[Zdalny dostęp do narzędzia programu Windows PowerShell dla urządzenia StorSimple](storsimple-remote-connect.md).</span><span class="sxs-lookup"><span data-stu-id="cb420-114">[Remotely access the tool via the Windows PowerShell for StorSimple](storsimple-remote-connect.md).</span></span>

<span data-ttu-id="cb420-115">W tym artykule przyjęto założenie, że nawiązano połączenie z konsolą szeregową urządzenia przy użyciu programu PuTTY.</span><span class="sxs-lookup"><span data-stu-id="cb420-115">In this article, we assume that you have connected to the device serial console via PuTTY.</span></span>

#### <a name="to-run-the-diagnostics-tool"></a><span data-ttu-id="cb420-116">Aby uruchomić narzędzie diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="cb420-116">To run the diagnostics tool</span></span>

<span data-ttu-id="cb420-117">Po podłączeniu do interfejsu programu Windows PowerShell, urządzenia, wykonaj następujące kroki, aby uruchomić polecenie cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cb420-117">Once you have connected to the Windows PowerShell interface of the device, perform the following steps to run the cmdlet.</span></span>
1. <span data-ttu-id="cb420-118">Zaloguj się do konsoli szeregowej urządzenia, wykonując kroki opisane w [przy użyciu programu PuTTY można nawiązać połączenia z konsolą szeregową urządzenia](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="cb420-118">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>

2. <span data-ttu-id="cb420-119">Wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="cb420-119">Type the following command:</span></span>

    `Invoke-HcsDiagnostics`

    <span data-ttu-id="cb420-120">Jeśli parametr zakresu nie jest określony, polecenie cmdlet wykonuje testów diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="cb420-120">If the scope parameter is not specified, the cmdlet executes all the diagnostic tests.</span></span> <span data-ttu-id="cb420-121">Te testy obejmują systemu, kondycja składnika sprzętu, sieci i wydajności.</span><span class="sxs-lookup"><span data-stu-id="cb420-121">These tests include system, hardware component health, network, and performance.</span></span> 
    
    <span data-ttu-id="cb420-122">Aby uruchomić specyficznego testu, należy określić parametr zakresu.</span><span class="sxs-lookup"><span data-stu-id="cb420-122">To run only a specific test, specify the scope parameter.</span></span> <span data-ttu-id="cb420-123">Na przykład aby uruchomić tylko testy sieci, wpisz</span><span class="sxs-lookup"><span data-stu-id="cb420-123">For instance, to run only the network test, type</span></span>

    `Invoke-HcsDiagnostics -Scope Network`

3. <span data-ttu-id="cb420-124">Zaznacz i skopiuj dane wyjściowe z okna programu PuTTY do pliku tekstowego w celu dalszej analizy.</span><span class="sxs-lookup"><span data-stu-id="cb420-124">Select and copy the output from the PuTTY window into a text file for further analysis.</span></span>

## <a name="scenarios-to-use-the-diagnostics-tool"></a><span data-ttu-id="cb420-125">Scenariusze użycia narzędzia diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="cb420-125">Scenarios to use the diagnostics tool</span></span>

<span data-ttu-id="cb420-126">Użyj narzędzia Diagnostyka rozwiązywać kondycji sieci, wydajności systemu i sprzętu, systemu.</span><span class="sxs-lookup"><span data-stu-id="cb420-126">Use the diagnostics tool to troubleshoot the network, performance, system, and hardware health of the system.</span></span> <span data-ttu-id="cb420-127">Poniżej przedstawiono kilka możliwych scenariuszy:</span><span class="sxs-lookup"><span data-stu-id="cb420-127">Here are some possible scenarios:</span></span>

* <span data-ttu-id="cb420-128">**Urządzenie w trybie offline** -Your StorSimple 8000 serii urządzenie jest w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="cb420-128">**Device offline** - Your StorSimple 8000 series device is offline.</span></span> <span data-ttu-id="cb420-129">W interfejsie programu Windows PowerShell wydaje czy obu kontrolerów są uruchomione i działają prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="cb420-129">However, from the Windows PowerShell interface, it seems that both the controllers are up and running.</span></span>
    * <span data-ttu-id="cb420-130">Za pomocą tego narzędzia, aby określić, stan sieci.</span><span class="sxs-lookup"><span data-stu-id="cb420-130">You can use this tool to then determine the network state.</span></span>
         
         > [!NOTE]
         > <span data-ttu-id="cb420-131">Nie należy używać tego narzędzia do oceny wydajności oraz ustawienia sieci na urządzenie przed rejestracji (lub konfigurowanie za pomocą Kreatora instalacji).</span><span class="sxs-lookup"><span data-stu-id="cb420-131">Do not use this tool to assess performance and network settings on a device before the registration (or configuring via setup wizard).</span></span> <span data-ttu-id="cb420-132">Prawidłowymi adresami IP są przypisywane do urządzenia podczas Kreatora konfiguracji i rejestracji.</span><span class="sxs-lookup"><span data-stu-id="cb420-132">A valid IP is assigned to the device during setup wizard and registration.</span></span> <span data-ttu-id="cb420-133">To polecenie cmdlet można uruchomić na urządzeniu, które nie jest zarejestrowane dla kondycji sprzętu i systemu.</span><span class="sxs-lookup"><span data-stu-id="cb420-133">You can run this cmdlet, on a device that is not registered, for hardware health and system.</span></span> <span data-ttu-id="cb420-134">Parametr zakresu, na przykład:</span><span class="sxs-lookup"><span data-stu-id="cb420-134">Use the scope parameter, for example:</span></span>
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* <span data-ttu-id="cb420-135">**Problemy dotyczące urządzenia trwałe** — występują problemy dotyczące urządzenia, które wydają się do innej witryny.</span><span class="sxs-lookup"><span data-stu-id="cb420-135">**Persistent device issues** - You are experiencing device issues that seem to persist.</span></span> <span data-ttu-id="cb420-136">Na przykład kończy się niepowodzeniem rejestracji.</span><span class="sxs-lookup"><span data-stu-id="cb420-136">For instance, registration is failing.</span></span> <span data-ttu-id="cb420-137">Użytkownik może również występować problemy dotyczące urządzenia gdy urządzenie jest pomyślnie zarejestrowane i działa na chwilę.</span><span class="sxs-lookup"><span data-stu-id="cb420-137">You could also be experiencing device issues after the device is successfully registered and operational for a while.</span></span>
    * <span data-ttu-id="cb420-138">W takim przypadku to narzędzie do wstępnego rozwiązywania problemów przed zalogowaniem się żądania obsługi z Support firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cb420-138">In this case, use this tool for preliminary troubleshooting before you log a service request with Microsoft Support.</span></span> <span data-ttu-id="cb420-139">Zalecamy uruchomienie tego narzędzia, a następnie przechwyć dane wyjściowe tego narzędzia.</span><span class="sxs-lookup"><span data-stu-id="cb420-139">We recommend that you run this tool and capture the output of this tool.</span></span> <span data-ttu-id="cb420-140">Te dane wyjściowe mogą udzielić im pomocy technicznej, aby przyspieszyć rozwiązywanie problemów.</span><span class="sxs-lookup"><span data-stu-id="cb420-140">You can then provide this output to Support to expedite troubleshooting.</span></span>
    * <span data-ttu-id="cb420-141">W przypadku dowolnego składnika lub klastra awariami sprzętu należy rejestrować w żądaniu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="cb420-141">If there are any hardware component or cluster failures, you should log in a Support request.</span></span>

* <span data-ttu-id="cb420-142">**Niska wydajność urządzenia** -Your StorSimple urządzenia jest powolne.</span><span class="sxs-lookup"><span data-stu-id="cb420-142">**Low device performance** - Your StorSimple device is slow.</span></span>
    * <span data-ttu-id="cb420-143">W takim przypadku Uruchom to polecenie cmdlet z parametrem zakresu wartość wydajności.</span><span class="sxs-lookup"><span data-stu-id="cb420-143">In this case, run this cmdlet with scope parameter set to performance.</span></span> <span data-ttu-id="cb420-144">Przeanalizuj dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="cb420-144">Analyze the output.</span></span> <span data-ttu-id="cb420-145">Określ chmurę opóźnienia odczytu i zapisu.</span><span class="sxs-lookup"><span data-stu-id="cb420-145">You get the cloud read-write latencies.</span></span> <span data-ttu-id="cb420-146">Użyj opóźnień jako maksymalną docelowy osiągalne, współczynnik pewne nadmiarowe obciążenie wewnętrzne przetwarzanie danych, a następnie wdrożyć obciążeń w systemie.</span><span class="sxs-lookup"><span data-stu-id="cb420-146">Use the reported latencies as maximum achievable target, factor in some overhead for the internal data processing, and then deploy the workloads on the system.</span></span> <span data-ttu-id="cb420-147">Aby uzyskać więcej informacji, przejdź do [test sieci umożliwia rozwiązywanie problemów z wydajnością urządzenia](#network-test).</span><span class="sxs-lookup"><span data-stu-id="cb420-147">For more information, go to [Use the network test to troubleshoot device performance](#network-test).</span></span>


## <a name="diagnostics-test-and-sample-outputs"></a><span data-ttu-id="cb420-148">Wyniki testów i przykładowych diagnostyki</span><span class="sxs-lookup"><span data-stu-id="cb420-148">Diagnostics test and sample outputs</span></span>

### <a name="hardware-test"></a><span data-ttu-id="cb420-149">Test sprzętu</span><span class="sxs-lookup"><span data-stu-id="cb420-149">Hardware test</span></span>

<span data-ttu-id="cb420-150">Ten test określa stan składników sprzętu, oprogramowania układowego należy i oprogramowanie układowe dysku w systemie.</span><span class="sxs-lookup"><span data-stu-id="cb420-150">This test determines the status of the hardware components, the USM firmware, and the disk firmware running on your system.</span></span>

* <span data-ttu-id="cb420-151">Składniki sprzętowe zgłaszane są tych składników, które nie powiodło się uruchomienie testu lub nie są dostępne w systemie.</span><span class="sxs-lookup"><span data-stu-id="cb420-151">The hardware components reported are those components that failed the test or are not present in the system.</span></span>
* <span data-ttu-id="cb420-152">Wersje oprogramowania układowego dysk i oprogramowania układowego należy są zgłaszane dla kontrolera 0 i kontrolera 1 i udostępnionych składników w systemie.</span><span class="sxs-lookup"><span data-stu-id="cb420-152">The USM firmware and disk firmware versions are reported for the Controller 0, Controller 1, and shared components in your system.</span></span> <span data-ttu-id="cb420-153">Aby uzyskać pełną listę składników sprzętowych przejdź do:</span><span class="sxs-lookup"><span data-stu-id="cb420-153">For a complete list of hardware components, go to:</span></span>

    * [<span data-ttu-id="cb420-154">Składniki w obudowie podstawowego</span><span class="sxs-lookup"><span data-stu-id="cb420-154">Components in primary enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [<span data-ttu-id="cb420-155">Składniki w obudowie EBOD</span><span class="sxs-lookup"><span data-stu-id="cb420-155">Components in EBOD enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> <span data-ttu-id="cb420-156">Jeśli test sprzętu zgłasza błędne składniki [Zaloguj żądania obsługi ze Microsoft Support](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="cb420-156">If the hardware test reports failed components, [log in a service request with Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a><span data-ttu-id="cb420-157">Przykładowe dane wyjściowe testu sprzętu uruchamianie na urządzeniu 8100</span><span class="sxs-lookup"><span data-stu-id="cb420-157">Sample output of hardware test run on an 8100 device</span></span>

<span data-ttu-id="cb420-158">Oto przykładowe dane wyjściowe z urządzenia StorSimple 8100.</span><span class="sxs-lookup"><span data-stu-id="cb420-158">Here is a sample output from a StorSimple 8100 device.</span></span> <span data-ttu-id="cb420-159">W urządzeniu 8100 modelu obudowa EBOD jest nieobecny.</span><span class="sxs-lookup"><span data-stu-id="cb420-159">In the 8100 model device, the EBOD enclosure is not present.</span></span> <span data-ttu-id="cb420-160">W związku z tym EBOD kontrolera składniki nie są zgłaszane.</span><span class="sxs-lookup"><span data-stu-id="cb420-160">Hence, the EBOD controller components are not reported.</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Hardware
Running hardware diagnostics ...
--------------------------------------------------
Hardware components failed or not present
----------------------

           Type           State      Controller           Index     EnclosureId
           ----           -----      ----------           -----     -----------
...rVipResource      NotPresent            None               1            None
...rVipResource      NotPresent            None               2            None
...rVipResource      NotPresent            None               3            None
...rVipResource      NotPresent            None               4            None
...rVipResource      NotPresent            None               5            None
...rVipResource      NotPresent            None               6            None
...rVipResource      NotPresent            None               7            None
...rVipResource      NotPresent            None               8            None
...rVipResource      NotPresent            None               9            None
...rVipResource      NotPresent            None              10            None
...rVipResource      NotPresent            None              11            None

Firmware information
----------------------
TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

--------------------------------------------------
```

### <a name="system-test"></a><span data-ttu-id="cb420-161">Test systemu</span><span class="sxs-lookup"><span data-stu-id="cb420-161">System test</span></span>

<span data-ttu-id="cb420-162">Ten test raportuje informacje o systemie, dostępne aktualizacje, informacje o klastrze i informacje o usługi dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="cb420-162">This test reports the system information, the updates available, the cluster information, and the service information for your device.</span></span>

* <span data-ttu-id="cb420-163">Informacje o systemie zawiera model, numer seryjny urządzenia strefy czasowej, stan kontrolera i wersji oprogramowania szczegółowe uruchomiona w systemie.</span><span class="sxs-lookup"><span data-stu-id="cb420-163">The system information includes the model, device serial number, time zone, controller status, and the detailed software version running on the system.</span></span> <span data-ttu-id="cb420-164">Aby poznać różne parametry systemu zgłoszone jako dane wyjściowe, przejdź do [interpretacji informacji o systemie](#appendix-interpreting-system-information).</span><span class="sxs-lookup"><span data-stu-id="cb420-164">To understand the various system parameters reported as the output, go to [Interpreting system information](#appendix-interpreting-system-information).</span></span>

* <span data-ttu-id="cb420-165">Czy tryby zwykłych oraz obsługi są dostępne raporty dostępności aktualizacji i ich nazw skojarzonego pakietu.</span><span class="sxs-lookup"><span data-stu-id="cb420-165">The update availability reports whether the regular and maintenance modes are available and their associated package names.</span></span> <span data-ttu-id="cb420-166">Jeśli `RegularUpdates` i `MaintenanceModeUpdates` są `false`, oznacza to, że aktualizacje nie są dostępne.</span><span class="sxs-lookup"><span data-stu-id="cb420-166">If `RegularUpdates` and `MaintenanceModeUpdates` are `false`, this indicates that the updates are not available.</span></span> <span data-ttu-id="cb420-167">Urządzenie jest aktualny.</span><span class="sxs-lookup"><span data-stu-id="cb420-167">Your device is up-to-date.</span></span>
* <span data-ttu-id="cb420-168">Informacje o klastrze zawiera informacje dotyczące różnych składników logicznych wszystkie grupy klastra moduł HCS oraz ich odpowiednich stanów.</span><span class="sxs-lookup"><span data-stu-id="cb420-168">The cluster information contains the information on various logical components of all the HCS cluster groups and their respective statuses.</span></span> <span data-ttu-id="cb420-169">Jeśli widzisz grupy klastra w trybie offline, w tej sekcji raportu, [skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="cb420-169">If you see an offline cluster group in this section of the report, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="cb420-170">Informacje o usłudze zawiera nazwy i Stanami wszystkich usług moduł HCS i konfiguracji (ci) uruchomione na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="cb420-170">The service information includes the names and statuses of all the HCS and CiS services running on your device.</span></span> <span data-ttu-id="cb420-171">Informacje te są przydatne do firmy Microsoft Support przy rozwiązywaniu problemu urządzenia.</span><span class="sxs-lookup"><span data-stu-id="cb420-171">This information is helpful for the Microsoft Support in troubleshooting the device issue.</span></span>

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a><span data-ttu-id="cb420-172">Przykładowe dane wyjściowe testu systemu uruchamianie na urządzeniu 8100</span><span class="sxs-lookup"><span data-stu-id="cb420-172">Sample output of system test run on an 8100 device</span></span>

<span data-ttu-id="cb420-173">Oto przykładowe dane wyjściowe uruchomienia na urządzeniu 8100 testu systemu.</span><span class="sxs-lookup"><span data-stu-id="cb420-173">Here is a sample output of the system test run on an 8100 device.</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope System
Running system diagnostics ...
--------------------------------------------------

System information
----------------------
Controller0:

InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                : (UTC-08:00) Pacific Time (US & Canada)
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : Disabled
FipsMode                : Enabled

Controller1:
InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                :
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : HttpsAndHttpEnabled
FipsMode                : Enabled

Update availability
----------------------
RegularUpdates              : False
MaintenanceModeUpdates      : False
RegularUpdatesTitle         : {}
MaintenanceModeUpdatesTitle : {}

Cluster information
----------------------
Name                          State OwnerGroup
----                          ----- ----------
ApplicationHostRLUA           Online HCS Cluster Group
Data0v4                       Online HCS Cluster Group
HCS Vnic Resource             Online HCS Cluster Group
hcs_cloud_connectivity_...    Online HCS Cluster Group
hcs_controller_replacement    Online HCS Cluster Group
hcs_datapath_service          Online HCS Cluster Group
hcs_management_servic         Online HCS Cluster Group
hcs_nvram_service             Online HCS Cluster Group
hcs_passive_datapath          Online HCS Passive Cluster Group
hcs_platform_service          Online HCS Cluster Group
hcs_saas_agent_service        Online HCS Cluster Group
HddDataClusterDisk            Online HCS Cluster Group
HddMgmtClusterDisk            Online HCS Cluster Group
HddReplClusterDisk            Online HCS Cluster Group
iSCSI Target Server           Online HCS Cluster Group
NvramClusterDisk              Online HCS Cluster Group
SSAdminRLUA                   Online HCS Cluster Group
SsdDataClusterDisk            Online HCS Cluster Group
SsdNvramClusterDisk           Online HCS Cluster Group

Service information
----------------------
Name                                          Status DisplayName
----                                          ------ -----------
CiSAgentSvc                                   Stopped CiS Service Agent
hcs_cloud_connectivity_...                    Running hcs_cloud_connectivity...
hcs_controller_replacement                    Running HCS Controller Replace...
hcs_datapath_service                          Running HCS Datapath Service
hcs_management_service                        Running HCS Management Service
hcs_minishell                                 Running hcs_minishell
HCS_NVRAM_Service                             Running HCS NVRAM Service
hcs_passive_datapath                          Stopped HCS Passive Datapath S...
hcs_platform_service                          Running HCS Platform Monitor S...
hcs_saas_agent_service                        Running hcs_saas_agent_service
hcs_startup                                   Stopped hcs_startup
--------------------------------------------------
```

### <a name="network-test"></a><span data-ttu-id="cb420-174">Test sieci</span><span class="sxs-lookup"><span data-stu-id="cb420-174">Network test</span></span>

<span data-ttu-id="cb420-175">Ten test sprawdza stan interfejsów sieciowych, porty, DNS i protokołu NTP łączności z serwerem, SSL certyfikatu, poświadczeń konta magazynu, łączność z serwerami aktualizacji i łączności serwera proxy sieci web na urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cb420-175">This test validates the status of the network interfaces, ports, DNS and NTP server connectivity, SSL certificate, storage account credentials, connectivity to the Update servers, and web proxy connectivity on your StorSimple device.</span></span>

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a><span data-ttu-id="cb420-176">Przykładowe dane wyjściowe sieci testów, gdy jest włączona tylko DATA0</span><span class="sxs-lookup"><span data-stu-id="cb420-176">Sample output of network test when only DATA0 is enabled</span></span>

<span data-ttu-id="cb420-177">Oto przykładowe dane wyjściowe urządzenia 8100.</span><span class="sxs-lookup"><span data-stu-id="cb420-177">Here is a sample output of the 8100 device.</span></span> <span data-ttu-id="cb420-178">Można zobaczyć w danych wyjściowych który:</span><span class="sxs-lookup"><span data-stu-id="cb420-178">You can see in the output that:</span></span>
* <span data-ttu-id="cb420-179">Tylko dane 0 i 1 danych interfejsy sieciowe są włączone i skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="cb420-179">Only DATA 0 and DATA 1 network interfaces are enabled and configured.</span></span>
* <span data-ttu-id="cb420-180">DANE 2 5 nie są włączone w portalu.</span><span class="sxs-lookup"><span data-stu-id="cb420-180">DATA 2 - 5 are not enabled in the portal.</span></span>
* <span data-ttu-id="cb420-181">Konfiguracja serwera DNS jest prawidłowa i urządzenia można połączyć za pośrednictwem serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="cb420-181">The DNS server configuration is valid and the device can connect via the DNS server.</span></span>
* <span data-ttu-id="cb420-182">Połączenie serwera NTP również funkcjonuje prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="cb420-182">The NTP server connectivity is also fine.</span></span>
* <span data-ttu-id="cb420-183">Otwartych portów 80 i 443.</span><span class="sxs-lookup"><span data-stu-id="cb420-183">Ports 80 and 443 are open.</span></span> <span data-ttu-id="cb420-184">Jednak port 9354 jest zablokowany.</span><span class="sxs-lookup"><span data-stu-id="cb420-184">However, port 9354 is blocked.</span></span> <span data-ttu-id="cb420-185">Na podstawie [wymagania sieciowe systemu](storsimple-system-requirements.md), należy otworzyć tego portu do komunikacji magistrali usługi.</span><span class="sxs-lookup"><span data-stu-id="cb420-185">Based on the [system network requirements](storsimple-system-requirements.md), you need to open this port for the service bus communication.</span></span>
* <span data-ttu-id="cb420-186">Certyfikat SSL jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="cb420-186">The SSL certification is valid.</span></span>
* <span data-ttu-id="cb420-187">Urządzenie można łączyć z kontem magazynu: _myss8000storageacct_.</span><span class="sxs-lookup"><span data-stu-id="cb420-187">The device can connect to the storage account: _myss8000storageacct_.</span></span>
* <span data-ttu-id="cb420-188">Łączność z serwerami aktualizacji jest prawidłowa.</span><span class="sxs-lookup"><span data-stu-id="cb420-188">The connectivity to Update servers is valid.</span></span>
* <span data-ttu-id="cb420-189">Nie skonfigurowano serwera proxy sieci web na tym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="cb420-189">The web proxy is not configured on this device.</span></span>

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a><span data-ttu-id="cb420-190">Przykładowe dane wyjściowe testu sieci, gdy są włączone DATA0 i dane1</span><span class="sxs-lookup"><span data-stu-id="cb420-190">Sample output of network test when DATA0 and DATA1 are enabled</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Network
Running network diagnostics ....
--------------------------------------------------
Validating networks .....
Name                Entity              Result              Details
----                ------              ------              -------
Network interface   Data0               Valid
Network interface   Data1               Valid
Network interface   Data2               Not enabled
Network interface   Data3               Not enabled
Network interface   Data4               Not enabled
Network interface   Data5               Not enabled
DNS                 10.222.118.154      Valid
NTP                 time.windows.com    Valid
Port                80                  Open
Port                443                 Open
Port                9354                Blocked
SSL certificate     https://myss8000... Valid
Storage account ... myss8000storageacct Valid
URL                 http://download.... Valid
URL                 http://download.... Valid
Web proxy                               Not enabled         Web proxy is not...
--------------------------------------------------
```

### <a name="performance-test"></a><span data-ttu-id="cb420-191">Test wydajności</span><span class="sxs-lookup"><span data-stu-id="cb420-191">Performance test</span></span>

<span data-ttu-id="cb420-192">Ten test raportów wydajności chmury za pośrednictwem chmury opóźnienia odczytu i zapisu dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="cb420-192">This test reports the cloud performance via the cloud read-write latencies for your device.</span></span> <span data-ttu-id="cb420-193">To narzędzie można ustalić linię bazową wydajności chmury, który można uzyskać z StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cb420-193">This tool can be used to establish a baseline of the cloud performance that you can achieve with StorSimple.</span></span> <span data-ttu-id="cb420-194">Narzędzie Raporty maksymalną wydajność (najlepsze scenariusz dla opóźnienia odczytu i zapisu) można uzyskać połączenia.</span><span class="sxs-lookup"><span data-stu-id="cb420-194">The tool reports the maximum performance (best case scenario for read-write latencies) that you can get for your connection.</span></span>

<span data-ttu-id="cb420-195">Jak narzędzie zgłasza maksymalną wydajność osiągalne, możemy użyć opóźnień odczytu i zapisu jako miejsca docelowe w przypadku wdrażania obciążeń.</span><span class="sxs-lookup"><span data-stu-id="cb420-195">As the tool reports the maximum achievable performance, we can use the reported read-write latencies as targets when deploying the workloads.</span></span>

<span data-ttu-id="cb420-196">Test symuluje rozmiarów obiektu blob skojarzony z typami inny wolumin na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="cb420-196">The test simulates the blob sizes associated with the different volume types on the device.</span></span> <span data-ttu-id="cb420-197">Do warstwy standardowych i kopii zapasowych woluminów przypiętych lokalnie użyj rozmiar obiektu blob 64 KB.</span><span class="sxs-lookup"><span data-stu-id="cb420-197">Regular tiered and backups of locally pinned volumes use a 64 KB blob size.</span></span> <span data-ttu-id="cb420-198">Woluminy warstwowe z zaznaczoną opcją archiwum Użyj rozmiar danych obiektu blob 512 KB.</span><span class="sxs-lookup"><span data-stu-id="cb420-198">Tiered volumes with archive option checked use 512 KB blob data size.</span></span> <span data-ttu-id="cb420-199">Jeśli urządzenie ma woluminów warstwowych i przypiętych lokalnie skonfigurowane, tylko testu odpowiadający blob 64 KB, rozmiar danych jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="cb420-199">If your device has tiered and locally pinned volumes configured, only the test corresponding to 64 KB blob data size is run.</span></span>

<span data-ttu-id="cb420-200">Aby użyć tego narzędzia, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cb420-200">To use this tool, perform the following steps:</span></span>

1.  <span data-ttu-id="cb420-201">Najpierw utwórz mieszane woluminy warstwowe i woluminy warstwowe z zaznaczoną opcją zarchiwizowane.</span><span class="sxs-lookup"><span data-stu-id="cb420-201">First, create a mix of tiered volumes and tiered volumes with archived option checked.</span></span> <span data-ttu-id="cb420-202">Ta akcja zapewnia, że narzędzie działa testy 64 KB i 512 KB rozmiarów obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="cb420-202">This action ensures that the tool runs the tests for both 64 KB and 512 KB blob sizes.</span></span>

2. <span data-ttu-id="cb420-203">Po utworzeniu i skonfigurowanych woluminach, uruchom polecenie cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cb420-203">Run the cmdlet after you have created and configured the volumes.</span></span> <span data-ttu-id="cb420-204">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="cb420-204">Type:</span></span>

    `Invoke-HcsDiagnostics -Scope Performance`

3. <span data-ttu-id="cb420-205">Zanotuj opóźnienia zapisu i odczytu zgłoszone przez narzędzie.</span><span class="sxs-lookup"><span data-stu-id="cb420-205">Make a note of the read-write latencies reported by the tool.</span></span> <span data-ttu-id="cb420-206">Ten test może potrwać kilka minut do uruchomienia przed rozpoczęciem zgłasza wyniki.</span><span class="sxs-lookup"><span data-stu-id="cb420-206">This test can take several minutes to run before it reports the results.</span></span>

4. <span data-ttu-id="cb420-207">W przypadku opóźnienia połączenia pod oczekiwanego zakresu, następnie opóźnienia zgłoszone przez narzędzie może służyć jako maksymalną osiągalne docelowego podczas wdrażania obciążeń.</span><span class="sxs-lookup"><span data-stu-id="cb420-207">If the connection latencies are all under the expected range, then the latencies reported by the tool can be used as maximum achievable target when deploying the workloads.</span></span> <span data-ttu-id="cb420-208">Współczynnik niektórych obciążenie przetwarzania danych wewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="cb420-208">Factor in some overhead for internal data processing.</span></span>

    <span data-ttu-id="cb420-209">W przypadku wysokiej opóźnienia zapisu i odczytu zgłoszone przez narzędzie diagnostyczne:</span><span class="sxs-lookup"><span data-stu-id="cb420-209">If the read-write latencies reported by the diagnostics tool are high:</span></span>

    1. <span data-ttu-id="cb420-210">Skonfiguruj analityka magazynu dla usług obiektów blob i analizowanie danych wyjściowych, aby zrozumieć opóźnienia dla konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cb420-210">Configure Storage Analytics for blob services and analyze the output to understand the latencies for the Azure storage account.</span></span> <span data-ttu-id="cb420-211">Aby uzyskać szczegółowe instrukcje, przejdź do [włączyć i skonfigurować analityka magazynu](../storage/common/storage-enable-and-view-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="cb420-211">For detailed instructions, go to [enable and configure Storage Analytics](../storage/common/storage-enable-and-view-metrics.md).</span></span> <span data-ttu-id="cb420-212">Jeśli te czasy oczekiwania są także wysokiej i porównywalnych numery otrzymany od narzędzia diagnostycznego StorSimple, następnie należy zalogować żądanie usługi z usługą Azure storage.</span><span class="sxs-lookup"><span data-stu-id="cb420-212">If those latencies are also high and comparable to the numbers you received from the StorSimple Diagnostics tool, then you need to log a service request with Azure storage.</span></span>

    2. <span data-ttu-id="cb420-213">Jeśli brakuje opóźnienia konta magazynu, skontaktuj się z administratorem sieci w celu zbadania problemów opóźnienie w sieci.</span><span class="sxs-lookup"><span data-stu-id="cb420-213">If the storage account latencies are low, contact your network administrator to investigate any latency issues in your network.</span></span>

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a><span data-ttu-id="cb420-214">Przykładowe dane wyjściowe uruchamiać na urządzeniu 8100 testu wydajności</span><span class="sxs-lookup"><span data-stu-id="cb420-214">Sample output of performance test run on an 8100 device</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Performance
Running performance diagnostics...
--------------------------------------------------
Cloud performance: writing blobs
Cloud write latency: 194 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: reading blobs..
Cloud read latency: 544 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: writing blobs.
Cloud write latency: 369 ms using credential 'myss8000storageacct', blob size '512KB'
Cloud performance: reading blobs...
Cloud read latency: 4924 ms using credential 'myss8000storageacct', blob size '512KB'
--------------------------------------------------
Controller0>
```

## <a name="appendix-interpreting-system-information"></a><span data-ttu-id="cb420-215">Dodatku: informacje o systemie interpretowanie</span><span class="sxs-lookup"><span data-stu-id="cb420-215">Appendix: interpreting system information</span></span>

<span data-ttu-id="cb420-216">Oto opisujące jaki różne parametry programu Windows PowerShell w mapie informacji systemu do tabeli.</span><span class="sxs-lookup"><span data-stu-id="cb420-216">Here is a table describing what the various Windows PowerShell parameters in the system information map to.</span></span> 

| <span data-ttu-id="cb420-217">Parametr programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb420-217">PowerShell Parameter</span></span>    | <span data-ttu-id="cb420-218">Opis</span><span class="sxs-lookup"><span data-stu-id="cb420-218">Description</span></span>  |
|-------------------------|------------------|
| <span data-ttu-id="cb420-219">Identyfikator wystąpienia</span><span class="sxs-lookup"><span data-stu-id="cb420-219">Instance ID</span></span>             | <span data-ttu-id="cb420-220">Każdy kontroler ma unikatowego identyfikatora lub identyfikator GUID skojarzony z nim.</span><span class="sxs-lookup"><span data-stu-id="cb420-220">Every controller has a unique identifier or a GUID associated with it.</span></span>|
| <span data-ttu-id="cb420-221">Nazwa</span><span class="sxs-lookup"><span data-stu-id="cb420-221">Name</span></span>                    | <span data-ttu-id="cb420-222">Przyjazna nazwa urządzenia, zgodnie z konfiguracją za pośrednictwem portalu Azure podczas wdrażania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="cb420-222">The friendly name of the device as configured through the Azure portal during device deployment.</span></span> <span data-ttu-id="cb420-223">Przyjazna nazwa domyślna jest numer seryjny urządzenia.</span><span class="sxs-lookup"><span data-stu-id="cb420-223">The default friendly name is the device serial number.</span></span> |
| <span data-ttu-id="cb420-224">Model</span><span class="sxs-lookup"><span data-stu-id="cb420-224">Model</span></span>                   | <span data-ttu-id="cb420-225">Model urządzenia serii StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="cb420-225">The model of your StorSimple 8000 series device.</span></span> <span data-ttu-id="cb420-226">Model może być 8100 lub 8600.</span><span class="sxs-lookup"><span data-stu-id="cb420-226">The model can be 8100 or 8600.</span></span>|
| <span data-ttu-id="cb420-227">numer seryjny</span><span class="sxs-lookup"><span data-stu-id="cb420-227">SerialNumber</span></span>            | <span data-ttu-id="cb420-228">Numer seryjny urządzenia jest przypisana w fabryce i 15 znaków.</span><span class="sxs-lookup"><span data-stu-id="cb420-228">The device serial number is assigned at the factory and is 15 characters long.</span></span> <span data-ttu-id="cb420-229">Wskazuje, na przykład 8600 SHX0991003G44HT:</span><span class="sxs-lookup"><span data-stu-id="cb420-229">For instance, 8600-SHX0991003G44HT indicates:</span></span><br> <span data-ttu-id="cb420-230">8600 — jest to model urządzenia.</span><span class="sxs-lookup"><span data-stu-id="cb420-230">8600 – Is the device model.</span></span><br><span data-ttu-id="cb420-231">SHX — jest miejsce produkcji.</span><span class="sxs-lookup"><span data-stu-id="cb420-231">SHX – Is the manufacturing site.</span></span><br> <span data-ttu-id="cb420-232">0991003 — jest określony produkt.</span><span class="sxs-lookup"><span data-stu-id="cb420-232">0991003 - Is a specific product.</span></span> <br> <span data-ttu-id="cb420-233">G44HT-5 ostatnich cyfr numeru są zwiększane, aby utworzyć unikatowe numery seryjne.</span><span class="sxs-lookup"><span data-stu-id="cb420-233">G44HT- the last 5 digits are incremented to create unique serial numbers.</span></span> <span data-ttu-id="cb420-234">Nie można sekwencyjnych zestawu.</span><span class="sxs-lookup"><span data-stu-id="cb420-234">This may not be a sequential set.</span></span>|
| <span data-ttu-id="cb420-235">Strefa czasowa</span><span class="sxs-lookup"><span data-stu-id="cb420-235">TimeZone</span></span>                | <span data-ttu-id="cb420-236">Strefa czasowa urządzenia, zgodnie z konfiguracją w portalu Azure podczas wdrażania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="cb420-236">The device time zone as configured in the Azure portal during device deployment.</span></span>|
| <span data-ttu-id="cb420-237">CurrentController</span><span class="sxs-lookup"><span data-stu-id="cb420-237">CurrentController</span></span>       | <span data-ttu-id="cb420-238">Kontroler, że masz połączenie za pośrednictwem interfejsu programu Windows PowerShell urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cb420-238">The controller that you are connected to through the Windows PowerShell interface of your StorSimple device.</span></span>|
| <span data-ttu-id="cb420-239">ActiveController</span><span class="sxs-lookup"><span data-stu-id="cb420-239">ActiveController</span></span>        | <span data-ttu-id="cb420-240">Kontroler, który jest aktywna na urządzeniu i kontroluje wszystkie operacje sieci i dysku.</span><span class="sxs-lookup"><span data-stu-id="cb420-240">The controller that is active on your device and is controlling all the network and disk operations.</span></span> <span data-ttu-id="cb420-241">Może to być kontrolera 0 i kontrolera 1.</span><span class="sxs-lookup"><span data-stu-id="cb420-241">This can be Controller 0 or Controller 1.</span></span>  |
| <span data-ttu-id="cb420-242">Controller0Status</span><span class="sxs-lookup"><span data-stu-id="cb420-242">Controller0Status</span></span>       | <span data-ttu-id="cb420-243">Stan kontrolera 0 na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="cb420-243">The status of Controller 0 on your device.</span></span> <span data-ttu-id="cb420-244">Stan kontrolera może być normalna w trybie odzyskiwania lub jest niedostępny.</span><span class="sxs-lookup"><span data-stu-id="cb420-244">The controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="cb420-245">Controller1Status</span><span class="sxs-lookup"><span data-stu-id="cb420-245">Controller1Status</span></span>       | <span data-ttu-id="cb420-246">Stan kontrolera 1 na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="cb420-246">The status of Controller 1 on your device.</span></span>  <span data-ttu-id="cb420-247">Stan kontrolera może być normalna w trybie odzyskiwania lub jest niedostępny.</span><span class="sxs-lookup"><span data-stu-id="cb420-247">The controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="cb420-248">SystemMode</span><span class="sxs-lookup"><span data-stu-id="cb420-248">SystemMode</span></span>              | <span data-ttu-id="cb420-249">Ogólny stan urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cb420-249">The overall status of your StorSimple device.</span></span> <span data-ttu-id="cb420-250">Stan urządzenia może zostać przeprowadzony normalnie, konserwacji lub wycofany z eksploatacji (odpowiada dezaktywowane w portalu Azure).</span><span class="sxs-lookup"><span data-stu-id="cb420-250">The device status can be normal, maintenance, or decommissioned (corresponds to deactivated in the Azure portal).</span></span>|
| <span data-ttu-id="cb420-251">FriendlySoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="cb420-251">FriendlySoftwareVersion</span></span> | <span data-ttu-id="cb420-252">Przyjazne ciąg, który odpowiada wersji oprogramowania na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="cb420-252">The friendly string that corresponds to the device software version.</span></span> <span data-ttu-id="cb420-253">Komputerze z systemem aktualizacji 4 wersja oprogramowania przyjazną będzie StorSimple 8000 serii aktualizacji 4.0.</span><span class="sxs-lookup"><span data-stu-id="cb420-253">For a system running Update 4, the friendly software version would be StorSimple 8000 Series Update 4.0.</span></span>|
| <span data-ttu-id="cb420-254">HcsSoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="cb420-254">HcsSoftwareVersion</span></span>      | <span data-ttu-id="cb420-255">Wersja oprogramowania moduł HCS uruchomione na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="cb420-255">The HCS software version running on your device.</span></span> <span data-ttu-id="cb420-256">Na przykład moduł HCS wersji oprogramowania odpowiadający StorSimple 8000 serii aktualizacji 4.0 jest 6.3.9600.17820.</span><span class="sxs-lookup"><span data-stu-id="cb420-256">For instance, the HCS software version corresponding to StorSimple 8000 Series Update 4.0 is 6.3.9600.17820.</span></span> |
| <span data-ttu-id="cb420-257">ApiVersion</span><span class="sxs-lookup"><span data-stu-id="cb420-257">ApiVersion</span></span>              | <span data-ttu-id="cb420-258">Wersja oprogramowania Windows API środowiska PowerShell moduł HCS urządzenia.</span><span class="sxs-lookup"><span data-stu-id="cb420-258">The software version of the Windows PowerShell API of the HCS device.</span></span>|
| <span data-ttu-id="cb420-259">VhdVersion</span><span class="sxs-lookup"><span data-stu-id="cb420-259">VhdVersion</span></span>              | <span data-ttu-id="cb420-260">Wersja oprogramowania dostarczonej urządzenia z obrazu.</span><span class="sxs-lookup"><span data-stu-id="cb420-260">The software version of the factory image that the device was shipped with.</span></span> <span data-ttu-id="cb420-261">W przypadku zresetowania urządzenia do ustawień fabrycznych uruchomieniu tej wersji oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="cb420-261">If you reset your device to factory defaults, then it runs this software version.</span></span>|
| <span data-ttu-id="cb420-262">OSVersion</span><span class="sxs-lookup"><span data-stu-id="cb420-262">OSVersion</span></span>               | <span data-ttu-id="cb420-263">Wersja oprogramowania systemu operacyjnego Windows Server uruchomionej na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="cb420-263">The software version of the Windows Server operating system running on the device.</span></span> <span data-ttu-id="cb420-264">Wyłączanie systemu Windows Server 2012 R2, który odpowiada 6.3.9600 opiera się urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cb420-264">The StorSimple device is based off the Windows Server 2012 R2 that corresponds to 6.3.9600.</span></span>|
| <span data-ttu-id="cb420-265">CisAgentVersion</span><span class="sxs-lookup"><span data-stu-id="cb420-265">CisAgentVersion</span></span>         | <span data-ttu-id="cb420-266">Wersja agenta konfiguracji (ci) uruchomione na urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cb420-266">The version for your Cis agent running on your StorSimple device.</span></span> <span data-ttu-id="cb420-267">Ten agent pomaga komunikować się z usługą Menedżer StorSimple, działające na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="cb420-267">This agent helps communicate with the StorSimple Manager service running in Azure.</span></span>|
| <span data-ttu-id="cb420-268">MdsAgentVersion</span><span class="sxs-lookup"><span data-stu-id="cb420-268">MdsAgentVersion</span></span>         | <span data-ttu-id="cb420-269">Wersja odpowiadający Mds agenta uruchomionego na urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cb420-269">The version corresponding to the Mds agent running on your StorSimple device.</span></span> <span data-ttu-id="cb420-270">Ten agent przeniesienie danych do monitorowania i diagnostyki usługi (MDS).</span><span class="sxs-lookup"><span data-stu-id="cb420-270">This agent moves data to the Monitoring and Diagnostics Service (MDS).</span></span>|
| <span data-ttu-id="cb420-271">Lsisas2Version</span><span class="sxs-lookup"><span data-stu-id="cb420-271">Lsisas2Version</span></span>          | <span data-ttu-id="cb420-272">Wersja odpowiadający sterowniki LSI na urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cb420-272">The version corresponding to the LSI drivers on your StorSimple device.</span></span>|
| <span data-ttu-id="cb420-273">Pojemność</span><span class="sxs-lookup"><span data-stu-id="cb420-273">Capacity</span></span>                | <span data-ttu-id="cb420-274">Całkowita pojemność urządzenia w bajtach.</span><span class="sxs-lookup"><span data-stu-id="cb420-274">The total capacity of the device in bytes.</span></span>|
| <span data-ttu-id="cb420-275">RemoteManagementMode</span><span class="sxs-lookup"><span data-stu-id="cb420-275">RemoteManagementMode</span></span>    | <span data-ttu-id="cb420-276">Wskazuje, czy urządzenia mogą być zarządzane zdalnie za pośrednictwem jej interfejsu programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cb420-276">Indicates whether the device can be remotely managed via its Windows PowerShell interface.</span></span> |
| <span data-ttu-id="cb420-277">FipsMode</span><span class="sxs-lookup"><span data-stu-id="cb420-277">FipsMode</span></span>                | <span data-ttu-id="cb420-278">Wskazuje, czy tryb Stanów Zjednoczonych informacji przetwarzania Standard FIPS (Federal) jest włączony na twoim urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="cb420-278">Indicates whether the United States Federal Information Processing Standard (FIPS) mode is enabled on your device.</span></span> <span data-ttu-id="cb420-279">Standard FIPS 140 definiuje zatwierdzone do użycia przez nas federalne dla instytucji rządowych systemów komputerowych do ochrony danych poufnych algorytmów kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="cb420-279">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span></span> <span data-ttu-id="cb420-280">W przypadku urządzeń programu Update 4 lub nowszego trybie FIPS jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="cb420-280">For devices running Update 4 or later, FIPS mode is enabled by default.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cb420-281">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cb420-281">Next steps</span></span>

* <span data-ttu-id="cb420-282">Dowiedz się [składni polecenia cmdlet Invoke-HcsDiagnostics](https://technet.microsoft.com/library/mt795371.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb420-282">Learn the [syntax of the Invoke-HcsDiagnostics cmdlet](https://technet.microsoft.com/library/mt795371.aspx).</span></span>

* <span data-ttu-id="cb420-283">Dowiedz się więcej o sposobie [Rozwiązywanie problemów dotyczących wdrożenia](storsimple-troubleshoot-deployment.md) na urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cb420-283">Learn more about how to [troubleshoot deployment issues](storsimple-troubleshoot-deployment.md) on your StorSimple device.</span></span>
