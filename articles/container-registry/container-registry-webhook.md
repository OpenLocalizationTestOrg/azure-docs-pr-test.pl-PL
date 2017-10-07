---
title: "elementów webhook rejestru kontenera aaaAzure | Dokumentacja firmy Microsoft"
description: "Elementów webhook rejestru kontenera platformy Azure"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acr, azure-container-registry
keywords: "Docker kontenerów, ACR"
ms.assetid: 
ms.service: container-registry
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/06/2017
ms.author: nepeters
ms.openlocfilehash: adc2afec486007e2d54cd689e6f7ef8b1098db06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a><span data-ttu-id="d1ab7-104">Za pomocą elementów webhook rejestru kontenera Azure - Azure portal</span><span class="sxs-lookup"><span data-stu-id="d1ab7-104">Using Azure Container Registry webhooks - Azure portal</span></span>

<span data-ttu-id="d1ab7-105">Rejestru kontenera platformy Azure przechowywanych i zarządzanych obrazów prywatnej kontenera Docker, podobnie toohello Centrum Docker przechowuje publiczny obrazy usługi Docker.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-105">An Azure container registry stores and manages private Docker container images, similar toohello way Docker Hub stores public Docker images.</span></span> <span data-ttu-id="d1ab7-106">Możesz użyć zdarzenia tootrigger elementów webhook, gdy pewne akcje została wykonana w jednym z repozytoriami rejestru.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-106">You use webhooks tootrigger events when certain actions take place in one of your registry repositories.</span></span> <span data-ttu-id="d1ab7-107">Elementów Webhook mogą odpowiadać tooevents na poziomie rejestru hello lub może być zakres dół tooa repozytorium określonego tagu.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-107">Webhooks can respond tooevents at hello registry level or they can be scoped down tooa specific repository tag.</span></span> 

