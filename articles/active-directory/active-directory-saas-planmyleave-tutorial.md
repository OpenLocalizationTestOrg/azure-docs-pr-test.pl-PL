---
title: 'Samouczek: Integracji Azure Active Directory z PlanMyLeave | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i PlanMyLeave."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: ba418a641b339a0d94a3c7b2596d37fbd88a30c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a><span data-ttu-id="6c14c-103">Samouczek: Integracji Azure Active Directory z PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="6c14c-103">Tutorial: Azure Active Directory integration with PlanMyLeave</span></span>

<span data-ttu-id="6c14c-104">Z tego samouczka dowiesz się integrowanie PlanMyLeave z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6c14c-104">In this tutorial, you learn how to integrate PlanMyLeave with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6c14c-105">Integracja z usługą Azure AD PlanMyLeave zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="6c14c-105">Integrating PlanMyLeave with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6c14c-106">Można kontrolować w usłudze Azure AD, który ma dostęp do PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="6c14c-106">You can control in Azure AD who has access to PlanMyLeave</span></span>
- <span data-ttu-id="6c14c-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do PlanMyLeave (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c14c-107">You can enable your users to automatically get signed-on to PlanMyLeave (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6c14c-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="6c14c-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="6c14c-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6c14c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c14c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6c14c-110">Prerequisites</span></span>

<span data-ttu-id="6c14c-111">Aby skonfigurować integrację usługi Azure AD z PlanMyLeave, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6c14c-111">To configure Azure AD integration with PlanMyLeave, you need the following items:</span></span>

- <span data-ttu-id="6c14c-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c14c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6c14c-113">PlanMyLeave jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6c14c-113">A PlanMyLeave single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="6c14c-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="6c14c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="6c14c-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="6c14c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6c14c-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="6c14c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="6c14c-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6c14c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="6c14c-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="6c14c-118">Scenario description</span></span>
<span data-ttu-id="6c14c-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="6c14c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6c14c-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="6c14c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6c14c-121">Dodawanie PlanMyLeave z galerii</span><span class="sxs-lookup"><span data-stu-id="6c14c-121">Adding PlanMyLeave from the gallery</span></span>
2. <span data-ttu-id="6c14c-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6c14c-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-planmyleave-from-the-gallery"></a><span data-ttu-id="6c14c-123">Dodawanie PlanMyLeave z galerii</span><span class="sxs-lookup"><span data-stu-id="6c14c-123">Adding PlanMyLeave from the gallery</span></span>
<span data-ttu-id="6c14c-124">Aby skonfigurować integrację usługi Azure AD PlanMyLeave, należy dodać PlanMyLeave z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="6c14c-124">To configure the integration of PlanMyLeave into Azure AD, you need to add PlanMyLeave from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6c14c-125">**Aby dodać PlanMyLeave z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6c14c-125">**To add PlanMyLeave from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6c14c-126">W  **[portalu zarządzania Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6c14c-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="6c14c-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="6c14c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6c14c-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6c14c-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="6c14c-131">Kliknij przycisk **Dodaj** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6c14c-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="6c14c-133">W polu wyszukiwania wpisz **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="6c14c-133">In the search box, type **PlanMyLeave**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. <span data-ttu-id="6c14c-135">W panelu wyników wybierz **PlanMyLeave**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="6c14c-135">In the results panel, select **PlanMyLeave**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6c14c-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6c14c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6c14c-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z PlanMyLeave w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="6c14c-138">In this section, you configure and test Azure AD single sign-on with PlanMyLeave based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6c14c-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w PlanMyLeave jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c14c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PlanMyLeave is to a user in Azure AD.</span></span> <span data-ttu-id="6c14c-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w PlanMyLeave musi się.</span><span class="sxs-lookup"><span data-stu-id="6c14c-140">In other words, a link relationship between an Azure AD user and the related user in PlanMyLeave needs to be established.</span></span>

<span data-ttu-id="6c14c-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="6c14c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in PlanMyLeave.</span></span>

<span data-ttu-id="6c14c-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z PlanMyLeave, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="6c14c-142">To configure and test Azure AD single sign-on with PlanMyLeave, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6c14c-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="6c14c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6c14c-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6c14c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6c14c-145">**[Tworzenie użytkownika testowego PlanMyLeave](#creating-a-planmyleave-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta PlanMyLeave połączonego z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c14c-145">**[Creating a PlanMyLeave test user](#creating-a-planmyleave-test-user)** - to have a counterpart of Britta Simon in PlanMyLeave that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="6c14c-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6c14c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6c14c-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="6c14c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6c14c-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6c14c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6c14c-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure i skonfigurować logowanie jednokrotne w aplikacji PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="6c14c-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your PlanMyLeave application.</span></span>

<span data-ttu-id="6c14c-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z PlanMyLeave, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6c14c-150">**To configure Azure AD single sign-on with PlanMyLeave, perform the following steps:**</span></span>

1. <span data-ttu-id="6c14c-151">W portalu zarządzania Azure na **PlanMyLeave** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="6c14c-151">In the Azure Management portal, on the **PlanMyLeave** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="6c14c-153">Na **logowanie jednokrotne** strony okna dialogowego jako **tryb** wybierz **na języku SAML logowania jednokrotnego** Włącz funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="6c14c-153">On the **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. <span data-ttu-id="6c14c-155">Na **PlanMyLeave domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6c14c-155">On the **PlanMyLeave Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    <span data-ttu-id="6c14c-157">a.</span><span class="sxs-lookup"><span data-stu-id="6c14c-157">a.</span></span> <span data-ttu-id="6c14c-158">W **na adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company-name>.planmyleave.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="6c14c-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company-name>.planmyleave.com/Login.aspx`</span></span>
    
    <span data-ttu-id="6c14c-159">b.</span><span class="sxs-lookup"><span data-stu-id="6c14c-159">b.</span></span> <span data-ttu-id="6c14c-160">W **identyfikatorem** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company-name>.planmyleave.com`</span><span class="sxs-lookup"><span data-stu-id="6c14c-160">In the **Identifer** textbox, type a URL using the following pattern: `https://<company-name>.planmyleave.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6c14c-161">Należy pamiętać, że nie są one rzeczywiste wartości.</span><span class="sxs-lookup"><span data-stu-id="6c14c-161">Please note that these are not the real values.</span></span> <span data-ttu-id="6c14c-162">Należy zaktualizować te wartości przy użyciu rzeczywistego logowania na adres URL i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="6c14c-162">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="6c14c-163">Skontaktuj się z [zespołem pomocy technicznej PlanMyLeave](mailto:support@planmyleave.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="6c14c-163">Contact [PlanMyLeave support team](mailto:support@planmyleave.com) to get these values.</span></span>

4. <span data-ttu-id="6c14c-164">Na **certyfikat podpisywania SAML** kliknij **Utwórz nowy certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="6c14c-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. <span data-ttu-id="6c14c-166">Na **Tworzenie nowego świadectwa** okna dialogowego, kliknij ikonę kalendarza i wybierz **Data wygaśnięcia**.</span><span class="sxs-lookup"><span data-stu-id="6c14c-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="6c14c-167">Następnie kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6c14c-167">Then click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="6c14c-169">Na **certyfikat podpisywania SAML** wybierz opcję **uaktywnić nowego świadectwa** i kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6c14c-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. <span data-ttu-id="6c14c-171">W oknie podręcznym **certyfikat przerzucania** okna, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c14c-171">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="6c14c-173">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="6c14c-173">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. <span data-ttu-id="6c14c-175">Na **konfiguracji PlanMyLeave** , kliknij przycisk **skonfigurować PlanMyLeave** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="6c14c-175">On the **PlanMyLeave Configuration** section, click **Configure PlanMyLeave** to open **Configure sign-on** window.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. <span data-ttu-id="6c14c-178">W oknie przeglądarki innej witryny sieci web Zaloguj się do dzierżawy PlanMyLeave jako administrator.</span><span class="sxs-lookup"><span data-stu-id="6c14c-178">In a different web browser window, log into your PlanMyLeave tenant as an administrator.</span></span>

11. <span data-ttu-id="6c14c-179">Przejdź do **konfiguracji systemu**.</span><span class="sxs-lookup"><span data-stu-id="6c14c-179">Go to **System Setup**.</span></span> <span data-ttu-id="6c14c-180">Następnie na **zarządzania zabezpieczeniami** kliknij sekcję **ustawienia SAML firmy** .</span><span class="sxs-lookup"><span data-stu-id="6c14c-180">Then on the **Security Management** section click **Company SAML settings** .</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. <span data-ttu-id="6c14c-182">Na **ustawienia SAML** sekcji, kliknij ikonę edytora.</span><span class="sxs-lookup"><span data-stu-id="6c14c-182">On the **SAML Settings** section, click editor icon.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. <span data-ttu-id="6c14c-184">Na **ustawienia SAML aktualizacji** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6c14c-184">On the **Update SAML Settings** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    <span data-ttu-id="6c14c-186">a.</span><span class="sxs-lookup"><span data-stu-id="6c14c-186">a.</span></span>  <span data-ttu-id="6c14c-187">W **adres URL logowania** pole tekstowe, umieścić wartość elementu **SAML pojedynczy znak na adres URL usługi** z okna konfiguracji aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c14c-187">In the **Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="6c14c-188">b.</span><span class="sxs-lookup"><span data-stu-id="6c14c-188">b.</span></span>  <span data-ttu-id="6c14c-189">Otwórz plik pobranego certyfikatu w programie Notatnik, skopiuj tylko zawartość między---rozpocząć certyfikatu---i---koniec certyfikatu---go do Schowka, a następnie wklej go do **certyfikatu** pole tekstowe.</span><span class="sxs-lookup"><span data-stu-id="6c14c-189">Open your downloaded certificate file in notepad, copy only the content between the ---Begin Certificate--- and ---End certificate---- of it into your clipboard, and then paste it to the **Certificate** textbox.</span></span>

    <span data-ttu-id="6c14c-190">c.</span><span class="sxs-lookup"><span data-stu-id="6c14c-190">c.</span></span> <span data-ttu-id="6c14c-191">Ustaw "**jest włączona**"do"**tak**".</span><span class="sxs-lookup"><span data-stu-id="6c14c-191">Set "**Is Enable**" to "**Yes**".</span></span>

    <span data-ttu-id="6c14c-192">d.</span><span class="sxs-lookup"><span data-stu-id="6c14c-192">d.</span></span> <span data-ttu-id="6c14c-193">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="6c14c-193">Click **Save**.</span></span>



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6c14c-194">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c14c-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="6c14c-195">Celem tej sekcji jest tworzenie użytkownika testowego w portalu zarządzania Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6c14c-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="6c14c-197">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6c14c-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6c14c-198">W **portalu zarządzania Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6c14c-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6c14c-200">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="6c14c-200">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6c14c-202">W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6c14c-202">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6c14c-204">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6c14c-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6c14c-206">a.</span><span class="sxs-lookup"><span data-stu-id="6c14c-206">a.</span></span> <span data-ttu-id="6c14c-207">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6c14c-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6c14c-208">b.</span><span class="sxs-lookup"><span data-stu-id="6c14c-208">b.</span></span> <span data-ttu-id="6c14c-209">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6c14c-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6c14c-210">c.</span><span class="sxs-lookup"><span data-stu-id="6c14c-210">c.</span></span> <span data-ttu-id="6c14c-211">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="6c14c-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6c14c-212">d.</span><span class="sxs-lookup"><span data-stu-id="6c14c-212">d.</span></span> <span data-ttu-id="6c14c-213">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6c14c-213">Click **Create**.</span></span> 



### <a name="creating-a-planmyleave-test-user"></a><span data-ttu-id="6c14c-214">Tworzenie użytkownika testowego PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="6c14c-214">Creating a PlanMyLeave test user</span></span>

<span data-ttu-id="6c14c-215">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="6c14c-215">The objective of this section is to create a user called Britta Simon in PlanMyLeave.</span></span> <span data-ttu-id="6c14c-216">PlanMyLeave obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="6c14c-216">PlanMyLeave supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="6c14c-217">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="6c14c-217">There is no action item for you in this section.</span></span> <span data-ttu-id="6c14c-218">Nowy użytkownik zostanie utworzony podczas próby dostępu PlanMyLeave, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="6c14c-218">A new user will be created during an attempt to access PlanMyLeave if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="6c14c-219">Jeśli trzeba ręcznie utworzyć użytkownika, należy skontaktować się [zespołem pomocy technicznej PlanMyLeave](mailto:support@planmyleave.com).</span><span class="sxs-lookup"><span data-stu-id="6c14c-219">If you need to create an user manually, you need to contact [PlanMyLeave support team](mailto:support@planmyleave.com).</span></span>



### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6c14c-220">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c14c-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6c14c-221">W tej sekcji można włączyć Simona Britta do udostępnienia jej PlanMyLeave za pomocą usługi Azure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6c14c-221">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to PlanMyLeave.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="6c14c-223">**Aby przypisać Simona Britta PlanMyLeave, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6c14c-223">**To assign Britta Simon to PlanMyLeave, perform the following steps:**</span></span>

1. <span data-ttu-id="6c14c-224">Otwórz widok aplikacji w portalu zarządzania Azure, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6c14c-224">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="6c14c-226">Na liście aplikacji zaznacz **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="6c14c-226">In the applications list, select **PlanMyLeave**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. <span data-ttu-id="6c14c-228">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="6c14c-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="6c14c-230">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6c14c-230">Click **Add** button.</span></span> <span data-ttu-id="6c14c-231">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6c14c-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="6c14c-233">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="6c14c-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6c14c-234">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6c14c-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6c14c-235">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6c14c-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="6c14c-236">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6c14c-236">Testing single sign-on</span></span>

<span data-ttu-id="6c14c-237">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="6c14c-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6c14c-238">Po kliknięciu kafelka PlanMyLeave w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="6c14c-238">When you click the PlanMyLeave tile in the Access Panel, you should get automatically signed-on to your PlanMyLeave application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="6c14c-239">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="6c14c-239">Additional resources</span></span>

* [<span data-ttu-id="6c14c-240">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6c14c-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6c14c-241">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6c14c-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png