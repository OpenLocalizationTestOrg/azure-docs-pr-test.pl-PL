---
title: aaaCreate wiele maszyn wirtualnych | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 37729fabd91049744f6bd94c55221f5c1c65d527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-multiple-azure-virtual-machines"></a>Tworzenie wielu maszyn wirtualnych platformy Azure
Istnieje wiele scenariuszy, w których należy toocreate wiele podobnych maszyn wirtualnych (VM). Oto kilka przykładów obliczeniowych wysokiej wydajności (HPC), analizy danych na dużą skalę, skalowalna i często bezstanowych serwerów warstwy środkowej lub wewnętrznej bazy danych (takich jak serwery sieci Web) i rozproszonej bazy danych.

W tym artykule omówiono hello dostępne opcje toocreate wiele maszyn wirtualnych na platformie Azure. Te opcje wykracza poza przypadków prostego powitania gdzie ręcznie tworzyć serie maszyn wirtualnych. toocreate wiele maszyn wirtualnych, procesów hello, które zwykle korzystają nie skalować dobrze, jeśli potrzebujesz toocreate więcej niż kilka maszyn wirtualnych.

Jednym ze sposobów toocreate wiele podobnych maszyn wirtualnych jest toouse hello Azure Resource Manager konstrukcja z *pętle zasobów*.

## <a name="resource-loops"></a>Pętle zasobów
Pętle zasobów są syntaktycznych skrótu w szablonach usługi Azure Resource Manager. Pętle zasobów można utworzyć zestaw zasobów, podobnie skonfigurowanym w pętli. Toocreate pętle zasobów można użyć wielu kont magazynu, interfejsy sieciowe lub maszyn wirtualnych. Aby uzyskać więcej informacji na temat pętle zasobów można znaleźć zbyt[Tworzenie maszyn wirtualnych w zestawach dostępności przy użyciu pętli zasobów](https://azure.microsoft.com/documentation/templates/201-vm-copy-index-loops/).

## <a name="challenges-of-scale"></a>Wyzwania skali
Pętle zasobów stał się łatwiejsze toobuild infrastruktury chmury na dużą skalę i utworzyć bardziej zwięzły szablony, pozostają pewne wyzwania. Na przykład jeśli używasz 100 maszyn wirtualnych zasobów pętli toocreate należy kontrolery interfejsu sieciowego toocorrelate (NIC) z odpowiednich maszyn wirtualnych i kont magazynu. Ponieważ hello liczbę maszyn wirtualnych jest prawdopodobnie toobe inny niż hello liczba kont magazynu, toodeal o rozmiarze pętli różnych zasobów, będziesz mieć zbyt. Są to solvable problemów, ale złożoność hello znacznie zwiększa się o skali.

Inne wyzwanie występuje, gdy potrzebujesz infrastrukturę, która może obsłużyć elastycznie. Na przykład można infrastrukturę automatycznego skalowania, która automatycznie zwiększa lub zmniejsza hello liczbę maszyn wirtualnych w tooworkload odpowiedzi. Maszyny wirtualne nie udostępniają mechanizm zintegrowanego toovary wiele (skalowanie w poziomie i skali w). Skala w przez usunięcie maszyn wirtualnych jest trudne tooguarantee wysokiej dostępności zapewniając równoważy maszyn wirtualnych między domenami aktualizacji i odporność.

Ponadto użycie pętli zasobów, wielu wywołań toocreate zasobów Przejdź toohello obsługującej ją sieci szkieletowej. Wiele wywołań tworzenia podobnych zasobów, Azure ma możliwość niejawnego tooimprove na ten projekt i zoptymalizować wdrożenia niezawodność i wydajność. Jest to, gdy *zestawy skalowania maszyny wirtualnej* się.

## <a name="virtual-machine-scale-sets"></a>Zestawy skalowania maszyn wirtualnych
Zestawy skalowania maszyny wirtualnej są toodeploy zasobów rozwiązań usługi obliczenia Azure i zarządzać zestawem identycznych maszyn wirtualnych. Z wszystkich maszyn wirtualnych skonfigurowanych hello takie same, zestawy skalowania maszyny Wirtualnej są łatwe tooscale w i skalowania w poziomie. Wystarczy zmienić hello liczbę maszyn wirtualnych w zestawie hello. Można również skonfigurować tooautoscale zestawy skalowania maszyny Wirtualnej zależności od potrzeb hello hello obciążenia.

W przypadku aplikacji wymagających tooscale zasoby obliczeniowe, a w skali operacji niejawnie równoważy w domenach awarii i aktualizacji.

Zamiast korelowanie wiele zasobów, takich jak karty sieciowe i maszyn wirtualnych, zestaw skali maszyny Wirtualnej ma sieci, magazynu maszyny wirtualnej i właściwości rozszerzenia, które można skonfigurować centralnie.

Dla zestawów skalowania tooVM wprowadzenie, zobacz toohello [stronę produktu zestawach skali maszyn wirtualnych](https://azure.microsoft.com/services/virtual-machine-scale-sets/). Aby uzyskać szczegółowe informacje, przejdź toohello [dokumentacji zestawach skali maszyn wirtualnych](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/).

