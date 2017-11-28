---
title: 'Samouczek: Integracji Azure Active Directory z RFPIO | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i RFPIO."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: e0c692276276edd8f859e73d81cf54d75a65957a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a><span data-ttu-id="ad39d-103">Samouczek: Integracji Azure Active Directory z RFPIO</span><span class="sxs-lookup"><span data-stu-id="ad39d-103">Tutorial: Azure Active Directory integration with RFPIO</span></span>

<span data-ttu-id="ad39d-104">Z tego samouczka, dowiesz się, jak toointegrate RFPIO w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ad39d-104">In this tutorial, you learn how toointegrate RFPIO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ad39d-105">Integracja z usługą Azure AD RFPIO zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ad39d-105">Integrating RFPIO with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ad39d-106">Możesz kontrolować, kto w usłudze Azure AD, kto ma dostęp do tooRFPIO.</span><span class="sxs-lookup"><span data-stu-id="ad39d-106">You can control who in Azure AD who has access tooRFPIO.</span></span>
- <span data-ttu-id="ad39d-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooRFPIO (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad39d-107">You can enable your users tooautomatically get signed-on tooRFPIO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ad39d-108">Możesz zarządzać kont w jednej centralnej lokalizacji — Witaj portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ad39d-108">You can manage your accounts in one central location--hello Azure portal.</span></span>

<span data-ttu-id="ad39d-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ad39d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad39d-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ad39d-110">Prerequisites</span></span>

<span data-ttu-id="ad39d-111">tooconfigure integracji z usługą Azure AD z RFPIO należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ad39d-111">tooconfigure Azure AD integration with RFPIO, you need hello following items:</span></span>

- <span data-ttu-id="ad39d-112">Subskrypcja usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad39d-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="ad39d-113">RFPIO pojedynczy znak z włączoną subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ad39d-113">A RFPIO single sign-on-enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="ad39d-114">Nie zaleca się użyć procedura hello tootest środowiska produkcyjnego w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="ad39d-114">We don't recommend that you use a production environment tootest hello steps in this tutorial.</span></span>

<span data-ttu-id="ad39d-115">kroki hello tootest w tym samouczku, wykonaj te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ad39d-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="ad39d-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ad39d-116">Do not use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="ad39d-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać [miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ad39d-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ad39d-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ad39d-118">Scenario description</span></span>
<span data-ttu-id="ad39d-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ad39d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ad39d-120">Scenariusz Hello, opisaną w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ad39d-120">hello scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ad39d-121">Dodawanie RFPIO z galerii hello.</span><span class="sxs-lookup"><span data-stu-id="ad39d-121">Adding RFPIO from hello gallery.</span></span>
2. <span data-ttu-id="ad39d-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="ad39d-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-rfpio-from-hello-gallery"></a><span data-ttu-id="ad39d-123">Dodaj RFPIO z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ad39d-123">Add RFPIO from hello gallery</span></span>
<span data-ttu-id="ad39d-124">tooconfigure hello integracji RFPIO do usługi Azure AD, należy tooadd RFPIO z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ad39d-124">tooconfigure hello integration of RFPIO into Azure AD, you need tooadd RFPIO from hello gallery tooyour list of managed SaaS apps.</span></span>

### <a name="tooadd-rfpio-from-hello-gallery"></a><span data-ttu-id="ad39d-125">tooadd RFPIO z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ad39d-125">tooadd RFPIO from hello gallery</span></span>

1. <span data-ttu-id="ad39d-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello w lewym okienku nawigacji, wybierz hello **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ad39d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="ad39d-128">Wybierz **aplikacje dla przedsiębiorstw**, a następnie wybierz **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ad39d-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ad39d-130">tooadd nowej aplikacji, wybierz opcję hello **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ad39d-130">tooadd a new application, select hello **New application** button on hello top of dialog box.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ad39d-132">W polu wyszukiwania hello wpisz **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="ad39d-132">In hello search box, type **RFPIO**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. <span data-ttu-id="ad39d-134">W panelu wyników hello, wybierz **RFPIO**, a następnie wybierz hello **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ad39d-134">In hello results panel, select **RFPIO**, and then select hello **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ad39d-136">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ad39d-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="ad39d-137">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z RFPIO w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="ad39d-137">In this section, you configure and test Azure AD single sign-on with RFPIO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ad39d-138">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow jakie relacje hello jest odpowiednikiem użytkownika w RFPIO i użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad39d-138">For single sign-on toowork, Azure AD needs tooknow what hello relationship is between counterpart user in RFPIO and a user in Azure AD.</span></span> <span data-ttu-id="ad39d-139">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w RFPIO musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="ad39d-139">In other words, a link relationship between an Azure AD user and hello related user in RFPIO needs toobe established.</span></span>

