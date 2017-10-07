---
title: "aaaTroubleshoot Azure backup błędów w klasycznym portalu | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z usługi Kopia zapasowa Azure i przywracanie maszyn wirtualnych platformy Azure w portalu klasycznym hello."
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 117201fb-c0cd-4be4-b47f-abd88fe914cf
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: trinadhk;markgal;
ms.openlocfilehash: b9907f6fa57c631f5446c4d00f946a57c4efd72b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-virtual-machine-backup"></a>Rozwiązywanie problemów z kopiami zapasowymi maszyn wirtualnych platformy Azure
> [!div class="op_single_selector"]
> * [Magazyn usług odzyskiwania](backup-azure-vms-troubleshoot.md)
> * [Magazyn kopii zapasowych](backup-azure-vms-troubleshoot-classic.md)
>
>

Można rozwiązać błędów napotkanych podczas przy użyciu usługi Kopia zapasowa Azure z informacjami o wymienione w poniższej tabeli hello.

## <a name="discovery"></a>Odnajdywania
| Operacja tworzenia kopii zapasowej | Szczegóły błędu | Obejście problemu |
| --- | --- | --- |
| Odnajdywania |Nie powiodło się nowych elementów toodiscover -, a kopia zapasowa Microsoft Azure napotkał błąd wewnętrzny. Poczekaj kilka minut, a następnie spróbuj ponowić operację hello. |Ponów próbę wykonania procesu odnajdywania powitania po 15 minutach. |
| Odnajdywania |Nie można toodiscover nowych elementów — kolejna operacja odnajdywania wykonana operacja jest już w toku. Poczekaj, aż do zakończenia hello bieżącej operacji odnajdywania. |Brak |

