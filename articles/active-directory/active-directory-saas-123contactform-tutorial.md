---
title: 'Samouczek: Integracji Azure Active Directory z 123ContactForm | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i 123ContactForm."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5211910a-ab96-4709-959a-524c4d57c43e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3a99f0841c3e0d973168991f5dbee40e54c1d054
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-123contactform"></a><span data-ttu-id="159ed-103">Samouczek: Integracji Azure Active Directory z 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="159ed-103">Tutorial: Azure Active Directory integration with 123ContactForm</span></span>

<span data-ttu-id="159ed-104">Z tego samouczka dowiesz się integrowanie 123ContactForm z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="159ed-104">In this tutorial, you learn how to integrate 123ContactForm with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="159ed-105">Integracja z usługą Azure AD 123ContactForm zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="159ed-105">Integrating 123ContactForm with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="159ed-106">Można kontrolować w usłudze Azure AD, który ma dostęp do 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="159ed-106">You can control in Azure AD who has access to 123ContactForm</span></span>
- <span data-ttu-id="159ed-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do 123ContactForm (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="159ed-107">You can enable your users to automatically get signed-on to 123ContactForm (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="159ed-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="159ed-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="159ed-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="159ed-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="159ed-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="159ed-110">Prerequisites</span></span>

<span data-ttu-id="159ed-111">Aby skonfigurować integrację usługi Azure AD z 123ContactForm, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="159ed-111">To configure Azure AD integration with 123ContactForm, you need the following items:</span></span>

- <span data-ttu-id="159ed-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="159ed-112">An Azure AD subscription</span></span>
- <span data-ttu-id="159ed-113">123ContactForm logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="159ed-113">A 123ContactForm single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="159ed-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="159ed-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="159ed-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="159ed-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="159ed-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="159ed-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="159ed-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="159ed-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="159ed-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="159ed-118">Scenario description</span></span>
<span data-ttu-id="159ed-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="159ed-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="159ed-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="159ed-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="159ed-121">Dodawanie 123ContactForm z galerii</span><span class="sxs-lookup"><span data-stu-id="159ed-121">Adding 123ContactForm from the gallery</span></span>
2. <span data-ttu-id="159ed-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="159ed-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-123contactform-from-the-gallery"></a><span data-ttu-id="159ed-123">Dodawanie 123ContactForm z galerii</span><span class="sxs-lookup"><span data-stu-id="159ed-123">Adding 123ContactForm from the gallery</span></span>
<span data-ttu-id="159ed-124">Aby skonfigurować integrację usługi Azure AD 123ContactForm, należy dodać 123ContactForm z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="159ed-124">To configure the integration of 123ContactForm into Azure AD, you need to add 123ContactForm from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="159ed-125">**Aby dodać 123ContactForm z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="159ed-125">**To add 123ContactForm from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="159ed-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="159ed-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="159ed-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="159ed-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="159ed-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="159ed-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="159ed-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="159ed-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="159ed-133">W polu wyszukiwania wpisz **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="159ed-133">In the search box, type **123ContactForm**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_search.png)

5. <span data-ttu-id="159ed-135">W panelu wyników wybierz **123ContactForm**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="159ed-135">In the results panel, select **123ContactForm**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="159ed-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="159ed-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="159ed-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z 123ContactForm na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="159ed-138">In this section, you configure and test Azure AD single sign-on with 123ContactForm based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="159ed-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w 123ContactForm jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="159ed-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 123ContactForm is to a user in Azure AD.</span></span> <span data-ttu-id="159ed-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w 123ContactForm musi się.</span><span class="sxs-lookup"><span data-stu-id="159ed-140">In other words, a link relationship between an Azure AD user and the related user in 123ContactForm needs to be established.</span></span>

<span data-ttu-id="159ed-141">W 123ContactForm, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="159ed-141">In 123ContactForm, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="159ed-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z 123ContactForm, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="159ed-142">To configure and test Azure AD single sign-on with 123ContactForm, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="159ed-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="159ed-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="159ed-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="159ed-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="159ed-145">**[Tworzenie użytkownika testowego 123ContactForm](#creating-a-123contactform-test-user)**  — mają odpowiednika Simona Britta w 123ContactForm połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="159ed-145">**[Creating a 123ContactForm test user](#creating-a-123contactform-test-user)** - to have a counterpart of Britta Simon in 123ContactForm that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="159ed-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="159ed-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="159ed-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="159ed-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="159ed-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="159ed-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="159ed-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="159ed-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 123ContactForm application.</span></span>

