---
title: aaaProblem Konfigurowanie federacyjne logowanie jednokrotne dla aplikacji w galerii Azure AD | Dokumentacja firmy Microsoft
description: "Niektóre hello typowe problemy mogą wystąpić podczas konfigurowania federacyjnych pojedynczy adres logowania jednokrotnego dla aplikacji, które są wymienione w hello galerii aplikacji usługi Azure AD za pomocą protokołu SAML"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 2ae1e511bd49b19159e1ab83cf79a7db5403b9a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="aacf8-103">Problem podczas konfiguracji federacyjne logowanie jednokrotne dla aplikacji w galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="aacf8-103">Problem configuring federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="aacf8-104">Jeśli napotkasz problem podczas konfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aacf8-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="aacf8-105">Sprawdź, czy zostały wykonane wszystkie kroki hello w samouczku hello aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="aacf8-105">Verify you have followed all hello steps in hello tutorial for hello application.</span></span> <span data-ttu-id="aacf8-106">W konfiguracji aplikacji hello masz dokumentacji wbudowany w sposób tooconfigure hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aacf8-106">In hello application’s configuration, you have inline documentation on how tooconfigure hello application.</span></span> <span data-ttu-id="aacf8-107">Ponadto można uzyskać dostęp hello [lista samouczków dotyczących toointegrate aplikacji SaaS w usłudze Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) szczegółowe wskazówki krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="aacf8-107">Also, you can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

## <a name="cant-add-another-instance-of-hello-application"></a><span data-ttu-id="aacf8-108">Nie można dodać inne wystąpienie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="aacf8-108">Can’t add another instance of hello application</span></span>

<span data-ttu-id="aacf8-109">tooadd drugiego wystąpienia aplikacji, należy toobe stanie:</span><span class="sxs-lookup"><span data-stu-id="aacf8-109">tooadd a second instance of an application, you need toobe able to:</span></span>

-   <span data-ttu-id="aacf8-110">Skonfiguruj Unikatowy identyfikator hello drugie wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="aacf8-110">Configure a unique identifier for hello second instance.</span></span> <span data-ttu-id="aacf8-111">Nie można tego samego identyfikatora używane dla pierwszego wystąpienia hello powitalne tooconfigure stanie.</span><span class="sxs-lookup"><span data-stu-id="aacf8-111">You won’t be able tooconfigure hello same identifier used for hello first instance.</span></span>

-   <span data-ttu-id="aacf8-112">Skonfiguruj inny certyfikat niż hello używane jako hello pierwszego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="aacf8-112">Configure a different certificate than hello one used for hello first instance.</span></span>

<span data-ttu-id="aacf8-113">Jeśli hello aplikacji nie obsługuje żadnego z hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="aacf8-113">If hello application doesn’t support any of hello above.</span></span> <span data-ttu-id="aacf8-114">Następnie nie będzie możliwe tooconfigure drugiego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="aacf8-114">Then, you won’t be able tooconfigure a second instance.</span></span>

## <a name="cant-add-hello-identifier-or-hello-reply-url"></a><span data-ttu-id="aacf8-115">Nie można dodać hello identyfikator lub hello adres URL odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="aacf8-115">Can’t add hello Identifier or hello Reply URL</span></span>

<span data-ttu-id="aacf8-116">Jeśli nie jest możliwe tooconfigure hello identyfikator lub hello adres URL odpowiedzi, potwierdź hello identyfikator i wartości adresu URL odpowiedzi są takie same wzorce hello wstępnie skonfigurowane dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="aacf8-116">If you’re not able tooconfigure hello Identifier or hello Reply URL, confirm hello Identifier and Reply URL values match hello patterns pre-configured for hello application.</span></span>

<span data-ttu-id="aacf8-117">wzorce hello tooknow wstępnie skonfigurowane dla aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="aacf8-117">tooknow hello patterns pre-configured for hello application:</span></span>

