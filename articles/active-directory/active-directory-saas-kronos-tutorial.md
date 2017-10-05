---
title: 'Samouczek: Integracji Azure Active Directory z Kronos | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Kronos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e28d6191-c375-43c6-b2df-22daa88d9939
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: eb61ec0a7d3e992a285b1af3d4a7fbe1feb8d991
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kronos"></a><span data-ttu-id="54a56-103">Samouczek: Integracji Azure Active Directory z Kronos</span><span class="sxs-lookup"><span data-stu-id="54a56-103">Tutorial: Azure Active Directory integration with Kronos</span></span>

<span data-ttu-id="54a56-104">Z tego samouczka dowiesz się integrowanie Kronos z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="54a56-104">In this tutorial, you learn how to integrate Kronos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="54a56-105">Integracja z usługą Azure AD Kronos zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="54a56-105">Integrating Kronos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="54a56-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Kronos</span><span class="sxs-lookup"><span data-stu-id="54a56-106">You can control in Azure AD who has access to Kronos</span></span>
- <span data-ttu-id="54a56-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Kronos (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="54a56-107">You can enable your users to automatically get signed-on to Kronos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="54a56-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="54a56-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="54a56-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="54a56-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54a56-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="54a56-110">Prerequisites</span></span>

<span data-ttu-id="54a56-111">Aby skonfigurować integrację usługi Azure AD z Kronos, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="54a56-111">To configure Azure AD integration with Kronos, you need the following items:</span></span>

- <span data-ttu-id="54a56-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="54a56-112">An Azure AD subscription</span></span>
- <span data-ttu-id="54a56-113">A **Kronos pracowników centralnej** logowanie Jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="54a56-113">A **Kronos Workforce Central** SSO enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="54a56-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="54a56-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="54a56-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="54a56-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="54a56-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="54a56-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="54a56-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="54a56-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="54a56-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="54a56-118">Scenario description</span></span>
<span data-ttu-id="54a56-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="54a56-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="54a56-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="54a56-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="54a56-121">Dodawanie Kronos z galerii</span><span class="sxs-lookup"><span data-stu-id="54a56-121">Adding Kronos from the gallery</span></span>
2. <span data-ttu-id="54a56-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="54a56-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kronos-from-the-gallery"></a><span data-ttu-id="54a56-123">Dodawanie Kronos z galerii</span><span class="sxs-lookup"><span data-stu-id="54a56-123">Adding Kronos from the gallery</span></span>
<span data-ttu-id="54a56-124">Aby skonfigurować integrację usługi Azure AD Kronos, należy dodać Kronos z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="54a56-124">To configure the integration of Kronos into Azure AD, you need to add Kronos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="54a56-125">**Aby dodać Kronos z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="54a56-125">**To add Kronos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="54a56-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="54a56-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="54a56-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="54a56-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="54a56-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="54a56-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="54a56-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="54a56-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="54a56-133">W polu wyszukiwania wpisz **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="54a56-133">In the search box, type **Kronos**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_search.png)

5. <span data-ttu-id="54a56-135">W panelu wyników wybierz **Kronos**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="54a56-135">In the results panel, select **Kronos**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="54a56-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="54a56-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="54a56-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Kronos na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="54a56-138">In this section, you configure and test Azure AD single sign-on with Kronos based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="54a56-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Kronos jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54a56-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kronos is to a user in Azure AD.</span></span> <span data-ttu-id="54a56-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Kronos musi się.</span><span class="sxs-lookup"><span data-stu-id="54a56-140">In other words, a link relationship between an Azure AD user and the related user in Kronos needs to be established.</span></span>

<span data-ttu-id="54a56-141">W Kronos, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="54a56-141">In Kronos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="54a56-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Kronos, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="54a56-142">To configure and test Azure AD single sign-on with Kronos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="54a56-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="54a56-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="54a56-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="54a56-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="54a56-145">**[Tworzenie użytkownika testowego Kronos](#creating-a-kronos-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Kronos połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="54a56-145">**[Creating a Kronos test user](#creating-a-kronos-test-user)** - to have a counterpart of Britta Simon in Kronos that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="54a56-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="54a56-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="54a56-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="54a56-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="54a56-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="54a56-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="54a56-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Kronos.</span><span class="sxs-lookup"><span data-stu-id="54a56-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kronos application.</span></span>

