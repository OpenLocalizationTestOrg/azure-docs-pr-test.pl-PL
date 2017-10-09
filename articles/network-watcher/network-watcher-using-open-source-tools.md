---
title: "wzorce ruchu w sieci aaaVisualize obserwatora sieciowego Azure i narzędzi typu open source | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera opis sposobu przechwytywania pakietów obserwatora sieciowego toouse z Capanalysis toovisualize ruchu wzorce tooand z maszyn wirtualnych."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 936d881b-49f9-4798-8e45-d7185ec9fe89
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fca9a226729162cd90d412c7b699ac54d2257a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-network-traffic-patterns-tooand-from-your-vms-using-open-source-tools"></a>Wizualizuj tooand wzorce ruchu sieciowego z maszyn wirtualnych za pomocą narzędzi typu open source

Przechwytywanie pakietów zawierają dane sieci, które pozwalają danych dowodowych sieci tooperform i inspekcję pakietów. Istnieją otwiera wiele narzędzia źródła można użyć tooanalyze pakiet przechwyconych obrazów toogain insights dotyczących sieci użytkownika. Jednym z takich narzędzi jest CapAnalysis, narzędzie do wizualizacji przechwytywania pakietów typu open source. Wizualizacja danych przechwytywania pakietów jest przydatna sposób tooquickly uzyskania szczegółowych informacji na wzorce i anomalii w sieci. Wizualizacje również oferują możliwość udostępniania tych wgląd w sposób łatwo dostępne.

Zawiera obserwatora sieciowego Azure hello toocapture możliwości, który przechwytuje tego cennych danych, umożliwiając tooperform pakietów w sieci. W tym artykule firma Microsoft udostępnia Przewodnik jak toovisualize i uzyskanie wgląd w dane dotyczące pakietów przechwytuje przy użyciu CapAnalysis z obserwatora sieciowego.

## <a name="scenario"></a>Scenariusz

Masz prostą aplikację sieci web wdrożone na maszynie Wirtualnej w toovisualize narzędzi typu open source toouse Azure chcesz jego tooquickly ruchu sieciowego zidentyfikować wzorce przepływu i wszelkich możliwych nieprawidłowości. Z obserwatora sieciowego można uzyskać przechwytywania pakietów, środowiska sieci i zapisz go bezpośrednio na koncie magazynu. CapAnalysis można pozyskiwania hello przechwytywania pakietów bezpośrednio z obiektu blob magazynu hello i wizualizacji jego zawartość.

![scenariusz][1]

## <a name="steps"></a>Kroki

### <a name="install-capanalysis"></a>Zainstaluj CapAnalysis

tooinstall CapAnalysis na maszynie wirtualnej, można odwoływać się instrukcje oficjalnego toohello https://www.capanalysis.net/ca/how-to-install-capanalysis tutaj.
W kolejności CapAnalysis zdalnego dostępu, potrzebujemy portu tooopen 9877 na maszynie Wirtualnej przez dodanie nowej reguły zabezpieczeń dla ruchu przychodzącego. Aby uzyskać więcej informacji o tworzeniu reguł grup zabezpieczeń sieci, można znaleźć zbyt[tworzenia reguł w istniejącej grupy NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg). Po została pomyślnie dodana reguła hello, powinno być możliwe tooaccess CapAnalysis z`http://<PublicIP>:9877`

### <a name="use-azure-network-watcher-toostart-a-packet-capture-session"></a>Użyj toostart obserwatora sieciowego Azure sesji przechwytywania pakietów

Obserwatora sieciowego umożliwia toocapture pakiety tootrack ruch do i z maszyny wirtualnej. Może się odwoływać toohello instrukcje [Przechwytywanie pakietów zarządzania z obserwatora sieciowego](network-watcher-packet-capture-manage-portal.md) toostart sesję przechwytywania pakietów. To Przechwytywanie pakietów mogą być przechowywane w toobe obiektu blob magazynu, CapAnalysis z niego.

### <a name="upload-a-packet-capture-toocapanalysis"></a>Przekaż tooCapAnalysis przechwytywania pakietów
Możesz przekazać bezpośrednio przechwytywania pakietów, wykonywaną przez obserwatora sieciowego przy użyciu karty "Z adresu URL importowania" hello i zapewnianie obiektu blob magazynu toohello łącza, gdzie przechwytywania pakietów hello jest przechowywany.

