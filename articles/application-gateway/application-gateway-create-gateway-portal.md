---
title: "aaaCreate bramę aplikacji - portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate bramę aplikacji przy użyciu hello portalu"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 54dffe95-d802-4f86-9e2e-293f49bd1e06
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 24c1d5701eae372cd233162ceb58dea36a3b6a39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-hello-portal"></a>Tworzenie bramy aplikacji za pomocą portalu hello

[Brama aplikacji w](application-gateway-introduction.md) jest dedykowany urządzenie wirtualne udostępniające kontroler dostarczania aplikacji (ADC) jako usługa, oferty różne obciążenia warstwy 7 równoważenia możliwości aplikacji. Ten artykuł przedstawia toocreate kroki hello bramę aplikacji przy użyciu hello portalu Azure i Dodawanie istniejącego serwera jako członka wewnętrznej bazy danych.

## <a name="log-in-tooazure"></a>Zaloguj się za tooAzure

Zaloguj się za toohello portalu Azure w [http://portal.azure.com](http://portal.azure.com)

## <a name="create-application-gateway"></a>Utwórz bramę aplikacji

toocreate bramę aplikacji hello pełną kroki, które należy wykonać. Brama aplikacji wymaga jego własnej podsieci. Podczas tworzenia sieci wirtualnej, upewnij się, pozostaw toohave miejsce za mało adresów wielu podsieci. Bramy aplikacji hello po podsieci tooa wdrożone tylko inne bramy aplikacji mogą być dodawane tooit.

1. W okienku Ulubione hello hello portalu kliknij **nowy**
1. W hello **nowy** bloku, kliknij przycisk **sieci**. W hello **sieci** bloku, kliknij przycisk **brama aplikacji w**, jak pokazano w powitania po obrazu:

    ![Tworzenie bramy aplikacji][1]

1. W hello **podstawy** bloku, zostanie wyświetlone, wprowadź następujące wartości hello, a następnie kliknij **OK**:

   | **Ustawienie** | **Wartość** | **Szczegóły**|
   |---|---|---|
   |**Nazwa**|AdatumAppGateway|Nazwa Hello hello bramy aplikacji|
   |**Warstwy**|Standardowa|Dostępne wartości to Standard i zapory aplikacji sieci Web. Odwiedź stronę [zapory aplikacji sieci web](application-gateway-web-application-firewall-overview.md) toolearn więcej informacji na temat zapory aplikacji sieci Web.|
   |**Rozmiar jednostki SKU**|Medium|Wybór, w przypadku wybrania warstwy standardowa jest mały, średni i duży. W przypadku wybrania warstwy zapory aplikacji sieci Web, opcje tylko są średni i duży.|
   |**Liczba wystąpień**|2|Liczba wystąpień bramy aplikacji hello wysokiej dostępności. Liczby wystąpień 1 należy używać tylko do celów testowych.|
   |**Subskrypcja**|[Twoja subskrypcja]|Wybierz bramę aplikacji hello toocreate subskrypcji w.|
   |**Grupa zasobów**|**Utwórz nowy:** AdatumAppGatewayRG|Utwórz grupę zasobów. Nazwa grupy zasobów Hello musi być unikatowa w ramach subskrypcji hello, wybranych. więcej informacji na temat grup zasobów, przeczytaj hello toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) artykuł z omówieniem.|
   |**Lokalizacja**|Zachodnie stany USA||

1. W hello **ustawienia** bloku, który jest wyświetlany w obszarze **sieci wirtualnej**, kliknij przycisk **wybierz sieć wirtualną**. Witaj **sieci wirtualnej wybierz** zostanie otwarty blok.  Kliknij przycisk **Utwórz nowy** tooopen hello **Utwórz sieć wirtualną** bloku.

   ![Wybierz sieć wirtualną][2]

1. Na powitania **bloku sieci wirtualnej Utwórz** wprowadź hello następujące wartości, a następnie kliknij przycisk **OK**. Witaj **Utwórz sieć wirtualną** i **sieci wirtualnej wybierz** zamknąć bloków. Ten krok powoduje wypełnienie hello **podsieci** na powitania **ustawienia** blok podsieci hello wybrany.

   | **Ustawienie** | **Wartość** | **Szczegóły**|
   |---|---|---|
   |**Nazwa**|AdatumAppGatewayVNET|Nazwa bramy aplikacji hello|
   |**Przestrzeń adresów**|10.0.0.0/16|Jest to hello przestrzeni adresowej dla sieci wirtualnej hello|
   |**Nazwa podsieci**|AppGatewaySubnet|Nazwa podsieci hello hello bramy aplikacji|
   |**Zakres adresów podsieci**|10.0.0.0/28|Ta podsieć umożliwia więcej dodatkowe podsieci w sieci wirtualnej hello członków puli wewnętrznej bazy danych|

1. Na powitania **ustawienia** bloku w obszarze **konfiguracji IP frontonu**, wybierz **publicznego** jako hello **typ adresu IP**

1. Na powitania **ustawienia** bloku w obszarze **publicznego adresu IP** kliknij **wybierz publiczny adres IP**, hello **wybierz publiczny adres IP** zostanie otwarty blok , kliknij przycisk **Utwórz nowy**.

   ![Wybierz publiczny adres ip][3]

1. Na powitania **tworzenie publicznego adresu IP** bloku, zaakceptuj wartość domyślną hello, a następnie kliknij przycisk **OK**. Blok Hello zamyka i wypełnia hello **publicznego adresu IP** z hello wybranego publicznego adresu IP.

