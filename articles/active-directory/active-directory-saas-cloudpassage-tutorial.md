---
title: 'Samouczek: Integracji Azure Active Directory z CloudPassage | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i CloudPassage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfe1f14e-74e4-4680-ac9e-f7355e1c94cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 094740e20570665e975dec1a591989e411f90c16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloudpassage"></a><span data-ttu-id="a1d65-103">Samouczek: Integracji Azure Active Directory z CloudPassage</span><span class="sxs-lookup"><span data-stu-id="a1d65-103">Tutorial: Azure Active Directory integration with CloudPassage</span></span>

<span data-ttu-id="a1d65-104">Z tego samouczka dowiesz się integrowanie CloudPassage z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a1d65-104">In this tutorial, you learn how to integrate CloudPassage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a1d65-105">Integracja z usługą Azure AD CloudPassage zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="a1d65-105">Integrating CloudPassage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a1d65-106">Można kontrolować w usłudze Azure AD, który ma dostęp do CloudPassage</span><span class="sxs-lookup"><span data-stu-id="a1d65-106">You can control in Azure AD who has access to CloudPassage</span></span>
- <span data-ttu-id="a1d65-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do CloudPassage (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a1d65-107">You can enable your users to automatically get signed-on to CloudPassage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a1d65-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a1d65-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a1d65-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a1d65-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1d65-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a1d65-110">Prerequisites</span></span>

<span data-ttu-id="a1d65-111">Aby skonfigurować integrację usługi Azure AD z CloudPassage, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a1d65-111">To configure Azure AD integration with CloudPassage, you need the following items:</span></span>

- <span data-ttu-id="a1d65-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a1d65-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a1d65-113">CloudPassage logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a1d65-113">A CloudPassage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a1d65-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="a1d65-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a1d65-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="a1d65-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a1d65-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="a1d65-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a1d65-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a1d65-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a1d65-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="a1d65-118">Scenario description</span></span>
<span data-ttu-id="a1d65-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="a1d65-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a1d65-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="a1d65-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a1d65-121">Dodawanie CloudPassage z galerii</span><span class="sxs-lookup"><span data-stu-id="a1d65-121">Adding CloudPassage from the gallery</span></span>
2. <span data-ttu-id="a1d65-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a1d65-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloudpassage-from-the-gallery"></a><span data-ttu-id="a1d65-123">Dodawanie CloudPassage z galerii</span><span class="sxs-lookup"><span data-stu-id="a1d65-123">Adding CloudPassage from the gallery</span></span>
<span data-ttu-id="a1d65-124">Aby skonfigurować integrację usługi Azure AD CloudPassage, należy dodać CloudPassage z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="a1d65-124">To configure the integration of CloudPassage into Azure AD, you need to add CloudPassage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a1d65-125">**Aby dodać CloudPassage z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a1d65-125">**To add CloudPassage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a1d65-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a1d65-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="a1d65-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="a1d65-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a1d65-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a1d65-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="a1d65-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a1d65-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="a1d65-133">W polu wyszukiwania wpisz **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="a1d65-133">In the search box, type **CloudPassage**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_search.png)

5. <span data-ttu-id="a1d65-135">W panelu wyników wybierz **CloudPassage**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="a1d65-135">In the results panel, select **CloudPassage**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a1d65-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a1d65-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a1d65-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z CloudPassage na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="a1d65-138">In this section, you configure and test Azure AD single sign-on with CloudPassage based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a1d65-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w CloudPassage jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1d65-139">For single sign-on to work, Azure AD needs to know what the counterpart user in CloudPassage is to a user in Azure AD.</span></span> <span data-ttu-id="a1d65-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w CloudPassage musi się.</span><span class="sxs-lookup"><span data-stu-id="a1d65-140">In other words, a link relationship between an Azure AD user and the related user in CloudPassage needs to be established.</span></span>

<span data-ttu-id="a1d65-141">W CloudPassage, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="a1d65-141">In CloudPassage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a1d65-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z CloudPassage, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="a1d65-142">To configure and test Azure AD single sign-on with CloudPassage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a1d65-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="a1d65-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a1d65-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a1d65-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a1d65-145">**[Tworzenie użytkownika testowego CloudPassage](#creating-a-cloudpassage-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta CloudPassage połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a1d65-145">**[Creating a CloudPassage test user](#creating-a-cloudpassage-test-user)** - to have a counterpart of Britta Simon in CloudPassage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a1d65-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a1d65-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a1d65-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="a1d65-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a1d65-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a1d65-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a1d65-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="a1d65-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CloudPassage application.</span></span>

<span data-ttu-id="a1d65-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z CloudPassage, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a1d65-150">**To configure Azure AD single sign-on with CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="a1d65-151">W portalu Azure na **CloudPassage** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="a1d65-151">In the Azure portal, on the **CloudPassage** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="a1d65-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="a1d65-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_samlbase.png)

