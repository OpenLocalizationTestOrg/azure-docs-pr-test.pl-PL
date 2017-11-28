---
title: 'Samouczek: Integracji Azure Active Directory z Kiteworks | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Kiteworks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7984aaf-ab1f-4a85-9646-a9523f5275d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 406417dd7f58cc3f1fa0d9e86b5cad0c1d7be750
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kiteworks"></a><span data-ttu-id="c6321-103">Samouczek: Integracji Azure Active Directory z Kiteworks</span><span class="sxs-lookup"><span data-stu-id="c6321-103">Tutorial: Azure Active Directory integration with Kiteworks</span></span>

<span data-ttu-id="c6321-104">Z tego samouczka, dowiesz się, jak toointegrate Kiteworks w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c6321-104">In this tutorial, you learn how toointegrate Kiteworks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c6321-105">Integracja z usługą Azure AD Kiteworks zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="c6321-105">Integrating Kiteworks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c6321-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooKiteworks</span><span class="sxs-lookup"><span data-stu-id="c6321-106">You can control in Azure AD who has access tooKiteworks</span></span>
- <span data-ttu-id="c6321-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooKiteworks (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6321-107">You can enable your users tooautomatically get signed-on tooKiteworks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c6321-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c6321-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c6321-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c6321-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6321-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c6321-110">Prerequisites</span></span>

<span data-ttu-id="c6321-111">tooconfigure integracji z usługą Azure AD z Kiteworks należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c6321-111">tooconfigure Azure AD integration with Kiteworks, you need hello following items:</span></span>

- <span data-ttu-id="c6321-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6321-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c6321-113">Kiteworks logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c6321-113">A Kiteworks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c6321-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c6321-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c6321-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="c6321-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c6321-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c6321-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c6321-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c6321-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c6321-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="c6321-118">Scenario description</span></span>
<span data-ttu-id="c6321-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="c6321-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c6321-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="c6321-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c6321-121">Dodawanie Kiteworks z galerii hello</span><span class="sxs-lookup"><span data-stu-id="c6321-121">Adding Kiteworks from hello gallery</span></span>
2. <span data-ttu-id="c6321-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c6321-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kiteworks-from-hello-gallery"></a><span data-ttu-id="c6321-123">Dodawanie Kiteworks z galerii hello</span><span class="sxs-lookup"><span data-stu-id="c6321-123">Adding Kiteworks from hello gallery</span></span>
<span data-ttu-id="c6321-124">tooconfigure hello integracji Kiteworks do usługi Azure AD, należy tooadd Kiteworks z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="c6321-124">tooconfigure hello integration of Kiteworks into Azure AD, you need tooadd Kiteworks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c6321-125">**tooadd Kiteworks z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c6321-125">**tooadd Kiteworks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6321-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c6321-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="c6321-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="c6321-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c6321-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c6321-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="c6321-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c6321-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="c6321-133">W polu wyszukiwania hello wpisz **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="c6321-133">In hello search box, type **Kiteworks**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_search.png)

5. <span data-ttu-id="c6321-135">W panelu wyników hello zaznacz **Kiteworks**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="c6321-135">In hello results panel, select **Kiteworks**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c6321-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c6321-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c6321-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Kiteworks w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="c6321-138">In this section, you configure and test Azure AD single sign-on with Kiteworks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c6321-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Kiteworks jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6321-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kiteworks is tooa user in Azure AD.</span></span> <span data-ttu-id="c6321-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Kiteworks musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="c6321-140">In other words, a link relationship between an Azure AD user and hello related user in Kiteworks needs toobe established.</span></span>

<span data-ttu-id="c6321-141">W Kiteworks, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="c6321-141">In Kiteworks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c6321-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Kiteworks, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="c6321-142">tooconfigure and test Azure AD single sign-on with Kiteworks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c6321-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="c6321-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c6321-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c6321-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c6321-145">**[Tworzenie użytkownika testowego Kiteworks](#creating-a-kiteworks-test-user)**  -toohave odpowiednikiem Simona Britta w Kiteworks, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c6321-145">**[Creating a Kiteworks test user](#creating-a-kiteworks-test-user)** - toohave a counterpart of Britta Simon in Kiteworks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c6321-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c6321-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c6321-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="c6321-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c6321-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c6321-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c6321-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="c6321-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kiteworks application.</span></span>

<span data-ttu-id="c6321-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Kiteworks, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c6321-150">**tooconfigure Azure AD single sign-on with Kiteworks, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6321-151">W portalu Azure na powitania hello **Kiteworks** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="c6321-151">In hello Azure portal, on hello **Kiteworks** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="c6321-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c6321-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_samlbase.png)

