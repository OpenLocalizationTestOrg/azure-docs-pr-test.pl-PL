---
title: "aaaAdd tooa użytkownika maszyny Wirtualnej systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dodaj użytkownika tooa maszyny Wirtualnej systemu Linux na platformie Azure."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8aa633b-8b75-45d7-b61d-11ac112cedd5
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/18/2016
ms.author: v-livech
ms.openlocfilehash: eed050154adf0cbed2c168e7aa675bd3ded85fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-user-tooan-azure-vm"></a><span data-ttu-id="b564d-103">Dodaj użytkownika tooan maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="b564d-103">Add a user tooan Azure VM</span></span>
<span data-ttu-id="b564d-104">Jednym z pierwszego zadania hello na nowej maszyny Wirtualnej z systemem Linux jest toocreate nowego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b564d-104">One of hello first tasks on any new Linux VM is toocreate a new user.</span></span>  <span data-ttu-id="b564d-105">W tym artykule, firma Microsoft przeprowadzenie Tworzenie konta użytkownika sudo, ustawienia hello hasła, dodawanie SSH kluczy publicznych, a na koniec użyj `visudo` sudo tooallow bez podania hasła.</span><span class="sxs-lookup"><span data-stu-id="b564d-105">In this article, we walk through creating a sudo user account, setting hello password, adding SSH Public Keys, and finally use `visudo` tooallow sudo without a password.</span></span>

