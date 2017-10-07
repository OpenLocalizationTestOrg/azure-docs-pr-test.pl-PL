---
title: "aaaCreate SSH parę kluczy dla maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Bezpiecznie utwórz parę kluczy SSH, prywatny i publiczny, dla maszyn wirtualnych z systemem Linux."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: rasquill
ms.openlocfilehash: c4c7cec77c9b48295f2a28c8179b30a4dc38a555
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a><span data-ttu-id="d4206-103">Tworzenie pary kluczy prywatnych i publicznych SSH dla maszyn wirtualnych z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="d4206-103">Create an SSH public and private key pair for Linux VMs</span></span>

<span data-ttu-id="d4206-104">W tym artykule opisano, jak toogenerate protocol w wersji 2 RSA publicznego i prywatnego klucza SSH pliku toouse pary maszyn wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="d4206-104">This article shows you how toogenerate an SSH protocol version 2 RSA public and private key file pair toouse with Linux VMs.</span></span>  <span data-ttu-id="d4206-105">Para kluczy SSH umożliwia tworzenie maszyn wirtualnych na platformie Azure, która domyślne toousing kluczy SSH do uwierzytelnienia, eliminując konieczność hello toolog haseł w.</span><span class="sxs-lookup"><span data-stu-id="d4206-105">With an SSH key pair, you can create Virtual Machines on Azure that default toousing SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span>  <span data-ttu-id="d4206-106">Hasła można złamać, a następnie otwórz maszyn wirtualnych się tooguess atakami siłowymi toorelentless hasła.</span><span class="sxs-lookup"><span data-stu-id="d4206-106">Passwords can be guessed, and open your VMs up toorelentless brute force attempts tooguess your password.</span></span> <span data-ttu-id="d4206-107">Maszyny wirtualne utworzone z szablonami platformy Azure lub hello `azure-cli` może zawierać klucz publiczny SSH jako część wdrożenia hello, usuwanie krok konfiguracji wdrożenia post wyłączenia hasło logowania SSH.</span><span class="sxs-lookup"><span data-stu-id="d4206-107">VMs created with Azure Templates or hello `azure-cli` can include your SSH public key as part of hello deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="d4206-108">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="d4206-108">Quick Commands</span></span>

<span data-ttu-id="d4206-109">Uruchom hello poniższych poleceń z powłoki Bash, zastępując przykłady hello własne wyborów.</span><span class="sxs-lookup"><span data-stu-id="d4206-109">Run hello following commands from a Bash shell, replacing hello examples with your own choices.</span></span>

<span data-ttu-id="d4206-110">Domyślnie plik klucza publicznego SSH jest tworzony w folderze `~/.ssh/id_rsa.pub`.</span><span class="sxs-lookup"><span data-stu-id="d4206-110">Your SSH public key file is by default created at `~/.ssh/id_rsa.pub`.</span></span> <span data-ttu-id="d4206-111">Po wyświetleniu monitu, za pomocą następującego polecenia hello, należy utworzyć toosecure "hasło" klucz prywatny.</span><span class="sxs-lookup"><span data-stu-id="d4206-111">When prompted using hello following command, you should create a "passphrase" toosecure your private key.</span></span> <span data-ttu-id="d4206-112">(hello hasło jest używane hasło tooencrypt klucz prywatny.)</span><span class="sxs-lookup"><span data-stu-id="d4206-112">(hello passphrase is a password used tooencrypt your private key.)</span></span>

```bash
ssh-keygen -t rsa -b 2048 
```

<span data-ttu-id="d4206-113">Dodaj klucz hello nowo utworzone za`ssh-agent`:</span><span class="sxs-lookup"><span data-stu-id="d4206-113">Add hello newly created key too`ssh-agent`:</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> <span data-ttu-id="d4206-114">Witaj powyżej pracy poleceń w systemach operacyjnych Linux prawie wszystkie dystrybucji, ale nie działać w kontenerach, jak hello środowiska może znacząco ograniczone.</span><span class="sxs-lookup"><span data-stu-id="d4206-114">hello above commands work on Linux operating systems of almost all distributions, but do not necessarily work in containers, as hello environment can be radically constrained.</span></span> 

