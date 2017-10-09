---
title: "aaaTroubleshoot zadania usługi Azure Data Lake Analytics przy użyciu portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello zadania usługi Data Lake Analytics tootroubleshoot portalu Azure. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: b7066d81-3142-474f-8a34-32b0b39656dc
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: e810d56bab8f1a8254721ec9906bb6a4508dc22a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a>Rozwiązywanie problemów z zadania usługi Azure Data Lake Analytics przy użyciu portalu Azure
Dowiedz się, jak toouse hello zadania usługi Data Lake Analytics tootroubleshoot portalu Azure.

W tym samouczku będzie skonfigurować Brak problem plik źródłowy i stosować problem hello tootroubleshoot hello w portalu Azure.

## <a name="submit-a-data-lake-analytics-job"></a>Przesyłanie zadania usługi Data Lake Analytics

Prześlij hello następujące zadania skryptu U-SQL:

```
@searchlog =
   EXTRACT UserId          int,
           Start           DateTime,
           Region          string,
           Query           string,
           Duration        int?,
           Urls            string,
           ClickedUrls     string
   FROM "/Samples/Data/SearchLog.tsv1"
   USING Extractors.Tsv();

OUTPUT @searchlog   
   too"/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
Witaj plik źródłowy zdefiniowana w skrypcie hello jest **/Samples/Data/SearchLog.tsv1**, gdzie powinien być **/Samples/Data/SearchLog.tsv**.


## <a name="troubleshoot-hello-job"></a>Rozwiązywanie problemów z hello zadania

**toosee hello wszystkich zadań**

1. Witaj portalu Azure kliknij **Microsoft Azure** w lewym górnym rogu hello.
2. Kliknij Kafelek hello nazwą konta usługi Data Lake Analytics.  Witaj zadania podsumowania jest wyświetlany na powitania **zadania zarządzania** kafelka.

    ![Zarządzanie zadaniami usługi Azure Data Lake Analytics](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    Hello zadania zarządzania zapewnia podstawowe informacje o stanie zadania hello. Należy zauważyć, że zadania nie powiodło się.
3. Kliknij przycisk hello **zadania zarządzania** kafelka toosee hello zadania. Witaj zadania są podzielone na **systemem**, **w kolejce**, i **zakończone**. Zostanie wyświetlona nieudane zadania hello **zakończone** sekcji. Jest ona pierwszego hello na liście. Jeśli masz wiele zadań, można kliknąć **filtru** toohelp można toolocate zadania.

    ![Usługa Azure Data Lake Analytics filtrowania zadań](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. Kliknij zadanie zakończone niepowodzeniem hello z hello listy tooopen hello szczegóły zadania w nowym bloku:

    ![Azure Data Lake Analytics zadania nie powiodło się](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    Powiadomienie hello **ponownie prześlij** przycisku. Po rozwiązaniu problemu hello można przesłać ponownie hello zadania.
5. Kliknij przycisk wyróżnione części z hello poprzedniej zrzut ekranu tooopen hello szczegóły błędu.  Zostanie wyświetlona wyglądać mniej więcej tak:

    ![Azure Data Lake Analytics szczegóły zadania nie powiodło się](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    Określa się, że nie można odnaleźć folderu źródłowego hello.
6. Kliknij przycisk **zduplikowane skryptu**.
7. Aktualizacja hello **FROM** ścieżka toohello poniżej:

    "/ Samples/Data/SearchLog.tsv"
8. Kliknij przycisk **Prześlij zadanie**.

## <a name="see-also"></a>Zobacz też
* [Omówienie programu Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Wprowadzenie do usługi Azure Data Lake Analytics przy użyciu programu Azure PowerShell](data-lake-analytics-get-started-powershell.md)
* [Rozpoczynanie pracy z usługą Azure Data Lake Analytics i języka U-SQL przy użyciu programu Visual Studio](data-lake-analytics-u-sql-get-started.md)
* [Zarządzanie usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal](data-lake-analytics-manage-use-portal.md)
