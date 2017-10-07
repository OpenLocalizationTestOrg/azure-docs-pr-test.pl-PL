---
title: "geograficzne aaaConfigure ruchu metody routingu za pomocą usługi Azure Traffic Manager | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooconfigure hello metody routingu ruchu geograficzny przy użyciu usługi Azure Traffic Manager"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: 4142389211ae54e7feea6564641e01e4477491e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-geographic-traffic-routing-method-using-traffic-manager"></a>Konfigurowanie metody routingu ruchu geograficzne hello przy użyciu Menedżera ruchu

Hello metody routingu ruchu geograficzny umożliwia ruch toodirect toospecific punktów końcowych na podstawie lokalizacji geograficznej hello, których pochodzą żądania hello. Ten samouczek pokazuje, jak profilu Menedżera ruchu toocreate przy użyciu tej metody routingu i skonfiguruj hello punkty końcowe tooreceive ruchu z określonych lokalizacji geograficznych.

## <a name="create-a-traffic-manager-profile"></a>Tworzenie profilu Menedżera ruchu

1. W przeglądarce, zaloguj się toohello [portalu Azure](http://portal.azure.com). Jeśli jeszcze nie masz konta, możesz skorzystać z [bezpłatnej miesięcznej wersji próbnej](https://azure.microsoft.com/free/).
2. W menu centralnym hello, kliknij polecenie **nowy** > **sieci** > **zobaczyć wszystkie**, a następnie kliknij przycisk **profilu usługi Traffic Manager**tooopen hello **profilu usługi Traffic Manager utwórz** bloku.
3. Na powitania **profilu usługi Traffic Manager utwórz** bloku:
    1. Podaj nazwę profilu. Ta nazwa musi toobe unikatowe w obrębie hello trafficmanager.net strefy i spowoduje nazwy DNS hello <profilename>, trafficmanager.net, który będzie można tooaccess używany profil Menedżera ruchu.
    2. Wybierz hello **Geographic** metody routingu.
    3. Wybierz subskrypcję hello, który ma toocreate tego profilu.
    4. Użyj istniejącej grupy zasobów lub Utwórz nowy tooplace grupy zasobów tego profilu. Jeśli wybierzesz toocreate nową grupę zasobów, użyj hello **lokalizacja grupy zasobów** listy rozwijanej toospecify hello lokalizacji hello grupy zasobów. To ustawienie dotyczy lokalizacji toohello hello grupy zasobów i nie ma wpływu na powitania profilu Menedżera ruchu, który zostanie wdrożony globalnie.
    5. Po kliknięciu **Utwórz**, profilu usługi Traffic Manager jest tworzona i wdrażana globalnie.

![Tworzenie profilu usługi Traffic Manager](./media/traffic-manager-geographic-routing-method/create-traffic-manager-profile.png)

## <a name="add-endpoints"></a>Dodawanie punktów końcowych

1. Wyszukiwanie nazwy profilu usługi Traffic Manager hello utworzone w portalu hello pasek wyszukiwania i kliknij wynik hello podczas jego wyświetlania.
2. Przejdź za**ustawienia** -> **punktów końcowych** w hello bloku Menedżera ruchu.
3. Kliknij przycisk **Dodaj** tooshow hello **Dodawanie punktu końcowego** bloku.
3. W hello **punkty końcowe** bloku, kliknij przycisk **Dodaj** w hello **dodać punkt końcowy** bloku, który jest wyświetlany wykonania w następujący sposób:
4. Wybierz **typu** w zależności od typu hello w przypadku dodawania punktu końcowego. Geograficzne profile routingu używane w środowisku produkcyjnym zaleca się używanie typów zagnieżdżonych punkt końcowy zawierający profil podrzędnego z więcej niż jeden punkt końcowy. Aby uzyskać więcej informacji, zobacz [— często zadawane pytania o metodach routingu ruchu geograficzne](traffic-manager-FAQs.md).
5. Podaj **nazwa** za pomocą którego chcesz toorecognize tego punktu końcowego.
6. Niektóre pola, w tym bloku są zależne od typu hello punktu końcowego, który dodajesz:
    1. W przypadku dodawania punktu końcowego platformy Azure, wybierz hello **typu zasobu docelowego** i hello **docelowej** oparte na powitania zasobów ma toodirect ruchu
    2. Jeśli dodajesz **zewnętrznych** punktu końcowego, podaj hello **pełni kwalifikowaną nazwę domeny (FQDN)** dla punktu końcowego.
    3. Jeśli dodajesz **punktu końcowego zagnieżdżone**, wybierz pozycję hello **zasób docelowy** toohello podrzędne profil toouse oraz określić hello, który odpowiada **punkty końcowe podrzędnych minimalna liczba**.
7. W sekcji map geograficznych hello hello Użyj listy rozwijanej tooadd hello regionów, z której mają być punkt końcowy toothis toobe wysyłane ruchu. Należy dodać co najmniej jeden region, a może mieć wielu regionach zamapowane.
8. Powtórz tę czynność dla wszystkich punktów końcowych ma tooadd w tym profilu

![Dodawanie punktu końcowego Menedżera ruchu](./media/traffic-manager-geographic-routing-method/add-traffic-manager-endpoint.png)

## <a name="use-hello-traffic-manager-profile"></a>Użyj hello profilu Menedżera ruchu
1.  Na pasku wyszukiwania portalu hello, wyszukaj hello **profilu usługi Traffic Manager** nazwy, czy utworzony w powyższej sekcji hello, a kliknięcie hello profilu Menedżera ruchu w hello wyników tego hello wyświetlane.
2. W hello **profilu usługi Traffic Manager** bloku, kliknij przycisk **omówienie**.
3. Witaj **profilu usługi Traffic Manager** bloku Wyświetla nazwę DNS hello nowo utworzony profil Menedżera ruchu. Może to posłużyć żadnych klientów (na przykład, przechodząc opcję tooit za pomocą przeglądarki sieci web) tooget kierowane toohello prawy punkt końcowy określone przez typ routingu hello.  W przypadku hello geograficzne routingu menedżera ruchu sprawdza hello źródłowy adres IP żądania przychodzące hello i określa region hello, z którego jest pochodzących. Jeśli region jest mapowanych tooan punkt końcowy, ruch jest kierowany toothere. Jeśli ten region nie jest zmapowane tooan punktu końcowego, Traffic Manager zwraca NODATA odpowiedzi na kwerendę.

## <a name="next-steps"></a>Następne kroki

- Dowiedz się więcej o [Metoda routingu ruchu Geographic](traffic-manager-routing-methods.md#geographic).
- Dowiedz się, jak za[Menedżera ruchu ustawienia testu](traffic-manager-testing-settings.md).
