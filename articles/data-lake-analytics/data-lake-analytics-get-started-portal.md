---
title: "Rozpoczynanie pracy z usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal | Microsoft Docs"
description: "Poznaj sposoby tworzenia konta usługi Data Lake Analytics przy użyciu witryny Azure Portal, tworzenia zadania usługi Data Lake Analytics przy użyciu języka U-SQL oraz przesyłania zadania. "
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
ms.openlocfilehash: 2722a2d72ed90ea0005362563ecaee30750c040a
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a>Rozpoczynanie pracy z usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Poznaj sposoby tworzenia kont usługi Azure Data Lake Analytics przy użyciu witryny Azure Portal, definiowania zadań w języku [U-SQL](data-lake-analytics-u-sql-get-started.md) oraz przesyłania zadań do usługi Data Lake Analytics. Więcej informacji na temat usługi Data Lake Analytics można znaleźć w artykule [Omówienie usługi Azure Data Lake Analytics](data-lake-analytics-overview.md).

## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem tego samouczka musisz dysponować **subskrypcją platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="create-a-data-lake-analytics-account"></a>Tworzenie konta Data Lake Analytics

Teraz nastąpi równoczesne utworzenie kont Data Lake Analytics oraz Data Lake Store.  Ten krok jest prosty i jego wykonanie zajmuje tylko około 60 sekund.

1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).
2. Kliknij pozycję **Nowy** >  **Dane + analiza** > **Data Lake Analytics**.
3. Wybierz wartości dla następujących elementów:
   * **Nazwa**: nazwa konta usługi Data Lake Analytics (dozwolone są tylko małe litery i cyfry).
   * **Subskrypcja**: wybierz subskrypcję platformy Azure używaną na potrzeby konta usługi Analytics.
   * **Grupa zasobów**. Wybierz istniejącą grupę zasobów platformy Azure lub utwórz nową.
   * **Lokalizacja**. Wybierz centrum danych platformy Azure na potrzeby konta usługi Data Lake Analytics.
   * **Data Lake Store**: postępuj zgodnie z instrukcjami, aby utworzyć nowe konto usługi Data Lake Store lub wybierz istniejące konto. 
4. Opcjonalnie wybierz warstwę cenową dla konta usługi Data Lake Analytics.
5. Kliknij przycisk **Utwórz**. 


## <a name="your-first-u-sql-script"></a>Pierwszy skrypt U-SQL

Poniższy tekst to bardzo prosty skrypt U-SQL. Ma on za zadanie tylko definiowanie małego zestawu danych w skrypcie, a następnie wpisanie tego zestawu danych do domyślnej usługi Data Lake Store jako pliku o nazwie `/data.csv`.

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
```

## <a name="submit-a-u-sql-job"></a>Przesyłanie zadania U-SQL

1. Na koncie usługi Data Lake Analytics kliknij pozycję **Nowe zadanie**.
2. Wklej tekst skryptu U-SQL przedstawiony powyżej. 
3. Kliknij przycisk **Prześlij zadanie**.   
4. Zaczekaj, aż stan zadania zmieni się na **Powodzenie**.
5. Jeśli zadanie zakończyło się niepowodzeniem, zobacz temat [Monitor and troubleshoot Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md) (Monitorowanie zadań usługi Data Lake Analytics i rozwiązywanie problemów).
6. Kliknij kartę **Dane wyjściowe**, a następnie kliknij pozycję `data.csv`. 

## <a name="see-also"></a>Zobacz też

* Aby rozpocząć tworzenie aplikacji w języku U-SQL, zobacz artykuł [Tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools dla Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
* Aby dowiedzieć się więcej o języku U-SQL, zobacz [Wprowadzenie do języka U-SQL w usłudze Azure Data Lake Analytics](data-lake-analytics-u-sql-get-started.md).
* Informacje o zadaniach zarządzania znajdziesz w artykule [Zarządzanie usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal](data-lake-analytics-manage-use-portal.md).
