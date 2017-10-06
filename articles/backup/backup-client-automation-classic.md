---
title: kopie zapasowe systemu Windows Server toomanage PowerShell aaaUse na platformie Azure | Dokumentacja firmy Microsoft
description: "Wdrażanie i zarządzanie kopiami zapasowymi systemu Windows Server przy użyciu programu PowerShell."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: e7e269e2-1f11-41a9-957b-a2155de6a1e0
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: saurse;markgal;nkolli;trinadhk
ms.openlocfilehash: 72292e510b0f059102440bd49a195be4ef700a6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a>Wdrażanie i zarządzanie nimi tooAzure kopii zapasowej dla klienta systemu Windows i serwera systemu Windows przy użyciu programu PowerShell
> [!div class="op_single_selector"]
> * [ARM](backup-client-automation.md)
> * [Wdrożenie klasyczne](backup-client-automation-classic.md)
>
>

W tym artykule opisano, jak magazynu kopii zapasowej na toouse tooback programu PowerShell systemu Windows Server lub tooa danych stacji roboczej systemu Windows. Firma Microsoft zaleca używanie Magazyny usług odzyskiwania dla wszystkich nowych wdrożeń. Jeśli dla nowych użytkowników kopia zapasowa Azure i nie został utworzony magazyn kopii zapasowych w ramach subskrypcji, użyj hello artykułu, [wdrażania i zarządzania nimi przy użyciu programu PowerShell tooAzure danych programu Data Protection Manager](backup-client-automation.md) , dane są przechowywane w magazynie usług odzyskiwania. 

> [!IMPORTANT]
> Teraz można uaktualnić Twoje Magazyny usług tooRecovery magazynów kopii zapasowych. Aby uzyskać więcej informacji, zobacz artykuł hello [uaktualnienia tooa magazynu kopii zapasowej, Magazyn usług odzyskiwania i](backup-azure-upgrade-backup-to-recovery-services.md). Firma Microsoft zachęca tooupgrade Magazyny usług tooRecovery magazyny kopii zapasowych.<br/> Po 15 października 2017 nie można użyć magazyny kopii zapasowych toocreate środowiska PowerShell. **Do 1 listopada 2017 r.**:
>- Wszystkie pozostałe magazyny kopii zapasowych zostanie automatycznie uaktualniony tooRecovery Magazyny usług.
>- Użytkownik nie będzie możliwe tooaccess danych kopii zapasowych w portalu klasycznym hello. Zamiast tego użyj hello Azure tooaccess portalu tej kopii zapasowej w Magazyny usług odzyskiwania.
>

## <a name="install-azure-powershell"></a>Instalowanie programu Azure PowerShell
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

Października 2015 Azure PowerShell 1.0 został wydany. Ta wersja zakończyło się pomyślnie wersji hello 0.9.8 i temat istotne zmiany, szczególnie w hello wzorzec nazewnictwa hello poleceń cmdlet. Wykonaj polecenia cmdlet 1.0 hello wzorzec nazewnictwa {czasownik}-AzureRm {rzeczownik}; natomiast nie dołączaj nazwy hello 0.9.8 **Rm** (na przykład, New-AzureRmResourceGroup zamiast New-AzureResourceGroup). Podczas korzystania z programu Azure PowerShell 0.9.8, należy najpierw włączyć tryb Resource Manager hello, uruchamiając hello **Switch-AzureMode AzureResourceManager** polecenia. To polecenie nie jest konieczne w wersji 1.0 lub nowszej.

Jeśli chcesz toouse skryptów przeznaczony dla środowiska hello 0.9.8, hello 1.0 lub nowszej środowiska, należy dokładnie przetestować skrypty hello w środowisku przedprodukcyjnym przed ich użyciem w środowisku produkcyjnym tooavoid nieoczekiwany wpływu.

