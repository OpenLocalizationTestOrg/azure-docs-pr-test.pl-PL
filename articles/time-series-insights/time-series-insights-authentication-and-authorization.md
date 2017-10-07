---
title: "aaaConfigure uwierzytelniania i autoryzacji dla aplikacji niestandardowej, która wywołuje interfejs API Azure czas serii szczegółowych informacji hello | Dokumentacja firmy Microsoft"
description: "W tym samouczku opisano, jak tooconfigure uwierzytelniania i autoryzacji dla aplikacji niestandardowej, która wywołuje hello interfejsu API usługi Azure czas serii Insights"
keywords: 
services: time-series-insights
documentationcenter: 
author: dmdenmsft
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/24/2017
ms.author: dmden
ms.openlocfilehash: 5043468bfc2af3c0d27e8602508d92ba2848409e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a><span data-ttu-id="80eab-103">Uwierzytelnianie i autoryzacja interfejsu API usługi Azure czas serii Insights</span><span class="sxs-lookup"><span data-stu-id="80eab-103">Authentication and authorization for Azure Time Series Insights API</span></span>

<span data-ttu-id="80eab-104">W tym artykule opisano, jak tooconfigure niestandardową aplikację, która wywołuje hello interfejsu API Azure czas serii szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="80eab-104">This article explains how tooconfigure a custom application that calls hello Azure Time Series Insights API.</span></span>

## <a name="service-principal"></a><span data-ttu-id="80eab-105">Nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="80eab-105">Service principal</span></span>

<span data-ttu-id="80eab-106">W tej sekcji opisano, jak tooconfigure tooaccess aplikacji hello interfejsu API Insights serii czasu w imieniu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="80eab-106">This section explains how tooconfigure an application tooaccess hello Time Series Insights API on behalf of hello application.</span></span> <span data-ttu-id="80eab-107">Aplikacja Hello można następnie zapytania na danych lub publikować dane referencyjne w środowisku Insights serii czasu hello z poświadczeniami aplikacji i poświadczenia użytkownika nie hello.</span><span class="sxs-lookup"><span data-stu-id="80eab-107">hello application can then query data or publish reference data in hello Time Series Insights environment with application credentials and not hello user credentials.</span></span>

<span data-ttu-id="80eab-108">Jeśli masz aplikację, która wymaga tooaccess Insights serii czasu, należy skonfigurować aplikację usługi Azure Active Directory i przypisać zasady dostępu hello danych w środowisku Insights serii czasu hello.</span><span class="sxs-lookup"><span data-stu-id="80eab-108">When you have an application that needs tooaccess Time Series Insights, you must set up an Azure Active Directory application and assign hello data access policies in hello Time Series Insights environment.</span></span> <span data-ttu-id="80eab-109">Ta metoda jest preferowana toorunning aplikacji hello z poświadczeniami użytkownika ponieważ:</span><span class="sxs-lookup"><span data-stu-id="80eab-109">This approach is preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="80eab-110">Można przypisać uprawnienia toohello tożsamości aplikacji, które różnią się od własnych uprawnień.</span><span class="sxs-lookup"><span data-stu-id="80eab-110">You can assign permissions toohello app identity that are different from your own permissions.</span></span> <span data-ttu-id="80eab-111">Zazwyczaj te uprawnienia są ograniczone tooexactly jakie aplikacji hello musi toodo.</span><span class="sxs-lookup"><span data-stu-id="80eab-111">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span> <span data-ttu-id="80eab-112">Na przykład można zezwolić tooonly aplikacji hello odczytu danych w określonym środowisku Insights serii czasu.</span><span class="sxs-lookup"><span data-stu-id="80eab-112">For example, you can allow hello app tooonly read data in a particular Time Series Insights environment.</span></span>
* <span data-ttu-id="80eab-113">Użytkownik nie ma poświadczeń aplikacji hello toochange zmienić Twoje obowiązki.</span><span class="sxs-lookup"><span data-stu-id="80eab-113">You don't have toochange hello app's credentials if your responsibilities change.</span></span>
* <span data-ttu-id="80eab-114">Po uruchomieniu skryptu instalacji nienadzorowanej, można użyć certyfikatu lub uwierzytelniania klucza tooautomate aplikacji.</span><span class="sxs-lookup"><span data-stu-id="80eab-114">You can use a certificate or an application key tooautomate authentication when you're running an unattended script.</span></span>

