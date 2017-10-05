---
title: "Wdrażanie usług Azure Analysis Services przy użyciu programu SSDT | Microsoft Docs"
description: "Dowiedz się, jak wdrożyć model tabelaryczny na serwerze usług Azure Analysis Services przy użyciu programu SSDT."
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
ms.openlocfilehash: e9a3aedfb6e55696e1525e226fada1062fd5eda8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-model-from-ssdt"></a><span data-ttu-id="3d923-103">Wdrażanie modelu w programie SSDT</span><span class="sxs-lookup"><span data-stu-id="3d923-103">Deploy a model from SSDT</span></span>
<span data-ttu-id="3d923-104">Po utworzeniu serwera w ramach subskrypcji platformy Azure wszystko jest gotowe do wdrożenia bazy danych modelu tabelarycznego.</span><span class="sxs-lookup"><span data-stu-id="3d923-104">Once you've created a server in your Azure subscription, you're ready to deploy a tabular model database to it.</span></span> <span data-ttu-id="3d923-105">Program SSDT (SQL Server Data Tools) służy do tworzenia i wdrażania projektu modelu tabelarycznego, nad którymi pracujesz.</span><span class="sxs-lookup"><span data-stu-id="3d923-105">You can use SQL Server Data Tools (SSDT) to build and deploy a tabular model project you're working on.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3d923-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3d923-106">Prerequisites</span></span>
<span data-ttu-id="3d923-107">Aby rozpocząć pracę, potrzebne będą następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="3d923-107">To get started, you need:</span></span>

