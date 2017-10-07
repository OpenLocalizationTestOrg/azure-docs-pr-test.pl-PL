---
title: "Operatory zdefiniowane przez użytkownika aaaDevelop U-SQL (udo) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodevelop toobe operatory zdefiniowane przez użytkownika używane i użyć ponownie w usługi Data Lake Analytics zadania. "
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: e5189e4e-9438-46d1-8686-ed4836bf3356
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 6b86618efd3751cd9a5e91875879d7dd6d6a7b02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-user-defined-operators-udos"></a>Opracowywanie operatorów języka U-SQL zdefiniowane przez użytkownika (udo)
Dowiedz się, jak toodevelop zdefiniowane przez użytkownika operatory tooprocess danych w ramach zadania skryptu U-SQL.

Aby uzyskać instrukcje na temat tworzenia ogólnego przeznaczenia zestawy dla U-SQL, zobacz [zestawy opracowanie U-SQL dla zadania usługi Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md)

## <a name="define-and-use-a-user-defined-operator-in-u-sql"></a>Definiowanie i użycie operatora zdefiniowanej przez użytkownika w języku U-SQL
**toocreate i przedstawia zadania skryptu U-SQL**

1. Z hello Visual Studio wybierz **Plik > Nowy > Projekt > Projekt U-SQL**.
2. Kliknij przycisk **OK**. Visual Studio tworzy rozwiązanie z plikiem Script.usql.
3. Z **Eksploratora rozwiązań**, rozwiń Script.usql, a następnie kliknij dwukrotnie ikonę **Script.usql.cs**.
4. Wklej powitania po kod do pliku hello:

        using Microsoft.Analytics.Interfaces;
        using System.Collections.Generic;

        namespace USQL_UDO
        {
            public class CountryName : IProcessor
            {
                private static IDictionary<string, string> CountryTranslation = new Dictionary<string, string>
                {
                    {
                        "Deutschland", "Germany"
                    },
                    {
                        "Suisse", "Switzerland"
                    },
                    {
                        "UK", "United Kingdom"
                    },
                    {
                        "USA", "United States of America"
                    },
                    {
                        "中国", "PR China"
                    }
                };

                public override IRow Process(IRow input, IUpdatableRow output)
                {

                    string UserID = input.Get<string>("UserID");
                    string Name = input.Get<string>("Name");
                    string Address = input.Get<string>("Address");
                    string City = input.Get<string>("City");
                    string State = input.Get<string>("State");
                    string PostalCode = input.Get<string>("PostalCode");
                    string Country = input.Get<string>("Country");
                    string Phone = input.Get<string>("Phone");

                    if (CountryTranslation.Keys.Contains(Country))
                    {
                        Country = CountryTranslation[Country];
                    }
                    output.Set<string>(0, UserID);
                    output.Set<string>(1, Name);
                    output.Set<string>(2, Address);
                    output.Set<string>(3, City);
                    output.Set<string>(4, State);
                    output.Set<string>(5, PostalCode);
                    output.Set<string>(6, Country);
                    output.Set<string>(7, Phone);

                    return output.AsReadOnly();
                }
            }
        }
6. Otwórz **Script.usql**, i Wklej hello następującego skryptu U-SQL:

        @drivers =
            EXTRACT UserID      string,
                    Name        string,
                    Address     string,
                    City        string,
                    State       string,
                    PostalCode  string,
                    Country     string,
                    Phone       string
            FROM "/Samples/Data/AmbulanceData/Drivers.txt"
            USING Extractors.Tsv(Encoding.Unicode);

        @drivers_CountryName =
            PROCESS @drivers
            PRODUCE UserID string,
                    Name string,
                    Address string,
                    City string,
                    State string,
                    PostalCode string,
                    Country string,
                    Phone string
            USING new USQL_UDO.CountryName();    

        OUTPUT @drivers_CountryName
            too"/Samples/Outputs/Drivers.csv"
            USING Outputters.Csv(Encoding.Unicode);
7. Określ konto usługi Data Lake Analytics hello, bazy danych i schematu.
8. W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy pozycję **Script.usql**, a następnie kliknij pozycję **Build Script** (Kompiluj skrypt).
9. W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy pozycję **Script.usql**, a następnie kliknij pozycję **Submit Script** (Prześlij skrypt).
10. Jeśli nie nawiązywano połączenia tooyour subskrypcji platformy Azure, będzie można tooenter zostanie wyświetlony monit o poświadczenia konta Azure.
11. Kliknij przycisk **przesłać**. Wyniki przesyłania i link do zadania są dostępne w oknie wyników powitania po zakończeniu przesyłania hello.
12. Kliknij przycisk hello **Odśwież** przycisk toosee hello najnowszego zadania stanu i Odśwież hello ekranu.

**dane wyjściowe hello toosee**

1. Z **Eksploratora serwera**, rozwiń węzeł **Azure**, rozwiń węzeł **usługi Data Lake Analytics**, rozwiń konto usługi Data Lake Analytics, rozwiń węzeł **kont magazynu**, kliknij prawym przyciskiem myszy hello domyślny magazyn, a następnie kliknij przycisk **Explorer**.
2. Rozwiń węzeł próbek, rozwiń dane wyjściowe, a następnie kliknij dwukrotnie ikonę **Drivers.csv**.

## <a name="see-also"></a>Zobacz też
* [Wprowadzenie do usługi Data Lake Analytics przy użyciu programu PowerShell](data-lake-analytics-get-started-powershell.md)
* [Wprowadzenie do usługi Data Lake Analytics przy użyciu hello portalu Azure](data-lake-analytics-get-started-portal.md)
* [Użyj narzędzi Data Lake Tools dla programu Visual Studio do tworzenia aplikacji U-SQL](data-lake-analytics-data-lake-tools-get-started.md)
