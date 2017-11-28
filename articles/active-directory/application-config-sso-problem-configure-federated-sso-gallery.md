---
title: Problem podczas konfiguracji federacyjne logowanie jednokrotne dla aplikacji w galerii Azure AD | Dokumentacja firmy Microsoft
description: "Niektóre typowe problemy mogą wystąpić podczas konfigurowania federacyjnych pojedynczy adres logowania jednokrotnego dla aplikacji, które są wymienione w galerii aplikacji usługi Azure AD za pomocą protokołu SAML"
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
ms.openlocfilehash: 290ca66048281de5e031b0404919bed84ab19ffa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="94c99-103">Problem podczas konfiguracji federacyjne logowanie jednokrotne dla aplikacji w galerii Azure AD</span><span class="sxs-lookup"><span data-stu-id="94c99-103">Problem configuring federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="94c99-104">Jeśli napotkasz problem podczas konfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94c99-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="94c99-105">Sprawdź, czy zostały wykonane wszystkie kroki samouczka dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94c99-105">Verify you have followed all the steps in the tutorial for the application.</span></span> <span data-ttu-id="94c99-106">W konfiguracji aplikacji masz wbudowanego dokumentacji na temat konfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94c99-106">In the application’s configuration, you have inline documentation on how to configure the application.</span></span> <span data-ttu-id="94c99-107">Ponadto można uzyskać dostęp [lista samouczków dotyczących sposobów integracji aplikacji SaaS w usłudze Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) szczegółowe wskazówki krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="94c99-107">Also, you can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

## <a name="cant-add-another-instance-of-the-application"></a><span data-ttu-id="94c99-108">Nie można dodać inne wystąpienie aplikacji</span><span class="sxs-lookup"><span data-stu-id="94c99-108">Can’t add another instance of the application</span></span>

<span data-ttu-id="94c99-109">Aby dodać drugie wystąpienie aplikacji, musisz mieć możliwość:</span><span class="sxs-lookup"><span data-stu-id="94c99-109">To add a second instance of an application, you need to be able to:</span></span>

-   <span data-ttu-id="94c99-110">Skonfiguruj Unikatowy identyfikator dla drugiego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="94c99-110">Configure a unique identifier for the second instance.</span></span> <span data-ttu-id="94c99-111">Nie można skonfigurować w taki sam identyfikator używany po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="94c99-111">You won’t be able to configure the same identifier used for the first instance.</span></span>

-   <span data-ttu-id="94c99-112">Skonfiguruj inny certyfikat niż w pierwszym wystąpieniu.</span><span class="sxs-lookup"><span data-stu-id="94c99-112">Configure a different certificate than the one used for the first instance.</span></span>

<span data-ttu-id="94c99-113">Jeśli aplikacja nie obsługuje dowolne z powyższych.</span><span class="sxs-lookup"><span data-stu-id="94c99-113">If the application doesn’t support any of the above.</span></span> <span data-ttu-id="94c99-114">Następnie, nie będzie można skonfigurować drugie wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="94c99-114">Then, you won’t be able to configure a second instance.</span></span>

## <a name="cant-add-the-identifier-or-the-reply-url"></a><span data-ttu-id="94c99-115">Nie można dodać identyfikatora lub adresu URL odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="94c99-115">Can’t add the Identifier or the Reply URL</span></span>

<span data-ttu-id="94c99-116">Jeśli nie możesz skonfigurować identyfikatora lub adresu URL odpowiedzi, należy potwierdzić, że wartości identyfikatora i adres URL odpowiedzi zgodne wzorce wstępnie skonfigurowane dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94c99-116">If you’re not able to configure the Identifier or the Reply URL, confirm the Identifier and Reply URL values match the patterns pre-configured for the application.</span></span>

<span data-ttu-id="94c99-117">Znajomość wzorce wstępnie skonfigurowane dla aplikacji:</span><span class="sxs-lookup"><span data-stu-id="94c99-117">To know the patterns pre-configured for the application:</span></span>

