---
title: 'Samouczek: Integracji Azure Active Directory z PerformanceCentre | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i PerformanceCentre."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65288c32-f7e6-4eb3-a6dc-523c3d748d1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 19781c0087093a67c70dc90072cf1a119bb2ade0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-performancecentre"></a><span data-ttu-id="771a2-103">Samouczek: Integracji Azure Active Directory z PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="771a2-103">Tutorial: Azure Active Directory integration with PerformanceCentre</span></span>

<span data-ttu-id="771a2-104">Z tego samouczka, dowiesz się, jak toointegrate PerformanceCentre w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="771a2-104">In this tutorial, you learn how toointegrate PerformanceCentre with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="771a2-105">Integracja z usługą Azure AD PerformanceCentre zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="771a2-105">Integrating PerformanceCentre with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="771a2-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooPerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="771a2-106">You can control in Azure AD who has access tooPerformanceCentre</span></span>
- <span data-ttu-id="771a2-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooPerformanceCentre (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="771a2-107">You can enable your users tooautomatically get signed-on tooPerformanceCentre (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="771a2-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="771a2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="771a2-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="771a2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="771a2-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="771a2-110">Prerequisites</span></span>

<span data-ttu-id="771a2-111">tooconfigure integracji z usługą Azure AD z PerformanceCentre należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="771a2-111">tooconfigure Azure AD integration with PerformanceCentre, you need hello following items:</span></span>

- <span data-ttu-id="771a2-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="771a2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="771a2-113">PerformanceCentre logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="771a2-113">A PerformanceCentre single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="771a2-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="771a2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="771a2-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="771a2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="771a2-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="771a2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="771a2-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="771a2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="771a2-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="771a2-118">Scenario description</span></span>
<span data-ttu-id="771a2-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="771a2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="771a2-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="771a2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="771a2-121">Dodawanie PerformanceCentre z galerii hello</span><span class="sxs-lookup"><span data-stu-id="771a2-121">Adding PerformanceCentre from hello gallery</span></span>
2. <span data-ttu-id="771a2-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="771a2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-performancecentre-from-hello-gallery"></a><span data-ttu-id="771a2-123">Dodawanie PerformanceCentre z galerii hello</span><span class="sxs-lookup"><span data-stu-id="771a2-123">Adding PerformanceCentre from hello gallery</span></span>
<span data-ttu-id="771a2-124">tooconfigure hello integracji PerformanceCentre do usługi Azure AD, należy tooadd PerformanceCentre z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="771a2-124">tooconfigure hello integration of PerformanceCentre into Azure AD, you need tooadd PerformanceCentre from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="771a2-125">**tooadd PerformanceCentre z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="771a2-125">**tooadd PerformanceCentre from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="771a2-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="771a2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="771a2-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="771a2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="771a2-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="771a2-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="771a2-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="771a2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="771a2-133">W polu wyszukiwania hello wpisz **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="771a2-133">In hello search box, type **PerformanceCentre**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_search.png)

5. <span data-ttu-id="771a2-135">W panelu wyników hello zaznacz **PerformanceCentre**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="771a2-135">In hello results panel, select **PerformanceCentre**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="771a2-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="771a2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="771a2-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z PerformanceCentre w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="771a2-138">In this section, you configure and test Azure AD single sign-on with PerformanceCentre based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="771a2-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w PerformanceCentre jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="771a2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PerformanceCentre is tooa user in Azure AD.</span></span> <span data-ttu-id="771a2-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w PerformanceCentre musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="771a2-140">In other words, a link relationship between an Azure AD user and hello related user in PerformanceCentre needs toobe established.</span></span>

<span data-ttu-id="771a2-141">W PerformanceCentre, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="771a2-141">In PerformanceCentre, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="771a2-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z PerformanceCentre, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="771a2-142">tooconfigure and test Azure AD single sign-on with PerformanceCentre, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="771a2-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="771a2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="771a2-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="771a2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="771a2-145">**[Tworzenie użytkownika testowego PerformanceCentre](#creating-a-performancecentre-test-user)**  -toohave odpowiednikiem Simona Britta w PerformanceCentre, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="771a2-145">**[Creating a PerformanceCentre test user](#creating-a-performancecentre-test-user)** - toohave a counterpart of Britta Simon in PerformanceCentre that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="771a2-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="771a2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="771a2-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="771a2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="771a2-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="771a2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="771a2-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="771a2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PerformanceCentre application.</span></span>

