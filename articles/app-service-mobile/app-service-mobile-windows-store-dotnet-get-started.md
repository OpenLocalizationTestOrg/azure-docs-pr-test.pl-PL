---
title: "Tworzenie aplikacji platformy uniwersalnej systemu Windows korzystającej z usługi Mobile Apps | Microsoft Docs"
description: "Wykonaj kroki opisane w tym samouczku, aby rozpocząć używanie zapleczy aplikacji mobilnych Azure na potrzeby tworzenia aplikacji platformy uniwersalnej systemu Windows w języku C#, Visual Basic lub JavaScript."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 47124296-2908-4d92-85e0-05c4aa6db916
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5408e032670dda7f149c442e08f52b02abe23f05
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-windows-app"></a><span data-ttu-id="8292a-103">Tworzenie aplikacji systemu Windows</span><span class="sxs-lookup"><span data-stu-id="8292a-103">Create a Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="8292a-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="8292a-104">Overview</span></span>
<span data-ttu-id="8292a-105">W tym samouczku przedstawiono sposób dodawania usługi zaplecza opartej na chmurze do aplikacji platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="8292a-105">This tutorial shows you how to add a cloud-based backend service to a Universal Windows Platform (UWP) app.</span></span> <span data-ttu-id="8292a-106">Aby uzyskać więcej informacji, zobacz artykuł [Co to jest usługa Mobile Apps](app-service-mobile-value-prop.md).</span><span class="sxs-lookup"><span data-stu-id="8292a-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span> <span data-ttu-id="8292a-107">Poniżej przedstawiono ekrany przechwycone z ukończonej aplikacji:</span><span class="sxs-lookup"><span data-stu-id="8292a-107">The following are screen captures from the completed app:</span></span>