1.  <span data-ttu-id="aacf8-118">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.** Przejdź toostep 7.</span><span class="sxs-lookup"><span data-stu-id="aacf8-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.** Go toostep 7.</span></span> <span data-ttu-id="aacf8-119">Jeśli jesteś już w bloku konfiguracji aplikacji hello w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aacf8-119">If you are already in hello application configuration blade on Azure AD.</span></span>

2.  <span data-ttu-id="aacf8-120">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="aacf8-120">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="aacf8-121">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="aacf8-121">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="aacf8-122">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aacf8-122">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="aacf8-123">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aacf8-123">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="aacf8-124">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="aacf8-124">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="aacf8-125">Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="aacf8-125">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="aacf8-126">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aacf8-126">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="aacf8-127">Wybierz **na języku SAML logowania jednokrotnego** z hello **tryb** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="aacf8-127">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="aacf8-128">Przejdź toohello **identyfikator** lub **adres URL odpowiedzi** pole tekstowe, w obszarze hello **sekcji domeny i adres URL.**</span><span class="sxs-lookup"><span data-stu-id="aacf8-128">Go toohello **Identifier** or **Reply URL** textbox, under hello **Domain and URLs section.**</span></span>

10. <span data-ttu-id="aacf8-129">Istnieją trzy sposoby tooknow hello obsługiwane wzorce dla aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="aacf8-129">There are three ways tooknow hello supported patterns for hello application:</span></span>

   * <span data-ttu-id="aacf8-130">W polu tekstowym hello, zobacz wzorcem hello obsługiwane jako symbol zastępczy *przykład:* <https://contoso.com>.</span><span class="sxs-lookup"><span data-stu-id="aacf8-130">In hello textbox, you see hello supported pattern(s) as a placeholder *Example:* <https://contoso.com>.</span></span>

   * <span data-ttu-id="aacf8-131">Jeśli wzorzec hello nie jest obsługiwana, podczas próby tooenter hello wartość w polu tekstowym hello zostanie wyświetlony czerwony wykrzyknik.</span><span class="sxs-lookup"><span data-stu-id="aacf8-131">if hello pattern is not supported, you see a red exclamation mark when you try tooenter hello value in hello textbox.</span></span> <span data-ttu-id="aacf8-132">Umieść kursor nad hello czerwony wykrzyknik, zobaczysz hello obsługiwane wzorce.</span><span class="sxs-lookup"><span data-stu-id="aacf8-132">If you hover your mouse over hello red exclamation mark, you see hello supported patterns.</span></span>

   * <span data-ttu-id="aacf8-133">W samouczku hello aplikacji hello można także uzyskać informacje o wzorce hello obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="aacf8-133">In hello tutorial for hello application, you can also get information about hello supported patterns.</span></span> <span data-ttu-id="aacf8-134">W obszarze hello **Konfigurowanie usługi Azure AD rejestracji jednokrotnej** sekcji.</span><span class="sxs-lookup"><span data-stu-id="aacf8-134">Under hello **Configure Azure AD single sign-on** section.</span></span> <span data-ttu-id="aacf8-135">Przejdź toohello krok w przypadku wartości skonfigurowanych hello hello **domeny i adres URL** sekcji.</span><span class="sxs-lookup"><span data-stu-id="aacf8-135">Go toohello step for configured hello values under hello **Domain and URLs** section.</span></span>

<span data-ttu-id="aacf8-136">Jeśli hello wartości nie są zgodne z wzorców hello wstępnie skonfigurowane w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aacf8-136">If hello values don’t match with hello patterns pre-configured on Azure AD.</span></span> <span data-ttu-id="aacf8-137">Możesz:</span><span class="sxs-lookup"><span data-stu-id="aacf8-137">You can:</span></span>

-   <span data-ttu-id="aacf8-138">Praca z hello aplikacji dostawcy tooget wartości, które jest zgodny z wzorcem hello wstępnie skonfigurowane w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="aacf8-138">Work with hello application vendor tooget values that match hello pattern pre-configured on Azure AD</span></span>

