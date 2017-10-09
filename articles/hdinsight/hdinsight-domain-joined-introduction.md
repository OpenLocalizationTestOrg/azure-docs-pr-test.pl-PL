---
title: "zabezpieczenia aaaHadoop — przyłączonych do domeny w usłudze hdinsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się..."
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7dc6847d-10d4-4b5c-9c83-cc513cf91965
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/31/2016
ms.author: saurinsh
ms.openlocfilehash: 5a9469402a61bcba4017e1ff4bd06dfba23ac963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-toohadoop-security-with-domain-joined-hdinsight-clusters-preview"></a>Wprowadzenie zabezpieczeń tooHadoop z klastrami HDInsight przyłączonych do domeny (wersja zapoznawcza)

Do tej pory usługa Azure HDInsight obsługiwała tylko jednego użytkownika z uprawnieniami lokalnego administratora. Bardzo dobrze funkcjonowało to dla mniejszych zespołów aplikacji lub działów. Jako Hadoop obciążeń na podstawie zebranych więcej popularne sektora enterprise hello hello potrzebę enterprise klasy możliwości, takie jak usługi active directory na podstawie uwierzytelniania, obsługa wielu użytkowników i kontroli dostępu opartej na rolach stał się coraz bardziej ważne. Z użyciem klastrów HDInsight przyłączonych do domeny, można utworzyć domenę usługi Active Directory tooan przyłączone do klastra usługi HDInsight, skonfiguruj listę pracowników hello Enterprise, którzy mogą uwierzytelniać za pośrednictwem usługi Azure Active Directory toolog w klastrze tooHDInsight. Każda osoba spoza organizacji hello nie może zalogować się lub dostępu do klastra usługi HDInsight hello. Witaj administratorem przedsiębiorstwa można skonfigurować kontroli dostępu opartej na rolach dla gałęzi zabezpieczeń przy użyciu [zakres Apache](http://hortonworks.com/apache/ranger/), w związku z tym ograniczanie dostępu toodata tooonly jak potrzebne. Na koniec Witaj, Administratorze przeprowadzać inspekcję dostępu do danych hello przez pracowników, a wszelkie zmiany wykonane tooaccess kontrolowanie zasad, w związku z tym uzyskanie wysoki stopień ładu ich zasobów firmy.

> [!NOTE]
> Witaj nowych funkcji opisanych w tej wersji zapoznawczej są dostępne tylko na opartych na systemie Linux klastrów usługi HDInsight Hive obciążenia pracą. Witaj innych obciążeń, takich jak bazy danych HBase, Spark, Storm i Kafka, będzie można włączyć w przyszłych wersjach.

> [!IMPORTANT]
> Oozie nie jest włączona w usłudze HDInsight z przyłączonych do domeny.

## <a name="benefits"></a>Korzyści
Na zabezpieczenia przedsiębiorstwa składają się cztery wielkie filary — zabezpieczenia brzegowe, uwierzytelnianie, autoryzacja i szyfrowanie.

![Filary korzyści z zastosowania przyłączonych do domeny klastrów usługi HDInsight](./media/hdinsight-domain-joined-introduction/hdinsight-domain-joined-four-pillars.png).

### <a name="perimeter-security"></a>Zabezpieczenia brzegowe
Zabezpieczenia brzegowe w usłudze HDInsight są realizowane za pomocą sieci wirtualnych i usługi bramy. Dzisiaj administrator przedsiębiorstwa można utworzyć klastra usługi HDInsight w sieci wirtualnej i korzystać z sieci wirtualnej toohello dostępu toorestrict grup zabezpieczeń sieci (reguły zapory dla ruchu przychodzącego lub wychodzącego). Tylko hello adresów IP zdefiniowanych w hello ruchu przychodzącego reguły zapory będą mogli toocommunicate z klastrem usługi HDInsight hello, zapewniając granicznej zabezpieczeń. Inna warstwa zabezpieczeń brzegowych jest realizowana przy użyciu usługi bramy. Witaj bramy jest hello usługi, która działa jako pierwszą linię obrony dla dowolnego klastra usługi HDInsight przychodzące toohello żądania. Akceptuje Żądanie hello, następnie zweryfikuje go i następnie umożliwia hello żądania toopass toohello inne węzły w klastrze, zapewniając granicznej zabezpieczeń tooother nazwy i danych węzłów w klastrze hello.

### <a name="authentication"></a>Authentication
W tej publicznej wersji zapoznawczej administrator przedsiębiorstwa może udostępnić przyłączony do domeny klaster usługi HDInsight w [sieci wirtualnej](https://azure.microsoft.com/services/virtual-network/). węzły klastra usługi HDInsight hello Hello będzie toohello przyłączone do domeny zarządza hello enterprise. Jest to realizowane poprzez użycie [usług Azure Active Directory Domain Services](../active-directory-domain-services/active-directory-ds-overview.md). Wszystkie węzły hello w klastrze hello są tooa przyłączone do domeny, która zarządza hello przedsiębiorstwa. W przypadku tej konfiguracji hello enterprise pracownicy mogą logować toohello węzłów klastra przy użyciu swoich poświadczeń domeny. Z innych zatwierdzonych punktów końcowych, takie jak toointeract Hue, widoki Ambari, ODBC, JDBC, programu PowerShell i interfejsów API REST z klastrem hello mogą również wykorzystać ich tooauthenticate poświadczenia domeny. Witaj, Administratorze ma pełną kontrolę nad ograniczanie hello liczby użytkowników, interakcji z hello klastra za pomocą tych punktów końcowych.

### <a name="authorization"></a>Autoryzacja
Najlepszym rozwiązaniem, a następnie większość przedsiębiorstw jest, że nie każdy pracownik ma dostęp do zasobów przedsiębiorstwa tooall. Podobnie w tym wydaniu Witaj, Administratorze można zdefiniować zasady kontroli dostępu opartej na rolach dla hello zasobów klastra. Na przykład można skonfigurować Witaj, Administratorze [zakres Apache](http://hortonworks.com/apache/ranger/) tooset zasady kontroli dostępu dla gałęzi. Ta funkcja zapewnia, że pracownicy będą mogli tooaccess tylko tyle danych potrzebują toobe powiodło się w swoich zadań. Klastra toohello dostępu SSH jest również ograniczony toohello tylko administrator.

### <a name="auditing"></a>Inspekcja
Wraz z ochrona powitalnych HDInsight zasoby klastra przed nieautoryzowanymi użytkownikami i zabezpieczania danych hello, inspekcji wszystkich uzyskiwać dostęp do zasobów klastra toohello i hello danych jest konieczne tootrack dostęp nieautoryzowani lub przypadkowe hello zasobów. W tej wersji zapoznawczej Witaj, Administratorze można wyświetlać i raportuje wszystkie zasoby klastra usługi HDInsight toohello dostępu i danych. Witaj, Administratorze można również wyświetlić i raportu wszystkie zmiany zasad kontroli dostępu toohello w zakres Apache obsługiwane punktów końcowych. Klaster HDInsight przyłączonych do domeny używa dzienników inspekcji toosearch znanego interfejsu użytkownika zakres Apache hello. Witaj wewnętrznej bazy danych, używa zakres [Apache Solr](http://hortonworks.com/apache/solr/) do przechowywania i wyszukiwanie hello dzienników.

### <a name="encryption"></a>Szyfrowanie
Ochrona danych jest ważne w przypadku spotkań zabezpieczeń organizacji i wymagań dotyczących zgodności i oraz ograniczenie dostępu toodata od nieautoryzowanych pracowników, jego powinny również były zabezpieczone przez ich szyfrowanie. Zarówno hello magazyny danych w klastrach HDInsight, obiektu Blob magazynu Azure i usługi Azure Data Lake Storage obsługuje przezroczysty po stronie serwera [szyfrowania danych](../storage/common/storage-service-encryption.md) w stanie spoczynku. Zabezpieczanie klastrów usługi HDInsight funkcjonuje bezproblemowo przy użyciu funkcji szyfrowania danych magazynowanych po stronie serwera.

## <a name="next-steps"></a>Następne kroki
* Aby skonfigurować przyłączony do domeny klaster usługi HDInsight, zobacz [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Konfigurowanie przyłączonych do domeny klastrów usługi HDInsight).
* Aby zarządzać przyłączonymi do domeny klastrami usługi HDInsight, zobacz [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md) (Zarządzanie przyłączonymi do domeny klastrami usługi HDInsight).
* Aby znaleźć informacje na temat konfigurowania zasad Hive i uruchamiania kwerend Hive, zobacz [Konfigurowanie zasad usługi Hive dla przyłączonych do domeny klastrów usługi HDInsight](hdinsight-domain-joined-run-hive.md).
* Do uruchamiania zapytań Hive przy użyciu protokołu SSH w klastrach HDInsight przyłączonych do domeny, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
