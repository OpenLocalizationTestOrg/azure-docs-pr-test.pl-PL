---
title: "Biznesowe ciągłości i odzyskiwanie po awarii (BCDR): łączyć regiony platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o Azure regionalnych tooensure parowania, że aplikacje są odporne podczas awarii centrum danych."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: c2d0a21c-2564-4d42-991a-bc31723f61a4
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 68a3a33a8e768c72fa296d42c9ab97049232d169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="business-continuity-and-disaster-recovery-bcdr-azure-paired-regions"></a>Biznesowe ciągłości i odzyskiwanie po awarii (BCDR): łączyć regiony platformy Azure

## <a name="what-are-paired-regions"></a>Co to są skojarzone regionów?

Azure działa w wielu lokalizacji geograficznych wokół hello world. Geograficzne Azure jest zdefiniowany obszar Witaj świecie, który zawiera co najmniej jeden Region platformy Azure. Region platformy Azure jest obszar wewnątrz obiektu geograficznego, zawierający co najmniej jeden centrów danych.

Każdy region platformy Azure jest łączyć się z innego regionu w hello tej samej lokalizacji geograficznej, razem wprowadzeniem regionalnych pary. wyjątek Hello jest Brazylia Południowa, który jest łączyć się z obszarem poza jego lokalizacji geograficznej.

![AzureGeography](./media/best-practices-availability-paired-regions/GeoRegionDataCenter.png)

Rysunek 1 — diagram Azure pary regionalne

| Lokalizacja geograficzna | Sparowanego regionów |  |
|:--- |:--- |:--- |
| Azja |Azja Wschodnia |Azja Południowo-Wschodnia |
| Australia |Australia Wschodnia |Australia Południowo-Wschodnia |
| Kanada |Kanada Środkowa |Kanada Wschodnia |
| Chiny |Chiny Północne |Chiny Wschodnie|
| Indie |Indie Środkowe |Indie Południowe |
| Japonia |Japonia Wschodnia |Japonia Zachodnia |
| Korea Południowa |Korea Środkowa |Korea Południowa |
| Ameryka Północna |Środkowo-północne stany USA |Środkowo-południowe stany USA |
| Ameryka Północna |Wschodnie stany USA |Zachodnie stany USA |
| Ameryka Północna |Wschodnie stany USA 2 |Środkowe stany USA |
| Ameryka Północna |Zachodnie stany USA 2 |Środkowo-zachodnie stany USA |
| Europa |Europa Północna |Europa Zachodnia |
| Japonia |Japonia Wschodnia |Japonia Zachodnia |
| Brazylia |Brazylia Południowa (1) |Środkowo-południowe stany USA |
| Rząd USA |Administracja USA — Iowa |Administracja USA — Wirginia |
| Rząd USA |Administracja USA — Wirginia |Administracja USA — Teksas |
| Rząd USA |Administracja USA — Teksas |Administracja USA — Arizona |
| Rząd USA |Administracja USA — Arizona |Administracja USA — Teksas |
| WIELKA BRYTANIA |Zachodnie Zjednoczone Królestwo |Południowe Zjednoczone Królestwo |
| Niemcy |Niemcy Środkowe |Niemcy Północno-Wschodnie |

Tabela 1 - mapowania par regionalnych Azure

> (1) Brazylia Południowa jest unikatowa, ponieważ jest łączyć się z obszarem poza jego własnej lokalizacji geograficznej. Brazylia Południowa region pomocniczy jest południowo-środkowe stany, ale południowo-środkowe stany w regionie pomocniczym nie jest Brazylia Południowa.


Firma Microsoft zaleca replikować obciążenia między toobenefit regionalnych pary z platformy Azure zasad izolacji i dostępności. Na przykład aktualizacje planowane systemu Azure są wdrażane kolejno (nie w hello jednocześnie) w parach regionach. Oznacza to, że nawet w przypadku rzadkich hello błędny aktualizacji, obu regionów nie zostaną zmienione jednocześnie. Ponadto w przypadku mało prawdopodobnego hello szerokie awarii, priorytetu jest Odzyskiwanie co najmniej jeden region poza każdej pary.

## <a name="an-example-of-paired-regions"></a>Przykład sparowanego regionów
Poniżej na rysunku 2 przedstawiono hipotetyczny aplikacji, która używa pary regionalnych hello odzyskiwania po awarii. numery Hello zielony zaznacz działań między region hello trzy usług platformy Azure (Azure obliczeniowe magazynu i bazy danych) i jak są one skonfigurowane tooreplicate w regionach. Hello unikatowy korzyści z wdrożenia w regionach sparowanego są wyróżnione hello pomarańczowy liczbami.

