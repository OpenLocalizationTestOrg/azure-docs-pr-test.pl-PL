---
title: aaaAzure AD Android wprowadzenie | Dokumentacja firmy Microsoft
description: "Jak toobuild aplikacji systemu Android, która integruje się z usługą Azure AD, logowania i wywołania usługi Azure AD chronione interfejsów API przy użyciu uwierzytelniania OAuth."
services: active-directory
documentationcenter: android
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1aedc8ff60874b405a182a4ccbfb2c8b4d9d3704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a><span data-ttu-id="10f46-103">Integrowanie usługi Azure AD do aplikacji systemu Android</span><span class="sxs-lookup"><span data-stu-id="10f46-103">Integrate Azure AD into an Android app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="10f46-104">Spróbuj hello Podgląd nowe [portalu dla deweloperów](https://identity.microsoft.com/Docs/Android), który pomoże Ci rozpocząć pracę z usługą Azure AD w ciągu kilku minut.</span><span class="sxs-lookup"><span data-stu-id="10f46-104">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/Android), which will help you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="10f46-105">portalu dla deweloperów Hello przeprowadzi Cię przez proces hello rejestrowanie aplikacji i Integrowanie usługi Azure AD w kodzie.</span><span class="sxs-lookup"><span data-stu-id="10f46-105">hello developer portal will walk you through hello process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="10f46-106">Po zakończeniu będziesz mieć prostą aplikację, która może uwierzytelniać użytkowników w dzierżawie oraz zaplecze, które mogą zaakceptować tokeny i sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="10f46-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a back end that can accept tokens and perform validation.</span></span>
>
>

<span data-ttu-id="10f46-107">Jeśli projektujesz aplikacja usługi Azure Active Directory (Azure AD) umożliwia proste i bezpośrednie dla tooauthenticate można użytkowników przy użyciu ich lokalnych kont usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="10f46-107">If you're developing a desktop application, Azure Active Directory (Azure AD) makes it simple and straightforward for you tooauthenticate your users by using their on-premises Active Directory accounts.</span></span> <span data-ttu-id="10f46-108">Umożliwia również toosecurely Twojej aplikacji korzystać z dowolnej sieci web interfejsu API chronione przez usługę Azure AD, takich jak hello interfejsami API usługi Office 365 lub hello interfejsu API Azure.</span><span class="sxs-lookup"><span data-stu-id="10f46-108">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="10f46-109">W przypadku systemu Android klientów, którzy potrzebują tooaccess chronionych zasobów usługi Azure AD zapewnia hello Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="10f46-109">For Android clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="10f46-110">jedynym celem ADAL Hello jest toomake go łatwo tooget tokenów dostępu do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="10f46-110">hello sole purpose of ADAL is toomake it easy for your app tooget access tokens.</span></span> <span data-ttu-id="10f46-111">jak łatwo jest, firma Microsoft będzie tworzenie aplikacji systemu Android listy zadań do wykonania który toodemonstrate:</span><span class="sxs-lookup"><span data-stu-id="10f46-111">toodemonstrate how easy it is, we’ll build an Android To-Do List application that:</span></span>

* <span data-ttu-id="10f46-112">Pobiera dostępu tokeny na potrzeby wywoływania API listy zadań do wykonania przy użyciu hello [protokół uwierzytelniania OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="10f46-112">Gets access tokens for calling a To-Do List API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="10f46-113">Pobiera listę zadań do wykonania przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="10f46-113">Gets a user's to-do list.</span></span>
* <span data-ttu-id="10f46-114">Wylogowuje użytkowników.</span><span class="sxs-lookup"><span data-stu-id="10f46-114">Signs out users.</span></span>

<span data-ttu-id="10f46-115">tooget uruchomiona, należy dzierżawa usługi Azure AD można tworzyć użytkowników i zarejestrowanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="10f46-115">tooget started, you need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="10f46-116">Jeśli nie masz już dzierżawę, [Dowiedz się, jak tooget jedną](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="10f46-116">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-download-and-run-hello-nodejs-rest-api-todo-sample-server"></a><span data-ttu-id="10f46-117">Krok 1: Pobierz i uruchom hello TODO interfejsu API REST Node.js przykładowym serwerem</span><span class="sxs-lookup"><span data-stu-id="10f46-117">Step 1: Download and run hello Node.js REST API TODO sample server</span></span>
<span data-ttu-id="10f46-118">Przykładowe TODO interfejsu API REST Node.js Hello są zapisywane w szczególności toowork względem naszego istniejący przykład tworzenia pojedynczej dzierżawy interfejsu API REST zadań do wykonania dla usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="10f46-118">hello Node.js REST API TODO sample is written specifically toowork against our existing sample for building a single-tenant To-Do REST API for Azure AD.</span></span> <span data-ttu-id="10f46-119">Jest to wymagane w przypadku hello Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="10f46-119">This is a prerequisite for hello Quick Start.</span></span>

<span data-ttu-id="10f46-120">Aby uzyskać informacje dotyczące tooset to, zobacz temat nasze przykłady istniejących w [Microsoft usługi Azure Active Directory próbki REST API for Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="10f46-120">For information on how tooset this up, see our existing samples in [Microsoft Azure Active Directory Sample REST API Service for Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span></span>


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a><span data-ttu-id="10f46-121">Krok 2: Zarejestruj interfejsu API sieci web z dzierżawy usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="10f46-121">Step 2: Register your web API with your Azure AD tenant</span></span>
<span data-ttu-id="10f46-122">Usługa Active Directory obsługuje dodawanie dwa typy aplikacji:</span><span class="sxs-lookup"><span data-stu-id="10f46-122">Active Directory supports adding two types of applications:</span></span>

- <span data-ttu-id="10f46-123">Interfejsy API, które oferują toousers usług sieci Web</span><span class="sxs-lookup"><span data-stu-id="10f46-123">Web APIs that offer services toousers</span></span>
- <span data-ttu-id="10f46-124">Aplikacji (z systemem w sieci web hello lub na urządzeniu), które uzyskują dostęp do tych interfejsów API sieci web</span><span class="sxs-lookup"><span data-stu-id="10f46-124">Applications (running either on hello web or on a device) that access those web APIs</span></span>

<span data-ttu-id="10f46-125">W tym kroku jest zarejestrowanie hello interfejsu API sieci web, której używasz lokalnie do testowania w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="10f46-125">In this step, you're registering hello web API that you're running locally for testing this sample.</span></span> <span data-ttu-id="10f46-126">Zazwyczaj interfejs API sieci web to usługa REST, która jest funkcja oferty, które mają tooaccess aplikacji.</span><span class="sxs-lookup"><span data-stu-id="10f46-126">Normally, this web API is a REST service that's offering functionality that you want an app tooaccess.</span></span> <span data-ttu-id="10f46-127">Usługi Azure AD może pomóc chronić dowolnego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="10f46-127">Azure AD can help protect any endpoint.</span></span>

<span data-ttu-id="10f46-128">Zakłada się, że w przypadku rejestrowania hello interfejsu API REST TODO odwołuje się do wcześniej.</span><span class="sxs-lookup"><span data-stu-id="10f46-128">We're assuming that you're registering hello TODO REST API referenced earlier.</span></span> <span data-ttu-id="10f46-129">Ale działa to w przypadku dowolnego interfejsu API sieci web interesujące toohelp ochrony usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="10f46-129">But this works for any web API that you want Azure Active Directory toohelp protect.</span></span>

1. <span data-ttu-id="10f46-130">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="10f46-130">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="10f46-131">Na górnym pasku powitania kliknij swoje konto.</span><span class="sxs-lookup"><span data-stu-id="10f46-131">On hello top bar, click your account.</span></span> <span data-ttu-id="10f46-132">W hello **katalogu** wybierz dzierżawy usługi Azure AD hello miejscu tooregister aplikacji.</span><span class="sxs-lookup"><span data-stu-id="10f46-132">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="10f46-133">Kliknij przycisk **więcej usług** w lewym okienku hello, a następnie wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="10f46-133">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="10f46-134">Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="10f46-134">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="10f46-135">Wprowadź przyjazną nazwę dla aplikacji hello (na przykład **TodoListService**), wybierz pozycję **aplikacji sieci Web i/lub interfejs API sieci Web**i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="10f46-135">Enter a friendly name for hello application (for example, **TodoListService**), select **Web Application and/or Web API**, and click **Next**.</span></span>
6. <span data-ttu-id="10f46-136">Dla przykładu hello hello logowania jednokrotnego adresu URL, wprowadź hello podstawowego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="10f46-136">For hello sign-on URL, enter hello base URL for hello sample.</span></span> <span data-ttu-id="10f46-137">Domyślnie jest to `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="10f46-137">By default, this is `https://localhost:8080`.</span></span>
7. <span data-ttu-id="10f46-138">Kliknij przycisk **OK** toocomplete hello rejestracji.</span><span class="sxs-lookup"><span data-stu-id="10f46-138">Click **OK** toocomplete hello registration.</span></span>
8. <span data-ttu-id="10f46-139">Nadal w hello portalu Azure, przejdź do strony aplikacji tooyour, Znajdź wartość Identyfikatora aplikacji hello i skopiuj go.</span><span class="sxs-lookup"><span data-stu-id="10f46-139">While still in hello Azure portal, go tooyour application page, find hello application ID value, and copy it.</span></span> <span data-ttu-id="10f46-140">Należy to później podczas konfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="10f46-140">You'll need this later when configuring your application.</span></span>
9. <span data-ttu-id="10f46-141">Z hello **ustawienia** -> **właściwości** strony, aktualizacja aplikacji hello identyfikator URI — wprowadź `https://<your_tenant_name>/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="10f46-141">From hello **Settings** -> **Properties** page, update hello app ID URI - enter `https://<your_tenant_name>/TodoListService`.</span></span> <span data-ttu-id="10f46-142">Zastąp `<your_tenant_name>` o nazwie hello dzierżawy usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="10f46-142">Replace `<your_tenant_name>` with hello name of your Azure AD tenant.</span></span>

## <a name="step-3-register-hello-sample-android-native-client-application"></a><span data-ttu-id="10f46-143">Krok 3: Zarejestruj hello przykładowej aplikacji systemu Android Native Client</span><span class="sxs-lookup"><span data-stu-id="10f46-143">Step 3: Register hello sample Android Native Client application</span></span>
<span data-ttu-id="10f46-144">W tym przykładzie należy zarejestrować aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="10f46-144">You must register your web application in this sample.</span></span> <span data-ttu-id="10f46-145">Dzięki temu toocommunicate Twojej aplikacji z hello zarejestrowana tylko interfejs API sieci web.</span><span class="sxs-lookup"><span data-stu-id="10f46-145">This allows your application toocommunicate with hello just-registered web API.</span></span> <span data-ttu-id="10f46-146">Usługi Azure AD będą odrzucać tooeven Zezwalaj tooask Twojej aplikacji do logowania, o ile jest on zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="10f46-146">Azure AD will refuse tooeven allow your application tooask for sign-in unless it's registered.</span></span> <span data-ttu-id="10f46-147">Który jest częścią zabezpieczeń hello hello modelu.</span><span class="sxs-lookup"><span data-stu-id="10f46-147">That's part of hello security of hello model.</span></span>

<span data-ttu-id="10f46-148">Zakłada się, że w przypadku rejestrowania hello Przykładowa aplikacja odwołuje się do wcześniej.</span><span class="sxs-lookup"><span data-stu-id="10f46-148">We're assuming that you're registering hello sample application referenced earlier.</span></span> <span data-ttu-id="10f46-149">Jednak ta procedura działa w przypadku dowolnej aplikacji, która projektujesz.</span><span class="sxs-lookup"><span data-stu-id="10f46-149">But this procedure works for any app that you're developing.</span></span>

> [!NOTE]
> <span data-ttu-id="10f46-150">Może zastanawiasz się, dlaczego chcesz umieścić zarówno aplikacji, jak i interfejs API sieci web w jednej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="10f46-150">You might wonder why you're putting both an application and a web API in one tenant.</span></span> <span data-ttu-id="10f46-151">Ponieważ użytkownik może mieć odgadnąć, można utworzyć aplikację, która uzyskuje dostęp do zewnętrznego interfejsu API, który jest zarejestrowany w usłudze Azure AD z innego dzierżawcę.</span><span class="sxs-lookup"><span data-stu-id="10f46-151">As you might have guessed, you can build an app that accesses an external API that is registered in Azure AD from another tenant.</span></span> <span data-ttu-id="10f46-152">Jeśli możesz to zrobić, klienci będą tooconsent toohello stosowania hello interfejsu API w aplikacji hello monit.</span><span class="sxs-lookup"><span data-stu-id="10f46-152">If you do that, your customers will be prompted tooconsent toohello use of hello API in hello application.</span></span> <span data-ttu-id="10f46-153">Biblioteki uwierzytelniania usługi Active Directory dla systemu iOS zapewnia obsługę tej zgody.</span><span class="sxs-lookup"><span data-stu-id="10f46-153">Active Directory Authentication Library for iOS takes care of this consent for you.</span></span> <span data-ttu-id="10f46-154">Jak możemy zapoznać się z bardziej zaawansowane funkcje, zobaczysz, że jest ważnym elementem hello pracy wymagane tooaccess hello zestawu Microsoft APIs z platformy Azure i pakietu Office, a także innych dostawcy usług.</span><span class="sxs-lookup"><span data-stu-id="10f46-154">As we explore more advanced features, you'll see that this is an important part of hello work needed tooaccess hello suite of Microsoft APIs from Azure and Office, as well as any other service provider.</span></span> <span data-ttu-id="10f46-155">Teraz, ponieważ w zarejestrowany zarówno interfejs API sieci web i aplikacji w obszarze hello sam dzierżawy, nie będą widzieć żadnych monitów o zgodę.</span><span class="sxs-lookup"><span data-stu-id="10f46-155">For now, because you registered both your web API and your application under hello same tenant, you won't see any prompts for consent.</span></span> <span data-ttu-id="10f46-156">Dotyczy to zazwyczaj hello specjalnie dla własnego toouse firmy w przypadku tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="10f46-156">This is usually hello case if you're developing an application just for your own company toouse.</span></span>

1. <span data-ttu-id="10f46-157">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="10f46-157">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="10f46-158">Na górnym pasku powitania kliknij swoje konto.</span><span class="sxs-lookup"><span data-stu-id="10f46-158">On hello top bar, click your account.</span></span> <span data-ttu-id="10f46-159">W hello **katalogu** wybierz dzierżawy usługi Azure AD hello miejscu tooregister aplikacji.</span><span class="sxs-lookup"><span data-stu-id="10f46-159">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="10f46-160">Kliknij przycisk **więcej usług** w lewym okienku hello, a następnie wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="10f46-160">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="10f46-161">Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="10f46-161">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="10f46-162">Wprowadź przyjazną nazwę dla aplikacji hello (na przykład **TodoListClient Android**), wybierz pozycję **natywną aplikację kliencką**i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="10f46-162">Enter a friendly name for hello application (for example, **TodoListClient-Android**), select **Native Client Application**, and click **Next**.</span></span>
6. <span data-ttu-id="10f46-163">Identyfikator URI przekierowania dla hello, wprowadź `http://TodoListClient`.</span><span class="sxs-lookup"><span data-stu-id="10f46-163">For hello redirect URI, enter `http://TodoListClient`.</span></span> <span data-ttu-id="10f46-164">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="10f46-164">Click **Finish**.</span></span>
7. <span data-ttu-id="10f46-165">Ze strony aplikacji hello Znajdź wartość Identyfikatora aplikacji hello i skopiuj go.</span><span class="sxs-lookup"><span data-stu-id="10f46-165">From hello application page, find hello application ID value and copy it.</span></span> <span data-ttu-id="10f46-166">Należy to później podczas konfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="10f46-166">You'll need this later when configuring your application.</span></span>
8. <span data-ttu-id="10f46-167">Z hello **ustawienia** wybierz pozycję **wymagane uprawnienia** i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="10f46-167">From hello **Settings** page, select **Required Permissions** and select **Add**.</span></span>  <span data-ttu-id="10f46-168">Zlokalizuj i wybierz TodoListService, dodać hello **TodoListService dostępu** uprawnienie w obszarze **delegowane uprawnienia**i kliknij przycisk **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="10f46-168">Locate and select TodoListService, add hello **Access TodoListService** permission under **Delegated Permissions**, and click **Done**.</span></span>

<span data-ttu-id="10f46-169">toobuild z Maven, można użyć pom.xml na najwyższym poziomie hello:</span><span class="sxs-lookup"><span data-stu-id="10f46-169">toobuild with Maven, you can use pom.xml at hello top level:</span></span>

1. <span data-ttu-id="10f46-170">Klonuj to repozytorium w wybranym katalogu:</span><span class="sxs-lookup"><span data-stu-id="10f46-170">Clone this repo into a directory of your choice:</span></span>

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. <span data-ttu-id="10f46-171">Wykonaj kroki hello hello [wymagania wstępne tooset Twojego środowiska Maven dla systemu Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span><span class="sxs-lookup"><span data-stu-id="10f46-171">Follow hello steps in hello [prerequisites tooset up your Maven environment for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span></span>
3. <span data-ttu-id="10f46-172">Konfigurowanie emulatora hello z 19 zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="10f46-172">Set up hello emulator with SDK 19.</span></span>
4. <span data-ttu-id="10f46-173">Przejdź toohello folderu głównego, gdzie sklonować repozytorium hello.</span><span class="sxs-lookup"><span data-stu-id="10f46-173">Go toohello root folder where you cloned hello repo.</span></span>
5. <span data-ttu-id="10f46-174">Uruchom następujące polecenie:`mvn clean install`</span><span class="sxs-lookup"><span data-stu-id="10f46-174">Run this command: `mvn clean install`</span></span>
6. <span data-ttu-id="10f46-175">Zmień hello katalogu toohello Szybki Start próbki:`cd samples\hello`</span><span class="sxs-lookup"><span data-stu-id="10f46-175">Change hello directory toohello Quick Start sample: `cd samples\hello`</span></span>
7. <span data-ttu-id="10f46-176">Uruchom następujące polecenie:`mvn android:deploy android:run`</span><span class="sxs-lookup"><span data-stu-id="10f46-176">Run this command: `mvn android:deploy android:run`</span></span>

   <span data-ttu-id="10f46-177">Powinny pojawić się uruchamianie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="10f46-177">You should see hello app starting.</span></span>
8. <span data-ttu-id="10f46-178">Wprowadź tootry poświadczenia użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="10f46-178">Enter test user credentials tootry.</span></span>

<span data-ttu-id="10f46-179">Pakiety JAR zostaną przesłane obok hello AAR pakietu.</span><span class="sxs-lookup"><span data-stu-id="10f46-179">JAR packages will be submitted beside hello AAR package.</span></span>

## <a name="step-4-download-hello-android-adal-and-add-it-tooyour-eclipse-workspace"></a><span data-ttu-id="10f46-180">Krok 4: Pobierz hello ADAL dla systemu Android i dodać go tooyour Eclipse roboczym</span><span class="sxs-lookup"><span data-stu-id="10f46-180">Step 4: Download hello Android ADAL and add it tooyour Eclipse workspace</span></span>
<span data-ttu-id="10f46-181">Wprowadziliśmy go łatwo możesz toohave wiele opcji toouse ADAL w projekcie systemu Android:</span><span class="sxs-lookup"><span data-stu-id="10f46-181">We've made it easy for you toohave multiple options toouse ADAL in your Android project:</span></span>

* <span data-ttu-id="10f46-182">Tooimport kod źródłowy hello można użyć tej biblioteki do aplikacji tooyour Eclipse i łącza.</span><span class="sxs-lookup"><span data-stu-id="10f46-182">You can use hello source code tooimport this library into Eclipse and link tooyour application.</span></span>
* <span data-ttu-id="10f46-183">Jeśli używasz programu Android Studio, używając hello AAR pakietu format i odwołanie hello plików binarnych.</span><span class="sxs-lookup"><span data-stu-id="10f46-183">If you're using Android Studio, you can use hello AAR package format and reference hello binaries.</span></span>

### <a name="option-1-source-zip"></a><span data-ttu-id="10f46-184">Opcja 1: Źródło Zip</span><span class="sxs-lookup"><span data-stu-id="10f46-184">Option 1: Source Zip</span></span>
<span data-ttu-id="10f46-185">toodownload kopię hello źródła kodu, kliknij przycisk **Pobierz ZIP** po prawej stronie powitania hello strony.</span><span class="sxs-lookup"><span data-stu-id="10f46-185">toodownload a copy of hello source code, click **Download ZIP** on hello right side of hello page.</span></span> <span data-ttu-id="10f46-186">Można także [pobrać z witryny GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span><span class="sxs-lookup"><span data-stu-id="10f46-186">Or you can [download from GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span></span>

### <a name="option-2-source-via-git"></a><span data-ttu-id="10f46-187">Opcja 2: Źródło za pomocą narzędzia Git</span><span class="sxs-lookup"><span data-stu-id="10f46-187">Option 2: Source via Git</span></span>
<span data-ttu-id="10f46-188">Kod źródłowy hello tooget hello zestawu SDK przez Git, wpisz:</span><span class="sxs-lookup"><span data-stu-id="10f46-188">tooget hello source code of hello SDK via Git, type:</span></span>

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a><span data-ttu-id="10f46-189">Opcja 3: Pliki binarne, za pomocą narzędzia Gradle</span><span class="sxs-lookup"><span data-stu-id="10f46-189">Option 3: Binaries via Gradle</span></span>
<span data-ttu-id="10f46-190">Pliki binarne hello możesz pobrać ze strony hello Maven centralnym repozytorium.</span><span class="sxs-lookup"><span data-stu-id="10f46-190">You can get hello binaries from hello Maven central repo.</span></span> <span data-ttu-id="10f46-191">Pakiet AAR Hello mogą zostać włączone w następujący sposób w projekcie w programie Android Studio:</span><span class="sxs-lookup"><span data-stu-id="10f46-191">hello AAR package can be included as follows in your project in Android Studio:</span></span>

```gradle
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
}
```

### <a name="option-4-aar-via-maven"></a><span data-ttu-id="10f46-192">Opcja 4: AAR za pomocą narzędzia Maven</span><span class="sxs-lookup"><span data-stu-id="10f46-192">Option 4: AAR via Maven</span></span>
<span data-ttu-id="10f46-193">Jeśli używasz hello M2Eclipse wtyczki, można określić zależności hello w pliku pom.xml:</span><span class="sxs-lookup"><span data-stu-id="10f46-193">If you're using hello M2Eclipse plug-in, you can specify hello dependency in your pom.xml file:</span></span>

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-hello-libs-folder"></a><span data-ttu-id="10f46-194">Opcja 5: JAR pakietu znajduje się w folderze libs hello</span><span class="sxs-lookup"><span data-stu-id="10f46-194">Option 5: JAR package inside hello libs folder</span></span>
<span data-ttu-id="10f46-195">Możesz pobrać plik JAR hello z repozytorium Maven hello i upuść ją na powitania **biblioteki** folder w projekcie.</span><span class="sxs-lookup"><span data-stu-id="10f46-195">You can get hello JAR file from hello Maven repo and drop it into hello **libs** folder in your project.</span></span> <span data-ttu-id="10f46-196">Toocopy hello wymaganych zasobów tooyour projektu również jest potrzebna, ponieważ pakiety JAR hello nie zawierają je.</span><span class="sxs-lookup"><span data-stu-id="10f46-196">You need toocopy hello required resources tooyour project as well, because hello JAR packages don't include them.</span></span>

## <a name="step-5-add-references-tooandroid-adal-tooyour-project"></a><span data-ttu-id="10f46-197">Krok 5: Dodawanie odwołań tooAndroid ADAL tooyour projektu</span><span class="sxs-lookup"><span data-stu-id="10f46-197">Step 5: Add references tooAndroid ADAL tooyour project</span></span>
1. <span data-ttu-id="10f46-198">Dodaj odwołanie do projektu tooyour i określ go jako biblioteka systemu Android.</span><span class="sxs-lookup"><span data-stu-id="10f46-198">Add a reference tooyour project and specify it as an Android library.</span></span> <span data-ttu-id="10f46-199">Jeśli nie jesteś pewien sposób toodo, można uzyskać więcej informacji na temat hello [lokacji Android Studio](http://developer.android.com/tools/projects/projects-eclipse.html).</span><span class="sxs-lookup"><span data-stu-id="10f46-199">If you're uncertain how toodo this, you can get more information on hello [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span></span>
2. <span data-ttu-id="10f46-200">Dodaj hello zależności projektu do debugowania do ustawień projektu.</span><span class="sxs-lookup"><span data-stu-id="10f46-200">Add hello project dependency for debugging into your project settings.</span></span>
3. <span data-ttu-id="10f46-201">Aktualizacja tooinclude pliku AndroidManifest.xml projektu:</span><span class="sxs-lookup"><span data-stu-id="10f46-201">Update your project's AndroidManifest.xml file tooinclude:</span></span>

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <application
            android:allowBackup="true"
            android:debuggable="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/AppTheme" >

            <activity
                android:name="com.microsoft.aad.adal.AuthenticationActivity"
                android:label="@string/title_login_hello_app" >
            </activity>
            ....
        <application/>

4. <span data-ttu-id="10f46-202">Utwórz wystąpienie kontekst AuthenticationContext na Twoje działania głównego.</span><span class="sxs-lookup"><span data-stu-id="10f46-202">Create an instance of AuthenticationContext at your main activity.</span></span> <span data-ttu-id="10f46-203">Hello szczegóły tego wywołania wykraczają poza zakres tego tematu hello, ale można uzyskać dobry początek, analizując hello [próbki Android Native Client](https://github.com/AzureADSamples/NativeClient-Android).</span><span class="sxs-lookup"><span data-stu-id="10f46-203">hello details of this call are beyond hello scope of this topic, but you can get a good start by looking at hello [Android Native Client sample](https://github.com/AzureADSamples/NativeClient-Android).</span></span> <span data-ttu-id="10f46-204">Poniższy przykład hello, SharedPreferences jest hello domyślne w pamięci podręcznej i urząd jest w formie hello `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span><span class="sxs-lookup"><span data-stu-id="10f46-204">In hello following example, SharedPreferences is hello default cache, and Authority is in hello form of `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span></span>

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. <span data-ttu-id="10f46-205">Skopiuj ten kod bloku toohandle hello koniec AuthenticationActivity po hello użytkownik wprowadza poświadczenia i odbiera kod autoryzacji:</span><span class="sxs-lookup"><span data-stu-id="10f46-205">Copy this code block toohandle hello end of AuthenticationActivity after hello user enters credentials and receives an authorization code:</span></span>

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. <span data-ttu-id="10f46-206">tooask dla tokenu, zdefiniuj wywołanie zwrotne:</span><span class="sxs-lookup"><span data-stu-id="10f46-206">tooask for a token, define a callback:</span></span>

        private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {

            @Override
            public void onError(Exception exc) {
                if (exc instanceof AuthenticationException) {
                    textViewStatus.setText("Cancelled");
                    Log.d(TAG, "Cancelled");
                } else {
                    textViewStatus.setText("Authentication error:" + exc.getMessage());
                    Log.d(TAG, "Authentication error:" + exc.getMessage());
                }
            }

            @Override
            public void onSuccess(AuthenticationResult result) {
                mResult = result;

                if (result == null || result.getAccessToken() == null
                        || result.getAccessToken().isEmpty()) {
                    textViewStatus.setText("Token is empty");
                    Log.d(TAG, "Token is empty");
                } else {
                    // request is successful
                    Log.d(TAG, "Status:" + result.getStatus() + " Expired:"
                            + result.getExpiresOn().toString());
                    textViewStatus.setText(PASSED);
                }
            }
        };

7. <span data-ttu-id="10f46-207">Na koniec uzyskać tokenu przy użyciu wywołanie zwrotne:</span><span class="sxs-lookup"><span data-stu-id="10f46-207">Finally, ask for a token by using that callback:</span></span>

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

<span data-ttu-id="10f46-208">Oto objaśnienie parametrów hello:</span><span class="sxs-lookup"><span data-stu-id="10f46-208">Here's an explanation of hello parameters:</span></span>

* <span data-ttu-id="10f46-209">*zasób* jest wymagany i jest zasobem hello próbujesz tooaccess.</span><span class="sxs-lookup"><span data-stu-id="10f46-209">*resource* is required and is hello resource you're trying tooaccess.</span></span>
* <span data-ttu-id="10f46-210">*ClientID* jest wymagany i pochodzi z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="10f46-210">*clientid* is required and comes from Azure AD.</span></span>
* <span data-ttu-id="10f46-211">*RedirectUri* nie jest wymagane toobe podany dla wywołania acquireToken hello.</span><span class="sxs-lookup"><span data-stu-id="10f46-211">*RedirectUri* is not required toobe provided for hello acquireToken call.</span></span> <span data-ttu-id="10f46-212">Można skonfigurować go jako nazwę pakietu.</span><span class="sxs-lookup"><span data-stu-id="10f46-212">You can set it up as your package name.</span></span>
* <span data-ttu-id="10f46-213">*PromptBehavior* pomaga tooask poświadczenia tooskip hello w pamięci podręcznej i plików cookie.</span><span class="sxs-lookup"><span data-stu-id="10f46-213">*PromptBehavior* helps tooask for credentials tooskip hello cache and cookie.</span></span>
* <span data-ttu-id="10f46-214">*Wywołanie zwrotne* jest wywoływana po kod autoryzacji hello są wymieniane dla tokenu.</span><span class="sxs-lookup"><span data-stu-id="10f46-214">*callback* is called after hello authorization code is exchanged for a token.</span></span> <span data-ttu-id="10f46-215">Ma ona obiektu AuthenticationResult, który ma token dostępu, Data wygasła i identyfikator informacji o tokenie.</span><span class="sxs-lookup"><span data-stu-id="10f46-215">It has an object of AuthenticationResult, which has access token, date expired, and ID token information.</span></span>
* <span data-ttu-id="10f46-216">*acquireTokenSilent* jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="10f46-216">*acquireTokenSilent* is optional.</span></span> <span data-ttu-id="10f46-217">Można go wywołać toohandle buforowanie i odświeżanie tokenu.</span><span class="sxs-lookup"><span data-stu-id="10f46-217">You can call it toohandle caching and token refresh.</span></span> <span data-ttu-id="10f46-218">Umożliwia także hello wersję usługi synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="10f46-218">It also provides hello sync version.</span></span> <span data-ttu-id="10f46-219">Akceptuje *userId* jako parametr.</span><span class="sxs-lookup"><span data-stu-id="10f46-219">It accepts *userId* as a parameter.</span></span>

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="10f46-220">Przy użyciu tego przewodnika, powinien mieć, jakie muszą toosuccessfully integracji z usługą Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="10f46-220">By using this walkthrough, you should have what you need toosuccessfully integrate with Azure Active Directory.</span></span> <span data-ttu-id="10f46-221">Więcej przykładów dotyczących tej pracy, odwiedź stronę hello AzureADSamples / repozytorium w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="10f46-221">For more examples of this working, visit hello AzureADSamples/ repository on GitHub.</span></span>

## <a name="important-information"></a><span data-ttu-id="10f46-222">Ważne informacje</span><span class="sxs-lookup"><span data-stu-id="10f46-222">Important information</span></span>
### <a name="customization"></a><span data-ttu-id="10f46-223">Dostosowywanie</span><span class="sxs-lookup"><span data-stu-id="10f46-223">Customization</span></span>
<span data-ttu-id="10f46-224">Zasoby aplikacji można zastąpić zasoby biblioteki projektu.</span><span class="sxs-lookup"><span data-stu-id="10f46-224">Your application resources can overwrite library project resources.</span></span> <span data-ttu-id="10f46-225">Dzieje się tak, gdy aplikacja została skompilowana.</span><span class="sxs-lookup"><span data-stu-id="10f46-225">This happens when your app is being built.</span></span> <span data-ttu-id="10f46-226">Z tego powodu można dostosować uwierzytelniania działania układu hello sposób.</span><span class="sxs-lookup"><span data-stu-id="10f46-226">For this reason, you can customize authentication activity layout hello way you want.</span></span> <span data-ttu-id="10f46-227">Należy się, że identyfikator kontrolki hello hello tookeep tej biblioteki ADAL używa (WebView).</span><span class="sxs-lookup"><span data-stu-id="10f46-227">Be sure tookeep hello ID of hello controls that ADAL uses (WebView).</span></span>

### <a name="broker"></a><span data-ttu-id="10f46-228">Broker</span><span class="sxs-lookup"><span data-stu-id="10f46-228">Broker</span></span>
<span data-ttu-id="10f46-229">aplikacji Portal firmy usługi Intune Microsoft Hello zawiera składnik brokera hello.</span><span class="sxs-lookup"><span data-stu-id="10f46-229">hello Microsoft Intune Company Portal app provides hello broker component.</span></span> <span data-ttu-id="10f46-230">Witaj, konto jest tworzone w elementu AccountManager.</span><span class="sxs-lookup"><span data-stu-id="10f46-230">hello account is created in AccountManager.</span></span> <span data-ttu-id="10f46-231">Typ konta Hello jest "com.microsoft.workaccount."</span><span class="sxs-lookup"><span data-stu-id="10f46-231">hello account type is "com.microsoft.workaccount."</span></span> <span data-ttu-id="10f46-232">Elementu AccountManager umożliwia tylko jedno konto logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="10f46-232">AccountManager allows only a single SSO account.</span></span> <span data-ttu-id="10f46-233">Tworzy plik cookie logowania jednokrotnego dla użytkownika powitania po zakończeniu hello urządzenia wyzwanie dla jednej z aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="10f46-233">It creates an SSO cookie for hello user after completing hello device challenge for one of hello apps.</span></span>

<span data-ttu-id="10f46-234">ADAL używa konta brokera hello, jeśli jedno konto użytkownika jest tworzona w tym uwierzytelniania i użytkownik wybierze nie tooskip go.</span><span class="sxs-lookup"><span data-stu-id="10f46-234">ADAL uses hello broker account if one user account is created at this authenticator and you choose not tooskip it.</span></span> <span data-ttu-id="10f46-235">Można pominąć hello brokera użytkownikowi:</span><span class="sxs-lookup"><span data-stu-id="10f46-235">You can skip hello broker user with:</span></span>

   `AuthenticationSettings.Instance.setSkipBroker(true);`

<span data-ttu-id="10f46-236">Należy tooregister specjalne RedirectUri użycia brokera.</span><span class="sxs-lookup"><span data-stu-id="10f46-236">You need tooregister a special RedirectUri for broker usage.</span></span> <span data-ttu-id="10f46-237">RedirectUri jest w formacie hello `msauth://packagename/Base64UrlencodedSignature`.</span><span class="sxs-lookup"><span data-stu-id="10f46-237">RedirectUri is in hello format of `msauth://packagename/Base64UrlencodedSignature`.</span></span> <span data-ttu-id="10f46-238">Twoje RedirectUri dla aplikacji można uzyskać za pomocą brokerRedirectPrint.ps1 skryptu hello lub mContext.getBrokerRedirectUri wywołania interfejsu API hello.</span><span class="sxs-lookup"><span data-stu-id="10f46-238">You can get your RedirectUri for your app by using hello script brokerRedirectPrint.ps1 or hello API call mContext.getBrokerRedirectUri.</span></span> <span data-ttu-id="10f46-239">Podpis Hello jest powiązane tooyour certyfikaty podpisywania.</span><span class="sxs-lookup"><span data-stu-id="10f46-239">hello signature is related tooyour signing certificates.</span></span>

<span data-ttu-id="10f46-240">bieżący model brokera Hello jest jeden użytkownik.</span><span class="sxs-lookup"><span data-stu-id="10f46-240">hello current broker model is for one user.</span></span> <span data-ttu-id="10f46-241">Element AuthenticationContext zawiera hello interfejsu API metody tooget hello brokera użytkownika.</span><span class="sxs-lookup"><span data-stu-id="10f46-241">AuthenticationContext provides hello API method tooget hello broker user.</span></span>

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

<span data-ttu-id="10f46-242">Manifest aplikacji powinien mieć następujące uprawnienia toouse elementu AccountManager kont hello.</span><span class="sxs-lookup"><span data-stu-id="10f46-242">Your app manifest should have hello following permissions toouse AccountManager accounts.</span></span> <span data-ttu-id="10f46-243">Aby uzyskać więcej informacji, zobacz hello [elementu AccountManager informacji na temat witryny systemu Android hello](http://developer.android.com/reference/android/accounts/AccountManager.html).</span><span class="sxs-lookup"><span data-stu-id="10f46-243">For details, see hello [AccountManager information on hello Android site](http://developer.android.com/reference/android/accounts/AccountManager.html).</span></span>

* <span data-ttu-id="10f46-244">GET_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="10f46-244">GET_ACCOUNTS</span></span>
* <span data-ttu-id="10f46-245">USE_CREDENTIALS</span><span class="sxs-lookup"><span data-stu-id="10f46-245">USE_CREDENTIALS</span></span>
* <span data-ttu-id="10f46-246">MANAGE_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="10f46-246">MANAGE_ACCOUNTS</span></span>

### <a name="authority-url-and-ad-fs"></a><span data-ttu-id="10f46-247">Adres URL urzędu i usługami AD FS</span><span class="sxs-lookup"><span data-stu-id="10f46-247">Authority URL and AD FS</span></span>
<span data-ttu-id="10f46-248">Active Directory Federation Services (AD FS) nie został rozpoznany jako produkcji STS, więc należy tooturn odnajdywania instancji i przekazać wartość false w hello kontekst AuthenticationContext konstruktora.</span><span class="sxs-lookup"><span data-stu-id="10f46-248">Active Directory Federation Services (AD FS) is not recognized as production STS, so you need tooturn of instance discovery and pass false at hello AuthenticationContext constructor.</span></span>

<span data-ttu-id="10f46-249">adres URL urzędu Hello wymaga wystąpienia usługi STS i [nazwa dzierżawcy](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="10f46-249">hello authority URL needs an STS instance and a [tenant name](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span></span>

### <a name="querying-cache-items"></a><span data-ttu-id="10f46-250">Wykonywanie zapytania o elementy pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="10f46-250">Querying cache items</span></span>
<span data-ttu-id="10f46-251">Biblioteka ADAL udostępnia pamięć podręczną domyślne w SharedPreferences z niektórych prostych pamięci podręcznej funkcje zapytań.</span><span class="sxs-lookup"><span data-stu-id="10f46-251">ADAL provides a default cache in SharedPreferences with some simple cache query functions.</span></span> <span data-ttu-id="10f46-252">Możesz uzyskać hello bieżącej pamięci podręcznej z kontekst AuthenticationContext przy użyciu:</span><span class="sxs-lookup"><span data-stu-id="10f46-252">You can get hello current cache from AuthenticationContext by using:</span></span>

    ITokenCacheStore cache = mContext.getCache();

<span data-ttu-id="10f46-253">Można też podać implementacji pamięci podręcznej, jeśli chcesz, aby toocustomize go.</span><span class="sxs-lookup"><span data-stu-id="10f46-253">You can also provide your cache implementation, if you want toocustomize it.</span></span>

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a><span data-ttu-id="10f46-254">Zachowanie monitu</span><span class="sxs-lookup"><span data-stu-id="10f46-254">Prompt behavior</span></span>
<span data-ttu-id="10f46-255">Biblioteka ADAL zapewnia zachowanie monitu toospecify opcji.</span><span class="sxs-lookup"><span data-stu-id="10f46-255">ADAL provides an option toospecify prompt behavior.</span></span> <span data-ttu-id="10f46-256">PromptBehavior.Auto wyświetli hello interfejsu użytkownika, jeśli token odświeżania hello jest nieprawidłowy i wymagane są poświadczenia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="10f46-256">PromptBehavior.Auto will show hello UI if hello refresh token is invalid and user credentials are required.</span></span> <span data-ttu-id="10f46-257">PromptBehavior.Always pominie hello użycia pamięci podręcznej i zawsze pokazuj hello interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="10f46-257">PromptBehavior.Always will skip hello cache usage and always show hello UI.</span></span>

### <a name="silent-token-request-from-cache-and-refresh"></a><span data-ttu-id="10f46-258">Dyskretnej żądania tokenu z pamięci podręcznej i Odśwież</span><span class="sxs-lookup"><span data-stu-id="10f46-258">Silent token request from cache and refresh</span></span>
<span data-ttu-id="10f46-259">Dyskretnej żądania tokenu nie używa hello podręcznym interfejsu użytkownika i nie wymaga działania.</span><span class="sxs-lookup"><span data-stu-id="10f46-259">A silent token request does not use hello UI pop-up and does not require an activity.</span></span> <span data-ttu-id="10f46-260">Zwraca token z hello pamięci podręcznej, jeśli jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="10f46-260">It returns a token from hello cache if available.</span></span> <span data-ttu-id="10f46-261">Jeśli hello token wygasł, ta metoda próbuje toorefresh go.</span><span class="sxs-lookup"><span data-stu-id="10f46-261">If hello token is expired, this method tries toorefresh it.</span></span> <span data-ttu-id="10f46-262">Jeśli token odświeżania hello wygasł lub nie powiodło się, zwraca authenticationexception —.</span><span class="sxs-lookup"><span data-stu-id="10f46-262">If hello refresh token is expired or failed, it returns AuthenticationException.</span></span>

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="10f46-263">Można również przeprowadzać synchronizacji wywołać za pomocą tej metody.</span><span class="sxs-lookup"><span data-stu-id="10f46-263">You can also make a sync call by using this method.</span></span> <span data-ttu-id="10f46-264">Można ustawić wartości null toocallback lub użyć acquireTokenSilentSync.</span><span class="sxs-lookup"><span data-stu-id="10f46-264">You can set null toocallback or use acquireTokenSilentSync.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="10f46-265">Diagnostyka</span><span class="sxs-lookup"><span data-stu-id="10f46-265">Diagnostics</span></span>
<span data-ttu-id="10f46-266">Są to hello podstawowego źródła informacji do diagnozowania problemów:</span><span class="sxs-lookup"><span data-stu-id="10f46-266">These are hello primary sources of information for diagnosing issues:</span></span>

* <span data-ttu-id="10f46-267">Wyjątki</span><span class="sxs-lookup"><span data-stu-id="10f46-267">Exceptions</span></span>
* <span data-ttu-id="10f46-268">Dzienniki</span><span class="sxs-lookup"><span data-stu-id="10f46-268">Logs</span></span>
* <span data-ttu-id="10f46-269">Śledzenie sieci</span><span class="sxs-lookup"><span data-stu-id="10f46-269">Network traces</span></span>

<span data-ttu-id="10f46-270">Należy zauważyć, że identyfikatorów korelacji centralnej toohello diagnostyki w bibliotece hello.</span><span class="sxs-lookup"><span data-stu-id="10f46-270">Note that correlation IDs are central toohello diagnostics in hello library.</span></span> <span data-ttu-id="10f46-271">Jeśli chcesz, aby toocorrelate ADAL żądania z innymi operacjami w kodzie można ustawić z identyfikatorów korelacji na podstawie danego żądania.</span><span class="sxs-lookup"><span data-stu-id="10f46-271">You can set your correlation IDs on a per-request basis if you want toocorrelate an ADAL request with other operations in your code.</span></span> <span data-ttu-id="10f46-272">Jeśli identyfikator korelacji nie jest ustawiona, biblioteka ADAL wygeneruje losowy.</span><span class="sxs-lookup"><span data-stu-id="10f46-272">If you don't set a correlation ID, ADAL will generate a random one.</span></span> <span data-ttu-id="10f46-273">Wszystkie komunikaty dziennika i wywołania sieci zostanie następnie opatrzone identyfikatora hello korelacji.</span><span class="sxs-lookup"><span data-stu-id="10f46-273">All log messages and network calls will then be stamped with hello correlation ID.</span></span> <span data-ttu-id="10f46-274">Witaj automatycznie wygenerowany zmiany Identyfikatora dla każdego żądania.</span><span class="sxs-lookup"><span data-stu-id="10f46-274">hello self-generated ID changes on each request.</span></span>

#### <a name="exceptions"></a><span data-ttu-id="10f46-275">Wyjątki</span><span class="sxs-lookup"><span data-stu-id="10f46-275">Exceptions</span></span>
<span data-ttu-id="10f46-276">Wyjątki są najpierw hello diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="10f46-276">Exceptions are hello first diagnostic.</span></span> <span data-ttu-id="10f46-277">Spróbujemy tooprovide przydatne komunikaty.</span><span class="sxs-lookup"><span data-stu-id="10f46-277">We try tooprovide helpful error messages.</span></span> <span data-ttu-id="10f46-278">Jeśli znajdziesz taki, który nie jest pomocna, zgłoś problem i Daj nam znać.</span><span class="sxs-lookup"><span data-stu-id="10f46-278">If you find one that is not helpful, please file an issue and let us know.</span></span> <span data-ttu-id="10f46-279">Zawierają informacje urządzenia, takie jak modelu oraz liczbę zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="10f46-279">Include device information such as model and SDK number.</span></span>

#### <a name="logs"></a><span data-ttu-id="10f46-280">Dzienniki</span><span class="sxs-lookup"><span data-stu-id="10f46-280">Logs</span></span>
<span data-ttu-id="10f46-281">Można skonfigurować hello biblioteki toogenerate komunikatów dziennika, których można używać toohelp diagnozowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="10f46-281">You can configure hello library toogenerate log messages that you can use toohelp diagnose issues.</span></span> <span data-ttu-id="10f46-282">Możesz skonfigurować rejestrowanie wprowadzając następujące hello wywołać tooconfigure ADAL użyje toohand poza wszystkich komunikatach dziennika, ponieważ jest ona generowana wywołanie zwrotne.</span><span class="sxs-lookup"><span data-stu-id="10f46-282">You configure logging by making hello following call tooconfigure a callback that ADAL will use toohand off each log message as it's generated.</span></span>

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this toolog file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

<span data-ttu-id="10f46-283">Komunikaty mogą być zapisywane tooa niestandardowego pliku dziennika, jak pokazano w hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="10f46-283">Messages can be written tooa custom log file, as shown in hello following code.</span></span> <span data-ttu-id="10f46-284">Niestety nie istnieje standardowy sposób pobierania dzienniki z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="10f46-284">Unfortunately, there is no standard way of getting logs from a device.</span></span> <span data-ttu-id="10f46-285">Brak niektórych usług, które mogą pomóc Ci z tym.</span><span class="sxs-lookup"><span data-stu-id="10f46-285">There are some services that can help you with this.</span></span> <span data-ttu-id="10f46-286">Można również zapasów własnych, takie jak wysyłanie hello tooa serwera plików.</span><span class="sxs-lookup"><span data-stu-id="10f46-286">You can also invent your own, such as sending hello file tooa server.</span></span>

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

<span data-ttu-id="10f46-287">Są to hello poziomów rejestrowania:</span><span class="sxs-lookup"><span data-stu-id="10f46-287">These are hello logging levels:</span></span>
* <span data-ttu-id="10f46-288">Błąd (wyjątków)</span><span class="sxs-lookup"><span data-stu-id="10f46-288">Error (exceptions)</span></span>
* <span data-ttu-id="10f46-289">Warn (ostrzeżenie)</span><span class="sxs-lookup"><span data-stu-id="10f46-289">Warn (warning)</span></span>
* <span data-ttu-id="10f46-290">Informacje o (celów informacyjnych)</span><span class="sxs-lookup"><span data-stu-id="10f46-290">Info (information purposes)</span></span>
* <span data-ttu-id="10f46-291">Pełne (więcej szczegółów)</span><span class="sxs-lookup"><span data-stu-id="10f46-291">Verbose (more details)</span></span>

<span data-ttu-id="10f46-292">Ustaw poziom dziennika hello następująco:</span><span class="sxs-lookup"><span data-stu-id="10f46-292">You set hello log level like this:</span></span>

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 <span data-ttu-id="10f46-293">Wszystkie komunikaty dziennika są wysyłane toologcat, w wywołania zwrotne — Dodawanie tooany dziennik niestandardowy.</span><span class="sxs-lookup"><span data-stu-id="10f46-293">All log messages are sent toologcat, in addition tooany custom log callbacks.</span></span>
<span data-ttu-id="10f46-294">Plik dziennika tooa można uzyskać z logcat w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="10f46-294">You can get a log tooa file from logcat as follows:</span></span>

    adb logcat > "C:\logmsg\logfile.txt"

 <span data-ttu-id="10f46-295">Aby uzyskać więcej informacji o poleceniach adb, zobacz hello [logcat informacji na temat witryny systemu Android hello](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span><span class="sxs-lookup"><span data-stu-id="10f46-295">For details about adb commands, see hello [logcat information on hello Android site](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span></span>

#### <a name="network-traces"></a><span data-ttu-id="10f46-296">Śledzenie sieci</span><span class="sxs-lookup"><span data-stu-id="10f46-296">Network traces</span></span>
<span data-ttu-id="10f46-297">Można użyć różnych narzędzi toocapture hello ruch HTTP generuje biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="10f46-297">You can use various tools toocapture hello HTTP traffic that ADAL generates.</span></span>  <span data-ttu-id="10f46-298">Jest to najbardziej przydatne, jeśli znasz hello protokołu OAuth lub jeśli potrzebujesz tooMicrosoft informacje diagnostyczne tooprovide lub inne kanały pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="10f46-298">This is most useful if you're familiar with hello OAuth protocol or if you need tooprovide diagnostic information tooMicrosoft or other support channels.</span></span>

<span data-ttu-id="10f46-299">Fiddler jest hello najprostszym narzędzie śledzenia HTTP.</span><span class="sxs-lookup"><span data-stu-id="10f46-299">Fiddler is hello easiest HTTP tracing tool.</span></span> <span data-ttu-id="10f46-300">Użyj następujących hello łączy tooset go rekordu toocorrectly ADAL ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="10f46-300">Use hello following links tooset it up toocorrectly record ADAL network traffic.</span></span> <span data-ttu-id="10f46-301">Dla narzędzia śledzenia, takiego jak toobe Fiddler lub Charlesa przydatne należy go skonfigurować toorecord bez szyfrowania ruchu protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="10f46-301">For a tracing tool like Fiddler or Charles toobe useful, you must configure it toorecord unencrypted SSL traffic.</span></span>  

> [!NOTE]
> <span data-ttu-id="10f46-302">Ślady generowane w ten sposób mogą zawierać wysoko uprzywilejowane informacje, takie jak tokenów dostępu, nazwy użytkowników i hasła.</span><span class="sxs-lookup"><span data-stu-id="10f46-302">Traces generated in this way might contain highly privileged information such as access tokens, usernames, and passwords.</span></span> <span data-ttu-id="10f46-303">Jeśli używasz konta produkcji, nie są udostępniane te operacje śledzenia stron trzecich.</span><span class="sxs-lookup"><span data-stu-id="10f46-303">If you're using production accounts, do not share these traces with third parties.</span></span> <span data-ttu-id="10f46-304">Toosupply toosomeone śledzenia, w kolejności tooget obsługi, należy odtworzyć problem hello przy użyciu tymczasowego konta o nazwach użytkowników i hasła, czy nie stanowi udostępniania.</span><span class="sxs-lookup"><span data-stu-id="10f46-304">If you need toosupply a trace toosomeone in order tooget support, reproduce hello issue by using a temporary account with usernames and passwords that you don't mind sharing.</span></span>

* <span data-ttu-id="10f46-305">Z witryny sieci Web hello strony firmy Telerik: [ustawienia zapasowej Fiddler dla systemu Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span><span class="sxs-lookup"><span data-stu-id="10f46-305">From hello Telerik website: [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span></span>
* <span data-ttu-id="10f46-306">Z witryny GitHub: [skonfigurować reguły Fiddler dotyczące biblioteki ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span><span class="sxs-lookup"><span data-stu-id="10f46-306">From GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span></span>

### <a name="dialog-mode"></a><span data-ttu-id="10f46-307">Tryb okna dialogowego</span><span class="sxs-lookup"><span data-stu-id="10f46-307">Dialog mode</span></span>
<span data-ttu-id="10f46-308">Metoda acquireToken Hello bez działania obsługuje wiersza okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="10f46-308">hello acquireToken method without activity supports a dialog prompt.</span></span>

### <a name="encryption"></a><span data-ttu-id="10f46-309">Szyfrowanie</span><span class="sxs-lookup"><span data-stu-id="10f46-309">Encryption</span></span>
<span data-ttu-id="10f46-310">Biblioteka ADAL szyfruje hello tokeny i magazynu w SharedPreferences domyślnie.</span><span class="sxs-lookup"><span data-stu-id="10f46-310">ADAL encrypts hello tokens and store in SharedPreferences by default.</span></span> <span data-ttu-id="10f46-311">Można przyjrzeć się hello StorageHelper klasy toosee hello szczegóły.</span><span class="sxs-lookup"><span data-stu-id="10f46-311">You can look at hello StorageHelper class toosee hello details.</span></span> <span data-ttu-id="10f46-312">Android wprowadzonej Android Keystore 4.3 (interfejs API 18) bezpieczny magazyn kluczy prywatnych.</span><span class="sxs-lookup"><span data-stu-id="10f46-312">Android introduced Android Keystore for 4.3 (API 18) secure storage of private keys.</span></span> <span data-ttu-id="10f46-313">Biblioteka ADAL użyty dla interfejsu API 18 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="10f46-313">ADAL uses that for API 18 and higher.</span></span> <span data-ttu-id="10f46-314">Jeśli chcesz toouse biblioteki ADAL dla niższych wersjach zestawu SDK, należy tooprovide klucza tajnego w AuthenticationSettings.INSTANCE.setSecretKey.</span><span class="sxs-lookup"><span data-stu-id="10f46-314">If you want toouse ADAL for lower SDK versions, you need tooprovide a secret key at AuthenticationSettings.INSTANCE.setSecretKey.</span></span>

### <a name="oauth2-bearer-challenge"></a><span data-ttu-id="10f46-315">Żądania elementu nośnego OAuth2</span><span class="sxs-lookup"><span data-stu-id="10f46-315">OAuth2 bearer challenge</span></span>
<span data-ttu-id="10f46-316">Hello klasy AuthenticationParameters udostępnia funkcje tooget authorization_uri z hello żądania elementu nośnego OAuth2.</span><span class="sxs-lookup"><span data-stu-id="10f46-316">hello AuthenticationParameters class provides functionality tooget authorization_uri from hello OAuth2 bearer challenge.</span></span>

### <a name="session-cookies-in-webview"></a><span data-ttu-id="10f46-317">Pliki cookie z sesji w widoku sieci Web</span><span class="sxs-lookup"><span data-stu-id="10f46-317">Session cookies in WebView</span></span>
<span data-ttu-id="10f46-318">Po zamknięciu aplikacji hello android WebView nie czyści plików cookie sesji.</span><span class="sxs-lookup"><span data-stu-id="10f46-318">Android WebView does not clear session cookies after hello app is closed.</span></span> <span data-ttu-id="10f46-319">Który można obsługiwać przy użyciu ten przykładowy kod:</span><span class="sxs-lookup"><span data-stu-id="10f46-319">You can handle that by using this sample code:</span></span>

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

<span data-ttu-id="10f46-320">Aby uzyskać więcej informacji o plikach cookie, zobacz hello [CookieSyncManager informacji na temat witryny systemu Android hello](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span><span class="sxs-lookup"><span data-stu-id="10f46-320">For details about cookies, see hello [CookieSyncManager information on hello Android site](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span></span>

### <a name="resource-overrides"></a><span data-ttu-id="10f46-321">Zastąpienia zasobów</span><span class="sxs-lookup"><span data-stu-id="10f46-321">Resource overrides</span></span>
<span data-ttu-id="10f46-322">Biblioteka ADAL Hello zawiera ciągi angielskiej wersji językowej ProgressDialog wiadomości.</span><span class="sxs-lookup"><span data-stu-id="10f46-322">hello ADAL library includes English strings for ProgressDialog messages.</span></span> <span data-ttu-id="10f46-323">Aplikacji należy je zastąpić, jeśli chcesz zlokalizowanych ciągów.</span><span class="sxs-lookup"><span data-stu-id="10f46-323">Your application should overwrite them if you want localized strings.</span></span>

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a><span data-ttu-id="10f46-324">Okno dialogowe NTLM</span><span class="sxs-lookup"><span data-stu-id="10f46-324">NTLM dialog box</span></span>
<span data-ttu-id="10f46-325">ADAL w wersji 1.1.0 obsługuje okno dialogowe NTLM, jest przetwarzany przez zdarzenie onReceivedHttpAuthRequest hello z WebViewClient.</span><span class="sxs-lookup"><span data-stu-id="10f46-325">ADAL version 1.1.0 supports an NTLM dialog box that is processed through hello onReceivedHttpAuthRequest event from WebViewClient.</span></span> <span data-ttu-id="10f46-326">Możesz dostosować hello układ i ciągi dla hello — okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="10f46-326">You can customize hello layout and strings for hello dialog box.</span></span>

### <a name="cross-app-sso"></a><span data-ttu-id="10f46-327">Usługa rejestracji Jednokrotnej w wielu aplikacji</span><span class="sxs-lookup"><span data-stu-id="10f46-327">Cross-app SSO</span></span>
<span data-ttu-id="10f46-328">Dowiedz się [jak tooenable logowania jednokrotnego wielu aplikacji w systemie Android przy użyciu biblioteki ADAL](active-directory-sso-android.md).</span><span class="sxs-lookup"><span data-stu-id="10f46-328">Learn [how tooenable cross-app SSO on Android by using ADAL](active-directory-sso-android.md).</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