[Pobierz najnowszą wersję programu PowerShell hello](https://github.com/Azure/azure-powershell/releases) (minimalna wersja wymagana jest: 1.0.0)

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-backup-vault"></a>Tworzenie magazynu kopii zapasowych
> [!WARNING]
> W przypadku klientów przy kopia zapasowa Azure powitania po raz pierwszy należy tooregister hello kopia zapasowa Azure dostawcy toobe używane w ramach subskrypcji. Można to zrobić, uruchamiając następujące polecenie hello: Register-AzureProvider - ProviderNamespace "Microsoft.Backup"
>
>

Można utworzyć nowy magazyn kopii zapasowych za pomocą hello **AzureRMBackupVault nowy** polecenia cmdlet. Hello magazynu kopii zapasowych jest zasobem ARM, więc należy tooplace go w grupie zasobów. W konsoli programu Azure PowerShell z podwyższonym poziomem uprawnień uruchom następujące polecenia hello:

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

Użyj hello **Get AzureRMBackupVault** magazyny kopii zapasowych hello toolist polecenia cmdlet w ramach subskrypcji.

## <a name="installing-hello-azure-backup-agent"></a>Instalowanie agenta usługi Kopia zapasowa Azure hello
Przed zainstalowaniem agenta usługi Kopia zapasowa Azure hello należy toohave hello Instalatora, pobranych i znajdują się na powitania serwera systemu Windows. Możesz pobrać najnowszą wersję Instalatora hello hello ze hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) lub ze strony pulpitu nawigacyjnego hello magazynu kopii zapasowych. Zapisz Instalator hello tooan łatwo dostępnej lokalizacji, takich jak * C:\Downloads\*.

tooinstall hello agenta, uruchom następujące polecenie w konsoli programu PowerShell z podwyższonym poziomem uprawnień hello:

```
PS C:\> MARSAgentInstaller.exe /q
```

Spowoduje to zainstalowanie agenta hello z wszystkich opcji domyślnych hello. Instalacja Hello zajmuje kilka minut w tle hello. Jeśli nie określisz hello */nu* opcji, a następnie hello **usługi Windows Update** na końcu hello hello toocheck instalacji dla wszystkich aktualizacji, zostanie otwarte okno. Po zainstalowaniu agenta hello wyświetli hello listy zainstalowanych programów.

toosee hello listy zainstalowanych programów, należy przejść za**Panelu sterowania** > **programy** > **programy i funkcje**.

