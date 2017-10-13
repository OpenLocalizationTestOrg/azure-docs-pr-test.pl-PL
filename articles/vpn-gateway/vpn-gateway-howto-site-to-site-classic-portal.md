---
title: "Łączenie sieci lokalnej z siecią wirtualną platformy Azure: sieć VPN typu lokacja-lokacja (model klasyczny): portal | Microsoft Docs"
description: "Kroki tworzenia połączenia IPsec z sieci lokalnej do sieci wirtualnej platformy Azure za pośrednictwem publicznego Internetu. Kroki te są pomocne podczas tworzenia obejmującego wiele lokalizacji połączenia bramy sieci VPN typu lokacja-lokacja za pomocą portalu."
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
ms.openlocfilehash: 0be8dd6d90edb7b32b6777c76c9778cda0dcd5ea
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="create-a-site-to-site-connection-using-the-azure-portal-classic"></a>Tworzenie sieci wirtualnej za pomocą połączenia typu lokacja-lokacja przy użyciu witryny Azure Portal (model klasyczny)

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

Ten artykuł pokazuje, jak używać witryny Azure Portal do tworzenia połączenia bramy sieci VPN lokacja-lokacja z sieci lokalnej do sieci wirtualnej. Kroki podane w tym artykule mają zastosowanie do klasycznego modelu wdrażania. Tę konfigurację możesz również utworzyć przy użyciu innego narzędzia wdrażania lub modelu wdrażania, wybierając inną opcję z następującej listy:

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [Interfejs wiersza polecenia](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portal Azure (klasyczny)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

Połączenie bramy sieci VPN typu lokacja-lokacja umożliwia łączenie sieci lokalnej z siecią wirtualną platformy Azure za pośrednictwem tunelu sieci VPN IPsec/IKE (IKEv1 lub IKEv2). Ten typ połączenia wymaga lokalnego urządzenia sieci VPN z przypisanym publicznym adresem IP dostępnym z zewnątrz. Więcej informacji o bramach sieci VPN można znaleźć w artykule [Informacje dotyczące bram sieci VPN](vpn-gateway-about-vpngateways.md).

![Diagram połączenia bramy VPN Gateway typu lokacja-lokacja obejmującego wiele lokalizacji](./media/vpn-gateway-howto-site-to-site-classic-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a>Przed rozpoczęciem

Przed rozpoczęciem konfiguracji sprawdź, czy są spełnione następujące kryteria:

* Upewnij się, że chcesz pracować w klasycznym modelu wdrażania. Jeśli chcesz pracować w modelu wdrażania usługi Resource Manager, zobacz [Tworzenie połączenia typu lokacja-lokacja (Resource Manager)](vpn-gateway-howto-site-to-site-resource-manager-portal.md). Zawsze, jeśli jest to możliwe, zalecamy użycie modelu wdrażania przy użyciu usługi Resource Manager.
* Upewnij się, że masz zgodne urządzenie sieci VPN i dostępna jest osoba, która umie je skonfigurować. Aby uzyskać więcej informacji o zgodnych urządzeniach sieci VPN i konfiguracji urządzeń, zobacz artykuł [Informacje o urządzeniach sieci VPN](vpn-gateway-about-vpn-devices.md).
* Sprawdź, czy masz dostępny zewnętrznie publiczny adres IPv4 urządzenia sieci VPN. Ten adres IP nie może się znajdować za translatorem adresów sieciowych.
* Jeśli nie znasz zakresów adresów IP w konfiguracji swojej sieci lokalnej, skontaktuj się z osobą, która może podać Ci te dane. Tworząc tę konfigurację, musisz określić prefiksy zakresu adresów IP, które platforma Azure będzie kierować do Twojej lokalizacji lokalnej. Żadna z podsieci sieci lokalnej nie może się nakładać na podsieci sieci wirtualnej, z którymi chcesz nawiązać połączenie.
* Obecnie w celu określenia klucza współużytkowanego i utworzenia połączenia bramy sieci VPN jest wymagany program PowerShell. Zainstaluj najnowszą wersję poleceń cmdlet programu PowerShell usługi Azure Service Management (SM). Aby uzyskać więcej informacji, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview). Podczas pracy z programem PowerShell dla tej konfiguracji upewnij się, że działasz jako administrator. 

### <a name="values"></a>Przykładowe wartości konfiguracji dla tego ćwiczenia

W przykładach w tym artykule są stosowane następujące wartości. Tych wartości możesz użyć do tworzenia środowiska testowego lub odwoływać się do nich, aby lepiej zrozumieć przykłady w niniejszym artykule.

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
* **Przestrzeń adresowa klienta:** przestrzeń adresowa znajdująca się w lokacji lokalnej.

## <a name="CreatVNet"></a>1. Tworzenie sieci wirtualnej

Podczas tworzenia sieci wirtualnej na potrzeby połączenia typu lokacja-lokacja upewnij się, że określone przestrzenie adresowe nie nakładają się na żadne przestrzenie adresowe klientów dla lokacji lokalnych, z którymi chcesz nawiązywać połączenia. Obecność nakładających się podsieci spowoduje, że połączenie nie będzie działać prawidłowo.

* Jeśli masz już sieć wirtualną, sprawdź, czy ustawienia są zgodne z projektem bramy sieci VPN. Zwróć szczególną uwagę na wszelkie podsieci, które mogą pokrywać się z innymi sieciami. 

* Jeśli nie masz jeszcze sieci wirtualnej, utwórz ją. Zamieszczone zrzuty ekranu są przykładowe. Przedstawione wartości należy zastąpić własnymi.

### <a name="to-create-a-virtual-network"></a>Aby utworzyć sieć wirtualną

1. W przeglądarce przejdź do witryny [Azure Portal](http://portal.azure.com) i, jeśli to konieczne, zaloguj się przy użyciu konta platformy Azure.
2. Kliknij pozycję **+**. W polu **Szukaj w witrynie Marketplace** wpisz „Sieć wirtualna”. Znajdź pozycję **Sieć wirtualna** na liście wyników i kliknij, aby otworzyć stronę **Sieć wirtualna**.

  ![Strona wyszukiwania sieci wirtualnej](./media/vpn-gateway-howto-site-to-site-classic-portal/newvnetportal700.png)
3. Z listy rozwijanej **Wybierz model wdrożenia** w dolnej części strony Sieć wirtualna wybierz pozycję **Klasyczny**, a następnie kliknij przycisk **Utwórz**.

  ![Wybieranie modelu wdrożenia](./media/vpn-gateway-howto-site-to-site-classic-portal/selectmodel.png)
4. Na stronie **Utwórz sieć wirtualną (klasyczną)** skonfiguruj ustawienia sieci wirtualnej. Na tej stronie dodaj pierwszą przestrzeń adresową i zakres adresów pojedynczej podsieci. Po zakończeniu tworzenia sieci wirtualnej możesz wrócić i dodać dodatkowe podsieci oraz przestrzenie adresowe.

  ![Strona Tworzenie sieci wirtualnej](./media/vpn-gateway-howto-site-to-site-classic-portal/createvnet.png "Strona Tworzenie sieci wirtualnej")
5. Sprawdź, czy pole **Subskrypcja** zawiera prawidłową wartość. Subskrypcje można zmieniać, korzystając z listy rozwijanej.
6. Kliknij przycisk **Grupa zasobów** i wybierz istniejącą grupę zasobów lub utwórz nową, wpisując nazwę. Aby uzyskać więcej informacji na temat grup zasobów, zobacz temat [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).
7. Następnie w polu **Lokalizacja** wybierz ustawienia sieci wirtualnej. Lokalizacja określa miejsce, w którym zostaną umieszczone zasoby wdrażane w tej sieci wirtualnej.
8. Jeśli chcesz, aby Twoją sieć wirtualną można było łatwo znaleźć na pulpicie nawigacyjnym, wybierz pozycję **Przypnij do pulpitu nawigacyjnego**. Kliknij przycisk **Utwórz**, aby utworzyć sieć wirtualną.

  ![Przypnij do pulpitu nawigacyjnego](./media/vpn-gateway-howto-site-to-site-classic-portal/pintodashboard150.png "Przypnij do pulpitu nawigacyjnego")
9. Po kliknięciu przycisku „Utwórz” na pulpicie nawigacyjnym zostanie umieszczony kafelek, który będzie odzwierciedlać postęp Twojej sieci wirtualnej. Wygląd kafelka zmienia się w trakcie tworzenia sieci wirtualnej.

  ![Kafelek Tworzenie sieci wirtualnej](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png "Tworzenie sieci wirtualnej")

Po utworzeniu sieci wirtualnej w obszarze **Stan** na stronie sieci w klasycznej witrynie Azure Portal będzie widoczna wartość **Utworzona**.

## <a name="additionaladdress"></a>2. Dodawanie kolejnej przestrzeni adresowej

Po utworzeniu sieci wirtualnej możesz dodać kolejną przestrzeń adresową. Dodanie kolejnej przestrzeni adresowej nie jest wymagane w przypadku konfiguracji typu lokacja-lokacja, ale jeśli potrzebujesz wielu przestrzeni adresowych, wykonaj następujące kroki:

1. Znajdź sieci wirtualne w portalu.
2. Na stronie Twojej sieci wirtualnej w sekcji **Ustawienia** kliknij pozycję **Przestrzeń adresowa**.
3. Na stronie Przestrzeń adresowa kliknij pozycję **+Dodaj** i wprowadź dodatkową przestrzeń adresową.

## <a name="dns"></a>3. Określanie serwera DNS

Ustawienia DNS nie są wymagane w przypadku konfiguracji typu lokacja-lokacja, ale serwer DNS jest konieczny, aby korzystać z rozpoznawania nazw. Określenie wartości nie powoduje utworzenia nowego serwera DNS. Określony adres IP serwera DNS powinien być adresem serwera będącego w stanie rozpoznawać nazwy zasobów, z którymi nawiązywane jest połączenie. W ustawieniach przykładowych użyto prywatnego adresu IP. Użyty przez nas adres IP prawdopodobnie nie jest adresem IP Twojego serwera DNS. Pamiętaj, aby użyć własnych wartości.

Po utworzeniu sieci wirtualnej możesz dodać adres IP serwera DNS, aby umożliwić obsługę rozpoznawania nazw. Otwórz ustawienia dla sieci wirtualnej, kliknij pozycję Serwery DNS i dodaj adres IP serwera DNS, który ma być używany do rozpoznawania nazw.

1. Znajdź sieci wirtualne w portalu.
2. Na stronie Twojej sieci wirtualnej w sekcji **Ustawienia** kliknij pozycję **Serwery DNS**.
3. Dodaj serwer DNS.
4. Aby zapisać ustawienia, kliknij przycisk **Zapisz** znajdujący się u góry strony.

## <a name="localsite"></a>4. Konfigurowanie lokacji lokalnej

Lokacja lokalna zazwyczaj oznacza lokalizację lokalną. Zawiera ona adres IP urządzenia sieci VPN, z którym będzie tworzone połączenie, oraz zakresy adresów IP, które będą kierowane za pośrednictwem bramy sieci VPN do tego urządzenia sieci VPN.

1. W witrynie portalu przejdź do sieci wirtualnej, dla której chcesz utworzyć bramę.
2. Na stronie **Przegląd** Twojej sieci wirtualnej w sekcji Połączenia VPN kliknij pozycję **Brama**, aby otworzyć stronę **Nowe połączenie VPN**.

  ![Kliknij, aby skonfigurować ustawienia bramy](./media/vpn-gateway-howto-site-to-site-classic-portal/beforegw125.png "Kliknij, aby skonfigurować ustawienia bramy")
3. Na stronie **Nowe połączenie VPN** wybierz pozycję **Lokacja-lokacja**.
4. Kliknij pozycję **Lokacja lokalna — Skonfiguruj wymagane ustawienia**, aby otworzyć stronę **Lokacja lokalna**. Skonfiguruj ustawienia, a następnie kliknij przycisk **OK**, aby je zapisać.
  - **Nazwa:** Utwórz nazwę lokacji lokalnej, aby ułatwić jej identyfikację.
  - **Adres IP bramy sieci VPN:** Publiczny adres IP urządzenia sieci VPN w sieci lokalnej. Urządzenie sieci VPN wymaga publicznego adresu IPv4. Określ prawidłowy publiczny adres IP dla urządzenia sieci VPN, z którym chcesz się połączyć. Nie może ono znajdować się za translatorem adresów sieciowych i musi być dostępne za pomocą usługi Azure. Jeśli nie znasz adresu IP urządzenia sieci VPN, zawsze możesz podać wartość zastępczą (o ile jest w formacie prawidłowego publicznego adresu IP) i zmienić ją później.
  - **Przestrzeń adresowa klienta:** Podaj listę zakresów adresów IP, które mają być kierowane do sieci lokalnej za pośrednictwem tej bramy. Można dodać wiele zakresów przestrzeni adresów. Upewnij się, że określone w tym miejscu zakresy nie pokrywają się z zakresami innych sieci, z którymi łączy się Twoja sieć wirtualna, ani z zakresami adresów samej sieci wirtualnej.

  ![Lokacja lokalna](./media/vpn-gateway-howto-site-to-site-classic-portal/localnetworksite.png "Konfigurowanie lokacji lokalnej")

## <a name="gatewaysubnet"></a>5. Konfigurowanie podsieci bramy

Musisz utworzyć podsieć dla bramy sieci VPN. Podsieć bramy zawiera adresy IP, z których korzystają usługi bramy sieci VPN.

1. Na stronie **Nowe połączenie VPN** zaznacz pole wyboru **Utwórz bramę natychmiast**. Zostanie wyświetlona strona „Opcjonalna konfiguracja bramy”. Jeśli nie zaznaczysz pola wyboru, strona umożliwiająca skonfigurowanie podsieci bramy nie zostanie wyświetlona.

  ![Konfiguracja bramy — Podsieć, rozmiar, typ routingu](./media/vpn-gateway-howto-site-to-site-classic-portal/optional.png "Konfiguracja bramy — Podsieć, rozmiar, typ routingu")
2. Aby otworzyć stronę **Konfiguracja bramy**, kliknij pozycję **Opcjonalna konfiguracja bramy — Podsieć, rozmiar i typ routingu**.
3. Na stronie **Konfiguracja bramy** kliknij pozycję **Podsieć — Skonfiguruj wymagane ustawienia**, aby otworzyć stronę **Dodawanie podsieci**.

  ![Konfiguracja bramy — Podsieć bramy](./media/vpn-gateway-howto-site-to-site-classic-portal/subnetrequired.png "Konfiguracja bramy — Podsieć bramy")
4. Na stronie **Dodawanie podsieci** dodaj podsieć bramy. Rozmiar określanej podsieci bramy zależy od konfiguracji bramy sieci VPN, którą chcesz utworzyć. Jest możliwe utworzenie małej podsieci bramy (/29), jednak zalecamy użycie rozmiaru /27 lub /28. Spowoduje to utworzenie większej podsieci obejmującej więcej adresów. Zastosowanie większej podsieci bramy daje wystarczającą liczbę adresów IP, aby uwzględnić możliwe przyszłe konfiguracje.

  ![Dodawanie podsieci bramy](./media/vpn-gateway-howto-site-to-site-classic-portal/addgwsubnet.png "Dodawanie podsieci bramy")

## <a name="sku"></a>6. Określ typ jednostki SKU i sieci VPN

1. Wybierz **rozmiar** bramy. To jest jednostka SKU bramy używana do tworzenia bramy sieci wirtualnej. W portalu domyślna jednostka SKU to **Podstawowa**. Klasyczne bramy sieci VPN używają starych (starszych) jednostek SKU bramy. Aby uzyskać więcej informacji o starszych jednostkach SKU bramy, zobacz [Working with virtual network gateway SKUs (old SKUs) (Praca z jednostkami SKU [starymi jednostkami SKU] bramy sieci wirtualnej)](vpn-gateway-about-skus-legacy.md).

  ![Wybieranie typu jednostki SKU i sieci VPN](./media/vpn-gateway-howto-site-to-site-classic-portal/sku.png "Wybieranie typu jednostki SKU i sieci VPN")
2. Wybierz **Typ routingu** dla bramy. Jest on również nazywany typem sieci VPN. Wybranie poprawnego typu bramy jest bardzo ważne, ponieważ nie można konwertować bramy na inny typ. Urządzenie sieci VPN musi być zgodne z wybranym typem routingu. Więcej informacji o typie sieci VPN można znaleźć w artykule [Informacje na temat ustawień usługi VPN Gateway](vpn-gateway-about-vpn-gateway-settings.md#vpntype). W niektórych artykułach mogą znajdować się odwołania do typów sieci VPN „RouteBased” i „PolicyBased”. Typ „Dynamiczny” odpowiada typowi „RouteBased”, a „Statyczny” — typowi „PolicyBased”.
3. Kliknij pozycję **OK**, aby zapisać ustawienia.
4. Na stronie **Nowe połączenie VPN** kliknij przycisk **OK** u dołu strony, aby rozpocząć tworzenie bramy sieci wirtualnej. W zależności od wybranej jednostki SKU tworzenie bramy sieci wirtualnej może potrwać do 45 minut.

## <a name="vpndevice"></a>7. Konfiguracja urządzenia sieci VPN

Połączenia typu lokacja-lokacja z siecią lokalną wymagają urządzenia sieci VPN. W tym kroku konfigurowane jest urządzenie sieci VPN. Podczas konfigurowania urządzenia sieci VPN potrzebne będą:

- Klucz współużytkowany. To ten sam klucz współużytkowany, który jest określany podczas tworzenia połączenia sieci VPN typu lokacja-lokacja. W naszych przykładach używamy podstawowego klucza współużytkowanego. Zalecamy, aby do użycia wygenerować bardziej złożony klucz.
- Publiczny adres IP bramy sieci wirtualnej. Publiczny adres IP można wyświetlić za pomocą witryny Azure Portal, programu PowerShell lub interfejsu wiersza polecenia.

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a>8. Tworzenie połączenia
W tym kroku należy ustawić klucz współużytkowany i utworzyć połączenie. Ustawiony klucz musi być tym samym kluczem, którego użyto do skonfigurowania urządzenia sieci VPN.

> [!NOTE]
> Obecnie tego kroku nie można wykonać w witrynie Azure Portal. Musisz użyć wersji poleceń cmdlet programu Azure PowerShell pochodzącej z usługi Service Management (SM).
>

### <a name="step-1-connect-to-your-azure-account"></a>Krok 1. Nawiąż połączenie z kontem platformy Azure

1. Otwórz konsolę programu PowerShell z podwyższonym poziomem uprawnień i połącz się ze swoim kontem. Użyj poniższego przykładu w celu łatwiejszego nawiązania połączenia:

  ```powershell
  Add-AzureAccount
  ```
2. Sprawdź subskrypcje dostępne na koncie.

  ```powershell
  Get-AzureSubscription
  ```
3. Jeśli masz więcej niż jedną subskrypcję, wybierz tę, której chcesz użyć.

  ```powershell
  Select-AzureSubscription -SubscriptionId "Replace_with_your_subscription_ID"
  ```

### <a name="step-2-set-the-shared-key-and-create-the-connection"></a>Krok 2. Ustaw klucz współużytkowany i utwórz połączenie

Podczas pracy z programem PowerShell w klasycznym modelu wdrażania czasami nazwy zasobów w portalu nie są nazwami, których platforma Azure oczekuje przy korzystaniu z programu PowerShell. Poniższe kroki pomogą Ci wyeksportować plik konfiguracji sieci, aby uzyskać dokładne wartości nazw.

1. Utwórz katalog na komputerze, a następnie wyeksportuj plik konfiguracji sieci do tego katalogu. W tym przykładzie plik konfiguracji sieci zostanie wyeksportowany do katalogu C:\AzureNet.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. Otwórz plik konfiguracji sieci przy użyciu edytora xml, a następnie sprawdź wartości właściwości „LocalNetworkSite name” i „VirtualNetworkSite name”. Zmodyfikuj przykład tak, aby odzwierciedlał odpowiednie wartości. W przypadku podawania nazwy, która zawiera spacje, umieść wartość w apostrofach.

3. Ustaw klucz współużytkowany i utwórz połączenie. Wartość „-SharedKey” jest generowana i określana przez Ciebie. W tym przykładzie użyliśmy wartości „abc123”, ale można (i należy) wygenerować bardziej złożoną wartość. Pamiętaj o tym, że wartość podana w tym miejscu musi być taka sama, jak wartość podana podczas konfigurowania urządzenia sieci VPN.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group TestRG1 TestVNet1' `
  -LocalNetworkSiteName 'D1BFC9CB_Site2' -SharedKey abc123
  ```
Wynik po utworzeniu połączenia: **Stan: Powodzenie**.

## <a name="verify"></a>9. Weryfikowanie połączenia

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

Jeśli występują problemy z połączeniem, zobacz sekcję **Rozwiązywanie problemów** spisu treści w okienku po lewej stronie.

## <a name="reset"></a>Jak zresetować bramę VPN Gateway

Resetowanie bramy Azure VPN Gateway przydaje się w przypadku utraty połączenia sieci VPN obejmującego wiele lokalizacji w jednym lub wielu tunelach VPN typu lokacja-lokacja. W takiej sytuacji urządzenia lokalnej sieci VPN działają prawidłowo, ale nie mogą nawiązać połączenia w ramach tuneli używających protokołu IPsec z bramami sieci VPN Azure. Aby uzyskać instrukcje, zobacz [Resetowanie bramy VPN Gateway](vpn-gateway-resetgw-classic.md).

## <a name="changesku"></a>Jak zmienić jednostkę SKU bramy

Aby uzyskać instrukcje zmiany jednostki SKU bramy, zobacz [Resize a gateway SKU (Zmiana rozmiaru jednostki SKU bramy)](vpn-gateway-about-SKUS-legacy.md).

## <a name="next-steps"></a>Następne kroki

* Po zakończeniu procesu nawiązywania połączenia można dodać do sieci wirtualnych maszyny wirtualne. Aby uzyskać więcej informacji, zobacz [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) (Maszyny wirtualne).
* Aby uzyskać informacje o wymuszonym tunelowaniu, zobacz [Informacje o wymuszonym tunelowaniu](vpn-gateway-about-forced-tunneling.md).