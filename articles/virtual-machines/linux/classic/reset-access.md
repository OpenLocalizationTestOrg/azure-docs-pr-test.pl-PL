---
title: "Resetowanie hasła maszyny Wirtualnej systemu Linux i klucz SSH z poziomu interfejsu wiersza polecenia | Dokumentacja firmy Microsoft"
description: "Resetowanie hasła maszyny Wirtualnej systemu Linux lub klucza SSH, popraw konfigurację SSH i sprawdzanie spójności dysku przy użyciu rozszerzenia VMAccess z Azure interfejsu wiersza polecenia (CLI)"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d975eb70-5ff1-40d1-a634-8dd2646dcd17
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: cynthn
ms.openlocfilehash: 74765877e7836d6878284b350a25d8355dc83d7d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-a-linux-vm-password-or-ssh-key-fix-the-ssh-configuration-and-check-disk-consistency-using-the-vmaccess-extension"></a><span data-ttu-id="77529-103">Jak można zresetować hasła maszyny Wirtualnej systemu Linux lub klucza SSH, popraw konfigurację SSH i sprawdzanie spójności dysku przy użyciu rozszerzenia VMAccess</span><span class="sxs-lookup"><span data-stu-id="77529-103">How to reset a Linux VM password or SSH key, fix the SSH configuration, and check disk consistency using the VMAccess extension</span></span>
<span data-ttu-id="77529-104">Nie można połączyć z maszyną wirtualną systemu Linux na platformie Azure z powodu zapomniane hasło, nieprawidłowy klucz Secure Shell (SSH), lub na problem z konfiguracją SSH za pomocą rozszerzenia VMAccessForLinux z wiersza polecenia platformy Azure można zresetować hasła lub klucza SSH, napraw SSH Konfiguracja i sprawdzania spójności dysku.</span><span class="sxs-lookup"><span data-stu-id="77529-104">If you can't connect to a Linux virtual machine on Azure because of a forgotten password, an incorrect Secure Shell (SSH) key, or a problem with the SSH configuration, use the VMAccessForLinux extension with the Azure CLI to reset the password or SSH key, fix the SSH configuration, and check disk consistency.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="77529-105">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="77529-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="77529-106">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="77529-106">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="77529-107">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="77529-107">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="77529-108">Dowiedz się, jak [wykonać te kroki przy użyciu modelu usługi Resource Manager](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="77529-108">Learn how to [perform these steps using the Resource Manager model](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span>

<span data-ttu-id="77529-109">Z wiersza polecenia platformy Azure, użyj **zestaw rozszerzenia maszyny wirtualnej azure** polecenie do dostępu do poleceń interfejsu wiersza polecenia (Bash, terminali, wiersza polecenia).</span><span class="sxs-lookup"><span data-stu-id="77529-109">With the Azure CLI, you use the **azure vm extension set** command from your command-line interface (Bash, Terminal, Command prompt) to access commands.</span></span> <span data-ttu-id="77529-110">Uruchom **zestaw rozszerzenia maszyny wirtualnej azure pomocy** użycia szczegółowe rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="77529-110">Run **azure help vm extension set** for detailed extension usage.</span></span>

<span data-ttu-id="77529-111">Z wiersza polecenia platformy Azure możesz wykonać następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="77529-111">With the Azure CLI, you can do the following tasks:</span></span>

