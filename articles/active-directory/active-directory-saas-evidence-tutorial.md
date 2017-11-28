---
title: 'Samouczek: Integracji Azure Active Directory z Evidence.com | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Evidence.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f9a7cb7c-ff67-40dc-872c-1fa35f9dd03b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: eed98c15dca8a6a77f0b5d407bb40ee0037fccad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evidencecom"></a><span data-ttu-id="67def-103">Samouczek: Integracji Azure Active Directory z Evidence.com</span><span class="sxs-lookup"><span data-stu-id="67def-103">Tutorial: Azure Active Directory integration with Evidence.com</span></span>

<span data-ttu-id="67def-104">Z tego samouczka, dowiesz się, jak toointegrate Evidence.com w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="67def-104">In this tutorial, you learn how toointegrate Evidence.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="67def-105">Integracja z usługą Azure AD Evidence.com zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="67def-105">Integrating Evidence.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="67def-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooEvidence.com.</span><span class="sxs-lookup"><span data-stu-id="67def-106">You can control in Azure AD who has access tooEvidence.com.</span></span>
- <span data-ttu-id="67def-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooEvidence.com (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67def-107">You can enable your users tooautomatically get signed-on tooEvidence.com (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="67def-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="67def-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="67def-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="67def-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67def-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="67def-110">Prerequisites</span></span>

<span data-ttu-id="67def-111">tooconfigure integracji z usługą Azure AD z Evidence.com należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="67def-111">tooconfigure Azure AD integration with Evidence.com, you need hello following items:</span></span>

- <span data-ttu-id="67def-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="67def-112">An Azure AD subscription</span></span>
- <span data-ttu-id="67def-113">Evidence.com logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="67def-113">A Evidence.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="67def-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="67def-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="67def-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="67def-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="67def-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="67def-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="67def-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="67def-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="67def-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="67def-118">Scenario description</span></span>
<span data-ttu-id="67def-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="67def-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="67def-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="67def-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="67def-121">Dodawanie Evidence.com z galerii hello</span><span class="sxs-lookup"><span data-stu-id="67def-121">Adding Evidence.com from hello gallery</span></span>
2. <span data-ttu-id="67def-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="67def-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evidencecom-from-hello-gallery"></a><span data-ttu-id="67def-123">Dodawanie Evidence.com z galerii hello</span><span class="sxs-lookup"><span data-stu-id="67def-123">Adding Evidence.com from hello gallery</span></span>
<span data-ttu-id="67def-124">tooconfigure hello integracji Evidence.com do usługi Azure AD, należy tooadd Evidence.com z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="67def-124">tooconfigure hello integration of Evidence.com into Azure AD, you need tooadd Evidence.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="67def-125">**tooadd Evidence.com z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="67def-125">**tooadd Evidence.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="67def-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="67def-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="67def-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="67def-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="67def-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="67def-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="67def-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="67def-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="67def-133">W polu wyszukiwania hello wpisz **Evidence.com**, wybierz pozycję **Evidence.com** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="67def-133">In hello search box, type **Evidence.com**, select **Evidence.com** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Evidence.com hello listy wyników](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="67def-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="67def-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="67def-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Evidence.com w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="67def-136">In this section, you configure and test Azure AD single sign-on with Evidence.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="67def-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Evidence.com jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67def-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Evidence.com is tooa user in Azure AD.</span></span> <span data-ttu-id="67def-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Evidence.com musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="67def-138">In other words, a link relationship between an Azure AD user and hello related user in Evidence.com needs toobe established.</span></span>

<span data-ttu-id="67def-139">W Evidence.com, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="67def-139">In Evidence.com, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="67def-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Evidence.com, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="67def-140">tooconfigure and test Azure AD single sign-on with Evidence.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="67def-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="67def-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="67def-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="67def-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="67def-143">**[Tworzenie użytkownika testowego Evidence.com](#create-a-evidencecom-test-user)**  -toohave odpowiednikiem Simona Britta w Evidence.com, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="67def-143">**[Create a Evidence.com test user](#create-a-evidencecom-test-user)** - toohave a counterpart of Britta Simon in Evidence.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="67def-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="67def-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="67def-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="67def-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="67def-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="67def-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="67def-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="67def-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Evidence.com application.</span></span>

<span data-ttu-id="67def-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Evidence.com, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="67def-148">**tooconfigure Azure AD single sign-on with Evidence.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="67def-149">W portalu Azure na powitania hello **Evidence.com** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="67def-149">In hello Azure portal, on hello **Evidence.com** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="67def-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="67def-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_samlbase.png)

3. <span data-ttu-id="67def-153">Na powitania **Evidence.com domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="67def-153">On hello **Evidence.com Domain and URLs** section, perform hello following steps:</span></span>

    ![Adresy URL i domeny Evidence.com pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_url.png)

    <span data-ttu-id="67def-155">a.</span><span class="sxs-lookup"><span data-stu-id="67def-155">a.</span></span> <span data-ttu-id="67def-156">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="67def-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<yourtenant>.evidence.com`</span></span>

    <span data-ttu-id="67def-157">b.</span><span class="sxs-lookup"><span data-stu-id="67def-157">b.</span></span> <span data-ttu-id="67def-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="67def-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<yourtenant>.evidence.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="67def-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="67def-159">These values are not real.</span></span> <span data-ttu-id="67def-160">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="67def-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="67def-161">Skontaktuj się z [zespołem pomocy technicznej klienta Evidence.com](https://communities.taser.com/support/SupportContactUs?typ=LE) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="67def-161">Contact [Evidence.com Client support team](https://communities.taser.com/support/SupportContactUs?typ=LE) tooget these values.</span></span> 

4. <span data-ttu-id="67def-162">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="67def-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_certificate.png) 

5. <span data-ttu-id="67def-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="67def-164">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-evidence-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="67def-166">Na powitania **konfiguracji Evidence.com** kliknij **skonfigurować Evidence.com** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="67def-166">On hello **Evidence.com Configuration** section, click **Configure Evidence.com** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="67def-167">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="67def-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfiguracja Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_configure.png) 

7. <span data-ttu-id="67def-169">W oknie przeglądarki sieci web w osobnych tooyour logowania Evidence.com dzierżawy z uprawnieniami administracyjnymi i przejdź zbyt**Admin** kartę</span><span class="sxs-lookup"><span data-stu-id="67def-169">In a separate web browser window, login tooyour Evidence.com tenant as an administrator and navigate too**Admin** Tab</span></span>

8. <span data-ttu-id="67def-170">Polecenie **agencji logowania jednokrotnego**</span><span class="sxs-lookup"><span data-stu-id="67def-170">Click on **Agency Single Sign On**</span></span>

9. <span data-ttu-id="67def-171">Wybierz **SAML na podstawie rejestracji jednokrotnej**</span><span class="sxs-lookup"><span data-stu-id="67def-171">Select **SAML Based Single Sign On**</span></span>

10. <span data-ttu-id="67def-172">Kopiuj hello **SAML identyfikator jednostki**, **SAML pojedynczy znak na adres URL usługi** i **Sign-Out adres URL** wartości widoczne w hello portalu Azure i odpowiednie pola toohello w Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="67def-172">Copy hello **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** values shown in hello Azure portal and toohello corresponding fields in Evidence.com.</span></span>

11. <span data-ttu-id="67def-173">Otwórz pobrany plik Certificate(Base64) w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikat zabezpieczeń** pole.</span><span class="sxs-lookup"><span data-stu-id="67def-173">Open your downloaded Certificate(Base64) file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Security Certificate** box.</span></span> 

12. <span data-ttu-id="67def-174">Zapisz konfigurację hello w Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="67def-174">Save hello configuration in Evidence.com.</span></span>

> [!TIP]
> <span data-ttu-id="67def-175">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="67def-175">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="67def-176">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="67def-176">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="67def-177">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="67def-177">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="67def-178">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="67def-178">Create an Azure AD test user</span></span>

<span data-ttu-id="67def-179">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="67def-179">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="67def-181">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="67def-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="67def-182">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="67def-182">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-evidence-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="67def-184">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="67def-184">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-evidence-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="67def-186">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="67def-186">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-evidence-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="67def-188">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="67def-188">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-evidence-tutorial/create_aaduser_04.png)

    <span data-ttu-id="67def-190">a.</span><span class="sxs-lookup"><span data-stu-id="67def-190">a.</span></span> <span data-ttu-id="67def-191">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="67def-191">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="67def-192">b.</span><span class="sxs-lookup"><span data-stu-id="67def-192">b.</span></span> <span data-ttu-id="67def-193">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="67def-193">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="67def-194">c.</span><span class="sxs-lookup"><span data-stu-id="67def-194">c.</span></span> <span data-ttu-id="67def-195">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="67def-195">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="67def-196">d.</span><span class="sxs-lookup"><span data-stu-id="67def-196">d.</span></span> <span data-ttu-id="67def-197">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="67def-197">Click **Create**.</span></span>
 
### <a name="create-a-evidencecom-test-user"></a><span data-ttu-id="67def-198">Tworzenie użytkownika testowego Evidence.com</span><span class="sxs-lookup"><span data-stu-id="67def-198">Create a Evidence.com test user</span></span>

<span data-ttu-id="67def-199">Dla usługi Azure AD użytkownicy toobe stanie toosign w musi być przygotowana dostępu wewnątrz hello Evidence.com aplikacji.</span><span class="sxs-lookup"><span data-stu-id="67def-199">For Azure AD users toobe able toosign in, they must be provisioned for access inside hello Evidence.com application.</span></span> <span data-ttu-id="67def-200">W tej sekcji opisano, jak konta użytkowników usługi Azure AD toocreate wewnątrz Evidence.com</span><span class="sxs-lookup"><span data-stu-id="67def-200">This section describes how toocreate Azure AD user accounts inside Evidence.com</span></span>

<span data-ttu-id="67def-201">**konto użytkownika w Evidence.com tooprovision:**</span><span class="sxs-lookup"><span data-stu-id="67def-201">**tooprovision a user account in Evidence.com:**</span></span>

1. <span data-ttu-id="67def-202">W oknie przeglądarki sieci web Zaloguj się do witryny firmy Evidence.com jako administrator.</span><span class="sxs-lookup"><span data-stu-id="67def-202">In a web browser window, log into your Evidence.com company site as an administrator.</span></span>

2. <span data-ttu-id="67def-203">Przejdź za**Admin** kartę.</span><span class="sxs-lookup"><span data-stu-id="67def-203">Navigate too**Admin** tab.</span></span>

3. <span data-ttu-id="67def-204">Polecenie **dodać użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="67def-204">Click on **Add User**.</span></span>

4. <span data-ttu-id="67def-205">Kliknij przycisk hello **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="67def-205">Click hello **Add** button.</span></span>

5. <span data-ttu-id="67def-206">Witaj **adres E-mail** hello dodanej użytkownika muszą być zgodne username hello hello użytkowników w usłudze Azure AD, który chcesz toogive dostępu.</span><span class="sxs-lookup"><span data-stu-id="67def-206">hello **Email Address** of hello added user must match hello username of hello users in Azure AD who you wish toogive access.</span></span> <span data-ttu-id="67def-207">Jeśli hello nazwy użytkownika i adres e-mail nie są hello tę samą wartość w Twojej organizacji, możesz użyć hello **Evidence.com > atrybuty > rejestracji jednokrotnej** sekcji nameidenitifer hello Azure toochange portalu hello wysyłane adres e-mail hello toobe tooEvidence.com.</span><span class="sxs-lookup"><span data-stu-id="67def-207">If hello username and email address are not hello same value in your organization, you can use hello **Evidence.com > Attributes > Single Sign-On** section of hello Azure portal toochange hello nameidenitifer sent tooEvidence.com toobe hello email address.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="67def-208">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="67def-208">Assign hello Azure AD test user</span></span>

<span data-ttu-id="67def-209">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooEvidence.com.</span><span class="sxs-lookup"><span data-stu-id="67def-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEvidence.com.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="67def-211">**tooassign tooEvidence.com Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="67def-211">**tooassign Britta Simon tooEvidence.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="67def-212">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="67def-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="67def-214">Z listy aplikacji hello wybierz **Evidence.com**.</span><span class="sxs-lookup"><span data-stu-id="67def-214">In hello applications list, select **Evidence.com**.</span></span>

    ![łącze Evidence.com Hello na liście aplikacji hello](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_app.png)  

3. <span data-ttu-id="67def-216">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="67def-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="67def-218">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="67def-218">Click **Add** button.</span></span> <span data-ttu-id="67def-219">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="67def-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="67def-221">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="67def-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="67def-222">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="67def-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="67def-223">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="67def-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="67def-224">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="67def-224">Test single sign-on</span></span>

<span data-ttu-id="67def-225">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="67def-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="67def-226">Po kliknięciu kafelka Evidence.com hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Evidence.com aplikacji.</span><span class="sxs-lookup"><span data-stu-id="67def-226">When you click hello Evidence.com tile in hello Access Panel, you should get automatically signed-on tooyour Evidence.com application.</span></span>
<span data-ttu-id="67def-227">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="67def-227">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="67def-228">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="67def-228">Additional resources</span></span>

* [<span data-ttu-id="67def-229">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="67def-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="67def-230">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="67def-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_203.png

