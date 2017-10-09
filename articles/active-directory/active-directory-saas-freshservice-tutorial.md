---
title: 'Samouczek: Integracji Azure Active Directory z Freshservice | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Freshservice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d73624b87d058f66885ae72fda69a0aacc89c1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a><span data-ttu-id="59fcc-103">Samouczek: Integracji Azure Active Directory z Freshservice</span><span class="sxs-lookup"><span data-stu-id="59fcc-103">Tutorial: Azure Active Directory integration with Freshservice</span></span>

<span data-ttu-id="59fcc-104">Z tego samouczka, dowiesz się, jak toointegrate Freshservice w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="59fcc-104">In this tutorial, you learn how toointegrate Freshservice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="59fcc-105">Integracja z usługą Azure AD Freshservice zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="59fcc-105">Integrating Freshservice with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="59fcc-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooFreshservice</span><span class="sxs-lookup"><span data-stu-id="59fcc-106">You can control in Azure AD who has access tooFreshservice</span></span>
- <span data-ttu-id="59fcc-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooFreshservice (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="59fcc-107">You can enable your users tooautomatically get signed-on tooFreshservice (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="59fcc-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="59fcc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="59fcc-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="59fcc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59fcc-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="59fcc-110">Prerequisites</span></span>

<span data-ttu-id="59fcc-111">tooconfigure integracji z usługą Azure AD z Freshservice należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="59fcc-111">tooconfigure Azure AD integration with Freshservice, you need hello following items:</span></span>

- <span data-ttu-id="59fcc-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="59fcc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="59fcc-113">Freshservice jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="59fcc-113">A Freshservice single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="59fcc-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="59fcc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="59fcc-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="59fcc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="59fcc-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="59fcc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="59fcc-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="59fcc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="59fcc-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="59fcc-118">Scenario description</span></span>
<span data-ttu-id="59fcc-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="59fcc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="59fcc-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="59fcc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="59fcc-121">Dodawanie Freshservice z galerii hello</span><span class="sxs-lookup"><span data-stu-id="59fcc-121">Adding Freshservice from hello gallery</span></span>
2. <span data-ttu-id="59fcc-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="59fcc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshservice-from-hello-gallery"></a><span data-ttu-id="59fcc-123">Dodawanie Freshservice z galerii hello</span><span class="sxs-lookup"><span data-stu-id="59fcc-123">Adding Freshservice from hello gallery</span></span>
<span data-ttu-id="59fcc-124">tooconfigure hello integracji Freshservice do usługi Azure AD, należy tooadd Freshservice z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="59fcc-124">tooconfigure hello integration of Freshservice into Azure AD, you need tooadd Freshservice from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="59fcc-125">**tooadd Freshservice z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="59fcc-125">**tooadd Freshservice from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="59fcc-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="59fcc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="59fcc-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="59fcc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="59fcc-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="59fcc-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="59fcc-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="59fcc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="59fcc-133">W polu wyszukiwania hello wpisz **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="59fcc-133">In hello search box, type **Freshservice**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_search.png)

5. <span data-ttu-id="59fcc-135">W panelu wyników hello zaznacz **Freshservice**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="59fcc-135">In hello results panel, select **Freshservice**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="59fcc-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="59fcc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="59fcc-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Freshservice w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="59fcc-138">In this section, you configure and test Azure AD single sign-on with Freshservice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="59fcc-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Freshservice jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59fcc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Freshservice is tooa user in Azure AD.</span></span> <span data-ttu-id="59fcc-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Freshservice musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="59fcc-140">In other words, a link relationship between an Azure AD user and hello related user in Freshservice needs toobe established.</span></span>

<span data-ttu-id="59fcc-141">W Freshservice, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="59fcc-141">In Freshservice, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="59fcc-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Freshservice, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="59fcc-142">tooconfigure and test Azure AD single sign-on with Freshservice, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="59fcc-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="59fcc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="59fcc-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="59fcc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="59fcc-145">**[Tworzenie użytkownika testowego Freshservice](#creating-a-freshservice-test-user)**  -toohave odpowiednikiem Simona Britta w Freshservice, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="59fcc-145">**[Creating a Freshservice test user](#creating-a-freshservice-test-user)** - toohave a counterpart of Britta Simon in Freshservice that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="59fcc-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="59fcc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="59fcc-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="59fcc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="59fcc-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="59fcc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="59fcc-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Freshservice.</span><span class="sxs-lookup"><span data-stu-id="59fcc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Freshservice application.</span></span>

