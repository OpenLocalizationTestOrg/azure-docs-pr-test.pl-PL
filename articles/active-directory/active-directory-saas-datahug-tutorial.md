---
title: 'Samouczek: Integracji Azure Active Directory z Datahug | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Datahug."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5c0dc1ea-7ff4-4554-b60b-0f2fa9f5abaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: jeedes
ms.openlocfilehash: 79ccb939c7a19720bcf696af141f747db00c8a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-datahug"></a><span data-ttu-id="80a7e-103">Samouczek: Integracji Azure Active Directory z Datahug</span><span class="sxs-lookup"><span data-stu-id="80a7e-103">Tutorial: Azure Active Directory integration with Datahug</span></span>

<span data-ttu-id="80a7e-104">Z tego samouczka, dowiesz się, jak toointegrate Datahug w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="80a7e-104">In this tutorial, you learn how toointegrate Datahug with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="80a7e-105">Integracja z usługą Azure AD Datahug zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="80a7e-105">Integrating Datahug with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="80a7e-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooDatahug</span><span class="sxs-lookup"><span data-stu-id="80a7e-106">You can control in Azure AD who has access tooDatahug</span></span>
- <span data-ttu-id="80a7e-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooDatahug (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="80a7e-107">You can enable your users tooautomatically get signed-on tooDatahug (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="80a7e-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="80a7e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="80a7e-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz.</span><span class="sxs-lookup"><span data-stu-id="80a7e-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="80a7e-110">[Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="80a7e-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80a7e-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="80a7e-111">Prerequisites</span></span>

<span data-ttu-id="80a7e-112">tooconfigure integracji z usługą Azure AD z Datahug należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="80a7e-112">tooconfigure Azure AD integration with Datahug, you need hello following items:</span></span>

- <span data-ttu-id="80a7e-113">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="80a7e-113">An Azure AD subscription</span></span>
- <span data-ttu-id="80a7e-114">Datahug jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="80a7e-114">A Datahug single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="80a7e-115">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="80a7e-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="80a7e-116">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="80a7e-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="80a7e-117">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="80a7e-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="80a7e-118">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="80a7e-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="80a7e-119">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="80a7e-119">Scenario description</span></span>
<span data-ttu-id="80a7e-120">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="80a7e-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="80a7e-121">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="80a7e-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="80a7e-122">Dodawanie Datahug z galerii hello</span><span class="sxs-lookup"><span data-stu-id="80a7e-122">Adding Datahug from hello gallery</span></span>
2. <span data-ttu-id="80a7e-123">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="80a7e-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-datahug-from-hello-gallery"></a><span data-ttu-id="80a7e-124">Dodawanie Datahug z galerii hello</span><span class="sxs-lookup"><span data-stu-id="80a7e-124">Adding Datahug from hello gallery</span></span>
<span data-ttu-id="80a7e-125">tooconfigure hello integracji Datahug do usługi Azure AD, należy tooadd Datahug z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="80a7e-125">tooconfigure hello integration of Datahug into Azure AD, you need tooadd Datahug from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="80a7e-126">**tooadd Datahug z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="80a7e-126">**tooadd Datahug from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="80a7e-127">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="80a7e-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="80a7e-129">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="80a7e-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="80a7e-130">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="80a7e-130">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="80a7e-132">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="80a7e-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="80a7e-134">W polu wyszukiwania hello wpisz **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="80a7e-134">In hello search box, type **Datahug**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_search.png)

5. <span data-ttu-id="80a7e-136">W panelu wyników hello zaznacz **Datahug**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="80a7e-136">In hello results panel, select **Datahug**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="80a7e-138">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="80a7e-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="80a7e-139">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Datahug na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="80a7e-139">In this section, you configure and test Azure AD single sign-on with Datahug based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="80a7e-140">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Datahug jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80a7e-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Datahug is tooa user in Azure AD.</span></span> <span data-ttu-id="80a7e-141">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Datahug musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="80a7e-141">In other words, a link relationship between an Azure AD user and hello related user in Datahug needs toobe established.</span></span>

<span data-ttu-id="80a7e-142">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Datahug.</span><span class="sxs-lookup"><span data-stu-id="80a7e-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Datahug.</span></span>

<span data-ttu-id="80a7e-143">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Datahug, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="80a7e-143">tooconfigure and test Azure AD single sign-on with Datahug, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="80a7e-144">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="80a7e-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="80a7e-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="80a7e-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="80a7e-146">**[Tworzenie użytkownika testowego Datahug](#creating-a-datahug-test-user)**  -toohave odpowiednikiem Simona Britta w Datahug, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="80a7e-146">**[Creating a Datahug test user](#creating-a-datahug-test-user)** - toohave a counterpart of Britta Simon in Datahug that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="80a7e-147">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="80a7e-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="80a7e-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="80a7e-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="80a7e-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="80a7e-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="80a7e-150">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Datahug.</span><span class="sxs-lookup"><span data-stu-id="80a7e-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Datahug application.</span></span>

