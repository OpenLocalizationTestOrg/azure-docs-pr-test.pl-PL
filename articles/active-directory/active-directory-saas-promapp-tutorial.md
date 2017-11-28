---
title: 'Samouczek: Integracji Azure Active Directory z Promapp | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Promapp."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 418d0601-6e7a-4997-a683-73fa30a2cfb5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 02de7679b0c86d7aa8cacb41762f900dbf2ff231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-promapp"></a><span data-ttu-id="69fce-103">Samouczek: Integracji Azure Active Directory z Promapp</span><span class="sxs-lookup"><span data-stu-id="69fce-103">Tutorial: Azure Active Directory integration with Promapp</span></span>

<span data-ttu-id="69fce-104">Z tego samouczka, dowiesz się, jak toointegrate Promapp w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="69fce-104">In this tutorial, you learn how toointegrate Promapp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="69fce-105">Integracja z usługą Azure AD Promapp zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="69fce-105">Integrating Promapp with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="69fce-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooPromapp</span><span class="sxs-lookup"><span data-stu-id="69fce-106">You can control in Azure AD who has access tooPromapp</span></span>
- <span data-ttu-id="69fce-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooPromapp (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="69fce-107">You can enable your users tooautomatically get signed-on tooPromapp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="69fce-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="69fce-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="69fce-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="69fce-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="69fce-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="69fce-110">Prerequisites</span></span>

<span data-ttu-id="69fce-111">tooconfigure integracji z usługą Azure AD z Promapp należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="69fce-111">tooconfigure Azure AD integration with Promapp, you need hello following items:</span></span>

- <span data-ttu-id="69fce-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="69fce-112">An Azure AD subscription</span></span>
- <span data-ttu-id="69fce-113">Promapp logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="69fce-113">A Promapp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="69fce-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="69fce-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="69fce-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="69fce-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="69fce-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="69fce-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="69fce-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="69fce-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="69fce-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="69fce-118">Scenario description</span></span>
<span data-ttu-id="69fce-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="69fce-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="69fce-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="69fce-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="69fce-121">Dodawanie Promapp z galerii hello</span><span class="sxs-lookup"><span data-stu-id="69fce-121">Adding Promapp from hello gallery</span></span>
2. <span data-ttu-id="69fce-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="69fce-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-promapp-from-hello-gallery"></a><span data-ttu-id="69fce-123">Dodawanie Promapp z galerii hello</span><span class="sxs-lookup"><span data-stu-id="69fce-123">Adding Promapp from hello gallery</span></span>
<span data-ttu-id="69fce-124">tooconfigure hello integracji Promapp do usługi Azure AD, należy tooadd Promapp z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="69fce-124">tooconfigure hello integration of Promapp into Azure AD, you need tooadd Promapp from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="69fce-125">**tooadd Promapp z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="69fce-125">**tooadd Promapp from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="69fce-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="69fce-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="69fce-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="69fce-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="69fce-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="69fce-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="69fce-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="69fce-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="69fce-133">W polu wyszukiwania hello wpisz **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="69fce-133">In hello search box, type **Promapp**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_search.png)

5. <span data-ttu-id="69fce-135">W panelu wyników hello zaznacz **Promapp**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="69fce-135">In hello results panel, select **Promapp**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="69fce-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="69fce-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="69fce-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Promapp w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="69fce-138">In this section, you configure and test Azure AD single sign-on with Promapp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="69fce-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Promapp jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="69fce-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Promapp is tooa user in Azure AD.</span></span> <span data-ttu-id="69fce-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Promapp musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="69fce-140">In other words, a link relationship between an Azure AD user and hello related user in Promapp needs toobe established.</span></span>

