---
title: "aaaDetailed kroki toocreate SSH parę kluczy dla maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Informacje dodatkowe kroki toocreate SSH publiczne i prywatne parę kluczy dla maszyn wirtualnych systemu Linux na platformie Azure, wraz z określonych certyfikatów dla innych przypadków użycia."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 6/28/2017
ms.author: danlep
ms.openlocfilehash: 9ac52ef4dc87e73b9c07ccc323adc955829e2014
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-walk-through-toocreate-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a><span data-ttu-id="db689-103">Szczegółowe krokach związanych z toocreate parę kluczy SSH i dodatkowych certyfikatów dla maszyny Wirtualnej systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="db689-103">Detailed walk through toocreate an SSH key pair and additional certificates for a Linux VM in Azure</span></span>
<span data-ttu-id="db689-104">Para kluczy SSH umożliwia tworzenie maszyn wirtualnych na platformie Azure, która domyślne toousing kluczy SSH do uwierzytelnienia, eliminując konieczność hello toolog haseł w.</span><span class="sxs-lookup"><span data-stu-id="db689-104">With an SSH key pair, you can create Virtual Machines on Azure that default toousing SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span> <span data-ttu-id="db689-105">Hasła można złamać, a następnie otwórz maszyn wirtualnych się tooguess atakami siłowymi toorelentless hasła.</span><span class="sxs-lookup"><span data-stu-id="db689-105">Passwords can be guessed, and open your VMs up toorelentless brute force attempts tooguess your password.</span></span> <span data-ttu-id="db689-106">Maszyny wirtualne utworzone za pomocą szablonów hello Azure CLI lub Menedżera zasobów mogą zawierać klucz publiczny SSH jako część wdrożenia hello, usuwanie krok konfiguracji wdrożenia post wyłączenia hasło logowania SSH.</span><span class="sxs-lookup"><span data-stu-id="db689-106">VMs created with hello Azure CLI or Resource Manager templates can include your SSH public key as part of hello deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span> <span data-ttu-id="db689-107">Ten artykuł zawiera szczegółowe kroki i dodatkowe przykłady generowania certyfikatów, takich jak do użycia z maszyn wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="db689-107">This article provides detailed steps and additional examples of generating certificates, such as for use with Linux virtual machines.</span></span> <span data-ttu-id="db689-108">Jeśli chcesz, aby tooquickly tworzenia i używania parę kluczy SSH, zobacz [jak skojarzyć toocreate klucz publiczny i prywatny SSH dla maszyn wirtualnych systemu Linux na platformie Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="db689-108">If you want tooquickly create and use an SSH key pair, see [How toocreate an SSH public and private key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

## <a name="understanding-ssh-keys"></a><span data-ttu-id="db689-109">Informacje o kluczach SSH</span><span class="sxs-lookup"><span data-stu-id="db689-109">Understanding SSH keys</span></span>

<span data-ttu-id="db689-110">Przy użyciu kluczy publicznych i prywatnych SSH jest hello Najprostszym sposobem toolog w tooyour serwerów z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="db689-110">Using SSH public and private keys is hello easiest way toolog in tooyour Linux servers.</span></span> <span data-ttu-id="db689-111">[Kryptografia klucza publicznego](https://en.wikipedia.org/wiki/Public-key_cryptography) zapewnia znacznie bezpieczniejsze toolog sposób w tooyour Linux lub BSD wirtualna na platformie Azure niż hasła, które może być metodą siłową znacznie łatwiej.</span><span class="sxs-lookup"><span data-stu-id="db689-111">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way toolog in tooyour Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

<span data-ttu-id="db689-112">Klucz publiczny można udostępniać wszystkim, ale tylko Ty (lub lokalna infrastruktura zabezpieczeń) posiadasz klucz prywatny.</span><span class="sxs-lookup"><span data-stu-id="db689-112">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="db689-113">powinien mieć klucz prywatny SSH Hello [bardzo bezpieczne hasło](https://www.xkcd.com/936/) (źródło:[xkcd.com](https://xkcd.com)) toosafeguard go.</span><span class="sxs-lookup"><span data-stu-id="db689-113">hello SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) toosafeguard it.</span></span>  <span data-ttu-id="db689-114">To hasło jest po prostu tooaccess hello SSH pliku klucza prywatnego i **nie jest** hello hasło do konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="db689-114">This password is just tooaccess hello private SSH key file and **is not** hello user account password.</span></span>  <span data-ttu-id="db689-115">Po dodaniu klucza SSH tooyour Hasło szyfruje hello klucza prywatnego za pomocą 128-bitowego szyfrowania AES, dzięki czemu hello klucz prywatny jest bezużyteczny bez toodecrypt hasło hello go.</span><span class="sxs-lookup"><span data-stu-id="db689-115">When you add a password tooyour SSH key, it encrypts hello private key using 128-bit AES, so that hello private key is useless without hello password toodecrypt it.</span></span>  <span data-ttu-id="db689-116">Jeśli osoba atakująca kraść klucz prywatny i że klucz nie ma hasła, będą mogli toouse to prywatnego klucza toolog w tooany serwerów, które mają hello odpowiadającym mu kluczem publicznym.</span><span class="sxs-lookup"><span data-stu-id="db689-116">If an attacker stole your private key and that key did not have a password, they would be able toouse that private key toolog in tooany servers that have hello corresponding public key.</span></span>  <span data-ttu-id="db689-117">Zabezpieczenie klucza prywatnego hasłem zapewnia dodatkową warstwę ochronną dla infrastruktury na platformie Azure, a osoba niepowołana nie może go użyć.</span><span class="sxs-lookup"><span data-stu-id="db689-117">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="db689-118">W tym artykule tworzy protokołu SSH w wersji 2 pliku klucza publicznego i prywatnego pary RSA (także klucze "ssh-rsa" tooas określonego), które są zalecane w przypadku wdrożeń za pomocą Menedżera zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="db689-118">This article creates an SSH protocol version 2 RSA public and private key file pair (also referred tooas "ssh-rsa" keys), which are recommended for deployments with Azure Resource Manager.</span></span> <span data-ttu-id="db689-119">*SSH-rsa* klucze są wymagane na powitania [portal](https://portal.azure.com) dla wdrożenia usługi Resource Manager i klasycznym.</span><span class="sxs-lookup"><span data-stu-id="db689-119">*ssh-rsa* keys are required on hello [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="ssh-keys-use-and-benefits"></a><span data-ttu-id="db689-120">Korzystanie z kluczy SSH i ich zalety</span><span class="sxs-lookup"><span data-stu-id="db689-120">SSH keys use and benefits</span></span>

<span data-ttu-id="db689-121">Platforma Azure wymaga co najmniej 2048-bitowego, protokołu SSH w wersji 2 RSA format klucze publiczne i prywatne; Plik klucza publicznego Hello ma hello `.pub` format kontenera.</span><span class="sxs-lookup"><span data-stu-id="db689-121">Azure requires at least 2048-bit, SSH protocol version 2 RSA format public and private keys; hello public key file has hello `.pub` container format.</span></span> <span data-ttu-id="db689-122">użycie kluczy toocreate hello `ssh-keygen`, która najpierw zadaje szereg pytań, a następnie zapisuje klucz prywatny i dopasowany klucz publiczny.</span><span class="sxs-lookup"><span data-stu-id="db689-122">toocreate hello keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="db689-123">Po utworzeniu maszyny Wirtualnej platformy Azure, Azure kopie hello toohello klucza publicznego `~/.ssh/authorized_keys` folderu na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="db689-123">When an Azure VM is created, Azure copies hello public key toohello `~/.ssh/authorized_keys` folder on hello VM.</span></span> <span data-ttu-id="db689-124">Kluczy SSH w `~/.ssh/authorized_keys` są używane toochallenge powitania klienta toomatch hello odpowiedni klucz prywatny na połączenia logowania SSH.</span><span class="sxs-lookup"><span data-stu-id="db689-124">SSH keys in `~/.ssh/authorized_keys` are used toochallenge hello client toomatch hello corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="db689-125">Po utworzeniu maszyny Wirtualnej systemu Linux na platformie Azure przy użyciu kluczy SSH do uwierzytelniania Azure konfiguruje hello SSHD toonot serwera Zezwalaj na hasło logowania, tylko kluczy SSH.</span><span class="sxs-lookup"><span data-stu-id="db689-125">When an Azure Linux VM is created using SSH keys for authentication, Azure configures hello SSHD server toonot allow password logins, only SSH keys.</span></span>  <span data-ttu-id="db689-126">W związku z tym tworzenie maszyn wirtualnych systemu Linux platformy Azure za pomocą kluczy SSH, pomaga zabezpieczyć hello wdrożenia maszyny Wirtualnej i zaoszczędzić hello typowej konfiguracji po wdrożeniu kroku wyłączenie haseł w hello **sshd_config** pliku.</span><span class="sxs-lookup"><span data-stu-id="db689-126">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure hello VM deployment and save yourself hello typical post-deployment configuration step of disabling passwords in hello **sshd_config** file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="db689-127">Korzystanie z programu ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="db689-127">Using ssh-keygen</span></span>

<span data-ttu-id="db689-128">To polecenie umożliwia utworzenie zabezpieczonej (zaszyfrowanej) pary kluczy SSH przy użyciu RSA 2048-bitowego i jest oznaczone jako tooeasily go zidentyfikować.</span><span class="sxs-lookup"><span data-stu-id="db689-128">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented tooeasily identify it.</span></span>  

<span data-ttu-id="db689-129">SSH klucze są domyślnie przechowywane w hello `~/.ssh` katalogu.</span><span class="sxs-lookup"><span data-stu-id="db689-129">SSH keys are by default kept in hello `~/.ssh` directory.</span></span>  <span data-ttu-id="db689-130">Jeśli nie masz `~/.ssh` katalogu, hello `ssh-keygen` polecenie tworzy go dla Ciebie hello odpowiednie uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="db689-130">If you do not have a `~/.ssh` directory, hello `ssh-keygen` command creates it for you with hello correct permissions.</span></span>

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

<span data-ttu-id="db689-131">*Opis polecenia*</span><span class="sxs-lookup"><span data-stu-id="db689-131">*Command explained*</span></span>

<span data-ttu-id="db689-132">`ssh-keygen`= hello program używany toocreate hello kluczy</span><span class="sxs-lookup"><span data-stu-id="db689-132">`ssh-keygen` = hello program used toocreate hello keys</span></span>

<span data-ttu-id="db689-133">`-t rsa`= Typ klucza toocreate, czyli formacie RSA hello [wikipedia][parens na końcu](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `) 
 `-b 2048` = liczba bitów klucza hello</span><span class="sxs-lookup"><span data-stu-id="db689-133">`-t rsa` = type of key toocreate which is hello RSA format [wikipedia][parens at end](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
`-b 2048` = bits of hello key</span></span>

<span data-ttu-id="db689-134">`-C "azureuser@myserver"`= komentarz identyfikację toohello dołączany na końcu hello tooeasily pliku klucza publicznego.</span><span class="sxs-lookup"><span data-stu-id="db689-134">`-C "azureuser@myserver"` = a comment appended toohello end of hello public key file tooeasily identify it.</span></span>  <span data-ttu-id="db689-135">Zwykle adres e-mail jest używany jako komentarz hello, ale można użyć sprawdzą się najlepiej dla infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="db689-135">Normally an email is used as hello comment but you can use whatever works best for your infrastructure.</span></span>

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="db689-136">Wdrażanie klasyczne przy użyciu programu `asm`</span><span class="sxs-lookup"><span data-stu-id="db689-136">Classic deploy using `asm`</span></span>

<span data-ttu-id="db689-137">Jeśli używasz hello klasycznego modelu wdrażania (`asm` trybu w hello interfejsu wiersza polecenia), można użyć klucza publicznego SSH-RSA lub sformatowany RFC4716 klucza w kontenerze pem.</span><span class="sxs-lookup"><span data-stu-id="db689-137">If you are using hello classic deployment model (`asm` mode in hello CLI), you can use an SSH-RSA public key or an RFC4716 formatted key in a pem container.</span></span>  <span data-ttu-id="db689-138">klucz publiczny SSH-RSA Hello jest co został utworzony we wcześniejszej części tego artykułu przy użyciu `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="db689-138">hello SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="db689-139">toocreate RFC4716 sformatowany klucza z istniejącego klucza publicznego SSH:</span><span class="sxs-lookup"><span data-stu-id="db689-139">toocreate a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="db689-140">Przykład polecenia ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="db689-140">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "azureuser@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/azureuser/.ssh/id_rsa.
Your public key has been saved in /home/azureuser/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 azureuser@myserver
hello keys randomart image is:
+--[ RSA 2048]----+
|        o o. .   |
|      E. = .o    |
|      ..o...     |
|     . o....     |
|      o S =      |
|     . + O       |
|      + = =      |
|       o +       |
|        .        |
+-----------------+
```

<span data-ttu-id="db689-141">Zapisane pliki klucza:</span><span class="sxs-lookup"><span data-stu-id="db689-141">Saved key files:</span></span>

`Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="db689-142">Nazwa pary kluczy Hello tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="db689-142">hello key pair name for this article.</span></span>  <span data-ttu-id="db689-143">Para kluczy o nazwie **id_rsa** jest domyślnym hello i niektóre narzędzia mogą wymagać hello **id_rsa** nazwę pliku klucza prywatnego, dobrym pomysłem jest o jeden.</span><span class="sxs-lookup"><span data-stu-id="db689-143">Having a key pair named **id_rsa** is hello default and some tools might expect hello **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="db689-144">katalog Hello `~/.ssh/` jest hello domyślna lokalizacja dla par kluczy SSH i pliku konfiguracyjnego SSH hello.</span><span class="sxs-lookup"><span data-stu-id="db689-144">hello directory `~/.ssh/` is hello default location for SSH key pairs and hello SSH config file.</span></span>  <span data-ttu-id="db689-145">Jeśli nie zostanie określony z pełną ścieżką `ssh-keygen` tworzy hello klucze w hello bieżący katalog roboczy, nie hello domyślne `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="db689-145">If not specified with a full path, `ssh-keygen` creates hello keys in hello current working directory, not hello default `~/.ssh`.</span></span>

<span data-ttu-id="db689-146">Lista hello `~/.ssh` katalogu.</span><span class="sxs-lookup"><span data-stu-id="db689-146">A listing of hello `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

<span data-ttu-id="db689-147">Hasło klucza:</span><span class="sxs-lookup"><span data-stu-id="db689-147">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="db689-148">`ssh-keygen`odwołuje się tooa hasło dla pliku klucza prywatnego hello jako "hasło".</span><span class="sxs-lookup"><span data-stu-id="db689-148">`ssh-keygen` refers tooa password for hello private key file as "a passphrase."</span></span>  <span data-ttu-id="db689-149">Jest *silnie* zalecane tooadd hasło klucza prywatnego tooyour.</span><span class="sxs-lookup"><span data-stu-id="db689-149">It is *strongly* recommended tooadd a password tooyour private key.</span></span> <span data-ttu-id="db689-150">Bez hasła ochrona powitalnych plik klucza każda osoba mająca hello plik może być używany toolog w tooany serwera, który ma hello odpowiadającym mu kluczem publicznym.</span><span class="sxs-lookup"><span data-stu-id="db689-150">Without a password protecting hello key file, anyone with hello file can use it toolog in tooany server that has hello corresponding public key.</span></span> <span data-ttu-id="db689-151">Dodanie hasła (hasło) zapewnia lepszą ochronę w przypadku, gdy osoba niepowołana jest w stanie toogain dostępu tooyour pliku klucza prywatnego, zabezpieczeniu masz czas toochange hello klucze tooauthenticate użytkownik.</span><span class="sxs-lookup"><span data-stu-id="db689-151">Adding a password (passphrase) offers more protection in case someone is able toogain access tooyour private key file, given you time toochange hello keys used tooauthenticate you.</span></span>

## <a name="using-ssh-agent-toostore-your-private-key-password"></a><span data-ttu-id="db689-152">Przy użyciu hasła klucza prywatnego ssh-agent toostore</span><span class="sxs-lookup"><span data-stu-id="db689-152">Using ssh-agent toostore your private key password</span></span>

<span data-ttu-id="db689-153">tooavoid hasło pliku klucza prywatnego przy każdym logowaniu przez protokół SSH, można użyć `ssh-agent` toocache hasło pliku klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="db689-153">tooavoid typing your private key file password with every SSH login, you can use `ssh-agent` toocache your private key file password.</span></span> <span data-ttu-id="db689-154">Jeśli używasz Mac hello łańcucha kluczy systemu OS x przechowuje bezpiecznego hasła do klucza prywatnego powitania po wywołaniu `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="db689-154">If you are using a Mac, hello OSX Keychain securely stores hello private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="db689-155">Sprawdź i użyj ssh-agent ssh — Dodaj tooinform hello SSH system o hello pliki klucza, aby hasło hello nie będzie używane w trybie interakcyjnym toobe.</span><span class="sxs-lookup"><span data-stu-id="db689-155">Verify and use ssh-agent and ssh-add tooinform hello SSH system about hello key files so that hello passphrase will not need toobe used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="db689-156">Teraz Dodaj klucz prywatny hello zbyt`ssh-agent` za pomocą polecenia hello `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="db689-156">Now add hello private key too`ssh-agent` using hello command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="db689-157">hasło klucza prywatnego Hello są obecnie przechowywane w `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="db689-157">hello private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-toocopy-hello-key-tooan-existing-vm"></a><span data-ttu-id="db689-158">Przy użyciu `ssh-copy-id` toocopy hello klucza tooan istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="db689-158">Using `ssh-copy-id` toocopy hello key tooan existing VM</span></span>
<span data-ttu-id="db689-159">Jeśli utworzono już Maszynę wirtualną można zainstalować hello nowe SSH publicznego klucza tooyour maszyny Wirtualnej systemu Linux z:</span><span class="sxs-lookup"><span data-stu-id="db689-159">If you have already created a VM you can install hello new SSH public key tooyour Linux VM with:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="db689-160">Tworzenie i konfigurowanie pliku konfiguracyjnego SSH</span><span class="sxs-lookup"><span data-stu-id="db689-160">Create and configure an SSH config file</span></span>

<span data-ttu-id="db689-161">Jest zalecanym najlepszym toocreate praktyki i skonfigurować `~/.ssh/config` toospeed pliku na górę logowania i optymalizacji Twoje zachowanie klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="db689-161">It is a recommended best practice toocreate and configure an `~/.ssh/config` file toospeed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="db689-162">Poniższy przykład Hello pokazano standardową konfigurację.</span><span class="sxs-lookup"><span data-stu-id="db689-162">hello following example shows a standard configuration.</span></span>

### <a name="create-hello-file"></a><span data-ttu-id="db689-163">Utwórz plik hello</span><span class="sxs-lookup"><span data-stu-id="db689-163">Create hello file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a><span data-ttu-id="db689-164">Edytuj hello pliku tooadd hello nową konfigurację SSH:</span><span class="sxs-lookup"><span data-stu-id="db689-164">Edit hello file tooadd hello new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="db689-165">Przykład pliku `~/.ssh/config`:</span><span class="sxs-lookup"><span data-stu-id="db689-165">Example `~/.ssh/config` file:</span></span>

```bash
# Azure Keys
Host fedora22
  Hostname 102.160.203.241
  User ahmet
# ./Azure Keys
# Default Settings
Host *
  PubkeyAuthentication=yes
  IdentitiesOnly=yes
  ServerAliveInterval=60
  ServerAliveCountMax=30
  ControlMaster auto
  ControlPath ~/.ssh/SSHConnections/ssh-%r@%h:%p
  ControlPersist 4h
  IdentityFile ~/.ssh/id_rsa
```

<span data-ttu-id="db689-166">To konfiguracji SSH umożliwia możesz sekcje dla każdego serwera tooenable każdego toohave własnej pary kluczy.</span><span class="sxs-lookup"><span data-stu-id="db689-166">This SSH config gives you sections for each server tooenable each toohave its own dedicated key pair.</span></span> <span data-ttu-id="db689-167">Witaj ustawienia domyślne (`Host *`) są przeznaczone dla wszystkich hostach, które nie należy do żadnej hello określonych hostach w górę w pliku konfiguracyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="db689-167">hello default settings (`Host *`) are for any hosts that do not match any of hello specific hosts higher up in hello config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="db689-168">Opis pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="db689-168">Config file explained</span></span>

<span data-ttu-id="db689-169">`Host`= Nazwa hello hello hosta wywołanego na powitania w terminalu.</span><span class="sxs-lookup"><span data-stu-id="db689-169">`Host` = hello name of hello host being called on hello terminal.</span></span>  <span data-ttu-id="db689-170">`ssh fedora22`Określa, że `SSH` toouse hello wartości w bloku ustawienia hello etykietą `Host fedora22` Uwaga: Host może być jakakolwiek etykieta jest dla Ciebie, który nie reprezentuje hello rzeczywiste nazwą hosta żadnego serwera.</span><span class="sxs-lookup"><span data-stu-id="db689-170">`ssh fedora22` tells `SSH` toouse hello values in hello settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent hello actual hostname of any server.</span></span>

<span data-ttu-id="db689-171">`Hostname 102.160.203.241`= hello adres IP lub nazwa DNS serwera hello.</span><span class="sxs-lookup"><span data-stu-id="db689-171">`Hostname 102.160.203.241` = hello IP address or DNS name for hello server being accessed.</span></span>

<span data-ttu-id="db689-172">`User ahmet`= toouse konta użytkownika zdalnego hello podczas logowania się na serwerze toohello.</span><span class="sxs-lookup"><span data-stu-id="db689-172">`User ahmet` = hello remote user account toouse when logging in toohello server.</span></span>

<span data-ttu-id="db689-173">`PubKeyAuthentication yes`= informuje protokół SSH, mają toouse toolog klucza SSH.</span><span class="sxs-lookup"><span data-stu-id="db689-173">`PubKeyAuthentication yes` = tells SSH you want toouse an SSH key toolog in.</span></span>

<span data-ttu-id="db689-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa`= klucza prywatnego SSH hello i odpowiednie toouse klucza publicznego dla uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="db689-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = hello SSH private key and corresponding public key toouse for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="db689-175">Korzystanie z protokołu SSH w systemie Linux bez użycia hasła</span><span class="sxs-lookup"><span data-stu-id="db689-175">SSH into Linux without a password</span></span>

<span data-ttu-id="db689-176">Teraz, gdy masz parę kluczy SSH i skonfigurowany plik konfiguracji SSH są możliwe toolog w tooyour maszyny Wirtualnej systemu Linux szybkie i bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="db689-176">Now that you have an SSH key pair and a configured SSH config file, you are able toolog in tooyour Linux VM quickly and securely.</span></span> <span data-ttu-id="db689-177">powitania po raz pierwszy logujesz się tooa serwera przy użyciu hello klucza SSH polecenie monituje możesz dla hello hasło dla tego pliku klucza.</span><span class="sxs-lookup"><span data-stu-id="db689-177">hello first time you log in tooa server using an SSH key hello command prompts you for hello passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="db689-178">Opis polecenia</span><span class="sxs-lookup"><span data-stu-id="db689-178">Command explained</span></span>

<span data-ttu-id="db689-179">Gdy `ssh fedora22` jest wykonywany SSH najpierw lokalizuje i ładuje wszystkie ustawienia z hello `Host fedora22` bloku, a następnie obciążeń hello wszystkie pozostałe ustawienia z ostatniego bloku hello `Host *`.</span><span class="sxs-lookup"><span data-stu-id="db689-179">When `ssh fedora22` is executed SSH first locates and loads any settings from hello `Host fedora22` block, and then loads all hello remaining settings from hello last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db689-180">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="db689-180">Next Steps</span></span>

<span data-ttu-id="db689-181">Następnie się jest toocreate maszyn wirtualnych systemu Linux platformy Azure przy użyciu nowego klucza publicznego hello SSH.</span><span class="sxs-lookup"><span data-stu-id="db689-181">Next up is toocreate Azure Linux VMs using hello new SSH public key.</span></span>  <span data-ttu-id="db689-182">Maszyny wirtualne platformy Azure utworzonych za pomocą klucza publicznego SSH jako hello logowania są lepiej zabezpieczone niż maszyny wirtualne utworzone przy użyciu metody logowania hello domyślne hasła.</span><span class="sxs-lookup"><span data-stu-id="db689-182">Azure VMs that are created with an SSH public key as hello login are better secured than VMs created with hello default login method, passwords.</span></span>  <span data-ttu-id="db689-183">W domyślnej konfiguracji maszyn wirtualnych platformy Azure utworzonych przy użyciu kluczy SSH hasła są wyłączone, aby uniknąć prób odgadnięcia hasła za pomocą ataków siłowych.</span><span class="sxs-lookup"><span data-stu-id="db689-183">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span>

* [<span data-ttu-id="db689-184">Tworzenie bezpiecznej maszyny wirtualnej systemu Linux przy użyciu szablonu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="db689-184">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="db689-185">Tworzenie bezpiecznej maszyny Wirtualnej systemu Linux przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="db689-185">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="db689-186">Tworzenie bezpiecznej maszyny Wirtualnej systemu Linux przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="db689-186">Create a secure Linux VM using hello Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
