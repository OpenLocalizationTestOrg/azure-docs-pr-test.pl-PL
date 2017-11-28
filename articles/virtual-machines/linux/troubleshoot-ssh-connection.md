---
title: "połączenie SSH aaaTroubleshoot wystawia tooan maszyny Wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Jak tootroubleshoot problemy takie jak \"Połączenia SSH nie powiodło się\" lub \"Odmowa połączenia SSH\" dla maszyny Wirtualnej platformy Azure systemem Linux."
keywords: "SSH połączenia zostało odrzucone, ssh błędu, platforma azure ssh, połączenia SSH nie powiodło się"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: dcb82e19-29b2-47bb-99f2-900d4cfb5bbb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: iainfou
ms.openlocfilehash: dfb4e75e571c8306edf5f300c4e0f07a5fe7750a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-ssh-connections-tooan-azure-linux-vm-that-fails-errors-out-or-is-refused"></a><span data-ttu-id="380a2-104">Rozwiązywanie problemów z tooan połączenia SSH maszyny Wirtualnej systemu Linux platformy Azure, który zakończy się niepowodzeniem, błędy, lub odmówiono</span><span class="sxs-lookup"><span data-stu-id="380a2-104">Troubleshoot SSH connections tooan Azure Linux VM that fails, errors out, or is refused</span></span>
<span data-ttu-id="380a2-105">Istnieją różne przyczyny, czy występują błędy protokołu Secure Shell (SSH), błędów połączenia SSH, lub SSH zostało odrzucone podczas próby tooconnect tooa maszyny wirtualnej systemu Linux (VM).</span><span class="sxs-lookup"><span data-stu-id="380a2-105">There are various reasons that you encounter Secure Shell (SSH) errors, SSH connection failures, or SSH is refused when you try tooconnect tooa Linux virtual machine (VM).</span></span> <span data-ttu-id="380a2-106">W tym artykule opisano, Znajdź i poprawne hello problemów.</span><span class="sxs-lookup"><span data-stu-id="380a2-106">This article helps you find and correct hello problems.</span></span> <span data-ttu-id="380a2-107">Można użyć hello portalu Azure, Azure CLI lub rozszerzenia dostępu do maszyny Wirtualnej dla systemu Linux tootroubleshoot i rozwiązać problemy z połączeniem.</span><span class="sxs-lookup"><span data-stu-id="380a2-107">You can use hello Azure portal, Azure CLI, or VM Access Extension for Linux tootroubleshoot and resolve connection problems.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="380a2-108">Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello ekspertów platformy Azure na [hello fora MSDN Azure i przepełnienie stosu](http://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="380a2-108">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](http://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="380a2-109">Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="380a2-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="380a2-110">Przejdź toohello [witrynę pomocy technicznej platformy Azure](http://azure.microsoft.com/support/options/) i wybierz **uzyskać pomoc techniczną**.</span><span class="sxs-lookup"><span data-stu-id="380a2-110">Go toohello [Azure support site](http://azure.microsoft.com/support/options/) and select **Get support**.</span></span> <span data-ttu-id="380a2-111">Informacje o korzystaniu z platformy Azure obsługuje, przeczytaj hello [pomocy technicznej Microsoft Azure — często zadawane pytania](http://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="380a2-111">For information about using Azure Support, read hello [Microsoft Azure support FAQ](http://azure.microsoft.com/support/faq/).</span></span>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="380a2-112">Szybkie kroki rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="380a2-112">Quick troubleshooting steps</span></span>
<span data-ttu-id="380a2-113">Po wykonaniu każdego kroku rozwiązywania problemów spróbuj połączyć się ponownie toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="380a2-113">After each troubleshooting step, try reconnecting toohello VM.</span></span>

1. <span data-ttu-id="380a2-114">Zresetuj konfigurację protokołu SSH hello.</span><span class="sxs-lookup"><span data-stu-id="380a2-114">Reset hello SSH configuration.</span></span>
2. <span data-ttu-id="380a2-115">Resetowanie poświadczeń hello hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="380a2-115">Reset hello credentials for hello user.</span></span>
3. <span data-ttu-id="380a2-116">Sprawdź hello [sieciowej grupy zabezpieczeń](../../virtual-network/virtual-networks-nsg.md) reguły zezwala na ruch protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="380a2-116">Verify hello [Network Security Group](../../virtual-network/virtual-networks-nsg.md) rules permit SSH traffic.</span></span>
   * <span data-ttu-id="380a2-117">Upewnij się, że zasady grupy zabezpieczeń sieci istnieje toopermit ruchu SSH (domyślnie TCP port 22).</span><span class="sxs-lookup"><span data-stu-id="380a2-117">Ensure that a Network Security Group rule exists toopermit SSH traffic (by default, TCP port 22).</span></span>
   * <span data-ttu-id="380a2-118">Nie można użyć przekierowania portu / mapowania bez korzystania z usługi równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="380a2-118">You cannot use port redirection / mapping without using an Azure load balancer.</span></span>
4. <span data-ttu-id="380a2-119">Sprawdź hello [kondycja zasobów maszyny Wirtualnej](../../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="380a2-119">Check hello [VM resource health](../../resource-health/resource-health-overview.md).</span></span> 
   * <span data-ttu-id="380a2-120">Upewnij się, że hello maszyny Wirtualnej raporty jako będące w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="380a2-120">Ensure that hello VM reports as being healthy.</span></span>
   * <span data-ttu-id="380a2-121">Jeśli masz włączoną diagnostykę rozruchu, sprawdź, czy hello maszyny Wirtualnej nie jest raportowanie błędów rozruchu w dziennikach hello.</span><span class="sxs-lookup"><span data-stu-id="380a2-121">If you have boot diagnostics enabled, verify hello VM is not reporting boot errors in hello logs.</span></span>
5. <span data-ttu-id="380a2-122">Uruchom ponownie hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="380a2-122">Restart hello VM.</span></span>
6. <span data-ttu-id="380a2-123">Należy ponownie wdrożyć hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="380a2-123">Redeploy hello VM.</span></span>

<span data-ttu-id="380a2-124">Kontynuuj lekturę dla bardziej szczegółowe kroki rozwiązywania problemów oraz objaśnienia.</span><span class="sxs-lookup"><span data-stu-id="380a2-124">Continue reading for more detailed troubleshooting steps and explanations.</span></span>

## <a name="available-methods-tootroubleshoot-ssh-connection-issues"></a><span data-ttu-id="380a2-125">Problemy z połączeniem SSH tootroubleshoot dostępne metody</span><span class="sxs-lookup"><span data-stu-id="380a2-125">Available methods tootroubleshoot SSH connection issues</span></span>
<span data-ttu-id="380a2-126">Można zresetować konfiguracji SSH, przy użyciu jednej z następujących metod hello lub poświadczeń:</span><span class="sxs-lookup"><span data-stu-id="380a2-126">You can reset credentials or SSH configuration using one of hello following methods:</span></span>

* <span data-ttu-id="380a2-127">[Azure portal](#use-the-azure-portal) — dobrze, jeśli potrzebujesz tooquickly Resetowanie konfiguracji SSH hello lub klucza SSH, a nie hello Azure narzędzia są zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="380a2-127">[Azure portal](#use-the-azure-portal) - great if you need tooquickly reset hello SSH configuration or SSH key and you don't have hello Azure tools installed.</span></span>
* <span data-ttu-id="380a2-128">[Azure CLI 2.0](#use-the-azure-cli-20) — Jeśli jesteś już w wierszu polecenia hello, szybko konfiguracji SSH hello resetowania lub poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="380a2-128">[Azure CLI 2.0](#use-the-azure-cli-20) - if you are already on hello command line, quickly reset hello SSH configuration or credentials.</span></span> <span data-ttu-id="380a2-129">Można również użyć hello [Azure CLI w wersji 1.0](#use-the-azure-cli-10)</span><span class="sxs-lookup"><span data-stu-id="380a2-129">You can also use hello [Azure CLI 1.0](#use-the-azure-cli-10)</span></span>
* <span data-ttu-id="380a2-130">[Azure rozszerzenia VMAccessForLinux](#use-the-vmaccess-extension) — tworzenie i ponowne użycie json definicji pliki tooreset hello SSH konfiguracji lub poświadczenia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="380a2-130">[Azure VMAccessForLinux extension](#use-the-vmaccess-extension) - create and reuse json definition files tooreset hello SSH configuration or user credentials.</span></span>

<span data-ttu-id="380a2-131">Po wykonaniu każdego kroku rozwiązywania problemów spróbuj ponownie nawiązać połączenie tooyour maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="380a2-131">After each troubleshooting step, try connecting tooyour VM again.</span></span> <span data-ttu-id="380a2-132">Jeśli nadal nie można połączyć, spróbuj hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="380a2-132">If you still cannot connect, try hello next step.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="380a2-133">Użyj hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="380a2-133">Use hello Azure portal</span></span>
<span data-ttu-id="380a2-134">Hello Azure portal udostępnia hello tooreset szybko SSH konfiguracji lub poświadczenia użytkownika bez konieczności instalowania narzędzi na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="380a2-134">hello Azure portal provides a quick way tooreset hello SSH configuration or user credentials without installing any tools on your local computer.</span></span>

<span data-ttu-id="380a2-135">Wybierz maszyny Wirtualnej w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="380a2-135">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="380a2-136">Przewiń w dół toohello **pomocy technicznej i rozwiązywania problemów** a następnie wybierz opcję **resetowania hasła** jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="380a2-136">Scroll down toohello **Support + Troubleshooting** section and select **Reset password** as in hello following example:</span></span>

![Resetowanie konfiguracji SSH lub poświadczenia w hello portalu Azure](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-hello-ssh-configuration"></a><span data-ttu-id="380a2-138">Zresetuj konfigurację protokołu SSH hello</span><span class="sxs-lookup"><span data-stu-id="380a2-138">Reset hello SSH configuration</span></span>
<span data-ttu-id="380a2-139">Pierwszym krokiem, wybierz `Reset configuration only` z hello **tryb** menu rozwijane w hello poprzedzających zrzut ekranu, następnie kliknij przycisk hello **zresetować** przycisku.</span><span class="sxs-lookup"><span data-stu-id="380a2-139">As a first step, select `Reset configuration only` from hello **Mode** drop-down menu as in hello preceding screenshot, then click hello **Reset** button.</span></span> <span data-ttu-id="380a2-140">Po zakończeniu tej akcji, ponów tooaccess maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="380a2-140">Once this action has completed, try tooaccess your VM again.</span></span>

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="380a2-141">Resetowanie poświadczeń SSH dla użytkownika</span><span class="sxs-lookup"><span data-stu-id="380a2-141">Reset SSH credentials for a user</span></span>
<span data-ttu-id="380a2-142">tooreset hello poświadczeń istniejącego użytkownika, wybierz opcję `Reset SSH public key` lub `Reset password` z hello **tryb** menu rozwijanego jak hello poprzedzających zrzut ekranu.</span><span class="sxs-lookup"><span data-stu-id="380a2-142">tooreset hello credentials of an existing user, select either `Reset SSH public key` or `Reset password` from hello **Mode** drop-down menu as in hello preceding screenshot.</span></span> <span data-ttu-id="380a2-143">Określ nazwę użytkownika hello i klucz SSH lub nowe hasło, a następnie kliknij przycisk hello **zresetować** przycisku.</span><span class="sxs-lookup"><span data-stu-id="380a2-143">Specify hello username and an SSH key or new password, then click hello **Reset** button.</span></span>

<span data-ttu-id="380a2-144">Można również utworzyć użytkownika z uprawnieniami sudo na powitania maszyny Wirtualnej z tego menu.</span><span class="sxs-lookup"><span data-stu-id="380a2-144">You can also create a user with sudo privileges on hello VM from this menu.</span></span> <span data-ttu-id="380a2-145">Wprowadź nową nazwę użytkownika i skojarzone hasła lub klucza SSH, a następnie kliknij przycisk hello **zresetować** przycisku.</span><span class="sxs-lookup"><span data-stu-id="380a2-145">Enter a new username and associated password or SSH key, and then click hello **Reset** button.</span></span>

## <a name="use-hello-azure-cli-20"></a><span data-ttu-id="380a2-146">Użyj hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="380a2-146">Use hello Azure CLI 2.0</span></span>
<span data-ttu-id="380a2-147">Jeśli nie jest jeszcze zainstalować hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) i zaloguj się za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="380a2-147">If you haven't already, install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="380a2-148">Jeśli utworzony i przekazać niestandardowego obrazu dysku dla systemu Linux, upewnij się hello [agenta usługi Microsoft Azure Linux](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) wersji 2.0.5 lub nowszy jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="380a2-148">If you created and uploaded a custom Linux disk image, make sure hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="380a2-149">Dla maszyn wirtualnych utworzonych przy użyciu obrazów w galerii to rozszerzenie dostępu jest już zainstalowane i skonfigurowane dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="380a2-149">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="380a2-150">Zresetuj konfigurację protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="380a2-150">Reset SSH configuration</span></span>
<span data-ttu-id="380a2-151">Można początkowo spróbuj zresetować hello SSH toodefault wartości konfiguracji i ponowny rozruch hello SSH serwera na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="380a2-151">You can initially try resetting hello SSH configuration toodefault values and rebooting hello SSH server on hello VM.</span></span> <span data-ttu-id="380a2-152">Należy pamiętać, że nie ma to wpływu hello nazwie konta, hasło lub kluczy SSH.</span><span class="sxs-lookup"><span data-stu-id="380a2-152">Note that this does not change hello user account name, password, or SSH keys.</span></span>
<span data-ttu-id="380a2-153">Witaj poniższym przykładzie użyto [az maszyny wirtualnej użytkownika resetowania-ssh](/cli/azure/vm/user#reset-ssh) tooreset konfiguracji SSH hello na powitania maszyny Wirtualnej o nazwie `myVM` w `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="380a2-153">hello following example uses [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh) tooreset hello SSH configuration on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="380a2-154">Użyj własne wartości w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="380a2-154">Use your own values as follows:</span></span>

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="380a2-155">Resetowanie poświadczeń SSH dla użytkownika</span><span class="sxs-lookup"><span data-stu-id="380a2-155">Reset SSH credentials for a user</span></span>
<span data-ttu-id="380a2-156">Witaj poniższym przykładzie użyto [aktualizację użytkownika maszyny wirtualnej az](/cli/azure/vm/user#update) tooreset hello poświadczeń dla `myUsername` toohello wartości określonej w `myPassword`, na powitania maszyny Wirtualnej o nazwie `myVM` w `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="380a2-156">hello following example uses [az vm user update](/cli/azure/vm/user#update) tooreset hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="380a2-157">Użyj własne wartości w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="380a2-157">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

<span data-ttu-id="380a2-158">Jeśli przy użyciu uwierzytelniania klucza SSH, można zresetować hello klucza SSH dla danego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="380a2-158">If using SSH key authentication, you can reset hello SSH key for a given user.</span></span> <span data-ttu-id="380a2-159">Witaj poniższym przykładzie użyto **wirtualna az dostępu set-linux-user** tooupdate hello SSH klucza przechowywanego u `~/.ssh/id_rsa.pub` hello użytkownika o nazwie `myUsername`, na powitania maszyny Wirtualnej o nazwie `myVM` w `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="380a2-159">hello following example uses **az vm access set-linux-user** tooupdate hello SSH key stored in `~/.ssh/id_rsa.pub` for hello user named `myUsername`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="380a2-160">Użyj własne wartości w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="380a2-160">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-hello-vmaccess-extension"></a><span data-ttu-id="380a2-161">Użyj rozszerzenia VMAccess hello</span><span class="sxs-lookup"><span data-stu-id="380a2-161">Use hello VMAccess extension</span></span>
<span data-ttu-id="380a2-162">odczytuje Hello rozszerzenia dostępu do maszyny Wirtualnej dla systemu Linux w pliku json, który definiuje akcje toocarry wychodzących. Dostępne są akcje Resetowanie SSHD, resetowanie klucza SSH lub dodanie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="380a2-162">hello VM Access Extension for Linux reads in a json file that defines actions toocarry out. These actions include resetting SSHD, resetting an SSH key, or adding a user.</span></span> <span data-ttu-id="380a2-163">Można nadal używać hello Azure CLI toocall hello rozszerzenia VMAccess, ale można użyć ponownie pliki w formacie json hello między wieloma maszynami wirtualnymi w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="380a2-163">You still use hello Azure CLI toocall hello VMAccess extension, but you can reuse hello json files across multiple VMs if desired.</span></span> <span data-ttu-id="380a2-164">Takie podejście umożliwia toocreate repozytorium pliki w formacie json, które następnie można wywołać dla danego scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="380a2-164">This approach allows you toocreate a repository of json files that can then be called for given scenarios.</span></span>

### <a name="reset-sshd"></a><span data-ttu-id="380a2-165">Resetuj SSHD</span><span class="sxs-lookup"><span data-stu-id="380a2-165">Reset SSHD</span></span>
<span data-ttu-id="380a2-166">Utwórz plik o nazwie `settings.json` z hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="380a2-166">Create a file named `settings.json` with hello following content:</span></span>

```json
{  
    "reset_ssh":"True"
}
```

<span data-ttu-id="380a2-167">Przy użyciu hello wiersza polecenia platformy Azure, możesz wywoływać hello `VMAccessForLinux` tooreset rozszerzenia SSHD połączenie przez określenie pliku json.</span><span class="sxs-lookup"><span data-stu-id="380a2-167">Using hello Azure CLI, you then call hello `VMAccessForLinux` extension tooreset your SSHD connection by specifying your json file.</span></span> <span data-ttu-id="380a2-168">Witaj poniższym przykładzie użyto [zestaw rozszerzenia maszyny wirtualnej az](/cli/azure/vm/extension#set) tooreset SSHD na powitania maszyny Wirtualnej o nazwie `myVM` w `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="380a2-168">hello following example uses [az vm extension set](/cli/azure/vm/extension#set) tooreset SSHD on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="380a2-169">Użyj własne wartości w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="380a2-169">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="380a2-170">Resetowanie poświadczeń SSH dla użytkownika</span><span class="sxs-lookup"><span data-stu-id="380a2-170">Reset SSH credentials for a user</span></span>
<span data-ttu-id="380a2-171">Jeśli SSHD pojawi się toofunction poprawnie, można zresetować hello poświadczeń użytkownika giver.</span><span class="sxs-lookup"><span data-stu-id="380a2-171">If SSHD appears toofunction correctly, you can reset hello credentials for a giver user.</span></span> <span data-ttu-id="380a2-172">tooreset hello hasła dla użytkownika, Utwórz plik o nazwie `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="380a2-172">tooreset hello password for a user, create a file named `settings.json`.</span></span> <span data-ttu-id="380a2-173">Witaj poniższy przykład resetuje hello poświadczenia dla `myUsername` toohello wartości określonej w `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="380a2-173">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`.</span></span> <span data-ttu-id="380a2-174">Wprowadź hello następujące wiersze do Twojej `settings.json` plików przy użyciu własnych wartości:</span><span class="sxs-lookup"><span data-stu-id="380a2-174">Enter hello following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

<span data-ttu-id="380a2-175">Lub tooreset hello klucza SSH dla użytkownika, najpierw utwórz plik o nazwie `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="380a2-175">Or tooreset hello SSH key for a user, first create a file named `settings.json`.</span></span> <span data-ttu-id="380a2-176">Witaj poniższy przykład resetuje hello poświadczenia dla `myUsername` toohello wartości określonej w `myPassword`, na powitania maszyny Wirtualnej o nazwie `myVM` w `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="380a2-176">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="380a2-177">Wprowadź hello następujące wiersze do Twojej `settings.json` plików przy użyciu własnych wartości:</span><span class="sxs-lookup"><span data-stu-id="380a2-177">Enter hello following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

<span data-ttu-id="380a2-178">Po utworzeniu pliku json, użyj hello Azure CLI toocall hello `VMAccessForLinux` tooreset rozszerzenia poświadczenia użytkownika SSH, określając pliku json.</span><span class="sxs-lookup"><span data-stu-id="380a2-178">After creating your json file, use hello Azure CLI toocall hello `VMAccessForLinux` extension tooreset your SSH user credentials by specifying your json file.</span></span> <span data-ttu-id="380a2-179">Witaj poniższy przykład powoduje zresetowanie poświadczeń na powitania maszyny Wirtualnej o nazwie `myVM` w `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="380a2-179">hello following example resets credentials on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="380a2-180">Użyj własne wartości w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="380a2-180">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-hello-azure-cli-10"></a><span data-ttu-id="380a2-181">Użyj hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="380a2-181">Use hello Azure CLI 1.0</span></span>
<span data-ttu-id="380a2-182">Jeśli nie jest jeszcze, [zainstalować hello Azure CLI 1.0 i połączyć tooyour subskrypcji platformy Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="380a2-182">If you haven't already, [install hello Azure CLI 1.0 and connect tooyour Azure subscription](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="380a2-183">Upewnij się, że używasz tryb usługi Resource Manager w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="380a2-183">Make sure that you are using Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="380a2-184">Jeśli utworzony i przekazać niestandardowego obrazu dysku dla systemu Linux, upewnij się hello [agenta usługi Microsoft Azure Linux](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) wersji 2.0.5 lub nowszy jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="380a2-184">If you created and uploaded a custom Linux disk image, make sure hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="380a2-185">Dla maszyn wirtualnych utworzonych przy użyciu obrazów w galerii to rozszerzenie dostępu jest już zainstalowane i skonfigurowane dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="380a2-185">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="380a2-186">Zresetuj konfigurację protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="380a2-186">Reset SSH configuration</span></span>
<span data-ttu-id="380a2-187">Konfiguracja SSHD Hello, sam może być niepoprawnie skonfigurowany lub hello Usługa napotkała błąd.</span><span class="sxs-lookup"><span data-stu-id="380a2-187">hello SSHD configuration itself may be misconfigured or hello service encountered an error.</span></span> <span data-ttu-id="380a2-188">Możesz resetować toomake SSHD się, że konfiguracji SSH hello sam jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="380a2-188">You can reset SSHD toomake sure hello SSH configuration itself is valid.</span></span> <span data-ttu-id="380a2-189">Resetowanie SSHD powinna być hello rozwiązywania problemów z krokiem, który należy wykonać.</span><span class="sxs-lookup"><span data-stu-id="380a2-189">Resetting SSHD should be hello first troubleshooting step you take.</span></span>

<span data-ttu-id="380a2-190">Witaj poniższy przykład resetuje SSHD na maszynie Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="380a2-190">hello following example resets SSHD on a VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="380a2-191">Użyj nazwy grupy własną maszyny Wirtualnej i zasobów w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="380a2-191">Use your own VM and resource group names as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="380a2-192">Resetowanie poświadczeń SSH dla użytkownika</span><span class="sxs-lookup"><span data-stu-id="380a2-192">Reset SSH credentials for a user</span></span>
<span data-ttu-id="380a2-193">SSHD widoczna toofunction poprawnie, można zresetować hasła hello giver użytkownika.</span><span class="sxs-lookup"><span data-stu-id="380a2-193">If SSHD appears toofunction correctly, you can reset hello password for a giver user.</span></span> <span data-ttu-id="380a2-194">Witaj poniższy przykład resetuje hello poświadczenia dla `myUsername` toohello wartości określonej w `myPassword`, na powitania maszyny Wirtualnej o nazwie `myVM` w `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="380a2-194">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="380a2-195">Użyj własne wartości w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="380a2-195">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

<span data-ttu-id="380a2-196">Jeśli przy użyciu uwierzytelniania klucza SSH, można zresetować hello klucza SSH dla danego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="380a2-196">If using SSH key authentication, you can reset hello SSH key for a given user.</span></span> <span data-ttu-id="380a2-197">Po aktualizacji przykład Hello hello klucz SSH, przechowywane w `~/.ssh/id_rsa.pub` hello użytkownika o nazwie `myUsername`, na powitania maszyny Wirtualnej o nazwie `myVM` w `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="380a2-197">hello following example updates hello SSH key stored in `~/.ssh/id_rsa.pub` for hello user named `myUsername`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="380a2-198">Użyj własne wartości w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="380a2-198">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a><span data-ttu-id="380a2-199">Ponowne uruchamianie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="380a2-199">Restart a VM</span></span>
<span data-ttu-id="380a2-200">Jeśli masz zresetować hello SSH konfiguracji oraz poświadczenia użytkownika lub wystąpił błąd w ten sposób, można spróbować uruchomić tooaddress wirtualna hello bazowy problemów obliczeń.</span><span class="sxs-lookup"><span data-stu-id="380a2-200">If you have reset hello SSH configuration and user credentials, or encountered an error in doing so, you can try restarting hello VM tooaddress underlying compute issues.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="380a2-201">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="380a2-201">Azure portal</span></span>
<span data-ttu-id="380a2-202">toorestart maszynę Wirtualną przy użyciu hello Azure portalu, wybierz tekst hello maszyny Wirtualnej i kliknij przycisk **ponowne uruchomienie** przycisku tak jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="380a2-202">toorestart a VM using hello Azure portal, select your VM and click hello **Restart** button as in hello following example:</span></span>

![Uruchom ponownie Maszynę wirtualną w hello portalu Azure](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="380a2-204">Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="380a2-204">Azure CLI 1.0</span></span>
<span data-ttu-id="380a2-205">Po uruchomieniu przykład Hello hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="380a2-205">hello following example restarts hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="380a2-206">Użyj własne wartości w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="380a2-206">Use your own values as follows:</span></span>

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="380a2-207">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="380a2-207">Azure CLI 2.0</span></span>
<span data-ttu-id="380a2-208">Witaj poniższym przykładzie użyto [ponownego uruchomienia maszyny wirtualnej az](/cli/azure/vm#restart) toorestart hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="380a2-208">hello following example uses [az vm restart](/cli/azure/vm#restart) toorestart hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="380a2-209">Użyj własne wartości w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="380a2-209">Use your own values as follows:</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a><span data-ttu-id="380a2-210">Ponowne wdrażanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="380a2-210">Redeploy a VM</span></span>
<span data-ttu-id="380a2-211">Można ponownie wdrożyć węzła tooanother maszyny Wirtualnej w systemie Azure, która może rozwiązać problemy z siecią podstawowej.</span><span class="sxs-lookup"><span data-stu-id="380a2-211">You can redeploy a VM tooanother node within Azure, which may correct any underlying networking issues.</span></span> <span data-ttu-id="380a2-212">Informacje dotyczące ponownego wdrażania maszyny Wirtualnej, zobacz [ponownie wdrożyć toonew maszyny wirtualnej Azure węzła](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="380a2-212">For information about redeploying a VM, see [Redeploy virtual machine toonew Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="380a2-213">Po zakończeniu tej operacji, tymczasowych dane zostaną utracone i dynamicznych adresów IP, które są skojarzone z maszyną wirtualną hello zostaną zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="380a2-213">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with hello virtual machine will be updated.</span></span>
> 
> 

### <a name="azure-portal"></a><span data-ttu-id="380a2-214">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="380a2-214">Azure portal</span></span>
<span data-ttu-id="380a2-215">tooredeploy maszynę Wirtualną przy użyciu hello Azure portalu, wybierz opcję sieci maszyny Wirtualnej i przewiń w dół toohello **pomocy technicznej i rozwiązywania problemów** sekcji.</span><span class="sxs-lookup"><span data-stu-id="380a2-215">tooredeploy a VM using hello Azure portal, select your VM and scroll down toohello **Support + Troubleshooting** section.</span></span> <span data-ttu-id="380a2-216">Kliknij przycisk hello **ponownie wdrożyć** przycisku tak jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="380a2-216">Click hello **Redeploy** button as in hello following example:</span></span>

![Wdrożenie maszyny Wirtualnej w ramach hello portalu Azure](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="380a2-218">Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="380a2-218">Azure CLI 1.0</span></span>
<span data-ttu-id="380a2-219">powitania po wdraża ponownie przykład Witaj maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="380a2-219">hello following example redeploys hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="380a2-220">Użyj własne wartości w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="380a2-220">Use your own values as follows:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="380a2-221">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="380a2-221">Azure CLI 2.0</span></span>
<span data-ttu-id="380a2-222">Witaj następujące przykładowe zastosowanie [ponownego wdrażania maszyny wirtualnej az](/cli/azure/vm#redeploy) tooredeploy hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="380a2-222">hello following example use [az vm redeploy](/cli/azure/vm#redeploy) tooredeploy hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="380a2-223">Użyj własne wartości w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="380a2-223">Use your own values as follows:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-hello-classic-deployment-model"></a><span data-ttu-id="380a2-224">Maszyny wirtualne utworzone przy użyciu klasycznego modelu wdrożenia hello</span><span class="sxs-lookup"><span data-stu-id="380a2-224">VMs created by using hello Classic deployment model</span></span>
<span data-ttu-id="380a2-225">Spróbuj te kroki tooresolve hello najczęściej SSH błędów połączenia dla maszyn wirtualnych, które zostały utworzone przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="380a2-225">Try these steps tooresolve hello most common SSH connection failures for VMs that were created by using hello classic deployment model.</span></span> <span data-ttu-id="380a2-226">Po wykonaniu każdego kroku spróbuj połączyć się ponownie toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="380a2-226">After each step, try reconnecting toohello VM.</span></span>

* <span data-ttu-id="380a2-227">Zresetuj dostęp zdalny z hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="380a2-227">Reset remote access from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="380a2-228">Na hello portalu Azure, wybierz maszyny Wirtualnej i kliknij przycisk hello **zresetować zdalnego...**  przycisku.</span><span class="sxs-lookup"><span data-stu-id="380a2-228">On hello Azure portal, select your VM and click hello **Reset Remote...** button.</span></span>
* <span data-ttu-id="380a2-229">Uruchom ponownie hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="380a2-229">Restart hello VM.</span></span> <span data-ttu-id="380a2-230">Na powitania [portalu Azure](https://portal.azure.com)wybierz maszyny Wirtualnej i kliknij hello **ponowne uruchomienie** przycisku.</span><span class="sxs-lookup"><span data-stu-id="380a2-230">On hello [Azure portal](https://portal.azure.com), select your VM and click hello **Restart** button.</span></span>
    
* <span data-ttu-id="380a2-231">Należy ponownie wdrożyć nowy węzeł Azure hello wirtualna tooa.</span><span class="sxs-lookup"><span data-stu-id="380a2-231">Redeploy hello VM tooa new Azure node.</span></span> <span data-ttu-id="380a2-232">Aby uzyskać informacje na temat tooredeploy maszyny Wirtualnej, zobacz [ponownie wdrożyć toonew maszyny wirtualnej Azure węzła](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="380a2-232">For information about how tooredeploy a VM, see [Redeploy virtual machine toonew Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
    <span data-ttu-id="380a2-233">Po zakończeniu tej operacji, tymczasowych dane zostaną utracone i dynamicznych adresów IP, które są skojarzone z maszyną wirtualną hello zostaną zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="380a2-233">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with hello virtual machine will be updated.</span></span>
* <span data-ttu-id="380a2-234">Postępuj zgodnie z instrukcjami hello [jak tooreset hasła lub SSH dla maszyn wirtualnych z systemem Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) do:</span><span class="sxs-lookup"><span data-stu-id="380a2-234">Follow hello instructions in [How tooreset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) to:</span></span>
  
  * <span data-ttu-id="380a2-235">Resetowanie hello hasła lub klucza SSH.</span><span class="sxs-lookup"><span data-stu-id="380a2-235">Reset hello password or SSH key.</span></span>
  * <span data-ttu-id="380a2-236">Utwórz *sudo* konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="380a2-236">Create a *sudo* user account.</span></span>
  * <span data-ttu-id="380a2-237">Zresetuj konfigurację protokołu SSH hello.</span><span class="sxs-lookup"><span data-stu-id="380a2-237">Reset hello SSH configuration.</span></span>
* <span data-ttu-id="380a2-238">Sprawdź kondycję zasobu hello wirtualna dla problemów z platformą.</span><span class="sxs-lookup"><span data-stu-id="380a2-238">Check hello VM's resource health for any platform issues.</span></span><br>
     <span data-ttu-id="380a2-239">Wybierz maszyny Wirtualnej, a następnie przewiń w dół **ustawienia** > **kondycji Sprawdź**.</span><span class="sxs-lookup"><span data-stu-id="380a2-239">Select your VM and scroll down **Settings** > **Check Health**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="380a2-240">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="380a2-240">Additional resources</span></span>
* <span data-ttu-id="380a2-241">Jeśli nadal nie tooSSH tooyour maszyny Wirtualnej po hello następujące po wykonaniu kroków, zobacz [bardziej szczegółowe kroki rozwiązywania problemów](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview dodatkowe kroki tooresolve problemu.</span><span class="sxs-lookup"><span data-stu-id="380a2-241">If you are still unable tooSSH tooyour VM after following hello after steps, see [more detailed troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview additional steps tooresolve your issue.</span></span>
* <span data-ttu-id="380a2-242">Aby uzyskać więcej informacji dotyczących rozwiązywania problemów z dostęp do aplikacji, zobacz [Rozwiązywanie problemów dotyczących dostępu tooan aplikacja była uruchomiona na maszynie wirtualnej platformy Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="380a2-242">For more information about troubleshooting application access, see [Troubleshoot access tooan application running on an Azure virtual machine](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="380a2-243">Aby uzyskać więcej informacji dotyczących rozwiązywania problemów z maszyn wirtualnych, które zostały utworzone przy użyciu hello klasycznego modelu wdrażania, zobacz [jak tooreset hasła lub SSH dla maszyn wirtualnych z systemem Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="380a2-243">For more information about troubleshooting virtual machines that were created by using hello classic deployment model, see [How tooreset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

