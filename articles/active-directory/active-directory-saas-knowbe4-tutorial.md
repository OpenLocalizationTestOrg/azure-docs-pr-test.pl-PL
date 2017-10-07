---
title: "Samouczek: Integracji Azure Active Directory szkolenie świadomości bezpieczeństwa KnowBe4 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i szkolenia w zakresie rozpoznawania KnowBe4 zabezpieczeń."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b80d2212-cc5f-4adb-836c-570640810c39
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 907fa814b82c9ffb2376f73470b746a37104c66e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-knowbe4-security-awareness-training"></a><span data-ttu-id="243f2-103">Samouczek: Integracji Azure Active Directory szkolenie świadomości bezpieczeństwa KnowBe4</span><span class="sxs-lookup"><span data-stu-id="243f2-103">Tutorial: Azure Active Directory integration with KnowBe4 Security Awareness Training</span></span>

<span data-ttu-id="243f2-104">Z tego samouczka, dowiesz się, jak toointegrate KnowBe4 zabezpieczeń świadomości szkolenia w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="243f2-104">In this tutorial, you learn how toointegrate KnowBe4 Security Awareness Training with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="243f2-105">Integracja z usługą Azure AD świadomości szkolenia w zakresie zabezpieczeń KnowBe4 zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="243f2-105">Integrating KnowBe4 Security Awareness Training with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="243f2-106">Można kontrolować w usłudze Azure AD, który ma dostęp do szkolenia w zakresie rozpoznawania tooKnowBe4 zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="243f2-106">You can control in Azure AD who has access tooKnowBe4 Security Awareness Training</span></span>
- <span data-ttu-id="243f2-107">Aby umożliwić użytkownikom uzyskać tooautomatically zalogowane szkolenia świadomości bezpieczeństwa tooKnowBe4 (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="243f2-107">You can enable your users tooautomatically get signed-on tooKnowBe4 Security Awareness Training (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="243f2-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="243f2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="243f2-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="243f2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="243f2-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="243f2-110">Prerequisites</span></span>

<span data-ttu-id="243f2-111">tooconfigure integracji usługi Azure AD z świadomości szkolenia w zakresie zabezpieczeń KnowBe4 należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="243f2-111">tooconfigure Azure AD integration with KnowBe4 Security Awareness Training, you need hello following items:</span></span>

- <span data-ttu-id="243f2-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="243f2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="243f2-113">Rozpoznawanie szkolenia w zakresie zabezpieczeń KnowBe4 logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="243f2-113">A KnowBe4 Security Awareness Training single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="243f2-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="243f2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="243f2-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="243f2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="243f2-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="243f2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="243f2-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="243f2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="243f2-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="243f2-118">Scenario description</span></span>
<span data-ttu-id="243f2-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="243f2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="243f2-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="243f2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="243f2-121">Dodawanie świadomości szkolenia w zakresie zabezpieczeń KnowBe4 z galerii hello</span><span class="sxs-lookup"><span data-stu-id="243f2-121">Adding KnowBe4 Security Awareness Training from hello gallery</span></span>
2. <span data-ttu-id="243f2-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="243f2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-knowbe4-security-awareness-training-from-hello-gallery"></a><span data-ttu-id="243f2-123">Dodawanie świadomości szkolenia w zakresie zabezpieczeń KnowBe4 z galerii hello</span><span class="sxs-lookup"><span data-stu-id="243f2-123">Adding KnowBe4 Security Awareness Training from hello gallery</span></span>
<span data-ttu-id="243f2-124">tooconfigure hello integracji szkolenia w zakresie rozpoznawania KnowBe4 zabezpieczeń w usłudze Azure Active Directory, należy tooadd świadomości szkolenia w zakresie zabezpieczeń KnowBe4 z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="243f2-124">tooconfigure hello integration of KnowBe4 Security Awareness Training into Azure AD, you need tooadd KnowBe4 Security Awareness Training from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="243f2-125">**tooadd szkolenia świadomości bezpieczeństwa KnowBe4 z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="243f2-125">**tooadd KnowBe4 Security Awareness Training from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="243f2-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="243f2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="243f2-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="243f2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="243f2-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="243f2-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="243f2-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="243f2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="243f2-133">W polu wyszukiwania hello wpisz **świadomości szkolenia w zakresie zabezpieczeń KnowBe4**.</span><span class="sxs-lookup"><span data-stu-id="243f2-133">In hello search box, type **KnowBe4 Security Awareness Training**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_search.png)

5. <span data-ttu-id="243f2-135">W panelu wyników hello, wybierz **świadomości szkolenia w zakresie zabezpieczeń KnowBe4**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="243f2-135">In hello results panel, select **KnowBe4 Security Awareness Training**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="243f2-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="243f2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="243f2-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z KnowBe4 świadomości szkolenia w zakresie zabezpieczeń w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="243f2-138">In this section, you configure and test Azure AD single sign-on with KnowBe4 Security Awareness Training based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="243f2-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello odpowiednikiem użytkownika w zakresie świadomości bezpieczeństwa KnowBe4 jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="243f2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in KnowBe4 Security Awareness Training is tooa user in Azure AD.</span></span> <span data-ttu-id="243f2-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w zakresie świadomości bezpieczeństwa KnowBe4 musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="243f2-140">In other words, a link relationship between an Azure AD user and hello related user in KnowBe4 Security Awareness Training needs toobe established.</span></span>

<span data-ttu-id="243f2-141">W zakresie świadomości bezpieczeństwa KnowBe4, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="243f2-141">In KnowBe4 Security Awareness Training, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="243f2-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej szkolenie świadomości bezpieczeństwa KnowBe4, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="243f2-142">tooconfigure and test Azure AD single sign-on with KnowBe4 Security Awareness Training, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="243f2-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="243f2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="243f2-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="243f2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="243f2-145">**[Tworzenie użytkownika testowego świadomości szkolenia w zakresie zabezpieczeń KnowBe4](#creating-a-knowbe4-security-awareness-training-test-user)**  -toohave odpowiednikiem Simona Britta w KnowBe4 świadomości szkolenia w zakresie zabezpieczeń, który jest odpowiednikiem połączonych toohello usługi Azure AD użytkownika.</span><span class="sxs-lookup"><span data-stu-id="243f2-145">**[Creating a KnowBe4 Security Awareness Training test user](#creating-a-knowbe4-security-awareness-training-test-user)** - toohave a counterpart of Britta Simon in KnowBe4 Security Awareness Training that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="243f2-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="243f2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="243f2-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="243f2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="243f2-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="243f2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="243f2-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w zakresie świadomości bezpieczeństwa KnowBe4 aplikacji.</span><span class="sxs-lookup"><span data-stu-id="243f2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your KnowBe4 Security Awareness Training application.</span></span>

<span data-ttu-id="243f2-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej KnowBe4 szkolenie pogłębianie wiedzy na temat zabezpieczeń, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="243f2-150">**tooconfigure Azure AD single sign-on with KnowBe4 Security Awareness Training, perform hello following steps:**</span></span>

1. <span data-ttu-id="243f2-151">W portalu Azure na powitania hello **świadomości szkolenia w zakresie zabezpieczeń KnowBe4** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="243f2-151">In hello Azure portal, on hello **KnowBe4 Security Awareness Training** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="243f2-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="243f2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_samlbase.png)