<span data-ttu-id="80a7e-151">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Datahug, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="80a7e-151">**tooconfigure Azure AD single sign-on with Datahug, perform hello following steps:**</span></span>

1. <span data-ttu-id="80a7e-152">W portalu Azure na powitania hello **Datahug** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="80a7e-152">In hello Azure portal, on hello **Datahug** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="80a7e-154">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="80a7e-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_samlbase.png)

3. <span data-ttu-id="80a7e-156">Na powitania **Datahug domeny i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="80a7e-156">On hello **Datahug Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_ur1.png)

    <span data-ttu-id="80a7e-158">a.</span><span class="sxs-lookup"><span data-stu-id="80a7e-158">a.</span></span> <span data-ttu-id="80a7e-159">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://apps.datahug.com/identity/<uniqueID>`</span><span class="sxs-lookup"><span data-stu-id="80a7e-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://apps.datahug.com/identity/<uniqueID>`</span></span>

    <span data-ttu-id="80a7e-160">b.</span><span class="sxs-lookup"><span data-stu-id="80a7e-160">b.</span></span> <span data-ttu-id="80a7e-161">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://apps.datahug.com/identity/<uniqueID>/acs`</span><span class="sxs-lookup"><span data-stu-id="80a7e-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://apps.datahug.com/identity/<uniqueID>/acs`</span></span>

