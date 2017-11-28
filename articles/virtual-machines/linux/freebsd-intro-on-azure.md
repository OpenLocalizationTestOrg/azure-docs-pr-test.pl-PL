---
title: tooFreeBSD aaaIntroduction na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się więcej o używaniu maszyn wirtualnych FreeBSD na platformie Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: 43ba7a70ed21e7fb8b331f4a26db0426e098c4aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toofreebsd-on-azure"></a><span data-ttu-id="e19bc-103">Wprowadzenie tooFreeBSD na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="e19bc-103">Introduction tooFreeBSD on Azure</span></span>
<span data-ttu-id="e19bc-104">Ten temat zawiera omówienie uruchomienie maszyny wirtualnej FreeBSD na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e19bc-104">This topic provides an overview of running a FreeBSD virtual machine in Azure.</span></span>

## <a name="overview"></a><span data-ttu-id="e19bc-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e19bc-105">Overview</span></span>
<span data-ttu-id="e19bc-106">FreeBSD platformy Microsoft Azure jest zaawansowane systemu operacyjnego używany toopower nowoczesnych serwery, komputery stacjonarne i osadzone platform.</span><span class="sxs-lookup"><span data-stu-id="e19bc-106">FreeBSD for Microsoft Azure is an advanced computer operating system used toopower modern servers, desktops, and embedded platforms.</span></span>

