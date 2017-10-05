---
title: "Informacje o sposobie zarządzania przy użyciu interfejsu API zarządzania usługami sieci web uczenie maszynowe Azure | Dokumentacja firmy Microsoft"
description: "Przewodnik pokazujący sposób zarządzania przy użyciu interfejsu API zarządzania usługami sieci web uczenie maszynowe Azure."
keywords: "uczenia maszynowego, zarządzanie interfejsami api"
services: machine-learning
documentationcenter: 
author: roalexan
manager: jhubbard
editor: 
ms.assetid: 05150ae1-5b6a-4d25-ac67-fb2f24a68e8d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/19/2017
ms.author: roalexan
ms.openlocfilehash: 65eff3f4971f79886a840bb19bf76aaab48878de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="learn-how-to-manage-azureml-web-services-using-api-management"></a><span data-ttu-id="e734f-104">Dowiedz się, jak zarządzać usługami sieci Web Azure ML za pomocą usługi API Management</span><span class="sxs-lookup"><span data-stu-id="e734f-104">Learn how to manage AzureML web services using API Management</span></span>
## <a name="overview"></a><span data-ttu-id="e734f-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e734f-105">Overview</span></span>
<span data-ttu-id="e734f-106">W tym przewodniku przedstawiono sposób szybkie rozpoczęcie pracy przy użyciu interfejsu API zarządzania do zarządzania usługami sieci web uczenie maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="e734f-106">This guide shows you how to quickly get started using API Management to manage your AzureML web services.</span></span>