* <span data-ttu-id="3d923-108">**Serwer usług Analysis Services** na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3d923-108">**Analysis Services server** in Azure.</span></span> <span data-ttu-id="3d923-109">Aby dowiedzieć się więcej, zobacz artykuł [Create an Azure Analysis Services server](analysis-services-create-server.md) (Tworzenie serwera usług Azure Analysis Services).</span><span class="sxs-lookup"><span data-stu-id="3d923-109">To learn more, see [Create an Azure Analysis Services server](analysis-services-create-server.md).</span></span>
* <span data-ttu-id="3d923-110">**Projekt modelu tabelarycznego** w programie SSDT lub istniejący model tabelaryczny na poziomie zgodności 1200 lub wyższym.</span><span class="sxs-lookup"><span data-stu-id="3d923-110">**Tabular model project** in SSDT or an existing tabular model at the 1200 or higher compatibility level.</span></span> <span data-ttu-id="3d923-111">Nie wiesz, jak go utworzyć?</span><span class="sxs-lookup"><span data-stu-id="3d923-111">Never created one?</span></span> <span data-ttu-id="3d923-112">Spróbuj skorzystać z [samouczka sprzedaży modelowania tabelarycznego projektu Adventure Works Internet Sales](https://msdn.microsoft.com/library/hh231691.aspx).</span><span class="sxs-lookup"><span data-stu-id="3d923-112">Try the [Adventure Works Internet sales tabular modeling tutorial](https://msdn.microsoft.com/library/hh231691.aspx).</span></span>
* <span data-ttu-id="3d923-113">**Brama lokalna** — jeśli co najmniej jedno źródło danych znajduje się w sieci organizacji, należy zainstalować [bramę danych lokalnych](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="3d923-113">**On-premises gateway** - If one or more data sources are on-premises in your organization's network, you need to install an [On-premises data gateway](analysis-services-gateway.md).</span></span> <span data-ttu-id="3d923-114">Brama jest niezbędna, aby umożliwić serwerowi w chmurze łączenie się z lokalnymi źródłami danych w celu przetwarzania i odświeżania danych w modelu.</span><span class="sxs-lookup"><span data-stu-id="3d923-114">The gateway is necessary for your server in the cloud connect to your on-premises data sources to process and refresh data in the model.</span></span>

> [!TIP]
> <span data-ttu-id="3d923-115">Przed jej wdrożeniem upewnij się, że można przetwarzać dane w tabelach.</span><span class="sxs-lookup"><span data-stu-id="3d923-115">Before you deploy, make sure you can process the data in your tables.</span></span> <span data-ttu-id="3d923-116">W programie SSDT kliknij opcje **Model** > **Przetwarzaj** > **Przetwarzaj wszystko**.</span><span class="sxs-lookup"><span data-stu-id="3d923-116">In SSDT, click **Model** > **Process** > **Process All**.</span></span> <span data-ttu-id="3d923-117">Jeśli przetwarzanie zakończy się niepowodzeniem, wdrożenie nie jest możliwe.</span><span class="sxs-lookup"><span data-stu-id="3d923-117">If processing fails, you cannot successfully deploy.</span></span>
> 
> 

## <a name="to-deploy-a-tabular-model-from-ssdt"></a><span data-ttu-id="3d923-118">Aby wdrożyć model tabelaryczny w programie SSDT</span><span class="sxs-lookup"><span data-stu-id="3d923-118">To deploy a tabular model from SSDT</span></span>

1. <span data-ttu-id="3d923-119">Przed wdrożeniem należy uzyskać nazwę serwera.</span><span class="sxs-lookup"><span data-stu-id="3d923-119">Before you deploy, you need to get the server name.</span></span> <span data-ttu-id="3d923-120">Skopiuj nazwę serwera z **portalu Azure** > serwer > **Omówienie** > **Nazwa serwera**.</span><span class="sxs-lookup"><span data-stu-id="3d923-120">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span></span>
   
    ![Pobieranie nazwy serwera z systemu Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="3d923-122">W programie SSDT > **Eksplorator rozwiązań** kliknij prawym przyciskiem myszy projekt > **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="3d923-122">In SSDT > **Solution Explorer**, right-click the project > **Properties**.</span></span> <span data-ttu-id="3d923-123">Następnie w obszarze **Wdrożenie** > **Serwer** wklej nazwę serwera.</span><span class="sxs-lookup"><span data-stu-id="3d923-123">Then in **Deployment** > **Server** paste the server name.</span></span>   
   
    ![Wklejanie nazwy serwera we właściwościach serwera wdrażania](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. <span data-ttu-id="3d923-125">W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy **Właściwości**, a następnie kliknij przycisk **Wdróż**.</span><span class="sxs-lookup"><span data-stu-id="3d923-125">In **Solution Explorer**, right-click **Properties**, then click **Deploy**.</span></span> <span data-ttu-id="3d923-126">Może zostać wyświetlony monit o zalogowanie się do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3d923-126">You may be prompted to sign in to Azure.</span></span>
   
    ![Wdrażanie na serwerze](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    <span data-ttu-id="3d923-128">Stan wdrożenia pojawia się w oknie danych wyjściowych i oknie wdrażania.</span><span class="sxs-lookup"><span data-stu-id="3d923-128">Deployment status appears in both the Output window and in Deploy.</span></span>
   
    ![Stan wdrożenia](./media/analysis-services-deploy/aas-deploy-status.png)

<span data-ttu-id="3d923-130">To wszystko!</span><span class="sxs-lookup"><span data-stu-id="3d923-130">That's all there is to it!</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="3d923-131">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="3d923-131">Troubleshooting</span></span>
<span data-ttu-id="3d923-132">Jeśli wdrożenie zakończy się niepowodzeniem podczas wdrażania metadanych, prawdopodobną przyczyną jest brak połączenia programu SSDT z serwerem.</span><span class="sxs-lookup"><span data-stu-id="3d923-132">If deployment fails when deploying metadata, it's likely because SSDT couldn't connect to your server.</span></span> <span data-ttu-id="3d923-133">Upewnij się, że możesz połączyć się z serwerem przy użyciu programu SSMS.</span><span class="sxs-lookup"><span data-stu-id="3d923-133">Make sure you can connect to your server using SSMS.</span></span> <span data-ttu-id="3d923-134">Upewnij się, że właściwość serwera wdrażania dla projektu jest poprawna.</span><span class="sxs-lookup"><span data-stu-id="3d923-134">Then make sure the Deployment Server property for the project is correct.</span></span>

<span data-ttu-id="3d923-135">Jeśli wdrożenie zakończy się niepowodzeniem dla tabeli, prawdopodobnie serwer nie mógł nawiązać połączenia ze źródłem danych.</span><span class="sxs-lookup"><span data-stu-id="3d923-135">If deployment fails on a table, it's likely because your server couldn't connect to a data source.</span></span> <span data-ttu-id="3d923-136">Jeśli źródło danych znajduje się w lokalnej sieci organizacji, należy zainstalować [bramę danych lokalnych](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="3d923-136">If your data source is on-premises in your organization's network, be sure to install an [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d923-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3d923-137">Next steps</span></span>
<span data-ttu-id="3d923-138">Po wdrożeniu modelu tabelarycznego na serwerze możesz się z nim połączyć.</span><span class="sxs-lookup"><span data-stu-id="3d923-138">Now that you have your tabular model deployed to your server, you're ready to connect to it.</span></span> <span data-ttu-id="3d923-139">W celu zarządzania modelem możesz [połączyć się przy użyciu programu SSMS](analysis-services-manage.md).</span><span class="sxs-lookup"><span data-stu-id="3d923-139">You can [connect to it with SSMS](analysis-services-manage.md) to manage it.</span></span> <span data-ttu-id="3d923-140">Możesz również [nawiązać połączenie za pomocą narzędzia klienta](analysis-services-connect.md), takiego jak usługi Power BI, Power BI Desktop lub program Excel, i rozpocząć tworzenie raportów.</span><span class="sxs-lookup"><span data-stu-id="3d923-140">And, you can [connect to it using a client tool](analysis-services-connect.md) like Power BI, Power BI Desktop, or Excel, and start creating reports.</span></span>

