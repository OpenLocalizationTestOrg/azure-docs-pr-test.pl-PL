---
title: "Tworzenie aplikacji systemu Android przy użyciu funkcji Azure App Service Mobile Apps | Microsoft Docs"
description: "Postępuj zgodnie z tym samouczkiem, aby rozpocząć korzystanie z zapleczy usług mobilnych Azure na potrzeby opracowywania aplikacji dla systemu Android."
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 355f0959-aa7f-472c-a6c7-9eecea3a34a9
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 418a5229a084d570bc6cab5925dbd8d30945a3c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-android-app"></a><span data-ttu-id="9b2ac-103">Tworzenie aplikacji systemu Android</span><span class="sxs-lookup"><span data-stu-id="9b2ac-103">Create an Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="9b2ac-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="9b2ac-104">Overview</span></span>
<span data-ttu-id="9b2ac-105">W tym samouczku przedstawiono sposób dodawania usługi zaplecza opartej na chmurze do aplikacji mobilnej systemu Android przy użyciu zaplecza aplikacji mobilnej Azure.</span><span class="sxs-lookup"><span data-stu-id="9b2ac-105">This tutorial shows you how to add a cloud-based backend service to an Android mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="9b2ac-106">Będziesz tworzyć nowe zaplecze aplikacji mobilnej oraz prostą aplikację systemu Android typu *Lista czynności do wykonania*, która przechowuje dane aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9b2ac-106">You will create both a new mobile app backend and a simple *Todo list* Android app that stores app data in Azure.</span></span>

<span data-ttu-id="9b2ac-107">Wykonanie kroków tego samouczka jest wymagane w przypadku wszystkich innych samouczków z zakresu systemu Android dotyczących używania funkcji Mobile Apps w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="9b2ac-107">Completing this tutorial is a prerequisite for all other Android tutorials about using the Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b2ac-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9b2ac-108">Prerequisites</span></span>
<span data-ttu-id="9b2ac-109">Do wykonania kroków tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9b2ac-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="9b2ac-110">[Narzędzia dla deweloperów systemu Android](https://developer.android.com/sdk/index.html), w tym zintegrowane środowisko projektowe Android Studio i najnowsza platforma systemu Android.</span><span class="sxs-lookup"><span data-stu-id="9b2ac-110">[Android Developer Tools](https://developer.android.com/sdk/index.html), which includes the Android Studio integrated development environment, and the latest Android platform.</span></span>
* <span data-ttu-id="9b2ac-111">Zestaw Azure Mobile Android SDK, który jest automatycznie używany jako część pobieranego projektu szybkiego startu.</span><span class="sxs-lookup"><span data-stu-id="9b2ac-111">Azure Mobile Android SDK, which is automatically referenced as part of the quickstart project you download.</span></span>
* <span data-ttu-id="9b2ac-112">[Aktywne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9b2ac-112">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="9b2ac-113">Tworzenie zaplecza nowej aplikacji mobilnej Azure</span><span class="sxs-lookup"><span data-stu-id="9b2ac-113">Create a new Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-the-server-project"></a><span data-ttu-id="9b2ac-114">Konfigurowanie projektu serwera</span><span class="sxs-lookup"><span data-stu-id="9b2ac-114">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-android-app"></a><span data-ttu-id="9b2ac-115">Pobieranie i uruchamianie aplikacji systemu Android</span><span class="sxs-lookup"><span data-stu-id="9b2ac-115">Download and run the Android app</span></span>
[!INCLUDE [app-service-mobile-android-run-app](../../includes/app-service-mobile-android-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203
