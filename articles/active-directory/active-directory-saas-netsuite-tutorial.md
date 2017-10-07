---
title: 'Samouczek: Integracji Azure Active Directory z Netsuite | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7cf205d5bda5333872fb589e57f4779a8670b595
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a><span data-ttu-id="eda32-103">Samouczek: Integracji Azure Active Directory z Netsuite</span><span class="sxs-lookup"><span data-stu-id="eda32-103">Tutorial: Azure Active Directory integration with Netsuite</span></span>

<span data-ttu-id="eda32-104">Z tego samouczka, dowiesz się, jak toointegrate Netsuite w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eda32-104">In this tutorial, you learn how toointegrate Netsuite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eda32-105">Integracja z usługą Azure AD Netsuite zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="eda32-105">Integrating Netsuite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eda32-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooNetsuite</span><span class="sxs-lookup"><span data-stu-id="eda32-106">You can control in Azure AD who has access tooNetsuite</span></span>
- <span data-ttu-id="eda32-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooNetsuite (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="eda32-107">You can enable your users tooautomatically get signed-on tooNetsuite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eda32-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="eda32-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="eda32-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eda32-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eda32-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="eda32-110">Prerequisites</span></span>

<span data-ttu-id="eda32-111">tooconfigure integracji z usługą Azure AD z Netsuite należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="eda32-111">tooconfigure Azure AD integration with Netsuite, you need hello following items:</span></span>

- <span data-ttu-id="eda32-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="eda32-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eda32-113">Netsuite jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="eda32-113">A Netsuite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eda32-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="eda32-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eda32-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="eda32-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eda32-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="eda32-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eda32-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eda32-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eda32-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="eda32-118">Scenario description</span></span>
<span data-ttu-id="eda32-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="eda32-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eda32-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="eda32-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eda32-121">Dodawanie Netsuite z galerii hello</span><span class="sxs-lookup"><span data-stu-id="eda32-121">Adding Netsuite from hello gallery</span></span>
2. <span data-ttu-id="eda32-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="eda32-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netsuite-from-hello-gallery"></a><span data-ttu-id="eda32-123">Dodawanie Netsuite z galerii hello</span><span class="sxs-lookup"><span data-stu-id="eda32-123">Adding Netsuite from hello gallery</span></span>
<span data-ttu-id="eda32-124">tooconfigure hello integracji Netsuite do usługi Azure AD, należy tooadd Netsuite z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="eda32-124">tooconfigure hello integration of Netsuite into Azure AD, you need tooadd Netsuite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eda32-125">**tooadd Netsuite z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="eda32-125">**tooadd Netsuite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eda32-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="eda32-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="eda32-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="eda32-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eda32-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="eda32-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="eda32-131">Kliknij przycisk **nowej aplikacji** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eda32-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="eda32-133">W polu wyszukiwania hello wpisz **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="eda32-133">In hello search box, type **Netsuite**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. <span data-ttu-id="eda32-135">W panelu wyników hello zaznacz **Netsuite**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="eda32-135">In hello results panel, select **Netsuite**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eda32-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="eda32-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eda32-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Netsuite na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="eda32-138">In this section, you configure and test Azure AD single sign-on with Netsuite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="eda32-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Netsuite jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eda32-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Netsuite is tooa user in Azure AD.</span></span> <span data-ttu-id="eda32-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Netsuite musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="eda32-140">In other words, a link relationship between an Azure AD user and hello related user in Netsuite needs toobe established.</span></span>

<span data-ttu-id="eda32-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Netsuite.</span><span class="sxs-lookup"><span data-stu-id="eda32-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Netsuite.</span></span>

