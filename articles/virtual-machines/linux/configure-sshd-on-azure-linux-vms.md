---
title: aaaConfigure SSHD na maszynach wirtualnych systemu Linux platformy Azure | Dokumentacja firmy Microsoft
description: "Skonfiguruj SSHD najlepszych rozwiązań dotyczących zabezpieczeń i toolockdown SSH tooAzure maszyn wirtualnych systemu Linux."
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
ms.openlocfilehash: c2361be7199a24b129c06acfc899dd32f6e1d6fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sshd-on-azure-linux-vms"></a><span data-ttu-id="c21a2-103">Skonfiguruj SSHD na maszynach wirtualnych systemu Linux platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c21a2-103">Configure SSHD on Azure Linux VMs</span></span>

<span data-ttu-id="c21a2-104">W tym artykule opisano, jak toolockdown hello serwera SSH w systemie Linux, tooprovide najlepsze rozwiązania w zakresie zabezpieczeń, a także toospeed proces logowania SSH hello przy użyciu kluczy SSH zamiast hasła.</span><span class="sxs-lookup"><span data-stu-id="c21a2-104">This article shows how toolockdown hello SSH Server on Linux, tooprovide best practices security and also toospeed up hello SSH login process by using SSH keys instead of passwords.</span></span>  <span data-ttu-id="c21a2-105">blokady toofurther SSHD zamierzamy toodisable hello głównego użytkownika przed toologin można ograniczyć hello użytkowników, którzy mogą toologin za pośrednictwem listy zatwierdzonych grupy wyłączenie protokołu SSH w wersji 1, minimalna bitowego klucza i Konfigurowanie automatycznego wylogowaniu bezczynnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c21a2-105">toofurther lockdown SSHD we are going toodisable hello root user from being able toologin, limit hello users that are allowed toologin via an approved group list, disabling SSH protocol version 1, set a minimum key bit, and configure auto-logout of idle users.</span></span>  <span data-ttu-id="c21a2-106">wymagania Hello w tym artykule są: konto platformy Azure ([Pobierz bezpłatną wersję próbną](https://azure.microsoft.com/pricing/free-trial/)) i [SSH publiczne i prywatne pliki klucza](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c21a2-106">hello requirements for this article are: an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="c21a2-107">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="c21a2-107">Quick Commands</span></span>

<span data-ttu-id="c21a2-108">Konfigurowanie `/etc/ssh/sshd_config` z hello następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="c21a2-108">Configure `/etc/ssh/sshd_config` with hello following settings:</span></span>

### <a name="disable-password-logins"></a><span data-ttu-id="c21a2-109">Wyłącz hasło logowania</span><span class="sxs-lookup"><span data-stu-id="c21a2-109">Disable password logins</span></span>

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-hello-root-user"></a><span data-ttu-id="c21a2-110">Wyłącz logowanie przez użytkownika głównego hello</span><span class="sxs-lookup"><span data-stu-id="c21a2-110">Disable login by hello root user</span></span>

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a><span data-ttu-id="c21a2-111">Dozwolona lista grup</span><span class="sxs-lookup"><span data-stu-id="c21a2-111">Allowed groups list</span></span>

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a><span data-ttu-id="c21a2-112">Lista dozwolonych użytkowników</span><span class="sxs-lookup"><span data-stu-id="c21a2-112">Allowed users list</span></span>

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="c21a2-113">Wyłączanie protokołu SSH w wersji 1</span><span class="sxs-lookup"><span data-stu-id="c21a2-113">Disable SSH protocol version 1</span></span>

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a><span data-ttu-id="c21a2-114">Minimalna bitów klucza</span><span class="sxs-lookup"><span data-stu-id="c21a2-114">Minimum key bits</span></span>

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a><span data-ttu-id="c21a2-115">Odłącz bezczynnych użytkowników</span><span class="sxs-lookup"><span data-stu-id="c21a2-115">Disconnect idle users</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="c21a2-116">Szczegółowy przewodnik</span><span class="sxs-lookup"><span data-stu-id="c21a2-116">Detailed Walkthrough</span></span>

<span data-ttu-id="c21a2-117">SSHD jest hello SSH serwera, który jest uruchamiany na powitania maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="c21a2-117">SSHD is hello SSH Server that runs on hello Linux VM.</span></span>  <span data-ttu-id="c21a2-118">SSH jest klienta z systemem Windows z powłoki na Twoje MacBook stacji roboczej systemu Linux lub Bash.</span><span class="sxs-lookup"><span data-stu-id="c21a2-118">SSH is a client that runs from a shell on your MacBook, Linux workstation, or from a Bash on Windows.</span></span>  <span data-ttu-id="c21a2-119">SSH jest również protokół hello używane toosecure i szyfrowania komunikacji hello między stacji roboczej i hello maszyny Wirtualnej systemu Linux wprowadzania SSH także sieci VPN (wirtualna sieć prywatna).</span><span class="sxs-lookup"><span data-stu-id="c21a2-119">SSH is also hello protocol used toosecure and encrypt hello communication between your workstation and hello Linux VM making SSH also a VPN (Virtual Private Network).</span></span>

