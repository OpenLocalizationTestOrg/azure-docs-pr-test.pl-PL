---
title: Tworzenie wielu maszyn wirtualnych | Dokumentacja firmy Microsoft
description: Opcje tworzenia wielu maszyn wirtualnych w systemie Windows
services: virtual-machines-windows
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dfc1d1bb-a47d-4d7c-9fd2-f12050baacab
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: guybo
ms.openlocfilehash: 5e96805f8880a30a5fc8779d8f07addb6d068c09
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-multiple-azure-virtual-machines"></a>Tworzenie wielu maszyn wirtualnych platformy Azure
Istnieje wiele scenariuszy, w których należy utworzyć wiele podobnych maszyn wirtualnych (VM). Oto kilka przykładów obliczeniowych wysokiej wydajności (HPC), analizy danych na dużą skalę, skalowalna i często bezstanowych serwerów warstwy środkowej lub wewnętrznej bazy danych (takich jak serwery sieci Web) i rozproszonej bazy danych.

W tym artykule opisano dostępne opcje, aby utworzyć wiele maszyn wirtualnych na platformie Azure. Te opcje wykracza poza proste przypadki, w którym ręcznie utworzyć serii maszyn wirtualnych. Aby utworzyć wiele maszyn wirtualnych, procesów, które zazwyczaj używają nie skalować również w przypadku, gdy trzeba utworzyć więcej niż kilka maszyn wirtualnych.

Jednym ze sposobów utworzyć wiele podobnych maszyn wirtualnych jest użycie konstrukcji usługi Azure Resource Manager z *pętle zasobów*.

## <a name="resource-loops"></a>Pętle zasobów
Pętle zasobów są syntaktycznych skrótu w szablonach usługi Azure Resource Manager. Pętle zasobów można utworzyć zestaw zasobów, podobnie skonfigurowanym w pętli. Pętle zasobów umożliwia utworzenie wielu kont magazynu, interfejsy sieciowe lub maszyn wirtualnych. Aby uzyskać więcej informacji na temat zasobów pętle dotyczą [Tworzenie maszyn wirtualnych w zestawach dostępności przy użyciu pętli zasobów](https://azure.microsoft.com/documentation/templates/201-vm-copy-index-loops/).

## <a name="challenges-of-scale"></a>Wyzwania skali
Mimo że pętle zasobów ułatwiają tworzenie infrastruktury chmury na dużą skalę i utworzyć bardziej zwięzły szablony, pozostają pewne wyzwania. Na przykład jeśli pętli zasobów umożliwia tworzenie 100 maszyn wirtualnych, należy do skorelowania kontrolery interfejsu sieciowego (NIC) z odpowiednich maszyn wirtualnych i kont magazynu. Ponieważ liczby maszyn wirtualnych nie może być inna niż liczba kont magazynu, będziesz mieć radzenia sobie z innego zasobu pętli rozmiary, zbyt. Są to solvable problemów, ale złożoność znacznie zwiększa się o skali.

Inne wyzwanie występuje, gdy potrzebujesz infrastrukturę, która może obsłużyć elastycznie. Na przykład można infrastrukturę automatycznego skalowania, która automatycznie zwiększa lub zmniejsza liczbę maszyn wirtualnych w odpowiedzi na obciążenie pracą. Maszyny wirtualne nie udostępniają mechanizm zintegrowane różnicującej wiele (skalowanie w poziomie i skali w). Jeśli skalować w przez usunięcie maszyn wirtualnych, trudno jest gwarantuje wysoką dostępność, zapewniając równoważy maszyn wirtualnych między domenami aktualizacji i odporność.

Na koniec korzystając z pętli zasobów, wielu wywołań utworzyć zasobów przejdź do obsługującej ją sieci szkieletowej. Wiele wywołań tworzenia podobnych zasobów, platforma Azure ma niejawne możliwość ulepszyć ten projekt i zoptymalizować wdrożenia niezawodność i wydajność. Jest to, gdy *zestawy skalowania maszyny wirtualnej* się.

## <a name="virtual-machine-scale-sets"></a>Zestawy skalowania maszyn wirtualnych
Zestawy skalowania maszyny wirtualnej są zasobami rozwiązań usługi obliczenia Azure do wdrażania i zarządzania zestaw identycznych maszyn wirtualnych. Wszystkie maszyny wirtualne skonfigurowany takie same, skalowania maszyny Wirtualnej, które zestawy są łatwe do skalowania w i skalowanie w poziomie. Wystarczy zmienić liczbę maszyn wirtualnych w zestawie. Można również skonfigurować zestawy skalowania maszyny Wirtualnej, aby stosować automatyczne skalowanie zależności od potrzeb obciążenia.

Dla aplikacji, które musi przebiegać proces skalowania zasobów obliczeniowych, wyloguj się i zaloguj wykonanie operacji skalowania niejawnie równoważy w domenach awarii i aktualizacji.

Zamiast korelowanie wiele zasobów, takich jak karty sieciowe i maszyn wirtualnych, zestaw skali maszyny Wirtualnej ma sieci, magazynu maszyny wirtualnej i właściwości rozszerzenia, które można skonfigurować centralnie.

Wprowadzenie do zestawy skalowania maszyny Wirtualnej, można znaleźć w temacie [stronę produktu zestawach skali maszyn wirtualnych](https://azure.microsoft.com/services/virtual-machine-scale-sets/). Aby uzyskać szczegółowe informacje, przejdź do [dokumentacji zestawach skali maszyn wirtualnych](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/).