<span data-ttu-id="54a56-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Kronos, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="54a56-150">**To configure Azure AD single sign-on with Kronos, perform the following steps:**</span></span>

1. <span data-ttu-id="54a56-151">W portalu Azure na **Kronos** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="54a56-151">In the Azure portal, on the **Kronos** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="54a56-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="54a56-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_samlbase.png)

3. <span data-ttu-id="54a56-155">Na **Kronos domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="54a56-155">On the **Kronos Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_url.png)

    <span data-ttu-id="54a56-157">a.</span><span class="sxs-lookup"><span data-stu-id="54a56-157">a.</span></span> <span data-ttu-id="54a56-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.kronos.net/`</span><span class="sxs-lookup"><span data-stu-id="54a56-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.kronos.net/`</span></span>

    <span data-ttu-id="54a56-159">b.</span><span class="sxs-lookup"><span data-stu-id="54a56-159">b.</span></span> <span data-ttu-id="54a56-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span><span class="sxs-lookup"><span data-stu-id="54a56-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="54a56-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="54a56-161">These values are not real.</span></span> <span data-ttu-id="54a56-162">Rzeczywisty identyfikator i adres URL odpowiedzi, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="54a56-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="54a56-163">Skontaktuj się z [Kronos obsługuje zespołu](https://www.kronos.in/contact/en-in/form) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="54a56-163">Contact [Kronos support team](https://www.kronos.in/contact/en-in/form) to get these values.</span></span>
 
4. <span data-ttu-id="54a56-164">Aplikacja Kronos oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="54a56-164">Your Kronos application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="54a56-165">Praca z [Kronos obsługuje zespołu](https://www.kronos.in/contact/en-in/form) najpierw, aby zidentyfikować identyfikator użytkownika, który jest mapowany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="54a56-165">Work with [Kronos support team](https://www.kronos.in/contact/en-in/form) first to identify the correct user identifier, which is mapped into the application.</span></span> <span data-ttu-id="54a56-166">Wykonaj również wskazówki dotyczące atrybut, który będzie używał do tego mapowania.</span><span class="sxs-lookup"><span data-stu-id="54a56-166">Also please take the guidance about the attribute, which they want to use for this mapping.</span></span>
 
     <span data-ttu-id="54a56-167">Firma Microsoft zaleca używanie **"NameIdentifier"** atrybut jako identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="54a56-167">Microsoft recommends using the **"NameIdentifier"** attribute as user identifier.</span></span> <span data-ttu-id="54a56-168">Możesz zarządzać wartości tych atrybutów z **"Atrybuty użytkownika"** sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="54a56-168">You can manage the values of these attributes from the **"User Attributes"** section on application integration page.</span></span>
     
     <span data-ttu-id="54a56-169">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="54a56-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="54a56-170">W tym miejscu możemy zamapowaniu **identyfikator użytkownika (nameid)** z **ExtractMailPrefix()** funkcji **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="54a56-170">Here we have mapped the **User Identifier (nameid)** with **ExtractMailPrefix()** function of **user.userprincipalname**.</span></span> <span data-ttu-id="54a56-171">Dzięki temu wartość prefiksu adres e-mail użytkownika, który jest unikatowy identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="54a56-171">This gives the prefix value of email of the user which is the unique User ID.</span></span> <span data-ttu-id="54a56-172">To są wysyłane do aplikacji Kronos w każdym pomyślnym odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="54a56-172">This is sent to the Kronos application in every successful response.</span></span> 
     
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_attribute.png)

5. <span data-ttu-id="54a56-174">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego:</span><span class="sxs-lookup"><span data-stu-id="54a56-174">In the **User Attributes** section on the **Single sign-on** dialog:</span></span>

    <span data-ttu-id="54a56-175">a.</span><span class="sxs-lookup"><span data-stu-id="54a56-175">a.</span></span> <span data-ttu-id="54a56-176">Na liście rozwijanej identyfikator użytkownika, wybierz **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="54a56-176">In the User Identifier dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="54a56-177">b.</span><span class="sxs-lookup"><span data-stu-id="54a56-177">b.</span></span> <span data-ttu-id="54a56-178">W **poczty** listy rozwijanej wybierz **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="54a56-178">In the **Mail** dropdown list, select **user.userprincipalname**.</span></span>

6. <span data-ttu-id="54a56-179">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="54a56-179">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_certificate.png) 

7. <span data-ttu-id="54a56-181">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="54a56-181">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kronos-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="54a56-183">Do konfigurowania rejestracji jednokrotnej na **Kronos** stronie, musisz wysłać pobrany **XML metadanych** do [Kronos obsługuje zespołu](https://www.kronos.in/contact/en-in/form).</span><span class="sxs-lookup"><span data-stu-id="54a56-183">To configure single sign-on on **Kronos** side, you need to send the downloaded **Metadata XML** to [Kronos support team](https://www.kronos.in/contact/en-in/form).</span></span> 

> [!TIP]
> <span data-ttu-id="54a56-184">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="54a56-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="54a56-185">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="54a56-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="54a56-186">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="54a56-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="54a56-187">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="54a56-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="54a56-188">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="54a56-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="54a56-190">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="54a56-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="54a56-191">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="54a56-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="54a56-193">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="54a56-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="54a56-195">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="54a56-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="54a56-197">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="54a56-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="54a56-199">a.</span><span class="sxs-lookup"><span data-stu-id="54a56-199">a.</span></span> <span data-ttu-id="54a56-200">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="54a56-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="54a56-201">b.</span><span class="sxs-lookup"><span data-stu-id="54a56-201">b.</span></span> <span data-ttu-id="54a56-202">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="54a56-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="54a56-203">c.</span><span class="sxs-lookup"><span data-stu-id="54a56-203">c.</span></span> <span data-ttu-id="54a56-204">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="54a56-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="54a56-205">d.</span><span class="sxs-lookup"><span data-stu-id="54a56-205">d.</span></span> <span data-ttu-id="54a56-206">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="54a56-206">Click **Create**.</span></span>
 
### <a name="creating-a-kronos-test-user"></a><span data-ttu-id="54a56-207">Tworzenie użytkownika testowego Kronos</span><span class="sxs-lookup"><span data-stu-id="54a56-207">Creating a Kronos test user</span></span>

<span data-ttu-id="54a56-208">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Kronos.</span><span class="sxs-lookup"><span data-stu-id="54a56-208">In this section, you create a user called Britta Simon in Kronos.</span></span> <span data-ttu-id="54a56-209">Aplikacja Kronos musi wszystkich użytkowników na potrzeby aprowizacji w aplikacji przed wykonaniem logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="54a56-209">Kronos application needs all the users to be provisioned in the application before doing SSO.</span></span> 

<span data-ttu-id="54a56-210">Praca z [Kronos obsługuje zespołu](https://www.kronos.in/contact/en-in/form) do udostępnienia tych użytkowników do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="54a56-210">Work with the [Kronos support team](https://www.kronos.in/contact/en-in/form) to provision all these users into the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="54a56-211">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="54a56-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="54a56-212">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Kronos.</span><span class="sxs-lookup"><span data-stu-id="54a56-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kronos.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="54a56-214">**Aby przypisać Simona Britta Kronos, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="54a56-214">**To assign Britta Simon to Kronos, perform the following steps:**</span></span>

1. <span data-ttu-id="54a56-215">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="54a56-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="54a56-217">Na liście aplikacji zaznacz **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="54a56-217">In the applications list, select **Kronos**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_app.png) 

3. <span data-ttu-id="54a56-219">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="54a56-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="54a56-221">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="54a56-221">Click **Add** button.</span></span> <span data-ttu-id="54a56-222">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="54a56-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="54a56-224">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="54a56-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="54a56-225">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="54a56-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="54a56-226">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="54a56-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="54a56-227">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="54a56-227">Testing single sign-on</span></span>

<span data-ttu-id="54a56-228">W tej sekcji można przetestować konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="54a56-228">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="54a56-229">Po kliknięciu kafelka Kronos w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Kronos.</span><span class="sxs-lookup"><span data-stu-id="54a56-229">When you click the Kronos tile in the Access Panel, you should get automatically signed-on to your Kronos application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="54a56-230">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="54a56-230">Additional resources</span></span>

* [<span data-ttu-id="54a56-231">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="54a56-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="54a56-232">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="54a56-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_203.png

