---
title: 'Samouczek: Integracji Azure Active Directory z Lecorpio | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Lecorpio."
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
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 35c94e2d9d8a938971f85ea732a74a7e1655545e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lecorpio"></a><span data-ttu-id="86620-103">Samouczek: Integracji Azure Active Directory z Lecorpio</span><span class="sxs-lookup"><span data-stu-id="86620-103">Tutorial: Azure Active Directory integration with Lecorpio</span></span>

<span data-ttu-id="86620-104">Z tego samouczka dowiesz się integrowanie Lecorpio z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="86620-104">In this tutorial, you learn how to integrate Lecorpio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="86620-105">Integracja z usługą Azure AD Lecorpio zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="86620-105">Integrating Lecorpio with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="86620-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Lecorpio</span><span class="sxs-lookup"><span data-stu-id="86620-106">You can control in Azure AD who has access to Lecorpio</span></span>
- <span data-ttu-id="86620-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Lecorpio (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="86620-107">You can enable your users to automatically get signed-on to Lecorpio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="86620-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="86620-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="86620-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="86620-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86620-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="86620-110">Prerequisites</span></span>

<span data-ttu-id="86620-111">Aby skonfigurować integrację usługi Azure AD z Lecorpio, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="86620-111">To configure Azure AD integration with Lecorpio, you need the following items:</span></span>

- <span data-ttu-id="86620-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="86620-112">An Azure AD subscription</span></span>
- <span data-ttu-id="86620-113">Lecorpio jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="86620-113">A Lecorpio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="86620-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="86620-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="86620-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="86620-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="86620-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="86620-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="86620-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="86620-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="86620-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="86620-118">Scenario description</span></span>
<span data-ttu-id="86620-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="86620-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="86620-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="86620-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="86620-121">Dodawanie Lecorpio z galerii</span><span class="sxs-lookup"><span data-stu-id="86620-121">Adding Lecorpio from the gallery</span></span>
2. <span data-ttu-id="86620-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="86620-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lecorpio-from-the-gallery"></a><span data-ttu-id="86620-123">Dodawanie Lecorpio z galerii</span><span class="sxs-lookup"><span data-stu-id="86620-123">Adding Lecorpio from the gallery</span></span>
<span data-ttu-id="86620-124">Aby skonfigurować integrację usługi Azure AD Lecorpio, należy dodać Lecorpio z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="86620-124">To configure the integration of Lecorpio into Azure AD, you need to add Lecorpio from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="86620-125">**Aby dodać Lecorpio z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="86620-125">**To add Lecorpio from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="86620-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="86620-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="86620-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="86620-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="86620-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="86620-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="86620-131">Kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="86620-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="86620-133">W polu wyszukiwania wpisz **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="86620-133">In the search box, type **Lecorpio**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_search.png)

5. <span data-ttu-id="86620-135">W panelu wyników wybierz **Lecorpio**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="86620-135">In the results panel, select **Lecorpio**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="86620-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="86620-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="86620-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Lecorpio na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="86620-138">In this section, you configure and test Azure AD single sign-on with Lecorpio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="86620-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Lecorpio jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86620-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lecorpio is to a user in Azure AD.</span></span> <span data-ttu-id="86620-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Lecorpio musi się.</span><span class="sxs-lookup"><span data-stu-id="86620-140">In other words, a link relationship between an Azure AD user and the related user in Lecorpio needs to be established.</span></span>

<span data-ttu-id="86620-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="86620-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Lecorpio.</span></span>

<span data-ttu-id="86620-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Lecorpio, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="86620-142">To configure and test Azure AD single sign-on with Lecorpio, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="86620-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="86620-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="86620-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="86620-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="86620-145">**[Tworzenie użytkownika testowego Lecorpio](#creating-a-lecorpio-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Lecorpio połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="86620-145">**[Creating a Lecorpio test user](#creating-a-lecorpio-test-user)** - to have a counterpart of Britta Simon in Lecorpio that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="86620-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="86620-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="86620-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="86620-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="86620-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="86620-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="86620-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="86620-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lecorpio application.</span></span>

<span data-ttu-id="86620-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Lecorpio, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="86620-150">**To configure Azure AD single sign-on with Lecorpio, perform the following steps:**</span></span>

1. <span data-ttu-id="86620-151">W portalu Azure na **Lecorpio** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="86620-151">In the Azure portal, on the **Lecorpio** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="86620-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="86620-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_samlbase.png)