3. <span data-ttu-id="243f2-155">Na powitania **KnowBe4 zabezpieczeń świadomości szkolenia domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="243f2-155">On hello **KnowBe4 Security Awareness Training Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_url.png)

    <span data-ttu-id="243f2-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.KnowBe4.com/auth/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="243f2-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.KnowBe4.com/auth/saml/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="243f2-158">wartość Hello nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="243f2-158">hello value is not real.</span></span> <span data-ttu-id="243f2-159">Wartość hello aktualizacji z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="243f2-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="243f2-160">Skontaktuj się z [zespołem pomocy technicznej klienta szkolenia świadomości bezpieczeństwa KnowBe4](mailto:support@KnowBe4.com) tooget hello wartość.</span><span class="sxs-lookup"><span data-stu-id="243f2-160">Contact [KnowBe4 Security Awareness Training Client support team](mailto:support@KnowBe4.com) tooget hello value.</span></span> 
 

4. <span data-ttu-id="243f2-161">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Raw)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="243f2-161">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_certificate.png) 

5. <span data-ttu-id="243f2-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="243f2-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="243f2-165">Na powitania **KnowBe4 zabezpieczeń świadomości szkolenia konfiguracji** kliknij **skonfigurować KnowBe4 świadomości szkolenia w zakresie zabezpieczeń** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="243f2-165">On hello **KnowBe4 Security Awareness Training Configuration** section, click **Configure KnowBe4 Security Awareness Training** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="243f2-166">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="243f2-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_configure.png) 

7. <span data-ttu-id="243f2-168">tooconfigure rejestracji jednokrotnej w **świadomości szkolenia w zakresie zabezpieczeń KnowBe4** strony, należy pobrać hello toosend **certyfikatu (Raw)**, **Sign-Out adres URL, identyfikator jednostki SAML i SAML logowania jednokrotnego Adres URL usługi** za[zespołem pomocy technicznej klienta szkolenia świadomości bezpieczeństwa KnowBe4](mailto:support@KnowBe4.com).</span><span class="sxs-lookup"><span data-stu-id="243f2-168">tooconfigure single sign-on on **KnowBe4 Security Awareness Training** side, you need toosend hello downloaded **Certificate (Raw)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[KnowBe4 Security Awareness Training Client support team](mailto:support@KnowBe4.com).</span></span>

