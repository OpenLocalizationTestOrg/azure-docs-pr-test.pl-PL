---
title: aaaRestore a maszyny wirtualne z kopii zapasowej | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toorestore maszyny wirtualnej platformy Azure z odzyskiwania punktu"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: Przywracanie kopii zapasowej. jak toorestore; punkt odzyskiwania;
ms.assetid: fed877b3-b496-49fb-99e4-653be7c23e3a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: trinadhk; jimpark;
ms.openlocfilehash: 44c25f3248784accd1c2beaabb2c9a4dca3232d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-virtual-machines-in-azure"></a>Przywracanie maszyn wirtualnych na platformie Azure
> [!div class="op_single_selector"]
> * [Przywracanie maszyn wirtualnych w portalu Azure](backup-azure-arm-restore-vms.md)
> * [Przywracanie maszyn wirtualnych w portalu klasycznym](backup-azure-restore-vms.md)
>
>

Przywróć tooa maszyny wirtualnej, który nowej maszyny Wirtualnej z kopii zapasowych hello przechowywane w magazynie usługi Kopia zapasowa Azure z hello następujące kroki.

> [!IMPORTANT]
> Teraz można uaktualnić Twoje Magazyny usług tooRecovery magazynów kopii zapasowych. Aby uzyskać więcej informacji, zobacz artykuł hello [uaktualnienia tooa magazynu kopii zapasowej, Magazyn usług odzyskiwania i](backup-azure-upgrade-backup-to-recovery-services.md). Firma Microsoft zachęca tooupgrade Magazyny usług tooRecovery magazyny kopii zapasowych.<br/> **15 października 2017**, użytkownik nie będzie już magazyny kopii zapasowych toocreate PowerShell toouse stanie. <br/> **Od 1 listopada 2017 roku**:
>- Wszystkie pozostałe magazyny kopii zapasowych zostanie automatycznie uaktualniony tooRecovery Magazyny usług.
>- Użytkownik nie będzie możliwe tooaccess danych kopii zapasowych w portalu klasycznym hello. Zamiast tego użyj hello Azure tooaccess portalu tej kopii zapasowej w Magazyny usług odzyskiwania.
>

## <a name="restore-workflow"></a>Przywróć przepływu pracy
### <a name="step-1-choose-an-item-toorestore"></a>Krok 1: Wybierz toorestore elementu
1. Przejdź toohello **chronione elementy** karcie i wybierz hello maszyny wirtualnej, którą chcesz toorestore tooa nowej maszyny Wirtualnej.

    ![Elementy chronione](./media/backup-azure-restore-vms/protected-items.png)

    Witaj **punkt odzyskiwania** kolumny w hello **chronione elementy** strony poinformuje hello liczbę punktów odzyskiwania dla maszyny wirtualnej. Witaj **punkt odzyskiwania najnowszych** kolumny informuje hello czas wykonania ostatniej kopii zapasowej hello z której można przywrócić maszyny wirtualnej.
2. Kliknij przycisk **przywrócić** tooopen hello **przywraca element** kreatora.

    ![Przywraca element](./media/backup-azure-restore-vms/restore-item.png)

### <a name="step-2-pick-a-recovery-point"></a>Krok 2: Wybierz punkt odzyskiwania
1. W hello **wybierz punkt odzyskiwania** ekranu, można przywrócić z najnowszego punktu odzyskiwania hello, lub z określonego punktu w czasie. Witaj wybrany, gdy zostanie otwarty Kreator opcja domyślna jest *punkt odzyskiwania najnowszych*.

    ![Wybierz punkt odzyskiwania](./media/backup-azure-restore-vms/select-recovery-point.png)