3. <span data-ttu-id="86620-155">Na **Lecorpio domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="86620-155">On the **Lecorpio Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_url.png)

    <span data-ttu-id="86620-157">a.</span><span class="sxs-lookup"><span data-stu-id="86620-157">a.</span></span> <span data-ttu-id="86620-158">W **adres URL logowania** tekstowym, wpisz wartość, przy użyciu następującego wzorca:`https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="86620-158">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    <span data-ttu-id="86620-159">b.</span><span class="sxs-lookup"><span data-stu-id="86620-159">b.</span></span> <span data-ttu-id="86620-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="86620-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="86620-161">Wartości te nie są rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="86620-161">These values are not the real.</span></span> <span data-ttu-id="86620-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="86620-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="86620-163">W tym miejscu zalecamy można używać unikatowej wartości ciągu w identyfikatorze.</span><span class="sxs-lookup"><span data-stu-id="86620-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="86620-164">Skontaktuj się z [zespołem pomocy technicznej klienta Lecorpio](mailto:info@lecorpio.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="86620-164">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) to get these values.</span></span> 
 
4. <span data-ttu-id="86620-165">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="86620-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_certificate.png) 

5. <span data-ttu-id="86620-167">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="86620-167">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lecorpio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="86620-169">Skonfigurować logowanie jednokrotne w **Lecorpio** stronie, musisz wysłać pobrany **XML metadanych** do [zespołem pomocy technicznej Lecorpio](mailto:info@lecorpio.com).</span><span class="sxs-lookup"><span data-stu-id="86620-169">To configure single sign-on on **Lecorpio** side, you need to send the downloaded **Metadata XML** to [Lecorpio support team](mailto:info@lecorpio.com).</span></span>

> [!TIP]
> <span data-ttu-id="86620-170">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="86620-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="86620-171">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="86620-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="86620-172">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="86620-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="86620-173">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="86620-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="86620-174">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="86620-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="86620-176">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="86620-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="86620-177">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="86620-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="86620-179">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="86620-179">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="86620-181">W górnej części okna dialogowego, kliknij przycisk **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="86620-181">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="86620-183">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="86620-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="86620-185">a.</span><span class="sxs-lookup"><span data-stu-id="86620-185">a.</span></span> <span data-ttu-id="86620-186">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="86620-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="86620-187">b.</span><span class="sxs-lookup"><span data-stu-id="86620-187">b.</span></span> <span data-ttu-id="86620-188">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="86620-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="86620-189">c.</span><span class="sxs-lookup"><span data-stu-id="86620-189">c.</span></span> <span data-ttu-id="86620-190">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="86620-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="86620-191">d.</span><span class="sxs-lookup"><span data-stu-id="86620-191">d.</span></span> <span data-ttu-id="86620-192">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="86620-192">Click **Create**.</span></span>
 
### <a name="creating-a-lecorpio-test-user"></a><span data-ttu-id="86620-193">Tworzenie użytkownika testowego Lecorpio</span><span class="sxs-lookup"><span data-stu-id="86620-193">Creating a Lecorpio test user</span></span>

<span data-ttu-id="86620-194">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="86620-194">In this section, you create a user called Britta Simon in Lecorpio.</span></span> 

<span data-ttu-id="86620-195">Skontaktuj się z [zespołem pomocy technicznej klienta Lecorpio](mailto:info@lecorpio.com) Aby dodać użytkowników w aplikacji Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="86620-195">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) to add the users in the Lecorpio application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="86620-196">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="86620-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="86620-197">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="86620-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lecorpio.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="86620-199">**Aby przypisać Simona Britta Lecorpio, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="86620-199">**To assign Britta Simon to Lecorpio, perform the following steps:**</span></span>

1. <span data-ttu-id="86620-200">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="86620-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="86620-202">Na liście aplikacji zaznacz **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="86620-202">In the applications list, select **Lecorpio**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_app.png) 

3. <span data-ttu-id="86620-204">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="86620-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="86620-206">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="86620-206">Click **Add** button.</span></span> <span data-ttu-id="86620-207">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="86620-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="86620-209">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="86620-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="86620-210">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="86620-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="86620-211">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="86620-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="86620-212">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="86620-212">Testing single sign-on</span></span>

<span data-ttu-id="86620-213">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="86620-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="86620-214">Po kliknięciu kafelka Lecorpio w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="86620-214">When you click the Lecorpio tile in the Access Panel, you should get automatically signed-on to your Lecorpio application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="86620-215">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="86620-215">Additional resources</span></span>

* [<span data-ttu-id="86620-216">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="86620-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="86620-217">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="86620-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_203.png

