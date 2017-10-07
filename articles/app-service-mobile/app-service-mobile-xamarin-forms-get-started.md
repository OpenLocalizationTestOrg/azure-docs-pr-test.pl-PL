---
title: "aaaGet pracę z usługą Mobile Apps za pomocą platformy Xamarin.Forms"
description: "Postępuj zgodnie z tego samouczka toostart używanie Mobile Apps do tworzenia aplikacji platformy Xamarin.Forms"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 5e692220-cc89-4548-96c8-35259722acf5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: af6b1c1ce4cf91c397552aa3d8ee40728129238c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinforms-app"></a><span data-ttu-id="9cf4d-103">Tworzenie aplikacji platformy Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="9cf4d-103">Create a Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="9cf4d-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="9cf4d-104">Overview</span></span>
<span data-ttu-id="9cf4d-105">Ten samouczek pokazuje, jak tooadd oparte na chmurze usługi zaplecza tooa aplikacji mobilnej platformy Xamarin.Forms przy użyciu hello funkcji Mobile Apps Azure App Service jako hello zaplecza.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-105">This tutorial shows you how tooadd a cloud-based back-end service tooa Xamarin.Forms mobile app by using hello Mobile Apps feature of Azure App Service as hello back end.</span></span> <span data-ttu-id="9cf4d-106">Tworzysz nowe zaplecze funkcji Mobile Apps oraz prostą aplikację platformy Xamarin.Forms typu Lista czynności do wykonania, która przechowuje dane aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-106">You create both a new Mobile Apps back end and a simple to-do list Xamarin.Forms app that stores app data in Azure.</span></span>

<span data-ttu-id="9cf4d-107">Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usługi Mobile Apps dotyczących aplikacji platformy Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-107">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Forms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cf4d-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9cf4d-108">Prerequisites</span></span>
<span data-ttu-id="9cf4d-109">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="9cf4d-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="9cf4d-110">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-110">An active Azure account.</span></span> <span data-ttu-id="9cf4d-111">Jeśli nie masz konta, możesz utworzyć konto wersji próbnej platformy Azure i Uzyskaj too10 bezpłatnych aplikacji mobilnych, które możesz korzystać nawet po próbnej.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-111">If you don't have an account, you can sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="9cf4d-112">Aby uzyskać więcej informacji, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9cf4d-112">For more information, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="9cf4d-113">Visual Studio z programem Xamarin.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="9cf4d-114">Aby uzyskać informacje, zobacz hello [ustawić Konfigurowanie i instalowanie programu Visual Studio i Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) strony.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-114">For information, see hello [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) page.</span></span>

