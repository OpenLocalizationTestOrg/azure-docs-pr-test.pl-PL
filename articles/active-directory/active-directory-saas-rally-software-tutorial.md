---
title: 'Samouczek: Azure Active Directory integracji z oprogramowaniem Rally | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między oprogramowaniem Rally i Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: c75c8b98ce7fab19964c13de5ad7e19ef3ebd0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a><span data-ttu-id="1ad56-103">Samouczek: Azure Active Directory integracji z oprogramowaniem Rally</span><span class="sxs-lookup"><span data-stu-id="1ad56-103">Tutorial: Azure Active Directory integration with Rally Software</span></span>

<span data-ttu-id="1ad56-104">Z tego samouczka, dowiesz się, jak toointegrate Rally oprogramowania z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1ad56-104">In this tutorial, you learn how toointegrate Rally Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1ad56-105">Integrowanie Rally oprogramowania z usługi Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="1ad56-105">Integrating Rally Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1ad56-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooRally oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="1ad56-106">You can control in Azure AD who has access tooRally Software.</span></span>
- <span data-ttu-id="1ad56-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooRally oprogramowania (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ad56-107">You can enable your users tooautomatically get signed-on tooRally Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="1ad56-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1ad56-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="1ad56-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1ad56-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ad56-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1ad56-110">Prerequisites</span></span>

<span data-ttu-id="1ad56-111">tooconfigure integracji usługi Azure AD z oprogramowaniem Rally należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="1ad56-111">tooconfigure Azure AD integration with Rally Software, you need hello following items:</span></span>

