---
title: 'Samouczek: Integracji Azure Active Directory z Jive | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Jive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fc5659a-c116-4a1b-a601-333325a26b46
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 6d2d4b777d7afd74598d2eba4a7e3571a8a18d6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jive"></a><span data-ttu-id="4579c-103">Samouczek: Integracji Azure Active Directory z Jive</span><span class="sxs-lookup"><span data-stu-id="4579c-103">Tutorial: Azure Active Directory integration with Jive</span></span>

<span data-ttu-id="4579c-104">Z tego samouczka dowiesz się integrowanie Jive z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4579c-104">In this tutorial, you learn how to integrate Jive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4579c-105">Integracja z usługą Azure AD Jive zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="4579c-105">Integrating Jive with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4579c-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Jive</span><span class="sxs-lookup"><span data-stu-id="4579c-106">You can control in Azure AD who has access to Jive</span></span>
- <span data-ttu-id="4579c-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Jive (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4579c-107">You can enable your users to automatically get signed-on to Jive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4579c-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4579c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4579c-109">Jeśli chcesz dowiedzieć się więcej informacji na temat integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4579c-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4579c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4579c-110">Prerequisites</span></span>

<span data-ttu-id="4579c-111">Aby skonfigurować integrację usługi Azure AD z Jive, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="4579c-111">To configure Azure AD integration with Jive, you need the following items:</span></span>

- <span data-ttu-id="4579c-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4579c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4579c-113">Jive jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="4579c-113">A Jive single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4579c-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="4579c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4579c-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="4579c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4579c-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="4579c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4579c-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4579c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4579c-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="4579c-118">Scenario description</span></span>
<span data-ttu-id="4579c-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="4579c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4579c-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="4579c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4579c-121">Dodawanie Jive z galerii</span><span class="sxs-lookup"><span data-stu-id="4579c-121">Adding Jive from the gallery</span></span>
2. <span data-ttu-id="4579c-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="4579c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jive-from-the-gallery"></a><span data-ttu-id="4579c-123">Dodawanie Jive z galerii</span><span class="sxs-lookup"><span data-stu-id="4579c-123">Adding Jive from the gallery</span></span>
<span data-ttu-id="4579c-124">Aby skonfigurować integrację Jive do usługi Azure AD, należy dodać Jive z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="4579c-124">To configure the integration of Jive into Azure AD, you need to add Jive from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4579c-125">**Aby dodać Jive z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4579c-125">**To add Jive from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4579c-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4579c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="4579c-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="4579c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4579c-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4579c-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="4579c-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4579c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="4579c-133">W polu wyszukiwania wpisz **Jive**.</span><span class="sxs-lookup"><span data-stu-id="4579c-133">In the search box, type **Jive**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jive-tutorial/tutorial_jive_search.png)

5. <span data-ttu-id="4579c-135">W panelu wyników wybierz **Jive**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="4579c-135">In the results panel, select **Jive**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jive-tutorial/tutorial_jive_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4579c-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="4579c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4579c-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Jive na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="4579c-138">In this section, you configure and test Azure AD single sign-on with Jive based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4579c-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Jive jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4579c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jive is to a user in Azure AD.</span></span> <span data-ttu-id="4579c-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Jive musi się.</span><span class="sxs-lookup"><span data-stu-id="4579c-140">In other words, a link relationship between an Azure AD user and the related user in Jive needs to be established.</span></span>

<span data-ttu-id="4579c-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Jive.</span><span class="sxs-lookup"><span data-stu-id="4579c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Jive.</span></span>

<span data-ttu-id="4579c-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Jive, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="4579c-142">To configure and test Azure AD single sign-on with Jive, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4579c-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="4579c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4579c-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="4579c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4579c-145">**[Tworzenie użytkownika testowego Jive](#creating-a-jive-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Jive połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4579c-145">**[Creating a Jive test user](#creating-a-jive-test-user)** - to have a counterpart of Britta Simon in Jive that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4579c-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="4579c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4579c-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="4579c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4579c-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4579c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4579c-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Jive.</span><span class="sxs-lookup"><span data-stu-id="4579c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jive application.</span></span>

<span data-ttu-id="4579c-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Jive, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4579c-150">**To configure Azure AD single sign-on with Jive, perform the following steps:**</span></span>

1. <span data-ttu-id="4579c-151">W portalu Azure na **Jive** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="4579c-151">In the Azure portal, on the **Jive** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="4579c-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="4579c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jive-tutorial/tutorial_jive_samlbase.png)

