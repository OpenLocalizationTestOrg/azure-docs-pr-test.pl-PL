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
# <a name="troubleshoot-ssh-connections-tooan-azure-linux-vm-that-fails-errors-out-or-is-refused"></a>Rozwiązywanie problemów z tooan połączenia SSH maszyny Wirtualnej systemu Linux platformy Azure, który zakończy się niepowodzeniem, błędy, lub odmówiono
Istnieją różne przyczyny, czy występują błędy protokołu Secure Shell (SSH), błędów połączenia SSH, lub SSH zostało odrzucone podczas próby tooconnect tooa maszyny wirtualnej systemu Linux (VM). W tym artykule opisano, Znajdź i poprawne hello problemów. Można użyć hello portalu Azure, Azure CLI lub rozszerzenia dostępu do maszyny Wirtualnej dla systemu Linux tootroubleshoot i rozwiązać problemy z połączeniem.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello ekspertów platformy Azure na [hello fora MSDN Azure i przepełnienie stosu](http://azure.microsoft.com/support/forums/). Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure. Przejdź toohello [witrynę pomocy technicznej platformy Azure](http://azure.microsoft.com/support/options/) i wybierz **uzyskać pomoc techniczną**. Informacje o korzystaniu z platformy Azure obsługuje, przeczytaj hello [pomocy technicznej Microsoft Azure — często zadawane pytania](http://azure.microsoft.com/support/faq/).

## <a name="quick-troubleshooting-steps"></a>Szybkie kroki rozwiązywania problemów
Po wykonaniu każdego kroku rozwiązywania problemów spróbuj połączyć się ponownie toohello maszyny Wirtualnej.

1. Zresetuj konfigurację protokołu SSH hello.
2. Resetowanie poświadczeń hello hello użytkownika.
3. Sprawdź hello [sieciowej grupy zabezpieczeń](../../virtual-network/virtual-networks-nsg.md) reguły zezwala na ruch protokołu SSH.
   * Upewnij się, że zasady grupy zabezpieczeń sieci istnieje toopermit ruchu SSH (domyślnie TCP port 22).
   * Nie można użyć przekierowania portu / mapowania bez korzystania z usługi równoważenia obciążenia Azure.
4. Sprawdź hello [kondycja zasobów maszyny Wirtualnej](../../resource-health/resource-health-overview.md). 
   * Upewnij się, że hello maszyny Wirtualnej raporty jako będące w dobrej kondycji.
   * Jeśli masz włączoną diagnostykę rozruchu, sprawdź, czy hello maszyny Wirtualnej nie jest raportowanie błędów rozruchu w dziennikach hello.
5. Uruchom ponownie hello maszyny Wirtualnej.
6. Należy ponownie wdrożyć hello maszyny Wirtualnej.

Kontynuuj lekturę dla bardziej szczegółowe kroki rozwiązywania problemów oraz objaśnienia.

## <a name="available-methods-tootroubleshoot-ssh-connection-issues"></a>Problemy z połączeniem SSH tootroubleshoot dostępne metody
Można zresetować konfiguracji SSH, przy użyciu jednej z następujących metod hello lub poświadczeń:

* [Azure portal](#use-the-azure-portal) — dobrze, jeśli potrzebujesz tooquickly Resetowanie konfiguracji SSH hello lub klucza SSH, a nie hello Azure narzędzia są zainstalowane.
* [Azure CLI 2.0](#use-the-azure-cli-20) — Jeśli jesteś już w wierszu polecenia hello, szybko konfiguracji SSH hello resetowania lub poświadczeń. Można również użyć hello [Azure CLI w wersji 1.0](#use-the-azure-cli-10)
* [Azure rozszerzenia VMAccessForLinux](#use-the-vmaccess-extension) — tworzenie i ponowne użycie json definicji pliki tooreset hello SSH konfiguracji lub poświadczenia użytkownika.

Po wykonaniu każdego kroku rozwiązywania problemów spróbuj ponownie nawiązać połączenie tooyour maszyny Wirtualnej. Jeśli nadal nie można połączyć, spróbuj hello następnego kroku.

## <a name="use-hello-azure-portal"></a>Użyj hello portalu Azure
Hello Azure portal udostępnia hello tooreset szybko SSH konfiguracji lub poświadczenia użytkownika bez konieczności instalowania narzędzi na komputerze lokalnym.

Wybierz maszyny Wirtualnej w hello portalu Azure. Przewiń w dół toohello **pomocy technicznej i rozwiązywania problemów** a następnie wybierz opcję **resetowania hasła** jak hello poniższy przykład:

![Resetowanie konfiguracji SSH lub poświadczenia w hello portalu Azure](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-hello-ssh-configuration"></a>Zresetuj konfigurację protokołu SSH hello
Pierwszym krokiem, wybierz `Reset configuration only` z hello **tryb** menu rozwijane w hello poprzedzających zrzut ekranu, następnie kliknij przycisk hello **zresetować** przycisku. Po zakończeniu tej akcji, ponów tooaccess maszyny Wirtualnej.

### <a name="reset-ssh-credentials-for-a-user"></a>Resetowanie poświadczeń SSH dla użytkownika
tooreset hello poświadczeń istniejącego użytkownika, wybierz opcję `Reset SSH public key` lub `Reset password` z hello **tryb** menu rozwijanego jak hello poprzedzających zrzut ekranu. Określ nazwę użytkownika hello i klucz SSH lub nowe hasło, a następnie kliknij przycisk hello **zresetować** przycisku.

Można również utworzyć użytkownika z uprawnieniami sudo na powitania maszyny Wirtualnej z tego menu. Wprowadź nową nazwę użytkownika i skojarzone hasła lub klucza SSH, a następnie kliknij przycisk hello **zresetować** przycisku.

## <a name="use-hello-azure-cli-20"></a>Użyj hello Azure CLI 2.0
Jeśli nie jest jeszcze zainstalować hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) i zaloguj się za pomocą konta Azure tooan [logowania az](/cli/azure/#login).

Jeśli utworzony i przekazać niestandardowego obrazu dysku dla systemu Linux, upewnij się hello [agenta usługi Microsoft Azure Linux](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) wersji 2.0.5 lub nowszy jest zainstalowany. Dla maszyn wirtualnych utworzonych przy użyciu obrazów w galerii to rozszerzenie dostępu jest już zainstalowane i skonfigurowane dla Ciebie.

### <a name="reset-ssh-configuration"></a>Zresetuj konfigurację protokołu SSH
Można początkowo spróbuj zresetować hello SSH toodefault wartości konfiguracji i ponowny rozruch hello SSH serwera na powitania maszyny Wirtualnej. Należy pamiętać, że nie ma to wpływu hello nazwie konta, hasło lub kluczy SSH.
Witaj poniższym przykładzie użyto [az maszyny wirtualnej użytkownika resetowania-ssh](/cli/azure/vm/user#reset-ssh) tooreset konfiguracji SSH hello na powitania maszyny Wirtualnej o nazwie `myVM` w `myResourceGroup`. Użyj własne wartości w następujący sposób:

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a>Resetowanie poświadczeń SSH dla użytkownika
Witaj poniższym przykładzie użyto [aktualizację użytkownika maszyny wirtualnej az](/cli/azure/vm/user#update) tooreset hello poświadczeń dla `myUsername` toohello wartości określonej w `myPassword`, na powitania maszyny Wirtualnej o nazwie `myVM` w `myResourceGroup`. Użyj własne wartości w następujący sposób:

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

Jeśli przy użyciu uwierzytelniania klucza SSH, można zresetować hello klucza SSH dla danego użytkownika. Witaj poniższym przykładzie użyto **wirtualna az dostępu set-linux-user** tooupdate hello SSH klucza przechowywanego u `~/.ssh/id_rsa.pub` hello użytkownika o nazwie `myUsername`, na powitania maszyny Wirtualnej o nazwie `myVM` w `myResourceGroup`. Użyj własne wartości w następujący sposób:

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-hello-vmaccess-extension"></a>Użyj rozszerzenia VMAccess hello
odczytuje Hello rozszerzenia dostępu do maszyny Wirtualnej dla systemu Linux w pliku json, który definiuje akcje toocarry wychodzących. Dostępne są akcje Resetowanie SSHD, resetowanie klucza SSH lub dodanie użytkownika. Można nadal używać hello Azure CLI toocall hello rozszerzenia VMAccess, ale można użyć ponownie pliki w formacie json hello między wieloma maszynami wirtualnymi w razie potrzeby. Takie podejście umożliwia toocreate repozytorium pliki w formacie json, które następnie można wywołać dla danego scenariuszy.

### <a name="reset-sshd"></a>Resetuj SSHD
Utwórz plik o nazwie `settings.json` z hello następującej zawartości:

```json
{  
    "reset_ssh":"True"
}
```

Przy użyciu hello wiersza polecenia platformy Azure, możesz wywoływać hello `VMAccessForLinux` tooreset rozszerzenia SSHD połączenie przez określenie pliku json. Witaj poniższym przykładzie użyto [zestaw rozszerzenia maszyny wirtualnej az](/cli/azure/vm/extension#set) tooreset SSHD na powitania maszyny Wirtualnej o nazwie `myVM` w `myResourceGroup`. Użyj własne wartości w następujący sposób:

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a>Resetowanie poświadczeń SSH dla użytkownika
Jeśli SSHD pojawi się toofunction poprawnie, można zresetować hello poświadczeń użytkownika giver. tooreset hello hasła dla użytkownika, Utwórz plik o nazwie `settings.json`. Witaj poniższy przykład resetuje hello poświadczenia dla `myUsername` toohello wartości określonej w `myPassword`. Wprowadź hello następujące wiersze do Twojej `settings.json` plików przy użyciu własnych wartości:

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

Lub tooreset hello klucza SSH dla użytkownika, najpierw utwórz plik o nazwie `settings.json`. Witaj poniższy przykład resetuje hello poświadczenia dla `myUsername` toohello wartości określonej w `myPassword`, na powitania maszyny Wirtualnej o nazwie `myVM` w `myResourceGroup`. Wprowadź hello następujące wiersze do Twojej `settings.json` plików przy użyciu własnych wartości:

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

Po utworzeniu pliku json, użyj hello Azure CLI toocall hello `VMAccessForLinux` tooreset rozszerzenia poświadczenia użytkownika SSH, określając pliku json. Witaj poniższy przykład powoduje zresetowanie poświadczeń na powitania maszyny Wirtualnej o nazwie `myVM` w `myResourceGroup`. Użyj własne wartości w następujący sposób:

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-hello-azure-cli-10"></a>Użyj hello Azure CLI w wersji 1.0
Jeśli nie jest jeszcze, [zainstalować hello Azure CLI 1.0 i połączyć tooyour subskrypcji platformy Azure](../../cli-install-nodejs.md). Upewnij się, że używasz tryb usługi Resource Manager w następujący sposób:

```azurecli
azure config mode arm
```

Jeśli utworzony i przekazać niestandardowego obrazu dysku dla systemu Linux, upewnij się hello [agenta usługi Microsoft Azure Linux](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) wersji 2.0.5 lub nowszy jest zainstalowany. Dla maszyn wirtualnych utworzonych przy użyciu obrazów w galerii to rozszerzenie dostępu jest już zainstalowane i skonfigurowane dla Ciebie.

### <a name="reset-ssh-configuration"></a>Zresetuj konfigurację protokołu SSH
Konfiguracja SSHD Hello, sam może być niepoprawnie skonfigurowany lub hello Usługa napotkała błąd. Możesz resetować toomake SSHD się, że konfiguracji SSH hello sam jest nieprawidłowy. Resetowanie SSHD powinna być hello rozwiązywania problemów z krokiem, który należy wykonać.

Witaj poniższy przykład resetuje SSHD na maszynie Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`. Użyj nazwy grupy własną maszyny Wirtualnej i zasobów w następujący sposób:

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a>Resetowanie poświadczeń SSH dla użytkownika
SSHD widoczna toofunction poprawnie, można zresetować hasła hello giver użytkownika. Witaj poniższy przykład resetuje hello poświadczenia dla `myUsername` toohello wartości określonej w `myPassword`, na powitania maszyny Wirtualnej o nazwie `myVM` w `myResourceGroup`. Użyj własne wartości w następujący sposób:

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

Jeśli przy użyciu uwierzytelniania klucza SSH, można zresetować hello klucza SSH dla danego użytkownika. Po aktualizacji przykład Hello hello klucz SSH, przechowywane w `~/.ssh/id_rsa.pub` hello użytkownika o nazwie `myUsername`, na powitania maszyny Wirtualnej o nazwie `myVM` w `myResourceGroup`. Użyj własne wartości w następujący sposób:

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a>Ponowne uruchamianie maszyny wirtualnej
Jeśli masz zresetować hello SSH konfiguracji oraz poświadczenia użytkownika lub wystąpił błąd w ten sposób, można spróbować uruchomić tooaddress wirtualna hello bazowy problemów obliczeń.

### <a name="azure-portal"></a>Azure Portal
toorestart maszynę Wirtualną przy użyciu hello Azure portalu, wybierz tekst hello maszyny Wirtualnej i kliknij przycisk **ponowne uruchomienie** przycisku tak jak hello poniższy przykład:

![Uruchom ponownie Maszynę wirtualną w hello portalu Azure](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a>Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0
Po uruchomieniu przykład Hello hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`. Użyj własne wartości w następujący sposób:

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a>Interfejs wiersza polecenia platformy Azure 2.0
Witaj poniższym przykładzie użyto [ponownego uruchomienia maszyny wirtualnej az](/cli/azure/vm#restart) toorestart hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`. Użyj własne wartości w następujący sposób:

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a>Ponowne wdrażanie maszyny wirtualnej
Można ponownie wdrożyć węzła tooanother maszyny Wirtualnej w systemie Azure, która może rozwiązać problemy z siecią podstawowej. Informacje dotyczące ponownego wdrażania maszyny Wirtualnej, zobacz [ponownie wdrożyć toonew maszyny wirtualnej Azure węzła](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!NOTE]
> Po zakończeniu tej operacji, tymczasowych dane zostaną utracone i dynamicznych adresów IP, które są skojarzone z maszyną wirtualną hello zostaną zaktualizowane.
> 
> 

### <a name="azure-portal"></a>Azure Portal
tooredeploy maszynę Wirtualną przy użyciu hello Azure portalu, wybierz opcję sieci maszyny Wirtualnej i przewiń w dół toohello **pomocy technicznej i rozwiązywania problemów** sekcji. Kliknij przycisk hello **ponownie wdrożyć** przycisku tak jak hello poniższy przykład:

![Wdrożenie maszyny Wirtualnej w ramach hello portalu Azure](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a>Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0
powitania po wdraża ponownie przykład Witaj maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`. Użyj własne wartości w następujący sposób:

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a>Interfejs wiersza polecenia platformy Azure 2.0
Witaj następujące przykładowe zastosowanie [ponownego wdrażania maszyny wirtualnej az](/cli/azure/vm#redeploy) tooredeploy hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`. Użyj własne wartości w następujący sposób:

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-hello-classic-deployment-model"></a>Maszyny wirtualne utworzone przy użyciu klasycznego modelu wdrożenia hello
Spróbuj te kroki tooresolve hello najczęściej SSH błędów połączenia dla maszyn wirtualnych, które zostały utworzone przy użyciu hello klasycznego modelu wdrażania. Po wykonaniu każdego kroku spróbuj połączyć się ponownie toohello maszyny Wirtualnej.

* Zresetuj dostęp zdalny z hello [portalu Azure](https://portal.azure.com). Na hello portalu Azure, wybierz maszyny Wirtualnej i kliknij przycisk hello **zresetować zdalnego...**  przycisku.
* Uruchom ponownie hello maszyny Wirtualnej. Na powitania [portalu Azure](https://portal.azure.com)wybierz maszyny Wirtualnej i kliknij hello **ponowne uruchomienie** przycisku.
    
* Należy ponownie wdrożyć nowy węzeł Azure hello wirtualna tooa. Aby uzyskać informacje na temat tooredeploy maszyny Wirtualnej, zobacz [ponownie wdrożyć toonew maszyny wirtualnej Azure węzła](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  
    Po zakończeniu tej operacji, tymczasowych dane zostaną utracone i dynamicznych adresów IP, które są skojarzone z maszyną wirtualną hello zostaną zaktualizowane.
* Postępuj zgodnie z instrukcjami hello [jak tooreset hasła lub SSH dla maszyn wirtualnych z systemem Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) do:
  
  * Resetowanie hello hasła lub klucza SSH.
  * Utwórz *sudo* konta użytkownika.
  * Zresetuj konfigurację protokołu SSH hello.
* Sprawdź kondycję zasobu hello wirtualna dla problemów z platformą.<br>
     Wybierz maszyny Wirtualnej, a następnie przewiń w dół **ustawienia** > **kondycji Sprawdź**.

## <a name="additional-resources"></a>Dodatkowe zasoby
* Jeśli nadal nie tooSSH tooyour maszyny Wirtualnej po hello następujące po wykonaniu kroków, zobacz [bardziej szczegółowe kroki rozwiązywania problemów](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview dodatkowe kroki tooresolve problemu.
* Aby uzyskać więcej informacji dotyczących rozwiązywania problemów z dostęp do aplikacji, zobacz [Rozwiązywanie problemów dotyczących dostępu tooan aplikacja była uruchomiona na maszynie wirtualnej platformy Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Aby uzyskać więcej informacji dotyczących rozwiązywania problemów z maszyn wirtualnych, które zostały utworzone przy użyciu hello klasycznego modelu wdrażania, zobacz [jak tooreset hasła lub SSH dla maszyn wirtualnych z systemem Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

