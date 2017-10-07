---
title: "udziału plików StorSimple aaaAutomate odzyskiwania po awarii z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano kroki hello i najlepsze rozwiązania dotyczące tworzenia rozwiązanie odzyskiwania po awarii dla udziałów plików hostowane na magazynu Microsoft Azure StorSimple."
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 23049a2c-055e-4d0e-b8f5-af2a87ecf53f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/09/2017
ms.author: vidarmsft
ms.openlocfilehash: fa3e8d4e77ca0f6a7b5f9bbb956a4de12547642e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automated-disaster-recovery-solution-using-azure-site-recovery-for-file-shares-hosted-on-storsimple"></a>Zautomatyzowane rozwiązanie odzyskiwania po awarii dla udziałów plików hostowane na StorSimple przy użyciu usługi Azure Site Recovery
## <a name="overview"></a>Omówienie
Microsoft Azure StorSimple jest rozwiązanie magazynu hybrydowego chmury, które adresy hello złożoności danych niestrukturalnych zwykle powiązanych ze udziałów plików. StorSimple używa magazynu w chmurze rozszerzenie hello lokalnego rozwiązania i automatycznie warstwy danych przez Magazyn lokalny i magazynu w chmurze. Zintegrowana ochrony danych z lokalnego i w chmurze migawek, eliminuje potrzebę hello sprawling infrastruktury magazynu.

[Usługa Azure Site Recovery](../site-recovery/site-recovery-overview.md) to usługa bazujących na platformie Azure, która zapewnia możliwości odzyskiwanie po awarii poprzez organizowanie replikacji, trybu failover i odzyskiwania maszyn wirtualnych. Usługa Azure Site Recovery obsługuje wiele replikowania tooconsistently technologii replikacji, ochrony i awaryjnie za pośrednictwem chmury tooprivate/public lub hostowanych maszyn wirtualnych i aplikacji.

Za pomocą usługi Azure Site Recovery, replikację maszyny wirtualnej i tworzenie migawek chmury StorSimple, można chronić środowiska serwera na zakończenie pliku hello. W przypadku hello przerw w działaniu można użyć toobring jednym kliknięciem, z udziałów plików online na platformie Azure w ciągu kilku minut.

Tego dokumentu szczegółowo opisano sposób można utworzyć rozwiązanie odzyskiwania po awarii dla Twojego udziały plików hostowane na magazynie StorSimple i wykonać planowane, nieplanowane i testy trybu failover przy użyciu planu odzyskiwania jednym kliknięciem. W zasadzie pokazuje, jak można zmodyfikować hello planu odzyskiwania z usługi Azure Site Recovery tooenable magazynu StorSimple w tryb failover podczas scenariuszach po awarii. Ponadto opisano obsługiwane konfiguracje i wymagania wstępne. Tym dokumencie przyjęto założenie, że czytelnik zna hello podstawowe informacje dotyczące architektury usługi Azure Site Recovery i StorSimple.

## <a name="supported-azure-site-recovery-deployment-options"></a>Obsługiwane opcje wdrażania usługi Azure Site Recovery
Klienci mogą wdrażania serwerów plików jako serwerów fizycznych lub maszynach wirtualnych (VM) działające w funkcji Hyper-V lub programu VMware, a następnie utwórz udziałów plików z woluminów używać poza magazynu StorSimple. Usługa Azure Site Recovery może chronić tooeither zarówno fizyczne i wirtualne wdrożenia lokacji dodatkowej lub tooAzure. W tym dokumencie opisano szczegóły rozwiązanie odzyskiwania po awarii z platformy Azure jako lokacja odzyskiwania powitania serwera plików, maszyna wirtualna hostowana w ramach funkcji Hyper-V i udziałów plików w magazynie StorSimple. Podobnie można stosować inne scenariusze, w których serwer plików hello maszyna wirtualna jest na maszynie Wirtualnej VMware lub komputera fizycznego.

## <a name="prerequisites"></a>Wymagania wstępne
Implementowanie rozwiązania odzyskiwania po awarii jednego kliknięcia, które używa usługi Azure Site Recovery udziały plików hostowane na magazynie StorSimple ma hello następujące wymagania wstępne:

* Lokalnego serwera z systemem Windows Server 2012 R2 pliku, maszyna wirtualna hostowana w funkcji Hyper-V lub programu VMware lub komputera fizycznego
* StorSimple urządzenia lokalnie zarejestrowana w usłudze Menedżer Azure StorSimple
* Urządzenia StorSimple chmury, utworzony w hello Azure StorSimple manager (to może znajdować się w stanie zamykanie)
* Udziały plików hostowane na woluminach hello skonfigurowane na urządzeniu magazynującym hello StorSimple
* [Magazynu usługi Azure Site Recovery](../site-recovery/site-recovery-vmm-to-vmm.md) utworzone w ramach subskrypcji Microsoft Azure

