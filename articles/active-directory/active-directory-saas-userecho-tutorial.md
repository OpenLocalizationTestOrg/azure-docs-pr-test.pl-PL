---
title: 'Samouczek: Integracji Azure Active Directory z UserEcho | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i UserEcho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bedd916b-8f69-4b50-9b8d-56f4ee3bd3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: efe4a94ed6e5d22d153565d4782850eac4dff37b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-userecho"></a><span data-ttu-id="8e8ff-103">Samouczek: Integracji Azure Active Directory z UserEcho</span><span class="sxs-lookup"><span data-stu-id="8e8ff-103">Tutorial: Azure Active Directory integration with UserEcho</span></span>

<span data-ttu-id="8e8ff-104">Z tego samouczka, dowiesz się, jak toointegrate UserEcho w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8e8ff-104">In this tutorial, you learn how toointegrate UserEcho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8e8ff-105">Integracja z usługą Azure AD UserEcho zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="8e8ff-105">Integrating UserEcho with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8e8ff-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooUserEcho</span><span class="sxs-lookup"><span data-stu-id="8e8ff-106">You can control in Azure AD who has access tooUserEcho</span></span>
- <span data-ttu-id="8e8ff-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooUserEcho (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e8ff-107">You can enable your users tooautomatically get signed-on tooUserEcho (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8e8ff-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8e8ff-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8e8ff-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8e8ff-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e8ff-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8e8ff-110">Prerequisites</span></span>

<span data-ttu-id="8e8ff-111">tooconfigure integracji z usługą Azure AD z UserEcho należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8e8ff-111">tooconfigure Azure AD integration with UserEcho, you need hello following items:</span></span>

- <span data-ttu-id="8e8ff-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e8ff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8e8ff-113">UserEcho logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8e8ff-113">A UserEcho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8e8ff-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8e8ff-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="8e8ff-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8e8ff-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8e8ff-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8e8ff-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8e8ff-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="8e8ff-118">Scenario description</span></span>
<span data-ttu-id="8e8ff-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8e8ff-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="8e8ff-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8e8ff-121">Dodawanie UserEcho z galerii hello</span><span class="sxs-lookup"><span data-stu-id="8e8ff-121">Adding UserEcho from hello gallery</span></span>
2. <span data-ttu-id="8e8ff-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8e8ff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-userecho-from-hello-gallery"></a><span data-ttu-id="8e8ff-123">Dodawanie UserEcho z galerii hello</span><span class="sxs-lookup"><span data-stu-id="8e8ff-123">Adding UserEcho from hello gallery</span></span>
<span data-ttu-id="8e8ff-124">tooconfigure hello integracji UserEcho do usługi Azure AD, należy tooadd UserEcho z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-124">tooconfigure hello integration of UserEcho into Azure AD, you need tooadd UserEcho from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8e8ff-125">**tooadd UserEcho z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8e8ff-125">**tooadd UserEcho from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e8ff-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="8e8ff-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8e8ff-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="8e8ff-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="8e8ff-133">W polu wyszukiwania hello wpisz **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-133">In hello search box, type **UserEcho**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_search.png)

5. <span data-ttu-id="8e8ff-135">W panelu wyników hello zaznacz **UserEcho**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-135">In hello results panel, select **UserEcho**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8e8ff-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8e8ff-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8e8ff-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z UserEcho w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-138">In this section, you configure and test Azure AD single sign-on with UserEcho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8e8ff-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w UserEcho jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UserEcho is tooa user in Azure AD.</span></span> <span data-ttu-id="8e8ff-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w UserEcho musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-140">In other words, a link relationship between an Azure AD user and hello related user in UserEcho needs toobe established.</span></span>

