---
title: "Publikowanie aplikacji Aplikacja native client - usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Uwzględniono również sposób umożliwić aplikacjom natywnego klienta do komunikowania się z łącznika serwera Proxy aplikacji usługi AD platformy Azure do zapewniania bezpiecznego dostępu zdalnego do aplikacji lokalnych."
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
ms.openlocfilehash: bdaa5af6ff5331bc310499586615b48a864c3c5e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-enable-native-client-apps-to-interact-with-proxy-applications"></a><span data-ttu-id="f5ac7-103">Jak włączyć klientami aplikacje do interakcji z serwerem proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="f5ac7-103">How to enable native client apps to interact with proxy Applications</span></span>

<span data-ttu-id="f5ac7-104">Oprócz aplikacji sieci web serwer Proxy usługi Azure Active Directory aplikacji mogą służyć do publikowania aplikacji klienta natywnego.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-104">In addition to web applications, Azure Active Directory Application Proxy can also be used to publish native client apps.</span></span> <span data-ttu-id="f5ac7-105">Aplikacja Native client aplikacji różnią się od aplikacji sieci web, ponieważ są zainstalowane na urządzeniu, podczas gdy aplikacje sieci web są dostępne za pośrednictwem przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-105">Native client apps differ from web apps because they are installed on a device, while web apps are accessed through a browser.</span></span> 

<span data-ttu-id="f5ac7-106">Serwer Proxy aplikacji obsługuje aplikacje klientami przez akceptują usługę Azure AD wystawione tokeny, które są wysyłane w standardowych nagłówków HTTP autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-106">Application Proxy supports native client apps by accepting Azure AD issued tokens that are sent in standard Authorize HTTP headers.</span></span>

![Relacja między użytkowników końcowych, Azure Active Directory i opublikowanych aplikacji](./media/active-directory-application-proxy-native-client/richclientflow.png)

<span data-ttu-id="f5ac7-108">Azure AD Authentication Library, która zajmuje się uwierzytelniania i obsługuje wiele środowiska klienta, należy używać do publikowania natywnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-108">Use the Azure AD Authentication Library, which takes care of authentication and supports many client environments, to publish native applications.</span></span> <span data-ttu-id="f5ac7-109">Serwer Proxy aplikacji jest dopasowywana do [aplikacji natywnej do interfejsu API sieci Web scenariusza](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="f5ac7-109">Application Proxy fits into the [Native Application to Web API scenario](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span></span> <span data-ttu-id="f5ac7-110">W tym artykule przedstawiono cztery kroki publikowania aplikacji natywnej z serwera Proxy aplikacji i Azure AD Authentication Library.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-110">This article walks you through the four steps to publish a native application with Application Proxy and the Azure AD Authentication Library.</span></span> 

## <a name="step-1-publish-your-application"></a><span data-ttu-id="f5ac7-111">Krok 1: Publikowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="f5ac7-111">Step 1: Publish your application</span></span>
<span data-ttu-id="f5ac7-112">Publikowanie serwera proxy aplikacji, jak w przypadku innych aplikacji i przypisać użytkownikom uzyskiwanie dostępu do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-112">Publish your proxy application as you would any other application and assign users to access your application.</span></span> <span data-ttu-id="f5ac7-113">Aby uzyskać więcej informacji, zobacz [publikowania aplikacji za pomocą serwera Proxy aplikacji](active-directory-application-proxy-publish.md).</span><span class="sxs-lookup"><span data-stu-id="f5ac7-113">For more information, see [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

## <a name="step-2-configure-your-application"></a><span data-ttu-id="f5ac7-114">Krok 2: Konfigurowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="f5ac7-114">Step 2: Configure your application</span></span>
<span data-ttu-id="f5ac7-115">Skonfiguruj natywnych aplikacji w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f5ac7-115">Configure your native application as follows:</span></span>

1. <span data-ttu-id="f5ac7-116">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f5ac7-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f5ac7-117">Przejdź do **usługi Azure Active Directory** > **rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-117">Navigate to **Azure Active Directory** > **App registrations**.</span></span>
3. <span data-ttu-id="f5ac7-118">Wybierz **nowej rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-118">Select **New application registration**.</span></span>
4. <span data-ttu-id="f5ac7-119">Określ nazwę aplikacji, wybierz pozycję **natywnego** jako typ aplikacji i podaj identyfikator URI przekierowania dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-119">Specify a name for your application, select **Native** as the application type, and provide the Redirect URI for your application.</span></span> 

   ![Tworzenie nowej rejestracji aplikacji](./media/active-directory-application-proxy-native-client/create.png)
5. <span data-ttu-id="f5ac7-121">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-121">Select **Create**.</span></span>

