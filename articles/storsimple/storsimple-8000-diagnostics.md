---
title: "urządzenie StorSimple 8000 tootroubleshoot narzędzie aaaDiagnostics | Dokumentacja firmy Microsoft"
description: "Zawiera opis tryby urządzenia StorSimple hello i jak toouse środowiska Windows PowerShell dla StorSimple toochange hello tryb urządzenia."
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
ms.openlocfilehash: e8b7fdbc44d2533973b63da841335ba73ba0014b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-diagnostics-tool-tootroubleshoot-8000-series-device-issues"></a><span data-ttu-id="43668-103">Użyj hello narzędzia diagnostycznego StorSimple tootroubleshoot 8000 serii problemów z urządzeniami</span><span class="sxs-lookup"><span data-stu-id="43668-103">Use hello StorSimple Diagnostics Tool tootroubleshoot 8000 series device issues</span></span>

## <a name="overview"></a><span data-ttu-id="43668-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="43668-104">Overview</span></span>

<span data-ttu-id="43668-105">Witaj narzędzia diagnostycznego StorSimple diagnozuje toosystem pokrewne problemy, wydajność sieci i kondycja składnika sprzętu dla urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="43668-105">hello StorSimple Diagnostics tool diagnoses issues related toosystem, performance, network, and hardware component health for a StorSimple device.</span></span> <span data-ttu-id="43668-106">Narzędzie diagnostyczne Hello służy w różnych scenariuszach.</span><span class="sxs-lookup"><span data-stu-id="43668-106">hello diagnostics tool can be used in various scenarios.</span></span> <span data-ttu-id="43668-107">Te scenariusze obejmują obciążenia planowania, wdrażania urządzenia StorSimple oceny środowiska sieciowego hello i określania hello wydajności operacyjnej urządzenia.</span><span class="sxs-lookup"><span data-stu-id="43668-107">These scenarios include workload planning, deploying a StorSimple device, assessing hello network environment, and determining hello performance of an operational device.</span></span> <span data-ttu-id="43668-108">Ten artykuł zawiera omówienie narzędzia diagnostycznego hello i zawiera opis sposobu użycia narzędzia hello z urządzeniem StorSimple.</span><span class="sxs-lookup"><span data-stu-id="43668-108">This article provides an overview of hello diagnostics tool and describes how hello tool can be used with a StorSimple device.</span></span>

<span data-ttu-id="43668-109">Narzędzie diagnostyczne Hello jest przeznaczone głównie dla urządzeń lokalnych, serii StorSimple 8000 (8100 i 8600).</span><span class="sxs-lookup"><span data-stu-id="43668-109">hello diagnostics tool is primarily intended for StorSimple 8000 series on-premises devices (8100 and 8600).</span></span>

## <a name="run-diagnostics-tool"></a><span data-ttu-id="43668-110">Uruchom narzędzie diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="43668-110">Run diagnostics tool</span></span>

<span data-ttu-id="43668-111">To narzędzie można uruchomić za pomocą interfejsu programu Windows PowerShell hello urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="43668-111">This tool can be run via hello Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="43668-112">Istnieją dwa sposoby tooaccess hello lokalnego interfejsu urządzenia:</span><span class="sxs-lookup"><span data-stu-id="43668-112">There are two ways tooaccess hello local interface of your device:</span></span>

