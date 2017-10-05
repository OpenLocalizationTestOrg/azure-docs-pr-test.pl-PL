---
title: "Tworzenie aplikacji systemu iOS przy użyciu funkcji Azure App Service Mobile Apps| Microsoft Docs"
description: "Postępuj zgodnie z tym samouczkiem, aby rozpocząć korzystanie z zapleczy usług mobilnych Azure na potrzeby opracowywania aplikacji systemu iOS w środowisku Objective-C lub Swift."
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 6461a899-9340-42dd-b118-ffc5ba00e846
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 36936ae66c458fcbedeec95cfa2f573a40c8af53
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-ios-app"></a><span data-ttu-id="bf746-103">Tworzenie aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="bf746-103">Create an iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="bf746-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="bf746-104">Overview</span></span>
<span data-ttu-id="bf746-105">W tym samouczku przedstawiono sposób dodawania [Azure Mobile Apps](app-service-mobile-value-prop.md), usługi zaplecza w chmurze, do aplikacji systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="bf746-105">This tutorial shows how to add [Azure Mobile Apps](app-service-mobile-value-prop.md), a cloud backend service, to an iOS app.</span></span> <span data-ttu-id="bf746-106">Najpierw utworzymy nowe zaplecze aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="bf746-106">We'll first create a new mobile backend.</span></span> <span data-ttu-id="bf746-107">Następnie użyjemy prostej aplikacji systemu iOS typu *Lista czynności do wykonania* do przechowywania danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="bf746-107">Then, we'll use a simple *Todo list* iOS app to store data in Azure.</span></span>

<span data-ttu-id="bf746-108">Aby można było ukończyć ten samouczek, potrzebny jest komputer Mac i [konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="bf746-108">To complete this tutorial, you need a Mac and [an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>

## <a name="step-i-create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="bf746-109">Krok I. Tworzenie nowego zaplecza aplikacji mobilnej Azure</span><span class="sxs-lookup"><span data-stu-id="bf746-109">Step I: Create a new Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="step-ii-configure-the-backend-project"></a><span data-ttu-id="bf746-110">Krok II. Konfigurowanie projektu zaplecza</span><span class="sxs-lookup"><span data-stu-id="bf746-110">Step II: Configure the backend project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="step-iii-download-and-run-the-ios-app"></a><span data-ttu-id="bf746-111">Krok III. Pobieranie i uruchamianie aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="bf746-111">Step III: Download and run the iOS app</span></span>
[!INCLUDE [app-service-mobile-ios-run-app](../../includes/app-service-mobile-ios-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203