![Agent został zainstalowany](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a>Opcje instalacji
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

## <a name="registering-with-hello-azure-backup-service"></a>Rejestrowanie w hello usługi Kopia zapasowa Azure
Przed zarejestrowaniem z hello usługi Kopia zapasowa Azure, należy tooensure tego hello [wymagania wstępne](backup-configure-vault.md) są spełnione. Należy:

* Masz ważną subskrypcję platformy Azure
* Masz magazyn kopii zapasowych

poświadczenia magazynu hello toodownload Uruchom hello **Get-AzureRMBackupVaultCredentials** polecenia cmdlet w konsoli programu PowerShell systemu Azure i zapisać go w dogodnym miejscu, takich jak * C:\Downloads\*.

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

Rejestracji hello maszyny z magazynem hello jest wykonywane przy użyciu hello [Start OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) polecenia cmdlet:

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration -VaultCredentials $cred -Confirm:$false

CertThumbprint      : 7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName : test-vault
Region              : West US

Machine registration succeeded.
```

> [!IMPORTANT]
> Nie należy używać pliku poświadczeń magazynu hello toospecify ścieżek względnych. Należy podać ścieżkę bezwzględną jako polecenia cmdlet toohello wejściowego.
>
>

## <a name="networking-settings"></a>Ustawienia sieciowe
Gdy łączność hello hello systemu Windows maszyny toohello jest internet za pośrednictwem serwera proxy, ustawienia serwera proxy hello można również podać o toohello agenta. W tym przykładzie nie żadnego serwera proxy, dlatego firma Microsoft są jawnie wyczyszczenie żadnych informacji dotyczących serwera proxy.

Wykorzystanie przepustowości można również sterować za pomocą opcji hello ```work hour bandwidth``` i ```non-work hour bandwidth``` dla danego zestawu dni tygodnia hello.

Ustawienie szczegóły serwera proxy i przepustowości hello jest wykonywane przy użyciu hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) polecenia cmdlet:

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a>Ustawienia szyfrowania
tooAzure wysyłane dane kopii zapasowej Hello kopii zapasowej jest zaszyfrowany tooprotect hello poufność danych hello. hasło szyfrowania Hello jest hello "password" toodecrypt hello danych w czasie hello przywracania.

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
Server properties updated successfully
```

> [!IMPORTANT]
> Zachowaj informacje hasło hello bezpieczne po ustawieniu. Nie będzie możliwe toorestore danych z platformy Azure bez tego hasła.
>
>

## <a name="back-up-files-and-folders"></a>Tworzenie kopii zapasowych plików i folderów
Kopie zapasowe z serwerów z systemem Windows i klientów tooAzure kopii zapasowej zarządzane przez zasady. zasady Hello składa się z trzech części:

1. A **harmonogram tworzenia kopii zapasowych** , który określa podczas tworzenia kopii zapasowych należy toobe podjęte, a następnie synchronizowane z usługą hello.
2. A **harmonogramu przechowywania** Określa, jak długo punkty odzyskiwania hello tooretain na platformie Azure.
3. A **określania włączenia/wyłączenia pliku** które nakazują, co należy utworzyć kopię.

W tym dokumencie ponieważ będziemy w przypadku automatyzacji kopii zapasowej, przyjęto będzie założenie, że nic nie skonfigurowano. Zaczniemy przez utworzenie nowych zasad tworzenia kopii zapasowej przy użyciu hello [OBPolicy nowy](https://technet.microsoft.com/library/hh770416.aspx) polecenia cmdlet i przy jego użyciu.

```
PS C:\> $newpolicy = New-OBPolicy
```

W tym hello czasu zasady jest pusta i innych poleceń cmdlet są potrzebne toodefine jakie elementy zostaną uwzględnione lub wykluczone, gdy kopie zapasowe zostaną uruchomione i gdy hello kopie zapasowe będą przechowywane.

### <a name="configuring-hello-backup-schedule"></a>Konfigurowanie hello harmonogram tworzenia kopii zapasowych
Witaj najpierw hello 3 części zasad jest harmonogram tworzenia kopii zapasowych hello, który został utworzony za pomocą hello [OBSchedule nowy](https://technet.microsoft.com/library/hh770401) polecenia cmdlet. harmonogram tworzenia kopii zapasowych Hello definiuje, podczas tworzenia kopii zapasowych należy toobe podjęte. Podczas tworzenia harmonogramu należy toospecify 2 parametry wejściowe:

* **Dni tygodnia hello** hello kopii zapasowej powinno być ono uruchomione. Można uruchomić zadanie tworzenia kopii zapasowej hello na tylko jeden dzień lub każdego dnia tygodnia hello lub dowolną kombinację między.
* **Pór dnia hello** uruchomienia hello kopii zapasowej. Można zdefiniować się too3 różnych porach dnia hello, gdy zostanie wywołane hello kopii zapasowej.

Na przykład można skonfigurować zasad tworzenia kopii zapasowej, wykonywany o 16: 00 w każdą sobotę i niedziela.

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

harmonogram tworzenia kopii zapasowych Hello musi toobe skojarzonej z zasadami i można to osiągnąć przy użyciu hello [OBSchedule zestaw](https://technet.microsoft.com/library/hh770407) polecenia cmdlet.

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a>Konfigurowania zasad przechowywania
zasady przechowywania Hello definiuje czas odzyskiwania, punkty utworzone na podstawie zadania tworzenia kopii zapasowej zostaną zachowane. Podczas tworzenia nowych zasad przechowywania przy użyciu hello [OBRetentionPolicy nowy](https://technet.microsoft.com/library/hh770425) polecenia cmdlet, można określić hello liczbę dni, które hello punktów odzyskiwania należy toobe przechowywane w usłudze Kopia zapasowa Azure. w poniższym przykładzie Hello ustawia zasady przechowywania wynosi 7 dni.

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

Witaj zasady przechowywania muszą być skojarzone z zasadami głównego hello przy użyciu polecenia cmdlet hello [OBRetentionPolicy zestaw](https://technet.microsoft.com/library/hh770405):

```
PS C:\> Set-OBRetentionPolicy -Policy $newpolicy -RetentionPolicy $retentionpolicy

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          :
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```
### <a name="including-and-excluding-files-toobe-backed-up"></a>Włączanie i wyłączanie toobe pliki kopii zapasowej
```OBFileSpec``` Obiekt definiuje hello pliki toobe dołączone i wykluczone w kopii zapasowej. Jest to zestaw reguł, że zakres limit hello chronione pliki i foldery na komputerze. Może mieć wiele pliku reguł dołączania lub wykluczania zgodnie z wymaganiami i skojarzyć je z zasadami. Tworząc nowy obiekt OBFileSpec, można:

* Określ toobe pliki i foldery hello włączone
* Określ toobe pliki i foldery hello wyłączone
* Określ rekursywne tworzenie kopii zapasowych danych w folderze (lub) czy tylko hello pliki najwyższego poziomu w określonym folderze hello należy utworzyć kopię zapasową.

ostatnie Hello odbywa się przy użyciu flagi - Nierekurencyjny hello w poleceniu hello OBFileSpec nowy.

W poniższym przykładzie hello możemy utworzyć kopię zapasową woluminu, C: i D: i wykluczanie plików binarnych systemu operacyjnego hello w folderze systemu Windows hello i foldery tymczasowe. toodo, utworzymy dwa specyfikacji pliku przy użyciu hello [OBFileSpec nowy](https://technet.microsoft.com/library/hh770408) polecenia cmdlet — jeden dla dołączania i jeden do wykluczenia. Po utworzeniu specyfikacji pliku hello są powiązane z zasadami hello przy użyciu hello [OBFileSpec Dodaj](https://technet.microsoft.com/library/hh770424) polecenia cmdlet.

```
PS C:\> $inclusions = New-OBFileSpec -FileSpec @("C:\", "D:\")

PS C:\> $exclusions = New-OBFileSpec -FileSpec @("C:\windows", "C:\temp") -Exclude

PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $inclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid


PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $exclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\windows
                  IsExclude:True
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\temp
                  IsExclude:True
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```

### <a name="applying-hello-policy"></a>Zastosowanie zasad hello
Teraz hello obiektu zasad została zakończona i ma skojarzone harmonogram tworzenia kopii zapasowych, zasad przechowywania i włączenia/wyłączenia lista plików. Te zasady można teraz zatwierdzone dla toouse kopia zapasowa Azure. Przed zastosowaniem hello nowo utworzone zasady upewnij się, że nie ma żadnych istniejących zasad tworzenia kopii zapasowej skojarzonego z serwerem hello przy użyciu hello [OBPolicy Usuń](https://technet.microsoft.com/library/hh770415) polecenia cmdlet. Usuwanie zasad hello wyświetli monit o potwierdzenie. Potwierdzenie hello tooskip Użyj hello ```-Confirm:$false``` flagę hello polecenia cmdlet.

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

Przekazywanie obiektu zasad hello jest wykonywane przy użyciu hello [OBPolicy zestaw](https://technet.microsoft.com/library/hh770421) polecenia cmdlet. Spowoduje to również monituje o potwierdzenie. Potwierdzenie hello tooskip Użyj hello ```-Confirm:$false``` flagę hello polecenia cmdlet.

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want toosave this backup policy ? [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s)
DsList : {DataSource
         DatasourceId:4508156004108672185
         Name:C:\
         FileSpec:FileSpec
         FileSpec:C:\
         IsExclude:False
         IsRecursive:True,

         FileSpec
         FileSpec:C:\windows
         IsExclude:True
         IsRecursive:True,

         FileSpec
         FileSpec:C:\temp
         IsExclude:True
         IsRecursive:True,

         DataSource
         DatasourceId:4508156005178868542
         Name:D:\
         FileSpec:FileSpec
         FileSpec:D:\
         IsExclude:False
         IsRecursive:True
    }
PolicyName : c2eb6568-8a06-49f4-a20e-3019ae411bac
RetentionPolicy : Retention Days : 7
              WeeklyLTRSchedule :
              Weekly schedule is not set

              MonthlyLTRSchedule :
              Monthly schedule is not set

              YearlyLTRSchedule :
              Yearly schedule is not set
State : Existing PolicyState : Valid
```

Możesz wyświetlić szczegóły hello hello istniejących zasad tworzenia kopii zapasowej przy użyciu hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) polecenia cmdlet. Użytkownik może przejść za pomocą hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) polecenia cmdlet hello harmonogram tworzenia kopii zapasowych i hello [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) polecenia cmdlet dla zasad przechowywania hello

```
PS C:> Get-OBPolicy | Get-OBSchedule
SchedulePolicyName : 71944081-9950-4f7e-841d-32f0a0a1359a
ScheduleRunDays : {Saturday, Sunday}
ScheduleRunTimes : {16:00:00}
State : Existing

PS C:> Get-OBPolicy | Get-OBRetentionPolicy
RetentionDays : 7
RetentionPolicyName : ca3574ec-8331-46fd-a605-c01743a5265e
State : Existing

PS C:> Get-OBPolicy | Get-OBFileSpec
FileName : *
FilePath : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
FileSpec : D:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\
FileSpec : C:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\windows
FileSpec : C:\windows
IsExclude : True
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\temp
FileSpec : C:\temp
IsExclude : True
IsRecursive : True
```

### <a name="performing-an-ad-hoc-backup"></a>Wykonywanie kopii zapasowych ad hoc
Po ustawieniu zasad tworzenia kopii zapasowej hello kopii zapasowych zostanie przeprowadzona na powitania harmonogramu. Wyzwolenie kopii zapasowych ad hoc jest także możliwe przy użyciu hello [Start OBBackup](https://technet.microsoft.com/library/hh770426) polecenia cmdlet:

```
PS C:> Get-OBPolicy | Start-OBBackup
Taking snapshot of volumes...
Preparing storage...
Estimating size of backup items...
Estimating size of backup items...
Transferring data...
Verifying backup...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a>Przywróć dane z usługi Kopia zapasowa Azure
W tej sekcji przedstawiono kroki hello do automatyzacji odzyskiwanie danych z kopii zapasowej Azure. Spowoduje to obejmuje hello następujące kroki:

1. Wybierz wolumin źródłowy hello
2. Wybierz opcję tworzenia kopii zapasowej toorestore punktu
3. Wybierz element toorestore
4. Proces przywracania hello wyzwalacza

### <a name="picking-hello-source-volume"></a>Wolumin źródła hello pobrania
W kolejności toorestore element z kopii zapasowej Azure najpierw tooidentify hello źródła elementu hello. Ponieważ firma Microsoft jest wykonywania poleceń hello w kontekście systemu Windows Server lub klienta systemu Windows hello, jest już zidentyfikowany hello maszyny. następnym krokiem Hello w identyfikacji źródła hello jest tooidentify hello woluminu zawierającego go. Listę woluminów lub źródła Trwa wykonywanie kopii zapasowej z tego komputera mogą być pobierane, wykonując hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) polecenia cmdlet. To polecenie zwraca tablicę wszystkich źródeł hello kopii zapasowej z serwera/klienta.

```
PS C:> $source = Get-OBRecoverableSource
PS C:> $source
FriendlyName : C:\
RecoverySourceName : C:\
ServerName : myserver.microsoft.com

FriendlyName : D:\
RecoverySourceName : D:\
ServerName : myserver.microsoft.com
```

### <a name="choosing-a-backup-point-toorestore"></a>Wybieranie kopii zapasowej toorestore punktu
Witaj listy punktów kopii zapasowej mogą zostać pobrane przez wykonywania hello [Get OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) polecenie cmdlet z odpowiednimi parametrami. W naszym przykładzie wybrano hello najnowszego punktu kopii zapasowej dla woluminu źródłowego hello *D:* i korzystać z niego toorecover określonego pliku.

```
PS C:> $rps = Get-OBRecoverableItem -Source $source[1]
IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :

IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 17-Jun-15 6:31:31 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :
```
Obiekt Hello ```$rps``` jest tablicą punktów kopii zapasowej. pierwszy element Hello jest hello najnowszy punkt i hello n-tego elementu jest hello starsze punkty. używamy toochoose hello najnowszy punkt ```$rps[0]```.

### <a name="choosing-an-item-toorestore"></a>Wybieranie toorestore elementu
tooidentify hello plików lub folder toorestore rekursywnie Użyj hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) polecenia cmdlet. Hierarchia folderów hello ten sposób można przeglądać wyłącznie przy użyciu hello ```Get-OBRecoverableItem```.

W tym przykładzie, jeśli chcemy pliku hello toorestore *finances.xls* firma Microsoft może odwoływać się przy użyciu tego obiektu hello ```$filesFolders[1]```.

```
PS C:> $filesFolders = Get-OBRecoverableItem $rps[0]
PS C:> $filesFolders
IsDir : True
ItemNameFriendly : D:\MyData\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\
LocalMountPoint : D:\
MountPointName : D:\
Name : MyData
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime : 15-Jun-15 8:49:29 AM

PS C:> $filesFolders = Get-OBRecoverableItem $filesFolders[0]
PS C:> $filesFolders
IsDir : False
ItemNameFriendly : D:\MyData\screenshot.oxps
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\screenshot.oxps
LocalMountPoint : D:\
MountPointName : D:\
Name : screenshot.oxps
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 228313
ItemLastModifiedTime : 21-Jun-14 6:45:09 AM

IsDir : False
ItemNameFriendly : D:\MyData\finances.xls
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\finances.xls
LocalMountPoint : D:\
MountPointName : D:\
Name : finances.xls
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 96256
ItemLastModifiedTime : 21-Jun-14 6:43:02 AM
```

Możesz również wyszukać toorestore elementów przy użyciu hello ```Get-OBRecoverableItem``` polecenia cmdlet. W naszym przykładzie toosearch dla *finances.xls* firma Microsoft można uzyskać dojścia do pliku hello, uruchamiając polecenie:

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a>Wyzwolenie procesu przywracania hello
proces przywracania hello tootrigger, najpierw musisz opcje odzyskiwania hello toospecify. Można to zrobić za pomocą hello [OBRecoveryOption nowy](https://technet.microsoft.com/library/hh770417.aspx) polecenia cmdlet. Na przykład załóżmy, że czy zbyt chcemy pliki hello toorestore*C:\temp*. Umożliwia również założono, że chcemy tooskip pliki, które już istnieją w folderze docelowym hello *C:\temp*. toocreate takie opcję odzyskiwania, użyj hello następujące polecenie:

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

Teraz wyzwalanie przywracania przy użyciu hello [Start OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) na powitania wybrane ```$item``` z danych wyjściowych hello hello ```Get-OBRecoverableItem``` polecenia cmdlet:

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a>Odinstalowanie agenta usługi Kopia zapasowa Azure hello
Odinstalowanie agenta usługi Kopia zapasowa Azure hello może odbywać się przy użyciu hello następujące polecenie:

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

Odinstalowywanie pliki binarne agenta hello z maszyny hello ma niektórych tooconsider konsekwencje:

* Usuwa filtr plików hello z hello maszyny i śledzenie zmian jest zatrzymana.
* Wszystkie informacje o zasadach zostanie usunięty z maszyny hello, ale informacje o zasadach hello nadal toobe przechowywany w usłudze hello.
* Wszystkie harmonogramy tworzenia kopii zapasowej są usuwane i są pobierane nie dalsze kopii zapasowych.

Jednak hello dane przechowywane w pozostaje Azure i są przechowywane zgodnie z ustawień zasad przechowywania hello przez użytkownika. Starsze punkty automatycznie są przestarzałe.

## <a name="remote-management"></a>Zdalne zarządzanie
Całe Zarządzanie hello wokół hello agenta usługi Kopia zapasowa Azure, zasady i źródłami danych mogą to robić zdalnie za pomocą programu PowerShell. Witaj maszyny, który będzie zarządzany zdalnie musi toobe poprawnie przygotowany.

Domyślnie program hello Usługa WinRM jest skonfigurowany do uruchamiania ręcznego. musi być zbyt ustawionym typem uruchomienia Hello*automatyczne* i hello usługi powinny być uruchamiane. tooverify, który hello Usługa WinRM jest uruchomiona, musi mieć wartość hello hello właściwość stanu *systemem*.

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

Programu PowerShell, należy skonfigurować dla niego komunikację zdalną.

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

maszyny Hello teraz można zarządzać zdalnie — począwszy od instalacji hello hello agenta. Na przykład hello następującego skryptu kopiuje hello maszyny zdalnej toohello agenta i instaluje je.

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji o kopii zapasowej dla systemu Windows Server/klienta Azure, zobacz

* [Wprowadzenie tooAzure kopii zapasowej](backup-introduction-to-azure-backup.md)
* [Wykonaj kopię zapasową serwerów z systemem Windows](backup-configure-vault.md)
