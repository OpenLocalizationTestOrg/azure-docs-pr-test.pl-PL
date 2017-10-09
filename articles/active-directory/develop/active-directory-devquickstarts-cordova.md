---
title: aaaAzure AD Cordova wprowadzenie | Dokumentacja firmy Microsoft
description: "Jak toobuild aplikacji Cordova integruje się z usługą Azure AD, logowania i wywołuje Azure interfejsów API, które są chronione przez usługi AD za pomocą uwierzytelniania OAuth."
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
ms.openlocfilehash: 573ed638c2180c5231648bcb8c49ceb6f53296f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a><span data-ttu-id="2b71a-103">Integrowanie usługi Azure AD z Apache aplikacji Cordova</span><span class="sxs-lookup"><span data-stu-id="2b71a-103">Integrate Azure AD with an Apache Cordova app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="2b71a-104">Można użyć oprogramowania Apache Cordova toodevelop HTML5/JavaScript aplikacji, które można uruchamiać na urządzeniach przenośnych jako pełni funkcjonalnymi natywnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2b71a-104">You can use Apache Cordova toodevelop HTML5/JavaScript applications that can run on mobile devices as full-fledged native applications.</span></span> <span data-ttu-id="2b71a-105">Usłudze Azure Active Directory (Azure AD) można dodać aplikacje Cordova tooyour możliwości uwierzytelniania korporacyjnej.</span><span class="sxs-lookup"><span data-stu-id="2b71a-105">With Azure Active Directory (Azure AD), you can add enterprise-grade authentication capabilities tooyour Cordova applications.</span></span>

<span data-ttu-id="2b71a-106">Wtyczka Cordova opakowuje Azure AD natywnych zestawów SDK w systemach iOS, Android, Sklep Windows i Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="2b71a-106">A Cordova plug-in wraps Azure AD native SDKs on iOS, Android, Windows Store, and Windows Phone.</span></span> <span data-ttu-id="2b71a-107">Za pomocą, że dodatek plug-in, można rozszerzyć aplikacji toosupport logowanie przy użyciu kont usługi Active Directory systemu Windows Server użytkowników, uzyskanie dostępu do tooOffice 365 i interfejsów API usługi Azure, a nawet chronić wywołania tooyour własny niestandardowy interfejs API sieci web.</span><span class="sxs-lookup"><span data-stu-id="2b71a-107">By using that plug-in, you can enhance your application toosupport sign-in with your users' Windows Server Active Directory accounts, gain access tooOffice 365 and Azure APIs, and even help protect calls tooyour own custom web API.</span></span>

<span data-ttu-id="2b71a-108">W tym samouczku użyjemy hello Apache Cordova wtyczki dla Active Directory Authentication Library (ADAL) tooimprove prostej aplikacji przez dodanie hello następujące funkcje:</span><span class="sxs-lookup"><span data-stu-id="2b71a-108">In this tutorial, we'll use hello Apache Cordova plug-in for Active Directory Authentication Library (ADAL) tooimprove a simple app by adding hello following features:</span></span>

* <span data-ttu-id="2b71a-109">Przy użyciu kilku wierszy kodu uwierzytelniania użytkownika i uzyskania tokenu.</span><span class="sxs-lookup"><span data-stu-id="2b71a-109">With just a few lines of code, authenticate a user and obtain a token.</span></span>
* <span data-ttu-id="2b71a-110">Użyj tego tokenu tooinvoke hello interfejsu API programu Graph tooquery tego katalogu i wyświetlić wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="2b71a-110">Use that token tooinvoke hello Graph API tooquery that directory and display hello results.</span></span>  
* <span data-ttu-id="2b71a-111">Użyj hello pamięci podręcznej tokenu ADAL toominimize uwierzytelniania wyświetli monit dla użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="2b71a-111">Use hello ADAL token cache toominimize authentication prompts for hello user.</span></span>

<span data-ttu-id="2b71a-112">toomake tych ulepszeń, konieczne jest:</span><span class="sxs-lookup"><span data-stu-id="2b71a-112">toomake those improvements, you need to:</span></span>

1. <span data-ttu-id="2b71a-113">Zarejestrować aplikację w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b71a-113">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="2b71a-114">Dodaj kod tooyour aplikacji toorequest tokenów.</span><span class="sxs-lookup"><span data-stu-id="2b71a-114">Add code tooyour app toorequest tokens.</span></span>
3. <span data-ttu-id="2b71a-115">Dodaj token hello toouse kodu na potrzeby zapytań hello interfejsu API programu Graph i wyświetlić wyniki.</span><span class="sxs-lookup"><span data-stu-id="2b71a-115">Add code toouse hello token for querying hello Graph API and display results.</span></span>
4. <span data-ttu-id="2b71a-116">Utwórz projekt wdrożenia oprogramowania Cordova hello na wszystkich platformach hello mają tootarget, Dodaj hello ADAL Cordova wtyczki i testować rozwiązanie hello w emulatory.</span><span class="sxs-lookup"><span data-stu-id="2b71a-116">Create hello Cordova deployment project with all hello platforms you want tootarget, add hello Cordova ADAL plug-in, and test hello solution in emulators.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b71a-117">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2b71a-117">Prerequisites</span></span>
<span data-ttu-id="2b71a-118">toocomplete tego samouczka należy:</span><span class="sxs-lookup"><span data-stu-id="2b71a-118">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="2b71a-119">Dzierżawa usługi Azure AD, gdzie masz konto z uprawnieniami rozwoju aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2b71a-119">An Azure AD tenant where you have an account with app development rights.</span></span>
* <span data-ttu-id="2b71a-120">Środowisko deweloperskie, który skonfigurował toouse Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="2b71a-120">A development environment that's configured toouse Apache Cordova.</span></span>  

