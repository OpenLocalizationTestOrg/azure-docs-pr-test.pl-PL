---
title: "aaaGet Started with Azure Data Lake Analytics przy użyciu portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć zadanie usługi Data Lake Analytics przy użyciu języka U-SQL toouse hello Azure toocreate portalu konta usługi Data Lake Analytics i przesłać zadanie hello. "
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: b1584d16-e0d2-4019-ad1f-f04be8c5b430
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: edmaca
ms.openlocfilehash: 6bb54404fa42cfed25b18bc2bfb7c72e6c361149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a>Rozpoczynanie pracy z usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Dowiedz się, jak toouse hello Azure toocreate portalu konta usługi Azure Data Lake Analytics, definiowania zadań w [U-SQL](data-lake-analytics-u-sql-get-started.md)i przesyłanie usługi Data Lake Analytics toohello zadania. Więcej informacji na temat usługi Data Lake Analytics można znaleźć w artykule [Omówienie usługi Azure Data Lake Analytics](data-lake-analytics-overview.md).

## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem tego samouczka musisz dysponować **subskrypcją platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="create-a-data-lake-analytics-account"></a>Tworzenie konta Data Lake Analytics

Teraz utworzysz usługi Data Lake Analytics i Data Lake Store konta na powitania sam czas.  Ten krok jest proste i trwa tylko około toofinish 60 sekund.

1. Zaloguj się na toohello [portalu Azure](https://portal.azure.com).
2. Kliknij pozycję **Nowy** >  **Dane + analiza** > **Data Lake Analytics**.
3. Wybierz wartości hello następujące elementy:
   * **Nazwa**: nazwa konta usługi Data Lake Analytics (dozwolone są tylko małe litery i cyfry).
   * **Subskrypcja**: Wybierz hello subskrypcja platformy Azure używana na potrzeby hello konta usługi Analytics.
   * **Grupa zasobów**. Wybierz istniejącą grupę zasobów platformy Azure lub utwórz nową.
   * **Lokalizacja**. Wybierz centrum danych platformy Azure dla konta usługi Data Lake Analytics hello.
   * **Data Lake Store**: wykonaj hello instrukcji toocreate nowe konto usługi Data Lake Store lub wybierz istniejący. 
4. Opcjonalnie wybierz warstwę cenową dla konta usługi Data Lake Analytics.
5. Kliknij przycisk **Utwórz**. 


## <a name="your-first-u-sql-script"></a>Pierwszy skrypt U-SQL

Witaj następującego tekstu jest bardzo prosty skrypt U-SQL. Wszystko robi to zdefiniować małym zestawie danych skryptu hello, a następnie wpisz tego zestawu danych wychodzących toohello domyślne Data Lake Store jako plik o nazwie `/data.csv`.

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

## <a name="submit-a-u-sql-job"></a>Przesyłanie zadania U-SQL

1. Hello konta usługi Data Lake Analytics kliknij **nowe zadanie**.
2. Wklej tekst hello hello powyższy skrypt U-SQL. 
3. Kliknij przycisk **Prześlij zadanie**.   
4. Czekać do momentu zmiany stanu zadania hello zbyt**zakończyło się pomyślnie**.
5. Jeśli zadanie hello nie powiodło się, zobacz [monitorowanie zadań usługi Data Lake Analytics i rozwiązywanie problemów](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).
6. Kliknij przycisk hello **dane wyjściowe** , a następnie kliknij pozycję `data.csv`. 

## <a name="see-also"></a>Zobacz też

* tooget Rozpoczęto tworzenie aplikacji U-SQL, zobacz [skryptów U-SQL opracowanie przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
* toolearn U-SQL, zobacz [wprowadzenie do języka Azure Data Lake Analytics U-SQL](data-lake-analytics-u-sql-get-started.md).
* Informacje o zadaniach zarządzania znajdziesz w artykule [Zarządzanie usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal](data-lake-analytics-manage-use-portal.md).
