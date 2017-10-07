---
title: "rejestruje aaaVisualizing przepływu grupy zabezpieczeń sieci Azure przy użyciu usługi Power BI | Dokumentacja firmy Microsoft"
description: "Na tej stronie opisano sposób rejestrowania toovisualize NSG przepływu z usługi Power BI."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 1e4f95fa-f5f0-4e03-bc25-008fbfc4934c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d9adcf256df8fed68c39be1a026ca64cc6b5c6d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a>Dzienniki przepływu visualizing sieciową grupę zabezpieczeń z usługi Power BI

Grupy zabezpieczeń sieci przepływu dzienniki pozwalają tooview informacje na temat przychodzące i wychodzące ruchu IP na grupy zabezpieczeń sieci. Te dzienniki przepływu Pokaż wychodzących i przepływów przychodzących na podstawie reguł na, hello kart hello przepływu dotyczy, 5-elementowej informacji na temat przepływu hello (źródłowego i docelowego adresu IP, portu źródłowego i docelowego protokołu), i jeśli ruch hello został dozwolony lub niedozwolony.

Może być trudne toogain wgląd w informacje rejestrowania danych przez ręcznie wyszukiwania plików dziennika hello przepływu. W tym artykule udostępniamy toovisualize rozwiązania z najnowszych przepływ dzienniki i Dowiedz się więcej o ruchu w sieci.

## <a name="scenario"></a>Scenariusz

Powitania od scenariusza połączymy konto magazynu pulpitu toohello usługi Power BI, którego możemy skonfigurowano jako hello odbioru dla grupy NSG przepływu rejestrowania danych. Po połączymy tooour konta magazynu usługi Power BI pobiera i analizuje tooprovide dzienniki hello wizualną reprezentację hello ruchu, który jest rejestrowane przez grup zabezpieczeń sieci.

Przy użyciu elementów wizualnych hello podane w szablonie hello, który można sprawdzić:

* Górny Talkers
* Czas serii przepływu danych decyzją kierunek i reguły
* Przepływy według adresu MAC interfejsu sieciowego
* Przepływy NSG i reguły
* Przepływy przez Port docelowy

dostarczonego szablonu Hello jest edytowalny, więc można modyfikować tooadd nowe dane, elementy wizualne, lub edytowanie zapytań toosuit potrzeb.

## <a name="setup"></a>Konfiguracja

Przed rozpoczęciem, musi mieć sieci grupy przepływu rejestrowanie zabezpieczeń włączone w jednej lub wielu grup zabezpieczeń sieci na Twoim koncie. Instrukcje dotyczące włączania zabezpieczenia sieci przepływu dzienniki, można znaleźć toohello poniższego artykułu: [wprowadzenie tooflow rejestrowania dla grup zabezpieczeń sieci](network-watcher-nsg-flow-logging-overview.md).

Musi mieć również hello Power BI Desktop zainstalowanego klienta na komputerze i wystarczającej ilości wolnego miejsca na maszynie toodownload obciążenia hello dziennika danych i czy istnieje na koncie magazynu.

![Diagram programu Visio][1]

### <a name="steps"></a>Kroki

