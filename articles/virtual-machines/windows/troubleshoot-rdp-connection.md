---
title: "aaaCannot połączenie z tooa RDP maszyny Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów, gdy nie można połączyć z tooyour maszyny wirtualnej systemu Windows na platformie Azure przy użyciu pulpitu zdalnego"
keywords: "Błąd pulpitu zdalnego, błąd połączeń usług pulpitu zdalnego nie może połączyć się z tooVM, rozwiązywania problemów pulpitu zdalnego"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 0d740f8e-98b8-4e55-bb02-520f604f5b18
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: bbb36136e7a4b187fe8deea621d2b8d46d8aa102
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-remote-desktop-connections-tooan-azure-virtual-machine"></a>Rozwiązywanie problemów z tooan połączeń usług pulpitu zdalnego maszyny wirtualnej platformy Azure
Witaj protokołu RDP (Remote Desktop) połączenia tooyour opartych na systemie Windows Azure maszyny wirtualnej (VM) może zakończyć się niepowodzeniem z różnych powodów, jeśli pozostanie tooaccess maszyny Wirtualnej. problem Hello można z hello usługi pulpitu zdalnego na powitania maszyny Wirtualnej, połączenie sieciowe hello lub powitania klienta pulpitu zdalnego na komputerze hosta. W tym artykule przedstawiono niektóre hello najbardziej typowe metody tooresolve problemów z połączeniem RDP. 

Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello ekspertów platformy Azure na [hello fora MSDN Azure i przepełnienie stosu](https://azure.microsoft.com/support/forums/). Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure. Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) i wybierz **uzyskać obsługuje**.

<a id="quickfixrdp"></a>

## <a name="quick-troubleshooting-steps"></a>Szybkie kroki rozwiązywania problemów
Po wykonaniu każdego kroku rozwiązywania problemów spróbuj połączyć się ponownie toohello maszyny Wirtualnej:

1. Zresetuj konfigurację pulpitu zdalnego.
2. Grupy zabezpieczeń sieci Sprawdź zasady / w chmurze usługi punktów końcowych.
3. Przejrzyj dzienniki konsoli maszyny Wirtualnej.
4. Resetuj hello kart interfejsu Sieciowego dla hello maszyny Wirtualnej.
5. Witaj Sprawdź kondycję zasobu maszyny Wirtualnej.
6. Resetowanie hasła maszyny Wirtualnej.
7. Ponowne uruchomienie maszyny Wirtualnej.
8. Należy ponownie wdrożyć maszyny Wirtualnej.

Aby uzyskać bardziej szczegółowy opis kroków i wyjaśnienia, Kontynuuj lekturę. Sprawdź ten lokalnych urządzeń sieciowych, takich jak routery i zapory nie blokują ruchu wychodzącego TCP portu 3389, zgodnie z opisem w [szczegółowe RDP scenariuszach rozwiązywania problemów z](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!TIP]
> Jeśli hello **Connect** przycisk dla maszyny Wirtualnej jest wyszarzony limit w portalu hello i nie jesteś tooAzure połączonych za pośrednictwem [Express Route](../../expressroute/expressroute-introduction.md) lub [sieci VPN typu lokacja-lokacja](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) połączenia, należy toocreate i przypisz adres publiczny adres IP maszyny Wirtualnej przed użyciem pulpitu zdalnego. Więcej informacji o [publicznych adresach IP na platformie Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).


## <a name="ways-tootroubleshoot-rdp-issues"></a>Problemy z tootroubleshoot sposoby protokołu RDP
Można rozwiązać, maszyny wirtualne utworzone przy użyciu modelu wdrażania usługi Resource Manager hello przy użyciu jednej z następujących metod hello:

* [Azure portal](#using-the-azure-portal) — dobrze, jeśli potrzebujesz tooquickly zresetować hello RDP konfiguracji lub poświadczenia użytkownika, a nie hello Azure narzędzia są zainstalowane.
* [Program Azure PowerShell](#using-azure-powershell) — Jeśli masz doświadczenia z wiersza polecenia programu PowerShell szybko resetowania hello RDP konfiguracji lub poświadczenia użytkownika przy użyciu poleceń cmdlet programu Azure PowerShell hello.

Możesz również znaleźć kroki dotyczące rozwiązywania problemów z maszyn wirtualnych utworzonych przy użyciu hello [klasycznego modelu wdrożenia](#troubleshoot-vms-created-using-the-classic-deployment-model).

<a id="fix-common-remote-desktop-errors"></a>

## <a name="troubleshoot-using-hello-azure-portal"></a>Rozwiązywanie problemów przy użyciu hello portalu Azure
Po wykonaniu każdego kroku rozwiązywania problemów spróbuj ponownie nawiązać połączenie tooyour maszyny Wirtualnej. Jeśli nadal nie można połączyć, spróbuj hello następnego kroku.

1. **Zresetuj połączenie RDP**. Ten krok rozwiązywania problemów powoduje zresetowanie konfiguracji RDP hello podczas połączenia zdalne są wyłączone lub reguł zapory systemu Windows blokuje RDP, na przykład.
   
    Wybierz maszyny Wirtualnej w hello portalu Azure. Przewiń w dół hello ustawienia okienka toohello **pomocy technicznej i rozwiązywania problemów** sekcji w dolnej części listy hello. Kliknij przycisk hello **resetowania hasła** przycisku. Zestaw hello **tryb** za**Resetowanie tylko konfiguracji** , a następnie kliknij przycisk hello **aktualizacji** przycisk:
   
    ![Zresetowanie konfiguracji RDP hello w hello portalu Azure](./media/troubleshoot-rdp-connection/reset-rdp.png)
2. **Zasady grupy zabezpieczeń sieci Sprawdź**. Użyj [Sprawdź przepływ IP](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) tooconfirm, jeśli zasada grupy zabezpieczeń sieci blokuje tooor ruch z maszyny wirtualnej. Można również przejrzeć grupy efektywnym elementem systemu zabezpieczeń, które reguły tooensure ruchu przychodzącego "Zezwalaj" NSG reguły istnieje i jest priorytety dla portu protokołu RDP (ustawienie domyślne 3389). Aby uzyskać więcej informacji, zobacz [przepływu ruchu przy użyciu reguł zabezpieczeń skuteczne tootroubleshoot maszyny Wirtualnej](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).

3. **Przejrzyj diagnostyki rozruchu maszyny Wirtualnej**. Ten krok rozwiązywania problemów przegląda toodetermine dzienniki konsoli maszyny Wirtualnej hello hello wirtualna zgłoszenie problemu. Nie wszystkie maszyny wirtualne mają diagnostyki rozruchu włączone, więc ten krok rozwiązywania problemów może być opcjonalny.
   
    Określone kroki rozwiązywania problemów wykraczają poza zakres tego artykułu hello, ale może wskazywać na problem szersze, który ma wpływ na połączenie RDP. Aby uzyskać więcej informacji na temat przeglądania i dzienniki konsoli hello zrzut ekranu maszyny Wirtualnej, zobacz [diagnostyki rozruchu dla maszyn wirtualnych](boot-diagnostics.md).

4. **Resetowanie hello karty Sieciowej dla maszyny Wirtualnej hello**. Aby uzyskać więcej informacji, zobacz [jak tooreset karty Sieciowej dla maszyny Wirtualnej systemu Windows Azure](reset-network-interface.md).
5. **Sprawdź hello kondycja zasobów maszyny Wirtualnej**. Ten krok rozwiązywania problemów sprawdza, czy nie ma żadnych znanych problemów z hello platformy Azure, które mogą mieć wpływ na łączność toohello maszyny Wirtualnej.
   
    Wybierz maszyny Wirtualnej w hello portalu Azure. Przewiń w dół hello ustawienia okienka toohello **pomocy technicznej i rozwiązywania problemów** sekcji w dolnej części listy hello. Kliknij przycisk hello **kondycja zasobów** przycisku. Raporty dobrej kondycji maszyny Wirtualnej jako **dostępne**:
   
    ![Sprawdź kondycję zasobu maszyny Wirtualnej w portalu Azure hello](./media/troubleshoot-rdp-connection/check-resource-health.png)
6. **Resetowanie poświadczeń użytkownika**. Ten krok rozwiązywania problemów resetuje hasło hello na konto administratora lokalnego pewności lub pamiętasz hello poświadczenia.
   
    Wybierz maszyny Wirtualnej w hello portalu Azure. Przewiń w dół hello ustawienia okienka toohello **pomocy technicznej i rozwiązywania problemów** sekcji w dolnej części listy hello. Kliknij przycisk hello **resetowania hasła** przycisku. Upewnij się, że hello **tryb** ustawiono zbyt**resetowania hasła** , a następnie wprowadź nazwy użytkownika i nowe hasło. Na koniec kliknij hello **aktualizacji** przycisk:
   
    ![Resetowanie poświadczeń użytkownika hello w hello portalu Azure](./media/troubleshoot-rdp-connection/reset-password.png)
7. **Ponowne uruchomienie maszyny Wirtualnej**. Ten krok rozwiązywania problemów można rozwiązać problemy podstawowej ma hello samej maszyny Wirtualnej.
   
    Wybierz maszyny Wirtualnej hello portalu Azure i kliknij przycisk hello **omówienie** kartę. Kliknij przycisk hello **ponowne uruchomienie** przycisk:
   
    ![Uruchom ponownie hello maszyny Wirtualnej w hello portalu Azure](./media/troubleshoot-rdp-connection/restart-vm.png)
8. **Wdrożenie maszyny Wirtualnej**. Ten krok rozwiązywania problemów wdraża ponownie hoście tooanother maszyny Wirtualnej w ramach platformy Azure toocorrect problemach podstawowej platformy lub sieci.
   
    Wybierz maszyny Wirtualnej w hello portalu Azure. Przewiń w dół hello ustawienia okienka toohello **pomocy technicznej i rozwiązywania problemów** sekcji w dolnej części listy hello. Kliknij przycisk hello **ponownie wdrożyć** przycisk, a następnie kliknij przycisk **ponownie wdrożyć**:
   
    ![Należy ponownie wdrożyć hello maszyny Wirtualnej w portalu Azure hello](./media/troubleshoot-rdp-connection/redeploy-vm.png)
   
    Po zakończeniu tej operacji, danych tymczasowych dysku jest utracone i dynamicznych adresów IP, które są skojarzone z hello maszyny Wirtualnej zostały zaktualizowane.

Jeśli nadal wystąpią problemy RDP, możesz [otwarcia żądania pomocy technicznej](https://azure.microsoft.com/support/options/) lub odczytać [bardziej szczegółowe Rozwiązywanie problemów z założenia i kroki RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="troubleshoot-using-azure-powershell"></a>Rozwiązywanie problemów przy użyciu programu Azure PowerShell
Jeśli nie jest jeszcze, [Instalowanie i konfigurowanie hello najnowsze programu Azure PowerShell](/powershell/azure/overview).

Witaj następujące przykłady używania zmiennych takich jak `myResourceGroup`, `myVM`, i `myVMAccessExtension`. Zastąp własne wartości tych zmiennych nazwy i lokalizacje.

> [!NOTE]
> Resetuj hello poświadczenia użytkownika i konfiguracji RDP hello przy użyciu hello [AzureRmVMAccessExtension zestaw](/powershell/module/azurerm.compute/set-azurermvmaccessextension) polecenia cmdlet programu PowerShell. W następujące przykłady, hello `myVMAccessExtension` jest określony jako część procesu hello nazwą. Wcześniej użytkownicy mający doświadczenie z hello VMAccessAgent, nazwę hello hello istniejące rozszerzenie można uzyskać za pomocą `Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"` toocheck właściwości hello hello maszyny Wirtualnej. Nazwa hello tooview, Szukaj w sekcji rozszerzenia"hello" hello danych wyjściowych.

Po wykonaniu każdego kroku rozwiązywania problemów spróbuj ponownie nawiązać połączenie tooyour maszyny Wirtualnej. Jeśli nadal nie można połączyć, spróbuj hello następnego kroku.

1. **Zresetuj połączenie RDP**. Ten krok rozwiązywania problemów powoduje zresetowanie konfiguracji RDP hello podczas połączenia zdalne są wyłączone lub reguł zapory systemu Windows blokuje RDP, na przykład.
   
    przykład Witaj wykonaj resetuje połączenie RDP hello na maszynie Wirtualnej o nazwie `myVM` w hello `WestUS` lokalizacji i w grupie zasobów hello o nazwie `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location Westus -Name "myVMAccessExtension"
    ```
2. **Zasady grupy zabezpieczeń sieci Sprawdź**. Ten krok rozwiązywania problemów sprawdza, czy zastosowano reguły w ruchu protokołu RDP toopermit grupy zabezpieczeń sieci. Witaj domyślnego portu dla protokołu RDP jest portu 3389 protokołu TCP. Ruch RDP toopermit reguła może nie zostać utworzony automatycznie po utworzeniu maszyny Wirtualnej.
   
    Najpierw należy przypisać wszystkie dane konfiguracyjne hello toohello Twojego sieciowej grupy zabezpieczeń `$rules` zmiennej. Witaj poniższy przykład uzyskuje informacje o hello sieciową grupę zabezpieczeń o nazwie `myNetworkSecurityGroup` hello grupy zasobów o nazwie `myResourceGroup`:
   
    ```powershell
    $rules = Get-AzureRmNetworkSecurityGroup -ResourceGroupName "myResourceGroup" `
        -Name "myNetworkSecurityGroup"
    ```
   
    Teraz przeglądanie hello reguł, które są skonfigurowane dla tej grupy zabezpieczeń sieci. Sprawdź, czy reguła istnieje tooallow TCP portu 3389 dla połączeń przychodzących w następujący sposób:
   
    ```powershell
    $rules.SecurityRules
    ```
   
    Witaj poniższy przykład przedstawia regułę podmioty zabezpieczeń, która zezwala na ruch RDP. Widać `Protocol`, `DestinationPortRange`, `Access`, i `Direction` są prawidłowo skonfigurowane:
   
    ```powershell
    Name                     : default-allow-rdp
    Id                       : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/default-allow-rdp
    Etag                     : 
    ProvisioningState        : Succeeded
    Description              : 
    Protocol                 : TCP
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : *
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 1000
    Direction                : Inbound
    ```
   
    Jeśli nie masz regułę zezwalającą na ruch RDP, [utworzyć regułę grupy zabezpieczeń sieci](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Zezwalaj na portu 3389 protokołu TCP.
3. **Resetowanie poświadczeń użytkownika**. Ten krok rozwiązywania problemów resetuje hello hasło konta administratora lokalnego hello, określona podczas pewności lub zapomniał hello poświadczeń.
   
    Najpierw określ hello nazwy użytkownika i nowe hasło, przypisując poświadczenia toohello `$cred` zmiennej w następujący sposób:
   
    ```powershell
    $cred=Get-Credential
    ```
   
    Teraz Zaktualizuj poświadczenia hello na maszynie Wirtualnej. Witaj poniższy przykład aktualizacji poświadczeń hello na maszynie Wirtualnej o nazwie `myVM` w hello `WestUS` lokalizacji i w grupie zasobów hello o nazwie `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location WestUS -Name "myVMAccessExtension" `
        -UserName $cred.GetNetworkCredential().Username `
        -Password $cred.GetNetworkCredential().Password
    ```
4. **Ponowne uruchomienie maszyny Wirtualnej**. Ten krok rozwiązywania problemów można rozwiązać problemy podstawowej ma hello samej maszyny Wirtualnej.
   
    Po uruchomieniu przykład Hello hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`:
   
    ```powershell
    Restart-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
    ```
5. **Wdrożenie maszyny Wirtualnej**. Ten krok rozwiązywania problemów wdraża ponownie hoście tooanother maszyny Wirtualnej w ramach platformy Azure toocorrect problemach podstawowej platformy lub sieci.
   
    powitania po wdraża ponownie przykład Witaj maszyny Wirtualnej o nazwie `myVM` w hello `WestUS` lokalizacji i w grupie zasobów hello o nazwie `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

Jeśli nadal wystąpią problemy RDP, możesz [otwarcia żądania pomocy technicznej](https://azure.microsoft.com/support/options/) lub odczytać [bardziej szczegółowe Rozwiązywanie problemów z założenia i kroki RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="troubleshoot-vms-created-using-hello-classic-deployment-model"></a>Rozwiązywanie problemów z maszyn wirtualnych utworzonych przy użyciu klasycznego modelu wdrożenia hello
Po wykonaniu każdego kroku rozwiązywania problemów spróbuj połączyć się ponownie toohello maszyny Wirtualnej.

1. **Zresetuj połączenie RDP**. Ten krok rozwiązywania problemów powoduje zresetowanie konfiguracji RDP hello podczas połączenia zdalne są wyłączone lub reguł zapory systemu Windows blokuje RDP, na przykład.
   
    Wybierz maszyny Wirtualnej w hello portalu Azure. Kliknij przycisk hello **... Więcej** przycisk, a następnie kliknij przycisk **Resetuj dostęp zdalny**:
   
    ![Zresetowanie konfiguracji RDP hello w hello portalu Azure](./media/troubleshoot-rdp-connection/classic-reset-rdp.png)
2. **Sprawdzanie punktów końcowych usługi w chmurze**. Ten krok rozwiązywania problemów sprawdza mają punkty końcowe w ruchu protokołu RDP toopermit usługi w chmurze. Witaj domyślnego portu dla protokołu RDP jest portu 3389 protokołu TCP. Ruch RDP toopermit reguła może nie zostać utworzony automatycznie po utworzeniu maszyny Wirtualnej.
   
   Wybierz maszyny Wirtualnej w hello portalu Azure. Kliknij przycisk hello **punkty końcowe** przycisk punkty końcowe hello tooview obecnie skonfigurowane dla maszyny Wirtualnej. Sprawdź, czy istnieją punkty końcowe, które zezwalają na ruch RDP na portu 3389 protokołu TCP.
   
   Witaj poniższy przykład przedstawia prawidłowe punkty końcowe, które zezwala na ruch RDP:
   
   ![Sprawdzanie punktów końcowych usługi w chmurze w hello portalu Azure](./media/troubleshoot-rdp-connection/classic-verify-cloud-services-endpoints.png)
   
   Jeśli nie masz punktu końcowego, który zezwala na ruch RDP, [Tworzenie punktu końcowego usługi w chmurze](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Zezwalaj tooprivate portu 3389 protokołu TCP.
3. **Przejrzyj diagnostyki rozruchu maszyny Wirtualnej**. Ten krok rozwiązywania problemów przegląda toodetermine dzienniki konsoli maszyny Wirtualnej hello hello wirtualna zgłoszenie problemu. Nie wszystkie maszyny wirtualne mają diagnostyki rozruchu włączone, więc ten krok rozwiązywania problemów może być opcjonalny.
   
    Określone kroki rozwiązywania problemów wykraczają poza zakres tego artykułu hello, ale może wskazywać na problem szersze, który ma wpływ na połączenie RDP. Aby uzyskać więcej informacji na temat przeglądania i dzienniki konsoli hello zrzut ekranu maszyny Wirtualnej, zobacz [diagnostyki rozruchu dla maszyn wirtualnych](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).
4. **Sprawdź hello kondycja zasobów maszyny Wirtualnej**. Ten krok rozwiązywania problemów sprawdza, czy nie ma żadnych znanych problemów z hello platformy Azure, które mogą mieć wpływ na łączność toohello maszyny Wirtualnej.
   
    Wybierz maszyny Wirtualnej w hello portalu Azure. Przewiń w dół hello ustawienia okienka toohello **pomocy technicznej i rozwiązywania problemów** sekcji w dolnej części listy hello. Kliknij przycisk hello **kondycja zasobów** przycisku. Raporty dobrej kondycji maszyny Wirtualnej jako **dostępne**:
   
    ![Sprawdź kondycję zasobu maszyny Wirtualnej w portalu Azure hello](./media/troubleshoot-rdp-connection/classic-check-resource-health.png)
5. **Resetowanie poświadczeń użytkownika**. Ten krok rozwiązywania problemów resetuje hello hasło konta administratora lokalnego hello można określić podczas pewności lub pamiętasz hello poświadczeń.
   
    Wybierz maszyny Wirtualnej w hello portalu Azure. Przewiń w dół hello ustawienia okienka toohello **pomocy technicznej i rozwiązywania problemów** sekcji w dolnej części listy hello. Kliknij przycisk hello **resetowania hasła** przycisku. Wprowadź nazwy użytkownika i nowe hasło. Na koniec kliknij hello **zapisać** przycisk:
   
    ![Resetowanie poświadczeń użytkownika hello w hello portalu Azure](./media/troubleshoot-rdp-connection/classic-reset-password.png)
6. **Ponowne uruchomienie maszyny Wirtualnej**. Ten krok rozwiązywania problemów można rozwiązać problemy podstawowej ma hello samej maszyny Wirtualnej.
   
    Wybierz maszyny Wirtualnej hello portalu Azure i kliknij przycisk hello **omówienie** kartę. Kliknij przycisk hello **ponowne uruchomienie** przycisk:
   
    ![Uruchom ponownie hello maszyny Wirtualnej w hello portalu Azure](./media/troubleshoot-rdp-connection/classic-restart-vm.png)

Jeśli nadal wystąpią problemy RDP, możesz [otwarcia żądania pomocy technicznej](https://azure.microsoft.com/support/options/) lub odczytać [bardziej szczegółowe Rozwiązywanie problemów z założenia i kroki RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="troubleshoot-specific-rdp-errors"></a>Rozwiązywanie problemów z określonych błędów protokołu RDP
Możesz napotkać komunikat o błędzie podczas próby tooyour tooconnect maszyny Wirtualnej za pomocą protokołu RDP. najbardziej typowe komunikaty o błędach programu hello są następujące Hello:

* [Witaj, sesja zdalna została rozłączona, ponieważ nie ma żadnych tooprovide dostępne serwery licencji usług pulpitu zdalnego licencji](troubleshoot-specific-rdp-errors.md#rdplicense).
* [Pulpit zdalny nie może odnaleźć hello komputera "name"](troubleshoot-specific-rdp-errors.md#rdpname).
* [Wystąpił błąd uwierzytelniania. Witaj urzędu zabezpieczeń lokalnych nie można skontaktować się z](troubleshoot-specific-rdp-errors.md#rdpauth).
* [Błąd zabezpieczeń systemu Windows: Twoje poświadczenia nie działają](troubleshoot-specific-rdp-errors.md#wincred).
* [Ten komputer nie może połączyć z komputerem zdalnym toohello](troubleshoot-specific-rdp-errors.md#rdpconnect).

## <a name="additional-resources"></a>Dodatkowe zasoby
Jeśli żaden z tych błędów wystąpił i nadal nie możesz połączyć toohello maszyny Wirtualnej za pośrednictwem pulpitu zdalnego, odczytać hello szczegółowe [Podręcznik rozwiązywania problemów dotyczących usług pulpitu zdalnego](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Kroki podczas uzyskiwania dostępu do aplikacji działających na maszynie Wirtualnej, zobacz [Rozwiązywanie problemów dotyczących dostępu tooan aplikacja była uruchomiona na maszynie Wirtualnej platformy Azure](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Jeśli występują problemy przy użyciu protokołu Secure Shell (SSH) tooconnect tooa maszyny Wirtualnej systemu Linux na platformie Azure, zobacz [Rozwiązywanie problemów z SSH połączeń tooa maszyny Wirtualnej systemu Linux na platformie Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

