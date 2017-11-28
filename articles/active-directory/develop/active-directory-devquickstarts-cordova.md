---
title: Azure AD oprogramowania Cordova wprowadzenie | Dokumentacja firmy Microsoft
description: "Jak utworzyć aplikację Cordova, która integruje się z usługą Azure AD, logowania i wywołuje Azure interfejsów API, które są chronione przez usługi AD za pomocą uwierzytelniania OAuth."
services: active-directory
documentationcenter: 
author: vibronet
manager: mbaldwin
editor: 
ms.assetid: b1a8d7bd-7ad6-44d5-8ccb-5255bb623345
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: vittorib
ms.custom: aaddev
ms.openlocfilehash: d9f53148787729d29a0a89cce1b8b2b83ba228f8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a><span data-ttu-id="540c9-103">Integrowanie usługi Azure AD z Apache aplikacji Cordova</span><span class="sxs-lookup"><span data-stu-id="540c9-103">Integrate Azure AD with an Apache Cordova app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="540c9-104">Apache Cordova służy do tworzenia aplikacji HTML5/JavaScript, które można uruchomić na urządzeniach przenośnych jako pełni funkcjonalnymi natywnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="540c9-104">You can use Apache Cordova to develop HTML5/JavaScript applications that can run on mobile devices as full-fledged native applications.</span></span> <span data-ttu-id="540c9-105">Usłudze Azure Active Directory (Azure AD) możesz dodać funkcje klasy korporacyjnej uwierzytelniania do aplikacji oprogramowania Cordova.</span><span class="sxs-lookup"><span data-stu-id="540c9-105">With Azure Active Directory (Azure AD), you can add enterprise-grade authentication capabilities to your Cordova applications.</span></span>

<span data-ttu-id="540c9-106">Wtyczka Cordova opakowuje Azure AD natywnych zestawów SDK w systemach iOS, Android, Sklep Windows i Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="540c9-106">A Cordova plug-in wraps Azure AD native SDKs on iOS, Android, Windows Store, and Windows Phone.</span></span> <span data-ttu-id="540c9-107">Za pomocą, że dodatek plug-in, można rozszerzyć aplikacji do obsługi logowania przy użyciu kont usługi Active Directory systemu Windows Server użytkowników, uzyskiwanie dostępu do usługi Office 365 i interfejsów API usługi Azure, a nawet chronić wywołania do własnego niestandardowego interfejsu API w sieci web.</span><span class="sxs-lookup"><span data-stu-id="540c9-107">By using that plug-in, you can enhance your application to support sign-in with your users' Windows Server Active Directory accounts, gain access to Office 365 and Azure APIs, and even help protect calls to your own custom web API.</span></span>

<span data-ttu-id="540c9-108">W tym samouczku Apache Cordova wtyczki dla Active Directory Authentication Library (ADAL) będą używane do poprawy prostej aplikacji przez dodanie następujących funkcji:</span><span class="sxs-lookup"><span data-stu-id="540c9-108">In this tutorial, we'll use the Apache Cordova plug-in for Active Directory Authentication Library (ADAL) to improve a simple app by adding the following features:</span></span>

* <span data-ttu-id="540c9-109">Przy użyciu kilku wierszy kodu uwierzytelniania użytkownika i uzyskania tokenu.</span><span class="sxs-lookup"><span data-stu-id="540c9-109">With just a few lines of code, authenticate a user and obtain a token.</span></span>
* <span data-ttu-id="540c9-110">Użyj tego tokenu do wywołania interfejsu API programu Graph do tego katalogu zapytania i wyświetlić wyniki.</span><span class="sxs-lookup"><span data-stu-id="540c9-110">Use that token to invoke the Graph API to query that directory and display the results.</span></span>  
* <span data-ttu-id="540c9-111">Użyj tokenu ADAL pamięci podręcznej, aby zminimalizować monitowania użytkownika o uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="540c9-111">Use the ADAL token cache to minimize authentication prompts for the user.</span></span>

<span data-ttu-id="540c9-112">Aby wprowadzić te ulepszenia, musisz:</span><span class="sxs-lookup"><span data-stu-id="540c9-112">To make those improvements, you need to:</span></span>

1. <span data-ttu-id="540c9-113">Zarejestrować aplikację w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="540c9-113">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="540c9-114">Dodawanie kodu do aplikacji do żądania tokenów.</span><span class="sxs-lookup"><span data-stu-id="540c9-114">Add code to your app to request tokens.</span></span>
3. <span data-ttu-id="540c9-115">Dodaj kod, aby Użyj tokenu na potrzeby realizacji zapytania interfejsu API programu Graph i wyświetlić wyniki.</span><span class="sxs-lookup"><span data-stu-id="540c9-115">Add code to use the token for querying the Graph API and display results.</span></span>
4. <span data-ttu-id="540c9-116">Utwórz projekt wdrożenia oprogramowania Cordova z platformami, które ma być docelowa, Dodaj Cordova ADAL wtyczki i przetestowania rozwiązania w emulatory.</span><span class="sxs-lookup"><span data-stu-id="540c9-116">Create the Cordova deployment project with all the platforms you want to target, add the Cordova ADAL plug-in, and test the solution in emulators.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="540c9-117">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="540c9-117">Prerequisites</span></span>
<span data-ttu-id="540c9-118">Do ukończenia tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="540c9-118">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="540c9-119">Dzierżawa usługi Azure AD, gdzie masz konto z uprawnieniami rozwoju aplikacji.</span><span class="sxs-lookup"><span data-stu-id="540c9-119">An Azure AD tenant where you have an account with app development rights.</span></span>
* <span data-ttu-id="540c9-120">Środowisko deweloperskie, który jest skonfigurowany do używania oprogramowania Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="540c9-120">A development environment that's configured to use Apache Cordova.</span></span>  