<span data-ttu-id="80eab-115">W tym artykule opisano, jak te kroki za pośrednictwem tooperform hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="80eab-115">This article shows you how tooperform those steps through hello Azure portal.</span></span> <span data-ttu-id="80eab-116">Głównie aplikacji pojedynczej dzierżawy, gdzie aplikacja hello jest zamierzone toorun w tylko jednej z organizacji.</span><span class="sxs-lookup"><span data-stu-id="80eab-116">It focuses on a single-tenant application where hello application is intended toorun in only one organization.</span></span> <span data-ttu-id="80eab-117">Aplikacje pojedynczej dzierżawy jest zazwyczaj używana dla aplikacji — biznesowych, które są uruchamiane w Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="80eab-117">You typically use single-tenant applications for line-of-business applications that run in your organization.</span></span>

<span data-ttu-id="80eab-118">Przepływ instalacji Hello składa się z trzech ogólne kroki:</span><span class="sxs-lookup"><span data-stu-id="80eab-118">hello setup flow consists of three high-level steps:</span></span>

1. <span data-ttu-id="80eab-119">Tworzenie aplikacji w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="80eab-119">Create an application in Azure Active Directory.</span></span>
2. <span data-ttu-id="80eab-120">Autoryzacja to środowisko czasu serii Insights hello tooaccess aplikacji.</span><span class="sxs-lookup"><span data-stu-id="80eab-120">Authorize this application tooaccess hello Time Series Insights environment.</span></span>
3. <span data-ttu-id="80eab-121">Użyj Identyfikatora aplikacji hello i tooacquire klucza tokenu toohello `"https://api.timeseries.azure.com/"` odbiorców lub zasobu.</span><span class="sxs-lookup"><span data-stu-id="80eab-121">Use hello application ID and key tooacquire a token toohello `"https://api.timeseries.azure.com/"` audience or resource.</span></span> <span data-ttu-id="80eab-122">Hello tokenu można następnie hello używane toocall interfejsu API Insights serii czasu.</span><span class="sxs-lookup"><span data-stu-id="80eab-122">hello token can then be used toocall hello Time Series Insights API.</span></span>

<span data-ttu-id="80eab-123">Poniżej przedstawiono szczegółowy opis kroków hello:</span><span class="sxs-lookup"><span data-stu-id="80eab-123">Here are hello detailed steps:</span></span>

