---
title: 'Samouczek: Integracji Azure Active Directory z mianowicie | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory, a mianowicie."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9541d5c4-4c82-4b5b-b01a-6a3f75a2b7a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: b0477ca6fa52a21abea7de458f8a99a01e8c25c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-namely"></a><span data-ttu-id="ae054-103">Samouczek: Integracji Azure Active Directory z mianowicie</span><span class="sxs-lookup"><span data-stu-id="ae054-103">Tutorial: Azure Active Directory integration with Namely</span></span>

<span data-ttu-id="ae054-104">Z tego samouczka, dowiesz się, jak toointegrate, czyli w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ae054-104">In this tutorial, you learn how toointegrate Namely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ae054-105">To znaczy integracji z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ae054-105">Integrating Namely with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ae054-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooNamely</span><span class="sxs-lookup"><span data-stu-id="ae054-106">You can control in Azure AD who has access tooNamely</span></span>
- <span data-ttu-id="ae054-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooNamely (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae054-107">You can enable your users tooautomatically get signed-on tooNamely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ae054-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ae054-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ae054-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ae054-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae054-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ae054-110">Prerequisites</span></span>

<span data-ttu-id="ae054-111">Integracja tooconfigure usługi Azure AD z mianowicie, możesz należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ae054-111">tooconfigure Azure AD integration with Namely, you need hello following items:</span></span>

- <span data-ttu-id="ae054-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae054-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ae054-113">To znaczy logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ae054-113">A Namely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ae054-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ae054-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ae054-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ae054-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ae054-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ae054-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ae054-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ae054-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ae054-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ae054-118">Scenario description</span></span>
<span data-ttu-id="ae054-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ae054-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ae054-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ae054-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ae054-121">Dodawanie mianowicie z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ae054-121">Adding Namely from hello gallery</span></span>
2. <span data-ttu-id="ae054-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ae054-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-namely-from-hello-gallery"></a><span data-ttu-id="ae054-123">Dodawanie mianowicie z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ae054-123">Adding Namely from hello gallery</span></span>
<span data-ttu-id="ae054-124">tooconfigure hello integracji mianowicie do usługi Azure AD, należy tooadd mianowicie od hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ae054-124">tooconfigure hello integration of Namely into Azure AD, you need tooadd Namely from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ae054-125">**tooadd, czyli z galerii hello, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ae054-125">**tooadd Namely from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae054-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ae054-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="ae054-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ae054-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ae054-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ae054-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ae054-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ae054-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ae054-133">W polu wyszukiwania hello wpisz **mianowicie**.</span><span class="sxs-lookup"><span data-stu-id="ae054-133">In hello search box, type **Namely**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-namely-tutorial/tutorial_namely_search.png)

5. <span data-ttu-id="ae054-135">W panelu wyników hello, wybierz **mianowicie**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ae054-135">In hello results panel, select **Namely**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-namely-tutorial/tutorial_namely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ae054-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ae054-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ae054-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z, a mianowicie w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="ae054-138">In this section, you configure and test Azure AD single sign-on with Namely based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ae054-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w mianowicie jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae054-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Namely is tooa user in Azure AD.</span></span> <span data-ttu-id="ae054-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w mianowicie musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="ae054-140">In other words, a link relationship between an Azure AD user and hello related user in Namely needs toobe established.</span></span>

