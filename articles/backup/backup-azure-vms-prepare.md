---
title: "aaaPreparing tooback Twojego środowiska zapasową maszyn wirtualnych platformy Azure | Dokumentacja firmy Microsoft"
description: "Upewnij się, że środowisko jest przygotowane do tworzenia kopii zapasowych maszyn wirtualnych na platformie Azure"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonn
editor: 
keywords: Tworzenie kopii zapasowych; Tworzenie kopii zapasowej;
ms.assetid: 238ab93b-8acc-4262-81b7-ce930f76a662
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/25/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 3b914c507dd6ad703ea799115ae84ac229e27787
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-environment-tooback-up-azure-virtual-machines"></a>Przygotowanie Twojego środowiska tooback zapasową maszyn wirtualnych platformy Azure
> [!div class="op_single_selector"]
> * [Model usługi Resource Manager](backup-azure-arm-vms-prepare.md)
> * [Modelu klasycznego](backup-azure-vms-prepare.md)
>
>

Przed utworzeniem kopii zapasowej maszyny wirtualnej platformy Azure (VM), istnieją trzy warunki, które musi istnieć.

* Należy toocreate magazynu kopii zapasowych, lub określa istniejącego magazynu kopii zapasowych *w hello tym samym regionie co maszyna wirtualna*.
* Ustanów połączenie sieciowe między hello Azure publicznej sieci Internet adresów i hello punkty końcowe usługi Azure storage.
* Zainstaluj agenta maszyny Wirtualnej hello na powitania maszyny Wirtualnej.

Jeśli znasz te warunki już istnieje w danym środowisku, a następnie kontynuować toohello [kopii zapasowych maszyn wirtualnych artykuł](backup-azure-vms.md). W przeciwnym razie odczytać, ten artykuł przeprowadzi Cię przez hello kroki tooprepare tooback Twojego środowiska zapasowej maszyny Wirtualnej platformy Azure.

##<a name="supported-operating-system-for-backup"></a>Obsługiwany system operacyjny do utworzenia kopii zapasowej
 * **Linux**: usługa Azure Backup obsługuje [dystrybucje zalecane dla platformy Azure](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) z wyjątkiem systemu operacyjnego Linux Core. _Innych Bring-Your-właścicielem — dystrybucje systemu Linux mogą również działać, dopóki agent maszyny Wirtualnej hello jest dostępne na maszynie wirtualnej hello i obsługę języka Python istnieje. Jednak firma Microsoft nie zatwierdza tych dystrybucji dla kopii zapasowej._
 * **Windows Server**: wersje starsze niż Windows Server 2008 R2 nie są obsługiwane.


## <a name="limitations-when-backing-up-and-restoring-a-vm"></a>Ograniczenia w przypadku tworzenia kopii zapasowej i przywracanie maszyny Wirtualnej
> [!NOTE]
> Platforma Azure ma dwa modele wdrażania związane z tworzeniem i pracą z zasobami: [Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md). Witaj Poniższa lista zawiera hello ograniczenia w przypadku wdrażania w klasycznym modelu hello.
>
>

