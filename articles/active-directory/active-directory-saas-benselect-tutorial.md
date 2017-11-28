---
title: 'Samouczek: Integracji Azure Active Directory z BenSelect | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i BenSelect."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffa17478-3ea1-4356-a289-545b5b9a4494
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: c3705da337bf8f6e76de58cd21c5b047c8f5e12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benselect"></a><span data-ttu-id="bf8d1-103">Samouczek: Integracji Azure Active Directory z BenSelect</span><span class="sxs-lookup"><span data-stu-id="bf8d1-103">Tutorial: Azure Active Directory integration with BenSelect</span></span>

<span data-ttu-id="bf8d1-104">Z tego samouczka, dowiesz się, jak toointegrate BenSelect w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bf8d1-104">In this tutorial, you learn how toointegrate BenSelect with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bf8d1-105">Integracja z usługą Azure AD BenSelect zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="bf8d1-105">Integrating BenSelect with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bf8d1-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooBenSelect</span><span class="sxs-lookup"><span data-stu-id="bf8d1-106">You can control in Azure AD who has access tooBenSelect</span></span>
- <span data-ttu-id="bf8d1-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooBenSelect (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf8d1-107">You can enable your users tooautomatically get signed-on tooBenSelect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bf8d1-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bf8d1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bf8d1-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bf8d1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf8d1-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bf8d1-110">Prerequisites</span></span>

<span data-ttu-id="bf8d1-111">tooconfigure integracji z usługą Azure AD z BenSelect należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="bf8d1-111">tooconfigure Azure AD integration with BenSelect, you need hello following items:</span></span>

- <span data-ttu-id="bf8d1-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf8d1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bf8d1-113">BenSelect logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="bf8d1-113">A BenSelect single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bf8d1-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bf8d1-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="bf8d1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bf8d1-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bf8d1-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bf8d1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bf8d1-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="bf8d1-118">Scenario description</span></span>
<span data-ttu-id="bf8d1-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bf8d1-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="bf8d1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bf8d1-121">Dodawanie BenSelect z galerii hello</span><span class="sxs-lookup"><span data-stu-id="bf8d1-121">Adding BenSelect from hello gallery</span></span>
2. <span data-ttu-id="bf8d1-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bf8d1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benselect-from-hello-gallery"></a><span data-ttu-id="bf8d1-123">Dodawanie BenSelect z galerii hello</span><span class="sxs-lookup"><span data-stu-id="bf8d1-123">Adding BenSelect from hello gallery</span></span>
<span data-ttu-id="bf8d1-124">tooconfigure hello integracji BenSelect do usługi Azure AD, należy tooadd BenSelect z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-124">tooconfigure hello integration of BenSelect into Azure AD, you need tooadd BenSelect from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bf8d1-125">**tooadd BenSelect z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="bf8d1-125">**tooadd BenSelect from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf8d1-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="bf8d1-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bf8d1-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="bf8d1-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="bf8d1-133">W polu wyszukiwania hello wpisz **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-133">In hello search box, type **BenSelect**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_search.png)

5. <span data-ttu-id="bf8d1-135">W panelu wyników hello zaznacz **BenSelect**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-135">In hello results panel, select **BenSelect**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bf8d1-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bf8d1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bf8d1-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z BenSelect na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="bf8d1-138">In this section, you configure and test Azure AD single sign-on with BenSelect based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bf8d1-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w BenSelect jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BenSelect is tooa user in Azure AD.</span></span> <span data-ttu-id="bf8d1-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w BenSelect musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-140">In other words, a link relationship between an Azure AD user and hello related user in BenSelect needs toobe established.</span></span>

<span data-ttu-id="bf8d1-141">W BenSelect, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-141">In BenSelect, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bf8d1-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z BenSelect, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="bf8d1-142">tooconfigure and test Azure AD single sign-on with BenSelect, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bf8d1-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bf8d1-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bf8d1-145">**[Tworzenie użytkownika testowego BenSelect](#creating-a-benselect-test-user)**  -toohave odpowiednikiem Simona Britta w BenSelect, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-145">**[Creating a BenSelect test user](#creating-a-benselect-test-user)** - toohave a counterpart of Britta Simon in BenSelect that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bf8d1-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bf8d1-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bf8d1-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bf8d1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bf8d1-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji BenSelect.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BenSelect application.</span></span>

<span data-ttu-id="bf8d1-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z BenSelect, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="bf8d1-150">**tooconfigure Azure AD single sign-on with BenSelect, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf8d1-151">W portalu Azure na powitania hello **BenSelect** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-151">In hello Azure portal, on hello **BenSelect** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="bf8d1-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_samlbase.png)

3. <span data-ttu-id="bf8d1-155">Na powitania **BenSelect domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="bf8d1-155">On hello **BenSelect Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_url.png)

    <span data-ttu-id="bf8d1-157">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span><span class="sxs-lookup"><span data-stu-id="bf8d1-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bf8d1-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-158">This value is not real.</span></span> <span data-ttu-id="bf8d1-159">Zaktualizuj tę wartość przy hello rzeczywisty adres URL odpowiedzi służący.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="bf8d1-160">Skontaktuj się z [zespołem pomocy technicznej BenSelect](mailto:support@selerix.com) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-160">Contact [BenSelect support team](mailto:support@selerix.com) tooget this value.</span></span>
 