<span data-ttu-id="59fcc-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Freshservice, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="59fcc-150">**tooconfigure Azure AD single sign-on with Freshservice, perform hello following steps:**</span></span>

1. <span data-ttu-id="59fcc-151">W portalu Azure na powitania hello **Freshservice** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="59fcc-151">In hello Azure portal, on hello **Freshservice** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="59fcc-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="59fcc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_samlbase.png)

3. <span data-ttu-id="59fcc-155">Na powitania **Freshservice domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="59fcc-155">On hello **Freshservice Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_url.png)

    <span data-ttu-id="59fcc-157">a.</span><span class="sxs-lookup"><span data-stu-id="59fcc-157">a.</span></span> <span data-ttu-id="59fcc-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="59fcc-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<democompany>.freshservice.com`</span></span>

    <span data-ttu-id="59fcc-159">b.</span><span class="sxs-lookup"><span data-stu-id="59fcc-159">b.</span></span> <span data-ttu-id="59fcc-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="59fcc-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<democompany>.freshservice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="59fcc-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="59fcc-161">These values are not real.</span></span> <span data-ttu-id="59fcc-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="59fcc-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="59fcc-163">Skontaktuj się z [zespołem pomocy technicznej klienta Freshservice](https://support.freshservice.com/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="59fcc-163">Contact [Freshservice Client support team](https://support.freshservice.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="59fcc-164">Na powitania **certyfikat podpisywania SAML** sekcji, skopiuj **odcisk PALCA** wartości certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="59fcc-164">On hello **SAML Signing Certificate** section, copy **THUMBPRINT** value of certificate.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_certificate.png) 

5. <span data-ttu-id="59fcc-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="59fcc-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshservice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="59fcc-168">Na powitania **konfiguracji Freshservice** kliknij **skonfigurować Freshservice** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="59fcc-168">On hello **Freshservice Configuration** section, click **Configure Freshservice** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="59fcc-169">Witaj kopii **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="59fcc-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_configure.png) 

7. <span data-ttu-id="59fcc-171">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy Freshservice tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="59fcc-171">In a different web browser window, log in tooyour Freshservice company site as an administrator.</span></span>

8. <span data-ttu-id="59fcc-172">W menu hello na górze hello, kliknij przycisk **Admin**.</span><span class="sxs-lookup"><span data-stu-id="59fcc-172">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="59fcc-173">![Administrator](./media/active-directory-saas-freshservice-tutorial/ic790814.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="59fcc-173">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

9. <span data-ttu-id="59fcc-174">W hello **portalu klienta**, kliknij przycisk **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="59fcc-174">In hello **Customer Portal**, click **Security**.</span></span>
   
    <span data-ttu-id="59fcc-175">![Zabezpieczenia](./media/active-directory-saas-freshservice-tutorial/ic790815.png "zabezpieczeń")</span><span class="sxs-lookup"><span data-stu-id="59fcc-175">![Security](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Security")</span></span>

10. <span data-ttu-id="59fcc-176">W hello **zabezpieczeń** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="59fcc-176">In hello **Security** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="59fcc-177">![Jednokrotne](./media/active-directory-saas-freshservice-tutorial/ic790816.png "jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="59fcc-177">![Single Sign On](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Single Sign On")</span></span>
   
    <span data-ttu-id="59fcc-178">a.</span><span class="sxs-lookup"><span data-stu-id="59fcc-178">a.</span></span> <span data-ttu-id="59fcc-179">Przełącznik **jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="59fcc-179">Switch **Single Sign On**.</span></span>

    <span data-ttu-id="59fcc-180">b.</span><span class="sxs-lookup"><span data-stu-id="59fcc-180">b.</span></span> <span data-ttu-id="59fcc-181">Wybierz **logowania jednokrotnego SAML**.</span><span class="sxs-lookup"><span data-stu-id="59fcc-181">Select **SAML SSO**.</span></span>

    <span data-ttu-id="59fcc-182">c.</span><span class="sxs-lookup"><span data-stu-id="59fcc-182">c.</span></span> <span data-ttu-id="59fcc-183">W hello **adres URL logowania SAML** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="59fcc-183">In hello **SAML Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="59fcc-184">d.</span><span class="sxs-lookup"><span data-stu-id="59fcc-184">d.</span></span> <span data-ttu-id="59fcc-185">W hello **adresu URL wylogowania** pole tekstowe, Wklej wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="59fcc-185">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="59fcc-186">e.</span><span class="sxs-lookup"><span data-stu-id="59fcc-186">e.</span></span> <span data-ttu-id="59fcc-187">W **odcisk palca certyfikatu zabezpieczeń** pole tekstowe, Wklej hello **odcisk PALCA** wartość certyfikatów, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="59fcc-187">In **Security Certificate Fingerprint** textbox, paste hello **THUMBPRINT** value of certificate which you have copied from Azure portal.</span></span>

    <span data-ttu-id="59fcc-188">f.</span><span class="sxs-lookup"><span data-stu-id="59fcc-188">f.</span></span> <span data-ttu-id="59fcc-189">Kliknij przycisk **Zapisz**</span><span class="sxs-lookup"><span data-stu-id="59fcc-189">Click **Save**</span></span>
   
> [!TIP]
> <span data-ttu-id="59fcc-190">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="59fcc-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="59fcc-191">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="59fcc-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="59fcc-192">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="59fcc-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="59fcc-193">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="59fcc-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="59fcc-194">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="59fcc-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="59fcc-196">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="59fcc-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="59fcc-197">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="59fcc-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="59fcc-199">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="59fcc-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="59fcc-201">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="59fcc-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="59fcc-203">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="59fcc-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="59fcc-205">a.</span><span class="sxs-lookup"><span data-stu-id="59fcc-205">a.</span></span> <span data-ttu-id="59fcc-206">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="59fcc-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="59fcc-207">b.</span><span class="sxs-lookup"><span data-stu-id="59fcc-207">b.</span></span> <span data-ttu-id="59fcc-208">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="59fcc-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="59fcc-209">c.</span><span class="sxs-lookup"><span data-stu-id="59fcc-209">c.</span></span> <span data-ttu-id="59fcc-210">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="59fcc-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="59fcc-211">d.</span><span class="sxs-lookup"><span data-stu-id="59fcc-211">d.</span></span> <span data-ttu-id="59fcc-212">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="59fcc-212">Click **Create**.</span></span>
 
### <a name="creating-a-freshservice-test-user"></a><span data-ttu-id="59fcc-213">Tworzenie użytkownika testowego Freshservice</span><span class="sxs-lookup"><span data-stu-id="59fcc-213">Creating a Freshservice test user</span></span>

<span data-ttu-id="59fcc-214">toolog użytkowników tooenable usługi Azure AD w tooFreshService, muszą mieć przydzielone do FreshService.</span><span class="sxs-lookup"><span data-stu-id="59fcc-214">tooenable Azure AD users toolog in tooFreshService, they must be provisioned into FreshService.</span></span> <span data-ttu-id="59fcc-215">W przypadku hello FreshService Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="59fcc-215">In hello case of FreshService, provisioning is a manual task.</span></span>

<span data-ttu-id="59fcc-216">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="59fcc-216">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="59fcc-217">Zaloguj się za tooyour **FreshService** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="59fcc-217">Log in tooyour **FreshService** company site as an administrator.</span></span>

2. <span data-ttu-id="59fcc-218">W menu hello na górze hello, kliknij przycisk **Admin**.</span><span class="sxs-lookup"><span data-stu-id="59fcc-218">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="59fcc-219">![Administrator](./media/active-directory-saas-freshservice-tutorial/ic790814.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="59fcc-219">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

3. <span data-ttu-id="59fcc-220">W hello **Zarządzanie użytkownikami** kliknij **jednostek żądających**.</span><span class="sxs-lookup"><span data-stu-id="59fcc-220">In hello **User Management** section, click **Requesters**.</span></span>
   
    <span data-ttu-id="59fcc-221">![Jednostek żądających](./media/active-directory-saas-freshservice-tutorial/ic790818.png "jednostek żądających")</span><span class="sxs-lookup"><span data-stu-id="59fcc-221">![Requesters](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Requesters")</span></span>

4. <span data-ttu-id="59fcc-222">Kliknij przycisk **nowy element żądający**.</span><span class="sxs-lookup"><span data-stu-id="59fcc-222">Click **New Requester**.</span></span>
   
    <span data-ttu-id="59fcc-223">![Nowych jednostek żądających](./media/active-directory-saas-freshservice-tutorial/ic790819.png "nowych jednostek żądających")</span><span class="sxs-lookup"><span data-stu-id="59fcc-223">![New Requesters](./media/active-directory-saas-freshservice-tutorial/ic790819.png "New Requesters")</span></span>

5. <span data-ttu-id="59fcc-224">W hello **nowy element żądający** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="59fcc-224">In hello **New Requester** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="59fcc-225">![Nowy element żądający](./media/active-directory-saas-freshservice-tutorial/ic790820.png "nowy element żądający")</span><span class="sxs-lookup"><span data-stu-id="59fcc-225">![New Requester](./media/active-directory-saas-freshservice-tutorial/ic790820.png "New Requester")</span></span>   

    <span data-ttu-id="59fcc-226">a.</span><span class="sxs-lookup"><span data-stu-id="59fcc-226">a.</span></span> <span data-ttu-id="59fcc-227">Wprowadź hello **imię** i **E-mail** atrybuty prawidłowe konto usługi Azure Active Directory mają tooprovision w hello związane z pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="59fcc-227">Enter hello **First Name** and **Email** attributes of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="59fcc-228">b.</span><span class="sxs-lookup"><span data-stu-id="59fcc-228">b.</span></span> <span data-ttu-id="59fcc-229">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="59fcc-229">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="59fcc-230">Właściciel konta usługi Azure Active Directory Hello pobiera wiadomość e-mail z tym kontem hello tooconfirm łącze zanim staje się aktywny</span><span class="sxs-lookup"><span data-stu-id="59fcc-230">hello Azure Active Directory account holder gets an email including a link tooconfirm hello account before it becomes active</span></span>
    >  

>[!NOTE]
><span data-ttu-id="59fcc-231">Możesz użyć innych FreshService użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez FreshService tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="59fcc-231">You can use any other FreshService user account creation tools or APIs provided by FreshService tooprovision AAD user accounts.</span></span>
>  

![Przypisz użytkownika][200] 

<span data-ttu-id="59fcc-233">**tooassign tooFreshservice Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="59fcc-233">**tooassign Britta Simon tooFreshservice, perform hello following steps:**</span></span>

1. <span data-ttu-id="59fcc-234">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="59fcc-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="59fcc-236">Z listy aplikacji hello wybierz **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="59fcc-236">In hello applications list, select **Freshservice**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_app.png) 

3. <span data-ttu-id="59fcc-238">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="59fcc-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="59fcc-240">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="59fcc-240">Click **Add** button.</span></span> <span data-ttu-id="59fcc-241">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="59fcc-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="59fcc-243">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="59fcc-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="59fcc-244">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="59fcc-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="59fcc-245">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="59fcc-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="59fcc-246">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="59fcc-246">Testing single sign-on</span></span>

<span data-ttu-id="59fcc-247">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="59fcc-247">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="59fcc-248">Po kliknięciu kafelka Freshservice hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Freshservice aplikacji.</span><span class="sxs-lookup"><span data-stu-id="59fcc-248">When you click hello Freshservice tile in hello Access Panel, you should get automatically signed-on tooyour Freshservice application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="59fcc-249">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="59fcc-249">Additional resources</span></span>

* [<span data-ttu-id="59fcc-250">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59fcc-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="59fcc-251">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="59fcc-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_203.png

