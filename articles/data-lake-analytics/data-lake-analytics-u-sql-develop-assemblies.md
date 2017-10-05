---
title: "Tworzenie zestawów języka U-SQL do zadania usługi Azure Data Lake Analytics | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć zestawy używanych i użyć ponownie w zadań usługi Data Lake Analytics. "
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
ms.openlocfilehash: c49f80f8dcd330d7f46726241e7178351b9cc28f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a><span data-ttu-id="be740-103">Tworzenie zestawów języka U-SQL do zadania usługi Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="be740-103">Develop U-SQL assemblies for Azure Data Lake Analytics jobs</span></span>
<span data-ttu-id="be740-104">Dowiedz się, jak włączyć kodu powiązanego do zestawów używanych i użyć ponownie w zadań usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="be740-104">Learn how to turn code-behind into assemblies to be used and reused in Data Lake Analytics jobs.</span></span> 

<span data-ttu-id="be740-105">U-SQL ułatwia dodawanie niestandardowego kodu w językach .net, takich jak C#, VB.Net lub F #.</span><span class="sxs-lookup"><span data-stu-id="be740-105">U-SQL makes it easy to add your own custom code in .Net languages, such as C#, VB.Net or F#.</span></span> <span data-ttu-id="be740-106">Można nawet wdrażanie własnego środowiska uruchomieniowego do obsługi innych języków.</span><span class="sxs-lookup"><span data-stu-id="be740-106">You can even deploy your own runtime to support other languages.</span></span>

<span data-ttu-id="be740-107">Najprostszym sposobem, aby użyć niestandardowego kodu jest do użycia narzędzi Data Lake Tools dla Visual Studio możliwości związane z kodem.</span><span class="sxs-lookup"><span data-stu-id="be740-107">The easiest way to use custom code is to use the Data Lake Tools for Visual Studio’s code-behind capabilities.</span></span> <span data-ttu-id="be740-108">Aby uzyskać więcej informacji, zobacz [samouczek: tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="be740-108">For more information, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="be740-109">Istnieje kilka wady używania związane z kodem:</span><span class="sxs-lookup"><span data-stu-id="be740-109">There are a few drawbacks of using code-behind:</span></span>

- <span data-ttu-id="be740-110">Kod źródłowy pobiera przekazany do przesłania każdego skryptu.</span><span class="sxs-lookup"><span data-stu-id="be740-110">The source code gets uploaded for every script submission.</span></span>
- <span data-ttu-id="be740-111">związane z kodem nie mogą być udostępniane przez inne zadania.</span><span class="sxs-lookup"><span data-stu-id="be740-111">code-behind cannot be shared with other jobs.</span></span>

<span data-ttu-id="be740-112">Aby rozwiązać te wady, można włączyć kodu powiązanego do zestawów i zarejestruj zestawy do katalogu Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="be740-112">To address these drawbacks, you can turn code-behind into assemblies, and register the assemblies to the Data Lake Analytics catalog.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be740-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="be740-113">Prerequisites</span></span>
* <span data-ttu-id="be740-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 update 4 lub Visual Studio 2012 z zainstalowany program Visual C++</span><span class="sxs-lookup"><span data-stu-id="be740-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed</span></span>
* <span data-ttu-id="be740-115">Microsoft Azure SDK dla platformy .NET w wersji 2.5 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="be740-115">Microsoft Azure SDK for .NET version 2.5 or above.</span></span>  <span data-ttu-id="be740-116">Instalowanie przy użyciu Instalatora platformy sieci Web lub Instalator programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="be740-116">Install it using the Web platform installer or Visual Studio Installer</span></span>
* <span data-ttu-id="be740-117">Konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="be740-117">A Data Lake Analytics account.</span></span>  <span data-ttu-id="be740-118">Zobacz temat [Rozpoczynanie pracy z usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="be740-118">See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="be740-119">Przejdź przez [wprowadzenie do usługi Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="be740-119">Go through the [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.</span></span>
* <span data-ttu-id="be740-120">Połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="be740-120">Connect to Azure.</span></span>
* <span data-ttu-id="be740-121">Przekaż źródło danych, zobacz [wprowadzenie do usługi Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="be740-121">Upload the source data, see [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span></span> 

## <a name="develop-assemblies-for-u-sql"></a><span data-ttu-id="be740-122">Tworzenie zestawów dla U-SQL</span><span class="sxs-lookup"><span data-stu-id="be740-122">Develop assemblies for U-SQL</span></span>

<span data-ttu-id="be740-123">**Aby utworzyć i przesłać zadanie U-SQL**</span><span class="sxs-lookup"><span data-stu-id="be740-123">**To create and submit a U-SQL job**</span></span>

1. <span data-ttu-id="be740-124">W menu **Plik** kliknij pozycję **Nowy**, a następnie kliknij pozycję **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="be740-124">From the **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="be740-125">Rozwiń węzeł **zainstalowana**, **szablony**, **usługi Azure Data Lake**, **U-SQL(ADLA)**, wybierz pozycję **biblioteki klas (dla aplikacji U-SQL)** szablonu, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="be740-125">Expand **Installed**, **Templates**, **Azure Data Lake**, **U-SQL(ADLA)**, select the **Class Library (For U-SQL Application)** template, and then click **OK**.</span></span>
3. <span data-ttu-id="be740-126">Wpisz swój kod w Class1.cs.</span><span class="sxs-lookup"><span data-stu-id="be740-126">Write your code in Class1.cs.</span></span>  <span data-ttu-id="be740-127">Poniżej przedstawiono przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="be740-127">The following is a code sample.</span></span>

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
4. <span data-ttu-id="be740-128">Kliknij przycisk **kompilacji** menu, a następnie kliknij przycisk **Kompiluj rozwiązanie** do tworzenia biblioteki dll.</span><span class="sxs-lookup"><span data-stu-id="be740-128">Click the **Build** menu, and then click **Build Solution** to create the dll.</span></span>

## <a name="register-assemblies"></a><span data-ttu-id="be740-129">Rejestrowanie zestawów</span><span class="sxs-lookup"><span data-stu-id="be740-129">Register assemblies</span></span>

<span data-ttu-id="be740-130">Zobacz [Analytics(U-SQL) Lake danych użyj katalogu](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="be740-130">See [Use Data Lake Analytics(U-SQL) catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>


## <a name="use-the-assemblies"></a><span data-ttu-id="be740-131">Korzystanie z zestawów</span><span class="sxs-lookup"><span data-stu-id="be740-131">Use the assemblies</span></span>

<span data-ttu-id="be740-132">Zobacz [użycia usługi Azure Data Lake Tools dla programu Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="be740-132">See [Use the Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="be740-133">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="be740-133">See also</span></span>
* [<span data-ttu-id="be740-134">Wprowadzenie do usługi Data Lake Analytics przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="be740-134">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="be740-135">Wprowadzenie do usługi Data Lake Analytics przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="be740-135">Get started with Data Lake Analytics using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="be740-136">Użyj narzędzi Data Lake Tools dla programu Visual Studio do tworzenia aplikacji U-SQL</span><span class="sxs-lookup"><span data-stu-id="be740-136">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="be740-137">Użyj Data Lake Analytics(U-SQL) katalogu</span><span class="sxs-lookup"><span data-stu-id="be740-137">Use Data Lake Analytics(U-SQL) catalog</span></span>](data-lake-analytics-use-u-sql-catalog.md)
* [<span data-ttu-id="be740-138">Korzystanie z narzędzi Azure Data Lake Tools for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="be740-138">Use the Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)