Azure w przypadku odzyskiwania lokacji, uruchom hello [narzędzie oceny gotowości maszyny wirtualnej Azure](http://azure.microsoft.com/downloads/vm-readiness-assessment/) na tooensure maszyn wirtualnych, że są one zgodne z maszynami wirtualnymi Azure i usługi Azure Site Recovery services.

tooavoid opóźnień (co może spowodować zwiększenie kosztów), upewnij się, że tworzenia urządzenia StorSimple chmury konta automatyzacji i tym samym regionie hello kont magazynu w.

## <a name="enable-dr-for-storsimple-file-shares"></a>Włącz odzyskiwania po awarii dla udziałów plików StorSimple
Każdy składnik hello w lokalnym środowisku potrzebuje toobe chronione tooenable dokończenie replikacji i odzyskiwania. W tej sekcji opisano sposób:

* Konfigurowanie replikacji usługi Active Directory i DNS (opcjonalny)
* Korzystanie z usługi Azure Site Recovery tooenable ochrony powitania serwera plików maszyny Wirtualnej
* Włączanie ochrony woluminów StorSimple
* Skonfiguruj sieć hello

### <a name="set-up-active-directory-and-dns-replication-optional"></a>Konfigurowanie replikacji usługi Active Directory i DNS (opcjonalny)
Jeśli chcesz hello tooprotect komputerów z systemem usługi Active Directory i DNS, tak aby były dostępne w witrynie hello odzyskiwania po awarii, należy tooexplicitly je chronić (tak, aby serwery plików hello są dostępne po pracy awaryjnej z uwierzytelnianiem). Istnieją dwie opcje zalecane oparte na powitania złożoność powitania klienta w środowisku lokalnym.

#### <a name="option-1"></a>Opcja 1
Jeśli powitania klienta ma małej liczby aplikacji, jednego kontrolera domeny dla całej hello lokalnej lokacji i będzie można przechodzenie w tryb failover hello całej lokacji, zaleca się używanie maszyny kontrolera domeny hello tooreplicate replikacji usługi Azure Site Recovery, a następnie tooa lokacji dodatkowej (dotyczy to zarówno do lokacji i lokacji do platformy Azure).

#### <a name="option-2"></a>Opcja 2
Jeśli powitania klienta ma dużą liczbę aplikacji, działa lasu usługi Active Directory, a jednocześnie będzie awaryjne kilka aplikacji, a następnie zalecamy skonfigurowanie dodatkowego kontrolera domeny w lokacji hello DR (dodatkowej lokacji lub na platformie Azure).

Zobacz zbyt[rozwiązania automatycznego odzyskiwania po awarii dla usługi Active Directory i DNS za pomocą usługi Azure Site Recovery](../site-recovery/site-recovery-active-directory.md) instrukcje podczas udostępniania kontrolera domeny na powitania odzyskiwania po awarii lokacji. Witaj pozostałej części tego dokumentu będzie przyjęto założenie, że kontroler domeny jest dostępny na powitania odzyskiwania po awarii lokacji.

### <a name="use-azure-site-recovery-tooenable-protection-of-hello-file-server-vm"></a>Korzystanie z usługi Azure Site Recovery tooenable ochrony powitania serwera plików maszyny Wirtualnej
Ten krok wymaga przygotowanie środowiska serwera plików lokalne powitania, Utwórz i przygotuj magazyn Azure Site Recovery i włączyć ochronę pliku hello maszyny Wirtualnej.

#### <a name="tooprepare-hello-on-premises-file-server-environment"></a>Witaj tooprepare lokalnego środowiska serwera plików
1. Zestaw hello **Kontrola konta użytkownika** za**nigdy nie Powiadamiaj**. Jest to wymagane, dzięki czemu można użyć obiektów docelowych iSCSI hello tooconnect skryptów automatyzacji Azure po błędów przez usługi Azure Site Recovery.

   1. Naciśnij klawisze Windows hello + Q i wyszukaj **UAC**.
   2. Wybierz **ustawienia kontroli konta użytkownika zmiany**.
   3. Witaj przeciągnij pasek dołu toohello **nigdy nie Powiadamiaj**.
   4. Kliknij przycisk **OK** , a następnie wybierz **tak** po wyświetleniu monitu.

      ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image1.png)
