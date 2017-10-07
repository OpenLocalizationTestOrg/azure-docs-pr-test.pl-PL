---
title: "aplikacje klienta natywnego aaaPublish — usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Opisano sposób toocommunicate aplikacji klienta natywnego tooenable z łącznika serwera Proxy aplikacji w usłudze Azure AD tooprovide bezpieczny dostęp zdalny tooyour lokalnej aplikacji."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f0cae145-e346-4126-948f-3f699747b96e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 0ed2be217bf992f034d8321d5e66569b4cace24f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-native-client-apps-toointeract-with-proxy-applications"></a><span data-ttu-id="703bc-103">Jak toointeract aplikacji klienta natywnego tooenable przy użyciu serwera proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="703bc-103">How tooenable native client apps toointeract with proxy Applications</span></span>

<span data-ttu-id="703bc-104">W aplikacjach tooweb dodawania serwera Proxy usługi Azure Active Directory aplikacji może być również używane toopublish natywnego klienta aplikacji.</span><span class="sxs-lookup"><span data-stu-id="703bc-104">In addition tooweb applications, Azure Active Directory Application Proxy can also be used toopublish native client apps.</span></span> <span data-ttu-id="703bc-105">Aplikacja Native client aplikacji różnią się od aplikacji sieci web, ponieważ są zainstalowane na urządzeniu, podczas gdy aplikacje sieci web są dostępne za pośrednictwem przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="703bc-105">Native client apps differ from web apps because they are installed on a device, while web apps are accessed through a browser.</span></span> 

<span data-ttu-id="703bc-106">Serwer Proxy aplikacji obsługuje aplikacje klientami przez akceptują usługę Azure AD wystawione tokeny, które są wysyłane w standardowych nagłówków HTTP autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="703bc-106">Application Proxy supports native client apps by accepting Azure AD issued tokens that are sent in standard Authorize HTTP headers.</span></span>

![Relacja między użytkowników końcowych, Azure Active Directory i opublikowanych aplikacji](./media/active-directory-application-proxy-native-client/richclientflow.png)

