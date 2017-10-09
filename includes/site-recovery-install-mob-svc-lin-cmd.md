1. Skopiuj hello Instalator tooa folder lokalny (na przykład /tmp) na powitania serwera, które mają tooprotect. W terminalu uruchom następujące polecenia hello:
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. tooinstall usługi mobilności, uruchom następujące polecenie hello:

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. Po zakończeniu instalacji hello usługi mobilności musi tooget zarejestrowanych toohello konfiguracji serwera. Hello uruchom następujące polecenie tooregister hello usługi mobilności z serwerem konfiguracji.

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a>Instalator usługi mobilności wiersza polecenia

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|Parametr|Typ|Opis|Możliwe wartości|
|-|-|-|-|
|-r |Obowiązkowy|Określa, czy należy zainstalować usługi mobilności (MS) lub MasterTarget(MT) powinna zostać zainstalowana.|MS </br> MT|
|-d |Optional (Opcjonalność)|Lokalizacja, w którym zostanie zainstalowana usługa mobilności|/usr/local/ASR|
|-v|Obowiązkowy|Określa platformę hello, na które hello usługa mobilności jest wprowadzenie zainstalowana </br> </br>- **VMware** : Użyj tej wartości, jeśli instalujesz usługi mobilności na maszynie Wirtualnej uruchomionych na *VMware vSphere hostach ESXi*, *hosty funkcji Hyper-V* i *Phsyical serwerów* </br> - **Azure** : Użyj tej wartości, jeśli instalujesz agenta na maszynie Wirtualnej Azure IaaS| VMware </br> Azure|
|-q|Optional (Opcjonalność)|Określa toorun Instalatora w trybie dyskretnym| Nie dotyczy|


#### <a name="mobility-service-configuration-command-line"></a>Konfiguracja usługi mobilności wiersza polecenia

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|Parametr|Typ|Opis|Możliwe wartości|
|-|-|-|-|
|-i |Obowiązkowy|Adres IP serwera konfiguracji hello|Dowolny prawidłowy adres IP|
|-P |Obowiązkowy|Pełna ścieżka hello pliku której jest zapisywany hello hasło połączenia|Nieprawidłowa folderu|
