---
title: "aaaMonitor i rozwiązywanie problemów z ochroną maszyn wirtualnych i serwerów fizycznych | Dokumentacja firmy Microsoft"
description: "Usługa Azure Site Recovery koordynuje hello replikacji, trybu failover i odzyskiwania maszyn wirtualnych znajdujących się na lokalnych serwerach tooAzure lub dodatkowego centrum danych. Użyj tego artykułu toomonitor i rozwiązywanie problemów z ochroną witryny programu Virtual Machine Manager lub funkcji Hyper-V."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 0fc8e368-0c0e-4bb1-9d50-cffd5ad0853f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: d790375db5f30e98f009c8d8272558188c51934c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-troubleshoot-protection-for-virtual-machines-and-physical-servers"></a>Monitorowanie i rozwiązywanie problemów z ochroną maszyn wirtualnych i serwerów fizycznych
Tego monitorowania i rozwiązywania problemów Przewodnik ułatwia dowiesz się, jak kondycję replikacji tootrack i rozwiązywanie problemów z techniki dla usługi Azure Site Recovery.

## <a name="understand-hello-components"></a>Zrozumienie składników hello
### <a name="vmware-virtual-machine-or-physical-server-site-deployment-for-replication-between-on-premises-and-azure"></a>Maszyny wirtualnej VMware lub serwerów fizycznych wdrożenia lokacji replikacji między lokalną i platformą Azure
tooset się odzyskiwanie bazy danych między na lokalnej maszynie wirtualnej VMware lub serwerów fizycznych i usługi Azure, należy tooset hello konfiguracji serwera, główny serwer docelowy i procesu składników serwera na maszynie wirtualnej lub serwerze. Po włączeniu ochrony dla serwera źródłowego hello Azure Site Recovery instaluje funkcji Mobile Apps hello usługi Microsoft Azure App Service. Po awarii lokalnymi i po awarii serwera źródłowego hello za pośrednictwem tooAzure klienci muszą tooset serwer przetwarzania na platformie Azure i głównego serwera docelowego na serwerze źródłowym hello toorebuild lokalne lokalnie.

![Wdrożenie lokacji VMware/fizyczne replikacji między lokalną i platformą Azure](media/site-recovery-monitoring-and-troubleshooting/image18.png)

### <a name="virtual-machine-manager-site-deployment-for-replication-between-on-premises-sites"></a>Wdrożenie lokacji programu Virtual Machine Manager do replikacji między lokacjami lokalnymi
tooset się odzyskiwanie bazy danych między dwiema lokalizacjami lokalnymi, wymagany dostawca usługi Azure Site Recovery hello toodownload i zainstalować ją na powitania serwera programu Virtual Machine Manager. Dostawca Hello musi tooensure łączności Internet czy wszystkie operacje hello, które są uruchamiane z hello portalu Azure Pobierz operacje przetłumaczonego tooon firmą.

![Wdrożenie lokacji programu Virtual Machine Manager do replikacji między lokacjami lokalnymi](media/site-recovery-monitoring-and-troubleshooting/image1.png)

### <a name="virtual-machine-manager-site-deployment-for-replication-between-on-premises-locations-and-azure"></a>Wdrożenie lokacji programu Virtual Machine Manager replikacji między lokalizacje lokalną i platformą Azure
Po skonfigurowaniu odzyskiwanie bazy danych między lokalizacje lokalną i platformą Azure wymagany dostawca usługi Azure Site Recovery hello toodownload i zainstalować ją na powitania serwera programu Virtual Machine Manager. Należy również hello tooinstall agenta usług odzyskiwania Azure, którą należy toobe zainstalowane na każdym hoście funkcji Hyper-V. [Dowiedz się więcej](site-recovery-hyper-v-azure-architecture.md) Aby uzyskać więcej informacji.

![Wdrożenie lokacji programu Virtual Machine Manager replikacji między lokalizacje lokalną i platformą Azure](media/site-recovery-monitoring-and-troubleshooting/image2.png)

