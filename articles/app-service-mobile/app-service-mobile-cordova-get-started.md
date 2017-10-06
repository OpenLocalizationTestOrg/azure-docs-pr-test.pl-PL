---
title: "aaaCreate aplikacji platformy Cordova w usłudze Azure App Service Mobile Apps | Dokumentacja firmy Microsoft"
description: "Postępuj zgodnie z tego samouczka tooget wprowadzenie do zapleczy aplikacji mobilnych Azure przy użyciu oprogramowania Apache cordova."
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
tags: 
keywords: cordova,javascript,mobile,client
ms.assetid: 0b08fc12-0a80-42d3-9cc1-9b3f8d3e3a3f
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: hero-article
ms.date: 07/07/2017
ms.author: glenga
ms.openlocfilehash: 4981cbc0686c15230019ac9f30495f30cbf2c791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-cordova-app"></a><span data-ttu-id="78adc-104">Tworzenie aplikacji oprogramowania Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="78adc-104">Create an Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="78adc-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="78adc-105">Overview</span></span>
<span data-ttu-id="78adc-106">Ten samouczek pokazuje, jak tooadd wewnętrznej bazy danych opartej na chmurze usługi aplikacji mobilnej oprogramowania Apache Cordova tooan przy użyciu zaplecza aplikacji mobilnej Azure.</span><span class="sxs-lookup"><span data-stu-id="78adc-106">This tutorial shows you how tooadd a cloud-based backend service tooan Apache Cordova mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="78adc-107">Utworzysz nowe zaplecze aplikacji mobilnej oraz prostą aplikację oprogramowania Apache Cordova typu *Lista czynności do wykonania*, która przechowuje dane aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="78adc-107">You create both a new mobile app backend and a simple *Todo list* Apache Cordova app that stores app data in Azure.</span></span>

<span data-ttu-id="78adc-108">Wykonanie kroków tego samouczka jest wymaganiem wstępnym dla wszystkich innych samouczków Apache Cordova dotyczących używania funkcji Mobile Apps hello w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="78adc-108">Completing this tutorial is a prerequisite for all other Apache Cordova tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78adc-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="78adc-109">Prerequisites</span></span>
<span data-ttu-id="78adc-110">toocomplete tego samouczka należy hello następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="78adc-110">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="78adc-111">Komputer z programem [Visual Studio Community 2017] lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="78adc-111">A PC with [Visual Studio Community 2017] or newer.</span></span>
* <span data-ttu-id="78adc-112">[Visual Studio Tools for Apache Cordova].</span><span class="sxs-lookup"><span data-stu-id="78adc-112">[Visual Studio Tools for Apache Cordova].</span></span>
* <span data-ttu-id="78adc-113">[Aktywne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="78adc-113">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="78adc-114">Można również pominąć program Visual Studio i używać bezpośrednio wiersza polecenia hello Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="78adc-114">You may also bypass Visual Studio and use hello Apache Cordova command line directly.</span></span>  <span data-ttu-id="78adc-115">Przy użyciu wiersza polecenia hello jest przydatne, gdy wykonanie kroków samouczka hello na komputerze Mac.</span><span class="sxs-lookup"><span data-stu-id="78adc-115">Using hello command line is useful when completing hello tutorial on a Mac computer.</span></span>  <span data-ttu-id="78adc-116">Kompilowanie aplikacji klienckich oprogramowania Apache Cordova za pomocą wiersza polecenia hello nie jest opisane w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="78adc-116">Compiling Apache Cordova client applications using hello command line is not covered by this tutorial.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="78adc-117">Tworzenie zaplecza aplikacji mobilnej Azure</span><span class="sxs-lookup"><span data-stu-id="78adc-117">Create an Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[<span data-ttu-id="78adc-118">Obejrzyj wideo przedstawiające podobne kroki</span><span class="sxs-lookup"><span data-stu-id="78adc-118">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-hello-server-project"></a><span data-ttu-id="78adc-119">Konfigurowanie projektu serwera hello</span><span class="sxs-lookup"><span data-stu-id="78adc-119">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-apache-cordova-app"></a><span data-ttu-id="78adc-120">Pobieranie i uruchamianie aplikacji oprogramowania Apache Cordova hello</span><span class="sxs-lookup"><span data-stu-id="78adc-120">Download and run hello Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a><span data-ttu-id="78adc-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="78adc-121">Next Steps</span></span>
<span data-ttu-id="78adc-122">Teraz, gdy ukończeniu tego samouczka szybkiego startu przejść tooone hello następujące samouczki:</span><span class="sxs-lookup"><span data-stu-id="78adc-122">Now that you completed this quick start tutorial, move on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="78adc-123">[Dodawanie danych w trybie Offline](app-service-mobile-cordova-get-started-offline-data.md) tooyour aplikacji oprogramowania Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="78adc-123">[Add Offline Data](app-service-mobile-cordova-get-started-offline-data.md) tooyour Apache Cordova app.</span></span>
* <span data-ttu-id="78adc-124">[Dodawanie uwierzytelniania](app-service-mobile-cordova-get-started-users.md) tooyour aplikacji oprogramowania Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="78adc-124">[Add Authentication](app-service-mobile-cordova-get-started-users.md) tooyour Apache Cordova app.</span></span>
* <span data-ttu-id="78adc-125">[Dodawanie powiadomień wypychanych](app-service-mobile-cordova-get-started-push.md) tooyour aplikacji oprogramowania Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="78adc-125">[Add Push Notifications](app-service-mobile-cordova-get-started-push.md) tooyour Apache Cordova app.</span></span>

<span data-ttu-id="78adc-126">Dowiedz się więcej na temat najważniejszych pojęć związanych z usługą Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="78adc-126">Learn more about key concepts with Azure App Service.</span></span>

* <span data-ttu-id="78adc-127">[Dane w trybie offline]</span><span class="sxs-lookup"><span data-stu-id="78adc-127">[Offline Data]</span></span>
* <span data-ttu-id="78adc-128">[Uwierzytelnianie]</span><span class="sxs-lookup"><span data-stu-id="78adc-128">[Authentication]</span></span>
* <span data-ttu-id="78adc-129">[Powiadomienia wypychane]</span><span class="sxs-lookup"><span data-stu-id="78adc-129">[Push Notifications]</span></span>

<span data-ttu-id="78adc-130">Dowiedz się, jak toouse hello zestawów SDK.</span><span class="sxs-lookup"><span data-stu-id="78adc-130">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="78adc-131">[Zestaw Apache Cordova SDK]</span><span class="sxs-lookup"><span data-stu-id="78adc-131">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="78adc-132">[Zestaw ASP.NET Server SDK]</span><span class="sxs-lookup"><span data-stu-id="78adc-132">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="78adc-133">[Zestaw Node.js Server SDK]</span><span class="sxs-lookup"><span data-stu-id="78adc-133">[Node.js Server SDK]</span></span>

<!-- Images. -->

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2017]: http://www.visualstudio.com/
[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Dane w trybie offline]: app-service-mobile-offline-data-sync.md
[Uwierzytelnianie]: app-service-mobile-auth.md
[Powiadomienia wypychane]: ../notification-hubs/notification-hubs-push-notification-overview.md
[Zestaw Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[Zestaw ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Zestaw Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
