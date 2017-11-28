---
title: 'Samouczek: Integracji Azure Active Directory z Showpad | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Showpad."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48b6bee0-dbc5-4863-964d-75b25e517741
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2c8c306b4b94c368a93f92123d3abe9fe35167db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-showpad"></a><span data-ttu-id="a2f4f-103">Samouczek: Integracji Azure Active Directory z Showpad</span><span class="sxs-lookup"><span data-stu-id="a2f4f-103">Tutorial: Azure Active Directory integration with Showpad</span></span>

<span data-ttu-id="a2f4f-104">Z tego samouczka, dowiesz się, jak toointegrate Showpad w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a2f4f-104">In this tutorial, you learn how toointegrate Showpad with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a2f4f-105">Integracja z usługą Azure AD Showpad zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="a2f4f-105">Integrating Showpad with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a2f4f-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooShowpad</span><span class="sxs-lookup"><span data-stu-id="a2f4f-106">You can control in Azure AD who has access tooShowpad</span></span>
- <span data-ttu-id="a2f4f-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooShowpad (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2f4f-107">You can enable your users tooautomatically get signed-on tooShowpad (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a2f4f-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a2f4f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a2f4f-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a2f4f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2f4f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a2f4f-110">Prerequisites</span></span>

<span data-ttu-id="a2f4f-111">tooconfigure integracji z usługą Azure AD z Showpad należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a2f4f-111">tooconfigure Azure AD integration with Showpad, you need hello following items:</span></span>

- <span data-ttu-id="a2f4f-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2f4f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a2f4f-113">Showpad logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a2f4f-113">A Showpad single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a2f4f-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a2f4f-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="a2f4f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a2f4f-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a2f4f-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a2f4f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a2f4f-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="a2f4f-118">Scenario description</span></span>
<span data-ttu-id="a2f4f-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a2f4f-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="a2f4f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a2f4f-121">Dodawanie Showpad z galerii hello</span><span class="sxs-lookup"><span data-stu-id="a2f4f-121">Adding Showpad from hello gallery</span></span>
2. <span data-ttu-id="a2f4f-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a2f4f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-showpad-from-hello-gallery"></a><span data-ttu-id="a2f4f-123">Dodawanie Showpad z galerii hello</span><span class="sxs-lookup"><span data-stu-id="a2f4f-123">Adding Showpad from hello gallery</span></span>

<span data-ttu-id="a2f4f-124">tooconfigure hello integracji Showpad do usługi Azure AD, należy tooadd Showpad z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-124">tooconfigure hello integration of Showpad into Azure AD, you need tooadd Showpad from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a2f4f-125">**tooadd Showpad z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="a2f4f-125">**tooadd Showpad from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2f4f-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="a2f4f-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a2f4f-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="a2f4f-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="a2f4f-133">W polu wyszukiwania hello wpisz **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-133">In hello search box, type **Showpad**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_search.png)

5. <span data-ttu-id="a2f4f-135">W panelu wyników hello zaznacz **Showpad**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-135">In hello results panel, select **Showpad**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a2f4f-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a2f4f-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="a2f4f-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Showpad na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="a2f4f-138">In this section, you configure and test Azure AD single sign-on with Showpad based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a2f4f-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Showpad jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Showpad is tooa user in Azure AD.</span></span> <span data-ttu-id="a2f4f-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Showpad musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-140">In other words, a link relationship between an Azure AD user and hello related user in Showpad needs toobe established.</span></span>

<span data-ttu-id="a2f4f-141">W Showpad, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-141">In Showpad, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a2f4f-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Showpad, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a2f4f-142">tooconfigure and test Azure AD single sign-on with Showpad, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a2f4f-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a2f4f-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a2f4f-145">**[Tworzenie użytkownika testowego Showpad](#creating-a-showpad-test-user)**  -toohave odpowiednikiem Simona Britta w Showpad, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-145">**[Creating a Showpad test user](#creating-a-showpad-test-user)** - toohave a counterpart of Britta Simon in Showpad that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a2f4f-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a2f4f-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a2f4f-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a2f4f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a2f4f-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Showpad.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Showpad application.</span></span>

<span data-ttu-id="a2f4f-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Showpad, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="a2f4f-150">**tooconfigure Azure AD single sign-on with Showpad, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2f4f-151">W portalu Azure na powitania hello **Showpad** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-151">In hello Azure portal, on hello **Showpad** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="a2f4f-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_samlbase.png)

3. <span data-ttu-id="a2f4f-155">Na powitania **Showpad domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="a2f4f-155">On hello **Showpad Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_url.png)

    <span data-ttu-id="a2f4f-157">a.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-157">a.</span></span> <span data-ttu-id="a2f4f-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<comapany-name>.showpad.biz/login`</span><span class="sxs-lookup"><span data-stu-id="a2f4f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<comapany-name>.showpad.biz/login`</span></span>

    <span data-ttu-id="a2f4f-159">b.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-159">b.</span></span> <span data-ttu-id="a2f4f-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company-name>.showpad.biz`</span><span class="sxs-lookup"><span data-stu-id="a2f4f-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company-name>.showpad.biz`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a2f4f-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-161">These values are not real.</span></span> <span data-ttu-id="a2f4f-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a2f4f-163">Skontaktuj się z [zespołem pomocy technicznej Showpad](https://help.showpad.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-163">Contact [Showpad support team](https://help.showpad.com) tooget these values.</span></span> 
 


4. <span data-ttu-id="a2f4f-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_certificate.png) 

5. <span data-ttu-id="a2f4f-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-showpad-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a2f4f-168">Dzierżawca Showpad tooyour logowania jako administrator.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-168">Sign-on tooyour Showpad tenant as an administrator.</span></span>

7. <span data-ttu-id="a2f4f-169">W menu hello na górze powitania kliknij hello **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-169">In hello menu on hello top, click hello **Settings**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_001.png) 

8. <span data-ttu-id="a2f4f-171">Przejdź za"**rejestracji jednokrotnej**"i kliknij przycisk"**włączyć**."</span><span class="sxs-lookup"><span data-stu-id="a2f4f-171">Navigate too"**Single Sign-On**" and click "**Enable**."</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_002.png)

