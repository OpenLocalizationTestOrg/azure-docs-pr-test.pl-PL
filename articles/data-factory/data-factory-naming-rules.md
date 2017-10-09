---
title: aaaRules nazewnictwa jednostek fabryki danych Azure | Dokumentacja firmy Microsoft
description: "Opisuje reguły nazewnictwa dla jednostek fabryki danych."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: bc5e801d-0b3b-48ec-9501-bb4146ea17f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 98c5fc5fc932b72b65894afad438b4dc321c8aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---naming-rules"></a>Fabryka danych Azure - reguły nazewnictwa
Witaj w poniższej tabeli zawiera reguły nazewnictwa artefaktów fabryki danych.

| Nazwa | Unikatowość nazwy | Sprawdzanie poprawności |
|:--- |:--- |:--- |
| Fabryka danych |Unikatowe w obrębie platformy Microsoft Azure. Nazwy jest rozróżniana wielkość liter, czyli `MyDF` i `mydf` można znaleźć toohello tej samej fabryki danych. |<ul><li>Każdej fabryki danych jest wiązana tooexactly jedną subskrypcją platformy Azure.</li><li>Nazwy obiektów muszą zaczynać się literą lub cyfrą i może zawierać tylko litery, cyfry i znak kreski (-) hello.</li><li>Każdy znak kreski (-) musi być od razu poprzedzone i następuje literą lub cyfrą. Następujących po sobie kresek nie są dozwolone w nazwach kontenerów.</li><li>Nazwa może być 3 do 63 znaków.</li></ul> |
| Połączonej usługi/tabel/potoki |Unikatowy o w fabryce danych. Nazwy jest rozróżniana wielkość liter. |<ul><li>Maksymalna liczba znaków w nazwie tabeli: 260.</li><li>Nazwa obiektu musi rozpoczynać się od litery, liczby lub znaku podkreślenia (_).</li><li>Następujące znaki nie są dozwolone: ".", "+","?", "/", "<", ">","*", "%", "&", ":","\\"</li></ul> |
| Grupa zasobów |Unikatowe w obrębie platformy Microsoft Azure. Nazwy jest rozróżniana wielkość liter. |<ul><li>Maksymalna liczba znaków: 1000.</li><li>Nazwa może zawierać litery, cyfry i hello następujących znaków: "-", "_",","i"."</li></ul> |

