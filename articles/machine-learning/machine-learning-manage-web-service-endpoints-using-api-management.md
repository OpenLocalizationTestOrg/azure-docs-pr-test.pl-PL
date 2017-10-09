---
title: "jak toomanage uczenie maszynowe Azure w sieci web usług przy użyciu interfejsu API zarządzania aaaLearn | Dokumentacja firmy Microsoft"
description: "Przewodnik pokazujący sposób toomanage uczenie maszynowe Azure w sieci web usług przy użyciu interfejsu API zarządzania."
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
ms.openlocfilehash: 6e764fbfd71be6cc908a1c8d3d8889969fc651a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="learn-how-toomanage-azureml-web-services-using-api-management"></a><span data-ttu-id="37ea7-104">Dowiedz się, jak toomanage uczenie maszynowe Azure w sieci web usług przy użyciu interfejsu API zarządzania</span><span class="sxs-lookup"><span data-stu-id="37ea7-104">Learn how toomanage AzureML web services using API Management</span></span>
## <a name="overview"></a><span data-ttu-id="37ea7-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="37ea7-105">Overview</span></span>
<span data-ttu-id="37ea7-106">W tym przewodniku przedstawiono sposób tooquickly rozpoczęcie pracy z toomanage zarządzanie interfejsami API usług sieci web uczenie maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="37ea7-106">This guide shows you how tooquickly get started using API Management toomanage your AzureML web services.</span></span>