<span data-ttu-id="eda32-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Netsuite, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="eda32-142">tooconfigure and test Azure AD single sign-on with Netsuite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eda32-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="eda32-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eda32-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="eda32-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eda32-145">**[Tworzenie użytkownika testowego Netsuite](#creating-a-netsuite-test-user)**  -toohave odpowiednikiem Simona Britta w Netsuite, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="eda32-145">**[Creating a Netsuite test user](#creating-a-netsuite-test-user)** - toohave a counterpart of Britta Simon in Netsuite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="eda32-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="eda32-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eda32-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="eda32-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eda32-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="eda32-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eda32-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Netsuite.</span><span class="sxs-lookup"><span data-stu-id="eda32-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Netsuite application.</span></span>

<span data-ttu-id="eda32-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Netsuite, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="eda32-150">**tooconfigure Azure AD single sign-on with Netsuite, perform hello following steps:**</span></span>

1. <span data-ttu-id="eda32-151">W portalu Azure na powitania hello **Netsuite** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="eda32-151">In hello Azure portal, on hello **Netsuite** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="eda32-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="eda32-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. <span data-ttu-id="eda32-155">Na powitania **Netsuite domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="eda32-155">On hello **Netsuite Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    <span data-ttu-id="eda32-157">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs``https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span><span class="sxs-lookup"><span data-stu-id="eda32-157">In hello **Reply URL** textbox, type a URL using hello following pattern:   `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="eda32-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="eda32-158">This value is not real value.</span></span> <span data-ttu-id="eda32-159">Wartość hello aktualizacji z hello rzeczywisty adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="eda32-159">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="eda32-160">Skontaktuj się z [zespołem pomocy technicznej Netsuite](http://www.netsuite.com/portal/services/support.shtml) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="eda32-160">Contact [Netsuite support team](http://www.netsuite.com/portal/services/support.shtml) tooget this value.</span></span>
 
4. <span data-ttu-id="eda32-161">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="eda32-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. <span data-ttu-id="eda32-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="eda32-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eda32-165">Na powitania **konfiguracji Netsuite** kliknij **skonfigurować Netsuite** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="eda32-165">On hello **Netsuite Configuration** section, click **Configure Netsuite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="eda32-166">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="eda32-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. <span data-ttu-id="eda32-168">Otwórz nową kartę w przeglądarce i zaloguj się do witryny firmy Netsuite jako administrator.</span><span class="sxs-lookup"><span data-stu-id="eda32-168">Open a new tab in your browser, and sign into your Netsuite company site as an administrator.</span></span>

8. <span data-ttu-id="eda32-169">Hello pasku narzędzi u góry hello hello strony, kliknij przycisk **Instalator**, następnie kliknij przycisk **Menedżer instalacji**.</span><span class="sxs-lookup"><span data-stu-id="eda32-169">In hello toolbar at hello top of hello page, click **Setup**, then click **Setup Manager**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. <span data-ttu-id="eda32-171">Z hello **zadań konfiguracyjnych** listy, wybierz **integracji**.</span><span class="sxs-lookup"><span data-stu-id="eda32-171">From hello **Setup Tasks** list, select **Integration**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. <span data-ttu-id="eda32-173">W hello **Zarządzanie uwierzytelniania** kliknij **SAML logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="eda32-173">In hello **Manage Authentication** section, click **SAML Single Sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. <span data-ttu-id="eda32-175">Na powitania **Instalatora SAML** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="eda32-175">On hello **SAML Setup** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="eda32-176">a.</span><span class="sxs-lookup"><span data-stu-id="eda32-176">a.</span></span> <span data-ttu-id="eda32-177">Kopia hello **SAML pojedynczy znak na adres URL usługi** wartość z **krótkimi opisami** sekcji **Konfigurowanie logowania jednokrotnego** i wklej go do hello **dostawcy tożsamości Strona logowania** w Netsuite.</span><span class="sxs-lookup"><span data-stu-id="eda32-177">Copy hello **SAML Single Sign-On Service URL** value from **Quick Reference** section of **Configure sign-on** and paste it into hello **Identity Provider Login Page** field in Netsuite.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    <span data-ttu-id="eda32-179">b.</span><span class="sxs-lookup"><span data-stu-id="eda32-179">b.</span></span> <span data-ttu-id="eda32-180">Netsuite, wybierz **podstawowej metody uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="eda32-180">In Netsuite, select **Primary Authentication Method**.</span></span>

    <span data-ttu-id="eda32-181">c.</span><span class="sxs-lookup"><span data-stu-id="eda32-181">c.</span></span> <span data-ttu-id="eda32-182">Dla pola hello etykietą **metadanych dostawcy tożsamości SAMLV2**, wybierz pozycję **Przekaż plik metadanych IDP**.</span><span class="sxs-lookup"><span data-stu-id="eda32-182">For hello field labeled **SAMLV2 Identity Provider Metadata**, select **Upload IDP Metadata File**.</span></span> <span data-ttu-id="eda32-183">Następnie kliknij przycisk **Przeglądaj** tooupload hello metadanych pliku, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="eda32-183">Then click **Browse** tooupload hello metadata file that you downloaded from Azure portal.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    <span data-ttu-id="eda32-185">d.</span><span class="sxs-lookup"><span data-stu-id="eda32-185">d.</span></span> <span data-ttu-id="eda32-186">Kliknij przycisk **przesłać**.</span><span class="sxs-lookup"><span data-stu-id="eda32-186">Click **Submit**.</span></span>

12. <span data-ttu-id="eda32-187">W usłudze Azure AD, kliknij **widoku i edytować wszystkie atrybuty użytkowników** pole wyboru i dodać atrybut.</span><span class="sxs-lookup"><span data-stu-id="eda32-187">In Azure AD, Click on **View and edit all other user attributes** check-box and add attribute.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. <span data-ttu-id="eda32-189">Dla hello **nazwa atrybutu** wpisz w `account`.</span><span class="sxs-lookup"><span data-stu-id="eda32-189">For hello **Attribute Name** field, type in `account`.</span></span> <span data-ttu-id="eda32-190">Dla hello **wartość atrybutu** wpisz w identyfikatora konta Netsuite Ta wartość jest stała i zmianę konta.</span><span class="sxs-lookup"><span data-stu-id="eda32-190">For hello **Attribute Value** field, type in your Netsuite account ID.This value is constant and change with account.</span></span> <span data-ttu-id="eda32-191">Instrukcje dotyczące toofind identyfikator konta znajdują się poniżej:</span><span class="sxs-lookup"><span data-stu-id="eda32-191">Instructions on how toofind your account ID are included below:</span></span>

      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    <span data-ttu-id="eda32-193">a.</span><span class="sxs-lookup"><span data-stu-id="eda32-193">a.</span></span> <span data-ttu-id="eda32-194">W Netsuite, kliknij przycisk **Instalator** menu górnym menu nawigacyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="eda32-194">In Netsuite, click **Setup** from hello top navigation menu.</span></span>

    <span data-ttu-id="eda32-195">b.</span><span class="sxs-lookup"><span data-stu-id="eda32-195">b.</span></span> <span data-ttu-id="eda32-196">Kliknięcie w obszarze hello **zadań konfiguracyjnych** sekcji hello menu nawigacji po lewej stronie, wybierz opcję hello **integracji** sekcji, a następnie kliknij polecenie **preferencje usług sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="eda32-196">Then click under hello **Setup Tasks** section of hello left navigation menu, select hello **Integration** section, and click **Web Services Preferences**.</span></span>

    <span data-ttu-id="eda32-197">c.</span><span class="sxs-lookup"><span data-stu-id="eda32-197">c.</span></span> <span data-ttu-id="eda32-198">Identyfikator konta Netsuite skopiuj i wklej go do hello **wartość atrybutu** pole w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eda32-198">Copy your Netsuite Account ID and paste it into hello **Attribute Value** field in Azure AD.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. <span data-ttu-id="eda32-200">Zanim użytkownicy mogą wykonywać logowania jednokrotnego do Netsuite, ich należy przypisać odpowiednie uprawnienia hello w Netsuite.</span><span class="sxs-lookup"><span data-stu-id="eda32-200">Before users can perform single sign-on into Netsuite, they must first be assigned hello appropriate permissions in Netsuite.</span></span> <span data-ttu-id="eda32-201">Wykonaj instrukcje hello poniżej tooassign te uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="eda32-201">Follow hello instructions below tooassign these permissions.</span></span>

    <span data-ttu-id="eda32-202">a.</span><span class="sxs-lookup"><span data-stu-id="eda32-202">a.</span></span> <span data-ttu-id="eda32-203">W menu górnym menu nawigacyjnym powitania kliknij **Instalator**, następnie kliknij przycisk **Menedżer instalacji**.</span><span class="sxs-lookup"><span data-stu-id="eda32-203">On hello top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="eda32-205">b.</span><span class="sxs-lookup"><span data-stu-id="eda32-205">b.</span></span> <span data-ttu-id="eda32-206">W menu nawigacji po lewej stronie powitania wybierz **użytkownicy i role**, następnie kliknij przycisk **Zarządzanie rolami**.</span><span class="sxs-lookup"><span data-stu-id="eda32-206">On hello left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span></span>
      
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    <span data-ttu-id="eda32-208">c.</span><span class="sxs-lookup"><span data-stu-id="eda32-208">c.</span></span> <span data-ttu-id="eda32-209">Kliknij przycisk **nową rolę**.</span><span class="sxs-lookup"><span data-stu-id="eda32-209">Click **New Role**.</span></span>

    <span data-ttu-id="eda32-210">d.</span><span class="sxs-lookup"><span data-stu-id="eda32-210">d.</span></span> <span data-ttu-id="eda32-211">Wpisz w **nazwa** nową rolę i wybierz hello **pojedynczego logowania tylko** wyboru.</span><span class="sxs-lookup"><span data-stu-id="eda32-211">Type in a **Name** for your new role, and select hello **Single Sign-On Only** checkbox.</span></span>
      
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    <span data-ttu-id="eda32-213">e.</span><span class="sxs-lookup"><span data-stu-id="eda32-213">e.</span></span> <span data-ttu-id="eda32-214">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="eda32-214">Click **Save**.</span></span>

    <span data-ttu-id="eda32-215">f.</span><span class="sxs-lookup"><span data-stu-id="eda32-215">f.</span></span> <span data-ttu-id="eda32-216">W menu hello na górze hello, kliknij przycisk **uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="eda32-216">In hello menu on hello top, click **Permissions**.</span></span> <span data-ttu-id="eda32-217">Następnie kliknij przycisk **Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="eda32-217">Then click **Setup**.</span></span>
      
       ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    <span data-ttu-id="eda32-219">g.</span><span class="sxs-lookup"><span data-stu-id="eda32-219">g.</span></span> <span data-ttu-id="eda32-220">Wybierz **ustawić się SAM rejestracji jednokrotnej**, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="eda32-220">Select **Set Up SAM Single Sign-on**, and then click **Add**.</span></span>

    <span data-ttu-id="eda32-221">h.</span><span class="sxs-lookup"><span data-stu-id="eda32-221">h.</span></span> <span data-ttu-id="eda32-222">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="eda32-222">Click **Save**.</span></span>

    <span data-ttu-id="eda32-223">i.</span><span class="sxs-lookup"><span data-stu-id="eda32-223">i.</span></span> <span data-ttu-id="eda32-224">W menu górnym menu nawigacyjnym powitania kliknij **Instalator**, następnie kliknij przycisk **Menedżer instalacji**.</span><span class="sxs-lookup"><span data-stu-id="eda32-224">On hello top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
       ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="eda32-226">j.</span><span class="sxs-lookup"><span data-stu-id="eda32-226">j.</span></span> <span data-ttu-id="eda32-227">W menu nawigacji po lewej stronie powitania wybierz **użytkownicy i role**, następnie kliknij przycisk **Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="eda32-227">On hello left navigation menu, select **Users/Roles**, then click **Manage Users**.</span></span>
      
       ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    <span data-ttu-id="eda32-229">k.</span><span class="sxs-lookup"><span data-stu-id="eda32-229">k.</span></span> <span data-ttu-id="eda32-230">Wybierz użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="eda32-230">Select a test user.</span></span> <span data-ttu-id="eda32-231">Następnie kliknij przycisk **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="eda32-231">Then click **Edit**.</span></span>
      
       ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    <span data-ttu-id="eda32-233">l.</span><span class="sxs-lookup"><span data-stu-id="eda32-233">l.</span></span> <span data-ttu-id="eda32-234">W oknie dialogowym ról hello, wybierz rolę hello, które zostały utworzone i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="eda32-234">On hello Roles dialog, select hello role that you have created and click **Add**.</span></span>
      
       ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    <span data-ttu-id="eda32-236">m.</span><span class="sxs-lookup"><span data-stu-id="eda32-236">m.</span></span> <span data-ttu-id="eda32-237">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="eda32-237">Click **Save**.</span></span>
    
> [!TIP]
> <span data-ttu-id="eda32-238">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="eda32-238">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="eda32-239">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="eda32-239">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="eda32-240">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eda32-240">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eda32-241">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="eda32-241">Creating an Azure AD test user</span></span>
<span data-ttu-id="eda32-242">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="eda32-242">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="eda32-244">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="eda32-244">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eda32-245">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="eda32-245">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="eda32-247">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="eda32-247">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eda32-249">U góry okna dialogowego hello hello, kliknij przycisk **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eda32-249">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eda32-251">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="eda32-251">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eda32-253">a.</span><span class="sxs-lookup"><span data-stu-id="eda32-253">a.</span></span> <span data-ttu-id="eda32-254">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eda32-254">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eda32-255">b.</span><span class="sxs-lookup"><span data-stu-id="eda32-255">b.</span></span> <span data-ttu-id="eda32-256">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eda32-256">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eda32-257">c.</span><span class="sxs-lookup"><span data-stu-id="eda32-257">c.</span></span> <span data-ttu-id="eda32-258">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="eda32-258">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="eda32-259">d.</span><span class="sxs-lookup"><span data-stu-id="eda32-259">d.</span></span> <span data-ttu-id="eda32-260">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="eda32-260">Click **Create**.</span></span> 

### <a name="creating-a-netsuite-test-user"></a><span data-ttu-id="eda32-261">Tworzenie użytkownika testowego Netsuite</span><span class="sxs-lookup"><span data-stu-id="eda32-261">Creating a Netsuite test user</span></span>

<span data-ttu-id="eda32-262">W tej sekcji użytkownika o nazwie Simona Britta jest tworzony w Netsuite.</span><span class="sxs-lookup"><span data-stu-id="eda32-262">In this section, a user called Britta Simon is created in Netsuite.</span></span> <span data-ttu-id="eda32-263">Netsuite obsługę w czasie, który jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="eda32-263">Netsuite supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="eda32-264">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="eda32-264">There is no action item for you in this section.</span></span> <span data-ttu-id="eda32-265">Jeśli użytkownik nie istnieje w Netsuite, tworzona jest nowy, podczas próby tooaccess Netsuite.</span><span class="sxs-lookup"><span data-stu-id="eda32-265">If a user doesn't already exist in Netsuite, a new one is created when you attempt tooaccess Netsuite.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="eda32-266">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="eda32-266">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="eda32-267">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="eda32-267">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNetsuite.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="eda32-269">**tooassign tooNetsuite Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="eda32-269">**tooassign Britta Simon tooNetsuite, perform hello following steps:**</span></span>

1. <span data-ttu-id="eda32-270">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="eda32-270">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="eda32-272">Z listy aplikacji hello wybierz **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="eda32-272">In hello applications list, select **Netsuite**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. <span data-ttu-id="eda32-274">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="eda32-274">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="eda32-276">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="eda32-276">Click **Add** button.</span></span> <span data-ttu-id="eda32-277">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eda32-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="eda32-279">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="eda32-279">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eda32-280">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eda32-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eda32-281">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eda32-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eda32-282">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="eda32-282">Testing single sign-on</span></span>

<span data-ttu-id="eda32-283">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="eda32-283">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="eda32-284">tootest pojedynczego logowania jednokrotnego ustawienia, otwórz hello panelu dostępu pod adresem [https://myapps.microsoft.com](https://myapps.microsoft.com/), zaloguj się do konta testowego hello i kliknij przycisk **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="eda32-284">tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into hello test account, and click **Netsuite**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eda32-285">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="eda32-285">Additional resources</span></span>

* [<span data-ttu-id="eda32-286">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eda32-286">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eda32-287">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="eda32-287">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="eda32-288">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="eda32-288">Configure User Provisioning</span></span>](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

