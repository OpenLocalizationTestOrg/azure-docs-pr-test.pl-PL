---
title: 'Samouczek: Integracji Azure Active Directory z LearnUpon | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i LearnUpon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: b6ac8acc244e9029be01ede5e0865c280171217d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a><span data-ttu-id="5c850-103">Samouczek: Integracji Azure Active Directory z LearnUpon</span><span class="sxs-lookup"><span data-stu-id="5c850-103">Tutorial: Azure Active Directory integration with LearnUpon</span></span>

<span data-ttu-id="5c850-104">Z tego samouczka dowiesz się integrowanie LearnUpon z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5c850-104">In this tutorial, you learn how to integrate LearnUpon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5c850-105">Integracja z usługą Azure AD LearnUpon zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5c850-105">Integrating LearnUpon with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5c850-106">Można kontrolować w usłudze Azure AD, który ma dostęp do LearnUpon</span><span class="sxs-lookup"><span data-stu-id="5c850-106">You can control in Azure AD who has access to LearnUpon</span></span>
- <span data-ttu-id="5c850-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do LearnUpon (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c850-107">You can enable your users to automatically get signed-on to LearnUpon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5c850-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5c850-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5c850-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5c850-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c850-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5c850-110">Prerequisites</span></span>

<span data-ttu-id="5c850-111">Aby skonfigurować integrację usługi Azure AD z LearnUpon, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5c850-111">To configure Azure AD integration with LearnUpon, you need the following items:</span></span>

- <span data-ttu-id="5c850-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c850-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5c850-113">LearnUpon logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5c850-113">A LearnUpon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5c850-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5c850-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5c850-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5c850-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5c850-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5c850-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5c850-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c850-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5c850-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5c850-118">Scenario description</span></span>
<span data-ttu-id="5c850-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5c850-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5c850-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5c850-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5c850-121">Dodawanie LearnUpon z galerii</span><span class="sxs-lookup"><span data-stu-id="5c850-121">Adding LearnUpon from the gallery</span></span>
2. <span data-ttu-id="5c850-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5c850-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learnupon-from-the-gallery"></a><span data-ttu-id="5c850-123">Dodawanie LearnUpon z galerii</span><span class="sxs-lookup"><span data-stu-id="5c850-123">Adding LearnUpon from the gallery</span></span>
<span data-ttu-id="5c850-124">Aby skonfigurować integrację usługi Azure AD LearnUpon, należy dodać LearnUpon z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5c850-124">To configure the integration of LearnUpon into Azure AD, you need to add LearnUpon from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5c850-125">**Aby dodać LearnUpon z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5c850-125">**To add LearnUpon from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5c850-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5c850-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="5c850-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5c850-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5c850-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5c850-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="5c850-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5c850-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="5c850-133">W polu wyszukiwania wpisz **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="5c850-133">In the search box, type **LearnUpon**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. <span data-ttu-id="5c850-135">W panelu wyników wybierz **LearnUpon**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="5c850-135">In the results panel, select **LearnUpon**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5c850-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5c850-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5c850-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z LearnUpon w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="5c850-138">In this section, you configure and test Azure AD single sign-on with LearnUpon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5c850-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w LearnUpon jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c850-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LearnUpon is to a user in Azure AD.</span></span> <span data-ttu-id="5c850-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w LearnUpon musi się.</span><span class="sxs-lookup"><span data-stu-id="5c850-140">In other words, a link relationship between an Azure AD user and the related user in LearnUpon needs to be established.</span></span>

<span data-ttu-id="5c850-141">W LearnUpon, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="5c850-141">In LearnUpon, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5c850-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z LearnUpon, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="5c850-142">To configure and test Azure AD single sign-on with LearnUpon, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5c850-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5c850-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5c850-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5c850-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5c850-145">**[Tworzenie użytkownika testowego LearnUpon](#creating-a-learnupon-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta LearnUpon połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5c850-145">**[Creating a LearnUpon test user](#creating-a-learnupon-test-user)** - to have a counterpart of Britta Simon in LearnUpon that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5c850-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5c850-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5c850-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="5c850-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5c850-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5c850-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5c850-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="5c850-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LearnUpon application.</span></span>

<span data-ttu-id="5c850-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z LearnUpon, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5c850-150">**To configure Azure AD single sign-on with LearnUpon, perform the following steps:**</span></span>

1. <span data-ttu-id="5c850-151">W portalu Azure na **LearnUpon** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="5c850-151">In the Azure portal, on the **LearnUpon** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="5c850-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="5c850-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. <span data-ttu-id="5c850-155">Na **LearnUpon domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5c850-155">On the **LearnUpon Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    <span data-ttu-id="5c850-157">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.learnupon.com/saml/consumer`</span><span class="sxs-lookup"><span data-stu-id="5c850-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.learnupon.com/saml/consumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5c850-158">Należy pamiętać, że nie jest rzeczywistą wartość.</span><span class="sxs-lookup"><span data-stu-id="5c850-158">Please note that this is not the real value.</span></span> <span data-ttu-id="5c850-159">należy zaktualizować tę wartość do rzeczywistego adresu URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="5c850-159">you have to update this value with the actual Reply URL.</span></span> <span data-ttu-id="5c850-160">Aby uzyskać tę wartość, skontaktuj się z [zespołem pomocy technicznej LearnUpon](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="5c850-160">To get this value Contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span>



4. <span data-ttu-id="5c850-161">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Raw)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5c850-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. <span data-ttu-id="5c850-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5c850-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5c850-165">Na **konfiguracji LearnUpon** , kliknij przycisk **skonfigurować LearnUpon** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="5c850-165">On the **LearnUpon Configuration** section, click **Configure LearnUpon** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5c850-166">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="5c850-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. <span data-ttu-id="5c850-168">Otwórz innego wystąpienia przeglądarki i zaloguj do LearnUpon przy użyciu konta administratora.</span><span class="sxs-lookup"><span data-stu-id="5c850-168">Open another browser instance and login into LearnUpon with an administrator account.</span></span> 

