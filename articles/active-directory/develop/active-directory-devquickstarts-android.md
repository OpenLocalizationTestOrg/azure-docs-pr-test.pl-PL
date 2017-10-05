---
title: Azure AD systemu Android wprowadzenie | Dokumentacja firmy Microsoft
description: "Sposób tworzenia aplikacji systemu Android, która integruje się z usługą Azure AD, logowania i wywołania usługi Azure AD chronione interfejsów API przy użyciu uwierzytelniania OAuth."
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
ms.openlocfilehash: 746cad19093fd2a1ad23ddd9412394f8d9da331c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a><span data-ttu-id="f08ca-103">Integrowanie usługi Azure AD do aplikacji systemu Android</span><span class="sxs-lookup"><span data-stu-id="f08ca-103">Integrate Azure AD into an Android app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="f08ca-104">Spróbuj Podgląd nowe [portalu dla deweloperów](https://identity.microsoft.com/Docs/Android), który pomoże Ci rozpocząć pracę z usługą Azure AD w ciągu kilku minut.</span><span class="sxs-lookup"><span data-stu-id="f08ca-104">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/Android), which will help you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="f08ca-105">Portalu dla deweloperów przeprowadzi Cię przez proces rejestracji aplikacji i Integrowanie usługi Azure AD w kodzie.</span><span class="sxs-lookup"><span data-stu-id="f08ca-105">The developer portal will walk you through the process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="f08ca-106">Po zakończeniu będziesz mieć prostą aplikację, która może uwierzytelniać użytkowników w dzierżawie oraz zaplecze, które mogą zaakceptować tokeny i sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="f08ca-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a back end that can accept tokens and perform validation.</span></span>
>
>

<span data-ttu-id="f08ca-107">Jeśli projektujesz klasycznej aplikacji usługi Azure Active Directory (Azure AD) umożliwia proste i bezpośrednie umożliwia uwierzytelnianie użytkowników przy użyciu ich lokalnych kont usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f08ca-107">If you're developing a desktop application, Azure Active Directory (Azure AD) makes it simple and straightforward for you to authenticate your users by using their on-premises Active Directory accounts.</span></span> <span data-ttu-id="f08ca-108">Umożliwia również aplikacji bezpiecznego używać dowolnego składnika web API chronione przez usługę Azure AD, takie jak interfejsami API usługi Office 365 lub interfejsu API platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f08ca-108">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="f08ca-109">W przypadku systemu Android klientów, którzy potrzebują dostępu do chronionych zasobów usługi Azure AD zapewnia Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="f08ca-109">For Android clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="f08ca-110">Wyłącznie do celów ADAL jest umożliwia łatwe uzyskanie tokenów dostępu do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f08ca-110">The sole purpose of ADAL is to make it easy for your app to get access tokens.</span></span> <span data-ttu-id="f08ca-111">Aby zademonstrować, jak łatwo, firma Microsoft będzie kompilacji aplikacji systemu Android listy zadań do wykonania który:</span><span class="sxs-lookup"><span data-stu-id="f08ca-111">To demonstrate how easy it is, we’ll build an Android To-Do List application that:</span></span>

* <span data-ttu-id="f08ca-112">Pobiera dostępu tokeny na potrzeby wywoływania API listy zadań do wykonania przy użyciu [protokół uwierzytelniania OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="f08ca-112">Gets access tokens for calling a To-Do List API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="f08ca-113">Pobiera listę zadań do wykonania przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f08ca-113">Gets a user's to-do list.</span></span>
* <span data-ttu-id="f08ca-114">Wylogowuje użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f08ca-114">Signs out users.</span></span>

<span data-ttu-id="f08ca-115">Aby rozpocząć pracę, należy dzierżawa usługi Azure AD można tworzyć użytkowników i zarejestrowanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f08ca-115">To get started, you need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="f08ca-116">Jeśli nie masz już dzierżawę, [Dowiedz się, jak kupić](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="f08ca-116">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-download-and-run-the-nodejs-rest-api-todo-sample-server"></a><span data-ttu-id="f08ca-117">Krok 1: Pobierz i uruchom serwer próbki TODO interfejsu API REST Node.js</span><span class="sxs-lookup"><span data-stu-id="f08ca-117">Step 1: Download and run the Node.js REST API TODO sample server</span></span>
<span data-ttu-id="f08ca-118">Przykładowe TODO interfejsu API REST Node.js są zapisywane w szczególności pracy projektowej naszej próbki istniejących tworzenia pojedynczej dzierżawy interfejsu API REST zadań do wykonania dla usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f08ca-118">The Node.js REST API TODO sample is written specifically to work against our existing sample for building a single-tenant To-Do REST API for Azure AD.</span></span> <span data-ttu-id="f08ca-119">Jest to wymagane w przypadku Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="f08ca-119">This is a prerequisite for the Quick Start.</span></span>

<span data-ttu-id="f08ca-120">Aby uzyskać informacje na temat tej konfiguracji, zobacz nasze przykłady istniejących w [Microsoft usługi Azure Active Directory próbki REST API for Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f08ca-120">For information on how to set this up, see our existing samples in [Microsoft Azure Active Directory Sample REST API Service for Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span></span>


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a><span data-ttu-id="f08ca-121">Krok 2: Zarejestruj interfejsu API sieci web z dzierżawy usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f08ca-121">Step 2: Register your web API with your Azure AD tenant</span></span>
<span data-ttu-id="f08ca-122">Usługa Active Directory obsługuje dodawanie dwa typy aplikacji:</span><span class="sxs-lookup"><span data-stu-id="f08ca-122">Active Directory supports adding two types of applications:</span></span>

- <span data-ttu-id="f08ca-123">Interfejsy API, które oferują usługi dla użytkowników sieci Web</span><span class="sxs-lookup"><span data-stu-id="f08ca-123">Web APIs that offer services to users</span></span>
- <span data-ttu-id="f08ca-124">Aplikacje (z systemem w sieci web lub na urządzeniu), które uzyskują dostęp do tych interfejsów API sieci web</span><span class="sxs-lookup"><span data-stu-id="f08ca-124">Applications (running either on the web or on a device) that access those web APIs</span></span>

<span data-ttu-id="f08ca-125">W tym kroku jest zarejestrowanie sieci web interfejsu API, której używasz lokalnie do testowania w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="f08ca-125">In this step, you're registering the web API that you're running locally for testing this sample.</span></span> <span data-ttu-id="f08ca-126">Zazwyczaj interfejs API sieci web to usługa REST, która oferuje funkcje, które mają dostęp do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f08ca-126">Normally, this web API is a REST service that's offering functionality that you want an app to access.</span></span> <span data-ttu-id="f08ca-127">Usługi Azure AD może pomóc chronić dowolnego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="f08ca-127">Azure AD can help protect any endpoint.</span></span>

<span data-ttu-id="f08ca-128">Zakłada się, że w przypadku rejestrowania interfejsu API REST TODO odwołuje się do wcześniej.</span><span class="sxs-lookup"><span data-stu-id="f08ca-128">We're assuming that you're registering the TODO REST API referenced earlier.</span></span> <span data-ttu-id="f08ca-129">Ale działa to w przypadku dowolnej sieci web interfejsu API, który ma usługi Azure Active Directory w celu ochrony.</span><span class="sxs-lookup"><span data-stu-id="f08ca-129">But this works for any web API that you want Azure Active Directory to help protect.</span></span>

1. <span data-ttu-id="f08ca-130">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f08ca-130">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f08ca-131">Na górnym pasku kliknij konto.</span><span class="sxs-lookup"><span data-stu-id="f08ca-131">On the top bar, click your account.</span></span> <span data-ttu-id="f08ca-132">W **katalogu** wybierz dzierżawy usługi Azure AD, które chcesz zarejestrować aplikację.</span><span class="sxs-lookup"><span data-stu-id="f08ca-132">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="f08ca-133">Kliknij przycisk **więcej usług** w okienku po lewej stronie, a następnie wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f08ca-133">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="f08ca-134">Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="f08ca-134">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="f08ca-135">Wprowadź przyjazną nazwę dla aplikacji (na przykład **TodoListService**), wybierz pozycję **aplikacji sieci Web i/lub interfejs API sieci Web**i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="f08ca-135">Enter a friendly name for the application (for example, **TodoListService**), select **Web Application and/or Web API**, and click **Next**.</span></span>
6. <span data-ttu-id="f08ca-136">Zaloguj się na adres URL wprowadź podstawowy adres URL przykładowej.</span><span class="sxs-lookup"><span data-stu-id="f08ca-136">For the sign-on URL, enter the base URL for the sample.</span></span> <span data-ttu-id="f08ca-137">Domyślnie jest to `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="f08ca-137">By default, this is `https://localhost:8080`.</span></span>
7. <span data-ttu-id="f08ca-138">Kliknij przycisk **OK** do ukończenia rejestracji.</span><span class="sxs-lookup"><span data-stu-id="f08ca-138">Click **OK** to complete the registration.</span></span>
8. <span data-ttu-id="f08ca-139">Nadal w portalu Azure, przejdź do strony aplikacji, Znajdź wartość Identyfikatora aplikacji i skopiuj go.</span><span class="sxs-lookup"><span data-stu-id="f08ca-139">While still in the Azure portal, go to your application page, find the application ID value, and copy it.</span></span> <span data-ttu-id="f08ca-140">Należy to później podczas konfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f08ca-140">You'll need this later when configuring your application.</span></span>
9. <span data-ttu-id="f08ca-141">Z **ustawienia** -> **właściwości** strony, aktualizacja identyfikator URI — wprowadź `https://<your_tenant_name>/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="f08ca-141">From the **Settings** -> **Properties** page, update the app ID URI - enter `https://<your_tenant_name>/TodoListService`.</span></span> <span data-ttu-id="f08ca-142">Zastąp `<your_tenant_name>` o nazwie dzierżawy usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f08ca-142">Replace `<your_tenant_name>` with the name of your Azure AD tenant.</span></span>

## <a name="step-3-register-the-sample-android-native-client-application"></a><span data-ttu-id="f08ca-143">Krok 3: Zarejestruj przykładowej aplikacji systemu Android Native Client</span><span class="sxs-lookup"><span data-stu-id="f08ca-143">Step 3: Register the sample Android Native Client application</span></span>
<span data-ttu-id="f08ca-144">W tym przykładzie należy zarejestrować aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="f08ca-144">You must register your web application in this sample.</span></span> <span data-ttu-id="f08ca-145">Dzięki temu aplikacja do komunikacji z zarejestrowana tylko interfejs API sieci web.</span><span class="sxs-lookup"><span data-stu-id="f08ca-145">This allows your application to communicate with the just-registered web API.</span></span> <span data-ttu-id="f08ca-146">Usługi Azure AD odmówi nawet Zezwalaj aplikacji na poproś dla logowania, chyba że jest on zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="f08ca-146">Azure AD will refuse to even allow your application to ask for sign-in unless it's registered.</span></span> <span data-ttu-id="f08ca-147">Który jest częścią modelu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="f08ca-147">That's part of the security of the model.</span></span>

<span data-ttu-id="f08ca-148">Zakłada się, że w przypadku rejestrowania przykładowej aplikacji odwołuje się do wcześniej.</span><span class="sxs-lookup"><span data-stu-id="f08ca-148">We're assuming that you're registering the sample application referenced earlier.</span></span> <span data-ttu-id="f08ca-149">Jednak ta procedura działa w przypadku dowolnej aplikacji, która projektujesz.</span><span class="sxs-lookup"><span data-stu-id="f08ca-149">But this procedure works for any app that you're developing.</span></span>

> [!NOTE]
> <span data-ttu-id="f08ca-150">Może zastanawiasz się, dlaczego chcesz umieścić zarówno aplikacji, jak i interfejs API sieci web w jednej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="f08ca-150">You might wonder why you're putting both an application and a web API in one tenant.</span></span> <span data-ttu-id="f08ca-151">Ponieważ użytkownik może mieć odgadnąć, można utworzyć aplikację, która uzyskuje dostęp do zewnętrznego interfejsu API, który jest zarejestrowany w usłudze Azure AD z innego dzierżawcę.</span><span class="sxs-lookup"><span data-stu-id="f08ca-151">As you might have guessed, you can build an app that accesses an external API that is registered in Azure AD from another tenant.</span></span> <span data-ttu-id="f08ca-152">Jeśli to zrobisz, który, klienci wyświetli monit o zgodę na korzystanie z interfejsu API w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f08ca-152">If you do that, your customers will be prompted to consent to the use of the API in the application.</span></span> <span data-ttu-id="f08ca-153">Biblioteki uwierzytelniania usługi Active Directory dla systemu iOS zapewnia obsługę tej zgody.</span><span class="sxs-lookup"><span data-stu-id="f08ca-153">Active Directory Authentication Library for iOS takes care of this consent for you.</span></span> <span data-ttu-id="f08ca-154">Jak możemy zapoznać się z bardziej zaawansowane funkcje, zobaczysz, że jest ważnym elementem pracy wymagane do uzyskiwania dostępu do pakietu Microsoft APIs z Azure i pakietu Office, a także innych dostawcy usług.</span><span class="sxs-lookup"><span data-stu-id="f08ca-154">As we explore more advanced features, you'll see that this is an important part of the work needed to access the suite of Microsoft APIs from Azure and Office, as well as any other service provider.</span></span> <span data-ttu-id="f08ca-155">Teraz ponieważ w zarejestrowany zarówno interfejs API sieci web i aplikacji w ramach tej samej dzierżawy, nie zobaczysz żadnych monitów o zgodę.</span><span class="sxs-lookup"><span data-stu-id="f08ca-155">For now, because you registered both your web API and your application under the same tenant, you won't see any prompts for consent.</span></span> <span data-ttu-id="f08ca-156">To jest zwykle w przypadku tworzenia aplikacji, po prostu przez firmę do użycia.</span><span class="sxs-lookup"><span data-stu-id="f08ca-156">This is usually the case if you're developing an application just for your own company to use.</span></span>

1. <span data-ttu-id="f08ca-157">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f08ca-157">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f08ca-158">Na górnym pasku kliknij konto.</span><span class="sxs-lookup"><span data-stu-id="f08ca-158">On the top bar, click your account.</span></span> <span data-ttu-id="f08ca-159">W **katalogu** wybierz dzierżawy usługi Azure AD, które chcesz zarejestrować aplikację.</span><span class="sxs-lookup"><span data-stu-id="f08ca-159">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="f08ca-160">Kliknij przycisk **więcej usług** w okienku po lewej stronie, a następnie wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f08ca-160">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="f08ca-161">Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="f08ca-161">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="f08ca-162">Wprowadź przyjazną nazwę dla aplikacji (na przykład **TodoListClient Android**), wybierz pozycję **natywną aplikację kliencką**i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="f08ca-162">Enter a friendly name for the application (for example, **TodoListClient-Android**), select **Native Client Application**, and click **Next**.</span></span>
6. <span data-ttu-id="f08ca-163">Identyfikator URI przekierowania, można wprowadzić `http://TodoListClient`.</span><span class="sxs-lookup"><span data-stu-id="f08ca-163">For the redirect URI, enter `http://TodoListClient`.</span></span> <span data-ttu-id="f08ca-164">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="f08ca-164">Click **Finish**.</span></span>
7. <span data-ttu-id="f08ca-165">Na stronie aplikacji Znajdź wartość Identyfikatora aplikacji i skopiuj go.</span><span class="sxs-lookup"><span data-stu-id="f08ca-165">From the application page, find the application ID value and copy it.</span></span> <span data-ttu-id="f08ca-166">Należy to później podczas konfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f08ca-166">You'll need this later when configuring your application.</span></span>
8. <span data-ttu-id="f08ca-167">Z **ustawienia** wybierz pozycję **wymagane uprawnienia** i wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="f08ca-167">From the **Settings** page, select **Required Permissions** and select **Add**.</span></span>  <span data-ttu-id="f08ca-168">Zlokalizuj i wybierz TodoListService, dodać **TodoListService dostępu** uprawnienie w obszarze **delegowane uprawnienia**i kliknij przycisk **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="f08ca-168">Locate and select TodoListService, add the **Access TodoListService** permission under **Delegated Permissions**, and click **Done**.</span></span>

<span data-ttu-id="f08ca-169">Tworzenia za pomocą narzędzia Maven, można użyć pom.xml na najwyższym poziomie:</span><span class="sxs-lookup"><span data-stu-id="f08ca-169">To build with Maven, you can use pom.xml at the top level:</span></span>

1. <span data-ttu-id="f08ca-170">Klonuj to repozytorium w wybranym katalogu:</span><span class="sxs-lookup"><span data-stu-id="f08ca-170">Clone this repo into a directory of your choice:</span></span>

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. <span data-ttu-id="f08ca-171">Postępuj zgodnie z instrukcjami [wymagania wstępne dotyczące konfigurowania środowiska Maven dla systemu Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span><span class="sxs-lookup"><span data-stu-id="f08ca-171">Follow the steps in the [prerequisites to set up your Maven environment for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span></span>
3. <span data-ttu-id="f08ca-172">Konfigurowanie emulatora z 19 zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="f08ca-172">Set up the emulator with SDK 19.</span></span>
4. <span data-ttu-id="f08ca-173">Przejdź do folderu głównego, w którym sklonować repozytorium.</span><span class="sxs-lookup"><span data-stu-id="f08ca-173">Go to the root folder where you cloned the repo.</span></span>
5. <span data-ttu-id="f08ca-174">Uruchom następujące polecenie:`mvn clean install`</span><span class="sxs-lookup"><span data-stu-id="f08ca-174">Run this command: `mvn clean install`</span></span>
6. <span data-ttu-id="f08ca-175">Zmień katalog na przykład Szybki Start:`cd samples\hello`</span><span class="sxs-lookup"><span data-stu-id="f08ca-175">Change the directory to the Quick Start sample: `cd samples\hello`</span></span>
7. <span data-ttu-id="f08ca-176">Uruchom następujące polecenie:`mvn android:deploy android:run`</span><span class="sxs-lookup"><span data-stu-id="f08ca-176">Run this command: `mvn android:deploy android:run`</span></span>

   <span data-ttu-id="f08ca-177">Powinna zostać wyświetlona uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f08ca-177">You should see the app starting.</span></span>
8. <span data-ttu-id="f08ca-178">Wprowadź poświadczenia użytkownika testowego próby.</span><span class="sxs-lookup"><span data-stu-id="f08ca-178">Enter test user credentials to try.</span></span>

<span data-ttu-id="f08ca-179">Pakiety JAR zostaną przesłane obok pakietu AAR.</span><span class="sxs-lookup"><span data-stu-id="f08ca-179">JAR packages will be submitted beside the AAR package.</span></span>

## <a name="step-4-download-the-android-adal-and-add-it-to-your-eclipse-workspace"></a><span data-ttu-id="f08ca-180">Krok 4: Pobierz ADAL dla systemu Android i dodaj go do swojego obszaru roboczego programu Eclipse</span><span class="sxs-lookup"><span data-stu-id="f08ca-180">Step 4: Download the Android ADAL and add it to your Eclipse workspace</span></span>
<span data-ttu-id="f08ca-181">Wprowadziliśmy go łatwo jest wiele sposobów używania biblioteki ADAL w projekcie systemu Android:</span><span class="sxs-lookup"><span data-stu-id="f08ca-181">We've made it easy for you to have multiple options to use ADAL in your Android project:</span></span>

* <span data-ttu-id="f08ca-182">Kod źródłowy służy do importowania tej biblioteki do Eclipse i łącza do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f08ca-182">You can use the source code to import this library into Eclipse and link to your application.</span></span>
* <span data-ttu-id="f08ca-183">Jeśli używasz programu Android Studio, można użyć formatu pakietu AAR i odwoływać pliki binarne.</span><span class="sxs-lookup"><span data-stu-id="f08ca-183">If you're using Android Studio, you can use the AAR package format and reference the binaries.</span></span>

### <a name="option-1-source-zip"></a><span data-ttu-id="f08ca-184">Opcja 1: Źródło Zip</span><span class="sxs-lookup"><span data-stu-id="f08ca-184">Option 1: Source Zip</span></span>
<span data-ttu-id="f08ca-185">Aby pobrać kopię kodu źródłowego, kliknij przycisk **Pobierz ZIP** w prawej części strony.</span><span class="sxs-lookup"><span data-stu-id="f08ca-185">To download a copy of the source code, click **Download ZIP** on the right side of the page.</span></span> <span data-ttu-id="f08ca-186">Można także [pobrać z witryny GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span><span class="sxs-lookup"><span data-stu-id="f08ca-186">Or you can [download from GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span></span>

### <a name="option-2-source-via-git"></a><span data-ttu-id="f08ca-187">Opcja 2: Źródło za pomocą narzędzia Git</span><span class="sxs-lookup"><span data-stu-id="f08ca-187">Option 2: Source via Git</span></span>
<span data-ttu-id="f08ca-188">Aby uzyskać kod źródłowy zestawu SDK przez Git, wpisz:</span><span class="sxs-lookup"><span data-stu-id="f08ca-188">To get the source code of the SDK via Git, type:</span></span>

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a><span data-ttu-id="f08ca-189">Opcja 3: Pliki binarne, za pomocą narzędzia Gradle</span><span class="sxs-lookup"><span data-stu-id="f08ca-189">Option 3: Binaries via Gradle</span></span>
<span data-ttu-id="f08ca-190">Pliki binarne można uzyskać z centralnym repozytorium Maven.</span><span class="sxs-lookup"><span data-stu-id="f08ca-190">You can get the binaries from the Maven central repo.</span></span> <span data-ttu-id="f08ca-191">Pakiet AAR mogą zostać włączone w następujący sposób w projekcie w programie Android Studio:</span><span class="sxs-lookup"><span data-stu-id="f08ca-191">The AAR package can be included as follows in your project in Android Studio:</span></span>

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

### <a name="option-4-aar-via-maven"></a><span data-ttu-id="f08ca-192">Opcja 4: AAR za pomocą narzędzia Maven</span><span class="sxs-lookup"><span data-stu-id="f08ca-192">Option 4: AAR via Maven</span></span>
<span data-ttu-id="f08ca-193">Jeśli używasz wtyczek M2Eclipse zależności można określić w pliku pom.xml:</span><span class="sxs-lookup"><span data-stu-id="f08ca-193">If you're using the M2Eclipse plug-in, you can specify the dependency in your pom.xml file:</span></span>

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-the-libs-folder"></a><span data-ttu-id="f08ca-194">Opcja 5: Pakiet JAR w folderze libs</span><span class="sxs-lookup"><span data-stu-id="f08ca-194">Option 5: JAR package inside the libs folder</span></span>
<span data-ttu-id="f08ca-195">Możesz pobrać plik JAR z repozytorium Maven i upuść ją na **biblioteki** folder w projekcie.</span><span class="sxs-lookup"><span data-stu-id="f08ca-195">You can get the JAR file from the Maven repo and drop it into the **libs** folder in your project.</span></span> <span data-ttu-id="f08ca-196">Musisz skopiować wymagane zasoby do projektu również, ponieważ pakiety JAR nie zawierają je.</span><span class="sxs-lookup"><span data-stu-id="f08ca-196">You need to copy the required resources to your project as well, because the JAR packages don't include them.</span></span>

## <a name="step-5-add-references-to-android-adal-to-your-project"></a><span data-ttu-id="f08ca-197">Krok 5: Dodaj odwołania do ADAL dla systemu Android do projektu</span><span class="sxs-lookup"><span data-stu-id="f08ca-197">Step 5: Add references to Android ADAL to your project</span></span>
1. <span data-ttu-id="f08ca-198">Dodaj odwołanie do projektu i określ go jako biblioteka systemu Android.</span><span class="sxs-lookup"><span data-stu-id="f08ca-198">Add a reference to your project and specify it as an Android library.</span></span> <span data-ttu-id="f08ca-199">Jeśli masz pewności, jak to zrobić, więcej informacji można znaleźć [lokacji Android Studio](http://developer.android.com/tools/projects/projects-eclipse.html).</span><span class="sxs-lookup"><span data-stu-id="f08ca-199">If you're uncertain how to do this, you can get more information on the [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span></span>
2. <span data-ttu-id="f08ca-200">Dodaj zależności projektu do debugowania do ustawień projektu.</span><span class="sxs-lookup"><span data-stu-id="f08ca-200">Add the project dependency for debugging into your project settings.</span></span>
3. <span data-ttu-id="f08ca-201">Aktualizowanie pliku AndroidManifest.xml projektu, aby uwzględnić:</span><span class="sxs-lookup"><span data-stu-id="f08ca-201">Update your project's AndroidManifest.xml file to include:</span></span>

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

4. <span data-ttu-id="f08ca-202">Utwórz wystąpienie kontekst AuthenticationContext na Twoje działania głównego.</span><span class="sxs-lookup"><span data-stu-id="f08ca-202">Create an instance of AuthenticationContext at your main activity.</span></span> <span data-ttu-id="f08ca-203">Szczegóły tego wywołania wykraczają poza zakres tego tematu, ale można uzyskać dobry początek, analizując [próbki Android Native Client](https://github.com/AzureADSamples/NativeClient-Android).</span><span class="sxs-lookup"><span data-stu-id="f08ca-203">The details of this call are beyond the scope of this topic, but you can get a good start by looking at the [Android Native Client sample](https://github.com/AzureADSamples/NativeClient-Android).</span></span> <span data-ttu-id="f08ca-204">W poniższym przykładzie SharedPreferences jest domyślne pamięci podręcznej, a Urząd jest w formie `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span><span class="sxs-lookup"><span data-stu-id="f08ca-204">In the following example, SharedPreferences is the default cache, and Authority is in the form of `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span></span>

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. <span data-ttu-id="f08ca-205">Skopiuj ten blok kodu do obsługi koniec AuthenticationActivity po użytkownik wprowadza poświadczenia i odbiera kod autoryzacji:</span><span class="sxs-lookup"><span data-stu-id="f08ca-205">Copy this code block to handle the end of AuthenticationActivity after the user enters credentials and receives an authorization code:</span></span>

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. <span data-ttu-id="f08ca-206">Aby uzyskać token, zdefiniować wywołanie zwrotne:</span><span class="sxs-lookup"><span data-stu-id="f08ca-206">To ask for a token, define a callback:</span></span>

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

7. <span data-ttu-id="f08ca-207">Na koniec uzyskać tokenu przy użyciu wywołanie zwrotne:</span><span class="sxs-lookup"><span data-stu-id="f08ca-207">Finally, ask for a token by using that callback:</span></span>

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

<span data-ttu-id="f08ca-208">Oto objaśnienie parametrów:</span><span class="sxs-lookup"><span data-stu-id="f08ca-208">Here's an explanation of the parameters:</span></span>

* <span data-ttu-id="f08ca-209">*zasób* jest wymagany i próbujesz uzyskać dostęp do zasobu.</span><span class="sxs-lookup"><span data-stu-id="f08ca-209">*resource* is required and is the resource you're trying to access.</span></span>
* <span data-ttu-id="f08ca-210">*ClientID* jest wymagany i pochodzi z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f08ca-210">*clientid* is required and comes from Azure AD.</span></span>
* <span data-ttu-id="f08ca-211">*RedirectUri* nie jest wymagana dla wywołania acquireToken.</span><span class="sxs-lookup"><span data-stu-id="f08ca-211">*RedirectUri* is not required to be provided for the acquireToken call.</span></span> <span data-ttu-id="f08ca-212">Można skonfigurować go jako nazwę pakietu.</span><span class="sxs-lookup"><span data-stu-id="f08ca-212">You can set it up as your package name.</span></span>
* <span data-ttu-id="f08ca-213">*PromptBehavior* pozwala pytanie o poświadczenia pominąć pamięci podręcznej i plik cookie.</span><span class="sxs-lookup"><span data-stu-id="f08ca-213">*PromptBehavior* helps to ask for credentials to skip the cache and cookie.</span></span>
* <span data-ttu-id="f08ca-214">*Wywołanie zwrotne* jest wywoływana po kod autoryzacji są wymieniane dla tokenu.</span><span class="sxs-lookup"><span data-stu-id="f08ca-214">*callback* is called after the authorization code is exchanged for a token.</span></span> <span data-ttu-id="f08ca-215">Ma ona obiektu AuthenticationResult, który ma token dostępu, Data wygasła i identyfikator informacji o tokenie.</span><span class="sxs-lookup"><span data-stu-id="f08ca-215">It has an object of AuthenticationResult, which has access token, date expired, and ID token information.</span></span>
* <span data-ttu-id="f08ca-216">*acquireTokenSilent* jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="f08ca-216">*acquireTokenSilent* is optional.</span></span> <span data-ttu-id="f08ca-217">Można go wywołać do obsługi pamięci podręcznej i token odświeżania.</span><span class="sxs-lookup"><span data-stu-id="f08ca-217">You can call it to handle caching and token refresh.</span></span> <span data-ttu-id="f08ca-218">Umożliwia także wersję usługi synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="f08ca-218">It also provides the sync version.</span></span> <span data-ttu-id="f08ca-219">Akceptuje *userId* jako parametr.</span><span class="sxs-lookup"><span data-stu-id="f08ca-219">It accepts *userId* as a parameter.</span></span>

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="f08ca-220">Przy użyciu tego przewodnika, powinien mieć, co jest potrzebne do pomyślnie integracji z usługą Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f08ca-220">By using this walkthrough, you should have what you need to successfully integrate with Azure Active Directory.</span></span> <span data-ttu-id="f08ca-221">Więcej przykładów dotyczących tej pracy, odwiedź stronę AzureADSamples / repozytorium w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="f08ca-221">For more examples of this working, visit the AzureADSamples/ repository on GitHub.</span></span>

## <a name="important-information"></a><span data-ttu-id="f08ca-222">Ważne informacje</span><span class="sxs-lookup"><span data-stu-id="f08ca-222">Important information</span></span>
### <a name="customization"></a><span data-ttu-id="f08ca-223">Dostosowywanie</span><span class="sxs-lookup"><span data-stu-id="f08ca-223">Customization</span></span>
<span data-ttu-id="f08ca-224">Zasoby aplikacji można zastąpić zasoby biblioteki projektu.</span><span class="sxs-lookup"><span data-stu-id="f08ca-224">Your application resources can overwrite library project resources.</span></span> <span data-ttu-id="f08ca-225">Dzieje się tak, gdy aplikacja została skompilowana.</span><span class="sxs-lookup"><span data-stu-id="f08ca-225">This happens when your app is being built.</span></span> <span data-ttu-id="f08ca-226">Z tego powodu można dostosować sposób, który ma układ działania uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="f08ca-226">For this reason, you can customize authentication activity layout the way you want.</span></span> <span data-ttu-id="f08ca-227">Pamiętaj zachować identyfikator kontrolki używany ADAL (WebView).</span><span class="sxs-lookup"><span data-stu-id="f08ca-227">Be sure to keep the ID of the controls that ADAL uses (WebView).</span></span>

### <a name="broker"></a><span data-ttu-id="f08ca-228">Broker</span><span class="sxs-lookup"><span data-stu-id="f08ca-228">Broker</span></span>
<span data-ttu-id="f08ca-229">Aplikacja Portal firmy usługi Microsoft Intune zawiera składnik brokera.</span><span class="sxs-lookup"><span data-stu-id="f08ca-229">The Microsoft Intune Company Portal app provides the broker component.</span></span> <span data-ttu-id="f08ca-230">Konto jest tworzone w elementu AccountManager.</span><span class="sxs-lookup"><span data-stu-id="f08ca-230">The account is created in AccountManager.</span></span> <span data-ttu-id="f08ca-231">Typ konta jest "com.microsoft.workaccount."</span><span class="sxs-lookup"><span data-stu-id="f08ca-231">The account type is "com.microsoft.workaccount."</span></span> <span data-ttu-id="f08ca-232">Elementu AccountManager umożliwia tylko jedno konto logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="f08ca-232">AccountManager allows only a single SSO account.</span></span> <span data-ttu-id="f08ca-233">Tworzy plik cookie logowania jednokrotnego dla użytkownika po zakończeniu wyzwanie urządzenia dla jednej z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f08ca-233">It creates an SSO cookie for the user after completing the device challenge for one of the apps.</span></span>

<span data-ttu-id="f08ca-234">Konta brokera, jeśli jedno konto użytkownika jest tworzona w to wystawca uwierzytelnienia i można zrezygnować z Pomiń je używa biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="f08ca-234">ADAL uses the broker account if one user account is created at this authenticator and you choose not to skip it.</span></span> <span data-ttu-id="f08ca-235">Można pominąć brokera użytkownikowi:</span><span class="sxs-lookup"><span data-stu-id="f08ca-235">You can skip the broker user with:</span></span>

   `AuthenticationSettings.Instance.setSkipBroker(true);`

<span data-ttu-id="f08ca-236">Należy zarejestrować specjalne RedirectUri użycia brokera.</span><span class="sxs-lookup"><span data-stu-id="f08ca-236">You need to register a special RedirectUri for broker usage.</span></span> <span data-ttu-id="f08ca-237">RedirectUri jest w formacie `msauth://packagename/Base64UrlencodedSignature`.</span><span class="sxs-lookup"><span data-stu-id="f08ca-237">RedirectUri is in the format of `msauth://packagename/Base64UrlencodedSignature`.</span></span> <span data-ttu-id="f08ca-238">Możesz też uzyskać Twojej RedirectUri aplikacji przy użyciu skryptu brokerRedirectPrint.ps1 lub mContext.getBrokerRedirectUri wywołania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="f08ca-238">You can get your RedirectUri for your app by using the script brokerRedirectPrint.ps1 or the API call mContext.getBrokerRedirectUri.</span></span> <span data-ttu-id="f08ca-239">Podpis jest powiązany z podpisywania certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="f08ca-239">The signature is related to your signing certificates.</span></span>

<span data-ttu-id="f08ca-240">Bieżący model brokera jest jeden użytkownik.</span><span class="sxs-lookup"><span data-stu-id="f08ca-240">The current broker model is for one user.</span></span> <span data-ttu-id="f08ca-241">Element AuthenticationContext udostępnia metodę interfejsu API można pobrać użytkownika brokera.</span><span class="sxs-lookup"><span data-stu-id="f08ca-241">AuthenticationContext provides the API method to get the broker user.</span></span>

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

<span data-ttu-id="f08ca-242">Manifest aplikacji powinien mieć następujące uprawnienia do korzystania z kont elementu AccountManager.</span><span class="sxs-lookup"><span data-stu-id="f08ca-242">Your app manifest should have the following permissions to use AccountManager accounts.</span></span> <span data-ttu-id="f08ca-243">Aby uzyskać więcej informacji, zobacz [elementu AccountManager informacji na temat witryny systemu Android](http://developer.android.com/reference/android/accounts/AccountManager.html).</span><span class="sxs-lookup"><span data-stu-id="f08ca-243">For details, see the [AccountManager information on the Android site](http://developer.android.com/reference/android/accounts/AccountManager.html).</span></span>

* <span data-ttu-id="f08ca-244">GET_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="f08ca-244">GET_ACCOUNTS</span></span>
* <span data-ttu-id="f08ca-245">USE_CREDENTIALS</span><span class="sxs-lookup"><span data-stu-id="f08ca-245">USE_CREDENTIALS</span></span>
* <span data-ttu-id="f08ca-246">MANAGE_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="f08ca-246">MANAGE_ACCOUNTS</span></span>

### <a name="authority-url-and-ad-fs"></a><span data-ttu-id="f08ca-247">Adres URL urzędu i usługami AD FS</span><span class="sxs-lookup"><span data-stu-id="f08ca-247">Authority URL and AD FS</span></span>
<span data-ttu-id="f08ca-248">Active Directory Federation Services (AD FS) nie został rozpoznany jako produkcji STS, więc należy włączyć odnajdywania instancji i przekazać wartość false w Konstruktorze kontekst AuthenticationContext.</span><span class="sxs-lookup"><span data-stu-id="f08ca-248">Active Directory Federation Services (AD FS) is not recognized as production STS, so you need to turn of instance discovery and pass false at the AuthenticationContext constructor.</span></span>

<span data-ttu-id="f08ca-249">Adres URL urzędu wymaga wystąpienia usługi STS i [nazwa dzierżawcy](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="f08ca-249">The authority URL needs an STS instance and a [tenant name](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span></span>

### <a name="querying-cache-items"></a><span data-ttu-id="f08ca-250">Wykonywanie zapytania o elementy pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="f08ca-250">Querying cache items</span></span>
<span data-ttu-id="f08ca-251">Biblioteka ADAL udostępnia pamięć podręczną domyślne w SharedPreferences z niektórych prostych pamięci podręcznej funkcje zapytań.</span><span class="sxs-lookup"><span data-stu-id="f08ca-251">ADAL provides a default cache in SharedPreferences with some simple cache query functions.</span></span> <span data-ttu-id="f08ca-252">Możesz uzyskać bieżącej pamięci podręcznej z kontekst AuthenticationContext przy użyciu:</span><span class="sxs-lookup"><span data-stu-id="f08ca-252">You can get the current cache from AuthenticationContext by using:</span></span>

    ITokenCacheStore cache = mContext.getCache();

<span data-ttu-id="f08ca-253">Można też podać implementacji pamięci podręcznej, jeśli chcesz dostosować.</span><span class="sxs-lookup"><span data-stu-id="f08ca-253">You can also provide your cache implementation, if you want to customize it.</span></span>

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a><span data-ttu-id="f08ca-254">Zachowanie monitu</span><span class="sxs-lookup"><span data-stu-id="f08ca-254">Prompt behavior</span></span>
<span data-ttu-id="f08ca-255">ADAL udostępnia opcję, aby określić zachowanie monitu.</span><span class="sxs-lookup"><span data-stu-id="f08ca-255">ADAL provides an option to specify prompt behavior.</span></span> <span data-ttu-id="f08ca-256">PromptBehavior.Auto wyświetli interfejsu użytkownika, jeśli token odświeżania jest nieprawidłowy i wymagane są poświadczenia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f08ca-256">PromptBehavior.Auto will show the UI if the refresh token is invalid and user credentials are required.</span></span> <span data-ttu-id="f08ca-257">PromptBehavior.Always pominie użycia pamięci podręcznej i zawsze pokazuj interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f08ca-257">PromptBehavior.Always will skip the cache usage and always show the UI.</span></span>

### <a name="silent-token-request-from-cache-and-refresh"></a><span data-ttu-id="f08ca-258">Dyskretnej żądania tokenu z pamięci podręcznej i Odśwież</span><span class="sxs-lookup"><span data-stu-id="f08ca-258">Silent token request from cache and refresh</span></span>
<span data-ttu-id="f08ca-259">Dyskretnej żądania tokenu nie używa wyskakujących interfejsu użytkownika i nie wymaga działania.</span><span class="sxs-lookup"><span data-stu-id="f08ca-259">A silent token request does not use the UI pop-up and does not require an activity.</span></span> <span data-ttu-id="f08ca-260">Zwraca tokenu z pamięci podręcznej Jeśli jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="f08ca-260">It returns a token from the cache if available.</span></span> <span data-ttu-id="f08ca-261">Jeśli token utracił ważność, ta metoda próbuje go odświeżyć.</span><span class="sxs-lookup"><span data-stu-id="f08ca-261">If the token is expired, this method tries to refresh it.</span></span> <span data-ttu-id="f08ca-262">Jeśli token odświeżania wygasła lub nie powiodło się, zwraca authenticationexception —.</span><span class="sxs-lookup"><span data-stu-id="f08ca-262">If the refresh token is expired or failed, it returns AuthenticationException.</span></span>

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="f08ca-263">Można również przeprowadzać synchronizacji wywołać za pomocą tej metody.</span><span class="sxs-lookup"><span data-stu-id="f08ca-263">You can also make a sync call by using this method.</span></span> <span data-ttu-id="f08ca-264">Można ustawić wartości null do wywołania zwrotnego lub użyć acquireTokenSilentSync.</span><span class="sxs-lookup"><span data-stu-id="f08ca-264">You can set null to callback or use acquireTokenSilentSync.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="f08ca-265">Diagnostyka</span><span class="sxs-lookup"><span data-stu-id="f08ca-265">Diagnostics</span></span>
<span data-ttu-id="f08ca-266">Są to podstawowego źródła informacji dotyczących diagnozowania problemów:</span><span class="sxs-lookup"><span data-stu-id="f08ca-266">These are the primary sources of information for diagnosing issues:</span></span>

* <span data-ttu-id="f08ca-267">Wyjątki</span><span class="sxs-lookup"><span data-stu-id="f08ca-267">Exceptions</span></span>
* <span data-ttu-id="f08ca-268">Dzienniki</span><span class="sxs-lookup"><span data-stu-id="f08ca-268">Logs</span></span>
* <span data-ttu-id="f08ca-269">Śledzenie sieci</span><span class="sxs-lookup"><span data-stu-id="f08ca-269">Network traces</span></span>

<span data-ttu-id="f08ca-270">Należy zauważyć, że identyfikatorów korelacji Centrum diagnostyki w bibliotece.</span><span class="sxs-lookup"><span data-stu-id="f08ca-270">Note that correlation IDs are central to the diagnostics in the library.</span></span> <span data-ttu-id="f08ca-271">Można ustawić sieci korelacji identyfikatorów na podstawie danego żądania, jeśli chcesz skorelować ADAL żądania z innymi operacjami w kodzie.</span><span class="sxs-lookup"><span data-stu-id="f08ca-271">You can set your correlation IDs on a per-request basis if you want to correlate an ADAL request with other operations in your code.</span></span> <span data-ttu-id="f08ca-272">Jeśli identyfikator korelacji nie jest ustawiona, biblioteka ADAL wygeneruje losowy.</span><span class="sxs-lookup"><span data-stu-id="f08ca-272">If you don't set a correlation ID, ADAL will generate a random one.</span></span> <span data-ttu-id="f08ca-273">Wszystkie komunikaty dziennika i wywołania sieci zostanie następnie opatrzone identyfikatora korelacji.</span><span class="sxs-lookup"><span data-stu-id="f08ca-273">All log messages and network calls will then be stamped with the correlation ID.</span></span> <span data-ttu-id="f08ca-274">Automatycznie wygenerowany identyfikator zmian na każdym żądaniu.</span><span class="sxs-lookup"><span data-stu-id="f08ca-274">The self-generated ID changes on each request.</span></span>

#### <a name="exceptions"></a><span data-ttu-id="f08ca-275">Wyjątki</span><span class="sxs-lookup"><span data-stu-id="f08ca-275">Exceptions</span></span>
<span data-ttu-id="f08ca-276">Wyjątki są dane diagnostyczne pierwszy.</span><span class="sxs-lookup"><span data-stu-id="f08ca-276">Exceptions are the first diagnostic.</span></span> <span data-ttu-id="f08ca-277">Spróbujemy Podaj przydatne komunikaty.</span><span class="sxs-lookup"><span data-stu-id="f08ca-277">We try to provide helpful error messages.</span></span> <span data-ttu-id="f08ca-278">Jeśli znajdziesz taki, który nie jest pomocna, zgłoś problem i Daj nam znać.</span><span class="sxs-lookup"><span data-stu-id="f08ca-278">If you find one that is not helpful, please file an issue and let us know.</span></span> <span data-ttu-id="f08ca-279">Zawierają informacje urządzenia, takie jak modelu oraz liczbę zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="f08ca-279">Include device information such as model and SDK number.</span></span>

#### <a name="logs"></a><span data-ttu-id="f08ca-280">Dzienniki</span><span class="sxs-lookup"><span data-stu-id="f08ca-280">Logs</span></span>
<span data-ttu-id="f08ca-281">Można skonfigurować biblioteki do generowania komunikatów dziennika, które można użyć do diagnozowania problemów.</span><span class="sxs-lookup"><span data-stu-id="f08ca-281">You can configure the library to generate log messages that you can use to help diagnose issues.</span></span> <span data-ttu-id="f08ca-282">Rejestrowanie można skonfigurować za pomocą następujących wywołania, aby skonfigurować wywołanie zwrotne, które ADAL użyje do strony poza wszystkich komunikatach dziennika, ponieważ jest ona generowana.</span><span class="sxs-lookup"><span data-stu-id="f08ca-282">You configure logging by making the following call to configure a callback that ADAL will use to hand off each log message as it's generated.</span></span>

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this to log file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

<span data-ttu-id="f08ca-283">Komunikaty można pisać do niestandardowego pliku dziennika, jak pokazano w poniższym kodzie.</span><span class="sxs-lookup"><span data-stu-id="f08ca-283">Messages can be written to a custom log file, as shown in the following code.</span></span> <span data-ttu-id="f08ca-284">Niestety nie istnieje standardowy sposób pobierania dzienniki z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f08ca-284">Unfortunately, there is no standard way of getting logs from a device.</span></span> <span data-ttu-id="f08ca-285">Brak niektórych usług, które mogą pomóc Ci z tym.</span><span class="sxs-lookup"><span data-stu-id="f08ca-285">There are some services that can help you with this.</span></span> <span data-ttu-id="f08ca-286">Możesz można również zapasów własny, takie jak wysyłanie pliku na serwerze.</span><span class="sxs-lookup"><span data-stu-id="f08ca-286">You can also invent your own, such as sending the file to a server.</span></span>

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

<span data-ttu-id="f08ca-287">Są to poziomów rejestrowania:</span><span class="sxs-lookup"><span data-stu-id="f08ca-287">These are the logging levels:</span></span>
* <span data-ttu-id="f08ca-288">Błąd (wyjątków)</span><span class="sxs-lookup"><span data-stu-id="f08ca-288">Error (exceptions)</span></span>
* <span data-ttu-id="f08ca-289">Warn (ostrzeżenie)</span><span class="sxs-lookup"><span data-stu-id="f08ca-289">Warn (warning)</span></span>
* <span data-ttu-id="f08ca-290">Informacje o (celów informacyjnych)</span><span class="sxs-lookup"><span data-stu-id="f08ca-290">Info (information purposes)</span></span>
* <span data-ttu-id="f08ca-291">Pełne (więcej szczegółów)</span><span class="sxs-lookup"><span data-stu-id="f08ca-291">Verbose (more details)</span></span>

<span data-ttu-id="f08ca-292">Możesz ustawić poziom dziennika następująco:</span><span class="sxs-lookup"><span data-stu-id="f08ca-292">You set the log level like this:</span></span>

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 <span data-ttu-id="f08ca-293">Wszystkie komunikaty dziennika są wysyłane do logcat oprócz wszystkie wywołania zwrotne dziennika niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="f08ca-293">All log messages are sent to logcat, in addition to any custom log callbacks.</span></span>
<span data-ttu-id="f08ca-294">Możesz pobrać dziennik do pliku ze logcat w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f08ca-294">You can get a log to a file from logcat as follows:</span></span>

    adb logcat > "C:\logmsg\logfile.txt"

 <span data-ttu-id="f08ca-295">Aby uzyskać więcej informacji o poleceniach adb, zobacz [logcat informacji na temat witryny systemu Android](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span><span class="sxs-lookup"><span data-stu-id="f08ca-295">For details about adb commands, see the [logcat information on the Android site](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span></span>

#### <a name="network-traces"></a><span data-ttu-id="f08ca-296">Śledzenie sieci</span><span class="sxs-lookup"><span data-stu-id="f08ca-296">Network traces</span></span>
<span data-ttu-id="f08ca-297">Można użyć różnych narzędzi do przechwytywania ruchu HTTP, które generuje biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="f08ca-297">You can use various tools to capture the HTTP traffic that ADAL generates.</span></span>  <span data-ttu-id="f08ca-298">Jest to najbardziej przydatne, jeśli znasz protokołu OAuth lub należy podać informacje diagnostyczne do firmy Microsoft lub innych kanałów pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="f08ca-298">This is most useful if you're familiar with the OAuth protocol or if you need to provide diagnostic information to Microsoft or other support channels.</span></span>

<span data-ttu-id="f08ca-299">Fiddler jest najprostszym narzędzie śledzenia HTTP.</span><span class="sxs-lookup"><span data-stu-id="f08ca-299">Fiddler is the easiest HTTP tracing tool.</span></span> <span data-ttu-id="f08ca-300">Skorzystaj z poniższych linków, aby ustawić ją do poprawnie rekordów ADAL ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="f08ca-300">Use the following links to set it up to correctly record ADAL network traffic.</span></span> <span data-ttu-id="f08ca-301">Dla narzędzia śledzenia, takiego jak Fiddler lub Charlesa powinna być użyteczna musisz skonfigurować je do rejestrowania nieszyfrowanego ruchu protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="f08ca-301">For a tracing tool like Fiddler or Charles to be useful, you must configure it to record unencrypted SSL traffic.</span></span>  

> [!NOTE]
> <span data-ttu-id="f08ca-302">Ślady generowane w ten sposób mogą zawierać wysoko uprzywilejowane informacje, takie jak tokenów dostępu, nazwy użytkowników i hasła.</span><span class="sxs-lookup"><span data-stu-id="f08ca-302">Traces generated in this way might contain highly privileged information such as access tokens, usernames, and passwords.</span></span> <span data-ttu-id="f08ca-303">Jeśli używasz konta produkcji, nie są udostępniane te operacje śledzenia stron trzecich.</span><span class="sxs-lookup"><span data-stu-id="f08ca-303">If you're using production accounts, do not share these traces with third parties.</span></span> <span data-ttu-id="f08ca-304">Jeśli musisz podać śledzenia do osoby, aby uzyskać pomoc techniczną, Odtwórz problem przy użyciu tymczasowego konta użytkowników i hasła, które nie stanowi udostępniania.</span><span class="sxs-lookup"><span data-stu-id="f08ca-304">If you need to supply a trace to someone in order to get support, reproduce the issue by using a temporary account with usernames and passwords that you don't mind sharing.</span></span>

* <span data-ttu-id="f08ca-305">Ze strony firmy Telerik witryny sieci Web: [ustawienia zapasowej Fiddler dla systemu Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span><span class="sxs-lookup"><span data-stu-id="f08ca-305">From the Telerik website: [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span></span>
* <span data-ttu-id="f08ca-306">Z witryny GitHub: [skonfigurować reguły Fiddler dotyczące biblioteki ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span><span class="sxs-lookup"><span data-stu-id="f08ca-306">From GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span></span>

### <a name="dialog-mode"></a><span data-ttu-id="f08ca-307">Tryb okna dialogowego</span><span class="sxs-lookup"><span data-stu-id="f08ca-307">Dialog mode</span></span>
<span data-ttu-id="f08ca-308">Metoda acquireToken bez działania obsługuje wiersza okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f08ca-308">The acquireToken method without activity supports a dialog prompt.</span></span>

### <a name="encryption"></a><span data-ttu-id="f08ca-309">Szyfrowanie</span><span class="sxs-lookup"><span data-stu-id="f08ca-309">Encryption</span></span>
<span data-ttu-id="f08ca-310">Biblioteka ADAL szyfruje tokeny i magazynu w SharedPreferences domyślnie.</span><span class="sxs-lookup"><span data-stu-id="f08ca-310">ADAL encrypts the tokens and store in SharedPreferences by default.</span></span> <span data-ttu-id="f08ca-311">Można przyjrzeć się klasy StorageHelper, aby wyświetlić szczegóły.</span><span class="sxs-lookup"><span data-stu-id="f08ca-311">You can look at the StorageHelper class to see the details.</span></span> <span data-ttu-id="f08ca-312">Android wprowadzonej Android Keystore 4.3 (interfejs API 18) bezpieczny magazyn kluczy prywatnych.</span><span class="sxs-lookup"><span data-stu-id="f08ca-312">Android introduced Android Keystore for 4.3 (API 18) secure storage of private keys.</span></span> <span data-ttu-id="f08ca-313">Biblioteka ADAL użyty dla interfejsu API 18 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="f08ca-313">ADAL uses that for API 18 and higher.</span></span> <span data-ttu-id="f08ca-314">Jeśli chcesz używać biblioteki ADAL dla niższych wersjach zestawu SDK, należy podać klucz tajny w AuthenticationSettings.INSTANCE.setSecretKey.</span><span class="sxs-lookup"><span data-stu-id="f08ca-314">If you want to use ADAL for lower SDK versions, you need to provide a secret key at AuthenticationSettings.INSTANCE.setSecretKey.</span></span>

### <a name="oauth2-bearer-challenge"></a><span data-ttu-id="f08ca-315">Żądania elementu nośnego OAuth2</span><span class="sxs-lookup"><span data-stu-id="f08ca-315">OAuth2 bearer challenge</span></span>
<span data-ttu-id="f08ca-316">Klasa AuthenticationParameters udostępnia funkcję można pobrać authorization_uri z żądania elementu nośnego OAuth2.</span><span class="sxs-lookup"><span data-stu-id="f08ca-316">The AuthenticationParameters class provides functionality to get authorization_uri from the OAuth2 bearer challenge.</span></span>

### <a name="session-cookies-in-webview"></a><span data-ttu-id="f08ca-317">Pliki cookie z sesji w widoku sieci Web</span><span class="sxs-lookup"><span data-stu-id="f08ca-317">Session cookies in WebView</span></span>
<span data-ttu-id="f08ca-318">Android WebView nie wyczyść pliki cookie z sesji, po zamknięciu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f08ca-318">Android WebView does not clear session cookies after the app is closed.</span></span> <span data-ttu-id="f08ca-319">Który można obsługiwać przy użyciu ten przykładowy kod:</span><span class="sxs-lookup"><span data-stu-id="f08ca-319">You can handle that by using this sample code:</span></span>

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

<span data-ttu-id="f08ca-320">Aby uzyskać więcej informacji o plikach cookie, zobacz [CookieSyncManager informacji na temat witryny systemu Android](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span><span class="sxs-lookup"><span data-stu-id="f08ca-320">For details about cookies, see the [CookieSyncManager information on the Android site](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span></span>

### <a name="resource-overrides"></a><span data-ttu-id="f08ca-321">Zastąpienia zasobów</span><span class="sxs-lookup"><span data-stu-id="f08ca-321">Resource overrides</span></span>
<span data-ttu-id="f08ca-322">Biblioteka ADAL zawiera ciągi angielskiej wersji językowej ProgressDialog wiadomości.</span><span class="sxs-lookup"><span data-stu-id="f08ca-322">The ADAL library includes English strings for ProgressDialog messages.</span></span> <span data-ttu-id="f08ca-323">Aplikacji należy je zastąpić, jeśli chcesz zlokalizowanych ciągów.</span><span class="sxs-lookup"><span data-stu-id="f08ca-323">Your application should overwrite them if you want localized strings.</span></span>

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a><span data-ttu-id="f08ca-324">Okno dialogowe NTLM</span><span class="sxs-lookup"><span data-stu-id="f08ca-324">NTLM dialog box</span></span>
<span data-ttu-id="f08ca-325">ADAL w wersji 1.1.0 obsługuje okno dialogowe NTLM, jest przetwarzany przez zdarzenie onReceivedHttpAuthRequest z WebViewClient.</span><span class="sxs-lookup"><span data-stu-id="f08ca-325">ADAL version 1.1.0 supports an NTLM dialog box that is processed through the onReceivedHttpAuthRequest event from WebViewClient.</span></span> <span data-ttu-id="f08ca-326">Można dostosować układ i ciągi dla okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f08ca-326">You can customize the layout and strings for the dialog box.</span></span>

### <a name="cross-app-sso"></a><span data-ttu-id="f08ca-327">Usługa rejestracji Jednokrotnej w wielu aplikacji</span><span class="sxs-lookup"><span data-stu-id="f08ca-327">Cross-app SSO</span></span>
<span data-ttu-id="f08ca-328">Dowiedz się [jak włączyć logowanie Jednokrotne wielu aplikacji w systemie Android przy użyciu biblioteki ADAL](active-directory-sso-android.md).</span><span class="sxs-lookup"><span data-stu-id="f08ca-328">Learn [how to enable cross-app SSO on Android by using ADAL](active-directory-sso-android.md).</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
