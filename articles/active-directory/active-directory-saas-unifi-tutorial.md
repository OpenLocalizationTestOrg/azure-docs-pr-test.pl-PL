---
title: 'Samouczek: Integracji Azure Active Directory z UNIFI | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i UNIFI."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1f49ee4-d2d4-4a82-9baf-0587ca1f20f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 09074d4628825909f0bb961c8001e53fb06cf7c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-unifi"></a><span data-ttu-id="9e427-103">Samouczek: Integracji Azure Active Directory z UNIFI</span><span class="sxs-lookup"><span data-stu-id="9e427-103">Tutorial: Azure Active Directory integration with UNIFI</span></span>

<span data-ttu-id="9e427-104">Z tego samouczka dowiesz się integrowanie UNIFI w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9e427-104">In this tutorial, you learn how to integrate UNIFI with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9e427-105">Integracja z usługą Azure AD UNIFI zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="9e427-105">Integrating UNIFI with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9e427-106">Można kontrolować w usłudze Azure AD, który ma dostęp do UNIFI</span><span class="sxs-lookup"><span data-stu-id="9e427-106">You can control in Azure AD who has access to UNIFI</span></span>
- <span data-ttu-id="9e427-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do UNIFI (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e427-107">You can enable your users to automatically get signed-on to UNIFI (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9e427-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9e427-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9e427-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9e427-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e427-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9e427-110">Prerequisites</span></span>

<span data-ttu-id="9e427-111">Aby skonfigurować integrację usługi Azure AD z UNIFI, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9e427-111">To configure Azure AD integration with UNIFI, you need the following items:</span></span>

- <span data-ttu-id="9e427-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e427-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9e427-113">UNIFI logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9e427-113">A UNIFI single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9e427-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="9e427-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9e427-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="9e427-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9e427-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="9e427-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9e427-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9e427-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9e427-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="9e427-118">Scenario description</span></span>
<span data-ttu-id="9e427-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="9e427-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9e427-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="9e427-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9e427-121">Dodawanie UNIFI z galerii</span><span class="sxs-lookup"><span data-stu-id="9e427-121">Adding UNIFI from the gallery</span></span>
2. <span data-ttu-id="9e427-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9e427-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-unifi-from-the-gallery"></a><span data-ttu-id="9e427-123">Dodawanie UNIFI z galerii</span><span class="sxs-lookup"><span data-stu-id="9e427-123">Adding UNIFI from the gallery</span></span>
<span data-ttu-id="9e427-124">Aby skonfigurować integrację usługi Azure AD UNIFI, należy dodać UNIFI z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="9e427-124">To configure the integration of UNIFI into Azure AD, you need to add UNIFI from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9e427-125">**Aby dodać UNIFI z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9e427-125">**To add UNIFI from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9e427-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9e427-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="9e427-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="9e427-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9e427-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9e427-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="9e427-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9e427-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="9e427-133">W polu wyszukiwania wpisz **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="9e427-133">In the search box, type **UNIFI**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_search.png)

5. <span data-ttu-id="9e427-135">W panelu wyników wybierz **UNIFI**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="9e427-135">In the results panel, select **UNIFI**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9e427-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9e427-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9e427-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z UNIFI w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="9e427-138">In this section, you configure and test Azure AD single sign-on with UNIFI based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9e427-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w UNIFI jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e427-139">For single sign-on to work, Azure AD needs to know what the counterpart user in UNIFI is to a user in Azure AD.</span></span> <span data-ttu-id="9e427-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w UNIFI musi się.</span><span class="sxs-lookup"><span data-stu-id="9e427-140">In other words, a link relationship between an Azure AD user and the related user in UNIFI needs to be established.</span></span>

<span data-ttu-id="9e427-141">W UNIFI, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="9e427-141">In UNIFI, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9e427-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z UNIFI, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="9e427-142">To configure and test Azure AD single sign-on with UNIFI, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9e427-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="9e427-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9e427-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9e427-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9e427-145">**[Użytkownik testowy tworzenie UNIFI](#creating-a-unifi-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta UNIFI połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9e427-145">**[Creating a UNIFI test user](#creating-a-unifi-test-user)** - to have a counterpart of Britta Simon in UNIFI that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9e427-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9e427-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9e427-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="9e427-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9e427-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9e427-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9e427-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji UNIFI.</span><span class="sxs-lookup"><span data-stu-id="9e427-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UNIFI application.</span></span>

<span data-ttu-id="9e427-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z UNIFI, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9e427-150">**To configure Azure AD single sign-on with UNIFI, perform the following steps:**</span></span>

1. <span data-ttu-id="9e427-151">W portalu Azure na **UNIFI** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="9e427-151">In the Azure portal, on the **UNIFI** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="9e427-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="9e427-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_samlbase.png)

3. <span data-ttu-id="9e427-155">Na **UNIFI domeny i adres URL** sekcji, jeśli chcesz skonfigurować aplikację w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="9e427-155">On the **UNIFI Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url1.png)

    <span data-ttu-id="9e427-157">W **identyfikator** tekstowym, wpisz wartość:`INVIEWlabs`</span><span class="sxs-lookup"><span data-stu-id="9e427-157">In the **Identifier** textbox, type the value: `INVIEWlabs`</span></span> 

