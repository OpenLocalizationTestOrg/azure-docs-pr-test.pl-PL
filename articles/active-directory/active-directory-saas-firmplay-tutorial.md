---
title: 'Samouczek: Integracji Azure Active Directory z FirmPlay - propagowanie pracownika dla Rekrutacja | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i FirmPlay - propagowanie pracownika dla Rekrutacja."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: 3cddd5b9508159089bf344dbb3882d462799747c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a><span data-ttu-id="215f6-103">Samouczek: Integracji Azure Active Directory z FirmPlay - propagowanie pracownika dla Rekrutacja</span><span class="sxs-lookup"><span data-stu-id="215f6-103">Tutorial: Azure Active Directory integration with FirmPlay - Employee Advocacy for Recruiting</span></span>

<span data-ttu-id="215f6-104">Z tego samouczka dowiesz się integrowanie FirmPlay - propagowanie pracownika dla Rekrutacja w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="215f6-104">In this tutorial, you learn how to integrate FirmPlay - Employee Advocacy for Recruiting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="215f6-105">Integrowanie FirmPlay - propagowanie pracownika dla Rekrutacja z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="215f6-105">Integrating FirmPlay - Employee Advocacy for Recruiting with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="215f6-106">Można kontrolować w usłudze Azure AD, który ma dostęp do FirmPlay - propagowanie pracownika dla Rekrutacja</span><span class="sxs-lookup"><span data-stu-id="215f6-106">You can control in Azure AD who has access to FirmPlay - Employee Advocacy for Recruiting</span></span>
- <span data-ttu-id="215f6-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do FirmPlay - propagowanie pracownika dla Rekrutacja (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="215f6-107">You can enable your users to automatically get signed-on to FirmPlay - Employee Advocacy for Recruiting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="215f6-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="215f6-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="215f6-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="215f6-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="215f6-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="215f6-110">Prerequisites</span></span>

<span data-ttu-id="215f6-111">Aby skonfigurować integrację usługi Azure AD z FirmPlay - propagowanie pracownika dla Rekrutacja, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="215f6-111">To configure Azure AD integration with FirmPlay - Employee Advocacy for Recruiting, you need the following items:</span></span>

