---
title: "Przykładowym skrypcie interfejsu wiersza polecenia Azure — wiązanie certyfikatu SSL niestandardowych aplikacji sieci web | Dokumentacja firmy Microsoft"
description: "Przykładowym skrypcie interfejsu wiersza polecenia Azure — wiązanie niestandardowe certyfikat SSL do aplikacji sieci web"
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
ms.openlocfilehash: d4fab3fb2c297bf5f498b63bee46692febb9180b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-web-app"></a><span data-ttu-id="d58e6-103">Wiązania niestandardowego certyfikatu SSL w aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="d58e6-103">Bind a custom SSL certificate to a web app</span></span>

<span data-ttu-id="d58e6-104">Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z powiązane zasoby, a następnie wiąże certyfikatu SSL z niestandardowej nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="d58e6-104">This sample script creates a web app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> <span data-ttu-id="d58e6-105">Dla tego przykładu potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="d58e6-105">For this sample, you will need:</span></span>

* <span data-ttu-id="d58e6-106">Dostęp do strony konfiguracji DNS rejestratora domen.</span><span class="sxs-lookup"><span data-stu-id="d58e6-106">Access to your domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="d58e6-107">Nieprawidłowa. Plik PFX i jego hasło dla certyfikatu SSL chcesz przekazać i ich powiązania.</span><span class="sxs-lookup"><span data-stu-id="d58e6-107">A valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d58e6-108">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="d58e6-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d58e6-109">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="d58e6-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="d58e6-110">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d58e6-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="d58e6-111">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="d58e6-111">Sample script</span></span>

<span data-ttu-id="d58e6-112">[!code-azurecli-interactive[główne](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "wiązania niestandardowego certyfikatu SSL w aplikacji sieci web")]</span><span class="sxs-lookup"><span data-stu-id="d58e6-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="d58e6-113">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="d58e6-113">Script explanation</span></span>

<span data-ttu-id="d58e6-114">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="d58e6-114">This script uses the following commands.</span></span> <span data-ttu-id="d58e6-115">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="d58e6-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d58e6-116">Polecenie</span><span class="sxs-lookup"><span data-stu-id="d58e6-116">Command</span></span> | <span data-ttu-id="d58e6-117">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d58e6-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d58e6-118">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="d58e6-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d58e6-119">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="d58e6-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d58e6-120">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="d58e6-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="d58e6-121">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="d58e6-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="d58e6-122">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="d58e6-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="d58e6-123">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d58e6-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="d58e6-124">Dodaj az nazwy hosta z konfiguracji aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="d58e6-124">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="d58e6-125">Mapuje domeny niestandardowej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="d58e6-125">Maps a custom domain to a web app.</span></span> |
| [<span data-ttu-id="d58e6-126">AZ aplikacji sieci Web config ssl przekazywania</span><span class="sxs-lookup"><span data-stu-id="d58e6-126">az webapp config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#upload) | <span data-ttu-id="d58e6-127">Przekazywanie certyfikatu SSL w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="d58e6-127">Uploads an SSL certificate to a web app.</span></span> |
| [<span data-ttu-id="d58e6-128">Powiązanie ssl konfiguracji aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="d58e6-128">az webapp config ssl bind</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#bind) | <span data-ttu-id="d58e6-129">Wiąże przekazano certyfikat SSL do aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="d58e6-129">Binds an uploaded SSL certificate to a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d58e6-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d58e6-130">Next steps</span></span>

<span data-ttu-id="d58e6-131">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d58e6-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d58e6-132">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d58e6-132">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
