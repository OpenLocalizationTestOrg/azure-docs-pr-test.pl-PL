---
title: 'Samouczek: Integracji Azure Active Directory z obrazu przekazywania | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i przekazywania obrazu."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: baf39e4437b85c2de5b524984ad5ca39badbab63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a><span data-ttu-id="e63b0-103">Samouczek: Integracji Azure Active Directory z przekaźnika obrazu</span><span class="sxs-lookup"><span data-stu-id="e63b0-103">Tutorial: Azure Active Directory integration with Image Relay</span></span>

<span data-ttu-id="e63b0-104">Z tego samouczka, dowiesz się, jak toointegrate przekazywania obrazu w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e63b0-104">In this tutorial, you learn how toointegrate Image Relay with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e63b0-105">Integrowanie przekazywania obrazu z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e63b0-105">Integrating Image Relay with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e63b0-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooImage przekazywania</span><span class="sxs-lookup"><span data-stu-id="e63b0-106">You can control in Azure AD who has access tooImage Relay</span></span>
- <span data-ttu-id="e63b0-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooImage przekazywania (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e63b0-107">You can enable your users tooautomatically get signed-on tooImage Relay (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e63b0-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e63b0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e63b0-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e63b0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e63b0-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e63b0-110">Prerequisites</span></span>

<span data-ttu-id="e63b0-111">tooconfigure integracji usługi Azure AD z przekaźnika obrazu należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e63b0-111">tooconfigure Azure AD integration with Image Relay, you need hello following items:</span></span>

- <span data-ttu-id="e63b0-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e63b0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e63b0-113">Obraz przekazywania logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e63b0-113">An Image Relay single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e63b0-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e63b0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e63b0-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="e63b0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e63b0-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e63b0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e63b0-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e63b0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e63b0-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="e63b0-118">Scenario description</span></span>
<span data-ttu-id="e63b0-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="e63b0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e63b0-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="e63b0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e63b0-121">Dodawanie obrazu przekazywania z galerii hello</span><span class="sxs-lookup"><span data-stu-id="e63b0-121">Adding Image Relay from hello gallery</span></span>
2. <span data-ttu-id="e63b0-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e63b0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-image-relay-from-hello-gallery"></a><span data-ttu-id="e63b0-123">Dodawanie obrazu przekazywania z galerii hello</span><span class="sxs-lookup"><span data-stu-id="e63b0-123">Adding Image Relay from hello gallery</span></span>
<span data-ttu-id="e63b0-124">tooconfigure hello integrację przekaźnika obrazu usługi Azure AD, należy tooadd przekazywania obrazu z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="e63b0-124">tooconfigure hello integration of Image Relay into Azure AD, you need tooadd Image Relay from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e63b0-125">**tooadd przekazywania obrazu z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e63b0-125">**tooadd Image Relay from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e63b0-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e63b0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="e63b0-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e63b0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e63b0-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e63b0-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="e63b0-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e63b0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="e63b0-133">W polu wyszukiwania hello wpisz **przekazywania obrazu**.</span><span class="sxs-lookup"><span data-stu-id="e63b0-133">In hello search box, type **Image Relay**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_search.png)

5. <span data-ttu-id="e63b0-135">W panelu wyników hello, wybierz **przekazywania obrazu**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="e63b0-135">In hello results panel, select **Image Relay**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e63b0-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e63b0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e63b0-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z przekaźnika obraz w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="e63b0-138">In this section, you configure and test Azure AD single sign-on with Image Relay based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e63b0-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w przekazywania obrazu jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e63b0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Image Relay is tooa user in Azure AD.</span></span> <span data-ttu-id="e63b0-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w przekazywania obrazu musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="e63b0-140">In other words, a link relationship between an Azure AD user and hello related user in Image Relay needs toobe established.</span></span>

