---
title: "aaaGet wprowadzenie do usługi Azure App Service Mobile Apps dla aplikacji Xamarin.iOS | Dokumentacja firmy Microsoft"
description: "Postępuj zgodnie z tego samouczka tooget wprowadzenie używanie Mobile Apps do tworzenia aplikacji platformy Xamarin.iOS."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 14428794-52ad-4b51-956c-deb296cafa34
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: syntaxc4
ms.openlocfilehash: 524c5ac4d8a29d7cb858f74132aad5d6e2201d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinios-app"></a><span data-ttu-id="a6af4-103">Tworzenie aplikacji platformy Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="a6af4-103">Create a Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="a6af4-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="a6af4-104">Overview</span></span>
<span data-ttu-id="a6af4-105">Ten samouczek pokazuje, jak tooadd wewnętrznej bazy danych opartej na chmurze usługi tooa aplikacji mobilnej platformy Xamarin.iOS przy użyciu zaplecza aplikacji mobilnej Azure.</span><span class="sxs-lookup"><span data-stu-id="a6af4-105">This tutorial shows you how tooadd a cloud-based backend service tooa Xamarin.iOS mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="a6af4-106">Utworzysz zaplecze nowej aplikacji mobilnej oraz prostą aplikację platformy Xamarin.iOS typu *Lista czynności do wykonania*, która przechowuje dane aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a6af4-106">You create both a new mobile app backend and a simple *Todo list* Xamarin.iOS app that stores app data in Azure.</span></span>

<span data-ttu-id="a6af4-107">Wykonanie kroków tego samouczka jest wymaganiem wstępnym dla wszystkich innych samouczków Xamarin.iOS dotyczących używania funkcji Mobile Apps hello w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="a6af4-107">Completing this tutorial is a prerequisite for all other Xamarin.iOS tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6af4-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a6af4-108">Prerequisites</span></span>
<span data-ttu-id="a6af4-109">toocomplete tego samouczka należy hello następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="a6af4-109">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="a6af4-110">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a6af4-110">An active Azure account.</span></span> <span data-ttu-id="a6af4-111">Jeśli nie masz konta, należy utworzyć konto wersji próbnej platformy Azure i Uzyskaj too10 bezpłatnych aplikacji mobilnych, które możesz korzystać nawet po próbnej.</span><span class="sxs-lookup"><span data-stu-id="a6af4-111">If you don't have an account, sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="a6af4-112">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a6af4-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a6af4-113">Visual Studio z programem Xamarin.</span><span class="sxs-lookup"><span data-stu-id="a6af4-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="a6af4-114">Instrukcje można znaleźć w temacie [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) (Konfigurowanie i instalowanie dla programów Visual Studio i Xamarin).</span><span class="sxs-lookup"><span data-stu-id="a6af4-114">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>
* <span data-ttu-id="a6af4-115">Komputer Mac z zainstalowanym środowiskiem Xcode v7.0 lub nowszym i rozwiązaniem Xamarin Studio Community.</span><span class="sxs-lookup"><span data-stu-id="a6af4-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="a6af4-116">Zobacz tematy [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) (Konfigurowanie i instalowanie dla programów Visual Studio i Xamarin) oraz [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (Konfigurowanie, instalowanie oraz weryfikacje dla użytkowników komputerów Mac) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="a6af4-116">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="a6af4-117">Tworzenie zaplecza Aplikacji mobilnej Azure</span><span class="sxs-lookup"><span data-stu-id="a6af4-117">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="a6af4-118">Wykonaj te kroki toocreate zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="a6af4-118">Follow these steps toocreate a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a><span data-ttu-id="a6af4-119">Konfigurowanie projektu serwera hello</span><span class="sxs-lookup"><span data-stu-id="a6af4-119">Configure hello server project</span></span>
<span data-ttu-id="a6af4-120">W ten sposób zainicjowano obsługę zaplecza Aplikacji mobilnej Azure, które może być używane przez aplikacje mobilne klientów.</span><span class="sxs-lookup"><span data-stu-id="a6af4-120">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="a6af4-121">Następnie należy pobrać Projekt serwera dla prostego "Lista czynności do wykonania" wewnętrznej bazy danych i opublikuj go tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a6af4-121">Next, download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

