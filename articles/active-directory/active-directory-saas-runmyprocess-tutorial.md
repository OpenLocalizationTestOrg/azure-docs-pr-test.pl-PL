---
title: 'Samouczek: Integracji Azure Active Directory z RunMyProcess | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i RunMyProcess."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d31f7395-048b-4a61-9505-5acf9fc68d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f8a08ef4f90d5cb98e7648ae6001055a3f4696e8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-runmyprocess"></a><span data-ttu-id="5312c-103">Samouczek: Integracji Azure Active Directory z RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="5312c-103">Tutorial: Azure Active Directory integration with RunMyProcess</span></span>

<span data-ttu-id="5312c-104">Z tego samouczka dowiesz się integrowanie RunMyProcess z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5312c-104">In this tutorial, you learn how to integrate RunMyProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5312c-105">Integracja z usługą Azure AD RunMyProcess zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5312c-105">Integrating RunMyProcess with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5312c-106">Można kontrolować w usłudze Azure AD, który ma dostęp do RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="5312c-106">You can control in Azure AD who has access to RunMyProcess</span></span>
- <span data-ttu-id="5312c-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do RunMyProcess (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5312c-107">You can enable your users to automatically get signed-on to RunMyProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5312c-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5312c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5312c-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5312c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5312c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5312c-110">Prerequisites</span></span>

<span data-ttu-id="5312c-111">Aby skonfigurować integrację usługi Azure AD z RunMyProcess, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5312c-111">To configure Azure AD integration with RunMyProcess, you need the following items:</span></span>

- <span data-ttu-id="5312c-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5312c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5312c-113">RunMyProcess logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5312c-113">A RunMyProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5312c-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5312c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5312c-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5312c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5312c-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5312c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5312c-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj:[oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5312c-117">If you don't have an Azure AD trial environment, you can get a one-month trial here:[Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5312c-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5312c-118">Scenario description</span></span>
<span data-ttu-id="5312c-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5312c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5312c-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5312c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5312c-121">Dodawanie RunMyProcess z galerii</span><span class="sxs-lookup"><span data-stu-id="5312c-121">Adding RunMyProcess from the gallery</span></span>
2. <span data-ttu-id="5312c-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5312c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-runmyprocess-from-the-gallery"></a><span data-ttu-id="5312c-123">Dodawanie RunMyProcess z galerii</span><span class="sxs-lookup"><span data-stu-id="5312c-123">Adding RunMyProcess from the gallery</span></span>
<span data-ttu-id="5312c-124">Aby skonfigurować integrację usługi Azure AD RunMyProcess, należy dodać RunMyProcess z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5312c-124">To configure the integration of RunMyProcess into Azure AD, you need to add RunMyProcess from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5312c-125">**Aby dodać RunMyProcess z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5312c-125">**To add RunMyProcess from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5312c-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5312c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="5312c-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5312c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5312c-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5312c-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="5312c-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5312c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="5312c-133">W polu wyszukiwania wpisz **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="5312c-133">In the search box, type **RunMyProcess**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_search.png)

5. <span data-ttu-id="5312c-135">W panelu wyników wybierz **RunMyProcess**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="5312c-135">In the results panel, select **RunMyProcess**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5312c-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5312c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5312c-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z RunMyProcess w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="5312c-138">In this section, you configure and test Azure AD single sign-on with RunMyProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5312c-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w RunMyProcess jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5312c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RunMyProcess is to a user in Azure AD.</span></span> <span data-ttu-id="5312c-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w RunMyProcess musi się.</span><span class="sxs-lookup"><span data-stu-id="5312c-140">In other words, a link relationship between an Azure AD user and the related user in RunMyProcess needs to be established.</span></span>

<span data-ttu-id="5312c-141">W RunMyProcess, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="5312c-141">In RunMyProcess, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5312c-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z RunMyProcess, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="5312c-142">To configure and test Azure AD single sign-on with RunMyProcess, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5312c-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5312c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5312c-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5312c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5312c-145">**[Tworzenie użytkownika testowego RunMyProcess](#creating-a-runmyprocess-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta RunMyProcess połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5312c-145">**[Creating a RunMyProcess test user](#creating-a-runmyprocess-test-user)** - to have a counterpart of Britta Simon in RunMyProcess that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5312c-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5312c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5312c-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="5312c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5312c-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5312c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5312c-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="5312c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RunMyProcess application.</span></span>

<span data-ttu-id="5312c-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z RunMyProcess, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5312c-150">**To configure Azure AD single sign-on with RunMyProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="5312c-151">W portalu Azure na **RunMyProcess** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="5312c-151">In the Azure portal, on the **RunMyProcess** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="5312c-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="5312c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_samlbase.png)