<span data-ttu-id="e19bc-107">Microsoft Corporation jest udostępnianie obrazów FreeBSD na platformie Azure z hello [Agent gościa maszyny Wirtualnej Azure](https://github.com/Azure/WALinuxAgent/) wstępnie skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="e19bc-107">Microsoft Corporation is making images of FreeBSD available on Azure with hello [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) pre-configured.</span></span> <span data-ttu-id="e19bc-108">Obecnie hello następujące wersje FreeBSD mogą używać jako obrazy przez firmę Microsoft:</span><span class="sxs-lookup"><span data-stu-id="e19bc-108">Currently, hello following FreeBSD versions are offered as images by Microsoft:</span></span>

- <span data-ttu-id="e19bc-109">FreeBSD 10.3-wersja</span><span class="sxs-lookup"><span data-stu-id="e19bc-109">FreeBSD 10.3-RELEASE</span></span>
- <span data-ttu-id="e19bc-110">FreeBSD 11.0-wersja</span><span class="sxs-lookup"><span data-stu-id="e19bc-110">FreeBSD 11.0-RELEASE</span></span>

<span data-ttu-id="e19bc-111">Hello agent jest odpowiedzialny za komunikację między hello FreeBSD maszyny Wirtualnej i hello Azure fabric dla operacji, takich jak inicjowanie obsługi administracyjnej hello maszyny Wirtualnej przy pierwszym użyciu (nazwa użytkownika, hasło lub klucz SSH, nazwy hosta, itp.) i włączenie funkcji selektywnego rozszerzeń maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e19bc-111">hello agent is responsible for communication between hello FreeBSD VM and hello Azure fabric for operations such as provisioning hello VM on first use (user name, password or SSH key, host name, etc.) and enabling functionality for selective VM extensions.</span></span>

<span data-ttu-id="e19bc-112">Podobnie jak w przypadku przyszłych wersji FreeBSD strategii hello jest toostay bieżącego i Udostępnij hello najnowsze wersje wkrótce po ich opublikowaniu przez zespół inżynieryjny hello FreeBSD wersji.</span><span class="sxs-lookup"><span data-stu-id="e19bc-112">As for future versions of FreeBSD, hello strategy is toostay current and make hello latest releases available shortly after they are published by hello FreeBSD release engineering team.</span></span>

## <a name="deploying-a-freebsd-virtual-machine"></a><span data-ttu-id="e19bc-113">Wdrażanie maszyny wirtualnej FreeBSD</span><span class="sxs-lookup"><span data-stu-id="e19bc-113">Deploying a FreeBSD virtual machine</span></span>
<span data-ttu-id="e19bc-114">Wdrażanie maszyny wirtualnej FreeBSD jest dość proste przy użyciu obrazu z hello Azure Marketplace z hello portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="e19bc-114">Deploying a FreeBSD virtual machine is a straightforward process using an image from hello Azure Marketplace from hello Azure portal:</span></span>

- [<span data-ttu-id="e19bc-115">10.3 FreeBSD na hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="e19bc-115">FreeBSD 10.3 on hello Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [<span data-ttu-id="e19bc-116">11.0 FreeBSD na hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="e19bc-116">FreeBSD 11.0 on hello Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a><span data-ttu-id="e19bc-117">Tworzenie maszyny Wirtualnej FreeBSD za pośrednictwem interfejsu wiersza polecenia platformy Azure 2.0 na FreeBSD</span><span class="sxs-lookup"><span data-stu-id="e19bc-117">Create a FreeBSD VM through Azure CLI 2.0 on FreeBSD</span></span>
<span data-ttu-id="e19bc-118">Najpierw należy tooinstall [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) chociaż następujące polecenia na komputerze FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="e19bc-118">First you need tooinstall [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) though following command on a FreeBSD machine.</span></span>

```bash 
curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="e19bc-119">Jeśli bash nie jest zainstalowany na tym komputerze FreeBSD, uruchom następujące polecenie przed rozpoczęciem powitalne instalacji.</span><span class="sxs-lookup"><span data-stu-id="e19bc-119">If bash is not installed on your FreeBSD machine, run following command before hello installation.</span></span> 

```bash
sudo pkg install bash
```

<span data-ttu-id="e19bc-120">Jeśli python nie jest zainstalowany na tym komputerze FreeBSD, uruchom następujące polecenia przed rozpoczęciem powitalne instalacji.</span><span class="sxs-lookup"><span data-stu-id="e19bc-120">If python is not installed on your FreeBSD machine, run following commands before hello installation.</span></span> 

```bash
sudo pkg install python35
cd /usr/local/bin 
sudo rm /usr/local/bin/python 
sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

<span data-ttu-id="e19bc-121">Podczas instalacji hello prośba `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`.</span><span class="sxs-lookup"><span data-stu-id="e19bc-121">During hello installation, you are asked `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`.</span></span> <span data-ttu-id="e19bc-122">Jeśli wybierzesz odpowiedź `y` , a następnie wprowadź `/etc/rc.conf` jako `a path tooan rc file tooupdate`, może spełniać hello problem `ERROR: [Errno 13] Permission denied`.</span><span class="sxs-lookup"><span data-stu-id="e19bc-122">If you answer `y` and enter `/etc/rc.conf` as `a path tooan rc file tooupdate`, you may meet hello problem `ERROR: [Errno 13] Permission denied`.</span></span> <span data-ttu-id="e19bc-123">tooresolve ten problem, należy udzielić hello zapisu toocurrent prawo użytkownika w odniesieniu do pliku hello `etc/rc.conf`.</span><span class="sxs-lookup"><span data-stu-id="e19bc-123">tooresolve this problem, you should grant hello write right toocurrent user against hello file `etc/rc.conf`.</span></span>

<span data-ttu-id="e19bc-124">Teraz możesz zalogować się na platformie Azure i utworzyć FreeBSD maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e19bc-124">Now you can log in Azure and create your FreeBSD VM.</span></span> <span data-ttu-id="e19bc-125">Poniżej znajduje się przykład toocreate 11.0 FreeBSD maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e19bc-125">Below is an example toocreate a FreeBSD 11.0 VM.</span></span> <span data-ttu-id="e19bc-126">Możesz także dodać parametr hello `--public-ip-address-dns-name` z globalnie unikatowej nazwy DNS dla nowo utworzonego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="e19bc-126">You can also add hello parameter `--public-ip-address-dns-name` with a globally unique DNS name for a newly created Public IP.</span></span> 

```azurecli
az login 
az group create --name myResourceGroup --location eastus
az vm create --name myFreeBSD11 \
    --resource-group myResourceGroup \
    --image MicrosoftOSTC:FreeBSD:11.0:latest \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="e19bc-127">Następnie możesz zalogować się tooyour FreeBSD maszyny Wirtualnej za pośrednictwem adresu ip hello wydrukowania w hello powyższych danych wyjściowych z wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="e19bc-127">Then you can log in tooyour FreeBSD VM through hello ip address that printed in hello output of above deployment.</span></span> 

```bash
ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a><span data-ttu-id="e19bc-128">Rozszerzenia maszyny Wirtualnej dla FreeBSD</span><span class="sxs-lookup"><span data-stu-id="e19bc-128">VM extensions for FreeBSD</span></span>
<span data-ttu-id="e19bc-129">Poniżej przedstawiono obsługiwane rozszerzeń maszyny Wirtualnej w FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="e19bc-129">Following are supported VM extensions in FreeBSD.</span></span>

### <a name="vmaccess"></a><span data-ttu-id="e19bc-130">Rozszerzenia VMAccess</span><span class="sxs-lookup"><span data-stu-id="e19bc-130">VMAccess</span></span>
<span data-ttu-id="e19bc-131">Witaj [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) rozszerzenia można:</span><span class="sxs-lookup"><span data-stu-id="e19bc-131">hello [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension can:</span></span>

* <span data-ttu-id="e19bc-132">Resetowanie hasła hello hello oryginalnego sudo użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e19bc-132">Reset hello password of hello original sudo user.</span></span>
* <span data-ttu-id="e19bc-133">Utwórz nowego użytkownika sudo z hello hasło.</span><span class="sxs-lookup"><span data-stu-id="e19bc-133">Create a new sudo user with hello password specified.</span></span>
* <span data-ttu-id="e19bc-134">Ustaw klucz publiczny hosta hello kluczem hello podane.</span><span class="sxs-lookup"><span data-stu-id="e19bc-134">Set hello public host key with hello key given.</span></span>
* <span data-ttu-id="e19bc-135">Resetuj klucz publiczny hosta hello podane podczas obsługi, jeśli nie zostanie podany klucz hosta hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e19bc-135">Reset hello public host key provided during VM provisioning if hello host key is not provided.</span></span>
* <span data-ttu-id="e19bc-136">Otwórz hello portu SSH (22) i przywrócić hello sshd_config, jeśli reset_ssh ustawiono tootrue.</span><span class="sxs-lookup"><span data-stu-id="e19bc-136">Open hello SSH port (22) and restore hello sshd_config if reset_ssh is set tootrue.</span></span>
* <span data-ttu-id="e19bc-137">Usuń hello istniejącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e19bc-137">Remove hello existing user.</span></span>
* <span data-ttu-id="e19bc-138">Sprawdź dyski.</span><span class="sxs-lookup"><span data-stu-id="e19bc-138">Check disks.</span></span>
* <span data-ttu-id="e19bc-139">Napraw dodanych dysków.</span><span class="sxs-lookup"><span data-stu-id="e19bc-139">Repair an added disk.</span></span>

### <a name="customscript"></a><span data-ttu-id="e19bc-140">CustomScript</span><span class="sxs-lookup"><span data-stu-id="e19bc-140">CustomScript</span></span>
<span data-ttu-id="e19bc-141">Witaj [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) rozszerzenia można:</span><span class="sxs-lookup"><span data-stu-id="e19bc-141">hello [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension can:</span></span>

* <span data-ttu-id="e19bc-142">Jeśli zostanie podana, Pobierz skrypty hello dostosowane z usługi Azure Storage lub magazynu publicznego zewnętrznego (na przykład GitHub).</span><span class="sxs-lookup"><span data-stu-id="e19bc-142">If provided, download hello customized scripts from Azure Storage or external public storage (for example, GitHub).</span></span>
* <span data-ttu-id="e19bc-143">Uruchom skrypt punktu wejścia hello.</span><span class="sxs-lookup"><span data-stu-id="e19bc-143">Run hello entry point script.</span></span>
* <span data-ttu-id="e19bc-144">Obsługuje wbudowanego polecenia.</span><span class="sxs-lookup"><span data-stu-id="e19bc-144">Support inline commands.</span></span>
* <span data-ttu-id="e19bc-145">Konwertuj automatycznie dopasuje styl systemu Windows w powłoki i skryptów języka Python.</span><span class="sxs-lookup"><span data-stu-id="e19bc-145">Convert Windows-style newline in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="e19bc-146">Automatycznie Usuń BOM powłoki i skryptów języka Python.</span><span class="sxs-lookup"><span data-stu-id="e19bc-146">Remove BOM in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="e19bc-147">Ochrona poufnych danych w CommandToExecute.</span><span class="sxs-lookup"><span data-stu-id="e19bc-147">Protect sensitive data in CommandToExecute.</span></span>

> [!NOTE]
> <span data-ttu-id="e19bc-148">Maszyna wirtualna FreeBSD obsługuje tylko wersję CustomScript 1.x przez teraz.</span><span class="sxs-lookup"><span data-stu-id="e19bc-148">FreeBSD VM only supports CustomScript version 1.x by now.</span></span>  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a><span data-ttu-id="e19bc-149">Uwierzytelniania: nazwy użytkowników, hasła i klucze SSH</span><span class="sxs-lookup"><span data-stu-id="e19bc-149">Authentication: user names, passwords, and SSH keys</span></span>
<span data-ttu-id="e19bc-150">Podczas tworzenia maszyny wirtualnej FreeBSD przy użyciu hello portalu Azure, musisz podać nazwę użytkownika, hasło lub klucz publiczny SSH.</span><span class="sxs-lookup"><span data-stu-id="e19bc-150">When you're creating a FreeBSD virtual machine by using hello Azure portal, you must provide a user name, password, or SSH public key.</span></span>
<span data-ttu-id="e19bc-151">Nazwy użytkownika podczas wdrażania maszyny wirtualnej FreeBSD na platformie Azure nie muszą być zgodne nazwy kont systemowych (UID < 100) znajduje się już w hello maszyny wirtualnej ("root", na przykład).</span><span class="sxs-lookup"><span data-stu-id="e19bc-151">User names for deploying a FreeBSD virtual machine on Azure must not match names of system accounts (UID <100) already present in hello virtual machine ("root", for example).</span></span>
<span data-ttu-id="e19bc-152">Aktualnie obsługiwana jest tylko hello RSA klucza SSH.</span><span class="sxs-lookup"><span data-stu-id="e19bc-152">Currently, only hello RSA SSH key is supported.</span></span> <span data-ttu-id="e19bc-153">Wielowierszowy klucz SSH musi zaczynać się od `---- BEGIN SSH2 PUBLIC KEY ----` się i kończyć `---- END SSH2 PUBLIC KEY ----`.</span><span class="sxs-lookup"><span data-stu-id="e19bc-153">A multiline SSH key must begin with `---- BEGIN SSH2 PUBLIC KEY ----` and end with `---- END SSH2 PUBLIC KEY ----`.</span></span>

## <a name="obtaining-superuser-privileges"></a><span data-ttu-id="e19bc-154">Uzyskanie uprawnień administratora</span><span class="sxs-lookup"><span data-stu-id="e19bc-154">Obtaining superuser privileges</span></span>
<span data-ttu-id="e19bc-155">Witaj konta użytkownika, które określono podczas wdrażania wystąpienia maszyny wirtualnej na platformie Azure jest uprzywilejowanego konta.</span><span class="sxs-lookup"><span data-stu-id="e19bc-155">hello user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="e19bc-156">Witaj pakietu sudo został zainstalowany w hello opublikowane FreeBSD obrazu.</span><span class="sxs-lookup"><span data-stu-id="e19bc-156">hello package of sudo was installed in hello published FreeBSD image.</span></span>
<span data-ttu-id="e19bc-157">Po zalogowano się za pomocą tego konta użytkownika, możesz uruchamiać polecenia jako główny przy użyciu składni polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="e19bc-157">After you're logged in through this user account, you can run commands as root by using hello command syntax.</span></span>

```
$ sudo <COMMAND>
```

<span data-ttu-id="e19bc-158">Powłoka głównego Opcjonalnie można uzyskać za pomocą `sudo -s`.</span><span class="sxs-lookup"><span data-stu-id="e19bc-158">You can optionally obtain a root shell by using `sudo -s`.</span></span>

## <a name="known-issues"></a><span data-ttu-id="e19bc-159">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="e19bc-159">Known issues</span></span>
<span data-ttu-id="e19bc-160">Witaj [Agent gościa maszyny Wirtualnej Azure](https://github.com/Azure/WALinuxAgent/) wersji 2.2.2 ma [znany problem] (https://github.com/Azure/WALinuxAgent/pull/517), która powoduje niepowodzenie udostępniania hello dla maszyny Wirtualnej FreeBSD na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e19bc-160">hello [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.2 has a [known issue] (https://github.com/Azure/WALinuxAgent/pull/517) that causes hello provision failure for FreeBSD VM on Azure.</span></span> <span data-ttu-id="e19bc-161">Witaj poprawka została przechwycona przez [Agent gościa maszyny Wirtualnej Azure](https://github.com/Azure/WALinuxAgent/) wersji 2.2.3 i jego nowszych wersjach.</span><span class="sxs-lookup"><span data-stu-id="e19bc-161">hello fix was captured by [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.3 and later releases.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e19bc-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e19bc-162">Next steps</span></span>
* <span data-ttu-id="e19bc-163">Przejdź za[portalu Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate FreeBSD maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e19bc-163">Go too[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate a FreeBSD VM.</span></span>
* <span data-ttu-id="e19bc-164">Toobring własne tooAzure FreeBSD, zapoznaj się zbyt[tworzenie i przekazywanie wirtualnego dysku twardego FreeBSD tooAzure](classic/freebsd-create-upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="e19bc-164">If you want toobring your own FreeBSD tooAzure, refer too[Create and upload a FreeBSD VHD tooAzure](classic/freebsd-create-upload-vhd.md).</span></span>