* <span data-ttu-id="43668-113">[Konsoli szeregowej urządzenia użyj PuTTY tooconnect toohello](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="43668-113">[Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
* <span data-ttu-id="43668-114">[Zdalny dostęp do narzędzia hello za pośrednictwem hello środowiska Windows PowerShell dla urządzenia StorSimple](storsimple-remote-connect.md).</span><span class="sxs-lookup"><span data-stu-id="43668-114">[Remotely access hello tool via hello Windows PowerShell for StorSimple](storsimple-remote-connect.md).</span></span>

<span data-ttu-id="43668-115">W tym artykule przyjęto założenie, że nawiązano połączenie toohello konsolą szeregową urządzenia przy użyciu programu PuTTY.</span><span class="sxs-lookup"><span data-stu-id="43668-115">In this article, we assume that you have connected toohello device serial console via PuTTY.</span></span>

#### <a name="toorun-hello-diagnostics-tool"></a><span data-ttu-id="43668-116">Narzędzie diagnostyczne hello toorun</span><span class="sxs-lookup"><span data-stu-id="43668-116">toorun hello diagnostics tool</span></span>

<span data-ttu-id="43668-117">Po połączeniu interfejsu programu Windows PowerShell toohello hello urządzenia, należy wykonać hello następującego polecenia cmdlet hello toorun czynności.</span><span class="sxs-lookup"><span data-stu-id="43668-117">Once you have connected toohello Windows PowerShell interface of hello device, perform hello following steps toorun hello cmdlet.</span></span>
1. <span data-ttu-id="43668-118">Zaloguj się na konsoli szeregowej urządzenia toohello wykonując kroki hello w [konsolą szeregową urządzenia przy użyciu programu PuTTY tooconnect toohello](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="43668-118">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>

2. <span data-ttu-id="43668-119">Wpisz następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="43668-119">Type hello following command:</span></span>

    `Invoke-HcsDiagnostics`

    <span data-ttu-id="43668-120">Jeśli nie określono parametru zakresu hello, polecenia cmdlet hello wykonuje wszystkich testów diagnostycznych hello.</span><span class="sxs-lookup"><span data-stu-id="43668-120">If hello scope parameter is not specified, hello cmdlet executes all hello diagnostic tests.</span></span> <span data-ttu-id="43668-121">Te testy obejmują systemu, kondycja składnika sprzętu, sieci i wydajności.</span><span class="sxs-lookup"><span data-stu-id="43668-121">These tests include system, hardware component health, network, and performance.</span></span> 
    
    <span data-ttu-id="43668-122">toorun tylko określone testy, określ parametr zakresu hello.</span><span class="sxs-lookup"><span data-stu-id="43668-122">toorun only a specific test, specify hello scope parameter.</span></span> <span data-ttu-id="43668-123">Na przykład toorun tylko hello test sieci, typ</span><span class="sxs-lookup"><span data-stu-id="43668-123">For instance, toorun only hello network test, type</span></span>

    `Invoke-HcsDiagnostics -Scope Network`

3. <span data-ttu-id="43668-124">Zaznacz i skopiuj dane wyjściowe hello z hello PuTTY okna do pliku tekstowego w celu dalszej analizy.</span><span class="sxs-lookup"><span data-stu-id="43668-124">Select and copy hello output from hello PuTTY window into a text file for further analysis.</span></span>

## <a name="scenarios-toouse-hello-diagnostics-tool"></a><span data-ttu-id="43668-125">Narzędzie diagnostyczne hello toouse scenariuszy</span><span class="sxs-lookup"><span data-stu-id="43668-125">Scenarios toouse hello diagnostics tool</span></span>

<span data-ttu-id="43668-126">Użyj hello diagnostyki narzędzia tootroubleshoot hello sieci, wydajności systemu i sprzętu kondycję hello systemu.</span><span class="sxs-lookup"><span data-stu-id="43668-126">Use hello diagnostics tool tootroubleshoot hello network, performance, system, and hardware health of hello system.</span></span> <span data-ttu-id="43668-127">Poniżej przedstawiono kilka możliwych scenariuszy:</span><span class="sxs-lookup"><span data-stu-id="43668-127">Here are some possible scenarios:</span></span>

* <span data-ttu-id="43668-128">**Urządzenie w trybie offline** -Your StorSimple 8000 serii urządzenie jest w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="43668-128">**Device offline** - Your StorSimple 8000 series device is offline.</span></span> <span data-ttu-id="43668-129">Z hello interfejsu programu Windows PowerShell, prawdopodobnie czy obu kontrolerów hello są uruchomione i działają prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="43668-129">However, from hello Windows PowerShell interface, it seems that both hello controllers are up and running.</span></span>
    * <span data-ttu-id="43668-130">Za pomocą tego narzędzia toothen określić hello stanu sieci.</span><span class="sxs-lookup"><span data-stu-id="43668-130">You can use this tool toothen determine hello network state.</span></span>
         
         > [!NOTE]
         > <span data-ttu-id="43668-131">Nie należy używać tego narzędzia tooassess wydajności i ustawienia sieciowe na urządzenie przed hello rejestracji (lub konfigurowanie za pomocą Kreatora instalacji).</span><span class="sxs-lookup"><span data-stu-id="43668-131">Do not use this tool tooassess performance and network settings on a device before hello registration (or configuring via setup wizard).</span></span> <span data-ttu-id="43668-132">Prawidłowymi adresami IP są przypisywane toohello urządzenia podczas Kreatora konfiguracji i rejestracji.</span><span class="sxs-lookup"><span data-stu-id="43668-132">A valid IP is assigned toohello device during setup wizard and registration.</span></span> <span data-ttu-id="43668-133">To polecenie cmdlet można uruchomić na urządzeniu, które nie jest zarejestrowane dla kondycji sprzętu i systemu.</span><span class="sxs-lookup"><span data-stu-id="43668-133">You can run this cmdlet, on a device that is not registered, for hardware health and system.</span></span> <span data-ttu-id="43668-134">Parametr hello zakresu, na przykład:</span><span class="sxs-lookup"><span data-stu-id="43668-134">Use hello scope parameter, for example:</span></span>
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* <span data-ttu-id="43668-135">**Problemy dotyczące urządzenia trwałe** — występują problemy dotyczące urządzenia, które wydają się toopersist.</span><span class="sxs-lookup"><span data-stu-id="43668-135">**Persistent device issues** - You are experiencing device issues that seem toopersist.</span></span> <span data-ttu-id="43668-136">Na przykład kończy się niepowodzeniem rejestracji.</span><span class="sxs-lookup"><span data-stu-id="43668-136">For instance, registration is failing.</span></span> <span data-ttu-id="43668-137">Użytkownik może również występować problemy dotyczące urządzenia po urządzenia hello jest pomyślnie zarejestrowane i działa przez pewien czas.</span><span class="sxs-lookup"><span data-stu-id="43668-137">You could also be experiencing device issues after hello device is successfully registered and operational for a while.</span></span>
    * <span data-ttu-id="43668-138">W takim przypadku to narzędzie do wstępnego rozwiązywania problemów przed zalogowaniem się żądania obsługi z Support firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="43668-138">In this case, use this tool for preliminary troubleshooting before you log a service request with Microsoft Support.</span></span> <span data-ttu-id="43668-139">Firma Microsoft zaleca uruchomienie tego narzędzia i przechwytywania hello dane wyjściowe tego narzędzia.</span><span class="sxs-lookup"><span data-stu-id="43668-139">We recommend that you run this tool and capture hello output of this tool.</span></span> <span data-ttu-id="43668-140">Możesz także podać dane wyjściowe tooSupport tooexpedite procedury rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="43668-140">You can then provide this output tooSupport tooexpedite troubleshooting.</span></span>
    * <span data-ttu-id="43668-141">W przypadku dowolnego składnika lub klastra awariami sprzętu należy rejestrować w żądaniu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="43668-141">If there are any hardware component or cluster failures, you should log in a Support request.</span></span>

* <span data-ttu-id="43668-142">**Niska wydajność urządzenia** -Your StorSimple urządzenia jest powolne.</span><span class="sxs-lookup"><span data-stu-id="43668-142">**Low device performance** - Your StorSimple device is slow.</span></span>
    * <span data-ttu-id="43668-143">W takim przypadku Uruchom to polecenie cmdlet z tooperformance zestaw parametrów zakresu.</span><span class="sxs-lookup"><span data-stu-id="43668-143">In this case, run this cmdlet with scope parameter set tooperformance.</span></span> <span data-ttu-id="43668-144">Analizowanie danych wyjściowych hello.</span><span class="sxs-lookup"><span data-stu-id="43668-144">Analyze hello output.</span></span> <span data-ttu-id="43668-145">Pobierz chmury hello opóźnienia odczytu i zapisu.</span><span class="sxs-lookup"><span data-stu-id="43668-145">You get hello cloud read-write latencies.</span></span> <span data-ttu-id="43668-146">Hello używany zgłaszane opóźnienia jako maksymalną docelowy osiągalne, współczynnik niektórych obciążenie hello wewnętrzne przetwarzanie danych, a następnie Wdróż hello obciążeń w systemie hello.</span><span class="sxs-lookup"><span data-stu-id="43668-146">Use hello reported latencies as maximum achievable target, factor in some overhead for hello internal data processing, and then deploy hello workloads on hello system.</span></span> <span data-ttu-id="43668-147">Aby uzyskać więcej informacji, przejdź zbyt[Użyj hello sieci test tootroubleshoot urządzenia wydajności](#network-test).</span><span class="sxs-lookup"><span data-stu-id="43668-147">For more information, go too[Use hello network test tootroubleshoot device performance](#network-test).</span></span>


## <a name="diagnostics-test-and-sample-outputs"></a><span data-ttu-id="43668-148">Wyniki testów i przykładowych diagnostyki</span><span class="sxs-lookup"><span data-stu-id="43668-148">Diagnostics test and sample outputs</span></span>

### <a name="hardware-test"></a><span data-ttu-id="43668-149">Test sprzętu</span><span class="sxs-lookup"><span data-stu-id="43668-149">Hardware test</span></span>

<span data-ttu-id="43668-150">Ten test określa stan hello hello składniki sprzętowe, oprogramowania układowego należy hello i oprogramowanie układowe dysku hello uruchomionych w systemie.</span><span class="sxs-lookup"><span data-stu-id="43668-150">This test determines hello status of hello hardware components, hello USM firmware, and hello disk firmware running on your system.</span></span>

* <span data-ttu-id="43668-151">składniki sprzętowe Hello zgłaszane są te składniki test hello nie powiodło się lub nie są dostępne w systemie hello.</span><span class="sxs-lookup"><span data-stu-id="43668-151">hello hardware components reported are those components that failed hello test or are not present in hello system.</span></span>
* <span data-ttu-id="43668-152">Hello należy oprogramowania układowego i dysku wersji oprogramowania układowego są raportowane hello kontrolera 0 i kontrolera 1 i udostępnionych składników w systemie.</span><span class="sxs-lookup"><span data-stu-id="43668-152">hello USM firmware and disk firmware versions are reported for hello Controller 0, Controller 1, and shared components in your system.</span></span> <span data-ttu-id="43668-153">Aby uzyskać pełną listę składników sprzętowych przejdź do:</span><span class="sxs-lookup"><span data-stu-id="43668-153">For a complete list of hardware components, go to:</span></span>

    * [<span data-ttu-id="43668-154">Składniki w obudowie podstawowego</span><span class="sxs-lookup"><span data-stu-id="43668-154">Components in primary enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [<span data-ttu-id="43668-155">Składniki w obudowie EBOD</span><span class="sxs-lookup"><span data-stu-id="43668-155">Components in EBOD enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> <span data-ttu-id="43668-156">Jeśli test sprzętu hello zgłasza błędne składniki [Zaloguj żądania obsługi ze Microsoft Support](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="43668-156">If hello hardware test reports failed components, [log in a service request with Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a><span data-ttu-id="43668-157">Przykładowe dane wyjściowe testu sprzętu uruchamianie na urządzeniu 8100</span><span class="sxs-lookup"><span data-stu-id="43668-157">Sample output of hardware test run on an 8100 device</span></span>

<span data-ttu-id="43668-158">Oto przykładowe dane wyjściowe z urządzenia StorSimple 8100.</span><span class="sxs-lookup"><span data-stu-id="43668-158">Here is a sample output from a StorSimple 8100 device.</span></span> <span data-ttu-id="43668-159">W urządzeniu modelu 8100 hello hello obudowa EBOD jest nieobecny.</span><span class="sxs-lookup"><span data-stu-id="43668-159">In hello 8100 model device, hello EBOD enclosure is not present.</span></span> <span data-ttu-id="43668-160">W związku z tym hello EBOD kontrolera składniki nie są zgłaszane.</span><span class="sxs-lookup"><span data-stu-id="43668-160">Hence, hello EBOD controller components are not reported.</span></span>

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

### <a name="system-test"></a><span data-ttu-id="43668-161">Test systemu</span><span class="sxs-lookup"><span data-stu-id="43668-161">System test</span></span>

<span data-ttu-id="43668-162">Ten test raporty hello informacje o systemie, dostępne aktualizacje hello, informacje o klastrze hello i hello usługi informacje o urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="43668-162">This test reports hello system information, hello updates available, hello cluster information, and hello service information for your device.</span></span>

* <span data-ttu-id="43668-163">informacje o systemie Hello obejmuje hello modelu, numer seryjny urządzenia strefy czasowej, stan kontrolera i wersji oprogramowania szczegółowe hello uruchomiona w systemie hello.</span><span class="sxs-lookup"><span data-stu-id="43668-163">hello system information includes hello model, device serial number, time zone, controller status, and hello detailed software version running on hello system.</span></span> <span data-ttu-id="43668-164">Witaj toounderstand różnych parametrów systemu zgłoszone jako dane wyjściowe hello, przejdź za[interpretacji informacji o systemie](#appendix-interpreting-system-information).</span><span class="sxs-lookup"><span data-stu-id="43668-164">toounderstand hello various system parameters reported as hello output, go too[Interpreting system information](#appendix-interpreting-system-information).</span></span>

* <span data-ttu-id="43668-165">czy hello tryby zwykłych oraz konserwacji są dostępne raporty Hello dostępności aktualizacji i ich nazw skojarzonego pakietu.</span><span class="sxs-lookup"><span data-stu-id="43668-165">hello update availability reports whether hello regular and maintenance modes are available and their associated package names.</span></span> <span data-ttu-id="43668-166">Jeśli `RegularUpdates` i `MaintenanceModeUpdates` są `false`, oznacza to, że hello aktualizacje nie są dostępne.</span><span class="sxs-lookup"><span data-stu-id="43668-166">If `RegularUpdates` and `MaintenanceModeUpdates` are `false`, this indicates that hello updates are not available.</span></span> <span data-ttu-id="43668-167">Urządzenie jest aktualny.</span><span class="sxs-lookup"><span data-stu-id="43668-167">Your device is up-to-date.</span></span>
* <span data-ttu-id="43668-168">informacje o klastrze Hello zawiera hello informacje na temat różnych składników logicznych wszystkie grupy klastra moduł HCS hello i ich odpowiednich stanów.</span><span class="sxs-lookup"><span data-stu-id="43668-168">hello cluster information contains hello information on various logical components of all hello HCS cluster groups and their respective statuses.</span></span> <span data-ttu-id="43668-169">Jeśli widzisz grupy klastra w trybie offline, w tej sekcji raportu hello [skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="43668-169">If you see an offline cluster group in this section of hello report, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="43668-170">Witaj usługi informacje obejmują hello nazwy i Stanami wszystkich hello moduł HCS i usługi konfiguracji (ci) są uruchomione na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="43668-170">hello service information includes hello names and statuses of all hello HCS and CiS services running on your device.</span></span> <span data-ttu-id="43668-171">Informacje te są przydatne do hello Microsoft Support przy rozwiązywaniu problemu urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="43668-171">This information is helpful for hello Microsoft Support in troubleshooting hello device issue.</span></span>

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a><span data-ttu-id="43668-172">Przykładowe dane wyjściowe testu systemu uruchamianie na urządzeniu 8100</span><span class="sxs-lookup"><span data-stu-id="43668-172">Sample output of system test run on an 8100 device</span></span>

<span data-ttu-id="43668-173">Oto przykładowe dane wyjściowe testu systemu hello uruchamianie na urządzeniu 8100.</span><span class="sxs-lookup"><span data-stu-id="43668-173">Here is a sample output of hello system test run on an 8100 device.</span></span>

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

### <a name="network-test"></a><span data-ttu-id="43668-174">Test sieci</span><span class="sxs-lookup"><span data-stu-id="43668-174">Network test</span></span>

<span data-ttu-id="43668-175">Ten test sprawdza hello stan hello interfejsów sieciowych, porty, DNS i NTP łączności z serwerem, SSL certyfikatu, poświadczeń konta magazynu, łączności toohello aktualizacji serwerów i łączności serwera proxy sieci web na urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="43668-175">This test validates hello status of hello network interfaces, ports, DNS and NTP server connectivity, SSL certificate, storage account credentials, connectivity toohello Update servers, and web proxy connectivity on your StorSimple device.</span></span>

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a><span data-ttu-id="43668-176">Przykładowe dane wyjściowe sieci testów, gdy jest włączona tylko DATA0</span><span class="sxs-lookup"><span data-stu-id="43668-176">Sample output of network test when only DATA0 is enabled</span></span>

<span data-ttu-id="43668-177">Oto przykładowe dane wyjściowe hello 8100 urządzenia.</span><span class="sxs-lookup"><span data-stu-id="43668-177">Here is a sample output of hello 8100 device.</span></span> <span data-ttu-id="43668-178">Można zobaczyć w danych wyjściowych hello który:</span><span class="sxs-lookup"><span data-stu-id="43668-178">You can see in hello output that:</span></span>
* <span data-ttu-id="43668-179">Tylko dane 0 i 1 danych interfejsy sieciowe są włączone i skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="43668-179">Only DATA 0 and DATA 1 network interfaces are enabled and configured.</span></span>
* <span data-ttu-id="43668-180">DANE 2 5 nie są włączone w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="43668-180">DATA 2 - 5 are not enabled in hello portal.</span></span>
* <span data-ttu-id="43668-181">Konfiguracja serwera DNS Hello jest prawidłowy i hello urządzenie można połączyć za pośrednictwem powitania serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="43668-181">hello DNS server configuration is valid and hello device can connect via hello DNS server.</span></span>
* <span data-ttu-id="43668-182">Witaj łączności serwera NTP również funkcjonuje prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="43668-182">hello NTP server connectivity is also fine.</span></span>
* <span data-ttu-id="43668-183">Otwartych portów 80 i 443.</span><span class="sxs-lookup"><span data-stu-id="43668-183">Ports 80 and 443 are open.</span></span> <span data-ttu-id="43668-184">Jednak port 9354 jest zablokowany.</span><span class="sxs-lookup"><span data-stu-id="43668-184">However, port 9354 is blocked.</span></span> <span data-ttu-id="43668-185">Oparte na powitania [wymagania sieciowe systemu](storsimple-system-requirements.md), należy tooopen ten port komunikacji hello magistrali usługi.</span><span class="sxs-lookup"><span data-stu-id="43668-185">Based on hello [system network requirements](storsimple-system-requirements.md), you need tooopen this port for hello service bus communication.</span></span>
* <span data-ttu-id="43668-186">certyfikacji SSL Hello jest prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="43668-186">hello SSL certification is valid.</span></span>
* <span data-ttu-id="43668-187">urządzenie Hello można połączyć konto magazynu toohello: _myss8000storageacct_.</span><span class="sxs-lookup"><span data-stu-id="43668-187">hello device can connect toohello storage account: _myss8000storageacct_.</span></span>
* <span data-ttu-id="43668-188">serwery tooUpdate łączności Hello jest prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="43668-188">hello connectivity tooUpdate servers is valid.</span></span>
* <span data-ttu-id="43668-189">nie skonfigurowano serwera proxy sieci web Hello na tym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="43668-189">hello web proxy is not configured on this device.</span></span>

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a><span data-ttu-id="43668-190">Przykładowe dane wyjściowe testu sieci, gdy są włączone DATA0 i dane1</span><span class="sxs-lookup"><span data-stu-id="43668-190">Sample output of network test when DATA0 and DATA1 are enabled</span></span>

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

### <a name="performance-test"></a><span data-ttu-id="43668-191">Test wydajności</span><span class="sxs-lookup"><span data-stu-id="43668-191">Performance test</span></span>

<span data-ttu-id="43668-192">Ten test raportów wydajności chmury hello za pośrednictwem hello chmury odczytu i zapisu opóźnienia dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="43668-192">This test reports hello cloud performance via hello cloud read-write latencies for your device.</span></span> <span data-ttu-id="43668-193">To narzędzie może być używane tooestablish linię bazową wydajności chmury hello, który można uzyskać z StorSimple.</span><span class="sxs-lookup"><span data-stu-id="43668-193">This tool can be used tooestablish a baseline of hello cloud performance that you can achieve with StorSimple.</span></span> <span data-ttu-id="43668-194">Hello narzędzie raporty hello maksymalną wydajność (najlepsze scenariusz dla opóźnienia odczytu i zapisu), który można uzyskać połączenia.</span><span class="sxs-lookup"><span data-stu-id="43668-194">hello tool reports hello maximum performance (best case scenario for read-write latencies) that you can get for your connection.</span></span>

<span data-ttu-id="43668-195">Jak narzędzie hello zgłasza maksymalną wydajność osiągalne hello, możemy użyć hello zgłosił opóźnienia odczytu i zapisu jako obiekty docelowe, wdrażając hello obciążeń.</span><span class="sxs-lookup"><span data-stu-id="43668-195">As hello tool reports hello maximum achievable performance, we can use hello reported read-write latencies as targets when deploying hello workloads.</span></span>

<span data-ttu-id="43668-196">Badanie Hello symuluje hello rozmiarów obiektu blob skojarzony z typami inny wolumin hello na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="43668-196">hello test simulates hello blob sizes associated with hello different volume types on hello device.</span></span> <span data-ttu-id="43668-197">Do warstwy standardowych i kopii zapasowych woluminów przypiętych lokalnie użyj rozmiar obiektu blob 64 KB.</span><span class="sxs-lookup"><span data-stu-id="43668-197">Regular tiered and backups of locally pinned volumes use a 64 KB blob size.</span></span> <span data-ttu-id="43668-198">Woluminy warstwowe z zaznaczoną opcją archiwum Użyj rozmiar danych obiektu blob 512 KB.</span><span class="sxs-lookup"><span data-stu-id="43668-198">Tiered volumes with archive option checked use 512 KB blob data size.</span></span> <span data-ttu-id="43668-199">Jeśli urządzenie ma woluminów warstwowych i przypiętych lokalnie skonfigurowane, tylko hello testu odpowiedniego too64 KB blob rozmiar danych jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="43668-199">If your device has tiered and locally pinned volumes configured, only hello test corresponding too64 KB blob data size is run.</span></span>

<span data-ttu-id="43668-200">toouse to narzędzie, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="43668-200">toouse this tool, perform hello following steps:</span></span>

1.  <span data-ttu-id="43668-201">Najpierw utwórz mieszane woluminy warstwowe i woluminy warstwowe z zaznaczoną opcją zarchiwizowane.</span><span class="sxs-lookup"><span data-stu-id="43668-201">First, create a mix of tiered volumes and tiered volumes with archived option checked.</span></span> <span data-ttu-id="43668-202">Ta akcja gwarantuje, że narzędzia hello uruchamia testy hello 64 KB i 512 KB rozmiarów obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="43668-202">This action ensures that hello tool runs hello tests for both 64 KB and 512 KB blob sizes.</span></span>

2. <span data-ttu-id="43668-203">Po utworzeniu i skonfigurowanych woluminach hello, należy uruchomić polecenie cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="43668-203">Run hello cmdlet after you have created and configured hello volumes.</span></span> <span data-ttu-id="43668-204">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="43668-204">Type:</span></span>

    `Invoke-HcsDiagnostics -Scope Performance`

3. <span data-ttu-id="43668-205">Zanotuj opóźnienia odczytu i zapisu hello zgłoszone przez narzędzie hello.</span><span class="sxs-lookup"><span data-stu-id="43668-205">Make a note of hello read-write latencies reported by hello tool.</span></span> <span data-ttu-id="43668-206">Ten test może upłynąć kilka minut toorun zgłasza wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="43668-206">This test can take several minutes toorun before it reports hello results.</span></span>

4. <span data-ttu-id="43668-207">W przypadku opóźnienia połączenia hello wszystko pod hello oczekiwano zakresu, a następnie hello opóźnienia zgłoszone przez narzędzie hello mogą być używane jako maksymalną osiągalne docelowego podczas wdrażania hello obciążeń.</span><span class="sxs-lookup"><span data-stu-id="43668-207">If hello connection latencies are all under hello expected range, then hello latencies reported by hello tool can be used as maximum achievable target when deploying hello workloads.</span></span> <span data-ttu-id="43668-208">Współczynnik niektórych obciążenie przetwarzania danych wewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="43668-208">Factor in some overhead for internal data processing.</span></span>

    <span data-ttu-id="43668-209">Jeśli opóźnienia odczytu i zapisu hello zgłoszone przez narzędzie Diagnostyka hello są wysokiej:</span><span class="sxs-lookup"><span data-stu-id="43668-209">If hello read-write latencies reported by hello diagnostics tool are high:</span></span>

    1. <span data-ttu-id="43668-210">Konfigurowanie magazynu Analytics usług obiektów blob i analizowanie hello dane wyjściowe toounderstand hello opóźnienia dla hello kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="43668-210">Configure Storage Analytics for blob services and analyze hello output toounderstand hello latencies for hello Azure storage account.</span></span> <span data-ttu-id="43668-211">Aby uzyskać szczegółowe instrukcje, przejdź zbyt[włączyć i skonfigurować analityka magazynu](../storage/common/storage-enable-and-view-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="43668-211">For detailed instructions, go too[enable and configure Storage Analytics](../storage/common/storage-enable-and-view-metrics.md).</span></span> <span data-ttu-id="43668-212">Jeśli te opóźnienia również są liczbami toohello wysokiej i porównywanie, otrzymany od hello narzędzia diagnostycznego StorSimple, należy toolog żądanie usługi z usługą Azure storage.</span><span class="sxs-lookup"><span data-stu-id="43668-212">If those latencies are also high and comparable toohello numbers you received from hello StorSimple Diagnostics tool, then you need toolog a service request with Azure storage.</span></span>

    2. <span data-ttu-id="43668-213">Jeśli opóźnienia konta magazynu hello niski, skontaktuj się z Twojego tooinvestigate administratora sieci opóźnienia wszelkie problemy w sieci.</span><span class="sxs-lookup"><span data-stu-id="43668-213">If hello storage account latencies are low, contact your network administrator tooinvestigate any latency issues in your network.</span></span>

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a><span data-ttu-id="43668-214">Przykładowe dane wyjściowe uruchamiać na urządzeniu 8100 testu wydajności</span><span class="sxs-lookup"><span data-stu-id="43668-214">Sample output of performance test run on an 8100 device</span></span>

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

## <a name="appendix-interpreting-system-information"></a><span data-ttu-id="43668-215">Dodatku: informacje o systemie interpretowanie</span><span class="sxs-lookup"><span data-stu-id="43668-215">Appendix: interpreting system information</span></span>

<span data-ttu-id="43668-216">W tym miejscu znajduje się tabela opisujące jaki hello mapowania różnych parametrów środowiska Windows PowerShell w hello informacje o systemie.</span><span class="sxs-lookup"><span data-stu-id="43668-216">Here is a table describing what hello various Windows PowerShell parameters in hello system information map to.</span></span> 

| <span data-ttu-id="43668-217">Parametr programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="43668-217">PowerShell Parameter</span></span>    | <span data-ttu-id="43668-218">Opis</span><span class="sxs-lookup"><span data-stu-id="43668-218">Description</span></span>  |
|-------------------------|------------------|
| <span data-ttu-id="43668-219">Identyfikator wystąpienia</span><span class="sxs-lookup"><span data-stu-id="43668-219">Instance ID</span></span>             | <span data-ttu-id="43668-220">Każdy kontroler ma unikatowego identyfikatora lub identyfikator GUID skojarzony z nim.</span><span class="sxs-lookup"><span data-stu-id="43668-220">Every controller has a unique identifier or a GUID associated with it.</span></span>|
| <span data-ttu-id="43668-221">Nazwa</span><span class="sxs-lookup"><span data-stu-id="43668-221">Name</span></span>                    | <span data-ttu-id="43668-222">Witaj przyjazna nazwa urządzenia hello zgodnie z konfiguracją za pośrednictwem portalu Azure hello podczas wdrażania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="43668-222">hello friendly name of hello device as configured through hello Azure portal during device deployment.</span></span> <span data-ttu-id="43668-223">Przyjazna nazwa domyślna Hello jest numer seryjny urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="43668-223">hello default friendly name is hello device serial number.</span></span> |
| <span data-ttu-id="43668-224">Model</span><span class="sxs-lookup"><span data-stu-id="43668-224">Model</span></span>                   | <span data-ttu-id="43668-225">model Hello urządzenia serii StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="43668-225">hello model of your StorSimple 8000 series device.</span></span> <span data-ttu-id="43668-226">Hello model może być 8100 lub 8600.</span><span class="sxs-lookup"><span data-stu-id="43668-226">hello model can be 8100 or 8600.</span></span>|
| <span data-ttu-id="43668-227">numer seryjny</span><span class="sxs-lookup"><span data-stu-id="43668-227">SerialNumber</span></span>            | <span data-ttu-id="43668-228">numer seryjny urządzenia Hello przydzielono fabryki hello i 15 znaków.</span><span class="sxs-lookup"><span data-stu-id="43668-228">hello device serial number is assigned at hello factory and is 15 characters long.</span></span> <span data-ttu-id="43668-229">Wskazuje, na przykład 8600 SHX0991003G44HT:</span><span class="sxs-lookup"><span data-stu-id="43668-229">For instance, 8600-SHX0991003G44HT indicates:</span></span><br> <span data-ttu-id="43668-230">8600 — jest hello model urządzenia.</span><span class="sxs-lookup"><span data-stu-id="43668-230">8600 – Is hello device model.</span></span><br><span data-ttu-id="43668-231">SHX — jest hello produkcyjny lokacji.</span><span class="sxs-lookup"><span data-stu-id="43668-231">SHX – Is hello manufacturing site.</span></span><br> <span data-ttu-id="43668-232">0991003 — jest określony produkt.</span><span class="sxs-lookup"><span data-stu-id="43668-232">0991003 - Is a specific product.</span></span> <br> <span data-ttu-id="43668-233">Unikatowe numery seryjne toocreate zwiększany G44HT-hello są ostatnich 5 cyfr.</span><span class="sxs-lookup"><span data-stu-id="43668-233">G44HT- hello last 5 digits are incremented toocreate unique serial numbers.</span></span> <span data-ttu-id="43668-234">Nie można sekwencyjnych zestawu.</span><span class="sxs-lookup"><span data-stu-id="43668-234">This may not be a sequential set.</span></span>|
| <span data-ttu-id="43668-235">Strefa czasowa</span><span class="sxs-lookup"><span data-stu-id="43668-235">TimeZone</span></span>                | <span data-ttu-id="43668-236">Witaj urządzenia strefa czasowa zgodnie z konfiguracją hello portalu Azure podczas wdrażania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="43668-236">hello device time zone as configured in hello Azure portal during device deployment.</span></span>|
| <span data-ttu-id="43668-237">CurrentController</span><span class="sxs-lookup"><span data-stu-id="43668-237">CurrentController</span></span>       | <span data-ttu-id="43668-238">Kontroler Hello czy interfejsu programu Windows PowerShell hello toothrough podłączonego urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="43668-238">hello controller that you are connected toothrough hello Windows PowerShell interface of your StorSimple device.</span></span>|
| <span data-ttu-id="43668-239">ActiveController</span><span class="sxs-lookup"><span data-stu-id="43668-239">ActiveController</span></span>        | <span data-ttu-id="43668-240">Kontroler Hello jest aktywna na urządzeniu, który kontroluje wszystkie operacje hello sieci i dysku.</span><span class="sxs-lookup"><span data-stu-id="43668-240">hello controller that is active on your device and is controlling all hello network and disk operations.</span></span> <span data-ttu-id="43668-241">Może to być kontrolera 0 i kontrolera 1.</span><span class="sxs-lookup"><span data-stu-id="43668-241">This can be Controller 0 or Controller 1.</span></span>  |
| <span data-ttu-id="43668-242">Controller0Status</span><span class="sxs-lookup"><span data-stu-id="43668-242">Controller0Status</span></span>       | <span data-ttu-id="43668-243">Stan Hello kontrolera 0 na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="43668-243">hello status of Controller 0 on your device.</span></span> <span data-ttu-id="43668-244">Stan kontrolera Hello może być normalna w trybie odzyskiwania lub jest niedostępny.</span><span class="sxs-lookup"><span data-stu-id="43668-244">hello controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="43668-245">Controller1Status</span><span class="sxs-lookup"><span data-stu-id="43668-245">Controller1Status</span></span>       | <span data-ttu-id="43668-246">Witaj stan kontrolera 1 na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="43668-246">hello status of Controller 1 on your device.</span></span>  <span data-ttu-id="43668-247">Stan kontrolera Hello może być normalna w trybie odzyskiwania lub jest niedostępny.</span><span class="sxs-lookup"><span data-stu-id="43668-247">hello controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="43668-248">SystemMode</span><span class="sxs-lookup"><span data-stu-id="43668-248">SystemMode</span></span>              | <span data-ttu-id="43668-249">Witaj ogólny stan urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="43668-249">hello overall status of your StorSimple device.</span></span> <span data-ttu-id="43668-250">Stan urządzenia Hello może być normalne, konserwacji lub wycofany z eksploatacji (odpowiada toodeactivated w hello portalu Azure).</span><span class="sxs-lookup"><span data-stu-id="43668-250">hello device status can be normal, maintenance, or decommissioned (corresponds toodeactivated in hello Azure portal).</span></span>|
| <span data-ttu-id="43668-251">FriendlySoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="43668-251">FriendlySoftwareVersion</span></span> | <span data-ttu-id="43668-252">Witaj przyjazną ciąg, który odpowiada wersji oprogramowania toohello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="43668-252">hello friendly string that corresponds toohello device software version.</span></span> <span data-ttu-id="43668-253">Komputerze z systemem aktualizacji 4 wersja oprogramowania przyjazną hello będzie StorSimple 8000 serii aktualizacji 4.0.</span><span class="sxs-lookup"><span data-stu-id="43668-253">For a system running Update 4, hello friendly software version would be StorSimple 8000 Series Update 4.0.</span></span>|
| <span data-ttu-id="43668-254">HcsSoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="43668-254">HcsSoftwareVersion</span></span>      | <span data-ttu-id="43668-255">wersji oprogramowania moduł HCS Hello działającej na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="43668-255">hello HCS software version running on your device.</span></span> <span data-ttu-id="43668-256">Na przykład Witaj odpowiedniego tooStorSimple wersji oprogramowania moduł HCS 8000 serii aktualizacji 4.0 jest 6.3.9600.17820.</span><span class="sxs-lookup"><span data-stu-id="43668-256">For instance, hello HCS software version corresponding tooStorSimple 8000 Series Update 4.0 is 6.3.9600.17820.</span></span> |
| <span data-ttu-id="43668-257">ApiVersion</span><span class="sxs-lookup"><span data-stu-id="43668-257">ApiVersion</span></span>              | <span data-ttu-id="43668-258">Wersja oprogramowania Hello hello interfejsu API programu PowerShell systemu Windows hello moduł HCS urządzenia.</span><span class="sxs-lookup"><span data-stu-id="43668-258">hello software version of hello Windows PowerShell API of hello HCS device.</span></span>|
| <span data-ttu-id="43668-259">VhdVersion</span><span class="sxs-lookup"><span data-stu-id="43668-259">VhdVersion</span></span>              | <span data-ttu-id="43668-260">Wersja oprogramowania Hello hello fabryki obrazu, który hello urządzenia został wysłany z.</span><span class="sxs-lookup"><span data-stu-id="43668-260">hello software version of hello factory image that hello device was shipped with.</span></span> <span data-ttu-id="43668-261">Po zresetowaniu urządzenia domyślnych toofactory uruchomieniu tej wersji oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="43668-261">If you reset your device toofactory defaults, then it runs this software version.</span></span>|
| <span data-ttu-id="43668-262">OSVersion</span><span class="sxs-lookup"><span data-stu-id="43668-262">OSVersion</span></span>               | <span data-ttu-id="43668-263">wersja systemu operacyjnego Windows Server hello działającej na urządzeniu hello oprogramowania Hello.</span><span class="sxs-lookup"><span data-stu-id="43668-263">hello software version of hello Windows Server operating system running on hello device.</span></span> <span data-ttu-id="43668-264">urządzenia StorSimple Hello opiera się poza hello systemu Windows Server 2012 R2, który odpowiada too6.3.9600.</span><span class="sxs-lookup"><span data-stu-id="43668-264">hello StorSimple device is based off hello Windows Server 2012 R2 that corresponds too6.3.9600.</span></span>|
| <span data-ttu-id="43668-265">CisAgentVersion</span><span class="sxs-lookup"><span data-stu-id="43668-265">CisAgentVersion</span></span>         | <span data-ttu-id="43668-266">Wersja Hello agenta konfiguracji (ci) uruchomione na urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="43668-266">hello version for your Cis agent running on your StorSimple device.</span></span> <span data-ttu-id="43668-267">Ten agent pomaga komunikować się z usługą Menedżer StorSimple hello działające na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="43668-267">This agent helps communicate with hello StorSimple Manager service running in Azure.</span></span>|
| <span data-ttu-id="43668-268">MdsAgentVersion</span><span class="sxs-lookup"><span data-stu-id="43668-268">MdsAgentVersion</span></span>         | <span data-ttu-id="43668-269">Witaj wersji odpowiedniego toohello Mds agenta uruchomionego na urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="43668-269">hello version corresponding toohello Mds agent running on your StorSimple device.</span></span> <span data-ttu-id="43668-270">Ten agent przenosi toohello danych monitorowania i diagnostyki usługi (MDS).</span><span class="sxs-lookup"><span data-stu-id="43668-270">This agent moves data toohello Monitoring and Diagnostics Service (MDS).</span></span>|
| <span data-ttu-id="43668-271">Lsisas2Version</span><span class="sxs-lookup"><span data-stu-id="43668-271">Lsisas2Version</span></span>          | <span data-ttu-id="43668-272">Witaj odpowiednich sterowników toohello LSI wersji na urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="43668-272">hello version corresponding toohello LSI drivers on your StorSimple device.</span></span>|
| <span data-ttu-id="43668-273">Pojemność</span><span class="sxs-lookup"><span data-stu-id="43668-273">Capacity</span></span>                | <span data-ttu-id="43668-274">Całkowita pojemność Hello urządzenia hello w bajtach.</span><span class="sxs-lookup"><span data-stu-id="43668-274">hello total capacity of hello device in bytes.</span></span>|
| <span data-ttu-id="43668-275">RemoteManagementMode</span><span class="sxs-lookup"><span data-stu-id="43668-275">RemoteManagementMode</span></span>    | <span data-ttu-id="43668-276">Wskazuje, czy urządzenie hello mogą być zarządzane zdalnie za pośrednictwem jej interfejsu programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="43668-276">Indicates whether hello device can be remotely managed via its Windows PowerShell interface.</span></span> |
| <span data-ttu-id="43668-277">FipsMode</span><span class="sxs-lookup"><span data-stu-id="43668-277">FipsMode</span></span>                | <span data-ttu-id="43668-278">Wskazuje, czy tryb Stanów Zjednoczonych informacji przetwarzania Standard FIPS (Federal) hello jest włączony na twoim urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="43668-278">Indicates whether hello United States Federal Information Processing Standard (FIPS) mode is enabled on your device.</span></span> <span data-ttu-id="43668-279">standard Hello FIPS 140 definiuje zatwierdzone do użycia przez nas federalne systemów komputerowych dla instytucji rządowych hello ochrony danych poufnych algorytmów kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="43668-279">hello FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for hello protection of sensitive data.</span></span> <span data-ttu-id="43668-280">W przypadku urządzeń programu Update 4 lub nowszego trybie FIPS jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="43668-280">For devices running Update 4 or later, FIPS mode is enabled by default.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="43668-281">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="43668-281">Next steps</span></span>

* <span data-ttu-id="43668-282">Dowiedz się hello [składni polecenia cmdlet Invoke-HcsDiagnostics hello](https://technet.microsoft.com/library/mt795371.aspx).</span><span class="sxs-lookup"><span data-stu-id="43668-282">Learn hello [syntax of hello Invoke-HcsDiagnostics cmdlet](https://technet.microsoft.com/library/mt795371.aspx).</span></span>

* <span data-ttu-id="43668-283">Dowiedz się więcej o tym, jak za[Rozwiązywanie problemów dotyczących wdrożenia](storsimple-troubleshoot-deployment.md) na urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="43668-283">Learn more about how too[troubleshoot deployment issues](storsimple-troubleshoot-deployment.md) on your StorSimple device.</span></span>
