---
title: "aaaInstall lasu usługi Active Directory w sieci wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Samouczek, który objaśnia, jak toocreate nowej usługi Active Directory lasu na maszynie wirtualnej (VM) w sieci wirtualnej platformy Azure."
services: active-directory, virtual-network
keywords: "Maszyna wirtualna usługi Active directory, instalacja lasu usługi active directory, filmy wideo z usługi azure active directory "
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
tags: 
ms.assetid: eb7170d0-266a-4caa-adce-1855589d65d1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/06/2017
ms.author: joflore
ms.openlocfilehash: 08121130777cc3c206d7b5b38974982884dca1c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-new-active-directory-forest-on-an-azure-virtual-network"></a>Instalowanie nowego lasu usługi Active Directory w sieci wirtualnej platformy Azure
W tym temacie przedstawiono sposób toocreate nowe Windows Server Active Directory środowiska w sieci wirtualnej platformy Azure na maszynie wirtualnej (VM) na [sieci wirtualnej platformy Azure](../virtual-network/virtual-networks-overview.md). W takim przypadku hello sieci wirtualnej platformy Azure nie jest połączony tooan sieci lokalnej.

Być może zainteresuje te tematy pokrewne:

* Film przedstawiający tych kroków, zobacz [jak tooinstall nowej usługi Active Directory lasu w sieci wirtualnej platformy Azure](http://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/How-to-install-a-new-Active-Directory-forest-on-an-Azure-virtual-network)
* Można opcjonalnie [skonfigurowania sieci VPN lokacja lokacja](../vpn-gateway/vpn-gateway-site-to-site-create.md) , a następnie zainstalować nowy las lub rozszerzyć tooan lasu lokalnej sieci wirtualnej platformy Azure. Te kroki opisane w artykule [Instalowanie repliki kontrolera domeny Active Directory w sieci wirtualnej platformy Azure](active-directory-install-replica-active-directory-domain-controller.md).
* Aby uzyskać ogólne wskazówki dotyczące instalowania usług domenowych w usłudze Active Directory (AD DS) w sieci wirtualnej platformy Azure, zobacz [wskazówki dotyczące wdrażania systemu Windows Server Active Directory na maszynach wirtualnych Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx).

## <a name="scenario-diagram"></a>Diagram scenariusza
W tym scenariuszu użytkownicy zewnętrzni muszą aplikacje tooaccess, które działają na serwerach przyłączonych do domeny. Witaj maszyn wirtualnych serwerów aplikacji hello i hello maszyn wirtualnych kontrolerów domeny są instalowane, zainstalować ich w usłudze w chmurze w sieci wirtualnej platformy Azure. Są one również uwzględniona w obrębie zbiór dostępności dla ulepszone odporność na uszkodzenia.

![Las usługi Active Directory na maszyny wirtualne w sieci wirtualnej Azure ][1] 7

## <a name="how-does-this-differ-from-on-premises"></a>Jak jest to różnica między lokalnymi?
Nie jest znacznie różnica między instalowania kontrolera domeny na platformie Azure lub lokalnie. główne różnice Hello są wyświetlane w hello w poniższej tabeli.

| tooconfigure... | Lokalnie | Sieć wirtualna Azure |
| --- | --- | --- |
| **Adres IP dla kontrolera domeny hello** |Przypisz statyczny adres IP na właściwości karty sieciowej hello |Uruchom tooassign polecenia cmdlet Set-AzureStaticVNetIP hello statycznego adresu IP |
| **Program rozpoznawania nazw DNS klienta** |Ustaw preferowany i alternatywny serwer DNS adresu serwera na powitania właściwości karty sieciowej elementów członkowskich domeny |Ustaw adres serwera DNS na powitania hello sieci wirtualnej właściwości |
| **Magazyn baz danych w usłudze Active Directory** |Opcjonalnie zmienić domyślną lokalizację przechowywania hello z C:\ |Należy toochange domyślną lokalizację przechowywania z C:\ |

## <a name="create-an-azure-virtual-network"></a>Tworzenie sieci wirtualnej platformy Azure
1. Zaloguj się toohello klasycznego portalu Azure.
2. Tworzenie sieci wirtualnej. Kliknij przycisk **sieci** > **utworzyć sieć wirtualną**. Użycie w tabeli toocomplete hello kreatora po hello hello wartości.

   | Na tej stronie kreatora... | Określ te wartości |
   | --- | --- |
   |  **Szczegóły sieci wirtualnej** |<p>Nazwa: Wprowadź nazwę sieci wirtualnej</p><p>Region: Wybierz region najbliższy hello</p> |
   |  **DNS i sieci VPN** |<p>Pozostaw puste serwera DNS</p><p>Nie należy wybierać opcji albo sieci VPN</p> |
   |  **Przestrzeniami adresów sieci wirtualnej** |<p>Nazwa podsieci: Wprowadź nazwę dla podsieci</p><p>Rozpoczynanie IP: <b>10.0.0.0</b></p><p>CIDR: <b>PREFIKSIE/24 (256)</b></p> |

## <a name="create-vms-toorun-hello-domain-controller-and-dns-server-roles"></a>Tworzenie kontrolera domeny hello toorun maszyn wirtualnych i ról serwera DNS
Powtórz hello następujące kroki toocreate maszyn wirtualnych toohost hello DC roli zgodnie z potrzebami. Należy wdrożyć co najmniej dwa kontrolery domeny tooprovide odporność na uszkodzenia i nadmiarowość wirtualnego. Jeśli hello sieci wirtualnej platformy Azure zawiera co najmniej dwa kontrolery domeny, podobnie skonfigurowanych (to, że są one zarówno wykazów globalnych, uruchom serwer DNS, i nie zawiera żadnych ról FSMO i tak dalej) umieścić hello maszyn wirtualnych te kontrolery domeny w zbiór dostępności dla ulepszone odporność na uszkodzenia.

toocreate hello maszyn wirtualnych przy użyciu programu Windows PowerShell zamiast hello interfejsu użytkownika, zobacz [toocreate Użyj programu PowerShell Azure i wstępnie skonfigurować maszyn wirtualnych z systemem Windows](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

1. W portalu klasycznym powitania kliknij **nowy** > **obliczeniowe** > **maszyny wirtualnej** > **z galerii**. Użyj Kreatora hello toocomplete wartości po hello. Zaakceptowanie hello domyślna wartość to ustawienie, chyba inną wartość jest sugerowane lub wymagane.

   | Na tej stronie kreatora... | Określ te wartości |
   | --- | --- |
   |  **Wybierz obraz** |Windows Server 2012 R2 Datacenter |
   |  **Konfiguracja maszyny wirtualnej** |<p>Nazwa maszyny wirtualnej: Wpisz nazwy o pojedynczej etykiecie (na przykład AzureDC1).</p><p>Nowa nazwa użytkownika: Wpisz nazwę hello użytkownika. Ten użytkownik będzie członkiem lokalnej grupy administratorów hello na powitania maszyny Wirtualnej. Konieczne będzie toosign tej nazwy w toohello maszyny Wirtualnej na powitania po raz pierwszy. wbudowane konto Hello o nazwie Administrator nie będzie działać.</p><p>Nowe hasło/Potwierdź: Wpisz hasło</p> |
   |  **Konfiguracja maszyny wirtualnej** |<p>Usługi w chmurze: Wybierz <b>Utwórz nową usługę w chmurze</b> dla hello pierwsza maszyna wirtualna i zaznacz, że sama nazwa usługi chmury, podczas tworzenia więcej maszyn wirtualnych, które będą obsługiwać hello roli kontrolera domeny.</p><p>Nazwa DNS usługi w chmurze: Określ globalnie unikatowa nazwa</p><p>Region/grupy koligacji/sieci wirtualnej: Określ nazwę sieci wirtualnej hello (na przykład WestUSVNet).</p><p>Konto magazynu: Wybierz <b>użyć konta magazynu automatycznie generowanych</b> dla hello pierwsza maszyna wirtualna, a następnie wybierz, czy nazwa tego samego konta magazynu podczas tworzenia więcej maszyn wirtualnych, które będą obsługiwać hello roli kontrolera domeny.</p><p>Zestaw dostępności: Wybierz <b>tworzenia zestawu dostępności</b>.</p><p>Nazwa zbioru dostępności: typ nazwę dostępności powitania po utworzeniu hello pierwsza maszyna wirtualna, a następnie wybierz, same nazwy podczas tworzenia więcej maszyn wirtualnych.</p> |
   |  **Konfiguracja maszyny wirtualnej** |<p>Wybierz <b>hello Zainstaluj agenta maszyny Wirtualnej</b> oraz innych rozszerzeń należy.</p> |
2. Dołącz tooeach dysku maszyny Wirtualnej, który zostanie uruchomiony w roli serwera hello kontrolera domeny. dodatkowy dysk Hello jest wymagane toostore hello AD w bazie danych, dzienników i folderu SYSVOL. Określ rozmiar dysku hello (np. 10 GB) i pozostawić hello **hosta pamięci podręcznej preferencji** ustawić także**Brak**. Witaj kroki opisane w artykule [jak tooAttach tooa dysku danych maszyny wirtualnej systemu Windows](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. Po pierwszym zalogowaniu toohello maszyny Wirtualnej, należy otworzyć **Menedżera serwera** > **usług plików i magazynowania** toocreate wolumin na dysku w systemie plików NTFS.
4. Zarezerwuj statyczny adres IP dla maszyn wirtualnych, które uruchomi hello roli kontrolera domeny. tooreserve statyczny adres IP, Pobierz hello Instalatora platformy sieci Web firmy Microsoft i [zainstalować program Azure PowerShell](/powershell/azure/overview) i uruchom polecenie cmdlet hello AzureStaticVNetIP zestawu. Na przykład:

    `Get-AzureVM -ServiceName AzureDC1 -Name AzureDC1 | Set-AzureStaticVNetIP -IPAddress 10.0.0.4 | Update-AzureVM`

Aby uzyskać więcej informacji na temat ustawiania statycznego adresu IP, zobacz [skonfigurować statyczny adres IP wewnętrznego dla maszyny Wirtualnej,](../virtual-network/virtual-networks-reserved-private-ip.md).

## <a name="install-windows-server-active-directory"></a>Zainstaluj usługi Active Directory systemu Windows Server
Użyj zbyt hello tej samej procedury[zainstalowania usług AD DS](https://technet.microsoft.com/library/jj574166.aspx) Używanie lokalnego (to znaczy służy hello interfejsu użytkownika, pliku odpowiedzi lub środowiska Windows PowerShell). Należy tooinstall poświadczenia administratora tooprovide nowego lasu. lokalizację hello toospecify hello bazy danych usługi Active Directory, dzienników i folderu SYSVOL, zmienić domyślną lokalizację przechowywania hello z hello systemu operacyjnego toohello dodatkowe dane dysku że dołączony toohello maszyny Wirtualnej.

Po zakończeniu hello instalacji kontrolera domeny, ponownie nawiąż połączenie toohello maszyny Wirtualnej i zaloguj się na toohello kontrolera domeny. Pamiętaj poświadczenia domeny toospecify.

## <a name="reset-hello-dns-server-for-hello-azure-virtual-network"></a>Resetuj powitania serwera DNS dla hello sieci wirtualnej platformy Azure
1. Zresetować ustawienie usługi przesyłania dalej DNS hello na powitania nowego serwera DNS kontrolera domeny.
   1. W Menedżerze serwera kliknij **narzędzia** > **DNS**.
   2. W **Menedżera DNS**, kliknij prawym przyciskiem myszy nazwę hello powitania serwera DNS i kliknij przycisk **właściwości**.
   3. Na powitania **usług przesyłania dalej** , kliknij adres IP hello hello usługi przesyłania dalej i kliknij **Edytuj**.  Wybierz adres IP hello i kliknij przycisk **usunąć**.
   4. Kliknij przycisk **OK** tooclose hello edytora i **Ok** ponownie tooclose hello właściwości: serwer DNS.
2. Aktualizacja hello ustawienia serwera DNS dla sieci wirtualnej hello.
   1. Kliknij przycisk **sieci wirtualnych** > kliknij dwukrotnie hello sieci wirtualnej utworzony > **Konfiguruj** > **serwerów DNS**, wpisz nazwę hello i hello DIP jednego z Witaj maszyn wirtualnych działa rola serwera DNS kontrolera domeny hello i kliknij przycisk **zapisać**.
   2. Wybierz hello maszyny Wirtualnej, a następnie kliknij przycisk **Uruchom ponownie** tootrigger hello wirtualna tooconfigure DNS ustawień programu rozpoznawania nazw adresu IP hello hello nowego serwera DNS.

## <a name="create-vms-for-domain-members"></a>Tworzenie maszyn wirtualnych dla członków domeny
1. Powtórz następujące kroki toocreate maszyn wirtualnych toorun jako serwery aplikacji hello. Zaakceptowanie hello domyślna wartość to ustawienie, chyba inną wartość jest sugerowane lub wymagane.

   | Na tej stronie kreatora... | Określ te wartości |
   | --- | --- |
   |  **Wybierz obraz** |Windows Server 2012 R2 Datacenter |
   |  **Konfiguracja maszyny wirtualnej** |<p>Nazwa maszyny wirtualnej: Wpisz nazwy o pojedynczej etykiecie (na przykład AppServer1).</p><p>Nowa nazwa użytkownika: Wpisz nazwę hello użytkownika. Ten użytkownik będzie członkiem lokalnej grupy administratorów hello na powitania maszyny Wirtualnej. Konieczne będzie toosign tej nazwy w toohello maszyny Wirtualnej na powitania po raz pierwszy. wbudowane konto Hello o nazwie Administrator nie będzie działać.</p><p>Nowe hasło/Potwierdź: Wpisz hasło</p> |
   |  **Konfiguracja maszyny wirtualnej** |<p>Usługi w chmurze: Wybierz **Utwórz nową usługę w chmurze** dla hello pierwsza maszyna wirtualna i wybierz podczas tworzenia więcej maszyn wirtualnych, które same chmury nazwa usługi zostanie hosta aplikacji hello.</p><p>Nazwa DNS usługi w chmurze: Określ globalnie unikatowa nazwa</p><p>Region/grupy koligacji/sieci wirtualnej: Określ nazwę sieci wirtualnej hello (na przykład WestUSVNet).</p><p>Konto magazynu: Wybierz **użyć konta magazynu automatycznie generowanych** dla hello pierwsza maszyna wirtualna, a następnie wybierz, czy nazwa tego samego konta magazynu podczas tworzenia maszyn wirtualnych więcej będzie hostem aplikacji hello.</p><p>Zestaw dostępności: Wybierz **tworzenia zestawu dostępności**.</p><p>Nazwa zbioru dostępności: typ nazwę dostępności powitania po utworzeniu hello pierwsza maszyna wirtualna, a następnie wybierz, same nazwy podczas tworzenia więcej maszyn wirtualnych.</p> |
   |  **Konfiguracja maszyny wirtualnej** |<p>Wybierz <b>hello Zainstaluj agenta maszyny Wirtualnej</b> oraz innych rozszerzeń należy.</p> |
2. Po udostępnieniu każdej maszyny Wirtualnej, zaloguj się i przyłączyć go toohello domeny. W **Menedżera serwera**, kliknij przycisk **lokalnego serwera** > **grupy roboczej** > **zmian...** a następnie wybierz **domeny** i typ hello nazwy domeny lokalnej. Podaj poświadczenia użytkownika domeny i uruchom ponownie przyłączenie do domeny hello hello wirtualna toocomplete.

toocreate hello maszyn wirtualnych przy użyciu programu Windows PowerShell zamiast hello interfejsu użytkownika, zobacz [toocreate Użyj programu PowerShell Azure i wstępnie skonfigurować maszyn wirtualnych z systemem Windows](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Aby uzyskać więcej informacji o korzystaniu z programu Windows PowerShell, zobacz [wprowadzenie do poleceń cmdlet Azure](/powershell/azure/overview) i [dokumentacji poleceń Cmdlet Azure](/powershell/azure/get-started-azureps).

## <a name="see-also"></a>Zobacz też
* [Jak tooinstall nowej usługi Active Directory lasu w sieci wirtualnej platformy Azure](http://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/How-to-install-a-new-Active-Directory-forest-on-an-Azure-virtual-network)
* [Wskazówki dotyczące wdrażania systemu Windows serwer usługi Active Directory na maszynach wirtualnych Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx)
* [Konfigurowanie sieci VPN lokacja lokacja](../vpn-gateway/vpn-gateway-site-to-site-create.md)
* [Instalowanie repliki kontrolera domeny Active Directory w sieci wirtualnej platformy Azure](active-directory-install-replica-active-directory-domain-controller.md)
* [Microsoft Azure IaaS specjalista IT: (01) maszyny wirtualnej podstawy](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure IaaS specjalista IT: (05) tworzenie sieci wirtualnych i łączności między lokalizacjami](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)
* [Omówienie sieci wirtualnej](../virtual-network/virtual-networks-overview.md)
* [Jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview)
* [Azure PowerShell](/powershell/azure/overview)
* [Dokumentacja poleceń cmdlet platformy Azure](/powershell/azure/get-started-azureps)
* [Ustaw adres statyczny adres IP maszyny Wirtualnej platformy Azure](http://windowsitpro.com/windows-azure/set-azure-vm-static-ip-address)
* [Jak tooassign tooAzure statyczny adres IP maszyny Wirtualnej](http://www.bhargavs.com/index.php/2014/03/13/how-to-assign-static-ip-to-azure-vm/)
* [Instalowanie nowego lasu usługi Active Directory](https://technet.microsoft.com/library/jj574166.aspx)
* [Wprowadzenie tooActive wirtualizacja usług domenowych Directory (AD DS) (poziom 100)](https://technet.microsoft.com/library/hh831734.aspx)

<!--Image references-->
[1]: ./media/active-directory-new-forest-virtual-machine/AD_Forest.png
