---
title: "aaaUse akcji skryptu tooinstall Solr na klastra usługi Hadoop - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak klaster toocustomize HDInsight z Solr za pomocą akcji skryptu."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b1e6f338-8ac1-4b38-bbb5-2f7388b9de3b
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 022ba56b7499390a91bfe869e5069893e56b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a>Zainstalować i używać Solr w klastrach HDInsight opartych na systemie Windows

Dowiedz się, jak klaster toocustomize HDInsight opartych na systemie Windows z Solr za pomocą akcji skryptu i jak toouse Solr toosearch danych.

> [!IMPORTANT]
> Witaj czynnościach w ramach tego dokumentu działać tylko w przypadku klastrów usługi HDInsight opartych na systemie Windows. HDInsight jest dostępna tylko w systemie Windows dla wersji starszej niż HDInsight 3.4. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows). Dla informacji o korzystaniu z opartą na systemie Linux klastrem Solr, zobacz [instalacji i używania Solr w klastrach HDinsight Hadoop (Linux)](hdinsight-hadoop-solr-install-linux.md).


Solr można zainstalować w klastrze (na platformie Hadoop, Storm, HBase, Spark) w usłudze Azure HDInsight dowolnego typu za pomocą *akcji skryptu*. Przykładowy skrypt tooinstall Solr w klastrze usługi HDInsight jest dostępna z obiektu blob magazynu Azure w trybie tylko do odczytu w [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

Witaj przykładowy skrypt działa tylko w przypadku klastra HDInsight w wersji 3.1. Aby uzyskać więcej informacji o wersjach klastra usługi HDInsight, zobacz [wersji klastra usługi HDInsight](hdinsight-component-versioning.md).

używane w tym temacie program Hello przykładowy skrypt tworzy klaster Solr opartych na systemie Windows z określonej konfiguracji. Jeśli chcesz tooconfigure hello Solr klaster z różnych kolekcji, odłamków, schematów, replik, itp., należy zmodyfikować skrypt hello i pliki binarne Solr odpowiednio.

**Pokrewne artykuły**

* [Zainstalować i używać Solr w klastrach HDinsight Hadoop (Linux)](hdinsight-hadoop-solr-install-linux.md)
* [Tworzenie klastrów Hadoop w usłudze HDInsight](hdinsight-provision-clusters.md): ogólne informacje na temat tworzenia klastrów usługi HDInsight.
* [Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu][hdinsight-cluster-customize]: ogólne informacje na temat Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu.
* [Tworzenie skryptów akcji skryptu dla usługi HDInsight](hdinsight-hadoop-script-actions.md).

## <a name="what-is-solr"></a>Co to jest Solr?
<a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> to platforma wyszukiwania przedsiębiorstwa, która umożliwia wydajne wyszukiwanie pełnotekstowe danych. Gdy Hadoop umożliwia przechowywanie i zarządzania nimi czasach ogromne ilości danych, Apache Solr zapewnia możliwości wyszukiwania hello tooquickly pobierania hello danych.

## <a name="install-solr-using-portal"></a>Zainstaluj Solr przy użyciu portalu
1. Rozpocznij tworzenie klastra przy użyciu hello **Utwórz niestandardowy** opcji, zgodnie z opisem w [klastrów utworzyć Hadoop w HDInsight](hdinsight-provision-clusters.md).
2. Na powitania **akcji skryptu** strony kreatora powitania kliknij przycisk **dodać akcję skryptu** tooprovide szczegółowych informacji o hello akcji skryptu, jak pokazano poniżej:

    ![Użyj akcji skryptu toocustomize klastra](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "toocustomize akcji skryptu Użyj klastra")

    <table border='1'>
        <tr><th>Właściwość</th><th>Wartość</th></tr>
        <tr><td>Nazwa</td>
            <td>Określ nazwę hello akcji skryptu. Na przykład <b>zainstalować Solr</b>.</td></tr>
        <tr><td>Identyfikator URI skryptu</td>
            <td>Określ hello identyfikator URI (Uniform Resource) toohello skrypt, który jest wywołana toocustomize hello klastra. Na przykład <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></td></tr>
        <tr><td>Typ węzła</td>
            <td>Określ hello węzłów, na których uruchomiono hello dostosowywania skryptu. Możesz wybrać <b>we wszystkich węzłach</b>, <b>tylko węzły główne</b>, lub <b>tylko węzłów procesu roboczego</b>.
        <tr><td>Parametry</td>
            <td>Określ parametry hello, jeśli są wymagane przez skrypt hello. Hello skryptu tooinstall Solr nie wymaga żadnych parametrów, więc można to pole pozostanie puste.</td></tr>
    </table>

    Więcej niż jeden tooinstall akcji skryptu można dodać wiele składników w klastrze hello. Po dodaniu hello skryptów, kliknij przycisk toostart znacznikiem wyboru hello tworzenia klastra hello.

## <a name="use-solr"></a>Korzystanie z platformy Solr
Musi rozpoczynać się od indeksowanie Solr z niektórych plików danych. Następnie można zapytania wyszukiwania toorun Solr hello indeksowania danych. Wykonaj następujące kroki toouse Solr w klastrze HDInsight hello:

1. **Za pomocą protokołu RDP (Remote Desktop) tooremote do klastra usługi HDInsight hello Solr zainstalowane**. Z hello portalu Azure włączenie pulpitu zdalnego dla klastra hello, utworzone za pomocą Solr hello zainstalowane, a następnie zdalnego w klastrze. Aby uzyskać instrukcje, zobacz [połączyć za pomocą protokołu RDP klastrów tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).
2. **Indeks Solr, przekazując pliki danych**. Indeks Solr, możesz zaznaczyć dokumentów w nim, który może być konieczne toosearch na. tooindex Solr, użyj tooremote RDP do klastra hello Przejdź toohello pulpitu, otwórz wiersz polecenia hello Hadoop i przejdź zbyt**C:\apps\dist\solr-4.7.2\example\exampledocs**. Uruchom następujące polecenie hello:

        java -jar post.jar solr.xml monitor.xml

    Zostanie wyświetlony hello następujące dane wyjściowe w konsoli hello:

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    Narzędzie post.jar Hello indeksuje Solr z dwa dokumenty przykładowe, **solr.xml** i **monitor.xml**. Narzędzie post.jar Hello i hello przykładowe dokumenty są dostępne z instalacją Solr.
3. **Użyj hello Solr pulpitu nawigacyjnego toosearch w hello indeksowane dokumenty**. W toohello sesji protokołu RDP hello HDInsight klastra, Otwórz program Internet Explorer i uruchomić pulpitu nawigacyjnego Solr hello na **http://headnodehost:8983/solr / #/**. W lewym okienku hello z hello **selektora Core** listy rozwijanej, wybierz pozycję **collection1**, a w ramach, kliknij przycisk **zapytania**. Jako przykład tooselect i powrotu wszystkie dokumenty hello w Solr, zawierają hello następujące wartości:

   * W hello **q** tekst wprowadź  **\*:**\*. Zwróci wszystkie dokumenty hello, które są indeksowane w Solr. Jeśli chcesz toosearch dla określonego ciągu w dokumentach hello, można wprowadzić ten ciąg w tym miejscu.
   * W hello **wt** pole tekstowe, hello wybierz format danych wyjściowych. Domyślnie jest **json**. Kliknij przycisk **wykonać kwerendy**.

     ![Użyj akcji skryptu toocustomize klastra](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "uruchomić kwerendę na pulpicie nawigacyjnym Solr")

     dane wyjściowe Hello zwraca hello dwa dokumenty, używane do indeksowania Solr. Witaj dane wyjściowe podobne hello następującego:

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }
4. **Zalecane: Kopia zapasowa hello indeksowane dane z tooAzure Solr magazynu obiektów Blob skojarzony z klastrem usługi HDInsight hello**. Dobrym rozwiązaniem należy wykonać kopię zapasową danych hello indeksowana z węzłów klastra Solr hello na magazynu obiektów Blob platformy Azure. Wykonaj hello, więc po toodo kroki:

   1. Z sesji protokołu RDP hello Otwórz program Internet Explorer i toohello punktu następującego adresu URL:

           http://localhost:8983/solr/replication?command=backup

       Powinna zostać wyświetlona odpowiedź następująco:

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. W sesji zdalnej hello Przejdź zbyt {SOLR_HOME}\{kolekcji} \data. Dla klastra hello utworzony za pośrednictwem hello przykładowy skrypt, należy to **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**. W tej lokalizacji powinna zostać wyświetlona folder migawki utworzone z nazwą podobne**migawki.* Sygnatura czasowa***.
   3. Folder migawki hello zip, a następnie przekaż tooAzure magazynu obiektów Blob. Z wiersza polecenia platformy Hadoop hello należy przejść toohello lokalizację folderu migawek hello za pomocą hello następujące polecenie:

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       To polecenie kopie hello zbyt/przykład/dane migawki/w kontenerze hello w domyślnej hello magazynu konta skojarzonego z klastrem hello.