2. Hello agenta maszyny Wirtualnej należy zainstalować na każdym serwerze plików hello maszyn wirtualnych. Jest to wymagane, co umożliwia uruchamianie skryptów automatyzacji Azure na powitania przejścia w tryb failover maszyn wirtualnych.

   1. [Pobierz agenta hello](http://aka.ms/vmagentwin) zbyt`C:\\Users\\<username>\\Downloads`.
   2. Otwórz program Windows PowerShell w trybie administratora (Uruchom jako Administrator), a następnie wprowadź powitania po lokalizacji pobierania toohello toonavigate polecenia:

      `cd C:\\Users\\<username>\\Downloads\\WindowsAzureVmAgent.2.6.1198.718.rd\_art\_stable.150415-1739.fre.msi`

      > [!NOTE]
      > Nazwa pliku Hello mogą ulec zmianie w zależności od wersji powitania.
      >
      >
3. Kliknij przycisk **Dalej**.
4. Zaakceptuj hello **postanowienia Umowy** , a następnie kliknij przycisk **dalej**.
5. Kliknij przycisk **Zakończ**.
6. Tworzenie udziałów plików za pomocą woluminów używać poza magazynu StorSimple. Aby uzyskać więcej informacji, zobacz [korzysta z woluminów toomanage usługi Menedżer StorSimple hello](storsimple-manage-volumes.md).

   1. Na lokalnych maszyn wirtualnych, naciśnij klawisz systemu Windows hello + Q, a następnie wyszukaj **iSCSI**.
   2. Wybierz **inicjatora iSCSI**.
   3. Wybierz hello **konfiguracji** Nazwa inicjatora hello kartę i kopii.
   4. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).
   5. Wybierz hello **StorSimple** karcie, a następnie wybierz hello usługi Menedżer StorSimple, która zawiera hello urządzenia fizycznego.
   6. Utwórz wolumin kontenerów, a następnie utwórz woluminy. (Te woluminy są hello udziałów plików na serwerze plików hello maszyn wirtualnych). Skopiuj Nazwa inicjatora hello i zapewniają odpowiednią nazwę hello rekordy kontroli dostępu, podczas tworzenia hello woluminów.
   7. Wybierz hello **Konfiguruj** kartę i zanotuj adres IP hello hello urządzenia.
   8. W przypadku maszyn wirtualnych lokalnie, przejść toohello **inicjatora iSCSI** ponownie, a następnie wprowadź hello IP w hello sekcji szybkie połączenie. Kliknij przycisk **szybkie połączenie** (hello urządzenie powinno być teraz połączone).
   9. Otwórz hello portalu Azure i wybierz hello **woluminów i urządzeń** kartę. Kliknij przycisk **automatycznie skonfigurować**. powinna zostać wyświetlona Hello woluminu, który został właśnie utworzony.
   10. W portalu hello wybierz hello **urządzeń** karcie, a następnie wybierz **utworzyć nowe urządzenie wirtualne.** (Będzie można używać tego urządzenia wirtualnego, jeśli do pracy awaryjnej). Tym nowym urządzeniu wirtualnym można przechowywać w tooavoid stanu offline dodatkowych kosztów. tootake hello urządzenia wirtualnego w trybie offline, przejdź do pozycji toohello **maszyn wirtualnych** sekcji na powitania portalu i zamykają ją.
   11. Przejdź wstecz toohello lokalnych maszyn wirtualnych i Otwórz przystawkę Zarządzanie dyskami (naciśnij klawisz systemu Windows hello + X i wybierz **Zarządzanie dyskami**).
   12. Można zauważyć pewne dodatkowe dysków (w zależności od liczby hello woluminów, które utworzono). Kliknij prawym przyciskiem myszy hello pierwszego z nich, zaznacz **Inicjowanie dysku**i wybierz **OK**. Kliknij prawym przyciskiem myszy hello **Unallocated** zaznacz **nowy wolumin prosty**, a następnie przypisać jej literę dysku i zakończyć pracę kreatora hello.
   13. Powtórz krok l dla wszystkich dysków hello. Teraz można wyświetlić wszystkie dyski hello na **ten komputer** w Eksploratorze Windows hello.
   14. Użyj hello usług plików i magazynowania roli toocreate udziałów plików na tych woluminach.

#### <a name="toocreate-and-prepare-an-azure-site-recovery-vault"></a>toocreate i przygotuj magazyn Azure Site Recovery
Zobacz toohello [dokumentacji usługi Azure Site Recovery](../site-recovery/site-recovery-hyper-v-site-to-azure.md) tooget wprowadzenie do usługi Azure Site Recovery przed rozpoczęciem ochrony powitania serwera plików maszyny Wirtualnej.

#### <a name="tooenable-protection"></a>tooenable ochrony
1. Odłącz hello iSCSI docelowych z hello lokalnych maszyn wirtualnych, które mają tooprotect za pośrednictwem usługi Azure Site Recovery:

   1. Naciśnij klawisze Windows + Q i wyszukaj **iSCSI**.
   2. Wybierz **Konfigurowanie inicjatora iSCSI**.
   3. Odłącz urządzenia StorSimple hello, którą wcześniej połączenia. Alternatywnie możesz wyłączyć powitania serwera plików, kilka minut po włączeniu ochrony.

   > [!NOTE]
   > Spowoduje to toobe udziały plików hello jest tymczasowo niedostępny.
   >
   >
