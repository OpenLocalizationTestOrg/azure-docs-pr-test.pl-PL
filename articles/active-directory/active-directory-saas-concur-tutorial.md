---
title: 'Samouczek: Integracji Azure Active Directory z Concur | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Concur."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1eee0a5d-24fa-4986-9aef-3c543cfe3296
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 1012bf8c6f036306d0ca90689415d5e22e449989
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-concur"></a><span data-ttu-id="955de-103">Samouczek: Integracji Azure Active Directory z Concur</span><span class="sxs-lookup"><span data-stu-id="955de-103">Tutorial: Azure Active Directory integration with Concur</span></span>

<span data-ttu-id="955de-104">Z tego samouczka, dowiesz się, jak toointegrate cząstkowe z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="955de-104">In this tutorial, you learn how toointegrate Concur with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="955de-105">Integracja z usługą Azure AD Concur zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="955de-105">Integrating Concur with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="955de-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooConcur</span><span class="sxs-lookup"><span data-stu-id="955de-106">You can control in Azure AD who has access tooConcur</span></span>
- <span data-ttu-id="955de-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooConcur (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="955de-107">You can enable your users tooautomatically get signed-on tooConcur (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="955de-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="955de-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="955de-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="955de-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="955de-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="955de-110">Prerequisites</span></span>

<span data-ttu-id="955de-111">tooconfigure integracji z usługą Azure AD z Concur należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="955de-111">tooconfigure Azure AD integration with Concur, you need hello following items:</span></span>

- <span data-ttu-id="955de-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="955de-112">An Azure AD subscription</span></span>
- <span data-ttu-id="955de-113">Concur logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="955de-113">A Concur single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="955de-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="955de-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="955de-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="955de-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="955de-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="955de-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="955de-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="955de-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="955de-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="955de-118">Scenario description</span></span>
<span data-ttu-id="955de-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="955de-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="955de-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="955de-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="955de-121">Dodawanie Concur z galerii hello</span><span class="sxs-lookup"><span data-stu-id="955de-121">Adding Concur from hello gallery</span></span>
2. <span data-ttu-id="955de-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="955de-122">Configuring and testing Azure AD single sign-on</span></span>

