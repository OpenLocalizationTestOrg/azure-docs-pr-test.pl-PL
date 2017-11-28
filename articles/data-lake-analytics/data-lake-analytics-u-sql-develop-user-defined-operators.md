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
# <a name="develop-u-sql-user-defined-operators-udos"></a><span data-ttu-id="c8fcd-103">Opracowywanie operatorów języka U-SQL zdefiniowane przez użytkownika (udo)</span><span class="sxs-lookup"><span data-stu-id="c8fcd-103">Develop U-SQL user-defined operators (UDOs)</span></span>
<span data-ttu-id="c8fcd-104">Dowiedz się, jak toodevelop zdefiniowane przez użytkownika operatory tooprocess danych w ramach zadania skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c8fcd-104">Learn how toodevelop user-defined operators tooprocess data in a U-SQL job.</span></span>

<span data-ttu-id="c8fcd-105">Aby uzyskać instrukcje na temat tworzenia ogólnego przeznaczenia zestawy dla U-SQL, zobacz [zestawy opracowanie U-SQL dla zadania usługi Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md)</span><span class="sxs-lookup"><span data-stu-id="c8fcd-105">For instructions on developing general-purpose assemblies for U-SQL, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md)</span></span>

## <a name="define-and-use-a-user-defined-operator-in-u-sql"></a><span data-ttu-id="c8fcd-106">Definiowanie i użycie operatora zdefiniowanej przez użytkownika w języku U-SQL</span><span class="sxs-lookup"><span data-stu-id="c8fcd-106">Define and use a user-defined operator in U-SQL</span></span>
<span data-ttu-id="c8fcd-107">**toocreate i przedstawia zadania skryptu U-SQL**</span><span class="sxs-lookup"><span data-stu-id="c8fcd-107">**toocreate and submit a U-SQL job**</span></span>

1. <span data-ttu-id="c8fcd-108">Z hello Visual Studio wybierz **Plik > Nowy > Projekt > Projekt U-SQL**.</span><span class="sxs-lookup"><span data-stu-id="c8fcd-108">From hello Visual Studio select **File > New > Project > U-SQL Project**.</span></span>
2. <span data-ttu-id="c8fcd-109">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c8fcd-109">Click **OK**.</span></span> <span data-ttu-id="c8fcd-110">Visual Studio tworzy rozwiązanie z plikiem Script.usql.</span><span class="sxs-lookup"><span data-stu-id="c8fcd-110">Visual Studio creates a solution with a Script.usql file.</span></span>
3. <span data-ttu-id="c8fcd-111">Z **Eksploratora rozwiązań**, rozwiń Script.usql, a następnie kliknij dwukrotnie ikonę **Script.usql.cs**.</span><span class="sxs-lookup"><span data-stu-id="c8fcd-111">From **Solution Explorer**, expand Script.usql, and then double-click **Script.usql.cs**.</span></span>
4. <span data-ttu-id="c8fcd-112">Wklej powitania po kod do pliku hello:</span><span class="sxs-lookup"><span data-stu-id="c8fcd-112">Paste hello following code into hello file:</span></span>

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
6. <span data-ttu-id="c8fcd-113">Otwórz **Script.usql**, i Wklej hello następującego skryptu U-SQL:</span><span class="sxs-lookup"><span data-stu-id="c8fcd-113">Open **Script.usql**, and paste hello following U-SQL script:</span></span>

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
7. <span data-ttu-id="c8fcd-114">Określ konto usługi Data Lake Analytics hello, bazy danych i schematu.</span><span class="sxs-lookup"><span data-stu-id="c8fcd-114">Specify hello Data Lake Analytics account, Database, and Schema.</span></span>
8. <span data-ttu-id="c8fcd-115">W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy pozycję **Script.usql**, a następnie kliknij pozycję **Build Script** (Kompiluj skrypt).</span><span class="sxs-lookup"><span data-stu-id="c8fcd-115">From **Solution Explorer**, right-click **Script.usql**, and then click **Build Script**.</span></span>
9. <span data-ttu-id="c8fcd-116">W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy pozycję **Script.usql**, a następnie kliknij pozycję **Submit Script** (Prześlij skrypt).</span><span class="sxs-lookup"><span data-stu-id="c8fcd-116">From **Solution Explorer**, right-click **Script.usql**, and then click **Submit Script**.</span></span>
10. <span data-ttu-id="c8fcd-117">Jeśli nie nawiązywano połączenia tooyour subskrypcji platformy Azure, będzie można tooenter zostanie wyświetlony monit o poświadczenia konta Azure.</span><span class="sxs-lookup"><span data-stu-id="c8fcd-117">If you haven't connected tooyour Azure subscription, you will be prompted tooenter your Azure account credentials.</span></span>
11. <span data-ttu-id="c8fcd-118">Kliknij przycisk **przesłać**.</span><span class="sxs-lookup"><span data-stu-id="c8fcd-118">Click **Submit**.</span></span> <span data-ttu-id="c8fcd-119">Wyniki przesyłania i link do zadania są dostępne w oknie wyników powitania po zakończeniu przesyłania hello.</span><span class="sxs-lookup"><span data-stu-id="c8fcd-119">Submission results and job link are available in hello Results window when hello submission is completed.</span></span>
12. <span data-ttu-id="c8fcd-120">Kliknij przycisk hello **Odśwież** przycisk toosee hello najnowszego zadania stanu i Odśwież hello ekranu.</span><span class="sxs-lookup"><span data-stu-id="c8fcd-120">Click hello **Refresh** button toosee hello latest job status and refresh hello screen.</span></span>

<span data-ttu-id="c8fcd-121">**dane wyjściowe hello toosee**</span><span class="sxs-lookup"><span data-stu-id="c8fcd-121">**toosee hello output**</span></span>

1. <span data-ttu-id="c8fcd-122">Z **Eksploratora serwera**, rozwiń węzeł **Azure**, rozwiń węzeł **usługi Data Lake Analytics**, rozwiń konto usługi Data Lake Analytics, rozwiń węzeł **kont magazynu**, kliknij prawym przyciskiem myszy hello domyślny magazyn, a następnie kliknij przycisk **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="c8fcd-122">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click hello Default Storage, and then click **Explorer**.</span></span>
2. <span data-ttu-id="c8fcd-123">Rozwiń węzeł próbek, rozwiń dane wyjściowe, a następnie kliknij dwukrotnie ikonę **Drivers.csv**.</span><span class="sxs-lookup"><span data-stu-id="c8fcd-123">Expand Samples, expand Outputs, and then double-click **Drivers.csv**.</span></span>

## <a name="see-also"></a><span data-ttu-id="c8fcd-124">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="c8fcd-124">See also</span></span>
* [<span data-ttu-id="c8fcd-125">Wprowadzenie do usługi Data Lake Analytics przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8fcd-125">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="c8fcd-126">Wprowadzenie do usługi Data Lake Analytics przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c8fcd-126">Get started with Data Lake Analytics using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="c8fcd-127">Użyj narzędzi Data Lake Tools dla programu Visual Studio do tworzenia aplikacji U-SQL</span><span class="sxs-lookup"><span data-stu-id="c8fcd-127">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
