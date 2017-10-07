---
title: aaaUse pulpitu zdalnego tooa maszyny Wirtualnej systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooinstall i konfigurowanie pulpitu zdalnego (xrdp) tooconnect tooa maszyny Wirtualnej systemu Linux na platformie Azure za pomocą narzędzi graficznych"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: iainfou
ms.openlocfilehash: 64d30be101ceeb49fc05bb10293ad63db358efe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-remote-desktop-tooconnect-tooa-linux-vm-in-azure"></a>Instalowanie i konfigurowanie pulpitu zdalnego tooconnect tooa maszyny Wirtualnej systemu Linux na platformie Azure
Maszyn wirtualnych systemu Linux (VM) na platformie Azure zwykle są zarządzane z wiersza polecenia hello przy użyciu połączenia bezpiecznej powłoki (SSH). Gdy nowy tooLinux lub scenariuszach rozwiązywania problemów z szybkiego hello pulpitu zdalnego mogą być łatwiejsze. Ten sposób artykuł szczegóły tooinstall i skonfigurować środowisko pulpitu ([xfce](https://www.xfce.org)) i pulpitu zdalnego ([xrdp](http://www.xrdp.org)) dla maszyny Wirtualnej systemu Linux przy użyciu modelu wdrażania usługi Resource Manager hello.


## <a name="prerequisites"></a>Wymagania wstępne
W tym artykule wymaga istniejącej maszyny Wirtualnej systemu Linux na platformie Azure. Toocreate maszyny Wirtualnej, należy użyć jednej z następujących metod hello:

- Witaj [2.0 interfejsu wiersza polecenia platformy Azure](quick-create-cli.md)
- Witaj [portalu Azure](quick-create-portal.md)


## <a name="install-a-desktop-environment-on-your-linux-vm"></a>Zainstaluj środowisko pulpitu na maszynie Wirtualnej systemu Linux
Większość maszyn wirtualnych systemu Linux na platformie Azure nie masz środowisko pulpitu instalowane domyślnie. Maszyn wirtualnych systemu Linux są często zarządzane za pomocą połączeń SSH, a nie środowiska pulpitu. Istnieją różne środowiska pulpitu w systemie Linux, możesz wybrać następujące opcje. W zależności od wybranych środowiska pulpitu może korzystać z jednego too2 GB miejsca na dysku i zająć 5 tooinstall minut too10 i skonfiguruj wszystkie hello wymagane pakiety.

Witaj poniższym przykładzie przedstawiono instalację hello lightweight [xfce4](https://www.xfce.org/) środowiska pulpitu na maszynie Wirtualnej systemu Ubuntu. Polecenia dla innych dystrybucje się nieco różnić (Użyj `yum` tooinstall w systemie Red Hat Enterprise Linux i skonfigurować odpowiednie `selinux` reguły lub użyj `zypper` tooinstall na SUSE, na przykład).

Najpierw tooyour SSH maszyny Wirtualnej. Witaj poniższy przykład łączy toohello maszyny Wirtualnej o nazwie *myvm.westus.cloudapp.azure.com* z nazwą użytkownika hello z *azureuser*:

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

Jeśli używasz systemu Windows i uzyskać więcej informacji o korzystaniu z protokołu SSH, zobacz [jak klucze toouse SSH z systemem Windows](ssh-from-windows.md).

Następnie zainstaluj przy użyciu xfce `apt` w następujący sposób:

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a>Instalowanie i konfigurowanie serwera usług pulpitu zdalnego
Teraz, gdy masz środowisko pulpitu instalowane, skonfiguruj toolisten usługi usług pulpitu zdalnego dla połączeń przychodzących. [xrdp](http://xrdp.org) jest serwer protokołu RDP (Remote Desktop) typu open source, który jest dostępny na większości dystrybucje systemu Linux i dobrze działa z xfce. Zainstaluj xrdp na maszynie Wirtualnej systemu Ubuntu w następujący sposób:

```bash
sudo apt-get install xrdp
```

Poinformuj xrdp jakie toouse środowiska pulpitu podczas uruchamiania sesji. Skonfiguruj xrdp toouse xfce jako środowisko pulpitu w następujący sposób:

```bash
echo xfce4-session >~/.xsession
```

Ponownie uruchomić usługę hello xrdp efekt tootake zmiany hello w następujący sposób:

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a>Ustaw hasło konta użytkownika lokalnego
Jeśli hasło zostało utworzone dla tego konta użytkownika, po utworzeniu maszyny Wirtualnej, Pomiń ten krok. Jeśli tylko uwierzytelniania klucza SSH i nie mają hasła konta lokalnego ustawiona, określ hasło, zanim użycie xrdp toolog w tooyour maszyny Wirtualnej. xrdp nie może zaakceptować kluczy SSH do uwierzytelniania. Witaj poniższy przykład określa hasło dla konta użytkownika hello *azureuser*:

```bash
sudo passwd azureuser
```

> [!NOTE]
> Określenie hasła nie powoduje aktualizacji logowania do hasła SSHD konfiguracji toopermit, jeśli obecnie nie. Z punktu widzenia zabezpieczeń mogą ma tooyour tooconnect maszyny Wirtualnej z tunelu SSH przy użyciu uwierzytelniania opartego na kluczach i połączyć z tooxrdp. Jeśli tak, Pomiń powitania po kroku dotyczące tworzenia zabezpieczeń grupy reguł tooallow zdalnego pulpitu ruchu sieciowego.


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a>Tworzenie reguły grupy zabezpieczeń sieci dla ruchu pulpitu zdalnego
tooallow pulpitu zdalnego ruchu tooreach maszyny Wirtualnej systemu Linux, reguły grupy zabezpieczeń sieci musi utworzyć toobe umożliwiająca TCP na porcie 3389 tooreach maszyny Wirtualnej. Aby uzyskać więcej informacji dotyczących zasad grupy zabezpieczeń sieci, zobacz [co to jest grupa zabezpieczeń sieci?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Możesz również [Użyj hello Azure toocreate portalu reguły grupy zabezpieczeń sieci](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Hello następujące przykłady tworzenia reguły grupy zabezpieczeń sieci z [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create) o nazwie *myNetworkSecurityGroupRule* za*Zezwalaj* ruch na *tcp* portu *3389*.

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a>Połączenie z maszyną Wirtualną systemu Linux za pomocą klienta usług pulpitu zdalnego
Otwórz klienta pulpitu zdalnego lokalnego i połącz toohello adres IP lub nazwę DNS maszyny Wirtualnej systemu Linux. Wprowadź hello użytkownika i hasło dla konta użytkownika hello na maszynie Wirtualnej w następujący sposób:

![Połącz tooxrdp przy użyciu klienta pulpitu zdalnego](./media/use-remote-desktop/remote-desktop-client.png)

Po uwierzytelnieniu środowiska pulpitu xfce hello obciążenia i wyglądać podobnie toohello poniższy przykład:

![xfce środowisko pulpitu za pośrednictwem xrdp](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a>Rozwiązywanie problemów
Jeśli nie możesz połączyć tooyour maszyny Wirtualnej systemu Linux przy użyciu klienta pulpitu zdalnego, należy użyć `netstat` na tooverify sieci maszyny Wirtualnej systemu Linux, nasłuchującej maszyny Wirtualnej dla połączeń protokołu RDP w następujący sposób:

```bash
sudo netstat -plnt | grep rdp
```

powitania po przykładzie hello wirtualna nasłuchiwanie na porcie TCP 3389 zgodnie z oczekiwaniami:

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

Jeśli nie nasłuchuje usługa xrdp hello, na maszynie Wirtualnej systemu Ubuntu Uruchom ponownie usługi hello w następujący sposób:

```bash
sudo service xrdp restart
```

Przejrzyj dzienniki w */var/log*Thug na maszynie Wirtualnej systemu Ubuntu do oznaczenia jako toowhy hello usługa może nie odpowiadać. Można również monitorować hello syslog podczas tooview próba połączenia pulpitu zdalnego błędy:

```bash
tail -f /var/log/syslog
```

Inne dystrybucje systemu Linux, takie jak Red Hat Enterprise Linux i SUSE mogą mieć różne sposoby toorestart usług i tooreview lokalizacji pliku dziennika alternatywny.

Jeśli nie mają żadnych odpowiedzi na kliencie usług pulpitu zdalnego i nie ma żadnych zdarzeń w dzienniku systemowym hello, to zachowanie wskazuje, że ruchu pulpitu zdalnego nie może nawiązać połączenie hello maszyny Wirtualnej. Zapoznaj się z sieci zabezpieczeń grupy reguł tooensure ma toopermit reguły TCP na porcie 3389. Aby uzyskać więcej informacji, zobacz [Rozwiązywanie problemów z łącznością aplikacji](../windows/troubleshoot-app-connection.md).


## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat tworzenia i używania kluczy SSH z maszyn wirtualnych systemu Linux, zobacz [utworzyć SSH kluczy dla maszyn wirtualnych systemu Linux na platformie Azure](mac-create-ssh-keys.md).

Aby uzyskać informacji o korzystaniu z protokołu SSH z systemu Windows, zobacz [jak klucze toouse SSH z systemem Windows](ssh-from-windows.md).