<span data-ttu-id="2b71a-121">Jeśli masz zarówno już skonfigurowany, przejdź bezpośrednio toostep 1.</span><span class="sxs-lookup"><span data-stu-id="2b71a-121">If you have both already set up, proceed directly toostep 1.</span></span>

<span data-ttu-id="2b71a-122">Jeśli nie masz dzierżawę usługi Azure AD, użyj hello [instrukcje na temat tooget jedną](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="2b71a-122">If you don't have an Azure AD tenant, use hello [instructions on how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="2b71a-123">Jeśli nie masz Apache Cordova na komputerze, należy zainstalować następujące hello:</span><span class="sxs-lookup"><span data-stu-id="2b71a-123">If you don't have Apache Cordova set up on your machine, install hello following:</span></span>

* [<span data-ttu-id="2b71a-124">Git</span><span class="sxs-lookup"><span data-stu-id="2b71a-124">Git</span></span>](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [<span data-ttu-id="2b71a-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="2b71a-125">Node.js</span></span>](https://nodejs.org/download/)
* <span data-ttu-id="2b71a-126">[Interfejs Cordova CLI](https://cordova.apache.org/) (można łatwo zainstalować za pomocą Menedżera pakietów NPM: `npm install -g cordova`)</span><span class="sxs-lookup"><span data-stu-id="2b71a-126">[Cordova CLI](https://cordova.apache.org/) (can be easily installed via NPM package manager: `npm install -g cordova`)</span></span>

<span data-ttu-id="2b71a-127">Witaj poprzedzających instalacji powinny działać zarówno na powitania komputerze i na powitania Mac.</span><span class="sxs-lookup"><span data-stu-id="2b71a-127">hello preceding installations should work both on hello PC and on hello Mac.</span></span>

<span data-ttu-id="2b71a-128">Każda platforma docelowa ma inne wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="2b71a-128">Each target platform has different prerequisites:</span></span>

* <span data-ttu-id="2b71a-129">toobuild i uruchom aplikację dla komputerów typu Tablet z systemem Windows lub Windows Phone:</span><span class="sxs-lookup"><span data-stu-id="2b71a-129">toobuild and run an app for Windows Tablet/PC or Windows Phone:</span></span>
  * <span data-ttu-id="2b71a-130">Zainstaluj [programu Visual Studio 2013 dla systemu Windows z Update 2 lub nowszym](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express lub inna wersja) lub [programu Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span><span class="sxs-lookup"><span data-stu-id="2b71a-130">Install [Visual Studio 2013 for Windows with Update 2 or later](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express or another version) or [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span></span>

* <span data-ttu-id="2b71a-131">toobuild i uruchom aplikację dla systemu iOS:</span><span class="sxs-lookup"><span data-stu-id="2b71a-131">toobuild and run an app for iOS:</span></span>

  * <span data-ttu-id="2b71a-132">Zainstaluj program Xcode 6.x lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="2b71a-132">Install Xcode 6.x or later.</span></span> <span data-ttu-id="2b71a-133">Pobierz go z hello [witryny dla deweloperów firmy Apple](http://developer.apple.com/downloads) lub hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span><span class="sxs-lookup"><span data-stu-id="2b71a-133">Download it from hello [Apple Developer site](http://developer.apple.com/downloads) or hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span></span>
  * <span data-ttu-id="2b71a-134">Zainstaluj [ios-sim](https://www.npmjs.org/package/ios-sim).</span><span class="sxs-lookup"><span data-stu-id="2b71a-134">Install [ios-sim](https://www.npmjs.org/package/ios-sim).</span></span> <span data-ttu-id="2b71a-135">Umożliwia aplikacji systemu iOS toostart w symulatorze systemu iOS z wiersza polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="2b71a-135">You can use it toostart iOS apps in iOS Simulator from hello command line.</span></span> <span data-ttu-id="2b71a-136">(Można łatwo zainstalować ją za pomocą hello terminala: `npm install -g ios-sim`.)</span><span class="sxs-lookup"><span data-stu-id="2b71a-136">(You can easily install it via hello terminal: `npm install -g ios-sim`.)</span></span>
* <span data-ttu-id="2b71a-137">toobuild i uruchom aplikację dla systemu Android:</span><span class="sxs-lookup"><span data-stu-id="2b71a-137">toobuild and run an app for Android:</span></span>

  * <span data-ttu-id="2b71a-138">Zainstaluj [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="2b71a-138">Install [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or later.</span></span> <span data-ttu-id="2b71a-139">Upewnij się, że `JAVA_HOME` (zmienną środowiskową) jest prawidłowo ustawiona zgodnie z ścieżki instalacji JDK toohello (na przykład C:\Program Files\Java\jdk1.7.0_75).</span><span class="sxs-lookup"><span data-stu-id="2b71a-139">Make sure `JAVA_HOME` (environment variable) is correctly set according toohello JDK installation path (for example, C:\Program Files\Java\jdk1.7.0_75).</span></span>
  * <span data-ttu-id="2b71a-140">Zainstaluj [zestawu SDK systemu Android](http://developer.android.com/sdk/installing/index.html?pkg=tools) i Dodaj hello `<android-sdk-location>\tools` tooyour lokalizacji (na przykład C:\tools\Android\android-sdk\tools) `PATH` zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="2b71a-140">Install [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) and add hello `<android-sdk-location>\tools` location (for example, C:\tools\Android\android-sdk\tools) tooyour `PATH` environment variable.</span></span>
  * <span data-ttu-id="2b71a-141">Otwórz Menedżera zestawu SDK systemu Android (na przykład za pośrednictwem hello terminala: `android`) i zainstalować:</span><span class="sxs-lookup"><span data-stu-id="2b71a-141">Open Android SDK Manager (for example, via hello terminal: `android`) and install:</span></span>
    * <span data-ttu-id="2b71a-142">*5.0.1 systemu android (interfejs API 21)* zestawu SDK platformy</span><span class="sxs-lookup"><span data-stu-id="2b71a-142">*Android 5.0.1 (API 21)* platform SDK</span></span>
    * <span data-ttu-id="2b71a-143">*Narzędzia kompilacji zestawu SDK dla systemu android* wersji 19.1.0 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="2b71a-143">*Android SDK Build Tools* version 19.1.0 or later</span></span>
    * <span data-ttu-id="2b71a-144">*Obsługa systemu android repozytorium* (dodatki)</span><span class="sxs-lookup"><span data-stu-id="2b71a-144">*Android Support Repository* (Extras)</span></span>

  <span data-ttu-id="2b71a-145">Witaj zestawu SDK systemu Android nie zapewnia żadnych domyślne wystąpienie emulatora.</span><span class="sxs-lookup"><span data-stu-id="2b71a-145">hello Android SDK doesn't provide any default emulator instance.</span></span> <span data-ttu-id="2b71a-146">Utworzyć, uruchamiając `android avd` z hello terminali, a następnie wybierając **Utwórz**, jeśli chcesz, aby toorun hello aplikacji systemu Android na emulatorze.</span><span class="sxs-lookup"><span data-stu-id="2b71a-146">Create one by running `android avd` from hello terminal and then selecting **Create**, if you want toorun hello Android app on an emulator.</span></span> <span data-ttu-id="2b71a-147">Zaleca się poziom interfejsu API 19 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="2b71a-147">We recommend an API level of 19 or higher.</span></span> <span data-ttu-id="2b71a-148">Aby uzyskać więcej informacji na temat hello Android opcje emulatora i tworzenia, zobacz [Menedżera AVD](http://developer.android.com/tools/help/avd-manager.html) na powitania witryny systemu Android.</span><span class="sxs-lookup"><span data-stu-id="2b71a-148">For more information about hello Android emulator and creation options, see [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) on hello Android site.</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="2b71a-149">Krok 1: Rejestrowanie aplikacji w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b71a-149">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="2b71a-150">Ten krok jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="2b71a-150">This step is optional.</span></span> <span data-ttu-id="2b71a-151">Ten samouczek zawiera wstępnie przygotowany wartości, których można używać toosee hello przykładowe działanie bez wykonywania żadnych alokacji w własne dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="2b71a-151">This tutorial provides pre-provisioned values that you can use toosee hello sample in action without doing any provisioning in your own tenant.</span></span> <span data-ttu-id="2b71a-152">Jednak zaleca się wykonać ten krok i zapoznać się z procesem hello, ponieważ będzie wymagane podczas tworzenia własnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2b71a-152">However, we recommend that you do perform this step and become familiar with hello process, because it will be required when you create your own applications.</span></span>

<span data-ttu-id="2b71a-153">Usługa Azure AD wystawia tokeny tooonly znane aplikacje.</span><span class="sxs-lookup"><span data-stu-id="2b71a-153">Azure AD issues tokens tooonly known applications.</span></span> <span data-ttu-id="2b71a-154">Zanim użyjesz usługi Azure AD z aplikacji, należy toocreate wpis dla niego w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="2b71a-154">Before you can use Azure AD from your app, you need toocreate an entry for it in your tenant.</span></span> <span data-ttu-id="2b71a-155">tooregister nową aplikację w dzierżawie:</span><span class="sxs-lookup"><span data-stu-id="2b71a-155">tooregister a new application in your tenant:</span></span>

1. <span data-ttu-id="2b71a-156">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2b71a-156">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2b71a-157">Na górnym pasku powitania kliknij swoje konto.</span><span class="sxs-lookup"><span data-stu-id="2b71a-157">On hello top bar, click your account.</span></span> <span data-ttu-id="2b71a-158">W hello **katalogu** wybierz dzierżawy usługi Azure AD hello miejscu tooregister aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2b71a-158">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="2b71a-159">Kliknij przycisk **więcej usług** w lewym okienku hello, a następnie wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2b71a-159">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="2b71a-160">Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2b71a-160">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="2b71a-161">Postępuj zgodnie z monitami hello i Utwórz **natywną aplikację kliencką**.</span><span class="sxs-lookup"><span data-stu-id="2b71a-161">Follow hello prompts and create a **Native Client Application**.</span></span> <span data-ttu-id="2b71a-162">(Chociaż aplikacje Cordova HTML na podstawie, tworzymy aplikację native client w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="2b71a-162">(Although Cordova apps are HTML based, we're creating a native client application here.</span></span> <span data-ttu-id="2b71a-163">Witaj **natywną aplikację kliencką** musi być zaznaczona opcja lub aplikacji hello nie będzie działać.)</span><span class="sxs-lookup"><span data-stu-id="2b71a-163">hello **Native Client Application** option must be selected, or hello application won't work.)</span></span>
  * <span data-ttu-id="2b71a-164">**Nazwa** opisuje toousers Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2b71a-164">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="2b71a-165">**Identyfikator URI przekierowania** jest hello identyfikator URI, który został użyty tooreturn tokenów tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2b71a-165">**Redirect URI** is hello URI that's used tooreturn tokens tooyour app.</span></span> <span data-ttu-id="2b71a-166">Wprowadź **http://MyDirectorySearcherApp**.</span><span class="sxs-lookup"><span data-stu-id="2b71a-166">Enter **http://MyDirectorySearcherApp**.</span></span>

<span data-ttu-id="2b71a-167">Po zakończeniu rejestracji usługi Azure AD przypisuje aplikacji Unikatowy identyfikator tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2b71a-167">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span> <span data-ttu-id="2b71a-168">Tę wartość w kolejnych sekcjach hello jest potrzebny.</span><span class="sxs-lookup"><span data-stu-id="2b71a-168">You’ll need this value in hello next sections.</span></span> <span data-ttu-id="2b71a-169">Znajdziesz ją na karcie aplikacji hello hello nowo utworzona aplikacja.</span><span class="sxs-lookup"><span data-stu-id="2b71a-169">You can find it on hello application tab of hello newly created app.</span></span>

<span data-ttu-id="2b71a-170">toorun `DirSearchClient Sample`, przyznaj hello nowo utworzona aplikacja uprawnienia tooquery hello Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="2b71a-170">toorun `DirSearchClient Sample`, grant hello newly created app permission tooquery hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="2b71a-171">Z hello **ustawienia** wybierz pozycję **wymagane uprawnienia**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2b71a-171">From hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>  
2. <span data-ttu-id="2b71a-172">Hello aplikacji usługi Azure Active Directory, można wybrać **Microsoft Graph** jako hello interfejsu API i Dodaj hello **dostępu do katalogu hello jako hello zalogowanego użytkownika** uprawnienie w obszarze **delegowani Uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="2b71a-172">For hello Azure Active Directory application, select **Microsoft Graph** as hello API and add hello **Access hello directory as hello signed-in user** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="2b71a-173">Dzięki temu Twojej hello tooquery aplikacji interfejsu API programu Graph dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2b71a-173">This enables your application tooquery hello Graph API for users.</span></span>

## <a name="step-2-clone-hello-sample-app-repository"></a><span data-ttu-id="2b71a-174">Krok 2: Klonuj repozytorium aplikacji przykładowej hello</span><span class="sxs-lookup"><span data-stu-id="2b71a-174">Step 2: Clone hello sample app repository</span></span>
<span data-ttu-id="2b71a-175">Z powłoki lub wiersza polecenia wpisz hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="2b71a-175">From your shell or command line, type hello following command:</span></span>

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-hello-cordova-app"></a><span data-ttu-id="2b71a-176">Krok 3: Tworzenie aplikacji platformy Cordova hello</span><span class="sxs-lookup"><span data-stu-id="2b71a-176">Step 3: Create hello Cordova app</span></span>
<span data-ttu-id="2b71a-177">Istnieje wiele sposobów toocreate Cordova aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2b71a-177">There are multiple ways toocreate Cordova applications.</span></span> <span data-ttu-id="2b71a-178">W tym samouczku użyjemy hello Cordova-interfejsu wiersza polecenia (CLI).</span><span class="sxs-lookup"><span data-stu-id="2b71a-178">In this tutorial, we'll use hello Cordova command-line interface (CLI).</span></span>

1. <span data-ttu-id="2b71a-179">Z powłoki lub wiersza polecenia wpisz hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="2b71a-179">From your shell or command line, type hello following command:</span></span>

        cordova create DirSearchClient

   <span data-ttu-id="2b71a-180">To polecenie tworzy hello struktury folderów i funkcją szkieletów dla projektu Cordova hello.</span><span class="sxs-lookup"><span data-stu-id="2b71a-180">That command creates hello folder structure and scaffolding for hello Cordova project.</span></span>

2. <span data-ttu-id="2b71a-181">Przenieść nowego folderu DirSearchClient toohello:</span><span class="sxs-lookup"><span data-stu-id="2b71a-181">Move toohello new DirSearchClient folder:</span></span>

        cd .\DirSearchClient

3. <span data-ttu-id="2b71a-182">Skopiuj zawartość hello hello początkowego projektu w podfolderze www hello przy użyciu Menedżera plików lub hello następujące polecenia powłoki:</span><span class="sxs-lookup"><span data-stu-id="2b71a-182">Copy hello content of hello starter project in hello www subfolder by using a file manager or hello following command in your shell:</span></span>

  * <span data-ttu-id="2b71a-183">System Windows:`xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span><span class="sxs-lookup"><span data-stu-id="2b71a-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span></span>
  * <span data-ttu-id="2b71a-184">Mac:`cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span><span class="sxs-lookup"><span data-stu-id="2b71a-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span></span>

4. <span data-ttu-id="2b71a-185">Dodaj dozwolonych hello wtyczki.</span><span class="sxs-lookup"><span data-stu-id="2b71a-185">Add hello whitelist plug-in.</span></span> <span data-ttu-id="2b71a-186">Jest to konieczne do wywoływania hello interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="2b71a-186">This is necessary for invoking hello Graph API.</span></span>

        cordova plugin add cordova-plugin-whitelist

5. <span data-ttu-id="2b71a-187">Dodaj wszystkie platformy hello, które mają toosupport.</span><span class="sxs-lookup"><span data-stu-id="2b71a-187">Add all hello platforms that you want toosupport.</span></span> <span data-ttu-id="2b71a-188">toohave próbki roboczej, należy tooexecute co najmniej jeden hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="2b71a-188">toohave a working sample, you need tooexecute at least one of hello following commands.</span></span> <span data-ttu-id="2b71a-189">Może nie być możliwe tooemulate z systemem iOS w systemie Windows lub emulacji systemu Windows na komputerach Mac.</span><span class="sxs-lookup"><span data-stu-id="2b71a-189">Note that you won't be able tooemulate iOS on Windows or emulate Windows on a Mac.</span></span>

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. <span data-ttu-id="2b71a-190">Dodaj hello biblioteki ADAL dla projektu tooyour wtyczki Cordova:</span><span class="sxs-lookup"><span data-stu-id="2b71a-190">Add hello ADAL for Cordova plug-in tooyour project:</span></span>

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-tooauthenticate-users-and-obtain-tokens-from-azure-ad"></a><span data-ttu-id="2b71a-191">Krok 4: Dodaj kod tooauthenticate użytkowników i uzyskać tokeny z usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b71a-191">Step 4: Add code tooauthenticate users and obtain tokens from Azure AD</span></span>
<span data-ttu-id="2b71a-192">Projektujesz w tym samouczku aplikacji Hello zapewni funkcji wyszukiwania prostego katalogu.</span><span class="sxs-lookup"><span data-stu-id="2b71a-192">hello application that you're developing in this tutorial will provide a simple directory search feature.</span></span> <span data-ttu-id="2b71a-193">Użytkownik Hello może, a następnie wpisz alias hello każdego użytkownika w katalogu hello i wizualizacji niektóre podstawowe atrybuty.</span><span class="sxs-lookup"><span data-stu-id="2b71a-193">hello user can then type hello alias of any user in hello directory and visualize some basic attributes.</span></span> <span data-ttu-id="2b71a-194">Projekt starter Hello zawiera definicję hello hello podstawowy interfejs użytkownika aplikacji hello (w www/index.html) i rusztowania hello, który tworzącej zdarzeń Podstawowa aplikacja cykli powiązania interfejsu użytkownika i powoduje wyświetlanie logikę (www/js/index.js).</span><span class="sxs-lookup"><span data-stu-id="2b71a-194">hello starter project contains hello definition of hello basic user interface of hello app (in www/index.html) and hello scaffolding that wires up basic app event cycles, user interface bindings, and results display logic (in www/js/index.js).</span></span> <span data-ttu-id="2b71a-195">Witaj zadań tylko dla Ciebie w lewo jest tooadd hello logikę, która implementuje zadania tożsamości.</span><span class="sxs-lookup"><span data-stu-id="2b71a-195">hello only task left for you is tooadd hello logic that implements identity tasks.</span></span>

<span data-ttu-id="2b71a-196">Witaj najpierw należy toodo w kodzie jest wprowadzenie wartości protokołu hello, używane do identyfikacji aplikacji usługi Azure AD i hello zasoby docelowe.</span><span class="sxs-lookup"><span data-stu-id="2b71a-196">hello first thing you need toodo in your code is introduce hello protocol values that Azure AD uses for identifying your app and hello resources that you target.</span></span> <span data-ttu-id="2b71a-197">Te wartości będą używane tooconstruct hello token żądania później.</span><span class="sxs-lookup"><span data-stu-id="2b71a-197">Those values will be used tooconstruct hello token requests later on.</span></span> <span data-ttu-id="2b71a-198">Wstaw powitania po fragment u góry pliku index.js hello hello:</span><span class="sxs-lookup"><span data-stu-id="2b71a-198">Insert hello following snippet at hello top of hello index.js file:</span></span>

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

<span data-ttu-id="2b71a-199">Witaj `redirectUri` i `clientId` wartości powinna być zgodna hello wartości, które opisują aplikacji w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b71a-199">hello `redirectUri` and `clientId` values should match hello values that describe your app in Azure AD.</span></span> <span data-ttu-id="2b71a-200">Można znaleźć od hello **Konfiguruj** karcie hello portalu Azure, zgodnie z opisem w kroku 1 we wcześniejszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="2b71a-200">You can find those from hello **Configure** tab in hello Azure portal, as described in step 1 earlier in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="2b71a-201">Jeśli zostanie wybrana opcja nie rejestruje nową aplikację w dzierżawie własnych, możesz po prostu wkleić hello wstępnie wartości, ponieważ jest.</span><span class="sxs-lookup"><span data-stu-id="2b71a-201">If you opted for not registering a new app in your own tenant, you can simply paste hello preconfigured values as is.</span></span> <span data-ttu-id="2b71a-202">Możesz sprawdzić hello uruchomiona próbki, że należy zawsze tworzyć własne wejścia dla aplikacji, które są przeznaczone do produkcji.</span><span class="sxs-lookup"><span data-stu-id="2b71a-202">You can then see hello sample running, though you should always create your own entry for your apps that are meant for production.</span></span>

<span data-ttu-id="2b71a-203">Następnie dodaj kod, hello żądania tokenu.</span><span class="sxs-lookup"><span data-stu-id="2b71a-203">Next, add hello token request code.</span></span> <span data-ttu-id="2b71a-204">Wstaw powitania po fragment między hello `search` i `renderData` definicje:</span><span class="sxs-lookup"><span data-stu-id="2b71a-204">Insert hello following snippet between hello `search` and `renderData` definitions:</span></span>

```javascript
    // Shows hello user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
        });

    },
```
<span data-ttu-id="2b71a-205">Przeanalizujmy tej funkcji, dzieląc go w dwie główne części.</span><span class="sxs-lookup"><span data-stu-id="2b71a-205">Let's examine that function by breaking it down in its two main parts.</span></span>
<span data-ttu-id="2b71a-206">Ten przykład jest zaprojektowana toowork z dowolnej dzierżawy jako min. toobeing powiązane tooa jedna z nich.</span><span class="sxs-lookup"><span data-stu-id="2b71a-206">This sample is designed toowork with any tenant, as opposed toobeing tied tooa particular one.</span></span> <span data-ttu-id="2b71a-207">Używa powitania "/ wspólnej" punktu końcowego, który umożliwia tooenter użytkownika hello dowolne konto podczas uwierzytelniania i kieruje hello żądania toohello dzierżawy, w której należy.</span><span class="sxs-lookup"><span data-stu-id="2b71a-207">It uses hello "/common" endpoint, which allows hello user tooenter any account at authentication time and directs hello request toohello tenant where it belongs.</span></span>

<span data-ttu-id="2b71a-208">To pierwsza część metody hello sprawdza hello toosee pamięci podręcznej biblioteki ADAL, jeśli token jest już zapisana.</span><span class="sxs-lookup"><span data-stu-id="2b71a-208">This first part of hello method inspects hello ADAL cache toosee if a token is already stored.</span></span> <span data-ttu-id="2b71a-209">Jeśli tak, metoda hello używa dzierżaw hello gdzie hello token pochodzeniu dla ponowne zainicjowanie biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="2b71a-209">If so, hello method uses hello tenants where hello token came from for reinitializing ADAL.</span></span> <span data-ttu-id="2b71a-210">To jest konieczne tooavoid dodatkowych monitów, ponieważ hello Użyj "/ wspólnej" zawsze powoduje pytaniem hello tooenter użytkownika, nowe konto.</span><span class="sxs-lookup"><span data-stu-id="2b71a-210">This is necessary tooavoid extra prompts, because hello use of "/common" always results in asking hello user tooenter a new account.</span></span>

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
<span data-ttu-id="2b71a-211">Hello drugiej części hello metoda wykonuje hello odpowiednie żądania tokenu.</span><span class="sxs-lookup"><span data-stu-id="2b71a-211">hello second part of hello method performs hello proper token request.</span></span> <span data-ttu-id="2b71a-212">Hello `acquireTokenSilentAsync` metody wprowadza się ADAL tooreturn token hello określony zasób bez wyświetlania dowolnego UX.</span><span class="sxs-lookup"><span data-stu-id="2b71a-212">hello `acquireTokenSilentAsync` method asks ADAL tooreturn a token for hello specified resource without showing any UX.</span></span> <span data-ttu-id="2b71a-213">Który może się zdarzyć, jeśli hello pamięci podręcznej ma już token dostępu odpowiedniego przechowywane, lub Jeśli token odświeżania mogą być używane tooget nowy token dostępu bez wyświetlania dowolnego wiersza.</span><span class="sxs-lookup"><span data-stu-id="2b71a-213">That can happen if hello cache already has a suitable access token stored, or if a refresh token can be used tooget a new access token without showing any prompt.</span></span> <span data-ttu-id="2b71a-214">Jeśli kończy się niepowodzeniem, które firma Microsoft może wrócić `acquireTokenAsync`— które monituje widoczny hello tooauthenticate użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2b71a-214">If that attempt fails, we fall back on `acquireTokenAsync`--which will visibly prompt hello user tooauthenticate.</span></span>

```javascript
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
```
<span data-ttu-id="2b71a-215">Teraz, gdy mamy hello token możemy koniec wywołania interfejsu API programu Graph hello i wykonywać zapytania wyszukiwania hello, która ma.</span><span class="sxs-lookup"><span data-stu-id="2b71a-215">Now that we have hello token, we can finally invoke hello Graph API and perform hello search query that we want.</span></span> <span data-ttu-id="2b71a-216">Wstaw powitania po fragment poniżej hello `authenticate` definicji:</span><span class="sxs-lookup"><span data-stu-id="2b71a-216">Insert hello following snippet below hello `authenticate` definition:</span></span>

```javascript
// Makes an API call tooreceive hello user list
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
<span data-ttu-id="2b71a-217">pliki punktu początkowego Hello dostarczona proste UX wprowadzania alias użytkownika w polu tekstowym.</span><span class="sxs-lookup"><span data-stu-id="2b71a-217">hello starting-point files supplied a simple UX for entering a user's alias in a text box.</span></span> <span data-ttu-id="2b71a-218">Ta metoda używa tego tooconstruct wartości zapytania, połączyć ją z tokenu dostępu hello przesyła tooMicrosoft wykres i przeanalizować hello wyników.</span><span class="sxs-lookup"><span data-stu-id="2b71a-218">This method uses that value tooconstruct a query, combine it with hello access token, send it tooMicrosoft Graph, and parse hello results.</span></span> <span data-ttu-id="2b71a-219">Witaj `renderData` metody już istnieje w pliku punktu początkowego hello, zajmuje się wizualizacja wyników hello.</span><span class="sxs-lookup"><span data-stu-id="2b71a-219">hello `renderData` method, already present in hello starting-point file, takes care of visualizing hello results.</span></span>

## <a name="step-5-run-hello-app"></a><span data-ttu-id="2b71a-220">Krok 5: Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="2b71a-220">Step 5: Run hello app</span></span>
<span data-ttu-id="2b71a-221">Aplikacja jest gotowy na koniec toorun.</span><span class="sxs-lookup"><span data-stu-id="2b71a-221">Your app is finally ready toorun.</span></span> <span data-ttu-id="2b71a-222">Jego działania jest prosty: po uruchomieniu aplikacji hello wprowadź hello alias użytkownika hello ma toolook w górę, a następnie kliknij przycisk hello.</span><span class="sxs-lookup"><span data-stu-id="2b71a-222">Operating it is simple: when hello app starts, enter hello alias of hello user you want toolook up, and then click hello button.</span></span> <span data-ttu-id="2b71a-223">Zostanie wyświetlony monit o uwierzytelnienie.</span><span class="sxs-lookup"><span data-stu-id="2b71a-223">You're prompted for authentication.</span></span> <span data-ttu-id="2b71a-224">Po pomyślnym uwierzytelnieniu i pomyślne wyszukiwania hello atrybuty użytkownika hello przeszukiwane są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="2b71a-224">Upon successful authentication and successful search, hello attributes of hello searched user are displayed.</span></span>

<span data-ttu-id="2b71a-225">Kolejnych uruchomieniach wykona wyszukiwania hello bez wyświetlania dowolnego wiersza, dzięki toohello obecności hello wcześniej uzyskać token w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="2b71a-225">Subsequent runs will perform hello search without showing any prompt, thanks toohello presence of hello previously acquired token in cache.</span></span>

<span data-ttu-id="2b71a-226">konkretne kroki Hello do uruchamiania aplikacji hello zależy od platformy.</span><span class="sxs-lookup"><span data-stu-id="2b71a-226">hello concrete steps for running hello app vary by platform.</span></span>

### <a name="windows-10"></a><span data-ttu-id="2b71a-227">Windows 10</span><span class="sxs-lookup"><span data-stu-id="2b71a-227">Windows 10</span></span>
   <span data-ttu-id="2b71a-228">Komputer typu Tablet:`cordova run windows --archs=x64 -- --appx=uap`</span><span class="sxs-lookup"><span data-stu-id="2b71a-228">Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`</span></span>

   <span data-ttu-id="2b71a-229">Urządzenie przenośne (wymaga systemu Windows 10 Mobile urządzenie podłączone tooa PC):`cordova run windows --archs=arm -- --appx=uap --phone`</span><span class="sxs-lookup"><span data-stu-id="2b71a-229">Mobile (requires a Windows 10 Mobile device connected tooa PC): `cordova run windows --archs=arm -- --appx=uap --phone`</span></span>

   > [!NOTE]
   > <span data-ttu-id="2b71a-230">Podczas pierwszego uruchomienia hello może zostać poproszony toosign w licencji dewelopera.</span><span class="sxs-lookup"><span data-stu-id="2b71a-230">During hello first run, you might be asked toosign in for a developer license.</span></span> <span data-ttu-id="2b71a-231">Aby uzyskać więcej informacji, zobacz [licencji dewelopera](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b71a-231">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-81-tabletpc"></a><span data-ttu-id="2b71a-232">Komputer typu Tablet Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="2b71a-232">Windows 8.1 Tablet/PC</span></span>
   `cordova run windows`

   > [!NOTE]
   > <span data-ttu-id="2b71a-233">Podczas pierwszego uruchomienia hello może zostać poproszony toosign w licencji dewelopera.</span><span class="sxs-lookup"><span data-stu-id="2b71a-233">During hello first run, you might be asked toosign in for a developer license.</span></span> <span data-ttu-id="2b71a-234">Aby uzyskać więcej informacji, zobacz [licencji dewelopera](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b71a-234">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-phone-81"></a><span data-ttu-id="2b71a-235">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="2b71a-235">Windows Phone 8.1</span></span>
   <span data-ttu-id="2b71a-236">toorun na połączonym urządzeniu:`cordova run windows --device -- --phone`</span><span class="sxs-lookup"><span data-stu-id="2b71a-236">toorun on a connected device: `cordova run windows --device -- --phone`</span></span>

   <span data-ttu-id="2b71a-237">toorun na powitania emulatorem domyślnym:`cordova emulate windows -- --phone`</span><span class="sxs-lookup"><span data-stu-id="2b71a-237">toorun on hello default emulator: `cordova emulate windows -- --phone`</span></span>

   <span data-ttu-id="2b71a-238">Użyj `cordova run windows --list -- --phone` toosee wszystkich dostępnych elementów docelowych i `cordova run windows --target=<target_name> -- --phone` aplikacji hello toorun określonego urządzenia lub emulatora (na przykład `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span><span class="sxs-lookup"><span data-stu-id="2b71a-238">Use `cordova run windows --list -- --phone` toosee all available targets and `cordova run windows --target=<target_name> -- --phone` toorun hello application on a specific device or emulator (for example, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span></span>

### <a name="android"></a><span data-ttu-id="2b71a-239">Android</span><span class="sxs-lookup"><span data-stu-id="2b71a-239">Android</span></span>
   <span data-ttu-id="2b71a-240">toorun na połączonym urządzeniu:`cordova run android --device`</span><span class="sxs-lookup"><span data-stu-id="2b71a-240">toorun on a connected device: `cordova run android --device`</span></span>

   <span data-ttu-id="2b71a-241">toorun na powitania emulatorem domyślnym:`cordova emulate android`</span><span class="sxs-lookup"><span data-stu-id="2b71a-241">toorun on hello default emulator: `cordova emulate android`</span></span>

   <span data-ttu-id="2b71a-242">Upewnij się, że po utworzeniu wystąpienia emulatora za pomocą Menedżera AVD, jak opisano wcześniej w sekcji "Wymagania wstępne" hello.</span><span class="sxs-lookup"><span data-stu-id="2b71a-242">Make sure you've created an emulator instance by using AVD Manager, as described earlier in hello "Prerequisites" section.</span></span>

   <span data-ttu-id="2b71a-243">Użyj `cordova run android --list` toosee wszystkich dostępnych elementów docelowych i `cordova run android --target=<target_name>` aplikacji hello toorun określonego urządzenia lub emulatora (na przykład `cordova run android --target="Nexus4_emulator"`).</span><span class="sxs-lookup"><span data-stu-id="2b71a-243">Use `cordova run android --list` toosee all available targets and `cordova run android --target=<target_name>` toorun hello application on a specific device or emulator (for example, `cordova run android --target="Nexus4_emulator"`).</span></span>

### <a name="ios"></a><span data-ttu-id="2b71a-244">iOS</span><span class="sxs-lookup"><span data-stu-id="2b71a-244">iOS</span></span>
   <span data-ttu-id="2b71a-245">toorun na połączonym urządzeniu:`cordova run ios --device`</span><span class="sxs-lookup"><span data-stu-id="2b71a-245">toorun on a connected device: `cordova run ios --device`</span></span>

   <span data-ttu-id="2b71a-246">toorun na powitania emulatorem domyślnym:`cordova emulate ios`</span><span class="sxs-lookup"><span data-stu-id="2b71a-246">toorun on hello default emulator: `cordova emulate ios`</span></span>

   > [!NOTE]
   > <span data-ttu-id="2b71a-247">Upewnij się, że masz hello `ios-sim` toorun zainstalowanym pakietem hello emulatora.</span><span class="sxs-lookup"><span data-stu-id="2b71a-247">Make sure you have hello `ios-sim` package installed toorun on hello emulator.</span></span> <span data-ttu-id="2b71a-248">Aby uzyskać więcej informacji, zobacz hello "wymagania wstępne" sekcji.</span><span class="sxs-lookup"><span data-stu-id="2b71a-248">For more information, see hello "Prerequisites" section.</span></span>

    Use `cordova run ios --list` toosee all available targets and `cordova run ios --target=<target_name>` toorun hello application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` toosee additional build and run options.

## <a name="next-steps"></a><span data-ttu-id="2b71a-249">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2b71a-249">Next steps</span></span>
<span data-ttu-id="2b71a-250">Odwołania, jest dostępna w ukończyć powitalnych próbka (bez wartości konfiguracji) [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span><span class="sxs-lookup"><span data-stu-id="2b71a-250">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span></span>

<span data-ttu-id="2b71a-251">Możesz teraz scenariusze przeniesienia na toomore Zaawansowane (i inne ciekawe).</span><span class="sxs-lookup"><span data-stu-id="2b71a-251">You can now move on toomore advanced (and more interesting) scenarios.</span></span> <span data-ttu-id="2b71a-252">Może być tootry: [zabezpieczyć interfejs API sieci Web Node.js w usłudze Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="2b71a-252">You might want tootry: [Secure a Node.js Web API with Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