<span data-ttu-id="159ed-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z 123ContactForm, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="159ed-150">**To configure Azure AD single sign-on with 123ContactForm, perform the following steps:**</span></span>

1. <span data-ttu-id="159ed-151">W portalu Azure na **123ContactForm** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="159ed-151">In the Azure portal, on the **123ContactForm** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="159ed-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="159ed-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_samlbase.png)

3. <span data-ttu-id="159ed-155">Na **123ContactForm domeny i adres URL** sekcji, jeśli chcesz skonfigurować aplikację w **IDP zainicjował tryb**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="159ed-155">On the **123ContactForm Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-123contactform-tutorial/url1.png)

    <span data-ttu-id="159ed-157">a.</span><span class="sxs-lookup"><span data-stu-id="159ed-157">a.</span></span> <span data-ttu-id="159ed-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span><span class="sxs-lookup"><span data-stu-id="159ed-158">In the **Identifier** textbox, type a URL using the following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span></span>

    <span data-ttu-id="159ed-159">b.</span><span class="sxs-lookup"><span data-stu-id="159ed-159">b.</span></span> <span data-ttu-id="159ed-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span><span class="sxs-lookup"><span data-stu-id="159ed-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span></span>

4. <span data-ttu-id="159ed-161">Jeśli chcesz skonfigurować aplikację w **SP zainicjował tryb**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="159ed-161">If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-123contactform-tutorial/url2.png)

    <span data-ttu-id="159ed-163">a.</span><span class="sxs-lookup"><span data-stu-id="159ed-163">a.</span></span> <span data-ttu-id="159ed-164">Kliknij przycisk **Pokaż zaawansowane ustawienia adresu URL** opcji</span><span class="sxs-lookup"><span data-stu-id="159ed-164">Click the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="159ed-165">b.</span><span class="sxs-lookup"><span data-stu-id="159ed-165">b.</span></span> <span data-ttu-id="159ed-166">W **na adres URL logowania** tekstowym, wpisz adres URL jako:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span><span class="sxs-lookup"><span data-stu-id="159ed-166">In the **Sign On URL** textbox, type a URL as: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="159ed-167">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="159ed-167">These values are not real.</span></span> <span data-ttu-id="159ed-168">Musisz zaktualizować te wartości z rzeczywistego adresy URL i identyfikator, który znajduje się w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="159ed-168">You'll need to update these value from actual URLs and Identifier which is explained later in the tutorial.</span></span>
    
5. <span data-ttu-id="159ed-169">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="159ed-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_certificate.png) 

6. <span data-ttu-id="159ed-171">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="159ed-171">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-123contactform-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="159ed-173">Aby skonfigurować logowanie jednokrotne w **123ContactForm** stronie, przejdź do [https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="159ed-173">To configure single sign-on on **123ContactForm** side, go to [https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) and perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-123contactform-tutorial/submit.png) 

    <span data-ttu-id="159ed-175">a.</span><span class="sxs-lookup"><span data-stu-id="159ed-175">a.</span></span> <span data-ttu-id="159ed-176">W **E-mail** tekstowym, wpisz adres e-mail użytkownika tj</span><span class="sxs-lookup"><span data-stu-id="159ed-176">In the **Email** textbox, type the email of the user i.e</span></span> <span data-ttu-id="159ed-177">**BrittaSimon@Contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="159ed-177">**BrittaSimon@Contoso.com**.</span></span>

    <span data-ttu-id="159ed-178">b.</span><span class="sxs-lookup"><span data-stu-id="159ed-178">b.</span></span> <span data-ttu-id="159ed-179">Kliknij przycisk **przekazać** , a następnie przejdź do pliku XML metadanych, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="159ed-179">Click **Upload** and browse the Metadata XML file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="159ed-180">c.</span><span class="sxs-lookup"><span data-stu-id="159ed-180">c.</span></span> <span data-ttu-id="159ed-181">Kliknij przycisk **przesyłania formularza**.</span><span class="sxs-lookup"><span data-stu-id="159ed-181">Click **SUBMIT FORM**.</span></span>

