---
title: "Samouczek: Azure Active Directory integrację ze IBM Kenexa ankiety | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i IBM Kenexa ankiety przedsiębiorstwa."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 5c276c23288292a1c54dd9d57177d5072b90c9e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a><span data-ttu-id="20fac-103">Samouczek: Azure Active Directory integrację ze IBM Kenexa ankiety</span><span class="sxs-lookup"><span data-stu-id="20fac-103">Tutorial: Azure Active Directory integration with IBM Kenexa Survey Enterprise</span></span>

<span data-ttu-id="20fac-104">Z tego samouczka dowiesz integrowanie IBM Kenexa ankiety przedsiębiorstwa z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="20fac-104">In this tutorial, you learn how to integrate IBM Kenexa Survey Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="20fac-105">Integrowanie IBM Kenexa ankiety przedsiębiorstwa z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="20fac-105">Integrating IBM Kenexa Survey Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="20fac-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do IBM Kenexa ankiety przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="20fac-106">You can control in Azure AD who has access to IBM Kenexa Survey Enterprise.</span></span>
- <span data-ttu-id="20fac-107">Umożliwia użytkownikom automatycznie logować się do IBM Kenexa ankiety przedsiębiorstwa przy użyciu rejestracji jednokrotnej (SSO) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20fac-107">You can enable your users to automatically sign in to IBM Kenexa Survey Enterprise by using single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="20fac-108">Możesz zarządzać kont w jednej centralnej lokalizacji: portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="20fac-108">You can manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="20fac-109">Jeśli chcesz dowiedzieć się więcej na temat oprogramowania jako usługa (SaaS) integracji aplikacji z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="20fac-109">If you want to know more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20fac-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="20fac-110">Prerequisites</span></span>

<span data-ttu-id="20fac-111">Do konfigurowania integracji z usługą Azure AD z IBM Kenexa ankiety przedsiębiorstwa, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="20fac-111">To configure Azure AD integration with IBM Kenexa Survey Enterprise, you need the following items:</span></span>

- <span data-ttu-id="20fac-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="20fac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="20fac-113">Włączone IBM Kenexa ankiety Enterprise SSO subskrypcji</span><span class="sxs-lookup"><span data-stu-id="20fac-113">An IBM Kenexa Survey Enterprise SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="20fac-114">Podczas testowania czynności w tym samouczku, firma Microsoft zaleca, nie używaj do środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="20fac-114">When you test the steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="20fac-115">Aby przetestować kroki opisane w tym samouczku, wykonaj te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="20fac-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="20fac-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="20fac-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="20fac-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="20fac-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="20fac-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="20fac-118">Scenario description</span></span>
<span data-ttu-id="20fac-119">W tym samouczku można przetestować logowania jednokrotnego programu Azure AD w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="20fac-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="20fac-120">Scenariusz opisane w samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="20fac-120">The scenario outlined in the tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="20fac-121">Dodawanie IBM Kenexa ankiety przedsiębiorstwa z galerii</span><span class="sxs-lookup"><span data-stu-id="20fac-121">Adding IBM Kenexa Survey Enterprise from the gallery</span></span>
* <span data-ttu-id="20fac-122">Konfigurowanie i testowania logowania jednokrotnego programu Azure AD</span><span class="sxs-lookup"><span data-stu-id="20fac-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-ibm-kenexa-survey-enterprise-from-the-gallery"></a><span data-ttu-id="20fac-123">Dodaj IBM Kenexa ankiety przedsiębiorstwa z galerii</span><span class="sxs-lookup"><span data-stu-id="20fac-123">Add IBM Kenexa Survey Enterprise from the gallery</span></span>
<span data-ttu-id="20fac-124">Aby skonfigurować integrację usługi Azure AD IBM Kenexa ankiety przedsiębiorstwa, należy dodać IBM Kenexa ankiety przedsiębiorstwa z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="20fac-124">To configure the integration of IBM Kenexa Survey Enterprise into Azure AD, add IBM Kenexa Survey Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="20fac-125">Aby dodać IBM Kenexa ankiety przedsiębiorstwa z galerii, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="20fac-125">To add IBM Kenexa Survey Enterprise from the gallery, do the following:</span></span>