2. [Włącz ochronę maszyny wirtualnej](../site-recovery/site-recovery-hyper-v-site-to-azure.md) powitania serwera plików maszyny Wirtualnej w portalu usługi Azure Site Recovery hello.
3. Po rozpoczęciu hello wstępnej synchronizacji, można ponownie hello docelowej. Przejdź toohello inicjatora iSCSI, wybierz hello urządzenia StorSimple, a następnie kliknij przycisk **Connect**.
4. Po ukończeniu synchronizacji hello i jest w stanie hello hello wirtualna **chronione**wybierz hello maszyny Wirtualnej, wybierz hello **Konfiguruj** , a następnie odpowiednio zaktualizować hello sieci hello maszyny Wirtualnej (jest to hello sieci tego hello przejścia w tryb failover wirtualne będą częścią.) Sieci hello nie widać, oznacza, że synchronizacji hello nadal trwa.

### <a name="enable-protection-of-storsimple-volumes"></a>Włączanie ochrony woluminów StorSimple
Jeśli nie wybrano hello **włączyć domyślnego tworzenia kopii zapasowej dla tego woluminu** hello woluminów StorSimple, należy przejść za**zasad tworzenia kopii zapasowych** w hello usługi Menedżer StorSimple, a tworzenie kopii zapasowej odpowiedniego zasady dla wszystkich woluminów hello. Firma Microsoft zaleca ustawienie częstotliwości kopii zapasowych toohello cel punktu odzyskiwania (RPO) ma toosee dla aplikacji hello hello.

### <a name="configure-hello-network"></a>Skonfiguruj sieć hello
Dla serwera plików hello maszyny Wirtualnej należy skonfigurować ustawienia sieciowe w usłudze Azure Site Recovery tak, aby hello sieci maszyn wirtualnych są dołączone toohello poprawnej odzyskiwania po awarii sieci po pracy awaryjnej.

Możesz wybrać hello maszyny Wirtualnej w hello **elementy replikowane** karcie Ustawienia sieciowe hello tooconfigure, jak pokazano na następującej ilustracji hello.

![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image2.png)

## <a name="create-a-recovery-plan"></a>Tworzenie planu odzyskiwania
Funkcja automatycznego odzyskiwania systemu tooautomate hello trybu failover procesu hello udziałów plików, można utworzyć planu odzyskiwania. W przypadku przerw w działaniu przełączeniem udziałów plików hello w ciągu kilku minut za pomocą jednego kliknięcia. tooenable taką automatyzację, musisz mieć konto usługi Automatyzacja Azure.

#### <a name="toocreate-an-automation-account"></a>toocreate konto automatyzacji
1. Przejdź do portalu Azure toohello &gt; **automatyzacji** sekcji.
2. Kliknij przycisk **+ Dodaj** przycisku, otwiera poniżej bloku.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image11.png)

   * Name — wprowadź nowe konto automatyzacji
   * Subskrypcja — Wybierz subskrypcję
   * Resource group - Utwórz nowe/wybierz istniejącą grupę zasobów
   * Lokalizacja — wybierz lokalizację, przechowuj go w hello tego samego geograficznie/regionu, w których hello urządzenia chmury StorSimple i konta magazynu zostały utworzone.
   * Utwórz konto Uruchom jako platformy Azure — wybierz **tak** opcji.

3. Przejdź do konta automatyzacji toohello, kliknij przycisk **elementów Runbook** &gt; **galerii przeglądania** tooimport hello wszystkie wymagane elementy runbook pod uwagę automatyzacji hello.
4. Dodaj następujące elementy runbook znajdując hello **odzyskiwania po awarii** tag w galerii hello:

   * Wyczyść woluminów StorSimple po Test pracy awaryjnej (TFO)
   * Kontenery woluminów StorSimple trybu failover
   * Zainstalować woluminów na urządzeniu StorSimple po pracy awaryjnej
   * Odinstaluj niestandardowego rozszerzenia skryptu na maszynie Wirtualnej Azure
   * Uruchom urządzenia wirtualnego StorSimple

     ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image3.png)

5. Publikuj wszystkie skrypty hello wybierając hello runbook na koncie automatyzacji hello, a następnie kliknij przycisk **Edytuj** &gt; **publikowania** , a następnie **tak** toohello weryfikacji Komunikat. Po wykonaniu tego kroku hello **elementów Runbook** karta pojawi się w następujący sposób:

    ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image4.png)

