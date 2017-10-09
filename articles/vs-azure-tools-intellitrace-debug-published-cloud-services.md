---
title: "aaaDebugging opublikowane usługi Azure usługę w chmurze z programu Visual Studio i IntelliTrace | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usługa toodebug chmurę z programu Visual Studio i IntelliTrace"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5e6662fc-b917-43ea-bf2b-4f2fc3d213dc
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 60734a71d5499de72e1ca81a3ab0ab9f34bc303a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a><span data-ttu-id="c49f9-103">Debugowanie usługi opublikowana chmura Azure za pomocą programu Visual Studio i IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="c49f9-103">Debugging a published Azure cloud service with Visual Studio and IntelliTrace</span></span>
<span data-ttu-id="c49f9-104">Przy użyciu funkcji IntelliTrace można rejestrować szeroką gamę informacji o debugowaniu dla wystąpienia roli, po uruchomieniu na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c49f9-104">With IntelliTrace, you can log extensive debugging information for a role instance when it runs in Azure.</span></span> <span data-ttu-id="c49f9-105">Toofind hello przyczynę problemu, należy tak, jakby były uruchomione w systemie Azure można użyć toostep dzienniki IntelliTrace hello za pomocą kodu w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c49f9-105">If you need toofind hello cause of a problem, you can use hello IntelliTrace logs toostep through your code from Visual Studio as if it were running in Azure.</span></span> <span data-ttu-id="c49f9-106">W rezultacie rekordy kod klucza wykonywania i środowiska danych IntelliTrace, gdy aplikacja Azure działa jako usługa w chmurze na platformie Azure i umożliwia powtarzania hello rejestrowane dane z programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c49f9-106">In effect, IntelliTrace records key code execution and environment data when your Azure application is running as a cloud service in Azure, and lets you replay hello recorded data from Visual Studio.</span></span> 

<span data-ttu-id="c49f9-107">Można użyć funkcji IntelliTrace, jeśli masz zainstalowany program Visual Studio Enterprise i celów aplikacji Azure .NET Framework 4 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="c49f9-107">You can use IntelliTrace if you have Visual Studio Enterprise installed and your Azure application targets .NET Framework 4 or a later version.</span></span> <span data-ttu-id="c49f9-108">IntelliTrace zbiera informacje dotyczące poszczególnych ról platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c49f9-108">IntelliTrace collects information for your Azure roles.</span></span> <span data-ttu-id="c49f9-109">Hello maszyny wirtualnej dla tych ról są zawsze uruchamiane w 64-bitowych systemach operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="c49f9-109">hello virtual machines for these roles always run 64-bit operating systems.</span></span>

