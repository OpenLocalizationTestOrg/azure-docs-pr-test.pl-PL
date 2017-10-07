---
title: "Pulpit zdalny aaaDetailed rozwiązywania problemów na platformie Azure | Dokumentacja firmy Microsoft"
description: "Przeglądanie szczegółowe kroki rozwiązywania problemów dla zdalnego pulpitu błędy, którym nie tooa maszyn wirtualnych systemu Windows na platformie Azure"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
keywords: "Nie można połączyć z tooremote pulpitu, rozwiązywanie problemów z pulpitu zdalnego pulpitu zdalnego nie może połączyć błędy usług pulpitu zdalnego, rozwiązywania problemów pulpitu zdalnego, problemy z pulpitu zdalnego"
ms.assetid: 9da36f3d-30dd-44af-824b-8ce5ef07e5e0
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: fcb0d06aa66b748f3ebbbbe3431471d3cbe7c60d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-troubleshooting-steps-for-remote-desktop-connection-issues-toowindows-vms-in-azure"></a>Szczegółowe kroki rozwiązywania problemów dla usługi Podłączanie pulpitu zdalnego wystawia tooWindows maszyn wirtualnych na platformie Azure
Ten artykuł zawiera szczegółowe kroki rozwiązywania problemów toodiagnose i popraw błędy złożonych pulpitu zdalnego dla systemu Windows Azure maszyny wirtualne.

> [!IMPORTANT]
> tooeliminate hello rozwiązywać typowe błędy pulpitu zdalnego, upewnij się, że tooread [hello podstawowe artykuł dotyczący rozwiązywania problemów dla pulpitu zdalnego](troubleshoot-rdp-connection.md) przed kontynuowaniem.