6. Konto automatyzacji hello, wybierz hello **zasoby** kartę &gt; kliknij **zmienne** &gt; **dodać zmienną** i dodaj następujące zmienne hello. Możesz wybrać tooencrypt tych zasobów. Te zmienne są specyficzne dla planu odzyskiwania. Jeśli odzyskiwania (który zostanie utworzony w następnym kroku hello) nazwa jest TestPlan, a następnie zmiennych powinny być TestPlan StorSimRegKey, TestPlan AzureSubscriptionName i tak dalej.

   * *RecoveryPlanName***- StorSimRegKey**: klucz rejestracji hello hello usługi Menedżer StorSimple.
   * *RecoveryPlanName***- AzureSubscriptionName**: Nazwa hello hello subskrypcji platformy Azure.
   * *RecoveryPlanName***- ResourceName**: Nazwa hello hello zasobu StorSimple, który hello urządzenia StorSimple.
   * *RecoveryPlanName***- DeviceName**: hello urządzenia, które ma toobe przejścia w tryb failover.
   * *RecoveryPlanName***- VolumeContainers**: przecinkami ciąg kontenery woluminów znajduje się on na powitania urządzenia, które wymagają toobe nie powiodło się powyżej, na przykład volcon1, volcon2, volcon3.
   * *RecoveryPlanName***- TargetDeviceName**: hello urządzenia StorSimple chmury, na które hello kontenery są toobe przejścia w tryb failover.
   * *RecoveryPlanName***- TargetDeviceDnsName**: Nazwa usługi hello hello urządzenia docelowego (znajdują się w hello **maszyny wirtualnej** sekcji: hello nazwa usługi jest takie same hello jako hello Nazwa DNS).
   * *RecoveryPlanName***- StorageAccountName**: Nazwa konta magazynu hello, w którym skrypt hello (który toorun na powitania przeszła w tryb failover maszyny Wirtualnej) będzie przechowywany. Może to być konto magazynu, które ma skryptu hello toostore niektóre miejsca tymczasowo.
   * *RecoveryPlanName***- StorageAccountKey**: hello klucza dostępu dla hello powyżej konta magazynu.
   * *RecoveryPlanName***- ScriptContainer**: hello nazwa kontenera hello, w których hello skryptu będą przechowywane w chmurze hello. Kontener hello nie istnieje, zostanie utworzona.
   * *RecoveryPlanName***- VMGUIDS**: w przypadku ochrony maszyn wirtualnych, usługi Azure Site Recovery przypisuje każdej maszyny Wirtualnej Unikatowy identyfikator, który przedstawia szczegóły hello hello przejścia w tryb failover maszyny Wirtualnej. Witaj tooobtain VMGUID, wybierz opcję hello **usług odzyskiwania** i kliknij polecenie **chronionego elementu** &gt; **grup ochrony** &gt; **Maszyny** &gt; **właściwości**. Jeśli masz wiele maszyn wirtualnych, Dodaj hello identyfikatory GUID jako ciąg rozdzielony przecinkami.
   * *RecoveryPlanName***- AutomationAccountName** — Witaj nazwa konta automatyzacji hello, w którym można dodać hello elementy runbook i zasoby hello.

  Na przykład jeśli hello Nazwa planu odzyskiwania hello jest fileServerpredayRP, a następnie z **poświadczenia** & **zmienne** po dodaniu wszystkich zasobów hello karty powinna wyglądać następująco.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image5.png)

