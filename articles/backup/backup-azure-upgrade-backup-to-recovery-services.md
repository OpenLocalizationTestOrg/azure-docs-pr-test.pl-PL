---
title: "aaaUpgrade magazynu usług odzyskiwania tooa magazynu kopii zapasowych (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
description: "Instrukcje i tooupgrade informacje pomocy technicznej kopia zapasowa Azure magazynu tooa, które Magazyn usług odzyskiwania."
services: backup
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
ms.assetid: 228fef19-2f6b-4067-acc3-fb6e501afb88
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/03/2017
ms.author: sogup;markgal;arunak
ms.openlocfilehash: 49062ca4556a009c82f143bb3a60ec71748bed01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-backup-vault-tooa-recovery-services-vault"></a>Uaktualnij magazynu usług odzyskiwania tooa magazynu kopii zapasowej

W tym artykule opisano, jak tooupgrade magazynu kopii zapasowych tooa magazyn usług odzyskiwania. proces uaktualniania Hello bez wpływu na wszystkie zadania uruchomione w kopii zapasowej, a nie zostały utracone nie dane kopii zapasowej. Hello głównej przyczyny tooupgrade tooa magazynu kopii zapasowej, które Magazyn usług odzyskiwania:
- Wszystkie funkcje magazynu kopii zapasowych są przechowywane w magazynie usług odzyskiwania.
- Magazyny usług odzyskiwania mają więcej funkcji niż magazyny kopii zapasowych, w tym: ze względów bezpieczeństwa zintegrowane monitorowanie, szybciej przeprowadzać operacje przywracania i na poziomie pozycji.
- Zarządzanie elementów kopii zapasowych z ulepszonych, uproszczone portalu.
- Nowe funkcje mają zastosowanie tylko tooRecovery Magazyny usług.

## <a name="impact-toooperations-during-upgrade"></a>Wpływ toooperations podczas uaktualniania

W przypadku uaktualniania magazynu usług odzyskiwania tooa magazynu kopii zapasowej, nie ma żadnego wpływu tooyour danych płaszczyzny operacji. Wszystkie zadania tworzenia kopii zapasowych nadal normalnie, a wszystkie zadania przywracania active nadal bez przeszkód. Podczas uaktualniania hello operacji zarządzania pociągnąć za sobą krótki czas przestoju i nie można chronić nowych elementów lub utworzyć zadania tworzenia kopii zapasowych ad hoc. Zadania przywracania dla maszyn wirtualnych IaaS nie działają podczas uaktualniania hello. Witaj magazynu uaktualnienia może zająć w obszarze toocomplete godzinę. Po skończeniu magazynu usług odzyskiwania zastępuje hello magazyn kopii zapasowych.

## <a name="changes-tooyour-automation-and-tool-after-upgrading"></a>Narzędzie po uaktualnieniu i zmiany tooyour automatyzacji

Podczas przygotowywanie infrastruktury hello magazynu uaktualnienia, należy zaktualizować Twojego istniejącej automatyzacji lub narzędzi tooensure jego odtwarzanie jest kontynuowane toowork hello uaktualnienia.
Poszukaj odwołania do poleceń cmdlet programu PowerShell hello hello [modelu wdrażania programu Service Manager](backup-client-automation-classic.md) i hello [modelu wdrażania usługi Resource Manager](backup-client-automation.md).


## <a name="before-you-upgrade"></a>Przed uaktualnieniem

Sprawdź, czy hello następujące kwestie przed uaktualnieniem programu magazyny kopii zapasowych magazynów usługi tooRecovery.

- **Wersja agenta minimalna**: tooupgrade Twojego magazynu, upewnij się, że agent usług odzyskiwania Azure firmy Microsoft (MARS) hello jest co najmniej wersji 2.0.9070.0. Jeśli agenta MARS hello jest starsza niż 2.0.9070.0, należy zaktualizować agenta hello przed rozpoczęciem procesu uaktualniania hello.
- **Metoda oparta na modelu rozliczeń**: Magazyny usług odzyskiwania obsługują tylko hello metoda oparta na modelu rozliczeń. Jeśli masz magazyn kopii zapasowych używanym hello starsze oparty na magazynie modelu rozliczeń, należy przekonwertować modelu rozliczeń hello podczas uaktualniania.
- **Żadne operacje konfiguracji kopii zapasowej w toku**: podczas uaktualniania, płaszczyzny zarządzania toohello dostęp jest ograniczony. Wykonanie wszystkich akcji płaszczyzny zarządzania, a następnie uruchom uaktualnianie hello.

