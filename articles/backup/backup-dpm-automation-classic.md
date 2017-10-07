---
title: "Kopia zapasowa Azure: Użyj programu PowerShell tooback zapasowej obciążeń programu DPM | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy i zarządzanie nimi dla Data Protection Manager (DPM) przy użyciu programu PowerShell usługi Kopia zapasowa Azure"
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
ms.assetid: bcbcef79-9d33-4e84-a558-9866614f2cae
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;trinadhk;anuragm;markgal
ms.openlocfilehash: 48ebe6b520857836e89749ffb6fe83d1f14c5597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a>Wdrażanie i zarządzanie nimi tooAzure kopii zapasowej na serwerach Data Protection Manager (DPM) przy użyciu programu PowerShell
> [!div class="op_single_selector"]
> * [ARM](backup-dpm-automation.md)
> * [Wdrożenie klasyczne](backup-dpm-automation-classic.md)
>
>

W tym artykule opisano sposób toouse PowerShell tooback Konfigurowanie i odzyskiwanie danych programu DPM z magazynu kopii zapasowych. Firma Microsoft zaleca używanie Magazyny usług odzyskiwania dla wszystkich nowych wdrożeń. Nowy użytkownik kopia zapasowa Azure, za pomocą hello artykułu, [wdrażanie i zarządzanie nimi przy użyciu programu PowerShell tooAzure danych programu Data Protection Manager](backup-dpm-automation.md), więc dane są przechowywane w magazynie usług odzyskiwania.

> [!IMPORTANT]
> Teraz można uaktualnić Twoje Magazyny usług tooRecovery magazynów kopii zapasowych. Aby uzyskać więcej informacji, zobacz artykuł hello [uaktualnienia tooa magazynu kopii zapasowej, Magazyn usług odzyskiwania i](backup-azure-upgrade-backup-to-recovery-services.md). Firma Microsoft zachęca tooupgrade Magazyny usług tooRecovery magazyny kopii zapasowych. Po 15 października 2017 nie można użyć magazyny kopii zapasowych toocreate środowiska PowerShell. **Do 1 listopada 2017 r.**:
>- Wszystkie pozostałe magazyny kopii zapasowych zostanie automatycznie uaktualniony tooRecovery Magazyny usług.
>- Użytkownik nie będzie możliwe tooaccess danych kopii zapasowych w portalu klasycznym hello. Zamiast tego użyj hello Azure tooaccess portalu tej kopii zapasowej w Magazyny usług odzyskiwania.
>

## <a name="setting-up-hello-powershell-environment"></a>Konfigurowanie środowiska PowerShell hello
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

Przed użyciem programu PowerShell toomanage tworzenia kopii zapasowych z tooAzure programu Data Protection Manager, należy toohave hello prawo środowiska PowerShell. Na początku hello hello sesji programu PowerShell upewnij się, uruchom hello następujące polecenia tooimport hello prawo modułów i pozwala toocorrectly poleceń cmdlet DPM powitania dla odwołania:

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome toohello DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a>Instalację i rejestrację
toobegin:

