---
title: "aaaCreate modelu tabelarycznego przy użyciu narzędzia Projektant sieci Web Azure Analysis Services hello | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate modelu tabelarycznego usług Azure Analysis Services przy użyciu hello Projektant stron sieci Web w portalu Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: a37b326b76c84fc3a4300827bc1c8706b0584701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-model-in-azure-portal"></a><span data-ttu-id="9da44-103">Tworzenie modelu w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9da44-103">Create a model in Azure portal</span></span>

<span data-ttu-id="9da44-104">Funkcja Hello Azure Analysis Services web projektanta (wersja zapoznawcza) w portalu Azure zapewnia toocreate szybka i łatwa metoda i Edytuj modele tabelaryczne i zapytania modelu danych bezpośrednio w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="9da44-104">hello Azure Analysis Services web designer (preview) feature in Azure portal provides a quick and easy way toocreate and edit tabular models and query model data right in your browser.</span></span> 

<span data-ttu-id="9da44-105">Należy pamiętać, Projektant hello jest **Podgląd**.</span><span class="sxs-lookup"><span data-stu-id="9da44-105">Keep in mind, hello web designer is **preview**.</span></span> <span data-ttu-id="9da44-106">Gdy nowych funkcji jest dodawany cały czas hello, w wersji zapoznawczej, funkcje są ograniczone.</span><span class="sxs-lookup"><span data-stu-id="9da44-106">While new functionality is being added all hello time, in preview, functionality is limited.</span></span> <span data-ttu-id="9da44-107">Do bardziej zaawansowanego modelu programowania i testowania jest najlepszym toouse programu Visual Studio (SSDT) i SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="9da44-107">For more advanced model development and testing, it's best toouse Visual Studio (SSDT) and SQL Server Management Studio (SSMS).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9da44-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9da44-108">Prerequisites</span></span>

- <span data-ttu-id="9da44-109">Serwer usług Azure Analysis Services na powitania warstwy standardowa lub dewelopera.</span><span class="sxs-lookup"><span data-stu-id="9da44-109">An Azure Analysis Services server at hello Standard or Developer tier.</span></span> <span data-ttu-id="9da44-110">Nowe modele utworzone przy użyciu narzędzia Projektant sieci Web hello są zapytania bezpośredniego, obsługiwane tylko przez te warstwy.</span><span class="sxs-lookup"><span data-stu-id="9da44-110">New models created by using hello Web designer are DirectQuery, supported only by these tiers.</span></span>
- <span data-ttu-id="9da44-111">Baza danych SQL Azure, Magazyn danych SQL Azure lub pliku Power BI Desktop (pbix) jako źródła danych.</span><span class="sxs-lookup"><span data-stu-id="9da44-111">An Azure SQL Database, Azure SQL Data Warehouse, or Power BI Desktop (.pbix) file as a datasource.</span></span> <span data-ttu-id="9da44-112">Nowe modele utworzone na podstawie obsługi plików bazy danych SQL Azure, Magazyn danych SQL Azure, Oracle i Teradata Power BI Desktop źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="9da44-112">New models created from Power BI Desktop files support Azure SQL Database, Azure SQL Data Warehouse, Oracle, and Teradata data sources.</span></span>
- <span data-ttu-id="9da44-113">Konto programu SQL Server i hasła do łączenia tooAzure źródeł danych bazy danych SQL lub magazyn danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9da44-113">A SQL Server account and password for connecting tooAzure SQL Database or Azure SQL Data Warehouse data sources.</span></span>

## <a name="toocreate-a-new-tabular-model"></a><span data-ttu-id="9da44-114">toocreate nowego modelu tabelarycznego</span><span class="sxs-lookup"><span data-stu-id="9da44-114">toocreate a new tabular model</span></span>

