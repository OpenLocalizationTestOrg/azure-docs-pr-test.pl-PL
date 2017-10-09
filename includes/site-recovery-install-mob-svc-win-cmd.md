1. Skopiuj hello Instalator tooa folder lokalny (na przykład C:\Temp) na powitania serwera, które mają tooprotect. Uruchom następujące polecenia z uprawnieniami administracyjnymi w wierszu polecenia hello:

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. tooinstall usługi mobilności, uruchom następujące polecenie hello:

  ```
  UnifiedAgent.exe /Role "MS" /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
  ```
3. Hello agent musi teraz toobe zarejestrowane na powitania serwera konfiguracji.

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
|/InstallLocation|Optional (Opcjonalność)|Lokalizacja, w którym jest zainstalowana usługa mobilności|Dowolnego folderu na komputerze hello|
|/ Platform|Obowiązkowy|Określa platformę hello, na które hello usługa mobilności jest wprowadzenie zainstalowana </br> </br>- **VMware** : Użyj tej wartości, jeśli instalujesz usługi mobilności na maszynie Wirtualnej uruchomionych na *VMware vSphere hostach ESXi*, *hosty funkcji Hyper-V* i *Phsyical serwerów* </br> - **Azure** : Użyj tej wartości, jeśli instalujesz agenta na maszynie Wirtualnej Azure IaaS| VMware </br> Azure|
|/ Dyskretnej|Optional (Opcjonalność)|Określa toorun hello Instalatora w trybie dyskretnym| Nie dotyczy|

>[!TIP]
> dzienniki instalacji Hello znajduje się w obszarze %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log

#### <a name="mobility-service-registration-command-line-arguments"></a>Argumenty wiersza polecenia rejestracji usługi mobilności

```
Usage :
UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
```

  | Parametr|Typ|Opis|Możliwe wartości|
  |-|-|-|-|
  |/ CSEndPoint |Obowiązkowy|Adres IP serwera konfiguracji hello| Dowolny prawidłowy adres IP|
  |/PassphraseFilePath|Obowiązkowy|Lokalizacja hello hasło |Wszelkie prawidłową ścieżką UNC lub ścieżkę do pliku lokalnego|


>[!TIP]
> Hello AgentConfiguration Dzienniki znajdują się w obszarze %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log