4. <span data-ttu-id="bf8d1-161">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Raw)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-161">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_certificate.png) 

5. <span data-ttu-id="bf8d1-163">Aplikacja BenSelect oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-163">BenSelect application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="bf8d1-164">Skonfiguruj powitania po oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-164">Configure hello following claims for this application.</span></span> <span data-ttu-id="bf8d1-165">Można zarządzać hello wartości tych atrybutów z hello **atrybuty użytkownika** sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-165">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="bf8d1-166">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-166">hello following screenshot shows an example for this.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_06.png)

6. <span data-ttu-id="bf8d1-168">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego:</span><span class="sxs-lookup"><span data-stu-id="bf8d1-168">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="bf8d1-169">a.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-169">a.</span></span> <span data-ttu-id="bf8d1-170">W hello **identyfikator użytkownika** listy rozwijanej wybierz **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-170">In hello **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="bf8d1-171">b.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-171">b.</span></span> <span data-ttu-id="bf8d1-172">W hello **poczty** listy rozwijanej wybierz **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-172">In hello **Mail** dropdown list, select **user.userprincipalname**.</span></span>

7. <span data-ttu-id="bf8d1-173">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-173">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benselect-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="bf8d1-175">Na powitania **konfiguracji BenSelect** kliknij **skonfigurować BenSelect** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-175">On hello **BenSelect Configuration** section, click **Configure BenSelect** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bf8d1-176">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="bf8d1-176">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_configure.png) 

9. <span data-ttu-id="bf8d1-178">tooconfigure rejestracji jednokrotnej w **BenSelect** strony, należy pobrać hello toosend **Certificate(Raw)** i **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi**za[zespołem pomocy technicznej BenSelect](mailto:support@selerix.com).</span><span class="sxs-lookup"><span data-stu-id="bf8d1-178">tooconfigure single sign-on on **BenSelect** side, you need toosend hello downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[BenSelect support team](mailto:support@selerix.com).</span></span>

   >[!NOTE]
   ><span data-ttu-id="bf8d1-179">Należy toomention, że ta integracja wymaga algorytm hello SHA256 (SHA1 nie jest obsługiwana) tooset hello logowania jednokrotnego na powitania odpowiedniego serwera, takich jak app2101 itp.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-179">You need toomention that this integration requires hello SHA256 algorithm (SHA1 is not supported) tooset hello SSO on hello appropriate server like app2101 etc.</span></span> 
   
> [!TIP]
> <span data-ttu-id="bf8d1-180">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="bf8d1-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bf8d1-181">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bf8d1-182">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bf8d1-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bf8d1-183">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf8d1-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="bf8d1-184">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="bf8d1-186">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="bf8d1-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf8d1-187">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bf8d1-189">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bf8d1-191">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bf8d1-193">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="bf8d1-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bf8d1-195">a.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-195">a.</span></span> <span data-ttu-id="bf8d1-196">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bf8d1-197">b.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-197">b.</span></span> <span data-ttu-id="bf8d1-198">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bf8d1-199">c.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-199">c.</span></span> <span data-ttu-id="bf8d1-200">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bf8d1-201">d.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-201">d.</span></span> <span data-ttu-id="bf8d1-202">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-202">Click **Create**.</span></span>
 
### <a name="creating-a-benselect-test-user"></a><span data-ttu-id="bf8d1-203">Tworzenie użytkownika testowego BenSelect</span><span class="sxs-lookup"><span data-stu-id="bf8d1-203">Creating a BenSelect test user</span></span>

<span data-ttu-id="bf8d1-204">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w BenSelect.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-204">hello objective of this section is toocreate a user called Britta Simon in BenSelect.</span></span> <span data-ttu-id="bf8d1-205">Praca z [zespołem pomocy technicznej BenSelect](mailto:support@selerix.com) tooadd hello użytkowników w hello BenSelect konta.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-205">Work with [BenSelect support team](mailto:support@selerix.com) tooadd hello users in hello BenSelect account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bf8d1-206">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf8d1-206">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bf8d1-207">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooBenSelect.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-207">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBenSelect.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="bf8d1-209">**tooassign tooBenSelect Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="bf8d1-209">**tooassign Britta Simon tooBenSelect, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf8d1-210">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-210">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="bf8d1-212">Z listy aplikacji hello wybierz **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-212">In hello applications list, select **BenSelect**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_app.png) 

3. <span data-ttu-id="bf8d1-214">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-214">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="bf8d1-216">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-216">Click **Add** button.</span></span> <span data-ttu-id="bf8d1-217">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="bf8d1-219">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-219">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bf8d1-220">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bf8d1-221">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bf8d1-222">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bf8d1-222">Testing single sign-on</span></span>

<span data-ttu-id="bf8d1-223">W tej sekcji można przetestować konfigurację usługi Azure AD z logowania jednokrotnego za pomocą hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-223">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="bf8d1-224">Po kliknięciu kafelka BenSelect hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour BenSelect aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bf8d1-224">When you click hello BenSelect tile in hello Access Panel, you should get automatically signed-on tooyour BenSelect application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bf8d1-225">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="bf8d1-225">Additional resources</span></span>

* [<span data-ttu-id="bf8d1-226">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bf8d1-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bf8d1-227">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bf8d1-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_203.png