> [!TIP]
> <span data-ttu-id="243f2-169">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="243f2-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="243f2-170">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="243f2-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="243f2-171">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="243f2-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="243f2-172">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="243f2-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="243f2-173">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="243f2-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="243f2-175">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="243f2-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="243f2-176">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="243f2-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="243f2-178">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="243f2-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="243f2-180">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="243f2-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="243f2-182">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="243f2-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="243f2-184">a.</span><span class="sxs-lookup"><span data-stu-id="243f2-184">a.</span></span> <span data-ttu-id="243f2-185">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="243f2-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="243f2-186">b.</span><span class="sxs-lookup"><span data-stu-id="243f2-186">b.</span></span> <span data-ttu-id="243f2-187">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="243f2-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="243f2-188">c.</span><span class="sxs-lookup"><span data-stu-id="243f2-188">c.</span></span> <span data-ttu-id="243f2-189">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="243f2-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="243f2-190">d.</span><span class="sxs-lookup"><span data-stu-id="243f2-190">d.</span></span> <span data-ttu-id="243f2-191">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="243f2-191">Click **Create**.</span></span>
 
### <a name="creating-a-knowbe4-security-awareness-training-test-user"></a><span data-ttu-id="243f2-192">Tworzenie użytkownika testowego świadomości szkolenia w zakresie zabezpieczeń KnowBe4</span><span class="sxs-lookup"><span data-stu-id="243f2-192">Creating a KnowBe4 Security Awareness Training test user</span></span>

<span data-ttu-id="243f2-193">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w zakresie świadomości bezpieczeństwa KnowBe4.</span><span class="sxs-lookup"><span data-stu-id="243f2-193">hello objective of this section is toocreate a user called Britta Simon in KnowBe4 Security Awareness Training.</span></span> <span data-ttu-id="243f2-194">Rozpoznawanie szkolenia w zakresie zabezpieczeń KnowBe4 obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="243f2-194">KnowBe4 Security Awareness Training supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="243f2-195">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="243f2-195">There is no action item for you in this section.</span></span> <span data-ttu-id="243f2-196">Nowy użytkownik jest tworzona podczas tooaccess próba szkolenia świadomości bezpieczeństwa KnowBe4, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="243f2-196">A new user is created during an attempt tooaccess KnowBe4 Security Awareness Training if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="243f2-197">Jeśli potrzebujesz ręcznie toocreate użytkownika, należy toocontact hello [zespołem pomocy technicznej w zakresie świadomości bezpieczeństwa KnowBe4](mailto:support@KnowBe4.com).</span><span class="sxs-lookup"><span data-stu-id="243f2-197">If you need toocreate a user manually, you need toocontact hello [KnowBe4 Security Awareness Training support team](mailto:support@KnowBe4.com).</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="243f2-198">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="243f2-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="243f2-199">W tej sekcji, musisz włączyć Simona Britta toouse Azure logowania jednokrotnego za udzielanie dostępu tooKnowBe4 zabezpieczeń świadomości szkolenia.</span><span class="sxs-lookup"><span data-stu-id="243f2-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKnowBe4 Security Awareness Training.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="243f2-201">**tooassign Simona Britta tooKnowBe4 świadomości szkolenia w zakresie zabezpieczeń, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="243f2-201">**tooassign Britta Simon tooKnowBe4 Security Awareness Training, perform hello following steps:**</span></span>

1. <span data-ttu-id="243f2-202">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="243f2-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="243f2-204">Z listy aplikacji hello wybierz **świadomości szkolenia w zakresie zabezpieczeń KnowBe4**.</span><span class="sxs-lookup"><span data-stu-id="243f2-204">In hello applications list, select **KnowBe4 Security Awareness Training**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_app.png) 

3. <span data-ttu-id="243f2-206">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="243f2-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="243f2-208">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="243f2-208">Click **Add** button.</span></span> <span data-ttu-id="243f2-209">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="243f2-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="243f2-211">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="243f2-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="243f2-212">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="243f2-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="243f2-213">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="243f2-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="243f2-214">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="243f2-214">Testing single sign-on</span></span>

<span data-ttu-id="243f2-215">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="243f2-215">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>
  
<span data-ttu-id="243f2-216">Po kliknięciu kafelka świadomości szkolenia w zakresie zabezpieczeń KnowBe4 hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour szkolenia w zakresie rozpoznawania KnowBe4 zabezpieczeń aplikacji.</span><span class="sxs-lookup"><span data-stu-id="243f2-216">When you click hello KnowBe4 Security Awareness Training tile in hello Access Panel, you should get automatically signed-on tooyour KnowBe4 Security Awareness Training application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="243f2-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="243f2-217">Additional resources</span></span>

* [<span data-ttu-id="243f2-218">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="243f2-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="243f2-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="243f2-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_203.png

