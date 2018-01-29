---
title: "Rozwiązywanie problemów z usługi Kopia zapasowa Azure awarii: niedostępny stan agenta gościa | Dokumentacja firmy Microsoft"
description: "Objawy, przyczyny i rozwiązania związane z agenta, rozszerzenia, dyski awarie usługi Kopia zapasowa Azure"
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
ms.topic: troubleshooting
ms.date: 01/09/2018
ms.author: genli;markgal;sogup;
ms.openlocfilehash: 0be2391268e11593802cb0f455e8c4553f0d4731
ms.sourcegitcommit: 1fbaa2ccda2fb826c74755d42a31835d9d30e05f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/22/2018
---
# <a name="troubleshoot-azure-backup-failure-issues-with-agent-andor-extension"></a>Rozwiązywanie problemów z usługi Kopia zapasowa Azure awarii: problemy z agenta i/lub rozszerzenie

Ten artykuł zawiera kroki ułatwiające rozwiązanie tworzenia kopii zapasowej błędy związane z problemami w ramach komunikacji z agentem maszyny Wirtualnej i rozszerzenia.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="vm-agent-unable-to-communicate-with-azure-backup"></a>Agent maszyny Wirtualnej nie można nawiązać połączenia z usługą kopia zapasowa Azure

> [!NOTE]
> Jeśli kopie zapasowe Azure maszyny Wirtualnej systemu Linux uruchomiony niepowodzeniem z powodu tego błędu na lub po 4 stycznia 2018, uruchom następujące polecenie w odpowiednich maszynach wirtualnych, a następnie spróbuj ponownie tworzenie kopii zapasowych

    sudo rm -f /var/lib/waagent/*.[0-9]*.xml

Po zarejestrować i zaplanować maszyny Wirtualnej dla usługi Kopia zapasowa Azure kopii zapasowej inicjuje zadania przy komunikacji z agentem maszyny Wirtualnej do tworzenia migawki punktu w czasie. Jeden z następujących warunków mogą uniemożliwić migawki z inicjowane, co z kolei może prowadzić do awarii kopii zapasowej. Postępuj zgodnie z poniższych czynności w podanej kolejności i ponów operację.

##### <a name="cause-1-the-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Przyczyna 1: [maszyny Wirtualnej nie ma dostępu Internet](#the-vm-has-no-internet-access)
##### <a name="cause-2-the-agent-is-installed-in-the-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Przyczyny 2: [agent jest zainstalowany na maszynie wirtualnej, ale nie odpowiada (dla maszyn wirtualnych systemu Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-the-agent-installed-in-the-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Przyczyny 3: [agent zainstalowany na maszynie wirtualnej są nieaktualne (dla maszyn wirtualnych systemu Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Przyczyna 4: [nie można pobrać stanu migawki lub migawka nie można pobrać](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-the-backup-extension-fails-to-update-or-loadthe-backup-extension-fails-to-update-or-load"></a>Przyczyny 5: [zapasowy numer wewnętrzny nie może zaktualizować lub załadować](#the-backup-extension-fails-to-update-or-load)
##### <a name="cause-6-azure-classic-vms-may-require-additional-step-to-complete-registrationazure-classic-vms-may-require-additional-step-to-complete-registration"></a>Przyczyna 6: [Azure klasycznych maszyn wirtualnych może wymagać dodatkowych czynności, aby ukończyć rejestrację](#azure-classic-vms-may-require-additional-step-to-complete-registration)

## <a name="snapshot-operation-failed-due-to-no-network-connectivity-on-the-virtual-machine"></a>Operacja migawki nie powiodła się ze względu na brak łączności sieciowej na maszynie wirtualnej
Po zarejestrować i zaplanować maszyny Wirtualnej dla usługi Kopia zapasowa Azure kopii zapasowej inicjuje zadania komunikując się z rozszerzenia kopii zapasowej maszyny Wirtualnej do tworzenia migawki punktu w czasie. Jeden z następujących warunków mogą uniemożliwić migawki z inicjowane, co z kolei może prowadzić do awarii kopii zapasowej. Postępuj zgodnie z poniższych czynności w podanej kolejności i ponów operację.
##### <a name="cause-1-the-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Przyczyna 1: [maszyny Wirtualnej nie ma dostępu Internet](#the-vm-has-no-internet-access)
##### <a name="cause-2-the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Przyczyny 2: [nie można pobrać stanu migawki lub migawka nie można pobrać](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-3-the-backup-extension-fails-to-update-or-loadthe-backup-extension-fails-to-update-or-load"></a>Przyczyny 3: [zapasowy numer wewnętrzny nie może zaktualizować lub załadować](#the-backup-extension-fails-to-update-or-load)

## <a name="vmsnapshot-extension-operation-failed"></a>Nie można wykonać operacji rozszerzenia VMSnapshot

Po zarejestrować i zaplanować maszyny Wirtualnej dla usługi Kopia zapasowa Azure kopii zapasowej inicjuje zadania komunikując się z rozszerzenia kopii zapasowej maszyny Wirtualnej do tworzenia migawki punktu w czasie. Jeden z następujących warunków mogą uniemożliwić migawki z inicjowane, co z kolei może prowadzić do awarii kopii zapasowej. Postępuj zgodnie z poniższych czynności w podanej kolejności i ponów operację.
##### <a name="cause-1-the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Przyczyna 1: [nie można pobrać stanu migawki lub migawka nie można pobrać](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-2-the-backup-extension-fails-to-update-or-loadthe-backup-extension-fails-to-update-or-load"></a>Przyczyny 2: [zapasowy numer wewnętrzny nie może zaktualizować lub załadować](#the-backup-extension-fails-to-update-or-load)
##### <a name="cause-3-the-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Przyczyny 3: [maszyny Wirtualnej nie ma dostępu Internet](#the-vm-has-no-internet-access)
##### <a name="cause-4-the-agent-is-installed-in-the-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Przyczyna 4: [agent jest zainstalowany na maszynie wirtualnej, ale nie odpowiada (dla maszyn wirtualnych systemu Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-5-the-agent-installed-in-the-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Przyczyny 5: [agent zainstalowany na maszynie wirtualnej są nieaktualne (dla maszyn wirtualnych systemu Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)

## <a name="unable-to-perform-the-operation-as-the-vm-agent-is-not-responsive"></a>Nie można wykonać operacji, ponieważ Agent maszyny Wirtualnej nie jest elastyczny

Po zarejestrować i zaplanować maszyny Wirtualnej dla usługi Kopia zapasowa Azure kopii zapasowej inicjuje zadania komunikując się z rozszerzenia kopii zapasowej maszyny Wirtualnej do tworzenia migawki punktu w czasie. Jeden z następujących warunków mogą uniemożliwić migawki z inicjowane, co z kolei może prowadzić do awarii kopii zapasowej. Postępuj zgodnie z poniższych czynności w podanej kolejności i ponów operację.
##### <a name="cause-1-the-agent-is-installed-in-the-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Przyczyna 1: [agent jest zainstalowany na maszynie wirtualnej, ale nie odpowiada (dla maszyn wirtualnych systemu Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-2-the-agent-installed-in-the-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Przyczyny 2: [agent zainstalowany na maszynie wirtualnej są nieaktualne (dla maszyn wirtualnych systemu Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-3-the-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Przyczyny 3: [maszyny Wirtualnej nie ma dostępu Internet](#the-vm-has-no-internet-access)

## <a name="backup-failed-with-an-internal-error---please-retry-the-operation-in-a-few-minutes"></a>Kopii zapasowej nie powiodło się z powodu wewnętrznego błędu — spróbuj ponownie wykonać operację w ciągu kilku minut

Po zarejestrować i zaplanować maszyny Wirtualnej dla usługi Kopia zapasowa Azure kopii zapasowej inicjuje zadania komunikując się z rozszerzenia kopii zapasowej maszyny Wirtualnej do tworzenia migawki punktu w czasie. Jeden z następujących warunków mogą uniemożliwić migawki z inicjowane, co z kolei może prowadzić do awarii kopii zapasowej. Postępuj zgodnie z poniższych czynności w podanej kolejności i ponów operację.
##### <a name="cause-1-the-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Przyczyna 1: [maszyny Wirtualnej nie ma dostępu Internet](#the-vm-has-no-internet-access)
##### <a name="cause-2-the-agent-installed-in-the-vm-but-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Przyczyny 2: [agent zainstalowany na maszynie wirtualnej, ale odpowiadać (dla maszyn wirtualnych systemu Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-the-agent-installed-in-the-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Przyczyny 3: [agent zainstalowany na maszynie wirtualnej są nieaktualne (dla maszyn wirtualnych systemu Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Przyczyna 4: [nie można pobrać stanu migawki lub migawka nie można pobrać](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-the-backup-extension-fails-to-update-or-loadthe-backup-extension-fails-to-update-or-load"></a>Przyczyny 5: [zapasowy numer wewnętrzny nie może zaktualizować lub załadować](#the-backup-extension-fails-to-update-or-load)
##### <a name="cause-6-backup-service-does-not-have-permission-to-delete-the-old-restore-points-due-to-resource-group-lockbackup-service-does-not-have-permission-to-delete-the-old-restore-points-due-to-resource-group-lock"></a>Przyczyna 6: [usługi Kopia zapasowa nie ma uprawnienia do usuwania starych punktów przywracania z powodu blokady grupy zasobów](#backup-service-does-not-have-permission-to-delete-the-old-restore-points-due-to-resource-group-lock)

## <a name="the-specified-disk-configuration-is-not-supported"></a>Określona konfiguracja dysku nie jest obsługiwana.

> [!NOTE]
> Mamy prywatnej wersji zapoznawczej do obsługi kopii zapasowych dla maszyn wirtualnych o > dysków 1TB. Aby uzyskać szczegółowe informacje, zobacz [prywatnej wersji zapoznawczej do obsługi kopii zapasowych dużych dysków maszyny Wirtualnej](https://gallery.technet.microsoft.com/Instant-recovery-point-and-25fe398a)
>
>

Kopia zapasowa Azure nie obsługuje obecnie rozmiary dysków [większa niż 1023GB](https://docs.microsoft.com/azure/backup/backup-azure-arm-vms-prepare#limitations-when-backing-up-and-restoring-a-vm). 
- Jeśli masz dyski większe od 1 TB, [dołącz nowe dyski](https://docs.microsoft.com/azure/virtual-machines/windows/attach-managed-disk-portal) o rozmiarze poniżej 1 TB. <br>
- Następnie skopiuj dane z dysku większego od 1 TB na nowo utworzone dyski mniejsze niż 1 TB. <br>
- Upewnij się, że wszystkie dane zostały skopiowane, a następnie usuń dyski większe od 1 TB.
- Inicjowanie kopii zapasowej

## <a name="causes-and-solutions"></a>Przyczyny i potencjalne rozwiązania

### <a name="the-vm-has-no-internet-access"></a>Maszyna wirtualna nie ma dostępu Internet
Na wymagania wdrożenia maszyny Wirtualnej nie ma dostępu Internetu lub ma ograniczenia w miejscu, uniemożliwiające dostęp do infrastruktury platformy Azure.

Do poprawnego działania zapasowy numer wewnętrzny wymaga łączności Azure publicznych adresów IP. Rozszerzenie wysyła polecenia do punktu końcowego usługi Azure Storage (adres URL protokołu HTTP) do zarządzania migawki maszyny wirtualnej. Jeśli rozszerzenie nie ma dostępu do publicznej sieci Internet, nie zostanie ostatecznie kopii zapasowej.

####  <a name="solution"></a>Rozwiązanie
Aby rozwiązać ten problem, wypróbuj jedną z metod wymienione w tym miejscu.
##### <a name="allow-access-to-the-azure-storage-corresponding-to-the-region"></a>Zezwalaj na dostęp do magazynu Azure odpowiadający regionu

Umożliwia połączenia z magazynem określonego regionu za pomocą [usługi tagi](../virtual-network/security-overview.md#service-tags). Upewnij się, że reguła, która umożliwia uzyskanie dostępu do konta magazynu ma wyższy priorytet niż regułę, która blokuje dostęp do Internetu. 

![Grupy NSG z tagami magazynu dla regionu](./media/backup-azure-arm-vms-prepare/storage-tags-with-nsg.png)

> [!WARNING]
> Tagi usługi magazynu są dostępne tylko w określonych regionach i są w wersji zapoznawczej. Aby uzyskać listę regionów, zobacz [usługi tagi dla magazynu](../virtual-network/security-overview.md#service-tags).

##### <a name="create-a-path-for-http-traffic-to-flow"></a>Tworzenie ścieżki dla przepływ ruchu HTTP

1. Jeśli masz ograniczeń sieci w miejscu (na przykład grupa zabezpieczeń sieci), wdrażania serwera proxy HTTP do kierowania ruchem.
2. Aby umożliwić dostęp do Internetu z serwera proxy HTTP, należy dodać reguły do grupy zabezpieczeń sieci, jeśli istnieje.

Aby dowiedzieć się, jak skonfigurować serwer proxy HTTP dla kopii zapasowych maszyn wirtualnych, zobacz [przygotowania środowiska do tworzenia kopii zapasowych maszyn wirtualnych platformy Azure](backup-azure-arm-vms-prepare.md#establish-network-connectivity).

W przypadku, gdy używane są zarządzane dysków, może być konieczne dodatkowe portu (8443) otwarcia na zapory.

### <a name="the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Agent zainstalowany na maszynie wirtualnej, ale odpowiadać (dla maszyn wirtualnych systemu Windows)

#### <a name="solution"></a>Rozwiązanie
Agent maszyny Wirtualnej może być uszkodzony lub może być zatrzymana usługa. Ponowne zainstalowanie agenta maszyny Wirtualnej może pomóc, Pobierz najnowszą wersję i uruchom ponownie komunikacji.

1. Sprawdź, czy Usługa agenta gościa z systemem Windows w usługach (services.msc) maszyna wirtualna jest uruchomiona. Spróbuj uruchomić ponownie usługę agenta gościa z systemem Windows i zainicjować tworzenie kopii zapasowej<br>
2. Jeśli nie jest widoczny w usługach, sprawdź w aplecie Programy i funkcje czy Usługa agenta gościa z systemem Windows jest zainstalowany.
4. Jeśli można wyświetlić w aplecie Programy i funkcje, odinstaluj agenta gościa z systemem Windows.
5. Pobierz i zainstaluj [najnowszej wersji pliku MSI agenta](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Do ukończenia procesu instalacji niezbędne są uprawnienia administratora.
6. Następnie powinien mieć możliwość wyświetlania usługi agenta gościa z systemem Windows w usługach
7. Spróbuj uruchomić na — żądanie/kopię zapasową adhoc, klikając przycisk "Utwórz kopię zapasową teraz" w portalu.

Sprawdź również, Twoja maszyna wirtualna ma  **[.NET 4.5 zainstalowane w systemie](https://docs.microsoft.com/dotnet/framework/migration-guide/how-to-determine-which-versions-are-installed)**. Jest to wymagane do komunikacji z usługą agenta maszyny Wirtualnej

### <a name="the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Agent zainstalowany na maszynie wirtualnej są nieaktualne (dla maszyn wirtualnych systemu Linux)

#### <a name="solution"></a>Rozwiązanie
Najbardziej związane z agenta lub rozszerzenie błędów dla maszyn wirtualnych systemu Linux są spowodowane przez problemy, które mają wpływ na nieaktualne agenta maszyny Wirtualnej. Aby rozwiązać ten problem, wykonaj następujące ogólne wytyczne:

1. Postępuj zgodnie z instrukcjami dotyczącymi [aktualizacja agenta maszyny Wirtualnej systemu Linux](../virtual-machines/linux/update-agent.md).

 >[!NOTE]
 >Firma Microsoft *zdecydowanie zaleca się* zaktualizowanie agenta tylko za pośrednictwem repozytorium dystrybucji. Nie zaleca się pobierania kodu agenta bezpośrednio z witryny GitHub i zaktualizowaniem go. Czy najnowsza wersja agenta jest niedostępna w przypadku dystrybucji, należy się z pomocą techniczną dystrybucji, aby uzyskać instrukcje dotyczące instalacji. Aby sprawdzić najnowsze agenta, przejdź do [agenta Windows Azure w systemie Linux](https://github.com/Azure/WALinuxAgent/releases) strony w repozytorium GitHub.

2. Upewnij się, że agent programu Azure działa na maszynie Wirtualnej, uruchamiając następujące polecenie:`ps -e`

 Jeśli proces nie jest uruchomiona, uruchom go ponownie za pomocą następujących poleceń:

 * Dla Ubuntu:`service walinuxagent start`
 * Inne dystrybucji:`service waagent start`

3. [Konfigurowanie automatycznego ponownego uruchomienia agenta](https://github.com/Azure/WALinuxAgent/wiki/Known-Issues#mitigate_agent_crash).
4. Uruchom nową kopię zapasową testu. Jeśli błąd będzie się powtarzać, z maszyny Wirtualnej klienta Zbierz następujące dzienniki:

   * /var/lib/waagent/*.xml
   * /var/log/waagent.log
   * /var/log/azure/*

Jeśli wymagane pełne rejestrowanie dla agenta waagent, wykonaj następujące kroki:

1. W pliku /etc/waagent.conf Znajdź następujący wiersz: **Włącz pełne rejestrowanie (y | n)**
2. Zmień **Logs.Verbose** wartość z  *n*  do *y*.
3. Zapisać zmiany, a następnie ponownie uruchom agenta waagent poprzedniego przedstawionych w tej sekcji.

### <a name="the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Nie można pobrać stanu migawki lub migawka nie można pobrać
Kopii zapasowej maszyny Wirtualnej zależy od wydawania polecenia migawki podstawowym konta magazynu. Kopia zapasowa może nie powieść, ponieważ go nie ma dostępu do konta magazynu lub wykonanie zadania migawki jest opóźnione.

#### <a name="solution"></a>Rozwiązanie
Poniższe warunki mogą spowodować niepowodzenie zadań migawki:

| Przyczyna | Rozwiązanie |
| --- | --- |
| Maszyna wirtualna ma skonfigurowano kopii zapasowej programu SQL Server. | Domyślnie kopii zapasowej maszyny Wirtualnej jest uruchamiane VSS pełnej kopii zapasowej na maszynach wirtualnych systemu Windows. Na maszynach wirtualnych, które działają na serwerach programu SQL Server i programem SQL Server kopia zapasowa została skonfigurowana, mogą występować opóźnienia z powodu wykonywania migawki.<br><br>W przypadku niepowodzenia tworzenia kopii zapasowej z powodu problemu z migawki, należy ustawić następujący klucz rejestru:<br><br>**[HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT] "USEVSSCOPYBACKUP"="TRUE"** |
| Stan maszyny Wirtualnej jest zgłaszana niepoprawnie, ponieważ maszyna wirtualna jest zamknięta w protokole RDP. | Jeśli wyłączysz maszyny Wirtualnej w protokołu RDP (Remote Desktop) sprawdź portalu, aby ustalić, czy stan maszyny Wirtualnej jest prawidłowa. Jeśli nie jest poprawny, należy wyłączyć maszynę Wirtualną w portalu przy użyciu **zamknięcia** opcji na pulpicie maszyny Wirtualnej. |
| Maszyna wirtualna nie można pobrać adresu hosta/sieci szkieletowej z serwera DHCP. | DHCP musi być włączona na gościu przeznaczonego na kopie zapasowe maszyn wirtualnych IaaS do pracy.  Jeśli maszyna wirtualna nie może pobrać adres hosta/sieci szkieletowej z odpowiedzi DHCP 245, go nie można pobrać lub uruchomić wszystkich rozszerzeń. Jeśli potrzebujesz statycznego prywatnego adresu IP, należy skonfigurować go za pośrednictwem platformy. Opcja DHCP w ramach maszyny Wirtualnej powinna być włączona w lewo. Aby uzyskać więcej informacji, zobacz [ustawienie wewnętrzny statycznego prywatnego adresu IP](../virtual-network/virtual-networks-reserved-private-ip.md). |

### <a name="the-backup-extension-fails-to-update-or-load"></a>Zapasowy numer wewnętrzny nie może zaktualizować lub załadować
Jeśli nie można załadować rozszerzeń, tworzenia kopii zapasowej nie powiedzie się, ponieważ nie można pobrać migawek.

#### <a name="solution"></a>Rozwiązanie

**Dla gości systemu Windows:** Sprawdź, czy usługa iaasvmprovider jest włączony i ma określony typ uruchamiania *automatyczne*. Jeśli usługa nie jest skonfigurowana w taki sposób, włącz go określić, czy następną kopią zapasową powiedzie się.

**Dla systemu Linux gości:** Sprawdź najnowszą wersję VMSnapshot dla systemu Linux (rozszerzenia używane przez kopię zapasową) jest 1.0.91.0.<br>


Jeśli zapasowy numer wewnętrzny nadal nie można zaktualizować lub załadować, możesz wymusić rozszerzenia VMSnapshot ponownego załadowania przez odinstalowywania rozszerzenia. Następnej próbie kopii zapasowej spowoduje ponowne załadowanie rozszerzenia.

Aby odinstalować rozszerzenia, wykonaj następujące czynności:

1. Przejdź do witryny [Azure Portal](https://portal.azure.com/).
2. Zlokalizuj maszynę Wirtualną, która ma problemy z kopii zapasowej.
3. Kliknij przycisk **ustawienia**.
4. Kliknij przycisk **rozszerzenia**.
5. Kliknij przycisk **Vmsnapshot rozszerzenia**.
6. Kliknij przycisk **odinstalować**.

Ta procedura powoduje, że rozszerzenie, należy zainstalować ponownie podczas następnej kopii zapasowej.

### <a name="backup-service-does-not-have-permission-to-delete-the-old-restore-points-due-to-resource-group-lock"></a>Usługa tworzenia kopii zapasowej nie ma uprawnienia do usuwania starych punktów przywracania z powodu blokady grupy zasobów
Ten problem dotyczy zarządzanych maszyn wirtualnych, których użytkownika blokuje grupy zasobów i usługi Kopia zapasowa nie jest w stanie usunąć z wcześniejszych punktów przywracania. Z tego powodu nowe kopie zapasowe zaczęło kończyć się niepowodzeniem, ponieważ istnieje limit maksymalnego 18 punktów przywracania nałożone z wewnętrznej bazy danych.

#### <a name="solution"></a>Rozwiązanie

Aby rozwiązać ten problem, użyj następujące kroki w celu usunięcia kolekcji punkt przywracania: <br>
 
1. Usuń zablokować grupy zasobów, w którym znajduje się maszyna wirtualna 
     
2. Instalowanie przy użyciu Chocolatey ARMClient <br>
   https://github.com/projectkudu/ARMClient
     
3. Zaloguj się do ARMClient <br>
             `.\armclient.exe login`
         
4. Punkt przywracania Get kolekcji odpowiadającej Maszynie wirtualnej <br>
    `.\armclient.exe get https://management.azure.com/subscriptions/<SubscriptionId>/resourceGroups/<ResourceGroupName>/providers/Microsoft.Compute/restorepointcollections/AzureBackup_<VM-Name>?api-version=2017-03-30`

    Przykład:`.\armclient.exe get https://management.azure.com/subscriptions/f2edfd5d-5496-4683-b94f-b3588c579006/resourceGroups/winvaultrg/providers/Microsoft.Compute/restorepointcollections/AzureBackup_winmanagedvm?api-version=2017-03-30`
             
5. Usuń kolekcję punktu przywracania <br>
            `.\armclient.exe delete https://management.azure.com/subscriptions/<SubscriptionId>/resourceGroups/<ResourceGroupName>/providers/Microsoft.Compute/restorepointcollections/AzureBackup_<VM-Name>?api-version=2017-03-30` 
 
6. Następnego zaplanowanego tworzenia kopii zapasowej automatycznie utworzy kolekcji punktu przywracania i nowe punkty przywracania 
 
7. Problem zostanie wyświetlony ponownie w przypadku zablokowania grupy zasobów ponownie jako jest ograniczona tylko do 18 punktów przywracania, po których kopie zapasowe kończyć się niepowodzeniem 

