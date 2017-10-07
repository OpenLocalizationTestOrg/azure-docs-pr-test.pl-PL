---
title: "aaaDeploy tooAzure usług Analysis Services przy użyciu narzędzi SSDT | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy tooan modelu tabelarycznego Azure Analysis Services serwera za pomocą narzędzi SSDT."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 5f1f0ae7-11de-4923-a3da-888b13a3638c
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: e3f3771fe32a37b9e0173c274080c647152edd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-model-from-ssdt"></a><span data-ttu-id="118b6-103">Wdrażanie modelu w programie SSDT</span><span class="sxs-lookup"><span data-stu-id="118b6-103">Deploy a model from SSDT</span></span>
<span data-ttu-id="118b6-104">Po utworzeniu serwera w ramach subskrypcji platformy Azure, wszystko jest gotowe toodeploy tooit bazy danych modelu tabelarycznego.</span><span class="sxs-lookup"><span data-stu-id="118b6-104">Once you've created a server in your Azure subscription, you're ready toodeploy a tabular model database tooit.</span></span> <span data-ttu-id="118b6-105">Można użyć programu SQL Server Data Tools (SSDT) toobuild i Wdróż projekt modelu tabelarycznego, nad którymi pracuje.</span><span class="sxs-lookup"><span data-stu-id="118b6-105">You can use SQL Server Data Tools (SSDT) toobuild and deploy a tabular model project you're working on.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="118b6-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="118b6-106">Prerequisites</span></span>
<span data-ttu-id="118b6-107">Rozpoczęto tooget, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="118b6-107">tooget started, you need:</span></span>