## <a name="install-solr-using-aure-powershell"></a>Zainstaluj Solr przy użyciu programu Azure PowerShell
Zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  Witaj w przykładzie pokazano, jak tooinstall Spark przy użyciu programu Azure PowerShell. Należy toocustomize hello skryptu toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

## <a name="install-solr-using-net-sdk"></a>Zainstaluj Solr przy użyciu zestawu .NET SDK
Zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). Witaj w przykładzie pokazano, jak tooinstall Spark przy użyciu hello zestawu .NET SDK. Należy toocustomize hello skryptu toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).

## <a name="see-also"></a>Zobacz też
* [Zainstalować i używać Solr w klastrach HDinsight Hadoop (Linux)](hdinsight-hadoop-solr-install-linux.md)
* [Tworzenie klastrów Hadoop w usłudze HDInsight](hdinsight-provision-clusters.md): ogólne informacje na temat tworzenia klastrów usługi HDInsight.
* [Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu][hdinsight-cluster-customize]: ogólne informacje na temat Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu.
* [Tworzenie skryptów akcji skryptu dla usługi HDInsight](hdinsight-hadoop-script-actions.md).
* [Zainstalować i używać platformy Spark w klastrach HDInsight][hdinsight-install-spark]: Akcja skryptu próbki o instalowaniu Spark.
* [Zainstalować język R w klastrach HDInsight][hdinsight-install-r]: Akcja skryptu próbki o instalowaniu R.
* [Zainstaluj w klastrach HDInsight Giraph](hdinsight-hadoop-giraph-install.md): Akcja skryptu próbki o instalowaniu Giraph.

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
