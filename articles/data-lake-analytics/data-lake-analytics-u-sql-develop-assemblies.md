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
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a><span data-ttu-id="409fb-103">Tworzenie zestawów języka U-SQL do zadania usługi Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="409fb-103">Develop U-SQL assemblies for Azure Data Lake Analytics jobs</span></span>
<span data-ttu-id="409fb-104">Dowiedz się, jak tooturn kodu powiązanego do toobe zestawy używane i użyć ponownie w zadań usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="409fb-104">Learn how tooturn code-behind into assemblies toobe used and reused in Data Lake Analytics jobs.</span></span> 

<span data-ttu-id="409fb-105">U-SQL umożliwia łatwe tooadd własnego niestandardowego kodu w językach .net, takich jak C#, VB.Net lub F #.</span><span class="sxs-lookup"><span data-stu-id="409fb-105">U-SQL makes it easy tooadd your own custom code in .Net languages, such as C#, VB.Net or F#.</span></span> <span data-ttu-id="409fb-106">Można nawet wdrażać własne toosupport środowiska wykonawczego innych języków.</span><span class="sxs-lookup"><span data-stu-id="409fb-106">You can even deploy your own runtime toosupport other languages.</span></span>

<span data-ttu-id="409fb-107">kod niestandardowy Hello Najprostszym sposobem toouse jest toouse hello narzędzi Data Lake Tools dla Visual Studio możliwości związane z kodem.</span><span class="sxs-lookup"><span data-stu-id="409fb-107">hello easiest way toouse custom code is toouse hello Data Lake Tools for Visual Studio’s code-behind capabilities.</span></span> <span data-ttu-id="409fb-108">Aby uzyskać więcej informacji, zobacz [samouczek: tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="409fb-108">For more information, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="409fb-109">Istnieje kilka wady używania związane z kodem:</span><span class="sxs-lookup"><span data-stu-id="409fb-109">There are a few drawbacks of using code-behind:</span></span>

- <span data-ttu-id="409fb-110">Kod źródłowy Hello pobiera przekazać wszystkich przesłanych danych skryptu.</span><span class="sxs-lookup"><span data-stu-id="409fb-110">hello source code gets uploaded for every script submission.</span></span>
- <span data-ttu-id="409fb-111">związane z kodem nie mogą być udostępniane przez inne zadania.</span><span class="sxs-lookup"><span data-stu-id="409fb-111">code-behind cannot be shared with other jobs.</span></span>

<span data-ttu-id="409fb-112">tooaddress te wady włączyć kodu powiązanego do zestawów i zarejestrować hello zestawy toohello usługi Data Lake Analytics katalogu.</span><span class="sxs-lookup"><span data-stu-id="409fb-112">tooaddress these drawbacks, you can turn code-behind into assemblies, and register hello assemblies toohello Data Lake Analytics catalog.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="409fb-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="409fb-113">Prerequisites</span></span>
* <span data-ttu-id="409fb-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 update 4 lub Visual Studio 2012 z zainstalowany program Visual C++</span><span class="sxs-lookup"><span data-stu-id="409fb-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed</span></span>
* <span data-ttu-id="409fb-115">Microsoft Azure SDK dla platformy .NET w wersji 2.5 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="409fb-115">Microsoft Azure SDK for .NET version 2.5 or above.</span></span>  <span data-ttu-id="409fb-116">Instalowanie przy użyciu Instalatora platformy sieci Web hello lub Instalator programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="409fb-116">Install it using hello Web platform installer or Visual Studio Installer</span></span>
* <span data-ttu-id="409fb-117">Konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="409fb-117">A Data Lake Analytics account.</span></span>  <span data-ttu-id="409fb-118">Zobacz temat [Rozpoczynanie pracy z usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="409fb-118">See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="409fb-119">Przejdź przez hello [wprowadzenie do usługi Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="409fb-119">Go through hello [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.</span></span>
* <span data-ttu-id="409fb-120">Połącz tooAzure.</span><span class="sxs-lookup"><span data-stu-id="409fb-120">Connect tooAzure.</span></span>
* <span data-ttu-id="409fb-121">Przekazywanie hello źródła danych, zobacz [wprowadzenie do usługi Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="409fb-121">Upload hello source data, see [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span></span> 

## <a name="develop-assemblies-for-u-sql"></a><span data-ttu-id="409fb-122">Tworzenie zestawów dla U-SQL</span><span class="sxs-lookup"><span data-stu-id="409fb-122">Develop assemblies for U-SQL</span></span>

<span data-ttu-id="409fb-123">**toocreate i przedstawia zadania skryptu U-SQL**</span><span class="sxs-lookup"><span data-stu-id="409fb-123">**toocreate and submit a U-SQL job**</span></span>

1. <span data-ttu-id="409fb-124">Z hello **pliku** menu, kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**.</span><span class="sxs-lookup"><span data-stu-id="409fb-124">From hello **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="409fb-125">Rozwiń węzeł **zainstalowana**, **szablony**, **usługi Azure Data Lake**, **U-SQL(ADLA)**, wybierz pozycję hello **biblioteki klas (dla U-SQL Aplikacja)** szablonu, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="409fb-125">Expand **Installed**, **Templates**, **Azure Data Lake**, **U-SQL(ADLA)**, select hello **Class Library (For U-SQL Application)** template, and then click **OK**.</span></span>
3. <span data-ttu-id="409fb-126">Wpisz swój kod w Class1.cs.</span><span class="sxs-lookup"><span data-stu-id="409fb-126">Write your code in Class1.cs.</span></span>  <span data-ttu-id="409fb-127">Witaj poniżej przedstawiono przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="409fb-127">hello following is a code sample.</span></span>

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
4. <span data-ttu-id="409fb-128">Kliknij przycisk hello **kompilacji** menu, a następnie kliknij przycisk **Kompiluj rozwiązanie** toocreate hello dll.</span><span class="sxs-lookup"><span data-stu-id="409fb-128">Click hello **Build** menu, and then click **Build Solution** toocreate hello dll.</span></span>

## <a name="register-assemblies"></a><span data-ttu-id="409fb-129">Rejestrowanie zestawów</span><span class="sxs-lookup"><span data-stu-id="409fb-129">Register assemblies</span></span>

<span data-ttu-id="409fb-130">Zobacz [Analytics(U-SQL) Lake danych użyj katalogu](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="409fb-130">See [Use Data Lake Analytics(U-SQL) catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>


## <a name="use-hello-assemblies"></a><span data-ttu-id="409fb-131">Korzystanie z zestawów hello</span><span class="sxs-lookup"><span data-stu-id="409fb-131">Use hello assemblies</span></span>

<span data-ttu-id="409fb-132">Zobacz [Użyj hello Azure Data Lake Tools dla Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="409fb-132">See [Use hello Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="409fb-133">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="409fb-133">See also</span></span>
* [<span data-ttu-id="409fb-134">Wprowadzenie do usługi Data Lake Analytics przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="409fb-134">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="409fb-135">Wprowadzenie do usługi Data Lake Analytics przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="409fb-135">Get started with Data Lake Analytics using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="409fb-136">Użyj narzędzi Data Lake Tools dla programu Visual Studio do tworzenia aplikacji U-SQL</span><span class="sxs-lookup"><span data-stu-id="409fb-136">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="409fb-137">Użyj Data Lake Analytics(U-SQL) katalogu</span><span class="sxs-lookup"><span data-stu-id="409fb-137">Use Data Lake Analytics(U-SQL) catalog</span></span>](data-lake-analytics-use-u-sql-catalog.md)
* [<span data-ttu-id="409fb-138">Użyj hello Azure Data Lake Tools dla Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="409fb-138">Use hello Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