* Tworzenie kopii zapasowych maszyn wirtualnych z więcej niż 16 dysków danych nie jest obsługiwane.
* Tworzenie kopii zapasowych maszyn wirtualnych z zastrzeżonego adresu IP i nie zdefiniowanych punktów końcowych nie jest obsługiwane.
* Dane kopii zapasowej nie zawiera tooVM dołączone dyski sieciowe zainstalowane.
* Zamiana istniejącej maszyny wirtualnej podczas przywracania nie jest obsługiwana. Najpierw usuń hello istniejącej maszyny wirtualnej i wszystkie skojarzone dyski, a następnie przywróć hello dane z kopii zapasowej.
* Region między kopii zapasowej i przywracania nie jest obsługiwana.
* Tworzenie kopii zapasowych maszyn wirtualnych za pomocą usługi Kopia zapasowa Azure hello jest obsługiwana we wszystkich regionach publicznej platformy Azure (zobacz hello [Lista kontrolna](https://azure.microsoft.com/regions/#services) obsługiwanych regionów). Jeśli obecnie jest obsługiwany region hello, którego szukasz, nie zostanie wyświetlony na liście rozwijanej hello podczas tworzenia magazynu.
* Tworzenie kopii zapasowych maszyn wirtualnych za pomocą usługi Kopia zapasowa Azure hello jest obsługiwana tylko dla wersji systemu operacyjnego wybierz:
* Przywracanie kontrolera domeny (DC) maszyny Wirtualnej, która jest częścią konfiguracji kontrolera domeny na wielu jest obsługiwane tylko za pomocą programu PowerShell. Przeczytaj więcej na temat [Przywracanie kontrolera domeny, kontrolera domeny na wielu](backup-azure-restore-vms.md#restoring-domain-controller-vms).
* Przywracanie maszyn wirtualnych, które mają następujące konfiguracje sieciowe specjalne hello jest obsługiwane tylko za pomocą programu PowerShell. Maszyny wirtualne utworzone za pomocą przepływu pracy przywracania hello w hello interfejsu użytkownika nie będą miały te konfiguracje sieci, po zakończeniu operacji przywracania hello. toolearn więcej, zobacz [przywracanie maszyn wirtualnych z konfiguracjami sieci specjalne](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations).
  * Maszyny wirtualne znajdujące się w konfiguracji usługi równoważenia obciążenia (wewnętrznych i zewnętrznych)
  * Maszyny wirtualne z wielu zastrzeżonych adresów IP
  * Maszyny wirtualne z wieloma kartami sieciowymi

## <a name="create-a-backup-vault-for-a-vm"></a>Utwórz magazyn kopii zapasowych dla maszyny Wirtualnej
Magazyn kopii zapasowych to jednostka, która przechowuje wszystkie hello kopie zapasowe i punkty odzyskiwania, które zostały utworzone w czasie. Witaj magazynu kopii zapasowych zawiera również hello zasad tworzenia kopii zapasowych, które mają być zastosowane toohello maszyn wirtualnych tworzona kopia zapasowa.

> [!IMPORTANT]
> Uruchamianie 2017 marca, można dłużej korzystać magazyny kopii zapasowych w klasycznym portalu toocreate hello. Istniejące magazyny kopii zapasowych nadal są obsługiwane i możliwe jest zbyt[Użyj magazyny kopii zapasowych programu Azure PowerShell toocreate](./backup-client-automation-classic.md#create-a-backup-vault). Jednak firma Microsoft zaleca się, że możesz utworzyć magazyny usług odzyskiwania dla wszystkich wdrożeń, ponieważ przyszłe ulepszenia zastosować Magazyny usług tooRecovery, tylko.


Ten obraz zawiera hello relacje między hello różnymi jednostkami kopia zapasowa Azure: ![kopia zapasowa Azure jednostki i relacje](./media/backup-azure-vms-prepare/vault-policy-vm.png)



## <a name="network-connectivity"></a>Połączenie sieciowe
W kolejności toomanage hello migawki maszyny Wirtualnej, zapasowy numer wewnętrzny hello musi mieć łączność toohello Azure publicznych adresów IP. Bez hello prawo łączność z Internetem, maszyny wirtualnej hello HTTP żądania limitu czasu i hello kopii zapasowej kończy się niepowodzeniem. Jeśli wdrożenie obowiązują ograniczenia dostępu w (za pośrednictwem sieciową grupę zabezpieczeń (NSG), na przykład), wybierz jedną z następujących opcji do prezentowania wyczyść ścieżki dla kopii zapasowej ruchu:

* [Zakresy IP centrum danych Azure hello dozwolonych](http://www.microsoft.com/en-us/download/details.aspx?id=41653) — zobacz artykuł hello instrukcje w sposób toowhitelist hello adresów IP.
* Wdrażanie serwera proxy HTTP dla routingu ruchu.

Podczas wybierania który toouse opcji, kompromisy hello należą do zakresu od możliwości zarządzania, kontrolę i kosztów.

| Opcja | Zalety | Wady |
| --- | --- | --- |
| Lista dozwolonych adresów IP, zakresów |Brak dodatkowych kosztów.<br><br>Do otwierania dostępu w grupy NSG, użyj hello <i>AzureNetworkSecurityRule zestaw</i> polecenia cmdlet. |Złożone toomanage jako hello wpływ zmiany zakresów adresów IP w czasie.<br><br>Zapewnia dostęp do całej toohello Azure, a nie tylko magazynu. |
| Serwer proxy HTTP |Dozwolone adresy URL kontrolę powitania serwera proxy za pośrednictwem hello magazynu. toosetup kontrolę w hello proxy https://\*.blob.core.windows.net/\* toobe białej musi wzorca adresu URL. toowhitelist hello tylko konto magazynu używane przez hello maszyny Wirtualnej, https://\<storageAccount\>.blob.core.windows.net/\* toobe białej musi wzorca adresu URL. <br>Pojedynczy punkt Internet tooVMs dostępu.<br>Nie podmiotu tooAzure zmiany adresu IP. |Dodatkowe koszty uruchomioną maszynę Wirtualną z hello oprogramowanie serwera proxy. |

### <a name="whitelist-hello-azure-datacenter-ip-ranges"></a>Zakresy IP centrum danych Azure hello listy dozwolonych adresów IP
toowhitelist hello zakresy IP centrum danych Azure, zobacz hello [witryny sieci Web Azure](http://www.microsoft.com/en-us/download/details.aspx?id=41653) szczegółowe informacje na temat zakresów IP hello i instrukcje.

### <a name="using-an-http-proxy-for-vm-backups"></a>Za pomocą serwera proxy HTTP dla kopii zapasowych maszyn wirtualnych
Podczas tworzenia kopii zapasowej maszyny Wirtualnej, zapasowy numer wewnętrzny hello na powitania maszyna wirtualna wysyła hello migawki zarządzania polecenia tooAzure magazynu przy użyciu interfejsu API protokołu HTTPS. Kierować ruchem zapasowy numer wewnętrzny hello za pośrednictwem serwera proxy hello HTTP, ponieważ jest jedynym składnikiem hello skonfigurowane dla toohello dostępu do publicznej sieci Internet.

> [!NOTE]
> Nie ma żadnych zalecenie hello proxy oprogramowania, które mają być używane. Upewnij się, że wybierz serwer proxy, który ma lepkości wychodzących i który jest zgodny z hello poniższe kroki konfiguracji. Upewnij się, że oprogramowanie innych firm nie należy modyfikować ustawienia serwera proxy hello
>
>

Hello przykład obraz poniżej przedstawia kroki konfiguracji trzy hello niezbędne toouse HTTP serwera proxy:

* Trasy wirtualna aplikacji, które powiązane cały ruch HTTP dla hello publicznej sieci Internet za pośrednictwem serwera Proxy maszyny Wirtualnej.
* Maszyna wirtualna serwera proxy zezwala na ruch przychodzący z maszyn wirtualnych w sieci wirtualnej hello.
* Witaj sieciowej grupy zabezpieczeń (NSG) o nazwie NF blokady musi zabezpieczeń reguły zezwalanie Internet ruch wychodzący z maszyny Wirtualnej serwera Proxy.

![Grupy NSG z diagram wdrożenia serwera proxy HTTP](./media/backup-azure-vms-prepare/nsg-with-http-proxy.png)

toouse HTTP serwera proxy toocommunicating toohello publicznej sieci Internet, wykonaj następujące kroki:

#### <a name="step-1-configure-outgoing-network-connections"></a>Krok 1. Konfigurowanie połączeń wychodzących sieci
###### <a name="for-windows-machines"></a>W przypadku komputerów z systemem Windows
Będzie to ustawienia konfiguracji serwera proxy dla lokalnego konta systemowego.

1. Pobierz [PsExec](https://technet.microsoft.com/sysinternals/bb897553)
2. Uruchom następujące polecenia z podwyższonym poziomem uprawnień wiersza

     ```
     psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"
     ```
     Otworzy się okno programu internet explorer.
3. Przejdź tooTools -> Opcje internetowe -> połączenia -> Ustawienia sieci LAN.
4. Sprawdź ustawienia serwera proxy dla konta System. Ustaw Proxy adresu IP i portu.
5. Zamknij program Internet Explorer.

Zostanie utworzenie konfiguracji serwera proxy dla komputera i będą używane dla każdego wychodzącego ruchu HTTP/HTTPS.

Jeśli skonfigurowano serwer proxy dla bieżącego konta użytkownika (nie lokalnego konta systemowego), użyj hello następujący skrypt tooapply ich tooSYSTEMACCOUNT:

```
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name DefaultConnectionSettings -Value $obj.DefaultConnectionSettings
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name SavedLegacySettings -Value $obj.SavedLegacySettings
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name ProxyEnable -Value $obj.ProxyEnable
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name Proxyserver -Value $obj.Proxyserver
```

> [!NOTE]
> Jeśli zauważysz "(407) uwierzytelniania serwera Proxy wymagane" w dzienniku serwera proxy, sprawdź, czy uwierzytelnianie jest poprawnie skonfigurowana.
>
>

###### <a name="for-linux-machines"></a>Dla maszyn z systemem Linux
Dodaj powitania po wierszu toohello ```/etc/environment``` pliku:

```
http_proxy=http://<proxy IP>:<proxy port>
```

Dodaj następujące wiersze toohello hello ```/etc/waagent.conf``` pliku:

```
HttpProxy.Host=<proxy IP>
HttpProxy.Port=<proxy port>
```

#### <a name="step-2-allow-incoming-connections-on-hello-proxy-server"></a>Krok 2. Zezwalaj na połączenia przychodzące na powitania serwera proxy:
1. Na powitania serwera proxy otwórz Zaporę systemu Windows. Witaj Najprostszym sposobem tooaccess hello zapory jest toosearch zapory systemu Windows z zabezpieczeniami zaawansowanymi.

    ![Otwórz hello zapory](./media/backup-azure-vms-prepare/firewall-01.png)
2. W oknie dialogowym zapory systemu Windows hello, kliknij prawym przyciskiem myszy **reguły ruchu przychodzącego** i kliknij przycisk **nową regułę...** .

    ![Utwórz nową regułę](./media/backup-azure-vms-prepare/firewall-02.png)
3. W hello **Kreatora nowej reguły przychodzącej**, wybierz hello **niestandardowy** opcję hello **typ reguły** i kliknij przycisk **dalej**.
4. Na powitania strony tooselect hello **Program**, wybierz **wszystkie programy** i kliknij przycisk **dalej**.
5. Na powitania **protokoły i porty** , wprowadź hello następujące informacje i kliknij przycisk **dalej**:

    ![Utwórz nową regułę](./media/backup-azure-vms-prepare/firewall-03.png)

   * Aby uzyskać *protokół typu* wybierz *TCP*
   * dla *portów lokalnych* wybierz *określonych portów*, w polu hello poniżej Określ hello ```<Proxy Port>``` który został skonfigurowany.
   * Aby uzyskać *port zdalny* wybierz *wszystkie porty*

     Hello pozostałej części hello kreatora kliknij wszystkie hello sposób toohello zakończenia i nadaj nazwę tej reguły.

#### <a name="step-3-add-an-exception-rule-toohello-nsg"></a>Krok 3. Dodaj wyjątek toohello reguły NSG:
W wierszu polecenia programu PowerShell systemu Azure wprowadź hello następujące polecenie:

Witaj następujące polecenie dodaje wyjątek toohello NSG. Ten wyjątek zezwala na ruch TCP z dowolnego portu na 10.0.0.5 tooany adresu internetowego na porcie 80 (HTTP) lub 443 (HTTPS). Jeśli potrzebujesz określonego portu w hello publicznej sieci Internet, można tooadd się upewnić, że port toohello ```-DestinationPortRange``` również.

```
Get-AzureNetworkSecurityGroup -Name "NSG-lockdown" |
Set-AzureNetworkSecurityRule -Name "allow-proxy " -Action Allow -Protocol TCP -Type Outbound -Priority 200 -SourceAddressPrefix "10.0.0.5/32" -SourcePortRange "*" -DestinationAddressPrefix Internet -DestinationPortRange "80-443"
```

*Upewnij się, Zastąp nazwy hello w przykładzie hello z wdrożeniem tooyour odpowiednie szczegóły hello.*

## <a name="vm-agent"></a>Agent maszyny Wirtualnej
Przed utworzeniem kopii zapasowej hello maszyny wirtualnej platformy Azure, należy upewnić się, że agent maszyny Wirtualnej Azure hello jest poprawnie zainstalowany na maszynie wirtualnej hello. Ponieważ hello agent maszyny Wirtualnej jest opcjonalnym składnikiem o hello czas hello maszyna wirtualna została utworzona, zapewnić tego pola wyboru hello hello agenta maszyny Wirtualnej jest zaznaczone, zanim zostanie zainicjowana hello maszyny wirtualnej.

### <a name="manual-installation-and-update"></a>Aktualizacja i Instalacja ręczna
agent maszyny Wirtualnej Hello jest już obecny na maszynach wirtualnych, które są tworzone na podstawie hello galerii Azure. Jednakże maszyn wirtualnych, które są migrowane z lokalnych centrów danych nie mieć zainstalowanego agenta maszyny Wirtualnej hello. Dla tych maszyn wirtualnych agent maszyny Wirtualnej hello musi toobe jawnie zainstalowany. Przeczytaj więcej na temat [instalowanie hello agenta maszyny Wirtualnej na istniejącej maszyny Wirtualnej](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx).

| **Operacja** | **Windows** | **Linux** |
| --- | --- | --- |
| Instalowanie agenta maszyny Wirtualnej hello |<li>Pobierz i zainstaluj hello [pliku MSI agenta](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Konieczne będzie instalacji hello toocomplete uprawnienia administratora. <li>[Aktualizuj właściwości maszyny Wirtualnej hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate, który hello agent jest zainstalowany. |<li> Zainstaluj najnowsze hello [agenta systemu Linux](https://github.com/Azure/WALinuxAgent) z usługi GitHub. Konieczne będzie instalacji hello toocomplete uprawnienia administratora. <li> [Aktualizuj właściwości maszyny Wirtualnej hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate, który hello agent jest zainstalowany. |
| Aktualizowanie hello agenta maszyny Wirtualnej |Trwa aktualizowanie agenta maszyny Wirtualnej hello jest tak proste, jak ponowne zainstalowanie hello [plików binarnych agenta maszyny Wirtualnej](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br><br>Upewnij się, że żadna operacja tworzenia kopii zapasowej działa podczas aktualizowania hello agenta maszyny Wirtualnej. |Wykonaj instrukcje hello [aktualizowanie hello agenta maszyny Wirtualnej systemu Linux ](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). <br><br>Upewnij się, że żadna operacja tworzenia kopii zapasowej działa podczas aktualizowania hello agenta maszyny Wirtualnej. |
| Sprawdzanie poprawności instalacji agenta hello maszyny Wirtualnej |<li>Przejdź toohello *C:\WindowsAzure\Packages* folderu w hello maszyny Wirtualnej platformy Azure. <li>Powinien znajdować się plik WaAppAgent.exe hello jest obecny.<li> Kliknij prawym przyciskiem myszy plik hello znajduje się zbyt**właściwości**, a następnie wybierz hello **szczegóły** kartę hello wersji produktu pole powinno być 2.6.1198.718 lub nowszej. |Nie dotyczy |

Dowiedz się więcej o hello [agenta maszyny Wirtualnej](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) i [jak tooinstall go](https://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/).

### <a name="backup-extension"></a>Rozszerzenie kopii zapasowej
tooback hello maszyny wirtualnej, hello usługi Kopia zapasowa Azure instaluje agenta maszyny Wirtualnej toohello rozszerzenia. Witaj usługi Kopia zapasowa Azure bezproblemowo uaktualniania i poprawek hello zapasowy numer wewnętrzny bez interwencji użytkownika dodatkowe.

zapasowy numer wewnętrzny Hello jest zainstalowany, jeśli hello maszyna wirtualna jest uruchomiona. Uruchomionych maszynach wirtualnych zapewnia także największe prawdopodobieństwo hello pobieranie punktów odzyskiwania zapewniających spójność aplikacji. Jednak hello kopia zapasowa Azure usługa będzie nadal tooback się hello maszyny Wirtualnej — nawet jeśli jest wyłączona, a rozszerzenie hello nie może być zainstalowana (alias w trybie Offline maszyny Wirtualnej). W takim przypadku hello punkt odzyskiwania będzie *awaria spójne* zgodnie z powyższym opisem.

## <a name="questions"></a>Pytania?
Jeśli masz pytania lub w przypadku dowolnej funkcji, które chcesz toosee uwzględnione, [Prześlij nam opinię](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy przygotowania środowiska do tworzenia kopii zapasowej maszyny Wirtualnej, następnym krokiem logicznej jest toocreate kopii zapasowej. Witaj planowania artykuł zawiera bardziej szczegółowe informacje o tworzeniu kopii zapasowych maszyn wirtualnych.

* [Tworzenie kopii zapasowych maszyn wirtualnych](backup-azure-vms.md)
* [Zaplanuj infrastrukturę kopii zapasowej maszyny Wirtualnej](backup-azure-vms-introduction.md)
* [Zarządzanie kopii zapasowych maszyn wirtualnych](backup-azure-manage-vms.md)
