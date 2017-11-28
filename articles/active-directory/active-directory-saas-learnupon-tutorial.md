---
title: 'Samouczek: Integracji Azure Active Directory z LearnUpon | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i LearnUpon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: fdb9c62172327a539f0459c98aa20e63fa441e4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a><span data-ttu-id="0f47d-103">Samouczek: Integracji Azure Active Directory z LearnUpon</span><span class="sxs-lookup"><span data-stu-id="0f47d-103">Tutorial: Azure Active Directory integration with LearnUpon</span></span>

<span data-ttu-id="0f47d-104">Z tego samouczka, dowiesz się, jak toointegrate LearnUpon w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0f47d-104">In this tutorial, you learn how toointegrate LearnUpon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0f47d-105">Integracja z usługą Azure AD LearnUpon zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="0f47d-105">Integrating LearnUpon with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0f47d-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooLearnUpon</span><span class="sxs-lookup"><span data-stu-id="0f47d-106">You can control in Azure AD who has access tooLearnUpon</span></span>
- <span data-ttu-id="0f47d-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooLearnUpon (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f47d-107">You can enable your users tooautomatically get signed-on tooLearnUpon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0f47d-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="0f47d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0f47d-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0f47d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f47d-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0f47d-110">Prerequisites</span></span>

<span data-ttu-id="0f47d-111">tooconfigure integracji z usługą Azure AD z LearnUpon należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="0f47d-111">tooconfigure Azure AD integration with LearnUpon, you need hello following items:</span></span>

- <span data-ttu-id="0f47d-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f47d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0f47d-113">LearnUpon logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="0f47d-113">A LearnUpon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0f47d-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="0f47d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0f47d-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="0f47d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0f47d-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="0f47d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0f47d-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0f47d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0f47d-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="0f47d-118">Scenario description</span></span>
<span data-ttu-id="0f47d-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="0f47d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0f47d-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="0f47d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0f47d-121">Dodawanie LearnUpon z galerii hello</span><span class="sxs-lookup"><span data-stu-id="0f47d-121">Adding LearnUpon from hello gallery</span></span>
2. <span data-ttu-id="0f47d-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="0f47d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learnupon-from-hello-gallery"></a><span data-ttu-id="0f47d-123">Dodawanie LearnUpon z galerii hello</span><span class="sxs-lookup"><span data-stu-id="0f47d-123">Adding LearnUpon from hello gallery</span></span>
<span data-ttu-id="0f47d-124">tooconfigure hello integracji LearnUpon do usługi Azure AD, należy tooadd LearnUpon z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="0f47d-124">tooconfigure hello integration of LearnUpon into Azure AD, you need tooadd LearnUpon from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0f47d-125">**tooadd LearnUpon z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0f47d-125">**tooadd LearnUpon from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0f47d-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0f47d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="0f47d-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="0f47d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0f47d-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0f47d-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="0f47d-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0f47d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="0f47d-133">W polu wyszukiwania hello wpisz **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="0f47d-133">In hello search box, type **LearnUpon**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. <span data-ttu-id="0f47d-135">W panelu wyników hello zaznacz **LearnUpon**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="0f47d-135">In hello results panel, select **LearnUpon**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0f47d-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="0f47d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0f47d-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z LearnUpon w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="0f47d-138">In this section, you configure and test Azure AD single sign-on with LearnUpon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0f47d-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w LearnUpon jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f47d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LearnUpon is tooa user in Azure AD.</span></span> <span data-ttu-id="0f47d-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w LearnUpon musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="0f47d-140">In other words, a link relationship between an Azure AD user and hello related user in LearnUpon needs toobe established.</span></span>