<span data-ttu-id="e63b0-141">W przekazywania obrazu, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="e63b0-141">In Image Relay, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e63b0-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z przekaźnika obrazu, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="e63b0-142">tooconfigure and test Azure AD single sign-on with Image Relay, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e63b0-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e63b0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e63b0-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e63b0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e63b0-145">**[Tworzenie użytkownika testowego przekazywania obrazu](#creating-an-image-relay-test-user)**  -toohave odpowiednikiem Simona Britta w przekazywania obrazu, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e63b0-145">**[Creating an Image Relay test user](#creating-an-image-relay-test-user)** - toohave a counterpart of Britta Simon in Image Relay that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e63b0-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e63b0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e63b0-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="e63b0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e63b0-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e63b0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e63b0-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji przekaźnika obrazu.</span><span class="sxs-lookup"><span data-stu-id="e63b0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Image Relay application.</span></span>

<span data-ttu-id="e63b0-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z obrazu przekazywania, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e63b0-150">**tooconfigure Azure AD single sign-on with Image Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="e63b0-151">W portalu Azure na powitania hello **przekazywania obrazu** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e63b0-151">In hello Azure portal, on hello **Image Relay** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="e63b0-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e63b0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_samlbase.png)

3. <span data-ttu-id="e63b0-155">Na powitania **obrazu przekazywania domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="e63b0-155">On hello **Image Relay Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_url.png)

    <span data-ttu-id="e63b0-157">a.</span><span class="sxs-lookup"><span data-stu-id="e63b0-157">a.</span></span> <span data-ttu-id="e63b0-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.imagerelay.com/`</span><span class="sxs-lookup"><span data-stu-id="e63b0-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.imagerelay.com/`</span></span>

    <span data-ttu-id="e63b0-159">b.</span><span class="sxs-lookup"><span data-stu-id="e63b0-159">b.</span></span> <span data-ttu-id="e63b0-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.imagerelay.com/sso/metadata`</span><span class="sxs-lookup"><span data-stu-id="e63b0-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.imagerelay.com/sso/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e63b0-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="e63b0-161">These values are not real.</span></span> <span data-ttu-id="e63b0-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="e63b0-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e63b0-163">Skontaktuj się z [zespołem pomocy technicznej klienta przekazywania obrazu](http://support.imagerelay.com/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="e63b0-163">Contact [Image Relay Client support team](http://support.imagerelay.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="e63b0-164">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e63b0-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_certificate.png) 

5. <span data-ttu-id="e63b0-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e63b0-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e63b0-168">Na powitania **Konfiguracja przekazywania obrazu** kliknij **Konfigurowanie przekazywania obrazu** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="e63b0-168">On hello **Image Relay Configuration** section, click **Configure Image Relay** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e63b0-169">Kopiuj hello **Sign-Out adres URL usługi i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="e63b0-169">Copy hello **Sign-Out Service URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_configure.png) 

7. <span data-ttu-id="e63b0-171">W innym oknie przeglądarki Zaloguj się w witrynie firmy przekazywania obrazu tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e63b0-171">In another browser window, sign in tooyour Image Relay company site as an administrator.</span></span>

8. <span data-ttu-id="e63b0-172">Witaj pasku narzędzi u góry hello, kliknij przycisk hello **użytkowników i uprawnienia** obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e63b0-172">In hello toolbar on hello top, click hello **Users & Permissions** workload.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 

9. <span data-ttu-id="e63b0-174">Kliknij przycisk **utworzyć nowe uprawnienie**.</span><span class="sxs-lookup"><span data-stu-id="e63b0-174">Click **Create New Permission**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png)

10. <span data-ttu-id="e63b0-176">W hello **pojedynczy znak na ustawienia** obciążenie, wybierz hello **tej grupie można tylko logowania za pomocą rejestracji jednokrotnej** pole wyboru, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="e63b0-176">In hello **Single Sign On Settings** workload, select hello **This Group can only sign-in via Single Sign On** check box, and then click **Save**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 

11. <span data-ttu-id="e63b0-178">Przejdź za**ustawienia konta**.</span><span class="sxs-lookup"><span data-stu-id="e63b0-178">Go too**Account Settings**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 

12. <span data-ttu-id="e63b0-180">Przejdź toohello **pojedynczy znak na ustawienia** obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e63b0-180">Go toohello **Single Sign On Settings** workload.</span></span>
    
     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)

