---
title: 'Samouczek: Azure Active Directory integracji z pakietem Office wirtualnej 8 x 8 | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między Azure Active Directory oraz 8 x 8 wirtualnych pakietu Office."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b34a6edf-e745-4aec-b0b2-7337473d64c5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d8dcf0171b93fec15347e810a1b525bd815dbf04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-8x8-virtual-office"></a><span data-ttu-id="7a746-103">Samouczek: Azure Active Directory integracji z pakietem Office wirtualnej 8 x 8</span><span class="sxs-lookup"><span data-stu-id="7a746-103">Tutorial: Azure Active Directory integration with 8x8 Virtual Office</span></span>

<span data-ttu-id="7a746-104">Z tego samouczka dowiesz się integrowanie 8 x 8 wirtualnych Office z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7a746-104">In this tutorial, you learn how to integrate 8x8 Virtual Office with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7a746-105">Integrowanie 8 x 8 wirtualnych Office z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="7a746-105">Integrating 8x8 Virtual Office with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7a746-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do pakietu Office wirtualnej 8 x 8</span><span class="sxs-lookup"><span data-stu-id="7a746-106">You can control in Azure AD who has access to 8x8 Virtual Office</span></span>
- <span data-ttu-id="7a746-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do 8 x 8 wirtualnych Office (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a746-107">You can enable your users to automatically get signed-on to 8x8 Virtual Office (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7a746-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="7a746-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7a746-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7a746-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a746-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7a746-110">Prerequisites</span></span>

<span data-ttu-id="7a746-111">Aby skonfigurować integrację usługi Azure AD z pakietem Office wirtualnej 8 x 8, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="7a746-111">To configure Azure AD integration with 8x8 Virtual Office, you need the following items:</span></span>

- <span data-ttu-id="7a746-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a746-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7a746-113">8 x 8 wirtualnych Office logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7a746-113">A 8x8 Virtual Office single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7a746-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="7a746-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7a746-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="7a746-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7a746-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="7a746-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7a746-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7a746-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7a746-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="7a746-118">Scenario description</span></span>
<span data-ttu-id="7a746-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="7a746-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7a746-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="7a746-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7a746-121">Dodawanie pakietu Office wirtualnej 8 x 8 z galerii</span><span class="sxs-lookup"><span data-stu-id="7a746-121">Adding 8x8 Virtual Office from the gallery</span></span>
2. <span data-ttu-id="7a746-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="7a746-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-8x8-virtual-office-from-the-gallery"></a><span data-ttu-id="7a746-123">Dodawanie pakietu Office wirtualnej 8 x 8 z galerii</span><span class="sxs-lookup"><span data-stu-id="7a746-123">Adding 8x8 Virtual Office from the gallery</span></span>
<span data-ttu-id="7a746-124">Aby skonfigurować integrację usługi Azure AD Office wirtualnej 8 x 8, należy dodać 8 x 8 wirtualnych Office z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="7a746-124">To configure the integration of 8x8 Virtual Office into Azure AD, you need to add 8x8 Virtual Office from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7a746-125">**Aby dodać 8 x 8 Office wirtualnych z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7a746-125">**To add 8x8 Virtual Office from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7a746-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="7a746-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="7a746-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="7a746-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7a746-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7a746-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="7a746-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7a746-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="7a746-133">W polu wyszukiwania wpisz **8 x 8 wirtualnych Office**.</span><span class="sxs-lookup"><span data-stu-id="7a746-133">In the search box, type **8x8 Virtual Office**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_search.png)

5. <span data-ttu-id="7a746-135">W panelu wyników wybierz **8 x 8 wirtualnych Office**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="7a746-135">In the results panel, select **8x8 Virtual Office**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7a746-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="7a746-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7a746-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z 8 x 8 Office wirtualnych opartych na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="7a746-138">In this section, you configure and test Azure AD single sign-on with 8x8 Virtual Office based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7a746-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, jakie użytkownika odpowiednika w 8 x 8 Office wirtualnego użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a746-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 8x8 Virtual Office is to a user in Azure AD.</span></span> <span data-ttu-id="7a746-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w 8 x 8 wirtualnych Office musi określone.</span><span class="sxs-lookup"><span data-stu-id="7a746-140">In other words, a link relationship between an Azure AD user and the related user in 8x8 Virtual Office needs to be established.</span></span>