![Ukończona aplikacja klasyczna](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
<span data-ttu-id="8292a-109">Uruchamianie na komputerze</span><span class="sxs-lookup"><span data-stu-id="8292a-109">Running on a desktop.</span></span>

![Ukończona aplikacja na telefon](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
<span data-ttu-id="8292a-111">Uruchamianie na telefonie</span><span class="sxs-lookup"><span data-stu-id="8292a-111">Running on a phone</span></span>

<span data-ttu-id="8292a-112">Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków Aplikacji mobilnych dotyczących aplikacji platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="8292a-112">Completing this tutorial is a prerequisite for all other Mobile App tutorials for UWP apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8292a-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8292a-113">Prerequisites</span></span>
<span data-ttu-id="8292a-114">Do wykonania kroków tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8292a-114">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="8292a-115">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8292a-115">An active Azure account.</span></span> <span data-ttu-id="8292a-116">Jeśli nie masz konta, możesz utworzyć konto wersji próbnej platformy Azure i uzyskać maksymalnie 10 bezpłatnych aplikacji mobilnych, z których możesz korzystać nawet po zakończeniu okresu ważności wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="8292a-116">If you don't have an account, you can sign up for an Azure trial and get up to 10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="8292a-117">Aby uzyskać szczegółowe informacje, zobacz temat [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/) (Bezpłatna wersja próbna platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="8292a-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8292a-118">Program [Visual Studio Community 2015] lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="8292a-118">[Visual Studio Community 2015] or a later version.</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="8292a-119">Tworzenie zaplecza nowej Aplikacji mobilnej Azure</span><span class="sxs-lookup"><span data-stu-id="8292a-119">Create a new Azure Mobile App backend</span></span>
<span data-ttu-id="8292a-120">Wykonaj te kroki, aby utworzyć zaplecze nowej Aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="8292a-120">Follow these steps to create a new Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="8292a-121">W ten sposób zainicjowano obsługę zaplecza Aplikacji mobilnej Azure, które może być używane przez aplikacje mobilne klientów.</span><span class="sxs-lookup"><span data-stu-id="8292a-121">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="8292a-122">Teraz pobierzesz projekt serwera dla prostego zaplecza typu „lista czynności do wykonania” i opublikujesz go na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="8292a-122">Next, you will download a server project for a simple "todo list" backend and publish it to Azure.</span></span>

## <a name="configure-the-server-project"></a><span data-ttu-id="8292a-123">Konfigurowanie projektu serwera</span><span class="sxs-lookup"><span data-stu-id="8292a-123">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-client-project"></a><span data-ttu-id="8292a-124">Pobieranie i uruchamianie projektu klienta</span><span class="sxs-lookup"><span data-stu-id="8292a-124">Download and run the client project</span></span>
<span data-ttu-id="8292a-125">Po skonfigurowaniu zaplecza Aplikacji mobilnej można utworzyć nową aplikację klienta lub zmodyfikować istniejącą aplikację w celu nawiązania połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="8292a-125">Once you have configured your Mobile App backend, you can either create a new client app or modify an existing app to connect to Azure.</span></span> <span data-ttu-id="8292a-126">W tej sekcji można pobrać projekt szablonu aplikacji platformy uniwersalnej systemu Windows zmodyfikowany pod kątem potrzeb nawiązywania połączenia z zapleczem Aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="8292a-126">In this section, you download a UWP app template project that is customized to connect to your Mobile App backend.</span></span>

1. <span data-ttu-id="8292a-127">W bloku **Szybki start** dla zaplecza Aplikacji mobilnej kliknij pozycję **Utwórz nową aplikację** > **Pobieranie**, a następnie wyodrębnij skompresowane pliki projektu na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="8292a-127">Back in the **Quick start** blade for your Mobile App backend, click **Create a new app** > **Download**, then extract the compressed project files to your local computer.</span></span>

    ![Pobieranie projektu Szybki start systemu Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. <span data-ttu-id="8292a-129">(Opcjonalnie) Dodaj projekt aplikacji platformy uniwersalnej systemu Windows do tego samego rozwiązania co projekt serwera.</span><span class="sxs-lookup"><span data-stu-id="8292a-129">(Optional) Add the UWP app project to the same solution as the server project.</span></span> <span data-ttu-id="8292a-130">Ułatwi to debugowanie oraz testowanie zaplecza i aplikacji w tym samym rozwiązaniu Visual Studio (jeśli chcesz to zrobić).</span><span class="sxs-lookup"><span data-stu-id="8292a-130">This makes it easier to debug and test both the app and the backend in the same Visual Studio solution, if you choose to do so.</span></span> <span data-ttu-id="8292a-131">Aby dodać projekt aplikacji platformy uniwersalnej systemu Windows do rozwiązania, musisz korzystać z programu Visual Studio 2015 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="8292a-131">To add a UWP app project to the solution, you must be using Visual Studio 2015 or a later version.</span></span>
3. <span data-ttu-id="8292a-132">Z aplikacją platformy uniwersalnej systemu Windows jako projektem startowym naciśnij klawisz F5, aby wdrożyć i uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="8292a-132">With the UWP app as the startup project, press the F5 key to deploy and run the app.</span></span>
4. <span data-ttu-id="8292a-133">W aplikacji wpisz znaczący tekst, na przykład *Ukończ samouczek* w polu tekstowym **Wstaw czynność do wykonania**, a następnie kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="8292a-133">In the app, type meaningful text, such as *Complete the tutorial*, in the **Insert a TodoItem** text box, and then click **Save**.</span></span>

    ![Kompletna aplikacja systemu Windows typu Szybki start na komputerze](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    <span data-ttu-id="8292a-135">Spowoduje to wysłanie żądania POST do zaplecza nowej aplikacji mobilnej, która jest obsługiwana na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="8292a-135">This sends a POST request to the new mobile app backend that's hosted in Azure.</span></span>
5. <span data-ttu-id="8292a-136">(Opcjonalnie) Zatrzymaj aplikację i uruchom ją ponownie na innym urządzeniu lub w emulatorze aplikacji mobilnych.</span><span class="sxs-lookup"><span data-stu-id="8292a-136">(Optional) Stop the app and restart it on a different device or mobile emulator.</span></span>

    ![Kompletna aplikacja systemu Windows typu Szybki start na telefonie](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    <span data-ttu-id="8292a-138">Zauważ, że dane zapisane w poprzednim kroku są ładowane z platformy Azure po uruchomieniu aplikacji platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="8292a-138">Notice that data saved from the previous step is loaded from Azure after the UWP app starts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8292a-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8292a-139">Next steps</span></span>
* [<span data-ttu-id="8292a-140">Dodawanie uwierzytelniania do aplikacji</span><span class="sxs-lookup"><span data-stu-id="8292a-140">Add authentication to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="8292a-141">Dowiedz się, jak uwierzytelniać użytkowników aplikacji przy użyciu dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="8292a-141">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="8292a-142">Dodawanie powiadomień wypychanych do aplikacji</span><span class="sxs-lookup"><span data-stu-id="8292a-142">Add push notifications to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="8292a-143">Dowiedz się, jak dodać obsługę powiadomień wypychanych do aplikacji i skonfigurować zaplecze Aplikacji mobilnej na potrzeby wysyłania powiadomień wypychanych przy użyciu usługi Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="8292a-143">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="8292a-144">Włączanie synchronizacji w trybie offline dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="8292a-144">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="8292a-145">Dowiedz się, jak dodać obsługę aplikacji w trybie offline przy użyciu zaplecza Aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="8292a-145">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="8292a-146">Synchronizacja w trybie offline umożliwia użytkownikom końcowym interakcję z aplikacją mobilną &mdash; przeglądanie, dodawanie lub modyfikowanie danych &mdash; nawet w przypadku braku połączenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="8292a-146">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
<span data-ttu-id="8292a-147">[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203</span><span class="sxs-lookup"><span data-stu-id="8292a-147">[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203</span></span>
