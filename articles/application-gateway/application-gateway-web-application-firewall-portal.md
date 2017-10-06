---
title: "aaaCreate lub zaktualizuj bramę aplikacji Azure z zapory aplikacji sieci web | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate bramę aplikacji z zapory aplikacji sieci web przy użyciu hello portalu"
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
ms.openlocfilehash: 68d140fef14499da654ea251d1208e6a800f55a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-web-application-firewall-by-using-hello-portal"></a>Utwórz bramę aplikacji z zapory aplikacji sieci web przy użyciu portalu hello

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Interfejs wiersza polecenia platformy Azure](application-gateway-web-application-firewall-cli.md)

Dowiedz się, jak toocreate zapory aplikacji sieci web włączone bramy aplikacji.

Hello zapory aplikacji sieci web (WAF) brama aplikacji w usłudze Azure chroni aplikacje sieci web przed wspólnej ataków opartych na sieci web takich jak iniekcja kodu SQL, ataki skryptów między witrynami i hijacks sesji. Aplikacja sieci Web chroni przed wiele hello OWASP top 10 wspólnej sieci web luk w zabezpieczeniach.

## <a name="scenarios"></a>Scenariusze

W tym artykule istnieją dwa scenariusze:

W hello pierwszego scenariusza, możesz dowiedzieć się zbyt[Utwórz bramę aplikacji z zapory aplikacji sieci web](#create-an-application-gateway-with-web-application-firewall)

W drugim scenariuszu hello, możesz dowiedzieć się zbyt[dodawania bramy sieci web aplikacji zapory tooan istniejących aplikacji](#add-web-application-firewall-to-an-existing-application-gateway).

![Przykładowy scenariusz][scenario]

> [!NOTE]
> Dodatkowa konfiguracja bramy aplikacji hello, w tym kondycji niestandardowych sondy, adresy w puli zaplecza i dodatkowe reguły są konfigurowane po skonfigurowaniu bramy aplikacji hello i nie podczas pierwszego wdrożenia.

## <a name="before-you-begin"></a>Przed rozpoczęciem

Brama aplikacji w Azure wymaga jego własnej podsieci. Podczas tworzenia sieci wirtualnej, upewnij się, pozostaw toohave miejsce za mało adresów wielu podsieci. Po wdrożeniu tooa podsieci bramy aplikacji jedynymi dodatkowymi aplikacji bramy są toobe można dodać podsieci toohello.

##<a name="add-web-application-firewall-to-an-existing-application-gateway"></a>Dodawanie sieci web aplikacji zapory tooan istniejącej bramy aplikacji

W tym przykładzie aktualizuje istniejącą aplikację bramy toosupport zapory aplikacji sieci web w trybie zapobiegania.

1. W portalu Azure hello **ulubione** okienku, kliknij przycisk **wszystkie zasoby**. Kliknij przycisk hello istniejącą bramę aplikacji w hello **wszystkie zasoby** bloku. Jeśli subskrypcja hello już ma kilka zasobów, można wprowadzić nazwę hello w hello **filtrować według nazwy...** Witaj strefy DNS pole tooeasily dostępu.

   ![Tworzenie bramy aplikacji][1]

1. Kliknij przycisk **zapory aplikacji sieci Web** i zaktualizuj ustawienia bramy aplikacji hello. Po zakończeniu kliknij przycisk **Zapisz**

    Witaj tooupdate ustawień istniejącej aplikacji bramy toosupport zapory aplikacji sieci web są:

   | **Ustawienie** | **Wartość** | **Szczegóły**
   |---|---|---|
   |**Uaktualnij tooWAF warstwy**| Zaznaczone | To ustawienie warstwy hello hello aplikacji bramy toohello zapory aplikacji sieci Web warstwy.|
   |**Stan zapory**| Enabled (Włączony) | To ustawienie umożliwia włączenie zapory hello na powitania zapory aplikacji sieci Web.|
   |**Trybie zapory** | Zapobieganie | To ustawienie jest sposób obsługi zapory aplikacji sieci web z szkodliwy ruch. **Wykrywanie** tryb tylko dzienniki zdarzeń hello, gdzie **zapobiegania** tryb rejestruje zdarzenia hello i zatrzymuje hello szkodliwy ruch.|
   |**Zestaw reguł**|3.0|To ustawienie określa hello [podstawowego zestawu reguł](application-gateway-web-application-firewall-overview.md#core-rule-sets) czyli używane tooprotect hello zaplecza członków puli.|
   |**Konfigurowanie reguł wyłączone**|Zmienia się|tooprevent możliwe fałszywych alarmów, to ustawienie pozwala toodisable niektórych [reguł i grup reguł](application-gateway-crs-rulegroups-rules.md).|

    >[!NOTE]
    > W przypadku uaktualniania istniejącego toohello bramy aplikacji SKU zapory aplikacji sieci Web, hello SKU rozmiaru zmiany zbyt**średni**. Można go ponownie skonfigurować, po zakończeniu konfiguracji.

    ![Ustawienia podstawowe przedstawiający bloku][2-1]

    > [!NOTE]
    > musi być włączona dzienniki zapory aplikacji sieci web tooview, diagnostyki i wybrać ApplicationGatewayFirewallLog. Liczba wystąpień 1 można wybrać do celów testowych. Ważne jest tooknow, że wszystkie wystąpienia liczba wystąpień w dwóch nie pasuje do żadnego hello umowy dotyczącej poziomu usług i dlatego nie zaleca się. Małe bramy nie są dostępne, korzystając z zapory aplikacji sieci web.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Utwórz bramę aplikacji z zapory aplikacji sieci web

W tym scenariuszu obejmują:

* Utwórz bramę aplikacji zapory aplikacji sieci web średnie z dwoma wystąpieniami.
* Tworzenie sieci wirtualnej o nazwie AdatumAppGatewayVNET z zarezerwowanym blokiem CIDR 10.0.0.0/16.
* Tworzenie podsieci o nazwie Appgatewaysubnet używającej bloku 10.0.0.0/28 jako bloku CIDR.
* Konfigurowanie certyfikatu dla odciążania protokołu SSL.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com). Jeśli nie masz już konto, możesz zarejestrować się w celu [bezpłatna miesięczna wersja próbna](https://azure.microsoft.com/free)
1. W okienku Ulubione hello hello portalu kliknij **nowy**
1. W hello **nowy** bloku, kliknij przycisk **sieci**. W hello **sieci** bloku, kliknij przycisk **brama aplikacji w**, jak pokazano w powitania po obrazu:
1. Przejdź toohello portalu Azure, kliknij pozycję **nowy** > **sieci** > **bramy aplikacji**

    ![Tworzenie bramy aplikacji][1]

1. W hello **podstawy** bloku, zostanie wyświetlone, wprowadź następujące wartości hello, a następnie kliknij **OK**:

   | **Ustawienie** | **Wartość** | **Szczegóły**
   |---|---|---|
   |**Nazwa**|AdatumAppGateway|Nazwa Hello hello bramy aplikacji|
   |**Warstwy**|ZAPORY APLIKACJI SIECI WEB|Dostępne wartości to Standard i zapory aplikacji sieci Web. Odwiedź stronę [zapory aplikacji sieci web](application-gateway-web-application-firewall-overview.md) toolearn więcej informacji na temat zapory aplikacji sieci Web.|
   |**Rozmiar jednostki SKU**|Medium|Wybór, w przypadku wybrania warstwy standardowa jest mały, średni i duży. W przypadku wybrania warstwy zapory aplikacji sieci Web, opcje tylko są średni i duży.|
   |**Liczba wystąpień**|2|Liczba wystąpień bramy aplikacji hello wysokiej dostępności. Liczby wystąpień 1 należy używać tylko do celów testowych.|
   |**Subskrypcja**|[Twoja subskrypcja]|Wybierz bramę aplikacji hello toocreate subskrypcji w.|
   |**Grupa zasobów**|**Utwórz nowy:** AdatumAppGatewayRG|Utwórz grupę zasobów. Nazwa grupy zasobów Hello musi być unikatowa w ramach subskrypcji hello, wybranych. więcej informacji na temat grup zasobów, przeczytaj hello toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) artykuł z omówieniem.|
   |**Lokalizacja**|Zachodnie stany USA||

   ![Ustawienia podstawowe przedstawiający bloku][2-2]

1. W hello **ustawienia** bloku, który jest wyświetlany w obszarze **sieci wirtualnej**, kliknij przycisk **wybierz sieć wirtualną**. W tym kroku zostanie otwarta wprowadź hello **sieci wirtualnej wybierz** bloku.  Kliknij przycisk **Utwórz nowy** tooopen hello **Utwórz sieć wirtualną** bloku.

   ![Wybierz sieć wirtualną][2]

1. Na powitania **bloku sieci wirtualnej Utwórz** wprowadź hello następujące wartości, a następnie kliknij przycisk **OK**. Ten krok powoduje zamknięcie hello **Utwórz sieć wirtualną** i **sieci wirtualnej wybierz** bloków. Spowoduje to wypełnienie hello **podsieci** na powitania **ustawienia** blok podsieci hello wybrany.

   |**Ustawienie** | **Wartość** | **Szczegóły** |
   |---|---|---|
   |**Nazwa**|AdatumAppGatewayVNET|Nazwa bramy aplikacji hello|
   |**Przestrzeń adresów**|10.0.0.0/16| Ta wartość jest hello przestrzeni adresowej dla sieci wirtualnej hello|
   |**Nazwa podsieci**|AppGatewaySubnet|Nazwa podsieci hello hello bramy aplikacji|
   |**Zakres adresów podsieci**|10.0.0.0/28 | Ta podsieć umożliwia więcej dodatkowe podsieci w sieci wirtualnej hello członków puli wewnętrznej bazy danych|

1. Na powitania **ustawienia** bloku w obszarze **konfiguracji IP frontonu**, wybierz **publicznego** jako hello **typ adresu IP**

1. Na powitania **ustawienia** bloku w obszarze **publicznego adresu IP**, kliknij przycisk **wybierz publiczny adres IP**, ten krok powoduje otwarcie hello **wybierz publiczny adres IP**bloku, kliknij przycisk **Utwórz nowy**.

   ![Wybierz publiczny adres ip][3]

1. Na powitania **tworzenie publicznego adresu IP** bloku, zaakceptuj wartość domyślną hello, a następnie kliknij przycisk **OK**. Ten krok powoduje zamknięcie hello **wybierz publiczny adres IP** bloku, hello **tworzenie publicznego adresu IP** bloku i wypełnić **publicznego adresu IP** z hello wybranego publicznego adresu IP.

1. Na powitania **ustawienia** bloku w obszarze **konfiguracji odbiornika**, kliknij przycisk **HTTP** w obszarze **protokołu**. toouse **https**, wymagany jest certyfikat. Witaj klucza prywatnego certyfikatu hello jest potrzebne, dlatego do eksportu pliku PFX certyfikatu hello musi podać toobe i hello hasło dla pliku hello.

1. Skonfiguruj hello **WAF** określonych ustawień.

   |**Ustawienie** | **Wartość** | **Szczegóły** |
   |---|---|---|
   |**Stan zapory**| Enabled (Włączony)| To ustawienie włącza zapory aplikacji sieci Web lub wyłącz.|
   |**Trybie zapory** | Zapobieganie| To ustawienie określa akcje hello zapory aplikacji sieci Web przejmuje szkodliwy ruch. Jeśli **wykrywania** wybrano ruchu tylko jest rejestrowane.  Jeśli **zapobiegania** wybrano, ruch jest rejestrowane i została zatrzymana z nieautoryzowanego odpowiedź 403.|


1. Znajdziesz na stronie podsumowania hello, a następnie kliknij przycisk **OK**.  Brama aplikacji hello jest teraz w kolejce, a utworzony.

1. Po utworzeniu bramy aplikacji hello Przejdź tooit w konfiguracji portalu toocontinue hello hello bramy aplikacji.

    ![Widok zasobów bramy aplikacji][10]

Te kroki Utwórz bramę aplikacji w warstwie podstawowa z domyślnych ustawień odbiornika hello, puli zaplecza, ustawienia http zaplecza i zasady. Można modyfikować tych ustawień toosuit wdrożenia po hello inicjowania obsługi administracyjnej zakończy się pomyślnie

> [!NOTE]
> Bramy aplikacji utworzonych za pomocą konfiguracji zapory aplikacji sieci web podstawowe hello są skonfigurowane z CRS 3.0 do ochrony.

## <a name="next-steps"></a>Następne kroki

Następnie możesz dowiedzieć się jak tooconfigure alias domeny niestandardowej dla hello [publicznego adresu IP](../dns/dns-custom-domain.md#public-ip-address) przy użyciu usługi Azure DNS lub innego dostawcy usługi DNS.

Dowiedz się, jak tooconfigure rejestrowania diagnostycznego, toolog hello zdarzenia, które są wykrywane lub zapobiec za pomocą zapory aplikacji sieci web, odwiedzając [diagnostyki bramy aplikacji](application-gateway-diagnostics.md)

Dowiedz się, jak sondy kondycji niestandardowych toocreate odwiedzając [utworzyć sondy kondycji niestandardowych](application-gateway-create-probe-portal.md)

Dowiedz się, jak tooconfigure odciążanie protokołu SSL i kosztowne odszyfrowywania SSL podjęcia hello wyłączone serwerów sieci web, odwiedzając [skonfigurować odciążanie protokołu SSL](application-gateway-ssl-portal.md)

<!--Image references-->
[1]: ./media/application-gateway-web-application-firewall-portal/figure1.png
[2]: ./media/application-gateway-web-application-firewall-portal/figure2.png
[2-1]: ./media/application-gateway-web-application-firewall-portal/figure2-1.png
[2-2]: ./media/application-gateway-web-application-firewall-portal/figure2-2.png
[3]: ./media/application-gateway-web-application-firewall-portal/figure3.png
[10]: ./media/application-gateway-web-application-firewall-portal/figure10.png
[scenario]: ./media/application-gateway-web-application-firewall-portal/scenario.png
