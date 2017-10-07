---
title: 'Samouczek: Integracji Azure Active Directory z Clarizen | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Clarizen."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: f24ccda3b90e5df9a203a444dfda905043b30276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a><span data-ttu-id="954da-103">Samouczek: Integracji Azure Active Directory z Clarizen</span><span class="sxs-lookup"><span data-stu-id="954da-103">Tutorial: Azure Active Directory integration with Clarizen</span></span>

<span data-ttu-id="954da-104">Z tego samouczka, dowiesz się, jak Azure Active Directory (Azure AD) z Clarizen toointegrate.</span><span class="sxs-lookup"><span data-stu-id="954da-104">In this tutorial, you learn how toointegrate Azure Active Directory (Azure AD) with Clarizen.</span></span> <span data-ttu-id="954da-105">Umożliwia to integracji hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="954da-105">This integration gives you hello following benefits:</span></span>

- <span data-ttu-id="954da-106">Można kontrolować, w usłudze Azure AD, kto ma dostęp do tooClarizen.</span><span class="sxs-lookup"><span data-stu-id="954da-106">You can control, in Azure AD, who has access tooClarizen.</span></span>
- <span data-ttu-id="954da-107">Można włączyć użytkownika toobe użytkowników zostanie automatycznie zalogowany tooClarizen (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="954da-107">You can enable your users toobe automatically signed in tooClarizen (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="954da-108">Możesz zarządzać kont w jednej centralnej lokalizacji, hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="954da-108">You can manage your accounts in one central location, hello Azure portal.</span></span>

<span data-ttu-id="954da-109">Scenariusz Hello w tym samouczku składa się z dwóch głównych zadań:</span><span class="sxs-lookup"><span data-stu-id="954da-109">hello scenario in this tutorial consists of two main tasks:</span></span>

1. <span data-ttu-id="954da-110">Dodaj Clarizen z galerii hello.</span><span class="sxs-lookup"><span data-stu-id="954da-110">Add Clarizen from hello gallery.</span></span>
2. <span data-ttu-id="954da-111">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="954da-111">Configure and test Azure AD single sign-on.</span></span>

<span data-ttu-id="954da-112">Więcej informacji na temat oprogramowania jako usługa (SaaS) integracji aplikacji z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="954da-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="954da-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="954da-113">Prerequisites</span></span>
<span data-ttu-id="954da-114">tooconfigure integracji z usługą Azure AD z Clarizen należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="954da-114">tooconfigure Azure AD integration with Clarizen, you need hello following items:</span></span>

- <span data-ttu-id="954da-115">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="954da-115">An Azure AD subscription</span></span>
- <span data-ttu-id="954da-116">Clarizen subskrypcji, która jest włączone dla rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="954da-116">A Clarizen subscription that's enabled for single sign-on</span></span>

<span data-ttu-id="954da-117">kroki hello tootest w tym samouczku, wykonaj te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="954da-117">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="954da-118">Testowanie usługi Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="954da-118">Test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="954da-119">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="954da-119">Don't use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="954da-120">Jeśli nie masz usługi Azure AD w środowisku testowym, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="954da-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="add-clarizen-from-hello-gallery"></a><span data-ttu-id="954da-121">Dodaj Clarizen z galerii hello</span><span class="sxs-lookup"><span data-stu-id="954da-121">Add Clarizen from hello gallery</span></span>
<span data-ttu-id="954da-122">Integracja hello tooconfigure Clarizen w usłudze Azure AD, Dodaj Clarizen hello galerii tooyour listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="954da-122">tooconfigure hello integration of Clarizen into Azure AD, add Clarizen from hello gallery tooyour list of managed SaaS apps.</span></span>

1. <span data-ttu-id="954da-123">W hello [portalu Azure](https://portal.azure.com), w lewym okienku hello, kliknij przycisk hello **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="954da-123">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Active Directory** icon.</span></span>

    ![Ikona usługi Azure Active Directory][1]

2. <span data-ttu-id="954da-125">Kliknij przycisk **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="954da-125">Click **Enterprise applications**.</span></span> <span data-ttu-id="954da-126">Następnie kliknij przycisk **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="954da-126">Then click **All applications**.</span></span>

    ![Kliknięcie przycisku "aplikacje przedsiębiorstwa" i "Wszystkie aplikacje"][2]

3. <span data-ttu-id="954da-128">Kliknij przycisk hello **Dodaj** u góry hello hello — okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="954da-128">Click hello **Add** button at hello top of hello dialog box.</span></span>

    ![przycisk "Dodaj" Hello][3]

4. <span data-ttu-id="954da-130">W polu wyszukiwania hello wpisz **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="954da-130">In hello search box, type **Clarizen**.</span></span>

    ![Wpisz "Clarizen" w polu wyszukiwania hello](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. <span data-ttu-id="954da-132">Wybierz w okienku wyników hello **Clarizen**, a następnie kliknij przycisk **Dodaj** tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="954da-132">In hello results pane, select **Clarizen**, and then click **Add** tooadd hello application.</span></span>

    ![Wybieranie Clarizen w okienku wyników hello](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="954da-134">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="954da-134">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="954da-135">W hello następujące sekcje zawierają informacje skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Clarizen na podstawie użytkownika testu hello Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="954da-135">In hello following sections, you configure and test Azure AD single sign-on with Clarizen based on hello test user Britta Simon.</span></span>

<span data-ttu-id="954da-136">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Clarizen jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="954da-136">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Clarizen is tooa user in Azure AD.</span></span> <span data-ttu-id="954da-137">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Clarizen musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="954da-137">In other words, a link relationship between an Azure AD user and hello related user in Clarizen needs toobe established.</span></span> <span data-ttu-id="954da-138">Ustanowić tę relację łącza, przypisując wartość hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello **Username** w Clarizen.</span><span class="sxs-lookup"><span data-stu-id="954da-138">You establish this link relationship by assigning hello value of **user name** in Azure AD as hello value of **Username** in Clarizen.</span></span>

<span data-ttu-id="954da-139">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Clarizen, pełną powitania po bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="954da-139">tooconfigure and test Azure AD single sign-on with Clarizen, complete hello following building blocks:</span></span>

1. <span data-ttu-id="954da-140">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="954da-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="954da-141">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="954da-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="954da-142">**[Tworzenie użytkownika testowego Clarizen](#create-a-clarizen-test-user)**  toohave odpowiednikiem Simona Britta w Clarizen, że jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="954da-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** toohave a counterpart of Britta Simon in Clarizen that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="954da-143">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="954da-143">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="954da-144">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="954da-144">**[Test single sign-on](#test-single-sign-on)** tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="954da-145">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="954da-145">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="954da-146">Włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Clarizen.</span><span class="sxs-lookup"><span data-stu-id="954da-146">Enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Clarizen application.</span></span>

1. <span data-ttu-id="954da-147">W portalu Azure na powitania hello **Clarizen** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="954da-147">In hello Azure portal, on hello **Clarizen** application integration page, click **Single sign-on**.</span></span>

    ![Kliknięcie przycisku "Logowanie jednokrotne"][4]

2. <span data-ttu-id="954da-149">W hello **logowanie jednokrotne** okno dialogowe dla **tryb**, wybierz pozycję **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="954da-149">In hello **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** tooenable single sign-on.</span></span>

    ![Wybieranie "na podstawie SAML logowania"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. <span data-ttu-id="954da-151">W hello **Clarizen domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="954da-151">In hello **Clarizen Domain and URLs** section, perform hello following steps:</span></span>

    ![Pola Adres URL identyfikatora i odpowiedzi](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    <span data-ttu-id="954da-153">a.</span><span class="sxs-lookup"><span data-stu-id="954da-153">a.</span></span> <span data-ttu-id="954da-154">W hello **identyfikator** polu wartość hello typu jako: **Clarizen**</span><span class="sxs-lookup"><span data-stu-id="954da-154">In hello **Identifier** box, type hello value as: **Clarizen**</span></span>

    <span data-ttu-id="954da-155">b.</span><span class="sxs-lookup"><span data-stu-id="954da-155">b.</span></span> <span data-ttu-id="954da-156">W hello **adres URL odpowiedzi** wpisz adres URL przy użyciu hello następującego wzorca: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span><span class="sxs-lookup"><span data-stu-id="954da-156">In hello **Reply URL** box, type a URL by using hello following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span></span>

    > [!NOTE]
    > <span data-ttu-id="954da-157">Nie są hello wartości rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="954da-157">These are not hello real values.</span></span> <span data-ttu-id="954da-158">Masz toouse hello rzeczywisty identyfikator i adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="954da-158">You have toouse hello actual identifier and reply URL.</span></span> <span data-ttu-id="954da-159">W tym miejscu zalecamy Użyj hello unikatowej wartości ciągu, ponieważ hello identyfikator.</span><span class="sxs-lookup"><span data-stu-id="954da-159">Here we suggest that you use hello unique value of a string as hello identifier.</span></span> <span data-ttu-id="954da-160">tooget hello wartości rzeczywistych, skontaktuj się z pomocą hello [zespołem pomocy technicznej Clarizen](https://success.clarizen.com/hc/en-us/requests/new).</span><span class="sxs-lookup"><span data-stu-id="954da-160">tooget hello actual values, contact hello [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span></span>

4. <span data-ttu-id="954da-161">Na powitania **certyfikat podpisywania SAML** kliknij **Utwórz nowy certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="954da-161">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Klikając przycisk "Utwórz nowy certyfikat"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. <span data-ttu-id="954da-163">W hello **Tworzenie nowego świadectwa** okno dialogowe pola, kliknij ikonę kalendarza hello i wybierz datę wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="954da-163">In hello **Create New Certificate** dialog box, click hello calendar icon and select an expiry date.</span></span> <span data-ttu-id="954da-164">Następnie kliknij przycisk **Save** (Zapisz).</span><span class="sxs-lookup"><span data-stu-id="954da-164">Then click **Save**.</span></span>

    ![Wybranie i zapisanie Data wygaśnięcia](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="954da-166">W hello **certyfikat podpisywania SAML** wybierz opcję **uaktywnić nowy certyfikat**, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="954da-166">In hello **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span></span>

    ![Po zaznaczeniu pola wyboru hello na uaktywnienie hello nowego certyfikatu](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. <span data-ttu-id="954da-168">W hello **certyfikat przerzucania** okno dialogowe, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="954da-168">In hello **Rollover certificate** dialog box, click **OK**.</span></span>

    ![Klikając przycisk OK, tooconfirm, które mają certyfikat hello toomake active](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="954da-170">W hello **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="954da-170">In hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Klikając przycisk Pobierz hello toostart "Certyfikat (Base64)"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. <span data-ttu-id="954da-172">W hello **konfiguracji Clarizen** , kliknij przycisk **skonfigurować Clarizen** tooopen hello **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="954da-172">In hello **Clarizen Configuration** section, click **Configure Clarizen** tooopen hello **Configure sign-on** window.</span></span>

    ![Klikając przycisk "Konfigurowanie Clarizen"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![Okno "Konfigurowanie logowania jednokrotnego", w tym adresy URL i pliki](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. <span data-ttu-id="954da-175">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy Clarizen tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="954da-175">In a different web browser window, sign in tooyour Clarizen company site as an administrator.</span></span>

11. <span data-ttu-id="954da-176">Kliknij nazwy użytkownika, a następnie kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="954da-176">Click your username, and then click **Settings**.</span></span>

    <span data-ttu-id="954da-177">![Klikając pozycję "Ustawienia" w obszarze nazwy użytkownika](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="954da-177">![Clicking "Settings" under your username](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span></span>

12. <span data-ttu-id="954da-178">Kliknij przycisk hello **ustawienia globalne** kartę. Następnie dalej zbyt**Federated Authentication**, kliknij przycisk **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="954da-178">Click hello **Global Settings** tab. Then, next too**Federated Authentication**, click **edit**.</span></span>

    <span data-ttu-id="954da-179">![Kartę "Ustawienia globalne"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "ustawienia globalne")</span><span class="sxs-lookup"><span data-stu-id="954da-179">!["Global Settings" tab](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span></span>

13. <span data-ttu-id="954da-180">W hello **Federated Authentication** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="954da-180">In hello **Federated Authentication** dialog box, perform hello following steps:</span></span>

    <span data-ttu-id="954da-181">![Okno dialogowe "Uwierzytelnianie federacyjne"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span><span class="sxs-lookup"><span data-stu-id="954da-181">!["Federated Authentication" dialog box](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span></span>

    <span data-ttu-id="954da-182">a.</span><span class="sxs-lookup"><span data-stu-id="954da-182">a.</span></span> <span data-ttu-id="954da-183">Wybierz **uwierzytelnianie federacyjne Włącz**.</span><span class="sxs-lookup"><span data-stu-id="954da-183">Select **Enable Federated Authentication**.</span></span>

    <span data-ttu-id="954da-184">b.</span><span class="sxs-lookup"><span data-stu-id="954da-184">b.</span></span> <span data-ttu-id="954da-185">Kliknij przycisk **przekazać** tooupload pobranego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="954da-185">Click **Upload** tooupload your downloaded certificate.</span></span>

    <span data-ttu-id="954da-186">c.</span><span class="sxs-lookup"><span data-stu-id="954da-186">c.</span></span> <span data-ttu-id="954da-187">W hello **adres URL logowania** wprowadź wartość hello **SAML pojedynczy znak na adres URL usługi** z okna konfiguracji aplikacji hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="954da-187">In hello **Sign-in URL** box, enter hello value of **SAML Single Sign-On Service URL** from hello Azure AD application configuration window.</span></span>

    <span data-ttu-id="954da-188">d.</span><span class="sxs-lookup"><span data-stu-id="954da-188">d.</span></span> <span data-ttu-id="954da-189">W hello **Sign-out URL** wprowadź wartość hello **Sign-Out URL** z okna konfiguracji aplikacji hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="954da-189">In hello **Sign-out URL** box, enter hello value of **Sign-Out URL** from hello Azure AD application configuration window.</span></span>

    <span data-ttu-id="954da-190">e.</span><span class="sxs-lookup"><span data-stu-id="954da-190">e.</span></span> <span data-ttu-id="954da-191">Wybierz **Użyj POST**.</span><span class="sxs-lookup"><span data-stu-id="954da-191">Select **Use POST**.</span></span>

    <span data-ttu-id="954da-192">f.</span><span class="sxs-lookup"><span data-stu-id="954da-192">f.</span></span> <span data-ttu-id="954da-193">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="954da-193">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="954da-194">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="954da-194">Create an Azure AD test user</span></span>
<span data-ttu-id="954da-195">W portalu Azure hello Tworzenie użytkownika testowego o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="954da-195">In hello Azure portal, create a test user called Britta Simon.</span></span>

![Nazwa i adres e-mail użytkownika testu hello Azure AD][100]

1. <span data-ttu-id="954da-197">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="954da-197">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** icon.</span></span>

    ![Ikona usługi Azure Active Directory](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="954da-199">Kliknij przycisk **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="954da-199">Click **Users and groups**, and then click **All users** toodisplay hello list of users.</span></span>

    ![Klikając pozycję "Użytkownicy i grupy" i "Wszyscy użytkownicy"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="954da-201">U góry hello hello — okno dialogowe, kliknij przycisk **Dodaj** tooopen hello **użytkownika** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="954da-201">At hello top of hello dialog box, click **Add** tooopen hello **User** dialog box.</span></span>

    ![przycisk "Dodaj" Hello](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="954da-203">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="954da-203">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Okno dialogowe "Użytkownika" z nazwę, adres e-mail i hasło wypełnione](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    <span data-ttu-id="954da-205">a.</span><span class="sxs-lookup"><span data-stu-id="954da-205">a.</span></span> <span data-ttu-id="954da-206">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="954da-206">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="954da-207">b.</span><span class="sxs-lookup"><span data-stu-id="954da-207">b.</span></span> <span data-ttu-id="954da-208">W hello **nazwy użytkownika** pole adresu e-mail hello typu hello Simona Britta konta.</span><span class="sxs-lookup"><span data-stu-id="954da-208">In hello **User name** box, type hello email address of hello Britta Simon account.</span></span>

    <span data-ttu-id="954da-209">c.</span><span class="sxs-lookup"><span data-stu-id="954da-209">c.</span></span> <span data-ttu-id="954da-210">Wybierz **Pokaż hasło** i zanotuj wartość hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="954da-210">Select **Show Password** and write down hello value of **Password**.</span></span>

    <span data-ttu-id="954da-211">d.</span><span class="sxs-lookup"><span data-stu-id="954da-211">d.</span></span> <span data-ttu-id="954da-212">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="954da-212">Click **Create**.</span></span>

### <a name="create-a-clarizen-test-user"></a><span data-ttu-id="954da-213">Tworzenie użytkownika testowego Clarizen</span><span class="sxs-lookup"><span data-stu-id="954da-213">Create a Clarizen test user</span></span>
<span data-ttu-id="954da-214">tooenable toosign użytkowników usługi Azure AD w tooClarizen, należy udostępnić kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="954da-214">tooenable Azure AD users toosign in tooClarizen, you must provision user accounts.</span></span> <span data-ttu-id="954da-215">W przypadku hello Clarizen Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="954da-215">In hello case of Clarizen, provisioning is a manual task.</span></span>

1. <span data-ttu-id="954da-216">Zaloguj się tooyour Clarizen witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="954da-216">Sign in tooyour Clarizen company site as an administrator.</span></span>

2. <span data-ttu-id="954da-217">Kliknij przycisk **osób**.</span><span class="sxs-lookup"><span data-stu-id="954da-217">Click **People**.</span></span>

    <span data-ttu-id="954da-218">![Klikając przycisk "Osoby"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "osób")</span><span class="sxs-lookup"><span data-stu-id="954da-218">![Clicking "People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="954da-219">Kliknij przycisk **zaprosić użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="954da-219">Click **Invite User**.</span></span>

    <span data-ttu-id="954da-220">![Przycisk "Zaprosić użytkowników"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "zaprosić użytkowników")</span><span class="sxs-lookup"><span data-stu-id="954da-220">!["Invite User" button](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="954da-221">W hello **zaprosić użytkowników** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="954da-221">In hello **Invite People** dialog box, perform hello following steps:</span></span>

    <span data-ttu-id="954da-222">![Okno dialogowe "Zaproś inne osoby"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "zaprosić użytkowników")</span><span class="sxs-lookup"><span data-stu-id="954da-222">!["Invite People" dialog box](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="954da-223">a.</span><span class="sxs-lookup"><span data-stu-id="954da-223">a.</span></span> <span data-ttu-id="954da-224">W hello **E-mail** pole adresu e-mail hello typu hello Simona Britta konta.</span><span class="sxs-lookup"><span data-stu-id="954da-224">In hello **Email** box, type hello email address of hello Britta Simon account.</span></span>

    <span data-ttu-id="954da-225">b.</span><span class="sxs-lookup"><span data-stu-id="954da-225">b.</span></span> <span data-ttu-id="954da-226">Kliknij przycisk **zaprosić**.</span><span class="sxs-lookup"><span data-stu-id="954da-226">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="954da-227">właścicielem konta usługi Azure Active Directory Hello będzie otrzymywać wiadomości e-mail i postępuj zgodnie tooconfirm łącze swojego konta przed staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="954da-227">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="954da-228">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="954da-228">Assign hello Azure AD test user</span></span>
<span data-ttu-id="954da-229">Włącz toouse Simona Britta Azure rejestracji jednokrotnej, przyznając jej tooClarizen dostępu.</span><span class="sxs-lookup"><span data-stu-id="954da-229">Enable Britta Simon toouse Azure single sign-on by granting her access tooClarizen.</span></span>

![Test przypisany użytkownik][200]

1. <span data-ttu-id="954da-231">W portalu Azure hello, otwórz widok aplikacji hello, przejdź do widoku katalogu toohello, kliknij przycisk **aplikacje dla przedsiębiorstw**, a następnie kliknij przycisk **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="954da-231">In hello Azure portal, open hello applications view, browse toohello directory view, click **Enterprise applications**, and then click **All applications**.</span></span>

    ![Kliknięcie przycisku "aplikacje przedsiębiorstwa" i "Wszystkie aplikacje"][201]

2. <span data-ttu-id="954da-233">Z listy aplikacji hello wybierz **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="954da-233">In hello applications list, select **Clarizen**.</span></span>

    ![Wybierając Clarizen hello listy](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. <span data-ttu-id="954da-235">W okienku po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="954da-235">In hello left pane, click **Users and groups**.</span></span>

    ![Klikając pozycję "Użytkownicy i grupy"][202]

4. <span data-ttu-id="954da-237">Kliknij przycisk hello **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="954da-237">Click hello **Add** button.</span></span> <span data-ttu-id="954da-238">Następnie w hello **Dodaj przydziału** okno dialogowe, wybierz opcję **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="954da-238">Then, in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Hello przycisk "Dodaj" i "Dodaj przydziału" hello, okno dialogowe][203]

5. <span data-ttu-id="954da-240">W hello **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="954da-240">In hello **Users and groups** dialog box, select **Britta Simon** in hello list of users.</span></span>

6. <span data-ttu-id="954da-241">W hello **użytkowników i grup** okna dialogowego kliknij hello **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="954da-241">In hello **Users and groups** dialog box, click hello **Select** button.</span></span>

7. <span data-ttu-id="954da-242">W hello **Dodaj przydziału** okna dialogowego kliknij hello **przypisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="954da-242">In hello **Add Assignment** dialog box, click hello **Assign** button.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="954da-243">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="954da-243">Test single sign-on</span></span>
<span data-ttu-id="954da-244">Test konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="954da-244">Test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="954da-245">Po kliknięciu kafelka Clarizen hello w panelu dostępu hello powinny być automatycznie zalogowano tooyour Clarizen aplikacji.</span><span class="sxs-lookup"><span data-stu-id="954da-245">When you click hello Clarizen tile in hello Access Panel, you should be automatically signed in tooyour Clarizen application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="954da-246">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="954da-246">Additional resources</span></span>

* [<span data-ttu-id="954da-247">Lista samouczków dotyczących toointegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="954da-247">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="954da-248">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="954da-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