![Omówienie zalet sparowanego regionu](./media/best-practices-availability-paired-regions/PairedRegionsOverview2.png)

Rysunek 2 — hipotetyczny Azure pary regionalne

## <a name="cross-region-activities"></a>Region między działaniami
Jako tooin określonego rysunek 2.

![PaaS](./media/best-practices-availability-paired-regions/1Green.png) **(PaaS) rozwiązań usługi obliczenia Azure** — należy udostępnić zasoby obliczeniowe z wyprzedzeniem tooensure zasoby są dostępne w innym regionie podczas awarii. Aby uzyskać więcej informacji, zobacz [wskazówki techniczne Azure odporności](resiliency/resiliency-technical-guidance.md).

![Magazyn](./media/best-practices-availability-paired-regions/2Green.png) **usługi Azure Storage** — magazyn geograficznie nadmiarowy (GRS) jest domyślnie skonfigurowany podczas tworzenia konta usługi Azure Storage. W wypadku magazynu GRS dane są automatycznie replikowane trzy razy w regionie podstawowym hello i trzy razy w regionie sparowanego hello. Aby uzyskać więcej informacji, zobacz [opcje nadmiarowość magazynu Azure](storage/common/storage-redundancy.md).

![Azure SQL](./media/best-practices-availability-paired-regions/3Green.png) **baz danych SQL Azure** — z usługi Azure SQL standardowa replikacja geograficzna, możesz konfigurować replikację asynchroniczną regionu sparowanego tooa transakcji. Premium replikacja geograficzna można skonfigurować replikację tooany region Witaj świecie; jednak zaleca się wdrażanie tych zasobów w regionie sparowanego większości scenariuszy odzyskiwania po awarii. Aby uzyskać więcej informacji, zobacz [— replikacja geograficzna w bazie danych SQL Azure](sql-database/sql-database-geo-replication-overview.md).

![Menedżer zasobów](./media/best-practices-availability-paired-regions/4Green.png) **usługi Azure Resource Manager** -Resource Manager zapewnia z założenia izolacji logicznej składników usługi zarządzania w regionach. Oznacza to logiczne błędów w jednym regionie są rzadziej tooimpact innego.

## <a name="benefits-of-paired-regions"></a>Korzyści sparowanego regionów
Jako tooin określonego rysunek 2.  

![Izolacja](./media/best-practices-availability-paired-regions/5Orange.png)
**fizycznych izolacji** — Jeśli to możliwe, Azure preferuje co najmniej 300 mil rozdzielenie centrów danych w parze regionalnych, chociaż nie jest praktyczne lub możliwe w wszystkich regionów geograficznych. Rozdzielenie fizycznego centrum danych zmniejsza prawdopodobieństwo hello klęski żywiołowej, unrest cywilnego, awarie zasilania lub awarie sieci fizycznej wpływających na obu regionów jednocześnie. Izolacja jest podmiotu toohello ograniczenia w obrębie geograficzne hello (rozmiar obiektu geograficznego, dostępność infrastruktury zasilania i sieci, wykonawcze itp.).  

![Replikacja](./media/best-practices-availability-paired-regions/6Orange.png)
**replikacji dostarczane przez platformę** -niektórych usług, takich jak magazyn geograficznie nadmiarowy Podaj region sparowanego toohello automatyczne replikacji.

![Odzyskiwanie](./media/best-practices-availability-paired-regions/7Orange.png)
**kolejności odzyskiwania Region** — w przypadku hello szerokie awarii odzyskiwania jeden region jest priorytety poza każdej pary. Aplikacje, które są wdrażane w regionach sparowanego dotrą toohave regionów hello odzyskane o priorytecie. Jeśli aplikacja jest wdrażana w regionach, które nie są skojarzone, odzyskiwania mogą być opóźnione — w hello najgorszy hello wielkość wybranych regionów może hello ostatnich dwóch toobe odzyskane.

![Aktualizacje](./media/best-practices-availability-paired-regions/8Orange.png)
**kolejnych aktualizacji** — aktualizacji systemu Azure planowane są rozwijane regionów toopaired sekwencyjnie (nie w hello jednocześnie) toominimize przestojów, efekt hello usterek i błędów logicznych w rzadkich hello Zły aktualizacji.

![Dane](./media/best-practices-availability-paired-regions/9Orange.png)
**siedziby danych** — region znajduje się w obrębie hello sam geograficzne jako jego pary (z wyjątkiem hello Brazylia Południowa) w kolejności toomeet danych siedziby wymagań kwota podatku i prawa celów właściwość wymuszania.