- <span data-ttu-id="1ad56-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ad56-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1ad56-113">Oprogramowanie Rally logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1ad56-113">A Rally Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1ad56-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="1ad56-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1ad56-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="1ad56-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1ad56-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="1ad56-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1ad56-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1ad56-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1ad56-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="1ad56-118">Scenario description</span></span>
<span data-ttu-id="1ad56-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="1ad56-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1ad56-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="1ad56-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1ad56-121">Dodawanie oprogramowania Rally z galerii hello</span><span class="sxs-lookup"><span data-stu-id="1ad56-121">Adding Rally Software from hello gallery</span></span>
2. <span data-ttu-id="1ad56-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="1ad56-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rally-software-from-hello-gallery"></a><span data-ttu-id="1ad56-123">Dodawanie oprogramowania Rally z galerii hello</span><span class="sxs-lookup"><span data-stu-id="1ad56-123">Adding Rally Software from hello gallery</span></span>
<span data-ttu-id="1ad56-124">tooconfigure hello integracji Rally oprogramowania do usługi Azure AD, należy tooadd Rally oprogramowania z listy tooyour galerii hello zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="1ad56-124">tooconfigure hello integration of Rally Software into Azure AD, you need tooadd Rally Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1ad56-125">**tooadd Rally oprogramowania z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="1ad56-125">**tooadd Rally Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1ad56-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="1ad56-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="1ad56-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="1ad56-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1ad56-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1ad56-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="1ad56-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1ad56-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="1ad56-133">W polu wyszukiwania hello wpisz **Rally oprogramowania**, wybierz pozycję **Rally oprogramowania** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1ad56-133">In hello search box, type **Rally Software**, select **Rally Software** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Rally oprogramowania hello listy wyników](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1ad56-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1ad56-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="1ad56-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z oprogramowaniem Rally w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="1ad56-136">In this section, you configure and test Azure AD single sign-on with Rally Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1ad56-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello Rally oprogramowania jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ad56-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Rally Software is tooa user in Azure AD.</span></span> <span data-ttu-id="1ad56-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w oprogramowaniu Rally musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="1ad56-138">In other words, a link relationship between an Azure AD user and hello related user in Rally Software needs toobe established.</span></span>

<span data-ttu-id="1ad56-139">Rally oprogramowania, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="1ad56-139">In Rally Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1ad56-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z oprogramowaniem Rally, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="1ad56-140">tooconfigure and test Azure AD single sign-on with Rally Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1ad56-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="1ad56-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1ad56-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1ad56-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1ad56-143">**[Tworzenie użytkownika testowego Rally oprogramowania](#create-a-rally-software-test-user)**  -toohave odpowiednikiem Simona Britta Rally oprogramowania, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1ad56-143">**[Create a Rally Software test user](#create-a-rally-software-test-user)** - toohave a counterpart of Britta Simon in Rally Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1ad56-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1ad56-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1ad56-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="1ad56-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1ad56-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1ad56-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1ad56-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji Rally oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="1ad56-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Rally Software application.</span></span>

<span data-ttu-id="1ad56-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z oprogramowaniem Rally, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="1ad56-148">**tooconfigure Azure AD single sign-on with Rally Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="1ad56-149">W portalu Azure na powitania hello **Rally oprogramowania** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="1ad56-149">In hello Azure portal, on hello **Rally Software** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="1ad56-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1ad56-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

3. <span data-ttu-id="1ad56-153">Na powitania **Rally domeny oprogramowania i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1ad56-153">On hello **Rally Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Rally domeny oprogramowania i adres URL pojedynczego logowania jednokrotnego informacji](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_url.png)

    <span data-ttu-id="1ad56-155">a.</span><span class="sxs-lookup"><span data-stu-id="1ad56-155">a.</span></span> <span data-ttu-id="1ad56-156">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="1ad56-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.rally.com`</span></span>

    <span data-ttu-id="1ad56-157">b.</span><span class="sxs-lookup"><span data-stu-id="1ad56-157">b.</span></span> <span data-ttu-id="1ad56-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="1ad56-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.rally.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1ad56-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="1ad56-159">These values are not real.</span></span> <span data-ttu-id="1ad56-160">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="1ad56-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1ad56-161">Skontaktuj się z [zespołem pomocy technicznej klienta oprogramowania Rally](https://help.rallydev.com/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="1ad56-161">Contact [Rally Software Client support team](https://help.rallydev.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="1ad56-162">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="1ad56-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

5. <span data-ttu-id="1ad56-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1ad56-164">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-rally-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1ad56-166">Na powitania **Rally konfiguracji oprogramowania** kliknij **Konfigurowanie oprogramowania Rally** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="1ad56-166">On hello **Rally Software Configuration** section, click **Configure Rally Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1ad56-167">Kopia hello **Sign-Out adresu URL i identyfikator jednostki SAML** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="1ad56-167">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Rally konfiguracji oprogramowania](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_configure.png) 

7. <span data-ttu-id="1ad56-169">Zaloguj się za tooyour **Rally oprogramowania** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="1ad56-169">Log in tooyour **Rally Software** tenant.</span></span>

8. <span data-ttu-id="1ad56-170">Witaj pasku narzędzi u góry hello, kliknij przycisk **Instalatora**, a następnie wybierz **subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="1ad56-170">In hello toolbar on hello top, click **Setup**, and then select **Subscription**.</span></span>
   
    <span data-ttu-id="1ad56-171">![Subskrypcja](./media/active-directory-saas-rally-software-tutorial/ic769531.png "subskrypcji")</span><span class="sxs-lookup"><span data-stu-id="1ad56-171">![Subscription](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Subscription")</span></span>

9. <span data-ttu-id="1ad56-172">Kliknij przycisk hello **akcji** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1ad56-172">Click hello **Action** button.</span></span> <span data-ttu-id="1ad56-173">Wybierz **edytować subskrypcji** na powitania górnym rogu paska narzędzi hello.</span><span class="sxs-lookup"><span data-stu-id="1ad56-173">Select **Edit Subscription** at hello top right side of hello toolbar.</span></span>

10. <span data-ttu-id="1ad56-174">Na powitania **subskrypcji** strony okna dialogowego, wykonaj następujące kroki hello, a następnie kliknij **Zapisz i Zamknij**:</span><span class="sxs-lookup"><span data-stu-id="1ad56-174">On hello **Subscription** dialog page, perform hello following steps, and then click **Save & Close**:</span></span>
   
    <span data-ttu-id="1ad56-175">![Uwierzytelnianie](./media/active-directory-saas-rally-software-tutorial/ic769542.png "uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="1ad56-175">![Authentication](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Authentication")</span></span>
   
    <span data-ttu-id="1ad56-176">a.</span><span class="sxs-lookup"><span data-stu-id="1ad56-176">a.</span></span> <span data-ttu-id="1ad56-177">Wybierz **uwierzytelniania Rally lub logowania jednokrotnego** z listy rozwijanej uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="1ad56-177">Select **Rally or SSO authentication** from Authentication dropdown.</span></span>

    <span data-ttu-id="1ad56-178">b.</span><span class="sxs-lookup"><span data-stu-id="1ad56-178">b.</span></span> <span data-ttu-id="1ad56-179">W hello **adres URL dostawcy tożsamości** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1ad56-179">In hello **Identity provider URL** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="1ad56-180">c.</span><span class="sxs-lookup"><span data-stu-id="1ad56-180">c.</span></span> <span data-ttu-id="1ad56-181">W hello **wylogowania logowania jednokrotnego** pole tekstowe, Wklej hello wartość **Sign-Out URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1ad56-181">In hello **SSO Logout** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="1ad56-182">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="1ad56-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1ad56-183">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="1ad56-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1ad56-184">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1ad56-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1ad56-185">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ad56-185">Create an Azure AD test user</span></span>

<span data-ttu-id="1ad56-186">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="1ad56-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="1ad56-188">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="1ad56-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1ad56-189">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1ad56-189">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-rally-software-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="1ad56-191">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="1ad56-191">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-rally-software-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="1ad56-193">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="1ad56-193">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-rally-software-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="1ad56-195">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1ad56-195">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-rally-software-tutorial/create_aaduser_04.png)

    <span data-ttu-id="1ad56-197">a.</span><span class="sxs-lookup"><span data-stu-id="1ad56-197">a.</span></span> <span data-ttu-id="1ad56-198">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1ad56-198">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1ad56-199">b.</span><span class="sxs-lookup"><span data-stu-id="1ad56-199">b.</span></span> <span data-ttu-id="1ad56-200">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1ad56-200">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="1ad56-201">c.</span><span class="sxs-lookup"><span data-stu-id="1ad56-201">c.</span></span> <span data-ttu-id="1ad56-202">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="1ad56-202">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="1ad56-203">d.</span><span class="sxs-lookup"><span data-stu-id="1ad56-203">d.</span></span> <span data-ttu-id="1ad56-204">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1ad56-204">Click **Create**.</span></span>
 
### <a name="create-a-rally-software-test-user"></a><span data-ttu-id="1ad56-205">Tworzenie użytkownika testowego Rally oprogramowania</span><span class="sxs-lookup"><span data-stu-id="1ad56-205">Create a Rally Software test user</span></span>

<span data-ttu-id="1ad56-206">Dla usługi Azure AD użytkownicy toobe stanie toosign w muszą być elastycznie toohello Rally aplikacji przy użyciu nazwy użytkowników usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1ad56-206">For Azure AD users toobe able toosign in, they must be provisioned toohello Rally Software application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="1ad56-207">**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="1ad56-207">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="1ad56-208">Zaloguj się za tooyour dzierżawy Rally oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="1ad56-208">Log in tooyour Rally Software tenant.</span></span>

2. <span data-ttu-id="1ad56-209">Przejdź za**Instalator \> użytkowników**, a następnie kliknij przycisk **+ Dodaj nowy**.</span><span class="sxs-lookup"><span data-stu-id="1ad56-209">Go too**Setup \> USERS**, and then click **+ Add New**.</span></span>
   
    <span data-ttu-id="1ad56-210">![Użytkownicy](./media/active-directory-saas-rally-software-tutorial/ic781039.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="1ad56-210">![Users](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Users")</span></span>

3. <span data-ttu-id="1ad56-211">Wpisz nazwę hello w hello nowego użytkownika w polu tekstowym, a następnie kliknij przycisk **Dodaj szczegóły**.</span><span class="sxs-lookup"><span data-stu-id="1ad56-211">Type hello name in hello New User textbox, and then click **Add with Details**.</span></span>

4. <span data-ttu-id="1ad56-212">W hello **Tworzenie użytkownika** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1ad56-212">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="1ad56-213">![Utwórz użytkownika](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Tworzenie użytkownika")</span><span class="sxs-lookup"><span data-stu-id="1ad56-213">![Create User](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Create User")</span></span>

    <span data-ttu-id="1ad56-214">a.</span><span class="sxs-lookup"><span data-stu-id="1ad56-214">a.</span></span> <span data-ttu-id="1ad56-215">W hello **nazwy użytkownika** pole tekstowe, nazwę użytkownika, takie jak hello typu **Brittsimon**.</span><span class="sxs-lookup"><span data-stu-id="1ad56-215">In hello **User Name** textbox, type hello name of user like **Brittsimon**.</span></span>
   
    <span data-ttu-id="1ad56-216">b.</span><span class="sxs-lookup"><span data-stu-id="1ad56-216">b.</span></span> <span data-ttu-id="1ad56-217">W **adres E-mail** pole tekstowe, wprowadź adres e-mail użytkownika, takie jak hello  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="1ad56-217">In **E-mail Address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="1ad56-218">c.</span><span class="sxs-lookup"><span data-stu-id="1ad56-218">c.</span></span> <span data-ttu-id="1ad56-219">W **imię** tekst Wprowadź hello imię użytkownika, takich jak **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1ad56-219">In **First Name** text box, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="1ad56-220">d.</span><span class="sxs-lookup"><span data-stu-id="1ad56-220">d.</span></span> <span data-ttu-id="1ad56-221">W **nazwisko** tekst Wprowadź hello nazwisko użytkownika, takich jak **Simona**.</span><span class="sxs-lookup"><span data-stu-id="1ad56-221">In **Last Name** text box, enter hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="1ad56-222">e.</span><span class="sxs-lookup"><span data-stu-id="1ad56-222">e.</span></span> <span data-ttu-id="1ad56-223">Kliknij przycisk **Zapisz i Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="1ad56-223">Click **Save & Close**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="1ad56-224">Możesz użyć innych Rally oprogramowania użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision Rally oprogramowania kont użytkowników usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ad56-224">You can use any other Rally Software user account creation tools or APIs provided by Rally Software tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="1ad56-225">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ad56-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="1ad56-226">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooRally oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="1ad56-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRally Software.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="1ad56-228">**tooassign tooRally Simona Britta oprogramowania, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="1ad56-228">**tooassign Britta Simon tooRally Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="1ad56-229">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1ad56-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="1ad56-231">Z listy aplikacji hello wybierz **Rally oprogramowania**.</span><span class="sxs-lookup"><span data-stu-id="1ad56-231">In hello applications list, select **Rally Software**.</span></span>

    ![łącze Rally oprogramowania Hello na liście aplikacji hello](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_app.png)  

3. <span data-ttu-id="1ad56-233">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="1ad56-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="1ad56-235">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1ad56-235">Click **Add** button.</span></span> <span data-ttu-id="1ad56-236">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1ad56-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="1ad56-238">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="1ad56-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1ad56-239">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1ad56-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1ad56-240">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1ad56-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1ad56-241">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1ad56-241">Test single sign-on</span></span>

<span data-ttu-id="1ad56-242">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1ad56-242">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1ad56-243">Po kliknięciu kafelka Rally oprogramowania hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Rally aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1ad56-243">When you click hello Rally Software tile in hello Access Panel, you should get automatically signed-on tooyour Rally Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1ad56-244">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="1ad56-244">Additional resources</span></span>

* [<span data-ttu-id="1ad56-245">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ad56-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1ad56-246">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1ad56-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_203.png