3. <span data-ttu-id="a1d65-155">Na **CloudPassage domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a1d65-155">On the **CloudPassage Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_url.png)

    <span data-ttu-id="a1d65-157">a.</span><span class="sxs-lookup"><span data-stu-id="a1d65-157">a.</span></span> <span data-ttu-id="a1d65-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://portal.cloudpassage.com/saml/init/accountid`</span><span class="sxs-lookup"><span data-stu-id="a1d65-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://portal.cloudpassage.com/saml/init/accountid`</span></span>

    <span data-ttu-id="a1d65-159">b.</span><span class="sxs-lookup"><span data-stu-id="a1d65-159">b.</span></span> <span data-ttu-id="a1d65-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca: `https://portal.cloudpassage.com/saml/consume/accountid`.</span><span class="sxs-lookup"><span data-stu-id="a1d65-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://portal.cloudpassage.com/saml/consume/accountid`.</span></span> <span data-ttu-id="a1d65-161">Możesz też uzyskać wartość tego atrybutu, klikając **dokumentacji ustawienia logowania jednokrotnego** w **ustawień rejestracji jednokrotnej** sekcji portalem CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="a1d65-161">You can get your value for this attribute by clicking **SSO Setup documentation** in the **Single Sign-on Settings** section of your CloudPassage portal.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_05.png)
     
    > [!NOTE] 
    > <span data-ttu-id="a1d65-163">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="a1d65-163">These values are not real.</span></span> <span data-ttu-id="a1d65-164">Rzeczywisty adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="a1d65-164">Update these values with the actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="a1d65-165">Skontaktuj się z [zespołem pomocy technicznej klienta CloudPassage](https://www.cloudpassage.com/company/contact/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="a1d65-165">Contact [CloudPassage Client support team](https://www.cloudpassage.com/company/contact/) to get these values.</span></span> 

4. <span data-ttu-id="a1d65-166">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="a1d65-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_certificate.png) 

5. <span data-ttu-id="a1d65-168">Aplikacja CloudPassage oczekuje potwierdzenia języka SAML w określonym formacie, musisz dodać mapowania atrybutu niestandardowego do konfiguracji atrybuty tokenu SAML.</span><span class="sxs-lookup"><span data-stu-id="a1d65-168">Your CloudPassage application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="a1d65-169">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="a1d65-169">The following screenshot shows an example for this.</span></span>
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_25.png) 

6. <span data-ttu-id="a1d65-171">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano na ilustracji powyżej i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a1d65-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>

    | <span data-ttu-id="a1d65-172">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="a1d65-172">Attribute Name</span></span> | <span data-ttu-id="a1d65-173">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="a1d65-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="a1d65-174">Imię</span><span class="sxs-lookup"><span data-stu-id="a1d65-174">firstname</span></span> |<span data-ttu-id="a1d65-175">User.givenName</span><span class="sxs-lookup"><span data-stu-id="a1d65-175">user.givenname</span></span> |
    | <span data-ttu-id="a1d65-176">nazwisko</span><span class="sxs-lookup"><span data-stu-id="a1d65-176">lastname</span></span> |<span data-ttu-id="a1d65-177">User.surname</span><span class="sxs-lookup"><span data-stu-id="a1d65-177">user.surname</span></span> |
    | <span data-ttu-id="a1d65-178">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="a1d65-178">email</span></span> |<span data-ttu-id="a1d65-179">User.mail</span><span class="sxs-lookup"><span data-stu-id="a1d65-179">user.mail</span></span> |
    
    <span data-ttu-id="a1d65-180">a.</span><span class="sxs-lookup"><span data-stu-id="a1d65-180">a.</span></span> <span data-ttu-id="a1d65-181">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a1d65-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_04.png)
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="a1d65-184">b.</span><span class="sxs-lookup"><span data-stu-id="a1d65-184">b.</span></span> <span data-ttu-id="a1d65-185">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="a1d65-185">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="a1d65-186">c.</span><span class="sxs-lookup"><span data-stu-id="a1d65-186">c.</span></span> <span data-ttu-id="a1d65-187">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="a1d65-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="a1d65-188">d.</span><span class="sxs-lookup"><span data-stu-id="a1d65-188">d.</span></span> <span data-ttu-id="a1d65-189">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a1d65-189">Click **Ok**.</span></span>

7. <span data-ttu-id="a1d65-190">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a1d65-190">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="a1d65-192">Na **konfiguracji CloudPassage** , kliknij przycisk **skonfigurować CloudPassage** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="a1d65-192">On the **CloudPassage Configuration** section, click **Configure CloudPassage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a1d65-193">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="a1d65-193">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_configure.png) 

