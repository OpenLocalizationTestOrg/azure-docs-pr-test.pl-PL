---
title: "tooAzure aaaConnect usług Analysis Services przy użyciu usługi Power BI | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconnect tooan Azure Analysis Services serwera za pomocą usługi Power BI."
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
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: f6c4cdec6edb92900ad2e552e23a4d9172ba9b84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-power-bi"></a><span data-ttu-id="c2409-103">Uzyskuj dostęp do usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="c2409-103">Connect with Power BI</span></span>

<span data-ttu-id="c2409-104">Po utworzeniu serwera na platformie Azure i wdrożone tooit modelu tabelarycznego, użytkownicy w Twojej organizacji są gotowe tooconnect i rozpocząć eksplorowanie danych.</span><span class="sxs-lookup"><span data-stu-id="c2409-104">Once you've created a server in Azure, and deployed a tabular model tooit, users in your organization are ready tooconnect and begin exploring data.</span></span> 

> [!TIP]
> <span data-ttu-id="c2409-105">Czy toouse hello najnowszą wersję można [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="c2409-105">Be sure toouse hello latest version of [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span></span>
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a><span data-ttu-id="c2409-106">Połącz w programie Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="c2409-106">Connect in Power BI Desktop</span></span>

1. <span data-ttu-id="c2409-107">W programie Power BI Desktop, kliknij przycisk **Pobierz dane** > **Azure** > **usług Azure Analysis Service database**.</span><span class="sxs-lookup"><span data-stu-id="c2409-107">In Power BI Desktop, click **Get Data** > **Azure** > **Azure Analysis Services database**.</span></span>

2. <span data-ttu-id="c2409-108">W **serwera**, wprowadź nazwę serwera hello.</span><span class="sxs-lookup"><span data-stu-id="c2409-108">In **Server**, enter hello server name.</span></span> 
    
    <span data-ttu-id="c2409-109">Należy się tooinclude hello pełny adres URL.</span><span class="sxs-lookup"><span data-stu-id="c2409-109">Be sure tooinclude hello full URL.</span></span> <span data-ttu-id="c2409-110">Na przykład asazure://westcentralus.asazure.windows.net/advworks.</span><span class="sxs-lookup"><span data-stu-id="c2409-110">For example, asazure://westcentralus.asazure.windows.net/advworks.</span></span>

3. <span data-ttu-id="c2409-111">W **bazy danych**, jeśli znasz nazwę hello bazy danych modelu tabelarycznego hello lub perspektywy ma tooconnect do, wklej go tutaj.</span><span class="sxs-lookup"><span data-stu-id="c2409-111">In **Database**, if you know hello name of hello tabular model database or perspective you want tooconnect to, paste it here.</span></span> <span data-ttu-id="c2409-112">W przeciwnym razie można pozostawić to pole puste i wybierz bazę danych lub perspektywy później.</span><span class="sxs-lookup"><span data-stu-id="c2409-112">Otherwise, you can leave this field blank and select a database or perspective later.</span></span>

4. <span data-ttu-id="c2409-113">Pozostaw domyślną hello **połączenia na żywo** opcji, a następnie naciśnij klawisz **Connect**.</span><span class="sxs-lookup"><span data-stu-id="c2409-113">Leave hello default **Connect live** option, then press **Connect**.</span></span> 

5. <span data-ttu-id="c2409-114">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="c2409-114">If prompted, enter your login credentials.</span></span> 

6. <span data-ttu-id="c2409-115">W **Nawigator**, rozwiń węzeł serwera hello, a następnie wybierz hello model lub perspektywy ma tooconnect do, a następnie kliknij przycisk **Connect**.</span><span class="sxs-lookup"><span data-stu-id="c2409-115">In **Navigator**, expand hello server, then select hello model or perspective you want tooconnect to, then click **Connect**.</span></span> <span data-ttu-id="c2409-116">Kliknij przycisk tooshow modelu lub Perspektywa wszystkie obiekty hello tego widoku.</span><span class="sxs-lookup"><span data-stu-id="c2409-116">Click  a model or perspective tooshow all hello objects for that view.</span></span>

    <span data-ttu-id="c2409-117">Hello model zostanie otwarty w programie Power BI Desktop z pustym raportem w widoku raportu.</span><span class="sxs-lookup"><span data-stu-id="c2409-117">hello model opens in Power BI Desktop with a blank report in Report view.</span></span> <span data-ttu-id="c2409-118">Lista pól Hello Wyświetla wszystkie obiekty modelu ukryty.</span><span class="sxs-lookup"><span data-stu-id="c2409-118">hello Fields list displays all non-hidden model objects.</span></span> <span data-ttu-id="c2409-119">Stan połączenia jest wyświetlany w hello prawym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="c2409-119">Connection status is displayed in hello lower-right corner.</span></span>

## <a name="connect-in-power-bi-service"></a><span data-ttu-id="c2409-120">Połączenia w usłudze Power BI (usługa)</span><span class="sxs-lookup"><span data-stu-id="c2409-120">Connect in Power BI (service)</span></span>

1. <span data-ttu-id="c2409-121">Utwórz plik Power BI Desktop, który ma modelu tooyour połączenia na żywo na serwerze.</span><span class="sxs-lookup"><span data-stu-id="c2409-121">Create a Power BI Desktop file that has a live connection tooyour model on your server.</span></span>
2. <span data-ttu-id="c2409-122">W [usługi Power BI](https://powerbi.microsoft.com), kliknij przycisk **Pobierz dane** > **pliki**.</span><span class="sxs-lookup"><span data-stu-id="c2409-122">In [Power BI](https://powerbi.microsoft.com), click **Get Data** > **Files**.</span></span> <span data-ttu-id="c2409-123">Znajdź i zaznacz plik.</span><span class="sxs-lookup"><span data-stu-id="c2409-123">Locate and select your file.</span></span>



## <a name="see-also"></a><span data-ttu-id="c2409-124">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="c2409-124">See also</span></span>
<span data-ttu-id="c2409-125">[Połączenie usług analizy tooAzure](analysis-services-connect.md) </span><span class="sxs-lookup"><span data-stu-id="c2409-125">[Connect tooAzure Analysis Services](analysis-services-connect.md) </span></span>  
[<span data-ttu-id="c2409-126">Biblioteki klienta</span><span class="sxs-lookup"><span data-stu-id="c2409-126">Client libraries</span></span>](analysis-services-data-providers.md)