7. Przejdź toohello **usług odzyskiwania** sekcji i magazynem Azure Site Recovery hello wybierz utworzony wcześniej.
8. Wybierz hello **plany odzyskiwania (lokacji odzyskiwania)** opcję **Zarządzaj** grupy i utworzenie nowego planu odzyskiwania w następujący sposób:

   a.  Kliknij przycisk **+ planu odzyskiwania** przycisku, otwiera poniżej bloku.

      ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image6.png)

   b.  Wprowadź nazwę planu odzyskiwania, wybierz wartości modelu źródłowego, docelowego i wdrożenia.

   c.  Wybierz maszyny wirtualne hello z grupy ochrony hello mają tooinclude hello planu odzyskiwania i kliknij przycisk **OK** przycisku.

   d.  Wybierz wcześniej utworzony plan odzyskiwania, kliknij przycisk **Dostosuj** przycisk widoku dostosowywania planu odzyskiwania hello tooopen.

   e.  Kliknij prawym przyciskiem myszy **wszystkich grup zamykania** i kliknij przycisk **dodać akcję sprzed**.

   f.  Otwiera Wstaw blok akcji, wprowadź nazwę, wybierz **głównej stronie** opcja, w którym toorun opcji, wybierz konto automatyzacji (w którym można dodać hello elementów runbook), a następnie wybierz hello  **Tryb failover-StorSimple--kontenery woluminów** elementu runbook.

   g.  Kliknij prawym przyciskiem myszy **Grupa 1: Uruchom** i kliknij przycisk **Dodaj chronione elementy** opcji, a następnie wybierz maszyny wirtualne hello, które są chronione w hello planu odzyskiwania i kliknij przycisk toobe **Ok** przycisku. Opcjonalne, jeśli jest ono już zaznaczone maszyn wirtualnych.

   h.  Kliknij prawym przyciskiem myszy **Grupa 1: Uruchom** i kliknij przycisk **Post akcji** opcji, a następnie dodaj wszystkie hello następujące skrypty:

   * Element runbook Start-StorSimple--urządzenie wirtualne
   * Niepowodzenie elementu runbook przez StorSimple--kontenery woluminów
   * Element runbook instalacji woluminów po failover
   * Odinstaluj niestandardowy skryptu — rozszerzenia elementu runbook

   i.  Dodaj akcję ręczną po hello powyżej 4 skrypty w hello takie same **Grupa 1: kroki po** sekcji. Ta akcja jest hello punktu, w którym można sprawdzić, czy wszystko działa poprawnie. Ta akcja wymaga toobe dodać tylko w ramach testowego trybu failover (tak wybierać tylko hello **testowy tryb Failover** wyboru).

   j.  Po hello akcji ręcznej, Dodaj hello **oczyszczania** skryptu, za pomocą tej samej procedury, która została użyta w przypadku hello hello inne elementy runbook. **Zapisz** hello planu odzyskiwania.

    > [!NOTE]
    > Podczas uruchamiania test trybu failover, należy sprawdzić wszystkie elementy w kroku akcji ręcznej hello ponieważ hello woluminów StorSimple, które ma zostać sklonowany na urządzeniu docelowym hello zostaną usunięte w ramach oczyszczania powitania po wykonaniu akcji ręcznej hello.
    >

    ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image7.png)

## <a name="perform-a-test-failover"></a>Wykonaj test trybu failover
Zobacz toohello [rozwiązania Active Directory DR](../site-recovery/site-recovery-active-directory.md) Przewodnik uzupełniający tooActive szczególne zagadnienia dotyczące katalogu podczas hello testowy tryb failover. ustawienia lokalne powitania nie zakłóceń w ogóle, gdy hello test pracy awaryjnej. Witaj woluminów StorSimple, które zostały dołączone toohello lokalnej maszyny Wirtualnej są sklonowany toohello urządzenia chmury StorSimple na platformie Azure. Maszyny Wirtualnej do celów testowych jest włączane na platformie Azure i hello sklonowany woluminy są dołączone toohello maszyny Wirtualnej.

#### <a name="tooperform-hello-test-failover"></a>tooperform hello testowy tryb failover
1. W hello portalu Azure wybierz magazyn odzyskiwania lokacji.
2. Kliknij przycisk hello planu odzyskiwania utworzone dla serwera plików hello maszyny Wirtualnej.
3. Kliknij przycisk **testowanie trybu Failover**.
4. Wybierz hello sieci wirtualnej platformy Azure toowhich maszynach wirtualnych platformy Azure zostaną połączone po pracy awaryjnej.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image8.png)
5. Kliknij przycisk **OK** toobegin hello w tryb failover. Możesz śledzić postępy, klikając na powitania wirtualna tooopen jego właściwości lub na powitania **zadania testowego trybu failover** w nazwie magazynu &gt; **zadania** &gt; **zadania usługi Site Recovery**.
6. Po zakończeniu pracy awaryjnej hello również powinno być możliwe toosee repliki hello Azure machine są wyświetlane w portalu Azure hello &gt; **maszyn wirtualnych**. Można wykonywać z operacji sprawdzania poprawności.
7. Po operacji sprawdzania poprawności hello gotowe, kliknij przycisk **pełne sprawdzanie poprawności**. To spowoduje oczyszczania hello woluminów StorSimple i zamykania hello urządzenia chmury StorSimple.
8. Gdy wszystko będzie gotowe, kliknij przycisk **oczyszczania testowy tryb failover** na powitania planu odzyskiwania. W rekordzie uwagi i zapisać wszelkie obserwacje związane z hello testowanie trybu failover. Spowoduje to usunięcie maszyny wirtualnej hello, które zostały utworzone podczas testowania trybu failover.

## <a name="perform-a-planned-failover"></a>Realizacja planowanego trybu failover
   Podczas planowanego trybu failover lokalne powitania serwera plików zamknięcia maszyny Wirtualnej jest bezpieczne i chmury, w których wykonywana jest migawka kopii zapasowej woluminów hello na urządzeniu StorSimple. woluminy StorSimple Hello są przejścia w tryb failover toohello urządzenia wirtualnego, replika maszyny Wirtualnej jest włączane na platformie Azure, i woluminy hello są dołączone toohello maszyny Wirtualnej.

