---
title: 'Samouczek: Integracji Azure Active Directory z Ariba | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Ariba."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 45a8364c-55d1-4dc7-b079-9eb2a701842d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: a1b17129c1298b59c155a0890e41e41ff9544a24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ariba"></a><span data-ttu-id="49b48-103">Samouczek: Integracji Azure Active Directory z Ariba</span><span class="sxs-lookup"><span data-stu-id="49b48-103">Tutorial: Azure Active Directory integration with Ariba</span></span>

<span data-ttu-id="49b48-104">Z tego samouczka, dowiesz się, jak toointegrate Ariba z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="49b48-104">In this tutorial, you learn how toointegrate Ariba with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="49b48-105">Integracja z usługą Azure AD Ariba zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="49b48-105">Integrating Ariba with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="49b48-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooAriba</span><span class="sxs-lookup"><span data-stu-id="49b48-106">You can control in Azure AD who has access tooAriba</span></span>
- <span data-ttu-id="49b48-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAriba (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="49b48-107">You can enable your users tooautomatically get signed-on tooAriba (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="49b48-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="49b48-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="49b48-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="49b48-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49b48-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="49b48-110">Prerequisites</span></span>

<span data-ttu-id="49b48-111">tooconfigure integracji z usługą Azure AD z Ariba należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="49b48-111">tooconfigure Azure AD integration with Ariba, you need hello following items:</span></span>

- <span data-ttu-id="49b48-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="49b48-112">An Azure AD subscription</span></span>
- <span data-ttu-id="49b48-113">Ariba jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="49b48-113">An Ariba single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="49b48-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="49b48-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="49b48-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="49b48-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="49b48-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="49b48-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="49b48-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="49b48-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="49b48-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="49b48-118">Scenario description</span></span>
<span data-ttu-id="49b48-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="49b48-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="49b48-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="49b48-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="49b48-121">Dodawanie Ariba z galerii hello</span><span class="sxs-lookup"><span data-stu-id="49b48-121">Adding Ariba from hello gallery</span></span>
2. <span data-ttu-id="49b48-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="49b48-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ariba-from-hello-gallery"></a><span data-ttu-id="49b48-123">Dodawanie Ariba z galerii hello</span><span class="sxs-lookup"><span data-stu-id="49b48-123">Adding Ariba from hello gallery</span></span>
<span data-ttu-id="49b48-124">tooconfigure hello integracji Ariba do usługi Azure AD, należy tooadd Ariba z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="49b48-124">tooconfigure hello integration of Ariba into Azure AD, you need tooadd Ariba from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="49b48-125">**tooadd Ariba z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="49b48-125">**tooadd Ariba from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="49b48-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="49b48-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="49b48-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="49b48-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="49b48-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="49b48-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="49b48-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="49b48-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="49b48-133">W polu wyszukiwania hello wpisz **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="49b48-133">In hello search box, type **Ariba**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_search.png)

5. <span data-ttu-id="49b48-135">W panelu wyników hello zaznacz **Ariba**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="49b48-135">In hello results panel, select **Ariba**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="49b48-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="49b48-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="49b48-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Ariba oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="49b48-138">In this section, you configure and test Azure AD single sign-on with Ariba based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="49b48-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Ariba jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49b48-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Ariba is tooa user in Azure AD.</span></span> <span data-ttu-id="49b48-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Ariba musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="49b48-140">In other words, a link relationship between an Azure AD user and hello related user in Ariba needs toobe established.</span></span>

<span data-ttu-id="49b48-141">W Ariba, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="49b48-141">In Ariba, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="49b48-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Ariba, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="49b48-142">tooconfigure and test Azure AD single sign-on with Ariba, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="49b48-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="49b48-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="49b48-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="49b48-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="49b48-145">**[Tworzenie użytkownika testowego Ariba](#creating-an-ariba-test-user)**  -toohave odpowiednikiem Simona Britta w Ariba, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="49b48-145">**[Creating an Ariba test user](#creating-an-ariba-test-user)** - toohave a counterpart of Britta Simon in Ariba that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="49b48-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="49b48-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="49b48-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="49b48-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="49b48-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="49b48-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="49b48-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Ariba.</span><span class="sxs-lookup"><span data-stu-id="49b48-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Ariba application.</span></span>

<span data-ttu-id="49b48-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Ariba, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="49b48-150">**tooconfigure Azure AD single sign-on with Ariba, perform hello following steps:**</span></span>

1. <span data-ttu-id="49b48-151">W portalu Azure na powitania hello **Ariba** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="49b48-151">In hello Azure portal, on hello **Ariba** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="49b48-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="49b48-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_samlbase.png)