## <a name="register"></a>Zarejestruj subskrypcję
| Operacja tworzenia kopii zapasowej | Szczegóły błędu | Obejście problemu |
| --- | --- | --- |
| Zarejestruj subskrypcję |Liczba dysków danych dołączonych toohello maszyny wirtualnej przekracza hello obsługiwany limit — należy odłączyć niektóre dyski danych w ramach tej operacji hello maszyny wirtualnej i spróbuj ponownie. Azure obsługuje kopii zapasowych zapasowe dysków danych too16 dołączony tooan maszyny wirtualnej platformy Azure do utworzenia kopii zapasowej |Brak |
| Zarejestruj subskrypcję |Kopia zapasowa Microsoft Azure napotkał błąd wewnętrzny - Poczekaj kilka minut, a następnie spróbuj ponowić operację hello. Jeśli hello problem będzie się powtarzać, skontaktuj się z Microsoft Support. |Ten błąd powodu tooone z hello następujące, nieobsługiwane konfiguracji maszyny wirtualnej można uzyskać na LRS warstwie Premium. <br> Magazyn w warstwie Premium maszyn wirtualnych utworzeniem kopii zapasowej za pomocą magazynu usług odzyskiwania. [Więcej informacji](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup) |
| Zarejestruj subskrypcję |Rejestracja nie powiodła się limit czasu operacji instalacji agenta |Sprawdź, czy wersja systemu operacyjnego hello maszyny wirtualnej hello jest obsługiwana. |
| Zarejestruj subskrypcję |Wykonanie polecenia nie powiodło się — inna operacja jest w toku dla tego elementu. Zaczekaj na ukończenie hello poprzedniej operacji |Brak |
| Zarejestruj subskrypcję |Maszyny wirtualne o wirtualnych dyskach twardych przechowywanych na magazyn w warstwie Premium nie są obsługiwane dla kopii zapasowej |Brak |
| Zarejestruj subskrypcję |Agent maszyny wirtualnej nie jest obecna na maszynie wirtualnej hello — Zainstaluj hello wymagane wstępnie wymaganego składnika, agent maszyny Wirtualnej i hello operacji ponownego uruchamiania. |[Dowiedz się więcej](#vm-agent) informacji o instalacji agenta maszyny Wirtualnej, i jak toovalidate hello instalacji agenta maszyny Wirtualnej. |

## <a name="backup"></a>Tworzenie kopii zapasowych
| Operacja tworzenia kopii zapasowej | Szczegóły błędu | Obejście problemu |
| --- | --- | --- |
| Tworzenie kopii zapasowych |Nie można skomunikować się z hello agenta maszyny Wirtualnej do stanu migawki. Upłynął limit czasu zadania sub wirtualna migawki. — Można znaleźć pod adresem hello Rozwiązywanie problemów z wskazówki na temat tooresolve to. |Ten błąd jest zgłaszany, jeśli występuje problem z hello agenta maszyny Wirtualnej lub toohello dostępu do sieci infrastruktury platformy Azure jest zablokowana w określony sposób. Dowiedz się więcej o [debugowania zapasowej maszyny Wirtualnej migawki problemów](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md). <br> Jeśli hello agenta maszyny Wirtualnej nie powoduje żadnych problemów, a następnie uruchom ponownie hello maszyny Wirtualnej. W czasie niepoprawny stan maszyny Wirtualnej mogą powodować problemy i ponownego uruchamiania maszyny Wirtualnej hello resetuje to "nieprawidłowego stanu" |
| Tworzenie kopii zapasowych |Kopii zapasowej nie powiodło się z powodu wewnętrznego błędu — spróbuj hello operację ponownie za kilka minut. Jeśli hello problem będzie się powtarzać, skontaktuj się z pomocą techniczną firmy Microsoft Support |Sprawdź, czy jest to problem przejściowy podczas uzyskiwania dostępu do magazynu maszyny Wirtualnej. Sprawdź, czy [stan Azure](https://azure.microsoft.com/en-us/status/) toosee, jeśli wszystkie bieżące wystawiać pokrewne toocompute / / sieć magazynu w regionie hello. Sprawdź skuteczność została osłabiona problem kopii zapasowej post hello ponów próbę. |
| Tworzenie kopii zapasowych |Nie można wykonać operacji hello, ponieważ maszyna wirtualna już nie istnieje. |Nie można wykonać kopii zapasowej, ponieważ hello skonfigurowane dla kopii zapasowej maszyny Wirtualnej został usunięty. Zatrzymaj przechodzi do widoku elementy tooProtected dodatkowe kopie zapasowe, wybierz chronionego elementu i wybierz polecenie Zatrzymaj ochronę. Wybierając opcję danych zachować kopii zapasowej, można zachować danych. Później można wznowić ochronę dla tej maszyny wirtualnej, klikając na konfigurowanie ochrony z widoku zarejestrowane elementy |
| Tworzenie kopii zapasowych |Nie powiodło się tooinstall hello rozszerzenia usług odzyskiwania Azure na powitania wybrany element — Agent maszyny Wirtualnej jest jako warunek wstępny dla rozszerzenia usług odzyskiwania Azure. Zainstaluj agenta maszyny Wirtualnej Azure hello i hello rejestracji operacji ponownego uruchamiania |<ol> <li>Sprawdź, czy agent maszyny Wirtualnej hello został poprawnie zainstalowany. <li>Upewnij się, że hello flagi na powitania konfiguracji maszyny Wirtualnej została poprawnie ustawiona.</ol> [Dowiedz się więcej](#validating-vm-agent-installation) informacji o instalacji agenta maszyny Wirtualnej, i jak toovalidate hello instalacji agenta maszyny Wirtualnej. |
| Tworzenie kopii zapasowych |Wykonanie polecenia nie powiodło się — inna operacja jest obecnie w toku dla tego elementu. Zaczekaj na ukończenie hello poprzedniej operacji, a następnie spróbuj ponownie |Istniejące zadanie tworzenia kopii zapasowej lub przywracania hello maszyna wirtualna jest uruchomiona, i nie można uruchomić nowe zadanie, istniejące zadanie hello jest uruchomiona. |
| Tworzenie kopii zapasowych |Instalacja rozszerzenia nie powiodło się z powodu błędu hello "COM + nie toohello tootalk Microsoft Distributed Transaction Coordinator |Zwykle oznacza to, że hello usług COM + nie jest uruchomiony. Aby uzyskać pomoc dotyczącą rozwiązywania tego problemu, skontaktuj się z pomocą techniczną firmy Microsoft. |
| Tworzenie kopii zapasowych |Migawki nie można wykonać operacji hello błąd operacji VSS "ten dysk jest zablokowany przez szyfrowanie dysków funkcją BitLocker. Należy odblokować ten dysk z Panelu sterowania. |Wyłącz funkcję BitLocker na wszystkich dyskach na powitania maszyny Wirtualnej i sprawdź, czy hello VSS problem został rozwiązany |
| Tworzenie kopii zapasowych |Maszyny wirtualne o wirtualnych dyskach twardych przechowywanych na magazyn w warstwie Premium nie są obsługiwane dla kopii zapasowej |Brak |
| Tworzenie kopii zapasowych |Nie można odnaleźć maszyny wirtualnej platformy Azure. |Dzieje się tak, gdy hello podstawowej maszyny Wirtualnej jest usuwane, ale zasady tworzenia kopii zapasowej hello nadal toolook dla kopii zapasowej tooperform maszyny Wirtualnej. toofix ten błąd: <ol><li>Utwórz ponownie maszynę wirtualną hello z hello samą nazwą i tej samej nazwy grupy zasobów [nazwa usługi w chmurze], <br>(LUB) <li> Wyłącz ochronę dla tej maszyny Wirtualnej tak, aby kolejnych kopii zapasowych nie zostanie uzyskać wywołane. </ol> |
| Tworzenie kopii zapasowych |Agent maszyny wirtualnej nie jest obecna na maszynie wirtualnej hello — Zainstaluj hello wymagane wstępnie wymaganego składnika, agent maszyny Wirtualnej i hello operacji ponownego uruchamiania. |[Dowiedz się więcej](#vm-agent) informacji o instalacji agenta maszyny Wirtualnej, i jak toovalidate hello instalacji agenta maszyny Wirtualnej. |

## <a name="jobs"></a>Zadania
| Operacja | Szczegóły błędu | Obejście problemu |
| --- | --- | --- |
| Anulowanie zadania |Anulowanie nie jest obsługiwana dla tego typu zadania — poczekaj, aż hello zadanie zostało ukończone. |Brak |
| Anulowanie zadania |zadanie Hello nie jest w stanie można anulować — poczekaj, aż hello zadanie zostało ukończone. <br>LUB<br> Witaj wybrane zadanie nie jest w stanie można anulować — poczekaj hello toocomplete zadania. |Najprawdopodobniej zadanie hello jest prawie zakończone; Poczekaj, aż hello zadanie zostało ukończone |
| Anulowanie zadania |Nie można anulować zadania hello, ponieważ nie jest w toku — anulowania jest obsługiwana tylko dla zadania, które są w toku. Anuluj próba w toku zadania. |Dzieje się ze względu na stan przejściowy tooa. Poczekaj chwilę i ponów próbę wykonania operacji anulowania hello |
| Anulowanie zadania |Witaj toocancel zakończone niepowodzeniem zadanie — Zaczekaj na zakończenie zadania. |Brak |

## <a name="restore"></a>Przywracanie
| Operacja | Szczegóły błędu | Obejście problemu |
| --- | --- | --- |
| Przywracanie |Przywracanie nie powiodło się z powodu błędu wewnętrznego w chmurze |<ol><li>Próbujesz toorestore toowhich usługi chmury jest skonfigurowany przy użyciu ustawień DNS. Możesz sprawdzić <br>$deployment = get-AzureDeployment - ServiceName "ServiceName"-miejsca "Production" Get-AzureDns - DnsSettings $deployment. DnsSettings<br>W przypadku skonfigurowany adres, oznacza to, czy ustawienia DNS są skonfigurowane.<br> <li>Próbujesz tooyou toowhich usługi w chmurze toorestore jest skonfigurowany z zastrzeżonego adresu IP i istniejących maszyn wirtualnych w usłudze w chmurze są w stanie zatrzymania.<br>Można sprawdzić, czy usługa w chmurze ma zastrzeżony adres IP za pomocą następujących poleceń cmdlet programu powershell:<br>$deployment = get-AzureDeployment - ServiceName "servicename"-gniazdo $ "Production" w programie dep. Nazwa zastrzeżonego adresu IP <br><li>Próbujesz toorestore maszynę wirtualną o następujące konfiguracje sieciowe specjalne toosame w usłudze w chmurze. <br>— Maszyny wirtualne w konfiguracji usługi równoważenia obciążenia (wewnętrznych i zewnętrznych)<br>— Maszyny wirtualne z wielu zastrzeżonych adresów IP<br>— Maszyny wirtualne z wieloma kartami sieciowymi<br>Wybierz nową usługę w chmurze hello interfejsu użytkownika lub zapoznaj zbyt[zagadnienia dotyczące przywracania](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations) dla maszyn wirtualnych z konfiguracjami sieci specjalne</ol> |
| Przywracanie |Witaj wybrana nazwa DNS jest już zajęta — Określ inną nazwę DNS i spróbuj ponownie. |Witaj tutaj nazwę DNS odwołuje się nazwa usługi w chmurze toohello (zazwyczaj kończąc. cloudapp.net). Musi on toobe unikatowy. Jeśli wystąpi ten błąd, należy toochoose inną nazwę maszyny Wirtualnej podczas przywracania. <br><br> Ten błąd jest wyświetlany tylko toousers hello portalu Azure. Witaj operacji przywracania za pomocą programu PowerShell zakończy się pomyślnie, ponieważ tylko przywraca hello dysków i nie tworzy hello maszyny Wirtualnej. Błąd Hello zostanie skierowany, gdy hello maszyny Wirtualnej jest jawnie utworzone przez użytkownika, po zakończeniu operacji przywracania dysku hello. |
| Przywracanie |Witaj konfiguracji określonej sieci wirtualnej jest niepoprawna — Określ konfiguracji innej sieci wirtualnej i spróbuj ponownie. |Brak |
| Przywracanie |Witaj określony używa zastrzeżonego adresu IP, który nie pasuje do hello konfiguracji maszyny wirtualnej hello przywracana — Podaj usługi inną chmurę, która nie używa zastrzeżonego adresu IP lub wybierz inny toorestore punkt odzyskiwania z usługi w chmurze. |Brak |
| Przywracanie |Usługi w chmurze osiągnął limit liczby wejściowych punktów końcowych — operacja hello ponawiania przez określenie innej usługi w chmurze lub przy użyciu istniejącego punktu końcowego. |Brak |
| Przywracanie |Konto magazynu kopii zapasowej magazynu i obiekt docelowy znajdują się w dwóch różnych regionach — upewnij się, że konto magazynu hello podczas operacji przywracania jest w hello tego samego regionu Azure hello magazynu kopii zapasowych. |Brak |
| Przywracanie |Konta magazynu określony dla operacji przywracania hello jest obsługiwana — konta magazynu tylko Basic/Standard z lokalnie nadmiarowego lub z magazynu geograficznie nadmiarowego replikacji ustawienia są obsługiwane. Wybierz konto magazynu obsługiwane |Brak |
| Przywracanie |Typ konta magazynu określony dla operacji przywracania nie jest w trybie online — upewnij się, że hello konta magazynu określony w operacji przywracania jest w trybie online |Taka sytuacja może wystąpić z powodu błędu przejściowego w usłudze Azure Storage lub z powodu awarii tooan. Wybierz inne konto magazynu. |
| Przywracanie |Osiągnięto limit przydziału Grupa zasobów — Usuń niektóre grupy zasobów z portalu Azure lub skontaktuj się z pomocą techniczną platformy Azure tooincrease hello limitów. |Brak |
| Przywracanie |Wybrana podsieć nie istnieje — Wybierz podsieć, która istnieje |Brak |

## <a name="policy"></a>Zasady
| Operacja | Szczegóły błędu | Obejście problemu |
| --- | --- | --- |
| Tworzenie zasad |Nie powiodło się zasad hello toocreate - Zmniejsz toocontinue opcji przechowywania hello z konfiguracją zasad. |Brak |

## <a name="vm-agent"></a>Agent maszyny Wirtualnej
### <a name="setting-up-hello-vm-agent"></a>Konfigurowanie hello agenta maszyny Wirtualnej
Zazwyczaj hello agenta maszyny Wirtualnej jest już obecny na maszynach wirtualnych, które są tworzone na podstawie hello galerii Azure. Jednak maszyn wirtualnych, które są migrowane z lokalnymi centrami danych, nie będzie zawierało hello zainstalowanego agenta maszyny Wirtualnej. Dla tych maszyn wirtualnych hello agenta maszyny Wirtualnej musi toobe jawnie zainstalowany. Przeczytaj więcej na temat [instalowanie hello agenta maszyny Wirtualnej na istniejącej maszyny Wirtualnej](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx).

Dla maszyn wirtualnych systemu Windows:

* Pobierz i zainstaluj hello [pliku MSI agenta](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Konieczne będzie instalacji hello toocomplete uprawnienia administratora.
* [Aktualizuj właściwości maszyny Wirtualnej hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate, który hello agent jest zainstalowany.

Dla maszyn wirtualnych systemu Linux:

* Zainstaluj najnowsze [agenta systemu Linux](https://github.com/Azure/WALinuxAgent) z usługi github.
* [Aktualizuj właściwości maszyny Wirtualnej hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate, który hello agent jest zainstalowany.

### <a name="updating-hello-vm-agent"></a>Aktualizowanie hello agenta maszyny Wirtualnej
Dla maszyn wirtualnych systemu Windows:

* Aktualizowanie hello agenta maszyny Wirtualnej jest tak proste, jak ponowne zainstalowanie hello [plików binarnych agenta maszyny Wirtualnej](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Należy jednak tooensure uruchomioną podczas powitalne agenta maszyny Wirtualnej jest aktualizowana żadna operacja tworzenia kopii zapasowej.

Dla maszyn wirtualnych systemu Linux:

* Wykonaj instrukcje hello [aktualizacja agenta maszyny Wirtualnej systemu Linux](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="validating-vm-agent-installation"></a>Sprawdzanie poprawności instalacji agenta maszyny Wirtualnej
Jak toocheck dla hello wersji agenta maszyny Wirtualnej na maszynach wirtualnych systemu Windows:

1. Zaloguj się na toohello maszyny wirtualnej platformy Azure i przejdź do folderu toohello *C:\WindowsAzure\Packages*. Powinien znajdować się plik WaAppAgent.exe hello jest obecny.
2. Kliknij prawym przyciskiem myszy plik hello znajduje się zbyt**właściwości**, a następnie wybierz hello **szczegóły** kartę hello wersji produktu pole powinno być 2.6.1198.718 lub nowszej
