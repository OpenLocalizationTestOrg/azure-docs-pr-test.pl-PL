---
title: 'Samouczek: Integracji Azure Active Directory z Wingspan eTMF | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Wingspan eTMF."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ace320d3-521c-449c-992f-feabe7538de7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: ed5fda5318a0d3841af8b2db4fb74db550befaea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wingspan-etmf"></a><span data-ttu-id="accb8-103">Samouczek: Integracji Azure Active Directory z Wingspan eTMF</span><span class="sxs-lookup"><span data-stu-id="accb8-103">Tutorial: Azure Active Directory integration with Wingspan eTMF</span></span>

<span data-ttu-id="accb8-104">Z tego samouczka, dowiesz się, jak eTMF Wingspan toointegrate w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="accb8-104">In this tutorial, you learn how toointegrate Wingspan eTMF with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="accb8-105">Integracja z usługą Azure AD Wingspan eTMF zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="accb8-105">Integrating Wingspan eTMF with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="accb8-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooWingspan eTMF</span><span class="sxs-lookup"><span data-stu-id="accb8-106">You can control in Azure AD who has access tooWingspan eTMF</span></span>
- <span data-ttu-id="accb8-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooWingspan eTMF (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="accb8-107">You can enable your users tooautomatically get signed-on tooWingspan eTMF (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="accb8-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="accb8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="accb8-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="accb8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="accb8-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="accb8-110">Prerequisites</span></span>

<span data-ttu-id="accb8-111">tooconfigure integracji usługi Azure AD z Wingspan eTMF należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="accb8-111">tooconfigure Azure AD integration with Wingspan eTMF, you need hello following items:</span></span>

- <span data-ttu-id="accb8-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="accb8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="accb8-113">Wingspan eTMF jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="accb8-113">A Wingspan eTMF single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="accb8-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="accb8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="accb8-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="accb8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="accb8-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="accb8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="accb8-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="accb8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="accb8-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="accb8-118">Scenario description</span></span>
<span data-ttu-id="accb8-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="accb8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="accb8-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="accb8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="accb8-121">Dodawanie Wingspan eTMF z galerii hello</span><span class="sxs-lookup"><span data-stu-id="accb8-121">Adding Wingspan eTMF from hello gallery</span></span>
2. <span data-ttu-id="accb8-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="accb8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wingspan-etmf-from-hello-gallery"></a><span data-ttu-id="accb8-123">Dodawanie Wingspan eTMF z galerii hello</span><span class="sxs-lookup"><span data-stu-id="accb8-123">Adding Wingspan eTMF from hello gallery</span></span>
<span data-ttu-id="accb8-124">tooconfigure hello integracji Wingspan eTMF do usługi Azure AD, należy eTMF Wingspan tooadd z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="accb8-124">tooconfigure hello integration of Wingspan eTMF into Azure AD, you need tooadd Wingspan eTMF from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="accb8-125">**eTMF Wingspan tooadd z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="accb8-125">**tooadd Wingspan eTMF from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="accb8-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="accb8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="accb8-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="accb8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="accb8-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="accb8-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="accb8-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="accb8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="accb8-133">W polu wyszukiwania hello wpisz **Wingspan eTMF**.</span><span class="sxs-lookup"><span data-stu-id="accb8-133">In hello search box, type **Wingspan eTMF**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_search.png)

5. <span data-ttu-id="accb8-135">W panelu wyników hello, wybierz **Wingspan eTMF**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="accb8-135">In hello results panel, select **Wingspan eTMF**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="accb8-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="accb8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="accb8-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z eTMF Wingspan na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="accb8-138">In this section, you configure and test Azure AD single sign-on with Wingspan eTMF based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="accb8-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Wingspan eTMF jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="accb8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Wingspan eTMF is tooa user in Azure AD.</span></span> <span data-ttu-id="accb8-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Wingspan eTMF musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="accb8-140">In other words, a link relationship between an Azure AD user and hello related user in Wingspan eTMF needs toobe established.</span></span>

<span data-ttu-id="accb8-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="accb8-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Wingspan eTMF.</span></span>

