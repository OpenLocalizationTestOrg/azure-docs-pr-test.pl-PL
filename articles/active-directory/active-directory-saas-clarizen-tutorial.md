---
title: 'Samouczek: Integracji Azure Active Directory z Clarizen | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Clarizen."
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
ms.openlocfilehash: 574c6877bddac8be7d6d541bfabbdc10f6be3101
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a><span data-ttu-id="ac72e-103">Samouczek: Integracji Azure Active Directory z Clarizen</span><span class="sxs-lookup"><span data-stu-id="ac72e-103">Tutorial: Azure Active Directory integration with Clarizen</span></span>

<span data-ttu-id="ac72e-104">Z tego samouczka dowiesz Integrowanie usługi Azure Active Directory (Azure AD) z Clarizen.</span><span class="sxs-lookup"><span data-stu-id="ac72e-104">In this tutorial, you learn how to integrate Azure Active Directory (Azure AD) with Clarizen.</span></span> <span data-ttu-id="ac72e-105">Integracja ta zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ac72e-105">This integration gives you the following benefits:</span></span>

- <span data-ttu-id="ac72e-106">Można kontrolować, w usłudze Azure AD, który ma dostęp do Clarizen.</span><span class="sxs-lookup"><span data-stu-id="ac72e-106">You can control, in Azure AD, who has access to Clarizen.</span></span>
- <span data-ttu-id="ac72e-107">Można umożliwić użytkownikom można zostanie automatycznie zalogowany do Clarizen (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac72e-107">You can enable your users to be automatically signed in to Clarizen (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ac72e-108">Możesz zarządzać kont w jednej centralnej lokalizacji, portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ac72e-108">You can manage your accounts in one central location, the Azure portal.</span></span>

<span data-ttu-id="ac72e-109">Scenariusz, w tym samouczku składa się z dwóch głównych zadań:</span><span class="sxs-lookup"><span data-stu-id="ac72e-109">The scenario in this tutorial consists of two main tasks:</span></span>

1. <span data-ttu-id="ac72e-110">Dodaj Clarizen z galerii.</span><span class="sxs-lookup"><span data-stu-id="ac72e-110">Add Clarizen from the gallery.</span></span>
2. <span data-ttu-id="ac72e-111">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ac72e-111">Configure and test Azure AD single sign-on.</span></span>

<span data-ttu-id="ac72e-112">Więcej informacji na temat oprogramowania jako usługa (SaaS) integracji aplikacji z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ac72e-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac72e-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ac72e-113">Prerequisites</span></span>
<span data-ttu-id="ac72e-114">Aby skonfigurować integrację usługi Azure AD z Clarizen, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ac72e-114">To configure Azure AD integration with Clarizen, you need the following items:</span></span>

- <span data-ttu-id="ac72e-115">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac72e-115">An Azure AD subscription</span></span>
- <span data-ttu-id="ac72e-116">Clarizen subskrypcji, która jest włączone dla rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ac72e-116">A Clarizen subscription that's enabled for single sign-on</span></span>

<span data-ttu-id="ac72e-117">Aby przetestować kroki opisane w tym samouczku, wykonaj te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ac72e-117">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="ac72e-118">Testowanie usługi Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ac72e-118">Test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ac72e-119">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ac72e-119">Don't use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="ac72e-120">Jeśli nie masz usługi Azure AD w środowisku testowym, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ac72e-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="add-clarizen-from-the-gallery"></a><span data-ttu-id="ac72e-121">Dodaj Clarizen z galerii</span><span class="sxs-lookup"><span data-stu-id="ac72e-121">Add Clarizen from the gallery</span></span>
<span data-ttu-id="ac72e-122">Aby skonfigurować integrację usługi Azure AD Clarizen, należy dodać Clarizen z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ac72e-122">To configure the integration of Clarizen into Azure AD, add Clarizen from the gallery to your list of managed SaaS apps.</span></span>

1. <span data-ttu-id="ac72e-123">W [portalu Azure](https://portal.azure.com), w okienku po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ac72e-123">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Active Directory** icon.</span></span>

    ![Ikona usługi Azure Active Directory][1]

2. <span data-ttu-id="ac72e-125">Kliknij przycisk **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ac72e-125">Click **Enterprise applications**.</span></span> <span data-ttu-id="ac72e-126">Następnie kliknij przycisk **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ac72e-126">Then click **All applications**.</span></span>

    ![Kliknięcie przycisku "aplikacje przedsiębiorstwa" i "Wszystkie aplikacje"][2]

3. <span data-ttu-id="ac72e-128">Kliknij przycisk **Dodaj** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ac72e-128">Click the **Add** button at the top of the dialog box.</span></span>

    ![Przycisk "Dodaj"][3]

4. <span data-ttu-id="ac72e-130">W polu wyszukiwania wpisz **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="ac72e-130">In the search box, type **Clarizen**.</span></span>

    ![Wpisz "Clarizen" w polu wyszukiwania](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. <span data-ttu-id="ac72e-132">W okienku wyników wybierz **Clarizen**, a następnie kliknij przycisk **Dodaj** można dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="ac72e-132">In the results pane, select **Clarizen**, and then click **Add** to add the application.</span></span>

    ![Wybieranie Clarizen w okienku wyników](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ac72e-134">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ac72e-134">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="ac72e-135">W poniższych sekcjach skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Clarizen na podstawie użytkownika testu Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ac72e-135">In the following sections, you configure and test Azure AD single sign-on with Clarizen based on the test user Britta Simon.</span></span>

<span data-ttu-id="ac72e-136">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Clarizen jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac72e-136">For single sign-on to work, Azure AD needs to know what the counterpart user in Clarizen is to a user in Azure AD.</span></span> <span data-ttu-id="ac72e-137">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Clarizen musi się.</span><span class="sxs-lookup"><span data-stu-id="ac72e-137">In other words, a link relationship between an Azure AD user and the related user in Clarizen needs to be established.</span></span> <span data-ttu-id="ac72e-138">Ustanowić tę relację łącza, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Clarizen.</span><span class="sxs-lookup"><span data-stu-id="ac72e-138">You establish this link relationship by assigning the value of **user name** in Azure AD as the value of **Username** in Clarizen.</span></span>

<span data-ttu-id="ac72e-139">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Clarizen, wykonaj poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="ac72e-139">To configure and test Azure AD single sign-on with Clarizen, complete the following building blocks:</span></span>

1. <span data-ttu-id="ac72e-140">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  umożliwienie użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ac72e-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ac72e-141">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  do testowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ac72e-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ac72e-142">**[Tworzenie użytkownika testowego Clarizen](#create-a-clarizen-test-user)**  w celu zapewnienia odpowiednikiem Simona Britta Clarizen połączonego z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac72e-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** to have a counterpart of Britta Simon in Clarizen that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="ac72e-143">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  umożliwiające Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ac72e-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ac72e-144">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="ac72e-144">**[Test single sign-on](#test-single-sign-on)** to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ac72e-145">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ac72e-145">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="ac72e-146">Włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Clarizen.</span><span class="sxs-lookup"><span data-stu-id="ac72e-146">Enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clarizen application.</span></span>

1. <span data-ttu-id="ac72e-147">W portalu Azure na **Clarizen** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ac72e-147">In the Azure portal, on the **Clarizen** application integration page, click **Single sign-on**.</span></span>

    ![Kliknięcie przycisku "Logowanie jednokrotne"][4]

2. <span data-ttu-id="ac72e-149">W **logowanie jednokrotne** okno dialogowe dla **tryb**, wybierz pozycję **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="ac72e-149">In the **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Wybieranie "na podstawie SAML logowania"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. <span data-ttu-id="ac72e-151">W **Clarizen domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ac72e-151">In the **Clarizen Domain and URLs** section, perform the following steps:</span></span>

    ![Pola Adres URL identyfikatora i odpowiedzi](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    <span data-ttu-id="ac72e-153">a.</span><span class="sxs-lookup"><span data-stu-id="ac72e-153">a.</span></span> <span data-ttu-id="ac72e-154">W **identyfikator** wpisz wartość, jak: **Clarizen**</span><span class="sxs-lookup"><span data-stu-id="ac72e-154">In the **Identifier** box, type the value as: **Clarizen**</span></span>

    <span data-ttu-id="ac72e-155">b.</span><span class="sxs-lookup"><span data-stu-id="ac72e-155">b.</span></span> <span data-ttu-id="ac72e-156">W **adres URL odpowiedzi** wpisz adres URL przy użyciu następującego wzorca: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span><span class="sxs-lookup"><span data-stu-id="ac72e-156">In the **Reply URL** box, type a URL by using the following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span></span>

    > [!NOTE]
    > <span data-ttu-id="ac72e-157">Nie są to rzeczywiste wartości.</span><span class="sxs-lookup"><span data-stu-id="ac72e-157">These are not the real values.</span></span> <span data-ttu-id="ac72e-158">Należy użyć rzeczywisty identyfikator i adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ac72e-158">You have to use the actual identifier and reply URL.</span></span> <span data-ttu-id="ac72e-159">W tym miejscu zaleca się, że używasz unikatowej wartości ciągu jako identyfikator.</span><span class="sxs-lookup"><span data-stu-id="ac72e-159">Here we suggest that you use the unique value of a string as the identifier.</span></span> <span data-ttu-id="ac72e-160">Aby uzyskać rzeczywiste wartości, skontaktuj się z [zespołem pomocy technicznej Clarizen](https://success.clarizen.com/hc/en-us/requests/new).</span><span class="sxs-lookup"><span data-stu-id="ac72e-160">To get the actual values, contact the [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span></span>

4. <span data-ttu-id="ac72e-161">Na **certyfikat podpisywania SAML** kliknij **Utwórz nowy certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="ac72e-161">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Klikając przycisk "Utwórz nowy certyfikat"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. <span data-ttu-id="ac72e-163">W **Tworzenie nowego świadectwa** okno dialogowe pola, kliknij ikonę kalendarza i wybierz datę wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="ac72e-163">In the **Create New Certificate** dialog box, click the calendar icon and select an expiry date.</span></span> <span data-ttu-id="ac72e-164">Następnie kliknij przycisk **Save** (Zapisz).</span><span class="sxs-lookup"><span data-stu-id="ac72e-164">Then click **Save**.</span></span>

    ![Wybranie i zapisanie Data wygaśnięcia](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="ac72e-166">W **certyfikat podpisywania SAML** wybierz opcję **uaktywnić nowy certyfikat**, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="ac72e-166">In the **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span></span>

    ![Po zaznaczeniu pola wyboru dla uaktywnienie nowego certyfikatu](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. <span data-ttu-id="ac72e-168">W **certyfikat przerzucania** okno dialogowe, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="ac72e-168">In the **Rollover certificate** dialog box, click **OK**.</span></span>

    ![Klikając przycisk "OK", aby potwierdzić uaktywnić certyfikatu](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ac72e-170">W **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ac72e-170">In the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Klikając przycisk "Certyfikat (Base64)", aby rozpocząć pobieranie](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. <span data-ttu-id="ac72e-172">W **konfiguracji Clarizen** , kliknij przycisk **skonfigurować Clarizen** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="ac72e-172">In the **Clarizen Configuration** section, click **Configure Clarizen** to open the **Configure sign-on** window.</span></span>

    ![Klikając przycisk "Konfigurowanie Clarizen"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![Okno "Konfigurowanie logowania jednokrotnego", w tym adresy URL i pliki](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. <span data-ttu-id="ac72e-175">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy Clarizen.</span><span class="sxs-lookup"><span data-stu-id="ac72e-175">In a different web browser window, sign in to your Clarizen company site as an administrator.</span></span>

11. <span data-ttu-id="ac72e-176">Kliknij nazwy użytkownika, a następnie kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="ac72e-176">Click your username, and then click **Settings**.</span></span>

    <span data-ttu-id="ac72e-177">![Klikając pozycję "Ustawienia" w obszarze nazwy użytkownika](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="ac72e-177">![Clicking "Settings" under your username](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span></span>

12. <span data-ttu-id="ac72e-178">Kliknij przycisk **ustawienia globalne** kartę.</span><span class="sxs-lookup"><span data-stu-id="ac72e-178">Click the **Global Settings** tab.</span></span> <span data-ttu-id="ac72e-179">A następnie obok pozycji **Federated Authentication**, kliknij przycisk **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="ac72e-179">Then, next to **Federated Authentication**, click **edit**.</span></span>

    <span data-ttu-id="ac72e-180">![Kartę "Ustawienia globalne"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "ustawienia globalne")</span><span class="sxs-lookup"><span data-stu-id="ac72e-180">!["Global Settings" tab](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span></span>

13. <span data-ttu-id="ac72e-181">W **Federated Authentication** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ac72e-181">In the **Federated Authentication** dialog box, perform the following steps:</span></span>

    <span data-ttu-id="ac72e-182">![Okno dialogowe "Uwierzytelnianie federacyjne"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span><span class="sxs-lookup"><span data-stu-id="ac72e-182">!["Federated Authentication" dialog box](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span></span>

    <span data-ttu-id="ac72e-183">a.</span><span class="sxs-lookup"><span data-stu-id="ac72e-183">a.</span></span> <span data-ttu-id="ac72e-184">Wybierz **uwierzytelnianie federacyjne Włącz**.</span><span class="sxs-lookup"><span data-stu-id="ac72e-184">Select **Enable Federated Authentication**.</span></span>

    <span data-ttu-id="ac72e-185">b.</span><span class="sxs-lookup"><span data-stu-id="ac72e-185">b.</span></span> <span data-ttu-id="ac72e-186">Kliknij przycisk **przekazać** przekazać pobranego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="ac72e-186">Click **Upload** to upload your downloaded certificate.</span></span>

    <span data-ttu-id="ac72e-187">c.</span><span class="sxs-lookup"><span data-stu-id="ac72e-187">c.</span></span> <span data-ttu-id="ac72e-188">W **adres URL logowania** wprowadź wartość **SAML pojedynczy znak na adres URL usługi** w oknie Konfiguracja aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac72e-188">In the **Sign-in URL** box, enter the value of **SAML Single Sign-On Service URL** from the Azure AD application configuration window.</span></span>

    <span data-ttu-id="ac72e-189">d.</span><span class="sxs-lookup"><span data-stu-id="ac72e-189">d.</span></span> <span data-ttu-id="ac72e-190">W **Sign-out URL** wprowadź wartość **Sign-Out URL** w oknie Konfiguracja aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac72e-190">In the **Sign-out URL** box, enter the value of **Sign-Out URL** from the Azure AD application configuration window.</span></span>

    <span data-ttu-id="ac72e-191">e.</span><span class="sxs-lookup"><span data-stu-id="ac72e-191">e.</span></span> <span data-ttu-id="ac72e-192">Wybierz **Użyj POST**.</span><span class="sxs-lookup"><span data-stu-id="ac72e-192">Select **Use POST**.</span></span>

    <span data-ttu-id="ac72e-193">f.</span><span class="sxs-lookup"><span data-stu-id="ac72e-193">f.</span></span> <span data-ttu-id="ac72e-194">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ac72e-194">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ac72e-195">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac72e-195">Create an Azure AD test user</span></span>
<span data-ttu-id="ac72e-196">W portalu Azure Tworzenie użytkownika testowego o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ac72e-196">In the Azure portal, create a test user called Britta Simon.</span></span>

![Nazwa i adres e-mail użytkownika usługi Azure AD][100]

1. <span data-ttu-id="ac72e-198">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ac72e-198">In the Azure portal, in the left pane, click the **Azure Active Directory** icon.</span></span>

    ![Ikona usługi Azure Active Directory](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ac72e-200">Kliknij przycisk **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="ac72e-200">Click **Users and groups**, and then click **All users** to display the list of users.</span></span>

    ![Klikając pozycję "Użytkownicy i grupy" i "Wszyscy użytkownicy"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ac72e-202">W górnej części okna dialogowego, kliknij przycisk **Dodaj** otworzyć **użytkownika** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="ac72e-202">At the top of the dialog box, click **Add** to open the **User** dialog box.</span></span>

    ![Przycisk "Dodaj"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ac72e-204">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ac72e-204">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe "Użytkownika" z nazwę, adres e-mail i hasło wypełnione](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ac72e-206">a.</span><span class="sxs-lookup"><span data-stu-id="ac72e-206">a.</span></span> <span data-ttu-id="ac72e-207">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ac72e-207">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ac72e-208">b.</span><span class="sxs-lookup"><span data-stu-id="ac72e-208">b.</span></span> <span data-ttu-id="ac72e-209">W **nazwy użytkownika** wpisz adres e-mail konta Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ac72e-209">In the **User name** box, type the email address of the Britta Simon account.</span></span>

    <span data-ttu-id="ac72e-210">c.</span><span class="sxs-lookup"><span data-stu-id="ac72e-210">c.</span></span> <span data-ttu-id="ac72e-211">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="ac72e-211">Select **Show Password** and write down the value of **Password**.</span></span>

    <span data-ttu-id="ac72e-212">d.</span><span class="sxs-lookup"><span data-stu-id="ac72e-212">d.</span></span> <span data-ttu-id="ac72e-213">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ac72e-213">Click **Create**.</span></span>

### <a name="create-a-clarizen-test-user"></a><span data-ttu-id="ac72e-214">Tworzenie użytkownika testowego Clarizen</span><span class="sxs-lookup"><span data-stu-id="ac72e-214">Create a Clarizen test user</span></span>
<span data-ttu-id="ac72e-215">Aby umożliwić użytkownikom usługi Azure AD do logowania się na Clarizen, należy udostępnić kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ac72e-215">To enable Azure AD users to sign in to Clarizen, you must provision user accounts.</span></span> <span data-ttu-id="ac72e-216">W przypadku Clarizen Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="ac72e-216">In the case of Clarizen, provisioning is a manual task.</span></span>

1. <span data-ttu-id="ac72e-217">Zaloguj się do witryny firmy Clarizen jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ac72e-217">Sign in to your Clarizen company site as an administrator.</span></span>

2. <span data-ttu-id="ac72e-218">Kliknij przycisk **osób**.</span><span class="sxs-lookup"><span data-stu-id="ac72e-218">Click **People**.</span></span>

    <span data-ttu-id="ac72e-219">![Klikając przycisk "Osoby"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "osób")</span><span class="sxs-lookup"><span data-stu-id="ac72e-219">![Clicking "People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="ac72e-220">Kliknij przycisk **zaprosić użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="ac72e-220">Click **Invite User**.</span></span>

    <span data-ttu-id="ac72e-221">![Przycisk "Zaprosić użytkowników"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "zaprosić użytkowników")</span><span class="sxs-lookup"><span data-stu-id="ac72e-221">!["Invite User" button](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="ac72e-222">W **zaprosić użytkowników** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ac72e-222">In the **Invite People** dialog box, perform the following steps:</span></span>

    <span data-ttu-id="ac72e-223">![Okno dialogowe "Zaproś inne osoby"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "zaprosić użytkowników")</span><span class="sxs-lookup"><span data-stu-id="ac72e-223">!["Invite People" dialog box](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="ac72e-224">a.</span><span class="sxs-lookup"><span data-stu-id="ac72e-224">a.</span></span> <span data-ttu-id="ac72e-225">W **E-mail** wpisz adres e-mail konta Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ac72e-225">In the **Email** box, type the email address of the Britta Simon account.</span></span>

    <span data-ttu-id="ac72e-226">b.</span><span class="sxs-lookup"><span data-stu-id="ac72e-226">b.</span></span> <span data-ttu-id="ac72e-227">Kliknij przycisk **zaprosić**.</span><span class="sxs-lookup"><span data-stu-id="ac72e-227">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ac72e-228">Właścicielem konta usługi Azure Active Directory otrzymasz wiadomość e-mail, a następnie kliknij łącze, aby potwierdzić swoje konto, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="ac72e-228">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ac72e-229">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac72e-229">Assign the Azure AD test user</span></span>
<span data-ttu-id="ac72e-230">Włącz Simona Britta do udostępnienia jej Clarizen za pomocą usługi Azure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ac72e-230">Enable Britta Simon to use Azure single sign-on by granting her access to Clarizen.</span></span>

![Test przypisany użytkownik][200]

1. <span data-ttu-id="ac72e-232">Na platformie Azure kliknij przycisk Otwórz portalu, wyświetlać aplikacje, przejdź do widoku katalogu **aplikacje dla przedsiębiorstw**, a następnie kliknij przycisk **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ac72e-232">In the Azure portal, open the applications view, browse to the directory view, click **Enterprise applications**, and then click **All applications**.</span></span>

    ![Kliknięcie przycisku "aplikacje przedsiębiorstwa" i "Wszystkie aplikacje"][201]

2. <span data-ttu-id="ac72e-234">Na liście aplikacji zaznacz **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="ac72e-234">In the applications list, select **Clarizen**.</span></span>

    ![Wybieranie Clarizen na liście](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. <span data-ttu-id="ac72e-236">W okienku po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ac72e-236">In the left pane, click **Users and groups**.</span></span>

    ![Klikając pozycję "Użytkownicy i grupy"][202]

4. <span data-ttu-id="ac72e-238">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ac72e-238">Click the **Add** button.</span></span> <span data-ttu-id="ac72e-239">Następnie w **Dodaj przydziału** okno dialogowe, wybierz opcję **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ac72e-239">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Przycisk "Dodaj" i "Dodaj przydziału" — okno dialogowe][203]

5. <span data-ttu-id="ac72e-241">W **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="ac72e-241">In the **Users and groups** dialog box, select **Britta Simon** in the list of users.</span></span>

6. <span data-ttu-id="ac72e-242">W **użytkowników i grup** okno dialogowe, kliknij przycisk **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ac72e-242">In the **Users and groups** dialog box, click the **Select** button.</span></span>

7. <span data-ttu-id="ac72e-243">W **Dodaj przydziału** okno dialogowe, kliknij przycisk **przypisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ac72e-243">In the **Add Assignment** dialog box, click the **Assign** button.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="ac72e-244">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ac72e-244">Test single sign-on</span></span>
<span data-ttu-id="ac72e-245">Test konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ac72e-245">Test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="ac72e-246">Po kliknięciu kafelka Clarizen w panelu dostępu należy powinny być automatycznie zalogowany do aplikacji Clarizen.</span><span class="sxs-lookup"><span data-stu-id="ac72e-246">When you click the Clarizen tile in the Access Panel, you should be automatically signed in to your Clarizen application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ac72e-247">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ac72e-247">Additional resources</span></span>

* [<span data-ttu-id="ac72e-248">Lista samouczków dotyczących sposobów integracji aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ac72e-248">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ac72e-249">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ac72e-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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
