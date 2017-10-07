---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia - Bind niestandardowych aplikacji funkcji tooa certyfikatu SSL | Dokumentacja firmy Microsoft"
description: "Przykładowym skrypcie interfejsu wiersza polecenia Azure — wiązanie niestandardowych SSL certyfikatu tooa funkcji aplikacji na platformie Azure"
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 04/10/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 692dbc03583f2978131823083f1bfd257882664c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-function-app"></a><span data-ttu-id="ff063-103">Powiąż niestandardowych aplikacji funkcji tooa certyfikat protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="ff063-103">Bind a custom SSL certificate tooa function app</span></span>

<span data-ttu-id="ff063-104">Ten przykładowy skrypt tworzy aplikacji funkcji w usłudze App Service z powiązane zasoby, a następnie powiązania certyfikatu SSL hello tooit nazwy domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="ff063-104">This sample script creates a function app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> <span data-ttu-id="ff063-105">Dla tego przykładu należy:</span><span class="sxs-lookup"><span data-stu-id="ff063-105">For this sample, you need:</span></span>

* <span data-ttu-id="ff063-106">Dostęp do strony konfiguracji DNS rejestratora domen tooyour.</span><span class="sxs-lookup"><span data-stu-id="ff063-106">Access tooyour domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="ff063-107">Nieprawidłowa. Plik PFX i jego hasło dla hello SSL certyfikatów można mają tooupload i ich powiązania.</span><span class="sxs-lookup"><span data-stu-id="ff063-107">A valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

<span data-ttu-id="ff063-108">toobind certyfikatu SSL w planie usługi aplikacji, a nie w planie zużycia, należy utworzyć aplikację funkcji.</span><span class="sxs-lookup"><span data-stu-id="ff063-108">toobind an SSL certificate, your function app must be created in an App Service plan and not in a consumption plan.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ff063-109">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="ff063-109">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ff063-110">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="ff063-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ff063-111">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ff063-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ff063-112">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="ff063-112">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="ff063-113">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="ff063-113">Script explanation</span></span>

<span data-ttu-id="ff063-114">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="ff063-114">This script uses hello following commands.</span></span> <span data-ttu-id="ff063-115">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="ff063-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ff063-116">Polecenie</span><span class="sxs-lookup"><span data-stu-id="ff063-116">Command</span></span> | <span data-ttu-id="ff063-117">Uwagi</span><span class="sxs-lookup"><span data-stu-id="ff063-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ff063-118">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="ff063-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ff063-119">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="ff063-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ff063-120">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="ff063-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="ff063-121">Tworzy certyfikaty SSL toobind wymagane planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ff063-121">Creates an App Service plan required toobind SSL certificates.</span></span> |
| [<span data-ttu-id="ff063-122">Utwórz az functionapp</span><span class="sxs-lookup"><span data-stu-id="ff063-122">az functionapp create</span></span>]() | <span data-ttu-id="ff063-123">Tworzy aplikację funkcji.</span><span class="sxs-lookup"><span data-stu-id="ff063-123">Creates a function app.</span></span> |
| [<span data-ttu-id="ff063-124">Dodaj nazwę az usługi aplikacji sieci web konfiguracji hosta</span><span class="sxs-lookup"><span data-stu-id="ff063-124">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="ff063-125">Mapuje aplikacji funkcji toohello domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="ff063-125">Maps a custom domain toohello function app.</span></span> |
| [<span data-ttu-id="ff063-126">AZ usługi aplikacji sieci web config ssl przekazywania</span><span class="sxs-lookup"><span data-stu-id="ff063-126">az appservice web config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | <span data-ttu-id="ff063-127">Przekazanie aplikacji funkcja tooa certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="ff063-127">Uploads an SSL certificate tooa function app.</span></span> |
| [<span data-ttu-id="ff063-128">powiązania ssl config az usługi aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="ff063-128">az appservice web config ssl bind</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | <span data-ttu-id="ff063-129">Wiąże przekazanej aplikacji funkcji tooa certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="ff063-129">Binds an uploaded SSL certificate tooa function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ff063-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ff063-130">Next steps</span></span>

<span data-ttu-id="ff063-131">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ff063-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ff063-132">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure App Service]().</span><span class="sxs-lookup"><span data-stu-id="ff063-132">Additional App Service CLI script samples can be found in hello [Azure App Service documentation]().</span></span>