<span data-ttu-id="c49f9-110">Alternatywnie, można użyć [zdalnego debugowania](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach bezpośrednio tooa usługi w chmurze jest uruchomiona na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c49f9-110">As an alternative, you can use [remote debugging](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach directly tooa cloud service that's running in Azure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c49f9-111">IntelliTrace jest przeznaczona tylko w scenariuszach debugowania i nie powinna być używana w przypadku wdrożenia produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c49f9-111">IntelliTrace is intended for debug scenarios only, and should not be used for a production deployment.</span></span>
> 

## <a name="configure-an-azure-application-for-intellitrace"></a><span data-ttu-id="c49f9-112">Skonfigurować aplikację Azure dla funkcji IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="c49f9-112">Configure an Azure application for IntelliTrace</span></span>
<span data-ttu-id="c49f9-113">tooenable IntelliTrace aplikacji platformy Azure, musisz utworzyć i opublikować aplikacji hello z projektu programu Visual Studio Azure.</span><span class="sxs-lookup"><span data-stu-id="c49f9-113">tooenable IntelliTrace for an Azure application, you must create and publish hello application from a Visual Studio Azure project.</span></span> <span data-ttu-id="c49f9-114">Przed opublikowaniem tooAzure, należy skonfigurować funkcji IntelliTrace dla aplikacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c49f9-114">You must configure IntelliTrace for your Azure application before you publish it tooAzure.</span></span> <span data-ttu-id="c49f9-115">W przypadku publikowania aplikacji bez konfigurowania funkcji IntelliTrace, należy toorepublish hello projektu.</span><span class="sxs-lookup"><span data-stu-id="c49f9-115">If you publish your application without configuring IntelliTrace, you need toorepublish hello project.</span></span> <span data-ttu-id="c49f9-116">Aby uzyskać więcej informacji, zobacz [publikowania Azure cloud services projektów przy użyciu programu Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span><span class="sxs-lookup"><span data-stu-id="c49f9-116">For more information, see [Publishing an Azure cloud services projects using Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span></span>

1. <span data-ttu-id="c49f9-117">Jeśli jesteś gotowe toodeploy aplikacji platformy Azure, sprawdź, czy elementy docelowe kompilacji projektu są zbyt**debugowania**.</span><span class="sxs-lookup"><span data-stu-id="c49f9-117">When you are ready toodeploy your Azure application, verify that your project build targets are set too**Debug**.</span></span>

1. <span data-ttu-id="c49f9-118">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt i wybierz z menu kontekstowego hello **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="c49f9-118">In **Solution Explorer**, right-click project, and, from hello context menu, select **Publish**.</span></span>
   
1. <span data-ttu-id="c49f9-119">W hello **publikowanie aplikacji platformy Azure** okno dialogowe, wybierz opcję hello subskrypcji platformy Azure i wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c49f9-119">In hello **Publish Azure Application** dialog, select hello Azure subscription, and select **Next**.</span></span>

1. <span data-ttu-id="c49f9-120">W hello **ustawienia** strona, wybierz hello **Zaawansowane ustawienia** kartę.</span><span class="sxs-lookup"><span data-stu-id="c49f9-120">In hello **Settings** page, select hello **Advanced Settings** tab.</span></span>

1. <span data-ttu-id="c49f9-121">Włącz hello **włączyć IntelliTrace** opcję toocollect dzienniki IntelliTrace dla aplikacji po opublikowaniu go w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="c49f9-121">Turn on hello **Enable IntelliTrace** option toocollect IntelliTrace logs for your application when it is published in hello cloud.</span></span>
   
1. <span data-ttu-id="c49f9-122">toocustomize hello IntelliTrace konfiguracji podstawowej, wybierz opcję **ustawienia** dalej zbyt**włączyć IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="c49f9-122">toocustomize hello basic IntelliTrace configuration, select **Settings** next too**Enable IntelliTrace**.</span></span>

    ![Łącze Ustawienia funkcji IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. <span data-ttu-id="c49f9-124">W hello **ustawienia IntelliTrace** okna dialogowego, można określić toolog zdarzenia, które, czy toocollect informacji o wywołaniach, które toocollect moduły i procesy w dziennikach i rejestrowania toohello tooallocate ilość miejsca.</span><span class="sxs-lookup"><span data-stu-id="c49f9-124">In hello **IntelliTrace Settings** dialog, you can specify which events toolog, whether toocollect call information, which modules and processes toocollect logs for, and how much space tooallocate toohello recording.</span></span> <span data-ttu-id="c49f9-125">Aby uzyskać więcej informacji o funkcji IntelliTrace, zobacz [debugowanie przy użyciu funkcji IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span><span class="sxs-lookup"><span data-stu-id="c49f9-125">For more information about IntelliTrace, see [Debugging with IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span></span>
   
    ![Ustawienia funkcji IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

<span data-ttu-id="c49f9-127">dziennika IntelliTrace Hello jest cyklicznego pliku dziennika hello maksymalny rozmiar określony w ustawieniach IntelliTrace hello (hello domyślny rozmiar to 250 MB).</span><span class="sxs-lookup"><span data-stu-id="c49f9-127">hello IntelliTrace log is a circular log file of hello maximum size specified in hello IntelliTrace settings (hello default size is 250 MB).</span></span> <span data-ttu-id="c49f9-128">Dzienniki IntelliTrace są zbierane tooa pliku w systemie plików hello hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c49f9-128">IntelliTrace logs are collected tooa file in hello file system of hello virtual machine.</span></span> <span data-ttu-id="c49f9-129">W przypadku żądania hello dzienniki, migawki są podejmowane w danym momencie i pobrać tooyour komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="c49f9-129">When you request hello logs, a snapshot is taken at that point in time and downloaded tooyour local computer.</span></span>

<span data-ttu-id="c49f9-130">Po hello usługi w chmurze Azure została opublikowana tooAzure, można określić, jeśli włączono IntelliTrace z hello Azure w węźle **Eksploratora serwera**, jak pokazano w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="c49f9-130">After hello Azure cloud service has been published tooAzure, you can determine if IntelliTrace has been enabled from hello Azure node in **Server Explorer**, as shown in hello following image:</span></span>

![Eksplorator serwera - IntelliTrace włączone](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a><span data-ttu-id="c49f9-132">Pobierz dzienniki IntelliTrace dla wystąpienia roli</span><span class="sxs-lookup"><span data-stu-id="c49f9-132">Download IntelliTrace logs for a role instance</span></span>
<span data-ttu-id="c49f9-133">Za pomocą programu Visual Studio, możesz pobrać dzienniki IntelliTrace dla wystąpienia roli wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c49f9-133">Using Visual Studio, you can download IntelliTrace logs for a role instance by following these steps:</span></span>

1. <span data-ttu-id="c49f9-134">W **Eksploratora serwera**, rozwiń węzeł hello **usługi w chmurze** węzeł i Znajdź wystąpienia roli dzienniki, których chcesz toodownload.</span><span class="sxs-lookup"><span data-stu-id="c49f9-134">In **Server Explorer**, expand hello **Cloud Services** node, and locate role instance whose logs you wish toodownload.</span></span> 

1. <span data-ttu-id="c49f9-135">Kliknij prawym przyciskiem myszy hello wystąpienia roli, a następnie wybierz z menu kontekstowego hello s, **Wyświetl dzienniki IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="c49f9-135">Right-click hello role instance, and from hello s context menu, select **View IntelliTrace Logs**.</span></span> 

    ![Wyświetlanie opcji menu Dzienniki IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. <span data-ttu-id="c49f9-137">Dzienniki IntelliTrace Hello są tooa pobranego pliku w katalogu na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="c49f9-137">hello IntelliTrace logs are downloaded tooa file in a directory on your local computer.</span></span> <span data-ttu-id="c49f9-138">Zawsze zażądania hello dzienników IntelliTrace, utworzyć nową migawkę.</span><span class="sxs-lookup"><span data-stu-id="c49f9-138">Each time that you request hello IntelliTrace logs, a new snapshot is created.</span></span> <span data-ttu-id="c49f9-139">Podczas pobierania dzienników hello Visual Studio Wyświetla hello postęp operacji hello hello **dziennika aktywności platformy Azure** okna.</span><span class="sxs-lookup"><span data-stu-id="c49f9-139">While hello logs are being downloaded, Visual Studio displays hello progress of hello operation in hello **Azure Activity Log** window.</span></span> <span data-ttu-id="c49f9-140">Jak pokazano na następującej ilustracji hello, możesz rozszerzyć hello pozycji dla toosee operacji hello więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="c49f9-140">As shown in hello following figure, you can expand hello line item for hello operation toosee more detail.</span></span>

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

<span data-ttu-id="c49f9-142">Podczas pobierania dzienników IntelliTrace hello, możesz kontynuować toowork w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c49f9-142">You can continue toowork in Visual Studio while hello IntelliTrace logs are downloading.</span></span> <span data-ttu-id="c49f9-143">Dziennik hello zakończył pobieranie, zostanie otwarty w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c49f9-143">When hello log has finished downloading, it opens in Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="c49f9-144">Witaj dzienniki IntelliTrace może zawierać wyjątki tego framework hello generuje i obsługuje później.</span><span class="sxs-lookup"><span data-stu-id="c49f9-144">hello IntelliTrace logs might contain exceptions that hello framework generates and handles afterwards.</span></span> <span data-ttu-id="c49f9-145">Kod wewnętrzny framework generuje tych wyjątków w ramach normalnego uruchamiania roli, więc można je bezpiecznie zignorować.</span><span class="sxs-lookup"><span data-stu-id="c49f9-145">Internal framework code generates these exceptions as a normal part of starting up a role, so you may safely ignore them.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c49f9-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c49f9-146">Next steps</span></span>
- [<span data-ttu-id="c49f9-147">Opcje debugowania usług w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="c49f9-147">Options for debugging Azure cloud services</span></span>](vs-azure-tools-debugging-cloud-services-overview.md)
- [<span data-ttu-id="c49f9-148">Publikowanie usługi w chmurze platformy Azure przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c49f9-148">Publishing an Azure cloud service using Visual Studio</span></span>](vs-azure-tools-publishing-a-cloud-service.md)