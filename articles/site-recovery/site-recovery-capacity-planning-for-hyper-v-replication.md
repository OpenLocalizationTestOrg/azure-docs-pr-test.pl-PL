---
title: "aaaRun hello funkcji Hyper-V planisty wydajności dla usługi Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toorun hello planisty wydajności funkcji Hyper-V dla usługi Azure Site Recovery"
services: site-recovery
documentationcenter: na
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 2bc3832f-4d6e-458d-bf0c-f00567200ca0
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: b853598e5cd290c48b59794ba48eefc72ac8ded6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-hyper-v-capacity-planner-tool-for-site-recovery"></a>Uruchamianie narzędzi planowania pojemności funkcji Hyper-V hello Site Recovery

W ramach wdrożenia usługi Azure Site Recovery należy toofigure Twojego replikacji i wymaganiach odnośnie do przepustowości. planisty wydajności Hello funkcji Hyper-V dla usługi Site Recovery pomaga możesz toodo, replikacji maszyny wirtualnej funkcji Hyper-V.

W tym artykule opisano, jak toorun hello planisty wydajności funkcji Hyper-V. To narzędzie należy używane wraz z informacjami hello w [Planowanie wydajności dla usługi Site Recovery](site-recovery-capacity-planner.md).

## <a name="before-you-start"></a>Przed rozpoczęciem
Należy uruchomić narzędzie hello na węzeł serwera lub klastra funkcji Hyper-V w lokacji głównej. Serwery hosta funkcji Hyper-V hello toorun hello narzędzie musi:

* System operacyjny: Windows Server 2012 lub 2012 R2
* Pamięć: 20 MB (minimum)
* Procesora: obciążenie 5 procent (minimum)
* Miejsce na dysku: 5 MB (minimum)

Przed uruchomieniem narzędzia hello należy tooprepare hello podstawowej lokacji. Jeśli replikujesz między dwoma lokacjami lokalnymi i ma przepustowości toocheck należy tooprepare jako serwer repliki.

## <a name="step-1-prepare-hello-primary-site"></a>Krok 1: Przygotowanie hello lokacji głównej

1. W lokacji głównej hello należy utworzyć listę wszystkich hello maszyn wirtualnych funkcji Hyper-V ma tooreplicate hello funkcji Hyper-V hosts/klaster i na których są przechowywane. można uruchomić narzędzie Hello, dla wielu autonomicznych hostów lub dla jednego klastra, ale nie oba jednocześnie. Również musi toorun osobno dla każdego systemu operacyjnego, więc należy zebrać informacje na temat serwerów funkcji Hyper-V w następujący sposób:

   * Samodzielne serwery usługi systemu Windows Server 2012
   * Klastry z systemem Windows Server 2012
   * Samodzielne serwery usługi Windows Server 2012 R2
   * Klastry z systemem Windows Server 2012 R2
2. Włącz tooWMI dostępu zdalnego na wszystkich hostach funkcji Hyper-V hello i klastrów. Uruchom to polecenie na każdym klastra, czy reguły zapory toomake i uprawnienia użytkownika są ustawione:

        netsh firewall set service RemoteAdmin enable
3. Włącz wydajności na monitorowanie serwerów i klastrów, w następujący sposób:

   * Otwórz hello zapory systemu Windows z hello **zabezpieczeniami zaawansowanymi** przystawki, a następnie włącz hello następujące reguły dla ruchu przychodzącego: **dostęp sieciowy COM + (DCOM-IN)** i wszystkie reguły w hello **zdalnego dziennika zdarzeń Grupa zarządzania**.

## <a name="step-2-prepare-a-replica-server-on-premises-tooon-premises-replication"></a>Krok 2: Przygotowanie serwera repliki (replikacji lokalnej tooon lokalnych)
Nie trzeba toodo to Jeśli replikujesz tooAzure.

Zaleca się jeden host funkcji Hyper-V jest skonfigurowany jako serwer odzyskiwania, aby umożliwić fikcyjny maszyny Wirtualnej zreplikowanej tooit toocheck przepustowości.  Możesz to pominąć, ale nie będzie możliwe toomeasure przepustowości, dopiero po wykonaniu.

