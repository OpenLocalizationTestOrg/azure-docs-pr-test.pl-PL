---
title: "Samouczek: Integracji usługi Azure Active Directory z Dowiedz się, tablica | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Tablica Dowiedz się więcej."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b8ca505-61ea-487c-9a3e-fa50c936df0c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jeedes
ms.openlocfilehash: e94cdd6eaf876d4f66bdd783c442dc468f104e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn"></a><span data-ttu-id="bbcce-103">Samouczek: Integracji Azure Active Directory z tablica Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="bbcce-103">Tutorial: Azure Active Directory integration with Blackboard Learn</span></span>

<span data-ttu-id="bbcce-104">Z tego samouczka, dowiesz się, jak toointegrate tablica Dowiedz się więcej o usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bbcce-104">In this tutorial, you learn how toointegrate Blackboard Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bbcce-105">Integrowanie tablica Dowiedz się więcej o usłudze Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="bbcce-105">Integrating Blackboard Learn with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bbcce-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooBlackboard Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="bbcce-106">You can control in Azure AD who has access tooBlackboard Learn</span></span>
- <span data-ttu-id="bbcce-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooBlackboard informacje (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbcce-107">You can enable your users tooautomatically get signed-on tooBlackboard Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bbcce-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bbcce-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bbcce-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bbcce-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bbcce-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bbcce-110">Prerequisites</span></span>

<span data-ttu-id="bbcce-111">tooconfigure integracji usługi Azure AD z tablica Dowiedz się więcej, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="bbcce-111">tooconfigure Azure AD integration with Blackboard Learn, you need hello following items:</span></span>

- <span data-ttu-id="bbcce-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbcce-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bbcce-113">Dowiedz się, tablica logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="bbcce-113">A Blackboard Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bbcce-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="bbcce-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bbcce-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="bbcce-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bbcce-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="bbcce-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bbcce-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bbcce-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bbcce-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="bbcce-118">Scenario description</span></span>
<span data-ttu-id="bbcce-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="bbcce-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bbcce-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="bbcce-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bbcce-121">Dodawanie informacji tablica z galerii hello</span><span class="sxs-lookup"><span data-stu-id="bbcce-121">Adding Blackboard Learn from hello gallery</span></span>
2. <span data-ttu-id="bbcce-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bbcce-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn-from-hello-gallery"></a><span data-ttu-id="bbcce-123">Dodawanie informacji tablica z galerii hello</span><span class="sxs-lookup"><span data-stu-id="bbcce-123">Adding Blackboard Learn from hello gallery</span></span>
<span data-ttu-id="bbcce-124">tooconfigure hello integracji tablica informacje do usługi Azure AD, należy tooadd tablica Dowiedz się od hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="bbcce-124">tooconfigure hello integration of Blackboard Learn into Azure AD, you need tooadd Blackboard Learn from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bbcce-125">**Tablica informacje z galerii hello tooadd wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="bbcce-125">**tooadd Blackboard Learn from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bbcce-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bbcce-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="bbcce-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="bbcce-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bbcce-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bbcce-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="bbcce-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bbcce-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="bbcce-133">W polu wyszukiwania hello wpisz **Dowiedz się, tablica**.</span><span class="sxs-lookup"><span data-stu-id="bbcce-133">In hello search box, type **Blackboard Learn**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_search.png)

5. <span data-ttu-id="bbcce-135">W panelu wyników hello, wybierz **tablica Dowiedz się**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="bbcce-135">In hello results panel, select **Blackboard Learn**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bbcce-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bbcce-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bbcce-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z tablica Dowiedz się na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="bbcce-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bbcce-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow jakie hello odpowiednikiem użytkownik w Dowiedz się, tablica jest tooa w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbcce-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Blackboard Learn is tooa user in Azure AD.</span></span> <span data-ttu-id="bbcce-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w tablica Dowiedz się musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="bbcce-140">In other words, a link relationship between an Azure AD user and hello related user in Blackboard Learn needs toobe established.</span></span>

<span data-ttu-id="bbcce-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **nazwy użytkownika** w tablica Dowiedz się więcej.</span><span class="sxs-lookup"><span data-stu-id="bbcce-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Blackboard Learn.</span></span>