* <span data-ttu-id="118b6-108">**Serwer usług Analysis Services** na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="118b6-108">**Analysis Services server** in Azure.</span></span> <span data-ttu-id="118b6-109">toolearn więcej, zobacz [Tworzenie serwera usług Azure Analysis Services](analysis-services-create-server.md).</span><span class="sxs-lookup"><span data-stu-id="118b6-109">toolearn more, see [Create an Azure Analysis Services server](analysis-services-create-server.md).</span></span>
* <span data-ttu-id="118b6-110">**Projekt modelu tabelarycznego** SSDT lub istniejącego modelu tabelarycznego na powitania 1200 lub wyższym poziomie zgodności.</span><span class="sxs-lookup"><span data-stu-id="118b6-110">**Tabular model project** in SSDT or an existing tabular model at hello 1200 or higher compatibility level.</span></span> <span data-ttu-id="118b6-111">Nie wiesz, jak go utworzyć?</span><span class="sxs-lookup"><span data-stu-id="118b6-111">Never created one?</span></span> <span data-ttu-id="118b6-112">Spróbuj hello [samouczek sprzedaży modelowania tabelarycznym Adventure Works Internet](https://msdn.microsoft.com/library/hh231691.aspx).</span><span class="sxs-lookup"><span data-stu-id="118b6-112">Try hello [Adventure Works Internet sales tabular modeling tutorial](https://msdn.microsoft.com/library/hh231691.aspx).</span></span>
* <span data-ttu-id="118b6-113">**Brama lokalna** — Jeśli co najmniej jedno źródło danych lokalnych w sieci organizacji, należy tooinstall [bramy danych lokalnych](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="118b6-113">**On-premises gateway** - If one or more data sources are on-premises in your organization's network, you need tooinstall an [On-premises data gateway](analysis-services-gateway.md).</span></span> <span data-ttu-id="118b6-114">Brama Hello jest niezbędne, tooyour danych źródeł tooprocess i odświeżania danych lokalnych w modelu hello połączenia z serwerem w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="118b6-114">hello gateway is necessary for your server in hello cloud connect tooyour on-premises data sources tooprocess and refresh data in hello model.</span></span>

> [!TIP]
> <span data-ttu-id="118b6-115">Przed wdrożeniem, upewnij się, że można przetwarzać hello dane w tabelach.</span><span class="sxs-lookup"><span data-stu-id="118b6-115">Before you deploy, make sure you can process hello data in your tables.</span></span> <span data-ttu-id="118b6-116">W programie SSDT kliknij opcje **Model** > **Przetwarzaj** > **Przetwarzaj wszystko**.</span><span class="sxs-lookup"><span data-stu-id="118b6-116">In SSDT, click **Model** > **Process** > **Process All**.</span></span> <span data-ttu-id="118b6-117">Jeśli przetwarzanie zakończy się niepowodzeniem, wdrożenie nie jest możliwe.</span><span class="sxs-lookup"><span data-stu-id="118b6-117">If processing fails, you cannot successfully deploy.</span></span>
> 
> 

## <a name="toodeploy-a-tabular-model-from-ssdt"></a><span data-ttu-id="118b6-118">toodeploy modelu tabelarycznego z narzędzi SSDT</span><span class="sxs-lookup"><span data-stu-id="118b6-118">toodeploy a tabular model from SSDT</span></span>

1. <span data-ttu-id="118b6-119">Przed wdrożeniem, potrzebna jest nazwa serwera hello tooget.</span><span class="sxs-lookup"><span data-stu-id="118b6-119">Before you deploy, you need tooget hello server name.</span></span> <span data-ttu-id="118b6-120">W **portalu Azure** > serwera > **omówienie** > **nazwy serwera**, nazwę serwera na powitania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="118b6-120">In **Azure portal** > server > **Overview** > **Server name**, copy hello server name.</span></span>
   
    ![Pobieranie nazwy serwera z systemu Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="118b6-122">Programu SSDT > **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello > **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="118b6-122">In SSDT > **Solution Explorer**, right-click hello project > **Properties**.</span></span> <span data-ttu-id="118b6-123">Następnie w **wdrożenia** > **serwera** Wklej hello nazwy serwera.</span><span class="sxs-lookup"><span data-stu-id="118b6-123">Then in **Deployment** > **Server** paste hello server name.</span></span>   
   
    ![Wklejanie nazwy serwera we właściwościach serwera wdrażania](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. <span data-ttu-id="118b6-125">W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy **Właściwości**, a następnie kliknij przycisk **Wdróż**.</span><span class="sxs-lookup"><span data-stu-id="118b6-125">In **Solution Explorer**, right-click **Properties**, then click **Deploy**.</span></span> <span data-ttu-id="118b6-126">Zostanie wyświetlony monit o toosign w tooAzure może być.</span><span class="sxs-lookup"><span data-stu-id="118b6-126">You may be prompted toosign in tooAzure.</span></span>
   
    ![Wdrażanie tooserver](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    <span data-ttu-id="118b6-128">Stan wdrożenia pojawia się w oknie danych wyjściowych zarówno hello i wdrażania.</span><span class="sxs-lookup"><span data-stu-id="118b6-128">Deployment status appears in both hello Output window and in Deploy.</span></span>
   
    ![Stan wdrożenia](./media/analysis-services-deploy/aas-deploy-status.png)

<span data-ttu-id="118b6-130">To wszystko jest tooit!</span><span class="sxs-lookup"><span data-stu-id="118b6-130">That's all there is tooit!</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="118b6-131">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="118b6-131">Troubleshooting</span></span>
<span data-ttu-id="118b6-132">Jeśli wdrożenie zakończy się niepowodzeniem, wdrażając metadanych, prawdopodobnie ponieważ SSDT nie może nawiązać połączenia tooyour serwera.</span><span class="sxs-lookup"><span data-stu-id="118b6-132">If deployment fails when deploying metadata, it's likely because SSDT couldn't connect tooyour server.</span></span> <span data-ttu-id="118b6-133">Upewnij się, że możesz połączyć tooyour serwera przy użyciu narzędzia SSMS.</span><span class="sxs-lookup"><span data-stu-id="118b6-133">Make sure you can connect tooyour server using SSMS.</span></span> <span data-ttu-id="118b6-134">Upewnij się, że hello właściwość serwera wdrażania projektu hello jest poprawna.</span><span class="sxs-lookup"><span data-stu-id="118b6-134">Then make sure hello Deployment Server property for hello project is correct.</span></span>

<span data-ttu-id="118b6-135">Jeśli wdrożenie zakończy się niepowodzeniem dla tabeli, prawdopodobnie ponieważ serwer nie może nawiązać połączenia tooa źródła danych.</span><span class="sxs-lookup"><span data-stu-id="118b6-135">If deployment fails on a table, it's likely because your server couldn't connect tooa data source.</span></span> <span data-ttu-id="118b6-136">Jeśli źródło danych jest lokalnie w sieci organizacji, należy się tooinstall [bramy danych lokalnych](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="118b6-136">If your data source is on-premises in your organization's network, be sure tooinstall an [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="118b6-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="118b6-137">Next steps</span></span>
<span data-ttu-id="118b6-138">Teraz, gdy masz serwer tooyour wdrożonym modelu tabelarycznego wszystko jest gotowe tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="118b6-138">Now that you have your tabular model deployed tooyour server, you're ready tooconnect tooit.</span></span> <span data-ttu-id="118b6-139">Możesz [tooit Uzyskuj dostęp do narzędzia SSMS](analysis-services-manage.md) toomanage go.</span><span class="sxs-lookup"><span data-stu-id="118b6-139">You can [connect tooit with SSMS](analysis-services-manage.md) toomanage it.</span></span> <span data-ttu-id="118b6-140">I będzie możliwe [połączyć za pomocą narzędzia klienta tooit](analysis-services-connect.md) , takie jak usługi Power BI, Power BI Desktop lub programu Excel i rozpoczęcia tworzenia raportów.</span><span class="sxs-lookup"><span data-stu-id="118b6-140">And, you can [connect tooit using a client tool](analysis-services-connect.md) like Power BI, Power BI Desktop, or Excel, and start creating reports.</span></span>