<span data-ttu-id="540c9-121">Jeśli masz zarówno już skonfigurować, bezpośrednio przejść do kroku 1.</span><span class="sxs-lookup"><span data-stu-id="540c9-121">If you have both already set up, proceed directly to step 1.</span></span>

<span data-ttu-id="540c9-122">Jeśli nie masz dzierżawę usługi Azure AD, użyj [instrukcje dotyczące sposobu uzyskania jedną](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="540c9-122">If you don't have an Azure AD tenant, use the [instructions on how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="540c9-123">Jeśli nie masz Apache Cordova na komputerze, należy zainstalować następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="540c9-123">If you don't have Apache Cordova set up on your machine, install the following:</span></span>

* [<span data-ttu-id="540c9-124">Git</span><span class="sxs-lookup"><span data-stu-id="540c9-124">Git</span></span>](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [<span data-ttu-id="540c9-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="540c9-125">Node.js</span></span>](https://nodejs.org/download/)
* <span data-ttu-id="540c9-126">[Interfejs Cordova CLI](https://cordova.apache.org/) (można łatwo zainstalować za pomocą Menedżera pakietów NPM: `npm install -g cordova`)</span><span class="sxs-lookup"><span data-stu-id="540c9-126">[Cordova CLI](https://cordova.apache.org/) (can be easily installed via NPM package manager: `npm install -g cordova`)</span></span>

<span data-ttu-id="540c9-127">Poprzednie instalacje powinny działać zarówno na komputerze, jak i komputerów Mac.</span><span class="sxs-lookup"><span data-stu-id="540c9-127">The preceding installations should work both on the PC and on the Mac.</span></span>

<span data-ttu-id="540c9-128">Każda platforma docelowa ma inne wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="540c9-128">Each target platform has different prerequisites:</span></span>

* <span data-ttu-id="540c9-129">Aby skompilować i uruchomić aplikację dla komputerów typu Tablet z systemem Windows lub Windows Phone:</span><span class="sxs-lookup"><span data-stu-id="540c9-129">To build and run an app for Windows Tablet/PC or Windows Phone:</span></span>
  * <span data-ttu-id="540c9-130">Zainstaluj [programu Visual Studio 2013 dla systemu Windows z Update 2 lub nowszym](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express lub inna wersja) lub [programu Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span><span class="sxs-lookup"><span data-stu-id="540c9-130">Install [Visual Studio 2013 for Windows with Update 2 or later](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express or another version) or [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span></span>

* <span data-ttu-id="540c9-131">Aby skompilować i uruchomić aplikację dla systemu iOS:</span><span class="sxs-lookup"><span data-stu-id="540c9-131">To build and run an app for iOS:</span></span>

  * <span data-ttu-id="540c9-132">Zainstaluj program Xcode 6.x lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="540c9-132">Install Xcode 6.x or later.</span></span> <span data-ttu-id="540c9-133">Pobierz go z [witryny dla deweloperów firmy Apple](http://developer.apple.com/downloads) lub [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span><span class="sxs-lookup"><span data-stu-id="540c9-133">Download it from the [Apple Developer site](http://developer.apple.com/downloads) or the [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span></span>
  * <span data-ttu-id="540c9-134">Zainstaluj [ios-sim](https://www.npmjs.org/package/ios-sim).</span><span class="sxs-lookup"><span data-stu-id="540c9-134">Install [ios-sim](https://www.npmjs.org/package/ios-sim).</span></span> <span data-ttu-id="540c9-135">Służy on do uruchomienia aplikacji systemu iOS w symulatora systemu iOS z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="540c9-135">You can use it to start iOS apps in iOS Simulator from the command line.</span></span> <span data-ttu-id="540c9-136">(Można go łatwo zainstalować przy użyciu terminala: `npm install -g ios-sim`.)</span><span class="sxs-lookup"><span data-stu-id="540c9-136">(You can easily install it via the terminal: `npm install -g ios-sim`.)</span></span>
* <span data-ttu-id="540c9-137">Aby skompilować i uruchomić aplikację dla systemu Android:</span><span class="sxs-lookup"><span data-stu-id="540c9-137">To build and run an app for Android:</span></span>

  * <span data-ttu-id="540c9-138">Zainstaluj [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="540c9-138">Install [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or later.</span></span> <span data-ttu-id="540c9-139">Upewnij się, że `JAVA_HOME` (zmienną środowiskową) jest poprawnie ustawiony odpowiednio do atrybutów JDK ścieżki instalacji (na przykład C:\Program Files\Java\jdk1.7.0_75).</span><span class="sxs-lookup"><span data-stu-id="540c9-139">Make sure `JAVA_HOME` (environment variable) is correctly set according to the JDK installation path (for example, C:\Program Files\Java\jdk1.7.0_75).</span></span>
  * <span data-ttu-id="540c9-140">Zainstaluj [zestawu SDK systemu Android](http://developer.android.com/sdk/installing/index.html?pkg=tools) i Dodaj `<android-sdk-location>\tools` lokalizację (na przykład C:\tools\Android\android-sdk\tools) do sieci `PATH` zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="540c9-140">Install [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) and add the `<android-sdk-location>\tools` location (for example, C:\tools\Android\android-sdk\tools) to your `PATH` environment variable.</span></span>
  * <span data-ttu-id="540c9-141">Otwórz Menedżera zestawu SDK systemu Android (na przykład przy użyciu terminala: `android`) i zainstalować:</span><span class="sxs-lookup"><span data-stu-id="540c9-141">Open Android SDK Manager (for example, via the terminal: `android`) and install:</span></span>
    * <span data-ttu-id="540c9-142">*5.0.1 systemu android (interfejs API 21)* zestawu SDK platformy</span><span class="sxs-lookup"><span data-stu-id="540c9-142">*Android 5.0.1 (API 21)* platform SDK</span></span>
    * <span data-ttu-id="540c9-143">*Narzędzia kompilacji zestawu SDK dla systemu android* wersji 19.1.0 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="540c9-143">*Android SDK Build Tools* version 19.1.0 or later</span></span>
    * <span data-ttu-id="540c9-144">*Obsługa systemu android repozytorium* (dodatki)</span><span class="sxs-lookup"><span data-stu-id="540c9-144">*Android Support Repository* (Extras)</span></span>

  <span data-ttu-id="540c9-145">Zestaw SDK systemu Android nie zapewnia żadnych domyślne wystąpienie emulatora.</span><span class="sxs-lookup"><span data-stu-id="540c9-145">The Android SDK doesn't provide any default emulator instance.</span></span> <span data-ttu-id="540c9-146">Utworzyć, uruchamiając `android avd` z terminala i wybierając **Utwórz**, jeśli chcesz uruchomić emulatora aplikacji systemu Android.</span><span class="sxs-lookup"><span data-stu-id="540c9-146">Create one by running `android avd` from the terminal and then selecting **Create**, if you want to run the Android app on an emulator.</span></span> <span data-ttu-id="540c9-147">Zaleca się poziom interfejsu API 19 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="540c9-147">We recommend an API level of 19 or higher.</span></span> <span data-ttu-id="540c9-148">Aby uzyskać więcej informacji o opcji Android emulator i tworzenia, zobacz [Menedżera AVD](http://developer.android.com/tools/help/avd-manager.html) w witrynie systemu Android.</span><span class="sxs-lookup"><span data-stu-id="540c9-148">For more information about the Android emulator and creation options, see [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) on the Android site.</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="540c9-149">Krok 1: Rejestrowanie aplikacji w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="540c9-149">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="540c9-150">Ten krok jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="540c9-150">This step is optional.</span></span> <span data-ttu-id="540c9-151">Ten samouczek zawiera wstępnie przygotowany wartości, których można użyć, aby zobaczyć przykładowy w akcji bez wykonywania żadnych alokacji w własną dzierżawę.</span><span class="sxs-lookup"><span data-stu-id="540c9-151">This tutorial provides pre-provisioned values that you can use to see the sample in action without doing any provisioning in your own tenant.</span></span> <span data-ttu-id="540c9-152">Jednak zaleca się wykonać ten krok i zapoznać się z procesem, ponieważ będzie wymagane podczas tworzenia własnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="540c9-152">However, we recommend that you do perform this step and become familiar with the process, because it will be required when you create your own applications.</span></span>

<span data-ttu-id="540c9-153">Usługi Azure AD wystawia tokeny tylko znane aplikacje.</span><span class="sxs-lookup"><span data-stu-id="540c9-153">Azure AD issues tokens to only known applications.</span></span> <span data-ttu-id="540c9-154">Zanim użyjesz usługi Azure AD z aplikacji, musisz utworzyć wpis dla niego w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="540c9-154">Before you can use Azure AD from your app, you need to create an entry for it in your tenant.</span></span> <span data-ttu-id="540c9-155">Aby zarejestrować nową aplikację w dzierżawie:</span><span class="sxs-lookup"><span data-stu-id="540c9-155">To register a new application in your tenant:</span></span>

1. <span data-ttu-id="540c9-156">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="540c9-156">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="540c9-157">Na górnym pasku kliknij konto.</span><span class="sxs-lookup"><span data-stu-id="540c9-157">On the top bar, click your account.</span></span> <span data-ttu-id="540c9-158">W **katalogu** wybierz dzierżawy usługi Azure AD, które chcesz zarejestrować aplikację.</span><span class="sxs-lookup"><span data-stu-id="540c9-158">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="540c9-159">Kliknij przycisk **więcej usług** w okienku po lewej stronie, a następnie wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="540c9-159">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="540c9-160">Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="540c9-160">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="540c9-161">Postępuj zgodnie z monitami i Utwórz **natywną aplikację kliencką**.</span><span class="sxs-lookup"><span data-stu-id="540c9-161">Follow the prompts and create a **Native Client Application**.</span></span> <span data-ttu-id="540c9-162">(Chociaż aplikacje Cordova HTML na podstawie, tworzymy aplikację native client w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="540c9-162">(Although Cordova apps are HTML based, we're creating a native client application here.</span></span> <span data-ttu-id="540c9-163">**Natywną aplikację kliencką** musi być zaznaczona opcja lub aplikacja nie będzie działać.)</span><span class="sxs-lookup"><span data-stu-id="540c9-163">The **Native Client Application** option must be selected, or the application won't work.)</span></span>
  * <span data-ttu-id="540c9-164">**Nazwa** opisuje aplikacji dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="540c9-164">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="540c9-165">**Identyfikator URI przekierowania** jest identyfikator URI, który służy do zwracania tokenów do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="540c9-165">**Redirect URI** is the URI that's used to return tokens to your app.</span></span> <span data-ttu-id="540c9-166">Wprowadź **http://MyDirectorySearcherApp**.</span><span class="sxs-lookup"><span data-stu-id="540c9-166">Enter **http://MyDirectorySearcherApp**.</span></span>

<span data-ttu-id="540c9-167">Po zakończeniu rejestracji usługi Azure AD przypisuje unikatowy identyfikator aplikacji do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="540c9-167">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span> <span data-ttu-id="540c9-168">Będziesz potrzebować tę wartość w kolejnych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="540c9-168">You’ll need this value in the next sections.</span></span> <span data-ttu-id="540c9-169">Można go znaleźć na karcie aplikacji nowo utworzonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="540c9-169">You can find it on the application tab of the newly created app.</span></span>

<span data-ttu-id="540c9-170">Aby uruchomić `DirSearchClient Sample`, udziel uprawnienia nowo utworzoną aplikacją wykonać zapytania interfejsu API Azure AD Graph:</span><span class="sxs-lookup"><span data-stu-id="540c9-170">To run `DirSearchClient Sample`, grant the newly created app permission to query the Azure AD Graph API:</span></span>

1. <span data-ttu-id="540c9-171">Z **ustawienia** wybierz pozycję **wymagane uprawnienia**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="540c9-171">From the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>  
2. <span data-ttu-id="540c9-172">Dla aplikacji usługi Azure Active Directory wybierz **Microsoft Graph** jako interfejsu API i Dodaj **dostępu do katalogu jako zalogowany użytkownik** uprawnienie w obszarze **delegowane uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="540c9-172">For the Azure Active Directory application, select **Microsoft Graph** as the API and add the **Access the directory as the signed-in user** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="540c9-173">Dzięki temu aplikacja wykonać zapytania interfejsu API programu Graph dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="540c9-173">This enables your application to query the Graph API for users.</span></span>

## <a name="step-2-clone-the-sample-app-repository"></a><span data-ttu-id="540c9-174">Krok 2: Klonowanie repozytorium przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="540c9-174">Step 2: Clone the sample app repository</span></span>
<span data-ttu-id="540c9-175">Z powłoki lub wiersza polecenia wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="540c9-175">From your shell or command line, type the following command:</span></span>

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-the-cordova-app"></a><span data-ttu-id="540c9-176">Krok 3: Tworzenie aplikacji Cordova</span><span class="sxs-lookup"><span data-stu-id="540c9-176">Step 3: Create the Cordova app</span></span>
<span data-ttu-id="540c9-177">Istnieje wiele sposobów tworzenia aplikacji Cordova.</span><span class="sxs-lookup"><span data-stu-id="540c9-177">There are multiple ways to create Cordova applications.</span></span> <span data-ttu-id="540c9-178">W tym samouczku użyjemy Cordova interfejsu wiersza polecenia (CLI).</span><span class="sxs-lookup"><span data-stu-id="540c9-178">In this tutorial, we'll use the Cordova command-line interface (CLI).</span></span>

1. <span data-ttu-id="540c9-179">Z powłoki lub wiersza polecenia wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="540c9-179">From your shell or command line, type the following command:</span></span>

        cordova create DirSearchClient

   <span data-ttu-id="540c9-180">To polecenie tworzy struktury folderów i funkcją szkieletów dla projektu oprogramowania Cordova.</span><span class="sxs-lookup"><span data-stu-id="540c9-180">That command creates the folder structure and scaffolding for the Cordova project.</span></span>

2. <span data-ttu-id="540c9-181">Przenieś do nowego folderu DirSearchClient:</span><span class="sxs-lookup"><span data-stu-id="540c9-181">Move to the new DirSearchClient folder:</span></span>

        cd .\DirSearchClient

3. <span data-ttu-id="540c9-182">Skopiuj zawartość projektu starter w podfolderze www przy użyciu Menedżera plików lub polecenie powłoki:</span><span class="sxs-lookup"><span data-stu-id="540c9-182">Copy the content of the starter project in the www subfolder by using a file manager or the following command in your shell:</span></span>

  * <span data-ttu-id="540c9-183">System Windows:`xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span><span class="sxs-lookup"><span data-stu-id="540c9-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span></span>
  * <span data-ttu-id="540c9-184">Mac:`cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span><span class="sxs-lookup"><span data-stu-id="540c9-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span></span>

4. <span data-ttu-id="540c9-185">Dodaj wtyczkę dozwolonych.</span><span class="sxs-lookup"><span data-stu-id="540c9-185">Add the whitelist plug-in.</span></span> <span data-ttu-id="540c9-186">Jest to konieczne do wywoływania interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="540c9-186">This is necessary for invoking the Graph API.</span></span>

        cordova plugin add cordova-plugin-whitelist

5. <span data-ttu-id="540c9-187">Dodaj wszystkie platformy, które mają być obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="540c9-187">Add all the platforms that you want to support.</span></span> <span data-ttu-id="540c9-188">Aby próbki roboczej, należy wykonać co najmniej jeden z następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="540c9-188">To have a working sample, you need to execute at least one of the following commands.</span></span> <span data-ttu-id="540c9-189">Należy pamiętać, że nie będzie można emulować systemu iOS w systemie Windows lub emulacji systemu Windows na komputerach Mac.</span><span class="sxs-lookup"><span data-stu-id="540c9-189">Note that you won't be able to emulate iOS on Windows or emulate Windows on a Mac.</span></span>

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. <span data-ttu-id="540c9-190">Dodawanie biblioteki ADAL dla wtyczki Cordova do projektu:</span><span class="sxs-lookup"><span data-stu-id="540c9-190">Add the ADAL for Cordova plug-in to your project:</span></span>

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-to-authenticate-users-and-obtain-tokens-from-azure-ad"></a><span data-ttu-id="540c9-191">Krok 4: Dodaj kod, aby uwierzytelniać użytkowników i uzyskać tokeny z usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="540c9-191">Step 4: Add code to authenticate users and obtain tokens from Azure AD</span></span>
<span data-ttu-id="540c9-192">Aplikacja, która projektujesz w tym samouczku zapewni funkcji wyszukiwania prostego katalogu.</span><span class="sxs-lookup"><span data-stu-id="540c9-192">The application that you're developing in this tutorial will provide a simple directory search feature.</span></span> <span data-ttu-id="540c9-193">Użytkownik może następnie wpisz alias każdego użytkownika w katalogu i wizualizacji niektóre podstawowe atrybuty.</span><span class="sxs-lookup"><span data-stu-id="540c9-193">The user can then type the alias of any user in the directory and visualize some basic attributes.</span></span> <span data-ttu-id="540c9-194">Projekt starter nie zawiera definicji podstawowy interfejs użytkownika aplikacji (w www/index.html) i funkcja szkieletów, który tworzącej zdarzeń Podstawowa aplikacja cykli powiązania interfejsu użytkownika i powoduje wyświetlanie logikę (www/js/index.js).</span><span class="sxs-lookup"><span data-stu-id="540c9-194">The starter project contains the definition of the basic user interface of the app (in www/index.html) and the scaffolding that wires up basic app event cycles, user interface bindings, and results display logic (in www/js/index.js).</span></span> <span data-ttu-id="540c9-195">Zadania po lewej dla Ciebie jest dodanie logiki, która implementuje zadania tożsamości.</span><span class="sxs-lookup"><span data-stu-id="540c9-195">The only task left for you is to add the logic that implements identity tasks.</span></span>

<span data-ttu-id="540c9-196">W pierwszej kolejności należy wykonać w kodzie jest wprowadzenie wartości protokołu usługi Azure AD używane do identyfikowania Twojej aplikacji i zasobów przez docelowe.</span><span class="sxs-lookup"><span data-stu-id="540c9-196">The first thing you need to do in your code is introduce the protocol values that Azure AD uses for identifying your app and the resources that you target.</span></span> <span data-ttu-id="540c9-197">Te wartości ma być użyty do utworzenia tokenu żądania później.</span><span class="sxs-lookup"><span data-stu-id="540c9-197">Those values will be used to construct the token requests later on.</span></span> <span data-ttu-id="540c9-198">Wstaw następujący fragment kodu w górnej części pliku index.js:</span><span class="sxs-lookup"><span data-stu-id="540c9-198">Insert the following snippet at the top of the index.js file:</span></span>

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

<span data-ttu-id="540c9-199">`redirectUri` i `clientId` wartości powinna być zgodna wartości, które opisują aplikacji w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="540c9-199">The `redirectUri` and `clientId` values should match the values that describe your app in Azure AD.</span></span> <span data-ttu-id="540c9-200">Można znaleźć od **Konfiguruj** karcie w portalu Azure, zgodnie z opisem w kroku 1 we wcześniejszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="540c9-200">You can find those from the **Configure** tab in the Azure portal, as described in step 1 earlier in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="540c9-201">Jeśli zostanie wybrana opcja nie rejestruje nową aplikację w dzierżawie własnych, możesz po prostu wkleić wstępnie skonfigurowane wartości, ponieważ jest.</span><span class="sxs-lookup"><span data-stu-id="540c9-201">If you opted for not registering a new app in your own tenant, you can simply paste the preconfigured values as is.</span></span> <span data-ttu-id="540c9-202">Możesz sprawdzić, przykładowe uruchomiona, że należy zawsze tworzyć własne wejścia dla aplikacji, które są przeznaczone do produkcji.</span><span class="sxs-lookup"><span data-stu-id="540c9-202">You can then see the sample running, though you should always create your own entry for your apps that are meant for production.</span></span>

<span data-ttu-id="540c9-203">Następnie dodaj kod żądania tokenu.</span><span class="sxs-lookup"><span data-stu-id="540c9-203">Next, add the token request code.</span></span> <span data-ttu-id="540c9-204">Wstaw następujący fragment kodu między `search` i `renderData` definicje:</span><span class="sxs-lookup"><span data-stu-id="540c9-204">Insert the following snippet between the `search` and `renderData` definitions:</span></span>

```javascript
    // Shows the user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt to authorize the user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers the authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed to authenticate: " + err);
                });
            });
        });

    },
```
<span data-ttu-id="540c9-205">Przeanalizujmy tej funkcji, dzieląc go w dwie główne części.</span><span class="sxs-lookup"><span data-stu-id="540c9-205">Let's examine that function by breaking it down in its two main parts.</span></span>
<span data-ttu-id="540c9-206">Ten przykład jest przeznaczona do pracy z dowolnej dzierżawy, a nie jest powiązana z jedna z nich.</span><span class="sxs-lookup"><span data-stu-id="540c9-206">This sample is designed to work with any tenant, as opposed to being tied to a particular one.</span></span> <span data-ttu-id="540c9-207">Używa "/ wspólnej" punktu końcowego, który umożliwia użytkownikowi wprowadzenie dowolne konto podczas uwierzytelniania i kieruje żądanie do dzierżawy, w którym należy.</span><span class="sxs-lookup"><span data-stu-id="540c9-207">It uses the "/common" endpoint, which allows the user to enter any account at authentication time and directs the request to the tenant where it belongs.</span></span>

<span data-ttu-id="540c9-208">To pierwsza część metoda sprawdza ADAL pamięci podręcznej, aby zobaczyć, czy token jest już zapisana.</span><span class="sxs-lookup"><span data-stu-id="540c9-208">This first part of the method inspects the ADAL cache to see if a token is already stored.</span></span> <span data-ttu-id="540c9-209">Jeśli tak, metoda korzysta z dzierżawcami gdzie token pochodzeniu dla ponowne zainicjowanie biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="540c9-209">If so, the method uses the tenants where the token came from for reinitializing ADAL.</span></span> <span data-ttu-id="540c9-210">Jest to konieczne, aby uniknąć dodatkowych monitów, ponieważ użycie "/ wspólnej" zawsze powoduje pytaniem, użytkownik musi wprowadzić nowe konto.</span><span class="sxs-lookup"><span data-stu-id="540c9-210">This is necessary to avoid extra prompts, because the use of "/common" always results in asking the user to enter a new account.</span></span>

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
<span data-ttu-id="540c9-211">Druga część metoda wykonuje odpowiednie żądania tokenu.</span><span class="sxs-lookup"><span data-stu-id="540c9-211">The second part of the method performs the proper token request.</span></span> <span data-ttu-id="540c9-212">`acquireTokenSilentAsync` ADAL, aby zwrócić token dla określonego zasobu bez żadnych UX. przedstawiający zapyta — metoda</span><span class="sxs-lookup"><span data-stu-id="540c9-212">The `acquireTokenSilentAsync` method asks ADAL to return a token for the specified resource without showing any UX.</span></span> <span data-ttu-id="540c9-213">Który może się zdarzyć, jeśli pamięć podręczna ma już token dostępu odpowiedniego przechowywane, lub Jeśli token odświeżania może służyć do Uzyskaj token dostępu nowe bez wyświetlania dowolnego wiersza.</span><span class="sxs-lookup"><span data-stu-id="540c9-213">That can happen if the cache already has a suitable access token stored, or if a refresh token can be used to get a new access token without showing any prompt.</span></span> <span data-ttu-id="540c9-214">Jeśli kończy się niepowodzeniem, które firma Microsoft może wrócić `acquireTokenAsync`— które wizualnie monitują użytkownika do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="540c9-214">If that attempt fails, we fall back on `acquireTokenAsync`--which will visibly prompt the user to authenticate.</span></span>

```javascript
            // Attempt to authorize the user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers the authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed to authenticate: " + err);
                });
            });
```
<span data-ttu-id="540c9-215">Teraz, gdy mamy token możemy koniec wywołania interfejsu API programu Graph i wykonywać zapytania wyszukiwania, która ma.</span><span class="sxs-lookup"><span data-stu-id="540c9-215">Now that we have the token, we can finally invoke the Graph API and perform the search query that we want.</span></span> <span data-ttu-id="540c9-216">Wstaw następujący fragment kodu poniżej `authenticate` definicji:</span><span class="sxs-lookup"><span data-stu-id="540c9-216">Insert the following snippet below the `authenticate` definition:</span></span>

```javascript
// Makes an API call to receive the user list
    requestData: function (authResult, searchText) {
        var req = new XMLHttpRequest();
        var url = resourceUri + "/" + authResult.tenantId + "/users?api-version=" + graphApiVersion;
        url = searchText ? url + "&$filter=mailNickname eq '" + searchText + "'" : url + "&$top=10";

        req.open("GET", url, true);
        req.setRequestHeader('Authorization', 'Bearer ' + authResult.accessToken);

        req.onload = function(e) {
            if (e.target.status >= 200 && e.target.status < 300) {
                app.renderData(JSON.parse(e.target.response));
                return;
            }
            app.error('Data request failed: ' + e.target.response);
        };
        req.onerror = function(e) {
            app.error('Data request failed: ' + e.error);
        }

        req.send();
    },

```
<span data-ttu-id="540c9-217">Pliki punktu początkowego dostarczona proste UX wprowadzania alias użytkownika w polu tekstowym.</span><span class="sxs-lookup"><span data-stu-id="540c9-217">The starting-point files supplied a simple UX for entering a user's alias in a text box.</span></span> <span data-ttu-id="540c9-218">Ta metoda używa tej wartości do utworzenia kwerendy, połączyć ją z tokenu dostępu, wysyłają je do programu Microsoft Graph i przeanalizować wyniki.</span><span class="sxs-lookup"><span data-stu-id="540c9-218">This method uses that value to construct a query, combine it with the access token, send it to Microsoft Graph, and parse the results.</span></span> <span data-ttu-id="540c9-219">`renderData` Metody już istnieje w pliku punktu początkowego zajmuje się wizualizacja wyników.</span><span class="sxs-lookup"><span data-stu-id="540c9-219">The `renderData` method, already present in the starting-point file, takes care of visualizing the results.</span></span>

## <a name="step-5-run-the-app"></a><span data-ttu-id="540c9-220">Krok 5: Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="540c9-220">Step 5: Run the app</span></span>
<span data-ttu-id="540c9-221">Aplikacja jest ostatecznie gotowy do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="540c9-221">Your app is finally ready to run.</span></span> <span data-ttu-id="540c9-222">Jego działania jest prosty: po uruchomieniu aplikacji, wprowadź alias użytkownika, aby wyszukać, a następnie kliknij przycisk.</span><span class="sxs-lookup"><span data-stu-id="540c9-222">Operating it is simple: when the app starts, enter the alias of the user you want to look up, and then click the button.</span></span> <span data-ttu-id="540c9-223">Zostanie wyświetlony monit o uwierzytelnienie.</span><span class="sxs-lookup"><span data-stu-id="540c9-223">You're prompted for authentication.</span></span> <span data-ttu-id="540c9-224">Po pomyślnym uwierzytelnieniu i pomyślne wyszukiwania atrybutów wyszukiwanych użytkowników są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="540c9-224">Upon successful authentication and successful search, the attributes of the searched user are displayed.</span></span>

<span data-ttu-id="540c9-225">Kolejnych uruchomieniach przeprowadzi wyszukiwanie bez wyświetlania dowolnego wiersza dzięki użyciu obecności wcześniej nabytych przez niego tokenu w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="540c9-225">Subsequent runs will perform the search without showing any prompt, thanks to the presence of the previously acquired token in cache.</span></span>

<span data-ttu-id="540c9-226">Konkretne kroki dotyczące uruchamiania aplikacji zależy od platformy.</span><span class="sxs-lookup"><span data-stu-id="540c9-226">The concrete steps for running the app vary by platform.</span></span>

### <a name="windows-10"></a><span data-ttu-id="540c9-227">Windows 10</span><span class="sxs-lookup"><span data-stu-id="540c9-227">Windows 10</span></span>
   <span data-ttu-id="540c9-228">Komputer typu Tablet:`cordova run windows --archs=x64 -- --appx=uap`</span><span class="sxs-lookup"><span data-stu-id="540c9-228">Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`</span></span>

   <span data-ttu-id="540c9-229">Urządzenie przenośne (wymaga systemu Windows 10 Mobile urządzenie podłączone do komputera z systemem):`cordova run windows --archs=arm -- --appx=uap --phone`</span><span class="sxs-lookup"><span data-stu-id="540c9-229">Mobile (requires a Windows 10 Mobile device connected to a PC): `cordova run windows --archs=arm -- --appx=uap --phone`</span></span>

   > [!NOTE]
   > <span data-ttu-id="540c9-230">Przy pierwszym uruchomieniu może zostać poproszona o logowania licencji dewelopera.</span><span class="sxs-lookup"><span data-stu-id="540c9-230">During the first run, you might be asked to sign in for a developer license.</span></span> <span data-ttu-id="540c9-231">Aby uzyskać więcej informacji, zobacz [licencji dewelopera](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="540c9-231">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-81-tabletpc"></a><span data-ttu-id="540c9-232">Komputer typu Tablet Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="540c9-232">Windows 8.1 Tablet/PC</span></span>
   `cordova run windows`

   > [!NOTE]
   > <span data-ttu-id="540c9-233">Przy pierwszym uruchomieniu może zostać poproszona o logowania licencji dewelopera.</span><span class="sxs-lookup"><span data-stu-id="540c9-233">During the first run, you might be asked to sign in for a developer license.</span></span> <span data-ttu-id="540c9-234">Aby uzyskać więcej informacji, zobacz [licencji dewelopera](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="540c9-234">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-phone-81"></a><span data-ttu-id="540c9-235">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="540c9-235">Windows Phone 8.1</span></span>
   <span data-ttu-id="540c9-236">Aby uruchomić na połączonym urządzeniu:`cordova run windows --device -- --phone`</span><span class="sxs-lookup"><span data-stu-id="540c9-236">To run on a connected device: `cordova run windows --device -- --phone`</span></span>

   <span data-ttu-id="540c9-237">Aby uruchomić emulatora domyślne:`cordova emulate windows -- --phone`</span><span class="sxs-lookup"><span data-stu-id="540c9-237">To run on the default emulator: `cordova emulate windows -- --phone`</span></span>

   <span data-ttu-id="540c9-238">Użyj `cordova run windows --list -- --phone` Aby wyświetlić wszystkie dostępne elementy docelowe i `cordova run windows --target=<target_name> -- --phone` do uruchamiania aplikacji dla określonego urządzenia lub emulatora (na przykład `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span><span class="sxs-lookup"><span data-stu-id="540c9-238">Use `cordova run windows --list -- --phone` to see all available targets and `cordova run windows --target=<target_name> -- --phone` to run the application on a specific device or emulator (for example, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span></span>

### <a name="android"></a><span data-ttu-id="540c9-239">Android</span><span class="sxs-lookup"><span data-stu-id="540c9-239">Android</span></span>
   <span data-ttu-id="540c9-240">Aby uruchomić na połączonym urządzeniu:`cordova run android --device`</span><span class="sxs-lookup"><span data-stu-id="540c9-240">To run on a connected device: `cordova run android --device`</span></span>

   <span data-ttu-id="540c9-241">Aby uruchomić emulatora domyślne:`cordova emulate android`</span><span class="sxs-lookup"><span data-stu-id="540c9-241">To run on the default emulator: `cordova emulate android`</span></span>

   <span data-ttu-id="540c9-242">Upewnij się, że po utworzeniu wystąpienia emulatora za pomocą Menedżera AVD, zgodnie z wcześniejszym opisem w sekcji "Wymagania wstępne".</span><span class="sxs-lookup"><span data-stu-id="540c9-242">Make sure you've created an emulator instance by using AVD Manager, as described earlier in the "Prerequisites" section.</span></span>

   <span data-ttu-id="540c9-243">Użyj `cordova run android --list` Aby wyświetlić wszystkie dostępne elementy docelowe i `cordova run android --target=<target_name>` do uruchamiania aplikacji dla określonego urządzenia lub emulatora (na przykład `cordova run android --target="Nexus4_emulator"`).</span><span class="sxs-lookup"><span data-stu-id="540c9-243">Use `cordova run android --list` to see all available targets and `cordova run android --target=<target_name>` to run the application on a specific device or emulator (for example, `cordova run android --target="Nexus4_emulator"`).</span></span>

### <a name="ios"></a><span data-ttu-id="540c9-244">iOS</span><span class="sxs-lookup"><span data-stu-id="540c9-244">iOS</span></span>
   <span data-ttu-id="540c9-245">Aby uruchomić na połączonym urządzeniu:`cordova run ios --device`</span><span class="sxs-lookup"><span data-stu-id="540c9-245">To run on a connected device: `cordova run ios --device`</span></span>

   <span data-ttu-id="540c9-246">Aby uruchomić emulatora domyślne:`cordova emulate ios`</span><span class="sxs-lookup"><span data-stu-id="540c9-246">To run on the default emulator: `cordova emulate ios`</span></span>

   > [!NOTE]
   > <span data-ttu-id="540c9-247">Upewnij się, że masz `ios-sim` zainstalowane do uruchamiania na emulatorze pakietu.</span><span class="sxs-lookup"><span data-stu-id="540c9-247">Make sure you have the `ios-sim` package installed to run on the emulator.</span></span> <span data-ttu-id="540c9-248">Aby uzyskać więcej informacji zobacz sekcję "Wymagania wstępne".</span><span class="sxs-lookup"><span data-stu-id="540c9-248">For more information, see the "Prerequisites" section.</span></span>

    Use `cordova run ios --list` to see all available targets and `cordova run ios --target=<target_name>` to run the application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` to see additional build and run options.

## <a name="next-steps"></a><span data-ttu-id="540c9-249">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="540c9-249">Next steps</span></span>
<span data-ttu-id="540c9-250">Odwołanie, ukończonych próbka (bez wartości konfiguracji) są dostępne w [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span><span class="sxs-lookup"><span data-stu-id="540c9-250">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span></span>

<span data-ttu-id="540c9-251">Możesz teraz przejść do bardziej zaawansowanych (i bardziej interesującego) scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="540c9-251">You can now move on to more advanced (and more interesting) scenarios.</span></span> <span data-ttu-id="540c9-252">Możesz spróbować: [zabezpieczyć interfejs API sieci Web Node.js w usłudze Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="540c9-252">You might want to try: [Secure a Node.js Web API with Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
