---
title: "Zarządzanie obszaru roboczego usługi Machine Learning | Dokumentacja firmy Microsoft"
description: "Zarządzanie dostępem do usługi Azure Machine Learning obszary robocze oraz wdrażania i zarządzania nimi usług sieci web interfejsu API uczenia Maszynowego"
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
ms.openlocfilehash: 94800f51baf83311c33490cada5f991ff2101da9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-an-azure-machine-learning-workspace"></a><span data-ttu-id="49017-103">Zarządzanie obszarem roboczym usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="49017-103">Manage an Azure Machine Learning workspace</span></span>

> [!NOTE]
> <span data-ttu-id="49017-104">Informacje na temat zarządzania usługami sieci Web w portalu usługi sieci Web usługi Machine Learning, zobacz [zarządzania usługi sieci Web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="49017-104">For information on managing Web services in the Machine Learning Web Services portal, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span>
> 
> 

<span data-ttu-id="49017-105">Możesz zarządzać obszarów roboczych uczenia maszynowego w portalu Azure lub klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="49017-105">You can manage Machine Learning workspaces in either the Azure portal or the Azure classic portal.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-the-azure-portal"></a><span data-ttu-id="49017-106">Korzystanie z witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="49017-106">Use the Azure portal</span></span>

<span data-ttu-id="49017-107">Aby zarządzać obszaru roboczego w portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="49017-107">To manage a workspace in the Azure portal:</span></span>

1. <span data-ttu-id="49017-108">Zaloguj się do [portalu Azure](https://portal.azure.com/) przy użyciu konta administratora subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="49017-108">Sign in to the [Azure portal](https://portal.azure.com/) using an Azure subscription administrator account.</span></span>
2. <span data-ttu-id="49017-109">W polu wyszukiwania w górnej części strony wprowadź "komputera learning obszary robocze", a następnie wybierz **obszarów roboczych Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="49017-109">In the search box at the top of the page, enter "machine learning workspaces" and then select **Machine Learning Workspaces**.</span></span>
3. <span data-ttu-id="49017-110">Kliknij obszar roboczy, którą chcesz zarządzać.</span><span class="sxs-lookup"><span data-stu-id="49017-110">Click the workspace you want to manage.</span></span>

<span data-ttu-id="49017-111">Oprócz informacji o zarządzaniu standardowych zasobów i dostępne opcje można:</span><span class="sxs-lookup"><span data-stu-id="49017-111">In addition to the standard resource management information and options available, you can:</span></span>

- <span data-ttu-id="49017-112">Widok **właściwości** — ta strona zawiera informacje dotyczące obszaru roboczego i zasobów, a można zmienić ten obszar roboczy jest połączony z grupą subskrypcji i zasobu.</span><span class="sxs-lookup"><span data-stu-id="49017-112">View **Properties** - This page displays the workspace and resource information, and you can change the subscription and resource group that this workspace is connected with.</span></span>
- <span data-ttu-id="49017-113">**Ponownej synchronizacji magazynu kluczy** -obszar roboczy obsługuje kluczy do konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="49017-113">**Resync Storage Keys** - The workspace maintains keys to the storage account.</span></span> <span data-ttu-id="49017-114">Jeśli zmienia się na koncie magazynu kluczy, a następnie kliknięcie **ponownej synchronizacji kluczy** zsynchronizować klucze z obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="49017-114">If the storage account changes keys, then you can click **Resync keys** to synchronize the keys with the workspace.</span></span>

<span data-ttu-id="49017-115">Aby zarządzać usługami sieci web skojarzony z tym obszarem roboczym, należy korzystać z portalu usługi sieci Web usługi Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="49017-115">To manage the web services associated with this workspace, use the Machine Learning Web Services portal.</span></span> <span data-ttu-id="49017-116">Zobacz [zarządzania usługi sieci Web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning](machine-learning-manage-new-webservice.md) pełne informacje.</span><span class="sxs-lookup"><span data-stu-id="49017-116">See [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md) for complete information.</span></span>

> [!NOTE]
> <span data-ttu-id="49017-117">Aby wdrożyć lub zarządzać nowych usług sieci web musi mieć przypisaną rolę współautora lub administrator w subskrypcji, w której wdrażana jest usługa sieci web.</span><span class="sxs-lookup"><span data-stu-id="49017-117">To deploy or manage New web services you must be assigned a contributor or administrator role on the subscription to which the web service is deployed.</span></span> <span data-ttu-id="49017-118">Jeśli musisz poprosić innego użytkownika do obszaru roboczego uczenia maszynowego, należy je przypisać do roli współautora lub administratora dla subskrypcji przed wdrożeniem lub zarządzania usługami sieci web.</span><span class="sxs-lookup"><span data-stu-id="49017-118">If you invite another user to a machine learning workspace, you must assign them to a contributor or administrator role on the subscription before they can deploy or manage web services.</span></span> 
> 
><span data-ttu-id="49017-119">Aby uzyskać więcej informacji o ustawianiu uprawnień dostępu, zobacz [Wyświetl przypisania dostępu dla użytkowników i grup w portalu Azure - publicznej wersji zapoznawczej](../active-directory/role-based-access-control-manage-assignments.md).</span><span class="sxs-lookup"><span data-stu-id="49017-119">For more information on setting access permissions, see [View access assignments for users and groups in the Azure portal - Public preview](../active-directory/role-based-access-control-manage-assignments.md).</span></span>

## <a name="use-the-azure-classic-portal"></a><span data-ttu-id="49017-120">Użyj klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="49017-120">Use the Azure classic portal</span></span>

<span data-ttu-id="49017-121">Przy użyciu klasycznego portalu Azure, można zarządzać do uczenia maszynowego obszarów roboczych:</span><span class="sxs-lookup"><span data-stu-id="49017-121">Using the Azure classic portal, you can manage your Machine Learning workspaces to:</span></span>

* <span data-ttu-id="49017-122">Monitorowanie, sposobu używania obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="49017-122">Monitor how the workspace is being used</span></span>
* <span data-ttu-id="49017-123">Konfiguruj obszar roboczy, aby zezwolić lub odmówić dostępu</span><span class="sxs-lookup"><span data-stu-id="49017-123">Configure the workspace to allow or deny access</span></span>
* <span data-ttu-id="49017-124">Zarządzanie usługami sieci Web utworzona w obszarze roboczym</span><span class="sxs-lookup"><span data-stu-id="49017-124">Manage Web services created in the workspace</span></span>
* <span data-ttu-id="49017-125">Usuwanie obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="49017-125">Delete the workspace</span></span>

<span data-ttu-id="49017-126">Ponadto karty Pulpit nawigacyjny zawiera omówienie użycie obszaru roboczego i szybkiego dostępu informacji obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="49017-126">In addition, the dashboard tab provides an overview of your workspace usage and a quick glance of your workspace information.</span></span>  

> [!TIP]
> <span data-ttu-id="49017-127">W usłudze Azure Machine Learning Studio na **usług sieci WEB** karcie, można dodać, zaktualizować lub usunąć usługi Machine Learning w sieci Web.</span><span class="sxs-lookup"><span data-stu-id="49017-127">In Azure Machine Learning Studio, on the **WEB SERVICES** tab, you can add, update, or delete a Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="49017-128">Aby zarządzać obszaru roboczego w klasycznym portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="49017-128">To manage a workspace in the Azure classic portal:</span></span>

1. <span data-ttu-id="49017-129">Zaloguj się do [klasycznego portalu Azure](https://manage.windowsazure.com/) konta przy użyciu platformy Microsoft Azure — należy użyć konta, na którym jest skojarzony z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="49017-129">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use the account that's associated with the Azure subscription.</span></span>
2. <span data-ttu-id="49017-130">W panelu usługi Microsoft Azure, kliknij przycisk **UCZENIA MASZYNOWEGO**.</span><span class="sxs-lookup"><span data-stu-id="49017-130">In the Microsoft Azure services panel, click **MACHINE LEARNING**.</span></span>
3. <span data-ttu-id="49017-131">Kliknij obszar roboczy, którą chcesz zarządzać.</span><span class="sxs-lookup"><span data-stu-id="49017-131">Click the workspace you want to manage.</span></span>

<span data-ttu-id="49017-132">Strona obszaru roboczego zawiera trzy karty:</span><span class="sxs-lookup"><span data-stu-id="49017-132">The workspace page has three tabs:</span></span>

* <span data-ttu-id="49017-133">**Pulpit NAWIGACYJNY** — pozwala na wyświetlanie obszaru roboczego użycia i informacji</span><span class="sxs-lookup"><span data-stu-id="49017-133">**DASHBOARD** - Allows you to view workspace usage and information</span></span>
* <span data-ttu-id="49017-134">**Konfiguruj** — umożliwia zarządzanie dostępem do obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="49017-134">**CONFIGURE** - Allows you to manage access to the workspace</span></span>
* <span data-ttu-id="49017-135">**USŁUGI sieci WEB** — umożliwia zarządzanie usługami sieci Web, które zostały opublikowane z tego obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="49017-135">**WEB SERVICES** - Allows you to manage Web services that have been published from this workspace</span></span>

### <a name="to-monitor-how-the-workspace-is-being-used"></a><span data-ttu-id="49017-136">Aby monitorować sposobu używania obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="49017-136">To monitor how the workspace is being used</span></span>
<span data-ttu-id="49017-137">Kliknij przycisk **pulpitu NAWIGACYJNEGO** kartę.</span><span class="sxs-lookup"><span data-stu-id="49017-137">Click the **DASHBOARD** tab.</span></span>

<span data-ttu-id="49017-138">Na pulpicie nawigacyjnym możesz wyświetlić ogólne użycie obszaru roboczego i uzyskać szybkiego dostępu informacji obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="49017-138">From the dashboard, you can view overall usage of your workspace and get a quick glance of workspace information.</span></span>

* <span data-ttu-id="49017-139">**OBLICZENIOWE** wykres zawiera zasoby obliczeniowe, używany przez obszar roboczy.</span><span class="sxs-lookup"><span data-stu-id="49017-139">The **COMPUTE** chart shows the compute resources being used by the workspace.</span></span> <span data-ttu-id="49017-140">Można zmienić widok, aby wyświetlić względną lub bezwzględną wartości, a można zmienić zakres czasu wyświetlane na wykresie.</span><span class="sxs-lookup"><span data-stu-id="49017-140">You can change the view to display relative or absolute values, and you can change the timeframe displayed in the chart.</span></span>
* <span data-ttu-id="49017-141">**Przegląd wykorzystania** Wyświetla magazynu Azure używany przez obszar roboczy.</span><span class="sxs-lookup"><span data-stu-id="49017-141">**Usage overview** displays Azure storage being used by the workspace.</span></span>
* <span data-ttu-id="49017-142">**Szybkiego dostępu** zawiera podsumowanie informacji obszaru roboczego i przydatne łącza.</span><span class="sxs-lookup"><span data-stu-id="49017-142">**Quick glance** provides a summary of workspace information and useful links.</span></span>

> [!NOTE]
> <span data-ttu-id="49017-143">**Zalogować się do ML Studio** łącze powoduje otwarcie przy użyciu Account Microsoft jest obecnie zarejestrowany w usłudze Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="49017-143">The **Sign-in to ML Studio** link opens Machine Learning Studio using the Microsoft Account you are currently signed into.</span></span> <span data-ttu-id="49017-144">Account firmy Microsoft, używanego do logowania się do klasycznego portalu Azure do utworzenia obszaru roboczego nie ma automatycznie uprawnień do otwierania tego obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="49017-144">The Microsoft Account you used to sign in to the Azure classic portal to create a workspace does not automatically have permission to open that workspace.</span></span> <span data-ttu-id="49017-145">Aby otworzyć obszar roboczy, użytkownik musi zalogować się Account firmy Microsoft, która została zdefiniowana jako właściciela obszaru roboczego lub konieczność odbierania zaproszenia od właściciela do obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="49017-145">To open a workspace, you must be signed in to the Microsoft Account that was defined as the owner of the workspace, or you need to receive an invitation from the owner to join the workspace.</span></span>
> 
> 

### <a name="to-grant-or-suspend-access-for-users"></a><span data-ttu-id="49017-146">Aby przydzielić lub zawiesić dostęp dla użytkowników</span><span class="sxs-lookup"><span data-stu-id="49017-146">To grant or suspend access for users</span></span>
<span data-ttu-id="49017-147">Kliknij przycisk **Konfiguruj** kartę.</span><span class="sxs-lookup"><span data-stu-id="49017-147">Click the **CONFIGURE** tab.</span></span>

<span data-ttu-id="49017-148">Na karcie Konfiguracja można:</span><span class="sxs-lookup"><span data-stu-id="49017-148">From the configuration tab you can:</span></span>

* <span data-ttu-id="49017-149">Zawiesić dostęp do obszaru roboczego uczenia maszynowego, klikając przycisk ODMÓW.</span><span class="sxs-lookup"><span data-stu-id="49017-149">Suspend access to the Machine Learning workspace by clicking DENY.</span></span> <span data-ttu-id="49017-150">Użytkownicy nie będą już mogli otworzyć obszar roboczy w usłudze Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="49017-150">Users will no longer be able to open the workspace in Machine Learning Studio.</span></span> <span data-ttu-id="49017-151">Aby przywrócić dostęp, kliknij przycisk Zezwalaj.</span><span class="sxs-lookup"><span data-stu-id="49017-151">To restore access, click ALLOW.</span></span>

<span data-ttu-id="49017-152">Aby zarządzać dodatkowych kont, którzy mają dostęp do obszaru roboczego usługi Machine Learning Studio, kliknij przycisk **zalogować się do ML Studio** w **pulpitu NAWIGACYJNEGO** kartę (patrz Uwaga poprzedzających dotyczące **zalogować się do ML Studio**).</span><span class="sxs-lookup"><span data-stu-id="49017-152">To manage additional accounts who have access to the workspace in Machine Learning Studio, click **Sign-in to ML Studio** in the **DASHBOARD** tab (see the preceeding note regarding **Sign-in to ML Studio**).</span></span> <span data-ttu-id="49017-153">Spowoduje to otwarcie obszaru roboczego usługi Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="49017-153">This opens the workspace in Machine Learning Studio.</span></span> <span data-ttu-id="49017-154">W tym miejscu, kliknij przycisk **ustawienia** kartę, a następnie **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="49017-154">From here, click the **SETTINGS** tab and then **USERS**.</span></span> <span data-ttu-id="49017-155">Możesz kliknąć **ZAPROSIĆ użytkowników więcej** udzielać użytkownikom dostępu do obszaru roboczego, lub wybierz użytkownika i kliknij przycisk **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="49017-155">You can click **INVITE MORE USERS** to give users access to the workspace, or select a user and click **REMOVE**.</span></span>

### <a name="to-manage-web-services-in-this-workspace"></a><span data-ttu-id="49017-156">Do zarządzania usługami sieci web, w tym obszarze roboczym</span><span class="sxs-lookup"><span data-stu-id="49017-156">To manage web services in this workspace</span></span>
<span data-ttu-id="49017-157">Kliknij przycisk **usług sieci WEB** kartę.</span><span class="sxs-lookup"><span data-stu-id="49017-157">Click the **WEB SERVICES** tab.</span></span>

<span data-ttu-id="49017-158">Spowoduje to wyświetlenie listy publikowane z tym obszarem roboczym usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="49017-158">This displays a list of web services published from this workspace.</span></span>
<span data-ttu-id="49017-159">Aby zarządzać usługą sieci web, kliknij nazwę na liście, aby otworzyć stronę usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="49017-159">To manage a web service, click the name in the list to open the Web service page.</span></span>

<span data-ttu-id="49017-160">Usługi sieci Web może mieć co najmniej jeden zdefiniowanych punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="49017-160">A Web service may have one or more endpoints defined.</span></span>

* <span data-ttu-id="49017-161">Można zdefiniować więcej punktów końcowych oprócz punktu końcowego "Domyślny".</span><span class="sxs-lookup"><span data-stu-id="49017-161">You can define more endpoints in addition to the "Default" endpoint.</span></span> <span data-ttu-id="49017-162">Aby dodać punkt końcowy, kliknij przycisk **zarządzanie punktami końcowymi** w dolnej części pulpitu nawigacyjnego, aby otworzyć portal usługi sieci Web systemu Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="49017-162">To add the endpoint, click **Manage Endpoints** at the bottom of the dashboard to open the Azure Machine Learning Web Services portal.</span></span>
* <span data-ttu-id="49017-163">Aby usunąć punkt końcowy (nie można usunąć punktu końcowego "Domyślne"), kliknij pole wyboru na początku wiersza punktu końcowego, a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="49017-163">To delete an endpoint (you cannot delete the "Default" endpoint), click the check box at the beginning of the endpoint row, and click **DELETE**.</span></span> <span data-ttu-id="49017-164">Spowoduje to usunięcie punkt końcowy usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="49017-164">This removes the endpoint from the Web service.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="49017-165">Jeśli aplikacja używa punkt końcowy usługi sieci web po usunięciu punktu końcowego, aplikacji spowoduje wystąpienie błędu podczas kolejnej próby uzyskania dostępu do usługi.</span><span class="sxs-lookup"><span data-stu-id="49017-165">If an application is using the web service endpoint when the endpoint is deleted, the application will receive an error the next time it tries to access the service.</span></span>
  > 
  > 

<span data-ttu-id="49017-166">Kliknij nazwę punktu końcowego usługi sieci Web, aby go otworzyć.</span><span class="sxs-lookup"><span data-stu-id="49017-166">Click the name of a Web service endpoint to open it.</span></span> 

<span data-ttu-id="49017-167">Z poziomu pulpitu nawigacyjnego można wyświetlić ogólne użycie usługi sieci Web w danym okresie czasu.</span><span class="sxs-lookup"><span data-stu-id="49017-167">From the dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="49017-168">Można wybrać okres, aby wyświetlić z menu rozwijanego okresu, w prawym górnym rogu wykresy użycia.</span><span class="sxs-lookup"><span data-stu-id="49017-168">You can select the period to view from the Period dropdown menu in the upper right of the usage charts.</span></span> <span data-ttu-id="49017-169">Pulpit nawigacyjny zawiera następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="49017-169">The dashboard shows the following information:</span></span>

* <span data-ttu-id="49017-170">**Żądań w czasie** wykres krok to liczba żądań przez wybrany okres czasu.</span><span class="sxs-lookup"><span data-stu-id="49017-170">**Requests Over Time** displays a step graph of the number of requests over the selected time period.</span></span> <span data-ttu-id="49017-171">Może pomóc ustalić, czy występują wzrostów użycia.</span><span class="sxs-lookup"><span data-stu-id="49017-171">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="49017-172">**Żądanie-odpowiedź żądań** Wyświetla całkowitą liczbę wywołań żądań i odpowiedzi usługa odebrała przez wybrany okres czasu i ile z nich nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="49017-172">**Request-Response Requests** displays the total number of Request-Response calls the service has received over the selected time period and how many of them failed.</span></span>
* <span data-ttu-id="49017-173">**Średni czas obliczeniowe żądanie-odpowiedź** wyświetla średni czas potrzebny na wykonanie odebranych żądań.</span><span class="sxs-lookup"><span data-stu-id="49017-173">**Average Request-Response Compute Time** displays an average of the time needed to execute the received requests.</span></span>
* <span data-ttu-id="49017-174">**Partie żądania** Wyświetla całkowitą liczbę żądań wsadowych usługa odebrała przez wybrany okres czasu i ile z nich nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="49017-174">**Batch Requests** displays the total number of Batch Requests the service has received over the selected time period and how many of them failed.</span></span>
* <span data-ttu-id="49017-175">**Średni czas oczekiwania zadania** wyświetla średni czas potrzebny na wykonanie odebranych żądań.</span><span class="sxs-lookup"><span data-stu-id="49017-175">**Average Job Latency** displays an average of the time needed to execute the received requests.</span></span>
* <span data-ttu-id="49017-176">**Błędy** Wyświetla łączna liczba błędów, które wystąpiły na połączenia z usługą sieci web.</span><span class="sxs-lookup"><span data-stu-id="49017-176">**Errors** displays the aggregate number of errors that have occurred on calls to the web service.</span></span>
* <span data-ttu-id="49017-177">**Koszty usługi** Wyświetla opłat za plan rozliczeniowy skojarzony z usługą.</span><span class="sxs-lookup"><span data-stu-id="49017-177">**Services Costs** displays the charges for the billing plan associated with the service.</span></span>

<span data-ttu-id="49017-178">Na stronie Konfiguracja można aktualizować następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="49017-178">From the Configure page, you can update the following properties:</span></span>

* <span data-ttu-id="49017-179">**Opis elementu** umożliwia wprowadzenie opisu usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="49017-179">**Description** allows you to enter a description for the Web service.</span></span> <span data-ttu-id="49017-180">Opis jest polem wymaganym.</span><span class="sxs-lookup"><span data-stu-id="49017-180">Description is a required field.</span></span>
* <span data-ttu-id="49017-181">**Rejestrowanie** umożliwia włączanie lub wyłączanie rejestrowania w punkcie końcowym błędów.</span><span class="sxs-lookup"><span data-stu-id="49017-181">**Logging** allows you to enable or disable error logging on the endpoint.</span></span> <span data-ttu-id="49017-182">Aby uzyskać więcej informacji, zobacz Włącz [rejestrowania dla usług sieci web uczenie maszynowe](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="49017-182">For more information on Logging, see Enable [logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>
* <span data-ttu-id="49017-183">**Włącz przykładowe dane** umożliwia podanie przykładowych danych, które służy do testowania usługi żądań i odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="49017-183">**Enable Sample data** allows you to provide sample data that you can use to test the Request-Response service.</span></span> <span data-ttu-id="49017-184">Jeśli utworzono usługę sieci web w usłudze Machine Learning Studio przykładowych danych jest pobierana z danych użytkownika używanych do uczenia modelu.</span><span class="sxs-lookup"><span data-stu-id="49017-184">If you created the web service in Machine Learning Studio, the sample data is taken from the data your used to train your model.</span></span> <span data-ttu-id="49017-185">Jeśli usługi zostały utworzone programowo, dane są pobierane z przykładowe dane podane jako część pakietu JSON.</span><span class="sxs-lookup"><span data-stu-id="49017-185">If you created the service programmatically, the data is taken from the example data you provided as part of the JSON package.</span></span>

