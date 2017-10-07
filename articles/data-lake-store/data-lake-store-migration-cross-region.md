---
title: "aaaAzure migracji między region usługi Data Lake Store | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat migracji między regionu Azure Data Lake Store."
services: data-lake-store
documentationcenter: 
author: swums
manager: amitkul
editor: swums
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/27/2017
ms.author: stewu
ms.openlocfilehash: 561ac821c1bd555886035867678cb685997564eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-data-lake-store-across-regions"></a>Migracja usługi Data Lake Store w regionach

Jak usługa Azure Data Lake Store stają się dostępne w nowych regionów, możesz wybrać toodo migracji jednorazowej tootake zaletą hello nowy region. Jakie tooconsider Dowiedz się, jak zaplanować i ukończyć powitalnych migracji.

## <a name="prerequisites"></a>Wymagania wstępne

* **Subskrypcja platformy Azure**. Aby uzyskać więcej informacji, zobacz [utworzyć bezpłatne konto platformy Azure obecnie](https://azure.microsoft.com/pricing/free-trial/).
* **Konto usługi Data Lake Store w dwóch różnych regionach**. Aby uzyskać więcej informacji, zobacz [wprowadzenie do usługi Azure Data Lake Store](data-lake-store-get-started-portal.md).
* **Fabryka danych Azure**. Aby uzyskać więcej informacji, zobacz [tooAzure wprowadzenie fabryki danych](../data-factory/data-factory-introduction.md).


## <a name="migration-considerations"></a>Zagadnienia dotyczące migracji

Ustalenie strategii migracji hello, który jest najlepsza dla aplikacji, która zapisuje lub odczytuje przetwarza dane w usłudze Data Lake Store. W przypadku strategii, należy wziąć pod uwagę wymagania dostępności aplikacji i hello przestoju, która występuje podczas migracji. Na przykład Twoje najprostsza metoda może być toouse hello chmury "przyrostu i shift" migracji modelu. W tej metody, w przypadku wstrzymania aplikacji hello w danym regionie istniejących podczas, gdy wszystkie dane są kopiowane toohello nowego regionu. Po zakończeniu procesu kopiowania hello wznowić aplikacji hello nowy region, a następnie usuń stare konto usługi Data Lake Store hello. Czas przestoju w trakcie migracji hello jest wymagana.

tooreduce przestojów, mogą natychmiast rozpoczęciem wprowadzania nowych danych w regionie nowe hello. Jeśli masz hello minimalną ilość danych potrzebne, uruchom aplikację w regionie nowe hello. W tle hello nadal toocopy starszych danych z hello istniejącej usługi Data Lake Store konta toohello nowego konta Data Lake Store w regionie nowe hello. Przy użyciu tej metody, można wprowadzić nowy region toohello przełącznika hello małego przestojów. Po skopiowaniu wszystkich starszych danych hello Usuń stare konto usługi Data Lake Store hello.

Inne tooconsider ważne informacje dotyczące planowania migracji są:

* **Ilość danych**. Witaj ilość danych (w gigabajtach, hello liczbę plików i folderów i tak dalej) wpływa na powitania czasu i zasobów potrzebnych do migracji hello.

* **Nazwa konta usługi Data Lake Store**. nazwę nowego konta Hello w regionie nowe hello musi być globalnie unikatowe. Na przykład nazwa hello starego konta usługi Data Lake Store w wschodnie stany USA 2 może być contosoeastus2.azuredatalakestore.net. Możesz nazwać nowego konta usługi Data Lake Store w contosonortheu.azuredatalakestore.net Północna, Europa.

* **Narzędzia**. Zalecane jest użycie hello [działanie kopiowania fabryki danych Azure](../data-factory/data-factory-azure-datalake-connector.md) toocopy Data Lake — magazyn plików. Fabryka danych obsługuje przenoszenie danych o wysokiej wydajności i niezawodności. Należy pamiętać, że fabryki danych kopiuje tylko hello hierarchii folderów i zawartość plików hello. Należy toomanually Zastosuj wszelkie listy kontroli dostępu (ACL) używanych w hello stare konto toohello nowe konto. Aby uzyskać więcej informacji, w tym cele wydajności dla scenariuszy najlepszym Zobacz hello [wydajności działania kopiowania i dostrajania przewodnik](../data-factory/data-factory-copy-activity-performance.md). Jeśli chcesz, aby szybciej skopiować dane, może być konieczne toouse jednostki dodatkowe przepływu danych w chmurze. Kopiowanie danych między regionami innych narzędzi, takich jak AdlCopy, nie jest obsługiwane.  

* **Opłaty przepustowości**. [Opłaty przepustowości](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) zastosować, ponieważ dane są przesyłane poza region platformy Azure.

* **Listy kontroli dostępu na podstawie danych**. Zabezpieczanie danych w regionie nowe hello stosując toofiles listy kontroli dostępu i folderów. Aby uzyskać więcej informacji, zobacz [Zabezpieczanie danych przechowywanych w usłudze Azure Data Lake Store](data-lake-store-secure-data.md). Firma Microsoft zaleca używanie hello tooupdate migracji i dostosować Twojej listy kontroli dostępu. Możesz toouse podobne tooyour bieżącego ustawienia. Możesz wyświetlić hello listy kontroli dostępu są stosowane tooany pliku przy użyciu hello portalu Azure, [poleceń cmdlet programu PowerShell](/powershell/module/azurerm.datalakestore/get-azurermdatalakestoreitempermission), ani zestawów SDK.  

* **Lokalizacja usługi analizy**. Aby uzyskać najlepszą wydajność, usługi analytics, takich jak Azure Data Lake Analytics lub Azure HDInsight powinna mieć hello tego samego regionu danych.  

## <a name="next-steps"></a>Następne kroki
* [Omówienie usługi Azure Data Lake Store](data-lake-store-overview.md)