3. <span data-ttu-id="c6321-155">Na powitania **Kiteworks domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="c6321-155">On hello **Kiteworks Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_url.png)

    <span data-ttu-id="c6321-157">a.</span><span class="sxs-lookup"><span data-stu-id="c6321-157">a.</span></span> <span data-ttu-id="c6321-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.kiteworks.com`</span><span class="sxs-lookup"><span data-stu-id="c6321-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.kiteworks.com`</span></span>

    <span data-ttu-id="c6321-159">b.</span><span class="sxs-lookup"><span data-stu-id="c6321-159">b.</span></span> <span data-ttu-id="c6321-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span><span class="sxs-lookup"><span data-stu-id="c6321-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c6321-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="c6321-161">These values are not real.</span></span> <span data-ttu-id="c6321-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="c6321-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c6321-163">Skontaktuj się z [zespołem pomocy technicznej klienta Kiteworks](http://accellion.com/support) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="c6321-163">Contact [Kiteworks Client support team](http://accellion.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="c6321-164">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c6321-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_certificate.png) 

5. <span data-ttu-id="c6321-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c6321-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kiteworks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c6321-168">Na powitania **konfiguracji Kiteworks** kliknij **skonfigurować Kiteworks** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="c6321-168">On hello **Kiteworks Configuration** section, click **Configure Kiteworks** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c6321-169">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="c6321-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_configure.png) 

7. <span data-ttu-id="c6321-171">Rejestracja tooyour Kiteworks witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="c6321-171">Sign on tooyour Kiteworks company site as an administrator.</span></span>

8. <span data-ttu-id="c6321-172">Witaj pasku narzędzi u góry hello, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="c6321-172">In hello toolbar on hello top, click **Settings**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_06.png) 

9. <span data-ttu-id="c6321-174">W hello **uwierzytelniania i autoryzacji** kliknij **ustawienia logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="c6321-174">In hello **Authentication and Authorization** section, click **SSO Setup**.</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_07.png)
 
10. <span data-ttu-id="c6321-176">Na stronie Ustawienia logowania jednokrotnego hello wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c6321-176">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_09.png)   

    <span data-ttu-id="c6321-178">a.</span><span class="sxs-lookup"><span data-stu-id="c6321-178">a.</span></span> <span data-ttu-id="c6321-179">Wybierz **uwierzytelniania za pomocą logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="c6321-179">Select **Authenticate via SSO**.</span></span>

    <span data-ttu-id="c6321-180">b.</span><span class="sxs-lookup"><span data-stu-id="c6321-180">b.</span></span> <span data-ttu-id="c6321-181">Wybierz **zainicjować AuthnRequest**.</span><span class="sxs-lookup"><span data-stu-id="c6321-181">Select **Initiate AuthnRequest**.</span></span>

    <span data-ttu-id="c6321-182">c.</span><span class="sxs-lookup"><span data-stu-id="c6321-182">c.</span></span> <span data-ttu-id="c6321-183">W hello **identyfikator jednostki IDP** pole tekstowe, Wklej wartość hello **SAML identyfikator jednostki**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c6321-183">In hello **IDP Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="c6321-184">d.</span><span class="sxs-lookup"><span data-stu-id="c6321-184">d.</span></span> <span data-ttu-id="c6321-185">W hello **pojedynczy znak na adres URL usługi** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c6321-185">In hello **Single Sign-On Service URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c6321-186">e.</span><span class="sxs-lookup"><span data-stu-id="c6321-186">e.</span></span> <span data-ttu-id="c6321-187">W hello **pojedynczy adres URL usługi wylogowania** pole tekstowe, Wklej wartość hello **Sign-Out adres URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c6321-187">In hello **Single Logout Service URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c6321-188">f.</span><span class="sxs-lookup"><span data-stu-id="c6321-188">f.</span></span> <span data-ttu-id="c6321-189">Otwórz pobrany certyfikat w Notatniku, hello kopiowania zawartości, a następnie wklej go do hello **certyfikatu klucza publicznego RSA** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="c6321-189">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **RSA Public Key Certificate** textbox.</span></span>
 
    <span data-ttu-id="c6321-190">g.</span><span class="sxs-lookup"><span data-stu-id="c6321-190">g.</span></span> <span data-ttu-id="c6321-191">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="c6321-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c6321-192">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="c6321-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c6321-193">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="c6321-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c6321-194">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c6321-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c6321-195">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6321-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="c6321-196">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="c6321-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="c6321-198">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c6321-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6321-199">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c6321-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c6321-201">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="c6321-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c6321-203">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c6321-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c6321-205">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c6321-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c6321-207">a.</span><span class="sxs-lookup"><span data-stu-id="c6321-207">a.</span></span> <span data-ttu-id="c6321-208">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c6321-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c6321-209">b.</span><span class="sxs-lookup"><span data-stu-id="c6321-209">b.</span></span> <span data-ttu-id="c6321-210">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c6321-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c6321-211">c.</span><span class="sxs-lookup"><span data-stu-id="c6321-211">c.</span></span> <span data-ttu-id="c6321-212">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="c6321-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c6321-213">d.</span><span class="sxs-lookup"><span data-stu-id="c6321-213">d.</span></span> <span data-ttu-id="c6321-214">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c6321-214">Click **Create**.</span></span>
 
### <a name="creating-a-kiteworks-test-user"></a><span data-ttu-id="c6321-215">Tworzenie użytkownika testowego Kiteworks</span><span class="sxs-lookup"><span data-stu-id="c6321-215">Creating a Kiteworks test user</span></span>

<span data-ttu-id="c6321-216">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="c6321-216">hello objective of this section is toocreate a user called Britta Simon in Kiteworks.</span></span>

<span data-ttu-id="c6321-217">Kiteworks obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="c6321-217">Kiteworks supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="c6321-218">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="c6321-218">There is no action item for you in this section.</span></span> <span data-ttu-id="c6321-219">Nowy użytkownik jest tworzona podczas próby tooaccess Kitewors, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="c6321-219">A new user is created during an attempt tooaccess Kitewors if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="c6321-220">Jeśli potrzebujesz ręcznie toocreate użytkownika, należy toocontact hello [Kiteworks obsługuje zespołu](http://accellion.com/support).</span><span class="sxs-lookup"><span data-stu-id="c6321-220">If you need toocreate a user manually, you need toocontact hello [Kiteworks support team](http://accellion.com/support).</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c6321-221">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6321-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c6321-222">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooKiteworks.</span><span class="sxs-lookup"><span data-stu-id="c6321-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKiteworks.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="c6321-224">**tooassign tooKiteworks Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="c6321-224">**tooassign Britta Simon tooKiteworks, perform hello following steps:**</span></span>

1. <span data-ttu-id="c6321-225">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c6321-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="c6321-227">Z listy aplikacji hello wybierz **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="c6321-227">In hello applications list, select **Kiteworks**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_app.png) 

3. <span data-ttu-id="c6321-229">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="c6321-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="c6321-231">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c6321-231">Click **Add** button.</span></span> <span data-ttu-id="c6321-232">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c6321-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="c6321-234">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c6321-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c6321-235">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c6321-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c6321-236">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c6321-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c6321-237">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c6321-237">Testing single sign-on</span></span>

<span data-ttu-id="c6321-238">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="c6321-238">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="c6321-239">Po kliknięciu powitalne Kiteworks kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Kiteworks aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c6321-239">When you click hello Kiteworks tile in hello Access Panel, you should get automatically signed-on tooyour Kiteworks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c6321-240">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c6321-240">Additional resources</span></span>

* [<span data-ttu-id="c6321-241">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c6321-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c6321-242">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c6321-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_203.png

