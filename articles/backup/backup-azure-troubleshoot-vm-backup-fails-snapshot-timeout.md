---
title: "Rozwiązywanie problemów z usługi Kopia zapasowa Azure awarii: niedostępny stan agenta gościa | Dokumentacja firmy Microsoft"
description: "Objawy, przyczyny i rozwiązania tooerror powiązane błędy kopia zapasowa Azure: nie można skomunikować się z hello agenta maszyny Wirtualnej"
services: backup
documentationcenter: 
author: genlin
manager: cshepard
editor: 
keywords: "Kopia zapasowa Azure; Agent maszyny Wirtualnej; Łączności sieciowej;"
ms.assetid: 4b02ffa4-c48e-45f6-8363-73d536be4639
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: genli;markgal;
ms.openlocfilehash: 724c61ba80d0a9ef91a5f8543ae72bb86968881b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-backup-failure-issues-with-agent-andor-extension"></a>Rozwiązywanie problemów z usługi Kopia zapasowa Azure awarii: problemy z agenta i/lub rozszerzenie

Ten artykuł zawiera rozwiązywania problemów toohelp kroki rozwiązania niepowodzenia tworzenia kopii zapasowej powiązane tooproblems komunikuje się z agenta maszyny Wirtualnej i rozszerzenia.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="vm-agent-unable-toocommunicate-with-azure-backup"></a>Agent maszyny Wirtualnej toocommunicate z usługi Kopia zapasowa Azure
Po zarejestrować i zaplanować maszyny Wirtualnej dla usługi Kopia zapasowa Azure hello kopii zapasowej inicjuje zadania hello komunikując się z hello tootake agenta maszyny Wirtualnej w momencie migawki. Wszelkie hello następujące warunki mogą uniemożliwić migawki hello z inicjowane, co z kolei może prowadzić tooBackup awarii. Wykonaj poniżej kroki w podanej kolejności hello rozwiązywania problemów, a następnie ponów operację.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Przyczyna 1: [hello maszyny Wirtualnej nie ma dostępu Internet](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Przyczyny 2: [hello agent jest zainstalowany w hello maszyny Wirtualnej, ale nie odpowiada (dla maszyn wirtualnych systemu Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Przyczyny 3: [hello agent zainstalowany w hello maszyny Wirtualnej są nieaktualne (dla maszyn wirtualnych systemu Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Przyczyna 4: [nie można pobrać stanu migawki hello lub nie można pobrać migawek](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Przyczyny 5: [hello rozszerzenia kopii zapasowej nie powiedzie się, tooupdate lub obciążenia](#the-backup-extension-fails-to-update-or-load)

## <a name="snapshot-operation-failed-due-toono-network-connectivity-on-hello-virtual-machine"></a>Operacja migawki nie powiodła z powodu toono łączności sieciowej na maszynie wirtualnej hello
Po zarejestrować i zaplanować maszyny Wirtualnej dla usługi Kopia zapasowa Azure hello kopii zapasowej inicjuje zadania hello komunikując się z migawki tootake punktu w czasie tworzenia kopii zapasowej rozszerzenia maszyny Wirtualnej hello. Wszelkie hello następujące warunki mogą uniemożliwić migawki hello z inicjowane, co z kolei może prowadzić tooBackup awarii. Wykonaj poniżej kroki w podanej kolejności hello rozwiązywania problemów, a następnie ponów operację.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Przyczyna 1: [hello maszyny Wirtualnej nie ma dostępu Internet](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Przyczyny 2: [nie można pobrać stanu migawki hello lub nie można pobrać migawek](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-3-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Przyczyny 3: [hello rozszerzenia kopii zapasowej nie powiedzie się, tooupdate lub obciążenia](#the-backup-extension-fails-to-update-or-load)

## <a name="vmsnapshot-extension-operation-failed"></a>Nie można wykonać operacji rozszerzenia VMSnapshot

Po zarejestrować i zaplanować maszyny Wirtualnej dla usługi Kopia zapasowa Azure hello kopii zapasowej inicjuje zadania hello komunikując się z migawki tootake punktu w czasie tworzenia kopii zapasowej rozszerzenia maszyny Wirtualnej hello. Wszelkie hello następujące warunki mogą uniemożliwić migawki hello z inicjowane, co z kolei może prowadzić tooBackup awarii. Wykonaj poniżej kroki w podanej kolejności hello rozwiązywania problemów, a następnie ponów operację.
##### <a name="cause-1-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Przyczyna 1: [nie można pobrać stanu migawki hello lub nie można pobrać migawek](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-2-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Przyczyny 2: [hello rozszerzenia kopii zapasowej nie powiedzie się, tooupdate lub obciążenia](#the-backup-extension-fails-to-update-or-load)
##### <a name="cause-3-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Przyczyny 3: [hello maszyny Wirtualnej nie ma dostępu Internet](#the-vm-has-no-internet-access)
##### <a name="cause-4-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Przyczyna 4: [hello agent jest zainstalowany w hello maszyny Wirtualnej, ale nie odpowiada (dla maszyn wirtualnych systemu Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-5-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Przyczyny 5: [hello agent zainstalowany w hello maszyny Wirtualnej są nieaktualne (dla maszyn wirtualnych systemu Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)

## <a name="unable-tooperform-hello-operation-as-hello-vm-agent-is-not-responsive"></a>Operacja hello tooperform jako hello agenta maszyny Wirtualnej nie jest reakcji

Po zarejestrować i zaplanować maszyny Wirtualnej dla usługi Kopia zapasowa Azure hello kopii zapasowej inicjuje zadania hello komunikując się z migawki tootake punktu w czasie tworzenia kopii zapasowej rozszerzenia maszyny Wirtualnej hello. Wszelkie hello następujące warunki mogą uniemożliwić migawki hello z inicjowane, co z kolei może prowadzić tooBackup awarii. Wykonaj poniżej kroki w podanej kolejności hello rozwiązywania problemów, a następnie ponów operację.
##### <a name="cause-1-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Przyczyna 1: [hello agent jest zainstalowany w hello maszyny Wirtualnej, ale nie odpowiada (dla maszyn wirtualnych systemu Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-2-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Przyczyny 2: [hello agent zainstalowany w hello maszyny Wirtualnej są nieaktualne (dla maszyn wirtualnych systemu Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-3-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Przyczyny 3: [hello maszyny Wirtualnej nie ma dostępu Internet](#the-vm-has-no-internet-access)

## <a name="backup-failed-with-an-internal-error---please-retry-hello-operation-in-a-few-minutes"></a>Kopii zapasowej nie powiodło się z powodu wewnętrznego błędu — ponów operację hello za kilka minut

Po zarejestrować i zaplanować maszyny Wirtualnej dla usługi Kopia zapasowa Azure hello kopii zapasowej inicjuje zadania hello komunikując się z migawki tootake punktu w czasie tworzenia kopii zapasowej rozszerzenia maszyny Wirtualnej hello. Wszelkie hello następujące warunki mogą uniemożliwić migawki hello z inicjowane, co z kolei może prowadzić tooBackup awarii. Wykonaj poniżej kroki w podanej kolejności hello rozwiązywania problemów, a następnie ponów operację.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Przyczyna 1: [hello maszyny Wirtualnej nie ma dostępu Internet](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-agent-installed-in-hello-vm-but-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Przyczyny 2: [agenta hello zainstalowane na powitania maszyny Wirtualnej, ale odpowiadać (dla maszyn wirtualnych systemu Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Przyczyny 3: [hello agent zainstalowany w hello maszyny Wirtualnej są nieaktualne (dla maszyn wirtualnych systemu Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Przyczyna 4: [nie można pobrać stanu migawki hello lub nie można pobrać migawek](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Przyczyny 5: [hello rozszerzenia kopii zapasowej nie powiedzie się, tooupdate lub obciążenia](#the-backup-extension-fails-to-update-or-load)


## <a name="causes-and-solutions"></a>Przyczyny i potencjalne rozwiązania

### <a name="hello-vm-has-no-internet-access"></a>Witaj maszyny Wirtualnej nie ma dostępu Internet
Na powitania wymagania wdrożenia hello maszyny Wirtualnej nie ma dostępu Internetu lub ma ograniczenia w miejscu, uniemożliwiające toohello dostęp do infrastruktury platformy Azure.

toofunction poprawnie, wymaga zapasowy numer wewnętrzny hello adresów Azure publicznego adresu IP toohello łączności. rozszerzenie Hello wysyła polecenia tooan usługi Azure Storage punktu końcowego (adres URL protokołu HTTP) toomanage hello migawek hello maszyny Wirtualnej. Jeśli hello rozszerzenia nie ma żadnych toohello dostępu, publicznej sieci Internet, po pewnym czasie kopii zapasowej nie powiedzie się.

####  <a name="solution"></a>Rozwiązanie
tooresolve hello problem, wypróbuj jedną z metod hello wymienione w tym miejscu.
##### <a name="allow-access-toohello-azure-datacenter-ip-ranges"></a>Zezwalaj na dostęp do zakresów IP centrum danych Azure toohello

1. Uzyskaj hello [listy Azure datacenter IP](https://www.microsoft.com/download/details.aspx?id=41653) tooallow dostęp do.
2. Odblokuj hello adresów IP, uruchamiając hello **NetRoute nowy** polecenia cmdlet w hello maszyny Wirtualnej platformy Azure w oknie programu PowerShell z podwyższonym poziomem uprawnień. Uruchom polecenie cmdlet hello jako administrator.
3. tooallow toohello dostępu do adresów IP, Dodaj reguły toohello sieciowej grupy zabezpieczeń, jeśli istnieje.

##### <a name="create-a-path-for-http-traffic-tooflow"></a>Tworzenie ścieżki dla tooflow ruch HTTP

1. Jeśli masz ograniczeń sieci w miejscu (na przykład grupa zabezpieczeń sieci), należy wdrożyć ruch HTTP serwera proxy serwera tooroute hello.
2. tooallow toohello dostęp do Internetu z serwera proxy HTTP hello, Dodaj reguły toohello sieciowej grupy zabezpieczeń, jeśli istnieje.

toolearn tooset się serwer proxy HTTP kopii zapasowych maszyn wirtualnych, zobacz temat [przygotowanie Twojego środowiska tooback zapasowych maszyn wirtualnych Azure](backup-azure-vms-prepare.md#using-an-http-proxy-for-vm-backups).

W przypadku, gdy używane są zarządzane dysków, może być konieczne dodatkowe portu (8443) otwarcia na powitania zapory.

### <a name="hello-agent-installed-in-hello-vm-but-unresponsive-for-windows-vms"></a>agent Hello zainstalowane na powitania maszyny Wirtualnej, ale odpowiadać (dla maszyn wirtualnych systemu Windows)

#### <a name="solution"></a>Rozwiązanie
Witaj agenta maszyny Wirtualnej może być uszkodzony lub może hello usługa została zatrzymana. Ponowne instalowanie agenta maszyny Wirtualnej hello byłaby pomocna Pobierz hello najnowszą wersję i uruchom ponownie hello komunikacji.

1. Sprawdź, czy Usługa agenta gościa z systemem Windows w usługi (services.msc) jest uruchomiona hello maszyny wirtualnej. Spróbuj ponownie uruchom usługę agenta gościa Windows hello i zainicjować hello kopii zapasowej<br>
2. Jeśli nie jest widoczny w usługach, sprawdź w aplecie Programy i funkcje czy Usługa agenta gościa z systemem Windows jest zainstalowany.
4. Jeśli jesteś stanie tooview w aplecie Programy i funkcje Odinstaluj hello agenta gościa z systemem Windows.
5. Pobierz i zainstaluj hello [najnowszej wersji pliku MSI agenta](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Potrzebujesz instalacji hello toocomplete uprawnienia administratora.
6. Następnie powinno być możliwe tooview usługi agenta gościa z systemem Windows w usługach
7. Spróbuj uruchomić, klikając pozycję "Utwórz kopię zapasową teraz" w portalu hello na — żądanie/kopię zapasową adhoc.

Sprawdź również, Twoja maszyna wirtualna ma  **[.NET 4.5 zainstalowane w systemie hello](https://docs.microsoft.com/en-us/dotnet/framework/migration-guide/how-to-determine-which-versions-are-installed)**. Jest to wymagane toocommunicate agenta maszyny Wirtualnej hello z usługą hello

### <a name="hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vms"></a>agent Hello zainstalowany w hello maszyny Wirtualnej są nieaktualne (dla maszyn wirtualnych systemu Linux)

#### <a name="solution"></a>Rozwiązanie
Najbardziej związane z agenta lub rozszerzenie błędów dla maszyn wirtualnych systemu Linux są spowodowane przez problemy, które mają wpływ na nieaktualne agenta maszyny Wirtualnej. tootroubleshoot ten problem, wykonaj następujące ogólne wytyczne:

1. Wykonaj instrukcje hello [aktualizowanie hello agenta maszyny Wirtualnej systemu Linux](../virtual-machines/linux/update-agent.md).

 >[!NOTE]
 >Firma Microsoft *zdecydowanie zaleca się* zaktualizowanie agenta hello tylko za pośrednictwem repozytorium dystrybucji. Nie zaleca się pobierania kodu agenta hello bezpośrednio z witryny GitHub i zaktualizowaniem go. Jeśli hello najnowsza wersja agenta jest niedostępna w przypadku dystrybucji, skontaktuj się z dystrybucji pomocy technicznej Aby uzyskać instrukcje dotyczące tooinstall go. toocheck hello najnowszych agenta, przejdź toohello [agenta Windows Azure w systemie Linux](https://github.com/Azure/WALinuxAgent/releases) strony w repozytorium GitHub hello.

2. Upewnij się, że tego hello Azure agent działa na powitania maszyny Wirtualnej, uruchamiając następujące polecenie hello:`ps -e`

 Jeśli proces hello nie jest uruchomiona, uruchom go ponownie przy użyciu hello następujące polecenia:

 * Dla Ubuntu:`service walinuxagent start`
 * Inne dystrybucji:`service waagent start`

3. [Konfigurowanie hello automatycznego ponownego uruchomienia agenta](https://github.com/Azure/WALinuxAgent/wiki/Known-Issues#mitigate_agent_crash).
4. Uruchom nową kopię zapasową testu. Jeśli hello błąd będzie się powtarzać, Zbierz powitania po dzienniki z maszyny Wirtualnej powitania klienta:

   * /var/lib/waagent/*.XML
   * /var/log/waagent.log
   * / var/logowania/azure / *

Jeśli wymagane pełne rejestrowanie dla agenta waagent, wykonaj następujące kroki:

1. W pliku /etc/waagent.conf hello Znajdź powitania po wierszu: **Włącz pełne rejestrowanie (y | n)**
2. Zmień hello **Logs.Verbose** wartość z  *n*  za*y*.
3. Zapisz zmiany hello i ponownie uruchom agenta waagent wykonując hello poprzednie kroki w tej sekcji.

### <a name="hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Nie można pobrać stanu migawki Hello lub nie można pobrać migawek
Hello kopii zapasowej maszyny Wirtualnej zależy od wydawania migawki polecenia toohello podstawowym konta magazynu. Kopia zapasowa może nie powieść, ponieważ zawiera ona żadnego konta magazynu toohello dostępu lub hello wykonywanie zadania migawki hello została opóźniona.

#### <a name="solution"></a>Rozwiązanie
Witaj następujące warunki mogą spowodować niepowodzenie zadań migawki:

| Przyczyna | Rozwiązanie |
| --- | --- |
| Witaj maszyna wirtualna ma skonfigurowano kopii zapasowej programu SQL Server. | Domyślnie pełna kopia zapasowa VSS uruchomienia tworzenia kopii zapasowej hello maszyny Wirtualnej na maszynach wirtualnych systemu Windows. Na maszynach wirtualnych, które działają na serwerach programu SQL Server i programem SQL Server kopia zapasowa została skonfigurowana, mogą występować opóźnienia z powodu wykonywania migawki.<br><br>W przypadku niepowodzenia tworzenia kopii zapasowej z powodu problemu z migawki, należy ustawić powitania po klucz rejestru:<br><br>**[HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT] "USEVSSCOPYBACKUP"="TRUE"** |
| Witaj stanu maszyny Wirtualnej jest raportowane niepoprawnie, ponieważ hello maszyna wirtualna jest zamknięta w protokole RDP. | Jeśli wyłączysz hello maszyny Wirtualnej w protokołu RDP (Remote Desktop) sprawdź toodetermine portalu hello czy hello stanu maszyny Wirtualnej jest prawidłowa. Jeśli nie jest poprawny, należy zamknąć hello maszyny Wirtualnej w portalu hello za pomocą hello **zamknięcia** opcji na powitania maszyny Wirtualnej z pulpitu nawigacyjnego. |
| Wiele maszyn wirtualnych z hello tej samej usługi chmury są skonfigurowane tooback się na powitania tym samym czasie. | Jest najlepszym toospread praktyki limit harmonogramy tworzenia kopii zapasowej powitania dla maszyn wirtualnych z hello sama usługa w chmurze. |
| Witaj maszyna wirtualna jest uruchomiona na wysokiego użycia procesora CPU lub pamięci. | Hello maszyna wirtualna jest uruchomiona na wysokie użycie Procesora (ponad 90%) lub wysokie użycie pamięci, zadania migawki hello jest umieszczona w kolejce i opóźnione, a ostatecznie upływie limitu czasu. W takim przypadku spróbuj kopii zapasowej na żądanie. |
| Hello maszyny Wirtualnej nie można pobrać adres hosta/sieci szkieletowej powitania od serwera DHCP. | DHCP musi być włączona wewnątrz hello gościa dla hello toowork kopii zapasowych maszyn wirtualnych IaaS.  Jeśli hello maszyny Wirtualnej nie można pobrać adresu hosta/sieci szkieletowej hello z odpowiedzi DHCP 245, go nie można pobrać lub uruchomić wszystkich rozszerzeń. Jeśli potrzebujesz statycznego prywatnego adresu IP, należy skonfigurować go za pośrednictwem platformy hello. Witaj opcji DHCP wewnątrz powitalne maszyny Wirtualnej, należy pozostawić włączone. Aby uzyskać więcej informacji, zobacz [ustawienie wewnętrzny statycznego prywatnego adresu IP](../virtual-network/virtual-networks-reserved-private-ip.md). |

### <a name="hello-backup-extension-fails-tooupdate-or-load"></a>zapasowy numer wewnętrzny Hello zakończy się niepowodzeniem, tooupdate lub obciążenia
Jeśli nie można załadować rozszerzeń, tworzenia kopii zapasowej nie powiedzie się, ponieważ nie można pobrać migawek.

#### <a name="solution"></a>Rozwiązanie

**Dla gości systemu Windows:** Sprawdź, czy usługa iaasvmprovider hello jest włączony i ma typ uruchamiania *automatyczne*. Jeśli usługa hello nie jest skonfigurowana w taki sposób, włączyć toodetermine czy hello następnej kopii zapasowej zakończy się pomyślnie.

**Dla systemu Linux gości:** 1.0.91.0 jest Sprawdź hello najnowszą wersję VMSnapshot dla systemu Linux (rozszerzenie hello używane przez kopię zapasową).<br>


Jeśli zapasowy numer wewnętrzny hello nadal nie tooupdate lub obciążenia, możesz wymusić toobe rozszerzenia VMSnapshot hello ponownie załadowana przez odinstalowanie hello rozszerzenia. Witaj przy następnej próbie kopii zapasowej spowoduje ponowne załadowanie hello rozszerzenia.

toouninstall hello rozszerzenia, hello następujące:

1. Przejdź toohello [portalu Azure](https://portal.azure.com/).
2. Zlokalizuj hello maszynę Wirtualną, która ma problemy z kopii zapasowej.
3. Kliknij przycisk **ustawienia**.
4. Kliknij przycisk **rozszerzenia**.
5. Kliknij przycisk **Vmsnapshot rozszerzenia**.
6. Kliknij przycisk **odinstalować**.

Ta procedura powoduje, że toobe rozszerzenia hello ponownej instalacji podczas tworzenia kopii zapasowej dalej hello.