3. <span data-ttu-id="5312c-155">Na **RunMyProcess domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5312c-155">On the **RunMyProcess Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_url.png)

    <span data-ttu-id="5312c-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://live.runmyprocess.com/live/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="5312c-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://live.runmyprocess.com/live/<tenant id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5312c-158">Wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="5312c-158">The value is not real.</span></span> <span data-ttu-id="5312c-159">Zaktualizuj tę wartość z adresem URL logowania rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="5312c-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="5312c-160">Skontaktuj się z [zespołem pomocy technicznej klienta RunMyProcess](mailto:support@runmyprocess.com) można uzyskać wartość.</span><span class="sxs-lookup"><span data-stu-id="5312c-160">Contact [RunMyProcess Client support team](mailto:support@runmyprocess.com) to get the value.</span></span> 

4. <span data-ttu-id="5312c-161">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5312c-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_certificate.png) 

5. <span data-ttu-id="5312c-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5312c-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5312c-165">Na **konfiguracji RunMyProcess** , kliknij przycisk **skonfigurować RunMyProcess** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="5312c-165">On the **RunMyProcess Configuration** section, click **Configure RunMyProcess** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5312c-166">Kopiuj **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="5312c-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_configure.png) 

7. <span data-ttu-id="5312c-168">W oknie przeglądarki innej witryny sieci web logowanie do dzierżawy RunMyProcess jako administrator.</span><span class="sxs-lookup"><span data-stu-id="5312c-168">In a different web browser window, sign-on to your RunMyProcess tenant as an administrator.</span></span>

8. <span data-ttu-id="5312c-169">W lewym panelu nawigacyjnym kliknij **konta** i wybierz **konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="5312c-169">In left navigation panel, click **Account** and select **Configuration**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_001.png)

9. <span data-ttu-id="5312c-171">Przejdź do **metodę uwierzytelniania** sekcji i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5312c-171">Go to **Authentication method** section and perform below steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_002.png)

    <span data-ttu-id="5312c-173">a.</span><span class="sxs-lookup"><span data-stu-id="5312c-173">a.</span></span> <span data-ttu-id="5312c-174">Jako **metody**, wybierz pozycję **rejestracji Jednokrotnej z Samlv2**.</span><span class="sxs-lookup"><span data-stu-id="5312c-174">As **Method**, select **SSO with Samlv2**.</span></span> 

    <span data-ttu-id="5312c-175">b.</span><span class="sxs-lookup"><span data-stu-id="5312c-175">b.</span></span> <span data-ttu-id="5312c-176">W **przekierowania logowania jednokrotnego** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5312c-176">In the **SSO redirect** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5312c-177">c.</span><span class="sxs-lookup"><span data-stu-id="5312c-177">c.</span></span> <span data-ttu-id="5312c-178">W **przekierowania wylogowania** pole tekstowe, Wklej wartość **Sign-Out URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5312c-178">In the **Logout redirect** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5312c-179">d.</span><span class="sxs-lookup"><span data-stu-id="5312c-179">d.</span></span> <span data-ttu-id="5312c-180">W **Format identyfikatora nazwy** tekstowym, wpisz wartość **Format identyfikatora nazwy** jako **urn: oasis: nazwy: tc: SAML:1.1:nameid-format: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="5312c-180">In the **Name Id Format** textbox, type the value of **Name Identifier Format** as **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="5312c-181">e.</span><span class="sxs-lookup"><span data-stu-id="5312c-181">e.</span></span> <span data-ttu-id="5312c-182">Skopiuj zawartość pliku pobranego certyfikatu, a następnie wklej go do **certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5312c-182">Copy the content of the downloaded certificate file and then paste it into the **Certificate** textbox.</span></span> 
 
    <span data-ttu-id="5312c-183">f.</span><span class="sxs-lookup"><span data-stu-id="5312c-183">f.</span></span> <span data-ttu-id="5312c-184">Kliknij przycisk **zapisać** ikony.</span><span class="sxs-lookup"><span data-stu-id="5312c-184">Click **Save** icon.</span></span>

> [!TIP]
> <span data-ttu-id="5312c-185">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="5312c-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5312c-186">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="5312c-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5312c-187">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5312c-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5312c-188">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5312c-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="5312c-189">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5312c-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="5312c-191">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5312c-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5312c-192">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5312c-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5312c-194">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="5312c-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5312c-196">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5312c-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5312c-198">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5312c-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5312c-200">a.</span><span class="sxs-lookup"><span data-stu-id="5312c-200">a.</span></span> <span data-ttu-id="5312c-201">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5312c-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5312c-202">b.</span><span class="sxs-lookup"><span data-stu-id="5312c-202">b.</span></span> <span data-ttu-id="5312c-203">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5312c-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5312c-204">c.</span><span class="sxs-lookup"><span data-stu-id="5312c-204">c.</span></span> <span data-ttu-id="5312c-205">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="5312c-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5312c-206">d.</span><span class="sxs-lookup"><span data-stu-id="5312c-206">d.</span></span> <span data-ttu-id="5312c-207">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5312c-207">Click **Create**.</span></span>
 
