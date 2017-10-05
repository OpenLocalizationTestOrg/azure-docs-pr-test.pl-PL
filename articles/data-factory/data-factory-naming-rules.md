---
title: "Reguły nazewnictwa jednostek fabryki danych Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: d447bbceb4ab344e011311eaf143b20f0a0400d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-data-factory---naming-rules"></a>Fabryka danych Azure - reguły nazewnictwa
W poniższej tabeli przedstawiono reguły nazewnictwa artefaktów fabryki danych.

| Nazwa | Unikatowość nazwy | Sprawdzanie poprawności |
|:--- |:--- |:--- |
| Fabryka danych |Unikatowe w obrębie platformy Microsoft Azure. Nazwy jest rozróżniana wielkość liter, czyli `MyDF` i `mydf` odwoływać się do tej samej fabryki danych. |<ul><li>Każdej fabryki danych jest powiązany dokładnie jedną subskrypcją platformy Azure.</li><li>Nazwy obiektów muszą zaczynać się literą lub cyfrą i może zawierać tylko litery, cyfry i znak kreski (-).</li><li>Każdy znak kreski (-) musi być od razu poprzedzone i następuje literą lub cyfrą. Następujących po sobie kresek nie są dozwolone w nazwach kontenerów.</li><li>Nazwa może być 3 do 63 znaków.</li></ul> |
| Połączonej usługi/tabel/potoki |Unikatowy o w fabryce danych. Nazwy jest rozróżniana wielkość liter. |<ul><li>Maksymalna liczba znaków w nazwie tabeli: 260.</li><li>Nazwa obiektu musi rozpoczynać się od litery, liczby lub znaku podkreślenia (_).</li><li>Następujące znaki nie są dozwolone: ".", "+","?", "/", "<", ">","*", "%", "&", ":","\\"</li></ul> |
| Grupa zasobów |Unikatowe w obrębie platformy Microsoft Azure. Nazwy jest rozróżniana wielkość liter. |<ul><li>Maksymalna liczba znaków: 1000.</li><li>Nazwa może zawierać litery, cyfry i następujące znaki: "-", "_",","i"."</li></ul> |