1. <span data-ttu-id="20fac-126">W [portalu Azure](https://portal.azure.com), w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="20fac-126">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Active Directory** button.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="20fac-128">Wybierz **aplikacje dla przedsiębiorstw**, a następnie wybierz **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="20fac-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="20fac-130">Aby dodać aplikację, kliknij przycisk **nowej aplikacji** przycisku.</span><span class="sxs-lookup"><span data-stu-id="20fac-130">To add an application, click the **New application** button.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="20fac-132">W polu wyszukiwania wpisz **IBM Kenexa ankiety Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="20fac-132">In the search box, type **IBM Kenexa Survey Enterprise**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. <span data-ttu-id="20fac-134">Na liście wyników wybierz **IBM Kenexa ankiety Enterprise**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="20fac-134">In the results list, select **IBM Kenexa Survey Enterprise**, and then click the **Add** button to add the application.</span></span>

    ![IBM Kenexa ankiety przedsiębiorstwa na liście wyników](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="20fac-136">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="20fac-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="20fac-137">W tej sekcji Konfiguracja i testowanie logowania jednokrotnego AD Azure z przedsiębiorstwem ankiety Kenexa IBM oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="20fac-137">In this section, you configure and test Azure AD SSO with IBM Kenexa Survey Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="20fac-138">Dla logowania jednokrotnego do pracy usługi Azure AD musi zidentyfikować odpowiednikiem użytkownika IBM Kenexa ankiety przedsiębiorstwa w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20fac-138">For SSO to work, Azure AD needs to identify the IBM Kenexa Survey Enterprise user counterpart in Azure AD.</span></span> <span data-ttu-id="20fac-139">Innymi słowy usługi Azure AD ustanowić relację łącza między użytkownika usługi Azure AD i powiązanych użytkowników w przedsiębiorstwie ankiety Kenexa IBM.</span><span class="sxs-lookup"><span data-stu-id="20fac-139">In other words, Azure AD must establish a link relationship between an Azure AD user and a related user in IBM Kenexa Survey Enterprise.</span></span>

<span data-ttu-id="20fac-140">Do ustanawiania relacji łącza, należy przypisać wartość **nazwy użytkownika** w przedsiębiorstwie ankiety Kenexa IBM jako wartość **Username** w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20fac-140">To establish the link relationship, assign the value of the **user name** in IBM Kenexa Survey Enterprise as the value of the **Username** in Azure AD.</span></span>

<span data-ttu-id="20fac-141">Aby skonfigurować i przetestować logowania jednokrotnego AD Azure z przedsiębiorstwem ankiety Kenexa IBM, wykonaj bloków konstrukcyjnych w dwóch następnych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="20fac-141">To configure and test Azure AD SSO with IBM Kenexa Survey Enterprise, complete the building blocks in the next two sections.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="20fac-142">Konfigurowanie usługi Azure AD logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="20fac-142">Configure Azure AD SSO</span></span>

<span data-ttu-id="20fac-143">W tej sekcji włączenia funkcji logowania jednokrotnego usługi Azure AD w portalu Azure i konfigurowanie logowania jednokrotnego w aplikacji IBM Kenexa ankiety przedsiębiorstwa w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="20fac-143">In this section, you enable Azure AD SSO in the Azure portal and configure SSO in your IBM Kenexa Survey Enterprise application by doing the following:</span></span>

1. <span data-ttu-id="20fac-144">W portalu Azure na **IBM Kenexa ankiety Enterprise** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="20fac-144">In the Azure portal, on the **IBM Kenexa Survey Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![IBM Kenexa ankiety Enterprise Konfigurowanie logowania jednokrotnego łącza][4]

2. <span data-ttu-id="20fac-146">W **logowanie jednokrotne** okna dialogowego, **tryb** wybierz opcję **na języku SAML logowania jednokrotnego** do włączenia funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="20fac-146">In the **Single sign-on** dialog box, in the **Mode** box, select **SAML-based Sign-on** to enable SSO.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. <span data-ttu-id="20fac-148">W **IBM Kenexa ankiety Enterprise domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="20fac-148">In the **IBM Kenexa Survey Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![IBM Kenexa ankiety Enterprise domeny i adres URL z jednym informacje logowania jednokrotnego](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    <span data-ttu-id="20fac-150">a.</span><span class="sxs-lookup"><span data-stu-id="20fac-150">a.</span></span> <span data-ttu-id="20fac-151">W **identyfikator** tekstowym, wpisz adres URL z następującego wzorca:`https://surveys.kenexa.com/<companycode>`</span><span class="sxs-lookup"><span data-stu-id="20fac-151">In the **Identifier** textbox, type a URL with the following pattern: `https://surveys.kenexa.com/<companycode>`</span></span>

    <span data-ttu-id="20fac-152">b.</span><span class="sxs-lookup"><span data-stu-id="20fac-152">b.</span></span> <span data-ttu-id="20fac-153">W **adres URL odpowiedzi** tekstowym, wpisz adres URL z następującego wzorca:`https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span><span class="sxs-lookup"><span data-stu-id="20fac-153">In the **Reply URL** textbox, type a URL with the following pattern: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="20fac-154">Poprzednie wartości nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="20fac-154">The preceding values are not real.</span></span> <span data-ttu-id="20fac-155">Zaktualizuj je z rzeczywistego identyfikatora i adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="20fac-155">Update them with the actual identifier and reply URL.</span></span> <span data-ttu-id="20fac-156">Aby uzyskać rzeczywiste wartości, skontaktuj się z [zespołem pomocy technicznej Enterprise ankiety Kenexa IBM](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="20fac-156">To obtain the actual values, contact the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

4. <span data-ttu-id="20fac-157">W obszarze **certyfikat podpisywania SAML**, kliknij przycisk **certyfikatu (Base64)**, a następnie zapisz plik certyfikatu na komputerze.</span><span class="sxs-lookup"><span data-stu-id="20fac-157">Under **SAML Signing Certificate**, click **Certificate (Base64)**, and then save the certificate file to your computer.</span></span>

    ![Łącze pobierania certyfikatu (Base64)](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    <span data-ttu-id="20fac-159">IBM Kenexa ankiety aplikacją oczekuje do odbierania potwierdzeń zabezpieczeń potwierdzenia Markup Language (SAML) w określonym formacie, musisz dodać mapowania atrybutów niestandardowych do konfiguracji z atrybutów tokenu SAML.</span><span class="sxs-lookup"><span data-stu-id="20fac-159">The IBM Kenexa Survey Enterprise application expects to receive the Security Assertions Markup Language (SAML) assertions in a specific format, which requires you to add custom attribute mappings to the configuration of your SAML token attributes.</span></span> <span data-ttu-id="20fac-160">Wartość oświadczenia identyfikatora użytkownika w odpowiedzi musi być zgodna z Identyfikatorem logowania jednokrotnego, który jest skonfigurowany w systemie Kenexa.</span><span class="sxs-lookup"><span data-stu-id="20fac-160">The value of the user-identifier claim in the response must match the SSO ID that's configured in the Kenexa system.</span></span> <span data-ttu-id="20fac-161">Aby mapować identyfikator odpowiedniego użytkownika w organizacji jako SSO Internet Datagram Protocol (IDP), pracy z [zespołem pomocy technicznej Enterprise ankiety Kenexa IBM](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="20fac-161">To map the appropriate user identifier in your organization as SSO Internet Datagram Protocol (IDP), work with the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> 

    <span data-ttu-id="20fac-162">Domyślnie program Azure AD Ustawia identyfikator użytkownika jako wartość głównej nazwy (UPN) użytkownika.</span><span class="sxs-lookup"><span data-stu-id="20fac-162">By default, Azure AD sets the user identifier as the user principal name (UPN) value.</span></span> <span data-ttu-id="20fac-163">Tę wartość można zmienić na **atrybutu** karcie, jak pokazano na poniższym zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="20fac-163">You can change this value on the **Attribute** tab, as shown in the following screenshot.</span></span> <span data-ttu-id="20fac-164">Integracja działa tylko po zakończeniu mapowanie poprawnie.</span><span class="sxs-lookup"><span data-stu-id="20fac-164">The integration works only after you've completed the mapping correctly.</span></span>
    
    ![Okno dialogowe atrybuty użytkownika](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png)   

5. <span data-ttu-id="20fac-166">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="20fac-166">Click **Save**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej przycisk zapisywania](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="20fac-168">Aby otworzyć **Konfigurowanie logowania jednokrotnego** okna, w obszarze **konfiguracja dla przedsiębiorstw ankiety Kenexa IBM**, kliknij przycisk **skonfigurować IBM Kenexa ankiety Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="20fac-168">To open the **Configure sign-on** window, under **IBM Kenexa Survey Enterprise Configuration**, click **Configure IBM Kenexa Survey Enterprise**.</span></span> 
 
    ![Łącze skonfigurować IBM Kenexa ankiety Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. <span data-ttu-id="20fac-170">Kopiuj **Sign-Out adres URL**, **SAML identyfikator jednostki**, i **SAML pojedynczy znak na adres URL usługi** wartości z **krótkimi opisami** sekcji.</span><span class="sxs-lookup"><span data-stu-id="20fac-170">Copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values from the **Quick Reference** section.</span></span>

8. <span data-ttu-id="20fac-171">W **Konfigurowanie logowania jednokrotnego** okna, w obszarze **krótkimi opisami**, kopiowania **Sign-Out adres URL**, **identyfikator jednostki SAML**, i **SAML pojedynczy znak na adres URL usługi** wartości.</span><span class="sxs-lookup"><span data-stu-id="20fac-171">In the **Configure sign-on** window, under **Quick Reference**, copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values.</span></span>

9. <span data-ttu-id="20fac-172">Do konfigurowania rejestracji Jednokrotnej w **IBM Kenexa ankiety Enterprise** po stronie, Wyślij pobrany **certyfikatu (Base64)**, **Sign-Out adres URL**, **SAML identyfikator jednostki**, i **SAML pojedynczy znak na adres URL usługi** wartości do [zespołem pomocy technicznej Enterprise ankiety Kenexa IBM](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="20fac-172">To configure SSO on the **IBM Kenexa Survey Enterprise** side, send the downloaded **Certificate (Base64)**, **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values to the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

> [!TIP]
> <span data-ttu-id="20fac-173">Można odwołać się do wersji krótkie instrukcje zawarte w [portalu Azure](https://portal.azure.com) podczas konfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="20fac-173">You can refer to a concise version of these instructions in the [Azure portal](https://portal.azure.com) while you are setting up the app.</span></span> <span data-ttu-id="20fac-174">Po dodaniu aplikacji z **usługi Active Directory** > **aplikacje dla przedsiębiorstw** po prostu kliknij **logowanie jednokrotne** karcie, a następnie dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji na końcu.</span><span class="sxs-lookup"><span data-stu-id="20fac-174">After you add the app from the **Active Directory** > **Enterprise Applications** section, simply click the **single sign-on** tab, and then access the embedded documentation through the **Configuration** section at the end.</span></span> <span data-ttu-id="20fac-175">Aby dowiedzieć się więcej o funkcji osadzonych dokumentacji, zobacz [usługi Azure AD osadzonych dokumentacji](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="20fac-175">To learn more about the embedded documentation feature, see [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="20fac-176">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="20fac-176">Create an Azure AD test user</span></span>
<span data-ttu-id="20fac-177">W tej sekcji możesz tworzyć użytkownika testowego Simona Britta w portalu Azure w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="20fac-177">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span></span>

![Tworzenie użytkownika testowego usługi Azure AD][100]

1. <span data-ttu-id="20fac-179">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="20fac-179">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="20fac-181">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="20fac-181">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>
    
    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="20fac-183">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="20fac-183">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>
 
    ![Przycisk Dodaj](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="20fac-185">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="20fac-185">In the **User** dialog box, perform the following steps:</span></span>
 
    ![Okno dialogowe użytkownika](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="20fac-187">a.</span><span class="sxs-lookup"><span data-stu-id="20fac-187">a.</span></span> <span data-ttu-id="20fac-188">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="20fac-188">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="20fac-189">b.</span><span class="sxs-lookup"><span data-stu-id="20fac-189">b.</span></span> <span data-ttu-id="20fac-190">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="20fac-190">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="20fac-191">c.</span><span class="sxs-lookup"><span data-stu-id="20fac-191">c.</span></span> <span data-ttu-id="20fac-192">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="20fac-192">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="20fac-193">d.</span><span class="sxs-lookup"><span data-stu-id="20fac-193">d.</span></span> <span data-ttu-id="20fac-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="20fac-194">Click **Create**.</span></span>
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a><span data-ttu-id="20fac-195">Tworzenie użytkownika testowego IBM Kenexa ankiety Enterprise</span><span class="sxs-lookup"><span data-stu-id="20fac-195">Create an IBM Kenexa Survey Enterprise test user</span></span>

<span data-ttu-id="20fac-196">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w przedsiębiorstwie ankiety Kenexa IBM.</span><span class="sxs-lookup"><span data-stu-id="20fac-196">In this section, you create a user called Britta Simon in IBM Kenexa Survey Enterprise.</span></span> 

<span data-ttu-id="20fac-197">Aby utworzyć użytkowników systemu IBM Kenexa ankiety przedsiębiorstwa i mapowanie Identyfikatora logowania jednokrotnego dla nich, można pracować z [zespołem pomocy technicznej Enterprise ankiety Kenexa IBM](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="20fac-197">To create users in the IBM Kenexa Survey Enterprise system and map the SSO ID for them, you can work with the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> <span data-ttu-id="20fac-198">Ta wartość Identyfikatora logowania jednokrotnego należy również mapować na wartość identyfikatora użytkownika z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20fac-198">This SSO ID value should also be mapped to the user identifier value from Azure AD.</span></span> <span data-ttu-id="20fac-199">To ustawienie domyślne można zmienić na **atrybutu** kartę.</span><span class="sxs-lookup"><span data-stu-id="20fac-199">You can change this default setting on the **Attribute** tab.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="20fac-200">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="20fac-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="20fac-201">W tej sekcji można włączyć użytkownika Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do IBM Kenexa ankiety przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="20fac-201">In this section, you enable user Britta Simon to use Azure SSO by granting access to IBM Kenexa Survey Enterprise.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="20fac-203">Aby przypisać użytkownika Simona Britta IBM Kenexa ankiety przedsiębiorstwa, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="20fac-203">To assign user Britta Simon to IBM Kenexa Survey Enterprise, do the following:</span></span>

1. <span data-ttu-id="20fac-204">W portalu Azure Otwórz **aplikacji** widok, przejdź do **katalogu** widok, wybierz opcję **aplikacje przedsiębiorstwa**, a następnie kliknij przycisk **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="20fac-204">In the Azure portal, open the **Applications** view, go to the **Directory** view, select **Enterprise applications**, and then click **All applications**.</span></span>

    !["Aplikacje przedsiębiorstwa" i "Wszystkie aplikacje" łącza][201] 

2. <span data-ttu-id="20fac-206">W **aplikacji** listy, wybierz **IBM Kenexa ankiety Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="20fac-206">In the **Applications** list, select **IBM Kenexa Survey Enterprise**.</span></span>

    ![Łącze IBM Kenexa ankiety przedsiębiorstwa na liście aplikacji](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. <span data-ttu-id="20fac-208">W okienku po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="20fac-208">In the left pane, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202] 

4. <span data-ttu-id="20fac-210">Kliknij przycisk **Dodaj** przycisk, a następnie w **Dodaj przydziału** okienku wybierz **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="20fac-210">Click the **Add** button and then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="20fac-212">W **użytkowników i grup** okna dialogowego, **użytkowników** listy, wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="20fac-212">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="20fac-213">W **użytkowników i grup** okno dialogowe, kliknij przycisk **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="20fac-213">In the **Users and groups** dialog box, click the **Select** button.</span></span>

7. <span data-ttu-id="20fac-214">W **Dodaj przydziału** okno dialogowe, kliknij przycisk **przypisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="20fac-214">In the **Add Assignment** dialog box, click the **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="20fac-215">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="20fac-215">Test single sign-on</span></span>

<span data-ttu-id="20fac-216">W tej sekcji możesz przetestować konfigurację programu Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="20fac-216">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span></span>

<span data-ttu-id="20fac-217">Po kliknięciu **IBM Kenexa ankiety Enterprise** kafelka w panelu dostępu należy powinien można automatycznie zalogowany do aplikacji IBM Kenexa ankiety przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="20fac-217">When you click the **IBM Kenexa Survey Enterprise** tile in the Access Panel, you should be automatically signed in to your IBM Kenexa Survey Enterprise application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="20fac-218">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="20fac-218">Additional resources</span></span>

* [<span data-ttu-id="20fac-219">Lista samouczków dotyczących sposobów integracji aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="20fac-219">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="20fac-220">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="20fac-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
