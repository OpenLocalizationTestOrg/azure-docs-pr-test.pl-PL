---
title: 'Samouczek: Integracji Azure Active Directory z Convercent | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Convercent."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9c9d290-0e13-490b-b559-0be772d6a690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: e6d09d7de52779dcf05e80215df9369ebc2ed06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-convercent"></a><span data-ttu-id="4fef1-103">Samouczek: Integracji Azure Active Directory z Convercent</span><span class="sxs-lookup"><span data-stu-id="4fef1-103">Tutorial: Azure Active Directory integration with Convercent</span></span>

<span data-ttu-id="4fef1-104">Z tego samouczka, dowiesz się, jak toointegrate Convercent w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4fef1-104">In this tutorial, you learn how toointegrate Convercent with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4fef1-105">Integracja z usługą Azure AD Convercent zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="4fef1-105">Integrating Convercent with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4fef1-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooConvercent</span><span class="sxs-lookup"><span data-stu-id="4fef1-106">You can control in Azure AD who has access tooConvercent</span></span>
- <span data-ttu-id="4fef1-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooConvercent (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fef1-107">You can enable your users tooautomatically get signed-on tooConvercent (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4fef1-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4fef1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4fef1-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4fef1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fef1-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4fef1-110">Prerequisites</span></span>

<span data-ttu-id="4fef1-111">tooconfigure integracji z usługą Azure AD z Convercent należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="4fef1-111">tooconfigure Azure AD integration with Convercent, you need hello following items:</span></span>

- <span data-ttu-id="4fef1-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fef1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4fef1-113">Convercent jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="4fef1-113">A Convercent single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4fef1-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="4fef1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4fef1-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="4fef1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4fef1-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="4fef1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4fef1-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4fef1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4fef1-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="4fef1-118">Scenario description</span></span>
<span data-ttu-id="4fef1-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="4fef1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4fef1-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="4fef1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4fef1-121">Dodawanie Convercent z galerii hello</span><span class="sxs-lookup"><span data-stu-id="4fef1-121">Adding Convercent from hello gallery</span></span>
2. <span data-ttu-id="4fef1-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="4fef1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-convercent-from-hello-gallery"></a><span data-ttu-id="4fef1-123">Dodawanie Convercent z galerii hello</span><span class="sxs-lookup"><span data-stu-id="4fef1-123">Adding Convercent from hello gallery</span></span>
<span data-ttu-id="4fef1-124">tooconfigure hello integracji Convercent do usługi Azure AD, należy tooadd Convercent z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="4fef1-124">tooconfigure hello integration of Convercent into Azure AD, you need tooadd Convercent from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4fef1-125">**tooadd Convercent z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="4fef1-125">**tooadd Convercent from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fef1-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4fef1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="4fef1-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="4fef1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4fef1-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4fef1-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="4fef1-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4fef1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="4fef1-133">W polu wyszukiwania hello wpisz **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="4fef1-133">In hello search box, type **Convercent**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_search.png)

5. <span data-ttu-id="4fef1-135">W panelu wyników hello zaznacz **Convercent**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="4fef1-135">In hello results panel, select **Convercent**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4fef1-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="4fef1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4fef1-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Convercent na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="4fef1-138">In this section, you configure and test Azure AD single sign-on with Convercent based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4fef1-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Convercent jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4fef1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Convercent is tooa user in Azure AD.</span></span> <span data-ttu-id="4fef1-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Convercent musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="4fef1-140">In other words, a link relationship between an Azure AD user and hello related user in Convercent needs toobe established.</span></span>

<span data-ttu-id="4fef1-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Convercent.</span><span class="sxs-lookup"><span data-stu-id="4fef1-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Convercent.</span></span>

<span data-ttu-id="4fef1-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Convercent, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="4fef1-142">tooconfigure and test Azure AD single sign-on with Convercent, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4fef1-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="4fef1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4fef1-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="4fef1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4fef1-145">**[Tworzenie użytkownika testowego Convercent](#creating-a-convercent-test-user)**  -toohave odpowiednikiem Simona Britta w Convercent, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4fef1-145">**[Creating a Convercent test user](#creating-a-convercent-test-user)** - toohave a counterpart of Britta Simon in Convercent that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4fef1-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="4fef1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4fef1-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="4fef1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4fef1-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4fef1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4fef1-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Convercent.</span><span class="sxs-lookup"><span data-stu-id="4fef1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Convercent application.</span></span>

<span data-ttu-id="4fef1-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Convercent, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="4fef1-150">**tooconfigure Azure AD single sign-on with Convercent, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fef1-151">W portalu Azure na powitania hello **Convercent** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="4fef1-151">In hello Azure portal, on hello **Convercent** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="4fef1-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="4fef1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_samlbase.png)

3. <span data-ttu-id="4fef1-155">Na powitania **Convercent domeny i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP zainicjował tryb**, wykonaj powitania po kroku:</span><span class="sxs-lookup"><span data-stu-id="4fef1-155">On hello **Convercent Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following step:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url.png)

    <span data-ttu-id="4fef1-157">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="4fef1-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.convercent.com/`</span></span>
 