Podczas dostarczania tooCapAnalysis łącza, upewnij się, że tooappend adres URL SAS tokenu toohello magazynu obiektów blob.  toodo, przejdź tooShared sygnatury dostępu z konta magazynu hello, wyznaczyć hello uprawnienia i naciśnij klawisz toocreate przycisk Generuj SAS hello tokenu. Następnie można dodać ten token toohello pakietów przechwytywania magazynu obiektów blob adres URL SAS.

Witaj wynikowego adresu URL będzie wyglądać następująco: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere


### <a name="analyzing-packet-captures"></a>Przechwytywanie analizowania pakietów

CapAnalysis oferuje różne opcje toovisualize Twojego przechwytywania pakietów, każda udostępnienie analiza z różnych perspektyw. Te podsumowania visual możesz zrozumieć trendy ruchu sieciowego i szybko dodatkowe wszelkie nietypowe działania związane z. Niektóre z tych funkcji są wyświetlane w hello następującej listy:

1. Tabele przepływu

    Dzięki temu tabeli hello listy przepływów danych pakietów hello, hello sygnatura czasowa skojarzona z przepływami hello i hello różnych protokołów powiązanych z przepływem hello, a także źródłowego i docelowego adresu IP.

    ![Strona przepływu capanalysis][5]

1. Omówienie protokołu

    W tym okienku pozwala tooquickly Zobacz dystrybucji hello ruchu sieciowego za pośrednictwem hello różnych protokołów i lokalizacji geograficznych.

    ![Omówienie protokołu capanalysis][6]

1. Statystyki

    W tym okienku umożliwia statystyki ruchu sieciowego tooview — bajtów wysłanych i odebranych z źródłowe i docelowe adresy IP, przepływów dla każdego z hello źródłowe i docelowe adresy IP, protokół używany dla różnych przepływów i czas trwania hello przepływów.

    ![statystyki capanalysis][7]

1. geomap

    W tym okienku zawiera widoku mapy ruchu sieciowego, z kolorami skalowanie toohello ilość ruchu każdego z krajów. Możesz wybrać wyróżnione krajach tooview przepływu dodatkowe statystyki takich jak hello część danych wysłanych i odebranych z adresów IP, w tym kraju.

    ![geomap][8]

1. Filtry

    CapAnalysis zawiera zestaw filtrów do szybkiego analizy określonych pakietów. Na przykład można toofilter hello danych przez protokół toogain określonych szczegółowych informacji na ten podzestaw ruchu.

    ![filtry][11]

    Odwiedź stronę [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn więcej informacji na temat wszystkich CapAnalysis możliwości.

## <a name="conclusion"></a>Podsumowanie

Funkcja przechwytywania pakietów obserwatora sieciowego umożliwia toocapture hello danych konieczne tooperform sieci dowodowe oraz lepsze zrozumienie ruchu sieciowego. W tym scenariuszu firma Microsoft pokazano, jak przechwytywanie pakietów z obserwatora sieciowego łatwo można zintegrować z narzędzi wizualizacji typu open source. Za pomocą narzędzi typu open source, takie jak przechwytuje CapAnalysis toovisualize pakietów, możesz głębokiej inspekcji pakietów i szybkie Określanie trendów w ramach ruchu sieciowego.

## <a name="next-steps"></a>Następne kroki

toolearn więcej informacji na temat dzienniki przepływu NSG, odwiedź stronę [dzienniki przepływu NSG](network-watcher-nsg-flow-logging-overview.md)

Dowiedz się, jak toovisualize Twojego przepływu NSG dzienniki przy użyciu usługi Power BI odwiedzając [wizualizacji NSG przepływa dzienników przy użyciu usługi Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)
<!--Image references-->

[1]: ./media/network-watcher-using-open-source-tools/figure1.png
[2]: ./media/network-watcher-using-open-source-tools/figure2.png
[3]: ./media/network-watcher-using-open-source-tools/figure3.png
[4]: ./media/network-watcher-using-open-source-tools/figure4.png
[5]: ./media/network-watcher-using-open-source-tools/figure5.png
[6]: ./media/network-watcher-using-open-source-tools/figure6.png
[7]: ./media/network-watcher-using-open-source-tools/figure7.png
[8]: ./media/network-watcher-using-open-source-tools/figure8.png
[9]: ./media/network-watcher-using-open-source-tools/figure9.png
[10]: ./media/network-watcher-using-open-source-tools/figure10.png
[11]: ./media/network-watcher-using-open-source-tools/figure11.png