<span data-ttu-id="ad39d-140">W RFPIO, należy przypisać wartość hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="ad39d-140">In RFPIO, assign hello value of **user name** in Azure AD as hello value of  **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ad39d-141">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z RFPIO, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ad39d-141">tooconfigure and test Azure AD single sign-on with RFPIO, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ad39d-142">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**— tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ad39d-142">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ad39d-143">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**— tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ad39d-143">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)**-- tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ad39d-144">**[Tworzenie użytkownika testowego RFPIO](#creating-a-rfpio-test-user)**  — toohave odpowiednikiem Simona Britta w RFPIO, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ad39d-144">**[Create a RFPIO test user](#creating-a-rfpio-test-user)** --toohave a counterpart of Britta Simon in RFPIO that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ad39d-145">**[Przypisz użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**tooenable — Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ad39d-145">**[Assign hello Azure AD test user](#assigning-the-azure-ad-test-user)**--tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ad39d-146">**[Test rejestracji jednokrotnej](#testing-single-sign-on)**  — tooverify, jeśli konfiguracja hello działa.</span><span class="sxs-lookup"><span data-stu-id="ad39d-146">**[Test Single Sign-On](#testing-single-sign-on)** --tooverify if hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ad39d-147">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ad39d-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ad39d-148">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji RFPIO.</span><span class="sxs-lookup"><span data-stu-id="ad39d-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RFPIO application.</span></span>

<span data-ttu-id="ad39d-149">**tooconfigure usługi Azure AD rejestracji jednokrotnej z RFPIO, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ad39d-149">**tooconfigure Azure AD single sign-on with RFPIO, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad39d-150">W portalu Azure na powitania hello **RFPIO** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ad39d-150">In hello Azure portal, on hello **RFPIO** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="ad39d-152">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ad39d-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. <span data-ttu-id="ad39d-154">Na powitania **RFPIO domeny i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="ad39d-154">On hello **RFPIO Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    <span data-ttu-id="ad39d-156">a.</span><span class="sxs-lookup"><span data-stu-id="ad39d-156">a.</span></span> <span data-ttu-id="ad39d-157">W hello **identyfikator** pole tekstowe, wprowadź adres URL hello:`https://www.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="ad39d-157">In hello **Identifier** textbox, type hello URL: `https://www.rfpio.com`</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    <span data-ttu-id="ad39d-159">b.</span><span class="sxs-lookup"><span data-stu-id="ad39d-159">b.</span></span> <span data-ttu-id="ad39d-160">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="ad39d-160">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="ad39d-161">c.</span><span class="sxs-lookup"><span data-stu-id="ad39d-161">c.</span></span> <span data-ttu-id="ad39d-162">W hello **stan przekazywania** pole tekstowe Wprowadź wartość ciągu.</span><span class="sxs-lookup"><span data-stu-id="ad39d-162">In hello **Relay State** textbox enter a string value.</span></span> <span data-ttu-id="ad39d-163">Skontaktuj się z [RFPIO obsługuje zespołu](https://www.rfpio.com/contact/) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="ad39d-163">Contact [RFPIO support team](https://www.rfpio.com/contact/) tooget this value.</span></span> 

4. <span data-ttu-id="ad39d-164">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="ad39d-164">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="ad39d-165">Jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="ad39d-165">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>   

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    <span data-ttu-id="ad39d-167">W hello **Zaloguj się na adres URL** pole tekstowe, wprowadź adres URL hello:`https://www.app.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="ad39d-167">In hello **Sign on URL** textbox, type hello URL: `https://www.app.rfpio.com`</span></span>

5. <span data-ttu-id="ad39d-168">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ad39d-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. <span data-ttu-id="ad39d-170">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ad39d-170">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="ad39d-172">W oknie przeglądarki innej witryny sieci web, logowania toohello **RFPIO** witryny sieci Web jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ad39d-172">In a different web browser window, login toohello **RFPIO** website as an administrator.</span></span>

8. <span data-ttu-id="ad39d-173">Polecenie hello dolnej lewym rogu z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="ad39d-173">Click on hello bottom left corner dropdown.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. <span data-ttu-id="ad39d-175">Polecenie hello **ustawienia organizacji**.</span><span class="sxs-lookup"><span data-stu-id="ad39d-175">Click on hello **Organization Settings**.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. <span data-ttu-id="ad39d-177">Polecenie hello **funkcje & integracji**.</span><span class="sxs-lookup"><span data-stu-id="ad39d-177">Click on hello **FEATURES & INTEGRATION**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. <span data-ttu-id="ad39d-179">W hello **konfiguracji logowania jednokrotnego SAML** kliknij **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="ad39d-179">In hello **SAML SSO Configuration** Click **Edit**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. <span data-ttu-id="ad39d-181">W tej sekcji należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ad39d-181">In this Section perform following actions:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    <span data-ttu-id="ad39d-183">a.</span><span class="sxs-lookup"><span data-stu-id="ad39d-183">a.</span></span> <span data-ttu-id="ad39d-184">Skopiuj zawartość hello hello **pobierane metadane XML** i wklej go do hello **konfiguracji tożsamości** pola.</span><span class="sxs-lookup"><span data-stu-id="ad39d-184">Copy hello content of hello **Downloaded Metadata XML** and paste it into hello **identity configuration** field.</span></span>

    > [!NOTE]
    ><span data-ttu-id="ad39d-185">pobrane hello toocopy zawartości **XML metadanych** użyj **Notatnik ++** lub właściwe **edytora XML**.</span><span class="sxs-lookup"><span data-stu-id="ad39d-185">toocopy hello content of downloaded **Metadata XML** Use **Notepad++** or proper **XML Editor**.</span></span> 

    <span data-ttu-id="ad39d-186">b.</span><span class="sxs-lookup"><span data-stu-id="ad39d-186">b.</span></span> <span data-ttu-id="ad39d-187">Kliknij przycisk **zweryfikować**.</span><span class="sxs-lookup"><span data-stu-id="ad39d-187">Click **Validate**.</span></span>

    <span data-ttu-id="ad39d-188">c.</span><span class="sxs-lookup"><span data-stu-id="ad39d-188">c.</span></span> <span data-ttu-id="ad39d-189">Po kliknięcie przycisku **weryfikacji**, przerzucania **SAML(Enabled)** tooon.</span><span class="sxs-lookup"><span data-stu-id="ad39d-189">After Clicking **Validate**, Flip **SAML(Enabled)** tooon.</span></span>

    <span data-ttu-id="ad39d-190">d.</span><span class="sxs-lookup"><span data-stu-id="ad39d-190">d.</span></span> <span data-ttu-id="ad39d-191">Kliknij przycisk **przesłać**.</span><span class="sxs-lookup"><span data-stu-id="ad39d-191">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="ad39d-192">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="ad39d-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ad39d-193">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="ad39d-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ad39d-194">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ad39d-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ad39d-195">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad39d-195">Create an Azure AD test user</span></span>
<span data-ttu-id="ad39d-196">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="ad39d-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="ad39d-198">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ad39d-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad39d-199">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ad39d-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ad39d-201">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ad39d-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ad39d-203">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ad39d-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ad39d-205">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ad39d-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ad39d-207">a.</span><span class="sxs-lookup"><span data-stu-id="ad39d-207">a.</span></span> <span data-ttu-id="ad39d-208">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ad39d-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ad39d-209">b.</span><span class="sxs-lookup"><span data-stu-id="ad39d-209">b.</span></span> <span data-ttu-id="ad39d-210">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ad39d-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ad39d-211">c.</span><span class="sxs-lookup"><span data-stu-id="ad39d-211">c.</span></span> <span data-ttu-id="ad39d-212">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="ad39d-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ad39d-213">d.</span><span class="sxs-lookup"><span data-stu-id="ad39d-213">d.</span></span> <span data-ttu-id="ad39d-214">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ad39d-214">Click **Create**.</span></span>
 
### <a name="create-a-rfpio-test-user"></a><span data-ttu-id="ad39d-215">Tworzenie użytkownika testowego RFPIO</span><span class="sxs-lookup"><span data-stu-id="ad39d-215">Create a RFPIO test user</span></span>

<span data-ttu-id="ad39d-216">toolog użytkowników tooenable usługi Azure AD w tooRFPIO, muszą mieć przydzielone do RFPIO.</span><span class="sxs-lookup"><span data-stu-id="ad39d-216">tooenable Azure AD users toolog in tooRFPIO, they must be provisioned into RFPIO.</span></span>  
<span data-ttu-id="ad39d-217">W przypadku hello RFPIO Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="ad39d-217">In hello case of RFPIO, provisioning is a manual task.</span></span>

<span data-ttu-id="ad39d-218">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ad39d-218">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad39d-219">Zaloguj się za tooyour RFPIO witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ad39d-219">Log in tooyour RFPIO company site as an administrator.</span></span>

2. <span data-ttu-id="ad39d-220">Polecenie hello dolnej lewym rogu z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="ad39d-220">Click on hello bottom left corner dropdown.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. <span data-ttu-id="ad39d-222">Polecenie hello **ustawienia organizacji**.</span><span class="sxs-lookup"><span data-stu-id="ad39d-222">Click on hello **Organization Settings**.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. <span data-ttu-id="ad39d-224">Kliknij przycisk **członków zespołu**.</span><span class="sxs-lookup"><span data-stu-id="ad39d-224">Click **TEAM MEMBERS**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. <span data-ttu-id="ad39d-226">Polecenie **Dodaj członków**.</span><span class="sxs-lookup"><span data-stu-id="ad39d-226">Click on **ADD MEMBERS**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. <span data-ttu-id="ad39d-228">W hello **Dodawanie nowych elementów członkowskich** sekcji.</span><span class="sxs-lookup"><span data-stu-id="ad39d-228">In hello **Add New Members** section.</span></span> <span data-ttu-id="ad39d-229">Wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ad39d-229">Perform following actions:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/app8.png)

    <span data-ttu-id="ad39d-231">a.</span><span class="sxs-lookup"><span data-stu-id="ad39d-231">a.</span></span> <span data-ttu-id="ad39d-232">Wprowadź **adres E-mail** w hello **Podaj jeden adres e-mail w jednym wierszu** pola.</span><span class="sxs-lookup"><span data-stu-id="ad39d-232">Enter **Email address** in hello **Enter one email per line** field.</span></span>

    <span data-ttu-id="ad39d-233">b.</span><span class="sxs-lookup"><span data-stu-id="ad39d-233">b.</span></span> <span data-ttu-id="ad39d-234">Wybierz Plese **roli** zgodnie z wymaganiami.</span><span class="sxs-lookup"><span data-stu-id="ad39d-234">Plese select **Role** according your requirements.</span></span>

    <span data-ttu-id="ad39d-235">c.</span><span class="sxs-lookup"><span data-stu-id="ad39d-235">c.</span></span> <span data-ttu-id="ad39d-236">Kliknij przycisk **Dodaj członków**.</span><span class="sxs-lookup"><span data-stu-id="ad39d-236">Click **ADD MEMBERS**.</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="ad39d-237">Właściciel konta usługi Azure Active Directory Hello otrzymuje wiadomość e-mail i następuje tooconfirm łącze swojego konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="ad39d-237">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ad39d-238">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad39d-238">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ad39d-239">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooRFPIO.</span><span class="sxs-lookup"><span data-stu-id="ad39d-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRFPIO.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="ad39d-241">**tooassign tooRFPIO Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ad39d-241">**tooassign Britta Simon tooRFPIO, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad39d-242">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ad39d-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ad39d-244">Z listy aplikacji hello wybierz **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="ad39d-244">In hello applications list, select **RFPIO**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. <span data-ttu-id="ad39d-246">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ad39d-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="ad39d-248">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ad39d-248">Click **Add** button.</span></span> <span data-ttu-id="ad39d-249">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ad39d-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="ad39d-251">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ad39d-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ad39d-252">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ad39d-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ad39d-253">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ad39d-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ad39d-254">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ad39d-254">Test single sign-on</span></span>

<span data-ttu-id="ad39d-255">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ad39d-255">In this section, you test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="ad39d-256">Po kliknięciu hello RFPIO kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour RFPIO aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ad39d-256">When you click hello RFPIO tile in hello Access Panel, you should get automatically signed-on tooyour RFPIO application.</span></span>
<span data-ttu-id="ad39d-257">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ad39d-257">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ad39d-258">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ad39d-258">Additional resources</span></span>

* [<span data-ttu-id="ad39d-259">Lista samouczków dotyczących toointegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ad39d-259">List of tutorials about how toointegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ad39d-260">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ad39d-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