#### <a name="tooperform-a-planned-failover"></a>tooperform planowanego trybu failover
1. Hello portalu Azure, wybierz **usług odzyskiwania** magazynu &gt; **planów odzyskiwania (lokacji odzyskiwania)** &gt; **recoveryplan_name** utworzone dla Serwer plików Hello maszyny Wirtualnej.
2. W bloku planu odzyskiwania hello, kliknij **więcej** &gt; **planowanego trybu failover**.  

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image9.png)
3. Na powitania **potwierdzić planowanego trybu Failover** bloku, wybierz źródło hello i docelowych lokalizacji i Sieć docelowa wybierz i kliknij hello wyboru Ikona ✓ toostart hello trybu failover procesu.
4. Po utworzeniu maszyny wirtualnej repliki, są one w stan oczekiwania na zatwierdzenie. Kliknij przycisk **zatwierdzić** toocommit hello w tryb failover.
5. Po zakończeniu replikacji maszyn wirtualnych hello uruchomienia w hello lokalizacji dodatkowej.

## <a name="perform-a-failover"></a>Przejściu w tryb failover
Podczas nieplanowanego trybu failover woluminów StorSimple hello są przejścia w tryb failover toohello urządzenia wirtualnego, replika maszyny Wirtualnej zostanie przeniesiony na platformie Azure, a woluminy hello są dołączone toohello maszyny Wirtualnej.

#### <a name="tooperform-a-failover"></a>tooperform trybu failover
1. Hello portalu Azure, wybierz **usług odzyskiwania** magazynu &gt; **planów odzyskiwania (lokacji odzyskiwania)** &gt; **recoveryplan_name** utworzone dla Serwer plików Hello maszyny Wirtualnej.
2. W bloku planu odzyskiwania hello, kliknij **więcej** &gt; **pracy awaryjnej**.  
3. Na powitania **potwierdzić trybu Failover** bloku, wybierz źródło hello i docelowych lokalizacji.
4. Wybierz **wyłączyć maszyny wirtualne i zsynchronizuj najnowsze dane hello** toospecify czy Site Recovery należy spróbuj tooshut maszynę wirtualną hello chronione i synchronizacji danych hello tak, aby hello najnowszej wersji hello danych nie powiodło się za pośrednictwem.
5. Po hello w tryb failover maszyny wirtualne hello są w stan oczekiwania na zatwierdzenie. Kliknij przycisk **zatwierdzić** toocommit hello w tryb failover.


## <a name="perform-a-failback"></a>Wykonaj powrót po awarii
Podczas powrotu po awarii kontenery woluminów StorSimple są nie powiodło się za pośrednictwem urządzenia fizycznego toohello wstecz po wykonywana jest kopia zapasowa.

#### <a name="tooperform-a-failback"></a>tooperform powrotu po awarii
1. Hello portalu Azure, wybierz **usług odzyskiwania** magazynu &gt; **planów odzyskiwania (lokacji odzyskiwania)** &gt; **recoveryplan_name** utworzone dla Serwer plików Hello maszyny Wirtualnej.
2. W bloku planu odzyskiwania hello, kliknij **więcej** &gt; **planowanego trybu Failover**.  
3. Wybierz lokalizacje źródłowa i docelowa hello, hello wybierz odpowiednie synchronizacji danych i opcje tworzenia maszyny Wirtualnej.
4. Kliknij przycisk **OK** przycisk toostart hello powrotu po awarii procesu.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image10.png)