4. <span data-ttu-id="9e427-158">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="9e427-158">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url2.png)

    <span data-ttu-id="9e427-160">W **adres URL logowania** tekstowym, wpisz adres URL:`https://app.discoverunifi.com/login`</span><span class="sxs-lookup"><span data-stu-id="9e427-160">In the **Sign-on URL** textbox, type the URL: `https://app.discoverunifi.com/login`</span></span>

5. <span data-ttu-id="9e427-161">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="9e427-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_certificate.png) 

6. <span data-ttu-id="9e427-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9e427-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-unifi-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="9e427-165">Na **konfiguracji UNIFI** , kliknij przycisk **skonfigurować UNIFI** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="9e427-165">On the **UNIFI Configuration** section, click **Configure UNIFI** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9e427-166">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="9e427-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_configure.png)

8. <span data-ttu-id="9e427-168">W oknie przeglądarki innej witryny sieci web, zaloguj się na Twojej **UNIFI** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="9e427-168">In a different web browser window, sign on to your **UNIFI** company site as administrator.</span></span>

9. <span data-ttu-id="9e427-169">Polecenie **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="9e427-169">Click on the **Users**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-unifi-tutorial/app1.png) 

10. <span data-ttu-id="9e427-171">Polecenie **Dodaj nowego dostawcę tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="9e427-171">Click on the **Add New Identity Provider**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-unifi-tutorial/app2.png)

11. <span data-ttu-id="9e427-173">W **Dodawanie dostawcy tożsamości** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9e427-173">In the **Add Identity Provider** section, perform the following steps:</span></span>   

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-unifi-tutorial/app3.png) 

    <span data-ttu-id="9e427-175">a.</span><span class="sxs-lookup"><span data-stu-id="9e427-175">a.</span></span> <span data-ttu-id="9e427-176">W **Nazwa dostawcy** tekstowym, wpisz nazwę dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="9e427-176">In the **Provider Name** textbox, type the name of the Identity Provider..</span></span>

    <span data-ttu-id="9e427-177">b.</span><span class="sxs-lookup"><span data-stu-id="9e427-177">b.</span></span> <span data-ttu-id="9e427-178">W **adres URL dostawcy** Wklej w pole tekstowe **SAML pojedynczy znak na adres URL usługi** wartość, która została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9e427-178">In the the **Provider URL** textbox paste the **SAML Single Sign-On Service URL** value, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9e427-179">c.</span><span class="sxs-lookup"><span data-stu-id="9e427-179">c.</span></span> <span data-ttu-id="9e427-180">Usuń certyfikat został już pobrany z portalu Azure w programie Notatnik Otwórz **---BEGIN CERTIFICATE---** i **---END CERTIFICATE---** tag, a następnie wklej zawartość pozostałych **certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9e427-180">Open the Certificate that you have downloaded from the Azure portal in notepad, remove the **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste the remaining content in the **Certificate** textbox.</span></span>

    <span data-ttu-id="9e427-181">d.</span><span class="sxs-lookup"><span data-stu-id="9e427-181">d.</span></span> <span data-ttu-id="9e427-182">Wybierz **jest domyślny dostawca** wyboru.</span><span class="sxs-lookup"><span data-stu-id="9e427-182">Select the **is Default Provider** checkbox.</span></span>

