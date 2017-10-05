---
title: "Samouczek: Integracji Azure Active Directory z zespołową | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Praca w zespole."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03760032-3d76-4b47-ab84-241f72fbd561
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: edd2f9446515531f1147a8abf99295b618b89b25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamwork"></a><span data-ttu-id="97705-103">Samouczek: Integracji Azure Active Directory z zespołową</span><span class="sxs-lookup"><span data-stu-id="97705-103">Tutorial: Azure Active Directory integration with Teamwork</span></span>

<span data-ttu-id="97705-104">Z tego samouczka dowiesz się integrowanie pracę z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="97705-104">In this tutorial, you learn how to integrate Teamwork with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="97705-105">Integrowanie pracę z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="97705-105">Integrating Teamwork with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="97705-106">Można kontrolować w usłudze Azure AD, który ma dostęp do wszystkich członków zespołu</span><span class="sxs-lookup"><span data-stu-id="97705-106">You can control in Azure AD who has access to Teamwork</span></span>
- <span data-ttu-id="97705-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do wszystkich członków zespołu (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="97705-107">You can enable your users to automatically get signed-on to Teamwork (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="97705-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="97705-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="97705-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="97705-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97705-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="97705-110">Prerequisites</span></span>

<span data-ttu-id="97705-111">Aby skonfigurować integrację usługi Azure AD z zespołowej, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="97705-111">To configure Azure AD integration with Teamwork, you need the following items:</span></span>

- <span data-ttu-id="97705-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="97705-112">An Azure AD subscription</span></span>
- <span data-ttu-id="97705-113">Praca w zespole jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="97705-113">A Teamwork single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="97705-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="97705-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="97705-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="97705-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="97705-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="97705-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="97705-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="97705-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="97705-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="97705-118">Scenario description</span></span>
<span data-ttu-id="97705-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="97705-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="97705-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="97705-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="97705-121">Dodawanie pracę z galerii</span><span class="sxs-lookup"><span data-stu-id="97705-121">Adding Teamwork from the gallery</span></span>
2. <span data-ttu-id="97705-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="97705-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-teamwork-from-the-gallery"></a><span data-ttu-id="97705-123">Dodawanie pracę z galerii</span><span class="sxs-lookup"><span data-stu-id="97705-123">Adding Teamwork from the gallery</span></span>
<span data-ttu-id="97705-124">Aby skonfigurować integrację pracę z usługą Azure AD, należy dodać pracę z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="97705-124">To configure the integration of Teamwork into Azure AD, you need to add Teamwork from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="97705-125">**Aby dodać pracę z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="97705-125">**To add Teamwork from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="97705-126">W  **[portalu zarządzania Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="97705-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="97705-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="97705-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="97705-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="97705-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="97705-131">Kliknij przycisk **Dodaj** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="97705-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="97705-133">W polu wyszukiwania wpisz **zespołową**.</span><span class="sxs-lookup"><span data-stu-id="97705-133">In the search box, type **Teamwork**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_001.png)

5. <span data-ttu-id="97705-135">W panelu wyników wybierz **zespołową**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="97705-135">In the results panel, select **Teamwork**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="97705-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="97705-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="97705-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z zespołową w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="97705-138">In this section, you configure and test Azure AD single sign-on with Teamwork based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="97705-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w zespołowej jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97705-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamwork is to a user in Azure AD.</span></span> <span data-ttu-id="97705-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w zespołowej musi się.</span><span class="sxs-lookup"><span data-stu-id="97705-140">In other words, a link relationship between an Azure AD user and the related user in Teamwork needs to be established.</span></span>

<span data-ttu-id="97705-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w zespołowej.</span><span class="sxs-lookup"><span data-stu-id="97705-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Teamwork.</span></span>

<span data-ttu-id="97705-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z zespołowej, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="97705-142">To configure and test Azure AD single sign-on with Teamwork, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="97705-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="97705-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="97705-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="97705-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="97705-145">**[Tworzenie użytkownika testowego zespołową](#creating-a-teamwork-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta zespołową połączonego z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97705-145">**[Creating a Teamwork test user](#creating-a-teamwork-test-user)** - to have a counterpart of Britta Simon in Teamwork that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="97705-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="97705-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="97705-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="97705-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="97705-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="97705-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="97705-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure i skonfigurować logowanie jednokrotne w aplikacji zespołowej.</span><span class="sxs-lookup"><span data-stu-id="97705-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Teamwork application.</span></span>

<span data-ttu-id="97705-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z zespołowej, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="97705-150">**To configure Azure AD single sign-on with Teamwork, perform the following steps:**</span></span>

1. <span data-ttu-id="97705-151">W portalu zarządzania Azure na **zespołową** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="97705-151">In the Azure Management portal, on the **Teamwork** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="97705-153">Na **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** Włącz funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="97705-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_01.png)

3. <span data-ttu-id="97705-155">Na **zespołową domeny i adres URL** sekcji w **na adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.teamwork.com`</span><span class="sxs-lookup"><span data-stu-id="97705-155">On the **Teamwork Domain and URLs** section, in the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.teamwork.com`</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_02.png)

    > [!NOTE] 
    > <span data-ttu-id="97705-157">Należy pamiętać, że nie jest rzeczywistą wartość.</span><span class="sxs-lookup"><span data-stu-id="97705-157">Please note that this is not the real value.</span></span> <span data-ttu-id="97705-158">Należy zaktualizować tę wartość rzeczywista logowania na adres URL.</span><span class="sxs-lookup"><span data-stu-id="97705-158">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="97705-159">Skontaktuj się z [zespołem pomocy technicznej zespołową](mailto:support@teamwork.com) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="97705-159">Contact [Teamwork support team](mailto:support@teamwork.com) to get this value.</span></span> 