<span data-ttu-id="a6af4-122">Wykonaj następujące kroki tooconfigure powitania serwera projektu toouse hello albo hello zaplecza Node.js lub .NET.</span><span class="sxs-lookup"><span data-stu-id="a6af4-122">Follow hello following steps tooconfigure hello server project toouse either hello Node.js or .NET backend.</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinios-app"></a><span data-ttu-id="a6af4-123">Pobieranie i uruchamianie aplikacji platformy Xamarin.iOS hello</span><span class="sxs-lookup"><span data-stu-id="a6af4-123">Download and run hello Xamarin.iOS app</span></span>
1. <span data-ttu-id="a6af4-124">Otwórz hello [portalu Azure] w oknie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="a6af4-124">Open hello [Azure portal] in a browser window.</span></span>
2. <span data-ttu-id="a6af4-125">W bloku ustawień hello aplikacji mobilnej kliknij **wprowadzenie** > **Xamarin.iOS**.</span><span class="sxs-lookup"><span data-stu-id="a6af4-125">On hello settings blade for your Mobile App, click **Get Started** > **Xamarin.iOS**.</span></span> <span data-ttu-id="a6af4-126">W kroku 3 kliknij pozycję **Utwórz nową aplikację**, jeśli nie została jeszcze wybrana.</span><span class="sxs-lookup"><span data-stu-id="a6af4-126">Under step 3, click **Create a new app** if it's not already selected.</span></span>  <span data-ttu-id="a6af4-127">Następnie kliknij przycisk hello **Pobierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a6af4-127">Next click hello **Download** button.</span></span>

      <span data-ttu-id="a6af4-128">Aplikacji klienckiej, która łączy tooyour zaplecze aplikacji mobilnej zostanie pobrana.</span><span class="sxs-lookup"><span data-stu-id="a6af4-128">A client application that connects tooyour mobile backend is downloaded.</span></span> <span data-ttu-id="a6af4-129">Zapisz hello skompresowany plik projektu na komputerze lokalnym i Zapamiętaj miejsce jego zapisania.</span><span class="sxs-lookup"><span data-stu-id="a6af4-129">Save hello compressed project file to your local computer, and make a note of where you save it.</span></span>
3. <span data-ttu-id="a6af4-130">Wyodrębnij pobrany projekt hello, a następnie otwórz go w programie Xamarin Studio (lub programu Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="a6af4-130">Extract hello project that you downloaded, and then open it in Xamarin Studio (or Visual Studio).</span></span>

    ![][9]

    ![][8]
4. <span data-ttu-id="a6af4-131">Naciśnij hello F5 klucza toobuild hello projekt i uruchomić aplikacji hello w emulatorze urządzenia iPhone hello.</span><span class="sxs-lookup"><span data-stu-id="a6af4-131">Press hello F5 key toobuild hello project and start hello app in hello iPhone emulator.</span></span>
5. <span data-ttu-id="a6af4-132">W aplikacji hello wpisz znaczący tekst, na przykład *Poznaj program Xamarin*, a następnie kliknij przycisk hello ** + ** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a6af4-132">In hello app, type meaningful text, such as *Learn Xamarin*, and then click hello **+** button.</span></span>

    ![][10]

    <span data-ttu-id="a6af4-133">Dane z hello żądania zostaną wstawione do tabeli TodoItem hello.</span><span class="sxs-lookup"><span data-stu-id="a6af4-133">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="a6af4-134">Elementy przechowywane w tabeli hello są zwracane przez zaplecze aplikacji mobilnej hello, a dane są wyświetlane na liście hello.</span><span class="sxs-lookup"><span data-stu-id="a6af4-134">Items stored in hello table are returned by hello mobile app backend, and the data is displayed in hello list.</span></span>

> [!NOTE]
> <span data-ttu-id="a6af4-135">Można sprawdzić hello kod, który uzyskuje dostęp do Twojej aplikacji mobilnej tooquery wewnętrznej bazy danych i wstawianie danych w pliku C# QSTodoService.cs hello.</span><span class="sxs-lookup"><span data-stu-id="a6af4-135">You can review hello code that accesses your mobile app backend tooquery and insert data in hello QSTodoService.cs C# file.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="a6af4-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a6af4-136">Next steps</span></span>
* [<span data-ttu-id="a6af4-137">Dodaj aplikację tooyour synchronizacji w trybie Offline</span><span class="sxs-lookup"><span data-stu-id="a6af4-137">Add Offline Sync tooyour app</span></span>](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [<span data-ttu-id="a6af4-138">Dodaj aplikację tooyour uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="a6af4-138">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-ios-get-started-users.md)
* [<span data-ttu-id="a6af4-139">Dodawanie aplikacji platformy Xamarin.Android tooyour powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="a6af4-139">Add push notifications tooyour Xamarin.Android app</span></span>](app-service-mobile-xamarin-ios-get-started-push.md)
* [<span data-ttu-id="a6af4-140">Jak toouse hello zarządzanego klienta usługi Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="a6af4-140">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Anchors. -->
[Getting started with mobile app backends]:#getting-started
[Create a new mobile app backend]:#create-new-service
[Next Steps]:#next-steps

<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-ios-get-started/xamarin-ios-quickstart.png
[8]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-vs.png
[9]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-xs.png
[10]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-quickstart-startup-ios.png

<!-- URLs. -->
[Witryna Azure Portal]: https://portal.azure.com/
