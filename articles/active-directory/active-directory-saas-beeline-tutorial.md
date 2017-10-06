---
title: 'Samouczek: Integracji Azure Active Directory z BeeLine | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i BeeLine."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0726859d-1dac-44a0-810b-da56d89039ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 92f228d33980c21ad934185ab89d73795f7f69bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-beeline"></a><span data-ttu-id="861ab-103">Samouczek: Integracji Azure Active Directory z BeeLine</span><span class="sxs-lookup"><span data-stu-id="861ab-103">Tutorial: Azure Active Directory integration with BeeLine</span></span>

<span data-ttu-id="861ab-104">Z tego samouczka, dowiesz się, jak toointegrate BeeLine w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="861ab-104">In this tutorial, you learn how toointegrate BeeLine with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="861ab-105">Integracja z usługą Azure AD BeeLine zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="861ab-105">Integrating BeeLine with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="861ab-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooBeeLine</span><span class="sxs-lookup"><span data-stu-id="861ab-106">You can control in Azure AD who has access tooBeeLine</span></span>
- <span data-ttu-id="861ab-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooBeeLine (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="861ab-107">You can enable your users tooautomatically get signed-on tooBeeLine (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="861ab-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="861ab-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="861ab-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="861ab-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="861ab-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="861ab-110">Prerequisites</span></span>

<span data-ttu-id="861ab-111">tooconfigure integracji z usługą Azure AD z BeeLine należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="861ab-111">tooconfigure Azure AD integration with BeeLine, you need hello following items:</span></span>

- <span data-ttu-id="861ab-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="861ab-112">An Azure AD subscription</span></span>
- <span data-ttu-id="861ab-113">BeeLine logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="861ab-113">A BeeLine single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="861ab-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="861ab-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="861ab-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="861ab-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="861ab-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="861ab-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="861ab-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="861ab-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="861ab-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="861ab-118">Scenario description</span></span>
<span data-ttu-id="861ab-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="861ab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="861ab-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="861ab-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="861ab-121">Dodawanie BeeLine z galerii hello</span><span class="sxs-lookup"><span data-stu-id="861ab-121">Adding BeeLine from hello gallery</span></span>
2. <span data-ttu-id="861ab-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="861ab-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-beeline-from-hello-gallery"></a><span data-ttu-id="861ab-123">Dodawanie BeeLine z galerii hello</span><span class="sxs-lookup"><span data-stu-id="861ab-123">Adding BeeLine from hello gallery</span></span>
<span data-ttu-id="861ab-124">tooconfigure hello integracji BeeLine do usługi Azure AD, należy tooadd BeeLine z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="861ab-124">tooconfigure hello integration of BeeLine into Azure AD, you need tooadd BeeLine from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="861ab-125">**tooadd BeeLine z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="861ab-125">**tooadd BeeLine from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="861ab-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="861ab-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="861ab-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="861ab-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="861ab-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="861ab-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="861ab-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="861ab-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="861ab-133">W polu wyszukiwania hello wpisz **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="861ab-133">In hello search box, type **BeeLine**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_search.png)

5. <span data-ttu-id="861ab-135">W panelu wyników hello zaznacz **BeeLine**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="861ab-135">In hello results panel, select **BeeLine**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="861ab-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="861ab-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="861ab-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z BeeLine na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="861ab-138">In this section, you configure and test Azure AD single sign-on with BeeLine based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="861ab-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w BeeLine jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="861ab-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BeeLine is tooa user in Azure AD.</span></span> <span data-ttu-id="861ab-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w BeeLine musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="861ab-140">In other words, a link relationship between an Azure AD user and hello related user in BeeLine needs toobe established.</span></span>

<span data-ttu-id="861ab-141">W BeeLine, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="861ab-141">In BeeLine, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="861ab-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z BeeLine, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="861ab-142">tooconfigure and test Azure AD single sign-on with BeeLine, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="861ab-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="861ab-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="861ab-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="861ab-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="861ab-145">**[Tworzenie użytkownika testowego BeeLine](#creating-a-beeline-test-user)**  -toohave odpowiednikiem Simona Britta w BeeLine, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="861ab-145">**[Creating a BeeLine test user](#creating-a-beeline-test-user)** - toohave a counterpart of Britta Simon in BeeLine that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="861ab-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="861ab-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="861ab-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="861ab-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="861ab-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="861ab-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="861ab-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji BeeLine.</span><span class="sxs-lookup"><span data-stu-id="861ab-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BeeLine application.</span></span>