1. [Pobierz najnowsze PowerShell](https://github.com/Azure/azure-powershell/releases) (minimalna wersja wymagana jest: 1.0.0)
2. Włącz polecenia cmdlet usługi Kopia zapasowa Azure hello przełączając zbyt*AzureResourceManager* trybie przy użyciu hello **Switch-AzureMode** apletu polecenia:

```
PS C:\> Switch-AzureMode AzureResourceManager
```

Witaj następujące ustawienia i zadania rejestracji można zautomatyzować przy użyciu programu PowerShell:

* Tworzenie magazynu kopii zapasowych
* Instalowanie agenta usługi Kopia zapasowa Azure hello
* Rejestrowanie w hello usługi Kopia zapasowa Azure
* Ustawienia sieciowe
* Ustawienia szyfrowania

### <a name="create-a-backup-vault"></a>Tworzenie magazynu kopii zapasowych
> [!WARNING]
> W przypadku klientów przy kopia zapasowa Azure powitania po raz pierwszy należy tooregister hello kopia zapasowa Azure dostawcy toobe używane w ramach subskrypcji. Można to zrobić, uruchamiając następujące polecenie hello: Register-AzureProvider - ProviderNamespace "Microsoft.Backup"
>
>

Można utworzyć nowy magazyn kopii zapasowych za pomocą hello **AzureRMBackupVault nowy** apletu polecenia. Hello magazynu kopii zapasowych jest zasobem ARM, więc należy tooplace go w grupie zasobów. W konsoli programu Azure PowerShell z podwyższonym poziomem uprawnień uruchom następujące polecenia hello:

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

Można uzyskać listę wszystkich magazynów kopii zapasowych hello w ramach danej subskrypcji przy użyciu hello **Get AzureRMBackupVault** apletu polecenia.

### <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a>Instalowanie agenta usługi Kopia zapasowa Azure hello na serwerze programu DPM
Przed zainstalowaniem agenta usługi Kopia zapasowa Azure hello należy toohave hello Instalatora, pobranych i znajdują się na powitania serwera systemu Windows. Możesz pobrać najnowszą wersję Instalatora hello hello ze hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) lub ze strony pulpitu nawigacyjnego hello magazynu kopii zapasowych. Zapisz Instalator hello tooan łatwo dostępnej lokalizacji, takich jak * C:\Downloads\*.

tooinstall hello agenta, uruchom następujące polecenie w konsoli programu PowerShell z podwyższonym poziomem uprawnień hello **na serwerze DPM hello**:

```
PS C:\> MARSAgentInstaller.exe /q
```

Spowoduje to zainstalowanie agenta hello z wszystkich opcji domyślnych hello. Instalacja Hello zajmuje kilka minut w tle hello. Jeśli nie określisz hello */nu* hello opcja **usługi Windows Update** na końcu hello hello toocheck instalacji dla wszystkich aktualizacji, zostanie otwarte okno.

Hello agent wyświetli hello listy zainstalowanych programów. toosee hello listy zainstalowanych programów, należy przejść za**Panelu sterowania** > **programy** > **programy i funkcje**.

