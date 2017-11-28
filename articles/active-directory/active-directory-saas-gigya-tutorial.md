---
title: 'Samouczek: Integracji Azure Active Directory z Gigya | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Gigya."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2c7d200b-9242-44a5-ac8a-ab3214a78e41
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 1992c5ad09b097563377a488fbf5a375f6511020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gigya"></a><span data-ttu-id="673e2-103">Samouczek: Integracji Azure Active Directory z Gigya</span><span class="sxs-lookup"><span data-stu-id="673e2-103">Tutorial: Azure Active Directory integration with Gigya</span></span>

<span data-ttu-id="673e2-104">Z tego samouczka, dowiesz się, jak toointegrate Gigya w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="673e2-104">In this tutorial, you learn how toointegrate Gigya with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="673e2-105">Integracja z usługą Azure AD Gigya zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="673e2-105">Integrating Gigya with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="673e2-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooGigya</span><span class="sxs-lookup"><span data-stu-id="673e2-106">You can control in Azure AD who has access tooGigya</span></span>
- <span data-ttu-id="673e2-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooGigya (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="673e2-107">You can enable your users tooautomatically get signed-on tooGigya (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="673e2-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="673e2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="673e2-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="673e2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="673e2-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="673e2-110">Prerequisites</span></span>

<span data-ttu-id="673e2-111">tooconfigure integracji z usługą Azure AD z Gigya należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="673e2-111">tooconfigure Azure AD integration with Gigya, you need hello following items:</span></span>

- <span data-ttu-id="673e2-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="673e2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="673e2-113">Gigya logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="673e2-113">A Gigya single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="673e2-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="673e2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="673e2-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="673e2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="673e2-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="673e2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="673e2-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="673e2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="673e2-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="673e2-118">Scenario description</span></span>
<span data-ttu-id="673e2-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="673e2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="673e2-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="673e2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="673e2-121">Dodawanie Gigya z galerii hello</span><span class="sxs-lookup"><span data-stu-id="673e2-121">Adding Gigya from hello gallery</span></span>
2. <span data-ttu-id="673e2-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="673e2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gigya-from-hello-gallery"></a><span data-ttu-id="673e2-123">Dodawanie Gigya z galerii hello</span><span class="sxs-lookup"><span data-stu-id="673e2-123">Adding Gigya from hello gallery</span></span>
<span data-ttu-id="673e2-124">tooconfigure hello integracji Gigya do usługi Azure AD, należy tooadd Gigya z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="673e2-124">tooconfigure hello integration of Gigya into Azure AD, you need tooadd Gigya from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="673e2-125">**tooadd Gigya z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="673e2-125">**tooadd Gigya from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="673e2-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="673e2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="673e2-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="673e2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="673e2-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="673e2-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="673e2-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="673e2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="673e2-133">W polu wyszukiwania hello wpisz **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="673e2-133">In hello search box, type **Gigya**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_search.png)

5. <span data-ttu-id="673e2-135">W panelu wyników hello zaznacz **Gigya**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="673e2-135">In hello results panel, select **Gigya**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="673e2-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="673e2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="673e2-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Gigya w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="673e2-138">In this section, you configure and test Azure AD single sign-on with Gigya based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="673e2-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Gigya jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="673e2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Gigya is tooa user in Azure AD.</span></span> <span data-ttu-id="673e2-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Gigya musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="673e2-140">In other words, a link relationship between an Azure AD user and hello related user in Gigya needs toobe established.</span></span>

<span data-ttu-id="673e2-141">W Gigya, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="673e2-141">In Gigya, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="673e2-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Gigya, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="673e2-142">tooconfigure and test Azure AD single sign-on with Gigya, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="673e2-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="673e2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="673e2-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="673e2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="673e2-145">**[Tworzenie użytkownika testowego Gigya](#creating-a-gigya-test-user)**  -toohave odpowiednikiem Simona Britta w Gigya, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="673e2-145">**[Creating a Gigya test user](#creating-a-gigya-test-user)** - toohave a counterpart of Britta Simon in Gigya that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="673e2-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="673e2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="673e2-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="673e2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="673e2-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="673e2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="673e2-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Gigya.</span><span class="sxs-lookup"><span data-stu-id="673e2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Gigya application.</span></span>

<span data-ttu-id="673e2-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Gigya, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="673e2-150">**tooconfigure Azure AD single sign-on with Gigya, perform hello following steps:**</span></span>

1. <span data-ttu-id="673e2-151">W portalu Azure na powitania hello **Gigya** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="673e2-151">In hello Azure portal, on hello **Gigya** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="673e2-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="673e2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_samlbase.png)

