---
title: "Połącz z tooan sieci lokalnej sieci wirtualnej platformy Azure: sieci VPN lokacja-lokacja (klasyczne): Portal | Dokumentacja firmy Microsoft"
description: "Kroki toocreate połączenia IPsec z lokalnej sieci tooan sieci wirtualnej platformy Azure za pośrednictwem hello publicznej sieci Internet. Te kroki pomoże utworzyć przy użyciu portalu hello połączenie bramy sieci VPN typu lokacja-lokacja między lokalizacjami."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/010/2017
ms.author: cherylmc
ms.openlocfilehash: b260bdf610b264458660b278bd32bf0fc5b519ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-using-hello-azure-portal-classic"></a>Utwórz połączenie lokacja-lokacja za pomocą hello portalu Azure (klasyczne)

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

W tym artykule opisano, jak toouse hello Azure toocreate portalu połączenie bramy sieci VPN lokacja-lokacja z toohello sieci Twojej lokalnej sieci wirtualnej. Witaj czynności w tym artykule dotyczą toohello klasycznego modelu wdrażania. Można również utworzyć tę konfigurację za pomocą narzędzia wdrażania różnych lub model wdrożenia, wybierając inną opcję z hello następującej listy:

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [Interfejs wiersza polecenia](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portal Azure (klasyczny)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

Połączenie bramy sieci VPN typu lokacja-lokacja jest używane tooconnect lokalnej sieci tooan sieci wirtualnej platformy Azure za pośrednictwem tunelu VPN IPsec/IKE (IKEv1 lub IKEv2). Ten typ połączenia wymaga sieci VPN urządzeń znajdujących się lokalnie posiadających zewnętrznie połączonej publicznego tooit przypisany adres IP. Więcej informacji o bramach sieci VPN można znaleźć w artykule [Informacje dotyczące bram sieci VPN](vpn-gateway-about-vpngateways.md).

![Diagram połączenia bramy VPN Gateway typu lokacja-lokacja obejmującego wiele lokalizacji](./media/vpn-gateway-howto-site-to-site-classic-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a>Przed rozpoczęciem

Sprawdź, czy zostały spełnione następujące kryteria przed rozpoczęciem konfiguracji hello:

* Upewnij się, że chcesz toowork w hello klasycznego modelu wdrażania. Jeśli chcesz toowork w modelu wdrażania usługi Resource Manager hello, zobacz [utworzyć połączenie lokacja-lokacja (Resource Manager)](vpn-gateway-howto-site-to-site-resource-manager-portal.md). Jeśli to możliwe, zalecane jest użycie modelu wdrażania usługi Resource Manager hello.
* Upewnij się, że masz zgodne urządzenie sieci VPN i osoby, która jest w stanie tooconfigure go. Aby uzyskać więcej informacji o zgodnych urządzeniach sieci VPN i konfiguracji urządzeń, zobacz artykuł [Informacje o urządzeniach sieci VPN](vpn-gateway-about-vpn-devices.md).
* Sprawdź, czy masz dostępny zewnętrznie publiczny adres IPv4 urządzenia sieci VPN. Ten adres IP nie może się znajdować za translatorem adresów sieciowych.
* Jeśli nie znasz z zakresów adresów IP hello znajduje się w konfiguracji sieci lokalnej, należy toocoordinate z osobą, która Podaj te szczegóły należy. Podczas tworzenia tej konfiguracji należy określić hello prefiksów adresów IP zakresu czy Azure będzie przekierowywać tooyour lokalizacji lokalnej. Brak hello podsieci sieci lokalnej mogą za pośrednictwem laptop podsieci sieci wirtualnej hello, które mają tooconnect do.
* Obecnie programu PowerShell jest wymagane toospecify hello klucz i utworzyć połączenie bramy sieci VPN hello. Zainstaluj najnowszą wersję hello hello poleceń cmdlet programu PowerShell Azure usługi zarządzania (ko). Aby uzyskać więcej informacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview). Podczas pracy z programem PowerShell dla tej konfiguracji upewnij się, że działasz jako administrator. 

### <a name="values"></a>Przykładowe wartości konfiguracji dla tego ćwiczenia

Przykłady Hello w tym artykule Użyj hello następujące wartości. Można użyć tych wartości toocreate środowiska testowego, lub zobacz toothem toobetter zrozumieć hello przykłady w tym artykule.

* **Nazwa sieci wirtualnej:** TestVNet1
* **Przestrzeń adresowa:** 
  * 10.11.0.0/16
  * 10.12.0.0/16 (opcjonalnie na potrzeby tego ćwiczenia)
* **Podsieci:**
  * FrontEnd: 10.11.0.0/24
  * BackEnd: 10.12.0.0/24 (opcjonalnie na potrzeby tego ćwiczenia)
* **GatewaySubnet:** 10.11.255.0/27
* **Grupa zasobów:** TestRG1
* **Lokalizacja:** Wschodnie stany USA
* **Serwer DNS:** 10.11.0.3 (opcjonalnie na potrzeby tego ćwiczenia)
* **Nazwa lokacji lokalnej:** Lokacja2
* **Przestrzeń adresów klienta:** hello przestrzeń adresów, która znajduje się w lokacji lokalnej.

## <a name="CreatVNet"></a>1. Tworzenie sieci wirtualnej

Po utworzeniu sieci wirtualnej toouse dla połączeń S2S, należy się upewnić, że przestrzenie adresowe hello, które określisz nie pokrywają się ze wszystkimi hello przestrzeni adresów klienta dla hello lokalnych witryn, które mają tooconnect do toomake. Obecność nakładających się podsieci spowoduje, że połączenie nie będzie działać prawidłowo.

* Jeśli masz już sieć wirtualną, sprawdź, czy ustawienia hello są zgodne z projektu bramy sieci VPN. Należy zwrócić szczególną uwagę tooany podsieci, które nakładają się z innymi sieciami. 

* Jeśli nie masz jeszcze sieci wirtualnej, utwórz ją. Zamieszczone zrzuty ekranu są przykładowe. Należy się, że wartości hello tooreplace własnymi.

### <a name="toocreate-a-virtual-network"></a>toocreate sieci wirtualnej

1. W przeglądarce Przejdź toohello [portalu Azure](http://portal.azure.com) i, jeśli to konieczne, zaloguj się przy użyciu konta platformy Azure.
2. Kliknij pozycję **+**. W hello **marketplace hello wyszukiwania** wpisz "Sieci wirtualnej". Zlokalizuj **sieci wirtualnej** hello zwrócił listy i kliknij przycisk tooopen hello **sieci wirtualnej** strony.

  ![Strona wyszukiwania sieci wirtualnej](./media/vpn-gateway-howto-site-to-site-classic-portal/newvnetportal700.png)
3. Dolnej hello hello strony sieci wirtualnej, z hello **wybierz model wdrożenia** listy rozwijanej, wybierz **klasycznego**, a następnie kliknij przycisk **Utwórz**.

  ![Wybieranie modelu wdrożenia](./media/vpn-gateway-howto-site-to-site-classic-portal/selectmodel.png)
4. Na powitania **Tworzenie wirtualnych network(classic)** skonfiguruj hello ustawienia sieci wirtualnej. Na tej stronie dodaj pierwszą przestrzeń adresową i zakres adresów pojedynczej podsieci. Po utworzeniu hello sieci wirtualnej można wrócić do poprzedniej strony i dodać dodatkowe podsieci oraz przestrzenie adresowe.

  ![Strona Tworzenie sieci wirtualnej](./media/vpn-gateway-howto-site-to-site-classic-portal/createvnet.png "Strona Tworzenie sieci wirtualnej")
5. Sprawdź, że hello **subskrypcji** jest hello właściwy. Subskrypcje można zmienić za pomocą listy rozwijanej hello.
6. Kliknij przycisk **Grupa zasobów** i wybierz istniejącą grupę zasobów lub utwórz nową, wpisując nazwę. Aby uzyskać więcej informacji na temat grup zasobów, zobacz temat [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).
7. Następnie wybierz pozycję hello **lokalizacji** ustawienia sieci wirtualnej. Lokalizacja Hello Określa, gdzie znajdują się zasoby hello wdrożenie toothis sieci wirtualnej.
8. Toofind stanie toobe sieci wirtualnej w prosty sposób na powitania pulpitu nawigacyjnego, wybierz opcję **toodashboard numeru Pin**. Kliknij przycisk **Utwórz** toocreate sieci wirtualnej.

  ![Numer PIN toodashboard](./media/vpn-gateway-howto-site-to-site-classic-portal/pintodashboard150.png "toodashboard numeru Pin")
9. Po kliknięciu pozycji "Utwórz", Kafelek pojawia się na pulpicie nawigacyjnym hello, które odzwierciedla hello postęp Twojej sieci wirtualnej. Trwa tworzenie Hello kafelka zmienia hello sieci wirtualnej.

  ![Kafelek Tworzenie sieci wirtualnej](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png "Tworzenie sieci wirtualnej")

Po utworzeniu sieci wirtualnej, zobacz **utworzony** kategorii **stan** na stronie sieci hello hello klasycznego portalu Azure.

## <a name="additionaladdress"></a>2. Dodawanie kolejnej przestrzeni adresowej

Po utworzeniu sieci wirtualnej możesz dodać kolejną przestrzeń adresową. Dodawanie dodatkową przestrzeń adresów nie jest wymagana część konfiguracji S2S, ale jeśli wiele przestrzeni adresów, używaj hello następujące kroki:

1. W portalu hello Znajdź hello sieci wirtualnych.
2. Na stronie powitania dla sieci wirtualnej, w obszarze hello **ustawienia** kliknij **przestrzeni adresów**.
3. Na stronie przestrzeni adresów powitania kliknij **+ Dodaj** i wprowadzić dodatkową przestrzeń adresów.

## <a name="dns"></a>3. Określanie serwera DNS

Ustawienia DNS nie są wymagane w przypadku konfiguracji typu lokacja-lokacja, ale serwer DNS jest konieczny, aby korzystać z rozpoznawania nazw. Określenie wartości nie powoduje utworzenia nowego serwera DNS. Witaj adres IP serwera DNS, który określisz powinna być serwera DNS, który może rozpoznawać nazwy hello hello zasoby, które są nawiązywane. W przypadku ustawień przykład Witaj użyliśmy prywatnego adresu IP. adres IP Hello używanych prawdopodobnie nie jest adresem IP powitania serwera DNS. Należy się toouse własne wartości.

Po utworzeniu sieci wirtualnej, można dodać hello adres IP serwera toohandle nazwę DNS. Otwórz ustawienia powitania dla sieci wirtualnej, kliknij pozycję serwery DNS, a następnie dodaj hello adres IP serwera DNS hello mają toouse do rozpoznawania nazw.

1. W portalu hello Znajdź hello sieci wirtualnych.
2. Na stronie powitania dla sieci wirtualnej, w obszarze hello **ustawienia** kliknij **serwerów DNS**.
3. Dodaj serwer DNS.
4. toosave ustawienia, kliknij przycisk **zapisać** u góry hello hello strony.

## <a name="localsite"></a>4. Konfigurowanie lokacji lokalne powitania

witryny lokalne powitania odnosi się zazwyczaj tooyour lokalnej lokalizacji. Zawiera adres IP hello toowhich urządzenia sieci VPN hello utworzy połączenie i hello zakresów adresów IP, które zostaną przesłane za pomocą urządzenia sieci VPN toohello hello VPN bramy.

1. W portalu hello Przejdź toohello sieci wirtualnej, dla której ma zostać toocreate bramy.
2. Na stronie powitania dla sieci wirtualnej, na powitania **omówienie** w sekcji połączenia sieci VPN hello, kliknij **bramy** tooopen hello **nowego połączenia sieci VPN** strony.

  ![Kliknij przycisk Ustawienia bramy tooconfigure](./media/vpn-gateway-howto-site-to-site-classic-portal/beforegw125.png "kliknij ustawienia bramy tooconfigure")
3. Na powitania **nowego połączenia sieci VPN** wybierz pozycję **lokacja lokacja**.
4. Kliknij przycisk **lokalnej lokacji — Skonfiguruj wymagane ustawienia** tooopen hello **lokacji lokalnej** strony. Skonfiguruj ustawienia hello, a następnie kliknij przycisk **OK** toosave hello ustawienia.
  - **Nazwa:** Utwórz nazwę użytkownika toomake lokacji lokalnej go łatwo możesz tooidentify.
  - **Adres IP bramy sieci VPN:** to publiczny adres IP hello hello urządzenia sieci VPN w sieci lokalnej. Witaj urządzenia sieci VPN wymaga publiczny adres IP IPv4. Określ prawidłowy publiczny adres IP hello ma tooconnect toowhich urządzenia sieci VPN. Nie może być za translatorem adresów Sieciowych, a ma toobe osiągalny przez platformę Azure. Jeśli nie znasz hello adres IP urządzenia sieci VPN, możesz zawsze umieszczać w wartości symbolu zastępczego (o ile jest w formacie hello publiczny adres IP) i zmienić później.
  - **Przestrzeń adresów klienta:** zakresów adresów IP hello listy, które mają kierowane toohello sieć lokalną lokalnej za pośrednictwem tej bramy. Można dodać wiele zakresów przestrzeni adresów. Upewnij się, że hello określone w tym miejscu nie pokrywały zakresów z innymi sieciami, który łączy się z sieci wirtualnej lub hello zakresów adresów sieci wirtualnej hello samej siebie.

  ![Lokacja lokalna](./media/vpn-gateway-howto-site-to-site-classic-portal/localnetworksite.png "Konfigurowanie lokacji lokalnej")

## <a name="gatewaysubnet"></a>5. Skonfiguruj podsieci bramy hello

Musisz utworzyć podsieć dla bramy sieci VPN. podsieć bramy Hello zawiera adresy IP hello korzystających z usługi bramy sieci VPN hello.

1. Na powitania **nowego połączenia sieci VPN** strony, hello zaznacz pole wyboru **Utwórz bramę natychmiast**. zostanie wyświetlona strona powitania "konfiguracji bramy opcjonalne". Jeśli nie zaznaczysz pola wyboru hello, nie zobaczysz hello strony tooconfigure hello bramy podsieci.

  ![Konfiguracja bramy — Podsieć, rozmiar, typ routingu](./media/vpn-gateway-howto-site-to-site-classic-portal/optional.png "Konfiguracja bramy — Podsieć, rozmiar, typ routingu")
2. Witaj tooopen **konfiguracji bramy** kliknij przycisk **konfiguracji bramy opcjonalne — podsieć, rozmiar i typ routingu**.
3. Na powitania **konfiguracji bramy** kliknij przycisk **podsieci — Skonfiguruj wymagane ustawienia** tooopen hello **Dodaj podsieć** strony.

  ![Konfiguracja bramy — Podsieć bramy](./media/vpn-gateway-howto-site-to-site-classic-portal/subnetrequired.png "Konfiguracja bramy — Podsieć bramy")
4. Na powitania **Dodaj podsieć** Dodaj hello podsieci bramy. rozmiar Hello hello podsieć bramy, który określisz jest zależna od konfiguracji bramy sieci VPN hello, które mają toocreate. Mimo że jest możliwe toocreate jak /29 podsieć bramy, zalecane jest użycie /27 lub /28. Spowoduje to utworzenie większej podsieci obejmującej więcej adresów. Przy użyciu większych podsieci bramy umożliwia za mało adresów tooaccommodate możliwe przyszłych konfiguracją IP.

  ![Dodawanie podsieci bramy](./media/vpn-gateway-howto-site-to-site-classic-portal/addgwsubnet.png "Dodawanie podsieci bramy")

## <a name="sku"></a>6. Określ hello jednostki SKU i typ sieci VPN

1. Wybierz hello bramy **rozmiar**. To jest brama hello SKU bramy sieci wirtualnej można użyć toocreate. W portalu hello hello "SKU domyślna" = **podstawowe**. Klasycznego bramy sieci VPN Użyj hello starego bramy (starsze) jednostki SKU. Aby uzyskać więcej informacji na temat hello brama starszej wersji jednostki SKU, zobacz [Praca z bramy sieci wirtualnej jednostki SKU (stary jednostki SKU)](vpn-gateway-about-skus-legacy.md).

  ![Wybieranie typu jednostki SKU i sieci VPN](./media/vpn-gateway-howto-site-to-site-classic-portal/sku.png "Wybieranie typu jednostki SKU i sieci VPN")
2. Wybierz hello **typ routingu** dla bramy. To jest nazywana hello typ sieci VPN. Jest on typu bramy poprawne hello tooselect ważne, ponieważ hello bramy nie mogą konwertować z jednego typu tooanother. Urządzenie sieci VPN musi być zgodny z typem routingu hello, którą wybierzesz. Więcej informacji o typie sieci VPN można znaleźć w artykule [Informacje na temat ustawień usługi VPN Gateway](vpn-gateway-about-vpn-gateway-settings.md#vpntype). Może zostać wyświetlony artykuły przywołuje too'RouteBased "i"PolicyBased"VPN typów. "Dynamiczny"odpowiada too'RouteBased", a"Static"odpowiada"PolicyBased".
3. Kliknij przycisk **OK** toosave hello ustawienia.
4. Na powitania **nowego połączenia sieci VPN** kliknij przycisk **OK** u dołu hello toobegin strony hello Tworzenie bramy sieci wirtualnej. W zależności od hello zostanie wybrana jednostka SKU może potrwać toocreate minut too45 bramy sieci wirtualnej.

## <a name="vpndevice"></a>7. Konfiguracja urządzenia sieci VPN

Sieć lokalną tooan połączeń lokacja-lokacja wymagają urządzenia sieci VPN. W tym kroku konfigurowane jest urządzenie sieci VPN. Podczas konfigurowania urządzenia sieci VPN, potrzebne są następujące hello:

- Klucz współużytkowany. Jest to hello sam udostępniony klucz, który należy określić podczas tworzenia połączenia sieci VPN typu lokacja-lokacja. W naszych przykładach używamy podstawowego klucza współużytkowanego. Firma Microsoft zaleca, aby wygenerować bardziej złożonych toouse klucza.
- Witaj publiczny adres IP bramy sieci wirtualnej. Publiczny adres IP hello można wyświetlić za pomocą hello portalu Azure, programu PowerShell lub interfejsu wiersza polecenia.

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a>8. Utwórz połączenie hello
W tym kroku możesz ustawić klucza wspólnego hello i utworzyć hello połączenia. należy ustawić klucz Hello jest musi być hello tego samego klucza, który był używany w konfiguracji urządzenia sieci VPN.

> [!NOTE]
> Ten krok nie jest obecnie dostępna w hello portalu Azure. Należy użyć wersji usługi zarządzania (SM) hello hello poleceń cmdlet programu Azure PowerShell.
>

### <a name="step-1-connect-tooyour-azure-account"></a>Krok 1. Połącz tooyour konto platformy Azure

1. Otwórz konsolę programu PowerShell z podwyższonym poziomem uprawnień i Połącz konto tooyour. Użyj powitania po toohelp przykład, gdy nawiązujesz połączenie:

  ```powershell
  Add-AzureAccount
  ```
2. Sprawdź subskrypcje hello hello konta.

  ```powershell
  Get-AzureSubscription
  ```
3. Jeśli masz więcej niż jedną subskrypcję, wybierz subskrypcję hello, które mają toouse.

  ```powershell
  Select-AzureSubscription -SubscriptionId "Replace_with_your_subscription_ID"
  ```

### <a name="step-2-set-hello-shared-key-and-create-hello-connection"></a>Krok 2. Ustaw klucz udostępniony hello oraz tworzenie połączenia hello

Podczas pracy z programu PowerShell i hello klasycznego modelu wdrażania, czasami hello nazwy zasobów w portalu hello są hello nazwy hello Azure oczekuje toosee przy użyciu programu PowerShell. Witaj Poniższe etapy ułatwiają wyeksportować hello sieci tooobtain hello dokładne wartości w pliku konfiguracji dla nazw hello.

1. Utwórz katalog na komputerze, a następnie wyeksportować katalogu toohello pliku konfiguracji sieci hello. W tym przykładzie pliku konfiguracji sieci hello jest tooC:\AzureNet wyeksportowane.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. Otwórz plik konfiguracji sieci hello w edytorze xml i sprawdź hello wartości "Nazwa LocalNetworkSite" i "VirtualNetworkSite name". Zmodyfikuj hello przykładowe tooreflect hello wartości, które są potrzebne. Podczas określania nazwy, która zawiera spacje, użyj pojedynczy znaki cudzysłowu otaczające wartość hello.

3. Ustaw klucz udostępniony hello oraz tworzenie połączenia hello. Witaj "-SharedKey" to Generowanie i określ wartość. Przykład Witaj użyliśmy "abc123", ale może generować (i powinien) użyj bardziej złożonych. Witaj ważne, czy element jest daną hello określone w tym miejscu musi być powitalne samą wartość, że zostało określone podczas konfigurowania urządzenia sieci VPN.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group TestRG1 TestVNet1' `
  -LocalNetworkSiteName 'D1BFC9CB_Site2' -SharedKey abc123
  ```
Po utworzeniu połączenia hello jest wynik hello: **stanu: pomyślnie**.

## <a name="verify"></a>9. Weryfikowanie połączenia

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

Jeśli występują problemy z połączeniem, zobacz hello **rozwiązywanie** sekcji hello spisu treści w okienku po lewej stronie powitania.

## <a name="reset"></a>Jak tooreset bramy sieci VPN

Resetowanie bramy Azure VPN Gateway przydaje się w przypadku utraty połączenia sieci VPN obejmującego wiele lokalizacji w jednym lub wielu tunelach VPN typu lokacja-lokacja. W takiej sytuacji lokalnego urządzenia sieci VPN są wszystkie działa poprawnie, ale są nie jest w stanie tooestablish tuneli protokołu IPsec o hello bram sieci VPN platformy Azure. Aby uzyskać instrukcje, zobacz [Resetowanie bramy VPN Gateway](vpn-gateway-resetgw-classic.md).

## <a name="changesku"></a>Jak toochange jednostka SKU bramy

Aby hello kroki toochange jednostka SKU bramy, zobacz [Resize jednostka SKU bramy](vpn-gateway-about-SKUS-legacy.md).

## <a name="next-steps"></a>Następne kroki

* Po zakończeniu połączenia można dodać sieci wirtualnych tooyour maszyn wirtualnych. Aby uzyskać więcej informacji, zobacz [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) (Maszyny wirtualne).
* Aby uzyskać informacje o wymuszonym tunelowaniu, zobacz [Informacje o wymuszonym tunelowaniu](vpn-gateway-about-forced-tunneling.md).