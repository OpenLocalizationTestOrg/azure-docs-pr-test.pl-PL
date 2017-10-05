---
title: "Przykłady programu Azure PowerShell - usługi aplikacji | Dokumentacja firmy Microsoft"
description: "Przykłady programu Azure PowerShell - usługi aplikacji"
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: b48d1137-8c04-46e0-b430-101e07d7e470
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 3254fdd57cfcd170f22374c1e3b058e6081d8e8e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-powershell-samples"></a><span data-ttu-id="c73a2-103">Przykłady programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c73a2-103">Azure PowerShell Samples</span></span>

<span data-ttu-id="c73a2-104">Poniższa tabela zawiera linki do bash skrypty utworzone przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c73a2-104">The following table includes links to bash scripts built using the Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="c73a2-105">**Tworzenie aplikacji**</span><span class="sxs-lookup"><span data-stu-id="c73a2-105">**Create app**</span></span>||
| [<span data-ttu-id="c73a2-106">Tworzenie aplikacji sieci web z wdrożeniem z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="c73a2-106">Create a web app with deployment from GitHub</span></span>](./scripts/app-service-powershell-deploy-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="c73a2-107">Tworzy aplikacji sieci web platformy Azure, która pobiera kod z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="c73a2-107">Creates an Azure web app which pulls code from GitHub.</span></span> |
| [<span data-ttu-id="c73a2-108">Tworzenie aplikacji sieci Web z ciągłym wdrażania z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="c73a2-108">Create a web app with continuous deployment from GitHub</span></span>](./scripts/app-service-powershell-continuous-deployment-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="c73a2-109">Tworzy aplikacji sieci web platformy Azure, która wdraża stale kod z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="c73a2-109">Creates an Azure web app which continuously deploys code from GitHub.</span></span> |
| [<span data-ttu-id="c73a2-110">Tworzenie aplikacji sieci web i wdrażanie kodu przy użyciu FTP</span><span class="sxs-lookup"><span data-stu-id="c73a2-110">Create a web app and deploy code with FTP</span></span>](./scripts/app-service-powershell-deploy-ftp.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="c73a2-111">Tworzy Azure web app i przekazać pliki z katalogiem lokalnym za pomocą protokołu FTP.</span><span class="sxs-lookup"><span data-stu-id="c73a2-111">Creates an Azure web app and upload files from a local directory using FTP.</span></span> |
| [<span data-ttu-id="c73a2-112">Tworzenie aplikacji sieci Web i wdrażanie kodu z lokalnego repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="c73a2-112">Create a web app and deploy code from a local Git repository</span></span>](./scripts/app-service-powershell-deploy-local-git.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="c73a2-113">Tworzenie aplikacji sieci web platformy Azure i konfiguruje wypychania kodu z lokalnego repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="c73a2-113">Creates an Azure web app and configures code push from a local Git repository.</span></span> |
| [<span data-ttu-id="c73a2-114">Tworzenie aplikacji sieci Web i wdrażanie kodu w środowisku przejściowym</span><span class="sxs-lookup"><span data-stu-id="c73a2-114">Create a web app and deploy code to a staging environment</span></span>](./scripts/app-service-powershell-deploy-staging-environment.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="c73a2-115">Tworzy aplikację sieci web platformy Azure z miejscem wdrożenia, do przemieszczania zmian w kodzie.</span><span class="sxs-lookup"><span data-stu-id="c73a2-115">Creates an Azure web app with a deployment slot for staging code changes.</span></span> |
|<span data-ttu-id="c73a2-116">**Konfigurowanie aplikacji**</span><span class="sxs-lookup"><span data-stu-id="c73a2-116">**Configure app**</span></span>||
| [<span data-ttu-id="c73a2-117">Mapowanie domeny niestandardowej na aplikację sieci Web</span><span class="sxs-lookup"><span data-stu-id="c73a2-117">Map a custom domain to a web app</span></span>](./scripts/app-service-powershell-configure-custom-domain.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="c73a2-118">Tworzenie aplikacji sieci web platformy Azure i mapuje niestandardowej nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="c73a2-118">Creates an Azure web app and maps a custom domain name to it.</span></span> |
| [<span data-ttu-id="c73a2-119">Wiązania niestandardowego certyfikatu SSL w aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="c73a2-119">Bind a custom SSL certificate to a web app</span></span>](./scripts/app-service-powershell-configure-ssl-certificate.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="c73a2-120">Tworzenie aplikacji sieci web platformy Azure i wiąże certyfikatu SSL z niestandardowej nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="c73a2-120">Creates an Azure web app and binds the SSL certificate of a custom domain name to it.</span></span> |
|<span data-ttu-id="c73a2-121">**Skalowanie aplikacji**</span><span class="sxs-lookup"><span data-stu-id="c73a2-121">**Scale app**</span></span>||
| [<span data-ttu-id="c73a2-122">Ręczne skalowanie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="c73a2-122">Scale a web app manually</span></span>](./scripts/app-service-powershell-scale-manual.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="c73a2-123">Tworzenie aplikacji sieci web platformy Azure i skaluje go w wystąpieniach 2.</span><span class="sxs-lookup"><span data-stu-id="c73a2-123">Creates an Azure web app and scales it across 2 instances.</span></span> |
| [<span data-ttu-id="c73a2-124">Skalowanie aplikacji sieci Web na całym świecie przy użyciu architektury wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="c73a2-124">Scale a web app worldwide with a high-availability architecture</span></span>](./scripts/app-service-powershell-scale-high-availability.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="c73a2-125">Tworzy dwie aplikacje sieci web platformy Azure w dwóch różnych regionach geograficznych i udostępnia je poprzez jeden punkt końcowy za pomocą usługi Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="c73a2-125">Creates two Azure web apps in two different geographical regions and makes them available through a single endpoint using Azure Traffic Manager.</span></span> |
|<span data-ttu-id="c73a2-126">**Łączenie aplikacji z zasobów**</span><span class="sxs-lookup"><span data-stu-id="c73a2-126">**Connect app to resources**</span></span>||
| [<span data-ttu-id="c73a2-127">Łączenie aplikacji sieci web z bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="c73a2-127">Connect a web app to a SQL Database</span></span>](./scripts/app-service-powershell-connect-to-sql.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="c73a2-128">Tworzy aplikację sieci web platformy Azure i bazy danych SQL, a następnie dodaje parametry połączenia bazy danych do ustawień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c73a2-128">Creates an Azure web app and a SQL database, then adds the database connection string to the app settings.</span></span> |
| [<span data-ttu-id="c73a2-129">Łączenie aplikacji sieci Web z kontem magazynu</span><span class="sxs-lookup"><span data-stu-id="c73a2-129">Connect a web app to a storage account</span></span>](./scripts/app-service-powershell-connect-to-storage.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="c73a2-130">Tworzy aplikację sieci web platformy Azure i konto magazynu, a następnie dodaje parametry połączenia magazynu do ustawień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c73a2-130">Creates an Azure web app and a storage account, then adds the storage connection string to the app settings.</span></span> |
|<span data-ttu-id="c73a2-131">**Monitoruj aplikację**</span><span class="sxs-lookup"><span data-stu-id="c73a2-131">**Monitor app**</span></span>||
| [<span data-ttu-id="c73a2-132">Monitorowanie aplikacji sieci Web za pomocą dzienników serwera sieci Web</span><span class="sxs-lookup"><span data-stu-id="c73a2-132">Monitor a web app with web server logs</span></span>](./scripts/app-service-powershell-monitor.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="c73a2-133">Tworzenie aplikacji sieci web platformy Azure, włączenie rejestrowania dla niego i pobiera dzienniki na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="c73a2-133">Creates an Azure web app, enables logging for it, and downloads the logs to your local machine.</span></span> |
| | |