<span data-ttu-id="703bc-108">Użyj hello Azure AD Authentication Library, która zajmuje się uwierzytelniania i obsługuje wiele środowisk klienckich, toopublish natywnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="703bc-108">Use hello Azure AD Authentication Library, which takes care of authentication and supports many client environments, toopublish native applications.</span></span> <span data-ttu-id="703bc-109">Serwer Proxy aplikacji jest dopasowywana do hello [scenariusza tooWeb interfejsu API aplikacji natywnej](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="703bc-109">Application Proxy fits into hello [Native Application tooWeb API scenario](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span></span> <span data-ttu-id="703bc-110">W tym artykule przedstawiono hello cztery kroki toopublish aplikacji natywnej z serwera Proxy aplikacji i hello Azure AD Authentication Library.</span><span class="sxs-lookup"><span data-stu-id="703bc-110">This article walks you through hello four steps toopublish a native application with Application Proxy and hello Azure AD Authentication Library.</span></span> 

## <a name="step-1-publish-your-application"></a><span data-ttu-id="703bc-111">Krok 1: Publikowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="703bc-111">Step 1: Publish your application</span></span>
<span data-ttu-id="703bc-112">Publikowanie aplikacji serwera proxy, jak w przypadku innych aplikacji i przypisz tooaccess użytkowników aplikacji.</span><span class="sxs-lookup"><span data-stu-id="703bc-112">Publish your proxy application as you would any other application and assign users tooaccess your application.</span></span> <span data-ttu-id="703bc-113">Aby uzyskać więcej informacji, zobacz [publikowania aplikacji za pomocą serwera Proxy aplikacji](active-directory-application-proxy-publish.md).</span><span class="sxs-lookup"><span data-stu-id="703bc-113">For more information, see [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

## <a name="step-2-configure-your-application"></a><span data-ttu-id="703bc-114">Krok 2: Konfigurowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="703bc-114">Step 2: Configure your application</span></span>
<span data-ttu-id="703bc-115">Skonfiguruj natywnych aplikacji w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="703bc-115">Configure your native application as follows:</span></span>

1. <span data-ttu-id="703bc-116">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="703bc-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="703bc-117">Przejdź za**usługi Azure Active Directory** > **rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="703bc-117">Navigate too**Azure Active Directory** > **App registrations**.</span></span>
3. <span data-ttu-id="703bc-118">Wybierz **nowej rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="703bc-118">Select **New application registration**.</span></span>
4. <span data-ttu-id="703bc-119">Określ nazwę aplikacji, wybierz pozycję **natywnego** jako typ aplikacji hello i podaj hello identyfikator URI przekierowania dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="703bc-119">Specify a name for your application, select **Native** as hello application type, and provide hello Redirect URI for your application.</span></span> 

   ![Tworzenie nowej rejestracji aplikacji](./media/active-directory-application-proxy-native-client/create.png)
5. <span data-ttu-id="703bc-121">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="703bc-121">Select **Create**.</span></span>

<span data-ttu-id="703bc-122">Aby uzyskać szczegółowe informacje dotyczące tworzenia nowej rejestracji aplikacji, zobacz [Integrowanie aplikacji z usługą Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="703bc-122">For more detailed information about creating a new app registration, see [Integrating applications with Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span></span>


## <a name="step-3-grant-access-tooother-applications"></a><span data-ttu-id="703bc-123">Krok 3: Udziel dostępu tooother aplikacji</span><span class="sxs-lookup"><span data-stu-id="703bc-123">Step 3: Grant access tooother applications</span></span>
<span data-ttu-id="703bc-124">Włącz hello aplikacji natywnej toobe widoczne tooother aplikacje w katalogu:</span><span class="sxs-lookup"><span data-stu-id="703bc-124">Enable hello native application toobe exposed tooother applications in your directory:</span></span>

1. <span data-ttu-id="703bc-125">Nadal **rejestracji aplikacji**, wybierz hello nowej aplikacji natywnej nowo utworzony.</span><span class="sxs-lookup"><span data-stu-id="703bc-125">Still in **App registrations**, select hello new native application that you just created.</span></span>
2. <span data-ttu-id="703bc-126">Wybierz **wymagane uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="703bc-126">Select **Required permissions**.</span></span>
3. <span data-ttu-id="703bc-127">Wybierz pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="703bc-127">Select **Add**.</span></span>
4. <span data-ttu-id="703bc-128">Pierwszym krokiem hello Otwórz **wybierz interfejs API**.</span><span class="sxs-lookup"><span data-stu-id="703bc-128">Open hello first step, **Select an API**.</span></span>
5. <span data-ttu-id="703bc-129">Używać hello wyszukiwania paska toofind hello serwera Proxy aplikacji aplikacji, która została opublikowana w pierwszej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="703bc-129">Use hello search bar toofind hello Application Proxy app that you published in hello first section.</span></span> <span data-ttu-id="703bc-130">Wybierz tej aplikacji, a następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="703bc-130">Choose that app, then click **Select**.</span></span> 

   ![Wyszukaj powitania serwera proxy aplikacji](./media/active-directory-application-proxy-native-client/select_api.png)
6. <span data-ttu-id="703bc-132">Otwórz hello drugi etap **wybierz uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="703bc-132">Open hello second step, **Select permissions**.</span></span>
7. <span data-ttu-id="703bc-133">Za pomocą toogrant wyboru hello aplikacji natywnej dostępu tooyour serwera proxy aplikacji, a następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="703bc-133">Use hello checkbox toogrant your native application access tooyour proxy application, then click **Select**.</span></span>

   ![Udziel dostępu tooproxy aplikacji](./media/active-directory-application-proxy-native-client/select_perms.png)
8. <span data-ttu-id="703bc-135">Wybierz **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="703bc-135">Select **Done**.</span></span>


## <a name="step-4-edit-hello-active-directory-authentication-library"></a><span data-ttu-id="703bc-136">Krok 4: Edytuj hello biblioteki uwierzytelniania usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="703bc-136">Step 4: Edit hello Active Directory Authentication Library</span></span>
<span data-ttu-id="703bc-137">Edytuj kod natywnych aplikacji hello w kontekście uwierzytelniania hello hello tooinclude Active Directory Authentication Library (ADAL) hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="703bc-137">Edit hello native application code in hello authentication context of hello Active Directory Authentication Library (ADAL) tooinclude hello following text:</span></span>

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of hello Native app>",
        new Uri("<Redirect Uri of hello Native App>"),
        PromptBehavior.Never);

//Use hello Access Token tooaccess hello Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

<span data-ttu-id="703bc-138">zmienne Hello w hello przykładowy kod powinien zostać zastąpiony w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="703bc-138">hello variables in hello sample code should be replaced as follows:</span></span>

* <span data-ttu-id="703bc-139">**Identyfikator dzierżawy** można znaleźć w portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="703bc-139">**Tenant ID** can be found in hello Azure portal.</span></span> <span data-ttu-id="703bc-140">Przejdź za**usługi Azure Active Directory** > **właściwości** i kopiowania hello identyfikator katalogu.</span><span class="sxs-lookup"><span data-stu-id="703bc-140">Navigate too**Azure Active Directory** > **Properties** and copy hello Directory ID.</span></span> 
* <span data-ttu-id="703bc-141">**Zewnętrzny adres URL** jest frontonu adres URL hello wprowadzony w powitania serwera Proxy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="703bc-141">**External URL** is hello front-end URL you entered in hello Proxy Application.</span></span> <span data-ttu-id="703bc-142">toofind to wartość, przejdź toohello **serwera proxy aplikacji** sekcji powitania serwera proxy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="703bc-142">toofind this value, navigate toohello **Application proxy** section of hello proxy app.</span></span>
* <span data-ttu-id="703bc-143">**Identyfikator aplikacji** z hello aplikacji natywnej znajduje się na powitania **właściwości** strony natywnej aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="703bc-143">**App ID** of hello native app can be found on hello **Properties** page of hello native application.</span></span>
* <span data-ttu-id="703bc-144">**Identyfikator URI przekierowania aplikacji natywnej hello** znajduje się na powitania **identyfikator URI przekierowania** strony natywnej aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="703bc-144">**Redirect URI of hello native app** can be found on hello **Redirect URIs** page of hello native application.</span></span>


## <a name="see-also"></a><span data-ttu-id="703bc-145">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="703bc-145">See also</span></span>

<span data-ttu-id="703bc-146">Aby uzyskać więcej informacji o przepływie natywnych aplikacji hello, zobacz [tooweb natywnych aplikacji interfejsu API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span><span class="sxs-lookup"><span data-stu-id="703bc-146">For more information about hello native application flow, see [Native application tooweb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span></span>

<span data-ttu-id="703bc-147">Najnowsze wiadomości powitania i aktualizacji, zapoznaj się z hello [Blog dotyczący serwera Proxy aplikacji](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="703bc-147">For hello latest news and updates, check out hello [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
