---
title: 'Samouczek: Integracji Azure Active Directory z piaskownicy Salesforce | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i usług Salesforce piaskownicy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7539f08356568a17ebfcee2764bbbefa129b0553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="d6364-103">Samouczek: Integracji Azure Active Directory z piaskownicy usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="d6364-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="d6364-104">Z tego samouczka, dowiesz się, jak toointegrate piaskownicy usługi Salesforce z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d6364-104">In this tutorial, you learn how toointegrate Salesforce Sandbox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d6364-105">Integrowanie piaskownicy usługi Salesforce z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d6364-105">Integrating Salesforce Sandbox with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d6364-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooSalesforce piaskownicy</span><span class="sxs-lookup"><span data-stu-id="d6364-106">You can control in Azure AD who has access tooSalesforce Sandbox</span></span>
- <span data-ttu-id="d6364-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSalesforce piaskownicy (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6364-107">You can enable your users tooautomatically get signed-on tooSalesforce Sandbox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d6364-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d6364-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d6364-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d6364-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6364-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d6364-110">Prerequisites</span></span>

<span data-ttu-id="d6364-111">tooconfigure integracji usługi Azure AD z piaskownicy Salesforce należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d6364-111">tooconfigure Azure AD integration with Salesforce Sandbox, you need hello following items:</span></span>

- <span data-ttu-id="d6364-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6364-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d6364-113">Piaskownica Salesforce jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d6364-113">A Salesforce Sandbox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d6364-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d6364-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d6364-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d6364-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d6364-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d6364-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d6364-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d6364-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d6364-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d6364-118">Scenario description</span></span>
<span data-ttu-id="d6364-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d6364-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d6364-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d6364-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d6364-121">Dodawanie piaskownicy usługi Salesforce z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d6364-121">Adding Salesforce Sandbox from hello gallery</span></span>
2. <span data-ttu-id="d6364-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d6364-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-sandbox-from-hello-gallery"></a><span data-ttu-id="d6364-123">Dodawanie piaskownicy usługi Salesforce z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d6364-123">Adding Salesforce Sandbox from hello gallery</span></span>
<span data-ttu-id="d6364-124">tooconfigure hello integracji piaskownicy usługi Salesforce z usługą Azure AD, należy tooadd piaskownicy usługi Salesforce z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d6364-124">tooconfigure hello integration of Salesforce Sandbox into Azure AD, you need tooadd Salesforce Sandbox from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d6364-125">**tooadd piaskownicy usługi Salesforce z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d6364-125">**tooadd Salesforce Sandbox from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d6364-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d6364-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="d6364-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="d6364-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d6364-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d6364-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="d6364-131">Kliknij przycisk **nowej aplikacji** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d6364-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="d6364-133">W polu wyszukiwania hello wpisz **piaskownicy Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="d6364-133">In hello search box, type **Salesforce Sandbox**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. <span data-ttu-id="d6364-135">W panelu wyników hello, wybierz **piaskownicy Salesforce**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d6364-135">In hello results panel, select **Salesforce Sandbox**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d6364-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d6364-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d6364-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z piaskownicy Salesforce oparte na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="d6364-138">In this section, you configure and test Azure AD single sign-on with Salesforce Sandbox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d6364-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w piaskownicy Salesforce jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6364-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Salesforce Sandbox is tooa user in Azure AD.</span></span> <span data-ttu-id="d6364-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w piaskownicy Salesforce musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="d6364-140">In other words, a link relationship between an Azure AD user and hello related user in Salesforce Sandbox needs toobe established.</span></span>

<span data-ttu-id="d6364-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w piaskownicy Salesforce.</span><span class="sxs-lookup"><span data-stu-id="d6364-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Salesforce Sandbox.</span></span>

