---
title: "aaaOverview usługi Azure Data Lake Store | Dokumentacja firmy Microsoft"
description: "Informacje o funkcjach usługi Azure Data Lake Store i hello wartość, która jest lepsza od innych magazynów danych"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: b3475057-9427-4492-a3af-25a802a23a79
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 5a60a6b86a51c44647cf4ee168fb333d1c37b1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-data-lake-store"></a>Omówienie usługi Azure Data Lake Store
Azure Data Lake Store to repozytorium w hiperskali obsługujące całe przedsiębiorstwo na potrzeby obciążeń analizy dużych ilości danych (big data). Usługa Azure Data Lake umożliwia toocapture danych o dowolnym rozmiar, typ i wprowadzanie szybkości w jednym miejscu na potrzeby analiz operacyjnych i poznawczych.

> [!TIP]
> Użyj hello [ścieżka szkoleniowa dotycząca usługi Data Lake Store](https://azure.microsoft.com/documentation/learning-paths/data-lake-store-self-guided-training/) toostart Eksplorowanie usługi Azure Data Lake Store hello.
> 
> 

Azure Data Lake Store można uzyskać z platformy Hadoop (dostępnych z klastrem usługi HDInsight) przy użyciu hello interfejsów API REST zgodny z WebHDFS. Jest specjalnie zaprojektowanego tooenable analizy hello przechowywanych danych i dostosowana pod kątem wydajności dla scenariuszy analizy danych. Fabrycznej hello obejmuje wszystkie funkcje klasy korporacyjnej hello — zabezpieczeń, możliwości zarządzania, skalowalności, niezawodności i dostępności — niezbędne dla organizacji rzeczywistych przypadków użycia.

![Azure Data Lake](./media/data-lake-store-overview/data-lake-store-concept.png)

Niektóre z kluczowych możliwości hello Azure Data Lake hello obejmują następujące hello.

### <a name="built-for-hadoop"></a>Stworzona dla platformy Hadoop
Hello Azure Data Lake store jest zgodna z platformą Hadoop Distributed pliku System (HDFS) systemem plików Apache Hadoop i działa z ekosystemem Hadoop hello.  Istniejące aplikacje usługi HDInsight lub usługi, które korzystają z interfejsu API WebHDFS hello można łatwo zintegrować z usługą Data Lake Store. Usługa Data Lake Store udostępnia również interfejs REST zgodny z WebHDFS dla aplikacji.

Dane przechowywane w usłudze Data Lake Store można łatwo analizować za pomocą platform analitycznych Hadoop, takich jak MapReduce lub Hive. Microsoft Azure w usłudze hdinsight można udostępnić i skonfigurować toodirectly dostępu do danych przechowywanych w usłudze Data Lake Store.

### <a name="unlimited-storage-petabyte-files"></a>Nieograniczony magazyn, petabajtowe pliki
Usługa Azure Data Lake Store zapewnia nieograniczony magazyn i nadaje się do przechowywania różnorodnych danych na potrzeby analiz. Nie nakłada żadnych limitów dotyczących rozmiarów kont, rozmiarów plików lub hello ilość danych, które mogą być przechowywane w usłudze data lake. Pojedyncze pliki mogą należeć do zakresu od kilobajta toopetabytes rozmiaru, dzięki czemu toostore doskonałym wyborem danych dowolnego typu. Dane są przechowywane trwale dzięki tworzeniu wielu kopii i nie ma żadnego limitu na czas hello, dla których hello dane mogą być przechowywane w usłudze data lake hello.

### <a name="performance-tuned-for-big-data-analytics"></a>Wydajność dostosowana na potrzeby analizy danych big data
Azure Data Lake Store jest skompilowany dla działania dużych systemów analitycznych, które wymagają ogromnej przepływności tooquery i analizowania dużych ilości danych. Witaj data lake rozmieszcza części pliku na wielu serwerach magazynu. Zwiększa to hello przepływności do odczytu podczas odczytywania pliku hello równolegle w celu wykonywania analizy danych.

### <a name="enterprise-ready-highly-available-and-secure"></a>Gotowa do użycia w przedsiębiorstwie: wysoce dostępna i bezpieczna
Usługa Azure Data Lake Store zapewnia dostępność i niezawodność zgodne ze standardami branżowymi. Twoje dane są przechowywane trwale dzięki tooguard nadmiarowe kopie na wypadek nieoczekiwanych awarii. Przedsiębiorstwa mogą wykorzystywać usługę Azure Data Lake w swoich rozwiązaniach jako istotny element istniejącej platformy danych.

Data Lake Store zapewnia również zabezpieczenia korporacyjnej hello przechowywanych danych. Aby uzyskać więcej informacji, zobacz [Zabezpieczanie danych w usłudze Azure Data Lake Store](#DataLakeStoreSecurity).

### <a name="all-data"></a>Wszystkie dane
Usługa Azure Data Lake Store może przechowywać wszystkie dane w ich natywnym formacie, bez wymagania jakiegokolwiek uprzedniego przekształcania danych. Data Lake Store nie wymagają toobe schematu, zdefiniowane przed załadowaniem danych hello pozostawieniu ich w górę toohello poszczególnym środowiskom analitycznym toointerpret hello danych i zdefiniowanie schematu w czasie hello hello analizy. Trwa stanie toostore plików dowolnych rozmiarów i formaty umożliwia strukturę, toohandle Data Lake — magazyn danych z częściową strukturą i bez struktury.

Kontenerami danych usługi Azure Data Lake Store są zasadniczo foldery i pliki. Możesz pracować na powitania przechowywanych danych przy użyciu zestawów SDK, portalu Azure i programu Azure Powershell. Tak długo, jak dane są umieszczane w magazynie hello za pomocą tych interfejsów i przy użyciu odpowiednich kontenerów hello, można przechowywać dane dowolnego typu. Data Lake Store nie wykonuje żadnej specjalnej obsługi danych na podstawie typu danych, które przechowuje hello.

## <a name="DataLakeStoreSecurity"></a>Zabezpieczanie danych w usłudze Azure Data Lake Store
Azure Data Lake Store używa usługi Azure Active Directory do uwierzytelniania i listy kontroli dostępu (ACL) toomanage dostępu tooyour danych.

| Funkcja | Opis |
| --- | --- |
| Authentication |Azure Data Lake Store integruje się z usługi Azure Active Directory (AAD) do zarządzania tożsamościami i dostępem dla wszystkich danych hello przechowywane w usłudze Azure Data Lake Store. W wyniku integracji hello Azure Data Lake korzysta ze wszystkich funkcji usługi AAD, w tym uwierzytelniania wieloskładnikowego, dostępu warunkowego, kontroli dostępu opartej na rolach, monitorowania użycia aplikacji, zabezpieczeń, alertów itp. Azure Data Lake Store obsługuje hello protokołu OAuth 2.0 do uwierzytelniania przy użyciu interfejsu REST hello. |
| Kontrola dostępu |Azure Data Lake Store zapewnia kontrolę dostępu dzięki obsłudze uprawnień POSIX udostępnianych przez hello protokół WebHDFS. W hello Data Lake magazynu publicznej wersji zapoznawczej (hello bieżącej wersji) można włączyć listy kontroli dostępu w folderze głównym hello, podfoldery i poszczególnych plików. Aby uzyskać więcej informacji na temat sposobu działania list kontroli dostępu w kontekście usługi Data Lake Store, zobacz [Kontrola dostępu w usłudze Data Lake Store](data-lake-store-access-control.md). |
| Szyfrowanie |Data Lake Store zapewnia również szyfrowanie danych przechowywanych w hello konta. Ustawienia szyfrowania hello należy określić podczas tworzenia konta usługi Data Lake Store. Można wybrać toohave dane szyfrowane lub wybrać opcję bez szyfrowania. Aby uzyskać więcej informacji na temat konfiguracji tooprovide związane z szyfrowaniem, zobacz [wprowadzenie do usługi Azure Data Lake Store za pomocą portalu Azure hello](data-lake-store-get-started-portal.md). |

Mają toolearn więcej informacji na temat zabezpieczania danych w usłudze Data Lake Store. Wykonaj poniższe linki hello.

* Aby uzyskać instrukcje dotyczące toosecure dane w usłudze Data Lake Store, zobacz [Zabezpieczanie danych w usłudze Azure Data Lake Store](data-lake-store-secure-data.md).
* Wolisz filmy wideo? [Obejrzyj ten film](https://mix.office.com/watch/1q2mgzh9nn5lx) na sposób przechowywania danych toosecure w usłudze Data Lake Store.

## <a name="applications-compatible-with-azure-data-lake-store"></a>Aplikacje zgodne z usługą Azure Data Lake Store
Azure Data Lake Store jest zgodna z najbardziej otwartych składników źródła w ekosystemie Hadoop hello. Bardzo dobrze integruje się również z innymi usługami Azure. Wszystko to sprawia, że usługa Data Lake Store jest doskonałą opcją dla potrzeb magazynu danych. Skorzystaj z linków hello poniżej toolearn więcej informacji na temat sposobu użycia usługi Data Lake Store ze składnikami typu open source, a także innych usług platformy Azure.

* Zobacz [Aplikacje i usługi zgodne z usługą Azure Data Lake Store](data-lake-store-compatible-oss-other-applications.md), aby uzyskać listę aplikacji typu „open source” współpracujących z usługą Azure Data Lake Store.
* Zobacz [integracji z innymi usługami Azure](data-lake-store-integrate-with-other-services.md) toounderstand sposobu użycia usługi Data Lake Store z platformy Azure, innych usług tooenable szerszego zakresu scenariuszy.
* Zobacz [scenariusze korzystania z usługi Data Lake Store](data-lake-store-data-scenarios.md) toolearn jak przechowywać toouse Data Lake w scenariuszach, takich jak odbieranie danych, przetwarzanie danych, pobieranie danych i wizualizacja danych.

## <a name="what-is-azure-data-lake-store-file-system-adl"></a>Co to jest system plików usługi Azure Data Lake Store (adl://)?
Data Lake Store jest dostępny za pośrednictwem hello nowego systemu plików, hello AzureDataLakeFilesystem (adl: / /), w środowiskach Hadoop (dostępnych z klastrem usługi HDInsight). Aplikacje i usługi, które używają adl: / / są tootake można skorzystać z dalszej optymalizacji wydajności, które nie są obecnie dostępne w systemie plików WebHDFS. W związku z tym usługa Data Lake Store zapewnia hello tooeither elastyczność korzystać hello najlepszą wydajność z hello zalecana opcja używania adl: / / lub nadal obsługiwać istniejący kod przez kontynuowanie hello toouse interfejsu API WebHDFS bezpośrednio. Usługa Azure HDInsight w pełni wykorzystuje hello AzureDataLakeFilesystem tooprovide hello najlepszą wydajność w usłudze Data Lake Store.

Można uzyskać dostępu do danych za pomocą usługi Data Lake Store hello `adl://<data_lake_store_name>.azuredatalakestore.net`. Aby uzyskać więcej informacji dotyczących sposobu tooaccess hello danych w hello usługi Data Lake Store, zobacz [Wyświetl właściwości hello przechowywanych danych](data-lake-store-get-started-portal.md#properties)

## <a name="how-do-i-start-using-azure-data-lake-store"></a>Jak zacząć korzystać z usługi Azure Data Lake Store?
Zobacz [wprowadzenie do usługi Data Lake Store za pomocą hello Azure Portal](data-lake-store-get-started-portal.md), w sposób tooprovision za pomocą usługi Data Lake Store hello portalu Azure. Po aprowizowaniu usługi Azure Data Lake, aby dowiedzieć się jak toouse oferty danych big data, takich jak Azure Data Lake Analytics lub Azure HDInsight z usługą Data Lake Store. Można również utworzyć konto usługi Azure Data Lake Store toocreate aplikacji .NET i wykonywanie operacji takich jak przekazywanie danych, pobieranie danych itp.

* [Rozpoczynanie pracy z usługą Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Korzystanie z usługi Azure HDInsight z usługą Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Rozpoczynanie pracy z usługą Azure Data Lake Store z użyciem zestawu SDK .NET](data-lake-store-get-started-net-sdk.md)

## <a name="data-lake-store-videos"></a>Filmy wideo dotyczące usługi Data Lake Store
Jeśli wolisz obserwowanie toolearn wideo, Data Lake Store udostępnia filmy wideo dotyczące różnych funkcji.

* [Tworzenie konta usługi Azure Data Lake Store](https://mix.office.com/watch/1k1cycy4l4gen)
* [Użyj hello Eksploratora danych tooManage danych w usłudze Azure Data Lake Store](https://mix.office.com/watch/icletrxrh6pc)
* [Łączenie usługi Azure Data Lake Analytics tooAzure Data Lake Store](https://mix.office.com/watch/qwji0dc9rx9k)
* [Uzyskiwanie dostępu do usługi Azure Data Lake Store za pomocą usługi Data Lake Analytics](https://mix.office.com/watch/1n0s45up381a8)
* [Łączenie usługi Azure HDInsight tooAzure Data Lake Store](https://mix.office.com/watch/l93xri2yhtp2)
* [Uzyskiwanie dostępu do usługi Azure Data Lake Store za pomocą technologii Hive i Pig](https://mix.office.com/watch/1n9g5w0fiqv1q)
* [Użyj narzędzia DistCp (Hadoop Distributed Copy) toocopy danych tooand z usługi Azure Data Lake Store](https://mix.office.com/watch/1liuojvdx6sie)
* [Używanie Apache Sqoop toomove danych między źródłami relacyjnymi i usługą Azure Data Lake Store](https://mix.office.com/watch/1butcdjxmu114)
* [Organizowanie danych za pomocą usługi Azure Data Factory dla usługi Azure Data Lake Store](https://mix.office.com/watch/1oa7le7t2u4ka)
* [Zabezpieczanie danych w hello Azure Data Lake Store](https://mix.office.com/watch/1q2mgzh9nn5lx)