<span data-ttu-id="8e8ff-141">W UserEcho, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-141">In UserEcho, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8e8ff-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z UserEcho, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8e8ff-142">tooconfigure and test Azure AD single sign-on with UserEcho, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8e8ff-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8e8ff-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8e8ff-145">**[Tworzenie użytkownika testowego UserEcho](#creating-a-userecho-test-user)**  -toohave odpowiednikiem Simona Britta w UserEcho, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-145">**[Creating a UserEcho test user](#creating-a-userecho-test-user)** - toohave a counterpart of Britta Simon in UserEcho that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8e8ff-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8e8ff-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8e8ff-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8e8ff-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8e8ff-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji UserEcho.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UserEcho application.</span></span>

<span data-ttu-id="8e8ff-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z UserEcho, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8e8ff-150">**tooconfigure Azure AD single sign-on with UserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e8ff-151">W portalu Azure na powitania hello **UserEcho** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-151">In hello Azure portal, on hello **UserEcho** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="8e8ff-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_samlbase.png)

3. <span data-ttu-id="8e8ff-155">Na powitania **UserEcho domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8e8ff-155">On hello **UserEcho Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_url.png)

    <span data-ttu-id="8e8ff-157">a.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-157">a.</span></span> <span data-ttu-id="8e8ff-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.userecho.com/`</span><span class="sxs-lookup"><span data-stu-id="8e8ff-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.userecho.com/`</span></span>

    <span data-ttu-id="8e8ff-159">b.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-159">b.</span></span> <span data-ttu-id="8e8ff-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.userecho.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="8e8ff-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.userecho.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8e8ff-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-161">These values are not real.</span></span> <span data-ttu-id="8e8ff-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8e8ff-163">Skontaktuj się z [zespołem pomocy technicznej klienta UserEcho](https://feedback.userecho.com/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-163">Contact [UserEcho Client support team](https://feedback.userecho.com/) tooget these values.</span></span> 

4. <span data-ttu-id="8e8ff-164">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_certificate.png) 

5. <span data-ttu-id="8e8ff-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-userecho-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8e8ff-168">Na powitania **konfiguracji UserEcho** kliknij **skonfigurować UserEcho** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-168">On hello **UserEcho Configuration** section, click **Configure UserEcho** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8e8ff-169">Kopiuj hello **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="8e8ff-169">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_configure.png) 

7. <span data-ttu-id="8e8ff-171">W innym oknie przeglądarki Zaloguj się w witrynie firmy UserEcho tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-171">In another browser window, sign on tooyour UserEcho company site as an administrator.</span></span>

8. <span data-ttu-id="8e8ff-172">Witaj pasku narzędzi u góry hello, kliknij przycisk z menu hello tooexpand nazwa użytkownika, a następnie kliknij **Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-172">In hello toolbar on hello top, click your user name tooexpand hello menu, and then click **Setup**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png) 

9. <span data-ttu-id="8e8ff-174">Kliknij przycisk **integracji**.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-174">Click **Integrations**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_07.png) 

10. <span data-ttu-id="8e8ff-176">Kliknij przycisk **witryny sieci Web**, a następnie kliknij przycisk **logowanie jednokrotne (SAML2)**.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-176">Click **Website**, and then click **Single sign-on (SAML2)**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_08.png) 

11. <span data-ttu-id="8e8ff-178">Na powitania **logowanie jednokrotne (SAML)** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8e8ff-178">On hello **Single sign-on (SAML)** page, perform hello following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_09.png)
    
    <span data-ttu-id="8e8ff-180">a.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-180">a.</span></span> <span data-ttu-id="8e8ff-181">Jako **włączone SAML**, wybierz pozycję **tak**.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-181">As **SAML-enabled**, select **Yes**.</span></span>
    
    <span data-ttu-id="8e8ff-182">b.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-182">b.</span></span> <span data-ttu-id="8e8ff-183">Wklej **SAML pojedynczy znak na adres URL usługi**, która została skopiowana z hello portalu Azure do hello **adres URL logowania jednokrotnego SAML** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-183">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **SAML SSO URL** textbox.</span></span>
    
    <span data-ttu-id="8e8ff-184">c.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-184">c.</span></span> <span data-ttu-id="8e8ff-185">Wklej **Sign-Out adres URL**, która została skopiowana z hello portalu Azure do hello **logoout zdalnego adresu URL** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-185">Paste **Sign-Out URL**, which you have copied from hello Azure portal into hello **Remote logoout URL** textbox.</span></span>
    
    <span data-ttu-id="8e8ff-186">d.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-186">d.</span></span> <span data-ttu-id="8e8ff-187">Otwórz pobrany certyfikat w Notatniku, hello kopiowania zawartości, a następnie wklej go do hello **certyfikatu X.509** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-187">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **X.509 Certificate** textbox.</span></span>
    
    <span data-ttu-id="8e8ff-188">e.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-188">e.</span></span> <span data-ttu-id="8e8ff-189">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="8e8ff-190">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="8e8ff-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8e8ff-191">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8e8ff-192">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8e8ff-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8e8ff-193">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e8ff-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="8e8ff-194">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="8e8ff-196">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8e8ff-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e8ff-197">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8e8ff-199">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8e8ff-201">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8e8ff-203">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8e8ff-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8e8ff-205">a.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-205">a.</span></span> <span data-ttu-id="8e8ff-206">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8e8ff-207">b.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-207">b.</span></span> <span data-ttu-id="8e8ff-208">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8e8ff-209">c.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-209">c.</span></span> <span data-ttu-id="8e8ff-210">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8e8ff-211">d.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-211">d.</span></span> <span data-ttu-id="8e8ff-212">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-212">Click **Create**.</span></span>
 
