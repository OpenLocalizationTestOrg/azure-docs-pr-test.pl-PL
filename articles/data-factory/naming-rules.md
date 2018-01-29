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
ms.date: 01/16/2018
ms.author: shlo
ms.openlocfilehash: 17661f139c162f1ed22f9e186ae12bcf963e57f9
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/23/2018
---
# <a name="azure-data-factory---naming-rules"></a>Fabryka danych Azure - reguły nazewnictwa
W poniższej tabeli przedstawiono reguły nazewnictwa artefaktów fabryki danych.

> [!NOTE]
> Ten artykuł dotyczy wersji 2 usługi Data Factory, która jest obecnie dostępna w wersji zapoznawczej. Jeśli używasz wersji 1 usługi fabryka danych, która jest ogólnie dostępna (GA), zobacz [reguły w fabryce danych version1 nazewnictwa](v1/data-factory-naming-rules.md).

| Name (Nazwa) | Name Uniqueness | Sprawdzanie poprawności |
|:--- |:--- |:--- |
| Fabryka danych |Unikatowe w obrębie platformy Microsoft Azure. Nazwy jest rozróżniana wielkość liter, czyli `MyDF` i `mydf` odwoływać się do tej samej fabryki danych. |<ul><li>Każdej fabryki danych jest powiązany dokładnie jedną subskrypcją platformy Azure.</li><li>Nazwy obiektów muszą zaczynać się literą lub cyfrą i może zawierać tylko litery, cyfry i znak kreski (-).</li><li>Każdy znak kreski (-) musi być od razu poprzedzone i następuje literą lub cyfrą. Następujących po sobie kresek nie są dozwolone w nazwach kontenerów.</li><li>Nazwa może być 3 do 63 znaków.</li></ul> |
| Połączonej usługi/tabel/potoki |Unikatowy o w fabryce danych. Nazwy jest rozróżniana wielkość liter. |<ul><li>Maksymalna liczba znaków w nazwie tabeli: 260.</li><li>Nazwa obiektu musi rozpoczynać się od litery, liczby lub znaku podkreślenia (_).</li><li>Następujące znaki nie są dozwolone: ".", "+","?", "/", "<", ">","*", "%", "&", ":","\\"</li></ul> |
| Grupa zasobów |Unikatowe w obrębie platformy Microsoft Azure. Nazwy jest rozróżniana wielkość liter. |<ul><li>Maksymalna liczba znaków: 1000.</li><li>Nazwa może zawierać litery, cyfry i następujące znaki: "-", "_",","i"."</li></ul> |

## <a name="next-steps"></a>Kolejne kroki
Dowiedz się, jak można utworzyć fabryki danych, wykonując następujące instrukcje krok po kroku w [Szybki Start: tworzenie fabryki danych](quickstart-create-data-factory-powershell.md) artykułu. 