3. <span data-ttu-id="4579c-155">Na **Jive domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4579c-155">On the **Jive Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jive-tutorial/tutorial_jive_url.png)

    <span data-ttu-id="4579c-157">a.</span><span class="sxs-lookup"><span data-stu-id="4579c-157">a.</span></span> <span data-ttu-id="4579c-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<instance name>.jivecustom.com`</span><span class="sxs-lookup"><span data-stu-id="4579c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instance name>.jivecustom.com`</span></span>

    <span data-ttu-id="4579c-159">b.</span><span class="sxs-lookup"><span data-stu-id="4579c-159">b.</span></span> <span data-ttu-id="4579c-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<instance name>.jiveon.com`</span><span class="sxs-lookup"><span data-stu-id="4579c-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance name>.jiveon.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4579c-161">Wartości te nie są rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="4579c-161">These values are not the real.</span></span> <span data-ttu-id="4579c-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="4579c-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="4579c-163">Skontaktuj się z [zespołem pomocy technicznej klienta Jive](https://www.jivesoftware.com/services-support/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="4579c-163">Contact [Jive Client support team](https://www.jivesoftware.com/services-support/) to get these values.</span></span> 
 
4. <span data-ttu-id="4579c-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="4579c-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jive-tutorial/tutorial_jive_certificate.png) 

5. <span data-ttu-id="4579c-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4579c-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jive-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4579c-168">Aby skonfigurować logowanie jednokrotne w **Jive** po stronie logowania jednokrotnego dla Twojej dzierżawy Jive jako administrator.</span><span class="sxs-lookup"><span data-stu-id="4579c-168">To configure single sign-on on **Jive** side, sign-on to your Jive tenant as an administrator.</span></span>

7. <span data-ttu-id="4579c-169">W menu u góry kliknij pozycję "**Saml**."</span><span class="sxs-lookup"><span data-stu-id="4579c-169">In the menu on the top, Click "**Saml**."</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-jive-tutorial/tutorial_jive_002.png)

    <span data-ttu-id="4579c-171">a.</span><span class="sxs-lookup"><span data-stu-id="4579c-171">a.</span></span> <span data-ttu-id="4579c-172">Wybierz **włączone** w obszarze **ogólne** kartę.</span><span class="sxs-lookup"><span data-stu-id="4579c-172">Select **Enabled** under the **General** tab.</span></span>   
    <span data-ttu-id="4579c-173">b.</span><span class="sxs-lookup"><span data-stu-id="4579c-173">b.</span></span> <span data-ttu-id="4579c-174">Kliknij przycisk "**Zapisz wszystkie ustawienia saml**" przycisku.</span><span class="sxs-lookup"><span data-stu-id="4579c-174">Click the "**Save all saml settings**" button.</span></span>

8. <span data-ttu-id="4579c-175">Przejdź do "**metadanych Idp**" kartę.</span><span class="sxs-lookup"><span data-stu-id="4579c-175">Navigate to the "**Idp Metadata**" tab.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-jive-tutorial/tutorial_jive_003.png)
   
    <span data-ttu-id="4579c-177">a.</span><span class="sxs-lookup"><span data-stu-id="4579c-177">a.</span></span> <span data-ttu-id="4579c-178">Skopiuj zawartość pliku XML metadanych pobranych, a następnie wklej go do **metadanych dostawcy tożsamości (IDP)** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="4579c-178">Copy the content of the downloaded metadata XML file, and then paste it into the **Identity Provider (IDP) Metadata** textbox.</span></span>
    
    <span data-ttu-id="4579c-179">b.</span><span class="sxs-lookup"><span data-stu-id="4579c-179">b.</span></span> <span data-ttu-id="4579c-180">Kliknij przycisk "**Zapisz wszystkie ustawienia saml**" przycisku.</span><span class="sxs-lookup"><span data-stu-id="4579c-180">Click the "**Save all saml settings**" button.</span></span> 