<span data-ttu-id="771a2-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z PerformanceCentre, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="771a2-150">**tooconfigure Azure AD single sign-on with PerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="771a2-151">W portalu Azure na powitania hello **PerformanceCentre** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="771a2-151">In hello Azure portal, on hello **PerformanceCentre** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="771a2-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="771a2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_samlbase.png)

3. <span data-ttu-id="771a2-155">Na powitania **PerformanceCentre domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="771a2-155">On hello **PerformanceCentre Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_url.png)

    <span data-ttu-id="771a2-157">a.</span><span class="sxs-lookup"><span data-stu-id="771a2-157">a.</span></span> <span data-ttu-id="771a2-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`http://companyname.performancecentre.com/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="771a2-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://companyname.performancecentre.com/saml/SSO`</span></span>

    <span data-ttu-id="771a2-159">b.</span><span class="sxs-lookup"><span data-stu-id="771a2-159">b.</span></span> <span data-ttu-id="771a2-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`http://companyname.performancecentre.com`</span><span class="sxs-lookup"><span data-stu-id="771a2-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://companyname.performancecentre.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="771a2-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="771a2-161">These values are not real.</span></span> <span data-ttu-id="771a2-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="771a2-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="771a2-163">Skontaktuj się z [zespołem pomocy technicznej klienta PerformanceCentre](https://www.performancecentre.com/contact-us/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="771a2-163">Contact [PerformanceCentre Client support team](https://www.performancecentre.com/contact-us/) tooget these values.</span></span> 

4. <span data-ttu-id="771a2-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="771a2-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_certificate.png) 

5. <span data-ttu-id="771a2-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="771a2-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-performancecentre-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="771a2-168">Na powitania **konfiguracji PerformanceCentre** kliknij **skonfigurować PerformanceCentre** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="771a2-168">On hello **PerformanceCentre Configuration** section, click **Configure PerformanceCentre** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="771a2-169">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="771a2-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_configure.png) 

7. <span data-ttu-id="771a2-171">Logowania jednokrotnego tooyour **PerformanceCentre** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="771a2-171">Sign-on tooyour **PerformanceCentre** company site as administrator.</span></span>

8. <span data-ttu-id="771a2-172">Na karcie powitania po lewej stronie powitania kliknij **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="771a2-172">In hello tab on hello left side, click **Configure**.</span></span>
   
    ![Azure AD rejestracji jednokrotnej][10]

9. <span data-ttu-id="771a2-174">Na karcie powitania po lewej stronie powitania kliknij **różne**, a następnie kliknij przycisk **rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="771a2-174">In hello tab on hello left side, click **Miscellaneous**, and then click **Single Sign On**.</span></span>
   
    ![Azure AD rejestracji jednokrotnej][11]

10. <span data-ttu-id="771a2-176">Jako **protokołu**, wybierz pozycję **SAML**.</span><span class="sxs-lookup"><span data-stu-id="771a2-176">As **Protocol**, select **SAML**.</span></span>
   
    ![Azure AD rejestracji jednokrotnej][12]

11. <span data-ttu-id="771a2-178">Otwieranie pliku metadanych pobranych w Notatniku hello skopiować zawartość, wklej go do hello **metadanych dostawcy tożsamości** pola tekstowego, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="771a2-178">Open your downloaded metadata file in notepad, copy hello content, paste it into hello **Identity Provider Metadata** textbox, and then click **Save**.</span></span>
   
    ![Azure AD rejestracji jednokrotnej][13]

12. <span data-ttu-id="771a2-180">Sprawdź, czy wartości hello hello **jednostki podstawowego adresu URL** i **adres URL Identyfikatora jednostki** są poprawne.</span><span class="sxs-lookup"><span data-stu-id="771a2-180">Verify that hello values for hello **Entity Base URL** and **Entity ID URL** are correct.</span></span>
    
     ![Azure AD rejestracji jednokrotnej][14]

> [!TIP]
> <span data-ttu-id="771a2-182">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="771a2-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="771a2-183">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="771a2-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="771a2-184">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="771a2-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="771a2-185">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="771a2-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="771a2-186">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="771a2-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="771a2-188">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="771a2-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="771a2-189">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="771a2-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="771a2-191">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="771a2-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="771a2-193">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="771a2-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="771a2-195">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="771a2-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="771a2-197">a.</span><span class="sxs-lookup"><span data-stu-id="771a2-197">a.</span></span> <span data-ttu-id="771a2-198">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="771a2-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="771a2-199">b.</span><span class="sxs-lookup"><span data-stu-id="771a2-199">b.</span></span> <span data-ttu-id="771a2-200">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="771a2-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="771a2-201">c.</span><span class="sxs-lookup"><span data-stu-id="771a2-201">c.</span></span> <span data-ttu-id="771a2-202">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="771a2-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="771a2-203">d.</span><span class="sxs-lookup"><span data-stu-id="771a2-203">d.</span></span> <span data-ttu-id="771a2-204">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="771a2-204">Click **Create**.</span></span>
 