* [<span data-ttu-id="77529-112">Resetowanie hasła</span><span class="sxs-lookup"><span data-stu-id="77529-112">Reset the password</span></span>](#pwresetcli)
* [<span data-ttu-id="77529-113">Resetuj klucz SSH</span><span class="sxs-lookup"><span data-stu-id="77529-113">Reset the SSH key</span></span>](#sshkeyresetcli)
* [<span data-ttu-id="77529-114">Resetowanie hasła i klucza SSH</span><span class="sxs-lookup"><span data-stu-id="77529-114">Reset the password and the SSH key</span></span>](#resetbothcli)
* [<span data-ttu-id="77529-115">Utwórz nowe konto użytkownika sudo</span><span class="sxs-lookup"><span data-stu-id="77529-115">Create a new sudo user account</span></span>](#createnewsudocli)
* [<span data-ttu-id="77529-116">Zresetuj konfigurację protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="77529-116">Reset the SSH configuration</span></span>](#sshconfigresetcli)
* [<span data-ttu-id="77529-117">Usuń użytkownika</span><span class="sxs-lookup"><span data-stu-id="77529-117">Delete a user</span></span>](#deletecli)
* [<span data-ttu-id="77529-118">Wyświetla stan rozszerzenia VMAccess</span><span class="sxs-lookup"><span data-stu-id="77529-118">Display the status of the VMAccess extension</span></span>](#statuscli)
* [<span data-ttu-id="77529-119">Sprawdzanie spójności dodanych dysków</span><span class="sxs-lookup"><span data-stu-id="77529-119">Check consistency of added disks</span></span>](#checkdisk)
* [<span data-ttu-id="77529-120">Napraw dodane dyski na maszynie Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="77529-120">Repair added disks on your Linux VM</span></span>](#repairdisk)

## <a name="prerequisites"></a><span data-ttu-id="77529-121">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="77529-121">Prerequisites</span></span>
<span data-ttu-id="77529-122">Należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="77529-122">You will need to do the following:</span></span>

* <span data-ttu-id="77529-123">Konieczne będzie [instalowanie interfejsu wiersza polecenia Azure](../../../cli-install-nodejs.md) i [nawiązać połączenia z subskrypcją](../../../xplat-cli-connect.md) korzystać z zasobów platformy Azure skojarzonych z Twoim kontem.</span><span class="sxs-lookup"><span data-stu-id="77529-123">You will need to [install the Azure CLI](../../../cli-install-nodejs.md) and [connect to your subscription](../../../xplat-cli-connect.md) to use Azure resources associated with your account.</span></span>
* <span data-ttu-id="77529-124">Ustaw tryb dla klasycznym modelu wdrażania, wpisując następujące polecenie w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="77529-124">Set the correct mode for the classic deployment model by typing the following at the command prompt:</span></span>
    ``` 
        azure config mode asm
    ```
* <span data-ttu-id="77529-125">Jeśli chcesz przywrócić jedną mają nowe hasło lub zestawu kluczy SSH.</span><span class="sxs-lookup"><span data-stu-id="77529-125">Have a new password or set of SSH keys, if you want to reset either one.</span></span> <span data-ttu-id="77529-126">Nie trzeba je, aby zresetować konfiguracji SSH.</span><span class="sxs-lookup"><span data-stu-id="77529-126">You don't need these if you want to reset the SSH configuration.</span></span>

## <span data-ttu-id="77529-127"><a name="pwresetcli"></a>Resetowanie hasła</span><span class="sxs-lookup"><span data-stu-id="77529-127"><a name="pwresetcli"></a>Reset the password</span></span>
1. <span data-ttu-id="77529-128">Utwórz plik na komputerze o nazwie PrivateConf.json z tych wierszy.</span><span class="sxs-lookup"><span data-stu-id="77529-128">Create a file on your local computer named PrivateConf.json with these lines.</span></span> <span data-ttu-id="77529-129">Zastąp **myUserName** i  **myP@ssW0rd**  z własną nazwę użytkownika i hasło i ustawić własne datę wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="77529-129">Replace **myUserName** and **myP@ssW0rd** with your own user name and password and set your own date for expiration.</span></span>

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. <span data-ttu-id="77529-130">Uruchom to polecenie, zastępując nazwę maszyny wirtualnej dla **myVM**.</span><span class="sxs-lookup"><span data-stu-id="77529-130">Run this command, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <span data-ttu-id="77529-131"><a name="sshkeyresetcli"></a>Resetuj klucz SSH</span><span class="sxs-lookup"><span data-stu-id="77529-131"><a name="sshkeyresetcli"></a>Reset the SSH key</span></span>
1. <span data-ttu-id="77529-132">Utwórz plik o nazwie PrivateConf.json z tych zawartości.</span><span class="sxs-lookup"><span data-stu-id="77529-132">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="77529-133">Zastąp **myUserName** i **mySSHKey** wartościami odpowiednimi informacjami.</span><span class="sxs-lookup"><span data-stu-id="77529-133">Replace the **myUserName** and **mySSHKey** values with your own information.</span></span>

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. <span data-ttu-id="77529-134">Uruchom to polecenie, zastępując nazwę maszyny wirtualnej dla **myVM**.</span><span class="sxs-lookup"><span data-stu-id="77529-134">Run this command, substituting the name of your virtual machine for **myVM**.</span></span>
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <span data-ttu-id="77529-135"><a name="resetbothcli"></a>Zresetuj hasło i klucz SSH</span><span class="sxs-lookup"><span data-stu-id="77529-135"><a name="resetbothcli"></a>Reset both the password and the SSH key</span></span>
1. <span data-ttu-id="77529-136">Utwórz plik o nazwie PrivateConf.json z tych zawartości.</span><span class="sxs-lookup"><span data-stu-id="77529-136">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="77529-137">Zastąp **myUserName**, **mySSHKey** i  **myP@ssW0rd**  wartościami odpowiednimi informacjami.</span><span class="sxs-lookup"><span data-stu-id="77529-137">Replace the **myUserName**, **mySSHKey** and **myP@ssW0rd** values with your own information.</span></span>

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. <span data-ttu-id="77529-138">Uruchom to polecenie, zastępując nazwę maszyny wirtualnej dla **myVM**.</span><span class="sxs-lookup"><span data-stu-id="77529-138">Run this command, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="77529-139"><a name="createnewsudocli"></a>Utwórz nowe konto użytkownika sudo</span><span class="sxs-lookup"><span data-stu-id="77529-139"><a name="createnewsudocli"></a>Create a new sudo user account</span></span>

<span data-ttu-id="77529-140">Jeśli zapomnisz swoją nazwę użytkownika, można użyć rozszerzenia VMAccess do Utwórz nową z urzędem sudo.</span><span class="sxs-lookup"><span data-stu-id="77529-140">If you forget your user name, you can use VMAccess to create a new one with the sudo authority.</span></span> <span data-ttu-id="77529-141">W takim przypadku istniejące nazwę użytkownika i hasło nie zostaną zmodyfikowane.</span><span class="sxs-lookup"><span data-stu-id="77529-141">In this case, the existing user name and password will not be modified.</span></span>

<span data-ttu-id="77529-142">Aby utworzyć nowy użytkownik sudo z dostępem do hasła, należy użyć skryptu w [resetowania hasła](#pwresetcli) i określić nową nazwę użytkownika.</span><span class="sxs-lookup"><span data-stu-id="77529-142">To create a new sudo user with password access, use the script in [Reset the password](#pwresetcli) and specify the new user name.</span></span>

<span data-ttu-id="77529-143">Aby utworzyć nowego użytkownika sudo z dostępu do klucza SSH, należy użyć skryptu w [Resetuj klucz SSH](#sshkeyresetcli) i określić nową nazwę użytkownika.</span><span class="sxs-lookup"><span data-stu-id="77529-143">To create a new sudo user with SSH key access, use the script in [Reset the SSH key](#sshkeyresetcli) and specify the new user name.</span></span>

<span data-ttu-id="77529-144">Można również użyć [resetowania hasła i klucza SSH](#resetbothcli) do utworzenia nowego użytkownika z hasła i dostęp do klucza SSH.</span><span class="sxs-lookup"><span data-stu-id="77529-144">You can also use [Reset the password and the SSH key](#resetbothcli) to create a new user with both password and SSH key access.</span></span>

## <span data-ttu-id="77529-145"><a name="sshconfigresetcli"></a>Zresetuj konfigurację protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="77529-145"><a name="sshconfigresetcli"></a>Reset the SSH configuration</span></span>
<span data-ttu-id="77529-146">Jeśli konfiguracji SSH jest w stanie niepożądane, użytkownik może również utracić dostęp do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="77529-146">If the SSH configuration is in an undesired state, you might also lose access to the VM.</span></span> <span data-ttu-id="77529-147">Można użyć rozszerzenia VMAccess do zresetowania konfiguracji do stanu domyślnego.</span><span class="sxs-lookup"><span data-stu-id="77529-147">You can use the VMAccess extension to reset the configuration to its default state.</span></span> <span data-ttu-id="77529-148">W tym celu wystarczy ustawić klucza "reset_ssh" na "True".</span><span class="sxs-lookup"><span data-stu-id="77529-148">To do so, you just need to set the “reset_ssh” key to “True”.</span></span> <span data-ttu-id="77529-149">Rozszerzenia Uruchom ponownie serwer SSH, otwórz port SSH na maszynie Wirtualnej i zresetowanie konfiguracji SSH do wartości domyślnych.</span><span class="sxs-lookup"><span data-stu-id="77529-149">The extension will restart the SSH server, open the SSH port on your VM, and reset the SSH configuration to default values.</span></span> <span data-ttu-id="77529-150">Konto użytkownika (nazwy, hasła lub kluczy SSH) nie zostaną zmienione.</span><span class="sxs-lookup"><span data-stu-id="77529-150">The user account (name, password or SSH keys) will not be changed.</span></span>

> [!NOTE]
> <span data-ttu-id="77529-151">Plik konfiguracji SSH, który pobiera zresetować znajduje się w /etc/ssh/sshd_config.</span><span class="sxs-lookup"><span data-stu-id="77529-151">The SSH configuration file that gets reset is located at /etc/ssh/sshd_config.</span></span>
> 
> 

1. <span data-ttu-id="77529-152">Utwórz plik o nazwie PrivateConf.json z tą zawartością.</span><span class="sxs-lookup"><span data-stu-id="77529-152">Create a file named PrivateConf.json with this content.</span></span>

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. <span data-ttu-id="77529-153">Uruchom to polecenie, zastępując nazwę maszyny wirtualnej dla **myVM**.</span><span class="sxs-lookup"><span data-stu-id="77529-153">Run this command, substituting the name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="77529-154"><a name="deletecli"></a>Usuń użytkownika</span><span class="sxs-lookup"><span data-stu-id="77529-154"><a name="deletecli"></a>Delete a user</span></span>
<span data-ttu-id="77529-155">Jeśli chcesz usunąć konto użytkownika, bez logowania do do maszyny Wirtualnej bezpośrednio, możesz użyć tego skryptu.</span><span class="sxs-lookup"><span data-stu-id="77529-155">If you want to delete a user account without logging into to the VM directly, you can use this script.</span></span>

1. <span data-ttu-id="77529-156">Utwórz plik o nazwie PrivateConf.json z tej zawartości, zastępując nazwę użytkownika, aby usunąć **removeUserName**.</span><span class="sxs-lookup"><span data-stu-id="77529-156">Create a file named PrivateConf.json with this content, substituting the user name to remove for **removeUserName**.</span></span> 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. <span data-ttu-id="77529-157">Uruchom to polecenie, zastępując nazwę maszyny wirtualnej dla **myVM**.</span><span class="sxs-lookup"><span data-stu-id="77529-157">Run this command, substituting the name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="77529-158"><a name="statuscli"></a>Wyświetla stan rozszerzenia VMAccess</span><span class="sxs-lookup"><span data-stu-id="77529-158"><a name="statuscli"></a>Display the status of the VMAccess extension</span></span>
<span data-ttu-id="77529-159">Aby wyświetlić stan rozszerzenia VMAccess, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="77529-159">To display the status of the VMAccess extension, run this command.</span></span>

```
        azure vm extension get
```

## <span data-ttu-id="77529-160"><a name='checkdisk'></a>Sprawdzanie spójności dodanych dysków</span><span class="sxs-lookup"><span data-stu-id="77529-160"><a name='checkdisk'></a>Check consistency of added disks</span></span>
<span data-ttu-id="77529-161">Aby uruchomić fsck na wszystkich dyskach na maszynie wirtualnej systemu Linux, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="77529-161">To run fsck on all disks in your Linux virtual machine, you will need to do the following:</span></span>

1. <span data-ttu-id="77529-162">Utwórz plik o nazwie PublicConf.json z tą zawartością.</span><span class="sxs-lookup"><span data-stu-id="77529-162">Create a file named PublicConf.json with this content.</span></span> <span data-ttu-id="77529-163">Sprawdź, czy dysk przyjmuje wartość logiczną, czy należy sprawdzić dysków dołączonych do maszyny wirtualnej, czy nie.</span><span class="sxs-lookup"><span data-stu-id="77529-163">Check Disk takes a boolean for whether to check disks attached to your virtual machine or not.</span></span> 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. <span data-ttu-id="77529-164">Uruchom to polecenie do wykonania, zastępując nazwę maszyny wirtualnej dla **myVM**.</span><span class="sxs-lookup"><span data-stu-id="77529-164">Run this command to execute, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <span data-ttu-id="77529-165"><a name='repairdisk'></a>Napraw dyski</span><span class="sxs-lookup"><span data-stu-id="77529-165"><a name='repairdisk'></a>Repair disks</span></span>
<span data-ttu-id="77529-166">Aby naprawić dysków, które nie są Instalowanie lub błędy konfiguracji instalacji, należy użyć rozszerzenia VMAccess do zresetowania konfiguracji instalacji na maszynie wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="77529-166">To repair disks that are not mounting or have mount configuration errors, use the VMAccess extension to reset the mount configuration on your Linux virtual machine.</span></span> <span data-ttu-id="77529-167">Zastępując nazwę dysku dla **myDisk**.</span><span class="sxs-lookup"><span data-stu-id="77529-167">Substituting the name of your disk for **myDisk**.</span></span>

1. <span data-ttu-id="77529-168">Utwórz plik o nazwie PublicConf.json z tą zawartością.</span><span class="sxs-lookup"><span data-stu-id="77529-168">Create a file named PublicConf.json with this content.</span></span> 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. <span data-ttu-id="77529-169">Uruchom to polecenie do wykonania, zastępując nazwę maszyny wirtualnej dla **myVM**.</span><span class="sxs-lookup"><span data-stu-id="77529-169">Run this command to execute, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a><span data-ttu-id="77529-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="77529-170">Next steps</span></span>
* <span data-ttu-id="77529-171">Jeśli chcesz użyć poleceń cmdlet programu Azure PowerShell lub szablonów usługi Azure Resource Manager można zresetować hasła lub klucza SSH, zobacz SSH konfiguracji i sprawdzania spójności dysku, napraw [dokumentacją dotyczącą rozszerzenia VMAccess w serwisie GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="77529-171">If you want to use Azure PowerShell cmdlets or Azure Resource Manager templates to reset the password or SSH key, fix the SSH configuration, and check disk consistency, see the [VMAccess extension documentation on GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span> 
* <span data-ttu-id="77529-172">Można również użyć [portalu Azure](https://portal.azure.com) do resetowania hasła lub klucza SSH maszyny wirtualnej systemu Linux wdrożonych w klasycznym modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="77529-172">You can also use the [Azure portal](https://portal.azure.com) to reset the password or SSH key of a Linux VM deployed in the classic deployment model.</span></span> <span data-ttu-id="77529-173">Nie można obecnie używać portalu tej maszyny wirtualnej systemu Linux wdrożonych w modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="77529-173">You can't currently use the portal do to this for a Linux VM deployed in the Resource Manager deployment model.</span></span>
* <span data-ttu-id="77529-174">Zobacz [o rozszerzenia maszyny wirtualnej i funkcjach](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) więcej informacji o przy użyciu rozszerzeń maszyny Wirtualnej dla maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="77529-174">See [About virtual machine extensions and features](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more about using VM extensions for Azure virtual machines.</span></span>