> [!TIP]
> <span data-ttu-id="9e427-183">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="9e427-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9e427-184">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="9e427-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9e427-185">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9e427-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9e427-186">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e427-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="9e427-187">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9e427-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="9e427-189">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9e427-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9e427-190">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9e427-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9e427-192">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="9e427-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9e427-194">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9e427-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9e427-196">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9e427-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9e427-198">a.</span><span class="sxs-lookup"><span data-stu-id="9e427-198">a.</span></span> <span data-ttu-id="9e427-199">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9e427-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9e427-200">b.</span><span class="sxs-lookup"><span data-stu-id="9e427-200">b.</span></span> <span data-ttu-id="9e427-201">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9e427-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9e427-202">c.</span><span class="sxs-lookup"><span data-stu-id="9e427-202">c.</span></span> <span data-ttu-id="9e427-203">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="9e427-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9e427-204">d.</span><span class="sxs-lookup"><span data-stu-id="9e427-204">d.</span></span> <span data-ttu-id="9e427-205">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9e427-205">Click **Create**.</span></span>
 
### <a name="creating-a-unifi-test-user"></a><span data-ttu-id="9e427-206">Tworzenie użytkownika testowego UNIFI</span><span class="sxs-lookup"><span data-stu-id="9e427-206">Creating a UNIFI test user</span></span>

<span data-ttu-id="9e427-207">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9e427-207">In this section, you create a user called Britta Simon.</span></span> <span data-ttu-id="9e427-208">**UNIFI** obsługę użytkowników, więc nie są wymagane żadne czynności ręcznych.</span><span class="sxs-lookup"><span data-stu-id="9e427-208">**UNIFI** supports automatic user provisioning so no manual steps are required.</span></span> <span data-ttu-id="9e427-209">Użytkownicy są tworzone automatycznie po pomyślnym uwierzytelnieniu z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e427-209">Users are created automatically after successful authentication from the Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9e427-210">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e427-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9e427-211">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu UNIFI.</span><span class="sxs-lookup"><span data-stu-id="9e427-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UNIFI.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="9e427-213">**Aby przypisać Simona Britta UNIFI, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9e427-213">**To assign Britta Simon to UNIFI, perform the following steps:**</span></span>

1. <span data-ttu-id="9e427-214">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9e427-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="9e427-216">Na liście aplikacji zaznacz **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="9e427-216">In the applications list, select **UNIFI**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_app.png) 

3. <span data-ttu-id="9e427-218">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="9e427-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="9e427-220">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9e427-220">Click **Add** button.</span></span> <span data-ttu-id="9e427-221">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9e427-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="9e427-223">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="9e427-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9e427-224">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9e427-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9e427-225">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9e427-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9e427-226">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9e427-226">Testing single sign-on</span></span>

<span data-ttu-id="9e427-227">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9e427-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9e427-228">Po kliknięciu kafelka UNIFI w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji UNIFI.</span><span class="sxs-lookup"><span data-stu-id="9e427-228">When you click the UNIFI tile in the Access Panel, you should get automatically signed-on to your UNIFI application.</span></span>
<span data-ttu-id="9e427-229">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9e427-229">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9e427-230">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="9e427-230">Additional resources</span></span>

* [<span data-ttu-id="9e427-231">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9e427-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9e427-232">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9e427-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_203.png