<span data-ttu-id="7a746-141">W pakiecie Office wirtualnej 8 x 8, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="7a746-141">In 8x8 Virtual Office, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7a746-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z pakietem Office wirtualnej 8 x 8, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="7a746-142">To configure and test Azure AD single sign-on with 8x8 Virtual Office, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7a746-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="7a746-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7a746-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7a746-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7a746-145">**[Tworzenie użytkownika testowego wirtualnego Office 8 x 8](#creating-a-8x8-virtual-office-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta 8 x 8 wirtualnej biuro, które jest połączone z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7a746-145">**[Creating a 8x8 Virtual Office test user](#creating-a-8x8-virtual-office-test-user)** - to have a counterpart of Britta Simon in 8x8 Virtual Office that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7a746-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="7a746-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7a746-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="7a746-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7a746-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7a746-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7a746-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji pakietu Office wirtualnego 8 x 8.</span><span class="sxs-lookup"><span data-stu-id="7a746-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 8x8 Virtual Office application.</span></span>

<span data-ttu-id="7a746-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z pakietem Office wirtualnej 8 x 8, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7a746-150">**To configure Azure AD single sign-on with 8x8 Virtual Office, perform the following steps:**</span></span>

1. <span data-ttu-id="7a746-151">W portalu Azure na **8 x 8 wirtualnych Office** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="7a746-151">In the Azure portal, on the **8x8 Virtual Office** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="7a746-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="7a746-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_samlbase.png)

3. <span data-ttu-id="7a746-155">Na **8 x 8 wirtualnych Office domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7a746-155">On the **8x8 Virtual Office Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_url.png)

    <span data-ttu-id="7a746-157">a.</span><span class="sxs-lookup"><span data-stu-id="7a746-157">a.</span></span> <span data-ttu-id="7a746-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="7a746-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="7a746-159">| `https://sso.8x8.com/<companyname>` |
    | `https://www.8x8.com/<companyname>` |
    | `https://sso.8x8pilot.com/<companyname>` |</span><span class="sxs-lookup"><span data-stu-id="7a746-159">| `https://sso.8x8.com/<companyname>` |
 | `https://www.8x8.com/<companyname>` |
 | `https://sso.8x8pilot.com/<companyname>` |</span></span>

    <span data-ttu-id="7a746-160">b.</span><span class="sxs-lookup"><span data-stu-id="7a746-160">b.</span></span> <span data-ttu-id="7a746-161">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="7a746-161">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="7a746-162">| `https://<subdomain>.8x8.com/saml2` |
    | `https://<subdomain>.8x8pilot.com/saml2`|</span><span class="sxs-lookup"><span data-stu-id="7a746-162">| `https://<subdomain>.8x8.com/saml2` |
 | `https://<subdomain>.8x8pilot.com/saml2`|</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7a746-163">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="7a746-163">These values are not real.</span></span> <span data-ttu-id="7a746-164">Rzeczywisty identyfikator i adres URL odpowiedzi, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="7a746-164">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="7a746-165">Skontaktuj się z [zespołem pomocy technicznej wirtualnego Office 8 x 8](https://www.8x8.com/about-us/contact-us) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="7a746-165">Contact [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us) to get these values.</span></span>
 


4. <span data-ttu-id="7a746-166">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Raw)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="7a746-166">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_certificate.png) 

5. <span data-ttu-id="7a746-168">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7a746-168">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7a746-170">Na **konfiguracji wirtualnej 8 x 8** , kliknij przycisk **Office wirtualnego Konfiguruj 8 x 8** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="7a746-170">On the **8x8 Virtual Office Configuration** section, click **Configure 8x8 Virtual Office** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7a746-171">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="7a746-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_configure.png) 

7. <span data-ttu-id="7a746-173">Logowanie do dzierżawy 8 x 8 Office wirtualnego jako administrator.</span><span class="sxs-lookup"><span data-stu-id="7a746-173">Sign-on to your 8x8 Virtual Office tenant as an administrator.</span></span>

8. <span data-ttu-id="7a746-174">Wybierz **Mgr konta Office wirtualnego** w aplikacji panelu.</span><span class="sxs-lookup"><span data-stu-id="7a746-174">Select **Virtual Office Account Mgr** on Application Panel.</span></span>
   
    ![Konfigurowanie strony aplikacji](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_001.png)

9. <span data-ttu-id="7a746-176">Wybierz **firm** konta do zarządzania i kliknij przycisk **logowania** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7a746-176">Select **Business** account to manage and click **Sign In** button.</span></span>
   
    ![Konfigurowanie strony aplikacji](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_002.png)

10. <span data-ttu-id="7a746-178">Kliknij przycisk **kont** kartę na liście menu.</span><span class="sxs-lookup"><span data-stu-id="7a746-178">Click **Accounts** tab in the menu list.</span></span>
   
    ![Konfigurowanie strony aplikacji](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_003.png)

11. <span data-ttu-id="7a746-180">Kliknij przycisk **rejestracji jednokrotnej** na liście kont.</span><span class="sxs-lookup"><span data-stu-id="7a746-180">Click **Single Sign On** in the list of Accounts.</span></span>
   
    ![Konfigurowanie strony aplikacji](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_004.png)

12. <span data-ttu-id="7a746-182">Wybierz **rejestracji jednokrotnej** w obszarze metodę uwierzytelniania i kliknięcie **SAML**.</span><span class="sxs-lookup"><span data-stu-id="7a746-182">Select **Single Sign On** under Authentication method and click **SAML**.</span></span>
    
    ![Konfigurowanie strony aplikacji](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_005.png)