### <a name="creating-a-runmyprocess-test-user"></a><span data-ttu-id="5312c-208">Tworzenie użytkownika testowego RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="5312c-208">Creating a RunMyProcess test user</span></span>

<span data-ttu-id="5312c-209">Aby umożliwić użytkownikom zalogować się do RunMyProcess usługi Azure AD, musi być przygotowana do RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="5312c-209">In order to enable Azure AD users to log in to RunMyProcess, they must be provisioned into RunMyProcess.</span></span> <span data-ttu-id="5312c-210">W przypadku RunMyProcess Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="5312c-210">In the case of RunMyProcess, provisioning is a manual task.</span></span>

<span data-ttu-id="5312c-211">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5312c-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="5312c-212">Zaloguj się do witryny firmy RunMyProcess jako administrator.</span><span class="sxs-lookup"><span data-stu-id="5312c-212">Log in to your RunMyProcess company site as an administrator.</span></span>

2. <span data-ttu-id="5312c-213">Kliknij przycisk **konta** i wybierz **użytkowników** w panelu nawigacyjnym po lewej stronie, następnie kliknij przycisk **nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="5312c-213">Click **Account** and select **Users** in left navigation panel, then click **New User**.</span></span>
   
    <span data-ttu-id="5312c-214">![Nowy użytkownik](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="5312c-214">![New User](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "New User")</span></span>

3. <span data-ttu-id="5312c-215">W **ustawienia użytkownika** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5312c-215">In the **User Settings** section, perform the following steps:</span></span>
   
    <span data-ttu-id="5312c-216">![Profil](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "profilu")</span><span class="sxs-lookup"><span data-stu-id="5312c-216">![Profile](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profile")</span></span> 
  
    <span data-ttu-id="5312c-217">a.</span><span class="sxs-lookup"><span data-stu-id="5312c-217">a.</span></span> <span data-ttu-id="5312c-218">Typ **nazwa** i **E-mail** prawidłowy Azure konta AD ustanawiane do powiązanych pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="5312c-218">Type the **Name** and **E-mail** of a valid Azure AD account you want to provision into the related textboxes.</span></span> 

    <span data-ttu-id="5312c-219">b.</span><span class="sxs-lookup"><span data-stu-id="5312c-219">b.</span></span> <span data-ttu-id="5312c-220">Wybierz **IDE języka**, **języka**, i **profilu**.</span><span class="sxs-lookup"><span data-stu-id="5312c-220">Select an **IDE language**, **Language**, and **Profile**.</span></span> 

    <span data-ttu-id="5312c-221">c.</span><span class="sxs-lookup"><span data-stu-id="5312c-221">c.</span></span> <span data-ttu-id="5312c-222">Wybierz **Wyślij do mnie e-mail tworzenia konta**.</span><span class="sxs-lookup"><span data-stu-id="5312c-222">Select **Send account creation e-mail to me**.</span></span> 

    <span data-ttu-id="5312c-223">d.</span><span class="sxs-lookup"><span data-stu-id="5312c-223">d.</span></span> <span data-ttu-id="5312c-224">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="5312c-224">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="5312c-225">Możesz użyć innych RunMyProcess użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez RunMyProcess do świadczenia usługi Azure Active Directory kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5312c-225">You can use any other RunMyProcess user account creation tools or APIs provided by RunMyProcess to provision Azure Active Directory user accounts.</span></span> 
    > 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5312c-226">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5312c-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5312c-227">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="5312c-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RunMyProcess.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="5312c-229">**Aby przypisać Simona Britta RunMyProcess, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5312c-229">**To assign Britta Simon to RunMyProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="5312c-230">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5312c-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5312c-232">Na liście aplikacji zaznacz **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="5312c-232">In the applications list, select **RunMyProcess**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_app.png) 

3. <span data-ttu-id="5312c-234">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5312c-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="5312c-236">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5312c-236">Click **Add** button.</span></span> <span data-ttu-id="5312c-237">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5312c-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="5312c-239">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="5312c-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5312c-240">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5312c-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5312c-241">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5312c-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5312c-242">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5312c-242">Testing single sign-on</span></span>

<span data-ttu-id="5312c-243">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5312c-243">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="5312c-244">Po kliknięciu kafelka RunMyProcess w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="5312c-244">When you click the RunMyProcess tile in the Access Panel, you should get automatically signed-on to your RunMyProcess application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5312c-245">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5312c-245">Additional resources</span></span>

* [<span data-ttu-id="5312c-246">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5312c-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5312c-247">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5312c-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_203.png