## <a name="what-is-azure-api-management"></a><span data-ttu-id="e734f-107">Co to jest usługa Azure API Management?</span><span class="sxs-lookup"><span data-stu-id="e734f-107">What is Azure API Management?</span></span>
<span data-ttu-id="e734f-108">Zarządzanie interfejsami API Azure jest usługą platformy Azure, która umożliwia zarządzanie punktami końcowymi interfejsu API REST, definiując dostępu użytkownika, ograniczenie i pulpit nawigacyjny monitorowania.</span><span class="sxs-lookup"><span data-stu-id="e734f-108">Azure API Management is an Azure service that lets you manage your REST API endpoints by defining user access, usage throttling, and dashboard monitoring.</span></span> <span data-ttu-id="e734f-109">Kliknij przycisk [tutaj](https://azure.microsoft.com/services/api-management/) szczegółowe informacje na temat usługi Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="e734f-109">Click [here](https://azure.microsoft.com/services/api-management/) for details on Azure API Management.</span></span> <span data-ttu-id="e734f-110">Kliknij przycisk [tutaj](../api-management/api-management-get-started.md) Przewodnik na temat rozpocząć pracę z usługą Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="e734f-110">Click [here](../api-management/api-management-get-started.md) for a guide on how to get started with Azure API Management.</span></span> <span data-ttu-id="e734f-111">Inne w tym przewodniku, na podstawie tego przewodnika, dotyczą więcej tematy, w tym konfiguracji powiadomień, warstwy cenowej, Obsługa odpowiedzi, uwierzytelnianie użytkowników, tworzenie produktów, subskrypcji dewelopera i dashboarding użycia.</span><span class="sxs-lookup"><span data-stu-id="e734f-111">This other guide, which this guide is based on, covers more topics, including notification configurations, tier pricing, response handling, user authentication, creating products, developer subscriptions, and usage dashboarding.</span></span>

## <a name="what-is-azureml"></a><span data-ttu-id="e734f-112">Co to jest uczenie maszynowe Azure?</span><span class="sxs-lookup"><span data-stu-id="e734f-112">What is AzureML?</span></span>
<span data-ttu-id="e734f-113">Uczenie maszynowe Azure jest usługą platformy Azure do uczenia maszynowego, która umożliwia łatwe tworzenie, wdrażanie i Udostępnianie zaawansowane metody analizy rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="e734f-113">AzureML is an Azure service for machine learning that enables you to easily build, deploy, and share advanced analytics solutions.</span></span> <span data-ttu-id="e734f-114">Kliknij przycisk [tutaj](https://azure.microsoft.com/services/machine-learning/) szczegółowe informacje na temat uczenie maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="e734f-114">Click [here](https://azure.microsoft.com/services/machine-learning/) for details on AzureML.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e734f-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e734f-115">Prerequisites</span></span>
<span data-ttu-id="e734f-116">Aby ukończyć ten przewodnik, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="e734f-116">To complete this guide, you need:</span></span>

* <span data-ttu-id="e734f-117">Konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e734f-117">An Azure account.</span></span> <span data-ttu-id="e734f-118">Jeśli nie masz konta platformy Azure, kliknij przycisk [tutaj](https://azure.microsoft.com/pricing/free-trial/) szczegółowe informacje na temat tworzenia bezpłatne konto próbne.</span><span class="sxs-lookup"><span data-stu-id="e734f-118">If you don’t have an Azure account, click [here](https://azure.microsoft.com/pricing/free-trial/) for details on how to create a free trial account.</span></span>
* <span data-ttu-id="e734f-119">Konto uczenie maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="e734f-119">An AzureML account.</span></span> <span data-ttu-id="e734f-120">Jeśli nie masz konta uczenie maszynowe Azure, kliknij przycisk [tutaj](https://studio.azureml.net/) szczegółowe informacje na temat tworzenia bezpłatne konto próbne.</span><span class="sxs-lookup"><span data-stu-id="e734f-120">If you don’t have an AzureML account, click [here](https://studio.azureml.net/) for details on how to create a free trial account.</span></span>
* <span data-ttu-id="e734f-121">Obszar roboczy, usługi i api_key do eksperymentu uczenie maszynowe Azure wdrożyć jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="e734f-121">The workspace, service, and api_key for an AzureML experiment deployed as a web service.</span></span> <span data-ttu-id="e734f-122">Kliknij przycisk [tutaj](machine-learning-create-experiment.md) szczegółowe informacje na temat tworzenia eksperymentu uczenie maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="e734f-122">Click [here](machine-learning-create-experiment.md) for details on how to create an AzureML experiment.</span></span> <span data-ttu-id="e734f-123">Kliknij przycisk [tutaj](machine-learning-publish-a-machine-learning-web-service.md) dla szczegółowe informacje na temat wdrażania uczenie maszynowe Azure eksperymentu jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="e734f-123">Click [here](machine-learning-publish-a-machine-learning-web-service.md) for details on how to deploy an AzureML experiment as a web service.</span></span> <span data-ttu-id="e734f-124">Alternatywnie dodatek a. zawiera instrukcje dotyczące sposobu tworzenia i testowanie prostego eksperymentu uczenie maszynowe Azure i wdróż je jako usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="e734f-124">Alternately, Appendix A has instructions for how to create and test a simple AzureML experiment and deploy it as a web service.</span></span>

## <a name="create-an-api-management-instance"></a><span data-ttu-id="e734f-125">Tworzenie wystąpienia usługi API Management</span><span class="sxs-lookup"><span data-stu-id="e734f-125">Create an API Management instance</span></span>
<span data-ttu-id="e734f-126">Poniżej przedstawiono kroki przy użyciu interfejsu API zarządzania do zarządzania usługą sieci web uczenie maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="e734f-126">Below are the steps for using API Management to manage your AzureML web service.</span></span> <span data-ttu-id="e734f-127">Najpierw utwórz wystąpienie usługi.</span><span class="sxs-lookup"><span data-stu-id="e734f-127">First create a service instance.</span></span> <span data-ttu-id="e734f-128">Zaloguj się do [klasyczny Portal](https://manage.windowsazure.com/) i kliknij przycisk **nowy** > **usługi aplikacji** > **zarządzanie interfejsami API** > **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e734f-128">Log in to the [Classic Portal](https://manage.windowsazure.com/) and click **New** > **App Services** > **API Management** > **Create**.</span></span>

![Tworzenie wystąpienia](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

<span data-ttu-id="e734f-130">Określ unikatową **adres URL**.</span><span class="sxs-lookup"><span data-stu-id="e734f-130">Specify a unique **URL**.</span></span> <span data-ttu-id="e734f-131">Ten przewodnik po używa **demoazureml** — należy wybrać inny.</span><span class="sxs-lookup"><span data-stu-id="e734f-131">This guide uses **demoazureml** – you will need to choose something different.</span></span> <span data-ttu-id="e734f-132">W polach **Subskrypcja** i **Region** wybierz wartości odpowiednie dla swojego wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="e734f-132">Choose the desired **Subscription** and **Region** for your service instance.</span></span> <span data-ttu-id="e734f-133">Po wprowadzeniu wybrane opcje, kliknij przycisk Dalej.</span><span class="sxs-lookup"><span data-stu-id="e734f-133">After making your selections, click the next button.</span></span>

![Utwórz usług-1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

<span data-ttu-id="e734f-135">Określ wartość **nazwa organizacji**.</span><span class="sxs-lookup"><span data-stu-id="e734f-135">Specify a value for the **Organization Name**.</span></span> <span data-ttu-id="e734f-136">Ten przewodnik po używa **demoazureml** — należy wybrać inny.</span><span class="sxs-lookup"><span data-stu-id="e734f-136">This guide uses **demoazureml** – you will need to choose something different.</span></span> <span data-ttu-id="e734f-137">Wprowadź adres e-mail w **e-mail administratora** pola.</span><span class="sxs-lookup"><span data-stu-id="e734f-137">Enter your email address in the **administrator e-mail** field.</span></span> <span data-ttu-id="e734f-138">Ten adres e-mail służy do wysyłania powiadomienia z systemu usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="e734f-138">This email address is used for notifications from the API Management system.</span></span>

![Utwórz usług-2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

<span data-ttu-id="e734f-140">Kliknij pole wyboru, aby utworzyć wystąpienie usługi.</span><span class="sxs-lookup"><span data-stu-id="e734f-140">Click the check box to create your service instance.</span></span> <span data-ttu-id="e734f-141">*Trwa maksymalnie 30 minut do utworzenia nowej usługi*.</span><span class="sxs-lookup"><span data-stu-id="e734f-141">*It takes up to thirty minutes for a new service to be created*.</span></span>

## <a name="create-the-api"></a><span data-ttu-id="e734f-142">Utwórz ten interfejs API</span><span class="sxs-lookup"><span data-stu-id="e734f-142">Create the API</span></span>
<span data-ttu-id="e734f-143">Po utworzeniu wystąpienia usługi, następnym krokiem jest utworzenie interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="e734f-143">Once the service instance is created, the next step is to create the API.</span></span> <span data-ttu-id="e734f-144">Interfejs API składa się z zestawu operacji, które mogą być wywoływane z poziomu aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="e734f-144">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="e734f-145">Operacje interfejsu API są przekierowywane do istniejących usług sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e734f-145">API operations are proxied to existing web services.</span></span> <span data-ttu-id="e734f-146">Ten przewodnik utworzy interfejsów API czy serwera proxy do istniejących usług sieci web uczenie maszynowe Azure rekordy zasobów i usługi BES.</span><span class="sxs-lookup"><span data-stu-id="e734f-146">This guide creates APIs that proxy to the existing AzureML RRS and BES web services.</span></span>

<span data-ttu-id="e734f-147">Interfejsy API są tworzone i skonfigurować w portalu wydawcy interfejsu API, który jest dostępny za pośrednictwem klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e734f-147">APIs are created and configured from the API publisher portal, which is accessed through the Azure Classic Portal.</span></span> <span data-ttu-id="e734f-148">Aby uzyskać dostęp do portalu wydawcy, wybierz wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="e734f-148">To reach the publisher portal, select your service instance.</span></span>

![Wybierz usługę wystąpienia](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

<span data-ttu-id="e734f-150">Kliknij przycisk **Zarządzaj** w klasycznym portalu Azure usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="e734f-150">Click **Manage** in the Azure Classic Portal for your API Management service.</span></span>

![Usługa zarządzania](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

<span data-ttu-id="e734f-152">Kliknij przycisk **interfejsów API** z **zarządzanie interfejsami API** menu po lewej stronie, a następnie kliknij przycisk **dodać interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="e734f-152">Click **APIs** from the **API Management** menu on the left, and then click **Add API**.</span></span>

![Interfejs API zarządzania menu](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

<span data-ttu-id="e734f-154">Typ **API pokaz uczenie maszynowe Azure** jako **Nazwa interfejsu API sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="e734f-154">Type **AzureML Demo API** as the **Web API name**.</span></span> <span data-ttu-id="e734f-155">Typ **https://ussouthcentral.services.azureml.net** jako **adres URL usługi sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="e734f-155">Type **https://ussouthcentral.services.azureml.net** as the **Web service URL**.</span></span> <span data-ttu-id="e734f-156">Typ **pokaz uczenie maszynowe Azure** jako **sufiks adresu URL interfejsu API sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="e734f-156">Type **azureml-demo** as the **Web API URL suffix**.</span></span> <span data-ttu-id="e734f-157">Sprawdź **HTTPS** jako **adres URL interfejsu API sieci Web** schematu.</span><span class="sxs-lookup"><span data-stu-id="e734f-157">Check **HTTPS** as the **Web API URL** scheme.</span></span> <span data-ttu-id="e734f-158">Wybierz **Starter** jako **produkty**.</span><span class="sxs-lookup"><span data-stu-id="e734f-158">Select **Starter** as **Products**.</span></span> <span data-ttu-id="e734f-159">Gdy skończysz, kliknij przycisk **zapisać** do tworzenia interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="e734f-159">When finished, click **Save** to create the API.</span></span>

![Dodaj — nowy — interfejs api](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-the-operations"></a><span data-ttu-id="e734f-161">Dodawanie działań</span><span class="sxs-lookup"><span data-stu-id="e734f-161">Add the operations</span></span>
<span data-ttu-id="e734f-162">Kliknij przycisk **operacji dodawania** do dodawania działań do tego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="e734f-162">Click **Add operation** to add operations to this API.</span></span>

![Dodaj operację](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

<span data-ttu-id="e734f-164">**Nowej operacji** będzie wyświetlane okno i **podpisu** będzie domyślnie wybierany kartę.</span><span class="sxs-lookup"><span data-stu-id="e734f-164">The **New operation** window will be displayed and the **Signature** tab will be selected by default.</span></span>

## <a name="add-rrs-operation"></a><span data-ttu-id="e734f-165">Dodaj operację rekordy zasobów</span><span class="sxs-lookup"><span data-stu-id="e734f-165">Add RRS Operation</span></span>
<span data-ttu-id="e734f-166">Najpierw należy utworzyć operacji dla usługi uczenie maszynowe Azure rekordy zasobów.</span><span class="sxs-lookup"><span data-stu-id="e734f-166">First create an operation for the AzureML RRS service.</span></span> <span data-ttu-id="e734f-167">Wybierz **POST** jako **zlecenie HTTP**.</span><span class="sxs-lookup"><span data-stu-id="e734f-167">Select **POST** as the **HTTP verb**.</span></span> <span data-ttu-id="e734f-168">Typ **/services/ /workspaces/ {obszaru roboczego} {usługi} / execute? api-version = {apiversion} & szczegóły = {szczegóły}** jako **szablon adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="e734f-168">Type **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}** as the **URL template**.</span></span> <span data-ttu-id="e734f-169">Typ **wykonania rekordy zasobów** jako **Nazwa wyświetlana**.</span><span class="sxs-lookup"><span data-stu-id="e734f-169">Type **RRS Execute** as the **Display name**.</span></span>

![Dodawanie rekordów zasobów operacji podpisu](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

<span data-ttu-id="e734f-171">Kliknij przycisk **odpowiedzi** > **dodać** po lewej i wybierz **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="e734f-171">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="e734f-172">Kliknij przycisk **zapisać** można zapisać tej operacji.</span><span class="sxs-lookup"><span data-stu-id="e734f-172">Click **Save** to save this operation.</span></span>

![Dodawanie rekordów zasobów operacji odpowiedzi](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a><span data-ttu-id="e734f-174">Dodaj BES operacji</span><span class="sxs-lookup"><span data-stu-id="e734f-174">Add BES Operations</span></span>
<span data-ttu-id="e734f-175">Zrzuty ekranu nie są włączone dla operacji usługi BES, ponieważ są one bardzo podobne do tych rekordów zasobów operacji dodawania.</span><span class="sxs-lookup"><span data-stu-id="e734f-175">Screenshots are not included for the BES operations as they are very similar to those for adding the RRS operation.</span></span>

### <a name="submit-but-not-start-a-batch-execution-job"></a><span data-ttu-id="e734f-176">Przesyłanie (ale nie start) zadanie wsadowe</span><span class="sxs-lookup"><span data-stu-id="e734f-176">Submit (but not start) a Batch Execution job</span></span>
<span data-ttu-id="e734f-177">Kliknij przycisk **operacji dodawania** można dodać operacji BES uczenie maszynowe Azure do interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="e734f-177">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="e734f-178">Wybierz **POST** dla **zlecenie HTTP**.</span><span class="sxs-lookup"><span data-stu-id="e734f-178">Select **POST** for the **HTTP verb**.</span></span> <span data-ttu-id="e734f-179">Typ **/services/ /workspaces/ {obszaru roboczego} {usługi} / zadania? api-version = {apiversion}** dla **szablon adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="e734f-179">Type **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="e734f-180">Typ **przesłać BES** dla **Nazwa wyświetlana**.</span><span class="sxs-lookup"><span data-stu-id="e734f-180">Type **BES Submit** for the **Display name**.</span></span> <span data-ttu-id="e734f-181">Kliknij przycisk **odpowiedzi** > **dodać** po lewej i wybierz **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="e734f-181">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="e734f-182">Kliknij przycisk **zapisać** można zapisać tej operacji.</span><span class="sxs-lookup"><span data-stu-id="e734f-182">Click **Save** to save this operation.</span></span>

### <a name="start-a-batch-execution-job"></a><span data-ttu-id="e734f-183">Uruchom zadanie wsadowe</span><span class="sxs-lookup"><span data-stu-id="e734f-183">Start a Batch Execution job</span></span>
<span data-ttu-id="e734f-184">Kliknij przycisk **operacji dodawania** można dodać operacji BES uczenie maszynowe Azure do interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="e734f-184">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="e734f-185">Wybierz **POST** dla **zlecenie HTTP**.</span><span class="sxs-lookup"><span data-stu-id="e734f-185">Select **POST** for the **HTTP verb**.</span></span> <span data-ttu-id="e734f-186">Typ **/jobs/ /services/ {usługi} /workspaces/ {obszaru roboczego} {jobid} / start? api-version = {apiversion}** dla **szablon adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="e734f-186">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="e734f-187">Typ **BES Start** dla **Nazwa wyświetlana**.</span><span class="sxs-lookup"><span data-stu-id="e734f-187">Type **BES Start** for the **Display name**.</span></span> <span data-ttu-id="e734f-188">Kliknij przycisk **odpowiedzi** > **dodać** po lewej i wybierz **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="e734f-188">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="e734f-189">Kliknij przycisk **zapisać** można zapisać tej operacji.</span><span class="sxs-lookup"><span data-stu-id="e734f-189">Click **Save** to save this operation.</span></span>

### <a name="get-the-status-or-result-of-a-batch-execution-job"></a><span data-ttu-id="e734f-190">Pobierz stan lub wyniku zadania wsadowe</span><span class="sxs-lookup"><span data-stu-id="e734f-190">Get the status or result of a Batch Execution job</span></span>
<span data-ttu-id="e734f-191">Kliknij przycisk **operacji dodawania** można dodać operacji BES uczenie maszynowe Azure do interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="e734f-191">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="e734f-192">Wybierz **UZYSKAĆ** dla **zlecenie HTTP**.</span><span class="sxs-lookup"><span data-stu-id="e734f-192">Select **GET** for the **HTTP verb**.</span></span> <span data-ttu-id="e734f-193">Typ **/jobs/ /services/ {usługi} /workspaces/ {obszaru roboczego} {jobid}? api-version = {apiversion}** dla **szablon adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="e734f-193">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="e734f-194">Typ **stanu usługi BES** dla **Nazwa wyświetlana**.</span><span class="sxs-lookup"><span data-stu-id="e734f-194">Type **BES Status** for the **Display name**.</span></span> <span data-ttu-id="e734f-195">Kliknij przycisk **odpowiedzi** > **dodać** po lewej i wybierz **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="e734f-195">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="e734f-196">Kliknij przycisk **zapisać** można zapisać tej operacji.</span><span class="sxs-lookup"><span data-stu-id="e734f-196">Click **Save** to save this operation.</span></span>

### <a name="delete-a-batch-execution-job"></a><span data-ttu-id="e734f-197">Usuń zadanie wsadowe</span><span class="sxs-lookup"><span data-stu-id="e734f-197">Delete a Batch Execution job</span></span>
<span data-ttu-id="e734f-198">Kliknij przycisk **operacji dodawania** można dodać operacji BES uczenie maszynowe Azure do interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="e734f-198">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="e734f-199">Wybierz **usunąć** dla **zlecenie HTTP**.</span><span class="sxs-lookup"><span data-stu-id="e734f-199">Select **DELETE** for the **HTTP verb**.</span></span> <span data-ttu-id="e734f-200">Typ **/jobs/ /services/ {usługi} /workspaces/ {obszaru roboczego} {jobid}? api-version = {apiversion}** dla **szablon adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="e734f-200">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="e734f-201">Typ **usunąć BES** dla **Nazwa wyświetlana**.</span><span class="sxs-lookup"><span data-stu-id="e734f-201">Type **BES Delete** for the **Display name**.</span></span> <span data-ttu-id="e734f-202">Kliknij przycisk **odpowiedzi** > **dodać** po lewej i wybierz **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="e734f-202">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="e734f-203">Kliknij przycisk **zapisać** można zapisać tej operacji.</span><span class="sxs-lookup"><span data-stu-id="e734f-203">Click **Save** to save this operation.</span></span>

## <a name="call-an-operation-from-the-developer-portal"></a><span data-ttu-id="e734f-204">Wywoływanie operacji z portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="e734f-204">Call an operation from the Developer Portal</span></span>
<span data-ttu-id="e734f-205">Operacje można wywołać bezpośrednio z portalu dla deweloperów, które oferują wygodny sposób, aby wyświetlić i przetestować operacje interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="e734f-205">Operations can be called directly from the Developer portal, which provides a convenient way to view and test the operations of an API.</span></span> <span data-ttu-id="e734f-206">W tym kroku przewodnik wywoła **wykonania rekordy zasobów** metody, która została dodana do **API pokaz uczenie maszynowe Azure**.</span><span class="sxs-lookup"><span data-stu-id="e734f-206">In this guide step you will call the **RRS Execute** method that was added to the **AzureML Demo API**.</span></span> <span data-ttu-id="e734f-207">Kliknij przycisk **portalu dla deweloperów** w menu u góry po prawej z klasycznego portalu.</span><span class="sxs-lookup"><span data-stu-id="e734f-207">Click **Developer portal** from the menu at the top right of the Classic Portal.</span></span>

![portalu dla deweloperów](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

<span data-ttu-id="e734f-209">Kliknij przycisk **interfejsów API** z menu u góry, a następnie kliknij przycisk **API pokaz uczenie maszynowe Azure** Aby wyświetlić dostępne operacje.</span><span class="sxs-lookup"><span data-stu-id="e734f-209">Click **APIs** from the top menu, and then click **AzureML Demo API** to see the operations available.</span></span>

![Interfejs api demoazureml](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

<span data-ttu-id="e734f-211">Wybierz **wykonania rekordy zasobów** dla tej operacji.</span><span class="sxs-lookup"><span data-stu-id="e734f-211">Select **RRS Execute** for the operation.</span></span> <span data-ttu-id="e734f-212">Kliknij przycisk **wypróbuj**.</span><span class="sxs-lookup"><span data-stu-id="e734f-212">Click **Try It**.</span></span>

![try it](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

<span data-ttu-id="e734f-214">Żądanie parametru, wpisz sieci **obszaru roboczego**, **usługi**, **2.0** dla **apiversion**, i **true** dla **szczegóły**.</span><span class="sxs-lookup"><span data-stu-id="e734f-214">For Request parameters, type your **workspace**,  **service**, **2.0** for the **apiversion**, and  **true** for the **details**.</span></span> <span data-ttu-id="e734f-215">Można znaleźć sieci **obszaru roboczego** i **usługi** na pulpicie nawigacyjnym usługi sieci web uczenie maszynowe Azure (zobacz **przetestować usługę sieci web** w dodatku A).</span><span class="sxs-lookup"><span data-stu-id="e734f-215">You can find your **workspace** and **service** in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span></span>

<span data-ttu-id="e734f-216">Dla nagłówków żądań, kliknij przycisk **Dodaj nagłówek** i typ **Content-Type** i **application/json**, następnie kliknij przycisk **Dodaj nagłówek** i typ **autoryzacji** i **elementu nośnego <YOUR AZUREML SERVICE API-KEY>** .</span><span class="sxs-lookup"><span data-stu-id="e734f-216">For Request headers, click **Add header** and type **Content-Type** and **application/json**, then click **Add header** and type **Authorization** and **Bearer <YOUR AZUREML SERVICE API-KEY>**.</span></span> <span data-ttu-id="e734f-217">Można znaleźć sieci **klucz interfejsu api** na pulpicie nawigacyjnym usługi sieci web uczenie maszynowe Azure (zobacz **przetestować usługę sieci web** w dodatku A).</span><span class="sxs-lookup"><span data-stu-id="e734f-217">You can find your **api key** in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span></span>

<span data-ttu-id="e734f-218">Typ **{"Dane wejściowe": {"input1": {"ColumnNames": ["Col2"] "wartości": [["jest to dobry dzień"]]}}, "GlobalParameters": {}}** dla treści żądania.</span><span class="sxs-lookup"><span data-stu-id="e734f-218">Type **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}** for the request body.</span></span>

![uczenie maszynowe Azure pokaz api](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

<span data-ttu-id="e734f-220">Kliknij przycisk **wysyłania**.</span><span class="sxs-lookup"><span data-stu-id="e734f-220">Click **Send**.</span></span>

![Wyślij](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

<span data-ttu-id="e734f-222">Po wywołaniu operacji portalu dla deweloperów Wyświetla **żądany adres URL** usługi zaplecza **stanu odpowiedzi**, **nagłówki odpowiedzi**, natomiast dla ustawienia **zawartości odpowiedzi**.</span><span class="sxs-lookup"><span data-stu-id="e734f-222">After an operation is invoked, the developer portal displays the **Requested URL** from the back-end service, the **Response status**, the **Response headers**, and any **Response content**.</span></span>

![Stan odpowiedzi](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a><span data-ttu-id="e734f-224">Dodatek A — tworzenie i testowanie prostego uczenie maszynowe Azure usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="e734f-224">Appendix A - Creating and testing a simple AzureML web service</span></span>
### <a name="creating-the-experiment"></a><span data-ttu-id="e734f-225">Tworzenie eksperymentu</span><span class="sxs-lookup"><span data-stu-id="e734f-225">Creating the experiment</span></span>
<span data-ttu-id="e734f-226">Poniżej przedstawiono procedurę tworzenia prostego eksperymentu uczenie maszynowe Azure i wdrażania go w postaci usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="e734f-226">Below are the steps for creating a simple AzureML experiment and deploying it as a web service.</span></span> <span data-ttu-id="e734f-227">Pobiera usługi sieci web, jakie danych wejściowych z kolumną zawierającą dowolnego tekstu i zwraca zestaw funkcji reprezentowane jako wartości całkowite.</span><span class="sxs-lookup"><span data-stu-id="e734f-227">The web service takes as input a column of arbitrary text and returns a set of features represented as integers.</span></span> <span data-ttu-id="e734f-228">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e734f-228">For example:</span></span>

| <span data-ttu-id="e734f-229">Tekst</span><span class="sxs-lookup"><span data-stu-id="e734f-229">Text</span></span> | <span data-ttu-id="e734f-230">Tekst w formie skrótu</span><span class="sxs-lookup"><span data-stu-id="e734f-230">Hashed Text</span></span> |
| --- | --- |
| <span data-ttu-id="e734f-231">Jest to dobry dzień</span><span class="sxs-lookup"><span data-stu-id="e734f-231">This is a good day</span></span> |<span data-ttu-id="e734f-232">1 1 2 2 0 2 0 1</span><span class="sxs-lookup"><span data-stu-id="e734f-232">1 1 2 2 0 2 0 1</span></span> |

<span data-ttu-id="e734f-233">Po pierwsze, za pomocą przeglądarki wybranych przez użytkownika, przejdź do: [https://studio.azureml.net/](https://studio.azureml.net/) i wprowadź swoje poświadczenia, aby się zalogować.</span><span class="sxs-lookup"><span data-stu-id="e734f-233">First, using a browser of your choice, navigate to: [https://studio.azureml.net/](https://studio.azureml.net/) and enter your credentials to log in.</span></span> <span data-ttu-id="e734f-234">Następnie należy utworzyć nowy eksperyment puste.</span><span class="sxs-lookup"><span data-stu-id="e734f-234">Next, create a new blank experiment.</span></span>

![Wyszukiwanie — eksperymentu — szablony](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

<span data-ttu-id="e734f-236">Zmienić jego nazwę na **SimpleFeatureHashingExperiment**.</span><span class="sxs-lookup"><span data-stu-id="e734f-236">Rename it to **SimpleFeatureHashingExperiment**.</span></span> <span data-ttu-id="e734f-237">Rozwiń węzeł **zapisane zestawów danych** i przeciągnij **przeglądami książki z Amazon** na eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="e734f-237">Expand **Saved Datasets** and drag **Book Reviews from Amazon** onto your experiment.</span></span>

![prosty — funkcja mieszania eksperymentu](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

<span data-ttu-id="e734f-239">Rozwiń węzeł **transformacji danych** i **manipulowania** i przeciągnij **Select Columns in Dataset** na eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="e734f-239">Expand **Data Transformation** and **Manipulation** and drag **Select Columns in Dataset** onto your experiment.</span></span> <span data-ttu-id="e734f-240">Połącz **skoroszyt z usługi Amazon przeglądami** do **Wybieranie kolumn w zestawie danych**.</span><span class="sxs-lookup"><span data-stu-id="e734f-240">Connect **Book Reviews from Amazon** to **Select Columns in Dataset**.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

<span data-ttu-id="e734f-242">Kliknij przycisk **Select Columns in Dataset** , a następnie kliknij przycisk **Uruchom selektor kolumn** i wybierz **Col2**.</span><span class="sxs-lookup"><span data-stu-id="e734f-242">Click **Select Columns in Dataset** and then click **Launch column selector** and select **Col2**.</span></span> <span data-ttu-id="e734f-243">Kliknij znacznik wyboru, aby zastosować te zmiany.</span><span class="sxs-lookup"><span data-stu-id="e734f-243">Click the checkmark to apply these changes.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

<span data-ttu-id="e734f-245">Rozwiń węzeł **Analiza tekstu** i przeciągnij **Tworzenie skrótu funkcji** na eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="e734f-245">Expand **Text Analytics** and drag **Feature Hashing** onto the experiment.</span></span> <span data-ttu-id="e734f-246">Połącz **Wybieranie kolumn w zestawie danych** do **Tworzenie skrótu funkcji**.</span><span class="sxs-lookup"><span data-stu-id="e734f-246">Connect **Select Columns in Dataset** to **Feature Hashing**.</span></span>

![Connect--kolumny projektu](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

<span data-ttu-id="e734f-248">Typ **3** dla **mieszania bitsize**.</span><span class="sxs-lookup"><span data-stu-id="e734f-248">Type **3** for the **Hashing bitsize**.</span></span> <span data-ttu-id="e734f-249">Spowoduje to utworzenie 8 (23) kolumny.</span><span class="sxs-lookup"><span data-stu-id="e734f-249">This will create 8 (23) columns.</span></span>

![Tworzenie skrótów bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

<span data-ttu-id="e734f-251">W tym momencie można kliknąć przycisk **Uruchom** do testowania eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="e734f-251">At this point, you may want to click **Run** to test the experiment.</span></span>

![Uruchom](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a><span data-ttu-id="e734f-253">Tworzenie usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="e734f-253">Create a web service</span></span>
<span data-ttu-id="e734f-254">Teraz Utwórz usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="e734f-254">Now create a web service.</span></span> <span data-ttu-id="e734f-255">Rozwiń węzeł **usługi sieci Web** i przeciągnij **dane wejściowe** na eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="e734f-255">Expand **Web Service** and drag **Input** onto your experiment.</span></span> <span data-ttu-id="e734f-256">Połącz **dane wejściowe** do **Tworzenie skrótu funkcji**.</span><span class="sxs-lookup"><span data-stu-id="e734f-256">Connect **Input** to **Feature Hashing**.</span></span> <span data-ttu-id="e734f-257">Przeciągnij również **dane wyjściowe** na eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="e734f-257">Also drag **output** onto your experiment.</span></span> <span data-ttu-id="e734f-258">Połącz **dane wyjściowe** do **Tworzenie skrótu funkcji**.</span><span class="sxs-lookup"><span data-stu-id="e734f-258">Connect **Output** to **Feature Hashing**.</span></span>

![dane wyjściowe do-— Tworzenie skrótu funkcji](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

<span data-ttu-id="e734f-260">Kliknij przycisk **opublikować usługi sieci web**.</span><span class="sxs-lookup"><span data-stu-id="e734f-260">Click **Publish web service**.</span></span>

![Publikowanie — Usługa sieci web](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

<span data-ttu-id="e734f-262">Kliknij przycisk **tak** publikowania eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="e734f-262">Click **Yes** to publish the experiment.</span></span>

![tak aby opublikować](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-the-web-service"></a><span data-ttu-id="e734f-264">Testowanie usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="e734f-264">Test the web service</span></span>
<span data-ttu-id="e734f-265">Usługi sieci web uczenie maszynowe Azure składa się z punktów końcowych (usługi wykonywania wsadowego) BES i RSS (żądania/odpowiedzi usługi).</span><span class="sxs-lookup"><span data-stu-id="e734f-265">An AzureML web service consists of RSS (request/response service) and BES (batch execution service) endpoints.</span></span> <span data-ttu-id="e734f-266">Funkcja RSS jest synchroniczne wykonywania.</span><span class="sxs-lookup"><span data-stu-id="e734f-266">RSS is for synchronous execution.</span></span> <span data-ttu-id="e734f-267">BES jest do wykonywania zadań asynchronicznych.</span><span class="sxs-lookup"><span data-stu-id="e734f-267">BES is for asynchronous job execution.</span></span> <span data-ttu-id="e734f-268">Aby przetestować usługi sieci web ze źródłem Python próbki poniżej, konieczne może być Pobierz i zainstaluj zestaw Azure SDK dla języka Python (zobacz: [sposób instalowania Python](../python-how-to-install.md)).</span><span class="sxs-lookup"><span data-stu-id="e734f-268">To test your web service with the sample Python source below, you may need to download and install the Azure SDK for Python (see: [How to install Python](../python-how-to-install.md)).</span></span>

<span data-ttu-id="e734f-269">Należy również **obszaru roboczego**, **usługi**, i **api_key** eksperymentu źródła próbki poniżej.</span><span class="sxs-lookup"><span data-stu-id="e734f-269">You will also need the **workspace**, **service**, and **api_key** of your experiment for the sample source below.</span></span> <span data-ttu-id="e734f-270">Obszar roboczy i usługi można znaleźć, klikając opcję **żądanie/odpowiedź** lub **Batch Execution** swojego eksperymentu w pulpicie nawigacyjnym usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="e734f-270">You can find the workspace and service by clicking either **Request/Response** or **Batch Execution** for your experiment in the web service dashboard.</span></span>

![Znajdź obszar roboczy i usługi](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

<span data-ttu-id="e734f-272">Można znaleźć **api_key** klikając eksperymentu w pulpicie nawigacyjnym usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="e734f-272">You can find the **api_key** by clicking your experiment in the web service dashboard.</span></span>

![Znajdź api-key](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a><span data-ttu-id="e734f-274">Punkt końcowy RR testu</span><span class="sxs-lookup"><span data-stu-id="e734f-274">Test RRS endpoint</span></span>
##### <a name="test-button"></a><span data-ttu-id="e734f-275">Przycisk Testuj</span><span class="sxs-lookup"><span data-stu-id="e734f-275">Test button</span></span>
<span data-ttu-id="e734f-276">Łatwe testowanie punktu końcowego rekordy zasobów jest kliknięcie **testu** na pulpicie nawigacyjnym usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="e734f-276">An easy way to test the RRS endpoint is to click **Test** on the web service dashboard.</span></span>

![Test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

<span data-ttu-id="e734f-278">Typ **to dobry dzień** dla **col2**.</span><span class="sxs-lookup"><span data-stu-id="e734f-278">Type **This is a good day** for **col2**.</span></span> <span data-ttu-id="e734f-279">Kliknij znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="e734f-279">Click the checkmark.</span></span>

![Wprowadź dane](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

<span data-ttu-id="e734f-281">Zobaczysz ekran podobny do</span><span class="sxs-lookup"><span data-stu-id="e734f-281">You will see something like</span></span>

![Przykładowe wyniki](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a><span data-ttu-id="e734f-283">Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="e734f-283">Sample Code</span></span>
<span data-ttu-id="e734f-284">Innym sposobem sprawdzenia Twoje rekordy zasobów jest z kodu klienta.</span><span class="sxs-lookup"><span data-stu-id="e734f-284">Another way to test your RRS is from your client code.</span></span> <span data-ttu-id="e734f-285">Jeśli klikniesz przycisk **żądania/odpowiedzi** na pulpicie nawigacyjnym i przewiń w dół, zostanie wyświetlone przykładowego kodu dla C#, Python i R. Można również wyświetlić składnię żądania rekordów zasobów, w tym żądaniu identyfikatora URI, nagłówków i treść.</span><span class="sxs-lookup"><span data-stu-id="e734f-285">If you click **Request/response** on the dashboard and scroll to the bottom, you will see sample code for C#, Python, and R. You will also see the syntax of the RRS request, including the request URI, headers, and body.</span></span>

<span data-ttu-id="e734f-286">Ten przewodnik zawiera pracy przykład Python.</span><span class="sxs-lookup"><span data-stu-id="e734f-286">This guide shows a working Python example.</span></span> <span data-ttu-id="e734f-287">Konieczne będzie jej modyfikowania **obszaru roboczego**, **usługi**, i **api_key** eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="e734f-287">You will need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span></span>

    import urllib2
    import json
    workspace = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE WORKSPACE ID>"
    service = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE SERVICE ID>"
    api_key = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE API KEY>"
    data = {
    "Inputs": {
        "input1": {
            "ColumnNames": ["Col2"],
            "Values": [ [ "This is a good day" ] ]
        },
    },
    "GlobalParameters": { }
    }
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace + "/services/" + service + "/execute?api-version=2.0&details=true"
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}
    body = str.encode(json.dumps(data))
    try:
        req = urllib2.Request(url, body, headers)
        response = urllib2.urlopen(req)
        result = response.read()
        print "result:" + result
            except urllib2.HTTPError, error:
        print("The request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a><span data-ttu-id="e734f-288">Punkt końcowy usługi BES testu</span><span class="sxs-lookup"><span data-stu-id="e734f-288">Test BES endpoint</span></span>
<span data-ttu-id="e734f-289">Kliknij przycisk **wykonywanie wsadowe** na pulpicie nawigacyjnym i przewiń w dół.</span><span class="sxs-lookup"><span data-stu-id="e734f-289">Click **Batch execution** on the dashboard and scroll to the bottom.</span></span> <span data-ttu-id="e734f-290">Zostanie wyświetlone przykładowego kodu dla C#, Python i R. Widoczne będzie także składnia żądania BES do przesyłania zadania, uruchomić zadanie pobieranie stanu lub wyniki zadania i usunąć zadania.</span><span class="sxs-lookup"><span data-stu-id="e734f-290">You will see sample code for C#, Python, and R. You will also see the syntax of the BES requests to submit a job, start a job, get the status or results of a job, and delete a job.</span></span>

<span data-ttu-id="e734f-291">Ten przewodnik zawiera pracy przykład Python.</span><span class="sxs-lookup"><span data-stu-id="e734f-291">This guide shows a working Python example.</span></span> <span data-ttu-id="e734f-292">Należy zmodyfikować za pomocą **obszaru roboczego**, **usługi**, i **api_key** eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="e734f-292">You need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span></span> <span data-ttu-id="e734f-293">Ponadto należy zmodyfikować **nazwy konta magazynu**, **klucz konta magazynu**, i **nazwa kontenera magazynu**.</span><span class="sxs-lookup"><span data-stu-id="e734f-293">Additionally, you need to modify the **storage account name**, **storage account key**, and **storage container name**.</span></span> <span data-ttu-id="e734f-294">Ponadto należy zmodyfikować lokalizację **pliku wejściowego** i lokalizację **pliku wyjściowego**.</span><span class="sxs-lookup"><span data-stu-id="e734f-294">Lastly, you will need to modify the location of the **input file** and the location of the **output file**.</span></span>

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH THE API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH THE LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH THE LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("The request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading the result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written to the file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("The results for " + outputName + " are available at the following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "The results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading the input to blob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded the input to blob storage"
    input_blob_path = "/" + storage_container_name + "/" + input_blob_name
    connection_string = "DefaultEndpointsProtocol=https;AccountName=" + storage_account_name + ";AccountKey=" + storage_account_key
    payload =  {
        "Input": {
            "ConnectionString": connection_string,
            "RelativeLocation": input_blob_path
        },
        "Outputs": {
            "output1": { "ConnectionString": connection_string, "RelativeLocation": "/" + storage_container_name + "/" + output_blob_name },
        },
        "GlobalParameters": {
        }
    }
        body = str.encode(json.dumps(payload))
    headers = { "Content-Type":"application/json", "Authorization":("Bearer " + api_key)}
    print("Submitting the job...")
    # submit the job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove the enclosing double-quotes
    print("Job ID: " + job_id)
    # start the job
    print("Starting the job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking the job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in the follwing code
        req = urllib2.Request(url2, headers = { "Authorization":("Bearer " + api_key) })
        try:
            response = urllib2.urlopen(req)
        except urllib2.HTTPError, error:
            printHttpError(error)
            return
        result = json.loads(response.read())
        status = result["StatusCode"]
        print "status:" + status
        if (status == 0 or status == "NotStarted"):
            print("Job " + job_id + " not yet started...")
        elif (status == 1 or status == "Running"):
            print("Job " + job_id + " running...")
        elif (status == 2 or status == "Failed"):
            print("Job " + job_id + " failed!")
            print("Error details: " + result["Details"])
            break
        elif (status == 3 or status == "Cancelled"):
            print("Job " + job_id + " cancelled!")
            break
        elif (status == 4 or status == "Finished"):
            print("Job " + job_id + " finished!")
            processResults(result)
            break
        time.sleep(1) # wait one second
    return
    invokeBatchExecutionService()
