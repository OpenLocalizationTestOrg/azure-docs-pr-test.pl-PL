---
title: aaaCreate niestandardowy pulpit nawigacyjny w Azure Log Analytics | Dokumentacja firmy Microsoft
description: "Ten przewodnik pomaga zrozumieć, jak pulpity nawigacyjne analizy dzienników można Wizualizuj wszystkie dziennika zapisanych wyszukiwań, umożliwiając pojedynczy obiektywu tooview środowiska."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: abb07f6c-b356-4f15-85f5-60e4415d0ba2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 73fcf131a91c743d473f37d5a40d52eaf78a7ba3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a>Utwórz niestandardowy pulpit nawigacyjny do użycia w analizy dzienników

>[!NOTE]
> Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), a następnie nie można utworzyć nowe pulpity nawigacyjne lub edytowanie istniejących pulpitów nawigacyjnych. 

Ten przewodnik pomaga zrozumieć, jak pulpity nawigacyjne analizy dzienników można Wizualizuj wszystkie dziennika zapisanych wyszukiwań, umożliwiając pojedynczy obiektywu tooview środowiska.

![Przykład pulpitu nawigacyjnego](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

Wszystkie hello niestandardowych pulpitów nawigacyjnych utworzonych w portalu OMS hello są także dostępne w hello OMS aplikacji mobilnej. Zobacz następujące strony, aby uzyskać więcej informacji na temat aplikacji hello hello.

* [OMS aplikacji mobilnej z hello Microsoft Store](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [OMS aplikacji mobilnej z iTunes firmy Apple](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![mobilnego pulpitu nawigacyjnego](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a>Jak utworzyć mój pulpit nawigacyjny?
toobegin, przejdź toohello strony Przegląd OMS. Zobaczysz hello **Mój pulpit nawigacyjny** kafelka powitania po lewej stronie. Kliknij go, toodrill w dół do pulpitu nawigacyjnego.

![Omówienie](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a>Dodawanie kafelka
W pulpitach nawigacyjnych Kafelki są obsługiwane przez zapisany dziennik wyszukiwania. OMS zawiera wiele wstępnie wprowadzone zapisany dziennik wyszukiwania, dzięki czemu będzie można od razu. Użyj następujących hello kroki konspektu jak toobegin.

W widoku pulpitu nawigacyjnego Moje hello, wystarczy kliknąć **Dostosuj** tooenter trybu dostosowania.

![Obrazkami](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 panel Hello, który zostanie otwarty po prawej stronie powitania hello strony są wyświetlane wszystkie obszaru roboczego zapisany dziennik wyszukiwania. toovisualize zapisany dziennik wyszukiwania jako Kafelek, umieść kursor nad zapisanego kryterium wyszukiwania, a następnie kliknij przycisk hello **plus** symbolu.

![Dodaj Kafelki 1](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

Po kliknięciu hello **plus** symboli, fragment pojawia się w hello Wyświetl mój pulpit nawigacyjny.

![Dodaj Kafelki 2](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a>Edytowanie kafelka
W widoku pulpitu nawigacyjnego Moje hello, wystarczy kliknąć **Dostosuj** tooenter trybu dostosowania. Kliknij Kafelek hello ma tooedit. Prawy panel Hello zmiany tooedit i umożliwia wybranie opcji:

![Edytowanie kafelka](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![Edytowanie kafelka](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a>Wizualizacje kafelka
Istnieją trzy rodzaje toochoose wizualizacje kafelka z:

| Typ wykresu | jaką pełni funkcję |
| --- | --- |
| ![Wykres słupkowy](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |Wyświetla oś czasu wyników wyszukiwania zapisany dziennik jako wykres słupkowy lub lista wyników według pola w zależności od, jeśli wyszukiwanie dziennika agreguje wyniki według pola, czy nie. |
| ![Metryka](./media/log-analytics-dashboards/oms-dashboards-metric.png) |Wyświetla trafień wynik wyszukiwania z całkowitej dziennika jako liczby na kafelku. Kafelki metryki pozwalają tooset wyróżnione kafelka powitania po osiągnięciu progu powitania od wartości progowej. |
| ![wiersz](./media/log-analytics-dashboards/oms-dashboards-line.png) |Wyświetla wykres liniowy osi czasu z zapisany dziennik wyszukiwania wynik trafień wartościami. |

### <a name="threshold"></a>Próg
Na kafelku, za pomocą wizualizacji metryki hello można utworzyć progu. Wybierz na toocreate na kafelku hello wartość progową. Wybierz, czy toohighlight hello kafelka, gdy wartość hello jest powyżej lub poniżej progu hello wybrany następnie ustaw wartość progowa hello poniżej.

## <a name="organizing-hello-dashboard"></a>Organizowanie hello pulpitu nawigacyjnego
tooorganize pulpitu nawigacyjnego Przejdź toohello Wyświetl mój pulpit nawigacyjny i kliknij **Dostosuj** tooenter trybu dostosowania. Kliknij i przeciągnij Kafelek hello toomove, a następnie przenieś go toowhere ma toobe Twojego kafelka.

![Organizowanie pulpitu nawigacyjnego](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a>Usuń Kafelek
tooremove kafelka, przejdź do widoku pulpitu nawigacyjnego Moje toohello i kliknij przycisk **Dostosuj** tooenter trybu dostosowania. Wybierz hello kafelka tooremove, a następnie w prawym panelu hello wybierz **usunąć kafelka**.

![Usuń Kafelek](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a>Następne kroki
* Utwórz [alerty](log-analytics-alerts.md) w powiadomieniach toogenerate analizy dzienników i tooremediate problemów.
