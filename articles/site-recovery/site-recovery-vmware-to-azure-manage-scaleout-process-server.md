---
title: " Zarządzanie serwerem proces skalowania w poziomie w usłudze Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tooset Konfigurowanie i zarządzanie serwerem proces skalowania w poziomie w usłudze Azure Site Recovery."
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
ms.openlocfilehash: 3d72f9c2c7014a4ff2fa2af168aa55ad1452eae5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-scale-out-process-server"></a>Zarządzanie serwerem proces skalowania w poziomie

Serwer przetwarzania skalowalnego w poziomie działa jako koordynatora do transferu danych między hello usługi Site Recovery i infrastruktury lokalnej. W tym artykule opisano, jak można skonfigurować, konfigurowania i zarządzania serwera przetwarzania skalowalnego w poziomie.

## <a name="prerequisites"></a>Wymagania wstępne
następujące Hello są zalecane hello sprzętu, oprogramowania i sieci tooset wymagana jest konfiguracja serwera proces skalowania w poziomie.

> [!NOTE]
> [Planowanie pojemności](site-recovery-capacity-planner.md) tooensure ważnym krokiem wdrażania hello skalowalnego w poziomie serwera przetwarzania konfiguracji z tego pakietu jest wymagań obciążenia. Przeczytaj więcej na temat [skalowanie właściwości dla skalowalnego w poziomie serwera procesu](#sizing-requirements-for-a-configuration-server).

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-scale-out-process-server-software"></a>Pobieranie oprogramowania skalowalnego w poziomie serwera przetwarzania hello
1. Zaloguj się na toohello Azure tooyour portalu i przeglądania magazynu usług odzyskiwania.
2. Przeglądaj zbyt**infrastruktura usługi Site Recovery** > **serwery konfiguracji** (w przypadku VMware i maszyn fizycznych).
3. Wybierz z konfiguracji serwera toodrill w dół do strony szczegółów hello konfiguracji serwera.
4. Kliknij przycisk hello **+ serwera przetwarzania** przycisku.
5. W hello **proces dodawania serwera** wybierz pozycję **wdrażanie skalowalnego w poziomie proces serwera lokalnego** opcję hello **wybierz miejsce toodeploy serwera przetwarzania** listy rozwijanej.

  ![Dodaj stronę serwerów](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. Kliknij przycisk hello **hello pobierania Instalatora Microsoft Azure Site Recovery Unified** łącze toodownload hello najnowszej wersji hello skalowalnego w poziomie serwera procesu instalacji.

  > [!WARNING]
  Witaj wersji serwera przetwarzania skalowalnego w poziomie powinny być takie same tooor wcześniejsza niż wersja serwera konfiguracji hello w swoim środowisku. Zgodność wersji tooensure prosty sposób jest toouse hello tego samego bitów Instalator że używane tooinstall lub zaktualizowania serwera konfiguracji.

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a>Instalowanie i rejestrowanie serwera przetwarzania skalowalnego w poziomie z graficznym interfejsem użytkownika
Jeśli masz tooscale limit wdrożenia ponad 200 maszyn źródłowych lub całkowity dzienny churn — liczba więcej niż 2 TB, należy procesu dodatkowe serwery toohandle hello ruchu woluminu.

Sprawdź hello [rozmiaru zalecenia dotyczące serwerów procesu](#size-recommendations-for-the-process-server), a następnie wykonaj te instrukcje tooset hello procesu serwera. Po skonfigurowaniu serwera hello, migracja toouse maszyny źródłowej go.

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a>Instalowanie i rejestrowanie serwera proces skalowania w poziomie przy użyciu wiersza polecenia

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a>Przykładowe zastosowanie
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a>Serwer przetwarzania skalowalnego w poziomie Instalator argumenty wiersza polecenia.
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a>Utwórz plik konfiguracji ustawień serwera proxy
Parametr ProxySettingsFilePath przyjmuje pliku jako dane wejściowe. Tworzenie pliku przy użyciu hello następujący format i przekaż go jako parametr wejściowy ProxySettingsFilePath.
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a>Modyfikowanie ustawień serwera proxy dla serwera przetwarzania skalowalnego w poziomie
1. Zaloguj się do serwera przetwarzania skalowalnego w poziomie.
2. Otwórz okno poleceń programu PowerShell administratora.
3. Uruchom następujące polecenie hello
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. Następnie przeglądanie katalogu toohello **%PROGRAMDATA%\ASR\Agent** i hello uruchom następujące polecenie
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a>Ponowne rejestrowanie serwera proces skalowania w poziomie
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* Następnie otwórz wiersz polecenia administratora.
* Przeglądanie katalogu toohello **%PROGRAMDATA%\ASR\Agent** i uruchom polecenie hello

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a>Uaktualnianie serwera proces skalowania w poziomie
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a>Wycofanie z eksploatacji serwera proces skalowania w poziomie
1. Upewnij się, że:
  - Stan połączenia serwera konfiguracji jest pokazywana jako **połączony** w hello portalu Azure
  - Serwer przetwarzania jest nadal toocommunicate z powitania serwera konfiguracji.
2. Zaloguj się jako administrator toohello serwera przetwarzania
3. Otwórz Panel sterowania > Program > Odinstaluj programy
4. Odinstaluj programy hello w sekwencji hello podane po:
  * Serwer procesu/serwera konfiguracji odzyskiwania witryny Microsoft Azure
  * Microsoft Azure Site odzyskiwania konfiguracji serwera zależności
  * Agent usług Microsoft Azure Recovery Services

Może upłynąć minut up too15 tooreflect usunięcia serwera przetwarzania hello w hello portalu Azure.

  > [!NOTE]
  Jeśli serwer przetwarzania hello jest toocommunicate z hello konfiguracji serwera (stan połączenia w portalu jest odłączony), wówczas należy toofollow hello następujące kroki toopurge go z powitania serwera konfiguracji.

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a>Wyrejestrowywanie odłączony serwer proces skalowania w poziomie z serwera konfiguracji

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a>Ustawianie rozmiaru wymagania dotyczące serwera przetwarzania skalowalnego w poziomie

| **Serwer przetwarzania dodatkowe** | **Rozmiar pamięci podręcznej dysku** | **Częstotliwość zmian danych** | **Chronione maszyny** |
| --- | --- | --- | --- |
|4 Vcpu (2 sockets * 2 rdzenie @ 2,5 GHz), 8 GB pamięci |300 GB |250 GB lub mniej |Replikowanie maszyn 85 lub mniej. |
|8 Vcpu (2 sockets * 4 rdzenie @ 2,5 GHz), 12 GB pamięci RAM |600 GB |TB too1 250 GB |Replikują między 85 150 maszyny. |
|12 Vcpu (2 sockets * 6 rdzeni @ 2,5 GHz) 24 GB pamięci |1 TB |1 TB too2 TB |Replikują między 150 225 komputerów. |