<span data-ttu-id="d1ab7-108">Więcej tła i pojęć, zobacz hello [omówienie](./container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="d1ab7-108">For more background and concepts, see hello [overview](./container-registry-intro.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1ab7-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d1ab7-109">Prerequisites</span></span> 

- <span data-ttu-id="d1ab7-110">Kontenera platformy Azure zarządzanych rejestru — Tworzenie rejestru kontenera zarządzanych w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-110">Azure container managed registry - Create a managed container registry in your Azure subscription.</span></span> <span data-ttu-id="d1ab7-111">Na przykład użyć hello portalu Azure lub hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-111">For example, use hello Azure portal or hello Azure CLI 2.0.</span></span> 
- <span data-ttu-id="d1ab7-112">Docker CLI - tooset komputera lokalnego jako Docker dostępu i host hello Docker polecenia interfejsu wiersza polecenia, należy zainstalować aparatem platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-112">Docker CLI - tooset up your local computer as a Docker host and access hello Docker CLI commands, install Docker Engine.</span></span> 

## <a name="create-webhook-azure-portal"></a><span data-ttu-id="d1ab7-113">Tworzenie elementu webhook w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d1ab7-113">Create webhook Azure portal</span></span>

1. <span data-ttu-id="d1ab7-114">Zaloguj się za toohello portalu Azure i przejdź toohello rejestru, w której ma zostać toocreate elementów webhook.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-114">Log in toohello Azure portal and navigate toohello registry in which you want toocreate webhooks.</span></span> 

2. <span data-ttu-id="d1ab7-115">W bloku kontenera hello wybierz kartę "Elementów Webhook" hello.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-115">In hello container blade, select hello "Webhooks" tab.</span></span> 

3. <span data-ttu-id="d1ab7-116">Wybierz "Dodaj" hello elementu webhook bloku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-116">Select "Add" from hello webhook blade toolbar.</span></span> 

4. <span data-ttu-id="d1ab7-117">Zakończenie hello *tworzenia elementu Webhook* formularza z hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="d1ab7-117">Complete hello *Create Webhook* form with hello following information:</span></span>

| <span data-ttu-id="d1ab7-118">Wartość</span><span class="sxs-lookup"><span data-stu-id="d1ab7-118">Value</span></span> | <span data-ttu-id="d1ab7-119">Opis</span><span class="sxs-lookup"><span data-stu-id="d1ab7-119">Description</span></span> |
|---|---|
| <span data-ttu-id="d1ab7-120">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d1ab7-120">Name</span></span> | <span data-ttu-id="d1ab7-121">Nazwa Hello ma toogive toohello webhook.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-121">hello name you want toogive toohello webhook.</span></span> <span data-ttu-id="d1ab7-122">Może zawierać tylko małe litery i cyfry oraz od 5 do 50 znaków.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-122">It can only contain lowercase letters and numbers and between 5-50 characters.</span></span> |
| <span data-ttu-id="d1ab7-123">Identyfikator URI usługi</span><span class="sxs-lookup"><span data-stu-id="d1ab7-123">Service URI</span></span> | <span data-ttu-id="d1ab7-124">Witaj gdzie hello webhook wysłać powiadomienia POST identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-124">hello URI where hello webhook should send POST notifications.</span></span> |
| <span data-ttu-id="d1ab7-125">Niestandardowe nagłówki</span><span class="sxs-lookup"><span data-stu-id="d1ab7-125">Custom headers</span></span> | <span data-ttu-id="d1ab7-126">Nagłówki ma toopass wraz z hello wysłanie żądania POST.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-126">Headers you want toopass along with hello POST request.</span></span> <span data-ttu-id="d1ab7-127">Należy je w "klucz: wartość" format.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-127">They should be in "key: value" format.</span></span> |
| <span data-ttu-id="d1ab7-128">Akcje wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="d1ab7-128">Trigger actions</span></span> | <span data-ttu-id="d1ab7-129">Akcje wyzwalających hello elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-129">Actions that trigger hello webhook.</span></span> <span data-ttu-id="d1ab7-130">Obecnie elementów webhook może zostać wyzwolone przez wypychania i/lub Usuń obraz tooan akcje.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-130">Currently webhooks can be triggered by push and/or delete actions tooan image.</span></span> |
| <span data-ttu-id="d1ab7-131">Stan</span><span class="sxs-lookup"><span data-stu-id="d1ab7-131">Status</span></span> | <span data-ttu-id="d1ab7-132">Stan Hello hello webhook po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-132">hello status for hello webhook after it's created.</span></span> <span data-ttu-id="d1ab7-133">Jest ona włączona domyślnie.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-133">It's enabled by default.</span></span> |
| <span data-ttu-id="d1ab7-134">Zakres</span><span class="sxs-lookup"><span data-stu-id="d1ab7-134">Scope</span></span> | <span data-ttu-id="d1ab7-135">Hello zakresu, na który hello działa elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-135">hello scope at which hello webhook works.</span></span> <span data-ttu-id="d1ab7-136">Zakres hello jest domyślnie dla wszystkich zdarzeń w rejestrze hello.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-136">By default hello scope is for all events in hello registry.</span></span> <span data-ttu-id="d1ab7-137">Można ją określić repozytorium lub tag przy użyciu formatu hello "repozytorium: tag".</span><span class="sxs-lookup"><span data-stu-id="d1ab7-137">It can be specified for a repository or a tag by using hello format "repository: tag".</span></span> |

<span data-ttu-id="d1ab7-138">Przykład elementu webhook formularza:</span><span class="sxs-lookup"><span data-stu-id="d1ab7-138">Example webhook form:</span></span>

![DCOS INTERFEJSU UŻYTKOWNIKA](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a><span data-ttu-id="d1ab7-140">Tworzenie elementu webhook wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d1ab7-140">Create webhook Azure CLI</span></span>

<span data-ttu-id="d1ab7-141">toocreate przy użyciu elementu webhook hello interfejsu wiersza polecenia Azure, użyj hello [tworzenia elementu webhook acr az](/cli/azure/acr/webhook#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-141">toocreate a webhook using hello Azure CLI, use hello [az acr webhook create](/cli/azure/acr/webhook#create) command.</span></span>

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a><span data-ttu-id="d1ab7-142">Element webhook testu</span><span class="sxs-lookup"><span data-stu-id="d1ab7-142">Test webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="d1ab7-143">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d1ab7-143">Azure portal</span></span>

<span data-ttu-id="d1ab7-144">Wcześniejsze toousing webhook hello w kontenerze obrazu wypychania i akcje usuwania, można zbadać, przy użyciu hello **Ping** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-144">Prior toousing hello webhook on container image push and delete actions, it can be tested using hello **Ping** button.</span></span> <span data-ttu-id="d1ab7-145">W przypadku hello Ping wysyła toohello żądania post ogólnego określony punkt końcowy i dzienniki hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-145">When used, hello Ping sends a generic post request toohello specified endpoint and logs hello response.</span></span> <span data-ttu-id="d1ab7-146">Jest to przydatne tooverify, który hello elementu webhook nie został skonfigurowany poprawnie.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-146">This is helpful tooverify that hello webhook has been set up correctly.</span></span>

1. <span data-ttu-id="d1ab7-147">Wybierz hello elementu webhook ma tootest.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-147">Select hello webhook you want tootest.</span></span> 
2. <span data-ttu-id="d1ab7-148">W górnym pasku narzędzi hello wybierz akcję "Wyślij polecenie Ping" hello.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-148">In hello top toolbar, select hello "Ping" action.</span></span> 
3. <span data-ttu-id="d1ab7-149">Sprawdź hello żądań i odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-149">Check hello request and response.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="d1ab7-150">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d1ab7-150">Azure CLI</span></span>

<span data-ttu-id="d1ab7-151">tootest element webhook ACR z hello Azure CLI Użyj hello [az acr elementu webhook ping](/cli/azure/acr/webhook#ping) polecenia.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-151">tootest an ACR webhook with hello Azure CLI, use hello [az acr webhook ping](/cli/azure/acr/webhook#ping) command.</span></span>

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

<span data-ttu-id="d1ab7-152">wyniki hello toosee, użyj hello [webhook acr az listy zdarzenia](/cli/azure/acr/webhook#list-events) polecenia.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-152">toosee hello results, use hello [az acr webhook list-events](/cli/azure/acr/webhook#list-events) command.</span></span> 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a><span data-ttu-id="d1ab7-153">Usuń element webhook</span><span class="sxs-lookup"><span data-stu-id="d1ab7-153">Delete webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="d1ab7-154">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d1ab7-154">Azure portal</span></span>

<span data-ttu-id="d1ab7-155">Każdy element webhook może zostać usunięta przez wybranie elementu webhook hello, a następnie przycisk Usuń hello na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d1ab7-155">Each webhook can be deleted by selecting hello webhook and then hello delete button on hello Azure portal.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="d1ab7-156">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d1ab7-156">Azure CLI</span></span>

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```