---
title: "aaaInstall repliki kontrolera domeny usługi Active Directory na platformie Azure | Dokumentacja firmy Microsoft"
description: "Samouczek, który objaśnia, jak tooinstall kontrolera domeny z lokalnej usługi Active Directory lasu na maszynie wirtualnej platformy Azure."
services: virtual-network
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 8c9ebf1b-289a-4dd6-9567-a946450005c0
ms.service: virtual-network
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 74876fce2ca2a29f02c2828f9b3a21227248233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-replica-active-directory-domain-controller-in-an-azure-virtual-network"></a>Instalowanie repliki kontrolera domeny usługi Active Directory w sieci wirtualnej platformy Azure
W tym temacie przedstawiono sposób tooinstall dodatkowe kontrolery domeny (znanej także jako replik kontrolerów domeny) do domeny usługi Active Directory lokalnego na maszynach wirtualnych Azure (maszyny wirtualne) w sieci wirtualnej platformy Azure.

> [!IMPORTANT]
> Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule.

Być może zainteresuje te tematy pokrewne:

* Można opcjonalnie zainstalować nowy las usługi Active Directory w sieci wirtualnej platformy Azure. Te kroki opisane w artykule [zainstalować nowy las usługi Active Directory w sieci wirtualnej platformy Azure](active-directory-new-forest-virtual-machine.md).
* Aby uzyskać ogólne wskazówki dotyczące instalowania usług domenowych w usłudze Active Directory (AD DS) w sieci wirtualnej platformy Azure, zobacz [wskazówki dotyczące wdrażania systemu Windows Server Active Directory na maszynach wirtualnych Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx).

## <a name="scenario-diagram"></a>Diagram scenariusza
W tym scenariuszu użytkownicy zewnętrzni muszą aplikacje tooaccess, które działają na serwerach przyłączonych do domeny. Witaj maszyn wirtualnych, które uruchomić serwerów aplikacji hello i hello replik kontrolerów domeny są zainstalowane w sieci wirtualnej platformy Azure. Witaj sieci wirtualnej może być sieci lokalnej podłączonej toohello przez [sieci VPN typu lokacja lokacja](../vpn-gateway/vpn-gateway-site-to-site-create.md) połączenia, jak pokazano poniżej hello diagramu lub użyć [ExpressRoute](../expressroute/expressroute-locations-providers.md) szybsze połączenia.

