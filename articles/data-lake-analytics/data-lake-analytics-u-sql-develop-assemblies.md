---
title: "zestawy aaaDevelop U-SQL dla zadania usługi Azure Data Lake Analytics | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toobe zestawy toodevelop używane i użyć ponownie w usługi Data Lake Analytics zadania. "
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/30/2016
ms.author: jejiang
ms.openlocfilehash: 86dd17b25e0967306ed36bb5b7f3178d9409d53d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a>Tworzenie zestawów języka U-SQL do zadania usługi Azure Data Lake Analytics
Dowiedz się, jak tooturn kodu powiązanego do toobe zestawy używane i użyć ponownie w zadań usługi Data Lake Analytics. 

U-SQL umożliwia łatwe tooadd własnego niestandardowego kodu w językach .net, takich jak C#, VB.Net lub F #. Można nawet wdrażać własne toosupport środowiska wykonawczego innych języków.

kod niestandardowy Hello Najprostszym sposobem toouse jest toouse hello narzędzi Data Lake Tools dla Visual Studio możliwości związane z kodem. Aby uzyskać więcej informacji, zobacz [samouczek: tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-get-started.md). Istnieje kilka wady używania związane z kodem:

- Kod źródłowy Hello pobiera przekazać wszystkich przesłanych danych skryptu.
- związane z kodem nie mogą być udostępniane przez inne zadania.

tooaddress te wady włączyć kodu powiązanego do zestawów i zarejestrować hello zestawy toohello usługi Data Lake Analytics katalogu.

## <a name="prerequisites"></a>Wymagania wstępne
* Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 update 4 lub Visual Studio 2012 z zainstalowany program Visual C++
* Microsoft Azure SDK dla platformy .NET w wersji 2.5 lub nowszej.  Instalowanie przy użyciu Instalatora platformy sieci Web hello lub Instalator programu Visual Studio
* Konto usługi Data Lake Analytics.  Zobacz temat [Rozpoczynanie pracy z usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal](data-lake-analytics-get-started-portal.md).
* Przejdź przez hello [wprowadzenie do usługi Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) samouczka.
* Połącz tooAzure.
* Przekazywanie hello źródła danych, zobacz [wprowadzenie do usługi Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md). 

## <a name="develop-assemblies-for-u-sql"></a>Tworzenie zestawów dla U-SQL

**toocreate i przedstawia zadania skryptu U-SQL**

1. Z hello **pliku** menu, kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**.
2. Rozwiń węzeł **zainstalowana**, **szablony**, **usługi Azure Data Lake**, **U-SQL(ADLA)**, wybierz pozycję hello **biblioteki klas (dla U-SQL Aplikacja)** szablonu, a następnie kliknij przycisk **OK**.
3. Wpisz swój kod w Class1.cs.  Witaj poniżej przedstawiono przykładowy kod.

        using Microsoft.Analytics.Interfaces;

        namespace USQLApplication_codebehind
        {
            [SqlUserDefinedProcessor]
            public class MyProcessor : IProcessor
            {
                public override IRow Process(IRow input, IUpdatableRow output)
                {
                    output.Set(0, input.Get<string>(0));
                    output.Set(0, input.Get<string>(0));
                    return output.AsReadOnly();
                }
            }
        }
4. Kliknij przycisk hello **kompilacji** menu, a następnie kliknij przycisk **Kompiluj rozwiązanie** toocreate hello dll.

## <a name="register-assemblies"></a>Rejestrowanie zestawów

Zobacz [Analytics(U-SQL) Lake danych użyj katalogu](data-lake-analytics-use-u-sql-catalog.md).


## <a name="use-hello-assemblies"></a>Korzystanie z zestawów hello

Zobacz [Użyj hello Azure Data Lake Tools dla Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).

## <a name="see-also"></a>Zobacz też
* [Wprowadzenie do usługi Data Lake Analytics przy użyciu programu PowerShell](data-lake-analytics-get-started-powershell.md)
* [Wprowadzenie do usługi Data Lake Analytics przy użyciu hello portalu Azure](data-lake-analytics-get-started-portal.md)
* [Użyj narzędzi Data Lake Tools dla programu Visual Studio do tworzenia aplikacji U-SQL](data-lake-analytics-data-lake-tools-get-started.md)
* [Użyj Data Lake Analytics(U-SQL) katalogu](data-lake-analytics-use-u-sql-catalog.md)
* [Użyj hello Azure Data Lake Tools dla Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md)