8. <span data-ttu-id="5c850-169">Kliknij przycisk **ustawienia** kartę.</span><span class="sxs-lookup"><span data-stu-id="5c850-169">Click the **settings** tab.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. <span data-ttu-id="5c850-171">Kliknij przycisk **rejestracji jednokrotnej - SAML**, a następnie kliknij przycisk **ustawienia ogólne** do konfigurowania ustawień SAML.</span><span class="sxs-lookup"><span data-stu-id="5c850-171">Click **Single Sign On - SAML**, and then click **General Settings** to configure SAML settings.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. <span data-ttu-id="5c850-173">W **ustawienia ogólne** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5c850-173">In the **General Settings** section, perform the following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    <span data-ttu-id="5c850-175">a.</span><span class="sxs-lookup"><span data-stu-id="5c850-175">a.</span></span> <span data-ttu-id="5c850-176">Wybierz **włączone**.</span><span class="sxs-lookup"><span data-stu-id="5c850-176">Select **Enabled**.</span></span>

    <span data-ttu-id="5c850-177">b.</span><span class="sxs-lookup"><span data-stu-id="5c850-177">b.</span></span> <span data-ttu-id="5c850-178">Wybierz **wersji** jako **2.0**.</span><span class="sxs-lookup"><span data-stu-id="5c850-178">Select **Version** as **2.0**.</span></span>

    <span data-ttu-id="5c850-179">c.</span><span class="sxs-lookup"><span data-stu-id="5c850-179">c.</span></span> <span data-ttu-id="5c850-180">Wybierz **pominąć warunki** jako **nr**.</span><span class="sxs-lookup"><span data-stu-id="5c850-180">Select **Skip conditions** as **No**.</span></span>

    <span data-ttu-id="5c850-181">d.</span><span class="sxs-lookup"><span data-stu-id="5c850-181">d.</span></span> <span data-ttu-id="5c850-182">W **Post tokenu SAML nazwę param** pole tekstowe, typ nazwę parametru post żądania na adres URL konsumenta SAML wymienionych powyżej, który zawiera potwierdzenia języka SAML ma zostać zweryfikowane i uwierzytelniony — na przykład **SAMLResponse**.</span><span class="sxs-lookup"><span data-stu-id="5c850-182">In the **SAML Token Post param name** textbox, type the name of request post parameter to the SAML consumer URL indicated above that contains the SAML Assertion to be verified and authenticated - for example **SAMLResponse**.</span></span>

    <span data-ttu-id="5c850-183">e.</span><span class="sxs-lookup"><span data-stu-id="5c850-183">e.</span></span> <span data-ttu-id="5c850-184">W **Format identyfikatora nazwy** tekstowym, wpisz wartość, która wskazuje, gdzie w Twojej potwierdzenia języka SAML identyfikator użytkowników (adres E-mail) znajduje się — na przykład **urn: oasis: nazwy: tc: SAML:1.1:nameid-format: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="5c850-184">In the **Name Identifier Format** textbox, type the value that indicates where in your SAML Assertion the users identifier (Email address) resides - for example **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>
  
    <span data-ttu-id="5c850-185">f.</span><span class="sxs-lookup"><span data-stu-id="5c850-185">f.</span></span> <span data-ttu-id="5c850-186">W **zidentyfikować lokalizacji dostawcy** tekstowym, wpisz wartość, która wskazuje, gdzie użytkownicy są wysyłane do po kliknięciu Twojej ikonę przekazanego z ekranu logowania do portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5c850-186">In the **Identify Provider Location** textbox, type the value that indicates where the users are sent to if they click on your uploaded icon from your Azure portal login screen.</span></span>
  
    <span data-ttu-id="5c850-187">g.</span><span class="sxs-lookup"><span data-stu-id="5c850-187">g.</span></span> <span data-ttu-id="5c850-188">W **Wyloguj adresu URL** pole tekstowe, Wklej **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5c850-188">In the **Sign out URL** textbox, paste the **Sign-Out URL** which you have copied from the Azure portal.</span></span>
    
    <span data-ttu-id="5c850-189">h.</span><span class="sxs-lookup"><span data-stu-id="5c850-189">h.</span></span> <span data-ttu-id="5c850-190">Kliknij przycisk **Zarządzanie odbitek palca**, a następnie przekaż odcisk palca certyfikatu pobrane.</span><span class="sxs-lookup"><span data-stu-id="5c850-190">Click **Manage finger prints**, and then upload the finger print of your downloaded certificate.</span></span>