9. <span data-ttu-id="a2f4f-173">Na powitania **dodawania usługi SAML 2.0** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="a2f4f-173">On hello **Add a SAML 2.0 Service** dialog, perform hello following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_003.png) 
   
    <span data-ttu-id="a2f4f-175">a.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-175">a.</span></span> <span data-ttu-id="a2f4f-176">W hello **nazwa** pole tekstowe, nazwa typu hello identyfikatora dostawcy (na przykład: Nazwa firmy).</span><span class="sxs-lookup"><span data-stu-id="a2f4f-176">In hello **Name** textbox, type hello name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="a2f4f-177">b.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-177">b.</span></span> <span data-ttu-id="a2f4f-178">Jako **źródła metadanych**, wybierz pozycję **XML**.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-178">As **Metadata Source**, select **XML**.</span></span>
   
    <span data-ttu-id="a2f4f-179">c.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-179">c.</span></span> <span data-ttu-id="a2f4f-180">Kopiowanie zawartości hello metadanych pliku XML, który został już pobrany z portalu Azure hello, a następnie wklej go do hello **XML metadanych** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-180">Copy hello content of metadata XML file, which you have downloaded from hello Azure portal, and then paste it into hello **Metadata XML** textbox.</span></span>
   
    <span data-ttu-id="a2f4f-181">d.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-181">d.</span></span> <span data-ttu-id="a2f4f-182">Wybierz **automatycznego udostępniania kont dla nowych użytkowników podczas logowania**.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-182">Select **Auto-provision accounts for new users when they log in**.</span></span>
   
    <span data-ttu-id="a2f4f-183">e.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-183">e.</span></span> <span data-ttu-id="a2f4f-184">Kliknij przycisk **przesłać**.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-184">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="a2f4f-185">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="a2f4f-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a2f4f-186">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a2f4f-187">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a2f4f-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a2f4f-188">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2f4f-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="a2f4f-189">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="a2f4f-191">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="a2f4f-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2f4f-192">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a2f4f-194">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a2f4f-196">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a2f4f-198">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="a2f4f-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a2f4f-200">a.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-200">a.</span></span> <span data-ttu-id="a2f4f-201">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a2f4f-202">b.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-202">b.</span></span> <span data-ttu-id="a2f4f-203">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a2f4f-204">c.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-204">c.</span></span> <span data-ttu-id="a2f4f-205">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a2f4f-206">d.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-206">d.</span></span> <span data-ttu-id="a2f4f-207">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-207">Click **Create**.</span></span>
 
### <a name="creating-a-showpad-test-user"></a><span data-ttu-id="a2f4f-208">Tworzenie użytkownika testowego Showpad</span><span class="sxs-lookup"><span data-stu-id="a2f4f-208">Creating a Showpad test user</span></span>

<span data-ttu-id="a2f4f-209">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Showpad.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-209">hello objective of this section is toocreate a user called Britta Simon in Showpad.</span></span> 

<span data-ttu-id="a2f4f-210">Showpad obsługę w czasie.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-210">Showpad supports just-in-time provisioning.</span></span> <span data-ttu-id="a2f4f-211">Włączono alokacji w  **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-211">You have enabled provisioning in **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**.</span></span> 

<span data-ttu-id="a2f4f-212">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-212">There is no action item for you in this section.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a2f4f-213">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2f4f-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a2f4f-214">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooShowpad.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooShowpad.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="a2f4f-216">**tooassign tooShowpad Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="a2f4f-216">**tooassign Britta Simon tooShowpad, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2f4f-217">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="a2f4f-219">Z listy aplikacji hello wybierz **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-219">In hello applications list, select **Showpad**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_app.png) 

3. <span data-ttu-id="a2f4f-221">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="a2f4f-223">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-223">Click **Add** button.</span></span> <span data-ttu-id="a2f4f-224">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="a2f4f-226">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a2f4f-227">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a2f4f-228">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a2f4f-229">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a2f4f-229">Testing single sign-on</span></span>

<span data-ttu-id="a2f4f-230">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a2f4f-231">Po kliknięciu kafelka Showpad hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooShowpad aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a2f4f-231">When you click hello Showpad tile in hello Access Panel, you should get automatically signed-on tooShowpad application.</span></span>
<span data-ttu-id="a2f4f-232">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a2f4f-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a2f4f-233">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="a2f4f-233">Additional resources</span></span>

* [<span data-ttu-id="a2f4f-234">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2f4f-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a2f4f-235">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a2f4f-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_203.png