### <a name="hyper-v-site-deployment-for-replication-between-on-premises-locations-and-azure"></a>Wdrożenie lokacji funkcji Hyper-V dla replikacji między lokalnymi lokalizacji i na platformie Azure
Ten proces jest podobny tooVirtual Machine Manager wdrożenia. Hello tylko różnicą jest to, czy zainstalowane na sam host funkcji Hyper-V hello hello dostawcy usługi Azure Site Recovery i Agent usług odzyskiwania Azure. [Dowiedz się więcej](site-recovery-hyper-v-azure-architecture.md). .

## <a name="monitor-configuration-protection-and-recovery-operations"></a>Monitorowanie operacji konfiguracji, ochrony i odzyskiwania
Każdej operacji w usłudze Azure Site Recovery jest sprawdzana i śledzić w obszarze hello **zadania** kartę. Dla każdego konfiguracji, ochrony lub odzyskiwania błąd, przejdź toohello **zadania** karcie i Znajdź błędy.

![Hello filtru nie powiodło się na karcie zadania hello](media/site-recovery-monitoring-and-troubleshooting/image3.png)

Jeśli okaże się błędy w obszarze hello **zadania** , kliknij zadanie hello a kliknij **szczegóły błędu** dla tego zadania.

![przycisk Szczegóły błędu Hello](media/site-recovery-monitoring-and-troubleshooting/image4.png)

Szczegóły błędu Hello pomoże Ci identyfikować możliwa przyczyna i zalecenia dotyczące hello problem.

![Powoduje wyświetlenie okna dialogowego szczegóły błędu dla określonego zadania](media/site-recovery-monitoring-and-troubleshooting/image5.png)

W poprzednim przykładzie hello inną operację, która jest w toku jest prawdopodobnie toobe powoduje toofail konfiguracji ochrony hello. Rozwiąż problem hello na podstawie zalecenia hello, a następnie kliknij przycisk **RESART** tooinitiate hello ponownie operację.

![przycisk Uruchom ponownie Hello na karcie zadania hello](media/site-recovery-monitoring-and-troubleshooting/image6.png)

Witaj **ponowne URUCHOMIENIE** opcja nie jest dostępna dla wszystkich operacji. Jeśli operacja nie ma hello **ponowne URUCHOMIENIE** opcji, przejdź wstecz obiektu toohello i ponów operację hello ponownie. Możesz anulować wszystkie zadania, który jest w toku przy użyciu hello **ANULOWAĆ** przycisku.

![Witaj przycisku Anuluj](media/site-recovery-monitoring-and-troubleshooting/image7.png)

## <a name="monitor-replication-health-for-virtual-machines"></a>Monitorowanie kondycji replikacji dla maszyny wirtualnej
Można użyć dostawcy usługi Azure Site Recovery monitor tooremotely portalu Azure hello dla poszczególnych jednostek hello chronione. Kliknij przycisk **chronione elementy**, a następnie kliknij przycisk **chmur programu VMM** lub **grup ochrony**. Witaj **chmur programu VMM** karta jest dostępna tylko dla wdrożeń, które są oparte na programu Virtual Machine Manager. W innych sytuacjach jednostek hello chronione podlegają hello **grup ochrony** kartę.

![Opcje Hello chmur programu VMM i grup ochrony](media/site-recovery-monitoring-and-troubleshooting/image8.png)

Kliknij chronionej jednostki w hello odpowiednich chmury lub ochrony grupy toosee wszystkich dostępnych operacji są wyświetlone powitalne dolnym okienku.

![Dostępne opcje dla wybranej jednostki chronionych](media/site-recovery-monitoring-and-troubleshooting/image9.png)

Jak pokazano na powitania poprzedni zrzut ekranu, kondycja maszyny wirtualnej hello jest **krytyczny**. Możesz kliknąć hello **szczegóły błędu** przycisk na powitania dolnej toosee hello błędu. Oparte na powitania **możliwe przyczyny** i **zalecenie**, rozwiąż problem hello.

![przycisk Szczegóły błędu Hello](media/site-recovery-monitoring-and-troubleshooting/image10.png)