## <a name="best-practices"></a>Najlepsze rozwiązania
### <a name="capacity-planning-and-readiness-assessment"></a>Pojemności oceny planowania i gotowości
#### <a name="hyper-v-site"></a>Lokacja funkcji Hyper-V
Użyj hello [planisty wydajności użytkownika](http://www.microsoft.com/download/details.aspx?id=39057) toodesign hello serwera, magazynu i infrastruktury sieci w środowisku funkcji Hyper-V replica.

#### <a name="azure"></a>Azure
Możesz uruchomić hello [narzędzie oceny gotowości maszyny wirtualnej Azure](http://azure.microsoft.com/downloads/vm-readiness-assessment/) na tooensure maszyn wirtualnych, że są one zgodne z maszynami wirtualnymi Azure i usług Azure Site Recovery. Hello narzędzie oceny gotowości sprawdza konfiguracji maszyny Wirtualnej, a także ostrzega konfiguracje są niezgodne z platformy Azure. Na przykład jego wygeneruje ostrzeżenie, jeśli dysk C: jest większy niż 127 GB.

Planowanie wydajności składa się z co najmniej dwie ważne procesów:

* Mapowanie lokalnego rozmiarów maszyn wirtualnych tooAzure maszyn wirtualnych funkcji Hyper-V (na przykład A6, A7 A8 i A9).
* Określanie hello wymagane przepustowości połączenia z Internetem.

## <a name="limitations"></a>Ograniczenia
* Obecnie tylko 1 urządzenia StorSimple można pracować w trybie Failover (tooa pojedynczy urządzenia chmury StorSimple). Scenariusz powitania serwera plików, które obejmuje kilka urządzeń StorSimple nie jest jeszcze obsługiwany.
* Jeśli wystąpi błąd podczas włączania ochrony dla maszyny Wirtualnej, upewnij się, Rozłączono hello obiektów docelowych iSCSI.
* Wszystkie kontenery woluminów hello, które zostały zgrupowane razem z powodu zasad tworzenia kopii zapasowych, dzieląc go w kontenery woluminów będzie można przełączyć razem.
* Wszystkie woluminy hello w kontenery woluminów hello wybrana zostanie zainicjowana.
* Woluminy, które sumują toomore niż 64 TB nie można przełączyć ponieważ maksymalną pojemność pojedynczego urządzenia chmury StorSimple hello jest 64 TB.
* Jeśli hello planowane lub nieplanowane przejście w tryb failover nie powiedzie się i hello maszyny wirtualne są tworzone na platformie Azure, następnie przeprowadź oczyszczanie nie hello maszyn wirtualnych. Zamiast tego powrotu po awarii. Jeśli usuniesz maszyn wirtualnych hello następnie hello w lokalnym maszyn wirtualnych nie można włączyć ponownie.
* Po przejściu w tryb failover Jeśli nie jest możliwe toosee hello woluminów, przejdź toohello maszyn wirtualnych, otwórz przystawkę Zarządzanie dyskami ponownie przeskanować dyski hello i dostosować je online.
* W niektórych przypadkach hello litery dysku w lokacji odzyskiwania po awarii hello może różnić się od hello litery lokalnymi. W takim przypadku należy toomanually poprawne hello problem po zakończeniu pracy awaryjnej hello.
* Powinno zostać wyłączone uwierzytelnianie wieloskładnikowe dla hello Azure poświadczeniami, które jest wprowadzana na koncie automatyzacji hello jako zasób. Jeśli uwierzytelnianie nie jest wyłączone, skrypty nie może być toorun automatycznie i hello planu odzyskiwania zakończy się niepowodzeniem.
* Limit czasu zadania trybu failover: hello StorSimple skryptu zostanie limit czasu, jeśli hello pracy w trybie failover kontenery woluminów zajmuje więcej czasu niż hello limit usługi Azure Site Recovery dla skryptu (obecnie 120 minut).
* Limit czasu zadania tworzenia kopii zapasowej: hello skryptu StorSimple upłynie limit czasu, jeśli kopia zapasowa hello woluminów trwa dłużej niż limit usługi Azure Site Recovery hello na skryptu (obecnie 120 minut).

  > [!IMPORTANT]
  > Ręcznie uruchom hello kopii zapasowej z hello portalu Azure, a następnie ponownie uruchom hello planu odzyskiwania.

* Limit czasu zadania sklonować: hello skryptu StorSimple upłynie limit czasu Jeśli hello Klonowanie woluminów zajmuje więcej czasu niż hello limit usługi Azure Site Recovery dla skryptu (obecnie 120 minut).
* Błąd synchronizacji czasu: błędy limit informujący o tym, że kopie zapasowe hello powiodły się nawet hello kopii zapasowej zakończy się pomyślnie w portalu hello skrypty hello StorSimple. Możliwą przyczyną tego może być czas tego urządzenia StorSimple hello mogą być zsynchronizowane z hello bieżący czas w strefie czasowej hello.

  > [!IMPORTANT]
  > Witaj urządzenia czas synchronizacji z hello bieżący czas w strefie czasowej hello.

* Błąd trybu failover urządzenia: hello StorSimple skrypt może zakończyć się niepowodzeniem, podczas gdy nie zawiera urządzenia trybu failover planu odzyskiwania hello jest uruchomiona.

  > [!IMPORTANT]
  > Po zakończeniu pracy awaryjnej urządzenia hello, uruchom ponownie hello planu odzyskiwania.


## <a name="summary"></a>Podsumowanie
Za pomocą usługi Azure Site Recovery, można utworzyć plan odzyskiwania ukończenia automatycznego po awarii dla serwera plików maszyny Wirtualnej o udziały plików hostowane na magazynie StorSimple. Możesz zainicjować hello trybu failover w ciągu kilku sekund z dowolnego miejsca w hello zdarzeń zakłócenia i pobrać aplikacji hello do pracy w ciągu kilku minut.