1. Na powitania **ustawienia** bloku w obszarze **konfiguracji odbiornika**, kliknij przycisk **HTTP** w obszarze **protokołu**. Wprowadź toouse portu hello w hello **portu** pola.

2. Kliknij przycisk **OK** na powitania **ustawienia** toocontinue bloku.

1. Przejrzyj ustawienia hello na powitania **Podsumowanie** bloku i kliknij przycisk **OK** toostart Tworzenie bramy aplikacji hello. Tworzenie bramy aplikacji jest długo działające zadania i Trwa toocomplete czasu.

## <a name="add-servers-toobackend-pools"></a>Dodawanie pul toobackend serwerów

Po utworzeniu bramy aplikacji hello systemy hello, obsługujące ze zrównoważonym obciążeniem toobe aplikacji hello nadal należy toobe dodano toohello aplikacji bramy. Witaj adresy IP, nazwy FQDN lub kart sieciowych z tych serwerów są dodawane pul adresów zaplecza toohello.

### <a name="ip-address-or-fqdn"></a>Adres IP lub nazwa FQDN

1. Bramy aplikacji hello utworzone w portalu Azure hello **ulubione** okienku, kliknij przycisk **wszystkie zasoby**. Kliknij przycisk hello **AdatumAppGateway** brama aplikacji w hello wszystkich bloku zasobów. Jeśli subskrypcja hello już ma kilka zasobów, możesz wprowadzić **AdatumAppGateway** w hello **filtrować według nazwy...** Brama aplikacji w polu tooeasily dostępu hello.

1. Brama aplikacji Hello utworzonego jest wyświetlany. Kliknij przycisk **pul zaplecza**i wybierz hello bieżącej puli zaplecza **appGatewayBackendPool**, hello **appGatewayBackendPool** zostanie otwarty blok.

   ![Pule zaplecza bramy aplikacji][4]

1. Kliknij przycisk **dodać docelowy** adresy IP tooadd wartości nazw FQDN. Wybierz **IP adres lub nazwa FQDN** jako hello **typu** i wprowadź adres IP lub nazwy FQDN w polu hello. Powtórz ten krok dla członków puli dodatkowych wewnętrznej bazy danych. Po zakończeniu kliknij przycisk **zapisać**.

### <a name="virtual-machine-and-nic"></a>Maszyna wirtualna i karty Sieciowej

Karty sieciowe maszyny wirtualnej można również dodać jako członków puli wewnętrznej bazy danych. Tylko maszyny wirtualne w tej samej sieci wirtualnej jako hello bramy aplikacji są dostępne za pośrednictwem hello hello listy rozwijanej.

1. Bramy aplikacji hello utworzone w portalu Azure hello **ulubione** okienku, kliknij przycisk **wszystkie zasoby**. Kliknij przycisk hello **AdatumAppGateway** brama aplikacji w hello wszystkich bloku zasobów. Jeśli subskrypcja hello już ma kilka zasobów, możesz wprowadzić **AdatumAppGateway** w hello **filtrować według nazwy...** Brama aplikacji w polu tooeasily dostępu hello.

1. Brama aplikacji Hello utworzonego jest wyświetlany. Kliknij przycisk **pul zaplecza**i wybierz hello bieżącej puli zaplecza **appGatewayBackendPool**, hello **appGatewayBackendPool** zostanie otwarty blok.

   ![Pule zaplecza bramy aplikacji][5]

1. Kliknij przycisk **dodać docelowy** adresy IP tooadd wartości nazw FQDN. Wybierz **maszyny wirtualnej** jako hello **typu** i wybierz hello maszyny wirtualnej, a toouse karty Sieciowej. Po zakończeniu kliknij przycisk **Zapisz**

   > [!NOTE]
   > Tylko maszyny wirtualne w hello tej samej sieci wirtualnej, zgodnie z bramy aplikacji hello są dostępne w polu rozwijanym hello.

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Gdy nie są już potrzebne, należy usunąć hello grupy zasobów, bramę aplikacji i wszystkie powiązane zasoby. toodo tak, wybierz grupę zasobów hello bloku bramy aplikacji hello i kliknij przycisk **usunąć**.

## <a name="next-steps"></a>Następne kroki

W tym scenariuszu wdrożyć bramę aplikacji i dodać toohello serwera wewnętrznej bazy danych. Następne kroki Hello są bramy aplikacji hello tooconfigure modyfikowania ustawień i dostosowywanie reguły w hello bramy. Te kroki można znaleźć, przechodząc na stronę hello następujące artykuły:

Dowiedz się, jak sondy kondycji niestandardowych toocreate odwiedzając [utworzyć sondy kondycji niestandardowych](application-gateway-create-probe-portal.md)

Dowiedz się, jak tooconfigure odciążanie protokołu SSL i kosztowne odszyfrowywania SSL podjęcia hello wyłączone serwerów sieci web, odwiedzając [skonfigurować odciążanie protokołu SSL](application-gateway-ssl-portal.md)

Dowiedz się, jak tooprotect aplikacji przy użyciu [zapory aplikacji sieci Web](application-gateway-webapplicationfirewall-overview.md) funkcji bramy aplikacji.

<!--Image references-->
[1]: ./media/application-gateway-create-gateway-portal/figure1.png
[2]: ./media/application-gateway-create-gateway-portal/figure2.png
[3]: ./media/application-gateway-create-gateway-portal/figure3.png
[4]: ./media/application-gateway-create-gateway-portal/figure4.png
[5]: ./media/application-gateway-create-gateway-portal/figure5.png
[scenario]: ./media/application-gateway-create-gateway-portal/scenario.png