![Błędy i zalecenia w oknie dialogowym Szczegóły błędu hello](media/site-recovery-monitoring-and-troubleshooting/image11.png)

> [!NOTE]
> Jeśli wszystkie aktywne operacje są w toku lub nie powiodło się, przejdź toohello **zadania** widoku w postaci wymienionych wcześniejszego błędu hello tooview dla określonego zadania.
>
>

## <a name="troubleshoot-on-premises-hyper-v-issues"></a>Rozwiązywanie problemów funkcji Hyper-V lokalnej
Połącz konsolę Menedżera funkcji Hyper-V toohello lokalnego, wybierz hello maszyny wirtualnej i Sprawdź kondycję replikacji hello.

![Opcja tooview replikacji kondycji w konsoli Menedżera funkcji Hyper-V hello](media/site-recovery-monitoring-and-troubleshooting/image12.png)

W takim przypadku **kondycję replikacji** jest **krytyczny**. Kliknij prawym przyciskiem myszy hello maszyny wirtualnej, a następnie kliknij przycisk **replikacji** > **Wyświetl kondycję replikacji** toosee hello szczegóły.

![Stan replikacji dla określonej maszyny wirtualnej](media/site-recovery-monitoring-and-troubleshooting/image13.png)

Jeśli replikacja została wstrzymana hello maszyny wirtualnej, kliknij prawym przyciskiem myszy hello maszyny wirtualnej, a następnie kliknij **replikacji** > **Wznów replikację**.

![Opcja tooresume replikacji w konsoli Menedżera funkcji Hyper-V hello](media/site-recovery-monitoring-and-troubleshooting/image19.png)

Jeśli maszyna wirtualna jest migrowana nowego hosta funkcji Hyper-V, który jest w ramach klastra hello lub autonomiczne maszyny i hello hosta funkcji Hyper-V został skonfigurowany za pomocą usługi Azure Site Recovery, replikacji dla maszyny wirtualnej hello nie będzie w pełni funkcjonalne. Upewnij się, że nowy host funkcji Hyper-V hello spełnia wszystkie wymagania wstępne hello i jest konfigurowana przy użyciu usługi Azure Site Recovery.

### <a name="event-log"></a>Dziennik zdarzeń
| Źródła zdarzeń | Szczegóły |
| --- |:--- |
| **Aplikacje i usługi Dzienniki/Microsoft/VirtualMachineManager/Server/Admin** (serwer programu Virtual Machine Manager) |Udostępnia wiele różnych problemów z programu Virtual Machine Manager tootroubleshoot przydatne rejestrowania. |
| **Aplikacje i usługi Dzienniki/MicrosoftAzureRecoveryServices/replikacji** (host funkcji Hyper-V) |Udostępnia przydatne rejestrowania tootroubleshoot wiele problemów agenta usług odzyskiwania Microsoft Azure. <br/> ![Lokalizacja źródła zdarzeń replikacji dla hosta funkcji Hyper-V](media/site-recovery-monitoring-and-troubleshooting/eventviewer03.png) |
| **Aplikacje i usługi Microsoft/dzienniki/Azure lokacji odzyskiwania/dostawcy/Operational** (host funkcji Hyper-V) |Udostępnia przydatne rejestrowania tootroubleshoot wiele problemów z usługą Microsoft Azure Site Recovery. <br/> ![Lokalizacja źródła zdarzeń operacyjnych hosta funkcji Hyper-V](media/site-recovery-monitoring-and-troubleshooting/eventviewer02.png) |
| **Aplikacje i usługi Dzienniki/Microsoft/Windows/Hyper-V-VMMS/Admin** (host funkcji Hyper-V) |Udostępnia przydatne rejestrowania tootroubleshoot wiele problemów z zarządzaniem maszyny wirtualnej funkcji Hyper-V. <br/> ![Lokalizacja źródła zdarzeń Menedżera maszyny wirtualnej dla hostów funkcji Hyper-V](media/site-recovery-monitoring-and-troubleshooting/eventviewer01.png) |