<span data-ttu-id="861ab-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z BeeLine, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="861ab-150">**tooconfigure Azure AD single sign-on with BeeLine, perform hello following steps:**</span></span>

1. <span data-ttu-id="861ab-151">W portalu Azure na powitania hello **BeeLine** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="861ab-151">In hello Azure portal, on hello **BeeLine** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="861ab-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="861ab-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_samlbase.png)

3. <span data-ttu-id="861ab-155">Na powitania **BeeLine domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="861ab-155">On hello **BeeLine Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_url.png)

    <span data-ttu-id="861ab-157">a.</span><span class="sxs-lookup"><span data-stu-id="861ab-157">a.</span></span> <span data-ttu-id="861ab-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://projects.beeline.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="861ab-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://projects.beeline.net/<instancename>`</span></span>

    <span data-ttu-id="861ab-159">b.</span><span class="sxs-lookup"><span data-stu-id="861ab-159">b.</span></span> <span data-ttu-id="861ab-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="861ab-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://projects.beeline.net/<instancename>/SSO_External.ashx`|
    | `https://projects.beeline.net/<companyname>/SSO_External.ashx` |

    > [!NOTE] 
    > <span data-ttu-id="861ab-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="861ab-161">These values are not real.</span></span> <span data-ttu-id="861ab-162">Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="861ab-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="861ab-163">Skontaktuj się z [zespołem pomocy technicznej BeeLine](https://www.beeline.com/contact-us/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="861ab-163">Contact [BeeLine support team](https://www.beeline.com/contact-us/) tooget these values.</span></span>
 
4. <span data-ttu-id="861ab-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="861ab-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_certificate.png) 

5. <span data-ttu-id="861ab-166">Aplikacja Beeline oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="861ab-166">Your Beeline application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="861ab-167">We współpracy z [zespołem pomocy technicznej BeeLine](https://www.beeline.com/contact-us/) tooidentify pierwszy hello identyfikator użytkownika, który zostanie zamapowane do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="861ab-167">Please work with [BeeLine support team](https://www.beeline.com/contact-us/) first tooidentify hello correct user identifier which will be mapped into hello application.</span></span> <span data-ttu-id="861ab-168">Należy również wziąć ze wskazówkami hello [BeeLine zespołem pomocy technicznej](https://www.beeline.com/contact-us/) o hello atrybutów, które chcą, aby to mapowanie toouse.</span><span class="sxs-lookup"><span data-stu-id="861ab-168">Also please take hello guidance from [BeeLine support team](https://www.beeline.com/contact-us/) about hello attribute which they want toouse for this mapping.</span></span> <span data-ttu-id="861ab-169">Wartość tego atrybutu hello można zarządzać za pomocą hello **atrybuty użytkownika** kartę aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="861ab-169">You can manage hello value of this attribute from hello **User Attributes** tab of hello application.</span></span> <span data-ttu-id="861ab-170">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="861ab-170">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="861ab-171">W tym miejscu zostały zamapowane hello **identyfikator użytkownika** oświadczenie z hello **userprincipalname** atrybut, który zawiera identyfikator unikatowy użytkownika, który zostanie wysłany toohello Beeline aplikacji hello co pomyślne SAML Odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="861ab-171">Here we have mapped hello **User Identifier** claim with hello **userprincipalname** attribute, which provides unique user ID, which will be sent toohello Beeline application in hello every successful SAML Response.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-beeline-tutorial/tutorial_attribute.png)  

6. <span data-ttu-id="861ab-173">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="861ab-173">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-beeline-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="861ab-175">Na powitania **konfiguracji BeeLine** kliknij **skonfigurować BeeLine** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="861ab-175">On hello **BeeLine Configuration** section, click **Configure BeeLine** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="861ab-176">Kopiuj hello **Sign-Out adres URL** i **SAML identyfikator jednostki** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="861ab-176">Copy hello **Sign-Out URL** and **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_configure.png) 