<span data-ttu-id="c21a2-120">W tym artykule jest bardzo ważne tookeep jedno logowanie tooyour maszyny Wirtualnej systemu Linux Otwórz dla całego przewodnika hello.</span><span class="sxs-lookup"><span data-stu-id="c21a2-120">For this article, it is very important tookeep one login tooyour Linux VM open for hello entire walk-through.</span></span>  <span data-ttu-id="c21a2-121">Po nawiązaniu połączenia SSH pozostaje jako otwartą sesję tak długo, jak hello okno nie jest zamknięty.</span><span class="sxs-lookup"><span data-stu-id="c21a2-121">Once an SSH connection is established, it remains as an open session as long as hello window is not closed.</span></span>  <span data-ttu-id="c21a2-122">Posiadanie jednego terminala zalogowany, umożliwia toohello toobe wprowadzone zmiany SSHD service bez są zablokowane, jeśli wprowadzono zmianę podziału.</span><span class="sxs-lookup"><span data-stu-id="c21a2-122">Having one terminal logged in, allows for changes toobe made toohello SSHD service without being locked out if a breaking change is made.</span></span>  <span data-ttu-id="c21a2-123">Jeśli maszyny Wirtualnej systemu Linux przerwane konfiguracji SSHD pobrać zablokowane, platforma Azure oferuje tooreset możliwości hello przerwane konfiguracji SSHD z hello [rozszerzenia dostępu do maszyny Wirtualnej Azure](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c21a2-123">If you do get locked out of your Linux VM with a broken SSHD configuration, Azure offers hello ability tooreset a broken SSHD configuration with hello [Azure VM Access Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="c21a2-124">Z tego powodu otworzyć dwóch terminale i toohello SSH maszyny Wirtualnej systemu Linux z obu z nich.</span><span class="sxs-lookup"><span data-stu-id="c21a2-124">For this reason we open two terminals and SSH toohello Linux VM from both of them.</span></span>  <span data-ttu-id="c21a2-125">Firma Microsoft może Użyj hello pierwszy terminali toomake hello zmiany tooSSHDs pliku konfiguracji, a następnie ponownie uruchom usługę SSHD hello.</span><span class="sxs-lookup"><span data-stu-id="c21a2-125">We use hello first terminal toomake hello changes tooSSHDs configuration file and restart hello SSHD service.</span></span>  <span data-ttu-id="c21a2-126">Używamy hello drugi tootest terminali te zmiany po ponownym uruchomieniu usługi hello.</span><span class="sxs-lookup"><span data-stu-id="c21a2-126">We use hello second terminal tootest those changes once hello service is restarted.</span></span>  <span data-ttu-id="c21a2-127">Ponieważ firma Microsoft wyłączania hasła SSH i zależne ściśle kluczy SSH, jeśli klucze SSH nie są prawidłowe i zamknąć hello połączenia toohello maszyny Wirtualnej, hello maszyny Wirtualnej zostanie trwale zablokowane i nie będzie możliwe toologin tooit wymaganiem go toobe usunięty i utworzony ponownie.</span><span class="sxs-lookup"><span data-stu-id="c21a2-127">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close hello connection toohello VM, hello VM will be permanently locked and no one will be able toologin tooit requiring it toobe deleted and recreated.</span></span>

## <a name="disable-password-logins"></a><span data-ttu-id="c21a2-128">Wyłącz hasło logowania</span><span class="sxs-lookup"><span data-stu-id="c21a2-128">Disable password logins</span></span>

<span data-ttu-id="c21a2-129">Witaj najszybszy sposób toosecure maszyny Wirtualnej systemu Linux jest toodisable hasło logowania.</span><span class="sxs-lookup"><span data-stu-id="c21a2-129">hello quickest way toosecure you Linux VM is toodisable password logins.</span></span>  <span data-ttu-id="c21a2-130">Po włączeniu hasła logowania robotów przeszukiwania hello sieci web natychmiast rozpocznie się próba toobrute wymusić wynik hello hasła dla maszyny Wirtualnej systemu Linux przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="c21a2-130">When password logins are enabled, bots crawling hello web will immediately start attempting toobrute force guess hello password for your Linux VM using SSH.</span></span>  <span data-ttu-id="c21a2-131">Wyłączenie całkowicie hasło logowania, włącza hello SSH serwera tooignore wszystkich prób logowania hasła.</span><span class="sxs-lookup"><span data-stu-id="c21a2-131">Disabling password logins completely, enables hello SSH server tooignore all password login attempts.</span></span>

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-hello-root-user"></a><span data-ttu-id="c21a2-132">Wyłącz logowanie przez użytkownika głównego hello</span><span class="sxs-lookup"><span data-stu-id="c21a2-132">Disable login by hello root user</span></span>

<span data-ttu-id="c21a2-133">Następujące najlepsze rozwiązania w systemie Linux, hello `root` użytkownika nigdy nie powinny być rejestrowane w za pośrednictwem protokołu SSH lub przy użyciu `sudo su`.</span><span class="sxs-lookup"><span data-stu-id="c21a2-133">Following Linux best practices, hello `root` user should never be logged into over SSH or using `sudo su`.</span></span>  <span data-ttu-id="c21a2-134">Wszystkie polecenia wymagające uprawnień na poziomie głównym powinna być uruchamiana zawsze za pośrednictwem hello `sudo` polecenia, które rejestruje wszystkie akcje dla przyszłych inspekcji.</span><span class="sxs-lookup"><span data-stu-id="c21a2-134">All commands needing root level permissions should always be run through hello `sudo` command, which logs all actions for future auditing.</span></span>  <span data-ttu-id="c21a2-135">Wyłączanie hello `root` użytkownikom możliwość logowania za pośrednictwem SSH jest zabezpieczeń najlepsze rozwiązania w zakresie krokiem, który zapewnia tooSSH mogą tylko autoryzowani użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="c21a2-135">Disabling hello `root` user from logging in via SSH is a security best practices step that ensures only authorized users are allowed tooSSH.</span></span>

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a><span data-ttu-id="c21a2-136">Dozwolona lista grup</span><span class="sxs-lookup"><span data-stu-id="c21a2-136">Allowed groups list</span></span>

<span data-ttu-id="c21a2-137">SSH udostępnia metody ograniczyć użytkowników i grupy, który ma być dozwolony lub niedozwolony logowanie za pomocą protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="c21a2-137">SSH offers a method of restricting users and group that are allowed or disallowed from logging in over SSH.</span></span>  <span data-ttu-id="c21a2-138">Ta funkcja korzysta z list tooapprove lub uniemożliwić logowanie konkretnych użytkowników i grup.</span><span class="sxs-lookup"><span data-stu-id="c21a2-138">This feature uses lists tooapprove or deny specific users and groups from logging in.</span></span>  <span data-ttu-id="c21a2-139">Ustawienie hello kółka grupy toohello `AllowGroups` listy ogranicza zatwierdzonych logowania za pośrednictwem SSH toojust użytkownika konta, które znajdują się w grupie kółka hello.</span><span class="sxs-lookup"><span data-stu-id="c21a2-139">Setting hello wheel group toohello `AllowGroups` list restricts approved logins over SSH toojust user accounts that are in hello wheel group.</span></span>

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a><span data-ttu-id="c21a2-140">Lista dozwolonych użytkowników</span><span class="sxs-lookup"><span data-stu-id="c21a2-140">Allowed users list</span></span>

<span data-ttu-id="c21a2-141">Ograniczenie dostępu użytkowników toojust logowania SSH jest bardziej szczegółowe sposób tooaccomplish hello sam zadanie, które `AllowGroups` jest.</span><span class="sxs-lookup"><span data-stu-id="c21a2-141">Restricting SSH logins toojust users is a more specific way tooaccomplish hello same task that `AllowGroups` is.</span></span>  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="c21a2-142">Wyłączanie protokołu SSH w wersji 1</span><span class="sxs-lookup"><span data-stu-id="c21a2-142">Disable SSH protocol version 1</span></span>

<span data-ttu-id="c21a2-143">Protokół SSH w wersji 1 jest niebezpieczne i powinny być wyłączone.</span><span class="sxs-lookup"><span data-stu-id="c21a2-143">SSH protocol version 1 is insecure and should be disabled.</span></span>  <span data-ttu-id="c21a2-144">Protokołu SSH w wersji 2 jest hello bieżącej wersji, która udostępnia serwer tooyour tooSSH bezpieczny sposób.</span><span class="sxs-lookup"><span data-stu-id="c21a2-144">SSH protocol version 2 is hello current version that offers a secure way tooSSH tooyour server.</span></span>  <span data-ttu-id="c21a2-145">Wyłączanie protokołu SSH w wersji 1 nie zezwala na wszystkich klientów SSH, które próbujesz tooestablish połączenie z serwerem SSH hello przy użyciu protokołu SSH w wersji 1.</span><span class="sxs-lookup"><span data-stu-id="c21a2-145">Disabling SSH version 1 denies any SSH clients that are attempting tooestablish a connection with hello SSH server using SSH version 1.</span></span>  <span data-ttu-id="c21a2-146">Tylko połączeń SSH w wersji 2 są dozwolone toonegotiate połączenia z serwerem SSH hello.</span><span class="sxs-lookup"><span data-stu-id="c21a2-146">Only SSH version 2 connections are allowed toonegotiate a connection with hello SSH server.</span></span>

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a><span data-ttu-id="c21a2-147">Minimalna bitów klucza</span><span class="sxs-lookup"><span data-stu-id="c21a2-147">Minimum key bits</span></span>

<span data-ttu-id="c21a2-148">Następujące najlepsze rozwiązania w zakresie zabezpieczeń hasło logowania SSH są wyłączone i tylko klucze SSH mogą toobe używanych tooauthenticate z serwerem SSH hello.</span><span class="sxs-lookup"><span data-stu-id="c21a2-148">Following security best practices, password SSH logins are disabled and only SSH keys are allowed toobe used tooauthenticate with hello SSH server.</span></span>  <span data-ttu-id="c21a2-149">Te klucze SSH mogą być tworzone przy użyciu różne długości klucza, liczony w bitach.</span><span class="sxs-lookup"><span data-stu-id="c21a2-149">These SSH keys can be created using different length keys, measured in bits.</span></span>  <span data-ttu-id="c21a2-150">Najlepsze praktyki stanów czy hello minimalną siłę klucza dopuszczalne klucze o długości 2048 bitów.</span><span class="sxs-lookup"><span data-stu-id="c21a2-150">Best practices states that keys of 2048 bits in length are hello minimum acceptable key strength.</span></span>  <span data-ttu-id="c21a2-151">Klucze mniej niż 2048 bitów teoretycznie może być uszkodzony.</span><span class="sxs-lookup"><span data-stu-id="c21a2-151">Keys of less than 2048 bits could theoretically be broken.</span></span>  <span data-ttu-id="c21a2-152">Ustawienie hello `ServerKeyBits` zbyt`2048` umożliwia połączeń przy użyciu kluczy 2048 bitów lub większej i odmowy połączeń mniej niż 2048 bitów.</span><span class="sxs-lookup"><span data-stu-id="c21a2-152">Setting hello `ServerKeyBits` too`2048` allows any connections using keys of 2048 bits or greater and deny connections of less than 2048 bits.</span></span>

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a><span data-ttu-id="c21a2-153">Odłącz bezczynnych użytkowników</span><span class="sxs-lookup"><span data-stu-id="c21a2-153">Disconnect idle users</span></span>

<span data-ttu-id="c21a2-154">SSH ma hello możliwości toodisconnect użytkowników, którzy mają otwarte połączenia, które po okresie bezczynności przez ponad Ustaw okres czasu w sekundach.</span><span class="sxs-lookup"><span data-stu-id="c21a2-154">SSH has hello ability toodisconnect users that have open connections that have remained idle for more than a set period of seconds.</span></span>  <span data-ttu-id="c21a2-155">Utrzymywanie otwartych sesji tooonly tych użytkowników, którzy są limity active narażenia hello hello maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="c21a2-155">Keeping open sessions tooonly those users who are active limits hello exposure of hello Linux VM.</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a><span data-ttu-id="c21a2-156">Uruchom ponownie SSHD</span><span class="sxs-lookup"><span data-stu-id="c21a2-156">Restart SSHD</span></span>

<span data-ttu-id="c21a2-157">Ustawienia hello tooenable w `/etc/ssh/sshd_config` ponownie uruchomić proces SSHD hello, co spowoduje ponowne uruchomienie hello serwer SSH.</span><span class="sxs-lookup"><span data-stu-id="c21a2-157">tooenable hello settings in `/etc/ssh/sshd_config` restart hello SSHD process which restarts hello SSH server.</span></span>  <span data-ttu-id="c21a2-158">Okno terminalu Hello w przypadku używania serwera SSH hello toorestart pozostają otwarte, bez utraty hello otwartych sesji SSH.</span><span class="sxs-lookup"><span data-stu-id="c21a2-158">hello terminal window you use toorestart hello SSH server remain open without losing hello open SSH session.</span></span>  <span data-ttu-id="c21a2-159">tootest hello nowych ustawień serwera SSH za pomocą drugiego okno terminalu lub kartę.  Użycie hello oddzielnych tootest terminali połączenia SSH umożliwia toogo Wstecz i Utwórz dodatkowe zmiany toohello `/etc/ssh/sshd_config` w pierwszym terminal hello bez jest zablokowane przez istotne zmiany SSHD.</span><span class="sxs-lookup"><span data-stu-id="c21a2-159">tootest hello new SSH server settings use a second terminal window or tab.  Using a separate terminal tootest hello SSH connection allows you toogo back and make additional changes toohello `/etc/ssh/sshd_config` in hello first terminal, without being locked out by a breaking SSHD change.</span></span>  

### <a name="on-redhat-centos-and-fedora"></a><span data-ttu-id="c21a2-160">Redhat, Centos i Fedora</span><span class="sxs-lookup"><span data-stu-id="c21a2-160">On Redhat, Centos and Fedora</span></span>

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a><span data-ttu-id="c21a2-161">Na Debian i Ubuntu</span><span class="sxs-lookup"><span data-stu-id="c21a2-161">On Debian & Ubuntu</span></span>

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a><span data-ttu-id="c21a2-162">Resetuj SSHD przy użyciu resetowania Azure — dostęp</span><span class="sxs-lookup"><span data-stu-id="c21a2-162">Reset SSHD using Azure reset-access</span></span>

<span data-ttu-id="c21a2-163">Jeśli użytkownik jest zablokowany z najważniejszych zmian toohello SSHD konfiguracji można użyć hello rozszerzenia dostępu do maszyny Wirtualnej Azure tooreset hello SSHD konfiguracji wstecz toohello oryginalnej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c21a2-163">If you are locked out from a breaking change toohello SSHD configuration you can use hello Azure VM access-extension tooreset hello SSHD configuration back toohello original configuration.</span></span>

<span data-ttu-id="c21a2-164">Wszystkie nazwy przykład zastąpić własnymi.</span><span class="sxs-lookup"><span data-stu-id="c21a2-164">Replace any example names with your own.</span></span>

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a><span data-ttu-id="c21a2-165">Zainstaluj Fail2ban</span><span class="sxs-lookup"><span data-stu-id="c21a2-165">Install Fail2ban</span></span>

<span data-ttu-id="c21a2-166">Zalecane jest tooinstall i Instalator hello typu open source aplikacja Fail2ban, które bloki powtarzane próby toologin tooyour maszyny Wirtualnej systemu Linux za pomocą protokołu SSH za pomocą siłowych.</span><span class="sxs-lookup"><span data-stu-id="c21a2-166">It is strongly recommended tooinstall and setup hello open source app Fail2ban, which blocks repeated attempts toologin tooyour Linux VM over SSH using brute force.</span></span>  <span data-ttu-id="c21a2-167">Dzienniki Fail2ban powtarzany nie powiodło się toologin prób za pomocą protokołu SSH, a następnie tworzy reguły zapory adres IP hello tooblock prób hello pochodzą z.</span><span class="sxs-lookup"><span data-stu-id="c21a2-167">Fail2ban logs repeated failed attempts toologin over SSH and then creates firewall rules tooblock hello IP address that hello attempts are originating from.</span></span>

* [<span data-ttu-id="c21a2-168">Strona główna Fail2ban</span><span class="sxs-lookup"><span data-stu-id="c21a2-168">Fail2ban homepage</span></span>](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a><span data-ttu-id="c21a2-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c21a2-169">Next Steps</span></span>

<span data-ttu-id="c21a2-170">Po skonfigurowaniu i zablokowane hello SSH serwera na maszynie Wirtualnej systemu Linux czy dodatkowe zabezpieczenia najlepsze rozwiązania, możesz skorzystać z.</span><span class="sxs-lookup"><span data-stu-id="c21a2-170">Now that you have configured and locked down hello SSH server on your Linux VM there are additional security best practices you can follow.</span></span>  

* [<span data-ttu-id="c21a2-171">Zarządzanie użytkownikami, SSH i wyboru lub naprawy dysków na maszynach wirtualnych systemu Linux platformy Azure przy użyciu hello rozszerzenia VMAccess</span><span class="sxs-lookup"><span data-stu-id="c21a2-171">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="c21a2-172">Szyfrowanie dysków na Maszynę wirtualną systemu Linux przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c21a2-172">Encrypt disks on a Linux VM using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="c21a2-173">Dostęp i większe bezpieczeństwo w szablonach usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c21a2-173">Access and security in Azure Resource Manager templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