serwery aplikacji Hello i hello kontrolery domeny są wdrażane w ramach usługi w chmurze oddzielnych toodistribute obliczeniowe przetwarzania i poziomu [zestawów dostępności](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ulepszone odporności na uszkodzenia.
kontrolery domeny Hello replikować ze sobą i z kontrolerów domeny lokalnej za pomocą replikacji usługi Active Directory. Nie są konieczne żadne narzędzia synchronizacji.

![Diagram sieci wirtualnej platformy Azure pf repliki kontrolera domeny usługi Active Directory][1]

## <a name="create-an-active-directory-site-for-hello-azure-virtual-network"></a>Tworzenie lokacji usługi Active Directory dla hello sieci wirtualnej platformy Azure
Należy dobrze toocreate lokacji w usłudze Active Directory, reprezentujący hello sieci region odpowiedniego toohello sieci wirtualnej. Czy pozwala zoptymalizować uwierzytelniania, replikacji i innych operacji lokalizacji kontrolera domeny. Hello poniższych krokach opisano sposób toocreate lokacji i w tle więcej, zobacz [Dodawanie nowej lokacji](https://technet.microsoft.com/library/cc781496.aspx).

1. Otwórz Lokacje i usługi Active Directory: **Menedżera serwera** > **narzędzia** > **Lokacje i usługi Active Directory**.
2. Tworzenie witryny toorepresent hello regionu, w którym utworzono sieci wirtualnej platformy Azure: kliknij **witryny** > **akcji** > **nowej lokacji** > typu Nazwa Hello hello nowej lokacji, takich jak Azure nam zachodnie > Wybierz link lokacji > **OK**.
3. Utwórz podsieć i skojarzyć z hello nowej lokacji: kliknij dwukrotnie **witryny** > kliknij prawym przyciskiem myszy **podsieci** > **nową podsieć** > wpisz zakres adresów IP hello Witaj sieci wirtualnej (np. 10.1.0.0/16 na diagramie scenariusz hello) > Wybierz hello nową witrynę Azure > **OK**.

## <a name="create-an-azure-virtual-network"></a>Tworzenie sieci wirtualnej platformy Azure
1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com), kliknij przycisk **nowy** > **usług sieciowych** > **sieci wirtualnej**  >  **Utwórz niestandardowy** i użyj hello następujące wartości toocomplete hello kreatora.

   | Na tej stronie kreatora... | Określ te wartości |
   | --- | --- |
   |  **Szczegóły sieci wirtualnej** |<p>Nazwa: Nazwa hello sieci wirtualnej, takie jak WestUSVNet.</p><p>Region: Wybierz region najbliższy hello.</p> |
   |  **Połączenie usługi DNS i sieci VPN** |<p>Serwery DNS: Określ nazwę hello i adres IP co najmniej jeden lokalnych serwerów DNS.</p><p>Połączenie: Wybierz **skonfigurowania sieci VPN lokacja lokacja**.</p><p>Sieć lokalna: Określ nowe sieci lokalnej.</p><p>Jeśli korzystasz z usługi ExpressRoute zamiast sieci VPN, zobacz [skonfigurować połączenie ExpressRoute za pośrednictwem dostawcy usług Exchange](../expressroute/expressroute-locations-providers.md).</p> |
   |  **Połączenie lokacja lokacja** |<p>Nazwa: Nazwa hello sieci lokalnej.</p><p>Adres IP urządzenia sieci VPN: Określ publiczny adres IP hello hello urządzenia, które będą łączyć toohello sieci wirtualnej. Nie można zlokalizować urządzenia sieci VPN Hello za urządzeniem NAT</p><p>Adres: Określ hello zakresów adresów w sieci lokalnej (na przykład 192.168.0.0/16 hello scenariusz diagramie).</p> |
   |  **Przestrzeniami adresów sieci wirtualnej** |<p>Przestrzeń adresowa: Określ zakres adresów IP powitania dla maszyn wirtualnych, które mają toorun w hello sieci wirtualnej platformy Azure (np. 10.1.0.0/16 hello scenariusz diagramie). Ten zakres adresów nie może nakładać się z zakresami adresów hello hello sieci lokalnej.</p><p>Podsieci: Określ nazwę i adres dla podsieci dla serwerów aplikacji hello (np. serwera sieci Web, 10.1.1.0/24) oraz hello kontrolerów domeny (np. wewnętrznej bazy danych, 10.1.2.0/24).</p><p>Kliknij przycisk **Dodaj podsieć bramy**.</p> |
2. Następnie należy skonfigurować toocreate bramy sieci wirtualnej hello bezpiecznego połączenia sieci VPN typu lokacja lokacja. Zobacz [należy skonfigurować bramę sieci wirtualnej](../vpn-gateway/vpn-gateway-configure-vpn-gateway-mp.md) hello instrukcje.
3. Utwórz połączenie sieci VPN lokacja lokacja hello między hello nową sieć wirtualną i lokalnego urządzenia sieci VPN. Zobacz [należy skonfigurować bramę sieci wirtualnej](../vpn-gateway/vpn-gateway-configure-vpn-gateway-mp.md) hello instrukcje.

## <a name="create-azure-vms-for-hello-dc-roles"></a>Tworzenie maszyn wirtualnych platformy Azure dla hello ról kontrolera domeny
Powtórz hello następujące kroki toocreate maszyn wirtualnych toohost hello DC roli zgodnie z potrzebami. Należy wdrożyć co najmniej dwa kontrolery domeny tooprovide odporność na uszkodzenia i nadmiarowość wirtualnego. Jeśli hello sieci wirtualnej platformy Azure zawiera co najmniej dwa kontrolery domeny, podobnie skonfigurowanych (to, że są one zarówno wykazów globalnych, uruchom serwer DNS, i nie zawiera żadnych ról FSMO i tak dalej) umieścić hello maszyn wirtualnych te kontrolery domeny w zbiór dostępności dla ulepszone odporność na uszkodzenia.
toocreate hello maszyn wirtualnych przy użyciu programu Windows PowerShell zamiast hello interfejsu użytkownika, zobacz [toocreate Użyj programu PowerShell Azure i wstępnie skonfigurować maszyn wirtualnych z systemem Windows](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com), kliknij przycisk **nowy** > **obliczeniowe** > **maszyny wirtualnej**  >  **z galerii**. Użyj Kreatora hello toocomplete wartości po hello. Zaakceptowanie hello domyślna wartość to ustawienie, chyba inną wartość jest sugerowane lub wymagane.

   | Na tej stronie kreatora... | Określ te wartości |
   | --- | --- |
   |  **Wybierz obraz** |Windows Server 2012 R2 Datacenter |
   |  **Konfiguracja maszyny wirtualnej** |<p>Nazwa maszyny wirtualnej: Wpisz nazwy o pojedynczej etykiecie (na przykład AzureDC1).</p><p>Nowa nazwa użytkownika: Wpisz nazwę hello użytkownika. Ten użytkownik będzie członkiem lokalnej grupy administratorów hello na powitania maszyny Wirtualnej. Konieczne będzie toosign tej nazwy w toohello maszyny Wirtualnej na powitania po raz pierwszy. wbudowane konto Hello o nazwie Administrator nie będzie działać.</p><p>Nowe hasło/Potwierdź: Wpisz hasło</p> |
   |  **Konfiguracja maszyny wirtualnej** |<p>Usługi w chmurze: Wybierz <b>Utwórz nową usługę w chmurze</b> dla hello pierwsza maszyna wirtualna i zaznacz, że sama nazwa usługi chmury, podczas tworzenia więcej maszyn wirtualnych, które będą obsługiwać hello roli kontrolera domeny.</p><p>Nazwa DNS usługi w chmurze: Określ globalnie unikatowa nazwa</p><p>Region/grupy koligacji/sieci wirtualnej: Określ nazwę sieci wirtualnej hello (na przykład WestUSVNet).</p><p>Konto magazynu: Wybierz <b>użyć konta magazynu automatycznie generowanych</b> dla hello pierwsza maszyna wirtualna, a następnie wybierz, czy nazwa tego samego konta magazynu podczas tworzenia więcej maszyn wirtualnych, które będą obsługiwać hello roli kontrolera domeny.</p><p>Zestaw dostępności: Wybierz <b>tworzenia zestawu dostępności</b>.</p><p>Nazwa zbioru dostępności: typ nazwę dostępności powitania po utworzeniu hello pierwsza maszyna wirtualna, a następnie wybierz, same nazwy podczas tworzenia więcej maszyn wirtualnych.</p> |
   |  **Konfiguracja maszyny wirtualnej** |<p>Wybierz <b>hello Zainstaluj agenta maszyny Wirtualnej</b> oraz innych rozszerzeń należy.</p> |
2. Dołącz tooeach dysku maszyny Wirtualnej, który zostanie uruchomiony w roli serwera hello kontrolera domeny. dodatkowy dysk Hello jest wymagane toostore hello AD w bazie danych, dzienników i folderu SYSVOL. Określ rozmiar dysku hello (np. 10 GB) i pozostawić hello **hosta pamięci podręcznej preferencji** ustawić także**Brak**. Witaj kroki opisane w artykule [jak tooAttach tooa dysku danych maszyny wirtualnej systemu Windows](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. Po pierwszym zalogowaniu toohello maszyny Wirtualnej, należy otworzyć **Menedżera serwera** > **usług plików i magazynowania** toocreate wolumin na dysku w systemie plików NTFS.
4. Zarezerwuj statyczny adres IP dla maszyn wirtualnych, które uruchomi hello roli kontrolera domeny. tooreserve statyczny adres IP, Pobierz hello Instalatora platformy sieci Web firmy Microsoft i [zainstalować program Azure PowerShell](/powershell/azure/overview) i uruchom polecenie cmdlet hello AzureStaticVNetIP zestawu. Na przykład:

    "AzureDC1 - ServiceName get AzureVM-Name AzureDC1 | Zestaw AzureStaticVNetIP - IPAddress 10.0.0.4 | AzureVM aktualizacji

Aby uzyskać więcej informacji na temat ustawiania statycznego adresu IP, zobacz [skonfigurować statyczny adres IP wewnętrznego dla maszyny Wirtualnej,](../virtual-network/virtual-networks-reserved-private-ip.md).

## <a name="install-ad-ds-on-azure-vms"></a>Instalowanie usług AD DS na maszynach wirtualnych Azure
Zaloguj się tooa maszyny Wirtualnej i sprawdź, czy istnieje połączenie między hello site-to-site VPN lub ExpressRoute połączenia tooresources w sieci lokalnej. Następnie należy zainstalować usługi AD DS na powitania maszynach wirtualnych platformy Azure. Można użyć tego samego procesu, użyj tooinstall dodatkowego kontrolera domeny w sieci lokalnej (interfejsu użytkownika, środowiska Windows PowerShell lub pliku odpowiedzi). Jak zainstalować usługi AD DS, upewnij się, że Określ hello nowego woluminu do lokalizacji hello hello AD bazy danych, dzienników i folderu SYSVOL. Jeśli potrzebujesz odświeżacz w instalacji usług AD DS, zobacz [Instalowanie usług Active Directory domeny (poziom 100)](https://technet.microsoft.com/library/hh472162.aspx) lub [instalacji kontrolera domeny repliki systemu Windows Server 2012 w istniejącej domenie (poziom 200)](https://technet.microsoft.com/library/jj574134.aspx).

## <a name="reconfigure-dns-server-for-hello-virtual-network"></a>Ponownie skonfiguruj serwer DNS dla sieci wirtualnej hello
1. W hello [portalu Azure](https://portal.azure.com), w hello **wyszukiwania zasobów** wprowadź *sieci wirtualnych*, następnie kliknij przycisk **sieci wirtualnych (klasyczne)** w Witaj wyników wyszukiwania. Kliknij nazwę hello hello sieci wirtualnej, a następnie [ponownie skonfigurować hello adresów IP serwerów DNS dla sieci wirtualnej](../virtual-network/virtual-network-manage-network.md#dns-servers) toouse hello statyczne adresy IP przypisane toohello replik kontrolerów domeny, zamiast adresów IP hello lokalnej usługi DNS serwery.
2. tooensure, że wszystkie repliki hello maszyn wirtualnych kontrolera domeny w sieci wirtualnej hello skonfigurowano toouse serwerów DNS w sieci wirtualnej hello, kliknij przycisk **maszyn wirtualnych**, kliknij hello kolumnę stan każdej maszyny wirtualnej, a następnie kliknij przycisk **ponownego uruchomienia** . Poczekaj, aż hello maszyny Wirtualnej zawiera **systemem** stanu przed podjęciem próby toosign do niego.

## <a name="create-vms-for-application-servers"></a>Tworzenie maszyn wirtualnych dla serwerów aplikacji
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

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Wskazówki dotyczące wdrażania systemu Windows serwer usługi Active Directory na maszynach wirtualnych Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx)
* [Jak tooupload istniejącymi lokalnymi tooAzure kontrolerów domeny w funkcji Hyper-V za pomocą programu Azure PowerShell](http://support.microsoft.com/kb/2904015)
* [Instalowanie nowego lasu usługi Active Directory w sieci wirtualnej platformy Azure](active-directory-new-forest-virtual-machine.md)
* [Azure Virtual Network](../virtual-network/virtual-networks-overview.md)
* [Microsoft Azure IaaS specjalista IT: (01) maszyny wirtualnej podstawy](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure IaaS specjalista IT: (05) tworzenie sieci wirtualnych i łączności między lokalizacjami](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)
* [Azure PowerShell](/powershell/azure/overview)
* [Polecenia cmdlet do zarządzania platformy Azure](/powershell/module/azurerm.compute/#virtual_machines)

<!--Image references-->
[1]: ./media/active-directory-install-replica-active-directory-domain-controller/ReplicaDCsOnAzureVNet.png
