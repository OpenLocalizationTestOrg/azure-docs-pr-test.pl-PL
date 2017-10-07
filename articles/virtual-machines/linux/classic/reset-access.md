---
title: "aaaReset hasła maszyny Wirtualnej systemu Linux i SSH klucz z hello interfejsu wiersza polecenia | Dokumentacja firmy Microsoft"
description: "Jak hello toouse rozszerzenia VMAccess z hello Azure interfejsu wiersza polecenia (CLI) tooreset maszyny Wirtualnej systemu Linux hasła lub klucza SSH, popraw konfigurację SSH hello i sprawdzanie spójności dysku"
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
ms.openlocfilehash: 1650ad64fb982627ae9f90b1a8209bb56bac7004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-a-linux-vm-password-or-ssh-key-fix-hello-ssh-configuration-and-check-disk-consistency-using-hello-vmaccess-extension"></a><span data-ttu-id="fdf87-103">Jak tooreset maszyny Wirtualnej systemu Linux hasła lub klucza SSH, popraw konfigurację SSH hello i sprawdzanie spójności dysku przy użyciu rozszerzenia VMAccess hello</span><span class="sxs-lookup"><span data-stu-id="fdf87-103">How tooreset a Linux VM password or SSH key, fix hello SSH configuration, and check disk consistency using hello VMAccess extension</span></span>
<span data-ttu-id="fdf87-104">Jeśli nie możesz połączyć tooa maszyny wirtualnej systemu Linux na platformie Azure z powodu zapomniane hasło, nieprawidłowy klucz Secure Shell (SSH) lub na problem z konfiguracją SSH hello, hello rozszerzenia VMAccessForLinux za pomocą hello Azure CLI tooreset hello hasła lub klucza SSH, napraw Witaj konfiguracji SSH i sprawdzanie spójności dysku.</span><span class="sxs-lookup"><span data-stu-id="fdf87-104">If you can't connect tooa Linux virtual machine on Azure because of a forgotten password, an incorrect Secure Shell (SSH) key, or a problem with hello SSH configuration, use hello VMAccessForLinux extension with hello Azure CLI tooreset hello password or SSH key, fix hello SSH configuration, and check disk consistency.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="fdf87-105">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fdf87-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fdf87-106">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="fdf87-106">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="fdf87-107">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fdf87-107">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="fdf87-108">Dowiedz się, jak za[wykonaj te czynności przy użyciu modelu Resource Manager hello](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="fdf87-108">Learn how too[perform these steps using hello Resource Manager model](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span>

<span data-ttu-id="fdf87-109">Hello wiersza polecenia platformy Azure, możesz za pomocą hello **zestaw rozszerzenia maszyny wirtualnej azure** polecenie poleceniach tooaccess interfejsu wiersza polecenia (Bash, terminali, wiersza polecenia).</span><span class="sxs-lookup"><span data-stu-id="fdf87-109">With hello Azure CLI, you use hello **azure vm extension set** command from your command-line interface (Bash, Terminal, Command prompt) tooaccess commands.</span></span> <span data-ttu-id="fdf87-110">Uruchom **zestaw rozszerzenia maszyny wirtualnej azure pomocy** użycia szczegółowe rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="fdf87-110">Run **azure help vm extension set** for detailed extension usage.</span></span>

<span data-ttu-id="fdf87-111">Z hello wiersza polecenia platformy Azure, możesz wykonać hello następujących zadań:</span><span class="sxs-lookup"><span data-stu-id="fdf87-111">With hello Azure CLI, you can do hello following tasks:</span></span>

