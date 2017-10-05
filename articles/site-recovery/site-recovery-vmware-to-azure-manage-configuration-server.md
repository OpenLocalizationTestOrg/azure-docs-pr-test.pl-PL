---
title: " Zarządzanie serwerem konfiguracji w usłudze Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób i zarządzanie serwerem konfiguracji."
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
ms.openlocfilehash: 36da8c7d0f3ace194522e5288f26069cf46d470e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-configuration-server"></a>Zarządzanie serwerem konfiguracji

Serwer konfiguracji pełni funkcję koordynatora między usługi Site Recovery i infrastruktury lokalnej. W tym artykule opisano, jak można skonfigurować, skonfigurować i zarządzać serwerem konfiguracji.

## <a name="prerequisites"></a>Wymagania wstępne
Poniżej przedstawiono minimalne wymagania dotyczące sprzętu, oprogramowania i konfiguracji sieci wymagane do skonfigurowania serwera konfiguracji.

> [!NOTE]
> [Planowanie pojemności](site-recovery-capacity-planner.md) jest to ważny krok, aby zapobiec wdrażaniu serwera konfiguracji z konfiguracją tego zestawy wymagań obciążenia. Przeczytaj więcej na temat [zmiany rozmiaru wymagania dotyczące serwera konfiguracji](#sizing-requirements-for-a-configuration-server).

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-the-configuration-server-software"></a>Pobieranie oprogramowania serwera konfiguracji
1. Zaloguj się do portalu Azure i przejdź do magazynu usług odzyskiwania.
2. Przejdź do **infrastrukturę odzyskiwania lokacji** > **serwery konfiguracji** (w obszarze VMware i maszyn fizycznych).

  ![Dodaj stronę serwerów](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. Kliknij przycisk **+ serwery** przycisku.
4. Na **Dodaj serwer** kliknij przycisk pobierania, aby pobrać klucz rejestracji. Ten klucz jest wymagane podczas instalacji serwera konfiguracji, aby zarejestrować go z usługą Azure Site Recovery.
5. Kliknij przycisk **Pobierz Instalatora Microsoft Azure Site Recovery Unified** łącze, aby pobrać najnowszą wersję serwera konfiguracji.

  ![Strona pobierania](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  Można pobrać najnowszą wersję serwera konfiguracji bezpośrednio z [strony pobierania witryny Microsoft Download Center](http://aka.ms/unifiedsetup)

## <a name="installing-and-registering-a-configuration-server-from-gui"></a>Instalowanie i rejestrowanie konfiguracji serwer z graficznym interfejsem użytkownika
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a>Instalowanie i rejestrowanie serwera konfiguracji przy użyciu wiersza polecenia

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]
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
Parametr MySQLCredsFilePath przyjmuje pliku jako dane wejściowe. Utwórz plik w następującym formacie, a następnie przekaż go jako parametr wejściowy MySQLCredsFilePath.
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a>Utwórz plik konfiguracji ustawień serwera proxy
Parametr ProxySettingsFilePath przyjmuje pliku jako dane wejściowe. Utwórz plik w następującym formacie, a następnie przekaż go jako parametr wejściowy ProxySettingsFilePath.

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a>Modyfikowanie ustawień konfiguracji serwera proxy
1. Zaloguj się do serwera konfiguracji.
2. Uruchamianie cspsconfigtool.exe za pomocą skrótu na użytkownika.
3. Kliknij przycisk **rejestracji magazynu** kartę.
4. Pobranie nowego pliku magazynu rejestracji z portalu i udostępnij go jako dane wejściowe do narzędzia.

  ![serwer w przypadku konfiguracji rejestru](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. Podaj nowe szczegóły serwera Proxy i kliknij przycisk **zarejestrować** przycisku.
6. Otwórz okno poleceń programu PowerShell administratora.
7. Uruchom następujące polecenie
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  Jeśli masz dołączony do tego serwera konfiguracji serwerów proces skalowania w poziomie należy [Popraw ustawienia serwera proxy na wszystkich serwerach proces skalowania w poziomie](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) w danym wdrożeniu.

## <a name="re-register-a-configuration-server-with-the-same-recovery-services-vault"></a>Zarejestruj ponownie serwer konfiguracji z tego samego magazynu usług odzyskiwania
  1. Zaloguj się do serwera konfiguracji.
  2. Uruchom cspsconfigtool.exe za pomocą skrótu na pulpicie.
  3. Kliknij przycisk **rejestracji magazynu** kartę.
  4. Pobranie nowego pliku rejestracji z portalu i udostępnij go jako dane wejściowe do narzędzia.
        ![serwer w przypadku konfiguracji rejestru](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
  5. Podaj szczegóły serwera Proxy, a następnie kliknij przycisk **zarejestrować** przycisku.  
  6. Otwórz okno poleceń programu PowerShell administratora.
  7. Uruchom następujące polecenie

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  Jeśli masz dołączony do tego serwera konfiguracji serwerów proces skalowania w poziomie należy [ponownie zarejestrować serwery proces skalowania w poziomie](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) w danym wdrożeniu.

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a>Rejestrowanie serwera konfiguracji w innym magazynie usług odzyskiwania.
1. Zaloguj się do serwera konfiguracji.
2. z wiersza polecenia z uprawnieniami administratora uruchom polecenie

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. Uruchamianie cspsconfigtool.exe za pomocą skrótu na użytkownika.
4. Kliknij przycisk **rejestracji magazynu** kartę.
5. Pobranie nowego pliku rejestracji z portalu i udostępnij go jako dane wejściowe do narzędzia.

    ![serwer w przypadku konfiguracji rejestru](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. Podaj szczegóły serwera Proxy, a następnie kliknij przycisk **zarejestrować** przycisku.  
7. Otwórz okno poleceń programu PowerShell administratora.
8. Uruchom następujące polecenie
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a>Wycofanie z eksploatacji serwera konfiguracji
Upewnij się przed rozpoczęciem likwidowania serwera konfiguracji.
1. Wyłącz ochronę dla wszystkich maszyn wirtualnych na tym serwerze konfiguracji.
2. Usuń skojarzenie wszystkich zasad replikacji z serwera konfiguracji.
3. Usuń wszystkie hosty serwerów/vSphere Vcenter, które są skojarzone z serwerem konfiguracji.

### <a name="delete-the-configuration-server-from-azure-portal"></a>Usuń serwer konfiguracji z portalu Azure
1. W portalu Azure, przejdź do **infrastruktura usługi Site Recovery** > **serwery konfiguracji** w menu magazynu.
2. Kliknij serwer konfiguracji, który ma zostać zlikwidowany.
3. Na stronie Szczegóły serwera konfiguracji kliknij przycisk Usuń.

  ![Usuwanie konfiguracji serwera](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. Kliknij przycisk **tak** o potwierdzenie usunięcia serwera.

  >[!WARNING]
  Jeśli masz maszyny wirtualne, zasady replikacji lub hostów serwerów/vSphere vCenter skojarzone z tym serwerem konfiguracji, nie można usunąć serwera. Przed usunięciem magazynu, należy usunąć te jednostki.

### <a name="uninstall-the-configuration-server-software-and-its-dependencies"></a>Odinstaluj oprogramowanie serwera konfiguracji i jego zależności
  > [!TIP]
  Jeśli planujesz ponowne serwerze konfiguracji z usługą Azure Site Recovery, następnie można przejść do kroku 4 bezpośrednio

1. Zaloguj się jako Administrator serwera konfiguracji.
2. Otwórz Panel sterowania > Program > Odinstaluj programy
3. Należy odinstalować te programy w następującej kolejności:
  * Agent usług Microsoft Azure Recovery Services
  * Microsoft Azure Site odzyskiwania mobilności usługi/główny serwer docelowy
  * Dostawcy usługi Microsoft Azure Site Recovery
  * Serwer procesu/serwera konfiguracji odzyskiwania witryny Microsoft Azure
  * Microsoft Azure Site odzyskiwania konfiguracji serwera zależności
  * Serwer MySQL 5,5
4. Uruchom następujące polecenie z i wiersza polecenia administratora.
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a>Odnów certyfikaty Layer(SSL) SSL serwera konfiguracji
Serwer konfiguracji ma wbudowane serwer sieci Web, która organizuje działania serwerów usługi mobilności, serwerów przetwarzania i główny cel, połączenie z serwerem konfiguracji. Serwer konfiguracji serwer sieci Web używa certyfikatu SSL do uwierzytelniania klientów. Ten certyfikat ma upływie trzech lat i mogą być odnawiane w dowolnej chwili za pomocą następujących metod:

> [!WARNING]
Okresu ważności certyfikatu można wykonywać tylko w wersji 9.4.XXXX. X lub nowszej. Uaktualnij wszystkie składniki usługi Azure Site Recovery (serwer konfiguracji, serwer przetwarzania, głównego serwera docelowego, usługa mobilności) przed rozpoczęciem odnowić certyfikaty przepływ pracy.

1. W portalu Azure, przejdź do magazynu > infrastruktura usługi Site Recovery > serwer konfiguracji.
2. Kliknij serwer konfiguracji, dla którego należy odnowić certyfikat protokołu SSL.
3. W obszarze kondycji serwera konfiguracji można zobaczyć datę wygaśnięcia certyfikatu SSL.
4. Odnów certyfikat, klikając **odnowić certyfikaty** akcji, jak pokazano na poniższej ilustracji:

  ![Usuwanie konfiguracji serwera](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a>Secure Socket Layer ostrzeżenie o wygaśnięciu certyfikatu

> [!NOTE]
Ważność certyfikatu protokołu SSL dla wszystkich instalacji, które wystąpiły przed maj 2016 została ustawiona na jeden rok. Rozpoczęto wyświetlać powiadomienia o wygasaniu certyfikatów wyświetlane w portalu Azure.

1. Jeśli certyfikat SSL serwera konfiguracji jest wkrótce wygaśnie w ciągu przyszłych dwóch miesięcy, Usługa uruchamia powiadamianie użytkowników przy użyciu portalu Azure i poczty e-mail (należy do subskrypcji powiadomień usługi Azure Site Recovery). Możesz uruchomić wyświetlanie transparencie powiadomienia na stronie zasobów magazynu.

  ![certyfikat powiadomień](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. Kliknij przycisk transparentu, aby uzyskać więcej informacji o wygaśnięciu certyfikatu.

  ![Szczegóły certyfikatu](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  Jeśli zamiast **odnowić teraz** przycisk widzisz **Uaktualnij teraz** przycisku. Oznacza to, że są niektóre składniki w danym środowisku, które nie zostały jeszcze uaktualnione do 9.4.xxxx.x lub nowszej wersji.

## <a name="sizing-requirements-for-a-configuration-server"></a>Ustawianie rozmiaru wymagania dotyczące serwera konfiguracji

| **PROCESOR CPU** | **Pamięci** | **Rozmiar pamięci podręcznej dysku** | **Częstotliwość zmian danych** | **Chronione maszyny** |
| --- | --- | --- | --- | --- |
| 8 Vcpu (2 sockets * 4 rdzenie @ 2,5 GHz) |16 GB |300 GB |500 GB lub mniej |Replikowanie maszyn mniej niż 100. |
| 12 Vcpu (2 sockets * 6 rdzeni @ 2,5 GHz) |18 GB |600 GB |500 GB do 1 TB |Replikują między 100 150 maszyn. |
| 16 Vcpu (2 sockets * 8 rdzeni @ 2,5 GHz) |32 GB |1 TB |1 TB do 2 TB |Replikują między 150 – 200 maszyn. |

  >[!TIP]
  Jeśli codziennych zmian ilości danych przekracza 2 TB lub planowana jest replikacja ponad 200 maszyn wirtualnych, zalecane jest wdrażanie serwerów dodatkowych procesów na potrzeby ruchu związanego z replikacją równoważenia obciążenia. Dowiedz się więcej na temat sposobu wdrażania proces skalowania w poziomie serwery.


## <a name="common-issues"></a>Typowe problemy
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
