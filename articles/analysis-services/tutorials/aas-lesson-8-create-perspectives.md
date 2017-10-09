---
title: AAA "Azure Analysis Services lekcji samouczka 8 Tworzenie perspektyw | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak perspektywy toocreate hello projekt samouczka usług Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 25391813e1969ecb22af4d6f9c1ccd8358d812fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-8-create-perspectives"></a>Lekcja 8. Tworzenie perspektyw

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

W tej lekcji utworzysz perspektywę sprzedaży internetowej. Perspektywa definiuje możliwy do wyświetlenia podzbiór modelu, który uwzględnia ukierunkowane punkty widzenia specyficzne dla firmy lub aplikacji. Gdy użytkownik łączy tooa modelu za pomocą perspektywy, zostanie wyświetlona tylko obiekty modelu (tabel, kolumn, miar, hierarchie i wskaźników KPI) jako pola zdefiniowane w tym perspektywy. toolearn więcej, zobacz [perspektywy](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).
  
Witaj perspektywy sprzedaży internetowej, utworzone w tej lekcji wyklucza hello DimCustomer tabeli obiektów. Po utworzeniu perspektywę, która wyklucza niektórych obiektów z widoku obiektu nadal istnieje w modelu hello. Nie są one jednak widoczne na liście pól raportu klienta. Niezależnie od tego, czy kolumny obliczeniowe i miary zostały uwzględnione w perspektywie, czy też nie, odpowiadające im wartości są nadal obliczane na podstawie danych z wykluczonych obiektów.  
  
Celem tej lekcji Hello jest toodescribe jak perspektywy toocreate i zapoznać się z modelu tabelarycznego hello narzędzia do tworzenia. Jeśli później rozszerzyć ten model tooinclude dodatkowe tabele, możesz utworzyć dodatkowe perspektywy toodefine inny punkt widzenia hello modelu, na przykład, spisu i sprzedaży.  
  
Szacowany czas toocomplete tej lekcji: **pięć minut**  
  
## <a name="prerequisites"></a>Wymagania wstępne  
Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności. Przed wykonaniem zadania hello w tej lekcji, powinno mieć ukończone poprzedniej lekcji hello: [7 lekcji: tworzenie kluczowych wskaźników wydajności](../tutorials/aas-lesson-7-create-key-performance-indicators.md).  
  
## <a name="create-perspectives"></a>Tworzenie perspektyw  
  
#### <a name="toocreate-an-internet-sales-perspective"></a>toocreate perspektywy sprzedaży internetowej  
  
1.  Kliknij przycisk hello **modelu** menu > **perspektywy** > **Utwórz i Zarządzaj**.  
  
2.  W hello **perspektywy** okno dialogowe, kliknij przycisk **nowej perspektywy**.  
  
3.  Kliknij dwukrotnie hello **nowej perspektywy** nagłówek kolumny, a następnie zmień nazwę **sprzedaży Internet**.  
  
4.  Wybierz hello wszystkie tabele hello *z wyjątkiem* **DimCustomer**.  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    W następnej lekcji Użyj hello analizowanie w tootest funkcji programu Excel ta perspektywa. Witaj listy pól tabeli przestawnej programu Excel zawiera każdej tabeli, z wyjątkiem hello DimCustomer tabeli.  

## <a name="whats-next"></a>Co dalej?
[Lekcja 9. Tworzenie hierarchii](../tutorials/aas-lesson-9-create-hierarchies.md).
  
  
  
  
