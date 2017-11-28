---
title: "Usługa sieci Web Machine Learning z programu Excel aaaConsume | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: e2e8bbf7ba75b6618a0285539555ce175ec03c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a><span data-ttu-id="75fe7-103">Korzystanie z usługi sieci Web Azure Machine Learning z poziomu programu Excel</span><span class="sxs-lookup"><span data-stu-id="75fe7-103">Consuming an Azure Machine Learning Web Service from Excel</span></span>
 <span data-ttu-id="75fe7-104">Azure Machine Learning Studio umożliwia łatwe toocall usług sieci web bezpośrednio z programu Excel bez hello muszą toowrite żadnego kodu.</span><span class="sxs-lookup"><span data-stu-id="75fe7-104">Azure Machine Learning Studio makes it easy toocall web services directly from Excel without hello need toowrite any code.</span></span>

<span data-ttu-id="75fe7-105">Jeśli używasz programu Excel 2013 (lub nowszy) lub aplikacji Excel Online, a następnie zalecane jest użycie hello Excel [dodatek programu Excel](machine-learning-excel-add-in-for-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="75fe7-105">If you are using Excel 2013 (or later) or Excel Online, then we recommend that you use hello Excel [Excel add-in](machine-learning-excel-add-in-for-web-services.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a><span data-ttu-id="75fe7-106">Kroki</span><span class="sxs-lookup"><span data-stu-id="75fe7-106">Steps</span></span>
<span data-ttu-id="75fe7-107">Publikowanie usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="75fe7-107">Publish a web service.</span></span> <span data-ttu-id="75fe7-108">[Ta strona](machine-learning-walkthrough-5-publish-web-service.md) wyjaśniono, jak toodo go.</span><span class="sxs-lookup"><span data-stu-id="75fe7-108">[This page](machine-learning-walkthrough-5-publish-web-service.md) explains how toodo it.</span></span> <span data-ttu-id="75fe7-109">Obecnie funkcja skoroszytu programu Excel hello jest obsługiwana tylko dla usług żądań i odpowiedzi, które mają jeden z (to znaczy pojedynczej oceniania etykiety).</span><span class="sxs-lookup"><span data-stu-id="75fe7-109">Currently hello Excel workbook feature is only supported for Request/Response services that have a single output (that is, a single scoring label).</span></span> 

<span data-ttu-id="75fe7-110">Po utworzeniu usługi sieci web, kliknij na powitania **usług sieci WEB** po lewej stronie powitania hello Studio, a następnie wybierz tooconsume usługi sieci web hello z programu Excel.</span><span class="sxs-lookup"><span data-stu-id="75fe7-110">Once you have a web service, click on hello **WEB SERVICES** section on hello left of hello studio, and then select hello web service tooconsume from Excel.</span></span>

<span data-ttu-id="75fe7-111">**Usługa sieci Web klasycznego**</span><span class="sxs-lookup"><span data-stu-id="75fe7-111">**Classic Web Service**</span></span>

1. <span data-ttu-id="75fe7-112">Na powitania **pulpitu NAWIGACYJNEGO** karcie dla usługi sieci web hello jest wiersz hello **żądanie/odpowiedź** usługi.</span><span class="sxs-lookup"><span data-stu-id="75fe7-112">On hello **DASHBOARD** tab for hello web service is a row for hello **REQUEST/RESPONSE** service.</span></span> <span data-ttu-id="75fe7-113">Jeśli ta usługa miała pojedynczego wyjścia, powinny pojawić się hello **Pobierz skoroszyt programu Excel** łącza w tym wierszu.</span><span class="sxs-lookup"><span data-stu-id="75fe7-113">If this service had a single output, you should see hello **Download Excel Workbook** link in that row.</span></span>
   
    ![][1]
2. <span data-ttu-id="75fe7-114">Polecenie **Pobierz skoroszyt programu Excel**.</span><span class="sxs-lookup"><span data-stu-id="75fe7-114">Click on **Download Excel Workbook**.</span></span>

<span data-ttu-id="75fe7-115">**Nowa usługa sieci Web**</span><span class="sxs-lookup"><span data-stu-id="75fe7-115">**New Web Service**</span></span>

1. <span data-ttu-id="75fe7-116">Hello Azure Machine Learning sieci Web portalu, wybierz **Consume**.</span><span class="sxs-lookup"><span data-stu-id="75fe7-116">In hello Azure Machine Learning Web Service portal, select **Consume**.</span></span>
2. <span data-ttu-id="75fe7-117">Na stronie Consume hello na powitania **opcje przez usługę sieci Web** kliknij ikonę hello w programie Excel.</span><span class="sxs-lookup"><span data-stu-id="75fe7-117">On hello Consume page, in hello **Web service consumption options** section, click hello Excel icon.</span></span>

<span data-ttu-id="75fe7-118">**Przy użyciu hello skoroszytu**</span><span class="sxs-lookup"><span data-stu-id="75fe7-118">**Using hello workbook**</span></span>

1. <span data-ttu-id="75fe7-119">Otwórz hello skoroszytu.</span><span class="sxs-lookup"><span data-stu-id="75fe7-119">Open hello workbook.</span></span>
2. <span data-ttu-id="75fe7-120">Zostanie wyświetlone ostrzeżenie o zabezpieczeniach; polecenie hello **Włącz edytowanie** przycisku.</span><span class="sxs-lookup"><span data-stu-id="75fe7-120">A Security Warning appears; click on hello **Enable Editing** button.</span></span>
   
    ![][2]
3. <span data-ttu-id="75fe7-121">Zostanie wyświetlone ostrzeżenie o zabezpieczeniach.</span><span class="sxs-lookup"><span data-stu-id="75fe7-121">A Security Warning appears.</span></span> <span data-ttu-id="75fe7-122">Polecenie hello **Włącz zawartość** przycisk toorun makra w arkuszu kalkulacyjnym.</span><span class="sxs-lookup"><span data-stu-id="75fe7-122">Click on hello **Enable Content** button toorun macros on your spreadsheet.</span></span>
   
    ![][3]
4. <span data-ttu-id="75fe7-123">Po włączeniu makra, jest generowany tabeli.</span><span class="sxs-lookup"><span data-stu-id="75fe7-123">Once macros are enabled, a table is generated.</span></span> <span data-ttu-id="75fe7-124">Kolumny w niebieski są wymagane jako dane wejściowe do hello rekordy zasobów usługi sieci web, lub **parametry**.</span><span class="sxs-lookup"><span data-stu-id="75fe7-124">Columns in blue are required as input into hello RRS web service, or **PARAMETERS**.</span></span> <span data-ttu-id="75fe7-125">Należy pamiętać, dane wyjściowe hello hello usługi RRS **PROGNOZOWANE wartości** na zielono.</span><span class="sxs-lookup"><span data-stu-id="75fe7-125">Note hello output of hello RRS service, **PREDICTED VALUES** in green.</span></span> <span data-ttu-id="75fe7-126">Jeśli są wszystkie kolumny dla danego wiersza, skoroszytu hello automatycznie wywołuje hello oceniania interfejsu API i wyświetla hello oceniane wyniki.</span><span class="sxs-lookup"><span data-stu-id="75fe7-126">When all columns for a given row are filled, hello workbook automatically calls hello scoring API, and displays hello scored results.</span></span>
   
    ![][4]
5. <span data-ttu-id="75fe7-127">tooscore więcej niż jeden wiersz, wypełnienie hello drugiego wiersza z danymi i hello przewidzieć, że wartości.</span><span class="sxs-lookup"><span data-stu-id="75fe7-127">tooscore more than one row, fill hello second row with data and hello predicted values are produced.</span></span> <span data-ttu-id="75fe7-128">Jednocześnie można wkleić nawet kilka wierszy.</span><span class="sxs-lookup"><span data-stu-id="75fe7-128">You can even paste several rows at once.</span></span>

<span data-ttu-id="75fe7-129">Można użyć dowolnego z funkcji programu Excel hello (wykresy, mapy zasilania, warunkowego formatowania itp.) z hello przewidzieć toohelp wartości wizualizacji danych hello.</span><span class="sxs-lookup"><span data-stu-id="75fe7-129">You can use any of hello Excel features (graphs, power map, conditional formatting, etc.) with hello predicted values toohelp visualize hello data.</span></span>    

## <a name="sharing-your-workbook"></a><span data-ttu-id="75fe7-130">Udostępnianie skoroszytu</span><span class="sxs-lookup"><span data-stu-id="75fe7-130">Sharing your workbook</span></span>
<span data-ttu-id="75fe7-131">Dla hello toowork makra klucz interfejsu API musi być częścią hello w arkuszu kalkulacyjnym.</span><span class="sxs-lookup"><span data-stu-id="75fe7-131">For hello macros toowork, your API Key must be part of hello spreadsheet.</span></span> <span data-ttu-id="75fe7-132">Oznacza to, że tylko z jednostek/osób, którym ufa powinny współużytkować hello skoroszytu.</span><span class="sxs-lookup"><span data-stu-id="75fe7-132">That means that you should share hello workbook only with entities/individuals you trust.</span></span>

## <a name="automatic-updates"></a><span data-ttu-id="75fe7-133">Automatyczne aktualizacje</span><span class="sxs-lookup"><span data-stu-id="75fe7-133">Automatic updates</span></span>
<span data-ttu-id="75fe7-134">Rekordy zasobów wywołanie w tych dwóch sytuacji:</span><span class="sxs-lookup"><span data-stu-id="75fe7-134">An RRS call is made in these two situations:</span></span>

1. <span data-ttu-id="75fe7-135">Witaj po raz pierwszy wiersz ma zawartość we wszystkich jego **parametrów**</span><span class="sxs-lookup"><span data-stu-id="75fe7-135">hello first time a row has content in all of its **PARAMETERS**</span></span>
2. <span data-ttu-id="75fe7-136">Wtedy żadnego hello **parametry** zmiany w wierszu, który ma wszystkie jego **parametry** wprowadzona.</span><span class="sxs-lookup"><span data-stu-id="75fe7-136">Any time any of hello **PARAMETERS** changes in a row that had all of its **PARAMETERS** entered.</span></span>

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
