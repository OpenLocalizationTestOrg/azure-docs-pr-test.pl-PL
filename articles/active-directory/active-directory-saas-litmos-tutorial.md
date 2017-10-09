---
title: 'Samouczek: Integracji Azure Active Directory z Litmos | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Litmos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: jeedes
ms.assetid: cfaae4bb-e8e5-41d1-ac88-8cc369653036
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 026fd10058760f2d63d185ef4aa9d7de3b82525e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-litmos"></a><span data-ttu-id="0bf8e-103">Samouczek: Integracji Azure Active Directory z Litmos</span><span class="sxs-lookup"><span data-stu-id="0bf8e-103">Tutorial: Azure Active Directory integration with Litmos</span></span>

<span data-ttu-id="0bf8e-104">Z tego samouczka, dowiesz się, jak toointegrate Litmos w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0bf8e-104">In this tutorial, you learn how toointegrate Litmos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0bf8e-105">Integracja z usługą Azure AD Litmos zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="0bf8e-105">Integrating Litmos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0bf8e-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooLitmos.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-106">You can control in Azure AD who has access tooLitmos.</span></span>
- <span data-ttu-id="0bf8e-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooLitmos (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-107">You can enable your users tooautomatically get signed-on tooLitmos (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0bf8e-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="0bf8e-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0bf8e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0bf8e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0bf8e-110">Prerequisites</span></span>

<span data-ttu-id="0bf8e-111">tooconfigure integracji z usługą Azure AD z Litmos należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="0bf8e-111">tooconfigure Azure AD integration with Litmos, you need hello following items:</span></span>

- <span data-ttu-id="0bf8e-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0bf8e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0bf8e-113">Litmos logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="0bf8e-113">A Litmos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0bf8e-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0bf8e-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="0bf8e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0bf8e-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0bf8e-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0bf8e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0bf8e-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="0bf8e-118">Scenario description</span></span>
<span data-ttu-id="0bf8e-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0bf8e-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="0bf8e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0bf8e-121">Dodawanie Litmos z galerii hello</span><span class="sxs-lookup"><span data-stu-id="0bf8e-121">Adding Litmos from hello gallery</span></span>
2. <span data-ttu-id="0bf8e-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="0bf8e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-litmos-from-hello-gallery"></a><span data-ttu-id="0bf8e-123">Dodawanie Litmos z galerii hello</span><span class="sxs-lookup"><span data-stu-id="0bf8e-123">Adding Litmos from hello gallery</span></span>
<span data-ttu-id="0bf8e-124">tooconfigure hello integracji Litmos do usługi Azure AD, należy tooadd Litmos z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-124">tooconfigure hello integration of Litmos into Azure AD, you need tooadd Litmos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0bf8e-125">**tooadd Litmos z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0bf8e-125">**tooadd Litmos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0bf8e-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="0bf8e-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0bf8e-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="0bf8e-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="0bf8e-133">W polu wyszukiwania hello wpisz **Litmos**, wybierz pozycję **Litmos** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-133">In hello search box, type **Litmos**, select **Litmos** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Litmos hello listy wyników](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0bf8e-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0bf8e-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0bf8e-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Litmos w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-136">In this section, you configure and test Azure AD single sign-on with Litmos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0bf8e-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Litmos jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Litmos is tooa user in Azure AD.</span></span> <span data-ttu-id="0bf8e-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Litmos musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-138">In other words, a link relationship between an Azure AD user and hello related user in Litmos needs toobe established.</span></span>

<span data-ttu-id="0bf8e-139">W Litmos, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-139">In Litmos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0bf8e-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Litmos, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="0bf8e-140">tooconfigure and test Azure AD single sign-on with Litmos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0bf8e-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0bf8e-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0bf8e-143">**[Tworzenie użytkownika testowego Litmos](#create-a-litmos-test-user)**  -toohave odpowiednikiem Simona Britta w Litmos, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-143">**[Create a Litmos test user](#create-a-litmos-test-user)** - toohave a counterpart of Britta Simon in Litmos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0bf8e-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0bf8e-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0bf8e-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0bf8e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0bf8e-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Litmos.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Litmos application.</span></span>

<span data-ttu-id="0bf8e-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Litmos, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0bf8e-148">**tooconfigure Azure AD single sign-on with Litmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="0bf8e-149">W portalu Azure na powitania hello **Litmos** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-149">In hello Azure portal, on hello **Litmos** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="0bf8e-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_samlbase.png)

3. <span data-ttu-id="0bf8e-153">Na powitania **Litmos domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="0bf8e-153">On hello **Litmos Domain and URLs** section, perform hello following steps:</span></span>

    ![Adresy URL i domeny Litmos pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_url.png)

    <span data-ttu-id="0bf8e-155">a.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-155">a.</span></span> <span data-ttu-id="0bf8e-156">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.litmos.com/account/Login`</span><span class="sxs-lookup"><span data-stu-id="0bf8e-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.litmos.com/account/Login`</span></span>

    <span data-ttu-id="0bf8e-157">b.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-157">b.</span></span> <span data-ttu-id="0bf8e-158">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.litmos.com/integration/samllogin`</span><span class="sxs-lookup"><span data-stu-id="0bf8e-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.litmos.com/integration/samllogin`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0bf8e-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-159">These values are not real.</span></span> <span data-ttu-id="0bf8e-160">Zaktualizować te wartości hello rzeczywisty identyfikator i odpowiedzi adresu URL, które opisano szczegółowo w dalszej części samouczka lub skontaktuj się z [Litmos obsługuje zespołu](https://www.litmos.com/contact-us/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-160">Update these values with hello actual Identifier and Reply URL, which are explained later in tutorial or contact [Litmos support team](https://www.litmos.com/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="0bf8e-161">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_certificate.png)

5. <span data-ttu-id="0bf8e-163">W ramach konfiguracji hello, potrzebujesz toocustomize hello **atrybuty tokenu SAML** Litmos aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-163">As part of hello configuration, you need toocustomize hello **SAML Token Attributes** for your Litmos application.</span></span>

    ![Atrybut sekcji](./media/active-directory-saas-litmos-tutorial/tutorial_attribute.png)
           
    | <span data-ttu-id="0bf8e-165">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="0bf8e-165">Attribute Name</span></span>   | <span data-ttu-id="0bf8e-166">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="0bf8e-166">Attribute Value</span></span> |   
    | ---------------  | ----------------|
    | <span data-ttu-id="0bf8e-167">Imię</span><span class="sxs-lookup"><span data-stu-id="0bf8e-167">FirstName</span></span> |<span data-ttu-id="0bf8e-168">User.givenName</span><span class="sxs-lookup"><span data-stu-id="0bf8e-168">user.givenname</span></span> |
    | <span data-ttu-id="0bf8e-169">Nazwisko</span><span class="sxs-lookup"><span data-stu-id="0bf8e-169">LastName</span></span>  |<span data-ttu-id="0bf8e-170">User.surname</span><span class="sxs-lookup"><span data-stu-id="0bf8e-170">user.surname</span></span> |
    | <span data-ttu-id="0bf8e-171">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="0bf8e-171">Email</span></span> |<span data-ttu-id="0bf8e-172">User.mail</span><span class="sxs-lookup"><span data-stu-id="0bf8e-172">user.mail</span></span> |

    <span data-ttu-id="0bf8e-173">a.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-173">a.</span></span> <span data-ttu-id="0bf8e-174">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-174">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Dodaj atrybut](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_04.png)

    ![Dodaj atrybut Dailog](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="0bf8e-177">b.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-177">b.</span></span> <span data-ttu-id="0bf8e-178">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="0bf8e-179">c.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-179">c.</span></span> <span data-ttu-id="0bf8e-180">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-180">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="0bf8e-181">d.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-181">d.</span></span> <span data-ttu-id="0bf8e-182">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-182">Click **Ok**.</span></span>     

6. <span data-ttu-id="0bf8e-183">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-183">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-litmos-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="0bf8e-185">W oknie innej przeglądarki, witryny firmy Litmos tooyour logowania jako administrator.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-185">In a different browser window, sign-on tooyour Litmos company site as administrator.</span></span>

8. <span data-ttu-id="0bf8e-186">W hello pasku nawigacyjnym po lewej stronie powitania kliknij **kont**.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-186">In hello navigation bar on hello left side, click **Accounts**.</span></span>
   
    ![Sekcja kont na stronie aplikacji][22] 

9. <span data-ttu-id="0bf8e-188">Kliknij przycisk hello **integracji** kartę.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-188">Click hello **Integrations** tab.</span></span>
   
    ![Karta Integracja][23] 

10. <span data-ttu-id="0bf8e-190">Na powitania **integracji** karcie, przewiń w dół za**3 integracji strona**, a następnie kliknij przycisk **SAML 2.0** kartę.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-190">On hello **Integrations** tab, scroll down too**3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0 sekcji][24] 

11. <span data-ttu-id="0bf8e-192">Kopiuj wartość hello w obszarze **hello SAML punktu końcowego jest litmos:** i wklej go do hello **adres URL odpowiedzi** textbox w hello **Litmos domeny i adres URL** sekcji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-192">Copy hello value under **hello SAML endpoint for litmos is:** and paste it into hello **Reply URL** textbox in hello **Litmos Domain and URLs** section in Azure portal.</span></span> 
   
    ![Punkt końcowy SAML][26] 

12. <span data-ttu-id="0bf8e-194">W Twojej **Litmos** aplikacji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="0bf8e-194">In your **Litmos** application, perform hello following steps:</span></span>
    
     ![Litmos aplikacji][25] 
     
     <span data-ttu-id="0bf8e-196">a.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-196">a.</span></span> <span data-ttu-id="0bf8e-197">Kliknij przycisk **Włącz SAML**.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-197">Click **Enable SAML**.</span></span>
    
     <span data-ttu-id="0bf8e-198">b.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-198">b.</span></span> <span data-ttu-id="0bf8e-199">Otwieranie certyfikatu zakodowanego base-64 w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu X.509 SAML** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-199">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **SAML X.509 Certificate** textbox.</span></span>
     
     <span data-ttu-id="0bf8e-200">c.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-200">c.</span></span> <span data-ttu-id="0bf8e-201">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-201">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="0bf8e-202">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="0bf8e-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0bf8e-203">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0bf8e-204">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0bf8e-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0bf8e-205">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0bf8e-205">Create an Azure AD test user</span></span>

<span data-ttu-id="0bf8e-206">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="0bf8e-208">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0bf8e-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0bf8e-209">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-litmos-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="0bf8e-211">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-litmos-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="0bf8e-213">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-litmos-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="0bf8e-215">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0bf8e-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-litmos-tutorial/create_aaduser_04.png)

    <span data-ttu-id="0bf8e-217">a.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-217">a.</span></span> <span data-ttu-id="0bf8e-218">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0bf8e-219">b.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-219">b.</span></span> <span data-ttu-id="0bf8e-220">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="0bf8e-221">c.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-221">c.</span></span> <span data-ttu-id="0bf8e-222">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="0bf8e-223">d.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-223">d.</span></span> <span data-ttu-id="0bf8e-224">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-224">Click **Create**.</span></span>
  
### <a name="create-a-litmos-test-user"></a><span data-ttu-id="0bf8e-225">Tworzenie użytkownika testowego Litmos</span><span class="sxs-lookup"><span data-stu-id="0bf8e-225">Create a Litmos test user</span></span>

<span data-ttu-id="0bf8e-226">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Litmos.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-226">hello objective of this section is toocreate a user called Britta Simon in Litmos.</span></span>  
<span data-ttu-id="0bf8e-227">Witaj Litmos aplikacji obsługuje Just in Time inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-227">hello Litmos application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="0bf8e-228">Oznacza to konto użytkownika jest tworzony automatycznie w razie potrzeby podczas aplikacji hello tooaccess próba przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-228">This means, a user account is automatically created if necessary during an attempt tooaccess hello application using hello Access Panel.</span></span>

<span data-ttu-id="0bf8e-229">**toocreate użytkownika o nazwie Simona Britta w Litmos, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0bf8e-229">**toocreate a user called Britta Simon in Litmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="0bf8e-230">W oknie innej przeglądarki, witryny firmy Litmos tooyour logowania jako administrator.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-230">In a different browser window, sign-on tooyour Litmos company site as administrator.</span></span>

2. <span data-ttu-id="0bf8e-231">W hello pasku nawigacyjnym po lewej stronie powitania kliknij **kont**.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-231">In hello navigation bar on hello left side, click **Accounts**.</span></span>
   
    ![Sekcja kont na stronie aplikacji][22] 

3. <span data-ttu-id="0bf8e-233">Kliknij przycisk hello **integracji** kartę.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-233">Click hello **Integrations** tab.</span></span>
   
    ![Karta integracji][23] 

4. <span data-ttu-id="0bf8e-235">Na powitania **integracji** karcie, przewiń w dół za**3 integracji strona**, a następnie kliknij przycisk **SAML 2.0** kartę.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-235">On hello **Integrations** tab, scroll down too**3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0][24] 
    
5. <span data-ttu-id="0bf8e-237">Wybierz **Autogenerate użytkowników**</span><span class="sxs-lookup"><span data-stu-id="0bf8e-237">Select **Autogenerate Users**</span></span>
   
    ![Automatyczne generowanie użytkowników][27] 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="0bf8e-239">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0bf8e-239">Assign hello Azure AD test user</span></span>

<span data-ttu-id="0bf8e-240">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooLitmos.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLitmos.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="0bf8e-242">**tooassign tooLitmos Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="0bf8e-242">**tooassign Britta Simon tooLitmos, perform hello following steps:**</span></span>

1. <span data-ttu-id="0bf8e-243">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="0bf8e-245">Z listy aplikacji hello wybierz **Litmos**.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-245">In hello applications list, select **Litmos**.</span></span>

    ![łącze Litmos Hello na liście aplikacji hello](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_app.png)  

3. <span data-ttu-id="0bf8e-247">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="0bf8e-249">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-249">Click **Add** button.</span></span> <span data-ttu-id="0bf8e-250">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="0bf8e-252">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0bf8e-253">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0bf8e-254">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0bf8e-255">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0bf8e-255">Test single sign-on</span></span>

<span data-ttu-id="0bf8e-256">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-256">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="0bf8e-257">Po kliknięciu powitalne Litmos kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Litmos aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0bf8e-257">When you click hello Litmos tile in hello Access Panel, you should get automatically signed-on tooyour Litmos application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0bf8e-258">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="0bf8e-258">Additional resources</span></span>

* [<span data-ttu-id="0bf8e-259">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0bf8e-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0bf8e-260">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0bf8e-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_04.png
[21]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_60.png
[22]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_61.png
[23]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_62.png
[24]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_63.png
[25]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_64.png
[26]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_65.png
[27]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_66.png

[100]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_203.png