8. <span data-ttu-id="861ab-178">tooconfigure rejestracji jednokrotnej w **BeeLine** strony, należy pobrać hello toosend **XML metadanych** i **identyfikator jednostki SAML**, **Sign-Out URL**za[zespołem pomocy technicznej BeeLine](https://www.beeline.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="861ab-178">tooconfigure single sign-on on **BeeLine** side, you need toosend hello downloaded **Metadata XML** and **SAML Entity ID**, **Sign-Out URL** too[BeeLine support team](https://www.beeline.com/contact-us/).</span></span>

> [!TIP]
> <span data-ttu-id="861ab-179">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="861ab-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="861ab-180">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="861ab-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="861ab-181">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="861ab-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="861ab-182">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="861ab-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="861ab-183">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="861ab-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="861ab-185">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="861ab-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="861ab-186">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="861ab-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="861ab-188">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="861ab-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="861ab-190">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="861ab-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="861ab-192">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="861ab-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="861ab-194">a.</span><span class="sxs-lookup"><span data-stu-id="861ab-194">a.</span></span> <span data-ttu-id="861ab-195">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="861ab-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="861ab-196">b.</span><span class="sxs-lookup"><span data-stu-id="861ab-196">b.</span></span> <span data-ttu-id="861ab-197">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="861ab-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="861ab-198">c.</span><span class="sxs-lookup"><span data-stu-id="861ab-198">c.</span></span> <span data-ttu-id="861ab-199">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="861ab-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="861ab-200">d.</span><span class="sxs-lookup"><span data-stu-id="861ab-200">d.</span></span> <span data-ttu-id="861ab-201">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="861ab-201">Click **Create**.</span></span>
 
### <a name="creating-a-beeline-test-user"></a><span data-ttu-id="861ab-202">Tworzenie użytkownika testowego BeeLine</span><span class="sxs-lookup"><span data-stu-id="861ab-202">Creating a BeeLine test user</span></span>

<span data-ttu-id="861ab-203">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Beeline.</span><span class="sxs-lookup"><span data-stu-id="861ab-203">In this section, you create a user called Britta Simon in Beeline.</span></span> <span data-ttu-id="861ab-204">Aplikacja beeline musi wszystkich toobe użytkowników hello udostępniane w aplikacji hello przed wykonaniem rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="861ab-204">Beeline application needs all hello users toobe provisioned in hello application before doing Single Sign On.</span></span> <span data-ttu-id="861ab-205">Aby pracować z hello [zespołem pomocy technicznej BeeLine](https://www.beeline.com/contact-us/) tooprovision tych użytkowników do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="861ab-205">So work with hello [BeeLine support team](https://www.beeline.com/contact-us/) tooprovision all these users into hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="861ab-206">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="861ab-206">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="861ab-207">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooBeeLine.</span><span class="sxs-lookup"><span data-stu-id="861ab-207">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBeeLine.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="861ab-209">**tooassign tooBeeLine Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="861ab-209">**tooassign Britta Simon tooBeeLine, perform hello following steps:**</span></span>

1. <span data-ttu-id="861ab-210">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="861ab-210">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="861ab-212">Z listy aplikacji hello wybierz **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="861ab-212">In hello applications list, select **BeeLine**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_app.png) 

3. <span data-ttu-id="861ab-214">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="861ab-214">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="861ab-216">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="861ab-216">Click **Add** button.</span></span> <span data-ttu-id="861ab-217">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="861ab-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="861ab-219">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="861ab-219">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="861ab-220">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="861ab-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="861ab-221">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="861ab-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="861ab-222">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="861ab-222">Testing single sign-on</span></span>

<span data-ttu-id="861ab-223">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="861ab-223">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="861ab-224">Po kliknięciu kafelka Beeline hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Beeline aplikacji.</span><span class="sxs-lookup"><span data-stu-id="861ab-224">When you click hello Beeline tile in hello Access Panel, you should get automatically signed-on tooyour Beeline application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="861ab-225">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="861ab-225">Additional resources</span></span>

* [<span data-ttu-id="861ab-226">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="861ab-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="861ab-227">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="861ab-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_203.png

