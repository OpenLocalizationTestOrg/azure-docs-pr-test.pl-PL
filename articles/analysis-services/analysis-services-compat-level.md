---
title: "poziom zgodności modelu aaaData w usług Azure Analysis Services | Dokumentacja firmy Microsoft"
description: "Opis poziomu zgodności modelu tabelarycznego."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/16/2017
ms.author: owend
ms.openlocfilehash: bfaf0c60666729d1e6e0baf082c046ea9faa4e86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a>Poziom zgodności dla modele tabelaryczne usług Analysis Services

*Poziom zgodności* odwołuje się zachowań określonych toorelease hello aparatu usług Analysis Services. Poziom zgodności toohello zmiany zwykle pokrywa się z główne wersje programu SQL Server. Te zmiany są również zaimplementowane w usług Azure Analysis Services toomaintain parzystości między obu platform. Zmiany poziomu zgodności dotyczy również funkcje dostępne w Twojej modeli tabelarycznych. Na przykład zapytania bezpośredniego i metadanych tabelarycznych obiektów mają implementacje różne w zależności od poziomu zgodności hello. 

Azure Analysis Services obsługuje modeli tabelarycznych przy hello 1200 i 1400 poziomy zgodności.

poziom zgodności najnowszych Hello jest 1400. Ten poziom pokrywa się z usługami analizy serwera SQL w 2017 r. Główne funkcje na poziomie zgodności 1400 hello:

*  Nowa infrastruktura dla połączenia danych, a następnie zaimportuj do modeli tabelarycznych z obsługą TOMASZ interfejsów API i skryptów TMSL. Ta nowa funkcja umożliwia obsługę dodatkowych źródeł danych takich jak magazynu obiektów Blob platformy Azure.
*  Przekształcenia danych i możliwości mashup danych za pomocą wyrażenia pobieranie danych i M.
*  Środki obsługuje właściwości wiersze szczegółów za pomocą wyrażenia języka DAX. Ta właściwość umożliwia klienta narzędzi, takich jak Microsoft Excel toodrill dół toodetailed dane zagregowane raportu. Na przykład przy przeglądaniu łączna sprzedaż dla regionu i miesiąc, można wyświetlić szczegółów zamówienia hello skojarzone. 
*  Zabezpieczenia na poziomie obiektu dla tabel i kolumn nazwy dodatkowo toohello danych w nich.
*  Rozszerzona obsługa niewyrównane hierarchie.
*  Wydajność i udoskonalenia funkcji monitorowania.
  
## <a name="set-compatibility-level"></a>Ustaw poziom zgodności 
 Podczas tworzenia nowego projektu modelu tabelarycznego programu SSDT, można określić poziom zgodności hello na powitania **Projektant modelu tabelarycznego** okna dialogowego. 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 W przypadku wybrania hello **nie pokazuj ponownie tego komunikatu** opcja, poziom zgodności hello określony jako domyślny hello użycie wszystkich kolejnych projektów. Można zmienić poziom zgodności domyślne hello programu SSDT w **narzędzia** > **opcje**.  
  
 tooupgrade istniejącego projektu modelu tabelarycznego programu SSDT, zestaw hello **poziom zgodności** właściwości w modelu hello **właściwości** okna. Zachowaj w uwadze, uaktualnienie hello poziom zgodności jest nieodwracalne.
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a>Sprawdź poziom zgodności bazy danych modelu tabelarycznego w programie SQL Server Management Studio 
 W programie SSMS, kliknij prawym przyciskiem myszy nazwę bazy danych hello > **właściwości** > **poziom zgodności**.  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a>Sprawdź obsługiwany poziom zgodności dla serwera w programie SSMS  
 W programie SSMS, kliknij prawym przyciskiem myszy nazwę serwera hello > **właściwości** > **obsługiwany poziom zgodności**.  
  
 Ta właściwość określa hello najwyższy poziom zgodności bazy danych, które zostanie uruchomione na serwerze hello (z wyjątkiem wersji zapoznawczej). Nie można zmienić poziomu zgodności Hello obsługiwane.  

## <a name="next-steps"></a>Następne kroki
  [Tworzenie modelu w portalu Azure](analysis-services-create-model-portal.md)   
  [Zarządzanie usług Analysis Services](analysis-services-manage.md)  
