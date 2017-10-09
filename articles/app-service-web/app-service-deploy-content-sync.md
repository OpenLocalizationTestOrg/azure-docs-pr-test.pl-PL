---
title: "aaaSync zawartość chmury tooAzure folderu usługi aplikacji"
description: "Dowiedz się, jak toodeploy Twojego tooAzure aplikacji usługi App Service za pośrednictwem zawartości synchronizacji z folderu chmury."
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
ms.openlocfilehash: e1c6d53a427c36126d9cdb33cc21b4126b9d9c2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sync-content-from-a-cloud-folder-tooazure-app-service"></a><span data-ttu-id="2604a-103">Synchronizowanie zawartości z chmury tooAzure folderu usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="2604a-103">Sync content from a cloud folder tooAzure App Service</span></span>
<span data-ttu-id="2604a-104">W tym samouczku przedstawiono sposób toodeploy za[usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) przez synchronizację zawartość z usługi magazynu w chmurze popularnych jak Dropbox i OneDrive.</span><span class="sxs-lookup"><span data-stu-id="2604a-104">This tutorial shows you how toodeploy too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by syncing your content from popular cloud storage services like Dropbox and OneDrive.</span></span> 

## <span data-ttu-id="2604a-105"><a name="overview"></a>Omówienie wdrażania zawartości synchronizacji</span><span class="sxs-lookup"><span data-stu-id="2604a-105"><a name="overview"></a>Overview of content sync deployment</span></span>
<span data-ttu-id="2604a-106">Witaj synchronizacji zawartości na żądanie wdrożenia jest obsługiwany przez hello [aparat wdrażania Kudu](https://github.com/projectkudu/kudu/wiki) zintegrowany z usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2604a-106">hello on-demand content sync deployment is powered by hello [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki) integrated with App Service.</span></span> <span data-ttu-id="2604a-107">W hello [Azure Portal](https://portal.azure.com), możesz wyznaczyć folder w magazynie w chmurze, Praca z kodu aplikacji i zawartości w tym folderze, a tooApp synchronizacji usługi z powitania kliknij przycisku.</span><span class="sxs-lookup"><span data-stu-id="2604a-107">In hello [Azure Portal](https://portal.azure.com), you can designate a folder in your cloud storage, work with your app code and content in that folder, and sync tooApp Service with hello click of a button.</span></span> <span data-ttu-id="2604a-108">Zawartości synchronizacji wykorzystuje hello Kudu procesu kompilacji i wdrażania.</span><span class="sxs-lookup"><span data-stu-id="2604a-108">Content sync utilizes hello Kudu process for build and deployment.</span></span> 

## <span data-ttu-id="2604a-109"><a name="contentsync"></a>Jak zawartość tooenable synchronizacji wdrożenia</span><span class="sxs-lookup"><span data-stu-id="2604a-109"><a name="contentsync"></a>How tooenable content sync deployment</span></span>
<span data-ttu-id="2604a-110">tooenable zawartości synchronizacji hello [Azure Portal](https://portal.azure.com), wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="2604a-110">tooenable content sync from hello [Azure Portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="2604a-111">W bloku aplikacji w portalu Azure hello, kliknij przycisk **ustawienia** > **źródło wdrożenia**.</span><span class="sxs-lookup"><span data-stu-id="2604a-111">In your app's blade in hello Azure Portal, click **Settings** > **Deployment Source**.</span></span> <span data-ttu-id="2604a-112">Kliknij przycisk **wybierz źródło**, a następnie wybierz pozycję **OneDrive** lub **Dropbox** jako źródło hello na potrzeby wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="2604a-112">Click **Choose Source**, then select **OneDrive** or **Dropbox** as hello source for deployment.</span></span> 
   
    ![Synchronizacja zawartości](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > <span data-ttu-id="2604a-114">Z powodu podstawowych różnic w hello interfejsów API **OneDrive dla firm** nie jest obsługiwana w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="2604a-114">Because of underlying differences in hello APIs, **OneDrive for Business** is not supported at this time.</span></span> 
   > 
   > 
2. <span data-ttu-id="2604a-115">Tooenable przepływu pracy autoryzacji pełną hello tooaccess usługi aplikacji określonego wstępnie zdefiniowane określonej ścieżce dla usługi OneDrive lub Dropbox całej zawartości z usługi aplikacji — zostanie przechowywania.</span><span class="sxs-lookup"><span data-stu-id="2604a-115">Complete hello authorization workflow tooenable App Service tooaccess a specific pre-defined designated path for OneDrive or Dropbox where all of your App Service content will be stored.</span></span>  
    <span data-ttu-id="2604a-116">Po hello autoryzacji, które pozwolą zdobyć usługi aplikacji platformy hello opcja toocreate zawartości folderu hello wyznaczone ścieżki zawartości lub toochoose istniejący folder zawartości w obszarze tej określonej ścieżce zawartości.</span><span class="sxs-lookup"><span data-stu-id="2604a-116">After authorization hello App Service platform will give you hello option toocreate a content folder under hello designated content path, or toochoose an existing content folder under this designated content path.</span></span> <span data-ttu-id="2604a-117">Witaj wyznaczone ścieżek zawartości w ramach kont magazynu chmurze używane do synchronizacji usługi aplikacji są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="2604a-117">hello designated content paths under your cloud storage accounts used for App Service sync are hello following:</span></span>  
   
   * <span data-ttu-id="2604a-118">**OneDrive**:`Apps\Azure Web Apps`</span><span class="sxs-lookup"><span data-stu-id="2604a-118">**OneDrive**: `Apps\Azure Web Apps`</span></span> 
   * <span data-ttu-id="2604a-119">**Dropbox**:`Dropbox\Apps\Azure`</span><span class="sxs-lookup"><span data-stu-id="2604a-119">**Dropbox**: `Dropbox\Apps\Azure`</span></span>
3. <span data-ttu-id="2604a-120">Po hello można zainicjować synchronizacji zawartości hello synchronizacji początkowej zawartości na żądanie z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2604a-120">After hello initial content sync hello content sync can be initiated on demand from hello Azure portal.</span></span> <span data-ttu-id="2604a-121">Historia wdrożenia jest dostępna z hello **wdrożeń** bloku.</span><span class="sxs-lookup"><span data-stu-id="2604a-121">Deployment history is available with hello **Deployments** blade.</span></span>
   
    ![Historia wdrażania](./media/app-service-deploy-content-sync/onedrive_sync.png)

<span data-ttu-id="2604a-123">Więcej informacji do wdrożenia usługi Dropbox znajduje się w obszarze [Wdróż z Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span><span class="sxs-lookup"><span data-stu-id="2604a-123">More information for Dropbox deployment is available under [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span></span> 

