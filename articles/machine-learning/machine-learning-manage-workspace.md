---
title: "aaaManage obszaru roboczego usługi Machine Learning | Dokumentacja firmy Microsoft"
description: "Obszary robocze uczenia maszynowego tooAzure dostępu, zarządzania i wdrażania i zarządzania nimi usług sieci web interfejsu API uczenia Maszynowego"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: daf3d413-7a77-4beb-9a7a-6b4bdf717719
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye
ms.openlocfilehash: 7bd378d82aa46f4340ca974c7dc5a612c089cdca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-machine-learning-workspace"></a><span data-ttu-id="47a42-103">Zarządzanie obszarem roboczym usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="47a42-103">Manage an Azure Machine Learning workspace</span></span>

> [!NOTE]
> <span data-ttu-id="47a42-104">Dla informacji o zarządzaniu usług sieci Web w portalu usługi sieci Web usługi Machine Learning hello, zobacz [zarządzania usługi sieci Web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="47a42-104">For information on managing Web services in hello Machine Learning Web Services portal, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span>
> 
> 

<span data-ttu-id="47a42-105">Możesz zarządzać obszary robocze uczenia maszynowego, albo hello portalu Azure lub hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="47a42-105">You can manage Machine Learning workspaces in either hello Azure portal or hello Azure classic portal.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-hello-azure-portal"></a><span data-ttu-id="47a42-106">Użyj hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="47a42-106">Use hello Azure portal</span></span>

<span data-ttu-id="47a42-107">toomanage obszaru roboczego w hello portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="47a42-107">toomanage a workspace in hello Azure portal:</span></span>

1. <span data-ttu-id="47a42-108">Zaloguj się toohello [portalu Azure](https://portal.azure.com/) przy użyciu konta administratora subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="47a42-108">Sign in toohello [Azure portal](https://portal.azure.com/) using an Azure subscription administrator account.</span></span>
2. <span data-ttu-id="47a42-109">W polu wyszukiwania hello u góry strony hello hello, wprowadź "komputera learning obszary robocze", a następnie wybierz **obszarów roboczych Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="47a42-109">In hello search box at hello top of hello page, enter "machine learning workspaces" and then select **Machine Learning Workspaces**.</span></span>
3. <span data-ttu-id="47a42-110">Kliknij obszar roboczy hello ma toomanage.</span><span class="sxs-lookup"><span data-stu-id="47a42-110">Click hello workspace you want toomanage.</span></span>

<span data-ttu-id="47a42-111">Oprócz informacji zarządzania standardowych zasobów toohello i dostępne opcje, można:</span><span class="sxs-lookup"><span data-stu-id="47a42-111">In addition toohello standard resource management information and options available, you can:</span></span>

- <span data-ttu-id="47a42-112">Widok **właściwości** — ta strona zawiera informacje dotyczące hello obszaru roboczego i zasobów, a można zmienić hello subskrypcji i grupy zasobów, połączony z tym obszarem roboczym.</span><span class="sxs-lookup"><span data-stu-id="47a42-112">View **Properties** - This page displays hello workspace and resource information, and you can change hello subscription and resource group that this workspace is connected with.</span></span>
- <span data-ttu-id="47a42-113">**Ponownej synchronizacji magazynu kluczy** -hello obszar roboczy obsługuje konto magazynu toohello kluczy.</span><span class="sxs-lookup"><span data-stu-id="47a42-113">**Resync Storage Keys** - hello workspace maintains keys toohello storage account.</span></span> <span data-ttu-id="47a42-114">Jeśli konto magazynu hello zmiany kluczy, a następnie kliknięcie **ponownej synchronizacji kluczy** toosynchronize hello kluczy do obszaru roboczego hello.</span><span class="sxs-lookup"><span data-stu-id="47a42-114">If hello storage account changes keys, then you can click **Resync keys** toosynchronize hello keys with hello workspace.</span></span>

<span data-ttu-id="47a42-115">portal usługi sieci Web usługi Machine Learning hello jest używany przez usługi sieci web hello toomanage skojarzony z tym obszarem roboczym.</span><span class="sxs-lookup"><span data-stu-id="47a42-115">toomanage hello web services associated with this workspace, use hello Machine Learning Web Services portal.</span></span> <span data-ttu-id="47a42-116">Zobacz [zarządzania usługi sieci Web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning hello](machine-learning-manage-new-webservice.md) pełne informacje.</span><span class="sxs-lookup"><span data-stu-id="47a42-116">See [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md) for complete information.</span></span>

> [!NOTE]
> <span data-ttu-id="47a42-117">toodeploy lub zarządzać nowych usług sieci web musi być przypisany współautora lub roli administratora usługi sieci web hello toowhich subskrypcji hello jest wdrażana.</span><span class="sxs-lookup"><span data-stu-id="47a42-117">toodeploy or manage New web services you must be assigned a contributor or administrator role on hello subscription toowhich hello web service is deployed.</span></span> <span data-ttu-id="47a42-118">Jeśli zaprosić inną maszynę tooa użytkownika obszaru roboczego uczenia, należy je przypisać rolę współautora lub administrator tooa na powitania subskrypcji przed wdrożeniem lub zarządzania usługami sieci web.</span><span class="sxs-lookup"><span data-stu-id="47a42-118">If you invite another user tooa machine learning workspace, you must assign them tooa contributor or administrator role on hello subscription before they can deploy or manage web services.</span></span> 
> 
><span data-ttu-id="47a42-119">Aby uzyskać więcej informacji o ustawianiu uprawnień dostępu, zobacz [Wyświetl przypisania dostępu dla użytkowników i grup w portalu Azure - publicznej wersji zapoznawczej hello](../active-directory/role-based-access-control-manage-assignments.md).</span><span class="sxs-lookup"><span data-stu-id="47a42-119">For more information on setting access permissions, see [View access assignments for users and groups in hello Azure portal - Public preview](../active-directory/role-based-access-control-manage-assignments.md).</span></span>

## <a name="use-hello-azure-classic-portal"></a><span data-ttu-id="47a42-120">Witaj Użyj klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="47a42-120">Use hello Azure classic portal</span></span>

<span data-ttu-id="47a42-121">Hello klasycznego portalu Azure można zarządzać do uczenia maszynowego obszarów roboczych:</span><span class="sxs-lookup"><span data-stu-id="47a42-121">Using hello Azure classic portal, you can manage your Machine Learning workspaces to:</span></span>

* <span data-ttu-id="47a42-122">Monitorowanie, sposobu używania hello obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="47a42-122">Monitor how hello workspace is being used</span></span>
* <span data-ttu-id="47a42-123">Konfigurowanie hello tooallow obszaru roboczego lub odmowa dostępu</span><span class="sxs-lookup"><span data-stu-id="47a42-123">Configure hello workspace tooallow or deny access</span></span>
* <span data-ttu-id="47a42-124">Zarządzanie usługami sieci Web utworzona w obszarze roboczym hello</span><span class="sxs-lookup"><span data-stu-id="47a42-124">Manage Web services created in hello workspace</span></span>
* <span data-ttu-id="47a42-125">Usuwanie obszaru roboczego hello</span><span class="sxs-lookup"><span data-stu-id="47a42-125">Delete hello workspace</span></span>

<span data-ttu-id="47a42-126">Ponadto hello karty Pulpit nawigacyjny zawiera omówienie użycie obszaru roboczego i szybkiego dostępu informacji obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="47a42-126">In addition, hello dashboard tab provides an overview of your workspace usage and a quick glance of your workspace information.</span></span>  

> [!TIP]
> <span data-ttu-id="47a42-127">W usłudze Azure Machine Learning Studio na powitania **usług sieci WEB** karcie, można dodać, zaktualizować lub usunąć usługi Machine Learning w sieci Web.</span><span class="sxs-lookup"><span data-stu-id="47a42-127">In Azure Machine Learning Studio, on hello **WEB SERVICES** tab, you can add, update, or delete a Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="47a42-128">toomanage obszaru roboczego w hello klasycznego portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="47a42-128">toomanage a workspace in hello Azure classic portal:</span></span>

1. <span data-ttu-id="47a42-129">Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com/) konta przy użyciu platformy Microsoft Azure — należy użyć konta hello, skojarzoną z hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="47a42-129">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use hello account that's associated with hello Azure subscription.</span></span>
2. <span data-ttu-id="47a42-130">Witaj Panel usługi Microsoft Azure, kliknij przycisk **UCZENIA MASZYNOWEGO**.</span><span class="sxs-lookup"><span data-stu-id="47a42-130">In hello Microsoft Azure services panel, click **MACHINE LEARNING**.</span></span>
3. <span data-ttu-id="47a42-131">Kliknij obszar roboczy hello ma toomanage.</span><span class="sxs-lookup"><span data-stu-id="47a42-131">Click hello workspace you want toomanage.</span></span>

<span data-ttu-id="47a42-132">Strona obszaru roboczego Hello zawiera trzy karty:</span><span class="sxs-lookup"><span data-stu-id="47a42-132">hello workspace page has three tabs:</span></span>

* <span data-ttu-id="47a42-133">**Pulpit NAWIGACYJNY** — pozwala tooview użycia obszaru roboczego i informacji</span><span class="sxs-lookup"><span data-stu-id="47a42-133">**DASHBOARD** - Allows you tooview workspace usage and information</span></span>
* <span data-ttu-id="47a42-134">**Konfiguruj** — pozwala toomanage dostępu toohello roboczym</span><span class="sxs-lookup"><span data-stu-id="47a42-134">**CONFIGURE** - Allows you toomanage access toohello workspace</span></span>
* <span data-ttu-id="47a42-135">**USŁUGI sieci WEB** — pozwala toomanage usług sieci Web, które zostały opublikowane z tego obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="47a42-135">**WEB SERVICES** - Allows you toomanage Web services that have been published from this workspace</span></span>

### <a name="toomonitor-how-hello-workspace-is-being-used"></a><span data-ttu-id="47a42-136">toomonitor sposobu używania hello obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="47a42-136">toomonitor how hello workspace is being used</span></span>
<span data-ttu-id="47a42-137">Kliknij przycisk hello **pulpitu NAWIGACYJNEGO** kartę.</span><span class="sxs-lookup"><span data-stu-id="47a42-137">Click hello **DASHBOARD** tab.</span></span>

<span data-ttu-id="47a42-138">Z poziomu pulpitu nawigacyjnego hello możesz wyświetlić ogólne użycie obszaru roboczego i uzyskać szybkiego dostępu informacji obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="47a42-138">From hello dashboard, you can view overall usage of your workspace and get a quick glance of workspace information.</span></span>

* <span data-ttu-id="47a42-139">Witaj **OBLICZENIOWE** wykres zawiera zasoby obliczeniowe hello używany przez hello obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="47a42-139">hello **COMPUTE** chart shows hello compute resources being used by hello workspace.</span></span> <span data-ttu-id="47a42-140">Można zmienić toodisplay widoku hello względną lub bezwzględną wartości, a przedział czasu hello wyświetlane na wykresie hello można zmienić.</span><span class="sxs-lookup"><span data-stu-id="47a42-140">You can change hello view toodisplay relative or absolute values, and you can change hello timeframe displayed in hello chart.</span></span>
* <span data-ttu-id="47a42-141">**Przegląd wykorzystania** Wyświetla magazynu Azure używany przez hello obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="47a42-141">**Usage overview** displays Azure storage being used by hello workspace.</span></span>
* <span data-ttu-id="47a42-142">**Szybkiego dostępu** zawiera podsumowanie informacji obszaru roboczego i przydatne łącza.</span><span class="sxs-lookup"><span data-stu-id="47a42-142">**Quick glance** provides a summary of workspace information and useful links.</span></span>

> [!NOTE]
> <span data-ttu-id="47a42-143">Witaj **logowania tooML Studio** łącze powoduje otwarcie przy użyciu hello Account Microsoft użytkownik jest już zarejestrowany w usłudze Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="47a42-143">hello **Sign-in tooML Studio** link opens Machine Learning Studio using hello Microsoft Account you are currently signed into.</span></span> <span data-ttu-id="47a42-144">Witaj Account Microsoft toosign jest używany w toohello klasycznego portalu Azure toocreate obszaru roboczego nie ma automatycznie tooopen uprawnienia tego obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="47a42-144">hello Microsoft Account you used toosign in toohello Azure classic portal toocreate a workspace does not automatically have permission tooopen that workspace.</span></span> <span data-ttu-id="47a42-145">tooopen obszaru roboczego, musisz zarejestrować się w toohello Account Microsoft został zdefiniowany jako hello właściciela obszaru roboczego hello, lub należy tooreceive zaproszenia od hello właściciela toojoin hello roboczym.</span><span class="sxs-lookup"><span data-stu-id="47a42-145">tooopen a workspace, you must be signed in toohello Microsoft Account that was defined as hello owner of hello workspace, or you need tooreceive an invitation from hello owner toojoin hello workspace.</span></span>
> 
> 

### <a name="toogrant-or-suspend-access-for-users"></a><span data-ttu-id="47a42-146">toogrant lub zawiesić dostęp dla użytkowników</span><span class="sxs-lookup"><span data-stu-id="47a42-146">toogrant or suspend access for users</span></span>
<span data-ttu-id="47a42-147">Kliknij przycisk hello **Konfiguruj** kartę.</span><span class="sxs-lookup"><span data-stu-id="47a42-147">Click hello **CONFIGURE** tab.</span></span>

<span data-ttu-id="47a42-148">Karta Konfiguracja hello można:</span><span class="sxs-lookup"><span data-stu-id="47a42-148">From hello configuration tab you can:</span></span>

* <span data-ttu-id="47a42-149">Wstrzymaj obszaru roboczego uczenia maszynowego toohello dostępu, klikając przycisk ODMÓW.</span><span class="sxs-lookup"><span data-stu-id="47a42-149">Suspend access toohello Machine Learning workspace by clicking DENY.</span></span> <span data-ttu-id="47a42-150">Użytkownicy będą już mogli tooopen hello roboczym w usłudze Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="47a42-150">Users will no longer be able tooopen hello workspace in Machine Learning Studio.</span></span> <span data-ttu-id="47a42-151">toorestore dostępu, kliknij przycisk Zezwalaj.</span><span class="sxs-lookup"><span data-stu-id="47a42-151">toorestore access, click ALLOW.</span></span>

<span data-ttu-id="47a42-152">toomanage dodatkowych kont mających roboczym toohello dostępu w usłudze Machine Learning Studio, kliknij przycisk **logowania tooML Studio** w hello **pulpitu NAWIGACYJNEGO** kartę (patrz Uwaga poprzedzających hello dotyczące  **Sign-in tooML Studio**).</span><span class="sxs-lookup"><span data-stu-id="47a42-152">toomanage additional accounts who have access toohello workspace in Machine Learning Studio, click **Sign-in tooML Studio** in hello **DASHBOARD** tab (see hello preceeding note regarding **Sign-in tooML Studio**).</span></span> <span data-ttu-id="47a42-153">Spowoduje to otwarcie hello obszaru roboczego usługi Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="47a42-153">This opens hello workspace in Machine Learning Studio.</span></span> <span data-ttu-id="47a42-154">W tym miejscu, kliknij przycisk hello **ustawienia** kartę, a następnie **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="47a42-154">From here, click hello **SETTINGS** tab and then **USERS**.</span></span> <span data-ttu-id="47a42-155">Możesz kliknąć **ZAPROSIĆ użytkowników więcej** toogive użytkowników dostępu toohello obszaru roboczego, lub wybierz użytkownika i kliknij przycisk **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="47a42-155">You can click **INVITE MORE USERS** toogive users access toohello workspace, or select a user and click **REMOVE**.</span></span>

### <a name="toomanage-web-services-in-this-workspace"></a><span data-ttu-id="47a42-156">usługi sieci web toomanage w tym obszarze roboczym</span><span class="sxs-lookup"><span data-stu-id="47a42-156">toomanage web services in this workspace</span></span>
<span data-ttu-id="47a42-157">Kliknij przycisk hello **usług sieci WEB** kartę.</span><span class="sxs-lookup"><span data-stu-id="47a42-157">Click hello **WEB SERVICES** tab.</span></span>

<span data-ttu-id="47a42-158">Spowoduje to wyświetlenie listy publikowane z tym obszarem roboczym usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="47a42-158">This displays a list of web services published from this workspace.</span></span>
<span data-ttu-id="47a42-159">toomanage usługi sieci web, kliknij nazwę hello tooopen listy hello hello strony usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="47a42-159">toomanage a web service, click hello name in hello list tooopen hello Web service page.</span></span>

<span data-ttu-id="47a42-160">Usługi sieci Web może mieć co najmniej jeden zdefiniowanych punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="47a42-160">A Web service may have one or more endpoints defined.</span></span>

* <span data-ttu-id="47a42-161">Można zdefiniować więcej punktów końcowych w punkcie końcowym Dodawanie toohello "Default".</span><span class="sxs-lookup"><span data-stu-id="47a42-161">You can define more endpoints in addition toohello "Default" endpoint.</span></span> <span data-ttu-id="47a42-162">tooadd hello punktu końcowego, kliknij przycisk **zarządzanie punktami końcowymi** u dołu hello hello pulpitu nawigacyjnego tooopen hello usługi sieci Web systemu Azure Machine Learning portalu.</span><span class="sxs-lookup"><span data-stu-id="47a42-162">tooadd hello endpoint, click **Manage Endpoints** at hello bottom of hello dashboard tooopen hello Azure Machine Learning Web Services portal.</span></span>
* <span data-ttu-id="47a42-163">toodelete punktu końcowego (nie można usunąć punktu końcowego hello "Default"), kliknij pole wyboru hello na początku hello hello wiersza punktu końcowego, a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="47a42-163">toodelete an endpoint (you cannot delete hello "Default" endpoint), click hello check box at hello beginning of hello endpoint row, and click **DELETE**.</span></span> <span data-ttu-id="47a42-164">Spowoduje to usunięcie punktu końcowego hello z hello usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="47a42-164">This removes hello endpoint from hello Web service.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="47a42-165">Jeśli aplikacja używa punkt końcowy usługi sieci web powitania po usunięciu punktu końcowego hello, aplikacji hello zostanie wyświetlony błąd hello następnym próbuje tooaccess hello usługi.</span><span class="sxs-lookup"><span data-stu-id="47a42-165">If an application is using hello web service endpoint when hello endpoint is deleted, hello application will receive an error hello next time it tries tooaccess hello service.</span></span>
  > 
  > 

<span data-ttu-id="47a42-166">Kliknij nazwę hello tooopen punkt końcowy usługi sieci Web go.</span><span class="sxs-lookup"><span data-stu-id="47a42-166">Click hello name of a Web service endpoint tooopen it.</span></span> 

<span data-ttu-id="47a42-167">Z poziomu pulpitu nawigacyjnego hello można wyświetlić ogólne użycie usługi sieci Web w danym okresie czasu.</span><span class="sxs-lookup"><span data-stu-id="47a42-167">From hello dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="47a42-168">Możesz wybrać tooview okresu hello z menu rozwijanego okresu hello w prawym górnym rogu hello hello użycia wykresów.</span><span class="sxs-lookup"><span data-stu-id="47a42-168">You can select hello period tooview from hello Period dropdown menu in hello upper right of hello usage charts.</span></span> <span data-ttu-id="47a42-169">pulpit nawigacyjny Hello zawiera hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="47a42-169">hello dashboard shows hello following information:</span></span>

* <span data-ttu-id="47a42-170">**Żądań w czasie** wykres krok hello liczba żądań za pośrednictwem hello w wybranym okresie.</span><span class="sxs-lookup"><span data-stu-id="47a42-170">**Requests Over Time** displays a step graph of hello number of requests over hello selected time period.</span></span> <span data-ttu-id="47a42-171">Może pomóc ustalić, czy występują wzrostów użycia.</span><span class="sxs-lookup"><span data-stu-id="47a42-171">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="47a42-172">**Żądanie-odpowiedź żądań** Wyświetla hello łączna liczba wywołań żądań i odpowiedzi usługi hello odebrał za pośrednictwem hello wybrany okres czasu i ile z nich nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="47a42-172">**Request-Response Requests** displays hello total number of Request-Response calls hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="47a42-173">**Średni czas obliczeniowe żądanie-odpowiedź** wyświetla średni czas hello potrzebne tooexecute hello odebranych żądań.</span><span class="sxs-lookup"><span data-stu-id="47a42-173">**Average Request-Response Compute Time** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="47a42-174">**Partie żądania** Wyświetla hello łączna liczba żądań wsadowych hello usługi odebrał w wybranym okresie hello i ile z nich nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="47a42-174">**Batch Requests** displays hello total number of Batch Requests hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="47a42-175">**Średni czas oczekiwania zadania** wyświetla średni czas hello potrzebne tooexecute hello odebranych żądań.</span><span class="sxs-lookup"><span data-stu-id="47a42-175">**Average Job Latency** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="47a42-176">**Błędy** Wyświetla hello łączna liczba błędów, które wystąpiły w usłudze sieci web toohello wywołania.</span><span class="sxs-lookup"><span data-stu-id="47a42-176">**Errors** displays hello aggregate number of errors that have occurred on calls toohello web service.</span></span>
* <span data-ttu-id="47a42-177">**Koszty usługi** Wyświetla hello opłat za hello plan rozliczeniowy skojarzonych z usługą hello.</span><span class="sxs-lookup"><span data-stu-id="47a42-177">**Services Costs** displays hello charges for hello billing plan associated with hello service.</span></span>

<span data-ttu-id="47a42-178">Na stronie Konfiguruj hello można zaktualizować hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="47a42-178">From hello Configure page, you can update hello following properties:</span></span>

* <span data-ttu-id="47a42-179">**Opis elementu** pozwala tooenter opis hello usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="47a42-179">**Description** allows you tooenter a description for hello Web service.</span></span> <span data-ttu-id="47a42-180">Opis jest polem wymaganym.</span><span class="sxs-lookup"><span data-stu-id="47a42-180">Description is a required field.</span></span>
* <span data-ttu-id="47a42-181">**Rejestrowanie** pozwala błąd tooenable lub Wyłącz rejestrowanie hello w punkcie końcowym.</span><span class="sxs-lookup"><span data-stu-id="47a42-181">**Logging** allows you tooenable or disable error logging on hello endpoint.</span></span> <span data-ttu-id="47a42-182">Aby uzyskać więcej informacji, zobacz Włącz [rejestrowania dla usług sieci web uczenie maszynowe](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="47a42-182">For more information on Logging, see Enable [logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>
* <span data-ttu-id="47a42-183">**Włącz przykładowe dane** pozwala tooprovide przykładowych danych służy tootest hello żądań i odpowiedzi usługi.</span><span class="sxs-lookup"><span data-stu-id="47a42-183">**Enable Sample data** allows you tooprovide sample data that you can use tootest hello Request-Response service.</span></span> <span data-ttu-id="47a42-184">Jeśli utworzono hello usługi sieci web w usłudze Machine Learning Studio hello przykładowych danych jest pobierana z danych hello sieci używanych tootrain modelu.</span><span class="sxs-lookup"><span data-stu-id="47a42-184">If you created hello web service in Machine Learning Studio, hello sample data is taken from hello data your used tootrain your model.</span></span> <span data-ttu-id="47a42-185">Jeśli utworzono usługi hello programowo, hello dane są pobierane z hello przykładowe dane podane jako część pakietu hello JSON.</span><span class="sxs-lookup"><span data-stu-id="47a42-185">If you created hello service programmatically, hello data is taken from hello example data you provided as part of hello JSON package.</span></span>

