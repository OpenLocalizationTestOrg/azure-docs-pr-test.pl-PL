---
title: "Korzystanie z usługi sieci Web Machine Learning z programu Excel | Dokumentacja firmy Microsoft"
description: "Korzystanie z usługi sieci Web Azure Machine Learning z programu Excel"
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
ms.assetid: 3f3cdd2f-1816-487e-ab78-530e01e9788f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/13/2017
ms.author: tedway
ms.openlocfilehash: 9f1aac04d54221888ee9374317be339400dcf085
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a><span data-ttu-id="b8301-103">Korzystanie z usługi sieci Web Azure Machine Learning z poziomu programu Excel</span><span class="sxs-lookup"><span data-stu-id="b8301-103">Consuming an Azure Machine Learning Web Service from Excel</span></span>
 <span data-ttu-id="b8301-104">Azure Machine Learning Studio ułatwia wywołują usługi sieci web bezpośrednio z programu Excel, bez konieczności pisania kodu.</span><span class="sxs-lookup"><span data-stu-id="b8301-104">Azure Machine Learning Studio makes it easy to call web services directly from Excel without the need to write any code.</span></span>

<span data-ttu-id="b8301-105">Jeśli używasz programu Excel 2013 (lub nowszy) lub aplikacji Excel Online, firma Microsoft zaleca użycie programu Excel [dodatek programu Excel](machine-learning-excel-add-in-for-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="b8301-105">If you are using Excel 2013 (or later) or Excel Online, then we recommend that you use the Excel [Excel add-in](machine-learning-excel-add-in-for-web-services.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a><span data-ttu-id="b8301-106">Kroki</span><span class="sxs-lookup"><span data-stu-id="b8301-106">Steps</span></span>
<span data-ttu-id="b8301-107">Publikowanie usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="b8301-107">Publish a web service.</span></span> <span data-ttu-id="b8301-108">[Ta strona](machine-learning-walkthrough-5-publish-web-service.md) wyjaśniono, jak to zrobić.</span><span class="sxs-lookup"><span data-stu-id="b8301-108">[This page](machine-learning-walkthrough-5-publish-web-service.md) explains how to do it.</span></span> <span data-ttu-id="b8301-109">Funkcja skoroszytu programu Excel jest obecnie obsługiwana tylko dla usług żądań i odpowiedzi, które mają jeden z (to znaczy pojedynczej oceniania etykiety).</span><span class="sxs-lookup"><span data-stu-id="b8301-109">Currently the Excel workbook feature is only supported for Request/Response services that have a single output (that is, a single scoring label).</span></span> 

<span data-ttu-id="b8301-110">Po utworzeniu usługi sieci web, kliknij **usług sieci WEB** studio po lewej stronie, a następnie wybierz usługę sieci web, aby korzystać z programu Excel.</span><span class="sxs-lookup"><span data-stu-id="b8301-110">Once you have a web service, click on the **WEB SERVICES** section on the left of the studio, and then select the web service to consume from Excel.</span></span>

<span data-ttu-id="b8301-111">**Usługa sieci Web klasycznego**</span><span class="sxs-lookup"><span data-stu-id="b8301-111">**Classic Web Service**</span></span>

1. <span data-ttu-id="b8301-112">Na **pulpitu NAWIGACYJNEGO** karcie dla usługi sieci web jest wiersz **żądanie/odpowiedź** usługi.</span><span class="sxs-lookup"><span data-stu-id="b8301-112">On the **DASHBOARD** tab for the web service is a row for the **REQUEST/RESPONSE** service.</span></span> <span data-ttu-id="b8301-113">Jeśli ta usługa miała pojedynczego wyjścia, powinny pojawić się **Pobierz skoroszyt programu Excel** łącza w tym wierszu.</span><span class="sxs-lookup"><span data-stu-id="b8301-113">If this service had a single output, you should see the **Download Excel Workbook** link in that row.</span></span>
   
    ![][1]
2. <span data-ttu-id="b8301-114">Polecenie **Pobierz skoroszyt programu Excel**.</span><span class="sxs-lookup"><span data-stu-id="b8301-114">Click on **Download Excel Workbook**.</span></span>

<span data-ttu-id="b8301-115">**Nowa usługa sieci Web**</span><span class="sxs-lookup"><span data-stu-id="b8301-115">**New Web Service**</span></span>

1. <span data-ttu-id="b8301-116">W portalu Azure Machine Learning sieci Web usługi wybierz **Consume**.</span><span class="sxs-lookup"><span data-stu-id="b8301-116">In the Azure Machine Learning Web Service portal, select **Consume**.</span></span>
2. <span data-ttu-id="b8301-117">Na stronie Consume w **opcje przez usługę sieci Web** sekcji, kliknij ikonę programu Excel.</span><span class="sxs-lookup"><span data-stu-id="b8301-117">On the Consume page, in the **Web service consumption options** section, click the Excel icon.</span></span>

<span data-ttu-id="b8301-118">**Używaj skoroszytu**</span><span class="sxs-lookup"><span data-stu-id="b8301-118">**Using the workbook**</span></span>

1. <span data-ttu-id="b8301-119">Otwórz skoroszyt.</span><span class="sxs-lookup"><span data-stu-id="b8301-119">Open the workbook.</span></span>
2. <span data-ttu-id="b8301-120">Zostanie wyświetlone ostrzeżenie o zabezpieczeniach; polecenie **Włącz edytowanie** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b8301-120">A Security Warning appears; click on the **Enable Editing** button.</span></span>
   
    ![][2]
3. <span data-ttu-id="b8301-121">Zostanie wyświetlone ostrzeżenie o zabezpieczeniach.</span><span class="sxs-lookup"><span data-stu-id="b8301-121">A Security Warning appears.</span></span> <span data-ttu-id="b8301-122">Polecenie **Włącz zawartość** przycisk, aby uruchomić makra w arkuszu kalkulacyjnym.</span><span class="sxs-lookup"><span data-stu-id="b8301-122">Click on the **Enable Content** button to run macros on your spreadsheet.</span></span>
   
    ![][3]
4. <span data-ttu-id="b8301-123">Po włączeniu makra, jest generowany tabeli.</span><span class="sxs-lookup"><span data-stu-id="b8301-123">Once macros are enabled, a table is generated.</span></span> <span data-ttu-id="b8301-124">Kolumny w niebieski są wymagane jako dane wejściowe do rekordów zasobów usługi sieci web, lub **parametry**.</span><span class="sxs-lookup"><span data-stu-id="b8301-124">Columns in blue are required as input into the RRS web service, or **PARAMETERS**.</span></span> <span data-ttu-id="b8301-125">Należy pamiętać, dane wyjściowe usługi RRS **PROGNOZOWANE wartości** na zielono.</span><span class="sxs-lookup"><span data-stu-id="b8301-125">Note the output of the RRS service, **PREDICTED VALUES** in green.</span></span> <span data-ttu-id="b8301-126">Po wprowadzeniu są wszystkie kolumny dla danego wiersza, skoroszyt automatycznie wywołuje interfejs API oceniania i wyświetla wyniki scored.</span><span class="sxs-lookup"><span data-stu-id="b8301-126">When all columns for a given row are filled, the workbook automatically calls the scoring API, and displays the scored results.</span></span>
   
    ![][4]
5. <span data-ttu-id="b8301-127">Aby otrzymać więcej niż jeden wiersz, wypełnienie drugiego wiersza z danymi i przewidywane wartości są tworzone.</span><span class="sxs-lookup"><span data-stu-id="b8301-127">To score more than one row, fill the second row with data and the predicted values are produced.</span></span> <span data-ttu-id="b8301-128">Jednocześnie można wkleić nawet kilka wierszy.</span><span class="sxs-lookup"><span data-stu-id="b8301-128">You can even paste several rows at once.</span></span>

<span data-ttu-id="b8301-129">Możesz ułatwiają dowolnej funkcji programu Excel (wykresy, mapy zasilania, warunkowego formatowania, itp.) z wartościami przewidywane wizualizacji danych.</span><span class="sxs-lookup"><span data-stu-id="b8301-129">You can use any of the Excel features (graphs, power map, conditional formatting, etc.) with the predicted values to help visualize the data.</span></span>    

## <a name="sharing-your-workbook"></a><span data-ttu-id="b8301-130">Udostępnianie skoroszytu</span><span class="sxs-lookup"><span data-stu-id="b8301-130">Sharing your workbook</span></span>
<span data-ttu-id="b8301-131">Makra do pracy klucz interfejsu API musi być częścią arkusza kalkulacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b8301-131">For the macros to work, your API Key must be part of the spreadsheet.</span></span> <span data-ttu-id="b8301-132">Oznacza to, że tylko z jednostek/osób, którym ufa powinny współużytkować skoroszytu.</span><span class="sxs-lookup"><span data-stu-id="b8301-132">That means that you should share the workbook only with entities/individuals you trust.</span></span>

## <a name="automatic-updates"></a><span data-ttu-id="b8301-133">Automatyczne aktualizacje</span><span class="sxs-lookup"><span data-stu-id="b8301-133">Automatic updates</span></span>
<span data-ttu-id="b8301-134">Rekordy zasobów wywołanie w tych dwóch sytuacji:</span><span class="sxs-lookup"><span data-stu-id="b8301-134">An RRS call is made in these two situations:</span></span>

1. <span data-ttu-id="b8301-135">Po raz pierwszy wiersz ma zawartość we wszystkich jego **parametrów**</span><span class="sxs-lookup"><span data-stu-id="b8301-135">The first time a row has content in all of its **PARAMETERS**</span></span>
2. <span data-ttu-id="b8301-136">Wtedy żadnego z **parametry** zmiany w wierszu, który ma wszystkie jego **parametry** wprowadzona.</span><span class="sxs-lookup"><span data-stu-id="b8301-136">Any time any of the **PARAMETERS** changes in a row that had all of its **PARAMETERS** entered.</span></span>

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