13. <span data-ttu-id="7a746-184">Kopia **adres URL logowania jednokrotnego SAML**, **pojedynczy uwagi się adres URL usługi** i **adres URL wystawcy** z usługi Azure AD do **Zaloguj się w adresie URL**, **Wyloguj adresu URL** i **adres URL wystawcy** w pakiecie Office wirtualnego 8 x 8.</span><span class="sxs-lookup"><span data-stu-id="7a746-184">Copy **SAML SSO URL**, **Single Sing Out Service URL** and **Issuer URL** from Azure AD to **Sign In URL**, **Sign Out URL** and **Issuer URL** in 8x8 Virtual Office.</span></span> 
    
    ![Konfigurowanie strony aplikacji](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_006.png)
    
14. <span data-ttu-id="7a746-186">Kliknij przycisk **przeglądarki** przycisk, aby przekazać certyfikat, który został pobrany z usługi Azure AD, a następnie kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7a746-186">Click **Browser** button to upload the certificate which you downloaded from Azure AD, and click the **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="7a746-187">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="7a746-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7a746-188">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="7a746-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7a746-189">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7a746-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7a746-190">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a746-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="7a746-191">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7a746-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="7a746-193">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7a746-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7a746-194">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="7a746-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7a746-196">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="7a746-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7a746-198">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7a746-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7a746-200">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7a746-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7a746-202">a.</span><span class="sxs-lookup"><span data-stu-id="7a746-202">a.</span></span> <span data-ttu-id="7a746-203">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7a746-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7a746-204">b.</span><span class="sxs-lookup"><span data-stu-id="7a746-204">b.</span></span> <span data-ttu-id="7a746-205">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7a746-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7a746-206">c.</span><span class="sxs-lookup"><span data-stu-id="7a746-206">c.</span></span> <span data-ttu-id="7a746-207">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="7a746-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7a746-208">d.</span><span class="sxs-lookup"><span data-stu-id="7a746-208">d.</span></span> <span data-ttu-id="7a746-209">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7a746-209">Click **Create**.</span></span>
 
### <a name="creating-a-8x8-virtual-office-test-user"></a><span data-ttu-id="7a746-210">Tworzenie użytkownika testowego wirtualnego Office 8 x 8</span><span class="sxs-lookup"><span data-stu-id="7a746-210">Creating a 8x8 Virtual Office test user</span></span>

<span data-ttu-id="7a746-211">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w pakiecie Office wirtualnej 8 x 8.</span><span class="sxs-lookup"><span data-stu-id="7a746-211">The objective of this section is to create a user called Britta Simon in 8x8 Virtual Office.</span></span> <span data-ttu-id="7a746-212">8 x 8 wirtualnych Office obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="7a746-212">8x8 Virtual Office supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="7a746-213">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="7a746-213">There is no action item for you in this section.</span></span> <span data-ttu-id="7a746-214">Nowy użytkownik został utworzony podczas próby dostępu 8 x 8 wirtualnych Office, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="7a746-214">A new user is created during an attempt to access 8x8 Virtual Office if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="7a746-215">Jeśli trzeba ręcznie utworzyć użytkownika, należy skontaktować się [zespołem pomocy technicznej wirtualnego Office 8 x 8](https://www.8x8.com/about-us/contact-us).</span><span class="sxs-lookup"><span data-stu-id="7a746-215">If you need to create a user manually, you need to contact the [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7a746-216">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a746-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7a746-217">W tej sekcji musisz włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udzielanie dostępu do pakietu Office wirtualnej 8 x 8.</span><span class="sxs-lookup"><span data-stu-id="7a746-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 8x8 Virtual Office.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="7a746-219">**Aby przypisać Simona Britta Office wirtualnej 8 x 8, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7a746-219">**To assign Britta Simon to 8x8 Virtual Office, perform the following steps:**</span></span>

1. <span data-ttu-id="7a746-220">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7a746-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="7a746-222">Na liście aplikacji zaznacz **8 x 8 wirtualnych Office**.</span><span class="sxs-lookup"><span data-stu-id="7a746-222">In the applications list, select **8x8 Virtual Office**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_app.png) 

3. <span data-ttu-id="7a746-224">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="7a746-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="7a746-226">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7a746-226">Click **Add** button.</span></span> <span data-ttu-id="7a746-227">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7a746-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="7a746-229">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="7a746-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7a746-230">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7a746-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7a746-231">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7a746-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7a746-232">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7a746-232">Testing single sign-on</span></span>

<span data-ttu-id="7a746-233">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="7a746-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7a746-234">Po kliknięciu kafelka wirtualnego Office 8 x 8 w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji pakietu Office wirtualnego 8 x 8.</span><span class="sxs-lookup"><span data-stu-id="7a746-234">When you click the 8x8 Virtual Office tile in the Access Panel, you should get automatically signed-on to your 8x8 Virtual Office application.</span></span>
<span data-ttu-id="7a746-235">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="7a746-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7a746-236">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="7a746-236">Additional resources</span></span>

* [<span data-ttu-id="7a746-237">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a746-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7a746-238">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7a746-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_203.png

