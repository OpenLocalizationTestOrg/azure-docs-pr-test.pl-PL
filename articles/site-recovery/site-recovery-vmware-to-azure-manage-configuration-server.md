---
title: " Zarządzanie serwerem konfiguracji w usłudze Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tooset i zarządzać serwerem konfiguracji."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 2852bcd25409121be46a1ebf135ebfcdce6e5de5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-configuration-server"></a>Zarządzanie serwerem konfiguracji

Serwer konfiguracji pełni funkcję koordynatora między hello usługi Site Recovery i infrastruktury lokalnej. W tym artykule opisano, jak można skonfigurować, konfigurowania i zarządzania powitania serwera konfiguracji.

## <a name="prerequisites"></a>Wymagania wstępne
Witaj poniżej przedstawiono hello minimalne wymagania dotyczące sprzętu, oprogramowania i sieci tooset wymagana jest konfiguracja serwera konfiguracji.

> [!NOTE]
> [Planowanie pojemności](site-recovery-capacity-planner.md) jest tooensure ważnym krokiem wdrażania powitania serwera konfiguracji z konfiguracją tego pakiety wymagań obciążenia. Przeczytaj więcej na temat [zmiany rozmiaru wymagania dotyczące serwera konfiguracji](#sizing-requirements-for-a-configuration-server).

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-configuration-server-software"></a>Pobieranie powitania serwera konfiguracji oprogramowania
1. Zaloguj się na toohello Azure tooyour portalu i przeglądania magazynu usług odzyskiwania.
2. Przeglądaj zbyt**infrastruktura usługi Site Recovery** > **serwery konfiguracji** (w przypadku VMware i maszyn fizycznych).

  ![Dodaj stronę serwerów](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. Kliknij przycisk hello **+ serwery** przycisku.
4. Na powitania **Dodaj serwer** kliknij klucz rejestracji hello toodownload hello pobierania przycisku. Ten klucz jest potrzebne podczas tooregister instalacji serwera konfiguracji hello za pomocą usługi Azure Site Recovery.
5. Kliknij przycisk hello **hello pobierania Instalatora Microsoft Azure Site Recovery Unified** łącze toodownload hello najnowszą wersję powitania serwera konfiguracji.

  ![Strona pobierania](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  Można pobrać najnowszą wersję powitania serwera konfiguracji bezpośrednio z [strony pobierania witryny Microsoft Download Center](http://aka.ms/unifiedsetup)

## <a name="installing-and-registering-a-configuration-server-from-gui"></a>Instalowanie i rejestrowanie konfiguracji serwer z graficznym interfejsem użytkownika
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a>Instalowanie i rejestrowanie serwera konfiguracji przy użyciu wiersza polecenia

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a>Przykładowe zastosowanie
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a>Serwer konfiguracji Instalator argumenty wiersza polecenia.
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a>Utwórz plik poświadczeń MySql
Parametr MySQLCredsFilePath przyjmuje pliku jako dane wejściowe. Tworzenie pliku hello przy użyciu hello następujący format i przekaż go jako parametr wejściowy MySQLCredsFilePath.
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a>Utwórz plik konfiguracji ustawień serwera proxy
Parametr ProxySettingsFilePath przyjmuje pliku jako dane wejściowe. Tworzenie pliku hello przy użyciu hello następujący format i przekaż go jako parametr wejściowy ProxySettingsFilePath.

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a>Modyfikowanie ustawień konfiguracji serwera proxy
1. Tooyour logowania serwera konfiguracji.
2. Uruchamianie cspsconfigtool.exe hello za pomocą skrótu hello na użytkownika.
3. Kliknij przycisk hello **rejestracji magazynu** kartę.
4. Pobranie nowego pliku magazynu rejestracji z portalu hello i przekazują je jako narzędzie toohello wejściowego.

  ![serwer w przypadku konfiguracji rejestru](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. Podaj nowe szczegóły serwera Proxy hello i kliknij przycisk hello **zarejestrować** przycisku.
6. Otwórz okno poleceń programu PowerShell administratora.
7. Uruchom następujące polecenie hello
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  Jeśli proces skalowania w poziomie serwery podłączone toothis konfiguracji serwera, należy za[napraw hello ustawienia serwera proxy na wszystkich serwerach proces skalowania w poziomie hello](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) w danym wdrożeniu.

## <a name="re-register-a-configuration-server-with-hello-same-recovery-services-vault"></a>Zarejestruj ponownie serwer konfiguracji hello tego samego magazynu usług odzyskiwania
  1. Tooyour logowania serwera konfiguracji.
  2. Uruchom program hello cspsconfigtool.exe za pomocą hello skrótu na pulpicie.
  3. Kliknij przycisk hello **rejestracji magazynu** kartę.
  4. Pobranie nowego pliku rejestracji z portalu hello i przekazują je jako narzędzie toohello wejściowego.
        ![serwer w przypadku konfiguracji rejestru](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
  5. Podaj szczegóły serwera Proxy hello, a następnie kliknij przycisk hello **zarejestrować** przycisku.  
  6. Otwórz okno poleceń programu PowerShell administratora.
  7. Uruchom następujące polecenie hello

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  Jeśli proces skalowania w poziomie serwery podłączone toothis konfiguracji serwera, należy za[ponownie zarejestrować wszystkie serwery proces skalowania w poziomie hello](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) w danym wdrożeniu.

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a>Rejestrowanie serwera konfiguracji w innym magazynie usług odzyskiwania.
1. Tooyour logowania serwera konfiguracji.
2. z wiersza polecenia z uprawnieniami administratora uruchom polecenie hello

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. Uruchamianie cspsconfigtool.exe hello za pomocą skrótu hello na użytkownika.
4. Kliknij przycisk hello **rejestracji magazynu** kartę.
5. Pobranie nowego pliku rejestracji z portalu hello i przekazują je jako narzędzie toohello wejściowego.

    ![serwer w przypadku konfiguracji rejestru](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. Podaj szczegóły serwera Proxy hello, a następnie kliknij przycisk hello **zarejestrować** przycisku.  
7. Otwórz okno poleceń programu PowerShell administratora.
8. Uruchom następujące polecenie hello
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a>Wycofanie z eksploatacji serwera konfiguracji
Upewnij się, poniżej hello przed rozpoczęciem likwidowania serwera konfiguracji.
1. Wyłącz ochronę dla wszystkich maszyn wirtualnych na tym serwerze konfiguracji.
2. Usuń skojarzenie wszystkich zasad replikacji z powitania serwera konfiguracji.
3. Usuń wszystkie hosty serwerów/vSphere Vcenter, które są toohello skojarzone serwerem konfiguracji.

### <a name="delete-hello-configuration-server-from-azure-portal"></a>Usuń powitania serwera konfiguracji z portalu Azure
1. W portalu Azure Przejdź zbyt**infrastruktura usługi Site Recovery** > **serwery konfiguracji** hello magazynu menu.
2. Kliknij przycisk powitania serwera konfiguracji, które mają toodecommission.
3. Na stronie szczegółów hello konfiguracji serwera kliknij przycisk Usuń hello.

  ![Usuwanie konfiguracji serwera](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. Kliknij przycisk **tak** tooconfirm hello usunięcia powitania serwera.

  >[!WARNING]
  Jeśli masz maszyny wirtualne, zasady replikacji lub hostów serwerów/vSphere vCenter skojarzone z tym serwerem konfiguracji, nie można usunąć serwera hello. Przed podjęciem próby toodelete hello magazynu, należy usunąć te jednostki.

### <a name="uninstall-hello-configuration-server-software-and-its-dependencies"></a>Odinstaluj powitania serwera konfiguracji oprogramowania i jego zależności
  > [!TIP]
  Jeśli planujesz ponownie hello tooreuse konfiguracji serwera z usługą Azure Site Recovery, następnie można pominąć toostep 4 bezpośrednio

1. Zaloguj się na toohello serwer konfiguracji jako Administrator.
2. Otwórz Panel sterowania > Program > Odinstaluj programy
3. Odinstaluj programy hello w hello w następującej kolejności:
  * Agent usług Microsoft Azure Recovery Services
  * Microsoft Azure Site odzyskiwania mobilności usługi/główny serwer docelowy
  * Dostawcy usługi Microsoft Azure Site Recovery
  * Serwer procesu/serwera konfiguracji odzyskiwania witryny Microsoft Azure
  * Microsoft Azure Site odzyskiwania konfiguracji serwera zależności
  * Serwer MySQL 5,5
4. Uruchom następujące polecenie z hello i wiersza polecenia administratora.
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a>Odnów certyfikaty Layer(SSL) SSL serwera konfiguracji
powitania serwera konfiguracji ma wbudowane serwer sieci Web, która organizuje działania hello hello usługi mobilności serwerów procesu i docelowego elementu głównego serwery połączone toohello serwera konfiguracji. Serwer konfiguracji Hello serwer sieci Web używa tooauthenticate certyfikatu SSL klientów. Ten certyfikat ma okres ważności trzech lat i mogą być odnawiane w dowolnej chwili za pomocą hello następujące metody:

> [!WARNING]
Okresu ważności certyfikatu można wykonywać tylko w wersji 9.4.XXXX. X lub nowszej. Uaktualnij wszystkie hello składniki usługi Azure Site Recovery (serwer konfiguracji, serwer przetwarzania, głównego serwera docelowego, usługa mobilności) przed rozpoczęciem hello odnowić certyfikaty w przepływie pracy.

1. Na hello portalu Azure, przejdź tooyour magazynu > infrastruktura usługi Site Recovery > serwer konfiguracji.
2. Kliknij serwer konfiguracji hello, dla których potrzebujesz toorenew hello certyfikat SSL do.
3. W obszarze hello kondycji serwera konfiguracji widać datę wygaśnięcia hello hello certyfikatu SSL.
4. Odnów certyfikat hello klikając hello **odnowić certyfikaty** akcji, jak pokazano w powitania po obrazu:

  ![Usuwanie konfiguracji serwera](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a>Secure Socket Layer ostrzeżenie o wygaśnięciu certyfikatu

> [!NOTE]
Witaj ważności certyfikatu SSL dla wszystkich instalacji, które wystąpiły przed maj 2016 ustawiono tooone roku. Wyświetlanie wyświetlane w portalu Azure hello powiadomienia o wygasaniu certyfikatów zostały uruchomione.

1. Jeśli certyfikat SSL serwera konfiguracji hello mają tooexpire w hello przyszłych dwóch miesięcy, usługa hello jest uruchamiana powiadamiania użytkowników za pośrednictwem hello portalu Azure i poczty e-mail (należy toobe subskrybowane tooAzure usługi Site Recovery powiadomienia). Możesz uruchomić wyświetlany na stronie zasobów magazynu hello transparencie powiadomienia.

  ![certyfikat powiadomień](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. Kliknij przycisk hello transparent tooget dodatkowe szczegóły dotyczące hello okresu ważności certyfikatu.

  ![Szczegóły certyfikatu](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  Jeśli zamiast **odnowić teraz** przycisk widzisz **Uaktualnij teraz** przycisku. Oznacza to, czy niektóre składniki w danym środowisku, które nie zostały jeszcze uaktualniony too9.4.xxxx.x lub nowszym.

## <a name="sizing-requirements-for-a-configuration-server"></a>Ustawianie rozmiaru wymagania dotyczące serwera konfiguracji

| **PROCESOR CPU** | **Pamięci** | **Rozmiar pamięci podręcznej dysku** | **Częstotliwość zmian danych** | **Chronione maszyny** |
| --- | --- | --- | --- | --- |
| 8 Vcpu (2 sockets * 4 rdzenie @ 2,5 GHz) |16 GB |300 GB |500 GB lub mniej |Replikowanie maszyn mniej niż 100. |
| 12 Vcpu (2 sockets * 6 rdzeni @ 2,5 GHz) |18 GB |600 GB |TB too1 500 GB |Replikują między 100 150 maszyn. |
| 16 Vcpu (2 sockets * 8 rdzeni @ 2,5 GHz) |32 GB |1 TB |1 TB too2 TB |Replikują między 150 – 200 maszyn. |

  >[!TIP]
  Jeśli codziennych zmian ilości danych przekracza 2 TB, lub planujesz tooreplicate ponad 200 maszyn wirtualnych, zalecane jest toodeploy procesu dodatkowe serwery tooload saldo hello ruch związany z replikacją. Dowiedz się więcej na temat sposobu serwery toodeploy proces skalowania w poziomie.


## <a name="common-issues"></a>Typowe problemy
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
