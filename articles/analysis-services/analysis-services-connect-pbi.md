---
title: "Połączenie do usług Azure Analysis Services przy użyciu usługi Power BI | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak połączyć się z serwerem usług Analysis Services dla platformy Azure przy użyciu usługi Power BI."
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
ms.openlocfilehash: 3a2af043feddb4a1d6d63f50e838c8a39035449f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="connect-with-power-bi"></a><span data-ttu-id="5c7da-103">Uzyskuj dostęp do usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="5c7da-103">Connect with Power BI</span></span>

<span data-ttu-id="5c7da-104">Po utworzeniu serwera na platformie Azure i wdrożone modelu tabelarycznego, użytkownicy w Twojej organizacji są gotowe do łączenia i rozpocząć eksplorowanie danych.</span><span class="sxs-lookup"><span data-stu-id="5c7da-104">Once you've created a server in Azure, and deployed a tabular model to it, users in your organization are ready to connect and begin exploring data.</span></span> 

> [!TIP]
> <span data-ttu-id="5c7da-105">Pamiętaj używać najnowszej wersji [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="5c7da-105">Be sure to use the latest version of [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span></span>
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a><span data-ttu-id="5c7da-106">Połącz w programie Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="5c7da-106">Connect in Power BI Desktop</span></span>

1. <span data-ttu-id="5c7da-107">W programie Power BI Desktop, kliknij przycisk **Pobierz dane** > **Azure** > **usług Azure Analysis Service database**.</span><span class="sxs-lookup"><span data-stu-id="5c7da-107">In Power BI Desktop, click **Get Data** > **Azure** > **Azure Analysis Services database**.</span></span>

2. <span data-ttu-id="5c7da-108">W **serwera**, wprowadź nazwę serwera.</span><span class="sxs-lookup"><span data-stu-id="5c7da-108">In **Server**, enter the server name.</span></span> 
    
    <span data-ttu-id="5c7da-109">Należy uwzględnić pełny adres URL.</span><span class="sxs-lookup"><span data-stu-id="5c7da-109">Be sure to include the full URL.</span></span> <span data-ttu-id="5c7da-110">Na przykład asazure://westcentralus.asazure.windows.net/advworks.</span><span class="sxs-lookup"><span data-stu-id="5c7da-110">For example, asazure://westcentralus.asazure.windows.net/advworks.</span></span>

3. <span data-ttu-id="5c7da-111">W **bazy danych**, jeśli znasz nazwę bazy danych modelu tabelarycznego lub perspektywy, aby nawiązać połączenie, wklej go tutaj.</span><span class="sxs-lookup"><span data-stu-id="5c7da-111">In **Database**, if you know the name of the tabular model database or perspective you want to connect to, paste it here.</span></span> <span data-ttu-id="5c7da-112">W przeciwnym razie można pozostawić to pole puste i wybierz bazę danych lub perspektywy później.</span><span class="sxs-lookup"><span data-stu-id="5c7da-112">Otherwise, you can leave this field blank and select a database or perspective later.</span></span>

4. <span data-ttu-id="5c7da-113">Pozostaw wartość domyślną **połączenia na żywo** opcji, a następnie naciśnij klawisz **Connect**.</span><span class="sxs-lookup"><span data-stu-id="5c7da-113">Leave the default **Connect live** option, then press **Connect**.</span></span> 

5. <span data-ttu-id="5c7da-114">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="5c7da-114">If prompted, enter your login credentials.</span></span> 

6. <span data-ttu-id="5c7da-115">W **Nawigator**, rozwiń węzeł serwera, a następnie wybierz model lub chcesz nawiązać połączenie, następnie kliknij przycisk perspektywy **Connect**.</span><span class="sxs-lookup"><span data-stu-id="5c7da-115">In **Navigator**, expand the server, then select the model or perspective you want to connect to, then click **Connect**.</span></span> <span data-ttu-id="5c7da-116">Kliknij modelu lub perspektywy, aby wyświetlić wszystkie obiekty w tym widoku.</span><span class="sxs-lookup"><span data-stu-id="5c7da-116">Click  a model or perspective to show all the objects for that view.</span></span>

    <span data-ttu-id="5c7da-117">Model zostanie otwarty w programie Power BI Desktop z pustym raportem w widoku raportu.</span><span class="sxs-lookup"><span data-stu-id="5c7da-117">The model opens in Power BI Desktop with a blank report in Report view.</span></span> <span data-ttu-id="5c7da-118">Na liście pól Wyświetla wszystkie obiekty modelu ukryty.</span><span class="sxs-lookup"><span data-stu-id="5c7da-118">The Fields list displays all non-hidden model objects.</span></span> <span data-ttu-id="5c7da-119">Stan połączenia jest wyświetlany w prawym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="5c7da-119">Connection status is displayed in the lower-right corner.</span></span>

## <a name="connect-in-power-bi-service"></a><span data-ttu-id="5c7da-120">Połączenia w usłudze Power BI (usługa)</span><span class="sxs-lookup"><span data-stu-id="5c7da-120">Connect in Power BI (service)</span></span>

1. <span data-ttu-id="5c7da-121">Utwórz plik Power BI Desktop, który ma aktywne połączenie modelu na serwerze.</span><span class="sxs-lookup"><span data-stu-id="5c7da-121">Create a Power BI Desktop file that has a live connection to your model on your server.</span></span>
2. <span data-ttu-id="5c7da-122">W [usługi Power BI](https://powerbi.microsoft.com), kliknij przycisk **Pobierz dane** > **pliki**.</span><span class="sxs-lookup"><span data-stu-id="5c7da-122">In [Power BI](https://powerbi.microsoft.com), click **Get Data** > **Files**.</span></span> <span data-ttu-id="5c7da-123">Znajdź i zaznacz plik.</span><span class="sxs-lookup"><span data-stu-id="5c7da-123">Locate and select your file.</span></span>



## <a name="see-also"></a><span data-ttu-id="5c7da-124">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="5c7da-124">See also</span></span>
<span data-ttu-id="5c7da-125">[Połącz do usług Azure Analysis Services](analysis-services-connect.md) </span><span class="sxs-lookup"><span data-stu-id="5c7da-125">[Connect to Azure Analysis Services](analysis-services-connect.md) </span></span>  
[<span data-ttu-id="5c7da-126">Biblioteki klienta</span><span class="sxs-lookup"><span data-stu-id="5c7da-126">Client libraries</span></span>](analysis-services-data-providers.md)