4. <span data-ttu-id="80a7e-162">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="80a7e-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="80a7e-163">Jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="80a7e-163">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_url2.png)

    <span data-ttu-id="80a7e-165">W hello **adres URL logowania** tekstowym, wpisz adres URL jako:`https://apps.datahug.com/`</span><span class="sxs-lookup"><span data-stu-id="80a7e-165">In hello **Sign-on URL** textbox, type a URL as: `https://apps.datahug.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="80a7e-166">Wartości te nie są hello prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="80a7e-166">These values are not hello real.</span></span> <span data-ttu-id="80a7e-167">Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="80a7e-167">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="80a7e-168">W tym miejscu zalecamy możesz toouse hello unikatową wartość ciągu w hello identyfikator i adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="80a7e-168">Here we suggest you toouse hello unique value of string in hello Identifier and Reply URL.</span></span> <span data-ttu-id="80a7e-169">Skontaktuj się z [zespołem pomocy technicznej klienta Datahug](http://datahug.com/about/contact-us/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="80a7e-169">Contact [Datahug Client support team](http://datahug.com/about/contact-us/) tooget these values.</span></span> 

5. <span data-ttu-id="80a7e-170">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="80a7e-170">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_certificate.png) 

6.  <span data-ttu-id="80a7e-172">Sprawdź **"Pokaż zaawansowane ustawienia podpisywania certyfikatu"** i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="80a7e-172">Check **“Show advanced certificate signing settings”** and perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_cert.png)

    <span data-ttu-id="80a7e-174">a.</span><span class="sxs-lookup"><span data-stu-id="80a7e-174">a.</span></span> <span data-ttu-id="80a7e-175">W **opcja podpisywania**, wybierz pozycję **potwierdzenia języka SAML logowania**.</span><span class="sxs-lookup"><span data-stu-id="80a7e-175">In **Signing Option**, select **Sign SAML assertion**.</span></span>
    
    <span data-ttu-id="80a7e-176">b.</span><span class="sxs-lookup"><span data-stu-id="80a7e-176">b.</span></span> <span data-ttu-id="80a7e-177">W **algorytm podpisywania**, wybierz pozycję **SHA1**.</span><span class="sxs-lookup"><span data-stu-id="80a7e-177">In **Signing algorithm**, select **SHA1**.</span></span>
 
7. <span data-ttu-id="80a7e-178">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="80a7e-178">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-datahug-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="80a7e-180">Na powitania **konfiguracji Datahug** kliknij **skonfigurować Datahug** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="80a7e-180">On hello **Datahug Configuration** section, click **Configure Datahug** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="80a7e-181">Kopiuj hello **SAML identyfikator jednostki** i **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="80a7e-181">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_configure.png) 

9. <span data-ttu-id="80a7e-183">tooconfigure rejestracji jednokrotnej w **Datahug** strony, należy pobrać hello toosend **XML metadanych**, **identyfikator jednostki SAML** i **SAML logowania jednokrotnego usługi pojedynczej Adres URL** za[Obsługa Datahug](http://datahug.com/about/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="80a7e-183">tooconfigure single sign-on on **Datahug** side, you need toosend hello downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** too[Datahug support](http://datahug.com/about/contact-us/).</span></span> <span data-ttu-id="80a7e-184">Ustaw one tej aplikacji hello toohave prawidłowo po obu stronach połączenia logowania jednokrotnego SAML.</span><span class="sxs-lookup"><span data-stu-id="80a7e-184">They set this application up toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="80a7e-185">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="80a7e-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="80a7e-186">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="80a7e-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="80a7e-187">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="80a7e-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="80a7e-188">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="80a7e-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="80a7e-189">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="80a7e-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="80a7e-191">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="80a7e-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="80a7e-192">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="80a7e-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="80a7e-194">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="80a7e-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="80a7e-196">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="80a7e-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="80a7e-198">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="80a7e-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="80a7e-200">a.</span><span class="sxs-lookup"><span data-stu-id="80a7e-200">a.</span></span> <span data-ttu-id="80a7e-201">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="80a7e-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="80a7e-202">b.</span><span class="sxs-lookup"><span data-stu-id="80a7e-202">b.</span></span> <span data-ttu-id="80a7e-203">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="80a7e-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="80a7e-204">c.</span><span class="sxs-lookup"><span data-stu-id="80a7e-204">c.</span></span> <span data-ttu-id="80a7e-205">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="80a7e-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="80a7e-206">d.</span><span class="sxs-lookup"><span data-stu-id="80a7e-206">d.</span></span> <span data-ttu-id="80a7e-207">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="80a7e-207">Click **Create**.</span></span>
 
### <a name="creating-a-datahug-test-user"></a><span data-ttu-id="80a7e-208">Tworzenie użytkownika testowego Datahug</span><span class="sxs-lookup"><span data-stu-id="80a7e-208">Creating a Datahug test user</span></span>

<span data-ttu-id="80a7e-209">toolog użytkowników tooenable usługi Azure AD w tooDatahug, muszą mieć przydzielone do Datahug.</span><span class="sxs-lookup"><span data-stu-id="80a7e-209">tooenable Azure AD users toolog in tooDatahug, they must be provisioned into Datahug.</span></span>  
<span data-ttu-id="80a7e-210">Gdy Datahug, inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="80a7e-210">When Datahug, provisioning is a manual task.</span></span>

<span data-ttu-id="80a7e-211">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="80a7e-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="80a7e-212">Zaloguj się za tooyour Datahug witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="80a7e-212">Log in tooyour Datahug company site as an administrator.</span></span>

2. <span data-ttu-id="80a7e-213">Umieść kursor nad hello **koło zębate** w prawym górnym rogu hello i kliknij **ustawienia**</span><span class="sxs-lookup"><span data-stu-id="80a7e-213">Hover over hello **cog** in hello top right-hand corner and click **Settings**</span></span>
   
   ![Dodawanie pracownika](./media/active-directory-saas-datahug-tutorial/1.png)

3. <span data-ttu-id="80a7e-215">Wybierz **osób** i kliknij przycisk hello **Dodaj użytkowników** kartę</span><span class="sxs-lookup"><span data-stu-id="80a7e-215">Choose **People** and click hello **Add Users** tab</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-datahug-tutorial/2.png)

4. <span data-ttu-id="80a7e-217">Wpisz adres e-mail hello hello osoby, które chcesz toocreate konta dla i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="80a7e-217">Type hello email of hello person you would like toocreate an account for and click **Add**.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-datahug-tutorial/3.png)

    > [!NOTE] 
    > <span data-ttu-id="80a7e-219">Możesz wysłać toouser poczty rejestracji, wybierając **wysyłania powitalnej wiadomości e-mail** wyboru.</span><span class="sxs-lookup"><span data-stu-id="80a7e-219">You can send registration mail toouser by selecting **Send welcome email** checkbox.</span></span>  
    > <span data-ttu-id="80a7e-220">Jeśli tworzysz konto Salesforce nie wysyłaj hello powitalnej wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="80a7e-220">If you are creating an account for Salesforce do not send hello welcome email.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="80a7e-221">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="80a7e-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="80a7e-222">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooDatahug.</span><span class="sxs-lookup"><span data-stu-id="80a7e-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDatahug.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="80a7e-224">**tooassign tooDatahug Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="80a7e-224">**tooassign Britta Simon tooDatahug, perform hello following steps:**</span></span>

1. <span data-ttu-id="80a7e-225">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="80a7e-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="80a7e-227">Z listy aplikacji hello wybierz **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="80a7e-227">In hello applications list, select **Datahug**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_app.png) 

3. <span data-ttu-id="80a7e-229">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="80a7e-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="80a7e-231">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="80a7e-231">Click **Add** button.</span></span> <span data-ttu-id="80a7e-232">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="80a7e-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="80a7e-234">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="80a7e-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="80a7e-235">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="80a7e-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="80a7e-236">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="80a7e-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="80a7e-237">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="80a7e-237">Testing single sign-on</span></span>

<span data-ttu-id="80a7e-238">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="80a7e-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="80a7e-239">Po kliknięciu kafelka Datahug hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Datahug aplikacji.</span><span class="sxs-lookup"><span data-stu-id="80a7e-239">When you click hello Datahug tile in hello Access Panel, you should get automatically signed-on tooyour Datahug application.</span></span> <span data-ttu-id="80a7e-240">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="80a7e-240">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="80a7e-241">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="80a7e-241">Additional resources</span></span>

* [<span data-ttu-id="80a7e-242">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="80a7e-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="80a7e-243">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="80a7e-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_203.png