<span data-ttu-id="ae054-141">Mianowicie, przypisywanie wartości hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="ae054-141">In Namely, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ae054-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z mianowicie, możesz należy hello toocomplete po bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="ae054-142">tooconfigure and test Azure AD single sign-on with Namely, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ae054-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ae054-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ae054-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ae054-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ae054-145">**[Tworzenie mianowicie użytkownik testowy](#creating-a-namely-test-user)**  -toohave odpowiednikiem Simona Britta w mianowicie czyli połączonego toohello reprezentacja użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae054-145">**[Creating a Namely test user](#creating-a-namely-test-user)** - toohave a counterpart of Britta Simon in Namely that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ae054-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ae054-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ae054-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="ae054-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ae054-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ae054-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ae054-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w mianowicie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ae054-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Namely application.</span></span>

<span data-ttu-id="ae054-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z mianowicie, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ae054-150">**tooconfigure Azure AD single sign-on with Namely, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae054-151">W portalu Azure na powitania hello **mianowicie** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ae054-151">In hello Azure portal, on hello **Namely** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="ae054-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ae054-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_namely_samlbase.png)

3. <span data-ttu-id="ae054-155">Na powitania **mianowicie domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ae054-155">On hello **Namely Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_namely_url.png)

    <span data-ttu-id="ae054-157">a.</span><span class="sxs-lookup"><span data-stu-id="ae054-157">a.</span></span> <span data-ttu-id="ae054-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.namely.com`</span><span class="sxs-lookup"><span data-stu-id="ae054-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.namely.com`</span></span>

    <span data-ttu-id="ae054-159">b.</span><span class="sxs-lookup"><span data-stu-id="ae054-159">b.</span></span> <span data-ttu-id="ae054-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.namely.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="ae054-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.namely.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ae054-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="ae054-161">These values are not real.</span></span> <span data-ttu-id="ae054-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="ae054-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ae054-163">Skontaktuj się z [zespół obsługi klienta a mianowicie](https://www.namely.com/contact/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="ae054-163">Contact [Namely Client support team](https://www.namely.com/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="ae054-164">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ae054-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_namely_certificate.png) 

5. <span data-ttu-id="ae054-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ae054-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ae054-168">Na powitania **mianowicie konfiguracji** kliknij **skonfigurować mianowicie** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="ae054-168">On hello **Namely Configuration** section, click **Configure Namely** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ae054-169">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="ae054-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_namely_configure.png) 

7. <span data-ttu-id="ae054-171">W innym oknie przeglądarki logowania tooyour mianowicie witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ae054-171">In another browser window, sign on tooyour Namely company site as an administrator.</span></span>

8. <span data-ttu-id="ae054-172">Witaj pasku narzędzi u góry hello, kliknij przycisk **firmy**.</span><span class="sxs-lookup"><span data-stu-id="ae054-172">In hello toolbar on hello top, click **Company**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_namely_06.png) 

9. <span data-ttu-id="ae054-174">Kliknij przycisk hello **ustawienia** kartę.</span><span class="sxs-lookup"><span data-stu-id="ae054-174">Click hello **Settings** tab.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_namely_07.png) 

10. <span data-ttu-id="ae054-176">Kliknij przycisk **SAML**.</span><span class="sxs-lookup"><span data-stu-id="ae054-176">Click **SAML**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_namely_08.png) 

11. <span data-ttu-id="ae054-178">Na powitania **ustawienia SAML** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ae054-178">On hello **SAML Settings** page, perform hello following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_namely_09.png)
 
    <span data-ttu-id="ae054-180">a.</span><span class="sxs-lookup"><span data-stu-id="ae054-180">a.</span></span> <span data-ttu-id="ae054-181">Kliknij przycisk **Włącz SAML**.</span><span class="sxs-lookup"><span data-stu-id="ae054-181">Click **Enable SAML**.</span></span> 

    <span data-ttu-id="ae054-182">b.</span><span class="sxs-lookup"><span data-stu-id="ae054-182">b.</span></span> <span data-ttu-id="ae054-183">W hello **adres url logowania jednokrotnego dostawcy tożsamości** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ae054-183">In hello **Identity provider SSO url** textbox,  paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="ae054-184">c.</span><span class="sxs-lookup"><span data-stu-id="ae054-184">c.</span></span> <span data-ttu-id="ae054-185">Otwórz pobrany certyfikat w Notatniku, hello kopiowania zawartości, a następnie wklej go do hello **certyfikat dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="ae054-185">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **Identity provider certificate** textbox.</span></span>
     
    <span data-ttu-id="ae054-186">d.</span><span class="sxs-lookup"><span data-stu-id="ae054-186">d.</span></span> <span data-ttu-id="ae054-187">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ae054-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="ae054-188">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="ae054-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ae054-189">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="ae054-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ae054-190">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ae054-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ae054-191">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae054-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="ae054-192">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="ae054-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="ae054-194">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ae054-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae054-195">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ae054-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ae054-197">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ae054-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ae054-199">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ae054-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ae054-201">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ae054-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ae054-203">a.</span><span class="sxs-lookup"><span data-stu-id="ae054-203">a.</span></span> <span data-ttu-id="ae054-204">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ae054-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ae054-205">b.</span><span class="sxs-lookup"><span data-stu-id="ae054-205">b.</span></span> <span data-ttu-id="ae054-206">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ae054-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ae054-207">c.</span><span class="sxs-lookup"><span data-stu-id="ae054-207">c.</span></span> <span data-ttu-id="ae054-208">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="ae054-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ae054-209">d.</span><span class="sxs-lookup"><span data-stu-id="ae054-209">d.</span></span> <span data-ttu-id="ae054-210">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ae054-210">Click **Create**.</span></span>
 
### <a name="creating-a-namely-test-user"></a><span data-ttu-id="ae054-211">Tworzenie mianowicie użytkownik testowy</span><span class="sxs-lookup"><span data-stu-id="ae054-211">Creating a Namely test user</span></span>

<span data-ttu-id="ae054-212">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w mianowicie.</span><span class="sxs-lookup"><span data-stu-id="ae054-212">hello objective of this section is toocreate a user called Britta Simon in Namely.</span></span>

<span data-ttu-id="ae054-213">**toocreate użytkownika o nazwie Simona Britta w mianowicie, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ae054-213">**toocreate a user called Britta Simon in Namely, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae054-214">Logowania jednokrotnego tooyour mianowicie firmy lokacji jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ae054-214">Sign-on tooyour Namely company site as an administrator.</span></span>

2. <span data-ttu-id="ae054-215">Witaj pasku narzędzi u góry hello, kliknij przycisk **osób**.</span><span class="sxs-lookup"><span data-stu-id="ae054-215">In hello toolbar on hello top, click **People**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_namely_10.png) 

3. <span data-ttu-id="ae054-217">Kliknij przycisk hello **katalogu** kartę.</span><span class="sxs-lookup"><span data-stu-id="ae054-217">Click hello **Directory** tab.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_namely_11.png) 

4. <span data-ttu-id="ae054-219">Kliknij przycisk **Dodawanie nowej osoby**.</span><span class="sxs-lookup"><span data-stu-id="ae054-219">Click **Add New Person**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_namely_12.png)

5. <span data-ttu-id="ae054-221">Na powitania **Dodawanie nowej osoby** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ae054-221">On hello **Add New Person** dialog, perform hello following steps:</span></span>

    <span data-ttu-id="ae054-222">a.</span><span class="sxs-lookup"><span data-stu-id="ae054-222">a.</span></span> <span data-ttu-id="ae054-223">W hello **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ae054-223">In hello **First name** textbox, type **Britta**.</span></span>

    <span data-ttu-id="ae054-224">b.</span><span class="sxs-lookup"><span data-stu-id="ae054-224">b.</span></span> <span data-ttu-id="ae054-225">W hello **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="ae054-225">In hello **Last name** textbox, type **Simon**.</span></span>

    <span data-ttu-id="ae054-226">c.</span><span class="sxs-lookup"><span data-stu-id="ae054-226">c.</span></span> <span data-ttu-id="ae054-227">W hello **E-mail** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ae054-227">In hello **Email** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ae054-228">d.</span><span class="sxs-lookup"><span data-stu-id="ae054-228">d.</span></span> <span data-ttu-id="ae054-229">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ae054-229">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ae054-230">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae054-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ae054-231">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooNamely.</span><span class="sxs-lookup"><span data-stu-id="ae054-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNamely.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="ae054-233">**tooassign tooNamely Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ae054-233">**tooassign Britta Simon tooNamely, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae054-234">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ae054-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ae054-236">Z listy aplikacji hello wybierz **mianowicie**.</span><span class="sxs-lookup"><span data-stu-id="ae054-236">In hello applications list, select **Namely**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_namely_app.png) 

3. <span data-ttu-id="ae054-238">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ae054-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="ae054-240">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ae054-240">Click **Add** button.</span></span> <span data-ttu-id="ae054-241">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ae054-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="ae054-243">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ae054-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ae054-244">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ae054-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ae054-245">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ae054-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ae054-246">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ae054-246">Testing single sign-on</span></span>

<span data-ttu-id="ae054-247">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ae054-247">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="ae054-248">Po kliknięciu hello mianowicie kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour mianowicie aplikacji</span><span class="sxs-lookup"><span data-stu-id="ae054-248">When you click hello Namely tile in hello Access Panel, you should get automatically signed-on tooyour Namely application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ae054-249">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ae054-249">Additional resources</span></span>

* [<span data-ttu-id="ae054-250">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae054-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ae054-251">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ae054-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-namely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-namely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-namely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-namely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-namely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-namely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-namely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-namely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-namely-tutorial/tutorial_general_203.png

