---
title: Skonfiguruj SSHD na maszynach wirtualnych Azure Linux | Dokumentacja firmy Microsoft
description: "Skonfiguruj SSHD do najlepszych rozwiązań dotyczących zabezpieczeń i blokady SSH do maszyn wirtualnych systemu Linux platformy Azure."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/21/2016
ms.author: v-livech
ms.openlocfilehash: 0195c385b00ab92b2b92ce8ff00983a0d91bf3a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-sshd-on-azure-linux-vms"></a><span data-ttu-id="8ee46-103">Skonfiguruj SSHD na maszynach wirtualnych systemu Linux platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8ee46-103">Configure SSHD on Azure Linux VMs</span></span>

<span data-ttu-id="8ee46-104">W tym artykule opisano, jak do blokowania SSH serwera w systemie Linux, aby zapewnić najlepsze rozwiązania w zakresie zabezpieczeń, a także aby przyspieszyć proces logowania SSH przy użyciu protokołu SSH kluczy zamiast hasła.</span><span class="sxs-lookup"><span data-stu-id="8ee46-104">This article shows how to lockdown the SSH Server on Linux, to provide best practices security and also to speed up the SSH login process by using SSH keys instead of passwords.</span></span>  <span data-ttu-id="8ee46-105">Do kontynuowania blokady SSHD zamierzamy można wyłączyć użytkownika głównego mogli się zalogować, ograniczyć użytkowników, którzy mogą zalogować się za pomocą listy zatwierdzonych grup, wyłączenie protokołu SSH w wersji 1, minimalna bitowego klucza i Konfigurowanie automatycznego wylogowaniu bezczynnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="8ee46-105">To further lockdown SSHD we are going to disable the root user from being able to login, limit the users that are allowed to login via an approved group list, disabling SSH protocol version 1, set a minimum key bit, and configure auto-logout of idle users.</span></span>  <span data-ttu-id="8ee46-106">Wymagania dotyczące tego artykułu: konto platformy Azure ([Pobierz bezpłatną wersję próbną](https://azure.microsoft.com/pricing/free-trial/)) i [SSH publiczne i prywatne pliki klucza](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8ee46-106">The requirements for this article are: an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="8ee46-107">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="8ee46-107">Quick Commands</span></span>

<span data-ttu-id="8ee46-108">Konfigurowanie `/etc/ssh/sshd_config` z następującymi ustawieniami:</span><span class="sxs-lookup"><span data-stu-id="8ee46-108">Configure `/etc/ssh/sshd_config` with the following settings:</span></span>

### <a name="disable-password-logins"></a><span data-ttu-id="8ee46-109">Wyłącz hasło logowania</span><span class="sxs-lookup"><span data-stu-id="8ee46-109">Disable password logins</span></span>

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-the-root-user"></a><span data-ttu-id="8ee46-110">Wyłącz logowanie przez użytkownika głównego</span><span class="sxs-lookup"><span data-stu-id="8ee46-110">Disable login by the root user</span></span>

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a><span data-ttu-id="8ee46-111">Dozwolona lista grup</span><span class="sxs-lookup"><span data-stu-id="8ee46-111">Allowed groups list</span></span>

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a><span data-ttu-id="8ee46-112">Lista dozwolonych użytkowników</span><span class="sxs-lookup"><span data-stu-id="8ee46-112">Allowed users list</span></span>

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="8ee46-113">Wyłączanie protokołu SSH w wersji 1</span><span class="sxs-lookup"><span data-stu-id="8ee46-113">Disable SSH protocol version 1</span></span>

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a><span data-ttu-id="8ee46-114">Minimalna bitów klucza</span><span class="sxs-lookup"><span data-stu-id="8ee46-114">Minimum key bits</span></span>

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a><span data-ttu-id="8ee46-115">Odłącz bezczynnych użytkowników</span><span class="sxs-lookup"><span data-stu-id="8ee46-115">Disconnect idle users</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="8ee46-116">Szczegółowy przewodnik</span><span class="sxs-lookup"><span data-stu-id="8ee46-116">Detailed Walkthrough</span></span>

<span data-ttu-id="8ee46-117">SSHD to SSH serwer, który działa na Maszynie wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="8ee46-117">SSHD is the SSH Server that runs on the Linux VM.</span></span>  <span data-ttu-id="8ee46-118">SSH jest klienta z systemem Windows z powłoki na Twoje MacBook stacji roboczej systemu Linux lub Bash.</span><span class="sxs-lookup"><span data-stu-id="8ee46-118">SSH is a client that runs from a shell on your MacBook, Linux workstation, or from a Bash on Windows.</span></span>  <span data-ttu-id="8ee46-119">SSH jest również protokół używany do zabezpieczania i szyfrowania komunikacji między tą stacją roboczą a maszyny Wirtualnej systemu Linux wprowadzania SSH także sieci VPN (wirtualna sieć prywatna).</span><span class="sxs-lookup"><span data-stu-id="8ee46-119">SSH is also the protocol used to secure and encrypt the communication between your workstation and the Linux VM making SSH also a VPN (Virtual Private Network).</span></span>

<span data-ttu-id="8ee46-120">W tym artykule jest bardzo ważne jedno logowanie do maszyny Wirtualnej systemu Linux otwarte dla całego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="8ee46-120">For this article, it is very important to keep one login to your Linux VM open for the entire walk-through.</span></span>  <span data-ttu-id="8ee46-121">Po nawiązaniu połączenia SSH pozostaje jako otwartą sesję tak długo, jak okno nie jest zamknięty.</span><span class="sxs-lookup"><span data-stu-id="8ee46-121">Once an SSH connection is established, it remains as an open session as long as the window is not closed.</span></span>  <span data-ttu-id="8ee46-122">Posiadanie jednego terminala do zalogowania się zezwala na zmiany wprowadzone do usługi SSHD bez są zablokowane Jeśli podziału zostaną zmienione.</span><span class="sxs-lookup"><span data-stu-id="8ee46-122">Having one terminal logged in, allows for changes to be made to the SSHD service without being locked out if a breaking change is made.</span></span>  <span data-ttu-id="8ee46-123">Jeśli maszyny Wirtualnej systemu Linux przerwane konfiguracji SSHD pobrać zablokowane, platforma Azure oferuje możliwość resetowania przerwane konfiguracji SSHD o [rozszerzenia dostępu do maszyny Wirtualnej Azure](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8ee46-123">If you do get locked out of your Linux VM with a broken SSHD configuration, Azure offers the ability to reset a broken SSHD configuration with the [Azure VM Access Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="8ee46-124">Z tego powodu otworzyć dwóch terminale i SSH do maszyny Wirtualnej systemu Linux z obu z nich.</span><span class="sxs-lookup"><span data-stu-id="8ee46-124">For this reason we open two terminals and SSH to the Linux VM from both of them.</span></span>  <span data-ttu-id="8ee46-125">Firma Microsoft przy użyciu terminala pierwszy wprowadź zmiany w pliku konfiguracji SSHDs i ponownie uruchomić usługę SSHD.</span><span class="sxs-lookup"><span data-stu-id="8ee46-125">We use the first terminal to make the changes to SSHDs configuration file and restart the SSHD service.</span></span>  <span data-ttu-id="8ee46-126">Firma Microsoft przy użyciu terminala drugi do testowania te zmiany po ponownym uruchomieniu usługi.</span><span class="sxs-lookup"><span data-stu-id="8ee46-126">We use the second terminal to test those changes once the service is restarted.</span></span>  <span data-ttu-id="8ee46-127">Ponieważ firma Microsoft wyłączania hasła SSH i zależne ściśle kluczy SSH, jeśli klucze SSH nie są prawidłowe, a następnie zamknij połączenie z maszyną wirtualną, maszyna wirtualna zostanie trwale zablokowane i nie będzie można do niego zalogować się do niego wymaganiem go do usunięty i utworzony ponownie.</span><span class="sxs-lookup"><span data-stu-id="8ee46-127">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close the connection to the VM, the VM will be permanently locked and no one will be able to login to it requiring it to be deleted and recreated.</span></span>

## <a name="disable-password-logins"></a><span data-ttu-id="8ee46-128">Wyłącz hasło logowania</span><span class="sxs-lookup"><span data-stu-id="8ee46-128">Disable password logins</span></span>

<span data-ttu-id="8ee46-129">Jest najszybszym sposobem na zapewnienie maszyny Wirtualnej systemu Linux można wyłączyć hasło logowania.</span><span class="sxs-lookup"><span data-stu-id="8ee46-129">The quickest way to secure you Linux VM is to disable password logins.</span></span>  <span data-ttu-id="8ee46-130">Po włączeniu hasła logowania robotów przeszukiwania sieci web zostanie natychmiast start próby siłowych odgadnąć hasło dla maszyny Wirtualnej systemu Linux przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="8ee46-130">When password logins are enabled, bots crawling the web will immediately start attempting to brute force guess the password for your Linux VM using SSH.</span></span>  <span data-ttu-id="8ee46-131">Całkowite wyłączenie hasło logowania, umożliwia serwerowi SSH Ignoruj wszystkie próby logowania hasła.</span><span class="sxs-lookup"><span data-stu-id="8ee46-131">Disabling password logins completely, enables the SSH server to ignore all password login attempts.</span></span>

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-the-root-user"></a><span data-ttu-id="8ee46-132">Wyłącz logowanie przez użytkownika głównego</span><span class="sxs-lookup"><span data-stu-id="8ee46-132">Disable login by the root user</span></span>

<span data-ttu-id="8ee46-133">Następujące najlepsze rozwiązania w systemie Linux, `root` użytkownika nigdy nie powinny być rejestrowane w za pośrednictwem protokołu SSH lub przy użyciu `sudo su`.</span><span class="sxs-lookup"><span data-stu-id="8ee46-133">Following Linux best practices, the `root` user should never be logged into over SSH or using `sudo su`.</span></span>  <span data-ttu-id="8ee46-134">Wszystkie polecenia wymagające uprawnień na poziomie głównym powinna być uruchamiana zawsze za pośrednictwem `sudo` polecenia, które rejestruje wszystkie akcje dla przyszłych inspekcji.</span><span class="sxs-lookup"><span data-stu-id="8ee46-134">All commands needing root level permissions should always be run through the `sudo` command, which logs all actions for future auditing.</span></span>  <span data-ttu-id="8ee46-135">Wyłączanie `root` użytkownikom możliwość logowania za pośrednictwem SSH jest zabezpieczeń najlepsze rozwiązania w zakresie krokiem, który zapewnia tylko autoryzowani użytkownicy będą mogli SSH.</span><span class="sxs-lookup"><span data-stu-id="8ee46-135">Disabling the `root` user from logging in via SSH is a security best practices step that ensures only authorized users are allowed to SSH.</span></span>

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a><span data-ttu-id="8ee46-136">Dozwolona lista grup</span><span class="sxs-lookup"><span data-stu-id="8ee46-136">Allowed groups list</span></span>

<span data-ttu-id="8ee46-137">SSH udostępnia metody ograniczyć użytkowników i grupy, który ma być dozwolony lub niedozwolony logowanie za pomocą protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="8ee46-137">SSH offers a method of restricting users and group that are allowed or disallowed from logging in over SSH.</span></span>  <span data-ttu-id="8ee46-138">Ta funkcja używa list na zatwierdzenie lub odrzucenie logowania konkretnych użytkowników i grup.</span><span class="sxs-lookup"><span data-stu-id="8ee46-138">This feature uses lists to approve or deny specific users and groups from logging in.</span></span>  <span data-ttu-id="8ee46-139">Ustawienie grupy koło `AllowGroups` listy ogranicza zatwierdzonych logowania za pomocą protokołu SSH tylko konta użytkowników, które znajdują się w grupie kółka.</span><span class="sxs-lookup"><span data-stu-id="8ee46-139">Setting the wheel group to the `AllowGroups` list restricts approved logins over SSH to just user accounts that are in the wheel group.</span></span>

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a><span data-ttu-id="8ee46-140">Lista dozwolonych użytkowników</span><span class="sxs-lookup"><span data-stu-id="8ee46-140">Allowed users list</span></span>

<span data-ttu-id="8ee46-141">Ograniczenie logowania SSH do użytkowników po prostu jest bardziej szczegółowe sposobem wykonywać takie same zadanie, które `AllowGroups` jest.</span><span class="sxs-lookup"><span data-stu-id="8ee46-141">Restricting SSH logins to just users is a more specific way to accomplish the same task that `AllowGroups` is.</span></span>  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="8ee46-142">Wyłączanie protokołu SSH w wersji 1</span><span class="sxs-lookup"><span data-stu-id="8ee46-142">Disable SSH protocol version 1</span></span>

<span data-ttu-id="8ee46-143">Protokół SSH w wersji 1 jest niebezpieczne i powinny być wyłączone.</span><span class="sxs-lookup"><span data-stu-id="8ee46-143">SSH protocol version 1 is insecure and should be disabled.</span></span>  <span data-ttu-id="8ee46-144">Protokół SSH w wersji 2 jest bieżącej wersji, która zapewnia bezpieczny sposób SSH na serwerze.</span><span class="sxs-lookup"><span data-stu-id="8ee46-144">SSH protocol version 2 is the current version that offers a secure way to SSH to your server.</span></span>  <span data-ttu-id="8ee46-145">Wyłączanie protokołu SSH w wersji 1 nie zezwala na wszystkich klientów SSH, które próbują nawiązać połączenie z serwerem SSH, przy użyciu protokołu SSH w wersji 1.</span><span class="sxs-lookup"><span data-stu-id="8ee46-145">Disabling SSH version 1 denies any SSH clients that are attempting to establish a connection with the SSH server using SSH version 1.</span></span>  <span data-ttu-id="8ee46-146">Połączeń SSH tylko w wersji 2 są dozwolone w celu negocjowania połączenia z serwerem SSH.</span><span class="sxs-lookup"><span data-stu-id="8ee46-146">Only SSH version 2 connections are allowed to negotiate a connection with the SSH server.</span></span>

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a><span data-ttu-id="8ee46-147">Minimalna bitów klucza</span><span class="sxs-lookup"><span data-stu-id="8ee46-147">Minimum key bits</span></span>

<span data-ttu-id="8ee46-148">Następujące najlepsze rozwiązania w zakresie zabezpieczeń hasło logowania SSH są wyłączone, a tylko klucze SSH mogą służyć do uwierzytelniania z serwerem SSH.</span><span class="sxs-lookup"><span data-stu-id="8ee46-148">Following security best practices, password SSH logins are disabled and only SSH keys are allowed to be used to authenticate with the SSH server.</span></span>  <span data-ttu-id="8ee46-149">Te klucze SSH mogą być tworzone przy użyciu różne długości klucza, liczony w bitach.</span><span class="sxs-lookup"><span data-stu-id="8ee46-149">These SSH keys can be created using different length keys, measured in bits.</span></span>  <span data-ttu-id="8ee46-150">Najlepsze praktyki stanów to minimalne dopuszczalne siłę klucza klucze o długości 2048 bitów.</span><span class="sxs-lookup"><span data-stu-id="8ee46-150">Best practices states that keys of 2048 bits in length are the minimum acceptable key strength.</span></span>  <span data-ttu-id="8ee46-151">Klucze mniej niż 2048 bitów teoretycznie może być uszkodzony.</span><span class="sxs-lookup"><span data-stu-id="8ee46-151">Keys of less than 2048 bits could theoretically be broken.</span></span>  <span data-ttu-id="8ee46-152">Ustawienie `ServerKeyBits` do `2048` umożliwia połączeń przy użyciu kluczy 2048 bitów lub większej i odmowy połączeń mniej niż 2048 bitów.</span><span class="sxs-lookup"><span data-stu-id="8ee46-152">Setting the `ServerKeyBits` to `2048` allows any connections using keys of 2048 bits or greater and deny connections of less than 2048 bits.</span></span>

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a><span data-ttu-id="8ee46-153">Odłącz bezczynnych użytkowników</span><span class="sxs-lookup"><span data-stu-id="8ee46-153">Disconnect idle users</span></span>

<span data-ttu-id="8ee46-154">SSH ma możliwość odłączyć użytkowników, którzy mają otwarte połączenia, które po okresie bezczynności przez ponad Ustaw okres czasu w sekundach.</span><span class="sxs-lookup"><span data-stu-id="8ee46-154">SSH has the ability to disconnect users that have open connections that have remained idle for more than a set period of seconds.</span></span>  <span data-ttu-id="8ee46-155">Utrzymywanie otwartych sesji do tych użytkowników, którzy są aktywni ogranicza ryzyko maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="8ee46-155">Keeping open sessions to only those users who are active limits the exposure of the Linux VM.</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a><span data-ttu-id="8ee46-156">Uruchom ponownie SSHD</span><span class="sxs-lookup"><span data-stu-id="8ee46-156">Restart SSHD</span></span>

<span data-ttu-id="8ee46-157">Aby włączyć ustawienia w `/etc/ssh/sshd_config` ponownie uruchomić proces SSHD, co spowoduje ponowne uruchomienie serwera SSH.</span><span class="sxs-lookup"><span data-stu-id="8ee46-157">To enable the settings in `/etc/ssh/sshd_config` restart the SSHD process which restarts the SSH server.</span></span>  <span data-ttu-id="8ee46-158">Okno terminalu, używaną do ponownego uruchomienia serwera SSH pozostają otwarte, bez utraty otwartych sesji SSH.</span><span class="sxs-lookup"><span data-stu-id="8ee46-158">The terminal window you use to restart the SSH server remain open without losing the open SSH session.</span></span>  <span data-ttu-id="8ee46-159">Aby przetestować nowy SSH ustawienia serwera za pomocą drugiego okno terminalu lub kartę.</span><span class="sxs-lookup"><span data-stu-id="8ee46-159">To test the new SSH server settings use a second terminal window or tab.</span></span>  <span data-ttu-id="8ee46-160">Używanie osobnych terminal do testowania połączenia SSH umożliwia Przejdź wstecz i wprowadzenia dodatkowych zmian `/etc/ssh/sshd_config` w pierwszym terminalu bez jest zablokowane przez istotne zmiany SSHD.</span><span class="sxs-lookup"><span data-stu-id="8ee46-160">Using a separate terminal to test the SSH connection allows you to go back and make additional changes to the `/etc/ssh/sshd_config` in the first terminal, without being locked out by a breaking SSHD change.</span></span>  

### <a name="on-redhat-centos-and-fedora"></a><span data-ttu-id="8ee46-161">Redhat, Centos i Fedora</span><span class="sxs-lookup"><span data-stu-id="8ee46-161">On Redhat, Centos and Fedora</span></span>

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a><span data-ttu-id="8ee46-162">Na Debian i Ubuntu</span><span class="sxs-lookup"><span data-stu-id="8ee46-162">On Debian & Ubuntu</span></span>

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a><span data-ttu-id="8ee46-163">Resetuj SSHD przy użyciu resetowania Azure — dostęp</span><span class="sxs-lookup"><span data-stu-id="8ee46-163">Reset SSHD using Azure reset-access</span></span>

<span data-ttu-id="8ee46-164">Jeśli użytkownik jest zablokowany z istotne zmiany w konfiguracji SSHD służy rozszerzenia dostępu do maszyny Wirtualnej platformy Azure do zresetowania konfiguracji SSHD do oryginalnej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="8ee46-164">If you are locked out from a breaking change to the SSHD configuration you can use the Azure VM access-extension to reset the SSHD configuration back to the original configuration.</span></span>

<span data-ttu-id="8ee46-165">Wszystkie nazwy przykład zastąpić własnymi.</span><span class="sxs-lookup"><span data-stu-id="8ee46-165">Replace any example names with your own.</span></span>

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a><span data-ttu-id="8ee46-166">Zainstaluj Fail2ban</span><span class="sxs-lookup"><span data-stu-id="8ee46-166">Install Fail2ban</span></span>

<span data-ttu-id="8ee46-167">Zdecydowanie zaleca się zainstalować i skonfigurować aplikacji typu open source Fail2ban, która blokuje kolejnych nieudanych prób logowania do maszyny Wirtualnej systemu Linux za pomocą protokołu SSH za pomocą siłowych.</span><span class="sxs-lookup"><span data-stu-id="8ee46-167">It is strongly recommended to install and setup the open source app Fail2ban, which blocks repeated attempts to login to your Linux VM over SSH using brute force.</span></span>  <span data-ttu-id="8ee46-168">Fail2ban dzienniki powtarzane nieudane próby logowania za pomocą protokołu SSH, a następnie tworzy reguły zapory, aby zablokować adres IP, który prób pochodzą z.</span><span class="sxs-lookup"><span data-stu-id="8ee46-168">Fail2ban logs repeated failed attempts to login over SSH and then creates firewall rules to block the IP address that the attempts are originating from.</span></span>

* [<span data-ttu-id="8ee46-169">Strona główna Fail2ban</span><span class="sxs-lookup"><span data-stu-id="8ee46-169">Fail2ban homepage</span></span>](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a><span data-ttu-id="8ee46-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8ee46-170">Next Steps</span></span>

<span data-ttu-id="8ee46-171">Po skonfigurowaniu i zablokowane serwer SSH na maszynie Wirtualnej systemu Linux czy dodatkowe zabezpieczenia najlepsze rozwiązania, możesz skorzystać z.</span><span class="sxs-lookup"><span data-stu-id="8ee46-171">Now that you have configured and locked down the SSH server on your Linux VM there are additional security best practices you can follow.</span></span>  

* [<span data-ttu-id="8ee46-172">Zarządzanie użytkownikami, SSH i wyboru lub napraw dyski na maszynach wirtualnych systemu Linux platformy Azure przy użyciu rozszerzenia VMAccess</span><span class="sxs-lookup"><span data-stu-id="8ee46-172">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="8ee46-173">Szyfrowanie dysków na Maszynę wirtualną systemu Linux przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8ee46-173">Encrypt disks on a Linux VM using the Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="8ee46-174">Dostęp i większe bezpieczeństwo w szablonach usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8ee46-174">Access and security in Azure Resource Manager templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
