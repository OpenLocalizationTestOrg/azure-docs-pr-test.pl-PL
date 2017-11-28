---
title: aaaCreate Windows platformy Uniwersalnej na Mobile Apps | Dokumentacja firmy Microsoft
description: "Postępuj zgodnie z tego samouczka tooget wprowadzenie używanie zapleczy aplikacji mobilnych Azure do tworzenia aplikacji uniwersalnych platformy systemu Windows (UWP) w języku C#, Visual Basic lub JavaScript."
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
ms.openlocfilehash: d0f57bca5a8195b8b0461b8f7a0d8516371d56a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-app"></a><span data-ttu-id="89278-103">Tworzenie aplikacji systemu Windows</span><span class="sxs-lookup"><span data-stu-id="89278-103">Create a Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="89278-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="89278-104">Overview</span></span>
<span data-ttu-id="89278-105">Ten samouczek pokazuje, jak tooadd wewnętrznej bazy danych opartej na chmurze usługi tooa Windows platformy Uniwersalnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="89278-105">This tutorial shows you how tooadd a cloud-based backend service tooa Universal Windows Platform (UWP) app.</span></span> <span data-ttu-id="89278-106">Aby uzyskać więcej informacji, zobacz artykuł [Co to jest usługa Mobile Apps](app-service-mobile-value-prop.md).</span><span class="sxs-lookup"><span data-stu-id="89278-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span> <span data-ttu-id="89278-107">następujące Hello to przechwytywaniu zawartości ekranu aplikacji hello zakończone:</span><span class="sxs-lookup"><span data-stu-id="89278-107">hello following are screen captures from hello completed app:</span></span>