8. <span data-ttu-id="159ed-182">Na **Konfigurowanie ustawień aplikacji Microsoft Azure AD — logowanie jednokrotne -** należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="159ed-182">On the **Microsoft Azure AD - Single sign-on - Configure App Settings** perform the following steps:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-123contactform-tutorial/url3.png)

    <span data-ttu-id="159ed-184">a.</span><span class="sxs-lookup"><span data-stu-id="159ed-184">a.</span></span> <span data-ttu-id="159ed-185">Jeśli chcesz skonfigurować aplikację w **IDP zainicjował tryb**, kopiowania **identyfikator** wartość dla swojego wystąpienia, a następnie wklej je **identyfikator** textbox w  **123ContactForm domeny i adres URL** sekcji z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="159ed-185">If you wish to configure the application in **IDP initiated mode**, copy the **IDENTIFIER** value for your instance and paste it in **Identifier** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="159ed-186">b.</span><span class="sxs-lookup"><span data-stu-id="159ed-186">b.</span></span> <span data-ttu-id="159ed-187">Jeśli chcesz skonfigurować aplikację w **IDP zainicjował tryb**, kopiowania **adres URL odpowiedzi** wartość dla swojego wystąpienia, a następnie wklej je **adres URL odpowiedzi służący** textbox w  **123ContactForm domeny i adres URL** sekcji z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="159ed-187">If you wish to configure the application in **IDP initiated mode**, copy the **REPLY URL** value for your instance and paste it in **Reply URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="159ed-188">c.</span><span class="sxs-lookup"><span data-stu-id="159ed-188">c.</span></span> <span data-ttu-id="159ed-189">Jeśli chcesz skonfigurować aplikację w **SP zainicjował tryb**, kopiowania **adres URL logowania na** wartość dla swojego wystąpienia, a następnie wklej je **na adres URL logowania** textbox w  **123ContactForm domeny i adres URL** sekcji z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="159ed-189">If you wish to configure the application in **SP initiated mode**, copy the **SIGN ON URL** value for your instance and paste it in **Sign On URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="159ed-190">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="159ed-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="159ed-191">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="159ed-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="159ed-192">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="159ed-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="159ed-193">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="159ed-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="159ed-194">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="159ed-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="159ed-196">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="159ed-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="159ed-197">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="159ed-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="159ed-199">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="159ed-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="159ed-201">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="159ed-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="159ed-203">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="159ed-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="159ed-205">a.</span><span class="sxs-lookup"><span data-stu-id="159ed-205">a.</span></span> <span data-ttu-id="159ed-206">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="159ed-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="159ed-207">b.</span><span class="sxs-lookup"><span data-stu-id="159ed-207">b.</span></span> <span data-ttu-id="159ed-208">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="159ed-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="159ed-209">c.</span><span class="sxs-lookup"><span data-stu-id="159ed-209">c.</span></span> <span data-ttu-id="159ed-210">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="159ed-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="159ed-211">d.</span><span class="sxs-lookup"><span data-stu-id="159ed-211">d.</span></span> <span data-ttu-id="159ed-212">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="159ed-212">Click **Create**.</span></span>
 
### <a name="creating-a-123contactform-test-user"></a><span data-ttu-id="159ed-213">Tworzenie użytkownika testowego 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="159ed-213">Creating a 123ContactForm test user</span></span>

<span data-ttu-id="159ed-214">Aplikacja obsługuje tylko w czasie Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników zostaną utworzone w aplikacji automatycznie.</span><span class="sxs-lookup"><span data-stu-id="159ed-214">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="159ed-215">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="159ed-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="159ed-216">W tej sekcji musisz włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udzielanie dostępu do 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="159ed-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 123ContactForm.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="159ed-218">**Aby przypisać Simona Britta 123ContactForm, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="159ed-218">**To assign Britta Simon to 123ContactForm, perform the following steps:**</span></span>

1. <span data-ttu-id="159ed-219">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="159ed-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="159ed-221">Na liście aplikacji zaznacz **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="159ed-221">In the applications list, select **123ContactForm**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_app.png) 

3. <span data-ttu-id="159ed-223">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="159ed-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="159ed-225">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="159ed-225">Click **Add** button.</span></span> <span data-ttu-id="159ed-226">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="159ed-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="159ed-228">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="159ed-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="159ed-229">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="159ed-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="159ed-230">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="159ed-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="159ed-231">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="159ed-231">Testing single sign-on</span></span>

<span data-ttu-id="159ed-232">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="159ed-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="159ed-233">Po kliknięciu kafelka 123ContactForm w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="159ed-233">When you click the 123ContactForm tile in the Access Panel, you should get automatically signed-on to your 123ContactForm application.</span></span>
<span data-ttu-id="159ed-234">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="159ed-234">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="159ed-235">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="159ed-235">Additional resources</span></span>

* [<span data-ttu-id="159ed-236">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="159ed-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="159ed-237">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="159ed-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_203.png