1. Jeśli toouse węźle klastra jako repliki hello skonfiguruj brokera funkcji Hyper-V Replica:

   * W **Menedżera serwera**, otwórz **Menedżera klastra trybu Failover**.
   * Połącz toohello klastra, zaznacz hello nazwę klastra i kliknij przycisk **akcje** > **Konfiguruj rolę** Kreator wysokiej dostępności hello tooopen.
   * W **wybierz rolę**, kliknij przycisk **brokera funkcji Hyper-V Replica**. W Kreatorze hello podaj **nazwę NetBIOS** i hello **adres IP** toobe używane jako klaster toohello punktu połączenia hello (nazywany też punktem dostępu klienta). Witaj **brokera funkcji Hyper-V Replica** zostanie skonfigurowana, co w nazwie punktu dostępu klienta, które należy zwrócić uwagę.
   * Sprawdź tę rolę brokera funkcji Hyper-V Replica hello pomyślnym przejściu do trybu online i może przełączyć się pomiędzy wszystkimi węzłami klastra hello. toodo, kliknij prawym przyciskiem myszy rolę hello, wskaż zbyt**Przenieś**, a następnie kliknij przycisk **wybierz węzeł**. Wybierz węzeł > **OK**.
   * Jeśli używasz uwierzytelniania opartego na certyfikatach, upewnij się, że każdy węzeł klastra i punkt dostępu klienta hello wszystkie mają zainstalowany certyfikat hello.
2. Włącz funkcję serwera repliki:

   * W klastrze Otwórz Menedżera klastra awarii, Połącz toohello klastra i kliknij przycisk **ról** > Wybierz rolę > **ustawienia replikacji** > **Włącz ten klaster jako repliki Serwer**. Wybierz klaster jako hello repliki, należy najpierw rola brokera funkcji Hyper-V Replica hello toohave istnieje w klastrze hello w hello oraz lokacji głównej.
   * Na autonomicznym serwerze otwórz Menedżera funkcji Hyper-V. W hello **akcje** okienku, kliknij przycisk **ustawienia funkcji Hyper-V** powitania serwera ma tooenable i w **konfiguracji replikacji** kliknij **Włącz ten element komputer jako serwer repliki**.
3. Konfigurowanie uwierzytelniania:

   * W **uwierzytelnianie i porty**, wybierz, w jaki sposób tooauthenticate hello serwer podstawowy i porty uwierzytelniania hello. Jeśli używasz kliknij certyfikat **wybierz certyfikat** tooselect jeden. Użyj protokołu Kerberos, jeśli hosty funkcji Hyper-V hello podstawowymi i odzyskiwania znajdują się w hello tej samej domenie lub w domenach zaufanych. Wykorzystuje się certyfikaty dla różnych domenach lub wdrożenia grupy roboczej.
   * W **uwierzytelnianie i magazynowanie**, Zezwalaj na **żadnych** uwierzytelniony serwer repliki toothis (podstawowemu) serwerowi toosend replikacji danych.

     ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image1.png)
   * Uruchom **netsh http show servicestate**, toocheck tego odbiornik hello jest uruchomiony dla hello/port protokołu określonego:  
4. Konfigurowanie zapór. Podczas instalacji funkcji Hyper-V reguły zapory są tworzone tooallow ruchu na powitania domyślnych portów (HTTPS na 443, Kerberos na 80). Włącz te zasady w następujący sposób:
  - Certyfikat uwierzytelniania w klastrze (port 443):``Get-ClusterNode | ForEach-Object {Invoke-command -computername \$\_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTPS Listener (TCP-In)"}}``
  - Uwierzytelnianie Kerberos w klastrze (80):``Get-ClusterNode | ForEach-Object {Invoke-command -computername \$\_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"}}``
  - Uwierzytelnianie certyfikatu na autonomicznym serwerze:``Enable-Netfirewallrule -displayname "Hyper-V Replica HTTPS Listener (TCP-In)"``
  - Uwierzytelnianie Kerberos na autonomicznym serwerze:``Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"``

## <a name="step-3-run-hello-capacity-planner-tool"></a>Krok 3: Uruchom narzędzie planowania pojemności hello
Po utworzeniu przygotowane lokacji głównej i skonfigurować serwer odzyskiwania, można uruchomić narzędzie hello.

1. [Pobierz](https://www.microsoft.com/download/details.aspx?id=39057) hello narzędzie hello Microsoft Download Center.
2. Uruchom narzędzie hello z jednego z serwerów podstawowych hello (lub jednego z węzłów hello z klastra głównego hello). Kliknij prawym przyciskiem myszy plik .exe hello, a następnie wybierz pozycję **Uruchom jako administrator**.
3. W **przed rozpoczęciem**, określ, jak długo mają toocollect dane. Firma Microsoft zaleca, należy uruchomić narzędzie hello podczas produkcji tooensure godzin czy dane są przedstawicielem. Jeśli próbujesz toovalidate łączności sieciowej, można zebrać tylko minutę.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image2.png)
4. W **szczegóły lokacji głównej**, określ hello nazwa serwera lub nazwa FQDN hosta autonomicznego lub klastra określić hello FQDN powitania klienta zaakceptować punkt, nazwy klastra lub w dowolnym węźle klastra hello, a następnie kliknij przycisk **dalej**. Narzędzie Hello automatycznie wykrywa hello nazwę serwera hello, w którym jest uruchomiona na. Narzędzie Hello przejmuje maszyn wirtualnych, które mogą być monitorowane pod kątem hello określonych serwerów.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image3.png)
5. W **szczegóły lokacji repliki**, jeśli przeprowadzasz replikację tooAzure, lub jeśli przeprowadzasz replikację tooa dodatkowego centrum danych i nie skonfigurowano połączenia z serwerem repliki, zaznacz **pominąć testy lokacji repliki**. Jeśli ustawiono typ repliki jest replikowana tooa dodatkowego centrum danych, wprowadzić nazwę FQDN hello autonomicznym serwerem lub punktu dostępu klienta hello klastra hello w **Server name (lub) zakończenia brokera repliki funkcji Hyper-V**.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image4.png)
6. W **rozszerzony replice szczegóły**, Włącz **hello Pomiń testy dotyczące lokacji rozszerzonej repliki**. Te testy nie są obsługiwane przez usługę Site Recovery.
7. W **tooReplicate wybierz maszyny wirtualne**, narzędzia hello łączy toohello serwer lub klaster i wyświetla maszyn wirtualnych i dyski uruchomionych na serwerze podstawowym hello, zgodnie z ustawieniami hello określone na powitania **szczegóły lokacji głównej**  strony. Maszyny wirtualne, które są już włączone dla replikacji lub które nie są uruchomione, nie będą wyświetlane. Wybierz hello maszyn wirtualnych, dla których chcesz toocollect metryki. Automatyczne zaznaczanie hello wirtualne dyski twarde zbyt zbiera dane dla hello maszyn wirtualnych.
8. Jeśli skonfigurowano serwer repliki lub w klastrze, w **informacje o sieci**, określ hello przybliżonej przepustowości sieci WAN uważasz, że będą używane między lokacjami hello podstawowym i repliki i wybierz hello certyfikatów, jeśli skonfigurowano uwierzytelnianie certyfikatu.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image5.png)
9. W **Podsumowanie**, sprawdź ustawienia hello i kliknij przycisk **dalej** toobegin zbieranie metryk. Narzędzie postęp i stan jest wyświetlany na powitania **obliczania pojemności** strony. Po zakończeniu działania narzędzia hello, kliknij przycisk **Wyświetl raport** tooview hello w danych wyjściowych. Domyślnie dzienniki i raporty są przechowywane w **%systemdrive%\Users\Public\Documents\Capacity Planner**.

   ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image6.png)