<span data-ttu-id="69fce-141">W Promapp, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="69fce-141">In Promapp, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="69fce-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Promapp, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="69fce-142">tooconfigure and test Azure AD single sign-on with Promapp, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="69fce-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="69fce-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="69fce-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="69fce-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="69fce-145">**[Tworzenie użytkownika testowego Promapp](#creating-a-promapp-test-user)**  -toohave odpowiednikiem Simona Britta w Promapp, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="69fce-145">**[Creating a Promapp test user](#creating-a-promapp-test-user)** - toohave a counterpart of Britta Simon in Promapp that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="69fce-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="69fce-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="69fce-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="69fce-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="69fce-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="69fce-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="69fce-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Promapp.</span><span class="sxs-lookup"><span data-stu-id="69fce-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Promapp application.</span></span>

<span data-ttu-id="69fce-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Promapp, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="69fce-150">**tooconfigure Azure AD single sign-on with Promapp, perform hello following steps:**</span></span>

1. <span data-ttu-id="69fce-151">W portalu Azure na powitania hello **Promapp** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="69fce-151">In hello Azure portal, on hello **Promapp** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="69fce-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="69fce-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_samlbase.png)

3. <span data-ttu-id="69fce-155">Na powitania **Promapp domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="69fce-155">On hello **Promapp Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_url.png)

    <span data-ttu-id="69fce-157">a.</span><span class="sxs-lookup"><span data-stu-id="69fce-157">a.</span></span> <span data-ttu-id="69fce-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span><span class="sxs-lookup"><span data-stu-id="69fce-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span></span>

    <span data-ttu-id="69fce-159">b.</span><span class="sxs-lookup"><span data-stu-id="69fce-159">b.</span></span> <span data-ttu-id="69fce-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://DOMAINNAME.promapp.com/TENANTNAME`</span><span class="sxs-lookup"><span data-stu-id="69fce-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="69fce-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="69fce-161">These values are not real.</span></span> <span data-ttu-id="69fce-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="69fce-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="69fce-163">Skontaktuj się z [zespołem pomocy technicznej klienta Promapp](https://www.promapp.com/about-us/contact-us/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="69fce-163">Contact [Promapp Client support team](https://www.promapp.com/about-us/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="69fce-164">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="69fce-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_certificate.png) 

5. <span data-ttu-id="69fce-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="69fce-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-promapp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="69fce-168">Na powitania **konfiguracji Promapp** kliknij **skonfigurować Promapp** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="69fce-168">On hello **Promapp Configuration** section, click **Configure Promapp** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="69fce-169">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="69fce-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_configure.png) 

7. <span data-ttu-id="69fce-171">Logowania jednokrotnego tooyour Promapp witryna firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="69fce-171">Sign-on tooyour Promapp company site as administrator.</span></span> 

8. <span data-ttu-id="69fce-172">W menu hello na górze hello, kliknij przycisk **Admin**.</span><span class="sxs-lookup"><span data-stu-id="69fce-172">In hello menu on hello top, click **Admin**.</span></span> 
   
    ![Azure AD rejestracji jednokrotnej][12]

9. <span data-ttu-id="69fce-174">Kliknij pozycję **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="69fce-174">Click **Configure**.</span></span> 
   
    ![Azure AD rejestracji jednokrotnej][13]

10. <span data-ttu-id="69fce-176">Na powitania **zabezpieczeń** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="69fce-176">On hello **Security** dialog, perform hello following steps:</span></span>
   
    ![Azure AD rejestracji jednokrotnej][14]
    
    <span data-ttu-id="69fce-178">a.</span><span class="sxs-lookup"><span data-stu-id="69fce-178">a.</span></span> <span data-ttu-id="69fce-179">Wklej **SAML pojedynczy znak na adres URL usługi**, która została skopiowana z hello portalu Azure do hello **adres URL logowania jednokrotnego logowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="69fce-179">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **SSO-Login URL** textbox.</span></span>
    
    <span data-ttu-id="69fce-180">b.</span><span class="sxs-lookup"><span data-stu-id="69fce-180">b.</span></span> <span data-ttu-id="69fce-181">Jako **logowania jednokrotnego — tryb rejestracji jednokrotnej**, wybierz pozycję **opcjonalnie**, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="69fce-181">As **SSO - Single Sign-on Mode**, select **Optional**, and then click **Save**.</span></span>

    <span data-ttu-id="69fce-182">c.</span><span class="sxs-lookup"><span data-stu-id="69fce-182">c.</span></span> <span data-ttu-id="69fce-183">Otwórz hello pobrane certyfikatów w programie Notatnik, skopiować zawartość certyfikatu hello bez hello pierwszego wiersza (---BEGIN CERTIFICATE---) i hello ostatniego wiersza (---koniec certyfikat---), wklej go do hello **certyfikatu x.509 logowania jednokrotnego** pole tekstowe, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="69fce-183">Open hello downloaded certificate in notepad, copy hello certificate content without hello first line (-----BEGIN CERTIFICATE-----) and hello last line (-----END CERTIFICATE-----), paste it into hello **SSO-x.509 Certificate** textbox, and then click **Save**.</span></span>
        
