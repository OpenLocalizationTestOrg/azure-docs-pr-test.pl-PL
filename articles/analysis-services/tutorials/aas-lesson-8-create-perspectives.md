---
title: "Samouczek Azure Analysis Services: lekcja 8 — tworzenie perspektyw | Microsoft Docs"
description: "Opisuje sposób tworzenia perspektyw w projekcie samouczka usług Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: Minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 09/20/2017
ms.author: owend
ms.openlocfilehash: 68f4e9744007bcf71c5b9239ecfb6f18cf0cd86e
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="lesson-8-create-perspectives"></a>Lekcja 8. Tworzenie perspektyw

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

W tej lekcji utworzysz perspektywę sprzedaży internetowej. Perspektywa definiuje możliwy do wyświetlenia podzbiór modelu, który uwzględnia ukierunkowane punkty widzenia specyficzne dla firmy lub aplikacji. Użytkownik, który połączy się z modelem przy użyciu perspektywy, zobaczy jedynie odpowiednie obiekty modelu (tabele, kolumny, miary, hierarchie i kluczowe wskaźniki wydajności) w postaci pól zdefiniowanych w danej perspektywie. Aby dowiedzieć się więcej, zobacz temat [Perspektywy](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).
  
Utworzona w tej lekcji perspektywa sprzedaży internetowej nie zawiera obiektu tabeli DimCustomer. W przypadku utworzenia perspektywy, która wyłącza określone obiekty z widoku, obiekty te nadal istnieją w modelu. Nie są one jednak widoczne na liście pól raportu klienta. Niezależnie od tego, czy kolumny obliczeniowe i miary zostały uwzględnione w perspektywie, czy też nie, odpowiadające im wartości są nadal obliczane na podstawie danych z wykluczonych obiektów.  
  
Celem tej lekcji jest przedstawienie sposobu tworzenia perspektyw i zapoznanie się z narzędziami do tworzenia modelu tabelarycznego. Jeśli model zostanie później rozszerzony w celu uwzględnienia dodatkowych tabel, możesz utworzyć dodatkowe perspektywy, np. uwzględniające punkt widzenia zapasów magazynowych i sprzedaży.  
  
Szacowany czas trwania lekcji: **5 minut**  
  
## <a name="prerequisites"></a>Wymagania wstępne  
Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności. Przed przystąpieniem do wykonywania zadań w tej lekcji należy ukończyć lekcję poprzednią: [Lekcja 7. Tworzenie kluczowych wskaźników wydajności](../tutorials/aas-lesson-7-create-key-performance-indicators.md).  
  
## <a name="create-perspectives"></a>Tworzenie perspektyw  
  
#### <a name="to-create-an-internet-sales-perspective"></a>Tworzenie perspektywy sprzedaży internetowej  
  
1.  W menu **Model** kliknij pozycje **Perspektywy** > **Utwórz i zarządzaj**.  
  
2.  W oknie dialogowym **Perspektywy** kliknij przycisk **Nowa perspektywa**.  
  
3.  Kliknij dwukrotnie nagłówek kolumny **Nowa perspektywa**, a następnie zmień nazwę na **Internet Sales** (Sprzedaż internetowa).  
  
4.  Zaznacz wszystkie tabele *z wyjątkiem* tabeli **DimCustomer**.  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    W kolejnej lekcji użyjesz funkcji Analiza w programie Excel do testowania tej perspektywy. Lista pól tabeli przestawnej programu Excel zawiera wszystkie tabele z wyjątkiem tabeli DimCustomer.  

## <a name="whats-next"></a>Co dalej?
[Lekcja 9. Tworzenie hierarchii](../tutorials/aas-lesson-9-create-hierarchies.md).
  
  
  
  
