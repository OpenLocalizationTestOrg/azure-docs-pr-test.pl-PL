---
title: 'Samouczek: Integracji Azure Active Directory z Marketo | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i usługi Marketo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 87f88cde4f027f99a83c1ab3b318247bb4d658ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a><span data-ttu-id="61167-103">Samouczek: Integracji Azure Active Directory z usługi Marketo</span><span class="sxs-lookup"><span data-stu-id="61167-103">Tutorial: Azure Active Directory integration with Marketo</span></span>

<span data-ttu-id="61167-104">Z tego samouczka, dowiesz się, jak toointegrate Marketo w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="61167-104">In this tutorial, you learn how toointegrate Marketo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="61167-105">Integrowanie usługi Marketo w usłudze Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="61167-105">Integrating Marketo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="61167-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooMarketo</span><span class="sxs-lookup"><span data-stu-id="61167-106">You can control in Azure AD who has access tooMarketo</span></span>
- <span data-ttu-id="61167-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooMarketo (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="61167-107">You can enable your users tooautomatically get signed-on tooMarketo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="61167-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="61167-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="61167-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="61167-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61167-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="61167-110">Prerequisites</span></span>

<span data-ttu-id="61167-111">tooconfigure integracji usługi Azure AD z Marketo należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="61167-111">tooconfigure Azure AD integration with Marketo, you need hello following items:</span></span>

- <span data-ttu-id="61167-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="61167-112">An Azure AD subscription</span></span>
- <span data-ttu-id="61167-113">Usługi Marketo jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="61167-113">A Marketo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="61167-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="61167-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="61167-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="61167-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="61167-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="61167-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="61167-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="61167-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="61167-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="61167-118">Scenario description</span></span>
<span data-ttu-id="61167-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="61167-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="61167-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="61167-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="61167-121">Dodawanie usługi Marketo z galerii hello</span><span class="sxs-lookup"><span data-stu-id="61167-121">Adding Marketo from hello gallery</span></span>
2. <span data-ttu-id="61167-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="61167-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-marketo-from-hello-gallery"></a><span data-ttu-id="61167-123">Dodawanie usługi Marketo z galerii hello</span><span class="sxs-lookup"><span data-stu-id="61167-123">Adding Marketo from hello gallery</span></span>
<span data-ttu-id="61167-124">tooconfigure hello integracji usługi Marketo w usłudze Azure Active Directory, należy tooadd Marketo od hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="61167-124">tooconfigure hello integration of Marketo into Azure AD, you need tooadd Marketo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="61167-125">**tooadd Marketo z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="61167-125">**tooadd Marketo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="61167-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="61167-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="61167-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="61167-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="61167-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="61167-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="61167-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="61167-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="61167-133">W polu wyszukiwania hello wpisz **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="61167-133">In hello search box, type **Marketo**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. <span data-ttu-id="61167-135">W panelu wyników hello, wybierz **Marketo**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="61167-135">In hello results panel, select **Marketo**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="61167-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="61167-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="61167-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługi Marketo oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="61167-138">In this section, you configure and test Azure AD single sign-on with Marketo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="61167-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Marketo jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61167-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Marketo is tooa user in Azure AD.</span></span> <span data-ttu-id="61167-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Marketo musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="61167-140">In other words, a link relationship between an Azure AD user and hello related user in Marketo needs toobe established.</span></span>

<span data-ttu-id="61167-141">W Marketo, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="61167-141">In Marketo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="61167-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Marketo, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="61167-142">tooconfigure and test Azure AD single sign-on with Marketo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="61167-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="61167-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="61167-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="61167-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="61167-145">**[Tworzenie użytkownika testowego Marketo](#creating-a-marketo-test-user)**  -toohave odpowiednikiem Simona Britta w Marketo, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="61167-145">**[Creating a Marketo test user](#creating-a-marketo-test-user)** - toohave a counterpart of Britta Simon in Marketo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="61167-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="61167-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="61167-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="61167-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="61167-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="61167-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="61167-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji usługi Marketo.</span><span class="sxs-lookup"><span data-stu-id="61167-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Marketo application.</span></span>

<span data-ttu-id="61167-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Marketo, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="61167-150">**tooconfigure Azure AD single sign-on with Marketo, perform hello following steps:**</span></span>

