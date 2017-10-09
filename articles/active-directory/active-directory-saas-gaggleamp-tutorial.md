---
title: 'Samouczek: Integracji Azure Active Directory z GaggleAMP | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i GaggleAMP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9cc1a4b7-964b-406b-9e0c-05cb1a7c9856
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9761019a79f935b6695a5ae1214c256c887df457
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gaggleamp"></a><span data-ttu-id="ce0b7-103">Samouczek: Integracji Azure Active Directory z GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="ce0b7-103">Tutorial: Azure Active Directory integration with GaggleAMP</span></span>

<span data-ttu-id="ce0b7-104">Z tego samouczka, dowiesz się, jak toointegrate GaggleAMP w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ce0b7-104">In this tutorial, you learn how toointegrate GaggleAMP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ce0b7-105">Integracja z usługą Azure AD GaggleAMP zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ce0b7-105">Integrating GaggleAMP with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ce0b7-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooGaggleAMP</span><span class="sxs-lookup"><span data-stu-id="ce0b7-106">You can control in Azure AD who has access tooGaggleAMP</span></span>
- <span data-ttu-id="ce0b7-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooGaggleAMP (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce0b7-107">You can enable your users tooautomatically get signed-on tooGaggleAMP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ce0b7-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ce0b7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ce0b7-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ce0b7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce0b7-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ce0b7-110">Prerequisites</span></span>

<span data-ttu-id="ce0b7-111">tooconfigure integracji z usługą Azure AD z GaggleAMP należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ce0b7-111">tooconfigure Azure AD integration with GaggleAMP, you need hello following items:</span></span>

- <span data-ttu-id="ce0b7-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce0b7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ce0b7-113">GaggleAMP jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ce0b7-113">A GaggleAMP single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ce0b7-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ce0b7-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ce0b7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ce0b7-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ce0b7-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ce0b7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ce0b7-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ce0b7-118">Scenario description</span></span>
<span data-ttu-id="ce0b7-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ce0b7-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ce0b7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ce0b7-121">Dodawanie GaggleAMP z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ce0b7-121">Adding GaggleAMP from hello gallery</span></span>
2. <span data-ttu-id="ce0b7-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ce0b7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gaggleamp-from-hello-gallery"></a><span data-ttu-id="ce0b7-123">Dodawanie GaggleAMP z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ce0b7-123">Adding GaggleAMP from hello gallery</span></span>
<span data-ttu-id="ce0b7-124">tooconfigure hello integracji GaggleAMP do usługi Azure AD, należy tooadd GaggleAMP z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-124">tooconfigure hello integration of GaggleAMP into Azure AD, you need tooadd GaggleAMP from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ce0b7-125">**tooadd GaggleAMP z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ce0b7-125">**tooadd GaggleAMP from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce0b7-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="ce0b7-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ce0b7-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ce0b7-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ce0b7-133">W polu wyszukiwania hello wpisz **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-133">In hello search box, type **GaggleAMP**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_search.png)

5. <span data-ttu-id="ce0b7-135">W panelu wyników hello zaznacz **GaggleAMP**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-135">In hello results panel, select **GaggleAMP**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ce0b7-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ce0b7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ce0b7-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z GaggleAMP w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-138">In this section, you configure and test Azure AD single sign-on with GaggleAMP based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ce0b7-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w GaggleAMP jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in GaggleAMP is tooa user in Azure AD.</span></span> <span data-ttu-id="ce0b7-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w GaggleAMP musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-140">In other words, a link relationship between an Azure AD user and hello related user in GaggleAMP needs toobe established.</span></span>

