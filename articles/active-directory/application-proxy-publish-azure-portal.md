---
title: "aaaPublish aplikacji za pomocą serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Publikowanie chmury toohello aplikacji lokalnie z serwera Proxy aplikacji usługi Azure AD w hello portalu Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ed5458467fb7d4376f65a222f1ba5f23cfdfc57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="b4c9b-103">Publikowanie aplikacji przy użyciu serwera proxy aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4c9b-103">Publish applications using Azure AD Application Proxy</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b4c9b-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b4c9b-104">Azure portal</span></span>](application-proxy-publish-azure-portal.md)
> * [<span data-ttu-id="b4c9b-105">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b4c9b-105">Azure classic portal</span></span>](active-directory-application-proxy-publish.md)

<span data-ttu-id="b4c9b-106">Serwer Proxy aplikacji usługi Azure Active Directory (AD) pomaga obsługuje pracowników zdalnych, publikując lokalnymi toobe aplikacji udostępnianych za pośrednictwem hello internet.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-106">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications toobe accessed over hello internet.</span></span> <span data-ttu-id="b4c9b-107">Możesz opublikować te aplikacje za pomocą hello Azure tooprovide portalu bezpiecznego dostępu zdalnego spoza sieci.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-107">You can publish these applications through hello Azure portal tooprovide secure remote access from outside your network.</span></span>

<span data-ttu-id="b4c9b-108">W tym artykule przedstawiono hello kroki toopublish aplikacji lokalnej za pomocą serwera Proxy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-108">This article walks you through hello steps toopublish an on-premises app with Application Proxy.</span></span> <span data-ttu-id="b4c9b-109">Po zakończeniu pracy w tym artykule, użytkownicy będą się tooaccess mogli zdalnie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-109">After you complete this article, your users will be able tooaccess your app remotely.</span></span> <span data-ttu-id="b4c9b-110">I gotowe tooconfigure będzie dodatkowe funkcje dla aplikacji hello, takie jak pojedyncze logowania jednokrotnego, spersonalizowane informacje i wymagania dotyczące zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-110">And you'll be ready tooconfigure extra features for hello application like single sign-on, personalized information, and security requirements.</span></span>

<span data-ttu-id="b4c9b-111">Jeśli masz tooApplication nowego serwera Proxy, więcej informacji na temat tej funkcji z artykułem hello [jak tooprovide bezpiecznego dostępu zdalnego aplikacje lokalne tooon](active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b4c9b-111">If you're new tooApplication Proxy, learn more about this feature with hello article [How tooprovide secure remote access tooon-premises applications](active-directory-application-proxy-get-started.md).</span></span>


## <a name="publish-an-on-premises-app-for-remote-access"></a><span data-ttu-id="b4c9b-112">Publikowanie aplikacji lokalnych dla funkcji dostępu zdalnego</span><span class="sxs-lookup"><span data-stu-id="b4c9b-112">Publish an on-premises app for remote access</span></span>

<span data-ttu-id="b4c9b-113">Wykonaj te kroki toopublish aplikacjami za pomocą serwera Proxy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-113">Follow these steps toopublish your apps with Application Proxy.</span></span> <span data-ttu-id="b4c9b-114">Jeśli nie zostały już pobrane i skonfigurować łącznik w organizacji, należy przejść za[rozpoczęcie pracy z serwerem Proxy aplikacji i zainstalować łącznik hello](active-directory-application-proxy-enable.md) najpierw, a następnie opublikować aplikację.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-114">If you haven't already downloaded and configured a connector for your organization, go too[Get started with Application Proxy and install hello connector](active-directory-application-proxy-enable.md) first, and then publish your app.</span></span>

> [!TIP]
> <span data-ttu-id="b4c9b-115">Jeśli testujesz się serwera Proxy aplikacji dla powitania po raz pierwszy, wybierz aplikację, który jest skonfigurowany do uwierzytelniania opartego na hasłach.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-115">If you're testing out Application Proxy for hello first time, choose an application that's set up for password-based authentication.</span></span> <span data-ttu-id="b4c9b-116">Serwer Proxy aplikacji obsługuje inne typy uwierzytelniania, ale są oparte na hasłach aplikacji hello najprostszym tooget się i szybko uruchomić.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-116">Application Proxy supports other types of authentication, but password-based apps are hello easiest tooget up and running quickly.</span></span> 

1. <span data-ttu-id="b4c9b-117">Zaloguj się jako administrator w hello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b4c9b-117">Sign in as an administrator in hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b4c9b-118">Wybierz **usługi Azure Active Directory** > **aplikacje dla przedsiębiorstw** > **nowej aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-118">Select **Azure Active Directory** > **Enterprise applications** > **New application**.</span></span>

  ![Dodawanie aplikacji dla przedsiębiorstw](./media/application-proxy-publish-azure-portal/add-app.png)

3. <span data-ttu-id="b4c9b-120">Wybierz **wszystkie**, a następnie wybierz pozycję **lokalnej aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-120">Select **All**, then select **On-premises application**.</span></span>  

  ![Dodawanie aplikacji](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. <span data-ttu-id="b4c9b-122">Podaj następujące informacje na temat aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="b4c9b-122">Provide hello following information about your application:</span></span>

   - <span data-ttu-id="b4c9b-123">**Nazwa**: hello nazwę aplikacji hello, która będzie wyświetlana na panelu dostępu hello i w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-123">**Name**: hello name of hello application that will appear on hello access panel and in hello Azure portal.</span></span> 

   - <span data-ttu-id="b4c9b-124">**Wewnętrzny adres URL**: hello adres URL, którego używasz aplikacji hello tooaccess z poziomu sieci prywatnej.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-124">**Internal URL**: hello URL that you use tooaccess hello application from inside your private network.</span></span> <span data-ttu-id="b4c9b-125">Na powitania toopublish serwera wewnętrznej bazy danych, można wprowadzić określoną ścieżkę, zablokowaniu nieopublikowane rest hello powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-125">You can provide a specific path on hello backend server toopublish, while hello rest of hello server is unpublished.</span></span> <span data-ttu-id="b4c9b-126">W ten sposób można publikować różne Lokacje na tym samym serwerze co różnych aplikacji hello i nadaj każdej z nich własnej nazwy i reguły dostępu.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-126">In this way, you can publish different sites on hello same server as different apps, and give each one its own name and access rules.</span></span>

     > [!TIP]
     > <span data-ttu-id="b4c9b-127">Po opublikowaniu ścieżki, upewnij się, czy zawiera wszystkie obrazy niezbędne hello, skrypty i arkusze stylów dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-127">If you publish a path, make sure that it includes all hello necessary images, scripts, and style sheets for your application.</span></span> <span data-ttu-id="b4c9b-128">Na przykład jeśli aplikacja jest w https://yourapp/app i przy użyciu obrazów znajdujący się w https://yourapp/media, następnie należy opublikować https://yourapp/ jako ścieżka hello.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-128">For example, if your app is at https://yourapp/app and uses images located at https://yourapp/media, then you should publish https://yourapp/ as hello path.</span></span> <span data-ttu-id="b4c9b-129">Ten wewnętrzny adres URL nie ma strony docelowej hello toobe, które użytkownicy zobaczą.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-129">This internal URL doesn't have toobe hello landing page your users see.</span></span> <span data-ttu-id="b4c9b-130">Aby uzyskać więcej informacji, zobacz [ustawić niestandardową stronę główną dla opublikowanych aplikacji](application-proxy-office365-app-launcher.md).</span><span class="sxs-lookup"><span data-stu-id="b4c9b-130">For more information, see [Set a custom home page for published apps](application-proxy-office365-app-launcher.md).</span></span>

   - <span data-ttu-id="b4c9b-131">**Zewnętrzny adres URL**: hello adres Użytkownicy przechodzą tooin kolejności tooaccess hello aplikacji z spoza sieci.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-131">**External URL**: hello address your users will go tooin order tooaccess hello app from outside your network.</span></span> <span data-ttu-id="b4c9b-132">Jeśli nie chcesz toouse hello domyślny serwer Proxy aplikacji domeny, przeczytaj o [domen niestandardowych w serwera Proxy aplikacji usługi Azure AD](active-directory-application-proxy-custom-domains.md).</span><span class="sxs-lookup"><span data-stu-id="b4c9b-132">If you don't want toouse hello default Application Proxy domain, read about [custom domains in Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md).</span></span>
   - <span data-ttu-id="b4c9b-133">**Wstępne uwierzytelnianie**: jak serwer Proxy aplikacji zweryfikuje użytkowników przed udzieleniem im dostępu tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-133">**Pre Authentication**: How Application Proxy verifies users before giving them access tooyour application.</span></span> 

     - <span data-ttu-id="b4c9b-134">Azure Active Directory: Serwer Proxy aplikacji przekierowuje toosign użytkowników za pomocą usługi Azure AD, które umożliwi uwierzytelnienie ich uprawnień dla katalogu hello i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-134">Azure Active Directory: Application Proxy redirects users toosign in with Azure AD, which authenticates their permissions for hello directory and application.</span></span> <span data-ttu-id="b4c9b-135">Zaleca się pozostawienie tej opcji jako domyślny hello tak, aby można było korzystać z funkcji zabezpieczeń usługi Azure AD, takich jak dostęp warunkowy i usługa Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-135">We recommend keeping this option as hello default, so that you can take advantage of Azure AD security features like conditional access and Multi-Factor Authentication.</span></span>
     - <span data-ttu-id="b4c9b-136">Przekazywanie: Użytkownicy nie mają tooauthenticate względem aplikacji hello tooaccess usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-136">Passthrough: Users don't have tooauthenticate against Azure Active Directory tooaccess hello application.</span></span> <span data-ttu-id="b4c9b-137">Nadal można skonfigurować uwierzytelniania wymogi hello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-137">You can still set up authentication requirements on hello backend.</span></span>
   - <span data-ttu-id="b4c9b-138">**Łącznik grupy**: łączników hello dostępu zdalnego tooyour aplikacji i grup łącznika ułatwić organizowanie łączniki i aplikacje według obszaru, sieci lub cel.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-138">**Connector Group**: Connectors process hello remote access tooyour application, and connector groups help you organize connectors and apps by region, network, or purpose.</span></span> <span data-ttu-id="b4c9b-139">Jeśli nie masz jeszcze utworzony łącznik grupy aplikacji przypisano zbyt**domyślne**.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-139">If you don't have any connector groups created yet, your app is assigned too**Default**.</span></span>

   ![Konfigurowanie aplikacji](./media/application-proxy-publish-azure-portal/configure-app.png)
5. <span data-ttu-id="b4c9b-141">Jeśli to konieczne, należy skonfigurować dodatkowe ustawienia.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-141">If necessary, configure additional settings.</span></span> <span data-ttu-id="b4c9b-142">W przypadku większości aplikacji należy zachować te ustawienia w ich domyślne Stany.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-142">For most applications, you should keep these settings in their default states.</span></span> 
   - <span data-ttu-id="b4c9b-143">**Limit czasu aplikacji zaplecza**: Ustaw tę wartość za**długi** tylko wtedy, gdy aplikacja jest powolne tooauthenticate i nawiąż połączenie.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-143">**Backend Application Timeout**: Set this value too**Long** only if your application is slow tooauthenticate and connect.</span></span> 
   - <span data-ttu-id="b4c9b-144">**Tłumaczenie adresów URL w nagłówkach**: Zachowaj tę wartość jako **tak** , chyba że hello oryginalnego nagłówka hosta w żądaniu uwierzytelniania hello wymaganych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-144">**Translate URLs in Headers**: Keep this value as **Yes** unless your application required hello original host header in hello authentication request.</span></span>
   - <span data-ttu-id="b4c9b-145">**Tłumaczenie adresów URL w aplikacji treści**: Zachowaj tę wartość jako **nr** chyba, że masz aplikacji lokalnych tooother łącza HTML zapisane na stałe, a nie używaj domen niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-145">**Translate URLs in Application Body**: Keep this value as **No** unless you have hardcoded HTML links tooother on-premises applications, and don't use custom domains.</span></span> <span data-ttu-id="b4c9b-146">Aby uzyskać więcej informacji, zobacz [Link tłumaczenia z serwerem Proxy aplikacji](application-proxy-link-translation.md).</span><span class="sxs-lookup"><span data-stu-id="b4c9b-146">For more information, see [Link translation with Application Proxy](application-proxy-link-translation.md).</span></span>
   
   ![Konfigurowanie aplikacji](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. <span data-ttu-id="b4c9b-148">Wybierz pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-148">Select **Add**.</span></span>


## <a name="add-a-test-user"></a><span data-ttu-id="b4c9b-149">Dodaj użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="b4c9b-149">Add a test user</span></span> 

<span data-ttu-id="b4c9b-150">tootest, że aplikacja została opublikowana poprawnie, Dodaj konto użytkownika testu.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-150">tootest that your app was published correctly, add a test user account.</span></span> <span data-ttu-id="b4c9b-151">Sprawdź, czy to konto ma już aplikacji hello tooaccess uprawnienia z wewnątrz sieci firmowej hello.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-151">Verify that this account already has permissions tooaccess hello app from inside hello corporate network.</span></span>

1. <span data-ttu-id="b4c9b-152">W bloku szybki start hello, wybierz **przypisać użytkownika do testowania**.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-152">Back on hello Quick start blade, select **Assign a user for testing**.</span></span>

  ![Przypisz użytkownika do testowania](./media/application-proxy-publish-azure-portal/assign-user.png)

2. <span data-ttu-id="b4c9b-154">Na powitania użytkowników i grup bloku, wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-154">On hello Users and groups blade, select **Add**.</span></span>

  ![Dodaj użytkownika lub grupę](./media/application-proxy-publish-azure-portal/add-user.png)

3. <span data-ttu-id="b4c9b-156">W bloku przypisania Dodaj hello, wybierz **użytkowników i grup** następnie wybierz konto hello ma tooadd.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-156">On hello Add assignment blade, select **Users and groups** then choose hello account you want tooadd.</span></span> 
4. <span data-ttu-id="b4c9b-157">Wybierz **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-157">Select **Assign**.</span></span>

## <a name="test-your-published-app"></a><span data-ttu-id="b4c9b-158">Testowanie opublikowanych aplikacji</span><span class="sxs-lookup"><span data-stu-id="b4c9b-158">Test your published app</span></span>

<span data-ttu-id="b4c9b-159">W przeglądarce Przejdź toohello zewnętrzny adres URL, skonfigurowanego podczas hello publikowania kroku.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-159">In your browser, navigate toohello external URL that you configured during hello publish step.</span></span> <span data-ttu-id="b4c9b-160">Powinny pojawić się ekranu startowego hello i można toosign stanie się przy użyciu hello testowe konto można skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-160">You should see hello start screen, and be able toosign in with hello test account you set up.</span></span>

![Testowanie opublikowanych aplikacji](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a><span data-ttu-id="b4c9b-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b4c9b-162">Next steps</span></span>
- <span data-ttu-id="b4c9b-163">[Pobierz łączniki](active-directory-application-proxy-enable.md) i [tworzenie grup łącznika](active-directory-application-proxy-connectors-azure-portal.md) toopublish aplikacji w różnych sieciach i lokalizacje.</span><span class="sxs-lookup"><span data-stu-id="b4c9b-163">[Download connectors](active-directory-application-proxy-enable.md) and [create connector groups](active-directory-application-proxy-connectors-azure-portal.md) toopublish applications on separate networks and locations.</span></span>

- <span data-ttu-id="b4c9b-164">[Konfigurowanie rejestracji jednokrotnej](application-proxy-sso-azure-portal.md) nowo opublikowanych aplikacji</span><span class="sxs-lookup"><span data-stu-id="b4c9b-164">[Set up single sign-on](application-proxy-sso-azure-portal.md) for your newly published app</span></span>