<span data-ttu-id="f5ac7-122">Aby uzyskać szczegółowe informacje dotyczące tworzenia nowej rejestracji aplikacji, zobacz [Integrowanie aplikacji z usługą Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="f5ac7-122">For more detailed information about creating a new app registration, see [Integrating applications with Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span></span>


## <a name="step-3-grant-access-to-other-applications"></a><span data-ttu-id="f5ac7-123">Krok 3: Udzielanie dostępu do innych aplikacji</span><span class="sxs-lookup"><span data-stu-id="f5ac7-123">Step 3: Grant access to other applications</span></span>
<span data-ttu-id="f5ac7-124">Włącz aplikacji natywnej uwidocznienia do innych aplikacji w katalogu:</span><span class="sxs-lookup"><span data-stu-id="f5ac7-124">Enable the native application to be exposed to other applications in your directory:</span></span>

1. <span data-ttu-id="f5ac7-125">Nadal **rejestracji aplikacji**, wybierz nową aplikację native nowo utworzony.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-125">Still in **App registrations**, select the new native application that you just created.</span></span>
2. <span data-ttu-id="f5ac7-126">Wybierz **wymagane uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-126">Select **Required permissions**.</span></span>
3. <span data-ttu-id="f5ac7-127">Wybierz pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-127">Select **Add**.</span></span>
4. <span data-ttu-id="f5ac7-128">Pierwszym krokiem, otwórz **wybierz interfejs API**.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-128">Open the first step, **Select an API**.</span></span>
5. <span data-ttu-id="f5ac7-129">Użyj pasek wyszukiwania, aby znaleźć aplikację serwera Proxy aplikacji, która została opublikowana w pierwszej sekcji.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-129">Use the search bar to find the Application Proxy app that you published in the first section.</span></span> <span data-ttu-id="f5ac7-130">Wybierz tej aplikacji, a następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-130">Choose that app, then click **Select**.</span></span> 

   ![Wyszukaj aplikację, serwer proxy](./media/active-directory-application-proxy-native-client/select_api.png)
6. <span data-ttu-id="f5ac7-132">Otwórz drugi etap **wybierz uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-132">Open the second step, **Select permissions**.</span></span>
7. <span data-ttu-id="f5ac7-133">Użyj pola wyboru, aby udzielić dostępu aplikacji natywnej do serwera proxy aplikacji, a następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-133">Use the checkbox to grant your native application access to your proxy application, then click **Select**.</span></span>

   ![Udziel dostępu do serwera proxy aplikacji](./media/active-directory-application-proxy-native-client/select_perms.png)
8. <span data-ttu-id="f5ac7-135">Wybierz **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-135">Select **Done**.</span></span>


## <a name="step-4-edit-the-active-directory-authentication-library"></a><span data-ttu-id="f5ac7-136">Krok 4: Edytuj biblioteki uwierzytelniania usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="f5ac7-136">Step 4: Edit the Active Directory Authentication Library</span></span>
<span data-ttu-id="f5ac7-137">Edytuj kod natywnych aplikacji w kontekście uwierzytelniania programu Active Directory Authentication Library (ADAL) do uwzględnienia następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="f5ac7-137">Edit the native application code in the authentication context of the Active Directory Authentication Library (ADAL) to include the following text:</span></span>

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of the Native app>",
        new Uri("<Redirect Uri of the Native App>"),
        PromptBehavior.Never);

//Use the Access Token to access the Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

<span data-ttu-id="f5ac7-138">Zmienne w przykładowym kodzie powinna zostać zastąpiona w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f5ac7-138">The variables in the sample code should be replaced as follows:</span></span>

* <span data-ttu-id="f5ac7-139">**Identyfikator dzierżawy** można znaleźć w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-139">**Tenant ID** can be found in the Azure portal.</span></span> <span data-ttu-id="f5ac7-140">Przejdź do **usługi Azure Active Directory** > **właściwości** i skopiuj nazwę katalogu.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-140">Navigate to **Azure Active Directory** > **Properties** and copy the Directory ID.</span></span> 
* <span data-ttu-id="f5ac7-141">**Zewnętrzny adres URL** jest adres URL frontonu wprowadzony w aplikacji serwera Proxy.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-141">**External URL** is the front-end URL you entered in the Proxy Application.</span></span> <span data-ttu-id="f5ac7-142">Aby znaleźć tę wartość, przejdź do **serwera proxy aplikacji** części aplikacji serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-142">To find this value, navigate to the **Application proxy** section of the proxy app.</span></span>
* <span data-ttu-id="f5ac7-143">**Identyfikator aplikacji** natywnych aplikacji można znaleźć w **właściwości** strony natywnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-143">**App ID** of the native app can be found on the **Properties** page of the native application.</span></span>
* <span data-ttu-id="f5ac7-144">**Identyfikator URI przekierowania aplikacji natywnej** można znaleźć w **identyfikator URI przekierowania** strony natywnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f5ac7-144">**Redirect URI of the native app** can be found on the **Redirect URIs** page of the native application.</span></span>


## <a name="see-also"></a><span data-ttu-id="f5ac7-145">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="f5ac7-145">See also</span></span>

<span data-ttu-id="f5ac7-146">Aby uzyskać więcej informacji o przepływie natywnych aplikacji, zobacz [aplikacji natywnej do interfejsu API sieci web](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span><span class="sxs-lookup"><span data-stu-id="f5ac7-146">For more information about the native application flow, see [Native application to web API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span></span>

<span data-ttu-id="f5ac7-147">Aby zapoznać się z najnowszymi informacjami i aktualizacjami, zobacz [blog dotyczący serwera proxy aplikacji](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="f5ac7-147">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