1. <span data-ttu-id="9da44-115">Znajdujących się na serwerze **omówienie** bloku > **Projektant stron sieci Web**, kliknij przycisk **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="9da44-115">In your server's **Overview** blade > **Web designer**, click **Open**.</span></span>

    ![Tworzenie modelu w portalu Azure](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. <span data-ttu-id="9da44-117">W **Projektant stron sieci Web** > **modele**, kliknij przycisk **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="9da44-117">In **Web designer** > **Models**, click **+ Add**.</span></span>

    ![Tworzenie modelu w portalu Azure](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. <span data-ttu-id="9da44-119">W **nowy model**, wpisz nazwę modelu, a następnie wybierz źródło danych.</span><span class="sxs-lookup"><span data-stu-id="9da44-119">In **New model**, type a model name, and then select a data source.</span></span>

    ![Okno dialogowe nowego modelu w portalu Azure](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. <span data-ttu-id="9da44-121">W **Connect**, wprowadź właściwości połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="9da44-121">In **Connect**, enter hello connection properties.</span></span> <span data-ttu-id="9da44-122">Nazwa użytkownika i hasło musi być kontem programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9da44-122">Username and password must be a SQL Server account.</span></span>

     ![Połącz okna dialogowego w portalu Azure](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. <span data-ttu-id="9da44-124">W **tabele i widoki**wybierz hello tooinclude tabele w modelu, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9da44-124">In **Tables and views**, select hello tables tooinclude in your model, and then click **Create**.</span></span> <span data-ttu-id="9da44-125">Automatycznie tworzyć relacji między tabelami w pary kluczy.</span><span class="sxs-lookup"><span data-stu-id="9da44-125">Relationships are created automatically between tables with a key pair.</span></span>

     ![Wybierz tabele i widoki](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

<span data-ttu-id="9da44-127">Nowy model zostanie wyświetlona w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="9da44-127">Your new model appears in your browser.</span></span> <span data-ttu-id="9da44-128">W tym miejscu można wykonywać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9da44-128">From here, you can:</span></span>   

- <span data-ttu-id="9da44-129">Zapytania danych modelu, przeciągając projektanta zapytań toohello pól i dodawanie filtrów.</span><span class="sxs-lookup"><span data-stu-id="9da44-129">Query model data by dragging fields toohello query designer and adding filters.</span></span>
- <span data-ttu-id="9da44-130">Utwórz nowe miary w tabelach.</span><span class="sxs-lookup"><span data-stu-id="9da44-130">Create new measures in tables.</span></span>
- <span data-ttu-id="9da44-131">Edytowanie metadanych modelu przy użyciu edytora json hello.</span><span class="sxs-lookup"><span data-stu-id="9da44-131">Edit model metadata by using hello json editor.</span></span>
- <span data-ttu-id="9da44-132">Otwórz hello modelu w programie Visual Studio (SSDT), Power BI Desktop lub programu Excel.</span><span class="sxs-lookup"><span data-stu-id="9da44-132">Open hello model in Visual Studio (SSDT), Power BI Desktop, or Excel.</span></span>

![Wybierz tabele i widoki](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> <span data-ttu-id="9da44-134">Podczas edytowania metadanych modelu lub utworzyć nowe miary w przeglądarce, model tooyour te zmiany są zapisywane na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9da44-134">When you edit model metadata or create new measures in your browser, you're saving those changes tooyour model in Azure.</span></span> <span data-ttu-id="9da44-135">Jeśli pracujesz także do modelu w SSDT, Power BI Desktop lub programu Excel, modelu można uzyskać zsynchronizowane.</span><span class="sxs-lookup"><span data-stu-id="9da44-135">If you're also working on your model in SSDT, Power BI Desktop, or Excel, your model can get out of sync.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9da44-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9da44-136">Next steps</span></span> 
[<span data-ttu-id="9da44-137">Zarządzanie ról bazy danych i użytkowników</span><span class="sxs-lookup"><span data-stu-id="9da44-137">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="9da44-138">Łączenie z programem Excel</span><span class="sxs-lookup"><span data-stu-id="9da44-138">Connect with Excel</span></span>](analysis-services-connect-excel.md)  


