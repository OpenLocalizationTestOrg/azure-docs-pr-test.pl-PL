---
title: "Utwórz lub zaktualizuj bramę aplikacji Azure z zapory aplikacji sieci web | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć bramę aplikacji z zapory aplikacji sieci web przy użyciu portalu"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b561a210-ed99-4ab4-be06-b49215e3255a
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: 650f26d19615d27a94f3947aad7b7904b6c1fabc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-with-web-application-firewall-by-using-the-portal"></a>Utwórz bramę aplikacji z zapory aplikacji sieci web przy użyciu portalu

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Interfejs wiersza polecenia platformy Azure](application-gateway-web-application-firewall-cli.md)

Dowiedz się, jak utworzyć bramę aplikacji włączona jest Zapora aplikacji sieci web.

Zapora aplikacji sieci web (WAF) w brama aplikacji w usłudze Azure chroni aplikacje sieci web przed wspólnej ataków opartych na sieci web takich jak iniekcja kodu SQL, atakami skryptów między witrynami i hijacks sesji. Aplikacja sieci Web chroni przed wiele OWASP top 10 wspólnej sieci web luk w zabezpieczeniach.

## <a name="scenarios"></a>Scenariusze

W tym artykule istnieją dwa scenariusze:

Z pierwszego scenariusza, dowiesz się [Utwórz bramę aplikacji z zapory aplikacji sieci web](#create-an-application-gateway-with-web-application-firewall)

W drugim scenariuszu dowiesz się, aby [Dodawanie zapory aplikacji sieci web do istniejącej bramy aplikacji](#add-web-application-firewall-to-an-existing-application-gateway).

![Przykładowy scenariusz][scenario]

> [!NOTE]
> Dodatkowa konfiguracja bramy aplikacji, w tym kondycji niestandardowych sondy, adresy w puli zaplecza i dodatkowe reguły są konfigurowane po skonfigurowaniu bramy aplikacji i nie podczas pierwszego wdrożenia.

## <a name="before-you-begin"></a>Przed rozpoczęciem

Brama aplikacji w Azure wymaga jego własnej podsieci. Podczas tworzenia sieci wirtualnej, upewnij się, że pozostanie wystarczająco dużo przestrzeni adresowej do mają wiele podsieci. Po wdrożono bramę aplikacji do podsieci bramy aplikacji tylko dodatkowe mogą mają zostać dodane do tej podsieci.

##<a name="add-web-application-firewall-to-an-existing-application-gateway"></a>Dodawanie zapory aplikacji sieci web do istniejącej bramy aplikacji

W tym przykładzie aktualizuje istniejącą bramę aplikacji do obsługi w trybie zapobiegania zapory aplikacji sieci web.

1. W okienku **Ulubione** witryny Azure Portal kliknij pozycję **Wszystkie zasoby**. Kliknij istniejącą bramę aplikacji w **wszystkie zasoby** bloku. Jeśli subskrypcja już ma kilka zasobów, można wprowadzić nazwę w **filtrować według nazwy...** aby łatwo uzyskać dostęp do strefy DNS.

   ![Tworzenie bramy aplikacji][1]

1. Kliknij przycisk **zapory aplikacji sieci Web** i zaktualizuj ustawienia bramy aplikacji. Po zakończeniu kliknij przycisk **Zapisz**

    Dostępne są następujące ustawienia Zaktualizuj istniejącą bramę aplikacji do obsługi zapory aplikacji sieci web:

   | **Ustawienie** | **Wartość** | **Szczegóły**
   |---|---|---|
   |**Uaktualnij do warstwy zapory aplikacji sieci Web**| Zaznaczone | To ustawienie warstwy brama aplikacji w warstwie zapory aplikacji sieci Web.|
   |**Stan zapory**| Enabled (Włączony) | To ustawienie umożliwia włączenie zapory na zapory aplikacji sieci Web.|
   |**Trybie zapory** | Zapobieganie | To ustawienie jest sposób obsługi zapory aplikacji sieci web z szkodliwy ruch. **Wykrywanie** tryb tylko dzienniki zdarzeń, gdy **zapobiegania** tryb dzienniki zdarzeń i zatrzymuje szkodliwy ruch.|
   |**Zestaw reguł**|3.0|To ustawienie określa [podstawowego zestawu reguł](application-gateway-web-application-firewall-overview.md#core-rule-sets) używany do ochrony członków puli wewnętrznej bazy danych.|
   |**Konfigurowanie reguł wyłączone**|Zmienia się|Aby uniknąć możliwych fałszywych alarmów, to ustawienie umożliwia wyłączanie niektórych [reguł i grup reguł](application-gateway-crs-rulegroups-rules.md).|

    >[!NOTE]
    > Podczas uaktualniania istniejącą bramę aplikacji do jednostki SKU zapory aplikacji sieci Web, rozmiar jednostki SKU zmienia się na **średni**. Można go ponownie skonfigurować, po zakończeniu konfiguracji.

    ![Ustawienia podstawowe przedstawiający bloku][2-1]

    > [!NOTE]
    > Aby wyświetlić dzienniki zapory aplikacji sieci web, można włączyć diagnostyki i wybrać ApplicationGatewayFirewallLog. Liczba wystąpień 1 można wybrać do celów testowych. Jest ważne dowiedzieć się, że dowolnej liczby wystąpień w obszarze dwa wystąpienia nie pasuje do żadnego umowy SLA i dlatego nie zaleca się. Małe bramy nie są dostępne, korzystając z zapory aplikacji sieci web.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Utwórz bramę aplikacji z zapory aplikacji sieci web

W tym scenariuszu obejmują:

* Utwórz bramę aplikacji zapory aplikacji sieci web średnie z dwoma wystąpieniami.
* Tworzenie sieci wirtualnej o nazwie AdatumAppGatewayVNET z zarezerwowanym blokiem CIDR 10.0.0.0/16.
* Tworzenie podsieci o nazwie Appgatewaysubnet używającej bloku 10.0.0.0/28 jako bloku CIDR.
* Konfigurowanie certyfikatu dla odciążania protokołu SSL.

1. Zaloguj się do witryny [Azure Portal](https://portal.azure.com). Jeśli nie masz już konto, możesz zarejestrować się w celu [bezpłatna miesięczna wersja próbna](https://azure.microsoft.com/free)
1. W okienku Ulubione w portalu kliknij **nowy**
1. W bloku **Nowy** kliknij pozycję **Sieć**. W **sieci** bloku, kliknij przycisk **brama aplikacji w**, jak pokazano na poniższej ilustracji:
1. Przejdź do portalu Azure, kliknij pozycję **nowy** > **sieci** > **bramy aplikacji**

    ![Tworzenie bramy aplikacji][1]

1. W **podstawy** bloku, zostanie wyświetlone, wprowadź następujące wartości, a następnie kliknij przycisk **OK**:

   | **Ustawienie** | **Wartość** | **Szczegóły**
   |---|---|---|
   |**Nazwa**|AdatumAppGateway|Nazwa bramy aplikacji|
   |**Warstwy**|ZAPORY APLIKACJI SIECI WEB|Dostępne wartości to Standard i zapory aplikacji sieci Web. Odwiedź stronę [zapory aplikacji sieci web](application-gateway-web-application-firewall-overview.md) Aby dowiedzieć się więcej na temat zapory aplikacji sieci Web.|
   |**Rozmiar jednostki SKU**|Medium|Wybór, w przypadku wybrania warstwy standardowa jest mały, średni i duży. W przypadku wybrania warstwy zapory aplikacji sieci Web, opcje tylko są średni i duży.|
   |**Liczba wystąpień**|2|Liczba wystąpień brama aplikacji w celu zapewnienia wysokiej dostępności. Liczby wystąpień 1 należy używać tylko do celów testowych.|
   |**Subskrypcja**|[Twoja subskrypcja]|Wybierz subskrypcję, w której chcesz utworzyć bramę aplikacji.|
   |**Grupa zasobów**|**Utwórz nowy:** AdatumAppGatewayRG|Utwórz grupę zasobów. Nazwa grupy zasobów musi być unikatowa w obrębie wybranej subskrypcji. Aby dowiedzieć się więcej na temat grup zasobów, zapoznaj się z artykułem [Omówienie usługi Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups).|
   |**Lokalizacja**|Zachodnie stany USA||

   ![Ustawienia podstawowe przedstawiający bloku][2-2]

1. W **ustawienia** bloku, który jest wyświetlany w obszarze **sieci wirtualnej**, kliknij przycisk **wybierz sieć wirtualną**. W tym kroku zostanie otwarta wprowadź **sieci wirtualnej wybierz** bloku.  Kliknij przycisk **Utwórz nowy** otworzyć **Utwórz sieć wirtualną** bloku.

   ![Wybierz sieć wirtualną][2]

1. Na **bloku sieci wirtualnej Utwórz** wprowadź następujące wartości, a następnie kliknij przycisk **OK**. Ten krok powoduje zamknięcie **Utwórz sieć wirtualną** i **sieci wirtualnej wybierz** bloków. Spowoduje to wypełnienie **podsieci** na **ustawienia** blok podsieci wybrany.

   |**Ustawienie** | **Wartość** | **Szczegóły** |
   |---|---|---|
   |**Nazwa**|AdatumAppGatewayVNET|Nazwa bramy aplikacji|
   |**Przestrzeń adresów**|10.0.0.0/16| Ta wartość jest przestrzeni adresowej dla sieci wirtualnej|
   |**Nazwa podsieci**|AppGatewaySubnet|Nazwa podsieci bramy aplikacji|
   |**Zakres adresów podsieci**|10.0.0.0/28 | Ta podsieć umożliwia więcej dodatkowe podsieci w sieci wirtualnej dla członków puli wewnętrznej bazy danych|

1. Na **ustawienia** bloku w obszarze **konfiguracji IP frontonu**, wybierz **publicznego** jako **typ adresu IP**

1. Na **ustawienia** bloku w obszarze **publicznego adresu IP**, kliknij przycisk **wybierz publiczny adres IP**, ten krok powoduje otwarcie **wybierz publiczny adres IP** blok, kliknij przycisk **Utwórz nowy**.

   ![Wybierz publiczny adres ip][3]

1. Na **tworzenie publicznego adresu IP** bloku, zaakceptuj wartość domyślną, a następnie kliknij przycisk **OK**. Ten krok powoduje zamknięcie **wybierz publiczny adres IP** bloku **tworzenie publicznego adresu IP** bloku i wypełnić **publicznego adresu IP** z wybranego publicznego adresu IP.

1. Na **ustawienia** bloku w obszarze **konfiguracji odbiornika**, kliknij przycisk **HTTP** w obszarze **protokołu**. Aby użyć **https**, wymagany jest certyfikat. Klucz prywatny certyfikatu jest wymagane, eksportowania pliku PFX certyfikatu trzeba podać i hasło dla pliku.

1. Skonfiguruj **WAF** określonych ustawień.

   |**Ustawienie** | **Wartość** | **Szczegóły** |
   |---|---|---|
   |**Stan zapory**| Enabled (Włączony)| To ustawienie włącza zapory aplikacji sieci Web lub wyłącz.|
   |**Trybie zapory** | Zapobieganie| To ustawienie określa, że WAF akcje przejmuje szkodliwy ruch. Jeśli **wykrywania** wybrano ruchu tylko jest rejestrowane.  Jeśli **zapobiegania** wybrano, ruch jest rejestrowane i została zatrzymana z nieautoryzowanego odpowiedź 403.|


1. Znajdziesz na stronie podsumowania, a następnie kliknij przycisk **OK**.  Brama aplikacji jest teraz w kolejce, a utworzona.

1. Po utworzeniu bramy aplikacji, przejdź do niego w portalu, aby kontynuować konfigurację bramy aplikacji.

    ![Widok zasobów bramy aplikacji][10]

Te kroki Utwórz bramę aplikacji w warstwie podstawowa z domyślnych ustawień odbiornika, puli zaplecza, ustawienia http zaplecza i zasady. W przypadku zmodyfikowania ustawień do potrzeb wdrożenia po udostępnianie zakończy się pomyślnie

> [!NOTE]
> Bramy aplikacji utworzonych za pomocą konfiguracji zapory aplikacji sieci web podstawowe są skonfigurowane z CRS 3.0 do ochrony.

## <a name="next-steps"></a>Następne kroki

Następnie zostanie przedstawiony sposób skonfigurować alias domeny niestandardowej dla [publicznego adresu IP](../dns/dns-custom-domain.md#public-ip-address) przy użyciu usługi Azure DNS lub innego dostawcy usługi DNS.

Informacje o sposobie konfigurowania rejestrowania diagnostycznego do dziennika zdarzeń, które wykryte lub uniemożliwił z zapory aplikacji sieci web, odwiedzając [diagnostyki bramy aplikacji](application-gateway-diagnostics.md)

Dowiedz się, jak utworzyć sondy kondycji niestandardowych odwiedzając [utworzyć sondy kondycji niestandardowych](application-gateway-create-probe-portal.md)

Dowiedz się, jak skonfigurować odciążanie protokołu SSL i podejmij kosztowne odszyfrowywania SSL poza serwerów sieci web, odwiedzając [skonfigurować odciążanie protokołu SSL](application-gateway-ssl-portal.md)

<!--Image references-->
[1]: ./media/application-gateway-web-application-firewall-portal/figure1.png
[2]: ./media/application-gateway-web-application-firewall-portal/figure2.png
[2-1]: ./media/application-gateway-web-application-firewall-portal/figure2-1.png
[2-2]: ./media/application-gateway-web-application-firewall-portal/figure2-2.png
[3]: ./media/application-gateway-web-application-firewall-portal/figure3.png
[10]: ./media/application-gateway-web-application-firewall-portal/figure10.png
[scenario]: ./media/application-gateway-web-application-firewall-portal/scenario.png