<span data-ttu-id="d6364-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z piaskownicy Salesforce, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d6364-142">tooconfigure and test Azure AD single sign-on with Salesforce Sandbox, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d6364-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d6364-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d6364-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d6364-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d6364-145">**[Tworzenie użytkownika testowego piaskownicy Salesforce](#creating-a-salesforce-sandbox-test-user)**  -toohave odpowiednikiem Simona Britta w piaskownicy Salesforce, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d6364-145">**[Creating a Salesforce Sandbox test user](#creating-a-salesforce-sandbox-test-user)** - toohave a counterpart of Britta Simon in Salesforce Sandbox that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d6364-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d6364-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d6364-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="d6364-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d6364-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d6364-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d6364-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Salesforce piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="d6364-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Salesforce Sandbox application.</span></span>

<span data-ttu-id="d6364-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z piaskownicy Salesforce, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d6364-150">**tooconfigure Azure AD single sign-on with Salesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="d6364-151">W portalu Azure na powitania hello **piaskownicy Salesforce** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="d6364-151">In hello Azure portal, on hello **Salesforce Sandbox** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="d6364-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d6364-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. <span data-ttu-id="d6364-155">Na powitania **Salesforce piaskownicy domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d6364-155">On hello **Salesforce Sandbox Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     <span data-ttu-id="d6364-157">W hello **adres URL logowania** pole tekstowe, wartość hello typu przy użyciu hello następującego wzorca:`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="d6364-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<subdomain>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d6364-158">Ta wartość nie jest prawdziwe hello.</span><span class="sxs-lookup"><span data-stu-id="d6364-158">This value is not hello real.</span></span> <span data-ttu-id="d6364-159">Zaktualizuj tę wartość przy hello rzeczywisty adres URL logowania. Skontaktuj się z [zespołem pomocy technicznej klienta piaskownicy Salesforce](https://help.salesforce.com/support) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="d6364-159">Update this value with hello actual Sign-on URL.Contact [Salesforce Sandbox Client support team](https://help.salesforce.com/support) tooget this value.</span></span>


4. <span data-ttu-id="d6364-160">Jeśli skonfigurowano już program rejestracji jednokrotnej dla innego wystąpienia usług Salesforce piaskownicy w katalogu, a następnie należy także skonfigurować hello **identyfikator** toohave hello tę samą wartość jak hello **Zaloguj się na adres URL**.</span><span class="sxs-lookup"><span data-stu-id="d6364-160">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure hello **Identifier** toohave hello same value as hello **Sign on URL**.</span></span> 
    
    >[!Note]
    ><span data-ttu-id="d6364-161">Witaj **identyfikator** pola można znaleźć, sprawdzając hello **Pokaż zaawansowane ustawienia** wyboru na powitania **Konfigurowanie adresu URL aplikacji** stronę hello okna dialogowego</span><span class="sxs-lookup"><span data-stu-id="d6364-161">hello **Identifier** field can be found by checking hello **Show advanced settings** checkbox on hello **Configure App URL** page of hello dialog</span></span> 


5. <span data-ttu-id="d6364-162">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d6364-162">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. <span data-ttu-id="d6364-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d6364-164">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="d6364-166">Na powitania **konfiguracji piaskownicy Salesforce** kliknij **skonfigurować piaskownicy Salesforce** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="d6364-166">On hello **Salesforce Sandbox Configuration** section, click **Configure Salesforce Sandbox** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d6364-167">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="d6364-167">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="d6364-168">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="d6364-168">![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span></span>
8. <span data-ttu-id="d6364-169">Otwórz nową kartę w przeglądarce i zaloguj tooyour konto administratora usług Salesforce piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="d6364-169">Open a new tab in your browser and log in tooyour Salesforce Sandbox administrator account.</span></span>

9. <span data-ttu-id="d6364-170">W menu hello na górze hello, kliknij przycisk **Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="d6364-170">In hello menu on hello top, click **Setup**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. <span data-ttu-id="d6364-172">W okienku nawigacji hello po lewej stronie powitania kliknij **kontroli bezpieczeństwa**, a następnie kliknij przycisk **ustawień rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="d6364-172">In hello navigation pane on hello left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. <span data-ttu-id="d6364-174">Na hello w sekcji Ustawienia rejestracji jednokrotnej, wykonaj następujące kroki hello: ![skonfigurować logowanie jednokrotne](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span><span class="sxs-lookup"><span data-stu-id="d6364-174">On hello Single Sign-On Settings section, perform hello following steps:  ![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span></span>
     
     <span data-ttu-id="d6364-175">a.</span><span class="sxs-lookup"><span data-stu-id="d6364-175">a.</span></span>  <span data-ttu-id="d6364-176">Wybierz **SAML włączone**.</span><span class="sxs-lookup"><span data-stu-id="d6364-176">Select **SAML Enabled**.</span></span> 

     <span data-ttu-id="d6364-177">b.</span><span class="sxs-lookup"><span data-stu-id="d6364-177">b.</span></span>  <span data-ttu-id="d6364-178">Kliknij przycisk **Nowy**.</span><span class="sxs-lookup"><span data-stu-id="d6364-178">Click **New**.</span></span>

12. <span data-ttu-id="d6364-179">Witaj SAML pojedynczy znak w sekcji Ustawienia wykonywanie hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d6364-179">On hello SAML Single Sign-On Settings section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    <span data-ttu-id="d6364-181">pole tekstowe Nazwa hello a.In, hello nazwę typu konfiguracji hello (np.: *SPSSOWAAD\_testu*).</span><span class="sxs-lookup"><span data-stu-id="d6364-181">a.In hello Name textbox, type hello name of hello configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 

    <span data-ttu-id="d6364-182">b.</span><span class="sxs-lookup"><span data-stu-id="d6364-182">b.</span></span> <span data-ttu-id="d6364-183">Wklej **identyfikator jednostki SMAL** wartości do hello **wystawcy** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="d6364-183">Paste **SMAL Entity ID** value into hello **Issuer** textbox.</span></span>

    <span data-ttu-id="d6364-184">c.</span><span class="sxs-lookup"><span data-stu-id="d6364-184">c.</span></span> <span data-ttu-id="d6364-185">W hello **identyfikator jednostki** pole tekstowe, typ **https://test.salesforce.com** przypadku hello pierwszego wystąpienia usług Salesforce piaskownicy dodajesz tooyour katalogu.</span><span class="sxs-lookup"><span data-stu-id="d6364-185">In hello **Entity Id** textbox, type **https://test.salesforce.com** if it is hello first Salesforce Sandbox instance that you are adding tooyour directory.</span></span> <span data-ttu-id="d6364-186">Jeśli masz już dodany wystąpienia usług Salesforce piaskownicy, a następnie dla hello **identyfikator jednostki** typu w hello **na adres URL logowania**, która powinna być w następującym formacie:`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="d6364-186">If you have already added an instance of Salesforce Sandbox, then for hello **Entity ID** type in hello **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>  
 
    <span data-ttu-id="d6364-187">d.</span><span class="sxs-lookup"><span data-stu-id="d6364-187">d.</span></span> <span data-ttu-id="d6364-188">Kliknij przycisk **Przeglądaj** tooupload hello pobrać certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="d6364-188">Click **Browse** tooupload hello downloaded certificate.</span></span>  

    <span data-ttu-id="d6364-189">e.</span><span class="sxs-lookup"><span data-stu-id="d6364-189">e.</span></span> <span data-ttu-id="d6364-190">Jako **typ tożsamości SAML**, wybierz pozycję **potwierdzenia zawiera hello identyfikator federacyjnej z obiektu użytkownika hello**.</span><span class="sxs-lookup"><span data-stu-id="d6364-190">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>
 
    <span data-ttu-id="d6364-191">f.</span><span class="sxs-lookup"><span data-stu-id="d6364-191">f.</span></span> <span data-ttu-id="d6364-192">Jako **lokalizacji tożsamości SAML**, wybierz pozycję **jest tożsamość w elemencie NameIdentifier hello hello instrukcji podmiotu**.</span><span class="sxs-lookup"><span data-stu-id="d6364-192">As **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>

    <span data-ttu-id="d6364-193">g.</span><span class="sxs-lookup"><span data-stu-id="d6364-193">g.</span></span> <span data-ttu-id="d6364-194">Wklej **pojedynczy znak na adres URL usługi** do hello **adresu URL logowania do dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="d6364-194">Paste **Single Sign-On Service URL** into hello **Identity Provider Login URL** textbox.</span></span> 

    <span data-ttu-id="d6364-195">h.</span><span class="sxs-lookup"><span data-stu-id="d6364-195">h.</span></span> <span data-ttu-id="d6364-196">SFDC nie obsługuje SAML wylogowania.</span><span class="sxs-lookup"><span data-stu-id="d6364-196">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="d6364-197">Jako obejście, Wklej "https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0" go do hello **adres URL wylogowania dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="d6364-197">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="d6364-198">i.</span><span class="sxs-lookup"><span data-stu-id="d6364-198">i.</span></span> <span data-ttu-id="d6364-199">Jako **dostawcy zainicjował żądanie powiązania usługi**, wybierz pozycję **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="d6364-199">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 

    <span data-ttu-id="d6364-200">j.</span><span class="sxs-lookup"><span data-stu-id="d6364-200">j.</span></span> <span data-ttu-id="d6364-201">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="d6364-201">Click **Save**.</span></span>

### <a name="enable-your-domain"></a><span data-ttu-id="d6364-202">Włącz domeny</span><span class="sxs-lookup"><span data-stu-id="d6364-202">Enable your domain</span></span>
<span data-ttu-id="d6364-203">W tej sekcji założono, że już utworzono domeny.</span><span class="sxs-lookup"><span data-stu-id="d6364-203">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="d6364-204">Aby uzyskać więcej informacji, zobacz [Definiowanie Twojej nazwy domeny](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="d6364-204">For more information, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="d6364-205">**tooenable domeny, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d6364-205">**tooenable your domain, perform hello following steps:**</span></span>

1. <span data-ttu-id="d6364-206">W okienku nawigacji po lewej stronie powitania kliknij **Zarządzanie domenami**, a następnie kliknij przycisk **Moje domeny.**</span><span class="sxs-lookup"><span data-stu-id="d6364-206">In hello left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   ><span data-ttu-id="d6364-208">Upewnij się, że poprawnie skonfigurowano domenę.</span><span class="sxs-lookup"><span data-stu-id="d6364-208">Please make sure that your domain has been configured correctly.</span></span> 

2. <span data-ttu-id="d6364-209">W hello **ustawienia strony logowania** , kliknij przycisk **Edytuj**, następnie jako **usługi uwierzytelniania**, wybierz nazwę hello hello SAML pojedynczego logowania jednokrotnego ustawienia z poprzednich hello sekcja, a na koniec kliknij **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="d6364-209">In hello **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select hello name of hello SAML Single Sign-On Setting from hello previous section, and finally click **Save**.</span></span>
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

<span data-ttu-id="d6364-211">Jak masz domenę skonfigurowane, użytkownicy należy używać hello domeny adres URL toologin toohello Salesforce piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="d6364-211">As soon as you have a domain configured, your users should use hello domain URL toologin toohello Salesforce sandbox.</span></span>  

<span data-ttu-id="d6364-212">wartość hello tooget hello adresu URL, kliknij profil rejestracji Jednokrotnej hello, utworzony w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="d6364-212">tooget hello value of hello URL, click hello SSO profile you have created in hello previous section.</span></span>    

> [!TIP]
> <span data-ttu-id="d6364-213">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="d6364-213">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d6364-214">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="d6364-214">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d6364-215">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d6364-215">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d6364-216">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6364-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="d6364-217">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="d6364-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="d6364-219">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d6364-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d6364-220">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d6364-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d6364-222">toodisplay hello listę użytkowników przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d6364-222">toodisplay hello list of users go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d6364-224">U góry okna dialogowego hello hello, kliknij przycisk **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d6364-224">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d6364-226">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d6364-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d6364-228">a.</span><span class="sxs-lookup"><span data-stu-id="d6364-228">a.</span></span> <span data-ttu-id="d6364-229">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d6364-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d6364-230">b.</span><span class="sxs-lookup"><span data-stu-id="d6364-230">b.</span></span> <span data-ttu-id="d6364-231">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d6364-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d6364-232">c.</span><span class="sxs-lookup"><span data-stu-id="d6364-232">c.</span></span> <span data-ttu-id="d6364-233">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="d6364-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d6364-234">d.</span><span class="sxs-lookup"><span data-stu-id="d6364-234">d.</span></span> <span data-ttu-id="d6364-235">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d6364-235">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-sandbox-test-user"></a><span data-ttu-id="d6364-236">Tworzenie użytkownika testowego piaskownicy usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="d6364-236">Creating a Salesforce Sandbox test user</span></span>

<span data-ttu-id="d6364-237">W tej sekcji użytkownika o nazwie Simona Britta jest tworzony w piaskownicy Salesforce.</span><span class="sxs-lookup"><span data-stu-id="d6364-237">In this section, a user called Britta Simon is created in Salesforce Sandbox.</span></span> <span data-ttu-id="d6364-238">Piaskownica SalesForce obsługę w czasie, który jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="d6364-238">Salesforce Sandbox supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="d6364-239">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="d6364-239">There is no action item for you in this section.</span></span> <span data-ttu-id="d6364-240">Jeśli użytkownik nie istnieje w piaskownicy Salesforce, nowy jest tworzony podczas próby tooaccess piaskownicy Salesforce.</span><span class="sxs-lookup"><span data-stu-id="d6364-240">If a user doesn't already exist in Salesforce Sandbox, a new one is created when you attempt tooaccess Salesforce Sandbox.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d6364-241">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6364-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d6364-242">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSalesforce piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="d6364-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSalesforce Sandbox.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="d6364-244">**tooassign tooSalesforce Simona Britta piaskownicy, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d6364-244">**tooassign Britta Simon tooSalesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="d6364-245">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d6364-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d6364-247">Z listy aplikacji hello wybierz **piaskownicy Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="d6364-247">In hello applications list, select **Salesforce Sandbox**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. <span data-ttu-id="d6364-249">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d6364-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="d6364-251">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d6364-251">Click **Add** button.</span></span> <span data-ttu-id="d6364-252">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d6364-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="d6364-254">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d6364-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d6364-255">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d6364-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d6364-256">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d6364-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d6364-257">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d6364-257">Testing single sign-on</span></span>

<span data-ttu-id="d6364-258">Jeśli chcesz tootest ustawienia logowania jednokrotnego, otwórz hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d6364-258">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="d6364-259">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d6364-259">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d6364-260">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d6364-260">Additional resources</span></span>

* [<span data-ttu-id="d6364-261">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6364-261">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d6364-262">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d6364-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="d6364-263">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="d6364-263">Configure User Provisioning</span></span>](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

