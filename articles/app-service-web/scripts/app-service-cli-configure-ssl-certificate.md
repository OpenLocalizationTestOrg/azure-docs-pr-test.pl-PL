---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia - Bind niestandardowej aplikacji sieci web tooa certyfikatu SSL | Dokumentacja firmy Microsoft"
description: "Przykładowym skrypcie interfejsu wiersza polecenia Azure — wiązanie niestandardowej aplikacji sieci web tooa certyfikat SSL"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2fec2db84a2007fa6b005776c84d4f8cba392b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a><span data-ttu-id="a7c2d-103">Powiąż niestandardowej aplikacji sieci web tooa certyfikat protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="a7c2d-103">Bind a custom SSL certificate tooa web app</span></span>

<span data-ttu-id="a7c2d-104">Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z powiązane zasoby, a następnie powiązania certyfikatu SSL hello tooit nazwy domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="a7c2d-104">This sample script creates a web app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> <span data-ttu-id="a7c2d-105">Dla tego przykładu potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="a7c2d-105">For this sample, you will need:</span></span>

* <span data-ttu-id="a7c2d-106">Dostęp do strony konfiguracji DNS rejestratora domen tooyour.</span><span class="sxs-lookup"><span data-stu-id="a7c2d-106">Access tooyour domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="a7c2d-107">Nieprawidłowa. Plik PFX i jego hasło dla hello SSL certyfikatów można mają tooupload i ich powiązania.</span><span class="sxs-lookup"><span data-stu-id="a7c2d-107">A valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a7c2d-108">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="a7c2d-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a7c2d-109">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="a7c2d-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a7c2d-110">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a7c2d-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="a7c2d-111">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="a7c2d-111">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="a7c2d-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="a7c2d-112">Script explanation</span></span>

<span data-ttu-id="a7c2d-113">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="a7c2d-113">This script uses hello following commands.</span></span> <span data-ttu-id="a7c2d-114">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="a7c2d-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a7c2d-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="a7c2d-115">Command</span></span> | <span data-ttu-id="a7c2d-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a7c2d-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a7c2d-117">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="a7c2d-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a7c2d-118">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="a7c2d-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a7c2d-119">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="a7c2d-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="a7c2d-120">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="a7c2d-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="a7c2d-121">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="a7c2d-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="a7c2d-122">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a7c2d-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="a7c2d-123">Dodaj az nazwy hosta z konfiguracji aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="a7c2d-123">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="a7c2d-124">Mapuje aplikacji sieci web tooa domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="a7c2d-124">Maps a custom domain tooa web app.</span></span> |
| [<span data-ttu-id="a7c2d-125">AZ aplikacji sieci Web config ssl przekazywania</span><span class="sxs-lookup"><span data-stu-id="a7c2d-125">az webapp config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#upload) | <span data-ttu-id="a7c2d-126">Przekazanie aplikacji sieci web tooa certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="a7c2d-126">Uploads an SSL certificate tooa web app.</span></span> |
| [<span data-ttu-id="a7c2d-127">Powiązanie ssl konfiguracji aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="a7c2d-127">az webapp config ssl bind</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#bind) | <span data-ttu-id="a7c2d-128">Wiąże przekazanej aplikacji sieci web tooa certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="a7c2d-128">Binds an uploaded SSL certificate tooa web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a7c2d-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a7c2d-129">Next steps</span></span>

<span data-ttu-id="a7c2d-130">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a7c2d-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a7c2d-131">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a7c2d-131">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