## <a name="detailed-walkthrough"></a><span data-ttu-id="d4206-115">Szczegółowy przewodnik</span><span class="sxs-lookup"><span data-stu-id="d4206-115">Detailed Walkthrough</span></span>

<span data-ttu-id="d4206-116">Przy użyciu kluczy publicznych i prywatnych SSH jest hello Najprostszym sposobem toolog w tooyour serwerów z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="d4206-116">Using SSH public and private keys is hello easiest way toolog in tooyour Linux servers.</span></span> <span data-ttu-id="d4206-117">[Kryptografia klucza publicznego](https://en.wikipedia.org/wiki/Public-key_cryptography) zapewnia znacznie bezpieczniejsze toolog sposób w tooyour Linux lub BSD wirtualna na platformie Azure niż hasła, które może być metodą siłową znacznie łatwiej.</span><span class="sxs-lookup"><span data-stu-id="d4206-117">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way toolog in tooyour Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4206-118">Klucz publiczny można udostępniać wszystkim, ale tylko Ty (lub lokalna infrastruktura zabezpieczeń) posiadasz klucz prywatny.</span><span class="sxs-lookup"><span data-stu-id="d4206-118">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="d4206-119">powinien mieć klucz prywatny SSH Hello [bardzo bezpieczne hasło](https://www.xkcd.com/936/) (źródło:[xkcd.com](https://xkcd.com)) toosafeguard go.</span><span class="sxs-lookup"><span data-stu-id="d4206-119">hello SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) toosafeguard it.</span></span>  <span data-ttu-id="d4206-120">To hasło jest klucz prywatny SSH hello tylko tooaccess i **nie jest** hello hasło do konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d4206-120">This password is just tooaccess hello private SSH key and **is not** hello user account password.</span></span>  <span data-ttu-id="d4206-121">Po dodaniu klucza SSH tooyour Hasło szyfruje hello klucza prywatnego za pomocą 128-bitowego szyfrowania AES, dzięki czemu hello klucz prywatny jest bezużyteczny bez toodecrypt hasło hello go.</span><span class="sxs-lookup"><span data-stu-id="d4206-121">When you add a password tooyour SSH key, it encrypts hello private key using 128-bit AES, so that hello private key is useless without hello password toodecrypt it.</span></span>  <span data-ttu-id="d4206-122">Jeśli osoba atakująca kraść klucz prywatny i że klucz nie ma hasła, będą mogli toouse to prywatnego klucza toolog w tooany serwerów, które mają hello odpowiadającym mu kluczem publicznym.</span><span class="sxs-lookup"><span data-stu-id="d4206-122">If an attacker stole your private key and that key did not have a password, they would be able toouse that private key toolog in tooany servers that have hello corresponding public key.</span></span>  <span data-ttu-id="d4206-123">Zabezpieczenie klucza prywatnego hasłem zapewnia dodatkową warstwę ochronną dla infrastruktury na platformie Azure, a osoba niepowołana nie może go użyć.</span><span class="sxs-lookup"><span data-stu-id="d4206-123">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="d4206-124">W tym artykule tworzy protokołu SSH w wersji 2 RSA publicznego i prywatnego klucza pliki, które są zalecane w przypadku wdrożeń na powitania Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="d4206-124">This article creates SSH protocol version 2 RSA public and private key files, which are recommended for deployments on hello Resource Manager.</span></span>  <span data-ttu-id="d4206-125">*SSH-rsa* klucze są wymagane na powitania [portal](https://portal.azure.com) dla wdrożenia usługi Resource Manager i klasycznym.</span><span class="sxs-lookup"><span data-stu-id="d4206-125">*ssh-rsa* keys are required on hello [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a><span data-ttu-id="d4206-126">Wyłączanie haseł SSH przy użyciu kluczy SSH</span><span class="sxs-lookup"><span data-stu-id="d4206-126">Disable SSH passwords by using SSH keys</span></span>

<span data-ttu-id="d4206-127">Platforma Azure wymaga, aby klucz publiczny i prywatny miały długość co najmniej 2048 bitów oraz format ssh-rsa.</span><span class="sxs-lookup"><span data-stu-id="d4206-127">Azure requires at least 2048-bit, ssh-rsa format public and private keys.</span></span> <span data-ttu-id="d4206-128">użycie kluczy toocreate hello `ssh-keygen`, która najpierw zadaje szereg pytań, a następnie zapisuje klucz prywatny i dopasowany klucz publiczny.</span><span class="sxs-lookup"><span data-stu-id="d4206-128">toocreate hello keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="d4206-129">Po utworzeniu maszyny Wirtualnej platformy Azure klucza publicznego hello jest kopiowana za`~/.ssh/authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="d4206-129">When an Azure VM is created, hello public key is copied too`~/.ssh/authorized_keys`.</span></span>  <span data-ttu-id="d4206-130">Kluczy SSH w `~/.ssh/authorized_keys` są używane toochallenge powitania klienta toomatch hello odpowiedni klucz prywatny na połączenia logowania SSH.</span><span class="sxs-lookup"><span data-stu-id="d4206-130">SSH keys in `~/.ssh/authorized_keys` are used toochallenge hello client toomatch hello corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="d4206-131">Po utworzeniu maszyny Wirtualnej systemu Linux na platformie Azure przy użyciu kluczy SSH do uwierzytelniania Azure konfiguruje hello SSHD toonot serwera Zezwalaj na hasło logowania, tylko kluczy SSH.</span><span class="sxs-lookup"><span data-stu-id="d4206-131">When an Azure Linux VM is created using SSH keys for authentication, Azure configures hello SSHD server toonot allow password logins, only SSH keys.</span></span>  <span data-ttu-id="d4206-132">W związku z tym tworząc maszyn wirtualnych systemu Linux platformy Azure z kluczy SSH, można ułatwić hello bezpiecznego wdrażania maszyny Wirtualnej i zapisać samodzielnie hello typowej konfiguracji po wdrożeniu kroku wyłączenie hasła w pliku konfiguracyjnym sshd_config hello.</span><span class="sxs-lookup"><span data-stu-id="d4206-132">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure hello VM deployment and save yourself hello typical post-deployment configuration step of disabling passwords in hello sshd_config config file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="d4206-133">Korzystanie z programu ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="d4206-133">Using ssh-keygen</span></span>

<span data-ttu-id="d4206-134">To polecenie umożliwia utworzenie zabezpieczonej (zaszyfrowanej) pary kluczy SSH przy użyciu RSA 2048-bitowego i jest oznaczone jako tooeasily go zidentyfikować.</span><span class="sxs-lookup"><span data-stu-id="d4206-134">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented tooeasily identify it.</span></span>  

<span data-ttu-id="d4206-135">SSH klucze są domyślnie przechowywane w hello `~/.ssh` katalogu.</span><span class="sxs-lookup"><span data-stu-id="d4206-135">SSH keys are by default kept in hello `~/.ssh` directory.</span></span>  <span data-ttu-id="d4206-136">Jeśli nie masz `~/.ssh` katalogu, hello `ssh-keygen` polecenie tworzy go dla Ciebie hello odpowiednie uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="d4206-136">If you do not have a `~/.ssh` directory, hello `ssh-keygen` command creates it for you with hello correct permissions.</span></span>

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

<span data-ttu-id="d4206-137">*Opis polecenia*</span><span class="sxs-lookup"><span data-stu-id="d4206-137">*Command explained*</span></span>

<span data-ttu-id="d4206-138">`ssh-keygen`= hello program używany toocreate hello kluczy</span><span class="sxs-lookup"><span data-stu-id="d4206-138">`ssh-keygen` = hello program used toocreate hello keys</span></span>

<span data-ttu-id="d4206-139">`-t rsa`= Typ klucza toocreate, czyli formacie RSA hello [](https://en.wikipedia.org/Wiki/RSA_(cryptosystem) wikipedia</span><span class="sxs-lookup"><span data-stu-id="d4206-139">`-t rsa` = type of key toocreate which is hello RSA format [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span></span>

<span data-ttu-id="d4206-140">`-b 2048`= Liczba bitów klucza hello</span><span class="sxs-lookup"><span data-stu-id="d4206-140">`-b 2048` = bits of hello key</span></span>


## <a name="classic-portal-and-x509-certs"></a><span data-ttu-id="d4206-141">Portal klasyczny i certyfikaty X.509</span><span class="sxs-lookup"><span data-stu-id="d4206-141">Classic portal and X.509 certs</span></span>

<span data-ttu-id="d4206-142">Jeśli używasz hello Azure [klasyczny portal](https://manage.windowsazure.com/), wymaga certyfikatów X.509 hello kluczy SSH.</span><span class="sxs-lookup"><span data-stu-id="d4206-142">If you are using hello Azure [classic portal](https://manage.windowsazure.com/), it requires X.509 certs for hello SSH keys.</span></span>  <span data-ttu-id="d4206-143">Nie są dozwolone żadne inne typy publicznych kluczy SSH — *muszą* to być certyfikaty X.509.</span><span class="sxs-lookup"><span data-stu-id="d4206-143">No other types of SSH public keys are allowed, they *must* be X.509 certs.</span></span>

<span data-ttu-id="d4206-144">toocreate certyfikatu X.509 z istniejącego klucza prywatnego SSH-RSA:</span><span class="sxs-lookup"><span data-stu-id="d4206-144">toocreate an X.509 cert from your existing SSH-RSA private key:</span></span>

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="d4206-145">Wdrażanie klasyczne przy użyciu programu `asm`</span><span class="sxs-lookup"><span data-stu-id="d4206-145">Classic deploy using `asm`</span></span>

<span data-ttu-id="d4206-146">Jeśli używasz klasycznego hello wdrożyć model (Zarządzanie usługą Azure CLI `asm`), można użyć klucza publicznego SSH-RSA lub sformatowany RFC4716 klucza w **PEM** kontenera.</span><span class="sxs-lookup"><span data-stu-id="d4206-146">If you are using hello classic deploy model (Azure service management CLI `asm`), you can use an SSH-RSA public key or an RFC4716 formatted key in a **.pem** container.</span></span>  <span data-ttu-id="d4206-147">klucz publiczny SSH-RSA Hello jest co został utworzony we wcześniejszej części tego artykułu przy użyciu `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="d4206-147">hello SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="d4206-148">toocreate RFC4716 sformatowany klucza z istniejącego klucza publicznego SSH:</span><span class="sxs-lookup"><span data-stu-id="d4206-148">toocreate a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="d4206-149">Przykład polecenia ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="d4206-149">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "ahmet@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ahmet/.ssh/id_rsa.
Your public key has been saved in /home/ahmet/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 ahmet@myserver
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

<span data-ttu-id="d4206-150">Zapisane pliki klucza:</span><span class="sxs-lookup"><span data-stu-id="d4206-150">Saved key files:</span></span>

`Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="d4206-151">Nazwa pary kluczy Hello tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="d4206-151">hello key pair name for this article.</span></span>  <span data-ttu-id="d4206-152">Para kluczy o nazwie **id_rsa** jest domyślnym hello i niektóre narzędzia mogą wymagać hello **id_rsa** nazwę pliku klucza prywatnego, dobrym pomysłem jest o jeden.</span><span class="sxs-lookup"><span data-stu-id="d4206-152">Having a key pair named **id_rsa** is hello default and some tools might expect hello **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="d4206-153">katalog Hello `~/.ssh/` jest hello domyślna lokalizacja dla par kluczy SSH i pliku konfiguracyjnego SSH hello.</span><span class="sxs-lookup"><span data-stu-id="d4206-153">hello directory `~/.ssh/` is hello default location for SSH key pairs and hello SSH config file.</span></span>  <span data-ttu-id="d4206-154">Jeśli nie zostanie określony z pełną ścieżką `ssh-keygen` będzie utworzyć klucze hello w hello bieżący katalog roboczy, nie hello domyślne `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="d4206-154">If not specified with a full path, `ssh-keygen` will create hello keys in hello current working directory, not hello default `~/.ssh`.</span></span>

<span data-ttu-id="d4206-155">Lista hello `~/.ssh` katalogu.</span><span class="sxs-lookup"><span data-stu-id="d4206-155">A listing of hello `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

<span data-ttu-id="d4206-156">Hasło klucza:</span><span class="sxs-lookup"><span data-stu-id="d4206-156">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="d4206-157">`ssh-keygen`odwołuje się klucz prywatny tooencrypt hello tooa hasło używane jako "hasło".</span><span class="sxs-lookup"><span data-stu-id="d4206-157">`ssh-keygen` refers tooa password used tooencrypt hello private key as "a passphrase."</span></span>  <span data-ttu-id="d4206-158">Jest *silnie* zalecane tooadd pary kluczy tooyour hasło.</span><span class="sxs-lookup"><span data-stu-id="d4206-158">It is *strongly* recommended tooadd a passphrase tooyour key pairs.</span></span> <span data-ttu-id="d4206-159">Bez hasła ochrona powitalnych klucz prywatny każda osoba mająca hello plik klucza może być używany toolog w tooany serwera, który ma hello odpowiadającym mu kluczem publicznym.</span><span class="sxs-lookup"><span data-stu-id="d4206-159">Without a passphrase protecting hello private key, anyone with hello key file can use it toolog in tooany server that has hello corresponding public key.</span></span> <span data-ttu-id="d4206-160">Dodawanie hasło oferuje lepszą ochronę w przypadku, gdy osoba niepowołana jest w stanie toogain dostępu tooyour pliku klucza prywatnego, umożliwiając czasu toochange hello klucze tooauthenticate użytkownik.</span><span class="sxs-lookup"><span data-stu-id="d4206-160">Adding a passphrase offers more protection in case someone is able toogain access tooyour private key file, giving you time toochange hello keys used tooauthenticate you.</span></span>

## <a name="using-ssh-agent-toostore-your-private-key-password"></a><span data-ttu-id="d4206-161">Przy użyciu hasła klucza prywatnego ssh-agent toostore</span><span class="sxs-lookup"><span data-stu-id="d4206-161">Using ssh-agent toostore your private key password</span></span>

<span data-ttu-id="d4206-162">hasło pliku tooavoid wpisanie klucza prywatnego przy każdym logowaniu przez protokół SSH, można użyć `ssh-agent` toocache hasło pliku klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="d4206-162">tooavoid typing your private key file passphrase with every SSH login, you can use `ssh-agent` toocache your private key file password.</span></span> <span data-ttu-id="d4206-163">Jeśli używasz Mac hello łańcucha kluczy systemu OS x przechowuje bezpiecznego hasła do klucza prywatnego powitania po wywołaniu `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="d4206-163">If you are using a Mac, hello OSX Keychain securely stores hello private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="d4206-164">Sprawdź i użyj `ssh-agent` i `ssh-add` tooinform hello systemu SSH o hello pliki klucza, aby hasło hello nie będzie używane w trybie interakcyjnym toobe.</span><span class="sxs-lookup"><span data-stu-id="d4206-164">Verify and use `ssh-agent` and `ssh-add` tooinform hello SSH system about hello key files so that hello passphrase will not need toobe used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="d4206-165">Teraz Dodaj klucz prywatny hello zbyt`ssh-agent` za pomocą polecenia hello `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="d4206-165">Now add hello private key too`ssh-agent` using hello command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="d4206-166">hasło klucza prywatnego Hello są obecnie przechowywane w `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="d4206-166">hello private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-tooinstall-hello-new-key"></a><span data-ttu-id="d4206-167">Przy użyciu `ssh-copy-id` tooinstall hello nowego klucza</span><span class="sxs-lookup"><span data-stu-id="d4206-167">Using `ssh-copy-id` tooinstall hello new key</span></span>
<span data-ttu-id="d4206-168">Jeśli utworzono już Maszynę wirtualną można zainstalować z hello następujące polecenie, zastępując hello maszyny Wirtualnej użytkownika i adres serwera hello własne wartości hello nowe SSH publicznego klucza tooyour maszyny Wirtualnej systemu Linux:</span><span class="sxs-lookup"><span data-stu-id="d4206-168">If you have already created a VM you can install hello new SSH public key tooyour Linux VM with hello following command, replacing hello VM username and hello server address with your own values:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="d4206-169">Tworzenie i konfigurowanie pliku konfiguracyjnego SSH</span><span class="sxs-lookup"><span data-stu-id="d4206-169">Create and configure an SSH config file</span></span>

<span data-ttu-id="d4206-170">Jest najlepszym toocreate praktyki i skonfigurować `~/.ssh/config` toospeed pliku na górę logowania i optymalizacji Twoje zachowanie klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="d4206-170">It is a best practice toocreate and configure an `~/.ssh/config` file toospeed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="d4206-171">Poniższy przykład Hello pokazano standardową konfigurację.</span><span class="sxs-lookup"><span data-stu-id="d4206-171">hello following example shows a standard configuration.</span></span>

### <a name="create-hello-file"></a><span data-ttu-id="d4206-172">Utwórz plik hello</span><span class="sxs-lookup"><span data-stu-id="d4206-172">Create hello file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a><span data-ttu-id="d4206-173">Edytuj hello pliku tooadd hello nową konfigurację SSH:</span><span class="sxs-lookup"><span data-stu-id="d4206-173">Edit hello file tooadd hello new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="d4206-174">Przykład pliku `~/.ssh/config`:</span><span class="sxs-lookup"><span data-stu-id="d4206-174">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="d4206-175">To konfiguracji SSH umożliwia możesz sekcje dla każdego serwera tooenable każdego toohave własnej pary kluczy.</span><span class="sxs-lookup"><span data-stu-id="d4206-175">This SSH config gives you sections for each server tooenable each toohave its own dedicated key pair.</span></span> <span data-ttu-id="d4206-176">Witaj ustawienia domyślne (`Host *`) są przeznaczone dla wszystkich hostach, które nie należy do żadnej hello określonych hostach w górę w pliku konfiguracyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="d4206-176">hello default settings (`Host *`) are for any hosts that do not match any of hello specific hosts higher up in hello config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="d4206-177">Opis pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="d4206-177">Config file explained</span></span>

<span data-ttu-id="d4206-178">`Host`= Nazwa hello hello hosta wywołanego na powitania w terminalu.</span><span class="sxs-lookup"><span data-stu-id="d4206-178">`Host` = hello name of hello host being called on hello terminal.</span></span>  <span data-ttu-id="d4206-179">`ssh fedora22`Określa, że `SSH` toouse hello wartości w bloku ustawienia hello etykietą `Host fedora22` Uwaga: Host może być jakakolwiek etykieta jest dla Ciebie, który nie reprezentuje hello rzeczywiste nazwą hosta żadnego serwera.</span><span class="sxs-lookup"><span data-stu-id="d4206-179">`ssh fedora22` tells `SSH` toouse hello values in hello settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent hello actual hostname of any server.</span></span>

<span data-ttu-id="d4206-180">`Hostname 102.160.203.241`= hello adres IP lub nazwa DNS serwera hello.</span><span class="sxs-lookup"><span data-stu-id="d4206-180">`Hostname 102.160.203.241` = hello IP address or DNS name for hello server being accessed.</span></span>

<span data-ttu-id="d4206-181">`User ahmet`= toouse konta użytkownika zdalnego hello podczas logowania się na serwerze toohello.</span><span class="sxs-lookup"><span data-stu-id="d4206-181">`User ahmet` = hello remote user account toouse when logging in toohello server.</span></span>

<span data-ttu-id="d4206-182">`PubKeyAuthentication yes`= informuje protokół SSH, mają toouse toolog klucza SSH.</span><span class="sxs-lookup"><span data-stu-id="d4206-182">`PubKeyAuthentication yes` = tells SSH you want toouse an SSH key toolog in.</span></span>

<span data-ttu-id="d4206-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa`= klucza prywatnego SSH hello i odpowiednie toouse klucza publicznego dla uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="d4206-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = hello SSH private key and corresponding public key toouse for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="d4206-184">Korzystanie z protokołu SSH w systemie Linux bez użycia hasła</span><span class="sxs-lookup"><span data-stu-id="d4206-184">SSH into Linux without a password</span></span>

<span data-ttu-id="d4206-185">Teraz, gdy masz parę kluczy SSH i skonfigurowany plik konfiguracji SSH są możliwe toolog w tooyour maszyny Wirtualnej systemu Linux szybkie i bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="d4206-185">Now that you have an SSH key pair and a configured SSH config file, you are able toolog in tooyour Linux VM quickly and securely.</span></span> <span data-ttu-id="d4206-186">powitania po raz pierwszy logujesz się tooa serwera przy użyciu hello klucza SSH polecenie monituje możesz dla hello hasło dla tego pliku klucza.</span><span class="sxs-lookup"><span data-stu-id="d4206-186">hello first time you log in tooa server using an SSH key hello command prompts you for hello passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="d4206-187">Opis polecenia</span><span class="sxs-lookup"><span data-stu-id="d4206-187">Command explained</span></span>

<span data-ttu-id="d4206-188">Gdy `ssh fedora22` jest wykonywany SSH najpierw lokalizuje i ładuje wszystkie ustawienia z hello `Host fedora22` bloku, a następnie obciążeń hello wszystkie pozostałe ustawienia z ostatniego bloku hello `Host *`.</span><span class="sxs-lookup"><span data-stu-id="d4206-188">When `ssh fedora22` is executed SSH first locates and loads any settings from hello `Host fedora22` block, and then loads all hello remaining settings from hello last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4206-189">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d4206-189">Next Steps</span></span>

<span data-ttu-id="d4206-190">Następnie się jest toocreate maszyn wirtualnych systemu Linux platformy Azure przy użyciu nowego klucza publicznego hello SSH.</span><span class="sxs-lookup"><span data-stu-id="d4206-190">Next up is toocreate Azure Linux VMs using hello new SSH public key.</span></span>  <span data-ttu-id="d4206-191">Maszyny wirtualne platformy Azure utworzonych za pomocą klucza publicznego SSH jako hello logowania są lepiej zabezpieczone niż maszyny wirtualne utworzone przy użyciu metody logowania hello domyślne hasła.</span><span class="sxs-lookup"><span data-stu-id="d4206-191">Azure VMs that are created with an SSH public key as hello login are better secured than VMs created with hello default login method, passwords.</span></span>  <span data-ttu-id="d4206-192">W domyślnej konfiguracji maszyn wirtualnych platformy Azure utworzonych przy użyciu kluczy SSH hasła są wyłączone, aby uniknąć prób odgadnięcia hasła za pomocą ataków siłowych.</span><span class="sxs-lookup"><span data-stu-id="d4206-192">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span> <span data-ttu-id="d4206-193">Jeśli potrzebujesz więcej pomocy podczas tworzenia Twojej pary kluczy SSH, lub wymagać dodatkowych certyfikatów, takie jak w przypadku użycia z klasycznego portalu hello, zobacz [szczegółowe kroki par kluczy SSH toocreate i certyfikaty](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="d4206-193">If you need more assistance in creating your SSH key pair or require additional certificates, such as for use with hello classic portal, see [Detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

* [<span data-ttu-id="d4206-194">Tworzenie bezpiecznej maszyny wirtualnej systemu Linux przy użyciu szablonu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d4206-194">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="d4206-195">Tworzenie bezpiecznej maszyny Wirtualnej systemu Linux przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d4206-195">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="d4206-196">Tworzenie bezpiecznej maszyny Wirtualnej systemu Linux przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d4206-196">Create a secure Linux VM using hello Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