3. <span data-ttu-id="49b48-155">Na powitania **Ariba domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="49b48-155">On hello **Ariba Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_url.png)

    <span data-ttu-id="49b48-157">a.</span><span class="sxs-lookup"><span data-stu-id="49b48-157">a.</span></span> <span data-ttu-id="49b48-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca: `https://<subdomain>.sourcing.ariba.com` lub`https://<subdomain>.supplier.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="49b48-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sourcing.ariba.com` or `https://<subdomain>.supplier.ariba.com`</span></span>

    <span data-ttu-id="49b48-159">b.</span><span class="sxs-lookup"><span data-stu-id="49b48-159">b.</span></span> <span data-ttu-id="49b48-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`http://<subdomain>.procurement-2.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="49b48-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://<subdomain>.procurement-2.ariba.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="49b48-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="49b48-161">These values are not real.</span></span> <span data-ttu-id="49b48-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="49b48-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="49b48-163">W tym miejscu zalecamy możesz toouse hello unikatową wartość ciągu w hello identyfikator.</span><span class="sxs-lookup"><span data-stu-id="49b48-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="49b48-164">Skontaktuj się z zespołem pomocy technicznej klienta Ariba na **1-866-218-2155** tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="49b48-164">Contact Ariba Client support team at **1-866-218-2155** tooget these values.</span></span> 
 

4. <span data-ttu-id="49b48-165">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="49b48-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate  file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_certificate.png) 

5. <span data-ttu-id="49b48-167">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="49b48-167">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ariba-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="49b48-169">tooget logowania jednokrotnego skonfigurować aplikację tak, aby wywołać Ariba zespołem pomocy technicznej dla **1-866-218-2155** i będzie można dodatkowo assist na sposób pobierania ich hello tooprovide **certyfikatu (Base64)** pliku.</span><span class="sxs-lookup"><span data-stu-id="49b48-169">tooget SSO configured for your application, call Ariba support team on **1-866-218-2155** and they'll assist you further on how tooprovide them hello downloaded **Certificate (Base64)** file.</span></span>  
 
> [!TIP]
> <span data-ttu-id="49b48-170">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="49b48-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="49b48-171">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="49b48-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="49b48-172">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="49b48-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="49b48-173">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="49b48-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="49b48-174">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="49b48-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="49b48-176">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="49b48-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="49b48-177">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="49b48-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="49b48-179">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="49b48-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="49b48-181">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="49b48-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="49b48-183">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="49b48-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="49b48-185">a.</span><span class="sxs-lookup"><span data-stu-id="49b48-185">a.</span></span> <span data-ttu-id="49b48-186">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="49b48-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="49b48-187">b.</span><span class="sxs-lookup"><span data-stu-id="49b48-187">b.</span></span> <span data-ttu-id="49b48-188">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="49b48-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="49b48-189">c.</span><span class="sxs-lookup"><span data-stu-id="49b48-189">c.</span></span> <span data-ttu-id="49b48-190">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="49b48-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="49b48-191">d.</span><span class="sxs-lookup"><span data-stu-id="49b48-191">d.</span></span> <span data-ttu-id="49b48-192">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="49b48-192">Click **Create**.</span></span>
 
### <a name="creating-an-ariba-test-user"></a><span data-ttu-id="49b48-193">Tworzenie użytkownika testowego Ariba</span><span class="sxs-lookup"><span data-stu-id="49b48-193">Creating an Ariba test user</span></span>

<span data-ttu-id="49b48-194">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Ariba.</span><span class="sxs-lookup"><span data-stu-id="49b48-194">hello objective of this section is toocreate a user called Britta Simon in Ariba.</span></span> <span data-ttu-id="49b48-195">Współpraca z zespołem pomocy technicznej Ariba na **1-866-218-2155** tooadd hello użytkowników w hello Ariba systemu.</span><span class="sxs-lookup"><span data-stu-id="49b48-195">Work with Ariba support team at **1-866-218-2155** tooadd hello users in hello Ariba system.</span></span> 

 >[!NOTE]
 ><span data-ttu-id="49b48-196">Jeśli potrzebujesz ręcznie toocreate użytkownika, należy toocontact hello Ariba z pomocą techniczną w **1-866-218-2155**.</span><span class="sxs-lookup"><span data-stu-id="49b48-196">If you need toocreate a user manually, you need toocontact hello Ariba support team at **1-866-218-2155**.</span></span>
 >  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="49b48-197">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="49b48-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="49b48-198">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooAriba.</span><span class="sxs-lookup"><span data-stu-id="49b48-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAriba.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="49b48-200">**tooassign tooAriba Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="49b48-200">**tooassign Britta Simon tooAriba, perform hello following steps:**</span></span>

1. <span data-ttu-id="49b48-201">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="49b48-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="49b48-203">Z listy aplikacji hello wybierz **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="49b48-203">In hello applications list, select **Ariba**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_app.png) 

3. <span data-ttu-id="49b48-205">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="49b48-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="49b48-207">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="49b48-207">Click **Add** button.</span></span> <span data-ttu-id="49b48-208">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="49b48-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="49b48-210">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="49b48-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="49b48-211">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="49b48-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="49b48-212">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="49b48-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="49b48-213">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="49b48-213">Testing single sign-on</span></span>
<span data-ttu-id="49b48-214">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="49b48-214">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="49b48-215">Po kliknięciu kafelka Ariba hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Ariba aplikacji.</span><span class="sxs-lookup"><span data-stu-id="49b48-215">When you click hello Ariba tile in hello Access Panel, you should get automatically signed-on tooyour Ariba application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="49b48-216">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="49b48-216">Additional resources</span></span>

* [<span data-ttu-id="49b48-217">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="49b48-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="49b48-218">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="49b48-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_203.png