* [<span data-ttu-id="fdf87-112">Resetowanie hasła hello</span><span class="sxs-lookup"><span data-stu-id="fdf87-112">Reset hello password</span></span>](#pwresetcli)
* [<span data-ttu-id="fdf87-113">Resetuj klucz SSH hello</span><span class="sxs-lookup"><span data-stu-id="fdf87-113">Reset hello SSH key</span></span>](#sshkeyresetcli)
* [<span data-ttu-id="fdf87-114">Resetuj hello hasła i hello klucza SSH</span><span class="sxs-lookup"><span data-stu-id="fdf87-114">Reset hello password and hello SSH key</span></span>](#resetbothcli)
* [<span data-ttu-id="fdf87-115">Utwórz nowe konto użytkownika sudo</span><span class="sxs-lookup"><span data-stu-id="fdf87-115">Create a new sudo user account</span></span>](#createnewsudocli)
* [<span data-ttu-id="fdf87-116">Zresetuj konfigurację protokołu SSH hello</span><span class="sxs-lookup"><span data-stu-id="fdf87-116">Reset hello SSH configuration</span></span>](#sshconfigresetcli)
* [<span data-ttu-id="fdf87-117">Usuń użytkownika</span><span class="sxs-lookup"><span data-stu-id="fdf87-117">Delete a user</span></span>](#deletecli)
* [<span data-ttu-id="fdf87-118">Wyświetl stan hello hello rozszerzenia VMAccess</span><span class="sxs-lookup"><span data-stu-id="fdf87-118">Display hello status of hello VMAccess extension</span></span>](#statuscli)
* [<span data-ttu-id="fdf87-119">Sprawdzanie spójności dodanych dysków</span><span class="sxs-lookup"><span data-stu-id="fdf87-119">Check consistency of added disks</span></span>](#checkdisk)
* [<span data-ttu-id="fdf87-120">Napraw dodane dyski na maszynie Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="fdf87-120">Repair added disks on your Linux VM</span></span>](#repairdisk)

## <a name="prerequisites"></a><span data-ttu-id="fdf87-121">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fdf87-121">Prerequisites</span></span>
<span data-ttu-id="fdf87-122">Potrzebne są następujące hello toodo:</span><span class="sxs-lookup"><span data-stu-id="fdf87-122">You will need toodo hello following:</span></span>

* <span data-ttu-id="fdf87-123">Konieczne będzie zbyt[zainstalować hello Azure CLI](../../../cli-install-nodejs.md) i [połączenia subskrypcji tooyour](../../../xplat-cli-connect.md) toouse Azure zasoby skojarzone z Twoim kontem.</span><span class="sxs-lookup"><span data-stu-id="fdf87-123">You will need too[install hello Azure CLI](../../../cli-install-nodejs.md) and [connect tooyour subscription](../../../xplat-cli-connect.md) toouse Azure resources associated with your account.</span></span>
* <span data-ttu-id="fdf87-124">Ustaw hello poprawny tryb hello klasycznego modelu wdrażania, wpisując hello następujące polecenie w wierszu polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="fdf87-124">Set hello correct mode for hello classic deployment model by typing hello following at hello command prompt:</span></span>
    ``` 
        azure config mode asm
    ```
* <span data-ttu-id="fdf87-125">Jeśli chcesz, aby tooreset jedną mają nowe hasło lub zestawu kluczy SSH.</span><span class="sxs-lookup"><span data-stu-id="fdf87-125">Have a new password or set of SSH keys, if you want tooreset either one.</span></span> <span data-ttu-id="fdf87-126">Jeśli konfiguracja protokołu SSH hello tooreset nie trzeba je.</span><span class="sxs-lookup"><span data-stu-id="fdf87-126">You don't need these if you want tooreset hello SSH configuration.</span></span>

## <span data-ttu-id="fdf87-127"><a name="pwresetcli"></a>Resetowanie hasła hello</span><span class="sxs-lookup"><span data-stu-id="fdf87-127"><a name="pwresetcli"></a>Reset hello password</span></span>
1. <span data-ttu-id="fdf87-128">Utwórz plik na komputerze o nazwie PrivateConf.json z tych wierszy.</span><span class="sxs-lookup"><span data-stu-id="fdf87-128">Create a file on your local computer named PrivateConf.json with these lines.</span></span> <span data-ttu-id="fdf87-129">Zastąp **myUserName** i  **myP@ssW0rd**  z własną nazwę użytkownika i hasło i ustawić własne datę wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="fdf87-129">Replace **myUserName** and **myP@ssW0rd** with your own user name and password and set your own date for expiration.</span></span>

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. <span data-ttu-id="fdf87-130">Uruchom to polecenie, zastępując nazwę hello maszyny wirtualnej dla **myVM**.</span><span class="sxs-lookup"><span data-stu-id="fdf87-130">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <span data-ttu-id="fdf87-131"><a name="sshkeyresetcli"></a>Resetuj klucz SSH hello</span><span class="sxs-lookup"><span data-stu-id="fdf87-131"><a name="sshkeyresetcli"></a>Reset hello SSH key</span></span>
1. <span data-ttu-id="fdf87-132">Utwórz plik o nazwie PrivateConf.json z tych zawartości.</span><span class="sxs-lookup"><span data-stu-id="fdf87-132">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="fdf87-133">Zastąp hello **myUserName** i **mySSHKey** wartościami odpowiednimi informacjami.</span><span class="sxs-lookup"><span data-stu-id="fdf87-133">Replace hello **myUserName** and **mySSHKey** values with your own information.</span></span>

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. <span data-ttu-id="fdf87-134">Uruchom to polecenie, zastępując nazwę hello maszyny wirtualnej dla **myVM**.</span><span class="sxs-lookup"><span data-stu-id="fdf87-134">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <span data-ttu-id="fdf87-135"><a name="resetbothcli"></a>Zresetuj zarówno hello hasła i hello klucza SSH</span><span class="sxs-lookup"><span data-stu-id="fdf87-135"><a name="resetbothcli"></a>Reset both hello password and hello SSH key</span></span>
1. <span data-ttu-id="fdf87-136">Utwórz plik o nazwie PrivateConf.json z tych zawartości.</span><span class="sxs-lookup"><span data-stu-id="fdf87-136">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="fdf87-137">Zastąp hello **myUserName**, **mySSHKey** i  **myP@ssW0rd**  wartościami odpowiednimi informacjami.</span><span class="sxs-lookup"><span data-stu-id="fdf87-137">Replace hello **myUserName**, **mySSHKey** and **myP@ssW0rd** values with your own information.</span></span>

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. <span data-ttu-id="fdf87-138">Uruchom to polecenie, zastępując nazwę hello maszyny wirtualnej dla **myVM**.</span><span class="sxs-lookup"><span data-stu-id="fdf87-138">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="fdf87-139"><a name="createnewsudocli"></a>Utwórz nowe konto użytkownika sudo</span><span class="sxs-lookup"><span data-stu-id="fdf87-139"><a name="createnewsudocli"></a>Create a new sudo user account</span></span>

<span data-ttu-id="fdf87-140">Jeśli zapomnisz swoją nazwę użytkownika, można użyć rozszerzenia VMAccess toocreate nową z urzędem sudo hello.</span><span class="sxs-lookup"><span data-stu-id="fdf87-140">If you forget your user name, you can use VMAccess toocreate a new one with hello sudo authority.</span></span> <span data-ttu-id="fdf87-141">W takim przypadku hello istniejącej nazwy użytkownika i hasło nie zostaną zmodyfikowane.</span><span class="sxs-lookup"><span data-stu-id="fdf87-141">In this case, hello existing user name and password will not be modified.</span></span>

<span data-ttu-id="fdf87-142">toocreate nowego użytkownika sudo z dostępem do hasła, użyj skryptu hello w [resetowania hasła hello](#pwresetcli) i określić nową nazwę użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="fdf87-142">toocreate a new sudo user with password access, use hello script in [Reset hello password](#pwresetcli) and specify hello new user name.</span></span>

<span data-ttu-id="fdf87-143">toocreate nowego użytkownika sudo z dostępem klucza SSH, użyj skryptu hello w [klucza SSH hello resetowania](#sshkeyresetcli) i określić nową nazwę użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="fdf87-143">toocreate a new sudo user with SSH key access, use hello script in [Reset hello SSH key](#sshkeyresetcli) and specify hello new user name.</span></span>

<span data-ttu-id="fdf87-144">Można również użyć [resetowania hasła hello i klucz SSH hello](#resetbothcli) toocreate nowego użytkownika z jednocześnie hasło i dostęp do klucza SSH.</span><span class="sxs-lookup"><span data-stu-id="fdf87-144">You can also use [Reset hello password and hello SSH key](#resetbothcli) toocreate a new user with both password and SSH key access.</span></span>

## <span data-ttu-id="fdf87-145"><a name="sshconfigresetcli"></a>Zresetuj konfigurację protokołu SSH hello</span><span class="sxs-lookup"><span data-stu-id="fdf87-145"><a name="sshconfigresetcli"></a>Reset hello SSH configuration</span></span>
<span data-ttu-id="fdf87-146">Jeśli konfiguracji SSH hello jest w stanie niepożądane, może również utracić toohello dostęp do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fdf87-146">If hello SSH configuration is in an undesired state, you might also lose access toohello VM.</span></span> <span data-ttu-id="fdf87-147">Możesz użyć hello VMAccess rozszerzenia tooreset hello konfiguracji tooits domyślny stan.</span><span class="sxs-lookup"><span data-stu-id="fdf87-147">You can use hello VMAccess extension tooreset hello configuration tooits default state.</span></span> <span data-ttu-id="fdf87-148">toodo tak, wystarczy, że klucz "reset_ssh" hello tooset zbyt "True".</span><span class="sxs-lookup"><span data-stu-id="fdf87-148">toodo so, you just need tooset hello “reset_ssh” key too“True”.</span></span> <span data-ttu-id="fdf87-149">rozszerzenia Hello Uruchom ponownie serwer SSH hello, otwórz port SSH hello na maszynie Wirtualnej i zresetuj wartości toodefault konfiguracji SSH hello.</span><span class="sxs-lookup"><span data-stu-id="fdf87-149">hello extension will restart hello SSH server, open hello SSH port on your VM, and reset hello SSH configuration toodefault values.</span></span> <span data-ttu-id="fdf87-150">konto użytkownika Hello (nazwa, hasło lub kluczy SSH) nie zostaną zmienione.</span><span class="sxs-lookup"><span data-stu-id="fdf87-150">hello user account (name, password or SSH keys) will not be changed.</span></span>

> [!NOTE]
> <span data-ttu-id="fdf87-151">plik konfiguracji SSH Hello pobiera zresetować znajduje się w /etc/ssh/sshd_config.</span><span class="sxs-lookup"><span data-stu-id="fdf87-151">hello SSH configuration file that gets reset is located at /etc/ssh/sshd_config.</span></span>
> 
> 

1. <span data-ttu-id="fdf87-152">Utwórz plik o nazwie PrivateConf.json z tą zawartością.</span><span class="sxs-lookup"><span data-stu-id="fdf87-152">Create a file named PrivateConf.json with this content.</span></span>

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. <span data-ttu-id="fdf87-153">Uruchom to polecenie, zastępując nazwę hello maszyny wirtualnej dla **myVM**.</span><span class="sxs-lookup"><span data-stu-id="fdf87-153">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="fdf87-154"><a name="deletecli"></a>Usuń użytkownika</span><span class="sxs-lookup"><span data-stu-id="fdf87-154"><a name="deletecli"></a>Delete a user</span></span>
<span data-ttu-id="fdf87-155">Jeśli chcesz toodelete konto użytkownika, bez logowania do maszyny Wirtualnej toohello bezpośrednio, można użyć tego skryptu.</span><span class="sxs-lookup"><span data-stu-id="fdf87-155">If you want toodelete a user account without logging into toohello VM directly, you can use this script.</span></span>

1. <span data-ttu-id="fdf87-156">Utwórz plik o nazwie PrivateConf.json z tej zawartości, zastępując hello użytkownika nazwa tooremove dla **removeUserName**.</span><span class="sxs-lookup"><span data-stu-id="fdf87-156">Create a file named PrivateConf.json with this content, substituting hello user name tooremove for **removeUserName**.</span></span> 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. <span data-ttu-id="fdf87-157">Uruchom to polecenie, zastępując nazwę hello maszyny wirtualnej dla **myVM**.</span><span class="sxs-lookup"><span data-stu-id="fdf87-157">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="fdf87-158"><a name="statuscli"></a>Wyświetl stan hello hello rozszerzenia VMAccess</span><span class="sxs-lookup"><span data-stu-id="fdf87-158"><a name="statuscli"></a>Display hello status of hello VMAccess extension</span></span>
<span data-ttu-id="fdf87-159">Stan hello toodisplay hello rozszerzenia VMAccess, uruchom to polecenie.</span><span class="sxs-lookup"><span data-stu-id="fdf87-159">toodisplay hello status of hello VMAccess extension, run this command.</span></span>

```
        azure vm extension get
```

## <span data-ttu-id="fdf87-160"><a name='checkdisk'></a>Sprawdzanie spójności dodanych dysków</span><span class="sxs-lookup"><span data-stu-id="fdf87-160"><a name='checkdisk'></a>Check consistency of added disks</span></span>
<span data-ttu-id="fdf87-161">fsck toorun na wszystkich dyskach na maszynie wirtualnej systemu Linux, potrzebne są następujące hello toodo:</span><span class="sxs-lookup"><span data-stu-id="fdf87-161">toorun fsck on all disks in your Linux virtual machine, you will need toodo hello following:</span></span>

1. <span data-ttu-id="fdf87-162">Utwórz plik o nazwie PublicConf.json z tą zawartością.</span><span class="sxs-lookup"><span data-stu-id="fdf87-162">Create a file named PublicConf.json with this content.</span></span> <span data-ttu-id="fdf87-163">Sprawdź, czy dysk przyjmuje wartość typu boolean dla czy toocheck do niej dołączone dyski maszyny wirtualnej tooyour lub nie.</span><span class="sxs-lookup"><span data-stu-id="fdf87-163">Check Disk takes a boolean for whether toocheck disks attached tooyour virtual machine or not.</span></span> 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. <span data-ttu-id="fdf87-164">Uruchom ten tooexecute polecenie, zastępując nazwę hello maszyny wirtualnej dla **myVM**.</span><span class="sxs-lookup"><span data-stu-id="fdf87-164">Run this command tooexecute, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <span data-ttu-id="fdf87-165"><a name='repairdisk'></a>Napraw dyski</span><span class="sxs-lookup"><span data-stu-id="fdf87-165"><a name='repairdisk'></a>Repair disks</span></span>
<span data-ttu-id="fdf87-166">toorepair dysków, które nie są Instalowanie lub błędy konfiguracji instalacji, użyj hello VMAccess rozszerzenia tooreset hello instalacji konfiguracji na maszynie wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="fdf87-166">toorepair disks that are not mounting or have mount configuration errors, use hello VMAccess extension tooreset hello mount configuration on your Linux virtual machine.</span></span> <span data-ttu-id="fdf87-167">Zastępowanie hello nazwę dysku dla **myDisk**.</span><span class="sxs-lookup"><span data-stu-id="fdf87-167">Substituting hello name of your disk for **myDisk**.</span></span>

1. <span data-ttu-id="fdf87-168">Utwórz plik o nazwie PublicConf.json z tą zawartością.</span><span class="sxs-lookup"><span data-stu-id="fdf87-168">Create a file named PublicConf.json with this content.</span></span> 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. <span data-ttu-id="fdf87-169">Uruchom ten tooexecute polecenie, zastępując nazwę hello maszyny wirtualnej dla **myVM**.</span><span class="sxs-lookup"><span data-stu-id="fdf87-169">Run this command tooexecute, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a><span data-ttu-id="fdf87-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fdf87-170">Next steps</span></span>
* <span data-ttu-id="fdf87-171">Jeśli chcesz poleceń cmdlet programu Azure PowerShell toouse lub usługi Azure Resource Manager szablony tooreset hello hasła lub klucza SSH, popraw konfigurację SSH hello i sprawdzanie spójności dysku, zobacz hello [dokumentacją dotyczącą rozszerzenia VMAccess w serwisie GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="fdf87-171">If you want toouse Azure PowerShell cmdlets or Azure Resource Manager templates tooreset hello password or SSH key, fix hello SSH configuration, and check disk consistency, see hello [VMAccess extension documentation on GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span> 
* <span data-ttu-id="fdf87-172">Można również użyć hello [portalu Azure](https://portal.azure.com) tooreset hello hasła lub klucza SSH maszyny wirtualnej systemu Linux wdrożonych w hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="fdf87-172">You can also use hello [Azure portal](https://portal.azure.com) tooreset hello password or SSH key of a Linux VM deployed in hello classic deployment model.</span></span> <span data-ttu-id="fdf87-173">Nie można aktualnie użyć hello toothis portalu dla maszyny Wirtualnej systemu Linux wdrożonych w modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="fdf87-173">You can't currently use hello portal do toothis for a Linux VM deployed in hello Resource Manager deployment model.</span></span>
* <span data-ttu-id="fdf87-174">Zobacz [o rozszerzenia maszyny wirtualnej i funkcjach](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) więcej informacji o przy użyciu rozszerzeń maszyny Wirtualnej dla maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fdf87-174">See [About virtual machine extensions and features](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more about using VM extensions for Azure virtual machines.</span></span>