### <a name="hyper-v-replication-logging-options"></a>Opcje rejestrowania replikację funkcji Hyper-V
Wszystkie zdarzenia, które odnoszą się replikacji tooHyper-V są rejestrowane w funkcji Hyper-V-VMMS hello\\Admin dziennika znajduje się w obszarze Dzienniki aplikacji i usług\\Microsoft\\systemu Windows. Ponadto można włączyć w dzienniku analityczne hello Usługa zarządzania maszynami wirtualnymi funkcji Hyper-V. tooenable to logowania, najpierw należy hello analityczne i debugowania dzienniki możliwych do wyświetlenia na powitania Podgląd zdarzeń. Otwórz Podgląd zdarzeń, a następnie kliknij przycisk **widoku** > **dzienniki Pokaż analityczne i debugowania**.

![Witaj opcji Dzienniki Pokaż analityczne i debugowania](media/site-recovery-monitoring-and-troubleshooting/image14.png)

Analityczne dziennika jest widoczna w obszarze **funkcji Hyper-V-VMMS**.

![Hello analityczne Zaloguj hello drzewa Podgląd zdarzeń](media/site-recovery-monitoring-and-troubleshooting/image15.png)

W hello **akcje** okienku, kliknij przycisk **Włącz dziennik**. Po włączeniu, zostanie wyświetlony w **monitora wydajności** jako **sesji śledzenia zdarzeń** znajduje się w obszarze **zestawy modułów zbierających dane.**

![Sesji śledzenia zdarzeń w drzewie monitora wydajności hello](media/site-recovery-monitoring-and-troubleshooting/image16.png)

tooview hello zebranych informacji, najpierw Zatrzymaj sesję śledzenia hello wyłączając hello dziennika. Zapisz dziennik hello i otwórz go ponownie w Podglądzie zdarzeń lub użyć innych narzędzi tooconvert go zgodnie z potrzebami.