9. <span data-ttu-id="a1d65-195">W oknie innej przeglądarki logowania do witryny firmy CloudPassage jako administrator.</span><span class="sxs-lookup"><span data-stu-id="a1d65-195">In a different browser window, sign-on to your CloudPassage company site as administrator.</span></span>

10. <span data-ttu-id="a1d65-196">W menu u góry kliknij **ustawienia**, a następnie kliknij przycisk **administrowania lokacją**.</span><span class="sxs-lookup"><span data-stu-id="a1d65-196">In the menu on the top, click **Settings**, and then click **Site Administration**.</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej][12]

11. <span data-ttu-id="a1d65-198">Kliknij przycisk **ustawienia uwierzytelniania** kartę.</span><span class="sxs-lookup"><span data-stu-id="a1d65-198">Click the **Authentication Settings** tab.</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej][13]

12. <span data-ttu-id="a1d65-200">W **ustawień rejestracji jednokrotnej** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a1d65-200">In the **Single Sign-on Settings** section, perform the following steps:</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej][14]

    <span data-ttu-id="a1d65-202">a.</span><span class="sxs-lookup"><span data-stu-id="a1d65-202">a.</span></span> <span data-ttu-id="a1d65-203">Wybierz **sign-on(SSO) włączyć pojedynczego (dokumentacja Instalatora logowania jednokrotnego)** wyboru.</span><span class="sxs-lookup"><span data-stu-id="a1d65-203">Select **Enable Single sign-on(SSO)(SSO Setup Documentation)** checkbox.</span></span>
    
    <span data-ttu-id="a1d65-204">b.</span><span class="sxs-lookup"><span data-stu-id="a1d65-204">b.</span></span> <span data-ttu-id="a1d65-205">Wklej **identyfikator jednostki SAML** do **adres URL wystawcy SAML** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a1d65-205">Paste **SAML Entity ID** into the **SAML issuer URL** textbox.</span></span>
  
    <span data-ttu-id="a1d65-206">c.</span><span class="sxs-lookup"><span data-stu-id="a1d65-206">c.</span></span> <span data-ttu-id="a1d65-207">Wklej **SAML pojedynczy znak na adres URL usługi** do **adres URL punktu końcowego SAML** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a1d65-207">Paste **SAML Single Sign-On Service URL** into the **SAML endpoint URL** textbox.</span></span>
  
    <span data-ttu-id="a1d65-208">d.</span><span class="sxs-lookup"><span data-stu-id="a1d65-208">d.</span></span> <span data-ttu-id="a1d65-209">Wklej **Sign-Out URL** do **strony docelowej wylogowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a1d65-209">Paste **Sign-Out URL** into the **Logout landing page** textbox.</span></span>
  
    <span data-ttu-id="a1d65-210">e.</span><span class="sxs-lookup"><span data-stu-id="a1d65-210">e.</span></span> <span data-ttu-id="a1d65-211">Otwórz w Notatniku pobranego certyfikatu, skopiuj zawartość pobranego certyfikatu do Schowka, a następnie wklej go do **x 509 certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a1d65-211">Open your downloaded certificate in notepad, copy the content of downloaded certificate into your clipboard, and then paste it into the **x 509 certificate** textbox.</span></span>
  
    <span data-ttu-id="a1d65-212">f.</span><span class="sxs-lookup"><span data-stu-id="a1d65-212">f.</span></span> <span data-ttu-id="a1d65-213">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a1d65-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a1d65-214">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="a1d65-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a1d65-215">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="a1d65-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a1d65-216">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a1d65-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a1d65-217">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a1d65-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="a1d65-218">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a1d65-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="a1d65-220">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a1d65-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a1d65-221">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a1d65-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a1d65-223">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="a1d65-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a1d65-225">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a1d65-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a1d65-227">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a1d65-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a1d65-229">a.</span><span class="sxs-lookup"><span data-stu-id="a1d65-229">a.</span></span> <span data-ttu-id="a1d65-230">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a1d65-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a1d65-231">b.</span><span class="sxs-lookup"><span data-stu-id="a1d65-231">b.</span></span> <span data-ttu-id="a1d65-232">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a1d65-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a1d65-233">c.</span><span class="sxs-lookup"><span data-stu-id="a1d65-233">c.</span></span> <span data-ttu-id="a1d65-234">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="a1d65-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a1d65-235">d.</span><span class="sxs-lookup"><span data-stu-id="a1d65-235">d.</span></span> <span data-ttu-id="a1d65-236">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a1d65-236">Click **Create**.</span></span>
 
### <a name="creating-a-cloudpassage-test-user"></a><span data-ttu-id="a1d65-237">Tworzenie użytkownika testowego CloudPassage</span><span class="sxs-lookup"><span data-stu-id="a1d65-237">Creating a CloudPassage test user</span></span>

