---
title: 'Samouczek: Integracji Azure Active Directory z Weekdone | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Weekdone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 34921f9a-5637-4420-ab4c-9beb34421909
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f997f1b49ff1aa0659a2409fdd945c6f96413b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-weekdone"></a><span data-ttu-id="2d34b-103">Samouczek: Integracji Azure Active Directory z Weekdone</span><span class="sxs-lookup"><span data-stu-id="2d34b-103">Tutorial: Azure Active Directory integration with Weekdone</span></span>

<span data-ttu-id="2d34b-104">Z tego samouczka, dowiesz się, jak toointegrate Weekdone w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2d34b-104">In this tutorial, you learn how toointegrate Weekdone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2d34b-105">Integracja z usługą Azure AD Weekdone zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="2d34b-105">Integrating Weekdone with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2d34b-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooWeekdone</span><span class="sxs-lookup"><span data-stu-id="2d34b-106">You can control in Azure AD who has access tooWeekdone</span></span>
- <span data-ttu-id="2d34b-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooWeekdone (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d34b-107">You can enable your users tooautomatically get signed-on tooWeekdone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2d34b-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="2d34b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2d34b-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2d34b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d34b-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2d34b-110">Prerequisites</span></span>

<span data-ttu-id="2d34b-111">tooconfigure integracji z usługą Azure AD z Weekdone należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="2d34b-111">tooconfigure Azure AD integration with Weekdone, you need hello following items:</span></span>

- <span data-ttu-id="2d34b-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d34b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2d34b-113">Weekdone logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2d34b-113">A Weekdone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2d34b-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="2d34b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2d34b-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="2d34b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2d34b-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="2d34b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2d34b-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2d34b-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2d34b-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="2d34b-118">Scenario description</span></span>
<span data-ttu-id="2d34b-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="2d34b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2d34b-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="2d34b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2d34b-121">Dodawanie Weekdone z galerii hello</span><span class="sxs-lookup"><span data-stu-id="2d34b-121">Adding Weekdone from hello gallery</span></span>
2. <span data-ttu-id="2d34b-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="2d34b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-weekdone-from-hello-gallery"></a><span data-ttu-id="2d34b-123">Dodawanie Weekdone z galerii hello</span><span class="sxs-lookup"><span data-stu-id="2d34b-123">Adding Weekdone from hello gallery</span></span>
<span data-ttu-id="2d34b-124">tooconfigure hello integracji Weekdone do usługi Azure AD, należy tooadd Weekdone z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="2d34b-124">tooconfigure hello integration of Weekdone into Azure AD, you need tooadd Weekdone from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2d34b-125">**tooadd Weekdone z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="2d34b-125">**tooadd Weekdone from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d34b-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="2d34b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="2d34b-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="2d34b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2d34b-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="2d34b-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="2d34b-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2d34b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="2d34b-133">W polu wyszukiwania hello wpisz **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="2d34b-133">In hello search box, type **Weekdone**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_search.png)

5. <span data-ttu-id="2d34b-135">W panelu wyników hello zaznacz **Weekdone**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="2d34b-135">In hello results panel, select **Weekdone**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2d34b-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="2d34b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2d34b-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Weekdone w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="2d34b-138">In this section, you configure and test Azure AD single sign-on with Weekdone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2d34b-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Weekdone jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d34b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Weekdone is tooa user in Azure AD.</span></span> <span data-ttu-id="2d34b-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Weekdone musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="2d34b-140">In other words, a link relationship between an Azure AD user and hello related user in Weekdone needs toobe established.</span></span>

<span data-ttu-id="2d34b-141">W Weekdone, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="2d34b-141">In Weekdone, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2d34b-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Weekdone, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="2d34b-142">tooconfigure and test Azure AD single sign-on with Weekdone, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2d34b-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="2d34b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2d34b-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="2d34b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2d34b-145">**[Tworzenie użytkownika testowego Weekdone](#creating-a-weekdone-test-user)**  -toohave odpowiednikiem Simona Britta w Weekdone, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2d34b-145">**[Creating a Weekdone test user](#creating-a-weekdone-test-user)** - toohave a counterpart of Britta Simon in Weekdone that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2d34b-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="2d34b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2d34b-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="2d34b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2d34b-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2d34b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2d34b-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Weekdone.</span><span class="sxs-lookup"><span data-stu-id="2d34b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Weekdone application.</span></span>

<span data-ttu-id="2d34b-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Weekdone, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="2d34b-150">**tooconfigure Azure AD single sign-on with Weekdone, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d34b-151">W portalu Azure na powitania hello **Weekdone** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="2d34b-151">In hello Azure portal, on hello **Weekdone** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="2d34b-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="2d34b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_samlbase.png)

3. <span data-ttu-id="2d34b-155">Na powitania **Weekdone domeny i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="2d34b-155">On hello **Weekdone Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url1.png)

    <span data-ttu-id="2d34b-157">a.</span><span class="sxs-lookup"><span data-stu-id="2d34b-157">a.</span></span> <span data-ttu-id="2d34b-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="2d34b-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

    <span data-ttu-id="2d34b-159">b.</span><span class="sxs-lookup"><span data-stu-id="2d34b-159">b.</span></span> <span data-ttu-id="2d34b-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="2d34b-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