### <a name="creating-a-performancecentre-test-user"></a><span data-ttu-id="771a2-205">Tworzenie użytkownika testowego PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="771a2-205">Creating a PerformanceCentre test user</span></span>

<span data-ttu-id="771a2-206">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="771a2-206">hello objective of this section is toocreate a user called Britta Simon in PerformanceCentre.</span></span>

<span data-ttu-id="771a2-207">**toocreate użytkownika o nazwie Simona Britta w PerformanceCentre, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="771a2-207">**toocreate a user called Britta Simon in PerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="771a2-208">Rejestracja tooyour PerformanceCentre witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="771a2-208">Sign on tooyour PerformanceCentre company site as administrator.</span></span>

2. <span data-ttu-id="771a2-209">Hello menu po lewej stronie powitania kliknij **Interrelate**, a następnie kliknij przycisk **utworzyć uczestnika**.</span><span class="sxs-lookup"><span data-stu-id="771a2-209">In hello menu on hello left, click **Interrelate**, and then click **Create Participant**.</span></span>
   
    ![Utwórz użytkownika][400]

3. <span data-ttu-id="771a2-211">Na powitania **Interrelate — tworzenie uczestnika** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="771a2-211">On hello **Interrelate - Create Participant** dialog, perform hello following steps:</span></span>
   
    ![Utwórz użytkownika][401]
    
    <span data-ttu-id="771a2-213">a.</span><span class="sxs-lookup"><span data-stu-id="771a2-213">a.</span></span> <span data-ttu-id="771a2-214">Typ atrybutów hello wymagane dla Simona Britta do powiązanych pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="771a2-214">Type hello required attributes for Britta Simon into related textboxes.</span></span>
    
    >[!IMPORTANT]
    ><span data-ttu-id="771a2-215">Nazwa użytkownika Britta przez atrybut w PerformanceCentre musi być hello tak samo jak hello nazwę użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="771a2-215">Britta's User Name attribute in PerformanceCentre must be hello same as hello User Name in Azure AD.</span></span>
    
    <span data-ttu-id="771a2-216">b.</span><span class="sxs-lookup"><span data-stu-id="771a2-216">b.</span></span> <span data-ttu-id="771a2-217">Wybierz **Administrator klienta** jako **wybierz rolę**.</span><span class="sxs-lookup"><span data-stu-id="771a2-217">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="771a2-218">c.</span><span class="sxs-lookup"><span data-stu-id="771a2-218">c.</span></span> <span data-ttu-id="771a2-219">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="771a2-219">Click **Save**.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="771a2-220">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="771a2-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="771a2-221">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooPerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="771a2-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPerformanceCentre.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="771a2-223">**tooassign tooPerformanceCentre Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="771a2-223">**tooassign Britta Simon tooPerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="771a2-224">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="771a2-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="771a2-226">Z listy aplikacji hello wybierz **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="771a2-226">In hello applications list, select **PerformanceCentre**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_app.png) 

3. <span data-ttu-id="771a2-228">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="771a2-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="771a2-230">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="771a2-230">Click **Add** button.</span></span> <span data-ttu-id="771a2-231">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="771a2-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="771a2-233">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="771a2-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="771a2-234">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="771a2-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="771a2-235">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="771a2-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="771a2-236">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="771a2-236">Testing single sign-on</span></span>

<span data-ttu-id="771a2-237">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="771a2-237">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="771a2-238">Po kliknięciu kafelka PerformanceCentre hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour PerformanceCentre aplikacji.</span><span class="sxs-lookup"><span data-stu-id="771a2-238">When you click hello PerformanceCentre tile in hello Access Panel, you should get automatically signed-on tooyour PerformanceCentre application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="771a2-239">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="771a2-239">Additional resources</span></span>

* [<span data-ttu-id="771a2-240">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="771a2-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="771a2-241">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="771a2-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_06.png
[11]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_07.png
[12]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_08.png
[13]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_09.png
[14]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_10.png

[100]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_11.png
[401]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_12.png