![Ukończona aplikacja klasyczna](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
<span data-ttu-id="89278-109">Uruchamianie na komputerze</span><span class="sxs-lookup"><span data-stu-id="89278-109">Running on a desktop.</span></span>

![Ukończona aplikacja na telefon](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
<span data-ttu-id="89278-111">Uruchamianie na telefonie</span><span class="sxs-lookup"><span data-stu-id="89278-111">Running on a phone</span></span>

<span data-ttu-id="89278-112">Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków Aplikacji mobilnych dotyczących aplikacji platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="89278-112">Completing this tutorial is a prerequisite for all other Mobile App tutorials for UWP apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89278-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="89278-113">Prerequisites</span></span>
<span data-ttu-id="89278-114">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="89278-114">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="89278-115">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="89278-115">An active Azure account.</span></span> <span data-ttu-id="89278-116">Jeśli nie masz konta, możesz utworzyć konto wersji próbnej platformy Azure i Uzyskaj too10 bezpłatnych aplikacji mobilnych, które możesz korzystać nawet po próbnej.</span><span class="sxs-lookup"><span data-stu-id="89278-116">If you don't have an account, you can sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="89278-117">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="89278-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="89278-118">Program [Visual Studio Community 2015] lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="89278-118">[Visual Studio Community 2015] or a later version.</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="89278-119">Tworzenie zaplecza nowej Aplikacji mobilnej Azure</span><span class="sxs-lookup"><span data-stu-id="89278-119">Create a new Azure Mobile App backend</span></span>
<span data-ttu-id="89278-120">Wykonaj te kroki toocreate nowego zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="89278-120">Follow these steps toocreate a new Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="89278-121">W ten sposób zainicjowano obsługę zaplecza Aplikacji mobilnej Azure, które może być używane przez aplikacje mobilne klientów.</span><span class="sxs-lookup"><span data-stu-id="89278-121">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="89278-122">Następnie pobierzesz Projekt serwera dla prostego "Lista czynności do wykonania" wewnętrznej bazy danych i opublikuj go tooAzure.</span><span class="sxs-lookup"><span data-stu-id="89278-122">Next, you will download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="89278-123">Konfigurowanie projektu serwera hello</span><span class="sxs-lookup"><span data-stu-id="89278-123">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-client-project"></a><span data-ttu-id="89278-124">Pobieranie i uruchamianie projektu klienta hello</span><span class="sxs-lookup"><span data-stu-id="89278-124">Download and run hello client project</span></span>
<span data-ttu-id="89278-125">Po skonfigurowaniu zaplecza aplikacji mobilnej, możesz utworzyć nową aplikację klienta lub zmodyfikować istniejącą tooAzure tooconnect aplikacji.</span><span class="sxs-lookup"><span data-stu-id="89278-125">Once you have configured your Mobile App backend, you can either create a new client app or modify an existing app tooconnect tooAzure.</span></span> <span data-ttu-id="89278-126">W tej sekcji możesz pobrać projekt szablonu aplikacji platformy uniwersalnej systemu Windows jest zaplecza aplikacji mobilnej tooyour tooconnect dostosowane.</span><span class="sxs-lookup"><span data-stu-id="89278-126">In this section, you download a UWP app template project that is customized tooconnect tooyour Mobile App backend.</span></span>

1. <span data-ttu-id="89278-127">Po powrocie do hello **szybki start** bloku dla zaplecza aplikacji mobilnej, kliknij przycisk **Utwórz nową aplikację** > **Pobierz**, następnie wyodrębnić hello skompresowane pliki projektu tooyour komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="89278-127">Back in hello **Quick start** blade for your Mobile App backend, click **Create a new app** > **Download**, then extract hello compressed project files tooyour local computer.</span></span>

    ![Pobieranie projektu Szybki start systemu Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. <span data-ttu-id="89278-129">(Opcjonalnie) Dodaj toohello projekt aplikacji platformy uniwersalnej systemu Windows hello samego rozwiązania co projekt serwera hello.</span><span class="sxs-lookup"><span data-stu-id="89278-129">(Optional) Add hello UWP app project toohello same solution as hello server project.</span></span> <span data-ttu-id="89278-130">To ułatwia toodebug testu zarówno hello wewnętrznej bazy danych i aplikacji hello w hello tym samym rozwiązaniu Visual Studio, jeśli wybierzesz toodo, dlatego.</span><span class="sxs-lookup"><span data-stu-id="89278-130">This makes it easier toodebug and test both hello app and hello backend in hello same Visual Studio solution, if you choose toodo so.</span></span> <span data-ttu-id="89278-131">tooadd rozwiązania toohello projekt aplikacji platformy uniwersalnej systemu Windows, musisz korzystać z programu Visual Studio 2015 lub nowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="89278-131">tooadd a UWP app project toohello solution, you must be using Visual Studio 2015 or a later version.</span></span>
3. <span data-ttu-id="89278-132">Z aplikacją platformy uniwersalnej systemu Windows hello jako projekt startowy hello naciśnij klawisz toodeploy klucza F5 hello i hello uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="89278-132">With hello UWP app as hello startup project, press hello F5 key toodeploy and run hello app.</span></span>
4. <span data-ttu-id="89278-133">W aplikacji hello wpisz znaczący tekst, na przykład *hello ukończenia samouczka*, w hello **Wstaw czynność do wykonania** polu tekstowym, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="89278-133">In hello app, type meaningful text, such as *Complete hello tutorial*, in hello **Insert a TodoItem** text box, and then click **Save**.</span></span>

    ![Kompletna aplikacja systemu Windows typu Szybki start na komputerze](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    <span data-ttu-id="89278-135">To wysyła POST żądania toohello nowe zaplecze aplikacji mobilnej hostowanej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="89278-135">This sends a POST request toohello new mobile app backend that's hosted in Azure.</span></span>
5. <span data-ttu-id="89278-136">(Opcjonalnie) Zatrzymaj aplikacji hello i uruchom go ponownie na innym urządzeniu lub emulatorze przenośnym.</span><span class="sxs-lookup"><span data-stu-id="89278-136">(Optional) Stop hello app and restart it on a different device or mobile emulator.</span></span>

    ![Kompletna aplikacja systemu Windows typu Szybki start na telefonie](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    <span data-ttu-id="89278-138">Zwróć uwagę, że dane zapisane hello w poprzednim kroku są ładowane z platformy Azure, po uruchomieniu aplikacji platformy uniwersalnej systemu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="89278-138">Notice that data saved from hello previous step is loaded from Azure after hello UWP app starts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89278-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="89278-139">Next steps</span></span>
* [<span data-ttu-id="89278-140">Dodaj aplikację tooyour uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="89278-140">Add authentication tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="89278-141">Dowiedz się, jak tooauthenticate użytkowników aplikacji przy użyciu dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="89278-141">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="89278-142">Dodaj aplikację tooyour powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="89278-142">Add push notifications tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="89278-143">Dowiedz się, jak powiadomień wypychanych tooadd obsługują tooyour aplikacji i Konfigurowanie powiadomień wypychanych toosend usługi Azure Notification Hubs toouse aplikacji mobilnej wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="89278-143">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="89278-144">Włączanie synchronizacji w trybie offline dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="89278-144">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="89278-145">Dowiedz się, jak w trybie offline tooadd obsługują aplikację przy użyciu zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="89278-145">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="89278-146">Synchronizacja w trybie offline umożliwia użytkownikom końcowym toointeract z aplikacją mobilną&mdash;przeglądanie, dodawanie lub modyfikowanie danych&mdash;nawet wtedy, gdy istnieje połączenie sieciowe.</span><span class="sxs-lookup"><span data-stu-id="89278-146">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203