<span data-ttu-id="bbcce-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z tablica Dowiedz się, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="bbcce-142">tooconfigure and test Azure AD single sign-on with Blackboard Learn, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bbcce-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="bbcce-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bbcce-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bbcce-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bbcce-145">**[Tworzenie użytkownika testowego Dowiedz się, tablica](#creating-a-blackboard-learn-test-user)**  -toohave odpowiednikiem Simona Britta w tablica Dowiedz się, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bbcce-145">**[Creating a Blackboard Learn test user](#creating-a-blackboard-learn-test-user)** - toohave a counterpart of Britta Simon in Blackboard Learn that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bbcce-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="bbcce-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bbcce-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="bbcce-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bbcce-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bbcce-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bbcce-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji tablica Dowiedz się więcej.</span><span class="sxs-lookup"><span data-stu-id="bbcce-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Blackboard Learn application.</span></span>

<span data-ttu-id="bbcce-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z tablica dowiedzieć się, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="bbcce-150">**tooconfigure Azure AD single sign-on with Blackboard Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="bbcce-151">W portalu Azure na powitania hello **Dowiedz się, tablica** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="bbcce-151">In hello Azure portal, on hello **Blackboard Learn** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="bbcce-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="bbcce-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_samlbase.png)

3. <span data-ttu-id="bbcce-155">Na powitania **tablica Dowiedz się, domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="bbcce-155">On hello **Blackboard Learn Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_url.png)

    <span data-ttu-id="bbcce-157">a.</span><span class="sxs-lookup"><span data-stu-id="bbcce-157">a.</span></span> <span data-ttu-id="bbcce-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.blackboard.com/`</span><span class="sxs-lookup"><span data-stu-id="bbcce-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.blackboard.com/`</span></span>

    <span data-ttu-id="bbcce-159">b.</span><span class="sxs-lookup"><span data-stu-id="bbcce-159">b.</span></span> <span data-ttu-id="bbcce-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span><span class="sxs-lookup"><span data-stu-id="bbcce-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="bbcce-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="bbcce-161">These values are not real.</span></span> <span data-ttu-id="bbcce-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="bbcce-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="bbcce-163">Skontaktuj się z [tablica klienta Dowiedz się z pomocą techniczną](https://www.blackboard.com/support/index.aspx) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="bbcce-163">Contact [Blackboard Learn Client support team](https://www.blackboard.com/support/index.aspx) tooget these values.</span></span> 

4. <span data-ttu-id="bbcce-164">Tablica Dowiedz się więcej aplikacji oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="bbcce-164">Blackboard Learn application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="bbcce-165">Skonfiguruj powitania po oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bbcce-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="bbcce-166">Można zarządzać hello wartości tych atrybutów z hello **atrybuty użytkownika** sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bbcce-166">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span>
 <span data-ttu-id="bbcce-167">powitania po zrzut ekranu przedstawia przykład informacji na ten temat.</span><span class="sxs-lookup"><span data-stu-id="bbcce-167">hello following screenshot shows an example about it.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="bbcce-169">W hello **atrybuty użytkownika** sekcji na **logowanie jednokrotne** dialogowym Konfigurowanie atrybutów tokenu SAML, jak pokazano w obrazie hello i wykonywanie hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="bbcce-169">In hello **User Attributes** section on **Single sign-on** dialog, configure SAML token attributes as shown in hello image and perform hello following steps.</span></span> <span data-ttu-id="bbcce-170">Możemy zamapowaniu hello Userprincipalname jako atrybut unikatowego użytkownika hello w tym miejscu, ale można mapować toohello odpowiednią wartość, która odróżnia jednoznacznie hello użytkownik w organizacji hello i mapujący pole username tooBlackboard Dowiedz się więcej.</span><span class="sxs-lookup"><span data-stu-id="bbcce-170">We have mapped hello Userprincipalname as hello unique user attribute here but you can map it toohello appropriate value, which uniquely distinguishes hello user in hello organization and that maps tooBlackboard Learn username field.</span></span>
           
    | <span data-ttu-id="bbcce-171">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="bbcce-171">Attribute Name</span></span> | <span data-ttu-id="bbcce-172">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="bbcce-172">Attribute Value</span></span> |   
    | ---------------| ----------------|
    | <span data-ttu-id="bbcce-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span><span class="sxs-lookup"><span data-stu-id="bbcce-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span></span> |<span data-ttu-id="bbcce-174">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="bbcce-174">user.userprincipalname</span></span> |

    <span data-ttu-id="bbcce-175">a.</span><span class="sxs-lookup"><span data-stu-id="bbcce-175">a.</span></span> <span data-ttu-id="bbcce-176">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bbcce-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_04.png)
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="bbcce-179">b.</span><span class="sxs-lookup"><span data-stu-id="bbcce-179">b.</span></span> <span data-ttu-id="bbcce-180">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="bbcce-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="bbcce-181">c.</span><span class="sxs-lookup"><span data-stu-id="bbcce-181">c.</span></span> <span data-ttu-id="bbcce-182">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="bbcce-182">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="bbcce-183">d.</span><span class="sxs-lookup"><span data-stu-id="bbcce-183">d.</span></span> <span data-ttu-id="bbcce-184">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="bbcce-184">Click **Ok**.</span></span>

4. <span data-ttu-id="bbcce-185">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="bbcce-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_certificate.png)

7. <span data-ttu-id="bbcce-187">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bbcce-187">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="bbcce-189">Na powitania **tablica informacje konfiguracji** kliknij **skonfigurować tablica Dowiedz się,** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="bbcce-189">On hello **Blackboard Learn Configuration** section, click **Configure Blackboard Learn** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bbcce-190">Kopiuj hello **SAML identyfikator jednostki** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="bbcce-190">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_configure.png) 

9. <span data-ttu-id="bbcce-192">tooconfigure rejestracji jednokrotnej w **tablica Dowiedz się** strony, należy pobrać hello toosend **XML metadanych** i **identyfikator jednostki SAML** zbyt[tablica Dowiedz się więcej obsługuje](https://www.blackboard.com/support/index.aspx).</span><span class="sxs-lookup"><span data-stu-id="bbcce-192">tooconfigure single sign-on on **Blackboard Learn** side, you need toosend hello downloaded **Metadata XML** and **SAML Entity ID** too[Blackboard Learn support](https://www.blackboard.com/support/index.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="bbcce-193">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="bbcce-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bbcce-194">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="bbcce-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bbcce-195">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bbcce-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bbcce-196">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbcce-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="bbcce-197">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="bbcce-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="bbcce-199">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="bbcce-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bbcce-200">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bbcce-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bbcce-202">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="bbcce-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bbcce-204">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bbcce-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bbcce-206">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="bbcce-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bbcce-208">a.</span><span class="sxs-lookup"><span data-stu-id="bbcce-208">a.</span></span> <span data-ttu-id="bbcce-209">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bbcce-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bbcce-210">b.</span><span class="sxs-lookup"><span data-stu-id="bbcce-210">b.</span></span> <span data-ttu-id="bbcce-211">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bbcce-211">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="bbcce-212">c.</span><span class="sxs-lookup"><span data-stu-id="bbcce-212">c.</span></span> <span data-ttu-id="bbcce-213">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="bbcce-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bbcce-214">d.</span><span class="sxs-lookup"><span data-stu-id="bbcce-214">d.</span></span> <span data-ttu-id="bbcce-215">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="bbcce-215">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn-test-user"></a><span data-ttu-id="bbcce-216">Tworzenie użytkownika testowego tablica Dowiedz się więcej.</span><span class="sxs-lookup"><span data-stu-id="bbcce-216">Creating a Blackboard Learn test user</span></span>
<span data-ttu-id="bbcce-217">W tej sekcji można utworzyć użytkownika o nazwie Simona Britta w tablica Dowiedz się więcej.</span><span class="sxs-lookup"><span data-stu-id="bbcce-217">In this section, you create a user called Britta Simon in Blackboard Learn.</span></span> 

<span data-ttu-id="bbcce-218">Tablica Dowiedz się aplikacja obsługuje tylko w czasie Inicjowanie obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="bbcce-218">Blackboard Learn application support just in time user provisioning.</span></span> <span data-ttu-id="bbcce-219">Upewnij się, że skonfigurowano hello oświadczenia zgodnie z opisem w sekcji hello  **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**</span><span class="sxs-lookup"><span data-stu-id="bbcce-219">Make sure that you have configured hello claims as described in hello section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span></span>
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bbcce-220">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbcce-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bbcce-221">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooBlackboard Dowiedz się więcej.</span><span class="sxs-lookup"><span data-stu-id="bbcce-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlackboard Learn.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="bbcce-223">**tooassign tooBlackboard Simona Britta Dowiedz się więcej, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="bbcce-223">**tooassign Britta Simon tooBlackboard Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="bbcce-224">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bbcce-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="bbcce-226">Z listy aplikacji hello wybierz **Dowiedz się, tablica**.</span><span class="sxs-lookup"><span data-stu-id="bbcce-226">In hello applications list, select **Blackboard Learn**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_app.png) 

3. <span data-ttu-id="bbcce-228">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="bbcce-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="bbcce-230">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bbcce-230">Click **Add** button.</span></span> <span data-ttu-id="bbcce-231">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bbcce-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="bbcce-233">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="bbcce-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bbcce-234">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bbcce-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bbcce-235">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bbcce-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bbcce-236">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bbcce-236">Testing single sign-on</span></span>

<span data-ttu-id="bbcce-237">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="bbcce-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bbcce-238">Po kliknięciu kafelka hello tablica Dowiedz się więcej w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Dowiedz się, tablica aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bbcce-238">When you click hello Blackboard Learn tile in hello Access Panel, you should get automatically signed-on tooyour Blackboard Learn application.</span></span> <span data-ttu-id="bbcce-239">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bbcce-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bbcce-240">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="bbcce-240">Additional resources</span></span>

* [<span data-ttu-id="bbcce-241">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bbcce-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bbcce-242">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bbcce-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_203.png

