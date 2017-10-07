---
title: "aaaGet do korzystania z usługi Azure AD authentication przy użyciu hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello Azure tooaccess portalu tooconsume uwierzytelniania usługi Azure Active Directory (Azure AD) hello Azure Media Services API."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 497ad1806b3fd1262802adefb6e12b65ee9f2d61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-hello-azure-portal"></a><span data-ttu-id="71f71-103">Wprowadzenie do uwierzytelniania usługi Azure AD przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="71f71-103">Get started with Azure AD authentication by using hello Azure portal</span></span>

<span data-ttu-id="71f71-104">Dowiedz się, jak toouse hello Azure tooaccess portalu usługi Azure Active Directory (Azure AD) uwierzytelniania tooaccess hello Azure Media Services API.</span><span class="sxs-lookup"><span data-stu-id="71f71-104">Learn how toouse hello Azure portal tooaccess Azure Active Directory (Azure AD) authentication tooaccess hello Azure Media Services API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71f71-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="71f71-105">Prerequisites</span></span>

- <span data-ttu-id="71f71-106">Konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="71f71-106">An Azure account.</span></span> <span data-ttu-id="71f71-107">Jeśli nie masz konta, Rozpocznij od [Azure bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="71f71-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="71f71-108">Konto usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="71f71-108">A Media Services account.</span></span> <span data-ttu-id="71f71-109">Aby uzyskać więcej informacji, zobacz [utworzyć konto usługi Azure Media Services przy użyciu portalu Azure hello](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="71f71-109">For more information, see [Create an Azure Media Services account by using hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="71f71-110">Upewnij się, że przegląd hello [podczas uzyskiwania dostępu do usługi Azure Media usług interfejsu API za pomocą omówienie uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="71f71-110">Make sure you review hello [Accessing Azure Media Services API with Azure AD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="71f71-111">Korzystając z uwierzytelniania usługi Azure AD z usługi Azure Media Services, masz dwie opcje uwierzytelniania:</span><span class="sxs-lookup"><span data-stu-id="71f71-111">When you use Azure AD authentication with Azure Media Services, you have two authentication options:</span></span>

- <span data-ttu-id="71f71-112">**Uwierzytelnianie użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="71f71-112">**User authentication**.</span></span> <span data-ttu-id="71f71-113">Uwierzytelnianie osoby, która używa toointeract aplikacji hello z zasobami usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="71f71-113">Authenticate a person who is using hello app toointeract with Media Services resources.</span></span> <span data-ttu-id="71f71-114">Interaktywna aplikacja Hello należy najpierw monitują hello poświadczenia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="71f71-114">hello interactive application should first prompt hello user for credentials.</span></span> <span data-ttu-id="71f71-115">Przykładem jest aplikacja konsoli zarządzania używane przez zadania kodowania toomonitor autoryzowanych użytkowników lub transmisji strumieniowej na żywo.</span><span class="sxs-lookup"><span data-stu-id="71f71-115">An example is a management console app used by authorized users toomonitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="71f71-116">**Uwierzytelnianie głównej usługi**.</span><span class="sxs-lookup"><span data-stu-id="71f71-116">**Service principal authentication**.</span></span> <span data-ttu-id="71f71-117">Uwierzytelniania usługi.</span><span class="sxs-lookup"><span data-stu-id="71f71-117">Authenticate a service.</span></span> <span data-ttu-id="71f71-118">Aplikacje, które zazwyczaj używają tej metody uwierzytelniania są aplikacji uruchamianych demon usługi, usługi warstwy środkowej lub zaplanowane zadania: aplikacje sieci web funkcji aplikacji, aplikacji logiki, interfejsów API albo mikrousługi.</span><span class="sxs-lookup"><span data-stu-id="71f71-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs: web apps, function apps, logic apps, APIs, or a microservice.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="71f71-119">Obecnie usługa Media Services obsługuje hello Azure kontroli dostępu usługi uwierzytelniania modelu.</span><span class="sxs-lookup"><span data-stu-id="71f71-119">Currently, Media Services supports hello Azure Access Control service authentication model.</span></span> <span data-ttu-id="71f71-120">Jednak na 1 czerwca 2018 zostaną wycofane autoryzacji kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="71f71-120">However, Access Control authorization will be deprecated on June 1, 2018.</span></span> <span data-ttu-id="71f71-121">Zaleca się, jak najszybciej migracji model uwierzytelniania toohello usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71f71-121">We recommend that you migrate toohello Azure AD authentication model as soon as possible.</span></span>

## <a name="select-hello-authentication-method"></a><span data-ttu-id="71f71-122">Wybierz metodę uwierzytelniania hello</span><span class="sxs-lookup"><span data-stu-id="71f71-122">Select hello authentication method</span></span>

1. <span data-ttu-id="71f71-123">W hello [portalu Azure](https://portal.azure.com/), wybierz konto usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="71f71-123">In hello [Azure portal](https://portal.azure.com/), select your Media Services account.</span></span>
2. <span data-ttu-id="71f71-124">Wybierz jak toohello tooconnect Media Services API.</span><span class="sxs-lookup"><span data-stu-id="71f71-124">Select how tooconnect toohello Media Services API.</span></span>

    ![Wybierz połączenie stronę — metoda](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a><span data-ttu-id="71f71-126">Uwierzytelnianie użytkowników</span><span class="sxs-lookup"><span data-stu-id="71f71-126">User authentication</span></span>

<span data-ttu-id="71f71-127">tooconnect toohello interfejsu API usług Media Services przy użyciu hello opcji uwierzytelniania użytkownika, powitania klienta aplikacja potrzebuje toorequest token usługi Azure AD, który ma hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="71f71-127">tooconnect toohello Media Services API by using hello user authentication option, hello client app needs toorequest an Azure AD token that has hello following parameters:</span></span>  

* <span data-ttu-id="71f71-128">Punktu końcowego dzierżawcy usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="71f71-128">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="71f71-129">Identyfikator URI zasobu usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="71f71-129">Media Services resource URI</span></span>
* <span data-ttu-id="71f71-130">Identyfikator klienta aplikacji usługi Media Services (native)</span><span class="sxs-lookup"><span data-stu-id="71f71-130">Media Services (native) application client ID</span></span> 
* <span data-ttu-id="71f71-131">Identyfikator URI przekierowania aplikacji usługi Media Services (native)</span><span class="sxs-lookup"><span data-stu-id="71f71-131">Media Services (native) application redirect URI</span></span> 
* <span data-ttu-id="71f71-132">Identyfikator URI dla usługi REST Media Services</span><span class="sxs-lookup"><span data-stu-id="71f71-132">Resource URI for REST Media Services</span></span>

<span data-ttu-id="71f71-133">Można uzyskać hello wartości dla parametrów na powitania **Media Services API z uwierzytelnieniem użytkownika** strony.</span><span class="sxs-lookup"><span data-stu-id="71f71-133">You can get hello values for these parameters on hello **Media Services API with user authentication** page.</span></span> 

![Uzyskuj dostęp do strony uwierzytelniania użytkownika](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

<span data-ttu-id="71f71-135">Jeśli łączysz toohello interfejsu API usług Media Services przy użyciu hello zestawu .NET SDK nośnika usługi Microsoft hello wymaganych wartości tooyou dostępne jako część hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="71f71-135">If you connect toohello Media Services API by using hello Media Services Microsoft .NET SDK, hello required values are available tooyou as part of hello SDK.</span></span> <span data-ttu-id="71f71-136">Aby uzyskać więcej informacji, zobacz [użycia usługi Azure AD authentication tooaccess hello Azure Media Services API z platformą .NET](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="71f71-136">For more information, see [Use Azure AD authentication tooaccess hello Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="71f71-137">Jeśli nie używasz powitania klienta Media Services na platformie .NET SDK, należy ręcznie utworzyć żądania tokenu usługi Azure AD przy użyciu parametrów hello wcześniejszym opisem.</span><span class="sxs-lookup"><span data-stu-id="71f71-137">If you're not using hello Media Services .NET client SDK, you must manually create an Azure AD token request by using hello parameters discussed earlier.</span></span> <span data-ttu-id="71f71-138">Aby uzyskać więcej informacji, zobacz [jak toouse hello Azure AD Authentication Library tooget hello tokenu usługi Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="71f71-138">For more information, see [How toouse hello Azure AD Authentication Library tooget hello Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

## <a name="service-principal-authentication"></a><span data-ttu-id="71f71-139">Uwierzytelnianie jednostki usługi</span><span class="sxs-lookup"><span data-stu-id="71f71-139">Service principal authentication</span></span>

<span data-ttu-id="71f71-140">tooconnect toohello interfejsu API usług Media Services przy użyciu hello opcji głównej usługi, aplikacji warstwy środkowej (interfejs API sieci web lub aplikacji sieci web) musi toorequest token usługi Azure AD, który ma hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="71f71-140">tooconnect toohello Media Services API by using hello service principal option, your middle-tier app (web API or web application) needs toorequest an Azure AD token that has hello following parameters:</span></span>  

* <span data-ttu-id="71f71-141">Punktu końcowego dzierżawcy usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="71f71-141">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="71f71-142">Identyfikator URI zasobu usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="71f71-142">Media Services resource URI</span></span> 
* <span data-ttu-id="71f71-143">Identyfikator URI dla usługi REST Media Services</span><span class="sxs-lookup"><span data-stu-id="71f71-143">Resource URI for REST Media Services</span></span>
* <span data-ttu-id="71f71-144">Wartości aplikacji w usłudze Azure AD: hello **identyfikator klienta** i **klucz tajny klienta**</span><span class="sxs-lookup"><span data-stu-id="71f71-144">Azure AD application values: hello **client ID** and **client secret**</span></span>

<span data-ttu-id="71f71-145">Można uzyskać hello wartości dla parametrów na powitania **tooMedia interfejsu API usług Uzyskuj dostęp do nazwy głównej usługi** strony.</span><span class="sxs-lookup"><span data-stu-id="71f71-145">You can get hello values for these parameters on hello **Connect tooMedia Services API with service principal** page.</span></span> <span data-ttu-id="71f71-146">Użyj tej strony toocreate Azure nowej aplikacji usługi AD lub tooselect już istniejący.</span><span class="sxs-lookup"><span data-stu-id="71f71-146">Use this page toocreate a new Azure AD application or tooselect an existing one.</span></span> <span data-ttu-id="71f71-147">Po wybraniu hello aplikacji usługi Azure AD, możesz pobrać hello Identyfikatora klienta (identyfikator aplikacji) i generowanie wartości (klucz) klucz tajny klienta hello.</span><span class="sxs-lookup"><span data-stu-id="71f71-147">After you select hello Azure AD app, you can get hello client ID (Application ID) and generate hello client secret (key) values.</span></span> 

![Uzyskuj dostęp do strony głównej usługi](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

<span data-ttu-id="71f71-149">Gdy hello **nazwy głównej usługi** zostanie otwarty blok, zostanie wybrana hello pierwszej aplikacji usługi Azure AD spełniającego hello następujące kryteria:</span><span class="sxs-lookup"><span data-stu-id="71f71-149">When hello **Service Principal** blade opens, hello first Azure AD application that meets hello following criteria is selected:</span></span>

- <span data-ttu-id="71f71-150">Jest zarejestrowaną aplikację usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71f71-150">It is a registered Azure AD application.</span></span>
- <span data-ttu-id="71f71-151">Na powitania konto ma uprawnienia współautora lub Owner Role-Based kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="71f71-151">It has Contributor or Owner Role-Based Access Control permissions on hello account.</span></span>

<span data-ttu-id="71f71-152">Po utworzeniu, lub wybierz aplikację usługi Azure AD, można tworzyć i skopiować klucza tajnego klienta (klucz) i hello Identyfikatora klienta (identyfikator aplikacji).</span><span class="sxs-lookup"><span data-stu-id="71f71-152">After you create or select an Azure AD app, you can create and copy a client secret (key) and hello client ID (Application ID).</span></span> <span data-ttu-id="71f71-153">Identyfikator klucza tajnego i klienta klienta Hello są token dostępu hello tooget wymaganego w tym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="71f71-153">hello client secret and client ID are required tooget hello access token in this scenario.</span></span>

<span data-ttu-id="71f71-154">Jeśli nie masz aplikacji usługi Azure AD toocreate uprawnienia w domenie kontroli aplikacji usługi Azure AD hello hello bloku nie są wyświetlane, a następnie zostanie wyświetlony komunikat ostrzegawczy.</span><span class="sxs-lookup"><span data-stu-id="71f71-154">If you don't have permissions toocreate Azure AD apps in your domain, hello Azure AD app controls of hello blade are not shown, and a warning message is displayed.</span></span>

<span data-ttu-id="71f71-155">Jeśli łączysz toohello interfejsu API usług Media Services przy użyciu hello .NET SDK usługi Media Services, zobacz [użycia usługi Azure AD authentication tooaccess hello Azure Media Services API z platformą .NET](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="71f71-155">If you connect toohello Media Services API by using hello Media Services .NET SDK, see [Use Azure AD authentication tooaccess hello Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="71f71-156">Jeśli nie używasz powitania klienta Media Services na platformie .NET SDK, należy ręcznie utworzyć żądania tokenu usługi Azure AD przy użyciu parametrów hello wcześniejszym opisem.</span><span class="sxs-lookup"><span data-stu-id="71f71-156">If you are not using hello Media Services .NET client SDK, you must manually create an Azure AD token request using hello parameters discussed earlier.</span></span> <span data-ttu-id="71f71-157">Aby uzyskać więcej informacji, zobacz [jak toouse hello Azure AD Authentication Library tooget hello tokenu usługi Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="71f71-157">For more information, see [How toouse hello Azure AD Authentication Library tooget hello Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

### <a name="get-hello-client-id-and-client-secret"></a><span data-ttu-id="71f71-158">Pobierz klucz tajny identyfikator i klienta powitania klienta</span><span class="sxs-lookup"><span data-stu-id="71f71-158">Get hello client ID and client secret</span></span>

<span data-ttu-id="71f71-159">Po wybraniu istniejącej aplikacji usługi Azure AD lub hello wybierz opcję toocreate nowy, są wyświetlane następujące przyciski hello:</span><span class="sxs-lookup"><span data-stu-id="71f71-159">After you select an existing Azure AD app or select hello option toocreate a new one, hello following buttons appear:</span></span>

![Zarządzanie przyciski uprawnienia i zarządzanie aplikacji](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

<span data-ttu-id="71f71-161">Witaj tooopen bloku aplikacji usługi Azure AD, kliknij przycisk **Zarządzanie aplikacją**.</span><span class="sxs-lookup"><span data-stu-id="71f71-161">tooopen hello Azure AD application blade, click **Manage application**.</span></span> <span data-ttu-id="71f71-162">Na powitania **Zarządzanie aplikacją** bloku można uzyskać Identyfikatora klienta aplikacji hello (identyfikator aplikacji).</span><span class="sxs-lookup"><span data-stu-id="71f71-162">On hello **Manage application** blade, you can get hello app's client ID (Application ID).</span></span> <span data-ttu-id="71f71-163">toogenerate klucz tajny klienta (key), wybierz opcję **klucze**.</span><span class="sxs-lookup"><span data-stu-id="71f71-163">toogenerate a client secret (key), select **Keys**.</span></span>

![Zarządzanie aplikacji bloku klucze opcji](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-hello-application"></a><span data-ttu-id="71f71-165">Zarządzanie uprawnieniami i aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="71f71-165">Manage permissions and hello application</span></span>

<span data-ttu-id="71f71-166">Po wybraniu hello aplikacji usługi Azure AD, można zarządzać aplikacji hello i uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="71f71-166">After you select hello Azure AD application, you can manage hello application and permissions.</span></span> <span data-ttu-id="71f71-167">tooset się tooaccess aplikacji z usługą Azure AD innych aplikacji, kliknij przycisk **zarządzania uprawnieniami**.</span><span class="sxs-lookup"><span data-stu-id="71f71-167">tooset up your Azure AD application tooaccess other applications, click **Manage permissions**.</span></span> <span data-ttu-id="71f71-168">Dla zadań zarządzania, takich jak zmiana kluczy i adresy URL odpowiedzi lub manifest aplikacji hello tooedit, kliknij przycisk **Zarządzanie aplikacją**.</span><span class="sxs-lookup"><span data-stu-id="71f71-168">For management tasks, such as changing keys and reply URLs, or tooedit hello application’s manifest, click **Manage application**.</span></span>

### <a name="edit-hello-apps-settings-or-manifest"></a><span data-ttu-id="71f71-169">Edytuj ustawienia aplikacji hello lub manifestu</span><span class="sxs-lookup"><span data-stu-id="71f71-169">Edit hello app's settings or manifest</span></span>

<span data-ttu-id="71f71-170">Ustawienia aplikacji hello tooedit lub manifestu, kliknij przycisk **Zarządzanie aplikacją**.</span><span class="sxs-lookup"><span data-stu-id="71f71-170">tooedit hello app's settings or manifest, click **Manage application**.</span></span>

![Zarządzanie strony aplikacji](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a><span data-ttu-id="71f71-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="71f71-172">Next steps</span></span>

<span data-ttu-id="71f71-173">Rozpoczynanie pracy z [przekazywania plików konta tooyour](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="71f71-173">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
