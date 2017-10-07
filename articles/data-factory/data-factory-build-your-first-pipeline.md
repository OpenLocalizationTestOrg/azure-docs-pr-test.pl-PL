---
title: 'Data Factory samouczek: pierwszy potok danych | Dokumentacja firmy Microsoft'
description: "W tym samouczku fabryki danych Azure przedstawiono, jak toocreate i harmonogram fabryki danych, który przetwarza dane przy użyciu Hive skryptom na klastra usługi Hadoop."
services: data-factory
keywords: "usługi Azure data factory samouczek, klastra usługi hadoop, hadoop hive"
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.assetid: 81f36c76-6e78-4d93-a3f2-0317b413f1d0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: ed9c0ade4500d4ac1f7c2c2312c1fa675e0b1f02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-pipeline-tootransform-data-using-hadoop-cluster"></a>Samouczek: Tworzenie pierwszego potoku dane tootransform przy użyciu klastra usługi Hadoop
> [!div class="op_single_selector"]
> * [Przegląd i wymagania wstępne](data-factory-build-your-first-pipeline.md)
> * [Witryna Azure Portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Program Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Szablon usługi Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [Interfejs API REST](data-factory-build-your-first-pipeline-using-rest-api.md)

W tym samouczku należy utworzyć pierwszy fabrykę danych Azure z potokiem danych. potok Hello przekształca danych wejściowych przez uruchomienie skryptu Hive w danych wyjściowych tooproduce klastra Azure HDInsight (Hadoop).  

Ten artykuł zawiera omówienie i wymagania wstępne dotyczące samouczka hello. Po zakończeniu hello wymagań wstępnych, można wykonać przy użyciu jednej z hello następujące narzędzia/zestawów SDK samouczek hello: portal Azure, programu Visual Studio, programu PowerShell, szablon usługi Resource Manager, interfejsu API REST. Wybierz jedną z opcji hello na liście rozwijanej hello hello początek (lub) łącza na końcu hello tego samouczka hello toodo artykułu przy użyciu jednej z tych opcji.    

## <a name="tutorial-overview"></a>Omówienie samouczka
W tym samouczku należy wykonać następujące kroki hello:

1. Utwórz **fabryki danych**. Fabryka danych może zawierać potoki danych, które Przenieś i przekształcania danych. 

    W tym samouczku utworzysz jeden potok w fabryce danych hello. 
2. Utwórz **potoku**. Potok może mieć co najmniej jedno działanie (przykłady: działanie kopiowania, działania Hive HDInsight). W przykładzie użyto hello HDInsight Hive działania, które uruchamia skrypt Hive w klastrze usługi HDInsight Hadoop. skrypt Hello najpierw tworzy tabelę, która odwołania hello raw sieci web dziennika danych przechowywanych w magazynie obiektów blob platformy Azure, a następnie partycje hello nieprzetworzone dane przez rok i miesiąc.

    W tym samouczku potoku hello używa hello Hive działania tootransform danych przez uruchomienie zapytania programu Hive w klastrze usługi Azure HDInsight Hadoop. 
3. Utwórz **połączone usługi**. Można tworzyć toolink połączonej usługi magazynu danych lub fabryki danych toohello usługi obliczeniowej. Magazyn danych, takie jak magazyn Azure przechowuje dane wejścia/wyjścia działań w potoku hello. Usługi obliczeniowe, takich jak klaster usługi HDInsight Hadoop procesów/przekształcenia danych.

    W tym samouczku, Utwórz dwie połączonej usługi: **usługi Azure Storage** i **Azure HDInsight**. Hello Azure Storage połączone usługi łączy konta magazynu platformy Azure przechowuje fabryki danych toohello danych wejścia/wyjścia hello. Usługa Azure HDInsight połączone usługi łączy klaster Azure HDInsight fabryki danych toohello tootransform używane w danych. 
3. Utwórz dane wejściowe i wyjściowe **zestawów danych**. Zestaw danych wejściowych reprezentuje hello dane wejściowe dla działania w potoku hello a hello wyjściowy dla działania hello wyjściowy zestaw danych.

    W tym samouczku, hello danych wejściowych i wyjściowych zestawów danych Określ lokalizacje danych wejściowych, a dane wyjściowe w hello magazynu obiektów Blob Azure. Witaj połączoną usługą magazynu Azure Określa konto magazynu platformy Azure jest używana. Zestaw danych wejściowych Określa, gdzie znajdują się pliki wejściowe hello a wyjściowy zestaw danych rozmieszczenia hello plików wyjściowych. 


Zobacz [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) artykułu szczegółowe omówienie fabryki danych Azure.
  
Oto hello **widok diagramu** fabryki danych przykładowych hello kompilacji w tym samouczku. **MyFirstPipeline** ma jedno działanie typu Hive, który wykorzystuje **AzureBlobInput** zestawu danych jako dane wejściowe i tworzy **AzureBlobOutput** zestawu danych jako dane wyjściowe. 

![Widok diagramu w samouczku fabryki danych](media/data-factory-build-your-first-pipeline/data-factory-tutorial-diagram-view.png)


W tym samouczku **inputdata** folderu hello **adfgetstarted** kontenera obiektów blob platformy Azure zawiera jeden plik o nazwie input.log. Ten plik dziennika zawiera wpisy z trzech miesięcy: stycznia, lutego i marca 2016 r. Poniżej przedstawiono hello Przykładowe wiersze dla każdego miesiąca w pliku wejściowym hello. 

```
2016-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871 
2016-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2016-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

Podczas przetwarzania pliku hello przez potok hello z działaniem Hive HDInsight hello odbywa się działanie skryptu Hive w klastrze usługi HDInsight hello że partycje wprowadzanie danych przez rok i miesiąc. Witaj skrypt tworzy trzech plików zawierających plik z wpisów z każdego miesiąca.  

```
adfgetstarted/partitioneddata/year=2016/month=1/000000_0
adfgetstarted/partitioneddata/year=2016/month=2/000000_0
adfgetstarted/partitioneddata/year=2016/month=3/000000_0
```

Z hello przykładów — wiersze przedstawionych powyżej, hello najpierw (z 2016-01-01) jest zapisywany plik 000000_0 toohello w miesiącu hello = 1 folder. Podobnie, hello drugi z nich jest zapisywany plik toohello w miesiącu hello = 2 folderu i hello innej jedną jest zapisywany plik toohello w miesiącu hello = 3 folder.  

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka, musi mieć hello następujące wymagania wstępne:

1. **Subskrypcja platformy Azure** — Jeśli nie masz subskrypcji platformy Azure, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Zobacz hello [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/) artykuł, w jaki sposób można uzyskać bezpłatne konto próbne.
2. **Usługa Azure Storage** — używane konto magazynu ogólnego przeznaczenia, standard i Azure do przechowywania danych hello w tym samouczku. Jeśli nie masz konta magazynu ogólnego przeznaczenia Azure standardowego, zobacz hello [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) artykułu. Po utworzeniu konta magazynu hello notowanie niezbędnych hello **nazwa konta** i **klucz dostępu**. Zobacz [widoku, kopiowania i regenerate magazynu klucze dostępu](../storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys).
3. Pobierz i przejrzyj plik zapytania Hive hello (**HQL**) w lokalizacji: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql](https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql). To zapytanie przy użyciu danych wyjściowych tooproduce danych wejściowych. 
4. Pobierz i przejrzyj hello przykładowy plik wejściowy (**input.log**) w lokalizacji: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log](https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log)
5. Tworzenie kontenera obiektów blob o nazwie **adfgetstarted** w magazynie obiektów Blob Azure. 
6. Przekaż **partitionweblogs.hql** pliku toohello **skryptu** folderu w hello **adfgetstarted** kontenera. Użyj narzędzia takiego jak [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/). 
7. Przekaż **input.log** pliku toohello **inputdata** folderu w hello **adfgetstarted** kontenera. 

Po ukończeniu hello wymagania wstępne, wybierz jedną z hello samouczka hello toodo narzędzia/zestawów SDK: 

- [Witryna Azure Portal](data-factory-build-your-first-pipeline-using-editor.md)
- [Program Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
- [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
- [Szablon usługi Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
- [Interfejs API REST](data-factory-build-your-first-pipeline-using-rest-api.md)

Portalu Azure i programu Visual Studio umożliwiają graficznego interfejsu użytkownika w budynku z fabryki danych. Natomiast opcje środowiska PowerShell, szablon usługi Resource Manager i interfejsu API REST zawiera skryptów programowania sposób tworzenia z fabryki danych.

> [!NOTE]
> Witaj potoku danych w tym samouczku przekształca dane wyjściowe tooproduce danych wejściowych. Nie kopiuje danych z magazynu danych źródła danych magazynu tooa docelowego. Samouczek na temat danych toocopy przy użyciu fabryki danych Azure, zobacz [samouczek: kopiowanie danych z magazynu obiektów Blob tooSQL bazy danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Powiązane z dwóch działań (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań. Szczegółowe informacje znajdują się w artykule [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) (Planowanie i wykonywanie w usłudze Data Factory). 





  
