---
title: "aaaHow tooview powiązane zasoby danych w usłudze Azure Data Catalog | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, w jaki sposób tooview powiązane zasoby danych w usłudze Azure Data Catalog trwałego wybranych danych."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: b69686737070ac563a0318f48e693215c605f90b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-related-data-assets-in-azure-data-catalog"></a>Jak tooview powiązane zasoby danych w usłudze Azure Data Catalog?
Wykaz danych Azure umożliwia tooview danych zasoby pokrewne tooa wybrane dane zasobów i widoku relacji między nimi. 

## <a name="supported-data-sources"></a>Obsługiwane źródła danych 
Podczas rejestrowania zasobów danych z hello następujące źródła danych usługi Azure Data Catalog automatycznie rejestruje metadane dotyczące relacji sprzężenia między hello wybrane zasobów danych. 

- Oprogramowanie SQL Server
- Usługa Azure SQL Database
- MySQL
- Oracle

## <a name="view-related-data-assets"></a>Wyświetlanie powiązanych danych zasobów
tooview zasobów danych, które są powiązane tooa wybrany zestaw danych, użyj hello **relacje** karcie pokazane na powitania po obrazu: 

![Azure Data Catalog — wyświetlanie powiązanych zasobów danych](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

W tym przykładzie są dwie relacje dla hello wybrane **ProductSubcategory** zasobu danych: 

- Kolumna ProductSubcategoryID hello produktu tabeli ma relacji klucza obcego z kolumną ProductSubcategoryID hello wybrane ProductSubcategory tabeli. 
- Kolumna ProductCategoryID hello ProductSubCategory tabeli ma relacji klucza obcego z kolumną ProductCategoryID hello wybrane ProductCategory tabeli.

> [!NOTE]
> Zwróć uwagę, kierunku hello hello strzałki w widoku drzewa relacji hello.  

toosee więcej szczegółów, takich jak hello w pełni kwalifikowana nazwa kolumny hello Przesuń hello myszy nad i wyświetlić menu podręczne toohello podobne, po obrazu: 

![Azure Data Catalog — podręczny relacji](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

tooinclude relacje między zasoby, które zostały już zarejestrowane, Zarejestruj ponownie tych zasobów.

## <a name="next-steps"></a>Następne kroki
- [Jak toomanage zasobów danych](data-catalog-how-to-manage.md)