>[!NOTE]
><span data-ttu-id="955de-123">Konfiguracja Hello subskrypcją Concur federacyjną rejestracją Jednokrotną za pośrednictwem SAML jest osobnym zadaniem musisz skontaktować się z [zespołem pomocy technicznej klienta cząstkowe](https://www.concur.co.in/contact) tooperform.</span><span class="sxs-lookup"><span data-stu-id="955de-123">hello configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) tooperform.</span></span> 

## <a name="adding-concur-from-hello-gallery"></a><span data-ttu-id="955de-124">Dodawanie Concur z galerii hello</span><span class="sxs-lookup"><span data-stu-id="955de-124">Adding Concur from hello gallery</span></span>
<span data-ttu-id="955de-125">tooconfigure hello integracji Concur do usługi Azure AD, należy tooadd Concur z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="955de-125">tooconfigure hello integration of Concur into Azure AD, you need tooadd Concur from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="955de-126">**tooadd Concur z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="955de-126">**tooadd Concur from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="955de-127">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="955de-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="955de-129">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="955de-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="955de-130">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="955de-130">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="955de-132">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="955de-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="955de-134">W polu wyszukiwania hello wpisz **Concur**.</span><span class="sxs-lookup"><span data-stu-id="955de-134">In hello search box, type **Concur**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-concur-tutorial/tutorial_concur_search.png)

5. <span data-ttu-id="955de-136">W panelu wyników hello zaznacz **Concur**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="955de-136">In hello results panel, select **Concur**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-concur-tutorial/tutorial_concur_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="955de-138">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="955de-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="955de-139">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Concur na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="955de-139">In this section, you configure and test Azure AD single sign-on with Concur based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="955de-140">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Concur jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="955de-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Concur is tooa user in Azure AD.</span></span> <span data-ttu-id="955de-141">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Concur musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="955de-141">In other words, a link relationship between an Azure AD user and hello related user in Concur needs toobe established.</span></span>

<span data-ttu-id="955de-142">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Concur.</span><span class="sxs-lookup"><span data-stu-id="955de-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Concur.</span></span>

<span data-ttu-id="955de-143">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Concur, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="955de-143">tooconfigure and test Azure AD single sign-on with Concur, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="955de-144">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="955de-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="955de-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="955de-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="955de-146">**[Tworzenie użytkownika testowego Concur](#creating-a-concur-test-user)**  -toohave odpowiednikiem Simona Britta w Concur, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="955de-146">**[Creating a Concur test user](#creating-a-concur-test-user)** - toohave a counterpart of Britta Simon in Concur that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="955de-147">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="955de-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="955de-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="955de-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="955de-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="955de-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="955de-150">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Concur.</span><span class="sxs-lookup"><span data-stu-id="955de-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Concur application.</span></span>

<span data-ttu-id="955de-151">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Concur, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="955de-151">**tooconfigure Azure AD single sign-on with Concur, perform hello following steps:**</span></span>

1. <span data-ttu-id="955de-152">W portalu Azure na powitania hello **Concur** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="955de-152">In hello Azure portal, on hello **Concur** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="955de-154">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="955de-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-concur-tutorial/tutorial_concur_samlbase.png)

3. <span data-ttu-id="955de-156">Na powitania **cząstkowe domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="955de-156">On hello **Concur Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-concur-tutorial/tutorial_concur_url.png)

    <span data-ttu-id="955de-158">a.</span><span class="sxs-lookup"><span data-stu-id="955de-158">a.</span></span> <span data-ttu-id="955de-159">W hello **Zaloguj się na adres URL** pole tekstowe, wartość hello typu przy użyciu hello następującego wzorca:`https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span><span class="sxs-lookup"><span data-stu-id="955de-159">In hello **Sign on URL** textbox, type hello value using hello following pattern: `https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span></span>

    <span data-ttu-id="955de-160">b.</span><span class="sxs-lookup"><span data-stu-id="955de-160">b.</span></span> <span data-ttu-id="955de-161">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<customer-domain>.concursolutions.com`</span><span class="sxs-lookup"><span data-stu-id="955de-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<customer-domain>.concursolutions.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="955de-162">Wartości te nie są hello prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="955de-162">These values are not hello real.</span></span> <span data-ttu-id="955de-163">Aktualizacja adresu URL i identyfikator logowania tych wartości za pomocą hello rzeczywistego.</span><span class="sxs-lookup"><span data-stu-id="955de-163">Update these values with hello actual Sign on URL and Identifier.</span></span> <span data-ttu-id="955de-164">Skontaktuj się z [zespołem pomocy technicznej klienta cząstkowe](https://www.concur.co.in/contact) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="955de-164">Contact [Concur Client support team](https://www.concur.co.in/contact) tooget these values.</span></span> 

4. <span data-ttu-id="955de-165">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="955de-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-concur-tutorial/tutorial_concur_certificate.png) 

5. <span data-ttu-id="955de-167">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="955de-167">Click **Save** button.</span></span>

    <span data-ttu-id="955de-168">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="955de-168">![Configure Single Sign-On](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span></span>

6. <span data-ttu-id="955de-169">tooconfigure rejestracji jednokrotnej w **Concur** strony, należy pobrać hello toosend **XML metadanych** tooConcur pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="955de-169">tooconfigure single sign-on on **Concur** side, you need toosend hello downloaded **Metadata XML** tooConcur support.</span></span> <span data-ttu-id="955de-170">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="955de-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

  >[!NOTE]
  ><span data-ttu-id="955de-171">Konfiguracja Hello subskrypcją Concur federacyjną rejestracją Jednokrotną za pośrednictwem SAML jest osobnym zadaniem musisz skontaktować się z [zespołem pomocy technicznej klienta cząstkowe](https://www.concur.co.in/contact) tooperform.</span><span class="sxs-lookup"><span data-stu-id="955de-171">hello configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) tooperform.</span></span> 
  
<CE>

> [!TIP]
> <span data-ttu-id="955de-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="955de-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="955de-173">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="955de-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="955de-174">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="955de-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="955de-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="955de-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="955de-176">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="955de-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="955de-178">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="955de-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="955de-179">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="955de-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="955de-181">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="955de-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="955de-183">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="955de-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="955de-185">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="955de-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="955de-187">a.</span><span class="sxs-lookup"><span data-stu-id="955de-187">a.</span></span> <span data-ttu-id="955de-188">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="955de-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="955de-189">b.</span><span class="sxs-lookup"><span data-stu-id="955de-189">b.</span></span> <span data-ttu-id="955de-190">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="955de-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="955de-191">c.</span><span class="sxs-lookup"><span data-stu-id="955de-191">c.</span></span> <span data-ttu-id="955de-192">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="955de-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="955de-193">d.</span><span class="sxs-lookup"><span data-stu-id="955de-193">d.</span></span> <span data-ttu-id="955de-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="955de-194">Click **Create**.</span></span>
 
### <a name="creating-a-concur-test-user"></a><span data-ttu-id="955de-195">Tworzenie użytkownika testowego Concur</span><span class="sxs-lookup"><span data-stu-id="955de-195">Creating a Concur test user</span></span>

<span data-ttu-id="955de-196">Aplikacja obsługuje hello tylko w czasie Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników są tworzone automatycznie w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="955de-196">Application supports hello Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="955de-197">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="955de-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="955de-198">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooConcur.</span><span class="sxs-lookup"><span data-stu-id="955de-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooConcur.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="955de-200">**tooassign tooConcur Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="955de-200">**tooassign Britta Simon tooConcur, perform hello following steps:**</span></span>

1. <span data-ttu-id="955de-201">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="955de-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="955de-203">Z listy aplikacji hello wybierz **Concur**.</span><span class="sxs-lookup"><span data-stu-id="955de-203">In hello applications list, select **Concur**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-concur-tutorial/tutorial_concur_app.png) 

3. <span data-ttu-id="955de-205">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="955de-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="955de-207">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="955de-207">Click **Add** button.</span></span> <span data-ttu-id="955de-208">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="955de-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="955de-210">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="955de-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="955de-211">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="955de-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="955de-212">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="955de-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="955de-213">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="955de-213">Testing single sign-on</span></span>

<span data-ttu-id="955de-214">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="955de-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="955de-215">Po kliknięciu kafelka Concur hello w hello Panel dostępu, należy pobrać strony logowania Concur aplikacji.</span><span class="sxs-lookup"><span data-stu-id="955de-215">When you click hello Concur tile in hello Access Panel, you should get login page of Concur application.</span></span>
<span data-ttu-id="955de-216">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="955de-216">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="955de-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="955de-217">Additional resources</span></span>

* [<span data-ttu-id="955de-218">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="955de-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="955de-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="955de-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="955de-220">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="955de-220">Configure User Provisioning</span></span>](active-directory-saas-concur-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-concur-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-concur-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-concur-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-concur-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-concur-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-concur-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-concur-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-concur-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-concur-tutorial/tutorial_general_203.png