<span data-ttu-id="0f47d-141">W LearnUpon, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="0f47d-141">In LearnUpon, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0f47d-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z LearnUpon, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="0f47d-142">tooconfigure and test Azure AD single sign-on with LearnUpon, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0f47d-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="0f47d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0f47d-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0f47d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0f47d-145">**[Tworzenie użytkownika testowego LearnUpon](#creating-a-learnupon-test-user)**  -toohave odpowiednikiem Simona Britta w LearnUpon, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0f47d-145">**[Creating a LearnUpon test user](#creating-a-learnupon-test-user)** - toohave a counterpart of Britta Simon in LearnUpon that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0f47d-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="0f47d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0f47d-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="0f47d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0f47d-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0f47d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0f47d-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="0f47d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LearnUpon application.</span></span>

<span data-ttu-id="0f47d-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z LearnUpon, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0f47d-150">**tooconfigure Azure AD single sign-on with LearnUpon, perform hello following steps:**</span></span>

1. <span data-ttu-id="0f47d-151">W portalu Azure na powitania hello **LearnUpon** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="0f47d-151">In hello Azure portal, on hello **LearnUpon** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="0f47d-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="0f47d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. <span data-ttu-id="0f47d-155">Na powitania **LearnUpon domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="0f47d-155">On hello **LearnUpon Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    <span data-ttu-id="0f47d-157">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.learnupon.com/saml/consumer`</span><span class="sxs-lookup"><span data-stu-id="0f47d-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.learnupon.com/saml/consumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0f47d-158">Należy pamiętać, że nie jest hello rzeczywistą wartość.</span><span class="sxs-lookup"><span data-stu-id="0f47d-158">Please note that this is not hello real value.</span></span> <span data-ttu-id="0f47d-159">masz tooupdate tej wartości z adresem URL hello rzeczywiste odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="0f47d-159">you have tooupdate this value with hello actual Reply URL.</span></span> <span data-ttu-id="0f47d-160">Skontaktuj się z tej wartości tooget [zespołem pomocy technicznej LearnUpon](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="0f47d-160">tooget this value Contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span>



4. <span data-ttu-id="0f47d-161">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Raw)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="0f47d-161">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. <span data-ttu-id="0f47d-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0f47d-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0f47d-165">Na powitania **konfiguracji LearnUpon** kliknij **skonfigurować LearnUpon** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="0f47d-165">On hello **LearnUpon Configuration** section, click **Configure LearnUpon** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0f47d-166">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="0f47d-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. <span data-ttu-id="0f47d-168">Otwórz innego wystąpienia przeglądarki i zaloguj do LearnUpon przy użyciu konta administratora.</span><span class="sxs-lookup"><span data-stu-id="0f47d-168">Open another browser instance and login into LearnUpon with an administrator account.</span></span> 

8. <span data-ttu-id="0f47d-169">Kliknij przycisk hello **ustawienia** kartę.</span><span class="sxs-lookup"><span data-stu-id="0f47d-169">Click hello **settings** tab.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. <span data-ttu-id="0f47d-171">Kliknij przycisk **rejestracji jednokrotnej - SAML**, a następnie kliknij przycisk **ustawienia ogólne** tooconfigure SAML ustawienia.</span><span class="sxs-lookup"><span data-stu-id="0f47d-171">Click **Single Sign On - SAML**, and then click **General Settings** tooconfigure SAML settings.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. <span data-ttu-id="0f47d-173">W hello **ustawienia ogólne** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="0f47d-173">In hello **General Settings** section, perform hello following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    <span data-ttu-id="0f47d-175">a.</span><span class="sxs-lookup"><span data-stu-id="0f47d-175">a.</span></span> <span data-ttu-id="0f47d-176">Wybierz **włączone**.</span><span class="sxs-lookup"><span data-stu-id="0f47d-176">Select **Enabled**.</span></span>

    <span data-ttu-id="0f47d-177">b.</span><span class="sxs-lookup"><span data-stu-id="0f47d-177">b.</span></span> <span data-ttu-id="0f47d-178">Wybierz **wersji** jako **2.0**.</span><span class="sxs-lookup"><span data-stu-id="0f47d-178">Select **Version** as **2.0**.</span></span>

    <span data-ttu-id="0f47d-179">c.</span><span class="sxs-lookup"><span data-stu-id="0f47d-179">c.</span></span> <span data-ttu-id="0f47d-180">Wybierz **pominąć warunki** jako **nr**.</span><span class="sxs-lookup"><span data-stu-id="0f47d-180">Select **Skip conditions** as **No**.</span></span>

    <span data-ttu-id="0f47d-181">d.</span><span class="sxs-lookup"><span data-stu-id="0f47d-181">d.</span></span> <span data-ttu-id="0f47d-182">W hello **Post tokenu SAML nazwę param** pole tekstowe, nazwa typu hello żądania post parametru toohello adres URL klienta SAML wymienionych powyżej zawierający hello potwierdzenia języka SAML toobe zweryfikowane i uwierzytelniony — na przykład  **SAMLResponse**.</span><span class="sxs-lookup"><span data-stu-id="0f47d-182">In hello **SAML Token Post param name** textbox, type hello name of request post parameter toohello SAML consumer URL indicated above that contains hello SAML Assertion toobe verified and authenticated - for example **SAMLResponse**.</span></span>

    <span data-ttu-id="0f47d-183">e.</span><span class="sxs-lookup"><span data-stu-id="0f47d-183">e.</span></span> <span data-ttu-id="0f47d-184">W hello **Format identyfikatora nazwy** pole tekstowe, typ hello wartość, która wskazuje, gdzie w użytkownikom hello potwierdzenia języka SAML identyfikator (adres E-mail) znajduje się — na przykład **urn: oasis: nazwy: tc: SAML:1.1:nameid-format: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="0f47d-184">In hello **Name Identifier Format** textbox, type hello value that indicates where in your SAML Assertion hello users identifier (Email address) resides - for example **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>
  
    <span data-ttu-id="0f47d-185">f.</span><span class="sxs-lookup"><span data-stu-id="0f47d-185">f.</span></span> <span data-ttu-id="0f47d-186">W hello **zidentyfikować lokalizacji dostawcy** pole tekstowe, typ hello wartość, która wskazuje, gdzie hello użytkownicy są wysyłane tooif kliknij przycisk z przekazanego ikonę z ekranu logowania do portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0f47d-186">In hello **Identify Provider Location** textbox, type hello value that indicates where hello users are sent tooif they click on your uploaded icon from your Azure portal login screen.</span></span>
  
    <span data-ttu-id="0f47d-187">g.</span><span class="sxs-lookup"><span data-stu-id="0f47d-187">g.</span></span> <span data-ttu-id="0f47d-188">W hello **Wyloguj adresu URL** pole tekstowe, Wklej hello **Sign-Out URL** którego została skopiowana z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0f47d-188">In hello **Sign out URL** textbox, paste hello **Sign-Out URL** which you have copied from hello Azure portal.</span></span>
    
    <span data-ttu-id="0f47d-189">h.</span><span class="sxs-lookup"><span data-stu-id="0f47d-189">h.</span></span> <span data-ttu-id="0f47d-190">Kliknij przycisk **Zarządzanie odbitek palca**, a następnie przekaż hello odcisk palca certyfikatu pobrane.</span><span class="sxs-lookup"><span data-stu-id="0f47d-190">Click **Manage finger prints**, and then upload hello finger print of your downloaded certificate.</span></span>

11. <span data-ttu-id="0f47d-191">Kliknij przycisk **ustawienia użytkownika**, a następnie wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="0f47d-191">Click **User Settings**, and then perform hello following steps:</span></span>
   
     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    <span data-ttu-id="0f47d-193">a.</span><span class="sxs-lookup"><span data-stu-id="0f47d-193">a.</span></span> <span data-ttu-id="0f47d-194">W hello **Format identyfikatora imię** pole tekstowe, typ hello wartość, która informuje NAS w Twoje imię potwierdzenia języka SAML hello użytkowników znajduje się — na przykład: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="0f47d-194">In hello **First Name Identifier Format** textbox, type hello value that tells us where in your SAML Assertion hello users firstname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
  
    <span data-ttu-id="0f47d-195">b.</span><span class="sxs-lookup"><span data-stu-id="0f47d-195">b.</span></span> <span data-ttu-id="0f47d-196">W hello **ostatniego Format identyfikatora nazwy** pole tekstowe, typ hello wartość, która informuje NAS w Twoje nazwisko potwierdzenia języka SAML hello użytkowników znajduje się — na przykład: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="0f47d-196">In hello **Last Name Identifier Format** textbox, type hello value that tells us where in your SAML Assertion hello users lastname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

> [!TIP]
> <span data-ttu-id="0f47d-197">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="0f47d-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0f47d-198">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="0f47d-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0f47d-199">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0f47d-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0f47d-200">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f47d-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="0f47d-201">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="0f47d-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="0f47d-203">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0f47d-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0f47d-204">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0f47d-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0f47d-206">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="0f47d-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0f47d-208">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0f47d-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0f47d-210">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0f47d-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0f47d-212">a.</span><span class="sxs-lookup"><span data-stu-id="0f47d-212">a.</span></span> <span data-ttu-id="0f47d-213">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0f47d-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0f47d-214">b.</span><span class="sxs-lookup"><span data-stu-id="0f47d-214">b.</span></span> <span data-ttu-id="0f47d-215">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0f47d-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0f47d-216">c.</span><span class="sxs-lookup"><span data-stu-id="0f47d-216">c.</span></span> <span data-ttu-id="0f47d-217">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="0f47d-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0f47d-218">d.</span><span class="sxs-lookup"><span data-stu-id="0f47d-218">d.</span></span> <span data-ttu-id="0f47d-219">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0f47d-219">Click **Create**.</span></span>
 
### <a name="creating-a-learnupon-test-user"></a><span data-ttu-id="0f47d-220">Tworzenie użytkownika testowego LearnUpon</span><span class="sxs-lookup"><span data-stu-id="0f47d-220">Creating a LearnUpon test user</span></span>

<span data-ttu-id="0f47d-221">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="0f47d-221">hello objective of this section is toocreate a user called Britta Simon in LearnUpon.</span></span> <span data-ttu-id="0f47d-222">LearnUpon obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="0f47d-222">LearnUpon supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="0f47d-223">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="0f47d-223">There is no action item for you in this section.</span></span> <span data-ttu-id="0f47d-224">Nowy użytkownik zostanie utworzony podczas próby tooaccess LearnUpon, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="0f47d-224">A new user will be created during an attempt tooaccess LearnUpon if it doesn't exist yet.</span></span> <span data-ttu-id="0f47d-225">[Konfigurowanie usługi Azure AD jednokrotnej](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="0f47d-225">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="0f47d-226">Jeśli potrzebujesz ręcznie toocreate użytkownika, należy toocontact [zespołem pomocy technicznej LearnUpon](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="0f47d-226">If you need toocreate an user manually, you need toocontact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0f47d-227">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f47d-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0f47d-228">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooLearnUpon.</span><span class="sxs-lookup"><span data-stu-id="0f47d-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearnUpon.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="0f47d-230">**tooassign tooLearnUpon Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="0f47d-230">**tooassign Britta Simon tooLearnUpon, perform hello following steps:**</span></span>

1. <span data-ttu-id="0f47d-231">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0f47d-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="0f47d-233">Z listy aplikacji hello wybierz **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="0f47d-233">In hello applications list, select **LearnUpon**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. <span data-ttu-id="0f47d-235">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="0f47d-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="0f47d-237">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0f47d-237">Click **Add** button.</span></span> <span data-ttu-id="0f47d-238">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0f47d-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="0f47d-240">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0f47d-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0f47d-241">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0f47d-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0f47d-242">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0f47d-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0f47d-243">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0f47d-243">Testing single sign-on</span></span>

<span data-ttu-id="0f47d-244">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="0f47d-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0f47d-245">Po kliknięciu kafelka LearnUpon hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour LearnUpon aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0f47d-245">When you click hello LearnUpon tile in hello Access Panel, you should get automatically signed-on tooyour LearnUpon application.</span></span>
<span data-ttu-id="0f47d-246">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0f47d-246">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0f47d-247">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="0f47d-247">Additional resources</span></span>

* [<span data-ttu-id="0f47d-248">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f47d-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0f47d-249">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0f47d-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png