3. <span data-ttu-id="673e2-155">Na powitania **Gigya domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="673e2-155">On hello **Gigya Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_url.png)

    <span data-ttu-id="673e2-157">a.</span><span class="sxs-lookup"><span data-stu-id="673e2-157">a.</span></span> <span data-ttu-id="673e2-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`http://<companyname>.gigya.com`</span><span class="sxs-lookup"><span data-stu-id="673e2-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<companyname>.gigya.com`</span></span>

    <span data-ttu-id="673e2-159">b.</span><span class="sxs-lookup"><span data-stu-id="673e2-159">b.</span></span> <span data-ttu-id="673e2-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://fidm.gigya.com/saml/v2.0/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="673e2-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://fidm.gigya.com/saml/v2.0/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="673e2-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="673e2-161">These values are not real.</span></span> <span data-ttu-id="673e2-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="673e2-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="673e2-163">Skontaktuj się z [zespołem pomocy technicznej klienta Gigya](https://www.gigya.com/support-policy/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="673e2-163">Contact [Gigya Client support team](https://www.gigya.com/support-policy/) tooget these values.</span></span> 
 
4. <span data-ttu-id="673e2-164">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="673e2-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_certificate.png) 

5. <span data-ttu-id="673e2-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="673e2-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-gigya-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="673e2-168">Na powitania **konfiguracji Gigya** kliknij **skonfigurować Gigya** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="673e2-168">On hello **Gigya Configuration** section, click **Configure Gigya** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="673e2-169">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="673e2-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_configure.png) 

7. <span data-ttu-id="673e2-171">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Gigya jako administrator.</span><span class="sxs-lookup"><span data-stu-id="673e2-171">In a different web browser window, log into your Gigya company site as an administrator.</span></span>

8. <span data-ttu-id="673e2-172">Przejdź za**ustawienia \> logowania SAML**, a następnie kliknij przycisk hello **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="673e2-172">Go too**Settings \> SAML Login**, and then click hello **Add** button.</span></span>
   
    <span data-ttu-id="673e2-173">![Logowania SAML](./media/active-directory-saas-gigya-tutorial/ic789532.png "logowania SAML")</span><span class="sxs-lookup"><span data-stu-id="673e2-173">![SAML Login](./media/active-directory-saas-gigya-tutorial/ic789532.png "SAML Login")</span></span>

9. <span data-ttu-id="673e2-174">W hello **logowania SAML** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="673e2-174">In hello **SAML Login** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="673e2-175">![Konfiguracja SAML](./media/active-directory-saas-gigya-tutorial/ic789533.png "Konfiguracja SAML")</span><span class="sxs-lookup"><span data-stu-id="673e2-175">![SAML Configuration](./media/active-directory-saas-gigya-tutorial/ic789533.png "SAML Configuration")</span></span>
   
    <span data-ttu-id="673e2-176">a.</span><span class="sxs-lookup"><span data-stu-id="673e2-176">a.</span></span> <span data-ttu-id="673e2-177">W hello **nazwa** tekstowym, wpisz nazwę dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="673e2-177">In hello **Name** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="673e2-178">b.</span><span class="sxs-lookup"><span data-stu-id="673e2-178">b.</span></span> <span data-ttu-id="673e2-179">W **wystawcy** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="673e2-179">In **Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure Portal.</span></span> 
   
    <span data-ttu-id="673e2-180">c.</span><span class="sxs-lookup"><span data-stu-id="673e2-180">c.</span></span> <span data-ttu-id="673e2-181">W **pojedynczy znak na adres URL usługi** pole tekstowe, Wklej wartość hello **pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="673e2-181">In **Single Sign-On Service URL** textbox, paste hello value of **Single Sign-On Service URL** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="673e2-182">d.</span><span class="sxs-lookup"><span data-stu-id="673e2-182">d.</span></span> <span data-ttu-id="673e2-183">W **Format Identyfikatora nazwy** pole tekstowe, Wklej wartość hello **Format identyfikatora nazwy** , które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="673e2-183">In **Name ID Format** textbox, paste hello value of **Name Identifier Format** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="673e2-184">e.</span><span class="sxs-lookup"><span data-stu-id="673e2-184">e.</span></span> <span data-ttu-id="673e2-185">Otwieranie certyfikatu zakodowanego base-64 w Notatniku pobrany z portalu Azure, hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu X.509** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="673e2-185">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="673e2-186">f.</span><span class="sxs-lookup"><span data-stu-id="673e2-186">f.</span></span> <span data-ttu-id="673e2-187">Kliknij przycisk **Zapisz ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="673e2-187">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="673e2-188">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="673e2-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="673e2-189">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="673e2-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="673e2-190">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="673e2-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="673e2-191">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="673e2-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="673e2-192">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="673e2-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="673e2-194">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="673e2-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="673e2-195">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="673e2-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="673e2-197">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="673e2-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="673e2-199">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="673e2-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="673e2-201">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="673e2-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="673e2-203">a.</span><span class="sxs-lookup"><span data-stu-id="673e2-203">a.</span></span> <span data-ttu-id="673e2-204">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="673e2-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="673e2-205">b.</span><span class="sxs-lookup"><span data-stu-id="673e2-205">b.</span></span> <span data-ttu-id="673e2-206">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="673e2-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="673e2-207">c.</span><span class="sxs-lookup"><span data-stu-id="673e2-207">c.</span></span> <span data-ttu-id="673e2-208">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="673e2-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="673e2-209">d.</span><span class="sxs-lookup"><span data-stu-id="673e2-209">d.</span></span> <span data-ttu-id="673e2-210">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="673e2-210">Click **Create**.</span></span>
 
### <a name="creating-a-gigya-test-user"></a><span data-ttu-id="673e2-211">Tworzenie użytkownika testowego Gigya</span><span class="sxs-lookup"><span data-stu-id="673e2-211">Creating a Gigya test user</span></span>

<span data-ttu-id="673e2-212">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do Gigya muszą mieć przydzielone do Gigya.</span><span class="sxs-lookup"><span data-stu-id="673e2-212">In order tooenable Azure AD users toolog into Gigya, they must be provisioned into Gigya.</span></span>  
<span data-ttu-id="673e2-213">W przypadku hello Gigya Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="673e2-213">In hello case of Gigya, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="673e2-214">tooprovision kont użytkowników, wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="673e2-214">tooprovision a user accounts, perform hello following steps:</span></span>

1. <span data-ttu-id="673e2-215">Zaloguj się za tooyour **Gigya** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="673e2-215">Log in tooyour **Gigya** company site as an administrator.</span></span>

2. <span data-ttu-id="673e2-216">Przejdź za**Admin \> Zarządzanie użytkownikami**, a następnie kliknij przycisk **zaprosić użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="673e2-216">Go too**Admin \> Manage Users**, and then click **Invite Users**.</span></span>
   
    <span data-ttu-id="673e2-217">![Zarządzaj użytkownikami](./media/active-directory-saas-gigya-tutorial/ic789535.png "Zarządzanie użytkownikami")</span><span class="sxs-lookup"><span data-stu-id="673e2-217">![Manage Users](./media/active-directory-saas-gigya-tutorial/ic789535.png "Manage Users")</span></span>

3. <span data-ttu-id="673e2-218">W oknie dialogowym zaprosić użytkowników hello wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="673e2-218">On hello Invite Users dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="673e2-219">![Zaprosić użytkowników](./media/active-directory-saas-gigya-tutorial/ic789536.png "zaprosić użytkowników")</span><span class="sxs-lookup"><span data-stu-id="673e2-219">![Invite Users](./media/active-directory-saas-gigya-tutorial/ic789536.png "Invite Users")</span></span>
   
    <span data-ttu-id="673e2-220">a.</span><span class="sxs-lookup"><span data-stu-id="673e2-220">a.</span></span> <span data-ttu-id="673e2-221">W hello **E-mail** pole tekstowe, typ hello aliasów e-mail ma tooprovision prawidłowe konto usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="673e2-221">In hello **Email** textbox, type hello email alias of a valid Azure Active Directory account you want tooprovision.</span></span>
    
    <span data-ttu-id="673e2-222">b.</span><span class="sxs-lookup"><span data-stu-id="673e2-222">b.</span></span> <span data-ttu-id="673e2-223">Kliknij przycisk **zaprosić użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="673e2-223">Click **Invite User**.</span></span>
      
    > [!NOTE]
    > <span data-ttu-id="673e2-224">Właściciel konta usługi Azure Active Directory Hello otrzymają wiadomość e-mail zawierającą łącze tooconfirm hello konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="673e2-224">hello Azure Active Directory account holder will receive an email that includes a link tooconfirm hello account before it becomes active.</span></span>
    > 
    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="673e2-225">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="673e2-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="673e2-226">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooGigya.</span><span class="sxs-lookup"><span data-stu-id="673e2-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGigya.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="673e2-228">**tooassign tooGigya Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="673e2-228">**tooassign Britta Simon tooGigya, perform hello following steps:**</span></span>

1. <span data-ttu-id="673e2-229">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="673e2-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="673e2-231">Z listy aplikacji hello wybierz **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="673e2-231">In hello applications list, select **Gigya**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_app.png) 

3. <span data-ttu-id="673e2-233">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="673e2-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="673e2-235">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="673e2-235">Click **Add** button.</span></span> <span data-ttu-id="673e2-236">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="673e2-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="673e2-238">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="673e2-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="673e2-239">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="673e2-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="673e2-240">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="673e2-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="673e2-241">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="673e2-241">Testing single sign-on</span></span>

<span data-ttu-id="673e2-242">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="673e2-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="673e2-243">Po kliknięciu kafelka Gigya hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Gigya aplikacji.</span><span class="sxs-lookup"><span data-stu-id="673e2-243">When you click hello Gigya tile in hello Access Panel, you should get automatically signed-on tooyour Gigya application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="673e2-244">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="673e2-244">Additional resources</span></span>

* [<span data-ttu-id="673e2-245">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="673e2-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="673e2-246">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="673e2-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_203.png