<span data-ttu-id="accb8-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Wingspan eTMF, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="accb8-142">tooconfigure and test Azure AD single sign-on with Wingspan eTMF, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="accb8-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="accb8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="accb8-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="accb8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="accb8-145">**[Tworzenie użytkownika testowego eTMF Wingspan](#creating-a-wingspan-etmf-test-user)**  -toohave odpowiednikiem Simona Britta w eTMF Wingspan, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="accb8-145">**[Creating a Wingspan eTMF test user](#creating-a-wingspan-etmf-test-user)** - toohave a counterpart of Britta Simon in Wingspan eTMF that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="accb8-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="accb8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="accb8-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="accb8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="accb8-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="accb8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="accb8-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji eTMF Wingspan.</span><span class="sxs-lookup"><span data-stu-id="accb8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Wingspan eTMF application.</span></span>

<span data-ttu-id="accb8-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Wingspan eTMF wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="accb8-150">**tooconfigure Azure AD single sign-on with Wingspan eTMF, perform hello following steps:**</span></span>

1. <span data-ttu-id="accb8-151">W portalu Azure na powitania hello **Wingspan eTMF** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="accb8-151">In hello Azure portal, on hello **Wingspan eTMF** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="accb8-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="accb8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_samlbase.png)

3. <span data-ttu-id="accb8-155">Na powitania **eTMF Wingspan domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="accb8-155">On hello **Wingspan eTMF Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_url11.png)

    <span data-ttu-id="accb8-157">a.</span><span class="sxs-lookup"><span data-stu-id="accb8-157">a.</span></span> <span data-ttu-id="accb8-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<customer name>.<instance name>.mywingspan.com/saml`</span><span class="sxs-lookup"><span data-stu-id="accb8-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<customer name>.<instance name>.mywingspan.com/saml`</span></span>

    <span data-ttu-id="accb8-159">b.</span><span class="sxs-lookup"><span data-stu-id="accb8-159">b.</span></span> <span data-ttu-id="accb8-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`http://saml.<instance name>.wingspan.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="accb8-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://saml.<instance name>.wingspan.com/shibboleth`</span></span>

    <span data-ttu-id="accb8-161">c.</span><span class="sxs-lookup"><span data-stu-id="accb8-161">c.</span></span> <span data-ttu-id="accb8-162">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<customer name>.<instance name>.mywingspan.com/`</span><span class="sxs-lookup"><span data-stu-id="accb8-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<customer name>.<instance name>.mywingspan.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="accb8-163">Wartości te nie są hello prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="accb8-163">These values are not hello real.</span></span> <span data-ttu-id="accb8-164">Z hello rzeczywisty adres URL logowania, identyfikator i odpowiedzi adres URL uwzględniający powitania klienta rzeczywiste i nazwa wystąpienia, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="accb8-164">Update these values with hello actual Sign-On URL, Identifier and Reply URL including hello actual customer name and instance name.</span></span> <span data-ttu-id="accb8-165">Skontaktuj się z [zespołem pomocy technicznej klienta eTMF Wingspan](http://www.wingspan.com/contact-us/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="accb8-165">Contact [Wingspan eTMF Client support team](http://www.wingspan.com/contact-us/) tooget these values.</span></span> 

4. <span data-ttu-id="accb8-166">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="accb8-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_certificate.png) 

5. <span data-ttu-id="accb8-168">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="accb8-168">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="accb8-170">tooconfigure rejestracji jednokrotnej w **Wingspan eTMF** strony, należy pobrać hello toosend **XML metadanych** za[Wingspan eTMF Obsługa](http://www.wingspan.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="accb8-170">tooconfigure single sign-on on **Wingspan eTMF** side, you need toosend hello downloaded **Metadata XML** too[Wingspan eTMF support](http://www.wingspan.com/contact-us/).</span></span> <span data-ttu-id="accb8-171">Są to skonfigurować hello toohave prawidłowo po obu stronach połączenia logowania jednokrotnego SAML.</span><span class="sxs-lookup"><span data-stu-id="accb8-171">They set this up toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="accb8-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="accb8-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="accb8-173">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="accb8-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="accb8-174">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="accb8-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="accb8-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="accb8-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="accb8-176">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="accb8-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="accb8-178">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="accb8-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="accb8-179">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="accb8-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="accb8-181">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="accb8-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="accb8-183">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="accb8-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="accb8-185">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="accb8-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wingspanetmf-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="accb8-187">a.</span><span class="sxs-lookup"><span data-stu-id="accb8-187">a.</span></span> <span data-ttu-id="accb8-188">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="accb8-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="accb8-189">b.</span><span class="sxs-lookup"><span data-stu-id="accb8-189">b.</span></span> <span data-ttu-id="accb8-190">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="accb8-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="accb8-191">c.</span><span class="sxs-lookup"><span data-stu-id="accb8-191">c.</span></span> <span data-ttu-id="accb8-192">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="accb8-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="accb8-193">d.</span><span class="sxs-lookup"><span data-stu-id="accb8-193">d.</span></span> <span data-ttu-id="accb8-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="accb8-194">Click **Create**.</span></span>
 
### <a name="creating-a-wingspan-etmf-test-user"></a><span data-ttu-id="accb8-195">Tworzenie użytkownika testowego eTMF Wingspan</span><span class="sxs-lookup"><span data-stu-id="accb8-195">Creating a Wingspan eTMF test user</span></span>

<span data-ttu-id="accb8-196">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Wingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="accb8-196">In this section, you create a user called Britta Simon in Wingspan eTMF.</span></span> <span data-ttu-id="accb8-197">Praca z [Wingspan eTMF Obsługa](http://www.wingspan.com/contact-us/) tooadd hello użytkowników w hello Wingspan eTMF aplikacji.</span><span class="sxs-lookup"><span data-stu-id="accb8-197">Work with [Wingspan eTMF support](http://www.wingspan.com/contact-us/) tooadd hello users in hello Wingspan eTMF application.</span></span> <span data-ttu-id="accb8-198">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="accb8-198">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="accb8-199">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="accb8-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="accb8-200">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooWingspan eTMF.</span><span class="sxs-lookup"><span data-stu-id="accb8-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWingspan eTMF.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="accb8-202">**tooassign eTMF tooWingspan Simona Britta, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="accb8-202">**tooassign Britta Simon tooWingspan eTMF, perform hello following steps:**</span></span>

1. <span data-ttu-id="accb8-203">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="accb8-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="accb8-205">Z listy aplikacji hello wybierz **Wingspan eTMF**.</span><span class="sxs-lookup"><span data-stu-id="accb8-205">In hello applications list, select **Wingspan eTMF**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wingspanetmf-tutorial/tutorial_wingspanetmf_app.png) 

3. <span data-ttu-id="accb8-207">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="accb8-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="accb8-209">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="accb8-209">Click **Add** button.</span></span> <span data-ttu-id="accb8-210">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="accb8-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="accb8-212">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="accb8-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="accb8-213">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="accb8-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="accb8-214">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="accb8-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="accb8-215">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="accb8-215">Testing single sign-on</span></span>

<span data-ttu-id="accb8-216">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="accb8-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> 

<span data-ttu-id="accb8-217">Kliknij Kafelek eTMF Wingspan hello hello Panel dostępu, będziesz przekierowanie tooOrganization logowania na stronie.</span><span class="sxs-lookup"><span data-stu-id="accb8-217">Click hello Wingspan eTMF tile in hello Access Panel, you will be redirected tooOrganization sign on page.</span></span> <span data-ttu-id="accb8-218">Po pomyślnym logowaniu będzie zalogowane tooyour Wingspan eTMF aplikacji.</span><span class="sxs-lookup"><span data-stu-id="accb8-218">After successful login, you will be signed-on tooyour Wingspan eTMF application.</span></span> <span data-ttu-id="accb8-219">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="accb8-219">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="accb8-220">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="accb8-220">Additional resources</span></span>

* [<span data-ttu-id="accb8-221">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="accb8-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="accb8-222">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="accb8-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wingspanetmf-tutorial/tutorial_general_203.png