1. <span data-ttu-id="61167-151">W portalu Azure na powitania hello **Marketo** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="61167-151">In hello Azure portal, on hello **Marketo** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="61167-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="61167-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. <span data-ttu-id="61167-155">Na powitania **Marketo domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="61167-155">On hello **Marketo Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    <span data-ttu-id="61167-157">a.</span><span class="sxs-lookup"><span data-stu-id="61167-157">a.</span></span> <span data-ttu-id="61167-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://saml.marketo.com/sp`</span><span class="sxs-lookup"><span data-stu-id="61167-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://saml.marketo.com/sp`</span></span>

    <span data-ttu-id="61167-159">b.</span><span class="sxs-lookup"><span data-stu-id="61167-159">b.</span></span> <span data-ttu-id="61167-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://login.marketo.com/saml/assertion/\<munchkinid\>`</span><span class="sxs-lookup"><span data-stu-id="61167-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="61167-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="61167-161">These values are not real.</span></span> <span data-ttu-id="61167-162">Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="61167-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="61167-163">Skontaktuj się z [zespołem pomocy technicznej usługi Marketo](http://investors.marketo.com/contactus.cfm) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="61167-163">Contact [Marketo support team](http://investors.marketo.com/contactus.cfm) tooget these values.</span></span>
 
4. <span data-ttu-id="61167-164">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="61167-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. <span data-ttu-id="61167-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="61167-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="61167-168">Na powitania **konfiguracji usługi Marketo** kliknij **Konfiguruj usługi Marketo** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="61167-168">On hello **Marketo Configuration** section, click **Configure Marketo** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="61167-169">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="61167-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. <span data-ttu-id="61167-171">tooget Munchkin identyfikator aplikacji, zaloguj się przy użyciu poświadczeń administratora tooMarketo i wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="61167-171">tooget Munchkin Id of your application, log in tooMarketo using admin credentials and perform following actions:</span></span>
   
    <span data-ttu-id="61167-172">a.</span><span class="sxs-lookup"><span data-stu-id="61167-172">a.</span></span> <span data-ttu-id="61167-173">Zaloguj się w aplikacji tooMarketo przy użyciu poświadczeń administratora.</span><span class="sxs-lookup"><span data-stu-id="61167-173">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="61167-174">b.</span><span class="sxs-lookup"><span data-stu-id="61167-174">b.</span></span> <span data-ttu-id="61167-175">Kliknij przycisk hello **Admin** przycisk w okienku nawigacji w górnym hello.</span><span class="sxs-lookup"><span data-stu-id="61167-175">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="61167-177">c.</span><span class="sxs-lookup"><span data-stu-id="61167-177">c.</span></span> <span data-ttu-id="61167-178">Przejdź do menu integracji toohello, a następnie kliknij przycisk hello **łącze Munchkin**.</span><span class="sxs-lookup"><span data-stu-id="61167-178">Navigate toohello Integration menu and click hello **Munchkin link**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    <span data-ttu-id="61167-180">d.</span><span class="sxs-lookup"><span data-stu-id="61167-180">d.</span></span> <span data-ttu-id="61167-181">Skopiuj identyfikator Munchkin wyświetlany na ekranie powitania hello i wykonaj adres URL odpowiedzi, w Kreatorze konfiguracji hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61167-181">Copy hello Munchkin Id shown on hello screen and complete your Reply URL in hello Azure AD configuration wizard.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. <span data-ttu-id="61167-183">Witaj tooconfigure logowania jednokrotnego w aplikacji hello wykonaj hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="61167-183">tooconfigure hello SSO in hello application, follow hello below steps:</span></span>
   
    <span data-ttu-id="61167-184">a.</span><span class="sxs-lookup"><span data-stu-id="61167-184">a.</span></span> <span data-ttu-id="61167-185">Zaloguj się w aplikacji tooMarketo przy użyciu poświadczeń administratora.</span><span class="sxs-lookup"><span data-stu-id="61167-185">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="61167-186">b.</span><span class="sxs-lookup"><span data-stu-id="61167-186">b.</span></span> <span data-ttu-id="61167-187">Kliknij przycisk hello **Admin** przycisk w okienku nawigacji w górnym hello.</span><span class="sxs-lookup"><span data-stu-id="61167-187">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="61167-189">c.</span><span class="sxs-lookup"><span data-stu-id="61167-189">c.</span></span> <span data-ttu-id="61167-190">Przejdź do menu integracji toohello i kliknij przycisk **rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="61167-190">Navigate toohello Integration menu and click **Single Sign On**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    <span data-ttu-id="61167-192">d.</span><span class="sxs-lookup"><span data-stu-id="61167-192">d.</span></span> <span data-ttu-id="61167-193">tooenable hello SAML ustawienia, kliknij przycisk **Edytuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="61167-193">tooenable hello SAML Settings, click **Edit** button.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    <span data-ttu-id="61167-195">e.</span><span class="sxs-lookup"><span data-stu-id="61167-195">e.</span></span> <span data-ttu-id="61167-196">**Włączone** ustawienia logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="61167-196">**Enabled** Single Sign-On settings.</span></span>
   
    <span data-ttu-id="61167-197">f.</span><span class="sxs-lookup"><span data-stu-id="61167-197">f.</span></span> <span data-ttu-id="61167-198">Wklej hello **identyfikator jednostki SAML**, w hello **identyfikator wystawcy** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="61167-198">Paste hello **SAML Entity ID**, in hello **Issuer ID** textbox.</span></span>
   
    <span data-ttu-id="61167-199">g.</span><span class="sxs-lookup"><span data-stu-id="61167-199">g.</span></span> <span data-ttu-id="61167-200">W hello **identyfikator jednostki** pole tekstowe, wprowadź adres URL hello jako `http://saml.marketo.com/sp`.</span><span class="sxs-lookup"><span data-stu-id="61167-200">In hello **Entity ID** textbox, enter hello URL as `http://saml.marketo.com/sp`.</span></span>
   
    <span data-ttu-id="61167-201">h.</span><span class="sxs-lookup"><span data-stu-id="61167-201">h.</span></span> <span data-ttu-id="61167-202">Wybierz hello lokalizacji identyfikator użytkownika jako **element nazwa identyfikatora**.</span><span class="sxs-lookup"><span data-stu-id="61167-202">Select hello User ID Location as **Name Identifier element**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > <span data-ttu-id="61167-204">Jeśli Twojego identyfikatora użytkownika nie ma wartości głównej nazwy użytkownika, a następnie zmień wartość hello hello atrybutu karcie.</span><span class="sxs-lookup"><span data-stu-id="61167-204">If your User Identifier is not UPN value then change hello value in hello Attribute tab.</span></span>
   
    <span data-ttu-id="61167-205">i.</span><span class="sxs-lookup"><span data-stu-id="61167-205">i.</span></span> <span data-ttu-id="61167-206">Przekaż certyfikat hello, który został pobrany z Kreatora konfiguracji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61167-206">Upload hello certificate, which you have downloaded from Azure AD configuration wizard.</span></span> <span data-ttu-id="61167-207">**Zapisz** hello ustawienia.</span><span class="sxs-lookup"><span data-stu-id="61167-207">**Save** hello settings.</span></span>
   
    <span data-ttu-id="61167-208">j.</span><span class="sxs-lookup"><span data-stu-id="61167-208">j.</span></span> <span data-ttu-id="61167-209">Edytowanie ustawień stron przekierowania hello.</span><span class="sxs-lookup"><span data-stu-id="61167-209">Edit hello Redirect Pages settings.</span></span>
   
    <span data-ttu-id="61167-210">k.</span><span class="sxs-lookup"><span data-stu-id="61167-210">k.</span></span> <span data-ttu-id="61167-211">Wklej hello **SAML pojedynczy znak na adres URL usługi** w hello **adres URL logowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="61167-211">Paste hello **SAML Single Sign-On Service URL** in hello **Login URL** textbox.</span></span>
   
    <span data-ttu-id="61167-212">l.</span><span class="sxs-lookup"><span data-stu-id="61167-212">l.</span></span> <span data-ttu-id="61167-213">Wklej hello **Sign-Out URL** w hello **adresu URL wylogowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="61167-213">Paste hello **Sign-Out URL** in hello **Logout URL** textbox.</span></span>
   
    <span data-ttu-id="61167-214">m.</span><span class="sxs-lookup"><span data-stu-id="61167-214">m.</span></span> <span data-ttu-id="61167-215">W hello **adres URL błędu**, kopia programu **adresu URL wystąpienia usługi Marketo** i kliknij przycisk **zapisać** przycisk toosave ustawienia.</span><span class="sxs-lookup"><span data-stu-id="61167-215">In hello **Error URL**, copy your **Marketo instance URL** and click **Save** button toosave settings.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. <span data-ttu-id="61167-217">tooenable hello logowania jednokrotnego dla użytkowników, pełną hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="61167-217">tooenable hello SSO for users, complete hello following actions:</span></span>
   
    <span data-ttu-id="61167-218">a.</span><span class="sxs-lookup"><span data-stu-id="61167-218">a.</span></span> <span data-ttu-id="61167-219">Zaloguj się w aplikacji tooMarketo przy użyciu poświadczeń administratora.</span><span class="sxs-lookup"><span data-stu-id="61167-219">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="61167-220">b.</span><span class="sxs-lookup"><span data-stu-id="61167-220">b.</span></span> <span data-ttu-id="61167-221">Kliknij przycisk hello **Admin** przycisk w okienku nawigacji w górnym hello.</span><span class="sxs-lookup"><span data-stu-id="61167-221">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="61167-223">c.</span><span class="sxs-lookup"><span data-stu-id="61167-223">c.</span></span> <span data-ttu-id="61167-224">Przejdź toohello **zabezpieczeń** menu i kliknij przycisk **ustawienia logowania**.</span><span class="sxs-lookup"><span data-stu-id="61167-224">Navigate toohello **Security** menu and click **Login Settings**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    <span data-ttu-id="61167-226">d.</span><span class="sxs-lookup"><span data-stu-id="61167-226">d.</span></span> <span data-ttu-id="61167-227">Sprawdź hello **wymagają rejestracji Jednokrotnej** opcji i **zapisać** hello ustawienia.</span><span class="sxs-lookup"><span data-stu-id="61167-227">Check hello **Require SSO** option and **Save** hello settings.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> <span data-ttu-id="61167-229">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="61167-229">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="61167-230">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="61167-230">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="61167-231">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="61167-231">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="61167-232">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="61167-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="61167-233">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="61167-233">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="61167-235">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="61167-235">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="61167-236">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="61167-236">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="61167-238">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="61167-238">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="61167-240">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="61167-240">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="61167-242">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="61167-242">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="61167-244">a.</span><span class="sxs-lookup"><span data-stu-id="61167-244">a.</span></span> <span data-ttu-id="61167-245">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="61167-245">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="61167-246">b.</span><span class="sxs-lookup"><span data-stu-id="61167-246">b.</span></span> <span data-ttu-id="61167-247">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="61167-247">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="61167-248">c.</span><span class="sxs-lookup"><span data-stu-id="61167-248">c.</span></span> <span data-ttu-id="61167-249">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="61167-249">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="61167-250">d.</span><span class="sxs-lookup"><span data-stu-id="61167-250">d.</span></span> <span data-ttu-id="61167-251">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="61167-251">Click **Create**.</span></span>
 
### <a name="creating-a-marketo-test-user"></a><span data-ttu-id="61167-252">Tworzenie użytkownika testowego usługi Marketo</span><span class="sxs-lookup"><span data-stu-id="61167-252">Creating a Marketo test user</span></span>

<span data-ttu-id="61167-253">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Marketo.</span><span class="sxs-lookup"><span data-stu-id="61167-253">In this section, you create a user called Britta Simon in Marketo.</span></span> <span data-ttu-id="61167-254">Wykonaj te kroki toocreate użytkownika na platformie Marketo.</span><span class="sxs-lookup"><span data-stu-id="61167-254">follow these steps toocreate a user in Marketo platform.</span></span>

1. <span data-ttu-id="61167-255">Zaloguj się w aplikacji tooMarketo przy użyciu poświadczeń administratora.</span><span class="sxs-lookup"><span data-stu-id="61167-255">Log in tooMarketo app using admin credentials.</span></span>

2. <span data-ttu-id="61167-256">Kliknij przycisk hello **Admin** przycisk w okienku nawigacji w górnym hello.</span><span class="sxs-lookup"><span data-stu-id="61167-256">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. <span data-ttu-id="61167-258">Przejdź toohello **zabezpieczeń** menu i kliknij przycisk **użytkownicy i role**</span><span class="sxs-lookup"><span data-stu-id="61167-258">Navigate toohello **Security** menu and click **Users & Roles**</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. <span data-ttu-id="61167-260">Kliknij przycisk hello **zaprosić nowego użytkownika** link na karcie Użytkownicy hello</span><span class="sxs-lookup"><span data-stu-id="61167-260">Click hello **Invite New User** link on hello Users tab</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. <span data-ttu-id="61167-262">W hello zaprosić nowego użytkownika Kreatora wypełnienia hello następujących informacji</span><span class="sxs-lookup"><span data-stu-id="61167-262">In hello Invite New User wizard fill hello following information</span></span>
   
    <span data-ttu-id="61167-263">a.</span><span class="sxs-lookup"><span data-stu-id="61167-263">a.</span></span> <span data-ttu-id="61167-264">Wprowadź nazwę użytkownika hello **E-mail** adres w polu tekstowym hello</span><span class="sxs-lookup"><span data-stu-id="61167-264">Enter hello user **Email** address in hello textbox</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    <span data-ttu-id="61167-266">b.</span><span class="sxs-lookup"><span data-stu-id="61167-266">b.</span></span> <span data-ttu-id="61167-267">Wprowadź hello **imię** w polu tekstowym hello</span><span class="sxs-lookup"><span data-stu-id="61167-267">Enter hello **First Name** in hello textbox</span></span>
   
    <span data-ttu-id="61167-268">c.</span><span class="sxs-lookup"><span data-stu-id="61167-268">c.</span></span> <span data-ttu-id="61167-269">Wprowadź hello **nazwisko** w polu tekstowym hello</span><span class="sxs-lookup"><span data-stu-id="61167-269">Enter hello **Last Name**  in hello textbox</span></span>
   
    <span data-ttu-id="61167-270">d.</span><span class="sxs-lookup"><span data-stu-id="61167-270">d.</span></span> <span data-ttu-id="61167-271">Kliknij przycisk **Dalej**</span><span class="sxs-lookup"><span data-stu-id="61167-271">Click **Next**</span></span>

6. <span data-ttu-id="61167-272">W hello **uprawnienia** kartę, zaznacz hello **roli użytkownika** i kliknij przycisk **dalej**</span><span class="sxs-lookup"><span data-stu-id="61167-272">In hello **Permissions** tab, select hello **userRoles** and click **Next**</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. <span data-ttu-id="61167-274">Kliknij przycisk hello **wysyłania** przycisk toosend hello użytkownika zaproszenia</span><span class="sxs-lookup"><span data-stu-id="61167-274">Click hello **Send** button toosend hello user invitation</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. <span data-ttu-id="61167-276">Użytkownik otrzymuje powiadomienie e-mail hello i hello tooclick łącze i zmień hello hasło tooactivate hello konta.</span><span class="sxs-lookup"><span data-stu-id="61167-276">User receives hello email notification and has tooclick hello link and change hello password tooactivate hello account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="61167-277">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="61167-277">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="61167-278">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooMarketo.</span><span class="sxs-lookup"><span data-stu-id="61167-278">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMarketo.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="61167-280">**tooassign tooMarketo Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="61167-280">**tooassign Britta Simon tooMarketo, perform hello following steps:**</span></span>

1. <span data-ttu-id="61167-281">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="61167-281">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="61167-283">Z listy aplikacji hello wybierz **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="61167-283">In hello applications list, select **Marketo**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. <span data-ttu-id="61167-285">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="61167-285">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="61167-287">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="61167-287">Click **Add** button.</span></span> <span data-ttu-id="61167-288">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="61167-288">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="61167-290">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="61167-290">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="61167-291">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="61167-291">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="61167-292">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="61167-292">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="61167-293">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="61167-293">Testing single sign-on</span></span>

<span data-ttu-id="61167-294">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="61167-294">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="61167-295">Po kliknięciu kafelka Marketo hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Marketo aplikacji.</span><span class="sxs-lookup"><span data-stu-id="61167-295">When you click hello Marketo tile in hello Access Panel, you should get automatically signed-on tooyour Marketo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="61167-296">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="61167-296">Additional resources</span></span>

* [<span data-ttu-id="61167-297">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="61167-297">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="61167-298">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="61167-298">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

