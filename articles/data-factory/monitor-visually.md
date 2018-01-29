---
title: "Wizualne monitorować fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak monitorować wizualnie fabryki danych Azure"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2018
ms.author: shlo
ms.openlocfilehash: 97a8fa1779cd11830781528527ddfe998e0548b6
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/23/2018
---
# <a name="visually-monitor-azure-data-factories"></a>Wizualne monitorować fabryki danych Azure
Azure Data Factory to oparta na chmurze usługa integracji danych, za pomocą której możesz tworzyć oparte na danych przepływy pracy w chmurze służące do organizowania oraz automatyzowania przenoszenia i przekształcania danych. Za pomocą usługi Azure Data Factory można tworzyć oparte na danych przepływy pracy (nazywane potokami) i ustalać ich harmonogram. Te przepływy mogą pozyskiwać dane z różnych magazynów danych, przetwarzać/przekształcać je za pomocą usług obliczeniowych, takich jak Azure HDInsight Hadoop, Spark, Azure Data Lake Analytics i Azure Machine Learning, a następnie publikować dane wyjściowe w magazynach danych, np. Azure SQL Data Warehouse, do użycia przez aplikacje analizy biznesowej.
W tym szybki start dowiesz się, jak będzie monitorować potoki v2 fabryki danych bez pisania pojedynczy wiersz kodu.
Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne](https://azure.microsoft.com/free/) konto.

> [!NOTE]
> Ten artykuł dotyczy wersji 2 usługi Data Factory, która jest obecnie dostępna w wersji zapoznawczej. Jeśli używasz wersji 1 usługi fabryka danych, która jest ogólnie dostępna (GA), zobacz [monitorowanie i zarządzanie nimi potoków w fabryce danych version1](v1/data-factory-monitor-manage-app.md).

## <a name="monitor-data-factory-v2-pipelines"></a>Monitorowanie potoki v2 fabryki danych

1. Zaloguj się do [portalu Azure](https://portal.azure.com/).
2. Przejdź do bloku fabryki danych utworzonych w portalu Azure, a następnie kliknij Kafelek 'Monitor i Zarządzaj'. Spowoduje to uruchomienie ADF v2 visual funkcji monitorowania.

## <a name="list-view-monitoring"></a>Monitorowanie widok listy

Monitor potoku i działania jest uruchamiany z interfejsem widoku prostej listy. Wszystkie elementy są wyświetlane w przeglądarce lokalnej strefie czasowej. Możesz zmienić strefę czasową i wszystkie pola dat czasu spowoduje przyciąganie do wybranej strefie czasowej.  

#### <a name="monitoring-pipeline-runs"></a>Monitorowanie uruchamia potoku
Widok listy pokazujące każdego potoku uruchamiania dla Twojego potoków v2 fabryki danych. Uwzględnionych kolumn:

| **Nazwa kolumny** | **Opis** |
| --- | --- |
| Nazwa potoku | Nazwa potoku. |
| Akcje | Jednej akcji można wyświetlić uruchomień działania. |
| Początek uruchomienia | Data i godzina rozpoczęcia działania w potoku (MM/DD/RRRR GG: mm: SS AM/PM) |
| Czas trwania | Czas trwania zadania (GG) |
| Wyzwolone przez | Ręczne wyzwalacza, wyzwalacz harmonogramu |
| Stan | Nie można pomyślnie w toku |
| Parametry | Potok Uruchom parametrów (nazwa, wartość pary) |
| Błąd | Potok Uruchom błędu (jeśli/any) |
| Identyfikator uruchomienia | Identyfikator procesu, uruchom |

![Monitorowanie uruchomień potoku](media/monitor-visually/pipeline-runs.png)

#### <a name="monitoring-activity-runs"></a>Monitorowanie uruchomień działania
Widok listy pokazujące uruchomień działania odpowiadający każdej potoku uruchamiania. Kliknij przycisk **"Odbywa się działanie"** ikonę w obszarze **"Działania"** kolumnę do wyświetlenia działania jest uruchamiana dla każdego procesu uruchamiania. Uwzględnionych kolumn:

| **Nazwa kolumny** | **Opis** |
| --- | --- |
| Nazwa działania | Nazwa działania w potoku. |
| Typ działania | Typ działania tj. kopiowania, HDInsightSpark, HDInsightHive itp. |
| Początek uruchomienia | Rozpoczęcia uruchamiania działania Data i godzina (MM/DD/RRRR GG: mm: SS AM/PM) |
| Czas trwania | Czas trwania zadania (GG) |
| Stan | Nie można pomyślnie w toku |
| Dane wejściowe | Tablica JSON opisujące danych wejściowych działania |
| Dane wyjściowe | Tablica JSON opisujące danych wyjściowych działania |
| Błąd | Działanie Uruchom błędu (jeśli/any) |

![Monitorowanie uruchomień działania](media/monitor-visually/activity-runs.png)

> [!IMPORTANT]
> Musisz kliknąć przycisk **"Odśwież"** ikona u góry, aby odświeżyć listę uruchamia potoku i działania. Automatyczne odświeżanie nie jest obecnie obsługiwane.
>

![Odświeżanie](media/monitor-visually/refresh.png)

## <a name="features"></a>Funkcje

#### <a name="rich-ordering-and-filtering"></a>Kolejność bogaty i filtrowania

Kolejność potoku jest uruchamiany w desc/asc przez uruchomienie Start i potoku filtru uruchamia przez następujące kolumny:

| **Nazwa kolumny** | **Opis** |
| --- | --- |
| Nazwa potoku | Nazwa potoku. Opcje obejmują szybkie filtry "ostatnich 24 godzin", "Ostatni tydzień", "ostatnie 30 dni" lub wybierz godzinę niestandardowa data. |
| Początek uruchomienia | Data i godzina rozpoczęcia działania w potoku |
| Stan uruchomienia | Filtr działa według stanu tj zakończyło się pomyślnie, nie powiodło się, w toku |

![Filtr](media/monitor-visually/filter.png)

#### <a name="addremove-columns-to-list-view"></a>Dodaj/Usuń kolumny do widoku listy
Kliknij prawym przyciskiem myszy nagłówka widoku listy, a następnie wybierz kolumny, które mają być wyświetlane w widoku listy

![Kolumny](media/monitor-visually/columns.png)

#### <a name="reorder-column-widths-in-list-view"></a>Zmień kolejność szerokości kolumn w widoku listy
Zwiększyć i zmniejszyć szerokości kolumn w widoku listy, po prostu ustawiając kursor nad nagłówek kolumny

#### <a name="select-data-factory"></a>Wybieranie fabryki danych
Umieść wskaźnik na ikonie "Fabryki danych" u góry po lewej. Kliknij ikonę "Strzałka", aby wyświetlić listę azure fabryki subskrypcji i danych, które można monitorować.

![Wybieranie fabryki danych](media/monitor-visually/select-datafactory.png)

#### <a name="guided-tours"></a>Przewodniki z przewodnikiem
Kliknij ikonę"informacje" w lewym dolnym, a następnie kliknij przycisk "Z przewodnikiem przewodnikami", aby uzyskać instrukcje krok po kroku dotyczące monitorowania procesu i działania sekwencji.

![Przewodniki z przewodnikiem](media/monitor-visually/guided-tours.png)

#### <a name="feedback"></a>Opinia
Kliknij ikonę "Opinie", aby wysłać nam swoją opinię na różnych funkcji lub problemy, które może być zwrócone.

![Opinia](media/monitor-visually/feedback.png)

## <a name="next-steps"></a>Kolejne kroki

Zobacz [monitora i programowe zarządzanie potoki](https://docs.microsoft.com/azure/data-factory/monitor-programmatically) artykułu, aby uzyskać informacje o monitorowaniu i zarządzaniu nimi potoki