## <a name="using-powershell-scripts-tooupgrade-your-vaults"></a>Przy użyciu tooupgrade skrypty programu PowerShell z magazynów

Można użyć tooupgrade skryptów PowerShell Magazyny usług tooRecovery magazyny kopii zapasowych. Sprawdź, czy ma hello wymagane PowerShell składniki tootrigger hello magazynu uaktualnienia. Skrypty programu PowerShell dla magazyny kopii zapasowych nie działają w przypadku magazynów usług odzyskiwania. Przygotowanie środowiska tooupgrade hello magazynów:

1. Zainstaluj lub Uaktualnij [tooversion Windows Management Framework (WMF) 5](https://www.microsoft.com/download/details.aspx?id=50395) lub nowszej.
2. [Zainstaluj Azure PowerShell MSI](https://github.com/Azure/azure-powershell/releases/download/v3.8.0-April2017/azure-powershell.3.8.0.msi).
3. Pobierz hello [skrypt programu PowerShell](https://aka.ms/vaultupgradescript2) tooupgrade Twojego magazynów.

### <a name="run-hello-powershell-script"></a>Uruchom skrypt programu PowerShell hello

Użyj następującego skryptu tooupgrade hello z magazynów. Witaj następującego przykładowego skryptu ma wyjaśnienia hello parametrów.

RecoveryServicesVaultUpgrade 1.0.2.ps1 **- SubscriptionID** `<subscriptionID>` **- VaultName** `<vaultname>` **-lokalizacji** `<location>` **- ResourceType** `BackupVault` **- TargetResourceGroupName**`<rgname>`

**Identyfikator subskrypcji** — Witaj identyfikator subskrypcji hello magazynu, który jest uaktualniany.<br/>
**VaultName** — Witaj nazwę magazynu kopii zapasowych hello, który jest uaktualniany.<br/>
**Lokalizacja** — lokalizacja magazynu hello uaktualniany.<br/>
**Typ zasobu** -Użyj BackupVault.<br/>
**TargetResourceGroupName** — ponieważ w przypadku uaktualniania hello magazynu tooa Resource Manager wdrożenie oparte na, określ grupę zasobów. Można użyć istniejącej grupy zasobów lub utwórz go, podając nową nazwę. Jeśli wpiszesz nazwę hello grupy zasobów może utworzyć nową grupę zasobów. Przeczytaj toolearn więcej informacji na temat grup zasobów, [informacje na temat grup zasobów](../azure-resource-manager/resource-group-overview.md#resource-groups).

>[!NOTE]
> Nazwy grup zasobów ma ograniczenia. Należy się, że wskazówki hello toofollow; toodo awarii może to spowodować toofail uaktualnienia magazynu.
>
>

Witaj poniższy fragment kodu jest przykładem z polecenia programu PowerShell powinien wyglądać następująco:

```
RecoveryServicesVaultUpgrade.ps1 -SubscriptionID 53a3c692-5283-4f0a-baf6-49412f5ebefe -VaultName "TestVault" -Location "Australia East" -ResourceType BackupVault -TargetResourceGroupName "ContosoRG"
```

Można również uruchomić skrypt hello bez żadnych parametrów i prośba tooprovide dane wejściowe dla wszystkich wymaganych parametrów.

Hello skrypt programu PowerShell wyświetli monit możesz tooenter swoje poświadczenia. Wprowadź swoje poświadczenia dwa razy: raz dla konta programu Service Manager hello i po raz drugi dla hello konta Menedżera zasobów.

### <a name="pre-requisites-checking"></a>Wstępne sprawdzanie
Po wprowadzeniu poświadczeń platformy Azure, Azure sprawdza, czy dane środowisko spełnia następujące wymagania wstępne hello:

- **Wersja agenta minimalna** -Magazyny usług tooRecovery magazynów uaktualniania kopii zapasowej toobe agenta MARS hello wymaga co najmniej wersji 2.0.9070. Jeśli masz elementy zarejestrowany magazyn kopii zapasowych tooa agenta starszych niż 2.0.9070, hello Sprawdzanie wymagań wstępnych kończy się niepowodzeniem. W przypadku niepowodzenia sprawdzania wymagań wstępnych hello zaktualizować agenta hello i ponownie spróbuj tooupgrade hello magazynu. Możesz pobrać najnowszą wersję agenta hello z hello [http://download.microsoft.com/download/F/4/B/F4B06356-150F-4DB0-8AD8-95B4DB4BBF7C/MARSAgentInstaller.exe](http://download.microsoft.com/download/F/4/B/F4B06356-150F-4DB0-8AD8-95B4DB4BBF7C/MARSAgentInstaller.exe).
- **Zadania konfiguracji i nieustanne**: Jeśli ktoś konfiguruje zadania dla magazynu kopii zapasowych należy ustawić toobe uaktualniony lub zarejestrować element, hello Sprawdzanie wymagań wstępnych kończy się niepowodzeniem. Zakończ konfigurację hello lub zakończenie rejestracji hello elementu, a następnie uruchom proces uaktualniania hello magazynu.
- **Oparty na magazynie modelu rozliczeń**: usług odzyskiwania magazynów obsługi hello metoda oparta na modelu rozliczeń. Po uruchomieniu hello uaktualnienia magazynu na magazyn kopii zapasowych czy używa hello oparty na magazynie modelu rozliczeń, są tooupgrade zostanie wyświetlony monit o modelu rozliczeń oraz hello magazynu. W przeciwnym razie można zaktualizować modelu rozliczeń najpierw, a następnie uruchom Uaktualnianie magazynu hello.
- Określ grupę zasobów dla magazyn usług odzyskiwania hello. Zaletą tootake hello funkcji wdrażania usługi Resource Manager, Magazyn usług odzyskiwania należy umieścić w grupie zasobów. Jeśli nie wiadomo, które toouse grupy zasobów, podaj nazwę i hello procesu uaktualniania utworzy hello grupy zasobów. proces uaktualniania Hello powoduje również skojarzenie hello magazynu z hello nową grupę zasobów.

Po zakończeniu procesu uaktualniania hello sprawdzanie wstępne hello procesu hello monituje możesz toostart hello magazynu uaktualnienia. Po upewnieniu się, procesu uaktualniania hello zwykle trwa około toocomplete 15-20 minut, w zależności od rozmiaru hello magazynu. Jeśli masz dużą magazynu, uaktualnienie może potrwać too90 minut.

## <a name="managing-your-recovery-services-vaults"></a>Zarządzanie z Magazyny usług odzyskiwania

następujące ekranów powitalnych Pokaż nowy magazyn usług odzyskiwania uaktualnione z magazynu kopii zapasowych w hello portalu Azure. pierwszym ekranie powitania pokazuje hello pulpit nawigacyjny magazynu, który wyświetla kluczy jednostek hello magazynu.

![przykład uaktualnienia z magazynu kopii zapasowych magazynu usług odzyskiwania](./media/backup-azure-upgrade-backup-to-recovery-services/upgraded-rs-vault-in-dashboard.png)

drugim ekranie powitania zawiera łącza pomocy hello dostępne toohelp możesz rozpocząć korzystanie z usług odzyskiwania hello magazynu.

![łącza w bloku Szybki Start hello pomocy](./media/backup-azure-upgrade-backup-to-recovery-services/quick-start-w-help-links.png)

## <a name="post-upgrade-steps"></a>Czynności po uaktualnieniu
Magazyn usług odzyskiwania obsługują określania informacji o strefie czasowej zasad tworzenia kopii zapasowej. Po pomyślnym uaktualnieniu magazynu Przejdź tooBackup zasady z menu ustawień magazynu i zaktualizuj hello informacji o strefie czasowej dla każdej zasady hello skonfigurowane w magazynie hello. Ten ekran pokazuje już hello harmonogram tworzenia kopii zapasowych czas określony na lokalnej strefie czasowej używane podczas tworzenia zasad. 

## <a name="enhanced-security"></a>Większe bezpieczeństwo

Po uaktualnieniu magazynu kopii zapasowych magazyn usług odzyskiwania tooa, hello ustawienia zabezpieczeń dla tego magazynu są automatycznie włączone. Gdy hello ustawienia zabezpieczeń znajdują się na niektórych operacji, takich jak usuwanie kopii zapasowych lub zmiana hasła wymagają [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) numeru PIN. Aby uzyskać więcej informacji na powitania zwiększonych zabezpieczeń, zobacz artykuł hello [funkcje zabezpieczeń, kopie zapasowe hybrydowego tooprotect](backup-azure-security-feature.md). 

Gdy hello zwiększonych zabezpieczeń jest włączona, dane są przechowywane w górę too14 dni po informacje o punkcie odzyskiwania hello został usunięty z magazynu hello. Klienci są rozliczane do przechowywania tych danych zabezpieczeń. Przechowywanie danych zabezpieczeń stosuje punktów toorecovery hello Azure Backup agent, serwer usługi Kopia zapasowa Azure i System Center Data Protection Manager. 

## <a name="gather-data-on-your-vault"></a>Zbieranie danych dotyczących magazynu

Po uaktualnieniu magazynu usług odzyskiwania tooa konfigurowania raportów dla usługi Kopia zapasowa Azure (w przypadku maszyn wirtualnych IaaS i usług odzyskiwania Azure firmy Microsoft (MARS)), a następnie użyć raportów hello tooaccess usługi Power BI. Aby uzyskać dodatkowe informacje dotyczące zbierania danych, zobacz artykuł hello [raporty skonfigurować kopia zapasowa Azure](backup-azure-configure-reports.md).

## <a name="frequently-asked-questions"></a>Często zadawane pytania

**Plan uaktualniania hello wpływa na Moje bieżące kopie zapasowe?**</br>
Nie. Kopie zapasowe trwającą nadal przerwana podczas i po uaktualnieniu.

**Jeśli nie I planowane jest uaktualnienie wkrótce, co się stanie toomy magazynów?**</br>
Ponieważ wszystkie nowe funkcje tylko tooRecovery Magazyny usług Niniejsza możesz tooupgrade Twojego magazynów. Microsoft ostatecznie wycofuje hello klasycznego portalu. Uruchamianie 1 września 2017 Microsoft rozpocznie się automatycznie — uaktualnienie Magazyny usług tooRecovery magazynami kopii zapasowych. Przez 1 listopada 2017 Microsoft ukończy hello procesu uaktualniania. Magazyn może zostać automatycznie uaktualniony czasie września lub października. Firma Microsoft zaleca się, że jak najszybciej Uaktualnij magazynu.

**Jaki jest średnia ta uaktualnienia do mojej istniejącej oprzyrządowania?**</br>
Aktualizacja modelu wdrażania usługi Resource Manager toohello narzędzi. Usługi odzyskiwania, który magazynów zostały utworzone dla używać w modelu wdrażania usługi Resource Manager hello. Planowanie modelu wdrażania usługi Resource Manager hello i ewidencjonowanie aktywności hello różnicę w Twojej magazynów jest ważne. 

**Podczas uaktualniania hello jest znacznie Przestój?**</br>
To zależy od hello liczby zasobów, które jest uaktualniany. Przy mniejszych wdrożeniach (dziesiątki kilka wystąpień chronionym) uaktualnienie całego hello powinny zająć mniej niż 20 minut. W przypadku większych wdrożeń powinien upłynąć maksymalnie godziny.

**I przywrócić po uaktualnieniu?**</br>
Nie. Wycofanie nie jest obsługiwana po hello zasoby zostały pomyślnie uaktualnione.

**Moje toosee zasobów lub subskrypcji można sprawdzić, gdy są one możliwość uaktualnienia?**</br>
Tak. Hello pierwszym krokiem podczas uaktualnienia sprawdza, czy zasoby hello mogą uaktualnienia. W razie niepowodzenia weryfikacji hello wymagań wstępnych, komunikaty dla wszystkich przyczyny hello nie można ukończyć powitalnych uaktualnienia.

**Jakie uprawnienia powinny mieć tootrigger uaktualnienia magazynu?**</br>
Witaj tooperform magazynu uaktualnienia, musi zostać dodany jako współadministrator subskrypcji hello w hello klasycznego portalu Azure. Jest to wymagane, nawet jeśli już zostały przedstawione jako właściciela w hello portalu Azure. Spróbuj tooadd współadministratorem subskrypcji hello w Azure klasycznego portalu toofind wychodzących, jeśli jesteś współadministratorem subskrypcji hello. Jeśli nie jest możliwe tooadd współadministratorem, skontaktuj się z administratorem usługi ani współadministratorem subskrypcji hello, który można dodać jako współadministrator.

**Można uaktualnić mój opartych na dostawcy usług Kryptograficznych magazynu kopii zapasowej?**</br>
Nie. Obecnie nie można uaktualnić magazynów kopii zapasowych opartych na dostawcy usług Kryptograficznych. Firma Microsoft zostanie dodana obsługa uaktualniania opartych na dostawcy usług Kryptograficznych magazyny kopii zapasowych w wersjach dalej hello.

**Może wyświetlać Mój po uaktualnieniu magazynu classic?**</br>
Nie. Nie można wyświetlić lub zarządzaj nimi po uaktualnieniu magazynu klasycznego. Można tylko hello stanie toouse nowego portalu Azure do wszystkich akcji zarządzania na powitania magazynu.

**Moje uaktualnienie nie powiodło się, ale maszyna hello przechowywać hello agenta wymagające aktualizacji, już nie istnieje. Co zrobić w takim przypadku?**</br>
Toouse hello magazynu, należy hello kopii zapasowych dla tej maszyny w celu przechowywania długoterminowego, nie będzie możliwe tooupgrade hello magazynu. W przyszłych wersjach dodamy obsługę uaktualnianie takiego magazynu.
Jeśli nie potrzebujesz kopii zapasowych hello toostore tego komputera już, a następnie należy wyrejestrować tej maszyny z hello magazynu i ponów uaktualnienie hello.

**Dlaczego nie widzę hello informacji zadania dla mojej lokalnymi zasobami po uaktualnieniu**</br>
Monitorowanie lokalnej kopii zapasowych (MARS agenta, program DPM i serwer kopii zapasowej Azure) to nowa funkcja, która pojawia się po uaktualnieniu magazynu usługi tooRecovery magazynu kopii zapasowej. Hello informacje kontrolne zajmuje too12 toosync godzin z usługą hello.

**Jak zgłosić problem?**</br>
Jakiejkolwiek jego części magazynu hello uaktualnienia nie powiedzie się, powitalne Uwaga OperationId na liście hello błędu. Microsoft Support aktywnego będzie działać tooresolve hello problem. Możesz dotrzeć tooSupport lub wiadomość e-mail na adres rsvaultupgrade@service.microsoft.com Twojego Identyfikatora subskrypcji, nazwę magazynu i OperationId. Firma Microsoft podejmie tooresolve hello problem tak szybko jak to możliwe. Nie ponów operację hello, chyba że jawnie instrukcją toodo tak przez firmę Microsoft.


## <a name="next-steps"></a>Następne kroki
Użyj poniższego artykułu, aby hello:</br>
[Tworzenie kopii zapasowej maszyn wirtualnych IaaS](backup-azure-arm-vms-prepare.md)</br>
[Utwórz kopię zapasową serwera kopia zapasowa Azure](backup-azure-microsoft-azure-backup.md)</br>
[Tworzenie kopii zapasowej systemu Windows Server](backup-configure-vault.md).