13. <span data-ttu-id="e63b0-182">Na powitania **ustawienia SAML** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="e63b0-182">On hello **SAML Settings** dialog, perform hello following steps:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    <span data-ttu-id="e63b0-184">a.</span><span class="sxs-lookup"><span data-stu-id="e63b0-184">a.</span></span> <span data-ttu-id="e63b0-185">W **adres URL logowania** pole tekstowe, Wklej wartość hello **pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e63b0-185">In **Login URL** textbox, paste hello value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e63b0-186">b.</span><span class="sxs-lookup"><span data-stu-id="e63b0-186">b.</span></span> <span data-ttu-id="e63b0-187">W **adresu URL wylogowania** pole tekstowe, Wklej wartość hello **pojedynczy adres URL usługi Sign-Out** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e63b0-187">In **Logout URL**  textbox, paste hello value of **Single Sign-Out Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e63b0-188">c.</span><span class="sxs-lookup"><span data-stu-id="e63b0-188">c.</span></span> <span data-ttu-id="e63b0-189">Jako **Format identyfikatora nazwy**, wybierz pozycję **urn: oasis: nazwy: tc: SAML:1.1:nameid-format: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="e63b0-189">As **Name Id Format**, select **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="e63b0-190">d.</span><span class="sxs-lookup"><span data-stu-id="e63b0-190">d.</span></span> <span data-ttu-id="e63b0-191">Jako **powiązanie opcje dla żądań z hello dostawcy usług (obraz przekazywania)**, wybierz pozycję **powiązanie POST**.</span><span class="sxs-lookup"><span data-stu-id="e63b0-191">As **Binding Options for Requests from hello Service Provider (Image Relay)**, select **POST Binding**.</span></span>

    <span data-ttu-id="e63b0-192">e.</span><span class="sxs-lookup"><span data-stu-id="e63b0-192">e.</span></span> <span data-ttu-id="e63b0-193">W obszarze **certyfikatu x.509**, kliknij przycisk **certyfikatu aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="e63b0-193">Under **x.509 Certificate**, click **Update Certificate**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    <span data-ttu-id="e63b0-195">f.</span><span class="sxs-lookup"><span data-stu-id="e63b0-195">f.</span></span> <span data-ttu-id="e63b0-196">Otwórz w Notatniku hello pobrany certyfikat, skopiuj zawartość hello i wklej go w pole tekstowe certyfikatu x.509 hello.</span><span class="sxs-lookup"><span data-stu-id="e63b0-196">Open hello downloaded certificate in notepad, copy hello content, and then paste it into hello x.509 Certificate textbox.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    <span data-ttu-id="e63b0-198">g.</span><span class="sxs-lookup"><span data-stu-id="e63b0-198">g.</span></span> <span data-ttu-id="e63b0-199">W **Inicjowanie obsługi użytkowników just in Time** sekcji, wybierz hello **włączyć just in Time Inicjowanie obsługi użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="e63b0-199">In **Just-In-Time User Provisioning** section, select hello **Enable Just-In-Time User Provisioning**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    <span data-ttu-id="e63b0-201">h.</span><span class="sxs-lookup"><span data-stu-id="e63b0-201">h.</span></span> <span data-ttu-id="e63b0-202">Grupy uprawnień wybierz hello (na przykład **logowania jednokrotnego podstawowe**) co jest dozwolone toosign w tylko za pośrednictwem rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e63b0-202">Select hello permission group (for example, **SSO Basic**) which is allowed toosign in only through single sign-on.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    <span data-ttu-id="e63b0-204">i.</span><span class="sxs-lookup"><span data-stu-id="e63b0-204">i.</span></span> <span data-ttu-id="e63b0-205">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="e63b0-205">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e63b0-206">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="e63b0-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e63b0-207">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="e63b0-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e63b0-208">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e63b0-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e63b0-209">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e63b0-209">Creating an Azure AD test user</span></span>
