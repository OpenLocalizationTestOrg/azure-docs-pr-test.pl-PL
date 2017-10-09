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
# <a name="sync-content-from-a-cloud-folder-tooazure-app-service"></a>Synchronizowanie zawartości z chmury tooAzure folderu usługi aplikacji
W tym samouczku przedstawiono sposób toodeploy za[usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) przez synchronizację zawartość z usługi magazynu w chmurze popularnych jak Dropbox i OneDrive. 

## <a name="overview"></a>Omówienie wdrażania zawartości synchronizacji
Witaj synchronizacji zawartości na żądanie wdrożenia jest obsługiwany przez hello [aparat wdrażania Kudu](https://github.com/projectkudu/kudu/wiki) zintegrowany z usługi aplikacji. W hello [Azure Portal](https://portal.azure.com), możesz wyznaczyć folder w magazynie w chmurze, Praca z kodu aplikacji i zawartości w tym folderze, a tooApp synchronizacji usługi z powitania kliknij przycisku. Zawartości synchronizacji wykorzystuje hello Kudu procesu kompilacji i wdrażania. 

## <a name="contentsync"></a>Jak zawartość tooenable synchronizacji wdrożenia
tooenable zawartości synchronizacji hello [Azure Portal](https://portal.azure.com), wykonaj następujące kroki:

1. W bloku aplikacji w portalu Azure hello, kliknij przycisk **ustawienia** > **źródło wdrożenia**. Kliknij przycisk **wybierz źródło**, a następnie wybierz pozycję **OneDrive** lub **Dropbox** jako źródło hello na potrzeby wdrożenia. 
   
    ![Synchronizacja zawartości](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > Z powodu podstawowych różnic w hello interfejsów API **OneDrive dla firm** nie jest obsługiwana w tej chwili. 
   > 
   > 
2. Tooenable przepływu pracy autoryzacji pełną hello tooaccess usługi aplikacji określonego wstępnie zdefiniowane określonej ścieżce dla usługi OneDrive lub Dropbox całej zawartości z usługi aplikacji — zostanie przechowywania.  
    Po hello autoryzacji, które pozwolą zdobyć usługi aplikacji platformy hello opcja toocreate zawartości folderu hello wyznaczone ścieżki zawartości lub toochoose istniejący folder zawartości w obszarze tej określonej ścieżce zawartości. Witaj wyznaczone ścieżek zawartości w ramach kont magazynu chmurze używane do synchronizacji usługi aplikacji są następujące hello:  
   
   * **OneDrive**:`Apps\Azure Web Apps` 
   * **Dropbox**:`Dropbox\Apps\Azure`
3. Po hello można zainicjować synchronizacji zawartości hello synchronizacji początkowej zawartości na żądanie z hello portalu Azure. Historia wdrożenia jest dostępna z hello **wdrożeń** bloku.
   
    ![Historia wdrażania](./media/app-service-deploy-content-sync/onedrive_sync.png)

Więcej informacji do wdrożenia usługi Dropbox znajduje się w obszarze [Wdróż z Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx). 