4. <span data-ttu-id="2d34b-161">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="2d34b-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="2d34b-162">Jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="2d34b-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url2.png)

    <span data-ttu-id="2d34b-164">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="2d34b-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://weekdone.com/a/<tenantname>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="2d34b-165">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="2d34b-165">These values are not real.</span></span> <span data-ttu-id="2d34b-166">Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="2d34b-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="2d34b-167">Skontaktuj się z [zespołem pomocy technicznej klienta Weekdone](mailto:hello@weekdone.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="2d34b-167">Contact [Weekdone Client support team](mailto:hello@weekdone.com) tooget these values.</span></span> 

5. <span data-ttu-id="2d34b-168">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="2d34b-168">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_certificate.png) 

6. <span data-ttu-id="2d34b-170">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2d34b-170">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-weekdone-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="2d34b-172">Na powitania **konfiguracji Weekdone** kliknij **skonfigurować Weekdone** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="2d34b-172">On hello **Weekdone Configuration** section, click **Configure Weekdone** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2d34b-173">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="2d34b-173">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_configure.png) 

8. <span data-ttu-id="2d34b-175">tooconfigure rejestracji jednokrotnej w **Weekdone** strony, należy pobrać hello toosend **XML metadanych, adres URL Sign-Out identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** zbyt[Weekdone pomocy technicznej zespół](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="2d34b-175">tooconfigure single sign-on on **Weekdone** side, you need toosend hello downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Weekdone support team](mailto:hello@weekdone.com).</span></span>

> [!TIP]
> <span data-ttu-id="2d34b-176">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="2d34b-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2d34b-177">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="2d34b-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2d34b-178">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2d34b-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2d34b-179">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d34b-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="2d34b-180">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="2d34b-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="2d34b-182">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="2d34b-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d34b-183">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="2d34b-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2d34b-185">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="2d34b-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2d34b-187">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2d34b-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2d34b-189">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="2d34b-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2d34b-191">a.</span><span class="sxs-lookup"><span data-stu-id="2d34b-191">a.</span></span> <span data-ttu-id="2d34b-192">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2d34b-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2d34b-193">b.</span><span class="sxs-lookup"><span data-stu-id="2d34b-193">b.</span></span> <span data-ttu-id="2d34b-194">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2d34b-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2d34b-195">c.</span><span class="sxs-lookup"><span data-stu-id="2d34b-195">c.</span></span> <span data-ttu-id="2d34b-196">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="2d34b-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2d34b-197">d.</span><span class="sxs-lookup"><span data-stu-id="2d34b-197">d.</span></span> <span data-ttu-id="2d34b-198">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="2d34b-198">Click **Create**.</span></span>
 
### <a name="creating-a-weekdone-test-user"></a><span data-ttu-id="2d34b-199">Tworzenie użytkownika testowego Weekdone</span><span class="sxs-lookup"><span data-stu-id="2d34b-199">Creating a Weekdone test user</span></span>

<span data-ttu-id="2d34b-200">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Weekdone.</span><span class="sxs-lookup"><span data-stu-id="2d34b-200">hello objective of this section is toocreate a user called Britta Simon in Weekdone.</span></span> <span data-ttu-id="2d34b-201">Weekdone obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="2d34b-201">Weekdone supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="2d34b-202">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="2d34b-202">There is no action item for you in this section.</span></span> <span data-ttu-id="2d34b-203">Nowy użytkownik jest tworzona podczas próby tooaccess Weekdone, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="2d34b-203">A new user is created during an attempt tooaccess Weekdone if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="2d34b-204">Jeśli potrzebujesz ręcznie toocreate użytkownika, należy toocontact hello [zespołem pomocy technicznej klienta Weekdone](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="2d34b-204">If you need toocreate a user manually, you need toocontact hello [Weekdone Client support team](mailto:hello@weekdone.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2d34b-205">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d34b-205">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2d34b-206">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooWeekdone.</span><span class="sxs-lookup"><span data-stu-id="2d34b-206">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWeekdone.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="2d34b-208">**tooassign tooWeekdone Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="2d34b-208">**tooassign Britta Simon tooWeekdone, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d34b-209">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="2d34b-209">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="2d34b-211">Z listy aplikacji hello wybierz **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="2d34b-211">In hello applications list, select **Weekdone**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_app.png) 

3. <span data-ttu-id="2d34b-213">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="2d34b-213">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="2d34b-215">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2d34b-215">Click **Add** button.</span></span> <span data-ttu-id="2d34b-216">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2d34b-216">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="2d34b-218">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2d34b-218">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2d34b-219">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2d34b-219">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2d34b-220">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2d34b-220">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2d34b-221">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2d34b-221">Testing single sign-on</span></span>

<span data-ttu-id="2d34b-222">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="2d34b-222">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="2d34b-223">Po kliknięciu kafelka Weekdone hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Weekdone aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2d34b-223">When you click hello Weekdone tile in hello Access Panel, you should get automatically signed-on tooyour Weekdone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2d34b-224">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="2d34b-224">Additional resources</span></span>

* [<span data-ttu-id="2d34b-225">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d34b-225">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2d34b-226">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2d34b-226">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_203.png