### <a name="creating-a-userecho-test-user"></a><span data-ttu-id="8e8ff-213">Tworzenie użytkownika testowego UserEcho</span><span class="sxs-lookup"><span data-stu-id="8e8ff-213">Creating a UserEcho test user</span></span>

<span data-ttu-id="8e8ff-214">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w UserEcho.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-214">hello objective of this section is toocreate a user called Britta Simon in UserEcho.</span></span>

<span data-ttu-id="8e8ff-215">**toocreate użytkownika o nazwie Simona Britta w UserEcho, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8e8ff-215">**toocreate a user called Britta Simon in UserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e8ff-216">Logowania jednokrotnego tooyour UserEcho witryna firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-216">Sign-on tooyour UserEcho company site as an administrator.</span></span>

2. <span data-ttu-id="8e8ff-217">Witaj pasku narzędzi u góry hello, kliknij przycisk z menu hello tooexpand nazwa użytkownika, a następnie kliknij **Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-217">In hello toolbar on hello top, click your user name tooexpand hello menu, and then click **Setup**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png)

3. <span data-ttu-id="8e8ff-219">Kliknij przycisk **użytkowników**, tooexpand hello **użytkowników** sekcji.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-219">Click **Users**, tooexpand hello **Users** section.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_10.png)

4. <span data-ttu-id="8e8ff-221">Kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-221">Click **Users**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_11.png)

5. <span data-ttu-id="8e8ff-223">Kliknij przycisk **zaprosić nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-223">Click **Invite a new user**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_12.png)

6. <span data-ttu-id="8e8ff-225">Na powitania **zaprosić nowego użytkownika** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8e8ff-225">On hello **Invite a new user** dialog, perform hello following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_13.png)

    <span data-ttu-id="8e8ff-227">a.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-227">a.</span></span> <span data-ttu-id="8e8ff-228">W hello **nazwa** pole tekstowe, nazwa typu hello użytkownika, takich jak Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-228">In hello **Name** textbox, type name of hello user like Britta Simon.</span></span>
    
    <span data-ttu-id="8e8ff-229">b.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-229">b.</span></span>  <span data-ttu-id="8e8ff-230">W hello **E-mail** pole tekstowe, typ hello adres e-mail użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-230">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="8e8ff-231">c.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-231">c.</span></span> <span data-ttu-id="8e8ff-232">Kliknij przycisk **zaprosić**.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-232">Click **Invite**.</span></span>

<span data-ttu-id="8e8ff-233">TooBritta, co umożliwia jej toostart przy użyciu UserEcho jest wysłać zaproszenia.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-233">An invitation is sent tooBritta, which enables her toostart using UserEcho.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8e8ff-234">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e8ff-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8e8ff-235">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooUserEcho.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUserEcho.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="8e8ff-237">**tooassign tooUserEcho Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="8e8ff-237">**tooassign Britta Simon tooUserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e8ff-238">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="8e8ff-240">Z listy aplikacji hello wybierz **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-240">In hello applications list, select **UserEcho**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_app.png) 

3. <span data-ttu-id="8e8ff-242">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="8e8ff-244">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-244">Click **Add** button.</span></span> <span data-ttu-id="8e8ff-245">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="8e8ff-247">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8e8ff-248">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8e8ff-249">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8e8ff-250">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8e8ff-250">Testing single sign-on</span></span>

<span data-ttu-id="8e8ff-251">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-251">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="8e8ff-252">Po kliknięciu kafelka UserEcho hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour UserEcho aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8e8ff-252">When you click hello UserEcho tile in hello Access Panel, you should get automatically signed-on tooyour UserEcho application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8e8ff-253">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8e8ff-253">Additional resources</span></span>

* [<span data-ttu-id="8e8ff-254">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8e8ff-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8e8ff-255">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8e8ff-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_203.png

