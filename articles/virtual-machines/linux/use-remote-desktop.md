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
# <a name="install-and-configure-remote-desktop-tooconnect-tooa-linux-vm-in-azure"></a><span data-ttu-id="ad23b-103">Instalowanie i konfigurowanie pulpitu zdalnego tooconnect tooa maszyny Wirtualnej systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="ad23b-103">Install and configure Remote Desktop tooconnect tooa Linux VM in Azure</span></span>
<span data-ttu-id="ad23b-104">Maszyn wirtualnych systemu Linux (VM) na platformie Azure zwykle są zarządzane z wiersza polecenia hello przy użyciu połączenia bezpiecznej powłoki (SSH).</span><span class="sxs-lookup"><span data-stu-id="ad23b-104">Linux virtual machines (VMs) in Azure are usually managed from hello command line using a secure shell (SSH) connection.</span></span> <span data-ttu-id="ad23b-105">Gdy nowy tooLinux lub scenariuszach rozwiązywania problemów z szybkiego hello pulpitu zdalnego mogą być łatwiejsze.</span><span class="sxs-lookup"><span data-stu-id="ad23b-105">When new tooLinux, or for quick troubleshooting scenarios, hello use of remote desktop may be easier.</span></span> <span data-ttu-id="ad23b-106">Ten sposób artykuł szczegóły tooinstall i skonfigurować środowisko pulpitu ([xfce](https://www.xfce.org)) i pulpitu zdalnego ([xrdp](http://www.xrdp.org)) dla maszyny Wirtualnej systemu Linux przy użyciu modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="ad23b-106">This article details how tooinstall and configure a desktop environment ([xfce](https://www.xfce.org)) and remote desktop ([xrdp](http://www.xrdp.org)) for your Linux VM using hello Resource Manager deployment model.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="ad23b-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ad23b-107">Prerequisites</span></span>
<span data-ttu-id="ad23b-108">W tym artykule wymaga istniejącej maszyny Wirtualnej systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ad23b-108">This article requires an existing Linux VM in Azure.</span></span> <span data-ttu-id="ad23b-109">Toocreate maszyny Wirtualnej, należy użyć jednej z następujących metod hello:</span><span class="sxs-lookup"><span data-stu-id="ad23b-109">If you need toocreate a VM, use one of hello following methods:</span></span>

- <span data-ttu-id="ad23b-110">Witaj [2.0 interfejsu wiersza polecenia platformy Azure](quick-create-cli.md)</span><span class="sxs-lookup"><span data-stu-id="ad23b-110">hello [Azure CLI 2.0](quick-create-cli.md)</span></span>
- <span data-ttu-id="ad23b-111">Witaj [portalu Azure](quick-create-portal.md)</span><span class="sxs-lookup"><span data-stu-id="ad23b-111">hello [Azure portal](quick-create-portal.md)</span></span>


## <a name="install-a-desktop-environment-on-your-linux-vm"></a><span data-ttu-id="ad23b-112">Zainstaluj środowisko pulpitu na maszynie Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="ad23b-112">Install a desktop environment on your Linux VM</span></span>
<span data-ttu-id="ad23b-113">Większość maszyn wirtualnych systemu Linux na platformie Azure nie masz środowisko pulpitu instalowane domyślnie.</span><span class="sxs-lookup"><span data-stu-id="ad23b-113">Most Linux VMs in Azure do not have a desktop environment installed by default.</span></span> <span data-ttu-id="ad23b-114">Maszyn wirtualnych systemu Linux są często zarządzane za pomocą połączeń SSH, a nie środowiska pulpitu.</span><span class="sxs-lookup"><span data-stu-id="ad23b-114">Linux VMs are commonly managed using SSH connections rather than a desktop environment.</span></span> <span data-ttu-id="ad23b-115">Istnieją różne środowiska pulpitu w systemie Linux, możesz wybrać następujące opcje.</span><span class="sxs-lookup"><span data-stu-id="ad23b-115">There are various desktop environments in Linux that you can choose.</span></span> <span data-ttu-id="ad23b-116">W zależności od wybranych środowiska pulpitu może korzystać z jednego too2 GB miejsca na dysku i zająć 5 tooinstall minut too10 i skonfiguruj wszystkie hello wymagane pakiety.</span><span class="sxs-lookup"><span data-stu-id="ad23b-116">Depending on your choice of desktop environment, it may consume one too2 GB of disk space, and take 5 too10 minutes tooinstall and configure all hello required packages.</span></span>

<span data-ttu-id="ad23b-117">Witaj poniższym przykładzie przedstawiono instalację hello lightweight [xfce4](https://www.xfce.org/) środowiska pulpitu na maszynie Wirtualnej systemu Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="ad23b-117">hello following example installs hello lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM.</span></span> <span data-ttu-id="ad23b-118">Polecenia dla innych dystrybucje się nieco różnić (Użyj `yum` tooinstall w systemie Red Hat Enterprise Linux i skonfigurować odpowiednie `selinux` reguły lub użyj `zypper` tooinstall na SUSE, na przykład).</span><span class="sxs-lookup"><span data-stu-id="ad23b-118">Commands for other distributions vary slightly (use `yum` tooinstall on Red Hat Enterprise Linux and configure appropriate `selinux` rules, or use `zypper` tooinstall on SUSE, for example).</span></span>

<span data-ttu-id="ad23b-119">Najpierw tooyour SSH maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad23b-119">First, SSH tooyour VM.</span></span> <span data-ttu-id="ad23b-120">Witaj poniższy przykład łączy toohello maszyny Wirtualnej o nazwie *myvm.westus.cloudapp.azure.com* z nazwą użytkownika hello z *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="ad23b-120">hello following example connects toohello VM named *myvm.westus.cloudapp.azure.com* with hello username of *azureuser*:</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="ad23b-121">Jeśli używasz systemu Windows i uzyskać więcej informacji o korzystaniu z protokołu SSH, zobacz [jak klucze toouse SSH z systemem Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="ad23b-121">If you are using Windows and need more information on using SSH, see [How toouse SSH keys with Windows](ssh-from-windows.md).</span></span>

<span data-ttu-id="ad23b-122">Następnie zainstaluj przy użyciu xfce `apt` w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ad23b-122">Next, install xfce using `apt` as follows:</span></span>

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a><span data-ttu-id="ad23b-123">Instalowanie i konfigurowanie serwera usług pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="ad23b-123">Install and configure a remote desktop server</span></span>
<span data-ttu-id="ad23b-124">Teraz, gdy masz środowisko pulpitu instalowane, skonfiguruj toolisten usługi usług pulpitu zdalnego dla połączeń przychodzących.</span><span class="sxs-lookup"><span data-stu-id="ad23b-124">Now that you have a desktop environment installed, configure a remote desktop service toolisten for incoming connections.</span></span> <span data-ttu-id="ad23b-125">[xrdp](http://xrdp.org) jest serwer protokołu RDP (Remote Desktop) typu open source, który jest dostępny na większości dystrybucje systemu Linux i dobrze działa z xfce.</span><span class="sxs-lookup"><span data-stu-id="ad23b-125">[xrdp](http://xrdp.org) is an open source Remote Desktop Protocol (RDP) server that is available on most Linux distributions, and works well with xfce.</span></span> <span data-ttu-id="ad23b-126">Zainstaluj xrdp na maszynie Wirtualnej systemu Ubuntu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ad23b-126">Install xrdp on your Ubuntu VM as follows:</span></span>

```bash
sudo apt-get install xrdp
```

<span data-ttu-id="ad23b-127">Poinformuj xrdp jakie toouse środowiska pulpitu podczas uruchamiania sesji.</span><span class="sxs-lookup"><span data-stu-id="ad23b-127">Tell xrdp what desktop environment toouse when you start your session.</span></span> <span data-ttu-id="ad23b-128">Skonfiguruj xrdp toouse xfce jako środowisko pulpitu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ad23b-128">Configure xrdp toouse xfce as your desktop environment as follows:</span></span>

```bash
echo xfce4-session >~/.xsession
```

<span data-ttu-id="ad23b-129">Ponownie uruchomić usługę hello xrdp efekt tootake zmiany hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ad23b-129">Restart hello xrdp service for hello changes tootake effect as follows:</span></span>

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a><span data-ttu-id="ad23b-130">Ustaw hasło konta użytkownika lokalnego</span><span class="sxs-lookup"><span data-stu-id="ad23b-130">Set a local user account password</span></span>
<span data-ttu-id="ad23b-131">Jeśli hasło zostało utworzone dla tego konta użytkownika, po utworzeniu maszyny Wirtualnej, Pomiń ten krok.</span><span class="sxs-lookup"><span data-stu-id="ad23b-131">If you created a password for your user account when you created your VM, skip this step.</span></span> <span data-ttu-id="ad23b-132">Jeśli tylko uwierzytelniania klucza SSH i nie mają hasła konta lokalnego ustawiona, określ hasło, zanim użycie xrdp toolog w tooyour maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad23b-132">If you only use SSH key authentication and do not have a local account password set, specify a password before you use xrdp toolog in tooyour VM.</span></span> <span data-ttu-id="ad23b-133">xrdp nie może zaakceptować kluczy SSH do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="ad23b-133">xrdp cannot accept SSH keys for authentication.</span></span> <span data-ttu-id="ad23b-134">Witaj poniższy przykład określa hasło dla konta użytkownika hello *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="ad23b-134">hello following example specifies a password for hello user account *azureuser*:</span></span>

```bash
sudo passwd azureuser
```

> [!NOTE]
> <span data-ttu-id="ad23b-135">Określenie hasła nie powoduje aktualizacji logowania do hasła SSHD konfiguracji toopermit, jeśli obecnie nie.</span><span class="sxs-lookup"><span data-stu-id="ad23b-135">Specifying a password does not update your SSHD configuration toopermit password logins if it currently does not.</span></span> <span data-ttu-id="ad23b-136">Z punktu widzenia zabezpieczeń mogą ma tooyour tooconnect maszyny Wirtualnej z tunelu SSH przy użyciu uwierzytelniania opartego na kluczach i połączyć z tooxrdp.</span><span class="sxs-lookup"><span data-stu-id="ad23b-136">From a security perspective, you may wish tooconnect tooyour VM with an SSH tunnel using key-based authentication and then connect tooxrdp.</span></span> <span data-ttu-id="ad23b-137">Jeśli tak, Pomiń powitania po kroku dotyczące tworzenia zabezpieczeń grupy reguł tooallow zdalnego pulpitu ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="ad23b-137">If so, skip hello following step on creating a network security group rule tooallow remote desktop traffic.</span></span>


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a><span data-ttu-id="ad23b-138">Tworzenie reguły grupy zabezpieczeń sieci dla ruchu pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="ad23b-138">Create a Network Security Group rule for Remote Desktop traffic</span></span>
<span data-ttu-id="ad23b-139">tooallow pulpitu zdalnego ruchu tooreach maszyny Wirtualnej systemu Linux, reguły grupy zabezpieczeń sieci musi utworzyć toobe umożliwiająca TCP na porcie 3389 tooreach maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad23b-139">tooallow Remote Desktop traffic tooreach your Linux VM, a network security group rule needs toobe created that allows TCP on port 3389 tooreach your VM.</span></span> <span data-ttu-id="ad23b-140">Aby uzyskać więcej informacji dotyczących zasad grupy zabezpieczeń sieci, zobacz [co to jest grupa zabezpieczeń sieci?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="ad23b-140">For more information about network security group rules, see [What is a Network Security Group?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span> <span data-ttu-id="ad23b-141">Możesz również [Użyj hello Azure toocreate portalu reguły grupy zabezpieczeń sieci](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ad23b-141">You can also [use hello Azure portal toocreate a network security group rule](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="ad23b-142">Hello następujące przykłady tworzenia reguły grupy zabezpieczeń sieci z [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create) o nazwie *myNetworkSecurityGroupRule* za*Zezwalaj* ruch na *tcp* portu *3389*.</span><span class="sxs-lookup"><span data-stu-id="ad23b-142">hello following examples create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) named *myNetworkSecurityGroupRule* too*allow* traffic on *tcp* port *3389*.</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a><span data-ttu-id="ad23b-143">Połączenie z maszyną Wirtualną systemu Linux za pomocą klienta usług pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="ad23b-143">Connect your Linux VM with a Remote Desktop client</span></span>
<span data-ttu-id="ad23b-144">Otwórz klienta pulpitu zdalnego lokalnego i połącz toohello adres IP lub nazwę DNS maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="ad23b-144">Open your local remote desktop client and connect toohello IP address or DNS name of your Linux VM.</span></span> <span data-ttu-id="ad23b-145">Wprowadź hello użytkownika i hasło dla konta użytkownika hello na maszynie Wirtualnej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ad23b-145">Enter hello username and password for hello user account on your VM as follows:</span></span>

![Połącz tooxrdp przy użyciu klienta pulpitu zdalnego](./media/use-remote-desktop/remote-desktop-client.png)

<span data-ttu-id="ad23b-147">Po uwierzytelnieniu środowiska pulpitu xfce hello obciążenia i wyglądać podobnie toohello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="ad23b-147">After authenticating, hello xfce desktop environment will load and look similar toohello following example:</span></span>

![xfce środowisko pulpitu za pośrednictwem xrdp](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a><span data-ttu-id="ad23b-149">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="ad23b-149">Troubleshoot</span></span>
<span data-ttu-id="ad23b-150">Jeśli nie możesz połączyć tooyour maszyny Wirtualnej systemu Linux przy użyciu klienta pulpitu zdalnego, należy użyć `netstat` na tooverify sieci maszyny Wirtualnej systemu Linux, nasłuchującej maszyny Wirtualnej dla połączeń protokołu RDP w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ad23b-150">If you cannot connect tooyour Linux VM using a Remote Desktop client, use `netstat` on your Linux VM tooverify that your VM is listening for RDP connections  as follows:</span></span>

```bash
sudo netstat -plnt | grep rdp
```

<span data-ttu-id="ad23b-151">powitania po przykładzie hello wirtualna nasłuchiwanie na porcie TCP 3389 zgodnie z oczekiwaniami:</span><span class="sxs-lookup"><span data-stu-id="ad23b-151">hello following example shows hello VM listening on TCP port 3389 as expected:</span></span>

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

<span data-ttu-id="ad23b-152">Jeśli nie nasłuchuje usługa xrdp hello, na maszynie Wirtualnej systemu Ubuntu Uruchom ponownie usługi hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ad23b-152">If hello xrdp service is not listening, on an Ubuntu VM restart hello service as follows:</span></span>

```bash
sudo service xrdp restart
```

<span data-ttu-id="ad23b-153">Przejrzyj dzienniki w */var/log*Thug na maszynie Wirtualnej systemu Ubuntu do oznaczenia jako toowhy hello usługa może nie odpowiadać.</span><span class="sxs-lookup"><span data-stu-id="ad23b-153">Review logs in */var/log*Thug  on your Ubuntu VM for indications as toowhy hello service may not be responding.</span></span> <span data-ttu-id="ad23b-154">Można również monitorować hello syslog podczas tooview próba połączenia pulpitu zdalnego błędy:</span><span class="sxs-lookup"><span data-stu-id="ad23b-154">You can also monitor hello syslog during a remote desktop connection attempt tooview any errors:</span></span>

```bash
tail -f /var/log/syslog
```

<span data-ttu-id="ad23b-155">Inne dystrybucje systemu Linux, takie jak Red Hat Enterprise Linux i SUSE mogą mieć różne sposoby toorestart usług i tooreview lokalizacji pliku dziennika alternatywny.</span><span class="sxs-lookup"><span data-stu-id="ad23b-155">Other Linux distributions such as Red Hat Enterprise Linux and SUSE may have different ways toorestart services and alternate log file locations tooreview.</span></span>

<span data-ttu-id="ad23b-156">Jeśli nie mają żadnych odpowiedzi na kliencie usług pulpitu zdalnego i nie ma żadnych zdarzeń w dzienniku systemowym hello, to zachowanie wskazuje, że ruchu pulpitu zdalnego nie może nawiązać połączenie hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad23b-156">If you do not receive any response in your remote desktop client and do not see any events in hello system log, this behavior indicates that remote desktop traffic cannot reach hello VM.</span></span> <span data-ttu-id="ad23b-157">Zapoznaj się z sieci zabezpieczeń grupy reguł tooensure ma toopermit reguły TCP na porcie 3389.</span><span class="sxs-lookup"><span data-stu-id="ad23b-157">Review your network security group rules tooensure that you have a rule toopermit TCP on port 3389.</span></span> <span data-ttu-id="ad23b-158">Aby uzyskać więcej informacji, zobacz [Rozwiązywanie problemów z łącznością aplikacji](../windows/troubleshoot-app-connection.md).</span><span class="sxs-lookup"><span data-stu-id="ad23b-158">For more information, see [Troubleshoot application connectivity issues](../windows/troubleshoot-app-connection.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="ad23b-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ad23b-159">Next steps</span></span>
<span data-ttu-id="ad23b-160">Aby uzyskać więcej informacji na temat tworzenia i używania kluczy SSH z maszyn wirtualnych systemu Linux, zobacz [utworzyć SSH kluczy dla maszyn wirtualnych systemu Linux na platformie Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="ad23b-160">For more information about creating and using SSH keys with Linux VMs, see [Create SSH keys for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

<span data-ttu-id="ad23b-161">Aby uzyskać informacji o korzystaniu z protokołu SSH z systemu Windows, zobacz [jak klucze toouse SSH z systemem Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="ad23b-161">For information on using SSH from Windows, see [How toouse SSH keys with Windows](ssh-from-windows.md).</span></span>

