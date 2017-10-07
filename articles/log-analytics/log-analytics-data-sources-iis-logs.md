---
title: aaaIIS loguje Log Analytics | Dokumentacja firmy Microsoft
description: "Internet Information Services (IIS) są przechowywane działań użytkownika w plikach dziennika, które mogą zostać zebrane przez analizy dzienników.  W tym artykule opisano, jak tooconfigure zbierania dzienników usług IIS i szczegóły rekordów hello tworzą hello OMS repozytorium."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: cec5ff0a-01f5-4262-b2e8-e3db7b7467d2
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: bwren
ms.openlocfilehash: c5575351090cdabaf651bcb49867794ee3a4b6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="iis-logs-in-log-analytics"></a>Rejestrowania przez usługi IIS w analizy dzienników
Internet Information Services (IIS) są przechowywane działań użytkownika w plikach dziennika, które mogą zostać zebrane przez analizy dzienników.  

![Dzienniki usług IIS](media/log-analytics-data-sources-iis-logs/overview.png)

## <a name="configuring-iis-logs"></a>Konfigurowanie usług IIS dzienników
Analiza dzienników zbiera wpisy z pliki dziennika utworzone przez usługi IIS, więc należy [konfigurowania usług IIS do rejestrowania](https://technet.microsoft.com/library/hh831775.aspx).

Analiza dzienników tylko obsługuje przechowywane w formacie W3C plików dziennika usług IIS i nie obsługuje pól niestandardowych lub zaawansowanych rejestrowanie programu IIS.  
Analiza dzienników nie zbiera dzienniki w formacie native NCSA lub usług IIS.

Konfigurowanie dzienników usług IIS w analizy dzienników z hello [danych menu Ustawienia usługi Analiza dzienników](log-analytics-data-sources.md#configuring-data-sources).  Jest wymagana żadna konfiguracja innych niż wybranie **pliki dziennika w formacie W3C zbieranie IIS**.

Zaleca się, że po włączeniu zbierania dzienników usług IIS, należy skonfigurować ustawienie przerzucania dziennika usług IIS hello na każdym serwerze.

## <a name="data-collection"></a>Zbieranie danych
Analiza dzienników zbiera wpisy dziennika usług IIS z wszystkich połączonych źródeł, co 15 minut.  Hello agent rejestruje jego miejsce w każdym dzienniku zdarzeń zbierane z.  Jeśli hello agent przejdzie do trybu offline, następnie analizy dzienników zbiera dane zdarzeń z którym ostatnio przerwał, nawet jeśli te zdarzenia zostały utworzone podczas hello agent jest w trybie offline.

## <a name="iis-log-record-properties"></a>Właściwości rekordu dziennika usług IIS
Rekordy dziennika usług IIS zawiera typu **W3CIISLog** i mają właściwości hello w hello w poniższej tabeli:

| Właściwość | Opis |
|:--- |:--- |
| Computer (Komputer) |Nazwę komputera hello hello zdarzeń zostały zebrane. |
| cIP |Adres IP powitania klienta. |
| csMethod |Metoda żądania hello, takich jak GET lub POST. |
| csReferer |Lokacja tego hello użytkownika wybrane łącze toohello bieżącej lokacji. |
| csUserAgent |Typ przeglądarki powitania klienta. |
| csUserName |Nazwa hello uwierzytelniony użytkownik, który uzyskał dostęp powitania serwera. Użytkownicy anonimowi są wskazywani przez łącznik. |
| csUriStem |Obiekt docelowy żądania hello, takich jak strony sieci web. |
| csUriQuery |Zapytania, jeśli taki występuje, ten klient hello próbował tooperform. |
| ManagementGroupName |Nazwa grupy zarządzania hello agenty programu Operations Manager.  W przypadku innych agentów jest AOI -\<identyfikator obszaru roboczego\> |
| RemoteIPCountry |Kraj adres IP hello powitania klienta. |
| RemoteIPLatitude |Szerokość geograficzna adresu IP powitania klienta. |
| RemoteIPLongitude |Długość geograficzna adresu IP powitania klienta. |
| scStatus |Kod stanu HTTP. |
| scSubStatus |Kod błędu podstanu. |
| scWin32Status |Kod stanu systemu Windows. |
| sIP |Adres IP serwera sieci web hello. |
| SourceSystem |Program Operations Manager |
| sPort |Port na powitania serwera powitania klienta połączony. |
| sSiteName |Nazwa witryny usług IIS hello. |
| TimeGenerated |Data i godzina wpisu hello został zarejestrowany. |
| Właściwość timeTaken |Żądanie długość hello tooprocess czasu w milisekundach. |

## <a name="log-searches-with-iis-logs"></a>Dziennik wyszukiwania przy użyciu dzienników usług IIS
Witaj poniższej tabeli przedstawiono różne przykłady dziennika zapytań, które pobierają rekordy dziennika usług IIS.

| Zapytanie | Opis |
|:--- |:--- |
| Typ = W3CIISLog |Wszystkie rekordy dziennika usług IIS. |
| Typ = W3CIISLog scStatus = 500 |Wszystkie rekordy dziennika usług IIS o stanie zwracanych 500. |
| Typ = W3CIISLog &#124; Miara count() przez cIP |Liczba usług IIS pozycje dziennika za pomocą adresu IP klienta. |
| Typ = W3CIISLog csHost = "www.contoso.com" &#124; Miara count() przez csUriStem |Liczba usług IIS dziennika wpisy przez adres URL dla hello hosta www.contoso.com. |
| Typ = W3CIISLog &#124; Miara Sum(csBytes) przez komputer &#124; TOP 500000 |Całkowita liczba bajtów odebranych przez każdy komputer usług IIS. |

>[!NOTE]
> Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), następnie hello powyżej zapytania spowoduje zmianę następujących toohello.

> | Zapytanie | Opis |
|:--- |:--- |
| W3CIISLog |Wszystkie rekordy dziennika usług IIS. |
| W3CIISLog &#124; gdzie scStatus == 500 |Wszystkie rekordy dziennika usług IIS o stanie zwracanych 500. |
| W3CIISLog &#124; Podsumowanie funkcji count() przez cIP |Liczba usług IIS pozycje dziennika za pomocą adresu IP klienta. |
| W3CIISLog &#124; gdzie csHost == "www.contoso.com" &#124; Podsumowanie funkcji count() przez csUriStem |Liczba usług IIS dziennika wpisy przez adres URL dla hello hosta www.contoso.com. |
| W3CIISLog &#124; Podsumuj sum(csBytes) przez komputer &#124; podejmij 500000 |Całkowita liczba bajtów odebranych przez każdy komputer usług IIS. |

## <a name="next-steps"></a>Następne kroki
* Konfigurowanie analizy dzienników toocollect innych [źródeł danych](log-analytics-data-sources.md) do analizy.
* Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) tooanalyze hello dane zebrane ze źródeł danych i rozwiązań.
* Konfigurowanie alertów w analizy dzienników tooproactively informować o ważnych warunków znaleziono w dziennikach usług IIS.
