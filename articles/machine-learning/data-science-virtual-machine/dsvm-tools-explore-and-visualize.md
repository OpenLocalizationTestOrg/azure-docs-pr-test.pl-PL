---
title: "Eksploracja i wizualizacja narzędzia danych - Azure | Dokumentacja firmy Microsoft"
description: "Eksploracja i wizualizacja narzędzia danych dla maszyny wirtualnej analizy danych."
keywords: "narzędzia do analizy danych, maszyny wirtualnej analizy danych, narzędzia do analizy danych, nauki danych systemu linux"
services: machine-learning
documentationcenter: 
author: bradsev
manager: cgronlun
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/11/2017
ms.author: gokuma;bradsev
ms.openlocfilehash: d8f0616f17dbaa02082492cc1c68f1d989ea5aae
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="data-exploration-and-visualization-tools-on-the-data-science-virtual-machine"></a>Eksploracja i wizualizacja narzędzia danych na maszynie wirtualnej nauki danych

Klucza etap nauki danych jest zrozumieć dane. Narzędzia Eksploracja danych i wizualizacji pomocy przyspieszanie opis danych. Poniżej przedstawiono niektóre narzędzia, pod warunkiem na DSVM faciliate tego kroku tego klucza. 

## <a name="apache-drill"></a>Apache Przechodzenie do szczegółów
|    |           |
| ------------- | ------------- |
| Co to jest?   | Aparat zapytań SQL typu open source danych Big Data    |
| DSVM obsługiwane wersje      | Windows, Linux  |
| Jak jest on skonfigurowany / zainstalowanym DSVM?      |  Zainstalowane w `/dsvm/tools/drill*` osadzonych tylko w trybie   |
| Typowe zastosowania      |  Eksploracja danych w miejscu, bez konieczności ETL. Zapytanie danych z różnych źródeł i formaty includign CSV, JSON, tabel relacyjnych, Hadoop     |
| Jak używać / uruchom go?      | Skrót na pulpicie  <br/> [Rozpoczynanie pracy z Przechodzenie do szczegółów w ciągu 10 minut](https://drill.apache.org/docs/drill-in-10-minutes/)  |
| Pokrewne narzędzia na DSVM      |   Rattle Weka, SQL Server Management Studio      |

## <a name="weka"></a>Weka
|    |           |
| ------------- | ------------- |
| Co to jest?   |  Weka jest kolekcją algorytmów uczenia maszynowego dla zadań wyszukiwania danych. Algorytmy można zastosować bezpośrednio do zestawu danych lub wywoływać w kodzie języka Java. Weka zawiera narzędzia służące do wstępnego przetwarzania danych, klasyfikacji, regresji, klaster, reguły kojarzenia i wizualizacji. |
| DSVM obsługiwane wersje     | Windows, Linux     |
| Typowe zastosowania      | Narzędzie ML ogólne     |
| Jak używać / uruchom go?      | W systemie Windows wyszukaj Weka w Start Menu. W systemie Linux, zaloguj się za pomocą X2Go, a następnie przejdź do aplikacji -> Programowanie -> Weka. |
| Łącza do próbek      | [Przykłady weka](http://www.cs.waikato.ac.nz/ml/weka/documentation.html) |
| Pokrewne narzędzia na DSVM      |Xgboost LightGBM, Rattle,   |

## <a name="rattle"></a>Rattle
|    |           |
| ------------- | ------------- |
| Co to jest?   |   Graficzny interfejs użytkownika do wyszukiwania danych przy użyciu języka R   |
| DSVM obsługiwane wersje     | Windows, Linux     |
| Typowe zastosowania      | Ogólne interfejsu użytkownika narzędzia wyszukiwania danych dla języka R    |
| Jak używać / uruchom go?      | Narzędzia interfejsu użytkownika. W systemie Windows, uruchom wiersz polecenia, uruchom R, a następnie wewnątrz R Uruchom `rattle()`. W systemie Linux, połączenie z X2Go, rozpoczęcie terminal, uruchom R, a następnie wewnątrz R Uruchom `rattle()`. |
| Łącza do próbek      | [Rattle](https://togaware.com/onepager/) |
| Pokrewne narzędzia na DSVM      |Xgboost LightGBM, Weka,   |

## <a name="powerbi-desktop"></a>Usługa Power BI Desktop 
|    |           |
| ------------- | ------------- |
| Co to jest?   | Dane interakcyjne wizualizacje i narzędzia do analizy Biznesowej    |
| DSVM obsługiwane wersje      | Windows  |
| Typowe zastosowania      |  Wizualizacja danych i tworzenie pulpitów nawigacyjnych   |
| Jak używać / uruchom go?      | Skrót na pulpicie (`C:\Program Files\Microsoft Power BI Desktop\bin\PBIDesktop.exe`)      |
| Pokrewne narzędzia na DSVM      |   Visual Studio 2017, kod programu Visual Studio, Juno      |