1.  <span data-ttu-id="94c99-118">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="94c99-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span> <span data-ttu-id="94c99-119">Przejdź do kroku 7.</span><span class="sxs-lookup"><span data-stu-id="94c99-119">Go to step 7.</span></span> <span data-ttu-id="94c99-120">Jeśli jesteś już w bloku konfiguracji aplikacji w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94c99-120">If you are already in the application configuration blade on Azure AD.</span></span>

2.  <span data-ttu-id="94c99-121">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="94c99-121">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="94c99-122">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="94c99-122">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="94c99-123">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="94c99-123">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="94c99-124">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94c99-124">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="94c99-125">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="94c99-125">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="94c99-126">Wybierz aplikację, aby skonfigurować logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="94c99-126">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="94c99-127">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94c99-127">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="94c99-128">Wybierz **na języku SAML logowania jednokrotnego** z **tryb** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="94c99-128">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="94c99-129">Przejdź do **identyfikator** lub **adres URL odpowiedzi** pole tekstowe, w obszarze **sekcji domeny i adres URL.**</span><span class="sxs-lookup"><span data-stu-id="94c99-129">Go to the **Identifier** or **Reply URL** textbox, under the **Domain and URLs section.**</span></span>

10. <span data-ttu-id="94c99-130">Istnieją trzy sposoby znać obsługiwane wzorce dla aplikacji:</span><span class="sxs-lookup"><span data-stu-id="94c99-130">There are three ways to know the supported patterns for the application:</span></span>

   * <span data-ttu-id="94c99-131">W polu tekstowym, zobacz ze wzorcem obsługiwane jako symbol zastępczy *przykład:* <https://contoso.com>.</span><span class="sxs-lookup"><span data-stu-id="94c99-131">In the textbox, you see the supported pattern(s) as a placeholder *Example:* <https://contoso.com>.</span></span>

   * <span data-ttu-id="94c99-132">Jeśli wzorzec nie jest obsługiwana, zostanie wyświetlony czerwony wykrzyknik, podczas próby wprowadź wartość w polu tekstowym.</span><span class="sxs-lookup"><span data-stu-id="94c99-132">if the pattern is not supported, you see a red exclamation mark when you try to enter the value in the textbox.</span></span> <span data-ttu-id="94c99-133">Umieść kursor nad czerwony wykrzyknik, zobaczysz obsługiwane wzorce.</span><span class="sxs-lookup"><span data-stu-id="94c99-133">If you hover your mouse over the red exclamation mark, you see the supported patterns.</span></span>

   * <span data-ttu-id="94c99-134">W samouczku dla aplikacji można także uzyskać informacje o obsługiwanych wzorce.</span><span class="sxs-lookup"><span data-stu-id="94c99-134">In the tutorial for the application, you can also get information about the supported patterns.</span></span> <span data-ttu-id="94c99-135">W obszarze **Konfigurowanie usługi Azure AD rejestracji jednokrotnej** sekcji.</span><span class="sxs-lookup"><span data-stu-id="94c99-135">Under the **Configure Azure AD single sign-on** section.</span></span> <span data-ttu-id="94c99-136">Przejdź do kroku dla skonfigurować wartości w polach **domeny i adres URL** sekcji.</span><span class="sxs-lookup"><span data-stu-id="94c99-136">Go to the step for configured the values under the **Domain and URLs** section.</span></span>

<span data-ttu-id="94c99-137">Jeśli wartości nie są zgodne z wzorców wstępnie skonfigurowane w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94c99-137">If the values don’t match with the patterns pre-configured on Azure AD.</span></span> <span data-ttu-id="94c99-138">Możesz:</span><span class="sxs-lookup"><span data-stu-id="94c99-138">You can:</span></span>