<span data-ttu-id="b564d-106">Wymagania wstępne są: [konta platformy Azure](https://azure.microsoft.com/pricing/free-trial/), [kluczy publicznych i prywatnych SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), grupy zasobów platformy Azure i hello Azure CLI zainstalowany i wyłączyć przy użyciu tryb usługi Resource Manager tooAzure `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="b564d-106">Prerequisites are: [an Azure account](https://azure.microsoft.com/pricing/free-trial/), [SSH public and private keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), an Azure resource group, and hello Azure CLI installed and switched tooAzure Resource Manager mode using `azure config mode arm`.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="b564d-107">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="b564d-107">Quick Commands</span></span>
```bash
# Add a new user on RedHat family distros
sudo useradd -G wheel exampleUser

# Add a new user on Debian family distros
sudo useradd -G sudo exampleUser

# Set a password
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully

# Copy hello SSH Public Key toohello new user
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver

# Change sudoers tooallow no password
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL

# Verify everything
# Verify hello SSH keys & User account
bill@slackware$ ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="b564d-108">Szczegółowy przewodnik</span><span class="sxs-lookup"><span data-stu-id="b564d-108">Detailed Walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="b564d-109">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="b564d-109">Introduction</span></span>
<span data-ttu-id="b564d-110">Jednym z hello pierwsze i najbardziej typowych zadań z nowym serwerze jest tooadd konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b564d-110">One of hello first and most common task with a new server is tooadd a user account.</span></span>  <span data-ttu-id="b564d-111">Główny logowania powinny być wyłączone i nie należy używać konta głównego hello się z serwerem systemu Linux, tylko sudo.</span><span class="sxs-lookup"><span data-stu-id="b564d-111">Root logins should be disabled and hello root account itself should not be used with your Linux server, only sudo.</span></span>  <span data-ttu-id="b564d-112">Nadanie uprawnień przy użyciu funkcji sudo hello właściwy sposób tooadminister i użyj Linux eskalacji głównego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b564d-112">Giving a user root escalation privileges using sudo it hello proper way tooadminister and use Linux.</span></span>

<span data-ttu-id="b564d-113">Za pomocą polecenia hello `useradd` dodajemy toohello konta użytkownika maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="b564d-113">Using hello command `useradd` we are adding user accounts toohello Linux VM.</span></span>  <span data-ttu-id="b564d-114">Uruchomiona `useradd` modyfikuje `/etc/passwd`, `/etc/shadow`, `/etc/group`, i `/etc/gshadow`.</span><span class="sxs-lookup"><span data-stu-id="b564d-114">Running `useradd` modifies `/etc/passwd`, `/etc/shadow`, `/etc/group`, and `/etc/gshadow`.</span></span>  <span data-ttu-id="b564d-115">Dodajemy toohello flagi wiersza polecenia `useradd` polecenia tooalso dodać hello nowej toohello sudo odpowiednie grupy użytkowników w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="b564d-115">We are adding a command-line flag toohello `useradd` command tooalso add hello new user toohello proper sudo group on Linux.</span></span>  <span data-ttu-id="b564d-116">Nawet są jak `useradd` tworzy wejścia `/etc/passwd` nie daje hello nowego konta użytkownika hasła.</span><span class="sxs-lookup"><span data-stu-id="b564d-116">Even thou `useradd` creates an entry into `/etc/passwd` it does not give hello new user account a password.</span></span>  <span data-ttu-id="b564d-117">Tworzenie początkowej hasło dla nowego użytkownika hello przy użyciu prostego powitania `passwd` polecenia.</span><span class="sxs-lookup"><span data-stu-id="b564d-117">We are creating an initial password for hello new user using hello simple `passwd` command.</span></span>  <span data-ttu-id="b564d-118">ostatni krok Hello jest toomodify hello sudo zasady tooallow polecenia tooexecute tego użytkownika z uprawnieniami sudo bez konieczności tooenter hasła dla każdego polecenia.</span><span class="sxs-lookup"><span data-stu-id="b564d-118">hello last step is toomodify hello sudo rules tooallow that user tooexecute commands with sudo privileges without having tooenter a password for every command.</span></span>  <span data-ttu-id="b564d-119">Zalogował się przy użyciu klucza prywatnego hello przyjęto, że konto użytkownika jest zabezpieczony przed nieupoważnione i będą tooallow sudo dostępu bez podania hasła.</span><span class="sxs-lookup"><span data-stu-id="b564d-119">Logging in using hello Private key we are assuming that user account is safe from bad actors and are going tooallow sudo access without a password.</span></span>  

### <a name="adding-a-single-sudo-user-tooan-azure-vm"></a><span data-ttu-id="b564d-120">Dodawanie tooan użytkownika sudo jednej maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="b564d-120">Adding a single sudo user tooan Azure VM</span></span>
<span data-ttu-id="b564d-121">Zaloguj się za toohello maszyna wirtualna platformy Azure przy użyciu kluczy SSH.</span><span class="sxs-lookup"><span data-stu-id="b564d-121">Log in toohello Azure VM using SSH keys.</span></span>  <span data-ttu-id="b564d-122">Jeśli masz nie konfiguracji SSH publiczny dostęp do klucza, najpierw zostało wykonane w tym artykule [przy użyciu publicznego klucza uwierzytelniania za pomocą usługi Azure](http://link.to/article).</span><span class="sxs-lookup"><span data-stu-id="b564d-122">If you have not setup SSH public key access, complete this article first [Using Public Key Authentication with Azure](http://link.to/article).</span></span>  

<span data-ttu-id="b564d-123">Witaj `useradd` hello zadania po zakończeniu wykonywania polecenia:</span><span class="sxs-lookup"><span data-stu-id="b564d-123">hello `useradd` command completes hello following tasks:</span></span>

* <span data-ttu-id="b564d-124">Utwórz nowe konto użytkownika</span><span class="sxs-lookup"><span data-stu-id="b564d-124">create a new user account</span></span>
* <span data-ttu-id="b564d-125">Utwórz nową grupę użytkowników o hello samej nazwie</span><span class="sxs-lookup"><span data-stu-id="b564d-125">create a new user group with hello same name</span></span>
* <span data-ttu-id="b564d-126">Dodaj zbyt jest puste`/etc/passwd`</span><span class="sxs-lookup"><span data-stu-id="b564d-126">add a blank entry too`/etc/passwd`</span></span>
* <span data-ttu-id="b564d-127">Dodaj zbyt jest puste`/etc/gpasswd`</span><span class="sxs-lookup"><span data-stu-id="b564d-127">add a blank entry too`/etc/gpasswd`</span></span>

<span data-ttu-id="b564d-128">Witaj `-G` wiersza polecenia Flaga dodaje hello nowego konta toohello właściwego Linux grupy użytkowników nadanie hello nowego konta użytkownika uprawnień eskalacji głównego.</span><span class="sxs-lookup"><span data-stu-id="b564d-128">hello `-G` command-line flag adds hello new user account toohello proper Linux group giving hello new user account root escalation privileges.</span></span>

#### <a name="add-hello-user"></a><span data-ttu-id="b564d-129">Dodaj użytkownika hello</span><span class="sxs-lookup"><span data-stu-id="b564d-129">Add hello user</span></span>
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a><span data-ttu-id="b564d-130">Ustawienia hasła</span><span class="sxs-lookup"><span data-stu-id="b564d-130">Set a password</span></span>
<span data-ttu-id="b564d-131">Witaj `useradd` polecenie tworzy hello użytkownika i dodaje wpis tooboth `/etc/passwd` i `/etc/gpasswd` , ale faktycznie nie ustawia hasło hello.</span><span class="sxs-lookup"><span data-stu-id="b564d-131">hello `useradd` command creates hello user and adds an entry tooboth `/etc/passwd` and `/etc/gpasswd` but does not actually set hello password.</span></span>  <span data-ttu-id="b564d-132">Witaj hasło zostanie dodany wpis toohello przy użyciu hello `passwd` polecenia.</span><span class="sxs-lookup"><span data-stu-id="b564d-132">hello password is added toohello entry using hello `passwd` command.</span></span>

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

<span data-ttu-id="b564d-133">Mamy teraz użytkownik z uprawnieniami sudo na powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="b564d-133">We now have a user with sudo privileges on hello server.</span></span>

### <a name="add-your-ssh-public-key-toohello-new-user-account"></a><span data-ttu-id="b564d-134">Dodaj klucz publiczny SSH toohello nowe konto użytkownika</span><span class="sxs-lookup"><span data-stu-id="b564d-134">Add your SSH Public Key toohello new user account</span></span>
<span data-ttu-id="b564d-135">Na komputerze, użyj hello `ssh-copy-id` z hello nowe hasło.</span><span class="sxs-lookup"><span data-stu-id="b564d-135">From your machine, use hello `ssh-copy-id` command with hello new password.</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-tooallow-sudo-usage-without-a-password"></a><span data-ttu-id="b564d-136">Użycie sudo tooallow visudo bez hasła</span><span class="sxs-lookup"><span data-stu-id="b564d-136">Using visudo tooallow sudo usage without a password</span></span>
<span data-ttu-id="b564d-137">Przy użyciu `visudo` tooedit hello `/etc/sudoers` file dodaje kilka warstwy ochrony przed niepoprawnie modyfikowanie tego pliku ważne.</span><span class="sxs-lookup"><span data-stu-id="b564d-137">Using `visudo` tooedit hello `/etc/sudoers` file adds a few layers of protection against incorrectly modifying this important file.</span></span>  <span data-ttu-id="b564d-138">Podczas wykonywania `visudo`, hello `/etc/sudoers` plik jest zablokowany tooensure żaden inny użytkownik może wprowadzić zmiany, gdy jest aktywnie edytowany.</span><span class="sxs-lookup"><span data-stu-id="b564d-138">Upon executing `visudo`, hello `/etc/sudoers` file is locked tooensure no other user can make changes while it is actively being edited.</span></span>  <span data-ttu-id="b564d-139">Witaj `/etc/sudoers` pliku jest również sprawdzane pod kątem błędów przez `visudo` podczas prób toosave lub zamknąć, więc nie można zapisać pliku sudoers przerwane.</span><span class="sxs-lookup"><span data-stu-id="b564d-139">hello `/etc/sudoers` file is also checked for mistakes by `visudo` when you attempt toosave or exit so you cannot save a broken sudoers file.</span></span>

<span data-ttu-id="b564d-140">Mamy już użytkowników w grupie poprawne hello dostępu sudo.</span><span class="sxs-lookup"><span data-stu-id="b564d-140">We already have users in hello correct default group for sudo access.</span></span>  <span data-ttu-id="b564d-141">Teraz zamierzamy tooenable sudo toouse tych grup bez hasła.</span><span class="sxs-lookup"><span data-stu-id="b564d-141">Now we are going tooenable those groups toouse sudo with no password.</span></span>

```bash
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL
```

### <a name="verify-hello-user-ssh-keys-and-sudo"></a><span data-ttu-id="b564d-142">Sprawdź użytkownika hello ssh kluczy i operacji sudo</span><span class="sxs-lookup"><span data-stu-id="b564d-142">Verify hello user, ssh keys, and sudo</span></span>
```bash
# Verify hello SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