* <span data-ttu-id="9cf4d-115">Komputer Mac z zainstalowanym środowiskiem Xcode v7.0 lub nowszym i rozwiązaniem Xamarin Studio Community.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="9cf4d-116">Aby uzyskać informacje, zobacz tematy [Set up and install for Visual Studio and Xamarin (Konfigurowanie i instalowanie dla programów Visual Studio i Xamarin)](https://msdn.microsoft.com/library/mt613162.aspx) oraz [Set up, install, and verify for Mac users (Konfigurowanie, instalowanie i weryfikowanie dla użytkowników komputerów Mac)](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="9cf4d-116">For information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Set up, install, and verify for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-a-new-mobile-apps-back-end"></a><span data-ttu-id="9cf4d-117">Tworzenie nowego zaplecza funkcji Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="9cf4d-117">Create a new Mobile Apps back end</span></span>

<span data-ttu-id="9cf4d-118">toocreate zakończyć nowych aplikacji mobilnych w Wstecz, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="9cf4d-118">toocreate a new Mobile Apps back end, do hello following:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="9cf4d-119">Masz teraz zdefiniowane zaplecze funkcji Mobile Apps, którego mogą używać mobilne aplikacje klienckie.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-119">You have now set up a Mobile Apps back end that your mobile client applications can use.</span></span> <span data-ttu-id="9cf4d-120">Następnie należy pobrać Projekt serwera dla wewnętrznej listy zadań do wykonania prostego, a następnie opublikuj go tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-120">Next, you download a server project for a simple to-do list back end and then publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="9cf4d-121">Konfigurowanie projektu serwera hello</span><span class="sxs-lookup"><span data-stu-id="9cf4d-121">Configure hello server project</span></span>

<span data-ttu-id="9cf4d-122">tooconfigure powitania serwera projektu toouse hello zaplecza Node.js lub .NET, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="9cf4d-122">tooconfigure hello server project toouse either hello Node.js or .NET back end, do hello following:</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinforms-solution"></a><span data-ttu-id="9cf4d-123">Pobierz i uruchom hello rozwiązania platformy Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="9cf4d-123">Download and run hello Xamarin.Forms solution</span></span>

<span data-ttu-id="9cf4d-124">Możesz pobrać rozwiązanie hello na dwa sposoby.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-124">You can download hello solution in either of two ways.</span></span> <span data-ttu-id="9cf4d-125">Pobrać tooa Mac i otworzyć go w programie Xamarin Studio lub pobrać tooa komputer z systemem Windows i otworzyć go w programie Visual Studio za pomocą sieci Mac do tworzenia aplikacji dla systemu iOS hello.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-125">Download it tooa Mac and open it in Xamarin Studio, or download it tooa Windows computer and open it in Visual Studio by using a networked Mac for building hello iOS app.</span></span> <span data-ttu-id="9cf4d-126">Aby uzyskać więcej informacji, zobacz stronę [Set up and install Visual Studio and Xamarin (Konfigurowanie i instalowanie programów Visual Studio i Xamarin)](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="9cf4d-126">For more information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>

<span data-ttu-id="9cf4d-127">Na komputerze Mac lub Windows hello następujące:</span><span class="sxs-lookup"><span data-stu-id="9cf4d-127">On a Mac or Windows computer, do hello following:</span></span>

1. <span data-ttu-id="9cf4d-128">Przejdź toohello [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="9cf4d-128">Go toohello [Azure portal].</span></span>

2. <span data-ttu-id="9cf4d-129">Na powitania **ustawienia** bloku dla aplikacji mobilnej, w obszarze **Mobile**, wybierz pozycję **wprowadzenie** > **platformy Xamarin.Forms**.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-129">On hello **Settings** blade for your mobile app, under **Mobile**, select **Get Started** > **Xamarin.Forms**.</span></span> <span data-ttu-id="9cf4d-130">W **kroku 3** wybierz pozycję **Utwórz nową aplikację**, a następnie wybierz pozycję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-130">Under **step 3**, select  **Create a new app**, and then select **Download**.</span></span>

   <span data-ttu-id="9cf4d-131">Ta akcja spowoduje pobranie projektu, który zawiera aplikację klienta, który jest połączony tooyour aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-131">This action downloads a project that contains a client application that's connected tooyour mobile app.</span></span> <span data-ttu-id="9cf4d-132">Zapisz komputera lokalnego tooyour hello projektu skompresowany plik i zanotuj miejsce jego zapisania.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-132">Save hello compressed project file tooyour local computer, and make a note of where you save it.</span></span>

3. <span data-ttu-id="9cf4d-133">Wyodrębnij pobrany projekt hello, a następnie otwórz go w programie Xamarin Studio (Mac) lub programu Visual Studio (z systemem Windows).</span><span class="sxs-lookup"><span data-stu-id="9cf4d-133">Extract hello project that you downloaded, and then open it in Xamarin Studio (Mac) or Visual Studio (Windows).</span></span>

   ![Projekt wyodrębniony w programie Xamarin Studio][9]

   ![Projekt wyodrębniony w programie Visual Studio][8]

## <a name="optional-run-hello-ios-project"></a><span data-ttu-id="9cf4d-136">(Opcjonalnie) Uruchom projekt dla systemu iOS hello</span><span class="sxs-lookup"><span data-stu-id="9cf4d-136">(Optional) Run hello iOS project</span></span>
<span data-ttu-id="9cf4d-137">W tej sekcji możesz uruchomić projektu hello Xamarin iOS dla urządzeń z systemem iOS.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-137">In this section, you run hello Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="9cf4d-138">Jeśli nie pracujesz z urządzeniami z systemem iOS, możesz pominąć tę sekcję.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-138">You can skip this section if you are not working with iOS devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="9cf4d-139">W programie Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="9cf4d-139">In Xamarin Studio</span></span>
1. <span data-ttu-id="9cf4d-140">Kliknij prawym przyciskiem myszy projekt iOS hello, a następnie wybierz **Ustaw jako projekt startowy**.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-140">Right-click hello iOS project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="9cf4d-141">Na powitania **Uruchom** menu, wybierz opcję **Rozpocznij debugowanie** toobuild hello projekt i uruchomić aplikacji hello w emulatorze urządzenia iPhone hello.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-141">On hello **Run** menu, select **Start Debugging** toobuild hello project and start hello app in hello iPhone emulator.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="9cf4d-142">W programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9cf4d-142">In Visual Studio</span></span>
1. <span data-ttu-id="9cf4d-143">Kliknij prawym przyciskiem myszy projekt iOS hello, a następnie wybierz **Ustaw jako projekt startowy**.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-143">Right-click hello iOS project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="9cf4d-144">Na powitania **kompilacji** menu, wybierz opcję **programu Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-144">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="9cf4d-145">W hello **programu Configuration Manager** okno dialogowe, wybierz opcję hello **kompilacji** i **Wdróż** projektu iOS toohello dalej pola wyboru.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-145">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello iOS project.</span></span>

4. <span data-ttu-id="9cf4d-146">toobuild hello projekt i uruchomić aplikacji hello w emulatorze urządzenia iPhone hello, wybierz hello **F5** klucza.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-146">toobuild hello project and start hello app in hello iPhone emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9cf4d-147">Jeśli masz problemy z kompilacją hello projektu, uruchom hello NuGet pakietu manager i aktualizacji toohello najnowszą wersję hello Xamarin obsługi pakietów.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-147">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="9cf4d-148">Projekty Szybki Start może być wolne tooupdate toohello najnowszych wersji.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-148">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="9cf4d-149">W aplikacji hello wpisz znaczący tekst, na przykład *Poznaj program Xamarin*, a następnie wybierz hello znak plus (**+**).</span><span class="sxs-lookup"><span data-stu-id="9cf4d-149">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    ![][10]

    <span data-ttu-id="9cf4d-150">Ta akcja wysyła toohello żądania post, nowe aplikacje mobilne zaplecza, która jest hostowana na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-150">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="9cf4d-151">Dane z hello żądania zostaną wstawione do tabeli TodoItem hello.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-151">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="9cf4d-152">Elementy, które są przechowywane w tabeli hello są zwracane przez hello Mobile Apps ponownie zakończyć i hello się, że dane są wyświetlane na liście hello.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-152">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9cf4d-153">Znajdziesz hello kodu, który uzyskuje dostęp do Twojego Mobile Apps zaplecza w hello pliku C# TodoItemManager.cs projektu biblioteki klas przenośnych hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-153">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-hello-android-project"></a><span data-ttu-id="9cf4d-154">(Opcjonalnie) Uruchom projekt dla systemu Android hello</span><span class="sxs-lookup"><span data-stu-id="9cf4d-154">(Optional) Run hello Android project</span></span>
<span data-ttu-id="9cf4d-155">W tej sekcji możesz uruchomić hello Xamarin droid projektu dla systemu Android.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-155">In this section, you run hello Xamarin droid project for Android.</span></span> <span data-ttu-id="9cf4d-156">Jeśli nie pracujesz z urządzeniami z systemem Android, możesz pominąć tę sekcję.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-156">You can skip this section if you are not working with Android devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="9cf4d-157">W programie Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="9cf4d-157">In Xamarin Studio</span></span>

1. <span data-ttu-id="9cf4d-158">Kliknij prawym przyciskiem myszy projekt Android hello, a następnie wybierz **Ustaw jako projekt startowy**.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-158">Right-click hello Android project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="9cf4d-159">toobuild hello projekt i uruchomić aplikacji hello w emulatorze systemu Android, na powitania **Uruchom** menu, wybierz opcję **Rozpocznij debugowanie**.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-159">toobuild hello project and start hello app in an Android emulator, on hello **Run** menu, select **Start Debugging**.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="9cf4d-160">W programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9cf4d-160">In Visual Studio</span></span>

1. <span data-ttu-id="9cf4d-161">Kliknij prawym przyciskiem myszy projekt Android (Droid) hello, a następnie wybierz **Ustaw jako projekt startowy**.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-161">Right-click hello Android (Droid) project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="9cf4d-162">Na powitania **kompilacji** menu, wybierz opcję **programu Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-162">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="9cf4d-163">W hello **programu Configuration Manager** okno dialogowe, wybierz opcję hello **kompilacji** i **Wdróż** pola wyboru dalej toohello projekt systemu Android.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-163">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello Android project.</span></span>

4. <span data-ttu-id="9cf4d-164">toobuild hello projekt i uruchomić aplikacji hello w emulatorze systemu Android wybierz opcję hello **F5** klucza.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-164">toobuild hello project and start hello app in an Android emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9cf4d-165">Jeśli masz problemy z kompilacją hello projektu, uruchom hello NuGet pakietu manager i aktualizacji toohello najnowszą wersję hello Xamarin obsługi pakietów.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-165">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="9cf4d-166">Projekty Szybki Start może być wolne tooupdate toohello najnowszych wersji.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-166">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="9cf4d-167">W aplikacji hello wpisz znaczący tekst, na przykład *Poznaj program Xamarin*, a następnie wybierz hello znak plus (**+**).</span><span class="sxs-lookup"><span data-stu-id="9cf4d-167">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    ![][11]
    
    <span data-ttu-id="9cf4d-168">Ta akcja wysyła toohello żądania post, nowe aplikacje mobilne zaplecza, która jest hostowana na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-168">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="9cf4d-169">Dane z hello żądania zostaną wstawione do tabeli TodoItem hello.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-169">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="9cf4d-170">Elementy, które są przechowywane w tabeli hello są zwracane przez hello Mobile Apps ponownie zakończyć i hello się, że dane są wyświetlane na liście hello.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-170">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="9cf4d-171">Znajdziesz hello kodu, który uzyskuje dostęp do Twojego Mobile Apps zaplecza w hello pliku C# TodoItemManager.cs projektu biblioteki klas przenośnych hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-171">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-hello-windows-project"></a><span data-ttu-id="9cf4d-172">(Opcjonalnie) Uruchom projekt dla systemu Windows hello</span><span class="sxs-lookup"><span data-stu-id="9cf4d-172">(Optional) Run hello Windows project</span></span>

<span data-ttu-id="9cf4d-173">W tej sekcji służy do uruchamiania projektu Xamarin WinApp dla urządzeń z systemem Windows hello.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-173">In this section, you run hello Xamarin WinApp project for Windows devices.</span></span> <span data-ttu-id="9cf4d-174">Jeśli nie pracujesz z urządzeniami z systemem Windows, możesz pominąć tę sekcję.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="9cf4d-175">W programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9cf4d-175">In Visual Studio</span></span>

1. <span data-ttu-id="9cf4d-176">Kliknij prawym przyciskiem myszy projekty systemu Windows hello, a następnie wybierz **Ustaw jako projekt startowy**.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-176">Right-click any of hello Windows projects, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="9cf4d-177">Na powitania **kompilacji** menu, wybierz opcję **programu Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-177">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="9cf4d-178">W hello **programu Configuration Manager** okno dialogowe, wybierz opcję hello **kompilacji** i **Wdróż** pola wyboru dalej toohello Windows wybranego projektu.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-178">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello Windows project that you chose.</span></span>

4. <span data-ttu-id="9cf4d-179">toobuild hello projekt i uruchomić aplikacji hello w emulatorze systemu Windows, wybierz opcję hello **F5** klucza.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-179">toobuild hello project and start hello app in a Windows emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9cf4d-180">Jeśli masz problemy z kompilacją hello projektu, uruchom hello NuGet pakietu manager i aktualizacji toohello najnowszą wersję hello Xamarin obsługi pakietów.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-180">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="9cf4d-181">Projekty Szybki Start może być wolne tooupdate toohello najnowszych wersji.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-181">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="9cf4d-182">W aplikacji hello wpisz znaczący tekst, na przykład *Poznaj program Xamarin*, a następnie wybierz hello znak plus (**+**).</span><span class="sxs-lookup"><span data-stu-id="9cf4d-182">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    <span data-ttu-id="9cf4d-183">Ta akcja wysyła toohello żądania post, nowe aplikacje mobilne zaplecza, która jest hostowana na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-183">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="9cf4d-184">Dane z hello żądania zostaną wstawione do tabeli TodoItem hello.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-184">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="9cf4d-185">Elementy, które są przechowywane w tabeli hello są zwracane przez hello Mobile Apps ponownie zakończyć i hello się, że dane są wyświetlane na liście hello.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-185">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>
    
    ![][12]
    
    > [!NOTE]
    > <span data-ttu-id="9cf4d-186">Znajdziesz hello kodu, który uzyskuje dostęp do Twojego Mobile Apps zaplecza w hello pliku C# TodoItemManager.cs projektu biblioteki klas przenośnych hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-186">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="next-steps"></a><span data-ttu-id="9cf4d-187">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9cf4d-187">Next steps</span></span>

* [<span data-ttu-id="9cf4d-188">Dodaj aplikację tooyour uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="9cf4d-188">Add authentication tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="9cf4d-189">Dowiedz się, jak tooauthenticate użytkowników aplikacji przy użyciu dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-189">Learn how tooauthenticate users of your app with an identity provider.</span></span>

* [<span data-ttu-id="9cf4d-190">Dodaj aplikację tooyour powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="9cf4d-190">Add push notifications tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)  
  <span data-ttu-id="9cf4d-191">Dowiedz się, jak powiadomień wypychanych tooadd obsługują tooyour aplikacji i Konfigurowanie powiadomień wypychanych Mobile Apps zaplecza toouse usługi Azure Notification Hubs toosend hello.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-191">Learn how tooadd push notifications support tooyour app and configure your Mobile Apps back end toouse Azure Notification Hubs toosend hello push notifications.</span></span>

* [<span data-ttu-id="9cf4d-192">Włączanie synchronizacji w trybie offline dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="9cf4d-192">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="9cf4d-193">Dowiedz się, jak zaplecza tooadd obsługi w trybie offline dla aplikacji przy użyciu aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-193">Learn how tooadd offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="9cf4d-194">Synchronizacja w trybie offline umożliwia wyświetlanie, dodawanie lub modyfikowanie danych aplikacji mobilnej, nawet w przypadku braku połączenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-194">With offline sync, you can view, add, or modify your mobile app's data, even when there is no network connection.</span></span>

* [<span data-ttu-id="9cf4d-195">Użyj hello zarządzanego klienta dla aplikacji mobilnych</span><span class="sxs-lookup"><span data-stu-id="9cf4d-195">Use hello managed client for Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)  
  <span data-ttu-id="9cf4d-196">Dowiedz się, jak toowork z hello zarządzanego klienta SDK w aplikacji platformy Xamarin.</span><span class="sxs-lookup"><span data-stu-id="9cf4d-196">Learn how toowork with hello managed client SDK in your Xamarin app.</span></span>

<!-- Anchors. -->
[Get started with Mobile Apps back ends]:#getting-started
[Create a new Mobile Apps back end]:#create-new-service
[Next steps]:#next-steps


<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart.png
[8]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-vs.png
[9]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-xs.png
[10]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-ios.png
[11]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-android.png
[12]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-windows.png


<!-- URLs. -->
[Visual Studio Professional 2013]: https://go.microsoft.com/fwLink/p/?LinkID=257546
[Mobile app SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[portalu Azure]: https://portal.azure.com/
