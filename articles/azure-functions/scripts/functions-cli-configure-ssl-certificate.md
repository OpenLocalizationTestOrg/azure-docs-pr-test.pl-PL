---
title: "Przykładowym skrypcie interfejsu wiersza polecenia Azure — wiązanie SSL niestandardowych certyfikatów aplikacji funkcja | Dokumentacja firmy Microsoft"
description: "Przykładowym skrypcie interfejsu wiersza polecenia Azure — wiązanie niestandardowe certyfikat SSL do aplikacji funkcji na platformie Azure"
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
ms.openlocfilehash: ddabb701d7d5615232d1f6163aa6fb166efe5cb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-function-app"></a><span data-ttu-id="e4b27-103">Powiązania niestandardowego certyfikatu SSL do aplikacji — funkcja</span><span class="sxs-lookup"><span data-stu-id="e4b27-103">Bind a custom SSL certificate to a function app</span></span>

<span data-ttu-id="e4b27-104">Ten przykładowy skrypt tworzy aplikacji funkcji w usłudze App Service z powiązane zasoby, a następnie wiąże certyfikatu SSL z niestandardowej nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="e4b27-104">This sample script creates a function app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> <span data-ttu-id="e4b27-105">Dla tego przykładu należy:</span><span class="sxs-lookup"><span data-stu-id="e4b27-105">For this sample, you need:</span></span>

* <span data-ttu-id="e4b27-106">Dostęp do strony konfiguracji DNS rejestratora domen.</span><span class="sxs-lookup"><span data-stu-id="e4b27-106">Access to your domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="e4b27-107">Nieprawidłowa. Plik PFX i jego hasło dla certyfikatu SSL chcesz przekazać i ich powiązania.</span><span class="sxs-lookup"><span data-stu-id="e4b27-107">A valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

<span data-ttu-id="e4b27-108">Aby powiązać certyfikatu SSL, można utworzyć aplikacji funkcji w planie usługi aplikacji, a nie w planie zużycia.</span><span class="sxs-lookup"><span data-stu-id="e4b27-108">To bind an SSL certificate, your function app must be created in an App Service plan and not in a consumption plan.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e4b27-109">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="e4b27-109">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e4b27-110">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="e4b27-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="e4b27-111">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e4b27-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="e4b27-112">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="e4b27-112">Sample script</span></span>

<span data-ttu-id="e4b27-113">[!code-azurecli-interactive[główne](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "wiązania niestandardowego certyfikatu SSL w aplikacji sieci web")]</span><span class="sxs-lookup"><span data-stu-id="e4b27-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="e4b27-114">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="e4b27-114">Script explanation</span></span>

<span data-ttu-id="e4b27-115">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="e4b27-115">This script uses the following commands.</span></span> <span data-ttu-id="e4b27-116">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="e4b27-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e4b27-117">Polecenie</span><span class="sxs-lookup"><span data-stu-id="e4b27-117">Command</span></span> | <span data-ttu-id="e4b27-118">Uwagi</span><span class="sxs-lookup"><span data-stu-id="e4b27-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e4b27-119">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="e4b27-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e4b27-120">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="e4b27-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e4b27-121">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="e4b27-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="e4b27-122">Tworzy plan usługi aplikacji wymaganej do powiązania certyfikatów SSL.</span><span class="sxs-lookup"><span data-stu-id="e4b27-122">Creates an App Service plan required to bind SSL certificates.</span></span> |
| [<span data-ttu-id="e4b27-123">Utwórz az functionapp</span><span class="sxs-lookup"><span data-stu-id="e4b27-123">az functionapp create</span></span>]() | <span data-ttu-id="e4b27-124">Tworzy aplikację funkcji.</span><span class="sxs-lookup"><span data-stu-id="e4b27-124">Creates a function app.</span></span> |
| [<span data-ttu-id="e4b27-125">Dodaj nazwę az usługi aplikacji sieci web konfiguracji hosta</span><span class="sxs-lookup"><span data-stu-id="e4b27-125">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="e4b27-126">Mapuje niestandardową domenę do funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4b27-126">Maps a custom domain to the function app.</span></span> |
| [<span data-ttu-id="e4b27-127">AZ usługi aplikacji sieci web config ssl przekazywania</span><span class="sxs-lookup"><span data-stu-id="e4b27-127">az appservice web config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | <span data-ttu-id="e4b27-128">Przekazuje certyfikat SSL do aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="e4b27-128">Uploads an SSL certificate to a function app.</span></span> |
| [<span data-ttu-id="e4b27-129">powiązania ssl config az usługi aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="e4b27-129">az appservice web config ssl bind</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | <span data-ttu-id="e4b27-130">Wiąże aplikacji funkcji przekazano certyfikat SSL.</span><span class="sxs-lookup"><span data-stu-id="e4b27-130">Binds an uploaded SSL certificate to a function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e4b27-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e4b27-131">Next steps</span></span>

<span data-ttu-id="e4b27-132">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e4b27-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e4b27-133">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w [dokumentacji usługi Azure App Service]().</span><span class="sxs-lookup"><span data-stu-id="e4b27-133">Additional App Service CLI script samples can be found in the [Azure App Service documentation]().</span></span>
