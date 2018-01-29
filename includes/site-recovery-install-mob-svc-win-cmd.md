1. Skopiuj Instalatora na folder lokalny (na przykład C:\Temp) na serwerze, który chcesz chronić. Uruchom następujące polecenia z uprawnieniami administracyjnymi w wierszu polecenia:

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. Aby zainstalować usługi mobilności, uruchom następujące polecenie:

  ```
  UnifiedAgent.exe /Role "MS" /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
  ```
3. Teraz agent musi być zarejestrowany na serwerze konfiguracji.

  ```
  cd C:\Program Files (x86)\Microsoft Azure Site Recovery\agent
  UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a>Argumenty wiersza polecenia Instalatora usługi mobilności

```
Usage :
UnifiedAgent.exe /Role <MS|MT> /InstallLocation <Install Location> /Platform “VmWare” /Silent
```

| Parametr|Typ|Opis|Możliwe wartości|
|-|-|-|-|
|/ Roli|Obowiązkowy|Określa, czy należy zainstalować usługi mobilności (MS) lub MasterTarget(MT) powinna zostać zainstalowana.|MS </br> MT|
|/InstallLocation|Optional (Opcjonalność)|Lokalizacja, w którym jest zainstalowana usługa mobilności|Dowolny folder na komputerze|
|/ Platform|Obowiązkowy|Określa platformę, na którym zainstalowano pobierania usługi mobilności </br> </br>- **VMware** : Użyj tej wartości, jeśli instalujesz usługi mobilności na maszynie Wirtualnej systemem *VMware vSphere hostach ESXi*, *hosty funkcji Hyper-V* i *serwerów fizycznych* </br> - **Azure** : Użyj tej wartości, jeśli instalujesz agenta na maszynie Wirtualnej Azure IaaS| VMware </br> Azure|
|/ Dyskretnej|Optional (Opcjonalność)|Określa, aby uruchomić Instalatora w trybie dyskretnym| Nie dotyczy|

>[!TIP]
> Dzienniki instalacji można znaleźć w %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log

#### <a name="mobility-service-registration-command-line-arguments"></a>Argumenty wiersza polecenia rejestracji usługi mobilności

```
Usage :
UnifiedAgentConfigurator.exe  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
```

  | Parametr|Typ|Opis|Możliwe wartości|
  |-|-|-|-|
  |/ CSEndPoint |Obowiązkowy|Adres IP serwera konfiguracji| Dowolny prawidłowy adres IP|
  |/PassphraseFilePath|Obowiązkowy|Lokalizacja hasło |Wszelkie prawidłową ścieżką UNC lub ścieżkę do pliku lokalnego|


>[!TIP]
> Dzienniki AgentConfiguration znajduje się w obszarze %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log