![Agent został zainstalowany](./media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a>Opcje instalacji
toosee, który hello wszystkie opcje dostępne za pośrednictwem hello wiersza polecenia, użyj następującego polecenia hello:

```
PS C:\> MARSAgentInstaller.exe /?
```

Witaj dostępne opcje to:

| Opcja | Szczegóły | Domyślne |
| --- | --- | --- |
| /q |Instalację cichą |- |
| / p: "Lokalizacja" |Ścieżka folderu instalacji toohello hello Azure Backup Agent. |C:\Program Files\Microsoft Azure Recovery usługi agenta |
| / s: "Lokalizacja" |Ścieżka folderu pamięci podręcznej toohello hello Azure Backup Agent. |C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch |
| /m |TooMicrosoft opcjonalnych aktualizacji |- |
| /nu |Nie sprawdzaj aktualizacji po ukończeniu instalacji |- |
| /d |Odinstalowuje agenta usług odzyskiwania Microsoft Azure |- |
| /pH |Adres hosta serwera proxy |- |
| /Po |Numer portu hosta serwera proxy |- |
| /Pu |Nazwa użytkownika serwera proxy hosta |- |
| /PW |Hasło serwera proxy |- |

### <a name="registering-with-hello-azure-backup-service"></a>Rejestrowanie w hello usługi Kopia zapasowa Azure
Przed zarejestrowaniem z hello usługi Kopia zapasowa Azure, należy tooensure tego hello [wymagania wstępne](backup-azure-dpm-introduction.md) są spełnione. Należy:

* Masz ważną subskrypcję platformy Azure
* Masz magazyn kopii zapasowych

poświadczenia magazynu hello toodownload Uruchom hello **Get-AzureBackupVaultCredentials** polecenia w konsoli programu PowerShell systemu Azure i zapisać go w dogodnym miejscu, takich jak * C:\Downloads\*.

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

Rejestracji hello maszyny z magazynem hello jest wykonywane przy użyciu hello [Start DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) polecenia cmdlet:

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

To zarejestruje hello o nazwie "Serwerach" serwera DPM w magazynie usługi Microsoft Azure przy użyciu hello określone poświadczenia magazynu.

> [!IMPORTANT]
> Nie należy używać pliku poświadczeń magazynu hello toospecify ścieżek względnych. Należy podać ścieżkę bezwzględną jako polecenia cmdlet toohello wejściowego.
>
>

### <a name="initial-configuration-settings"></a>Ustawienia konfiguracji początkowej
Po hello serwer DPM jest zarejestrowany w magazynie usługi Kopia zapasowa Azure hello, rozpoczyna się od domyślnego ustawienia subskrypcji. Te ustawienia subskrypcji obejmują sieci, szyfrowania i hello obszaru przemieszczania. toobegin zmiana hello subskrypcji ustawień należy toofirst uzyskać dojścia do na powitania istniejące ustawienia (ustawienie domyślne) przy użyciu hello [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) polecenia cmdlet:

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

Wszystkie modyfikacje są wykonane toothis lokalnego środowiska PowerShell obiektu ```$setting``` , a następnie obiektowego hello jest tooDPM zatwierdzone i kopia zapasowa Azure toosave je przy użyciu hello [DPMCloudSubscriptionSetting zestaw](https://technet.microsoft.com/library/jj612791) polecenia cmdlet. Należy toouse hello ```–Commit``` tooensure flagę, która hello zmiany są zachowywane. Witaj ustawienia nie będą stosowane i używane przez usługi Kopia zapasowa Azure, chyba że zostało zatwierdzone.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a>Sieć
W przypadku łączności hello hello DPM maszyny toohello usługi Azure Backup na powitania internet za pośrednictwem serwera proxy, ustawienia serwera proxy hello należy podać dla toosucceed kopii zapasowych. Jest to zrobić za pomocą hello ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` i hello ```ProxyPassword``` parametrów z hello [DPMCloudSubscriptionSetting zestaw](https://technet.microsoft.com/library/jj612791) polecenia cmdlet. W tym przykładzie nie żadnego serwera proxy, dlatego firma Microsoft są jawnie wyczyszczenie żadnych informacji dotyczących serwera proxy.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

Wykorzystanie przepustowości można również sterować za pomocą opcji ```-WorkHourBandwidth``` i ```-NonWorkHourBandwidth``` dla danego zestawu dni tygodnia hello. W tym przykładzie firma Microsoft nie ustawienia dowolnej ograniczania.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-hello-staging-area"></a>Konfigurowanie hello obszaru przemieszczania
agent usługi Kopia zapasowa Azure Hello działającej na serwerze DPM hello wymaga tymczasowego magazynu dla danych przywróconych z chmury hello (lokalny obszar przemieszczania). Konfigurowanie przy użyciu hello obszaru przemieszczania hello [DPMCloudSubscriptionSetting zestaw](https://technet.microsoft.com/library/jj612791) polecenia cmdlet i hello ```-StagingAreaPath``` parametru.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

W powyższym przykładzie hello, obszaru przemieszczania hello zostanie ustawiona zbyt*C:\StagingArea* w obiekcie środowiska PowerShell hello ```$setting```. Upewnij się, że hello określony folder już istnieje, w przeciwnym razie hello końcowego zatwierdzania ustawienia subskrypcji hello zakończy się niepowodzeniem.

### <a name="encryption-settings"></a>Ustawienia szyfrowania
tooAzure wysyłane dane kopii zapasowej Hello kopii zapasowej jest zaszyfrowany tooprotect hello poufność danych hello. hasło szyfrowania Hello jest hello "password" toodecrypt hello danych w czasie hello przywracania. Jest to bezpieczne informacje ważne tookeep i secure po ustawieniu.

W poniższym przykładzie hello, pierwsze polecenie hello konwertuje ciąg hello ```passphrase123456789``` tooa bezpieczny ciąg i przypisuje hello bezpieczny ciąg toohello zmiennej o nazwie ```$Passphrase```. drugie polecenie Hello ustawia bezpieczny ciąg hello w ```$Passphrase``` jako hello hasła do szyfrowania kopii zapasowych.

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> Zachowaj informacje hasło hello bezpieczne po ustawieniu. Nie będzie możliwe toorestore danych z platformy Azure bez tego hasła.
>
>

W tym momencie powinien wprowadzone wszystkie hello wymagane zmiany toohello ```$setting``` obiektu. Należy pamiętać, toocommit hello zmiany.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a>Ochrona danych tooAzure kopii zapasowej
W tej sekcji możesz dodać tooDPM serwera produkcyjnego i chronić magazynu programu DPM toolocal danych hello, a następnie tooAzure kopii zapasowej. W przykładach hello przedstawiony zostanie sposób tooback zapasowe plików i folderów. Witaj logiki można łatwo można toobackup rozszerzonej z dowolnego źródła danych obsługiwane przez program DPM. Kopii zapasowych programu DPM są regulowane przez ochronę grupy (PG) z czterech części:

1. **Członków grupy** znajduje się lista wszystkich hello obiekty chronione (nazywane również *źródeł danych* w programie DPM), które mają tooprotect w hello tej samej grupy ochrony. Na przykład można tooprotect produkcji maszyny wirtualne w jednej grupy ochrony i baz danych programu SQL Server w innej grupy ochrony jako mogą mieć różne wymagania kopii zapasowej. Przed utworzeniem kopii zapasowej żadnego źródła danych na serwerze produkcyjnym należy toomake hello się, że Agent programu DPM jest zainstalowany na serwerze hello i jest zarządzany przez program DPM. Wykonaj procedurę hello [instalowanie hello agenta DPM](https://technet.microsoft.com/library/bb870935.aspx) i połączenie go toohello odpowiednie serwera DPM.
2. **Metoda ochrony danych** określa hello docelowej lokalizacji kopii zapasowych — taśma, dysk i chmura. W naszym przykładzie będzie chronić danych toohello lokalny dysk i toohello w chmurze.
3. A **harmonogram tworzenia kopii zapasowych** , który określa podczas tworzenia kopii zapasowych należy toobe podjęte i jak często hello dane mają być synchronizowane między hello serwera programu DPM i serwerze produkcyjnym hello.
4. A **harmonogramu przechowywania** Określa, jak długo punkty odzyskiwania hello tooretain na platformie Azure.

### <a name="creating-a-protection-group"></a>Utworzenie grupy ochrony
Rozpocznij od utworzenia nowej grupy ochrony za pomocą hello [DPMProtectionGroup nowy](https://technet.microsoft.com/library/hh881722) polecenia cmdlet.

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

Witaj powyżej polecenie cmdlet spowoduje utworzenie grupy ochrony o nazwie *ProtectGroup01*. Istniejącej grupy ochrony można także modyfikować nowszych kopii zapasowej tooadd toohello chmury Azure. Jednak toomake zmiany toohello grupy ochrony — nowy lub istniejący - potrzebujemy tooget dojścia na *modyfikowalnymi* obiektu przy użyciu hello [Get DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) polecenia cmdlet.

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a>Dodawanie grupy toohello członków grupy ochrony
Każdy Agent programu DPM wie hello listy źródeł danych na powitania serwera, który jest zainstalowany na. tooadd toohello datasource grupy ochrony, hello toofirst potrzeb agenta DPM wysyła listę hello źródeł danych toohello zapasowego serwera programu DPM. Jeden lub więcej źródeł danych są, a następnie wybrać i dodać toohello grupy ochrony. tooget kroki niezbędne PowerShell Hello osiągnięcia się to:

1. Pobierz listę wszystkich serwerów zarządzanych przez program DPM za pomocą hello agenta programu DPM.
2. Wybierz określonego serwera.
3. Pobranie listy wszystkich źródeł danych na powitania serwera.
4. Wybierz co najmniej jednego źródła danych, a następnie dodać toohello grupy ochrony

Hello listy serwerów, na które hello agenta programu DPM jest zainstalowany i jest zarządzany przez powitania serwera programu DPM są uzyskiwane z hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) polecenia cmdlet. W tym przykładzie firma Microsoft będzie filtrowania i skonfigurować tylko PS o nazwie *productionserver01* do utworzenia kopii zapasowej.

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

Teraz pobrać hello listy źródeł danych na ```$server``` przy użyciu hello [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) polecenia cmdlet. W tym przykładzie mamy filtrowania dla woluminu hello * D:\* którego chcemy tooconfigure do utworzenia kopii zapasowej. To źródło danych jest następnie dodawana toohello grupy ochrony za pomocą hello [DPMChildDatasource Dodaj](https://technet.microsoft.com/library/hh881732) polecenia cmdlet. Pamiętaj toouse hello *modifable* obiektu grupy ochrony ```$MPG``` toomake hello dodatków.

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

Powtórz ten krok liczbę razy, aż zostaną dodane wszystkie hello wybrane grupy ochrony toohello źródeł danych. Można również uruchomić tylko jedno źródło danych i hello pełny przepływ pracy tworzenia hello grupy ochrony i w późniejszym czasie dodać więcej źródeł danych toohello grupy ochrony.

### <a name="selecting-hello-data-protection-method"></a>Wybieranie metody ochrony danych hello
Po dodaniu źródła danych hello toohello grupy ochrony, hello następnym krokiem jest metoda ochrony hello toospecify przy użyciu hello [DPMProtectionType zestaw](https://technet.microsoft.com/library/hh881725) polecenia cmdlet. W tym przykładzie hello grupy ochrony będzie instalacji na dysku lokalnym, a kopia zapasowa w chmurze. Należy również toospecify hello datasource, które mają toocloud tooprotect przy użyciu hello [DPMChildDatasource Dodaj](https://technet.microsoft.com/library/hh881732.aspx) polecenia cmdlet flagą - Online.

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a>Ustawianie zakresu przechowywania hello
Ustawienia przechowywania hello hello punktów kopii zapasowej za pomocą hello [DPMPolicyObjective zestaw](https://technet.microsoft.com/library/hh881762) polecenia cmdlet. Gdy może wydawać się przechowywania hello nieparzysta tooset przed zdefiniowaniem hello harmonogram tworzenia kopii zapasowych, przy użyciu hello ```Set-DPMPolicyObjective``` polecenie cmdlet automatycznie ustawia domyślny harmonogram tworzenia kopii zapasowej, który może być modyfikowany. Jest zawsze harmonogram tworzenia kopii zapasowych hello możliwe tooset najpierw i hello zasady przechowywania po.

W poniższym przykładzie hello polecenia cmdlet hello ustawia hello parametry przechowywania kopii zapasowych na dysku. To zachowują kopie zapasowe 10 dni i synchronizowanie danych co 6 godzin między serwerem produkcyjnym hello i hello programu DPM. Witaj ```SynchronizationFrequencyMinutes``` nie definiuje, jak często punktu kopii zapasowej jest tworzony, ale jak często dane serwera DPM toohello skopiowanych; zapobiega to kopie zapasowe za duży.

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

Kopii zapasowych będzie tooAzure (Program DPM stosowany jest wspólny termin toothese kopii zapasowych Online) można skonfigurować dla zakresów przechowywania hello [długoterminowych przechowywania użyciu schematu dziadek-ojciec-syn. (GFS)](backup-azure-backup-cloud-as-tape.md). Oznacza to można zdefiniować zasady przechowywania Scalonej obejmujące codziennie, co tydzień, miesięcznych i rocznych zasady przechowywania. W tym przykładzie firma Microsoft utworzenia tablicy reprezentujący schemat przechowywania złożonych hello chcemy, a następnie skonfiguruj zakres przechowywania hello za pomocą hello [DPMPolicyObjective zestaw](https://technet.microsoft.com/library/hh881762) polecenia cmdlet.

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a>Harmonogram tworzenia kopii zapasowych hello zestawu
Program DPM ustawia automatycznie domyślny harmonogram tworzenia kopii zapasowej, jeśli Określ cel ochrony hello przy użyciu hello ```Set-DPMPolicyObjective``` polecenia cmdlet. toochange hello domyślne harmonogramy, użyj hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) polecenia cmdlet następuje hello [DPMPolicySchedule zestaw](https://technet.microsoft.com/library/hh881723) polecenia cmdlet.

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

W powyższym przykładzie hello ```$onlineSch``` jest tablicy z czterech elementów, które zawierają hello istniejący harmonogram ochrony w trybie online dla hello grupy ochrony w schemacie GFS hello:

1. ```$onlineSch[0]```będzie zawierać harmonogramu dziennego hello
2. ```$onlineSch[1]```będzie zawierać hello harmonogramu tygodniowego
3. ```$onlineSch[2]```będzie zawierać hello harmonogramu miesięcznego
4. ```$onlineSch[3]```będzie zawierać hello corocznych harmonogramu

Więc jeśli potrzebujesz harmonogramu tygodniowego hello toomodify należy toorefer toohello ```$onlineSch[1]```.

### <a name="initial-backup"></a>Początkowa kopia zapasowa
Podczas wykonywania kopii zapasowej źródła danych powitania po raz pierwszy, program DPM musi toocreate repliki początkowej, co spowoduje utworzenie kopii hello toobe źródeł danych chronionych na woluminie repliki programu DPM. To działanie albo mogą być planowane na określoną godzinę lub mogą być wyzwalane ręcznie, używając hello [DPMReplicaCreationMethod zestaw](https://technet.microsoft.com/library/hh881715) polecenia cmdlet z parametrem hello ```-NOW```.

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a>Zmiana rozmiaru hello repliki programu DPM i wolumin punktu odzyskiwania
Możesz również zmienić rozmiar woluminu repliki programu DPM, a także kopii w tle woluminu przy użyciu hello [DPMDatasourceDiskAllocation zestaw](https://technet.microsoft.com/library/hh881618.aspx) jak hello w poniższym przykładzie polecenie cmdlet: Get-DatasourceDiskAllocation - Datasource $DS Set-DatasourceDiskAllocation - Datasource $DS - ProtectionGroup $MPG-ręczne - ReplicaArea (2 gb) — ShadowCopyArea (2 gb)

### <a name="committing-hello-changes-toohello-protection-group"></a>Przekazywanie hello toohello zmiany grupy ochrony
Na koniec hello zmiany muszą toobe zatwierdzona przed programu DPM można wykonać kopię zapasową hello na powitania nowej konfiguracji grupy ochrony. Jest to realizowane przy użyciu hello [DPMProtectionGroup zestaw](https://technet.microsoft.com/library/hh881758) polecenia cmdlet.

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a>Wyświetlanie hello punktów kopii zapasowej
Można użyć hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) tooget polecenia cmdlet listę wszystkich punktów odzyskiwania dla źródła danych. W tym przykładzie zostaną wykonane następujące czynności:

* Pobierz wszystkie PGA hello na powitania serwera DPM, które będą przechowywane w tablicy```$PG```
* Pobierz toohello odpowiedniego hello źródeł danych```$PG[0]```
* Pobierz wszystkie hello punkty odzyskiwania dla źródła danych.

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a>Przywracanie danych chronionych na platformie Azure
Przywracanie danych jest kombinacją ```RecoverableItem``` obiektu i ```RecoveryOption``` obiektu. W poprzedniej sekcji hello dotarliśmy listę hello punktów kopii zapasowej dla źródła danych.

W poniższym przykładzie hello przedstawiony sposób toorestore funkcji Hyper-V maszyny wirtualnej z kopii zapasowej Azure za pomocą punktów kopii zapasowej łączenie z hello docelowe dla odzyskiwania. Obejmuje to:

* Tworzenie opcję odzyskiwania przy użyciu hello [DPMRecoveryOption nowy](https://technet.microsoft.com/library/hh881592) polecenia cmdlet.
* Pobrano tablicy hello punktów kopii zapasowej za pomocą hello ```Get-DPMRecoveryPoint``` polecenia cmdlet.
* Po wybraniu opcji tworzenia kopii zapasowej toorestore punktu z.

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

polecenia Hello można z łatwością rozszerzyć dla dowolnego typu źródła danych.

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać więcej informacji na temat tworzenia kopii zapasowej Azure dla programu DPM zobacz [tooDPM wprowadzenie kopii zapasowej](backup-azure-dpm-introduction.md)