9. <span data-ttu-id="4579c-181">Przejdź do "**mapowanie atrybutu użytkownika**" kartę.</span><span class="sxs-lookup"><span data-stu-id="4579c-181">Go to the "**User Attribute Mapping**" tab.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-jive-tutorial/tutorial_jive_004.png)
   
    <span data-ttu-id="4579c-183">a.</span><span class="sxs-lookup"><span data-stu-id="4579c-183">a.</span></span> <span data-ttu-id="4579c-184">W **E-mail** pole tekstowe, skopiuj i Wklej nazwę **poczty** wartość.</span><span class="sxs-lookup"><span data-stu-id="4579c-184">In the **Email** textbox, copy and paste the attribute name of **mail** value.</span></span>
   
    <span data-ttu-id="4579c-185">b.</span><span class="sxs-lookup"><span data-stu-id="4579c-185">b.</span></span> <span data-ttu-id="4579c-186">W **imię** pole tekstowe, skopiuj i Wklej nazwę **givenname** wartości.</span><span class="sxs-lookup"><span data-stu-id="4579c-186">In the **First Name** textbox, copy and paste the attribute name of **givenname** value.</span></span>
   
    <span data-ttu-id="4579c-187">c.</span><span class="sxs-lookup"><span data-stu-id="4579c-187">c.</span></span> <span data-ttu-id="4579c-188">W **nazwisko** pole tekstowe, skopiuj i Wklej nazwę **nazwisko** wartość.</span><span class="sxs-lookup"><span data-stu-id="4579c-188">In the **Last Name** textbox, copy and paste the attribute name of **surname** value.</span></span>

> [!TIP]
> <span data-ttu-id="4579c-189">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="4579c-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4579c-190">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="4579c-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4579c-191">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4579c-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4579c-192">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4579c-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="4579c-193">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="4579c-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="4579c-195">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4579c-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4579c-196">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4579c-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4579c-198">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="4579c-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4579c-200">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4579c-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4579c-202">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4579c-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4579c-204">a.</span><span class="sxs-lookup"><span data-stu-id="4579c-204">a.</span></span> <span data-ttu-id="4579c-205">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4579c-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4579c-206">b.</span><span class="sxs-lookup"><span data-stu-id="4579c-206">b.</span></span> <span data-ttu-id="4579c-207">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4579c-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4579c-208">c.</span><span class="sxs-lookup"><span data-stu-id="4579c-208">c.</span></span> <span data-ttu-id="4579c-209">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="4579c-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4579c-210">d.</span><span class="sxs-lookup"><span data-stu-id="4579c-210">d.</span></span> <span data-ttu-id="4579c-211">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4579c-211">Click **Create**.</span></span>
 
### <a name="creating-a-jive-test-user"></a><span data-ttu-id="4579c-212">Tworzenie użytkownika testowego Jive</span><span class="sxs-lookup"><span data-stu-id="4579c-212">Creating a Jive test user</span></span>

<span data-ttu-id="4579c-213">Praca z [zespołem pomocy technicznej klienta Jive](https://www.jivesoftware.com/services-support/) Aby dodać użytkowników do platformy Jive.</span><span class="sxs-lookup"><span data-stu-id="4579c-213">Work with [Jive Client support team](https://www.jivesoftware.com/services-support/) to add the users in the Jive platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4579c-214">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4579c-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4579c-215">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Jive.</span><span class="sxs-lookup"><span data-stu-id="4579c-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jive.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="4579c-217">**Aby przypisać Simona Britta Jive, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4579c-217">**To assign Britta Simon to Jive, perform the following steps:**</span></span>

1. <span data-ttu-id="4579c-218">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4579c-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="4579c-220">Na liście aplikacji zaznacz **Jive**.</span><span class="sxs-lookup"><span data-stu-id="4579c-220">In the applications list, select **Jive**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jive-tutorial/tutorial_jive_app.png) 

3. <span data-ttu-id="4579c-222">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="4579c-222">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="4579c-224">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4579c-224">Click **Add** button.</span></span> <span data-ttu-id="4579c-225">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4579c-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="4579c-227">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="4579c-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4579c-228">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4579c-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4579c-229">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4579c-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4579c-230">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4579c-230">Testing single sign-on</span></span>

<span data-ttu-id="4579c-231">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="4579c-231">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4579c-232">Po kliknięciu kafelka Jive w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Jive.</span><span class="sxs-lookup"><span data-stu-id="4579c-232">When you click the Jive tile in the Access Panel, you should get automatically signed-on to your Jive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4579c-233">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="4579c-233">Additional resources</span></span>

* [<span data-ttu-id="4579c-234">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4579c-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4579c-235">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4579c-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="4579c-236">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="4579c-236">Configure User Provisioning</span></span>](active-directory-saas-jive-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jive-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jive-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jive-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jive-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jive-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jive-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jive-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jive-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jive-tutorial/tutorial_general_203.png