## <a name="what-is-azure-api-management"></a><span data-ttu-id="37ea7-107">Co to jest usługa Azure API Management?</span><span class="sxs-lookup"><span data-stu-id="37ea7-107">What is Azure API Management?</span></span>
<span data-ttu-id="37ea7-108">Zarządzanie interfejsami API Azure jest usługą platformy Azure, która umożliwia zarządzanie punktami końcowymi interfejsu API REST, definiując dostępu użytkownika, ograniczenie i pulpit nawigacyjny monitorowania.</span><span class="sxs-lookup"><span data-stu-id="37ea7-108">Azure API Management is an Azure service that lets you manage your REST API endpoints by defining user access, usage throttling, and dashboard monitoring.</span></span> <span data-ttu-id="37ea7-109">Kliknij przycisk [tutaj](https://azure.microsoft.com/services/api-management/) szczegółowe informacje na temat usługi Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="37ea7-109">Click [here](https://azure.microsoft.com/services/api-management/) for details on Azure API Management.</span></span> <span data-ttu-id="37ea7-110">Kliknij przycisk [tutaj](../api-management/api-management-get-started.md) przewodnik, w jaki sposób tooget wprowadzenie do usługi Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="37ea7-110">Click [here](../api-management/api-management-get-started.md) for a guide on how tooget started with Azure API Management.</span></span> <span data-ttu-id="37ea7-111">Inne w tym przewodniku, na podstawie tego przewodnika, dotyczą więcej tematy, w tym konfiguracji powiadomień, warstwy cenowej, Obsługa odpowiedzi, uwierzytelnianie użytkowników, tworzenie produktów, subskrypcji dewelopera i dashboarding użycia.</span><span class="sxs-lookup"><span data-stu-id="37ea7-111">This other guide, which this guide is based on, covers more topics, including notification configurations, tier pricing, response handling, user authentication, creating products, developer subscriptions, and usage dashboarding.</span></span>

## <a name="what-is-azureml"></a><span data-ttu-id="37ea7-112">Co to jest uczenie maszynowe Azure?</span><span class="sxs-lookup"><span data-stu-id="37ea7-112">What is AzureML?</span></span>
<span data-ttu-id="37ea7-113">Uczenie maszynowe Azure jest usługą platformy Azure do uczenia maszynowego, umożliwiający tooeasily kompilacji, wdrażanie i Udostępnianie zaawansowane metody analizy rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="37ea7-113">AzureML is an Azure service for machine learning that enables you tooeasily build, deploy, and share advanced analytics solutions.</span></span> <span data-ttu-id="37ea7-114">Kliknij przycisk [tutaj](https://azure.microsoft.com/services/machine-learning/) szczegółowe informacje na temat uczenie maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="37ea7-114">Click [here](https://azure.microsoft.com/services/machine-learning/) for details on AzureML.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37ea7-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="37ea7-115">Prerequisites</span></span>
<span data-ttu-id="37ea7-116">toocomplete tego przewodnika należy:</span><span class="sxs-lookup"><span data-stu-id="37ea7-116">toocomplete this guide, you need:</span></span>

* <span data-ttu-id="37ea7-117">Konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="37ea7-117">An Azure account.</span></span> <span data-ttu-id="37ea7-118">Jeśli nie masz konta platformy Azure, kliknij przycisk [tutaj](https://azure.microsoft.com/pricing/free-trial/) szczegółowe informacje na temat toocreate bezpłatne konto próbne.</span><span class="sxs-lookup"><span data-stu-id="37ea7-118">If you don’t have an Azure account, click [here](https://azure.microsoft.com/pricing/free-trial/) for details on how toocreate a free trial account.</span></span>
* <span data-ttu-id="37ea7-119">Konto uczenie maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="37ea7-119">An AzureML account.</span></span> <span data-ttu-id="37ea7-120">Jeśli nie masz konta uczenie maszynowe Azure, kliknij przycisk [tutaj](https://studio.azureml.net/) szczegółowe informacje na temat toocreate bezpłatne konto próbne.</span><span class="sxs-lookup"><span data-stu-id="37ea7-120">If you don’t have an AzureML account, click [here](https://studio.azureml.net/) for details on how toocreate a free trial account.</span></span>
* <span data-ttu-id="37ea7-121">obszar roboczy Hello, usługi i api_key do eksperymentu uczenie maszynowe Azure wdrożyć jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="37ea7-121">hello workspace, service, and api_key for an AzureML experiment deployed as a web service.</span></span> <span data-ttu-id="37ea7-122">Kliknij przycisk [tutaj](machine-learning-create-experiment.md) szczegółowe informacje na temat sposobu eksperymentu toocreate uczenie maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="37ea7-122">Click [here](machine-learning-create-experiment.md) for details on how toocreate an AzureML experiment.</span></span> <span data-ttu-id="37ea7-123">Kliknij przycisk [tutaj](machine-learning-publish-a-machine-learning-web-service.md) szczegółowe informacje na temat sposobu toodeploy uczenie maszynowe Azure eksperymentu jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="37ea7-123">Click [here](machine-learning-publish-a-machine-learning-web-service.md) for details on how toodeploy an AzureML experiment as a web service.</span></span> <span data-ttu-id="37ea7-124">Alternatywnie dodatek a. zawiera instrukcje dotyczące sposobu toocreate i testowania proste uczenie maszynowe Azure eksperymentu i go wdrożyć jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="37ea7-124">Alternately, Appendix A has instructions for how toocreate and test a simple AzureML experiment and deploy it as a web service.</span></span>

## <a name="create-an-api-management-instance"></a><span data-ttu-id="37ea7-125">Tworzenie wystąpienia usługi API Management</span><span class="sxs-lookup"><span data-stu-id="37ea7-125">Create an API Management instance</span></span>
<span data-ttu-id="37ea7-126">Poniżej przedstawiono kroki hello przy użyciu interfejsu API zarządzania toomanage usługi sieci web uczenie maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="37ea7-126">Below are hello steps for using API Management toomanage your AzureML web service.</span></span> <span data-ttu-id="37ea7-127">Najpierw utwórz wystąpienie usługi.</span><span class="sxs-lookup"><span data-stu-id="37ea7-127">First create a service instance.</span></span> <span data-ttu-id="37ea7-128">Zaloguj się za toohello [klasyczny Portal](https://manage.windowsazure.com/) i kliknij przycisk **nowy** > **usługi aplikacji** > **zarządzanie interfejsami API**  >  **Utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-128">Log in toohello [Classic Portal](https://manage.windowsazure.com/) and click **New** > **App Services** > **API Management** > **Create**.</span></span>

![Tworzenie wystąpienia](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

<span data-ttu-id="37ea7-130">Określ unikatową **adres URL**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-130">Specify a unique **URL**.</span></span> <span data-ttu-id="37ea7-131">Ten przewodnik po używa **demoazureml** — należy toochoose coś innego.</span><span class="sxs-lookup"><span data-stu-id="37ea7-131">This guide uses **demoazureml** – you will need toochoose something different.</span></span> <span data-ttu-id="37ea7-132">Wybierz żądaną hello **subskrypcji** i **Region** wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="37ea7-132">Choose hello desired **Subscription** and **Region** for your service instance.</span></span> <span data-ttu-id="37ea7-133">Po wprowadzeniu wybrane opcje, kliknij przycisk Dalej hello.</span><span class="sxs-lookup"><span data-stu-id="37ea7-133">After making your selections, click hello next button.</span></span>

![Utwórz usług-1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

<span data-ttu-id="37ea7-135">Określ wartość hello **nazwa organizacji**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-135">Specify a value for hello **Organization Name**.</span></span> <span data-ttu-id="37ea7-136">Ten przewodnik po używa **demoazureml** — należy toochoose coś innego.</span><span class="sxs-lookup"><span data-stu-id="37ea7-136">This guide uses **demoazureml** – you will need toochoose something different.</span></span> <span data-ttu-id="37ea7-137">Wprowadź adres e-mail w hello **e-mail administratora** pola.</span><span class="sxs-lookup"><span data-stu-id="37ea7-137">Enter your email address in hello **administrator e-mail** field.</span></span> <span data-ttu-id="37ea7-138">Ten adres e-mail jest używany dla powiadomień z hello system zarządzania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="37ea7-138">This email address is used for notifications from hello API Management system.</span></span>

![Utwórz usług-2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

<span data-ttu-id="37ea7-140">Kliknij przycisk toocreate pole wyboru hello wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="37ea7-140">Click hello check box toocreate your service instance.</span></span> <span data-ttu-id="37ea7-141">*Zajmowała toothirty minut nowe toobe usługi utworzone*.</span><span class="sxs-lookup"><span data-stu-id="37ea7-141">*It takes up toothirty minutes for a new service toobe created*.</span></span>

## <a name="create-hello-api"></a><span data-ttu-id="37ea7-142">Utwórz interfejs API hello</span><span class="sxs-lookup"><span data-stu-id="37ea7-142">Create hello API</span></span>
<span data-ttu-id="37ea7-143">Po utworzeniu wystąpienia usługi hello hello następnym krokiem jest toocreate hello API.</span><span class="sxs-lookup"><span data-stu-id="37ea7-143">Once hello service instance is created, hello next step is toocreate hello API.</span></span> <span data-ttu-id="37ea7-144">Interfejs API składa się z zestawu operacji, które mogą być wywoływane z poziomu aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="37ea7-144">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="37ea7-145">Operacje interfejsu API są tooexisting serwerem proxy usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="37ea7-145">API operations are proxied tooexisting web services.</span></span> <span data-ttu-id="37ea7-146">W tym przewodniku tworzy interfejsów API toohello tego serwera proxy, istniejące rekordy zasobów uczenie maszynowe Azure i usługi BES usług sieci web.</span><span class="sxs-lookup"><span data-stu-id="37ea7-146">This guide creates APIs that proxy toohello existing AzureML RRS and BES web services.</span></span>

<span data-ttu-id="37ea7-147">Interfejsy API są tworzone i skonfigurowana z hello interfejsu API wydawcy portalu, który jest dostępny za pośrednictwem hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="37ea7-147">APIs are created and configured from hello API publisher portal, which is accessed through hello Azure Classic Portal.</span></span> <span data-ttu-id="37ea7-148">tooreach hello wydawcy portalu, wybierz wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="37ea7-148">tooreach hello publisher portal, select your service instance.</span></span>

![Wybierz usługę wystąpienia](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

<span data-ttu-id="37ea7-150">Kliknij przycisk **Zarządzaj** w hello portalu klasycznego Azure dla usługi interfejsu API zarządzania.</span><span class="sxs-lookup"><span data-stu-id="37ea7-150">Click **Manage** in hello Azure Classic Portal for your API Management service.</span></span>

![Usługa zarządzania](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

<span data-ttu-id="37ea7-152">Kliknij przycisk **interfejsów API** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij **dodać interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-152">Click **APIs** from hello **API Management** menu on hello left, and then click **Add API**.</span></span>

![Interfejs API zarządzania menu](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

<span data-ttu-id="37ea7-154">Typ **API pokaz uczenie maszynowe Azure** jako hello **Nazwa interfejsu API sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-154">Type **AzureML Demo API** as hello **Web API name**.</span></span> <span data-ttu-id="37ea7-155">Typ **https://ussouthcentral.services.azureml.net** jako hello **adres URL usługi sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-155">Type **https://ussouthcentral.services.azureml.net** as hello **Web service URL**.</span></span> <span data-ttu-id="37ea7-156">Typ **pokaz uczenie maszynowe Azure** jako hello **sufiks adresu URL interfejsu API sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-156">Type **azureml-demo** as hello **Web API URL suffix**.</span></span> <span data-ttu-id="37ea7-157">Sprawdź **HTTPS** jako hello **adres URL interfejsu API sieci Web** schematu.</span><span class="sxs-lookup"><span data-stu-id="37ea7-157">Check **HTTPS** as hello **Web API URL** scheme.</span></span> <span data-ttu-id="37ea7-158">Wybierz **Starter** jako **produkty**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-158">Select **Starter** as **Products**.</span></span> <span data-ttu-id="37ea7-159">Gdy skończysz, kliknij przycisk **zapisać** hello toocreate interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="37ea7-159">When finished, click **Save** toocreate hello API.</span></span>

![Dodaj — nowy — interfejs api](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-hello-operations"></a><span data-ttu-id="37ea7-161">Dodaj hello operacji</span><span class="sxs-lookup"><span data-stu-id="37ea7-161">Add hello operations</span></span>
<span data-ttu-id="37ea7-162">Kliknij przycisk **operacji dodawania** tooadd toothis operacje interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="37ea7-162">Click **Add operation** tooadd operations toothis API.</span></span>

![Dodaj operację](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

<span data-ttu-id="37ea7-164">Witaj **nowej operacji** oknie będą wyświetlane i hello **podpisu** będzie domyślnie wybierany kartę.</span><span class="sxs-lookup"><span data-stu-id="37ea7-164">hello **New operation** window will be displayed and hello **Signature** tab will be selected by default.</span></span>

## <a name="add-rrs-operation"></a><span data-ttu-id="37ea7-165">Dodaj operację rekordy zasobów</span><span class="sxs-lookup"><span data-stu-id="37ea7-165">Add RRS Operation</span></span>
<span data-ttu-id="37ea7-166">Najpierw utwórz operację na powitania usługi uczenie maszynowe Azure rekordy zasobów.</span><span class="sxs-lookup"><span data-stu-id="37ea7-166">First create an operation for hello AzureML RRS service.</span></span> <span data-ttu-id="37ea7-167">Wybierz **POST** jako hello **zlecenie HTTP**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-167">Select **POST** as hello **HTTP verb**.</span></span> <span data-ttu-id="37ea7-168">Typ **/services/ /workspaces/ {obszaru roboczego} {usługi} / execute? api-version = {apiversion} & szczegóły = {szczegóły}** jako hello **szablon adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-168">Type **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}** as hello **URL template**.</span></span> <span data-ttu-id="37ea7-169">Typ **wykonania rekordy zasobów** jako hello **Nazwa wyświetlana**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-169">Type **RRS Execute** as hello **Display name**.</span></span>

![Dodawanie rekordów zasobów operacji podpisu](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

<span data-ttu-id="37ea7-171">Kliknij przycisk **odpowiedzi** > **dodać** na powitania po lewej stronie i wybierz pozycję **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-171">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="37ea7-172">Kliknij przycisk **zapisać** toosave tej operacji.</span><span class="sxs-lookup"><span data-stu-id="37ea7-172">Click **Save** toosave this operation.</span></span>

![Dodawanie rekordów zasobów operacji odpowiedzi](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a><span data-ttu-id="37ea7-174">Dodaj BES operacji</span><span class="sxs-lookup"><span data-stu-id="37ea7-174">Add BES Operations</span></span>
<span data-ttu-id="37ea7-175">Zrzuty ekranu nie są włączone dla hello operacji usługi BES są one bardzo podobne toothose hello RR operacji dodawania.</span><span class="sxs-lookup"><span data-stu-id="37ea7-175">Screenshots are not included for hello BES operations as they are very similar toothose for adding hello RRS operation.</span></span>

### <a name="submit-but-not-start-a-batch-execution-job"></a><span data-ttu-id="37ea7-176">Przesyłanie (ale nie start) zadanie wsadowe</span><span class="sxs-lookup"><span data-stu-id="37ea7-176">Submit (but not start) a Batch Execution job</span></span>
<span data-ttu-id="37ea7-177">Kliknij przycisk **operacji dodawania** tooadd hello BES uczenie maszynowe Azure operacji toohello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="37ea7-177">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="37ea7-178">Wybierz **POST** dla hello **zlecenie HTTP**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-178">Select **POST** for hello **HTTP verb**.</span></span> <span data-ttu-id="37ea7-179">Typ **/services/ /workspaces/ {obszaru roboczego} {usługi} / zadania? api-version = {apiversion}** dla hello **szablon adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-179">Type **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="37ea7-180">Typ **przesłać BES** dla hello **Nazwa wyświetlana**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-180">Type **BES Submit** for hello **Display name**.</span></span> <span data-ttu-id="37ea7-181">Kliknij przycisk **odpowiedzi** > **dodać** na powitania po lewej stronie i wybierz pozycję **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-181">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="37ea7-182">Kliknij przycisk **zapisać** toosave tej operacji.</span><span class="sxs-lookup"><span data-stu-id="37ea7-182">Click **Save** toosave this operation.</span></span>

### <a name="start-a-batch-execution-job"></a><span data-ttu-id="37ea7-183">Uruchom zadanie wsadowe</span><span class="sxs-lookup"><span data-stu-id="37ea7-183">Start a Batch Execution job</span></span>
<span data-ttu-id="37ea7-184">Kliknij przycisk **operacji dodawania** tooadd hello BES uczenie maszynowe Azure operacji toohello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="37ea7-184">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="37ea7-185">Wybierz **POST** dla hello **zlecenie HTTP**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-185">Select **POST** for hello **HTTP verb**.</span></span> <span data-ttu-id="37ea7-186">Typ **/jobs/ /services/ {usługi} /workspaces/ {obszaru roboczego} {jobid} / start? api-version = {apiversion}** dla hello **szablon adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-186">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="37ea7-187">Typ **BES Start** dla hello **Nazwa wyświetlana**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-187">Type **BES Start** for hello **Display name**.</span></span> <span data-ttu-id="37ea7-188">Kliknij przycisk **odpowiedzi** > **dodać** na powitania po lewej stronie i wybierz pozycję **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-188">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="37ea7-189">Kliknij przycisk **zapisać** toosave tej operacji.</span><span class="sxs-lookup"><span data-stu-id="37ea7-189">Click **Save** toosave this operation.</span></span>

### <a name="get-hello-status-or-result-of-a-batch-execution-job"></a><span data-ttu-id="37ea7-190">Pobierz stan hello lub wyniku zadania wsadowe</span><span class="sxs-lookup"><span data-stu-id="37ea7-190">Get hello status or result of a Batch Execution job</span></span>
<span data-ttu-id="37ea7-191">Kliknij przycisk **operacji dodawania** tooadd hello BES uczenie maszynowe Azure operacji toohello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="37ea7-191">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="37ea7-192">Wybierz **UZYSKAĆ** dla hello **zlecenie HTTP**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-192">Select **GET** for hello **HTTP verb**.</span></span> <span data-ttu-id="37ea7-193">Typ **/jobs/ /services/ {usługi} /workspaces/ {obszaru roboczego} {jobid}? api-version = {apiversion}** dla hello **szablon adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-193">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="37ea7-194">Typ **stanu usługi BES** dla hello **Nazwa wyświetlana**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-194">Type **BES Status** for hello **Display name**.</span></span> <span data-ttu-id="37ea7-195">Kliknij przycisk **odpowiedzi** > **dodać** na powitania po lewej stronie i wybierz pozycję **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-195">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="37ea7-196">Kliknij przycisk **zapisać** toosave tej operacji.</span><span class="sxs-lookup"><span data-stu-id="37ea7-196">Click **Save** toosave this operation.</span></span>

### <a name="delete-a-batch-execution-job"></a><span data-ttu-id="37ea7-197">Usuń zadanie wsadowe</span><span class="sxs-lookup"><span data-stu-id="37ea7-197">Delete a Batch Execution job</span></span>
<span data-ttu-id="37ea7-198">Kliknij przycisk **operacji dodawania** tooadd hello BES uczenie maszynowe Azure operacji toohello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="37ea7-198">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="37ea7-199">Wybierz **usunąć** dla hello **zlecenie HTTP**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-199">Select **DELETE** for hello **HTTP verb**.</span></span> <span data-ttu-id="37ea7-200">Typ **/jobs/ /services/ {usługi} /workspaces/ {obszaru roboczego} {jobid}? api-version = {apiversion}** dla hello **szablon adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-200">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="37ea7-201">Typ **usunąć BES** dla hello **Nazwa wyświetlana**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-201">Type **BES Delete** for hello **Display name**.</span></span> <span data-ttu-id="37ea7-202">Kliknij przycisk **odpowiedzi** > **dodać** na powitania po lewej stronie i wybierz pozycję **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-202">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="37ea7-203">Kliknij przycisk **zapisać** toosave tej operacji.</span><span class="sxs-lookup"><span data-stu-id="37ea7-203">Click **Save** toosave this operation.</span></span>

## <a name="call-an-operation-from-hello-developer-portal"></a><span data-ttu-id="37ea7-204">Wywołaj operację z hello portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="37ea7-204">Call an operation from hello Developer Portal</span></span>
<span data-ttu-id="37ea7-205">Operacje mogą być wywoływane bezpośrednio z portalu dla deweloperów hello, która zapewnia tooview wygodny sposób i przetestować hello operacje interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="37ea7-205">Operations can be called directly from hello Developer portal, which provides a convenient way tooview and test hello operations of an API.</span></span> <span data-ttu-id="37ea7-206">W tym kroku przewodnik będzie wywoływać hello **wykonania rekordy zasobów** metody, która została dodana toohello **API pokaz uczenie maszynowe Azure**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-206">In this guide step you will call hello **RRS Execute** method that was added toohello **AzureML Demo API**.</span></span> <span data-ttu-id="37ea7-207">Kliknij przycisk **portalu dla deweloperów** menu hello w hello górnego prawego hello klasycznego portalu.</span><span class="sxs-lookup"><span data-stu-id="37ea7-207">Click **Developer portal** from hello menu at hello top right of hello Classic Portal.</span></span>

![portalu dla deweloperów](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

<span data-ttu-id="37ea7-209">Kliknij przycisk **interfejsów API** z hello menu u góry, a następnie kliknij przycisk **API pokaz uczenie maszynowe Azure** toosee hello operacje dostępne.</span><span class="sxs-lookup"><span data-stu-id="37ea7-209">Click **APIs** from hello top menu, and then click **AzureML Demo API** toosee hello operations available.</span></span>

![Interfejs api demoazureml](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

<span data-ttu-id="37ea7-211">Wybierz **wykonania rekordy zasobów** hello operacji.</span><span class="sxs-lookup"><span data-stu-id="37ea7-211">Select **RRS Execute** for hello operation.</span></span> <span data-ttu-id="37ea7-212">Kliknij przycisk **wypróbuj**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-212">Click **Try It**.</span></span>

![try it](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

<span data-ttu-id="37ea7-214">Żądanie parametru, wpisz sieci **obszaru roboczego**, **usługi**, **2.0** dla hello **apiversion**, i **true**dla hello **szczegóły**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-214">For Request parameters, type your **workspace**,  **service**, **2.0** for hello **apiversion**, and  **true** for hello **details**.</span></span> <span data-ttu-id="37ea7-215">Można znaleźć sieci **obszaru roboczego** i **usługi** w pulpicie nawigacyjnym usługi sieci web uczenie maszynowe Azure systemu hello (zobacz **testowanie usługi sieci web hello** w dodatku A).</span><span class="sxs-lookup"><span data-stu-id="37ea7-215">You can find your **workspace** and **service** in hello AzureML web service dashboard (see **Test hello web service** in Appendix A).</span></span>

<span data-ttu-id="37ea7-216">Dla nagłówków żądań, kliknij przycisk **Dodaj nagłówek** i typ **Content-Type** i **application/json**, następnie kliknij przycisk **Dodaj nagłówek** i typ **autoryzacji** i **elementu nośnego <YOUR AZUREML SERVICE API-KEY>** .</span><span class="sxs-lookup"><span data-stu-id="37ea7-216">For Request headers, click **Add header** and type **Content-Type** and **application/json**, then click **Add header** and type **Authorization** and **Bearer <YOUR AZUREML SERVICE API-KEY>**.</span></span> <span data-ttu-id="37ea7-217">Można znaleźć sieci **klucz interfejsu api** w pulpicie nawigacyjnym usługi sieci web uczenie maszynowe Azure systemu hello (zobacz **testowanie usługi sieci web hello** w dodatku A).</span><span class="sxs-lookup"><span data-stu-id="37ea7-217">You can find your **api key** in hello AzureML web service dashboard (see **Test hello web service** in Appendix A).</span></span>

<span data-ttu-id="37ea7-218">Typ **{"Dane wejściowe": {"input1": {"ColumnNames": ["Col2"] "wartości": [["jest to dobry dzień"]]}}, "GlobalParameters": {}}** hello treści żądania.</span><span class="sxs-lookup"><span data-stu-id="37ea7-218">Type **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}** for hello request body.</span></span>

![uczenie maszynowe Azure pokaz api](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

<span data-ttu-id="37ea7-220">Kliknij przycisk **wysyłania**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-220">Click **Send**.</span></span>

![Wyślij](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

<span data-ttu-id="37ea7-222">Po wywołaniu operacji portalu dla deweloperów hello Wyświetla hello **żądany adres URL** z hello usługi zaplecza, hello **stanu odpowiedzi**, hello **nagłówki odpowiedzi**, natomiast dla ustawienia **zawartości odpowiedzi**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-222">After an operation is invoked, hello developer portal displays hello **Requested URL** from hello back-end service, hello **Response status**, hello **Response headers**, and any **Response content**.</span></span>

![Stan odpowiedzi](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a><span data-ttu-id="37ea7-224">Dodatek A — tworzenie i testowanie prostego uczenie maszynowe Azure usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="37ea7-224">Appendix A - Creating and testing a simple AzureML web service</span></span>
### <a name="creating-hello-experiment"></a><span data-ttu-id="37ea7-225">Tworzenie eksperymentu hello</span><span class="sxs-lookup"><span data-stu-id="37ea7-225">Creating hello experiment</span></span>
<span data-ttu-id="37ea7-226">Poniżej przedstawiono kroki hello Tworzenie prostego eksperymentu uczenie maszynowe Azure i wdrażania go w postaci usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="37ea7-226">Below are hello steps for creating a simple AzureML experiment and deploying it as a web service.</span></span> <span data-ttu-id="37ea7-227">Witaj przyjmuje usługi sieci web jako danych wejściowych z kolumną zawierającą dowolnego tekstu i zwraca zestaw funkcji reprezentowane jako wartości całkowite.</span><span class="sxs-lookup"><span data-stu-id="37ea7-227">hello web service takes as input a column of arbitrary text and returns a set of features represented as integers.</span></span> <span data-ttu-id="37ea7-228">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="37ea7-228">For example:</span></span>

| <span data-ttu-id="37ea7-229">Tekst</span><span class="sxs-lookup"><span data-stu-id="37ea7-229">Text</span></span> | <span data-ttu-id="37ea7-230">Tekst w formie skrótu</span><span class="sxs-lookup"><span data-stu-id="37ea7-230">Hashed Text</span></span> |
| --- | --- |
| <span data-ttu-id="37ea7-231">Jest to dobry dzień</span><span class="sxs-lookup"><span data-stu-id="37ea7-231">This is a good day</span></span> |<span data-ttu-id="37ea7-232">1 1 2 2 0 2 0 1</span><span class="sxs-lookup"><span data-stu-id="37ea7-232">1 1 2 2 0 2 0 1</span></span> |

<span data-ttu-id="37ea7-233">Po pierwsze, za pomocą przeglądarki wybranych przez użytkownika, przejdź do: [https://studio.azureml.net/](https://studio.azureml.net/) , a następnie wprowadź toolog Twoje poświadczenia w.</span><span class="sxs-lookup"><span data-stu-id="37ea7-233">First, using a browser of your choice, navigate to: [https://studio.azureml.net/](https://studio.azureml.net/) and enter your credentials toolog in.</span></span> <span data-ttu-id="37ea7-234">Następnie należy utworzyć nowy eksperyment puste.</span><span class="sxs-lookup"><span data-stu-id="37ea7-234">Next, create a new blank experiment.</span></span>

![Wyszukiwanie — eksperymentu — szablony](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

<span data-ttu-id="37ea7-236">Zmień nazwę zbyt**SimpleFeatureHashingExperiment**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-236">Rename it too**SimpleFeatureHashingExperiment**.</span></span> <span data-ttu-id="37ea7-237">Rozwiń węzeł **zapisane zestawów danych** i przeciągnij **przeglądami książki z Amazon** na eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="37ea7-237">Expand **Saved Datasets** and drag **Book Reviews from Amazon** onto your experiment.</span></span>

![prosty — funkcja mieszania eksperymentu](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

<span data-ttu-id="37ea7-239">Rozwiń węzeł **transformacji danych** i **manipulowania** i przeciągnij **Select Columns in Dataset** na eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="37ea7-239">Expand **Data Transformation** and **Manipulation** and drag **Select Columns in Dataset** onto your experiment.</span></span> <span data-ttu-id="37ea7-240">Połącz **przeglądami książki z Amazon** za**Select Columns in Dataset**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-240">Connect **Book Reviews from Amazon** too**Select Columns in Dataset**.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

<span data-ttu-id="37ea7-242">Kliknij przycisk **Select Columns in Dataset** , a następnie kliknij przycisk **Uruchom selektor kolumn** i wybierz **Col2**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-242">Click **Select Columns in Dataset** and then click **Launch column selector** and select **Col2**.</span></span> <span data-ttu-id="37ea7-243">Kliknij przycisk tooapply znacznikiem wyboru hello tych zmian.</span><span class="sxs-lookup"><span data-stu-id="37ea7-243">Click hello checkmark tooapply these changes.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

<span data-ttu-id="37ea7-245">Rozwiń węzeł **Analiza tekstu** i przeciągnij **Tworzenie skrótu funkcji** na powitania eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="37ea7-245">Expand **Text Analytics** and drag **Feature Hashing** onto hello experiment.</span></span> <span data-ttu-id="37ea7-246">Połącz **Select Columns in Dataset** za**Tworzenie skrótu funkcji**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-246">Connect **Select Columns in Dataset** too**Feature Hashing**.</span></span>

![Connect--kolumny projektu](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

<span data-ttu-id="37ea7-248">Typ **3** dla hello **mieszania bitsize**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-248">Type **3** for hello **Hashing bitsize**.</span></span> <span data-ttu-id="37ea7-249">Spowoduje to utworzenie 8 (23) kolumny.</span><span class="sxs-lookup"><span data-stu-id="37ea7-249">This will create 8 (23) columns.</span></span>

![Tworzenie skrótów bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

<span data-ttu-id="37ea7-251">W tym momencie możesz tooclick **Uruchom** tootest hello eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="37ea7-251">At this point, you may want tooclick **Run** tootest hello experiment.</span></span>

![Uruchom](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a><span data-ttu-id="37ea7-253">Tworzenie usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="37ea7-253">Create a web service</span></span>
<span data-ttu-id="37ea7-254">Teraz Utwórz usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="37ea7-254">Now create a web service.</span></span> <span data-ttu-id="37ea7-255">Rozwiń węzeł **usługi sieci Web** i przeciągnij **dane wejściowe** na eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="37ea7-255">Expand **Web Service** and drag **Input** onto your experiment.</span></span> <span data-ttu-id="37ea7-256">Połącz **dane wejściowe** za**Tworzenie skrótu funkcji**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-256">Connect **Input** too**Feature Hashing**.</span></span> <span data-ttu-id="37ea7-257">Przeciągnij również **dane wyjściowe** na eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="37ea7-257">Also drag **output** onto your experiment.</span></span> <span data-ttu-id="37ea7-258">Połącz **dane wyjściowe** za**Tworzenie skrótu funkcji**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-258">Connect **Output** too**Feature Hashing**.</span></span>

![dane wyjściowe do-— Tworzenie skrótu funkcji](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

<span data-ttu-id="37ea7-260">Kliknij przycisk **opublikować usługi sieci web**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-260">Click **Publish web service**.</span></span>

![Publikowanie — Usługa sieci web](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

<span data-ttu-id="37ea7-262">Kliknij przycisk **tak** toopublish hello eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="37ea7-262">Click **Yes** toopublish hello experiment.</span></span>

![tak aby opublikować](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-hello-web-service"></a><span data-ttu-id="37ea7-264">Usługa sieci web hello testu</span><span class="sxs-lookup"><span data-stu-id="37ea7-264">Test hello web service</span></span>
<span data-ttu-id="37ea7-265">Usługi sieci web uczenie maszynowe Azure składa się z punktów końcowych (usługi wykonywania wsadowego) BES i RSS (żądania/odpowiedzi usługi).</span><span class="sxs-lookup"><span data-stu-id="37ea7-265">An AzureML web service consists of RSS (request/response service) and BES (batch execution service) endpoints.</span></span> <span data-ttu-id="37ea7-266">Funkcja RSS jest synchroniczne wykonywania.</span><span class="sxs-lookup"><span data-stu-id="37ea7-266">RSS is for synchronous execution.</span></span> <span data-ttu-id="37ea7-267">BES jest do wykonywania zadań asynchronicznych.</span><span class="sxs-lookup"><span data-stu-id="37ea7-267">BES is for asynchronous job execution.</span></span> <span data-ttu-id="37ea7-268">usługi sieci web ze źródłem Python próbki hello poniżej tootest, konieczne może toodownload i hello Zainstaluj zestaw Azure SDK dla języka Python (zobacz: [jak tooinstall Python](../python-how-to-install.md)).</span><span class="sxs-lookup"><span data-stu-id="37ea7-268">tootest your web service with hello sample Python source below, you may need toodownload and install hello Azure SDK for Python (see: [How tooinstall Python](../python-how-to-install.md)).</span></span>

<span data-ttu-id="37ea7-269">Należy również hello **obszaru roboczego**, **usługi**, i **api_key** eksperymentu źródła próbki hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="37ea7-269">You will also need hello **workspace**, **service**, and **api_key** of your experiment for hello sample source below.</span></span> <span data-ttu-id="37ea7-270">Hello obszaru roboczego i usługi można znaleźć, klikając opcję **żądanie/odpowiedź** lub **Batch Execution** swojego eksperymentu w pulpicie nawigacyjnym usługi sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="37ea7-270">You can find hello workspace and service by clicking either **Request/Response** or **Batch Execution** for your experiment in hello web service dashboard.</span></span>

![Znajdź obszar roboczy i usługi](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

<span data-ttu-id="37ea7-272">Można znaleźć hello **api_key** , klikając na pulpicie nawigacyjnym usługi sieci web hello eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="37ea7-272">You can find hello **api_key** by clicking your experiment in hello web service dashboard.</span></span>

![Znajdź api-key](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a><span data-ttu-id="37ea7-274">Punkt końcowy RR testu</span><span class="sxs-lookup"><span data-stu-id="37ea7-274">Test RRS endpoint</span></span>
##### <a name="test-button"></a><span data-ttu-id="37ea7-275">Przycisk Testuj</span><span class="sxs-lookup"><span data-stu-id="37ea7-275">Test button</span></span>
<span data-ttu-id="37ea7-276">Punkt końcowy łatwy sposób tootest hello rekordy zasobów jest tooclick **testu** na pulpicie nawigacyjnym usługi sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="37ea7-276">An easy way tootest hello RRS endpoint is tooclick **Test** on hello web service dashboard.</span></span>

![Test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

<span data-ttu-id="37ea7-278">Typ **to dobry dzień** dla **col2**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-278">Type **This is a good day** for **col2**.</span></span> <span data-ttu-id="37ea7-279">Kliknij znacznik wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="37ea7-279">Click hello checkmark.</span></span>

![Wprowadź dane](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

<span data-ttu-id="37ea7-281">Zobaczysz ekran podobny do</span><span class="sxs-lookup"><span data-stu-id="37ea7-281">You will see something like</span></span>

![Przykładowe wyniki](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a><span data-ttu-id="37ea7-283">Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="37ea7-283">Sample Code</span></span>
<span data-ttu-id="37ea7-284">Inny sposób tootest Twojego rekordy zasobów jest z kodu klienta.</span><span class="sxs-lookup"><span data-stu-id="37ea7-284">Another way tootest your RRS is from your client code.</span></span> <span data-ttu-id="37ea7-285">Jeśli klikniesz przycisk **żądania/odpowiedzi** na hello pulpitu nawigacyjnego i przewiń w dół toohello, zostanie wyświetlone przykładowego kodu dla C#, Python i R. Widoczne będzie także składni hello żądania RR hello, włącznie z identyfikatora URI żądania hello, nagłówki i treść.</span><span class="sxs-lookup"><span data-stu-id="37ea7-285">If you click **Request/response** on hello dashboard and scroll toohello bottom, you will see sample code for C#, Python, and R. You will also see hello syntax of hello RRS request, including hello request URI, headers, and body.</span></span>

<span data-ttu-id="37ea7-286">Ten przewodnik zawiera pracy przykład Python.</span><span class="sxs-lookup"><span data-stu-id="37ea7-286">This guide shows a working Python example.</span></span> <span data-ttu-id="37ea7-287">Konieczne będzie toomodify go przy użyciu hello **obszaru roboczego**, **usługi**, i **api_key** eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="37ea7-287">You will need toomodify it with hello **workspace**, **service**, and **api_key** of your experiment.</span></span>

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
        print("hello request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a><span data-ttu-id="37ea7-288">Punkt końcowy usługi BES testu</span><span class="sxs-lookup"><span data-stu-id="37ea7-288">Test BES endpoint</span></span>
<span data-ttu-id="37ea7-289">Kliknij przycisk **wykonywanie wsadowe** na dole toohello hello pulpitu nawigacyjnego i przewijania.</span><span class="sxs-lookup"><span data-stu-id="37ea7-289">Click **Batch execution** on hello dashboard and scroll toohello bottom.</span></span> <span data-ttu-id="37ea7-290">Zostanie wyświetlone przykładowego kodu dla C#, Python i R. Widoczne będzie także hello składnia hello BES żądań toosubmit zadania, uruchomić zadanie, Pobierz stan hello lub wyniki zadania i usuwanie zadania.</span><span class="sxs-lookup"><span data-stu-id="37ea7-290">You will see sample code for C#, Python, and R. You will also see hello syntax of hello BES requests toosubmit a job, start a job, get hello status or results of a job, and delete a job.</span></span>

<span data-ttu-id="37ea7-291">Ten przewodnik zawiera pracy przykład Python.</span><span class="sxs-lookup"><span data-stu-id="37ea7-291">This guide shows a working Python example.</span></span> <span data-ttu-id="37ea7-292">Należy toomodify za pomocą hello **obszaru roboczego**, **usługi**, i **api_key** eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="37ea7-292">You need toomodify it with hello **workspace**, **service**, and **api_key** of your experiment.</span></span> <span data-ttu-id="37ea7-293">Ponadto należy toomodify hello **nazwy konta magazynu**, **klucz konta magazynu**, i **nazwa kontenera magazynu**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-293">Additionally, you need toomodify hello **storage account name**, **storage account key**, and **storage container name**.</span></span> <span data-ttu-id="37ea7-294">Ponadto należy toomodify lokalizację hello hello **pliku wejściowego** i lokalizację hello hello **pliku wyjściowego**.</span><span class="sxs-lookup"><span data-stu-id="37ea7-294">Lastly, you will need toomodify hello location of hello **input file** and hello location of hello **output file**.</span></span>

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH hello API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH hello LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH hello LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("hello request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading hello result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written toohello file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("hello results for " + outputName + " are available at hello following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "hello results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading hello input tooblob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded hello input tooblob storage"
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
    print("Submitting hello job...")
    # submit hello job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove hello enclosing double-quotes
    print("Job ID: " + job_id)
    # start hello job
    print("Starting hello job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking hello job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in hello follwing code
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