## <a name="step-4-interpret-hello-results"></a>Krok 4: Interpretacji wyników hello

Poniżej przedstawiono hello ważne metryki. Metryki, które nie są wymienione w tym miejscu, można zignorować. Nie są one odpowiednie dla usługi Site Recovery.

### <a name="on-premises-tooon-premises-replication"></a>Replikacji lokalnej tooon lokalnej

* Wpływ na replikację na powitania hostem głównym obliczeniowych, pamięci
* Wpływ na replikację na powitania podstawowego, miejsca na dysku magazynu hostów odzyskiwania, IOPS
* Całkowitej przepustowości wymagane dla replikacji różnicowej (MB/s)
* Przepustowość sieci obserwowanych między podstawowym hostem hello i hello hoście odzyskiwania (MB/s)
* Sugestia hello idealne liczby aktywnych równolegle transferów między dwa hosty hello/klastry

### <a name="on-premises-tooazure-replication"></a>Lokalne tooAzure replikacji

* Wpływ na replikację na powitania hostem głównym obliczeniowych, pamięci
* Wpływ replikacji hostem głównym hello magazynu miejsca na dysku, IOPS
* Całkowitej przepustowości wymagane dla replikacji różnicowej (MB/s)

## <a name="more-resources"></a>Więcej zasobów
* Aby uzyskać szczegółowe informacje o narzędziu hello odczytu hello dokument, który towarzyszy hello Narzędzie pobierania.
* Obejrzyj wskazówki narzędzia hello na blogu Keitha Mayer [blogu w witrynie TechNet](http://blogs.technet.com/b/keithmayer/archive/2014/02/27/guided-hands-on-lab-capacity-planner-for-windows-server-2012-hyper-v-replica.aspx).
* [Pobierz wyniki hello](site-recovery-performance-and-scaling-testing-on-premises-to-on-premises.md) z naszych testowanie wydajnościowe na potrzeby replikacji funkcji Hyper-V lokalnych tooon lokalnej

## <a name="next-steps"></a>Następne kroki

Po zakończeniu planowania pojemności możesz przystąpić do wdrażania usługi Site Recovery:

* [Replikowanie maszyn wirtualnych funkcji Hyper-V w tooAzure chmury VMM](site-recovery-vmm-to-azure.md)
* [Replikowanie maszyn wirtualnych funkcji Hyper-V (bez VMM) tooAzure](site-recovery-hyper-v-site-to-azure.md)
* [Replikowanie maszyn wirtualnych funkcji Hyper-V między lokacjami programu VMM](site-recovery-vmm-to-vmm.md)
