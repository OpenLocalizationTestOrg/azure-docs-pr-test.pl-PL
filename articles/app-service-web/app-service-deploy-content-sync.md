---
title: "Synchronizowanie zawartości z folderu chmury do usługi Azure App Service"
description: "Dowiedz się, jak wdrożyć aplikację w usłudze Azure App Service za pośrednictwem synchronizacji zawartości z folderu chmury."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 88d3a670-303a-4fa2-9de9-715cc904acec
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 010e7dc492abefaa3afe814c0322af9f6fe5acd2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="sync-content-from-a-cloud-folder-to-azure-app-service"></a><span data-ttu-id="4ea88-103">Synchronizowanie zawartości z folderu chmury do usługi Azure App Service</span><span class="sxs-lookup"><span data-stu-id="4ea88-103">Sync content from a cloud folder to Azure App Service</span></span>
<span data-ttu-id="4ea88-104">Ten samouczek pokazuje, jak wdrożyć na [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) przez synchronizację zawartość z usługi magazynu w chmurze popularnych jak Dropbox i OneDrive.</span><span class="sxs-lookup"><span data-stu-id="4ea88-104">This tutorial shows you how to deploy to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by syncing your content from popular cloud storage services like Dropbox and OneDrive.</span></span> 

## <span data-ttu-id="4ea88-105"><a name="overview"></a>Omówienie wdrażania zawartości synchronizacji</span><span class="sxs-lookup"><span data-stu-id="4ea88-105"><a name="overview"></a>Overview of content sync deployment</span></span>
<span data-ttu-id="4ea88-106">Wdrażanie synchronizacji zawartości na żądanie jest obsługiwany przez [aparat wdrażania Kudu](https://github.com/projectkudu/kudu/wiki) zintegrowany z usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4ea88-106">The on-demand content sync deployment is powered by the [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki) integrated with App Service.</span></span> <span data-ttu-id="4ea88-107">W [Azure Portal](https://portal.azure.com), można wyznaczyć folder w magazynie w chmurze, pracy z kodu aplikacji, a zawartość w tym folderze oraz synchronizacji w usłudze App Service z kliknięcie przycisku.</span><span class="sxs-lookup"><span data-stu-id="4ea88-107">In the [Azure Portal](https://portal.azure.com), you can designate a folder in your cloud storage, work with your app code and content in that folder, and sync to App Service with the click of a button.</span></span> <span data-ttu-id="4ea88-108">Zawartości synchronizacji wykorzystuje Kudu proces kompilacji i wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="4ea88-108">Content sync utilizes the Kudu process for build and deployment.</span></span> 

## <span data-ttu-id="4ea88-109"><a name="contentsync"></a>Jak włączyć wdrożenie zawartości synchronizacji</span><span class="sxs-lookup"><span data-stu-id="4ea88-109"><a name="contentsync"></a>How to enable content sync deployment</span></span>
<span data-ttu-id="4ea88-110">Aby włączyć zawartości synchronizacji [Azure Portal](https://portal.azure.com), wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4ea88-110">To enable content sync from the [Azure Portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="4ea88-111">W bloku aplikacji w portalu Azure, kliknij **ustawienia** > **źródło wdrożenia**.</span><span class="sxs-lookup"><span data-stu-id="4ea88-111">In your app's blade in the Azure Portal, click **Settings** > **Deployment Source**.</span></span> <span data-ttu-id="4ea88-112">Kliknij przycisk **wybierz źródło**, a następnie wybierz pozycję **OneDrive** lub **Dropbox** jako źródło dla wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="4ea88-112">Click **Choose Source**, then select **OneDrive** or **Dropbox** as the source for deployment.</span></span> 
   
    ![Synchronizacja zawartości](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > <span data-ttu-id="4ea88-114">Z powodu podstawowych różnic w interfejsach API **OneDrive dla firm** nie jest obsługiwana w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="4ea88-114">Because of underlying differences in the APIs, **OneDrive for Business** is not supported at this time.</span></span> 
   > 
   > 
2. <span data-ttu-id="4ea88-115">Ukończenia przepływu pracy autoryzacji, aby włączyć usługę aplikacji, aby uzyskiwać dostęp do określonej ścieżki wyznaczonych wstępnie zdefiniowane dla usługi OneDrive lub Dropbox całej zawartości z usługi aplikacji — zostanie przechowywania.</span><span class="sxs-lookup"><span data-stu-id="4ea88-115">Complete the authorization workflow to enable App Service to access a specific pre-defined designated path for OneDrive or Dropbox where all of your App Service content will be stored.</span></span>  
    <span data-ttu-id="4ea88-116">Po autoryzacji usługi App Service platforma zapewni opcję Utwórz folder zawartości w określonej ścieżce zawartości lub wybierz istniejący folder zawartości w obszarze tej określonej ścieżce zawartości.</span><span class="sxs-lookup"><span data-stu-id="4ea88-116">After authorization the App Service platform will give you the option to create a content folder under the designated content path, or to choose an existing content folder under this designated content path.</span></span> <span data-ttu-id="4ea88-117">Wyznaczone ścieżek zawartości w ramach kont magazynu chmurze używane do synchronizacji usługi App Service są następujące:</span><span class="sxs-lookup"><span data-stu-id="4ea88-117">The designated content paths under your cloud storage accounts used for App Service sync are the following:</span></span>  
   
   * <span data-ttu-id="4ea88-118">**OneDrive**:`Apps\Azure Web Apps`</span><span class="sxs-lookup"><span data-stu-id="4ea88-118">**OneDrive**: `Apps\Azure Web Apps`</span></span> 
   * <span data-ttu-id="4ea88-119">**Dropbox**:`Dropbox\Apps\Azure`</span><span class="sxs-lookup"><span data-stu-id="4ea88-119">**Dropbox**: `Dropbox\Apps\Azure`</span></span>
3. <span data-ttu-id="4ea88-120">Po początkowej synchronizacji zawartości można zainicjować synchronizacji zawartości na żądanie z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4ea88-120">After the initial content sync the content sync can be initiated on demand from the Azure portal.</span></span> <span data-ttu-id="4ea88-121">Historia wdrożenia jest dostępna z **wdrożeń** bloku.</span><span class="sxs-lookup"><span data-stu-id="4ea88-121">Deployment history is available with the **Deployments** blade.</span></span>
   
    ![Historia wdrażania](./media/app-service-deploy-content-sync/onedrive_sync.png)

<span data-ttu-id="4ea88-123">Więcej informacji do wdrożenia usługi Dropbox znajduje się w obszarze [Wdróż z Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ea88-123">More information for Dropbox deployment is available under [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span></span> 