<span data-ttu-id="ce0b7-141">W GaggleAMP, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-141">In GaggleAMP, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ce0b7-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z GaggleAMP, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ce0b7-142">tooconfigure and test Azure AD single sign-on with GaggleAMP, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ce0b7-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ce0b7-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ce0b7-145">**[Tworzenie użytkownika testowego GaggleAMP](#creating-a-gaggleamp-test-user)**  -toohave odpowiednikiem Simona Britta w GaggleAMP, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-145">**[Creating a GaggleAMP test user](#creating-a-gaggleamp-test-user)** - toohave a counterpart of Britta Simon in GaggleAMP that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ce0b7-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ce0b7-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ce0b7-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ce0b7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ce0b7-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your GaggleAMP application.</span></span>

<span data-ttu-id="ce0b7-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z GaggleAMP, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ce0b7-150">**tooconfigure Azure AD single sign-on with GaggleAMP, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce0b7-151">W portalu Azure na powitania hello **GaggleAMP** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-151">In hello Azure portal, on hello **GaggleAMP** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="ce0b7-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_samlbase.png)

3. <span data-ttu-id="ce0b7-155">Na powitania **GaggleAMP domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ce0b7-155">On hello **GaggleAMP Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_url.png)

     <span data-ttu-id="ce0b7-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.gaggleamp.com`</span><span class="sxs-lookup"><span data-stu-id="ce0b7-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.gaggleamp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ce0b7-158">wartość Hello nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-158">hello value is not real.</span></span> <span data-ttu-id="ce0b7-159">Wartość hello aktualizacji z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="ce0b7-160">Skontaktuj się z [zespołem pomocy technicznej klienta GaggleAMP](mailto:sales@gaggleamp.com) tooget hello wartość.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-160">Contact [GaggleAMP Client support team](mailto:sales@gaggleamp.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="ce0b7-161">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_certificate.png) 

5. <span data-ttu-id="ce0b7-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ce0b7-165">Na powitania **konfiguracji GaggleAMP** kliknij **skonfigurować GaggleAMP** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-165">On hello **GaggleAMP Configuration** section, click **Configure GaggleAMP** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ce0b7-166">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="ce0b7-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_configure.png) 

7. <span data-ttu-id="ce0b7-168">W innym wystąpieniu przeglądarki, przejdź toohello strona logowania jednokrotnego SAML utworzona przez hello Gaggle obsługuje team (na przykład: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span><span class="sxs-lookup"><span data-stu-id="ce0b7-168">In another browser instance, navigate toohello SAML SSO page created for you by hello Gaggle support team (for example: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span></span>

8. <span data-ttu-id="ce0b7-169">W Twojej **logowania jednokrotnego SAML** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ce0b7-169">On your **SAML SSO** page, perform hello following steps:</span></span>  
   
    ![GaggleAMP rejestracji jednokrotnej](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_06.png) 
 
    <span data-ttu-id="ce0b7-171">a.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-171">a.</span></span> <span data-ttu-id="ce0b7-172">W hello **wystawcy dostawcy tożsamości** pole tekstowe, Wklej wartość hello **adres URL wystawcy** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-172">In hello **Identity Provider Issuer** textbox, paste hello value of **Issuer URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="ce0b7-173">b.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-173">b.</span></span> <span data-ttu-id="ce0b7-174">W hello **tożsamości dostawcy pojedynczy adres URL logowania** pole tekstowe, Wklej wartość hello **pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-174">In hello **Identity Provider Single Sign-On URL** textbox, paste hello  value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="ce0b7-175">c.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-175">c.</span></span> <span data-ttu-id="ce0b7-176">Kliknij przycisk **Zapisz**</span><span class="sxs-lookup"><span data-stu-id="ce0b7-176">Click **Save**</span></span>      

    <span data-ttu-id="ce0b7-177">d.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-177">d.</span></span> <span data-ttu-id="ce0b7-178">Wyślij hello **certyfikatu (Base64)** certyfikatu tooyour [zespołem pomocy technicznej GaggleAMP](mailto:sales@gaggleamp.com).</span><span class="sxs-lookup"><span data-stu-id="ce0b7-178">Send hello **Certificate (Base64)** certificate tooyour [GaggleAMP support team](mailto:sales@gaggleamp.com).</span></span>

> [!TIP]
> <span data-ttu-id="ce0b7-179">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="ce0b7-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ce0b7-180">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ce0b7-181">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ce0b7-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ce0b7-182">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce0b7-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="ce0b7-183">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="ce0b7-185">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ce0b7-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce0b7-186">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ce0b7-188">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ce0b7-190">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ce0b7-192">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ce0b7-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ce0b7-194">a.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-194">a.</span></span> <span data-ttu-id="ce0b7-195">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ce0b7-196">b.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-196">b.</span></span> <span data-ttu-id="ce0b7-197">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ce0b7-198">c.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-198">c.</span></span> <span data-ttu-id="ce0b7-199">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ce0b7-200">d.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-200">d.</span></span> <span data-ttu-id="ce0b7-201">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-201">Click **Create**.</span></span>
 
### <a name="creating-a-gaggleamp-test-user"></a><span data-ttu-id="ce0b7-202">Tworzenie użytkownika testowego GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="ce0b7-202">Creating a GaggleAMP test user</span></span>

<span data-ttu-id="ce0b7-203">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-203">hello objective of this section is toocreate a user called Britta Simon in GaggleAMP.</span></span> <span data-ttu-id="ce0b7-204">GaggleAMP obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-204">GaggleAMP supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="ce0b7-205">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-205">There is no action item for you in this section.</span></span> <span data-ttu-id="ce0b7-206">Nowy użytkownik jest tworzona podczas próby tooaccess GaggleAMP, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-206">A new user is created during an attempt tooaccess GaggleAMP if it doesn't exist yet.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ce0b7-207">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce0b7-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ce0b7-208">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooGaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGaggleAMP.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="ce0b7-210">**tooassign tooGaggleAMP Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ce0b7-210">**tooassign Britta Simon tooGaggleAMP, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce0b7-211">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ce0b7-213">Z listy aplikacji hello wybierz **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-213">In hello applications list, select **GaggleAMP**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_app.png) 

3. <span data-ttu-id="ce0b7-215">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="ce0b7-217">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-217">Click **Add** button.</span></span> <span data-ttu-id="ce0b7-218">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="ce0b7-220">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ce0b7-221">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ce0b7-222">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ce0b7-223">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ce0b7-223">Testing single sign-on</span></span>

<span data-ttu-id="ce0b7-224">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-224">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="ce0b7-225">Po kliknięciu kafelka GaggleAMP hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour GaggleAMP aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ce0b7-225">When you click hello GaggleAMP tile in hello Access Panel, you should get automatically signed-on tooyour GaggleAMP application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ce0b7-226">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ce0b7-226">Additional resources</span></span>

* [<span data-ttu-id="ce0b7-227">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ce0b7-227">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ce0b7-228">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ce0b7-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_203.png