2. toopick wcześniejszego punktu w czasie, wybierz hello **wybierz datę** opcji na liście rozwijanej hello i wybierz datę w formancie kalendarza hello, klikając hello **ikonę kalendarza**. W formancie hello wszystkie daty, które mają punkty odzyskiwania są wypełniane światła odcień szarości i można wybrać przez użytkownika hello.

    ![Wybierz datę](./media/backup-azure-restore-vms/select-date.png)

    Po kliknięciu Data w formancie kalendarza hello odzyskiwania hello punktów dostępnych na czy daty będą widoczne w poniższej tabeli punktów odzyskiwania. Witaj **czasu** kolumny wskazuje czas hello, w których hello migawki. Witaj **typu** kolumny Wyświetla hello [spójności](https://azure.microsoft.com/documentation/articles/backup-azure-vms/#consistency-of-recovery-points) hello punktu odzyskiwania. Nagłówek tabeli Hello pokazuje hello liczbę punktów odzyskiwania dostępnych w tym dniu w nawiasach.

    ![Punkty odzyskiwania](./media/backup-azure-restore-vms/recovery-points.png)
3. Wybierz punkt odzyskiwania hello z hello **punktów odzyskiwania** tabeli, a następnie kliknij przycisk hello dalej Strzałka toogo toohello następnego ekranu.

### <a name="step-3-specify-a-destination-location"></a>Krok 3: Określ lokalizację docelową
1. W hello **wybierz Przywracanie wystąpienia** ekranu Określ szczegóły gdzie toorestore hello maszyny wirtualnej.

   * Określ nazwę maszyny wirtualnej hello: podany w usłudze w chmurze, Nazwa maszyny wirtualnej hello powinna być unikatowa. Nie obsługujemy nadmiernie zapisywania istniejącej maszyny Wirtualnej.
   * Wybierz usługę chmury dla maszyny Wirtualnej hello: jest to obowiązkowa w przypadku tworzenia maszyny Wirtualnej. Można wybrać tooeither Użyj istniejącej usługi w chmurze lub Utwórz nową usługę w chmurze.

        Niezależnie od nazwy usługi w chmurze jest wybierany były unikatowe globalnie. Zazwyczaj nazwa usługi w chmurze hello pobiera skojarzony z adresem URL publicznych w formie hello [cloudservice]. cloudapp.net. Azure nie pozwoli toocreate nową usługę w chmurze, jeśli nazwa hello została już użyta. Jeśli wybierzesz toocreate nową usługę w chmurze, zostanie podany hello takie same nazwy jako maszyna wirtualna hello — w których wielkość hello maszyny Wirtualnej pobrana nazwa powinna być usługi w chmurze toohello skojarzone wystarczająco unikatowy toobe zastosowane.

        Tylko wyświetlić usługi w chmurze i sieci wirtualnych, które nie są skojarzone z wszystkich grup koligacji w hello przywracania Szczegóły wystąpienia. [Dowiedz się więcej](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
2. Wybierz konto magazynu dla maszyny Wirtualnej hello: jest to obowiązkowe przy tworzeniu hello maszyny Wirtualnej. Możesz wybrać z istniejących kont magazynu w hello sam regionie co magazyn usługi Kopia zapasowa Azure hello. Nie obsługujemy kont magazynu, które są strefy nadmiarowe lub typu magazynu Premium.

    Jeśli nie ma żadnych kont magazynu z obsługiwanych konfiguracji, Utwórz konto magazynu operacji przywracania przed toostarting obsługiwanej konfiguracji.

    ![Wybierz sieć wirtualną](./media/backup-azure-restore-vms/restore-sa.png)
3. Wybierz sieć wirtualną: hello sieć wirtualną (VNET) dla maszyny wirtualnej hello powinna być zaznaczona w momencie tworzenia hello hello maszyny Wirtualnej. Hello przywrócić interfejsu użytkownika pokazano wszystkie hello sieci wirtualnych w ramach tej subskrypcji, który może służyć. Nie jest obowiązkowe tooselect sieci Wirtualnej dla hello przywrócić maszyny Wirtualnej — można maszyny wirtualnej może tooconnect toohello przywrócone przez hello internet, nawet jeśli hello sieci Wirtualnej nie została zastosowana.

    Hello w chmurze wybranej usługi jest skojarzona z siecią wirtualną, a następnie hello sieci wirtualnej nie można zmienić.

    ![Wybierz sieć wirtualną](./media/backup-azure-restore-vms/restore-cs-vnet.png)
4. Wybierz podsieć: hello sieci Wirtualnej ma podsieci, domyślnie hello pierwszej podsieci zostanie wybrany. Wybierz podsieć hello dowolnego z opcji listy rozwijanej hello. Szczegółowe podsieci, przejdź w hello rozszerzenie tooNetworks [strony głównej portalu](https://manage.windowsazure.com/), przejdź zbyt**sieci wirtualnych** i wybierz hello sieci wirtualnej i przechodzenie do szczegółów podsieci toosee Konfigurowanie.

    ![Wybierz podsieć](./media/backup-azure-restore-vms/select-subnet.png)
5. Kliknij przycisk hello **przesyłania** ikonę w toosubmit kreatora hello hello szczegółów i utworzyć zadanie przywracania.

## <a name="track-hello-restore-operation"></a>Śledź hello operacji przywracania
Po wprowadź wszystkie informacje hello do Kreatora przywracania hello i przesłać go kopia zapasowa Azure spróbuje toocreate operacji przywracania hello tootrack zadania.

![Tworzenie zadania przywracania](./media/backup-azure-restore-vms/create-restore-job.png)

Tworzenie zadania hello zakończy się pomyślnie, pojawi się powiadomienie wyskakujące wskazujący, że to zadanie hello jest tworzony. Więcej informacji można uzyskać, klikając hello **zadania** przycisku, który trwać zbyt**zadania** kartę.

![Utworzono zadanie przywracania](./media/backup-azure-restore-vms/restore-job-created.png)

Po zakończeniu operacji przywracania hello, zostanie ona oznaczona jako zakończona w **zadania** kartę.

![Zadanie ukończenia przywracania](./media/backup-azure-restore-vms/restore-job-complete.png)

Po Przywracanie hello maszyny wirtualnej, może być konieczne toore instalacji rozszerzeń hello istniejących hello oryginalna maszyna wirtualna i [modyfikowania punktów końcowych hello](../virtual-machines/windows/classic/setup-endpoints.md) hello maszyny wirtualnej w hello portalu Azure.

## <a name="post-restore-steps"></a>Wykonywane po przywróceniu kroki
Korzystania z dystrybucji systemu Linux chmury inicjowania na podstawie takich jak Ubuntu, ze względów bezpieczeństwa hasło zostanie zablokowana po przywracania. Sprawdź użycie rozszerzenia VMAccess na powitania przywrócić maszyny Wirtualnej za[resetowania hasła hello](../virtual-machines/linux/classic/reset-access.md). Zalecamy używanie kluczy SSH w tych tooavoid dystrybucje Resetowanie hasła post przywracania.

## <a name="backup-for-restored-vms"></a>Tworzenie kopii zapasowej dla przywróconej maszyny wirtualne
Jeśli została przywrócona maszyny Wirtualnej usługi w chmurze toosame o hello tej samej nazwy pierwotnie kopii zapasowej maszyny Wirtualnej, kopia zapasowa będzie na powitania przywracania post maszyny Wirtualnej. Jeśli masz przywrócić maszyny Wirtualnej tooa innej usługi w chmurze lub określić inną nazwę dla maszyny Wirtualnej przywróconej, to będzie traktowany jako nowej maszyny Wirtualnej, i należy toosetup kopii zapasowej przywróconej maszyny wirtualnej.

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a>Przywracanie maszyny Wirtualnej podczas awarii centrum danych Azure
Kopia zapasowa Azure umożliwia przywracanie z kopii zapasowych centrum danych sparowanego toohello maszyn wirtualnych w przypadku, gdy centrum danych podstawowych hello którym maszyny wirtualne są uruchomione po awarii środowiska i skonfigurować geograficznie nadmiarowego toobe magazynu kopii zapasowej. W takich scenariuszach należy tooselect konta magazynu, który znajduje się w centrum danych sparowanego i resztę procesu przywracania hello pozostaje w tym samym. Kopia zapasowa Azure używa usługi obliczeniowe z maszyny wirtualnej hello przywrócić toocreate sparowanego geo. Dowiedz się więcej o [odporności centrum danych Azure](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)

## <a name="restoring-domain-controller-vms"></a>Przywracanie maszyn wirtualnych z kontrolera domeny
Kopia zapasowa maszyn wirtualnych kontrolera domeny (DC) jest obsługiwany scenariusz w usłudze Kopia zapasowa Azure. Jednak należy uważać podczas procesu przywracania hello. proces przywracania poprawne Hello zależy od struktury hello hello domeny. W przypadku najprostszym hello pojedynczy kontroler domeny znajduje się w jednej domenie. Najczęściej w przypadku obciążeń produkcyjnych, będziesz mieć pojedynczą domenę z wielu kontrolerów domeny, prawdopodobnie z kilka kontrolerów domeny lokalnie. Ponadto może być lesie z wieloma domenami.

Z usługi Active Directory perspektywy hello maszyny Wirtualnej platformy Azure jest podobnie jak inne maszyny Wirtualnej w nowoczesnych obsługiwanej funkcji hypervisor. Witaj główne różnice w funkcji hypervisor lokalnej jest dostępnej na platformie Azure jest konsoli maszyny Wirtualnej. Konsola jest wymagana dla niektórych scenariuszy, takich jak odzyskiwanie przy użyciu kopii zapasowej typu odzyskiwania systemu operacyjnego systemu od zera (BMR). Jednak przywrócenie maszyny Wirtualnej z magazynu kopii zapasowych hello nie zastępuje pełnego odzyskiwania systemu od ZERA. Active Directory przywracania trybu (DSRM) jest również dostępna, więc działało wszystkie scenariusze odzyskiwania usługi Active Directory. Aby uzyskać więcej informacji w tle, sprawdź, czy [kopia zapasowa i przywracanie zagadnienia dotyczące zwirtualizowanych kontrolerów domeny](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers) i [planowanie odzyskiwanie lasu usługi Active Directory](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx).

### <a name="single-dc-in-a-single-domain"></a>Pojedynczy kontroler domeny w jednej domenie
Witaj maszyny Wirtualnej można przywrócić (na przykład innych maszyn wirtualnych) z hello Azure portalu lub przy użyciu programu PowerShell.

### <a name="multiple-dcs-in-a-single-domain"></a>Wiele kontrolerów domeny w jednej domenie
Jeśli inne kontrolery domeny z tej samej domeny można połączyć się za pośrednictwem powitalne hello sieci, takich jak żadnej maszyny Wirtualnej można przywrócić hello kontrolera domeny. Jeśli jest hello ostatniego pozostałego kontrolera domeny w domenie hello lub przeprowadzane jest Odzyskiwanie w sieci izolowanej musi występować procedury odzyskiwania lasu.

### <a name="multiple-domains-in-one-forest"></a>Wiele domen w jednym lesie
Jeśli inne kontrolery domeny z tej samej domeny można połączyć się za pośrednictwem powitalne hello sieci, takich jak żadnej maszyny Wirtualnej można przywrócić hello kontrolera domeny. Jednak w innych przypadkach zaleca się przywrócenie lasu.

<!--- WK: this following original supportability statement is incorrect, taking it out.
hello challenge arises because DSRM mode is not present in Azure. So toorestore such a VM, you cannot use hello Azure portal. hello only supported restore mechanism is disk-based restore using PowerShell.

> [!WARNING]
> For Domain Controller VMs in a multi-DC environment, do not use hello Azure portal for restore! Only PowerShell based restore is supported
>
>

Read more about hello [USN rollback problem](https://technet.microsoft.com/library/dd363553) and hello strategies suggested toofix it.
--->

## <a name="restoring-vms-with-special-network-configurations"></a>Przywracanie maszyn wirtualnych z konfiguracjami sieci specjalne
Kopia zapasowa Azure obsługuje kopie zapasowe na następujących konfiguracji specjalnych sieci maszyn wirtualnych.

* Maszyn wirtualnych w usłudze równoważenia obciążenia (wewnętrznych i zewnętrznych)
* Maszyny wirtualne z wielu zastrzeżonych adresów IP
* Maszyny wirtualne z wieloma kartami sieciowymi

Te konfiguracje wprowadzić następujące zagadnienia dotyczące podczas przywracania ich.

> [!TIP]
> Użyj programu PowerShell na podstawie przywracania przepływu toorecreate hello specjalne konfiguracji sieci maszyn wirtualnych post przywracania.
>
>

### <a name="restoring-from-hello-ui"></a>Przywracanie z hello interfejsu użytkownika:
Podczas przywracania z interfejsu użytkownika, **zawsze wybierz nową usługę w chmurze**. Należy pamiętać, że ponieważ portal przyjmuje tylko obowiązkowe parametry podczas przywracania przepływu, maszyn wirtualnych przywrócony przy użyciu interfejsu użytkownika zostaną utracone hello specjalne sieci konfiguracji, które posiadają. Innymi słowy, przywracanie maszyn wirtualnych będzie normalne maszyn wirtualnych bez konfiguracji usługi równoważenia obciążenia lub wielu kart Sieciowych lub wielu zastrzeżonego adresu IP.

### <a name="restoring-from-powershell"></a>Przywracanie z programu PowerShell:
PowerShell ma hello możliwości toojust Przywracanie hello dysków maszyny Wirtualnej z kopii zapasowej i nie utworzyć hello maszyny wirtualnej. Jest to przydatne podczas przywracania maszyn wirtualnych, które wymagają konfiguracji sieci specjalnych wymienionych powyżej.

W kolejności toofully odtworzyć hello maszyny wirtualnej po przywracaniu dysków, wykonaj następujące kroki:

1. Przywróć hello dysków z magazynu kopii zapasowych za pomocą [kopii zapasowej programu Azure PowerShell](backup-azure-vms-classic-automation.md#restore-an-azure-vm)
2. Tworzenie konfiguracji maszyny Wirtualnej hello wymagane dla usługi równoważenia obciążenia / wielu kart/wiele zastrzeżonego adresu IP za pomocą hello poleceń cmdlet programu PowerShell i korzystać z niego toocreate hello wirtualna wymaganą konfiguracją.

   * Tworzenie maszyny Wirtualnej w usłudze w chmurze z [wewnętrznego modułu równoważenia obciążenia](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)
   * Tworzenie maszyny Wirtualnej tooconnect zbyt[internetowy modułu równoważenia obciążenia](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)
   * Tworzenie maszyny Wirtualnej z [wiele kart sieciowych](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)
   * Tworzenie maszyny Wirtualnej z [wielu zastrzeżone adresy IP](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)

## <a name="next-steps"></a>Następne kroki
* [Rozwiązywanie problemów z błędami](backup-azure-vms-troubleshoot.md#restore)
* [Zarządzanie maszynami wirtualnymi](backup-azure-manage-vms.md)