4. <span data-ttu-id="4fef1-158">Jeśli chcesz, aby aplikacja hello tooconfigure w **SP zainicjował tryb**, na powitania **Convercent domeny i adres URL** sekcji wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="4fef1-158">If you wish tooconfigure hello application in **SP initiated mode**, on hello **Convercent Domain and URLs** section perform hello following steps:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url1.png)

     <span data-ttu-id="4fef1-160">a.</span><span class="sxs-lookup"><span data-stu-id="4fef1-160">a.</span></span> <span data-ttu-id="4fef1-161">Kliknij przycisk **"Pokaż zaawansowane ustawienia adresu URL."**</span><span class="sxs-lookup"><span data-stu-id="4fef1-161">Click **"Show advanced URL settings."**</span></span> 

     <span data-ttu-id="4fef1-162">b.</span><span class="sxs-lookup"><span data-stu-id="4fef1-162">b.</span></span> <span data-ttu-id="4fef1-163">W hello **na adres URL logowania** pole tekstowe, wartość hello typu przy użyciu hello następującego wzorca:`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="4fef1-163">In hello **Sign On URL** textbox, type hello value using hello following pattern: `https://<instancename>.convercent.com/`</span></span>

     <span data-ttu-id="4fef1-164">c.</span><span class="sxs-lookup"><span data-stu-id="4fef1-164">c.</span></span> <span data-ttu-id="4fef1-165">W hello **stan przekazywania** pole tekstowe, wartość hello typu przy użyciu hello następującego wzorca:`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="4fef1-165">In hello **Relay State** textbox, type hello value using hello following pattern: `https://<instancename>.convercent.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4fef1-166">Wartości te nie są hello wartości rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="4fef1-166">These values are not hello real values.</span></span> <span data-ttu-id="4fef1-167">Zaktualizować te wartości z hello rzeczywisty identyfikator, zaloguj się na adres URL i stan przekazywania.</span><span class="sxs-lookup"><span data-stu-id="4fef1-167">Update these values with hello actual Identifier, Sign On URL and Relay State.</span></span> <span data-ttu-id="4fef1-168">Skontaktuj się z [zespołem pomocy technicznej klienta Convercent](http://support.convercent.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="4fef1-168">Contact [Convercent Client support team](http://support.convercent.com) tooget these values.</span></span>

5. <span data-ttu-id="4fef1-169">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="4fef1-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_certificate.png) 

6. <span data-ttu-id="4fef1-171">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4fef1-171">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-convercent-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="4fef1-173">tooget logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z [zespołem pomocy technicznej Convercent](mailto:support@convercent.com) i dostarczać hello pobrane **XML metadanych**.</span><span class="sxs-lookup"><span data-stu-id="4fef1-173">tooget SSO configured for your application, contact [Convercent support team](mailto:support@convercent.com) and provide them with hello downloaded **Metadata XML**.</span></span>

> [!TIP]
> <span data-ttu-id="4fef1-174">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="4fef1-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4fef1-175">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="4fef1-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4fef1-176">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4fef1-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4fef1-177">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fef1-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="4fef1-178">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="4fef1-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="4fef1-180">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="4fef1-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fef1-181">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4fef1-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4fef1-183">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="4fef1-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4fef1-185">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4fef1-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4fef1-187">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4fef1-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4fef1-189">a.</span><span class="sxs-lookup"><span data-stu-id="4fef1-189">a.</span></span> <span data-ttu-id="4fef1-190">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4fef1-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4fef1-191">b.</span><span class="sxs-lookup"><span data-stu-id="4fef1-191">b.</span></span> <span data-ttu-id="4fef1-192">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4fef1-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4fef1-193">c.</span><span class="sxs-lookup"><span data-stu-id="4fef1-193">c.</span></span> <span data-ttu-id="4fef1-194">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="4fef1-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4fef1-195">d.</span><span class="sxs-lookup"><span data-stu-id="4fef1-195">d.</span></span> <span data-ttu-id="4fef1-196">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4fef1-196">Click **Create**.</span></span>
 
### <a name="creating-a-convercent-test-user"></a><span data-ttu-id="4fef1-197">Tworzenie użytkownika testowego Convercent</span><span class="sxs-lookup"><span data-stu-id="4fef1-197">Creating a Convercent test user</span></span>

<span data-ttu-id="4fef1-198">Praca z [zespołem pomocy technicznej Convercent](mailto:support@convercent.com) tooadd hello użytkowników hello Convercent platformy.</span><span class="sxs-lookup"><span data-stu-id="4fef1-198">Work with [Convercent support team](mailto:support@convercent.com) tooadd hello users in hello Convercent platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4fef1-199">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fef1-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4fef1-200">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooConvercent.</span><span class="sxs-lookup"><span data-stu-id="4fef1-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooConvercent.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="4fef1-202">**tooassign tooConvercent Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="4fef1-202">**tooassign Britta Simon tooConvercent, perform hello following steps:**</span></span>

1. <span data-ttu-id="4fef1-203">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4fef1-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="4fef1-205">Z listy aplikacji hello wybierz **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="4fef1-205">In hello applications list, select **Convercent**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_app.png) 

3. <span data-ttu-id="4fef1-207">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="4fef1-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="4fef1-209">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4fef1-209">Click **Add** button.</span></span> <span data-ttu-id="4fef1-210">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4fef1-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="4fef1-212">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="4fef1-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4fef1-213">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4fef1-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4fef1-214">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4fef1-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4fef1-215">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4fef1-215">Testing single sign-on</span></span>

<span data-ttu-id="4fef1-216">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="4fef1-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4fef1-217">Po kliknięciu kafelka Convercent hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Convercent aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4fef1-217">When you click hello Convercent tile in hello Access Panel, you should get automatically signed-on tooyour Convercent application.</span></span>
<span data-ttu-id="4fef1-218">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4fef1-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4fef1-219">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="4fef1-219">Additional resources</span></span>

* [<span data-ttu-id="4fef1-220">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4fef1-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4fef1-221">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4fef1-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_203.png

