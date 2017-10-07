---
title: "toowork aaaHow ze źródłami danych danych big data | Dokumentacja firmy Microsoft"
description: "Wzorce wyróżnienia tooarticle sposób korzystania z danych big data źródeł danych, łącznie z magazynu obiektów Blob Azure, usługa Azure Data Lake i system plików HDFS Hadoop przy użyciu usługi Azure Data Catalog."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 626d1568-0780-4726-bad1-9c5000c6b31a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: e478f71f26744975a7d7e1784b74bf50b424cf65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowork-with-big-data-sources-in-azure-data-catalog"></a>Jak źródeł toowork z danymi big data w wykazie danych Azure
## <a name="introduction"></a>Wprowadzenie
**Microsoft Azure Data Catalog** to usługa w chmurze pełni zarządzana, która służy jako system rejestracji i system odnajdowania źródeł danych przedsiębiorstwa. Przede wszystkim chodzi o pomaga osób odnajdywania, zrozumienia i używania źródeł danych oraz tooget organizacje więcej korzyści z ich istniejących źródeł danych, łącznie z danymi big data.

**Wykaz danych Azure** obsługuje hello rejestracji obiektów blob Azure blogu magazynu i katalogi, a także system plików HDFS Hadoop plików i katalogów. Witaj częściowo ustrukturyzowanych rodzaj tych źródeł danych zapewnia dużą elastyczność. Jednak tooget hello największych korzyści z rejestracji je za pomocą **Azure Data Catalog**, użytkowników należy wziąć pod uwagę organizowania hello źródeł danych.

## <a name="directories-as-logical-data-sets"></a>Katalogi jako logiczne zestawów danych
Typowe wzorzec służący do organizowania źródeł danych big data jest tootreat katalogi jako logiczne zestawów danych. Katalogi najwyższego poziomu są używane toodefine zestawu danych podczas podfoldery Definiuj partycje, a same dane hello przechowywania hello pliki, które zawierają.

Przykładem tego wzorca może być:

    \vehicle_maintenance_events
        \2013
        \2014
        \2015
            \01
                \2015-01-trailer01.csv
                \2015-01-trailer92.csv
                \2015-01-canister9635.csv
                ...
    \location_tracking_events
        \2013
        ...

W tym przykładzie vehicle_maintenance_events i location_tracking_events reprezentują logiczne zestawów danych. Każdy z tych folderów zawiera pliki danych, które są zorganizowane według rok i miesiąc w podfolderach. Każdy z tych folderów potencjalnie może zawierać, setek lub tysięcy plików.

W tym wzorcu rejestrowania poszczególnych plików z **Azure Data Catalog** prawdopodobnie nie ma sensu. Zamiast tego należy zarejestrować hello katalogi, które reprezentują hello zbiory danych, które Praca z danymi hello użytkowników toohello łatwy do rozpoznania.

## <a name="reference-data-files"></a>Odwołanie do danych plików
Uzupełniające wzorzec jest zestawów danych referencyjnych toostore jako pojedyncze pliki. Te zestawy danych mogą być uważane za strony danych big data "mała" hello, a często są podobne toodimensions w modelu danych analitycznych. Odwołanie do danych plików zawiera rekordy, które są używane tooprovide kontekst dla zbiorczego hello hello plików danych przechowywanych w magazynie danych big data hello w innym miejscu.

Przykładem tego wzorca może być:

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

Pracując naukowca analityka lub dane z danymi hello w większych struktur katalogów hello tooprovide używany dla jednostek, które są określane tooonly według nazwy lub Identyfikatora w danych większych hello bardziej szczegółowe informacje można hello dane w tych plikach odwołania zestaw.

W tym wzorcu warto tooregister hello poszczególnych odwołanie do danych plików z **Azure Data Catalog**. Każdy plik reprezentuje zestaw danych, a każdej z nich może być adnotowany i odnalezione pojedynczo.

## <a name="alternate-patterns"></a>Alternatywne wzorce
Witaj wzorce opisane w powyższej sekcji hello są tylko dwa różne sposoby, które mogą być organizowane przechowywania danych big data, ale każda implementacja jest inny. Niezależnie od tego, jak strukturę źródeł danych, podczas rejestrowania źródła danych big data z **Azure Data Catalog**, skupić się na rejestracji hello pliki i katalogi, które reprezentują hello zestawów danych, które mają wartość tooothers w sieci organizacja. Rejestrowanie wszystkich plików i katalogów można zajmowały hello katalogu, dzięki czemu przeszkodę dla użytkowników toofind wymaganych.

## <a name="summary"></a>Podsumowanie
Rejestrowanie źródeł danych z **Azure Data Catalog** umożliwiają łatwiejsze toodiscover i zrozumieć. Rejestrowanie i adnotowanie hello danych big data pliki i katalogi, które reprezentują logiczne zestawów danych, można ułatwić użytkownikom znalezienia i użycia potrzebnych im źródeł danych big data hello.
