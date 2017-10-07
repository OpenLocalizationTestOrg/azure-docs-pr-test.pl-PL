---
title: 'Samouczek: Integracji Azure Active Directory z Zoho | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Zoho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 5d1c196d3b97babab196f509ea68e7d61523a7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a><span data-ttu-id="44872-103">Samouczek: Integracji Azure Active Directory z Zoho</span><span class="sxs-lookup"><span data-stu-id="44872-103">Tutorial: Azure Active Directory integration with Zoho</span></span>

<span data-ttu-id="44872-104">Z tego samouczka, dowiesz się, jak toointegrate Zoho w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="44872-104">In this tutorial, you learn how toointegrate Zoho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="44872-105">Integracja z usługą Azure AD Zoho zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="44872-105">Integrating Zoho with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="44872-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooZoho.</span><span class="sxs-lookup"><span data-stu-id="44872-106">You can control in Azure AD who has access tooZoho.</span></span>
- <span data-ttu-id="44872-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooZoho (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44872-107">You can enable your users tooautomatically get signed-on tooZoho (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="44872-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="44872-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="44872-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="44872-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44872-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="44872-110">Prerequisites</span></span>

<span data-ttu-id="44872-111">tooconfigure integracji z usługą Azure AD z Zoho należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="44872-111">tooconfigure Azure AD integration with Zoho, you need hello following items:</span></span>

- <span data-ttu-id="44872-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="44872-112">An Azure AD subscription</span></span>
- <span data-ttu-id="44872-113">Zoho logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="44872-113">A Zoho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="44872-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="44872-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="44872-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="44872-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="44872-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="44872-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="44872-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="44872-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="44872-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="44872-118">Scenario description</span></span>
<span data-ttu-id="44872-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="44872-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="44872-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="44872-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="44872-121">Dodawanie Zoho z galerii hello</span><span class="sxs-lookup"><span data-stu-id="44872-121">Adding Zoho from hello gallery</span></span>
2. <span data-ttu-id="44872-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="44872-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoho-from-hello-gallery"></a><span data-ttu-id="44872-123">Dodawanie Zoho z galerii hello</span><span class="sxs-lookup"><span data-stu-id="44872-123">Adding Zoho from hello gallery</span></span>
<span data-ttu-id="44872-124">tooconfigure hello integracji Zoho do usługi Azure AD, należy tooadd Zoho z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="44872-124">tooconfigure hello integration of Zoho into Azure AD, you need tooadd Zoho from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="44872-125">**tooadd Zoho z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="44872-125">**tooadd Zoho from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="44872-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="44872-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="44872-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="44872-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="44872-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="44872-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="44872-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44872-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="44872-133">W polu wyszukiwania hello wpisz **Zoho**, wybierz pozycję **Zoho** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="44872-133">In hello search box, type **Zoho**, select **Zoho** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Zoho hello listy wyników](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="44872-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="44872-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="44872-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Zoho w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="44872-136">In this section, you configure and test Azure AD single sign-on with Zoho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="44872-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Zoho jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44872-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zoho is tooa user in Azure AD.</span></span> <span data-ttu-id="44872-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Zoho musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="44872-138">In other words, a link relationship between an Azure AD user and hello related user in Zoho needs toobe established.</span></span>

<span data-ttu-id="44872-139">W Zoho, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="44872-139">In Zoho, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="44872-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Zoho, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="44872-140">tooconfigure and test Azure AD single sign-on with Zoho, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="44872-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="44872-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="44872-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="44872-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="44872-143">**[Tworzenie użytkownika testowego Zoho](#create-a-zoho-test-user)**  -toohave odpowiednikiem Simona Britta w Zoho, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="44872-143">**[Create a Zoho test user](#create-a-zoho-test-user)** - toohave a counterpart of Britta Simon in Zoho that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="44872-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="44872-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="44872-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="44872-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="44872-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="44872-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="44872-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Zoho.</span><span class="sxs-lookup"><span data-stu-id="44872-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zoho application.</span></span>

<span data-ttu-id="44872-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Zoho, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="44872-148">**tooconfigure Azure AD single sign-on with Zoho, perform hello following steps:**</span></span>

1. <span data-ttu-id="44872-149">W portalu Azure na powitania hello **Zoho** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="44872-149">In hello Azure portal, on hello **Zoho** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="44872-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="44872-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. <span data-ttu-id="44872-153">Na powitania **Zoho domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="44872-153">On hello **Zoho Domain and URLs** section, perform hello following steps:</span></span>

    ![Adresy URL i domeny Zoho pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    <span data-ttu-id="44872-155">a.</span><span class="sxs-lookup"><span data-stu-id="44872-155">a.</span></span> <span data-ttu-id="44872-156">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.zohomail.com`</span><span class="sxs-lookup"><span data-stu-id="44872-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.zohomail.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="44872-157">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="44872-157">This value is not real.</span></span> <span data-ttu-id="44872-158">Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="44872-158">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="44872-159">Skontaktuj się z [zespołem pomocy technicznej klienta Zoho](https://www.zoho.com/mail/contact.html) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="44872-159">Contact [Zoho Client support team](https://www.zoho.com/mail/contact.html) tooget this value.</span></span> 
 
4. <span data-ttu-id="44872-160">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="44872-160">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. <span data-ttu-id="44872-162">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="44872-162">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="44872-164">Na powitania **konfiguracji Zoho** kliknij **skonfigurować Zoho** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="44872-164">On hello **Zoho Configuration** section, click **Configure Zoho** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="44872-165">Kopiuj hello **Sign-Out adres URL, Zmień adres URL hasła i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="44872-165">Copy hello **Sign-Out URL, Change Password URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfiguracja Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. <span data-ttu-id="44872-167">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy poczty Zoho jako administrator.</span><span class="sxs-lookup"><span data-stu-id="44872-167">In a different web browser window, log into your Zoho Mail company site as an administrator.</span></span>

8. <span data-ttu-id="44872-168">Przejdź toohello **Panelu sterowania**.</span><span class="sxs-lookup"><span data-stu-id="44872-168">Go toohello **Control panel**.</span></span>
   
    <span data-ttu-id="44872-169">![Panel sterowania](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Panel sterowania")</span><span class="sxs-lookup"><span data-stu-id="44872-169">![Control Panel](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Control Panel")</span></span>

9. <span data-ttu-id="44872-170">Kliknij przycisk hello **uwierzytelnianie SAML** kartę.</span><span class="sxs-lookup"><span data-stu-id="44872-170">Click hello **SAML Authentication** tab.</span></span>
   
    <span data-ttu-id="44872-171">![Uwierzytelnianie SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "uwierzytelnianie SAML")</span><span class="sxs-lookup"><span data-stu-id="44872-171">![SAML Authentication](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML Authentication")</span></span>

10. <span data-ttu-id="44872-172">W hello **Szczegóły okna uwierzytelnianie SAML** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="44872-172">In hello **SAML Authentication Details** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="44872-173">![Szczegóły okna uwierzytelnianie SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "Szczegóły okna uwierzytelnianie SAML")</span><span class="sxs-lookup"><span data-stu-id="44872-173">![SAML Authentication Details](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML Authentication Details")</span></span>
   
    <span data-ttu-id="44872-174">a.</span><span class="sxs-lookup"><span data-stu-id="44872-174">a.</span></span> <span data-ttu-id="44872-175">W hello **adres URL logowania** pole tekstowe, Wklej **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="44872-175">In hello **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="44872-176">b.</span><span class="sxs-lookup"><span data-stu-id="44872-176">b.</span></span> <span data-ttu-id="44872-177">W hello **adresu URL wylogowania** pole tekstowe, Wklej **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="44872-177">In hello **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="44872-178">c.</span><span class="sxs-lookup"><span data-stu-id="44872-178">c.</span></span> <span data-ttu-id="44872-179">W hello **Zmień adres URL hasła** pole tekstowe, Wklej **Zmień adres URL hasła** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="44872-179">In hello **Change Password URL** textbox, paste **Change Password URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="44872-180">d.</span><span class="sxs-lookup"><span data-stu-id="44872-180">d.</span></span> <span data-ttu-id="44872-181">Otwórz base-64 zakodowany certyfikat pobrany z portalu Azure w programie Notatnik hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **PublicKey** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="44872-181">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **PublicKey** textbox.</span></span>
   
    <span data-ttu-id="44872-182">e.</span><span class="sxs-lookup"><span data-stu-id="44872-182">e.</span></span> <span data-ttu-id="44872-183">Jako **algorytm**, wybierz pozycję **RSA**.</span><span class="sxs-lookup"><span data-stu-id="44872-183">As **Algorithm**, select **RSA**.</span></span>
   
    <span data-ttu-id="44872-184">f.</span><span class="sxs-lookup"><span data-stu-id="44872-184">f.</span></span> <span data-ttu-id="44872-185">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="44872-185">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="44872-186">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="44872-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="44872-187">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="44872-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="44872-188">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="44872-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="44872-189">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="44872-189">Create an Azure AD test user</span></span>

<span data-ttu-id="44872-190">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="44872-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="44872-192">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="44872-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="44872-193">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="44872-193">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="44872-195">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="44872-195">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="44872-197">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="44872-197">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="44872-199">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="44872-199">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    <span data-ttu-id="44872-201">a.</span><span class="sxs-lookup"><span data-stu-id="44872-201">a.</span></span> <span data-ttu-id="44872-202">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="44872-202">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="44872-203">b.</span><span class="sxs-lookup"><span data-stu-id="44872-203">b.</span></span> <span data-ttu-id="44872-204">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="44872-204">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="44872-205">c.</span><span class="sxs-lookup"><span data-stu-id="44872-205">c.</span></span> <span data-ttu-id="44872-206">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="44872-206">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="44872-207">d.</span><span class="sxs-lookup"><span data-stu-id="44872-207">d.</span></span> <span data-ttu-id="44872-208">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="44872-208">Click **Create**.</span></span>
 
### <a name="create-a-zoho-test-user"></a><span data-ttu-id="44872-209">Tworzenie użytkownika testowego Zoho</span><span class="sxs-lookup"><span data-stu-id="44872-209">Create a Zoho test user</span></span>

<span data-ttu-id="44872-210">W kolejności tooenable usługi Azure AD użytkownicy toolog do Zoho poczty musi być przygotowana do Zoho poczty.</span><span class="sxs-lookup"><span data-stu-id="44872-210">In order tooenable Azure AD users toolog into Zoho Mail, they must be provisioned into Zoho Mail.</span></span> <span data-ttu-id="44872-211">W przypadku hello Zoho poczty Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="44872-211">In hello case of Zoho Mail, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="44872-212">Możesz użyć innych Zoho poczty użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision poczty Zoho kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="44872-212">You can use any other Zoho Mail user account creation tools or APIs provided by Zoho Mail tooprovision AAD user accounts.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="44872-213">tooprovision konta użytkownika, należy wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="44872-213">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="44872-214">Zaloguj się za tooyour **poczty Zoho** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="44872-214">Log in tooyour **Zoho Mail** company site as an administrator.</span></span>

2. <span data-ttu-id="44872-215">Przejdź za**Panelu sterowania \> poczty & Docs**.</span><span class="sxs-lookup"><span data-stu-id="44872-215">Go too**Control Panel \> Mail & Docs**.</span></span>

3. <span data-ttu-id="44872-216">Przejdź za**szczegóły użytkownika \> Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="44872-216">Go too**User Details \> Add User**.</span></span>
   
    <span data-ttu-id="44872-217">![Dodaj użytkownika](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="44872-217">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Add User")</span></span>

4. <span data-ttu-id="44872-218">Na powitania **dodawania użytkowników** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="44872-218">On hello **Add users** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="44872-219">![Dodaj użytkownika](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="44872-219">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Add User")</span></span>
   
    <span data-ttu-id="44872-220">a.</span><span class="sxs-lookup"><span data-stu-id="44872-220">a.</span></span> <span data-ttu-id="44872-221">W hello **imię** pole tekstowe, typ hello imię użytkownika, takich jak **Britta**.</span><span class="sxs-lookup"><span data-stu-id="44872-221">In hello **First Name** textbox, type hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="44872-222">b.</span><span class="sxs-lookup"><span data-stu-id="44872-222">b.</span></span> <span data-ttu-id="44872-223">W hello **nazwisko** pole tekstowe, typ hello nazwisko użytkownika, takich jak **Simona**.</span><span class="sxs-lookup"><span data-stu-id="44872-223">In hello **Last Name** textbox, type hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="44872-224">c.</span><span class="sxs-lookup"><span data-stu-id="44872-224">c.</span></span> <span data-ttu-id="44872-225">W hello **identyfikator wiadomości E-mail** pole tekstowe, identyfikator wiadomości e-mail hello typu użytkownika, takich jak  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="44872-225">In hello **Email ID** textbox, type hello email id of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="44872-226">d.</span><span class="sxs-lookup"><span data-stu-id="44872-226">d.</span></span> <span data-ttu-id="44872-227">W hello **hasło** pole tekstowe, wprowadź hasło użytkownika.</span><span class="sxs-lookup"><span data-stu-id="44872-227">In hello **Password** textbox, enter password of user.</span></span>
   
    <span data-ttu-id="44872-228">e.</span><span class="sxs-lookup"><span data-stu-id="44872-228">e.</span></span> <span data-ttu-id="44872-229">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="44872-229">Click **OK**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="44872-230">Właściciel konta usługi Azure Active Directory Hello otrzymają wiadomość e-mail przy użyciu konta hello tooconfirm łącza, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="44872-230">hello Azure Active Directory account holder will receive an email with a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="44872-231">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="44872-231">Assign hello Azure AD test user</span></span>

<span data-ttu-id="44872-232">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooZoho.</span><span class="sxs-lookup"><span data-stu-id="44872-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZoho.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="44872-234">**tooassign tooZoho Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="44872-234">**tooassign Britta Simon tooZoho, perform hello following steps:**</span></span>

1. <span data-ttu-id="44872-235">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="44872-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="44872-237">Z listy aplikacji hello wybierz **Zoho**.</span><span class="sxs-lookup"><span data-stu-id="44872-237">In hello applications list, select **Zoho**.</span></span>

    ![łącze Zoho Hello na liście aplikacji hello](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. <span data-ttu-id="44872-239">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="44872-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="44872-241">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="44872-241">Click **Add** button.</span></span> <span data-ttu-id="44872-242">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44872-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="44872-244">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="44872-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="44872-245">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44872-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="44872-246">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44872-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="44872-247">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="44872-247">Test single sign-on</span></span>

<span data-ttu-id="44872-248">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="44872-248">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="44872-249">Po kliknięciu kafelka Zoho hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Zoho aplikacji.</span><span class="sxs-lookup"><span data-stu-id="44872-249">When you click hello Zoho tile in hello Access Panel, you should get automatically signed-on tooyour Zoho application.</span></span>
<span data-ttu-id="44872-250">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="44872-250">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="44872-251">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="44872-251">Additional resources</span></span>

* [<span data-ttu-id="44872-252">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="44872-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="44872-253">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="44872-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_203.png

