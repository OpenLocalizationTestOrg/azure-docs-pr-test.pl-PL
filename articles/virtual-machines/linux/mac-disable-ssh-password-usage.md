---
title: "aaaDisable hasła SSH dla maszyny Wirtualnej systemu Linux przez skonfigurowanie SSHD | Dokumentacja firmy Microsoft"
description: "Zabezpieczenia sieci maszyny Wirtualnej systemu Linux na platformie Azure przez wyłączenie hasło logowania SSH."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 46137640-a7d2-40e5-a1e9-9effef7eb190
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/26/2016
ms.author: v-livech
ms.openlocfilehash: fb67b2f5b8b3bf2ba214858940b04f2ea9013fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a><span data-ttu-id="f77cf-103">Wyłącz konfigurując SSHD haseł SSH dla maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="f77cf-103">Disable SSH passwords on your Linux VM by configuring SSHD</span></span>
<span data-ttu-id="f77cf-104">Ten artykuł skupia się na temat toolock dół hello logowania zabezpieczeń maszyny wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="f77cf-104">This article focuses on how toolock down hello login security of your Linux VM.</span></span>  <span data-ttu-id="f77cf-105">Zaraz po otwarciu hello portu SSH 22 robotów world toohello start próby toologin przez odgadnięcie hasła.</span><span class="sxs-lookup"><span data-stu-id="f77cf-105">As soon as hello SSH port 22 is opened toohello world bots start trying toologin by guessing passwords.</span></span>  <span data-ttu-id="f77cf-106">Wykonamy w tym artykule jest, wyłącz hasło logowania za pomocą protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="f77cf-106">What we will do in this article is disable password logins over SSH.</span></span>  <span data-ttu-id="f77cf-107">Całkowicie usuwając możliwości hello hasła toouse hello maszyny Wirtualnej systemu Linux są chronione przez ten typ metodą siłową wymusić ataku.</span><span class="sxs-lookup"><span data-stu-id="f77cf-107">By completely removing hello ability toouse passwords we protect hello Linux VM from this type of brute force attack.</span></span>  <span data-ttu-id="f77cf-108">dodane Hello jest podwyższenia będzie skonfigurowanie SSHD Linux tooonly Zezwalaj logowania za pomocą kluczy publicznych i prywatnych SSH, znacznie Witaj najbezpieczniejszą tooLinux toologin sposób.</span><span class="sxs-lookup"><span data-stu-id="f77cf-108">hello added bonus is we will configure Linux SSHD tooonly allow logins via SSH public & private keys, by far hello most secure way toologin tooLinux.</span></span>  <span data-ttu-id="f77cf-109">Hello możliwych kombinacji go wymagają klucza prywatnego tooguess hello jest olbrzymie i w związku z tym odradza robotów z nawet bothering kluczy SSH w życie toobrute tootry.</span><span class="sxs-lookup"><span data-stu-id="f77cf-109">hello possible combinations of it would require tooguess hello private key is immense and therefore discourages bots from even bothering tootry toobrute force SSH keys.</span></span>

## <a name="goals"></a><span data-ttu-id="f77cf-110">Cele</span><span class="sxs-lookup"><span data-stu-id="f77cf-110">Goals</span></span>
* <span data-ttu-id="f77cf-111">Skonfiguruj SSHD toodisallow:</span><span class="sxs-lookup"><span data-stu-id="f77cf-111">Configure SSHD toodisallow:</span></span>
  * <span data-ttu-id="f77cf-112">Hasło nazwy logowania</span><span class="sxs-lookup"><span data-stu-id="f77cf-112">Password logins</span></span>
  * <span data-ttu-id="f77cf-113">Dane logowania użytkownika głównego</span><span class="sxs-lookup"><span data-stu-id="f77cf-113">Root user login</span></span>
  * <span data-ttu-id="f77cf-114">Odpowiedź na żądanie uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="f77cf-114">Challenge-response authentication</span></span>