<span data-ttu-id="e63b0-210">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="e63b0-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="e63b0-212">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e63b0-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e63b0-213">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e63b0-213">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e63b0-215">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="e63b0-215">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e63b0-217">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e63b0-217">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e63b0-219">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e63b0-219">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e63b0-221">a.</span><span class="sxs-lookup"><span data-stu-id="e63b0-221">a.</span></span> <span data-ttu-id="e63b0-222">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e63b0-222">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e63b0-223">b.</span><span class="sxs-lookup"><span data-stu-id="e63b0-223">b.</span></span> <span data-ttu-id="e63b0-224">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e63b0-224">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e63b0-225">c.</span><span class="sxs-lookup"><span data-stu-id="e63b0-225">c.</span></span> <span data-ttu-id="e63b0-226">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="e63b0-226">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e63b0-227">d.</span><span class="sxs-lookup"><span data-stu-id="e63b0-227">d.</span></span> <span data-ttu-id="e63b0-228">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e63b0-228">Click **Create**.</span></span>
 
### <a name="creating-an-image-relay-test-user"></a><span data-ttu-id="e63b0-229">Tworzenie użytkownika testowego przekazywania obrazu</span><span class="sxs-lookup"><span data-stu-id="e63b0-229">Creating an Image Relay test user</span></span>

<span data-ttu-id="e63b0-230">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w przekazywania obrazu.</span><span class="sxs-lookup"><span data-stu-id="e63b0-230">hello objective of this section is toocreate a user called Britta Simon in Image Relay.</span></span>

<span data-ttu-id="e63b0-231">**toocreate użytkownika o nazwie Simona Britta w przekazywania obrazu, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e63b0-231">**toocreate a user called Britta Simon in Image Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="e63b0-232">Logowania jednokrotnego tooyour przekazywania obrazu witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e63b0-232">Sign-on tooyour Image Relay company site as an administrator.</span></span>

2. <span data-ttu-id="e63b0-233">Przejdź za**użytkowników i uprawnienia** i wybierz **Tworzenie użytkownika logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="e63b0-233">Go too**Users & Permissions**     and select **Create SSO User**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 

3. <span data-ttu-id="e63b0-235">Wprowadź hello **E-mail**, **imię**, **nazwisko**, i **firmy** hello użytkownika ma tooprovision i wybierz hello uprawnień grupy (na przykład logowania jednokrotnego podstawowe) czyli hello grupę, której można zalogować się tylko za pośrednictwem rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e63b0-235">Enter hello **Email**, **First Name**, **Last Name**, and **Company** of hello user you want tooprovision and select hello permission group (for example, SSO Basic) which is hello group that can sign in only through single sign-on.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 

4. <span data-ttu-id="e63b0-237">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e63b0-237">Click **Create**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e63b0-238">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e63b0-238">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e63b0-239">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooImage przekazywania.</span><span class="sxs-lookup"><span data-stu-id="e63b0-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooImage Relay.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="e63b0-241">**tooassign tooImage Simona Britta przekazywania, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e63b0-241">**tooassign Britta Simon tooImage Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="e63b0-242">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e63b0-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="e63b0-244">Z listy aplikacji hello wybierz **przekazywania obrazu**.</span><span class="sxs-lookup"><span data-stu-id="e63b0-244">In hello applications list, select **Image Relay**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_app.png) 

3. <span data-ttu-id="e63b0-246">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e63b0-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="e63b0-248">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e63b0-248">Click **Add** button.</span></span> <span data-ttu-id="e63b0-249">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e63b0-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="e63b0-251">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e63b0-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e63b0-252">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e63b0-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e63b0-253">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e63b0-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e63b0-254">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e63b0-254">Testing single sign-on</span></span>

<span data-ttu-id="e63b0-255">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="e63b0-255">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>    

<span data-ttu-id="e63b0-256">Po kliknięciu kafelka przekazywania obraz powitania w hello panelu dostępu, należy pobrać automatycznie zalogowane tooyour obrazu przekazywania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e63b0-256">When you click hello Image Relay tile in hello Access Panel, you should get automatically signed-on tooyour Image Relay application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="e63b0-257">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e63b0-257">Additional resources</span></span>

* [<span data-ttu-id="e63b0-258">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e63b0-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e63b0-259">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e63b0-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png


[100]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png