-   <span data-ttu-id="aacf8-139">Można skontaktować się zespół usługi Azure AD < aadapprequest@microsoft.com > lub zostaw komentarz w aktualizacji hello samouczek toorequest hello hello obsługiwane wzorce dla aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="aacf8-139">Or, you can contact Azure AD team at <aadapprequest@microsoft.com> or leave a comment in hello tutorial toorequest hello update of hello supported patterns for hello application</span></span>

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a><span data-ttu-id="aacf8-140">Gdzie ustawić hello format EntityID (identyfikator użytkownika)</span><span class="sxs-lookup"><span data-stu-id="aacf8-140">Where do I set hello EntityID (User Identifier) format</span></span>

<span data-ttu-id="aacf8-141">Możesz nie być w formacie EntityID (identyfikator użytkownika) hello stanie tooselect usługi Azure AD wysyła toohello aplikacji hello odpowiedzi po uwierzytelnieniu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="aacf8-141">You won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="aacf8-142">Azure AD hello wybierz format dla atrybutu NameID hello (identyfikator użytkownika) oparte na wybranej wartości hello lub hello żądany przez aplikację hello w hello SAML AuthRequest format.</span><span class="sxs-lookup"><span data-stu-id="aacf8-142">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="aacf8-143">Aby uzyskać więcej informacji można znaleźć w artykule hello [protokołu SAML rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) sekcji hello NameIDPolicy,</span><span class="sxs-lookup"><span data-stu-id="aacf8-143">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy,</span></span>

## <a name="cant-find-hello-azure-ad-metadata-toocomplete-hello-configuration-with-hello-application"></a><span data-ttu-id="aacf8-144">Nie można znaleźć konfiguracji metadanych usługi Azure AD hello hello toocomplete z aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="aacf8-144">Can’t find hello Azure AD metadata toocomplete hello configuration with hello application</span></span>

<span data-ttu-id="aacf8-145">metadane aplikacji hello toodownload lub certyfikatu z usługi Azure AD, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="aacf8-145">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="aacf8-146">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="aacf8-146">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="aacf8-147">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="aacf8-147">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="aacf8-148">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="aacf8-148">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="aacf8-149">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aacf8-149">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="aacf8-150">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aacf8-150">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="aacf8-151">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="aacf8-151">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="aacf8-152">Wybierz aplikację hello skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="aacf8-152">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="aacf8-153">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aacf8-153">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="aacf8-154">Przejdź za**certyfikat podpisywania SAML** sekcji, a następnie kliknij przycisk **Pobierz** wartość w kolumnie.</span><span class="sxs-lookup"><span data-stu-id="aacf8-154">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="aacf8-155">W zależności od tego, jakie aplikacji hello wymaga Konfigurowanie logowania jednokrotnego zobacz temat albo toodownload opcji hello hello XML metadanych lub hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="aacf8-155">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="aacf8-156">Usługi Azure AD nie udostępnia metadane hello tooget adresu URL.</span><span class="sxs-lookup"><span data-stu-id="aacf8-156">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="aacf8-157">można pobrać metadanych Hello jako plik XML.</span><span class="sxs-lookup"><span data-stu-id="aacf8-157">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a><span data-ttu-id="aacf8-158">Nie wiadomo, jak toocustomize SAML oświadczenia wysyłane tooan aplikacji</span><span class="sxs-lookup"><span data-stu-id="aacf8-158">Don't know how toocustomize SAML claims sent tooan application</span></span>

<span data-ttu-id="aacf8-159">toolearn toocustomize hello SAML atrybutu oświadczenia wysyłane tooyour aplikacji, zobacz [oświadczeń mapowanie w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="aacf8-159">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aacf8-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="aacf8-160">Next steps</span></span>
[<span data-ttu-id="aacf8-161">Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aacf8-161">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