1. <span data-ttu-id="80eab-124">Hello portalu Azure, wybierz **usługi Azure Active Directory** > **rejestracji aplikacji** > **nowej rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="80eab-124">In hello Azure portal, select **Azure Active Directory** > **App registrations** > **New application registration**.</span></span>

   ![Nowej rejestracji aplikacji w usłudze Azure Active Directory](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. <span data-ttu-id="80eab-126">Nadaj aplikacji hello toobe typu hello nazwa, wybierz opcję **aplikacji sieci Web / interfejs API**, wybierz dowolny prawidłowy identyfikator URI dla **adres URL logowania**i kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="80eab-126">Give hello application a name, select hello type toobe **Web app / API**, select any valid URI for **Sign-on URL**, and click **Create**.</span></span>

   ![Tworzenie aplikacji hello w usłudze Azure Active Directory](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. <span data-ttu-id="80eab-128">Wybierz nowo utworzony aplikacji i skopiuj jej aplikacji identyfikator tooyour ulubionym edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="80eab-128">Select your newly created application and copy its application ID tooyour favorite text editor.</span></span>

   ![Skopiuj identyfikator aplikacji hello](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. <span data-ttu-id="80eab-130">Wybierz **klucze**, nazwę klucza hello, wybierz hello wygaśnięcia i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="80eab-130">Select **Keys**, enter hello key name, select hello expiration, and click **Save**.</span></span>

   ![Wybierz klucze aplikacji](media/authentication-and-authorization/active-directory-application-keys.png)

   ![Wprowadź nazwę klucza hello i wygaśnięcia i kliknij przycisk Zapisz](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. <span data-ttu-id="80eab-133">Skopiuj hello klucza tooyour ulubionym edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="80eab-133">Copy hello key tooyour favorite text editor.</span></span>

   ![Skopiuj klucz aplikacji hello](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. <span data-ttu-id="80eab-135">W środowisku Insights serii czasu hello, wybierz **zasady dostępu do danych** i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="80eab-135">For hello Time Series Insights environment, select **Data Access Policies** and click **Add**.</span></span>

   ![Dodanie nowych danych dostęp zasad toohello Insights serii czasu środowiska](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. <span data-ttu-id="80eab-137">W hello **wybór użytkownika** okno dialogowe, nazwa aplikacji hello Wklej (z kroku 2) lub identyfikator aplikacji (z kroku 3).</span><span class="sxs-lookup"><span data-stu-id="80eab-137">In hello **Select User** dialog box, paste hello application name (from step 2) or application ID (from step 3).</span></span>

   ![Znajdowanie aplikacji w oknie dialogowym Wybieranie użytkownika hello](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. <span data-ttu-id="80eab-139">Wybierz hello roli (**czytnika** na potrzeby zapytań o dane, **współautora** wykonywania kwerend danych i zmiana danych referencyjnych) i kliknij przycisk **Ok**.</span><span class="sxs-lookup"><span data-stu-id="80eab-139">Select hello role (**Reader** for querying data, **Contributor** for querying data and changing reference data) and click **Ok**.</span></span>

   ![Wybierz w oknie dialogowym Wybierz rolę hello czytelnika lub współautora](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. <span data-ttu-id="80eab-141">Zapisz zasady hello klikając **Ok**.</span><span class="sxs-lookup"><span data-stu-id="80eab-141">Save hello policy by clicking **Ok**.</span></span>

10. <span data-ttu-id="80eab-142">Za pomocą Identyfikatora aplikacji hello (z kroku 3) i token hello tooacquire klucza (z kroku 5) aplikacji w imieniu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="80eab-142">Use hello application ID (from step 3) and application key (from step 5) tooacquire hello token on behalf of hello application.</span></span> <span data-ttu-id="80eab-143">Witaj tokenu można następnie przekazać w hello `Authorization` nagłówka podczas wywołania aplikacji hello hello interfejsu API Insights serii czasu.</span><span class="sxs-lookup"><span data-stu-id="80eab-143">hello token can then be passed in hello `Authorization` header when hello application calls hello Time Series Insights API.</span></span>

    <span data-ttu-id="80eab-144">Jeśli używasz programu C#, można użyć następującego kodu tooacquire hello token w imieniu aplikacji hello hello.</span><span class="sxs-lookup"><span data-stu-id="80eab-144">If you're using C#, you can use hello following code tooacquire hello token on behalf of hello application.</span></span> <span data-ttu-id="80eab-145">Dla kompletnego przykładu, zobacz [zapytania na danych przy użyciu języka C#](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="80eab-145">For a complete sample, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set hello resource URI toohello Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of hello application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a><span data-ttu-id="80eab-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="80eab-146">Next steps</span></span>

<span data-ttu-id="80eab-147">Użyj Identyfikatora aplikacji hello i klucz w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="80eab-147">Use hello application ID and key in your application.</span></span> <span data-ttu-id="80eab-148">Przykładowy kod wywołuje hello czasu serii Insights API, zobacz [zapytania na danych przy użyciu języka C#](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="80eab-148">For sample code that calls hello Time Series Insights API, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="80eab-149">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="80eab-149">See also</span></span>

* <span data-ttu-id="80eab-150">[Zapytania interfejsu API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) dla hello pełną dokumentację interfejsu API zapytania</span><span class="sxs-lookup"><span data-stu-id="80eab-150">[Query API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) for hello full Query API reference</span></span>
* [<span data-ttu-id="80eab-151">Utwórz usługę podmiotu zabezpieczeń w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="80eab-151">Create a service principal in hello Azure portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