1. Pobierz i otwórz hello następującego szablonu usługi Power BI w programie Power BI Desktop aplikacji hello [przepływu PowerBI obserwatora sieciowego rejestruje szablonu](https://aka.ms/networkwatcherpowerbiflowlogstemplate)
1. Wprowadź hello wymaganych parametrów zapytania
    1. **StorageAccountName** — Określa nazwę toohello hello konta magazynu zawierającego przepływ NSG hello dzienniki, które chcesz tooload i wizualizacji.
    1. **NumberOfLogFiles** — określa hello liczbę plików dziennika, że chcesz toodownload i wizualizacji w usłudze Power BI. Na przykład jeśli określono 50, hello 50 najnowszych plików dziennika. Mamy 2 grup NSG FF włączona i skonfigurowana toosend NSG przepływu dzienniki toothis konta, a następnie hello ostatnich 25 godzin dzienników mogą być wyświetlane.

    ![main Power BI][2]

1. Wprowadź hello klucza dostępu dla konta magazynu. Klawisze dostępu prawidłowy można znaleźć przechodząc tooyour konta magazynu w hello Azure portalu i wybierając **klucze dostępu** z menu ustawień hello. Kliknij przycisk **Connect** następnie zastosować zmiany.

    ![Klawisze dostępu][3]

    ![klucz dostępu 2][4]

4.  Dzienniki są pobrać i przeanalizować i mogą teraz wykorzystywać hello wstępnie utworzone elementy wizualne.

## <a name="understanding-hello-visuals"></a>Opis elementów wizualnych hello

Zakładając, że w hello są szablonu zbiór elementów wizualnych, które pomagają sensu hello NSG przepływu danych. Witaj poniższych ilustracjach przedstawiono przykładowe jakie pulpitu nawigacyjnego hello wygląda po wypełniane przy użyciu danych. Poniżej omówione każdego visual większej liczby szczegółów 

![Usługa Power BI][5]
 
Witaj Talkers górnej visual pokazuje hello adresów IP, zainicjowane hello większość połączeń za pośrednictwem hello podanego okresu. rozmiar Hello pól hello odpowiada toohello względną liczbę połączeń. 

![toptalkers][6]

Witaj następujące czasu serii wykresów Pokaż hello liczbę przepływów w okresie hello. Wykres górny Hello jest segmentowanych przez kierunek przepływu hello i hello niższe jest segmentem decyzją hello (Zezwalaj lub Odmów). Z tego elementu wizualnego można przejrzeć trendy ruchu wraz z upływem czasu i dodatkowe żadnych nietypowych wzrostów lub spadek ruchu lub segmentacji ruchu.

![flowsoverperiod][7]

Hello następujące wykresy wyświetlanych przepływów hello na interfejsu sieciowego, hello górny segmentowanych przez kierunek przepływu i hello niższe segmentowanych przez decyzji. Dzięki tym informacjom można uzyskać wgląd w której maszyny wirtualne przekazywane hello większości tooothers względną, a jeśli tooa ruchu określonej maszyny Wirtualnej są dozwolone lub nie.

![flowspernic][8]

powitania po wykres pierścieniowy przedstawiający koło pokazuje podział przepływów przez Port docelowy. Dzięki tym informacjom można wyświetlić hello najczęściej używane porty docelowe używane w ramach hello określony okres.

![pierścień][9]

Witaj następujące wykres słupkowy zawiera hello przepływu NSG i reguły. Dzięki tym informacjom widać hello grup NSG odpowiedzialny za hello większość ruchu sieciowego i podział hello ruchu na grupy NSG przez regułę.

![barchart][10]
 
Hello następujące informacyjną wykresy wyświetlania informacje na temat grup NSG hello znajdujących się w dziennikach hello, hello liczba przepływów przechwycone przez okres hello oraz Data hello hello dziennika najwcześniejszą przechwytywane. Ta informacja daje wyobrażenie o jakie grupy NSG są rejestrowane i hello zakres dat przepływów.

![infochart1][11]

![infochart2][12]

Ten szablon obejmuje hello następujących tooallow fragmentatory możesz tooview wyłącznie dane hello najbardziej planuje się. Można filtrować według grup zasobów, grup NSG i zasady. Można również filtrować informacji 5-elementowej, decyzji i czas hello hello dziennik został zapisany.

![fragmentatory][13]

## <a name="conclusion"></a>Podsumowanie

Firma Microsoft pokazano w tym scenariuszu czy przy użyciu dzienników przepływu grupy zabezpieczeń sieci zapewniane przez obserwatora sieciowego i usługi Power BI, firma Microsoft są w stanie toovisualize i zrozumieć hello ruchu. Przy użyciu szablonu hello podane usługi Power BI pobiera dzienniki hello bezpośrednio z magazynu i przetwarza je lokalnie. Czas poświęcony na tooload hello szablonu różni się w zależności od liczby hello żądane pliki i pobrać łączny rozmiar plików.

Możesz wolnego toocustomize tego szablonu do własnych potrzeb. Istnieje wiele sposobów wiele, że za pomocą usługi Power BI dzienniki przepływu grupy zabezpieczeń sieci. 

## <a name="notes"></a>Uwagi

* Dzienniki domyślnie są przechowywane w`https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`

    * Jeśli istnieją inne dane w innym katalogu one hello toopull zapytań i przetwarzania danych hello muszą zostać zmodyfikowane.

* Hello podany szablon nie jest zalecane używanie z dzienników z ponad 1 GB.

* Jeśli masz dużą ilość dzienniki, firma Microsoft zaleca, aby zbadać rozwiązania za pomocą innego magazynu danych, takich jak Data Lake lub SQL server.

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak toovisualize Twojego przepływu NSG dzienniki z hello Elastick stosu odwiedzając [wizualizacji tooand wzorce ruchu sieciowego z maszyn wirtualnych za pomocą narzędzi typu open source](network-watcher-using-open-source-tools.md)

[1]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure7.png
[8]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure8.png
[9]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure9.png
[10]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure10.png
[11]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure11.png
[12]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure12.png
[13]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure13.png