4. <span data-ttu-id="97705-160">Na **certyfikat podpisywania SAML** kliknij **Utwórz nowy certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="97705-160">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_03.png)   

5. <span data-ttu-id="97705-162">Na **Tworzenie nowego świadectwa** okna dialogowego, kliknij ikonę kalendarza i wybierz **Data wygaśnięcia**.</span><span class="sxs-lookup"><span data-stu-id="97705-162">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="97705-163">Następnie kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="97705-163">Then click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamwork-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="97705-165">Na **certyfikat podpisywania SAML** wybierz opcję **uaktywnić nowego świadectwa** i kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="97705-165">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_04.png)

7. <span data-ttu-id="97705-167">W oknie podręcznym **certyfikat przerzucania** okna, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="97705-167">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamwork-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="97705-169">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="97705-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_05.png) 

9. <span data-ttu-id="97705-171">Aby uzyskać logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z [zespołem pomocy technicznej zespołową](mailto:support@teamwork.com) i udostępnia je z pobranego **metadanych**.</span><span class="sxs-lookup"><span data-stu-id="97705-171">To get SSO configured for your application, contact [Teamwork support team](mailto:support@teamwork.com) and provide them with the downloaded **metadata**.</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="97705-172">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="97705-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="97705-173">Celem tej sekcji jest tworzenie użytkownika testowego w portalu zarządzania Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="97705-173">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="97705-175">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="97705-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="97705-176">W **portalu zarządzania Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="97705-176">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="97705-178">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="97705-178">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="97705-180">W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="97705-180">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="97705-182">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="97705-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="97705-184">a.</span><span class="sxs-lookup"><span data-stu-id="97705-184">a.</span></span> <span data-ttu-id="97705-185">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="97705-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="97705-186">b.</span><span class="sxs-lookup"><span data-stu-id="97705-186">b.</span></span> <span data-ttu-id="97705-187">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="97705-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="97705-188">c.</span><span class="sxs-lookup"><span data-stu-id="97705-188">c.</span></span> <span data-ttu-id="97705-189">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="97705-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="97705-190">d.</span><span class="sxs-lookup"><span data-stu-id="97705-190">d.</span></span> <span data-ttu-id="97705-191">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="97705-191">Click **Create**.</span></span> 



### <a name="creating-a-teamwork-test-user"></a><span data-ttu-id="97705-192">Tworzenie użytkownika testowego zespołową</span><span class="sxs-lookup"><span data-stu-id="97705-192">Creating a Teamwork test user</span></span>

<span data-ttu-id="97705-193">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w zespołowej.</span><span class="sxs-lookup"><span data-stu-id="97705-193">In this section, you create a user called Britta Simon in Teamwork.</span></span> <span data-ttu-id="97705-194">We współpracy z [zespołem pomocy technicznej zespołową](mailto:support@teamwork.com) Aby dodać użytkowników na platformie Praca w zespole.</span><span class="sxs-lookup"><span data-stu-id="97705-194">Please work with [Teamwork support team](mailto:support@teamwork.com) to add the users in the Teamwork platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="97705-195">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="97705-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="97705-196">W tej sekcji można włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udostępnienie jej do wszystkich członków zespołu.</span><span class="sxs-lookup"><span data-stu-id="97705-196">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Teamwork.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="97705-198">**Aby przypisać Simona Britta zespołowej, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="97705-198">**To assign Britta Simon to Teamwork, perform the following steps:**</span></span>

1. <span data-ttu-id="97705-199">Otwórz widok aplikacji w portalu zarządzania Azure, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="97705-199">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="97705-201">Na liście aplikacji zaznacz **zespołową**.</span><span class="sxs-lookup"><span data-stu-id="97705-201">In the applications list, select **Teamwork**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_50.png) 

3. <span data-ttu-id="97705-203">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="97705-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="97705-205">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="97705-205">Click **Add** button.</span></span> <span data-ttu-id="97705-206">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="97705-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="97705-208">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="97705-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="97705-209">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="97705-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="97705-210">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="97705-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="97705-211">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="97705-211">Testing single sign-on</span></span>

<span data-ttu-id="97705-212">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="97705-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="97705-213">Po kliknięciu kafelka zespołową w panelu dostępu należy powinien pobrać automatycznie zalogowane do aplikacji Praca w zespole.</span><span class="sxs-lookup"><span data-stu-id="97705-213">When you click the Teamwork tile in the Access Panel, you should get automatically signed-on to your Teamwork application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="97705-214">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="97705-214">Additional resources</span></span>

* [<span data-ttu-id="97705-215">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="97705-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="97705-216">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="97705-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_203.png