<span data-ttu-id="a1d65-238">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="a1d65-238">The objective of this section is to create a user called Britta Simon in CloudPassage.</span></span>

<span data-ttu-id="a1d65-239">**Aby utworzyć użytkownika o nazwie Simona Britta w CloudPassage, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a1d65-239">**To create a user called Britta Simon in CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="a1d65-240">Logowanie do Twojej **CloudPassage** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="a1d65-240">Sign-on to your **CloudPassage** company site as an administrator.</span></span> 

2. <span data-ttu-id="a1d65-241">Na pasku narzędzi u góry kliknij **ustawienia**, a następnie kliknij przycisk **administrowania lokacją**.</span><span class="sxs-lookup"><span data-stu-id="a1d65-241">In the toolbar on the top, click **Settings**, and then click **Site Administration**.</span></span> 
   
   ![Tworzenie użytkownika testowego CloudPassage][22] 

3. <span data-ttu-id="a1d65-243">Kliknij przycisk **użytkowników** , a następnie kliknij pozycję **Dodaj nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="a1d65-243">Click the **Users** tab, and then click **Add New User**.</span></span> 
   
   ![Tworzenie użytkownika testowego CloudPassage][23]

4. <span data-ttu-id="a1d65-245">W **Dodaj nowego użytkownika** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a1d65-245">In the **Add New User** section, perform the following steps:</span></span> 
   
   ![Tworzenie użytkownika testowego CloudPassage][24]
    
    <span data-ttu-id="a1d65-247">a.</span><span class="sxs-lookup"><span data-stu-id="a1d65-247">a.</span></span> <span data-ttu-id="a1d65-248">W **imię** tekstowym, wpisz Britta.</span><span class="sxs-lookup"><span data-stu-id="a1d65-248">In the **First Name** textbox, type Britta.</span></span> 
  
    <span data-ttu-id="a1d65-249">b.</span><span class="sxs-lookup"><span data-stu-id="a1d65-249">b.</span></span> <span data-ttu-id="a1d65-250">W **nazwisko** tekstowym, wpisz Simona.</span><span class="sxs-lookup"><span data-stu-id="a1d65-250">In the **Last Name** textbox, type Simon.</span></span>
  
    <span data-ttu-id="a1d65-251">c.</span><span class="sxs-lookup"><span data-stu-id="a1d65-251">c.</span></span> <span data-ttu-id="a1d65-252">W **Username** pole tekstowe, **E-mail** pole tekstowe i **ponownie poczty E-mail** pole tekstowe, wpisz nazwę użytkownika w Britta w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1d65-252">In the **Username** textbox, the **Email** textbox and the **Retype Email** textbox, type Britta's user name in Azure AD.</span></span>
  
    <span data-ttu-id="a1d65-253">d.</span><span class="sxs-lookup"><span data-stu-id="a1d65-253">d.</span></span> <span data-ttu-id="a1d65-254">Jako **typu dostępu**, wybierz pozycję **Włącz dostęp do portalu Halo**.</span><span class="sxs-lookup"><span data-stu-id="a1d65-254">As **Access Type**, select **Enable Halo Portal Access**.</span></span>
  
    <span data-ttu-id="a1d65-255">e.</span><span class="sxs-lookup"><span data-stu-id="a1d65-255">e.</span></span> <span data-ttu-id="a1d65-256">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a1d65-256">Click **Add**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a1d65-257">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a1d65-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a1d65-258">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="a1d65-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CloudPassage.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="a1d65-260">**Aby przypisać Simona Britta CloudPassage, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a1d65-260">**To assign Britta Simon to CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="a1d65-261">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a1d65-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="a1d65-263">Na liście aplikacji zaznacz **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="a1d65-263">In the applications list, select **CloudPassage**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_app.png) 

3. <span data-ttu-id="a1d65-265">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="a1d65-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="a1d65-267">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a1d65-267">Click **Add** button.</span></span> <span data-ttu-id="a1d65-268">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a1d65-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="a1d65-270">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="a1d65-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a1d65-271">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a1d65-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a1d65-272">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a1d65-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a1d65-273">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a1d65-273">Testing single sign-on</span></span>

<span data-ttu-id="a1d65-274">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a1d65-274">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="a1d65-275">Po kliknięciu kafelka CloudPassage w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="a1d65-275">When you click the CloudPassage tile in the Access Panel, you should get automatically signed-on to your CloudPassage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a1d65-276">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="a1d65-276">Additional resources</span></span>

* [<span data-ttu-id="a1d65-277">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a1d65-277">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a1d65-278">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a1d65-278">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_07.png
[13]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_08.png
[14]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_09.png
[15]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_10.png
[22]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_15.png
[23]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_16.png
[24]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_17.png

[100]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_203.png