- <span data-ttu-id="215f6-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="215f6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="215f6-113">FirmPlay - propagowanie pracownika dla rekrutacji jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="215f6-113">A FirmPlay - Employee Advocacy for Recruiting single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="215f6-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="215f6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="215f6-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="215f6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="215f6-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="215f6-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="215f6-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="215f6-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="215f6-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="215f6-118">Scenario description</span></span>
<span data-ttu-id="215f6-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="215f6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="215f6-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="215f6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="215f6-121">Dodawanie FirmPlay - propagowanie pracownika dla Rekrutacja z galerii</span><span class="sxs-lookup"><span data-stu-id="215f6-121">Adding FirmPlay - Employee Advocacy for Recruiting from the gallery</span></span>
2. <span data-ttu-id="215f6-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="215f6-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-the-gallery"></a><span data-ttu-id="215f6-123">Dodawanie FirmPlay - propagowanie pracownika dla Rekrutacja z galerii</span><span class="sxs-lookup"><span data-stu-id="215f6-123">Adding FirmPlay - Employee Advocacy for Recruiting from the gallery</span></span>
<span data-ttu-id="215f6-124">Aby skonfigurować integrację FirmPlay - propagowanie pracownika dla Rekrutacja do usługi Azure AD, należy dodać FirmPlay - propagowanie pracownika dla Rekrutacja z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="215f6-124">To configure the integration of FirmPlay - Employee Advocacy for Recruiting into Azure AD, you need to add FirmPlay - Employee Advocacy for Recruiting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="215f6-125">**Aby dodać FirmPlay - propagowanie pracownika dla Rekrutacja z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="215f6-125">**To add FirmPlay - Employee Advocacy for Recruiting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="215f6-126">W  **[portalu zarządzania Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="215f6-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="215f6-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="215f6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="215f6-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="215f6-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="215f6-131">Kliknij przycisk **Dodaj** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="215f6-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="215f6-133">W polu wyszukiwania wpisz **FirmPlay - propagowanie pracownika dla Rekrutacja**.</span><span class="sxs-lookup"><span data-stu-id="215f6-133">In the search box, type **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. <span data-ttu-id="215f6-135">W panelu wyników wybierz **FirmPlay - propagowanie pracownika dla Rekrutacja**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="215f6-135">In the results panel, select **FirmPlay - Employee Advocacy for Recruiting**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="215f6-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="215f6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="215f6-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z FirmPlay - propagowanie pracownika dla Rekrutacja w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="215f6-138">In this section, you configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="215f6-139">Logowanie jednokrotne do pracy usługi Azure AD musi wiedzieć, jaki użytkownik odpowiednika w FirmPlay — propagowanie pracownika dla Rekrutacja jest użytkownikiem w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="215f6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FirmPlay - Employee Advocacy for Recruiting is to a user in Azure AD.</span></span> <span data-ttu-id="215f6-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w FirmPlay - propagowanie pracownika dla rekrutacji powinien być określony.</span><span class="sxs-lookup"><span data-stu-id="215f6-140">In other words, a link relationship between an Azure AD user and the related user in FirmPlay - Employee Advocacy for Recruiting needs to be established.</span></span>

<span data-ttu-id="215f6-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w FirmPlay - propagowanie pracownika dla Rekrutacja.</span><span class="sxs-lookup"><span data-stu-id="215f6-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FirmPlay - Employee Advocacy for Recruiting.</span></span>

<span data-ttu-id="215f6-142">Do konfigurowania i testowania usługi Azure AD rejestracji jednokrotnej z FirmPlay - propagowanie pracownika dla Rekrutacja, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="215f6-142">To configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="215f6-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="215f6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="215f6-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="215f6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="215f6-145">**[Tworzenie FirmPlay - propagowanie pracownika dla użytkownika testowego Rekrutacja](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta FirmPlay: propagowanie pracownika dla rekrutacji, który jest połączony z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="215f6-145">**[Creating a FirmPlay - Employee Advocacy for Recruiting test user](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** - to have a counterpart of Britta Simon in FirmPlay: Employee Advocacy for Recruiting that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="215f6-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="215f6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="215f6-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="215f6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="215f6-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="215f6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="215f6-149">W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure i skonfigurować logowanie jednokrotne w sieci FirmPlay - propagowanie pracownika Rekrutacja aplikacji.</span><span class="sxs-lookup"><span data-stu-id="215f6-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FirmPlay - Employee Advocacy for Recruiting application.</span></span>

<span data-ttu-id="215f6-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z FirmPlay - propagowanie pracownika dla Rekrutacja, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="215f6-150">**To configure Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, perform the following steps:**</span></span>

1. <span data-ttu-id="215f6-151">W portalu zarządzania Azure na **FirmPlay - propagowanie pracownika dla Rekrutacja** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="215f6-151">In the Azure Management portal, on the **FirmPlay - Employee Advocacy for Recruiting** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="215f6-153">Na **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** Włącz funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="215f6-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. <span data-ttu-id="215f6-155">Na **FirmPlay - propagowanie pracownika rekrutacji domeny i adresów URL** sekcji w **na adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<your-subdomain>.firmplay.com/`</span><span class="sxs-lookup"><span data-stu-id="215f6-155">On the **FirmPlay - Employee Advocacy for Recruiting Domain and URLs** section, in the **Sign On URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.firmplay.com/`</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > <span data-ttu-id="215f6-157">Należy pamiętać, że nie jest rzeczywistą wartość.</span><span class="sxs-lookup"><span data-stu-id="215f6-157">Please note that this is not the real value.</span></span> <span data-ttu-id="215f6-158">Należy zaktualizować tę wartość rzeczywista logowania na adres URL.</span><span class="sxs-lookup"><span data-stu-id="215f6-158">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="215f6-159">Skontaktuj się z [FirmPlay - propagowanie pracowników zespołu pomocy technicznej Rekrutacja](mailto:engineering@firmplay.com) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="215f6-159">Contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) to get this value.</span></span> 

4. <span data-ttu-id="215f6-160">Na **certyfikat podpisywania SAML** kliknij **Utwórz nowy certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="215f6-160">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. <span data-ttu-id="215f6-162">Na **Tworzenie nowego świadectwa** okna dialogowego, kliknij ikonę kalendarza i wybierz **Data wygaśnięcia**.</span><span class="sxs-lookup"><span data-stu-id="215f6-162">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="215f6-163">Następnie kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="215f6-163">Then click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="215f6-165">Na **certyfikat podpisywania SAML** wybierz opcję **uaktywnić nowego świadectwa** i kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="215f6-165">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. <span data-ttu-id="215f6-167">W oknie podręcznym **certyfikat przerzucania** okna, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="215f6-167">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="215f6-169">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="215f6-169">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. <span data-ttu-id="215f6-171">Na **FirmPlay - propagowanie pracownika rekrutacji konfiguracji** , kliknij przycisk **skonfigurować FirmPlay - propagowanie pracownika dla Rekrutacja** otworzyć **Konfigurowanie logowania jednokrotnego** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="215f6-171">On the **FirmPlay - Employee Advocacy for Recruiting Configuration** section, click **Configure FirmPlay - Employee Advocacy for Recruiting** to open **Configure sign-on** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. <span data-ttu-id="215f6-174">Aby uzyskać logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z [FirmPlay - propagowanie pracowników zespołu pomocy technicznej Rekrutacja](mailto:engineering@firmplay.com) i podaj następujące:</span><span class="sxs-lookup"><span data-stu-id="215f6-174">To get SSO configured for your application, contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) and provide them with the following:</span></span> 

    <span data-ttu-id="215f6-175">• Pobrany **plik certyfikatu**</span><span class="sxs-lookup"><span data-stu-id="215f6-175">•  The downloaded **Certificate file**</span></span>

    <span data-ttu-id="215f6-176">• **Adres URL usługi rejestracji jednokrotnej SAML**</span><span class="sxs-lookup"><span data-stu-id="215f6-176">•  The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="215f6-177">• **Identyfikator jednostki SAML**</span><span class="sxs-lookup"><span data-stu-id="215f6-177">•  The **SAML Entity ID**</span></span>

    <span data-ttu-id="215f6-178">• **Adresu URL wylogowania**</span><span class="sxs-lookup"><span data-stu-id="215f6-178">•  The **Sign-Out URL**</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="215f6-179">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="215f6-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="215f6-180">Celem tej sekcji jest tworzenie użytkownika testowego w portalu zarządzania Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="215f6-180">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="215f6-182">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="215f6-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="215f6-183">W **portalu zarządzania Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="215f6-183">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="215f6-185">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="215f6-185">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="215f6-187">W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="215f6-187">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="215f6-189">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="215f6-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="215f6-191">a.</span><span class="sxs-lookup"><span data-stu-id="215f6-191">a.</span></span> <span data-ttu-id="215f6-192">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="215f6-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="215f6-193">b.</span><span class="sxs-lookup"><span data-stu-id="215f6-193">b.</span></span> <span data-ttu-id="215f6-194">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="215f6-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="215f6-195">c.</span><span class="sxs-lookup"><span data-stu-id="215f6-195">c.</span></span> <span data-ttu-id="215f6-196">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="215f6-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="215f6-197">d.</span><span class="sxs-lookup"><span data-stu-id="215f6-197">d.</span></span> <span data-ttu-id="215f6-198">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="215f6-198">Click **Create**.</span></span> 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a><span data-ttu-id="215f6-199">Tworzenie FirmPlay - propagowanie pracownika dla użytkownika testowego Rekrutacja</span><span class="sxs-lookup"><span data-stu-id="215f6-199">Creating a FirmPlay - Employee Advocacy for Recruiting test user</span></span>

<span data-ttu-id="215f6-200">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w FirmPlay - propagowanie pracownika dla Rekrutacja.</span><span class="sxs-lookup"><span data-stu-id="215f6-200">In this section, you create a user called Britta Simon in FirmPlay - Employee Advocacy for Recruiting.</span></span> <span data-ttu-id="215f6-201">We współpracy z [FirmPlay - propagowanie pracowników zespołu pomocy technicznej Rekrutacja](mailto:engineering@firmplay.com) Aby dodać użytkowników w FirmPlay - propagowanie pracownika Rekrutacja platformy.</span><span class="sxs-lookup"><span data-stu-id="215f6-201">Please work with [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) to add the users in the FirmPlay - Employee Advocacy for Recruiting platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="215f6-202">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="215f6-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="215f6-203">W tej sekcji można włączyć Simona Britta do udostępnienia jej FirmPlay - propagowanie pracownika dla Rekrutacja za pomocą usługi Azure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="215f6-203">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to FirmPlay - Employee Advocacy for Recruiting.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="215f6-205">**Aby przypisać Simona Britta FirmPlay - propagowanie pracownika dla Rekrutacja, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="215f6-205">**To assign Britta Simon to FirmPlay - Employee Advocacy for Recruiting, perform the following steps:**</span></span>

1. <span data-ttu-id="215f6-206">Otwórz widok aplikacji w portalu zarządzania Azure, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="215f6-206">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="215f6-208">Na liście aplikacji zaznacz **FirmPlay - propagowanie pracownika dla Rekrutacja**.</span><span class="sxs-lookup"><span data-stu-id="215f6-208">In the applications list, select **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. <span data-ttu-id="215f6-210">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="215f6-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="215f6-212">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="215f6-212">Click **Add** button.</span></span> <span data-ttu-id="215f6-213">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="215f6-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="215f6-215">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="215f6-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="215f6-216">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="215f6-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="215f6-217">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="215f6-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="215f6-218">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="215f6-218">Testing single sign-on</span></span>

<span data-ttu-id="215f6-219">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="215f6-219">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="215f6-220">Po kliknięciu FirmPlay - propagowanie pracownika Rekrutacja kafelka w panelu dostępu należy należy pobrać automatycznie zalogowane do Twojej FirmPlay - propagowanie pracownika Rekrutacja aplikacji.</span><span class="sxs-lookup"><span data-stu-id="215f6-220">When you click the FirmPlay - Employee Advocacy for Recruiting tile in the Access Panel, you should get automatically signed-on to your FirmPlay - Employee Advocacy for Recruiting application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="215f6-221">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="215f6-221">Additional resources</span></span>

* [<span data-ttu-id="215f6-222">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="215f6-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="215f6-223">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="215f6-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png