11. <span data-ttu-id="5c850-191">Kliknij przycisk **ustawienia użytkownika**, a następnie wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5c850-191">Click **User Settings**, and then perform the following steps:</span></span>
   
     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    <span data-ttu-id="5c850-193">a.</span><span class="sxs-lookup"><span data-stu-id="5c850-193">a.</span></span> <span data-ttu-id="5c850-194">W **Format identyfikatora imię** tekstowym, wpisz wartość, która informuje NAS w Twoje imię użytkowników potwierdzenia języka SAML znajduje się — na przykład: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="5c850-194">In the **First Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users firstname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
  
    <span data-ttu-id="5c850-195">b.</span><span class="sxs-lookup"><span data-stu-id="5c850-195">b.</span></span> <span data-ttu-id="5c850-196">W **ostatniego Format identyfikatora nazwy** tekstowym, wpisz wartość, która informuje NAS w Twojej potwierdzenia języka SAML nazwisko użytkowników znajduje się — na przykład: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="5c850-196">In the **Last Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users lastname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

> [!TIP]
> <span data-ttu-id="5c850-197">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="5c850-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5c850-198">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="5c850-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5c850-199">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5c850-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5c850-200">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c850-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="5c850-201">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5c850-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="5c850-203">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5c850-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5c850-204">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5c850-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5c850-206">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="5c850-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5c850-208">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5c850-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5c850-210">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5c850-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5c850-212">a.</span><span class="sxs-lookup"><span data-stu-id="5c850-212">a.</span></span> <span data-ttu-id="5c850-213">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5c850-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5c850-214">b.</span><span class="sxs-lookup"><span data-stu-id="5c850-214">b.</span></span> <span data-ttu-id="5c850-215">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5c850-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5c850-216">c.</span><span class="sxs-lookup"><span data-stu-id="5c850-216">c.</span></span> <span data-ttu-id="5c850-217">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="5c850-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5c850-218">d.</span><span class="sxs-lookup"><span data-stu-id="5c850-218">d.</span></span> <span data-ttu-id="5c850-219">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5c850-219">Click **Create**.</span></span>
 
### <a name="creating-a-learnupon-test-user"></a><span data-ttu-id="5c850-220">Tworzenie użytkownika testowego LearnUpon</span><span class="sxs-lookup"><span data-stu-id="5c850-220">Creating a LearnUpon test user</span></span>

<span data-ttu-id="5c850-221">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="5c850-221">The objective of this section is to create a user called Britta Simon in LearnUpon.</span></span> <span data-ttu-id="5c850-222">LearnUpon obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="5c850-222">LearnUpon supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="5c850-223">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="5c850-223">There is no action item for you in this section.</span></span> <span data-ttu-id="5c850-224">Nowy użytkownik zostanie utworzony podczas próby dostępu LearnUpon, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="5c850-224">A new user will be created during an attempt to access LearnUpon if it doesn't exist yet.</span></span> <span data-ttu-id="5c850-225">[Konfigurowanie usługi Azure AD jednokrotnej](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="5c850-225">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="5c850-226">Jeśli trzeba ręcznie utworzyć użytkownika, należy skontaktować się [zespołem pomocy technicznej LearnUpon](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="5c850-226">If you need to create an user manually, you need to contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5c850-227">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c850-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5c850-228">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="5c850-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LearnUpon.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="5c850-230">**Aby przypisać Simona Britta LearnUpon, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5c850-230">**To assign Britta Simon to LearnUpon, perform the following steps:**</span></span>

1. <span data-ttu-id="5c850-231">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5c850-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5c850-233">Na liście aplikacji zaznacz **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="5c850-233">In the applications list, select **LearnUpon**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. <span data-ttu-id="5c850-235">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5c850-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="5c850-237">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5c850-237">Click **Add** button.</span></span> <span data-ttu-id="5c850-238">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5c850-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="5c850-240">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="5c850-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5c850-241">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5c850-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5c850-242">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5c850-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5c850-243">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5c850-243">Testing single sign-on</span></span>

<span data-ttu-id="5c850-244">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5c850-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5c850-245">Po kliknięciu kafelka LearnUpon w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="5c850-245">When you click the LearnUpon tile in the Access Panel, you should get automatically signed-on to your LearnUpon application.</span></span>
<span data-ttu-id="5c850-246">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5c850-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5c850-247">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5c850-247">Additional resources</span></span>

* [<span data-ttu-id="5c850-248">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c850-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5c850-249">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5c850-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png