> [!TIP]
> <span data-ttu-id="69fce-184">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="69fce-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="69fce-185">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="69fce-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="69fce-186">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="69fce-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="69fce-187">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="69fce-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="69fce-188">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="69fce-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="69fce-190">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="69fce-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="69fce-191">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="69fce-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="69fce-193">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="69fce-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="69fce-195">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="69fce-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="69fce-197">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="69fce-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="69fce-199">a.</span><span class="sxs-lookup"><span data-stu-id="69fce-199">a.</span></span> <span data-ttu-id="69fce-200">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="69fce-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="69fce-201">b.</span><span class="sxs-lookup"><span data-stu-id="69fce-201">b.</span></span> <span data-ttu-id="69fce-202">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="69fce-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="69fce-203">c.</span><span class="sxs-lookup"><span data-stu-id="69fce-203">c.</span></span> <span data-ttu-id="69fce-204">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="69fce-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="69fce-205">d.</span><span class="sxs-lookup"><span data-stu-id="69fce-205">d.</span></span> <span data-ttu-id="69fce-206">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="69fce-206">Click **Create**.</span></span>
 
### <a name="creating-a-promapp-test-user"></a><span data-ttu-id="69fce-207">Tworzenie użytkownika testowego Promapp</span><span class="sxs-lookup"><span data-stu-id="69fce-207">Creating a Promapp test user</span></span>

<span data-ttu-id="69fce-208">Witaj Promapp aplikacji obsługuje Just in Time inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="69fce-208">hello Promapp application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="69fce-209">Oznacza to konto użytkownika jest tworzony automatycznie w razie potrzeby podczas aplikacji hello tooaccess próba przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="69fce-209">This means, a user account is automatically created if necessary during an attempt tooaccess hello application using hello Access Panel.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="69fce-210">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="69fce-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="69fce-211">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooPromapp.</span><span class="sxs-lookup"><span data-stu-id="69fce-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPromapp.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="69fce-213">**tooassign tooPromapp Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="69fce-213">**tooassign Britta Simon tooPromapp, perform hello following steps:**</span></span>

1. <span data-ttu-id="69fce-214">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="69fce-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="69fce-216">Z listy aplikacji hello wybierz **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="69fce-216">In hello applications list, select **Promapp**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_app.png) 

3. <span data-ttu-id="69fce-218">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="69fce-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="69fce-220">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="69fce-220">Click **Add** button.</span></span> <span data-ttu-id="69fce-221">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="69fce-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="69fce-223">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="69fce-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="69fce-224">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="69fce-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="69fce-225">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="69fce-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="69fce-226">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="69fce-226">Testing single sign-on</span></span>

<span data-ttu-id="69fce-227">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="69fce-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="69fce-228">Po kliknięciu kafelka Promapp hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Promapp aplikacji.</span><span class="sxs-lookup"><span data-stu-id="69fce-228">When you click hello Promapp tile in hello Access Panel, you should get automatically signed-on tooyour Promapp application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="69fce-229">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="69fce-229">Additional resources</span></span>

* [<span data-ttu-id="69fce-230">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="69fce-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="69fce-231">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="69fce-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_05.png
[13]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_06.png
[14]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_07.png

[100]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_203.png