## <a name="reach-out-for-microsoft-support"></a>Dotrzeć do firmy Microsoft Support
### <a name="log-collection"></a>Zbierania dzienników
Ochrona lokacji programu Virtual Machine Manager, można znaleźć zbyt[zbierania dzienników usługi Azure Site Recovery przy użyciu narzędzia pomocy technicznej platformy diagnostyki (SDP)](http://social.technet.microsoft.com/wiki/contents/articles/28198.asr-data-collection-and-analysis-using-the-vmm-support-diagnostics-platform-sdp-tool.aspx) toocollect hello wymagane dzienników.

W przypadku ochrony lokacji funkcji Hyper-V, Pobierz [narzędzie](https://dcupload.microsoft.com/tools/win7files/DIAG_ASRHyperV_global.DiagCab) i wykonaj go na powitania funkcji Hyper-V host toocollect hello dzienników.

Scenariusze serwera VMware/fizycznych, można znaleźć zbyt[zbierania dzienników usługi Azure Site Recovery VMware i ich ochrony lokacji fizycznej](http://social.technet.microsoft.com/wiki/contents/articles/30677.azure-site-recovery-log-collection-for-vmware-and-physical-site-protection.aspx) toocollect hello wymagane dzienników.

Narzędzie Hello zbiera dzienniki hello lokalnie w losowo wybranej nazwie podfolderze % LocalAppData%\ElevatedDiagnostics.

![Przykładowe kroki opisane z ochrony lokacji funkcji Hyper-V.](media/site-recovery-monitoring-and-troubleshooting/animate01.gif)

### <a name="open-a-support-ticket"></a>Otwórz bilet pomocy technicznej
tooraise biletu pomocy technicznej dla usługi Azure Site Recovery dotrzeć tooAzure obsługi przy użyciu adresu URL w <http://aka.ms/getazuresupport>.

## <a name="kb-articles"></a>Artykuły z bazy wiedzy
* [Jak litera dysku hello toopreserve dla chronionych maszyn wirtualnych, które są przełączenie do trybu failover lub migracji tooAzure](http://support.microsoft.com/kb/3031135)
* [Jak toomanage lokalnymi użycia przepustowości sieci ochrony tooAzure](https://support.microsoft.com/kb/3056159)
* [Usługa Azure Site Recovery: "hello klastra nie można odnaleźć zasobu" błąd podczas próby tooenable ochrony dla maszyny wirtualnej](http://support.microsoft.com/kb/3010979)
* [Zrozumienie i rozwiązywanie problemów z funkcją Hyper-V replikacji przewodnik](http://social.technet.microsoft.com/wiki/contents/articles/21948.hyper-v-replica-troubleshooting-guide.aspx)

## <a name="common-azure-site-recovery-errors-and-their-resolutions"></a>Typowe błędy usługi Azure Site Recovery i ich rozwiązania
Poniżej przedstawiono typowe błędy oraz ich rozwiązania. Każdy z błędów jest udokumentowany na stronie osobnych stron typu wiki.

### <a name="general"></a>Ogólne
* <span style="color:green;">Nowy</span> [zadania kończą się niepowodzeniem z powodu błędu "operacja jest w toku". Błąd 505, 514, 532.](http://social.technet.microsoft.com/wiki/contents/articles/32190.azure-site-recovery-jobs-failing-with-error-an-operation-is-in-progress-error-505-514-532.aspx)
* <span style="color:green;">Nowy</span> [zadania kończą się niepowodzeniem z powodu błędu "Serwer nie jest toohello połączenia internetowego". Błąd 25018.](http://social.technet.microsoft.com/wiki/contents/articles/32192.azure-site-recovery-jobs-failing-with-error-server-isn-t-connected-to-the-internet-error-25018.aspx)

### <a name="setup"></a>Konfiguracja
* [Nie można zarejestrować serwera programu Virtual Machine Manager Hello powodu tooan błąd wewnętrzny. Aby uzyskać więcej informacji na temat błędu hello, zapoznaj się z toohello widoku zadania w portalu usługi Site Recovery hello. Uruchom Instalatora ponownie tooregister powitania serwera.](http://social.technet.microsoft.com/wiki/contents/articles/25570.the-vmm-server-cannot-be-registered-due-to-an-internal-error-please-refer-to-the-jobs-view-in-the-site-recovery-portal-for-more-details-on-the-error-run-setup-again-to-register-the-server.aspx)
* [Połączenie nie może być nawiązane toohello magazyn Menedżera odzyskiwania funkcji Hyper-V. Sprawdź ustawienia serwera proxy hello lub spróbuj ponownie później.](http://social.technet.microsoft.com/wiki/contents/articles/25571.a-connection-cant-be-established-to-the-hyper-v-recovery-manager-vault-verify-the-proxy-settings-or-try-again-later.aspx)

### <a name="configuration"></a>Konfiguracja
* [Nie można toocreate grupy ochrony: Wystąpił błąd podczas pobierania listy hello serwerów.](http://blogs.technet.com/b/somaning/archive/2015/08/12/unable-to-create-the-protection-group-in-azure-site-recovery-portal.aspx)
* [Klaster hosta funkcji Hyper-V zawiera co najmniej jedną kartę sieciową statyczny lub żadna podłączona karta nie są skonfigurowane toouse DHCP.](http://social.technet.microsoft.com/wiki/contents/articles/25498.hyper-v-host-cluster-contains-at-least-one-static-network-adapter-or-no-connected-adapters-are-configured-to-use-dhcp.aspx)
* [Program Virtual Machine Manager nie ma uprawnienia toocomplete akcji.](http://social.technet.microsoft.com/wiki/contents/articles/31110.vmm-does-not-have-permissions-to-complete-an-action.aspx)
* [Nie można wybrać hello konta magazynu w ramach subskrypcji hello podczas konfigurowania ochrony.](http://social.technet.microsoft.com/wiki/contents/articles/32027.can-t-select-the-storage-account-within-the-subscription-while-configuring-protection.aspx)

### <a name="protection"></a>Ochrona
* <span style="color:green;">Nowy</span> [Włącz ochronę niepowodzeniem z powodu błędu "Nie można skonfigurować ochrony dla maszyny wirtualnej hello". Błąd 60007, 40003.](http://social.technet.microsoft.com/wiki/contents/articles/32194.azure-site-recovery-enable-protection-failing-with-error-protection-couldn-t-be-configured-for-the-virtual-machine-error-60007-40003.aspx)
* <span style="color:green;">Nowy</span> [Włącz ochronę niepowodzeniem z powodu błędu "Nie można włączyć ochrony dla maszyny wirtualnej hello." Błąd 70094.](http://social.technet.microsoft.com/wiki/contents/articles/32195.azure-site-recovery-enable-protection-failing-with-error-protection-couldn-t-be-enabled-for-the-virtual-machine-error-70094.aspx)
* <span style="color:green;">Nowy</span> [migracji na żywo błąd 23848 - hello maszyny wirtualnej będzie toobe przeniesiona przy użyciu typu Live. Może to spowodować przerwanie stanu ochrony odzyskiwania hello hello maszyny wirtualnej.](http://social.technet.microsoft.com/wiki/contents/articles/32021.live-migration-error-23848-the-virtual-machine-is-going-to-be-moved-using-type-live-this-could-break-the-recovery-protection-status-of-the-virtual-machine.aspx)
* [Nie można włączyć ochrony, ponieważ Agent nie jest zainstalowany na komputerze-hoście.](http://social.technet.microsoft.com/wiki/contents/articles/31105.enable-protection-failed-since-agent-not-installed-on-host-machine.aspx)
* [Nie można odnaleźć odpowiedniego hosta dla maszyny wirtualnej repliki hello - powodu toolow zasoby obliczeniowe.](http://social.technet.microsoft.com/wiki/contents/articles/25501.a-suitable-host-for-the-replica-virtual-machine-can-t-be-found-due-to-low-compute-resources.aspx)
* [Nie można odnaleźć odpowiedniego hosta dla maszyny wirtualnej repliki hello - powodu toono dołączone do sieci logicznej.](http://social.technet.microsoft.com/wiki/contents/articles/25502.a-suitable-host-for-the-replica-virtual-machine-can-t-be-found-due-to-no-logical-network-attached.aspx)
* [Nie można połączyć komputer hosta repliki toohello — nie można nawiązać połączenia.](http://social.technet.microsoft.com/wiki/contents/articles/31106.cannot-connect-to-the-replica-host-machine-connection-could-not-be-established.aspx)

### <a name="recovery"></a>Odzyskiwanie
* Program Virtual Machine Manager nie może ukończyć operacji hosta hello:
  * [Tryb failover toohello wybrany punkt odzyskiwania dla maszyny wirtualnej: ogólny błąd odmowy dostępu.](http://social.technet.microsoft.com/wiki/contents/articles/25504.fail-over-to-the-selected-recovery-point-for-virtual-machine-general-access-denied-error.aspx)
  * [Nie powiodło się toofail funkcji Hyper-V za pośrednictwem toohello wybrany punkt odzyskiwania dla maszyny wirtualnej: operacja została przerwana.  Spróbuj nowszą punktu odzyskiwania. (0x80004004).](http://social.technet.microsoft.com/wiki/contents/articles/25503.hyper-v-failed-to-fail-over-to-the-selected-recovery-point-for-virtual-machine-operation-aborted-try-a-more-recent-recovery-point-0x80004004.aspx)
  * Połączenia z serwerem hello nie można ustanowić (0x00002EFD).
    * [Tooenable replikację odwrotną dla maszyny wirtualnej funkcji Hyper-V, nie powiodło się.](http://social.technet.microsoft.com/wiki/contents/articles/25505.a-connection-with-the-server-could-not-be-established-0x00002efd-hyper-v-failed-to-enable-reverse-replication-for-virtual-machine.aspx)
    * [Tooenable replikacji dla maszyny wirtualnej maszyny wirtualnej funkcji Hyper-V, nie powiodło się.](http://social.technet.microsoft.com/wiki/contents/articles/25506.a-connection-with-the-server-could-not-be-established-0x00002efd-hyper-v-failed-to-enable-replication-for-virtual-machine-virtual-machine.aspx)
  * [Nie można zadeklarować w tryb failover maszyny wirtualnej.](http://social.technet.microsoft.com/wiki/contents/articles/25508.could-not-commit-failover-for-virtual-machine.aspx)
* [Witaj plan odzyskiwania zawiera maszyny wirtualne, które nie jest gotowa na planowany tryb failover.](http://social.technet.microsoft.com/wiki/contents/articles/25509.the-recovery-plan-contains-virtual-machines-which-are-not-ready-for-planned-failover.aspx)
* [Witaj maszyny wirtualnej nie jest gotowa na planowany tryb failover.](http://social.technet.microsoft.com/wiki/contents/articles/25507.the-virtual-machine-isn-t-ready-for-planned-failover.aspx)
* [Maszyna wirtualna nie jest uruchomiony i nie jest wyłączony.](http://social.technet.microsoft.com/wiki/contents/articles/25510.virtual-machine-is-not-running-and-is-not-powered-off.aspx)
* [Operacja poza pasmem wystąpiło na maszynie wirtualnej i zatwierdzania trybu failover nie powiodła się.](http://social.technet.microsoft.com/wiki/contents/articles/25507.the-virtual-machine-isn-t-ready-for-planned-failover.aspx)
* Testowanie trybu failover
  * [Nie można zainicjować trybu failover, ponieważ trwa testowanie trybu failover.](http://social.technet.microsoft.com/wiki/contents/articles/31111.failover-could-not-be-initiated-since-test-failover-is-in-progress.aspx)
* <span style="color:green;">NOWE</span> pracy awaryjnej upłynie limit czasu "PreFailoverWorkflow zadania WaitForScriptExecutionTaskTimeout" ze względu na ustawienia konfiguracji toohello na powitania grupy zabezpieczeń sieci skojarzonych z hello maszyny wirtualnej lub hello podsieci toowhich hello maszyny należy. Odwołuje się zbyt["task PreFailoverWorkflow WaitForScriptExecutionTaskTimeout"](https://aka.ms/troubleshoot-nsg-issue-azure-site-recovery) szczegółowe informacje.

### <a name="configuration-server-process-server-master-target"></a>Serwer konfiguracji, serwer przetwarzania, główny serwer docelowy
* [Hello hosta ESXi, na które hello PS/CS jest hostowany jako maszyny Wirtualnej kończy się niepowodzeniem z purpurowa ekran.](http://social.technet.microsoft.com/wiki/contents/articles/31107.vmware-esxi-host-experiences-a-purple-screen-of-death.aspx)

### <a name="remote-desktop-troubleshooting-after-failover"></a>Rozwiązywanie problemów po pracy awaryjnej pulpitu zdalnego
* Wielu klientów ma muszą ponosić toohello tooconnect problemów przejścia w tryb failover maszyny wirtualnej platformy Azure. [Rozwiązywanie problemów z tooRDP dokumentu do maszyny wirtualnej hello hello użyj](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

#### <a name="adding-a-public-ip-on-a-resource-manager-virtual-machine"></a>Dodawanie publicznego adresu IP na maszynie wirtualnej Menedżera zasobów
Jeśli hello **Connect** przycisk w portalu hello jest wygaszona i nie jesteś tooAzure połączonych za pośrednictwem połączenia VPN Express Route lub lokacja-lokacja, należy toocreate i przypisać publicznego adresu IP sieci maszyny wirtualnej przed użyciem zdalnego Udostępniane pulpitu/powłoki. Następnie można dodać publicznego adresu IP dla interfejsu sieciowego hello hello maszyny wirtualnej.  

![Dodawanie publicznego adresu IP dla interfejsu sieci hello przejścia w tryb failover maszyny wirtualnej](media/site-recovery-monitoring-and-troubleshooting/createpublicip.gif)