-   <span data-ttu-id="94c99-139">Praca z dostawcą aplikacji, aby uzyskać wartości, które jest zgodny z wzorcem wstępnie skonfigurowane w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="94c99-139">Work with the application vendor to get values that match the pattern pre-configured on Azure AD</span></span>

-   <span data-ttu-id="94c99-140">Można skontaktować się zespół usługi Azure AD < aadapprequest@microsoft.com > lub zostaw komentarz w samouczku, aby zażądać aktualizacji obsługiwane wzorce dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="94c99-140">Or, you can contact Azure AD team at <aadapprequest@microsoft.com> or leave a comment in the tutorial to request the update of the supported patterns for the application</span></span>

## <a name="where-do-i-set-the-entityid-user-identifier-format"></a><span data-ttu-id="94c99-141">Gdy ustawienie formatu EntityID (identyfikator użytkownika)</span><span class="sxs-lookup"><span data-stu-id="94c99-141">Where do I set the EntityID (User Identifier) format</span></span>

<span data-ttu-id="94c99-142">Nie można wybrać format EntityID (identyfikator użytkownika) usługi Azure AD wysyła do aplikacji w odpowiedzi po uwierzytelnieniu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="94c99-142">You won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="94c99-143">Wybrano Azure wybierz AD format dla atrybutu NameID (identyfikator użytkownika) na podstawie wartości lub format żądany przez aplikację w SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="94c99-143">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="94c99-144">Aby uzyskać więcej informacji można znaleźć w artykule [protokołu SAML rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) w sekcji NameIDPolicy,</span><span class="sxs-lookup"><span data-stu-id="94c99-144">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy,</span></span>

## <a name="cant-find-the-azure-ad-metadata-to-complete-the-configuration-with-the-application"></a><span data-ttu-id="94c99-145">Nie można odnaleźć metadanych usługi Azure AD w celu ukończenia konfiguracji z aplikacją</span><span class="sxs-lookup"><span data-stu-id="94c99-145">Can’t find the Azure AD metadata to complete the configuration with the application</span></span>

<span data-ttu-id="94c99-146">Aby pobrać metadanych aplikacji lub certyfikatu z usługi Azure AD, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="94c99-146">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="94c99-147">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="94c99-147">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="94c99-148">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="94c99-148">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="94c99-149">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="94c99-149">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="94c99-150">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="94c99-150">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="94c99-151">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94c99-151">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="94c99-152">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="94c99-152">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="94c99-153">Wybierz aplikację, skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="94c99-153">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="94c99-154">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94c99-154">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="94c99-155">Przejdź do **certyfikat podpisywania SAML** sekcji, a następnie kliknij przycisk **Pobierz** wartość w kolumnie.</span><span class="sxs-lookup"><span data-stu-id="94c99-155">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="94c99-156">W zależności od tego, jakie aplikacji wymaga Konfigurowanie logowania jednokrotnego zobaczysz opcję, aby pobrać metadane XML albo certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="94c99-156">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="94c99-157">Usługi Azure AD nie udostępnia adresu URL można pobrać metadanych.</span><span class="sxs-lookup"><span data-stu-id="94c99-157">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="94c99-158">Można pobrać metadanych jako plik XML.</span><span class="sxs-lookup"><span data-stu-id="94c99-158">The metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-to-customize-saml-claims-sent-to-an-application"></a><span data-ttu-id="94c99-159">Nie wiadomo, jak dostosować SAML oświadczenia wysyłane do aplikacji</span><span class="sxs-lookup"><span data-stu-id="94c99-159">Don't know how to customize SAML claims sent to an application</span></span>

<span data-ttu-id="94c99-160">Aby dowiedzieć się, jak dostosować oświadczeń atrybutów SAML wysyłanych do aplikacji, zobacz [oświadczeń mapowanie w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="94c99-160">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94c99-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="94c99-161">Next steps</span></span>
[<span data-ttu-id="94c99-162">Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="94c99-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
