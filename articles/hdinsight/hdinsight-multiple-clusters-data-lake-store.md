---
title: "HDInsight wielu klastrów przy użyciu konta usługi Azure Data Lake Store - Azure aaaUse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak klaster toouse więcej niż jeden HDInsight z jednego konta usługi Data Lake Store"
keywords: "magazynu usługi hdinsight, system plików hdfs, danych strukturalnych, bez struktury danych, data lake — Magazyn"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: nitinme
ms.openlocfilehash: 3a125b91fcc1e436270a1bd349f7a2d8f27e06fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-multiple-hdinsight-clusters-with-an-azure-data-lake-store-account"></a>Użyj wielu klastrów usługi HDInsight przy użyciu konta usługi Azure Data Lake Store

Począwszy od usługi HDInsight w wersji 3.5, można utworzyć klastry usługi HDInsight przy użyciu kont usługi Azure Data Lake Store jako hello domyślne w systemie plików.
Data Lake Store obsługuje nieograniczony magazyn, który to idealny nie tylko do obsługi dużych ilości danych. można jednak również hostingu HDInsight wielu klastrów korzystających z jednego konta magazynu Data Lake. Aby instructionson jak toocreate HDInsight klaster z usługi Data Lake Store jako hello magazynu, zobacz [Tworzenie klastrów usługi HDInsight z usługą Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

Ten artykuł zawiera administratorem magazynu Data Lake toohello zalecenia dotyczące konfigurowania pojedynczego i udostępnionych przechowywania konta usługi Data Lake używany w wielu **active** klastrów usługi HDInsight. Zalecenia te mają zastosowanie toohosting wiele Hadoop bezpieczny, a także niezabezpieczonego klastrów udostępnionego konta sklepu usługi Data Lake.


## <a name="data-lake-store-file-and-folder-level-acls"></a>Data Lake — magazyn plików i folderów na poziomie listy kontroli dostępu

Witaj dalszej części tego artykułu założono, że dobrą znajomość poziomu plików i folderów listy kontroli dostępu w usłudze Azure Data Lake Store, które opisano szczegółowo w [kontroli dostępu w usłudze Azure Data Lake Store](../data-lake-store/data-lake-store-access-control.md).

## <a name="data-lake-store-setup-for-multiple-hdinsight-clusters"></a>Instalator usługi Data Lake Store dla wielu klastrów usługi HDInsight
Daj nam zająć hierarchię folderów dwupoziomowej tooexplain hello zalecenia dotyczące używania wiele klastrów usługi HDInsight przy użyciu konta usługi Data Lake Store. Należy wziąć pod uwagę konta usługi Data Lake Store z struktury folderów hello **/klastrów/finance**. Z tej struktury wszystkich klastrach hello wymagane przez organizację Finance hello służy /clusters/finance hello lokalizacji magazynu. W przyszłości, jeśli innej organizacji, powiedz Marketing, chce toocreate klastrów usługi HDInsight przy użyciu hello tego samego konta usługi Data Lake Store, można ich utworzyć /clusters/marketing hello. Teraz, po prostu Użyjmy **/klastrów/finance**.

tooenable tego toobe struktury folderu skutecznie używanych przez klastry usługi HDInsight, administrator usługi Data Lake Store hello musi przypisać odpowiednie uprawnienia, zgodnie z opisem w tabeli hello. uprawnienia Hello tabelą hello odpowiada listy ACL tooAccess, a nie domyślnej ACL. 


|Folder  |Uprawnienia  |Użytkownik będący właścicielem  |Grupa będąca właścicielem  | Użytkownik nazwany | Uprawnienia użytkownika o nazwie | Grupa o nazwie | Uprawnienia grupy o nazwie |
|---------|---------|---------|---------|---------|---------|---------|---------|
|/ | rwxr-x - x  |Administrator |Administrator  |Nazwy głównej usługi |--x  |FINGRP   |r-x         |
|/Clusters | rwxr-x - x |Administrator |Administrator |Nazwy głównej usługi |--x  |FINGRP |r-x         |
|/ klastrów/finance | rwxr-x - t |Administrator |FINGRP  |Nazwy głównej usługi |rwx  |-  |-     |

W tabeli hello

- **Administrator** jest twórcy Witaj i administrator hello konta usługi Data Lake Store.
- **Nazwy głównej usługi** jest hello Azure Active Directory (AAD) nazwy głównej usługi skojarzone z kontem hello.
- **FINGRP** to grupa użytkowników utworzone w usłudze AAD, zawierającą użytkowników z hello finansowych organizacji.

Aby uzyskać instrukcje dotyczące toocreate aplikację AAD (która także tworzy nazwy głównej usługi), zobacz temat [utworzyć aplikację AAD](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application). Aby uzyskać instrukcje dotyczące toocreate grupę użytkowników w usłudze AAD, zobacz temat [Zarządzanie grupami w usłudze Azure Active Directory](../active-directory/active-directory-accessmanagement-manage-groups.md).

Niektóre najważniejsze tooconsider.

- Struktura folderów poziomu Hello dwa (**/klastrów/finance/**) muszą być utworzone i udostępnione z odpowiednimi uprawnieniami przy Witaj, Administratorze usługi Data Lake Store **przed** za pomocą hello konta magazynu dla klastrów. Ta struktura nie jest tworzona automatycznie podczas tworzenia klastrów.
- w powyższym przykładzie Hello zaleca ustawienie hello będący właścicielem grupy **/klastrów/finance** jako **FINGRP** i umożliwiający **r x** dostępu tooFINGRP toohello cały folder, w hierarchii począwszy od głównego hello. Dzięki temu, że hello członkami FINGRP można przechodzić hello struktury folderów, począwszy od katalogu głównego.
- W przypadku hello różne jednostki usługi AAD może tworzenia klastrów w obszarze **/klastrów/finance**, hello trwałe z bitowego (ustawionej dla hello **finance** folder) zapewnia, że foldery utworzone przez jedną usługę Podmiot zabezpieczeń nie można usunąć przez hello innych.
- Po zatwierdzeniu hello struktury folderów i uprawnienia w miejscu, procesu tworzenia klastra usługi HDInsight tworzy lokalizacja magazynu specyficznych dla klastra, w obszarze **/klastrów/finance/**. Na przykład można hello magazynu dla klastra z hello nazwa fincluster01 **/clusters/finance/fincluster01**. Witaj własności i uprawnienia do folderów hello utworzoną przez klaster usługi HDInsight w hello tabeli przedstawiono w tym miejscu.

    |Folder  |Uprawnienia  |Użytkownik będący właścicielem  |Grupa będąca właścicielem  | Użytkownik nazwany | Uprawnienia użytkownika o nazwie | Grupa o nazwie | Uprawnienia grupy o nazwie |
    |---------|---------|---------|---------|---------|---------|---------|---------|
    |/Clusters/finanace/fincluster01 | rwxr-x---  |Nazwy głównej usługi |FINGRP  |- |-  |-   |-  | 
   


## <a name="recommendations-for-job-input-and-output-data"></a>Zalecenia dotyczące zadania danych wejściowych i wyjściowych

Firma Microsoft zaleca się zadania tooa danych wejściowych, którą hello dane wyjściowe z zadania być przechowywane w folderze poza **/klastrów**. Dzięki temu nawet, jeśli folder specyficznych dla klastra hello jest tooreclaim usunięte niektóre miejsca do magazynowania, dane wejściowe zadania hello i dane wyjściowe są nadal dostępne do użycia w przyszłości. W takim przypadku sprawdź, czy hierarchia folderów hello do przechowywania hello zadania wejściami i wyjściami pozwalają odpowiedni poziom dostępu dla hello nazwy głównej usługi.

## <a name="limit-on-clusters-sharing-a-single-storage-account"></a>Ograniczenia w klastrach udostępnianie konta jednego magazynu

limit Hello hello liczby klastrów, które współużytkują jedno konto usługi Data Lake Store, zależy od obciążenia hello uruchomione na tych klastrach. O zbyt wielu klastrów lub bardzo duże obciążenie pracą w klastrach hello, które mają konto magazynu może spowodować hello magazynu konta wejście/wyjście tooget ograniczany.

## <a name="support-for-default-acls"></a>Obsługa listy ACL domyślne

Podczas tworzenia nazwy głównej usługi z dostępem użytkownika o nazwie (zgodnie z informacjami podanymi w powyższej tabeli hello), zaleca się **nie** Dodawanie hello o nazwie użytkownika z domyślnej listy ACL. Inicjowanie obsługi o nazwie użytkownika dostęp przy użyciu list ACL domyślne wyniki w hello przypisanie uprawnień 770 użytkownik właściciel, będący właścicielem grupy i inne. Gdy ta wartość domyślną 770 nie odbieranie uprawnień z użytkownik właściciel (7) lub grupy będącej właścicielem [7], optymalizacji trwa wszystkie uprawnienia dla innych użytkowników (0). Powoduje to znany problem dotyczący jednego określonego przypadek użycia, która została omówiona szczegółowo w hello [— znane problemy i rozwiązania](#known-issues-and-workarounds) sekcji.

## <a name="known-issues-and-workarounds"></a>Znane problemy i rozwiązania

W tej sekcji wymieniono znane problemy dotyczące korzystania z usługi Data Lake Store i ich obejścia HDInsight hello.

### <a name="publicly-visible-localized-yarn-resources"></a>Widocznego publicznie zlokalizowanych zasobów YARN

Po utworzeniu nowego konta magazynu usługi Azure Data Lake katalog główny hello jest automatycznie udostępniane z too770 zestawu usługi bits uprawnienia dostępu ACL. folder główny Hello będący właścicielem użytkownika użytkownik toohello zestawu, który utworzył konto hello (Witaj, Administratorze usługi Data Lake Store), a właścicielem grupy hello jest ustawiana toohello grupą podstawową hello użytkownik, który utworzył konto hello. Brak dostępu jest dostępna dla "inne".

Te ustawienia są znane tooaffect jednego określonego HDInsight przypadek użycia przechwytywane [YARN 247](https://hwxmonarch.atlassian.net/browse/YARN-247). Przesyłanie zadań może zakończyć się niepowodzeniem z toothis podobne komunikat błędu:

    Resource XXXX is not publicly accessible and as such cannot be part of hello public cache.

Zgodnie z hello YARN JIRA połączony wcześniej, podczas lokalizowania zasobów publicznych hello się, że lokalizatora sprawdza, czy wszystkie hello wymagane zasoby są w rzeczywistości publicznego, sprawdzając swoje uprawnienia w zdalnym systemie plików hello. Lokalizacja odrzucenia żadnych LocalResource, który nie mieści się tego warunku. Witaj wyboru dla uprawnień, obejmuje toohello dostęp do odczytu pliku "inne". W tym scenariuszu nie działa poza pole odnośnie do hostowania klastrów HDInsight w usłudze Azure Data Lake, ponieważ usługa Azure Data Lake nie zezwala na dostęp za "inne" na poziomie folderu głównego.

#### <a name="workaround"></a>Obejście problemu
Zestaw odczytu-uprawnienia do uruchamiania **innym** przez hierarchię hello, na przykład  **/** , **/klastrów** i   **/klastrów/finance**  opisane w powyższej tabeli hello.

## <a name="see-also"></a>Zobacz też

* [Tworzenie klastra usługi HDInsight z usługą Data Lake Store jako magazyn](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)


