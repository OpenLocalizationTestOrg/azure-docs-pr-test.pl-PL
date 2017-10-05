---
title: "Za pomocą pulpitu zdalnego do maszyny Wirtualnej systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak instalowanie i konfigurowanie pulpitu zdalnego (xrdp), aby nawiązać połączenie Maszynę wirtualną systemu Linux na platformie Azure za pomocą narzędzi graficznych"
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
ms.openlocfilehash: d8d6130a270285c84c1dd057a3512cdeb39287f6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="install-and-configure-remote-desktop-to-connect-to-a-linux-vm-in-azure"></a><span data-ttu-id="e141d-103">Instalowanie i konfigurowanie pulpitu zdalnego, aby nawiązać połączenie Maszynę wirtualną systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="e141d-103">Install and configure Remote Desktop to connect to a Linux VM in Azure</span></span>
<span data-ttu-id="e141d-104">Maszyny wirtualne systemu Linux (VM) na platformie Azure zwykle są zarządzane z poziomu wiersza polecenia przy użyciu połączenia bezpiecznej powłoki (SSH).</span><span class="sxs-lookup"><span data-stu-id="e141d-104">Linux virtual machines (VMs) in Azure are usually managed from the command line using a secure shell (SSH) connection.</span></span> <span data-ttu-id="e141d-105">Gdy nowy, Linux lub szybkiego scenariuszach rozwiązywania problemów, użyj pulpitu zdalnego może być łatwiejsze.</span><span class="sxs-lookup"><span data-stu-id="e141d-105">When new to Linux, or for quick troubleshooting scenarios, the use of remote desktop may be easier.</span></span> <span data-ttu-id="e141d-106">W tym artykule szczegółowo przedstawiają, jak zainstalować i skonfigurować środowisko pulpitu ([xfce](https://www.xfce.org)) i pulpitu zdalnego ([xrdp](http://www.xrdp.org)) dla maszyny Wirtualnej systemu Linux przy użyciu modelu wdrażania Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="e141d-106">This article details how to install and configure a desktop environment ([xfce](https://www.xfce.org)) and remote desktop ([xrdp](http://www.xrdp.org)) for your Linux VM using the Resource Manager deployment model.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e141d-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e141d-107">Prerequisites</span></span>
<span data-ttu-id="e141d-108">W tym artykule wymaga istniejącej maszyny Wirtualnej systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e141d-108">This article requires an existing Linux VM in Azure.</span></span> <span data-ttu-id="e141d-109">Jeśli musisz utworzyć maszyny Wirtualnej, użyj jednej z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="e141d-109">If you need to create a VM, use one of the following methods:</span></span>

- <span data-ttu-id="e141d-110">[Azure CLI 2.0](quick-create-cli.md)</span><span class="sxs-lookup"><span data-stu-id="e141d-110">The [Azure CLI 2.0](quick-create-cli.md)</span></span>
- <span data-ttu-id="e141d-111">[Portalu Azure](quick-create-portal.md)</span><span class="sxs-lookup"><span data-stu-id="e141d-111">The [Azure portal](quick-create-portal.md)</span></span>


## <a name="install-a-desktop-environment-on-your-linux-vm"></a><span data-ttu-id="e141d-112">Zainstaluj środowisko pulpitu na maszynie Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="e141d-112">Install a desktop environment on your Linux VM</span></span>
<span data-ttu-id="e141d-113">Większość maszyn wirtualnych systemu Linux na platformie Azure nie masz środowisko pulpitu instalowane domyślnie.</span><span class="sxs-lookup"><span data-stu-id="e141d-113">Most Linux VMs in Azure do not have a desktop environment installed by default.</span></span> <span data-ttu-id="e141d-114">Maszyn wirtualnych systemu Linux są często zarządzane za pomocą połączeń SSH, a nie środowiska pulpitu.</span><span class="sxs-lookup"><span data-stu-id="e141d-114">Linux VMs are commonly managed using SSH connections rather than a desktop environment.</span></span> <span data-ttu-id="e141d-115">Istnieją różne środowiska pulpitu w systemie Linux, możesz wybrać następujące opcje.</span><span class="sxs-lookup"><span data-stu-id="e141d-115">There are various desktop environments in Linux that you can choose.</span></span> <span data-ttu-id="e141d-116">W zależności od wybranych środowiska pulpitu może korzystać z jednego do 2 GB miejsca na dysku i podjąć 5-10 minut, aby zainstalować i skonfigurować wymagane pakiety.</span><span class="sxs-lookup"><span data-stu-id="e141d-116">Depending on your choice of desktop environment, it may consume one to 2 GB of disk space, and take 5 to 10 minutes to install and configure all the required packages.</span></span>

<span data-ttu-id="e141d-117">W poniższym przykładzie instalowana niewielka [xfce4](https://www.xfce.org/) środowiska pulpitu na maszynie Wirtualnej systemu Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="e141d-117">The following example installs the lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM.</span></span> <span data-ttu-id="e141d-118">Polecenia dla innych dystrybucje się nieco różnić (Użyj `yum` zainstalować w systemie Red Hat Enterprise Linux i skonfigurować odpowiednie `selinux` reguły lub użyj `zypper` do zainstalowania w systemie SUSE, na przykład).</span><span class="sxs-lookup"><span data-stu-id="e141d-118">Commands for other distributions vary slightly (use `yum` to install on Red Hat Enterprise Linux and configure appropriate `selinux` rules, or use `zypper` to install on SUSE, for example).</span></span>

<span data-ttu-id="e141d-119">Pierwszy, SSH do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e141d-119">First, SSH to your VM.</span></span> <span data-ttu-id="e141d-120">Poniższy przykład nawiązuje połączenie z maszyną wirtualną o nazwie *myvm.westus.cloudapp.azure.com* nazwy użytkownika *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="e141d-120">The following example connects to the VM named *myvm.westus.cloudapp.azure.com* with the username of *azureuser*:</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="e141d-121">Jeśli używasz systemu Windows i uzyskać więcej informacji o korzystaniu z protokołu SSH, zobacz [kluczy sposobu korzystania z protokołu SSH z systemem Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="e141d-121">If you are using Windows and need more information on using SSH, see [How to use SSH keys with Windows](ssh-from-windows.md).</span></span>

<span data-ttu-id="e141d-122">Następnie zainstaluj przy użyciu xfce `apt` w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e141d-122">Next, install xfce using `apt` as follows:</span></span>

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a><span data-ttu-id="e141d-123">Instalowanie i konfigurowanie serwera usług pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="e141d-123">Install and configure a remote desktop server</span></span>
<span data-ttu-id="e141d-124">Teraz, gdy masz środowisko pulpitu, zainstalowane, należy skonfigurować usługi usług pulpitu zdalnego do nasłuchiwania przychodzących połączeń.</span><span class="sxs-lookup"><span data-stu-id="e141d-124">Now that you have a desktop environment installed, configure a remote desktop service to listen for incoming connections.</span></span> <span data-ttu-id="e141d-125">[xrdp](http://xrdp.org) jest serwer protokołu RDP (Remote Desktop) typu open source, który jest dostępny na większości dystrybucje systemu Linux i dobrze działa z xfce.</span><span class="sxs-lookup"><span data-stu-id="e141d-125">[xrdp](http://xrdp.org) is an open source Remote Desktop Protocol (RDP) server that is available on most Linux distributions, and works well with xfce.</span></span> <span data-ttu-id="e141d-126">Zainstaluj xrdp na maszynie Wirtualnej systemu Ubuntu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e141d-126">Install xrdp on your Ubuntu VM as follows:</span></span>

```bash
sudo apt-get install xrdp
```

<span data-ttu-id="e141d-127">Poinformuj xrdp środowiska pulpitu do użycia podczas uruchamiania sesji.</span><span class="sxs-lookup"><span data-stu-id="e141d-127">Tell xrdp what desktop environment to use when you start your session.</span></span> <span data-ttu-id="e141d-128">Skonfiguruj xrdp do użycia xfce jako środowisko pulpitu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e141d-128">Configure xrdp to use xfce as your desktop environment as follows:</span></span>

```bash
echo xfce4-session >~/.xsession
```

<span data-ttu-id="e141d-129">Uruchom ponownie usługę xrdp, aby zmiany zostały wprowadzone w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e141d-129">Restart the xrdp service for the changes to take effect as follows:</span></span>

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a><span data-ttu-id="e141d-130">Ustaw hasło konta użytkownika lokalnego</span><span class="sxs-lookup"><span data-stu-id="e141d-130">Set a local user account password</span></span>
<span data-ttu-id="e141d-131">Jeśli hasło zostało utworzone dla tego konta użytkownika, po utworzeniu maszyny Wirtualnej, Pomiń ten krok.</span><span class="sxs-lookup"><span data-stu-id="e141d-131">If you created a password for your user account when you created your VM, skip this step.</span></span> <span data-ttu-id="e141d-132">Jeśli tylko uwierzytelniania klucza SSH i nie masz hasła lokalnego konta ustawić, określ hasło, aby używać xrdp logować się do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e141d-132">If you only use SSH key authentication and do not have a local account password set, specify a password before you use xrdp to log in to your VM.</span></span> <span data-ttu-id="e141d-133">xrdp nie może zaakceptować kluczy SSH do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="e141d-133">xrdp cannot accept SSH keys for authentication.</span></span> <span data-ttu-id="e141d-134">W poniższym przykładzie określa hasło dla konta użytkownika *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="e141d-134">The following example specifies a password for the user account *azureuser*:</span></span>

```bash
sudo passwd azureuser
```

> [!NOTE]
> <span data-ttu-id="e141d-135">Określenie hasła nie powoduje aktualizacji konfiguracji SSHD, aby umożliwić hasło logowania, jeśli obecnie nie.</span><span class="sxs-lookup"><span data-stu-id="e141d-135">Specifying a password does not update your SSHD configuration to permit password logins if it currently does not.</span></span> <span data-ttu-id="e141d-136">Z punktu widzenia zabezpieczeń może chcesz nawiązać połączenie z maszyną Wirtualną z tunelu SSH przy użyciu uwierzytelniania opartego na kluczach, a następnie połącz się xrdp.</span><span class="sxs-lookup"><span data-stu-id="e141d-136">From a security perspective, you may wish to connect to your VM with an SSH tunnel using key-based authentication and then connect to xrdp.</span></span> <span data-ttu-id="e141d-137">Jeśli tak, pomiń następny krok na tworzenie reguły grupy zabezpieczeń sieci, aby zezwolić na ruch pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="e141d-137">If so, skip the following step on creating a network security group rule to allow remote desktop traffic.</span></span>


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a><span data-ttu-id="e141d-138">Tworzenie reguły grupy zabezpieczeń sieci dla ruchu pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="e141d-138">Create a Network Security Group rule for Remote Desktop traffic</span></span>
<span data-ttu-id="e141d-139">Aby zezwolić na ruch pulpitu zdalnego do maszyny Wirtualnej systemu Linux, zabezpieczenia sieci grupy reguł musi być utworzony umożliwia ruch TCP na porcie 3389 nawiązać połączenie z maszyną Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="e141d-139">To allow Remote Desktop traffic to reach your Linux VM, a network security group rule needs to be created that allows TCP on port 3389 to reach your VM.</span></span> <span data-ttu-id="e141d-140">Aby uzyskać więcej informacji dotyczących zasad grupy zabezpieczeń sieci, zobacz [co to jest grupa zabezpieczeń sieci?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e141d-140">For more information about network security group rules, see [What is a Network Security Group?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span> <span data-ttu-id="e141d-141">Możesz również [Użyj portalu Azure, aby utworzyć regułę grupy zabezpieczeń sieci](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e141d-141">You can also [use the Azure portal to create a network security group rule](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="e141d-142">Poniższe przykłady tworzenia reguły grupy zabezpieczeń sieci za pomocą [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create) o nazwie *myNetworkSecurityGroupRule* do *Zezwalaj* ruch na *tcp* portu *3389*.</span><span class="sxs-lookup"><span data-stu-id="e141d-142">The following examples create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) named *myNetworkSecurityGroupRule* to *allow* traffic on *tcp* port *3389*.</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a><span data-ttu-id="e141d-143">Połączenie z maszyną Wirtualną systemu Linux za pomocą klienta usług pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="e141d-143">Connect your Linux VM with a Remote Desktop client</span></span>
<span data-ttu-id="e141d-144">Otwórz klienta pulpitu zdalnego lokalnego i połącz się z adresu IP lub nazwę DNS maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="e141d-144">Open your local remote desktop client and connect to the IP address or DNS name of your Linux VM.</span></span> <span data-ttu-id="e141d-145">Wprowadź nazwę użytkownika i hasło dla konta użytkownika na maszynie Wirtualnej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e141d-145">Enter the username and password for the user account on your VM as follows:</span></span>

![Nawiązać xrdp przy użyciu klienta pulpitu zdalnego](./media/use-remote-desktop/remote-desktop-client.png)

<span data-ttu-id="e141d-147">Po uwierzytelnieniu środowiska pulpitu xfce obciążenia i wyglądać podobnie do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="e141d-147">After authenticating, the xfce desktop environment will load and look similar to the following example:</span></span>

![xfce środowisko pulpitu za pośrednictwem xrdp](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a><span data-ttu-id="e141d-149">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="e141d-149">Troubleshoot</span></span>
<span data-ttu-id="e141d-150">Jeśli nie można nawiązać połączenia z maszyny Wirtualnej systemu Linux przy użyciu klienta pulpitu zdalnego, należy użyć `netstat` na Twojej maszyny Wirtualnej systemu Linux, aby sprawdzić, czy maszyna wirtualna nasłuchuje połączeń protokołu RDP w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e141d-150">If you cannot connect to your Linux VM using a Remote Desktop client, use `netstat` on your Linux VM to verify that your VM is listening for RDP connections  as follows:</span></span>

```bash
sudo netstat -plnt | grep rdp
```

<span data-ttu-id="e141d-151">W poniższym przykładzie przedstawiono wirtualna nasłuchiwanie na porcie TCP 3389 zgodnie z oczekiwaniami:</span><span class="sxs-lookup"><span data-stu-id="e141d-151">The following example shows the VM listening on TCP port 3389 as expected:</span></span>

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

<span data-ttu-id="e141d-152">Jeśli nie nasłuchuje usługa xrdp, na maszynie Wirtualnej systemu Ubuntu ponownie uruchomić usługę w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e141d-152">If the xrdp service is not listening, on an Ubuntu VM restart the service as follows:</span></span>

```bash
sudo service xrdp restart
```

<span data-ttu-id="e141d-153">Przejrzyj dzienniki w */var/log*Thug na maszynie Wirtualnej systemu Ubuntu dla wskazać, dlaczego usługa może nie odpowiadać.</span><span class="sxs-lookup"><span data-stu-id="e141d-153">Review logs in */var/log*Thug  on your Ubuntu VM for indications as to why the service may not be responding.</span></span> <span data-ttu-id="e141d-154">Można również monitorować syslog, podczas próby połączeń usług pulpitu zdalnego, aby wyświetlić wszystkie błędy:</span><span class="sxs-lookup"><span data-stu-id="e141d-154">You can also monitor the syslog during a remote desktop connection attempt to view any errors:</span></span>

```bash
tail -f /var/log/syslog
```

<span data-ttu-id="e141d-155">Inne dystrybucje systemu Linux, takie jak Red Hat Enterprise Linux i SUSE mogą mieć różne sposoby, aby ponownie uruchomić usługi i lokalizacje plików dziennika alternatywne, aby przejrzeć.</span><span class="sxs-lookup"><span data-stu-id="e141d-155">Other Linux distributions such as Red Hat Enterprise Linux and SUSE may have different ways to restart services and alternate log file locations to review.</span></span>

<span data-ttu-id="e141d-156">Jeśli nie mają żadnych odpowiedzi na kliencie usług pulpitu zdalnego i nie ma żadnych zdarzeń w dzienniku systemowym, to zachowanie wskazuje, czy ruch pulpitu zdalnego nie może połączyć maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e141d-156">If you do not receive any response in your remote desktop client and do not see any events in the system log, this behavior indicates that remote desktop traffic cannot reach the VM.</span></span> <span data-ttu-id="e141d-157">Przejrzyj reguły grupy zabezpieczeń sieci, tak aby upewnić się, że masz regułę zezwalającą na ruch TCP na porcie 3389.</span><span class="sxs-lookup"><span data-stu-id="e141d-157">Review your network security group rules to ensure that you have a rule to permit TCP on port 3389.</span></span> <span data-ttu-id="e141d-158">Aby uzyskać więcej informacji, zobacz [Rozwiązywanie problemów z łącznością aplikacji](../windows/troubleshoot-app-connection.md).</span><span class="sxs-lookup"><span data-stu-id="e141d-158">For more information, see [Troubleshoot application connectivity issues](../windows/troubleshoot-app-connection.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="e141d-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e141d-159">Next steps</span></span>
<span data-ttu-id="e141d-160">Aby uzyskać więcej informacji na temat tworzenia i używania kluczy SSH z maszyn wirtualnych systemu Linux, zobacz [utworzyć SSH kluczy dla maszyn wirtualnych systemu Linux na platformie Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="e141d-160">For more information about creating and using SSH keys with Linux VMs, see [Create SSH keys for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

<span data-ttu-id="e141d-161">Aby uzyskać informacji o korzystaniu z protokołu SSH z systemu Windows, zobacz [kluczy sposobu korzystania z protokołu SSH z systemem Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="e141d-161">For information on using SSH from Windows, see [How to use SSH keys with Windows](ssh-from-windows.md).</span></span>

