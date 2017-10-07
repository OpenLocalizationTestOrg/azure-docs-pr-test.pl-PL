---
title: "aaaCreate aplikacji systemu Android w usłudze Azure App Service Mobile Apps | Dokumentacja firmy Microsoft"
description: "Postępuj zgodnie z tego samouczka tooget korzystanie z zapleczy zapleczy aplikacji mobilnych Azure dla systemu Android."
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
ms.openlocfilehash: 0af85a3a4de9fc265976bbe3f34d73effc3807df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-android-app"></a><span data-ttu-id="1f384-103">Tworzenie aplikacji systemu Android</span><span class="sxs-lookup"><span data-stu-id="1f384-103">Create an Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="1f384-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="1f384-104">Overview</span></span>
<span data-ttu-id="1f384-105">Ten samouczek pokazuje, jak tooadd wewnętrznej bazy danych opartej na chmurze usługi tooan aplikacji mobilnej systemu Android przy użyciu zaplecza aplikacji mobilnej Azure.</span><span class="sxs-lookup"><span data-stu-id="1f384-105">This tutorial shows you how tooadd a cloud-based backend service tooan Android mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="1f384-106">Będziesz tworzyć nowe zaplecze aplikacji mobilnej oraz prostą aplikację systemu Android typu *Lista czynności do wykonania*, która przechowuje dane aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="1f384-106">You will create both a new mobile app backend and a simple *Todo list* Android app that stores app data in Azure.</span></span>

<span data-ttu-id="1f384-107">Wykonanie kroków tego samouczka jest wymaganiem wstępnym dla wszystkich innych samouczków dla systemu Android dotyczących używania funkcji Mobile Apps hello w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="1f384-107">Completing this tutorial is a prerequisite for all other Android tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f384-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1f384-108">Prerequisites</span></span>
<span data-ttu-id="1f384-109">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="1f384-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="1f384-110">[Narzędzia dla deweloperów systemu android](https://developer.android.com/sdk/index.html), w tym hello Android Studio zintegrowane środowisko programistyczne oraz najnowszej platformy Android hello.</span><span class="sxs-lookup"><span data-stu-id="1f384-110">[Android Developer Tools](https://developer.android.com/sdk/index.html), which includes hello Android Studio integrated development environment, and hello latest Android platform.</span></span>
* <span data-ttu-id="1f384-111">Azure Mobile Android SDK, która jest automatycznie używany jako część hello pobieranego projektu szybkiego startu możesz pobrać.</span><span class="sxs-lookup"><span data-stu-id="1f384-111">Azure Mobile Android SDK, which is automatically referenced as part of hello quickstart project you download.</span></span>
* <span data-ttu-id="1f384-112">[Aktywne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1f384-112">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="1f384-113">Tworzenie zaplecza nowej aplikacji mobilnej Azure</span><span class="sxs-lookup"><span data-stu-id="1f384-113">Create a new Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a><span data-ttu-id="1f384-114">Konfigurowanie projektu serwera hello</span><span class="sxs-lookup"><span data-stu-id="1f384-114">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-android-app"></a><span data-ttu-id="1f384-115">Pobieranie i uruchamianie aplikacji systemu Android hello</span><span class="sxs-lookup"><span data-stu-id="1f384-115">Download and run hello Android app</span></span>
[!INCLUDE [app-service-mobile-android-run-app](../../includes/app-service-mobile-android-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203