Pulpit zdalny objęte komunikat o błędzie, który wygląda inaczej żadnego hello określone komunikaty o błędach mogą wystąpić [hello podstawowych pulpitem zdalnym przewodnik rozwiązywania problemów](troubleshoot-rdp-connection.md). Wykonaj te kroki toodetermine, dlaczego powitania klienta usług pulpitu zdalnego (RDP) jest tooconnect toohello RDP usługi na powitania maszyny Wirtualnej platformy Azure.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello ekspertów platformy Azure na [hello MSDN Azure i hello przepełnienie stosu fora](https://azure.microsoft.com/support/forums/). Alternatywnie można również pliku zdarzenia pomocy technicznej platformy Azure. Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) i kliknij przycisk **Get Support**. Aby uzyskać informacje o korzystaniu z pomocą techniczną platformy Azure, przeczytaj hello [często zadawane pytania dotyczące programu Microsoft Azure Obsługa](https://azure.microsoft.com/support/faq/).

## <a name="components-of-a-remote-desktop-connection"></a>Składniki połączenia pulpitu zdalnego
połączenie RDP obejmuje Hello następujące składniki:

![](./media/detailed-troubleshoot-rdp/tshootrdp_0.png)

Przed kontynuowaniem ułatwieniem może być toomentally Przejrzyj co zmienił się od hello ostatniego pomyślnego pulpitu zdalnego połączenia toohello maszyny Wirtualnej. Na przykład:

* Witaj publicznego adresu IP hello maszyny Wirtualnej lub hello usługi w chmurze zawierających hello maszyny Wirtualnej (nazywane również hello wirtualnego adresu IP [VIP](https://en.wikipedia.org/wiki/Virtual_IP_address)) została zmieniona. Hello RDP awarii może być spowodowane pamięć podręczną klienta DNS nadal ma hello *stary adres IP* zarejestrowany dla hello nazwy DNS. Opróżnienia pamięci podręcznej klienta DNS, a następnie spróbuj ponownie połączyć hello maszyny Wirtualnej. Lub spróbuj połączyć się bezpośrednio z hello nowego adresu VIP.
* Używasz toomanage aplikacji innych firm połączeń pulpitu zdalnego zamiast przy użyciu połączenia hello generowane przez hello portalu Azure. Sprawdź, czy w tej konfiguracji aplikacja hello obejmuje hello poprawne port TCP dla hello ruchu pulpitu zdalnego. Możesz sprawdzić tego portu klasyczne maszyny wirtualnej w hello [portalu Azure](https://portal.azure.com), klikając ustawienia hello maszyny Wirtualnej > punktów końcowych.

## <a name="preliminary-steps"></a>Czynności wstępne
Przed kontynuowaniem toohello szczegółowe Rozwiązywanie problemów

* Sprawdź stan hello hello maszyny wirtualnej w hello portal Azure oczywiste problemy.
* Wykonaj hello [przewodnik kroki szybkiej poprawki typowych błędów protokołu RDP podstawowe rozwiązywaniu hello](troubleshoot-rdp-connection.md#quick-troubleshooting-steps).

Spróbuj połączyć się ponownie po wykonaniu tych kroków toohello maszyny Wirtualnej za pośrednictwem pulpitu zdalnego.

## <a name="detailed-troubleshooting-steps"></a>Szczegółowe kroki rozwiązywania problemów
powitania klienta pulpitu zdalnego nie może być możliwe tooreach usługi pulpitu zdalnego hello na powitania maszyny Wirtualnej platformy Azure z powodu tooissues na powitania następujące źródła:

* [Komputer klienta usług pulpitu zdalnego](#source-1-remote-desktop-client-computer)
* [Urządzenie brzegowe intranetowych w organizacji](#source-2-organization-intranet-edge-device)
* [Punkt końcowy usługi w chmurze i uzyskiwać dostęp do listy kontroli (ACL)](#source-3-cloud-service-endpoint-and-acl)
* [Sieciowe grupy zabezpieczeń](#source-4-network-security-groups)
* [Oparte na systemie Windows Azure maszyny Wirtualnej](#source-5-windows-based-azure-vm)

## <a name="source-1-remote-desktop-client-computer"></a>Źródło 1: Komputer klienta usług pulpitu zdalnego
Sprawdź, czy komputer można utworzyć pulpitu zdalnego połączenia tooanother lokalnie, komputer z systemem Windows.

![](./media/detailed-troubleshoot-rdp/tshootrdp_1.png)

Jeśli nie możesz sprawdzić hello następujące ustawienia na komputerze:

* Ustawienia zapory lokalnej, która blokuje ruch pulpitu zdalnego.
* Lokalnie zainstalowane oprogramowanie serwera proxy klienta, który uniemożliwia połączeń pulpitu zdalnego.
* Lokalnie zainstalować oprogramowania, który uniemożliwia połączeń pulpitu zdalnego do monitorowania sieci.
* Inne rodzaje oprogramowania zabezpieczającego które monitorowania ruchu lub Zezwalaj/nie zezwalaj na określone typy ruchu, który uniemożliwia połączeń pulpitu zdalnego.

W takich przypadkach tymczasowo wyłączyć hello oprogramowania i spróbuj tooconnect tooan na komputerze lokalnym za pośrednictwem pulpitu zdalnego. Jeśli można znaleźć rzeczywista Przyczyna hello w ten sposób, współpracować z administratora toocorrect hello oprogramowania ustawienia tooallow pulpitu zdalnego połączenia sieciowe.

## <a name="source-2-organization-intranet-edge-device"></a>Źródło 2: Urządzenie brzegowe intranetu organizacji
Sprawdź, czy komputer bezpośrednio połączony toohello przez Internet tooyour połączeń usług pulpitu zdalnego maszyny wirtualnej platformy Azure.

![](./media/detailed-troubleshoot-rdp/tshootrdp_2.png)

Jeśli nie masz komputera podłączonego bezpośrednio toohello Internet, tworzenie i testowanie z nowej maszyny wirtualnej platformy Azure w usłudze chmury lub grupy zasobów. Aby uzyskać więcej informacji, zobacz [Utwórz maszynę wirtualną z systemem Windows na platformie Azure](../virtual-machines-windows-hero-tutorial.md). Można usunąć maszyny wirtualnej hello i hello grupy zasobów lub usługi w chmurze hello, po hello testu.

Jeśli można utworzyć połączenia pulpitu zdalnego z komputerem podłączony bezpośrednio toohello internetowe, sprawdź urządzenie krawędzi intranetu organizacji dla:

* Wewnętrzny Zapora blokuje HTTPS toohello połączeń internetowych.
* Serwer proxy uniemożliwia połączeń pulpitu zdalnego.
* Włamań lub oprogramowanie na urządzeniach w sieci krawędzi, która uniemożliwia połączeń pulpitu zdalnego do monitorowania sieci.

Współpraca z ustawień sieci administrator toocorrect hello z Twojej organizacji intranet krawędzi urządzenia tooallow oparty na protokole HTTPS pulpitu zdalnego połączenia toohello Internet.

## <a name="source-3-cloud-service-endpoint-and-acl"></a>Źródło 3: Punkt końcowy usługi w chmurze i listy ACL
Maszyny wirtualne utworzone przy użyciu klasycznego modelu wdrożenia hello, sprawdź innej maszyny Wirtualnej platformy Azure, która jest w hello sama usługa w chmurze lub sieci wirtualnej można wprowadzać tooyour połączeń usług pulpitu zdalnego maszyny Wirtualnej platformy Azure.

![](./media/detailed-troubleshoot-rdp/tshootrdp_3.png)

> [!NOTE]
> Dla maszyn wirtualnych utworzonych w Menedżerze zasobów, Pomiń zbyt[źródła 4: grup zabezpieczeń sieci](#source-4-network-security-groups).

Jeśli nie masz inną maszynę wirtualną w hello tej samej usługi w chmurze lub sieci wirtualnej, utwórz je. Wykonaj kroki hello w [Utwórz maszynę wirtualną z systemem Windows na platformie Azure](../virtual-machines-windows-hero-tutorial.md). Po zakończeniu testu hello, należy usunąć hello testowej maszyny wirtualnej.

Jeśli można połączyć za pośrednictwem pulpitu zdalnego maszyny wirtualnej tooa hello takie same w chmurze, usługi lub wirtualnych sieci, sprawdź, czy te ustawienia:

* Witaj konfiguracji punktu końcowego dla ruchu pulpitu zdalnego w celu hello maszyny Wirtualnej: port prywatny TCP hello hello punktu końcowego musi być zgodna hello port TCP, na które hello nasłuchuje usługa Pulpit zdalny maszyny Wirtualnej (wartość domyślna to 3389).
* Witaj listy ACL punktu końcowego ruchu pulpitu zdalnego hello w celu hello maszyny Wirtualnej: listy ACL umożliwiają toospecify dozwolony lub niedozwolony ruch przychodzący z hello Internet na podstawie źródłowego adresu IP. Nieprawidłowo skonfigurowane listy kontroli dostępu można zapobiec toohello ruchu przychodzącego usług pulpitu zdalnego punktu końcowego. Sprawdź tooensure Twojego listy ACL, ruch przychodzący z publicznych adresów IP, serwer proxy lub inny serwer krawędzi jest dozwolony. Aby uzyskać więcej informacji, zobacz [co to jest sieć listy kontroli dostępu (ACL)?](../../virtual-network/virtual-networks-acl.md)

toocheck Jeśli hello punkt końcowy jest źródłem hello hello problemu, Usuń hello bieżący punkt końcowy i utworzyć nową, wybierając losowego portu hello zakresu 49152 – 65535 hello numeru portu zewnętrznego. Aby uzyskać więcej informacji, zobacz [jak tooset maszyny wirtualnej tooa punkty końcowe](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="source-4-network-security-groups"></a>Źródła 4: Grupy zabezpieczeń sieci
Grupy zabezpieczeń sieci umożliwiają większą kontrolę nad dozwolonego ruchu przychodzącego i wychodzącego. Można utworzyć zasady obejmujące podsieci i usług w sieci wirtualnej platformy Azure w chmurze.

Użyj [Sprawdź przepływ IP](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) tooconfirm, jeśli zasada grupy zabezpieczeń sieci blokuje tooor ruch z maszyny wirtualnej. Można również przejrzeć grupy efektywnym elementem systemu zabezpieczeń, które reguły tooensure ruchu przychodzącego "Zezwalaj" NSG reguły istnieje i jest priorytety dla portu protokołu RDP (ustawienie domyślne 3389). Aby uzyskać więcej informacji, zobacz [przepływu ruchu przy użyciu reguł zabezpieczeń skuteczne tootroubleshoot maszyny Wirtualnej](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).

## <a name="source-5-windows-based-azure-vm"></a>Źródło 5: Opartych na systemie Windows Azure maszyny Wirtualnej
![](./media/detailed-troubleshoot-rdp/tshootrdp_5.png)

Postępuj zgodnie z instrukcjami hello [w tym artykule](reset-rdp.md). W tym artykule resetuje hello usługi pulpitu zdalnego na maszynie wirtualnej hello:

* Włącz regułę domyślną "Pulpit zdalny" Zapora systemu Windows hello (port 3389 protokołu TCP).
* Włączenie połączeń pulpitu zdalnego przez ustawienie too0 wartość rejestru HKLM\System\CurrentControlSet\Control\Terminal Server\fDenyTSConnections hello.

Spróbuj hello ponownie nawiązać połączenie z komputera. Jeśli nadal nie możesz tooconnect za pośrednictwem pulpitu zdalnego, sprawdź powitania po możliwych problemów:

* Witaj usługi pulpitu zdalnego nie jest uruchomiona na powitania docelowej maszyny Wirtualnej.
* Hello usługi Pulpit zdalny nie nasłuchuje portu 3389 protokołu TCP.
* Zapora systemu Windows lub innej zapory lokalnej ma wychodzącą regułę, która uniemożliwia ruchu pulpitu zdalnego.
* Włamań lub oprogramowania uruchomionego na powitania maszyny wirtualnej platformy Azure do monitorowania sieci uniemożliwia połączeń pulpitu zdalnego.

Dla maszyn wirtualnych utworzonych przy użyciu hello klasycznego modelu wdrażania można użyć zdalnego toohello sesji programu Azure PowerShell maszyny wirtualnej platformy Azure. Najpierw należy tooinstall certyfikatu dla maszyny wirtualnej hello usługi hostingu w chmurze. Przejdź za[tooAzure skonfigurować bezpiecznego środowiska PowerShell dostępu zdalnego maszyn wirtualnych](http://gallery.technet.microsoft.com/scriptcenter/Configures-Secure-Remote-b137f2fe) i Pobierz hello **InstallWinRMCertAzureVM.ps1** komputera lokalnego tooyour pliku skryptu.

Następnie zainstaluj programu Azure PowerShell, jeśli nie jest jeszcze. Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

Następnie otwórz wiersz polecenia programu PowerShell systemu Azure i zmienić hello bieżącego toohello lokalizację folderu hello **InstallWinRMCertAzureVM.ps1** pliku skryptu. toorun skryptu programu Azure PowerShell, należy ustawić zasady wykonywania poprawne hello. Uruchom hello **Get-ExecutionPolicy** polecenia toodetermine aktualny poziom zasad. Informacje o ustawianiu hello odpowiedni poziom, zobacz [Set-ExecutionPolicy](https://technet.microsoft.com/library/hh849812.aspx).

Następnie wypełnij nazwę subskrypcji platformy Azure, nazwa usługi w chmurze hello i nazwy maszyny wirtualnej (usuwanie hello < i > znaków), a następnie uruchom następujące polecenia.

```powershell
$subscr="<Name of your Azure subscription>"
$serviceName="<Name of hello cloud service that contains hello target virtual machine>"
$vmName="<Name of hello target virtual machine>"
.\InstallWinRMCertAzureVM.ps1 -SubscriptionName $subscr -ServiceName $serviceName -Name $vmName
```

Nazwa subskrypcji poprawne hello można pobrać z hello *Nazwa subskrypcji* właściwości wyświetlania hello hello **Get-AzureSubscription** polecenia. Nazwa usługi w chmurze hello hello maszyny wirtualnej można uzyskać z hello *ServiceName* kolumny w hello wyświetlanie hello **Get-AzureVM** polecenia.

Sprawdź, czy masz hello nowego certyfikatu. Otwórz przystawkę Certyfikaty dla bieżącego użytkownika hello i Znajdź hello **zaufany główny Certification Authorities\Certificates** folderu. Powinny pojawić się certyfikatu z nazwą DNS hello usługi w chmurze w hello toocolumn wydany (przykład: cloudservice4testing.cloudapp.net).

Następnie zainicjować sesję zdalną programu Azure PowerShell przy użyciu tych poleceń.

```powershell
$uri = Get-AzureWinRMUri -ServiceName $serviceName -Name $vmName
$creds = Get-Credential
Enter-PSSession -ConnectionUri $uri -Credential $creds
```

Po wprowadzeniu poświadczeń administratora prawidłowe, powinny być widoczne coś podobnego toohello po wierszu programu Azure PowerShell:

```powershell
[cloudservice4testing.cloudapp.net]: PS C:\Users\User1\Documents>
```

Pierwsza część tego monitu Hello jest nazwę usługi w chmurze zawierającego hello docelowej maszyny Wirtualnej, może być inny niż "cloudservice4testing.cloudapp.net". Teraz można wydać polecenia programu PowerShell systemu Azure dla tej chmury usługi tooinvestigate hello problemy wspomniane i popraw konfigurację hello.

### <a name="toomanually-correct-hello-remote-desktop-services-listening-tcp-port"></a>toomanually Popraw hello usług pulpitu zdalnego nasłuchiwania na porcie TCP
W wierszu hello zdalnego programu Azure PowerShell sesji Uruchom to polecenie.

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

Właściwość PortNumber Hello pokazuje hello bieżący numer portu. W razie potrzeby zmień hello pulpitu zdalnego portu numer wstecz tooits wartość domyślna (3389) za pomocą tego polecenia.

```powershell
Set-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber" -Value 3389
```

Upewnij się, że hello port zostało zmienione too3389 za pomocą tego polecenia.

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

Zamknąć sesji zdalnej programu Azure PowerShell hello za pomocą tego polecenia.

```powershell
Exit-PSSession
```

Sprawdź, czy tego punktu końcowego pulpitu zdalnego dla maszyny Wirtualnej Azure hello hello również używa portu TCP 3398 jako wewnętrznego portu. Uruchom ponownie hello maszyny Wirtualnej platformy Azure, a następnie spróbuj ponownie Podłączanie pulpitu zdalnego hello.

## <a name="additional-resources"></a>Dodatkowe zasoby
[Jak usługa tooreset hasła lub hello pulpitu zdalnego dla maszyn wirtualnych systemu Windows](reset-rdp.md)

[Jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview)

[Rozwiązywanie problemów z Secure Shell (SSH) połączeń tooa opartych na systemie Linux maszyny wirtualnej platformy Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Rozwiązywanie problemów z dostępu tooan aplikacji uruchomionych na maszynie wirtualnej platformy Azure](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