* <span data-ttu-id="f77cf-115">Skonfiguruj SSHD tooallow:</span><span class="sxs-lookup"><span data-stu-id="f77cf-115">Configure SSHD tooallow:</span></span>
  * <span data-ttu-id="f77cf-116">tylko logowania klucza SSH</span><span class="sxs-lookup"><span data-stu-id="f77cf-116">only SSH key logins</span></span>
* <span data-ttu-id="f77cf-117">Uruchom ponownie SSHD jest nadal zalogowany</span><span class="sxs-lookup"><span data-stu-id="f77cf-117">Restart SSHD while still logged in</span></span>
* <span data-ttu-id="f77cf-118">Nowa konfiguracja SSHD hello testu</span><span class="sxs-lookup"><span data-stu-id="f77cf-118">Test hello new SSHD configuration</span></span>

## <a name="introduction"></a><span data-ttu-id="f77cf-119">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="f77cf-119">Introduction</span></span>
[<span data-ttu-id="f77cf-120">Definicja SSH</span><span class="sxs-lookup"><span data-stu-id="f77cf-120">SSH defined</span></span>](https://en.wikipedia.org/wiki/Secure_Shell)

<span data-ttu-id="f77cf-121">SSHD jest hello SSH serwera, który jest uruchamiany na powitania maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="f77cf-121">SSHD is hello SSH Server that runs on hello Linux VM.</span></span>  <span data-ttu-id="f77cf-122">SSH jest klienta, który jest uruchamiany z powłoki na stacji roboczej MacBook lub Linux.</span><span class="sxs-lookup"><span data-stu-id="f77cf-122">SSH is a client that runs from a shell on your MacBook or Linux workstation.</span></span>  <span data-ttu-id="f77cf-123">SSH jest również protokół hello używane toosecure i szyfrowania komunikacji hello między stacji roboczej i hello maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="f77cf-123">SSH is also hello protocol used toosecure and encrypt hello communication between your workstation and hello Linux VM.</span></span>

<span data-ttu-id="f77cf-124">W tym artykule jest bardzo ważne tookeep jeden tooyour logowania przeprowadzenie otwarte dla hello całej maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="f77cf-124">For this article it is very important tookeep one login tooyour Linux VM open for hello entire walk through.</span></span>  <span data-ttu-id="f77cf-125">Z tego powodu z obu z nich zostanie otwarty dwóch terminale i toohello SSH maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="f77cf-125">For this reason we will open two terminals and SSH toohello Linux VM from both of them.</span></span>  <span data-ttu-id="f77cf-126">Firma Microsoft będzie Użyj hello pierwszy terminali toomake hello zmiany tooSSHDs pliku konfiguracji i ponownie uruchom usługę SSHD hello.</span><span class="sxs-lookup"><span data-stu-id="f77cf-126">We will use hello first terminal toomake hello changes tooSSHDs configuration file and restart hello SSHD service.</span></span>  <span data-ttu-id="f77cf-127">Używamy hello drugi tootest terminali te zmiany po ponownym uruchomieniu usługi hello.</span><span class="sxs-lookup"><span data-stu-id="f77cf-127">We will use hello second terminal tootest those changes once hello service is restarted.</span></span>  <span data-ttu-id="f77cf-128">Ponieważ firma Microsoft wyłączania hasła SSH i zależne ściśle kluczy SSH, jeśli klucze SSH nie są prawidłowe i zamknąć hello połączenia toohello maszyny Wirtualnej, hello maszyny Wirtualnej zostanie trwale zablokowane i nie będzie możliwe toologin tooit wymaganiem go toobe usunięty i utworzony ponownie.</span><span class="sxs-lookup"><span data-stu-id="f77cf-128">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close hello connection toohello VM, hello VM will be permanently locked and no one will be able toologin tooit requiring it toobe deleted and recreated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f77cf-129">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f77cf-129">Prerequisites</span></span>
* [<span data-ttu-id="f77cf-130">Tworzenie kluczy SSH w systemie Linux i komputerów Mac dla maszyn wirtualnych systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f77cf-130">Create SSH keys on Linux and Mac for Linux VMs in Azure</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* <span data-ttu-id="f77cf-131">Konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f77cf-131">Azure account</span></span>
  * [<span data-ttu-id="f77cf-132">zakładania wersji próbnej</span><span class="sxs-lookup"><span data-stu-id="f77cf-132">free trial signup</span></span>](https://azure.microsoft.com/pricing/free-trial/)
  * [<span data-ttu-id="f77cf-133">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f77cf-133">Azure portal</span></span>](http://portal.azure.com)
* <span data-ttu-id="f77cf-134">Maszyny Wirtualnej systemu Linux działających na platformie azure</span><span class="sxs-lookup"><span data-stu-id="f77cf-134">Linux VM running on azure</span></span>
* <span data-ttu-id="f77cf-135">SSH publicznych i prywatnych pary kluczy w`~/.ssh/`</span><span class="sxs-lookup"><span data-stu-id="f77cf-135">SSH public & private key pair in `~/.ssh/`</span></span>
* <span data-ttu-id="f77cf-136">Klucz publiczny SSH w `~/.ssh/authorized_keys` na powitania maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="f77cf-136">SSH public key in `~/.ssh/authorized_keys` on hello Linux VM</span></span>
* <span data-ttu-id="f77cf-137">Prawa Sudo na powitania maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f77cf-137">Sudo rights on hello VM</span></span>
* <span data-ttu-id="f77cf-138">Port 22 otwarte</span><span class="sxs-lookup"><span data-stu-id="f77cf-138">Port 22 open</span></span>

## <a name="quick-commands"></a><span data-ttu-id="f77cf-139">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="f77cf-139">Quick Commands</span></span>
<span data-ttu-id="f77cf-140">*Indywidualny Administratorzy systemu Linux, po prostu chcących hello TLDR wersji zacznij tutaj.  Szczegółowy opis i krokach związanych z dla wszystkich pozostałych użytkowników, który chce hello pominąć tę sekcję.*</span><span class="sxs-lookup"><span data-stu-id="f77cf-140">*Seasoned Linux Admins who just want hello TLDR version start here.  For everyone else that wants hello detailed explanation and walk through skip this section.*</span></span>

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="f77cf-141">Edytowanie pliku konfiguracji hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f77cf-141">Edit hello config file as follows:</span></span>

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no

# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes

# Change PermitRootLogin toothis:
PermitRootLogin no

# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

<span data-ttu-id="f77cf-142">Uruchom ponownie usługę SSHD hello.</span><span class="sxs-lookup"><span data-stu-id="f77cf-142">Restart hello SSHD service.</span></span> <span data-ttu-id="f77cf-143">Na podstawie Debian dystrybucjach:</span><span class="sxs-lookup"><span data-stu-id="f77cf-143">On Debian-based distros:</span></span>

```bash
sudo service ssh restart
```

<span data-ttu-id="f77cf-144">Na podstawie Red Hat dystrybucjach:</span><span class="sxs-lookup"><span data-stu-id="f77cf-144">On Red Hat-based distros:</span></span>

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a><span data-ttu-id="f77cf-145">Szczegółowe krokach związanych z</span><span class="sxs-lookup"><span data-stu-id="f77cf-145">Detailed Walk Through</span></span>
<span data-ttu-id="f77cf-146">Logowania toohello maszyny Wirtualnej systemu Linux na terminalu 1 (T1).</span><span class="sxs-lookup"><span data-stu-id="f77cf-146">Login toohello Linux VM on terminal 1 (T1).</span></span>  <span data-ttu-id="f77cf-147">Logowania toohello maszyny Wirtualnej systemu Linux na terminalu 2 (T2).</span><span class="sxs-lookup"><span data-stu-id="f77cf-147">Login toohello Linux VM on terminal 2 (T2).</span></span>

<span data-ttu-id="f77cf-148">Na T2 zamierzamy tooedit hello SSHD konfiguracji pliku.</span><span class="sxs-lookup"><span data-stu-id="f77cf-148">On T2 we are going tooedit hello SSHD configuration file.</span></span>  

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="f77cf-149">W tym miejscu możemy edytować tylko hello ustawienia toodisable hasła i włączyć logowania do klucza SSH.</span><span class="sxs-lookup"><span data-stu-id="f77cf-149">From here we will edit just hello settings toodisable passwords and enable SSH key logins.</span></span>  <span data-ttu-id="f77cf-150">Istnieje wiele ustawień w tym pliku należy badania i zmienić toomake Linux & SSH jako bezpieczne, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="f77cf-150">There are many settings in this file that you should research and change toomake Linux & SSH as secure as you need.</span></span>

#### <a name="disable-password-logins"></a><span data-ttu-id="f77cf-151">Wyłącz hasło logowania</span><span class="sxs-lookup"><span data-stu-id="f77cf-151">Disable Password logins</span></span>

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a><span data-ttu-id="f77cf-152">Włącz uwierzytelnianie klucza publicznego</span><span class="sxs-lookup"><span data-stu-id="f77cf-152">Enable Public Key Authentication</span></span>

```sh
# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a><span data-ttu-id="f77cf-153">Wyłącz logowanie głównego</span><span class="sxs-lookup"><span data-stu-id="f77cf-153">Disable Root Login</span></span>

```sh
# Change PermitRootLogin toothis:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a><span data-ttu-id="f77cf-154">Wyłącz uwierzytelnianie odpowiedź na żądanie</span><span class="sxs-lookup"><span data-stu-id="f77cf-154">Disable Challenge-response Authentication</span></span>
```sh
# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a><span data-ttu-id="f77cf-155">Uruchom ponownie SSHD</span><span class="sxs-lookup"><span data-stu-id="f77cf-155">Restart SSHD</span></span>
<span data-ttu-id="f77cf-156">Z powłoki hello T1 upewnij się, możesz nadal są rejestrowane w.</span><span class="sxs-lookup"><span data-stu-id="f77cf-156">From hello T1 shell verify that you are still logged in.</span></span>  <span data-ttu-id="f77cf-157">Jest to krytycznych, dlatego możesz nie być blokowane z maszyny Wirtualnej Jeśli klucze SSH nie są prawidłowe, ponieważ hasła są obecnie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="f77cf-157">This is critical so you do not get locked out of your VM if your SSH keys are not correct since passwords are now disabled.</span></span>  <span data-ttu-id="f77cf-158">Jeśli wszystkie ustawienia są niepoprawne na maszynie Wirtualnej systemu Linux można użyć T1 toofix sshd_config, nadal będziesz się logować i SSH będzie podtrzymywania połączenia hello podczas hello SSHD service ponownie.</span><span class="sxs-lookup"><span data-stu-id="f77cf-158">If any setting are incorrect on your Linux VM you can use T1 toofix sshd_config as you will still be logged in and SSH will keep hello connection alive during hello SSHD service restart.</span></span>

<span data-ttu-id="f77cf-159">Z T2 Uruchom:</span><span class="sxs-lookup"><span data-stu-id="f77cf-159">From T2 run:</span></span>

##### <a name="on-hello-debian-family"></a><span data-ttu-id="f77cf-160">Na powitania Debian rodziny</span><span class="sxs-lookup"><span data-stu-id="f77cf-160">On hello Debian Family</span></span>
```bash
sudo service ssh restart
```

##### <a name="on-hello-redhat-family"></a><span data-ttu-id="f77cf-161">Na powitania rodziny RedHat</span><span class="sxs-lookup"><span data-stu-id="f77cf-161">On hello RedHat Family</span></span>
```bash
sudo service sshd restart
```

<span data-ttu-id="f77cf-162">Hasła są teraz wyłączone na chronić je przed prób logowania siłowych hasła maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f77cf-162">Passwords are now disabled on your VM protecting it from brute force password login attempts.</span></span>  <span data-ttu-id="f77cf-163">Z tylko SSH klucze dozwolone będą mogli toologin szybsze i bardziej bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="f77cf-163">With only SSH Keys allowed you will be able toologin faster and much more secure.</span></span>

