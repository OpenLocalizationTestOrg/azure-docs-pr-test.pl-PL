---
title: Wprowadzenie do FreeBSD na platformie Azure | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 7ada9fddd7ffccc3dcbfe3eac05d99b710b67cbc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="introduction-to-freebsd-on-azure"></a><span data-ttu-id="ad811-103">Wprowadzenie do FreeBSD na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="ad811-103">Introduction to FreeBSD on Azure</span></span>
<span data-ttu-id="ad811-104">Ten temat zawiera omówienie uruchomienie maszyny wirtualnej FreeBSD na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ad811-104">This topic provides an overview of running a FreeBSD virtual machine in Azure.</span></span>

## <a name="overview"></a><span data-ttu-id="ad811-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="ad811-105">Overview</span></span>
<span data-ttu-id="ad811-106">FreeBSD platformy Microsoft Azure to zaawansowane systemu operacyjnego używany do zasilania nowoczesnych serwerów, komputerów stacjonarnych i osadzone platform.</span><span class="sxs-lookup"><span data-stu-id="ad811-106">FreeBSD for Microsoft Azure is an advanced computer operating system used to power modern servers, desktops, and embedded platforms.</span></span>

<span data-ttu-id="ad811-107">Microsoft Corporation jest udostępniania obrazów FreeBSD na platformie Azure za pomocą [Agent gościa maszyny Wirtualnej Azure](https://github.com/Azure/WALinuxAgent/) wstępnie skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="ad811-107">Microsoft Corporation is making images of FreeBSD available on Azure with the [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) pre-configured.</span></span> <span data-ttu-id="ad811-108">Obecnie następujące wersje FreeBSD są jako obrazów oferowanych przez firmę Microsoft:</span><span class="sxs-lookup"><span data-stu-id="ad811-108">Currently, the following FreeBSD versions are offered as images by Microsoft:</span></span>

- <span data-ttu-id="ad811-109">FreeBSD 10.3-wersja</span><span class="sxs-lookup"><span data-stu-id="ad811-109">FreeBSD 10.3-RELEASE</span></span>
- <span data-ttu-id="ad811-110">FreeBSD 11.0-wersja</span><span class="sxs-lookup"><span data-stu-id="ad811-110">FreeBSD 11.0-RELEASE</span></span>

<span data-ttu-id="ad811-111">Agent jest odpowiedzialny za komunikację między FreeBSD maszyny Wirtualnej i sieci szkieletowej Azure dla operacji, takich jak inicjowanie obsługi maszyn wirtualnych przy pierwszym użyciu (nazwa użytkownika, hasło lub klucz SSH, nazwy hosta, itp.) i włączenie funkcji selektywnego rozszerzeń maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad811-111">The agent is responsible for communication between the FreeBSD VM and the Azure fabric for operations such as provisioning the VM on first use (user name, password or SSH key, host name, etc.) and enabling functionality for selective VM extensions.</span></span>

<span data-ttu-id="ad811-112">Podobnie jak w przypadku przyszłych wersji FreeBSD strategii jest Pozostań na bieżąco i udostępnić najnowsze wersje, wkrótce po ich opublikowaniu przez zespół inżynieryjny wersji FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="ad811-112">As for future versions of FreeBSD, the strategy is to stay current and make the latest releases available shortly after they are published by the FreeBSD release engineering team.</span></span>

## <a name="deploying-a-freebsd-virtual-machine"></a><span data-ttu-id="ad811-113">Wdrażanie maszyny wirtualnej FreeBSD</span><span class="sxs-lookup"><span data-stu-id="ad811-113">Deploying a FreeBSD virtual machine</span></span>
<span data-ttu-id="ad811-114">Wdrażanie maszyny wirtualnej FreeBSD jest dość proste przy użyciu obrazu z portalu Azure Marketplace z portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="ad811-114">Deploying a FreeBSD virtual machine is a straightforward process using an image from the Azure Marketplace from the Azure portal:</span></span>

- [<span data-ttu-id="ad811-115">FreeBSD 10.3 w witrynie Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="ad811-115">FreeBSD 10.3 on the Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [<span data-ttu-id="ad811-116">FreeBSD 11.0 w witrynie Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="ad811-116">FreeBSD 11.0 on the Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a><span data-ttu-id="ad811-117">Tworzenie maszyny Wirtualnej FreeBSD za pośrednictwem interfejsu wiersza polecenia platformy Azure 2.0 na FreeBSD</span><span class="sxs-lookup"><span data-stu-id="ad811-117">Create a FreeBSD VM through Azure CLI 2.0 on FreeBSD</span></span>
<span data-ttu-id="ad811-118">Najpierw należy zainstalować [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) chociaż następujące polecenia na komputerze FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="ad811-118">First you need to install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) though following command on a FreeBSD machine.</span></span>

```bash 
curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="ad811-119">Jeśli bash nie jest zainstalowany na tym komputerze FreeBSD, uruchom następujące polecenie przed rozpoczęciem instalacji.</span><span class="sxs-lookup"><span data-stu-id="ad811-119">If bash is not installed on your FreeBSD machine, run following command before the installation.</span></span> 

```bash
sudo pkg install bash
```

<span data-ttu-id="ad811-120">Jeśli python nie jest zainstalowany na tym komputerze FreeBSD, uruchom następujące polecenia, przed rozpoczęciem instalacji.</span><span class="sxs-lookup"><span data-stu-id="ad811-120">If python is not installed on your FreeBSD machine, run following commands before the installation.</span></span> 

```bash
sudo pkg install python35
cd /usr/local/bin 
sudo rm /usr/local/bin/python 
sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

<span data-ttu-id="ad811-121">Podczas instalacji, zostanie wyświetlona prośba `Modify profile to update your $PATH and enable shell/tab completion now? (Y/n)`.</span><span class="sxs-lookup"><span data-stu-id="ad811-121">During the installation, you are asked `Modify profile to update your $PATH and enable shell/tab completion now? (Y/n)`.</span></span> <span data-ttu-id="ad811-122">Jeśli wybierzesz odpowiedź `y` , a następnie wprowadź `/etc/rc.conf` jako `a path to an rc file to update`, problem może spełniać `ERROR: [Errno 13] Permission denied`.</span><span class="sxs-lookup"><span data-stu-id="ad811-122">If you answer `y` and enter `/etc/rc.conf` as `a path to an rc file to update`, you may meet the problem `ERROR: [Errno 13] Permission denied`.</span></span> <span data-ttu-id="ad811-123">Aby rozwiązać ten problem, należy udzielić zapisu prawo do bieżącego użytkownika w odniesieniu do pliku `etc/rc.conf`.</span><span class="sxs-lookup"><span data-stu-id="ad811-123">To resolve this problem, you should grant the write right to current user against the file `etc/rc.conf`.</span></span>

<span data-ttu-id="ad811-124">Teraz możesz zalogować się na platformie Azure i utworzyć FreeBSD maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad811-124">Now you can log in Azure and create your FreeBSD VM.</span></span> <span data-ttu-id="ad811-125">Poniżej znajduje się przykład można utworzyć maszyny Wirtualnej 11.0 FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="ad811-125">Below is an example to create a FreeBSD 11.0 VM.</span></span> <span data-ttu-id="ad811-126">Możesz także dodać parametr `--public-ip-address-dns-name` z globalnie unikatowej nazwy DNS dla nowo utworzonego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="ad811-126">You can also add the parameter `--public-ip-address-dns-name` with a globally unique DNS name for a newly created Public IP.</span></span> 

```azurecli
az login 
az group create --name myResourceGroup --location eastus
az vm create --name myFreeBSD11 \
    --resource-group myResourceGroup \
    --image MicrosoftOSTC:FreeBSD:11.0:latest \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="ad811-127">Następnie możesz zalogować się do maszyny Wirtualnej FreeBSD za pośrednictwem adresu ip, który drukowany w powyższych danych wyjściowych z wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="ad811-127">Then you can log in to your FreeBSD VM through the ip address that printed in the output of above deployment.</span></span> 

```bash
ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a><span data-ttu-id="ad811-128">Rozszerzenia maszyny Wirtualnej dla FreeBSD</span><span class="sxs-lookup"><span data-stu-id="ad811-128">VM extensions for FreeBSD</span></span>
<span data-ttu-id="ad811-129">Poniżej przedstawiono obsługiwane rozszerzeń maszyny Wirtualnej w FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="ad811-129">Following are supported VM extensions in FreeBSD.</span></span>

### <a name="vmaccess"></a><span data-ttu-id="ad811-130">Rozszerzenia VMAccess</span><span class="sxs-lookup"><span data-stu-id="ad811-130">VMAccess</span></span>
<span data-ttu-id="ad811-131">[VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) rozszerzenia można:</span><span class="sxs-lookup"><span data-stu-id="ad811-131">The [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension can:</span></span>

* <span data-ttu-id="ad811-132">Zresetuj hasło dla oryginalnego użytkownika sudo.</span><span class="sxs-lookup"><span data-stu-id="ad811-132">Reset the password of the original sudo user.</span></span>
* <span data-ttu-id="ad811-133">Utwórz nowego użytkownika sudo z określone hasło.</span><span class="sxs-lookup"><span data-stu-id="ad811-133">Create a new sudo user with the password specified.</span></span>
* <span data-ttu-id="ad811-134">Ustaw klucz publiczny hosta przy użyciu danego klucza.</span><span class="sxs-lookup"><span data-stu-id="ad811-134">Set the public host key with the key given.</span></span>
* <span data-ttu-id="ad811-135">Zresetować klucz publiczny hosta dostarczone podczas dostarczania maszyny Wirtualnej, jeśli nie zostanie podany klucz hosta.</span><span class="sxs-lookup"><span data-stu-id="ad811-135">Reset the public host key provided during VM provisioning if the host key is not provided.</span></span>
* <span data-ttu-id="ad811-136">Otwarcie portu SSH (22) i przywrócić sshd_config, jeśli reset_ssh jest ustawiona na true.</span><span class="sxs-lookup"><span data-stu-id="ad811-136">Open the SSH port (22) and restore the sshd_config if reset_ssh is set to true.</span></span>
* <span data-ttu-id="ad811-137">Usuwanie istniejącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ad811-137">Remove the existing user.</span></span>
* <span data-ttu-id="ad811-138">Sprawdź dyski.</span><span class="sxs-lookup"><span data-stu-id="ad811-138">Check disks.</span></span>
* <span data-ttu-id="ad811-139">Napraw dodanych dysków.</span><span class="sxs-lookup"><span data-stu-id="ad811-139">Repair an added disk.</span></span>

### <a name="customscript"></a><span data-ttu-id="ad811-140">CustomScript</span><span class="sxs-lookup"><span data-stu-id="ad811-140">CustomScript</span></span>
<span data-ttu-id="ad811-141">[CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) rozszerzenia można:</span><span class="sxs-lookup"><span data-stu-id="ad811-141">The [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension can:</span></span>

* <span data-ttu-id="ad811-142">Jeśli zostanie podana, należy pobrać dostosowane skrypty z usługi Azure Storage lub magazynu publicznego zewnętrznego (na przykład GitHub).</span><span class="sxs-lookup"><span data-stu-id="ad811-142">If provided, download the customized scripts from Azure Storage or external public storage (for example, GitHub).</span></span>
* <span data-ttu-id="ad811-143">Uruchom skrypt punktu wejścia.</span><span class="sxs-lookup"><span data-stu-id="ad811-143">Run the entry point script.</span></span>
* <span data-ttu-id="ad811-144">Obsługuje wbudowanego polecenia.</span><span class="sxs-lookup"><span data-stu-id="ad811-144">Support inline commands.</span></span>
* <span data-ttu-id="ad811-145">Konwertuj automatycznie dopasuje styl systemu Windows w powłoki i skryptów języka Python.</span><span class="sxs-lookup"><span data-stu-id="ad811-145">Convert Windows-style newline in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="ad811-146">Automatycznie Usuń BOM powłoki i skryptów języka Python.</span><span class="sxs-lookup"><span data-stu-id="ad811-146">Remove BOM in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="ad811-147">Ochrona poufnych danych w CommandToExecute.</span><span class="sxs-lookup"><span data-stu-id="ad811-147">Protect sensitive data in CommandToExecute.</span></span>

> [!NOTE]
> <span data-ttu-id="ad811-148">Maszyna wirtualna FreeBSD obsługuje tylko wersję CustomScript 1.x przez teraz.</span><span class="sxs-lookup"><span data-stu-id="ad811-148">FreeBSD VM only supports CustomScript version 1.x by now.</span></span>  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a><span data-ttu-id="ad811-149">Uwierzytelniania: nazwy użytkowników, hasła i klucze SSH</span><span class="sxs-lookup"><span data-stu-id="ad811-149">Authentication: user names, passwords, and SSH keys</span></span>
<span data-ttu-id="ad811-150">Podczas tworzenia maszyny wirtualnej FreeBSD przy użyciu portalu Azure, musisz podać nazwę użytkownika, hasło lub klucz publiczny SSH.</span><span class="sxs-lookup"><span data-stu-id="ad811-150">When you're creating a FreeBSD virtual machine by using the Azure portal, you must provide a user name, password, or SSH public key.</span></span>
<span data-ttu-id="ad811-151">Nazwy użytkownika podczas wdrażania maszyny wirtualnej FreeBSD na platformie Azure nie muszą być zgodne nazwy kont systemowych (UID < 100) znajduje się już w maszynie wirtualnej ("root", na przykład).</span><span class="sxs-lookup"><span data-stu-id="ad811-151">User names for deploying a FreeBSD virtual machine on Azure must not match names of system accounts (UID <100) already present in the virtual machine ("root", for example).</span></span>
<span data-ttu-id="ad811-152">Aktualnie obsługiwana jest tylko RSA klucza SSH.</span><span class="sxs-lookup"><span data-stu-id="ad811-152">Currently, only the RSA SSH key is supported.</span></span> <span data-ttu-id="ad811-153">Wielowierszowy klucz SSH musi zaczynać się od `---- BEGIN SSH2 PUBLIC KEY ----` się i kończyć `---- END SSH2 PUBLIC KEY ----`.</span><span class="sxs-lookup"><span data-stu-id="ad811-153">A multiline SSH key must begin with `---- BEGIN SSH2 PUBLIC KEY ----` and end with `---- END SSH2 PUBLIC KEY ----`.</span></span>

## <a name="obtaining-superuser-privileges"></a><span data-ttu-id="ad811-154">Uzyskanie uprawnień administratora</span><span class="sxs-lookup"><span data-stu-id="ad811-154">Obtaining superuser privileges</span></span>
<span data-ttu-id="ad811-155">Konto użytkownika, które określono podczas wdrażania wystąpienia maszyny wirtualnej na platformie Azure jest uprzywilejowanego konta.</span><span class="sxs-lookup"><span data-stu-id="ad811-155">The user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="ad811-156">Pakiet sudo został zainstalowany w opublikowanej FreeBSD obrazu.</span><span class="sxs-lookup"><span data-stu-id="ad811-156">The package of sudo was installed in the published FreeBSD image.</span></span>
<span data-ttu-id="ad811-157">Po zalogowano się za pomocą tego konta użytkownika, możesz uruchamiać polecenia jako główny przy użyciu składni polecenia.</span><span class="sxs-lookup"><span data-stu-id="ad811-157">After you're logged in through this user account, you can run commands as root by using the command syntax.</span></span>

```
$ sudo <COMMAND>
```

<span data-ttu-id="ad811-158">Powłoka głównego Opcjonalnie można uzyskać za pomocą `sudo -s`.</span><span class="sxs-lookup"><span data-stu-id="ad811-158">You can optionally obtain a root shell by using `sudo -s`.</span></span>

## <a name="known-issues"></a><span data-ttu-id="ad811-159">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="ad811-159">Known issues</span></span>
<span data-ttu-id="ad811-160">[Agent gościa maszyny Wirtualnej Azure](https://github.com/Azure/WALinuxAgent/) wersji 2.2.2 ma [znany problem] (https://github.com/Azure/WALinuxAgent/pull/517), która powoduje niepowodzenie udostępniania dla maszyny Wirtualnej FreeBSD na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ad811-160">The [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.2 has a [known issue] (https://github.com/Azure/WALinuxAgent/pull/517) that causes the provision failure for FreeBSD VM on Azure.</span></span> <span data-ttu-id="ad811-161">Ta poprawka została przechwycona przez [Agent gościa maszyny Wirtualnej Azure](https://github.com/Azure/WALinuxAgent/) wersji 2.2.3 i jego nowszych wersjach.</span><span class="sxs-lookup"><span data-stu-id="ad811-161">The fix was captured by [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.3 and later releases.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ad811-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ad811-162">Next steps</span></span>
* <span data-ttu-id="ad811-163">Przejdź do [portalu Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) tworzenie FreeBSD maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ad811-163">Go to [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) to create a FreeBSD VM.</span></span>
* <span data-ttu-id="ad811-164">Jeśli chcesz przełączyć własne FreeBSD na platformie Azure, zobacz [tworzenie i przekazywanie wirtualnego dysku twardego FreeBSD na platformie Azure](classic/freebsd-create-upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="ad811-164">If you want to bring your own FreeBSD to Azure, refer to [Create and upload a FreeBSD VHD to Azure](classic/freebsd-create-upload-vhd.md).</span></span>
