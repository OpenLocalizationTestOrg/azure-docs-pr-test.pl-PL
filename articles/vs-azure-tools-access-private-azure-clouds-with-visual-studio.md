---
title: aaaAccessing prywatnej chmury Azure z programem Visual Studio | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak Chmura prywatna tooaccess zasobów za pomocą programu Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9d733c8d-703b-44e7-a210-bb75874c45c8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/19/2017
ms.author: kraigb
ms.openlocfilehash: 5cfd6439afdcf98c6f7d7f29ab6c4256ed02533a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a><span data-ttu-id="cb3db-103">Uzyskiwanie dostępu do chmur prywatnych Azure z programem Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cb3db-103">Accessing private Azure clouds with Visual Studio</span></span>
<span data-ttu-id="cb3db-104">Domyślnie program Visual Studio obsługuje punkty końcowe REST chmury publicznej Azure.</span><span class="sxs-lookup"><span data-stu-id="cb3db-104">By default, Visual Studio supports public Azure cloud REST endpoints.</span></span> <span data-ttu-id="cb3db-105">W tym temacie dowiesz się, jak toouse Twojego Chmura prywatna firmy tooaccess certyfikatu — i interakcję z — Witaj chmury prywatnej w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cb3db-105">In this topic, you learn how toouse your private cloud's certificate tooaccess - and interact with - hello private cloud from Visual Studio.</span></span>

## <a name="tooaccess-a-private-azure-cloud-in-visual-studio"></a><span data-ttu-id="cb3db-106">tooaccess prywatnej Azure w chmurze w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cb3db-106">tooaccess a private Azure cloud in Visual Studio</span></span>
1. <span data-ttu-id="cb3db-107">W hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885) hello chmury prywatnej, Pobierz swój plik ustawień publikowania, lub skontaktuj się z administratorem dla pliku ustawień publikowania.</span><span class="sxs-lookup"><span data-stu-id="cb3db-107">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) for hello private cloud, download your publish-settings file, or contact your administrator for a publish-settings file.</span></span> <span data-ttu-id="cb3db-108">W publicznej wersji hello Azure, hello toodownload łącze jest [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span><span class="sxs-lookup"><span data-stu-id="cb3db-108">On hello public version of Azure, hello link toodownload this is [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span></span> <span data-ttu-id="cb3db-109">(hello pobrany plik ma rozszerzenie `.publishsettings`)</span><span class="sxs-lookup"><span data-stu-id="cb3db-109">(hello downloaded file should have an extension of `.publishsettings`)</span></span>

1. <span data-ttu-id="cb3db-110">Otwórz program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cb3db-110">Open Visual Studio</span></span>

1. <span data-ttu-id="cb3db-111">W **Eksploratora serwera**, kliknij prawym przyciskiem myszy hello **Azure** węzła i wybierz z menu kontekstowego hello, **zarządzanie i subskrypcje filtru**.</span><span class="sxs-lookup"><span data-stu-id="cb3db-111">In **Server Explorer**, right-click hello **Azure** node and, from hello context menu, select **Manage and Filter Subscriptions**.</span></span>
   
    ![Zarządzanie subskrypcjami polecenia](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. <span data-ttu-id="cb3db-113">W hello **Zarządzanie subskrypcji platformy Microsoft Azure** okno dialogowe, wybierz opcję hello **certyfikaty** , a następnie wybierz **importu**.</span><span class="sxs-lookup"><span data-stu-id="cb3db-113">In hello **Manage Microsoft Azure Subscriptions** dialog, select hello **Certificates** tab, and then select **Import**.</span></span>
   
    ![Importowanie certyfikatów Azure](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. <span data-ttu-id="cb3db-115">W hello **importu subskrypcji platformy Microsoft Azure** okno dialogowe, wybierz opcję **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="cb3db-115">In hello **Import Microsoft Azure Subscriptions** dialog, select **Browse**.</span></span>

    ![Przeglądaj przycisk w oknie dialogowym Import subskrypcji platformy Microsoft Azure hello](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. <span data-ttu-id="cb3db-117">W hello **Otwórz** okna dialogowego, toohello przeglądania katalogów, w przypadku, gdy zostanie zapisany hello ustawień publikowania pliku, wybierz opcję hello pliku, a następnie wybierz **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="cb3db-117">In hello **Open** dialog, browse toohello directory where you saved hello publish-settings file, select hello file, and then select **Open**.</span></span>

    ![Wybierz plik ustawień publikowania hello](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. <span data-ttu-id="cb3db-119">Gdy zwrócony toohello **importu subskrypcji platformy Microsoft Azure** okno dialogowe, wybierz **importu**.</span><span class="sxs-lookup"><span data-stu-id="cb3db-119">When returned toohello **Import Microsoft Azure Subscriptions** dialog, select **Import**.</span></span>

    ![Plik ustawień publikowania hello importu](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    <span data-ttu-id="cb3db-121">Witaj certyfikaty są zaimportowane z pliku ustawień publikowania hello do programu Visual Studio, a teraz pozwala na interakcję z zasobami w chmurze prywatnej.</span><span class="sxs-lookup"><span data-stu-id="cb3db-121">hello certificates are imported from hello publish-settings file into Visual Studio, and you can now interact with your private cloud resources.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="cb3db-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cb3db-122">Next steps</span></span>
- [<span data-ttu-id="cb3db-123">Tooan publikowania usługi w chmurze Azure w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cb3db-123">Publishing tooan Azure Cloud Service from Visual Studio</span></span>](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- <span data-ttu-id="cb3db-124">[Porady: pobieranie i importowanie publikowania ustawienia i informacje o subskrypcji](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span><span class="sxs-lookup"><span data-stu-id="cb3db-124">[How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span></span>
