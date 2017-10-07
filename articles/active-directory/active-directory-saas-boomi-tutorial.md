---
title: 'Samouczek: Integracji Azure Active Directory z Boomi | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Boomi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ce64a4561697d311a8c7b1b244315bb552c5cfb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a><span data-ttu-id="5bd0d-103">Samouczek: Integracji Azure Active Directory z Boomi</span><span class="sxs-lookup"><span data-stu-id="5bd0d-103">Tutorial: Azure Active Directory integration with Boomi</span></span>

<span data-ttu-id="5bd0d-104">Z tego samouczka, dowiesz się, jak toointegrate Boomi w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5bd0d-104">In this tutorial, you learn how toointegrate Boomi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5bd0d-105">Integracja z usługą Azure AD Boomi zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5bd0d-105">Integrating Boomi with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5bd0d-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooBoomi</span><span class="sxs-lookup"><span data-stu-id="5bd0d-106">You can control in Azure AD who has access tooBoomi</span></span>
- <span data-ttu-id="5bd0d-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooBoomi (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bd0d-107">You can enable your users tooautomatically get signed-on tooBoomi (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5bd0d-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5bd0d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5bd0d-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5bd0d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bd0d-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5bd0d-110">Prerequisites</span></span>

<span data-ttu-id="5bd0d-111">tooconfigure integracji z usługą Azure AD z Boomi należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5bd0d-111">tooconfigure Azure AD integration with Boomi, you need hello following items:</span></span>

- <span data-ttu-id="5bd0d-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bd0d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5bd0d-113">Boomi logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5bd0d-113">A Boomi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5bd0d-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5bd0d-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5bd0d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5bd0d-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5bd0d-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5bd0d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5bd0d-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5bd0d-118">Scenario description</span></span>
<span data-ttu-id="5bd0d-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5bd0d-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5bd0d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5bd0d-121">Dodawanie Boomi z galerii hello</span><span class="sxs-lookup"><span data-stu-id="5bd0d-121">Adding Boomi from hello gallery</span></span>
2. <span data-ttu-id="5bd0d-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5bd0d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-boomi-from-hello-gallery"></a><span data-ttu-id="5bd0d-123">Dodawanie Boomi z galerii hello</span><span class="sxs-lookup"><span data-stu-id="5bd0d-123">Adding Boomi from hello gallery</span></span>
<span data-ttu-id="5bd0d-124">tooconfigure hello integracji Boomi do usługi Azure AD, należy tooadd Boomi z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-124">tooconfigure hello integration of Boomi into Azure AD, you need tooadd Boomi from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5bd0d-125">**tooadd Boomi z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5bd0d-125">**tooadd Boomi from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5bd0d-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="5bd0d-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5bd0d-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="5bd0d-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="5bd0d-133">W polu wyszukiwania hello wpisz **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-133">In hello search box, type **Boomi**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. <span data-ttu-id="5bd0d-135">W panelu wyników hello zaznacz **Boomi**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-135">In hello results panel, select **Boomi**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5bd0d-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5bd0d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5bd0d-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Boomi w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-138">In this section, you configure and test Azure AD single sign-on with Boomi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5bd0d-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Boomi jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Boomi is tooa user in Azure AD.</span></span> <span data-ttu-id="5bd0d-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Boomi musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-140">In other words, a link relationship between an Azure AD user and hello related user in Boomi needs toobe established.</span></span>

<span data-ttu-id="5bd0d-141">W Boomi, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-141">In Boomi, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5bd0d-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Boomi, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="5bd0d-142">tooconfigure and test Azure AD single sign-on with Boomi, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5bd0d-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5bd0d-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5bd0d-145">**[Tworzenie użytkownika testowego Boomi](#creating-a-boomi-test-user)**  -toohave odpowiednikiem Simona Britta w Boomi, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-145">**[Creating a Boomi test user](#creating-a-boomi-test-user)** - toohave a counterpart of Britta Simon in Boomi that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5bd0d-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5bd0d-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5bd0d-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5bd0d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5bd0d-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Boomi.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Boomi application.</span></span>

<span data-ttu-id="5bd0d-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Boomi, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5bd0d-150">**tooconfigure Azure AD single sign-on with Boomi, perform hello following steps:**</span></span>

1. <span data-ttu-id="5bd0d-151">W portalu Azure na powitania hello **Boomi** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-151">In hello Azure portal, on hello **Boomi** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="5bd0d-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. <span data-ttu-id="5bd0d-155">Na powitania **Boomi domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="5bd0d-155">On hello **Boomi Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    <span data-ttu-id="5bd0d-157">a.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-157">a.</span></span> <span data-ttu-id="5bd0d-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="5bd0d-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    <span data-ttu-id="5bd0d-159">b.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-159">b.</span></span> <span data-ttu-id="5bd0d-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="5bd0d-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5bd0d-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-161">These values are not real.</span></span> <span data-ttu-id="5bd0d-162">Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="5bd0d-163">Skontaktuj się z [zespołem pomocy technicznej Boomi](https://boomi.com/company/contact/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-163">Contact [Boomi support team](https://boomi.com/company/contact/) tooget these values.</span></span>

4. <span data-ttu-id="5bd0d-164">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. <span data-ttu-id="5bd0d-166">Aplikacja Boomi oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-166">Boomi application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="5bd0d-167">Skonfiguruj powitania po oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-167">Please configure hello following claims for this application.</span></span> <span data-ttu-id="5bd0d-168">Można zarządzać hello wartości tych atrybutów z hello "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-168">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="5bd0d-169">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-169">hello following screenshot shows an example for this.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="5bd0d-171">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, dla każdego wiersza przedstawione w poniższej tabeli hello wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5bd0d-171">In hello **User Attributes** section on hello **Single sign-on** dialog, for each row shown in hello table below, perform hello following steps:</span></span>

    | <span data-ttu-id="5bd0d-172">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="5bd0d-172">Attribute Name</span></span> | <span data-ttu-id="5bd0d-173">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="5bd0d-173">Attribute Value</span></span> |
    | -------------- | --------------- |
    | <span data-ttu-id="5bd0d-174">FEDERATION_ID</span><span class="sxs-lookup"><span data-stu-id="5bd0d-174">FEDERATION_ID</span></span> | <span data-ttu-id="5bd0d-175">User.mail</span><span class="sxs-lookup"><span data-stu-id="5bd0d-175">user.mail</span></span> |
    
    <span data-ttu-id="5bd0d-176">a.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-176">a.</span></span> <span data-ttu-id="5bd0d-177">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="5bd0d-180">b.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-180">b.</span></span> <span data-ttu-id="5bd0d-181">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="5bd0d-182">c.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-182">c.</span></span> <span data-ttu-id="5bd0d-183">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="5bd0d-184">d.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-184">d.</span></span> <span data-ttu-id="5bd0d-185">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-185">Click **Ok**.</span></span>

6. <span data-ttu-id="5bd0d-186">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-186">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="5bd0d-188">Na powitania **konfiguracji Boomi** kliknij **skonfigurować Boomi** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-188">On hello **Boomi Configuration** section, click **Configure Boomi** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5bd0d-189">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="5bd0d-189">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. <span data-ttu-id="5bd0d-191">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Boomi jako administrator.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-191">In a different web browser window, log into your Boomi company site as an administrator.</span></span> 

9. <span data-ttu-id="5bd0d-192">Przejdź za**nazwa firmy** i przejść za**Konfigurowanie**.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-192">Navigate too**Company Name** and go too**Set up**.</span></span>

10. <span data-ttu-id="5bd0d-193">Kliknij przycisk hello **opcje logowania jednokrotnego** karcie i wykonaj następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-193">Click hello **SSO Options** tab and perform below steps.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    <span data-ttu-id="5bd0d-195">a.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-195">a.</span></span> <span data-ttu-id="5bd0d-196">Sprawdź **Włącz SAML logowania jednokrotnego** wyboru.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-196">Check **Enable SAML Single Sign-On** checkbox.</span></span>

    <span data-ttu-id="5bd0d-197">b.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-197">b.</span></span> <span data-ttu-id="5bd0d-198">Kliknij przycisk **importu** tooupload hello pobrać certyfikatu z usługi Azure AD za**certyfikat dostawcy tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-198">Click **Import** tooupload hello downloaded certificate from Azure AD too**Identity Provider Certificate**.</span></span>
    
    <span data-ttu-id="5bd0d-199">c.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-199">c.</span></span> <span data-ttu-id="5bd0d-200">W hello **adresu URL logowania do dostawcy tożsamości** pole tekstowe, umieść wartość hello **SAML pojedynczy znak na adres URL usługi** z okna konfiguracji aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-200">In hello **Identity Provider Login URL** textbox, put hello value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="5bd0d-201">d.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-201">d.</span></span> <span data-ttu-id="5bd0d-202">Jako **federacyjnego identyfikator lokalizacji**, wybierz pozycję **identyfikator federacyjnej jest w elemencie atrybutu FEDERATION_ID** przycisk radiowy.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-202">As **Federation Id Location**, select **Federation Id is in FEDERATION_ID Attribute element** radio button.</span></span> 

    <span data-ttu-id="5bd0d-203">e.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-203">e.</span></span> <span data-ttu-id="5bd0d-204">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-204">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="5bd0d-205">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="5bd0d-205">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5bd0d-206">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-206">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5bd0d-207">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5bd0d-207">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5bd0d-208">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bd0d-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="5bd0d-209">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-209">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="5bd0d-211">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5bd0d-211">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5bd0d-212">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-212">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5bd0d-214">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-214">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5bd0d-216">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-216">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5bd0d-218">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5bd0d-218">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5bd0d-220">a.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-220">a.</span></span> <span data-ttu-id="5bd0d-221">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-221">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5bd0d-222">b.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-222">b.</span></span> <span data-ttu-id="5bd0d-223">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-223">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5bd0d-224">c.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-224">c.</span></span> <span data-ttu-id="5bd0d-225">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-225">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5bd0d-226">d.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-226">d.</span></span> <span data-ttu-id="5bd0d-227">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-227">Click **Create**.</span></span>
 
### <a name="creating-a-boomi-test-user"></a><span data-ttu-id="5bd0d-228">Tworzenie użytkownika testowego Boomi</span><span class="sxs-lookup"><span data-stu-id="5bd0d-228">Creating a Boomi test user</span></span>

<span data-ttu-id="5bd0d-229">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable w tooBoomi muszą mieć przydzielone do Boomi.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-229">In order tooenable Azure AD users toolog in tooBoomi, they must be provisioned into Boomi.</span></span> <span data-ttu-id="5bd0d-230">W przypadku hello Boomi Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-230">In hello case of Boomi, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="5bd0d-231">tooprovision konta użytkownika, należy wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5bd0d-231">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="5bd0d-232">Zaloguj się za tooyour Boomi witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-232">Log in tooyour Boomi company site as an administrator.</span></span>

2. <span data-ttu-id="5bd0d-233">Po zalogowaniu Przejdź zbyt**Zarządzanie użytkownikami** i przejść za**użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-233">After logging in, navigate too**User Management** and go too**Users**.</span></span>

    <span data-ttu-id="5bd0d-234">![Użytkownicy](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="5bd0d-234">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Users")</span></span>

3. <span data-ttu-id="5bd0d-235">Kliknij przycisk  **+**  ikony, jak i hello **ról użytkownika Add/Zachowaj** zostanie otwarte okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-235">Click **+**  icon and hello **Add/Maintain User Roles** dialog opens.</span></span>

    <span data-ttu-id="5bd0d-236">![Użytkownicy](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="5bd0d-236">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Users")</span></span>

    <span data-ttu-id="5bd0d-237">![Użytkownicy](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="5bd0d-237">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Users")</span></span>

    <span data-ttu-id="5bd0d-238">a.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-238">a.</span></span> <span data-ttu-id="5bd0d-239">W hello **adres e-mail użytkownika** pole tekstowe, powitalne wiadomości e-mail użytkownika, takich jak BrittaSimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-239">In hello **User e-mail address** textbox, type hello email of user like BrittaSimon@contoso.com.</span></span>
    
    <span data-ttu-id="5bd0d-240">b.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-240">b.</span></span> <span data-ttu-id="5bd0d-241">W hello **imię** pole tekstowe, typ hello imię użytkownika, takich jak Britta.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-241">In hello **First name** textbox, type hello First name of user like Britta.</span></span>

    <span data-ttu-id="5bd0d-242">c.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-242">c.</span></span> <span data-ttu-id="5bd0d-243">W hello **nazwisko** pole tekstowe, typ hello nazwisko użytkownika, takich jak Simona.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-243">In hello **Last name** textbox, type hello Last name of user like Simon.</span></span>
    
    <span data-ttu-id="5bd0d-244">d.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-244">d.</span></span> <span data-ttu-id="5bd0d-245">Wprowadź nazwę użytkownika hello **identyfikator federacyjnej**.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-245">Enter hello user's **Federation ID**.</span></span> <span data-ttu-id="5bd0d-246">Każdy użytkownik musi mieć identyfikator federacyjnego, który unikatowo identyfikuje użytkownika hello w ramach konta hello.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-246">Each user must have a Federation ID that uniquely identifies hello user within hello account.</span></span>
    
    <span data-ttu-id="5bd0d-247">e.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-247">e.</span></span> <span data-ttu-id="5bd0d-248">Przypisz hello **użytkownika standardowego** użytkownika toohello roli.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-248">Assign hello **Standard User** role toohello user.</span></span> <span data-ttu-id="5bd0d-249">Nie należy przypisywać hello rolę administratora, ponieważ który spowodowałoby to nadanie mu dostęp do atmosfery, a także dostępu rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-249">Do not assign hello Administrator role because that would give him normal Atmosphere access as well as single sign-on access.</span></span>
    
    <span data-ttu-id="5bd0d-250">f.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-250">f.</span></span> <span data-ttu-id="5bd0d-251">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-251">Click **OK**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="5bd0d-252">Hello użytkownik nie otrzyma wiadomość e-mail z powiadomieniem powitalnej zawierająca hasło, które mogą być toolog używanych w toohello AtomSphere konta, ponieważ jego hasło jest zarządzane przez dostawcę tożsamości hello.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-252">hello user will not receive a welcome notification email containing a password that can be used toolog in toohello AtomSphere account because his password is managed through hello identity provider.</span></span> <span data-ttu-id="5bd0d-253">Możesz użyć innych Boomi użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Boomi tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-253">You may use any other Boomi user account creation tools or APIs provided by Boomi tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5bd0d-254">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bd0d-254">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5bd0d-255">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooBoomi.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-255">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBoomi.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="5bd0d-257">**tooassign tooBoomi Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5bd0d-257">**tooassign Britta Simon tooBoomi, perform hello following steps:**</span></span>

1. <span data-ttu-id="5bd0d-258">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-258">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5bd0d-260">Z listy aplikacji hello wybierz **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-260">In hello applications list, select **Boomi**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. <span data-ttu-id="5bd0d-262">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-262">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="5bd0d-264">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-264">Click **Add** button.</span></span> <span data-ttu-id="5bd0d-265">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="5bd0d-267">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-267">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5bd0d-268">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5bd0d-269">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5bd0d-270">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5bd0d-270">Testing single sign-on</span></span>

<span data-ttu-id="5bd0d-271">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-271">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5bd0d-272">Po kliknięciu kafelka Boomi hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Boomi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5bd0d-272">When you click hello Boomi tile in hello Access Panel, you should get automatically signed-on tooyour Boomi application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5bd0d-273">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5bd0d-273">Additional resources</span></span>

* [<span data-ttu-id="5bd0d-274">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5bd0d-274">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5bd0d-275">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5bd0d-275">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png

